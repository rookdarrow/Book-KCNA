---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/deployment/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["deployment", "deployment-strategy", "rolling-update", "recreate-strategy", "maxsurge", "maxunavailable", "minreadyseconds", "readiness-gated-rollout", "revision-history-limit", "stuck-rollout", "selector-template-agreement", "replicas", "pause-rollout"]
---
# Deployment — spec field reference and status (kubernetes.io/docs/concepts/workloads/controllers/deployment/)

Supplements `k8s-docs-deployment-2026-08-23.md`, which covers the Deployment overview, strategy types, rollback, revisions and pause/resume. This snapshot carries the field-level detail that snapshot stops short of. Secondary corroboration for the field descriptions is the API reference at https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/deployment-v1/ , quoted in the final section below.

## Deployment status

A Deployment enters various states during its lifecycle. It can be progressing while rolling out a new ReplicaSet, it can be complete, or it can fail to progress.

### Progressing Deployment

Kubernetes marks a Deployment as progressing when one of the following tasks is performed: The Deployment creates a new ReplicaSet. The Deployment is scaling up its newest ReplicaSet. The Deployment is scaling down its older ReplicaSet(s). New Pods become ready or available (ready for at least MinReadySeconds).

### Complete Deployment

Kubernetes marks a Deployment as complete when it has the following characteristics: All of the replicas associated with the Deployment have been updated to the latest version you've specified, meaning any updates you've requested have been completed. All of the replicas associated with the Deployment are available. No old replicas for the Deployment are running.

### Failed Deployment

Your Deployment may get stuck trying to deploy its newest ReplicaSet without ever completing. This can occur due to some of the following factors: Insufficient quota. Readiness probe failures. Image pull errors. Insufficient permissions. Limit ranges. Application runtime misconfiguration.

## Writing a Deployment Spec

### .spec.selector

`.spec.selector` is a required field that specifies a label selector for the Pods targeted by this Deployment. `.spec.selector` must match `.spec.template.metadata.labels`, or it will be rejected by the API.

### .spec.replicas

`.spec.replicas` is an optional field that specifies the number of desired Pods. It defaults to 1.

### Max Unavailable

`.spec.strategy.rollingUpdate.maxUnavailable` is an optional field that specifies the maximum number of Pods that can be unavailable during the update process. The value can be an absolute number (for example, 5) or a percentage of desired Pods (for example, 10%). The absolute number is calculated from percentage by rounding down. The value cannot be 0 if `.spec.strategy.rollingUpdate.maxSurge` is 0. The default value is 25%.

### Max Surge

`.spec.strategy.rollingUpdate.maxSurge` is an optional field that specifies the maximum number of Pods that can be created over the desired number of Pods. The value can be an absolute number (for example, 5) or a percentage of desired Pods (for example, 10%). The value cannot be 0 if `maxUnavailable` is 0. The absolute number is calculated from the percentage by rounding up. The default value is 25%.

### .spec.progressDeadlineSeconds

`.spec.progressDeadlineSeconds` is an optional field that specifies the number of seconds you want to wait for your Deployment to progress before the system reports back that the Deployment has failed progressing - surfaced as a condition with `type: Progressing`, `status: "False"`. and `reason: ProgressDeadlineExceeded` in the status of the resource. The Deployment controller will keep retrying the Deployment. This defaults to 600.

### .spec.minReadySeconds

`.spec.minReadySeconds` is an optional field that specifies the minimum number of seconds for which a newly created Pod should be ready without any of its containers crashing, for it to be considered available. This defaults to 0 (the Pod will be considered available as soon as it is ready).

### .spec.revisionHistoryLimit

`.spec.revisionHistoryLimit` is an optional field that specifies the number of old ReplicaSets to retain to allow rollback. These old ReplicaSets consume resources in `etcd` and crowd the output of `kubectl get rs`. By default, 10 old ReplicaSets will be kept. More specifically, setting this field to zero means that all old ReplicaSets with 0 replicas will be cleaned up. In this case, a new Deployment rollout cannot be undone, since its revision history is cleaned up.

## Proportional scaling

RollingUpdate Deployments support running multiple versions of an application at the same time. When you or an autoscaler scales a RollingUpdate Deployment that is in the middle of a rollout (either in progress or paused), the Deployment controller balances the additional replicas in the existing active ReplicaSets (ReplicaSets with Pods) in order to mitigate risk. This is called proportional scaling.

## API reference — DeploymentSpec field descriptions

From https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/deployment-v1/ :

- **replicas**: "Number of desired pods. This is a pointer to distinguish between explicit zero and not specified. Defaults to 1."
- **selector**: "Label selector for pods. Existing ReplicaSets whose pods are selected by this will be the ones affected by this deployment. It must match the pod template's labels."
- **template**: "Template describes the pods that will be created. The only allowed template.spec.restartPolicy value is \"Always\"."
- **strategy**: "The deployment strategy to use to replace existing pods with new ones."
- **strategy.type**: "Type of deployment. Can be \"Recreate\" or \"RollingUpdate\". Default is RollingUpdate. Possible enum values: - `\"Recreate\"` Kill all existing pods before creating new ones. - `\"RollingUpdate\"` Replace the old ReplicaSets by new one using rolling update i.e gradually scale down the old ReplicaSets and scale up the new one."
- **strategy.rollingUpdate.maxSurge**: "The maximum number of pods that can be scheduled above the desired number of pods. Value can be an absolute number (ex: 5) or a percentage of desired pods (ex: 10%). This can not be 0 if MaxUnavailable is 0. Absolute number is calculated from percentage by rounding up. Defaults to 25%. Example: when this is set to 30%, the new ReplicaSet can be scaled up immediately when the rolling update starts, such that the total number of old and new pods do not exceed 130% of desired pods. Once old pods have been killed, new ReplicaSet can be scaled up further, ensuring that total number of pods running at any time during the update is at most 130% of desired pods."
- **strategy.rollingUpdate.maxUnavailable**: "The maximum number of pods that can be unavailable during the update. Value can be an absolute number (ex: 5) or a percentage of desired pods (ex: 10%). Absolute number is calculated from percentage by rounding down. This can not be 0 if MaxSurge is 0. Defaults to 25%. Example: when this is set to 30%, the old ReplicaSet can be scaled down to 70% of desired pods immediately when the rolling update starts. Once new pods are ready, old ReplicaSet can be scaled down further, followed by scaling up the new ReplicaSet, ensuring that the total number of pods available at all times during the update is at least 70% of desired pods."
- **minReadySeconds**: "Minimum number of seconds for which a newly created pod should be ready without any of its container crashing, for it to be considered available. Defaults to 0 (pod will be considered available as soon as it is ready)"
- **revisionHistoryLimit**: "The number of old ReplicaSets to retain to allow rollback. This is a pointer to distinguish between explicit zero and not specified. Defaults to 10."
- **progressDeadlineSeconds**: "The maximum time in seconds for a deployment to make progress before it is considered to be failed. The deployment controller will continue to process failed deployments and a condition with a ProgressDeadlineExceeded reason will be surfaced in the deployment status. Note that progress will not be estimated during the time a deployment is paused. Defaults to 600s."
- **paused**: "Indicates that the deployment is paused."

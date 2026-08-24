Now I have the exact contract: Stage 2 can't write files — it embeds snapshots as fenced blocks in stdout and the orchestrator harvests them. Emitting the manifest in that format.

# Research Manifest — KCNA Chapter 6

**Chapter:** 6 — *Fleets, Not Vessels* · **Objective:** D1.1 · **Stage 2 run:** 2026-08-24T07:57:36-0400

All five research gaps the outline flagged as **BLOCKING** in § Open questions #2 are now **CLOSED**, plus open questions #5, #6 and #7. Ten new snapshots below. One material factual correction to the outline is raised in § Notes — **read note 1 before drafting §4.**

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-replicaset-2026-08-24.md` | Kubernetes project | D1.1 | replicaset, replicas, pod-template, label-selector, selector-template-agreement, owner-reference, controller-adoption, orphaning, cascading-deletion, manual-horizontal-scaling |
| `k8s-docs-statefulset-2026-08-24.md` | Kubernetes project | D1.1 | statefulset, stable-pod-identity, pod-interchangeability |
| `k8s-docs-daemonset-2026-08-24.md` | Kubernetes project | D1.1 | daemonset, node-local-facility, selector-template-agreement |
| `k8s-docs-job-2026-08-24.md` | Kubernetes project | D1.1 | job, run-to-completion |
| `k8s-docs-cronjob-2026-08-24.md` | Kubernetes project | D1.1 | cronjob, cronjob-schedule, run-to-completion |
| `k8s-docs-garbage-collection-2026-08-24.md` | Kubernetes project | D1.1 | owner-reference, cascading-deletion, orphaning |
| `k8s-docs-deployment-spec-fields-2026-08-24.md` | Kubernetes project | D1.1 | maxsurge, maxunavailable, minreadyseconds, readiness-gated-rollout, revision-history-limit, stuck-rollout, deployment-strategy |
| `k8s-docs-replicationcontroller-2026-08-24.md` | Kubernetes project | D1.1 | replicationcontroller-legacy |
| `k8s-docs-hpa-2026-08-24.md` | Kubernetes project | D1.1 | horizontalpodautoscaler, horizontal-scaling, vertical-scaling |
| `k8s-docs-kubectl-rollout-2026-08-24.md` | Kubernetes project | D1.1 | kubectl-rollout-status, kubectl-rollout-history, kubectl-rollout-undo, kubectl-rollout-pause, kubectl-rollout-resume |

### Already cached and verified adequate (no re-fetch needed)

`k8s-docs-workloads-2026-08-23.md` · `k8s-docs-deployment-2026-08-23.md` · `k8s-docs-controllers-2026-08-23.md` · `k8s-docs-autoscaling-2026-08-23.md` · `k8s-docs-labels-selectors-2026-08-23.md` · `k8s-docs-objects-2026-08-23.md` · `k8s-docs-pod-lifecycle-2026-08-23.md` · `k8s-docs-kubectl-overview-2026-08-23.md` · `k8s-docs-custom-resources-2026-08-23.md` · `k8s-docs-operator-pattern-2026-08-23.md` · `k8s-docs-extending-kubernetes-2026-08-23.md`

I read the custom-resources and operator-pattern snapshots directly: **§8 is fully sourced as the outline claimed.** Every §8 beat — resource-as-endpoint, dynamic registration, identical kubectl access, "on their own… store and retrieve structured data", CRD defines name and schema, the operator pattern definition, the automation examples, and the controller running outside the control plane as a Deployment — is present verbatim. No §8 fetch was required.

---

## Snapshots

### A1 · `k8s-docs-replicaset-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["replicaset", "desired-replica-count", "replicas", "pod-template", "label-selector", "selector-template-agreement", "owner-reference", "controller-adoption", "orphaning", "cascading-deletion", "manual-horizontal-scaling", "horizontalpodautoscaler", "replicationcontroller-legacy", "workload-resource"]
---
# ReplicaSet (kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

## Purpose

A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. Usually, you define a Deployment and let that Deployment manage ReplicaSets automatically.

A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

## How a ReplicaSet works

A ReplicaSet is defined with fields, including a selector that specifies how to identify Pods it can acquire, a number of replicas indicating how many Pods it should be maintaining, and a pod template specifying the data of new Pods it should create to meet the number of replicas criteria. A ReplicaSet then fulfills its purpose by creating and deleting Pods as needed to reach the desired number. When a ReplicaSet needs to create new Pods, it uses its Pod template.

A ReplicaSet is linked to its Pods via the Pods' `metadata.ownerReferences` field, which specifies what resource the current object is owned by. All Pods acquired by a ReplicaSet have their owning ReplicaSet's identifying information within their ownerReferences field. It's through this link that the ReplicaSet knows of the state of the Pods it is maintaining and plans accordingly.

A ReplicaSet identifies new Pods to acquire by using its selector. If there is a Pod that has no OwnerReference or the OwnerReference is not a Controller and it matches a ReplicaSet's selector, it will be immediately acquired by said ReplicaSet.

## When to use a ReplicaSet

A ReplicaSet ensures that a specified number of pod replicas are running at any given time. However, a Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features. Therefore, we recommend using Deployments instead of directly using ReplicaSets, unless you require custom update orchestration or don't require updates at all.

This actually means that you may never need to manipulate ReplicaSet objects: use a Deployment instead, and define your application in the spec section.

## Pod Template

The `.spec.template` is a pod template which is also required to have labels in place. In our `frontend.yaml` example we had one label: `tier: frontend`. Be careful not to overlap with the selectors of other controllers, lest they try to adopt this Pod.

For the template's restart policy field, `.spec.template.spec.restartPolicy`, the only allowed value is `Always`, which is the default.

## Pod Selector

The `.spec.selector` field is a label selector. As discussed earlier these are the labels used to identify potential Pods to acquire.

In the ReplicaSet, `.spec.template.metadata.labels` must match `spec.selector`, or it will be rejected by the API.

For 2 ReplicaSets specifying the same `.spec.selector` but different `.spec.template.metadata.labels` and `.spec.template.spec` fields, each ReplicaSet ignores the Pods created by the other ReplicaSet.

## Replicas

You can specify how many Pods should run concurrently by setting `.spec.replicas`. The ReplicaSet will create/delete its Pods to match this number.

If you do not specify `.spec.replicas`, then it defaults to 1.

## Non-Template Pod acquisitions

While you can create bare Pods with no problems, it is strongly recommended to make sure that the bare Pods do not have labels which match the selector of one of your ReplicaSets. The reason for this is because a ReplicaSet is not limited to owning Pods specified by its template -- it can acquire other Pods in the manner specified in the previous sections.

As those Pods do not have a Controller (or any object) as their owner reference and match the selector of the frontend ReplicaSet, they will immediately be acquired by it.

Suppose you create the Pods after the frontend ReplicaSet has been deployed and has set up its initial Pod replicas to fulfill its replica count requirement: the new Pods will be acquired by the ReplicaSet, and then immediately terminated as the ReplicaSet would be over its desired count.

If you create the Pods first, and then create the ReplicaSet: you shall see that the ReplicaSet has acquired the Pods and has only created new ones according to its spec until the number of its new Pods and the original matches its desired count.

In this manner, a ReplicaSet can own a non-homogeneous set of Pods.

## Working with ReplicaSets

### Deleting a ReplicaSet and its Pods

To delete a ReplicaSet and all of its Pods, use `kubectl delete`. The Garbage collector automatically deletes all of the dependent Pods by default.

### Deleting just a ReplicaSet

You can delete a ReplicaSet without affecting any of its Pods using `kubectl delete` with the `--cascade=orphan` option.

Once the original is deleted, you can create a new ReplicaSet to replace it. As long as the old and new `.spec.selector` are the same, then the new one will adopt the old Pods.

### Isolating Pods from a ReplicaSet

You can remove Pods from a ReplicaSet by changing their labels. This technique may be used to remove Pods from service for debugging, data recovery, etc. Pods that are removed in this way will be replaced automatically (assuming that the number of replicas is not also changed).

### Scaling a ReplicaSet

A ReplicaSet can be easily scaled up or down by simply updating the `.spec.replicas` field. The ReplicaSet controller ensures that a desired number of Pods with a matching label selector are available and operational.

### ReplicaSet as a Horizontal Pod Autoscaler Target

A ReplicaSet can also be a target for Horizontal Pod Autoscalers (HPA). That is, a ReplicaSet can be auto-scaled by an HPA.

## Alternatives to ReplicaSet

### Deployment (recommended)

`Deployment` is an object which can own ReplicaSets and update them and their Pods via declarative, server-side rolling updates.

When you use Deployments you don't have to worry about managing the ReplicaSets that they create. Deployments own and manage their ReplicaSets. As such, it is recommended to use Deployments when you want ReplicaSets.

### Bare Pods

Unlike the case where a user directly created Pods, a ReplicaSet replaces Pods that are deleted or terminated for any reason, such as in the case of node failure or disruptive node maintenance, such as a kernel upgrade.

A ReplicaSet delegates local container restarts to some agent on the node such as Kubelet.

### Job

Use a `Job` instead of a ReplicaSet for Pods that are expected to terminate on their own (that is, batch jobs).

### DaemonSet

Use a `DaemonSet` instead of a ReplicaSet for Pods that provide a machine-level function, such as machine monitoring or machine logging.

### ReplicationController

ReplicaSets are the successors to ReplicationControllers. The two serve the same purpose, and behave similarly, except that a ReplicationController does not support set-based selector requirements as described in the labels user guide.

As such, ReplicaSets are preferred over ReplicationControllers.
```

### A2 · `k8s-docs-statefulset-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["statefulset", "stable-pod-identity", "pod-interchangeability", "workload-resource", "pod-template", "rolling-update"]
---
# StatefulSets (kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

## What a StatefulSet is

A StatefulSet runs a group of Pods, and maintains a sticky identity for each of those Pods. This is useful for managing applications that need persistent storage or a stable, unique network identity.

StatefulSet is the workload API object used to manage stateful applications.

Manages the deployment and scaling of a set of Pods, *and provides guarantees about the ordering and uniqueness* of these Pods.

Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec. Unlike a Deployment, a StatefulSet maintains a sticky identity for each of its Pods. These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling.

## Using StatefulSets

StatefulSets are valuable for applications that require one or more of the following:

- Stable, unique network identifiers.
- Stable, persistent storage.
- Ordered, graceful deployment and scaling.
- Ordered, automated rolling updates.

## Limitations

- The storage for a given Pod must either be provisioned by a PersistentVolume Provisioner based on the requested *storage class*, or pre-provisioned by an admin.
- Deleting and/or scaling a StatefulSet down will *not* delete the volumes associated with the StatefulSet. This is done to ensure data safety, which is generally more valuable than an automatic purge of all related StatefulSet resources.
- StatefulSets currently require a Headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service.
- StatefulSets do not provide any guarantees on the termination of pods when a StatefulSet is deleted. To achieve ordered and graceful termination of the pods in the StatefulSet, it is possible to scale the StatefulSet down to 0 prior to deletion.
- When using Rolling Updates with the default Pod Management Policy (`OrderedReady`), it's possible to get into a broken state that requires manual intervention to repair.

## Pod Identity

StatefulSet Pods have a unique identity that consists of an ordinal, a stable network identity, and stable storage. The identity sticks to the Pod, regardless of which node it's (re)scheduled on.

### Ordinal Index

For a StatefulSet with N replicas, each Pod in the StatefulSet will be assigned an integer ordinal, that is unique over the Set. By default, pods will be assigned ordinals from 0 up through N-1. The StatefulSet controller will also add a pod label with this index: `apps.kubernetes.io/pod-index`.

### Stable Network ID

Each Pod in a StatefulSet derives its hostname from the name of the StatefulSet and the ordinal of the Pod. The pattern for the constructed hostname is `$(statefulset name)-$(ordinal)`. The example above will create three Pods named `web-0,web-1,web-2`. A StatefulSet can use a Headless Service to control the domain of its Pods. The domain managed by this Service takes the form: `$(service name).$(namespace).svc.cluster.local`, where "cluster.local" is the cluster domain. As each Pod is created, it gets a matching DNS subdomain, taking the form: `$(podname).$(governing service domain)`, where the governing service is defined by the `serviceName` field on the StatefulSet.

Depending on how DNS is configured in your cluster, you may not be able to look up the DNS name for a newly-run Pod immediately. This behavior can occur when other clients in the cluster have already sent queries for the hostname of the Pod before it was created. Negative caching (normal in DNS) means that the results of previous failed lookups are remembered and reused, even after the Pod is running, for at least a few seconds.

As mentioned in the limitations section, you are responsible for creating the Headless Service responsible for the network identity of the pods.

### Stable Storage

For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim. In the nginx example above, each Pod receives a single PersistentVolumeClaim named `www`. This PersistentVolumeClaim will either be provisioned by a PersistentVolume Provisioner based on the StorageClass named `my-storage-class` or it will be pre-provisioned by an administrator. The same PersistentVolumeClaim will be bound to a Pod throughout its lifecycle.

When a Pod is (re)scheduled onto a (different) Node, its volumeMounts mount the PersistentVolumeClaim(s) associated with its PersistentVolume(s). Note that, the PersistentVolumeClaim(s) associated with the Pod's PersistentVolume(s) are not deleted when the Pod, or the StatefulSet is deleted. This must be done manually.

### Pod Name Label

FEATURE STATE: Kubernetes v1.33 [stable]

When a StatefulSet controller creates a Pod, it adds a label, `statefulset.kubernetes.io/pod-name`, that is set to the name of the Pod. This label allows you to attach a Service to a specific Pod in the StatefulSet.

## Deployment and Scaling Guarantees

- For a StatefulSet with N replicas, when Pods are being deployed, they are created sequentially, in order from {0..N-1}.
- When Pods are being deleted, they are terminated in reverse order, from {N-1..0}.
- Before a scaling operation is applied to a Pod, all of its predecessors must be Running and Ready.
- Before a Pod is terminated, all of its successors must be completely shut down.

The StatefulSet should not specify a pod.Spec.TerminationGracePeriodSeconds of 0. This practice is unsafe and strongly discouraged.

In the nginx example above, if you tried to scale the StatefulSet down from 3 replicas to 1 replica, the StatefulSet would not delete `web-0`. The StatefulSet controller would wait until `web-2` was Running and Ready, prior to deleting `web-1`. If, after `web-1` is deleted, `web-2` becomes not Ready, the StatefulSet controller would wait until `web-2` is Running and Ready again, before attempting any further deletions.

### Pod Management Policies

StatefulSet allows you to relax its ordering guarantees while maintaining its uniqueness guarantees via the `.spec.podManagementPolicy` field.

#### OrderedReady Pod Management

`OrderedReady` pod management is the default for StatefulSets. It implements the behavior described above.

#### Parallel Pod Management

`Parallel` pod management tells the StatefulSet controller to launch or terminate all Pods in parallel, and not to wait for Pods to become Running and Ready or completely terminated prior to launching or terminating other Pods. This option only affects the behavior for scaling operations. Updates are not affected.

## Update strategies

StatefulSet's `.spec.updateStrategy` field allows you to configure and disable automated rolling updates for containers, labels, resource request/limits, and annotations for the Pods in a StatefulSet.

### OnDelete

`OnDelete` update strategy implements the legacy (1.6 and prior) behavior. With this strategy, the StatefulSet controller will not automatically update the Pods in a StatefulSet. Users must manually delete Pods to cause the controller to create new Pods that reflect modifications made to the StatefulSet's `.spec.template`.

### RollingUpdate

The `RollingUpdate` update strategy implements automated, rolling update for the Pods in a StatefulSet. When `.spec.updateStrategy.type` is not specified, `RollingUpdate` is the default strategy. The StatefulSet controller will delete and recreate each Pod in the StatefulSet. It will proceed in the same order as Pod termination (from the largest ordinal to the smallest), updating each Pod one at a time.
```

### A3 · `k8s-docs-daemonset-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["daemonset", "node-local-facility", "workload-resource", "pod-template", "label-selector", "selector-template-agreement", "orphaning"]
---
# DaemonSet (kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

## What a DaemonSet is

A *DaemonSet* ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.

## Typical uses

Some typical uses of a DaemonSet are:

- running a cluster storage daemon on every node
- running a logs collection daemon on every node
- running a node monitoring daemon on every node

## Required Fields

As with all other Kubernetes config, a DaemonSet needs `apiVersion`, `kind`, and `metadata` fields.

The name of a DaemonSet object must be a valid DNS subdomain name.

A DaemonSet also needs a `.spec` section.

### Pod Template

The `.spec.template` is one of the required fields in `.spec`.

The `.spec.template` is a pod template. It has exactly the same schema as a Pod, except it is nested and does not have an `apiVersion` or `kind`.

In addition to required fields for a Pod, a Pod template in a DaemonSet has to specify appropriate labels (see pod selector).

A Pod Template in a DaemonSet must have a `RestartPolicy` equal to `Always`, or be unspecified, which defaults to `Always`.

### Pod Selector

The `.spec.selector` field is a pod selector. It works the same as the `.spec.selector` of a Job.

You must specify a pod selector that matches the labels of the `.spec.template`. Also, once a DaemonSet is created, its `.spec.selector` can not be mutated. Mutating the pod selector can lead to the unintentional orphaning of Pods, and it was found to be confusing to users.

The `.spec.selector` is an object consisting of two fields:

- `matchLabels` - works the same as the `.spec.selector` of a ReplicationController.
- `matchExpressions` - allows to build more sophisticated selectors by specifying key, list of values and an operator that relates the key and values.

When the two are specified the result is ANDed.

The `.spec.selector` must match the `.spec.template.metadata.labels`. Config with these two not matching will be rejected by the API.

## Running Pods on select Nodes

If you specify a `.spec.template.spec.nodeSelector`, then the DaemonSet controller will create Pods on nodes which match that node selector. Likewise if you specify a `.spec.template.spec.affinity`, then DaemonSet controller will create Pods on nodes which match that node affinity. If you do not specify either, then the DaemonSet controller will create Pods on all nodes.

## How Daemon Pods are scheduled

A DaemonSet can be used to ensure that all eligible nodes run a copy of a Pod. The DaemonSet controller creates a Pod for each eligible node and adds the `spec.affinity.nodeAffinity` field of the Pod to match the target host. After the Pod is created, the default scheduler typically takes over and then binds the Pod to the target host by setting the `.spec.nodeName` field. If the new Pod cannot fit on the node, the default scheduler may preempt (evict) some of the existing Pods based on the priority of the new Pod.

The user can specify a different scheduler for the Pods of the DaemonSet, by setting the `.spec.template.spec.schedulerName` field of the DaemonSet.

The original node affinity specified at the `.spec.template.spec.affinity.nodeAffinity` field (if specified) is taken into consideration by the DaemonSet controller when evaluating the eligible nodes, but is replaced on the created Pod with the node affinity that matches the name of the eligible node.

### Taints and tolerations

The DaemonSet controller automatically adds a set of tolerations to DaemonSet Pods:

| Toleration key | Effect | Details |
|---|---|---|
| `node.kubernetes.io/not-ready` | `NoExecute` | DaemonSet Pods can be scheduled onto nodes that are not healthy or ready to accept Pods. Any DaemonSet Pods running on such nodes will not be evicted. |
| `node.kubernetes.io/unreachable` | `NoExecute` | DaemonSet Pods can be scheduled onto nodes that are unreachable from the node controller. Any DaemonSet Pods running on such nodes will not be evicted. |
| `node.kubernetes.io/disk-pressure` | `NoSchedule` | DaemonSet Pods can be scheduled onto nodes with disk pressure issues. |
| `node.kubernetes.io/memory-pressure` | `NoSchedule` | DaemonSet Pods can be scheduled onto nodes with memory pressure issues. |
| `node.kubernetes.io/pid-pressure` | `NoSchedule` | DaemonSet Pods can be scheduled onto nodes with process pressure issues. |
| `node.kubernetes.io/unschedulable` | `NoSchedule` | DaemonSet Pods can be scheduled onto nodes that are unschedulable. |
| `node.kubernetes.io/network-unavailable` | `NoSchedule` | Only added for DaemonSet Pods that request host networking, i.e., Pods having `spec.hostNetwork: true`. Such DaemonSet Pods can be scheduled onto nodes with unavailable network. |

You can add your own tolerations to the Pods of a DaemonSet as well, by defining these in the Pod template of the DaemonSet.

Because the DaemonSet controller sets the `node.kubernetes.io/unschedulable:NoSchedule` toleration automatically, Kubernetes can run DaemonSet Pods on nodes that are marked as *unschedulable*.

---

NOT IN THIS SNAPSHOT: the "Alternatives to DaemonSet" section was truncated by the fetcher and is not cached. Also note that no fetched sentence states explicitly that a DaemonSet has no `replicas` field; the Pod count follows from node eligibility ("The DaemonSet controller creates a Pod for each eligible node"). See research-manifest Gaps, G-6A.
```

### A4 · `k8s-docs-job-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/job/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["job", "run-to-completion", "workload-resource"]
---
# Jobs (kubernetes.io/docs/concepts/workloads/controllers/job/)

## What a Job is

Jobs represent one-off tasks that run to completion and then stop.

A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. As pods successfully complete, the Job tracks the successful completions. When a specified number of successful completions is reached, the task (ie, Job) is complete. Deleting a Job will clean up the Pods it created. Suspending a Job will delete its active Pods until the Job is resumed again.

A simple case is to create one Job object in order to reliably run one Pod to completion. The Job object will start a new Pod if the first Pod fails or is deleted (for example due to a node hardware failure or a node reboot).

You can also use a Job to run multiple Pods in parallel.

## Completion mode

NonIndexed (default): the Job is considered complete when there have been `.spec.completions` successfully completed Pods.

Indexed: the Pods of a Job get an associated completion index from 0 to `.spec.completions-1`. The Job is considered complete when there is one successfully completed Pod for each index.

## Parallel execution for Jobs

There are three main types of task suitable to run as a Job:

1. Non-parallel Jobs
   - normally, only one Pod is started, unless the Pod fails.
   - the Job is complete as soon as its Pod terminates successfully.
2. Parallel Jobs with a *fixed completion count*:
   - specify a non-zero positive value for `.spec.completions`.
   - the Job represents the overall task, and is complete when there are `.spec.completions` successful Pods.
3. Parallel Jobs with a *work queue*:
   - do not specify `.spec.completions`, default to `.spec.parallelism`.
   - the Pods must coordinate amongst themselves or an external service to determine what each should work on.

The `.spec.parallelism` and `.spec.completions` fields define the parallelism and completion count for a Job.

Controlling parallelism: the requested parallelism (`.spec.parallelism`) can be set to any non-negative value. If it is unspecified, it defaults to 1.

## Handling Pod and container failures

Only a `RestartPolicy` equal to `Never` or `OnFailure` is allowed.

### Pod backoff failure policy

The `.spec.backoffLimit` is set by default to 6, unless the backoff limit per index (only Indexed Job) is specified.

## Job termination and cleanup

Another way to terminate a Job is by setting an active deadline. Do this by setting the `.spec.activeDeadlineSeconds` field of the Job to a number of seconds.

Note that a Job's `.spec.activeDeadlineSeconds` takes precedence over its `.spec.backoffLimit`.

## TTL mechanism for finished Jobs

Another way to clean up finished Jobs (either `Complete` or `Failed`) automatically is to use a TTL mechanism provided by a TTL controller for finished resources, by specifying the `.spec.ttlSecondsAfterFinished` field of the Job.

## Job patterns

The documented Job patterns (section headings, listed here without their prose):

- Queue with Pod Per Work Item
- Queue with Variable Pod Count
- Indexed Job with Static Work Assignment
- Job with Pod-to-Pod Communication
- Job Template Expansion

---

TRANSCRIPTION NOTE: the Job page is long and the fetcher truncated it on the first pass. The text above was recovered from the docs' raw markdown source (github.com/kubernetes/website, content/en/docs/concepts/workloads/controllers/job.md), which is the same content kubernetes.io renders. The "Job patterns" entries above are the source's own section headings; their prose bodies are NOT cached here. A first-pass fetch of the rendered page reported `.spec.backoffLimit` defaulting to 4; the raw source states 6. Treat 6 as correct and see research-manifest Notes, note 4.
```

### A5 · `k8s-docs-cronjob-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["cronjob", "cronjob-schedule", "job", "run-to-completion", "workload-resource"]
---
# CronJob (kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)

## What a CronJob is

A *CronJob* creates Jobs on a repeating schedule.

CronJob is meant for performing regular scheduled actions such as backups, report generation, and so on. One CronJob object is like one line of a *crontab* (cron table) file on a Unix system. It runs a Job periodically on a given schedule, written in Cron format.

## Job creation and idempotency

A CronJob creates a Job object approximately once per execution time of its schedule. The scheduling is approximate because there are certain circumstances where two Jobs might be created, or no Job might be created. Kubernetes tries to avoid those situations, but does not completely prevent them. Therefore, the Jobs that you define should be *idempotent*.

## Cron schedule syntax

The `.spec.schedule` field is required. The value of that field follows the Cron syntax:

    # ┌───────────── minute (0 - 59)
    # │ ┌───────────── hour (0 - 23)
    # │ │ ┌───────────── day of the month (1 - 31)
    # │ │ │ ┌───────────── month (1 - 12)
    # │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday)
    # │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
    # │ │ │ │ │
    # │ │ │ │ │
    # * * * * *

For example, `0 3 * * 1` means this task is scheduled to run weekly on a Monday at 3 AM.

Note: A question mark (`?`) in the schedule has the same meaning as an asterisk `*`, that is, it stands for any of available value for a given field.

### Time zones

You can specify a time zone for a CronJob by setting `.spec.timeZone` to the name of a valid time zone. For example, setting `.spec.timeZone: "Etc/UTC"` instructs Kubernetes to interpret the schedule relative to Coordinated Universal Time.

## Job template

The `.spec.jobTemplate` defines a template for the Jobs that the CronJob creates, and it is required. It has exactly the same schema as a Job, except that it is nested and does not have an `apiVersion` or `kind`.

## Deadline for delayed Job start

The `.spec.startingDeadlineSeconds` field is optional. This field defines a deadline (in whole seconds) for starting the Job, if that Job misses its scheduled time for any reason.

After missing the deadline, the CronJob skips that instance of the Job (future occurrences are still scheduled). For example, if you have a backup Job that runs twice a day, you might allow it to start up to 8 hours late, but no later, because a backup taken any later wouldn't be useful: you would instead prefer to wait for the next scheduled run.

If the `.spec.startingDeadlineSeconds` field is set (not null), the CronJob controller measures the time between when a Job is expected to be created and now. If the difference is higher than that limit, it will skip this execution.

## Concurrency policy

The `.spec.concurrencyPolicy` field is also optional. It specifies how to treat concurrent executions of a Job that is created by this CronJob. The spec may specify only one of the following concurrency policies:

- `Allow` (default): The CronJob allows concurrently running Jobs
- `Forbid`: The CronJob does not allow concurrent runs; if it is time for a new Job run and the previous Job run hasn't finished yet, the CronJob skips the new Job run. Also note that when the previous Job run finishes, `.spec.startingDeadlineSeconds` is still taken into account and may result in a new Job run.
- `Replace`: If it is time for a new Job run and the previous Job run hasn't finished yet, the CronJob replaces the currently running Job run with a new Job run

## Jobs history limits

The `.spec.successfulJobsHistoryLimit` and `.spec.failedJobsHistoryLimit` fields specify how many completed and failed Jobs should be kept. Both fields are optional.

- `.spec.successfulJobsHistoryLimit`: This field specifies the number of successful finished jobs to keep. The default value is `3`. Setting this field to `0` will not keep any successful jobs.
- `.spec.failedJobsHistoryLimit`: This field specifies the number of failed finished jobs to keep. The default value is `1`. Setting this field to `0` will not keep any failed jobs.
```

### A6 · `k8s-docs-garbage-collection-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/architecture/garbage-collection/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["owner-reference", "cascading-deletion", "orphaning", "ownership-chain", "label-selector"]
---
# Garbage Collection (kubernetes.io/docs/concepts/architecture/garbage-collection/)

Garbage collection is a collective term for the various mechanisms Kubernetes uses to clean up cluster resources. This allows the clean up of resources like the following:

- Terminated pods
- Completed Jobs
- Objects without owner references
- Unused containers and container images
- Dynamically provisioned PersistentVolumes with a StorageClass reclaim policy of Delete
- Stale or expired CertificateSigningRequests (CSRs)
- Nodes deleted in the following scenarios: on a cloud when the cluster uses a cloud controller manager; on-premises when the cluster uses an addon similar to a cloud controller manager
- Node Lease objects

## Owners and dependents

Many objects in Kubernetes link to each other through *owner references*. Owner references tell the control plane which objects are dependent on others. Kubernetes uses owner references to give the control plane, and other API clients, the opportunity to clean up related resources before deleting an object. In most cases, Kubernetes manages owner references automatically.

Ownership is different from the labels and selectors mechanism that some resources also use. For example, consider a Service that creates `EndpointSlice` objects. The Service uses *labels* to allow the control plane to determine which `EndpointSlice` objects are used for that Service. In addition to the labels, each `EndpointSlice` that is managed on behalf of a Service has an owner reference. Owner references help different parts of Kubernetes avoid interfering with objects they don't control.

Note: Cross-namespace owner references are disallowed by design. Namespaced dependents can specify cluster-scoped or namespaced owners. A namespaced owner **must** exist in the same namespace as the dependent. If it does not, the owner reference is treated as absent, and the dependent is subject to deletion once all owners are verified absent.

Cluster-scoped dependents can only specify cluster-scoped owners. In v1.20+, if a cluster-scoped dependent specifies a namespaced kind as an owner, it is treated as having an unresolvable owner reference, and is not able to be garbage collected.

In v1.20+, if the garbage collector detects an invalid cross-namespace `ownerReference`, or a cluster-scoped dependent with an `ownerReference` referencing a namespaced kind, a warning Event with a reason of `OwnerRefInvalidNamespace` and an `involvedObject` of the invalid dependent is reported.

## Cascading deletion

Kubernetes checks for and deletes objects that no longer have owner references, like the pods left behind when you delete a ReplicaSet. When you delete an object, you can control whether Kubernetes deletes the object's dependents automatically, in a process called *cascading deletion*. There are two types of cascading deletion, as follows:

- Foreground cascading deletion
- Background cascading deletion

You can also control how and when garbage collection deletes resources that have owner references using Kubernetes finalizers.

### Foreground cascading deletion

In foreground cascading deletion, the owner object you're deleting first enters a *deletion in progress* state. In this state, the following happens to the owner object:

- The Kubernetes API server sets the object's `metadata.deletionTimestamp` field to the time the object was marked for deletion.
- The Kubernetes API server also sets the `metadata.finalizers` field to `foregroundDeletion`.
- The object remains visible through the Kubernetes API until the deletion process is complete.

After the owner object enters the *deletion in progress* state, the controller deletes dependents it knows about. After deleting all the dependent objects it knows about, the controller deletes the owner object. At this point, the object is no longer visible in the Kubernetes API.

During foreground cascading deletion, the only dependents that block owner deletion are those that have the `ownerReference.blockOwnerDeletion=true` field and are in the garbage collection controller cache. The garbage collection controller cache may not contain objects whose resource type cannot be listed / watched successfully, or objects that are created concurrent with deletion of an owner object.

### Background cascading deletion

In background cascading deletion, the Kubernetes API server deletes the owner object immediately and the garbage collector controller (custom or default) cleans up the dependent objects in the background. If a finalizer exists, it ensures that objects are not deleted until all necessary clean-up tasks are completed. By default, Kubernetes uses background cascading deletion unless you manually use foreground deletion or choose to orphan the dependent objects.

## Orphaned dependents

When Kubernetes deletes an owner object, the dependents left behind are called *orphan* objects. By default, Kubernetes deletes dependent objects.
```

### A7 · `k8s-docs-deployment-spec-fields-2026-08-24.md` (new)

```markdown
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
```

### A8 · `k8s-docs-replicationcontroller-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["replicationcontroller-legacy", "replicaset", "deployment"]
---
# ReplicationController (kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/)

## Legacy notice (top of page)

A `Deployment` that configures a `ReplicaSet` is now the recommended way to set up replication.

Page header description: Legacy API for managing workloads that can scale horizontally. Superseded by the Deployment and ReplicaSet APIs.

## What a ReplicationController is

A *ReplicationController* ensures that a specified number of pod replicas are running at any one time. In other words, a ReplicationController makes sure that a pod or a homogeneous set of pods is always up and available.

## How a ReplicationController works

If there are too many pods, the ReplicationController terminates the extra pods. If there are too few, the ReplicationController starts more pods. Unlike manually created pods, the pods maintained by a ReplicationController are automatically replaced if they fail, are deleted, or are terminated. For example, your pods are re-created on a node after disruptive maintenance such as a kernel upgrade. For this reason, you should use a ReplicationController even if your application requires only a single pod. A ReplicationController is similar to a process supervisor, but instead of supervising individual processes on a single node, the ReplicationController supervises multiple pods across multiple nodes.

ReplicationController is often abbreviated to "rc" in discussion, and as a shortcut in kubectl commands.

A simple case is to create one ReplicationController object to reliably run one instance of a Pod indefinitely. A more complex use case is to run several identical replicas of a replicated service, such as web servers.

---

NOT IN THIS SNAPSHOT: the "Alternatives to ReplicationController" subsections were truncated by the fetcher. The equivalent statement from the ReplicaSet page is cached in `k8s-docs-replicaset-2026-08-24.md`: "ReplicaSets are the successors to ReplicationControllers. The two serve the same purpose, and behave similarly, except that a ReplicationController does not support set-based selector requirements... As such, ReplicaSets are preferred over ReplicationControllers."
```

### A9 · `k8s-docs-hpa-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["horizontalpodautoscaler", "horizontal-scaling", "vertical-scaling", "replicas", "daemonset"]
---
# HorizontalPodAutoscaler (kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

## What an HPA is

In Kubernetes, a *HorizontalPodAutoscaler* automatically updates a workload resource (such as a Deployment or StatefulSet), with the aim of automatically scaling capacity to match demand.

Horizontal scaling means that the response to increased load is to deploy more Pods. This is different from *vertical* scaling, which for Kubernetes would mean assigning more resources (for example: memory or CPU) to the Pods that are already running for the workload.

If the load decreases, and the number of Pods is above the configured minimum, the HorizontalPodAutoscaler instructs the workload resource (the Deployment, StatefulSet, or other similar resource) to scale back down.

Horizontal pod autoscaling does not apply to objects that can't be scaled (for example: a DaemonSet.)

## How does a HorizontalPodAutoscaler work?

The HorizontalPodAutoscaler is implemented as a Kubernetes API resource and a controller. The resource determines the behavior of the controller. The horizontal pod autoscaling controller, running within the Kubernetes control plane, periodically adjusts the desired scale of its target (for example, a Deployment) to match observed metrics such as average CPU utilization, average memory utilization, or any other custom metric you specify.

Kubernetes implements horizontal pod autoscaling as a control loop that runs intermittently (it is not a continuous process). The interval is set by the `--horizontal-pod-autoscaler-sync-period` parameter to the `kube-controller-manager` (and the default interval is 15 seconds).

The HorizontalPodAutoscaler controller accesses corresponding workload resources that support scaling (such as Deployments and StatefulSet).
```

### A10 · `k8s-docs-kubectl-rollout-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["rollout", "rollout-history", "rollback", "pause-rollout", "resume-rollout", "kubectl-rollout-status", "kubectl-rollout-history", "kubectl-rollout-undo", "kubectl-rollout-pause", "kubectl-rollout-resume"]
---
# kubectl rollout (kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

## Synopsis

Manage the rollout of a resource.

Manage the rollout of one or many resources.

Valid resource types include:

- deployments
- daemonsets
- statefulsets

## Subcommands

| Command | Description |
|---|---|
| `kubectl rollout history` | View rollout history |
| `kubectl rollout pause` | Mark the provided resource as paused |
| `kubectl rollout restart` | Restart a resource |
| `kubectl rollout resume` | Resume a paused resource |
| `kubectl rollout status` | Show the status of the rollout |
| `kubectl rollout undo` | Undo a previous rollout |
```

---

## Gaps

Nothing in the outline's concept list is now unsourced at the depth the outline asks for, with the following exceptions. **Drafting must not invent facts to fill these.**

**G-6A — "A DaemonSet has no `replicas` field" is not stated as such in any fetched source.** This is load-bearing: it is Exam Alert priority #3, the §7 Fixed Point, trap #22, and Bearings #3 item 2's correct answer. What *is* sourced, and is sufficient to make the claim positively rather than as a negative:
- "A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them." (DaemonSet page)
- "The DaemonSet controller creates a Pod for each eligible node…" (DaemonSet page)
- "If you do not specify either, then the DaemonSet controller will create Pods on all nodes." (DaemonSet page)
- "Horizontal pod autoscaling does not apply to objects that can't be scaled (for example: a DaemonSet.)" (HPA page) — the strongest corroboration that a DaemonSet is not replica-scaled.
**Recommendation:** phrase the Fixed Point as *the count is a consequence of how many nodes match*, which is directly sourced, rather than as *there is no `replicas` field*, which is true but uncited. The outline's own §7 wording already does this ("The count is a consequence of how many nodes match") — keep that wording and drop the "has no `replicas` field" clause, or cite it to the API reference in a later pass.

**G-6B — "Alternatives to DaemonSet" and "Alternatives to ReplicationController" sections not captured.** Both were truncated by the fetcher. Neither is needed: the outline gives DaemonSet one-third of a short section and ReplicationController one clause, and the ReplicaSet page's own "Alternatives" section (cached in full) supplies the DaemonSet-vs-ReplicaSet and ReplicaSet-vs-ReplicationController contrasts.

**G-6C — Job "Job patterns" prose bodies not captured** (section headings only). Out of scope — the outline explicitly excludes Job parallelism and patterns from §7.

**G-6D — No source fetched for the §7 claim that Job connects to Pod phases `Succeeded`/`Failed`.** See Notes, note 3 — this is a precision hazard, not a missing source.

**Not a gap, recorded for the audit trail:** the outline's § Open questions #2 lists five blocking research gaps. All five are closed by snapshots A1–A6. Open questions #5 (StatefulSet ordinal naming), #6 (`minReadySeconds` / `progressDeadlineSeconds`) and #7 (ReplicationController) are also closed by A2, A7 and A8 respectively.

---

## Notes for the author

**1. ⚠ CORRECTION REQUIRED — §4's worked example gives the wrong surge number, and the error propagates to a figure and an answer key.**

The outline states, in §4 and again in `ch06-fig02`'s spec and Bearings #2 item 1: *"ten replicas, defaults, so at most twelve Pods exist and at least eight are available"* — with **12 and 8** as the answer key and the figure's labels.

The sources are explicit that the two bounds round in **opposite directions**:

- `maxSurge`: "The absolute number is calculated from the percentage by **rounding up**." → 25% of 10 = 2.5 → **3** → maximum total Pods = **13**
- `maxUnavailable`: "The absolute number is calculated from percentage by **rounding down**." → 25% of 10 = 2.5 → **2** → minimum available Pods = **8**

So the correct pair is **13 and 8**, not 12 and 8. The "8" is right; the "12" is wrong. This is verbatim in both the concept page and the API reference (snapshot A7), which agree.

This matters in four places: §4's numeric walkthrough; the `⚠ Navigational Hazards` transposition trap; `ch06-fig02`, whose design brief says "use the worked ten-replica example's actual numbers (12 and 8)"; and Bearings #2 item 1, whose stated correct answer is "twelve and eight."

**Recommendation: correct to 13 and 8 and keep ten replicas.** The asymmetric rounding is not a nuisance to be designed around — it is the single best piece of evidence for the point `ch06-fig02` already exists to make, that surge is a ceiling on *total* and unavailable is a floor on *available*. They are not a symmetric pair, and the rounding proves it. It also gives Bearings #2 item 1 a genuinely good distractor (12, from a reader who rounded both the same way) that is a real misconception rather than an invented one.

If the author prefers to avoid rounding entirely, the alternative is a replica count divisible by four — 8 replicas gives maxSurge 2 and maxUnavailable 2, so at most 10 and at least 6, with no rounding in play. That is cleaner arithmetic but discards the asymmetry, and I'd advise against it for that reason.

**2. §4's safety claim is now precisely sourceable, and it is stronger than the outline assumed.** Open question #6 asked whether `minReadySeconds` could be included. It can, verbatim: *"the minimum number of seconds for which a newly created Pod should be ready without any of its containers crashing, for it to be considered available. This defaults to 0 (the Pod will be considered available as soon as it is ready)."* That is exactly the readiness-gates-availability link §4 needs, and the default of 0 lets the draft make the point without configuring anything.

`progressDeadlineSeconds` is also sourced, with the mechanism the outline wanted: default **600**, surfaced as a condition with `type: Progressing`, `status: "False"`, `reason: ProgressDeadlineExceeded`. Per the outline's own recommendation, use it as *the mechanism behind the stuck-rollout signal*, not as a tunable.

Better still for the Chapter 5 payoff: the "Failed Deployment" list names **"Readiness probe failures"** as a documented cause of a Deployment getting stuck without completing. That is the probe promise discharged in the source's own words, and it is what Bearings #2 item 4 should key against.

**3. Precision hazard in §7 — Job *conditions* and Pod *phases* are different vocabularies wearing similar words.** The outline's §7 plans to connect Job back to Chapter 5's phase vocabulary: *"work that ends is work that reaches `Succeeded` or `Failed`."* Note that the Job page's own terms for a finished Job are **`Complete` or `Failed`** (Job conditions), while `Succeeded`/`Failed` are **Pod phases** from `k8s-docs-pod-lifecycle-2026-08-23.md`. Both statements are true of different objects: the Job's *Pods* reach phase `Succeeded`; the *Job* gets condition `Complete`. The retrieval still works — it is the Pods whose phase the reader learned — but the draft should not write "the Job reaches `Succeeded`." Worth a line in the answer key for the §6–§7 Practice retrieval item, which is built on exactly this connection.

**4. One source disagreement, resolved.** A first-pass fetch of the rendered Job page reported `.spec.backoffLimit` "default value is 4"; the docs' raw markdown source states "set by default to **6**, unless the backoff limit per index (only Indexed Job) is specified." Treat **6** as correct — the raw source is the same content kubernetes.io renders and the rendered-page pass was a lossy extraction. Immaterial in practice: the outline excludes backoff limits from §7. Flagged only so a later fact-accuracy audit doesn't re-derive the conflict from the snapshot's transcription note.

**5. Open question #3 (ownership machinery depth) resolves in favour of including adoption.** The outline said to add controller adoption of pre-existing bare Pods *"only if the fetched ReplicaSet page presents it plainly."* It does — there is a dedicated **"Non-Template Pod acquisitions"** section, with the recommendation stated as a practical warning: *"it is strongly recommended to make sure that the bare Pods do not have labels which match the selector of one of your ReplicaSets."* It also supplies the outcome that makes membership-as-query visceral: a bare Pod matching the selector is *"immediately acquired,"* and if the ReplicaSet is then over count, *"immediately terminated."* That is a better §3 illustration than the runaway-Pods scenario alone, and it is documented rather than constructed.

`--cascade=orphan` is now sourced too, but the outline's instruction to keep it out (Chapter 8's territory) still stands on scope grounds, not source grounds.

**6. §3's selector Fixed Point is now sourced three times over, in three resources' own words** — which is useful, because the outline wants the rule stated as general rather than Deployment-specific:
- ReplicaSet: "`.spec.template.metadata.labels` must match `spec.selector`, or it will be rejected by the API."
- Deployment: "`.spec.selector` must match `.spec.template.metadata.labels`, or it will be rejected by the API."
- DaemonSet: "The `.spec.selector` must match the `.spec.template.metadata.labels`. Config with these two not matching will be rejected by the API."

One caveat worth the draft's attention: all three say the **API rejects** the mismatch. The outline's §3 generation-effect prompt asks the reader to predict a *runaway* — "the controller creates a Pod that it cannot see, notices the gap, creates more." For a Deployment or ReplicaSet the API refuses the object outright, so the runaway is not what a reader would actually observe. **Recommendation:** keep the prompt, but let the payoff be the better answer — *the API won't let you, and the reason it won't is that the runaway is what would otherwise happen*. That preserves the generation effect, is faithful to the source, and is a sharper Fixed Point than the uncorrected version. Do not describe the runaway as an observable outcome.

**7. §3's overlapping-selectors hazard needs a narrower framing than "two controllers fight."** The nearest sourced statement is the ReplicaSet page's *"For 2 ReplicaSets specifying the same `.spec.selector` but different `.spec.template.metadata.labels` and `.spec.template.spec` fields, each ReplicaSet ignores the Pods created by the other ReplicaSet"* — which describes controllers **not** fighting in that specific configuration. The sourced hazards are: the Pod-template warning *"Be careful not to overlap with the selectors of other controllers, lest they try to adopt this Pod"*; bare-Pod acquisition; and the DaemonSet page's *"Mutating the pod selector can lead to the unintentional orphaning of Pods."* The `🪝 Snag`'s "neither one reports an error, it looks like flapping" is a reasonable practitioner observation but is **not** in any fetched source — mark it as authored colour, or recast the Snag around adoption and orphaning, both of which are documented.

**8. §6's Fixed Point and `ch06-fig05`'s lower row are now fully unblocked.** The interchangeability claim is available in the strongest possible form — *"These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling"* — which is the source contradicting trap #21 directly, in one sentence, without the draft having to construct the contrast. Ordinal naming is sourced with the exact pattern `$(statefulset name)-$(ordinal)` and the concrete `web-0, web-1, web-2`, so the figure can use real names rather than the generic fallback the outline planned for.

Two further facts serve `ch06-fig05`'s design requirement that storage belong to the *identity*, not the Pod: *"The same PersistentVolumeClaim will be bound to a Pod throughout its lifecycle"* and *"the PersistentVolumeClaim(s) … are not deleted when the Pod, or the StatefulSet is deleted."* The second is arguably Chapter 11's, but it is the cleanest evidence that the claim outlives the Pod. Use it in the figure's design brief even if the prose holds it back.

**9. §2's HPA sentence can now be one sentence and still be precise.** Snapshot A9 gives horizontal-vs-vertical in the source's own words, which resolves open question #4 favourably: the draft can name horizontal scaling as "deploy more Pods" and get the vertical contrast for free in the same sentence, without importing VPA. The HPA page also confirms the ReplicaSet page's statement that a ReplicaSet is a valid HPA target, and — usefully for §7 — that HPA *"does not apply to objects that can't be scaled (for example: a DaemonSet)."*

**10. §5's `kubectl rollout` verb surface is confirmed closed and small.** Six subcommands: `history`, `pause`, `restart`, `resume`, `status`, `undo`. Note `restart` is in the set and the outline does not plan to teach it; that is the right call at associate tier, but the draft should not present the list as exhaustive if it omits one. Either name all six in passing or present the five it teaches without claiming completeness. Also note that `kubectl rollout` is valid for **deployments, daemonsets and statefulsets** — which quietly reinforces §9's Zenith claim that these are the same shape.

**11. Version currency.** All ten snapshots were fetched 2026-08-24 from current kubernetes.io docs. Two carry explicit version markers: the StatefulSet Pod Name Label is `v1.33 [stable]`, and the garbage-collection cross-namespace owner-reference rules are marked `v1.20+`. Neither is associate-tier material and neither is used by the outline. The cached `k8s-docs-autoscaling-2026-08-23.md` references `v1.35` for in-place pod vertical scaling, which is consistent with these being current-release docs; no version skew between the 08-23 and 08-24 snapshot sets was observed.
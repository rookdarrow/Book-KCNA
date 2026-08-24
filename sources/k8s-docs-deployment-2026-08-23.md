---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/deployment/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D3 Application Delivery"]
concepts_covered: ["deployment", "replicaset", "rolling-update", "recreate", "rollback", "rollout-history", "pause-resume", "revision"]
---
# Deployments (kubernetes.io/docs/concepts/workloads/controllers/deployment/)

A Deployment manages a set of Pods to run an application workload, usually one that doesn't maintain state. A Deployment provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

## Use case
The following are typical use cases for Deployments: create a Deployment to rollout a ReplicaSet — the ReplicaSet creates Pods in the background; declare the new state of the Pods by updating the PodTemplateSpec of the Deployment — a new ReplicaSet is created and the Deployment manages moving the Pods from the old ReplicaSet to the new one at a controlled rate, and each new ReplicaSet updates the revision of the Deployment; rollback to an earlier Deployment revision if the current state of the Deployment is not stable; scale up the Deployment to facilitate more load; pause the rollout of a Deployment to apply multiple fixes to its PodTemplateSpec and then resume it to start a new rollout; use the status of the Deployment as an indicator that a rollout has stuck; clean up older ReplicaSets that you don't need anymore.

## Strategy
.spec.strategy specifies the strategy used to replace old Pods by new ones. .spec.strategy.type can be "Recreate" or "RollingUpdate". "RollingUpdate" is the default value. Recreate Deployment: all existing Pods are killed before new ones are created. Rolling Update Deployment: the Deployment updates Pods in a rolling update fashion; you can specify maxUnavailable and maxSurge to control the rolling update process. Max Unavailable — the maximum number of Pods that can be unavailable during the update process; the value can be an absolute number or a percentage of desired Pods; the default value is 25%. Max Surge — the maximum number of Pods that can be created over the desired number of Pods; can be an absolute number or a percentage; the default value is 25%.

## Rolling back a Deployment
Sometimes, you may want to rollback a Deployment; for example, when the Deployment is not stable, such as crash looping. By default, all of the Deployment's rollout history is kept in the system so that you can rollback anytime you want (you can change that by modifying revision history limit). A Deployment's revision is created when a Deployment's rollout is triggered — a new revision is created if and only if the Deployment's Pod template (.spec.template) is changed; other updates, such as scaling the Deployment, do not create a Deployment revision. `kubectl rollout history deployment/<name>` shows revisions; `kubectl rollout undo deployment/<name>` rolls back to the previous revision, `--to-revision=<n>` to a specific one.

## Pausing and resuming a rollout
When you update a Deployment, or plan to, you can pause rollouts for that Deployment before you trigger one or more updates. When you're ready to apply those changes, you resume rollouts for the Deployment. This approach allows you to apply multiple fixes in between pausing and resuming without triggering unnecessary rollouts (`kubectl rollout pause` / `kubectl rollout resume`).

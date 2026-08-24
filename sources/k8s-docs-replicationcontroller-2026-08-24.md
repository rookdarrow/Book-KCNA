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

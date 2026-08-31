---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/"
fetched_at: "2026-08-31T13:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["evicted", "node-pressure-eviction", "eviction-order-by-qos-class", "node-conditions-as-diagnostic", "oomkilled-signature"]
closes_gap: "Node-pressure eviction had NO snapshot in the corpus. Load-bearing for sec.4 (Evicted vs OOMKilled) and the Exam Alert confusion pair."
---
# Node-pressure Eviction

> All passages below are **[VERBATIM]**.

> "Node-pressure eviction is the process by which the kubelet proactively terminates pods to reclaim resource on nodes."

> "The kubelet monitors resources like memory, disk space, and filesystem inodes on your cluster's nodes. When one or more of these resources reach specific consumption levels, the kubelet can proactively fail one or more pods on the node to reclaim resources and prevent starvation."

> "During a node-pressure eviction, the kubelet sets the phase for the selected pods to `Failed`, and terminates the Pod."

> "Node-pressure eviction is not the same as API-initiated eviction."

> "The kubelet does not respect your configured PodDisruptionBudget or the pod's `terminationGracePeriodSeconds`. If you use soft eviction thresholds, the kubelet respects your configured `eviction-max-pod-grace-period`. If you use hard eviction thresholds, the kubelet uses a `0s` grace period (immediate shutdown) for termination."

## Self healing behavior

> "The kubelet attempts to reclaim node-level resources before it terminates end-user pods. For example, it removes unused container images when disk resources are starved."

> "If the pods are managed by a workload management object (such as StatefulSet or Deployment) that replaces failed pods, the control plane (`kube-controller-manager`) creates new pods in place of the evicted pods."

## Eviction signals

> "Eviction signals are the current state of a particular resource at a specific point in time. The kubelet uses eviction signals to make eviction decisions by comparing the signals to eviction thresholds, which are the minimum amount of the resource that should be available on the node."

| Eviction Signal | Description |
|---|---|
| `memory.available` | `node.status.capacity[memory]` - `node.stats.memory.workingSet` |
| `nodefs.available` | `node.stats.fs.available` |
| `nodefs.inodesFree` | `node.stats.fs.inodesFree` |
| `imagefs.available` | `node.stats.runtime.imagefs.available` |
| `imagefs.inodesFree` | `node.stats.runtime.imagefs.inodesFree` |
| `containerfs.available` | `node.stats.runtime.containerfs.available` |
| `containerfs.inodesFree` | `node.stats.runtime.containerfs.inodesFree` |
| `pid.available` | `node.stats.rlimit.maxpid` - `node.stats.rlimit.curproc` |

## Eviction thresholds

> "The kubelet supports both soft and hard eviction thresholds."

> "A soft eviction threshold pairs an eviction signal with a grace period. The kubelet does not evict pods until the node conditions have been violated for the entire grace period. If no grace period is set, the kubelet evicts pods immediately upon reaching the threshold."

> "A hard eviction threshold has no grace period, and if observed, the kubelet will immediately evict pods."

> "The kubelet has the following default hard eviction thresholds:"

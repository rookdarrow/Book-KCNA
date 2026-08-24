---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Scheduling"]
concepts_covered: ["taints", "tolerations", "noschedule", "prefernoschedule", "noexecute", "tolerationseconds", "node-affinity-contrast"]
---
# Taints and Tolerations (kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

Node affinity is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement). Taints are the opposite — they allow a node to repel a set of pods. Tolerations are applied to pods. Tolerations allow the scheduler to schedule pods with matching taints. Tolerations allow scheduling but don't guarantee scheduling: the scheduler also evaluates other parameters as part of its function. Taints and tolerations work together to ensure that pods are not scheduled onto inappropriate nodes. One or more taints are applied to a node; this marks that the node should not accept any pods that do not tolerate the taints.

## Taint effects
- NoExecute — affects pods that are already running on the node: pods that do not tolerate the taint are evicted immediately; pods that tolerate the taint without specifying tolerationSeconds remain bound forever; pods that tolerate the taint with a specified tolerationSeconds remain bound for the specified amount of time, after which the node lifecycle controller evicts them.
- NoSchedule — no new Pods will be scheduled on the tainted node unless they have a matching toleration. Pods currently running on the node are not evicted.
- PreferNoSchedule — a "preference" or "soft" version of NoSchedule. The control plane will try to avoid placing a Pod that does not tolerate the taint on the node, but it is not guaranteed.

## Matching
A toleration "matches" a taint if the keys are the same and the effects are the same, and: the operator is Exists (in which case no value should be specified), or the operator is Equal and the values should be equal. If the key is empty, then the operator must be Exists, which matches all keys and values (the effect still needs to match). An empty effect matches all effects with the given key.

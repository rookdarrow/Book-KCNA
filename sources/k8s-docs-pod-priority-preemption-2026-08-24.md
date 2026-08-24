---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/scheduling-eviction/pod-priority-preemption.md"
fetched_at: "2026-08-24T09:51:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["preemption", "pod-priority", "priorityclass", "pending-pod", "scheduling-queue"]
scope_note: "Fetched at deliberately shallow depth to support ONE CLAUSE in ch-07 §2, per outline Open Question #3. This is not a teaching source for PriorityClass mechanics, which are out of scope for a 5-point associate chapter."
---
# Pod Priority and Preemption (kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

> **Extraction note.** All passages below are **[VERBATIM]** and safe to cite.

## Priority and preemption — overview

> Priority indicates the importance of a Pod relative to other Pods. If a Pod cannot be
> scheduled, the scheduler tries to preempt (evict) lower priority Pods to make scheduling
> of the pending Pod possible.

## How preemption is triggered

> When Pods are created, they go to a queue and wait to be scheduled. The scheduler picks
> a Pod from the queue and tries to schedule it on a Node. If no Node is found that
> satisfies all the specified requirements of the Pod, preemption logic is triggered for
> the pending Pod.

> Preemption logic tries to find a Node where removal of one or more Pods with lower
> priority than P would enable P to be scheduled on that Node.

## PriorityClass

> A PriorityClass is a non-namespaced object that defines a mapping from a priority class
> name to the integer value of the priority. The name is specified in the `name` field of
> the PriorityClass object's metadata. The value is specified in the required `value`
> field.

---

NOT IN THIS SNAPSHOT: preemption policies, `preemptionPolicy: Never`, the non-preempting
PriorityClass behaviour, graceful termination of preempted Pods, PodDisruptionBudget
interaction, cross-node preemption limitations, and the built-in
`system-cluster-critical` / `system-node-critical` classes. All deliberately out of scope
— see research-manifest Notes, note 5.

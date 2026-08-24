# Research Manifest — KCNA Chapter 7

**Chapter:** 7 — *Assigning the Berth* · **Objective:** D1.3 · **Stage 2 run:** 2026-08-24T09:52:00-0400

The one **BLOCKING** research gap the outline raised in § Open questions #2 — topology spread constraints — is now **CLOSED**, and closed well past the fallback the outline planned for. Open questions **#3, #5, #6, #8 and #10 also resolve**, four of them in favour of the outline's recommendation and one *against* it (**#5 — read note 1 before drafting §6**). Seven new snapshots below.

Two findings need author attention before drafting and are raised in § Notes: the Scheduling Policies currency call (note 1) and **Chapter 6 not being shipped at all** (note 9), which is a harder version of the outline's own open question #11.

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-topology-spread-constraints-2026-08-24.md` | Kubernetes project | D1.3 | topology-spread-constraints, topology-domain, topology-key, maxskew, whenunsatisfiable, mindomains, pod-affinity, pod-anti-affinity, cluster-level-default-constraints |
| `k8s-docs-taints-tolerations-depth-2026-08-24.md` | Kubernetes project | D1.3 | kubectl-taint, dedicated-nodes, special-hardware-nodes, taint-based-evictions, built-in-node-condition-taints, taint-nodes-by-condition, tolerationseconds, multiple-taint-filtering |
| `k8s-docs-assign-pod-node-depth-2026-08-24.md` | Kubernetes project | D1.3 | node-affinity, affinity-operators, preferred-during-scheduling, nodeselectorterms-semantics, pod-affinity, pod-anti-affinity, topology-key, nodename |
| `k8s-docs-pod-priority-preemption-2026-08-24.md` | Kubernetes project | D1.3 | preemption, priorityclass, pending-pod |
| `k8s-docs-assign-pods-nodes-task-2026-08-24.md` | Kubernetes project | D1.3 | kubectl-get-nodes, kubectl-label, kubectl-get-pods, nodeselector, node-labels |
| `k8s-docs-well-known-labels-2026-08-24.md` | Kubernetes project | D1.3 | standard-node-labels, topology-key |
| `k8s-docs-node-allocatable-2026-08-24.md` | Kubernetes project | D1.3 | node-allocatable, node-capacity, requests-as-scheduling-input |

### Already cached and verified adequate (no re-fetch needed)

`k8s-docs-kube-scheduler-2026-08-23.md` · `k8s-docs-assign-pod-node-2026-08-23.md` · `k8s-docs-taints-tolerations-2026-08-23.md` · `k8s-docs-pod-lifecycle-2026-08-23.md` · `k8s-docs-resource-management-2026-08-23.md` · `k8s-docs-nodes-2026-08-23.md` · `k8s-docs-runtime-class-2026-08-23.md` · `k8s-docs-daemonset-2026-08-24.md` · `k8s-docs-labels-selectors-2026-08-23.md` · `k8s-docs-cluster-architecture-2026-08-23.md` · `k8s-docs-components-2026-08-23.md` · `k8s-docs-pod-qos-2026-08-24.md` · `k8s-docs-kubectl-overview-2026-08-23.md`

I read the four core scheduling snapshots directly rather than trusting the outline's summary of them. **Every §1, §2, §3, §4 and §6 source claim the outline makes is present verbatim in the cached files as described** — including the random tie-break, `PodFitsResources`, the kubelet reserving at least the request amount, all three taint effects with `tolerationSeconds`, the four matching rules with both wildcards, `IgnoredDuringExecution`, the six operators, and `nodeName` overruling `nodeSelector` and affinity. The outline's source lines are accurate and no correction is needed there.

Two things the outline attributed to cached snapshots that I should flag as **already present and better than described**: `k8s-docs-daemonset-2026-08-24.md` carries the *complete* seven-row built-in taint table with effects (the outline treats this as the §4 source, correctly — it is the strongest cached version of that fact), and `k8s-docs-assign-pod-node-2026-08-23.md` already carries the `node-restriction.kubernetes.io/` prefix and NodeRestriction sentence that §3 forward-bears to Chapter 8 on. §3 is sourced today.

---

## Snapshots

### A1 · `k8s-docs-topology-spread-constraints-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/scheduling-eviction/topology-spread-constraints.md"
fetched_at: "2026-08-24T09:48:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["topology-spread-constraints", "topology-domain", "topology-key", "maxskew", "whenunsatisfiable", "donotschedule", "scheduleanyway", "mindomains", "pod-affinity", "pod-anti-affinity", "cluster-level-default-constraints"]
closes_gap: "B1 G4 remainder — topology spread constraints, flagged BLOCKING in ch-07 outline Open Question #2"
---
# Pod Topology Spread Constraints (kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)

> **Extraction note.** Passages marked **[VERBATIM]** are quoted word-for-word and are
> safe to cite and quote in draft prose. Passages marked **[PARTIAL]** are incomplete
> quotations — the fetch returned a fragment rather than the full sentence. Do not quote
> **[PARTIAL]** material as if it were a complete source sentence; use it only to confirm
> that a field exists and roughly what it does.

## What topology spread constraints are

**[VERBATIM]**

> You can use _topology spread constraints_ to control how Pods are spread across your
> cluster among failure-domains such as regions, zones, nodes, and other user-defined
> topology domains.

**[VERBATIM]**

> This can help to achieve high availability as well as efficient resource utilization.

**[VERBATIM]**

> You can set cluster-level constraints as a default, or configure topology spread
> constraints for individual workloads.

## Motivation

**[VERBATIM]**

> Imagine that you have a cluster of up to twenty nodes, and you want to run a workload
> that automatically scales how many replicas it uses. There could be as few as two Pods
> or as many as fifteen. When there are only two Pods, you'd prefer not to have both of
> those Pods run on the same node: you would run the risk that a single node failure
> takes your workload offline.
>
> In addition to this basic usage, there are some advanced usage examples that enable
> your workloads to benefit on high availability and cluster utilization.
>
> As you scale up and run more Pods, a different concern becomes important. Imagine that
> you have three nodes running five Pods each. The nodes have enough capacity to run that
> many replicas; however, the clients that interact with this workload are split across
> three different datacenters (or infrastructure zones). Now you have less concern about
> a single node failure, but you notice that latency is higher than you'd like, and you
> are paying for network costs associated with sending network traffic between the
> different zones.
>
> You decide that under normal operation you'd prefer to have a similar number of
> replicas scheduled into each infrastructure zone, and you'd like the cluster to
> self-heal in the case that there is a problem.
>
> Pod topology spread constraints offer you a declarative way to configure that.

## Node labels and topology

**[VERBATIM]**

> Topology spread constraints rely on node labels to identify the topology domain(s) that
> each node is in.

**[PARTIAL]** — well-known topology labels named on this page: `topology.kubernetes.io/zone`,
`topology.kubernetes.io/region`, `kubernetes.io/hostname`. Returned as a list of label
keys; the page's per-label description sentences were not captured in this fetch. See
`k8s-docs-well-known-labels-2026-08-24.md` for descriptions.

## Field definitions

### `maxSkew`

**[VERBATIM]**

> **maxSkew** describes the degree to which Pods may be unevenly distributed. You must
> specify this field and the number must be greater than zero. Its semantics differ
> according to the value of `whenUnsatisfiable`:
>
> - if you select `whenUnsatisfiable: DoNotSchedule`, then `maxSkew` defines the maximum
>   permitted difference between the number of matching pods in the target topology and
>   the _global minimum_ (the minimum number of matching pods in an eligible domain or
>   zero if the number of eligible domains is less than MinDomains). For example, if you
>   have 3 zones with 2, 2 and 1 matching pods respectively, `MaxSkew` is set to 1 then
>   the global minimum is 1.
> - if you select `whenUnsatisfiable: ScheduleAnyway`, the scheduler gives higher
>   precedence to topologies that would help reduce the skew.

### `topologyKey`

**[VERBATIM]**

> **topologyKey** is the key of node labels. Nodes that have a label with this key and
> identical values are considered to be in the same topology.

### `whenUnsatisfiable`

**[VERBATIM]**

> **whenUnsatisfiable** indicates how to deal with a Pod if it doesn't satisfy the spread
> constraint:
>
> - `DoNotSchedule` (default) tells the scheduler not to schedule it.
> - `ScheduleAnyway` tells the scheduler to still schedule it while prioritizing nodes
>   that minimize the skew.

### `labelSelector`

**[VERBATIM]**

> **labelSelector** is used to find matching Pods. Pods that match this label selector
> are counted to determine the number of Pods in their corresponding topology domain.

### `minDomains`

**[VERBATIM]**

> **minDomains** indicates a minimum number of eligible domains. This field is optional.
> A domain is a particular instance of a topology. An eligible domain is a domain whose
> nodes match the node selector.

### `matchLabelKeys`, `nodeAffinityPolicy`, `nodeTaintsPolicy`

**[PARTIAL]** — only these fragments were captured. Each field is confirmed present; the
full definition sentences were not returned.

> `matchLabelKeys`: "A null or empty list means only match against the `labelSelector`."

> `nodeAffinityPolicy`: "If this value is null, the behavior is equivalent to the Honor
> policy."

> `nodeTaintsPolicy`: "If this value is null, the behavior is equivalent to the Ignore
> policy."

## Comparison with podAffinity and podAntiAffinity

**[VERBATIM]**

> In Kubernetes, inter-Pod affinity and anti-affinity control how Pods are scheduled in
> relation to one another - either more packed or more scattered.
>
> `podAffinity`: attracts Pods; you can try to pack any number of Pods into qualifying
> topology domain(s).
>
> `podAntiAffinity`: repels Pods. If you set this to
> `requiredDuringSchedulingIgnoredDuringExecution` mode then only a single Pod can be
> scheduled into a single topology domain; if you choose
> `preferredDuringSchedulingIgnoredDuringExecution` then you lose the ability to enforce
> the constraint.
>
> For finer control, you can specify topology spread constraints to distribute Pods
> across different topology domains - to achieve either high availability or cost-saving.
> This can also help on rolling update workloads and scaling out replicas smoothly.

## Cluster-level default constraints

**[VERBATIM]**

> It is possible to set default topology spread constraints for a cluster. Default
> topology spread constraints are applied to a Pod if, and only if: It doesn't define any
> constraints in its `.spec.topologySpreadConstraints`. It belongs to a Service,
> ReplicaSet, StatefulSet or ReplicationController.

## Known limitations

**[VERBATIM]**

> There's no guarantee that the constraints remain satisfied when Pods are removed. For
> example, scaling down a Deployment may result in imbalanced Pods distribution. You can
> use a tool such as the Descheduler to rebalance the Pods distribution.
>
> Pods matched on tainted nodes are respected.
>
> The scheduler doesn't have prior knowledge of all the zones or other topology domains
> that a cluster has. They are determined from the existing nodes in the cluster. This
> could lead to a problem in autoscaled clusters, when a node pool (or node group) is
> scaled to zero nodes, and you're expecting the cluster to scale up, because, in this
> case, those topology domains won't be considered until there is at least one node in
> them. You can work around this by using a Node autoscaler that is aware of Pod topology
> spread constraints and is also aware of the overall set of topology domains.
>
> Pods that don't match their own labelSelector create 'ghost pods'. If a pod's labels
> don't match the `labelSelector` in its topology spread constraint, the pod won't count
> itself in spread calculations. This means: Multiple such pods can just accumulate on
> the same topology (until matching pods are newly created/deleted) because those pod's
> schedule don't change a spreading calculation result. The spreading constraint works in
> an unintended way, most likely not matching your expectations. Ensure your pod's labels
> match the `labelSelector` in your spread constraints. Typically, a pod should match its
> own topology spread constraint selector.

---

NOT IN THIS SNAPSHOT: no standalone formula or equation defining *skew* as a term was
extractable. The page discusses skew contextually (the `maxSkew` definition above, plus a
worked example in which "the actual skew is then 2 (calculated as `3 - 1`)"). **The
`maxSkew` definition above is the citable definition of the concept.** Do not write a
skew formula that is not present here. See research-manifest Gaps, G-7A.
```

### A2 · `k8s-docs-taints-tolerations-depth-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/scheduling-eviction/taint-and-toleration.md"
fetched_at: "2026-08-24T09:50:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["taint", "toleration", "kubectl-taint", "dedicated-nodes", "special-hardware-nodes", "taint-based-evictions", "built-in-node-condition-taints", "taint-nodes-by-condition", "tolerationseconds", "defaulttolerationseconds", "multiple-taint-filtering", "taint-plus-affinity-complementarity"]
supplements: "k8s-docs-taints-tolerations-2026-08-23.md — SAME source page, deeper cut. This file does NOT replace the 2026-08-23 snapshot; that one holds the core concept, the three effects and the four matching rules. This one adds the later sections of the same page."
closes_gap: "ch-07 outline Open Question #10 (kubectl taint command form) and the Bearings #2 item-2 answer-key requirement (taint-plus-affinity complementarity, previously unsourced)"
---
# Taints and Tolerations — later sections (kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

> **Extraction note.** **[VERBATIM]** passages are quoted word-for-word and safe to cite.
> **[PARTIAL]** passages are incomplete — a fragment or condensed list rather than the
> full sentence. Do not quote **[PARTIAL]** material as a complete source sentence.
>
> **This file supplements `k8s-docs-taints-tolerations-2026-08-23.md`, which remains the
> citation of record for the taint/toleration concept, the three effects, and the four
> matching rules.** Nothing here contradicts that snapshot.

## Command forms

**[VERBATIM]** — adding a taint to a node:

    kubectl taint nodes node1 key1=value1:NoSchedule

**[VERBATIM]** — removing a taint (note the trailing minus sign):

    kubectl taint nodes node1 key1=value1:NoSchedule-

## Example Use Cases — Dedicated Nodes

**[VERBATIM]**

> If you want to dedicate a set of nodes for exclusive use by a particular set of users,
> you can add a taint to those nodes (say,
> `kubectl taint nodes nodename dedicated=groupName:NoSchedule`) and then add a
> corresponding toleration to their pods (this would be done most easily by writing a
> custom admission controller). The pods with the tolerations will then be allowed to use
> the tainted (dedicated) nodes as well as any other nodes in the cluster.

**[VERBATIM]** — *this is the passage that sources the taint-plus-affinity
complementarity rule:*

> If you want to dedicate the nodes to them _and_ ensure they _only_ use the dedicated
> nodes, then you should additionally add a label similar to the taint to the same set of
> nodes (e.g. `dedicated=groupName`), and the admission controller should additionally
> add a node affinity to require that the pods can only schedule onto nodes labeled with
> `dedicated=groupName`.

## Example Use Cases — Nodes with Special Hardware

**[VERBATIM]**

> In a cluster where a small subset of nodes have specialized hardware (for example GPUs),
> it is desirable to keep pods that don't need the specialized hardware off of those
> nodes, thus leaving room for later-arriving pods that do need the specialized hardware.

## How multiple taints are processed

**[VERBATIM]**

> start with all of a node's taints, then ignore the ones for which the pod has a matching
> toleration; the remaining un-ignored taints have the indicated effects on the pod.

## `tolerationSeconds`

**[VERBATIM]**

> Pods that tolerate the taint with a specified `tolerationSeconds` remain bound for the
> specified amount of time. After that time elapses, the node lifecycle controller evicts
> the Pods.

## Empty key / `Exists` operator

**[VERBATIM]**

> If the `key` is empty, then the `operator` must be `Exists`, which matches all keys and
> values.

## Taint Nodes by Condition

**[VERBATIM]**

> The control plane, using the node controller, automatically creates taints with a
> `NoSchedule` effect for node conditions. The scheduler checks taints, not node
> conditions, when it makes scheduling decisions. This ensures that node conditions don't
> directly affect scheduling.

**[PARTIAL]** — the full condition-to-taint mapping table was not returned. Two mappings
were captured: `node.kubernetes.io/disk-pressure` (from the `DiskPressure` condition) and
`node.kubernetes.io/memory-pressure` (from the `MemoryPressure` condition). For the
complete built-in taint family with effects, use the table in
`k8s-docs-daemonset-2026-08-24.md`, which is fully cached and carries all seven entries.

## Taint-based Evictions — built-in taints added by the node controller

**[VERBATIM]** — intro fragments:

> The node controller automatically taints a Node when certain conditions are true.

> In some cases when the node is unreachable, the API server is unable to communicate
> with the kubelet on the node.

**[PARTIAL]** — the taint list below was returned in condensed form. Each key is confirmed
present on the page; the descriptions are abbreviated and the per-taint `NodeCondition`
cross-references were not captured. **Cite the key names from here; cite the effects from
`k8s-docs-daemonset-2026-08-24.md`.**

- `node.kubernetes.io/not-ready`: Node is not ready
- `node.kubernetes.io/unreachable`: Node is unreachable from the node controller
- `node.kubernetes.io/memory-pressure`: Node has memory pressure
- `node.kubernetes.io/disk-pressure`: Node has disk pressure
- `node.kubernetes.io/pid-pressure`: Node has PID pressure
- `node.kubernetes.io/network-unavailable`: Node's network is unavailable
- `node.kubernetes.io/unschedulable`: Node is unschedulable
- `node.cloudprovider.kubernetes.io/uninitialized`: When kubelet starts with external cloud provider

## Default tolerations added automatically

**[VERBATIM]**

> Kubernetes automatically adds a toleration for `node.kubernetes.io/not-ready` and
> `node.kubernetes.io/unreachable` with `tolerationSeconds=300`, unless you, or a
> controller, set those tolerations explicitly.

## DaemonSet Pods

**[PARTIAL]** — quoted with an elision in the source fetch:

> DaemonSet pods are created with `NoExecute` tolerations for the following taints with
> no `tolerationSeconds` […] This ensures that DaemonSet pods are never evicted due to
> these problems.

The complete, fully-cached version of this fact — the seven-row toleration table with
effects — is in `k8s-docs-daemonset-2026-08-24.md`. **Prefer that file for the DaemonSet
callback in §4.**

---

NOT IN THIS SNAPSHOT: the YAML toleration examples from the page's opening section; the
full condition-to-taint mapping table; the per-taint `NodeCondition` cross-references in
the taint-based-evictions list.
```

### A3 · `k8s-docs-assign-pod-node-depth-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/scheduling-eviction/assign-pod-node.md"
fetched_at: "2026-08-24T09:51:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["node-affinity", "affinity-operators", "preferred-during-scheduling", "affinity-weight", "nodeselectorterms-semantics", "pod-affinity", "pod-anti-affinity", "topology-key", "nodename", "inter-pod-affinity-cost"]
supplements: "k8s-docs-assign-pod-node-2026-08-23.md — SAME source page, deeper cut. Does NOT replace it; that snapshot holds node labels, nodeSelector, the two DuringScheduling forms, IgnoredDuringExecution, the six operators, and the node-restriction.kubernetes.io/ prefix."
closes_gap: "ch-07 outline Open Question #6 (the nodeSelectorTerms OR / matchExpressions AND concession) and §5's large-cluster performance caveat, which the outline flagged as unsourced and slated for cutting"
---
# Assigning Pods to Nodes — depth (kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

> **Extraction note.** **[VERBATIM]** passages are quoted word-for-word and safe to cite.
> **[PARTIAL]** passages are fragments. Do not quote **[PARTIAL]** material as a complete
> source sentence.

## Node affinity `weight` (preferred rules)

**[VERBATIM]**

> You can specify a `weight` between 1 and 100 for each instance of the
> `preferredDuringSchedulingIgnoredDuringExecution` affinity type.

**[VERBATIM]**

> The final sum is added to the score of other priority functions for the node. Nodes
> with the highest total score are prioritized when the scheduler makes a scheduling
> decision for the Pod.

## How multiple terms and expressions combine

**[VERBATIM]**

> If you specify multiple terms in `nodeSelectorTerms` associated with `nodeAffinity`
> types, then the Pod can be scheduled onto a node if one of the specified terms can be
> satisfied (terms are ORed).

**[VERBATIM]**

> If you specify multiple expressions in a single `matchExpressions` field associated
> with a term in `nodeSelectorTerms`, then the Pod can be scheduled onto a node only if
> all the expressions are satisfied (expressions are ANDed).

## Inter-pod affinity and anti-affinity — `topologyKey`

**[VERBATIM]**

> You express the topology domain (X) using a `topologyKey`, which is the key for the
> node label that the system uses to denote the domain.

## Inter-pod affinity and anti-affinity — cost

**[VERBATIM]**

> Inter-pod affinity and anti-affinity require substantial amounts of processing which can
> slow down scheduling in large clusters significantly. We do not recommend using them in
> clusters larger than several hundred nodes.

## Operator availability by affinity type

**[PARTIAL]** — fragments only:

> The following operators can only be used with `nodeAffinity`. [referring to `Gt` and `Lt`]

> `Gt` and `Lt` operators will not work with non-integer values […] `Gt` and `Lt` are not
> available for `podAffinity`.

## `nodeName`

**[VERBATIM]**

> Using `nodeName` overrules using `nodeSelector` or affinity and anti-affinity rules.

**[VERBATIM]** — the documented caveats of using `nodeName`:

> - If the named node does not exist, the Pod will not run, and in some cases may be
>   automatically deleted.
> - If the named node does not have the resources to accommodate the Pod, the Pod will
>   fail and its reason will indicate why, for example OutOfmemory or OutOfcpu.
> - Node names in cloud environments are not always predictable or stable.

---

NOT IN THIS SNAPSHOT: no explicit list of the standard node labels Kubernetes populates
appears on this page — the page states that it does so without enumerating them. See
`k8s-docs-well-known-labels-2026-08-24.md` for the enumeration. See research-manifest
Gaps, G-7B.
```

### A4 · `k8s-docs-pod-priority-preemption-2026-08-24.md` (new)

```markdown
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
```

### A5 · `k8s-docs-assign-pods-nodes-task-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/configure-pod-container/assign-pods-nodes.md"
fetched_at: "2026-08-24T09:51:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["kubectl-get-nodes", "kubectl-label", "kubectl-get-pods", "node-labels", "nodeselector"]
closes_gap: "ch-07 outline Open Question #10 — the kubectl-get-nodes, kubectl-label and kubectl-get-pods command forms in kb_tags.commands, none of which previously appeared with argument syntax in any cached source"
---
# Assign Pods to Nodes (kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/)

> **Extraction note.** All command lines below are **[VERBATIM]** and safe to reproduce
> exactly as written.

## List the nodes in the cluster

    kubectl get nodes

## List nodes with their labels

    kubectl get nodes --show-labels

## Add a label to a node

    kubectl label nodes <your-node-name> disktype=ssd

## Verify the label was added

    kubectl get nodes --show-labels

## Verify the Pod was scheduled to the chosen node

    kubectl get pods --output=wide

## The nodeSelector step

**[VERBATIM]**

> This pod configuration file describes a pod that has a node selector, `disktype: ssd`.
> This means that the pod will get scheduled on a node that has a `disktype=ssd` label.

---

NOT IN THIS SNAPSHOT: the full YAML manifests referenced by the task, and the
"Create a pod that gets scheduled to a specific node" section using `nodeName`.
```

### A6 · `k8s-docs-well-known-labels-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/reference/labels-annotations-taints/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/labels-annotations-taints/_index.md"
fetched_at: "2026-08-24T09:52:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["standard-node-labels", "node-labels", "topology-key"]
scope_note: "Targeted extraction of six entries only, to source §3's 'Kubernetes populates a standard set of labels on all nodes' claim with actual label names. The full reference page is very large and was not cached wholesale."
---
# Well-Known Labels, Annotations and Taints — selected node entries (kubernetes.io/docs/reference/labels-annotations-taints/)

> **Extraction note.** This page is a reference list with terse entries. Only
> `kubernetes.io/hostname` was returned as a clean **[VERBATIM]** description sentence.
> The remaining entries are **[PARTIAL]** — the label keys and their "Used on" targets are
> confirmed, but the description wording was condensed by the fetch. **Cite the label
> keys from this file; do not quote the [PARTIAL] descriptions as source sentences.**

## `kubernetes.io/hostname`

- Used on: Node
- **[VERBATIM]** — "The Kubelet populates this label with the hostname of the node."

## `topology.kubernetes.io/zone`

- Used on: Node, PersistentVolume
- **[PARTIAL]** — "A zone represents a logical failure domain"; populated by the kubelet
  or cloud-controller-manager.

## `topology.kubernetes.io/region`

- Used on: Node, PersistentVolume
- **[PARTIAL]** — cross-references the `topology.kubernetes.io/zone` entry; a region is a
  larger domain made up of zones.

## `kubernetes.io/os` and `kubernetes.io/arch`

- Used on: Node (and Pod, for `kubernetes.io/os`)
- **[PARTIAL]** — the kubelet populates these from the Go runtime values `runtime.GOOS`
  and `runtime.GOARCH`, to support heterogeneous clusters.

## `node.kubernetes.io/unschedulable` (taint)

- **[PARTIAL]** — "The taint will be added to a node when initializing the node to avoid
  race condition."

---

NOT IN THIS SNAPSHOT: the `node-restriction.kubernetes.io/` prefix entry was not returned
by this fetch. **It is not a gap** — that fact is already cached verbatim in
`k8s-docs-assign-pod-node-2026-08-23.md`: "the NodeRestriction admission plugin prevents
the kubelet from setting labels with a node-restriction.kubernetes.io/ prefix." Cite that
file for §3's forward-bearing to Chapter 8.
```

### A7 · `k8s-docs-node-allocatable-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/administer-cluster/reserve-compute-resources.md"
fetched_at: "2026-08-24T09:52:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["node-allocatable", "node-capacity", "requests-as-scheduling-input", "podfitsresources"]
closes_gap: "ch-07 outline Open Question #8 — 'available resources' in the PodFitsResources description is measured against allocatable, not capacity. Previously the relationship between the two words was named but not defined in any cached source."
scope_note: "Deliberately shallow. The reservation model itself (kube-reserved, system-reserved, eviction thresholds, cgroup enforcement) is Chapter 8's territory and was not extracted."
---
# Node Allocatable (kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources/)

> **Extraction note.** All passages below are **[VERBATIM]** and safe to cite.

## What Allocatable is

> 'Allocatable' on a Kubernetes node is defined as the amount of compute resources that
> are available for pods.

## What the scheduler does with it

> The scheduler treats 'Allocatable' as the available `capacity` for pods.

> The scheduler does not over-subscribe 'Allocatable'.

---

NOT IN THIS SNAPSHOT: the formula or diagram relating node Capacity to `kube-reserved`,
`system-reserved`, `eviction-threshold` and Allocatable. The source presents this as an
image (`node-capacity.svg`) with no text equivalent, so no equation is extractable. **§2
must not state an arithmetic relationship between capacity and allocatable.** The two
sentences above are sufficient for what §2 needs — that allocatable is the number the
reader should be doing arithmetic against. See research-manifest Gaps, G-7C.
```

---

## Gaps

**G-7A — No standalone definition or formula for the term *skew*.** The topology spread page defines `maxSkew` precisely (snapshot A1, quoted in full) and works an example, but never defines "skew" as a standalone term with an equation. Not blocking: §5 as planned needs the *concept* of uneven distribution across domains and the `DoNotSchedule`/`ScheduleAnyway` split, both of which are fully sourced. **Draft §5 using the `maxSkew` wording; do not compose a skew formula.**

**G-7B — The standard node label set is not enumerated on the assign-pod-node page.** That page asserts "Kubernetes also populates a standard set of labels on all nodes in a cluster" without listing them. Closed by snapshot A6, but note A6's descriptions are **[PARTIAL]** — cite the label *keys* freely, quote the *descriptions* only for `kubernetes.io/hostname`.

**G-7C — No text equivalent for the capacity-to-allocatable arithmetic.** The source presents it only as an SVG diagram. §2 gets the two sentences it needs (A7) and must not assert a formula.

**G-7D — Per-taint `NodeCondition` cross-references in the taint-based-evictions list were not captured**, and the taints page's own condition-to-taint mapping table returned only two of its rows. Not blocking: `k8s-docs-daemonset-2026-08-24.md` carries the complete seven-row built-in taint table *with effects*, which is what §4's built-in-taint block actually needs. **Cite DaemonSet for the effects, the taints page for the key names.**

**G-7E — `kubectl get pods` in its bare form is not separately sourced.** A5 gives `kubectl get pods --output=wide`. The bare verb-resource form is covered by the general grammar in `k8s-docs-kubectl-overview-2026-08-23.md`. Immaterial — the outline's restraint rule (command names freely, command lines only when sourced) is now satisfiable for all four tagged commands.

**No gap remains against the outline's `kb_tags`.** Every concept in the list is sourced, including all five that were uncached at outline time (`topology-spread-constraints`, `topology-domain`, `topology-key`, plus `scheduling-policies`/`predicates`/`priorities`, which are verified current — see note 1).

---

## Notes for the author

**1. ⚠ Open question #5 resolves *against* the outline's premise — Scheduling Policies is still presented as supported.** The outline states: *"In current upstream Kubernetes the Policy model has been removed, not merely deprecated, and the live page's framing differs."* I re-fetched the live page to check. It does not differ. The current kubernetes.io kube-scheduler page still reads, verbatim:

> There are two supported ways to configure the filtering and scoring behavior of the scheduler:
> 1. Scheduling Policies allow you to configure *Predicates* for filtering and *Priorities* for scoring.
> 2. Scheduling Profiles allow you to configure Plugins that implement different scheduling stages, including: `QueueSort`, `Filter`, `Score`, `Bind`, `Reserve`, `Permit`, and others. You can also configure the kube-scheduler to run different profiles.

This is **character-identical to the cached `k8s-docs-kube-scheduler-2026-08-23.md`**. The currency risk the outline flagged is not present *in the documentation*; the snapshot and the live page agree.

One nuance worth holding: this establishes what the *docs page* says, not what the *scheduler binary* accepts. The docs may lag the code here. **The outline's recommendation is still the right one and is now safer, not riskier** — teach Predicates and Priorities as the older vocabulary for filtering and scoring, which is true under every reading. Take that framing for the reason the outline gave (exam value, and it maps onto §1's spine), not because the snapshot is stale. **Remove the "currency risk" flag from the fact-accuracy stage's queue** — I checked it, and there is nothing to reconcile.

**2. Open question #2 closes far better than the fallback anticipated.** The outline's contingency was that §5 name topology spread constraints, state in one sentence that they are the purpose-built mechanism for even distribution, carry no field names, and stop. That contingency is no longer needed. Snapshot A1 sources the motivation narrative, all six primary fields, the `DoNotSchedule`/`ScheduleAnyway` split, cluster-level defaults, and four known limitations. §5 can now teach the block properly.

Three things in A1 are worth more than they cost:
- **The Motivation section is a ready-made §5 opening** and it arrives at the two-replicas-on-one-node problem by exactly the route Soundings question 7 sets up. It also escalates naturally into the zone case, which is the altitude jump §5 needs to make anyway.
- **The podAffinity/podAntiAffinity comparison section is the sourced version of the outline's `🪝 Snag`** — that "spread my replicas" and "never put two together" are different requirements. The source's own framing is sharper than the outline's: `requiredDuringSchedulingIgnoredDuringExecution` anti-affinity means *only a single Pod can be scheduled into a single topology domain*, and preferred means *you lose the ability to enforce the constraint*. Neither gives you "evenly, within a tolerance."
- **The scale-to-zero limitation is a live Chapter 17 hook** — topology domains "won't be considered until there is at least one node in them." Tempting, and it should be resisted: it names autoscaler behaviour, which is B3's second decay anchor. Leave it.

**3. Open question #10 closes; the outline's restraint rule can now be relaxed deliberately rather than by necessity.** All four tagged commands now have sourced argument syntax: `kubectl taint nodes node1 key1=value1:NoSchedule` and its removal form with the trailing minus (A2); `kubectl get nodes`, `kubectl get nodes --show-labels`, `kubectl label nodes <your-node-name> disktype=ssd`, `kubectl get pods --output=wide` (A5). **This does not oblige the chapter to use them.** The outline's scope argument for restraint — Chapter 8 owns the command surface — is unaffected by sources existing. My read: the trailing-minus removal form is the one genuinely worth a line, because it is the kind of small concrete detail that makes a taint feel like a thing you can put on and take off, and it costs one clause. The rest can stay as command names.

**4. Bearings #2 item 2's answer key is now sourced, which the outline expected it would not be.** The outline says the taint-plus-affinity complementarity "is not stated as a rule in any cached source, so the key is where it becomes explicit." It is now stated, in the docs' own words (A2, Dedicated Nodes): if you want pods to use the dedicated nodes *and only* those nodes, you must additionally label the nodes and add a node affinity requiring that label. The key can now cite rather than assert. This also strengthens the §4 `⚠ Navigational Hazards` beat and the `Logbook Entry` GPU scenario — the special-hardware use case is sourced in A2 too, and the docs frame it exactly as the outline wanted (keep pods that don't need the hardware *off*, leaving room for later arrivals that do).

**5. Open question #3 — preemption is now properly sourced, and I'd still spend only one clause.** A4 gives clean quotable definitions. The outline's instinct was right and the new source does not change the arithmetic: teaching preemption means teaching PriorityClass, and A4 deliberately stops short of that. What the source *does* now let §2 do is make the one clause accurate instead of vague — "if a Pod cannot be scheduled, the scheduler tries to preempt (evict) lower priority Pods to make scheduling of the pending Pod possible" is one sentence, is citable, and closes the honesty gap the outline was worried about without opening the mechanics.

One precision hazard if the clause is written: A4's framing is that preemption triggers *when no node satisfies the Pod's requirements* — i.e. it sits at exactly the same moment as §2's "the Pod stays Pending." The two facts are adjacent and a careless sentence will imply that Pending Pods routinely trigger evictions. **Phrase it as the exception, and keep §2's Fixed Point (the Pod waits, indefinitely, nothing times out) as the rule.** Chapter 13's anchor depends on that Fixed Point surviving intact.

**6. Open question #6's concession is now available if wanted.** The outline identified the `nodeSelectorTerms`-are-ORed / `matchExpressions`-are-ANDed rule as "the single most useful piece of the omitted set" but noted it needed a source line the snapshot did not contain. A3 supplies both sentences verbatim. Also now sourced: `weight` is "between 1 and 100" and how the sum feeds scoring. **My read: take the OR/AND rule if anything, skip the weight arithmetic.** The OR/AND rule is a comprehension fact about how a spec is read; the weight arithmetic is a scoring implementation detail, and the outline's ceiling argument for excluding it stands unchanged.

**7. `nodeName`'s failure mode is more specific than the outline assumed, and the detail is worth having.** The outline says the Pod "simply fails." A3 gives three distinct documented caveats, and the middle one names the observable: if the named node lacks resources, "the Pod will fail and its reason will indicate why, for example OutOfmemory or OutOfcpu." That is materially better for **Bearings #3 item 3**, whose whole point is that this failure does *not* look like `Pending`. The key can now name what it looks like instead. Note also the first caveat — a Pod naming a nonexistent node "will not run, and in some cases may be automatically deleted" — which is a second non-`Pending` outcome and a legitimate distractor.

**8. §5's large-cluster caveat is sourced and should stay in.** The outline hedged it — "not in the cached snapshot either; it needs the same fetch or must be cut." A3 has it verbatim: "Inter-pod affinity and anti-affinity require substantial amounts of processing which can slow down scheduling in large clusters significantly. We do not recommend using them in clusters larger than several hundred nodes." That is a firmer statement than the outline's paraphrase ("recommend against them in very large clusters") and it justifies §5's 🟡 rating and its closing "this is a sharp tool" beat. The `🔭 Closer Look` on why it is expensive is authored reasoning, not sourced — the docs assert the cost without explaining the mechanism. Mark it as authored colour or drop the causal explanation and keep the assertion.

**9. ⚠ Chapter 6 is not shipped at all — this is worse than the outline's open question #11 described, and it affects three mandatory cross-bearings.** The outline reports that `chapter-06-fleets-not-vessels.md` "currently contains only Practice Questions, Chapter Summary and The Voyage Ahead — roughly the last 30%." That is no longer accurate. **The file does not exist.** `Book-KCNA/` currently ships chapters 01 through 05 only, and `.pipeline-state/ch-06/` contains just `outline.md` and `research-manifest.md` — no draft at any version.

The consequence for this chapter is specific and worth stating plainly, because the outline builds on the opposite assumption:

- The outline says *"The Voyage Ahead is present and is quotable, so §1's opening beat and §4's DaemonSet callback are safe."* **Neither is safe.** Chapter 6's Voyage Ahead does not exist in shipped text. §1's opening beat ("collect Chapter 6's Voyage Ahead in one clause") and §4's DaemonSet callback (**mandatory**, per the outline) both currently point at nothing.
- The two back-bearings to Ch 6 §1 and Ch 6 §7 are unverifiable for the same reason, which the outline did anticipate.

This is a **sequencing** problem, not a research problem, and it is the author's call rather than mine. The honest options are to draft Chapter 6 before Chapter 7, or to draft Chapter 7 against the ch-06 *outline's* planned numbering (§1 The Resource That Holds the Intent, §7 One Per Node and Work That Ends) and accept a re-verification pass afterwards. **Flagging it rather than choosing.** Note that Chapter 6's outline and research manifest are both complete and in good shape, so the ordering is cheap to fix if that is the preference.

**10. The four published cross-bearings into this chapter are verified present and read exactly as the outline describes them.** I checked all four against shipped text rather than trusting the outline:

- `chapter-05` line 969 — *"requests are the input to the scheduler's filtering step `*[cross-bearing: see Ch 7 §2 — resource requests as a scheduling filter]*`"* ✓ Confirmed. The §2 pin is real and honored.
- `chapter-03` line 417 — *"the scheduler selects a node and records that choice. It does not start anything… That split will look familiar by the end of §6"* followed by `*[cross-bearing: see Ch 7 — how the scheduler actually chooses, in detail]*` ✓ Confirmed, unnumbered, and the binding sentence is already stated well enough that §1 should genuinely collect rather than re-argue it.
- `chapter-04` line 688 — *"Node scheduling constraints use labels on nodes… `*[cross-bearing: see Ch 7 — node labels and nodeSelector]*`"* ✓ Confirmed, unnumbered. Worth noting the surrounding `⚓ Worth Securing` explicitly promises the reader that "ReplicaSet, Service, NetworkPolicy, and node affinity are not four mechanisms to learn. They are one mechanism." **§3's direction-inversion beat is discharging a promise Chapter 4 made in stronger terms than the outline records.**
- `chapter-02` line 807 — *"`*[cross-bearing: see Ch 7 §3 — node selection, tolerations, and accounting for overhead]*`"* ✓ Confirmed, and the outline's diagnosis is correct: the pointer names three topics that land in §2, §3 and §4. The recommended one-token fix (drop `§3`) is accurate and mechanical — the line otherwise reads correctly and the surrounding sentence already says "scheduling has its own chapter," which the unnumbered form matches better anyway.

**11. Version currency.** All seven new snapshots were fetched 2026-08-24 from current Kubernetes documentation. Five were taken from the project's own CC BY 4.0 markdown source files in `kubernetes/website` rather than the rendered pages, because the rendered pages truncated before the sections this chapter needs; the `source_raw` field in each frontmatter records which. Content is identical — the raw files are what kubernetes.io renders. No version skew was observed between the 08-23 and 08-24 snapshot sets, and no fetched page carried a version gate (`v1.xx [stable]` or similar) on any fact this chapter uses.

**12. One process note on this run.** Several fetches initially returned refusals or heavy paraphrase from the extraction layer rather than quotable text. Where a passage came back condensed rather than quoted, I marked it **[PARTIAL]** in the snapshot and said so at the point of use, rather than smoothing it into prose that would look verbatim to a downstream audit. **The `[VERBATIM]` / `[PARTIAL]` distinction in these seven files is load-bearing** — the fact-accuracy stage should treat `[PARTIAL]` blocks as existence-confirmation only, not as quotable evidence. Every fact this chapter's outline actually depends on landed as `[VERBATIM]`.
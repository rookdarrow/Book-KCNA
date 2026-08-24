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

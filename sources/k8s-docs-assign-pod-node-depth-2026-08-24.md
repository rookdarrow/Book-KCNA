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

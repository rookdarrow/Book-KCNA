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

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

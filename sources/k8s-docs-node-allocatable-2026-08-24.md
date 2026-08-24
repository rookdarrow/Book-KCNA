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

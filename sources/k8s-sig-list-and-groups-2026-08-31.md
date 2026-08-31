---
source_url: "https://github.com/kubernetes/community/blob/master/sig-list.md"
fetched_at: "2026-08-31T09:55:00-0400"
authority: "Kubernetes project (kubernetes/community)"
objectives_covered: ["D4.3"]
concepts_covered: ["kubernetes-sig", "kubernetes-working-group", "kubernetes-committee", "steering-committee", "subproject"]
---
# Kubernetes SIGs, Working Groups and Committees — the actual roster

`k8s-community-governance-2026-08-23.md` supplies the DEFINITIONS. This supplies
the ROSTER, which is what makes §8's three-way distinction concrete instead of
abstract — and it is the source for the D4.3 Soundings question (Q7).

## Framing — verbatim

> "Most community activity is organized into Special Interest Groups (SIGs) and
> time bounded Working Groups."

> "SIGs follow these guidelines although each of these groups may operate a
> little differently depending on their needs and workflow."

## Special Interest Groups, as listed on this page (2026-08-31)

API Machinery · Apps · Architecture · Auth · Autoscaling · CLI · Cloud Provider ·
Cluster Lifecycle · Contributor Experience · Docs · etcd · Instrumentation ·
K8s Infra · Multicluster · Network · Node · Release · Scalability · Scheduling ·
Security · Storage · Testing · UI · Windows

## Working Groups, as listed on this page (2026-08-31)

AI Gateway · Batch · Checkpoint Restore · Data Protection · Device Management ·
etcd Operator · Node Lifecycle · Workload-aware Scheduling

## Committees, as listed on this page (2026-08-31)

Code of Conduct · Security Response · Steering

---
DRAFTING NOTES (not from source):

**1. There are exactly three Committees, and Steering is one of them.** That is a
sharper structural fact than the outline's §8 plan assumes, which treats Steering
as a separate fourth body. Both framings are defensible — the governance doc says
Committees "are formed by the steering committee", which cannot be true of
Steering itself — but a reader who opens sig-list.md will see three Committees
with Steering among them. Recommend §8 says Committees are closed-membership
bodies, names all three, and notes that Steering holds overall governance and
charters the other two. That is both accurate and more memorable than an org
chart.

**2. Three SIGs in this list are ones the reader has already met by name in this
book** — Release (Ch 8, and §8 here), Autoscaling (§7 here, via Karpenter and
Cluster Autoscaler), Storage/Network/Node (Ch 9, Ch 11, Ch 2). §8's "how you'd
join" half becomes concrete for free: the reader can be told that the interfaces
they learned in Chapters 2, 9 and 11 each have a SIG behind them with a public
meeting. That is the cheapest possible bridge from §8 to §9's pluggability claim,
and it costs one sentence.

**3. "time bounded Working Groups"** is the source's own phrasing and is a
tighter formulation than "short-lived" for the SIG/WG contrast.

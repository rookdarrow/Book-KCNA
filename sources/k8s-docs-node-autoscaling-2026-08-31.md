---
source_url: "https://kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/"
fetched_at: "2026-08-31T09:50:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D4.2"]
concepts_covered: ["node-autoscaling", "cluster-autoscaler", "karpenter", "horizontal-vs-vertical-autoscaling"]
---
# Node Autoscaling (kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/)

The dedicated node-autoscaling page. `k8s-docs-autoscaling-2026-08-23.md` covers
node autoscaling in a single closing sentence; this is the substance behind it,
and it is where §7's Ch 7 §2 retrieval anchor is sourced.

## Opening definition — verbatim

> "Automatically provision and consolidate the Nodes in your cluster to adapt to
> demand and optimize cost."

## Provisioning, and what triggers it — verbatim

> "If there are Pods in a cluster that can't be scheduled on existing Nodes, new
> Nodes can be automatically added to the cluster—_provisioned_—to accommodate
> the Pods."

## Consolidation — verbatim

> "Nodes in your cluster can be automatically _consolidated_ in order to improve
> the overall Node utilization, and in turn the cost-effectiveness of the
> cluster. Consolidation happens through removing a set of underutilized Nodes
> from the cluster."

## Interaction with the cloud provider — verbatim

> "In addition to the Kubernetes API, autoscalers also need to interact with
> cloud provider APIs to provision and consolidate Nodes."

## Implementations — verbatim

> "[Cluster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler)
> and [Karpenter](https://github.com/kubernetes-sigs/karpenter) are the two Node
> autoscalers currently sponsored by
> [SIG Autoscaling](https://github.com/kubernetes/community/tree/main/sig-autoscaling)."

> "Cluster Autoscaler adds or removes Nodes to pre-configured _Node groups_."

> "From the perspective of a cluster user, both autoscalers should provide a
> similar Node autoscaling experience. Both will provision new Nodes for
> unschedulable Pods, and both will consolidate the Nodes that are no longer
> optimally utilized."

> "Different autoscalers may also provide features outside the Node autoscaling
> scope described on this page, and those additional features may differ between
> them."

## Not captured

The page's `#karpenter` subsection body was truncated by the fetch tool across
three attempts. Karpenter's own description is captured separately in
`karpenter-concepts-2026-08-31.md`.

---
DRAFTING NOTE (not from source): "Pods in a cluster that can't be scheduled on
existing Nodes" is the second half of the sentence Ch 7:428 left open. This
snapshot is the tag for that retrieval anchor. Note also that this page is the
sourced answer to Open Question 5 — Karpenter's affiliation is SIG AUTOSCALING,
a Kubernetes SIG. Nothing here or anywhere in the official corpus assigns
Karpenter a CNCF maturity level.

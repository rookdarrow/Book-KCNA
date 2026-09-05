---
source_url: "https://kubernetes.io/docs/reference/scheduling/config/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/scheduling/config.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), reference page for kube-scheduler configuration, CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["scheduling-profiles", "scheduler-plugins", "extension-points", "filter-extension-point", "score-extension-point", "bind-extension-point", "predicates-as-filters", "taint-toleration-plugin", "node-affinity-plugin", "inter-pod-affinity-plugin", "pod-topology-spread-plugin", "node-resources-fit-plugin", "node-name-plugin", "node-unschedulable-plugin"]
closes_gap: "ch-07 §7 stage assignment (AUTHOR-REVIEW at the Zenith figure, 2026-09-03 draft): the only primary source that enumerates each placement mechanism against the scheduler stage that implements it. Also closes gap G-7G's alternate fetch (the scheduler-config plugin reference)."
---

# Scheduler Configuration (kubernetes.io/docs/reference/scheduling/config/)

Feature state on the page: `stable` since Kubernetes v1.25 (KubeSchedulerConfiguration v1).

All passages below are **[VERBATIM]** from the raw page markdown, with Hugo shortcodes and
in-page links removed.

## Profiles

> A scheduling Profile allows you to configure the different stages of scheduling
> in the kube-scheduler. Each stage is exposed in an extension point. Plugins provide
> scheduling behaviors by implementing one or more of these extension points.

> You can configure a single instance of `kube-scheduler` to run multiple profiles.

## Extension points (the ones the chapter names)

> Scheduling happens in a series of stages that are exposed through the following
> extension points:

> `queueSort`: These plugins provide an ordering function that is used to sort pending
> Pods in the scheduling queue. Exactly one queue sort plugin may be enabled at a time.

> `preFilter`: These plugins are used to pre-process or check information about a Pod
> or the cluster before filtering. They can mark a pod as unschedulable.

> `filter`: These plugins are the equivalent of Predicates in a scheduling Policy and
> are used to filter out nodes that can not run the Pod. Filters are called in the
> configured order. A pod is marked as unschedulable if no nodes pass all the filters.

> `score`: These plugins provide a score to each node that has passed the filtering
> phase. The scheduler will then select the node with the highest weighted scores sum.

> `reserve`: This is an informational extension point that notifies plugins when
> resources have been reserved for a given Pod. Plugins also implement an `Unreserve`
> call that gets called in the case of failure during or after `Reserve`.

> `permit`: These plugins can prevent or delay the binding of a Pod.

> `bind`: The plugins bind a Pod to a Node. `bind` plugins are called in order and once
> one has done the binding, the remaining plugins are skipped. At least one bind plugin
> is required.

## Scheduling plugins (enabled by default) — the entries the chapter relies on

> The following plugins, enabled by default, implement one or more of these extension
> points:

> `ImageLocality`: Favors nodes that already have the container images that the Pod
> runs. Extension points: `score`.

> `TaintToleration`: Implements taints and tolerations. Implements extension points:
> `filter`, `preScore`, `score`.

> `NodeName`: Checks if a Pod spec node name matches the current node. Extension
> points: `filter`.

> `NodeAffinity`: Implements node selectors and node affinity. Extension points:
> `filter`, `score`.

> `PodTopologySpread`: Implements Pod topology spread. Extension points: `preFilter`,
> `filter`, `preScore`, `score`.

> `NodeUnschedulable`: Filters out nodes that have `.spec.unschedulable` set to true.
> Extension points: `filter`.

> `NodeResourcesFit`: For pod-by-pod scheduling checks if the node has all the resources
> that the Pod is requesting. The score can use one of three strategies:
> `LeastAllocated` (default), `MostAllocated` and `RequestedToCapacityRatio`.
> [...] Extension points: `preFilter`, `filter`, `score`, `placementScore`.

> `NodeResourcesBalancedAllocation`: Favors nodes that would obtain a more balanced
> resource usage if the Pod is scheduled there. Extension points: `score`.

> `InterPodAffinity`: Implements inter-Pod affinity and anti-affinity. Extension points:
> `preFilter`, `filter`, `preScore`, `score`.

> `PrioritySort`: Provides the default priority based sorting. Extension points:
> `queueSort`.

> `DefaultBinder`: Provides the default binding mechanism. Extension points: `bind`.

> `DefaultPreemption`: Provides the default preemption mechanism. Extension points:
> `postFilter`, `podGroupPostFilter`.

## Reading note for ch-07

The page does not say "hard rules filter, soft rules score" in those words. What it
states is that every placement mechanism the chapter teaches — taints and tolerations,
`nodeSelector` and node affinity, inter-Pod affinity and anti-affinity, topology spread,
and the requests-against-allocatable fit — is implemented by a plugin registered at the
`filter` extension point, the `score` extension point, or both. `NodeName` is registered
at `filter` only; the concept page (`k8s-docs-assign-pod-node-2026-08-23.md`) is the
source for the statement that a Pod with `nodeName` already set is ignored by the
scheduler.

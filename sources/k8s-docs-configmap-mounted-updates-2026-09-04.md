---
source_url: "https://kubernetes.io/docs/concepts/configuration/configmap/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors. Transcribed from the page's canonical Markdown source at github.com/kubernetes/website/blob/main/content/en/docs/concepts/configuration/configmap.md"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["configmap", "configmap-consumption-paths", "configmap-volume-updates", "kubelet-sync-period", "subpath", "environment-variables"]
---

# ConfigMaps — how updates reach a running Pod (kubernetes.io/docs/concepts/configuration/configmap/)

> **Snapshot note (not source text).** This snapshot COMPLEMENTS `k8s-docs-configmap-2026-08-23.md`,
> which was packed before the page's "Mounted ConfigMaps are updated automatically" section and so
> carries only the four-consumption-path summary. The two snapshots share a source_url by design.
> Only sentences verified against the canonical Markdown source are transcribed here; the Hugo
> `{{< note >}}` shortcode wrapping the subPath sentence has been removed and the wording kept verbatim.

## ConfigMaps and Pods

"These different methods lend themselves to different ways of modeling the data being consumed. For the first three methods, the kubelet uses the data from the ConfigMap when it launches container(s) for a Pod."

## Using ConfigMaps as files from a Pod

"A container using a ConfigMap as a subPath volume mount will not receive ConfigMap updates."

## Mounted ConfigMaps are updated automatically

"When a ConfigMap currently consumed in a volume is updated, projected keys are eventually updated as well. The kubelet checks whether the mounted ConfigMap is fresh on every periodic sync. However, the kubelet uses its local cache for getting the current value of the ConfigMap. The type of the cache is configurable using the `configMapAndSecretChangeDetectionStrategy` field in the KubeletConfiguration struct. A ConfigMap can be either propagated by watch (default), ttl-based, or by redirecting all requests directly to the API server. As a result, the total delay from the moment when the ConfigMap is updated to the moment when new keys are projected to the Pod can be as long as the kubelet sync period + cache propagation delay, where the cache propagation delay depends on the chosen cache type (it equals to watch propagation delay, ttl of cache, or zero correspondingly)."

"ConfigMaps consumed as environment variables are not updated automatically and require a pod restart."

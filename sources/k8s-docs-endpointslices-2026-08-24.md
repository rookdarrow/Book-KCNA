---
source_url: "https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/"
source_url_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/services-networking/endpoint-slices.md"
fetched_at: "2026-08-24T14:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.1", "D2 Networking"]
concepts_covered: ["endpointslice", "endpointslice-controller", "readiness-gated-membership", "terminating-endpoint", "service-name-label", "owner-reference", "manually-managed-endpointslice"]
---
# EndpointSlices (kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

> **Snapshot note.** Fetched to close Chapter 9 § Open questions **#4** — EndpointSlice
> previously had no source of its own, and §4's claims were sourceable only from five
> snapshots in combination. Transcribed from the rendered page and cross-checked against
> the canonical Markdown source in github.com/kubernetes/website.
>
> Trimmed as out of scope for Chapter 9: the "Topology information" section, the custom /
> manually-authored EndpointSlice YAML, and the dual-stack discussion beyond the bare
> two-value address-type list. Elisions are marked. Hugo `{{< feature-state >}}` shortcodes
> are retained where they qualify a condition's stability, because §4's Closer Look may need
> to know these are stable rather than beta.

## Opening

The EndpointSlice API is the mechanism that Kubernetes uses to let your Service scale to handle large numbers of backends, and allows the cluster to update its list of healthy backends efficiently.

EndpointSlices track the IP addresses of backend endpoints. EndpointSlices are normally associated with a Service and the backend endpoints typically represent Pods.

## EndpointSlice API

{{< feature-state for_k8s_version="v1.21" state="stable" >}}

In Kubernetes, an EndpointSlice contains references to a set of network endpoints. The control plane automatically creates EndpointSlices for any Kubernetes Service that has a selector specified. These EndpointSlices include references to all the Pods that match the Service selector.

EndpointSlices act as the source of truth for kube-proxy when it comes to how to route internal traffic.

### Address types

EndpointSlices support two address types:

* IPv4
* IPv6

Each `EndpointSlice` object represents a specific IP address type.

[Dual-stack discussion beyond this list trimmed as out of scope — see § Open questions #9,
which records dual-stack as a deliberate omission at associate tier.]

## Ownership

In most use cases, EndpointSlices are owned by the Service that the endpoint slice object tracks endpoints for. This ownership is indicated by an owner reference on each EndpointSlice as well as a `kubernetes.io/service-name` label that enables simple lookups of all EndpointSlices belonging to a Service.

## Conditions

The EndpointSlice API stores conditions about endpoints that may be useful for consumers. The three conditions are `serving`, `terminating`, and `ready`.

### Ready

The `ready` condition is essentially a shortcut for checking "`serving` and not `terminating`" (though it will also always be `true` for Services with `spec.publishNotReadyAddresses` set to `true`).

### Serving

{{< feature-state for_k8s_version="v1.26" state="stable" >}}

The `serving` condition indicates that the endpoint is currently serving responses, and so it should be used as a target for Service traffic. For endpoints backed by a Pod, this maps to the Pod's `Ready` condition.

### Terminating

{{< feature-state for_k8s_version="v1.26" state="stable" >}}

The `terminating` condition indicates that the endpoint is terminating. For endpoints backed by a Pod, this condition is set when the Pod is first deleted (that is, when it receives a deletion timestamp, but most likely before the Pod's containers exit).

Service proxies will normally ignore endpoints that are `terminating`, but they may route traffic to endpoints that are both `serving` and `terminating` if all available endpoints are `terminating`. (This helps to ensure that no Service traffic is lost during rolling updates of the underlying Pods.)

[Topology information section trimmed as out of scope for Chapter 9.]

## Distribution of EndpointSlices

By default, the control plane creates and manages EndpointSlices to have no more than 100 endpoints each. You can configure this with the `--max-endpoints-per-slice` kube-controller-manager flag, up to a maximum of 1000.

With kube-proxy running on each Node and watching EndpointSlices, every change to an EndpointSlice becomes relatively expensive since it will be transmitted to every Node in the cluster. This approach is intended to limit the number of changes that need to be sent to every Node, even if it may result with multiple EndpointSlices that are not full.

The control plane tries to fill EndpointSlices as full as possible, but does not actively rebalance them.

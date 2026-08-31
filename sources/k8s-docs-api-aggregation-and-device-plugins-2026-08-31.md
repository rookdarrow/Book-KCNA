---
source_url: "https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/apiserver-aggregation/"
fetched_at: "2026-08-31T09:52:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — two pages, attributed inline"
objectives_covered: ["D4.2"]
concepts_covered: ["api-aggregation-layer", "device-plugin", "extension-point", "four-pluggable-interfaces"]
---
# The aggregation layer and device plugins — the two §4 extension points with no snapshot

`k8s-docs-extending-kubernetes-2026-08-23.md` names both in its six-extension-point
list but does not define either. Both are in this chapter's kb_tags and both
appear in the table that sits beside `ch17-fig02-extension-points-map`.

## Source A — API aggregation layer (kubernetes.io/docs/concepts/extend-kubernetes/api-extension/apiserver-aggregation/), verbatim

> "The aggregation layer allows Kubernetes to be extended with additional APIs,
> beyond what is offered by the core Kubernetes APIs."

> "The aggregation layer runs in-process with the kube-apiserver. Until an
> extension resource is registered, the aggregation layer will do nothing. To
> register an API, you add an _APIService_ object, which 'claims' the URL path in
> the Kubernetes API. At that point, the aggregation layer will proxy anything
> sent to that API path (e.g. `/apis/myextension.mycompany.io/v1/…`) to the
> registered APIService."

> "The aggregation layer is different from Custom Resource Definitions, which are
> a way to make the kube-apiserver recognise new kinds of object."

## Source B — Device plugins (kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/), verbatim

> "Device plugins let you configure your cluster with support for devices or
> resources that require vendor-specific setup, such as GPUs, NICs, FPGAs, or
> non-volatile main memory."

> "Kubernetes provides a device plugin framework that you can use to advertise
> system hardware resources to the Kubelet."

> "The targeted devices include GPUs, high-performance NICs, FPGAs, InfiniBand
> adapters, and other similar computing resources that may require vendor
> specific initialization and setup."

> "the device plugin sends the kubelet the list of devices it manages, and the
> kubelet is then in charge of advertising those resources to the API server as
> part of the kubelet node status update"

[Paraphrase, NOT verbatim: the kubelet exports a `Registration` gRPC service; a
device plugin registers itself through it, sending the name of its Unix socket,
the Device Plugin API version, and the `ResourceName` it wants to advertise,
following the extended-resource naming scheme `vendor-domain/resourcetype`.]

---
DRAFTING NOTE (not from source): the aggregation-layer page's closing sentence —
"The aggregation layer is different from Custom Resource Definitions" — is
load-bearing for §4. It is the documentation itself distinguishing the two
API-extension routes, which is precisely why Ch 2 §4's "API extensions" label and
Ch 6 §8's "CRDs" label are both defensible and neither is wrong. §4's
one-clause reconciliation can be written straight off this sentence. The device
plugin's "advertise system hardware resources to the Kubelet" is the same
interface-and-implementation shape as CRI/CNI/CSI, one layer over — useful for
§9 as evidence, but the ordinal rule still bars counting past four.

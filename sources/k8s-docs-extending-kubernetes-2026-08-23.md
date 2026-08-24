---
source_url: "https://kubernetes.io/docs/concepts/extend-kubernetes/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D2 Storage", "D2 Networking", "D1 Containerization"]
concepts_covered: ["extension-points", "cri", "cni", "csi", "device-plugins", "webhooks", "admission-control", "crd", "api-aggregation", "scheduler-extensions"]
---
# Extending Kubernetes (kubernetes.io/docs/concepts/extend-kubernetes/)

Kubernetes is highly configurable and extensible. As a result, there is rarely a need to fork or submit patches to the Kubernetes project code. Configuration means changing flags, local configuration files, or API resources (such as ResourceQuota, NetworkPolicy and RBAC); extensions are software components that extend and deeply integrate with Kubernetes, adapting it to support new types and new kinds of hardware.

## Extension patterns
- Controllers — client programs that read and/or write to the Kubernetes API, following a control loop: read an object's .spec, possibly do things, and then update the object's .status.
- Webhooks — Kubernetes makes synchronous HTTP requests to a remote service (a webhook backend); this adds a potential point of failure.
- Binary plugins — Kubernetes executes external binaries; used by the kubelet (CSI storage plugins, CNI network plugins) and by kubectl (plugins).

## Extension points
1. kubectl plugins and client credential providers.
2. API access extensions — authentication, authorization, dynamic admission control (webhooks).
3. API extensions — Custom Resource Definitions (CRDs) and the API aggregation layer.
4. Scheduling extensions — scheduler plugins/profiles and custom schedulers.
5. Controllers — custom controllers managing custom or built-in resources; the operator pattern.
6. Infrastructure extensions — Device Plugins (custom hardware); Storage plugins (CSI, the Container Storage Interface, to add new storage types); Network plugins (CNI, the Container Network Interface, to implement pod networking); Container runtime (CRI, the Container Runtime Interface, to support alternative container runtimes); kubelet image credential provider plugins.

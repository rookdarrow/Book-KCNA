---
source_url: "https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer"
source_url_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/services-networking/service.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.1", "D2 Networking"]
concepts_covered: ["loadbalancer", "service-type-ladder", "nodeport", "clusterip", "cloud-controller-manager", "status-loadbalancer"]
---
# Service — the `type: LoadBalancer` subsection (kubernetes.io/docs/concepts/services-networking/service/)

> **Snapshot note.** Fetched 2026-09-04 during the Chapter 9 audit from the canonical Markdown
> source in github.com/kubernetes/website (main). Third companion to
> `k8s-docs-service-2026-08-23.md` and `k8s-docs-service-ports-2026-08-24.md`, covering the one
> subsection neither of them carried. Transcribed verbatim; the YAML example and the
> `loadBalancerIP` / `allocateLoadBalancerNodePorts` / `ipMode` material that follows are out of
> scope for Chapter 9 and are not transcribed.
>
> **Verification note.** The sentence recorded in `k8s-docs-service-ports-2026-08-24.md` under
> "Transcription variance" ("Note that Service of type NodePort and type LoadBalancer are
> supersets of ClusterIP") does **not** appear anywhere on the live page as of this fetch; a
> search of the full source for "superset" returns nothing. The additivity of the three ladder
> types is instead supported by the two sentences below, read together with the NodePort entry
> in `k8s-docs-service-2026-08-23.md` ("To make the node port available, Kubernetes sets up a
> cluster IP address, the same as if you had requested a Service of type: ClusterIP").

## `type: LoadBalancer`

"On cloud providers which support external load balancers, setting the `type` field to `LoadBalancer` provisions a load balancer for your Service. The actual creation of the load balancer happens asynchronously, and information about the provisioned balancer is published in the Service's `.status.loadBalancer` field."

"Traffic from the external load balancer is directed at the backend Pods. The cloud provider decides how it is load balanced."

"To implement a Service of `type: LoadBalancer`, Kubernetes typically starts off by making the changes that are equivalent to you requesting a Service of `type: NodePort`. The cloud-controller-manager component then configures the external load balancer to forward traffic to that assigned node port."

"You can configure a load balanced Service to omit assigning a node port, provided that the cloud provider implementation supports this."

## `type: NodePort` (lead sentences, for corroboration of the range)

"If you set the `type` field to `NodePort`, the Kubernetes control plane allocates a port from a range specified by `--service-node-port-range` flag (default: 30000-32767). Each node proxies that port (the same port number on every Node) into your Service. Your Service reports the allocated port in its `.spec.ports[*].nodePort` field."

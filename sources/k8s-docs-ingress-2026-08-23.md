---
source_url: "https://kubernetes.io/docs/concepts/services-networking/ingress/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Networking"]
concepts_covered: ["ingress", "ingress-controller", "gateway-api", "http-routing", "tls-termination", "name-based-virtual-hosting"]
---
# Ingress (kubernetes.io/docs/concepts/services-networking/ingress/)

## Terminology
Node — a worker machine in Kubernetes, part of a cluster. Cluster — a set of Nodes that run containerized applications managed by Kubernetes; nodes in the cluster are not part of the public internet. Edge router — a router that enforces the firewall policy for your cluster (a gateway managed by a cloud provider or a physical piece of hardware). Cluster network — a set of links, logical or physical, that facilitate communication within a cluster according to the Kubernetes networking model. Service — a Kubernetes Service that identifies a set of Pods using label selectors; Services are assumed to have virtual IPs only routable within the cluster network.

## What is Ingress?
Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource. An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL / TLS, and offer name-based virtual hosting. An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends to help handle the traffic. An Ingress does not expose arbitrary ports or protocols. Exposing services other than HTTP and HTTPS to the internet typically uses a service of type Service.Type=NodePort or Service.Type=LoadBalancer.

Note: The Kubernetes project recommends using Gateway instead of Ingress. The Ingress API has been frozen: it is generally available and subject to the stability guarantees for GA APIs — the project has no plans to remove Ingress — but it is no longer being developed and will have no further changes or updates.

## Prerequisites
You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect. Ideally, all Ingress controllers should fit the reference specification; in reality, the various Ingress controllers operate slightly differently.

## Types of Ingress
Ingress backed by a single Service; simple fanout (routes traffic from a single IP address to more than one Service, based on the HTTP URI); name based virtual hosting (routing HTTP traffic to multiple host names at the same IP address); TLS (secure an Ingress by specifying a Secret that contains a TLS private key and certificate); load balancing.

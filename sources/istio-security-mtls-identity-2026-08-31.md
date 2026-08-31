---
source_url: "https://istio.io/latest/docs/concepts/security/"
fetched_at: "2026-08-31T09:48:00-0400"
authority: "Istio project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["mutual-tls", "zero-trust", "mesh-control-plane", "mesh-data-plane", "envoy", "service-mesh"]
---
# Istio — Security concepts (istio.io/latest/docs/concepts/security/)

Closes the outline's gap: `istio-service-mesh-2026-08-23.md` supports mTLS and
zero trust only at slogan depth. Direct quotations follow.

## Goals of Istio security — verbatim

> "The goals of Istio security are: Security by default: no changes needed to
> application code and infrastructure; Defense in depth: integrate with existing
> security systems to provide multiple layers of defense; Zero-trust network:
> build security solutions on distrusted networks."

## High-level architecture — verbatim

> "Security in Istio involves multiple components: A Certificate Authority (CA)
> for key and certificate management; The configuration API server distributes to
> the proxies: authentication policies, authorization policies, secure naming
> information; Sidecar and perimeter proxies work as Policy Enforcement Points
> (PEPs) to secure communication between clients and servers."

## Istio identity — verbatim

> "The Istio identity model uses the first-class `service identity` to determine
> the identity of a request's origin. This model allows for great flexibility and
> granularity for service identities to represent a human user, an individual
> workload, or a group of workloads."

## Mutual TLS authentication — verbatim

> "When a workload sends a request to another workload using mutual TLS
> authentication, the request is handled as follows: 1) Istio re-routes the
> outbound traffic from a client to the client's local sidecar Envoy; 2) The
> client side Envoy starts a mutual TLS handshake with the server side
> Envoy... 3) The client side Envoy and the server side Envoy establish a mutual
> TLS connection; 4) The server side Envoy authorizes the request."

## Permissive mode — verbatim

> "With the permissive mode enabled, the server accepts both plaintext and mutual
> TLS traffic. The mode provides greater flexibility for the on-boarding process."

---
DRAFTING NOTE (not from source): "The configuration API server distributes to the
proxies" is the mesh's control plane doing its job, stated in the source's own
words. This sentence is the cleanest available defusal of trap #101 — the mesh's
control plane distributes policy TO PROXIES, which is visibly a different job
from the cluster control plane of Ch 3 §2. Scope guardrail still applies: teach
what a mesh is and buys. Do NOT teach PeerAuthentication, AuthorizationPolicy,
VirtualService or DestinationRule — permissive mode above is a *concept* the
prose may name in a clause, not a resource to configure.

---
source_url: "https://glossary.cncf.io/service-mesh/"
fetched_at: "2026-08-31T09:40:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["service-mesh", "mesh-data-plane", "sidecar-mode", "microservices"]
---
# CNCF Cloud Native Glossary — Service Mesh (verbatim, complete)

This is the VENDOR-NEUTRAL definition, to be quoted beside Istio's. The two agree
on the substance and differ in framing: CNCF says "without requiring code
changes"; Istio says "without code changes".

## Service Mesh

In a microservices world, apps are broken down into multiple smaller services
that communicate over a network. Just like your wifi network, computer networks
are intrinsically unreliable, hackable, and often slow. Service meshes address
this new set of challenges by managing traffic (i.e., communication) between
services and adding reliability, observability, and security features uniformly
across all services.

## Problem it addresses

Having moved to a microservices architecture, engineers are now dealing with
hundreds, possibly even thousands of individual services, all needing to
communicate. That means a lot of traffic is going back and forth over the
network. On top of that, individual applications may need to encrypt
communications to support regulatory requirements, provide common metrics to
operations teams, or provide detailed insight into traffic to help diagnose
issues. If built into the individual applications, each one of these features
will cause friction between teams and slow down development of new features.

## How it helps

Service meshes add reliability, observability, and security features uniformly
across all services across a cluster without requiring code changes. Before
service meshes, that functionality had to be encoded into every single service,
becoming a potential source of bugs and technical debt.

The Sidecar Container model pairs each pod with a proxy. This per-pod proxy
intercepts and manages network traffic, enforces security policies, balances
workloads, and collects performance data for each service. While this approach
offers excellent control and service-specific traffic management, it also uses
more computing resources and becomes more complex to manage as your system grows.

A Sidecarless design, on the other hand, moves the aforementioned mesh
functionality to the operating system level by using kernel features like eBPF.
By doing away with per-pod proxies, this method drastically reduces resource
usage and removes unnecessary network hops, which lowers latency and boosts
performance. Because overhead remains constant regardless of pod count and there
are fewer agents to deploy, teams benefit from simplified operations and linear
scalability as workload increases.

---
DRAFTING NOTE (not from source): the final paragraph's "Sidecarless"/eBPF framing
is a THIRD model, distinct from Istio's sidecar-vs-ambient split. eBPF is barred
from graded text by the B7 Part 2 ruling (outline Open Question 11). §5 should
teach Istio's sidecar/ambient framing and may quote this entry's first three
paragraphs; do not import the eBPF sentence.

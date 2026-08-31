---
source_url: "https://istio.io/latest/docs/ambient/overview/"
fetched_at: "2026-08-31T09:44:00-0400"
authority: "Istio project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["ambient-mode", "sidecar-mode", "envoy", "mesh-data-plane"]
---
# Istio — Ambient mode overview (istio.io/latest/docs/ambient/overview/)

The source for trap #102 ("a service mesh means sidecars"). Direct quotations.

## What ambient mode is — verbatim

> "In ambient mode, Istio implements its features using a per-node Layer 4 (L4)
> proxy, and optionally a per-namespace Layer 7 (L7) proxy."

## The ztunnel node proxy — verbatim

> "The ztunnel (Zero Trust tunnel) component is a purpose-built, per-node proxy
> that powers Istio's ambient data plane mode."

## The L4 secure overlay — verbatim

> "The term 'secure overlay' is used to collectively describe the set of L4
> networking functions implemented in an ambient mesh via the ztunnel proxy."

## The waypoint proxy and the L7 layer — verbatim

> "The waypoint proxy is a deployment of the Envoy proxy; the same engine that
> Istio uses for its sidecar data plane mode."

> Waypoint proxies enable "advanced traffic management and L7 networking
> features" and "L7 authorization, telemetry and VirtualService routing."

## Comparison with sidecar mode — verbatim

> "Pods and workloads using sidecar mode can co-exist within the same mesh as
> pods that use ambient mode."

> In ambient mode, "workload pods no longer require proxies running in sidecars
> in order to participate in the mesh".

---
DRAFTING NOTE (not from source): "the same engine that Istio uses for its sidecar
data plane mode" is the sourced sentence behind the outline's claim that BOTH
modes use Envoy — and it is what makes the figure's requirement work, that
sidecar and ambient be drawn as "two arrangements of the same data plane, not two
products". The quoted L7 fragment mentions VirtualService; the §5 scope guardrail
bars teaching Istio CRDs, so do not carry that word into prose.

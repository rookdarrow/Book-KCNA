---
source_url: "https://istio.io/latest/about/service-mesh/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Istio project (CNCF graduated)"
objectives_covered: ["D4 Cloud Native Ecosystem and Principles", "D2 Networking", "D2 Security"]
concepts_covered: ["service-mesh", "mutual-tls", "zero-trust", "traffic-management", "sidecar", "ambient-mode", "envoy", "data-plane", "control-plane"]
---
# Istio — What is a service mesh? (istio.io/latest/about/service-mesh/)

A service mesh is an infrastructure layer that gives applications capabilities like zero-trust security, observability, and advanced traffic management, without code changes. Istio is the most popular, powerful, and trusted service mesh.

## Why would you want a service mesh?
- Security — Istio provides a market-leading zero-trust solution based on workload identity, mutual TLS, and strong policy controls.
- Observability — Istio generates telemetry within the service mesh, enabling observability on service behavior, and integrates with tools such as Grafana and Prometheus.
- Traffic management — Istio simplifies traffic routing and service-level configuration, allowing easy control over the flow of traffic between services, for use cases like A/B testing and canary deployments.

## Data plane and control plane
The mesh consists of a data plane (proxies that mediate and control all network communication between services) and a control plane (which manages and configures the proxies). Istio supports two data plane modes: sidecar mode, which deploys an Envoy proxy alongside each pod, and ambient mode, which uses per-node Layer 4 proxies and optional per-namespace Envoy proxies. Both modes use Envoy, the industry-standard proxy.

---
source_url: "https://kubernetes.io/docs/concepts/workloads/autoscaling/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["horizontal-scaling", "vertical-scaling", "hpa", "vpa", "keda", "cluster-autoscaling", "in-place-resize"]
---
# Autoscaling Workloads (kubernetes.io/docs/concepts/workloads/autoscaling/)

In Kubernetes, you can scale a workload depending on the current demand of resources. This allows your cluster to react to changes in resource demand more elastically and efficiently. When you scale a workload, you can either increase or decrease the number of replicas managed by the workload, or adjust the resources available to the replicas in-place.

## Scaling workloads manually
Horizontal scaling — use the kubectl CLI to change the replica count. Vertical scaling — patch the resource definition of the workload to adjust CPU/memory.

## Scaling workloads automatically
**Horizontal scaling** — the HorizontalPodAutoscaler (HPA) is implemented as a Kubernetes API resource and a controller; it periodically adjusts the number of replicas in a workload to match observed resource utilization such as CPU or memory usage.
**Vertical scaling** — the VerticalPodAutoscaler (VPA) is an add-on, not included by default, that automatically scales workload resources. As of Kubernetes v1.35, in-place pod vertical scaling is stable, but VPA does not yet support this directly.
**Autoscaling based on cluster size** — Cluster Proportional Autoscaler scales replica counts based on the number of schedulable nodes and cores (e.g., for cluster DNS); Cluster Proportional Vertical Autoscaler adjusts resource requests based on cluster size (beta).
**Event-driven autoscaling** — KEDA (Kubernetes Event Driven Autoscaler), a CNCF graduated project, scales workloads based on events such as the number of messages in a queue, with adapters for many event sources.
**Autoscaling based on schedules** — KEDA's Cron scaler defines schedules and time zones for scaling in or out.

## Scaling cluster infrastructure
Node autoscaling adds or removes nodes to scale the cluster infrastructure itself (Cluster Autoscaler, Karpenter).

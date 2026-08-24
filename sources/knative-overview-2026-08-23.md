---
source_url: "https://knative.dev/docs/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Knative project (CNCF graduated)"
objectives_covered: ["D4 Cloud Native Ecosystem and Principles", "D3 Application Delivery"]
concepts_covered: ["serverless", "knative-serving", "knative-eventing", "scale-to-zero", "cloudevents"]
---
# Knative — Overview (knative.dev/docs/)

Knative is a Kubernetes-based platform that provides a complete set of middleware components for building, deploying, and managing modern serverless workloads.

- **Knative Serving** — an HTTP-triggered autoscaling container runtime that manages the complete lifecycle of stateless HTTP services, including deployment, routing, and automatic scaling (including scale to zero).
- **Knative Eventing** — a CloudEvents-over-HTTP asynchronous routing layer that provides infrastructure for consuming and producing events, enabling loose coupling between event producers and consumers.
- **Knative Functions** — leverages Serving and Eventing to provide a simplified experience for building and deploying stateless functions.

Knative builds on the Kubernetes Pod abstraction, making it easy to access functionality like service accounts, accelerator access, and container sandboxing. Serving and Eventing are implemented as Kubernetes Custom Resource Definitions (CRDs). Knative is a CNCF graduated project.

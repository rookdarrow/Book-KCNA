---
source_url: "https://kubernetes.io/docs/concepts/overview/components/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1 Administration"]
concepts_covered: ["control-plane-components", "node-components", "addons"]
---
# Kubernetes Components (kubernetes.io/docs/concepts/overview/components/)

A Kubernetes cluster consists of a control plane and one or more worker nodes.

## Control plane components — manage the overall state of the cluster
- **kube-apiserver** — The core component server that exposes the Kubernetes HTTP API.
- **etcd** — Consistent and highly-available key value store for all API server data.
- **kube-scheduler** — Looks for Pods not yet bound to a node, and assigns each Pod to a suitable node.
- **kube-controller-manager** — Runs controllers to implement Kubernetes API behavior.
- **cloud-controller-manager** (optional) — Integrates with underlying cloud provider(s).

## Node components — run on every node, maintaining running pods and providing the Kubernetes runtime environment
- **kubelet** — Ensures that Pods are running, including their containers.
- **kube-proxy** (optional) — Maintains network rules on nodes to implement Services.
- **Container runtime** — Software responsible for running containers.

## Addons — extend the functionality of Kubernetes
- **DNS** — For cluster-wide DNS resolution.
- **Web UI (Dashboard)** — For cluster management via a web interface.
- **Container Resource Monitoring** — For collecting and storing container metrics.
- **Cluster-level Logging** — For saving container logs to a central log store.

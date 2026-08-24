---
source_url: "https://kubernetes.io/docs/setup/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Administration"]
concepts_covered: ["minikube", "kind", "kubeadm", "managed-kubernetes", "learning-environment", "production-environment"]
---
# Getting started — cluster setup options (kubernetes.io/docs/setup/)

## Learning environment
If you're learning Kubernetes, use the tools supported by the Kubernetes community, or tools in the ecosystem, to set up a Kubernetes cluster on a local machine: minikube (runs a single- or multi-node local Kubernetes cluster) and kind (Kubernetes IN Docker — runs local clusters using Docker containers as nodes).

## Production environment
When evaluating a solution for a production environment, consider which aspects of operating a Kubernetes cluster (or abstractions) you want to manage yourself and which you prefer to hand off to a provider. Options include managed / turnkey certified Kubernetes services from cloud providers, and self-managed clusters bootstrapped with kubeadm, the officially supported tool for creating clusters (used to install the control plane and join nodes). Other ecosystem tools include k3s (a lightweight distribution) and cluster lifecycle projects. A container runtime (containerd or CRI-O) must be installed on every node, and kubectl is the command-line tool for managing any cluster.

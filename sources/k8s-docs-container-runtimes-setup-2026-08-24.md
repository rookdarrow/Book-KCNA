---
source_url: "https://kubernetes.io/docs/setup/production-environment/container-runtimes/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.4"]
concepts_covered: ["container-runtime", "containerd", "cri-o", "cri"]
---
# Container Runtimes — kubernetes.io/docs/setup/production-environment/container-runtimes/

## Requirement

"You need to install a container runtime into each node in the cluster so that Pods
can run there."

Tooltip definition carried on that link: "The container runtime is the software that
is responsible for running containers."

"Kubernetes 1.36 requires that you use a runtime that conforms with the Container
Runtime Interface (CRI)."

## Runtimes documented on this page

containerd · CRI-O · Docker Engine · Mirantis Container Runtime

(Docker Engine appears here only via cri-dockerd; see
k8s-blog-dockershim-faq-2026-08-24.md for the history.)

## CRI socket paths

"On Linux the default CRI socket for containerd is `/run/containerd/containerd.sock`.
On Windows the default CRI endpoint is `npipe://./pipe/containerd-containerd`."

## Cgroup drivers — OUT OF SCOPE FOR CHAPTER 2, recorded for completeness

"Both the kubelet and the underlying container runtime need to interface with control
groups to enforce resource management for pods and containers and set resources such
as cpu/memory requests and limits. To interface with control groups, the kubelet and
the container runtime need to use a cgroup driver. It's critical that the kubelet and
the container runtime use the same cgroup driver and are configured the same."

DO NOT draft cgroup drivers into Chapter 2.

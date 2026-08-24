---
source_url: "https://kubernetes.io/docs/concepts/containers/runtime-class/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Containerization", "D2 Security"]
concepts_covered: ["runtimeclass", "sandboxed-runtime", "gvisor", "kata-containers", "pod-overhead"]
---
# Runtime Class (kubernetes.io/docs/concepts/containers/runtime-class/)

RuntimeClass is a feature for selecting the container runtime configuration. The container runtime configuration is used to run a Pod's containers.

## Motivation
You can set a different RuntimeClass between different Pods to provide a balance of performance versus security. For example, if part of your workload deserves a high level of information security assurance, you might choose to schedule those Pods so that they run in a container runtime that uses hardware virtualization (such as Kata Containers) or a user-space kernel (such as gVisor). You'd then benefit from the extra isolation of the alternative runtime, at the expense of some additional overhead. You can also use RuntimeClass to run different Pods with the same container runtime but with different settings.

## Setup and usage
Configure the CRI implementation on nodes (each configuration has a corresponding handler name), then create the corresponding RuntimeClass resources (apiVersion node.k8s.io/v1, kind RuntimeClass, with a handler field). Once RuntimeClasses are configured for the cluster, you can specify a runtimeClassName in the Pod spec to use it; if no runtimeClassName is specified, the default RuntimeHandler is used. RuntimeClass can carry scheduling constraints (nodeSelector, tolerations) so Pods land on nodes that support the handler, and a Pod overhead so the scheduler accounts for the runtime's resource cost.

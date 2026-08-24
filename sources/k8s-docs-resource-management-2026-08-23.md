---
source_url: "https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Scheduling", "D1 Core Concepts"]
concepts_covered: ["requests", "limits", "cpu-throttling", "oom-kill", "millicpu", "memory-units", "resource-types"]
---
# Resource Management for Pods and Containers (kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

When you specify a Pod, you can optionally specify how much of each resource a container needs. The most common resources to specify are CPU and memory (RAM). When you specify the resource request for containers in a Pod, the kube-scheduler uses this information to decide which node to place the Pod on. When you specify a resource limit for a container, the kubelet enforces those limits so that the running container is not allowed to use more of that resource than the limit you set. The kubelet also reserves at least the request amount of that system resource specifically for that container to use. If the node where a Pod is running has enough of a resource available, it's possible (and allowed) for a container to use more resource than its request for that resource specifies. However, a container is not allowed to use more than its resource limit.

cpu limits are enforced by CPU throttling. When a container approaches its cpu limit, the kernel will restrict access to the CPU corresponding to the container's limit. Thus, a cpu limit is a hard limit the kernel enforces. memory limits are enforced by the kernel with out of memory (OOM) kills. When a container uses more than its memory limit, the kernel may terminate it. However, terminations only happen when the kernel detects memory pressure. Thus, a container that over allocates memory may not be immediately killed; memory limits are enforced reactively.

## Resource types
cpu — compute processing, base unit: cpu (core); memory — RAM, base unit: bytes; ephemeral-storage — local ephemeral storage, bytes; hugepages-<size> — huge pages (Linux only), bytes. Clusters can also provide extended resources (custom-named resources, typically exposed by device plugins).

## Resource units
CPU: limits and requests for CPU resources are measured in cpu units. In Kubernetes, 1 CPU unit is equivalent to 1 physical CPU core, or 1 virtual core, depending on whether the node is a physical host or a virtual machine running inside a physical machine. Fractional requests are allowed: 0.5 requests half as much CPU time as 1.0; the quantity expression 0.1 is equivalent to 100m ("one hundred millicpu"). CPU resource is always specified as an absolute amount of resource, never as a relative amount — 500m CPU represents roughly the same amount of computing power whether that container runs on a single-core, dual-core, or 48-core machine. Kubernetes doesn't allow you to specify CPU resources with a precision finer than 1m.

Memory: limits and requests for memory are measured in bytes. You can express memory as a plain integer or as a fixed-point number using one of these quantity suffixes: E, P, T, G, M, k, or the power-of-two equivalents Ei, Pi, Ti, Gi, Mi, Ki. Pay attention to the case of the suffixes: "M" means megabytes while "m" means millibytes — a request of 400m of memory is a request for 0.4 bytes.

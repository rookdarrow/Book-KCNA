---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/scheduling-eviction/pod-overhead.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), concept page for Pod Overhead, CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["pod-overhead", "runtimeclass", "overhead-added-to-requests", "requests-as-scheduling-input", "resource-quota-counts-overhead"]
closes_gap: "ch-07 gap G-7F (§2 'One clause about overhead'): the mechanism by which a RuntimeClass overhead enters the scheduler's arithmetic. Supplements k8s-docs-runtime-class-2026-08-23.md, which states only that the overhead exists."
---

# Pod Overhead (kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/)

Feature state on the page: `stable` since Kubernetes v1.24.

All passages below are **[VERBATIM]** from the raw page markdown, with Hugo shortcodes and
in-page links removed.

## Overview

> When you run a Pod on a Node, the Pod itself takes an amount of system resources. These
> resources are additional to the resources needed to run the container(s) inside the Pod.
> In Kubernetes, _Pod Overhead_ is a way to account for the resources consumed by the Pod
> infrastructure on top of the container requests & limits.

> In Kubernetes, the Pod's overhead is set at admission time according to the overhead
> associated with the Pod's RuntimeClass.

> A pod's overhead is considered in addition to the sum of container resource requests when
> scheduling a Pod. Similarly, the kubelet will include the Pod overhead when sizing the Pod
> cgroup, and when carrying out Pod eviction ranking.

## Configuring Pod overhead

> You need to make sure a `RuntimeClass` is utilized which defines the `overhead` field.

> Workloads which are created which specify the `kata-fc` RuntimeClass handler will take the
> memory and cpu overheads into account for resource quota calculations, node scheduling, as
> well as Pod cgroup sizing.

## How the scheduler uses it

> If a ResourceQuota is defined, the sum of container requests as well as the `overhead`
> field are counted.

> When the kube-scheduler is deciding which node should run a new Pod, the scheduler
> considers that Pod's `overhead` as well as the sum of container requests for that Pod.
> For this example, the scheduler adds the requests and the overhead, then looks for a node
> that has 2.25 CPU and 320 MiB of memory available.

> Once a Pod is scheduled to a node, the kubelet on that node creates a new cgroup for the
> Pod. It is within this pod that the underlying container runtime will create containers.

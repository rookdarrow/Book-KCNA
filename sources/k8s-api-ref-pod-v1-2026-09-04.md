---
source_url: "https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), generated API reference for the core/v1 Pod resource, CC BY 4.0"
objectives_covered: ["D1.1"]
concepts_covered: ["pod", "podspec", "spec", "status", "podstatus"]
closes_gap: "Ch 5 §1 AUTHOR-REVIEW: the identity 'PodSpec = the spec field of a Pod' was entailed by two snapshots but stated verbatim in none. This reference states it directly."
---

# Pod (core/v1) — API reference

> All passages below are **[VERBATIM]** from the rendered API reference page.

## Pod

> "Pod is a collection of containers that can run on a host. This resource is created by clients and scheduled onto hosts."

Fields of Pod:

> "`spec` _PodSpec_ — Specification of the desired behavior of the pod. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status"

> "`status` _PodStatus_ — Most recently observed status of the pod. This data may not be up to date. Populated by the system. Read-only. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status"

## PodSpec

> "PodSpec is a description of a pod."

## Notes for the author

- The chapter relies on exactly one identity from this page: a Pod's `spec` field is of type `PodSpec`, so "PodSpec" and "the `spec` of a Pod" name the same thing.
- The `restartPolicy` field descriptions (PodSpec-level and the container-level sidecar field) were not captured in this fetch; the sidecar behavior is covered by `k8s-docs-sidecar-containers-2026-08-24.md`.

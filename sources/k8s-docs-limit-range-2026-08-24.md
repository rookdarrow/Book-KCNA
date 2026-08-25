---
source_url: "https://kubernetes.io/docs/concepts/policy/limit-range/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/policy/limit-range.md"
fetched_at: "2026-08-24T18:57:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["limit-range", "resource-quota", "admission-control", "default-requests", "namespaced-vs-cluster-scoped"]
closes_gap: "ch-08 outline Open Question #3 (BLOCKING), second half. Previously nothing cached described LimitRange's min/max/default structure or its per-object scope."
---
# Limit Ranges

> **Extraction note.** All passages below are **[VERBATIM]**.

## What it is

> "A LimitRange is a policy to constrain the resource allocations (limits and requests) that you can specify for each applicable object kind (such as Pod or PersistentVolumeClaim) in a namespace."

## What a LimitRange provides

> "Enforce minimum and maximum compute resources usage per Pod or Container in a namespace."

> "Enforce minimum and maximum storage request per PersistentVolumeClaim in a namespace."

> "Enforce a ratio between request and limit for a resource in a namespace."

> "Set default request/limit for compute resources in a namespace and automatically inject them to Containers at runtime."

## When it applies

> "Kubernetes constrains resource allocations to Pods in a particular namespace whenever there is at least one LimitRange object in that namespace."

> "LimitRange validations occur only at Pod admission stage, not on running Pods. If you add or modify a LimitRange, the Pods that already exist in that namespace continue unchanged."

> "A LimitRange does not check the consistency of the default values it applies."

## Constraints on resource limits and requests

> "The administrator creates a LimitRange in a namespace."

> "Users create (or try to create) objects in that namespace, such as Pods or PersistentVolumeClaims."

> "First, the LimitRange admission controller applies default request and limit values for all Pods (and their containers) that do not set compute resource requirements."

> "Second, the LimitRange tracks usage to ensure it does not exceed resource minimum, maximum and ratio defined in any LimitRange present in the namespace."

> "If you attempt to create or update an object (Pod or PersistentVolumeClaim) that violates a LimitRange constraint, your request to the API server will fail with an HTTP status code `403 Forbidden` and a message explaining the constraint that has been violated."

> "If you add a LimitRange in a namespace that applies to compute-related resources such as `cpu` and `memory`, you must specify requests or limits for those values. Otherwise, the system may reject Pod creation."

> "If two or more LimitRange objects exist in the namespace, it is not deterministic which default value will be applied."

---

## What this snapshot licenses Chapter 8 sec.3 to assert

- The **contrast** is now fully sourced on both sides. ResourceQuota "limit[s] aggregate
  resource consumption per namespace"; a LimitRange constrains "each applicable object kind
  ... in a namespace."
- The **mutate-vs-reject echo of sec.2** is sourced: a LimitRange "automatically inject[s]"
  defaults into Containers, and a quota violation is "reject[ed] ... with HTTP status code
  `403 Forbidden`." That is `ch08-fig05`'s design requirement, in the sources' own words.
- The sec.3 Snag ("the Pod you get is not the Pod you wrote") rests on "automatically
  inject them to Containers at runtime" plus "does not check the consistency of the default
  values it applies."

NOT IN THIS SNAPSHOT: the YAML examples, the per-container vs per-Pod limit type
distinction in detail, and PersistentVolumeClaim storage limit examples.

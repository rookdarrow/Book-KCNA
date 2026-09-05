---
source_url: "https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/configure-pod-container/configure-pod-configmap.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["createcontainerconfigerror", "configmap-must-exist", "optional-configmap", "missing-configmap-key"]
closes_gap: "ch-13 sec.2 RESEARCH GAP: no cached snapshot stated that a Pod referencing a ConfigMap that does not exist, or a key that does not exist inside one, fails to start. The task page's Restrictions list states both outright, and the Optional ConfigMaps section states the contrasting behavior when the reference is marked optional."
---

# Configure a Pod to Use a ConfigMap — Restrictions and Optional ConfigMaps

> All passages below are **[VERBATIM]**.

## Under `## Restrictions`

"You must create the `ConfigMap` object before you reference it in a Pod specification. Alternatively, mark the ConfigMap reference as `optional` in the Pod spec (see Optional ConfigMaps). If you reference a ConfigMap that doesn't exist and you don't mark the reference as `optional`, the Pod won't start. Similarly, references to keys that don't exist in the ConfigMap will also prevent the Pod from starting, unless you mark the key references as `optional`."

"If you use `envFrom` to define environment variables from ConfigMaps, keys that are considered invalid will be skipped. The pod will be allowed to start, but the invalid names will be recorded in the event log (`InvalidVariableNames`)."

## Under `## Optional ConfigMaps`

"You can mark a reference to a ConfigMap as _optional_ in a Pod specification. If the ConfigMap doesn't exist, the configuration for which it provides data in the Pod (for example: environment variable, mounted volume) will be empty. If the ConfigMap exists, but the referenced key is non-existent the data is also empty."

## What this supports

- A missing ConfigMap and a missing *key inside an existing* ConfigMap both prevent the Pod from starting — the same failure shape from two causes.
- The reference is checked when the Pod is run, not when the manifest is accepted: the page's instruction is to "create the `ConfigMap` object before you reference it," which presumes the Pod spec is accepted either way.
- The literal reason string is not on this page; see k8s-kubelet-kuberuntime-container-reasons-2026-09-04.

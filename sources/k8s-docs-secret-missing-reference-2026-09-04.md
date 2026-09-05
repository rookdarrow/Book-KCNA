---
source_url: "https://kubernetes.io/docs/concepts/configuration/secret/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/configuration/secret.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["createcontainerconfigerror", "secret-must-exist", "optional-secret", "kubelet-retries-missing-secret"]
closes_gap: "ch-13 sec.2 RESEARCH GAP (highest severity): no cached snapshot stated what happens when a Pod references a Secret that does not exist. This page states that the kubelet discovers the missing Secret when it tries to run the Pod (not at admission), retries periodically, reports an Event with details, and that no container starts until every non-optional Secret is available."
---

# Secrets — what happens when a referenced Secret does not exist

> All passages below are **[VERBATIM]** from the page's "Using a Secret" section and its "Optional Secrets" subsection.

## Under `## Using a Secret` — the kubelet discovers the absence, and retries

"If the Secret cannot be fetched (perhaps because it does not exist, or due to a temporary lack of connection to the API server) the kubelet periodically retries running that Pod. The kubelet also reports an Event for that Pod, including details of the problem fetching the Secret."

The two sentences immediately before it, for context (also verbatim):

"reference actually points to an object of type Secret. Therefore, a Secret needs to be created before any Pods that depend on it."

## Under `#### Optional Secrets {#restriction-secret-must-exist}`

"When you reference a Secret in a Pod, you can mark the Secret as _optional_, such as in the following example. If an optional Secret doesn't exist, Kubernetes ignores it."

"By default, Secrets are required. None of a Pod's containers will start until all non-optional Secrets are available."

## What this does and does not support

- SUPPORTS: a Pod that references a non-optional Secret which does not exist is accepted by the API (the page speaks of "any Pods that depend on it" existing) and its containers do not start; the **kubelet** is the component that finds the Secret missing, retries, and writes an Event carrying the detail.
- SUPPORTS: the failure is discovered at container-configuration time on the node, not at the admission gate.
- DOES NOT STATE: the literal container-state reason string `CreateContainerConfigError`. That string is sourced separately from the kubelet source (see k8s-kubelet-kuberuntime-container-reasons-2026-09-04).

---
source_url: "https://kubernetes.io/docs/concepts/configuration/secret/#restriction-secret-must-exist"
fetched_at: "2026-09-04T09:25:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors. Text taken from the page's source in the kubernetes/website repository (content/en/docs/concepts/configuration/secret.md, main branch) because the rendered page exceeded the fetch tool's length limit."
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["secret-must-exist", "pod-never-starts", "secret-type"]
---
# Secrets — "Optional Secrets" (kubernetes.io/docs/concepts/configuration/secret/)

Completes `k8s-docs-secret-2026-08-23.md`, which is truncated before the "Using a Secret" material. This snapshot carries the two sentences that state what happens when a Pod references a Secret that is not there. Ch 12 §4 hands the fact forward to Ch 13 §2.

## Optional Secrets

"By default, Secrets are required. None of a Pod's containers will start until all non-optional Secrets are available."

"If a Pod references a specific key in a non-optional Secret and that Secret does exist, but is missing the named key, the Pod fails during startup."

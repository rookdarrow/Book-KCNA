---
source_url: "https://kubernetes.io/docs/concepts/security/pod-security-admission/"
fetched_at: "2026-08-31T10:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["pod-security-admission", "psa-enforce", "psa-audit", "psa-warn", "namespace-label-control-surface", "pod-security-standards", "podsecuritypolicy-removed"]
---
# Pod Security Admission (kubernetes.io/docs/concepts/security/pod-security-admission/)

All passages below are the page's own sentences, quoted exactly.

## Feature state and what it is

"Feature state: Stable since Kubernetes v1.25"

"Kubernetes offers a built-in _Pod Security_ admission controller to enforce the Pod Security Standards."

## Pod Security levels

"Pod Security admission places requirements on a Pod's Security Context and other related fields according to the three levels defined by the Pod Security Standards: `privileged`, `baseline`, and `restricted`. Refer to the Pod Security Standards page for an in-depth look at those requirements."

> NOTE FOR DRAFTING: this page does **not** restate the one-line description of each level. Those live on the Pod Security Standards page — see `k8s-docs-pod-security-standards-2026-08-23.md` and `k8s-docs-pod-security-standards-profiles-2026-08-31.md`.

## Pod Security Admission labels for namespaces

The label form:

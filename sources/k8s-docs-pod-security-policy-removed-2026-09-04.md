---
source_url: "https://kubernetes.io/docs/concepts/security/pod-security-policy/"
fetched_at: "2026-09-04T09:25:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors. Text taken from the page's source in the kubernetes/website repository (content/en/docs/concepts/security/pod-security-policy.md, main branch); the rendered page timed out on fetch."
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["podsecuritypolicy-removed", "pod-security-admission"]
---
# PodSecurityPolicy — the removed-feature notice (kubernetes.io/docs/concepts/security/pod-security-policy/)

The one fact Ch 12 §6 needs about PodSecurityPolicy: when it left. The page opens with a "Removed feature" alert and then points readers to Pod Security Admission as the replacement.

## Removed feature

"PodSecurityPolicy was deprecated in Kubernetes v1.21, and removed from Kubernetes in v1.25."

The alert goes on to name the replacements for enforcing similar restrictions on Pods, the first of which is Pod Security Admission (linked to /docs/concepts/security/pod-security-admission/).

---
source_url: "https://kubernetes.io/docs/concepts/security/pod-security-admission/"
fetched_at: "2026-09-04T09:10:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["pod-security-admission", "psa-enforce", "psa-audit", "psa-warn", "namespace-label-control-surface"]
---
# Pod Security Admission — the namespace-label section (kubernetes.io/docs/concepts/security/pod-security-admission/)

Completes `k8s-docs-pod-security-admission-2026-08-31.md`, which is truncated at the heading "Pod Security Admission labels for namespaces / The label form:". This snapshot carries that section. It does **not** mention PodSecurityPolicy or the version in which it was removed; that statement lives on the PodSecurityPolicy page, not here.

## Feature state

"Feature state: Stable since Kubernetes v1.25"

"Kubernetes offers a built-in Pod Security admission controller to enforce the Pod Security Standards."

## Pod Security Admission labels for namespaces

"Once the feature is enabled or the webhook is installed, you can configure namespaces to define the admission control mode you want to use for pod security in each namespace. Kubernetes defines a set of labels that you can set to define which of the predefined Pod Security Standard levels you want to use for a namespace. The label you select defines what action the control plane takes if a potential violation is detected:"

- **enforce** — "Policy violations will cause the pod to be rejected."
- **audit** — "Policy violations will trigger the addition of an audit annotation to the event recorded in the audit log, but are otherwise allowed."
- **warn** — "Policy violations will trigger a user-facing warning, but are otherwise allowed."

"A namespace can configure any or all modes, or even set a different level for different modes."

"The per-mode level label indicates which policy level to apply for the mode."

Label form (as documented on the page): `pod-security.kubernetes.io/<MODE>: <LEVEL>`, where MODE is one of `enforce`, `audit`, `warn` and LEVEL is one of `privileged`, `baseline`, `restricted`.

---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/diffing/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Argo project (Argo CD; CNCF graduated) — user guide, Diffing Customization; text taken from the project's docs source (argoproj/argo-cd, docs/user-guide/diffing.md)"
objectives_covered: ["D3.1"]
concepts_covered: ["synced-outofsync", "drift-detection", "sync-operation"]
---
# Argo CD — Diffing Customization (opening section)

CAPTURE NOTE: supersedes argocd-diffing-outofsync-2026-08-31, which carried the first sentence only and disclaimed the list of causes. The list below is verbatim.

"It is possible for an application to be `OutOfSync` even immediately after a successful Sync operation. Some reasons for this might be:"

- "There is a bug in the manifest, where it contains extra/unknown fields from the actual K8s spec. These extra fields would get dropped when querying Kubernetes for the live state, resulting in an `OutOfSync` status indicating a missing field was detected."
- "The sync was performed (with pruning disabled), and there are resources which need to be deleted."
- "A controller or mutating webhook is altering the object after it was submitted to Kubernetes so it differs from the one in Git."
- "A Helm chart is using a template function such as `randAlphaNum`, which generates different data every time `helm template` is invoked."
- "For Horizontal Pod Autoscaling (HPA) objects, the HPA controller is known to reorder `spec.metrics` in a specific order. See kubernetes issue #74099. To work around this, you can order `spec.metrics` in Git in the same order that the controller prefers."

"In case it is impossible to fix the upstream issue, Argo CD allows you to optionally ignore differences of problematic resources. The diffing customization can be configured for single or multiple application resources or at a system level."

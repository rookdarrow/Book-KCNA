---
source_url: "https://kubernetes.io/docs/concepts/security/pod-security-standards/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched as the raw CC BY 4.0 markdown source from kubernetes/website, main branch (content/en/docs/concepts/security/pod-security-standards.md)"
objectives_covered: ["D2.2", "D3.2"]
concepts_covered: ["pod-security-standards", "pss-restricted-fields", "ephemeral-containers-under-pod-security-standards", "run-as-non-root", "privileged-container"]
---

# Pod Security Standards — the controls apply to ephemeral containers

> Companion to `k8s-docs-pod-security-standards-2026-08-23.md` (summary table) and `k8s-docs-pod-security-standards-profiles-2026-08-31.md` (condensed control tables). This snapshot exists to carry, verbatim, the field lists showing that every per-container control names `spec.ephemeralContainers[*]` alongside `spec.containers[*]` and `spec.initContainers[*]`. The page renders its control tables as HTML; the row text and `<code>` field paths below are reproduced exactly.

"These policies are _cumulative_ and range from highly-permissive to highly-restrictive."

## Baseline — Privileged Containers

Control: "Privileged Containers"

"Privileged Pods disable most security mechanisms and must be disallowed."

"Restricted Fields"

- `spec.containers[*].securityContext.privileged`
- `spec.initContainers[*].securityContext.privileged`
- `spec.ephemeralContainers[*].securityContext.privileged`

## Restricted — Running as Non-root

Control: "Running as Non-root"

"Containers must be required to run as non-root users."

"Restricted Fields"

- `spec.securityContext.runAsNonRoot`
- `spec.containers[*].securityContext.runAsNonRoot`
- `spec.initContainers[*].securityContext.runAsNonRoot`
- `spec.ephemeralContainers[*].securityContext.runAsNonRoot`

## Other controls whose field lists include `spec.ephemeralContainers[*]` (paths verbatim)

- `spec.ephemeralContainers[*].securityContext.windowsOptions.hostProcess`
- `spec.ephemeralContainers[*].securityContext.capabilities.add`
- `spec.ephemeralContainers[*].ports[*].hostPort`
- `spec.ephemeralContainers[*].securityContext.appArmorProfile.type`
- `spec.ephemeralContainers[*].securityContext.seLinuxOptions.type`
- `spec.ephemeralContainers[*].securityContext.procMount`
- `spec.ephemeralContainers[*].securityContext.seccompProfile.type`
- `spec.ephemeralContainers[*].securityContext.allowPrivilegeEscalation`
- `spec.ephemeralContainers[*].securityContext.runAsUser`
- `spec.ephemeralContainers[*].securityContext.capabilities.drop`

---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched as the raw CC BY 4.0 markdown source from kubernetes/website, main branch (content/en/docs/tasks/debug/debug-application/get-shell-running-container.md)"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["kubectl-exec", "double-dash-argument-boundary"]
---

# Get a Shell to a Running Container

> Supersedes `k8s-docs-get-shell-running-container-2026-08-31.md` for the double-dash note, which sat after the page's first code fence and was lost to truncation. Verbatim.

"This page shows how to use `kubectl exec` to get a shell to a running container."

Note: "The double dash (`--`) separates the arguments you want to pass to the command from the kubectl arguments."

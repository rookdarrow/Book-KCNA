---
source_url: "https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched as the raw CC BY 4.0 markdown source from kubernetes/website, main branch (content/en/docs/tasks/access-application-cluster/port-forward-access-application-cluster.md)"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["kubectl-port-forward", "port-forward-tcp-only"]
---

# Use Port Forwarding to Access Applications in a Cluster

> Supersedes `k8s-docs-port-forward-2026-08-31.md` for the TCP-only note, which sat after the page's first code fence and was lost to truncation. Verbatim.

"`kubectl port-forward` allows using resource name, such as a pod name, to select a matching pod to port forward to."

Note: "`kubectl port-forward` is implemented for TCP ports only. The support for UDP protocol is tracked in issue 47862."

---
source_url: "https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/command-line-tools-reference/kube-apiserver.md"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 -- fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["event-retention-window", "node-death-handling", "kubernetes-events"]
closes_gap: "ch-13 outline Open Question 4, items 1 and 3 -- the event retention default and the node-death eviction timeout, both of which the outline barred from being written from memory. BOTH ARE NOW PINNED."
---
# kube-apiserver flags — event retention and default NoExecute tolerations

> All rows below are **[VERBATIM]** from the options table.

## `--event-ttl`

---
source_url: "https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/command-line-tools-reference/kube-apiserver.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — the generated kube-apiserver flag reference, fetched from the kubernetes/website source markdown"
objectives_covered: ["D2.3"]
concepts_covered: ["event-retention-window", "event-ttl-default", "node-death-handling", "default-noexecute-tolerations"]
closes_gap: "The 2026-08-31 snapshot k8s-apiserver-event-ttl-and-toleration-defaults is transcribed only as far as the `--event-ttl` heading and holds no default value, despite its frontmatter saying the default is pinned. This snapshot carries the three flag rows with their defaults. Use the event-ttl default as a dated illustration of scale, not as an examinable fact — it is an operator-settable flag."
---

# kube-apiserver flags — event retention and default NoExecute tolerations

> All rows below are **[VERBATIM]** from the options table (HTML tags removed; the table prints the flag, its type and its default on one row and the description on the next).

## `--event-ttl`

"--event-ttl duration     Default: 1h0m0s"

"Amount of time to retain events."

## `--default-not-ready-toleration-seconds`

"--default-not-ready-toleration-seconds int     Default: 300"

"Indicates the tolerationSeconds of the toleration for notReady:NoExecute that is added by default to every pod that does not already have such a toleration."

## `--default-unreachable-toleration-seconds`

"--default-unreachable-toleration-seconds int     Default: 300"

"Indicates the tolerationSeconds of the toleration for unreachable:NoExecute that is added by default to every pod that does not already have such a toleration."

## What this supports

- Events are retained for a bounded window set by the API server; the shipped default is one hour. A failure investigated the next working day will have no events left unless the flag was raised.
- The 300-second default toleration that k8s-docs-taints-tolerations-depth-2026-08-24 describes is an API server default, set by these two flags, which is why Chapter 13 §5's "five minutes" appears twice (node controller wait, and Pod toleration) and is the same order of magnitude in both places.

---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/"
fetched_at: "2026-08-31T13:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["cluster-log-architecture", "kubelet-health", "node-conditions-as-diagnostic", "node-death-handling", "platform-scope-vs-application-scope"]
partial_note: "The 'Cluster failure modes' / 'Mitigations' sections were truncated by the fetcher and are NOT reproduced here. Do not cite this snapshot for failure-mode taxonomy."
---
# Troubleshooting Clusters

> All passages below are **[VERBATIM]**.

> "This doc is about cluster troubleshooting; we assume you have already ruled out your application as the root cause of the problem you are experiencing. See the application troubleshooting guide for tips on application debugging."

> "For troubleshooting kubectl, refer to Troubleshooting kubectl."

## Listing your cluster

> "The first thing to debug in your cluster is if your nodes are all registered correctly."

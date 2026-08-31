---
source_url: "https://kubernetes.io/docs/concepts/cluster-administration/logging/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["cluster-log-architecture", "kubectl-logs", "kubectl-logs-previous", "node-level-logging-agent"]
supersedes_note: "Fuller than k8s-docs-logging-architecture-2026-08-23.md (2.9KB). Carries the log-rotation defaults and the 'only the latest log file' note, both new."
ledger_guardrail: "Node-level logging agent is OWNED by Ch 18 sec.6. sec.7 gets one clause plus a pointer. The agent material below is included for accuracy of that one clause only -- do not expand it."
---
# Logging Architecture

> All passages below are **[VERBATIM]**.

> "For example, you may want to access your application's logs if a container crashes, a pod gets evicted, or a node dies."

> "In a cluster, logs should have a separate storage and lifecycle independent of nodes, pods, or containers. This concept is called cluster-level logging."

> **"Cluster-level logging architectures require a separate backend to store, analyze, and query logs. Kubernetes does not provide a native storage solution for log data. Instead, there are many logging solutions that integrate with Kubernetes."**

## Pod and container logs

> "Kubernetes captures logs from each container in a running Pod."

> "To fetch the logs, use the `kubectl logs` command, as follows:"

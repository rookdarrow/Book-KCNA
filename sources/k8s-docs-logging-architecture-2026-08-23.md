---
source_url: "https://kubernetes.io/docs/concepts/cluster-administration/logging/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D4 Observability", "D2 Troubleshooting"]
concepts_covered: ["logging", "stdout-stderr", "kubectl-logs", "log-rotation", "cluster-level-logging", "node-logging-agent", "sidecar-logging"]
---
# Logging Architecture (kubernetes.io/docs/concepts/cluster-administration/logging/)

Application logs can help you understand what is happening inside your application. The logs are particularly useful for debugging problems and monitoring cluster activity. Most modern applications have some kind of logging mechanism. Likewise, container engines are designed to support logging. The easiest and most adopted logging method for containerized applications is writing to standard output and standard error streams. However, the native functionality provided by a container engine or runtime is usually not enough for a complete logging solution. In a cluster, logs should have a separate storage and lifecycle independent of nodes, pods, or containers. This concept is called cluster-level logging. Cluster-level logging architectures require a separate backend to store, analyze, and query logs. Kubernetes does not provide a native storage solution for log data. Instead, there are many logging solutions that integrate with Kubernetes.

## Pod and container logs
Kubernetes captures logs from each container in a running Pod. `kubectl logs <pod>` prints them; for a multi-container Pod use `-c <container>`; `kubectl logs --previous` retrieves logs from a previous instantiation of a container. The container runtime handles and redirects any output generated to a containerized application's stdout and stderr streams; the kubelet manages the logs using the CRI logging format. By default, if a container restarts, the kubelet keeps one terminated container with its logs. If a pod is evicted from the node, all corresponding containers are also evicted, along with their logs. The kubelet is responsible for rotating container logs and managing the logging directory structure, configured via containerLogMaxSize (default 10Mi) and containerLogMaxFiles (default 5). When you run kubectl logs, the kubelet on that node handles the request and reads directly from the log file; the kubelet returns the content of the log file; only the latest log file's contents are available.

## Cluster-level logging architectures
- Use a node-level logging agent that runs on every node (typically a DaemonSet) and pushes logs to a backend.
- Include a dedicated sidecar container for logging in an application pod — either a streaming sidecar that writes logs to its own stdout/stderr, or a sidecar container with a logging agent configured to pick up logs from an application container.
- Push logs directly to a backend from within an application.

---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D2 Troubleshooting"]
concepts_covered: ["pod-phase", "container-states", "restart-policy", "probes", "liveness", "readiness", "startup-probe", "backoff"]
---
# Pod Lifecycle (kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

## Pod lifetime
Pods are scheduled once in their lifetime to a specific node; the kubelet runs a reconciliation loop that keeps the containers described in the Pod spec running. Pods are considered to be relatively ephemeral (rather than durable) entities. Pods are created, assigned a unique ID (UID), and scheduled to run on nodes where they remain until termination (according to restart policy) or deletion. A Pod is never "rescheduled" to a different node; instead, it is replaced by a new, near-identical Pod with a different UID. If a node dies, the Pods running on it are marked for deletion after a timeout. Pods do not survive evictions due to lack of resources or node maintenance. Higher-level controllers such as Deployments create replacement Pods.

## Pod phase
- Pending — The Pod has been accepted by the Kubernetes cluster, but one or more of the containers has not been set up and made ready to run. This includes time a Pod spends waiting to be scheduled as well as the time spent downloading container images over the network.
- Running — The Pod has been bound to a node, and all of the containers have been created. At least one container is still running, or is in the process of starting or restarting.
- Succeeded — All containers in the Pod have terminated in success, and will not be restarted.
- Failed — All containers in the Pod have terminated, and at least one container has terminated in failure. That is, the container either exited with non-zero status or was terminated by the system, and is not set for automatic restarting.
- Unknown — For some reason the state of the Pod could not be obtained. This phase typically occurs due to an error in communicating with the node where the Pod should be running.

## Container states
Waiting — the container is still running the operations it requires in order to complete start up (pulling the container image, applying Secret data); a Reason field summarizes why. Running — the container is executing without issues; a startedAt timestamp is recorded. Terminated — the container began execution and then either ran to completion or failed; reason, exit code, and start/finish times are recorded.

## Container restart policy
The spec of a Pod has a restartPolicy field with possible values Always (default), OnFailure, and Never. The restartPolicy applies to all containers in the Pod. After containers in a Pod exit, the kubelet restarts them with an exponential backoff delay (10s, 20s, 40s, …), that is capped at five minutes. Once a container has executed for 10 minutes without any problems, the kubelet resets the restart backoff timer for that container.

## Container probes
A probe is a diagnostic performed periodically by the kubelet on a container. Check mechanisms: exec (executes a command; success if exit status 0); grpc (gRPC health check); httpGet (HTTP GET against the pod's IP, port and path; success if status ≥200 and <400); tcpSocket (TCP check; success if the port is open). Probe types: livenessProbe — indicates whether the container is running; if it fails, the kubelet kills the container and the container is subjected to its restart policy. readinessProbe — indicates whether the container is ready to respond to requests; if it fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod. startupProbe — indicates whether the application within the container is started; all other probes are disabled if a startup probe is provided, until it succeeds; if it fails, the kubelet kills the container and applies the restart policy. Parameters: initialDelaySeconds, periodSeconds, timeoutSeconds, successThreshold, failureThreshold.

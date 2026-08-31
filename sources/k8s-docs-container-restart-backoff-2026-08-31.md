---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-restarts"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/workloads/pods/pod-lifecycle.md"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 -- fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["crashloopbackoff", "restart-backoff-curve"]
closes_gap: "ch-13 outline Open Question 4, item 2 -- the CrashLoopBackOff backoff schedule and its reset behaviour, which the outline barred from being written from memory."
conflict_note: "The rendered-page fetch returned '5 minutes' for the backoff RESET window. The source markdown says 10 minutes, and the cached k8s-docs-pod-lifecycle-2026-08-23.md also says 10 minutes. TWO sources agree on 10 minutes; the rendered-page fetch is rejected as a transcription error. Use 10 minutes."
---
# Container restart policy, the backoff curve, and CrashLoopBackOff

> All passages below are **[VERBATIM]** from the kubernetes/website source markdown.

## How Pods handle problems with containers

> "Kubernetes manages container failures within Pods using a `restartPolicy` defined in the Pod `spec`. This policy determines how Kubernetes reacts to containers exiting due to errors or other reasons, which follows this sequence:
> 1. **Initial crash**: Kubernetes attempts an immediate restart based on the Pod `restartPolicy`.
> 2. **Repeated crashes**: After the initial crash Kubernetes applies an exponential backoff delay for subsequent restarts. This prevents rapid, repeated restart attempts from overloading the system.
> 3. **CrashLoopBackOff state**: This indicates that the backoff delay mechanism is currently in effect for a container in a crash loop.
> 4. **Backoff reset**: If a container runs successfully for a certain duration, Kubernetes resets the backoff delay."

> "When a container enters the crash loop, Kubernetes applies exponential backoff delay. This mechanism prevents a faulty container from overwhelming the system with continuous failed start attempts."

> "The `CrashLoopBackOff` can be caused by application errors, configuration errors, resource constraints, failing health checks, or probe failures."

## Container restarts

> "The `spec` of a Pod has a `restartPolicy` field with possible values `Always`, `OnFailure`, and `Never`. The default value is `Always`."

| Exit Code | `restartPolicy: Always` | `restartPolicy: OnFailure` | `restartPolicy: Never` | Sidecar Containers |
|---|---|---|---|---|
| 0 (Success) | Restarts | Does not restart | Does not restart | Always restarts |
| Non-zero (Failure) | Restarts | Restarts | Does not restart | Always restarts |

**The backoff curve — the load-bearing numbers:**

> "After containers exit, the kubelet restarts them with an exponential backoff delay: 10s, 20s, 40s, …, capped at 300 seconds (5 minutes). Once a container executes successfully for 10 minutes without problems, the kubelet resets the restart backoff timer."

## Reduced container restart delay

> "With the alpha feature gate `ReduceDefaultCrashLoopBackOffDecay` enabled, container start retries begin at 1s (instead of 10s) and increase exponentially by 2x until a maximum delay of 60s (instead of 300s/5 minutes)."

## Configurable container restart delay

> "With the feature gate `KubeletCrashLoopBackOffMax` enabled, you can reconfigure the maximum delay between container start retries from the default 300s (5 minutes). In the kubelet configuration's `crashLoopBackOff` section, set the `maxContainerRestartPeriod` field between `1s` and `300s`."

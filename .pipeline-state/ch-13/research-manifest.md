Research complete. Network degraded near the end, so two lower-priority pages are recorded as gaps rather than guessed at. Below is the manifest with all snapshots inline.

---

# Research Manifest — KCNA Chapter 13

**Stage 2 · Source Snapshot Research · fetched 2026-08-31**
Chapter 13 — *When the Cluster Won't Answer* · D2.3 Troubleshooting

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-pod-failure-signatures-2026-08-31.md` | Kubernetes project | D2.3 | pod-phase, container-states, waiting-reason-table, errimagepull, imagepullbackoff, imageinspecterror, oomkilled-signature, crashloopbackoff |
| `k8s-docs-container-restart-backoff-2026-08-31.md` | Kubernetes project | D2.3 | crashloopbackoff, restart-backoff-curve |
| `k8s-docs-debug-pods-2026-08-31.md` | Kubernetes project | D2.3 | pending-diagnosis, imagepullbackoff-diagnosis, triage-flow, kubectl-describe |
| `k8s-docs-node-pressure-eviction-2026-08-31.md` | Kubernetes project | D2.3 | evicted, node-pressure-eviction, eviction-order-by-qos-class, node-conditions-as-diagnostic |
| `k8s-docs-crictl-2026-08-31.md` | Kubernetes project | D2.3 | crictl, crictl-ps, crictl-pods, crictl-logs |
| `k8s-docs-debug-cluster-2026-08-31.md` | Kubernetes project | D2.3 | cluster-log-architecture, kubelet-health, node-conditions-as-diagnostic |
| `k8s-docs-node-controller-heartbeats-2026-08-31.md` | Kubernetes project | D2.3 | node-lease-heartbeat, node-death-handling, kubelet-health |
| `k8s-version-skew-policy-2026-08-31.md` | Kubernetes project | D2.3 | version-skew-symptoms |
| `k8s-docs-resource-metrics-pipeline-2026-08-31.md` | Kubernetes project | D2.3 | resource-metrics-pipeline, metrics-server, kubectl-top |
| `k8s-docs-logging-architecture-2026-08-31.md` | Kubernetes project | D2.3 | cluster-log-architecture, kubectl-logs, kubectl-logs-previous |
| `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31.md` | Kubernetes project | D2.3 | kubectl-logs, kubectl-logs-previous, kubectl-top, kubectl-describe, kubectl-get-pod-o-wide |
| `k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31.md` | Kubernetes project | D2.3 | event-retention-window, node-death-handling |
| `k8s-docs-troubleshooting-overview-2026-08-31.md` | Kubernetes project | D2.3 | platform-scope-vs-application-scope, release-known-issues |
| `k8s-docs-troubleshoot-kubectl-2026-08-31.md` | Kubernetes project | D2.3 | kubectl-troubleshooting |

Already in corpus and sufficient — not re-fetched: `k8s-docs-node-status-2026-08-24.md` (node conditions table, `node-monitor-grace-period` default 50s), `k8s-docs-pod-qos-2026-08-24.md`, `k8s-docs-pod-lifecycle-2026-08-23.md` (probes, restart policy), `k8s-docs-images-2026-08-23.md` (imagePullPolicy), `k8s-docs-taints-tolerations-depth-2026-08-24.md`, `k8s-docs-pod-security-admission-2026-08-31.md`, `cncf-kcna-curriculum-pdf-2026-08-23.md`.

---

### A1 · `k8s-docs-pod-failure-signatures-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/"
fetched_at: "2026-08-31T13:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["pod-phase", "container-states", "waiting-reason-table", "errimagepull", "imagepullbackoff", "imageinspecterror", "errimageneverpull", "oomkilled-signature", "crashloopbackoff"]
extraction_method: "WebFetch verbatim-transcription prompt against the rendered page. Sections retained here were cross-checked against the cached k8s-docs-pod-lifecycle-2026-08-23.md snapshot and agree with it. Confabulated sections returned in the same response were DISCARDED -- see manifest Notes for the author, item 1."
closes_gap: "B1 gap G2 -- the named Pod failure signatures, previously absent from the entire 184-file corpus."
---
# Pod Lifecycle — phase, container state, and the Waiting Reason table

> All passages below are **[VERBATIM]**.

## Pod phase

> "A Pod's `status` field is a PodStatus object, which has a `phase` field."

> "The phase of a Pod is a simple, high-level summary of where the Pod is in its lifecycle. The phase is not intended to be a comprehensive rollup of observations of container or Pod state, nor is it intended to be a comprehensive state machine."

> "The number and meanings of Pod phase values are tightly guarded. Other than what is documented here, nothing should be assumed about Pods that have a given `phase` value."

Here are the possible values for `phase`:

| Value | Description |
|-------|-------------|
| `Pending` | The Pod has been accepted by the Kubernetes cluster, but one or more of the containers has not been set up and made ready to run. This includes time a Pod spends waiting to be scheduled as well as the time spent downloading container images over the network. |
| `Running` | The Pod has been bound to a node, and all of the containers have been created. At least one container is still running, or is in the process of starting or restarting. |
| `Succeeded` | All containers in the Pod have terminated in success, and will not be restarted. |
| `Failed` | All containers in the Pod have terminated, and at least one container has terminated in failure. That is, the container either exited with non-zero status or was terminated by the system, and is not set for automatic restarting. |
| `Unknown` | For some reason the state of the Pod could not be obtained. This phase typically occurs due to an error in communicating with the node where the Pod should be running. |

### Note (verbatim) — Status is not phase

> "When a pod is failing to start repeatedly, `CrashLoopBackOff` may appear in the `Status` field of some kubectl commands. Similarly, when a pod is being deleted, `Terminating` may appear in the `Status` field of some kubectl commands."

> "Make sure not to confuse *Status*, a kubectl display field for user intuition, with the pod's `phase`. Pod phase is an explicit part of the Kubernetes data model and of the Pod API."

> "Since Kubernetes 1.27, the kubelet transitions deleted Pods to a terminal phase (`Failed` or `Succeeded` depending on the exit statuses of the pod containers) before their deletion from the API server, with two exceptions: static Pods (which are managed directly by the kubelet and represented by mirror Pods); force-deleted Pods."

## Container states

> "As well as the phase of a Pod overall, Kubernetes tracks the state of each container inside a Pod."

> "Once the scheduler assigns a Pod to a Node, the kubelet starts creating containers for that Pod using a container runtime. There are three possible container states: `Waiting`, `Running`, and `Terminated`."

> "To check the state of a Pod's containers, you can use `kubectl describe pod <name of pod>`. The output shows the state for each container within that Pod."

### `Waiting`

> "If a container is not in either `Running` or `Terminated` state, it is `Waiting`. A container in the `Waiting` state is still running the operations it requires in order to complete start up, such as pulling the container image from a container image registry, or applying Secret data."

> "When you use `kubectl` to query a Pod with a container that is `Waiting`, you also see a `Reason` field to summarize why the container is waiting."

> "Some examples of reasons for a container being in a `Waiting` state include:"

| Reason | Description |
|--------|-------------|
| `ContainerCreating` | The container is being created. |
| `ImagePullBackOff` | The container image pull has failed, and kubelet will keep trying. |
| `ImageInspectError` | There was an error inspecting the container image. |
| `ErrImageNeverPull` | The image pull policy is set to `Never`, but the image is not present locally. |
| `ErrImagePull` | There was a general error pulling the image. |
| `ErrContainerStatusUnknown` | The container status could not be obtained. |
| `PodInitializing` | The Pod is being initialized. |
| `DockerDaemonNotAvailable` | The Docker daemon is not available. |
| `DockerContainerError` | Docker returned an overall error. |
| `OOMKilled` | The container ran out of memory. |
| `ContainerCannotRun` | There was an error running the container. |
| `TransitioningReason` | The container could not complete the transition from one state to another. |
| `DeadlineExceeded` | The deadline for the Pod/container was exceeded. |
| `ContainerWaitingReason` | The container is waiting for a condition. |

### `Running`

> "The `Running` state indicates that a container is executing without issues. If there was a `postStart` hook configured, it has already executed and finished. When you use `kubectl` to query a Pod with a container that is `Running`, you also see information about when the container entered the `Running` state."

### `Terminated`

> "A container in the `Terminated` state began execution and then either ran to completion or failed for some reason. When you use `kubectl` to query a Pod with a container that is `Terminated`, you see a `Reason`, an exit code, and the start and finish time for that container."

> "If a container is configured with a `preStop` hook, this hook runs before the container enters the `Terminated` state."

## Pod conditions

> "A Pod has a `status` field that contains a PodStatus object. The `PodStatus` object has an array of PodConditions through which the Pod has or has not passed."

> "The `type` field is a string with possible values: `PodScheduled`, `ContainersReady`, `Initialized`, and `Ready`."
> "The `status` field is a string, with possible values of `True`, `False`, or `Unknown`."
> "The `reason` field is a short, machine understandable string."
> "The `message` field is a longer, human-readable string indicating details about the transition."

## Fault recovery and node death

> "If a Pod is scheduled to a node and that node then fails, the Pod is treated as unhealthy and Kubernetes eventually deletes the Pod. A Pod won't survive an eviction due to a lack of resources or Node maintenance."

> "A given Pod (as defined by a UID) is never 'rescheduled' to a different node; instead, that Pod can be replaced by a new, near-identical Pod."

> "If a Node dies, the Pods running on (or scheduled to run on) that node are marked for deletion. The control plane marks the Pods for removal after a timeout period."

## Garbage collection of Pods

> "For failed Pods, the API objects remain on the cluster until human or controller processes explicitly remove those objects."
```

---

### A2 · `k8s-docs-container-restart-backoff-2026-08-31.md` (new)
```markdown
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
```

---

### A3 · `k8s-docs-debug-pods-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/"
fetched_at: "2026-08-31T13:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["triage-flow", "pending-diagnosis", "imagepullbackoff-diagnosis", "kubectl-describe", "platform-scope-vs-application-scope"]
supersedes_note: "Fuller transcription than k8s-docs-debug-pods-2026-08-23.md, which omitted the scope disclaimer, the triage list, and the 'My pod stays terminating' section. The 08-23 file remains valid; cite this one for sec.1 and sec.2."
---
# Debug Pods

> All passages below are **[VERBATIM]**.

> "This guide is to help users debug applications that are deployed into Kubernetes and not behaving correctly. This is *not* a guide for people who want to debug their cluster. For that you should check out this guide."

## Diagnosing the problem

> "The first step in troubleshooting is triage. What is the problem? Is it your Pods, your Replication Controller or your Service?"

## Debugging Pods

> "The first step in debugging a Pod is taking a look at it. Check the current state of the Pod and recent events with the following command:"

```
kubectl describe pods ${POD_NAME}
```

> "Look at the state of the containers in the pod. Are they all `Running`? Have there been recent restarts?"

> "Continue debugging depending on the state of the pods."

### My pod stays pending

> "If a Pod is stuck in `Pending` it means that it can not be scheduled onto a node. Generally this is because there are insufficient resources of one type or another that prevent scheduling. Look at the output of the `kubectl describe ...` command above. There should be messages from the scheduler about why it can not schedule your pod. Reasons include:"

> "**You don't have enough resources**: You may have exhausted the supply of CPU or Memory in your cluster, in this case you need to delete Pods, adjust resource requests, or add new nodes to your cluster."

> "**You are using `hostPort`**: When you bind a Pod to a `hostPort` there are a limited number of places that pod can be scheduled. In most cases, `hostPort` is unnecessary, try using a Service object to expose your Pod. If you do require `hostPort` then you can only schedule as many Pods as there are nodes in your Kubernetes cluster."

### My pod stays waiting

> "If a Pod is stuck in the `Waiting` state, then it has been scheduled to a worker node, but it can't run on that machine. Again, the information from `kubectl describe ...` should be informative. The most common cause of `Waiting` pods is a failure to pull the image. There are three things to check:"

> "Make sure that you have the name of the image correct."
> "Have you pushed the image to the registry?"
> "Try to manually pull the image to see if the image can be pulled."

### My pod stays terminating

> "If a Pod is stuck in the `Terminating` state, it means that a deletion has been issued for the Pod, but the control plane is unable to delete the Pod object."

> "This typically happens if the Pod has a finalizer and there is an admission webhook installed in the cluster that prevents the control plane from removing the finalizer."

> "To identify this scenario, check if your cluster has any ValidatingWebhookConfiguration or MutatingWebhookConfiguration that target `UPDATE` operations for `pods` resources."

### My pod is crashing or otherwise unhealthy

> "Once your pod has been scheduled, the methods described in Debug Running Pods are available for debugging."

### My pod is running but not doing what I told it to do

> "If your pod is not behaving as you expected, it may be that there was an error in your pod description (e.g. `mypod.yaml` file on your local machine), and that the error was silently ignored when you created the pod. Often a section of the pod description is nested incorrectly, or a key name is typed incorrectly, and so the key is ignored. For example, if you misspelled `command` as `commnd` then the pod will be created but will not use the command line you intended it to use."

> "The first thing to do is to delete your pod and try creating it again with the `--validate` option. For example, run `kubectl apply --validate -f mypod.yaml`."

> "The next thing to check is whether the pod on the apiserver matches the pod you meant to create."

## Debugging Services

> "Services provide load balancing across a set of pods. There are several common problems that can make Services not work properly."

> "First, verify that there are endpoints for the service. For every Service object, the apiserver makes one or more `EndpointSlice` resources available."

```
kubectl get endpointslices -l kubernetes.io/service-name=${SERVICE_NAME}
```

> "Make sure that the endpoints in the EndpointSlices match up with the number of pods that you expect to be members of your service."

### My service is missing endpoints

> "If you are missing endpoints, try listing pods using the labels that Service uses."

> "Verify that the list matches the Pods that you expect to provide your Service. Verify that the pod's `containerPort` matches up with the Service's `targetPort`."
```

---

### A4 · `k8s-docs-node-pressure-eviction-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/"
fetched_at: "2026-08-31T13:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["evicted", "node-pressure-eviction", "eviction-order-by-qos-class", "node-conditions-as-diagnostic", "oomkilled-signature"]
closes_gap: "Node-pressure eviction had NO snapshot in the corpus. Load-bearing for sec.4 (Evicted vs OOMKilled) and the Exam Alert confusion pair."
---
# Node-pressure Eviction

> All passages below are **[VERBATIM]**.

> "Node-pressure eviction is the process by which the kubelet proactively terminates pods to reclaim resource on nodes."

> "The kubelet monitors resources like memory, disk space, and filesystem inodes on your cluster's nodes. When one or more of these resources reach specific consumption levels, the kubelet can proactively fail one or more pods on the node to reclaim resources and prevent starvation."

> "During a node-pressure eviction, the kubelet sets the phase for the selected pods to `Failed`, and terminates the Pod."

> "Node-pressure eviction is not the same as API-initiated eviction."

> "The kubelet does not respect your configured PodDisruptionBudget or the pod's `terminationGracePeriodSeconds`. If you use soft eviction thresholds, the kubelet respects your configured `eviction-max-pod-grace-period`. If you use hard eviction thresholds, the kubelet uses a `0s` grace period (immediate shutdown) for termination."

## Self healing behavior

> "The kubelet attempts to reclaim node-level resources before it terminates end-user pods. For example, it removes unused container images when disk resources are starved."

> "If the pods are managed by a workload management object (such as StatefulSet or Deployment) that replaces failed pods, the control plane (`kube-controller-manager`) creates new pods in place of the evicted pods."

## Eviction signals

> "Eviction signals are the current state of a particular resource at a specific point in time. The kubelet uses eviction signals to make eviction decisions by comparing the signals to eviction thresholds, which are the minimum amount of the resource that should be available on the node."

| Eviction Signal | Description |
|---|---|
| `memory.available` | `node.status.capacity[memory]` - `node.stats.memory.workingSet` |
| `nodefs.available` | `node.stats.fs.available` |
| `nodefs.inodesFree` | `node.stats.fs.inodesFree` |
| `imagefs.available` | `node.stats.runtime.imagefs.available` |
| `imagefs.inodesFree` | `node.stats.runtime.imagefs.inodesFree` |
| `containerfs.available` | `node.stats.runtime.containerfs.available` |
| `containerfs.inodesFree` | `node.stats.runtime.containerfs.inodesFree` |
| `pid.available` | `node.stats.rlimit.maxpid` - `node.stats.rlimit.curproc` |

## Eviction thresholds

> "The kubelet supports both soft and hard eviction thresholds."

> "A soft eviction threshold pairs an eviction signal with a grace period. The kubelet does not evict pods until the node conditions have been violated for the entire grace period. If no grace period is set, the kubelet evicts pods immediately upon reaching the threshold."

> "A hard eviction threshold has no grace period, and if observed, the kubelet will immediately evict pods."

> "The kubelet has the following default hard eviction thresholds:"

```
memory.available<100Mi
nodefs.available<10%
imagefs.available<15%
nodefs.inodesFree<4%
imagefs.inodesFree<4%
containerfs.available<15%
pid.available<0.5%
```

## Node conditions

> "The kubelet maps one or more eviction signals to a Kubelet Node Condition. If a hard eviction threshold has been met, or a soft eviction threshold has been met for the specified grace period, the kubelet reports a node condition (`True`) to reflect that the node is under pressure."

| Node Condition | Eviction Signal | Description |
|---|---|---|
| `MemoryPressure` | `memory.available` | Available memory on the node has satisfied an eviction threshold |
| `DiskPressure` | `nodefs.available`, `nodefs.inodesFree`, `imagefs.available`, `imagefs.inodesFree`, `containerfs.available`, `containerfs.inodesFree` | Available disk space and inodes on node has satisfied an eviction threshold |
| `PIDPressure` | `pid.available` | Available processes on the node has satisfied an eviction threshold |

### Node condition oscillation

> "In some cases, nodes oscillate above and below a soft eviction threshold with the grace period not being met, causing the corresponding node condition to oscillate between `true` and `false`, and triggering eviction of pods. To prevent this oscillation, you can use the `--eviction-pressure-transition-period` flag to specify how long the kubelet must wait before transitioning a node condition to `false`. The default is `5m`."

## Reclaiming node level resources

> "If an eviction signal has not reached a threshold, but the kubelet observes that a node-level resource is starved, the kubelet attempts to reclaim that resource before evicting end-user pods. For example, when disk space is running low, the kubelet reclaims disk space by clearing out unused images or deleting dead containers and their logs."

## Pod selection for kubelet eviction

> "If reclaiming node-level resources is insufficient, the kubelet evicts pods. The kubelet ranks pods for eviction by using the following criteria, in order of precedence:
> 1. Whether pod resource usage exceeds its requests
> 2. Pod priority
> 3. Pod resource usage relative to requests"

> "Whenever the kubelet needs to evict pods, it ranks the Pods as follows:"

> "If a pod's resource usage does not exceed its requests, the pod is ranked lower for eviction than other pods whose usage exceeds their requests. Pods that do not exceed their requests are ranked by their QoS class:
> - `BestEffort` Pods are ranked highest for eviction
> - `Burstable` Pods have a medium eviction priority
> - `Guaranteed` Pods are ranked lowest for eviction"

> "If two pods have the same QoS class, the pod with the highest resource usage is ranked highest for eviction."

### kubelet eviction: pod selection based on QoS class

| QoS Class | Requests | Usage | Rank |
|---|---|---|---|
| `BestEffort` | not set | above requests | lowest |
| `Burstable` | set | above requests | medium |
| `Guaranteed` | set | above requests | highest |
| `Guaranteed` | set | below requests | lowest |
| `Burstable` | set | below requests | medium |
| `BestEffort` | not set | below requests | highest |

## Node out of memory behavior

> "If the node experiences an out-of-memory (OOM) condition before the kubelet can reclaim memory, the node's OOM killer takes action. The OOM killer selects and kills processes based on an `oom_score_adj` value set by the kubelet for each container."

> "The kubelet sets the `oom_score_adj` value for each container based on the pod's QoS class:"

| QoS Class | oom_score_adj |
|---|---|
| `Guaranteed` | -997 |
| `BestEffort` | 1000 |
| `Burstable` | min(max(2, 1000 - (1000 * memoryRequestBytes) / memoryLimitBytes), 999) |

> "Containers with lower `oom_score_adj` values are considered less likely candidates for eviction. `Guaranteed` pods, which have low `oom_score_adj` values, are less likely to be selected by the OOM killer. `BestEffort` pods, which have `oom_score_adj` values of 1000, are the most likely to be selected."

## DaemonSets and node-pressure eviction

> "The kubelet does not evict pods created by a DaemonSet controller."

## Good practices

> "Eviction thresholds should be set lower than the node allocatable settings to provide a buffer between the eviction threshold and the amount of resources reserved for system daemons."

> "Hard eviction thresholds should not be set aggressively, as this could result in poor scheduling decisions and premature pod evictions."
```

---

### A5 · `k8s-docs-crictl-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/crictl/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["crictl", "crictl-ps", "crictl-pods", "crictl-logs", "crictl-inspect"]
closes_gap: "crictl had NO snapshot in the corpus. Ch 3 line 451 pinned the 'why a node-level tool exists' framing to Ch 13 sec.5."
depth_note: "Outline Open Question 5 recommends naming crictl, showing `crictl ps` and `crictl logs`, and spending words on the layer argument rather than the command surface. This snapshot carries more surface than the chapter should use -- that is deliberate, so the drafting stage chooses from sourced material rather than inventing."
---
# Debugging Kubernetes nodes with crictl

> All passages below are **[VERBATIM]**.

> Feature state: Stable since Kubernetes v1.11

> "`crictl` is a command-line interface for CRI-compatible container runtimes. You can use it to inspect and debug container runtimes and applications on a Kubernetes node. `crictl` and its source are hosted in the cri-tools repository."

## Before you begin

> "`crictl` requires a Linux operating system with a CRI runtime."

## Installing crictl

> "You can download a compressed archive `crictl` from the cri-tools release page, for several different architectures. Download the version that corresponds to your version of Kubernetes. Extract it and move it to a location on your system path, such as `/usr/local/bin/`."

## General usage

> "The `crictl` command has several subcommands and runtime flags. Use `crictl help` or `crictl <subcommand> help` for more details."

> "You can set the endpoint for `crictl` by doing one of the following:
> - Set the `--runtime-endpoint` and `--image-endpoint` flags.
> - Set the `CONTAINER_RUNTIME_ENDPOINT` and `IMAGE_SERVICE_ENDPOINT` environment variables.
> - Set the endpoint in the configuration file `/etc/crictl.yaml`."

> Note: "If you don't set an endpoint, `crictl` attempts to connect to a list of known endpoints, which might result in an impact to performance."

> "To view or edit the current configuration, view or edit the contents of `/etc/crictl.yaml`. For example, the configuration when using the `containerd` container runtime would be similar to this:"

```yaml
runtime-endpoint: unix:///var/run/containerd/containerd.sock
image-endpoint: unix:///var/run/containerd/containerd.sock
timeout: 10
debug: true
```

## Example crictl commands

### List pods

> "List all pods:"

```
crictl pods
```

> "The output is similar to this:"

```
POD ID              CREATED              STATE               NAME                         NAMESPACE           ATTEMPT
926f1b5a1d33a       About a minute ago   Ready               sh-84d7dcf559-4r2gq          default             0
4dccb216c4adb       About a minute ago   Ready               nginx-65899c769f-wv2gp       default             0
a86316e96fa89       17 hours ago         Ready               kube-proxy-gblk4             kube-system         0
919630b8f81f1       17 hours ago         Ready               nvidia-device-plugin-zgbbv   kube-system         0
```

> "List pods by name:"

```
crictl pods --name nginx-65899c769f-wv2gp
```

> "List pods by label:"

```
crictl pods --label run=nginx
```

### List images

```
crictl images
```

```
IMAGE                                     TAG                 IMAGE ID            SIZE
busybox                                   latest              8c811b4aec35f       1.15MB
nginx                                     latest              cd5239a0906a6       109MB
```

### List containers

> "List all containers:"

```
crictl ps -a
```

> "The output is similar to this:"

```
CONTAINER ID        IMAGE                                       CREATED             STATE               NAME                       ATTEMPT
1f73f2d81bf98       busybox@sha256:141c253bc4c3...              7 minutes ago       Running             sh                         1
9c5951df22c78       busybox@sha256:141c253bc4c3...              8 minutes ago       Exited              sh                         0
87d3992f84f74       nginx@sha256:d0a8828cccb733...              8 minutes ago       Running             nginx                      0
```

> "List running containers:"

```
crictl ps
```

### Execute a command in a running container

```
crictl exec -i -t 1f73f2d81bf98 ls
```

```
bin   dev   etc   home  proc  root  sys   tmp   usr   var
```

### Get a container's logs

> "Get all container logs:"

```
crictl logs 87d3992f84f74
```

```
10.240.0.96 - - [06/Jun/2018:02:45:49 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.47.0" "-"
10.240.0.96 - - [06/Jun/2018:02:45:50 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.47.0" "-"
```

> "Get only the latest `N` lines of logs:"

```
crictl logs --tail=1 87d3992f84f74
```
```

---

### A6 · `k8s-docs-debug-cluster-2026-08-31.md` (new)
```markdown
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

```
kubectl get nodes
```

> "And verify that all of the nodes you expect to see are present and that they are all in the `Ready` state."

> "To get detailed information about the overall health of your cluster, you can run:"

```
kubectl cluster-info dump
```

### Example: debugging a down/unreachable node

> "Sometimes when debugging it can be useful to look at the status of a node -- for example, because you've noticed strange behavior of a Pod that's running on the node, or to find out why a Pod won't schedule onto the node. As with Pods, you can use `kubectl describe node` and `kubectl get node -o yaml` to retrieve detailed information about nodes. For example, here's what you'll see if a node is down (disconnected from the network, or kubelet dies and won't restart, etc.). Notice the events that show the node is NotReady, and also notice that the pods are no longer running (they are evicted after five minutes of NotReady status)."

```
NAME                     STATUS       ROLES     AGE     VERSION
kube-worker-1            NotReady     <none>    1h      v1.23.3
kubernetes-node-bols     Ready        <none>    1h      v1.23.3
```

Excerpt of `kubectl describe node kube-worker-1` for a dead node:

```
Taints:             node.kubernetes.io/unreachable:NoExecute
                    node.kubernetes.io/unreachable:NoSchedule
Lease:
  HolderIdentity:  kube-worker-1
  AcquireTime:     <unset>
  RenewTime:       Thu, 17 Feb 2022 17:13:09 -0500
Conditions:
  Type                 Status    LastHeartbeatTime                 LastTransitionTime                Reason              Message
  ----                 ------    -----------------                 ------------------                ------              -------
  NetworkUnavailable   False     Thu, 17 Feb 2022 17:09:13 -0500   Thu, 17 Feb 2022 17:09:13 -0500   WeaveIsUp           Weave pod has set this
  MemoryPressure       Unknown   Thu, 17 Feb 2022 17:12:40 -0500   Thu, 17 Feb 2022 17:13:52 -0500   NodeStatusUnknown   Kubelet stopped posting node status.
  DiskPressure         Unknown   Thu, 17 Feb 2022 17:12:40 -0500   Thu, 17 Feb 2022 17:13:52 -0500   NodeStatusUnknown   Kubelet stopped posting node status.
  PIDPressure          Unknown   Thu, 17 Feb 2022 17:12:40 -0500   Thu, 17 Feb 2022 17:13:52 -0500   NodeStatusUnknown   Kubelet stopped posting node status.
  Ready                Unknown   Thu, 17 Feb 2022 17:12:40 -0500   Thu, 17 Feb 2022 17:13:52 -0500   NodeStatusUnknown   Kubelet stopped posting node status.
```

A healthy node's conditions, from `kubectl get node -o yaml`:

```yaml
  conditions:
  - lastHeartbeatTime: "2022-02-17T22:20:15Z"
    message: kubelet has sufficient memory available
    reason: KubeletHasSufficientMemory
    status: "False"
    type: MemoryPressure
  - lastHeartbeatTime: "2022-02-17T22:20:15Z"
    message: kubelet is posting ready status
    reason: KubeletReady
    status: "True"
    type: Ready
```

## Looking at logs

> "For now, digging deeper into the cluster requires logging into the relevant machines. Here are the locations of the relevant log files. On systemd-based systems, you may need to use `journalctl` instead of examining log files."

### Control Plane nodes

> "`/var/log/kube-apiserver.log` - API Server, responsible for serving the API"
> "`/var/log/kube-scheduler.log` - Scheduler, responsible for making scheduling decisions"
> "`/var/log/kube-controller-manager.log` - a component that runs most Kubernetes built-in controllers, with the notable exception of the scheduler"

### Worker Nodes

> "`/var/log/kubelet.log` - Kubelet, responsible for running containers on the node"
> "`/var/log/kube-proxy.log` - Kube-proxy, responsible for service load balancing"
```

---

### A7 · `k8s-docs-node-controller-heartbeats-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/architecture/nodes/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/architecture/nodes.md"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 -- fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["node-lease-heartbeat", "node-death-handling", "kubelet-health", "node-conditions-as-diagnostic"]
closes_gap: "ch-13 outline Open Question 4, item 3 -- the node-death eviction timeout, which the outline barred from being written from memory. It is taint-based, and the node controller's wait is documented here."
companion: "Node conditions table and the node-monitor-grace-period default (50 seconds) are already sourced in k8s-docs-node-status-2026-08-24.md. Cite that file for the conditions themselves -- sec.5's guardrail forbids restating the table anyway."
---
# Node heartbeats and the node controller

> All passages below are **[VERBATIM]** from the kubernetes/website source markdown.

## Node heartbeats

> "Heartbeats sent by Kubernetes nodes help your cluster determine the availability of each node, and to take action when failures are detected."

> "For nodes there are two forms of heartbeats:
> - Updates to the `.status` of a Node.
> - Lease objects within the `kube-node-lease` namespace. Each Node has an associated Lease object."

## Node controller

> "The node controller is a Kubernetes control plane component that manages various aspects of nodes."

> "The node controller has multiple roles in a node's life. The first is assigning a CIDR block to the node when it is registered (if CIDR assignment is turned on)."

> "The second is keeping the node controller's internal list of nodes up to date with the cloud provider's list of available machines. When running in a cloud environment and whenever a node is unhealthy, the node controller asks the cloud provider if the VM for that node is still available. If not, the node controller deletes the node from its list of nodes."

> "The third is monitoring the nodes' health. The node controller is responsible for:
> - In the case that a node becomes unreachable, updating the `Ready` condition in the Node's `.status` field. In this case the node controller sets the `Ready` condition to `Unknown`.
> - If a node remains unreachable: triggering API-initiated eviction for all of the Pods on the unreachable node. **By default, the node controller waits 5 minutes between marking the node as `Unknown` and submitting the first eviction request.**"

> "By default, the node controller checks the state of each node every 5 seconds. This period can be configured using the `--node-monitor-period` flag on the `kube-controller-manager` component."

### Rate limits on eviction

> "In most cases, the node controller limits the eviction rate to `--node-eviction-rate` (default 0.1) per second, meaning it won't evict pods from more than 1 node per 10 seconds."

> "The node eviction behavior changes when a node in a given availability zone becomes unhealthy. The node controller checks what percentage of nodes in the zone are unhealthy (the `Ready` condition is `Unknown` or `False`) at the same time:
> - If the fraction of unhealthy nodes is at least `--unhealthy-zone-threshold` (default 0.55), then the eviction rate is reduced.
> - If the cluster is small (i.e. has less than or equal to `--large-cluster-size-threshold` nodes - default 50), then evictions are stopped.
> - Otherwise, the eviction rate is reduced to `--secondary-node-eviction-rate` (default 0.01) per second."

> "The corner case is when all zones are completely unhealthy (none of the nodes in the cluster are healthy). In such a case, the node controller assumes that there is some problem with connectivity between the control plane and the nodes, and doesn't perform any evictions."

### Taints for node problems

> "The node controller is also responsible for evicting pods running on nodes with `NoExecute` taints, unless those pods tolerate that taint. The node controller also adds taints corresponding to node problems like node unreachable or not ready. This means that the scheduler won't place Pods onto unhealthy nodes."
```

---

### A8 · `k8s-version-skew-policy-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/releases/version-skew-policy/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/releases), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["version-skew-symptoms", "release-known-issues"]
supersedes_note: "Fuller than k8s-version-skew-policy-2026-08-23.md (2.1KB), which Ch 8 sec.6 cites. Ch 8's citation stands; cite THIS file for Ch 13 sec.6. Version numbers on the page have advanced to the 1.35-1.37 series since the 08-23 fetch -- see manifest Notes for the author, item 5."
lts_finding: "The page contains NO statement using the term 'long-term support' or 'LTS'. It documents a three-minor-release support window and ~1 year of patch support. See manifest Notes item 6 -- this bears on outline Open Question 3."
---
# Version Skew Policy

> All passages below are **[VERBATIM]**.

> "This document describes the maximum version skew supported between various Kubernetes components. Specific cluster deployment tools may place additional restrictions on version skew."

## Supported versions

> "Kubernetes versions are expressed as **x.y.z**, where **x** is the major version, **y** is the minor version, and **z** is the patch version, following Semantic Versioning terminology."

> "The Kubernetes project maintains release branches for the most recent three minor releases (1.37, 1.36, 1.35). Kubernetes 1.19 and newer receive approximately 1 year of patch support. Kubernetes 1.18 and older received approximately 9 months of patch support."

> "Applicable fixes, including security fixes, may be backported to those three release branches, depending on severity and feasibility. Patch releases are cut from those branches at a regular cadence, plus additional urgent releases, when required."

## Supported version skew

### kube-apiserver

> "In highly-available (HA) clusters, the newest and oldest `kube-apiserver` instances must be within one minor version."

> Example: "newest `kube-apiserver` is at **1.37**; other `kube-apiserver` instances are supported at **1.37** and **1.36**"

### kubelet

> "`kubelet` must not be newer than `kube-apiserver`."
> "`kubelet` may be up to three minor versions older than `kube-apiserver` (`kubelet` < 1.25 may only be up to two minor versions older than `kube-apiserver`)."

> Example: "`kube-apiserver` is at **1.37**; `kubelet` is supported at **1.37**, **1.36**, **1.35**, and **1.34**"

> Note: "If version skew exists between `kube-apiserver` instances in an HA cluster, this narrows the allowed `kubelet` versions."

> Example: "`kube-apiserver` instances are at **1.37** and **1.36**; `kubelet` is supported at **1.36**, **1.35**, and **1.34** (**1.37** is not supported because that would be newer than the `kube-apiserver` instance at version **1.36**)"

### kube-proxy

> "`kube-proxy` must not be newer than `kube-apiserver`."
> "`kube-proxy` may be up to three minor versions older than `kube-apiserver`."
> "`kube-proxy` may be up to three minor versions older or newer than the `kubelet` instance it runs alongside."

### kube-controller-manager, kube-scheduler, and cloud-controller-manager

> "`kube-controller-manager`, `kube-scheduler`, and `cloud-controller-manager` must not be newer than the `kube-apiserver` instances they communicate with. They are expected to match the `kube-apiserver` minor version, but may be up to one minor version older (to allow live upgrades)."

### kubectl

> "`kubectl` is supported within one minor version (older or newer) of `kube-apiserver`."

> Example: "`kube-apiserver` is at **1.37**; `kubectl` is supported at **1.38**, **1.37**, and **1.36**"

## Supported component upgrade order

> "The supported version skew between components has implications on the order in which components must be upgraded."

> Note: "Project policies for API deprecation and API change guidelines require `kube-apiserver` to not skip minor versions when upgrading, even in single-instance clusters."

> Note (kubelet): "Before performing a minor version `kubelet` upgrade, drain pods from that node. In-place minor version `kubelet` upgrades are not supported."

> Warning: "Running a cluster with `kubelet` instances that are persistently three minor versions behind `kube-apiserver` means they must be upgraded before the control plane can be upgraded."

> Warning: "Running a cluster with `kube-proxy` instances that are persistently three minor versions behind `kube-apiserver` means they must be upgraded before the control plane can be upgraded."
```

---

### A9 · `k8s-docs-resource-metrics-pipeline-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["resource-metrics-pipeline", "metrics-server", "kubectl-top"]
supersedes_note: "Fuller than k8s-docs-resource-metrics-pipeline-2026-08-23.md (2.2KB). sec.7 is the definition home for metrics-server and Ch 17 sec.7 / Ch 18 sec.3 both refer back to it, so the definition must be complete enough to be referred to rather than re-derived -- cite THIS file."
---
# Resource metrics pipeline

> All passages below are **[VERBATIM]**.

> "For Kubernetes, the *Metrics API* offers a basic set of metrics to support automatic scaling and similar use cases. This API makes information available about resource usage for node and pod, including metrics for CPU and memory. If you deploy the Metrics API into your cluster, clients of the Kubernetes API can then query for this information, and you can use Kubernetes' access control mechanisms to manage permissions to do so."

> "The HorizontalPodAutoscaler (HPA) and VerticalPodAutoscaler (VPA) use data from the metrics API to adjust workload replicas and resources to meet customer demand."

> "You can also view the resource metrics using the `kubectl top` command."

> Note: "The Metrics API, and the metrics pipeline that it enables, only offers the minimum CPU and memory metrics to enable automatic scaling using HPA and / or VPA. If you would like to provide a more complete set of metrics, you can complement the simpler Metrics API by deploying a second metrics pipeline that uses the *Custom Metrics API*."

## The architecture components

> "The architecture components, from right to left in the figure, consist of the following:"

> "**cAdvisor**: Daemon for collecting, aggregating and exposing container metrics included in Kubelet."

> "**kubelet**: Node agent for managing container resources. Resource metrics are accessible using the `/metrics/resource` and `/stats` kubelet API endpoints."

> "**node level resource metrics**: API provided by the kubelet for discovering and retrieving per-node summarized stats available through the `/metrics/resource` endpoint."

> "**metrics-server**: Cluster addon component that collects and aggregates resource metrics pulled from each kubelet. The API server serves Metrics API for use by HPA, VPA, and by the `kubectl top` command. Metrics Server is a reference implementation of the Metrics API."

> "**Metrics API**: Kubernetes API supporting access to CPU and memory used for workload autoscaling. To make this work in your cluster, you need an API extension server that provides the Metrics API."

The rendered figure shows the flow: `Container runtime -> cAdvisor -> kubelet -> (node level resource metrics) -> Metrics-Server -> (metrics API) -> API server -> HPA`, with `API server -> kubectl top` as a separate consumer.

## Metrics API

> "The metrics-server implements the Metrics API. This API allows you to access CPU and memory usage for the nodes and pods in your cluster. Its primary role is to feed resource usage metrics to K8s autoscaler components."

> "Here is an example of the Metrics API request for a `minikube` node piped through `jq` for easier reading:"

```
kubectl get --raw "/apis/metrics.k8s.io/v1/nodes/minikube" | jq '.'
```

> "Sample response:"

```json
{
  "kind": "NodeMetrics",
  "apiVersion": "metrics.k8s.io/v1",
  "metadata": { "name": "minikube" },
  "timestamp": "2022-01-27T18:48:33Z",
  "window": "30s",
  "usage": { "cpu": "487558164n", "memory": "732212Ki" }
}
```

> "The Metrics API is defined in the k8s.io/metrics repository. You must enable the API aggregation layer and register an APIService for the `metrics.k8s.io` API."

> **Note: "You must deploy the metrics-server or alternative adapter that serves the Metrics API to be able to access it."**

## Measuring resource usage

### CPU

> "CPU is reported as the average core usage measured in cpu units. One cpu, in Kubernetes, is equivalent to 1 vCPU/Core for cloud providers, and 1 hyper-thread on bare-metal Intel processors."

> "This value is derived by taking a rate over a cumulative CPU counter provided by the kernel (in both Linux and Windows kernels). The time window used to calculate CPU is shown under window field in Metrics API."

### Memory

> "Memory is reported as the working set, measured in bytes, at the instant the metric was collected."

> "In an ideal world, the 'working set' is the amount of memory in-use that cannot be freed under memory pressure. However, calculation of the working set varies by host OS, and generally makes heavy use of heuristics to produce an estimate."

## Metrics Server

> "The metrics-server fetches resource metrics from the kubelets and exposes them in the Kubernetes API server through the Metrics API for use by the HPA and VPA. You can also view these metrics using the `kubectl top` command."

> "The metrics-server uses the Kubernetes API to track nodes and pods in your cluster. The metrics-server queries each node over HTTP to fetch metrics. The metrics-server also builds an internal view of pod metadata, and keeps a cache of pod health."

> "The metrics-server calls the kubelet API to collect metrics from each node. Depending on the metrics-server version it uses:
> - Metrics resource endpoint `/metrics/resource` in version v0.6.0+ or
> - Summary API endpoint `/stats/summary` in older versions"
```

---

### A10 · `k8s-docs-logging-architecture-2026-08-31.md` (new)
```markdown
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

```
kubectl logs counter
```

> "You can use `kubectl logs --previous` to retrieve logs from a previous instantiation of a container. If your pod has multiple containers, specify which container's logs you want to access by appending a container name to the command, with a `-c` flag, like so:"

```
kubectl logs counter -c count
```

## How nodes handle container logs

> "A container runtime handles and redirects any output generated to a containerized application's `stdout` and `stderr` streams. Different container runtimes implement this in different ways; however, the integration with the kubelet is standardized as the *CRI logging format*."

> **"By default, if a container restarts, the kubelet keeps one terminated container with its logs. If a pod is evicted from the node, all corresponding containers are also evicted, along with their logs."**

> "The kubelet makes logs available to clients via a special feature of the Kubernetes API. The usual way to access this is by running `kubectl logs`."

## Log rotation

> "The kubelet is responsible for rotating container logs and managing the logging directory structure. The kubelet sends this information to the container runtime (using CRI), and the runtime writes the container logs to the given location."

> "You can configure two kubelet configuration settings, `containerLogMaxSize` (default 10Mi) and `containerLogMaxFiles` (default 5), using the kubelet configuration file. These settings let you configure the maximum size for each log file and the maximum number of files allowed for each container respectively."

> "When you run `kubectl logs` as in the basic logging example, the kubelet on the node handles the request and reads directly from the log file. The kubelet returns the content of the log file."

> **Note: "Only the contents of the latest log file are available through `kubectl logs`."**

> "For example, if a Pod writes 40 MiB of logs and the kubelet rotates logs after 10 MiB, running `kubectl logs` returns at most 10MiB of data."

## System component logs

> "There are two types of system components: those that typically run in a container, and those components directly involved in running containers. For example:
> - The kubelet and container runtime do not run in containers. The kubelet runs your containers (grouped together in pods)
> - The Kubernetes scheduler, controller manager, and API server run within pods (usually static Pods). The etcd component runs in the control plane, and most commonly also as a static pod. If your cluster uses kube-proxy, you typically run this as a `DaemonSet`."

### Log locations (Linux)

> "On Linux nodes that use systemd, the kubelet and container runtime write to journald by default. You use `journalctl` to read the systemd journal; for example: `journalctl -u kubelet`."

> "If systemd is not present, the kubelet and container runtime write to `.log` files in the `/var/log` directory."

> "By default, kubelet directs your container runtime to write logs into directories within `/var/log/pods`."

## Cluster-level logging architectures

> "While Kubernetes does not provide a native storage solution for log data, you can choose from several approaches to integrate logging solutions into your cluster."

### Using a node logging agent

> "You can implement cluster-level logging by including a *node-level logging agent* on each node. The logging agent is a dedicated tool that exposes logs or pushes logs to a backend. Commonly, the logging agent is a container that has access to a directory with log files from all of the application containers on that node."

> "Because the logging agent must run on every node, it is common to implement it as a DaemonSet replica, a manifest Pod, or a dedicated native process on the node."

### Using a sidecar container with the logging agent

> "You can use a sidecar container in one of the following ways:
> 1. The sidecar container streams application logs to its own `stdout`.
> 2. The sidecar container runs a logging agent that is configured to pick up logs from an application container."

### Exposing logs directly from the application

> "You can also implement cluster-level logging by exposing or pushing logs directly from every application. However, the responsibility of exposing logs is then left to the application, which may be seen as a disadvantage."
```

---

### A11 · `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/reference/kubectl/quick-reference/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["kubectl-logs", "kubectl-logs-previous", "kubectl-describe", "kubectl-top", "kubectl-get-pod-o-wide"]
closes_gap: "B1 gap G1 -- the kubectl command surface. Partial: see manifest Gaps, item 1 (kubectl events is NOT covered)."
---
# kubectl Quick Reference — troubleshooting subset

> All command lines and their trailing comments below are **[VERBATIM]**.

## Interacting with running Pods

```bash
kubectl logs my-pod                                 # dump pod logs (stdout)
kubectl logs -l name=myLabel                        # dump pod logs, label selector
kubectl logs my-pod --previous                      # dump the previous pod's logs (useful if the pod has restarted)
kubectl logs my-pod -c my-container                 # dump pod container logs (stdout, multi-container case)
kubectl logs my-pod -c my-container --previous      # dump the previous pod's container logs (stdout, multi-container case)
kubectl logs -f my-pod                              # stream pod logs (stdout)
kubectl logs -f my-pod -c my-container              # stream pod container logs (stdout, multi-container case)
kubectl logs -f deployment/my-dep -c my-container   # stream pod logs (stdout)
kubectl logs my-pod --all-containers=true           # dump pod logs, all containers
kubectl logs -f deployment/my-dep --all-containers=true # stream pod logs, all containers
kubectl logs my-pod --tail=20                       # dump the last 20 lines of pod logs
kubectl logs my-pod --since=1h                      # dump pod logs, including timestamps
kubectl exec my-pod -- ls /                         # run command in pod
kubectl exec --stdin --tty my-pod -- /bin/sh        # Interactive TTY shell access to a pod
kubectl exec my-pod -c my-container -- ls /         # run command in pod - multi-container case
kubectl attach my-pod -i                            # Attach to the running container
kubectl port-forward my-pod 5000:6000               # Listen on port 5000 on the local machine and forward to port 6000 on my-pod
kubectl top pod POD_NAME                            # Show metrics for a given pod
kubectl top pod --all-namespaces                    # Show metrics for all pods in all namespaces
```

## Describe commands with verbose output

```bash
kubectl describe nodes my-node
kubectl describe pods my-pod
```

## Interacting with Nodes and cluster

```bash
kubectl cluster-info                        # display endpoint information about the master and services in the cluster
kubectl cluster-info dump                   # dump current cluster state to stdout
kubectl cluster-info dump --output-directory=/path/to/cluster-state # dump current cluster state to /path/to/cluster-state

kubectl get nodes                           # List all nodes
kubectl describe node my-node               # Display detailed information about one node
kubectl top node                            # Show metrics for all nodes
kubectl top node my-node                    # Show metrics for a given node

kubectl cordon my-node                      # Mark my-node as unschedulable
kubectl drain my-node                       # Drain my-node in preparation for maintenance
kubectl uncordon my-node                    # Mark my-node as schedulable
```

## Additional output

```bash
kubectl get pods -o wide                      # List all pods in the current namespace, with more details
kubectl get nodes -o wide                     # List all nodes with additional columns
```
```

---

### A12 · `k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31.md` (new)
```markdown
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

```
--event-ttl duration     Default: 1h0m0s
```

> "Amount of time to retain events."

## `--default-not-ready-toleration-seconds`

```
--default-not-ready-toleration-seconds int     Default: 300
```

> "Indicates the tolerationSeconds of the toleration for notReady:NoExecute that is added by default to every pod that does not already have such a toleration."

## `--default-unreachable-toleration-seconds`

```
--default-unreachable-toleration-seconds int     Default: 300
```

> "Indicates the tolerationSeconds of the toleration for unreachable:NoExecute that is added by default to every pod that does not already have such a toleration."

## `--min-request-timeout`

```
--min-request-timeout int     Default: 1800
```

> "An optional field indicating the minimum number of seconds a handler must keep a request open before timing it out. Currently only honored by the watch request handler, which picks a randomized value above this number as the connection timeout, to spread out load."

---

## Drafting notes

1. **Event retention is one hour by default.** This is a `kube-apiserver` flag, so it is a
   cluster-configurable default, not a constant. sec.3's "events expire; the absence of an event
   is not evidence" Hazard is now sourced. Present it as "one hour by default, and the
   administrator can change it" -- never as a fixed property of Kubernetes.
2. **The node-death timeout is 300 seconds, and it is taint-based.** The outline correctly
   recorded that this moved off `--pod-eviction-timeout`. The mechanism is a default
   `NoExecute` toleration with `tolerationSeconds: 300` that the API server adds to every Pod
   lacking one. This agrees with the independent statement in
   `k8s-docs-debug-cluster-2026-08-31.md` -- "they are evicted after five minutes of NotReady
   status" -- and with the node controller's documented five-minute wait in
   `k8s-docs-node-controller-heartbeats-2026-08-31.md`. Three sources, one number.
3. **TTL as an acronym.** If sec.3 names `--event-ttl`, outline Open Question 7 applies -- TTL
   has no acronym-register row. The alternative is to describe the behaviour and cite the flag
   without spelling the acronym.
```

---

### A13 · `k8s-docs-troubleshooting-overview-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["platform-scope-vs-application-scope", "triage-flow", "release-known-issues"]
load_bearing: "This is the official statement of the two-audience split that sec.1 owns, and the official warrant for sec.6's 'release-specific known issues as a legitimate triage step'."
---
# Monitoring, Logging, and Debugging (Troubleshooting overview)

> All passages below are **[VERBATIM]**.

> "Set up monitoring and logging to troubleshoot a cluster, or debug a containerized application."

> "Sometimes things go wrong. This guide helps you gather the relevant information and resolve issues. It has four sections:"

> "**Debugging your application** - Useful for users who are deploying code into Kubernetes and wondering why it is not working."

> "**Debugging your cluster** - Useful for cluster administrators and operators troubleshooting issues with the Kubernetes cluster itself."

> "**Logging in Kubernetes** - Useful for cluster administrators who want to set up and manage logging in Kubernetes."

> "**Monitoring in Kubernetes** - Useful for cluster administrators who want to enable monitoring in a Kubernetes cluster."

> **"You should also check the known issues for the release you're using."**
> (links to https://github.com/kubernetes/kubernetes/releases)

## Getting help — scope routing

> "If you have questions related to *software development* for your containerized app, you can ask those on Stack Overflow."

> "If you have Kubernetes questions related to *cluster management* or *configuration*, you can ask those on Server Fault."

## Bugs and feature requests

> "If you have what looks like a bug, or you would like to make a feature request, please use the GitHub issue tracking system."

> "If filing a bug, please include detailed information about how to reproduce the problem, such as:
> - Kubernetes version: `kubectl version`
> - Cloud provider, OS distro, network configuration, and container runtime version
> - Steps to reproduce the problem"
```

---

### A14 · `k8s-docs-troubleshoot-kubectl-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/troubleshoot-kubectl/"
fetched_at: "2026-08-31T14:10:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["kubectl-troubleshooting", "kubeconfig-context"]
partial_note: "PARTIAL. The fetch truncated after 'Check kubeconfig'. The sections on insufficient permissions, configuration context, API server connectivity and TLS errors are NOT reproduced here. Do not cite this snapshot for those. See manifest Gaps, item 2."
---
# Troubleshooting kubectl (partial)

> All passages below are **[VERBATIM]**.

> "This documentation is about investigating and diagnosing kubectl related issues. If you encounter issues accessing `kubectl` or connecting to your cluster, this document outlines various common scenarios and potential solutions to help identify and address the likely cause."

## Verify kubectl setup

> "Make sure you have installed and configured `kubectl` correctly on your local machine. Check the `kubectl` version to ensure it is up-to-date and compatible with your cluster."

> "Check kubectl version:"

```
kubectl version
```

> "You'll see a similar output:"

```
Client Version: version.Info{Major:"1", Minor:"27", GitVersion:"v1.27.4", ...}
Kustomize Version: v5.0.1
Server Version: version.Info{Major:"1", Minor:"27", GitVersion:"v1.27.3", ...}
```

> **"If you see `Unable to connect to the server: dial tcp <server-ip>:8443: i/o timeout`, instead of `Server Version`, you need to troubleshoot kubectl connectivity with your cluster."**

> "Make sure you have installed the kubectl by following the official documentation for installing kubectl, and you have properly configured the `$PATH` environment variable."

## Check kubeconfig

> "The `kubectl` requires a `kubeconfig` file to connect to a Kubernetes cluster. The `kubeconfig` file is usually located under the `~/.kube/config` directory. Make sure that you have a valid `kubeconfig` file. If you don't have a `kubeconfig` file, you can obtain it from your Kubernetes administrator, or you can copy it from your Kubernetes control plane's `/etc/kubernetes/admin.conf` directory. If you have deployed your Kubernetes cluster on a cloud platform and lost your `kubeconfig` file, you can re-generate it using your cloud provider's tools."

> "Check if the `$KUBECONFIG` environment variable is configured correctly. You can set `$KUBECONFIG` environment variable or use the `--kubeconfig` parameter with kubectl to specify the directory of a `kubeconfig` file."
```

---

## Gaps

Flagged so the drafting stage does **not** invent facts to fill them.

1. **`kubectl events` command reference — NOT FETCHED.** The generated reference page returned no output on two attempts. The cheat sheet subset in A11 does **not** contain a `kubectl events` line or a `kubectl get events --sort-by=` line. §3 owns `kubectl events` as an introduced command. **Do not write its flag surface (`--for`, `--types`, `--watch`) from memory.** Either re-fetch `https://kubernetes.io/docs/reference/kubectl/generated/kubectl_events/` before drafting §3, or restrict §3 to `kubectl describe` and `kubectl logs`, which are fully sourced, and name `kubectl events` without flags.

2. **`CreateContainerConfigError` — UNSOURCED.** This is the significant find. §2 lists it as an owned signature and Ch 12:1099 points here for the missing-Secret case, but **it does not appear in the official container-state `Reason` table** (A1), which is the authoritative list. The table has `ContainerCreating`, `ImagePullBackOff`, `ImageInspectError`, `ErrImageNeverPull`, `ErrImagePull`, `ErrContainerStatusUnknown`, `PodInitializing`, `DockerDaemonNotAvailable`, `DockerContainerError`, `OOMKilled`, `ContainerCannotRun`, `TransitioningReason`, `DeadlineExceeded`, `ContainerWaitingReason` — and no `CreateContainerConfigError`. It is a real kubelet-emitted reason, but kubernetes.io does not document it. **§2 must not present it as a documented Reason string** unless a source is found. See Notes item 3 for the recommended handling; this also affects the Ch 12:1099 debt.

3. **The literal `Evicted` reason string — UNSOURCED.** A4 states only that "the kubelet sets the phase for the selected pods to `Failed`, and terminates the Pod." The word `Evicted` as a status/reason value appears nowhere in the fetched eviction documentation. §4 and the Exam Alert both hinge on `OOMKilled` vs `Evicted` as a paired contrast. **What is sourced is the phase (`Failed`), the killer (kubelet vs kernel OOM killer), the trigger (node pressure vs the container's limit), and the QoS ordering.** Build the contrast on those four axes, which are fully sourced, and treat the display string `Evicted` as illustrative rather than examinable.

4. **`kubectl top` error text when metrics-server is absent — UNSOURCED.** A9 pins the load-bearing fact ("You must deploy the metrics-server or alternative adapter that serves the Metrics API to be able to access it") and that metrics-server is a "Cluster addon component." The *literal* error message a reader sees is not in any official page fetched. **Do not quote an error string.** State the behaviour, not the text.

5. **Release-specific known issues — POINTER ONLY.** A13 gives the official warrant ("You should also check the known issues for the release you're using") but there is no dated snapshot of an actual known-issues list; those live in per-release CHANGELOGs on GitHub. §6 can legitimately teach *consulting* the list as a triage step. It cannot cite a specific known issue.

6. **`troubleshoot-kubectl` is partial** (A14). Covered: version check, the `i/o timeout` error, kubeconfig location, `$KUBECONFIG`. Not covered: permissions, context errors, API-server connectivity, TLS. §3's "confirm which cluster and which context you are talking to" beat is sourced for the *kubeconfig* half; the *context* half is not. `k8s-docs-kubectl-overview-2026-08-23.md` may cover contexts — check it before drafting.

7. **`determine-reason-pod-failure` — NOT FETCHED** (termination messages, exit codes, `terminationMessagePath`, `terminationMessagePolicy`). Not required by any section as written, but it is the natural source if §4 wants to discuss exit codes. Currently the only sourced statement about exit codes is A1's "you see a `Reason`, an exit code, and the start and finish time."

8. **Dedicated probes page — NOT FETCHED.** Probe failure signatures are nonetheless **adequately sourced**: the cached `k8s-docs-pod-lifecycle-2026-08-23.md` and an independent fetch this session both carry "if the readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod" and the liveness→kill→restart-policy statement. Two independent agreements. §4's readiness signature (`Running`, `0/1 Ready`, dropped from endpoints) is safe to write. The *displayed* `0/1 Ready` column is an inference from the mechanism, not a quote.

9. **CNCF sub-competency weights — CONFIRMED ABSENT, not a research failure.** `cncf-kcna-curriculum-pdf-2026-08-23.md` publishes four domain weights only (44/28/16/12), with Troubleshooting listed as an unweighted sub-competency of Container Orchestration. This **confirms** the outline's handling: 4% is an authored allocation, 28% is the published figure for D2, and the disclaimer is required.

---

## Notes for the author

1. **The fetch tool confabulated, and I discarded the output.** One transcription of the Pod Lifecycle page returned three sections that do not exist: a `pod.spec.readyForStartupChecks` field, a "Configurable container restart delay" section describing `podFailurePolicy` as a Pod-spec field at v1.26 beta (it is a Job field, and the real section is about `KubeletCrashLoopBackOffMax`), and a kubelet-restart-detection section built on a UID file. **None of it is in A1 or A2.** Everything retained was either cross-checked against the cached 08-23 snapshot or re-fetched from the kubernetes/website source markdown. Flagging it because it is a standing risk for this stage, not a one-off: **treat any single fetch of a long page as unverified.**

2. **The restart-backoff reset window was the specific trap Open Question 4 predicted, and it caught the tooling.** A rendered-page fetch reported the reset at **5 minutes**. The source markdown and the cached 08-23 snapshot both say **10 minutes**. Two-to-one for 10 minutes, and the source markdown is the page's own origin. **Use: 10s, 20s, 40s, …, capped at 300 seconds (5 minutes); reset after 10 minutes of successful execution.** Note the cap and the reset are different five/ten-minute quantities — that is exactly the kind of pair a reader mis-remembers, and it argues for §4 stating both explicitly rather than gesturing at "a few minutes." Both numbers are now pinned, so the outline's fallback ("write the shape") is not needed.

3. **`CreateContainerConfigError` needs an author decision before §2 is drafted.** It is the string a reader will actually see when a Pod references a missing ConfigMap or Secret, and Ch 12:1099 has already promised this chapter will explain that case. But kubernetes.io does not document it (Gap 2). Three options: **(a)** teach the *case* (missing Secret → container cannot be configured → Pod never starts) and name the string as "what the kubelet reports, though it is not in the documented Reason table" — honest, and preserves the Ch 12 debt; **(b)** find a source — the string is in the kubelet source and in the CRI docs, neither of which is an acceptable authority under this stage's priority order; **(c)** drop the string and discharge Ch 12:1099 via `ErrImagePull`-family framing, which would not actually answer what Ch 12 promised. **Recommend (a).** It is the only option that keeps the promise without asserting an undocumented fact as documented.

4. **`OOMKilled` sits in the docs' *Waiting* table, which is a genuine source oddity.** A1's Reason table is introduced as "reasons for a container being in a `Waiting` state" and it includes `OOMKilled`. In practice `OOMKilled` is a `Terminated` reason — a container that was OOM-killed *ran*. This matters because Ch 5 §5 owns the phase/state taxonomy and §4 owns the `OOMKilled` signature, and the ⚑2 guardrail forbids §2 from re-teaching the taxonomy. **Do not let §4 cite the Waiting table as evidence that `OOMKilled` is a Waiting reason** — it would contradict shipped Ch 5 and confuse the very taxonomy the chapter is keyed on. Present `OOMKilled` via the `Terminated` state ("you see a `Reason`, an exit code, and the start and finish time"), which is also sourced in A1.

5. **The version numbers on the skew page have moved since Ch 8 shipped.** The 08-23 snapshot that Ch 8 §6 cites was taken when the supported branches were an earlier trio; the page now reads 1.37 / 1.36 / 1.35, and the kubelet example runs 1.37 / 1.36 / 1.35 / 1.34. **The rule is unchanged** — three minor releases maintained, kubelet up to three minor versions older than kube-apiserver — and the rule is what §6 retrieves. Since §6's guardrail is "retrieve the rule; do not restate the table," this drift should not surface in the text at all. Worth knowing so nobody "corrects" Ch 8's example numbers to match: **if a version number appears in §6, the section has taken the wrong turn.**

6. **Open Question 3 (LTS) — the sources do not let you say what you wanted to say.** The version-skew page never uses the term "LTS" or "long-term support." What it does say is precise and quotable: three maintained release branches, and "Kubernetes 1.19 and newer receive approximately 1 year of patch support." So "there is no Kubernetes LTS" is an *inference from absence*, not a sourced claim, and under this chapter's own standard it cannot be graded. **Recommendation: take option (b) from the outline** — accept that §6 cannot raise the LTS question and bar any item hinging on it — **or** retrofit Ch 8 §6 with the positive, sourced form ("support runs three minor releases and about a year of patches") rather than the negative form ("there is no LTS"). The positive form is defensible from A8; the negative form is not.

7. **§1's two-audience split is now sourced, and better than expected.** A13 is the Kubernetes project's own scope routing, in its own words: application debugging is "for users who are deploying code into Kubernetes," cluster debugging is "for cluster administrators and operators troubleshooting issues with the Kubernetes cluster itself," and the debug-cluster page opens by assuming "you have already ruled out your application as the root cause." That is the Ch 13 / Ch 16 boundary stated by the authority, which means §1 can *cite* the split rather than assert it — and the figure `ch13-fig01-two-audience-split` has a documented basis for both columns.

8. **Three independent sources agree on the five-minute node-death window**, which is unusually good footing for a number the outline flagged as risky: the API server's default `tolerationSeconds: 300` on both NoExecute taints (A12), the node controller's documented five-minute wait between marking a node `Unknown` and the first eviction request (A7), and the worked example in A6 ("they are evicted after five minutes of NotReady status"). §5 can state it plainly. Note it is a *default*, and the mechanism is a toleration the API server injects — which is a small, elegant retrieval of Ch 7 §4's taints material in a diagnostic register, exactly the kind of applied reuse §5 wants.

9. **PodDisruptionBudget (⚑3) — one sourced sentence now exists, if the author wants it.** A4 says the kubelet "does not respect your configured PodDisruptionBudget" during node-pressure eviction. That is a *negative* fact about PDB in precisely §4's context, and it does not require PDB to be defined. It does not resolve Open Question 2 — PDB is still unowned, and this sentence would still be the term's first appearance in the book. **Recommend keeping the bar in place.** Recording it because it is the cheapest possible retrofit if the author picks option (a): Ch 8 §4 gains one clause, and §4 here gains a genuinely useful "and it will not save you under node pressure" beat.
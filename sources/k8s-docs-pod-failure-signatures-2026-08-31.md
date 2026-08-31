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

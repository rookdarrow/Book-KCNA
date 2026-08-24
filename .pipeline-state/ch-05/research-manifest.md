All source material is gathered. One blocker to report first.

## Blocker: this session has no filesystem write access

`Write` is denied for every path, and sandboxed Bash refuses output redirection even into `C:\dev\lodestar\certcomp` itself. That matches `CLAUDE.md`'s note that the executor removes `Write` from `--allowed-tools` so stage output flows through stdout — which works for a single-artifact stage, but this stage produces six files.

The research itself is **complete**: all four blocking gaps from § Open questions #2 are closed, plus the sidecar page for #3. Everything below is finished content, ready to write verbatim. The orchestrator captures stdout into `research-manifest.md`, so the manifest lands correctly; the five snapshots need a materialization pass.

---

# Research Manifest — KCNA Chapter 5

## Snapshots fetched

### New this stage (pending write to `../Book-KCNA/sources/`)

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-pods-2026-08-24.md` | Kubernetes project | D1.1 | pod · smallest-deployable-unit · co-located-co-scheduled · pod-shared-context · pod-network-namespace · pod-ip · localhost-communication · pod-shared-volumes · podspec · pod-template · single-container-pod · multi-container-pod · pod-ephemerality · pod-replacement |
| `k8s-docs-init-containers-2026-08-24.md` | Kubernetes project | D1.1 | init-container · init-container-ordering · run-to-completion · restart-policy · phase-pending |
| `k8s-docs-pod-qos-2026-08-24.md` | Kubernetes project | D1.1 | qos-class · qos-guaranteed · qos-burstable · qos-besteffort · pod-eviction · resource-request · resource-limit |
| `k8s-docs-sidecar-containers-2026-08-24.md` | Kubernetes project | D1.1 | sidecar-container · multi-container-pod · init-container · probe |
| `k8s-docs-pod-termination-2026-08-24.md` | Kubernetes project | D1.1 | pod-termination · pod-lifetime · pod-phase · restart-policy |

### Already cached and verified against this chapter's needs

| Snapshot | Covers |
|---|---|
| `k8s-docs-pod-lifecycle-2026-08-23.md` | §5 phases/states/`restartPolicy`/backoff · §7 probes — **fully sourced, verified this stage** |
| `k8s-docs-resource-management-2026-08-23.md` | §8 movements 1–3 including the `m`/`M` warning — verified |
| `k8s-docs-service-accounts-2026-08-23.md` | §6 all four facts + TokenRequest — **G7 confirmed closed** |
| `k8s-docs-network-model-2026-08-23.md` | §1 unique cluster-wide IP, private namespace, `localhost` — verified |
| `k8s-docs-containers-2026-08-23.md` | §1 co-located/co-scheduled · §4 immutability parallel — verified |
| `k8s-docs-workloads-2026-08-23.md` | §1 Pod definition · §4 controllers create replacements — verified |
| `k8s-docs-names-and-uids-2026-08-24.md` | §4 UID distinguishes historical occurrences — verified |
| `k8s-docs-images-2026-08-23.md` | §5 `ImagePullBackOff` + `imagePullPolicy` (Ch 2 pinned payoff) — verified |
| `k8s-docs-secret-2026-08-23.md` | §6 `kubernetes.io/service-account-token` (Ch 4 pinned payoff) — verified |
| `k8s-docs-kubectl-overview-2026-08-23.md` | `kubectl-get` / `-describe` / `-explain` — verified |

## Gaps

**None blocking.** Every concept in `kb_tags` now resolves to an authoritative source. G3 is closed (QoS half retrieved); the Pod concept page, init containers, and the pod-lifecycle termination tail are all retrieved.

Two minor items, neither load-bearing:

- **`status.qosClass`** — the QoS page does not name this field in its prose. Do not assert the field name in the draft; say the class is assigned, not where it is reported.
- **`kubectl explain` detail** — only the one-line operation description is cached. Sufficient for the passing mention `kb_tags` implies; insufficient if drafting wants a worked invocation.

## Notes for the author

**1. Three open questions are now answerable.**

- **#3 (sidecar implementation)** — the source establishes it plainly: *"Kubernetes implements sidecar containers as a special case of init containers"*, active by default since v1.29, enabled via `restartPolicy: Always` on an `initContainers` entry. Your recommendation's condition is met. It also connects §2 and §3 exactly as you predicted, and the sidecar page carries the ordering guarantee and reverse-order termination.
- **#5 (graceful termination)** — now fully sourced: default grace period 30 seconds, `preStop` hook, TERM then KILL, `terminationGracePeriodSeconds`, and the 2-second one-off extension. Your proposed altitude — *"termination is a request with a deadline, not an instant event"* — is directly supportable.
- **#7 (init resource accounting)** — documented on **both** the init-containers and sidecar pages, in plain terms. It is less obscure than the outline assumed. Still your call whether §8 can absorb it.

**2. One correction the draft should not overstate.** §3's plan says a failed init container is restarted "according to the Pod's `restartPolicy`." The source adds a wrinkle: *"if the Pod `restartPolicy` is set to Always, the init containers use `restartPolicy` OnFailure."* The `Never` → Pod-failed behavior is exactly as planned; the `Always` case is not a straight inheritance.

**3. §7's "init containers don't carry probes" needs the sidecar exception.** Sourced as *"Regular init containers ... do not support the `lifecycle`, `livenessProbe`, `readinessProbe`, or `startupProbe` fields"* — the word *regular* is load-bearing, because sidecars support all three. If §2 names the modern implementation (#3), §7's axis needs the qualifier.

**4. QoS criteria carry clauses the outline didn't anticipate.** Burstable and BestEffort now both reference *"or the Pod has a Pod-level memory or CPU request or limit"* — Pod-level resources, a newer feature. The three-class taxonomy is unaffected and associate-tier framing holds; just don't quote the criteria as a clean two-bullet list. Also useful for `ch05-fig05`: the QoS class is fixed at creation and immutable for the Pod's lifetime.

**5. Version drift in the docs.** The Pods page reads "in Kubernetes v1.36." The KCNA curriculum is effective 2025-11-24. Nothing in Chapter 5's material is version-sensitive at associate tier, but the Pod conditions list now includes `PodReadyToStartContainers` (beta), `DisruptionTarget`, `PodResizePending`, and `PodResizeInProgress` — all almost certainly out of scope, and worth holding out alongside your § Open questions #11 list.

**6. Termination has an EndpointSlice entanglement.** The termination section states the control plane evaluates removal from EndpointSlice objects concurrently with shutdown. If #5 goes in, §4 must not develop this — it collides with your §7 instruction not to teach EndpointSlice, and Ch 9 owns the object.

**7. Provenance note on two fetches.** `k8s-docs-pods-2026-08-24.md` and `k8s-docs-pod-termination-2026-08-24.md` were retrieved from the `kubernetes/website` repository's raw markdown, because the rendered pages truncated mid-document. Same document, same authority, canonical URL recorded in `source_url` with the raw path in `source_url_raw`. `k8s-docs-init-containers-2026-08-24.md` is a merge of both retrievals for the same reason.

---

## Files to write

Each block below is a complete file. Path first, content between the markers.

<details>
<summary><code>../Book-KCNA/sources/k8s-docs-pods-2026-08-24.md</code></summary>

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/"
source_url_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/workloads/pods/_index.md"
fetched_at: "2026-08-24T06:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["pod", "smallest-deployable-unit", "co-located-co-scheduled", "pod-shared-context", "pod-network-namespace", "pod-ip", "localhost-communication", "pod-shared-volumes", "podspec", "pod-template", "single-container-pod", "multi-container-pod", "sidecar-container", "pod-ephemerality", "pod-replacement", "pod-lifetime"]
---
# Pods (kubernetes.io/docs/concepts/workloads/pods/)

## Opening definition

*Pods* are the smallest deployable units of computing that you can create and manage in Kubernetes.

A *Pod* (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. A Pod's contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific "logical host": it contains one or more application containers which are relatively tightly coupled. In non-cloud contexts, applications executed on the same physical or virtual machine are analogous to cloud applications executed on the same logical host.

As well as application containers, a Pod can contain init containers that run during Pod startup. You can also inject ephemeral containers for debugging a running Pod.

## What is a Pod?

Note: You need to install a container runtime into each node in the cluster so that Pods can run there.

The shared context of a Pod is a set of Linux namespaces, cgroups, and potentially other facets of isolation - the same things that isolate a container. Within a Pod's context, the individual applications may have further sub-isolations applied.

A Pod is similar to a set of containers with shared namespaces and shared filesystem volumes.

## Pods with multiple containers

Pods are designed to support multiple cooperating processes (as containers) that form a cohesive unit of service. The containers in a Pod are automatically co-located and co-scheduled on the same physical or virtual machine in the cluster. The containers can share resources and dependencies, communicate with one another, and coordinate when and how they are terminated.

Pods in a Kubernetes cluster are used in two main ways:

* **Pods that run a single container**. The "one-container-per-Pod" model is the most common Kubernetes use case; in this case, you can think of a Pod as a wrapper around a single container; Kubernetes manages Pods rather than managing the containers directly.
* **Pods that run multiple containers that need to work together**. A Pod can encapsulate an application composed of multiple co-located containers that are tightly coupled and need to share resources. These co-located containers form a single cohesive unit of service—for example, one container serving data stored in a shared volume to the public, while a separate sidecar container refreshes or updates those files. The Pod wraps these containers, storage resources, and an ephemeral network identity together as a single unit.

    Grouping multiple co-located and co-managed containers in a single Pod is a relatively advanced use case. You should use this pattern only in specific instances in which your containers are tightly coupled.

    You don't need to run multiple containers to provide replication (for resilience or capacity); if you need multiple replicas, see Workload management.

## Using Pods

The following is an example of a Pod which consists of a container running the image `nginx:1.14.2`.

    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

To create the Pod shown above, run the following command:

    kubectl apply -f https://k8s.io/examples/pods/simple-pod.yaml

Pods are generally not created directly and are created using workload resources.

## Working with Pods

You'll rarely create individual Pods directly in Kubernetes—even singleton Pods. This is because Pods are designed as relatively ephemeral, disposable entities. When a Pod gets created (directly by you, or indirectly by a controller), the new Pod is scheduled to run on a Node in your cluster. The Pod remains on that node until the Pod finishes execution, the Pod object is deleted, the Pod is *evicted* for lack of resources, or the node fails.

Note: Restarting a container in a Pod should not be confused with restarting a Pod. A Pod is not a process, but an environment for running container(s). A Pod persists until it is deleted.

### Pods and controllers

You can use workload resources to create and manage multiple Pods for you. A controller for the resource handles replication and rollout and automatic healing in case of Pod failure. For example, if a Node fails, a controller notices that Pods on that Node have stopped working and creates a replacement Pod. The scheduler places the replacement Pod onto a healthy Node.

Here are some examples of workload resources that manage one or more Pods:

* Deployment
* StatefulSet
* DaemonSet

### Pod templates

Controllers for workload resources create Pods from a *pod template* and manage those Pods on your behalf.

PodTemplates are specifications for creating Pods, and are included in workload resources such as Deployments, Jobs, and DaemonSets.

Each controller for a workload resource uses the `PodTemplate` inside the workload object to make actual Pods. The `PodTemplate` is part of the desired state of whatever workload resource you used to run your app.

When you create a Pod, you can include environment variables in the Pod template for the containers that run in the Pod.

## Pod update and replacement

As mentioned in the previous section, when the Pod template for a workload resource is changed, the controller creates new Pods based on the updated template instead of updating or patching the existing Pods.

Kubernetes doesn't prevent you from managing Pods directly. It is possible to update some fields of a running Pod, in place. However, Pod update operations like `patch`, and `replace` have some limitations:

- Most of the metadata about a Pod is immutable. For example, you cannot change the `namespace`, `name`, `uid`, or `creationTimestamp` fields.
- If the `metadata.deletionTimestamp` is set, no new entry can be added to the `metadata.finalizers` list.
- Pod updates may not change fields other than `spec.containers[*].image`, `spec.initContainers[*].image`, `spec.activeDeadlineSeconds`, `spec.terminationGracePeriodSeconds`, `spec.tolerations` or `spec.schedulingGates`. For `spec.tolerations`, you can only add new entries.
- When updating the `spec.activeDeadlineSeconds` field, two types of updates are allowed:
  1. setting the unassigned field to a positive number;
  2. updating the field from a positive number to a smaller, non-negative number.

## Resource sharing and communication

Pods enable data sharing and communication among their constituent containers.

### Storage in Pods

A Pod can specify a set of shared storage volumes. All containers in the Pod can access the shared volumes, allowing those containers to share data. Volumes also allow persistent data in a Pod to survive in case one of the containers within needs to be restarted. See Storage for more information on how Kubernetes implements shared storage and makes it available to Pods.

### Pod networking

Each Pod is assigned a unique IP address for each address family. Every container in a Pod shares the network namespace, including the IP address and network ports. Inside a Pod (and **only** then), the containers that belong to the Pod can communicate with one another using `localhost`. When containers in a Pod communicate with entities *outside the Pod*, they must coordinate how they use the shared network resources (such as ports). Within a Pod, containers share an IP address and port space, and can find each other via `localhost`. The containers in a Pod can also communicate with each other using standard inter-process communications like SystemV semaphores or POSIX shared memory. Containers in different Pods have distinct IP addresses and can not communicate by OS-level IPC without special configuration. Containers that want to interact with a container running in a different Pod can use IP networking to communicate.

Containers within the Pod see the system hostname as being the same as the configured `name` for the Pod. There's more about this in the networking section.

## Static Pods

*Static Pods* are managed directly by the kubelet daemon on a specific node, without the API server observing them. Whereas most Pods are managed by the control plane (for example, a Deployment), for static Pods, the kubelet directly supervises each static Pod (and restarts it if it fails).

Static Pods are always bound to one kubelet on a specific node. The main use for static Pods is to run a self-hosted control plane: in other words, using the kubelet to supervise the individual control plane components.

## Pod OS

FEATURE STATE: `Kubernetes v1.25 [stable]`

You should set the `.spec.os.name` field to either `windows` or `linux` to indicate the operating system that the containers in that Pod require. These two are the only operating systems supported for now by Kubernetes. In the future, this list may be expanded.

The kubelet refuses to run a Pod if the value of `.spec.os.name` does not match the operating system of the node. However, in Kubernetes v1.36, the value of `.spec.os.name` does not affect how the kube-scheduler picks a node for the Pod to run on. In any cluster where there is more than one operating system for running nodes, you should set the `kubernetes.io/os` label correctly on each node, and define pods with a `nodeSelector` based on the operating system label. The kube-scheduler assigns your pod to a node based on other criteria and may or may not succeed in picking a suitable node placement where the node OS is right for the containers in that Pod. The Pod security standards also use this field to avoid enforcing policies that aren't relevant to the operating system.
```

</details>

<details>
<summary><code>../Book-KCNA/sources/k8s-docs-init-containers-2026-08-24.md</code></summary>

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/init-containers/"
source_url_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/workloads/pods/init-containers.md"
fetched_at: "2026-08-24T06:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["init-container", "init-container-ordering", "run-to-completion", "restart-policy", "phase-pending", "sidecar-container"]
---
# Init Containers (kubernetes.io/docs/concepts/workloads/pods/init-containers/)

## Overview

This page provides an overview of init containers: specialized containers that run before app containers in a Pod. Init containers can contain utilities or setup scripts not present in an app image.

## Understanding init containers

A Pod can have multiple containers running apps within it, but it can also have one or more init containers, which are run before the app containers are started.

Init containers are exactly like regular containers, except:

* Init containers always run to completion.
* Each init container must complete successfully before the next one starts.

If a Pod's init container fails, the kubelet repeatedly restarts that init container until it succeeds. However, if the Pod has a `restartPolicy` of Never, and an init container fails during startup of that Pod, Kubernetes treats the overall Pod as failed.

## Differences from regular containers

Init containers support all the fields and features of app containers, including resource limits, volumes, and security settings. However, the resource requests and limits for an init container are handled differently, as documented in Resource sharing within containers.

Regular init containers (in other words: excluding sidecar containers) do not support the `lifecycle`, `livenessProbe`, `readinessProbe`, or `startupProbe` fields. Init containers must run to completion before the Pod can be ready; sidecar containers continue running during a Pod's lifetime, and *do* support some probes.

## Differences from sidecar containers

Init containers run and complete their tasks before the main application container starts. Unlike sidecar containers, init containers are not continuously running alongside the main containers.

Init containers run to completion sequentially, and the main container does not start until all the init containers have successfully completed.

init containers do not support `lifecycle`, `livenessProbe`, `readinessProbe`, or `startupProbe` whereas sidecar containers support all these probes to control their lifecycle.

Init containers share the same resources (CPU, memory, network) with the main application containers but do not interact directly with them. They can, however, use shared volumes for data exchange.

## Using init containers

Because init containers have separate images from app containers, they have some advantages for start-up related code:

* Init containers can contain utilities or custom code for setup that are not present in an app image. For example, there is no need to make an image `FROM` another image just to use a tool like `sed`, `awk`, `python`, or `dig` during setup.
* The application image builder and deployer roles can work independently without the need to jointly build a single app image.
* Init containers can run with a different view of the filesystem than app containers in the same Pod. Consequently, they can be given access to Secrets that app containers cannot access.
* Because init containers run to completion before any app containers start, init containers offer a mechanism to block or delay app container startup until a set of preconditions are met. Once preconditions are met, all of the app containers in a Pod can start in parallel.
* Init containers can securely run utilities or custom code that would otherwise make an app container image less secure. By keeping unnecessary tools separate you can limit the attack surface of your app container image.

## Detailed behavior

During Pod startup, the kubelet delays running init containers until the networking and storage are ready. Then the kubelet runs the Pod's init containers in the order they appear in the Pod's spec.

Each init container must exit successfully before the next container starts. If a container fails to start due to the runtime or exits with failure, it is retried according to the Pod `restartPolicy`. However, if the Pod `restartPolicy` is set to Always, the init containers use `restartPolicy` OnFailure.

A Pod cannot be `Ready` until all init containers have succeeded. The ports on an init container are not aggregated under a Service. A Pod that is initializing is in the `Pending` state but should have a condition `Initialized` set to false.

If the Pod restarts, or is restarted, all init containers must execute again.

## Resource sharing within containers

The highest of any particular resource request or limit defined on all init containers is the *effective init request/limit*. If any resource has no resource limit specified this is considered as the highest limit.

The Pod's *effective request/limit* for a resource is the higher of:

* the sum of all app containers request/limit for a resource
* the effective init request/limit for a resource

## Pod restart reasons

The Pod infrastructure container is restarted. This is uncommon and would have to be done by someone with root access to nodes.

All containers in a Pod are terminated while `restartPolicy` is set to Always, forcing a restart, and the init container completion record has been lost due to garbage collection.
```

</details>

<details>
<summary><code>../Book-KCNA/sources/k8s-docs-pod-qos-2026-08-24.md</code></summary>

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/pod-qos/"
fetched_at: "2026-08-24T06:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1 Scheduling", "D1.1"]
concepts_covered: ["qos-class", "qos-guaranteed", "qos-burstable", "qos-besteffort", "resource-request", "resource-limit", "pod-eviction"]
---
# Pod Quality of Service Classes (kubernetes.io/docs/concepts/workloads/pods/pod-qos/)

## Overview

Kubernetes classifies the Pods that you run and allocates each Pod into a specific *quality of service (QoS) class*. Kubernetes uses that classification to influence how different pods are handled. Kubernetes does this classification based on the resource requests of the Containers in that Pod, along with how those requests relate to resource limits. This is known as Quality of Service (QoS) class. Kubernetes assigns every Pod a QoS class based on the resource requests and limits of its component Containers. QoS classes are used by Kubernetes to decide which Pods to evict from a Node experiencing Node Pressure. The possible QoS classes are `Guaranteed`, `Burstable`, and `BestEffort`. When a Node runs out of resources, Kubernetes will first evict `BestEffort` Pods running on that Node, followed by `Burstable` and finally `Guaranteed` Pods. When this eviction is due to resource pressure, only Pods exceeding resource requests are candidates for eviction.

## Guaranteed

Pods that are `Guaranteed` have the strictest resource limits and are least likely to face eviction. They are guaranteed not to be killed until they exceed their limits or there are no lower-priority Pods that can be preempted from the Node. They may not acquire resources beyond their specified limits.

### Criteria

For a Pod to be given a QoS class of `Guaranteed`:

* Every Container in the Pod must have a memory limit and a memory request, both greater than zero.
* For every Container in the Pod, the memory limit must equal the memory request.
* Every Container in the Pod must have a CPU limit and a CPU request, both greater than zero.
* For every Container in the Pod, the CPU limit must equal the CPU request.

## Burstable

Pods that are `Burstable` have some lower-bound resource guarantees based on the request, but do not require a specific limit. If a limit is not specified, it defaults to a limit equivalent to the capacity of the Node, which allows the Pods to flexibly increase their resources if resources are available. In the event of Pod eviction due to Node resource pressure, these Pods are evicted only after all `BestEffort` Pods are evicted. Because a `Burstable` Pod can include a Container that has no resource limits or requests, a Pod that is `Burstable` can try to use any amount of node resources.

### Criteria

A Pod is given a QoS class of `Burstable` if:

* The Pod does not meet the criteria for QoS class `Guaranteed`.
* At least one Container in the Pod has a memory or CPU request or limit, or the Pod has a Pod-level memory or CPU request or limit.

## BestEffort

Pods in the `BestEffort` QoS class can use node resources that aren't specifically assigned to Pods in other QoS classes.

The kubelet prefers to evict `BestEffort` Pods if the node comes under resource pressure.

### Criteria

A Pod has a QoS class of `BestEffort` if it doesn't meet the criteria for either `Guaranteed` or `Burstable`. In other words, a Pod is `BestEffort` only if none of the Containers in the Pod have a memory limit or a memory request, and none of the Containers in the Pod have a CPU limit or a CPU request, and the Pod does not have any Pod-level memory or CPU limits or requests. Containers in a Pod can request other resources (not CPU or memory) and still be classified as `BestEffort`.

## Some behavior is independent of QoS class

Certain behavior is independent of the QoS class assigned by Kubernetes. For example:

* Any Container exceeding a resource limit will be killed and restarted by the kubelet without affecting other Containers in that Pod.

* If a Container exceeds its resource request and the node it runs on faces resource pressure, the Pod it is in becomes a candidate for eviction. If this occurs, all Containers in the Pod will be terminated. Kubernetes may create a replacement Pod, usually on a different node.

* The resource request of a Pod is equal to the sum of the resource requests of its component Containers, and the resource limit of a Pod is equal to the sum of the resource limits of its component Containers.

* The kube-scheduler does not consider QoS class when selecting which Pods to preempt. Preemption can occur when a cluster does not have enough resources to run all the Pods you defined.

* The QoS class is determined when the Pod is created and remains unchanged for the lifetime of the Pod. If you later attempt an in-place resize that would result in a different QoS class, the resize is rejected by admission.
```

</details>

<details>
<summary><code>../Book-KCNA/sources/k8s-docs-sidecar-containers-2026-08-24.md</code></summary>

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/"
fetched_at: "2026-08-24T06:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["sidecar-container", "multi-container-pod", "init-container", "init-container-ordering", "probe", "restart-policy", "qos-class"]
---
# Sidecar Containers (kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/)

## Overview

Sidecar containers are the secondary containers that run along with the main application container within the same Pod. These containers are used to enhance or to extend the functionality of the primary *app container* by providing additional services, or functionality such as logging, monitoring, security, or data synchronization, without directly altering the primary application code.

## Enabling sidecar containers

Kubernetes implements sidecar containers as a special case of init containers; sidecar containers remain running after Pod startup. This document uses the term *regular init containers* to clearly refer to containers that only run during Pod startup.

Provided that your cluster has the `SidecarContainers` feature gate enabled (the feature is active by default since Kubernetes v1.29), you can specify a `restartPolicy` for containers listed in a Pod's `initContainers` field. These restartable *sidecar* containers are independent from other init containers and from the main application container(s) within the same pod. These can be started, stopped, or restarted without affecting the main application container and other init containers.

## Differences from application containers

Sidecar containers run alongside *app containers* in the same pod. However, they do not execute the primary application logic; instead, they provide supporting functionality to the main application.

Sidecar containers have their own independent lifecycles. They can be started, stopped, and restarted independently of app containers. This means you can update, scale, or maintain sidecar containers without affecting the primary application.

Sidecar containers share the same network and storage namespaces with the primary container. This co-location allows them to interact closely and share resources.

From a Kubernetes perspective, the sidecar container's graceful termination is less important. When other containers take all allotted graceful termination time, the sidecar containers will receive the `SIGTERM` signal, followed by the `SIGKILL` signal, before they have time to terminate gracefully. So exit codes different from `0` (`0` indicates successful exit), for sidecar containers are normal on Pod termination and should be generally ignored by the external tooling.

## Differences from init containers

Sidecar containers work alongside the main container, extending its functionality and providing additional services.

Sidecar containers run concurrently with the main application container. They are active throughout the lifecycle of the pod and can be started and stopped independently of the main container. Unlike init containers, sidecar containers support probes to control their lifecycle.

Sidecar containers can interact directly with the main application containers, because like init containers they always share the same network, and can optionally also share volumes (filesystems).

Init containers stop before the main containers start up, so init containers cannot exchange messages with the app container in a Pod. Any data passing is one-way (for example, an init container can put information inside an `emptyDir` volume).

Changing the image of a sidecar container will not cause the Pod to restart, but will trigger a container restart.

## Sidecar containers and Pod lifecycle

If an init container is created with its `restartPolicy` set to `Always`, it will start and remain running during the entire life of the Pod. This can be helpful for running supporting services separated from the main application containers.

If a `readinessProbe` is specified for this init container, its result will be used to determine the `ready` state of the Pod.

Since these containers are defined as init containers, they benefit from the same ordering and sequential guarantees as regular init containers, allowing you to mix sidecar containers with regular init containers for complex Pod initialization flows.

Compared to regular init containers, sidecars defined within `initContainers` continue to run after they have started. This is important when there is more than one entry inside `.spec.initContainers` for a Pod. After a sidecar-style init container is running (the kubelet has set the `started` status for that init container to true), the kubelet then starts the next init container from the ordered `.spec.initContainers` list. That status either becomes true because there is a process running in the container and no startup probe defined, or as a result of its `startupProbe` succeeding.

Upon Pod termination, the kubelet postpones terminating sidecar containers until the main application container has fully stopped. The sidecar containers are then shut down in the opposite order of their appearance in the Pod specification. This approach ensures that the sidecars remain operational, supporting other containers within the Pod, until their service is no longer required.

## Resource sharing within containers

Given the order of execution for init, sidecar and app containers, the following rules for resource usage apply:

* The highest of any particular resource request or limit defined on all init containers is the *effective init request/limit*. If any resource has no resource limit specified this is considered as the highest limit.
* The Pod's *effective request/limit* for a resource is the sum of pod overhead and the higher of:
    * the sum of all non-init containers(app and sidecar containers) request/limit for a resource
    * the effective init request/limit for a resource
* Scheduling is done based on effective requests/limits, which means init containers can reserve resources for initialization that are not used during the life of the Pod.
* The QoS (quality of service) tier of the Pod's *effective QoS tier* is the QoS tier for all init, sidecar and app containers alike.

Quota and limits are applied based on the effective Pod request and limit.
```

</details>

<details>
<summary><code>../Book-KCNA/sources/k8s-docs-pod-termination-2026-08-24.md</code></summary>

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/"
source_url_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/workloads/pods/pod-lifecycle.md"
fetched_at: "2026-08-24T06:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["pod-termination", "pod-lifetime", "pod-phase", "pod-conditions", "restart-policy", "pod-eviction"]
---
# Pod Lifecycle — conditions, termination, and garbage collection

Continuation snapshot. This file covers the sections of the Pod Lifecycle page that follow "Container probes"; phases, container states, restartPolicy and probes are cached separately in `k8s-docs-pod-lifecycle-2026-08-23.md`.

## Pod conditions

A Pod has a PodStatus, which has an array of PodConditions through which the Pod has or has not passed. The kubelet manages the following PodConditions:

* `PodScheduled`: the Pod has been scheduled to a node.
* `PodReadyToStartContainers`: (beta feature; enabled by default) the Pod sandbox has been successfully created, networking configured, storage volumes mounted, and any dynamic resources (if requested) allocated.
* `ContainersReady`: all containers in the Pod are ready.
* `Initialized`: all init containers have completed successfully.
* `Ready`: the Pod is able to serve requests and should be added to the load balancing pools of all matching Services.
* `DisruptionTarget`: the pod is about to be terminated due to a disruption (such as preemption, eviction or garbage-collection).
* `PodResizePending`: a pod resize was requested but cannot be applied.
* `PodResizeInProgress`: the pod is in the process of resizing.

| Field name | Description |
|---|---|
| `type` | Name of this Pod condition. |
| `status` | Indicates whether that condition is applicable, with possible values "`True`", "`False`", or "`Unknown`". |
| `lastProbeTime` | Timestamp of when the Pod condition was last probed. |
| `lastTransitionTime` | Timestamp for when the Pod last transitioned from one status to another. |
| `reason` | Machine-readable, UpperCamelCase text indicating the reason for the condition's last transition. |
| `message` | Human-readable message indicating details about the last status transition. |

### Pod readiness

Your application can inject extra feedback or signals into PodStatus: *Pod readiness*. To use this, set `readinessGates` in the Pod's `spec` to specify a list of additional conditions that the kubelet evaluates for Pod readiness.

Readiness gates are determined by the current state of `status.condition` fields for the Pod. If Kubernetes cannot find such a condition in the `status.conditions` field of a Pod, the status of the condition is defaulted to "`False`".

## Termination of Pods

Because Pods represent processes running on nodes in the cluster, it is important to allow those processes to gracefully terminate when they are no longer needed (rather than being abruptly stopped with a `KILL` signal and having no chance to clean up).

The design aim is for you to be able to request deletion and know when processes terminate, but also be able to ensure that deletes eventually complete. When you request deletion of a Pod, the cluster records and tracks the intended grace period before the Pod is allowed to be forcefully killed. With that forceful shutdown tracking in place, the kubelet attempts graceful shutdown.

Typically, with this graceful termination of the pod, kubelet makes requests to the container runtime to attempt to stop the containers in the pod by first sending a TERM (aka. SIGTERM) signal, with a grace period timeout, to the main process in each container. The requests to stop the containers are processed by the container runtime asynchronously. There is no guarantee to the order of processing for these requests. Many container runtimes respect the `STOPSIGNAL` value defined in the container image and, if different, send the container image configured STOPSIGNAL instead of TERM. Once the grace period has expired, the KILL signal is sent to any remaining processes, and the Pod is then deleted from the API Server. If the kubelet or the container runtime's management service is restarted while waiting for processes to terminate, the cluster retries from the start including the full original grace period.

### Pod Termination Flow

Pod termination flow, illustrated with an example:

1. You use the `kubectl` tool to manually delete a specific Pod, with the default grace period (30 seconds).

2. The Pod in the API server is updated with the time beyond which the Pod is considered "dead" along with the grace period. If you use `kubectl describe` to check the Pod you're deleting, that Pod shows up as "Terminating". On the node where the Pod is running: as soon as the kubelet sees that a Pod has been marked as terminating (a graceful shutdown duration has been set), the kubelet begins the local Pod shutdown process.

   1. If one of the Pod's containers has defined a `preStop` hook and the `terminationGracePeriodSeconds` in the Pod spec is not set to 0, the kubelet runs that hook inside of the container. The default `terminationGracePeriodSeconds` setting is 30 seconds.

      If the `preStop` hook is still running after the grace period expires, the kubelet requests a small, one-off grace period extension of 2 seconds.

      If the `preStop` hook needs longer to complete than the default grace period allows, you must modify `terminationGracePeriodSeconds` to suit this.

   2. The kubelet triggers the container runtime to send a TERM signal to process 1 inside each container.

      There is special ordering if the Pod has any sidecar containers defined. Otherwise, the containers in the Pod receive the TERM signal at different times and in an arbitrary order. If the order of shutdowns matters, consider using a `preStop` hook to synchronize (or switch to using sidecar containers).

3. At the same time as the kubelet is starting graceful shutdown of the Pod, the control plane evaluates whether to remove that shutting-down Pod from EndpointSlice objects, where those objects represent a Service with a configured selector. ReplicaSets and other workload resources no longer treat the shutting-down Pod as a valid, in-service replica.

   Pods that shut down slowly should not continue to serve regular traffic and should start terminating and finish processing open connections. Some applications need to go beyond finishing open connections and need more graceful termination, for example, session draining and completion.

   Any endpoints that represent the terminating Pods are not immediately removed from EndpointSlices, and a status indicating terminating state is exposed from the EndpointSlice API. Terminating endpoints always have their `ready` status as `false` (for backward compatibility with versions before 1.26), so load balancers will not use it for regular traffic.

   If traffic draining on terminating Pod is needed, the actual readiness can be checked as a condition `serving`. You can find more details on how to implement connections draining in the tutorial Pods And Endpoints Termination Flow.

4. The kubelet ensures the Pod is shut down and terminated

   1. When the grace period expires, if there is still any container running in the Pod, the kubelet triggers forcible shutdown. The container runtime sends `SIGKILL` to any processes still running in any container in the Pod. The kubelet also cleans up a hidden `pause` container if that container runtime uses one.
   2. The kubelet transitions the Pod into a terminal phase (`Failed` or `Succeeded` depending on the end state of its containers).
   3. The kubelet triggers forcible removal of the Pod object from the API server, by setting grace period to 0 (immediate deletion).
   4. The API server deletes the Pod's API object, which is then no longer visible from any client.

### Forced Pod termination

Forced deletions can be potentially disruptive for some workloads and their Pods.

By default, all deletes are graceful within 30 seconds. The `kubectl delete` command supports the `--grace-period=<seconds>` option which allows you to override the default and specify your own value.

Setting the grace period to `0` forcibly and immediately deletes the Pod from the API server. If the Pod was still running on a node, that forcible deletion triggers the kubelet to begin immediate cleanup.

Using kubectl, You must specify an additional flag `--force` along with `--grace-period=0` in order to perform force deletions.

When a force deletion is performed, the API server does not wait for confirmation from the kubelet that the Pod has been terminated on the node it was running on. It removes the Pod in the API immediately so a new Pod can be created with the same name. On the node, Pods that are set to terminate immediately will still be given a small grace period before being force killed.

Immediate deletion does not wait for confirmation that the running resource has been terminated. The resource may continue to run on the cluster indefinitely.

If you need to force-delete Pods that are part of a StatefulSet, refer to the task documentation for deleting Pods from a StatefulSet.

### Garbage collection of Pods

For failed Pods, the API objects remain in the cluster's API until a human or controller process explicitly removes them.

The Pod garbage collector (PodGC), which is a controller in the control plane, cleans up terminated Pods (with a phase of `Succeeded` or `Failed`), when the number of Pods exceeds the configured threshold (determined by `terminated-pod-gc-threshold` in the kube-controller-manager). This avoids a resource leak as Pods are created and terminated over time.

Additionally, PodGC cleans up any Pods which satisfy any of the following conditions:

1. are orphan Pods - bound to a node which no longer exists,
2. are unscheduled terminating Pods,
3. are terminating Pods, bound to a non-ready node tainted with `node.kubernetes.io/out-of-service`.

Along with cleaning up the Pods, PodGC will also mark them as failed if they are in a non-terminal phase. Also, PodGC adds a Pod disruption condition when cleaning up an orphan Pod.
```

</details>

---

## What's needed to unblock

The stage is research-complete but not materialized. Re-running it with `Write` in `--allowed-tools` and `--add-dir ../Book-KCNA` would let it write the six files directly — though note that's the exact config change `CLAUDE.md` records as deliberately reverted on 2026-04-22, so the better fix is probably a small materializer that splits multi-file stage output rather than re-enabling `Write` globally. The five snapshots above are complete and can be written as-is by any means; `research-manifest.md` should receive the manifest section only (everything above "Files to write").
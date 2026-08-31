I have everything needed. Writing the manifest with all snapshots inline.

# Research Manifest — KCNA Chapter 16

**Stage 2, Source Snapshot Research · Book-KCNA · Chapter 16 "Your Application, Their Cluster"**
Curriculum: KCNA effective 2025-11-24 · Domain D3 Cloud Native Application Delivery (16%), competency Debugging · secondary D2.3 Troubleshooting
Fetched 2026-08-31.

**Headline result:** all nine pages the outline listed as blocking (Open Question 2) were retrieved. All five of the chapter's new tools are now documented in the corpus, where before none were. Fourteen snapshots below, thirteen new and one replacing a truncated file.

**Two findings that change drafting decisions**, both detailed in Notes:

1. **The `kubectl debug` profile set is contradicted between two live Kubernetes pages.** The task page lists six profiles and calls `legacy` the default; the generated CLI reference lists five (no `legacy`) and calls `general` the default. Open Question 4 anticipated exactly this. Both are snapshotted verbatim; §3 must not print a single unqualified list.
2. **`debug-statefulset` is a five-sentence stub.** It contains nothing about per-replica PVCs, ordinal triage, or headless DNS. §6 has no dedicated authority and must be built from Ch 6/Ch 11's existing snapshots. This is the chapter's one significant gap.

**Transcription honesty.** Kubernetes docs are CC BY 4.0, which permits verbatim reproduction with attribution, so snapshots were taken from the licensed markdown source in `kubernetes/website`. Fidelity still varied by page. Every snapshot carries a `transcription:` field reading `verbatim` or `near-verbatim`, and every `near-verbatim` file names in its `transcription_note` exactly what was condensed. **Downstream stages must cite `[source:]` only against passages marked `> "..."`**, which are the ones I am confident are exact.

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts | Fidelity |
|---|---|---|---|---|
| `k8s-docs-debug-running-pod-2026-08-31.md` | Kubernetes (CC BY 4.0) | D3.2, D2.3 | kubectl-exec, ephemeral-containers, distroless-image-debugging | verbatim |
| `k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31.md` | Kubernetes | D3.2, D2.3 | debug-copy-to, debug-node, debug-profiles | verbatim |
| `k8s-docs-ephemeral-containers-concept-2026-08-31.md` | Kubernetes | D3.2 | ephemeral-containers, pod-immutability | verbatim |
| `k8s-docs-kubectl-debug-reference-2026-08-31.md` | Kubernetes | D3.2 | debug-profiles, kubectl-debug | near-verbatim |
| `k8s-docs-debug-init-containers-2026-08-31.md` | Kubernetes | D3.2 | init-container-debugging, kubectl-logs-c-init-container | near-verbatim |
| `k8s-docs-debug-service-2026-08-31.md` | Kubernetes | D3.2, D2.3 | service-selector-mismatch, port-versus-targetport, empty-endpointslice-as-symptom, service-dns-name-shape | verbatim |
| `k8s-docs-debug-statefulset-2026-08-31.md` | Kubernetes | D3.2 | statefulset-application-debugging | verbatim |
| `k8s-docs-determine-reason-pod-failure-2026-08-31.md` | Kubernetes | D3.2 | termination-message, config-errors-visible-at-init | near-verbatim |
| `k8s-docs-port-forward-2026-08-31.md` | Kubernetes | D3.2, D2.3 | port-forward-as-diagnostic, service-path-versus-api-path | verbatim |
| `k8s-docs-port-forward-authorization-2026-08-31.md` | Kubernetes | D3.2, D2.3 | service-path-versus-api-path, port-forward-as-diagnostic | verbatim |
| `k8s-docs-local-debugging-telepresence-2026-08-31.md` | Kubernetes | D3.2 | local-development-loop, in-cluster-only-reproduction | near-verbatim |
| `k8s-docs-get-shell-running-container-2026-08-31.md` | Kubernetes | D3.2, D2.3 | kubectl-exec | near-verbatim |
| `k8s-docs-debug-pods-2026-08-31.md` *(replaces existing)* | Kubernetes | D2.3, D3.2 | application-scope-triage, scope-handoff-boundary, empty-endpointslice-as-symptom | near-verbatim |
| `k8s-docs-troubleshooting-applications-index-2026-08-31.md` | Kubernetes | D3.2, D2.3 | application-scope-triage | near-verbatim |

### A1 · `k8s-docs-debug-running-pod-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/"
fetched_at: "2026-08-31T09:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["kubectl-exec", "ephemeral-containers", "distroless-image-debugging", "kubectl-logs-previous"]
transcription: "verbatim"
transcription_note: "Transcribed from the CC BY 4.0 markdown source at kubernetes/website (content/en/docs/tasks/debug/debug-application/debug-running-pod.md, main branch). TRIMMED ON-TOPIC: the long 'Using kubectl describe pod to fetch details' and 'Example: debugging Pending Pods' sections are omitted here — that material is platform-scope and already held by k8s-docs-debug-pods and Ch 13's corpus. Sections A2 of this manifest carries the remainder of the same page."
companion_snapshot: "k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31.md (same source page, later sections)"
---
# Debug Running Pods

> Passages marked `> "..."` are **[VERBATIM]**.

> "This page explains how to debug Pods running (or crashing) on a Node."

## Prerequisites

> "Your Pod should already be scheduled and running. If your Pod is not yet running, start with Debugging Pods."

> "For some of the advanced debugging steps you need to know on which Node the Pod is running and have shell access to run commands on that Node. You don't need that access to run the standard debug steps that use `kubectl`."

## Examining pod logs

> "First, look at the logs of the affected container:"

```shell
kubectl logs ${POD_NAME} -c ${CONTAINER_NAME}
```

> "If your container has previously crashed, you can access the previous container's crash log with:"

```shell
kubectl logs ${POD_NAME} -c ${CONTAINER_NAME} --previous
```

## Debugging with container exec

> "If the container image includes debugging utilities, as is the case with images built from Linux and Windows OS base images, you can run commands inside a specific container with `kubectl exec`:"

```shell
kubectl exec ${POD_NAME} -c ${CONTAINER_NAME} -- ${CMD} ${ARG1} ${ARG2} ... ${ARGN}
```

> "Note: `-c ${CONTAINER_NAME}` is optional. You can omit it for Pods that only contain a single container."

> "As an example, to look at the logs from a running Cassandra pod, you might run"

```shell
kubectl exec cassandra -- cat /var/log/cassandra/system.log
```

> "You can run a shell that's connected to your terminal using the `-i` and `-t` arguments to `kubectl exec`, for example:"

```shell
kubectl exec -it cassandra -- sh
```

> "For more details, see Get a Shell to a Running Container."

## Debugging with an ephemeral debug container

> "Ephemeral containers are useful for interactive troubleshooting when `kubectl exec` is insufficient because a container has crashed or a container image doesn't include debugging utilities, such as with distroless images."

### Example debugging using ephemeral containers

> "You can use the `kubectl debug` command to add ephemeral containers to a running Pod. First, create a pod for the example:"

```shell
kubectl run ephemeral-demo --image=registry.k8s.io/pause:3.1 --restart=Never
```

> "The examples in this section use the `pause` container image because it does not contain debugging utilities, but this method works with all container images."

> "If you attempt to use `kubectl exec` to create a shell you will see an error because there is no shell in this container image."

```shell
kubectl exec -it ephemeral-demo -- sh
```

```
OCI runtime exec failed: exec failed: container_linux.go:346: starting container process caused "exec: \"sh\": executable file not found in $PATH": unknown
```

> "You can instead add a debugging container using `kubectl debug`. If you specify the `-i`/`--interactive` argument, `kubectl` will automatically attach to the console of the Ephemeral Container."

```shell
kubectl debug -it ephemeral-demo --image=busybox:1.28 --target=ephemeral-demo
```

```
Defaulting debug container name to debugger-8xzrl.
If you don't see a command prompt, try pressing enter.
/ #
```

> "This command adds a new busybox container and attaches to it. The `--target` parameter targets the process namespace of another container. It's necessary here because `kubectl run` does not enable process namespace sharing in the pod it creates."

> "Note: The `--target` parameter must be supported by the Container Runtime. When not supported, the Ephemeral Container may not be started, or it may be started with an isolated process namespace so that `ps` does not reveal processes in other containers."

> "You can view the state of the newly created ephemeral container using `kubectl describe`:"

```shell
kubectl describe pod ephemeral-demo
```

```
...
Ephemeral Containers:
  debugger-8xzrl:
    Container ID:   docker://b888f9adfd15bd5739fefaa39e1df4dd3c617b9902082b1cfdc29c4028ffb2eb
    Image:          busybox
    Image ID:       docker-pullable://busybox@sha256:1828edd60c5efd34b2bf5dd3282ec0cc04d47b2ff9caa0b6d4f07a21d1c08084
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 12 Feb 2020 14:25:42 +0100
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:         <none>
...
```

> "Use `kubectl delete` to remove the Pod when you're finished:"

```shell
kubectl delete pod ephemeral-demo
```
```

### A2 · `k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/"
fetched_at: "2026-08-31T09:24:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["debug-copy-to", "debug-node", "debug-profiles", "ephemeral-containers"]
transcription: "verbatim"
transcription_note: "Second half of the same source page as k8s-docs-debug-running-pod-2026-08-31.md, split for citation convenience. Transcribed from the CC BY 4.0 markdown source at kubernetes/website, main branch. Complete from the 'Debugging using a copy of the Pod' heading to end of document; nothing trimmed."
conflict_note: "The static-profile table below lists SIX profiles and names `legacy` as the default. The generated CLI reference (k8s-docs-kubectl-debug-reference-2026-08-31.md) lists FIVE and names `general` as the default. See manifest Notes item 1. Do NOT cite this table as the sole authority for the profile set."
---
# Debug Running Pods — copy, node, and profiles

> All passages below are **[VERBATIM]**.

## Debugging using a copy of the Pod

> "Sometimes Pod configuration options make it difficult to troubleshoot in certain situations. For example, you can't run `kubectl exec` to troubleshoot your container if your container image does not include a shell or if your application crashes on startup. In these situations you can use `kubectl debug` to create a copy of the Pod with configuration values changed to aid debugging."

### Copying a Pod while adding a new container

> "Adding a new container can be useful when your application is running but not behaving as you expect and you'd like to add additional troubleshooting utilities to the Pod."

> "For example, maybe your application's container images are built on `busybox` but you need debugging utilities not included in `busybox`. You can simulate this scenario using `kubectl run`:"

```shell
kubectl run myapp --image=busybox:1.28 --restart=Never -- sleep 1d
```

> "Run this command to create a copy of `myapp` named `myapp-debug` that adds a new Ubuntu container for debugging:"

```shell
kubectl debug myapp -it --image=ubuntu --share-processes --copy-to=myapp-debug
```

```
Defaulting debug container name to debugger-w7xmf.
If you don't see a command prompt, try pressing enter.
root@myapp-debug:/#
```

> "Note:
> * `kubectl debug` automatically generates a container name if you don't choose one using the `--container` flag.
> * The `-i` flag causes `kubectl debug` to attach to the new container by default. You can prevent this by specifying `--attach=false`. If your session becomes disconnected you can reattach using `kubectl attach`.
> * The `--share-processes` allows the containers in this Pod to see processes from the other containers in the Pod. For more information about how this works, see Share Process Namespace between Containers in a Pod."

> "Don't forget to clean up the debugging Pod when you're finished with it:"

```shell
kubectl delete pod myapp myapp-debug
```

### Copying a Pod while changing its command

> "Sometimes it's useful to change the command for a container, for example to add a debugging flag or because the application is crashing."

> "To simulate a crashing application, use `kubectl run` to create a container that immediately exits:"

```
kubectl run --image=busybox:1.28 myapp -- false
```

> "You can see using `kubectl describe pod myapp` that this container is crashing:"

```
Containers:
  myapp:
    Image:         busybox
    ...
    Args:
      false
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       Error
      Exit Code:    1
```

> "You can use `kubectl debug` to create a copy of this Pod with the command changed to an interactive shell:"

```
kubectl debug myapp -it --copy-to=myapp-debug --container=myapp -- sh
```

```
If you don't see a command prompt, try pressing enter.
/ #
```

> "Now you have an interactive shell that you can use to perform tasks like checking filesystem paths or running the container command manually."

> "Note:
> * To change the command of a specific container you must specify its name using `--container` or `kubectl debug` will instead create a new container to run the command you specified.
> * The `-i` flag causes `kubectl debug` to attach to the container by default. You can prevent this by specifying `--attach=false`. If your session becomes disconnected you can reattach using `kubectl attach`."

### Copying a Pod while changing container images

> "In some situations you may want to change a misbehaving Pod from its normal production container images to an image containing a debugging build or additional utilities."

> "As an example, create a Pod using `kubectl run`:"

```
kubectl run myapp --image=busybox:1.28 --restart=Never -- sleep 1d
```

> "Now use `kubectl debug` to make a copy and change its container image to `ubuntu`:"

```
kubectl debug myapp --copy-to=myapp-debug --set-image=*=ubuntu
```

> "The syntax of `--set-image` uses the same `container_name=image` syntax as `kubectl set image`. `*=ubuntu` means change the image of all containers to `ubuntu`."

## Debugging via a shell on the node

> "If none of these approaches work, you can find the Node on which the Pod is running and create a Pod running on the Node. To create an interactive shell on a Node using `kubectl debug`, run:"

```shell
kubectl debug node/mynode -it --image=ubuntu
```

```
Creating debugging pod node-debugger-mynode-pdx84 with container debugger on node mynode.
If you don't see a command prompt, try pressing enter.
root@ek8s:/#
```

> "When creating a debugging session on a node, keep in mind that:
> * `kubectl debug` automatically generates the name of the new Pod based on the name of the Node.
> * The root filesystem of the Node will be mounted at `/host`.
> * The container runs in the host IPC, Network, and PID namespaces, although the pod isn't privileged, so reading some process information may fail, and `chroot /host` may fail.
> * If you need a privileged pod, create it manually or use the `--profile=sysadmin` flag."

> "Don't forget to clean up the debugging Pod when you're finished with it:"

```shell
kubectl delete pod node-debugger-mynode-pdx84
```

## Capturing and analyzing Node/Pod traffic

> "When debugging networking issues, capturing and analyzing network traffic from Nodes/Pods can provide valuable insights into connectivity problems, DNS resolution failures, or unexpected network behavior."

> "You can use `kubectl debug` with the `--profile=sysadmin` flag to run network capture tools on a node."

```shell
kubectl debug --profile=sysadmin node/${NODE_NAME} -it --image=ubuntu:latest
```

> "You can also capture traffic from a specific Pod:"

```shell
kubectl debug --profile=sysadmin pod/${POD_NAME} -n ${NAMESPACE} -it --image=ubuntu:latest
```

## Debugging a Pod or Node while applying a profile

> "When using `kubectl debug` to debug a node via a debugging Pod, a Pod via an ephemeral container, or a copied Pod, you can apply a profile to them. By applying a profile, specific properties such as securityContext are set, allowing for adaptation to various scenarios. There are two types of profiles, static profile and custom profile."

## Applying a Static Profile

> "A static profile is a set of predefined properties, and you can apply them using the `--profile` flag. The available profiles are as follows:"

| Profile | Description |
| ------------ | --------------------------------------------------------------- |
| legacy | A set of properties backwards compatibility with 1.22 behavior |
| general | A reasonable set of generic properties for each debugging journey |
| baseline | A set of properties compatible with PodSecurityStandard baseline policy |
| restricted | A set of properties compatible with PodSecurityStandard restricted policy |
| netadmin | A set of properties including Network Administrator privileges |
| sysadmin | A set of properties including System Administrator (root) privileges |

> "Note: If you don't specify `--profile`, the `legacy` profile is used by default, but it is planned to be deprecated in the near future. So it is recommended to use other profiles such as `general`."

> "Then, debug the Pod using an ephemeral container. If the ephemeral container needs to have privilege, you can use the `sysadmin` profile:"

```shell
kubectl debug -it myapp --image=busybox:1.28 --target=myapp --profile=sysadmin
```

```
Targeting container "myapp". If you don't see processes from this container it may be because the container runtime doesn't support this feature.
Defaulting debug container name to debugger-6kg4x.
If you don't see a command prompt, try pressing enter.
/ #
```

> "This means the container process is granted full capabilities as a privileged container by applying `sysadmin` profile."

## Applying Custom Profile

> "Custom profile is stable as of Kubernetes v1.32."

> "You can define a partial container spec for debugging as a custom profile in either YAML or JSON format, and apply it using the `--custom` flag."

> "Note: Custom profile only supports the modification of the container spec, but modifications to `name`, `image`, `command`, `lifecycle` and `volumeDevices` fields of the container spec are not allowed. It does not support the modification of the Pod spec."

```shell
kubectl debug -it myapp --image=busybox:1.28 --target=myapp --profile=general --custom=custom-profile.yaml
```
```

### A3 · `k8s-docs-ephemeral-containers-concept-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/"
fetched_at: "2026-08-31T09:28:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["ephemeral-containers", "pod-immutability", "distroless-image-debugging"]
transcription: "verbatim"
transcription_note: "Transcribed from the CC BY 4.0 markdown source at kubernetes/website (content/en/docs/concepts/workloads/pods/ephemeral-containers.md, main branch). Complete concept page; only the front-matter block and the 'What's next' link list are trimmed."
resolves: "Open Question 4, second half — the ephemeral-container restriction list. This page pins it; drafting need not write it from memory."
---
# Ephemeral Containers

> All passages below are **[VERBATIM]**.

> "This page provides an overview of ephemeral containers: a special type of container that runs temporarily in an existing Pod to accomplish user-initiated actions such as troubleshooting. You use ephemeral containers to inspect services rather than to build applications."

## Understanding ephemeral containers

> "Pods are the fundamental building block of Kubernetes applications. Since Pods are intended to be disposable and replaceable, you cannot add a container to a Pod once it has been created. Instead, you usually delete and replace Pods in a controlled fashion using deployments."

> "Sometimes it's necessary to inspect the state of an existing Pod, however, for example to troubleshoot a hard-to-reproduce bug. In these cases you can run an ephemeral container in an existing Pod to inspect its state and run arbitrary commands."

### What is an ephemeral container?

> "Ephemeral containers differ from other containers in that they lack guarantees for resources or execution, and they will never be automatically restarted, so they are not appropriate for building applications. Ephemeral containers are described using the same `ContainerSpec` as regular containers, but many fields are incompatible and disallowed for ephemeral containers."

> "- Ephemeral containers may not have ports, so fields such as `ports`, `livenessProbe`, `readinessProbe` are disallowed.
> - Pod resource allocations are immutable, so setting `resources` is disallowed.
> - For a complete list of allowed fields, see the EphemeralContainer reference documentation."

> "Ephemeral containers are created using a special `ephemeralcontainers` handler in the API rather than by adding them directly to `pod.spec`, so it's not possible to add an ephemeral container using `kubectl edit`."

> "Like regular containers, you may not change or remove an ephemeral container after you have added it to a Pod."

> "Note: Ephemeral containers are not supported by static pods."

## Uses for ephemeral containers

> "Ephemeral containers are useful for interactive troubleshooting when `kubectl exec` is insufficient because a container has crashed or a container image doesn't include debugging utilities."

> "In particular, distroless images enable you to deploy minimal container images that reduce attack surface and exposure to bugs and vulnerabilities. Since distroless images do not include a shell or any debugging utilities, it's difficult to troubleshoot distroless images using `kubectl exec` alone."

> "When using ephemeral containers, it's helpful to enable process namespace sharing so you can view processes in other containers."
```

### A4 · `k8s-docs-kubectl-debug-reference-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_debug/"
fetched_at: "2026-08-31T09:47:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), generated CLI reference, CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["debug-profiles", "debug-copy-to", "debug-node", "ephemeral-containers"]
transcription: "near-verbatim"
transcription_note: "PARTIAL / REFORMATTED. The flag list is presented on the source page as a definition list; it is rendered here as a table. Flag DESCRIPTIONS marked `> \"...\"` were re-verified against the live page in a second targeted fetch and are exact. The Description prose is CONDENSED, not verbatim — do not cite it. Examples block is exact."
conflict_note: "AUTHORITATIVE ON PROFILES over the task page. This is the generated reference, produced from the kubectl binary, and it lists FIVE profiles with `general` as default. The task page (k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31.md) lists SIX with `legacy` as default. See manifest Notes item 1."
---
# kubectl debug (generated CLI reference)

## Synopsis

```
kubectl debug (POD | TYPE[[.VERSION].GROUP]/NAME) [ -- COMMAND [args...] ]
```

## Description (CONDENSED — not verbatim, do not cite)

Debug cluster resources using interactive debugging containers. `kubectl debug` automates common debugging tasks for cluster objects, defaulting to Pods when no resource is specified. Behaviour varies by target: for a workload it creates a modified copy of the Pod, or adds an ephemeral debugging container to a running Pod; for a node it launches a new Pod with access to the node's host namespaces and filesystem.

## Examples

```
# Interactive debugging session in pod mypod
kubectl debug mypod -it --image=busybox

# Debug from file
kubectl debug -f pod.yaml -it --image=busybox

# Named debug container with custom image
kubectl debug --image=myproj/debug-tools -c debugger mypod

# Create copy with debug container
kubectl debug mypod -it --image=busybox --copy-to=my-debugger

# Copy with modified container command
kubectl debug mypod -it --copy-to=my-debugger --container=mycontainer -- sh

# Copy with all images changed to busybox
kubectl debug mypod --copy-to=my-debugger --set-image=*=busybox

# Copy with debug container and modified images
kubectl debug mypod -it --copy-to=my-debugger --image=debian --set-image=app=app:debug,sidecar=sidecar:debug

# Node debugging with host access
kubectl debug node/mynode -it --image=busybox
```

## Flags

Descriptions in quotes are **[VERBATIM]**; unquoted ones are condensed.

| Flag | Description |
|------|-------------|
| `--profile string` | > "Options are "general", "baseline", "restricted", "netadmin" or "sysadmin". Defaults to "general"" |
| `--custom string` | > "Path to a JSON or YAML file containing a partial container spec to customize built-in debug profiles." |
| `--target string` | > "When using an ephemeral container, target processes in this container name" |
| `--set-image stringToString` | > "When used with '--copy-to', a list of name=image pairs for changing container images" |
| `--share-processes` | > "When used with '--copy-to', enable process namespace sharing in the copy" (default true) |
| `--replace` | > "When used with '--copy-to', delete the original Pod" |
| `--attach` | > "If true, wait for the container to start running, and then attach as if 'kubectl attach ...' were called" |
| `--copy-to string` | Create a copy of the target Pod with this name |
| `--image string` | Container image to use for the debug container |
| `-c, --container string` | Container name to use for the debug container |
| `-i, --stdin` | Keep stdin open on the container(s) in the pod |
| `-t, --tty` | Allocate a TTY for the debugging container |

## ★ Profile set as given by this page

`general`, `baseline`, `restricted`, `netadmin`, `sysadmin` — five. Default: `general`. **No `legacy` entry.**
```

### A5 · `k8s-docs-debug-init-containers-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-init-containers/"
fetched_at: "2026-08-31T09:31:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["init-container-debugging", "kubectl-logs-c-init-container"]
transcription: "near-verbatim"
transcription_note: "Content complete and faithful; FORMATTING NORMALIZED. The source renders 'Understanding Pod status' as a definition/bullet list and this snapshot renders it as a table. The status STRINGS and their meanings are accurate. Prose sentences marked `> \"...\"` are exact; unquoted connective sentences are lightly condensed. Do not cite unquoted prose."
scope_note: "This page is SHORT and covers only status-reading and log access. It does NOT cover init-container ordering deadlocks, idempotency/re-run hazards, or ConfigMap/Secret mount failures at init. Those parts of Ch 16 section 2 are NOT sourced here — see manifest Gaps item 3."
---
# Debug Init Containers

> "This page shows how to investigate problems related to the execution of Init Containers. The example command lines below refer to the Pod as `<pod-name>` and the Init Containers as `<init-container-1>` and `<init-container-2>`."

## Before you begin

Familiarity with the basics of Init Containers is assumed, and you should have configured an Init Container.

## Checking the status of Init Containers

Display your pod's status:

```shell
kubectl get pod <pod-name>
```

> "For example, a status of `Init:1/2` indicates that one of two Init Containers has completed successfully:"

```
NAME         READY     STATUS     RESTARTS   AGE
<pod-name>   0/1       Init:1/2   0          7s
```

## Getting details about Init Containers

View more detailed information about Init Container execution:

```shell
kubectl describe pod <pod-name>
```

A Pod with two Init Containers might display:

```
Init Containers:
  <init-container-1>:
    Container ID:    ...
    State:           Terminated
      Reason:        Completed
      Exit Code:     0
    Ready:           True
    Restart Count:   0
  <init-container-2>:
    Container ID:    ...
    State:           Waiting
      Reason:        CrashLoopBackOff
    Last State:      Terminated
      Reason:        Error
      Exit Code:     1
    Ready:           False
    Restart Count:   3
```

Init Container statuses can also be accessed programmatically:

```shell
kubectl get pod <pod-name> --template '{{.status.initContainerStatuses}}'
```

## Accessing logs from Init Containers

Pass the Init Container name along with the Pod name to access its logs:

```shell
kubectl logs <pod-name> -c <init-container-2>
```

> "Init Containers that run a shell script print commands as they're executed."

For example, this can be done in Bash by running `set -x` at the beginning of the script.

## Understanding Pod status

A Pod status beginning with `Init:` summarizes the status of Init Container execution.

| Status | Meaning |
|--------|---------|
| `Init:N/M` | The Pod has M Init Containers, and N have completed so far |
| `Init:Error` | An Init Container has failed to execute |
| `Init:CrashLoopBackOff` | An Init Container has failed repeatedly |
| `Pending` | The Pod has not yet begun executing Init Containers |
| `PodInitializing` or `Running` | The Pod has already finished executing Init Containers |
```

### A6 · `k8s-docs-debug-service-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/"
fetched_at: "2026-08-31T09:35:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["service-selector-mismatch", "empty-endpointslice-as-symptom", "port-versus-targetport", "service-dns-name-shape", "kubectl-get-endpointslices", "kubectl-describe-service"]
transcription: "verbatim"
transcription_note: "Transcribed from the CC BY 4.0 markdown source at kubernetes/website (content/en/docs/tasks/debug/debug-application/debug-service.md, main branch). TRIMMED ON-TOPIC: the iptables-save and ipvsadm dumps under 'Is the kube-proxy working?' are omitted — that is platform scope, owned by Ch 9 and Ch 13, and outside Ch 16 section 4. Everything bearing on selectors, ports, DNS and EndpointSlices is complete. A stray Hugo `{{< note >}}` shortcode in the source is preserved as a plain Note line."
---
# Debug Services

> All passages below are **[VERBATIM]**.

## Running commands in a Pod

> "For many steps here you will want to see what a Pod running in the cluster sees. The simplest way is to run an interactive busybox Pod:"

```none
kubectl run -it --rm --restart=Never busybox --image=registry.k8s.io/busybox:1.27.2 sh
```

> "If you already have a running Pod that you prefer to use, you can run a command in it using:"

```shell
kubectl exec <POD-NAME> -c <CONTAINER-NAME> -- <COMMAND>
```

## Setup

> "The label "app" is automatically set by `kubectl create deployment` to the name of the Deployment."

> "The example container used for this walk-through serves its own hostname via HTTP on port 9376, but if you are debugging your own app, you'll want to use whatever port number your Pods are listening on."

> "If you are not getting the responses you expect at this point, your Pods might not be healthy or might not be listening on the port you think they are. You might find `kubectl logs` to be useful for seeing what is happening, or perhaps you need to `kubectl exec` directly into your Pods and debug from there."

## Does the Service exist?

> "The astute reader will have noticed that you did not actually create a Service yet - that is intentional. This is a step that sometimes gets forgotten, and is the first thing to check."

> "What would happen if you tried to access a non-existent Service? If you have another Pod that consumes this Service by name you would get something like:"

```shell
wget -O- hostnames
```
```none
Resolving hostnames (hostnames)... failed: Name or service not known.
wget: unable to resolve host address 'hostnames'
```

> "The first thing to check is whether that Service actually exists:"

```shell
kubectl get svc hostnames
```
```none
No resources found.
Error from server (NotFound): services "hostnames" not found
```

```shell
kubectl expose deployment hostnames --port=80 --target-port=9376
```

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: hostnames
  name: hostnames
spec:
  selector:
    app: hostnames
  ports:
  - name: default
    protocol: TCP
    port: 80
    targetPort: 9376
```

> "In order to highlight the full range of configuration, the Service you created here uses a different port number than the Pods. For many real-world Services, these values might be the same."

## Any Network Policy Ingress rules affecting the target Pods?

> "If you have deployed any Network Policy Ingress rules which may affect incoming traffic to `hostnames-*` Pods, these need to be reviewed."

## Does the Service work by DNS name?

> "One of the most common ways that clients consume a Service is through a DNS name."

> "From a Pod in the same Namespace:"

```shell
nslookup hostnames
```
```none
Address 1: 10.0.0.10 kube-dns.kube-system.svc.cluster.local

Name:      hostnames
Address 1: 10.0.1.175 hostnames.default.svc.cluster.local
```

> "If this fails, perhaps your Pod and Service are in different Namespaces, try a namespace-qualified name (again, from within a Pod):"

```shell
nslookup hostnames.default
```

> "If this works, you'll need to adjust your app to use a cross-namespace name, or run your app and Service in the same Namespace. If this still fails, try a fully-qualified name:"

```shell
nslookup hostnames.default.svc.cluster.local
```

> "Note the suffix here: "default.svc.cluster.local". The "default" is the Namespace you're operating in. The "svc" denotes that this is a Service. The "cluster.local" is your cluster domain, which COULD be different in your own cluster."

> "If you are able to do a fully-qualified name lookup but not a relative one, you need to check that your `/etc/resolv.conf` file in your Pod is correct. From within a Pod:"

```
nameserver 10.0.0.10
search default.svc.cluster.local svc.cluster.local cluster.local example.com
options ndots:5
```

> "The `nameserver` line must indicate your cluster's DNS Service. This is passed into `kubelet` with the `--cluster-dns` flag."

> "The `search` line must include an appropriate suffix for you to find the Service name. In this case it is looking for Services in the local Namespace ("default.svc.cluster.local"), Services in all Namespaces ("svc.cluster.local"), and lastly for names in the cluster ("cluster.local"). Depending on your own install you might have additional records after that (up to 6 total). The cluster suffix is passed into `kubelet` with the `--cluster-domain` flag."

> "The `options` line must set `ndots` high enough that your DNS client library considers search paths at all. Kubernetes sets this to 5 by default, which is high enough to cover all of the DNS names it generates."

### Does any Service work by DNS name?

> "If the above still fails, DNS lookups are not working for your Service. You can take a step back and see what else is not working. The Kubernetes master Service should always work. From within a Pod:"

```shell
nslookup kubernetes.default
```

## Does the Service work by IP?

> "Assuming you have confirmed that DNS works, the next thing to test is whether your Service works by its IP address. From a Pod in your cluster, access the Service's IP (from `kubectl get` above)."

```shell
for i in $(seq 1 3); do 
    wget -qO- 10.0.1.175:80
done
```

> "If your Service is working, you should get correct responses. If not, there are a number of things that could be going wrong. Read on."

## Is the Service defined correctly?

> "It might sound silly, but you should really double and triple check that your Service is correct and matches your Pod's port. Read back your Service and verify it:"

```shell
kubectl get service hostnames -o json
```

> "* Is the Service port you are trying to access listed in `spec.ports[]`?
> * Is the `targetPort` correct for your Pods (some Pods use a different port than the Service)?
> * If you meant to use a numeric port, is it a number (9376) or a string "9376"?
> * If you meant to use a named port, do your Pods expose a port with the same name?
> * Is the port's `protocol` correct for your Pods?"

## Does the Service have any EndpointSlices?

> "If you got this far, you have confirmed that your Service is correctly defined and is resolved by DNS. Now let's check that the Pods you ran are actually being selected by the Service."

> "The `-l app=hostnames` argument is a label selector configured on the Service."

> "The "AGE" column says that these Pods are about an hour old, which implies that they are running fine and not crashing."

> "The "RESTARTS" column says that these pods are not crashing frequently or being restarted. Frequent restarts could lead to intermittent connectivity issues. If the restart count is high, read more about how to debug pods."

> "Inside the Kubernetes system is a control loop which evaluates the selector of every Service and saves the results into one or more EndpointSlice objects."

```shell
kubectl get endpointslices -l kubernetes.io/service-name=hostnames

NAME              ADDRESSTYPE   PORTS   ENDPOINTS
hostnames-ytpni   IPv4          9376    10.244.0.5,10.244.0.6,10.244.0.7
```

> "This confirms that the EndpointSlice controller has found the correct Pods for your Service. If the `ENDPOINTS` column is `<none>`, you should check that the `spec.selector` field of your Service actually selects for `metadata.labels` values on your Pods. A common mistake is to have a typo or other error, such as the Service selecting for `app=hostnames`, but the Deployment specifying `run=hostnames`, as in versions previous to 1.18, where the `kubectl run` command could have been also used to create a Deployment."

## Are the Pods working?

> "At this point, you know that your Service exists and has selected your Pods. At the beginning of this walk-through, you verified the Pods themselves. Let's check again that the Pods are actually working - you can bypass the Service mechanism and go straight to the Pods, as listed by the Endpoints above."

> "Note: These commands use the Pod port (9376), rather than the Service port (80)."

```shell
for ep in 10.244.0.5:9376 10.244.0.6:9376 10.244.0.7:9376; do
    wget -qO- $ep
done
```

> "You expect each Pod in the endpoints list to return its own hostname. If this is not what happens (or whatever the correct behavior is for your own Pods), you should investigate what's happening there."

## Is the kube-proxy working?

> "If you get here, your Service is running, has EndpointSlices, and your Pods are actually serving. At this point, the whole Service proxy mechanism is suspect. Let's confirm it, piece by piece."

> "The default implementation of Services, and the one used on most clusters, is kube-proxy. This is a program that runs on every node and configures one of a small set of mechanisms for providing the Service abstraction. If your cluster does not use kube-proxy, the following sections will not apply, and you will have to investigate whatever implementation of Services you are using."

> "Kube-proxy can run in one of a few modes. In the log listed above, the line `Using iptables Proxier` indicates that kube-proxy is running in "iptables" mode. The most common other mode is "ipvs"."

*(iptables/ipvs verification dumps trimmed — platform scope, out of Ch 16's boundary.)*
```

### A7 · `k8s-docs-debug-statefulset-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-statefulset/"
fetched_at: "2026-08-31T09:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["statefulset-application-debugging"]
transcription: "verbatim"
transcription_note: "COMPLETE. This is the entire page — it really is this short. Nothing was trimmed and nothing is missing."
scope_warning: "THIS PAGE IS A STUB. It contains NO material on per-replica PVC debugging, ordinal-specific triage, headless-Service peer DNS, or any StatefulSet-specific failure mode. Section 6 of Ch 16 CANNOT be sourced from this page beyond the label-selector listing and the Unknown/Terminating pointer. See manifest Gaps item 1 — build section 6 from the existing Ch 6 / Ch 11 snapshots instead."
---
# Debug a StatefulSet

> All passages below are **[VERBATIM]**. This is the complete page.

> "This task shows you how to debug a StatefulSet."

## Before you begin

> "You need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster."

> "You should have a StatefulSet running that you want to investigate."

## Debugging a StatefulSet

> "In order to list all the pods which belong to a StatefulSet, which have a label `app.kubernetes.io/name=MyApp` set on them, you can use the following:"

```shell
kubectl get pods -l app.kubernetes.io/name=MyApp
```

> "If you find that any Pods listed are in `Unknown` or `Terminating` state for an extended period of time, refer to the Deleting StatefulSet Pods task for instructions on how to deal with them."

> "You can debug individual Pods in a StatefulSet using the Debugging Pods guide."

## What's next

> "Learn more about debugging an init-container."
```

### A8 · `k8s-docs-determine-reason-pod-failure-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/determine-reason-pod-failure/"
fetched_at: "2026-08-31T09:32:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["termination-message", "config-errors-visible-at-init", "init-container-debugging"]
transcription: "near-verbatim"
transcription_note: "Prose marked `> \"...\"` is exact. The numbered walk-through steps are lightly condensed connective text — do not cite those. All field names, defaults and numeric limits below were carried through unchanged and are safe to cite."
---
# Determine the Reason for Pod Failure

> "This page shows how to write and read a Container termination message."

> "Termination messages provide a way for containers to write information about fatal events to a location where it can be easily retrieved and surfaced by tools like dashboards and monitoring software. In most cases, information that you put in a termination message should also be written to the general Kubernetes logs."

## Writing and reading a termination message

In this exercise you create a Pod that runs one container, whose manifest specifies a command that runs when the container starts. The container sleeps for 10 seconds and then writes "Sleep expired" to the `/dev/termination-log` file, after which it terminates.

```shell
kubectl apply -f https://k8s.io/examples/debug/termination.yaml
kubectl get pod termination-demo
kubectl get pod termination-demo --output=yaml
```

The output includes the "Sleep expired" message:

```yaml
    lastState:
      terminated:
        containerID: ...
        exitCode: 0
        finishedAt: ...
        message: |
          Sleep expired
```

Use a Go template to filter the output so it includes only the termination message:

```shell
kubectl get pod termination-demo -o go-template="{{range .status.containerStatuses}}{{.lastState.terminated.message}}{{end}}"
```

> "If you are running a multi-container Pod, you can use a Go template to include the container's name. By doing so, you can discover which of the containers is failing:"

```shell
kubectl get pod multi-container-pod -o go-template='{{range .status.containerStatuses}}{{printf "%s:\n%s\n\n" .name .lastState.terminated.message}}{{end}}'
```

## Customizing the termination message

> "Kubernetes retrieves termination messages from the termination message file specified in the `terminationMessagePath` field of a Container, which has a default value of `/dev/termination-log`. By customizing this field, you can tell Kubernetes to use a different file. Kubernetes use the contents from the specified file to populate the Container's status message on both success and failure."

> "The termination message is intended to be brief final status, such as an assertion failure message."

> "The kubelet truncates messages that are longer than 4096 bytes."

> "The total message length across all containers is limited to 12KiB, divided equally among each container. For example, if there are 12 containers (initContainers or containers), each has 1024 bytes of available termination message space."

> "The default termination message path is `/dev/termination-log`. You cannot set the termination message path after a Pod is launched."

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: msg-path-demo
spec:
  containers:
  - name: msg-path-demo-container
    image: debian
    terminationMessagePath: "/tmp/my-log"
```

> "Moreover, users can set the `terminationMessagePolicy` field of a Container for further customization. This field defaults to "File" which means the termination messages are retrieved only from the termination message file. By setting the `terminationMessagePolicy` to "FallbackToLogsOnError", you can tell Kubernetes to use the last chunk of container log output if the termination message file is empty and the container exited with an error. The log output is limited to 2048 bytes or 80 lines, whichever is smaller."
```

### A9 · `k8s-docs-port-forward-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/"
fetched_at: "2026-08-31T09:38:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["port-forward-as-diagnostic", "kubectl-port-forward", "service-path-versus-api-path"]
transcription: "verbatim"
transcription_note: "Transcribed from the CC BY 4.0 markdown source at kubernetes/website. TRIMMED ON-TOPIC: the MongoDB deployment setup steps and mongosh connection walk-through are omitted; the command forms, the TCP-only note, and the Discussion section are complete. Authorization section is carried separately in k8s-docs-port-forward-authorization-2026-08-31.md."
---
# Use Port Forwarding to Access Applications in a Cluster

> All passages below are **[VERBATIM]**.

> "This page shows how to use `kubectl port-forward` to connect to a MongoDB server running in a Kubernetes cluster. This type of connection can be useful for database debugging."

## Forward a local port to a port on the Pod

> "`kubectl port-forward` allows using resource name, such as a pod name, to select a matching pod to port forward to."

```shell
# Change mongo-75f59d57f4-4nd6q to the name of the Pod
kubectl port-forward mongo-75f59d57f4-4nd6q 28015:27017
```

> "which is the same as"

```shell
kubectl port-forward pods/mongo-75f59d57f4-4nd6q 28015:27017
```

> "or"

```shell
kubectl port-forward deployment/mongo 28015:27017
```

> "or"

```shell
kubectl port-forward replicaset/mongo-75f59d57f4 28015:27017
```

> "or"

```shell
kubectl port-forward service/mongo 28015:27017
```

> "Any of the above commands works. The output is similar to this:"

```
Forwarding from 127.0.0.1:28015 -> 27017
Forwarding from [::1]:28015 -> 27017
```

> "`kubectl port-forward` does not return. To continue with the exercises, you will need to open another terminal."

## Note

> "`kubectl port-forward` is implemented for TCP ports only. The support for UDP protocol is tracked in issue 47862."

## Automatic local port selection

The local port may be omitted, letting kubectl choose an available one:

```shell
kubectl port-forward deployment/mongo :27017
```

## Discussion

> "Connections made to local port 28015 are forwarded to port 27017 of the Pod that is running the MongoDB server. With this connection in place, you can use your local workstation to debug the database that is running in the Pod."
```

### A10 · `k8s-docs-port-forward-authorization-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/"
fetched_at: "2026-08-31T09:52:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["service-path-versus-api-path", "port-forward-as-diagnostic"]
transcription: "verbatim"
transcription_note: "The 'Authorization and security considerations' section of the port-forward page, isolated because it is the load-bearing evidence for Ch 16 section 5's claim that port-forward travels the API-server path rather than the Service path. Retrieved by a targeted fetch that was instructed to report NO SUCH SECTION if absent; it returned these three sentences."
significance: "The `pods/portforward` SUBRESOURCE is the authoritative evidence that port-forward is an API-server operation, and 'may bypass network-level controls' is the closest the docs come to stating section 5's inference outright. See manifest Notes item 4 — the full path (API server -> kubelet -> Pod) is still NOT stated on any page found."
---
# Use Port Forwarding to Access Applications in a Cluster — Authorization

> All passages below are **[VERBATIM]**, from the section headed "Authorization and security considerations".

> "Access to `kubectl port-forward` is controlled by Kubernetes authorization mechanisms like Role-Based Access Control (RBAC)."

> "To use `kubectl port-forward`, a user must have permission to access the target resource (for example, a Pod or Service) and the `portforward` subresource. Typical required permissions include `get` on `pods` and `create` on `pods/portforward`."

> "Cluster administrators should carefully restrict these permissions, as port-forwarding can provide direct network access to workloads and may bypass network-level controls."
```

### A11 · `k8s-docs-local-debugging-telepresence-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/local-debugging/"
fetched_at: "2026-08-31T09:44:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["local-development-loop", "in-cluster-only-reproduction"]
transcription: "near-verbatim"
transcription_note: "Passages marked `> \"...\"` are exact. Remaining prose is lightly condensed. The page is short and this snapshot covers all of its sections."
scope_warning: "The page names exactly ONE third-party tool (Telepresence) and is titled after it. It does NOT contain any general discussion of which failures are or are not reproducible locally — that framing, which is Ch 16 section 7's actual subject, is NOT sourced here. See manifest Gaps item 2 and Notes item 5."
---
# Developing and debugging services locally using telepresence

> "Kubernetes applications usually consist of multiple, separate services, each running in its own container. Developing and debugging these services on a remote Kubernetes cluster can be cumbersome, requiring you to get a shell on a running container in order to run debugging tools."

> "`telepresence` is a tool to ease the process of developing and debugging services locally while proxying the service to a remote Kubernetes cluster. Using `telepresence` allows you to use custom tools, such as a debugger and IDE, for a local service and provides the service full access to ConfigMap, secrets, and the services running on the remote cluster."

## Before you begin

* Kubernetes cluster is installed
* `kubectl` is configured to communicate with the cluster
* Telepresence is installed

## Connecting your local machine to a remote Kubernetes cluster

After installing telepresence, run `telepresence connect` to launch its Daemon and connect your local workstation to the cluster.

```
$ telepresence connect

Launching Telepresence Daemon
...
Connected to context default (https://<cluster public IP>)
```

Services can then be reached by their Kubernetes syntax, e.g. `curl -ik https://kubernetes.default`.

## Developing or debugging an existing service

> "Use the `telepresence intercept $SERVICE_NAME --port $LOCAL_PORT:$REMOTE_PORT` command to create an 'intercept' for rerouting remote service traffic."

Where:

- `$SERVICE_NAME` is the name of your local service
- `$LOCAL_PORT` is the port that your service is running on your local workstation
- `$REMOTE_PORT` is the port your service listens to in the cluster

Running this command tells Telepresence to send remote traffic to your local service instead of the service in the remote Kubernetes cluster. Make edits to your service source code locally, save, and see the corresponding changes take effect when accessing your remote application.

## How it works

Telepresence installs a traffic-agent sidecar next to your existing application's container running in the remote cluster. It then captures all traffic requests going into the Pod, and instead of forwarding this to the application in the remote cluster, it routes all traffic to your local development environment. Traffic can be routed in whole (a global intercept) or in part (a personal intercept).
```

### A12 · `k8s-docs-get-shell-running-container-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/"
fetched_at: "2026-08-31T09:49:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["kubectl-exec"]
transcription: "near-verbatim"
transcription_note: "Commands are exact. Prose is CONDENSED throughout except where marked `> \"...\"`. Cite only quoted lines and the command forms."
---
# Get a Shell to a Running Container

> "This page shows how to use `kubectl exec` to get a shell to a running container."

## Getting a shell to a container

Create a Pod running one container (nginx), then get a shell to it:

```shell
kubectl apply -f https://k8s.io/examples/application/shell-demo.yaml
kubectl get pod shell-demo
kubectl exec --stdin --tty shell-demo -- /bin/bash
```

> "The double dash (`--`) separates the arguments you want to pass to the command from the kubectl arguments."

Inside the shell you can explore the filesystem and install diagnostic tools:

```shell
ls /
cat /proc/mounts
cat /proc/1/maps
apt-get update
apt-get install -y tcpdump
apt-get install -y lsof
apt-get install -y procps
ps aux
```

## Running individual commands in a container

Commands can be run without an interactive shell:

```shell
kubectl exec shell-demo -- env
kubectl exec shell-demo -- ps aux
kubectl exec shell-demo -- ls /
kubectl exec shell-demo -- cat /proc/1/mounts
```

## Opening a shell when a Pod has more than one container

> "If a Pod has more than one container, use `--container` or `-c` to specify a container in the `kubectl exec` command."

```shell
kubectl exec -i -t my-pod --container main-app -- /bin/bash
```

> "The short options `-i` and `-t` are the same as the long options `--stdin` and `--tty`."
```

### A13 · `k8s-docs-debug-pods-2026-08-31.md` (replaces existing)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/"
fetched_at: "2026-08-31T09:41:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3", "D3.2"]
concepts_covered: ["application-scope-triage", "scope-handoff-boundary", "empty-endpointslice-as-symptom", "service-selector-mismatch", "port-versus-targetport"]
transcription: "near-verbatim"
transcription_note: "Passages marked `> \"...\"` are exact. Bullet bodies and connective prose are CONDENSED. Cite only quoted text."
supersedes: "Replaces the 2026-08-31 snapshot of the same URL, which stopped three sentences in at 'take a look at it'. The section 'My pod is running but not doing what I told it to do' — required by Ch 16 sections 1 and 3 and named as blocking in the outline's Open Question 2 — is now present. k8s-docs-debug-pods-2026-08-23.md remains on disk and is unaffected."
---
# Debug Pods

> "This guide is to help users debug applications that are deployed into Kubernetes and not behaving correctly. This is *not* a guide for people who want to debug their cluster."

## Diagnosing the problem

> "The first step in troubleshooting is triage. What is the problem? Is it your Pods, your Replication Controller or your Service?"

* Debugging Pods
* Debugging Replication Controllers
* Debugging Services

## Debugging Pods

> "The first step in debugging a Pod is taking a look at it. Check the current state of the Pod and recent events with the following command:"

```shell
kubectl describe pods ${POD_NAME}
```

Look at the state of the containers in the pod, and whether they are all `Running`. Check for recent restarts.

### My pod stays pending

A Pod stuck in `Pending` could not be scheduled onto a node. The `kubectl describe` output should carry scheduler messages explaining why. Common reasons:

* **Insufficient resources** — CPU or Memory capacity is exhausted. Delete Pods, adjust resource requests, or add nodes.
* **Using hostPort** — binding a Pod to a `hostPort` limits where it can be scheduled. > "In most cases, `hostPort` is unnecessary" and a Service object is preferable. The number of Pods cannot exceed the number of nodes.

### My pod stays waiting

A Pod stuck in `Waiting` has been scheduled to a worker node but cannot run there. > "The most common cause of `Waiting` pods is a failure to pull the image." Check three things: the image name is correct; the image has been pushed to the registry; the image can be pulled manually.

### My pod stays terminating

A Pod stuck in `Terminating` was requested for deletion but the control plane cannot remove it, typically because a finalizer exists and an admission webhook prevents its removal. Check whether a ValidatingWebhookConfiguration or MutatingWebhookConfiguration targets `UPDATE` operations for `pods`.

### My pod is crashing or otherwise unhealthy

Once your Pod has been scheduled, use the methods in Debug Running Pods for further investigation.

### My pod is running but not doing what I told it to do

> "If your pod is not behaving as you expected, it may be that there was an error in your pod description (e.g. `mypod.yaml` file on your local machine), and that the error was silently ignored when you created the pod."

> "Often a section of the pod description is nested incorrectly, or a key name is typed incorrectly, and so the key is ignored."

Delete your Pod and try creating it again with validation:

```shell
kubectl apply --validate -f mypod.yaml
```

A typo such as `commnd` for `command` produces:

```shell
I0805 10:43:25.129850   46757 schema.go:126] unknown field: commnd
I0805 10:43:25.129973   46757 schema.go:129] this may be a false alarm
pods/mypod
```

Next, check whether the Pod on the API server matches what you intended:

```shell
kubectl get pods/mypod -o yaml > mypod-on-apiserver.yaml
```

Manually compare the original file with the one from the API server. The API server version will normally have extra lines, which is expected. But if lines present in your original are **absent** from the API server version, that may indicate a problem with your Pod spec.

## Debugging Replication Controllers

Replication controllers either create Pods or they don't. If they aren't creating Pods, use the Pod instructions above. Review events with:

```shell
kubectl describe rc ${CONTROLLER_NAME}
```

## Debugging Services

Services provide load balancing across a set of Pods. First verify that a Service has endpoints:

```shell
kubectl get endpointslices -l kubernetes.io/service-name=${SERVICE_NAME}
```

Check that the endpoints match the number and identity of Pods you expect. For example, a Service for an nginx Deployment with 3 replicas should show three distinct IP addresses.

### My service is missing endpoints

List the Pods matching the Service's selector labels:

```shell
kubectl get pods --selector=name=nginx,type=frontend
```

Verify the list matches the Pods you expect, and that each Pod's `containerPort` matches the Service's `targetPort`.

### Network traffic is not forwarded

See the Debug Services document for further verification: that the Service runs, has Endpoints, that Pods serve correctly, that DNS resolves, that iptables rules exist, and that kube-proxy behaves normally.
```

### A14 · `k8s-docs-troubleshooting-applications-index-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/"
fetched_at: "2026-08-31T09:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["application-scope-triage"]
transcription: "near-verbatim"
transcription_note: "Index page, condensed. Value is that it enumerates the canonical application-scope debugging set, which is the boundary Ch 16 section 1 restates from the application side."
---
# Troubleshooting Applications

This section of the Kubernetes documentation covers debugging containerized applications. It addresses common problems with Kubernetes resources such as Pods, Services and StatefulSets, explains how to interpret container termination messages, and describes techniques for debugging running containers.

The pages grouped under Troubleshooting Applications are:

* Debug Pods
* Debug Services
* Debug a StatefulSet
* Determine the Reason for Pod Failure
* Debug Init Containers
* Debug Running Pods
* Get a Shell to a Running Container
```

## Gaps

Flagged clearly so the drafting stage does **not** invent facts to fill them.

### 1. `debug-statefulset` is a stub — §6 has no dedicated authority ⚠ **most significant**

The official StatefulSet debugging page is five sentences (snapshot A7 is the whole page). It contains **nothing** on the three things §6 is built from: per-replica PVC debugging, ordinal-specific triage, or headless-Service peer DNS failures. There is no other official "debug StatefulSets" page.

**This is not fatal, and it happens to align with §6's own guardrail.** §6 was already told it owns only "the consequences for a person holding a bug report," with ordinal identity owned by Ch 6 §6, `volumeClaimTemplates` by Ch 11 §6, and headless Services by Ch 9 §5. Those three are already sourced on disk: `k8s-docs-statefulset-2026-08-24.md`, `k8s-docs-statefulset-storage-2026-08-25.md`, `k8s-docs-dns-pod-service-2026-08-23.md`.

**Instruction to drafting:** build §6 by *retrieving* the shipped Ch 6 / Ch 11 / Ch 9 facts and adding the diagnostic turn. Cite the existing snapshots for the mechanics, and A7 only for the two things it actually says: the `-l app.kubernetes.io/name=` listing, and the `Unknown`/`Terminating` pointer. Do **not** attribute PVC-survival or peer-DNS claims to the debug-statefulset page.

### 2. §7's actual subject — what is *not* reproducible locally — is unsourced

The `local-debugging` page (A11) is titled after Telepresence and describes that one tool. It contains **no** general treatment of the dividing line §7 is built on: that anything depending on cluster-supplied identity, DNS, injected config, admission mutation, or Service routing is not locally reproducible. That framing is an authored synthesis, defensible but not quotable.

**Instruction to drafting:** §7's dividing line must be presented as the book's own reasoning, not as a sourced claim. It is well-founded — each of those five dependencies is documented elsewhere in the corpus — but no `[source:]` tag may be attached to the dividing line itself. The *pattern* (proxy a local process into the cluster so it sees real dependencies) **is** sourced: A11's "provides the service full access to ConfigMap, secrets, and the services running on the remote cluster."

### 3. §2's ordering and idempotency hazards are not on the init-container debugging page

`debug-init-containers` (A5) covers status strings and `kubectl logs -c` only. It says nothing about init containers that deadlock waiting on a dependency, init containers that cannot survive a re-run, or ConfigMap/Secret mount failures surfacing at init.

Partial coverage exists elsewhere on disk: `k8s-docs-init-containers-2026-08-24.md` is the concept page and does carry the re-run/idempotency requirement and the ordering semantics. **Check it before drafting §2** — I did not re-fetch it, and it is the correct citation target for those two hazards. The *config-error-at-init* case remains the least-sourced of the three.

### 4. "An empty endpoint list has two causes" is an authored synthesis, not a single-source claim

This is a Fixed Point in §4 and an Exam Alert item, so it matters. No single page states "two causes."

- **Cause 1 (selector mismatch)** is stated outright in A6: *"If the `ENDPOINTS` column is `<none>`, you should check that the `spec.selector` field of your Service actually selects for `metadata.labels` values on your Pods."*
- **Cause 2 (not Ready)** is stated in the existing `k8s-docs-endpointslices-2026-08-24.md`: the `ready` condition *"maps to the Pod's `Ready` condition,"* and service proxies use `ready`/`serving` endpoints.

Both halves are solidly sourced; the *pairing* and the *exhaustiveness* ("two, and only two") are the book's own. Tag each cause to its own snapshot and do not tag the count.

### 5. No CNCF sub-competency weights exist

Confirmed again against `cncf-kcna-curriculum-pdf-2026-08-23.md`, which publishes four domain weights only: `16% – Cloud Native Application Delivery: Application Delivery; Debugging`. There is **no** published weight for Debugging alone. The frontmatter's `domain_weight_pct: 4` is the book's authored allocation — this restates B1 gap G33 and B2 disclosure #1. The in-chapter metadata line must carry **16%** for D3 with the authored-allocation disclaimer, exactly as the outline's exam_domain note directs.

### 6. The "four triage questions" frame is authored

The docs' own triage is *"Is it your Pods, your Replication Controller or your Service?"* (A13) — three resource kinds, not four diagnostic questions. §1's *is it running / healthy / reachable / configured* is the book's structure. Legitimate and good pedagogy; simply not sourceable. Do not `[source:]` it.

### 7. The full port-forward request path is not documented

A10 gets §5 most of the way: the `pods/portforward` **subresource** proves this is an API-server operation, and *"may bypass network-level controls"* is close to §5's inference. But no page found states the chain *client → API server → kubelet → Pod* explicitly. §5 may assert the API-server hop on the subresource evidence; the **kubelet** hop is an inference and should be phrased as one, or checked against `k8s-docs-cluster-architecture-2026-08-23.md` before it is asserted flatly.

## Notes for the author

### 1. ⚠ Source conflict: the `kubectl debug` profile set — Open Question 4 confirmed

Two live pages in the same repository disagree, and this lands directly on a §3 Fixed Point.

| | Task page (A2) | Generated CLI reference (A4) |
|---|---|---|
| Profiles | `legacy`, `general`, `baseline`, `restricted`, `netadmin`, `sysadmin` — **six** | `general`, `baseline`, `restricted`, `netadmin`, `sysadmin` — **five** |
| Default | `legacy`, *"planned to be deprecated in the near future"* | `general` |

The reference page is generated from the kubectl binary, so it reflects the current release; the task page's prose has not been updated to match. I verified the reference figures with a second targeted fetch against the live page — five profiles, default `general` — so this is not a transcription artifact.

**Recommendation, matching the outline's own OQ4 fallback:** §3 should name the five profiles both pages agree on, state that the default is `general` on current kubectl, and describe the shape (profiles set `securityContext` properties to fit a scenario) rather than presenting the set as fixed. If `legacy` is mentioned at all, mention it as a deprecated compatibility profile — do not print a six-item list as current. Tag the count to A4, not A2. This is the same treatment Ch 13 gave the event TTL.

### 2. Open Question 5 (`kubectl debug node/`) — the sources support the "in" recommendation

A2 documents `kubectl debug node/mynode` fully, and its own bullets make the boundary crossing explicit: the node's root filesystem is mounted at `/host`, and the container runs in the host IPC, Network and PID namespaces. That is a clean, sourced way to write the paragraph as *the moment you step back across the line* rather than as an exception to §1's boundary. The page also notes the pod is **not** privileged by default and that `chroot /host` may fail without `--profile=sysadmin` — a good, concrete detail if one line can be spared.

### 3. Open Question 3 (§7 depth) — the source makes this decision easy

A11 names exactly one tool, Telepresence, and the page is titled after it. That is precisely the outline's recommendation: name the pattern, name at most one tool, source-tagged. There is no toolchain on the page to be tempted by. **The recommendation should be adopted as written.** Note the page is Kubernetes documentation about a third-party tool, so tag it as `[source: k8s-docs-local-debugging-telepresence-2026-08-31]` and let the *pattern* carry the weight, since the tool may churn.

### 4. A useful find for §3 that the outline did not anticipate

A13's *"My pod is running but not doing what I told it to do"* section is a better fit for §3's "is it configured" half than expected. Its argument is exactly §3's: the manifest you wrote and the object the API server holds can differ silently, so **compare them** — `kubectl get pods/mypod -o yaml` diffed against your local file, with *lines present in your original but absent from the API server version* as the tell. That is a sourced, mechanical version of "the value the process actually got is frequently not the value the manifest appears to set," and it pairs naturally with exec-ing in to read the value. Recommend §3 use it.

### 5. §3's distroless argument is fully sourced, and better than expected

Three independent passages support it. A3 gives the causal chain outright — Pods are disposable, *"you cannot add a container to a Pod once it has been created,"* therefore ephemeral containers. A3 also gives the security framing: distroless images *"reduce attack surface"* and consequently *"do not include a shell or any debugging utilities."* A1 gives the reproducible demonstration, including the literal `exec: "sh": executable file not found in $PATH` error. §3's Fixed Point ("You cannot add a container to a running Pod. That is why ephemeral containers exist.") is quotable almost verbatim from A3.

Likewise the ephemeral-container restriction list is now pinned and can be written without hedging: no ports, no `livenessProbe`/`readinessProbe`, no `resources`, *"lack guarantees for resources or execution,"* *"will never be automatically restarted,"* and *"you may not change or remove an ephemeral container after you have added it to a Pod."* One bonus for the Ch 13 tie-in: *"Ephemeral containers are not supported by static pods."*

### 6. `--copy-to` — the docs support the Fixed Point framing but never state it

A2 shows `--copy-to` three ways and never once says "the original Pod is untouched." The nearest support is indirect: every example ends with `kubectl delete pod myapp myapp-debug` — deleting **both**, which only makes sense if both exist — and `--replace` is documented as a separate opt-in flag meaning *"delete the original Pod."* The existence of `--replace` is the strongest available evidence that non-replacement is the default.

**Recommendation:** teach `--copy-to` as the outline directs, but source the claim on `--replace` rather than on a nonexistent sentence. Phrasing like "the copy is a copy — deleting the original is a separate flag, `--replace`" is both accurate and citable.

### 7. Terminology drift worth catching at drafting

The debug-service page heading is now **"Does the Service have any EndpointSlices?"** — not "Endpoints." But the body text still says *"as listed by the Endpoints above"* and the `kubectl get endpointslices` output column is still headed `ENDPOINTS`. Shipped Ch 9 uses EndpointSlice. Keep §4 on EndpointSlice, and be aware the column name in any transcribed output is `ENDPOINTS` — a reader comparing the two will notice, and one clause heading that off is cheap.

Two smaller ones: A13 still has a **"Debugging Replication Controllers"** section, which is legacy and should not be surfaced; and A6's selector-typo example is dated to *"versions previous to 1.18"* — the underlying mistake (Service selects `app=`, Deployment sets `run=`) is still the right teaching example, but do not carry the version clause into the book.

### 8. Glossary queue — one addition confirmed

The outline's OQ8 queues **distroless** for the glossary. A3 supplies a usable definition in the source's own words: minimal images that *"reduce attack surface and exposure to bugs and vulnerabilities"* and *"do not include a shell or any debugging utilities."* Cite A3 when the glossary entry is built. **ephemeral container** likewise has a clean sourced definition in A3's first line.

### 9. Transcription fidelity — read before assigning `[source:]` tags

Kubernetes docs are CC BY 4.0 and permit verbatim reproduction with attribution, so snapshots were taken from the licensed markdown source in `kubernetes/website` (`main`) rather than the rendered site. Fidelity still came back uneven. Snapshots A1, A2, A3, A6, A7, A9 and A10 are **verbatim** and are the safe citation targets — notably, these include all of §3's, §4's and §5's load-bearing material. A4, A5, A8, A11, A12, A13 and A14 are **near-verbatim**; each names in its own `transcription_note` exactly what was condensed. In every file, only passages marked `> "..."` should carry a `[source:]` tag. Where a downstream audit needs a claim that sits in unquoted prose in a near-verbatim file, re-fetch that page rather than citing it.
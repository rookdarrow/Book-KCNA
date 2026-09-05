---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched as the raw CC BY 4.0 markdown source from kubernetes/website, main branch (content/en/docs/tasks/debug/debug-application/debug-running-pod.md)"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["ephemeral-containers", "debug-target", "distroless-image-debugging", "debug-node", "debug-profiles"]
---

# Debug Running Pods — ephemeral containers, node shell, and profiles

> Supersedes the truncated `k8s-docs-debug-running-pod-2026-08-31.md` and `k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31.md` for the passages below. All passages are verbatim from the markdown source; Hugo shortcodes are dropped.

## Debugging with an ephemeral debug container

"Ephemeral containers are useful for interactive troubleshooting when `kubectl exec` is insufficient because a container has crashed or a container image doesn't include debugging utilities, such as with distroless images."

"You can use the `kubectl debug` command to add ephemeral containers to a running Pod."

"If you attempt to use `kubectl exec` to create a shell you will see an error because there is no shell in this container image."

```shell
kubectl exec -it ephemeral-demo -- sh
```

```
OCI runtime exec failed: exec failed: container_linux.go:346: starting container process caused "exec: \"sh\": executable file not found in $PATH": unknown
```

"You can instead add a debugging container using `kubectl debug`. If you specify the `-i`/`--interactive` argument, `kubectl` will automatically attach to the console of the Ephemeral Container."

```shell
kubectl debug -it ephemeral-demo --image=busybox:1.28 --target=ephemeral-demo
```

"This command adds a new busybox container and attaches to it. The `--target` parameter targets the process namespace of another container. It's necessary here because `kubectl run` does not enable process namespace sharing in the pod it creates."

Note: "The `--target` parameter must be supported by the Container Runtime. When not supported, the Ephemeral Container may not be started, or it may be started with an isolated process namespace so that `ps` does not reveal processes in other containers."

## Debugging via a shell on the node

"If none of these approaches work, you can find the Node on which the Pod is running and create a Pod running on the Node. To create an interactive shell on a Node using `kubectl debug`, run:"

```shell
kubectl debug node/mynode -it --image=ubuntu
```

"When creating a debugging session on a node, keep in mind that:"

- "`kubectl debug` automatically generates the name of the new Pod based on the name of the Node."
- "The root filesystem of the Node will be mounted at `/host`."
- "The container runs in the host IPC, Network, and PID namespaces, although the pod isn't privileged, so reading some process information may fail, and `chroot /host` may fail."
- "If you need a privileged pod, create it manually or use the `--profile=sysadmin` flag."

"Don't forget to clean up the debugging Pod when you're finished with it:"

## Debugging a Pod or Node while applying a profile

"When using `kubectl debug` to debug a node via a debugging Pod, a Pod via an ephemeral container, or a copied Pod, you can apply a profile to them. By applying a profile, specific properties such as securityContext are set, allowing for adaptation to various scenarios. There are two types of profiles, static profile and custom profile."

### Applying a Static Profile

"A static profile is a set of predefined properties, and you can apply them using the `--profile` flag. The available profiles are as follows:"

| Profile | Description |
|---|---|
| legacy | "A set of properties backwards compatibility with 1.22 behavior" |
| general | "A reasonable set of generic properties for each debugging journey" |
| baseline | "A set of properties compatible with PodSecurityStandard baseline policy" |
| restricted | "A set of properties compatible with PodSecurityStandard restricted policy" |
| netadmin | "A set of properties including Network Administrator privileges" |
| sysadmin | "A set of properties including System Administrator (root) privileges" |

Note: "If you don't specify `--profile`, the `legacy` profile is used by default, but it is planned to be deprecated in the near future. So it is recommended to use other profiles such as `general`."

> Conflict: the generated CLI reference (`k8s-docs-kubectl-debug-reference-2026-09-04.md`) lists five profiles without `legacy` and names `general` as the default. The two pages disagree; the default is release-dependent.

"If the ephemeral container needs to have privilege, you can use the `sysadmin` profile:"

```shell
kubectl debug -it myapp --image=busybox:1.28 --target=myapp --profile=sysadmin
```

"This means the container process is granted full capabilities as a privileged container by applying `sysadmin` profile."

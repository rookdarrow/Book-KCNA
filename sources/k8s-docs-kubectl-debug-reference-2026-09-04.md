---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_debug/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), generated CLI reference (auto-generated from the kubectl Go source), CC BY 4.0 — fetched as the raw markdown source from kubernetes/website, main branch (content/en/docs/reference/kubectl/generated/kubectl_debug/_index.md)"
objectives_covered: ["D3.2"]
concepts_covered: ["debug-profiles", "debug-copy-to", "debug-node", "ephemeral-containers", "debug-target", "debug-keep-labels"]
---

# kubectl debug (generated CLI reference)

> Supersedes `k8s-docs-kubectl-debug-reference-2026-08-31.md`, whose body was truncated at the page's first code fence and carries no flag table. Synopsis prose and flag descriptions below are verbatim; the flag table is rendered on the page as HTML table rows and is reproduced here as name + quoted description.

## Synopsis

"Debug cluster resources using interactive debugging containers."

"'debug' provides automation for common debugging tasks for cluster objects identified by resource and name. Pods will be used by default if no resource is specified."

"The action taken by 'debug' varies depending on what resource is specified. Supported actions include:"

- "Workload: Create a copy of an existing pod with certain attributes changed, for example changing the image tag to a new version."
- "Workload: Add an ephemeral container to an already running pod, for example to add debugging utilities without restarting the pod."
- "Node: Create a new pod that runs in the node's host namespaces and can access the node's filesystem."

"Note: When a non-root user is configured for the entire target Pod, some capabilities granted by debug profile may not work."

```
kubectl debug (POD | TYPE[[.VERSION].GROUP]/NAME) [ -- COMMAND [args...] ]
```

## Examples (excerpt, verbatim)

```
  # Create an interactive debugging session in pod mypod and immediately attach to it.
  kubectl debug mypod -it --image=busybox

  # Create a copy of mypod adding a debug container and attach to it
  kubectl debug mypod -it --image=busybox --copy-to=my-debugger

  # Create a copy of mypod changing the command of mycontainer
  kubectl debug mypod -it --copy-to=my-debugger --container=mycontainer -- sh

  # Create an interactive debugging session on a node and immediately attach to it.
  # The container will run in the host namespaces and the host's filesystem will be mounted at /host
```

## Options (selected flags, descriptions verbatim)

- `--copy-to string` — "Create a copy of the target Pod with this name."
- `--keep-annotations` — "If true, keep the original pod annotations.(This flag only works when used with '--copy-to')"
- `--keep-init-containers` (Default: true) — "Run the init containers for the pod. Defaults to true.(This flag only works when used with '--copy-to')"
- `--keep-labels` — "If true, keep the original pod labels.(This flag only works when used with '--copy-to')"
- `--keep-liveness` — "If true, keep the original pod liveness probes.(This flag only works when used with '--copy-to')"
- `--keep-readiness` — "If true, keep the original pod readiness probes.(This flag only works when used with '--copy-to')"
- `--keep-startup` — "If true, keep the original startup probes.(This flag only works when used with '--copy-to')"
- `--profile string` (Default: "general") — "Options are "general", "baseline", "restricted", "netadmin" or "sysadmin". Defaults to "general""
- `--replace` — "When used with '--copy-to', delete the original Pod."
- `--same-node` — "When used with '--copy-to', schedule the copy of target Pod on the same node."
- `--set-image stringToString` — "When used with '--copy-to', a list of name=image pairs for changing container images, similar to how 'kubectl set image' works."
- `--share-processes` (Default: true) — "When used with '--copy-to', enable process namespace sharing in the copy."
- `--target string` — "When using an ephemeral container, target processes in this container name."

## Conflict note

The generated reference lists FIVE profiles with `general` as the default. The task page *Debug Running Pods* (`k8s-docs-debug-running-pod-2026-09-04.md`) lists SIX, including `legacy`, and says `legacy` is used when `--profile` is omitted "but it is planned to be deprecated in the near future." The generated reference is produced from the kubectl binary and reflects the current release; the task page describes older behavior. The default is release-dependent and should not be taught as a fixed fact.

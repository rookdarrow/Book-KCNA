---
source_url: "https://kubernetes.io/docs/reference/kubectl/quick-reference/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/kubectl/quick-reference.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["kubectl-config-current-context", "kubectl-get-events-sort-by", "kubectl-logs", "kubectl-logs-previous", "kubectl-logs-all-containers", "kubectl-describe", "kubectl-top", "kubectl-get-pod-o-wide"]
closes_gap: "k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31 is transcribed only as far as its first heading and holds no command lines. This snapshot carries the troubleshooting-relevant command lines verbatim, with their trailing comments, so Chapter 13 sec.3's command blocks can be tagged."
---

# kubectl Quick Reference — troubleshooting subset

> All command lines and their trailing `#` comments below are **[VERBATIM]**, grouped under the page's own `##` headings.

## `## Kubectl context and configuration`

```
kubectl config current-context                       # display the current-context
```

## `## Viewing and finding resources`

```
kubectl get pods -o wide                      # List all pods in the current namespace, with more details
kubectl describe pods my-pod
kubectl get events --sort-by=.metadata.creationTimestamp
```

## `## Interacting with running Pods`

```
kubectl logs my-pod                                 # dump pod logs (stdout)
kubectl logs -l name=myLabel                        # dump pod logs, with label name=myLabel (stdout)
kubectl logs my-pod --previous                      # dump pod logs (stdout) for a previous instantiation of a container
kubectl logs my-pod -c my-container                 # dump pod container logs (stdout, multi-container case)
kubectl logs -l name=myLabel -c my-container        # dump pod container logs, with label name=myLabel (stdout)
kubectl logs my-pod -c my-container --previous      # dump pod container logs (stdout, multi-container case) for a previous instantiation of a container
kubectl logs -f my-pod                              # stream pod logs (stdout)
kubectl logs -f my-pod -c my-container              # stream pod container logs (stdout, multi-container case)
kubectl logs -f -l name=myLabel --all-containers    # stream all pods logs with label name=myLabel (stdout)
kubectl top pod                                     # Show metrics for all pods in the default namespace
kubectl top pod POD_NAME --containers               # Show metrics for a given pod and its containers
kubectl top pod POD_NAME --sort-by=cpu              # Show metrics for a given pod and sort it by 'cpu' or 'memory'
```

## `## Interacting with Deployments and Services`

```
kubectl logs deploy/my-deployment                         # dump Pod logs for a Deployment (single-container case)
kubectl logs deploy/my-deployment -c my-container         # dump Pod logs for a Deployment (multi-container case)
```

## `## Interacting with Nodes and cluster`

```
kubectl top node                                                      # Show metrics for all nodes
kubectl top node my-node                                              # Show metrics for a given node
```

## What this supports

- `kubectl config current-context` prints the active context — the "which cluster am I talking to" check.
- `kubectl get events --sort-by=.metadata.creationTimestamp` is the project's own recipe for reading a namespace's events in creation order.
- `--previous` reads "a previous instantiation of a container"; `-c` names the container in "the multi-container case"; `--all-containers` reads all containers at once.
- `kubectl logs deploy/<name>` reads a Pod's logs on the Deployment's behalf — the Deployment itself has no logs.

---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-init-containers/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched as the raw CC BY 4.0 markdown source from kubernetes/website, main branch (content/en/docs/tasks/debug/debug-application/debug-init-containers.md)"
objectives_covered: ["D3.2"]
concepts_covered: ["init-container-debugging", "kubectl-logs-c-init-container", "init-status-vocabulary", "kubectl-describe-init-containers"]
---

# Debug Init Containers

> Supersedes `k8s-docs-debug-init-containers-2026-08-31.md`, whose body was truncated at the page's first code fence and carries none of the passages below. All passages here are verbatim from the markdown source.

## Checking the status of Init Containers

"Display the status of your pod:"

```shell
kubectl get pod <pod-name>
```

"For example, a status of `Init:1/2` indicates that one of two Init Containers has completed successfully:"

```
NAME         READY     STATUS     RESTARTS   AGE
<pod-name>   0/1       Init:1/2   0          7s
```

## Getting details about Init Containers

"View more detailed information about Init Container execution:"

```shell
kubectl describe pod <pod-name>
```

"For example, a Pod with two Init Containers might show the following:"

```
Init Containers:
  <init-container-1>:
    Container ID:    ...
    ...
    State:           Terminated
      Reason:        Completed
      Exit Code:     0
      Started:       ...
      Finished:      ...
    Ready:           True
    Restart Count:   0
    ...
  <init-container-2>:
    Container ID:    ...
    ...
    State:           Waiting
      Reason:        CrashLoopBackOff
    Last State:      Terminated
      Reason:        Error
      Exit Code:     1
      Started:       ...
      Finished:      ...
    Ready:           False
    Restart Count:   3
    ...
```

"You can also access the Init Container statuses programmatically by reading the `status.initContainerStatuses` field on the Pod Spec:"

```shell
kubectl get pod <pod-name> --template '{{.status.initContainerStatuses}}'
```

## Accessing logs from Init Containers

"Pass the Init Container name along with the Pod name to access its logs."

```shell
kubectl logs <pod-name> -c <init-container-2>
```

"Init Containers that run a shell script print commands as they're executed. For example, you can do this in Bash by running `set -x` at the beginning of the script."

## Understanding Pod status

"A Pod status beginning with `Init:` summarizes the status of Init Container execution. The table below describes some example status values that you might see while debugging Init Containers."

| Status | Meaning |
|---|---|
| `Init:N/M` | "The Pod has `M` Init Containers, and `N` have completed so far." |
| `Init:Error` | "An Init Container has failed to execute." |
| `Init:CrashLoopBackOff` | "An Init Container has failed repeatedly." |
| `Pending` | "The Pod has not yet begun executing Init Containers." |
| `PodInitializing` or `Running` | "The Pod has already finished executing Init Containers." |

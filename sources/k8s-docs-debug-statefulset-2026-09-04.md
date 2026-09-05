---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-statefulset/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched as the raw CC BY 4.0 markdown source from kubernetes/website, main branch (content/en/docs/tasks/debug/debug-application/debug-statefulset.md)"
objectives_covered: ["D3.2"]
concepts_covered: ["statefulset-application-debugging", "statefulset-unknown-terminating-pods"]
---

# Debug a StatefulSet

> Supersedes `k8s-docs-debug-statefulset-2026-08-31.md`, whose body was truncated at the page's first code fence and lost the `Unknown`/`Terminating` paragraph. This is the complete page; it really is this short. All passages verbatim.

"This task shows you how to debug a StatefulSet."

## Before you begin

- "You need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster."
- "You should have a StatefulSet running that you want to investigate."

## Debugging a StatefulSet

"In order to list all the pods which belong to a StatefulSet, which have a label `app.kubernetes.io/name=MyApp` set on them, you can use the following:"

```shell
kubectl get pods -l app.kubernetes.io/name=MyApp
```

"If you find that any Pods listed are in `Unknown` or `Terminating` state for an extended period of time, refer to the Deleting StatefulSet Pods task for instructions on how to deal with them. You can debug individual Pods in a StatefulSet using the Debugging Pods guide."

## What's next

"Learn more about debugging an init-container."

---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["rollout", "rollout-history", "rollback", "pause-rollout", "resume-rollout", "kubectl-rollout-status", "kubectl-rollout-history", "kubectl-rollout-undo", "kubectl-rollout-pause", "kubectl-rollout-resume"]
---
# kubectl rollout (kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

## Synopsis

Manage the rollout of a resource.

Manage the rollout of one or many resources.

Valid resource types include:

- deployments
- daemonsets
- statefulsets

## Subcommands

| Command | Description |
|---|---|
| `kubectl rollout history` | View rollout history |
| `kubectl rollout pause` | Mark the provided resource as paused |
| `kubectl rollout restart` | Restart a resource |
| `kubectl rollout resume` | Resume a paused resource |
| `kubectl rollout status` | Show the status of the rollout |
| `kubectl rollout undo` | Undo a previous rollout |

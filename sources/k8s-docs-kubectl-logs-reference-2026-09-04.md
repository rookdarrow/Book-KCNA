---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_logs/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/kubectl/generated/kubectl_logs/_index.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — the generated kubectl logs command reference"
objectives_covered: ["D2.3"]
concepts_covered: ["kubectl-logs", "kubectl-logs-previous", "kubectl-logs-all-containers", "kubectl-logs-container-flag"]
closes_gap: "Chapter 13 sec.3 prints the -c, --all-containers and --previous flags; the cached logging-architecture snapshot describes -c and --previous in prose but --all-containers appeared in no snapshot. This reference carries all three flag descriptions verbatim."
---

# kubectl logs — command reference

> All passages below are **[VERBATIM]**.

## Synopsis

"Print the logs for a container in a pod or specified resource. If the pod has only one container, the container name is optional."

```
kubectl logs [-f] [-p] (POD | TYPE/NAME) [-c CONTAINER]
```

## Examples

```
  # Return snapshot logs from pod nginx with multi containers
  kubectl logs nginx --all-containers=true

  # Return snapshot logs from all containers in pods defined by label app=nginx
  kubectl logs -l app=nginx --all-containers=true

  # Return snapshot of previous terminated ruby container logs from pod web-1
  kubectl logs -p -c ruby web-1

  # Begin streaming the logs of the ruby container in pod web-1
  kubectl logs -f -c ruby web-1
```

## Flags

- `--all-containers` — "Get all containers' logs in the pod(s)."
- `-c, --container string` — "Print the logs of this container"
- `-p, --previous` — "If true, print the logs for the previous instance of the container in a pod if it exists."
- `--since duration` — "Only return logs newer than a relative duration like 5s, 2m, or 3h. Defaults to all logs. Only one of since-time / since may be used."

## What this supports

- `--previous` is the flag that reads the container instance that already terminated ("previous terminated ruby container logs"); it is optional in the sense that it prints those logs only "if it exists".
- `-c` selects one container; `--all-containers` selects every container in the Pod(s) — a selection across containers, not across time.
- The container name may be omitted only for a single-container Pod, which is the documented basis for saying that a bare `kubectl logs` on a multi-container Pod is an incomplete request.

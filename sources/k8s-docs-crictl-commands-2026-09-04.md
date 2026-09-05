---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/crictl/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/debug/debug-cluster/crictl.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["crictl", "crictl-ps", "crictl-logs", "crictl-pods"]
closes_gap: "k8s-docs-crictl-2026-08-31 declares crictl-ps and crictl-logs in its frontmatter but its transcription stops before the 'Example crictl commands' section, so the two command lines Chapter 13 sec.5 prints were unverifiable. This snapshot carries those examples verbatim."
---

# Debugging Kubernetes nodes with crictl — the example commands

> All passages below are **[VERBATIM]**.

## Overview

Feature state: `{{< feature-state for_k8s_version="v1.11" state="stable" >}}` — rendered on the page as "FEATURE STATE: Kubernetes v1.11 [stable]".

"`crictl` is a command-line interface for CRI-compatible container runtimes. You can use it to inspect and debug container runtimes and applications on a Kubernetes node. `crictl` and its source are hosted in the cri-tools repository."

"`crictl` requires a Linux operating system with a CRI runtime."

## `## Example crictl commands`

"The following examples show some `crictl` commands and example output."

### `### List pods`

"List all pods:"

```
crictl pods
```

"The output is similar to this:"

```
POD ID              CREATED              STATE               NAME                         NAMESPACE           ATTEMPT
926f1b5a1d33a       About a minute ago   Ready               sh-84d7dcf559-4r2gq          default             0
4dccb216c4adb       About a minute ago   Ready               nginx-65899c769f-wv2gp       default             0
a86316e96fa89       17 hours ago         Ready               kube-proxy-gblk4             kube-system         0
919630b8f81f1       17 hours ago         Ready               nvidia-device-plugin-zgbbv   kube-system         0
```

### `### List containers`

"List all containers:"

```
crictl ps -a
```

"List running containers:"

```
crictl ps
```

"The output is similar to this:"

```
CONTAINER ID        IMAGE                                                                                                             CREATED             STATE               NAME                       ATTEMPT
1f73f2d81bf98       busybox@sha256:141c253bc4c3fd0a201d32dc1f493bcf3fff003b6df416dea4f41046e0f37d47                                   6 minutes ago       Running             sh                         1
87d3992f84f74       nginx@sha256:d0a8828cccb73397acb0073bf34f4d7d8aa315263f1e7806bf8c55d8ac139d5f                                     7 minutes ago       Running             nginx                      0
1941fb4da154f       k8s-gcrio.azureedge.net/hyperkube-amd64@sha256:00d814b1f7763f4ab5be80c58e98140dfc69df107f253d7fdd714b30a714260a   17 hours ago        Running             kube-proxy                 0
```

### `### Get a container's logs`

"Get all container logs:"

```
crictl logs 87d3992f84f74
```

"Get only the latest `N` lines of logs:"

```
crictl logs --tail=1 87d3992f84f74
```

## What this supports

- `crictl ps` lists **containers** (one row per container, with a NAME and an ATTEMPT count); `crictl pods` lists Pod sandboxes. The two are different tables, which is the counting distinction Chapter 13 Practice Q13 turns on.
- `crictl logs <container id>` reads a container's logs from the runtime directly, by container ID rather than by Pod name.
- The page also documents `crictl exec`, `crictl pods --name` and `crictl pods --label`; Chapter 13 deliberately teaches only `ps` and `logs`.

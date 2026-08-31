---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/crictl/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["crictl", "crictl-ps", "crictl-pods", "crictl-logs", "crictl-inspect"]
closes_gap: "crictl had NO snapshot in the corpus. Ch 3 line 451 pinned the 'why a node-level tool exists' framing to Ch 13 sec.5."
depth_note: "Outline Open Question 5 recommends naming crictl, showing `crictl ps` and `crictl logs`, and spending words on the layer argument rather than the command surface. This snapshot carries more surface than the chapter should use -- that is deliberate, so the drafting stage chooses from sourced material rather than inventing."
---
# Debugging Kubernetes nodes with crictl

> All passages below are **[VERBATIM]**.

> Feature state: Stable since Kubernetes v1.11

> "`crictl` is a command-line interface for CRI-compatible container runtimes. You can use it to inspect and debug container runtimes and applications on a Kubernetes node. `crictl` and its source are hosted in the cri-tools repository."

## Before you begin

> "`crictl` requires a Linux operating system with a CRI runtime."

## Installing crictl

> "You can download a compressed archive `crictl` from the cri-tools release page, for several different architectures. Download the version that corresponds to your version of Kubernetes. Extract it and move it to a location on your system path, such as `/usr/local/bin/`."

## General usage

> "The `crictl` command has several subcommands and runtime flags. Use `crictl help` or `crictl <subcommand> help` for more details."

> "You can set the endpoint for `crictl` by doing one of the following:
> - Set the `--runtime-endpoint` and `--image-endpoint` flags.
> - Set the `CONTAINER_RUNTIME_ENDPOINT` and `IMAGE_SERVICE_ENDPOINT` environment variables.
> - Set the endpoint in the configuration file `/etc/crictl.yaml`."

> Note: "If you don't set an endpoint, `crictl` attempts to connect to a list of known endpoints, which might result in an impact to performance."

> "To view or edit the current configuration, view or edit the contents of `/etc/crictl.yaml`. For example, the configuration when using the `containerd` container runtime would be similar to this:"

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

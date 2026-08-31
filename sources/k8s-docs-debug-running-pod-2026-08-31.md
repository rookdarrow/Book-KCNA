---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/"
fetched_at: "2026-08-31T09:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["kubectl-exec", "ephemeral-containers", "distroless-image-debugging", "kubectl-logs-previous"]
transcription: "verbatim"
transcription_note: "Transcribed from the CC BY 4.0 markdown source at kubernetes/website (content/en/docs/tasks/debug/debug-application/debug-running-pod.md, main branch). TRIMMED ON-TOPIC: the long 'Using kubectl describe pod to fetch details' and 'Example: debugging Pending Pods' sections are omitted here — that material is platform-scope and already held by k8s-docs-debug-pods and Ch 13's corpus. Sections A2 of this manifest carries the remainder of the same page."
companion_snapshot: "k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31.md (same source page, later sections)"
---
# Debug Running Pods

> Passages marked `> "..."` are **[VERBATIM]**.

> "This page explains how to debug Pods running (or crashing) on a Node."

## Prerequisites

> "Your Pod should already be scheduled and running. If your Pod is not yet running, start with Debugging Pods."

> "For some of the advanced debugging steps you need to know on which Node the Pod is running and have shell access to run commands on that Node. You don't need that access to run the standard debug steps that use `kubectl`."

## Examining pod logs

> "First, look at the logs of the affected container:"

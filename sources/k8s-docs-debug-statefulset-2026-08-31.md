---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-statefulset/"
fetched_at: "2026-08-31T09:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["statefulset-application-debugging"]
transcription: "verbatim"
transcription_note: "COMPLETE. This is the entire page — it really is this short. Nothing was trimmed and nothing is missing."
scope_warning: "THIS PAGE IS A STUB. It contains NO material on per-replica PVC debugging, ordinal-specific triage, headless-Service peer DNS, or any StatefulSet-specific failure mode. Section 6 of Ch 16 CANNOT be sourced from this page beyond the label-selector listing and the Unknown/Terminating pointer. See manifest Gaps item 1 — build section 6 from the existing Ch 6 / Ch 11 snapshots instead."
---
# Debug a StatefulSet

> All passages below are **[VERBATIM]**. This is the complete page.

> "This task shows you how to debug a StatefulSet."

## Before you begin

> "You need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster."

> "You should have a StatefulSet running that you want to investigate."

## Debugging a StatefulSet

> "In order to list all the pods which belong to a StatefulSet, which have a label `app.kubernetes.io/name=MyApp` set on them, you can use the following:"

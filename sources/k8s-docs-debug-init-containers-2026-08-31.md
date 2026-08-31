---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-init-containers/"
fetched_at: "2026-08-31T09:31:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["init-container-debugging", "kubectl-logs-c-init-container"]
transcription: "near-verbatim"
transcription_note: "Content complete and faithful; FORMATTING NORMALIZED. The source renders 'Understanding Pod status' as a definition/bullet list and this snapshot renders it as a table. The status STRINGS and their meanings are accurate. Prose sentences marked `> \"...\"` are exact; unquoted connective sentences are lightly condensed. Do not cite unquoted prose."
scope_note: "This page is SHORT and covers only status-reading and log access. It does NOT cover init-container ordering deadlocks, idempotency/re-run hazards, or ConfigMap/Secret mount failures at init. Those parts of Ch 16 section 2 are NOT sourced here — see manifest Gaps item 3."
---
# Debug Init Containers

> "This page shows how to investigate problems related to the execution of Init Containers. The example command lines below refer to the Pod as `<pod-name>` and the Init Containers as `<init-container-1>` and `<init-container-2>`."

## Before you begin

Familiarity with the basics of Init Containers is assumed, and you should have configured an Init Container.

## Checking the status of Init Containers

Display your pod's status:

---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/"
fetched_at: "2026-08-31T13:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["triage-flow", "pending-diagnosis", "imagepullbackoff-diagnosis", "kubectl-describe", "platform-scope-vs-application-scope"]
supersedes_note: "Fuller transcription than k8s-docs-debug-pods-2026-08-23.md, which omitted the scope disclaimer, the triage list, and the 'My pod stays terminating' section. The 08-23 file remains valid; cite this one for sec.1 and sec.2."
---
# Debug Pods

> All passages below are **[VERBATIM]**.

> "This guide is to help users debug applications that are deployed into Kubernetes and not behaving correctly. This is *not* a guide for people who want to debug their cluster. For that you should check out this guide."

## Diagnosing the problem

> "The first step in troubleshooting is triage. What is the problem? Is it your Pods, your Replication Controller or your Service?"

## Debugging Pods

> "The first step in debugging a Pod is taking a look at it. Check the current state of the Pod and recent events with the following command:"

---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/"
fetched_at: "2026-08-31T09:41:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3", "D3.2"]
concepts_covered: ["application-scope-triage", "scope-handoff-boundary", "empty-endpointslice-as-symptom", "service-selector-mismatch", "port-versus-targetport"]
transcription: "near-verbatim"
transcription_note: "Passages marked `> \"...\"` are exact. Bullet bodies and connective prose are CONDENSED. Cite only quoted text."
supersedes: "Replaces the 2026-08-31 snapshot of the same URL, which stopped three sentences in at 'take a look at it'. The section 'My pod is running but not doing what I told it to do' — required by Ch 16 sections 1 and 3 and named as blocking in the outline's Open Question 2 — is now present. k8s-docs-debug-pods-2026-08-23.md remains on disk and is unaffected."
---
# Debug Pods

> "This guide is to help users debug applications that are deployed into Kubernetes and not behaving correctly. This is *not* a guide for people who want to debug their cluster."

## Diagnosing the problem

> "The first step in troubleshooting is triage. What is the problem? Is it your Pods, your Replication Controller or your Service?"

* Debugging Pods
* Debugging Replication Controllers
* Debugging Services

## Debugging Pods

> "The first step in debugging a Pod is taking a look at it. Check the current state of the Pod and recent events with the following command:"

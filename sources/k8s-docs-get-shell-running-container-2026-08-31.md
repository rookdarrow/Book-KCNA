---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/"
fetched_at: "2026-08-31T09:49:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["kubectl-exec"]
transcription: "near-verbatim"
transcription_note: "Commands are exact. Prose is CONDENSED throughout except where marked `> \"...\"`. Cite only quoted lines and the command forms."
---
# Get a Shell to a Running Container

> "This page shows how to use `kubectl exec` to get a shell to a running container."

## Getting a shell to a container

Create a Pod running one container (nginx), then get a shell to it:

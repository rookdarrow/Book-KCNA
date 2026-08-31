---
source_url: "https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/"
fetched_at: "2026-08-31T09:38:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["port-forward-as-diagnostic", "kubectl-port-forward", "service-path-versus-api-path"]
transcription: "verbatim"
transcription_note: "Transcribed from the CC BY 4.0 markdown source at kubernetes/website. TRIMMED ON-TOPIC: the MongoDB deployment setup steps and mongosh connection walk-through are omitted; the command forms, the TCP-only note, and the Discussion section are complete. Authorization section is carried separately in k8s-docs-port-forward-authorization-2026-08-31.md."
---
# Use Port Forwarding to Access Applications in a Cluster

> All passages below are **[VERBATIM]**.

> "This page shows how to use `kubectl port-forward` to connect to a MongoDB server running in a Kubernetes cluster. This type of connection can be useful for database debugging."

## Forward a local port to a port on the Pod

> "`kubectl port-forward` allows using resource name, such as a pod name, to select a matching pod to port forward to."

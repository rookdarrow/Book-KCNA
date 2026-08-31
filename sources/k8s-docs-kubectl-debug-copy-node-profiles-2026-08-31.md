---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/"
fetched_at: "2026-08-31T09:24:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["debug-copy-to", "debug-node", "debug-profiles", "ephemeral-containers"]
transcription: "verbatim"
transcription_note: "Second half of the same source page as k8s-docs-debug-running-pod-2026-08-31.md, split for citation convenience. Transcribed from the CC BY 4.0 markdown source at kubernetes/website, main branch. Complete from the 'Debugging using a copy of the Pod' heading to end of document; nothing trimmed."
conflict_note: "The static-profile table below lists SIX profiles and names `legacy` as the default. The generated CLI reference (k8s-docs-kubectl-debug-reference-2026-08-31.md) lists FIVE and names `general` as the default. See manifest Notes item 1. Do NOT cite this table as the sole authority for the profile set."
---
# Debug Running Pods — copy, node, and profiles

> All passages below are **[VERBATIM]**.

## Debugging using a copy of the Pod

> "Sometimes Pod configuration options make it difficult to troubleshoot in certain situations. For example, you can't run `kubectl exec` to troubleshoot your container if your container image does not include a shell or if your application crashes on startup. In these situations you can use `kubectl debug` to create a copy of the Pod with configuration values changed to aid debugging."

### Copying a Pod while adding a new container

> "Adding a new container can be useful when your application is running but not behaving as you expect and you'd like to add additional troubleshooting utilities to the Pod."

> "For example, maybe your application's container images are built on `busybox` but you need debugging utilities not included in `busybox`. You can simulate this scenario using `kubectl run`:"

---
source_url: "https://fluxcd.io/flux/components/kustomize/kustomizations/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux-controller-set", "continuously-reconciled-principle", "delivery-agent-identity", "drift-detection"]
---
# Flux — Kustomization API reference

## What it defines
"The `Kustomization` API defines a pipeline for fetching, decrypting, building, validating and applying Kustomize overlays or plain Kubernetes manifests."

## Interval
"`.spec.interval` is a required field that specifies the interval at which the Kustomization is reconciled, i.e. the controller fetches the source with the Kubernetes manifests, builds the Kustomization and applies it on the cluster, correcting any existing drift in the process. The minimum value should be 60 seconds."

CAPTURE NOTE: the API reference states no default for `.spec.interval` — only that
it is required and has a 60-second minimum. The "every five minutes by default"
figure comes from the concepts page and describes Flux's bootstrap-generated
Kustomization, not an API-level default.

## Prune
"`.spec.prune` is a required boolean field to enable/disable garbage collection for a Kustomization. Garbage collection means that the Kubernetes objects that were previously applied on the cluster but are missing from the current source revision, are removed from the cluster automatically."

## Service account impersonation
"`.spec.serviceAccountName` is an optional field used to specify the ServiceAccount to be impersonated while reconciling the Kustomization."

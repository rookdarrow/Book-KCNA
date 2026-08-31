---
source_url: "https://fluxcd.io/flux/components/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux-controller-set", "manifest-source", "flux"]
---
# Flux — GitOps Toolkit components (controllers and their custom resources)

## Source Controller
Custom resources: GitRepository, OCIRepository, HelmRepository, HelmChart, Bucket, ExternalArtifact, ArtifactGenerator.

## Kustomize Controller
Custom resource: Kustomization.

## Helm Controller
Custom resource: HelmRelease.

## Notification Controller
Custom resources: Provider, Alert, Receiver.

## Image Reflector and Image Automation Controllers
Custom resources: ImageRepository, ImagePolicy, ImageUpdateAutomation.

CAPTURE NOTE: this index page carries only the controller names, their linked
documentation titles ("The GitOps Toolkit <X> Controller documentation") and the
CRD lists reproduced above. Per-controller prose lives on the linked sub-pages and
was not captured. Do not attribute behavioural claims to this snapshot.

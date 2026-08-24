---
source_url: "https://fluxcd.io/flux/concepts/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3 Application Delivery"]
concepts_covered: ["flux", "gitops-toolkit", "sources", "reconciliation", "kustomization-cr", "bootstrap", "flux-controllers"]
---
# Flux — Core concepts (fluxcd.io/flux/concepts/)

Flux is a GitOps Toolkit: a set of composable APIs and specialized tools that can be used to build Continuous Delivery on top of Kubernetes. GitOps is a way of managing your infrastructure and applications so that whole system is described declaratively and version controlled, and having an automated process that ensures that the deployed environment matches the state specified in one or more Git repositories.

**Sources** — a source defines the origin of a repository containing the desired state of the system and the requirements to obtain it (e.g. credentials, version selectors). Sources produce an artifact that is consumed by other Flux components to perform actions, such as applying the contents of the artifact on the cluster. Examples: GitRepository, OCIRepository, HelmRepository, Bucket.

**Reconciliation** — ensuring that a given state (e.g. application running in the cluster, infrastructure) matches a desired state declaratively defined somewhere (e.g. a Git repository). The Kustomization resource reconciles Kubernetes resources from a source into the cluster (every five minutes by default); changes made with kubectl are reverted unless reconciliation is suspended or the change is pushed to the repository.

**Bootstrap** — installing Flux components in a GitOps manner: the manifests are applied, GitRepository and Kustomization objects are created for Flux itself, and the manifests are pushed to a Git repository so Flux manages itself like any other resource.

**Controllers** — Source Controller, Kustomize Controller, Helm Controller, Notification Controller, Image Automation Controllers.

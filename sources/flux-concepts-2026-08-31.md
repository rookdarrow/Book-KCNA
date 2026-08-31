---
source_url: "https://fluxcd.io/flux/concepts/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux", "flux-controller-set", "flux-bootstrap", "continuously-reconciled-principle", "drift-detection", "manifest-source"]
---
# Flux — Core concepts (2026-08-31 capture)

## GitOps Toolkit
"In Flux, GitOps Toolkit refers to a collection of specialized tools, Flux Controllers, composable APIs, and reusable Go packages available under the fluxcd GitHub organization."

## Sources
"A Source defines the origin of a repository containing the desired state of the system and the requirements to obtain it (e.g. credentials, version selectors)."

## Reconciliation
"Reconciliation refers to ensuring that a given state (e.g. application running in the cluster, infrastructure) matches a desired state declaratively defined somewhere (e.g. a Git repository)."

"The reconciliation runs every five minutes by default, but this can be changed with `.spec.interval`."

"If you make any changes to the cluster using `kubectl edit/patch/delete`, they will be promptly reverted."

## Bootstrap
"The process of installing the Flux components in a GitOps manner is called a bootstrap. The manifests are applied to the cluster, a `GitRepository` and `Kustomization` are created for the Flux components, then the manifests are pushed to an existing Git repository (or a new one is created)."

CAPTURE NOTE: the GitOps Toolkit definition differs from the 2026-08-23 capture,
which read "Flux is a GitOps Toolkit: a set of composable APIs and specialized
tools." Both captures are retained. Cite this one for the current wording.

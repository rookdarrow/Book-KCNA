---
source_url: "https://fluxcd.io/flux/guides/repository-structure/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Flux project (CNCF graduated) — guide, Ways of structuring your repositories; text taken from the project's website source (fluxcd/website, content/en/flux/guides/repository-structure.md)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux", "multi-cluster-delivery", "source-of-truth"]
---
# Flux — Ways of structuring your repositories (monorepo section)

The example structure shows `apps`, `infrastructure`, and `clusters` directories, with `clusters/production` and `clusters/staging` beneath the last.

"Each cluster state is defined in a dedicated dir e.g. `clusters/production` where the specific apps and infrastructure overlays are referenced."

"The separation between apps and infrastructure makes it possible to define the order in which a cluster is reconciled, e.g. first the cluster addons and other Kubernetes controllers, then the applications."

CAPTURE NOTE: the guide describes per-cluster directories within one repository. It does not describe any mechanism by which one cluster's Flux reconciles another cluster.

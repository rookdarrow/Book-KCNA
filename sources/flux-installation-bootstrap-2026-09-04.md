---
source_url: "https://fluxcd.io/flux/installation/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Flux project (CNCF graduated) — installation documentation; text taken from the project's website source (fluxcd/website, content/en/flux/installation/_index.md)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux", "flux-bootstrap", "multi-cluster-delivery", "pulled-automatically-principle"]
---
# Flux — Installation: bootstrap

"The recommended way of installing Flux on Kubernetes clusters is by using the bootstrap procedure."

## Bootstrap with Flux CLI
"The `flux bootstrap` command deploys the Flux controllers on Kubernetes cluster(s) and configures the controllers to sync the cluster(s) state from a Git repository. Besides installing the controllers, the bootstrap command pushes the Flux manifests to the Git repository and configures Flux to update itself from Git."

"If the Flux controllers are present on the cluster, the bootstrap command will perform an upgrade if needed. Bootstrap is idempotent, it's safe to run the command as many times as you want."

"After running the bootstrap command, any operation on the cluster(s) (including Flux upgrades) can be done via Git push, without the need to connect to the Kubernetes API."

CAPTURE NOTE: the page describes bootstrap per cluster ("cluster(s)") and says nothing about one Flux installation holding credentials to, or reconciling, a cluster other than the one it runs in.

---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/tracking_strategies/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["tracking-branch-tag-commit", "versioned-and-immutable-principle", "source-of-truth"]
---
# Argo CD — Tracking and Deployment Strategies

"An Argo CD application spec provides several different ways of tracking Kubernetes resource manifests."

## Branch or symbolic reference
"If a branch name or a symbolic reference (like HEAD) is specified, Argo CD will continually compare live state against the resource manifests defined at the tip of the specified branch or the resolved commit of the symbolic reference."

## Tag
"If a tag is specified, the manifests at the specified Git tag will be used to perform the sync comparison."

Tags are "generally considered more stable, and less frequently updated" than branches.

## Pinned commit
"If a Git commit SHA is specified, the app is effectively pinned to the manifests defined at the specified commit."

"Since commit SHAs cannot change meaning, the only way to change the live state of an app which is pinned to a commit, is by updating the tracking revision in the application to a different commit containing the new manifests."

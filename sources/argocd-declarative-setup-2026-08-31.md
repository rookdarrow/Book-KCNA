---
source_url: "https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["argo-cd-application-resource", "source-of-truth", "manifest-source", "tracking-branch-tag-commit", "multi-cluster-delivery", "delivery-agent-identity"]
---
# Argo CD — Declarative Setup (Applications, Projects, Clusters)

## Applications
"The Application CRD is the Kubernetes resource object representing a deployed application instance in an environment."

It is defined by two key pieces of information: a "source reference to the desired state in Git (repository, revision, path, environment)" and a "destination reference to the target cluster and namespace."

A minimal Application manifest:

---
source_url: "https://argo-cd.readthedocs.io/en/stable/operator-manual/security/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["delivery-agent-identity", "blast-radius", "pull-based-delivery", "argo-cd"]
---
# Argo CD — Security (cluster credentials and RBAC)

## Where cluster credentials live
"To manage external clusters, Argo CD stores the credentials of the external cluster as a Kubernetes Secret in the argocd namespace."

Those credentials comprise "the K8s API bearer token associated with the `argocd-manager` ServiceAccount created during `argocd cluster add`, along with connection options to that API server."

## Default permissions
"By default, Argo CD uses a clusteradmin level role in order to:
1. watch & operate on cluster state
2. deploy resources to the cluster"

## Reducing permissions
"Although Argo CD requires cluster-wide read privileges to resources in the managed cluster to function properly, it does not necessarily need full write privileges to the cluster."

Operators may edit the ClusterRole of `argocd-manager-role` "such that write privileges are limited to only the namespaces and resources that you wish Argo CD to manage."

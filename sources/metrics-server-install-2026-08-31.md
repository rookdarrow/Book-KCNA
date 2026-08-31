---
source_url: "https://kubernetes-sigs.github.io/metrics-server/"
fetched_at: "2026-08-31T06:20:00-0400"
authority: "Kubernetes SIGs (kubernetes-sigs/metrics-server), the reference implementation of the Metrics API"
objectives_covered: ["D3.1", "D2.3"]
concepts_covered: ["metrics-server", "components-yaml", "kubectl-apply-f", "aggregation-layer", "declarative-install", "metrics-api"]
---
# metrics-server — how it is installed (kubernetes-sigs.github.io/metrics-server/)

> **Snapshot note.** Fetched 2026-08-31 to close Chapter 14's G-14d, which asked whether
> metrics-server's *composition* could be sourced. **It cannot, from this page.** The page does
> not enumerate the objects inside `components.yaml` — no Deployment, Service, ClusterRole,
> ServiceAccount or APIService is named. What it does state is the installation *shape*, which
> is the fact Chapter 14 actually argues from: installation is `kubectl apply -f` against a file
> of objects somebody else wrote.
>
> **Do not use this snapshot to support an object-by-object enumeration.** Ch 14's earlier
> "a Deployment, a Service, RBAC rules, an APIService registration" phrasing is NOT supported
> here and was narrowed at the 2026-08-31 integration gate. Closing `components.yaml` itself
> would require caching a release artifact, which is a heavier and more perishable citation than
> this chapter needs.

## Installation

> "Latest Metrics Server release can be installed by running:"

```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

A Helm chart is referenced as an alternative install path; the page gives no object
specifications for it either.

## What it is, and what it requires

> "Metrics Server collects resource metrics from Kubelets and exposes them in Kubernetes
> apiserver through Metrics API"

> "kube-apiserver must enable an aggregation layer"

## Not on this page

The individual objects contained in `components.yaml` are not described. The page covers
requirements, use cases and configuration guidance rather than deployment composition.

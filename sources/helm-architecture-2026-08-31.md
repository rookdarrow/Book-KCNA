---
source_url: "https://helm.sh/docs/topics/architecture/"
fetched_at: "2026-08-31T04:29:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm", "chart", "chart-repository", "helm-release"]
---
# Helm — Architecture (helm.sh/docs/topics/architecture/)

Helm is the package manager for Kubernetes.

Three components describe how Helm works: charts, repositories, and releases.

A release is an instance of a chart running in a Kubernetes cluster.

The Helm client handles local chart development, manages repositories, manages releases, and sends charts to the Helm library to be installed, upgraded, or uninstalled.

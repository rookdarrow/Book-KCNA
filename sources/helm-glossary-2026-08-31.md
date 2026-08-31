---
source_url: "https://helm.sh/docs/glossary/"
fetched_at: "2026-08-31T04:29:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart", "chart-yaml", "helm-release", "helm-release-revision", "chart-repository", "chart-version-versus-appversion"]
---
# Helm — Glossary (helm.sh/docs/glossary/)

**Chart** — A Helm package that contains information sufficient for installing a set of Kubernetes resources into a Kubernetes cluster.

**Chart Archive** — A *chart archive* is a tarred and gzipped (and optionally signed) chart.

**Chart Version** — Charts are versioned according to the SemVer 2 spec. A version number is required on every chart.

**Chart.yaml** — Information about a chart is stored in a special file called `Chart.yaml`. Every chart must have this file.

**Kube Config (KUBECONFIG)** — The Helm client learns about Kubernetes clusters by using files in the *Kube config* file format. By default, Helm attempts to find this file in the place where `kubectl` creates it (`$HOME/.kube/config`).

**Lint (Linting)** — To *lint* a chart is to validate that it follows the conventions and requirements of the Helm chart standard.

**Release** — When a chart is installed, the Helm library creates a *release* to track that installation.

**Release Number (Release Version)** — A sequential counter is used to track releases as they change.

**Repository (Repo, Chart Repository)** — Helm charts may be stored on dedicated HTTP servers called *chart repositories* (*repositories*, or just *repos*).

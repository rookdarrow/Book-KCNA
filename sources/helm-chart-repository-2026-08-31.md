---
source_url: "https://helm.sh/docs/topics/chart_repository/"
fetched_at: "2026-08-31T04:26:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart-repository", "helm-repo-add", "chart-version-versus-appversion"]
---
# Helm — The Chart Repository Guide (helm.sh/docs/topics/chart_repository/)

A chart repository is an HTTP server that houses an `index.yaml` file and optionally some packaged charts.

Because a chart repository can be any HTTP server that can serve YAML and tar files and can answer GET requests, you have a plethora of options when it comes down to hosting your own chart repository.

## The index file

The index file is a yaml file called `index.yaml`. It contains some metadata about the package, including the contents of a chart's `Chart.yaml` file.

Example (excerpt, first entry only):

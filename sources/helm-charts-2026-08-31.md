---
source_url: "https://helm.sh/docs/topics/charts/"
fetched_at: "2026-08-31T04:12:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm", "chart", "chart-yaml", "values-yaml", "chart-templates-directory", "chart-dependencies-directory", "chart-crds-directory", "subchart", "notes-txt", "go-template-in-helm", "chart-version-versus-appversion", "crd-ordering-problem"]
---
# Helm — Charts (helm.sh/docs/topics/charts/)

Helm uses a packaging format called *charts*. A chart is a collection of files that describe a related set of Kubernetes resources. A single chart might be used to deploy something simple, like a memcached pod, or something complex, like a full web app stack with HTTP servers, databases, caches, and so on.

Charts are created as files laid out in a particular directory tree. They can be packaged into versioned archives to be deployed.

## The Chart File Structure

A chart is organized as a collection of files inside of a directory. The directory name is the name of the chart (without versioning information). Thus, a chart describing WordPress would be stored in a `wordpress/` directory.

Inside of this directory, Helm will expect a structure that matches this:

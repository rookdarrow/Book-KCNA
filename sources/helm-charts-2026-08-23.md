---
source_url: "https://helm.sh/docs/topics/charts/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Helm project (CNCF graduated)"
objectives_covered: ["D3 Application Delivery"]
concepts_covered: ["helm", "chart", "values", "templates", "chart-repository", "release"]
---
# Helm — Charts (helm.sh/docs/topics/charts/)

Helm uses a packaging format called charts. A chart is a collection of files that describe a related set of Kubernetes resources. A single chart might be used to deploy something simple, like a memcached pod, or something complex, like a full web app stack with HTTP servers, databases, caches, and so on. Charts are created as files laid out in a particular directory tree. They can be packaged into versioned archives to be deployed.

## The chart file structure
- Chart.yaml — a YAML file containing information about the chart
- LICENSE — optional: a plain text file containing the license for the chart
- README.md — optional: a human-readable README file
- values.yaml — the default configuration values for this chart
- values.schema.json — optional: a JSON Schema for imposing a structure on the values.yaml file
- charts/ — a directory containing any charts upon which this chart depends
- crds/ — Custom Resource Definitions
- templates/ — a directory of templates that, when combined with values, will generate valid Kubernetes manifest files
- templates/NOTES.txt — optional: a plain text file containing short usage notes

A chart repository is an HTTP server that houses one or more packaged charts, managed with the helm repo commands. An installed instance of a chart in a cluster is a release; the same chart can be installed many times, each creating a separately named release that can be upgraded and rolled back independently.

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

<!-- EXTENDED 2026-08-31 past the truncation point recorded in Ch 14's G-14a AUTHOR-REVIEW.
     Same page, same source_url; re-fetched to capture the Chart.yaml field table, which the
     first capture stopped immediately before. Scope of this extension: the Chart.yaml fields,
     the appVersion/version relationship, the charts/ dependency directory, and what one
     install of a parent chart produces. Not transcribed: the full templates/ and values
     discussion, chart hooks, and the .helmignore rules. -->

```
wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  values.yaml         # The default configuration values for this chart
  values.schema.json  # OPTIONAL: A JSON Schema for imposing a structure on the values.yaml file
  charts/             # A directory containing any charts upon which this chart depends.
  crds/               # Custom Resource Definitions
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
```

## The Chart.yaml File

The `Chart.yaml` file is required for a chart. It contains the following fields:

| Field | Description | Required? |
|---|---|---|
| `apiVersion` | The chart API version | required |
| `name` | The name of the chart | required |
| `version` | A SemVer 2 version | required |
| `kubeVersion` | A SemVer range of compatible Kubernetes versions | optional |
| `description` | A single-sentence description of this project | optional |
| `type` | The type of the chart | optional |
| `keywords` | A list of keywords about this project | optional |
| `home` | The URL of this project's home page | optional |
| `sources` | A list of URLs to source code for this project | optional |
| `dependencies` | A list of the chart requirements | optional |
| `maintainers` | Maintainer entries, each with `name`, `email`, `url` | optional |
| `icon` | A URL to an SVG or PNG image to be used as an icon | optional |
| `appVersion` | The version of the app that this contains | optional |
| `deprecated` | Whether this chart is deprecated (boolean) | optional |
| `annotations` | A list of annotations keyed by name | optional |

### appVersion

> "Note that the `appVersion` field is not related to the `version` field."

> "This field is informational, and has no impact on chart version calculations."

The documentation also notes that version numbers should be wrapped in quotes to prevent YAML
parsing errors.

## Chart Dependencies — the `charts/` directory

> "A dependency should be an unpacked chart directory"

placed inside the chart's `charts/` directory.

## What one install of a parent chart produces

> "After installation/upgrade of chart A a single Helm release is created/modified. The release
> will create/update all of the above Kubernetes objects in the following order:"

— the objects contributed by the parent chart and by its dependencies are aggregated, then
sorted by type and name, then created or updated in that order. One release covers all of them.


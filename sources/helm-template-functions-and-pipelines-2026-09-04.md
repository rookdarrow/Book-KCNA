---
source_url: "https://helm.sh/docs/chart_template_guide/functions_and_pipelines/"
fetched_at: "2026-09-04T17:20:00-0400"
authority: "Helm project (CNCF graduated project), Chart Template Developer's Guide; retrieved from the helm/helm-www source of record, docs/chart_template_guide/functions_and_pipelines.mdx and docs/chart_template_guide/index.mdx on branch main, because helm.sh was unreachable from the fetch layer"
objectives_covered: ["D3.1"]
concepts_covered: ["go-template-in-helm", "chart-templates-directory"]
---

# Helm — Chart Template Guide: Template Functions and Pipelines (helm.sh/docs/chart_template_guide/functions_and_pipelines/)

> **Snapshot note.** Fetched 2026-09-04 to close Chapter 14's G-14c (the identity of Helm's
> template language). Scope: the sentences naming the Go template language and the Sprig
> library, plus the guide's index description. Not transcribed: the function examples,
> pipelines, `default`, `quote`, `lookup` and the rest of the page.

## The Chart Template Developer's Guide (index page)

"This guide provides an introduction to Helm's chart templates, with emphasis on the template
language."

"Templates generate manifest files, which are YAML-formatted resource descriptions that
Kubernetes can understand. We'll look at how templates are structured, how they can be used,
how to write Go templates, and how to debug your work."

## Template Functions and Pipelines

"Helm has over 60 available functions. Some of them are defined by the Go template language
itself. Most of the others are part of the Sprig template library. We'll see many of them as we
progress through the examples."

"While we talk about the "Helm template language" as if it is Helm-specific, it is actually a
combination of the Go template language, some extra functions, and a variety of wrappers to
expose certain objects to the templates. Many resources on Go templates may be helpful as you
learn about templating."

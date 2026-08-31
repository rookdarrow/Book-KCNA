---
source_url: "https://helm.sh/docs/chart_template_guide/named_templates/"
fetched_at: "2026-08-31T04:33:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart-helpers", "go-template-in-helm", "chart-templates-directory"]
---
# Helm — Named Templates (helm.sh/docs/chart_template_guide/named_templates/)

But files whose name begins with an underscore (`_`) are assumed to *not* have a manifest inside. These files are not rendered to Kubernetes object definitions, but are available everywhere within other chart templates for use.

In fact, when we first created `mychart`, we saw a file called `_helpers.tpl`. That file is the default location for template partials.

The `define` action allows us to create a named template inside of a template file.

To work around this case, Helm provides an alternative to `template` that will import the contents of a template into the present pipeline where it can be passed along to other functions in the pipeline.

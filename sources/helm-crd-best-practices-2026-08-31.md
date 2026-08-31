---
source_url: "https://helm.sh/docs/chart_best_practices/custom_resource_definitions/"
fetched_at: "2026-08-31T04:26:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart-crds-directory", "crd-ordering-problem", "subchart"]
---
# Helm — Custom Resource Definitions (helm.sh/docs/chart_best_practices/custom_resource_definitions/)

There is a declaration of a CRD. This is the YAML file that has the kind `CustomResourceDefinition`. Then there are resources that *use* the CRD.

For a CRD, the declaration must be registered before any resources of that CRDs kind(s) can be used.

## Method 1: Let `helm` Do It For You

There is now a special directory called `crds` that you can create in your chart to hold your CRDs. These CRDs are not templated, but will be installed by default when running a `helm install` for the chart.

If you wish to skip the CRD installation step, you can pass the `--skip-crds` flag.

There is no support at this time for upgrading or deleting CRDs using Helm.

The `--dry-run` flag of `helm install` and `helm upgrade` is not currently supported for CRDs.

## Method 2: Separate Charts

Put the CRD definition in one chart, and then put any resources that use that CRD in *another* chart.

This workflow may be more useful for cluster operators who have admin access to a cluster.

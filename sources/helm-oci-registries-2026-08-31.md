---
source_url: "https://helm.sh/docs/topics/registries/"
fetched_at: "2026-08-31T04:26:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["oci-registry-as-chart-store", "chart-repository", "chart-version-versus-appversion"]
---
# Helm — Use OCI-based registries (helm.sh/docs/topics/registries/)

It is recommended to use container registries with OCI support to store and share chart packages.

An OCI-based registry can contain zero or more Helm repositories and each of those repositories can contain zero or more packaged Helm charts.

When using `helm push` to upload a chart an OCI registry, the reference must be prefixed with `oci://` and must not contain the basename or tag.

The basename (chart name) of the registry reference *is* included for any type of action involving chart download (vs. `helm push` where it is omitted).

The registry reference basename is inferred from the chart's name, and the tag is inferred from the chart's semantic version.

## Commands

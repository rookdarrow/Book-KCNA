---
source_url: "https://helm.sh/docs/intro/using_helm/"
fetched_at: "2026-08-31T04:24:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm-release", "helm-release-revision", "helm-rollback-versus-rollout-undo", "helm-install", "helm-upgrade", "helm-rollback", "helm-list", "values-yaml"]
---
# Helm — Using Helm (helm.sh/docs/intro/using_helm/)

## Installing a package, and the release object

Installing a chart creates a new *release* object.

If you want Helm to generate a name for you, leave off the release name and use `--generate-name`.

## Customizing the chart before installing

* `--values` (or `-f`): Specify a YAML file with overrides. This can be specified multiple times and the rightmost file will take precedence
* `--set`: Specify overrides on the command line.

If both are used, `--set` values are merged into `--values` with higher precedence.

## Upgrading a release and recovering on failure

It will only update things that have changed since the last release.

`helm rollback [RELEASE] [REVISION]`

Example:

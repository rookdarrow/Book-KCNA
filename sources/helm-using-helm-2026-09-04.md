---
source_url: "https://helm.sh/docs/intro/using_helm/"
fetched_at: "2026-09-04T17:20:00-0400"
authority: "Helm project (CNCF graduated project); retrieved from the helm/helm-www source of record, docs/intro/using_helm.mdx on branch main, because helm.sh was unreachable from the fetch layer"
objectives_covered: ["D3.1"]
concepts_covered: ["helm-release", "helm-release-revision", "helm-rollback", "helm-rollback-versus-rollout-undo", "helm-upgrade", "helm-install", "values-yaml"]
---

# Helm — Using Helm (helm.sh/docs/intro/using_helm/)

> **Snapshot note.** Fetched 2026-09-04 to close Chapter 14's G-14g: whether a `helm rollback`
> is recorded as a new numbered revision. The 2026-08-31 capture of this page stopped at the
> `helm rollback` synopsis, immediately before the sentences below. Same page, same source_url.

## Customizing the Chart Before Installing

"There are two ways to pass configuration data during install:

- `--values` (or `-f`): Specify a YAML file with overrides. This can be specified multiple
  times and the rightmost file will take precedence
- `--set`: Specify overrides on the command line."

"If both are used, `--set` values are merged into `--values` with higher precedence. Overrides
specified with `--set` are persisted in a Secret."

## Upgrading a Release, and Recovering on Failure

"An upgrade takes an existing release and upgrades it according to the information you
provide. Because Kubernetes charts can be large and complex, Helm tries to perform the least
invasive upgrade. It will only update things that have changed since the last release."

"Now, if something does not go as planned during a release, it is easy to roll back to a
previous release using `helm rollback [RELEASE] [REVISION]`."

```
$ helm rollback happy-panda 1
```

"The above rolls back our happy-panda to its very first release version. A release version is
an incremental revision. Every time an install, upgrade, or rollback happens, the revision
number is incremented by 1. The first revision number is always 1. And we can use
`helm history [RELEASE]` to see revision numbers for a certain release."

"If a release was created by a rollback, pass `--show-rollback-revision` to `helm history` to
add a `ROLLBACK` column to the output. This column shows which revision each rollback
targeted."

## What this settles for Chapter 14

A rollback does not move a pointer back to an earlier revision. It creates a new revision (the
counter increments on install, upgrade, and rollback alike) whose contents are those of the
targeted revision. In ch14-fig03's terms, `helm rollback marketing 2` after three revisions
produces revision 4, whose contents match revision 2.

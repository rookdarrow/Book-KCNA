---
source_url: "https://helm.sh/docs/helm/helm_rollback/"
fetched_at: "2026-08-31T04:31:00-0400"
authority: "Helm project (CLI reference)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm-rollback", "helm-release", "helm-release-revision", "helm-rollback-versus-rollout-undo"]
---
# helm rollback (helm.sh/docs/helm/helm_rollback/)

roll back a release to a previous revision

## Synopsis

The first argument of the rollback command is the name of a release, and the second is a revision (version) number.

If this argument is omitted or set to 0, it will roll back to the previous release.

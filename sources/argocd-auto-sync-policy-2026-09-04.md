---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/auto_sync/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Argo project (Argo CD; CNCF graduated) — user guide, Automated Sync Policy; text taken from the project's docs source (argoproj/argo-cd, docs/user-guide/auto_sync.md)"
objectives_covered: ["D3.1"]
concepts_covered: ["sync-operation", "self-heal", "drift-detection", "synced-outofsync", "continuously-reconciled-principle"]
---
# Argo CD — Automated Sync Policy

CAPTURE NOTE: supersedes argocd-auto-sync-policy-2026-08-31, which was truncated at the page's first code fence and carried only the opening sentence. Every passage below is verbatim from the page.

## Automated Sync Policy
"Argo CD has the ability to automatically sync an application when it detects differences between the desired manifests in Git, and the live state in the cluster. A benefit of automatic sync is that CI/CD pipelines no longer need direct access to the Argo CD API server to perform the deployment. Instead, the pipeline makes a commit and push to the Git repository with the changes to the manifests in the tracking Git repo."

## Automatic Pruning
"By default (and as a safety mechanism), automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git. To prune the resources, a manual sync can always be performed (with pruning checked). Pruning can also be enabled to happen automatically as part of the automated sync by running:"

## Automatic Self-Healing
"By default, changes that are made to the live cluster will not trigger automated sync. To enable automatic sync when the live cluster's state deviates from the state defined in Git, run:"

## Automated Sync Semantics
"An automated sync will only be performed if the application is OutOfSync. Applications in a Synced or error state will not attempt automated sync."

"Automated sync will only attempt one synchronization per unique combination of commit SHA1 and application parameters. If the most recent successful sync in the history was already performed against the same commit-SHA and parameters, a second sync will not be attempted, unless `selfHeal` flag is set to true."

"If the `selfHeal` flag is set to true, then the sync will be attempted again after self-heal timeout (5 seconds by default) which is controlled by `--self-heal-timeout-seconds` flag of `argocd-application-controller` deployment."

"Automatic sync will not reattempt a sync if the previous sync attempt against the same commit-SHA and parameters had failed."

"Rollback cannot be performed against an application with automated sync enabled."

"The automatic sync interval is determined by the `timeout.reconciliation` value in the `argocd-cm` ConfigMap, which defaults to `120s` with added jitter of `60s` for a maximum period of 3 minutes."

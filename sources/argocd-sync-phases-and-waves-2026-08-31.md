---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["sync-hook-phases", "sync-wave", "sync-operation"]
---
# Argo CD — Sync Phases and Waves

## Phases
Argo CD executes a sync in phases. The documented phase descriptions:

- **PreSync** — hooks run "prior to the application of the manifests."
- **Sync** — hooks run "after all PreSync hooks completed and were successful, at the same time as the application of the manifests."
- **PostSync** — hooks run "after all Sync hooks completed and were successful, a successful application, and all resources in a Healthy state."
- **SyncFail** — hooks run "when the sync operation fails."

Phase execution: all PreSync-marked resources are applied first, and if any fail the process stops. Sync-marked resources are applied next; a failure marks the operation failed and SyncFail hooks also execute. PostSync hooks run last; their failure marks the deployment failed.

## Waves
Waves are set with the `argocd.argoproj.io/sync-wave` annotation, taking an integer value.

"Hooks and resources are assigned to wave 0 by default. The wave can be negative, so you can create a wave that runs before all other resources."

## Ordering algorithm
When applying a sync, Argo CD orders resources by:

"1. The phase
2. The wave they are in (lower values first)
3. By kind
4. By name"

## Annotations
- `argocd.argoproj.io/hook: PreSync`
- `argocd.argoproj.io/sync-wave: "5"`

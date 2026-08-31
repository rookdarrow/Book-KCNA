---
source_url: "https://argo-cd.readthedocs.io/en/stable/operator-manual/architecture/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["argo-cd", "delivery-agent-identity", "sync-hook-phases", "drift-detection", "synced-outofsync", "cicd"]
---
# Argo CD — Architecture (components)

## API Server
"The API server is a gRPC/REST server which exposes the API consumed by the Web UI, CLI, and CI/CD systems."

Its listed responsibilities include: "application management and status reporting"; "invoking of application operations (e.g. sync, rollback, user-defined actions)"; "repository and cluster credential management"; "authentication and auth delegation to external identity providers"; "RBAC enforcement"; "listener/forwarder for Git webhook events".

## Repository Server
"The repository server is an internal service which maintains a local cache of the Git repository holding the application manifests."

It is responsible for "generating and returning the Kubernetes manifests when provided" a repository URL, a revision, an application path, and template-specific configuration.

## Application Controller
"The application controller is a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the repo)."

It "detects `OutOfSync` application state and optionally takes corrective action."

It is responsible for "invoking any user-defined hooks for lifecycle events (PreSync, Sync, PostSync)."

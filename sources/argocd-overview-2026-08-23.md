---
source_url: "https://argo-cd.readthedocs.io/en/stable/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Argo project (CNCF graduated)"
objectives_covered: ["D3 Application Delivery"]
concepts_covered: ["argo-cd", "gitops", "continuous-delivery", "sync-status", "outofsync", "declarative-deployment"]
---
# Argo CD — Overview (argo-cd.readthedocs.io)

## What is Argo CD?
Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.

## Why Argo CD?
Application definitions, configurations, and environments should be declarative and version controlled. Application deployment and lifecycle management should be automated, auditable, and easy to understand.

## How it works
Argo CD follows the GitOps pattern of using Git repositories as the source of truth for defining the desired application state. Kubernetes manifests can be specified in several ways: kustomize applications; helm charts; jsonnet files; plain directory of YAML/json manifests; any custom config management tool configured as a config management plugin. Argo CD automates the deployment of the desired application states in the specified target environments. Application deployments can track updates to branches, tags, or pinned to a specific version of manifests at a Git commit. Argo CD is implemented as a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the Git repo). A deployed application whose live state deviates from the target state is considered OutOfSync. Argo CD reports and visualizes the differences, while providing facilities to automatically or manually sync the live state back to the desired target state.

## Features
Automated deployment of applications to specified target environments; support for multiple config management/templating tools (Kustomize, Helm, Jsonnet, plain-YAML); ability to manage and deploy to multiple clusters; SSO integration; multi-tenancy and RBAC policies for authorization; rollback/roll-anywhere to any application configuration committed in Git repository; health status analysis of application resources; automated configuration drift detection and visualization; automated or manual syncing of applications to its desired state; web UI; CLI for automation and CI integration; webhook integration; access tokens for automation; PreSync, Sync, PostSync hooks to support complex application rollouts (e.g. blue/green and canary upgrades); audit trails for application events and API calls; Prometheus metrics; parameter overrides for overriding helm parameters in Git.

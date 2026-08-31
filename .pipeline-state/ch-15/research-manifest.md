I've gathered the sources. Here's the Stage 2 output.

# Research Manifest — KCNA Chapter 15

**Chapter:** 15 — *The Chart Is the Truth* · **Objective:** D3.1 Cloud Native Application Delivery (Application Delivery)
**Fetched:** 2026-08-31 · **New snapshots:** 26 · **Cached snapshots relied on:** 7

The outline flagged five blocking research gaps (Open Question 1) plus two facts that must not be written from memory (Open Question 8) and one fetch-or-drop decision (Open Question 2). **Four of the five blocking gaps are now closed, both OQ8 facts are pinned, and OQ2 is resolved with a caveat.** One gap survives and is flagged below.

---

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `argocd-core-concepts-2026-08-31.md` | Argo project (CNCF graduated) | D3.1 | argo-cd, argo-cd-application-resource, source-of-truth, manifest-source, synced-outofsync, sync-operation |
| `argocd-architecture-2026-08-31.md` | Argo project | D3.1 | argo-cd, delivery-agent-identity, sync-hook-phases, drift-detection |
| `argocd-declarative-setup-2026-08-31.md` | Argo project | D3.1 | argo-cd-application-resource, source-of-truth, manifest-source, multi-cluster-delivery |
| `argocd-auto-sync-policy-2026-08-31.md` | Argo project | D3.1 | sync-operation, self-heal, drift-detection, continuously-reconciled-principle |
| `argocd-sync-phases-and-waves-2026-08-31.md` | Argo project | D3.1 | sync-hook-phases, sync-wave |
| `argocd-tracking-strategies-2026-08-31.md` | Argo project | D3.1 | tracking-branch-tag-commit, versioned-and-immutable-principle |
| `argocd-security-cluster-credentials-2026-08-31.md` | Argo project | D3.1 | delivery-agent-identity, blast-radius, pull-based-delivery |
| `argocd-best-practices-2026-08-31.md` | Argo project | D3.1 | source-of-truth, versioned-and-immutable-principle, cicd |
| `argocd-diffing-outofsync-2026-08-31.md` | Argo project | D3.1 | synced-outofsync, drift-detection |
| `flux-concepts-2026-08-31.md` | Flux project (CNCF graduated) | D3.1 | flux, flux-bootstrap, continuously-reconciled-principle, drift-detection |
| `flux-components-2026-08-31.md` | Flux project | D3.1 | flux-controller-set, manifest-source |
| `flux-kustomization-api-2026-08-31.md` | Flux project | D3.1 | flux-controller-set, continuously-reconciled-principle, delivery-agent-identity |
| `flux-security-2026-08-31.md` | Flux project | D3.1 | delivery-agent-identity, blast-radius |
| `opengitops-principles-v1-2026-08-31.md` | OpenGitOps (CNCF) | D3.1 | opengitops-four-principles + all four principle concepts |
| `opengitops-glossary-2026-08-31.md` | OpenGitOps (CNCF) | D3.1 | gitops, source-of-truth, drift-detection, continuously-reconciled-principle |
| `opengitops-1-0-announcement-2026-08-31.md` | OpenGitOps (CNCF) | D3.1 | gitops, pulled-automatically-principle |
| `cncf-glossary-gitops-2026-08-31.md` | CNCF | D3.1 | gitops, drift-detection, rollback-by-revert, self-heal |
| `cncf-glossary-blue-green-deployment-2026-08-31.md` | CNCF | D3.1 | blue-green-deployment |
| `cncf-glossary-canary-deployment-2026-08-31.md` | CNCF | D3.1 | canary-deployment |
| `cncf-glossary-continuous-integration-2026-08-31.md` | CNCF | D3.1 | cicd |
| `cncf-glossary-continuous-delivery-2026-08-31.md` | CNCF | D3.1 | cicd |
| `cncf-glossary-continuous-deployment-2026-08-31.md` | CNCF | D3.1 | cicd |
| `argo-rollouts-experiments-2026-08-31.md` | Argo project | D3.1 | progressive-delivery, canary-deployment (A/B) |
| `argo-rollouts-canary-2026-08-31.md` | Argo project | D3.1 | canary-deployment, progressive-delivery |
| `twelve-factor-iii-config-2026-08-31.md` | The Twelve-Factor App | D3.1 | factor-iii-config-in-environment |
| `twelve-factor-vi-processes-2026-08-31.md` | The Twelve-Factor App | D3.1 | factor-vi-stateless-processes |
| `twelve-factor-ix-disposability-2026-08-31.md` | The Twelve-Factor App | D3.1 | factor-ix-disposability |
| `twelve-factor-xi-logs-2026-08-31.md` | The Twelve-Factor App | D3.1 | factor-xi-logs-as-event-streams |

**Cached snapshots this chapter still relies on and that were NOT re-fetched:** `opengitops-principles-2026-08-23`, `argocd-overview-2026-08-23`, `flux-concepts-2026-08-23`, `twelve-factor-app-2026-08-23`, `argo-rollouts-strategies-2026-08-23`, `k8s-docs-overview-2026-08-23`, `k8s-docs-service-accounts-2026-08-23`, `cncf-project-maturity-levels-2026-08-23`, `cncf-kcna-curriculum-pdf-2026-08-23`. All remain valid.

---

## Gaps

**G-15-1 — The push/pull *blast-radius* argument is still not directly sourced. PARTIALLY CLOSED, and the residue is real.**

The outline's Open Question 1 asked for `opengitops.dev/faq`. **That page does not exist** (HTTP 404), and the OpenGitOps `documents` repository contains only `PRINCIPLES.md`, `GLOSSARY.md`, `README.md`, `CONTRIBUTING.md`, `LICENSE.md` — there is no FAQ, no patterns document, and no push-vs-pull comparison anywhere in the OpenGitOps corpus. The Flux FAQ and Flux security best-practices pages were both checked and neither discusses push versus pull, agent placement, or credential exposure.

What §3 *can* now stand on, all newly sourced:

- Principle 3 verbatim — *"Software agents automatically pull the desired state declarations from the source"* — plus the 1.0 announcement's *"The GitOps software agents have to be aware of the actual state of a system under management and attempt to apply the desired state."*
- The pull side of the credential argument, concretely: Argo CD *"stores the credentials of the external cluster as a Kubernetes Secret in the `argocd` namespace"* and *"By default, Argo CD uses a clusteradmin level role."* Flux binds `cluster-admin` to the kustomize- and helm-controller service accounts. Both are in-cluster facts, stated by the projects themselves.
- Argo CD Best Practices supplies the access-separation reason directly: *"The developers who are developing the application, may not necessarily be the same people who can/should push to production environments."*

**What remains unsourced: the push side.** No cached or newly fetched source states that a CI pipeline holds cluster credentials outside the cluster, and **no source in the corpus uses the phrase "blast radius" at all.** Drafting may develop the argument as an *architectural consequence* of principle 3 plus the two projects' documented in-cluster credential storage — that is honest reasoning from tagged facts — but it may not attribute the push-side characterization or the term "blast radius" to a source. Recommend the draft either frames it explicitly as the book's own reading, or drops "blast radius" as a headword and keeps `blast-radius` in `kb_tags` as a glossary-only concept.

**G-15-2 — Flux's multi-cluster model ("a Flux per cluster, each pulling") is UNSOURCED.**

`fluxcd.io/flux/installation/configuration/multi-tenancy/` returns 404; the concepts, components, security, and FAQ pages do not describe a multi-cluster topology. Argo CD's side *is* sourced — the overview features list says *"ability to manage and deploy to multiple clusters"*, and declarative-setup shows external clusters registered as labelled Secrets alongside the in-cluster target `https://kubernetes.default.svc`. **§6 may state Argo CD's multi-cluster model with a tag. It may not state Flux's as fact.** Either soften to "Flux's controllers run in the cluster they reconcile" (which *is* supported by `flux-security-2026-08-31`) or cut the comparison to a single sourced sentence about Argo CD.

**G-15-3 — `AppProject` is not on the Argo CD core-concepts page.** It is on declarative-setup and is captured there. Not blocking; noted so no downstream stage cites the wrong snapshot.

**G-15-4 — No source enumerates the LFS250 course modules.** Confirmed again this pass; unchanged from Ch 14. The honesty framing in Open Question 7 stands exactly as the outline wrote it.

---

## Notes for the author

**1. Open Question 2 (A/B testing) — RESOLVED, but not in the direction the outline assumed. Read this before drafting §2.**

A/B testing *is* documented by Argo Rollouts — but **not as a deployment strategy.** It appears on the **Experiment** CRD page: *"A user can use experiments to enable A/B/C testing by launching multiple experiments with a different version of their application for a long duration."* The Canary strategy page was checked directly and **the string "A/B" does not appear on it.**

This confirms the outline's own suspicion verbatim: A/B is "a product-experimentation technique that release tooling can implement, not a deployment strategy in the same sense as the other four." The source now supports saying exactly that. **Recommendation: keep A/B in §2, but demote it** — name it as an *experimentation* pattern that canary tooling enables, tagged `[source: argo-rollouts-experiments-2026-08-31]`, rather than listing it as a fifth peer of Recreate / RollingUpdate / blue-green / canary. That is a stronger teaching move than either the original listing or the cut, and it keeps `ch15-fig02`'s four-panel structure intact. If you prefer the cut, the fetch no longer forces it.

**2. Open Question 8(a) — self-heal is OFF by default. Pinned.**

Argo CD: *"By default, changes that are made to the live cluster will not trigger automated sync."* Automatic pruning is likewise off: *"By default (and as a safety mechanism), automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git."* Both are opt-in via `syncPolicy.automated.selfHeal` / `.prune`.

**This materially changes §4's account of drift, exactly as the outline predicted.** Out of the box, a human editing the cluster produces `OutOfSync` and Argo CD **reports** it — it does not revert it. That is a *better* fit for the chapter's Fixed Point ("`OutOfSync` is a drift signal, not an error") than the reverting behavior would have been, and it makes the ⚠ trap sharper: readers who assume the agent always reverts are wrong by default. Also newly available: the automated sync interval *"defaults to `120s` with added jitter of `60s` for a maximum period of 3 minutes."*

**3. Open Question 8(b) — Flux's five minutes: CONFIRMED on one page, CONTRADICTED in emphasis on another. Do not write it as an API default.**

The concepts page still says *"The reconciliation runs every five minutes by default, but this can be changed with `.spec.interval`."* But the Kustomization API reference says *"`.spec.interval` is a required field... The minimum value should be 60 seconds"* and **states no default at all.** The reconciliation is therefore a required field on every Kustomization; the "five minutes" is what Flux's own bootstrap-generated Kustomization sets, not a value the API supplies.

**Recommendation for the ⚓ Worth Securing in §6:** secure the *behavior*, not the number — *"changes made with `kubectl edit/patch/delete` are promptly reverted"* is the load-bearing claim and it is unambiguous on both pages. If you want the interval, phrase it as "typically five minutes, and always explicitly configured," tagged to `flux-concepts-2026-08-31`. The reverting sentence also now has better wording than the cached snapshot: *"If you make any changes to the cluster using `kubectl edit/patch/delete`, they will be promptly reverted."*

**4. Version drift: Flux's own definition of "GitOps Toolkit" has changed since the 2026-08-23 snapshot.**

Cached (`flux-concepts-2026-08-23`): *"Flux is a GitOps Toolkit: a set of composable APIs and specialized tools."*
Current (`flux-concepts-2026-08-31`): *"In Flux, GitOps Toolkit refers to a collection of specialized tools, Flux Controllers, composable APIs, and reusable Go packages available under the fluxcd GitHub organization."*

Not a contradiction, but the newer wording is narrower — the Toolkit is now framed as the *implementation substrate*, not as what Flux *is*. §6's framing of Flux as "a GitOps Toolkit, a genuinely different design posture from Argo CD's integrated model" is still defensible, but **cite the newer snapshot** so the quoted phrase matches the live page. Both files are kept; the older one remains valid as a dated capture and is cited elsewhere in the outline.

**5. Sources disagree on blue/green, and the disagreement is worth a sentence.**

Argo Rollouts is neutral and mechanical. The **CNCF Glossary is openly disapproving**: *"its use is normally a 'smell' that legacy software needs to be re-engineered so that components can be updated individually."* CNCF also scopes blue/green to *entire systems* rather than single services, and explicitly notes the term is often misapplied to individual services.

Since CNCF is the exam authority and Argo is a vendor project, the priority rule applies: **where they differ, CNCF's framing governs.** This is a gift to §2 — it supplies a non-obvious, authority-backed nuance (blue/green is an environment-level strategy, and needing it is often a signal about the application) that lifts the section above four definitions. It also complicates the outline's "blue/green needs no traffic provider and suits queue workers" line, which is Argo's view; keep it, tag it to Argo, and let CNCF's caveat follow.

**6. §5's sync waves are now fully sourced, and the ordering is more precise than the outline assumed.**

Phases and waves are captured verbatim. Two details the outline did not anticipate: **the default wave is 0 and waves may be negative** (*"Hooks and resources are assigned to wave 0 by default. The wave can be negative, so you can create a wave that runs before all other resources."*), and the ordering is a **four-key sort**: *"1. The phase 2. The wave they are in (lower values first) 3. By kind 4. By name."* Argo CD also recognizes a fourth phase, `SyncFail`, which runs *"when the sync operation fails"* — worth one clause, since it makes the phase model legible as a lifecycle rather than a list of three.

The 🟡 depth ruling still holds: annotation syntax is captured in the snapshot but should not reach the page. The negative-wave fact is the one detail I'd argue *is* worth teaching, because it is what makes waves an ordering system rather than a queue.

**7. §4's identity pin is now solidly sourced from three directions — this was the outline's "worst gap in the chapter" and it is closed.**

Argo CD: cluster credentials are `argocd-manager` ServiceAccount bearer tokens stored as Secrets in the `argocd` namespace; *"By default, Argo CD uses a clusteradmin level role"*; and *"Although Argo CD requires cluster-wide read privileges to resources in the managed cluster to function properly, it does not necessarily need full write privileges to the cluster."* Flux: a `crd-controller` ClusterRole, and a `cluster-reconciler` ClusterRoleBinding referencing `cluster-admin` bound only to the kustomize- and helm-controller service accounts. Flux additionally supports `.spec.serviceAccountName` impersonation so a tenant's repo is not reconciled under `cluster-admin`.

That last fact is a genuine bonus for the Ch 12 cross-bearing: the delivery agent is not merely *a* subject with broad grants — both projects ship documented mechanisms for narrowing them, which is precisely Ch 12 §3's lesson arriving in production form. **Recommend §4 use it**; it converts the identity pin from a warning into a demonstration.

**8. The `Application` custom resource is now sourced — but note where from.**

The core-concepts glossary defines it (*"A group of Kubernetes resources as defined by a manifest. This is a Custom Resource Definition (CRD)."*) and declarative-setup supplies the full spec and a minimal YAML example. The cached `argocd-overview-2026-08-23` still never uses the word, so **every `Application` claim must tag the new snapshots**, not the overview. `AppProject` is on declarative-setup only.

**9. Capture-fidelity note, recorded for the audit stage.**

Every snapshot body below contains only material that came back from the fetch inside quotation marks, plus code blocks reproduced literally. Where the fetch tool summarized rather than quoted, that material was **discarded rather than included** — so these files are shorter than the source pages but contain no paraphrase presented as source text. Two snapshots (`argocd-diffing-outofsync`, `argo-rollouts-canary`) are consequently very short; they are kept because each carries one load-bearing sentence.

**10. Acronym register (Open Question 10) is now fully supplied.** CNCF's own glossary expands all three: continuous integration (*"often abbreviated as CI"*), continuous delivery (*"often abbreviated as CD"*), and continuous deployment (*"often abbreviated as CD"* — note that **CNCF uses "CD" for both**, which is itself the reason the CI/CD expansion in §3 should name all three senses). That collision is a genuine teaching point and the ledger's three-row register handles it correctly.

---

## Snapshots

### A1 · `argocd-core-concepts-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-cd.readthedocs.io/en/stable/core_concepts/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["argo-cd", "argo-cd-application-resource", "source-of-truth", "manifest-source", "synced-outofsync", "sync-operation", "drift-detection"]
---
# Argo CD — Core Concepts / Glossary

Quoted entries from the page's glossary:

**Application:** "A group of Kubernetes resources as defined by a manifest. This is a Custom Resource Definition (CRD)."

**Application source type:** "Which Tool is used to build the application."

**Target state:** "The desired state of an application, as represented by files in a Git repository."

**Live state:** "The live state of that application. What pods etc are deployed."

**Sync status:** "Whether or not the live state matches the target state. Is the deployed application the same as Git says it should be?"

**Sync:** "The process of making an application move to its target state. E.g. by applying changes to a Kubernetes cluster."

**Sync operation status:** "Whether or not a sync succeeded."

**Refresh:** "Compare the latest code in Git with the live state. Figure out what is different."

**Health:** "The health of the application, is it running correctly? Can it serve requests?"

**Tool:** "A tool to create manifests from a directory of files. E.g. Kustomize. See Application Source Type."

**Configuration management tool:** "See Tool."

**Configuration management plugin:** "A custom tool."

CAPTURE NOTE: this page carries no entry for Project or AppProject. Those are
defined on the declarative-setup page — see argocd-declarative-setup-2026-08-31.md.
```

### A2 · `argocd-architecture-2026-08-31.md` (new)
```markdown
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
```

### A3 · `argocd-declarative-setup-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["argo-cd-application-resource", "source-of-truth", "manifest-source", "tracking-branch-tag-commit", "multi-cluster-delivery", "delivery-agent-identity"]
---
# Argo CD — Declarative Setup (Applications, Projects, Clusters)

## Applications
"The Application CRD is the Kubernetes resource object representing a deployed application instance in an environment."

It is defined by two key pieces of information: a "source reference to the desired state in Git (repository, revision, path, environment)" and a "destination reference to the target cluster and namespace."

A minimal Application manifest:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: guestbook
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/argoproj/argocd-example-apps.git
    targetRevision: HEAD
    path: guestbook
  destination:
    server: https://kubernetes.default.svc
    namespace: guestbook
```

## Projects
The AppProject CRD provides "a logical grouping of applications", defined by:

- "sourceRepos reference to the repositories that applications within the project can pull manifests from"
- "destinations reference to clusters and namespaces that applications within the project can deploy into"
- "roles list of entities with definitions of their access to resources within the project"

## Clusters
"Cluster credentials are stored in secrets same as repositories or repository credentials. Each secret must have label `argocd.argoproj.io/secret-type: cluster`."

Example cluster secret:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mycluster-secret
  labels:
    argocd.argoproj.io/secret-type: cluster
type: Opaque
stringData:
  name: mycluster.example.com
  server: https://mycluster.example.com
  config: |
    {
      "bearerToken": "<authentication token>",
      "tlsClientConfig": {
        "insecure": false,
        "caData": "<base64 encoded certificate>"
      }
    }
```

The in-cluster destination is referenced as `https://kubernetes.default.svc`.
```

### A4 · `argocd-auto-sync-policy-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/auto_sync/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["sync-operation", "self-heal", "drift-detection", "synced-outofsync", "continuously-reconciled-principle"]
---
# Argo CD — Automated Sync Policy

## What automated sync does
"Argo CD has the ability to automatically sync an application when it detects differences between the desired manifests in Git, and the live state in the cluster."

Enabled declaratively:

```yaml
spec:
  syncPolicy:
    automated: {}
```

or with explicit control:

```yaml
spec:
  syncPolicy:
    automated:
      enabled: true
```

## Automated sync semantics
- "An automated sync will only be performed if the application is OutOfSync."
- "Automatic sync will only attempt one synchronization per unique combination of commit SHA1 and application parameters."
- The automatic sync interval "defaults to `120s` with added jitter of `60s` for a maximum period of 3 minutes."

## Automatic pruning — DISABLED BY DEFAULT
"By default (and as a safety mechanism), automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git."

Enabled with `argocd app set <APPNAME> --auto-prune`, or:

```yaml
spec:
  syncPolicy:
    automated:
      prune: true
```

## Automatic self-healing — DISABLED BY DEFAULT
"By default, changes that are made to the live cluster will not trigger automated sync."

Enabled with `argocd app set <APPNAME> --self-heal`, or:

```yaml
spec:
  syncPolicy:
    automated:
      selfHeal: true
```
```

### A5 · `argocd-sync-phases-and-waves-2026-08-31.md` (new)
```markdown
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
```

### A6 · `argocd-tracking-strategies-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/tracking_strategies/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["tracking-branch-tag-commit", "versioned-and-immutable-principle", "source-of-truth"]
---
# Argo CD — Tracking and Deployment Strategies

"An Argo CD application spec provides several different ways of tracking Kubernetes resource manifests."

## Branch or symbolic reference
"If a branch name or a symbolic reference (like HEAD) is specified, Argo CD will continually compare live state against the resource manifests defined at the tip of the specified branch or the resolved commit of the symbolic reference."

## Tag
"If a tag is specified, the manifests at the specified Git tag will be used to perform the sync comparison."

Tags are "generally considered more stable, and less frequently updated" than branches.

## Pinned commit
"If a Git commit SHA is specified, the app is effectively pinned to the manifests defined at the specified commit."

"Since commit SHAs cannot change meaning, the only way to change the live state of an app which is pinned to a commit, is by updating the tracking revision in the application to a different commit containing the new manifests."
```

### A7 · `argocd-security-cluster-credentials-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-cd.readthedocs.io/en/stable/operator-manual/security/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["delivery-agent-identity", "blast-radius", "pull-based-delivery", "argo-cd"]
---
# Argo CD — Security (cluster credentials and RBAC)

## Where cluster credentials live
"To manage external clusters, Argo CD stores the credentials of the external cluster as a Kubernetes Secret in the argocd namespace."

Those credentials comprise "the K8s API bearer token associated with the `argocd-manager` ServiceAccount created during `argocd cluster add`, along with connection options to that API server."

## Default permissions
"By default, Argo CD uses a clusteradmin level role in order to:
1. watch & operate on cluster state
2. deploy resources to the cluster"

## Reducing permissions
"Although Argo CD requires cluster-wide read privileges to resources in the managed cluster to function properly, it does not necessarily need full write privileges to the cluster."

Operators may edit the ClusterRole of `argocd-manager-role` "such that write privileges are limited to only the namespaces and resources that you wish Argo CD to manage."
```

### A8 · `argocd-best-practices-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/best_practices/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["source-of-truth", "versioned-and-immutable-principle", "cicd", "tracking-branch-tag-commit"]
---
# Argo CD — Best Practices

## Separating config vs. source code repositories
Reasons given for keeping application configuration in a repository separate from application source:

1. "It provides a clean separation of application code vs. application config."
2. "For auditing purposes, a repo which only holds configuration will have a much cleaner Git history of what changes were made."
3. "Your application may comprise services built from multiple Git repositories, but is deployed as a single unit."
4. "The developers who are developing the application, may not necessarily be the same people who can/should push to production environments."
5. "Pushing manifest changes to the same Git repository can trigger an infinite loop of build jobs and Git commit triggers. Having a separate repo to push config changes to, prevents this from happening."

## Ensuring manifest immutability
On tracking an unstable revision such as HEAD: "Since this is not a stable target, the manifests for this kustomize application can suddenly change meaning, even without any changes to your own Git repository."

"A better version would be to use a Git tag or commit SHA."
```

### A9 · `argocd-diffing-outofsync-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/diffing/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["synced-outofsync", "drift-detection"]
---
# Argo CD — Diffing Customization

"It is possible for an application to be `OutOfSync` even immediately after a successful Sync operation."

CAPTURE NOTE: this snapshot deliberately carries a single sentence. The remainder of
the page enumerates causes (unknown fields in manifests, pruning disabled, mutating
controllers and webhooks, Helm template functions generating differing data, HPA
metric reordering) but the fetch returned those as summary rather than quotation, so
they are not reproduced here. Do not attribute any specific cause to this snapshot.
```

### A10 · `flux-concepts-2026-08-31.md` (new)
```markdown
---
source_url: "https://fluxcd.io/flux/concepts/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux", "flux-controller-set", "flux-bootstrap", "continuously-reconciled-principle", "drift-detection", "manifest-source"]
---
# Flux — Core concepts (2026-08-31 capture)

## GitOps Toolkit
"In Flux, GitOps Toolkit refers to a collection of specialized tools, Flux Controllers, composable APIs, and reusable Go packages available under the fluxcd GitHub organization."

## Sources
"A Source defines the origin of a repository containing the desired state of the system and the requirements to obtain it (e.g. credentials, version selectors)."

## Reconciliation
"Reconciliation refers to ensuring that a given state (e.g. application running in the cluster, infrastructure) matches a desired state declaratively defined somewhere (e.g. a Git repository)."

"The reconciliation runs every five minutes by default, but this can be changed with `.spec.interval`."

"If you make any changes to the cluster using `kubectl edit/patch/delete`, they will be promptly reverted."

## Bootstrap
"The process of installing the Flux components in a GitOps manner is called a bootstrap. The manifests are applied to the cluster, a `GitRepository` and `Kustomization` are created for the Flux components, then the manifests are pushed to an existing Git repository (or a new one is created)."

CAPTURE NOTE: the GitOps Toolkit definition differs from the 2026-08-23 capture,
which read "Flux is a GitOps Toolkit: a set of composable APIs and specialized
tools." Both captures are retained. Cite this one for the current wording.
```

### A11 · `flux-components-2026-08-31.md` (new)
```markdown
---
source_url: "https://fluxcd.io/flux/components/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux-controller-set", "manifest-source", "flux"]
---
# Flux — GitOps Toolkit components (controllers and their custom resources)

## Source Controller
Custom resources: GitRepository, OCIRepository, HelmRepository, HelmChart, Bucket, ExternalArtifact, ArtifactGenerator.

## Kustomize Controller
Custom resource: Kustomization.

## Helm Controller
Custom resource: HelmRelease.

## Notification Controller
Custom resources: Provider, Alert, Receiver.

## Image Reflector and Image Automation Controllers
Custom resources: ImageRepository, ImagePolicy, ImageUpdateAutomation.

CAPTURE NOTE: this index page carries only the controller names, their linked
documentation titles ("The GitOps Toolkit <X> Controller documentation") and the
CRD lists reproduced above. Per-controller prose lives on the linked sub-pages and
was not captured. Do not attribute behavioural claims to this snapshot.
```

### A12 · `flux-kustomization-api-2026-08-31.md` (new)
```markdown
---
source_url: "https://fluxcd.io/flux/components/kustomize/kustomizations/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["flux-controller-set", "continuously-reconciled-principle", "delivery-agent-identity", "drift-detection"]
---
# Flux — Kustomization API reference

## What it defines
"The `Kustomization` API defines a pipeline for fetching, decrypting, building, validating and applying Kustomize overlays or plain Kubernetes manifests."

## Interval
"`.spec.interval` is a required field that specifies the interval at which the Kustomization is reconciled, i.e. the controller fetches the source with the Kubernetes manifests, builds the Kustomization and applies it on the cluster, correcting any existing drift in the process. The minimum value should be 60 seconds."

CAPTURE NOTE: the API reference states no default for `.spec.interval` — only that
it is required and has a 60-second minimum. The "every five minutes by default"
figure comes from the concepts page and describes Flux's bootstrap-generated
Kustomization, not an API-level default.

## Prune
"`.spec.prune` is a required boolean field to enable/disable garbage collection for a Kustomization. Garbage collection means that the Kubernetes objects that were previously applied on the cluster but are missing from the current source revision, are removed from the cluster automatically."

## Service account impersonation
"`.spec.serviceAccountName` is an optional field used to specify the ServiceAccount to be impersonated while reconciling the Kustomization."
```

### A13 · `flux-security-2026-08-31.md` (new)
```markdown
---
source_url: "https://fluxcd.io/flux/security/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["delivery-agent-identity", "blast-radius", "flux-controller-set"]
---
# Flux — Security model (RBAC and impersonation)

## RBAC manifests installed
"Flux installs a set of RBAC manifests. These include: A `crd-controller` `ClusterRole`, which: Has full access to all the Custom Resource Definitions defined by Flux controllers"

"A `cluster-reconciler` `ClusterRoleBinding`: References `cluster-admin` `ClusterRole` Bound to service accounts for only `kustomize-controller` and `helm-controller`"

Those two controllers are bound to `cluster-admin` because they "are the only two controllers that manage resources in the cluster."

## Multi-tenancy and impersonation
"In a soft multi-tenancy setup, Flux does not reconcile a tenant's repo under the `cluster-admin` role. Instead, you specify a different service account in your manifest, and the Flux controllers will use the Kubernetes Impersonation API under `cluster-admin` to impersonate that service account."

## Related, from the security best-practices page
(https://fluxcd.io/flux/security/best-practices/)
A controller flag "Enforces all reconciliations to impersonate a given Service Account, effectively disabling the use of the privileged service account that would otherwise be used by the controller."

CAPTURE NOTE: neither the security page nor the security best-practices page
discusses push-based versus pull-based delivery, agent placement rationale, or
credential exposure outside the cluster. Verified 2026-08-31.
```

### A14 · `opengitops-principles-v1-2026-08-31.md` (new)
```markdown
---
source_url: "https://github.com/open-gitops/documents/blob/main/PRINCIPLES.md"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "OpenGitOps (CNCF project; GitOps Working Group)"
objectives_covered: ["D3.1"]
concepts_covered: ["gitops", "opengitops-four-principles", "declarative-principle", "versioned-and-immutable-principle", "pulled-automatically-principle", "continuously-reconciled-principle"]
---
# OpenGitOps Principles v1.0.0 (source document)

"GitOps is a set of principles for operating and managing software systems."

1. **Declarative** — "A system managed by GitOps must have its desired state expressed declaratively."
2. **Versioned and Immutable** — "Desired state is stored in a way that enforces immutability, versioning and retains a complete version history."
3. **Pulled Automatically** — "Software agents automatically pull the desired state declarations from the source."
4. **Continuously Reconciled** — "Software agents continuously observe actual system state and attempt to apply the desired state."

CAPTURE NOTE: the open-gitops/documents repository root contains only
CONTRIBUTING.md, GLOSSARY.md, LICENSE.md, PRINCIPLES.md and README.md. There is
no FAQ document and no push-versus-pull comparison document in the OpenGitOps
corpus. Verified 2026-08-31. The README describes the repo as holding "Lasting
documents from the OpenGitOps project which are versioned and released together
(including the GitOps Principles and Glossary)."
```

### A15 · `opengitops-glossary-2026-08-31.md` (new)
```markdown
---
source_url: "https://github.com/open-gitops/documents/blob/main/GLOSSARY.md"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "OpenGitOps (CNCF project; GitOps Working Group)"
objectives_covered: ["D3.1"]
concepts_covered: ["gitops", "source-of-truth", "drift-detection", "continuously-reconciled-principle", "versioned-and-immutable-principle"]
---
# OpenGitOps Glossary v1.0.0

**Desired State:** "The aggregate of all configuration data that is sufficient to recreate the system..."

**State Store:** "A system for storing immutable versions of desired state declarations."

**Reconciliation:** "The process of ensuring the actual state of a system matches its desired state."

**Drift:** "When a system's actual state has moved or is in the process of moving away from the desired state..."

CAPTURE NOTE: the fetch confirmed the glossary carries no separate entries for
"GitOps", "Software Agent", "State Description", "Continuous Deployment",
"GitOps Managed Software System" or "Rollback". The ellipses above are the
fetch's truncation of longer definitions; treat the truncated definitions as
partial and do not extend them from memory.
```

### A16 · `opengitops-1-0-announcement-2026-08-31.md` (new)
```markdown
---
source_url: "https://opengitops.dev/blog/1.0-announcement/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "OpenGitOps (CNCF project; GitOps Working Group)"
objectives_covered: ["D3.1"]
concepts_covered: ["gitops", "pulled-automatically-principle", "continuously-reconciled-principle", "opengitops-four-principles"]
---
# OpenGitOps 1.0 announcement

"GitOps is a set of principles for operating and managing software systems, derived from modern software operations."

"The wording of each principle and linked glossary item was very carefully chosen."

On version control systems other than Git: "Likewise, many version control systems can be used in GitOps as long as they meet those two basic requirements and teams use them in a conformant manner."

On agents: "Software agents automatically pull the desired state declarations from the source."

"The GitOps software agents have to be aware of the actual state of a system under management and attempt to apply the desired state."
```

### A17 · `cncf-glossary-gitops-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/gitops/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["gitops", "drift-detection", "self-heal", "rollback-by-revert", "source-of-truth"]
---
# CNCF Glossary — GitOps

## What it is
"GitOps is a set of practices for managing software applications and infrastructure by continuously evaluating and reconciling their desired states as defined in a version control system such as Git against their actual state."

## Problem it addresses
Named problems: "configuration drift, failed deployments, inconsistent environments, deployment failures, and difficulty tracking historical changes."

"Configuration drift can be hard to detect and resolve without a source of truth governing it."

## How it helps
GitOps manages "the entire infrastructure, application development, and deployment lifecycle using a single and unified process."

Named benefits: "transparency and traceability of changes, reliability and security through declarative states, and rollback, revert, and self-healing attributes."
```

### A18 · `cncf-glossary-blue-green-deployment-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/blue-green-deployment/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["blue-green-deployment", "deployment-strategy-vocabulary"]
---
# CNCF Glossary — Blue Green Deployment

## What it is
"Blue-green deployment is a strategy for updating running computer systems with minimal downtime. The operator maintains two environments, dubbed 'blue' and 'green'."

One environment serves live production traffic while the other is updated; after testing on the inactive environment, traffic switches via load balancer. The entry notes this typically affects entire systems with multiple services simultaneously, and that the term is sometimes misapplied to individual services.

## Problem it addresses
"Blue-green deployments allow minimal downtime when updating software that must be changed in 'lockstep' owing to a lack of backwards compatibility."

## How it helps
"Blue-green deployment is an appropriate strategy for non-cloud native software that needs to be updated with minimal downtime. However, its use is normally a 'smell' that legacy software needs to be re-engineered so that components can be updated individually."
```

### A19 · `cncf-glossary-canary-deployment-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/canary-deployment/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["canary-deployment", "deployment-strategy-vocabulary", "progressive-delivery"]
---
# CNCF Glossary — Canary Deployment

## What it is
"Canary deployments is a deployment strategy that starts with two environments: one with live traffic and the other containing the updated code without live traffic. The traffic is gradually moved from the original version of the application to the updated version."

## Problem it addresses
"No matter how thorough the testing strategy, there are always some bugs discovered in production. Shifting 100% of traffic from one version of an app to another can lead to more impactful failures."

## How it helps
"Canary deployments allow organizations to see how new software behaves in real-world scenarios before moving significant traffic to the new version. This strategy enables organizations to minimize downtime and quickly rollback in case of issues with the new deployment."
```

### A20 · `cncf-glossary-continuous-integration-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/continuous-integration/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["cicd"]
---
# CNCF Glossary — Continuous Integration

## What it is
"Continuous integration, often abbreviated as CI, is the practice of integrating code changes as regularly as possible."

## How it helps
"CI software automatically checks that code changes merge cleanly whenever a developer commits a change. It's a near-ubiquitous practice to use the CI server to run code quality checks, tests, and even deployments. As such, it becomes a concrete implementation of quality control within teams. CI allows software teams to turn every code commit into either a concrete failure or a viable release candidate."
```

### A21 · `cncf-glossary-continuous-delivery-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/continuous-delivery/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["cicd"]
---
# CNCF Glossary — Continuous Delivery

## What it is
"Continuous delivery, often abbreviated as CD, is a set of practices in which code changes are automatically deployed into an acceptance environment (or, in the case of continuous deployment, into production)."

## Distinguishing features
Continuous delivery "includes procedures to ensure that software is adequately tested before deployment", and provides "a way to rollback changes if deemed necessary".

CAPTURE NOTE: CNCF abbreviates BOTH continuous delivery and continuous deployment
as "CD". See cncf-glossary-continuous-deployment-2026-08-31.md.
```

### A22 · `cncf-glossary-continuous-deployment-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/continuous-deployment/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["cicd", "push-based-delivery"]
---
# CNCF Glossary — Continuous Deployment

## What it is
"Continuous deployment, often abbreviated as CD, goes a step further than continuous delivery by deploying finished software directly to production."

## Problem it addresses
"Releasing new software versions can be a labor-intensive and error-prone process... Traditional software deployment models leave organizations in a vicious cycle where the process of releasing software fails to meet organizational needs around both stability and feature velocity."

## How it helps
"By automating the release cycle and forcing organizations to release to production more frequently, CD does what CI did for development teams for operations teams... it forces operations teams to automate the painful and error-prone portions of production deployments, reducing overall risk."
```

### A23 · `argo-rollouts-experiments-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-rollouts.readthedocs.io/en/stable/features/experiment/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo Rollouts; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["progressive-delivery", "canary-deployment", "deployment-strategy-vocabulary"]
---
# Argo Rollouts — Experiments (and A/B testing)

"The Experiment CRD allows users to have ephemeral runs of one or more ReplicaSets."

On A/B testing: "A user can use experiments to enable A/B/C testing by launching multiple experiments with a different version of their application for a long duration."

On use within a canary rollout: "The experiment step serves as a blocking step for the Rollout, and a Rollout will not continue until the Experiment succeeds."

On traffic: "When Traffic Routing is enabled, the Rollout Experiment step allows traffic to be shifted to experiment pods."

CAPTURE NOTE — resolves the outline's Open Question 2. A/B testing is documented
here as a use of the Experiment resource, NOT as a rollout/deployment strategy
alongside RollingUpdate, Recreate, Blue-Green and Canary. The Canary strategy page
(https://argo-rollouts.readthedocs.io/en/stable/features/canary/) was checked
directly on 2026-08-31 and does not contain the string "A/B".
```

### A24 · `argo-rollouts-canary-2026-08-31.md` (new)
```markdown
---
source_url: "https://argo-rollouts.readthedocs.io/en/stable/features/canary/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo Rollouts; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["canary-deployment", "progressive-delivery", "deployment-strategy-vocabulary"]
---
# Argo Rollouts — Canary Deployment Strategy

"A canary rollout is a deployment strategy where the operator releases a new version of their application to a small percentage of the production traffic."

On traffic management: "The traffic management rules to apply to control the flow of traffic between the active and canary versions. If not set, the default weighted pod replica based routing will be used."

On header-based shaping: "You wish to scale the canary stack up minimally, and use some header based traffic shaping to the canary, while setWeight is still set to 0."

CAPTURE NOTE: the string "A/B" does not appear on this page. Verified 2026-08-31.
```

### A25 · `twelve-factor-iii-config-2026-08-31.md` (new)
```markdown
---
source_url: "https://12factor.net/config"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-iii-config-in-environment"]
---
# The Twelve-Factor App — III. Config

"An app's config is everything that is likely to vary between deploys (staging, production, developer environments, etc)."

"A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials."

On config files: "This is a huge improvement over using constants which are checked into the code repo, but still has weaknesses: it's easy to mistakenly check in a config file to the repo."

"The twelve-factor app stores config in environment variables (often shortened to env vars or env). Env vars are easy to change between deploys without changing any code; unlike config files, there is little chance of them being checked into the code repo accidentally."

On grouping into named environments: "This method does not scale cleanly: as more deploys of the app are created, new environment names are necessary, such as staging or qa."

"In a twelve-factor app, env vars are granular controls, each fully orthogonal to other env vars. They are never grouped together as 'environments', but instead are independently managed for each deploy."
```

### A26 · `twelve-factor-vi-processes-2026-08-31.md` (new)
```markdown
---
source_url: "https://12factor.net/processes"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-vi-stateless-processes"]
---
# The Twelve-Factor App — VI. Processes

"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service, typically a database."

"Sticky sessions are a violation of twelve-factor and should never be used or relied upon. Session state data is a good candidate for a datastore that offers time-expiration, such as Memcached or Redis."
```

### A27 · `twelve-factor-ix-disposability-2026-08-31.md` (new)
```markdown
---
source_url: "https://12factor.net/disposability"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-ix-disposability"]
---
# The Twelve-Factor App — IX. Disposability

"The twelve-factor app's processes are disposable, meaning they can be started or stopped at a moment's notice."

"Processes should strive to minimize startup time. Ideally, a process takes a few seconds from the time the launch command is executed until the process is up and ready to receive requests or jobs."

"Processes shut down gracefully when they receive a SIGTERM signal from the process manager."

"Processes should also be robust against sudden death, in the case of a failure in the underlying hardware."
```

### A28 · `twelve-factor-xi-logs-2026-08-31.md` (new)
```markdown
---
source_url: "https://12factor.net/logs"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-xi-logs-as-event-streams"]
---
# The Twelve-Factor App — XI. Logs

"Logs are the stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services."

"A twelve-factor app never concerns itself with routing or storage of its output stream."

"Each running process writes its event stream, unbuffered, to stdout."

"In staging or production deploys, each process' stream will be captured by the execution environment, collated together with all other streams from the app, and routed to one or more final destinations for viewing and long-term archival."
```

---

## Stage 2 summary

28 snapshots delivered. **Open Question 1's blocking gaps: four of five closed** — the `Application`/`AppProject` object model, automated sync policy with self-heal and prune, sync phases and waves, and the agent's identity and credentials all now have primary sources from the projects themselves. **Open Question 8 fully pinned:** self-heal and prune are both off by default; Flux's five minutes is a bootstrap default, not an API default, and the API requires an explicit interval. **Open Question 2 resolved:** A/B testing is sourced, but as an Experiment rather than a deployment strategy — which supports demoting rather than cutting it.

**Two gaps go forward to drafting and must not be filled from memory:** the push-side credential argument and the term "blast radius" (G-15-1), and Flux's multi-cluster topology (G-15-2). Both are flagged above with the nearest sourced alternative.
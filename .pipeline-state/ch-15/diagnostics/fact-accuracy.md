# Fact-Accuracy Audit — Chapter 15

**Mode detected: STANDARD.** The `Cached sources` block carries 37 populated snapshots, and the draft carries ~175 inline `[source: ...]` tags. Untagged factual claims are therefore FAIL.

**Draft audited:** `draft-v1.md` (`draft-v2.md` reported unavailable at this stage; the pipeline note directs the fallback). Because the draft was supplied to this stage without line numbering, locators below are **section-anchored** (`§N`, block name, paragraph) rather than line numbers. The revision stage should search on the quoted excerpt.

---

## Summary

- Total factual claims inspected: **~124 distinct** (≈175 tagged instances; the same claim restated in Soundings, a Bearings answer, the Exam Alert, the Traps table and a Practice answer is counted once)
- Tagged claims verified: **117**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — every snapshot named by a tag is present in the corpus
- **Untagged factual claims (FAIL): 8**
- **Contradicted claims (FAIL): 1**
- Minor discrepancies (WARN): **13**

Two corpus-level observations that shape the findings below:

1. `argocd-auto-sync-policy-2026-08-31` is **truncated at "Enabled declaratively:"** — it contains no example and no statement of defaults for `automated`, `selfHeal` or `prune`. `argocd-declarative-setup-2026-08-31` is likewise truncated at "A minimal Application manifest:". Any claim about auto-sync defaults or `Application` field names is uncheckable against this corpus.
2. `opengitops-principles-v1-2026-08-31` and `flux-security-2026-08-31` both carry capture notes stating explicitly that **no cached source discusses push-based versus pull-based delivery, agent placement rationale, or credential exposure outside the cluster.** §3 — the chapter's central argument — therefore rests on authored reasoning, not on the corpus. That is defensible reasoning, but it must be marked as such rather than read as sourced.

---

## FAIL — Untagged factual claims

### §1, opening paragraph: "published in 2011 and drawn from experience running a large number of applications on a shared platform" (and the consequence two paragraphs later, "it predates Kubernetes by three years")

**Why it's a factual claim:** A publication date and a provenance claim about a third-party methodology, plus an arithmetic comparison to Kubernetes's own release date. Both are checkable external facts.
**Corpus status:** `twelve-factor-app-2026-08-23` contains no date, no author attribution, and no statement about the number of applications or the platform the methodology came from. The snapshot begins at "In the modern era, software is commonly delivered as a service". Neither the 2011 date nor Kubernetes's 2014 date appears anywhere in the 37 snapshots.
**Fix:** Open a research gap for a snapshot that carries 12factor.net's authorship/date preamble (the "Background" section of 12factor.net, and/or `kubernetes.io/releases/` for the Kubernetes date). Until one exists, either drop the two sentences or reduce them to what the snapshot supports — the methodology predates Kubernetes and describes it closely — without asserting a year or an interval. Note that "three years" is doing rhetorical work in the paragraph that follows ("That is not coincidence and it is not prophecy"), so a bare deletion needs a small rewrite.

### "Why This Chapter Matters", penultimate paragraph: "this domain doubled, from 8% to 16%"

**Why it's a factual claim:** A statement about the weighting of a domain in a prior published version of the KCNA curriculum.
**Corpus status:** `cncf-kcna-curriculum-pdf-2026-08-23` gives the current split (44 / 28 / 16 / 12) only. No cached snapshot carries any earlier revision of the curriculum, so the 8% figure is unverifiable here.
**Fix:** The sentence attributes the fact to Chapter 1 ("The stakes here were banked in Chapter 1"). If Ch 1 carries a source tag for the 8% figure, mirror that tag here. If it does not, open a research gap for an archived copy of the pre-revision KCNA curriculum PDF (`github.com/cncf/curriculum` history) — this is exactly the kind of number that ages badly and gets quoted back at the author.

### §3, "The architectural question", four-consequence passage ("Where the credentials sit" / "What a compromise gets" / "What happens between deploys" / "What 'the truth' means")

**Why it's a factual claim:** Assertions about where credentials physically reside in each architecture, what an attacker obtains on compromise, and what runs between deploys. These read as sourced description; none of the four bullets carries a tag.
**Corpus status:** Two capture notes state that the corpus does *not* cover this ground: `flux-security-2026-08-31` ("neither the security page nor the security best-practices page discusses push-based versus pull-based delivery, agent placement rationale, or credential exposure outside the cluster") and `opengitops-principles-v1-2026-08-31` ("There is no FAQ document and no push-versus-pull comparison document in the OpenGitOps corpus").
**Fix:** Two of the four are derivable from cached material and should be tagged accordingly — credential location under pull from `argocd-security-cluster-credentials-2026-08-31` (credentials as a Secret in the `argocd` namespace), and "what happens between deploys" from principle 4 in `opengitops-principles-v1-2026-08-31`. The remaining two (compromise scope, "what the truth means") are authored analysis; mark them as the book's reasoning rather than leaving them in sourced-prose register, or open a research gap for a cached source that makes the push/pull security comparison directly.

### §3, "What a compromise gets": "The term for this is **blast radius**"

**Why it's a factual claim:** An attribution of terminology to the field. The term is then load-bearing — it recurs in TYB2 Q3, Practice Q10, the Safe Harbor list and the Chapter Summary.
**Corpus status:** No cached snapshot defines or even uses "blast radius". Two snapshots carry `blast-radius` in their `concepts_covered` frontmatter (`argocd-security-cluster-credentials-2026-08-31`, `flux-security-2026-08-31`), but neither body text contains the phrase. Frontmatter is indexing metadata, not evidence.
**Fix:** Either open a research gap for a source that defines the term (CNCF glossary has no such entry as of this corpus; a NIST or CNCF security-whitepaper snapshot would serve), or present it as the book's own vocabulary — "this book calls that the blast radius" — which is a form the chapter already uses successfully for **rollback by revert**.

### §4, "Doing something about it": "**Self-heal** is the term for the agent correcting drift it detects in the cluster rather than only responding to new commits."

**Why it's a factual claim:** A vendor feature name and its definition.
**Corpus status:** `argocd-auto-sync-policy-2026-08-31` is truncated before any mention of `selfHeal`. `cncf-glossary-gitops-2026-08-31` mentions "self-healing attributes" as a GitOps benefit but does not define an Argo CD feature by that name. The draft's own AUTHOR-REVIEW comment at this point correctly refuses to assert the *default*, but the definition itself is still stated untagged.
**Fix:** Open a research gap for the full `argo-cd.readthedocs.io/en/stable/user-guide/auto_sync/` page. That single fetch resolves three things at once: the self-heal definition, outline Open Question 8(a) on defaults, and the `prune` behaviour. Until then, the CNCF glossary tag can support "self-healing" as a *GitOps* property, but not as an Argo CD feature name.

### §5, closing paragraph: "RBAC bindings are immutable in their subject reference: you cannot retarget a binding, you must delete it and create a new one"

**Why it's a factual claim:** A statement about the mutability of a Kubernetes API field, used to justify the section's worked ordering example.
**Corpus status:** No cached snapshot covers RoleBinding/ClusterRoleBinding mutability. `k8s-docs-service-accounts-2026-08-23` is the only RBAC-adjacent snapshot and says nothing about it.
**This one needs more than a tag.** As worded the claim names the wrong field. The immutable field on a RoleBinding/ClusterRoleBinding is `roleRef` — the role the binding points *at* — while `subjects` can be edited in place. "Immutable in their subject reference" and "you cannot retarget a binding" therefore describe a constraint that does not exist in the form stated, and the delete-then-create ordering example is built on it. This must not pass unverified.
**Fix:** Open a research gap for `kubernetes.io/docs/reference/access-authn-authz/rbac/` (the "A RoleBinding or ClusterRoleBinding... you cannot change the Role or ClusterRole that it refers to" passage), then restate as: the binding's `roleRef` is immutable, so *changing which role a binding grants* requires delete-and-recreate. The ordering argument survives the correction intact — it just has to be about `roleRef`.

### §6, "More than one cluster": "Flux's answer is per-cluster: each cluster runs its own Flux... No cluster holds credentials to another."

**Why it's a factual claim:** A description of a vendor's multi-cluster architecture and an absolute statement about credential placement.
**Corpus status:** Nothing in `flux-concepts-2026-08-31`, `flux-components-2026-08-31`, `flux-kustomization-api-2026-08-31` or `flux-security-2026-08-31` addresses multi-cluster delivery. `flux-concepts-2026-08-31` describes bootstrap on a single cluster; `flux-security-2026-08-31` covers soft multi-*tenancy* (impersonation within one cluster), which is a different subject and should not be read across to multi-cluster.
**The absolute is the risk.** "No cluster holds credentials to another" is stated without qualification, and the corpus provides no basis for an absolute in either direction. See also the contradicted-claim entry below, which is the tagged twin of this sentence.
**Fix:** Open a research gap for `fluxcd.io/flux/installation/configuration/multi-tenancy/` or the Flux multi-cluster guide. Until cached, soften to what the corpus supports — Flux bootstraps per cluster (`flux-concepts-2026-08-31`) — and drop the credential absolute.

### "Why This Chapter Matters", Dead Reckoning block: "Argo CD and Flux are two implementations. Both are Kubernetes controllers."

**Why it's a factual claim:** A structural assertion about two named projects. The single tag on the block (`opengitops-principles-v1-2026-08-31`) covers the four principles that precede it, not these two sentences.
**Corpus status:** Supported, and cheaply fixed. `argocd-architecture-2026-08-31` states the application controller "is a Kubernetes controller"; `flux-concepts-2026-08-31` refers to "Flux Controllers".
**Fix:** Add both tags. Note that `flux-components-2026-08-31` carries a capture note forbidding behavioural attribution, so cite `flux-concepts-2026-08-31` for the Flux half, not the components page.

---

## FAIL — Contradicted claims

### Practice Questions, Q21 answer, final paragraph: "Flux's model is one Flux per cluster, each bootstrapped into its own repository or path and pulling independently, with no cluster holding credentials to another"

**Tag:** `[source: flux-concepts-2026-08-31]`
**Snapshot says:** The snapshot's four sections are GitOps Toolkit, Sources, Reconciliation, and Bootstrap. The bootstrap entry reads in full: *"The process of installing the Flux components in a GitOps manner is called a bootstrap. The manifests are applied to the cluster, a `GitRepository` and `Kustomization` are created for the Flux components, then the manifests are pushed to an existing Git repository (or a new one is created)."* The snapshot contains no statement about multiple clusters, no statement about per-cluster repositories or paths, and no statement about credential placement across clusters.
**Draft says:** "one Flux per cluster, each bootstrapped into its own repository or path and pulling independently, with no cluster holding credentials to another [source: flux-concepts-2026-08-31]"
**Recommended fix:** This is a mis-tag, not a paraphrase drift — the cited snapshot does not contain the claim in any form, and a reader following the tag would find nothing. Remove the tag and treat the sentence as blocked on the same research gap as the §6 prose above. What the snapshot *does* support, and all it supports, is that bootstrap installs Flux into a cluster against a Git repository. The contrasting Argo CD half of the same answer is correctly sourced (`argocd-overview-2026-08-23` for multi-cluster management, `argocd-security-cluster-credentials-2026-08-31` for the Secret in the `argocd` namespace) and can stand as written.

---

## WARN — Minor discrepancies

**1. §1, Factor III, para 4 — "cannot be accidentally committed" overstates the source.** The snapshot says env vars have *"little chance of them being checked into the code repo accidentally"* (`twelve-factor-iii-config-2026-08-31`). The draft converts a probability claim into an impossibility claim. Fix: "are far less likely to be committed by accident."

**2. §3, principle 4 discussion — the Drift definition is quoted as if complete.** The snapshot renders it *"When a system's actual state has moved or is in the process of moving away from the desired state..."* with a trailing ellipsis, and the capture note says explicitly: "treat the truncated definitions as partial and do not extend them from memory." The draft quotes it without the ellipsis, presenting a partial definition as the whole. Fix: retain the ellipsis, or attribute as "drift is, in part, ...". The Reconciliation quote alongside it is complete in the snapshot and needs no change.

**3. §3, Closer Look — "the requirements being principle 2's immutability and complete version history" resolves something the snapshot leaves open.** `opengitops-1-0-announcement-2026-08-31` quotes *"as long as they meet those two basic requirements"* without stating what the two are; the fetch did not capture the antecedent. The draft's inference is reasonable and almost certainly right, but it is an inference presented inside a sourced sentence. Fix: mark it as the book's reading ("the two requirements principle 2 names"), or cache the fuller announcement page.

**4. §6 — the "every five minutes by default" figure is stated without the qualification the corpus itself records.** `flux-concepts-2026-08-31` says *"The reconciliation runs every five minutes by default"*; `flux-kustomization-api-2026-08-31` carries a capture note stating that `.spec.interval` is **required with a 60-second minimum and no API-level default**, and that the five-minute figure describes Flux's bootstrap-generated Kustomization. Both snapshots are current (2026-08-31). The unqualified figure appears three times: §6 body, the Worth Securing block, and TYB3 Q4's answer ("within roughly five minutes"). The draft's own AUTHOR-REVIEW comment flags this; recording it here so the revision stage acts rather than defers. Fix: add the API-level qualification at the §6 body occurrence and let the two downstream uses inherit it.

**5. §6, controller table — the Source controller row is incomplete.** `flux-components-2026-08-31` lists seven custom resources for the source controller: GitRepository, OCIRepository, HelmRepository, HelmChart, Bucket, **ExternalArtifact, ArtifactGenerator**. The draft's table lists the first five. A table implies completeness by its form. Fix: add the two, or add "among others" to the cell.

**6. "Why This Chapter Matters" — "OpenGitOps is a CNCF project [source: opengitops-principles-2026-08-23]"; §3 repeats "it comes from OpenGitOps, a CNCF project".** The cited snapshot's authority line reads "OpenGitOps (CNCF **sandbox** project)"; the 2026-08-31 captures read "OpenGitOps (CNCF project; GitOps Working Group)". Not wrong, but the surrounding argument leans on CNCF standing ("Argo and Flux are both CNCF **graduated** projects"), and a reader who checks will find OpenGitOps at a different tier from the two projects named beside it. Fix: state the tier explicitly, or cite the 2026-08-31 capture whose framing the draft actually uses.

**7. Header note and "Why This Chapter Matters" — "no sub-topic list beneath it" is looser than the curriculum snapshot.** `cncf-kcna-curriculum-pdf-2026-08-23` reads: "16% – Cloud Native Application Delivery: **Application Delivery; Debugging**." CNCF does publish two competencies beneath the domain. The draft's claim is defensible read narrowly (no topics beneath the *competency* "Application Delivery"), but as phrased it invites the reading that the domain is unenumerated. Fix: "CNCF publishes two competencies under this domain — Application Delivery and Debugging — and no topic list beneath either." That is both more accurate and stronger, since it also justifies the Ch 16 handoff.

**8. §6, opening contrast — "Argo CD presents as an integrated application: one controller, one API, one web UI".** `argocd-architecture-2026-08-31` documents three components: API Server, Repository Server, Application Controller. The draft asserts this in §4 itself ("Rendering is not an add-on. It is a whole component"). Fix: "one integrated product, one `Application` resource, one UI" — which preserves the contrast with Flux's composability without understating the component count the chapter has already taught.

**9. ☆ Taking Your Bearings 2, Q2 answer — the second explanation is mislabelled, and contradicts the book's own Practice Q13.** The question asks for two explanations "only one of which involves anything going wrong." The answer labels *"Something did go wrong: a new commit landed in the tracked path and has not been applied yet."* But Practice Q13's answer says of the same scenario: "A and B produce `OutOfSync` with nothing failing," where B is verbatim "A new commit landed in the tracked path and has not been applied." An unapplied commit is normal operation, and the chapter says so twice elsewhere. Fix: make the second explanation an actual failure — a sync operation that failed on one resource, or a mutating admission controller rewriting an applied field — and keep the pending-commit case in the "nothing went wrong" column, which is where the rest of the chapter puts it.

**10. Retrieval answers restate Kubernetes facts owned by earlier chapters, untagged.** Not flagged as FAIL because the draft's convention is to attribute retrievals by chapter pointer (`*(Ch 3 §6)*`) and this chapter's corpus was assembled for D3.1, so the owning snapshots are legitimately absent. Recorded so the revision stage can confirm each fact is tagged in its owning chapter: Soundings answers 1–6 (control loop; `spec`/`status`; `RollingUpdate` semantics and `maxSurge`/`maxUnavailable`; CRD-without-controller; ServiceAccount + RBAC, incl. "permissions are additive, and there is no deny rule"; ConfigMaps/Secrets); TYB1 Q3 and Q4 (the 12-max / 9-available arithmetic — correct as computed); TYB2 Q4; TYB3 Q5. Also in this group: the field name **`.spec.strategy`** (TYB1 Q6, Practice Q6). No cached snapshot names that field — `argo-rollouts-strategies-2026-08-23` says only that RollingUpdate "is the default strategy of the Deployment object" — so the tag currently attached to those answers does not cover the field name itself.

**11. Practitioner-frequency generalizations stated in sourced register.** Three instances: §2 Worth Securing, "People choose blue/green over canary **far more often** for infrastructure reasons than for risk reasons"; "Why This Chapter Matters", "Practitioners who make this shift describe the same two feelings in sequence"; §3 Closer Look, "Git is the overwhelming practical choice." None is checkable against any source, and the first two are quantified. The *second* sentence of the Worth Securing block ("If there is no service mesh and no metrics pipeline... canary is not on the menu") is fully supported by `argo-rollouts-strategies-2026-08-23` and needs no change. Fix: mark the generalizations as the narrator's experience rather than reportage, which the brand voice supports directly.

**12. Attention Budget total does not match its own rows (internal, not source-related).** Listed section times sum to 100 minutes (8+10+12+6+15+15+5+8+8+5+8); the header states "Total time: ~85 minutes". Fix: reconcile the total to the rows, or the rows to the total.

**13. Out of remit, observed in passing — figure anchors and captions are transposed.** `<!-- FIGURE: ch15-fig05-opengitops-four-principles -->` is captioned **Figure 15.4**, and `<!-- FIGURE: ch15-fig04-argocd-sync-states-and-hooks -->` is captioned **Figure 15.5**. Anchor order and caption order disagree. This belongs to the structural/diagram-handoff stage, not to fact accuracy; recorded here only because it will otherwise reach the diagram pipeline as a mismatched contract.

---

## PASS — Verified claims

Sampled coverage evidence. Each of the following was compared word-for-word against the named snapshot and matched.

**Curriculum and ecosystem**
- Domain weight 16%, "Cloud Native Application Delivery" — `cncf-kcna-curriculum-pdf-2026-08-23`
- Argo and Flux as CNCF graduated projects; graduated described as "stable, widely adopted, and production ready" — `cncf-project-maturity-levels-2026-08-23`

**Twelve-factor (§1)**
- The methodology's own five-clause summary; all twelve factor names and one-line glosses in the table — `twelve-factor-app-2026-08-23`
- Config definition; the open-source litmus test; the config-file weakness; env vars as granular controls never grouped as "environments" — `twelve-factor-iii-config-2026-08-31`
- Stateless and share-nothing; sticky sessions banned by name — `twelve-factor-vi-processes-2026-08-31`
- Disposable processes; minimize startup time; graceful SIGTERM; robust against sudden death — `twelve-factor-ix-disposability-2026-08-31`
- Logs as time-ordered event streams; never concerns itself with routing or storage; unbuffered to stdout; execution environment captures and routes — `twelve-factor-xi-logs-2026-08-31`

**Deployment strategies (§2)**
- Progressive delivery definition; Recreate; RollingUpdate as Deployment default; Blue-Green; Canary; the canary-vs-blue/green cost comparison including "suits workloads such as queue workers" — `argo-rollouts-strategies-2026-08-23`
- Blue-green two-environment description, the "smell" assessment, and the whole-system/individual-service misapplication note — `cncf-glossary-blue-green-deployment-2026-08-31`
- Canary rationale ("no matter how thorough the testing strategy...") — `cncf-glossary-canary-deployment-2026-08-31`
- Operator-side canary definition — `argo-rollouts-canary-2026-08-31`
- A/B/C testing as a use of the Experiment CRD, not a rollout strategy — `argo-rollouts-experiments-2026-08-31` (the draft's §2 exclusion argument correctly follows this snapshot's capture note, which resolves outline Open Question 2)

**CI/CD and GitOps (§3)**
- "Does not deploy source code and does not build your application" — `k8s-docs-overview-2026-08-23`
- CI definition and "concrete failure or a viable release candidate" — `cncf-glossary-continuous-integration-2026-08-31`
- Continuous delivery definition — `cncf-glossary-continuous-delivery-2026-08-31`; continuous deployment "goes a step further" — `cncf-glossary-continuous-deployment-2026-08-31`; the shared-"CD" ambiguity Snag is directly supported by the first snapshot's capture note
- All four principles, quoted verbatim in §3, restated in §7, the Exam Alert and the Traps table — `opengitops-principles-v1-2026-08-31`
- "Software agents automatically pull..."; "The wording of each principle... very carefully chosen"; "many version control systems can be used in GitOps" — `opengitops-1-0-announcement-2026-08-31`
- Reconciliation definition — `opengitops-glossary-2026-08-31`
- Drift named first among GitOps problems; "hard to detect and resolve without a source of truth governing it" — `cncf-glossary-gitops-2026-08-31`

**Argo CD (§4, §5)**
- "Declarative, GitOps continuous delivery tool"; the five manifest-source kinds; `OutOfSync` definition; reports-and-visualizes; drift detection and manual-or-automatic sync in the feature list; PreSync/Sync/PostSync hooks supporting blue/green and canary; rollback/roll-anywhere; multi-cluster management — `argocd-overview-2026-08-23`
- Application controller as "a Kubernetes controller which continuously monitors..."; repository server cache and manifest generation — `argocd-architecture-2026-08-31`
- Application, target state, live state, sync status, sync, refresh, tool, application source type, configuration management plugin; sync status vs sync **operation** status as separate entries — `argocd-core-concepts-2026-08-31`
- Application CRD; source (repository, revision, path, environment) and destination (cluster, namespace) — `argocd-declarative-setup-2026-08-31`
- Branch/symbolic-reference, tag, and pinned-commit tracking, incl. "commit SHAs cannot change meaning" — `argocd-tracking-strategies-2026-08-31`
- "Not a stable target... can suddenly change meaning"; "A better version would be to use a Git tag or commit SHA" — `argocd-best-practices-2026-08-31`
- "`OutOfSync` even immediately after a successful Sync operation" — `argocd-diffing-outofsync-2026-08-31`. The draft correctly declines to name causes, per that snapshot's capture note; its AUTHOR-REVIEW comment records the resulting weakness accurately.
- Automated sync capability — `argocd-auto-sync-policy-2026-08-31`
- clusteradmin default with the two numbered reasons; cluster-wide read required, full write not; `argocd-manager-role` narrowing; external-cluster credentials as a Secret in the `argocd` namespace with the `argocd-manager` bearer token — `argocd-security-cluster-credentials-2026-08-31`
- Four phase definitions; wave annotation and integer value; wave 0 default and negative waves; the four-step ordering algorithm — `argocd-sync-phases-and-waves-2026-08-31`
- ServiceAccount use case "an external service needs to communicate with the Kubernetes API server (CI/CD pipelines)" — `k8s-docs-service-accounts-2026-08-23`

**Flux (§6)**
- GitOps Toolkit definition (2026-08-31 wording) and the earlier 2026-08-23 wording, each attributed to the correct capture — `flux-concepts-2026-08-31` / `flux-concepts-2026-08-23`
- Source definition; five-minute reconciliation with `.spec.interval`; `kubectl edit/patch/delete` promptly reverted; bootstrap description — `flux-concepts-2026-08-31`
- "Flux manages itself like any other resource" — `flux-concepts-2026-08-23`
- Kustomize / Helm / Notification / Image controller custom-resource rows — `flux-components-2026-08-31`
- Kustomization API "defines a pipeline for fetching, decrypting, building, validating and applying"; `.spec.serviceAccountName` impersonation — `flux-kustomization-api-2026-08-31`
- `crd-controller` ClusterRole; `cluster-reconciler` ClusterRoleBinding bound to kustomize-controller and helm-controller only, with the stated reason; soft multi-tenancy impersonation under `cluster-admin` — `flux-security-2026-08-31`

---

## Recommended additions to the research manifest

Five fetches close every unverifiable finding above, in rough order of value:

1. **`argo-cd.readthedocs.io/en/stable/user-guide/auto_sync/` (full page).** Resolves the self-heal definition (FAIL 5), the `selfHeal`/`prune`/`automated` defaults, and outline Open Question 8(a). The current snapshot is truncated mid-page.
2. **`kubernetes.io/docs/reference/access-authn-authz/rbac/`.** Required before §5's binding-immutability sentence can ship in any form (FAIL 6) — the claim as written names the wrong field.
3. **`fluxcd.io` multi-cluster / multi-tenancy guide.** Closes FAIL 7 and the contradicted Q21 answer, which are the same claim in two places.
4. **12factor.net "Background" section** (authorship and date) and a dated Kubernetes release reference. Closes FAIL 1.
5. **Archived pre-revision KCNA curriculum PDF** from `github.com/cncf/curriculum` history. Closes FAIL 2 — and is worth caching for Chapter 1 regardless, since that chapter appears to be where the 8% figure originates.

Also worth re-fetching, though nothing currently FAILs on it: **`argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/`**, which is truncated at "A minimal Application manifest:" and so cannot support any claim about `Application` field names.
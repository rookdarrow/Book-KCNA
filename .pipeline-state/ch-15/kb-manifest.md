I verified the integration report's two headline "fixes" against the corpus rather than acting on them. One is correct and cheap; **the other would propagate a known miscitation into a third chapter**, and Chapter 14's Stage 14 already ruled against it. I also found a reader-facing tag drift that no prior stage caught.

# Knowledge-Base Manifest — KCNA Chapter 15

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice, carried forward and re-verified directly.** `Book-KCNA/knowledge-base/` **still does not exist on disk** — checked, not inherited. Fourteen manifests exist (`ch-01` … `ch-14`); none has been applied. Chapter 15 adds the fifteenth.
>
> **Ordering contract, inherited unchanged from Ch 12–14.** **APPEND** for the three shared registers and for every shard that already exists; **WRITE** only for filenames that collide with nothing. I enumerated all `=== WRITE …/concepts/*.md ===` blocks across `ch-01`–`ch-14`: **158 distinct shard slugs** exist. All 31 new Ch 15 slugs were checked against that set — **no collisions**. Chapter 15 introduces **no new full-file WRITE to a shared register**, so ⚑ I1's blast radius is unchanged.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

Two tiers, following Ch 11–14. The integration report marked **8 terms** as needing entries; skill Part 16 requires every technical term the book introduces, so the **23 B7-owned Chapter 15 rows** (`term-ownership.md:477–503`) are harvested alongside them, plus six terms Chapter 15 introduces that the ledger does not assign at all.

### Tier 1 — entries whose definition is unsourced, provisional, orphaned, or authored

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **Argo Rollouts** | *Never defined.* Named once — *"**Argo Rollouts** states the same idea from the operator's side"* — after four prior "Argo's description / Argo's comparison" shorthands ⚠ **ZERO self-definition in the corpus**, verified across all three `argo-rollouts-*` snapshots | Chapter 15 §2 |
| **Progressive delivery** | *"the process of releasing updates of a product in a controlled and gradual manner… typically coupling automation and metric analysis to drive the automated promotion or rollback"* `[source: argo-rollouts-strategies-2026-08-23]` — ⚠ **sourced but has no ledger row**, and it is graded directly (Practice Q7) | Chapter 15 §2 |
| **Blast radius** | *"how far the damage from a single compromise extends"* — ⚠ **authored, and the answer key overclaims it.** See ⚑ C8 | Chapter 15 §3 |
| **Push-versus-pull as a security posture** | The four consequences (credential location, compromise reach, between-deploy behaviour, what "the truth" means) — ⚠ **the chapter's own reading**, explicitly declared as such in §3, in TYB2 Q3's key and in Q10's key. Correctly handled; recorded so no later stage promotes it to a documented finding | Chapter 15 §3 |
| **Jsonnet** | *Never glossed.* Appears only inside the quoted manifest-source list — ⚠ but reaches **Q14's answer key** and the **Common Traps** table | Chapter 15 §4 |
| **Kubernetes Impersonation API** | Named and sourced (`flux-security-2026-08-31`), ⚠ **not defined**; no ledger row | Chapter 15 §6 |
| **Soft multi-tenancy** | ⚠ Appears **only inside a Flux quotation**, never glossed. Either gloss it or drop the phrase | Chapter 15 §6 |
| **`OutOfSync` causes** | The chapter states *"it is possible for an application to be `OutOfSync` even immediately after a successful Sync operation"* `[source: argocd-diffing-outofsync-2026-08-31]` and names **no cause** — ⚠ correctly, because that snapshot's capture note forbids attributing its enumerated causes. The draft's AUTHOR-REVIEW is accurate; **verified against the snapshot** | Chapter 15 §4 |
| **"OpenGitOps is a CNCF project"** | ⚠ Tagged to `opengitops-principles-v1-2026-08-31`, which supports it only in its `authority:` **metadata field**, not in body text. `domain-analysis.md:262` says "CNCF **sandbox** project"; the chapter's weaker claim is the safer one and should stand — but the tag is thin | Chapter 15, Why This Chapter Matters |
| **"This domain doubled"** | ⚠ **UNTAGGED, and asserts an unsourceable figure.** See ⚑ C1 — the fix is deletion, not restoration | Chapter 15, Why This Chapter Matters |

**I verified the two highest-severity items independently rather than accepting the integration report's reading, and they resolve in opposite directions.** Item ⚑ C1 inverts the report's recommendation. Item ⚑ C2 confirms it.

### Tier 2 — the 23 ledger rows plus 6 unassigned terms, harvested per skill Part 16

Twelve-factor app · factor III (config in the environment) · factor VI (stateless processes) · factor VIII (concurrency) · factor IX (disposability) · factor XI (logs as event streams) · deployment strategy · `Recreate` · `RollingUpdate` (vocabulary only; mechanics stay Ch 6 §4) · blue/green deployment · canary deployment · A/B testing · progressive delivery · CI · CD (delivery) · CD (deployment) · push-based delivery · pull-based delivery · GitOps · the four OpenGitOps principles · blast radius · Argo CD · `Application` · application source type · tool · configuration-management plugin · repository server · source of truth · target state · live state · sync · refresh · sync status · sync operation status · `Synced` · `OutOfSync` · self-heal · prune · drift · reconciliation · tracking revision (branch / tag / pinned commit) · rollback by revert · delivery-agent identity · `PreSync` / `Sync` / `PostSync` / `SyncFail` · sync wave · `argocd.argoproj.io/sync-wave` · Flux · GitOps Toolkit · Flux controller set · Source (Flux) · `Kustomization` · `HelmRelease` · bootstrap · impersonation · multi-cluster delivery.

**Six terms Chapter 15 introduces that the ledger does not assign:** progressive delivery · repository server · sync operation status · prune · Jsonnet · Kubernetes Impersonation API.

---

## Concept shards at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/{slug}.md`

**Thirty-one created.** Slugs are aligned to the outline's `kb_tags.concepts` list wherever a shard is warranted, so the concept index and the shard tree cannot drift apart. Three consolidations follow the `oomkilled-vs-evicted.md` / `tag-vs-digest.md` / `headless-and-selectorless-services.md` precedent — *the discrimination is the content*.

| Slug | § | Note |
|---|---|---|
| `twelve-factor-app.md` | §1 | the twelve, the three-column sort, the platform/application Fixed Point |
| `factor-iii-config-in-environment.md` | §1 | the litmus test; the "not a config file" correction; no grouped environments — graded 3× |
| `factor-vi-stateless-processes.md` | §1 | share-nothing; sticky sessions banned by name; StatefulSet as the exception |
| `factor-ix-disposability.md` | §1 | fast up / clean down / survive the floor dropping |
| `factor-xi-logs-as-event-streams.md` | §1 | unbuffered stdout; why `kubectl logs` needs no configuration |
| `deployment-strategy-vocabulary.md` | §2 | ★ the field-values-vs-patterns line — **absorbs `recreate-strategy` and the A/B ruling** |
| `blue-green-deployment.md` | §2 | two environments; CNCF's "smell" assessment, which most vendor material omits |
| `canary-deployment.md` | §2 | traffic proportion + the infrastructure precondition |
| `progressive-delivery.md` | §2 | ⚠ no ledger row; graded once |
| `argo-rollouts.md` | §2 | ⚑ **orphan stub.** Created for the reason ch-08 created `auditing.md`: under the bar, but nothing else owns it |
| `cicd.md` | §3 | three practices, two of them abbreviated identically |
| `push-versus-pull-delivery.md` | §3 | **consolidates `push-based-delivery` + `pull-based-delivery`**; carries the sourced/authored split |
| `blast-radius.md` | §3 | ⚑ see C8 |
| `gitops.md` | §3 | the CNCF and OpenGitOps definitions, both quoted |
| `opengitops-four-principles.md` | §3 | verbatim four — **absorbs the four per-principle kb_tags** |
| `source-of-truth.md` | §3 | ⚠ the misreading: Git does **not** replace etcd |
| `drift-detection.md` | §3–§4 | ⚑ ledger says §4; the chapter defines it in §3. See C6 |
| `argo-cd.md` | §4 | ★ *"is a Kubernetes controller"* — the three-claim reading |
| `argo-cd-application-resource.md` | §4 | a source reference and a destination reference; that is the whole contract |
| `manifest-source.md` | §4, §6 | the five Argo CD sources + the repository server; Flux's `Source` API |
| `synced-outofsync.md` | §4 | ★ drift signal, not error — **absorbs target state, live state, sync, refresh, sync operation status** |
| `self-heal.md` | §4 | ⚠ both self-heal and prune are opt-in; the 120s + 60s jitter |
| `tracking-branch-tag-commit.md` | §4 | branch moves · tag rarely moves · commit never moves |
| `rollback-by-revert.md` | §4 | the third mechanism to wear the word; no second code path |
| `delivery-agent-identity.md` | §4 | ⚠ clusteradmin by default; commit access **is** cluster access |
| `sync-hook-phases.md` | §5 | four phases, gated on success; PostSync's health gate |
| `sync-wave.md` | §5 | relative ordering, default 0, negatives allowed |
| `flux.md` | §6 | composable toolkit; self-bootstrap; **the opposite drift default** — absorbs `flux-bootstrap` |
| `flux-controller-set.md` | §6 | the controller/CRD table, roster-not-inventory caveat intact |
| `multi-cluster-delivery.md` | §6 | ⚑ carries the do-not-over-claim-Flux warning |
| `control-loop-pointed-at-a-repository.md` | §7 | **the Zenith.** Own file, per Ch 14's `package-not-template.md` precedent |

**Thirty-three amended by append.** Chapter 15's ratio inverts Chapter 14's back toward Chapter 13's, and that is the chapter working correctly: a synthesis chapter should mostly be *extending* what already exists.

- `control-loop.md` (ch-03) — ⚑⚑ **the single most important append in the book.** Carries the Zenith and the no-ordinal rule
- `status.md` (ch-04) — ⚑ **the strongest append in this chapter.** Ch 4's shard already carries *"a gap is not a fault"*; `OutOfSync` is that rule at book scale
- `spec.md` (ch-04) — the authored `spec`, relocated outside the cluster
- `declarative-configuration.md` (ch-04) — principle 1 is Chapter 4 with nothing added
- `api-server-hub.md` (ch-03) — the agent is an ordinary API client; Ch 3's claim is not suspended
- `api-access-gates.md` (ch-08) — authn → authz → admission apply to the agent unchanged
- `absent-component-pattern.md` (ch-03/10/11) — ⚑ **good news, see C9**
- `custom-resource.md` (ch-06) — `Application` as a CRD; registration ≠ action
- `operator-pattern.md` (ch-06) — a controller acting on custom resources, aimed somewhere unexpected
- `serviceaccount.md` (ch-05) — the k8s-docs line naming CI/CD pipelines as a reason non-human identity exists
- `serviceaccounts-and-identity.md` (ch-12) — the same, from the RBAC side
- `rbac.md` (ch-12) — ⚑ **the `roleRef` immutability ordering example belongs here — see C2**
- `additive-never-deny.md` (ch-12) — retrieved verbatim in Soundings A5; pointer-only
- `secret.md` (ch-04) — external-cluster credentials as an ordinary Secret
- `secret-exposure-and-hardening.md` (ch-12) — the credential-location half of §3's argument
- `namespace.md` (ch-04) — the `argocd` namespace as a credential store; cross-namespace scope
- `configmap.md` (ch-04) — factor III's Kubernetes form, named as such
- `pod-lifetime.md` (ch-05) — scheduled once, replaced never, now underwriting factors VI and IX
- `probe.md` (ch-05) — PostSync's *Healthy* gate; pointer-only
- `helm-chart.md` (ch-14) — ⚑ **B6 mandatory anchor discharged**
- `kustomize.md` (ch-14) — ⚑ **second half of that anchor discharged**
- `base-and-overlay.md` (ch-14) — Flux's Kustomize controller consumes overlays
- `chart-repository.md` (ch-14) — `HelmRepository` as one Flux source kind
- `helm-rollback-versus-rollout-undo.md` (ch-14) — the third mechanism completes the set
- `helm-release-revision.md` (ch-14) — ⚑ "revision" is now **three** senses deep
- `crds-in-charts.md` (ch-14) — the CRD-before-CR rule restated as a sync wave
- `distribute-versus-adapt.md` (ch-14) — the delivery agent renders both, which reframes the choice
- `package-not-template.md` (ch-14) — Ch 14's Zenith collects: the package now has somewhere to go
- `oci.md` (ch-02) · `registry.md` (ch-02) — `OCIRepository` as a first-class Flux source
- `published-vs-commonly-reported.md` (ch-01) — ⚑⚑ the chapter's ethics discipline, and the C1 ruling
- `domain-weights-44-28-16-12.md` (ch-01) — ⚑⚑ **third chapter now: do not restore the 8% claim**
- `blueprint-change-2025-11-24.md` (ch-01) — where the "doubled" claim actually lives

Not shard-worthy, adequately carried by the glossary: application source type · tool · configuration-management plugin · Jsonnet · `SyncFail` · `HelmRelease` · `ImageUpdateAutomation` · soft multi-tenancy · impersonation.

---

## ⚑ Contradictions and conflicts — flagged, not resolved

Rule 6 requires these loud. **The integration report's two headline recommendations resolve in opposite directions, and one of its top-five fixes is unexecutable as written.**

### ⚑ C1. HIGH — do **not** apply Recommended Fix #1. Restoring the 8% figure would put a known miscitation in a third chapter.

The integration report states: *"That is checking the wrong snapshot… the prior weights are in the Linux Foundation program-changes page, which is cached."* I read that snapshot. It says the opposite, in a block placed at the top of the file for exactly this purpose:

> *"CORRECTION 2026-08-23: the previous capture of this page listed the retired five-domain weights (46/22/16/8/8) as if sourced here. Targeted re-fetch confirms **THE PAGE DOES NOT DISPLAY THE PREVIOUS DOMAIN STRUCTURE OR WEIGHTS.** Those figures have been removed from this snapshot."* — `lf-kcna-program-changes-2026-08-23.md:11–15`

and closes: *"## Not stated on this page — No question count, no passing score, no duration, and **no retired-blueprint weights**."* (`:44`)

The snapshot it redirects to now exists, and it is still an open gap:

> *"The retired domain weights are **NOT recorded in this snapshot** because the research stage could not extract the PDF's text… **DO NOT draft the retired weights from memory or from third-party study guides.**"* — `cncf-curriculum-repo-kcna-versions-2026-08-23.md:36–44`

**Chapter 14's Stage 14 already ruled on this (its ⚑ C1) and reached the same conclusion.** Shipped `chapter-01:274` cites `lf-kcna-program-changes-2026-08-23` for a figure that snapshot explicitly disclaims. The only corpus file carrying `8%` for this domain is `provenance-kcna-60-questions-2026-08-23.md`, headed **"DO NOT CITE THE CONTENTS OF THIS FILE AS FACT."**

**But the integration report is right about the ethical half, and that half is real.** The draft currently reads *"this domain doubled in the 2025-11-24 blueprint revision"* with no tag. "Doubled" asserts the prior weight was 8% exactly as writing "8%" would. Under `style-decisions.md`'s fact-accuracy rule, an untagged factual claim is an audit failure — so the sentence as it stands is *worse* than the version that was cut, because it makes the same claim with the tag stripped off.

**The fix is deletion, not restoration.** Both of these are sourced and both preserve the rhetorical beat:

- *"Cloud Native Application Delivery – 16%"* `[source: lf-kcna-program-changes-2026-08-23]`
- *"The KCNA domains… will remain mostly unchanged except that observability will be rolled under Cloud Native Architecture"* `[source: lf-kcna-program-changes-2026-08-23]`

Recommended replacement: *"this domain carries 16% of the exam, and the 2025-11-24 revision rolled Observability under Cloud Native Architecture rather than leaving it a domain of its own [source: lf-kcna-program-changes-2026-08-23]."* Then delete the AUTHOR-REVIEW comment. **The correction Chapter 1 needs is Chapter 1's, and it should not be propagated forward to make three chapters consistent in the same error.**

### ⚑ C2. HIGH — Recommended Fix #2 is confirmed. Restore the §5 example; the source and the shipped wording both hold.

Verified independently and both halves check out:

> *"After you create a binding, you cannot change the Role or ClusterRole that it refers to."* — `k8s-docs-rbac-2026-08-23.md:17`

> *"**And a binding cannot be retargeted.** …If a RoleBinding points at the wrong role, you delete it and create a new one… under a system that reconciles a cluster against a repository, a delete-and-create rather than an update. *[cross-bearing: see Ch 15 §5 — ordering the sync]*"* — `chapter-12-locks-keys-and-watchstanders.md:866`

The revision stage's diagnosis was right on substance — the immutable field is the role reference, not `subjects` — and shipped Ch 12 already words it correctly. So the corrected example can be restored exactly as the AUTHOR-REVIEW specifies, and **it must be**, because Chapter 12 emits a forward pointer into §5 on the strength of it. A reader following that pointer currently lands on *"it is a good illustration of why ordering is not a theoretical concern"* followed by no illustration.

### ⚑ C3. HIGH — the cross-domain tag has a **third** surface form, and no prior stage caught it.

I grepped every tag across all fourteen shipped chapters. The interleave tag has exactly two shipped forms — and Chapter 15 proposes a third:

| Chapter | Form | Status |
|---|---|---|
| Ch 13 (shipped) | `[interleaved: D1.3 scheduling]` — with topic word | shipped |
| Ch 14 (shipped) | `[interleaved: D1.1]` — bare | shipped; Ch 14's manifest ⚑ C7 asked for the topic word and **was not applied** |
| **Ch 15 (draft)** | **`[cross-domain: D2.2]`** — different keyword entirely | **new** |

The integration report checked these tags for *accuracy* (correct: Q16→Ch 12 §3, Q17→Ch 4 §2) and did not check them for *form*. Three surface forms across three consecutive chapters is drift, and it is reader-facing — these strings print.

**Recommendation, and it is a book-level call rather than a Chapter 15 one:** ratify `[interleaved: DN.N topic]` (Ch 13's form, the only one whose legibility survives the fact that `domain-analysis.md:33` records the D-numbering as *"a **Lodestar convention**"* CNCF does not publish). Then fix Ch 14 and Ch 15 together in one sweep: `[interleaved: D2.2 security]` and `[interleaved: D1.1 core concepts]`. Doing it per chapter has now failed twice.

### ⚑ C4. MEDIUM — Recommended Fix #4 is right about the problem and **cannot be executed as stated**.

The integration report's Argo Rollouts finding is correct and important: §2 says "Argo" five times before §4 introduces "Argo CD," and a reader will fuse them. Its proposed one-clause fix, however, needs a definition the corpus does not contain. I checked all three snapshots:

| Snapshot | Defines what Argo Rollouts *is*? |
|---|---|
| `argo-rollouts-strategies-2026-08-23` | no — opens at "Progressive delivery is…" |
| `argo-rollouts-canary-2026-08-31` | no |
| `argo-rollouts-experiments-2026-08-31` | no — "The Experiment CRD allows users to…" |

**Two clean routes, second one free.**

1. Fetch `argo-rollouts.readthedocs.io/en/stable/` for a one-sentence self-description. Cheap, and it also closes B1 gap G9's remaining edge.
2. **Introduce it through the maturity roster instead, which is already sourced.** `cncf-project-maturity-levels-2026-08-23:14` lists the graduated project as **"Argo"** — the umbrella, not "Argo CD." So: *"Argo Rollouts — a separate controller in the same Argo project as §4's Argo CD, and one concrete instance of the tooling this section says these patterns require."* Every clause there is supportable: the umbrella name from the roster, the separation from the two snapshots' distinct `source_url`s and authority fields.

Route 2 also discharges shipped Ch 6's promise of *"blue/green, canary, and A/B, and **the tooling that implements them**"* (`chapter-06:665`), which §2's Fixed Point currently asserts without ever naming an instance.

### ⚑ C5. MEDIUM — the Practice pool carries **zero** `[retrieval:]` tags for the third consecutive chapter.

| Chapter | Bearings retrieval | Practice retrieval | Verdict |
|---|---|---|---|
| Ch 13 | present | 0 (3 × `[interleaved:]`) | flagged in ch-13's manifest |
| Ch 14 | 2 of 10 | 0 (3 × `[interleaved:]`) | flagged in ch-14's manifest ⚑ C7 |
| **Ch 15** | **4 of 16 = 25%** | **0 of 21** (2 × `[cross-domain:]`) | **third occurrence** |

Chapter 15 is one of B3's five chapters at the **25% ceiling**. Its Bearings hit it exactly. Its Practice pool reads as 0% to any mechanical audit that greps `[retrieval:`, despite Q16 and Q17 carrying genuine backward reach to Ch 12 and Ch 4. **Chapter 19 is built by exactly such an audit.**

Cheapest fix, no new questions, and it combines with ⚑ C3: dual-tag Q16 → `[retrieval: ch12]` `[interleaved: D2.2 security]` and Q17 → `[retrieval: ch4]` `[interleaved: D1.1 core concepts]`. That puts Practice at 2/21 = 9.5% and the chapter at 6/37 = **16.2%** — still under the 25% target but no longer reading as a structural zero. Three chapters make this a book-level fix, not a per-chapter one.

### ⚑ C6. MEDIUM — two ledger rows the draft does not honour, both defensibly

**A/B testing** (`term-ownership.md:486`, `section-skeleton.md:223`, acronym register `:653`, and shipped `chapter-06:665`) is assigned to Ch 15 §2 as one of five strategies. The draft names it, sources it, and bounds it correctly — under a heading announcing **"One term this book will not teach you."** The substance is right: `argo-rollouts-experiments-2026-08-31`'s capture note resolves this explicitly, stating A/B is documented *"NOT as a rollout/deployment strategy alongside RollingUpdate, Recreate, Blue-Green and Canary."* The framing is what collides — with three contracts and one shipped promise a reader arrives holding.

*Fix: retitle to "One term that belongs somewhere else," open by discharging Ch 6's promise explicitly, and amend the ledger row to read "named and bounded, not taught as a release strategy." No content change.*

**Drift** (`term-ownership.md:497`) is assigned to Ch 15 §4. The draft defines it in **§3** via OpenGitOps' glossary and does detection in §4. **The draft's arrangement is better** — drift is what principle 4 exists to catch, so it belongs with the principles. *Amend the row to `§3 (definition) / §4 (detection)`; do not move the chapter.*

### ⚑ C7. MEDIUM — the question inventory exceeds B4 by six, all in Bearings

| | B4 budget (`length-budget.md:65`) | Actual | Verdict |
|---|---|---|---|
| Soundings | 8 | 8 | ✅ |
| Taking Your Bearings | 10 | **16** (6 · 5 · 5) | ⚑ +6 |
| Practice | 21 | 21 | ✅ |
| **Chapter total** | **39** | **45** | ⚑ +6 |

Above the skill's per-chapter floor (10 minimum, ≥2 checkpoints of ≥5) and above the book's budget. Not a defect — the third checkpoint exists to gate §7's retrieval, which is load-bearing — but the B4 arithmetic should be updated rather than left silently wrong, since the 715-question book total is computed from it.

### ⚑ C8. LOW — "blast radius" is standard security vocabulary, and one answer key overclaims it

§3 words this carefully: *"This book calls that reach the **blast radius**"* — a claim about the book's usage, which is fine. **Q10's answer key hardens it:** *"Blast radius is **this book's term** for how far the damage from a single compromise reaches."* It is not the book's term; it is widely used in security engineering. What *is* the book's is the push-versus-pull argument the term carries, and the chapter is scrupulous about saying so everywhere else.

*Fix: "this book's shorthand" in Q10, or drop the possessive. One word.* The B7 row (`:491`) should say the same, so a later chapter does not inherit the overclaim.

### ⚑ C9. GOOD NEWS — Chapter 15 neither repeats Ch 13's drift nor re-fights it

Ch 13's manifest raised a canon conflict: shipped Ch 13 retrieves the absent-component pattern by the **ledger** string rather than the **shipped Ch 10** string that four graded options depend on. Ch 14 used Ch 10's form. **Chapter 15 quotes neither** — §4 closes with *"An `Application` on a cluster with no Argo CD controller is a stored document. It describes a deployment that will never occur,"* pointing at Ch 10 §3 rather than restating any canonical string. That is the correct move for a chapter that is applying the pattern rather than defining it, and it means the drift stays confined to Chapter 13. Recorded for the Ch 17 §4 collection stage, which meets the whole thread at once.

### ⚑ C10. HIGH, escalated not re-reported — the Zenith figure pair

Image-specs caught it; the draft carries it; the integration report escalated it with three shipped promises. I add the fourth and strongest: **the BINDING B6 contract states the requirement directly.**

> §7 *"re-presents `ch03-fig02` with Git substituted for etcd as the desired-state store. **Owns no new material — the payoff is recognition, and it fails if the figure does not visually rhyme with Ch 3 §6's**."* — `section-skeleton.md:228`

Against three shipped chapters staking the book's payoff on it (`chapter-06:1465`, `chapter-09:1249`, Ch 14's Voyage Ahead), and a caption that asks the reader to lay the two side by side and see that one box changed. As drawn, they are not the same drawing. **Of the three resolutions, redrawing `ch03-fig02` onto this chapter's chassis is the only one that preserves what four contracts have promised.** It costs a Chapter 3 edit. That is a cheap price for the book's designated primary Zenith, and it is the single highest-risk open item in the chapter.

---

## Infrastructure flags — the knowledge base itself

**⚑ I1 — HIGH, unchanged and now fifteen chapters expensive.** Chapters 03, 10 and 11 emit full **WRITE** blocks for `glossary.md`, `objective-coverage.md` and `retrieval-log.md`; `absent-component-pattern.md` is written as a full file **three separate times** (ch-03, ch-10, ch-11). Replaying `ch-01` → `ch-15` in order therefore discards everything written before each of those points. Chapter 15 adds only APPENDs. **Convert those WRITE blocks to APPENDs before any replay.** Mechanical, and appends cannot clobber.

**⚑ I2 — MEDIUM, unchanged.** `concepts/pluggable-interface-pattern.md` (ch-02) and `concepts/pluggable-interfaces.md` (ch-11) are one concept under two slugs. Chapter 15 touches neither. **Merge at the replay, leaving a stub**, before Ch 17 §4 reads one file and concludes it has the set.

**⚑ I3 — LOW, unchanged and now blocking a third thing.** `.pipeline-state/book-outline/retrieval-architecture.md` is still 19 lines of permissions-failure message plus the stage's own summary; the B3 document was never written. Everything I cite from B3 above — the 25% ceiling for Ch 15, the ≥4-chapters-back spacing floor, the must-not-retrieve list — is recovered from that summary. **Re-run before Ch 19.** It now also holds the only statement of the rule that would have caught ⚑ C1 (*"the unpublished 60-question/75% figures"* are on its must-not-retrieve list, and the 8% comes from the same non-authoritative snapshot).

**⚑ I4 — LOW, new.** `kb_tags.commands` is `[]` by design, and the outline's note defends that well. But the draft demonstrates **`git revert`** in §4's prose and names the **`argocd.argoproj.io/sync-wave`** annotation in §5. The outline flagged `git revert` as the single plausible exception. *Add `git-revert` to `kb_tags.commands`; leave the annotation out, since §5 explicitly tells the reader not to memorize it.*

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Naming what the chapter costs the reader** | "This chapter asks you to become someone who *maintains a claim about what a cluster should contain*, and then never touches the cluster again. **That is genuinely uncomfortable, and it should be said plainly rather than sold.** Thirteen chapters of your growing competence have been measured in `kubectl` fluency… In my experience, practitioners who make this shift describe the same two feelings in sequence: first that it is slower, then that they cannot go back." | **Strong candidate.** The catalog has nothing that concedes a chapter's *cost* before selling its benefit. "Said plainly rather than sold" is the brand's anti-marketing instinct made explicit, and the two-feelings close earns the seasoned-navigator register without a nautical word in sight. |
| **Zenith / synthesis** | "This section teaches nothing new. **That is not modesty and it is not a warning; it is the design.** … Now move it. Take the desired state out of etcd and put it in a Git repository. … **One box changed contents. That is the entire technical delta between 'Kubernetes' and 'GitOps.'**" | **Strong candidate.** Opens by disclaiming novelty, then performs a single substitution in front of the reader. Compare Ch 14's "You have been taking the sight from too low" — different move, same confidence. The catalog should hold both. |
| **Turning the title into an argument** | "The chart is the truth, but not because a file is inherently authoritative. Files are only ever claims. A YAML manifest on somebody's laptop is a claim nothing enforces… **The chart is the truth because something is continuously making it true.** The authority is not in the file. It is in the loop that never stops comparing the file to the world." | **Strong candidate.** A chapter title interrogated rather than restated, and the correction lands on the chapter's actual thesis. Rare construction; the book has not used it before. |
| **Logbook Entry** | "The incident is small… one field, one `kubectl edit`, thirty seconds. The service recovers. **It is genuinely the right call in the moment**; the alternative is a code review at 6pm. … Nobody writes it down, because writing it down was the slow path they were avoiding. … The mechanism that catches it has a name, **and it is not an alarm**." | **Strong candidate.** Subject-dignity guardrail executed exactly right: the engineer is defended twice, the fault is relocated to the system, and the sidebar ends on a withheld answer that §4 pays. Composite framing is explicit ("There is a version of this story on every platform team"), so no fabricated-incident risk. |
| **Disclosure that argues rather than hedges** | "What supports the inference that GitOps belongs here is **positive rather than speculative**. Argo and Flux are both CNCF **graduated** projects… A CNCF exam asking about application delivery is asking about the delivery model CNCF's own graduated projects implement. **That is the basis. It is a good one, and it is honest about being an inference.**" | **Strong candidate.** Ch 14's disclosure exemplar concedes and defends; this one *builds a positive case* and then still labels it an inference. The pair reads as a developed technique rather than a repeated tic. |
| **Calibrating a Soundings before the reader starts** | "Two of these questions are load-bearing: **miss them and the last section will not land, and no amount of careful reading here will fix that. Better to find out now.**" → and in the key: "If you missed **question 1** in particular, that re-read is not optional. Everything else here will make sense without it. The last section will not." | **Moderate to strong.** Turns the pre-test rubric from a reading-speed dial into a genuine gate, and is honest that one section has a hard prerequisite. New Soundings move; hold at moderate only because it depends on the ⚑ C10 figure landing. |
| **Refusing to over-teach** | §5's opening — "This section is marked Advanced, and the marking is honest: it goes somewhat deeper than an associate credential is likely to reach" — closing with "The annotation is here for concreteness, not for memorization; you do not need to be able to write one from memory, and nothing in this chapter's questions asks you to." | **Moderate.** Respects the reader's time by scoping a section against the credential rather than against the subject. Skill Part 14's "don't pad" as an explicit contract with the reader. |

---

## Objective coverage log

Appended to `objective-coverage.md`. Audited row by row against `domain-analysis.md:261–288` and the B1 trap table at `:586–598`.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D3.1 — Application Delivery** | Chapter 14 (packaging half) | **deep — Chapter 15 covers the delivery half** | — |

**D3.1 GitOps/delivery concept coverage: 12 of 12 taught here.** GitOps · OpenGitOps · the four principles · Argo CD · source of truth · `OutOfSync` · sync · Argo CD manifest sources · tracking targets · Twelve-Factor App · deployment-strategy vocabulary · Flux — every `domain-analysis` D3.1 row outside Knative lands in Chapter 15, at depth. The Knative rows (`:283–287`) belong to **Ch 17 §6** per `section-skeleton.md:260` and are correctly untouched.

**Trap coverage: 6 of 6 D3.1 GitOps traps, all `[source]`-tagged, all deep.**

| # | Trap | Where addressed |
|---|---|---|
| 73 | "GitOps means running CI from Git" | §7's Fixed Point; Exam Alert #1; Common Traps row 1; Practice Q12 |
| 74 | Missing "pulled" — assuming a pipeline pushes | §3's principle-3 paragraph; TYB2 Q1 keyed; Practice Q11 distractor C |
| 76 | "`OutOfSync` means the sync failed" | §4 ★ Fixed Point; Exam Alert #2; TYB2 Q2; Practice Q13 |
| 77 | "Argo CD only deploys plain YAML" | §4 🪝 Snag; Common Traps; Practice Q14 |
| 78 | "Argo CD can only track a branch" | §4's three tracking targets; Common Traps; Practice Q15 |
| 85 | Reciting twelve-factor as twelve unrelated rules | §1's three-column sort (fig 15.1) — the trap's stated remedy, executed as the section's spine |

Trap 85's `[inferred]` correct-understanding reads *"the factors cluster."* Figure 15.1 is that clustering, and §1 makes the sorting question explicit — *"the useful question is not 'what is factor VII' but **who solves this**."* Contract honoured without being copied.

**Research gaps closed by Chapter 15:**

| Gap | Status |
|---|---|
| **G9 — deployment strategy vocabulary** (*"named across Argo CD and Istio sources but nowhere defined or contrasted"*) | **Closed.** §2 defines and contrasts all four from `argo-rollouts-strategies-2026-08-23` plus two CNCF glossary entries, and adds the decision criterion (traffic-splitting availability) the gap did not ask for. |
| **G18 — Flux** (*"appears only as a name in the graduated-projects roster"*) | **Closed, and over-delivered.** §6 gives Flux a full section from five snapshots, including the security model and the opposite drift default. |

**Still open and touching Chapter 15:** Argo Rollouts' self-definition (**new**, see ⚑ C4 — one graded section depends on it for coherence, not for fact) · the retired KCNA blueprint (**do not restore**, see ⚑ C1) · `argocd-diffing-outofsync`'s enumerated causes (the AUTHOR-REVIEW is correct; a full re-fetch would let §4 name one concrete cause).

---

## Retrieval-practice ledger

Appended to `retrieval-log.md`.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| ConfigMaps and Secrets deliver environment-specific values to an identical image | ch 4 §4 | ch 15 — Taking Your Bearings 1 Q3 *(`[retrieval: ch4]`)* |
| `maxSurge` and `maxUnavailable` are independent caps, not one budget | ch 6 §4 | ch 15 — Taking Your Bearings 1 Q4 *(`[retrieval: ch6]`)* |
| A ServiceAccount is identity; a ClusterRoleBinding supplies cross-namespace scope | ch 12 §2–§3 | ch 15 — Taking Your Bearings 2 Q4 *(`[retrieval: ch12]`)* |
| **A controller compares desired against current and acts, continuously, forever** | **ch 3 §6** | **ch 15 — Taking Your Bearings 3 Q5** *(`[retrieval: ch3]`)* — ⚑ **the item §7 depends on** |
| RBAC scope for a cross-namespace agent | ch 12 §3 | ch 15 — Practice Q16 *(currently `[cross-domain: D2.2]` — see ⚑ C3, C5)* |
| `spec` / `status` mapped onto target state / live state | ch 4 §2 | ch 15 — Practice Q17 *(currently `[cross-domain: D1.1]` — see ⚑ C3, C5)* |
| Permissions are additive; there is no deny rule | ch 12 §3 | ch 15 — Soundings Q5 (excluded from budget per B3) |
| A CRD extends the API; nothing acts without a controller | ch 6 §8 / ch 10 §3 | ch 15 — Soundings Q4 (excluded from budget per B3) |

### Compliance

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of **Bearings** | 25% (Ch 15 is at the ceiling) | 4 of 16 = **25.0%** | ✅ exactly |
| Retrieval share of the **Practice pool** | same target | **0 of 21 = 0%** | ❌ — ⚑ C5 |
| Retrieval share of **all graded items** | 25% | 4 of 37 = **10.8%** | ❌ |
| Spacing floor (≥4 chapters back, from Ch 8 on) | ≥1 item | ch 3 is **twelve** back | ✅ comfortably |
| Question inventory vs B4 | 8 · 10 · 21 · 39 | 8 · **16** · 21 · **45** | ⚑ C7 |

**The chapter's retrieval architecture is otherwise the best in the book, and that is worth recording rather than assuming.** TYB3 Q5 forbids the words *"Git, repositories, or delivery"* — forcing the reader to state Chapter 3's loop in its own terms rather than pattern-matching this chapter's — and its answer key routes a failed reader back to Ch 3 §6 **before** §7, not after. The Soundings does the same for question 1, and says so up front. For a chapter whose Zenith is a recognition rather than a fact, that is exactly the right structure: the retrieval item *is* the load-bearing beam, and the chapter treats it that way in both directions.

### Obligations Chapter 15 discharged — twelve, all verified by line number against shipped text

| Promise | Shipped at | Discharged by |
|---|---|---|
| *"a whole vocabulary of release strategies"* incl. blue/green, canary, A/B, and the tooling | `chapter-06:665` | §2 — ⚑ partially; see C4 and C6 |
| *"the third time is the one that matters"* (control loop) | `chapter-06:1465` | §7 — the sanctioned count, spent correctly |
| *"it will look like a new idea for about ten seconds"* | `chapter-06:1147` (§9, **not §8**) | §7's closing line |
| *"the structural claim this whole book is building toward"* | `chapter-09:1249` | §7 |
| Ch 5 §4's `terminationGracePeriodSeconds` → *"disposability"* | `chapter-05:559` | §1, factor IX, by name |
| Ch 4 §4's *"the twelve factors… Kubernetes hands you for free"* | `chapter-04:722` | §1's three-column sort |
| Ch 12 §2's *"an agent… whose job is to reconcile the cluster's contents"* | `chapter-12:617` | §4's agent-identity subsection |
| Ch 12 §3's roleRef-immutability ordering pointer | `chapter-12:866` | §5 — ⚑ **currently broken; see C2** |
| Ch 12 §1's *"GitOps before anyone has given you the word"* | `chapter-12:485` | §3 |
| Ch 14's *"who applies it / afterward, nothing keeps watch"* | `chapter-14:1387` | Why This Chapter Matters — ⚑ see the redundancy note below |
| Ch 14's rollback-by-revert reservation | `chapter-14:671` | §4, in the ledger's exact three-word form |
| Ch 14's charts-as-manifest-source anchor (B6: *"may not be dropped"*) | `section-skeleton.md:214` | §4's manifest-sources subsection |

**Verified on the redundancy finding, because it is larger than either the draft or the report states.** `chapter-14:1393`'s closing quote is **character-identical** to Chapter 15's epigraph, and `chapter-14:1387` is near-verbatim to Chapter 15's second paragraph. That is roughly 60 words of Chapter 14's final page reproduced on Chapter 15's first — channel redundancy under skill Part 7, at the exact point where arousal must be established. **The prose recap earns its place** (it sets up the two-halves structure that organizes the whole chapter); **the epigraph does not**. Cut one. Keeping both is the only option to avoid.

### Forward obligations Chapter 15 creates

| Topic Ch 15 owns | Must be retrieved in | How |
|---|---|---|
| The Pod that is running, healthy, `Synced`, **and wrong** | **Ch 16** | The Voyage Ahead states it and declines to resolve it; Ch 13 §8's handoff comes due there |
| CNCF maturity **levels** (not the roster) | **Ch 17 §2** | §6's 🔭 Closer Look points at it and explicitly tells the reader not to memorize the roster — B3's must-not-retrieve rule honoured |
| The control loop, collected across all five altitudes | **Ch 17 §4** | §7 spends Ch 6's sanctioned "third time." ⚠ **No chapter after this may assert a running ordinal** (`term-ownership.md:754`) |
| Service mesh as the thing canary needs | **Ch 17 §5** | §2 emits the cross-bearing; the dependency is stated, not the mechanism |
| Knative as the remaining D3.1 material | **Ch 17 §6** | Correctly untouched here |
| Twelve-factor as a predecessor of cloud-native vocabulary | **Ch 17 §3** | §1's closing paragraph plants it explicitly |

### Ledger and glossary debts to record at the glossary build

New B7 rows for **progressive delivery**, **repository server**, **sync operation status**, **prune**, **Jsonnet**, **Kubernetes Impersonation API**, and **Argo Rollouts** (no owner anywhere in the ledger). Amend the **Drift** row to `§3 (definition) / §4 (detection)` (⚑ C6). Amend the **A/B testing** row to "named and bounded, not taught as a release strategy" (⚑ C6). Soften the **blast radius** row's ownership claim (⚑ C8). Add a canonical-forms row for **revision (Argo CD / Git sense) → always write "commit"**, and move the disambiguating clause forward from §4's rollback subsection to its first bare use in "What it tracks." Carried forward unchanged from earlier gates: **CNAME**, **BGP**, **eBPF**, **IPVS**, **CIDR**, the **VPA** first-appearance correction, the hyphenated "cloud-native" instances, and the orphaned **Go template** row (`term-ownership.md:461`).

**Not flagged — checked and clean, recorded so a later stage does not re-open them.** All source tags in the chapter resolve to files that exist in `sources/` (45 Ch 15-relevant snapshots enumerated). The five highest-risk quotations were verified verbatim against their snapshots: the four OpenGitOps principles, Argo CD's clusteradmin default, Flux's "promptly reverted," the `.spec.interval` 60-second minimum with no API default, and the `OutOfSync`-after-successful-sync sentence. The chapter's careful walk-back of Flux's "five minutes by default" against the API reference is **correct and better than its source** — `flux-kustomization-api-2026-08-31`'s own capture note makes exactly that distinction. Terminology is clean on all twelve canonical forms checked; the single `K8s` instance is inside a permitted quotation. The `ch15-zenith-…` figure anchor matches shipped `ch14-zenith-package-not-template` and is a rule-amendment question, not a Chapter 15 defect.

---

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 15 additions

> ⚠ **MERGE REQUIRED BEFORE PROMOTION.** A further A–Z sequence appended after the
> Chapter 14 block, for the reason recorded there: merging in place would require
> re-transcribing verbatim documentation definitions, and Rule 5 treats definitional
> drift as worse than a duplicated alphabet. Interleave mechanically before promoting
> this file to the shipped back-of-book glossary. No entry below duplicates an entry above.

---

## A

**A/B testing** — Product experimentation, not a release strategy. Documented as a use of a
separate resource: *"A user can use experiments to enable A/B/C testing by launching multiple
experiments with a different version of their application for a long duration."*
`[source: argo-rollouts-experiments-2026-08-31]` (Chapter 15 §2)

> ★ **Not a fourth member of the Recreate / RollingUpdate / blue-green / canary list.** The four
> release strategies measure whether a new version is *broken*, for as short a duration as
> possible. A/B testing measures which version users *prefer*, over a long duration, on purpose.
>
> ⚠ **Ledger conflict.** `term-ownership.md:486`, `section-skeleton.md:223` and the acronym
> register all assign A/B to Ch 15 §2 as a taught strategy, and shipped `chapter-06:665`
> promises the reader "blue/green, canary, **and A/B**." The chapter's exclusion is
> substantively right — `argo-rollouts-canary-2026-08-31`'s capture note confirms the string
> "A/B" does not appear on the canary strategy page — but the framing collides with three
> contracts. See manifest ⚑ C6.

**`Application` (Argo CD)** — ★ *"A group of Kubernetes resources as defined by a manifest.
This is a Custom Resource Definition (CRD)."* `[source: argocd-core-concepts-2026-08-31]`
More precisely: *"The Application CRD is the Kubernetes resource object representing a deployed
application instance in an environment."* It is defined by two pieces of information — a
*"source reference to the desired state in Git (repository, revision, path, environment)"* and a
*"destination reference to the target cluster and namespace."*
`[source: argocd-declarative-setup-2026-08-31]` (Chapter 15 §4)

> ★ **The whole contract is: this content, from there, goes there.** An `Application` on a
> cluster with no Argo CD controller is a stored document describing a deployment that will
> never occur — the absent-component pattern, in its cleanest instance in this book.
> See [[absent-component-pattern]].

**Application source type** — *"Which Tool is used to build the application,"* where a **tool**
is *"a tool to create manifests from a directory of files. E.g. Kustomize"* and a
**configuration management plugin** is *"a custom tool."*
`[source: argocd-core-concepts-2026-08-31]` (Chapter 15 §4)

**Argo CD** — ★ A *"declarative, GitOps continuous delivery tool for Kubernetes."*
`[source: argocd-overview-2026-08-23]` Its application controller *"is a Kubernetes controller
which continuously monitors running applications and compares the current, live state against
the desired target state (as specified in the repo)."*
`[source: argocd-architecture-2026-08-31]` (Chapter 15 §4; named at Ch 3 §5)

> ★ **Read that definition as three claims: it is a Kubernetes controller (Ch 3 §6's thing); it
> continuously compares current against desired (Ch 3 §6's behaviour); its desired state is in
> a repository (the only new part).** This is the chapter's central Fixed Point and the whole
> basis of §7. See [[control-loop-pointed-at-a-repository]].
>
> ⚠ **First appears in the book at Ch 3 §5, not Ch 3 §6.** The draft's cross-bearing points at
> §6; Argo CD is named at `chapter-03:653`, inside §5 (610–749). Verified.

**Argo Rollouts** — ⚠ **NOT DEFINED ANYWHERE IN THE BOOK OR THE CORPUS.** Named once in
Chapter 15 §2, after four prior references to "Argo's description" / "Argo's comparison" /
"Argo's documentation."

> ⚠ **PROVISIONAL, and it is a comprehension hazard rather than a factual one.** Verified
> independently: none of the three `argo-rollouts-*` snapshots contains a self-definition.
> `argo-rollouts-strategies-2026-08-23` opens at "Progressive delivery is…";
> `argo-rollouts-experiments-2026-08-31` opens at "The Experiment CRD allows users…";
> `argo-rollouts-canary-2026-08-31` defines only canary.
>
> The consequence: a reader meets "Argo" five times in §2 and then meets "**Argo CD**" in §4 as
> though for the first time, and will fuse them. They are different tools; Argo CD does not
> include Argo Rollouts. **FIX (no fetch required):**
> `cncf-project-maturity-levels-2026-08-23` lists the graduated project as **"Argo"** — the
> umbrella. So §2 can say: *"Argo Rollouts — a separate controller in the same Argo project as
> §4's Argo CD, and one concrete instance of the tooling this section says these patterns
> require."* Every clause is supportable from cached metadata, and it discharges shipped
> `chapter-06:665`'s promise of "the tooling that implements them" at the same time.

---

## B

**Blast radius** — How far the damage from a single compromise extends. A shared CI system
holding write credentials for twelve clusters has a blast radius of twelve clusters; a per-cluster
in-cluster agent has a blast radius of one. *"Pull does not prevent compromise. It bounds it."*
(Chapter 15 §3)

> ⚠ **Standard security vocabulary, not a Lodestar coinage.** §3 words this correctly
> ("This book calls that reach the blast radius"); **Practice Q10's answer key overclaims it**
> as "this book's term." What is the book's is the push-versus-pull *argument*, which the
> chapter is otherwise scrupulous about labelling. One-word fix. See manifest ⚑ C8.
>
> ⚠ The push-versus-pull security comparison is **the book's reading** of principle 3 combined
> with the two projects' documented credential storage. No CNCF or vendor source in this
> chapter's corpus argues it in these terms, and the chapter says so three times — in §3's
> "A note on what follows," in TYB2 Q3's key, and in Practice Q10's key. Correctly handled;
> do not let a later stage promote it to a documented finding.

**Blue/green deployment** — Two complete environments, one live. *"During this time, only the
old version of the application will receive production traffic. This allows the developers to run
tests against the new version before switching the live traffic to the new version."*
`[source: argo-rollouts-strategies-2026-08-23]` CNCF describes the operator maintaining "blue" and
"green" environments with traffic switched via load balancer after testing the inactive one.
`[source: cncf-glossary-blue-green-deployment-2026-08-31]` (Chapter 15 §2)

> ★ **A pattern, not a Deployment field.** A Deployment object has no concept of a second
> environment and no control over traffic routing. Cost: double capacity. What it buys: testing
> against production configuration and production backing services before one user arrives,
> and a rollback that is one moment rather than a gradual unwind.
>
> 🔭 CNCF's glossary is more critical than most vendor material: blue/green *"is an appropriate
> strategy for non-cloud native software that needs to be updated with minimal downtime.
> However, its use is normally a 'smell' that legacy software needs to be re-engineered so that
> components can be updated individually."*
> `[source: cncf-glossary-blue-green-deployment-2026-08-31]`
>
> ⚑ Needs **no traffic provider** and *"suits workloads such as queue workers"*
> `[source: argo-rollouts-strategies-2026-08-23]` — which is the practical answer to
> "blue/green or canary," and it is a platform question more than a risk-appetite one.

**Bootstrap (Flux)** — *"The process of installing the Flux components in a GitOps manner is
called a bootstrap. The manifests are applied to the cluster, a `GitRepository` and
`Kustomization` are created for the Flux components, then the manifests are pushed to an existing
Git repository (or a new one is created)."* `[source: flux-concepts-2026-08-31]` The 2026-08-23
capture states the consequence plainly: *"Flux manages itself like any other resource."*
`[source: flux-concepts-2026-08-23]` (Chapter 15 §6)

> ★ Upgrading Flux is a commit. Reconfiguring Flux is a commit. Argo CD documents no equivalent.

---

## C

**Canary deployment** — *"A Canary deployment exposes a subset of users to the new version of the
application while serving the rest of the traffic to the old version. Once the new version is
verified to be correct, the new version can gradually replace the old version."*
`[source: argo-rollouts-strategies-2026-08-23]` From the operator's side: *"a canary rollout is a
deployment strategy where the operator releases a new version of their application to a small
percentage of the production traffic."* `[source: argo-rollouts-canary-2026-08-31]`
(Chapter 15 §2)

> ★ **Requires infrastructure, not just intent.** Canary strategies *"offer greater flexibility
> but demand more infrastructure (traffic-splitting via a service mesh or ingress controller)
> and metric analysis."* `[source: argo-rollouts-strategies-2026-08-23]` Without traffic
> splitting there is nowhere to send 5%; without metrics there is nothing to abort on. A queue
> worker has no inbound traffic to proportion, so canary is not a better blue/green — it is a
> different tool that needs a request path.
>
> Why anyone bothers: *"No matter how thorough the testing strategy, there are always some bugs
> discovered in production. Shifting 100% of traffic from one version of an app to another can
> lead to more impactful failures."* `[source: cncf-glossary-canary-deployment-2026-08-31]`

**CD (continuous delivery)** — *"A set of practices in which code changes are automatically
deployed into an acceptance environment (or, in the case of continuous deployment, into
production)."* Includes procedures ensuring software is adequately tested before deployment, and
a way to roll changes back. `[source: cncf-glossary-continuous-delivery-2026-08-31]`
(Chapter 15 §3)

**CD (continuous deployment)** — *"Goes a step further than continuous delivery by deploying
finished software directly to production."*
`[source: cncf-glossary-continuous-deployment-2026-08-31]` (Chapter 15 §3)

> ⚠ **CNCF abbreviates both as "CD."** This is genuinely ambiguous in the field. When the
> distinction matters — and it matters exactly when the question is whether a human approves the
> production step — spell the word out.

**CI (continuous integration)** — *"The practice of integrating code changes as regularly as
possible."* It *"allows software teams to turn every code commit into either a concrete failure or
a viable release candidate."* `[source: cncf-glossary-continuous-integration-2026-08-31]`
(Chapter 15 §3)

> ★ **CI is not part of the GitOps definition.** None of the four principles mentions
> integration, building, or testing. Kubernetes says so from its own side: it *"does not deploy
> source code and does not build your application."* `[source: k8s-docs-overview-2026-08-23]`
> This is B1 trap #73, and it is wrong at the level of category, not detail.

---

## D

**Delivery-agent identity** — The ServiceAccount and RBAC grants a GitOps agent runs as. The
Kubernetes documentation names this use explicitly: *"an external service needs to communicate
with the Kubernetes API server (CI/CD pipelines)."*
`[source: k8s-docs-service-accounts-2026-08-23]` (Chapter 15 §4)

> ⚠ **Not exempt infrastructure — one of the highest-value subjects in the cluster.**
> *"By default, Argo CD uses a clusteradmin level role in order to: 1. watch & operate on
> cluster state 2. deploy resources to the cluster."*
> `[source: argocd-security-cluster-credentials-2026-08-31]`
>
> ★ **Note the asymmetry.** Cluster-wide **read** is structural — an agent cannot detect drift in
> what it cannot see. Broad **write** is a default, not a requirement: *"it does not necessarily
> need full write privileges to the cluster,"* and operators may edit the ClusterRole
> `argocd-manager-role` *"such that write privileges are limited to only the namespaces and
> resources that you wish Argo CD to manage."*
> `[source: argocd-security-cluster-credentials-2026-08-31]`
>
> ★ **Commit access to the tracked branch is cluster access**, mediated by an agent that will
> faithfully apply whatever it finds. In a mature GitOps setup the repository's branch-protection
> rules *are* an access-control mechanism, exactly as load-bearing as RBAC. Not a metaphor.

**Deployment strategy** — ★ **The vocabulary, not the mechanics.** `RollingUpdate` and `Recreate`
are values of a field on a Deployment; blue/green and canary are patterns requiring tooling above
the Deployment object. A Deployment cannot express either one on its own. (Chapter 15 §2;
mechanics at Ch 6 §4)

> ⚠ This is the single distinction from §2 most likely to be tested, and the one readers most
> often collapse. `RollingUpdate` *"is the default strategy of the Deployment object"*
> `[source: argo-rollouts-strategies-2026-08-23]`.
>
> 🔭 Chapter 6 called these *"release strategies"* (`chapter-06:665`). This book's headword is
> **deployment strategy**, because "release" already carries a Kubernetes minor version and a
> Helm release. Both phrases name the same thing.

**Drift** — *"When a system's actual state has moved or is in the process of moving away from the
desired state…"* `[source: opengitops-glossary-2026-08-31]` CNCF names it first among the problems
GitOps addresses, observing that *"configuration drift can be hard to detect and resolve without a
source of truth governing it."* `[source: cncf-glossary-gitops-2026-08-31]` (Chapter 15 §3
definition; §4 detection)

> ⚠ **The OpenGitOps definition is truncated in the snapshot** — the ellipsis is the capture's,
> and its note says explicitly: *"treat the truncated definitions as partial and do not extend
> them from memory."* The chapter honours this.
>
> ⚑ B7 (`term-ownership.md:497`) assigns drift to §4. The chapter defines it in §3 and detects in
> §4, which is the better arrangement — drift is what principle 4 exists to catch. Amend the
> ledger row, not the chapter.

---

## F

**Flux** — A **GitOps Toolkit**: *"a collection of specialized tools, Flux Controllers, composable
APIs, and reusable Go packages available under the fluxcd GitHub organization."*
`[source: flux-concepts-2026-08-31]` The 2026-08-23 capture is blunter: *"Flux is a GitOps
Toolkit: a set of composable APIs and specialized tools that can be used to build Continuous
Delivery on top of Kubernetes."* `[source: flux-concepts-2026-08-23]` (Chapter 15 §6)

> ★ **The contrast with Argo CD is composability, not capability.** Argo CD presents as one
> integrated product with a single `Application` resource and a UI over everything; Flux presents
> as a set of controllers you assemble, each owning its own custom resources.
> `[source: flux-components-2026-08-31]` Neither posture is better. Teams pick on organizational
> grounds more than technical ones.
>
> ⚠ **"Integrated" does not mean "one process."** Argo CD sits on three components — an API
> server, a repository server, and an application controller.
> `[source: argocd-architecture-2026-08-31]`
>
> ★ **Opposite drift default from Argo CD.** *"If you make any changes to the cluster using
> `kubectl edit/patch/delete`, they will be promptly reverted."*
> `[source: flux-concepts-2026-08-31]` Argo CD, out of the box, does not.
> `[source: argocd-auto-sync-policy-2026-08-31]` Two graduated projects, four shared principles,
> opposite answers to "what do I do about drift I detect."
>
> **Security model differs too.** A `crd-controller` ClusterRole has *"full access to all the
> Custom Resource Definitions defined by Flux controllers"*; a `cluster-reconciler`
> ClusterRoleBinding references `cluster-admin`, bound *"to service accounts for only
> `kustomize-controller` and `helm-controller`"* because those *"are the only two controllers
> that manage resources in the cluster."* `[source: flux-security-2026-08-31]` Reduction is by
> **impersonation** rather than narrowing.

**Flux controller set** — Source (`GitRepository`, `OCIRepository`, `HelmRepository`, `HelmChart`,
`Bucket`, `ExternalArtifact`, `ArtifactGenerator`) · Kustomize (`Kustomization`) · Helm
(`HelmRelease`) · Notification (`Provider`, `Alert`, `Receiver`) · Image Reflector and Image
Automation (`ImageRepository`, `ImagePolicy`, `ImageUpdateAutomation`).
`[source: flux-components-2026-08-31]` (Chapter 15 §6)

> ⚠ The snapshot's capture note is explicit: it carries only controller names and CRD lists.
> **Do not attribute behavioural claims to it.** The chapter cites it only for the roster, which
> is correct. What is worth carrying is the shape — one controller per concern, each with its own
> API — not the roster.

---

## G

**GitOps** — ★ *"GitOps is a set of principles for operating and managing software systems."*
`[source: opengitops-principles-v1-2026-08-31]` CNCF's fuller phrasing: *"a set of practices for
managing software applications and infrastructure by continuously evaluating and reconciling their
desired states as defined in a version control system such as Git against their actual state."*
`[source: cncf-glossary-gitops-2026-08-31]` (Chapter 15 §3; named at Ch 1 and Ch 12 §1)

> ★ **Four principles, all about desired state — how it is expressed, stored, obtained, and
> applied.** Continuous integration is not among them. See
> [[opengitops-four-principles]].
>
> ⚠ **The name says Git; the principles do not require it.** *"Many version control systems can
> be used in GitOps as long as they meet those two basic requirements and teams use them in a
> conformant manner."* `[source: opengitops-1-0-announcement-2026-08-31]` (The announcement does
> not restate which two; on this book's reading they are principle 2's immutability and complete
> version history, which is the only pair the principles state about the store itself.)
>
> Named benefits: *"transparency and traceability of changes, reliability and security through
> declarative states, and rollback, revert, and self-healing attributes."*
> `[source: cncf-glossary-gitops-2026-08-31]`

---

## J

**Jsonnet** — ⚠ **Never glossed in the book.** Appears only inside the quoted list of Argo CD
manifest sources — yet reaches **Practice Q14's answer key** and the **Common Traps** table.
One clause, or drop it from the key. (Chapter 15 §4)

---

## L

**Live state (Argo CD)** — *"The live state of that application. What pods etc are deployed."*
`[source: argocd-core-concepts-2026-08-31]` (Chapter 15 §4)

> ★ Anchor to Chapter 4 under pressure: **target state is `spec`, kept outside the cluster;
> live state is what `status` reports.** Argo CD's central comparison is the one you have been
> reading since Ch 4 §2, with one operand relocated. See [[spec]], [[status]].

---

## M

**Manifest source (Argo CD)** — Manifests may be specified *"in several ways: kustomize
applications; helm charts; jsonnet files; plain directory of YAML/json manifests; any custom
config management tool configured as a config management plugin."*
`[source: argocd-overview-2026-08-23]` (Chapter 15 §4)

> ⚠ **"Argo CD only deploys plain YAML" is B1 trap #77 and a confident mistake.** Rendering is a
> whole component: the **repository server** *"maintains a local cache of the Git repository
> holding the application manifests"* and is responsible for *"generating and returning the
> Kubernetes manifests"* given a repository URL, revision, path, and template-specific
> configuration. `[source: argocd-architecture-2026-08-31]`
>
> ★ This is where Chapter 14's work gets collected: a Helm chart is a manifest source, and so is
> a Kustomize overlay. Chapter 14 gave you packaging; Chapter 15 gives packaging somewhere to go.
> See [[helm-chart]], [[kustomize]].

**Multi-cluster delivery** — Argo CD documents an *"ability to manage and deploy to multiple
clusters"* `[source: argocd-overview-2026-08-23]`, with each external cluster's credentials stored
as a Secret in the `argocd` namespace of the managing cluster.
`[source: argocd-security-cluster-credentials-2026-08-31]` (Chapter 15 §6)

> ⚠ **DO NOT OVER-CLAIM THE FLUX SIDE.** Flux's documented position is narrower: its reconciling
> controllers run *in* the cluster they reconcile `[source: flux-security-2026-08-31]`, and
> bootstrap installs Flux into a cluster against a Git repository
> `[source: flux-concepts-2026-08-31]`. **There is no cached source for a Flux multi-cluster
> topology or for cross-cluster credential handling in either direction.** An earlier draft
> asserted "one Flux per cluster… no cluster holding credentials to another" under a
> mis-attributed tag; the claim is now correctly reduced. `flux-security-2026-08-31`'s soft
> multi-tenancy material is about tenants **within one cluster** and must not be read across.
> To restore the fuller comparison, cache fluxcd.io's multi-cluster/multi-tenancy guide.

---

## O

**OpenGitOps four principles** — ★ Desired state must be:
1. **Declarative** — *"A system managed by GitOps must have its desired state expressed
   declaratively."*
2. **Versioned and Immutable** — *"Desired state is stored in a way that enforces immutability,
   versioning and retains a complete version history."*
3. **Pulled Automatically** — *"Software agents automatically pull the desired state declarations
   from the source."*
4. **Continuously Reconciled** — *"Software agents continuously observe actual system state and
   attempt to apply the desired state."*
`[source: opengitops-principles-v1-2026-08-31]` (Chapter 15 §3)

> ★ **Two words carry the definition: *pulled* and *continuously*.** A pipeline that stores
> manifests in Git and pushes them into a cluster satisfies 1 and 2 and fails 3 and 4 completely.
> That is a perfectly reasonable thing to build. It is not GitOps. (B1 traps #73 and #74.)
>
> The project is explicit that the precision is deliberate: *"The wording of each principle and
> linked glossary item was very carefully chosen."*
> `[source: opengitops-1-0-announcement-2026-08-31]`
>
> ★ **Only principle 2 is new to a reader of this book.** 1 is Ch 4 §1's declarative model, 3 is
> Ch 3 §5's watch, 4 is Ch 3 §6's loop verbatim. That is the whole content of §7.
>
> ⚠ *"OpenGitOps is a CNCF project"* is supported by this snapshot's `authority:` **metadata
> field only**, not by body text. `domain-analysis.md:262` says "CNCF **sandbox** project." The
> chapter's weaker claim is correct and should stand; the tag is thin.

**`OutOfSync`** — ★ *"A deployed application whose live state deviates from the target state is
considered OutOfSync."* Argo CD *"reports and visualizes the differences, while providing
facilities to automatically or manually sync the live state back to the desired target state."*
`[source: argocd-overview-2026-08-23]` (Chapter 15 §4)

> ★ **A drift signal, not an error.** Nothing has necessarily failed. A person editing an object
> by hand produces one; so does a commit that has not been applied yet. This is B1 trap #76.
>
> ★ **Two fields, two questions.** *Sync status* answers *"is the deployed application the same
> as Git says it should be?"*; *sync operation status* answers *"whether or not a sync
> succeeded."* `[source: argocd-core-concepts-2026-08-31]` The documentation states the
> combination outright: *"It is possible for an application to be `OutOfSync` even immediately
> after a successful Sync operation."* `[source: argocd-diffing-outofsync-2026-08-31]`
>
> ⚠ **No cause may be attributed to that snapshot.** Its capture note records that the page's
> enumerated causes were returned as summary rather than quotation. The chapter correctly states
> the claim without naming a cause; a full re-fetch would let §4 name one.
>
> ★ **The out-of-the-box behaviour is the Fixed Point's own best proof.** If `OutOfSync` were an
> error, a tool would not sit there reporting it.

---

## P

**Progressive delivery** — *"The process of releasing updates of a product in a controlled and
gradual manner, thereby reducing the risk of the release, typically coupling automation and
metric analysis to drive the automated promotion or rollback of the update."*
`[source: argo-rollouts-strategies-2026-08-23]` (Chapter 15 §2)

> ★ **The metric-analysis half is what distinguishes it from deploying slowly.** A
> `RollingUpdate` with a small `maxSurge` is gradual and is not progressive delivery. Gradual
> buys time; metric analysis is what uses the time. Graded at Practice Q7.
>
> ⚠ No B7 ledger row, despite being the umbrella term for the whole of §2.

**Prune** — Deletion of resources no longer defined in the repository. ⚠ **Opt-in in Argo CD:**
*"By default (and as a safety mechanism), automated sync will not delete resources when Argo CD
detects the resource is no longer defined in Git."*
`[source: argocd-auto-sync-policy-2026-08-31]` (Chapter 15 §4)

> ★ **Permission and configuration are different things.** The agent must hold the `delete` verb
> before it can prune, but holding it does not make it prune. Graded twice on that distinction
> (TYB2 Q4, Practice Q16). ⚠ No ledger row.

**Pull-based delivery** — An agent runs inside the cluster, holds credentials to a repository,
reaches outward for desired state, and applies it locally. Nothing outside the cluster holds
cluster credentials. (Chapter 15 §3) — see [[push-versus-pull-delivery]] for the four consequences
and which of them are sourced.

**Push-based delivery** — A pipeline runs outside the cluster, holds credentials *to the cluster*,
and reaches inward across the cluster boundary to apply manifests. (Chapter 15 §3)

> ⚠ **Push versus pull is about where the credentials live, not about network topology.** A
> self-hosted runner, a VPN, or a private CI instance all push to an API server that is not
> publicly reachable. Nothing about push requires exposure — this is the confusion Practice Q9
> exists to clear.
>
> ⚠ **Push-based CD is a perfectly good delivery system.** The chapter says so twice, on purpose.
> It is not GitOps, whatever its manifests are stored in.

---

## R

**Reconciliation** — *"The process of ensuring the actual state of a system matches its desired
state."* `[source: opengitops-glossary-2026-08-31]` Flux's form: *"ensuring that a given state
(e.g. application running in the cluster, infrastructure) matches a desired state declaratively
defined somewhere (e.g. a Git repository)."* `[source: flux-concepts-2026-08-31]`
(Chapter 15 §3, §4, §7)

**`Recreate`** — *"A Recreate deployment deletes the old version of the application before bringing
up the new version. As a result, this ensures that two versions of the application never run at the
same time, but there is downtime during the deployment."*
`[source: argo-rollouts-strategies-2026-08-23]` (Chapter 15 §2; mechanics at Ch 6 §4)

> ★ **The guarantee is not a consolation prize.** If the new version runs a schema migration the
> old version cannot read, coexistence *is* the failure mode, and Recreate is the correct choice
> rather than the lazy one.

**Refresh (Argo CD)** — *"Compare the latest code in Git with the live state. Figure out what is
different."* `[source: argocd-core-concepts-2026-08-31]` (Chapter 15 §4)

> ★ **Refresh compares; sync acts.** They are separate words because a system can know it is out
> of agreement without doing anything about it, and whether it acts is a policy decision with a
> documented default that surprises people.

**Repository server (Argo CD)** — The component that *"maintains a local cache of the Git
repository holding the application manifests"* and is responsible for *"generating and returning
the Kubernetes manifests"* given a repository URL, revision, path, and template-specific
configuration. `[source: argocd-architecture-2026-08-31]` (Chapter 15 §4)

> ⚠ No ledger row, and it is required by name in Practice Q14's answer key.

**Rollback by revert** — ★ Changing what the repository says — typically with `git revert`,
producing a new commit whose content is the old content — and letting the agent close the gap it
has been closing continuously since it started. Argo CD offers *"rollback/roll-anywhere to any
application configuration committed in Git repository."* `[source: argocd-overview-2026-08-23]`
(Chapter 15 §4)

> ★ **There is no second code path.** The rollback mechanism *is* the sync mechanism. You move
> the target; the loop does what it always does.
>
> ⚠ **The third mechanism in this book to wear the word, and the ledger requires this exact
> three-word unhyphenated form** (`term-ownership.md:854`). Chapter 15 complies throughout;
> shipped `chapter-14:671` writes it hyphenated and is the outlier.
>
> | | What moves | Where the previous state was kept |
> |---|---|---|
> | `kubectl rollout undo` (Ch 6 §5) | the Deployment's Pod template | the old ReplicaSet, on the cluster |
> | `helm rollback` (Ch 14 §3) | the Helm release to a prior revision | Helm's release history, on the cluster |
> | **rollback by revert** (Ch 15 §4) | a commit in the repository | the repository's history |
>
> ⚠ **Do not call the thing you revert a "revision."** *Revision* has two owners already (a
> Deployment revision, a Helm release revision). A Git revision is a **commit**. Argo CD's own
> API field is named `revision`, which is why this needs saying.

---

## S

**Self-heal** — The agent correcting drift it detects in the cluster, rather than only responding
to new commits. ⚠ **Off by default in Argo CD:** *"By default, changes that are made to the live
cluster will not trigger automated sync."* `[source: argocd-auto-sync-policy-2026-08-31]`
(Chapter 15 §4)

> ★ **"Every GitOps agent reverts manual changes" is false.** Flux does, promptly
> `[source: flux-concepts-2026-08-31]`; Argo CD, out of the box, does not. Principle 4 requires
> continuous *observation*; what the agent then *does* is configuration.
>
> Two further facts: automated sync fires only on a difference — *"An automated sync will only be
> performed if the application is `OutOfSync`"* — and the cadence *"defaults to `120s` with added
> jitter of `60s` for a maximum period of 3 minutes."*
> `[source: argocd-auto-sync-policy-2026-08-31]`

**Soft multi-tenancy (Flux)** — ⚠ **Appears only inside a quotation and is never glossed.**
*"In a soft multi-tenancy setup, Flux does not reconcile a tenant's repo under the `cluster-admin`
role. Instead, you specify a different service account in your manifest, and the Flux controllers
will use the Kubernetes Impersonation API under `cluster-admin` to impersonate that service
account."* `[source: flux-security-2026-08-31]` Gloss it or drop the phrase. (Chapter 15 §6)

**Source (Flux)** — *"A Source defines the origin of a repository containing the desired state of
the system and the requirements to obtain it (e.g. credentials, version selectors)."*
`[source: flux-concepts-2026-08-31]` (Chapter 15 §6)

> ★ Flux elevates where-state-comes-from into its own API. The source controller produces an
> artifact; other controllers consume it. `OCIRepository` and `HelmRepository` sit alongside
> `GitRepository` as source kinds — Chapter 2's OCI work and Chapter 14's chart-store work, both
> collected. See [[oci]], [[chart-repository]].

**Source of truth** — The authored desired state, upstream of the cluster, from which the agent
keeps the cluster in agreement by ordinary API calls. (Chapter 15 §3, §4)

> ⚠ **Git does NOT replace etcd, and this is the misreading the phrase invites.** etcd still holds
> every object. A GitOps agent does not write to the datastore directly and does not bypass the
> API server — it is an API client like any other, subject to authentication, then authorization,
> then admission, in that order. Chapter 3's claim about the only door in is not suspended.
> See [[api-server-hub]], [[api-access-gates]].
>
> The consequence you can act on: an agent lacking RBAC permission to create a resource fails with
> an ordinary authorization error. GitOps grants no exemption from any cluster control. If
> anything it is *more* constrained than a human operator, because its permissions are written
> down.

**Sync** — *"The process of making an application move to its target state. E.g. by applying
changes to a Kubernetes cluster."* `[source: argocd-core-concepts-2026-08-31]` (Chapter 15 §4)

**Sync hook phases** — *PreSync* hooks run *"prior to the application of the manifests"*; *Sync*
hooks *"after all PreSync hooks completed and were successful, at the same time as the application
of the manifests"*; *PostSync* hooks *"after all Sync hooks completed and were successful, a
successful application, and all resources in a Healthy state"*; *SyncFail* hooks *"when the sync
operation fails."* `[source: argocd-sync-phases-and-waves-2026-08-31]` (Chapter 15 §5)

> ★ **PostSync requires health, not merely completion.** That gate is the part readers miss:
> PostSync is not "after the apply," it is "after the apply worked and the result is healthy."
> Suitable for smoke tests, notifications, and traffic cutover — which is how the tooling above a
> Deployment gets built. Argo CD ties them directly to §2's vocabulary: *"PreSync, Sync, PostSync
> hooks to support complex application rollouts (e.g. blue/green and canary upgrades)."*
> `[source: argocd-overview-2026-08-23]`

**Sync operation status** — *"Whether or not a sync succeeded."*
`[source: argocd-core-concepts-2026-08-31]` A different field answering a different question from
sync status. ⚠ No ledger row; graded twice. (Chapter 15 §4)

**Sync status** — *"Whether or not the live state matches the target state. Is the deployed
application the same as Git says it should be?"* `[source: argocd-core-concepts-2026-08-31]`
(Chapter 15 §4)

**Sync wave** — Integer ordering *within* a phase, lower values first. *"Hooks and resources are
assigned to wave 0 by default. The wave can be negative, so you can create a wave that runs before
all other resources."* `[source: argocd-sync-phases-and-waves-2026-08-31]` The mechanism is the
annotation `argocd.argoproj.io/sync-wave`. Precedence: *"1. The phase 2. The wave they are in
(lower values first)"*, with two deterministic tie-breaks after.
`[source: argocd-sync-phases-and-waves-2026-08-31]` (Chapter 15 §5)

> ★ **Relative ordering, not absolute positions.** `-5` and `0` order exactly as `0` and `1` do.
> There is no requirement to use consecutive integers. Readers who treat the number as a slot
> invent constraints the mechanism does not have.
>
> ⚠ The annotation is here for concreteness, **not for memorization** — §5 says so explicitly and
> no question in the chapter asks you to write one.

---

## T

**Target state (Argo CD)** — *"The desired state of an application, as represented by files in a
Git repository."* `[source: argocd-core-concepts-2026-08-31]` (Chapter 15 §4)

**Tracking revision** — What an `Application` compares against. A **branch or symbolic reference**:
*"Argo CD will continually compare live state against the resource manifests defined at the tip of
the specified branch or the resolved commit of the symbolic reference."* A **tag**: *"the manifests
at the specified Git tag will be used to perform the sync comparison"*; tags are *"generally
considered more stable, and less frequently updated."* A **pinned commit**: *"the app is
effectively pinned to the manifests defined at the specified commit… Since commit SHAs cannot
change meaning, the only way to change the live state of an app which is pinned to a commit, is by
updating the tracking revision in the application to a different commit."*
`[source: argocd-tracking-strategies-2026-08-31]` (Chapter 15 §4)

> ★ **Branch moves. Tag rarely moves. Commit never moves.** This is B1 trap #78 ("Argo CD can only
> track a branch").
>
> ★ Pinning is principle 2 showing up as an operational property. Argo CD's best-practices page
> makes the same argument: an unstable revision means manifests *"can suddenly change meaning,
> even without any changes to your own Git repository. A better version would be to use a Git tag
> or commit SHA."* `[source: argocd-best-practices-2026-08-31]`

**Twelve-factor app** — A methodology for software delivered as a service. A twelve-factor app
*"uses declarative formats for setup automation… has a clean contract with the underlying operating
system, offering maximum portability… is suitable for deployment on modern cloud platforms…
minimizes divergence between development and production… and can scale up without significant
changes to tooling, architecture, or development practices."*
`[source: twelve-factor-app-2026-08-23]` (Chapter 15 §1; promised at Ch 4 §4 and Ch 5 §4)

> ★ **A set of constraints an application accepts in exchange for being run by a platform.**
> Kubernetes implements the platform side — config injection, stateless replication, graceful
> termination, log collection. It cannot implement the application side. An application that
> writes its own log files, keeps session state in memory, or takes ninety seconds to start is not
> made twelve-factor by being containerized.
>
> ★ **The useful question is not "what is factor VII" but *who solves this*** — the platform, or
> you. That sorting is B1 trap #85's stated remedy and it is §1's spine.
>
> ⚠ The methodology's publication date, authorship, and precedence-by-three-years over Kubernetes
> were removed at revision and should stay removed: `twelve-factor-app-2026-08-23` begins at "In
> the modern era, software is commonly delivered as a service" and carries no date or provenance,
> and no snapshot carries a Kubernetes release date. The bare precedence relation the chapter
> retains is supported by the surrounding argument.

**Factor III (Config)** — *"An app's config is everything that is likely to vary between deploys
(staging, production, developer environments, etc)."* The litmus test: *"whether the codebase could
be made open source at any moment, without compromising any credentials."*
`[source: twelve-factor-iii-config-2026-08-31]` (Chapter 15 §1)

> ⚠ **"Store config in the environment" is not "put it in a config file."** A config file is an
> improvement on hard-coded constants but *"still has weaknesses: it's easy to mistakenly check in
> a config file to the repo."* The prescription is environment variables, because there is *"little
> chance of them being checked into the code repo accidentally."*
> `[source: twelve-factor-iii-config-2026-08-31]`
>
> 🪝 It is a claim about *where config lives relative to your code*, not about the literal `env:`
> block. A ConfigMap mounted as a file satisfies factor III perfectly well.
>
> ⚠ **Never group variables into named environments:** *"In a twelve-factor app, env vars are
> granular controls, each fully orthogonal to other env vars. They are never grouped together as
> 'environments', but instead are independently managed for each deploy."*
> `[source: twelve-factor-iii-config-2026-08-31]`

**Factor VI (Processes)** — *"Twelve-factor processes are stateless and share-nothing. Any data
that needs to persist must be stored in a stateful backing service, typically a database."*
And, banned by name: *"Sticky sessions are a violation of twelve-factor and should never be used or
relied upon."* `[source: twelve-factor-vi-processes-2026-08-31]` (Chapter 15 §1)

> ★ This is the assumption underneath Deployments. When it genuinely does not hold, Kubernetes has
> a different object — and it is a different object precisely because it steps outside this
> factor. See [[statefulset-storage]].

**Factor IX (Disposability)** — *"The twelve-factor app's processes are disposable, meaning they can
be started or stopped at a moment's notice."* Startup: *"a process takes a few seconds from the time
the launch command is executed until the process is up and ready."* Shutdown: *"Processes shut down
gracefully when they receive a SIGTERM signal from the process manager."* And: *"Processes should
also be robust against sudden death, in the case of a failure in the underlying hardware."*
`[source: twelve-factor-ix-disposability-2026-08-31]` (Chapter 15 §1; mechanism at Ch 5 §4)

> 🪢 **Fast up. Clean down. Survive the floor dropping.** Graceful shutdown is a courtesy the
> platform extends when it can. A node that loses power extends nothing.
>
> ⚑ Surface-form note: this chapter writes `SIGTERM`/`SIGKILL` (following its source); shipped
> Ch 5 §4 writes "a TERM signal" / "they get KILL." Both defensible, neither in the ledger.
> Recorded so a later sweep does not "correct" one toward the other by accident.

**Factor XI (Logs)** — *"Logs are the stream of aggregated, time-ordered events collected from the
output streams of all running processes and backing services."* The rule: *"A twelve-factor app
never concerns itself with routing or storage of its output stream. Each running process writes its
event stream, unbuffered, to stdout."* `[source: twelve-factor-xi-logs-2026-08-31]`
(Chapter 15 §1)

> ★ **This is why `kubectl logs` works on every container without any container being configured
> for it**, and why cluster-wide log collection can be a node-level concern. See
> [[cluster-level-logging]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

## Chapter 15 update (2026-08-31)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D3.1 — Application Delivery | Chapter 14 (packaging) | **deep — Chapter 15 covers delivery: strategies, push/pull, GitOps, Argo CD, Flux** | 2026-08-31 |

### Chapter 15 — D3.1 coverage detail

12 of 12 non-Knative D3.1 concept rows (`domain-analysis.md:261–288`) taught at depth:
GitOps · OpenGitOps · the four principles · Argo CD · source of truth · OutOfSync · sync ·
Argo CD manifest sources · tracking targets · Twelve-Factor App · deployment-strategy
vocabulary · Flux. Knative rows (`:283–287`) belong to Ch 17 §6 per `section-skeleton.md:260`
and are correctly untouched.

### Trap coverage — 6 of 6 D3.1 GitOps traps, all [source]-tagged, all deep

| # | Trap | Where addressed |
|---|---|---|
| 73 | "GitOps means running CI from Git" | §7 Fixed Point; Exam Alert #1; Common Traps 1; Q12 |
| 74 | Missing "pulled" | §3 principle-3 paragraph; TYB2 Q1; Q11 distractor C |
| 76 | "OutOfSync means the sync failed" | §4 Fixed Point; Exam Alert #2; TYB2 Q2; Q13 |
| 77 | "Argo CD only deploys plain YAML" | §4 Snag; Common Traps; Q14 |
| 78 | "Argo CD can only track a branch" | §4 three targets; Common Traps; Q15 |
| 85 | Twelve factors as unrelated rules | §1's three-column sort — the trap's own remedy |

### Research gaps CLOSED by Chapter 15

- **G9 — deployment strategy vocabulary.** Closed. All four defined and contrasted, plus the
  decision criterion (traffic-splitting availability) the gap did not ask for.
- **G18 — Flux.** Closed and over-delivered: a full section from five snapshots, including
  the security model and the opposite drift default.

### Still open and touching Chapter 15

- **NEW — Argo Rollouts' self-definition.** Zero occurrences across all three
  argo-rollouts-* snapshots. Not a factual gap; a comprehension hazard (readers will fuse it
  with Argo CD). Closable without a fetch via the "Argo" umbrella in
  cncf-project-maturity-levels-2026-08-23. See manifest ⚑ C4.
- **The retired KCNA blueprint weights.** ⚠ STILL AN OPEN GAP and STILL MUST NOT BE DRAFTED.
  cncf-curriculum-repo-kcna-versions-2026-08-23:36-44 records the retired PDF as
  text-not-extracted and says "DO NOT draft the retired weights from memory or from
  third-party study guides." lf-kcna-program-changes-2026-08-23:11-15 carries a CORRECTION
  confirming that page never displayed them. **Chapter 15 must NOT restore the 8% figure.**
  Chapter 1's line 274 and domain-analysis.md:39 are the things needing correction.
  See manifest ⚑ C1.
- **argocd-diffing-outofsync's enumerated causes.** The snapshot's capture note forbids
  attributing them. The chapter correctly states the claim causeless. A full re-fetch would
  let §4 name one concrete cause and strengthen the Fixed Point.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

## Chapter 15 (2026-08-31)

| Tested topic | Original chapter | Retested in |
|---|---|---|
| ConfigMaps/Secrets deliver env-specific values to an identical image | ch 4 §4 | ch 15 — TYB 1 Q3 [retrieval: ch4] |
| maxSurge and maxUnavailable are independent caps, not one budget | ch 6 §4 | ch 15 — TYB 1 Q4 [retrieval: ch6] |
| ServiceAccount = identity; ClusterRoleBinding = cross-namespace scope | ch 12 §2-§3 | ch 15 — TYB 2 Q4 [retrieval: ch12] |
| A controller compares desired vs current and acts, continuously, forever | ch 3 §6 | ch 15 — TYB 3 Q5 [retrieval: ch3] — LOAD-BEARING FOR §7 |
| RBAC scope for a cross-namespace agent | ch 12 §3 | ch 15 — Practice Q16 [cross-domain: D2.2] |
| spec/status mapped onto target state/live state | ch 4 §2 | ch 15 — Practice Q17 [cross-domain: D1.1] |
| Permissions are additive; there is no deny rule | ch 12 §3 | ch 15 — Soundings Q5 (excluded per B3) |
| A CRD extends the API; nothing acts without a controller | ch 6 §8 / ch 10 §3 | ch 15 — Soundings Q4 (excluded per B3) |

### Compliance

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Bearings retrieval share | 25% (Ch 15 at ceiling) | 4 of 16 = 25.0% | PASS, exactly |
| Practice retrieval share | 25% | 0 of 21 = 0% | FAIL — third chapter running |
| All graded items | 25% | 4 of 37 = 10.8% | FAIL |
| Spacing floor (>=4 chapters back) | >=1 item | ch 3 is twelve back | PASS |
| Question inventory vs B4 (8/10/21/39) | -- | 8/16/21/45 | +6 Bearings, +6 total |

### ⚑ THREE OPEN TAG ISSUES — fix at the book level, not per chapter

1. **Practice pool reads as 0% retrieval for the third consecutive chapter** (ch 13, 14, 15).
   Q16 and Q17 carry genuine backward reach but under a different keyword, so any audit
   grepping "[retrieval:" sees zero. Ch 19 is built by exactly such an audit.

2. **The interleave tag now has THREE surface forms across three consecutive chapters:**
   ch 13 shipped "[interleaved: D1.3 scheduling]"; ch 14 shipped "[interleaved: D1.1]";
   ch 15 proposes "[cross-domain: D2.2]". Verified by grep across all 14 shipped chapters.
   Ratify Ch 13's form — the trailing topic word is what keeps the tag legible given that
   domain-analysis.md:33 records the D-numbering as a Lodestar convention CNCF does not
   publish.

3. **Combined fix, no new questions:**
   Q16 -> [retrieval: ch12] [interleaved: D2.2 security]
   Q17 -> [retrieval: ch4]  [interleaved: D1.1 core concepts]
   Puts Practice at 9.5% and the chapter at 16.2%. Apply the same sweep to ch 14.

### Obligations discharged by Chapter 15 (verified by line number)

chapter-06:665 (strategy vocabulary — PARTIAL, see manifest C4/C6) ·
chapter-06:1465 ("the third time is the one that matters" — spent at §7) ·
chapter-06:1147 ("about ten seconds" — note this is Ch 6 §9, NOT §8) ·
chapter-09:1249 · chapter-05:559 (disposability) · chapter-04:722 (twelve factors) ·
chapter-12:617 (the agent as a subject) · chapter-12:485 (GitOps before the word) ·
chapter-12:866 (roleRef ordering — CURRENTLY BROKEN AT THE RECEIVING END, see manifest C2) ·
chapter-14:1387 (who applies it) · chapter-14:671 (rollback by revert) ·
section-skeleton.md:214 (charts as a manifest source — B6 mandatory anchor)

### Forward obligations Chapter 15 creates

Running/healthy/Synced/wrong -> Ch 16 · maturity LEVELS not the roster -> Ch 17 §2 ·
the control loop collected -> Ch 17 §4 (NO RUNNING ORDINAL — term-ownership.md:754) ·
service mesh as canary's precondition -> Ch 17 §5 · Knative -> Ch 17 §6 ·
twelve-factor as cloud-native predecessor -> Ch 17 §3

=== END APPEND ===
```

---

### Concept shard writes — 31 created

*Bodies are written tight. Every definitional sentence is quoted from the chapter, which quotes its source; Rule 5 forbids paraphrase, so where the chapter carries a source tag the shard carries it too.*

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/twelve-factor-app.md ===
# Concept: The twelve-factor app

A methodology for software delivered as a service. It "uses declarative formats for setup
automation… has a clean contract with the underlying operating system… is suitable for
deployment on modern cloud platforms… minimizes divergence between development and
production… and can scale up without significant changes to tooling, architecture, or
development practices." [source: twelve-factor-app-2026-08-23]

It predates Kubernetes and describes Kubernetes exactly. Not coincidence and not prophecy:
both came out of the same problem — running many applications reliably on shared
infrastructure — and reached the same conclusions.

## The twelve

I Codebase · II Dependencies · III Config · IV Backing services · V Build/release/run ·
VI Processes · VII Port binding · VIII Concurrency · IX Disposability · X Dev/prod parity ·
XI Logs · XII Admin processes [source: twelve-factor-app-2026-08-23]

## The sort that matters (fig 15.1)

| The platform gives you this | The platform makes this easy | Still your application's problem |
|---|---|---|
| III, VI, VIII, IX, XI | IV, V, X | I, II, VII, XII |

The middle column is where most disappointment lives — Kubernetes makes dev/prod parity
*achievable*, not automatic.

## ★ Fixed Point (verbatim — do not reword)

**The twelve-factor app is a set of constraints an application accepts in exchange for being
run by a platform. Kubernetes implements the platform side — config injection, stateless
replication, graceful termination, log collection. It cannot implement the application side.
An application that writes its own log files, keeps session state in memory, or takes ninety
seconds to start is not made twelve-factor by being containerized.**

## ⚠ Do not restore

Publication date, authorship, and "predates Kubernetes by three years" were removed at
revision for want of a source and must stay removed. twelve-factor-app-2026-08-23 begins at
"In the modern era, software is commonly delivered as a service" and carries no provenance.

## Related
[[factor-iii-config-in-environment]] [[factor-vi-stateless-processes]]
[[factor-ix-disposability]] [[factor-xi-logs-as-event-streams]] [[configmap]] [[pod-lifetime]]
Forward: Ch 17 §3 — several cloud-native characteristics are these factors under newer names.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/factor-iii-config-in-environment.md ===
# Concept: Factor III — config in the environment

"An app's config is everything that is likely to vary between deploys (staging, production,
developer environments, etc)." [source: twelve-factor-iii-config-2026-08-31]

## The litmus test — runnable against your own repo this afternoon

"A litmus test for whether an app has all config correctly factored out of the code is whether
the codebase could be made open source at any moment, without compromising any credentials."
[source: twelve-factor-iii-config-2026-08-31]

More honest than most compliance checklists, because it has a single unambiguous outcome.

## Three things readers get wrong

1. **"Store config in the environment" is not "put it in a config file."** A config file beats
   hard-coded constants but "still has weaknesses: it's easy to mistakenly check in a config
   file to the repo." [source: twelve-factor-iii-config-2026-08-31]
2. **It is also not literally the `env:` block.** A ConfigMap mounted as a file satisfies
   factor III: the file is supplied by the deploy environment, not committed. Readers who take
   the phrase literally wrongly conclude mounted-file config violates the methodology.
3. **Never group variables into named environments.** "In a twelve-factor app, env vars are
   granular controls, each fully orthogonal to other env vars. They are never grouped together
   as 'environments', but instead are independently managed for each deploy."
   [source: twelve-factor-iii-config-2026-08-31] This is why a `staging` bundle acquires a
   permanent load-bearing difference from `production` that nobody remembers introducing.

## The Kubernetes form

ConfigMaps and Secrets, mounted as environment variables or as files. The object model was
designed for factor III. The image is identical across environments; the object differs.

Graded three times (TYB1 Q2, TYB1 Q3, Practice Q2) — the most-tested factor in the chapter.

## Related
[[twelve-factor-app]] [[configmap]] [[secret]] [[declarative-configuration]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/factor-vi-stateless-processes.md ===
# Concept: Factor VI — stateless, share-nothing processes

"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must
be stored in a stateful backing service, typically a database."
[source: twelve-factor-vi-processes-2026-08-31]

Banned by name: "Sticky sessions are a violation of twelve-factor and should never be used or
relied upon." [source: twelve-factor-vi-processes-2026-08-31]

## Why it is the assumption underneath Deployments

A Deployment can replace any Pod with any other Pod only because this constraint holds: no Pod
carries anything the next one will need. Scale out by adding processes (factor VIII), and any
process serves any request.

## What breaks in Kubernetes when it does not hold

Two failures, and the second is the serious one. A request retrieving a file may land on a
replica that never had it — that is misplacement. And the Pod's writable layer is destroyed
with the Pod, so the data is gone at the next rollout, drain, or eviction.

## ⚠ The near-miss answer

"Factor IX, disposability" is tempting and adjacent — a Pod holding unique data is certainly
not disposable. But IX is about startup and shutdown *behaviour*; the root violation is holding
state at all, which is VI.

## When the constraint genuinely does not hold

Kubernetes has a different object, and it is a different object *because* it steps outside this
factor. Ch 6 §6 / Ch 11 §6.

## Related
[[twelve-factor-app]] [[pod-lifetime]] [[statefulset-storage]] [[pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/factor-ix-disposability.md ===
# Concept: Factor IX — disposability

"The twelve-factor app's processes are disposable, meaning they can be started or stopped at a
moment's notice." [source: twelve-factor-ix-disposability-2026-08-31]

Three clauses, all sourced:

- **Startup.** "Processes should strive to minimize startup time. Ideally, a process takes a
  few seconds from the time the launch command is executed until the process is up and ready to
  receive requests or jobs."
- **Shutdown.** "Processes shut down gracefully when they receive a SIGTERM signal from the
  process manager."
- **Sudden death.** "Processes should also be robust against sudden death, in the case of a
  failure in the underlying hardware."
[source: twelve-factor-ix-disposability-2026-08-31]

## 🪢 Mnemonic

**Fast up. Clean down. Survive the floor dropping.**

The third is the one that matters most on a real cluster: graceful shutdown is a courtesy the
platform extends when it can, and a node that loses power extends nothing.

## Promise discharged

Ch 5 §4 (chapter-05:559) taught `terminationGracePeriodSeconds` and the TERM-then-KILL sequence
and said the word was coming. This is the word.

## ⚑ Surface-form note (neither form is in the ledger)

This chapter writes `SIGTERM`/`SIGKILL`, following its source. Shipped Ch 5 §4 writes "a TERM
signal" and "they get KILL." Both defensible. Recorded so a later sweep does not normalise one
toward the other by accident.

## Related
[[twelve-factor-app]] [[restart-policy]] [[pod-lifetime]] [[probe]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/factor-xi-logs-as-event-streams.md ===
# Concept: Factor XI — logs as event streams

"Logs are the stream of aggregated, time-ordered events collected from the output streams of
all running processes and backing services." [source: twelve-factor-xi-logs-2026-08-31]

The rule is that the application does not participate in log management at all: "A twelve-factor
app never concerns itself with routing or storage of its output stream. Each running process
writes its event stream, unbuffered, to stdout." The execution environment captures the stream,
collates it, and routes it onward. [source: twelve-factor-xi-logs-2026-08-31]

## Why this is the factor with the most visible Kubernetes payoff

It is exactly why `kubectl logs` works on every container without any container being configured
for it, and why cluster-wide collection can be a node-level concern rather than an application
concern.

## What violating it costs (Practice Q1)

An app that writes to `/var/log/app.log` and rotates it itself: `kubectl logs` returns nothing
useful because stdout is empty; node-level collection sees nothing; and the logs live only in
the container's writable layer, so **the logs from the crash you are investigating died with
the thing that crashed.**

## Related
[[twelve-factor-app]] [[reading-container-logs]] [[cluster-level-logging]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/deployment-strategy-vocabulary.md ===
# Concept: Deployment strategy vocabulary

Ch 6 §4 owns the mechanics. This owns the names, the trade each makes, and one line readers
persistently get wrong.

## ★ Fixed Point (verbatim — do not reword)

**`RollingUpdate` and `Recreate` are values of a field on a Deployment. Blue/green and canary
are patterns that require tooling above the Deployment object. A Deployment cannot express
either one on its own.**

## The two field values

- **`Recreate`** — "deletes the old version of the application before bringing up the new
  version. As a result, this ensures that two versions of the application never run at the same
  time, but there is downtime during the deployment."
- **`RollingUpdate`** — "slowly replaces the old version with the new version… This is the
  default strategy of the Deployment object."
[source: argo-rollouts-strategies-2026-08-23]

The trade is stated in each definition and it is symmetric: Recreate buys the no-coexistence
guarantee with downtime; RollingUpdate buys no downtime with mandatory coexistence.

Recreate is **the correct choice rather than the lazy one** when the new version runs a schema
migration the old cannot read — there, coexistence is the failure mode.

## ⚠ A/B testing — named and bounded, not taught (see manifest ⚑ C6)

A/B is documented not as a rollout strategy but as a use of a separate resource: "A user can use
experiments to enable A/B/C testing by launching multiple experiments with a different version
of their application for a long duration." [source: argo-rollouts-experiments-2026-08-31]
That snapshot's capture note is explicit that A/B is NOT a strategy alongside the four, and the
canary page does not contain the string.

**Product experimentation asks which version users prefer, over a long duration, on purpose.
Release mechanics ask whether the new version is broken, for as short a duration as possible.**

⚑ LEDGER CONFLICT: term-ownership.md:486, section-skeleton.md:223, the acronym register, and
shipped chapter-06:665 all promise A/B as a taught strategy. The exclusion is right; the
framing ("One term this book will not teach you") collides with a promise the reader is
holding. Retitle and discharge Ch 6's promise explicitly; amend the ledger row.

## ⚠ The tooling is never named — see manifest ⚑ C4

This shard's Fixed Point says these patterns "require tooling above the Deployment" and the
chapter names no instance. Naming Argo Rollouts at §2's first shorthand fixes that AND
discharges chapter-06:665's "and the tooling that implements them."

## Related
[[blue-green-deployment]] [[canary-deployment]] [[progressive-delivery]] [[argo-rollouts]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/blue-green-deployment.md ===
# Concept: Blue/green deployment

Two complete environments; one serves production traffic. CNCF describes the operator
maintaining "blue" and "green" environments, updating the inactive one, and switching traffic
via load balancer after testing. [source: cncf-glossary-blue-green-deployment-2026-08-31]

Argo's description agrees and supplies the reason: "During this time, only the old version of
the application will receive production traffic. This allows the developers to run tests
against the new version before switching the live traffic to the new version."
[source: argo-rollouts-strategies-2026-08-23]

## The trade

**Cost:** double capacity. **Buys:** testing the new version *in production, against production
configuration and production backing services*, before one user reaches it. The cutover is one
moment, which means the rollback is also one moment.

## Needs no traffic provider

"Blue/Green needs no traffic provider and suits workloads such as queue workers."
[source: argo-rollouts-strategies-2026-08-23] This is the practical answer to "blue/green or
canary": a queue worker has no inbound traffic to proportion.

## 🔭 CNCF's assessment, which is more critical than vendor material

Blue/green "is an appropriate strategy for non-cloud native software that needs to be updated
with minimal downtime. However, its use is normally a 'smell' that legacy software needs to be
re-engineered so that components can be updated individually." The term is typically applied to
whole systems updated in lockstep and is sometimes misapplied to individual services.
[source: cncf-glossary-blue-green-deployment-2026-08-31]

## What must exist (Practice Q6)

Two complete environments running simultaneously, something controlling which receives
production traffic (Service selector, load balancer, or ingress rule), and something to flip it.
A Deployment object has neither concept.

## Related
[[deployment-strategy-vocabulary]] [[canary-deployment]] [[sync-hook-phases]] [[service-types]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/canary-deployment.md ===
# Concept: Canary deployment

"A Canary deployment exposes a subset of users to the new version of the application while
serving the rest of the traffic to the old version. Once the new version is verified to be
correct, the new version can gradually replace the old version."
[source: argo-rollouts-strategies-2026-08-23]

From the operator's side: "a canary rollout is a deployment strategy where the operator releases
a new version of their application to a small percentage of the production traffic."
[source: argo-rollouts-canary-2026-08-31]

## Why anyone bothers

"No matter how thorough the testing strategy, there are always some bugs discovered in
production. Shifting 100% of traffic from one version of an app to another can lead to more
impactful failures." [source: cncf-glossary-canary-deployment-2026-08-31]

## ★ The precondition, which is mechanical rather than cultural

Canary strategies "offer greater flexibility but demand more infrastructure (traffic-splitting
via a service mesh or ingress controller) and metric analysis."
[source: argo-rollouts-strategies-2026-08-23]

Without traffic splitting there is nowhere to send 5%. Without metrics there is nothing to abort
on. **Canary is not a better blue/green; it is a different tool that needs a request path to
work on.** Knowing why a team runs blue/green tells you more about their platform than about
their risk appetite.

## Related
[[deployment-strategy-vocabulary]] [[blue-green-deployment]] [[progressive-delivery]]
[[ingress-controller]]
Forward: Ch 17 §5 — a network that knows what it's carrying.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/progressive-delivery.md ===
# Concept: Progressive delivery

The umbrella term for the whole strategy family: "the process of releasing updates of a product
in a controlled and gradual manner, thereby reducing the risk of the release, typically coupling
automation and metric analysis to drive the automated promotion or rollback of the update."
[source: argo-rollouts-strategies-2026-08-23]

## ★ Two halves, and the second is the one that makes it more than a slow deploy

*Gradual* is the visible part — and gradual alone is just a slower deployment. A
`RollingUpdate` with a small `maxSurge` is gradual and is not progressive delivery.

*Metric analysis driving automated promotion or rollback* is what makes the release watch
itself. **Gradual buys time; metric analysis is what uses the time.**

Graded directly at Practice Q7, and again at TYB1 Q5 (the tell for canary is *proportion of
traffic* plus *automated abort on a metric*).

## ⚠ No B7 ledger row

Despite being the section's umbrella term and reaching two graded items. Add one.

## Related
[[deployment-strategy-vocabulary]] [[canary-deployment]] [[blue-green-deployment]]
[[argo-rollouts]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/argo-rollouts.md ===
# Concept: Argo Rollouts

⚑ **THIS SHARD EXISTS TO RECORD A GAP, NOT TO FILL ONE.** Created under the ch-08
`auditing.md` precedent: under the 200-word bar, but the term has no other owner and it reaches
graded material.

## What the book says

Named exactly once, in §2: "**Argo Rollouts** states the same idea from the operator's side."
Before that, four references to "Argo's description," "Argo's comparison," "Argo's
documentation." All five of §2's strategy definitions come from argo-rollouts-* snapshots.

## ⚠ The problem

A reader meets "Argo" five times in §2 and then meets "**Argo CD**" in §4 as though for the
first time. They will fuse them. **They are different tools; Argo CD does not include Argo
Rollouts.** No B7 ledger row, no glossary entry, no introduction.

## ⚠ Verified: no self-definition exists in the corpus

| Snapshot | Defines what Argo Rollouts is? |
|---|---|
| argo-rollouts-strategies-2026-08-23 | no — opens at "Progressive delivery is…" |
| argo-rollouts-canary-2026-08-31 | no |
| argo-rollouts-experiments-2026-08-31 | no — "The Experiment CRD allows users to…" |

## FIX — route 2 costs nothing

1. Fetch argo-rollouts.readthedocs.io/en/stable/ for one sentence.
2. **Free:** cncf-project-maturity-levels-2026-08-23:14 lists the graduated project as
   **"Argo"** — the umbrella. So: *"Argo Rollouts — a separate controller in the same Argo
   project as §4's Argo CD, and one concrete instance of the tooling this section says these
   patterns require."* Every clause supportable from cached metadata, and it discharges
   chapter-06:665's "and the tooling that implements them" at the same time.

## Related
[[deployment-strategy-vocabulary]] [[argo-cd]] [[progressive-delivery]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cicd.md ===
# Concept: CI, CD, and CD

Three practices bundled into one abbreviation, and the exam-relevant distinctions live in the
gaps between them.

- **CI — continuous integration.** "The practice of integrating code changes as regularly as
  possible." It "allows software teams to turn every code commit into either a concrete failure
  or a viable release candidate." [source: cncf-glossary-continuous-integration-2026-08-31]
- **CD — continuous delivery.** "A set of practices in which code changes are automatically
  deployed into an acceptance environment (or, in the case of continuous deployment, into
  production)." Includes testing procedures and a rollback path.
  [source: cncf-glossary-continuous-delivery-2026-08-31]
- **CD — continuous deployment.** "Goes a step further than continuous delivery by deploying
  finished software directly to production."
  [source: cncf-glossary-continuous-deployment-2026-08-31]

## 🪝 Snag

CNCF abbreviates **both** delivery and deployment as "CD." Genuinely ambiguous in the field, not
just on paper. When the distinction matters — and it matters exactly when the question is
whether a human approves the production step — spell the word out.

## ★ The fact that clears the ground

Kubernetes "does not deploy source code and does not build your application. Continuous
Integration, Delivery, and Deployment (CI/CD) workflows are determined by organization cultures
and preferences as well as technical requirements." [source: k8s-docs-overview-2026-08-23]

**CI and GitOps are orthogonal concerns, not stages of one thing.** A team can have excellent CI
and no GitOps, or GitOps with an entirely manual build. This is why "GitOps means running CI
from Git" (B1 trap #73) is wrong at the level of category.

## Related
[[gitops]] [[push-versus-pull-delivery]] [[opengitops-four-principles]] [[what-kubernetes-is-not]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/push-versus-pull-delivery.md ===
# Concept: Push versus pull delivery

*(Consolidates the kb_tags `push-based-delivery` and `pull-based-delivery` — the discrimination
is the content, per the `oomkilled-vs-evicted` / `tag-vs-digest` precedent.)*

**Push.** A pipeline runs outside the cluster, holds credentials *to the cluster*, and reaches
inward across the boundary to apply manifests. What most teams do first, because it is the
obvious extension of a build pipeline.

**Pull.** An agent runs *inside* the cluster, holds credentials *to a repository*, reaches
outward for desired state, and applies it locally. Nothing outside the cluster holds cluster
credentials, because nothing outside needs them.

The cluster boundary is the same line in both; the arrow is the only thing that reverses, and
everything else is a consequence of where the key sits (fig 15.3).

## The four consequences

1. **Where the credentials sit.** Push: in the CI system's secret store, often readable by
   anyone who can edit a pipeline. Pull: in a Kubernetes Secret in the cluster they apply to —
   Argo CD "stores the credentials of the external cluster as a Kubernetes Secret in the argocd
   namespace." [source: argocd-security-cluster-credentials-2026-08-31]
2. **What a compromise gets.** See [[blast-radius]].
3. **What happens between deploys.** Push: nothing — the pipeline exits and the cluster is on
   its own. Pull: the agent is still comparing. CNCF names drift first among the problems GitOps
   addresses, noting it "can be hard to detect and resolve without a source of truth governing
   it." [source: cncf-glossary-gitops-2026-08-31]
4. **What "the truth" means.** Push: whatever the last pipeline applied, reconstructible only
   from build logs. Pull: a file, in a repository, with a history of every previous answer.

## ⚠ EPISTEMIC STATUS — read before extending this shard

**No CNCF or vendor document in this chapter's corpus argues push-versus-pull as a security
question.** Consequences 2 and 3's framing are the book's reading of principle 3 plus the two
projects' documented credential storage. The chapter declares this three times (§3's "A note on
what follows," TYB2 Q3's key, Practice Q10's key). Do not let a later stage promote it.

What the corpus *does* support: credential locations, and Argo CD's access-separation argument —
"The developers who are developing the application, may not necessarily be the same people who
can/should push to production environments." [source: argocd-best-practices-2026-08-31]

## ⚠ Push is not about network topology

A self-hosted runner, a VPN, or a private CI instance all push to an API server that is not
publicly reachable. Nothing about push requires exposure (Practice Q9 distractor A).

## Related
[[gitops]] [[blast-radius]] [[opengitops-four-principles]] [[delivery-agent-identity]] [[cicd]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/blast-radius.md ===
# Concept: Blast radius

How far the damage from a single compromise extends.

A shared CI system holding write credentials for twelve clusters has a blast radius of twelve
clusters: whoever controls the pipeline controls every cluster it deploys to. Under pull, each
cluster's agent holds credentials only to its own cluster, so compromising the CI system yields
the ability to build and publish artifacts — a serious supply-chain problem — but not direct
cluster-write access anywhere.

**Pull does not prevent compromise. It bounds it.**

## ⚠ What pull does NOT change

It does not make the agent's own credentials smaller. Argo CD's default is "a clusteradmin level
role." [source: argocd-security-cluster-credentials-2026-08-31] Anyone who can commit to the
tracked branch can, transitively, do whatever the agent may do.

## ⚑ Two flags

**1. Standard vocabulary, not a Lodestar coinage.** §3 words it correctly ("This book calls that
reach the blast radius"). **Practice Q10's key overclaims:** "Blast radius is *this book's term*
for how far…" — it is widely used in security engineering. What *is* the book's is the
push-versus-pull argument the term carries. One-word fix ("this book's shorthand"), and amend
term-ownership.md:491 so no later chapter inherits the overclaim.

**2. The argument is authored.** See [[push-versus-pull-delivery]]'s epistemic-status block.

## Related
[[push-versus-pull-delivery]] [[delivery-agent-identity]] [[supply-chain-security]]
[[secret-exposure-and-hardening]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/gitops.md ===
# Concept: GitOps

★ "GitOps is a set of principles for operating and managing software systems."
[source: opengitops-principles-v1-2026-08-31]

CNCF's fuller phrasing: "a set of practices for managing software applications and
infrastructure by continuously evaluating and reconciling their desired states as defined in a
version control system such as Git against their actual state."
[source: cncf-glossary-gitops-2026-08-31]

## Problems it addresses

"Configuration drift, failed deployments, inconsistent environments, deployment failures, and
difficulty tracking historical changes." Drift is named first, and "can be hard to detect and
resolve without a source of truth governing it." [source: cncf-glossary-gitops-2026-08-31]

Benefits: "transparency and traceability of changes, reliability and security through
declarative states, and rollback, revert, and self-healing attributes."
[source: cncf-glossary-gitops-2026-08-31]

## ★ Fixed Point (verbatim — do not reword)

**GitOps is not "running CI from Git." None of the four principles mentions integration,
building, testing, or a pipeline. All four are about desired state — how it is expressed, how it
is stored, how it is obtained, and how it is applied. The build is somebody else's job, and
Kubernetes said so in its own documentation: it "does not deploy source code and does not build
your application." [source: k8s-docs-overview-2026-08-23]**

## 🔭 The name says Git; the definition does not require it

"Many version control systems can be used in GitOps as long as they meet those two basic
requirements and teams use them in a conformant manner."
[source: opengitops-1-0-announcement-2026-08-31] The announcement does not restate which two;
on this book's reading they are principle 2's immutability and complete version history — the
only pair the principles state about the store itself. Git is the overwhelmingly common choice.
The definition is about the properties, not the tool.

## ⚠ Sourcing note

"OpenGitOps is a CNCF project" is supported by opengitops-principles-v1-2026-08-31's `authority:`
metadata field only, not by body text. domain-analysis.md:262 says "CNCF **sandbox** project."
The chapter's weaker claim is the safer one; the tag is thin.

## Related
[[opengitops-four-principles]] [[push-versus-pull-delivery]] [[drift-detection]]
[[source-of-truth]] [[cicd]] [[control-loop-pointed-at-a-repository]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/opengitops-four-principles.md ===
# Concept: The four OpenGitOps principles

*(Absorbs the kb_tags `declarative-principle`, `versioned-and-immutable-principle`,
`pulled-automatically-principle`, `continuously-reconciled-principle`.)*

Desired state of a GitOps-managed system must be:

1. **Declarative** — "A system managed by GitOps must have its desired state expressed
   declaratively."
2. **Versioned and Immutable** — "Desired state is stored in a way that enforces immutability,
   versioning and retains a complete version history."
3. **Pulled Automatically** — "Software agents automatically pull the desired state declarations
   from the source."
4. **Continuously Reconciled** — "Software agents continuously observe actual system state and
   attempt to apply the desired state."
[source: opengitops-principles-v1-2026-08-31]

## ★ Two words carry the definition

**Principle 3 is why push-based CD is not GitOps.** The word is *pulled*. A pipeline that stores
manifests in Git and pushes them into a cluster satisfies 1 and 2 and fails 3 and 4 completely.
That is a perfectly reasonable thing to build. It is not GitOps, and calling it GitOps loses the
distinction the term exists to make. (B1 trap #74.)

**Principle 4 is why GitOps is not a deploy-time event.** *Continuously* observe — not "at deploy
time," not "when triggered." "The GitOps software agents have to be aware of the actual state of
a system under management and attempt to apply the desired state."
[source: opengitops-1-0-announcement-2026-08-31]

The precision is deliberate: "The wording of each principle and linked glossary item was very
carefully chosen." [source: opengitops-1-0-announcement-2026-08-31]

## ★ Only ONE of the four is new to a reader of this book

| # | Where you already met it |
|---|---|
| 1 Declarative | Ch 4 §1 — you file a declaration |
| 2 Versioned and immutable | **NEW.** A property of the *store*, not of Kubernetes |
| 3 Pulled automatically | Ch 3 §5 — the watch; the direction was never inward |
| 4 Continuously reconciled | Ch 3 §6 — the loop, word for word |

etcd holds the current desired state. A repository holds every desired state there has ever
been, in order, each one fixed. **That difference is what makes rollback by revert possible at
all: you cannot return to a state your store did not keep.**

## ⚠ Principle 3 pulls, but does not distinguish observation from correction

Principle 4 requires continuous *observation*. What the agent then *does* about a difference is
configuration — and Argo CD and Flux ship opposite defaults. See [[self-heal]].

## Related
[[gitops]] [[control-loop]] [[control-loop-pointed-at-a-repository]] [[declarative-configuration]]
[[api-server-hub]] [[rollback-by-revert]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/source-of-truth.md ===
# Concept: Source of truth

The authored desired state, upstream of the cluster, which the agent keeps the cluster in
agreement with by ordinary API calls.

## ⚠ Navigational Hazard — the misreading the phrase invites

**A GitOps agent does NOT write to the cluster's datastore directly, and does not bypass the API
server.**

Readers hear "the repository is the source of truth" and picture the repository *replacing*
etcd. It does not. etcd still holds every object. What Git holds is the *authored* desired
state, and the agent's job is to keep the two in agreement.

Chapter 3's claim has held for twelve chapters: the API server is the only thing that mutates
cluster state, and every actor goes through it. A delivery agent is an API client like any
other. Its requests pass through authentication, then authorization, then admission, in that
order, exactly as yours do.

## The consequence you can act on

An agent lacking RBAC permission to create a resource fails to create it, with an ordinary
authorization error. **GitOps grants no exemption from any cluster control.** If anything it is
*more* constrained than a human operator, because its permissions are written down.

## What "the truth" means under each model

Under push, the authoritative answer to "what is supposed to be running" is whatever the last
pipeline applied — a fact you reconstruct from build logs. Under pull it is a file, in a
repository, that anyone can read, with a history showing every previous answer.

## Related
[[api-server-hub]] [[api-access-gates]] [[gitops]] [[rbac]] [[delivery-agent-identity]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/drift-detection.md ===
# Concept: Drift and reconciliation

**Drift** — "When a system's actual state has moved or is in the process of moving away from the
desired state…" [source: opengitops-glossary-2026-08-31]

**Reconciliation** — "The process of ensuring the actual state of a system matches its desired
state." [source: opengitops-glossary-2026-08-31] Flux's form: "ensuring that a given state (e.g.
application running in the cluster, infrastructure) matches a desired state declaratively
defined somewhere (e.g. a Git repository)." [source: flux-concepts-2026-08-31]

⚠ **The OpenGitOps drift definition is truncated in the snapshot** — the ellipsis is the
capture's. Its note says explicitly: "treat the truncated definitions as partial and do not
extend them from memory." The chapter honours this; so must any later stage.

## Why drift is invisible without a source of truth

The canonical shape (§3's Logbook Entry): a correct, thirty-second `kubectl edit` on a Friday
afternoon, never written down because writing it down was the slow path being avoided. Six weeks
later a routine deployment applies manifests that never knew about it. The field reverts, the
original problem returns, and the change log points at an unrelated commit.

Push-based delivery has no mechanism that would catch this — the pipeline was not running for
those six weeks and had nothing to compare against if it had been.

**Under a GitOps agent, that edit produces an `OutOfSync` status within one reconciliation
interval. Not an alert, not a page, not a failure. A status field, changed. The mechanism that
catches the story is not an alarm — it is a comparison that never stops running.**

## ⚑ Ledger amendment needed

term-ownership.md:497 assigns "Drift · drift detection" to Ch 15 §4. The chapter defines drift
in **§3** (with the principles, where it belongs — drift is what principle 4 exists to catch)
and does detection in §4. Amend the row to `§3 (definition) / §4 (detection)`; do not move the
chapter.

## Related
[[synced-outofsync]] [[self-heal]] [[opengitops-four-principles]] [[gitops]] [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/argo-cd.md ===
# Concept: Argo CD

A "declarative, GitOps continuous delivery tool for Kubernetes."
[source: argocd-overview-2026-08-23]

## ★ The most important sentence in the chapter

The application controller "is a Kubernetes controller which continuously monitors running
applications and compares the current, live state against the desired target state (as specified
in the repo)." [source: argocd-architecture-2026-08-31]

Read it as three separate claims:

- *is a Kubernetes controller* — the thing Ch 3 §6 defined
- *continuously monitors and compares current against desired* — the thing Ch 3 §6 said
  controllers do
- *desired target state as specified in the repo* — **the only part that is new**

## ★ Fixed Point (verbatim — do not reword)

**A GitOps delivery agent is a controller. Its desired state lives in a repository instead of in
etcd. Nothing else about the architecture is different — not the API server's position, not the
watch-based coordination, not the shape of the loop.**

## Three components, not one process

An API server, a **repository server**, and an application controller.
[source: argocd-architecture-2026-08-31] "Integrated" describes the product surface, not the
process count — a distractor Practice Q21 grades.

## ⚠ First appearance is Ch 3 §5, not §6

Argo CD is named once in shipped Chapter 3, at chapter-03:653, inside §5 "The Only Door In"
(610–749). §6 (750–836) contains no mention of it. The draft's cross-bearing points at §6 and
must be retargeted; the three subsequent "the thing Chapter 3 §6 defined" references are correct
and should stay.

## Structural point worth carrying

This is a controller acting on custom resources — precisely the thing Ch 6 §8 said you could
build. **It is not a new category of technology. It is the category you were taught, aimed
somewhere unexpected.**

## Related
[[control-loop]] [[argo-cd-application-resource]] [[synced-outofsync]] [[manifest-source]]
[[custom-resource]] [[operator-pattern]] [[flux]] [[argo-rollouts]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/argo-cd-application-resource.md ===
# Concept: The Argo CD `Application`

★ "A group of Kubernetes resources as defined by a manifest. This is a Custom Resource
Definition (CRD)." [source: argocd-core-concepts-2026-08-31]

More precisely: "The Application CRD is the Kubernetes resource object representing a deployed
application instance in an environment." [source: argocd-declarative-setup-2026-08-31]

## Two pieces of information, and that is the whole contract

- a "source reference to the desired state in Git (repository, revision, path, environment)"
- a "destination reference to the target cluster and namespace"
[source: argocd-declarative-setup-2026-08-31]

**This content, from there, goes there.**

## ★ The absent-component pattern, in its cleanest instance in the book

Installing the CRD extends the API so `Application` objects can *exist*. Whether anything
*happens* to them depends entirely on whether the application controller is running.

**An `Application` on a cluster with no Argo CD controller is a stored document. It describes a
deployment that will never occur.**

⚑ Note for the Ch 17 §4 collection: Chapter 15 **applies** this pattern and points at Ch 10 §3
rather than restating either canonical string. So it neither repeats Ch 13's drifted form nor
re-fights it. The drift remains confined to Chapter 13.

## Related
[[absent-component-pattern]] [[custom-resource]] [[argo-cd]] [[manifest-source]]
[[tracking-branch-tag-commit]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/manifest-source.md ===
# Concept: Manifest sources

An `Application`'s source is a repository path, but the content there need not be plain YAML.
Argo CD accepts manifests "in several ways: kustomize applications; helm charts; jsonnet files;
plain directory of YAML/json manifests; any custom config management tool configured as a config
management plugin." [source: argocd-overview-2026-08-23]

The vocabulary: **application source type** is "which Tool is used to build the application";
a **tool** is "a tool to create manifests from a directory of files. E.g. Kustomize"; a
**configuration management plugin** is "a custom tool."
[source: argocd-core-concepts-2026-08-31]

## 🪝 "Argo CD only deploys plain YAML" (B1 trap #77)

A confident mistake, usually from having seen one tutorial. **Rendering is not an add-on; it is
a whole component.** The repository server "maintains a local cache of the Git repository holding
the application manifests" and is responsible for "generating and returning the Kubernetes
manifests" given a repository URL, revision, path, and template-specific configuration.
[source: argocd-architecture-2026-08-31]

⚠ **repository server** has no B7 ledger row and is required by name in Practice Q14's key.

## Where Chapter 14's work gets collected — B6 MANDATORY ANCHOR

section-skeleton.md:214 records this as one of two anchors that "may not be dropped": charts as
an Argo CD manifest source. Discharged here. A Helm chart is a manifest source; so is a Kustomize
overlay. **Chapter 14 gave you packaging; this gives packaging somewhere to go.** The agent
renders the chart or builds the overlay and compares the *result* against the cluster.

## Flux's version of the same idea, elevated to an API

"A Source defines the origin of a repository containing the desired state of the system and the
requirements to obtain it (e.g. credentials, version selectors)."
[source: flux-concepts-2026-08-31] The source controller produces an artifact; other controllers
consume it. `OCIRepository` and `HelmRepository` sit alongside `GitRepository`.

## Related
[[helm-chart]] [[kustomize]] [[base-and-overlay]] [[chart-repository]] [[oci]]
[[flux-controller-set]] [[distribute-versus-adapt]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/synced-outofsync.md ===
# Concept: `Synced`, `OutOfSync`, and the two questions

*(Absorbs target state, live state, sync, refresh, and sync operation status — the five Argo CD
glossary entries are one comparison and its vocabulary.)*

- **Target state** — "The desired state of an application, as represented by files in a Git
  repository."
- **Live state** — "The live state of that application. What pods etc are deployed."
- **Sync status** — "Whether or not the live state matches the target state. Is the deployed
  application the same as Git says it should be?"
- **Sync** — "The process of making an application move to its target state."
- **Refresh** — "Compare the latest code in Git with the live state. Figure out what is
  different."
- **Sync operation status** — "Whether or not a sync succeeded."
[source: argocd-core-concepts-2026-08-31]

★ **Refresh compares. Sync acts.** They are separate words because a system can know it is out
of agreement without doing anything about it.

## ★ Fixed Point (verbatim — do not reword)

**`OutOfSync` means live state deviates from the target state in Git. It is a drift signal, not
an error. Nothing has necessarily failed. A person editing an object by hand produces an
`OutOfSync` application, and so does a commit that has not been applied yet.**

"A deployed application whose live state deviates from the target state is considered
OutOfSync." [source: argocd-overview-2026-08-23] (B1 trap #76.)

## Two fields, two questions, one of which readers collapse

Sync status and sync **operation** status are separate glossary entries. The documentation states
the combination outright: "It is possible for an application to be `OutOfSync` even immediately
after a successful Sync operation." [source: argocd-diffing-outofsync-2026-08-31]

⚠ **NO CAUSE MAY BE ATTRIBUTED TO THAT SNAPSHOT.** Its capture note records that the page's
enumerated causes were returned as summary rather than quotation. The chapter correctly states
the claim without naming one; a full re-fetch would let §4 name a concrete cause.

## ★ Anchor to Chapter 4 under pressure

**Target state is `spec`, kept outside the cluster. Live state is what `status` reports.** The
one refinement: in an ordinary object, `spec` and `status` are two fields of one record in etcd.
Under GitOps the authored `spec` lives outside the cluster entirely — which is why an object's
own `spec` can be perfectly satisfied while the application is `OutOfSync`.

## ★ The default is the Fixed Point's best proof

If `OutOfSync` were an error, a tool would not sit there reporting it. See [[self-heal]].

## Related
[[spec]] [[status]] [[drift-detection]] [[self-heal]] [[argo-cd]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/self-heal.md ===
# Concept: Self-heal and prune

Reporting a difference and correcting it are separate decisions, and Argo CD keeps them separate
— including in what it does when you say nothing.

"Argo CD has the ability to automatically sync an application when it detects differences between
the desired manifests in Git, and the live state in the cluster."
[source: argocd-auto-sync-policy-2026-08-31] Configured declaratively, which is itself in
keeping: the agent's own behaviour is a field on an object in the repository.

## ⚠ Out of the box, Argo CD reports drift. It does not revert it.

- **Self-healing is off by default.** "By default, changes that are made to the live cluster will
  not trigger automated sync." [source: argocd-auto-sync-policy-2026-08-31] Until you enable it,
  a hand-edited object stays hand-edited.
- **Pruning is off by default.** "By default (and as a safety mechanism), automated sync will not
  delete resources when Argo CD detects the resource is no longer defined in Git."
  [source: argocd-auto-sync-policy-2026-08-31]
- **Fires only on a difference.** "An automated sync will only be performed if the application is
  `OutOfSync`." [source: argocd-auto-sync-policy-2026-08-31]
- **Not instantaneous.** The interval "defaults to `120s` with added jitter of `60s` for a
  maximum period of 3 minutes." [source: argocd-auto-sync-policy-2026-08-31]

## ⚠ "Every GitOps agent reverts manual changes" is false

Flux "promptly reverts" manual `kubectl` changes [source: flux-concepts-2026-08-31]; Argo CD, by
default, does not. **Two graduated implementations of the same four principles ship with opposite
defaults.** Principle 4 requires continuous *observation*; what the agent then *does* is
configuration.

## ⚠ Permission and configuration are different things

The agent must hold the `delete` verb before it can prune, but holding it does not make it prune.
Graded on that distinction twice (TYB2 Q4, Practice Q16). ⚠ `prune` has no B7 ledger row.

## Practical consequence

Under continuous reconciliation with self-heal on, an emergency fix must be committed to survive.
The tool is not being obstructive; it is doing the job it was installed for. A team that finds
this intolerable during incidents needs a documented way to **suspend** reconciliation, not a
workaround.

## Related
[[synced-outofsync]] [[drift-detection]] [[flux]] [[opengitops-four-principles]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/tracking-branch-tag-commit.md ===
# Concept: Tracking a branch, a tag, or a commit

An `Application` names a revision as well as a repository, and the three kinds differ in
stability.

- **Branch or symbolic reference** (incl. `HEAD`): "Argo CD will continually compare live state
  against the resource manifests defined at the tip of the specified branch or the resolved
  commit of the symbolic reference." The tip moves; so does your target.
- **Tag:** "If a tag is specified, the manifests at the specified Git tag will be used to perform
  the sync comparison." Tags are "generally considered more stable, and less frequently updated."
- **Pinned commit:** "the app is effectively pinned to the manifests defined at the specified
  commit… Since commit SHAs cannot change meaning, the only way to change the live state of an
  app which is pinned to a commit, is by updating the tracking revision in the application to a
  different commit containing the new manifests."
[source: argocd-tracking-strategies-2026-08-31]

## 🪢 Mnemonic

**Branch moves. Tag rarely moves. Commit never moves.** Pick according to how much you want the
deck under your production cluster to shift without a commit of your own.

## Principle 2 as an operational property

Argo CD's best-practices page makes the same argument against tracking an unstable revision:
manifests "can suddenly change meaning, even without any changes to your own Git repository. A
better version would be to use a Git tag or commit SHA."
[source: argocd-best-practices-2026-08-31]

Pinning also makes the *change itself* reviewable: somebody must edit the `Application`'s own
revision field, which is itself typically a commit in a repository. That is the point of pinning.

## ⚠ Terminology

Argo CD's API field is called `revision`. In this book, a Git revision is a **commit** —
*revision* already has two owners (a Deployment revision, a Helm release revision).

B1 trap #78: "Argo CD can only track a branch."

## Related
[[argo-cd-application-resource]] [[opengitops-four-principles]] [[helm-release-revision]]
[[rollback-by-revert]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/rollback-by-revert.md ===
# Concept: Rollback by revert

Argo CD offers "rollback/roll-anywhere to any application configuration committed in Git
repository." [source: argocd-overview-2026-08-23]

## ★ What is actually happening

You do not invoke a rollback subsystem. You change what the repository says — typically with
`git revert`, producing a new commit whose content is the old content — and the agent does what
it has been doing continuously since it started: it notices the target moved and closes the gap.

**The rollback mechanism IS the sync mechanism. There is no second code path.**

## The third mechanism to wear the word

| | What moves | Where the previous state was kept |
|---|---|---|
| `kubectl rollout undo` (Ch 6 §5) | the Deployment's Pod template | the old ReplicaSet, on the cluster |
| `helm rollback` (Ch 14 §3) | the Helm release to a prior revision | Helm's release history, on the cluster |
| **rollback by revert** (Ch 15 §4) | a commit in the repository | the repository's history |

## ⚠ Canonical form is mandatory

The B7 ledger (term-ownership.md:854) requires the exact unhyphenated three-word form **rollback
by revert**. Chapter 15 complies throughout. Shipped chapter-14:671 writes it hyphenated and is
the outlier — cosmetic sweep item for Ch 14, author's call.

## ⚠ Do not call the reverted thing a "revision"

A Git revision is a **commit**. Argo CD's own API field is named `revision`, which is why this
needs saying rather than assuming.

## Promise discharged

chapter-06:714 said the word would appear twice more; Ch 14 §3 spent the first, this is the
second and last. (Ch 6 does not characterise the third instance as "a delivery tool" — §4's
phrasing overstates slightly; "pointed at Chapter 14 and at this chapter" is exact.)

## Related
[[helm-rollback-versus-rollout-undo]] [[helm-release-revision]] [[synced-outofsync]]
[[opengitops-four-principles]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/delivery-agent-identity.md ===
# Concept: The delivery agent's own identity

A delivery agent is a Pod. A Pod that talks to the API server needs a ServiceAccount. Kubernetes
lists this use explicitly: "an external service needs to communicate with the Kubernetes API
server (CI/CD pipelines)." [source: k8s-docs-service-accounts-2026-08-23]

Then ask what this Pod does for a living: it creates, updates, and deletes objects — Deployments,
Services, ConfigMaps, RBAC objects, custom resources — across many namespaces, on behalf of
whatever is committed to a repository. **Its grants must be broad, because "apply whatever the
repository says" is a broad job description.**

## The documented default, and the documented reduction

"By default, Argo CD uses a clusteradmin level role in order to: 1. watch & operate on cluster
state 2. deploy resources to the cluster."

"Although Argo CD requires cluster-wide read privileges to resources in the managed cluster to
function properly, it does not necessarily need full write privileges to the cluster." Operators
may edit the ClusterRole `argocd-manager-role` "such that write privileges are limited to only
the namespaces and resources that you wish Argo CD to manage."
[source: argocd-security-cluster-credentials-2026-08-31]

★ **Note the asymmetry: cluster-wide READ is structural** — the agent cannot detect drift in what
it cannot see — **while broad WRITE is a default, not a requirement.**

External-cluster credentials are ordinary objects: "the K8s API bearer token associated with the
`argocd-manager` ServiceAccount created during `argocd cluster add`, along with connection
options to that API server," stored as a Secret in the `argocd` namespace.
[source: argocd-security-cluster-credentials-2026-08-31]

## ⚠ Navigational Hazard — the reasoning that goes wrong

"GitOps is more secure than push, therefore the agent is a security improvement, therefore I do
not need to think about it." The first clause is the book's blast-radius argument, not a
documented finding — and the conclusion does not follow from it in any case. **Pull moves the
credentials inside the cluster; it does not make them smaller.**

★ **Anyone who can commit to the tracked repository can, transitively, do whatever the agent may
do. So branch-protection rules ARE an access-control mechanism, exactly as load-bearing as your
RBAC policy. Not a metaphor.**

## Flux solves the same problem differently

Broad role retained, narrower identity impersonated per workload:
`.spec.serviceAccountName` specifies "the ServiceAccount to be impersonated while reconciling."
[source: flux-kustomization-api-2026-08-31]

## Promise discharged
chapter-12:617 — "a shape you will meet again."

## Related
[[serviceaccount]] [[serviceaccounts-and-identity]] [[rbac]] [[blast-radius]] [[secret]]
[[additive-never-deny]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/sync-hook-phases.md ===
# Concept: Sync phases and hooks

A sync runs in phases, and hooks attach to them:

- **PreSync** — "prior to the application of the manifests"
- **Sync** — "after all PreSync hooks completed and were successful, at the same time as the
  application of the manifests"
- **PostSync** — "after all Sync hooks completed and were successful, a successful application,
  and all resources in a Healthy state"
- **SyncFail** — "when the sync operation fails"
[source: argocd-sync-phases-and-waves-2026-08-31]

Phase execution is strictly ordered and gated on success. A PreSync failure stops the process; a
Sync failure marks the operation failed and triggers SyncFail hooks; a PostSync failure marks the
deployment failed. [source: argocd-sync-phases-and-waves-2026-08-31]

## How to read them

**PreSync = "this must be finished before anything else changes"** — the database migration, the
schema check.
**PostSync = "this runs only if everything else worked AND is healthy"** — the smoke test, the
notification, the traffic cutover.

## ★ The health gate is the part readers miss

PostSync is not "after the apply." It is "after the apply worked and the result is healthy."

## Where §2 and §5 join

Argo CD ties hooks to the strategy vocabulary directly: "PreSync, Sync, PostSync hooks to support
complex application rollouts (e.g. blue/green and canary upgrades)."
[source: argocd-overview-2026-08-23] §2 said blue/green and canary need tooling above the
Deployment. **Hooks are part of how that tooling is built** — a PostSync hook is the natural
place for "now switch the traffic."

## Related
[[sync-wave]] [[blue-green-deployment]] [[canary-deployment]] [[probe]]
[[deployment-strategy-vocabulary]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/sync-wave.md ===
# Concept: Sync waves

Phases are coarse. Within a phase, resources carry an integer that determines order.

"Hooks and resources are assigned to wave 0 by default. The wave can be negative, so you can
create a wave that runs before all other resources." Lower values sync first. The mechanism is
the annotation `argocd.argoproj.io/sync-wave`, taking an integer.
[source: argocd-sync-phases-and-waves-2026-08-31]

Ordering precedence: "1. The phase 2. The wave they are in (lower values first)", with two
further deterministic tie-breaks. [source: argocd-sync-phases-and-waves-2026-08-31]
**Phase first, then wave. Everything you can control is in those two lines.**

## ⚠ Relative ordering, not absolute positions

`-5` and `0` order exactly as `0` and `1` do. There is no requirement to use consecutive integers
or to start anywhere in particular. Readers who treat the number as a slot invent constraints the
mechanism does not have. The negative-wave capability is what makes waves an ordering system
rather than a queue — you can insert ahead of the default without renumbering.

## The problem waves exist for

GitOps does not inherit `kubectl apply -f`'s ordering fix; it inherits the problem at larger
scale. A namespace before the things inside it; a CRD before any custom resource that uses it; a
migration before the version expecting the new schema.

## ⚠ RESTORE THE CH 12 EXAMPLE — see manifest ⚑ C2

The `roleRef`-immutability illustration was removed at revision for want of a source. **The
source exists** — "After you create a binding, you cannot change the Role or ClusterRole that it
refers to" [source: k8s-docs-rbac-2026-08-23] — and shipped chapter-12:866 already states it
correctly and emits a forward pointer INTO this section. As drafted, that pointer lands on "it is
a good illustration" followed by no illustration. Restore one sentence: a binding's `roleRef` is
immutable, so changing which role a binding grants is a delete-and-recreate — a real ordering
constraint for a system reconciling a whole repository against a whole cluster.

## Scope honesty

§5 is marked 🟡 Advanced and says so. The annotation is here for concreteness, **not for
memorization**; no question in the chapter asks you to write one.

## Related
[[sync-hook-phases]] [[crds-in-charts]] [[custom-resource]] [[rbac]] [[namespace]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/flux.md ===
# Concept: Flux

A **GitOps Toolkit**: "a collection of specialized tools, Flux Controllers, composable APIs, and
reusable Go packages available under the fluxcd GitHub organization."
[source: flux-concepts-2026-08-31] The earlier capture is blunter: "Flux is a GitOps Toolkit: a
set of composable APIs and specialized tools that can be used to build Continuous Delivery on top
of Kubernetes." [source: flux-concepts-2026-08-23]

## The contrast with Argo CD is packaging, not capability

Argo CD presents as one integrated product with a single `Application` resource and one UI. Flux
presents as controllers you assemble, each owning its own custom resources. Neither is better:
integration gives one thing to learn and one console; composition gives pieces you can adopt and
replace independently. **Teams pick on organizational grounds more than technical ones.**

⚠ "Composable" does not mean "less capable," and "integrated" does not mean "one process" —
Argo CD sits on three components. [source: argocd-architecture-2026-08-31]

## ★ The most concrete statement of principle 4 in the book

"The reconciliation runs every five minutes by default, but this can be changed with
`.spec.interval`." And: "If you make any changes to the cluster using `kubectl edit/patch/delete`,
they will be promptly reverted." [source: flux-concepts-2026-08-31]

**Continuous reconciliation is not a scheduling detail. Your manual change has a shelf life
measured in minutes.**

⚠ **Qualify the number.** The `Kustomization` API states `.spec.interval` is "a required field…
The minimum value should be 60 seconds" and declares **no API-level default**.
[source: flux-kustomization-api-2026-08-31] So "five minutes by default" describes Flux's
bootstrap-generated Kustomization, not an API default. The chapter's walk-back is correct and is
better than its own source's headline. **The durable answer is the behaviour, not the number.**

## Bootstrap — Flux installs itself the way it installs everything else

"The process of installing the Flux components in a GitOps manner is called a bootstrap. The
manifests are applied to the cluster, a `GitRepository` and `Kustomization` are created for the
Flux components, then the manifests are pushed to an existing Git repository."
[source: flux-concepts-2026-08-31] — so that "Flux manages itself like any other resource."
[source: flux-concepts-2026-08-23] **Upgrading Flux is a commit.**

## Security model

A `crd-controller` ClusterRole has "full access to all the Custom Resource Definitions defined by
Flux controllers"; a `cluster-reconciler` ClusterRoleBinding references `cluster-admin`, bound "to
service accounts for only `kustomize-controller` and `helm-controller`" because those "are the
only two controllers that manage resources in the cluster." Reduction is by **impersonation**:
Flux uses "the Kubernetes Impersonation API under `cluster-admin` to impersonate that service
account." [source: flux-security-2026-08-31]

**Same problem as Argo CD's, different route: Argo CD narrows the ClusterRole; Flux keeps the
broad role and impersonates a narrower identity per workload.**

## Related
[[flux-controller-set]] [[argo-cd]] [[self-heal]] [[multi-cluster-delivery]]
[[delivery-agent-identity]] [[kustomize]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/flux-controller-set.md ===
# Concept: The Flux controller set

| Controller | Its custom resources |
|---|---|
| Source | `GitRepository`, `OCIRepository`, `HelmRepository`, `HelmChart`, `Bucket`, `ExternalArtifact`, `ArtifactGenerator` |
| Kustomize | `Kustomization` |
| Helm | `HelmRelease` |
| Notification | `Provider`, `Alert`, `Receiver` |
| Image Reflector / Image Automation | `ImageRepository`, `ImagePolicy`, `ImageUpdateAutomation` |
[source: flux-components-2026-08-31]

★ **What is worth carrying is the shape — one controller per concern, each with its own API —
not the roster.** The source controller alone carries seven resources.

## ⚠ Snapshot constraint

flux-components-2026-08-31's capture note is explicit: it carries only controller names, linked
doc titles, and CRD lists. **"Do not attribute behavioural claims to this snapshot."** The
chapter cites it only for the roster, which is correct.

## The Kustomization API

"The `Kustomization` API defines a pipeline for fetching, decrypting, building, validating and
applying Kustomize overlays or plain Kubernetes manifests."
[source: flux-kustomization-api-2026-08-31] `.spec.prune` is "a required boolean field to
enable/disable garbage collection" — note that Flux makes this decision *mandatory* where Argo CD
defaults it off.

## Chapter 14 collected

`OCIRepository` and `HelmRepository` are source kinds, so Ch 14's charts-in-OCI-registries work
and Ch 2's registry work both land here as ordinary configuration.

## Related
[[flux]] [[kustomize]] [[base-and-overlay]] [[oci]] [[chart-repository]] [[custom-resource]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/multi-cluster-delivery.md ===
# Concept: Multi-cluster delivery

Where does desired state live when there are twenty clusters?

**Argo CD's answer is documented and is a control point.** Among its features is the "ability to
manage and deploy to multiple clusters" [source: argocd-overview-2026-08-23], with each external
cluster's credentials stored as a Secret in the `argocd` namespace of the managing cluster
[source: argocd-security-cluster-credentials-2026-08-31]. One Argo CD, many destinations, one
place to look — and one place holding credentials to everywhere.

**Flux's documented position is narrower, and the honest statement is the narrow one.** Its
reconciling controllers run *in* the cluster they reconcile [source: flux-security-2026-08-31],
and bootstrap installs Flux into a cluster against a Git repository
[source: flux-concepts-2026-08-31]. There is no equivalent documented mechanism for one Flux
storing credentials to other clusters.

## ⚠⚠ DO NOT OVER-CLAIM THE FLUX SIDE

An earlier draft asserted "one Flux per cluster, each bootstrapped into its own repository or
path and pulling independently, **with no cluster holding credentials to another**," tagged to
flux-concepts-2026-08-31. That snapshot describes bootstrap on a single cluster and says nothing
about multi-cluster topology or cross-cluster credentials. **The tag was a mis-attribution and
the absolute had no basis in either direction.** Both the body text and Practice Q21's key are
now correctly reduced.

**flux-security-2026-08-31's soft multi-tenancy material is about tenants WITHIN one cluster and
must not be read across to multi-cluster.**

To restore the fuller comparison, cache fluxcd.io's multi-cluster / multi-tenancy guide.

## The trade (the book's argument, at larger scale)

A single control point gives one console to reason about and one component whose compromise
reaches every destination it holds credentials for. Per-cluster agents give isolation and no
unified view. See [[blast-radius]]'s epistemic-status note.

## Related
[[flux]] [[argo-cd]] [[blast-radius]] [[delivery-agent-identity]] [[secret]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop-pointed-at-a-repository.md ===
# Concept: The control loop, pointed at a repository  ☀️ THE BOOK'S PRIMARY ZENITH

**This section teaches nothing new. That is not modesty and it is not a warning; it is the
design.**

## The substitution, performed slowly

A controller holds a **desired state**. It observes the **current state**. When they differ it
acts to close the gap. Then it checks again. There is no completion condition, no final state, no
moment at which it decides its work is finished and exits. (Ch 3 §6.)

In Chapter 3, desired state was in etcd, reached through the API server.

**Now move it. Take the desired state out of etcd and put it in a Git repository.**

## What did NOT move

- **The API server is still the only mutator.** The agent writes as an API client, through
  authentication, authorization, and admission. (Ch 3 §5.)
- **The coordination is still watching, not telling.** Nothing pushes work to the controller.
- **The controller is still shaped the same way.** Compare, act, repeat.
- **Reconciliation is still endless.** A ReplicaSet does not finish. Neither does this.

**One box changed contents. That is the entire technical delta between "Kubernetes" and
"GitOps."**

## Why the chapter is called what it is

The chart is the truth, but not because a file is inherently authoritative. Files are only ever
claims. **The chart is the truth because something is continuously making it true. The authority
is not in the file. It is in the loop that never stops comparing the file to the world and acting
on the difference.**

## ⚑⚑ SHIP-BLOCKER — the figure pair. Highest-risk open item in the chapter.

The BINDING contract states the requirement directly: §7 "re-presents `ch03-fig02` with Git
substituted for etcd as the desired-state store. Owns no new material — the payoff is
recognition, and **it fails if the figure does not visually rhyme with Ch 3 §6's**."
[section-skeleton.md:228]

Four contracts stake the book's payoff on it: chapter-06:1465 ("the third time is the one that
matters"), chapter-09:1249 ("the structural claim this whole book is building toward"),
chapter-14's Voyage Ahead ("the one this book has been saving"), and the skeleton above.

**As drawn they are not the same drawing.** `ch03-fig02` is DESIRED → COMPARE → ACT → CURRENT
(four boxes, no controller node, no API server). This one is DESIRED → CONTROLLER → API SERVER →
CURRENT. The caption asks the reader to lay them side by side and see one box changed; that claim
is not checkable by a reader who flips back, and the Zenith depends on it being literally
checkable.

**Redraw `ch03-fig02` onto this chapter's chassis.** It costs a Chapter 3 edit and it is the only
resolution that preserves what four contracts promised. Redrawing this figure onto Ch 3's chassis
loses the API-server node §3's Navigational Hazards depends on. Commission and render the two as
a pair, on one chassis, so they superimpose.

## ⚠ NO RUNNING ORDINAL — book-level rule

term-ownership.md:754: no chapter may assert "the fourth time," "the sixth control loop," etc.
**Ch 6's two-altitudes framing and this Zenith are the only sanctioned control-loop count in the
book.** Chapter 15 complies and spends Ch 6's reserved "third time" here, correctly. Ch 17 §4
collects the thread and must add nothing to the count.

⚠ The "ten seconds" callback is at **chapter-06:1147, inside Ch 6 §9** (1101–1153), not §8
(969–1041). Retarget the cross-bearing.

## Related
[[control-loop]] [[opengitops-four-principles]] [[api-server-hub]] [[declarative-configuration]]
[[package-not-template]] [[gitops]]
=== END WRITE ===
```

### Concept shard appends — 33 amended

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

## Chapter 15 update (2026-08-31) — ⚑⚑ THE BOOK'S PRIMARY ZENITH LANDS HERE

Chapter 15 §7 performs the loop's final and largest substitution: **desired state moves out of
etcd and into a Git repository, and nothing else about the architecture changes.**

Argo CD's application controller "is a Kubernetes controller which continuously monitors running
applications and compares the current, live state against the desired target state (as specified
in the repo)." [source: argocd-architecture-2026-08-31] Three claims: it is the thing Ch 3 §6
defined; it does the thing Ch 3 §6 said controllers do; **only the location of the desired state
is new.**

⚠ **NO ORDINAL — the instruction on this shard from ch-09's Stage 14 stands, and Ch 15 is the
reason it exists.** term-ownership.md:754 sanctions exactly two control-loop counts in the whole
book: Ch 6's two-altitudes framing, and Ch 15 §7's "third time." Chapter 15 spends the reserved
third correctly and adds nothing. **Ch 17 §4 collects the thread and must not add to the count.**

⚑ **SHIP-BLOCKER inherited:** the §7 figure must visually rhyme with `ch03-fig02`, and as drawn
it does not. See [[control-loop-pointed-at-a-repository]].

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/status.md ===

## Chapter 15 update (2026-08-31) — the strongest single extension of this shard

This shard carries the rule Ch 13 depended on: **a gap between spec and status is not a fault.**
Chapter 15 is that rule at book scale.

Argo CD's **live state** — "the live state of that application. What pods etc are deployed"
[source: argocd-core-concepts-2026-08-31] — is what `status` reports on, and `OutOfSync` is the
report that live state and target state differ.

★ **`OutOfSync` is a drift signal, not an error. Nothing has necessarily failed.** A person
editing an object by hand produces one. A commit not yet applied produces one. And a successful
sync can leave one: "It is possible for an application to be `OutOfSync` even immediately after a
successful Sync operation." [source: argocd-diffing-outofsync-2026-08-31]

The refinement worth carrying: in an ordinary object, `spec` and `status` are two fields of one
record in etcd. Under GitOps the authored `spec` lives **outside the cluster entirely** — which
is why an object's own `spec` can be perfectly satisfied while its application is `OutOfSync`.

Related: [[synced-outofsync]] [[spec]] [[drift-detection]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/spec.md ===

## Chapter 15 update (2026-08-31)

**Target state is `spec`, relocated.** "The desired state of an application, as represented by
files in a Git repository." [source: argocd-core-concepts-2026-08-31]

Ch 15 §4's anchor for readers who confuse target and live state under pressure: *target state is
`spec`, kept outside the cluster; live state is what `status` reports.* Argo CD's central
comparison is the one this shard has described since Chapter 4, with one operand moved.

Related: [[synced-outofsync]] [[status]] [[source-of-truth]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\cert```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/spec.md ===

## Chapter 15 update (2026-08-31)

**Target state is `spec`, relocated.** "The desired state of an application, as represented by
files in a Git repository." [source: argocd-core-concepts-2026-08-31]

Ch 15 §4's anchor for readers who confuse target and live state under pressure: *target state is
`spec`, kept outside the cluster; live state is what `status` reports.* Argo CD's central
comparison is the one this shard has described since Chapter 4, with one operand moved.

Related: [[synced-outofsync]] [[status]] [[source-of-truth]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/declarative-configuration.md ===

## Chapter 15 update (2026-08-31)

OpenGitOps principle 1 is this shard with nothing added: "A system managed by GitOps must have
its desired state expressed declaratively." [source: opengitops-principles-v1-2026-08-31]

Ch 15 §7 says so explicitly — "This is Chapter 4. You file a declaration; the system's job is to
make it true. Nothing added." Of the four principles, **only principle 2 (versioned and
immutable) is new**, and it is a property of the *store*, not of Kubernetes.

Related: [[opengitops-four-principles]] [[control-loop-pointed-at-a-repository]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-server-hub.md ===

## Chapter 15 update (2026-08-31)

⚠ **A GitOps agent does not bypass the API server, and this shard's claim is not suspended.**

Ch 15 §3's Navigational Hazards block exists to kill the misreading that "the repository is the
source of truth" means Git *replaces* etcd. It does not. etcd still holds every object. Git holds
the *authored* desired state, upstream, and the agent keeps the two in agreement by making
ordinary API calls — through authentication, then authorization, then admission, in that order.

The consequence a reader can act on: an agent lacking RBAC permission to create a resource fails
with an ordinary authorization error. **GitOps grants no exemption from any cluster control. If
anything it is more constrained than a human operator, because its permissions are written down.**

Related: [[source-of-truth]] [[api-access-gates]] [[delivery-agent-identity]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-access-gates.md ===

## Chapter 15 update (2026-08-31)

The three gates apply to a delivery agent exactly as they apply to `kubectl`. Ch 15 §3: "A
delivery agent is an API client like any other. Its requests pass through authentication, then
authorization, then admission, in that order, exactly as yours do."

Graded at Practice Q9 distractor D ("it bypasses the Kubernetes API server" — wrong in **both**
delivery models, not just pull).

Related: [[source-of-truth]] [[api-server-hub]] [[admission-control]] [[rbac]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

## Chapter 15 update (2026-08-31) — ⚑ GOOD NEWS for the open canon conflict

Ch 15 §4 supplies the pattern's cleanest instance in the book: installing Argo CD's CRD lets
`Application` objects *exist*; whether anything *happens* to them depends entirely on whether the
application controller is running. **"An `Application` on a cluster with no Argo CD controller is
a stored document. It describes a deployment that will never occur."**

⚑ **Chapter 15 quotes NEITHER canonical string.** It applies the pattern and points at Ch 10 §3
rather than restating Ch 10's shipped form or the ledger's drifted one. So it does not repeat
Ch 13's breach (still unfixed at chapter-13:1279) and does not re-fight it either.

**State of the conflict entering Ch 16:** shipped Ch 10 and Ch 14 use Ch 10's form; shipped Ch 13
uses the ledger's; Ch 15 uses neither. The graded text is Ch 10's — the planning artifacts should
move, not the book. Ch 17 §4 meets the whole thread at once.

Related: [[argo-cd-application-resource]] [[custom-resource]] [[ingress-controller]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/custom-resource.md ===

## Chapter 15 update (2026-08-31)

Argo CD's `Application` is "a Custom Resource Definition (CRD)"
[source: argocd-core-concepts-2026-08-31], and Flux ships a controller set each of whose members
owns its own custom resources [source: flux-components-2026-08-31].

Two things this shard's registration-before-use rule now covers:

1. **Registration is not action.** An `Application` on a controller-less cluster is stored and
   inert. (Ch 6 §8's rule, applied to delivery.)
2. **Ordering.** A CRD must land before any custom resource of its kind, or the API server
   rejects it. Under a system reconciling a whole repository at once, that is expressed as a sync
   wave rather than as apply order. See [[sync-wave]].

Ch 15 §4's structural close: "this is a controller acting on custom resources, which is precisely
the thing Chapter 6 said you could build. It is not a new category of technology."

Related: [[argo-cd-application-resource]] [[operator-pattern]] [[sync-wave]] [[crds-in-charts]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/operator-pattern.md ===

## Chapter 15 update (2026-08-31)

A GitOps delivery agent has the operator pattern's exact shape: a controller, running in-cluster,
acting on custom resources, encoding operational knowledge that would otherwise live in a
person's head — here, "apply whatever the repository says, forever."

Ch 15 §4 is careful not to overclaim the label; it says the structural thing instead: "It is not
a new category of technology. It is the category you were taught, aimed somewhere unexpected."

⚑ **Canonical-forms note carried forward from ch-14:** that manifest flagged Chapter 14 for using
"operator" to mean a person. **Chapter 15 does the same, twice, inside quotations it cannot
alter** — argo-rollouts-canary-2026-08-31's "the operator releases a new version" and CNCF's
blue/green entry describing "the operator maintaining two environments." Quoted usage is not a
breach, but the two senses now sit four pages apart. A one-clause gloss at first quoted use would
close it.

Related: [[custom-resource]] [[argo-cd]] [[control-loop]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serviceaccount.md ===

## Chapter 15 update (2026-08-31) — Ch 5 §6's forward pointer paid

Kubernetes names this use among the reasons non-human identity exists: "an external service needs
to communicate with the Kubernetes API server (CI/CD pipelines)."
[source: k8s-docs-service-accounts-2026-08-23]

Ch 15 §4 asks the next question — what does *this* Pod do for a living? It creates, updates and
deletes objects across many namespaces on behalf of whatever is committed to a repository. **Its
grants must be broad, because "apply whatever the repository says" is a broad job description.**

Argo CD uses an `argocd-manager` ServiceAccount; its external-cluster credentials are "the K8s API
bearer token associated with the `argocd-manager` ServiceAccount created during
`argocd cluster add`." [source: argocd-security-cluster-credentials-2026-08-31]

Related: [[delivery-agent-identity]] [[serviceaccounts-and-identity]] [[rbac]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serviceaccounts-and-identity.md ===

## Chapter 15 update (2026-08-31) — chapter-12:617's promise discharged

Ch 12 §2 closed by naming the shape: "An agent running outside the cluster, or an agent running
inside it whose job is to reconcile the cluster's contents against something, is a subject exactly
like any Pod is a subject. It needs an identity, it needs grants, and because its job is broad its
grants tend to be broad. That is a shape you will meet again."

Ch 15 §4 is that meeting, and it supplies the number Ch 12 could not: **cluster-admin by default.**
"By default, Argo CD uses a clusteradmin level role."
[source: argocd-security-cluster-credentials-2026-08-31]

★ **The identity/permission separation this shard teaches is what makes the reduction possible.**
Cluster-wide *read* is structural — an agent cannot detect drift in what it cannot see. Broad
*write* is a default, not a requirement.

Related: [[delivery-agent-identity]] [[rbac]] [[blast-radius]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/rbac.md ===

## Chapter 15 update (2026-08-31)

**Cross-namespace scope requires a cluster-scoped grant.** A delivery agent creating Deployments
and Services in namespaces it does not own needs a ClusterRole bound by a ClusterRoleBinding, not
a Role in each namespace. Argo CD's own model does exactly this: reduction is done by editing the
ClusterRole `argocd-manager-role`. [source: argocd-security-cluster-credentials-2026-08-31]

**Why per-namespace Roles are the wrong answer:** they work, and they break. Every new namespace
the repository introduces needs a new Role and RoleBinding first, so the agent cannot create a
namespace and populate it in one sync — and the failure surfaces as a permissions error at exactly
the moment somebody adds a namespace.

**Flux takes the other route.** It keeps the broad role and impersonates a narrower identity:
`.spec.serviceAccountName` specifies "the ServiceAccount to be impersonated while reconciling."
[source: flux-kustomization-api-2026-08-31] ⚠ *Kubernetes Impersonation API* is named and never
defined, in either chapter, and has no ledger row.

## ⚑ RESTORE THE ORDERING EXAMPLE — see manifest ⚑ C2

This shard already carries the source: "After you create a binding, you cannot change the Role or
ClusterRole that it refers to." [source: k8s-docs-rbac-2026-08-23] Shipped chapter-12:866 states it
correctly **and emits a forward pointer into Ch 15 §5** on the strength of it. As drafted, §5
removed the illustration and the pointer lands on nothing. Restore: a binding's `roleRef` is
immutable, so changing which role a binding grants is a delete-and-recreate — a real ordering
constraint for a system reconciling a whole repository against a whole cluster.

★ **And the largest consequence, which is not an RBAC object at all:** anyone who can commit to the
tracked branch can, transitively, do whatever the agent may do. **Branch-protection rules are an
access-control mechanism exactly as load-bearing as this shard.**

Related: [[delivery-agent-identity]] [[sync-wave]] [[additive-never-deny]] [[blast-radius]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/additive-never-deny.md ===

## Chapter 15 update (2026-08-31)

Retrieved verbatim in Ch 15's Soundings (Q5, answer key): "Permissions are additive, and there is
no deny rule." Pointer-only extension — Chapter 15 adds no new semantics, and correctly declines
to re-derive the rule it is testing.

Worth noting for the Ch 17 §4 sweep: this is the second chapter to retrieve the rule in a
*Soundings* rather than a graded checkpoint, which keeps it out of the retrieval budget by B3's
design while still spacing it.

Related: [[rbac]] [[delivery-agent-identity]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/secret.md ===

## Chapter 15 update (2026-08-31)

External-cluster credentials are ordinary Secrets: "To manage external clusters, Argo CD stores
the credentials of the external cluster as a Kubernetes Secret in the argocd namespace,"
comprising the API bearer token for the `argocd-manager` ServiceAccount plus connection options.
[source: argocd-security-cluster-credentials-2026-08-31]

★ **The Ch 12 §4 consequence applies unchanged:** whoever can read Secrets in `argocd` can read
credentials to every cluster that Argo CD manages. Under a multi-cluster control point, one
namespace's Secrets are the keys to the estate.

This is the second time the book has found a delivery tool's bookkeeping sitting in an ordinary
Secret under ordinary rules — Helm's release history was the first (Ch 14 §3).

Related: [[secret-exposure-and-hardening]] [[multi-cluster-delivery]] [[helm-release]]
[[delivery-agent-identity]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/secret-exposure-and-hardening.md ===

## Chapter 15 update (2026-08-31)

Ch 15 §3's first consequence is this shard's subject viewed from the delivery path: under push,
cluster-write credentials sit in a CI system's secret store, readable by its jobs and often by
anyone who can edit a pipeline definition; under pull they sit in a Secret in the cluster they
apply to.

⚠ **This comparison is the book's reading, not a documented finding** — no CNCF or vendor source
in the corpus argues push-versus-pull as a security question, and Chapter 15 says so three times.
What *is* documented is the credential locations, plus Argo CD's access-separation argument: "The
developers who are developing the application, may not necessarily be the same people who
can/should push to production environments." [source: argocd-best-practices-2026-08-31]

★ **Pull moves the credentials inside the cluster; it does not make them smaller.**

Related: [[blast-radius]] [[push-versus-pull-delivery]] [[secret]] [[supply-chain-security]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespace.md ===

## Chapter 15 update (2026-08-31)

Two uses in Ch 15, both ordinary and both consequential:

- **`argocd` is a credential store.** External-cluster Secrets live there.
  [source: argocd-security-cluster-credentials-2026-08-31] Namespace-scoped RBAC on that one
  namespace is therefore estate-wide access control.
- **An `Application`'s destination is a cluster *and a namespace*.**
  [source: argocd-declarative-setup-2026-08-31] The namespace is half the contract.

And the ordering consequence: a namespace must exist before namespaced objects can be placed in
it, which under one-shot reconciliation is a sync-wave problem rather than an apply-order problem.

Related: [[sync-wave]] [[argo-cd-application-resource]] [[secret]] [[namespaced-vs-cluster-scoped]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/configmap.md ===

## Chapter 15 update (2026-08-31)

Ch 15 §1 names what this shard has been an instance of since Chapter 4: **ConfigMaps and Secrets
are Kubernetes' implementation of twelve-factor factor III.** "The object model was designed for
factor III."

The litmus test now attaches to it: "whether the codebase could be made open source at any moment,
without compromising any credentials." [source: twelve-factor-iii-config-2026-08-31]

🪝 And the correction worth carrying: "store config in the environment" is a claim about *where
config lives relative to your code*, **not** about the literal `env:` block. A ConfigMap mounted
as a file satisfies factor III perfectly well — the file is supplied by the deploy environment,
not committed. Readers who take the phrase literally conclude mounted-file config violates the
methodology. It doesn't.

Related: [[factor-iii-config-in-environment]] [[twelve-factor-app]] [[secret]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-lifetime.md ===

## Chapter 15 update (2026-08-31)

"Scheduled once, replaced never" is the platform-side guarantee that factors VI and IX are the
application-side price of.

- **Factor VI** is why replacement is safe: "Twelve-factor processes are stateless and
  share-nothing." [source: twelve-factor-vi-processes-2026-08-31] A Deployment can substitute any
  Pod for any other only because no Pod carries what the next one needs.
- **Factor IX** is what replacement demands: fast startup, graceful SIGTERM shutdown, and
  robustness "against sudden death, in the case of a failure in the underlying hardware."
  [source: twelve-factor-ix-disposability-2026-08-31]

The second failure mode Ch 15 names is the one this shard has always implied and never spelled
out: a Pod's writable layer is destroyed with the Pod, so state held there is not merely
misplaced at the next rollout — it is gone.

Related: [[factor-vi-stateless-processes]] [[factor-ix-disposability]] [[restart-policy]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/probe.md ===

## Chapter 15 update (2026-08-31) — pointer only

Health gating reappears one level up. A PostSync hook runs "after all Sync hooks completed and
were successful, a successful application, **and all resources in a Healthy state**."
[source: argocd-sync-phases-and-waves-2026-08-31]

Argo CD's glossary carries **Health** as its own entry — "The health of the application, is it
running correctly? Can it serve requests?" [source: argocd-core-concepts-2026-08-31] — which is
this shard's question asked about an application rather than a container.

The rule stays here; the delivery-time gate lives at [[sync-hook-phases]].

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-chart.md ===

## Chapter 15 update (2026-08-31) — ⚑ B6 MANDATORY ANCHOR DISCHARGED

section-skeleton.md:214 records two Helm anchors that "may not be dropped." This is the first:
**charts as a delivery agent's manifest source.**

Argo CD accepts manifests as "kustomize applications; **helm charts**; jsonnet files; plain
directory of YAML/json manifests; any custom config management tool configured as a config
management plugin." [source: argocd-overview-2026-08-23] Flux's source controller carries
`HelmChart` and `HelmRepository` resources, and a Helm controller owns `HelmRelease`.
[source: flux-components-2026-08-31]

★ **Chapter 14 gave you packaging; Chapter 15 gives packaging somewhere to go.** The agent renders
the chart and compares the *result* against the cluster. Rendering is a dedicated component, not
an afterthought — the repository server. [source: argocd-architecture-2026-08-31]

Related: [[manifest-source]] [[kustomize]] [[argo-cd]] [[flux-controller-set]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kustomize.md ===

## Chapter 15 update (2026-08-31)

Kustomize appears twice in Chapter 15, in both delivery tools. Argo CD lists "kustomize
applications" first among its manifest sources [source: argocd-overview-2026-08-23] and names the
**application source type** as "which Tool is used to build the application," with Kustomize as
its own example [source: argocd-core-concepts-2026-08-31].

Flux gives it a whole controller: the `Kustomization` API "defines a pipeline for fetching,
decrypting, building, validating and applying Kustomize overlays or plain Kubernetes manifests."
[source: flux-kustomization-api-2026-08-31]

⚑ Note the collision this creates and that Chapter 15 handles without comment: **Flux's
`Kustomization` is a Flux CRD, not Kustomize's `kustomization.yaml`.** They are different objects
with near-identical names. Worth one clause if a later retrofit touches §6.

Related: [[base-and-overlay]] [[manifest-source]] [[flux-controller-set]] [[kustomization-fields]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/base-and-overlay.md ===

## Chapter 15 update (2026-08-31)

The base/overlay model is what a delivery agent consumes when its source is a Kustomize
application: the agent builds the overlay and compares the built output against the cluster,
exactly as it renders a chart.

This closes the loop Ch 14 §5 opened. An overlay's whole purpose is to express per-environment
difference without forking the originals; a GitOps agent's `Application` names a *path*, so one
repository can carry a base and several overlays, each tracked by its own `Application` with its
own destination.

Related: [[kustomize]] [[manifest-source]] [[argo-cd-application-resource]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-rollback-versus-rollout-undo.md ===

## Chapter 15 update (2026-08-31) — the set is now complete

This shard held two mechanisms wearing one word. Chapter 15 supplies the third and last.

| | What moves | Where the previous state was kept |
|---|---|---|
| `kubectl rollout undo` (Ch 6 §5) | the Deployment's Pod template | the old ReplicaSet, on the cluster |
| `helm rollback` (Ch 14 §3) | the Helm release to a prior revision | Helm's release history, on the cluster |
| **rollback by revert** (Ch 15 §4) | a commit in the repository | the repository's history |

★ **The third has no dedicated rollback code path.** You move the target and the loop does the
rest — the same loop that handles every ordinary change. Argo CD describes the capability as
"rollback/roll-anywhere to any application configuration committed in Git repository."
[source: argocd-overview-2026-08-23]

chapter-06:714's "twice more" promise is now fully discharged. **No further sense of the word may
be introduced without amending term-ownership.md:854.**

Related: [[rollback-by-revert]] [[helm-release-revision]] [[tracking-branch-tag-commit]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-release-revision.md ===

## Chapter 15 update (2026-08-31) — ⚠ "revision" is now three senses deep

This shard owns the Helm sense. Chapter 6 owns the Deployment sense. **Chapter 15 introduces a
third: Argo CD's `revision` field, which names a Git branch, tag, or commit.**

Ch 15 §4's ruling: "In this book, *revision* has two owners already… A Git revision is a
**commit**. Argo CD's own API field happens to be called `revision`, which is why this needs
saying rather than assuming."

⚑ **Two gaps to close at the glossary build:**
1. The B7 canonical-forms table covers only the Deployment and Helm senses. **Add a row for the
   Argo CD/Git sense: always write "commit."**
2. §4 uses bare *revision* five times in the new sense ("An `Application` names a revision…",
   "updating the tracking revision") **before** the disambiguating Snag two subsections later.
   Move the clause forward to first use.

Related: [[tracking-branch-tag-commit]] [[rollback-by-revert]] [[helm-rollback-versus-rollout-undo]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/crds-in-charts.md ===

## Chapter 15 update (2026-08-31)

Ch 14 §6 framed CRD ordering as a packaging problem Helm's `crds/` directory partly solves.
Ch 15 §5 shows the general form: **GitOps does not inherit that fix — it inherits the problem, at
larger scale.**

An agent reconciling a whole repository against a whole cluster faces the same question about far
more objects: a namespace before what goes in it, a CRD before any custom resource of its kind, a
migration before the version expecting the new schema.

The expression is a **sync wave** — resources ordered within a phase, "lower values first," with
negatives available so you can run something ahead of everything else.
[source: argocd-sync-phases-and-waves-2026-08-31] What matters is relative order, not the numbers.

Related: [[sync-wave]] [[custom-resource]] [[sync-hook-phases]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/distribute-versus-adapt.md ===

## Chapter 15 update (2026-08-31)

Ch 14 §6 framed Helm-versus-Kustomize as a choice. Chapter 15 shows the frame from above: **a
delivery agent renders both, so at the delivery layer it is not a choice at all.**

Argo CD lists Kustomize applications and Helm charts side by side as manifest sources
[source: argocd-overview-2026-08-23]; Flux ships a controller for each
[source: flux-components-2026-08-31].

The choice Ch 14 described is real and stays real — it is a question about *authoring*, and it is
settled before the agent ever sees the repository. What Chapter 15 removes is the idea that the
delivery tool has a stake in the answer.

Related: [[manifest-source]] [[helm-chart]] [[kustomize]] [[package-not-template]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/package-not-template.md ===

## Chapter 15 update (2026-08-31) — Ch 14's Zenith collects

Ch 14 §7 argued that a chart is a *package*, and left the reader holding one with nowhere to put
it — the complaint Ch 15 opens on: the unit still gets applied by a person, and afterward nothing
keeps watch.

Chapter 15 is the destination. A package becomes a **source reference** in an `Application`, and
the thing that applies it is a controller that never stops.

⚠ **Redundancy note for the retrofit pass.** Ch 15's epigraph is character-identical to
chapter-14:1393, and its second paragraph is near-verbatim to chapter-14:1387 — roughly 60 words
of Ch 14's final page on Ch 15's first. Skill Part 7 classifies this as channel redundancy, and it
lands exactly where arousal must be established. **The prose recap earns its place (it sets up the
two-halves structure organising the whole chapter); the epigraph does not.** Cut one.

Related: [[control-loop-pointed-at-a-repository]] [[manifest-source]] [[distribute-versus-adapt]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/oci.md ===

## Chapter 15 update (2026-08-31)

Flux treats an OCI registry as one source kind among several: the source controller carries
`OCIRepository` alongside `GitRepository` and `Bucket`. [source: flux-components-2026-08-31]

Chapter 2 established that the distribution spec distributes *content*, not images specifically;
Chapter 14 showed charts living in registries; Chapter 15 shows a delivery agent treating that as
unremarkable configuration. The claim has now paid off in three chapters, each time without
needing restatement.

Related: [[registry]] [[oci-registry-as-chart-store]] [[flux-controller-set]] [[manifest-source]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/registry.md ===

## Chapter 15 update (2026-08-31)

A registry appears in Chapter 15 as a *desired-state source*, not an image store: Flux's
`OCIRepository` and `HelmRepository` sit beside `GitRepository` as origins a Source can name.
[source: flux-components-2026-08-31]

★ This is the strongest available demonstration of the shard's central claim — **a registry serves
content, not images.** By Chapter 15 the reader needs no argument for it; the roster is enough.

Related: [[oci]] [[chart-repository]] [[manifest-source]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/chart-repository.md ===

## Chapter 15 update (2026-08-31)

Flux models a chart repository as a first-class source: `HelmRepository` is one of the source
controller's custom resources, consumed by the Helm controller via `HelmRelease`.
[source: flux-components-2026-08-31]

Worth carrying for the trap this shard exists to prevent (B1 #81, `charts/` vs a chart
repository): under Flux the distinction becomes structural rather than definitional. A
`HelmRepository` is an object naming an HTTP server on the network. `charts/` is still a directory
inside a chart. Nothing about GitOps blurs them.

Related: [[registry]] [[flux-controller-set]] [[helm-chart]] [[manifest-source]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/published-vs-commonly-reported.md ===

## Chapter 15 update (2026-08-31) — the discipline held, and the ruling stands

**Chapter 15 states its own rule up front and keeps it for the whole chapter:** "nothing here is
described as 'frequently tested' or 'commonly appears'… What you will see instead is 'easy to
confuse' and 'this is the distinction the material rewards,' which are claims this book can
actually stand behind."

Verified: **zero** instances of "frequently tested" or "commonly appears." The Common Traps
preamble reads "these are distinctions that are easy to confuse." The B1 trap tags license the
*confusion*, not the frequency, and Chapter 15 is the cleanest execution of that distinction in
the book so far.

It also goes beyond the requirement: §3 carries an explicit "A note on what follows" declaring
which push/pull consequences are sourced and which are the book's reading, and repeats the
disclosure **inside two graded answer keys** (TYB2 Q3, Practice Q10) rather than only in prose.

## ⚑⚑ THE 8% RULING STANDS — third chapter now

Ch 15's integration report recommends restoring "8% to 16%" using shipped Chapter 1's tag.
**Do not.** Verified directly:

- `lf-kcna-program-changes-2026-08-23:11–15` carries a CORRECTION stating "THE PAGE DOES NOT
  DISPLAY THE PREVIOUS DOMAIN STRUCTURE OR WEIGHTS," and closes with "no retired-blueprint
  weights" (`:44`).
- `cncf-curriculum-repo-kcna-versions-2026-08-23:36–44` records the retired PDF as
  text-not-extracted and says **"DO NOT draft the retired weights from memory or from third-party
  study guides."** Still an open gap.
- The only corpus file carrying `8%` is `provenance-kcna-60-questions-2026-08-23`, headed
  "DO NOT CITE THE CONTENTS OF THIS FILE AS FACT."

**But the ethical half is real and needs action:** Ch 15's untagged "this domain **doubled**"
asserts the same figure with the tag stripped off. Fix by deletion, to the supported claim: the
domain carries 16%, and the revision rolled Observability under Cloud Native Architecture
[source: lf-kcna-program-changes-2026-08-23].

The irony this shard exists to record deepens: **Chapter 1 §2's entire subject is
published-versus-commonly-reported figures, and chapter-01:274 cites a community blog post's
number under a Linux Foundation source tag.** Correct Chapter 1 and domain-analysis.md:39; do not
renormalise Chapters 14 or 15 upward toward them.

Related: [[domain-weights-44-28-16-12]] [[blueprint-change-2025-11-24]] [[kcna-exam-format]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/domain-weights-44-28-16-12.md ===

## Chapter 15 update (2026-08-31) — ⚑⚑ DO NOT RESTORE THE 8% CLAIM (third chapter)

Chapter 15's metadata line states the published figure correctly and tags it: "Domain Weight: 16%
(Cloud Native Application Delivery) [source: cncf-kcna-curriculum-pdf-2026-08-23]," followed by
the house disclosure that the split across Ch 14–16 is authored allocation.

**Two instructions, both carried forward from ch-14's manifest and both re-verified today:**

1. **The retired weights remain unsourceable.** See [[published-vs-commonly-reported]] for the
   three-file verification. Ch 15's integration report recommends restoring them; that
   recommendation is wrong and must not be applied.
2. **`domain-analysis.md:39` still asserts it flatly** — "Doubled from 8% to 16% in the
   revision." A B-stage artifact carrying an unsourced figure is how this reached two shipped
   chapters, and **Ch 16 reads the same row.** Correct it in the same pass as Chapter 1.

★ **What Chapter 15 does right and should be preserved:** it never presents the authored 7%
sub-allocation as published, and it discloses the allocation in the metadata block itself rather
than burying it. Follow this pattern in Ch 16.

Related: [[published-vs-commonly-reported]] [[blueprint-change-2025-11-24]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/blueprint-change-2025-11-24.md ===

## Chapter 15 update (2026-08-31)

Chapter 15 refers to "the 2025-11-24 blueprint revision" once, in Why This Chapter Matters, and
attaches an untagged "doubled" to it.

**What this shard can support:** the effective date (independently confirmed by two commits dated
Nov 24, 2025 in `cncf-curriculum-repo-kcna-versions-2026-08-23:17–18`), and the structural change
— "The KCNA domains… will remain mostly unchanged except that observability will be rolled under
Cloud Native Architecture." [source: lf-kcna-program-changes-2026-08-23]

**What it cannot support:** any statement of the prior weights, including "doubled." See
[[domain-weights-44-28-16-12]].

Recommended replacement for Ch 15: "this domain carries 16% of the exam, and the 2025-11-24
revision rolled Observability under Cloud Native Architecture rather than leaving it a domain of
its own [source: lf-kcna-program-changes-2026-08-23]." The rhetorical beat survives; the
unsourceable arithmetic does not.

Related: [[domain-weights-44-28-16-12]] [[published-vs-commonly-reported]]

=== END APPEND ===
```

---

## What a reader of this manifest should act on first

Five things, in order, and only two of them are Chapter 15's:

1. **Do not apply the integration report's Recommended Fix #1.** Delete "doubled" instead. Verified against three snapshots; Chapter 14's Stage 14 reached the same conclusion independently. The correction belongs to `chapter-01:274` and `domain-analysis.md:39`.
2. **Apply Recommended Fix #2 — restore the §5 `roleRef` ordering example.** Sourced at `k8s-docs-rbac-2026-08-23:17`, shipped correctly at `chapter-12:866`, and Chapter 12's forward pointer currently lands on nothing.
3. **Commission the Zenith figure pair on one chassis.** Four contracts stake the book's primary payoff on `ch03-fig02` and `ch15-zenith-…` superimposing. They do not.
4. **Retarget three cross-bearings** (Ch 3 §6 → §5; Ch 14 §1 → chapter-level; Ch 6 §8 → §9). All three verified by line number; the third is the closing sentence of the Zenith, where a reader is most likely to check.
5. **Fix the tag drift once, at book level** — three surface forms across three consecutive chapters, and a Practice pool that has read as 0% retrieval for all three. Per-chapter fixes have now failed twice.

Everything else in this manifest is recorded for the replay and for the Ch 17 §4 collection, not for this gate.
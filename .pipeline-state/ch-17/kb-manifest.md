I'll start by reading the existing knowledge base so I don't duplicate entries or silently overwrite prior canon.No knowledge-base directory exists yet. Let me check whether earlier chapters ran this stage, and what format sibling books use.Prior chapters produced manifests. Let me read the most recent one to match convention and see whether earlier writes ever landed.Now let me build the complete inventory of existing concept shards so I can correctly choose WRITE vs APPEND.Let me read the binding scaffolding and Ch 17's outline to ground the manifest.Let me independently verify the integration report's headline finding rather than passing it through.The integration report's headline finding needs correcting. Let me quantify the actual situation precisely.Chapter 16's manifest asked the next stage to check whether the snapshot truncation it found also hit other chapters. Chapter 17 leans heavily on `2026-08-31` captures, so let me check.A curriculum-repo snapshot exists, which the draft's AUTHOR-REVIEW claims is an open gap. Let me check it.A curriculum PDF snapshot exists too. Let me read it — this bears directly on the draft's G33 gap claim.This is a significant find. Let me verify it's genuinely unused and confirm what remains open.Let me check the established shard file format so the new ones match.I have everything I need. Two of my checks changed the picture materially, so I'll lead with those.

---

# Knowledge-Base Manifest — KCNA Chapter 17

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice, re-verified this run.** `Book-KCNA/knowledge-base/` **still does not exist on disk.** Sixteen manifests exist (`ch-01`…`ch-16`); none has been applied. Chapter 17 adds the seventeenth.
>
> **Ordering contract, inherited from Ch 12–16.** **APPEND** for the three shared registers and for every shard that already exists; **WRITE** only for slugs that collide with nothing. I enumerated all 190 distinct `concepts/*.md` slugs referenced across `ch-01`–`ch-16` and checked every proposed Ch 17 slug against it. **One collision found and deliberately not created** — see ⚑ C7.

---

## ⚑ Findings that change what downstream stages should do

### ⚑ C0. HIGH — the draft's chapter-wide G33 gap is **already closed by a cached snapshot**, and it is the book's most-cited provenance file

The draft's opening `AUTHOR-REVIEW` states:

> *"the Dead Reckoning block below states that Domain 4 has three competencies and names them … **No cached snapshot supports the count or the names** — cncf-kcna-certification-page-2026-08-23 publishes the four domain names and weights and nothing below that level, and the KCNA curriculum document (github.com/cncf/curriculum) is still an open research gap, tracked as G33."*

**A cached snapshot supports both.** `sources/cncf-kcna-curriculum-pdf-2026-08-23.md` is the curriculum PDF, text-extracted, three pages. Line 16 reads:

```
- 12% – Cloud Native Architecture: Observability; Cloud Native Ecosystem
  and Principles; Cloud Native Community and Collaboration
```

That is the count and the names, from CNCF's own publication channel. This is not an obscure file: **all sixteen shipped chapters cite it**, and shipped Ch 16 uses it for this exact purpose in its metadata line (`ch16:227`).

Three consequences, all cheap:

1. **Tag the Dead Reckoning block** `[source: cncf-kcna-curriculum-pdf-2026-08-23]` and delete the second half of the chapter-wide AUTHOR-REVIEW.
2. **Correct one competency name.** The draft says *"Cloud Native Observability."* The curriculum says **"Observability."** Ch 18's own naming depends on this.
3. **Match Ch 16's metadata convention**, which the draft's first AUTHOR-REVIEW is reaching for and reinventing:
   `**Domain Weight: 12% (Cloud Native Architecture) [source: cncf-kcna-curriculum-pdf-2026-08-23] | Competencies: Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration | Authored allocation for this chapter: ~7%**`

**Bonus corroboration.** The curriculum lists the three competencies in the order Observability → Ecosystem and Principles → Community and Collaboration. The outline's `kb_tags.objectives: ["D4.2", "D4.3"]` therefore maps exactly: **D4.1 = Observability (Ch 18), D4.2 and D4.3 = this chapter.** The authored 7/5 split lands on a competency boundary the curriculum itself draws — a stronger position than the draft claims for itself.

Also sourceable now, and currently carried as inference: the Exam Alert trap row and The Voyage Ahead both assert Observability is competency material inside Cloud Native Architecture rather than a domain. The curriculum states it.

### ⚑ C1. HIGH — the integration report's headline blocker is **misdiagnosed**, and the correct fix is different

The integration report (F1/C1) asserts that Ch 17 §7 hands back the pattern in words the reader has never seen, and that *"Ch 13 uses neither the sentence nor the alternate name anywhere (verified: zero hits in Ch 12–16)"*, making Ch 17 the last chance for a promised retrieval.

I measured it. **Chapter 13 retrieves the pattern three times.** There are three phrasings live in shipped text:

| Variant | Wording | Where | Count |
|---|---|---|---|
| **A** (canonical ★) | *an object without its component does nothing* | Ch 3 ×2, **Ch 10 ×12**, Ch 11 ×4 | **18** |
| **B** | *the object exists; nothing happens without the component* | **Ch 13 ×3** (`:300`, `:1279`, `:1281`) | 3 |
| **C** | *the object exists **but** nothing happens without the component* | Ch 6 ×2 (`:1005`, `:1082`) | 2 |

Chapter 17 uses **Variant B** — the same words Chapter 13 uses, and the same words the B7 ledger row (`:339`) specifies. The drift is older and wider than the ledger: **B3 `retrieval-architecture.md` states the pattern in Variant C**, and Ch 6 §? tells the reader *"Name the pattern, because you will retrieve it by name"* in Variant C before Ch 10 ever states Variant A.

So this is a **book-level unification sweep across five chapters and two binding artifacts**, not a Chapter 17 defect, and the promised retrieval did land in Ch 13. Ch 17 should not be singled out for repair.

**What the integration report gets right, and what still needs fixing in Ch 17:** the attribution. Ch 17 says *"Chapter 10 §3 christened it."* Chapter 3 both names it (`ch03:601`, "⚓ Worth Securing — **the absent-component pattern**") and gives the phrase, and Ch 11 `:811` says so explicitly: *"The phrase is Chapter 3's, and Chapter 10 §3 named it as a pattern."* One-line fix:

> You have met this shape before, and you have met it under a name. Chapter 3 gave you the phrase and Chapter 10 §3 named it as a pattern: **the object exists; nothing happens without the component.**

Leave the wording alone until the book-wide sweep picks a winner. Recommendation: **standardize on Variant A** — it is 18 of 23 occurrences, it is the ★ Fixed Point, and it is in a graded Ch 11 answer option. Then correct B3, B7, Ch 6, Ch 13 and Ch 17 together, in one commit.

### ⚑ C2. CONFIRMED — the fifteen-weeks promise is real and unpaid

Ch 8 says "fifteen weeks" three times (`:861`, `:1003`, `:1009`), and `:1009` commits: *"where SIG Release and the KEP process explain **where those fifteen weeks go**."* The number appears nowhere in Ch 17. §8's phase walk-through is exactly that accounting. The integration report's one-clause fix is correct and is the cheapest option.

### ⚑ C3. CONFIRMED — CloudEvents reaches graded text undefined

Zero occurrences in Ch 1–16. Never defined in Ch 17. Carries Practice Q14's correct answer. Take the integration report's option 1 (define in §6 + glossary + register row); removing it from the option while leaving it in body prose would make the two disagree.

### ⚑ C4. GOOD NEWS — Chapter 16's ⚑ I0 truncation escalation **does not extend to Chapter 17**

Ch 16's manifest found eleven `2026-08-31` snapshots truncated at their first code fence with frontmatter falsely asserting completeness, and asked the next stage to check chapters 08–15 for the same fault. Chapter 17 has **108 `2026-08-31` captures**. I measured 22 of the load-bearing ones: **39–112 lines**, none showing the truncation signature, all ending in the researcher's own prose commentary rather than mid-fence.

| Snapshot | Lines | Snapshot | Lines |
|---|---|---|---|
| `k8s-docs-autoscaling-and-vpa` | 112 | `cncf-glossary-service-mesh` | 60 |
| `k8s-release-cycle-and-cadence` | 99 | `k8s-sig-list-and-groups` | 60 |
| `cncf-glossary-microservices-monoliths-coupling` | 82 | `istio-security-mtls-identity` | 57 |
| `cncf-tags-current-structure` | 76 | `cncf-mentoring-and-community-groups` | 53 |
| `cncf-toc-project-lifecycle-process` | 70 | `karpenter-concepts` | 52 |
| `k8s-docs-node-autoscaling` | 67 | `istio-ambient-mode` | 49 |
| `k8s-docs-api-aggregation-and-device-plugins` | 60 | `envoy-what-is-envoy` | 39 |

The fault was confined to Ch 16's twelve-page debug batch, not a shared code path. **Chapters 08–15 still need the check**; Chapter 17 is clear.

### ⚑ C5. CONFIRMED — the Helm `crds/` tag is available, no research gap needed

The draft's AUTHOR-REVIEW asks whether a Helm snapshot exists to tag the `crds/` ordering claim. **`sources/helm-crd-best-practices-2026-08-31.md` exists**, line 10 carries the declaration-vs-usage distinction, and shipped Ch 14 §6 already cites it for this exact claim. Apply the tag to §4 and to Practice Q10. Do not open a gap.

### ⚑ C6. CONFIRMED — the retired blueprint is genuinely still open, and the cut must stay cut

There is **no** `cncf-kcna-curriculum-retired-*.md` in `sources/`. `cncf-curriculum-repo-kcna-versions-2026-08-23.md` documents the two 2025-11-24 commits and the archived PDF's URL, then states plainly: *"The retired domain weights are NOT recorded in this snapshot… DO NOT draft the retired weights from memory or from third-party study guides."*

The revision's removal of the comparative weights claim ("rose to 28%", "doubled to 16%") was correct and must not be restored. This is now the **fourth consecutive chapter** to rule on it. Ch 16's ⚑ I4 remains live: `ch-17/outline.md` and `domain-analysis.md` should be checked for the same retired figures before Ch 18 drafts.

### ⚑ C7. The `four-pluggable-interfaces` slug is a collision, and this stage declines to create it

`kb_tags.concepts` names `four-pluggable-interfaces`. Two shards already carry this concept: **`pluggable-interface-pattern.md`** (ch-02) and **`pluggable-interfaces.md`** (ch-11) — Ch 16's ⚑ I2, still unmerged. Creating a third slug at the chapter that *collects* the pattern would be exactly the drift I am supposed to flag.

**Chapter 17 appends to `pluggable-interface-pattern.md`** (the earlier, ch-02 original) and does **not** create `four-pluggable-interfaces.md`. `pluggable-interfaces.md` gets **no append** — merge it to a stub at the replay. Ch 17 §4 is the last chapter that can make this decision cheaply.

### ⚑ C8. B3 compliance — checked, and Chapter 17 honors all four prohibitions

`retrieval-architecture.md` names four things that must not be retrieved. Ch 17 honors every one: no Ch 1 exam mechanics; the graduated-project **roster** is explicitly refused in favor of the levels (⚓ Worth Securing, §2); no 60-question/75% figures; and both `[inferred]` trap rows use the *"(Easy to confuse …)"* convention rather than an exam-frequency claim. B3 also specifies release cadence land in Ch 17 "where the three-supported-minors rule and the ~3/year cadence explain each other" — §8 delivers exactly that.

One overage to record: B3 sets Ch 17 at the **25% ceiling**. Measured, checkpoints are 4/16 (25%) and Practice is 6/21 (**29%**). Over ceiling, on the safe side, and worth a note rather than a cut.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

Two tiers, following Ch 11–16. The integration report marked 4 terms as needing entries; skill Part 16 requires every technical term the book introduces, so the **44 B7-owned Ch 17 rows** (`term-ownership.md:521–568`) are harvested alongside them, plus the acronym-register rows at `:656–725`.

### Tier 1 — unsourced, provisional, orphaned, newly graded, or corrected

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **CloudEvents** | ⚠ **Undefined in the chapter and in Ch 1–16, yet carries Practice Q14's correct answer.** The reader gets only Knative's phrasing, *"a CloudEvents-over-HTTP asynchronous routing layer."* Enter only once §6 defines it. See ⚑ C3 | Chapter 17 §6 |
| **Observability** *(as a D4 competency)* | *"Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration"* `[source: cncf-kcna-curriculum-pdf-2026-08-23]` — ⚠ the draft names it *"Cloud Native Observability."* **Use "Observability."** See ⚑ C0 | Chapter 17 (Ch 18 owns) |
| **CKAD · CKS** | ⚠ **Expanded nowhere in Ch 1–17.** CKA is expanded once at `ch01:180`. B7 `:661–662` assigns all three to Ch 17 §8. Expand at first use | Chapter 17 §8 |
| **KCSA** | *"Kubernetes and Cloud Native Security Associate"* — ⚠ **expansion not in any cached snapshot**; `cncf-who-we-are-2026-08-23` gives the bare acronym. Standard and near-certainly correct; carried under the acronym register's expand-at-first-use rule | Chapter 17 §8 |
| **FaaS** | ⚠ **Ledger row `:553` assigns it to Ch 17 §6; the draft never uses the term.** Orphaned register row — add one clause at Knative Functions or retire the row | — (unassigned) |
| **ztunnel** | *"a purpose-built, per-node proxy that powers Istio's ambient data plane mode"* `[source: istio-ambient-mode-2026-08-31]` — graded twice; no ledger row | Chapter 17 §5 |
| **waypoint proxy** | *"The waypoint proxy is a deployment of the Envoy proxy; the same engine that Istio uses for its sidecar data plane mode"* `[source: istio-ambient-mode-2026-08-31]` — graded twice; no ledger row | Chapter 17 §5 |
| **Permissive mode** | *"the server accepts both plaintext and mutual TLS traffic,"* existing *"to provide greater flexibility for the on-boarding process"* `[source: istio-security-mtls-identity-2026-08-31]` — named, ungraded, no ledger row | Chapter 17 §5 |
| **Secure overlay** | The set of L4 functions ztunnel implements in ambient mode `[source: istio-ambient-mode-2026-08-31]` — named, ungraded, no ledger row | Chapter 17 §5 |
| **Consolidation** *(node autoscaling)* | *"Nodes … can be automatically consolidated in order to improve the overall Node utilization … through removing a set of underutilized Nodes"* `[source: k8s-docs-node-autoscaling-2026-08-31]` — no ledger row; the half nobody teaches | Chapter 17 §7 |
| **In-place Pod vertical resize** | Stable in v1.35; *"As of Kubernetes 1.37, VPA does not support resizing pods in-place"* on one page, while the VPA page and the v1.35 blog describe `InPlaceOrRecreate` at beta `[source: k8s-docs-autoscaling-and-vpa-2026-08-31]` — ⚠ **live three-way source conflict; the chapter writes to it deliberately. Do not "resolve" it.** | Chapter 17 §7 |
| **Cluster Proportional Autoscaler** | Scales replica counts on schedulable node and core count `[source: k8s-docs-autoscaling-2026-08-23]` — named for completeness, explicitly ungraded | Chapter 17 §7 |
| **Archived** *(CNCF)* | *"inactive or low activity projects that are no longer supported"* `[source: cncf-toc-project-lifecycle-process-2026-08-31]` — ⚠ **not a rung**; graded as a distractor twice | Chapter 17 §2 |
| **Incubation vs Incubating** | The lifecycle document says "Incubation" (the process); the projects page says "Incubating" (the level). ⚠ **Book uses "Incubating" throughout** | Chapter 17 §2 |
| **Karpenter's status** | Sponsored by Kubernetes SIG Autoscaling; ⚠ **no official source assigns it a CNCF maturity level.** Contrast Knative and KEDA, both sourced as Graduated | Chapter 17 §7 |

### Tier 2 — the 44 B7-owned Ch 17 rows, harvested per skill Part 16

Cloud native (v1.1) · the five characteristics · CNCF as institution · project maturity level · CNCF project lifecycle · Governing Board · TOC · TAG · End User TAB · CNCF Landscape · microservices · monolith · loose coupling · immutable infrastructure · declarative API (as a characteristic) · extension point · API aggregation layer · `APIService` · device plugin · service mesh · data plane · the mesh's control plane · Envoy · sidecar proxy · mTLS · zero trust · ambient mode · Istio · Linkerd · serverless · Knative · Knative Serving · Knative Eventing · Knative Functions · Knative Service · scale to zero · KPA · autoscaling (the landscape) · VPA · Cluster Autoscaler · Karpenter · KEDA · SIG · Working Group · Committee · Steering Committee · subproject · contributor ladder · KEP · SIG Release · KubeCon + CloudNativeCon · Code of Conduct · the CNCF certification ladder.

**Acronym-register rows to enter** (`term-ownership.md:656–725`): CA · CKA · CKAD · CKS · CNCF *(institution sense)* · FaaS · KCSA · KEDA · KEP · mTLS · SIG · TAB · TAG · TOC · VPA · WG.

---

## Concept shards at `Book-KCNA/knowledge-base/concepts/{slug}.md`

**Thirty-nine created**, mapping the outline's 47 `kb_tags.concepts` with seven consolidations (where the discrimination *is* the content, per the `oomkilled-vs-evicted.md` / `tag-vs-digest.md` precedent) and **one deliberate non-creation** (⚑ C7).

| Slug | § | Note |
|---|---|---|
| `cloud-native-definition-v1-1.md` | §1 | the document; the public/private/hybrid correction in the first clause |
| `cloud-native-characteristics.md` | §1 | ★ the five, hung on loose coupling |
| `cncf-mission-and-vendor-neutrality.md` | §1 | 227 projects, 715 members; vendor-neutral as structural claim |
| `cncf-project-maturity-levels.md` | §2 | ★ three rungs; **Archived is the exit, not a rung** |
| `cncf-project-lifecycle.md` | §2 | where the criteria actually live; the application→vote process |
| `cncf-governance-bodies.md` | §2 | **absorbs `cncf-governing-board`, `cncf-toc`, `end-user-technical-advisory-board`** — the Board/TOC pair is the confusion, so the discrimination is the file |
| `cncf-tags.md` | §2 | ⚠ the 2025 restructuring; both lists recorded |
| `cncf-landscape.md` | §2 | the categories, and that they mirror this book's TOC |
| `microservices-and-monoliths.md` | §3 | **consolidated** — the glossary argues both sides; splitting them loses the argument |
| `loose-coupling.md` | §3 | same loose coupling as §1's, not a homonym |
| `immutable-infrastructure.md` | §3 | ⚠ the book's *second* immutability |
| `small-pieces-replaced-whole.md` | §3 | **absorbs `declarative-api-as-a-characteristic`** — §3's three-in-one argument, the only thing there not available elsewhere |
| `kubernetes-extension-points.md` | §4 | **absorbs `extension-point`** — the documentation's six, printed beside the book's four |
| `api-aggregation-layer.md` | §4 | the CRD-vs-aggregation discrimination; graded from both directions |
| `device-plugin.md` | §4 | graded distractor twice |
| `service-mesh.md` | §5 | ★ without code changes; **absorbs the what-a-mesh-adds boundary table** |
| `mesh-data-plane-vs-control-plane.md` | §5 | **consolidated** — ★ and the three-way vocabulary collision with Ch 3 |
| `envoy.md` | §5 | "unaware of the network topology" — the property from the proxy's side |
| `sidecar-and-ambient-modes.md` | §5 | **consolidated** — ⚠ both use Envoy; they coexist |
| `mutual-tls.md` | §5 | CA + config API server + PEPs; workload identity |
| `zero-trust.md` | §5 | trust is a vulnerability; lateral movement |
| `serverless.md` | §6 | abstracts servers away from the **user** |
| `knative.md` | §6 | ★ builds on Pods, ships as CRDs |
| `knative-serving-versus-eventing.md` | §6 | **absorbs `knative-functions`** — the graded discrimination |
| `scale-to-zero.md` | §6 | KPA; the Knative Service vs Deployment relation |
| `horizontal-vs-vertical-autoscaling.md` | §7 | ★ the axis distinction |
| `vertical-pod-autoscaler.md` | §7 | ⚠ **the add-on** — the absent-component instance |
| `node-autoscaling.md` | §7 | **absorbs `cluster-autoscaler` + `karpenter`** — sources say the two give a similar experience; provisioning *and* consolidation |
| `keda-event-driven-autoscaling.md` | §7 | events + Cron scaler; shares HPA's axis |
| `autoscaler-axis-and-trigger.md` | §7 | the two-questions method; the grid is reconstructible, not memorized |
| `in-place-pod-vertical-resize.md` | §7 | ⚑ **carries the live three-way source conflict** |
| `kubernetes-sig-wg-committee.md` | §8 | **absorbs `steering-committee` + `subproject`** — ★ and ⚠; the closed-membership asymmetry |
| `contributor-ladder.md` | §8 | four rungs; the two-sponsors-different-companies check |
| `kubernetes-enhancement-proposal.md` | §8 | alpha→beta→stable; the discoverable record |
| `sig-release-and-release-cadence.md` | §8 | ★ **one fact stated three ways**; ⚑ carries the C2 fifteen-weeks debt |
| `cncf-community-onramps.md` | §8 | **absorbs `kubecon-cloudnativecon`** — LFX/GSoC/Outreachy/CNCGs/Ambassadors |
| `code-of-conduct.md` | §8 | the scope statement, which is broader than assumed |
| `cncf-certification-ladder.md` | §8 | the **format** change is the headline |
| `one-pluggability-story.md` | §9 | **the Zenith.** Own file, per `the-boundary-is-the-method.md` / `control-loop-pointed-at-a-repository.md` |

**Not created — ⚑ C7.** `four-pluggable-interfaces.md` is **not** written. Its content appends to `pluggable-interface-pattern.md` (ch-02).

**Twenty amended by append.** `pluggable-interface-pattern.md` ⚑⚑ · `absent-component-pattern.md` ⚑⚑ · `release-cadence.md` ⚑⚑ · `cloud-native-framing.md` ⚑ · `cri.md` · `cni.md` · `csi.md` · `custom-resource.md` · `network-policy.md` ⚑ · `resource-metrics-pipeline.md` · `multi-container-pod.md` · `pod.md` · `image-immutability.md` · `api-server-hub.md` · `pending-pod.md` · `crds-in-charts.md` · `twelve-factor-app.md` · `kcna-exam-format.md` · `control-loop.md` ⚠ · `domain-weights-44-28-16-12.md` ⚑.

**⚑ DO NOT APPEND: `pluggable-interfaces.md`** (ch-11). Merge to a stub pointing at `pluggable-interface-pattern.md`. Appending Ch 17's collection to a duplicate slug entrenches the split at the one chapter that could have closed it.

Not shard-worthy, adequately carried by the glossary: permissive mode · secure overlay · Cluster Proportional Autoscaler · Linkerd · `APIService` · Incubation-vs-Incubating · node group.

---

## Infrastructure flags — the knowledge base itself

**⚑ I7 — HIGH, new.** `ch-16/kb-manifest.md` describes **21 new shards and 16 appends and emits zero shard blocks** — its only three blocks are the shared registers. Chapter 16's entire concept layer is documented but unwritten. Slugs including `ephemeral-containers.md`, `four-triage-questions.md` and `the-boundary-is-the-method.md` exist in no WRITE block anywhere. **Re-emit before the replay**, or Ch 16 contributes nothing to the concept index.

**⚑ I8 — LOW, new.** `ch-15/kb-manifest.md:2605` contains a corrupt marker — `=== APPEND C:\dev\lodestar\cert``` ` — immediately followed by a correct duplicate of the `spec.md` append at `:2606`. A naive parser will either fail or write a garbage path. Delete line 2605.

**⚑ I1 — HIGH, unchanged, now seventeen chapters expensive.** Chapters 03, 10 and 11 emit full **WRITE** blocks for `glossary.md`, `objective-coverage.md` and `retrieval-log.md`; `absent-component-pattern.md` is written as a full file twice (ch-03, ch-10). Replaying `ch-01`→`ch-17` in order discards everything written before each of those points. Chapter 17 adds only APPENDs to shared registers. **Convert those WRITE blocks to APPENDs before any replay.**

**⚑ I2 — MEDIUM, now acute.** `pluggable-interface-pattern.md` (ch-02) and `pluggable-interfaces.md` (ch-11) are one concept under two slugs. **Chapter 17 §4 is the collection point.** Ch 17 refuses to add a third (⚑ C7) but cannot merge the existing two. Merge at the replay.

**⚑ I3 — MEDIUM, unchanged, and now blocking Ch 18 and Ch 19.** `book-outline/retrieval-architecture.md` is **18 lines** of permissions-failure message plus the stage's own summary — verified again this run. Every B3 figure in ⚑ C8 is recovered from that summary. It also contains the Variant C phrasing that seeded ⚑ C1.

**⚑ I4 — MEDIUM, inherited from ch-16, still live.** Check `ch-17/outline.md` and `domain-analysis.md` for the retired-blueprint comparative weights before Ch 18 drafts. Four consecutive chapters have now ruled they must not ship (⚑ C6).

**⚑ I9 — LOW, new.** With ⚑ C0 resolved, `cncf-kcna-curriculum-pdf-2026-08-23.md` should carry `concepts_covered: ["kcna-competencies", "domain-weights-44-28-16-12"]`. Its frontmatter currently names only the former, which is why three separate stages searched for the D4 competency list and did not find it.

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Paying a debt named as a debt** | "Chapter 1 named the phrase *cloud native*. It said the near-universal reading, 'it runs in a public cloud,' is not what the term means. Then it declined to define it, and pointed here. **That is the longest-running open loop in this book,** and §1 closes it with the actual published document rather than a paraphrase." | **Strong candidate.** The catalog has no passage that opens by naming its own outstanding obligation and then discharging it in the reader's sight. Curiosity-gap resolution done as bookkeeping rather than as reveal. |
| **Refusing a memorization task the reader expects** | "⚓ **Worth Securing:** Learn the *levels*, not the roster. Which specific projects are Graduated on the day you sit the exam is a moving target, and **no responsible study guide should ask you to memorize a list that changes faster than it prints.** What does not move is what each level *asserts*." | **Strong candidate.** A study guide declining to make the reader memorize something, with the reason stated in terms of the book's own shelf life. Trust-building through self-limitation; the catalog has nothing like it. |
| **Marking the book's own judgment as judgment** | "That grouping is *this book's*, and honesty requires saying so. Kubernetes does not publish a document titled 'the four pluggable interfaces.' … **Both maps are correct. They are answering different questions.** … This book is answering *what is the pattern?*" | **Strong candidate.** Skill Part 14's simplification guardrail executed structurally — the book prints the authoritative list *beside* its own and defends the difference rather than hiding it. Followed by the generalizable ⚓: *"When two authoritative-looking lists of the same subject have different lengths, the useful question is almost never 'which is right.' It is 'what is each one for.'"* |
| **Derivation offered instead of memorization** | "Three releases a year. Three maintained branches. Which means a release stays supported for roughly — **do the arithmetic yourself before reading on.** … They are one fact stated three ways. … you can *derive* the support window instead of memorizing it." | **Strong candidate.** Generation effect (Part 10) inside a ★ Fixed Point, converting the book's self-declared most-forgettable material into one relationship. The mid-sentence break is the whole technique. |
| **Zenith by altitude, with the metaphor disciplined** | "The same vocabulary as the extension-points map, one altitude higher — and **altitude, to a navigator, is not a metaphor for importance. It is the angle you take on a fixed body to learn where you actually are.**" | **Strong candidate.** Corrects the reader's likely reading of the brand's own maritime register mid-caption. Guards against the overwrought-metaphor failure the theming guidance warns about, by using the register precisely enough to reject the loose reading. |
| **An invitation that lowers the bar honestly** | "> **Logbook Entry:** The most common misconception about contributing to a project this size is that the work is all deep systems programming, and that a first contribution has to be impressive. **It does not.** … **Forty-five minutes spent following a group of engineers arguing about a KEP will do more for your retention of this section than reading it three times.**" | **Moderate to strong.** Connection architecture (Part 3) at its most literal — identity transformation with a specific, doable first action. Held at moderate only because the surrounding claim was softened at revision for want of a source; the passage should be re-nominated if the SIG meeting schedules are re-fetched. |
| **Difficulty markers justified against reader expectation** | "§2 and §8 … carry ⚪ Foundation difficulty markers for the same reason: **not because the material is easy, but because the signal you need when scanning the left margin is *everyone needs this*, not *optional depth*.**" | **Moderate.** Explains a brand mechanic to the reader in-line, in one sentence, without breaking register. Useful precedent for any chapter whose difficulty markers will look wrong to a strong reader. |

---

## Objective coverage log

Audited against `cncf-kcna-curriculum-pdf-2026-08-23` (⚑ C0), `outline.md:227–228`, and `domain-analysis.md`.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D4.2 — Cloud Native Ecosystem and Principles** | **Chapter 17** | **deep — whole competency** | 2026-08-31 |
| **D4.3 — Cloud Native Community and Collaboration** | **Chapter 17** | **deep — whole competency** | 2026-08-31 |

**Two whole competencies in one chapter** — the only such chapter in the book, and the stated reason it is the longest. **D4.1 (Observability) is Chapter 18's**, and the curriculum's own ordering corroborates the split (⚑ C0).

---

## Retrieval-practice ledger

10 tags, all verified against the section skeleton and shipped text. Distribution 4/16 checkpoints (25%) and 6/21 practice (29%) against B3's 25% ceiling — over, on the safe side (⚑ C8).

| Tested topic | Original chapter | Retested in |
|---|---|---|
| image immutability vs immutable infrastructure | ch 2 §2 | ch 17 (Bearings 1 Q6) |
| the four pluggable interfaces | ch 2 §4 · 6 §8 · 9 §1 · 11 §5 | ch 17 (Bearings 2 Q1) — **the chapter's central item** |
| NetworkPolicy cannot encrypt | ch 10 §6–§7 | ch 17 (Bearings 2 Q3, Practice Q12) |
| CRD vs API aggregation | ch 6 §8 | ch 17 (Practice Q9) |
| Helm `crds/` ordering | ch 14 §6 | ch 17 (Practice Q10) |
| metrics-server / `kubectl top` | ch 13 §7 | ch 17 (Practice Q16) |
| `Pending` / unschedulable / preemption | ch 7 §2 | ch 17 (Practice Q17) |
| release cadence + support window | ch 8 §6 | ch 17 (Bearings 3 Q4, Practice Q19) — **B3's named anchor, delivered** |
| the absent-component pattern | ch 3 (phrase) · ch 10 §3 (named) | ch 13 ×3, **ch 17 §7** — see ⚑ C1 |
| version-skew decay anchor | ch 8 §6 | ch 17 §8 — B3's flagged decay problem, repaired |

---

## Recommended actions, ranked

1. **Apply ⚑ C0.** Tag the Dead Reckoning block, rename *"Cloud Native Observability"* → **"Observability"**, adopt Ch 16's metadata-line form, and delete the second half of the chapter-wide AUTHOR-REVIEW. Highest value-per-edit in this chapter.
2. **Re-scope the ⚑ C1 fix.** Do **not** treat Ch 17 as the defect. Fix the attribution clause in §7; open a book-wide sweep for the three-way wording drift across B3, B7, Ch 6, Ch 13, Ch 17; standardize on Variant A.
3. **Close the fifteen-weeks loop (⚑ C2)** — one clause in §8.
4. **Resolve CloudEvents (⚑ C3)** — define in §6, glossary entry, register row.
5. **Tag the Helm claim (⚑ C5)** to `helm-crd-best-practices-2026-08-31` in §4 and Practice Q10. No gap needed.
6. **Expand CKAD and CKS** at first use in §8.
7. **Minor sweep:** "operator" → "user" at the identity-shift paragraph; reconcile the KEDA expansion to *Kubernetes Event-Driven Autoscaling*; optionally restore *"among the most forgettable."*
8. **Infrastructure, before any replay:** ⚑ I7 (re-emit Ch 16's shards), ⚑ I8 (delete `ch-15:2605`), ⚑ I1 (WRITE→APPEND), ⚑ I2 (merge the duplicate slug), ⚑ I3 (re-run B3), ⚑ I4 (scrub retired weights from Ch 17's upstream artifacts), ⚑ I9 (retag the curriculum snapshot).
9. **Still genuinely open, correctly:** KCSA's expansion; the retired blueprint's weights (⚑ C6); the per-SIG meeting schedules; the FaaS orphan row; the figure-numbering order. The `ch17-zenith-…` anchor is **valid** per `structural-contract.yaml` — no action.

---

Below are the write intentions. Register appends first, then the twenty shard appends, then the thirty-nine new shards.

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

# Chapter 17 additions (2026-08-31)

## A

**Ambient mode** — An Istio data plane mode in which "Istio implements its features using a per-node Layer 4 (L4) proxy, and optionally a per-namespace Layer 7 (L7) proxy," and "workload pods no longer require proxies running in sidecars in order to participate in the mesh." [source: istio-ambient-mode-2026-08-31] Coexists with sidecar mode in one mesh. (Chapter 17 §5)

**API aggregation layer** — The mechanism that "allows Kubernetes to be extended with additional APIs, beyond what is offered by the core Kubernetes APIs." Runs in-process with the kube-apiserver; does nothing until an `APIService` object claims a URL path, after which it proxies requests on that path to a registered service. "Different from Custom Resource Definitions, which are a way to make the kube-apiserver recognise new kinds of object." [source: k8s-docs-api-aggregation-and-device-plugins-2026-08-31] (Chapter 17 §4)

**APIService** — The object registered with the aggregation layer that "claims" a URL path in the Kubernetes API. [source: k8s-docs-api-aggregation-and-device-plugins-2026-08-31] (Chapter 17 §4)

**Archived (CNCF)** — "inactive or low activity projects that are no longer supported." [source: cncf-toc-project-lifecycle-process-2026-08-31] NOT a maturity rung; the exit from the ladder. (Chapter 17 §2)

**Autoscaling axis** — The book's frame for classifying an autoscaler: ask what moves (replicas, per-replica resources, or nodes) and separately what triggers it. (Chapter 17 §7)

## C

**CA** — Cluster Autoscaler. (Chapter 17 §7)

**Certification ladder (CNCF)** — KCNA "is a pre-professional certification designed for candidates interested in advancing to the professional level" and "lays the groundwork for further CNCF certifications like CKA, CKAD, and CKS." [source: cncf-kcna-certification-page-2026-08-23] The format changes up the ladder: KCNA is online and multiple-choice; CKA, CKAD and CKS are performance-based. (Chapter 17 §8)

**CKA (Certified Kubernetes Administrator)** — "a performance-based exam where candidates interact with the command line to solve real-world challenges." [source: cncf-kcna-certification-page-2026-08-23] (Chapter 1; Chapter 17 §8)

**CKAD (Certified Kubernetes Application Developer)** — Taken in "a hands-on, command-line environment." [source: cncf-kcna-certification-page-2026-08-23] (Chapter 17 §8)

**CKS (Certified Kubernetes Security Specialist)** — "performance-based." [source: cncf-kcna-certification-page-2026-08-23] (Chapter 17 §8)

**Cloud native** — "Cloud native practices empower organizations to develop, build, and deploy workloads in computing environments (public, private, hybrid cloud) to meet their organizational needs at scale in a programmatic and repeatable manner. It is characterized by loosely coupled systems that interoperate in a manner that is secure, resilient, manageable, sustainable, and observable." [source: cncf-cloud-native-definition-2026-08-23] The term is about method, not location. (Chapter 17 §1; named in Chapter 1)

**Cloud Native Architecture** — KCNA exam domain, 12%. Competencies: Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration. [source: cncf-kcna-curriculum-pdf-2026-08-23] (Chapters 17 and 18)

**CloudEvents** — [PENDING — see kb-manifest C3. Do not enter until Chapter 17 §6 defines the term. It currently carries Practice Q14's correct answer while being defined nowhere in the book.]

**Cluster Autoscaler** — A node autoscaler that provisions Nodes for unschedulable Pods and consolidates underutilized ones, working against pre-configured node groups. Sponsored by Kubernetes SIG Autoscaling. [source: k8s-docs-node-autoscaling-2026-08-31] (Chapter 17 §7)

**CNCF (Cloud Native Computing Foundation)** — Part of the nonprofit Linux Foundation [source: cncf-who-we-are-2026-08-23]; mission "to make cloud native computing ubiquitous" [source: cncf-charter-governance-bodies-2026-08-31]. Hosts 227 projects across four categories, with 715 member organizations and over 329,000 project contributors. [source: cncf-who-we-are-2026-08-23] (Chapter 1 as exam sponsor; Chapter 17 §1 as institution)

**CNCF Ambassadors** — An extension of the CNCF furthering the mission through community leadership and mentorship; many organize local community groups. [source: cncf-landscape-and-community-2026-08-23] (Chapter 17 §8)

**CNCF Landscape** — "a map through the previously uncharted terrain of cloud native technologies," categorizing most projects and product offerings in the space, "of which CNCF-hosted projects are a particularly well-traveled path." [source: cncf-landscape-and-community-2026-08-23] Categories: Provisioning · Runtime · Orchestration and Management · App Definition and Development · Observability and Analysis · Platforms and Special. (Chapter 17 §2)

**Cloud Native Community Groups (CNCGs)** — "free, volunteer-run meetups on the CNCF community platform, including Kubernetes Community Days." [source: cncf-landscape-and-community-2026-08-23] (Chapter 17 §8)

**Code of Conduct (CNCF Community)** — Applies "within project and community spaces, in other spaces when an individual CNCF community participant's words or actions are directed at or are about a CNCF project, the CNCF community, or another CNCF community participant in the context of a CNCF activity." Administered by the CNCF Code of Conduct Committee, with a stated expectation of "a response within three business days." [source: cncf-code-of-conduct-2026-08-31] (Chapter 17 §8)

**Committee (Kubernetes)** — A community group that "do[es] not have open membership and do[es] not always operate in the open. They are formed by the steering committee for specific topics requiring discretion (for example Security, Code of Conduct), have charters and chairs, and report periodically to the steering committee." [source: k8s-community-governance-2026-08-23] There are exactly three: Code of Conduct, Security Response, and Steering. [source: k8s-sig-list-and-groups-2026-08-31] (Chapter 17 §8)

**Consolidation (node autoscaling)** — "Nodes in your cluster can be automatically consolidated in order to improve the overall Node utilization, and in turn the cost-effectiveness of the cluster. Consolidation happens through removing a set of underutilized Nodes from the cluster." [source: k8s-docs-node-autoscaling-2026-08-31] (Chapter 17 §7)

**Contributor ladder (Kubernetes)** — Member → Reviewer → Approver → Subproject Owner. Member requires two-factor authentication, multiple contributions, dev list subscription, having read the contributor guide, sponsorship by 2 reviewers **from different companies**, and a membership request issue. [source: k8s-community-membership-ladder-2026-08-23] (Chapter 17 §8)

**Control plane, the mesh's** — "which manages and configures the proxies." [source: istio-service-mesh-2026-08-23] Distinct from the cluster's control plane (Chapter 3 §2). Always written as "the mesh's control plane" on first use. (Chapter 17 §5)

## D

**Data plane (mesh)** — "proxies that mediate and control all network communication between services." [source: istio-service-mesh-2026-08-23] (Chapter 17 §5)

**Declarative API** — Named in the CNCF Cloud Native Definition as a cloud native technology, alongside containers and microservices. [source: cncf-cloud-native-definition-2026-08-23] The mechanism itself is Chapter 4 §1. (Chapter 17 §3)

**Device plugin** — Lets you "configure your cluster with support for devices or resources that require vendor-specific setup, such as GPUs, NICs, FPGAs, or non-volatile main memory." Registers with the kubelet, "sends the kubelet the list of devices it manages, and the kubelet is then in charge of advertising those resources to the API server as part of the kubelet node status update." [source: k8s-docs-api-aggregation-and-device-plugins-2026-08-31] (Chapter 17 §4)

## E

**End User TAB (End User Technical Advisory Board)** — "will serve as the voice of End Users in the CNCF community, advance topics of concern to End Users, and raise awareness about the needs and perspectives of end users." [source: cncf-charter-governance-bodies-2026-08-31] Its feedback is mapped to projects by the TOC. (Chapter 17 §2)

**Envoy** — "an L7 proxy and communication bus designed for large modern service oriented architectures." "Envoy is a self contained process that is designed to run alongside every application server. All of the Envoys form a transparent communication mesh in which each application sends and receives messages to and from localhost and is unaware of the network topology." [source: envoy-what-is-envoy-2026-08-31] (Chapter 17 §5)

**Extension point** — The Kubernetes documentation's own category for places the system can be extended. Six are documented: kubectl plugins and client credential providers; API access extensions; API extensions; scheduling extensions; controllers; infrastructure extensions. [source: k8s-docs-extending-kubernetes-2026-08-23] Distinct from this book's four pluggable interfaces, which are a subset cut differently. (Chapter 17 §4; named Chapter 2 §4)

## F

**FaaS (Functions as a Service)** — [ORPHANED — assigned to Chapter 17 §6 by the term-ownership ledger; the chapter does not use the term. Add a clause at Knative Functions or retire this row.]

## G

**Governing Board (CNCF)** — "responsible for marketing and other business oversight and budget decisions for the CNCF." [source: cncf-charter-governance-bodies-2026-08-31] Sets the scope within which the TOC approves projects. (Chapter 17 §2)

**Graduated (CNCF)** — "stable, widely adopted, production ready, attracting thousands of contributors." [source: cncf-project-maturity-levels-2026-08-23] (Chapter 17 §2)

## H

**Horizontal scaling** — "the response to increased load is to deploy more Pods." [source: k8s-docs-hpa-2026-08-24] Changes the NUMBER of replicas. (Chapter 17 §7)

**HorizontalPodAutoscaler (HPA)** — Implemented "as a Kubernetes API resource and a controller," where the controller "periodically adjusts the desired scale of its target (for example, a Deployment) to match observed metrics such as average CPU utilization, average memory utilization, or any other custom metric you specify." Runs "as a control loop that runs intermittently (it is not a continuous process)" and "does not apply to objects that can't be scaled (for example: a DaemonSet)." [source: k8s-docs-hpa-2026-08-24] Ships with Kubernetes. (Chapter 6 §2; landscape at Chapter 17 §7)

## I

**Immutable infrastructure** — "computer infrastructure (virtual machines, containers, network appliances) that cannot be changed once deployed." [source: cncf-glossary-immutable-infrastructure-2026-08-31] Distinct from image immutability (Chapter 2 §2); always written as the full two-word phrase. (Chapter 17 §3)

**Incubating (CNCF)** — "used successfully in production by a small number of users, with a healthy pool of contributors." [source: cncf-project-maturity-levels-2026-08-23] The lifecycle document says "Incubation" for the process; this book uses "Incubating" for the level. (Chapter 17 §2)

**In-place Pod vertical scaling** — Changing a running Pod's CPU and memory requests and limits without recreating it; stable in Kubernetes v1.35. [source: k8s-docs-autoscaling-and-vpa-2026-08-31] ⚠ Whether VPA supports it is a live conflict among official sources; do not state it as settled. (Chapter 17 §7)

**Istio** — A service mesh that "gives applications capabilities like zero-trust security, observability, and advanced traffic management, without code changes." [source: istio-service-mesh-2026-08-23] (Chapter 17 §5)

## K

**Karpenter** — "an open-source node lifecycle management project built for Kubernetes" whose job is "to add nodes to handle unschedulable pods, schedule pods on those nodes, and remove the nodes when they are not needed." [source: karpenter-concepts-2026-08-31] Sponsored by Kubernetes SIG Autoscaling. ⚠ No official source assigns it a CNCF maturity level. (Chapter 17 §7)

**KCSA (Kubernetes and Cloud Native Security Associate)** — A CNCF credential. [source: cncf-who-we-are-2026-08-23] ⚠ The acronym expansion is not in the cached corpus. (Chapter 17 §8)

**KEDA (Kubernetes Event-Driven Autoscaling)** — "a CNCF-graduated project enabling you to scale your workloads based on the number of events to be processed, for example the amount of messages in a queue." Its `Cron` scaler "allows you to define schedules (and time zones) for scaling your workloads in or out." [source: k8s-docs-autoscaling-and-vpa-2026-08-31] Moves the replica count, the same axis as the HPA. (Chapter 17 §7)

**KEP (Kubernetes Enhancement Proposal)** — "a way to propose, communicate and coordinate on new efforts for the Kubernetes project," using "a standard proposal format with useful metadata." Inspired by IETF RFCs and Python PEPs; provides "exposure through searchable websites, cross-referencing, and structured decision-making with a discoverable record." Tracks features through alpha → beta → stable. [source: k8s-keps-and-feature-stages-2026-08-23] (Chapter 17 §8)

**Knative** — "a Kubernetes-based platform that provides a complete set of middleware components for building, deploying, and managing modern serverless workloads." A CNCF Graduated project. Builds on the Kubernetes Pod abstraction; Serving and Eventing "are implemented as Kubernetes Custom Resource Definitions (CRDs)." [source: knative-overview-2026-08-23] (Chapter 17 §6)

**Knative Eventing** — "a CloudEvents-over-HTTP asynchronous routing layer that provides infrastructure for consuming and producing events, enabling loose coupling between event producers and consumers." [source: knative-overview-2026-08-23] (Chapter 17 §6)

**Knative Functions** — "leverages Serving and Eventing to provide a simplified experience for building and deploying stateless functions." [source: knative-overview-2026-08-23] (Chapter 17 §6)

**Knative Pod Autoscaler (KPA)** — Knative Serving's default autoscaler, which scales applications down to zero replicas when they receive no traffic and scale to zero is enabled. [source: knative-serving-autoscaling-2026-08-31] (Chapter 17 §6)

**Knative Serving** — "an HTTP-triggered autoscaling container runtime that manages the complete lifecycle of stateless HTTP services, including deployment, routing, and automatic scaling (including scale to zero)." [source: knative-overview-2026-08-23] (Chapter 17 §6)

**Knative Service** — A Knative Serving object holding Pods running your container, with an autoscaler that will take it to zero and bring it back on a request. Always written in full; distinct from the Kubernetes Service (Chapter 9 §2). (Chapter 17 §6)

**KubeCon + CloudNativeCon** — The flagship CNCF conference series where the community convenes. [source: cncf-landscape-and-community-2026-08-23] (Chapter 17 §8)

## L

**LFX Mentorship** — "a mentoring initiative by the Linux Foundation." [source: cncf-mentoring-and-community-groups-2026-08-31] (Chapter 17 §8)

**Linkerd** — With Istio, one of the two most widely deployed meshes in the CNCF ecosystem. (Chapter 17 §5)

**Loosely coupled architecture** — "an architectural style where individual components are built independently of one another, each performing a specific function in a way that can be used by any number of other services." "Generally slower to implement than tightly coupled architecture but has a number of benefits, particularly as applications scale," chiefly that teams can "develop features, deploy, and scale independently." [source: cncf-glossary-microservices-monoliths-coupling-2026-08-31] (Chapter 17 §3)

## M

**Maturity level (CNCF project)** — Sandbox → Incubating → Graduated. [source: cncf-project-maturity-levels-2026-08-23] The criteria for moving between them live in the CNCF TOC's project lifecycle documentation, not on the projects page. (Chapter 17 §2)

**Microservices architecture** — "an architectural approach that breaks applications into individual independent (micro)services, with each service focused on a specific functionality." Creates "operational overhead — the things you need to deploy and keep track of increase by order of magnitude." [source: cncf-glossary-microservices-monoliths-coupling-2026-08-31] (Chapter 17 §3)

**Monolithic app** — An application shipped as one unit; the CNCF glossary argues a well-designed monolith "can uphold lean principles by being the simplest way to get an application up and running," and that "crafting a microservices-based app before it has proven valuable may be premature spending of engineering effort." [source: cncf-glossary-microservices-monoliths-coupling-2026-08-31] (Chapter 17 §3)

**mTLS (mutual Transport Layer Security)** — Mutual authentication and encryption between workloads, in which the server verifies the client's workload identity as well as the client verifying the server. In Istio, delivered by a Certificate Authority, a configuration API server distributing policy and secure naming information to proxies, and sidecar and perimeter proxies acting as Policy Enforcement Points. [source: istio-security-mtls-identity-2026-08-31] (Chapter 17 §5)

## N

**Node autoscaling** — "Automatically provision and consolidate the Nodes in your cluster to adapt to demand and optimize cost." Triggered when "there are Pods in a cluster that can't be scheduled on existing Nodes." Requires interaction with cloud provider APIs. [source: k8s-docs-node-autoscaling-2026-08-31] (Chapter 17 §7)

## O

**Observability (D4 competency)** — One of the three competencies of the Cloud Native Architecture domain. [source: cncf-kcna-curriculum-pdf-2026-08-23] Covered in Chapter 18. Not itself a domain on the current blueprint. (Chapter 17; Chapter 18)

## P

**Permissive mode** — A mesh mode in which "the server accepts both plaintext and mutual TLS traffic," existing "to provide greater flexibility for the on-boarding process." [source: istio-security-mtls-identity-2026-08-31] (Chapter 17 §5)

## S

**Sandbox (CNCF)** — "experimental projects, not yet widely tested in production, on the bleeding edge of technology." [source: cncf-project-maturity-levels-2026-08-23] Capitalized and always used alongside a sibling level; distinct from a sandboxed runtime (Chapter 2 §7). (Chapter 17 §2)

**Scale to zero** — "If an application is receiving no traffic and scale to zero is enabled, Knative Serving scales the application down to zero replicas." [source: knative-serving-autoscaling-2026-08-31] (Chapter 17 §6)

**Secure overlay** — The set of L4 functions ztunnel implements in Istio's ambient mode. [source: istio-ambient-mode-2026-08-31] (Chapter 17 §5)

**Serverless computing** — "abstracts servers away from the user." Charges are pay-per-use; scaling and resource provisioning "are automatically adjusted based on application demand without user intervention"; the provider "consolidates resources to serve multiple users on a single physical machine, ensuring isolation through virtualization." [source: cncf-glossary-serverless-2026-08-31] Abstracts away, not eliminates. (Chapter 17 §6)

**Service mesh** — A layer that manages "traffic (i.e., communication) between services and adding reliability, observability, and security features uniformly across all services … without requiring code changes. Before service meshes, that functionality had to be encoded into every single service, becoming a potential source of bugs and technical debt." [source: cncf-glossary-service-mesh-2026-08-31] (Chapter 17 §5; named Chapter 5 §2)

**SIG (Special Interest Group)** — The primary, durable, topic-focused organizational unit of the Kubernetes project. Oriented vertically (Network, Storage, Node), horizontally (Scalability, Architecture), or project-support (Testing, Release, Docs). Each "must have at least one and ideally two SIG chairs at any given time." Work within a SIG "is divided into subprojects, each with designated owners." [source: k8s-community-governance-2026-08-23] Distinct from a CNCF TAG. (Chapter 17 §8; named Chapter 8 §6)

**SIG Release** — The SIG responsible for "Production of Kubernetes releases on a reliable schedule," defining and staffing release roles, and "managing the creation of release specific artifacts, including: Code branches, Binary artifacts, Container Images, Release notes." [source: k8s-release-cycle-and-cadence-2026-08-31] (Chapter 17 §8)

**Sidecar mode** — An Istio data plane mode in which an Envoy proxy is deployed alongside each Pod. [source: istio-ambient-mode-2026-08-31] (Chapter 17 §5; the Pod shape is Chapter 5 §2)

**Steering Committee** — One of the three Kubernetes Committees; holds overall project governance and charters the other two. [source: k8s-community-governance-2026-08-23] (Chapter 17 §8)

**Subproject** — A division of work within a SIG, "each with designated owners who serve as technical leaders for their respective areas." [source: k8s-community-governance-2026-08-23] (Chapter 17 §8)

## T

**TAB** — Technical Advisory Board. See End User TAB. (Chapter 17 §2)

**TAG (Technical Advisory Group)** — "the primary organizational units within the CNCF that oversee and coordinate interests across projects, working groups, and the broader cloud native community," serving "as bridges between CNCF projects, end users, and the Technical Oversight Committee." [source: cncf-tags-current-structure-2026-08-31] Restructured in 2025; the current five are Developer Experience, Infrastructure, Operational Resilience, Security and Compliance, and Workloads Foundation. CNCF-wide, unlike a Kubernetes SIG. (Chapter 17 §2)

**TOC (Technical Oversight Committee)** — The CNCF's technical governing body, facilitating "driving neutral consensus for: defining and maintaining the technical vision for the Cloud Native Computing Foundation," approving "new projects within the scope of the CNCF set by the Governing Board," creating a conceptual architecture, aligning projects, removing or archiving them, and mapping End User TAB feedback to projects. [source: cncf-charter-governance-bodies-2026-08-31] [source: cncf-toc-and-tags-2026-08-23] (Chapter 17 §2)

## V

**Vertical scaling** — "assigning more resources (for example: memory or CPU) to the Pods that are already running for the workload." [source: k8s-docs-hpa-2026-08-24] Changes the RESOURCES available to each replica. (Chapter 17 §7)

**VPA (VerticalPodAutoscaler)** — Adjusts per-replica CPU and memory based on observed usage. ⚠ "Unlike HorizontalPodAutoscaler, which is part of the core Kubernetes API, VPA must be installed separately in your cluster," and requires metrics-server. Runs as a recommender, an updater, and an admission controller webhook. [source: k8s-docs-autoscaling-and-vpa-2026-08-31] (Chapter 17 §7)

## W

**Waypoint proxy** — The optional per-namespace L7 component of Istio's ambient mode. "The waypoint proxy is a deployment of the Envoy proxy; the same engine that Istio uses for its sidecar data plane mode." [source: istio-ambient-mode-2026-08-31] (Chapter 17 §5)

**WG** — Working Group. (Chapter 17 §8)

**Working Group (Kubernetes)** — Time-bounded groups "primarily used to facilitate topics of discussion that are in scope for Kubernetes but that cross SIG lines. They are short-lived or address issues spanning multiple SIGs." [source: k8s-community-governance-2026-08-23] (Chapter 17 §8)

## Z

**Zero trust architecture** — "never trust, always verify." Where a traditional perimeter model lets components inside the boundary communicate freely, zero trust requires that "components within the system first have to pass verification before any communication is made," because it "recognises that trust is a vulnerability." [source: cncf-glossary-zero-trust-architecture-2026-08-31] (Chapter 17 §5)

**ztunnel** — "a purpose-built, per-node proxy that powers Istio's ambient data plane mode," implementing the L4 secure overlay. [source: istio-ambient-mode-2026-08-31] (Chapter 17 §5)

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

## Chapter 17 (2026-08-31)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D4.2 — Cloud Native Ecosystem and Principles | Chapter 17 | deep — whole competency | 2026-08-31 |
| D4.3 — Cloud Native Community and Collaboration | Chapter 17 | deep — whole competency | 2026-08-31 |

### The D4 competency list is now sourced — correction to the draft's own gap note

`cncf-kcna-curriculum-pdf-2026-08-23` line 16 publishes the domain and its competencies:

    12% – Cloud Native Architecture: Observability; Cloud Native Ecosystem
          and Principles; Cloud Native Community and Collaboration

The draft's chapter-wide AUTHOR-REVIEW asserts no cached snapshot supports the
count or the names. It does, and it is the snapshot all sixteen shipped chapters
already cite. Two corrections follow: the third competency is **Observability**,
not "Cloud Native Observability"; and the metadata line should follow shipped
Ch 16's form at ch16:227.

### The curriculum's own ordering corroborates the chapter split

The curriculum lists Observability first, then Ecosystem and Principles, then
Community and Collaboration. The outline's D4.2/D4.3 labels map onto that
ordering exactly, which makes **D4.1 = Observability = Chapter 18**. The authored
7/5 allocation of the domain's 12% therefore falls on a competency boundary CNCF
itself draws, rather than on a line this book invented. That is a materially
stronger position than the draft claims for itself, and the disclosure in
"Why This Chapter Matters" can say so.

### What remains unpublished, and must stay disclosed

CNCF publishes weights at the domain level only. There is no published
per-competency weighting [source: lf-kcna-exam-page-2026-08-23]
[source: cncf-kcna-curriculum-pdf-2026-08-23]. The 7/5 split between Chapters 17
and 18 is authored judgment. The chapter discloses this in prose, per B2
disclosure #1, and the disclosure stays.

### The retired blueprint is still genuinely open

There is no `cncf-kcna-curriculum-retired-*.md` in sources/.
`cncf-curriculum-repo-kcna-versions-2026-08-23` documents the two 2025-11-24
commits and the archived PDF's URL, then states: "The retired domain weights are
NOT recorded in this snapshot… DO NOT draft the retired weights from memory or
from third-party study guides."

The revision's removal of the comparative claims ("Container Orchestration rose
to 28%", "Application Delivery doubled to 16%") was correct. This is the fourth
consecutive chapter to rule on it. Restore only if the archived PDF is cached.

### Two competencies in one chapter

Chapter 17 is the only chapter in this book carrying two whole competencies,
which is the stated reason it is the longest. No D4.2 or D4.3 material is
deferred.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

## Chapter 17 (2026-08-31)

| Tested topic | Original chapter | Retested in |
|---|---|---|
| image immutability vs immutable infrastructure | ch 2 §2 | ch 17 Bearings 1 Q6 |
| the four pluggable interfaces | ch 2 §4 · 6 §8 · 9 §1 · 11 §5 | ch 17 Bearings 2 Q1 |
| NetworkPolicy cannot encrypt | ch 10 §6–§7 | ch 17 Bearings 2 Q3, Practice Q12 |
| CRD vs API aggregation | ch 6 §8 | ch 17 Practice Q9 |
| Helm crds/ ordering | ch 14 §6 | ch 17 Practice Q10 |
| metrics-server / kubectl top | ch 13 §7 | ch 17 Practice Q16 |
| Pending / unschedulable / preemption | ch 7 §2 | ch 17 Practice Q17 |
| release cadence + support window | ch 8 §6 | ch 17 Bearings 3 Q4, Practice Q19 |
| the absent-component pattern | ch 3 (phrase) · ch 10 §3 (named) | ch 13 x3, ch 17 §7 |
| version-skew decay anchor | ch 8 §6 | ch 17 §8 |

### Compliance against B3

B3 sets Chapter 17 at the 25% ceiling — one of five chapters there, "because
retrieval IS the chapter's method, not a tax on it."

Measured: 4 of 16 checkpoint questions (25%) and 6 of 21 practice questions
(29%). Practice is over ceiling. Over on the safe side, and recorded rather
than cut.

Spacing floor (from Ch 8 on, at least one item from >=4 chapters back): met
several times over — Ch 2, 6, 7, 8, 10, 13, 14 are all reached.

### B3's four prohibitions — all four honored

1. No Chapter 1 exam mechanics retrieved.
2. The dated Graduated-project roster is explicitly REFUSED. §2's Worth
   Securing: "Learn the levels, not the roster… no responsible study guide
   should ask you to memorize a list that changes faster than it prints."
   Six project names are given as ballast with the instruction repeated.
3. No 60-question or 75% figures anywhere.
4. Neither [inferred] trap row is framed as exam frequency; both use the
   ratified "(Easy to confuse …)" form.

### B3's named decay repair, delivered

B3 flagged Ch 8's version-skew block as "the densest pure-recall material in
the book, taught at the 40% mark and otherwise never revisited before exam
day," and scheduled release cadence into Ch 17 "where the three-supported-
minors rule and the ~3/year cadence explain each other."

Chapter 17 §8 does exactly this and goes further, deriving the ~1-year support
window from the two numbers and then confirming it independently from the same
source. Three integers become one relationship. This is the repair B3 asked
for, in the strongest available form.

### ONE OPEN DEBT, and it is Chapter 8's promise, not Chapter 17's

Chapter 8 says "fifteen weeks" three times (ch08:861, :1003, :1009) and at
:1009 promises: "where SIG Release and the KEP process explain WHERE THOSE
FIFTEEN WEEKS GO." The number appears nowhere in Chapter 17.

Chapter 17 §8 declined the 15-week figure deliberately (its AUTHOR-REVIEW
prefers the current page's "approximately three times per year") without
knowing Ch 8 had shipped the promise twice. But §8 already contains the
accounting: Enhancements Freeze ~week 4, Code Freeze from ~week 12 for ~2
weeks, post-release from week 14.

FIX: one clause after §8's phase list — "That is where the fifteen weeks
Chapter 8 gave you actually go." Both halves stay true. The alternative is
editing shipped Chapter 8, which is more expensive.

### THE PATTERN-WORDING DRIFT — book-level, three variants, five chapters

The integration report claims Ch 13 never retrieves the absent-component
pattern and that Ch 17 is therefore the last chance. Measured, that is wrong.
Chapter 13 retrieves it three times.

  Variant A  "an object without its component does nothing"
             ch 3 x2, ch 10 x12, ch 11 x4  = 18 occurrences, the ★ Fixed Point
  Variant B  "the object exists; nothing happens without the component"
             ch 13 x3 (:300, :1279, :1281), ch 17 §7, and the B7 ledger row :339
  Variant C  "the object exists BUT nothing happens without the component"
             ch 6 x2 (:1005, :1082), and B3's own summary

Chapter 17 matches Chapter 13 and its own binding contract. This is a
book-wide unification sweep, not a Chapter 17 defect, and the promised
retrieval did land in Chapter 13.

RECOMMEND standardizing on Variant A — 18 of 23 occurrences, the ★ Fixed
Point, and inside a graded Ch 11 answer option — then correcting B3, B7,
Ch 6, Ch 13 and Ch 17 in one commit.

STILL TO FIX IN CH 17 REGARDLESS: the attribution. §7 says "Chapter 10 §3
christened it." Chapter 3 both names the pattern (ch03:601) and gives the
phrase; Ch 11:811 says so: "The phrase is Chapter 3's, and Chapter 10 §3
named it as a pattern." Recast to "Chapter 3 gave you the phrase and Chapter
10 §3 named it as a pattern."

### Forward obligations Chapter 17 creates

- Ch 18 inherits Observability as D4.1 and must not present it as a domain.
- Ch 18 §3 is promised "utilization relative to requests" by Ch 17 §7.
- Ch 19 §2 owes a confusion-pair row for Sandbox (level) vs sandboxed runtime.
- The mesh/cluster control-plane collision needs a Ch 19 confusion-pair row.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interface-pattern.md ===

## Chapter 17 update (2026-08-31) — ⚑⚑ THE COLLECTION POINT. All four interfaces land here.

Chapter 17 §4 is where the book's four pluggable interfaces are finally put side by
side, and §9 is where the shape is named. Chapter 2 §8 promised this would "feel like
recognition rather than a fourth list"; that promise is discharged here.

## ★ Fixed Point (verbatim — do not reword)

**At every one of the four pluggable interfaces — CRI, CNI, CSI, and CRDs — Kubernetes
defines an interface and hands the implementation to somebody else.**

| Interface | Layer | Taught at |
|---|---|---|
| CRI | the container runtime on the node | Ch 2 §4 |
| CNI | pod networking | Ch 9 §1 |
| CSI | storage | Ch 11 §5 |
| CRDs | new object kinds | Ch 6 §8 |

Mnemonic: **Run it, wire it, store it, name it.**

## The grouping is the BOOK'S, and the chapter says so

Kubernetes publishes no document titled "the four pluggable interfaces." Its own list
has six extension points cut differently [source: k8s-docs-extending-kubernetes-2026-08-23].
Ch 17 §4 prints both maps and defends the difference rather than hiding it. See
[[kubernetes-extension-points]].

## The second-order effect (§9's Zenith)

Because the parts that vary sit behind interfaces, they can vary WITHOUT PERMISSION.
A storage vendor ships a CSI driver on their own schedule; you define a CRD on a
Tuesday afternoon. The alternative — Kubernetes shipping each implementation — does not
scale technically OR organizationally, and §8 makes the organizational half concrete:
every such feature would be a KEP, argued in a SIG, competing for review time.

## ⚑⚑ SLUG COLLISION — do not create a third file

The outline's kb_tags names `four-pluggable-interfaces`. Chapter 17's Stage 14
DELIBERATELY DID NOT CREATE IT. Two shards already carry this concept:

  - `pluggable-interface-pattern.md`  (ch-02) — THIS FILE, the canonical one
  - `pluggable-interfaces.md`         (ch-11) — duplicate, flagged as ch-16's ⚑ I2

Merge `pluggable-interfaces.md` into this file at the replay and leave a stub.
Chapter 17 is the last chapter that could have made this decision cheaply.

## Related
[[cri]] [[cni]] [[csi]] [[custom-resource]] [[kubernetes-extension-points]]
[[api-aggregation-layer]] [[device-plugin]] [[one-pluggability-story]]
[[absent-component-pattern]] — the four interfaces are also where that pattern fires.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

## Chapter 17 update (2026-08-31) — the fifth instance, and a WORDING RULING

Chapter 17 §7 fires the pattern at the VerticalPodAutoscaler: the VPA object can be
created on a cluster where no VPA is installed, and nothing acts on it. Same shape as
an Ingress with no controller and `kubectl top` with no metrics-server, one layer over.
See [[vertical-pod-autoscaler]].

## ⚑⚑ THREE PHRASINGS ARE LIVE IN SHIPPED TEXT. Do not "fix" Ch 17 in isolation.

  Variant A  "an object without its component does nothing"
             ch 3 x2, ch 10 x12, ch 11 x4  = 18. The ★ Fixed Point, and inside a
             graded Ch 11 Practice option.
  Variant B  "the object exists; nothing happens without the component"
             ch 13 x3 (:300, :1279, :1281); ch 17 §7; AND the B7 ledger row :339.
  Variant C  "the object exists BUT nothing happens without the component"
             ch 6 x2 (:1005, :1082); AND B3 retrieval-architecture.md's own summary.

The integration report for Ch 17 states that Chapter 13 never retrieves this pattern
and that Ch 17 is the last chance. That is measurably wrong — Ch 13 retrieves it three
times, in Variant B, which is exactly what Ch 17 uses and exactly what the binding
ledger specifies.

RECOMMEND standardizing on VARIANT A and correcting B3, B7, Ch 6, Ch 13 and Ch 17
together. Do not single out Chapter 17.

## ⚠ ATTRIBUTION — this one IS a Ch 17 error and should be fixed now

Ch 17 §7 says "Chapter 10 §3 christened it." Chapter 3 both NAMES the pattern
(ch03:601, "⚓ Worth Securing — the absent-component pattern") and gives the phrase.
Chapter 11:811 states the correct division: "The phrase is Chapter 3's, and Chapter 10
§3 named it as a pattern."

Recast: "Chapter 3 gave you the phrase and Chapter 10 §3 named it as a pattern."

## ⚠ The ledger row is the proximate cause

term-ownership.md:339 carries BOTH errors — Variant B wording, and Ch 10 §3 as the
sole owner. Correct the row or the next stage re-introduces both.

## Related
[[vertical-pod-autoscaler]] [[ingress-controller]] [[resource-metrics-pipeline]]
[[pluggable-interface-pattern]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/release-cadence.md ===

## Chapter 17 update (2026-08-31) — the cadence stops being three integers

Chapter 8 §6 taught three numbers and warned they were "among the most forgettable
material in this book." Chapter 17 §8 collapses them into one relationship.

## ★ Fixed Point (verbatim — do not reword)

**Three minor releases a year, three supported minor versions, and roughly one year of
patch support are not three facts. They are one fact stated three ways. Three releases
per year x three maintained branches ~ one year — and because the documentation states
that year independently, you can DERIVE the support window instead of memorizing it.**

Sourced: releases happen "approximately three times per year"; the project "maintains
release branches for the most recent three minor releases"; "Kubernetes 1.19 and newer
receive approximately 1 year of patch support" [source: k8s-release-cycle-and-cadence-2026-08-31].

The chapter uses a generation-effect break — "do the arithmetic yourself before reading
on" — before confirming. That construction is the technique; preserve it.

## The cycle, and who runs it

SIG Release owns "Production of Kubernetes releases on a reliable schedule"
[source: k8s-release-cycle-and-cadence-2026-08-31]. Three phases: Enhancement
Definition, Implementation, Stabilization. Enhancements Freeze ~week 4; Code Freeze
from ~week 12 for ~2 weeks, during which "only critical bug fixes are accepted";
post-release from week 14. See [[sig-release-and-release-cadence]].

## ⚑⚑ AN OPEN PROMISE FROM CHAPTER 8, NOT YET PAID

Chapter 8 says "fifteen weeks" three times (ch08:861, :1003, :1009) and at :1009
promises Chapter 17 will explain "where those fifteen weeks go." The word "fifteen"
appears NOWHERE in Chapter 17.

Ch 17's AUTHOR-REVIEW declined the 15-week figure on purpose — an older snapshot
(k8s-releases-cadence-2026-08-23) says "approximately every 15 weeks" while the current
page says "approximately three times per year" — but did so without knowing Ch 8 had
shipped the promise twice with the number attached.

§8 ALREADY CONTAINS THE ACCOUNTING. The fix is one clause after the phase list:

    That is where the fifteen weeks Chapter 8 gave you actually go.

Both halves stay true: the cadence is ~3/year per the current page, and the cycle Ch 8
measured at ~15 weeks is the one just described. Alternative — drop "those fifteen
weeks" from ch08:1009 — edits shipped text and costs more.

## Related
[[version-skew]] [[sig-release-and-release-cadence]] [[kubernetes-enhancement-proposal]]
[[kubernetes-sig-wg-committee]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cloud-native-framing.md ===

## Chapter 17 update (2026-08-31) — the book's longest open loop closes

Chapter 1 used the phrase "cloud native" ~40 times, said the common reading ("it runs
in a public cloud") is wrong, then declined to define it and pointed at Chapter 17.
That deferral is ledger flag ⚑4 and it was deliberate. Chapter 17 §1 closes it by
quoting CNCF Cloud Native Definition v1.1 in full rather than paraphrasing.

The correction lands inside the definition's own first sentence: "public, private,
hybrid cloud" [source: cncf-cloud-native-definition-2026-08-23]. The term is about how
you build and operate, not where the machines are. A workload on three servers in a
closet can be cloud native; one on the largest public cloud can fail to be.

Ch 17 §1's construction is worth preserving: the reader writes their own one-sentence
guess at Soundings Q2, then measures it against the published text word for word. The
misconception is retired by collision, not by lecture.

## ⚑ Hyphenation debt (ledger ⚑8) — still open

16 instances of hyphenated "cloud-native" in shipped Ch 1, 2, 3, 4, 8, against the
unhyphenated CNCF form the book now quotes. Chapter 17 itself is CLEAN — its only
hyphenated hits are inside the snapshot filename and a figure anchor. Cosmetic sweep,
author's call, not load-bearing.

## Related
[[cloud-native-definition-v1-1]] [[cloud-native-characteristics]]
[[cncf-mission-and-vendor-neutrality]] [[small-pieces-replaced-whole]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cri.md ===

## Chapter 17 update (2026-08-31)

Collected at Ch 17 §4 as the first of the four pluggable interfaces: Kubernetes needs
to run containers, does not implement a container runtime, publishes the Container
Runtime Interface, and containerd or CRI-O implements it.

Ch 17 does not redefine CRI — Ch 2 §4 taught it in full and §4 points back rather than
repeating. What §4 adds is the comparison: CRI is one instance of a shape, not a
one-off design decision about runtimes.

In the mnemonic: **CRI runs it.**

## Related
[[pluggable-interface-pattern]] [[cni]] [[csi]] [[custom-resource]]
[[one-pluggability-story]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cni.md ===

## Chapter 17 update (2026-08-31)

Collected at Ch 17 §4 as the second of the four pluggable interfaces: Kubernetes states
the network model's requirements, does not implement pod networking, and requires a
plugin satisfying the Container Network Interface — Calico, Cilium, Flannel.

Ch 17 does not redefine it; Ch 9 §1 owns it. §4 adds the pattern membership.

In the mnemonic: **CNI wires it.**

Note the ledger's canonical-form rule: "plugin" is never bare, always qualified by its
interface. Ch 17 §4 conforms — all 11 uses are qualified.

## Related
[[pluggable-interface-pattern]] [[cri]] [[csi]] [[custom-resource]]
[[network-policy]] [[one-pluggability-story]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/csi.md ===

## Chapter 17 update (2026-08-31)

Collected at Ch 17 §4 as the third of the four pluggable interfaces. Ch 17 is careful
about the verb: Kubernetes ADOPTED CSI rather than publishing it. Practice Q8's answer
makes the point explicit with the spec's own objective — to "enable storage vendors
(SP) to develop a plugin once and have it work across a number of container
orchestration (CO) systems" [source: csi-spec-objective-2026-08-25].

That is worth holding: CSI is not a Kubernetes feature vendors happen to use. It is a
cross-orchestrator standard Kubernetes implements. It is the strongest single piece of
evidence for §9's argument.

In the mnemonic: **CSI stores it.**

## Related
[[pluggable-interface-pattern]] [[cri]] [[cni]] [[custom-resource]]
[[storageclass-and-provisioning]] [[one-pluggability-story]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/custom-resource.md ===

## Chapter 17 update (2026-08-31) — the fourth interface, and its two names

Collected at Ch 17 §4. Kubernetes needs object types it did not anticipate, does not
add them, and provides CustomResourceDefinitions instead.

## The naming reconciliation Ch 2 §8 required

Chapter 2 §4 called the set "CRI, CNI, CSI, and API extensions." Chapters 6, 10, 11 and
17 call the fourth one CRDs. Ch 17 §4 settles it: "API extensions" is the
documentation's heading for a category containing TWO things — CRDs and the aggregation
layer. When this book counts four interfaces, the fourth is specifically CRDs, because
that is where the interface-and-implementation shape is cleanest.

The B6 drafting note requiring this reconciliation is discharged.

## CRD vs aggregation — graded from both directions

With a CRD the API server stores and serves your objects. With aggregation you run your
own API server and Kubernetes routes to it. The documentation states the distinction
outright [source: k8s-docs-api-aggregation-and-device-plugins-2026-08-31]. Ch 17 grades
it twice with the constraint reversed, so the two items discriminate rather than
duplicate. See [[api-aggregation-layer]].

## A real instance, not an example

Knative is implemented as CRDs — a whole serverless platform sitting on the fourth
interface, with the API server storing and serving its objects. See [[knative]].

In the mnemonic: **CRDs name it.**

## Related
[[pluggable-interface-pattern]] [[api-aggregation-layer]] [[operator-pattern]]
[[crds-in-charts]] [[knative]] [[one-pluggability-story]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/network-policy.md ===

## Chapter 17 update (2026-08-31) — the gap Ch 10 identified now has a remedy

Chapter 10 §7 established that NetworkPolicy says WHO MAY TALK TO WHOM and cannot
encrypt a single byte, and that TLS terminating at the Ingress leaves the leg to the
Pod in plaintext. Chapter 10 named the gap twice and pointedly declined a remedy.

Chapter 17 §5 is the remedy: a service mesh's mTLS encrypts and mutually authenticates
service-to-service traffic, including that leg. See [[mutual-tls]].

## The boundary table (Ch 17 §5)

| You already have | It gives you | It cannot give you |
|---|---|---|
| Service (Ch 9 §2) | stable virtual address, load balancing | encryption, retries, per-request routing, telemetry |
| Ingress / Gateway API (Ch 10) | L7 north-south routing, TLS termination at the edge | anything about edge-to-Pod |
| NetworkPolicy (Ch 10 §6) | allow-listed connectivity | encryption, identity, observability, traffic shaping |
| service mesh | mTLS between every pair of workloads, per-service telemetry, L7 east-west control | it is not free — more moving parts, more resource use, another control plane |

Summary: Service gives a name, NetworkPolicy gives a fence, a mesh gives a conversation
you can inspect and trust.

## ⚠ Mesh does NOT replace NetworkPolicy

Ch 17 Practice Q12 option C is built on this error. The two are complementary and many
clusters run both; Istio names defense in depth among its own security goals
[source: istio-security-mtls-identity-2026-08-31].

## ⚠ The single most common misreading, retested here

"NetworkPolicy encrypts the traffic on connections it allows." It permits and denies;
it does not protect what it permits. Graded at Ch 17 Bearings 2 Q3 and Practice Q12.

## Related
[[service-mesh]] [[mutual-tls]] [[zero-trust]] [[ingress]] [[cni]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-metrics-pipeline.md ===

## Chapter 17 update (2026-08-31) — the debt Ch 13 §7 opened, paid

Ch 17 §7 states the dependency plainly: "The HorizontalPodAutoscaler (HPA) and
VerticalPodAutoscaler (VPA) use data from the metrics API to adjust workload replicas
and resources to meet customer demand," with metrics-server a "cluster addon component"
and "a reference implementation of the Metrics API"
[source: k8s-docs-resource-metrics-pipeline-2026-08-31].

No Metrics API server — metrics-server or an equivalent — no HPA scaling, and no VPA at
all.

BOTH autoscalers depend on it. That is the addition over Ch 13, which established the
`kubectl top` half.

## The diagnostic shape, graded

Ch 17 Practice Q16 gives an HPA that never scales plus a failing `kubectl top`, and the
failing `top` is the giveaway: both consume the same API. Soundings Q5 tests the same
dependency in the abstract before the reader arrives.

## Related
[[vertical-pod-autoscaler]] [[horizontal-vs-vertical-autoscaling]]
[[absent-component-pattern]] [[api-aggregation-layer]] — metrics-server registers
through the aggregation layer, and its install notes require it
[source: metrics-server-install-2026-08-31].

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/multi-container-pod.md ===

## Chapter 17 update (2026-08-31) — the sidecar's promised return

Chapter 5 §2 promised the sidecar would be met again in Chapter 17. §5 delivers, and
adds a complication: the sidecar was the mesh's ORIGINAL answer and is now ONE OF TWO.

What makes the sidecar mesh model work is exactly what Ch 5 §2 taught — the Pod's
shared network namespace, so the application reaches the proxy on localhost. Envoy
states it from the proxy's side: applications send and receive "to and from localhost
and [are] unaware of the network topology"
[source: envoy-what-is-envoy-2026-08-31].

That is "without code changes," told from the other end. See [[envoy]] and
[[sidecar-and-ambient-modes]].

Ch 17 Soundings Q4 pre-tests the shared-namespace fact before §5 uses it.

## Related
[[service-mesh]] [[envoy]] [[sidecar-and-ambient-modes]] [[pod-shared-context]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod.md ===

## Chapter 17 update (2026-08-31) — serverless does not escape the Pod

Ch 17 §6's ★ Fixed Point rests on this shard: Knative "builds on the Kubernetes Pod
abstraction," and Serving and Eventing "are implemented as Kubernetes Custom Resource
Definitions (CRDs)" [source: knative-overview-2026-08-23].

Serverless workloads on Kubernetes are still containers in Pods. A container image is
still pulled; a Pod is still scheduled onto a node; a kubelet still starts it. What
changed is that none of it happens until a request arrives, and it all goes away again
when requests stop.

The Pod remains the unit of scheduling even at the far end of the abstraction ladder.
That is the most useful thing this chapter says about the Pod.

## Related
[[knative]] [[scale-to-zero]] [[serverless]] [[pod-lifetime]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/image-immutability.md ===

## Chapter 17 update (2026-08-31) — ⚠ the book's SECOND immutability arrives

Ch 17 §3 introduces IMMUTABLE INFRASTRUCTURE and draws the line explicitly, because the
two are easy to collapse:

  - IMAGE IMMUTABILITY (this shard, Ch 2 §2) — a property of a build artifact. Fixed
    content, addressed by digest.
  - IMMUTABLE INFRASTRUCTURE (Ch 17 §3) — an operational discipline for deployed
    systems: replace, do not modify.

The relationship: image immutability is what MAKES the infrastructure discipline
practical, because the thing you replace with is itself fixed and identifiable. They
are not the same claim, and you can have the first without adopting the second.

Ledger canonical form: sense B is ALWAYS the full two-word phrase "immutable
infrastructure." Ch 17 §3 conforms and back-bears here rather than re-deriving.

Graded at Ch 17 Bearings 1 Q6 as a `[retrieval: ch2]` item, with all three wrong
options built on plausible collapses of the distinction.

## Related
[[immutable-infrastructure]] [[tag-vs-digest]] [[container-image]]
[[small-pieces-replaced-whole]] [[pod-lifetime]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-server-hub.md ===

## Chapter 17 update (2026-08-31) — the API surface is extensible in two ways

Ch 17 §4 adds the aggregation layer to what this shard describes. It "allows Kubernetes
to be extended with additional APIs, beyond what is offered by the core Kubernetes
APIs," runs IN-PROCESS with the kube-apiserver, and does nothing until an `APIService`
object claims a URL path — after which it proxies anything on that path to the
registered service [source: k8s-docs-api-aggregation-and-device-plugins-2026-08-31].

So the hub can be extended two ways: CRDs, where the API server itself stores and
serves your objects, and aggregation, where you run the server and Kubernetes routes to
it. More work, more flexibility.

One is already in the reader's cluster: metrics-server registers through the
aggregation layer, and its install notes state the "kube-apiserver must enable an
aggregation layer" [source: metrics-server-install-2026-08-31].

## Related
[[api-aggregation-layer]] [[custom-resource]] [[kubernetes-extension-points]]
[[resource-metrics-pipeline]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pending-pod.md ===

## Chapter 17 update (2026-08-31) — the sentence Ch 7 left open is closed

Chapter 7 §2 said an unschedulable Pod sits in `Pending`, and that its continued
existence is "a standing, machine-readable statement that the cluster is short of
somewhere to put work. Something could be watching for exactly that."

Chapter 17 §7 names the something. A node autoscaler: "If there are Pods in a cluster
that can't be scheduled on existing Nodes, new Nodes can be automatically added to the
cluster — provisioned — to accommodate the Pods"
[source: k8s-docs-node-autoscaling-2026-08-31].

`Pending` is not merely a diagnostic state. It is an INPUT to an automated control
loop. That reframing is what Ch 17 adds.

Pre-tested at Ch 17 Soundings Q6 and graded at Practice Q17, where preemption is the
distractor — preemption relocates a shortage rather than resolving it, and does nothing
when there is no lower-priority work to evict.

## Related
[[node-autoscaling]] [[feasible-node]] [[scheduling]] [[autoscaler-axis-and-trigger]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/crds-in-charts.md ===

## Chapter 17 update (2026-08-31) — retrieved, and a SOURCE TAG IS AVAILABLE

Ch 17 §4 uses the Helm `crds/` directory as evidence that the packaging format had to
grow a special case for the extension mechanism: a chart shipping custom resources must
install the definitions before the objects that use them. Graded at Practice Q10 as a
`[retrieval: ch14]` item.

## ⚑ RESOLVES the draft's own open AUTHOR-REVIEW

Ch 17's AUTHOR-REVIEW asks whether a Helm snapshot exists to tag this claim, and
proposes either reusing Ch 14's snapshot or opening a research gap.

NO GAP IS NEEDED. `sources/helm-crd-best-practices-2026-08-31.md` exists; line 10
carries the declaration-vs-usage distinction; and shipped Ch 14 §6 already cites it for
this exact claim (ch14:987, :991). Apply the tag in §4 and in Practice Q10.

Consistency verified against Ch 14 canon: ch14:987 — "the declaration must be
registered before any resources of that CRDs kind(s) can be used"; ch14:989 — "no
ordering guarantee, and one case where the absence of a guarantee is fatal."

## Related
[[custom-resource]] [[helm-chart]] [[pluggable-interface-pattern]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/twelve-factor-app.md ===

## Chapter 17 update (2026-08-31) — the forward promise, discharged

This shard's own forward note said: "Ch 17 §3 — several cloud-native characteristics
are these factors under newer names." Chapter 17 §3 delivers it as a 🔭 Closer Look:
several of the twelve factors are the same principles as microservices, immutable
infrastructure and declarative APIs, "written for a platform that did not exist yet."

The connection runs both ways and is worth stating once: the twelve factors describe
what an application must accept; the cloud native definition describes what the
resulting system looks like from outside. Same constraints, two vantage points.

Ch 17 §3's synthesis — small pieces, replaced whole, described rather than commanded —
is the architectural statement of the same bargain. See [[small-pieces-replaced-whole]].

## Related
[[small-pieces-replaced-whole]] [[immutable-infrastructure]]
[[microservices-and-monoliths]] [[cloud-native-characteristics]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kcna-exam-format.md ===

## Chapter 17 update (2026-08-31) — the ladder above this exam

Chapter 1 deferred the certification ladder to Chapter 17 by name. §8 answers it, and
the answer is about FORMAT, not difficulty.

KCNA "is a pre-professional certification designed for candidates interested in
advancing to the professional level" and "lays the groundwork for further CNCF
certifications like CKA, CKAD, and CKS" [source: cncf-kcna-certification-page-2026-08-23].

  KCNA  — online and multiple-choice
  CKA   — "a performance-based exam where candidates interact with the command line
           to solve real-world challenges"
  CKAD  — "a hands-on, command-line environment"
  CKS   — "performance-based"

CNCF also offers KCSA and the Cloud Native Network Function certification
[source: cncf-who-we-are-2026-08-23].

The chapter's framing, which is the memorable half: KCNA is the only one on this ladder
you can pass by KNOWING things. Everything above requires DOING things, at a terminal,
under time pressure — which is why the vocabulary has to be solid before going on.

## ⚠ ACRONYM DEBT

CKA is expanded once, at ch01:180. CKAD and CKS are expanded NOWHERE in Chapters 1–17,
though B7 :661–662 assigns both to Ch 17 §8. KCSA's expansion is standard but is not in
the cached corpus. Expand CKAD and CKS at first use in §8.

## Related
[[cncf-certification-ladder]] [[domain-weights-44-28-16-12]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

## Chapter 17 update (2026-08-31) — ⚠ NO ORDINAL ADDED. Compliance record.

The instruction placed on this shard by ch-09's and ch-15's Stage 14 runs stands:
term-ownership.md:754 sanctions exactly TWO control-loop counts in the whole book —
Ch 6's two-altitudes framing and Ch 15 §7's "third time." Ch 15's manifest closed with
"Ch 17 §4 collects the thread and must not add to the count."

VERIFIED: Chapter 17 asserts no control-loop ordinal anywhere. Its repeated "four
times" refers to the closed set of four pluggable interfaces, which the ledger's
2026-08-30 running-ordinal convention explicitly sanctions because the reader can see
all four in one figure.

What Ch 17 DOES add, without counting: §1's practices clause — "programmatic and
repeatable… at scale" — is named as the reason the book spent so much length on
declarative objects and reconciling controllers. The loop is not a Kubernetes quirk;
it is a named characteristic of the paradigm. See [[cloud-native-definition-v1-1]].

Chapter 3 §7's forward promise — that the control loop "turns out to be one of the
things 'cloud native' means" — is discharged here.

## Related
[[cloud-native-definition-v1-1]] [[declarative-configuration]]
[[small-pieces-replaced-whole]] [[control-loop-pointed-at-a-repository]]

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/domain-weights-44-28-16-12.md ===

## Chapter 17 update (2026-08-31) — ⚑ THE COMPETENCY LIST IS SOURCED. Correction.

Chapter 17's chapter-wide AUTHOR-REVIEW asserts that no cached snapshot supports the
count or names of Domain 4's competencies, and treats it as open research gap G33.

THAT IS WRONG. `sources/cncf-kcna-curriculum-pdf-2026-08-23.md` line 16 publishes them:

    12% – Cloud Native Architecture: Observability; Cloud Native Ecosystem
          and Principles; Cloud Native Community and Collaboration

The full curriculum, from CNCF's own publication channel:

  44% – Kubernetes Fundamentals: Core Concepts; Administration; Scheduling;
        Containerization
  28% – Container Orchestration: Networking; Security; Troubleshooting; Storage
  16% – Cloud Native Application Delivery: Application Delivery; Debugging
  12% – Cloud Native Architecture: Observability; Cloud Native Ecosystem and
        Principles; Cloud Native Community and Collaboration

This snapshot is cited by ALL SIXTEEN shipped chapters. Shipped Ch 16 uses it for
exactly this purpose at ch16:227.

## Three corrections that follow

1. Tag Ch 17's Dead Reckoning block [source: cncf-kcna-curriculum-pdf-2026-08-23] and
   delete the second half of the chapter-wide AUTHOR-REVIEW.
2. The third competency is "Observability," NOT "Cloud Native Observability" as the
   draft has it. Ch 18's naming depends on this.
3. Adopt Ch 16's metadata-line form.

## The curriculum's ordering corroborates the 7/5 split

Observability is listed FIRST, so D4.1 = Observability = Chapter 18, and the outline's
D4.2/D4.3 labels for Chapter 17 map onto the curriculum's own order. The authored
allocation falls on a boundary CNCF itself draws.

## ⚠ Still unpublished, and still disclosed

CNCF publishes weights at the DOMAIN level only. No per-competency weighting exists
[source: lf-kcna-exam-page-2026-08-23]. The 7/5 split is authored judgment and the
prose disclosure stays.

## ⚠ Still open: the RETIRED blueprint

No `cncf-kcna-curriculum-retired-*.md` exists.
`cncf-curriculum-repo-kcna-versions-2026-08-23` records the two 2025-11-24 commits and
the archived PDF's URL, then states: "DO NOT draft the retired weights from memory or
from third-party study guides." The removal of the comparative claims stands — fourth
consecutive chapter to so rule.

## ⚑ Frontmatter fix
`cncf-kcna-curriculum-pdf-2026-08-23` should carry
`concepts_covered: ["kcna-competencies", "domain-weights-44-28-16-12"]`. Its current
frontmatter is why three separate stages searched for this list and missed it.

## Related
[[blueprint-change-2025-11-24]] [[published-vs-commonly-reported]] [[kcna-exam-format]]

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cloud-native-definition-v1-1.md ===
# Concept: CNCF Cloud Native Definition v1.1

The published document Chapter 1 refused to paraphrase, quoted whole at Ch 17 §1
[source: cncf-cloud-native-definition-2026-08-23].

> Cloud native practices empower organizations to develop, build, and deploy workloads
> in computing environments (public, private, hybrid cloud) to meet their organizational
> needs at scale in a programmatic and repeatable manner. It is characterized by loosely
> coupled systems that interoperate in a manner that is secure, resilient, manageable,
> sustainable, and observable.
>
> Cloud native technologies and architectures typically consist of some combination of
> containers, service meshes, multi-tenancy, microservices, immutable infrastructure,
> serverless, and declarative APIs — this list is non-exhaustive.
>
> These techniques enable loosely coupled systems that are resilient, manageable, and
> observable. Combined with robust automation, they allow engineers to make high-impact
> changes frequently and predictably with minimal toil and clear separation of concerns.
>
> The Cloud Native Computing Foundation seeks to drive adoption of this paradigm by
> fostering and sustaining an ecosystem of open source, vendor-neutral projects. We
> democratize state-of-the-art patterns to make these innovations accessible for everyone.

## Four clauses

- **Practices** — programmatic, repeatable, at scale. Every load-bearing word is about
  METHOD. This is why the book spent so long on declarative objects and reconciling
  controllers.
- **Characteristics** — the quotable part. See [[cloud-native-characteristics]].
- **Technology** — seven items, and "this list is non-exhaustive" in the same sentence.
- **Payoff** — high-impact changes made frequently and predictably, minimal toil, clear
  separation of concerns. If a practice does not move you toward that, it is cargo cult.

## ★ The misconception, retired in one clause

"public, private, hybrid cloud" appears before the first sentence is half over. Cloud
native does NOT mean "runs in a public cloud." A workload on three servers in a closet
can be cloud native; one on the largest public cloud can fail to be.

## ⚠ The technology list is NOT closed

Seven items in an authoritative document read like an enumeration. The document says
otherwise in the same breath. Graded twice (Bearings 1 Q5, Practice Q1/Q2), and the
chapter deliberately places it three sections before §4's list, which genuinely IS
finite — two lists, only one closed.

## Related
[[cloud-native-characteristics]] [[cloud-native-framing]] [[loose-coupling]]
[[cncf-mission-and-vendor-neutrality]] [[small-pieces-replaced-whole]] [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cloud-native-characteristics.md ===
# Concept: The five characteristics of cloud native systems

## ★ Fixed Point (verbatim — do not reword)

**Cloud native is characterized by loosely coupled systems that interoperate in a manner
that is secure, resilient, manageable, sustainable, and observable.**

[source: cncf-cloud-native-definition-2026-08-23]

## The structure matters as much as the list

Five characteristics ATTACHED TO loosely coupled systems — not five characteristics
floating free. The loose coupling is the spine; the five are what a loosely coupled
system must manage to be worth having.

| Characteristic | What it costs you to skip |
|---|---|
| Secure | verification at every boundary, not just the edge |
| Resilient | survives the loss of any one part |
| Manageable | changeable without rebuilding it |
| Sustainable | affordable to keep running, in people and in power |
| Observable | you can ask it what it is doing, and it will answer |

## ⚠ The two most-dropped items

"Sustainable" and "observable" are what distinguish this list from a generic
software-quality list, and they are the two candidates most often drop. Practice Q1's
distractor D is built precisely on that.

## Where each is delivered elsewhere in the book

Secure — Ch 12 and Ch 17 §5. Resilient — Ch 6. Manageable — Ch 14, Ch 15.
Observable — Ch 18. Sustainable is the one the book touches least directly; §7's node
consolidation is its clearest instance.

## Related
[[cloud-native-definition-v1-1]] [[loose-coupling]] [[zero-trust]]
[[node-autoscaling]] [[small-pieces-replaced-whole]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-mission-and-vendor-neutrality.md ===
# Concept: The CNCF as an institution

Part of the nonprofit Linux Foundation [source: cncf-who-we-are-2026-08-23]. Mission
stated in one line: **to make cloud native computing ubiquitous**
[source: cncf-charter-governance-bodies-2026-08-31].

Hosts critical components of global technology infrastructure — Kubernetes, Prometheus,
Envoy among them: **227 projects** at the time of this book's research, across four
categories, with **715 member organizations** and over **329,000 project contributors**
[source: cncf-who-we-are-2026-08-23].

## Vendor-neutral is a STRUCTURAL claim, not a marketing one

The CNCF does not sell you anything. It holds projects no single company owns, so that
a company adopting Kubernetes is not betting on one vendor's continued goodwill. The
governance structure is what makes that true, which is why §2 follows §1.

## ⚠ Two senses of "CNCF" in this book

Chapter 1 meets the CNCF as the body that issues the credential and publishes the
blueprint. Chapter 17 §1 meets it as an institution with a mission, a project
portfolio, and governance. Both are correct; the ledger assigns the exam-sponsor sense
to Ch 1 and the institutional sense to Ch 17 §1.

## ⚠ Do not confuse with the OCI

The Open Container Initiative is a DIFFERENT standards body with an overlapping mission
(Ch 2 §5). Keep them distinct.

## Related
[[cncf-governance-bodies]] [[cncf-project-maturity-levels]] [[cncf-landscape]]
[[oci]] [[cloud-native-definition-v1-1]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-project-maturity-levels.md ===
# Concept: CNCF project maturity levels

## ★ Fixed Point (verbatim — do not reword)

**Sandbox → Incubating → Graduated, in that order.**

- **Sandbox** — experimental projects, not yet widely tested in production, on the
  bleeding edge of technology.
- **Incubating** — used successfully in production by a small number of users, with a
  healthy pool of contributors.
- **Graduated** — stable, widely adopted, production ready, attracting thousands of
  contributors.

[source: cncf-project-maturity-levels-2026-08-23]

## Read them as claims about EVIDENCE, not quality

A Sandbox project is not bad; it is unproven. An Incubating project is not
half-finished; somebody runs it in production and there are enough hands to keep it
alive. A Graduated project is one where the evidence is overwhelming enough that the
foundation will point at it and say: safe to build on.

## ⚠ Archived is NOT a rung

"inactive or low activity projects that are no longer supported"
[source: cncf-toc-project-lifecycle-process-2026-08-31]. Projects do not climb to it;
it is the exit. Graded as a distractor twice.

## ⚠ LEARN THE LEVELS, NOT THE ROSTER — and this is a B3 prohibition

B3 explicitly forbids retrieving the dated Graduated-project roster. Ch 17 §2 honors
it in the reader's sight: "no responsible study guide should ask you to memorize a list
that changes faster than it prints."

Six Graduated projects are named as ballast only, all already met by name in this book
(2026-08-23 snapshot): containerd, CoreDNS, etcd, Helm, Prometheus, Argo. Kubernetes
itself is Graduated — it climbed the same ladder.

## ⚠ Terminology
The lifecycle document says "Incubation" (the process); the projects page says
"Incubating" (the level). This book uses **Incubating** throughout.

## ⚠ Homonym
CNCF **Sandbox** (capitalized, always beside a sibling level) vs a **sandboxed runtime**
— gVisor, Kata, Ch 2 §7, adjectival only. A Ch 19 §2 confusion-pair row is owed.

## Related
[[cncf-project-lifecycle]] [[cncf-governance-bodies]] [[cncf-landscape]]
[[knative]] [[keda-event-driven-autoscaling]] [[node-autoscaling]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-project-lifecycle.md ===
# Concept: The CNCF project lifecycle — where the criteria actually live

## ⚠ The examinable distinction

The **projects page** tells you what the LEVELS MEAN. It does not tell you what a
project must DO to move between them. The criteria live in the **CNCF TOC's project
lifecycle documentation**, in the TOC's own repository
[source: cncf-project-maturity-levels-2026-08-23]: due diligence, adopter interviews,
governance and security requirements.

A question asking where graduation criteria are defined is testing whether you know
these are two different documents. Graded at Bearings 1 Q3, where "on the projects
page, beside each maturity level" is the trap — reasonable-sounding, because the levels
and criteria feel like they should live together, and they do not.

## The process

Application issue on the TOC repository → adopter interview form naming real adopters
willing to be interviewed → TOC sponsor assigned → kickoff meeting → due diligence
document → interviews with those adopters → internal TOC comment period → public
comment period → TOC vote
[source: cncf-toc-project-lifecycle-process-2026-08-31].

Not a rubber stamp: a months-long evidence-gathering exercise in which strangers are
asked, on the record, whether they actually run the thing.

## 🔭 Numbers — NOT exam material, recorded so they are not mistaken for it

Five to seven adopters on the interview form; ~1 week internal comment; 2 weeks public
comment; two-thirds supermajority of the TOC
[source: cncf-toc-project-lifecycle-process-2026-08-31]. TOC operating detail, not
blueprint material. Ch 17 marks them 🔭 deliberately.

## Related
[[cncf-project-maturity-levels]] [[cncf-governance-bodies]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-governance-bodies.md ===
# Concept: CNCF governing bodies

Consolidated deliberately: the Board/TOC pair IS the confusion this material tests, so
splitting them across files would lose the discrimination.

## The Governing Board

"responsible for marketing and other business oversight and budget decisions for the
CNCF" [source: cncf-charter-governance-bodies-2026-08-31]. Money, marketing, and the
boundaries of what the foundation is for.

## The Technical Oversight Committee (TOC)

The technical governing body, facilitating "driving neutral consensus for: defining and
maintaining the technical vision for the Cloud Native Computing Foundation"
[source: cncf-charter-governance-bodies-2026-08-31]. Its README expands the list:
approving new projects **within the scope of the CNCF set by the Governing Board**;
creating a conceptual architecture; aligning projects; removing or archiving them;
accepting End User TAB feedback and mapping it to projects
[source: cncf-toc-and-tags-2026-08-23].

## 🪢 Mnemonic (preserve — it carries the most-confused pair)

**The Board draws the fence. The TOC decides what lives inside it.**

## Technical Advisory Groups (TAGs)

The TOC's technical arms. See [[cncf-tags]].

## The End User Technical Advisory Board (End User TAB)

"will serve as the voice of End Users in the CNCF community, advance topics of concern
to End Users, and raise awareness about the needs and perspectives of end users"
[source: cncf-charter-governance-bodies-2026-08-31]. The TOC's own responsibilities
include "accepting feedback from the end user technical advisory board and mapping it to
projects" [source: cncf-toc-and-tags-2026-08-23]. A DESIGNED feedback path, closing a
loop — not a suggestion box.

## ⚠ Common inversions, all graded
- "The Board approves projects within the TOC's technical vision" — exactly backwards.
  Tempting because "Technical Oversight Committee" sounds more senior than "Board."
- "The End User TAB approves projects" — it feeds requirements; it does not vote.
- "A TAG approves projects in its own area" — TAGs coordinate and bridge; the vote is
  the TOC's.

## Related
[[cncf-tags]] [[cncf-project-lifecycle]] [[cncf-mission-and-vendor-neutrality]]
[[kubernetes-sig-wg-committee]] — a DIFFERENT structure with confusingly similar words.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-tags.md ===
# Concept: CNCF Technical Advisory Groups (TAGs)

"the primary organizational units within the CNCF that oversee and coordinate interests
across projects, working groups, and the broader cloud native community," serving "as
bridges between CNCF projects, end users, and the Technical Oversight Committee"
[source: cncf-tags-current-structure-2026-08-31].

## ⚠ NAVIGATIONAL HAZARD — the list was restructured in 2025

The **current five** [source: cncf-tags-current-structure-2026-08-31]:

| TAG | Scope, in the source's own words |
|---|---|
| Developer Experience | Databases, Microservices, Streaming, Messaging, API Management, Developer Frameworks |
| Infrastructure | Data, Storage, Network, DNS, Compute, Service Mesh, Infrastructure-as-Code, Edge, Sovereignty, Load Balancing |
| Operational Resilience | Observability, Management, Business Continuity, Resource Optimization, Cost Efficiency, Energy, Performance, Troubleshooting, Reliability, Day 2 Operations |
| Security and Compliance | Security Hygiene, Policy-as-Code, Compliance, Auditing, Threat Modeling, Secure Software Supply Chain |
| Workloads Foundation | Fundamental cloud native workload execution environments and lifecycle management |

The **pre-2025** list — App Delivery, Contributor Strategy, Environmental
Sustainability, Network, Observability, Runtime, Security, Storage
[source: cncf-toc-and-tags-2026-08-23] — is still all over older guides, blog posts and
courses, so a reader may well arrive holding it. Restructuring approved by the TOC and
announced May 2025 [source: cncf-tags-current-structure-2026-08-31].

If a question offers "TAG Observability," it is offering the old map.

## ⚠ TAGs are NOT Kubernetes SIGs — and there is a historical reason

"By June 2019, this number had grown to 37 projects and the TOC approved the creation
of SIGs, later to be renamed Technical Advisory Groups"
[source: cncf-tags-current-structure-2026-08-31].

They were the same word once, at two scales, and CNCF renamed theirs. TAGs operate
across the whole foundation; SIGs operate inside the Kubernetes project.

## Related
[[cncf-governance-bodies]] [[kubernetes-sig-wg-committee]] [[cncf-landscape]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-landscape.md ===
# Concept: The CNCF Landscape

"a map through the previously uncharted terrain of cloud native technologies,"
attempting to categorize most of the projects and product offerings in the space, "of
which CNCF-hosted projects are a particularly well-traveled path"
[source: cncf-landscape-and-community-2026-08-23].

The interactive version at landscape.cncf.io is generated from the repository's data
files. Entries must represent cloud native technologies with meaningful community
adoption, fit an existing category, and appear in the single category where they best
fit.

## The categories, by layer

- **Provisioning** — automation and configuration, container registries, security and
  compliance, key management
- **Runtime** — cloud native storage, container runtime, cloud native network
- **Orchestration and Management** — scheduling and orchestration, coordination and
  service discovery, service proxy, API gateway, service mesh
- **App Definition and Development** — databases, streaming and messaging, application
  definition and image build, CI/CD
- **Observability and Analysis** — monitoring, logging, tracing, chaos engineering
- **Platforms and Special** — Kubernetes distributions, hosted and installable
  platforms, PaaS and container services, serverless

[source: cncf-landscape-and-community-2026-08-23]

## The observation worth keeping

Read slowly, that list is roughly this book's table of contents in a different order.
Runtime is Ch 2. Cloud native network is Ch 9–10. Storage is Ch 11. Scheduling and
orchestration is Ch 3–8. CI/CD is Ch 14–15. Service mesh and serverless are Ch 17
§5–§6. Observability is Ch 18.

Entries are also tagged by the owning TAG — the governance structure and the map are
the same structure seen from different sides.

## ⚠ The Landscape is NOT where graduation criteria live
Graded as a distractor at Bearings 1 Q3. It catalogs the terrain and has nothing to do
with graduation.

## ⚠ Deliberate omission, recorded so it is visible
Cost management — FinOps, OpenCost, Kubecost — is omitted from Ch 17. The Landscape's
categories name no cost layer, `opencost-overview-2026-08-23.md` sits unused in the
corpus, and D4's sub-objectives are not enumerated in any cached source. If reversed,
the minimal home is one ungraded clause beside Observability and Analysis.

## Related
[[cncf-tags]] [[cncf-governance-bodies]] [[cncf-project-maturity-levels]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/microservices-and-monoliths.md ===
# Concept: Microservices and monoliths

Consolidated deliberately: the CNCF glossary argues BOTH sides, and separating them
would lose the argument, which is the examinable content.

## Microservices

"an architectural approach that breaks applications into individual independent
(micro)services, with each service focused on a specific functionality"
[source: cncf-glossary-microservices-monoliths-coupling-2026-08-31].

The problem, stated as a scaling complaint: in a monolith, if one function gets
hammered, "the entire app would have to be scaled to accommodate the increase — a very
inefficient use of resources." Everything ships together, so everything scales together.

The benefit: "different teams to work simultaneously on a small part of a bigger
application without inadvertently negatively impacting the rest of the app."

## The bill, which the glossary states honestly

"it also creates operational overhead — the things you need to deploy and keep track of
increase by ORDER OF MAGNITUDE"
[source: cncf-glossary-microservices-monoliths-coupling-2026-08-31].

## ⚓ The foundation for cloud native computing argues against microservices, in writing

A well-designed monolith "can uphold lean principles by being the simplest way to get
an application up and running." Early in a product's life it may be advantageous to
defer the complexity: "Crafting a microservices-based app before it has proven valuable
may be premature spending of engineering effort. If the application yields no value,
that effort becomes wasted."

Take it as a license to think, not a license to argue. The exam tests what microservices
ARE and what they TRADE AWAY, not which you should pick.

## ⚠ The misconception worth catching
Microservices do not REDUCE total complexity. They redistribute WHO CARRIES which
complexity. Practice Q7 option B is built on this.

## Related
[[loose-coupling]] [[small-pieces-replaced-whole]] [[immutable-infrastructure]]
[[service-mesh]] — meshes exist because of the operational overhead named above.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/loose-coupling.md ===
# Concept: Loosely coupled architecture

"an architectural style where individual components are built independently of one
another, each performing a specific function in a way that can be used by any number of
other services." It is "generally slower to implement than tightly coupled architecture
but has a number of benefits, particularly as applications scale," chiefly that teams
can "develop features, deploy, and scale independently"
[source: cncf-glossary-microservices-monoliths-coupling-2026-08-31].

## ⚠ Not a separate concept that happens to share a name

This is THE SAME loose coupling the CNCF definition hangs its five characteristics on
(§1). The book states this explicitly, because a reader meeting the phrase twice in one
chapter will otherwise assume two senses.

The definition's structure depends on it: five characteristics ATTACHED TO loosely
coupled systems. See [[cloud-native-characteristics]].

## Note the honest cost
"Generally slower to implement." The glossary does not sell loose coupling as free, and
neither should the book.

## Related
[[cloud-native-characteristics]] [[cloud-native-definition-v1-1]]
[[microservices-and-monoliths]] [[small-pieces-replaced-whole]]
[[knative-serving-versus-eventing]] — Eventing enables "loose coupling between event
producers and consumers," the same idea at the messaging layer.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/immutable-infrastructure.md ===
# Concept: Immutable infrastructure

**"Immutable Infrastructure refers to computer infrastructure (virtual machines,
containers, network appliances) that cannot be changed once deployed."**
[source: cncf-glossary-immutable-infrastructure-2026-08-31]

You do not patch a running thing. You build a new thing and replace the old one.
Enforcement comes either from automation that overwrites unauthorized modifications, or
from systems that prevent changes altogether.

## The benefit the glossary reaches for FIRST is not security

"Operating such a system becomes a lot more straightforward because administrators can
make assumptions about it." When nothing drifts, what you deployed is what is running,
and you can reason about it. Combined with version control, "there is a durable audit
log of every authorized change to a system"
[source: cncf-glossary-immutable-infrastructure-2026-08-31].

Worth noticing which benefit comes first — reasoning, not hardening.

## ⚠ THE BOOK'S SECOND IMMUTABILITY

  - IMAGE IMMUTABILITY (Ch 2 §2) — a property of a build ARTIFACT, fixed content
    addressed by digest.
  - IMMUTABLE INFRASTRUCTURE (here) — an operational DISCIPLINE for deployed systems.

The first makes the second practical; they are not the same claim. Ledger canonical
form: ALWAYS write the full two-word phrase. Graded at Bearings 1 Q6.

Neither concept is confined to one substrate — the glossary's definition names "virtual
machines, containers, network appliances" together.

## Where the reader already met it as behavior
Ch 5 §4 — a Pod is scheduled once and replaced, never moved. That is this discipline
enacted at the Pod level, before it had a name.

## Related
[[image-immutability]] [[small-pieces-replaced-whole]] [[pod-lifetime]]
[[twelve-factor-app]] [[microservices-and-monoliths]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/small-pieces-replaced-whole.md ===
# Concept: Small pieces, replaced whole — why the three principles are one argument

Absorbs `declarative-api-as-a-characteristic`. This is Ch 17 §3's synthesis and the
only thing in that section not available elsewhere in the book.

## The argument

You can only replace a piece WHOLE if the piece is small and independently deployable.
**That is microservices.**

You can only make replacement the default operation if the thing being replaced was
never meant to be edited in the first place. **That is immutable infrastructure.**

And you can only do that safely, repeatedly, at scale, if what you replace it with is
DESCRIBED rather than COMMANDED — if you can say "there should be five of these, at this
version" and have something else work out the difference. **That is declarative APIs.**

## Take any one away

- Small pieces you have to patch in place are just a distributed monolith with extra
  network hops.
- Immutable replacement of a monolith means redeploying everything to change one line.
- Declarative desired state over components you edit by hand is a description that is
  constantly wrong.

That is what §1's "loosely coupled systems… combined with robust automation" is actually
made of.

## Declarative APIs are NAMED in the definition

The thing the reader has been doing since Chapter 4 — describing desired state and
letting a controller reconcile — is not a Kubernetes quirk. It is a named cloud native
technology [source: cncf-cloud-native-definition-2026-08-23].

## Related
[[microservices-and-monoliths]] [[immutable-infrastructure]] [[loose-coupling]]
[[declarative-configuration]] [[control-loop]] [[twelve-factor-app]]
[[cloud-native-definition-v1-1]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubernetes-extension-points.md ===
# Concept: Kubernetes extension points (the documentation's own map)

Absorbs `extension-point`. Printed at Ch 17 §4 BESIDE this book's four pluggable
interfaces, deliberately, so the reader holds both maps.

| # | Extension point | What it lets you replace or add |
|---|---|---|
| 1 | kubectl plugins and client credential providers | client-side behavior |
| 2 | API access extensions | authentication, authorization, dynamic admission control via webhooks (Ch 8 §2) |
| 3 | API extensions | CustomResourceDefinitions AND the API aggregation layer |
| 4 | Scheduling extensions | scheduler plugins, profiles, custom schedulers (Ch 7 §6) |
| 5 | Controllers | custom controllers over custom or built-in resources; the operator pattern |
| 6 | Infrastructure extensions | device plugins; storage plugins (CSI); network plugins (CNI); container runtime (CRI); kubelet image credential providers |

[source: k8s-docs-extending-kubernetes-2026-08-23]

Six extension points, with five plugin types crammed into the sixth, and custom
resources filed under a completely different heading from the storage and network
plugins they sit beside in the book's four.

## ⚓ Both maps are correct — they answer different questions

The documentation answers *where can I hook in?* The book answers *what is the pattern?*

**"When two authoritative-looking lists of the same subject have different lengths, the
useful question is almost never 'which is right.' It is 'what is each one for.' Hold
both. The exam can ask you either."**

## Related
[[pluggable-interface-pattern]] [[api-aggregation-layer]] [[device-plugin]]
[[admission-control]] [[operator-pattern]] [[scheduling]]
[[policy-engines-and-runtime-detection]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-aggregation-layer.md ===
# Concept: The API aggregation layer

"The aggregation layer allows Kubernetes to be extended with additional APIs, beyond
what is offered by the core Kubernetes APIs." It runs in-process with the
kube-apiserver and does nothing until you register an `APIService` object, which
"claims" a URL path in the Kubernetes API. From then on the layer proxies anything sent
to that path to the registered service
[source: k8s-docs-api-aggregation-and-device-plugins-2026-08-31].

## ★ The distinction the documentation states outright

"The aggregation layer is different from Custom Resource Definitions, which are a way to
make the kube-apiserver recognise new kinds of object."

- **CRD** — the API server stores and serves your objects FOR you.
- **Aggregation** — you run your own API server; Kubernetes routes to it.

More work, more flexibility.

## Already in the reader's cluster

metrics-server registers through the aggregation layer; its install notes state the
"kube-apiserver must enable an aggregation layer"
[source: metrics-server-install-2026-08-31]. The reader has been depending on this
mechanism since Chapter 13 without knowing its name.

## Graded from BOTH directions — deliberately

- Bearings 2 Q2: team ALREADY RUNS its own API server → aggregation is right, CRD is
  the trap.
- Practice Q9: team wants NO additional server process → CRD is right, aggregation is
  the trap.

The constraint in the stem is what separates them. Two items that discriminate rather
than duplicate.

## Related
[[custom-resource]] [[api-server-hub]] [[kubernetes-extension-points]]
[[resource-metrics-pipeline]] [[pluggable-interface-pattern]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/device-plugin.md ===
# Concept: Device plugins

Device plugins "let you configure your cluster with support for devices or resources
that require vendor-specific setup, such as GPUs, NICs, FPGAs, or non-volatile main
memory." A device plugin registers with the kubelet, "sends the kubelet the list of
devices it manages, and the kubelet is then in charge of advertising those resources to
the API server as part of the kubelet node status update"
[source: k8s-docs-api-aggregation-and-device-plugins-2026-08-31].

## The shape should look familiar

Kubernetes does not know what a GPU is. It knows how to ADVERTISE A RESOURCE SOMEBODY
ELSE TOLD IT ABOUT. That is the §4 pattern again, at the hardware layer — which is why
the documentation files it under infrastructure extensions alongside CRI, CNI and CSI.

## ⚠ Graded twice as a distractor, in both directions

- Bearings 2 Q2 — offered where the aggregation layer is correct.
- Practice Q8 — offered where CSI is correct.

Both times the discriminator is the same: device plugins advertise HARDWARE RESOURCES
to the kubelet. They do not serve APIs and they do not mount volumes.

## Ledger note
"plugin" is never bare — always qualified by its interface. "Device plugin" is one of
the sanctioned qualified forms.

## Related
[[kubernetes-extension-points]] [[pluggable-interface-pattern]] [[csi]]
[[node-components]] [[resource-request]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/service-mesh.md ===
# Concept: Service mesh

Absorbs the "what a mesh adds" boundary table — the two are one argument.

"In a microservices world, apps are broken down into multiple smaller services that
communicate over a network. Just like your wifi network, computer networks are
intrinsically unreliable, hackable, and often slow. Service meshes address this new set
of challenges by managing traffic (i.e., communication) between services and adding
reliability, observability, and security features uniformly across all services"
[source: cncf-glossary-service-mesh-2026-08-31].

## ★ Fixed Point (verbatim — do not reword)

**Service meshes add reliability, observability, and security features uniformly across
all services across a cluster WITHOUT REQUIRING CODE CHANGES. Before service meshes,
that functionality had to be encoded into every single service, becoming a potential
source of bugs and technical debt.**

[source: cncf-glossary-service-mesh-2026-08-31]

Istio states its own version almost identically: a mesh "gives applications capabilities
like zero-trust security, observability, and advanced traffic management, without code
changes" [source: istio-service-mesh-2026-08-23].

## ⚠ "Without code changes" is the DEFINING property, not a flourish

If an answer option says a mesh requires the application to be modified, instrumented,
or recompiled, it is describing something else. Graded at Practice Q11, where the
distractor is SDK-based instrumentation — the option a reader who has only met
library-based tracing will reach for.

## Three reasons to want one
Security (zero-trust, workload identity, mTLS, policy) · Observability (telemetry
generated within the mesh) · Traffic management (service-level routing for A/B testing
and canary deployments) [source: istio-service-mesh-2026-08-23].

## What it adds over what you already have

| You already have | It gives you | It cannot give you |
|---|---|---|
| Service (Ch 9 §2) | stable virtual address, load balancing | encryption, retries, per-request routing, telemetry |
| Ingress / Gateway API (Ch 10) | L7 north-south routing, TLS termination at the edge | anything about edge-to-Pod |
| NetworkPolicy (Ch 10 §6) | allow-listed connectivity | encryption, identity, observability, traffic shaping |
| a service mesh | mTLS between every pair of workloads, per-service telemetry, L7 east-west control | it is not free |

Service gives a name, NetworkPolicy gives a fence, a mesh gives a conversation you can
inspect and trust.

## The honest cost
The sidecar model "uses more computing resources and becomes more complex to manage as
your system grows" [source: cncf-glossary-service-mesh-2026-08-31] — the pressure
ambient mode responds to.

## Scope for this tier
Know what a mesh IS and what it BUYS, not how to configure one. Istio and Linkerd are
the two most widely deployed. If you are learning a mesh's own custom resource names,
you have gone past the exam.

## Related
[[mesh-data-plane-vs-control-plane]] [[sidecar-and-ambient-modes]] [[envoy]]
[[mutual-tls]] [[zero-trust]] [[network-policy]] [[ingress]]
[[deployment-strategy-vocabulary]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/mesh-data-plane-vs-control-plane.md ===
# Concept: A mesh's data plane vs its control plane vs THE cluster's control plane

Consolidated deliberately: this is the most dangerous vocabulary collision in the
chapter, and the discrimination is the content.

## ★ Fixed Point (verbatim — do not reword)

**A mesh's data plane is the set of proxies that mediate and control all network
communication between services. A mesh's control plane is what manages and configures
those proxies. Neither of them is the cluster's control plane from Chapter 3.**

[source: istio-service-mesh-2026-08-23]

## Why the collision is honest

They share a name because they genuinely do the same KIND of job at different layers.
The mesh's control plane takes policy you wrote and pushes it to the things that
enforce it: "The configuration API server distributes to the proxies: authentication
policies, authorization policies, secure naming information"
[source: istio-security-mtls-identity-2026-08-31].

The cluster's control plane takes objects you declared and drives the cluster toward
them. Same SHAPE — a central thing configuring distributed things — completely
different subject matter.

## 🪢 Mnemonic (preserve)

**The cluster's control plane manages OBJECTS. The mesh's control plane manages
PROXIES.**

When a question stem says "control plane" bare, it means the cluster's. A well-written
question that means the mesh's will say so.

## ⚠ Ledger canonical form
Sense B is always "the mesh's control plane" or "the service mesh control plane" on
first use, and the section must say in one clause that this is a different control
plane from Ch 3 §2's. Ch 17 §5 conforms — the disclaimer is inside the ★ itself.

A Ch 19 confusion-pair row is owed.

## ⚠ The distractor to recognize
"The data plane is the kube-apiserver and etcd; the control plane is the set of Envoy
proxies" (Bearings 2 Q4 option B) collapses both distinctions at once.

## Related
[[service-mesh]] [[envoy]] [[sidecar-and-ambient-modes]] [[control-plane-components]]
[[mutual-tls]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/envoy.md ===
# Concept: Envoy

"an L7 proxy and communication bus designed for large modern service oriented
architectures" [source: envoy-what-is-envoy-2026-08-31].

## Its own account of the deployment shape — worth reading twice

> Envoy is a self contained process that is designed to run alongside every application
> server. All of the Envoys form a transparent communication mesh in which each
> application sends and receives messages to and from localhost and is unaware of the
> network topology.

[source: envoy-what-is-envoy-2026-08-31]

**"Unaware of the network topology"** is "without code changes" told from the proxy's
side. The application talks to localhost; something else worries about TLS, retries,
routing and telemetry.

That works because of what Chapter 5 §2 taught: containers in a Pod share the network
namespace, so localhost reaches the container beside you.

## ⚠ Envoy is in BOTH Istio data plane modes

Sidecar mode: one Envoy per Pod. Ambient mode: ztunnel (purpose-built) at L4 per node,
and the L7 waypoint, which "is a deployment of the Envoy proxy; the same engine that
Istio uses for its sidecar data plane mode" [source: istio-ambient-mode-2026-08-31].

Ambient removes SIDECARS, not Envoy. This is the near-miss in two graded items.

## Language independence
Envoy "works with any application language" [source: envoy-what-is-envoy-2026-08-31] —
which is why Practice Q11's SDK-per-language distractor is wrong, and why the proxy
model exists at all.

## Related
[[service-mesh]] [[sidecar-and-ambient-modes]] [[mesh-data-plane-vs-control-plane]]
[[multi-container-pod]] [[pod-shared-context]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/sidecar-and-ambient-modes.md ===
# Concept: Sidecar mode and ambient mode

Consolidated deliberately: they are two ARRANGEMENTS OF ONE DATA PLANE, and teaching
them apart is what produces the misconception below.

## ⚠ NAVIGATIONAL HAZARD — "a service mesh means sidecars" is out of date

**Sidecar mode** — an Envoy proxy deployed alongside each Pod.

**Ambient mode** — "Istio implements its features using a per-node Layer 4 (L4) proxy,
and optionally a per-namespace Layer 7 (L7) proxy," and "workload pods no longer require
proxies running in sidecars in order to participate in the mesh"
[source: istio-ambient-mode-2026-08-31].

  - **ztunnel** — "a purpose-built, per-node proxy that powers Istio's ambient data
    plane mode." The L4 functions it implements are the **secure overlay**.
  - **waypoint proxy** — the optional per-namespace L7 component, and "a deployment of
    the Envoy proxy; the same engine that Istio uses for its sidecar data plane mode."

## ★ The two facts that carry the graded items

**BOTH modes use Envoy.** Ambient removes sidecars, not Envoy — it adds a purpose-built
proxy at L4 only.

**They coexist.** "Pods and workloads using sidecar mode can co-exist within the same
mesh as pods that use ambient mode" [source: istio-ambient-mode-2026-08-31].

## Why ambient exists
The sidecar model "uses more computing resources and becomes more complex to manage as
your system grows" [source: cncf-glossary-service-mesh-2026-08-31].

## ⚠ Ledger headword correction
term-ownership.md carries the headword "Ambient mesh (sidecar-less)". The draft and the
sources both say **ambient MODE**. Correct the LEDGER, not the chapter.

## Related
[[envoy]] [[service-mesh]] [[mesh-data-plane-vs-control-plane]] [[multi-container-pod]]
[[mutual-tls]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/mutual-tls.md ===
# Concept: mTLS in a service mesh

The mesh's answer to the gap Chapter 10 identified and declined to fix: TLS terminates
at the Ingress, and the leg from there to the Pod continues in the clear. NetworkPolicy
can say who may talk to whom and cannot encrypt a byte.

## Istio's three stated security goals — a direct response to that gap

"Security by default: no changes needed to application code and infrastructure; Defense
in depth: integrate with existing security systems to provide multiple layers of
defense; Zero-trust network: build security solutions on distrusted networks"
[source: istio-security-mtls-identity-2026-08-31].

## The mechanism — three named components

- a **Certificate Authority** for key and certificate management
- a **configuration API server** distributing authentication policies, authorization
  policies and secure naming information to the proxies
- **sidecar and perimeter proxies** acting as Policy Enforcement Points

[source: istio-security-mtls-identity-2026-08-31]

## The identity model — what MUTUAL means here

"The Istio identity model uses the first-class `service identity` to determine the
identity of a request's origin," flexible enough to represent "a human user, an
individual workload, or a group of workloads". Not just the client verifying the server,
but the server verifying the client's WORKLOAD IDENTITY too.

## The handshake

Outbound traffic is re-routed to the client's local sidecar Envoy → the client-side
Envoy starts a mutual TLS handshake with the server-side Envoy → they establish the
connection → the server-side Envoy authorizes the request
[source: istio-security-mtls-identity-2026-08-31].

Four steps, and the application was not consulted at any of them.

## 🔭 Permissive mode
"the server accepts both plaintext and mutual TLS traffic," existing "to provide greater
flexibility for the on-boarding process." You cannot switch a hundred services to
mandatory mTLS on a Tuesday afternoon. Know the concept exists; the configuration is
past this tier.

## ⚠ mTLS does not replace NetworkPolicy
Complementary. Istio names defense in depth among its own goals. Practice Q12 option C
is built on this error.

## Related
[[zero-trust]] [[service-mesh]] [[network-policy]] [[envoy]]
[[secret-exposure-and-hardening]] — encryption in transit is not encryption at rest.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/zero-trust.md ===
# Concept: Zero trust architecture

Core principle, four words: **never trust, always verify**
[source: cncf-glossary-zero-trust-architecture-2026-08-31].

## Why, in the glossary's own framing

"In many networks today, within the corporate network, systems and devices inside may
freely communicate with each other as they are within the trusted boundary of the
corporate network perimeter. Zero trust architecture takes the opposite approach where
although inside the network perimeter, components within the system first have to pass
verification before any communication is made."

## ★ The sentence to keep

**"Zero trust architecture however, recognises that TRUST IS A VULNERABILITY."**

[source: cncf-glossary-zero-trust-architecture-2026-08-31]

The consequence named is **lateral movement**: if an attacker takes one trusted device
inside the perimeter, they can move sideways through everything that trusts it.

## Where the reader has already met the vulnerability

Chapter 10: TLS terminates at the Ingress; traffic continues to the Pod unencrypted;
NetworkPolicy permits and denies but cannot encrypt. That unprotected leg, inside the
perimeter, between components that trust each other BECAUSE they are both inside, is
precisely what the glossary is describing.

Ch 17 Soundings Q8 pre-tests the gap, and §5 closes it. The pedagogical construction —
open the gap in the pre-test, name the principle, then supply the remedy — is worth
preserving.

## Related
[[mutual-tls]] [[network-policy]] [[service-mesh]] [[api-access-gates]]
[[pod-security-standards-and-admission]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serverless.md ===
# Concept: Serverless computing

**"Serverless Computing abstracts servers away from the user."**
[source: cncf-glossary-serverless-2026-08-31]

*Abstracts away from the user.* NOT *eliminates*. The servers are still there; somebody
is still running them; you are simply not the one thinking about them.

## Three further defining properties

- "Charges are based on a pay-per-use model."
- "Scaling and resource provisioning for computing, storage, or networking are
  automatically adjusted based on application demand without user intervention."
- "A serverless platform provider consolidates resources to serve multiple users on a
  single physical machine, ensuring isolation through virtualization."

[source: cncf-glossary-serverless-2026-08-31]

## The problem it addresses

Without it, "users commit to a predefined capacity, resulting in charges for continuous
server availability regardless of actual use," and "responsibility for adjusting server
capacity to meet fluctuating demands falls on the user, maintaining active
infrastructure even during idle periods." The answer is "activating services solely upon
demand."

## ⚠ The name actively misleads, and the book says so

"Serverless" is the worst-named idea in this book, and correcting the name is most of
what §6 does. Read "abstracts servers away from the user" alongside Knative's Pod-based
implementation and the misconception dissolves completely. Nothing disappeared.

**The serverless property is the LIFECYCLE — driven by requests, scaled to zero when
idle — not the absence of containers or servers.** See [[knative]].

## Related
[[knative]] [[scale-to-zero]] [[knative-serving-versus-eventing]] [[pod]]
[[cloud-native-definition-v1-1]] — serverless is one of the seven named technologies.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/knative.md ===
# Concept: Knative

"a Kubernetes-based platform that provides a complete set of middleware components for
building, deploying, and managing modern serverless workloads." A **CNCF Graduated**
project [source: knative-overview-2026-08-23].

## ★ Fixed Point (verbatim — do not reword)

**Serverless workloads on Kubernetes are still containers in Pods. Knative "builds on
the Kubernetes Pod abstraction," and Serving and Eventing "are implemented as Kubernetes
Custom Resource Definitions (CRDs)". The serverless property is the LIFECYCLE — driven
by requests, scaled to zero when idle — not the absence of containers or servers.**

[source: knative-overview-2026-08-23]

A container image still gets pulled; a Pod still gets scheduled onto a node; a kubelet
still starts it. What changed is that none of it happens until a request arrives, and it
all goes away again when requests stop.

## 🔭 Notice what Knative is BUILT OUT OF

Implemented as CRDs — the fourth pluggable interface, two sections earlier. A whole
serverless platform sitting on the extension mechanism, with the API server storing and
serving its objects. This is §4's pattern doing real work rather than being an example,
and it is the strongest single piece of evidence §9 has.

## ⚠ Knative does not replace or fork Kubernetes
Practice Q15 grades this. Option C ("Knative replaces the Kubernetes control plane")
reaches a right-sounding verdict for the wrong reason, which is what makes it the trap.

## ⚠ Always write "Knative Service" in full
Chapter 9 §2 owns the Kubernetes Service. A bare "Service" in a Knative context is a
sentence somebody will misread. Ledger canonical form.

## Related
[[serverless]] [[knative-serving-versus-eventing]] [[scale-to-zero]]
[[custom-resource]] [[pod]] [[pluggable-interface-pattern]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/knative-serving-versus-eventing.md ===
# Concept: Knative Serving vs Eventing (and Functions)

Consolidated deliberately: the discrimination is the graded content. A candidate who can
only say "Knative does serverless" loses the item.

## Serving — SYNCHRONOUS

"an HTTP-triggered autoscaling container runtime that manages the complete lifecycle of
stateless HTTP services, including deployment, routing, and automatic scaling (including
scale to zero)" [source: knative-overview-2026-08-23].

A request arrives, something serves it.

## Eventing — ASYNCHRONOUS

"a CloudEvents-over-HTTP asynchronous routing layer that provides infrastructure for
consuming and producing events, enabling loose coupling between event producers and
consumers" [source: knative-overview-2026-08-23].

Something happened; interested parties get told.

## Functions — built on the other two

"leverages Serving and Eventing to provide a simplified experience for building and
deploying stateless functions" [source: knative-overview-2026-08-23]. NOT a third
independent thing; it inherits the same container-and-Pod substrate.

## 🪝 One sentence each, and keep them apart

**Serving: synchronous HTTP, autoscaling, scale to zero. Eventing: asynchronous event
routing over CloudEvents.**

## ⚑ CLOUDEVENTS IS UNDEFINED IN THIS BOOK

"CloudEvents" appears in NO shipped chapter and is never defined in Ch 17. It carries
Practice Q14's CORRECT ANSWER. Recommended fix: one clause in §6 — "CloudEvents, a
vendor-neutral specification for describing event data" — plus a glossary entry and an
acronym-register row. Do NOT instead strip it from the option, because the phrase is
quoted from the Knative source and body prose would then disagree with the key.

## ⚠ The near-miss worth understanding
"Serving runs the workload; Eventing is the autoscaler" (Practice Q14 option B) splits
ONE component into two. The Knative Pod Autoscaler is part of Serving. Eventing is not
an autoscaler; it routes events.

## ⚠ "Stateless" belongs to Serving
Serving manages "the complete lifecycle of stateless HTTP services" — its own
description of its workloads. Neither component is distinguished by statefulness.

## Related
[[knative]] [[scale-to-zero]] [[serverless]] [[loose-coupling]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/scale-to-zero.md ===
# Concept: Scale to zero

Knative Serving "provides automatic scaling, or *autoscaling*, for applications to match
incoming demand," provided by default "by using the Knative Pod Autoscaler (KPA)"
[source: knative-serving-autoscaling-2026-08-31].

## The headline behavior

> If an application is receiving no traffic and scale to zero is enabled, Knative
> Serving scales the application down to zero replicas.

[source: knative-serving-autoscaling-2026-08-31]

Zero. Not one idle replica riding at anchor, burning memory in case somebody shows up.
None.

## The cycle

idle (replicas 0) → request arrives → KPA scales 0 → N → serving → traffic stops → KPA
scales N → 0.

Containers and Pods are REAL at every populated step. That visibility is the point of
the figure, and it is why "serverless" describes the lifecycle rather than an absence.

## Knative Service vs Deployment

A Deployment holds a replica count you or a controller sets (Ch 6 §1). A Knative Service
holds the same underlying idea — Pods running your container — with an autoscaler that
will take it all the way to zero and bring it back on a request. Specialist to
generalist, not a replacement.

## The bridge into §7
Knative Serving can also be configured to use the Kubernetes HorizontalPodAutoscaler
instead of the default KPA [source: knative-serving-autoscaling-2026-08-31].

## Related
[[knative]] [[knative-serving-versus-eventing]] [[serverless]]
[[horizontal-vs-vertical-autoscaling]] [[autoscaler-axis-and-trigger]] [[pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/horizontal-vs-vertical-autoscaling.md ===
# Concept: Horizontal vs vertical scaling

## ★ Fixed Point (verbatim — do not reword)

**Horizontal scaling changes the NUMBER of replicas. Vertical scaling changes the
RESOURCES available to each replica.**

"Horizontal scaling means that the response to increased load is to deploy more Pods.
This is different from *vertical* scaling, which for Kubernetes would mean assigning
more resources (for example: memory or CPU) to the Pods that are already running for
the workload" [source: k8s-docs-hpa-2026-08-24].

More of them, or bigger ones. And a third axis that is not about Pods at all: node
autoscaling adds or removes the machines underneath.

## ⚠ The most common error in this material

Swapping the two. Practice Q18 option B does exactly this and compounds it by misfiling
KEDA. If you can state which word attaches to WHICH NOUN — number vs resources — the
rest of §7 reconstructs itself.

## Two HPA details worth carrying

- It runs "as a control loop that runs intermittently (it is not a continuous process)"
  — so a change in load does not produce an instant change in replicas.
- It "does not apply to objects that can't be scaled (for example: a DaemonSet)" —
  which makes sense, because a DaemonSet's replica count is a function of node count.

[source: k8s-docs-hpa-2026-08-24]

## Utilization is relative to REQUESTS
An HPA reasons about utilization relative to what a Pod REQUESTED, which is why Ch 5's
requests-and-limits material is load-bearing here rather than merely adjacent. Ch 18 §3
examines it properly.

## Related
[[autoscaler-axis-and-trigger]] [[vertical-pod-autoscaler]] [[node-autoscaling]]
[[keda-event-driven-autoscaling]] [[resource-request]] [[resource-metrics-pipeline]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/vertical-pod-autoscaler.md ===
# Concept: VerticalPodAutoscaler (VPA)

Adjusts the RESOURCES available to each replica, based on observed usage.

## ⚠ NAVIGATIONAL HAZARD — the VPA is an ADD-ON. It is not there unless installed.

The documentation says it twice, on two pages. The autoscaling concepts page: unlike the
HPA, the VPA "doesn't come with Kubernetes by default," and is an add-on you or a
cluster administrator may need to deploy. The VPA's own page: "Unlike
HorizontalPodAutoscaler, which is part of the core Kubernetes API, VPA must be installed
separately in your cluster" [source: k8s-docs-autoscaling-and-vpa-2026-08-31].

It also needs metrics-server to work at all.

## This is the absent-component pattern, one layer over

An Ingress with no Ingress controller is a document nobody reads. A `kubectl top` with
no metrics-server is a command with nothing to query. A VPA object on a cluster with no
VPA installed is the same failure. See [[absent-component-pattern]].

⚠ NOTE FOR THE WORDING SWEEP: Ch 17 §7 quotes the pattern as "the object exists;
nothing happens without the component" and credits Ch 10 §3 with coining it. Three
phrasings are live across five chapters, and Ch 3 owns the phrase. Do not repair Ch 17
alone — see [[absent-component-pattern]].

## Three cooperating pieces
A **recommender** that analyzes usage, an **updater** that acts on recommendations, and
an **admission controller webhook** that applies them to new or recreated Pods
[source: k8s-docs-autoscaling-and-vpa-2026-08-31].

Worth noticing: the VPA reaches the cluster through the admission webhook extension
point from §4.

## Related
[[absent-component-pattern]] [[horizontal-vs-vertical-autoscaling]]
[[in-place-pod-vertical-resize]] [[resource-metrics-pipeline]] [[admission-control]]
[[autoscaler-axis-and-trigger]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-autoscaling.md ===
# Concept: Node autoscaling — Cluster Autoscaler and Karpenter

Consolidated deliberately: the sources say the two give a similar experience, and
teaching them apart invites a distinction the documentation does not draw.

> Automatically provision and consolidate the Nodes in your cluster to adapt to demand
> and optimize cost.

[source: k8s-docs-node-autoscaling-2026-08-31]

## The trigger — the second half of a sentence Chapter 7 left hanging

"If there are Pods in a cluster that can't be scheduled on existing Nodes, new Nodes can
be automatically added to the cluster — *provisioned* — to accommodate the Pods."

Chapter 7 §2 said an unschedulable Pod's continued existence is "a standing,
machine-readable statement that the cluster is short of somewhere to put work. Something
could be watching for exactly that." This is the something.

## Consolidation — the half nobody puts on the brochure

"Nodes in your cluster can be automatically *consolidated* in order to improve the
overall Node utilization, and in turn the cost-effectiveness of the cluster.
Consolidation happens through removing a set of underutilized Nodes from the cluster."

The fleet gets smaller when the work does.

## Not purely Kubernetes-internal
Node autoscalers "need to interact with cloud provider APIs to provision and consolidate
Nodes" — because buying a machine is not a Kubernetes operation.

## The two implementations
Both are "sponsored by SIG Autoscaling," and "from the perspective of a cluster user,
both autoscalers should provide a similar Node autoscaling experience." Cluster
Autoscaler works against pre-configured **node groups**; Karpenter is "an open-source
node lifecycle management project built for Kubernetes" that adds nodes for
unschedulable pods, schedules pods on them, and removes them when not needed
[source: karpenter-concepts-2026-08-31].

## ⚓ Karpenter has NO CNCF maturity level

Sponsored by Kubernetes SIG Autoscaling; no official source assigns it a level.
Contrast Knative, whose own documentation states it is CNCF Graduated, and KEDA, which
kubernetes.io describes the same way. If an answer option gives Karpenter a maturity
level, besuspicious of it — and notice that §2 taught you why that distinction is meaningful.

## Related
[[pending-pod]] [[feasible-node]] [[autoscaler-axis-and-trigger]]
[[horizontal-vs-vertical-autoscaling]] [[cncf-project-maturity-levels]]
[[kubernetes-sig-wg-committee]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/keda-event-driven-autoscaling.md ===
# Concept: KEDA

"a CNCF-graduated project enabling you to scale your workloads based on the number of
events to be processed, for example the amount of messages in a queue. There exists a
wide range of adapters for different event sources to choose from"
[source: k8s-docs-autoscaling-and-vpa-2026-08-31].

## Also schedule-based

Through its `Cron` scaler, which "allows you to define schedules (and time zones) for
scaling your workloads in or out" — for reducing consumption during off-peak hours
[source: k8s-docs-autoscaling-and-vpa-2026-08-31].

Both requirements, one tool. That pairing is what Bearings 3 Q1 tests.

## ⚠ KEDA shares the HPA's AXIS with a different TRIGGER

KEDA moves the REPLICA COUNT, same as the HPA. That is not a flaw in the taxonomy — it
is the most useful thing in §7, because it forces the reader to separate two questions
that look like one. See [[autoscaler-axis-and-trigger]].

## ⚠ Two errors to recognize
- "KEDA is a CPU autoscaler." It is event-driven plus schedule-based.
- Filing KEDA with the node autoscalers because it is "the external one" (Practice Q18
  option C). KEDA scales WORKLOADS, not machines.

## ⚠ And the near-miss on the other side
Getting queue depth in front of an HPA is possible through custom-metrics plumbing, but
it is not native, and it does not address scheduling at all.

## Maturity level, sourced
kubernetes.io calls KEDA CNCF-graduated. Contrast Karpenter, which no official source
assigns a level. Ch 17 uses this contrast deliberately to make §2's ladder do work.

## Related
[[autoscaler-axis-and-trigger]] [[horizontal-vs-vertical-autoscaling]]
[[node-autoscaling]] [[cncf-project-maturity-levels]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/autoscaler-axis-and-trigger.md ===
# Concept: The autoscaler landscape — four autoscalers, three axes

The section's synthesis. Four autoscalers do not produce four axes, and the overlap is
the lesson rather than a flaw.

| Autoscaler | What moves | What triggers it |
|---|---|---|
| **HPA** (ships with Kubernetes) | replica count | observed utilization |
| **KEDA** | replica count — SAME AXIS as HPA | external event (queue depth; schedule via Cron) |
| **VPA** — ⚠ ADD-ON, NOT SHIPPED | per-replica resources (CPU, memory) | observed usage (needs metrics-server) |
| **Cluster Autoscaler / Karpenter** | the NODE POOL | unschedulable Pods (provision); underutilized nodes (consolidate) |

[source: k8s-docs-autoscaling-and-vpa-2026-08-31] [source: k8s-docs-node-autoscaling-2026-08-31] [source: k8s-docs-hpa-2026-08-24]

## 🪢 Mnemonic (preserve — it is the section's method)

**Ask two questions of every autoscaler, never one: WHAT MOVES? WHAT TRIGGERS IT?**

HPA and KEDA give the same answer to the first and different answers to the second.
Cluster Autoscaler and Karpenter give the same answer to both. Once you separate the two
questions, the taxonomy stops being four things to memorize and becomes a small grid you
can reconstruct.

This is the highest-value construction in §7. It converts recall into derivation, the
same move §8 makes with the release cadence.

## The two cells carrying most of the exam value
VPA's add-on status, and KEDA's axis overlap with the HPA.

## Named, not taught
The **Cluster Proportional Autoscaler**, which scales replica counts on schedulable node
and core count (classic use: cluster DNS), and its vertical counterpart
[source: k8s-docs-autoscaling-2026-08-23]. Explicitly ungraded.

## Related
[[horizontal-vs-vertical-autoscaling]] [[vertical-pod-autoscaler]] [[node-autoscaling]]
[[keda-event-driven-autoscaling]] [[scale-to-zero]] [[resource-metrics-pipeline]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/in-place-pod-vertical-resize.md ===
# Concept: In-place Pod vertical resize — ⚑ A LIVE SOURCE CONFLICT

Changing a running Pod's CPU and memory requests and limits without recreating it. Went
**stable in Kubernetes v1.35**, "more than 6 years after its initial conception," having
been alpha in v1.27 and beta in v1.33
[source: k8s-docs-autoscaling-and-vpa-2026-08-31].

## ⚑⚑ THREE OFFICIAL SOURCES DISAGREE. DO NOT "RESOLVE" THIS.

The question is whether the VPA can use it.

- The **autoscaling concepts page** states flatly: "As of Kubernetes 1.37, VPA does not
  support resizing pods in-place, but this integration is being worked on."
- The **VPA's own documentation page** lists `InPlaceOrRecreate` and `InPlace` among its
  update modes.
- The **v1.35 release blog** says VPA's "`InPlaceOrRecreate` update mode, which leverages
  this feature, has graduated to beta."

All three [source: k8s-docs-autoscaling-and-vpa-2026-08-31].

Chapter 17 writes TO the conflict rather than through it, which is correct and is
recorded here so a later stage does not tidy it into a false certainty.

## 🪝 The safe statement the book stands behind

**In-place Pod vertical resize is a stable Kubernetes feature, and full VPA support for
it is not a settled story.**

Do not write or believe "VPA now resizes in place" as an unqualified claim.

## What an exam item would actually hinge on
The durable half: that horizontal and vertical are different axes, and that VPA is an
add-on. Chapter 17 grades neither side of the conflict, deliberately.

## Related
[[vertical-pod-autoscaler]] [[horizontal-vs-vertical-autoscaling]]
[[autoscaler-axis-and-trigger]] [[version-skew]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubernetes-sig-wg-committee.md ===
# Concept: SIGs, Working Groups, and Committees

Absorbs `steering-committee` and `subproject`. Consolidated deliberately: the
three-way discrimination is the graded content.

## ★ Fixed Point (verbatim — do not reword)

- **A SIG (Special Interest Group)** is the primary, **durable**, topic-focused unit.
  Members from multiple companies, common purpose of advancing the project on a
  specific topic.
- **A Working Group** is **time-bounded** and **crosses SIG lines**. Formed for a topic
  in scope for Kubernetes that spans multiple SIGs.
- **A Committee** does **not have open membership** and does not always operate in the
  open.

[source: k8s-community-governance-2026-08-23] [source: k8s-sig-list-and-groups-2026-08-31]

## SIG orientations, with the project's own examples
**Vertical** (Network, Storage, Node) · **horizontal** (Scalability, Architecture) ·
**project-support** (Testing, Release, Docs). Each SIG "must have at least one and
ideally two SIG chairs at any given time," who are "organizers and facilitators."

**Subprojects** divide work within a SIG, "each with designated owners who serve as
technical leaders for their respective areas." SIG Release's Release Engineering
subproject is the worked example.

## ⚠ Committees are the one group that is NOT open — and that asymmetry is the item

"Committees do not have open membership and do not always operate in the open. They are
formed by the steering committee for specific topics requiring discretion (for example
Security, Code of Conduct), have charters and chairs, and report periodically to the
steering committee" [source: k8s-community-governance-2026-08-23].

There are exactly **three**: **Code of Conduct**, **Security Response**, **Steering**
[source: k8s-sig-list-and-groups-2026-08-31]. Steering is one of them and charters the
other two.

A project whose stated principle is "transparent and accessible" has three closed
bodies, and the reason is not hypocrisy — you cannot handle an unreported vulnerability
or a conduct complaint in a public meeting. The exception is deliberate and chartered.

## The four community principles
**Open** · **Welcoming and respectful** · **Transparent and accessible** · **Merit**
[source: k8s-community-governance-2026-08-23]. Hold the third one; the Committee
exemption is measured against it.

## ⚠ SIGs are NOT CNCF TAGs
Different organizations, different scopes. The confusion has a real historical root —
CNCF's groups were originally called SIGs before being renamed. See [[cncf-tags]].

## SIGs the reader has already met the work of
SIG Network (Ch 9–10) · SIG Storage (Ch 11) · SIG Node (Ch 2, Ch 5) · SIG Release
(Ch 8) · SIG Autoscaling (Ch 17 §7, which sponsors both node autoscalers)
[source: k8s-sig-list-and-groups-2026-08-31].

## ⚠ Pre-existing acronym debt, not Ch 17's
"SIG" is first used in the book at ch08:861 ("a SIG Release team") UNEXPANDED. Ch 17
correctly expands it at its own first use. Fix Ch 8 in the sweep.

## Related
[[cncf-governance-bodies]] [[cncf-tags]] [[contributor-ladder]]
[[sig-release-and-release-cadence]] [[kubernetes-enhancement-proposal]]
[[code-of-conduct]] [[node-autoscaling]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/contributor-ladder.md ===
# Concept: The Kubernetes contributor ladder

Four rungs [source: k8s-community-membership-ladder-2026-08-23]:

| Role | Responsibility | What it requires |
|---|---|---|
| **Member** | Active contributor in the community | Sponsored by 2 reviewers; multiple contributions |
| **Reviewer** | Review contributions from other members | History of review and authorship in a subproject |
| **Approver** | Approve acceptance of contributions | Highly experienced active reviewer and contributor |
| **Subproject Owner** | Set direction and priorities for a subproject | Demonstrated responsibility and excellent technical judgement |

## Member requirements in full

Two-factor authentication enabled on your GitHub account; multiple contributions "enough
to demonstrate an ongoing and long-term commitment to the project"; subscribed to the
dev mailing list; read the contributor guide; **sponsored by 2 reviewers from different
companies**; and open a membership request issue.

Reviewer: member for ≥3 months, primary reviewer on ≥5 PRs, reviewed or merged ≥20
substantial PRs. Approver: 3 months as reviewer, primary reviewer on ≥10 substantial
PRs, 30 reviewed or merged, nomination by a subproject owner.

## ★ What is NOT on the list

No employer requirement. No seniority requirement. No credential. The gate is
CONTRIBUTIONS and TWO PEOPLE WILLING TO VOUCH FOR YOU — and the sponsors must be from
DIFFERENT COMPANIES, a deliberate structural check against any one employer
manufacturing members.

Practice Q20 turns on exactly that constraint: two sponsors from the candidate's own
employer satisfies the count and fails the check.

## The invitation is real, and the first rung is lower than it looks
SIG Docs exists. So does SIG Contributor Experience. Documentation fixes, a test for an
uncovered code path, reproducing a bug report a maintainer cannot reproduce — all are
ordinary first contributions.

⚠ SOURCING NOTE: an earlier draft claimed every SIG holds a public meeting on a public
calendar. Neither cached snapshot supports it — the roster snapshot lacks the
meeting-schedule columns the upstream sig-list.md carries. Softened to the sourced
transparency principle. To restore the stronger invitation, re-fetch sig-list.md
capturing per-SIG meeting schedules.

## Related
[[kubernetes-sig-wg-committee]] [[kubernetes-enhancement-proposal]]
[[cncf-community-onramps]] [[code-of-conduct]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubernetes-enhancement-proposal.md ===
# Concept: KEP — Kubernetes Enhancement Proposal

"a way to propose, communicate and coordinate on new efforts for the Kubernetes
project," using "a standard proposal format with useful metadata"
[source: k8s-keps-and-feature-stages-2026-08-23].

Required for potentially controversial changes, most new features, major modifications
to existing features, and changes affecting most of the project. The framework was
"inspired by similar processes such as IETF RFCs and Python PEPs," and provides
"exposure through searchable websites, cross-referencing, and structured decision-making
with a discoverable record."

## The feature stages

**alpha → beta → stable (GA)**, with graduation criteria stated in the KEP itself.

The reader has already seen this machinery from the outside: every "Feature state:
Stable since Kubernetes v1.35" banner in the documentation is the visible end of a KEP
that ran its course. In-place vertical resize is the worked example — alpha v1.27, beta
v1.33, stable v1.35.

## ⚓ The discoverable record is the real product

When you find yourself asking "why on earth does Kubernetes do it THIS way," there is
very often a KEP with the argument written down, including the alternatives that were
rejected and why. An unusually good property for a system you have to reason about under
exam conditions, and for one you have to operate.

## Why it matters to §9's argument
Every hypothetical feature Kubernetes did NOT implement — a storage driver per vendor, a
network implementation per fabric — would have been a KEP, argued in a SIG, competing
for review time. The interface is how a project this size stays a project rather than
becoming a marketplace of forks.

## Related
[[kubernetes-sig-wg-committee]] [[sig-release-and-release-cadence]] [[version-skew]]
[[in-place-pod-vertical-resize]] [[one-pluggability-story]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/sig-release-and-release-cadence.md ===
# Concept: SIG Release and the release cycle

## ★ Fixed Point (verbatim — do not reword)

**Three minor releases a year, three supported minor versions, and roughly one year of
patch support are not three facts. They are one fact stated three ways. Three releases
per year × three maintained branches ≈ one year — and because the documentation states
that year independently, you can DERIVE the support window instead of memorizing it.**

Sourced: releases happen "approximately three times per year"; the project "maintains
release branches for the most recent three minor releases"; "Kubernetes 1.19 and newer
receive approximately 1 year of patch support"
[source: k8s-release-cycle-and-cadence-2026-08-31].

## SIG Release

Charter lists "Production of Kubernetes releases on a reliable schedule" first, along
with defining and staffing release roles, driving the development and release processes,
and "managing the creation of release specific artifacts, including: Code branches,
Binary artifacts, Container Images, Release notes"
[source: k8s-release-cycle-and-cadence-2026-08-31].

## The cycle — three phases

**Enhancement Definition → Implementation → Stabilization**, with an **Enhancements
Freeze** around week 4, **Code Freeze** from around week 12 running about two weeks,
during which "only critical bug fixes are accepted into the release codebase," and a
post-release phase from week 14.

## ⚑ CHAPTER 8'S "FIFTEEN WEEKS" PROMISE IS UNPAID

ch08:1009 commits: this is "where SIG Release and the KEP process explain WHERE THOSE
FIFTEEN WEEKS GO." The word "fifteen" appears nowhere in Chapter 17.

Ch 17's AUTHOR-REVIEW declined the 15-week figure on purpose — an older snapshot says
"approximately every 15 weeks," the current page says "approximately three times per
year" — without knowing Ch 8 shipped the promise twice.

The phase list above IS the accounting. Fix: one clause after it —

    That is where the fifteen weeks Chapter 8 gave you actually go.

Both halves stay true. See [[release-cadence]].

## ⚠ Do not "correct" toward 15 weeks
The three-times-a-year formulation is current, sourced, and the half the exam would
test. The clause above closes the loop without asserting the disputed phrasing.

## Related
[[release-cadence]] [[version-skew]] [[kubernetes-enhancement-proposal]]
[[kubernetes-sig-wg-committee]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-community-onramps.md ===
# Concept: CNCF community on-ramps

Absorbs `kubecon-cloudnativecon`. These are the CNCF-side entry points, DISTINCT from
the Kubernetes contributor ladder.

## Mentoring programs

- **LFX Mentorship** — "a mentoring initiative by the Linux Foundation"
- **Google Summer of Code** — "a mentoring program for the open source beginners"
- **Outreachy** — "a mentoring initiative for the communities traditionally
  underrepresented in tech"

[source: cncf-mentoring-and-community-groups-2026-08-31]

## Cloud Native Community Groups (CNCGs)

The foundation "supports the worldwide community of the Cloud Native Community Groups"
[source: cncf-mentoring-and-community-groups-2026-08-31] — "free, volunteer-run meetups
on the CNCF community platform, including Kubernetes Community Days"
[source: cncf-landscape-and-community-2026-08-23].

## CNCF Ambassadors

An extension of the CNCF, furthering the mission of making cloud native ubiquitous
through community leadership and mentorship; many organize those local groups
[source: cncf-landscape-and-community-2026-08-23].

## KubeCon + CloudNativeCon

The flagship conference series where the whole community convenes
[source: cncf-landscape-and-community-2026-08-23].

## ⚠ Two ladders, two organizations
The contributor ladder (Member → Reviewer → Approver → Subproject Owner) is
KUBERNETES-internal. These on-ramps are CNCF-wide. Same distinction as SIGs vs TAGs, one
layer over.

## Related
[[contributor-ladder]] [[cncf-governance-bodies]] [[code-of-conduct]] [[cncf-tags]]
[[cncf-mission-and-vendor-neutrality]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/code-of-conduct.md ===
# Concept: The CNCF Community Code of Conduct

Applies across all CNCF projects and events. The **scope statement is the examinable
part**, because it is broader than people assume:

> This code of conduct applies: within project and community spaces, in other spaces
> when an individual CNCF community participant's words or actions are directed at or
> are about a CNCF project, the CNCF community, or another CNCF community participant in
> the context of a CNCF activity.

[source: cncf-code-of-conduct-2026-08-31]

Project spaces, event spaces, **and** conduct outside both when it is directed at the
community.

## The pledge
Commits to "making participation in the CNCF community a harassment-free experience for
everyone," across a long enumerated list of dimensions of diversity
[source: cncf-code-of-conduct-2026-08-31].

## Administration
The **CNCF Code of Conduct Committee**, reachable at a published address for incidents
that are project-agnostic or span multiple projects, with a stated expectation of "a
response within three business days".

## ⚠ Two Code of Conduct bodies — keep them apart
- The **CNCF** Code of Conduct Committee (foundation-wide, above).
- The **Kubernetes** Code of Conduct Committee — one of the project's three Committees,
  chartered by Steering, with closed membership. See [[kubernetes-sig-wg-committee]].

Ch 17 introduces both, in §8, a few paragraphs apart. Worth a Ch 19 confusion-pair row.

## Related
[[kubernetes-sig-wg-committee]] [[cncf-community-onramps]] [[cncf-governance-bodies]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-certification-ladder.md ===
# Concept: The CNCF certification ladder

Chapter 1 deferred this to Chapter 17 §8 by name.

KCNA "is a pre-professional certification designed for candidates interested in
advancing to the professional level," and "lays the groundwork for further CNCF
certifications like CKA, CKAD, and CKS"
[source: cncf-kcna-certification-page-2026-08-23].

## ★ The FORMAT is what changes, not just the difficulty

| Credential | Format |
|---|---|
| **KCNA** | "online and multiple-choice" |
| **CKA** | "a performance-based exam where candidates interact with the command line to solve real-world challenges" |
| **CKAD** | "a hands-on, command-line environment" |
| **CKS** | "performance-based" |

[source: cncf-kcna-certification-page-2026-08-23]

CNCF also offers **KCSA** and the Cloud Native Network Function certification
[source: cncf-who-we-are-2026-08-23].

## 🪢 Mnemonic (preserve)

**KCNA is the only one on this ladder — CKA, CKAD, CKS — you can pass by KNOWING
things.** Everything above requires DOING things, at a terminal, against a live cluster,
under time pressure. Not a reason to underrate this exam — the reason the vocabulary
has to be solid before going on, because at the next tier nobody gives you four options
to pick from.

## ⚠ ACRONYM DEBTS — all three are Ch 17 §8's to discharge

- **CKA** — expanded once, at ch01:180 ("the Certified Kubernetes Administrator").
- **CKAD / CKS** — expanded NOWHERE in Chapters 1–17. B7 :661–662 assigns both here.
  Add "Certified Kubernetes Application Developer" and "Certified Kubernetes Security
  Specialist" at first use.
- **KCSA** — "Kubernetes and Cloud Native Security Associate" is standard and almost
  certainly correct but is NOT in the cached corpus. Tag to the CNCF certification
  overview page on the next research pass, or drop the expansion.

No snapshot states KCSA's exam format, which is why the mnemonic scopes its claim to
CKA/CKAD/CKS. Do not extend it.

## Related
[[kcna-exam-format]] [[domain-weights-44-28-16-12]] [[cncf-mission-and-vendor-neutrality]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/one-pluggability-story.md ===
# Concept: One pluggability story — Chapter 17's Zenith

The chapter's synthesis section (§9). It teaches nothing new; it names what four
chapters were evidence of.

## The claim

**Kubernetes is not a system that happens to be extensible in four places. It is a
system built on the premise that IT SHOULD NOT BE THE ONE IMPLEMENTING THE PARTS THAT
VARY.**

Kubernetes defines WHAT MUST BE TRUE; somebody else SUPPLIES THE THING. Four instances
— CRI (Ch 2 §4), CNI (Ch 9 §1), CSI (Ch 11 §5), CRDs (Ch 6 §8) — not four decisions.
One decision, made four times because it was right four times.

## The counterfactual, which is what makes it an argument

Kubernetes ships a container runtime → every hardening requirement, compliance regime
and sandboxed-isolation need becomes a feature request against the Kubernetes codebase.
Ships a network implementation → every network fabric on earth becomes a patch somebody
must get merged. Ships storage drivers → the project maintains code for every array,
appliance and cloud volume service in existence. Ships a fixed set of object kinds →
the only way to model your database is to convince the API reviewers your database
belongs in Kubernetes.

None of that scales. **Not technically, and not organizationally** — which §8 made
concrete, because the reader now knows how a change becomes a change here. Every one of
those features would be a KEP, argued in a SIG, competing for review time.

**The interface is how a project of this size stays a project rather than becoming a
marketplace of forks.**

## The second-order effect — the part that took four chapters to earn

Because the parts that vary sit behind interfaces, they can vary **without permission**.
A storage vendor writes a CSI driver on their own schedule. A network project ships a
CNI plugin without asking. You define a CRD on a Tuesday afternoon and your cluster
gains a kind of object upstream Kubernetes has never heard of and never needs to.

## Why it lands as recognition
Chapter 2 §8 promised this would "feel like recognition rather than a fourth list." It
does, because the reader was not learning four things — they were learning one thing,
four times, in the four places it showed up.

## The caption's discipline, worth preserving
"altitude, to a navigator, is not a metaphor for importance. It is the angle you take on
a fixed body to learn where you actually are." The brand register used precisely enough
to reject its own loose reading.

## ⚠ Anchor form
`ch17-zenith-one-pluggability-story` has no `figMM` segment and is VALID —
structural-contract.yaml's `anchor_id_pattern` is
`^ch\d{2}-(fig\d{2}|zenith)-[a-z0-9-]+$`, which sanctions the zenith form explicitly.
No change needed.

## ⚠ NO CONTROL-LOOP ORDINAL
This Zenith is about the interface pattern, not the control loop. Ch 15 §7 holds the
book's reserved "third time." Verified: Ch 17 adds no count. See [[control-loop]].

## Related
[[pluggable-interface-pattern]] [[cri]] [[cni]] [[csi]] [[custom-resource]]
[[kubernetes-extension-points]] [[kubernetes-enhancement-proposal]]
[[kubernetes-sig-wg-committee]] [[knative]]
=== END WRITE ===
```

---

That completes the manifest: 3 register appends, 20 shard appends, and 39 new shards.

**Two things worth your attention before Chapter 18 drafts.**

The first is a straight win. `sources/cncf-kcna-curriculum-pdf-2026-08-23.md` — cited by every shipped chapter — publishes Domain 4's three competencies verbatim, which is exactly what the draft's chapter-wide AUTHOR-REVIEW says no cached snapshot supports. Tagging it retires the note, fixes one competency name ("Observability," not "Cloud Native Observability"), and lets §8's authored 7/5 split rest on a boundary CNCF itself draws rather than one the book invented.

The second is a correction to the prior stage. The integration report's ship-blocker rests on the claim that Chapter 13 never retrieves the absent-component pattern. It does — three times, in the same words Chapter 17 uses, which are also the words the binding B7 ledger specifies. There are three phrasings live across five chapters and both binding artifacts, so this is a book-wide sweep rather than a Chapter 17 repair. What does still need fixing in Chapter 17 is the attribution clause, which is one line.

I could not write to `Book-KCNA/` (permission denied, consistent with every prior stage — the knowledge-base directory has never been created). The blocks above are ready for the orchestrator to parse, or grant write access and I'll place them.
Write isn't permitted here — which matches the pipeline convention (`Write` is deliberately removed from `--allowed-tools` so stage output flows through stdout for the orchestrator to capture atomically). Emitting the audit below.

---

# Curriculum-Alignment Audit — KCNA Chapter 6

**Chapter:** 6 — *Fleets, Not Vessels*
**Audited artifact:** `.pipeline-state/ch-06/draft-v1-prevoice.md` (1,213 lines / 17,859 words)
**Authority:** `cncf-kcna-curriculum-pdf-2026-08-23.md`, corroborated by `lf-kcna-exam-page-2026-08-23.md` and `lf-kcna-program-changes-2026-08-23.md`
**Verdict:** Objective coverage is **complete and correctly scoped.** Four metadata over-claims, one depth overrun, two precision defects. No under-coverage.

---

## ⚠ BLOCKING — read before acting on anything below

**The voiced draft on disk is truncated to ~21% of the chapter.**

This stage was invoked with `draft-voice.md` reported as "file not available." On disk:

| File | Size | Lines | Content |
|---|---|---|---|
| `draft-v1-prevoice.md` | 119 KB | 1,213 | Complete chapter, `# Chapter 6` → 🏆 Safe Harbor |
| `draft-v1.md` (current draft) | 24 KB | 253 | **Starts mid-word** — `ognition exam can ask about…`, inside Exam Alert priority #1 |

`draft-v1.md` retains only Exam Alert (partial) → Practice Questions → Answers → Chapter Summary → Voyage Ahead → Safe Harbor. **Sections §1–§9, Soundings, Attention Budget, Why This Chapter Matters, What You'll Learn, and all three Taking Your Bearings checkpoints are gone,** along with all six FIGURE anchors and both AUTHOR-REVIEW comments.

The voice-swap stage renamed its input to `draft-v1-prevoice.md` and wrote a truncated output to `draft-v1.md`. Nothing was lost — the full chapter is intact in the prevoice file — but every downstream stage (fact-accuracy, question-quality, theming-density, structural, revision) will audit a chapter that is 79% missing, and `structural_lint.py` will fire on absent required elements rather than on anything real.

**This audit therefore ran against `draft-v1-prevoice.md`.** That is the methodologically correct target regardless: voice-swap alters register, not objective coverage, so a curriculum-alignment verdict taken on the prevoice draft holds for the voiced draft once regenerated.

**Fix before any other revision work:** re-run the voice stage for ch-06 and verify the output is ~1,200 lines and begins with `# Chapter 6: Fleets, Not Vessels`. Do not hand-patch `draft-v1.md`.

---

## Objectives the outline claims to cover

The outline tags every one of its nine sections `objectives: ["D1.1"]` and claims no other objective. Under this book's scheme, **D1.1 = Kubernetes Fundamentals › Kubernetes Core Concepts**.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.1 | Kubernetes Fundamentals › Kubernetes Core Concepts (workload resources) | **YES** | appropriate |

That single row is the entire published-granularity claim, and it is satisfied. **CNCF publishes four domain weights and twelve named competencies with no sub-objective IDs and no sub-weights** [`cncf-kcna-curriculum-pdf-2026-08-23`, `lf-kcna-program-changes-2026-08-23`]. There is no authoritative objective finer than "Kubernetes Core Concepts" to audit against, so a one-row table is the honest published-level result — and the draft's own framing is correct (line 104 states the 6% as an authored allocation and cites the curriculum PDF).

The auditable claim at working granularity is the outline's `kb_tags` block — 52 concepts and 10 commands. That is the finest-grained coverage commitment the pipeline actually makes, so it is where the rest of this audit operates.

### Concept tags — 50 of 52 delivered

| Cluster | Concept tags claimed | Covered? | Depth | Where |
|---|---|---|---|---|
| Ownership | `workload-resource` `deployment` `replicaset` `pod-template` `podtemplatespec` `ownership-chain` `replicationcontroller-legacy` | YES (7/7) | appropriate | §1 |
| Control loop | `replicas` `desired-replica-count` `manual-horizontal-scaling` `horizontal-scaling` `horizontalpodautoscaler` | YES (5/5) | appropriate | §2 |
| — | `vertical-scaling` | **NO** | — | deliberately deferred to Ch 17 |
| Selectors | `label-selector` `matchlabels` `matchexpressions` `selector-template-agreement` `overlapping-selectors` | YES (5/5) | appropriate | §3 |
| Ownership mechanics | `owner-reference` `controller-adoption` `cascading-deletion` | YES (3/3) | appropriate | §3 |
| — | `orphaning` | **NO** | — | deliberately excluded by §3's own scope guard |
| Update mechanics | `deployment-strategy` `rolling-update` `recreate-strategy` `maxsurge` `maxunavailable` `minreadyseconds` `readiness-gated-rollout` | YES (7/7) | deep — correct | §4 |
| Revisions | `rollout` `revision` `rollout-history` `rollback` `revision-history-limit` `pause-rollout` `resume-rollout` `stuck-rollout` | YES (8/8) | appropriate | §5 |
| Identity | `statefulset` `stable-pod-identity` `pod-interchangeability` | YES (3/3) | **over-covered** | §6 |
| Siblings | `daemonset` `node-local-facility` `job` `run-to-completion` `cronjob` `cronjob-schedule` | YES (6/6) | appropriate | §7 |
| Extension | `custom-resource` `customresourcedefinition` `custom-controller` `operator-pattern` `declarative-api` `dynamic-registration` | YES (6/6) | appropriate | §8 |

### Command tags — 8 of 10 delivered

`kubectl-get` `kubectl-scale` `kubectl-delete` `kubectl-rollout-status` `kubectl-rollout-history` `kubectl-rollout-undo` `kubectl-rollout-pause` `kubectl-rollout-resume` — all present.

`kubectl-apply` and `kubectl-describe` — **absent from the draft entirely** (verified by search; zero occurrences).

### Reading of the four misses

All four are **metadata over-claims, not drafting failures.** In every case the outline's own section-level prose instructs the draft to omit the concept:

- `vertical-scaling` — Open question #4: *"one clause in §2 naming horizontal scaling… and no mention of vertical scaling at all."* Draft complies exactly.
- `orphaning` — §3 scope guard: *"Do not teach garbage-collection internals, finalizers, or foreground-versus-background deletion"*; Open question #3 rules `--cascade=orphan` out on Chapter 8 grounds. Draft complies.
- `kubectl-describe` — Bearings #2 answer-key requirement: *"item 4's key must stop short of diagnosis… `kubectl describe` and the event stream are Chapter 13's."* Draft complies.
- `kubectl-apply` — never assigned to a section; the chapter is deliberately not a command-surface chapter (Ch 8 owns that).

The defect is that `kb_tags` promises four things the outline body forbids. This matters beyond bookkeeping: `kb_tags` feeds `kcna-domain-index.md`, so the index will assert Chapter 6 as the coverage site for vertical scaling and `kubectl describe` — and Chapters 13 and 17, which actually teach them, will look like duplicates to `reconcile.py`.

---

## Objectives covered in the draft but NOT in the outline

Genuine scope expansion, ranked. None is fabricated — every item below is sourced — so the question for the author is scope, not accuracy.

**1. StatefulSet storage and networking machinery (§6) — the material expansion.** `MEDIUM`

The outline's Open question #5 set an explicit ceiling: *"Ordinal naming and ordered creation/termination are conditional on the source fetch and, if included, should be one sentence."* The draft delivers considerably more:

- a three-bullet identity breakdown — ordinal index, stable network ID, stable storage (lines 620–624)
- `volumeClaimTemplate` named, with the one-PVC-per-Pod binding rule (line 624)
- a full paragraph on ordered creation 0→N-1, reverse-order termination, and the predecessors-must-be-Ready rule (line 652)
- a paragraph carrying two StatefulSet *limitations* verbatim: storage must be provisioner- or admin-provisioned, and scale-down does not delete volumes (line 674)
- the Headless Service requirement, stated as a requirement (line 676)

`volumeClaimTemplate`, storage classes, provisioners and volume-retention-on-delete are **D2.4 Storage**. Headless Services are **D2.1 Networking**. Both are Chapter 11's and Chapter 9's by B2's split, and the outline's §6 guard is blunt: *"Do not teach PersistentVolume, PersistentVolumeClaim, StorageClass, access modes, or provisioning."*

In the draft's defence, all of it is forward-pointed and §6 carries an explicit "the loop this section is deliberately leaving open" subsection that does exactly what the outline asked for. This is a well-executed overrun, not an accident. But it is an overrun: the draft states substantive Chapter 11 facts rather than deferring them, which is the specific failure mode the B2 split was designed to prevent.

**2. DaemonSet scheduling surface (§7).** `LOW — sanctioned`

Line 694 covers `nodeSelector`, node affinity, default-scheduler binding, and the auto-added toleration set (unschedulable / disk pressure / memory pressure / not-ready). That is **D1.3 Scheduling**, Chapter 7's. The outline anticipated and sanctioned it: *"forward to Ch 7 (a DaemonSet's Pods still go through scheduling, and taints are how a node opts out)."* The draft forward-points correctly and the Voyage Ahead reuses it as Chapter 7's hook. Within tolerance — noted for completeness only.

**3. NetworkPolicy-without-a-controller (§8, line 812).** `LOW`

Cited to `k8s-docs-network-policies-2026-08-23` and used as a fourth instance of the named *object-without-component* rule. Touches **D2.1 Networking / D2.2 Security**. Pedagogically the strongest paragraph in §8 — [B3] designates this theme as a named retrievable — and the mention is one clause with no development. Recommend keeping.

**4. CronJob idempotency and approximate scheduling (§7 Closer Look, line 718).** `LOW`

Beyond the outline's "once-versus-on-a-schedule" ceiling, and adjacent to concurrency policy, which §7's guard excludes. But it is not concurrency policy, it is sourced, and it is genuinely associate-relevant. Recommend keeping.

**5. Job `restartPolicy` constraint (§7, line 708).** `NONE`

`Never` or `OnFailure` only. Not on the outline's exclusion list, sourced, and it earns its place as Chapter 5 retrieval. No action.

---

## Depth mismatches

**A note on method.** CNCF publishes **no** sub-weights — Kubernetes Fundamentals is 44% across four competencies, and that is the finest published number. The chapter's `domain_weight_pct: 6` is an authored allocation, and the draft says so at line 104. Depth is therefore assessed against the outline's own **standard-plus** depth band and its per-section attention-cost plan, not against a fabricated per-objective weight. Presenting an authored 6% as an exam weight would itself be a finding.

| Section / cluster | Planned cost | Draft depth | Mismatch |
|---|---|---|---|
| §1 ownership chain | Medium | Medium | OK |
| §2 control loop + HPA | Low | Low — HPA held to two sentences + two forward bearings | OK — correctly resisted |
| §3 selectors + ownership | Medium | Medium; GC internals explicitly named-and-declined (line 291) | OK |
| §4 rolling update | **High** | Deep — two figures, worked arithmetic, Dead Reckoning block | OK — highest-value block, depth earned |
| §5 revisions | Medium | Medium | OK |
| §6 StatefulSet | Medium | **Deep** — ~70 lines incl. figure, Extended Analogy, ordering, Ch 11 limitations | **over-covered** (see drift #1) |
| §7 siblings | Low | Low-Medium | OK — brisk as specified; decision tree lands |
| §8 CRDs + operator | Medium-High | Medium-High; no Operator Framework / OLM / Kubebuilder / maturity levels | OK — exclusions held |
| §9 Zenith | Low | Low, zero new facts | OK |

**Nothing is under-covered.** All eight Exam Alert priorities are taught in-body before they are listed, all three B1 traps (#21/#22/#23) are defused at the point of teaching *and* carry distractors in the question pool, and all six planned figures are present as anchors.

**One over-coverage, one internal inconsistency.**

- **§6 is the only depth overrun** — see drift #1 for the specific paragraphs.
- **`ch06-fig02` contradicts its own section.** The figure labels the surge ceiling **12** (line 376: `surge ceiling (10 + 25%)`), while the prose two pages later correctly computes **13** (lines 407–408: 25% of 10 = 2.5, rounded **up** = 3). Bearings #2 item 1 also answers "Thirteen" (line 557). The figure retained the outline's pre-correction number after the prose adopted the research manifest's Note 1 fix. As drawn, the figure teaches the exact rounding error it exists to prevent, and it is the diagram for Exam Alert priority #6. *(Numeric correctness is the fact-accuracy stage's call; flagged here because it degrades the depth of a load-bearing objective.)*

---

## Gaps the research stage flagged

The research manifest recorded four gaps (G-6A–G-6D) plus a Notes block. Handling:

| Gap | What it flagged | Draft handling | Verdict |
|---|---|---|---|
| **G-6A** | *"A DaemonSet has no `replicas` field"* is not stated verbatim in any fetched source. Load-bearing: Exam Alert #3, §7 Fixed Point, trap #22, Bearings #3 item 2. Manifest recommended phrasing the claim **positively** — *the count is a consequence of how many nodes match* — rather than as an unsourced negative. | **Partially handled.** Body prose (line 698) complies exactly: *"its Pod count is a consequence of how many nodes are eligible, since the controller creates a Pod for each eligible node"* [sourced], plus the HPA corroboration the manifest named as strongest. An AUTHOR-REVIEW comment at line 696 flags the framing for revision — correct pipeline behaviour. **But three summary surfaces still assert the negative:** §7 Fixed Point (line 722), Exam Alert #3 (line 963), Bearings #3 answer 2 (line 870). | **Fix the three summaries** |
| **G-6B** | "Alternatives to DaemonSet" / "Alternatives to ReplicationController" truncated by fetcher. Manifest: not needed. | Draft gives ReplicationController one clause (line 185) sourced to the ReplicaSet page's own successor statement. Correct. | ✅ handled |
| **G-6C** | Job "Job patterns" prose bodies not captured. Manifest: out of scope. | Draft teaches no Job patterns, no parallelism, no `completions`, no `backoffLimit`. | ✅ handled |
| **G-6D** | **Precision hazard.** Job *conditions* are `Complete`/`Failed`; `Succeeded`/`Failed` are *Pod phases*. Manifest: *"the draft should not write 'the Job reaches `Succeeded`.'"* | **Violated in one place.** Practice Q16 and its key are correctly scoped to the Pod (lines 1097, 1159) — good. §7 line 706 is borderline (*"for a Job those two phases are the entire scoreboard"*). But **Chapter Summary line 1189 reads: `**Job** \| Runs to completion, once. Reaches `Succeeded` or `Failed`** — attributing Pod phases to the Job object, which is the exact error G-6D named. Summary rows are high-retrieval surfaces. | **Fix** |

Manifest **Note 1** (the 12→13 surge correction) was adopted in prose and in the Bearings key but **not** in `ch06-fig02` — see the depth section above.

Manifest **Notes 2, 5 and 6** (include `minReadySeconds`; include controller adoption; the three-source selector rule) were all adopted. Notes 3 and 4 are handled above and are immaterial respectively.

**No objective in this chapter lacks an authoritative snapshot.** Per Rule 3, nothing here is a curriculum-alignment failure on source-availability grounds.

---

## Recommended fixes

Ordered by blocking status, then severity. One per issue.

**F1 — BLOCKING, pipeline.** Re-run the voice stage for ch-06. `draft-v1.md` is truncated to 253 of ~1,213 lines and begins mid-word. Verify the regenerated file opens with `# Chapter 6: Fleets, Not Vessels` and retains all six `<!-- FIGURE: -->` anchors and both `<!-- AUTHOR-REVIEW: -->` comments. Do not hand-patch. Every other diagnostic run against ch-06 before this is repaired is invalid.

**F2 — Metadata, outline frontmatter.** Remove `vertical-scaling` and `orphaning` from `kb_tags.concepts`, and `kubectl-apply` and `kubectl-describe` from `kb_tags.commands`. All four are forbidden by the outline's own section-level scope guards and are correctly absent from the draft. Leaving them in makes `kcna-domain-index.md` name Chapter 6 as the coverage site for material Chapters 13 and 17 actually teach, which will surface as false duplicates in `reconcile.py`.

**F3 — Depth, §6.** Cut the StatefulSet section back toward the outline's stated ceiling. Specifically: reduce the ordering paragraph (line 652) to the single sentence Open question #5 authorised, and cut the Chapter 11 limitations paragraph (line 674) down to the forward cross-bearing without stating the two limitations. Retain the three-part identity breakdown, the figure, the interchangeability Fixed Point, and the Snag — those are §6's actual job. `volumeClaimTemplate`, provisioners and volume retention are Chapter 11's material, and stating them here spends Chapter 11's setup.

**F4 — G-6D precision, Chapter Summary.** Change the Job row (line 1189) from *"Reaches `Succeeded` or `Failed`"* to *"Its Pods reach `Succeeded` or `Failed`"*. The Job object's own terminal conditions are `Complete`/`Failed`; `Succeeded` is a Pod phase. Also tighten §7 line 706 to attribute the phases to the Pods explicitly. Practice Q16 and its key already get this right and need no change.

**F5 — G-6A framing, three summary surfaces.** Bring the §7 Fixed Point (line 722), Exam Alert priority #3 (line 963), and Bearings #3 answer 2 (line 870) into line with the body prose and the manifest's recommendation: state the count as *a consequence of how many nodes match*, not as *no replica count*. The body prose at line 698 is the model. Alternatively, cite the negative to the DaemonSet API reference in a later research pass and keep the current wording — but do not ship the negative uncited across three high-retrieval surfaces while an AUTHOR-REVIEW comment flags it as unsourced.

**F6 — Figure/prose consistency, `ch06-fig02`.** Correct the surge ceiling label from **12** to **13** (line 376), and re-label it as `10 + maxSurge(3)` rather than `10 + 25%` so the rounding is visible in the figure rather than implied. The availability floor of 8 is correct. Carry the correction into the illustrator brief, whose current spec still says *"use the worked ten-replica example's actual numbers (12 and 8)."*

**F7 — Editorial, outside this draft.** The two published cross-bearing collisions the draft's AUTHOR-REVIEW comment at line 778 correctly declines to resolve: `chapter-01` line 435 (`§3` → `§6`) and `chapter-02` line 600 (`§3` → `§8`). Two one-token edits in shipped text, per outline Open question #1. Not a Chapter 6 revision task — route to the reconcile pass.

---

**Two notes on how this ran.** First, the audit target had to be substituted: `draft-voice.md` doesn't exist, and the file the voice stage did write is 79% truncated, so I audited `draft-v1-prevoice.md` — the complete chapter — and flagged the truncation as F1. Voice-swap doesn't change objective coverage, so the verdict transfers once F1 is repaired. Second, this file wasn't written to disk because `Write` isn't permitted in this stage; the content above is the stage output for the orchestrator to capture. If you'd like it on disk at `.pipeline-state/ch-06/diagnostics/curriculum-alignment.md`, say so and I'll write it.
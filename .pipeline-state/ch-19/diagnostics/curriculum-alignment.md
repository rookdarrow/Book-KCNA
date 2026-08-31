Working from the cached CNCF/LF curriculum snapshots as the objective authority, the Ch 19 outline's claims, and the draft.

Two notes on method before the artifact: the curriculum publishes **domain** weights but not **per-competency** weights, so the per-objective weights below are an even split within each domain and labelled as derived. And the draft was supplied inline without line numbering, so anchors are by section and quoted phrase rather than fabricated `draft-v1.md:N` citations.

---

# Curriculum-Alignment Audit — KCNA Chapter 19

**Chapter type:** synthesis · **Declared domain weight:** 0% (no new objectives) · **Claimed objectives:** all 13

**Objective ID scheme.** IDs are positional within each domain as the curriculum lists them [source: cncf-kcna-curriculum-pdf-2026-08-23]. This mapping is cross-validated at seven points against the `objectives_covered:` frontmatter of the cached snapshots (D2.4↔Storage, D2.3↔Troubleshooting, D3.1↔Application Delivery, D4.1↔Observability, D4.2↔Ecosystem, D4.3↔Community, D1.1↔Core Concepts) and is consistent everywhere it can be checked.

**Audit posture for a synthesis chapter.** Ch 19 owns no new material; every §1/§2 claim is a retrieval from a shipped chapter. So "covered" here means *the objective's discriminating content is retrievable from this chapter*, not *taught here first*. An objective the reader met in Ch 5 but that Ch 19 never re-surfaces is a synthesis gap, because the whole stated value of the chapter is the second pass.

## Objectives the outline claims to cover

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.1 | Kubernetes Core Concepts | YES | deep |
| D1.2 | Administration | YES | narrow (see note) |
| D1.3 | Scheduling | partial | moderate |
| D1.4 | Containerization | partial | **shallow** |
| D2.1 | Networking | YES | deep |
| D2.2 | Security | YES | deep |
| D2.3 | Troubleshooting | YES | appropriate |
| D2.4 | Storage | YES | deep |
| D3.1 | Application Delivery | YES | appropriate |
| D3.2 | Debugging | partial | **shallow** |
| D4.1 | Observability | YES | appropriate |
| D4.2 | Cloud Native Ecosystem and Principles | YES | deep |
| D4.3 | Cloud Native Community and Collaboration | YES | appropriate by weight, **thin against the chapter's own priority** |

**Structural finding first, because it is the good news:** the draft's §2 pair matrix matches the outline's planned pair list *exactly* — 13 D1 pairs planned / 13 delivered, 13 D2 entries planned / 14 delivered (the outline's three-part NetworkPolicy entry split into two rows), 6 D3 / 6 delivered, 14 D4 / 14 delivered, 14 homonyms / 14 delivered. All nine §1 thread paths reproduce the outline's chapter-and-section paths without deviation. There is no structural drift between outline and draft in the objective-bearing sections.

**Notes on the four non-clean rows:**

- **D1.2 Administration — narrow, not shallow.** Every D1.2 touchpoint in the chapter is version skew: the §2 skew row, the 🔭 Closer Look, Exam Alert #4, practice Q3. The competency's other half — ResourceQuota and LimitRange — survives only as a subordinate clause inside Thread 2 ("Ch 8 §3 builds ResourceQuota (a namespace total) and LimitRange (a per-object default) on it"). ResourceQuota-vs-LimitRange is precisely a §2-shaped confusion pair and it is absent from the matrix. This is an outline-level omission the draft inherited faithfully, not a drafting error.

- **D1.3 Scheduling — taints and tolerations are entirely absent.** The strings "taint" and "toleration" do not appear anywhere in the draft. Scheduling is covered via requests-as-filter-input (Thread 8), node labels (Thread 5), and the scheduler-binds/kubelet-starts and scheduled-once/rescheduled rows. Taints/tolerations vs node affinity is a standard D1.3 discrimination and the highest-value missing pair in the chapter.

- **D1.4 Containerization — one pair row for a competency notionally worth ~11%.** The whole of D1.4 in §2 is `OCI vs CRI`, plus three homonym rows (namespace/kernel, sandbox/runtime, immutable/image) and Thread 6's CRI mention. No practice question is primarily D1.4. Nothing on image tags vs digests, `imagePullPolicy`, or the container/Pod/image boundary.

- **D3.2 Debugging — one row, no practice item, no thread.** The entire competency is the `troubleshooting vs debugging scope: platform vs application` row in the D3 table. D3.2 is one of two competencies in a 16% domain that the chapter's own §4 flags as newly doubled in weight.

## Objectives covered in the draft but NOT in the outline

**No objective-level drift.** Every objective the draft touches is in the outline's `kb_tags.objectives` list, and §3–§6 correctly carry no objectives, as the outline planned (`objectives: []` on all four).

Two scope expansions worth an author decision, both non-objective:

1. **§6 grew a full exam-logistics block the outline did not plan.** The outline's §6 is "a dated final-week plan: what to review, what to leave alone, and what to do the night before." The draft adds equipment checks (monitor count, webcam, wired connection, no VMs, avoid work devices), ID-versus-registration name matching, room preparation, and the check-in window and selfie procedure — five sourced paragraphs drawn from four handbook snapshots. **Recommend keeping it.** It is accurate, it is actionable, and no other chapter owns it. But it is real added length against an Attention Budget line that allots §6 five minutes, and the length/structural stage should see it flagged rather than discover it.

2. **§3's closed-book paragraph** (the CKA-advice-does-not-transfer contrast) is not in the outline's §3 plan. It is well sourced [source: lf-certification-resources-allowed-2026-08-31] and uses that snapshot's own sanctioned phrasing verbatim. Keep.

Neither is scope creep into curriculum territory. Both are strategy material in strategy sections.

## Depth mismatches

Weights below are **derived**, not published: domain weight divided evenly across the competencies the curriculum lists under it. CNCF publishes no per-competency split, so treat these as proportions for allocation reasoning, not as facts about the exam.

| Objective | Exam weight (derived) | Draft depth | Mismatch |
|---|---|---|---|
| D1.1 Core Concepts | ~11% | deep — 6 threads, 9 pair rows, 3 checkpoint items | OK |
| D1.2 Administration | ~11% | moderate but single-topic | narrow — all skew, no quota/limit pair |
| D1.3 Scheduling | ~11% | moderate — 2 pair rows, 2 threads | **under-covered** |
| D1.4 Containerization | ~11% | shallow — 1 pair row, 0 practice items | **under-covered** |
| D2.1 Networking | ~7% | deep — 6 pair rows, 2 threads, 2 practice items | OK (justified) |
| D2.2 Security | ~7% | deep — 3 threads, 4 pair rows, 2 practice items | OK (justified) |
| D2.3 Troubleshooting | ~7% | appropriate | OK |
| D2.4 Storage | ~7% | deep — 4 pair rows, a Snag, 2 of 4 Hazards, Soundings Q3, practice Q6 | over-weight but **earned** — do not trim |
| D3.1 Application Delivery | ~8% | appropriate — 5 pair rows, 2 threads, 2 practice items | OK, with two gaps below |
| D3.2 Debugging | ~8% | shallow — 1 pair row | **under-covered** |
| D4.1 Observability | ~4% | appropriate — 4 pair rows | OK |
| D4.2 Ecosystem | ~4% | deep — 7 pair rows, practice Q10, 3 homonyms | over-covered *relative to D4.3* |
| D4.3 Community | ~4% | 3 pair rows, practice Q9, §4 argument | **under-covered against the chapter's own case** |

### The headline mismatch

**The chapter argues D4.3 is the best hour a reader can spend, then allocates against that argument.**

§4 states Community and Collaboration "has the best ratio of exam presence to study time in the entire book," and Exam Alert #5 repeats it. The outline's practice plan is explicit that D4's two items are "**both from D4.3**, per the deliberate over-representation."

The draft delivers **one** D4.3 practice item (Q9, TOC vs Governing Board). Q10 is VPA-as-add-on — D4.2 Ecosystem. And in §2, D4.2 gets **seven** pair rows to D4.3's **three**. The chapter's stated priority and its actual allocation point in opposite directions, and the practice section misses an explicit outline instruction.

Compounding it: **Q1 and Q10 both resolve to the absent-component pattern.** Two of ten cross-domain items test the same rule, which is what frees Q10's slot for the D4.3 item the outline asked for. The VPA-as-add-on point already lives in §2's HPA/VPA row ("This is thread 3 in Domain 4 clothing"), so relocating it costs the reader nothing.

Also missing from D4.3: **the End User TAB**. It is sourced [source: cncf-charter-governance-bodies-2026-08-31] and the draft *uses* it — as distractor C in Q9, where the answer key explains it. The reader meets a CNCF governance body only in an answer key, never in the matrix that teaches the discriminations.

### Secondary mismatches

- **D3.1 has two uncovered discriminations** in an otherwise well-built section: deployment strategies (rolling update / recreate / canary / blue-green — none of these strings appear in the draft) and Kustomize-versus-Helm (Kustomize is never named; Thread 4 says only "charts and overlays"). Both are D3.1 Application Delivery material, in the domain §4 singles out as having doubled at the 2025-11-24 change.

- **D2.1 has no DNS or service-discovery discriminator.** CoreDNS is never named; stable DNS naming appears once as a clause ("Headless plus StatefulSet is the stable-DNS-name pattern"). Lower priority than the above — the Service ladder and NetworkPolicy rows carry most of the competency's weight.

- **The over-coverage is not the problem.** D2.4 and D2.2 both run deeper than derived weight would suggest, and both are justified: two of the four Navigational Hazards are storage-intuition traps, and the RBAC-matrix derivation is the chapter's cleanest "derive, don't memorize" payoff. **Close the D1.4 / D3.2 / D1.3 gaps additively; do not trim storage or security to fund them.**

## Gaps the research stage flagged

### Handled correctly — recorded so the compliance is on the record

- **Retired five-domain weights (OPEN GAP, `cncf-curriculum-repo-kcna-versions-2026-08-23`).** The snapshot says the retired weights were never extracted and warns: "DO NOT draft the retired weights from memory or from third-party study guides." The outline invited the framing anyway ("D3 doubled from 8% to 16%"). **The draft declined it** — §4 says only "Cloud Native Application Delivery is now 16%" and names the retired observability domain without a weight. Correct call, made against the outline's own prompting.
- **PV phase bullets (RETRIEVAL NOTE, `k8s-docs-persistent-volumes-depth`).** The snapshot bars reproducing the Phase bullets inside quotation marks without another verification pass. The draft's 🪝 Snag paraphrases rather than quotes; Q6's quoted strings come from the **Reclaiming/Retain** subsection, which carries no such caveat. Compliant.
- **Five-phase vs four-phase source disagreement** (API reference vs concept page). The draft never enumerates the phase list, so it does not have to pick a side. Sidestepped cleanly.
- **Check-in time versus exam time (`lf-handbook2-taking-the-exam`: "DO NOT ASSERT EITHER WAY").** §6's morning paragraph describes the check-in window and the specialist wait without claiming either way whether it consumes the 90 minutes. Compliant.
- **LTS (`k8s-version-skew-policy-2026-08-31` `lts_finding`).** The page contains no LTS statement; the draft makes no LTS claim.
- **Version numbers.** Q3 uses a 1.37 API server with 1.33–1.38 distractors, matching the refreshed 08-31 snapshot's 1.35–1.37 series rather than the stale 08-23 capture.
- **`the-lodestar.md` does not exist (outline Open Question #1).** The draft flags it inline with an `AUTHOR-REVIEW` comment naming the blocking status and the provisional block names. That is appropriate gap handling. **Still blocking** — §5's opening sentence asserts the file "ships with this book at the repository root" in the present tense, which must not ship before the file does.

### Not handled — these need action

- **⛔ The exam interface's flag / skip / review-back mechanic is undocumented, and §3's ★ Fixed Point depends on it.** Four cached snapshots independently record the same absence, each under an explicit heading: `lf-mc-exam-important-instructions-2026-08-31` ("No statement about skipping, flagging, marking for review, returning to previous questions, changing an answer, a review screen, or how the exam is submitted. Confirmed absent on targeted fetch"), `lf-mc-exam-faq-2026-08-31`, `lf-exam-rules-and-policies-2026-08-31`, and `lf-handbook2-taking-the-exam-2026-08-31`.

  §3 is built end to end on that mechanic: "flag it, move," "Your flagged questions, in the order you flagged them," "Change an answer only when you can say why," "the flag is a tool, and using it is not surrender," "reserve the rest for flagged questions" in the ★ Fixed Point, and a `flag budget` band in `ch19-fig03-exam-day-pacing`. The draft neither hedges the mechanic nor flags it for author review.

  If the PSI Bridge multiple-choice interface has no flag control, or does not permit returning to an earlier question, the chapter's single strategy Fixed Point is a procedure the reader has memorized and cannot execute — on an exam where, as §3 correctly sources, there is no scratch paper to fall back on. This is the most consequential unhandled gap in the chapter.

- **VPA in-place resize walks into a documented source conflict.** `k8s-docs-autoscaling-and-vpa-2026-08-31` carries an explicit "⚠ SOURCE CONFLICT" header: Sources A, B and C are all kubernetes.io and disagree on whether VPA supports in-place resize (A says it does not; B lists `InPlace` and `InPlaceOrRecreate` among update modes; C says `InPlaceOrRecreate` "has graduated to beta"). The snapshot's instruction is that the trap "must be written to the conflict, not through it."

  Q10's rebuttal of option D quotes Source A only — "as of the sources cached here, 'VPA does not support resizing pods in-place, but this integration is being worked on'" — resolving the conflict silently in one direction. The hedge phrase acknowledges uncertainty without disclosing that the same page family contradicts the quote.

- **Ethical Guardrail #8 frequency-claim discipline is breached on trap #70.** The outline names #70 (`Pending` → don't reach for logs) in the `[inferred]` set, and requires `[inferred]` pairs be called "easy to confuse," never framed by frequency. The draft calls it "the most common instrument error" in §2's D2 table and "the single most common instrument error" in Q2's answer key. Q8's key carries a comparable unsourced claim ("the most common Domain 1 discrimination failure") on a pair that is not `[inferred]`, so #8 does not govern it, but it is the same unsourced-frequency habit.

  Worth noting by contrast: the draft handles **#112 (TAG vs SIG) exactly right** — "These are easy to confuse for a documented reason," with the shared-origin explanation, and no drift into "which is why it's such a common exam trap." That is the pattern the #70 rows should follow.

- **The Logbook Entry states the question count as bare fact.** §6's Logbook says "It is one question out of sixty," unhedged, unsourced, in narrative voice. Both `lf-mc-exam-important-instructions-2026-08-31` and `provenance-kcna-60-questions-2026-08-31` require the class-level hedge and explicitly forbid attributing the figure to KCNA directly. §3's ⚓ Worth Securing gets this right; the Logbook undoes it 2,000 words later.

- **Themes 4–9 provenance (outline Open Question #3) — recorded, no draft fix.** The outline predicted §1 "will present all nine as canonical, which is the right reader experience but overstates their provenance." It does exactly that, with no marker. Confirming for the record so the author's acceptance is a decision rather than an oversight. The three B3-sourced threads (1, 2, 3) are the ones carrying shipped downstream dependencies, so reader-facing risk is contained.

## Recommended fixes

Ordered by consequence. Items 1–2 are the ones that should not reach the integration gate unresolved.

| # | Objective / gap | Fix |
|---|---|---|
| 1 | §3 flag-and-review mechanic | Either commission a targeted research pass on the PSI Bridge multiple-choice interface (does it support flagging, skipping, returning, and answer changes?), or rewrite the ★ Fixed Point and the §3 procedure to be interface-independent — a first pass that answers everything and a reserve that works whether or not the reader can navigate back, with the flag control named as "if the interface offers one." Research is strongly preferable: this is a ★ the reader executes from memory with no scratch paper. |
| 2 | §5 / `the-lodestar.md` | Unchanged from the outline's Open Question #1 and still blocking. Produce the file, then reconcile §5's block names and remove the present-tense "ships with this book" claim until it is true. |
| 3 | D4.3 practice allocation | Replace Q10 with a D4.3 item (SIG vs Working Group vs Committee, or End User TAB vs TOC), satisfying the outline's "both from D4.3." Q10's absent-component payload is already duplicated by Q1 and already stated in §2's HPA/VPA row, so nothing is lost. Budget-neutral. |
| 4 | D4.3 §2 coverage | Add an End User TAB row to the D4 pair table — "voice of end users in CNCF community decisions; the TOC maps that feedback to projects" [source: cncf-charter-governance-bodies-2026-08-31]. Q9 already relies on the reader knowing this body. |
| 5 | D3.2 Debugging | Add one D3 pair row on instrument-by-layer: `describe`/events for platform-layer questions versus `logs`/`exec`/`port-forward` for application-layer ones. Reinforces the phase-first rule the chapter already teaches, and doubles the competency's footprint for one row. |
| 6 | D1.4 Containerization | Add one or two D1 pair rows — image tag vs digest, or `imagePullPolicy` vs image immutability. Retrievable from shipped Ch 2; no new sourcing needed. |
| 7 | D1.3 Scheduling | Add a taints/tolerations vs node affinity row: repel-by-default versus attract-by-preference. Retrievable from shipped Ch 7 §3. |
| 8 | D3.1 Application Delivery | Verify against the section skeleton whether Ch 14/16 shipped deployment strategies and Kustomize; if so, add a rolling-update-vs-recreate-vs-canary row and a Kustomize-overlay-vs-Helm-template row. If neither shipped, this is a book-level gap to record, not a Ch 19 fix. |
| 9 | VPA source conflict | Delete the in-place-resize clause from Q10's option-D rebuttal (or from its replacement item's §2 home). Option D is wrong because VPA is not removed — the in-place sentence is decoration that resolves a flagged conflict in one direction without saying so. |
| 10 | Guardrail #8 / trap #70 | Replace "the most common instrument error" (§2 D2 table) and "the single most common instrument error" (Q2 key) with a mechanism framing — "the error that costs the most time," or simply "easy to reach for." Apply the same softening to Q8's "most common Domain 1 discrimination failure." |
| 11 | Question-count discipline | Rewrite the Logbook's "one question out of sixty" to carry the class-level hedge, or drop the number: "it is one question, it is worth the same as every other question." |
| 12 | D1.2 Administration | Optional, lower priority: add a ResourceQuota (namespace total) vs LimitRange (per-object default) row so the competency is not entirely version skew. |

**Editorial, noted in passing** because it sits inside the objective-bearing section: the homonym table's **`plugin`** row has an empty Sense B column, so a two-sense table row currently teaches nothing, and the **`volume`** row's Sense B ("A Docker volume") carries no chapter anchor where every other row has one. Both are in §2 and both are quick.

---

*Stage output — capture to `../Book-KCNA/.pipeline-state/ch-19/diagnostics/curriculum-alignment.md` per the executor convention rather than writing it from this session.*
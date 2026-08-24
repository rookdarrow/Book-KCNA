Verification complete. Emitting the stage artifact to stdout (per pipeline convention — `Write` is deliberately excluded from stage `--allowed-tools` so the orchestrator captures output atomically).

---

# Integration Check — KCNA Chapter 6

## ⚠ SCOPE NOTICE — read before consuming this report

**The artifact I was handed is not a shippable chapter, and the defect is not cosmetic.**

The stage input (identical, byte-for-byte, to `.pipeline-state/ch-06/draft-v2.md` on disk) contains only the chapter tail: partial Exam Alert → Practice Questions → Answers → Chapter Summary → The Voyage Ahead → Safe Harbor. Sections §1–§9, the frontmatter, Attention Budget, epigraph, Soundings, Why This Chapter Matters, What You'll Learn, and all three Taking Your Bearings checkpoints are absent.

This is independently corroborated four ways, and I confirmed all four on disk:

| Evidence | Finding |
|---|---|
| `draft-v1-prevoice.md` | **1,213 lines / 119 KB — intact.** Opens `# Chapter 6: Fleets, Not Vessels`. Nothing is lost. |
| `draft-v1.md` | 253 lines / 24 KB — begins mid-word (`ognition exam can ask about…`) |
| `draft-v2.md` (my input) | 26 KB — same truncation, voice-polished |
| `diagnostics/structural.md` | 8 FAIL / 4 WARN, every one an artifact of the truncation |

`diagnostics/fact-accuracy.md`, `question-quality.md`, and `curriculum-alignment.md` each detected this independently and each re-targeted onto `draft-v1-prevoice.md`. I did the same. **Checks below are run against the intact chapter where the revised draft cannot support them, and every row states which artifact it was verified against.** That is the methodologically correct target: voice-swap alters register, not integration surface.

**I did not reconstruct the chapter.** That is the revision stage's job after re-harvest.

---

## Summary

- Terminology consistency: **pass** — 2 low-severity drifts, 0 canon conflicts
- Callbacks to earlier chapters: **15 correct / 0 incorrect outbound** (Ch 6 → Ch 1–5); **6 correct / 2 incorrect inbound** (Ch 1–5 → Ch 6)
- Retrieval-practice accuracy: **pass** — 4/4 correct in the revised draft, 7/7 across the intact chapter
- Glossary coverage: **51 concepts introduced** per outline; **48 defined in the intact chapter**, **0 definable from the revised draft**; **3 mis-attributed** (belong to Ch 4); **1 term never appears in prose**
- Contradictions with earlier canon: **none in prose** — 2 broken inbound cross-bearings + 1 figure-anchor mismatch are pointer defects, not doctrinal conflicts
- Ethical guardrails (skill Part 14): **pass for the revised draft's own content**; 1 unresolved accuracy defect sits in the absent head

---

## Terminology consistency

Verified against shipped `chapter-01`…`chapter-05` and the intact `draft-v1-prevoice.md`.

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| Pod | `Pod` (Ch 5) | throughout | No |
| Deployment / ReplicaSet / StatefulSet / DaemonSet | CamelCase resource kinds (Ch 4 §5 established) | throughout | No |
| Job / CronJob | `Job`, `CronJob` | throughout | No |
| kubelet | `kubelet`, lowercase (Ch 3 §3) | 1 (answer key A12) | No |
| kube-controller-manager | lowercase hyphenated (Ch 3 §2) | 2 | No |
| kube-scheduler | lowercase hyphenated (Ch 3 §2) | 1 | No |
| control plane | lowercase in prose (Ch 3) | 5 | No |
| `spec` / `status` | code-styled lowercase (Ch 4 §2) | throughout | No |
| label selector | `label selector` (Ch 4 §5 ★ Fixed Point) | throughout | No |
| `matchLabels` / `matchExpressions` | code-styled camelCase (Ch 4 §5) | 2 | No |
| Service | `Service` (Ch 3/4/5) | 4 | No |
| readiness / liveness probe | lowercase (Ch 5 §7) | 6 | No |
| namespace | lowercase (Ch 4 §3) | 2 | No |
| **Pod template** | `Pod template` — 27 of 28 uses | 28 | **Yes, minor** — one lowercase `pod template` at prevoice line 179 |
| **CRD / CustomResourceDefinition** | Ch 2 line 600 uses bare `CRDs`, never expanded | expanded properly in Ch 6 §8 | **Yes, minor** — first mention in the book (Ch 2) is an unexpanded acronym |
| HorizontalPodAutoscaler / HPA | expanded on first use, prevoice line 251 | 4 | No *(in intact draft)* |
| PodSpec vs PodTemplateSpec | distinct concepts, correctly separated | — | No |

**Drift 1 — `pod template` (lowercase), prevoice line 179.** Sits inside a paraphrase of the DaemonSet docs, so the lowercasing is explicable, but it is inconsistent with the chapter's own 27 other uses. One-token fix.

**Drift 2 — `CRDs` unexpanded at first mention.** Chapter 2 line 600 introduces the acronym with no expansion; the expansion doesn't arrive until Chapter 6 §8. Not a Ch 6 defect, but it is a book-level terminology gap that stage 14 should resolve by giving the glossary entry a "first mentioned Ch 2, defined Ch 6 §8" cross-reference.

**Not drift, but worth recording:** in the *revised draft*, `HPA`, `PodTemplateSpec`, and `Service` all appear in the answer key with no antecedent, because the sections that introduce them are missing. These resolve on re-harvest.

---

## Callback correctness

### Outbound — Chapter 6 → earlier chapters (15 checked, 15 correct)

Verified against shipped chapter files, not from memory.

| Ch 6 location | Claim | Target verified | Verdict |
|---|---|---|---|
| Soundings A7, §2 | Ch 3 §6 — the control loop | Ch 3 §6 "Controllers and the Control Loop" (line 750) | ✓ |
| Soundings A8 | "Chapter 5 said a Pod is never rescheduled" | Ch 5 line 539 🪝 Snag, verbatim match | ✓ |
| §1 line 98 | "Chapter 5 ended on a question and refused to answer it" | Ch 5 §4 "Why this forces something else to exist" + Voyage Ahead line 1464 | ✓ |
| §1 line 127 | Ch 5 §4 — Pod disposability and replacement | Ch 5 §4 "Scheduled Once, Replaced Never" (line 525) | ✓ |
| §1 line 181 | Ch 4 §2 — the four fields every object carries | Ch 4 §2 "The four fields" (line 194) | ✓ |
| §2 line 195 | "Chapter 3 promised a loop you could watch, and named the ReplicaSet" | Ch 3 line 831 cross-bearing, exact | ✓ |
| §2 line 199 | "Chapter 3's thermostat" | Ch 3 uses the thermostat 3× | ✓ |
| §3 line 261 | "Chapter 4 listed four things that use selectors and named ReplicaSet" | Ch 4 line 688 lists exactly four (ReplicaSet, Service, node scheduling, NetworkPolicy) and points here | ✓ |
| §4 line 454/460 | Ch 5 §7 — readiness probes | Ch 5 §7 "Three Probes, Three Jobs" (line 785) | ✓ |
| §8 line 776 | Ch 3 §6 — controllers you configure yourself | Ch 3 line 956 cross-bearing | ✓ |
| §8 line 776 | Ch 2 §4 — the pluggable-interface pattern | Ch 2 §4 "The pattern to name now" (line 596) | ✓ |
| §8 line 804, §9 line 914 | "Chapter 3's control loop" | Ch 3 §6 | ✓ |

One precision nit, not an error: §8 line 776 says *"Chapter 2 named **CustomResourceDefinitions** as the fourth socket."* Chapter 2 wrote `CRDs`. The substance is right; the quoted form isn't what Chapter 2 actually printed.

### Inbound — earlier chapters → Chapter 6 (8 checked, **2 incorrect**)

Chapter 6's §-numbering is fixed by its Attention Budget: **§3 = "How a Controller Knows Its Own" (selectors/ownership), §6 = "When Pods Are Not Interchangeable" (StatefulSets), §8 = "The Control Loop, Extended" (CRDs/operators).**

| Source | Pointer | Correct target | Verdict |
|---|---|---|---|
| `chapter-01` line 436 | `see Ch 6 §3 — StatefulSets and stable identity` | **§6** | ❌ **WRONG** |
| `chapter-02` line 600 | `see Ch 6 §3 — CRDs and extending the API` | **§8** | ❌ **WRONG** |
| `chapter-03` line 831 | `see Ch 6 — ReplicaSet, a control loop you can watch` | §2 (chapter-level, no §) | ✓ |
| `chapter-03` line 956 | `see Ch 6 — controllers you configure yourself` | §8 (chapter-level) | ✓ |
| `chapter-04` line 269 | `see Ch 6 — Deployments and ReplicaSets` | §1 (chapter-level) | ✓ |
| `chapter-04` line 688 | `see Ch 6 — a controller's selector and the Pods it owns` | §3 (chapter-level) | ✓ |
| `chapter-05` line 539 | `see Ch 6 — StatefulSets` | §6 (chapter-level) | ✓ |
| `chapter-05` line 551 / 1464 | `see Ch 6 §1 — the resource that holds the surviving intent` | §1 | ✓ |

**Both failures are already known to the draft.** `draft-v1-prevoice.md` line 778 carries an `AUTHOR-REVIEW` comment naming exactly these two and recommending a one-token edit in the shipped Chapter 1 and Chapter 2 text rather than renumbering Chapter 6. **I confirm that recommendation is correct** — six other inbound pointers and the entire outline depend on the current numbering; editing two tokens in two shipped files is the cheap side of the trade.

This failure mode is a known repo hazard: `chapter-02`'s own frontmatter (lines 17–21) carries a standing warning that *"Section NUMBERING IS LOAD-BEARING."* Chapter 1 and Chapter 2 published pointers into Chapter 6 before Chapter 6's section order existed.

**Author decision required — 2 edits, outside this chapter's files:**
- `chapter-01-taking-departure.md:436` — `Ch 6 §3` → `Ch 6 §6`
- `chapter-02-cargo-in-standard-crates.md:600` — `Ch 6 §3` → `Ch 6 §8`

---

## Retrieval-practice accuracy

Every `[retrieval: chN]` tag was checked against the named chapter's actual section content.

### In the revised draft (4 tags, 4 correct)

| Q | Tag | Topic | Target section verified | Verdict |
|---|---|---|---|---|
| P2 | `ch4` | `spec` vs `status` | Ch 4 §2 "The two fields that matter most" (line 259) | ✓ **Exact** |
| P4 | `ch5` | Pod replaced, not moved; new UID | Ch 5 §4 "Scheduled Once, Replaced Never" (line 525) | ✓ |
| P16 | `ch5` | Pod phase `Succeeded` | Ch 5 §5 "Pod Phases and Container States" (line 563) | ✓ |
| P18 | `ch3` | control loop vs kube-controller-manager built-ins | Ch 3 §6 (line 750) + §2 kube-controller-manager (line 419) | ✓ |

P2 is better than merely correct. Chapter 4 line 273 explicitly forecasts it: *"Chapter 5 reads it against a Pod's phase, **Chapter 6 reads it against a replica count**."* Ch 6 P2 is the promised payoff, drawing on the same snapshot (`k8s-docs-objects-2026-08-23`) and the same worked example.

### In the intact chapter (3 further tags, 3 correct)

Bearings #1 Q4 (`ch3`, control loop states) ✓ · Bearings #1 Q5 (`ch4`, selectors as shared join) ✓ · Bearings #2 Q4 (`ch5`, readiness probes) ✓ · Soundings Q8 (`ch5`, node dies) ✓.

`question-quality.md` measured spacing at **20.6% (7 of 34)** against a 20% target — compliant. I confirm the target attribution for all seven.

### Header tallies

The revised draft's header — *"Nineteen questions. Four reach back to Chapters 3, 4, and 5. Five require two sections at once."* — is **arithmetically correct**: 19 items, 4 `[retrieval:]` tags spanning ch3/ch4/ch5, 5 `[interleaved:]` tags (P11, P12, P14, P18, P19).

One under-count worth noting: **P12 is tagged `[interleaved: Ch 5 §7 + §4]` and genuinely reaches back to Chapter 5, but carries no `[retrieval:]` tag**, so it isn't in the "four." Ch 5 §7 is "Three Probes, Three Jobs" — the tag is accurate. If the book's retrieval metric is ever computed mechanically from `[retrieval:]` tags alone, this item is invisible to it. Low severity; flagging because it affects a book-level measurement, not this chapter's correctness.

---

## Glossary coverage

Concept inventory taken from `outline.md` frontmatter (`concepts:` per section). **51 concepts** across §1–§8; §9 introduces none.

**Definitional status could not be assessed from the revised draft** — it contains no body prose, so 0 of 51 are defined there. The column below reports the **intact chapter**.

| Concept/command introduced | § | Defined in-chapter? | Needs glossary entry? |
|---|---|---|---|
| `workload-resource`, `deployment`, `replicaset`, `pod-template`, `podtemplatespec`, `ownership-chain` | §1 | yes | yes |
| `replicationcontroller-legacy` | §1 | yes (line 185, one clause, deliberate) | yes — mark superseded |
| `replicas`, `desired-replica-count`, `horizontal-scaling`, `manual-horizontal-scaling` | §2 | yes | yes |
| `horizontalpodautoscaler` | §2 | yes — expanded on first use (line 251) | yes |
| `label-selector`, `matchlabels`, `matchexpressions` | §3 | **defined in Ch 4 §5, not here** | yes — **cross-reference Ch 4** |
| `selector-template-agreement`, `owner-reference`, `cascading-deletion`, `overlapping-selectors`, `controller-adoption` | §3 | yes | yes |
| `orphaning` | §3 | **no — term never appears in the draft** | **author decision** |
| `deployment-strategy`, `rolling-update`, `recreate-strategy`, `maxsurge`, `maxunavailable`, `minreadyseconds`, `readiness-gated-rollout` | §4 | yes | yes |
| `rollout`, `revision`, `rollout-history`, `rollback`, `revision-history-limit`, `pause-rollout`, `resume-rollout`, `stuck-rollout` | §5 | yes | yes |
| `statefulset`, `stable-pod-identity`, `pod-interchangeability` | §6 | yes | yes |
| `daemonset`, `node-local-facility`, `job`, `run-to-completion`, `cronjob`, `cronjob-schedule` | §7 | yes | yes |
| `custom-resource`, `customresourcedefinition`, `custom-controller`, `operator-pattern`, `declarative-api`, `dynamic-registration` | §8 | yes | yes |

**Three findings for stage 14:**

1. **`label-selector` / `matchlabels` / `matchexpressions` are mis-attributed.** The outline tags them "introduced" at Ch 6 §3, but Chapter 4 §5 introduces them, sources them (`k8s-docs-labels-selectors-2026-08-23`), and gives the label selector its own ★ Fixed Point. Chapter 6 §3 *applies* them. Glossary cross-references must read **(Chapter 4)**, not (Chapter 6).

2. **`orphaning` never appears.** Zero occurrences of `orphan` in the intact 1,213-line draft. The adjacent concept is covered — §3 discusses adoption of Pods that "carry no controller owner reference" — but the term the outline promises is never given to the reader. Either add the term to §3 or drop the outline tag; do not let stage 14 mint a glossary entry for a word the book never uses.

3. **Terms borrowed forward.** `PersistentVolumeClaim` (§6, line 624) and `Headless Service` (§6, line 676) are named and used in Chapter 6 but deliberately left half-taught, with cross-bearings to Ch 11 and Ch 9 §5. The outline flags this as the book's only intentional half-teach. Glossary entries should point at Ch 11 / Ch 9, with Ch 6 as first mention. This is correct handling, not a defect — recording it so stage 14 doesn't "fix" it.

---

## Cross-artifact consistency (figure anchors)

Not covered by any sibling diagnostic; checked here because `style-decisions.md` locks the anchor ID as the join key between draft prose and `image-specs.md`.

**One mismatch — the Zenith figure will not join.**

| Draft anchor (`draft-v1-prevoice.md:916`) | `image-specs.md` ID | Match? |
|---|---|---|
| `ch06-zenith-control-loop-instantiated` | `ch06-fig06-control-loop-instantiated` | ❌ |

The draft follows the outline, which names it `ch06-zenith-control-loop-instantiated` (outline line 213). Stage 10 renamed it to `fig06`. The other five anchors (`fig01`–`fig05`) join cleanly. **Author decision: pick one ID and align both artifacts** — the outline/draft form carries the semantic marker (`zenith`), which is the one the diagram pipeline's metadata check reads.

Separately: **the revised draft contains zero FIGURE anchors** — all six live in the missing body — so all six specs currently dangle. Resolves on re-harvest.

---

## Ethical guardrails check

Applied to the revised draft's own content, per skill Part 14.

- [x] **No fabricated statistics or claims** — the revised draft contains no statistics. Cross-referencing `fact-accuracy.md`: **2 contradicted claims** exist chapter-wide. One (Chapter Summary Job row) **was fixed** in this revision. The other — *"twelve named competencies"* where all three cached CNCF sources enumerate **thirteen** (prevoice line 104) — **remains unresolved and sits in the absent head.** This is a miscount about the exam itself, in the section that establishes the chapter's authority. Highest-priority content fix after re-harvest.
- [x] **Fear-based content uses real examples** — no fear framing present. The `Recreate` treatment is exemplary: downtime is presented as a deliberate engineering trade with a stated cost, not a warning.
- [ ] **Simplification acknowledged** — cannot verify from the revised draft: 0 Dead Reckoning blocks, 0 ★ Fixed Points, 0 ⚠ Navigational Hazards (all truncated away). The intact chapter carries them. The answer keys that *are* present do this well — A16 pauses to distinguish the Pod phase `Succeeded` from the Job condition `Complete`; A7 flags that rounding never bites at `replicas: 8`.
- [x] **Authority claims cite legitimate sources** — every answer-key claim in the revised draft carries a `[source: ...]` tag; `fact-accuracy.md` reports **zero dangling tags** across 162 tags / 25 snapshots.
- [x] **"Frequently tested" claims verifiable** — the Common Traps preamble (*"these are documented confusions, not invented ones"*) is substantiated: the outline binds §6–§7 distractors to book-level trap register entries #21–#23, and `question-quality.md` independently rates trap fidelity as "unusually good."
- [x] **No strawmanning of alternative study methods** — none present.
- [x] **Subject dignity (v5.7)** — pass. The wry beats are aimed at the practitioner (*"the answer people hope for"*, *"which is why the trap is worth a question"*), never at users harmed by an outage.

**One guardrail caveat carried forward, not re-audited here:** `fact-accuracy.md` flags that Practice Q5's keyed answer (*"there is no such validation"*) rests on an **uncited negative** — the cached docs document the overlapping-selector hazard but say nothing about whether an error is emitted. That answer key is present in the revised draft and unchanged. Under guardrail 4 (*never claim certainty where legitimate uncertainty exists*), this one needs the softening the fact-accuracy stage proposed, or a new fetch. Flagging because **it is in the shipping text**, not merely in the missing head.

---

## Recommended fixes

The revision stage resolved very little, and the reason is structural rather than a lapse in judgment.

**What the revision stage actually did.** Its own output, `draft-v2-prevoice.md`, carries **21** numbered practice questions — two inserted after Q15 — plus the fact-accuracy fix to the Chapter Summary Job row and the DaemonSet count-as-consequence reframing. The voice stage that followed saw a damaged, triplicated input, chose the "internally complete" 19-question set, and carried over only the two wordings it could map cleanly. **The 19-question set it selected is the pre-revision set.** I verified this directly: P6, P7, and P14 in the delivered draft are byte-identical to their `draft-v1.md` forms.

**This resolves the voice stage's open question.** It asked whether 19 or 21 is correct and kept 19. `question-quality.md` confirms the outline budget is **19 practice questions / 42 chapter total, met exactly**. So 19 is the budgeted number — but the revision stage's two additions were almost certainly *repairs*, not padding, and dropping to 19 reverted them. **Do not treat "19" as settled by budget arithmetic alone.** Recover `draft-v2-prevoice.md`'s Q16–Q17 and judge them on merit; above-budget is explicitly sanctioned by the skill.

### Unresolved in the delivered draft — ranked

1. **Re-harvest `draft-v1.md` from `draft-v1-prevoice.md` and re-run the voice stage.** Everything else is downstream. Verify the output is ~1,200 lines and begins `# Chapter 6: Fleets, Not Vessels`. Do not hand-patch. Four sibling diagnostics reach the same conclusion independently. This is the same failure class as commits `c358a92` and `821f1ef`, and the harvester's `<details>` extraction is now producing *overlapping concatenated regions* — the triplicated tail and the spliced `(If the block above contains [file not available]…` marker are harvester output, not draft content. **The harvester regression is the root cause and will recur on ch-07 if it isn't fixed.**

2. **P14 is still broken — the most severe question-quality finding in the chapter.** Three of four options are defensible correct answers; the key concedes it (*"C is `.spec.replicas`. D is `metadata.namespace`"*) rather than resolving it. Skill Part 10B classifies this as *undesirable* difficulty. `question-quality.md` supplies a drop-in replacement stem that also closes the `matchLabels`/`matchExpressions` coverage gap. **Unapplied.**

3. **P7 options A and B assert identical cluster state** (both "10 max, 6 min"). At `replicas: 8`, nothing rounds, so the discriminating clause is inert. Recommended repair: change to `replicas: 6`, which makes all four options numerically distinct and actually tests the rounding asymmetry. **Unapplied.**

4. **P6 option A is implausible** (a `--show-labels` display flag driving API validation), reducing the item to three options; option B's why-wrong is a five-word dismissal where the reader needs the `.spec.selector`-vs-`nodeSelector` distinction. **Unapplied.**

5. **"Twelve named competencies" contradicts all three cached CNCF sources** (thirteen). In the absent head; fix on re-harvest.

6. **Practice Q5's key rests on an uncited negative.** In the shipping text. Soften or fetch.

7. **Two shipped-file cross-bearing edits** (Ch 1 §3→§6, Ch 2 §3→§8) — see Callback correctness.

8. **Zenith figure anchor ID mismatch** between draft and `image-specs.md`.

9. **Minor:** lowercase `pod template` at prevoice line 179; `orphaning` term absent; `label-selector` family mis-attributed to Ch 6 in the outline's concept tags.

### What passed cleanly

Terminology discipline across five chapters is genuinely strong — no canon conflicts, no marker drift, no resource-kind casing errors. Outbound callback precision is 15/15 with section-level accuracy, and the Ch 4 → Ch 6 `spec`/`status` handoff is the tightest cross-chapter setup-and-payoff in the book so far. Retrieval tagging is accurate in every instance checked. **The chapter's integration surface is sound; the pipeline's transport is what failed.**

---

Two things I'd flag for your attention above the report itself:

- **The harvester is the root cause, and it's still live.** Commit `821f1ef` fixed `<details>` extraction but appears to have introduced overlapping-region concatenation. Chapter 7 will hit this too. That's worth fixing before re-running ch-06, or you'll re-harvest into the same corruption.
- **The revision stage's work is recoverable but only from `draft-v2-prevoice.md`**, which is itself truncated to its last 7 KB. Its two added questions survive there in full; its edits to Q1–Q14 do not. Worth reading before deciding whether re-running revision from a clean re-harvest is cheaper than salvaging.
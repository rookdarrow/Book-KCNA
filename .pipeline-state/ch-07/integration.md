I have everything I need. Verification is complete across all five shipped chapters, the ch-06 outline and its withdrawn draft, the ch-07 outline, and all four diagnostics.

Per the `--allowed-tools` contract in CLAUDE.md, I'm emitting this to stdout for the orchestrator to capture rather than writing the file myself.

```markdown
# Integration Check — KCNA Chapter 7

**Draft audited:** `.pipeline-state/ch-07/draft-v2.md` (1,124 lines, 2026-08-24)
**Verified against:** shipped `chapter-01` … `chapter-05`; `.pipeline-state/ch-06/outline.md`; the withdrawn `chapter-06` draft (git `2a78912`); `.pipeline-state/ch-07/outline.md`; all four `diagnostics/` reports.

**Note on knowledge-base shards.** The stage prompt passed `[no knowledge-base shards tagged]`. Rather than hedge, I read the shipped chapter files directly from `../Book-KCNA/`. Every back-bearing below is verified against real text and cited by line number. The two exceptions are Chapter 6 back-bearings, which cannot be verified against shipped text because **Chapter 6 does not exist in the repository** — see Finding 1.

---

## Summary

- Terminology consistency: **fail** — one systematic drift (British spellings, 15 instances, zero precedent in the shipped corpus), one intra-chapter inconsistency, one house-convention break on the metadata line
- Callbacks to earlier chapters: **7 correct / 2 unverifiable** (both point at unshipped Chapter 6)
- Retrieval-practice accuracy: **pass** — 5 of 7 verified against shipped text; 2 point at Chapter 6 and match its planned numbering
- Glossary coverage: **44 concepts introduced, 35 defined in-chapter, 9 require glossary entries**
- Contradictions with earlier canon: **none** — 1 unpaid promise flagged (Chapter 3's six scheduling factors)
- Ethical guardrails (skill Part 14): **fail** — one unsourced disparagement of competing study guides (guardrail #3)

**Gate-level finding that outranks everything below:** the revision stage did not apply the diagnostics. See Finding 0.

---

## Finding 0 — The revision stage produced no revisions

`draft-v2.md` differs from `draft-v1.md` at **22 line ranges**. All 22 are em-dash-to-comma/colon punctuation substitutions and two expanded `AUTHOR-REVIEW` comments. Representative:

- L129 `…any suitable nodes — often more than one.` → `…any suitable nodes, often more than one.`
- L716 `Overrules — not "takes precedence…"` → `Overrules, not "takes precedence…"`

**Not one diagnostic finding was applied.** The fact-accuracy FAIL lines are byte-identical in v2:

| Diagnostic finding | v1 line | Status in v2 |
|---|---|---|
| Metadata line untagged + breaks ch-02/ch-05 house form | 4, 6 | unchanged |
| "which the scheduler never consults at all" — unsourced absolute negative, and Practice Q3 grades distractor **A** wrong on it | 203 (recurs 215, 297, 882, 1038) | unchanged |
| "Some of that total is spoken for by things that aren't Pods" — asserts the capacity/allocatable relationship that research-manifest gap **G-7C** exists to prevent | 229 | unchanged |
| `node.kubernetes.io/unschedulable` "deliberate administrative act" — untagged causal claim | 522, 1105 | unchanged |
| Soundings A5 spends ☆ Bearings #2 Q2, the chapter's designated struggle item | 68 | unchanged |
| Theming density 0.4/1,000 against a 1–3 floor | whole chapter | unchanged |
| D1.3-09 scheduling factors — 3 of 6 absent | §1/§2 | unchanged |

Structural lint is genuinely clean (0 fail, 0 warn, 29 pass) and question budget is exact (40/40), so the chapter is not in bad shape. But **this gate is being asked to pass a draft whose audit findings were never worked.** That is an author decision, not mine to make — flagging it as the primary item.

Two contributing causes worth fixing at the pipeline rather than per-chapter, both self-reported by the diagnostics:

- `context_packer.py:216` maps `draft_voice → draft-voice.md`, but `apply_voice_swap()` (`orchestrator.py:250`) has already renamed that file into `draft-v1.md`. Every downstream stage requesting the voiced draft gets an empty substitution and has to recover by hand. Three of four diagnostics open with a paragraph about this.
- `draft-v2-prevoice.md` is **68 lines** against draft-v1-prevoice's 1,122. That artifact is truncated.

---

## Terminology consistency

| Term | Canonical form (evidence) | Occurrences in this chapter | Drift? |
|---|---|---|---|
| kubelet | lowercase — ch03 §3, ch05 §8 | ~30 | no — zero `Kubelet` in ch7 or corpus |
| kube-scheduler | lowercase hyphenated — ch03:415 | ~20 | no |
| API server / `kube-apiserver` | "API server" in prose, component name in figures — ch03 §2 | 16 prose, 1 figure | no |
| Pod / pod | `Pod` capitalized in house prose — ch01–05 throughout | ~400 | no — lowercase appears only inside verbatim source quotes |
| control plane | two words, lowercase — ch03 §2 | 8 | no |
| ReplicaSet, Deployment, DaemonSet, StatefulSet | CamelCase — ch04 §5, ch06 outline | ~25 | no |
| label selector | "label selector" — ch04:660 ★ Fixed Point | 6 | no |
| set-based operators | `in`, `notin`, `exists` **lowercase** — ch04 §5 | Practice Q12 uses lowercase; affinity operators use `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt` capitalized | **no — correctly distinguished.** Two different enums, and the chapter keeps them apart. Verified deliberate |
| requests / limits | lowercase — ch05 §8 | ~40 | no |
| Allocatable / Capacity | capitalized per `k8s-docs-node-allocatable` | 6 | no — new to this chapter |
| inter-Pod | — | **11 `inter-Pod` vs 3 `Inter-pod`** (L628, L673, L796) | **yes — intra-chapter.** See below |
| -ise/-our spellings | corpus is **100% American**: 61 American forms across ch01–05, **0 British** | **15 British forms** | **yes — systematic.** See below |
| Metadata line form | ch05:190 — domain + published weight + both source tags inline | L4/L6 drop the 44% domain weight and both tags, and move the disclosure to a separate italic line | **yes — house-convention break.** Already raised by fact-accuracy; unfixed |
| Section heading form | ch02/ch03 ship `## §1 — ⚪ Title`; ch05 ships `## ⚪ §1 — Title` | ch7 uses the ch05 form | no — correct per outline OQ#12; the ch02/ch03 reconciliation is a book-level sweep, not this chapter's |

### Drift 1 — British spellings (15 instances, systematic)

The shipped corpus uses American spellings exclusively: 61 occurrences of `behavior`/`recognize`/`organize`/`analyze`/`prioritize`/`internalize` across all five chapters, **zero** British forms. Chapter 7 introduces:

| Form | Lines | House form |
|---|---|---|
| behaviour | 68, 479, 748, 1040, 1042 | behavior |
| honour | 181, 591 | honor |
| recognise / Recognise | 113, 683 | recognize |
| neighbouring | 1000, 1058 | neighboring |
| labelled | 370, 647 | labeled (ch05:718; note ch04:753 has one `labelled`, so this pair is already mixed book-wide) |
| internalised | 326 | internalized |
| optimise | 1042 | optimize |

L113 is in **What You'll Learn** and L1042 is in a graded answer explanation — both high-visibility. Mechanical fix.

### Drift 2 — `inter-Pod` casing (intra-chapter)

Eleven instances use `inter-Pod`; three use `Inter-pod` (L628, L673, L796). The three lowercase ones track the Kubernetes docs, which write `Inter-pod` (`k8s-docs-assign-pod-node-2026-08-23:19`). That is defensible **inside quotation marks** — and L673 is inside a genuine quoted passage, so it is correct there. But L628 and L796 are the chapter's own prose carrying a source tag, not quotations.

**Recommend:** house form `inter-Pod` in unquoted prose (L628, L796); leave L673 alone as verbatim.

---

## Callback correctness

Every back-bearing traced to the shipped file and line.

| # | Cross-bearing (ch7 line) | Target | Verified? |
|---|---|---|---|
| 1 | Ch 2 §7 — RuntimeClass (L233) | `chapter-02:787` `## §7 — 🟡 Not All Isolation Is Equal: RuntimeClass` | ✅ correct |
| 2 | Ch 3 §2 — the control plane components (L121) | `chapter-03:354` `## §2 — ⚪ The Control Plane`; the deferral is at `:417` — *"see Ch 7 — how the scheduler actually chooses, in detail"* | ✅ correct, and the promise is real |
| 3 | Ch 3 §2 — the control plane (L890, Exam Alert) | `chapter-03:415` — *"the scheduler selects a node and records that choice. It does not start anything."* Ch 7's claim that the trap "was defused explicitly" in Chapter 3 is exactly right | ✅ correct |
| 4 | Ch 4 §5 — labels and selectors (L324) | `chapter-04:630` `## §5 — 🔵 The Universal Join`. Ch 7 says Chapter 4 "listed node scheduling constraints as one of the **four** things they're used for" — `chapter-04:688` lists exactly four: ReplicaSet, Service, node scheduling constraints, NetworkPolicy | ✅ correct, and the count is exact |
| 5 | Ch 5 §4 — the Pod's lifecycle (L185) | `chapter-05:525` `## ⚪ §4 — Scheduled Once, Replaced Never` | ✅ correct |
| 6 | Ch 5 §8 — requests and limits (L197) | `chapter-05:864` `## 🟡 §8 — What a Pod Is Owed`. The inbound pin at `chapter-05:969` reads *"see Ch 7 §2 — resource requests as a scheduling filter"* and §2 **is** exactly that | ✅ correct — pin honored precisely |
| 7 | Ch 5 §8 — QoS classes (L223) | QoS classes are in §8, in figure `ch05-fig05-requests-limits-qos-classes` at `chapter-05:938` — the figure ID Ch 7 cites by name | ✅ correct, figure ID verified |
| 8 | Ch 6 §7 — DaemonSets (L526) | `.pipeline-state/ch-06/outline.md:498` `### §7 — ⚪ One Per Node, and Work That Ends` | ⚠ **unverifiable — see Finding 1** |
| 9 | Ch 6 §1 — Deployments and ReplicaSets (L622) | `.pipeline-state/ch-06/outline.md:353` `### §1 — ⚪ The Resource That Holds the Intent`. Corroborated by `chapter-05:559`, which independently pins *"see Ch 6 §1 — the resource that holds the surviving intent"* | ⚠ **unverifiable — see Finding 1** |

Forward-bearings (Ch 8 ×4, Ch 9, Ch 12, Ch 13 ×2, Ch 17 ×2) cannot be verified against text that doesn't exist yet, which is expected. All ten match the forward contracts in `ch-07/outline.md` § *What this chapter owes forward*, and §6's Ch 17 pointer correctly **names** the pluggable-scheduler fact without pre-collecting the four-socket extension story the outline reserves for Chapter 17's secondary Zenith.

### Finding 1 — Chapter 6 does not exist, and Chapter 7 leans on it six times

`git log`:
```
2bb971b Chapter 6: withdraw truncated draft pending re-run
2a78912 Chapter 6: drafted via pipeline
```

`chapter-06-fleets-not-vessels.md` was committed and then **withdrawn**. `Book-KCNA/` currently ships chapters 01–05 only. The ch-07 outline's Open Question #11 describes the file as present-but-truncated; that description is now stale — it is gone entirely.

Chapter 7's dependencies on it:

| Ch 7 location | Depends on |
|---|---|
| §1 opening (L96) | *"The last chapter ended on the one thing the control loop cannot do"* — Chapter 6's Voyage Ahead |
| Why This Chapter Matters (L98) | *"Chapters 4 through 6 made you someone who can write down what should exist"* |
| Soundings preamble (L45) | *"Three of them ask you to retrieve something specific from Chapters 5 and 6"* |
| §4 DaemonSet callback (L524–526) | *"Chapter 6 told you that DaemonSets keep running on nodes where nothing else will, and said you'd already met the mechanism in disguise"* |
| §5 (L622) | Ch 6 §1 back-bearing |
| §7 (L862) | *"the same shape as every controller in Chapter 6"* |

The two riskiest are §1's opening beat and §4's callback, because both assert **what Chapter 6 said**, not merely what it covered. The ch-07 outline recorded (from the now-withdrawn draft) that Chapter 6's Voyage Ahead did say both things, including naming *"the DaemonSet's tolerations as the mechanism already seen in disguise."* But that text has been withdrawn for re-drafting, and **a re-run is not obliged to reproduce it.**

**Recommend:** record both as explicit debts Chapter 6 now owes Chapter 7 — the Voyage Ahead must end on the scheduler gap, and §7 must plant the DaemonSet-tolerations tease — and add them to `ch-06/outline.md` § *What this chapter owes forward* before the re-run. Otherwise Chapter 7 ships two callbacks to sentences nobody wrote. Re-verify §1 and §7 numbering after the harvest.

### Finding 2 — Chapter 2's inbound pointer is still partially wrong (author decision)

`chapter-02:807` reads *[cross-bearing: see Ch 7 §3 — node selection, tolerations, and accounting for overhead]*. Those three topics land in **§3, §4 and §2** respectively. Confirmed against shipped text.

The draft's own `AUTHOR-REVIEW` at L1121 flags this and correctly declines to edit shipped Chapter 2 from inside Chapter 7. The outline's recommendation stands and I endorse it: **delete the `§3` token**, making it `*[cross-bearing: see Ch 7 — node selection, tolerations, and accounting for overhead]*`. That matches the two other Chapter 7 inbound pointers (`chapter-03:417`, `chapter-04:688`), both already unnumbered. One-token edit in shipped text; needs author sign-off because it touches a committed chapter.

### Finding 3 — Chapter 3 published a six-item list that Chapter 7 never closes

`chapter-03:413` gives the reader, verbatim from the docs:

> Factors taken into account for scheduling decisions include individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, **data locality**, **inter-workload interference**, and **deadlines**.

Chapter 7 is the chapter that owes the detail. It delivers resource requirements, policy constraints, and affinity/anti-affinity. It never mentions data locality, inter-workload interference, or deadlines — not even to place them out of scope. Curriculum-alignment flagged this as coverage (D1.3-09, PARTIAL); the *integration* cost is that a reader who remembers Chapter 3's list gets no acknowledgement that three items were dropped.

Not a contradiction, and not an argument for teaching them. But the chapter already models the right fix twice — the preemption clause (*"Register that they exist so that nothing in this chapter reads as a lie later"*) and the `minDomains` mention. **Recommend one sentence in §2 or §7** doing the same for the remaining three factors.

---

## Retrieval-practice accuracy

| Question | Tag | Topic | Target verified |
|---|---|---|---|
| ☆ Bearings #1 Q3 | `[retrieval: ch5]` | request vs limit; which component reads which | ✅ `chapter-05:872` — the two-words/two-components table and its ★ Fixed Point |
| ☆ Bearings #1 Q5 | `[retrieval: ch6]` | ReplicaSet creates a Pod that can't be placed | ⚠ Ch 6 §1 (unshipped). Contract exists: `ch-06/outline.md` owes-forward names *"Workload resources create Pods → Ch 7 (**named anchor** — the controller that produced the unscheduled Pod)"* |
| ☆ Bearings #2 Q1 | `[retrieval: ch4]` | selector direction inverts for node selection | ✅ `chapter-04:630` §5, and `:688` explicitly names node scheduling constraints as a selector use |
| Practice Q5 | `[retrieval: ch5]` | scheduled once, never rescheduled | ✅ `chapter-05:531–533` |
| Practice Q6 | `[retrieval: ch3]` | scheduler records; kubelet starts | ✅ `chapter-03:415`, near-verbatim |
| Practice Q12 | `[retrieval: ch4]` | set-based operators `in`, `notin`, `exists` | ✅ `chapter-04:656`. Casing matches Chapter 4 exactly, and the contrast with affinity's capitalized enum is handled correctly |
| Practice Q15 | `[retrieval: ch6]` | DaemonSet one-per-node needs no anti-affinity | ⚠ Ch 6 §7 (unshipped). `ch-06/outline.md:498` plans exactly this, incl. the "not a replica count" trap |

**Verdict: pass.** Five verified against shipped text, two against Chapter 6's planned content with explicit outline contracts on both sides. Spacing is 21.9% against a 20% target (question-quality). No misaligned tags.

One sub-item, low priority: the Soundings preamble says *"Three of them ask you to retrieve something specific from Chapters 5 and 6"* (Q3, Q4, Q6), but the 0–2 rubric sends the reader only to *"Chapter 5 §8 and Chapter 5 §4."* Q6's ReplicaSet framing is Chapter 6's. As it happens `chapter-05:551–557` does cover "something outside it has to know that three replicas were wanted… and create a third," so the rubric is not wrong — just narrower than the preamble. Add Ch 6 §1 to the rubric, or drop "and 6" from the preamble.

---

## Glossary coverage

All 44 `kb_tags.concepts` appear in the draft (confirmed by curriculum-alignment). Tabling only the ones with a definition question — the other 35 are defined in-chapter at recognition depth and need no separate entry.

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| `node-capacity` (**Capacity**) | no — named alongside Allocatable, then deferred: *"What exactly, and how it's configured, is Chapter 8's material"* | **yes** |
| `node-allocatable` (**Allocatable**) | yes — defined by quotation | no |
| `pod-overhead` | partial — existence and purpose only; the `AUTHOR-REVIEW` at §2 states the mechanism is deliberately withheld for lack of a snapshot | **yes** |
| `scheduler-plugins` (`QueueSort`, `Reserve`, `Permit`) | no — listed as stage names, never defined | **yes** (or accept as list-only) |
| `custom-scheduler` / `schedulerName` | minimal — *"you can write your own scheduling component"* | **yes** |
| PriorityClass / preemption | no — one clause, explicitly scoped out | **yes** — named terms should be findable |
| `OutOfmemory` / `OutOfcpu` | no — cited as failure reasons | **yes** |
| ResourceQuota, LimitRange | no — named, deferred to Ch 8 | **yes** (Ch 8 owns the definition) |
| NodeRestriction admission plugin | no — named, deferred to Ch 8 | **yes** (Ch 8 owns the definition) |
| `minDomains` | yes | no |
| Predicates / Priorities | yes — defined as older names for filtering/scoring | no |
| `topologyKey`, `maxSkew`, `whenUnsatisfiable`, `labelSelector` | yes — four-field table | no |
| taint, toleration, `NoSchedule`, `PreferNoSchedule`, `NoExecute`, `tolerationSeconds`, taint matching, built-in condition taints | yes | no |
| `nodeSelector`, node affinity, the six operators, `…DuringScheduling…DuringExecution`, `nodeName` | yes | no |
| filtering, scoring, binding, feasible node, `PodFitsResources`, random tie-break, unschedulable, `Pending` | yes | no |
| `kubectl get nodes`, `kubectl label`, `kubectl taint` | yes — shown with argument syntax, incl. the trailing-minus removal form | no |

**Count: 44 introduced, 35 defined in-chapter, 9 require glossary entries.**

Reused-not-reintroduced (correctly assume prior definition, no ch7 glossary obligation): Pod, node, kubelet, kube-scheduler, control plane, API server, label, label selector, ReplicaSet, Deployment, DaemonSet, requests, limits, QoS class, UID, RuntimeClass.

One note for stage 14: `kubectl get nodes --show-labels`, `kubectl label nodes`, and both `kubectl taint` forms are the first full command lines in the chapter. Outline OQ#10 recommended *command names freely, command lines not at all* unless a fetch supplied them — `k8s-docs-assign-pods-nodes-task-2026-08-24` and `k8s-docs-taints-tolerations-depth-2026-08-24` did land, and the draft tags both. Compliant; recorded so the ch-08 command-surface work knows these three already shipped.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims** — the chapter contains no statistics at all. The Logbook Entry's "two hundred nodes, eight of which are GPUs" is explicit scenario framing, not asserted data. (Fact-accuracy owns the 6 untagged-claim FAILs; not re-audited here per rule 3.)
- [x] **Fear-based content uses real examples** — no fear framing. Consequences described are practitioner-experience ("the run is slow"), never third-party harm. **Subject-dignity guardrail (skill v5.7 Part 14): pass** — every wry beat is aimed at practitioners, including "being wrong first is exactly why this will stick" and "the answers a competent engineer would design."
- [x] **Simplification acknowledged** — §4's matching rules use a `— Dead Reckoning` block. Three explicit uncertainty signals, all well-formed: the preemption clause (*"Register that they exist so that nothing in this chapter reads as a lie later"*), the §5 spread-constraint limitation (*"no guarantee that the constraints remain satisfied when Pods are removed"*), and §6's `PodFitsResources`-is-an-example 🔭 Closer Look. This is the chapter's strongest guardrail performance.
- [x] **Authority claims cite legitimate sources** — 146 inline `[source:]` tags across 16 snapshots, all resolving to cached files. Zero unresolvable tags.
- [~] **"Frequently tested" claims verifiable** — no exam-frequency claims. There are four unhedged superlatives about *candidate error* frequency: L285 *"the single most common misconception about the scheduler,"* L439 *"the most common real-world mistake in this material,"* L898 *"The most durable error in this material,"* L1044 *"the most common misconception about this component."* The skill's Voice Alignment section sanctions this register, but its example hedges (*"Common confusion: many candidates mix up…"*). The shipped corpus contains **zero** instances of this phrasing. **Advisory, not a fail** — soften one or two to "a common" and the register matches both the skill and the corpus.
- [ ] **No strawmanning of alternative study methods — FAIL**

### Guardrail #3 violation, L1113 (🏆 Safe Harbor)

> "Scheduling is the material that **most study guides present as a catalogue of six unrelated features**, and you have it as one pipeline with two slots."

This is an unsourced negative claim about competitors' pedagogy, in service of a favorable comparison to this book. Skill Part 14 guardrail #3 is *"NEVER strawman alternative study methods,"* and the Part 14 table marks the Social Proof analogue ("Everyone uses our guide") as the manipulative column.

The nearest corpus precedent is `chapter-01:200` — *"Now a disclosure most study guides skip"* — which is materially different: it claims competitors **omit** something and then supplies it, rather than claiming they **teach it badly**. Chapter 7's version is the only instance of its kind in the book.

**Recommend** rewriting to make the claim about the material rather than about other publishers, which loses nothing and is also just truer:

> "Scheduling is easy to meet as a catalogue of six unrelated features, and you have it as one pipeline with two slots."

---

## Recommended fixes

Diagnostics that revision did **not** address are listed in Finding 0 and are not repeated here. These are integration-scope items the diagnostics did not raise.

**Blocking — author decision required**

1. **Chapter 6 dependencies (Finding 1).** Record the §1-opening and §4-DaemonSet callbacks as explicit debts in `ch-06/outline.md` § *What this chapter owes forward* before the harvest re-run, then re-verify the §1/§7 numbering. Without this, two Chapter 7 callbacks assert sentences that may not survive the re-draft.
2. **`chapter-02:807` (Finding 2).** Delete the `§3` token. One-token edit to shipped text; endorsed, but it touches a committed chapter.

**Should fix before the knowledge-base update**

3. **Guardrail #3 violation at L1113.** Rewrite as above. This is the only ethical FAIL and the fix is one clause.
4. **British spellings, 15 instances.** Mechanical sweep to house American forms. L113 (What You'll Learn) and L1042 (graded answer) are the visible ones.
5. **Chapter 3's six scheduling factors (Finding 3).** One sentence acknowledging data locality, inter-workload interference, and deadlines as out of scope. The chapter already does this correctly for preemption; copy that move.

**Low priority**

6. `inter-Pod` casing at L628 and L796 (leave L673, it's a verbatim quote).
7. Soundings preamble says "Chapters 5 and 6"; the 0–2 rubric names only Chapter 5. Add Ch 6 §1 to the rubric or drop "and 6."
8. §1 introduces binding as *"not what most people assume"* — `chapter-03:415` already told the reader exactly what binding is, and the ch-07 outline instructed §1 to *"collect it rather than re-argue it."* The Exam Alert handles the callback correctly; §1's framing slightly wastes the reader's prior knowledge.
9. §7's *"the same shape as every controller in Chapter 6"* carries no cross-bearing. `chapter-03:750` §6 is where the control loop was first taught; a pointer there would strengthen the Zenith.

**Pipeline (not chapter content)**

10. `context_packer.py:216` `draft_voice → draft-voice.md` is stale after `apply_voice_swap()`. Three of four diagnostics opened by recovering from this by hand.
11. `draft-v2-prevoice.md` is 68 lines against 1,122 expected — truncated artifact.
```

**The headline for you:** the chapter's integration is genuinely good — all seven verifiable back-bearings are correct, two of them exact to a counted list and a figure ID, and retrieval spacing is clean. But two things need your call before this passes: **the revision stage shipped punctuation changes and nothing else**, so every diagnostic finding is still open; and **Chapter 6 has been withdrawn from the repo**, while Chapter 7 asserts twice what Chapter 6 *said*.
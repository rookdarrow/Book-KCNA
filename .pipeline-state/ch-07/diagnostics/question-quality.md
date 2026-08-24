I have the draft (the voice stage wrote in place — `draft-v1.md`, 10:07, with `draft-v1-prevoice.md` as the backup), the outline's `question_budget` block, and all six ★ Fixed Points. Emitting the audit to stdout for the orchestrator to capture (per the `--allowed-tools` contract in CLAUDE.md, rather than writing the file myself and racing its atomic write).

```markdown
# Question-Quality Audit — Chapter 7

## Summary

- Chapter type: content
- Total questions inspected: 40
  - 🧭 Soundings questions: 8
  - ☆ Taking Your Bearings questions: 15 (across 3 checkpoints)
  - Practice questions: 17
- Question budget compliance: **met** (40/40, every category exact)
- Weak distractors (WARN): 5
- Trap answers that don't target real misconceptions (WARN): 4
- Missing or incomplete why-wrong explanations (FAIL): **0 missing** — every MCQ has per-option coverage. 4 grouped explanations are imprecise (WARN, not FAIL); detailed below.
- Retrieval-practice spacing: **compliant** (21.9% against a 20% target)
- Soundings spoiler check: **stems and distractors clean (8/8)** — but 2 answer-key entries pre-state material the chapter later relies on as a surprise. WARN, detailed below.

The question architecture here is strong. Prediction and discrimination items dominate (11 of 17 Practice questions), the enumeration cap the outline set was honoured, all four planned interleaving pairings are present, and all ten Exam Alert traps appear as live distractors somewhere. The findings below are refinements, not a rebuild. The two that materially cost the chapter something are the Soundings answer-key leak into the designated struggle item, and the untested §4 matching block / §5 spread-constraint fields.

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 15 | 15 | met |
| Taking Your Bearings (checkpoints) | ≥2 | 3 (5 + 5 + 5) | met |
| Practice Questions | 17 | 17 | met |
| **Chapter total** | **40** | **40** | **met** |

Practice-block distribution also matches the outline's plan: §1–§2 = 6 (P1–P6), §3–§4 = 6 (P7–P12), §5 = 3 (P13–P15), §6 = 2 (P16–P17). Interleaving requirement (≥4 items needing two sections at once) met exactly by the four pairings the outline named: P7 (§2+§3), P10 (§1+§4), P13 (§4+§5), P16 (§6+§2+§3). Enumeration cap ("no more than three of seventeen") met: P1, P11, P12 are the pure-recall items, and P11 is the taint-effect list the outline explicitly authorised.

Soundings mechanics: `<details>` disclosure present (draft-v1.md:63–90) ✓. Rubric present with all three bands, plus the outline's specified 0–2 branch instruction naming Ch 5 §8 and Ch 5 §4 (draft-v1.md:84–88) ✓. Designated struggle item is labelled and the difficulty normalised (draft-v1.md:556) ✓.

## Soundings spoiler check

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Declaring a job's requirement in advance | no | Stem is machine-agnostic. Answer teases "hold onto the word *available*" without defining it — correct handling |
| 2 | Tie-breaking as a design question | no | Answer eliminates three wrong rules and says "Kubernetes' actual answer is in §1, and it isn't any of the three above." Withholds `random`. Well built |
| 3 | [retrieval ch5] request vs limit | no | Prerequisite retrieval, not a chapter Fixed Point. §2's Fixed Point is the *booking consequence*, which is withheld |
| 4 | [retrieval ch5] scheduled-once | no | Prerequisite retrieval. §3's `IgnoredDuringExecution` naming is withheld |
| 5 | Mark the machines vs mark the jobs | **stem no — answer key yes** | A5: *"marked jobs are only **permitted** onto the reserved machines, not **pulled** toward them, so they may still end up somewhere else entirely"* vs §4 Fixed Point: *"Tolerations permit — they never attract."* Same claim, same verb |
| 6 | [retrieval ch6] the loop with nowhere to put a Pod | no | Answer explicitly withholds the status string: "What the Pod's own status says while that's true is §2's material" |
| 7 | Two replicas, one machine | no | Names the loss, withholds `topologyKey` and the labels-of-other-Pods mechanism |
| 8 | Pinning to a named worker | **stem no — answer key partially** | A8: *"the job **fails** instead of going somewhere else, and you've opted out of every check the assigner was performing for free"* vs §6 Fixed Point: *"because it skips the feasibility check, a Pod that doesn't fit **fails** rather than waiting in `Pending`"* |

**Verdict on the rule as the template defines it (stem + distractors): clean, 8/8.** Both leaks are in the `<details>` answer key, which the reader opens only after answering — so the *pre-test* itself is not compromised in either case. The cost is downstream, and it is real, so I am reporting it rather than passing it silently. See the two per-question findings below.

## Per-question findings

### Q Soundings 5: "Some machines in your fleet are reserved for one team's workloads…"

**Issue:** The answer key pre-spends ☆ Bearings #2 item 2 — the chapter's *designated* struggle item, whose entire pedagogical value is that the intuitive answer is wrong. Bearings #2 Q2 is labelled "This one is intentionally hard, and the intuitive answer is wrong. Struggle is the point." But a reader who read Soundings A5 was told, in plain English and 30-odd pages earlier, that marking the machines *permits* rather than *pulls*, and that marked jobs "may still end up somewhere else entirely" — which is precisely the Bearings scenario's outcome. The struggle item degrades from a genuine misconception trap into a recall check.

This is not a broken pre-test (the reader answers before opening the box) and not a Fixed Point spoiled in a stem. It is a spent surprise, which is a different failure and worth naming as such.

**Why-wrong explanation status:** present and specific (open-response item; both halves of the asymmetry are addressed).

**Recommended fix:** truncate A5 at the asymmetry without resolving the second half. Replace *"but marked jobs are only permitted onto the reserved machines, not pulled toward them, so they may still end up somewhere else entirely"* with *"but marking the machines only changes what they refuse. Whether it also changes where your marked jobs actually land is a separate question, and §4 turns on the answer."* Keeps the pre-test's diagnostic value, keeps the forward pointer, hands over nothing.

### Q Soundings 8: "…give one good reason to override the assignment and pin a job to a named worker"

**Issue:** A8 states the distinctive half of §6's Fixed Point — that pinning makes the job *fail* rather than relocate, because you opted out of the check — in generic terms. That exact discrimination is the load-bearing content of both ☆ Bearings #3 item 3 and Practice Q16, and both answer keys describe `Pending`-instead-of-fails as "the trap" / "the good distractor."

Lower severity than the Q5 finding: the question *asks* the reader to generate the drawback, so a reader who gets it right generated it themselves (pretesting effect working as designed), and the framing is system-agnostic rather than Kubernetes-specific.

**Why-wrong explanation status:** present and specific.

**Recommended fix:** optional. If touched, soften "the job fails instead of going somewhere else" to "the job has nowhere to fall back to," which preserves the insight without pre-announcing the `fails`-not-`Pending` discrimination that two later questions turn on.

### Q B2.2 / P9: the dedicated-GPU-node scenario, used twice

**Issue:** Two distinct problems, one fix.

First, the two items share a near-identical scenario: taint `dedicated=gpu:NoSchedule`, matching toleration added, Pods landing on ordinary nodes. Bearings #2 Q2 is open-response, P9 is MCQ — different *format*, but the outline required "two different question **shapes**." With the scenario held constant, P9 tests whether the reader remembers the Bearings answer, not whether the principle transfers.

Second, the outline's §3–§4 Practice requirement — *"the toleration-attracts misconception must appear at least twice, in two different question shapes"* — is unmet inside the Practice block. P9 is the only Practice item carrying it. P10 and P11 test taint *effects*; P13 tests that pod affinity cannot restore a filtered-out node, which is adjacent but a different error.

**Distractor analysis (P9):**
- A) "The toleration is malformed" — plausible to someone who assumes a correct toleration would place the Pod. Strong.
- B) "The taint effect should be `NoExecute` to force the Pods onto the GPU nodes" — plausible to someone conflating effect strength with attraction. Strong.
- C) correct.
- D) "The scheduler prefers untainted nodes and cannot be persuaded" — plausible to someone who thinks taints lower a score rather than filter. Moderate.

Distractors are fine. The problem is scenario reuse, not option quality.

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** no budget change required. Re-skin one of the two and re-shape P9 into a *remediation* item, which also satisfies the two-shapes requirement:
- Change B2.2's scenario to a licensed-software node pool (`license=matlab:NoSchedule`), keeping the diagnosis framing.
- Re-shape P9 to: *"Which single change makes the training Pods land on the GPU nodes?"* — A) add a second toleration for the same taint; B) change the effect to `NoExecute`; C) label the GPU nodes and add a matching `nodeSelector` or required node affinity to the Pods **(correct)**; D) remove the taint. That is the "what fixes it" shape rather than the "what's wrong" shape, and it converts the chapter's most durable error into a transfer test.

### Q P6: "Which pair correctly assigns responsibility?"

**Issue:** The three distractors are not independent. B, C and D all encode the single error "the scheduler starts the containers," which the answer key states outright: *"**B**, **C** and **D** all put container-starting in the scheduler's hands."* A reader holding only that one fact eliminates all three simultaneously — the item collapses from a four-option question to a one-bit question, and the additional errors bundled into C (controller manager records the placement) and D (API server selects the node) do no discriminating work and go unexplained.

**Distractor analysis:**
- A) correct.
- B) "The scheduler starts the containers; the kubelet reports their status" — plausible to trap #24. Strong.
- C) "The controller manager records the placement; the scheduler starts the containers" — carries trap #24 *plus* a distinct controller-manager confusion, but the second error is redundant once the first is spotted.
- D) "The API server selects the node; the scheduler starts the containers" — same redundancy.

**Why-wrong explanation status:** present but imprecise. One grouped sentence covers three options and addresses only their shared error.

**Recommended fix:** make one distractor wrong on a *different* axis so the item has more than one discriminating dimension. Replace D with *"The scheduler selects the node and notifies the kubelet directly; the kubelet starts the containers"* — this concedes trap #24 (the reader cannot eliminate it with that fact alone) and instead tests whether they know the scheduler talks to the API server, not to nodes. Then split the why-wrong: B and C for the container-starting error, D for the direct-to-kubelet error.

### Q P3 option D: "No — a node may only host three Pods."

**Issue:** Fabricated for symmetry. No reader holds this belief, and the key concedes it: *"**D** invents a Pod-count limit that isn't the constraint under discussion."* The item is effectively three-option, which matters because P3 is one of the chapter's best questions (option A is the usage-arithmetic trap, and it is excellent).

**Recommended fix:** replace D with a second usage-flavoured wrong answer so the trap has company: *"No — the node's limits sum to more than its allocatable memory."* That targets a real and common confusion (limits, not requests, as the scheduling input) and keeps every option in the same conceptual family. A max-pods-per-node ceiling does exist in Kubernetes, so if the Pod-count shape is wanted, use a plausible figure and make it clearly not the binding constraint — but the limits-sum version is the better distractor.

### Q P12 option C: "Node affinity supports only `Exists` and `DoesNotExist`."

**Issue:** Arbitrary subset with no misconception behind it. Nobody arrives believing affinity has exactly those two operators and no others.

**Distractor analysis:**
- A) "only equality, exactly like `nodeSelector`" — targets the real "two syntaxes for the same power" trap. Strong.
- B) correct.
- C) arbitrary subset. Weak.
- D) "no operators; expressiveness comes solely from the soft/hard distinction" — targets a genuine partial reading of §3. Moderate.

**Why-wrong explanation status:** present but imprecise. *"**C** and **D** understate the operator set"* mischaracterises D, which claims there are *no* operators rather than fewer, and leaves D's second clause (that soft/hard is the sole differentiator) unaddressed — despite that being the more interesting error of the two.

**Recommended fix:** replace C with *"Node affinity supports the same operators as `nodeSelector`, plus `Gt` and `Lt` for numeric comparison"* — plausible to a reader who half-remembers that `Gt`/`Lt` are the unusual additions, and it forces recall of the full list rather than recognition. Then split the why-wrong: C for the incomplete list, D for "soft/hard is the only difference — affinity adds both, and this option drops one."

### Q P13 option C: "The Pod schedules there and the taint is automatically tolerated because affinity implies intent."

**Issue:** Fabricated. "Affinity implies intent" is not a belief anyone holds; the rationale clause reads as hand-wavy and marks the option as wrong on register alone, before any Kubernetes knowledge is applied. The key concedes it: *"**C** invents implicit toleration."*

P13 is otherwise one of the strongest items in the set — A (ordering rule lets affinity override a taint) is a genuinely tempting misconception, and the correct answer's "affinity can only narrow, never restore" is the chapter's best filter-composition insight.

**Recommended fix:** replace C with *"The Pod schedules there, because a required pod-affinity rule is evaluated as a filter and a `NoSchedule` taint only affects scoring."* That targets a real and specific error — misfiling `NoSchedule` on the scoring side — and it directly interferes with P10, which is exactly the kind of cross-item tension a good distractor creates.

### Q P14 option D: "The rule becomes invalid, because `topology.kubernetes.io/zone` is not a valid topology key."

**Issue:** Eliminable by anyone who read §5, where the label appears repeatedly as a worked example. It tests page-recency, not understanding.

**Distractor analysis:**
- A) "No change — the rule already spread the Pods across nodes" — targets the reader who hasn't registered that the domain changed. Strong.
- B) "The rule becomes weaker; more Pods can share a zone" — the direction inversion, and the single most valuable distractor in the item. Strong.
- C) correct.
- D) invalidity claim. Weak.

**Why-wrong explanation status:** present and specific for all three (each gets its own sentence). Good.

**Recommended fix:** replace D with *"The rule becomes stricter, and the scheduler places the extra replicas on nodes that minimise skew rather than leaving them `Pending`."* That targets the `DoNotSchedule` vs `ScheduleAnyway` confusion, which is currently taught in §5 and tested nowhere (see Coverage below) — one edit closes a distractor gap and a coverage gap together.

### Q P1 option A: "Bind, filter, score"

**Issue:** Binding-first is not a permutation anyone arrives at; the key calls it *"incoherent."* Labelling your own distractor incoherent is an admission it isn't doing work. P1 effectively has two live distractors (C, the order inversion, and D, binding-as-middle-step).

Lower severity than the four above — this is a duplicate-by-design item (it re-tests B1.1 for spacing), so its job is confirmation rather than discrimination.

**Recommended fix:** low priority. If touched, replace A with *"Filter, score, bind — and the scheduler then instructs the kubelet directly"* — same correct sequence, one wrong actor, which forces the reader to read past the sequence rather than pattern-matching on word order alone.

### Q P5: grouped why-wrong is inaccurate for one option

**Issue:** The key reads *"**A**, **C** and **D** all describe a rebalancing behaviour the platform does not have."* True of A ("re-evaluates placement periodically and migrates it") and D ("evicted and rescheduled at the next scoring cycle"). Not true of C — "The kubelet on the new node claims it" describes a *pull* model with the wrong actor, not rebalancing. A reader who chose C is told they made an error they didn't make.

**Why-wrong explanation status:** present but inaccurate for one of three grouped options.

**Recommended fix:** split C out: *"**C** has the wrong actor and the wrong direction — a kubelet never claims Pods. It acts on Pods the API server has already recorded as bound to its node."* That also reinforces the §1 binding boundary, which is the chapter's most-retrieved Fixed Point.

### Q P17: grouped why-wrong is generic

**Issue:** *"**C** and **D** both deny a correspondence that is stated directly in the source."* C's specific claim — "filtering had no configurable component" — is a substantive assertion that goes unrefuted. Minor, but it is the last item in the chapter and the reader's last impression of the answer-key standard.

**Recommended fix:** *"**C** is wrong on the specific point that filtering was unconfigurable: Predicates were exactly the configurable filtering component. **D** denies a mapping the source states directly."*

### Cross-cutting: the correct option is the longest in 7 of 17 Practice questions

**Issue:** In P7, P9, P12, P13, P14, P15 and P16, the correct option is visibly the longest — usually because it carries a because-clause the distractors don't. This is a well-known test-wise tell, and a reader who notices it can score above their knowledge level on roughly 40% of the set. It also inverts the desirable-difficulty design: the option that should require the most thought is flagged as the answer before it's read.

Not present in P3, P10, P11 (well balanced), and B3.3 handles it correctly — options B and C are near-identical in length and differ only in the one word that matters (`Pending` vs `fails`). That item is the model.

**Recommended fix:** pad the distractors' rationale clauses to match, rather than cutting the correct answers. P13 is the clearest case: A/C/D are one clause each against B's three. Giving each distractor its own because-clause costs nothing pedagogically and removes the tell. Where a because-clause genuinely can't be invented for a distractor, move the correct answer's rationale into the answer key instead of the option text.

## Retrieval-practice spacing

- Chapter 7 target: **20%** of checkpoint questions from earlier chapters (arc outline, tagged **[B3]**; supersedes B4's ~15% figure, per the outline's recorded resolution)
- Actual: **21.9%** — 7 of 32 combined Bearings + Practice items tagged `[retrieval: chN]`
  - ☆ Bearings: 3 of 15 (20.0%) — B1.3 `[ch5]`, B1.5 `[ch6]`, B2.1 `[ch4]`
  - Practice: 4 of 17 (23.5%) — P5 `[ch5]`, P6 `[ch3]`, P12 `[ch4]`, P15 `[ch6]`
- Status: **compliant.** Within skill Part 10's 10–25% band and matched to the outline's planned 3-in-Bearings / 4-in-Practice split exactly.

All three **[B3]** named anchors landed in their designated sections:

| **[B3]** anchor | Planned placement | Actual | Status |
|---|---|---|---|
| Requests (Ch 5) as the filter input | Bearings #1, item 3 | B1.3 | ✓ |
| The controller (Ch 6) that produced the unscheduled Pod | Bearings #1, item 5 | B1.5 | ✓ |
| Labels (Ch 4) now doing node selection | Bearings #2, item 1 | B2.1 | ✓, and written as the *inversion* rather than the definition, as the outline required |

Two notes, neither a defect:

- **Bearings #1 carries 2 of the 3 Bearings retrieval items (40% for that checkpoint).** The outline anticipated and justified this: both anchors belong to §2 and nowhere else. The chapter-level rate is what the schedule measures, and it is compliant.
- **P6 is tagged `[retrieval: ch3]`**, four chapters back. The outline recorded this as voluntary early adoption of B3's ≥4-back spacing floor, which doesn't formally activate until Chapter 8. Consistent with plan, not drift.
- **Bearings #3 carries zero retrieval**, as planned — the outline's reasoning (a fourth Bearings retrieval would push the checkpoint off its own topic) holds, and the chapter rate is met without it.

Recommended additions if short: **none needed.**

## Coverage vs concepts

Against `kb_tags.concepts` in the outline frontmatter (45 concepts) plus `kb_tags.commands` (4).

| Concept introduced in chapter | Tested in a question? |
|---|---|
| scheduling | yes (B1.1, P1) |
| kube-scheduler | yes (B1.2, P2, P6) |
| unbound-pod | yes (P1) |
| feasible-node | yes (B1.1, P7) |
| filtering | yes (B1.1, P1, P7, P10) |
| scoring | yes (B1.1, P1, P10) |
| binding | yes (B1.1, P1, P6, B3.5) |
| random-tie-break | yes (B1.2, P2) |
| unschedulable | yes (B1.5, P4) |
| pending-pod | yes (B1.5, P4, P7) |
| podfitsresources | yes (P17 stem, P7) |
| requests-as-scheduling-input | yes (B1.3, B1.4, P3) |
| node-capacity | **NO** — `Capacity` vs `Allocatable` is taught with a practical rule (draft-v1.md:227–229) but every stem hands the reader "allocatable" already (B1.4, P3, P7), so the distinction is never the object of a question |
| node-allocatable | partial — used in stems, never tested |
| pod-overhead | **NO** |
| scheduled-once-per-lifetime | yes (P5, B2.4, P8) |
| node-labels | yes (B2.1, P12) |
| standard-node-labels | partial — `topology.kubernetes.io/zone` appears in P14-D as a to-be-rejected option only |
| nodeselector | yes (B2.5, P7, P12, B3.3, P16) |
| node-affinity | yes (B2.4, B2.5, P8, P12) |
| required-during-scheduling | yes (B2.4, P8) |
| preferred-during-scheduling | yes (B2.5) — weakly; no item turns on preferred *behaviour* |
| ignored-during-execution | yes (B2.4, P8) |
| affinity-operators | yes (B2.5, P12) |
| taint | yes (B2.2, B2.3, P9–P11, P13) |
| toleration | yes (B2.2, B2.3, P9, P11) |
| noschedule | yes (B2.3, P10, P11, P13) |
| prefernoschedule | yes (B2.3, P10, P11) |
| noexecute | yes (B2.3, P11) |
| tolerationseconds | **NO** — taught in depth including the automatic 300s default for `not-ready`/`unreachable` (draft-v1.md:449, 520); appears only as P8's *wrong* option C |
| taint-toleration-matching | **NO** — the four matching rules and two wildcards (the required `— Dead Reckoning` block, draft-v1.md:487–492) get zero retrieval |
| built-in-node-condition-taints | yes (B3.5) |
| pod-affinity | yes (P13) |
| pod-anti-affinity | yes (B3.1, B3.2, P14, P15) |
| topology-domain | yes (B3.2, P14) |
| topology-key | yes (B3.2, P14) |
| topology-spread-constraints | **NO** — named in P15's stem and B3.1's key, but `maxSkew`, `whenUnsatisfiable`, `DoNotSchedule`/`ScheduleAnyway`, `labelSelector` and `minDomains` are untested |
| nodename | yes (B3.3, P15-C, P16) |
| direct-node-assignment | yes (B3.3, P16) |
| schedulername | **NO** |
| custom-scheduler | **NO** |
| scheduling-policies | yes (B3.4, P17) |
| predicates | yes (B3.4, P17) |
| priorities | yes (B3.4, P17) |
| scheduling-profiles | **NO** — appears in B3.4's answer key only |
| scheduler-plugins | **NO** — appears in B3.4's answer key only |
| kubectl-get-nodes / kubectl-get-pods / kubectl-label / kubectl-taint | not tested — **correctly so.** The outline (Open Question #10) established that no command *line* is sourced in the cached snapshots, and Chapter 8 owns the command surface. Testing syntax here would be out of scope and unsourceable. Not a finding |

**Nine concepts introduced and never tested.** Three of them matter:

1. **`taint-toleration-matching` (the four rules + two wildcards).** The outline designated this the chapter's required `— Dead Reckoning` block — i.e. explicitly flagged as reference-grade material the reader is meant to hold. It gets a table, a marker, and zero retrieval. This is the largest single coverage gap in the chapter. One item closes it, and it discriminates well: *"A Pod has a toleration with `key: dedicated`, `operator: Exists`, and no `effect` specified. Which taints on a node does it tolerate?"* — A) only `dedicated` taints with `NoSchedule`; B) all taints with key `dedicated`, any value, any effect **(correct)**; C) all taints on the node regardless of key; D) none — `effect` is a required field.

2. **Topology spread constraint fields.** §5 states outright: *"for this exam you want to recognise them rather than compose them"* (draft-v1.md:683) — and then no question asks the reader to recognise anything. `whenUnsatisfiable`'s `DoNotSchedule`/`ScheduleAnyway` is the more costly omission, because §5 flags it as *"the fourth appearance of the same pair in this chapter"* and §7's Zenith turns on exactly that hard/soft recurrence. Fixing P14-D as recommended above closes this at zero budget cost.

3. **`tolerationSeconds`.** Currently the reader's only exposure is being told it's the *wrong* answer (P8-C). The 300-second automatic toleration for `not-ready`/`unreachable` is a memorable, exam-shaped fact taught at draft-v1.md:520 and never asked about. Candidate for absorbing one of the low-value items above, or for folding into the matching-rules item.

`schedulerName`, `custom-scheduler`, `scheduling-profiles` and `scheduler-plugins` are all §6 material, and §6 has only two Practice items (correct per the outline's allocation), both of which went to `nodeName` and the Predicates/Priorities mapping. Given §6's stated depth ceiling — the reader needs to know the seat is pluggable, not how to build a scheduler — leaving these untested is defensible. Recording them as gaps for the record, not recommending a budget change.

`pod-overhead` and the `Capacity`/`Allocatable` distinction are one-clause and two-sentence teachings respectively; leaving them untested is proportionate. Noting only that P3 and B1.4 both *hand* the reader "allocatable" in the stem, so the chapter's own practical rule — "do the arithmetic against Allocatable, not against the machine's total RAM" — is never actually exercised. If one edit is wanted, changing P3's stem from "32 GiB allocatable memory" to "32 GiB of RAM, of which 30 GiB is allocatable" makes the distinction load-bearing at the cost of one clause.
```

**The three things worth your attention:**

1. **Soundings answer 5 pre-spends the chapter's designated struggle item.** It states the permit-vs-attract distinction — §4's Fixed Point — in plain English, and Bearings #2 item 2 is explicitly built on the reader *not* knowing it. Stem is clean, so this isn't a spoiled pre-test; it's a spent surprise. One-sentence fix proposed.

2. **Two teaching blocks get zero retrieval:** the §4 taint-matching rules (the chapter's required Dead Reckoning block) and §5's topology-spread fields (which the draft itself frames as recognition-depth exam material). Both are closable — the spread-constraint gap by rewriting P14's weak fourth option, the matching-rules gap by one new item or by converting one of the four fabricated distractors.

3. **Budget, retrieval, interleaving and trap fidelity are all clean.** 40/40 exact, 21.9% retrieval against a 20% target, all three [B3] anchors in their designated sections, all four planned interleaving pairings present, all ten Exam Alert traps live as distractors, and no fabricated frequency claims anywhere. The remaining findings are five weak distractors, four imprecise grouped why-wrongs, and a correct-answer-is-longest pattern in 7 of 17 Practice items.
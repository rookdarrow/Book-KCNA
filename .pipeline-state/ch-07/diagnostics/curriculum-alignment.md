I am the `curriculum_alignment_audit` stage (orchestrator pid 7172); per the pipeline contract the orchestrator writes my stdout to `diagnostics/curriculum-alignment.md`, so I emit the document rather than writing the file myself.

Two things resolved before the audit: the stage prompt reported `draft-voice.md` unavailable, but the voice stage **did** complete (10:07) and writes **in place** — the voiced draft is `draft-v1.md` (1122 lines), with `draft-v1-prevoice.md` as the backup. I audited the real voiced draft. And the exam-objectives authority is `cncf-kcna-curriculum-pdf-2026-08-23.md`, which was not among the 20 snapshots passed to this stage; I read it from the corpus.

---

# Curriculum-Alignment Audit — KCNA Chapter 7

**Draft audited:** `.pipeline-state/ch-07/draft-v1.md` (voiced, 1122 lines, 2026-08-24T10:07)
**Objective authority:** `sources/cncf-kcna-curriculum-pdf-2026-08-23.md` + `sources/cncf-kcna-certification-page-2026-08-23.md`
**Objective decomposition:** `book-outline/domain-analysis.md` §D1.3 (13 concept rows) + `book-outline/arc-outline.md` § Chapter 7 *Covers* (7 further mechanisms)

**Numbering caveat, stated once.** CNCF publishes **four domain weights and twelve named competencies, with no numbering and no sub-competency weights** (`cncf-kcna-curriculum-pdf`, corroborated by the certification page). `D1.3` is a Lodestar convention, declared as such at `domain-analysis.md:33`. The `D1.3-NN` sub-IDs below are **this audit's** decomposition of that competency, derived from the two artifacts named above. They are an audit instrument, not a CNCF taxonomy, and should not leak into shipped text. The chapter's `Authored weight: 5%` line and its disclaimer (draft lines 4–6) handle this correctly and match the standing front-matter disclosure.

**Headline:** coverage is essentially complete. Of 20 auditable sub-objectives, **19 are covered and 1 is partial**. There are **no uncovered objectives**. All 44 `kb_tags.concepts` entries appear in the draft. The findings below are therefore depth and scope calls, not holes.

---

## Objectives the outline claims to cover

The outline claims exactly one competency: **D1.3 — Scheduling** (frontmatter `objectives: ["D1.3"]`, applied uniformly to all seven sections).

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.3-01 | Scheduling — assigning a newly-created, unbound Pod to a suitable node | YES (§1, L123) | appropriate |
| D1.3-02 | `kube-scheduler` — default scheduler, runs as part of the control plane, replaceable | YES (§1 L123; §6 L742) | appropriate |
| D1.3-03 | Feasible node | YES (§1 L123; §2 L201) | appropriate |
| D1.3-04 | Filtering (step 1); `PodFitsResources` checks available capacity | YES (§1 L129; §2 L201–221) | deep — justified |
| D1.3-05 | Scoring (step 2) — rank surviving nodes by the active scoring rules | YES (§1 L131) | shallow — source-bounded, see Depth |
| D1.3-06 | Binding — the scheduler notifying the API server of its node choice | YES (§1 L133; §6 L732–738) | deep — justified |
| D1.3-07 | Tie-breaking — equal scores broken **at random** | YES (§1 L177) | appropriate |
| D1.3-08 | Unschedulable — empty feasible list ⇒ Pod remains unscheduled (`Pending`) | YES (§2 L243–249) | deep — mandated [B3] anchor |
| D1.3-09 | **Scheduling factors** — individual *and collective* resource requirements; hardware/software/policy constraints; affinity and anti-affinity; **data locality**; **inter-workload interference**; **deadlines** | **PARTIAL** (§1/§2 cover 2 of 6; never presented as a list) | **shallow — 3 of 6 factors absent** |
| D1.3-10 | Scheduling Policies — Predicates (filtering) / Priorities (scoring) | YES (§6 L750, L755–758) | appropriate |
| D1.3-11 | Scheduling Profiles — plugins; `QueueSort`/`Filter`/`Score`/`Bind`/`Reserve`/`Permit`; multiple profiles | YES (§6 L751) | appropriate |
| D1.3-12 | Direct node assignment — the API permits naming a node at creation; unusual, special cases only | YES (§6 L714–726) | deep — justified |
| D1.3-13 | Pod scheduling is once-only; a Pod is never rescheduled to a different node | YES (§1 L185–191) | appropriate |
| D1.3-14 | Node labels — attached manually, plus the standard set Kubernetes populates | YES (§3 L328) | appropriate |
| D1.3-15 | `nodeSelector` | YES (§3 L343–345) | appropriate |
| D1.3-16 | Node affinity — required vs preferred; operator set; `IgnoredDuringExecution` | YES (§3 L351–370) | deep — **one item over ceiling** |
| D1.3-17 | Pod affinity / anti-affinity | YES (§5 L628–633) | appropriate |
| D1.3-18 | Taints and tolerations — `NoSchedule` / `PreferNoSchedule` / `NoExecute`, matching, built-in condition taints | YES (§4 L416–546) | deep — at ceiling |
| D1.3-19 | `nodeName` | YES (§6 L714–738) | deep — justified |
| D1.3-20 | Topology spread constraints | YES (§5 L675–700) | deep — **mildly over-covered** |

**One tagging discrepancy, low severity.** `kb_tags.commands` lists four commands; the draft exercises three (`kubectl get nodes --show-labels`, `kubectl label`, `kubectl taint` ×2). **`kubectl get pods` never appears** in any form. Either drop the tag or accept it as unexercised — it does not affect objective coverage, and G-7E already noted the bare form is only generically sourced.

---

## Objectives covered in the draft but NOT in the outline

Drift is modest and mostly authorized. Ranked by how much author attention each deserves.

**1. Node-affinity `weight` arithmetic — §3, L360. The one genuinely unauthorized expansion.**
The outline carries an explicit directive: *"⚠ **Do not teach affinity `weight` arithmetic** for preferred rules. Naming that preferred rules can be weighted is the ceiling."* The research manifest independently agreed (note 6: *"take the OR/AND rule if anything, skip the weight arithmetic"*). The draft states the **`between 1 and 100` range** and the **sum-added-to-other-scoring-functions mechanic**. Two sentences, self-disclaimed (*"You don't need the arithmetic for this exam"*), but it breaches a ceiling that two upstream stages set independently. See Recommended fixes — the correct trim is surgical, not a deletion.

**2. `kubectl` command lines ×3 — §3 L333–334, §4 L427–428 (plus L532 inline).**
Outline Open Question #10 recommended *"command **names** freely and command **lines** not at all,"* partly on scope grounds: **the `kubectl` command surface is D1.2 and belongs to Chapter 8** (`arc-outline.md` § Chapter 8 *Covers*; gap G1). The research manifest then relaxed this on sourcing grounds (note 3) and specifically endorsed **one** line — the trailing-minus taint removal — as *"the one genuinely worth a line."* The draft ships four. The taint pair earns its place (it makes a taint feel like a thing you put on and take off, exactly as the manifest argued). The `kubectl label` / `get nodes --show-labels` pair is the one that reaches into Chapter 8 without a teaching point that needs it — §3's argument is the *direction inversion*, which the command lines do not carry. **Author decision, not a defect.**

**3. Topology-spread depth beyond recognition — §5 L692, L696, L700.**
`arc-outline.md` lists this as a single Covers item ("topology spread"). The draft teaches four core fields in a table (correctly framed: *"for this exam you want to recognise them rather than compose them"*), then adds **`minDomains`**, **cluster-level default constraints**, and a **known limitation**. Sourced and accurate, but three items past recognition depth on the least-likely-to-be-tested item in D1.3. See Depth mismatches.

**4. Preemption and `PriorityClass` — §2 L239.** Not in the D1.3 concept table, but **explicitly authorized** by outline Open Question #3 and re-endorsed by manifest note 5. The draft honours the manifest's precision hazard exactly: it frames preemption as *the exception* and leaves §2's Fixed Point (the Pod waits, indefinitely) intact as the rule, which is what Chapter 13's anchor depends on. **No action.**

**5. Node `Capacity` / `Allocatable` — §2 L227–229.** D1.2-adjacent (primary source `k8s-docs-nodes` is a Chapter 8 source). Outline Open Question #8 authorized *"one or two sentences"*; the draft runs about five plus a practical-translation paragraph. It defers the reservation model to Chapter 8 cleanly and asserts no arithmetic (see G-7C below). Mild over-run on an explicitly bounded concession. **Acceptable; trim optional.**

**6. Minor sourced additions inside §4**, none of which the outline planned but all of which are cheap and useful: default tolerations at `tolerationSeconds=300` (L520), the eighth built-in taint `node.cloudprovider.kubernetes.io/uninitialized` (L516), and the multiple-taint filtering procedure (L494). **Keep all three.**

**7. `nodeSelectorTerms` OR / `matchExpressions` AND — §3 L364.** Reads as drift against the outline's stated ceiling, but is **authorized**: Open Question #6 named it *"the single most useful piece of the omitted set"* and the manifest confirmed A3 supplies both sentences verbatim. **No action.**

---

## Depth mismatches

An objective is "covered" if the draft addresses its learning outcome. Depth is judged against exam weight — and because **CNCF publishes no sub-weights**, the weight column below states the published signal (D1 = 44%) alongside the authored allocation (5% of book) and the section's share of the chapter's own 120-minute Attention Budget, which is the only fine-grained weight signal that exists here.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| D1.3-09 scheduling factors | D1 44% / core sourced D1.3 content; ~1 sentence to fix | 2 of 6 factors; never given as a list | **under-covered** |
| D1.3-05 Scoring | half the two-step spine; 6 of 9 exam-priority topics sit in §1–§2 | 3 sentences (§1) + the §7 collection | **source-bounded — OK, see note** |
| D1.3-16 affinity `weight` | outline ceiling: *"naming that preferred rules can be weighted"* | states `1`–`100` range **and** the sum mechanic | **over-covered — breaches an explicit ⚠ directive** |
| D1.3-20 topology spread | one line in arc-outline *Covers*; §5 = 18 min (15% of chapter) | 4 fields + `minDomains` + cluster defaults + a limitation | **over-covered (mild) — consider trimming** |
| D1.3-18 taint matching rules | outline-mandated Dead Reckoning block | 4-rule table + 2 wildcards + multi-taint procedure | **at ceiling — hold, but first trim candidate** |
| D1.3-18 taints overall | §4 = 25 min (21% of chapter), carries 2 of 9 exam-priority topics | deep | **OK** — densest discrete-recall block in the chapter; the *If you only have 15 minutes* route (L32) points here for the right reason |
| D1.3-04/-06/-08/-12/-19 | carry 6 of the chapter's 9 exam-priority topics | deep | **OK** |
| `kubectl` command surface | D1.2 — Chapter 8's, not this chapter's | 3–4 command lines | **mild cross-domain over-reach** |

**Note on D1.3-05 (Scoring), because it will otherwise read as an oversight.** Filtering gets a whole section (§2, 15 min); scoring gets three sentences. That asymmetry is **source-bounded, not a drafting failure** — the cached snapshots say almost nothing about scoring beyond "assigns a score based on the active scoring rules" and "highest ranking wins," and the draft uses everything available. §7 then does the real work by collecting the score side into a column. **No fix is warranted, and none is proposed.** This is precisely why the `weight` fix below is a trim rather than a deletion: the sum-feeds-the-score clause is one of the only concrete scoring facts in the chapter and it is load-bearing setup for §7's claim.

**Note on §4's size.** 21% of the chapter's time for 2 of 9 exam-priority topics looks disproportionate on arithmetic alone. It is not. The three effects, four matching rules, two wildcards, eight built-in taints and the DaemonSet callback are a large number of *discrete* facts, and discrete facts are what a multiple-choice recognition exam converts into questions. Depth here is correct; the internal trim candidate is named above.

---

## Gaps the research stage flagged

The research manifest (`research-manifest.md` § Gaps) listed five gaps, **G-7A through G-7E**, each with an explicit drafting instruction. All five are handled correctly, several of them to the letter.

| Gap | Manifest instruction | Draft handling | Verdict |
|---|---|---|---|
| **G-7A** — no standalone definition or formula for *skew* | *"Draft §5 using the `maxSkew` wording; do not compose a skew formula."* | L689 uses the `maxSkew` wording; **no formula anywhere in §5** | ✅ correct |
| **G-7B** — standard node label set not enumerated on the assign-pod-node page; A6's descriptions are `[PARTIAL]` | *"Cite the label keys freely, quote the descriptions only for `kubernetes.io/hostname`."* | L328 cites five keys; quotes a description for `kubernetes.io/hostname` **only** | ✅ correct, to the letter |
| **G-7C** — no text equivalent for capacity→allocatable arithmetic | *"§2 must not assert a formula."* | L227–229 names both words, states allocatable is what the scheduler treats as available, defers the reservation model to Ch 8. **No arithmetic relationship asserted** | ✅ correct |
| **G-7D** — per-taint `NodeCondition` cross-refs not captured | *"Cite DaemonSet for the effects, the taints page for the key names."* | Seven-row table cited to `k8s-docs-daemonset-2026-08-24`; the eighth key cited to `taints-tolerations-depth` | ✅ correct, to the letter |
| **G-7E** — bare `kubectl get pods` not separately sourced | immaterial under the restraint rule | Draft never uses it | ✅ moot |

**Three items the drafting stage surfaced that the manifest did not, all correctly in scope for a downstream stage:**

**(a) New gap — Pod-overhead mechanism (§2, `AUTHOR-REVIEW` at L235).** The draft correctly identifies that the cached RuntimeClass snapshot supports only *that* overhead exists so the scheduler accounts for the runtime's cost, **not** the mechanism (overhead added to the Pod's effective request). It held the prose to what the snapshot supports and named the fetch that would close it. **This is exactly right handling of an unsourced objective, and it is a genuinely new gap — record it as G-7F.** The objective (`pod-overhead`) is covered at the depth the sources permit; per Rule 3 this is a research-stage item, not an alignment failure.

**(b) ⚠ Stale currency flag — §6 `AUTHOR-REVIEW` at L762.** The comment asserts *"In current upstream Kubernetes the Policy model has been removed rather than deprecated"* and routes the question to the fact-accuracy stage. **The research manifest already investigated and closed this** (note 1): it re-fetched the live page, found it *character-identical* to the cached snapshot, and instructed *"Remove the 'currency risk' flag from the fact-accuracy stage's queue — I checked it, and there is nothing to reconcile."* The **prose** at L748–760 is the correct framing and needs no change. The **comment** repeats a claim the research stage disproved and will send a parallel stage on a closed errand. Correct it or delete it.

**(c) Manifest instruction not followed — §5 `🔭 Closer Look`, L673.** Manifest note 8: the causal explanation of *why* inter-Pod rules are expensive is *"authored reasoning, not sourced — the docs assert the cost without explaining the mechanism. Mark it as authored colour or drop the causal explanation and keep the assertion."* The draft states the mechanism (*"the answer for node-a depends on the contents of node-b"*) as plain prose, unmarked. The quoted caveat beside it is correctly sourced. **Sourcing lane, not curriculum — hand to the fact-accuracy stage rather than fixing here.**

**Blocking gaps from the arc outline, both now closed.** **G3** (requests/limits/QoS) was already closed at outline time. **G4** (taints/tolerations, affinity, `nodeSelector`, topology spread) was the outline's one live BLOCKING gap; the manifest closed it well past the planned fallback, and the draft's `AUTHOR-REVIEW` at L702 correctly records that **outline Open Question #2 can be closed** — §5 teaches the block properly rather than using the name-it-and-stop contingency. Verified: no topology-spread field name in the draft is unsourced.

---

## Recommended fixes

Concrete edits for the revision stage, ordered by priority. One per issue.

**1. Add the scheduling-factor list to §1 — the only real coverage gap.** *(D1.3-09, under-covered)*
Three of the six named factors — **data locality**, **inter-workload interference**, **deadlines** — appear **nowhere** in the draft (verified by search). The list is fully sourced twice over: `k8s-docs-kube-scheduler-2026-08-23` (*"individual and collective resource requirements, hardware / software / policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and so on"*) and `k8s-docs-cluster-architecture-2026-08-23`, which adds *deadlines*. This is exactly the shape a recognition exam converts into a "which of the following does the scheduler consider?" item, and the chapter currently cannot answer it. **Add one sentence to §1 after the feasible-node definition (≈L123), naming the factors as a list** and noting that this chapter teaches the two the reader can control. Cheapest high-value fix in the audit.

**2. Trim the affinity `weight` passage to the outline ceiling — §3, L360.** *(D1.3-16, over-covered)*
Cut **`between 1 and 100`**. Keep the rest. The numeric range is the item both the outline and the manifest excluded and it carries no pedagogical load; the sum-feeds-the-score clause and the *"preferred rules land in the **scoring** step"* pointer are load-bearing §7 setup and are among the chapter's only concrete scoring facts (see the D1.3-05 note above). Suggested: *"For preferred rules you can attach a weight to each instance, and those weights feed the node's score alongside the other scoring functions. You don't need the arithmetic for this exam. You do need to notice where preferred rules land: in the **scoring** step, not the filtering step."*

**3. Correct or delete the stale currency comment — §6, L762.** *(gap-handling)*
The research stage verified the live kube-scheduler page is character-identical to the cached snapshot and explicitly closed this. Replace the comment's premise with that finding, or delete it. **Do not change the prose at L748–760** — teaching Predicates/Priorities as *older names for the two steps* is the framing both upstream stages endorsed and it is true under every reading.

**4. Trim two items from §5's topology-spread block.** *(D1.3-20, mildly over-covered)*
Drop **`minDomains`** (L692) and **cluster-level default constraints** (L696). Keep the four-field table, the `whenUnsatisfiable` → required/preferred recognition beat at L694 (which is direct §7 setup and does real work), and the scale-down limitation at L700 (cheap, and it reinforces the chapter's "scheduling-time decision, not a standing invariant" spine). That lands the block at recognition depth, matching the single-line weight the arc outline gives it, without touching anything §7 depends on.

**5. Author decision — the `kubectl label` / `get nodes --show-labels` pair, §3 L333–334.**
Not a defect; a scope call the outline and the manifest split on. **Keep the `kubectl taint` pair** (§4) — manifest-endorsed, and the trailing-minus form earns its line. **Consider dropping the §3 pair**, because Chapter 8 owns the `kubectl` surface (D1.2, gap G1) and §3's teaching point is the direction inversion, which the commands do not carry. If they stay, nothing downstream breaks.

**6. Optional, low priority — tighten §2's Capacity/Allocatable block (L227–229) toward the one-to-two sentences Open Question #8 authorized**, and either drop `kubectl-get-pods` from `kb_tags.commands` or exercise it. Neither affects objective coverage.

**Explicitly not recommended, so the revision stage does not "fix" them:** §4's matching-rules table (outline-mandated Dead Reckoning content, at ceiling but correct); the preemption clause (authorized, and its framing protects Chapter 13's anchor); the `nodeSelectorTerms` OR/AND rule (authorized by Open Question #6 and the manifest); §5's `🔭 Closer Look` (a sourcing question for the fact-accuracy stage, not a curriculum one). The chapter also holds every one of the thirteen out-of-scope boundaries listed in outline Open Question #13 — `cordon`/`drain` are named nowhere, Cluster Autoscaler is named nowhere, and the four-socket extension synthesis is left to Chapter 17. The three load-bearing restraints [B3] flagged are intact.
I have everything I need. Emitting the audit document (the orchestrator captures stdout to `diagnostics/curriculum-alignment.md`).

---

I am the `curriculum_alignment_audit` stage (orchestrator pid 35120); per the pipeline contract the orchestrator writes my stdout to `diagnostics/curriculum-alignment.md`, so I emit the document rather than writing the file myself.

Three things resolved before the audit. **(1)** The stage prompt's draft was reconstructed from `.draft-v1.md.progress.log` because stdout capture kept only the final assistant message. That reconstruction has since been written to disk: `draft-v1.md` is 1254 lines, voiced, and **complete** — all nine sections, all six figure anchors, and every required structural element are present. I audited the file, and all line citations below are against it. **(2)** The exam-objectives authority is `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`, which was not among the 21 snapshots passed to this stage; I read it from the corpus, corroborated by `lf-kcna-exam-page-2026-08-23.md`. **(3)** The structural stage's one FAIL (line 392, "ASCII diagram without preceding figure anchor") is the `maxSurge`/`maxUnavailable` **arithmetic** fenced block, not an unanchored figure — all six planned figures are anchored (L137, L406, L431, L618, L714, L899). No figure is missing, so there is no coverage consequence.

---

# Curriculum-Alignment Audit — KCNA Chapter 6

**Draft audited:** `.pipeline-state/ch-06/draft-v1.md` (voiced, 1254 lines)
**Objective authority:** `sources/cncf-kcna-curriculum-pdf-2026-08-23.md` + `sources/lf-kcna-exam-page-2026-08-23.md`
**Objective decomposition:** `book-outline/domain-analysis.md` § D1.1 (workload-resource slice) + `book-outline/arc-outline.md` § Chapter 6 *Covers*

**Numbering caveat, stated once.** CNCF publishes **four domain weights and twelve named competencies, with no numbering and no sub-competency weights** (`cncf-kcna-curriculum-pdf`, corroborated verbatim by the LF exam page). `D1.1` is a Lodestar convention, declared as such at `domain-analysis.md:33`. The `D1.1-NN` sub-IDs below are **this audit's** decomposition, derived from the two artifacts named above. They are an audit instrument, not a CNCF taxonomy, and must not leak into shipped text. The chapter's metadata line (L5) and its `AUTHOR-REVIEW` at L7 handle the disclosure correctly and flag it for phrasing-match against Chapters 2–5 — that flag should stay open.

**Headline:** coverage is near-complete and the chapter's scope discipline is the strongest in Part II so far. Of **36 auditable sub-objectives, 35 are covered and 1 is absent**. There are no partials. Every one of the eleven out-of-scope boundaries the outline set is held — `concurrencyPolicy`, `parallelism`, `backoffLimit`, Indexed Jobs, job-history limits, TTL, proportional scaling, `--cascade=orphan`, finalizers, OLM/Kubebuilder, and Knative/Argo-by-name all return **zero** hits. Blue/green, canary and A/B appear exactly once, inside the single authorized forward cross-bearing (L469). The findings below are depth and boundary calls, not holes.

---

## Objectives the outline claims to cover

The outline claims exactly one competency: **D1.1 — Kubernetes Core Concepts** (frontmatter `objectives: ["D1.1"]`, applied uniformly to all nine sections).

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.1-01 | Workload resource — you don't manage Pods directly; the resource configures a controller | YES (§1 L127) | appropriate |
| D1.1-02 | Deployment — declarative updates for Pods *and ReplicaSets* | YES (§1 L131) | deep — justified |
| D1.1-03 | ReplicaSet — maintains a stable set of replica Pods | YES (§1 L133; §2 L195) | deep — justified |
| D1.1-04 | Ownership chain Deployment → ReplicaSet → Pod, and which layer holds what | YES (§1 L165 + fig01 L137) | deep — justified |
| D1.1-05 | Pod template (`.spec.template`), same schema as a Pod, nested | YES (§1 L179) | appropriate |
| D1.1-06 | ReplicationController — legacy, superseded | YES (§1 L185) | mild over-run — see Depth |
| D1.1-07 | The control loop instantiated — desired vs current, replacement not recovery | YES (§2 L195–215) | appropriate |
| D1.1-08 | `.spec.replicas` / desired replica count (on both objects) | YES (§1 L169–175; §2) | deep — justified |
| D1.1-09 | Manual horizontal scaling / `kubectl scale` | YES (§2 L231) | appropriate |
| D1.1-10 | HorizontalPodAutoscaler — concept only | YES (§2 L239) | appropriate — at ceiling |
| D1.1-11 | Label selector as the ReplicaSet→Pod join; `matchLabels` / `matchExpressions` | YES (§3 L256) | appropriate |
| D1.1-12 | Selector–template agreement; the API **rejects** a mismatch | YES (§3 L262–268) | deep — justified |
| D1.1-13 | Owner references — a mechanism distinct from selection | YES (§3 L274–276) | appropriate |
| D1.1-14 | Cascading deletion (background is the default) | YES (§3 L278) | appropriate |
| D1.1-15 | Controller adoption of bare Pods; immediate acquisition then termination | YES (§3 L284–286) | appropriate |
| D1.1-16 | **Orphaning** — dependents left behind when an owner is deleted / a selector is mutated | **NO** | **—** |
| D1.1-17 | Overlapping selectors as a hazard | YES (§3 L288–292) | appropriate — framing partly unsourced |
| D1.1-18 | Deployment strategy — `RollingUpdate` is the default; `Recreate` kills all first | YES (§4 L418, L429, L451) | deep — justified |
| D1.1-19 | `maxSurge` / `maxUnavailable`, 25% defaults, **asymmetric rounding** | YES (§4 L392, L406, L451) | deep — justified; salience gap, see Depth |
| D1.1-20 | `minReadySeconds` / readiness-gated availability | YES (§4 L457) | appropriate |
| D1.1-21 | Stuck rollout; `progressDeadlineSeconds` as the signal, not a tunable | YES (§4 L465–467) | appropriate |
| D1.1-22 | Revision rule — created **iff** `.spec.template` changes | YES (§5 L479, L483) | deep — justified |
| D1.1-23 | `kubectl rollout` verb surface (all six subcommands) | YES (§5 L502) | appropriate |
| D1.1-24 | Rollback semantics — restore a template, run the same update backwards | YES (§5 L519–522) | deep — justified |
| D1.1-25 | `revisionHistoryLimit`, default 10; `0` removes undo | YES (§5 L512) | appropriate |
| D1.1-26 | StatefulSet — Pods created from the same spec but **not interchangeable** | YES (§6 L610, L644) | appropriate |
| D1.1-27 | Stable Pod identity — ordinal, `$(name)-$(ordinal)`, sticky across rescheduling | YES (§6 L612) | over-covered (mild) |
| D1.1-28 | StatefulSet stable storage — one PVC per volumeClaimTemplate | YES (§6 L614, L662) | **over-covered — crosses into Ch 11** |
| D1.1-29 | DaemonSet — one Pod per eligible node, added as nodes join | YES (§7 L680, L739) | appropriate |
| D1.1-30 | Job — runs to completion once | YES (§7 L694) | appropriate |
| D1.1-31 | CronJob — creates Jobs on a schedule; Cron syntax | YES (§7 L704–706) | appropriate |
| D1.1-32 | The workload-resource decision (six resources, four questions) | YES (§7 fig04 L714, L745) | deep — justified |
| D1.1-33 | Custom resource; dynamic registration; identical `kubectl` access | YES (§8 L773) | appropriate |
| D1.1-34 | CustomResourceDefinition — API serves and stores it for you | YES (§8 L779) | appropriate |
| D1.1-35 | Custom controller → true declarative API (vs imperative) | YES (§8 L789, L793) | appropriate |
| D1.1-36 | Operator pattern; the operator's own controller runs as a Deployment | YES (§8 L803, L820) | appropriate |

**Two unexercised concept tags, both low severity and neither a coverage gap.**
`podtemplatespec` — the string "PodTemplateSpec" appears **nowhere**; the draft consistently says "Pod template," which is the better reader-facing term and matches the sources. `vertical-scaling` — the only occurrence of "vertical" is *"a vertical autoscaler that isn't shipped by default"* (L799), which is an instance of the object-without-component pattern, not a horizontal-vs-vertical contrast. That omission is **correct**: outline Open Question #4 explicitly recommended "no mention of vertical scaling at all," and the draft followed it. In both cases the fix is to drop the tag, not to add the content.

---

## Objectives covered in the draft but NOT in the outline

Drift is small, almost entirely sourced, and mostly improves on the plan. Ranked by how much author attention each deserves.

**1. StatefulSet storage-lifecycle facts — §6, L662. The one genuinely unauthorized expansion, and the research stage predicted it.**
The outline's §6 carries an explicit directive: *"⚠ **Do not teach PersistentVolume, PersistentVolumeClaim, StorageClass, access modes, or provisioning.** Every one of them is Chapter 11's."* Naming those terms to *declare the open loop* is mandated and correct — that part is fine. But L662 then delivers two **substantive** Chapter 11 facts: that the storage must be provisioned by a PV provisioner per the requested storage class or pre-provisioned by an admin, and that deleting or scaling down a StatefulSet does not delete the volumes. The research manifest anticipated exactly this and advised against it (note 8): *"The second is arguably Chapter 11's… Use it in the figure's design brief even if the prose holds it back."* The draft put it in the prose. See Recommended fixes — the trim is surgical.

**2. `.spec.replicas` exists on both the Deployment and the ReplicaSet — §1, L169–175. Unplanned, and an improvement.**
The outline's Fixed Point simplifies to "the Deployment holds the template, the ReplicaSet holds the count." The draft states the simplification, then immediately complicates it correctly: both objects carry the field, the Deployment is the author of the second copy, and the ReplicaSet is where the count is *enforced*. Sourced twice (A1 + A7). This makes Bearings #1 item 1's answer key sharper, not muddier, and the answer key at L340 handles the nuance explicitly. **Keep.**

**3. Job `restartPolicy` restricted to `Never` or `OnFailure` — §7, L700.** Not in the outline's §7 concept list. Sourced, one sentence, and the draft draws the right inference unaided (*"a Pod that is always restarted can never complete"*). Cheap and it reinforces run-to-completion. **Keep.**

**4. CronJob idempotency warning — §7, L708.** Not planned. Sourced verbatim (*"the Jobs that you define should be idempotent"*) and it is the single most operationally consequential CronJob fact in the snapshot. **Keep.**

**5. `.spec.timeZone` and `.spec.jobTemplate` — §7, L706.** Two field names beyond the planned `cronjob-schedule`. `jobTemplate` earns its place — the draft ties it back to §1's nesting move, which is a real structural callback. `timeZone` is the marginal one. **Author decision; both are cheap.**

**6. ReplicationController's set-based-selector distinction — §1, L185.** The outline budgeted "one clause"; the draft spends four sentences. The extra content is the one substantive difference between RC and ReplicaSet, and it retroactively justifies §3's `matchExpressions`. **Acceptable; optional trim.**

**7. §8's `🔭 Closer Look` on API aggregation — L830.** The outline planned "one sentence; Chapter 17 owns extension points." The draft gives roughly four, including the published choose-between rubric. It closes by self-limiting (*"knowing that both exist is enough"*), which contains the damage. **Mild over-run; acceptable.**

**Explicitly authorized, listed so the revision stage does not mistake them for drift:** StatefulSet ordering guarantees at L616 (outline Open Question #5 authorized this conditionally at one sentence; the draft delivers exactly one sentence); the naming of VPA-in-all-but-name at L799 (the outline's §8 marker plan lists "VPA not shipped by default" as one of the four instances of the recurring pattern, and the draft is *more* restrained than planned — it avoids the acronym); the blue/green–canary–A/B pointer at L469 (the single forward cross-bearing the outline permits).

---

## Depth mismatches

An objective is "covered" if the draft addresses its learning outcome. Depth is judged against exam weight — and because **CNCF publishes no sub-weights**, the weight column states the published signal (D1 = 44%) alongside the authored allocation (6% of book) and the section's share of the chapter's own Attention Budget, which is the only fine-grained weight signal that exists here.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| D1.1-16 orphaning | sourced twice over; ~1 clause to fix | absent | **under-covered** |
| D1.1-28 StatefulSet storage | Ch 11 owns it; outline ⚠ forbids teaching it | 2 substantive Ch-11 facts in prose (L662) | **over-covered — crosses a chapter boundary** |
| D1.1-19 maxSurge/maxUnavailable | exam-priority #6; the chapter's densest transposable pair | deep and numerically correct, but **no ★ Fixed Point in §4** | covered; **salience gap** |
| D1.1-27 stable Pod identity | outline: "if included, one sentence" | ~3 sentences (L612) | over-covered (mild) |
| D1.1-06 ReplicationController | outline: "one clause" | 4 sentences (L185) | over-covered (mild) |
| D1.1-32 decision tree | exam-priority #1; defuses traps #21/#22/#23 together | deep, correct question order | **OK** |
| D1.1-04 ownership chain | exam-priority #5; retrieved by Ch 7, 9, 14, 15 | deep | **OK** |
| D1.1-22/-24 revision & rollback | exam-priority #7; Ch 14 needs the contrast | deep, mechanism stated explicitly | **OK** |
| D1.1-10 HPA | Ch 13 and Ch 17 own the landscape | 1 short paragraph + 3 forward pointers | **OK — at ceiling** |
| D1.1-33…-36 CRD / operator | §8 = 12 min; 1 of 8 exam-priority topics | appropriate; no OLM, no Kubebuilder | **OK** |

**Note on §6's size, because the arithmetic looks wrong until you check it.** §6 is budgeted **9 minutes** (7th of nine sections) but runs **74 lines** (4th of nine) — longer than §3 (53) and §5 (66), both of which are budgeted higher. The excess is concentrated in exactly three places: L612 (identity, mild), L614 (storage mechanism, mild), and L662 (the Chapter 11 facts, the real one). Trimming L662 alone brings the section back inside its budget without touching the Fixed Point, the Snag, the figure, or the Extended Analogy. The analogy at L652–656 is long but it is *shorter than its section*, which is the test the outline set for it; it is a theming-density call rather than a curriculum one and I have not costed it here.

**Note on §7's size, which is not a mismatch.** §7 is budgeted 10 minutes and runs 89 lines, second-longest in the chapter. That is correct: it carries **three of the eight exam-priority topics** (#1, #3, #4) plus the decision tree, and three resources each needing a defining property. Length here is load-bearing. **No action.**

**Note on the §4 salience gap, because it is the one finding that is easy to dismiss.** §4 has no `★ Fixed Point`. The outline planned seven (§1, §3, §4, §5, §6, §7, §8) in its section plans while its chapter-type table said six (§1, §3, §4, §5, §6, §7) — the outline is internally inconsistent, so the draft cannot be faulted for landing on six. But the six it shipped are at §1, §3, §5, §6, §7, §8, which means **the one section the outline itself labels "the chapter's densest block" and the source of exam-priority topic #6 is the section without a must-memorize marker.** The content is all present and correct — the Dead Reckoning block at L451 states every field, default and rounding rule flat, and the mnemonic at L427 handles the transposition. This is a retrieval-handle gap, not a content gap, and it overlaps the structural stage's lane (the linter's min-1 rule is satisfied, so it will not fire). Low priority, cheap to fix.

---

## Gaps the research stage flagged

The research manifest listed four gaps, **G-6A through G-6D**, each with a drafting instruction. **All four are handled correctly, three of them to the letter.** The manifest's eleven author notes are separately relevant; nine are followed, two are not.

| Gap | Manifest instruction | Draft handling | Verdict |
|---|---|---|---|
| **G-6A** — "a DaemonSet has no `replicas` field" is stated in no fetched source | *"Phrase the Fixed Point as the count is a consequence of how many nodes match… drop the 'has no replicas field' clause."* | L739 Fixed Point reads *"The count is a consequence of the cluster, not a setting."* The uncited negative appears **nowhere**. Corroborated at L688 with the HPA page's *"does not apply to objects that can't be scaled (for example: a DaemonSet)."* `AUTHOR-REVIEW` at L690 names the fetch that would license the stronger form | ✅ correct, to the letter |
| **G-6B** — "Alternatives to DaemonSet / ReplicationController" truncated | *"Neither is needed; the ReplicaSet page's Alternatives section supplies the contrasts."* | L735 uses the ReplicaSet page's Alternatives framing for all three contrasts; L185 uses it for RC-vs-ReplicaSet | ✅ correct |
| **G-6C** — Job "Job patterns" prose not captured | out of scope | Draft omits entirely; no parallelism, completions, or backoff anywhere | ✅ moot |
| **G-6D** — Job↔Pod-phase connection not separately sourced; **precision hazard** | *"The draft should not write 'the Job reaches `Succeeded`.'"* | L698 attributes the phases to **the Pod** (*"all containers in the Pod terminated in success"*); Q16 asks about *"a Job's Pod"*; the draft never mentions Job *conditions* at all | ✅ correct — hazard avoided cleanly |

**Manifest note 1 — the 12→13 correction. Applied everywhere, and this is the audit's best news.** The outline stated the ten-replica ceiling as **12** in four places (§4's walkthrough, `ch06-fig02`'s design brief, Bearings #2 item 1's answer key, and the transposition trap). The manifest caught it: `maxSurge` rounds **up** (2.5 → 3), so the ceiling is **13**. The draft carries 13 consistently at L392 (the arithmetic block), L406 (fig02's labels and axis annotations), Bearings #2 item 1 (answer B, with 12 preserved as the rounding distractor), Q7 (answer C), and Q8's independent six-replica case (8 and 5, correctly derived). The `AUTHOR-REVIEW` at L398 flags the outline's stale number so it does not propagate to The Lodestar. **No residual instances of 12-as-ceiling exist.** This is exactly what the research→draft handoff is for.

**Manifest notes 2, 3, 5, 6, 9, 10 — all followed.** `minReadySeconds` at L457 and `progressDeadlineSeconds` at L467 land as the manifest specified (the latter as *the mechanism behind the signal*, not a tunable), and Bearings #2 item 4 keys against the source's own "Readiness probe failures" line. §3 teaches the **API rejection** with the runaway as its *reason* rather than as an observable outcome (L262–268), exactly per note 6, with an `AUTHOR-REVIEW` at L270 and Bearings #1 item 3 rewritten to match. Bare-Pod adoption is used (note 5). The HPA gets one paragraph (note 9). The `kubectl rollout` table at L502 lists **all six** subcommands including `restart`, which note 10 asked for specifically so the set is not presented as complete-while-short.

**Two manifest instructions not followed.**

**(a) Note 7 — the overlapping-selector framing.** The manifest was precise: the *"neither one reports an error, it looks like flapping"* observation is **not in any fetched source**, and the fix was to *"mark it as authored colour, or recast the Snag around adoption and orphaning, both of which are documented."* The draft took neither option cleanly. It **did** add adoption (L284–286, well sourced, and a genuine improvement). But the flapping narrative survives unmarked in the `Logbook Entry` at L288–292, and **orphaning is absent from the chapter entirely** — which is simultaneously the source of the one uncovered objective above. The sourcing half of this belongs to the fact-accuracy stage; the missing-concept half is mine and is Recommended fix #1.

**(b) Note 8 — StatefulSet storage.** Covered as drift item #1 above. The manifest advised the PVC-not-deleted fact for the **figure design brief**, not the prose. It is in the prose at L662.

**One new gap surfaced by the drafting stage — record as G-6E.** The `AUTHOR-REVIEW` at L690 correctly identifies that the stronger claim (*a DaemonSet has no `replicas` field*) would need the DaemonSet API reference fetched, and asks whether the author wants it. The objective is covered at the depth the sources permit; **per Rule 3 this is a research-stage item, not an alignment failure.** Same shape as ch-07's G-7F.

**Blocking gaps from the arc outline, both closed.** **G8** (update mechanics, rollout, rollback) and **G10** (CRDs, operator pattern) were the outline's two named blocking gaps; both were already closed at outline time and the draft teaches both at full planned depth. The outline's own Open Question #2 opened five *new* blocking gaps (ReplicaSet, garbage collection, StatefulSet, DaemonSet, Job/CronJob pages) — **all five closed** by snapshots A1–A6, and every section that depended on them is now primary-sourced rather than running on secondary mentions.

**Two editorial escalations, correctly handled and still open.** The `AUTHOR-REVIEW` comments at L670 and L765 escalate outline Open Question #1's published cross-bearing collisions — `chapter-01:435` points at "Ch 6 §3 — StatefulSets and stable identity" (actually §6) and `chapter-02:600` points at "Ch 6 §3 — CRDs" (actually §8). Both correctly note the fix is a one-token edit in shipped text and is **not fixable from inside this draft**. These are editorial, not curriculum, but they were flagged BLOCKING upstream and must not be lost — they need a Chapter 1 and Chapter 2 edit before ship.

---

## Recommended fixes

Concrete edits for the revision stage, ordered by priority. One per issue.

**1. Add orphaning to §3 — the only coverage gap.** *(D1.1-16, under-covered)*
The word appears nowhere in the chapter, yet `orphaning` is tagged in `kb_tags.concepts`, listed in the outline's §3 concepts-introduced, sourced twice (`k8s-docs-garbage-collection-2026-08-24` has a dedicated *"Orphaned dependents"* section: *"When Kubernetes deletes an owner object, the dependents left behind are called orphan objects"*; `k8s-docs-daemonset-2026-08-24` supplies *"Mutating the pod selector can lead to the unintentional orphaning of Pods"*), and named by manifest note 7 as one of the two documented replacements for the unsourced flapping narrative. It is also the natural complement to cascading deletion, which §3 already teaches — the two are the same mechanism's two outcomes. **Add one clause to §3 after the cascading-deletion sentence at L278**, naming orphans as what dependents are called when they survive their owner, and — if the Logbook Entry is recast per fix #2 — use the DaemonSet selector-mutation line as its concrete cause. Cheapest fix in the audit and it closes the last open row in the table.

**2. Recast or mark the Logbook Entry at §3, L288–292.** *(sourcing lane, but it interlocks with fix #1)*
The flapping-with-no-error narrative is a reasonable practitioner observation that no fetched source states. Manifest note 7 gave two acceptable exits: mark it as authored colour, or rebuild it on adoption and orphaning. **The second is better here**, because it costs nothing — §3 already teaches adoption at L284, and fix #1 adds orphaning — and because it converts an unsourced anecdote into two documented failure modes. If the author prefers to keep the flapping narrative for its practitioner texture, mark it as authored and hand the marking to the fact-accuracy stage. **Do not simply delete it**; the section needs a consequence for overlapping selectors and this is currently the only one.

**3. Trim the two Chapter 11 facts from §6, L662.** *(D1.1-28, over-covered — the boundary crossing)*
Cut the sentence beginning *"The documentation itself flags two consequences you will want when you get there…"* through the end of that sentence. **Keep** the preceding sentence (the deliberate-open-loop declaration naming PersistentVolume, PersistentVolumeClaim, StorageClass and access modes as Chapter 11's), which the outline mandates and which is the honest move the section is built around. Keep the Ch 11 cross-bearing at L664. Per manifest note 8, the volumes-survive-deletion fact should go into `ch06-fig05`'s **design brief** — where it is genuinely useful, because it is the cleanest evidence for the figure's stated requirement that storage belongs to the *identity* rather than the Pod — rather than into the reader's prose. This single trim also brings §6 back inside its 9-minute budget.

**4. Give §4 a `★ Fixed Point`.** *(D1.1-19, salience gap)*
The outline drafted the text already: *"`RollingUpdate` is the default; `maxSurge` and `maxUnavailable` both default to 25%; `Recreate` kills all old Pods first."* Add it after the `Recreate` contrast (≈L429) or after the Dead Reckoning block (≈L451). Nothing needs rewriting — the content is present, correct, and numerically verified; it simply has no must-memorize handle in the section the outline itself calls the chapter's densest, and which supplies exam-priority topic #6. Consider extending the Fixed Point with the asymmetric-rounding rule (surge up, unavailable down), which is the actual discriminator between the two names and is what Q7 and Q8 both test.

**5. Optional trims, in descending order of value.** §6 L612 — the ordinal paragraph can lose its third sentence (the identity-sticks-across-rescheduling clause is restated in the Fixed Point at L648) to reach the outline's one-sentence ceiling. §1 L185 — the ReplicationController passage can drop to the planned one clause, though the set-based-selector distinction is the one part worth keeping. §7 L706 — `.spec.timeZone` is the most droppable field name in the chapter if space is wanted; `.spec.jobTemplate` should stay, because it pays off §1's nesting move. §8 L830 — the API-aggregation Closer Look can shed the choose-between rubric and keep its first and last sentences.

**6. Tagging hygiene, no reader-visible change.** Drop `podtemplatespec` from `kb_tags.concepts` (the draft correctly says "Pod template" throughout) and drop `vertical-scaling` (its absence is the outline's own Open Question #4 recommendation, correctly followed — the tag is the error, not the omission). Neither affects objective coverage.

**Explicitly not recommended, so the revision stage does not "fix" them:** the `replicas`-on-both-objects nuance at L169–175 (unplanned but sourced and better than the plan); StatefulSet ordering guarantees at L616 (authorized at one sentence, delivered at one sentence); the Job `restartPolicy` restriction at L700 and the CronJob idempotency warning at L708 (both cheap, sourced, and operationally load-bearing); the VPA reference at L799 (the outline's own marker plan authorizes it, and the draft is more restrained than planned); the blue/green pointer at L469 (the single permitted forward cross-bearing, teaching nothing); and §7's length (three exam-priority topics justify it). The structural stage's FAIL at L392 is a linter false positive on a non-figure fenced block — **do not add a figure anchor to the arithmetic**; all six planned figures are present and correctly anchored.
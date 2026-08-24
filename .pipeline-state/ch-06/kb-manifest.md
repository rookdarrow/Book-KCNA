I have what I need. Two things I verified that change the picture the integration report handed me, both recorded in the manifest below.

# Knowledge-Base Manifest — KCNA Chapter 6

## ⚠ Read first — two scope facts

**1. `Book-KCNA/knowledge-base/` does not exist on disk.** Not gitignored, not stale, absent. Chapters 1, 3, 4, and 5 each emitted a stage-14 manifest (66 KB / 104 KB / 108 KB / 130 KB) containing `=== WRITE ===` and `=== APPEND ===` blocks for `glossary.md`, `objective-coverage.md`, `retrieval-log.md`, and 29 concept shards. **None of them landed.** Every write below is therefore a *first* write against a path that has no predecessor content, even though four chapters of predecessor content have been authored and are recoverable from the prior manifests. Stage 14's stated purpose — "so subsequent chapters see the latest concept definitions" — has not been met for any chapter of this book. This is an orchestrator write-back defect, not a content defect, and it outranks everything else here.

**2. Definitions are inherited from `draft-v1-prevoice.md`, not from this stage's input.** The input is the truncated 26 KB tail; it contains no body prose and therefore no definitions. Rule 5 (inherit exact definitions, never paraphrase) cannot be satisfied from it. I verified `draft-v1-prevoice.md` is intact (1,213 lines, opens `# Chapter 6: Fleets, Not Vessels`, all nine sections present) and took every verbatim quote from it. Voice-swap alters register, not definitions, so this is the correct source. Where the revision stage sharpened a *factual* wording (Job `Complete`), I take the revision's form and say so.

---

## Correction to the integration report — the figure anchor is not a mismatch

Integration reports the Zenith anchor as diverging: draft `ch06-zenith-control-loop-instantiated` vs `image-specs.md` `ch06-fig06-control-loop-instantiated`, marked ❌, escalated as an author decision.

`image-specs.md:631` reads `anchor_id: ch06-zenith-control-loop-instantiated`. **The join key does not diverge.** `fig06` appears only as a *suggested correction* in three prose notes (lines 65, 575, 628), explicitly marked "pending author review." Integration read the suggestion as the field value.

And the suggestion should be struck, not adopted. Chapter 5's manifest already settled this exact class: `arc-outline.md:156` prescribes `ch06-zenith-control-loop-instantiated` by name, `arc-outline` uses `chNN-zenith-<slug>` for every chapter's Zenith, and **Chapter 2 already shipped `ch02-zenith-standard-crate` in published prose.** Renaming would make Chapter 6 the second deviating chapter against a pattern set for eighteen. Recorded below as closed-not-a-defect, matching the two identical rulings Chapter 5 made.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**58 terms contributed** — 52 defined verbatim, 4 reserved forward, 2 outline-tagged but absent from the text. Full rows in the append block; summary of the load-bearing ones:

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **workload resource** | "you use workload resources that manage a set of Pods on your behalf, and those resources configure controllers that make sure the right number of the right kind of Pod are running, to match the state you specified" | Chapter 6 §1 |
| **Deployment** | "manages a set of Pods to run an application workload — usually one that doesn't maintain state — and it provides declarative updates for Pods *and ReplicaSets*" | Chapter 6 §1 |
| **ReplicaSet** | "maintain a stable set of replica Pods running at any given time" | Chapter 6 §1–§2 |
| **Pod template** | "lives inside the workload resource as `.spec.template`, a pod template with exactly the same schema as a Pod, except that it's nested and has no `apiVersion` or `kind` of its own" | Chapter 6 §1 |
| **owner reference** | "the Pods' `metadata.ownerReferences` field, which specifies what resource the current object is owned by" | Chapter 6 §3 |
| **adoption** | "if there's a Pod that has no owner reference, or whose owner reference is not a controller, and it matches a ReplicaSet's selector, it will be immediately acquired by that ReplicaSet" | Chapter 6 §3 |
| **`maxSurge`** | "the maximum number of Pods that can be created *over* the desired number of Pods… calculated from the percentage by *rounding up*. The default is 25%" | Chapter 6 §4 |
| **`maxUnavailable`** | "the maximum number of Pods that can be unavailable during the update process… calculated from the percentage by *rounding down*. The default is 25%" | Chapter 6 §4 |
| **revision** | "a new revision is created **if and only if** the Deployment's Pod template (`.spec.template`) is changed. Other updates, such as scaling the Deployment, do not create a Deployment revision" | Chapter 6 §5 |
| **StatefulSet** | "runs a group of Pods and maintains a sticky identity for each of them — useful for applications that need persistent storage or a stable, unique network identity" | Chapter 6 §6 |
| **interchangeability** | "any Pod in the Deployment is interchangeable and can be replaced if needed" — the property that decides Deployment vs StatefulSet | Chapter 6 §6 |
| **DaemonSet** | "defines Pods that provide facilities local to nodes. Every time you add a node to your cluster that matches the specification in a DaemonSet, the control plane schedules a Pod for that DaemonSet onto the new node" | Chapter 6 §7 |
| **Job** | "represents a one-off task that runs to completion and then stops… continues to retry execution until a specified number of them successfully terminate" | Chapter 6 §7 |
| **CronJob** | "creates Jobs on a repeating schedule" | Chapter 6 §7 |
| **custom resource** | "an extension of the Kubernetes API that is not necessarily available in a default Kubernetes installation; it represents a customization of a particular Kubernetes installation" | Chapter 6 §8 |
| **operator pattern** | "combines custom resources and custom controllers" | Chapter 6 §8 |
| *(42 further defined rows — full text in the append block)* | | |

### Three status corrections to rows this chapter does *not* own

- **`label-selector` / `matchLabels` / `matchExpressions`** — the outline's `kb_tags.concepts` claims these are introduced at Ch 6 §3. They are not. **Chapter 4 §5 introduces, sources, and Fixed-Points them.** Chapter 6 §3 *applies* them and adds a consequence. Glossary cross-references must read **(Chapter 4)**. Do not let a mechanical read of `kb_tags` mint Chapter 6 rows.
- **`CRD`** — Chapter 2 line 600 uses the bare acronym with no expansion; the expansion first arrives at Ch 6 §8. Row reads *first mentioned Ch 2, defined Ch 6 §8*.
- **`PersistentVolumeClaim`, `volumeClaimTemplate`, `Headless Service`** — named and used at Ch 6 §6 but deliberately half-taught, with cross-bearings to Ch 11 §4 and Ch 9 §5. This is correct handling and the chapter tells the reader it is doing it. Recorded so a later pass does not "fix" it.

### Two outline-tagged concepts that never appear in the prose

- **`orphaning`** — zero occurrences of `orphan` in 1,213 lines. §3 covers the adjacent mechanism ("a Pod that has no owner reference") but never gives the reader the word. **Do not mint a glossary entry for a term the book does not use.** Either add it to §3 or drop the tag.
- **`vertical-scaling`** — never defined. The only match in the chapter is `VerticalPodAutoscaler`, named at §8 solely as one of four instances of the absent-component pattern. §2 defines *horizontal* scaling and stops. Same disposition.

---

## Concept shards added/updated at `Book-KCNA/knowledge-base/concepts/{slug}.md`

**13 created:**

- `workload-resource.md` — created (absorbs `pod-template` / `podtemplatespec`; see note)
- `deployment.md` — created
- `replicaset.md` — created
- `owner-reference.md` — created
- `controller-adoption.md` — created
- `rolling-update.md` — created
- `deployment-revision.md` — created
- `statefulset.md` — created
- `daemonset.md` — created
- `job.md` — created
- `cronjob.md` — created
- `custom-resource.md` — created
- `operator-pattern.md` — created

**3 updated by append (not overwrite):**

- `control-loop.md` — appended Chapter 6 section. **Discharges Ch 3's binding downstream obligation** ("Instantiate the loop in ReplicaSet — a control loop you can watch working in real time"). No contradiction; §9 extends it to six controllers.
- `label-selector.md` — appended Chapter 6 section. Adds ownership-is-not-selection, adoption, and the overlapping-selector hazard. No contradiction with Chapter 4's canon.
- `absent-component-pattern.md` — appended Chapter 6 section. **⚑ CANON DRIFT — see below.** Appended rather than overwritten precisely because it disagrees.

**Why append, not overwrite:** Rule 6 forbids silently replacing a shard whose canon this chapter touches. Appending a dated section preserves the prior chapter's wording as the reference point and makes the divergence legible. It is also the only safe move given that these three files do not exist on disk yet — an overwrite would silently drop Chapter 3's and Chapter 4's contributions if the orchestrator ever replays writes out of order.

**`pod-template` folded, not sharded.** §1's direct treatment is ~150 words, under the 200-word bar, but the template is load-bearing in three sections (§1 locates it, §4 mutates it, §5 makes it the sole revision trigger). Folding it into `workload-resource.md` with back-links from `rolling-update.md` and `deployment-revision.md` keeps it findable without minting a thin shard.

### ⚑ CANON DRIFT — the absent-component pattern was re-coined

`absent-component-pattern.md` (Chapter 3) carries an explicit instruction in capitals:

> **⚑ USE THIS NAME. DO NOT RE-COIN IT.** … Canonical name: "absent-component pattern." Canonical short form: **"an object without its component does nothing."**

The shard states the reason: *"If Chapters 10, 13, and 17 each invent their own phrasing, the reader gets four unrelated gotchas to memorize instead of one rule to apply."*

**Chapter 6 §8 is the pattern's first recurrence anywhere in the book, and it re-coins it twice:**

> "**This is a pattern the book will hit four times, and it's worth naming once: the object exists, but nothing happens without the component.**"
>
> "Four gotchas, one rule. **A Kubernetes API object is a record of intent. Intent with nothing watching it is just a row.**"

Neither is Chapter 3's string. The reader is now holding three phrasings of one rule, and this is the retrieval Chapter 3 spent a Worth-Securing box setting up. Chapter 5's manifest already recorded this theme at "⚑ still zero named recurrences" — the first recurrence has arrived and it does not use the name.

**Three things are true at once and all three should be recorded:**

1. **The instance is legitimate and good.** CRD-installed-but-nothing-happens is a textbook case, and §8's Snag teaches it well.
2. **Chapter 6 closes Chapter 3's count gap.** Chapter 3 promised "four more times" and beared only three, omitting NetworkPolicy-on-a-non-enforcing-CNI. §8 names all four — Ingress, `kubectl top`, VPA, **and NetworkPolicy** — with a source tag on the last. That defect is discharged.
3. **But the arithmetic now double-counts.** Chapter 3 promised four recurrences *after Chapter 3*. Chapter 6's CRD case is a fifth instance, and §8 says "four times" while pointing at the same four Chapter 3 named — so the reader is told four and shown five. Whichever count is chosen, Chapter 6 and Chapter 3 must agree.

**Recommended fix, one sentence in §8:** replace the coined phrase with Chapter 3's — *"the object exists, but nothing happens without the component"* → *"an object without its component does nothing — the pattern Chapter 3 named"* — and change "four times" to "four more times" so the CRD case reads as the instance it is. Costs about eight words and makes the first recurrence do the job the pattern was named for. **Author call; flagged, not fixed.**

---

## Voice-exemplar candidates nominated

Nine candidates. Not written to `voice-exemplars.md` — the author ratifies exemplars explicitly.

| Function | Excerpt | Recommendation |
|---|---|---|
| **☀️ Zenith** | "You have spent this chapter learning six workload resources. You have actually been looking at one diagram the entire time." | **Strong.** Two sentences that reframe a nine-section chapter. The second sentence does all the work and spends no words on setup. Directly comparable to Chapter 5's Zenith, which the prior manifest also rated strong — a series signature is forming. |
| **★ Fixed Point** | "**A controller's Pods are the Pods that match its selector. Membership is a query, not a list — which is why the Pod template's labels must satisfy the selector, and why two controllers whose selectors overlap are a hazard rather than a curiosity.**" | **Strong.** Rule, then two consequences derived from it rather than listed beside it. Same structure as Chapter 4's `spec`/`status` and Chapter 5's phase/state Fixed Points. |
| **Dead Reckoning** | "`.spec.strategy.type` accepts two values: `Recreate` and `RollingUpdate`. `RollingUpdate` is the default. Under `Recreate`, all existing Pods are killed before any new Pod is created… `maxSurge` caps how many Pods may exist above `.spec.replicas`; it defaults to 25% and rounds up when given as a percentage…" | **Strong.** The best facts-only block the book has produced — nine mechanism facts, zero framing, zero maritime register, and it is the densest section's safety net. Models §18.14 register discipline exactly. |
| **Extended Analogy** | "On a Deployment crew, any bosun's mate can stand any watch… On a StatefulSet crew, the pilot who knows this harbour is the pilot who knows *this* harbour. Her replacement is not another pilot… **Both crews are three or four people. Only one of them can be described by a count.**" | **Strong.** The closing sentence is the concept, and the analogy earns it rather than decorating it. Every element maps: roster→replicas, the annotated chart→PVC, "occupied not filled"→ordinal identity. Best sidebar-format exemplar available. |
| **⚓ Worth Securing** | "Self-healing and scaling are the same operation. There is no 'recovery mode' that switches on when something fails… Everything that looks like resilience in Kubernetes is this, wearing a different name." | **Strong.** Inline-scope discipline (three sentences), and the last clause converts a mechanism into a lens the reader carries forward. |
| **🪝 Snag** | "'We installed the CRD but nothing happened.' That is the correct behaviour, not a bug. You installed a place to put data. You did not install anything that reads it." | **Moderate.** Excellent as prose. Held at moderate only because of the canon-drift finding above — do not ratify the surrounding coinage as exemplar wording until the naming is reconciled with `absent-component-pattern.md`. |
| **chapter-opening / identity framing** | "Newcomers reach for the Pod. Then for a script that recreates the Pod. Then for a cron entry that checks whether the script ran, and eventually for a monitor that checks the cron entry. Practitioners write down the count and the template and go home. **You have probably written one of those scripts. This chapter is about not needing it.**" | **Strong.** Skill Part 3 connection architecture done without a single "security professionals think…" construction. The escalating clause rhythm is the joke and the argument simultaneously, and the direct address lands warm rather than accusing. |
| **🔵 register — cost stated, not hidden** | "That gap in the upper timeline is downtime, deliberately chosen… `Recreate` isn't the wrong answer; it's the correct answer with a known cost, and choosing it consciously is what a practitioner does. Choosing `RollingUpdate` for an application that can't tolerate two concurrent versions is the actual mistake." | **Strong.** Refuses the easy "here's the bad option" framing and inverts it. Exactly the confident-not-hedging register the brand voice specifies, and it models Part 14's honesty guardrail in prose rather than in a callout. |
| **closing epigraph (original)** | "*A fleet is not a number of ships. It is an intention, expressed in ships.*" — Lodestar Ledgers | **Strong.** Original quote that states the chapter's thesis before the chapter argues it, then reads as summary on the way out. Pairs with §9's "a single Pod is a statement about *right now*." |

**One nomination withheld.** §9's closing beat ("you crossed it somewhere around §2 without being asked to sign anything") is the best sentence in the chapter, but it is load-bearing *inside* the Zenith and does not survive extraction. Recorded here so a later pass does not re-discover and nominate it standalone.

---

## Objective coverage log

Chapter 6 tags `["D1.1"]` on all nine sections. That tagging is **incomplete**, and the gap is worth recording rather than silently propagating — see below the table.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.1** — Kubernetes Core Concepts | Chapter 3 *(cluster layer)* | deep | 2026-08-24 |
| **D1.1** | Chapter 4 *(object layer)* | deep | 2026-08-24 |
| **D1.1** | Chapter 5 *(Pod layer)* | deep | 2026-08-24 |
| **D1.1** | **Chapter 6** *(workload layer)* | **deep** | **2026-08-24** |
| **D3.1** — Application Delivery | **Chapter 6 §4–§5** *(untagged — first substantive coverage)* | moderate | 2026-08-24 |
| **D4.2** — Cloud Native Ecosystem and Principles | **Chapter 6 §8** *(untagged — partial)* | light | 2026-08-24 |

### ⚑ Chapter 6 discharges two research gaps it does not claim credit for

`domain-analysis.md` assigns research gaps to objectives. Two of them are closed by this chapter under objectives it never tags:

- **G8 — "Deployment update mechanics. Rolling update strategy, `maxSurge`/`maxUnavailable`, `Recreate`, rollout status, revision history, rollback."** Assigned **D3.1, D1.1**. §4 and §5 deliver every named item. `domain-analysis.md` calls this "D3.1's most operationally central topic" and notes D3.1 doubled in weight.
- **G10 — "CRDs, the operator pattern, and API extension."** Assigned **D1.1, D4.2, D3.1**. §8 delivers all three.

Under a D1.1-only tag, a later coverage audit will read D3.1 as uncovered through Chapter 6 and either re-teach the material in the delivery chapter or report a false gap. **Add `D3.1` to §4 and §5, and `D4.2` to §8, in `outline.md`'s `kb_tags.objectives`.** One-line edit; no prose change.

### The domain-weight alarm from Chapter 5 is resolved

Chapter 5's manifest raised this as blocking: four chapters inside the 44% Kubernetes Fundamentals domain had authored 28% between them, "leaving **16 points for Chapter 6 alone** — larger than Chapters 3, 4, and 5 combined," with the recommendation to settle before Chapter 6 drafted.

**Chapter 6 authored 6%, not 16%.** Subtotal is now 34% of 44%, leaving 10 points for the remaining D1 chapters (D1.2 Administration, D1.3 Scheduling). The chapter was authored to its content, not to a residue — which is what the concern asked for. **Close the finding.**

The *disclosure* half of it stands, though, and Chapter 6 makes it worse in a specific way. Chapter 6's metadata says "roughly six percent of the exam under this book's authored allocation — CNCF publishes four domain weights and twelve named competencies with no sub-weights, and the front matter says so plainly," with a source tag. That is the **best** disclosure of the five, better even than Chapter 2's. But it contains the chapter's one unresolved factual error.

### ⚑ "Twelve named competencies" — thirteen is correct

`draft-v1-prevoice.md:104`, inside the sourced disclosure sentence. `fact-accuracy.md` reports all three cached CNCF sources enumerate **thirteen**, and `domain-analysis.md` independently lists thirteen: D1.1–D1.4, D2.1–D2.4, D3.1–D3.2, D4.1–D4.3.

Two reasons this outranks a normal miscount. It sits in the sentence that establishes the chapter's epistemic authority — the one place the chapter tells the reader "here is what is published and here is what we authored." And **Chapter 5 shipped the same number**: its manifest records finding C2 as *fixed* by rewording to "one of the **twelve** named KCNA competencies" with a source tag. So the error is now in two chapters, both source-tagged, both in authority-establishing positions. **Book-level fix, not a Chapter 6 fix.** Sweep for the string before either chapter publishes.

---

## Retrieval-practice ledger

**7 tagged in-budget items · graded pool 34 (15 Bearings + 19 Practice) · rate = 20.6%.** Clears the 20% floor. Two further tagged items sit in Soundings, excluded from the budget per B3.

Every target verified against the named chapter's actual section content, not from memory.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| the control loop: two states compared, action on the gap | ch 3 §6 | **ch 6** — Soundings Q7 *(excluded from budget)* |
| Pod not rescheduled on node death; what happens instead | ch 5 §4 | **ch 6** — Soundings Q8 *(excluded from budget)* |
| control-loop states + the action, named with the real field | ch 3 §6 | **ch 6** — Bearings #1 Q4 |
| label selectors as the universal join; ReplicaSet as one of four users | ch 4 §5 | **ch 6** — Bearings #1 Q5 |
| readiness probes and what a not-ready Pod does to a rollout | ch 5 §7 | **ch 6** — Bearings #2 Q4 |
| `spec` = requested, `status` = actual | ch 4 §2 | **ch 6** — Practice Q2 |
| Pod replaced, not moved; new UID, new name | ch 5 §4 | **ch 6** — Practice Q4 |
| Pod phase `Succeeded` and what it means | ch 5 §5 | **ch 6** — Practice Q16 |
| control loop vs kube-controller-manager's built-ins | ch 3 §6 + §2 | **ch 6** — Practice Q18 |

**Chapter 6 draws from three predecessors**, matching Chapter 5. Chapter 4 drew from two, Chapter 3 from one.

**Practice Q2 is the cleanest setup-and-payoff in the book so far.** Chapter 4 line 273 forecasts it in published prose: *"Chapter 5 reads it against a Pod's phase, **Chapter 6 reads it against a replica count**."* Q2 is that promise cashed, drawing on the same snapshot (`k8s-docs-objects-2026-08-23`) and the same worked example the docs use. A reader who noticed the forecast gets a small reward two chapters later; one who didn't loses nothing.

**⚑ One cross-chapter item is invisible to a mechanical count.** Practice Q12 is tagged `[interleaved: Ch 5 §7 + §4]` and genuinely reaches Chapter 5 — but carries no `[retrieval:]` tag, so it does not appear in the seven. If the book's retrieval rate is ever computed by grepping `[retrieval:` — which is how a linter would do it — Q12 is uncounted and the true rate is 8/34 = 23.5%. Low severity for correctness; it matters because the metric is book-level. Adding the tag costs one token.

**⚑ Retrieval tags still absent from Chapter 6's answer keys.** Chapter 4 repeats the tag in its answers; Chapters 5 and 6 tag only the stems. Chapter 5's manifest raised this and recommended matching Chapter 4; Chapter 6 did not. Repeating the tag tells a reader who missed the item *which chapter to go back to* — the entire point. Two chapters of divergence now; **decide and sweep.**

### Cross-cutting themes — status after Chapter 6

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **The control loop** (B3 headline) | Ch 3 §6 | Ch 4 · Ch 5 *(unplanned)* · ✅ **Ch 6 — the planned instantiation, discharged in full** | **Ch 11 (still unbeared)**, Ch 15, Ch 17 |
| **Labels/selectors as the universal join** | Ch 4 §5 | Ch 5 *(unplanned)* · ✅ **Ch 6 §3 — first retrieval BY NAME, and the deep application** | Ch 7, Ch 9, Ch 10 |
| **The absent-component pattern** | Ch 3 §4, named | ⚑ **Ch 6 §8 — FIRST recurrence, but re-coined.** See canon drift above | Ch 10 ×2, Ch 13, Ch 17 |
| **"Kubernetes defines an interface, the ecosystem implements it"** | Ch 2 §4, named | ✅ **Ch 6 §8 — FIRST named recurrence.** "That is the fourth socket Chapter 2 promised" — CRI, CNI, CSI, API extension | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §2 |
| **Namespaced vs cluster-scoped** | Ch 4 §5 | Ch 5 §6 | ⚑ **not retrieved in Ch 6** — Ch 12 §3, Ch 10, Ch 11 |

**Chapter 6 discharges the two theme debts Chapter 5 flagged as stuck at zero.** Both the absent-component pattern and the four-interfaces theme get their first named recurrence here, and the control loop gets the instantiation Chapter 3 beared to it three chapters ago. This is the chapter the theme architecture was built around and it performs.

**⚑ The `reconciliation` gap is now three chapters deep and has crossed into prose.** Chapter 3 promised the reader that later chapters saying "reconciliation" would mean closing-the-gap work, then never bridged "control loop" to the word. Chapter 4 described the behavior three times without naming it. Chapter 5 used it in **two graded answers**. Chapter 6 now uses it in body prose — §3: *"Not 'on the next reconcile as a special case' — this **is** the reconcile"* — and again in §5's Helm/GitOps distinction. The book has used a word it promised to define in four chapters and defined it in none, while grading readers on it. **One appositive at Chapter 3's ★ Fixed Point closes this.** It was recommended at Chapter 5 and not done.

### Forward commitments — status

| # | Commitment | Status |
|---|---|---|
| 7 | **Ch 6 must open on "if Pods are designed to be replaced, who does the replacing?"** | ✅ **DISCHARGED verbatim.** §Why This Chapter Matters line 1: *"Chapter 5 ended on a question and deliberately refused to answer it: if Pods are designed to be replaced rather than repaired, who does the replacing?"* Also honors the second half — §1 tells the reader the Pod is "something you will almost never create directly." |
| 2 | Ch 11 must retrieve the control loop | ⚑ **OPEN, now four chapters overdue.** Chapter 6 bears to Ch 11 §4 twice (StatefulSet storage) and carries the loop to neither. Ch 3, 4, 5, and 6 have each passed it forward. |
| 5 | Ch 9 must retrieve the Pod IP / shared network namespace | **OPEN.** Ch 6 bears to Ch 9 four times (§1 stable name, §3 Service-selects-by-label, §6 headless, §7 CNI) and names the Pod IP in none. |
| 1 · 4 · 6 · 8 | Ch 13/Ch 8 version skew · Ch 12 RBAC 2×2 · Ch 13's "read the phase before you read the logs" · Ch 7/13/17/18 requests-and-limits | **OPEN** — Ch 7 is the next test, for #8. |
| **9** | **Ch 7 must open on the unplaced Pod** | **NEW.** The Voyage Ahead publishes it: *"It creates a Pod. It does not decide where the Pod goes."* Also pre-announces taints/tolerations via the DaemonSet's tolerations — "a node saying 'not for general traffic'." |
| **10** | **Ch 11 §4 must deliver PVC + `volumeClaimTemplate` for StatefulSets** | **NEW.** §6 tells the reader outright what was skipped and why: *"What this chapter owes you is the taxonomy… What that chapter owes you is how the storage actually works."* A published promise, and the book's only intentional half-teach. |
| **11** | **Ch 9 §5 must deliver headless Services** | **NEW.** §6 tells the reader a StatefulSet *requires* one and that they must create it. |
| **12** | **Ch 15 must land the GitOps controller as "the same figure"** | **NEW, and the strongest synthesis promise the book has published.** §9: *"come back and check this figure. It will be the same figure."* If Ch 15 redraws it, the promise breaks visibly. |
| **13** | **Ch 14 §5 and Ch 15 §3 must distinguish three "rollback" mechanisms** | **NEW.** §5 names all three (Deployment / Helm release / GitOps commit) and stakes the claim that knowing this one is what makes the other two distinguishable. |
| **14** | **Ch 17 §2 must collect the four pluggable interfaces in one place** | **NEW.** §8 hands it over explicitly: "Collecting all four into one story is Chapter 17's job." |

### ⚑ §N reservations — Ch 9 §1 collision is now three-deep and hardening

Chapter 6 pins §-numbers into twelve undrafted chapters. Most are compatible. Two are not:

| Reservation | Claimants | Status |
|---|---|---|
| **Ch 9 §1** | Ch 2 (*CNI and pod networking*) · Ch 5 (*why a Service is necessary*) · **Ch 6 §2** (*why a Service exists*) | ⚑ **HARD COLLISION, now three-deep. Blocking before Ch 9 drafts.** Chapter 5's manifest already ruled Ch 2 has precedence and the arc ordering supports it. Ch 6's claim is near-identical to Ch 5's — move both to §2/§3. |
| **Ch 17 §5** | **Ch 6 ×2** (*the autoscaling landscape*) vs Ch 5's **Ch 17 §2/§3** (autoscaling / mesh) vs Ch 2's **Ch 17 §4** | ⚑ Four-way. Chapter 5's recommendation — drop to chapter-level until Ch 17 is outlined — still applies and is a sanctioned form. |
| **Ch 13 §2 vs Ch 13 §4** | **Ch 6, internally inconsistent** | ⚑ **New, and it's Chapter 6 disagreeing with itself.** §2 bears to *"Ch 13 §4 — metrics-server as the HPA's input"*; §8 bears to *"Ch 13 §2 — the resource metrics pipeline."* Same subject, two reserved sections, one chapter. Pick one. |
| Ch 7 §1/§5 · Ch 9 §2/§5/§7 · Ch 10 §3 · Ch 11 §4 · Ch 12 §3 · Ch 14 §2/§3/§5 · Ch 15 §2/§3/§4 · Ch 16 §3 · Ch 18 §3 | Ch 6 | ✅ verified compatible with published claims and the arc outline |

Chapter 3's proposed convention — *no `§N` in cross-bearings pointing into undrafted chapters* — remains unratified and is now broken by four consecutive chapters. Ch 4: 15 times. Ch 5: 17 times across eleven chapters. **Ch 6: 22 times across twelve chapters.** The count grows every chapter and it is the direct cause of all three collisions above. This is a governance decision the author has not been asked to make explicitly; asking is cheap and the cost of not asking compounds.

### Inbound pointer repairs — confirmed, two shipped-file edits

Integration's finding is correct and I confirm its recommendation. Chapter 6's section order is fixed by six other inbound pointers plus the entire outline; editing two tokens in two shipped files is the cheap side.

- `chapter-01-taking-departure.md:436` — `Ch 6 §3` → **`Ch 6 §6`** (StatefulSets land in §6)
- `chapter-02-cargo-in-standard-crates.md:600` — `Ch 6 §3` → **`Ch 6 §8`** (CRDs land in §8)

Both are named in `draft-v1-prevoice.md:778`'s own `AUTHOR-REVIEW` comment and in the outline's open questions. Outside this chapter's files, so outside every stage's write scope — which is why they have survived to stage 14 unactioned.

---

## Closed as NOT defects

Recorded so downstream stages stop re-raising them.

1. **`ch06-zenith-control-loop-instantiated` is correctly named.** `arc-outline.md:156` prescribes it verbatim; `chNN-zenith-<slug>` is the pattern for all eighteen chapters; Chapter 2 shipped `ch02-zenith-standard-crate` in published prose. `image-specs.md`'s actual `anchor_id` field already matches the draft. **Strike the suggested `fig06` rename at `image-specs.md` lines 65, 575, and 628.** Identical to the ruling Chapter 5's manifest made on `ch05-zenith-smallest-deployable-unit`; this is the second chapter where Stage 10 has proposed the same wrong rename, which suggests Stage 10's anchor linter needs the `chNN-zenith-<slug>` form added as sanctioned.
2. **`fig04` appearing after `fig05` in the draft is not misordering.** The five `figMM` slugs are prescribed by `arc-outline.md` and the anchors are the join key into `image-specs.md`. Chapter 2 shipped with the same property. Preserving them unrenamed is correct.

---

## What I could not do

- **No glossary/coverage/retrieval content from Chapters 1–5 is merged into the append blocks below.** Those files do not exist; their content lives only inside four prior manifests. My blocks append cleanly onto whatever is there — including nothing — but if the orchestrator replays all five manifests in order, it must replay them *in order*, or Chapter 6's sections will sit above chapters that logically precede them.
- **Definitions could not be taken from this stage's declared input.** Stated at the top; sourced from `draft-v1-prevoice.md` instead.
- **No shard was written for `orphaning` or `vertical-scaling`.** Both are outline-tagged and neither exists in the prose. Minting entries for them would be inventing book content at stage 14, which is the one thing this stage must never do.

---

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 6 additions — Fleets, Not Vessels (2026-08-24)

**Appended, not merged.** This file is append-only under the current pipeline. Book
assembly merges alphabets mechanically.

**⚑ Source note.** Definitions below are inherited verbatim from
`.pipeline-state/ch-06/draft-v1-prevoice.md`, the intact 1,213-line draft. The stage-14
input (`draft-v2.md`) was truncated to its tail and contains no body prose. Voice-swap
alters register, not definitions, so the prevoice draft is the correct definitional
source. Where the revision stage sharpened a *factual* wording, the revised form is used
and marked.

Terms contributed: **58** — 52 defined · 4 reserved forward · 2 outline-tagged but absent.

## ⚑ Status changes to EXISTING rows above (apply at reconcile — cannot be done by append)

| Row | Current text | Correction | Evidence |
|---|---|---|---|
| **label selector** | introduced Ch 4 §5 | **CONFIRMED Ch 4.** ⚑ Ch 6's `kb_tags.concepts` wrongly claims `label-selector`, `matchlabels`, `matchexpressions` as introduced at Ch 6 §3. Ch 6 *applies* them. Cross-references must read **(Chapter 4)**. | ch-04 §5 defines, sources, and Fixed-Points them |
| **`matchLabels` / `matchExpressions`** | introduced Ch 4 §5 | **CONFIRMED Ch 4.** Ch 6 §3 adds only: "when both are specified the result is ANDed." | ch-06 §3 |
| **CRD / CustomResourceDefinition** | first used Ch 2 line 600, unexpanded | **first mentioned Ch 2 (bare acronym, no expansion) · DEFINED Ch 6 §8** | ch-02:600; ch-06 §8 |
| **PersistentVolumeClaim** | reserved → Ch 11 | **SURFACED Ch 6 §6** (named, used, deliberately half-taught). Full treatment remains Ch 11 §4. | ch-06 §6 |
| **Headless Service** | reserved → Ch 9 | **SURFACED Ch 6 §6** (named as a StatefulSet requirement). Full treatment remains Ch 9 §5. | ch-06 §6 |
| **control loop** | Ch 3 §6, canonical | **Ch 3's downstream obligation for Ch 6 DISCHARGED.** §2 instantiates it mechanically; §9 generalizes to six controllers. | ch-06 §2, §9 |
| **reconciliation** | ⚑ GAP — used but never defined | ⚑ **STILL OPEN, fourth chapter.** Ch 6 uses "reconcile" in §3 body prose and "reconciliation" in §5. Ch 5 used it in two graded answers. | ch-06:297, ch-06:533 |
| **absent-component pattern** | Ch 3 §4, canonical short form *"an object without its component does nothing"* | ⚑ **RE-COINED at Ch 6 §8.** See `concepts/absent-component-pattern.md` Chapter 6 section. | ch-06 §8 |

---

## Tier 1 — Defined at Chapter 6 (prose inherited verbatim)

### A

**adoption (controller adoption)** — "A ReplicaSet identifies new Pods to acquire using
its selector: if there's a Pod that has no owner reference, or whose owner reference is
not a controller, and it matches a ReplicaSet's selector, it will be **immediately**
acquired by that ReplicaSet." [source: k8s-docs-replicaset-2026-08-24] (Ch 6 §3)
> The chapter's gloss, worth keeping: "Immediately. Not 'on the next reconcile as a
> special case' — this *is* the reconcile." And: "The ReplicaSet is not limited to owning
> Pods created from its own template. It owns what matches."

**API server aggregation** — the alternative to CRDs for extending the API, which "gives
more flexibility at the cost of writing and operating your own API server."
[source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8, 🔭 Closer Look)

**available (Deployment sense)** — a Pod counts as available once it is ready and has
stayed ready for `minReadySeconds`. "Kubernetes marks a Deployment as progressing when new
Pods become ready or available — available meaning ready for at least `minReadySeconds`."
[source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §4)

### C

**cascading deletion** — "Kubernetes checks for and deletes objects that no longer have
owner references — like the Pods left behind when you delete a ReplicaSet — and when you
delete an object you can control whether its dependents are deleted automatically."
[source: k8s-docs-garbage-collection-2026-08-24] (Ch 6 §3)
> In practice: delete the Deployment, and the ReplicaSets and Pods go with it. "To delete
> a ReplicaSet and all of its Pods, use `kubectl delete`; the garbage collector
> automatically deletes all of the dependent Pods by default."
> [source: k8s-docs-replicaset-2026-08-24]
> ⚑ Deliberately NOT taught: foreground vs background cascading deletion, finalizers,
> `blockOwnerDeletion`. Named as real and out of scope at this level.

**CronJob** — "A CronJob creates Jobs on a repeating schedule."
[source: k8s-docs-cronjob-2026-08-24] (Ch 6 §7)
> Canonical mental model, from the docs: "one CronJob object is like one line of a crontab
> file on a Unix system."
> Canonical retrieval string: **"a CronJob's output is Jobs. It doesn't run work; it
> creates the thing that runs work."**

**custom controller** — a controller written outside the Kubernetes project that acts on a
custom resource. "When you combine a custom resource with a custom controller, custom
resources provide a true declarative API… You can deploy and update a custom controller on
a running cluster, independently of the cluster's own lifecycle."
[source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8)

**custom resource** — "an extension of the Kubernetes API that is not necessarily available
in a default Kubernetes installation; it represents a customization of a particular
Kubernetes installation. Custom resources can appear and disappear in a running cluster
through dynamic registration." [source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8)
> The clause the chapter says makes it click: "**once a custom resource is installed, users
> can create and access its objects using `kubectl`, just as they do for built-in resources
> like Pods.**"

**CustomResourceDefinition (CRD)** — "The CustomResourceDefinition API resource allows you
to define custom resources. Defining a CRD object creates a new custom resource with a name
and schema that you specify, and the Kubernetes API then serves and handles the storage of
your custom resource." [source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8)
> ⚑ First mentioned Ch 2 line 600 as a bare, unexpanded acronym. This is the definition.

### D

**DaemonSet** — "defines Pods that provide facilities local to nodes. Every time you add a
node to your cluster that matches the specification in a DaemonSet, the control plane
schedules a Pod for that DaemonSet onto the new node. Each Pod in a DaemonSet performs a job
similar to a system daemon on a classic Unix server."
[source: k8s-docs-workloads-2026-08-23] (Ch 6 §7)
> Stated from the other page: "ensures that all (or some) Nodes run a copy of a Pod — as
> nodes are added to the cluster, Pods are added to them; as nodes are removed, those Pods
> are garbage collected." [source: k8s-docs-daemonset-2026-08-24]
> **★ Fixed Point wording, canonical:** "DaemonSet: one Pod per matching node, added
> automatically as nodes join — no replica count."
> ⚑ **Count-as-consequence** (framing adopted from the revision stage): "A DaemonSet does
> not take a replica count; its Pod count is a *consequence* of how many nodes are eligible,
> since the controller creates a Pod for each eligible node."
> [source: k8s-docs-daemonset-2026-08-24] Corroborated: "horizontal pod autoscaling does not
> apply to objects that can't be scaled — for example, a DaemonSet."
> [source: k8s-docs-hpa-2026-08-24]
> ⚑ Research-manifest gap G-6A: no fetched sentence states verbatim that a DaemonSet has no
> `replicas` field. The claim is entailed, and the prose correctly states it as a consequence
> rather than a quotation.

**declarative API** — "you declare the desired state of your resource, and the Kubernetes
controller keeps the current state of Kubernetes objects in sync with your declared desired
state — in contrast to an imperative API, where you instruct a server what to do."
[source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8)
> The chapter's gloss: "It's Chapter 3's control loop, written by somebody who does not work
> on Kubernetes."

**Deployment** — "A Deployment manages a set of Pods to run an application workload — usually
one that doesn't maintain state — and it provides declarative updates for Pods **and
ReplicaSets**." [source: k8s-docs-deployment-2026-08-23] (Ch 6 §1)
> "You create a Deployment to roll out a ReplicaSet; the ReplicaSet creates Pods in the
> background." The Deployment holds the Pod template and the update policy.

**desired replica count (`.spec.replicas`)** — the number of Pods a ReplicaSet should be
maintaining; the desired-state half of the control loop. "A ReplicaSet can be scaled up or
down by simply updating the `.spec.replicas` field."
[source: k8s-docs-replicaset-2026-08-24] (Ch 6 §2)

**dynamic registration** — the property by which "custom resources can appear and disappear
in a running cluster," letting cluster admins "update them independently of the cluster
itself." [source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8)

### H

**horizontal scaling** — "Horizontal scaling means changing the number of replicas."
[source: k8s-docs-autoscaling-2026-08-23] (Ch 6 §2)
> ⚑ **Vertical scaling is NOT defined in this chapter** despite the `vertical-scaling`
> concept tag. Only VerticalPodAutoscaler is named, and only as an absent-component instance.

**HorizontalPodAutoscaler (HPA)** — "an API resource plus a controller that periodically
adjusts the desired scale of its target to match observed metrics such as average CPU
utilization." [source: k8s-docs-hpa-2026-08-24] (Ch 6 §2)
> "A ReplicaSet can itself be a target for an HPA."
> [source: k8s-docs-replicaset-2026-08-24] Full autoscaling landscape reserved → Ch 17.

### I

**idempotent (Job design requirement)** — "A CronJob creates a Job approximately once per
execution time of its schedule. The scheduling is approximate — there are circumstances where
two Jobs might be created, or no Job might be created… which is why the docs state that the
Jobs you define should be idempotent."
[source: k8s-docs-cronjob-2026-08-24] (Ch 6 §7, 🔭 Closer Look)

**interchangeability** — the property that decides Deployment vs StatefulSet. A Deployment
"is a good fit for managing a stateless application workload on your cluster, *where any Pod
in the Deployment is interchangeable and can be replaced if needed*."
[source: k8s-docs-workloads-2026-08-23] (Ch 6 §6)
> **★ Fixed Point wording, canonical:** "The property that decides Deployment versus
> StatefulSet is *interchangeability*, not disk."
> The chapter's operational test, worth keeping verbatim: "The question is never 'does it
> write.' It's 'if I destroyed this Pod and built an identical one, would anything care
> *which one it was*?'"

### J

**Job** — "represents a one-off task that runs to completion and then stops. A Job creates
one or more Pods and continues to retry execution until a specified number of them
successfully terminate; when that number is reached, the Job is complete."
[source: k8s-docs-job-2026-08-24] (Ch 6 §7)
> **Level distinction (wording adopted from the revision stage, Practice A16):** `Succeeded`
> is a *Pod* phase; the **Job object itself finishes as `Complete`.**
> [source: k8s-docs-job-2026-08-24] Ch 6 §7's prose gives only the Ch 3 form ("the Job
> controller updates the Job object to mark it Finished"); the revision's `Complete` is the
> sharper and correct API wording.
> Field consequence: "for a Job, only a `restartPolicy` of `Never` or `OnFailure` is allowed."
> [source: k8s-docs-job-2026-08-24] "`Always` would be a category error."

**`.spec.jobTemplate`** — "defines the Jobs the CronJob creates, and has exactly the same
schema as a Job." [source: k8s-docs-cronjob-2026-08-24] (Ch 6 §7)

### M

**`maxSurge`** — "the maximum number of Pods that can be created **over** the desired number
of Pods. The absolute number is calculated from the percentage by **rounding up**. The default
is 25%." [source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §4)

**`maxUnavailable`** — "the maximum number of Pods that can be unavailable during the update
process. The absolute number is calculated from the percentage by **rounding down**. The
default is 25%." [source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §4)
> "Neither can be `0` if the other is `0`." Chapter gloss: "with no headroom above and no
> slack below, there is no legal move."
> 🪢 **Mnemonic, canonical:** "Surge is above the line. Unavailable is below it."

**`minReadySeconds`** — "the minimum number of seconds for which a newly created Pod should be
ready, without any of its containers crashing, for it to be considered available; it defaults
to 0, meaning the Pod counts as available as soon as it is ready."
[source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §4)

### N

**node-local facility** — the role a DaemonSet fills. Documented uses: "running a cluster
storage daemon on every node, running a logs collection daemon on every node, running a node
monitoring daemon on every node." [source: k8s-docs-daemonset-2026-08-24] (Ch 6 §7)
> Grouped by role in the workloads overview: "fundamental to the operation of your cluster,
> such as a plugin to run cluster networking"; "help you manage the node"; or "provide
> optional behaviour that enhances the container platform."
> [source: k8s-docs-workloads-2026-08-23]

### O

**operator pattern** — "combines custom resources and custom controllers."
[source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8)
> Motivation, which explains the name: it "aims to capture the key aim of a *human* operator
> who is managing a service or set of services — people who look after specific applications
> and have deep knowledge of how the system ought to behave, how to deploy it, and how to
> react if there are problems." Operators "are clients of the Kubernetes API that act as
> controllers for a custom resource," and the pattern extends cluster behaviour "**without
> modifying the code of Kubernetes itself**."
> [source: k8s-docs-operator-pattern-2026-08-23]
> **Where it runs — the fact that closes the chapter's loop:** "The controller will normally
> run outside of the control plane, much as you would run any containerized application — for
> example, as a Deployment." [source: k8s-docs-operator-pattern-2026-08-23]

**ordinal index** — "For a StatefulSet with N replicas, each Pod is assigned an integer
ordinal, unique over the set, from 0 through N-1."
[source: k8s-docs-statefulset-2026-08-24] (Ch 6 §6)

**owner reference** — "the Pods' `metadata.ownerReferences` field, which specifies what
resource the current object is owned by. All Pods acquired by a ReplicaSet carry the owning
ReplicaSet's identifying information in that field, and it is through this link that the
ReplicaSet knows the state of the Pods it's maintaining."
[source: k8s-docs-replicaset-2026-08-24] (Ch 6 §3)
> ⚑ **Explicitly a DIFFERENT mechanism from labels-and-selectors.** "labels determine *which*
> EndpointSlices belong to the Service and owner references keep different parts of Kubernetes
> from interfering with objects they don't control."
> [source: k8s-docs-garbage-collection-2026-08-24]
> Chapter's framing: "Selectors answer 'which Pods should I be looking at.' Ownership answers
> 'which Pods am I responsible for.'"

**overlapping selectors** — the hazard where two controllers' selectors match the same Pods.
"Two controllers whose selectors overlap will fight over the same Pods — and neither one
reports an error. Each sees a count that keeps changing for reasons it didn't cause, and each
keeps acting on it." (Ch 6 §3, 🪝 Snag)
> Docs warning: "be careful not to overlap with the selectors of other controllers, lest they
> try to adopt this Pod." [source: k8s-docs-replicaset-2026-08-24]
> ⚑ There is **no API validation** against this — the API does not police cross-object overlap.

### P

**pause / resume (rollout)** — "you can pause rollouts before you trigger one or more updates,
then resume when you're ready to apply the changes — this lets you apply multiple fixes in
between pausing and resuming without triggering unnecessary rollouts."
[source: k8s-docs-deployment-2026-08-23] (Ch 6 §5)

**Pod template (`.spec.template`)** — "it now lives inside the workload resource as
`.spec.template`, a pod template with exactly the same schema as a Pod, except that it's
nested and has no `apiVersion` or `kind` of its own."
[source: k8s-docs-daemonset-2026-08-24] (Ch 6 §1)
> "Controllers for workload resources create Pods from that template and manage them on your
> behalf." [source: k8s-docs-pods-2026-08-24]
> ⚑ Load-bearing in three sections: §1 locates it, §4 mutates it, §5 makes it the *sole*
> revision trigger.

**PodTemplateSpec** — the schema name for the Pod template as it appears on a Deployment.
"You declare the new state of the Pods by updating the PodTemplateSpec of the Deployment."
[source: k8s-docs-deployment-2026-08-23] (Ch 6 §4)

**`.spec.progressDeadlineSeconds`** — "how long the Deployment may go without progressing
before the system reports failure; it defaults to 600."
[source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §4)
> ⚑ "The deadline **reports**; it does not abort." The controller keeps retrying.

### R

**`Recreate`** — deployment strategy in which "all existing Pods are killed before new ones
are created." [source: k8s-docs-deployment-2026-08-23] API reference: "kill all existing pods
before creating new ones." [source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §4)
> Canonical framing, and the chapter defends it at length: "it's the correct answer with a
> known cost." For apps that genuinely cannot run two versions at once — schema migration,
> exclusive lock, single-instance licence.

**ReplicaSet** — "maintain a stable set of replica Pods running at any given time."
[source: k8s-docs-replicaset-2026-08-24] (Ch 6 §1–§2)
> Full definition: "defined with a selector that specifies how to identify Pods it can
> acquire, a number of replicas indicating how many Pods it should be maintaining, and a Pod
> template specifying the data of new Pods it should create to meet the replica count
> criteria. It fulfills its purpose by creating and deleting Pods as needed to reach the
> desired number." [source: k8s-docs-replicaset-2026-08-24]
> The difference from a bare Pod, in one documented line: "a ReplicaSet replaces Pods that are
> deleted or terminated for any reason, such as node failure or disruptive node maintenance
> like a kernel upgrade."

**ReplicationController (legacy)** — "the legacy resource that ReplicaSet replaced
[source: k8s-docs-workloads-2026-08-23]; ReplicaSets are its successors, serving the same
purpose and behaving similarly, except that a ReplicationController doesn't support set-based
selector requirements." [source: k8s-docs-replicaset-2026-08-24] (Ch 6 §1)
> ⚑ Mark **superseded** in the glossary. The chapter gives it one clause deliberately: "if you
> see it, it's superseded."

**resource (API sense)** — "an endpoint in the Kubernetes API that stores a collection of API
objects of a certain kind — the built-in `pods` resource, for instance, contains a collection
of Pod objects." [source: k8s-docs-custom-resources-2026-08-23] (Ch 6 §8)

**revision (Deployment)** — "A Deployment's revision is created when a rollout is triggered —
and a new revision is created **if and only if** the Deployment's Pod template
(`.spec.template`) is changed. Other updates, such as scaling the Deployment, do not create a
Deployment revision." [source: k8s-docs-deployment-2026-08-23] (Ch 6 §5)
> **★ Fixed Point wording, canonical:** "A new revision is created if and only if
> `.spec.template` changes. Scaling does not create a revision."
> The chapter's clean mental model, worth keeping: "**revisions are a history of what your
> Pods are, not of how many.**"
> The test the chapter gives the reader: "The test is not 'did I edit the Deployment.' It is
> 'did I edit `.spec.template`.'"

**`.spec.revisionHistoryLimit`** — "specifies the number of old ReplicaSets to retain to allow
rollback; **by default, 10 old ReplicaSets will be kept**. Setting it to zero means all old
ReplicaSets with 0 replicas are cleaned up — and in that case a new Deployment rollout cannot
be undone, since its revision history is cleaned up."
[source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §5)

**rollback** — "setting the Pod template to a previous value and letting the same rolling
update run in the other direction — same controller, same two ReplicaSets, same `maxSurge` and
`maxUnavailable`, same readiness gate." (Ch 6 §5)
> "The Deployment doesn't have a special reverse gear. It has one gear, and rollback points it
> at an older template."
> ⚑ **Three mechanisms share this word.** Deployment rollback (here) · Helm rollback, which
> operates on releases (Ch 14 §5) · GitOps rollback, which reverts committed configuration
> (Ch 15 §3). The chapter stakes the claim that knowing this one is what makes the other two
> distinguishable.
> ⚠ **Navigational Hazard, canonical:** "`rollout undo` will put my replica count back." It
> will not. The replica count is not in the Pod template.

**rollout** — the process of applying a Pod-template change. Verb surface, closed set:
`kubectl rollout status` / `history` / `undo` / `pause` / `resume` / `restart`. Valid resource
types include deployments, daemonsets, and statefulsets.
[source: k8s-docs-kubectl-rollout-2026-08-24] [source: k8s-docs-kubectl-overview-2026-08-23]
(Ch 6 §5)

**`RollingUpdate`** — the **default** value of `.spec.strategy.type`. "A new ReplicaSet is
created, and the Deployment manages moving the Pods from the old ReplicaSet to the new one at
a controlled rate." [source: k8s-docs-deployment-2026-08-23] (Ch 6 §4)
> **★ Fixed Point wording, canonical:** "`RollingUpdate` is the default strategy. `maxSurge`
> and `maxUnavailable` both default to 25%. `Recreate` kills all existing Pods before any new
> ones are created."
> ⚑ **Two ReplicaSets exist at once** during a rolling update. This is normal, not a transient
> artifact, and it is only expressible because the Deployment layer sits above the ReplicaSet
> layer.

**run to completion** — the defining shape of Job work, as against a service that should never
exit. "You can use a Job to define a task that runs to completion, just once."
[source: k8s-docs-workloads-2026-08-23] (Ch 6 §7)
> Retroactively justifies Ch 5's `Succeeded` and `Failed` phases: "for a long-running service,
> `Succeeded` would be a malfunction; for a Job, it's the goal."

### S

**`.spec.schedule`** — "required and takes standard five-field cron syntax — `0 3 * * 1` means
weekly on a Monday at 3 a.m." [source: k8s-docs-cronjob-2026-08-24] (Ch 6 §7)

**selector–template agreement** — the API-enforced rule that a controller's Pod-template labels
must satisfy its own selector. "In a ReplicaSet, `.spec.template.metadata.labels` must match
`spec.selector`, or the object will be rejected."
[source: k8s-docs-replicaset-2026-08-24] Same for Deployment
[source: k8s-docs-deployment-spec-fields-2026-08-24] and DaemonSet
[source: k8s-docs-daemonset-2026-08-24]. (Ch 6 §3)
> **The principle beneath the validation, which is the part to carry:** "because membership is
> computed rather than recorded, the labels a controller stamps on its own Pods have to satisfy
> the question it will later ask about them."

**stable network identity** — "Each Pod derives its hostname from the StatefulSet's name and its
ordinal: `$(statefulset name)-$(ordinal)`."
[source: k8s-docs-statefulset-2026-08-24] (Ch 6 §6)

**stable storage** — "For each `volumeClaimTemplate` entry, each Pod receives one
PersistentVolumeClaim, and the same claim is bound to that Pod throughout its lifecycle."
[source: k8s-docs-statefulset-2026-08-24] (Ch 6 §6)
> Canonical gloss from the figure: "the storage belongs to the IDENTITY, not to the Pod."

**StatefulSet** — "runs a group of Pods and maintains a sticky identity for each of them —
useful for applications that need persistent storage or a stable, unique network identity."
[source: k8s-docs-statefulset-2026-08-24] (Ch 6 §6)
> The contrast sentence, canonical: "like a Deployment, a StatefulSet manages Pods that are
> based on an identical container spec; *unlike* a Deployment, a StatefulSet maintains a sticky
> identity for each of its Pods — these Pods are created from the same spec, but **are not
> interchangeable**: each has a persistent identifier that it maintains across any
> rescheduling."
> Ordering: "Pods are created sequentially in order from 0 to N-1… terminated in reverse order,
> N-1 down to 0. Before a scaling operation is applied to a Pod, all of its predecessors must
> be Running and Ready."
> ⚑ Two documented limitations flagged forward to Ch 11: storage must be provisioned by a PV
> provisioner or pre-provisioned by an admin; and "deleting or scaling down a StatefulSet does
> **not** delete the associated volumes."

**`.spec.strategy`** — "specifies the strategy used to replace old Pods by new ones.
`.spec.strategy.type` can be `Recreate` or `RollingUpdate`, and `RollingUpdate` is the default
value." [source: k8s-docs-deployment-2026-08-23] (Ch 6 §4)

**stuck rollout** — "Deployments can get stuck trying to deploy a newest ReplicaSet without ever
completing, from causes including insufficient quota, readiness probe failures, image pull
errors, insufficient permissions, and limit ranges."
[source: k8s-docs-deployment-spec-fields-2026-08-24] (Ch 6 §4, 🪝 Snag)
> "A stalled rollout is not a failed one, and it does not clean itself up." Reported as
> `type: Progressing`, `status: "False"`, `reason: ProgressDeadlineExceeded`.

### W

**workload resource** — "you don't need to manage each Pod directly — instead you use workload
resources that manage a set of Pods on your behalf, and those resources configure controllers
that make sure the right number of the right kind of Pod are running, to match the state you
specified." [source: k8s-docs-workloads-2026-08-23] (Ch 6 §1)
> **★ Fixed Point wording, canonical (the ownership chain):** "The chain is Deployment →
> ReplicaSet → Pod. The Deployment holds the Pod template and the update policy. The ReplicaSet
> holds the replica count. The Pods run."
> ⚓ Worth Securing, canonical: "Pods are generally not created directly, and are created using
> workload resources instead [source: k8s-docs-pods-2026-08-24]. A bare Pod is not replaced
> when its node fails — it is simply gone."

---

## Tier 2 — Commands introduced or given their motivation at Chapter 6

**`kubectl scale`** — "a first-class verb for exactly that — update the size of the specified
deployment." [source: k8s-docs-kubectl-overview-2026-08-23] (Ch 6 §2)
Example form: `kubectl scale deployment/web --replicas=5`

**`kubectl rollout status`** — "Show the status of the rollout."
[source: k8s-docs-kubectl-rollout-2026-08-24] (Ch 6 §5)

**`kubectl rollout history`** — "View rollout history." Form:
`kubectl rollout history deployment/<name>` [source: k8s-docs-deployment-2026-08-23] (Ch 6 §5)

**`kubectl rollout undo`** — "Undo a previous rollout." `--to-revision=<n>` targets a specific
revision. [source: k8s-docs-deployment-2026-08-23] (Ch 6 §5)

**`kubectl rollout pause` / `resume`** — "Mark the provided resource as paused" / "Resume a
paused resource." [source: k8s-docs-kubectl-rollout-2026-08-24] (Ch 6 §5)
> ⚓ Worth Securing: "`pause` before a batch of edits. It is the difference between one rollout
> and four, and it costs one command."

**`kubectl rollout restart`** — "Restart a resource."
[source: k8s-docs-kubectl-rollout-2026-08-24] (Ch 6 §5)

**`kubectl delete` (cascading)** — "the garbage collector automatically deletes all of the
dependent Pods by default." [source: k8s-docs-replicaset-2026-08-24] (Ch 6 §3)

⚑ The general `kubectl` command surface — flags, output formats, everything else — is
deliberately deferred to Ch 8 §2. Ch 6 introduces verbs only where a concept needs a name.

---

## Tier 3 — Reserved forward from Chapter 6

| Term | Surfaced at | Full treatment reserved to | Note |
|---|---|---|---|
| **PersistentVolumeClaim** | Ch 6 §6 | **Ch 11 §4** | Named and used; the chapter tells the reader explicitly what was skipped and why. The book's only intentional half-teach. |
| **`volumeClaimTemplate`** | Ch 6 §6 | **Ch 11 §4** | Same. |
| **Headless Service** | Ch 6 §6 | **Ch 9 §5** | "StatefulSets currently require a Headless Service to be responsible for the network identity of the Pods, and you are responsible for creating it." [source: k8s-docs-statefulset-2026-08-24] |
| **VerticalPodAutoscaler** | Ch 6 §8 | **Ch 17 §5** | Named ONLY as one of four absent-component instances: "an add-on and not included by default." [source: k8s-docs-autoscaling-2026-08-23] Not a scaling definition. |
| **taints and tolerations** | Ch 6 §7 | **Ch 7 §5** | The DaemonSet controller "automatically adds a set of tolerations so DaemonSet Pods can run on nodes that are unschedulable, under disk or memory pressure, or not yet ready." [source: k8s-docs-daemonset-2026-08-24] |
| **blue/green, canary, A/B** | Ch 6 §4 (named, not defined) | **Ch 15 §4** | The chapter is explicit that it teaches rolling-update *mechanics*, not strategy *vocabulary*. |

---

## Tier 4 — ⚑ Outline-tagged, ABSENT from the chapter. Do not mint entries.

| Concept tag | Finding |
|---|---|
| **`orphaning`** | **Zero occurrences of `orphan` in 1,213 lines.** §3 covers the adjacent mechanism — adoption of Pods that "carry no controller owner reference" — but never gives the reader the word. Either add the term to §3 or drop the tag from `outline.md`. **Do not create a glossary row for a word the book does not use.** |
| **`vertical-scaling`** | **Never defined.** The single match is `VerticalPodAutoscaler` at §8, present only as an absent-component instance. §2 defines horizontal scaling and stops, correctly — the chapter has no scope for vertical scaling. Drop the tag. |

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/workload-resource.md ===
# Concept: Workload resources and the ownership chain

**Home:** Chapter 6 §1 · **Competency:** D1.1 · **Status:** canonical
**Absorbs:** `pod-template`, `podtemplatespec`, `ownership-chain`, `replicationcontroller-legacy`
**Answers:** Chapter 5's published closing question — *"if Pods are designed to be replaced
rather than repaired, who does the replacing?"*

## Definition (verbatim)

> You don't need to manage each Pod directly — instead you use **workload resources** that
> manage a set of Pods on your behalf, and those resources configure controllers that make
> sure the right number of the right kind of Pod are running, to match the state you
> specified. [source: k8s-docs-workloads-2026-08-23]

The chapter's instruction on how to read it is worth preserving: *"Read that again with an eye
on the verbs. You specify. The resource configures. The controller makes sure. Nobody in that
sentence performs the replacement as an action; the replacement is a consequence of a
specification and a loop."*

## ★ Fixed Point (verbatim — do not reword)

> **The chain is Deployment → ReplicaSet → Pod. The Deployment holds the Pod template and the
> update policy. The ReplicaSet holds the replica count. The Pods run.**

## Three layers, not two — why this is the structural key

This is the chapter's load-bearing claim and the thing "almost everyone skips on first
reading." Two later sections are direct consequences of it:

| Consequence | Section | Why it needs three layers |
|---|---|---|
| A rolling update works the way it does | §4 | A Deployment can hold **two ReplicaSets at once** — one scaling down, one scaling up. There has to be somewhere for the old count and the new count to live separately. |
| A revision means what it means | §5 | The **template lives one layer above the count**, so changing the template is a different kind of event from changing the count. |

The chapter's test of the model: *"A reader who has the chain finds the rolling update obvious…
A reader who thinks a Deployment owns Pods directly finds it magic."*

## The Pod template

> It now lives inside the workload resource as **`.spec.template`**, a pod template with
> exactly the same schema as a Pod, except that it's nested and has no `apiVersion` or `kind`
> of its own. [source: k8s-docs-daemonset-2026-08-24]

"Controllers for workload resources create Pods from that template and manage them on your
behalf." [source: k8s-docs-pods-2026-08-24]

**Not sharded separately, deliberately** — §1's direct treatment is ~150 words, under the bar.
But it is load-bearing in three places and both consumers link back here:

- §1 **locates** it (one nesting level down from where Ch 4 §2 left it)
- §4 **mutates** it — see [[rolling-update]]
- §5 makes it the **sole** revision trigger — see [[deployment-revision]]

`PodTemplateSpec` is the schema name for the same thing as it appears on a Deployment: "You
declare the new state of the Pods by updating the PodTemplateSpec of the Deployment."
[source: k8s-docs-deployment-2026-08-23]

## ⚓ Worth Securing (verbatim)

> If you find yourself writing a bare Pod manifest for anything other than a one-off
> experiment, you've picked the wrong object. The Kubernetes docs put it flatly: Pods are
> generally not created directly, and are created using workload resources instead
> [source: k8s-docs-pods-2026-08-24]. **A bare Pod is not replaced when its node fails — it is
> simply gone.**

## The reframe this section exists for

> The Pod you spent an entire chapter learning is something you will almost never create
> directly. Not because Pods are unimportant — the Pod is still the unit of everything — but
> because **being the thing that gets created for you is what a Pod is for.**

This discharges the commitment Chapter 5 published in its Voyage Ahead.

## ReplicationController — superseded, one clause

"The legacy resource that ReplicaSet replaced [source: k8s-docs-workloads-2026-08-23];
ReplicaSets are its successors, serving the same purpose and behaving similarly, except that a
ReplicationController doesn't support set-based selector requirements."
[source: k8s-docs-replicaset-2026-08-24]

Appears in older tutorials and in `kubectl scale`'s own help text. The chapter's disposition is
correct and should not be expanded: *"if you see it, it's superseded."*

## Figure

`ch06-fig01-deployment-replicaset-pod-ownership` — three stacked boxes with `owns` arrows, and
the caption axis that carries the idea: **"intent flows DOWN / existence is reported UP."** Any
redraw must preserve that axis; it is the `spec`/`status` distinction from Ch 4 §2 rendered
spatially.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 7** | Every Pod this chain creates arrives **unplaced.** §1's replacements, §4's surge Pods, §7's DaemonSet Pods on new nodes — the Voyage Ahead hands Ch 7 the unplaced Pod as its opening question. |
| **Ch 9** | The churn — "Pods appearing and disappearing with different names each time" — is the published argument for why a stable name has to come from somewhere else. |
| **Ch 14 §2** | "A Helm chart's job is to template this object." Beared from §1. |

## Related

[[deployment]] · [[replicaset]] · [[control-loop]] · [[pod]] · [[pod-lifetime]] ·
[[kubernetes-object]] · [[spec]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/deployment.md ===
# Concept: Deployment

**Home:** Chapter 6 §1, §4, §5 · **Competency:** D1.1 (⚑ **also D3.1** — see coverage note)
**Status:** canonical

## Definition (verbatim)

> A Deployment manages a set of Pods to run an application workload — usually one that doesn't
> maintain state — and it provides declarative updates for Pods **and ReplicaSets.**
> [source: k8s-docs-deployment-2026-08-23]

"You create a Deployment to roll out a ReplicaSet; the ReplicaSet creates Pods in the
background." [source: k8s-docs-deployment-2026-08-23]

## What the Deployment layer holds, and what it does not

| Holds | Does not hold |
|---|---|
| The **Pod template** (`.spec.template`) | The replica count *(the ReplicaSet holds it)* |
| The **update strategy** (`.spec.strategy`) | Any Pod directly |
| `revisionHistoryLimit`, `progressDeadlineSeconds`, `minReadySeconds` | |

You *set* `replicas` on a Deployment and it propagates to the ReplicaSet it manages — but the
object whose job is maintaining that many Pods is the ReplicaSet, and **during a rollout there
are two of them holding different numbers.** That distinction is the whole point of the
Practice Q1 item and is the most-missed fact in the chapter.

## The defining fit condition

A Deployment "is a good fit for managing a stateless application workload on your cluster,
*where any Pod in the Deployment is interchangeable and can be replaced if needed*."
[source: k8s-docs-workloads-2026-08-23]

**Interchangeability is the condition, not statelessness.** See [[statefulset]] for the
misconception this kills.

## ⚑ Objective-tagging note

`outline.md` tags all nine sections `["D1.1"]`. §4 and §5 deliver research gap **G8** —
*"Deployment update mechanics. Rolling update strategy, `maxSurge`/`maxUnavailable`,
`Recreate`, rollout status, revision history, rollback"* — which `domain-analysis.md` assigns to
**D3.1 and D1.1**, and calls "D3.1's most operationally central topic."

Under a D1.1-only tag a coverage audit will read D3.1 as uncovered through Ch 6. **Add `D3.1`
to §4 and §5.**

## Related

[[workload-resource]] · [[replicaset]] · [[rolling-update]] · [[deployment-revision]] ·
[[statefulset]] · [[operator-pattern]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/replicaset.md ===
# Concept: ReplicaSet — the control loop you can watch

**Home:** Chapter 6 §1, §2, §3 · **Competency:** D1.1 · **Status:** canonical
**Discharges:** Chapter 3's binding obligation on Chapter 6 — *"Instantiate the loop in
ReplicaSet — 'a control loop you can watch working in real time.' B2 calls this the second beat
of the book's spine."*

## Definition (verbatim)

> A ReplicaSet's purpose is to **maintain a stable set of replica Pods running at any given
> time.** [source: k8s-docs-replicaset-2026-08-24]

Full form: "defined with a selector that specifies how to identify Pods it can acquire, a
number of replicas indicating how many Pods it should be maintaining, and a Pod template
specifying the data of new Pods it should create to meet the replica count criteria. It fulfills
its purpose by creating and deleting Pods as needed to reach the desired number."
[source: k8s-docs-replicaset-2026-08-24]

## The mapping onto Chapter 3's loop — exact, and the reason this section exists

| Control loop (Ch 3 §6) | ReplicaSet |
|---|---|
| Desired state | `.spec.replicas` — the number you asked for |
| Current state | The number of Pods matching its selector that actually exist |
| Action on a gap | Create Pods, or delete them |

The chapter's instruction: *"You don't need to be told to feel the recognition. You should be
able to see it."*

## The demonstration — two commands

Delete a Pod a ReplicaSet owns, then list Pods. A third appears in `ContainerCreating`.

> Nobody triggered that third Pod. Nothing was scheduled. No script ran. A gap appeared between
> "three wanted" and "two exist," and a loop that was already running noticed and closed it.

**Note the name.** The replacement is `qh7bl`, not the deleted `x8k2q` — "a *different* Pod,
with a different UID, built from the same template," exactly the behaviour Ch 5 §4 described.
[source: k8s-docs-pod-lifecycle-2026-08-23] This is the second time the book cashes the UID rule.

Documented contrast with a bare Pod, one line: "unlike the case where a user directly created
Pods, a ReplicaSet replaces Pods that are deleted or terminated for any reason, such as node
failure or disruptive node maintenance like a kernel upgrade."
[source: k8s-docs-replicaset-2026-08-24]

## ⚓ Worth Securing (verbatim — canonical)

> **Self-healing and scaling are the same operation.** There is no "recovery mode" that switches
> on when something fails. The loop only ever sees a number it wanted and a number it has, and it
> only ever does one thing about the difference. Everything that looks like resilience in
> Kubernetes is this, wearing a different name.

The chapter earns this by showing both cases and noting: *"The loop cannot tell those situations
apart, and doesn't try to."*

## 🔭 Closer Look — the controller does not create Pods itself

"Built-in controllers manage state by interacting with the cluster API server — the Job
controller, for instance, does not run any Pods or containers itself; instead it tells the API
server to create or remove Pods, and other components in the control plane act on that new
information." [source: k8s-docs-controllers-2026-08-23]

> Chapter 3 established that nobody is in charge. It stays true at this altitude: the ReplicaSet
> controller is **not a supervisor process holding your Pods. It's a program writing to an API.**

## Scaling

"Horizontal scaling means changing the number of replicas."
[source: k8s-docs-autoscaling-2026-08-23] "A ReplicaSet can be scaled up or down by simply
updating the `.spec.replicas` field." [source: k8s-docs-replicaset-2026-08-24]

When the thing writing `.spec.replicas` isn't you, it's usually a **HorizontalPodAutoscaler** —
"an API resource plus a controller that periodically adjusts the desired scale of its target to
match observed metrics such as average CPU utilization." [source: k8s-docs-hpa-2026-08-24] "A
ReplicaSet can itself be a target for an HPA." [source: k8s-docs-replicaset-2026-08-24]
Autoscaling landscape reserved → Ch 17.

## Related

[[control-loop]] · [[workload-resource]] · [[deployment]] · [[label-selector]] ·
[[owner-reference]] · [[controller-adoption]] · [[pod-lifetime]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/owner-reference.md ===
# Concept: Owner references and cascading deletion

**Home:** Chapter 6 §3 · **Competency:** D1.1 · **Status:** canonical

## The distinction this shard exists to protect

**Selectors and ownership are two different mechanisms**, and the docs say so explicitly. The
chapter states the split in one line:

> Selectors answer "**which Pods should I be looking at.**" Ownership answers "**which Pods am I
> responsible for**," and it's a separate mechanism.

Do not collapse these. A reader who thinks ownership *is* the selector cannot explain adoption,
cascading deletion, or why the docs describe them as distinct.

## Definition (verbatim)

> A ReplicaSet is linked to its Pods via the Pods' **`metadata.ownerReferences`** field, which
> specifies what resource the current object is owned by. All Pods acquired by a ReplicaSet carry
> the owning ReplicaSet's identifying information in that field, and it is through this link that
> the ReplicaSet knows the state of the Pods it's maintaining.
> [source: k8s-docs-replicaset-2026-08-24]

More broadly: "many objects in Kubernetes link to each other through owner references, which tell
the control plane which objects are dependent on others."
[source: k8s-docs-garbage-collection-2026-08-24]

## The docs' own example of the two-mechanism split

Using a Service and its EndpointSlices: **labels determine *which* EndpointSlices belong to the
Service**, and **owner references keep different parts of Kubernetes from interfering with objects
they don't control.** [source: k8s-docs-garbage-collection-2026-08-24]

## What ownership buys — cascading deletion

> Kubernetes checks for and deletes objects that no longer have owner references — like the Pods
> left behind when you delete a ReplicaSet — and when you delete an object you can control whether
> its dependents are deleted automatically.
> [source: k8s-docs-garbage-collection-2026-08-24]

In practice: **delete the Deployment, and the ReplicaSets and Pods go with it.** "To delete a
ReplicaSet and all of its Pods, use `kubectl delete`; the garbage collector automatically deletes
all of the dependent Pods by default." [source: k8s-docs-replicaset-2026-08-24]

## ⚑ Deliberately out of scope — do not add

Foreground vs background cascading deletion, finalizers, and `blockOwnerDeletion` are real and
documented [source: k8s-docs-garbage-collection-2026-08-24] and the chapter names them as such
before declining to teach them. That is the correct associate-tier boundary. A later chapter
adding them here would break the level.

## Forward note the chapter publishes

Deleting a workload does **not** automatically delete everything it merely *referenced* — a
distinction that becomes load-bearing with storage. Beared to Ch 12 §3, and it is the same fact
that makes StatefulSet volume retention safe. See [[statefulset]].

## Related

[[replicaset]] · [[controller-adoption]] · [[label-selector]] · [[workload-resource]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/controller-adoption.md ===
# Concept: Adoption, and the overlapping-selector hazard

**Home:** Chapter 6 §3 · **Competency:** D1.1 · **Status:** canonical
**Why its own shard:** this is the sharpest available proof that *membership is a query*, and the
hazard it implies is one of the book's registered trap-register entries.

## ★ Fixed Point (verbatim — canonical retrieval string)

> **A controller's Pods are the Pods that match its selector. Membership is a query, not a list —
> which is why the Pod template's labels must satisfy the selector, and why two controllers whose
> selectors overlap are a hazard rather than a curiosity.**

## Adoption (verbatim)

> A ReplicaSet identifies new Pods to acquire using its selector: if there's a Pod that has no
> owner reference, or whose owner reference is not a controller, and it matches a ReplicaSet's
> selector, it will be **immediately** acquired by that ReplicaSet.
> [source: k8s-docs-replicaset-2026-08-24]

The chapter's emphasis, worth keeping: *"Immediately. Not 'on the next reconcile as a special
case' — this **is** the reconcile."*

**⚑ Terminology note.** That sentence is the fourth chapter in which the book uses
*reconcile/reconciliation* without ever having defined it. See `glossary.md` § reconciliation and
[[control-loop]]'s open terminology gap.

## The two orderings, worked

| You create bare matching Pods… | Result |
|---|---|
| **After** the ReplicaSet reached its count | "The new Pods are acquired and then **immediately terminated**, because the ReplicaSet is now over its desired count." |
| **Before** | "The ReplicaSet adopts them and only creates as many new Pods as it needs to reach the count." |

[source: k8s-docs-replicaset-2026-08-24] — which is why the docs recommend making sure bare Pods
don't carry labels matching a ReplicaSet's selector.

> This is the sharpest possible demonstration that membership is a query. **The ReplicaSet is not
> limited to owning Pods created from its own template. It owns what matches.**

## 🪝 Snag (verbatim — canonical)

> Two controllers whose selectors overlap will fight over the same Pods — **and neither one
> reports an error.** Each sees a count that keeps changing for reasons it didn't cause, and each
> keeps acting on it. It looks like flapping, not like a configuration mistake, which is why it's
> expensive to diagnose.

Docs warning: "be careful not to overlap with the selectors of other controllers, lest they try to
adopt this Pod." [source: k8s-docs-replicaset-2026-08-24]

## ⚑ There is no API validation against overlap

The API enforces **selector–template agreement** *within* one object — `.spec.template.metadata.labels`
must match `spec.selector` or the object is rejected, for ReplicaSet
[source: k8s-docs-replicaset-2026-08-24], Deployment
[source: k8s-docs-deployment-spec-fields-2026-08-24], and DaemonSet
[source: k8s-docs-daemonset-2026-08-24].

It does **not** police overlap *across* objects. Two Deployments in one namespace can both select
`tier: web` and neither will error.

⚑ **This negative is the basis of Practice Q5's keyed answer** ("there is no such validation"), and
`fact-accuracy.md` flags it as resting on an **uncited negative** — the cached docs document the
hazard but say nothing about whether an error is emitted. Under skill Part 14 guardrail 4, the
answer key needs softening or a new fetch. **The item is in the shipping text.** Recorded here so
the shard does not harden an uncited claim into canon.

## The practical rule the chapter gives

> Give each workload a label that is genuinely unique to it, and don't hand-write labels that
> overlap across controllers. **This is the fifteen seconds of care that saves the afternoon.**

## Not a conflict: a Service selecting the same Pods

"A Service selects its backends with the same mechanism — a *different* controller reading the
*same* labels." That is not overlap; "it's the point of a shared identifying vocabulary." Beared to
Ch 9 §2, and it is what Bearings #1 Q5 tests.

## Related

[[label-selector]] · [[owner-reference]] · [[replicaset]] · [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/rolling-update.md ===
# Concept: Rolling updates, and what makes one safe

**Home:** Chapter 6 §4 · **Competency:** D1.1 + **D3.1** (research gap G8)
**Status:** canonical · **Chapter's densest block** (Attention Budget rates §4 the only *high*)

## The mechanism (verbatim)

> You declare the new state of the Pods by updating the PodTemplateSpec of the Deployment. **A new
> ReplicaSet is created,** and the Deployment manages moving the Pods from the old ReplicaSet to
> the new one at a controlled rate. [source: k8s-docs-deployment-2026-08-23]

**Two ReplicaSets exist at once.** One scaling down, one scaling up, the Deployment holding both.
This is [[workload-resource]]'s three-layer chain earning its keep, and it is normal mid-rollout
state — not a transient artifact.

## ★ Fixed Point (verbatim — do not reword)

> **`RollingUpdate` is the default strategy. `maxSurge` and `maxUnavailable` both default to 25%.
> `Recreate` kills all existing Pods before any new ones are created.**

## The two bounds

| Field | Meaning | Rounding | Default |
|---|---|---|---|
| **`maxSurge`** | max Pods that can be created **over** the desired number | **up** | **25%** |
| **`maxUnavailable`** | max Pods that can be **unavailable** during the update | **down** | **25%** |

[source: k8s-docs-deployment-spec-fields-2026-08-24]

"Neither can be `0` if the other is `0`" — *"with no headroom above and no slack below, there is no
legal move."*

🪢 **Mnemonic (canonical):** **Surge is above the line. Unavailable is below it.**

**Worked once, at ten replicas:** surge = 25% of 10 = 2.5 → **3** (up); unavailable = 25% of 10 =
2.5 → **2** (down). Total may reach 13; at least 8 must stay available. The docs work the same
shape at 30%: total ≤ 130% of desired, available ≥ 70%.
[source: k8s-docs-deployment-spec-fields-2026-08-24]

⚑ **Question-design note.** Practice Q7 uses **8 replicas**, where both values come out whole and
nothing rounds — so the item cannot test the rounding asymmetry, and its options A and B assert
identical cluster state. `question-quality.md` recommends `replicas: 6`. **Unapplied.** The
*concept* is correct here; the *item* does not exercise it.

## `Recreate` — a strategy, not a mistake

> All existing Pods are killed before new ones are created.
> [source: k8s-docs-deployment-2026-08-23]

The chapter's defence, which is also a voice exemplar candidate:

> That gap in the timeline is downtime, **deliberately chosen.** It exists because some
> applications genuinely cannot have two versions running at once — a schema migration that the old
> code can't read, an exclusive lock on a resource, a licence that permits one active instance. In
> those cases `Recreate` isn't the wrong answer; **it's the correct answer with a known cost**…
> Choosing `RollingUpdate` for an application that can't tolerate two concurrent versions is the
> actual mistake, and it fails in a subtler and more expensive way.

⚑ **Registered trap:** *"`Recreate` is a mistake."* Treating a supported strategy as an error is
itself a trap.

## What makes it safe — the readiness gate

A gradual replacement is not automatically a safe one: *"Replacing ten Pods slowly with ten broken
Pods is still replacing ten Pods with ten broken Pods; it just takes longer to finish being wrong."*

The safety property, and it is a **composition of two facts from two chapters**:

1. A new Pod does not count as **available** until it reports ready and stays ready for
   `minReadySeconds` — "the minimum number of seconds for which a newly created Pod should be ready,
   without any of its containers crashing, for it to be considered available; it defaults to 0."
   [source: k8s-docs-deployment-spec-fields-2026-08-24]
2. **Ch 5 §7:** a readiness probe "indicates whether a container is ready to respond to requests;
   when it fails, the endpoints controller removes the Pod's IP address from the endpoints of all
   Services matching the Pod." [source: k8s-docs-pod-lifecycle-2026-08-23]

> **A new version that never becomes ready never displaces the old one.** The new Pods start. They
> don't report ready. They therefore don't count as available. The Deployment can't scale down the
> old ReplicaSet any further without breaching `maxUnavailable` — so it doesn't. The rollout stalls,
> both ReplicaSets alive, old Pods still serving, and *nobody outside the cluster notices anything
> at all.*

This discharges Ch 5's published promise that "probes are what make a rolling update safe." It is
the moment probes stop being a health-checking feature and become a **release-safety mechanism.**

**The opt-out is real and worth stating:** "a Pod with no readiness probe is ready as soon as its
containers are running, whether or not the application inside can serve anything."

## 🪝 Snag — a stalled rollout is not a failed one

"Deployments can get stuck trying to deploy a newest ReplicaSet without ever completing, from causes
including insufficient quota, readiness probe failures, image pull errors, insufficient permissions,
and limit ranges." [source: k8s-docs-deployment-spec-fields-2026-08-24]

`.spec.progressDeadlineSeconds` (default **600**) turns the silence into a reported condition:
`type: Progressing`, `status: "False"`, `reason: ProgressDeadlineExceeded`.

⚑ **Note the wording: the controller *keeps retrying*. The deadline reports; it does not abort.**

## Figures

- `ch06-fig02-rolling-update-maxsurge-maxunavailable` — surge ceiling above, availability floor
  below, old/new bands crossing. The two horizontal bounds are the pedagogy.
- `ch06-fig03-recreate-vs-rolling` — the caption on the Recreate gap is load-bearing:
  **"NOTHING IS AVAILABLE (this window is the whole point)."** Do not soften it in a redraw.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 13 §3** | Diagnosing a stuck rollout — what to run, which events, what next. §4 explicitly defers diagnosis. |
| **Ch 15 §4** | Deployment strategy *vocabulary* — blue/green, canary, A/B. §4 teaches mechanics only and says so. |

## Related

[[deployment]] · [[deployment-revision]] · [[probe]] · [[replicaset]] · [[workload-resource]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/deployment-revision.md ===
# Concept: Revisions, rollout verbs, and rollback

**Home:** Chapter 6 §5 · **Competency:** D1.1 + **D3.1** (research gap G8)
**Status:** canonical

## ★ Fixed Point (verbatim — do not reword)

> **A new revision is created if and only if `.spec.template` changes. Scaling does not create a
> revision.**

Source form: "a new revision is created **if and only if** the Deployment's Pod template
(`.spec.template`) is changed. Other updates, such as scaling the Deployment, do not create a
Deployment revision." [source: k8s-docs-deployment-2026-08-23]

The chapter is explicit about *why* the exactness is the content: *"the intuitive answer ('any
change to the Deployment') is wrong and the correct answer is one clause long"* — precisely the
shape a recognition exam builds an item from.

## The test, and the worked cases

> **The test is not "did I edit the Deployment." It is "did I edit `.spec.template`."**

| Change | Revision? | Why |
|---|---|---|
| Scale 3 → 6 | **no** | count is not in the template |
| Change the container image | **yes** | image lives in the template |
| Change an env var in the template | **yes** | |
| Change `maxSurge` | **no** | `.spec.strategy` is a *sibling* of `.spec.template` |
| Change a label on the template's Pods | **yes** | the template changed |
| Change `revisionHistoryLimit` | **no** | retention policy, not template |

## The verb surface — small and closed

| Command | What it does |
|---|---|
| `kubectl rollout status` | Show the status of the rollout |
| `kubectl rollout history` | View rollout history |
| `kubectl rollout undo` | Undo a previous rollout (`--to-revision=<n>` for a specific one) |
| `kubectl rollout pause` | Mark the provided resource as paused |
| `kubectl rollout resume` | Resume a paused resource |
| `kubectl rollout restart` | Restart a resource |

[source: k8s-docs-kubectl-rollout-2026-08-24] Valid resource types include deployments, daemonsets,
and statefulsets. [source: k8s-docs-kubectl-overview-2026-08-23]

**Pause/resume needs its motivation attached** or it reads as an arbitrary pair. Three edits applied
one at a time = three rollouts, three revisions, three sets of Pod churn, "and the first two are
rolling out versions nobody wanted." Pause, edit thrice, resume = one rollout, one revision.

⚓ **Worth Securing:** "`pause` before a batch of edits. It is the difference between one rollout and
four, and it costs one command."

## What's kept

"By default, all of a Deployment's rollout history is kept in the system so that you can roll back
any time you want." [source: k8s-docs-deployment-2026-08-23] `.spec.revisionHistoryLimit` "specifies
the number of old ReplicaSets to retain to allow rollback; **by default, 10 old ReplicaSets will be
kept.** Setting it to zero means all old ReplicaSets with 0 replicas are cleaned up — and in that
case a new Deployment rollout cannot be undone."
[source: k8s-docs-deployment-spec-fields-2026-08-24]

*"'Can I still roll back?' is a real question at a real bad moment, and the default answer is yes,
ten deep."*

## ⚠ Navigational Hazards (verbatim — canonical, both directions)

> **Hazard one: "I changed the Deployment, so there must be a new revision."** Scaling is the
> counterexample that matters, because scaling is the most common Deployment edit there is.
>
> **Hazard two, which follows from it: "`rollout undo` will put my replica count back."** It will
> not. `rollout undo` restores a previous *Pod template*. Your replica count is not in the Pod
> template. If you scaled up and then rolled back an unrelated image change, you will still have six
> replicas afterward — and if you were expecting three, you will spend a while looking for the bug.
> **There isn't one.**
>
> The clean mental model: **revisions are a history of what your Pods are, not of how many.**

## What a rollback actually is

> Rolling back is not undoing an edit, and it is not restoring a backup. It is setting the Pod
> template to a previous value and letting the same rolling update run in the other direction — same
> controller, same two ReplicaSets, same `maxSurge` and `maxUnavailable`, same readiness gate. **The
> Deployment doesn't have a special reverse gear. It has one gear, and rollback points it at an
> older template.**

The old ReplicaSet is still there — that's what `revisionHistoryLimit` retains — so rollback "is
largely a matter of scaling it back up while scaling the current one down."

## ⚑ Three mechanisms share the word "rollback" — binding on two later chapters

| Mechanism | Operates on | Chapter |
|---|---|---|
| **Deployment rollback** | the Pod template | Ch 6 §5 (here) |
| **Helm rollback** | releases | **Ch 14 §5** |
| **GitOps rollback** | committed configuration, carried in by reconciliation | **Ch 15 §3** |

The chapter stakes a claim on this: *"Knowing what **this** one is is what makes the other two
distinguishable rather than confusing."* Both later chapters must honour the contrast explicitly.

## Related

[[rolling-update]] · [[deployment]] · [[replicaset]] · [[workload-resource]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/statefulset.md ===
# Concept: StatefulSet, and the interchangeability test

**Home:** Chapter 6 §6 · **Competency:** D1.1 · **Status:** canonical
**⚑ Contains the book's only intentional half-teach** — the storage half is deliberately deferred to
Ch 11 and the chapter tells the reader so.

## Definition (verbatim)

> A StatefulSet runs a group of Pods and **maintains a sticky identity for each of them** — useful
> for applications that need persistent storage or a stable, unique network identity.
> [source: k8s-docs-statefulset-2026-08-24]

The contrast sentence, and the chapter says to read it slowly:

> Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec;
> *unlike* a Deployment, a StatefulSet maintains a sticky identity for each of its Pods — these Pods
> are created from the same spec, but **are not interchangeable**: each has a persistent identifier
> that it maintains across any rescheduling. [source: k8s-docs-statefulset-2026-08-24]

> **Same spec. Not interchangeable. Those two facts sitting together is the entire concept.**

## ★ Fixed Point (verbatim — do not reword)

> **The property that decides Deployment versus StatefulSet is *interchangeability*, not disk. A
> StatefulSet is for related Pods with stable identities, each typically paired with its own durable
> storage.**

## Identity has three parts

[source: k8s-docs-statefulset-2026-08-24]

- **An ordinal index.** "For a StatefulSet with N replicas, each Pod is assigned an integer ordinal,
  unique over the set, from 0 through N-1."
- **A stable network identity.** "Each Pod derives its hostname from the StatefulSet's name and its
  ordinal: `$(statefulset name)-$(ordinal)`." A StatefulSet `web` with three replicas produces
  `web-0`, `web-1`, `web-2` — "every time, on every reschedule."
- **Stable storage.** "For each `volumeClaimTemplate` entry, each Pod receives one
  PersistentVolumeClaim, and the same claim is bound to that Pod throughout its lifecycle."

**Ordering is part of identity too.** "Pods are created sequentially in order from 0 to N-1… when
they're deleted they're terminated in reverse order, N-1 down to 0. Before a scaling operation is
applied to a Pod, all of its predecessors must be Running and Ready." — *"you cannot bring up a
replica before the primary it replicates from."*

## 🪝 Snag — the misconception this shard exists to kill (verbatim)

> The wrong version of this, which most people arrive holding, is: ***"if my application writes to
> disk, I need a StatefulSet."*** It isn't true, and believing it will send you to the harder
> resource for no benefit. A stateless web server can write to disk. A Deployment's Pod can mount a
> volume [source: k8s-docs-pods-2026-08-24] [source: k8s-docs-volumes-2026-08-23]. **The question is
> never "does it write." It's "if I destroyed this Pod and built an identical one, would anything
> care *which one it was*?"** If nothing cares, it's a Deployment, disk or no disk. If something
> cares — a hostname in a replication config, a specific shard of data, an election that assumed a
> fixed member list — that's a StatefulSet.

Registered as a book-level trap-register entry. **Do not paraphrase the operational test**; it is the
retrieval string.

## The selector does not carry this

Two Pods matching the same selector may be freely substitutable (Deployment) or may each hold a
distinct identity and its own storage (StatefulSet). **The distinction lives in the resource kind,
not in the labels.** This is what Practice Q14 is built on — see the ⚑ below.

⚑ **Practice Q14 is the chapter's most severe question-quality defect and is unapplied.** Three of
four options are defensible; the key concedes it rather than resolving it. Skill Part 10B classifies
this as *undesirable* difficulty. `question-quality.md` supplies a drop-in replacement stem that also
closes the `matchLabels`/`matchExpressions` coverage gap. **The concept here is sound; the item
testing it is not.**

## Extended Analogy (verbatim — voice-exemplar candidate)

> On a Deployment crew, any bosun's mate can stand any watch… The roster is a number and a
> description: *four hands who can do this.*
>
> On a StatefulSet crew, the pilot who knows this harbour is the pilot who knows *this* harbour. Her
> replacement is not another pilot; her replacement is someone who has to have learned the same
> channel, and until they have, the post is not filled — it is merely occupied…
>
> **Both crews are three or four people. Only one of them can be described by a count.**

## ⚑ The deliberate deferral — a published promise to the reader

§6 tells the reader outright what was skipped and why: *"What this chapter owes you is the
**taxonomy**: which resource, and why. What that chapter owes you is how the storage actually
works."*

Two documented limitations flagged forward now "so they don't surprise you later":

- storage "must either be provisioned by a PersistentVolume provisioner based on the requested
  storage class or pre-provisioned by an admin"
- "deleting or scaling down a StatefulSet does **not** delete the associated volumes" —
  deliberately, "because data safety is generally more valuable than an automatic purge"

[source: k8s-docs-statefulset-2026-08-24]

**Headless Service:** "StatefulSets currently require a Headless Service to be responsible for the
network identity of the Pods, and **you are responsible for creating it.**"
[source: k8s-docs-statefulset-2026-08-24]

## Figure

`ch06-fig05-statefulset-vs-deployment-identity` — two stacked panels. The caption that carries the
concept: **"storage belongs to the IDENTITY, not to the Pod"** with `db-2`'s replacement reattaching
to the same claim. Preserve that annotation in any redraw.

## Downstream obligations — binding

| Chapter | Obligation |
|---|---|
| **Ch 11 §4** | PV, PVC, StorageClass, access modes, `volumeClaimTemplate` provisioning. **A published promise.** |
| **Ch 9 §5** | Headless Services — the mechanism behind `db-0` being resolvable by name. |
| **Ch 16 §3** | Debugging StatefulSets — named explicitly in the exam's troubleshooting competency. |
| **Ch 12 §3** | What deletion does and does not remove. |

## ⚑ Inbound pointer repair required

`chapter-01-taking-departure.md:436` publishes `*[cross-bearing: see Ch 6 §3 — StatefulSets and
stable identity]*`. StatefulSets are **§6**. One-token edit in the shipped Chapter 1 text; do not
renumber Chapter 6 (six other inbound pointers and the outline depend on the current order).

## Related

[[deployment]] · [[workload-resource]] · [[daemonset]] · [[label-selector]] · [[pod-lifetime]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/daemonset.md ===
# Concept: DaemonSet

**Home:** Chapter 6 §7 · **Competency:** D1.1 · **Status:** canonical

## Definition (verbatim)

> A DaemonSet defines Pods that provide facilities local to nodes. **Every time you add a node to
> your cluster that matches the specification in a DaemonSet, the control plane schedules a Pod for
> that DaemonSet onto the new node.** Each Pod in a DaemonSet performs a job similar to a system
> daemon on a classic Unix server. [source: k8s-docs-workloads-2026-08-23]

From the other page: "ensures that all (or some) Nodes run a copy of a Pod — as nodes are added to
the cluster, Pods are added to them; as nodes are removed, those Pods are garbage collected."
[source: k8s-docs-daemonset-2026-08-24]

## ★ Fixed Point (verbatim, shared with [[job]] and [[cronjob]])

> **DaemonSet: one Pod per matching node, added automatically as nodes join — no replica count.**

## ⚑ The count is a consequence, not a setting

This is the registered trap and the chapter's sharpest DaemonSet fact.

> A DaemonSet does not take a replica count; its Pod count is a **consequence** of how many nodes
> are eligible, since the controller creates a Pod for each eligible node.
> [source: k8s-docs-daemonset-2026-08-24]

Clearest corroboration, from the autoscaler: "horizontal pod autoscaling does not apply to objects
that can't be scaled — for example, a DaemonSet." [source: k8s-docs-hpa-2026-08-24] **There's no
number to adjust.**

⚑ **Research gap G-6A, carried forward.** No fetched sentence states verbatim that a DaemonSet has no
`replicas` field. The claim is entailed two independent ways (per-eligible-node creation; HPA
inapplicability), and the prose correctly states it **as a consequence rather than as a quoted
fact.** The draft's own AUTHOR-REVIEW comment asked revision to confirm that framing; the revision
stage confirmed it and sharpened the Exam Alert wording to match. **Framing is settled — do not
re-raise.**

⚑ Registered trap: *"I need six copies, so I'll use a DaemonSet."* The chapter's rebuttal is worth
keeping: "If you want six copies, you want a Deployment; if you want *one on each machine*, you want
a DaemonSet — and if the cluster has four nodes today and nine next month, **that's a feature.**"

## Narrowing the node set

"If you specify a `nodeSelector` in the Pod template, the DaemonSet controller creates Pods only on
nodes matching that selector; likewise for node affinity. **If you specify neither, the controller
creates Pods on all nodes.**" [source: k8s-docs-daemonset-2026-08-24]

The Pods still go through scheduling — the controller creates a Pod per eligible node and the default
scheduler binds it. The controller "automatically adds a set of tolerations so DaemonSet Pods can run
on nodes that are unschedulable, under disk or memory pressure, or not yet ready."
[source: k8s-docs-daemonset-2026-08-24]

**⚑ This is a Chapter 7 seam the Voyage Ahead names explicitly:** "The DaemonSet's tolerations in §7
were a node saying 'not for general traffic' and a controller saying 'this one's an exception.'" Ch 7
§5 must land taints/tolerations against this already-planted instance.

## Documented uses, and two that come back

"Running a cluster storage daemon on every node, running a logs collection daemon on every node,
running a node monitoring daemon on every node." [source: k8s-docs-daemonset-2026-08-24]

Grouped by role: "fundamental to the operation of your cluster, such as a plugin to run cluster
networking"; "help you manage the node"; or "provide optional behaviour that enhances the container
platform." [source: k8s-docs-workloads-2026-08-23]

| Held concretely for | Chapter |
|---|---|
| Networking plugins ship as DaemonSets | **Ch 9 §7** |
| Node-level log agents — the canonical observability example | **Ch 18 §3** |

## Related

[[workload-resource]] · [[deployment]] · [[statefulset]] · [[job]] · [[node-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/job.md ===
# Concept: Job — work that ends

**Home:** Chapter 6 §7 · **Competency:** D1.1 · **Status:** canonical
**Retroactively justifies:** two of Chapter 5's five Pod phases.

## Definition (verbatim)

> A Job represents a one-off task that **runs to completion and then stops.** A Job creates one or
> more Pods and continues to retry execution until a specified number of them successfully
> terminate; when that number is reached, the Job is complete. [source: k8s-docs-job-2026-08-24]

"You can use a Job to define a task that runs to completion, just once."
[source: k8s-docs-workloads-2026-08-23]

## Same loop, different desired state

The Job controller was Chapter 3's own worked example of a built-in controller. Collecting it here:

> When the Job controller sees a new task, it makes sure that somewhere in your cluster the kubelets
> on a set of nodes are running the right number of Pods to get the work done — and once the work is
> done, the Job controller updates the Job object to mark it Finished.
> [source: k8s-docs-controllers-2026-08-23]

> **Same loop. Different desired state: *completion* rather than *a count*.**

## ⚑ Level distinction — Pod phase vs Job condition

**Wording adopted from the revision stage** (Practice A16), which is sharper than §7's prose and
correct at the API level:

- **`Succeeded`** is a **Pod phase** — "all containers terminated in success and will not be
  restarted." [source: k8s-docs-pod-lifecycle-2026-08-23]
- The **Job object itself** finishes as **`Complete`** (or `Failed`).
  [source: k8s-docs-job-2026-08-24]

§7's prose gives only the Ch 3 form ("mark it Finished"). Practice Q16 asks about the Pod level and
its key states the distinction explicitly. **Keep both levels; they are separate questions.**

## Why Chapter 5's phases finally earn their place

Chapter 5 taught five Pod phases, and two of them had no obvious use — "a long-running service that
reaches `Succeeded` has malfunctioned." [source: k8s-docs-pod-lifecycle-2026-08-23]

> **Work that ends is work that reaches a terminal phase, and for a Job those two phases are the
> entire scoreboard.**

This is one of the book's cleanest delayed payoffs: a fact taught in Ch 5 §5 with an acknowledged
absence of motivation, motivated two chapters later.

## One field difference, following directly

"For a Job, only a `restartPolicy` of `Never` or `OnFailure` is allowed."
[source: k8s-docs-job-2026-08-24]

> `Always` would be a **category error** — restarting a process that succeeded is precisely what you
> don't want.

## Related

[[cronjob]] · [[pod-phase]] · [[restart-policy]] · [[control-loop]] · [[workload-resource]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cronjob.md ===
# Concept: CronJob

**Home:** Chapter 6 §7 · **Competency:** D1.1 · **Status:** canonical

## Definition (verbatim)

> A CronJob creates **Jobs** on a repeating schedule. [source: k8s-docs-cronjob-2026-08-24]

"You can use a CronJob to run the same Job multiple times according to a schedule."
[source: k8s-docs-workloads-2026-08-23]

## The canonical mental model, from the docs

> One CronJob object is like **one line of a crontab file** on a Unix system. It runs a Job
> periodically on a given schedule, written in Cron format. [source: k8s-docs-cronjob-2026-08-24]

## The relationship is nested, not parallel

> **A CronJob's output is Jobs. It doesn't run work; it creates the thing that runs work.**

Canonical retrieval string. ⚑ Registered trap: *"Job and CronJob do the same thing."* Practice Q17's
distractor A ("seven Pods, directly") skips the Job layer — the exact misconception the distinction
exists to prevent.

## Fields

| Field | Definition |
|---|---|
| **`.spec.schedule`** | Required; standard five-field cron syntax. `0 3 * * 1` = weekly on a Monday at 3 a.m. |
| **`.spec.jobTemplate`** | "defines the Jobs the CronJob creates, and has **exactly the same schema as a Job**" |

[source: k8s-docs-cronjob-2026-08-24]

## 🔭 Closer Look — scheduling is approximate, so Jobs must be idempotent

> A CronJob creates a Job **approximately** once per execution time of its schedule. The scheduling
> is approximate — there are circumstances where **two Jobs might be created, or no Job might be
> created.** Kubernetes tries to avoid those situations but does not completely prevent them, which
> is why the docs state that the Jobs you define should be **idempotent.**
> [source: k8s-docs-cronjob-2026-08-24]

The chapter's landing: *"If your nightly report generator would double-bill a customer when run
twice, that's a design problem the scheduler will eventually find for you."*

⚑ This is a **subject-dignity-clean** stakes beat under skill v5.7 — the consequence lands on the
practitioner's design choice, not on the customer as a punchline. Worth preserving as written.

## Related

[[job]] · [[workload-resource]] · [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/custom-resource.md ===
# Concept: Custom resources and CustomResourceDefinitions

**Home:** Chapter 6 §8 · **Competency:** D1.1 (⚑ also **D4.2**) · **Status:** canonical
**Closes:** research gap **G10** · **Discharges:** Chapter 2 §4's promised fourth socket
**Difficulty:** 🟡 — the chapter's only advanced-band section, and its abstraction jump

## Start with the resource, not the pattern

The chapter's teaching order is deliberate and should be preserved: **resource → custom resource →
CRD → the limitation → the pattern.** Opening with "operator" teaches a buzzword; opening with
"resource" teaches a mechanism.

> A **resource** is an endpoint in the Kubernetes API that stores a collection of API objects of a
> certain kind — the built-in `pods` resource, for instance, contains a collection of Pod objects.
> [source: k8s-docs-custom-resources-2026-08-23]

## Custom resource (verbatim)

> A **custom resource** is an extension of the Kubernetes API that is not necessarily available in a
> default Kubernetes installation; it represents a customization of a particular Kubernetes
> installation. Custom resources can appear and disappear in a running cluster through **dynamic
> registration**, and cluster admins can update them independently of the cluster itself.
> [source: k8s-docs-custom-resources-2026-08-23]

**The clause the chapter says makes it click:**

> Once a custom resource is installed, users can create and access its objects using `kubectl`, just
> as they do for built-in resources like Pods.

> Nothing about your tooling changes. `kubectl get backup` works the same way `kubectl get pods`
> does, because **as far as `kubectl` is concerned there was never a difference.**

"Many core Kubernetes functions are now built using custom resources, which is what makes Kubernetes
as modular as it is." [source: k8s-docs-custom-resources-2026-08-23]

## CustomResourceDefinition (verbatim)

> The **CustomResourceDefinition** API resource allows you to define custom resources. Defining a CRD
> object creates a new custom resource with a name and schema that you specify, and the Kubernetes
> API then serves and handles the storage of your custom resource — which frees you from writing your
> own API server, at the cost of some flexibility compared with API server aggregation.
> [source: k8s-docs-custom-resources-2026-08-23]

> **You write a schema. The cluster gives you a working API endpoint for it. That's the whole
> transaction.**

⚑ **First mention of `CRD` in the book is Chapter 2 line 600, as a bare unexpanded acronym.** The
expansion arrives only here. Glossary row must record both.

## ★ Fixed Point (verbatim — do not reword)

> **A custom resource alone stores and retrieves structured data. A custom resource plus a custom
> controller is the operator pattern.**

## The honest limitation

> On their own, custom resources let you store and retrieve structured data. **That is all.** A CRD by
> itself is a shape in a database with an HTTP interface in front of it. You can create objects; you
> can list them; you can delete them. **Nothing acts on them.**

## Custom controller and the declarative API

> When you combine a custom resource with a **custom controller**, custom resources provide a true
> declarative API. The Kubernetes declarative API enforces a **separation of responsibilities**: you
> declare the desired state of your resource, and the Kubernetes controller keeps the current state of
> Kubernetes objects in sync with your declared desired state — in contrast to an imperative API, where
> you instruct a server what to do. [source: k8s-docs-custom-resources-2026-08-23]

The chapter's landing, which is the whole reason §8 exists:

> Read that "separation of responsibilities" sentence again and notice what it is. **It's Chapter 3's
> control loop, written by somebody who does not work on Kubernetes.**

## 🔭 API server aggregation — the other route

"Gives more flexibility at the cost of writing and operating your own API server"; the docs recommend a
custom resource "when your API is declarative, you want `kubectl` and dashboard support, and your
resources are naturally cluster- or namespace-scoped."
[source: k8s-docs-custom-resources-2026-08-23] "For nearly everything, and certainly for everything at
this level, the answer is a CRD."

## ⚑ Inbound pointer repair required

`chapter-02-cargo-in-standard-crates.md:600` publishes `*[cross-bearing: see Ch 6 §3 — CRDs and
extending the API]*`. CRDs are **§8**. One-token edit in shipped Chapter 2 text.

## Related

[[operator-pattern]] · [[absent-component-pattern]] · [[control-loop]] · [[kubernetes-object]] ·
[[declarative-configuration]] · [[api-server-hub]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/operator-pattern.md ===
# Concept: The operator pattern

**Home:** Chapter 6 §8 · **Competency:** D1.1 (⚑ also **D4.2**, **D3.1**) · **Status:** canonical
**Closes:** research gap **G10** (with [[custom-resource]])

## Definition (verbatim)

> The **operator pattern** combines custom resources and custom controllers.
> [source: k8s-docs-custom-resources-2026-08-23]

## Why it's called that

> The operator pattern aims to capture the key aim of a **human** operator who is managing a service or
> set of services — people who look after specific applications and have deep knowledge of how the
> system ought to behave, how to deploy it, and how to react if there are problems. The pattern captures
> how you can write code to automate a task beyond what Kubernetes itself provides.
> [source: k8s-docs-operator-pattern-2026-08-23]

> Operators are clients of the Kubernetes API that act as controllers for a custom resource, and the
> pattern lets you extend the cluster's behaviour **without modifying the code of Kubernetes itself.**
> [source: k8s-docs-operator-pattern-2026-08-23]

## What people automate with them — the docs' own list

Deploying an application on demand · taking and restoring backups of application state · handling
upgrades of application code alongside related changes such as database schemas or extra configuration ·
publishing a Service to applications that don't support Kubernetes APIs to discover them · simulating
failure in all or part of a cluster to test resilience · choosing a leader for a distributed application
without an internal member election process. [source: k8s-docs-operator-pattern-2026-08-23]

The chapter's reading of that list is the argument for the pattern:

> Read that list as a **job description** and you'll see the argument. Those are the things a
> knowledgeable human on-call would do at 3 a.m. The operator pattern is the claim that **they can be
> written down.**

## ⭐ The fact that closes the chapter's loop

> The most common way to deploy an operator is to add the CustomResourceDefinition and its associated
> controller to your cluster. **The controller will normally run outside of the control plane, much as
> you would run any containerized application — for example, as a Deployment.**
> [source: k8s-docs-operator-pattern-2026-08-23]

> The thing that extends Kubernetes is itself deployed *by* Kubernetes, using the resource from §1. An
> operator managing a production database is a Deployment: a Pod template, a replica count, a
> ReplicaSet, a control loop maintaining it. **It is not privileged infrastructure. It is a workload,
> exactly like yours, that happens to spend its time watching an API and creating objects.**

This is the structural payoff of the whole chapter and the reason §8 sits after §1 rather than in a
separate extensibility chapter. Practice Q19 and Bearings #3 Q5 both test it.

## The fourth socket — Chapter 2's debt, paid

"CRI let the ecosystem supply container runtimes; CNI, networking; CSI, storage; and **API extension**
lets the ecosystem supply *resource types and the controllers that act on them*" — the published
extension-points list names API extensions (CRDs and the aggregation layer) and controllers among them
explicitly. [source: k8s-docs-extending-kubernetes-2026-08-23]

⚑ **This is the FIRST named recurrence of Chapter 2 §4's "Kubernetes defines an interface and lets the
ecosystem implement it" theme.** Chapter 5's manifest recorded it at *"still zero named recurrences."*
**Discharged.**

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 14 §3** | A Helm chart's dedicated `crds/` directory — charts ship CRDs as content. [source: helm-charts-2026-08-23] |
| **Ch 15 §2** | "A certain widely-used delivery tool is implemented as a Kubernetes controller acting on custom resources, which will look like new technology right up until you notice it isn't." |
| **Ch 17 §2** | Collect all four pluggable interfaces into one story. §8 explicitly hands this over. |

## Related

[[custom-resource]] · [[control-loop]] · [[absent-component-pattern]] · [[deployment]] ·
[[workload-resource]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

---

## Chapter 6 update (2026-08-24) — ✅ the Ch 6 obligation is DISCHARGED, twice over

**Appended, not overwritten.** Chapter 3's canon is unchanged and uncontradicted by Chapter 6.

### Obligation discharged

This shard's downstream-obligations table read:

> | Ch 6 | Instantiate the loop in ReplicaSet — "a control loop you can watch working in real time."
> B2 calls this the second beat of the book's spine. |

**Chapter 6 §2 delivers it literally.** It opens by naming the debt — *"Chapter 3 promised you a control
loop you could watch working in real time, and named the ReplicaSet as the place you'd see it. This is
that."* — then supplies the exact mapping:

| Control loop (Ch 3) | ReplicaSet (Ch 6 §2) |
|---|---|
| Desired state | `.spec.replicas` |
| Current state | Pods matching the selector that actually exist |
| Action on a gap | Create Pods, or delete them |

And makes it observable in two commands: delete a Pod, list Pods, watch a third appear that nobody
asked for.

### §9 goes further than the obligation required — six controllers, one loop

Figure `ch06-zenith-control-loop-instantiated` draws the loop **once** with six desired-state inputs
feeding it. The argument is that there is only one loop, which is why the figure has a single centre
rather than six:

| Controller | Its desired state |
|---|---|
| ReplicaSet | a number |
| Deployment | a template plus an update policy |
| DaemonSet | *one per matching node* — "a number, but one the cluster computes rather than one you write" |
| Job | *completion* |
| CronJob | *a Job existing at each scheduled time* |
| Operator | "whatever its author decided a database, or a certificate, or a message queue ought to look like" |

The chapter's claim, and it is the strongest statement of this shard's thesis anywhere in the book:

> This shape is not a Kubernetes implementation detail. **It is the thing Kubernetes *is*.**

### ⭐ A published, checkable promise to Chapter 15

§9 tells the reader, in the shipped text:

> Chapter 15 will show you a controller whose desired state lives outside the cluster entirely, in a Git
> repository, and that will look like an entirely new technology right up until this section makes it
> look like the same one. **When you get there, come back and check this figure. It will be the same
> figure.**

This upgrades the Ch 15 row from an internal obligation to a **promise the reader can verify**. If
Chapter 15 redraws the loop rather than reusing this figure, the promise breaks visibly on the page.
**Binding on Ch 15's figure selection, not just its prose.**

### Obligation still open, now four chapters overdue

| Ch 11 | **Retrieve the control loop.** ⚑ Chapter 6 bears to Ch 11 §4 twice (StatefulSet storage) and carries the loop to neither. Ch 3, 4, 5, and 6 have each passed it forward. |

### ⚑ The `reconciliation` terminology gap is now four chapters old and in body prose

This shard's open gap — *"reconciliation" is never tied to "control loop"* — has compounded:

| Chapter | Use |
|---|---|
| Ch 3 | 3× including a pre-definition instruction to the reader; never bridged |
| Ch 4 | behaviour described 3×, word never used |
| Ch 5 | **2 graded answers** (Bearings #1 A5, Practice Q21) |
| **Ch 6** | **body prose ×2** — §3 *"this **is** the reconcile"*; §5 *"letting reconciliation carry it into the cluster"* |

The book grades readers on a word it promised to define and hasn't, and now teaches with it. **One
appositive at Chapter 3's ★ Fixed Point closes it.** Recommended at Ch 5, not done.

## Related (additions)

[[replicaset]] · [[workload-resource]] · [[job]] · [[cronjob]] · [[daemonset]] · [[operator-pattern]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/label-selector.md ===

---

## Chapter 6 update (2026-08-24) — first retrieval by name; no canon conflict

**Appended, not overwritten.** Chapter 4 remains the home. Nothing below contradicts it.

### ⚑ Attribution correction

`ch-06/outline.md`'s `kb_tags.concepts` lists `label-selector`, `matchlabels`, and `matchexpressions` as
concepts **introduced** at Ch 6 §3. **They are not.** Chapter 4 §5 introduces, sources, and Fixed-Points
them. Chapter 6 §3 *applies* them to a controller and adds consequences.

**Glossary cross-references for all three must read (Chapter 4).** A mechanical read of Chapter 6's
`kb_tags` will mint duplicate Chapter 6 rows.

### What Chapter 6 §3 adds — three things Chapter 4 did not state

**1. Membership is a query — stated as a rule, with the derivation.**

> A ReplicaSet does not track its Pods by name. It does not hold a list. It has a `.spec.selector`,
> which is a label selector, and its Pods are **whichever Pods match it.**
> [source: k8s-docs-replicaset-2026-08-24]

The chapter earns it with a generation-effect prompt: a Deployment whose template labels `app: web` but
whose selector seeks `app: frontend` creates Pods forever and can see none of them. *"The Pods are real,
running, and consuming resources, and the controller cannot see a single one of them."*

**2. Selector–template agreement is API-enforced — and the principle beneath the enforcement.**

`.spec.template.metadata.labels` must match `.spec.selector` or the object is rejected — for ReplicaSet
[source: k8s-docs-replicaset-2026-08-24], Deployment
[source: k8s-docs-deployment-spec-fields-2026-08-24], and DaemonSet
[source: k8s-docs-daemonset-2026-08-24].

> The validation is a kindness. The *principle* is what you need to carry: **because membership is
> computed rather than recorded, the labels a controller stamps on its own Pods have to satisfy the
> question it will later ask about them.**

**3. Ownership is a SEPARATE mechanism — the docs say so explicitly.**

This is the most important addition and the one most at risk of being collapsed by a later chapter.
Labels determine *which* objects belong; owner references "keep different parts of Kubernetes from
interfering with objects they don't control."
[source: k8s-docs-garbage-collection-2026-08-24] See [[owner-reference]] and [[controller-adoption]].

### One syntax detail Chapter 6 adds

"When both `matchLabels` and `matchExpressions` are specified, the result is **ANDed**."
[source: k8s-docs-labels-selectors-2026-08-23] [source: k8s-docs-daemonset-2026-08-24]

### Theme status — ✅ first retrieval BY NAME

Chapter 5 retrieved this theme once, unplanned, at Practice Q5. **Chapter 6 §3 is the first retrieval
that uses the canonical name and the first deep application.** It also honours Chapter 4's forward
bearing exactly: Ch 4 line 688 lists four selector users and points here for the ReplicaSet mechanism.

Bearings #1 Q5 does the theme's best work — it asks what it means for one Pod to be selected by both a
ReplicaSet and a Service, which is precisely the "one mechanism, four problems" claim this shard's
⚓ Worth Securing makes, converted into a graded item.

### The exception still holds

Chapter 6 does **not** disturb `⚑ THE EXCEPTION` — RBAC names its subjects explicitly and does not select
by label. Ch 6 touches RBAC nowhere. Chapter 12's inherited risk is unchanged.

### Figure reuse, correctly handled

§3 does not draw a new join figure. It reuses Chapter 4's: *"The join itself is drawn in
`ch04-fig03-labels-selectors-join`, and it hasn't changed — this is that same figure with a ReplicaSet on
the left and Pods on the right."* Good practice; record it as precedent.

## Related (additions)

[[replicaset]] · [[owner-reference]] · [[controller-adoption]] · [[statefulset]] · [[daemonset]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

---

## Chapter 6 update (2026-08-24) — ⚑ FIRST RECURRENCE, AND IT WAS RE-COINED

**Appended, not overwritten — deliberately.** This chapter disagrees with the canon above, and
overwriting would erase the wording this shard exists to protect.

### The good news, first

**Chapter 6 §8 is the pattern's first recurrence anywhere in the book.** Chapter 5's manifest recorded it
at *"still zero, two chapters on."* The instance is a strong one — installing a CRD and having nothing
happen is a textbook case, and the 🪝 Snag teaches it cleanly:

> "We installed the CRD but nothing happened." **That is the correct behaviour, not a bug. You installed
> a place to put data. You did not install anything that reads it.**

**And Chapter 6 closes this shard's count gap.** The table above recorded instance #4 —
NetworkPolicy-on-a-non-enforcing-CNI — as B3's fourth and **missing** from Chapter 3's bearings. §8 names
all four, with a source tag on the last:

| # | Instance | Named in Ch 6 §8? |
|---|---|---|
| 1 | Ingress without an Ingress controller | ✓ beared to Ch 10 §3 |
| 2 | `kubectl top` without metrics-server | ✓ beared to Ch 13 §2 |
| 3 | VPA is an add-on, not shipped by default | ✓ [source: k8s-docs-autoscaling-2026-08-23], beared to Ch 17 §5 |
| 4 | **NetworkPolicy without a controller that implements it** | ✓ [source: k8s-docs-network-policies-2026-08-23] — **the previously missing bearing** |

### ⚑ The problem: the canonical name was not used

This shard's instruction, in capitals:

> **⚑ USE THIS NAME. DO NOT RE-COIN IT.** … Canonical name: "absent-component pattern." Canonical short
> form: **"an object without its component does nothing."**
>
> If Chapters 10, 13, and 17 each invent their own phrasing, the reader gets four unrelated gotchas to
> memorize instead of one rule to apply.

**Chapter 6 §8 coins two new phrasings and uses neither canonical form:**

> "This is a pattern the book will hit four times, and it's worth naming once: **the object exists, but
> nothing happens without the component.**"
>
> "Four gotchas, one rule. **A Kubernetes API object is a record of intent. Intent with nothing watching
> it is just a row.**"

Bearings #3 A4 repeats the first coinage as a bolded rule. The reader is now holding **three phrasings**
of one pattern, and this is the first recurrence — the one the naming discipline existed to protect.

### ⚑ And the arithmetic now double-counts

Chapter 3 promised **four more** recurrences *after Chapter 3*. Chapter 6 says the book "will hit [it]
four times" and then names the same four still ahead — while **itself being a fifth instance.** Told
four, shown five. Whichever count is chosen, Ch 3 and Ch 6 must agree.

### Recommended fix — one sentence, ~8 words

In §8's Snag, replace the coinage with Chapter 3's and fix the count:

> ~~"This is a pattern the book will hit four times, and it's worth naming once: the object exists, but
> nothing happens without the component."~~
>
> → **"This is the pattern Chapter 3 named: *an object without its component does nothing.* You'll meet
> it four more times."**

This keeps §8's excellent instance, discharges the count gap, retrieves the pattern **by name** on its
first recurrence — which is what the naming was for — and makes the CRD case read as the fifth instance
it is.

**Author call. Flagged, not fixed.** Stage 14 does not edit chapter prose.

### Instance table — updated

| # | Instance | Chapter | Status |
|---|---|---|---|
| 0 | Cluster DNS as an addon *(the pointer, not an instance)* | Ch 3 §4 | home |
| **0b** | **CRD installed, no controller** | **Ch 6 §8** | ⚑ **NEW fifth instance, not in B3's list** |
| 1 | Ingress without an Ingress controller | Ch 10 | beared from Ch 3 and Ch 6 |
| 2 | `kubectl top` without metrics-server | Ch 13 | beared from Ch 3 and Ch 6 |
| 3 | VPA not shipped by default | Ch 17 | beared from Ch 3 and Ch 6 |
| 4 | NetworkPolicy on a non-enforcing CNI | Ch 10 | ⚑ **now beared, from Ch 6** — Ch 3's gap closed |

### Downstream obligations — unchanged, but now urgent

Chapters 10, 13, and 17 must retrieve the pattern **by name**. With three phrasings already in
circulation and the naming discipline broken on its first test, the risk this shard was written to
prevent is now live rather than hypothetical.

## Related (additions)

[[custom-resource]] · [[operator-pattern]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 6 update (2026-08-24)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.1** | Chapter 3 *(cluster layer)* | deep | 2026-08-24 |
| **D1.1** | Chapter 4 *(object layer)* | deep | 2026-08-24 |
| **D1.1** | Chapter 5 *(Pod layer)* | deep | 2026-08-24 |
| **D1.1** | **Chapter 6** *(workload layer)* | **deep** | **2026-08-24** |
| **D3.1** — Application Delivery | **Chapter 6 §4–§5** ⚑ *untagged* | **moderate — first substantive coverage** | **2026-08-24** |
| **D4.2** — Cloud Native Ecosystem and Principles | **Chapter 6 §8** ⚑ *untagged* | light — partial | **2026-08-24** |

**Registry row change:** `D1.1 | Kubernetes Core Concepts | Ch 3, 4, 5, 6` → status becomes
**"in progress — Ch 3, 4, 5, and 6 covered 2026-08-24."** The four-chapter D1.1 arc
(cluster → object → Pod → workload) is complete.

### Chapter 6 — D1.1 coverage detail

`kb_tags.objectives: ["D1.1"]`; all nine sections carry `objectives: ["D1.1"]`.

| Sub-topic | Depth |
|---|---|
| Workload resources as a category; you don't manage Pods directly | **deep — answers Ch 5's published closing question** |
| Deployment → ReplicaSet → Pod ownership chain | **deep — the chapter's structural key; six later chapters depend on it** |
| ReplicaSet as the control loop made observable | **deep — discharges Ch 3's binding obligation** |
| Scaling and self-healing as one operation | deep |
| HorizontalPodAutoscaler | light — one name, deliberately; full treatment Ch 17 |
| Selector as membership-query; selector–template agreement | **deep** |
| Owner references, cascading deletion | moderate — foreground/background and finalizers deliberately out of scope |
| Adoption and the overlapping-selector hazard | **deep** |
| `RollingUpdate`, `maxSurge`/`maxUnavailable`, `Recreate` | **deep — the chapter's densest block** |
| Readiness-gated rollout safety | **deep — composes Ch 5 §7 with Ch 6 §4; the chapter's best cross-chapter synthesis** |
| Revision rule, `kubectl rollout` verbs, rollback | **deep** |
| StatefulSet, interchangeability, stable identity | **deep — storage half deliberately deferred to Ch 11** |
| DaemonSet, count-as-consequence | deep |
| Job, CronJob, run-to-completion | deep |
| Custom resources, CRDs, custom controllers, operator pattern | **deep — closes research gap G10** |
| `orphaning` | ⚑ **ABSENT** — `kb_tags` claims it; term appears zero times in 1,213 lines |
| `vertical-scaling` | ⚑ **ABSENT** — `kb_tags` claims it; never defined (only VPA named, as an absent-component instance) |
| `kubectl` command surface | deliberately deferred → Ch 8 §2 |

### ⚑ Two research gaps closed under objectives the chapter does not tag

`domain-analysis.md` assigns research gaps to objectives. Chapter 6 closes two of them:

| Gap | Content | Assigned objectives | Delivered at |
|---|---|---|---|
| **G8** | "Deployment update mechanics. Rolling update strategy, `maxSurge`/`maxUnavailable`, `Recreate`, rollout status, revision history, rollback." Called *"D3.1's most operationally central topic"*; D3.1 doubled in weight. | **D3.1, D1.1** | **§4, §5 — every named item** |
| **G10** | "CRDs, the operator pattern, and API extension." | **D1.1, D4.2, D3.1** | **§8 — all three** |

Under a D1.1-only tag, a coverage audit reads D3.1 as uncovered through Chapter 6 and will either
re-teach the material in the delivery chapter or report a false gap.

**Action: add `D3.1` to §4 and §5, and `D4.2` to §8, in `ch-06/outline.md`'s section objectives and
`kb_tags.objectives`.** One-line edit; no prose change.

---

## ✅ The domain-weight alarm from Chapter 5 is RESOLVED

Chapter 5's manifest raised this as needing settlement before Chapter 6 drafted:

> Four chapters sit inside the 44% Kubernetes Fundamentals domain and have authored **28%** between
> them. That leaves **16 points for Chapter 6 alone** — larger than Chapters 3, 4, and 5 combined.

**Chapter 6 authored 6%, not 16%.**

| Chapter | Claimed | Metadata form |
|---|---|---|
| Ch 2 | ~9% | discloses "authored allocation" inline, source-tagged |
| Ch 3 | ~6% | "authored estimate" |
| Ch 4 | ~6% | no caveat |
| Ch 5 | 7% | "This book's allocation" — no caveat, no tag |
| **Ch 6** | **6%** | **"under this book's authored allocation" + source tag + explicit note that CNCF publishes no sub-weights — the best disclosure of the five** |
| **Subtotal** | **34% of 44%** | 10 points remain for D1.2 Administration and D1.3 Scheduling |

The chapter was authored **to its content, not to a residue**, which is what the finding asked for.
**Close it.**

The **disclosure-consistency** half stands: five chapters, four different metadata forms, and the
competency separator drifts three ways (`— competency: X` / `— X` / `(X)`). Chapter 6 now models the
correct shape. **Conform Ch 3, Ch 4, and Ch 5 to Chapter 6's form; flag for `reconcile.py`.**

---

## ⚑ BLOCKING FACTUAL ERROR — "twelve named competencies" (thirteen is correct)

`draft-v1-prevoice.md:104`, inside the source-tagged disclosure sentence:

> "CNCF publishes four domain weights and **twelve** named competencies with no sub-weights, and the
> front matter says so plainly [source: cncf-kcna-curriculum-pdf-2026-08-23]."

`fact-accuracy.md` reports **all three cached CNCF sources enumerate thirteen.** `domain-analysis.md`
independently lists thirteen: **D1.1–D1.4, D2.1–D2.4, D3.1–D3.2, D4.1–D4.3.**

Two reasons this outranks a routine miscount:

1. It sits in the sentence that establishes the chapter's epistemic authority — the one place the
   chapter distinguishes what CNCF publishes from what the book authored. A wrong number there
   undermines a passage whose entire purpose is credibility.
2. **Chapter 5 shipped the same number.** Its manifest records finding C2 as *fixed* by rewording to
   "one of the **twelve** named KCNA competencies," with a source tag. So the error is now in two
   chapters, both source-tagged, both in authority-establishing positions.

**This is a book-level sweep, not a Chapter 6 fix.** Grep for "twelve" across all drafted chapters
before either publishes. Highest-priority content fix after re-harvest.

**Related, low-severity, worth carrying:** `domain-analysis.md:44` records that the published
KCNA_Curriculum.pdf contains the typo *"**Could** Native Community and Collaboration"* for D4.3.
Candidates who download the PDF will see it. A one-line footnote in the blueprint appendix was already
recommended; still open.

## ⚑ Ethical-guardrail status — Chapter 6

| Chapter | Guardrail #8 (*distinguish "frequently tested" from "might be tested"*) | Note |
|---|---|---|
| Ch 1 | pass | |
| Ch 2 | pass | models the compliant phrasing |
| Ch 3 | **FAIL — open** | six unverifiable exam-frequency assertions |
| Ch 4 | BORDERLINE | five practitioner-prevalence superlatives |
| Ch 5 | BORDERLINE | four exam-frequency assertions + prevalence superlatives |
| **Ch 6** | **PASS — and it is the first chapter to do this well** | see below |

**Chapter 6 reverses the Ch 3–Ch 5 drift.** Where those chapters asserted exam behaviour flatly, Chapter
6 hedges structurally and says *why* a claim is safe to make:

- "this material carries roughly six percent of the exam **under this book's authored allocation** — CNCF
  publishes four domain weights and twelve named competencies with **no sub-weights**" — the claim, its
  provenance, and its limit, in one sentence.
- "The stakes, **stated without inflation**."
- Common Traps preamble: "**these are documented confusions, not invented ones**" — and it is
  substantiated. The outline binds §6–§7 distractors to book-level trap-register entries #21–#23, and
  `question-quality.md` independently rates trap fidelity "unusually good."
- Exam Alert is ranked "**in descending order of confidence**" — an explicit epistemic gradient rather
  than a flat list of assertions.
- "the workload-resource decision… is exactly the kind of thing a **recognition exam** asks about in a
  single sentence" — a claim about exam *format*, which is published, not about frequency, which is not.

**Everything else on the Part 14 checklist passes:**

- **No fabricated statistics.** Every number is a sourced mechanism value (25%, 10 revisions, 600 s,
  ordinals 0..N-1, five-field cron).
- **Subject dignity (v5.7): clean.** Every wry beat lands on the practitioner — "the answer people hope
  for," "you will spend a while looking for the bug. There isn't one," "that's a design problem the
  scheduler will eventually find for you." None lands on anyone harmed by a failure.
- **Simplification acknowledged, unusually well.** §3 names foreground/background deletion and finalizers
  before declining them. §6 tells the reader exactly which half of StatefulSet storage was deferred and
  to which chapter. §4 declines strategy vocabulary and says why. §8's 🔭 names API server aggregation as
  the road not taken.
- **No strawmanning.** §4's treatment of `Recreate` refuses the easy "here's the bad option" framing and
  argues the opposite.

**⚑ Two conditions on the pass, both already in the shipping text:**

1. **"Twelve competencies"** — above. A source-tagged claim that the sources contradict.
2. **Practice Q5's keyed answer rests on an uncited negative.** *"There is no such validation"* — the
   cached docs document the overlapping-selector hazard but say nothing about whether an error is
   emitted. Under guardrail 4 (*never claim certainty where legitimate uncertainty exists*), this needs
   the softening `fact-accuracy.md` proposed, or a new fetch.

## ⚑ Gate status — Chapter 6

**The chapter's integration surface is sound; the pipeline's transport failed.**

| Artifact | State |
|---|---|
| `draft-v1-prevoice.md` | **1,213 lines / 119 KB — intact.** Opens `# Chapter 6: Fleets, Not Vessels`. |
| `draft-v1.md` | 253 lines / 24 KB — begins mid-word (`ognition exam can ask about…`) |
| `draft-v2.md` (stage-14 input) | 26 KB — same truncation, voice-polished |
| `diagnostics/structural.md` | 8 FAIL / 4 WARN — **every one an artifact of the truncation** |

Four sibling diagnostics detected this independently and each re-targeted onto `draft-v1-prevoice.md`.
Stage 14 did the same for all definitional work.

**Root cause is the harvester and it is still live.** Commit `821f1ef` fixed `<details>` extraction but
appears to have introduced overlapping-region concatenation — the triplicated tail plus the spliced
`(If the block above contains [file not available]…` marker is harvester output, not draft content. Same
failure class as `c358a92` and `821f1ef`. **Chapter 7 will hit it.** Fix the harvester before
re-harvesting ch-06, or the re-harvest reproduces the corruption.

**Also recoverable and currently being lost:** `draft-v2-prevoice.md` (7 KB) carries the revision stage's
**21** practice questions — two inserted after Q15 — plus its Chapter Summary and DaemonSet fixes. The
voice stage, handed a triplicated input, selected the "internally complete" 19-question set, which is the
**pre-revision** set (P6, P7, P14 are byte-identical to `draft-v1.md`). The outline budget is 19 and
`question-quality.md` confirms it is met exactly — but the revision's two additions were almost certainly
*repairs*, not padding. **Recover them and judge on merit before treating 19 as settled.**

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 6 update (2026-08-24)

**7 tagged in-budget items · graded pool 34 (15 Bearings + 19 Practice) · rate = 20.6%.** Clears the 20%
floor. Two further tagged items sit in Soundings, excluded from the budget by B3.

**Chapter 6 draws from three predecessors** (Ch 3, 4, 5), matching Chapter 5. Ch 4 drew from two, Ch 3
from one.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| the control loop: two states compared, action on the gap | ch 3 §6 | **ch 6** — Soundings Q7 *(excluded from budget)* |
| a Pod's node dies; Ch 5 said it is not rescheduled — what happens instead | ch 5 §4 | **ch 6** — Soundings Q8 *(excluded from budget)* |
| control-loop states + the action, named with the real field | ch 3 §6 | **ch 6** — Bearings #1 Q4 |
| label selectors as the universal join; ReplicaSet as one of four users | ch 4 §5 | **ch 6** — Bearings #1 Q5 |
| readiness probes; what a never-ready Pod does to a rollout | ch 5 §7 | **ch 6** — Bearings #2 Q4 |
| `spec` = what you asked for, `status` = what is | ch 4 §2 | **ch 6** — Practice Q2 |
| Pod replaced, not moved; new UID | ch 5 §4 | **ch 6** — Practice Q4 |
| Pod phase `Succeeded` | ch 5 §5 | **ch 6** — Practice Q16 |
| control loop vs kube-controller-manager's built-ins | ch 3 §6 + §2 | **ch 6** — Practice Q18 |

**Every target verified against the named chapter's actual section content.**

### Notes on quality

- **Practice Q2 is the cleanest setup-and-payoff in the book so far.** Chapter 4 line 273 forecasts it in
  published prose: *"Chapter 5 reads it against a Pod's phase, **Chapter 6 reads it against a replica
  count**."* Q2 cashes it, drawing on the same snapshot (`k8s-docs-objects-2026-08-23`) and the same
  worked example the docs use. A reader who noticed the forecast is rewarded two chapters later; one who
  didn't loses nothing.
- **Bearings #1 Q5 is the theme architecture working as designed.** It asks what it means for one Pod to
  be selected by *both* a ReplicaSet and a Service — converting `label-selector.md`'s "one mechanism, four
  problems" claim into a graded item, and setting up Ch 9 rather than merely pointing at it.
- **Practice Q16 tests the right level.** `Succeeded` is a *Pod* phase; the Job object finishes as
  `Complete`. The key states the distinction explicitly rather than letting the two blur.
- **Practice Q18 is genuine retrieval, not new material wearing a tag.** Chapter 3 §6 publishes the
  controller definition and §2 publishes kube-controller-manager; Q18 requires both.

### ⚑ One cross-chapter item is invisible to a mechanical count

**Practice Q12** is tagged `[interleaved: Ch 5 §7 + §4]` and genuinely reaches Chapter 5 — Ch 5 §7 is
"Three Probes, Three Jobs," so the tag is accurate — but it carries **no `[retrieval:]` tag**, so it is
not among the seven. If the book's retrieval rate is ever computed by grepping `[retrieval:` (which is how
a linter would do it), Q12 is uncounted and the true rate is **8/34 = 23.5%**.

Low severity for chapter correctness; it matters because the metric is book-level. **Adding the tag costs
one token.**

### ⚑ Retrieval tags still absent from Chapter 6's answer keys

Chapter 4 repeats the tag in its answers. Chapters 5 and 6 tag only the stems. Repeating it tells a reader
who missed the item *which chapter to go back to* — the entire point of the tag. Chapter 5's manifest
raised this and recommended matching Chapter 4; **Chapter 6 did not.** Two chapters of divergence.
**Decide and sweep before Ch 7.**

---

## Cross-cutting themes — status after Chapter 6

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **The control loop** (B3 headline) | Ch 3 §6 | Ch 4 · Ch 5 *(unplanned)* · ✅ **Ch 6 — the planned instantiation, discharged twice: §2 mechanically, §9 as synthesis** | **Ch 11 (still unbeared)**, Ch 15, Ch 17 |
| **Labels/selectors as the universal join** | Ch 4 §5 | Ch 5 *(unplanned)* · ✅ **Ch 6 §3 — FIRST retrieval by name; the deep application** | Ch 7, Ch 9, Ch 10 |
| **The absent-component pattern** | Ch 3 §4, named | ⚑ **Ch 6 §8 — FIRST recurrence, but RE-COINED.** See `concepts/absent-component-pattern.md` | Ch 10 ×2, Ch 13, Ch 17 |
| **"Kubernetes defines an interface, the ecosystem implements it"** | Ch 2 §4, named | ✅ **Ch 6 §8 — FIRST named recurrence.** "That is the fourth socket Chapter 2 promised" — CRI / CNI / CSI / API extension | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §2 |
| **Namespaced vs cluster-scoped** | Ch 4 §5 | Ch 5 §6 | ⚑ **not retrieved in Ch 6** — Ch 12 §3, Ch 10, Ch 11 |

**Chapter 6 discharges the two theme debts Chapter 5 flagged as stuck at zero**, and delivers the control
loop's planned instantiation. This is the chapter the theme architecture was built around and it performs.

**⚑ But the naming discipline broke on its first test.** Of the two themes retrieved for the first time
here, one (labels/selectors) uses the canonical name and one (absent-component) does not. The whole
argument for coining names — *"four gotchas, one rule"* — depends on the name surviving contact with the
first downstream chapter. It did not. See the shard append for the ~8-word fix.

---

## Forward commitments — status

| # | Commitment | Status |
|---|---|---|
| 7 | **Ch 6 must open on "if Pods are designed to be replaced, who does the replacing?"** | ✅ **DISCHARGED verbatim.** §Why This Chapter Matters, first line. Also honours the second half — §1 delivers "something you will almost never create directly." |
| 3 | Ch 5 must retrieve the UID rule | ✅ discharged at Ch 5; **cashed a second time** at Ch 6 §2's demonstration (`qh7bl`, not `x8k2q`) and Practice Q4 |
| 2 | **Ch 11 must retrieve the control loop** | ⚑ **OPEN, four chapters overdue.** Ch 6 bears to Ch 11 §4 twice and carries the loop to neither. Ch 3, 4, 5, 6 have each passed it forward. |
| 5 | Ch 9 must retrieve the Pod IP / shared network namespace | **OPEN.** Ch 6 bears to Ch 9 four times and names the Pod IP in none. |
| 1 | Ch 13 must carry a Ch 8 retrieval item (version skew) | **OPEN** — untouched at Ch 6 |
| 4 | Ch 12 must **derive** the RBAC 2×2 from the namespaced boundary | **OPEN** |
| 6 | Ch 13's method must be "read the phase before you read the logs" | **OPEN.** Ch 6 §4 bears to Ch 13 §3 for stuck-rollout diagnosis. |
| 8 | Ch 7, 13, 17, 18 must each retrieve requests/limits | **OPEN — Ch 7 is the next test.** Ch 6 does not touch requests/limits, correctly. |
| **9** | **Ch 7 must open on the unplaced Pod** | **NEW.** Voyage Ahead publishes it: *"It creates a Pod. It does not decide where the Pod goes."* Plus the `Pending`-Pod-and-unsatisfied-count image. |
| **10** | **Ch 7 §5 must land taints/tolerations against §7's planted instance** | **NEW.** The Voyage Ahead names it: *"You've already met the mechanism in disguise. The DaemonSet's tolerations in §7 were a node saying 'not for general traffic' and a controller saying 'this one's an exception.'"* |
| **11** | **Ch 11 §4 must deliver PVC + `volumeClaimTemplate` for StatefulSets** | **NEW.** §6 tells the reader outright what was skipped and what Ch 11 owes them. The book's only intentional half-teach; a published promise. |
| **12** | **Ch 9 §5 must deliver headless Services** | **NEW.** §6 tells the reader a StatefulSet *requires* one and that they must create it. |
| **13** | **Ch 15 must reuse §9's figure, not redraw it** | **NEW, and the strongest synthesis promise in the book.** §9: *"come back and check this figure. **It will be the same figure.**"* Binding on Ch 15's figure selection, not just its prose. |
| **14** | **Ch 14 §5 and Ch 15 §3 must distinguish three "rollback" mechanisms** | **NEW.** §5 names all three and stakes the claim that knowing the Deployment one is what makes the others distinguishable. |
| **15** | **Ch 17 §2 must collect the four pluggable interfaces in one place** | **NEW.** §8: "Collecting all four into one story is Chapter 17's job, and it's a better story told all at once." |
| **16** | **Ch 10 must retrieve the absent-component pattern by name** | **NEW/escalated.** Two instances land there (Ingress, NetworkPolicy) and the pattern now has three circulating phrasings. |

---

## ⚑ §N reservations — Ch 9 §1 is now three-deep, and Chapter 6 collides with itself

Chapter 3's proposed convention — *no `§N` in cross-bearings pointing into undrafted chapters* — remains
unratified and is now broken by four consecutive chapters. Ch 4: 15 times. Ch 5: 17 times across eleven
chapters. **Ch 6: 22 times across twelve chapters.** The count grows every chapter and it is the direct
cause of every collision below. **This is a governance decision the author has never been asked to make
explicitly. Asking is cheap; the cost of not asking compounds.**

| Reservation | Claimants | Status |
|---|---|---|
| **Ch 9 §1** | Ch 2 (*CNI and pod networking*) · Ch 5 (*why a Service is necessary*) · **Ch 6 §2** (*why a Service exists*) | ⚑ **HARD COLLISION, now three-deep. BLOCKING before Ch 9 drafts.** Ch 5's manifest already ruled Ch 2 has precedence and the arc ordering (network model → Pod IP → CNI → Service) supports it. Ch 6's claim is near-identical to Ch 5's — **move both to §2/§3.** |
| **Ch 17 §5** | **Ch 6 ×2** (*the autoscaling landscape*) vs Ch 5's **Ch 17 §2/§3** vs Ch 2's **Ch 17 §4** | ⚑ Four-way. Ch 5's recommendation stands: **drop to chapter-level** until Ch 17 is outlined — a sanctioned form Ch 3 already uses. |
| **Ch 13 §2 vs Ch 13 §4** | **Ch 6, internally inconsistent** | ⚑ **NEW — and it is Chapter 6 disagreeing with itself.** §2 bears to *"Ch 13 §4 — metrics-server as the HPA's input"*; §8 bears to *"Ch 13 §2 — the resource metrics pipeline."* Same subject, two reserved sections, one chapter. Pick one. |
| **Ch 12 §2/§3** | Ch 2 · Ch 4 · Ch 5 · **Ch 6 §3** (*what deletion does and does not remove* → §3) | Ch 6 correctly picked §3, avoiding the three-deep §2 pile-up. ✓ |
| **Ch 6 §3** | Ch 1 · Ch 2 · Ch 4 | ⚑ **RESOLVED BY EDIT, not by renumbering.** See below. |
| Ch 7 §1/§5 · Ch 9 §2/§5/§7 · Ch 10 §3 · Ch 11 §4 · Ch 14 §2/§3/§5 · Ch 15 §2/§3/§4 · Ch 16 §3 · Ch 18 §3 | Ch 6 | ✅ verified compatible with published claims and the arc outline |

### Inbound pointer repairs — two shipped-file edits, confirmed

Chapter 6's section order is fixed by its Attention Budget and honoured by six other inbound pointers plus
the entire outline. Two published pointers collide with it. **Editing two tokens in two shipped files is
the cheap side of the trade** — the draft's own `AUTHOR-REVIEW` at line 778 and the outline's Open
Questions #1 both reach the same conclusion, and stage-11 integration confirmed it independently.

- `chapter-01-taking-departure.md:436` — `Ch 6 §3` → **`Ch 6 §6`** (StatefulSets)
- `chapter-02-cargo-in-standard-crates.md:600` — `Ch 6 §3` → **`Ch 6 §8`** (CRDs)

Outside every stage's write scope, which is why they have survived to stage 14 unactioned. `chapter-02`'s
own frontmatter (lines 17–21) carries the standing warning that *"Section NUMBERING IS LOAD-BEARING"* —
Chapters 1 and 2 published pointers into Chapter 6 before Chapter 6's section order existed.

---

## ✅ Figure-anchor notes closed as NOT defects

Recorded so downstream stages stop re-raising them. **This is the second chapter in which Stage 10 has
proposed the same wrong rename**, which suggests its anchor linter needs `chNN-zenith-<slug>` added as a
sanctioned form.

1. **`ch06-zenith-control-loop-instantiated` is correctly named. Do not rename to `fig06`.**
   - `arc-outline.md:156` prescribes this exact slug.
   - `chNN-zenith-<slug>` is the prescribed form for every chapter's Zenith figure.
   - **Chapter 2 already shipped `ch02-zenith-standard-crate` in published prose.**
   - Chapter 5's manifest made the identical ruling for `ch05-zenith-smallest-deployable-unit`.
   - **Strike the suggested correction at `image-specs.md` lines 65, 575, and 628.**

2. **The join key does not currently diverge.** ⚑ Correction to `integration.md:187`, which tabulates
   draft vs `image-specs.md` as `ch06-zenith-…` vs `ch06-fig06-…` and marks it ❌. **`image-specs.md:631`
   reads `anchor_id: ch06-zenith-control-loop-instantiated`** — matching the draft, the outline, and the
   arc outline. `fig06` appears only in three prose notes explicitly marked "pending author review."
   Integration read the suggestion as the field value. **There is no mismatch to repair — only a
   suggestion to strike.**

3. **All six anchors are absent from the *revised* draft** because they live in the truncated body. They
   resolve on re-harvest; the specs are not dangling against the intact draft.

## Convention status

`[retrieval: chN]` tags render reader-visible, bold-bracketed in the stem. **Four chapters of consistent
practice (Ch 3, 4, 5, 6).** ⚑ The *answer-key* half of Chapter 4's practice is now broken by two chapters.
**Still OBSERVED PRACTICE pending author ratification — and the window to change it cheaply closed two
chapters ago.**

=== END APPEND ===
```

---

## Summary of what needs the author

Ranked. Nothing below is fixable at stage 14.

1. **The orchestrator is not performing stage-14 writes.** `Book-KCNA/knowledge-base/` does not exist after five manifests emitted writes to it. Every downstream chapter has been drafting without the KB the pipeline believes it has.
2. **Re-harvest ch-06, but fix the harvester first.** The overlapping-region concatenation introduced around `821f1ef` is the root cause and will hit Chapter 7. Also recover `draft-v2-prevoice.md`'s two added practice questions before treating the 19-question set as settled.
3. **"Twelve named competencies" is wrong in two chapters,** both source-tagged, both in authority-establishing positions. Thirteen is correct. Book-level grep.
4. **The absent-component pattern was re-coined on its first recurrence** — the exact failure the naming discipline was written to prevent. ~8-word fix in §8; it also discharges Chapter 3's count gap cleanly.
5. **Two shipped-file cross-bearing edits** (Ch 1 §3→§6, Ch 2 §3→§8), plus Chapter 6's internal Ch 13 §2/§4 self-collision, plus the now-three-deep Ch 9 §1 collision that blocks Chapter 9.
6. **Strike the `fig06` rename suggestion** in `image-specs.md` — and add `chNN-zenith-<slug>` to the structural contract so Stage 10 stops proposing it every chapter.
7. **Add `D3.1` to §4/§5 and `D4.2` to §8** in the outline's objective tags, or research gaps G8 and G10 will read as uncovered.
8. **Drop `orphaning` and `vertical-scaling`** from the outline's concept tags, or add the terms to the prose. I did not mint glossary entries for either.
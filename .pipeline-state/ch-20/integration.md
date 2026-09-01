<!-- Stage 13 output for KCNA Ch 20. Emitted to stdout per the executor convention; the orchestrator writes `.pipeline-state/ch-20/integration.md`. -->

# Integration Check — KCNA Chapter 20

## Summary

- Terminology consistency: **fail** — 1 binding-convention violation, 4 minor items
- Callbacks to earlier chapters: **54 correct / 0 incorrect**
- Retrieval-practice accuracy: **fail** — all 42 surviving domain/section tags resolve correctly, but 18 of 60 items carry no answer at all, and the answer key has two independently detectable positional signatures
- Glossary coverage: 0 concepts introduced, 0 defined in-chapter (correct for this chapter type), 3 inherited debts reach graded text
- Contradictions with earlier canon: **2 flagged**, 1 unverifiable
- Ethical guardrails (skill Part 14): **fail** — the Ethical Checkpoint line "why-wrong explanations provided for all questions" fails outright for items 43–60, and the chapter's own Instructions promise those explanations

**Scope note (rule 2).** The context for this stage carried `[no knowledge-base shards tagged]`. Every verification below is against the **B6 section skeleton** and the **B7 term ownership ledger** — both marked BINDING and both supplied in full — plus the draft itself. I have **not** read the shipped prose of Chapters 1–19 and do not assert anything about it that those two contracts do not already record. Where a check needs shipped text, it is marked **unverifiable here** rather than guessed.

**The truncation.** The draft's own ship-blocking AUTHOR-REVIEW block is correct and I confirm it independently: the document ends after walkthrough 42, and both walkthroughs 43–60 and the entire `## Scoring Rubric` block are absent. The skeleton's Ch 20 contract specifies four blocks; three are present. I have not re-litigated that finding, but three of the six findings below are consequences of it and one of them (§ Answer-key positional signature) **constrains how the tail must be restored**, so it needs to reach the author before stage-11 is re-run.

---

## Terminology consistency

Checked against the B7 **Canonical forms** table and its homonym rules. The chapter's compliance is high — the homonym discipline in particular is the best I have seen in this commission. Four homonym pairs are not merely avoided but *actively disposed of in reader-facing text*, which is the ledger's stated intent rather than its minimum.

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| "An object without its component does nothing" | **quote VERBATIM** (Ch 3 coins, Ch 10 §3 names as pattern) | 1 reader-facing invocation (walkthrough 31), 3 further instances of the pattern un-named (walkthroughs 2, 31D, item 43) | **YES — binding violation.** See below. |
| `Soundings` / `Fixed Point` | 🧭 and ★ paired with the name | 2, both bare (Instructions) | Minor — see below |
| pod network / pod networking | lowercase sanctioned for *"pod networking"* only | 3 ("a pod network" ×1, "the pod network" ×1, "pod-to-pod networking" ×1) | Minor |
| process namespace | no ledger row; Ch 2 §1 owns "Linux namespace" | 1, bare, in a graded distractor (item 55 B) | Minor |
| plugin | "Never bare. Always qualified by its interface." | "CNI plugin" ×3 ✓; "a plugin that extends the `kubectl` client" ×1 | Minor |
| namespace (Linux vs Kubernetes) | sense A always "Linux namespace" | Item 5 + walkthrough 5 A | **No** — walkthrough 5 A names it "the *Linux* namespace from Chapter 2, a different mechanism that shares an English word" |
| control plane (cluster vs mesh) | sense B always marked | Item 29 + walkthrough 29 D | **No** — stem scopes with "In a service mesh"; walkthrough 29 D says outright "'control plane' here is the *mesh's*, not the cluster's" |
| revision / rollback (Deployment vs Helm) | "release revision"; never bare "rollback" where either could be meant | Item 18 + walkthrough 18 | **No** — exemplary; the item exists to teach the collision |
| operator (pattern vs person) | never used for a person; "cluster operator" is a two-word role name | Walkthrough 33 A; item 46 A | **No** — walkthrough 33 A states the rule explicitly and cross-bears to Ch 10 §5 |
| request (resource vs API) | qualify wherever both are in scope | Items 3, 8, 16, 40, 41 | **No** — every ambiguous instance is qualified |
| binding (scheduler vs PV/PVC) | neither bare outside its own chapter | Walkthroughs 2, 3 A, 45 | **No** — all instances sit inside sentences whose whole subject is scheduling |
| Sandbox (maturity vs runtime) | capitalized, always beside a sibling level | Item 15, walkthrough 15 | **No** — always with Incubating/Graduated |
| `Endpoints` (legacy object) | declared unowned; capitalized bare form forbidden | 0 | **No** — correctly absent; lowercase "endpoints" for backend addresses ✓ |
| Argo CD | two words | 3 | **No** — no `ArgoCD` anywhere |
| Kubernetes / `K8s` | spell out in prose | ~40 / 0 | **No** |
| cloud native | never hyphenated | 3 (incl. two blueprint domain names) | **No** — does not inherit the 16-instance hyphenation debt from Ch 1–8 |
| worker node | only where the control-plane contrast is the point | 1 (item 35) | **No** — used exactly as the rule prescribes |
| `kubectl`, `etcd` | lowercase even sentence-initially | ~25 / 4 | **No** — never capitalized. Two sentence-initial uses (item 50 stem, walkthrough 35) satisfy the hard rule but not the "recast rather than capitalize" preference; not worth an edit |
| CamelCase object names | unspaced, never lowercased in prose | ~30 | **No** — including correct external pluralization ("CustomResourceDefinitions", "StatefulSets") |
| twelve-factor app | hyphenated, spelled out | 1 | **No** |

### The one that matters: the absent-component pattern

The ledger row is unambiguous, and carries the strongest instruction in the document:

> **"An object without its component does nothing"** … quote it VERBATIM — this exact wording now appears 24× across Ch 3/6/10/11/13/17, including a graded Practice option

The 2026-08-31 errata note records why the row is worded that way: Ch 17 followed a *defective* version of this row and "hand[ed] back the book's most-reinforced retrieval phrase in words the reader had never seen," and the same defect was found propagating in Ch 6 — "inside the very instruction *Name the pattern, because you will retrieve it by name.*"

Walkthrough 31 opens: *"The object exists; nothing happens without the component."*

That is a paraphrase, in the chapter whose entire function is retrieval, of the phrase the book has spent 24 reinforcements making retrievable by its exact wording. It is the same failure the errata note describes, one chapter later. The cross-bearing to `Ch 10 §3` is correct; the words are not.

**Fix (one line):** open walkthrough 31 with the canonical sentence, then keep the existing gloss —

> An object without its component does nothing. Kubernetes accepts and stores the Ingress, and no traffic moves until an Ingress controller is watching for it.

Three further instances invoke the pattern without naming it: walkthrough 2 (no CNI plugin), walkthrough 31 D ("it too requires a component, the cloud-controller-manager, to act"), and item 43's correct answer (a StorageClass needs a provisioner). Naming it in **one** of those — walkthrough 43, when it is written — would let the mock exam land the pattern twice, which is what a capstone retrieval instrument is for. Naming it in all four would be over-reinforcement; the ledger's "retrieved *by name*" instruction does not require every instance.

### The three minor items

1. **Bare `Soundings` / `Fixed Points`** (Instructions: *"There is no Soundings block here, no Fixed Points, no callouts in the margin"*). The style ledger holds that "bare 'Soundings' without the compass symbol is drift." The counter-argument is real and I do not think it is weak: this is a chapter that deliberately carries no markers, and the sentence exists to say the markers are *absent* — pasting 🧭 and ★ in reintroduces the glyphs the paragraph is disclaiming, and the marker-icon build would render them as navy PNGs mid-denial. **Author's call.** If the strict reading wins, the fix is `no 🧭 Soundings block here, no ★ Fixed Points`. My recommendation is to leave it and record the exemption, because the sentence is *about* the markers rather than *using* them.

   Related, trivial: the Instructions' `**Dead Reckoning:**` is a plain bold-led paragraph rather than the skill's blockquote form (`> **Dead Reckoning:** …`). The em-dash in the marker table is the "no symbol" placeholder, not a required prefix, so the name is correct; only the blockquote is missing.

2. **"a pod network" / "the pod network."** The ledger sanctions lowercase for the phrase *"pod networking"* specifically. "Pod network" as a noun is one step outside that. Same idiom, and both instances read naturally; flagging only so a later sweep does not "correct" it in the wrong direction.

3. **"process namespace" bare in item 55 B.** No ledger row exists for it, and it reaches a graded distractor. It is the real field name (`shareProcessNamespace`) and Ch 5 §1 owns "shared network namespace" in the same bare style, so this is consistent with the book rather than against it. Recommend adding a ledger row under Ch 5 §1 rather than editing the item.

4. **"a plugin that extends the `kubectl` client"** (item 33 B) is qualified descriptively but by an interface the ledger's plugin list does not carry (CNI / scheduler / admission / device). Acceptable; noted so the ledger row can be widened rather than the item narrowed.

---

## Callback correctness

**54 cross-bearings. 54 resolve. 0 defects.** Every `Ch N §M` pointer was checked mechanically against the B6 skeleton's section titles and ownership columns, not against my reading of the target chapters.

| Check | Result |
|---|---|
| Pointers with an explicit `§N` | 53 — all name a section the skeleton grants that chapter, with matching owned content |
| Pointers to Ch 1 | 1, and it correctly uses **heading-name form** (`Ch 1 § Ninety Minutes: The Exam as Published`) rather than inventing a `§N`, which is exactly what skeleton Collision #1 requires |
| Pointers emitting `Ch 20 §N` | **0** — the skeleton's absolute prohibition is honored |
| Pointers to undrafted sections | 0 — every target is a skeleton-granted section |
| Forward pointers | 0 — correct; Ch 20 is terminal |

Spot-checked against the skeleton's own pinned-anchor table (Collision #5), since those numbers are immovable: `Ch 9 §1`, `Ch 9 §4`, `Ch 11 §1`, `Ch 12 §2`-adjacent, `Ch 13 §2/§3/§4/§5`, `Ch 15 §4`, `Ch 16 §1/§3`, `Ch 17 §2`, `Ch 18 §1/§3`, `Ch 19 §3` — all consistent with the published pins.

Densest chapters pointed into: Ch 13 (4 pointers), Ch 12 (5), Ch 2 (5), Ch 5 (5), Ch 6 (5), Ch 9 (4), Ch 11 (3). That distribution tracks the domain weighting, which is the right shape for a capstone.

**One structurally-correct pointer lands in contested text.** `*[cross-bearing: see Ch 19 §3 — pacing and time discipline]*` resolves — Ch 19 §3 is "Ninety Minutes," which the skeleton says owns exactly that. But see § Contradictions: the target section currently contains a sentence Ch 20 refutes. The pointer is not the defect; the destination is.

---

## Retrieval-practice accuracy

Ch 20 does not use `[retrieval: chN]` tags. It uses a richer per-answer form — `*D<domain>.<competency> · Ch N §M · <difficulty>*` — which is the same contract in a better shape, and I checked it as such.

### Section tags: 42 / 42 correct

Every one of the 42 surviving answers tags a section that, per the skeleton, actually owns the material the question tests. No misdirected retrieval. Sample of the tightest cases:

- **8 → Ch 5 §8** — QoS class computation. Skeleton: "**requests vs limits**; QoS classes." ✓
- **21 → Ch 6 §6** — StatefulSet identity, *not* storage. Skeleton splits identity (Ch 6 §6) from storage pairing (Ch 11 §6); the walkthrough refutes distractor A by cross-bearing to Ch 11 §6 for the PVC half. Exactly the split the skeleton designed. ✓
- **41 → Ch 13 §4** with a supporting bearing to **Ch 5 §8** — `OOMKilled` diagnosis at Ch 13 §4, mechanism at Ch 5 §8. Matches ledger flag ⚑2's resolution precisely. ✓
- **14 → Ch 10 §6** closing to **Ch 12 §9** — NetworkPolicy allow-only semantics retrieved into the cross-cutting theme its Zenith owns. ✓

### Domain distribution: verified, and achievable by the missing tail

The Instructions promise D1 26 · D2 17 · D3 10 · D4 7, derived from the published 44/28/16/12 blueprint. That arithmetic is right (26.4/16.8/9.6/7.2 → 26/17/10/7, summing to 60).

The 42 tagged answers supply **D1 18 · D2 13 · D3 6 · D4 5**. The residual the tail must supply is therefore **D1 8 · D2 4 · D3 4 · D4 2 = 18**. Inferring domains for items 43–60 from their subject matter gives exactly **8 / 4 / 4 / 2**.

**This is load-bearing for the restorer: the exam block's weighting is already correct and must not be adjusted.** Items 43–60 need walkthroughs written against their existing stems; they do not need reweighting, resequencing, or substitution. Any change to the item set breaks a distribution that currently matches the published blueprint exactly.

### Instrument validity: the answer key has two detectable signatures

This is not in the draft's AUTHOR-REVIEW and I believe it has not been seen. It survives the fix that draft-v2 applied.

Draft-v1 keyed roughly 55 of 60 items to **B**, which draft-v2 correctly identified as a position giveaway and rewrote. The rewrite balanced the *totals* — A 11 · B 10 · C 10 · D 11 across 42 — but introduced structure:

**Signature 1 — every consecutive block of four contains each letter exactly once.**

```
 1– 4  C B D A        21–24  C B D A
 5– 8  B D C A        25–28  C B A D
 9–12  B C A D        29–32  B C A D
13–16  B C A D        33–36  C A D B
17–20  C B A D        37–40  A C D B
```

Ten complete blocks, ten complete Latin sets, zero exceptions. On a random key each block completes with probability 24/256 ≈ 0.094; ten in a row is ≈ 5 × 10⁻¹¹. The sequence `B C A D` recurs three times verbatim, `C B A D` twice.

**Signature 2 — no letter ever repeats on consecutive items.** Zero adjacent repeats in 41 adjacent pairs, against ≈ 10 expected on a random key.

**Why this matters for a scored instrument.** A test-wise candidate who answers three items in a block confidently can deduce the fourth by elimination, without knowing the material. Over 60 items that is a substantial score inflation available to exactly the reader the book is trying to calibrate honestly — and it defeats the purpose of the score sheet the Instructions promise, which exists to give a *domain-level* diagnostic the real exam never provides. A per-domain breakdown computed partly from guessed-by-elimination answers is a worse instrument than no breakdown.

**Fix, and its ordering.** Re-key after the tail is restored, not before, so it is a single relabeling pass rather than two:

1. Write walkthroughs 43–60 against draft-v2's stems (see the draft's own AUTHOR-REVIEW for the required shape and for why draft-v1's tail cannot be pasted in — item numbering does not map).
2. Then generate a fresh 60-item key by unconstrained random assignment, accepting only a global balance target (15 ± 2 per letter). **Permit** adjacent repeats and **permit** blocks of four that repeat a letter — those are the properties a real key has.
3. Apply it by permuting each stem's four options so the correct text moves to its new letter, and update the walkthrough's header letter and refutation bullets to match.

**Step 3 is mechanically safe here, and I verified it:** no option references another by letter, none uses "all/none of the above," and no option's wrongness depends on its position. Every distractor is independently refutable, which is what makes the permutation a pure relabeling.

### Difficulty distribution

Across 42: ⚪ 8 · 🔵 25 · 🟡 9 · 🔴 0. The absence of 🔴 Expert is defensible for an associate-tier credential and I am not recommending a change — flagged only so the restorer treats it as a deliberate choice rather than a gap to fill when keying 43–60.

---

## Glossary coverage

Ch 20 is a mock exam. It **introduces no new concepts** and defines none, by design. So the interesting question is not "what needs an entry" but "does anything reach graded text without a lookup path," which is the ledger's own stated test:

> a term used in question text or an answer key may not be glossary-only, because a reader who meets it there has no place to look it up mid-question

### Graded-use restrictions: full compliance

Every restricted term in the ledger's Part 2 was checked against all 60 stems, all 240 options, and all 42 walkthroughs:

| Restricted term | Ledger restriction | In Ch 20? |
|---|---|---|
| **PodDisruptionBudget / PDB** | "not eligible for graded question text or an answer key anywhere in the book, **including the Ch 20 mock**" | **Absent ✓** — including item 19 (cordon/drain), where it would have been the natural reach |
| **ABAC** | not a distractor unless Ch 12 §3's clause is written | **Absent ✓** — item 36 is a pure RBAC item |
| **eBPF** | not eligible for graded text | **Absent ✓** |
| **SRE** | not eligible for graded text | **Absent ✓** — item 39 attributes nothing |
| **LTS** | no question may hinge on it | **Absent ✓** |
| **PSP** | only as a wrong option in a PSA item | **Absent ✓** |
| **descheduler** | not eligible | **Absent ✓** |
| **`Endpoints`** (legacy, capitalized) | unowned; no chapter should use the bare form | **Absent ✓** |
| **static Pod / mirror Pod** | Ch 13 debt, entries pending | **Absent ✓** |
| **SLA** | to be owned at Ch 18 §7; expected as a Ch 20 distractor | **Absent** — no issue, but see below |

That is a clean sweep across ten restrictions in a 60-item instrument. Worth recording as a positive: the drafting stage evidently read Part 2.

Two notes rather than defects. **SLA** — the ledger predicted it would appear "in Ch 18 and Ch 20 answer keys as a wrong option." It does not, so Ch 20 creates no pressure to resolve that orphan; it can be resolved on Ch 18's schedule. **Item 44 D** ("A ConfigMap generator in Helm") deliberately misattributes a Kustomize feature (`configMapGenerator`, Ch 14 §5) to Helm — a good distractor, but its refutation is in the missing tail, so a reader who picks it currently learns nothing.

### Three inherited debts reaching graded text

| Concept | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| **SIG**, bare and unexpanded in item 53 **D — the correct answer** | no | **Yes, plus an in-place fix.** The ledger records this as a pre-existing Ch 8 debt: "**SIG** is first used unexpanded at Ch 8 line 861." Ch 20 inherits it at the worst possible place — a correct answer the reader must recognize under time pressure, with three sibling options (TOC, TAG, Steering Committee) all correctly expanded around it. **Fix:** "…brought to the Special Interest Group (SIG) that owns that subsystem." One clause, no other change. |
| **"63-character limit"** on label values (item 51 **C**, a distractor) | no | No — but the specific is untaught anywhere in the ledger. The option's wrongness does not depend on the number (selectors cannot match annotations *at all*), so the item is sound; the number is decoration a reader cannot check. Its refutation is in the missing tail. Consider cutting the clause when 51's walkthrough is written. |
| **"process namespace"** (item 55 B) | no | See Terminology §3 — add a ledger row under Ch 5 §1 rather than editing the item |

**Net for stage 14: zero new glossary entries are generated by this chapter.** The three items above are Ch 5 / Ch 8 / Ch 14 debts that Ch 20 surfaces.

---

## Contradictions with earlier canon

### 1. Ch 19 §3 vs Ch 20 Instructions — the exam console. **Real. Author decision required.**

Ch 20 documents the multiple-choice console behavior (Previous/Next, flagging, the Review Screen, Finish Exam, Pause-does-not-stop-the-timer) with `[source: lf-examui-multiple-choice-2026-08-31]`.

The draft's AUTHOR-REVIEW records that `ch-19/draft-v2.md:541` currently states *"The Linux Foundation does not publish how its multiple-choice exam console behaves."*

Both chapters cannot ship. Ch 20's framing is sourced and Ch 19's is not, so **the correction runs Ch 19 → Ch 20, never the reverse** — the draft's own note says this and it is right. Two additions from my side:

- The B6 skeleton's Ch 20 block has already been corrected (its ⛑ CORRECTION of 2026-08-31 supersedes the false "NOT FOUND in any authoritative source" finding and lists the forbidden phrasings). **The skeleton's Ch 19 block has not been checked** against that correction. Ch 19 §3's sentence looks like a second instance of the same superseded finding, in which case Ch 19 needs the same retrofit Ch 1 already received — not a one-line edit but a check of every provenance claim in that chapter.
- Ch 20 emits a cross-bearing *into* Ch 19 §3. Until Ch 19 is fixed, the mock exam sends the reader to a section that contradicts the page they just left.

**Ch 20 itself is clean on the superseded finding.** Its Dead Reckoning block reads: *"The Linux Foundation publishes both of the numbers this instrument is built around… Neither number appears on the KCNA product page."* That is the skeleton's prescribed correct form, near-verbatim. Neither forbidden phrasing appears anywhere in the chapter.

### 2. The absent-component pattern phrase — **binding-convention contradiction.** Detailed under Terminology.

### 3. Unverifiable without shipped text: does Ch 8 §4 teach that `drain` cordons?

Walkthrough 19 B asserts parenthetically: *"In practice `kubectl drain` cordons for you. The exam tests the conceptual order."* The skeleton grants Ch 8 §4 "cordon / drain / uncordon," and the ledger's Ch 8 notes say only that Ch 8 §4 "states that `kubectl drain` evicts the Pods." Whether Ch 8 teaches the auto-cordon is **not recoverable from the two contracts**, and no shards were supplied.

This matters slightly more than a stray detail, because it is what makes option A ("cordon, then drain") the *conceptually* right answer rather than a redundant one. If Ch 8 §4 does not teach it, Ch 20 is introducing a mechanism in an answer key. **Verify at Ch 8 §4; do not edit on my say-so.**

### Two that look like drift and are not

- **Item 15 omits `Archived`.** The ledger's Ch 17 §2 row is "(Sandbox · Incubating · Graduated · **Archived**)". Ch 20's walkthrough names only three. Not drift: Archived is not a rung you are promoted *to*, and the item asks which level *follows*. The three-level framing is a correct subset. No action.
- **Item 33 A vs item 46 A on "operator."** Item 33's key states "'operator' is never used for a person in this book"; item 46's correct answer uses "cluster operator" as a role. These are reconciled inside walkthrough 33 A itself, which names the Gateway API exception and cross-bears to Ch 10 §5. Exactly what the canonical-forms table asks for. No action.

### Applying the Ch 18-gate ruling to this chapter's open provenance flags

The draft carries four AUTHOR-REVIEW blocks asking for `[source:]` tags on retrieved claims (the 4Cs ordering, the CNCF maturity levels, the OpenGitOps principle count, `kubectl logs --previous`). The ledger's **BOOK-LEVEL RULING of 2026-08-31**, ratified at the Ch 18 gate, addresses this class directly and ends: *"Fact-accuracy stages should stop re-raising this class."*

Applied here — a cross-bearing to the owning section discharges the tag, provided the pointer names the owning section and the claim is not strengthened:

| Flag | Pointer | Owning section | Verdict |
|---|---|---|---|
| 4Cs ordering (item 6) | `Ch 12 §1 — four layers and four phases` ✓ | Ch 12 §1 owns "the 4Cs (Cloud, Cluster, Container, Code)" | **Discharged**, conditional on Ch 12 §1 carrying its own tag. Ordering is inherent in the owned set, not a strengthening. Close the flag. |
| OpenGitOps principle count (item 11) | `Ch 15 §3 — push, or pull` ✓ | Ch 15 §3 owns "**the four OpenGitOps principles**" | **Discharged.** Ch 20 says "one of the OpenGitOps principles" — *weaker* than the owner, and weakening is always safe. The proposed research gap belongs to Ch 15, not here. Close the flag for Ch 20. |
| `kubectl logs --previous` (item 24) | `Ch 13 §3 — looking inside` ✓ | Ch 13 §3 owns "`kubectl logs` · `--previous`" | **Discharged**, conditional on Ch 13 §3 being tagged. The corpus-truncation worry in the AUTHOR-REVIEW is then Ch 13's problem, not Ch 20's. |
| CNCF maturity levels (item 15) | `Ch 17 §2 — Sandbox, Incubating, Graduated, and who decides` ✓ | Ch 17 §2 owns the levels and lifecycle | **Split.** The *ordering* is discharged. The **stem's premise** — "before it has been asked to demonstrate broad production adoption" — is a claim about *admission criteria*, which exceeds the owner's scope and is a strengthening. The draft's own proposed fix is right: cut the clause so the stem reads "at the entry level of its maturity ladder." |

Three of four flags close on the ruling; the fourth needs a five-word cut, not a fetch. The conditionals are conditional only because I have no shards — each is a one-command check at the named section.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Zero statistics in any stem. Every exam-fact claim in the Instructions carries a `[source:]` tag.
- [x] **Fear-based content uses real examples.** No fear-based content.
- [x] **Simplification acknowledged.** Exemplary, and beyond the checklist's requirement. The Instructions volunteer the instrument's own limits: *"It was written by Lodestar Ledgers. It is not a leaked exam, not a reconstruction of one, and not a prediction of your score."* And on the four-option shape: *"The Linux Foundation does not publish how many options its multiple-choice items carry… Four options and one right answer is a reasonable authoring choice. **Do not read it as a disclosure.**"* That is guardrail 5 discharged by a chapter that had every commercial incentive not to.
- [x] **Authority claims cite legitimate sources.** LF candidate handbook, LF exam-code table, LF scoring policy, CNCF curriculum README, Kubernetes docs — all named and dated.
- [ ] **"Frequently tested" claims verifiable.** — **soft fail, one instance.** The phrase "frequently tested" appears nowhere ✓, and the B1 register discipline ("easy to confuse," never "frequently tested") is honored throughout: "part of why the confusion is easy to have" (18 C), "exactly what this manifest is testing" (26 A), "the distinction the question exists for" (41 A) — all correctly scoped to *the item*. One instance scopes to *the exam* instead: walkthrough 38 A, "three distinct jobs, and **the exam will test** whether you can keep them apart." Unsourced claim about exam behavior in a book otherwise scrupulous about the distinction. **Fix:** "…and keeping them apart is the whole of it." Two adjacent misconception-prevalence claims — "the single most common QoS error" (8 B), "the most common belief about StatefulSets" (21 A) — are claims about readers rather than about the exam and sit inside the sanctioned register; leaving them is defensible.
- [x] **No strawmanning of alternative study methods.** None. *"A reader who looks things up is measuring how good this book's index is. That is a fine thing to measure, but it is not the thing you came here for."* — wry, self-directed, and aimed at the practitioner.
- [x] **Subject dignity (v5.7 Part 14 #9).** Every wry beat points at the practitioner or at the instrument. *"a diagnostic instrument that keeps interrupting itself with encouragement is not a diagnostic instrument."*
- [ ] **Why-wrong explanations provided for all questions.** — **HARD FAIL.** Items 43–60 have no answer, no rationale, and no refutations. This is the Ethical Checkpoint line the truncation breaks.

### Why this is a guardrail failure and not just a missing section

The chapter's own Instructions make three promises it currently cannot keep:

1. *"Every question there carries the correct answer, an explanation of why the wrong options are wrong, the domain it belongs to, and a pointer back to the section that taught it."* — false for 30% of the instrument.
2. *"That is the whole argument for the score sheet at the end of this chapter."* — there is no score sheet.
3. *"The per-domain breakdown you are about to generate… is the only domain-level diagnostic you will get anywhere in this preparation."* — and the walkthrough preamble instructs the reader to "record two things per question… which domain it belonged to," which is only useful if the tally exists.

The third is the sharpest. Ch 20 correctly establishes, with a source, that the real exam *"does not report performance on individual items and will not honor requests for more detailed information."* The chapter then asks the reader to spend ninety minutes and hand-tally 60 results toward an instrument that is not in the file. A reader who follows the Instructions faithfully does real work for nothing. That is a truthfulness problem in reader-facing prose, not a formatting gap, and it is why the guardrails line reads fail rather than pass.

---

## Recommended fixes

Ordered by severity. Items 1–3 block ship.

**1. Restore the tail — stage 11, not stage 12/13.** Walkthroughs 43–60 plus the `## Scoring Rubric` block. The draft's own AUTHOR-REVIEW specifies the shape and explains why draft-v1's tail cannot be pasted in (draft-v2 rebuilt the exam block; item numbering does not map — v1's 43 is a DaemonSet log-collector item, v2's 43 is dynamic provisioning). Two things to carry in from this review:
   - **Do not adjust the exam block.** Its domain distribution already lands exactly on 26/17/10/7; the missing 18 items are already the right 8/4/4/2. Reweighting would break a correct instrument.
   - **Derive the rubric's per-domain rows mechanically** from the per-item domain tags, then assert 26/17/10/7. Draft-v1's rubric had rows that did not sum to their maxima and listed items 9, 12 and 48 twice; re-keying that table by hand against draft-v2's numbering would reproduce the defect.

**2. Re-key the answer positions, after step 1.** Two detectable signatures: every consecutive block of four contains each letter exactly once (10/10 blocks, p ≈ 5 × 10⁻¹¹), and zero adjacent repeats in 41 pairs (≈ 10 expected). Both are exploitable by elimination and both survive draft-v2's fix to draft-v1's all-B key. Generate an unconstrained random key balanced only globally (15 ± 2 per letter), then permute each stem's options to match. Verified safe: no option references another by letter, none is "all/none of the above," and no distractor's wrongness depends on its position.

**3. Restore the canonical pattern sentence in walkthrough 31.** Replace *"The object exists; nothing happens without the component"* with **"An object without its component does nothing."** This is the book's most-reinforced retrieval phrase (24 verbatim uses across six chapters, one of them a graded option), and paraphrasing it in the retrieval capstone reproduces the exact ledger-defect-into-shipped-text failure the 2026-08-31 errata note documents for Ch 6 and Ch 17. Consider naming it once more in walkthrough 43 when written, where the same pattern governs StorageClass and its provisioner.

**4. Expand SIG in item 53 D.** *"…brought to the Special Interest Group (SIG) that owns that subsystem."* A bare acronym in a correct answer, surrounded by three correctly-expanded siblings, inheriting a known Ch 8 first-use debt.

**5. Cut five words from item 15's stem.** *"…at the entry level of its maturity ladder, ~~before it has been asked to demonstrate broad production adoption~~."* The clause is a claim about admission criteria that exceeds what Ch 17 §2 owns, and it is the only one of the chapter's four provenance flags that the Ch 18-gate ruling does not discharge. The item works without it.

**6. Soften walkthrough 38 A.** *"the exam will test whether you can keep them apart"* → *"and keeping them apart is the whole of it."* One unsourced exam-behavior claim in an otherwise scrupulous chapter.

**7. Resolve the Ch 19 §3 contradiction at Ch 19's gate, not here.** Ch 20's framing is sourced and correct. Check Ch 19 for other instances of the superseded "NOT FOUND in any authoritative source" finding rather than editing line 541 alone — Ch 1 needed a retrofit for the same reason.

**8. Verify at Ch 8 §4 whether `drain` auto-cordons is taught there.** Walkthrough 19 B asserts it; the two contracts do not record it; no shards were available. If Ch 8 does not teach it, either add the clause there or drop the parenthetical here.

**Housekeeping for stage 14:** six HTML comment blocks (the stage-4 voice header, five AUTHOR-REVIEW notes, and the ship-blocker block) must be stripped at materialization. Items 1–3 and 5 above resolve four of them; the frontmatter note is a pipeline question, below.

**Passed through, not mine to resolve:** the frontmatter AUTHOR-REVIEW asks whether `structural_lint.py` reads `chapter_type` from the draft's own frontmatter or only from the outline in pipeline state. That determines whether stage 11's eight FAILs recur on the restored draft. It is a linter question rather than an integration one, but it will bite the next run. Its accompanying instruction is correct and worth repeating: **do not resolve those findings by adding Soundings or Bearings to a scored instrument** — every one of those rules carries `exempt_chapter_types: [mock_exam]`.

---

## What this chapter got right

Recorded because a fail-heavy summary misrepresents the document. Fifty-four cross-bearings resolve without a single defect, in a chapter that points into nineteen others and into four of the skeleton's immovable pinned anchors. Ten graded-use restrictions from the ledger's orphan list are honored across 240 options, including the one the ledger names Ch 20 specifically for (PodDisruptionBudget). Four homonym pairs are not merely avoided but disposed of in reader-facing text — the mesh-versus-cluster control plane, the Helm-versus-Deployment revision, the Linux-versus-Kubernetes namespace, and the operator-as-pattern-versus-person — which is the ledger's intent rather than its floor. The provenance framing in the Instructions matches the skeleton's post-correction prescribed wording near-verbatim, and both forbidden phrasings are absent. And the disclosure that the four-option shape is the book's own authoring choice rather than a published fact is the kind of thing a study guide gains nothing commercial by saying.

The defects are real and two of them block ship. But the chapter that arrives after they are fixed is in good condition.
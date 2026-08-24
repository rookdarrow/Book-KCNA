# Question-Quality Audit — Chapter 4

## Audit provenance (read first — pipeline defect)

This stage's prompt received `[file not available: draft-voice.md]` in place of the chapter draft. That is a **prompt-assembly bug, not a missing draft**. `context_packer.py:176` maps `{{draft_voice}}` → `draft-voice.md`, but `orchestrator.py:208–240` (`apply_voice_swap`) renames `draft-voice.md` into the canonical slot the moment the voice stage completes. By the time any Stage 6–9 audit runs, `draft-voice.md` no longer exists.

The audit below was performed against the actual voiced text at `.pipeline-state/ch-04/draft-v1.md` (mtime 05:04, post-swap; pre-voice baseline preserved at `draft-v1-prevoice.md`, mtime 04:54), located from disk.

**All four diagnostic prompts are affected** — `06_fact_accuracy_audit.md`, `07_curriculum_alignment_audit.md`, `08_question_quality_audit.md`, and `09_theming_density_audit.md` all reference `{{draft_voice}}`. Suggested fix: have `UPSTREAM_OUTPUT_KEYS["draft_voice"]` resolve through the same fallback `context_packer.py:281–286` already uses for KB-shard filtering (prefer `draft-voice.md`, fall back to `draft-vN.md`), or point the audit templates at `{{draft_v1}}` directly.

---

## Summary

- Chapter type: **content**
- Total questions inspected: **40**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **13** (across **3** checkpoints — 5 / 4 / 4)
  - Practice questions: **19**
- Question budget compliance: **met** — exact on every category, and on the chapter total
- Weak distractors (WARN): **7** (5 clear, 2 borderline)
- Trap answers that don't target real misconceptions (WARN): **3**
- Missing or incomplete why-wrong explanations (FAIL): **0 missing, 1 incomplete, 2 thin**
- Retrieval-practice spacing: **compliant on tag count (15.6%), substantively short (~9–12%)** — see that section
- Soundings spoiler check: **clean** — no question or answer reveals a ★ Fixed Point

**One cross-cutting defect outranks every individual question below, and it is a repeat of a Chapter 3 finding that was not carried forward.** It is reported in its own section immediately after the budget table.

The individual questions are, with the listed exceptions, well-built. Q14, Q16, Q8, Q7, Q2 and Bearings #1 Q3 / #2 Q3 are unusually good items — the distractors in those come from documented misconceptions rather than invented symmetry, and the why-wrong prose does real teaching. The problems are concentrated in three places: answer-position mechanics, two duplicated question pairs, and a set of concepts that the chapter teaches with emphasis and then never assesses.

---

## Question-budget compliance

Compared against `question_budget` in the outline frontmatter.

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 13 | 13 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 | 3 | **met** |
| Practice Questions | 19 | 19 | **met** |
| **Chapter total** | **40** | **40** | **met** |

Checkpoint distribution matches the outline's planned **5 + 4 + 4** exactly, placed after §2, §4, and §5 as specified. The outline's raise from B4's allocated 10 Bearings to 13 was honoured, and the justification (four distinct cognitive modes) holds up against the delivered items — #1 is structural recall, #2 is boundary reasoning plus misconception correction, #3 is syntax plus discrimination.

All eight `soundings_planned.topics` from the outline are present, in the planned order, one question each.

The interleaving contract is met exactly: the outline required **four** items requiring two sections at once, and the draft delivers Q14 (ConfigMap + namespace), Q17 (annotation + controller behaviour), Q18 (selector + namespace scope), Q19 (`spec`/`status` + labels). The draft's own claim at line 821 ("Four require two sections at once") is accurate.

**Difficulty-marker regression (WARN, not a budget failure).** All 13 Bearings items carry ⚪/🔵/🟡 markers. **None of the 19 Practice questions carries one.** Chapter 3's Practice block did carry them — its Stage 8 audit was able to report a 4 ⚪ / 11 🔵 / 4 🟡 mix against plan. Chapter 4's outline §7 specifies no difficulty column, so this is not an outline violation, but it is a consistency regression against the shipped chapter and it removes the difficulty signalling that skill Part 12 asks for. Recommend adding markers to the Practice block during revision, and adding a difficulty column to §7 of future outlines so the mix stays trackable book-wide.

---

## Cross-cutting: answer-position distribution

This is the same defect Chapter 3's Stage 8 audit reported as its lead finding. It is improved but not fixed, and the improved half is not the half that matters.

Correct-answer positions across all **24** multiple-choice items (5 Bearings + 19 Practice):

| Position | All MC (24) | Practice only (19) |
|---|---|---|
| A | **1 (4%)** | **0 (0%)** |
| B | 12 (50%) | 10 (53%) |
| C | 9 (38%) | 8 (42%) |
| D | 2 (8%) | 1 (5%) |

The B-clustering improved from Chapter 3 (66% → 50% overall). **The A-absence did not.** Across nineteen Practice questions, option A is never correct — exactly as in Chapter 3. A reader who notices this across two chapters is not being test-wise; they are reading a pattern the book is broadcasting. Eliminating A for free converts every four-option item into a three-option item, and B-first-among-the-remaining is a better-than-chance heuristic on top of that.

The mechanical cause is visible in the drafting: option A is consistently used as the "naïve first guess" slot. Q1 A is the kubelet confusion, Q4 A is the authorship inversion, Q7 A is the habit the docs correct, Q10 A is the misconception the chapter exists to dismantle, Q13 A is the workaround, Q17 A is the performance mental model. That is good pedagogical instinct about *what* belongs in a distractor and a bad habit about *where* it goes.

**Recommended fix (mechanical, cheap, no content change):** permute option order on roughly eight Practice items so the position distribution lands near 5/5/5/4. Specifically, promote the key to A on Q1, Q6, Q11, Q13, Q16 and to D on Q7, Q10, Q17. The distractors and the why-wrong text move with their options and need no rewriting; only the letters in the answer key change.

**Secondary tell: correct-answer length.** In **8 of 19** Practice items the key is the longest and most qualified option in its set — Q5, Q8, Q10, Q11, Q12, Q13, Q14, Q17. Q10 is the clearest case: the key runs 24 words against 8, 15 and 12 for the distractors, and is the only option carrying a hedging clause ("— but no encryption by default"). Combined with the position bias, Q10 is answerable by technique alone. Recommend either trimming the key or extending one distractor to match on Q10, Q12 and Q13 at minimum.

Neither of these is a content problem. Both are cheap. Both were flagged one chapter ago.

---

## Soundings spoiler check

The chapter's four ★ Fixed Points, against which every Soundings item is checked:

- **FP1 (§2):** `spec` is what you want, `status` is what is; you write `spec`, the system writes `status`.
- **FP2 (§3):** Not everything lives in a namespace — Nodes, PersistentVolumes, StorageClasses, and namespace objects are cluster-scoped.
- **FP3 (§4):** Neither ConfigMap nor Secret encrypts anything.
- **FP4 (§5):** The label selector is the core grouping primitive; labels are selectable, annotations are not.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Declarative vs imperative, in its general form | no | Answer names idempotency, state-independence, durability. Names no Kubernetes construct. §1's teaching (object as maintained record, `kubectl apply` as the verb) is untouched |
| 2 | Why a config format carries a version field | no | Answer is "schema evolution." Never names `apiVersion`. §2 supplies the field name and the per-object rationale |
| 3 | The two states of a control loop, plus the closer | no | Answer is "desired state, current state, and the controller" — Chapter 3's vocabulary, not Chapter 4's. **FP1 is that these states have field names and an authorship asymmetry.** Neither `spec` nor `status` appears anywhere in the question or answer |
| 4 | Which component receives a submission, what stores it | no | Answer is kube-apiserver / etcd — Chapter 3's Fixed Points, correctly retrieved. Reveals nothing about FP1–FP4 |
| 5 | One image, two environments, differing config | no — **see note** | Answer lists "an environment variable, a mounted config file, a startup argument, or a call to a configuration service." FP3 is about encryption and is untouched. **Note:** that four-item list is near-isomorphic to §4's four consumption paths, which §4 then teaches as load-bearing (and which Bearings #2 Q3 and Q11 both test). Not a Fixed Point, so not a FAIL — but it softens a taught list. Consider trimming the answer to two examples |
| 6 | Is base64 encryption? | no — **but see finding below** | Answer establishes base64 ≠ encryption as a general-IT prior and never mentions Secrets. FP3 is not revealed. The problem with this item is the opposite of a spoiler |
| 7 | Selecting by attribute in a familiar system | no | Answer is `WHERE environment = 'production'`, tag filters, saved searches. FP4's specific claim (labels selectable, annotations not, selector is *the* primitive) is entirely absent |
| 8 | Two teams, one shared system, same name wanted twice | no | Answer names "a scope for names: a namespace, a tenant, a project, a schema." This does hand the reader §3's opening framing — but **FP2 is the namespaced/cluster-scoped boundary**, not the existence of namespaces, and FP2 is untouched. The outline explicitly sanctioned this ("'Namespaces exist' is not the teaching") |

**Verdict: clean.** No Soundings question or answer reveals a Fixed Point.

**Rubric check: PASS.** The 6+ / 3–5 / 0–2 reading-strategy rubric is present and complete (lines 93–97). The 0–2 branch carries the outline's specific instruction rather than a generic one: *"If questions 3 and 4 were among your misses, re-read Chapter 3 §5–§6 before you start §2."* That is the best-calibrated rubric branch the pipeline has produced.

**Answer disclosure: PASS.** Answers are inside `<details><summary>Answers + reading strategy</summary>` (lines 74–99). Readers can attempt before seeing.

---

## Per-question findings

### Soundings Q6: "Is base64 encoding a form of encryption? If not, what is it for?"

**Issue:** The answer key ends *"Hold onto that answer; §4 will want it."* **§4 never uses it.** The `AUTHOR-REVIEW` comment at line 456 records that the base64 claim was deliberately omitted from §4 because `k8s-docs-secret-2026-08-23.md` is an abridged capture that does not support it (outline Open Question #2). The omission is the right call. The forward pointer was not updated to match.

The reader is explicitly told to carry an answer forward to a section that then never mentions it. That is a broken promise in the pipeline's most trust-sensitive block — the pre-test whose entire premise is "your score picks your reading strategy."

**Why-wrong explanation status:** n/a (open-ended; model answer is correct and well-argued)

**Recommended fix:** Two options, in order of preference.

1. **If the full Secret page is re-fetched during revision** (outline Open Question #2 recommends this), restore the base64 clause to §4's Fixed Point and the pointer becomes accurate with no further edit.
2. **If it is not fetched**, change the trailing sentence to point at what §4 *does* deliver: *"Hold onto that answer. §4 has a stronger version of the same lesson waiting for you."* This preserves the pretesting effect — the prior is still surfaced before the correction — without promising a specific payoff the chapter cannot make.

Do not simply delete the sentence; the forward pointer is doing real pretesting work, it is just aimed at the wrong target.

---

### Practice Q18: "A selector for `tier=frontend` returns three objects. You know that four objects in the cluster carry that exact label. What is the most likely explanation?"

**Issue:** Two of three distractors are fabricated for symmetry rather than drawn from real misconceptions, and the item substantially duplicates Bearings #3 Q4 — which is the better-built version of the same question.

**Distractor analysis:**
- A) *"One object's label was applied after creation, and post-creation labels are not indexed"* — **plausible to a specific misconception** (a database/indexing mental model). Legitimate distractor. The key rebuts it correctly with the docs' "attached at creation time and subsequently added and modified at any time."
- B) *"The fourth object is in a different namespace than the one the query was scoped to"* — correct.
- C) *"The fourth object also carries an annotation, which suppresses label matching"* — **implausible.** No practitioner believes annotations suppress label matching; there is no partial understanding of the material that produces this belief. The key concedes as much: *"invents an interaction between annotations and labels."* A distractor whose rebuttal is "this is invented" is a distractor that was invented.
- D) *"Equality-based selectors return a maximum of three results without pagination"* — **implausible, and internally nonsensical.** A hard limit of exactly three, matching the number in the stem. The key's rebuttal is four words: *"invents a result limit."*

With C and D eliminated on sight, this is a two-option item.

**Duplication:** Bearings #3 Q4 asks the identical question ("A selector matches several objects in one namespace, but matches nothing in another namespace where identically labelled objects demonstrably exist. What is happening?"), with the same key, and with better distractors — its option C (*"Set-based selectors work across namespaces but equality-based ones do not"*) targets a genuine half-memory of "set-based is more expressive," and its option D targets the reserved-prefix rule. The outline planned these as differentiated: Bearings #3 item 4 as a checkpoint item, and the Practice version *"in multiple-choice form with distractors."* The draft made **both** multiple-choice, so the planned differentiation collapsed into near-duplication and the weaker twin shipped.

**Why-wrong explanation status:** present but thin on C and D — necessarily, because there is nothing substantive to say about them.

**Recommended fix:** Preferred — **replace Q18 entirely** and let Bearings #3 Q4 own the selector/namespace interaction. The chapter has an untested concept that would slot straight into this position and into the same §5 block: the reserved `kubernetes.io/` and `k8s.io/` prefixes and the 63-character name-segment limit, which §5 teaches explicitly (line 601) and which currently appears only as distractor filler in Q17 C and Bearings #3 Q4 D. A stem such as *"Which of the following is a valid user-defined label key?"* tests real syntax knowledge and fills a coverage gap in one move.

Alternative, if Q18 is kept — revert **Bearings #3 Q4 to open-ended** (as the outline planned) so the two are no longer competing, and replace Q18 C and D with: *"The fourth object's label value differs in case — label matching is case-sensitive"* (real and commonly hit) and *"The fourth object is Terminating, and objects in Terminating state are excluded from selector results"* (real half-belief about lifecycle and selection).

---

### Practice Q15: "Which of the following is a valid **set-based** selector?"

**Issue:** Two distractors carry the same meaning, which a test-wise reader eliminates as a pair without knowing anything about selectors.

**Distractor analysis:**
- A) `environment != production` — **legitimate and the best distractor in the set.** `!=` reads like a set operation and is not one; the key singles this out correctly.
- B) `environment in (production, qa)` — correct.
- C) `environment == production` — equality-based.
- D) `environment = production` — equality-based.

**C and D are the same operator spelled two ways.** The chapter itself states this at line 609: equality-based selectors use `=`, `==`, and `!=`, and Bearings #3 Q1's answer says `environment = production` "(or `environment == production`)" — explicitly identical. A single-answer item cannot have two options that mean the same thing and expect either to be it, so both are eliminable on structure alone. That reduces a four-option item to a coin flip between A and B.

**Why-wrong explanation status:** present but thin. The key groups A, C and D under one shared reason and singles out A. It never addresses that C and D are the same requirement, which is the item's actual defect.

**Recommended fix:** Replace one of C/D with a distractor that fails for a *different* reason. Candidates, both drawn from material the chapter actually teaches: `environment notin production` (set-based operator, but missing the required parentheses around the value list) or `environment` alone with the key `exists` semantics misapplied. The cleanest single edit is to replace D with `!environment`, which *is* set-based syntax (the negation of `exists`) — turning the item from "spot the set-based one" into "spot the *valid* set-based one," a genuinely harder and more useful discrimination. Update the key accordingly.

---

### Practice Q11: "An application reads a setting from an environment variable populated by a ConfigMap. An operator edits the ConfigMap. What does the running application see?"

**Issue:** One weak distractor in an otherwise strong item.

**Distractor analysis:**
- A) *"The new value immediately"* — **real misconception**, and the most common one. ✓
- B) *"The new value after a short kubelet resync interval"* — **excellent distractor.** It is the sophisticated wrong answer: it correctly identifies the kubelet as the relevant actor and correctly knows that *something* resyncs, and gets the consumption path wrong. This is exactly what a trap answer should look like.
- C) *"The old value — the kubelet used the ConfigMap data when it launched the container"* — correct.
- D) *"An error, because the environment variable is now inconsistent with its source"* — **implausible.** No mental model of Kubernetes produces an expectation that the platform performs a consistency check between a running container's environment and its source object and then errors. The key's rebuttal confirms it: *"imagines a consistency check the platform does not perform."*

**Why-wrong explanation status:** present and specific for A, B and D.

**Recommended fix:** Replace D with a real belief. Best candidate, drawn from the chapter's own Bearings #2 Q3 answer key (line 569): *"The new value, but only if the ConfigMap is mounted with `subPath`."* This inverts a genuine and documented gotcha — `subPath` mounts are the case that specifically does *not* update — and it rewards a reader who read the Bearings #2 answer carefully. Alternatively: *"The old value until the Pod is deleted and recreated, at which point the container is rebuilt from the image"* — real, and wrong in an instructive way (the Pod does not need recreating for the *image*, only for the *launch*).

---

### Practice Q12: "ConfigMaps gained an analogous property in v1.19. Which statement about it is correct?"

**Issue:** One fabricated distractor, plus a retrieval tag the question does not earn (the tag issue is treated in the retrieval section below).

**Distractor analysis:**
- A) *"An immutable ConfigMap can be edited by an administrator but not by an application"* — **implausible.** This invents a caller-based privilege distinction on a field-level immutability flag. Nobody holds this belief, because nothing in Kubernetes works this way and nothing in the chapter suggests it might. The key concedes the point: *"invents a privilege distinction."*
- B) *"Immutability can be toggled off if the ConfigMap has no Pods consuming it"* — **the best distractor in the item.** It is the reasonable-safety-valve assumption, and the key names it as such. Genuinely tempting. ✓
- C) Correct.
- D) *"Immutability applies to the `data` field but the `binaryData` field remains editable"* — **good.** Precise, plausible to someone who half-remembers the field list, and rebutted precisely. ✓

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** Replace A with a real belief about immutability. Candidate: *"An immutable ConfigMap can be updated with `kubectl replace --force`, which recreates the object in place"* — this is genuinely tempting because `--force` *does* delete-and-recreate, so the reader has to reason about whether "delete and recreate" satisfies the rule (it does, but not as an *edit* — the UID changes and consumers must be relaunched). That turns a throwaway option into the item's hardest discrimination.

---

### Practice Q3: "Which of the following is **not** one of the four fields you must set in a manifest?"

**Issue:** No per-option why-wrong treatment, and heavy redundancy with three other items.

**Distractor analysis:**
- A) `apiVersion` — a required field. Correct as a distractor by construction.
- B) `kind` — a required field.
- C) `status` — correct answer.
- D) `metadata` — a required field.

The distractor construction here is sound for a "which is not" item; the three wrong options are necessarily the three remaining correct fields. No fabrication.

**Why-wrong explanation status:** **incomplete.** The key states the four fields and notes that `status` is system-supplied, but gives **no per-option treatment for A, B or D**. Rule 3 requires the key to explain why wrong answers are wrong. For a "which is not" item this is close to self-evident — but every other item in the chapter carries per-option prose, and the absence reads as an oversight rather than a decision. It is also a missed teaching opportunity: the natural per-option line here is *what each of the three does*, which is precisely the recall the item is nominally testing and currently is not.

**Redundancy:** Four separate items test the `spec`/`status` authorship boundary — Bearings #1 Q2, Bearings #1 Q3, Practice Q3, Practice Q4. That is 4 of 24 MC items (17%) on one Fixed Point. FP1 is the chapter's most reused fact and deserves weight, but Q3 and Q4 are the two thinnest of the four and sit adjacent to each other.

**Recommended fix:** Add three one-line why-wrongs (*"A is a required field: it selects the schema the rest of the document is parsed under"*, and so on). Then consider whether Q3 or Q4 should be repurposed — Q3 is the weaker of the pair, and the chapter has several emphasised-but-untested concepts competing for the slot (see Coverage below). Recommended replacement target for Q3: `Opaque` as the default Secret type, which §4 sets in bold (line 474) and no question touches.

---

### Practice Q10: "What does using a Secret instead of a ConfigMap give you?"

**Issue:** Borderline weak distractor, compounded by a severe length tell on a high-value item.

**Distractor analysis:**
- A) *"Encryption of the data at rest, enabled by default"* — **the target misconception, and the correct one to target.** This is the chapter's densest trap (B1 #16) and its Fixed Point exists to kill it. ✓
- B) Correct — 24 words, three clauses, one hedge.
- C) *"Encryption in transit between the API server and the kubelet, which ConfigMaps do not get"* — **good.** Plausible to a reader who knows TLS is involved somewhere and misattributes it. Rebutted precisely. ✓
- D) *"Automatic redaction so that no principal with API access can read the contents"* — **borderline.** There *is* an adjacent real belief (that Secret values are hidden in `kubectl get` output), but "no principal with API access can read" is a stronger claim than anyone actually holds, and it directly contradicts a sentence the reader met three paragraphs earlier. Weak as written; salvageable.

**Length tell:** B is 24 words against 8 (A), 15 (C), 12 (D), and is the only option with a qualifying clause. On this item, "pick the longest, most hedged option" is a reliable strategy that requires no knowledge of Secrets at all. Given that this is the item defending the chapter's most important Fixed Point, that is the worst possible place for a mechanical tell.

**Why-wrong explanation status:** present and specific for A, C and D.

**Recommended fix:** Two edits. First, **trim B** to match the others: *"A distinct object type and access-control surface, with no encryption by default."* The full three-clause version belongs in the answer key, where it already appears. Second, **sharpen D** to the belief people actually hold: *"Redaction in `kubectl get` output, so the values are not displayed"* — which is *true* of the display behaviour and *false* as a protection claim, making it a genuinely instructive near-miss rather than a straw man.

---

### Bearings #3 Q4, option A: "Labels are cluster-scoped, so the second namespace's labels were silently overwritten"

**Issue:** Borderline weak distractor within an otherwise strong item.

The "silently overwritten" half is not a belief anyone holds — it invents a destructive mechanism with no analogue in the platform. The "labels are cluster-scoped" half *is* a real confusion, and would work on its own. The key rebuts on two counts, which is correct but confirms the option is doing two jobs and only one of them honestly.

**Recommended fix:** Trim to the real half: *"Labels are cluster-scoped, so the same label key cannot carry different values in two namespaces."* Same misconception, no invented mechanism.

---

## Retrieval-practice spacing

- **Chapter 4 target:** 15% of the combined Bearings + Practice pool, drawn from Chapters 2–3 (outline **[B3]**; skill Part 10 places Chapter 4 in a 10–25% band). Chapter 1 is excluded from the retrieval schedule.
- **Pool:** 32 items (13 Bearings + 19 Practice).
- **Tagged:** **5 of 32 = 15.6%** — Bearings #1 Q5 `[retrieval: ch3]`, Bearings #2 Q4 `[retrieval: ch2]`, Practice Q1 `[retrieval: ch3]`, Practice Q2 `[retrieval: ch3]`, Practice Q12 `[retrieval: ch2]`.
- **Status: compliant on tag count. Short on substance.**

All three of **[B3]**'s named anchors are placed where the outline specified, and the placements are well-reasoned. But **two of the five tagged items do not require the reader to recall anything from an earlier chapter.** The earlier-chapter material appears in the *stem*, as scene-setting, rather than in what the reader must produce:

| Item | Tag | Does it require earlier-chapter recall? |
|---|---|---|
| Bearings #1 Q5 | ch3 | **Yes, partly.** Naming `spec`/`status` is current-chapter; naming **etcd** and **kube-apiserver** is genuine Chapter 3 recall. This is the outline's intended "translation" design and it works |
| Practice Q1 | ch3 | **Yes.** The component names are Chapter 3's, and the distractors (kubelet, scheduler, controller-manager) discriminate on Chapter 3 knowledge |
| Practice Q2 | ch3 | **Partly.** Rejecting A and D requires Chapter 3's non-terminating-loop model. But §2 of this chapter restates the loop in full, so a reader who skipped Chapter 3 can still answer from §2 |
| Bearings #2 Q4 | ch2 | **No.** The stem supplies the Chapter 2 context ("Chapter 2 named five ways… and deferred the most common one"). The answer — `kubernetes.io/dockerconfigjson` and `~/.docker/config.json` — is taught in §4, in the same paragraph that mentions Chapter 2 (line 485). A reader who read only §4 answers this correctly |
| Practice Q12 | ch2 | **No.** The stem *states* the Chapter 2 fact rather than asking for it: *"Chapter 2 established that container images are immutable: changing one means building a new image and recreating the container."* Every option then discriminates purely on Chapter 4's immutable-ConfigMap rule. No option can be eliminated using Chapter 2 knowledge |

**Genuine retrieval: 2 clear + 1 partial = 3–4 of 32 (9.4–12.5%)**, against a 15% target and a 10% skill-band floor. The chapter is at or just under the floor on substance while reporting 15.6% on tags.

This is not a drafting failure so much as a design collapse at the seam: Bearings #2 Q4 and Practice Q12 were both conceived as loop-closers (the pinned Chapter 2 `imagePullSecrets` payoff, and the image-immutability parallel), and closing a loop *for* the reader is the opposite of making them retrieve. Both items are good; they are just not retrieval items.

**Recommended additions.** Convert the two, or add one net item, using material Chapter 4 does not re-teach:

1. **Bearings #2 Q4 — make the reader supply the Chapter 2 half.** Reverse the direction: *"An `imagePullSecret` is a Secret of type `kubernetes.io/dockerconfigjson`. Chapter 2 listed five mechanisms for giving a cluster access to a private registry — name two others, and say why a Secret is the most common choice."* The Secret type is now given; the Chapter 2 list is what must be produced. Same loop closed, retrieval preserved.

2. **Practice Q12 — move the Chapter 2 content into the options.** Add a distractor that only Chapter 2 knowledge eliminates, e.g. *"Immutability makes the ConfigMap behave like a container image layer: the old contents remain readable to already-running containers, and new containers get the new contents"* — which requires the reader to hold Chapter 2's image/layer model to see why it does not transfer. Alternatively, retag Q12 as a non-retrieval item and add one genuine ch2/ch3 item elsewhere.

3. **Cheapest single fix if only one edit is made:** add a third genuine Chapter 3 item to the §1–§2 Practice block. The outline named an anchor that the draft used only as scene-setting — Chapter 3's *control loop as the consumer of `spec`* — and there is an unused angle on it: *"Two controllers watch the same object. Chapter 3 described what a controller does with the object it watches. What prevents them from conflicting?"* That requires Chapter 3's model and is answerable from nothing in Chapter 4.

Bearings #3 carries **zero** retrieval items. The outline explicitly sanctioned this ("loading a third retrieval here would push this checkpoint above its own topic"), and that judgement is sound — the fix belongs in the Practice block, not in checkpoint #3.

---

## Coverage vs concepts

Mapped against `kb_tags.concepts` and `kb_tags.commands` in the outline frontmatter. "Tested" means a Bearings or Practice item requires the reader to produce or discriminate on it — Soundings is a pre-test and does not count as coverage. Distractor-only appearances are marked as such.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| `kubernetes-object` | yes (B1.1, P3) |
| `record-of-intent` | **NO** — the "constantly maintained, not serviced-and-completed" framing is §1's central claim and the chapter title; nothing assesses it. P2 gets closest |
| `persistent-entity` | **NO** |
| `declarative-configuration` / `imperative-command` | **NO** — see note below |
| `manifest` | yes (B1.1, P3) |
| `yaml-by-convention` | **NO** |
| `apiversion` | yes (B1.4, P5) |
| `kind` | yes (B1.1, P3) |
| `metadata` | yes (B1.1, P3) |
| `object-name` | partial — only via namespace uniqueness (P9) |
| `object-uid` | **NO** |
| `spec` | yes (B1.2, B1.3, B1.5, P3, P4, P19) |
| `status` | yes (B1.2, B1.3, P3, P4, P19) |
| `desired-state` / `current-state` | yes (B1.3, B1.5, P2) |
| `actual-state-reconciliation` | yes (B1.3, P2) |
| `namespace` | yes (B2.1, B2.2, P7, P9, P14, P18) |
| `scope-for-names` | yes (P9, P14) |
| `initial-namespaces` | partial — only `kube-node-lease` is tested (P8) |
| `default-namespace` | **NO** — including the docs' production advice against using it |
| `kube-system` | distractor only (P8 option D) |
| `kube-public` | **NO** — and the chapter flags the convention-not-a-requirement point as one "examiners like" (line 404) |
| `kube-node-lease` | yes (P8) |
| `namespaced-resource` / `cluster-scoped-resource` | yes (B2.1, P6, P9) |
| `namespace-not-nested` | yes (P9, P7 option C) |
| `namespace-dns-form` | distractor only (P14 option B) |
| `configmap` | yes (B2.3, P11, P13, P14) |
| `configmap-size-limit` | yes (P13) |
| `configmap-consumption-paths` | yes (B2.3, P11) |
| `immutable-configmap` | yes (P12) |
| `decoupling-configuration` | **NO** — the one-image-two-environments motivation is §4's opening and is never assessed |
| `secret` | yes (P10) |
| `secret-types` | partial — only `dockerconfigjson` (B2.4) |
| `opaque-secret` | **NO** — §4 sets "**the default type**" in bold (line 474); nothing tests it |
| `dockerconfigjson` | yes (B2.4) |
| `service-account-token-secret` | **NO** — deliberate, deferred to Ch 5/12. Acceptable |
| `tls-secret` | **NO** — table row only. Acceptable |
| `secret-storage-default` | yes (P10) |
| `secret-hardening` | **NO** — deliberate, handed to Ch 12. Acceptable |
| `encryption-at-rest` | partial — named inside P10's key and option B, never the subject of an item |
| `label` | yes (B3.1, B3.3, P17, P19) |
| label syntax (63-char name, reserved `kubernetes.io/` prefix) | distractor only (P17 option C, B3.4 option D) — §5 teaches it explicitly at line 601 |
| `label-selector` | yes (B3.1, B3.4, P15, P17, P19) |
| `equality-based-selector` | yes (B3.1, P15) |
| `set-based-selector` | yes (B3.1, P15) |
| `matchlabels` / `matchexpressions` | yes (B3.2, P16) |
| `annotation` | yes (B3.3, P17) |
| `kubectl-apply` | yes — in P1's stem |
| `kubectl-get` | **NO** |
| `kubectl-create` | **NO** — not taught either; correctly out of scope |
| `kubectl-explain` | **NO** — §2 teaches it as the lookup tool that makes unfamiliar `spec` blocks readable (line 278), and it is load-bearing for the chapter's transferability claim |
| `kubectl-api-resources` | **NO** — §3's ⚓ Worth Securing frames it as the answer to the namespaced/cluster-scoped question (line 389), including for resource types that postdate the book |

### The three gaps worth fixing

**1. Declarative versus imperative is never assessed after reading.** This is the largest gap in the chapter. §1 is **pinned by a published Chapter 1 cross-bearing** that promised this section would name the distinction; §6 is the Zenith and spends its closing pages on the precise version of the claim ("the objects are declarations, and the imperative commands work by changing declarations"); the concept is one of the book's nine cross-cutting themes and is retrieved in Chapters 6, 14 and 15. It is tested **once, in the Soundings pre-test**, and never again. The nearest post-reading contact is Practice Q2 option B — the imperative instinct deployed as a distractor, which the key rightly calls "the single most useful wrong answer in this chapter" — but no item *stems* on it.

A reader can score 40/40 on this chapter without ever demonstrating they understood its title.

Recommended item, for the §1–§2 Practice block, testing §6's precise claim rather than the slogan: *"`kubectl scale deployment/web --replicas=5` is an imperative command. What does it actually do?"* with the key being *"edits `spec.replicas` on the Deployment object; a controller then observes the difference and acts"* and distractors covering (a) it directly instructs the kubelet to start containers, (b) it bypasses the object model and acts on running Pods, (c) it is rejected because Kubernetes only accepts declarative input. Option (c) in particular targets the over-correction the chapter's own precision guard warns about, and would reward a reader who read §6's honest-correction subsection.

**2. `kube-public` and `Opaque` are both emphasised and both untested.** The chapter marks each as an examiner favourite — `kube-public`'s convention-not-requirement status gets its own bolded paragraph, `Opaque` gets bold in the types table — and neither appears in any item. Both are cheap to add and both fit existing blocks: `kube-public` slots into the §3 Practice block alongside Q8 (or as a fifth option-set on Q8 itself), and `Opaque` slots into the §4 block, ideally as the replacement for Q3 or Q12A discussed above.

**3. Both lookup commands are taught as capabilities and neither is assessed.** `kubectl explain` and `kubectl api-resources --namespaced` are the chapter's two answers to "you do not have to memorise this," and the ⚓ Worth Securing callout makes an explicit pedagogical argument for the second. Chapter 8 owns the kubectl command surface, so a syntax question would violate the scope boundary the outline draws — but a *capability* question does not. Recommended, for the §3 block: *"You encounter a resource type installed by an operator and need to know whether it is namespaced. What settles it?"* This tests the §3 Fixed Point's practical corollary, respects Chapter 8's boundary, and rewards the reader who took the callout seriously.

---

## Recommended edit list, in priority order

| # | Item | Edit | Cost |
|---|---|---|---|
| 1 | Whole Practice block | Permute option order on ~8 items to break the A-never-correct / B-half-the-time pattern. No content change | Trivial — letters only |
| 2 | Soundings Q6 | Fix or remove the *"§4 will want it"* pointer, which §4 does not honour | One sentence |
| 3 | P-Q18 | Replace entirely (label-key syntax is the best replacement); or revert B3.4 to open-ended and rebuild C and D | One item |
| 4 | P-Q3 | Add per-option why-wrong for A, B, D | Three lines |
| 5 | P-Q15 | Replace C or D — `==` and `=` are the same operator, so both are eliminable as a pair | One option + key line |
| 6 | Coverage | Add one item on declarative-vs-imperative (§6's precise claim, not the slogan) | One item |
| 7 | Retrieval | Convert B2.4 and/or P-Q12 into genuine recall, or add one net Chapter 3 item | One item |
| 8 | P-Q10 | Trim the key to match distractor length; sharpen option D to the real belief | Two edits |
| 9 | P-Q11 / P-Q12 | Replace P-Q11 D and P-Q12 A with real misconceptions (`subPath`; `replace --force`) | Two options |
| 10 | Coverage | Add items for `kube-public` (convention) and `Opaque` (default type) | Two items |
| 11 | Practice block | Add ⚪/🔵/🟡 difficulty markers, matching Chapter 3's convention | Nineteen glyphs |
| 12 | B3.4 option A | Trim "silently overwritten" to the real half of the misconception | One clause |

Edits 6, 7 and 10 add three to four net items. At 40 questions against a 40-question budget, the chapter has headroom in the book-level count (715 against a 300 floor) but would exceed its own `question_budget`. If the budget is treated as a ceiling, edits 6 and 10 should displace P-Q3 and P-Q18 rather than supplement them — both are the weakest items in the chapter and both are recommended for replacement independently.
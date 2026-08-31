Write access to the book's pipeline-state tree isn't granted (the orchestrator captures stage output from stdout by design). Emitting the audit as the stage output:

```markdown
# Question-Quality Audit — Chapter 15

*Audited against `draft-v1.md` (1,313 lines). Line numbers cite that file. `draft-voice.md` does not exist at this stage.*

## Summary

- Chapter type: **content**
- Total questions inspected: **45**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **16** (across **3** checkpoints — 6 / 5 / 5)
  - Practice questions: **21**
- Question budget compliance: **met** (45 of 45, every category exact)
- Weak distractors (WARN): **2** (Q9 A; Q2 D, borderline)
- Trap answers that don't target real misconceptions (WARN): **1** (Q9 A — fabricated for symmetry)
- Missing or incomplete why-wrong explanations (FAIL): **0** — all five multiple-choice items explain every wrong option
- Retrieval-practice spacing: **compliant** — 4 of 16 = **25.0%**, exactly the outline's ceiling
- Soundings spoiler check: **clean** (0 of 8 reveal a ★ Fixed Point; 1 watch item recorded)
- Soundings rubric present (6+ / 3–5 / 0–2): **yes** (draft-v1.md:87–93)
- Soundings answers in `<details>`: **yes** (draft-v1.md:68–95)

**Three findings outrank everything else in this report, and none of them is a distractor problem:**

1. **FAIL — ★ Fixed Point 3 is never tested.** "A GitOps delivery agent is a controller; its desired state lives in a repository instead of etcd; nothing else about the architecture is different" (draft-v1.md:546–548) is the chapter's central structural claim, its Zenith payoff, and Exam Alert high-priority topic #3. No question in any of the 45 asks the reader to produce it. See § "Coverage vs concepts".
2. **FAIL — ☆ TYB 2 Q2's stem and answer key contradict each other and contradict Fixed Point 4.** See per-question findings.
3. **WARN — three items are answer-identical or near-identical duplicates** (Practice Q8 ≈ TYB 2 Q1; Practice Q6 ≈ TYB 1 Q6), consuming two of twenty-one practice slots on discriminations already made.

## Question-budget compliance

Compared to `question_budget` in the outline frontmatter.

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 16 | 16 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 (outline plans 3) | 3 (6 + 5 + 5) | **met** — each ≥5 |
| Practice Questions | 21 | 21 | **met** |
| **Chapter total** | **45** | **45** | **met** |

No budget action required. The outline's raise from B4's 10 Bearings to 16 was carried through correctly, and the three-checkpoint split (6/5/5) is what makes the 25.0% retrieval figure land cleanly.

## Soundings spoiler check

The chapter's five ★ Fixed Points, for reference:

- **FP1** (draft-v1.md:237–239) — twelve-factor is constraints an app accepts; Kubernetes implements the platform side and cannot implement the application side.
- **FP2** (draft-v1.md:251–253) — `RollingUpdate` / `Recreate` are Deployment field values; blue/green and canary need tooling above the Deployment.
- **FP3** (draft-v1.md:546–548) — a delivery agent is a controller; desired state lives in a repository; nothing else changed.
- **FP4** (draft-v1.md:600–602) — `OutOfSync` means live state deviates from target state in Git; drift signal, not error.
- **FP5** (draft-v1.md:1029–1031) — GitOps is not "running CI from Git"; none of the four principles mentions integration or a pipeline.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 (:52) | Controller compares target vs actual, acts, cadence (Ch 3 §6) | **no** | Stem and answer stay entirely in Ch 3 vocabulary. No mention of Git, repository, agent, or delivery. Supplies the *first operand* of FP3's substitution without performing it — which is the intended pre-test design. |
| 2 (:54) | `spec` vs `status`, and what disagreement means (Ch 4 §2) | **no** | FP4 requires the phrase "in Git." The stem and answer never leave the object model; answer reads "a report, not necessarily a fault" (:73), which is the Ch 4 claim, not the `OutOfSync` claim. |
| 3 (:56) | Default update strategy; `maxSurge` / `maxUnavailable` (Ch 6 §4) | **no** | Asks only what the default does. Does not name blue/green or canary, and does not state the field-vs-pattern line that constitutes FP2. Correctly avoids re-opening Ch 6:665's deferral. |
| 4 (:58) | CRD installed — what can exist, what must still be true (Ch 6 §8 / Ch 10 §3) | **no** | Tests custom resources in isolation. Never joins them to a delivery agent, which is the join FP3 makes. |
| 5 (:60) | In-cluster process needs cross-namespace create/delete (Ch 5 §6, Ch 12 §2–§3) | **no** | The §4 agent-identity material is a ⚠ Navigational Hazards block (:695–701), not a ★ Fixed Point, so no Fixed Point is in scope. Reader constructs the requirement; §4 later attaches the name. |
| 6 (:62) | Where environment-specific config belongs (Ch 4 §4, Ch 2 §2) | **no** | Answer gives the platform-side half ("ConfigMaps and Secrets, injected at runtime", :81). FP1's actual claim — the platform/application partition, and that containerizing does not confer compliance — is absent, as is the term "twelve-factor". |
| 7 (:64) | Direct production change outside process: consequence and detection lag | **no** — *watch item* | The outline flagged this as the one item at risk. It holds. The stem asks for *consequence*, never for detection mechanism, and the answer's framing is that **"nothing announces this"** (:83) — the opposite of FP4's claim that a status field reports it. It sets up the problem FP4's mechanism solves rather than revealing it. **Watch in revision:** the answer's clause "at the next deployment, when the change is silently overwritten" (:83) drifts toward §6's Flux-reverts-your-patch behavior (:880) and TYB 3 Q4. Keep it as an overwrite-by-accident outcome; do not let it acquire the word "reverted." |
| 8 (:66) | What commit history gives you that a live server does not | **no** | Approaches OpenGitOps principle 2 and rollback-by-revert from the outside, as consequences. Neither is a ★ Fixed Point. FP5 is untouched — no stem mentions CI, pipelines, or building. |

**Verdict: clean.** All eight are answerable from Chapters 1–14 or general professional knowledge, none states or paraphrases a Fixed Point, the rubric is present with all three branches, and the 0–2 branch correctly names **sections** (Ch 3 §6, Ch 4 §2) rather than chapters and singles out Q1 as non-optional (:93).

## Per-question findings

### ☆ TYB 2 Q2 (draft-v1.md:711): "An Argo CD application shows `OutOfSync`. The most recent sync operation completed successfully. Give two different explanations, only one of which involves anything going wrong."

**Issue: FAIL — the stem's constraint cannot be satisfied by the key, and the key contradicts the chapter's own Fixed Point.**

The stem promises exactly one benign and one problematic explanation. The key (:730–738) supplies:

- *"Nothing went wrong:"* somebody edited a live object with `kubectl`. — benign, correct.
- *"Something did go wrong:"* a new commit landed in the tracked path and has not been applied yet. — **this is not something going wrong.** It is the normal transient state between commit and sync.
- A third explanation (`OutOfSync` immediately after a successful sync), unlabelled.

FP4 at :602 lists both of the key's first two causes side by side as non-failures: *"A person editing an object by hand produces an `OutOfSync` application, **and so does a commit that has not been applied yet**."* The key labels the second one a failure four hundred lines later. A reader who has internalised the Fixed Point — which is the reader this chapter is trying to produce — will read the key as wrong, and they will be right.

**Distractor analysis:** n/a — open response.

**Why-wrong explanation status:** present and specific for the misconception it targets (*"Why 'the sync failed' is wrong"*, :738). The defect is upstream of the why-wrong, in the stem/key contract.

**Recommended fix — change the stem, not the key.** The key's content is correct and well-sourced; only its labelling is wrong. Replace the stem with:

> **2.** An Argo CD application shows `OutOfSync`. The most recent sync operation completed successfully. Give two explanations that require nothing to have failed, and say where a *failure* would have been reported instead.

That aligns stem, key, and FP4; keeps the item's real target (sync status vs sync *operation* status, :604); and lets the key's existing third paragraph carry the discrimination rather than sitting unlabelled. Then delete the *"Something did go wrong:"* label at :734 and re-head that paragraph *"Also benign:"*.

---

### Practice Q9 (draft-v1.md:1125): "Which statement about push-based delivery is accurate?"

**Issue: WARN — one implausible distractor reduces a four-option item to three.**

**Distractor analysis:**
- A) *It cannot be automated* — **implausible, and fabricated for symmetry.** No reader holds this belief. Push-based CD is the arrangement teams reach for *because* it automates; the key concedes as much (*"push-based delivery is normally entirely automated; that is its appeal"*, :1205). A distractor whose own answer key calls it obviously false is not testing anything.
- B) *It stores cluster-write credentials outside the cluster* — correct.
- C) *It is incompatible with storing manifests in Git* — **strong.** Targets the reader who over-learned "GitOps = manifests in Git" and now believes the two are mutually exclusive. The key rightly calls this "what makes the distinction subtle" (:1205), and it is the same confusion Q8 and TYB 2 Q1 exist for.
- D) *It bypasses the Kubernetes API server* — **strong.** Mirrors the derived Exam Alert trap ("assuming a GitOps agent writes to the datastore directly") back onto push, and Ch 3 §5 is the correction.

**Why-wrong explanation status:** present and specific for all three wrong options (:1205).

**Recommended fix:** replace A with a distractor that carries a real misconception. Suggested:

> A) It requires the cluster to be reachable from the public internet

Plausible (many readers assume push implies an exposed API endpoint), wrong for a defensible reason (private runners, VPN, and self-hosted CI all push to unexposed clusters), and it strengthens the section's actual argument — the pull/push difference is about *credential location*, not *network topology*. Add one clause to the key accordingly.

---

### Practice Q13 (draft-v1.md:1143): "An Argo CD `Application` reports `OutOfSync`. Which of these could be the cause?"

**Issue: WARN — the "all of the above" format defeats the item's own purpose.**

**Distractor analysis:**
- A) *An engineer ran `kubectl scale` on a managed Deployment* — plausible and correct; stated almost verbatim in FP4 (:602).
- B) *A new commit landed in the tracked path and has not been applied* — plausible and correct; also stated verbatim in FP4.
- C) *The most recent sync operation failed* — the interesting option, and the only one that requires the reader to hold two fields apart.
- D) *All of the above* — correct.

Because FP4 explicitly names A and B as causes, any reader who has read the Fixed Point recognises two correct options immediately and can infer D **without ever evaluating C** — which is the only option that tests the sync-status / sync-operation-status discrimination the item was built for. The key does the discrimination work (:1221–1223), but the reader never had to.

There is a second, subtler problem. The chapter hammers "`OutOfSync` is not an error." A reader who has over-learned that will read C as the trap and want an "A and B only" option. None exists, so their correct instinct is punished.

**Why-wrong explanation status:** present and specific — the key explains A, B, and C individually (:1221).

**Recommended fix:** convert to a discrimination item that forces the reader to name the field. Suggested:

> **Q13.** An Argo CD `Application` reports `OutOfSync`, and the most recent sync operation reports success. Which is true?
>
> A) The report is contradictory; one of the two must be stale
> B) Sync status and sync operation status answer different questions, and both readings are valid simultaneously
> C) `OutOfSync` overrides the operation status; the sync did not actually complete
> D) The application will self-heal, so the report can be ignored

B is correct. A targets the reader who thinks the two fields are one fact. C targets the "`OutOfSync` means failure" misconception directly — the one Exam Alert #2 exists for. D targets the reader who assumes self-heal is on by default, which is *exactly* the assumption the AUTHOR-REVIEW note at :654 flags as unsourced, and the key can say so without asserting a default. This version also removes the overlap with TYB 2 Q2 noted below.

---

### Practice Q8 (draft-v1.md:1123) vs ☆ TYB 2 Q1 (draft-v1.md:709)

**Issue: WARN — answer-identical duplicates.**

Both present a CI pipeline that builds an image and then runs `kubectl apply` against the cluster with externally-held credentials, and both ask which OpenGitOps principles are satisfied and which fail. Both keys return **1 and 2 satisfied, 3 and 4 failed**, and both close on the same observation about storing manifests in Git being insufficient (:728, :1201). Q8's only addition — "commits the new image tag to a Git repository" — strengthens principle 2, which neither item was testing.

**Distractor analysis:** n/a — both open response.

**Why-wrong explanation status:** present and specific in both.

**Recommended fix:** keep TYB 2 Q1 (it closes the §3–§4 arc and is correctly placed) and **repurpose Practice Q8 to carry Fixed Point 3**, which is currently untested anywhere in the chapter. Suggested replacement:

> **Q8.** A colleague who has just installed Argo CD says "so this is a new kind of thing — a deployment engine that sits outside the normal Kubernetes machinery and pushes state in." Correct them in structural terms: what *category* of component is the Argo CD application controller, what two things does it compare, and what single element of the Chapter 3 architecture is different?

This discharges FP3, Exam Alert high-priority topic #3, and the §7 Zenith claim in one item; it is fully supported by the quoted architecture snapshot at :536 (*"is a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state"*); and it is a correction task, so the misconception sits in the stem where the reader must dismantle it.

---

### Practice Q6 (draft-v1.md:1119) vs ☆ TYB 1 Q6 (draft-v1.md:345)

**Issue: WARN — the same question with the same four items, reworded.**

TYB 1 Q6: *"Which of these is a value you can set on a Deployment's `.spec.strategy`, and which requires additional tooling: `Recreate`, blue/green, `RollingUpdate`, canary?"*
Practice Q6: *"Sort these into 'value of a Deployment's `.spec.strategy`' and 'pattern requiring tooling above the Deployment': canary, `Recreate`, blue/green, `RollingUpdate`."*

Identical item set, identical partition, identical keys (:370, :1191). Testing FP2 twice is defensible — it is Exam Alert topic #4 — but the second pass should test it *differently*, or it is channel redundancy (skill Part 7) rather than spaced retrieval.

**Recommended fix:** keep TYB 1 Q6 as the recall form and turn Practice Q6 into an application form. Suggested:

> **Q6.** A team tells you they have configured blue/green deployment "in the Deployment spec." Without seeing their manifests, what do you already know is wrong with that description, and what two things must actually exist for them to be running blue/green?

Same Fixed Point, scenario-shaped, and it exercises the *consequence* of the distinction rather than re-sorting the same four words.

---

### Practice Q2 (draft-v1.md:1101): "…strongest evidence that an application has correctly factored out its config?"

**Issue: WARN (minor) — one thin distractor.**

**Distractor analysis:**
- A) *Reads all settings from a `config.yaml` at startup* — **strong.** The methodology names this as the near-miss (*"still has weaknesses: it's easy to mistakenly check in a config file"*, quoted at :356), and §1's 🪝 Snag exists because readers land here.
- B) Correct — the litmus test, quoted verbatim.
- C) *Separate configuration bundles named `staging` and `production`* — **strong.** Targets the grouped-environments anti-pattern the methodology bans by name. A reader who thinks environment bundles are good practice is a real reader.
- D) *Stores all settings in a database table* — **thin.** Nobody proposes a DB table as *evidence of correct factoring*; it is a relocation, not a belief. The key handles it in half a sentence (*"it relocates the problem without solving it"*, :1177), which is the tell.

**Why-wrong explanation status:** present and specific for A, C, D (:1177).

**Recommended fix:** low priority — the item works on the strength of A and C. If touched, replace D with *"It has no configuration; every value is a compile-time constant"*, which targets a real and confidently-held misconception (that eliminating config satisfies factor III, when factor III is about *where config lives*, not about having less of it).

---

### Items reviewed and found sound

**Practice Q4** (:1110) is the best-built multiple-choice item in the chapter and worth preserving as the pattern. Every distractor pairs a *wrong strategy* with a *correct cost* — `RollingUpdate`/capacity, canary/traffic-splitting, blue/green/double capacity — so no option can be eliminated on the half the reader happens to remember. D is the strongest trap in the chapter: blue/green does keep versions apart *in traffic terms*, and the key draws the distinction precisely (:1185).

**Practice Q11** (:1134) lists all four principles as options. In a "which of the four is violated" item that is structurally required, not a plausibility failure, and C (*pulled automatically*) is a genuine trap for readers conflating principles 3 and 4. Key explains all three wrong options collectively and correctly (:1213).

**TYB 1 Q5 / Practice Q5** are a complementary pair rather than duplicates — one asks *which strategy fits an HTTP workload with metrics* (canary), the other *why canary fails a queue worker* (blue/green). The pairing tests the same trade-off from both sides. Good design; leave alone.

**TYB 3 Q5** (:915) is correctly placed and correctly worded. Restricting the answer to Ch 3 terms ("without mentioning Git, repositories, or delivery") is what keeps it a retrieval item rather than a chapter item, and placing it immediately before the Zenith is the strongest structural decision in the question set.

## Retrieval-practice spacing

- Chapter 15 target: **25%** of checkpoint questions from earlier chapters (arc-outline ceiling; outline sets 4 of 16 as the exact figure)
- Actual: **25.0%** — 4 of 16 tagged `[retrieval: chN]`
- Status: **compliant**

| Item | Tag | Source | Genuine retrieval? |
|---|---|---|---|
| TYB 1 Q3 (:339) | `[retrieval: ch4]` | Ch 4 §4 | **yes** — answer (ConfigMap/Secret, value lives in etcd outside the image) lives wholly in Ch 4 |
| TYB 1 Q4 (:341) | `[retrieval: ch6]` | Ch 6 §4 | **yes** — the arithmetic is Ch 6 mechanics; §2 deliberately declined to restate them |
| TYB 2 Q4 (:715) | `[retrieval: ch12]` | Ch 12 §3 | **yes** — stem is dressed as a delivery-agent question, but the answer is ServiceAccount + ClusterRoleBinding, which is Ch 12's |
| TYB 3 Q5 (:915) | `[retrieval: ch3]` | Ch 3 §6 | **yes** — and the strongest of the four, being explicitly fenced off from this chapter's vocabulary |

All four survive the outline's narrow test (*a retrieval question is one whose **answer** lives in an earlier chapter*). Spread covers Ch 3, 4, 6, and 12, satisfying both the "from all previous" requirement and the ≥4-back floor. The Ch 9–13 window is covered by the Ch 12 draw.

No additions needed. If Practice Q8 is repurposed as recommended above, note that it would *not* count toward this figure — the spacing rule scopes to checkpoints, and the count stays at 4 of 16.

## Coverage vs concepts

Against `kb_tags.concepts` in the outline frontmatter (38 entries).

| Concept introduced in chapter | Tested in a question? |
|---|---|
| twelve-factor-app | yes (Q1, Q2, Q3; TYB1.1, TYB1.2) |
| factor-iii-config-in-environment | yes (Q2; TYB1.2, TYB1.3) |
| factor-vi-stateless-processes | yes (Q3; TYB1.1) |
| factor-ix-disposability | **NO** — appears only as a *rejected* distractor in TYB1.1's key (:354). Never tested on its own terms, despite being promised by name at Ch 5:559 and given a 🪢 Mnemonic at :227 |
| factor-xi-logs-as-event-streams | yes (Q1) |
| deployment-strategy-vocabulary | yes (Q6; TYB1.6) — *redundantly; see findings* |
| recreate-strategy | yes (Q4, Q6) |
| blue-green-deployment | yes (Q4, Q5, Q6) |
| canary-deployment | yes (Q5, Q6; TYB1.5) |
| progressive-delivery | yes (Q7) |
| push-based-delivery | yes (Q8, Q9; TYB2.1) |
| pull-based-delivery | yes (Q10; TYB2.3) |
| cicd | yes (Q12) — but the CI / continuous **delivery** / continuous **deployment** three-way split (:394–400) and the "both abbreviate to CD" 🪝 Snag (:402) are untested |
| gitops | yes (Q8, Q11, Q12; TYB2.1) |
| opengitops-four-principles | yes (Q8, Q11; TYB2.1) |
| declarative-principle | yes (Q8, Q11 — as a satisfied principle) |
| versioned-and-immutable-principle | yes (TYB2.5; Q15) |
| pulled-automatically-principle | yes (Q8, Q11; TYB2.1) |
| continuously-reconciled-principle | yes (Q11; TYB3.4) |
| blast-radius | yes (Q10; TYB2.3) |
| argo-cd | yes (Q13–Q17, Q21; TYB2.2, TYB2.5) |
| argo-cd-application-resource | yes (Q14, Q15, Q21) |
| source-of-truth | **NO** — used throughout as connective tissue, never the object of a question |
| manifest-source | yes (Q14) |
| tracking-branch-tag-commit | yes (Q15; TYB2.5) |
| synced-outofsync | yes (Q13, Q17; TYB2.2) |
| sync-operation | yes (Q13 key; TYB2.2) — the *refresh vs sync* distinction (:568) is untested |
| self-heal | **NO** — introduced at :643–654 and tested nowhere |
| drift-detection | yes (TYB3.4; TYB2.2) |
| rollback-by-revert | yes (Q18) |
| delivery-agent-identity | yes (Q16; TYB2.4) |
| sync-hook-phases | yes (Q20; TYB3.2) |
| sync-wave | yes (Q19; TYB3.1) |
| flux | yes (Q21; TYB3.3, TYB3.4) |
| flux-controller-set | yes (Q21) |
| flux-bootstrap | **NO** — given a full prose beat at :884–888 ("Flux manages itself like any other resource") and tested nowhere |
| multi-cluster-delivery | yes (Q21) |

### Fixed Points and Exam Alert topics, cross-checked

| Claim | Tested? |
|---|---|
| FP1 — platform side vs application side | yes — Q3 tests exactly this ("containerized + Deployment ≠ compliant") |
| FP2 — Deployment fields vs patterns needing tooling | yes — Q6, TYB1.6 (twice, redundantly) |
| **FP3 — a delivery agent is a controller; only the desired-state store moved** | **NO — FAIL** |
| FP4 — `OutOfSync` is a drift signal, not an error | yes — Q13, Q17, TYB2.2 |
| FP5 — GitOps is not "running CI from Git" | yes — Q12 |
| Exam Alert #1 — four principles, in order | partial — Q8/Q11/TYB2.1 test them individually; nothing asks for the ordered set |
| Exam Alert #2 — `OutOfSync` is a signal | yes |
| **Exam Alert #3 — Argo CD is a Kubernetes controller** | **NO — FAIL** |
| Exam Alert #4 — strategy vocabulary vs Deployment fields | yes |

**On FP3.** This is the chapter's load-bearing claim: it is the Fixed Point at :546, high-priority Exam Alert topic #3 at :1071, the §7 Zenith's entire content, and the subtitle. §7 correctly carries no checkpoint — it is the Zenith, and interrupting it with questions would be wrong — so the burden falls entirely on the Practice Questions, and none of the twenty-one carries it. A reader can answer all 45 questions correctly without once stating that a delivery agent is a controller.

Q17 is the nearest approach: its key closes on *"That relocation is the whole substitution"* (:1241). But Q17 asks about the `spec`/`status` mapping, not about the *category* of component, and a reader can answer it fully while still believing Argo CD is a new kind of thing bolted onto Kubernetes — which is precisely the belief FP3 exists to destroy.

The fix is free: **Practice Q8 is a duplicate of TYB 2 Q1 and can be repurposed** (draft text supplied in the per-question findings above). That closes the chapter's largest coverage gap without touching the question budget.

### Recommended additions if slots are found

Priority order. Only the first requires no budget change.

1. **FP3 / Argo-CD-is-a-controller** — repurpose Practice Q8. **Do this one.**
2. **self-heal** — a natural fit inside the revised Q13 (option D in the suggested rewrite tests the "self-heal is on by default" assumption without asserting a default, respecting the AUTHOR-REVIEW note at :654).
3. **factor IX disposability** — promote it out of TYB1.1's why-wrong into its own item. The three-part shape at :227 ("fast up, clean down, survive the floor dropping") is question-shaped already, and the third clause — *"robust against sudden death"* — is the one readers miss.
4. **flux-bootstrap** — a one-line addition to Q21, which already contrasts the two postures: *"…and name the thing Flux does at install time that Argo CD does not."*
5. **CD ambiguity** — continuous delivery vs continuous deployment. Cheap, and the §3 🪝 Snag says the distinction matters exactly when a human approval gate is in play, which is a testable scenario.

## Items checked and clear

- **Question budget**: exact in all four categories; no drift between outline and draft.
- **Why-wrong completeness on multiple-choice**: all five MC items (Q2, Q4, Q9, Q11, Q13) explain every wrong option. Zero FAILs under skill Part 11.
- **Soundings structure**: 8 questions (correct for a content chapter), answers in `<details>`, all three rubric branches present, 0–2 branch names sections rather than chapters.
- **Checkpoint structure**: 3 checkpoints, each ≥5 questions, each with a scoring rubric that names a specific section for low scorers (:378, :760, :948).
- **Retrieval tagging**: all four tags accurate; none is a chapter question wearing a retrieval label.
- **Barred material**: no question touches Knative/serverless/service mesh as a subject, `kubectl debug`, Helm chart anatomy, the graduated-project roster, PodDisruptionBudget, or A/B testing. The outline's bar list is respected throughout, including A/B, which §2 explicitly declines to teach (:319–329) and which appears in no stem, key, or distractor.
- **No question requires a command the chapter never taught.** `kb_tags.commands` is empty; the only CLI strings in questions are `kubectl apply`, `kubectl scale`, and `kubectl patch`, all from earlier chapters.

## Open-response caveat (WARN, not FAIL)

**41 of 45 questions are open-response.** Only Practice Q2, Q4, Q9, Q11, and Q13 offer options; no Soundings or Taking Your Bearings item does. Skill Part 11 specifies trap answers at "all self-assessment checkpoints," and by the letter of that the three checkpoints carry none.

I am **not** recording this as a FAIL, for two reasons. First, the draft substitutes the functional equivalent in most keys — an explicitly named anticipated wrong answer with its correction (*"Why not 'factor IX, disposability'?"*, *"Common wrong answer:"*, *"Why '11 and 10' is wrong"*, *"Why 'the sync failed' is wrong"*, *"Why 'just a ServiceAccount' is wrong"*). Second, the outline chose this shape deliberately for a chapter whose material is architectural rather than factual, and open-response is the better instrument for "explain why push-based CD is not GitOps."

Where it does thin out is **TYB 3**, which carries anticipated-wrong-answer treatment on roughly one of five items (Q2's *"the part readers miss"*). Q1, Q3, Q4, and Q5 give correct answers with supporting quotation and no account of how a reader goes wrong. Tally across all checkpoints:

| Checkpoint | Items | With named wrong-answer treatment |
|---|---|---|
| ☆ TYB 1 | 6 | 3 (Q1, Q3, Q4) |
| ☆ TYB 2 | 5 | 3 (Q1, Q2, Q4) |
| ☆ TYB 3 | 5 | 1–2 (Q2 partial) |
| Practice | 21 | 15 |

**Recommendation:** add one named-misconception clause to TYB 3 Q1, Q3, and Q5. The misconceptions are already available and unused — for Q1, that waves are absolute positions rather than relative ordering; for Q3, that "composable" means Flux is less capable; for Q5, the count-the-loops error the outline's ⛑ convention guardrail warns about at §7. No structural change, three sentences.
```

---

**Note on file output:** I could not write `diagnostics/question-quality.md` — the Write tool call was denied. Per `CLAUDE.md`, `Write` is deliberately removed from the executor's `--allowed-tools` so stage output flows through stdout for the orchestrator to capture atomically, so the document above is the stage output. If you want it on disk manually: `C:\dev\lodestar\Book-KCNA\.pipeline-state\ch-15\diagnostics\question-quality.md`.

**Headline results:** budget is exact (45/45), retrieval lands at exactly 25.0%, and the Soundings spoiler check is clean — including the Q7 item the outline flagged as at-risk, which holds because its answer says *nothing announces this*, the opposite of Fixed Point 4's claim.

Two FAILs, both fixable without touching the budget:

1. **Fixed Point 3 is never tested.** "A delivery agent is a controller; only the desired-state store moved" is the chapter's Fixed Point, its Zenith, its subtitle, and Exam Alert topic #3 — and no question asks the reader to produce it. §7 correctly has no checkpoint, so the burden fell on the 21 Practice Questions and none picked it up.
2. **TYB 2 Q2 contradicts itself and Fixed Point 4.** The stem demands "only one of which involves anything going wrong"; the key labels *"a new commit that has not been applied yet"* as the failure — but Fixed Point 4 at line 602 lists that exact case alongside the manual edit as a non-failure. Fix the stem, not the key.

These two collide usefully: Practice Q8 is answer-identical to TYB 2 Q1 (both return "1 and 2 satisfied, 3 and 4 failed"), so repurposing Q8 closes the FP3 gap for free. Practice Q6 is likewise a reworded TYB 1 Q6 with the same four items.

On distractors specifically — only 5 of 45 questions are multiple-choice, and all five explain every wrong option, so there are zero why-wrong FAILs. Q4 is the best-built item in the chapter (each distractor pairs a wrong strategy with a *correct* cost). The weak ones are Q9's option A ("cannot be automated" — the key itself calls it obviously false) and Q13's "all of the above" format, which lets a reader infer D from the two options the Fixed Point states verbatim, without ever evaluating the one option that tests the discrimination.
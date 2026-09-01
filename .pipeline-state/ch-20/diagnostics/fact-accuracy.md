# Fact-Accuracy Audit — Chapter 20

**Mode detected: STANDARD.** The draft carries nine `[source: ...]` tags and the cached-source block is populated (10 snapshots). Untagged factual claims are therefore FAIL, not advisory.

> Line numbers are approximate (±15). The draft was supplied to this stage inline rather than as a file, so every finding is anchored by quoted text and by its section heading as well as by an estimated line in `draft-v1.md`.

## Summary

- Total factual claims inspected: **84** — 24 discrete external-fact assertions in the instructional and rubric prose, plus 60 technical assertions (one per exam item / walkthrough pair)
- Tagged claims verified: **15** (carried by 9 `[source:]` tags; all 9 resolve to snapshots present in the corpus, and all 9 verify)
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0**
- **Untagged factual claims (FAIL): 6 discrete**, plus 56 exam-item technical assertions carried without tags by design — see the structural note heading that section
- **Contradicted claims (FAIL): 2**
- Minor discrepancies (WARN): **9**

No technical error was found in the substance of any of the 60 items or their distractor refutations. Both FAILs in the contradicted category are about how the instrument is *assembled*, not about what it asserts.

---

## FAIL — Untagged factual claims

**Structural note, read before the individual entries.** Fifty-six of the sixty exam items assert Kubernetes or CNCF product behaviour (QoS class derivation, `NoExecute` semantics, `ReadWriteOnce` node scoping, Prometheus's pull model, and so on) with no `[source:]` tag. Each walkthrough instead carries a cross-bearing to the owning section — `Ch 5 §8`, `Ch 7 §4`, `Ch 11 §4`, `Ch 18 §4` — which is a deliberate delegation of provenance to a chapter that was itself fact-audited. I am not raising 56 separate FAILs on that pattern; a mock exam that re-cited every upstream snapshot inline would be unreadable, and the design is defensible. But it is only defensible if the delegation actually holds, so:

**Blanket fix for the 56:** the revision stage must confirm that each cross-bearing target exists and that the owning chapter's own fact-accuracy diagnostic cleared the specific claim being tested. Where a cross-bearing points at a section that no longer exists or never owned the claim, that item drops out of the delegation and needs its own tag. This is a mechanical check against `section-skeleton.md`, and it is stage 13's normal job — flagging it here so it is not assumed done.

Four of those 56 assert externally-defined frameworks by name, count, or ordering, which is a stronger claim than product behaviour and which no chapter cross-bearing can discharge without a snapshot behind it. Those four are listed individually below, along with two untagged claims in the instructional prose.

### Line ~13 (Instructions, Dead Reckoning): "Neither number appears on the KCNA product page."

**Why it's a factual claim:** it asserts what a specific vendor page does and does not publish — an authority-scoped negative, which is precisely the class of claim the corpus twice records the research getting wrong.

**Fix:** trivial. The support is already in the corpus and unused. Tag it `[source: provenance-kcna-60-questions-2026-08-31]`, whose "Phrasings" section prescribes almost this exact sentence as CORRECT: *"The Linux Foundation publishes both figures in its candidate handbook, for multiple-choice exams as a class; neither appears on the KCNA exam page itself."* The draft's wording is already conformant; it just needs the tag.

### Line ~1360 (What to do next): "it is also the domain candidates most reliably under-study"

**Why it's a factual claim:** it is an empirical assertion about the study behaviour of a candidate population. No snapshot in this corpus — and no snapshot the manifest names — reports candidate study patterns, pass rates by domain, or anything from which this could be drawn.

**Fix:** no source exists to add. Either recast it as the book's own judgment rather than a fact about candidates (*"and it is the domain this book leaves for last, which is its own kind of risk"*), or open a research gap in the research-manifest for domain-level candidate performance data — noting in advance that the LF publishes none, per `lf-exam-scoring-and-notification-2026-08-31` ("LF does not report performance on individual items"). Recasting is the realistic option.

### Line ~800 (Answer 17, correct-answer paragraph): "`--previous` retrieves the logs of the previous terminated container instance, which is the run that actually failed."

**Why it's a factual claim:** it states the behaviour of a specific `kubectl` flag. Note that the sibling claim two bullets down — `kubectl events --for pod/<pod>` — *is* tagged, so the tagging here is inconsistent within a single walkthrough.

**Fix:** tag `[source: k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31]`, whose `concepts_covered` lists `kubectl-logs-previous` explicitly. **Caveat for the revision stage:** the body of that snapshot as delivered to this stage ends at the heading `## Interacting with running Pods` with no command lines beneath it. I could not verify the flag's documented wording against it. Confirm the snapshot on disk actually carries the `kubectl logs --previous` line before tagging; if the file is genuinely truncated, that is a corpus defect to raise, not something to paper over with a tag.

### Line ~854 (Answer 18, refutation of C): "continuous reconciliation is one of the four OpenGitOps principles"

**Why it's a factual claim:** it names an external standards body's document and asserts a specific cardinality (*four*). Cardinality claims are exactly what drifts when an external framework is revised.

**Fix:** no OpenGitOps snapshot is in this corpus. Open a research gap for the OpenGitOps Principles (opengitops.dev). Until it is cached, either soften to *"continuous reconciliation is one of the OpenGitOps principles"* — dropping the count removes the fragile part — or drop the attribution and make the point in the book's own voice.

### Line ~890 (Answer 21): "The ordered progression from Sandbox through Incubating to Graduated"

**Why it's a factual claim:** it asserts a CNCF governance structure by name and ordering. The irony is sharp: this is the item whose whole teaching point is that point-in-time CNCF data has an expiry date, and its own durable-fact claim is uncited.

**Fix:** `cncf-curriculum-kcna-readme-2026-08-31` covers domain weights only and does not reach maturity levels. Open a research gap for the CNCF Graduation Criteria / project maturity levels document. This one is worth actually caching rather than softening — the item's rhetorical force depends on the levels being right.

### Line ~178 (Item 13) and ~740 (Answer 13): "Cloud, Cluster, Container, Code, from outside in."

**Why it's a factual claim:** it asserts the composition and ordering of a named external model (the 4C's of Cloud Native Security, from the Kubernetes documentation). The item is built entirely on the ordering being correct — a reader who learns it backwards fails the real question.

**Fix:** open a research gap for the Kubernetes docs page on the 4C's of Cloud Native Security and tag both the stem's premise and the walkthrough. The cross-bearing to `Ch 12 §1 — four layers and four phases` suggests Ch 12 owns and sourced this; if Ch 12's fact-accuracy diagnostic cleared it against a cached snapshot, name that snapshot here instead of opening a new gap.

---

## FAIL — Contradicted claims

### Line ~19 (What this instrument is, and is not): "It is sized to the published count and weighted to the published blueprint: 44% Kubernetes Fundamentals, 28% Container Orchestration, 16% Cloud Native Application Delivery, 12% Cloud Native Architecture ... Twenty-six questions, seventeen, ten, and seven."

**Tag:** `[source: cncf-curriculum-kcna-readme-2026-08-31]`

**Snapshot says:** "Kubernetes Fundamentals: 44% / Container Orchestration: 28% / Cloud Native Application Delivery: 16% / Cloud Native Architecture: 12%"

**Draft says:** the instrument is *weighted to* that blueprint, at 26 / 17 / 10 / 7 items.

**The contradiction:** the weights themselves are quoted correctly, and 26/17/10/7 is the correct rounding of 26.4 / 16.8 / 9.6 / 7.2. But the instrument as actually built does not match. Tallying the domain tag on every walkthrough — which is the only per-item domain assignment in the chapter — gives:

| Domain | Items, by walkthrough tag | Count | Claimed |
|---|---|---|---|
| D1 | 1,2,3,4,5,6,11,16,22,23,24,25,29,31,32,33,38,39,41,42*,43,45,46,51,52,60 | 26 | 26 ✓ |
| D2 | 7,8,12,13,14,15,17,19,20,26,27,34,36,37,48,50,53,56 | **18** | 17 ✗ |
| D3 | 10,18,28,35,47,54,57 | **7** | 10 ✗ |
| D4 | 9,21,30,40,44,49,55,58,59 | **9** | 7 ✗ |
| | | 60 ✓ | 60 |

(\*Item 42 has no walkthrough; counted as D1 per the AUTHOR-REVIEW comment's stated intent.)

Every item is assigned exactly once and the total is 60, so this is not a bookkeeping slip in my count — the instrument is genuinely built to 26/18/7/9. Cloud Native Application Delivery is under-represented by three items and Cloud Native Architecture over-represented by two. The sourced sentence "weighted to the published blueprint" is therefore false as the chapter stands, and the per-domain score sheet — which the chapter argues at length is the single thing this exam exists to produce — reports D3 out of a stated 10 while only 7 items feed it.

**Recommended fix:** this is a content change, not a list edit. The delta needed is **D2 −1, D3 +3, D4 −2**. Two routes: re-tag five items whose domain assignment is genuinely arguable (items 40, 55, and 57 are the obvious candidates — Prometheus, Knative scale-to-zero, and `kubectl debug` all sit near a domain boundary), or replace two D4 items and one D2 item with new Cloud Native Application Delivery items. Re-tagging is cheaper but must be defensible against the curriculum's own competency lists, not chosen to make the arithmetic work.

**Note for the revision stage:** the existing AUTHOR-REVIEW comment at ~line 1312 instructs *"Reconcile against the per-question domain tags in the answer key, which are authoritative."* Following that instruction as written cannot produce 26/17/10/7 — the per-question tags are what produce 26/18/7/9. That comment's premise is wrong and should not be actioned literally.

### Line ~47 (The answers): "Every question there carries the correct answer, an explanation of why each of the three wrong options is wrong, the domain it belongs to, and a pointer back to the section that taught it."

**Tag:** none (claim about the chapter's own contents)

**Draft says:** *every* question.

**The contradiction:** item 42 (`imagePullPolicy`) appears in the exam block at ~line 436 but has no walkthrough. The answer key runs 41 → 43. A reader who follows the chapter's own instructions cannot score item 42 or assign it a domain, and item 42 is one of the 26 the D1 row counts on.

**Recommended fix:** restore the item 42 walkthrough. The AUTHOR-REVIEW comment at ~line 1075 already specifies the content, and I confirm its substance is technically correct: the default `imagePullPolicy` is `IfNotPresent` unless the tag is `:latest` or omitted, in which case `Always`; `Never` uses only what is already on the node and builds nothing; `Always` re-checks the registry and does not require a digest reference. Delete the stray `**43 continues on the next item.**` line at ~line 454 in the same pass.

---

## WARN — Minor discrepancies

**1. Answer-key skew defeats the instrument's stated purpose (not minor — flagged here only because it contradicts no snapshot).** Fifty-six of the sixty correct answers are **B**. The four exceptions are items 13 (D), 16 (C), 46 (A), and 53 (C). A reader who answers B to every question scores 56/60 and lands in the top band, "Comfortable margin above the published standard." That directly falsifies the chapter's central argument at ~line 23 — "What it predicts is *readiness*" — and the score sheet's diagnostic value, which the chapter grounds in `lf-exam-scoring-and-notification-2026-08-31`. The distribution should be roughly even across A–D. This is a substantial revision, and it is worth doing before anything else on this list, because re-lettering interacts with the item 42 restoration and the domain re-tagging.

**2. Line ~55 onward — the item format implies two unsourced facts about the real exam.** Every item presents four options with one correct answer. `lf-examui-multiple-choice-2026-08-31` records under "Question format — NOT PRESENT ON PAGE": no statement about "single-best-answer versus multi-select, 'choose two', the number of answer options per item, partial credit, or unscored/pretest items," and cautions that the handbook's singular "update your answer" "is NOT dispositive and must not be cited as proof of a single-best-answer format." The chapter never asserts either fact, which is correct discipline — but a reader will infer both from the instrument's shape. Recommend one hedging clause in "What this instrument is, and is not": the option count and answer format here are this book's construction, not published figures.

**3. Line ~41: "It tells you whether you passed."** `lf-exam-scoring-and-notification-2026-08-31` establishes that a "score report" is emailed within 24 hours and posted to the Portal, and that per-item performance is withheld. It does not enumerate what the report *does* contain. The claim is almost certainly right and the snapshot's own analysis section asserts it ("The real exam returns a pass/fail result and a score"), but that is the snapshot author's characterisation, not LF verbatim. Low risk; note it so nobody later hardens it into a quoted claim.

**4. Lines ~41 and ~1350 — domain-level inference from an item-level statement.** The draft writes "It does not tell you which domain you were weak in" and "gives you a number and not a breakdown," both against `lf-exam-scoring-and-notification-2026-08-31`. The LF's verbatim sentence covers *individual items* — "LF does not report performance on individual items and will not honor requests for more detailed information." Domain-level silence follows from the second clause but is one inferential step past the quote. The snapshot's analysis makes the same step explicitly, so this is supported; flagging it so the phrasing is not tightened into "the Linux Foundation states it does not report per-domain scores," which would be a misquote.

**5. Line ~1360: "D4 is only 12% of the exam."** Untagged restatement of a figure tagged at ~line 19 against `cncf-curriculum-kcna-readme-2026-08-31`. Verified, but 1,300 lines from its tag. Carry the tag or accept the distance deliberately.

**6. Line ~1320: "On a 60-item instrument that is **45 correct**."** Arithmetically exact (75% × 60). The conversion of a percentage into a raw correct-count silently assumes every item is scored, equally weighted, and unpenalised. `lf-exam-scoring-and-notification-2026-08-31` records under "Partial credit, pretest items, and penalties — NOT PRESENT ON PAGE" that none of that is published, and warns "DO NOT ASSERT 'there is no penalty for a wrong answer.'" The draft handles this well — the very next sentence says "It is not a promise about how this instrument maps onto the real one." Keep that sentence adjacent to the 45; do not let a revision separate them.

**7. Line ~127 (Item 9 stem): "the CNCF's stated purpose for the KCNA-level tier of certification."** The snapshot describes the KCNA certification specifically: "provides a beginner friendly option to learn about the Kubernetes community and vast cloud native ecosystem of projects." It says nothing about a "tier," nor about other credentials sharing that purpose. Recommend "for the KCNA" over "for the KCNA-level tier."

**8. Line ~47: "an explanation of why each of the three wrong options is wrong."** Several walkthroughs group their refutations rather than treating each separately — 13 ("B and C are wrong"), 16 ("A, B, and D are wrong"), 21 and 50 ("A, C, and D are wrong"), 53 ("A, B, and D are all plausible causes"). The grouping is good writing in each case and should stay; the promise should soften to "an explanation of why the wrong options are wrong."

**9. Line ~1300 — the rubric's typed item lists have defects beyond the weighting FAIL.** Independently of finding C1: items **31** (`NoExecute`, tagged D1.3) and **50** (SBOM, tagged D2.2) appear in no row at all, and items 9, 12, and 48 appear in two rows each (already starred in the draft). Fixing the weighting will not fix these; they need a separate mechanical pass. Recommend generating the four rows from the walkthrough tags programmatically after the domain re-tagging settles, rather than by hand.

---

## PASS — Verified claims

All nine `[source:]` tags resolve to snapshots present in this corpus, and all fifteen assertions they carry verify against snapshot text.

| Claim (abbreviated) | Line | Tag | Verification |
|---|---|---|---|
| MC exam "consists of 60* multiple-choice questions" | ~13 | `lf-mc-exam-important-instructions-2026-08-31` | Verbatim match |
| Candidates "have 90* minutes to complete" | ~13 | same | Verbatim match |
| Asterisks footnote CNPA at 85 questions / 120 minutes | ~13 | same | Matches both footnotes; correctly characterised as a per-exam carve-out, not a hedge |
| KCNA in MC column beside KCSA and LFCA; CKA and CKAD performance-based | ~13 | `lf-exam-user-interface-exam-codes-2026-08-31` | Matches the table exactly, including first-position ordering of KCNA KCSA LFCA |
| Domain weights 44 / 28 / 16 / 12 | ~19 | `cncf-curriculum-kcna-readme-2026-08-31` | Verbatim match (see C1 — the weights are right; the instrument's build is not) |
| Previous / Next navigation between items | ~33 | `lf-examui-multiple-choice-2026-08-31` | Matches; correctly paraphrased rather than quoted, per the snapshot's instruction not to reproduce its typographic irregularities |
| Flag an item for later review | ~33 | same | Match |
| Flagged items highlighted on a Review Screen | ~33 | same | Match |
| Can return to a flagged item and change the answer | ~33 | same | Match |
| Prompted to review after final item; Finish Exam sits on the Review Screen | ~33 | same | Match |
| Pause Exam exists and does not stop the timer | ~33 | same | Match ("Requesting a break via the Pause Exam function will not stop the timer") |
| Score report within 24 hours, by email and on the Portal | ~41 | `lf-exam-scoring-and-notification-2026-08-31` | Match; tag sits two sentences downstream but within the same paragraph |
| LF "does not report performance on individual items and will not honor requests for more detailed information" | ~41 | same | Verbatim match |
| CNCF describes KCNA as "a beginner friendly option to learn about the Kubernetes community and vast cloud native ecosystem of projects" | ~890 (Answer 9) | `cncf-curriculum-kcna-readme-2026-08-31` | Verbatim match |
| `kubectl events --for pod/<pod>` filters events to a resource | ~800 (Answer 17) | `k8s-docs-kubectl-events-2026-08-31` | Match (`--for string` — "Filter events to only those pertaining to the specified resource") |

### Hazards explicitly avoided — do not reintroduce during revision

The corpus contains two correction records and several named FALSE phrasings. This chapter clears all of them, which is not accidental and should survive revision:

- **The 60-question provenance.** The draft's framing — "publishes both of the numbers ... in its candidate handbook, for multiple-choice exams as a class ... Neither number appears on the KCNA product page" — is almost word-for-word the CORRECT phrasing prescribed by `provenance-kcna-60-questions-2026-08-31`. The superseded 2026-08-23 claim that the count is "NOT FOUND in any authoritative source" appears nowhere.
- **The exam-interface provenance.** `provenance-kcna-exam-interface-2026-08-31` records that `ch-19/draft-v2.md` line 541 asserts "The Linux Foundation does not publish how its multiple-choice exam console behaves," and that the sentence must be corrected before Ch 19 ships. **Chapter 20 does not carry that error** — it states the opposite, correctly, at ~line 33. Ch 19's defect is unfixed and remains outstanding; a revision pass that harmonises the two chapters must move Ch 19 to Ch 20's framing, never the reverse.
- **No penalty claim.** The draft nowhere asserts "there is no penalty for a wrong answer," which `lf-exam-scoring-and-notification-2026-08-31` forbids as unsourced. See WARN 6 for the one place this could erode.
- **`kubectl events` claims stay inside the source.** The draft says only that `--for` filters to a resource. It does not claim the command sorts by timestamp by default or that it replaces or deprecates `kubectl get events` — both named as unsourced and unbuildable in `k8s-docs-kubectl-events-2026-08-31`.

### Technical substance

I checked all 60 items and their distractor refutations for technical error and found none. Several are notably careful: item 33 says a kubelet may run behind the API server "by a bounded number of minor versions" without naming the number, which avoids a real version-drift hazard; answer 23 concedes in a parenthetical that `kubectl drain` cordons for you, so the item tests the conceptual order honestly rather than a falsehood; answer 26 names `ReadWriteOncePod` as the reason `ReadWriteOnce` cannot mean one Pod. Answer 40's Pushgateway caveat and answer 11's `volumeClaimTemplate` correction are both accurate. The tagging gap described at the head of the FAIL section is a provenance problem, not a correctness one.
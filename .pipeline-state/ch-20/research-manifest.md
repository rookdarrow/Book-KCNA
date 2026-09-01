Research complete. Four findings, one of which closes a gap the pipeline had recorded as its highest-value missing snapshot.

---

# Research Manifest — KCNA Chapter 20

**Stage 2 · Full Mock Exam · researched 2026-08-31**

Ch 20 is a retrieval-only chapter: per the ratified citation-discipline ruling it introduces no new facts, and its curriculum surface is already covered by the 303 snapshots cached for Ch 2–18. I verified that coverage rather than duplicating it (domain weights 44/28/16/12 confirmed against `cncf-curriculum-kcna-readme-2026-08-31.md`; the `kb_tags` command list checked snapshot-by-snapshot). Research therefore concentrated on the chapter's **apparatus** — the Instructions and Scoring Rubric blocks — plus the one standing command gap.

**The headline: Open Question 2 is closed.** The outline asked for "one targeted fetch" of a Linux Foundation or PSI page documenting the multiple-choice interface. It exists, it is official, and Ch 19's six-page sweep never reached it. Question navigation, flagging, the review screen and answer-changing are all published.

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `lf-examui-multiple-choice-2026-08-31.md` | Linux Foundation (Candidate Handbook, PSI BRIDGE) | — | exam-pacing, kcna-exam-format, exam-navigation |
| `lf-exam-user-interface-exam-codes-2026-08-31.md` | Linux Foundation (Candidate Handbook, PSI BRIDGE) | — | kcna-exam-format, published-vs-commonly-reported |
| `lf-exam-scoring-and-notification-2026-08-31.md` | Linux Foundation (Candidate Handbook, PSI BRIDGE) | — | per-domain-score-sheet, mock-exam-calibration |
| `k8s-docs-kubectl-events-2026-08-31.md` | Kubernetes (kubectl command reference) | D2.3 | kubectl-events, kubectl-get |
| `provenance-kcna-exam-interface-2026-08-31.md` | Correction record | — | published-vs-commonly-reported, exam-navigation |

---

### A1 · `lf-examui-multiple-choice-2026-08-31.md` (new)

````markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface/examui-multiple-choice-exams"
fetched_at: "2026-08-31T21:15:00-0400"
authority: "The Linux Foundation — 'ExamUI: Multiple Choice Exams', Candidate Handbook (PSI BRIDGE Proctoring platform)"
objectives_covered: []
concepts_covered: ["kcna-exam-format", "exam-pacing", "exam-navigation"]
closes_gap: "Ch 19 research manifest gap G1 (question navigation, flagging, skipping). CLOSED. Also discharges the AUTHOR-REVIEW comment at ch-19/draft-v2.md line 551."
---

# ExamUI: Multiple Choice Exams — Linux Foundation Candidate Handbook (PSI BRIDGE)

> THIS SNAPSHOT CLOSES THE HIGHEST-VALUE OPEN GAP IN THE BOOK'S EXAM-MECHANICS
> RESEARCH. Ch 19's manifest recorded question navigation as "confirmed absent on
> targeted fetch across six official pages" and recommended drafting around the
> absence. This page was NOT among those six. It publishes the behaviour directly.
>
> The parent page (lf-exam-user-interface-exam-codes-2026-08-31.md) routes the
> exam code KCNA to THIS page by name.

## Guidelines and Tips for using the Multiple Choice ExamUI — verbatim, complete

The page's entire body list, reproduced exactly:

* "To navigate between items, click the Previous or Next button"
* "The candidate can \"Flag\" an item for later review. This items will be highlighted on the \"Review Screen\" and they can return to the item to update your answer."
* "When the candidate reaches the final multiple choice item, they will be prompted to click on \"Review Exam\"  the Review screen contains the \"Finish Exam\" button."
* "The timer  indicates the testing time remaining."
  * "NOTE: Requesting a break via the Pause Exam function will not stop the timer."
  * "NOTE: The timer will not pause, and there is no way to ADD time back to the timer in the event of a system disconnect during your exam."
* "The Exam will end when the timer or expires, or when the candidate clicks \"Finish Exam\"."

(Typographic irregularities — "This items", the doubled spaces, the mid-sentence
person shift from "they" to "your", and the malformed "when the timer or expires"
— are in the source. Reproduced verbatim. Do not quote these sentences to the
reader unedited; paraphrase the mechanic instead.)

## Figures on the page

Two screenshots, captioned:

- "Multiple Choice ExamUI"
- "Multiple Choice Review Screen"

Image bodies were not retrievable as text. Any claim about on-screen layout,
button placement, or whether a question counter is displayed would rest on the
images and is therefore NOT sourced by this snapshot.

## What is established, and usable as fact

1. Navigation is bidirectional. Previous and Next buttons exist.
2. Items can be flagged for later review.
3. Flagged items are highlighted on a Review Screen.
4. A candidate can return to a flagged item AND CHANGE THE ANSWER.
5. A Review Exam prompt appears after the final item; the Review screen holds
   the Finish Exam button.
6. The exam ends on timer expiry or on Finish Exam.
7. A Pause Exam function exists, and using it does not stop the timer.

Point 7 is new and independent of the navigation finding: it means a break is
available but is purchased with exam time.

## Scope

The page governs the multiple-choice ExamUI as a class. KCNA is assigned to that
class by exam code on the parent page. Same class-inheritance situation as the
60-question and 75% figures, and the same phrasing discipline applies:

- CORRECT: "The Linux Foundation publishes the multiple-choice exam interface's
  behaviour in its candidate handbook, for the interface KCNA uses."
- FALSE, do not write: "The Linux Foundation does not publish how its
  multiple-choice exam console behaves." (This sentence is currently in
  ch-19/draft-v2.md line 541 and must be corrected before Ch 19 ships.)
- FALSE, do not write: "The KCNA exam page describes the exam interface."

## Question format — NOT PRESENT ON PAGE

No statement about single-best-answer versus multi-select, "choose two", the
number of answer options per item, partial credit, or unscored/pretest items.
Confirmed absent on verbatim markdown fetch 2026-08-31.

The phrase "update your answer" is SINGULAR. That is suggestive of one selection
per item but is NOT dispositive and must not be cited as proof of a
single-best-answer format.
````

### A2 · `lf-exam-user-interface-exam-codes-2026-08-31.md` (new)

````markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface"
fetched_at: "2026-08-31T21:15:00-0400"
authority: "The Linux Foundation — 'Exam User Interface: Configuration & Features', Candidate Handbook (PSI BRIDGE Proctoring platform)"
objectives_covered: []
concepts_covered: ["kcna-exam-format", "published-vs-commonly-reported"]
---

# Exam User Interface: Configuration & Features — LF Candidate Handbook

Independent value beyond routing: this is an official Linux Foundation page that
NAMES THE EXAM CODE KCNA and assigns it to the multiple-choice class. Prior to
this snapshot the book's class-inheritance argument for the 60-question and 75%
figures rested on two weaker anchors — the KCNA exam page's self-description
("an online, proctored, multiple-choice exam") and the MC FAQ's CARE section.
This is a direct, tabular, first-party assignment.

## Body — verbatim

"Please review the list of exam codes below, and click on the \"ExamUI Information\" to learn about the exam environment that will be presented when your exam launches:"

| Exam Code | Exam UI Information |
|---|---|
| CKA     CKAD   CKS<br>LFCS   ICA   CNPE | ExamUI for Performance Based Exams |
| KCNA  KCSA  LFCA <br>PCA  RVFA  FCFP <br>FSOSD  CGOA  CCA <br>CAPA  CNPA  CODE <br>BCP  KCA  OTCA  CBA | ExamUI for Multiple Choice Exams |

Link targets:

- Performance Based: https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface/examui-performance-based-exams
- Multiple Choice: https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface/examui-multiple-choice-exams

## What this establishes

KCNA appears in the multiple-choice column, first position. CKA appears in the
performance-based column. The two credentials the book discusses side by side are
separated by the Linux Foundation itself, by exam code, on interface grounds.

Note also that CNPA — the carve-out named in both asterisk footnotes on
important-instructions-mc (85 questions, 120 minutes) — sits in the multiple-choice
column. This confirms the asterisks are per-exam carve-outs WITHIN the
multiple-choice class, not hedges on the class-wide figures.

## Question navigation and format — NOT PRESENT ON PAGE

This page routes only. The behaviour is on the child page; see
lf-examui-multiple-choice-2026-08-31.md.
````

### A3 · `lf-exam-scoring-and-notification-2026-08-31.md` (new)

````markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-scoring-and-notification"
fetched_at: "2026-08-31T21:15:00-0400"
authority: "The Linux Foundation — 'Exam Scoring and Notification', Candidate Handbook (PSI BRIDGE Proctoring platform)"
objectives_covered: []
concepts_covered: ["per-domain-score-sheet", "mock-exam-calibration", "domain-weighted-assessment"]
---

# Exam Scoring and Notification — LF Candidate Handbook (PSI BRIDGE)

## Score reporting — verbatim

"Upon completion, exams are scored automatically and barring any exceptions or technical difficulties, a score report will be sent to the candidate via email within 24 hours from the time that the exam was completed.  Results will also be made available on the Portal."

## No item-level reporting — verbatim

"LF does not report performance on individual items and will not honor requests for more detailed information"

DIRECTLY LOAD-BEARING FOR THE CH 20 SCORING RUBRIC. The real exam returns a
pass/fail result and a score. It does NOT return a per-domain breakdown and does
NOT return item-level performance. The mock's per-domain score sheet is therefore
not a convenience that duplicates something the real exam provides — it is the
ONLY place in the candidate's preparation where a domain-level diagnostic is
available at all. This is a sourced justification for the block's existence.

## Performance-based carve-out — verbatim

"For performance based exams (non multiple choice exams) there may be more than one way to perform a task on an Exam and unless otherwise specified, the candidate can pick any available path to perform the task as long as it produces the correct result."

Note the parenthetical: the LF's own gloss for "performance based" is "non
multiple choice". The multiple-path allowance is explicitly scoped AWAY from
multiple-choice exams, and so away from KCNA.

## Score review, forensics and invalidation — verbatim

"The Linux Foundation (LF) and/or the Exam Proctoring Partner will review your exam record for scoring accuracy, for evidence of possible misconduct, and for response patterns that may suggest that your scores do not represent a valid measure of your knowledge or competence as sampled by the examination (measurement error)."

"LF will use statistical analyses of exam data (\"Data Forensics\") to identify patterns indicative of test fraud, including cheating and piracy."

"LF reserves the right to invalidate your exam score and certification result if review of your exam record reveals scoring inaccuracies (attributable to LF or the Exam Proctoring Partner) or response patterns indicative of possible misconduct or measurement error. If LF determines that an Exam score is invalid due to issues that are beyond the control of the candidate, the candidate will be advised of options to retake the Exam at no charge."

## Partial credit, pretest items, and penalties — NOT PRESENT ON PAGE

No statement about partial credit, unscored/experimental/pretest items, or any
penalty or negative marking for incorrect answers. Confirmed absent on verbatim
markdown fetch 2026-08-31.

DO NOT ASSERT "there is no penalty for a wrong answer." It is not sourced here or
on any other cached page. See the Ch 20 manifest, Gaps G4.
````

### A4 · `k8s-docs-kubectl-events-2026-08-31.md` (new)

`````markdown
---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_events/"
fetched_at: "2026-08-31T21:15:00-0400"
authority: "Kubernetes — official kubectl command reference"
objectives_covered: ["2.3"]
concepts_covered: ["kubectl-events", "kubectl-get", "kubectl-describe"]
closes_gap: "B1 gap G1 residual. k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31.md records 'kubectl events is NOT covered'. Now covered."
---

# kubectl events — Kubernetes command reference

## Synopsis — verbatim

"List events"

"Display events."

"Prints a table of the most important information about events. You can request events for a namespace, for all namespace, or filtered to only those pertaining to a specified resource."

```
kubectl events [(-o|--output=)json|yaml|kyaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file] [--for TYPE/NAME] [--watch] [--types=Normal,Warning]
```

## Examples — verbatim

```bash
# List recent events in the default namespace
kubectl events

# List recent events in all namespaces
kubectl events --all-namespaces

# List recent events for the specified pod, then wait for more events and list them as they arrive
kubectl events --for pod/web-pod-13je7 --watch

# List recent events in YAML format
kubectl events -oyaml

# List recent only events of type 'Warning' or 'Normal'
kubectl events --types=Warning,Normal
```

## Flags — verbatim descriptions

- `-A, --all-namespaces` — "If present, list the requested object(s) across all namespaces. Namespace in current context is ignored even if specified with --namespace."
- `--allow-missing-template-keys` (default true) — "If true, ignore any errors in templates when a field or map key is missing in the template. Only applies to golang and jsonpath output formats."
- `--chunk-size int` (default 500) — "Return large lists in chunks rather than all at once. Pass 0 to disable."
- `--for string` — "Filter events to only those pertaining to the specified resource."
- `-h, --help` — "help for events"
- `--no-headers` — "When using the default output format, don't print headers."
- `-o, --output string` — "Output format. One of: (json, yaml, kyaml, name, go-template, go-template-file, template, templatefile, jsonpath, jsonpath-as-json, jsonpath-file)."
- `--show-managed-fields` — "If true, keep the managedFields when printing objects in JSON or YAML format."
- `--template string` — "Template string or path to template file to use when -o=go-template, -o=go-template-file."
- `--types strings` — "Output only events of given types."
- `-w, --watch` — "After listing the requested events, watch for more events."

## Relationship to `kubectl get events` — NOT STATED ON PAGE

The reference page does not state how `kubectl events` relates to or differs from
`kubectl get events`. Confirmed absent 2026-08-31.

USABLE FOR A STEM: the `--for TYPE/NAME` filter and the `--types` filter are
documented and exact. A distractor turning on the CLAIM that `kubectl events`
sorts by timestamp by default, or that it replaces/deprecates `kubectl get
events`, is NOT sourced and must not be built.
`````

### A5 · `provenance-kcna-exam-interface-2026-08-31.md` (new)

````markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface/examui-multiple-choice-exams"
fetched_at: "2026-08-31T21:20:00-0400"
authority: "Correction record. Primary evidence is the Linux Foundation Candidate Handbook page cited above."
objectives_covered: []
concepts_covered: ["published-vs-commonly-reported", "exam-navigation"]
---

# CORRECTION — the multiple-choice exam interface IS documented

> AFFECTS DRAFTED TEXT. ch-19/draft-v2.md line 541 currently asserts the
> opposite. That sentence must be corrected before Ch 19 ships.

## The false claim, as currently drafted in Ch 19 §3

"The Linux Foundation does not publish how its multiple-choice exam console
behaves: whether you can skip a question, mark one for review, navigate back, or
change an answer you have already given. That silence is not an oversight in this
book's research; it is confirmed absent on four separate official pages..."

The four page-scoped negatives cited are each individually TRUE. The
generalisation drawn from them is FALSE.

## What is actually published

The Linux Foundation Candidate Handbook contains a page, "ExamUI: Multiple Choice
Exams", that documents the interface directly:

- "To navigate between items, click the Previous or Next button"
- "The candidate can \"Flag\" an item for later review. This items will be highlighted on the \"Review Screen\" and they can return to the item to update your answer."
- "When the candidate reaches the final multiple choice item, they will be prompted to click on \"Review Exam\"  the Review screen contains the \"Finish Exam\" button."

KCNA is assigned to this interface by exam code on the parent page,
"Exam User Interface: Configuration & Features".

## Current, accurate status

| Behaviour | Status | Where published |
|---|---|---|
| Navigate backward/forward | PUBLISHED | ExamUI: Multiple Choice Exams |
| Flag an item for later review | PUBLISHED | ExamUI: Multiple Choice Exams |
| Review screen highlighting flagged items | PUBLISHED | ExamUI: Multiple Choice Exams |
| Change a previously given answer | PUBLISHED | ExamUI: Multiple Choice Exams |
| Explicit "skip" control | NOT PUBLISHED | — (bidirectional nav makes skipping possible; no named skip control) |
| Question format / option count | NOT PUBLISHED | — |
| Unscored or pretest items | NOT PUBLISHED | — |
| Penalty for incorrect answers | NOT PUBLISHED | — |

## This is the SECOND instance of the same research error

The 2026-08-23 provenance file made an identical mistake with the question count:
it enumerated six checked pages, found the figure on none of them, and concluded
"NOT FOUND in any authoritative source." The figure was published on a seventh
page. See provenance-kcna-60-questions-2026-08-31.md.

The pattern: a bounded search yields page-scoped negatives, which are then
generalised into an unbounded claim about what the authority publishes. Both
times the missing page was in the same documentation tree, reachable from the
tree's own index (docs.linuxfoundation.org/tc-docs/llms.txt).

RULE GOING FORWARD: a page-scoped negative ("not present on this page") may be
recorded from a targeted fetch. An authority-scoped negative ("the authority does
not publish X") requires the documentation index to have been enumerated. Do not
promote the first into the second.

## Phrasings

- CORRECT: "The Linux Foundation documents the multiple-choice exam interface in
  its candidate handbook: you can move between questions with Previous and Next,
  flag an item for review, and return to change your answer before you finish."
- FALSE, do not write: "The Linux Foundation does not publish how its
  multiple-choice exam console behaves."
- FALSE, do not write: "Whether the console permits navigation is undocumented."
- STILL CORRECT, keep: the interface behaviour is published for multiple-choice
  exams as a class, and does not appear on the KCNA product page.
````

---

## Gaps

Flagged for the drafting stage. **Do not invent facts to fill these.**

### G1 — Question format (single-best vs multi-select) is UNPUBLISHED

No cached source states whether items are single-best-answer, whether "choose two" items appear, or whether any item is multi-select. Confirmed absent on `examui-multiple-choice-exams`, `important-instructions-mc`, `faq-mc`, `exam-scoring-and-notification`, and the three `lf-handbook2` pages.

The ExamUI page's "update your **answer**" is singular. That is weak circumstantial support for single-selection, **not** proof. The outline's plan — default to four-option single-best, and say nothing about other forms — remains the right call. Do not upgrade it to a claim about the real exam.

### G2 — Number of answer options per item is UNPUBLISHED

Nothing states four options, or any number. The mock's four-option form is an **authoring choice**, not a documented property of the KCNA exam. The Instructions block must not imply otherwise.

### G3 — Unscored / pretest / experimental items are UNPUBLISHED

The scoring page describes automatic scoring and forensic review, and says nothing about unscored items. Do not assert their presence or absence.

### G4 — Penalty for incorrect answers is UNPUBLISHED

Nothing anywhere states there is no penalty for a wrong answer. **This matters**: Ch 19's manifest floated the phrasing "answer everything since there is no penalty for a wrong answer" as pacing advice. That premise is unsourced. Ch 19's draft-v2 does not appear to have used it — keep it that way, and keep it out of Ch 20's Instructions block. Advice to answer every item can stand on the sourced 75% threshold and the sourced ability to return to flagged items, without a claim about negative marking.

### G5 — Whether check-in consumes exam time (inherited, unchanged)

Still absent, as Ch 19 recorded. Ch 20 does not depend on it.

### No curriculum gaps

All thirteen competencies are sourced by the existing 303-snapshot library. Every `kb_tags` command now resolves to at least one snapshot; `kubectl events` was the sole outstanding item and A4 closes it.

## Notes for the author

**1. Open Question 2 is closed, and it pays out on two chapters as the outline predicted.** The Instructions block can now state the navigation mechanic as fact: Previous/Next, flag for review, a review screen that highlights flagged items, and the ability to return and change an answer. The outline's planned hedge — "whether the real console permits any of that is **undocumented**, confirmed absent across four official pages" — should be **deleted**, not softened.

More importantly this discharges the standing `<!-- AUTHOR-REVIEW -->` request at `ch-19/draft-v2.md:551`, which asked for exactly this source and specified the remedy: *"this subsection collapses to two sentences and the ★ Fixed Point can name the flag control directly."* Ch 19 §3's "What the reserve is for depends on the interface" subsection (lines 539–551) can now collapse — the conditional fork at lines 545–547 is dead, and the reserve is unambiguously a genuine second pass through flagged items.

**2. Ch 19 draft-v2 line 541 currently contains a false sentence.** It asserts the Linux Foundation does not publish console behaviour. It does. This is not a Ch 20 problem, but Ch 20's Instructions block points at Ch 19 §3, so drafting Ch 20 to the corrected evidence while Ch 19 still carries the hedge would reproduce the exact contradiction the outline's Open Question 1 was raised to prevent. **Ch 19 needs a revision pass before either chapter ships.**

**3. Open Question 1: the outline's read is correct, and I verified it against the primary source rather than the summary.** I re-fetched `important-instructions-mc` in full verbatim markdown; the 60-question and 90-minute quotes match the cached snapshot exactly, and both asterisks resolve to CNPA carve-outs. A2 strengthens the case further — CNPA sits in the multiple-choice column, so the asterisks are demonstrably per-exam exceptions *within* the class, not hedges on the class-wide figures. **Draft Blocks 1 and 4 to the current evidence state and amend the B6 skeleton's Ch 20 entry**, as the outline recommends. The skeleton's 2026-08-25 constraints are stale.

**4. The Scoring Rubric block gains a sourced spine it did not have.** "LF does not report performance on individual items and will not honor requests for more detailed information" means the real exam gives the candidate a score and nothing else. The per-domain score sheet is therefore the only domain-level diagnostic the reader will ever get. That converts Block 4(a) from a convenience into the chapter's justified centrepiece, and it is quotable.

**5. One new mechanic worth a sentence in Instructions.** A Pause Exam function exists, and "Requesting a break via the Pause Exam function will not stop the timer." Breaks are available but bought with exam time — consistent with the "no way to ADD time back" rule Ch 19 §3 already sources, and a natural fit for the reproduce-the-conditions paragraph.

**6. Quote the ExamUI page's mechanics, not its prose.** The source contains "This items will be highlighted", a person shift from "they" to "your", and "when the timer or expires". Paraphrase the behaviour; do not reproduce these sentences to the reader.

**7. A process finding, offered because it has now happened twice.** Both the question-count error and the navigation error came from the same move: a bounded page sweep produces page-scoped negatives, which get generalised into a claim about what the authority publishes. Both times the missing page sat in the same documentation tree, listed in that tree's own index at `docs.linuxfoundation.org/tc-docs/llms.txt`. I've written the guardrail into A5 — page-scoped negatives may be recorded from a targeted fetch; authority-scoped negatives require the index to have been enumerated. Worth promoting into the research prompt template so later books inherit it.

I did not act on the outline's Open Questions 3, 4, or 5 — the Safe Harbor marker decision is a brand call, `the-lodestar.md` is out of scope for this chapter, and the incremental-draft splitter question is an infrastructure check rather than a research one. All three remain correctly flagged for you.
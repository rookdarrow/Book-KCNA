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

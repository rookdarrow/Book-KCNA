# Image Specifications — KCNA Chapter 20

*Generated from draft-v1.md (draft-voice.md does not exist at this stage). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

---

## NO FIGURES IN THIS CHAPTER

The draft contains **zero** `<!-- FIGURE: chNN-figMM-slug -->` anchors and **zero** ASCII diagrams. This document is therefore empty of figure entries by extraction, not by omission.

**Scan result:**

| Check | Result |
|---|---|
| `<!-- FIGURE: ... -->` anchors found | 0 |
| Fenced code blocks found | 1 (draft-v1.md ~line 96, question 12) |
| Fenced blocks that are ASCII diagrams | 0 |
| Unanchored diagrams to flag | 0 |
| Malformed anchor IDs to flag | 0 |

**The one fenced block is not a diagram.** Question 12 embeds a Pod manifest:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: check
spec:
  containers:
    - name: app
      image: example/app:1.0
```

This is literal YAML the reader must parse as source text to answer the item — it is the question's stimulus, not a spatial or structural depiction. Rendering it as a figure would destroy the item: the candidate is being tested on reading a manifest, which is what the real exam presents. It is correctly excluded from the figure inventory and must remain a fenced `yaml` block through to build. Under `diagram_enforcement`, this block is expected to carry no anchor.

**Why the chapter has no figures at all.** Chapter 20 is `chapter_type: mock_exam`. Its Instructions section states the design constraint explicitly — "There is no Soundings block here, no Fixed Points, no callouts in the margin: a diagnostic instrument that keeps interrupting itself with encouragement is not a diagnostic instrument." A figure in the exam block would either leak an answer or give one item a visual scaffold the other fifty-nine lack, which is a fairness defect in a scored instrument. The answer-key walkthroughs are deliberately prose-and-pointer: the visual explanation of every concept already lives in the owning chapter that each cross-bearing points back to, and duplicating those figures here would be decorative reuse, which skill Part 18.12 bans.

**The two tables in the Scoring Rubric stay tables.** The per-domain score sheet is a fill-in instrument the reader writes into, and the score-band table is a four-row lookup. Neither meets a Part 18 criterion — no spatial structure, no temporal sequence, no quantitative relationship a reader must see rather than read — and the score sheet in particular must remain selectable, reflowable text so it survives the EPUB at every column width and stays usable on a phone.

---

## UNANCHORED DIAGRAMS

None.

---

## Notes for the downstream stages

- **No `yaml-figure-spec` blocks are emitted.** The certcomp-diagrams D1 router should receive an empty figure set for `kcna/ch-20` and take no action. This is a valid empty result, not a missing file.
- **Two `<!-- AUTHOR-REVIEW: ... -->` comments are present in the draft** (at the item-42 gap in the answer key, and above the per-domain score sheet). Both concern item numbering and domain tallies, not figures. They are out of scope for this stage and are left untouched — flagging them here only so a later stage does not read this document's emptiness as evidence the chapter is clean.
The write to `Book-KCNA` is blocked — the tool needs permission that hasn't been granted, and this session is non-interactive so the prompt can't be answered. The document is fully composed and ready; I just can't put it on disk.

**To unblock:** grant write access to `C:\dev\lodestar\Book-KCNA\.pipeline-state\` (via `/permissions` or `.claude/settings.json`), and I'll write it immediately. Alternatively, tell me to stage it under `certcomp/` and you can move it.

Here's what B3 concluded, so you can sanity-check the design before it lands:

**Spacing targets.** Ch 3 at 10%, Ch 4 at 15%, then 20–25% through Ch 18. Five chapters sit at the 25% ceiling — Ch 13 and 16 (the troubleshooting/debugging arc), Ch 15 and 17 (the two Zeniths), and Ch 18 (last content chapter, most accumulated decay). Each because retrieval *is* the chapter's method, not a tax on it.

**Three structural decisions worth your review:**

1. **Ch 1 is excluded from retrieval entirely.** The skill's table assumes Ch 1 is a content chapter; here it's orientation at 0% weight. So Ch 3's 10% draws from Ch 2, and no item anywhere tests exam mechanics.
2. **Soundings are excluded from the budget but do the work anyway.** Part 11 requires Soundings be answerable from prerequisites — which in this book *means earlier chapters*. So every Soundings block is already a spaced retrieval event. Counting it would distort its calibration purpose; the drafting instruction is to source Soundings from B2's Prerequisites column, making the spacing free.
3. **A spacing floor:** from Ch 8 on, at least one item must come from ≥4 chapters back. Without it the schedule quietly degenerates into "test the previous chapter."

**Nine cross-cutting themes**, headed by the control loop (Ch 3 → 4 → 6 → 11 → 15 → 17 — the primary Zenith depends on it) and namespaced-vs-cluster-scoped (which *derives* the RBAC four-way matrix instead of memorizing it). One is a pattern rather than a fact: **"the object exists but nothing happens without the component"** — Ingress without a controller, NetworkPolicy on an unsupporting CNI, `kubectl top` without metrics-server, VPA not shipped by default. Naming it once and retrieving it by name turns four gotchas into one rule.

**A decay problem I flagged and fixed:** Ch 8's version-skew block is the densest pure-recall material in the book, taught at the 40% mark and otherwise never revisited before exam day. The schedule deliberately places version skew in Ch 13 (as a troubleshooting cause) and release cadence in Ch 17 (where the three-supported-minors rule and the ~3/year cadence explain each other). Ch 7 (scheduling) and Ch 14 (Helm) are similarly thin and get named anchors.

**Also specified:** four things that must *not* be retrieved — Ch 1 mechanics, the dated graduated-project roster (retrieve the maturity *levels* instead), the unpublished 60-question/75% figures, and any `[inferred]` trap framed as exam frequency.
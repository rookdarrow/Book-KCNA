```markdown
# Fact-Accuracy Audit — Chapter 4

## Mode detected: **BLOCKED — no draft available**

Neither input file could be read:

- `draft-v2.md` — `[file not available]`
- `draft-voice.md` — `[file not available]`

Mode detection could not be run, because both detection signals (presence of
`[source:` tags in the draft; state of the sources directory) require the draft
text. The cached-sources block IS populated (79 snapshots, KCNA-scoped, fetched
2026-08-23 / 2026-08-24), so signal 1 does *not* indicate adoption mode — but
signal 2 is undeterminable without the draft.

## Summary

- Total factual claims inspected: 0
- Tagged claims verified: 0
- Tagged claims unverifiable (source tag points to missing/empty snapshot): 0
- **Untagged factual claims (FAIL): 0**
- **Contradicted claims (FAIL): 0**
- Minor discrepancies (WARN): 0

No audit was performed. The zeroes above are the absence of an audit, **not a
clean bill of health**. Do not treat this report as a passing gate.

## BLOCKER — draft input missing

**What happened:** Stage 6 received `[file not available: draft-v2.md]` and the
fallback `[file not available: draft-voice.md]` in place of chapter text.

**Likely causes, in order of probability:**

1. **Upstream stage did not produce output.** Stage 3 (drafting) or the voice
   stage failed, was killed, or wrote nothing. Check for a `.heartbeat` sidecar
   and the `.progress.log` NDJSON stream in the chapter's pipeline-state
   directory — presence of a heartbeat means a stage is still live and Stage 6
   was run too early.
2. **Path resolution.** The executor passes `--add-dir` so the CLI subprocess can
   reach the book's `.pipeline-state/` tree. If that flag was dropped, the stage
   reads a path relative to `certcomp/` and silently finds nothing — this is the
   exact failure mode the 2026-04-22 executor change was made to fix.
3. **Chapter-number mismatch.** This prompt is headed "Chapter 4", but the
   cached sources are heavily annotated for Chapters 1, 2, and 3 (§-level
   drafting notes for ch01/ch02/ch03, `ch02-fig02`/`ch02-fig04`/`ch03-fig03`
   anchors, Chapter 3 open questions #8/#9). No snapshot carries Chapter 4
   scoping notes. It is worth confirming that a Chapter 4 draft exists at all
   before assuming a read failure.

## Required before re-running Stage 6

1. Confirm the draft exists on disk:
   `ls ../Book-KCNA/.pipeline-state/ch-04/draft-v2.md` (and `draft-voice.md`).
2. If absent, check for a live or crashed upstream stage:
   `cat ../Book-KCNA/.pipeline-state/ch-04/.draft-v2.md.heartbeat`
   `tail -50 ../Book-KCNA/.pipeline-state/ch-04/.draft-v2.md.progress.log`
3. If present on disk but not delivered to this stage, verify the executor's
   `--add-dir` argument covers the book's pipeline-state tree.
4. Re-run Stage 6 once the draft materializes. The cached-source block is intact
   and sufficient to audit; only the draft is missing.

## Notes for the re-run (carried forward, not findings)

These are known hazards in the cache that the eventual Chapter 4 audit should
apply. They are recorded here so the information isn't lost to a failed stage;
none of them is a finding against a draft.

- **Do not accept "60 questions" as sourced.** `provenance-kcna-60-questions-2026-08-23.md`
  is explicitly marked NOT AUTHORITATIVE. The count is absent from every
  authoritative LF/CNCF source checked.
- **Passing score phrasing is constrained.** Only
  "The Linux Foundation publishes a 75% passing standard for its multiple-choice
  exams, of which the KCNA is one" is supportable
  (`lf-mc-exam-faq-2026-08-23.md`). Attributing 75% to the KCNA exam page is FALSE.
- **Retired domain weights (46/22/16/8/8) are an OPEN GAP.** Per
  `cncf-curriculum-repo-kcna-versions-2026-08-23.md`, the retired PDF's text was
  never extracted. Any draft stating those weights is unsourced regardless of tag.
- **CRI/registry boundary.** `cncf-glossary-container-image-2026-08-24.md`
  carries a DO-NOT-QUOTE marker on its CRI sentence; cite
  `k8s-docs-cri-2026-08-24.md` for CRI instead.
- **Kernel vs. OS wording.** Three authorities, two registers, no factual
  conflict — see the wording note in `docker-docs-what-is-a-container-2026-08-24.md`.
  Chapters must not diverge on this sentence; the reconcile pass will surface a
  mismatch.
```
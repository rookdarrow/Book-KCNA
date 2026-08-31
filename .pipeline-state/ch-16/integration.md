I couldn't write `.pipeline-state/ch-16/integration.md` — the write permission wasn't granted in this session. The report is complete and ready to write on approval. Here are the findings.

## Summary

- Terminology consistency: **pass**
- Callbacks: **51 cross-bearings / 24 distinct targets — all correct.** All 9 inbound pointers from Ch 5, 9, 12, 13 resolve.
- Retrieval-practice accuracy: **fail** (6 of 7 correct)
- Glossary coverage: 28 concepts, 26 defined in-chapter, **6 need entries, 4 need new ledger rows**
- Contradictions with earlier canon: **1, and it's a blocker**
- Ethical guardrails: **fail** — 3 exam-frequency claims

## The blocker: Ch 16 §4 contradicts shipped Ch 9 §4, and both are graded

Shipped Ch 9 teaches that a not-ready Pod is **not in the EndpointSlice**:
- `chapter-09:740` Fixed Point — "A Pod must both **match the selector** and be **Ready** to appear in the Service's EndpointSlice"
- `chapter-09:844` Bearings #2: four matching Pods, one failing readiness → published answer is **three**, and `:874` explicitly refutes "Four"
- `chapter-09:868`, `:1602`, `:1729` carry the same rule

Ch 16 §4 teaches the opposite ("**All** the matching Pods — readiness is not a filter on membership"), grades it at Bearings 2 Q1, and its Exam Alert names the Ch 9 position as a trap to unlearn. A reader gets marked wrong once in each direction by the same book.

Both chapters cite snapshots; the upstream docs are themselves inconsistent across pages. Adjudicating that is stage 6's call. What's useful here: **Ch 9 already contains the machinery to state it Ch 16's way** — `:750` says terminating Pods are "not immediately removed from EndpointSlices" with `ready: false`, and `:754` already introduces the `serving` condition. So if the ruling favours Ch 16, the Ch 9 repair is contained: the Fixed Point, one Bearings answer (3→4), Practice Q11's answer, two table rows. Needs an author ruling; both chapters move in one commit.

Same commit should fix `chapter-09:766`, whose inbound gloss "*a Service whose endpoint list is empty*" no longer describes a section built on the list often not being empty.

## Other findings

**Retrieval fail — Bearings 3 Q2** (`[retrieval: ch11]`): Ch 11 teaches the Retain default (`:1235`, `:1412`) but never names `persistentVolumeClaimRetentionPolicy`, and `whenDeleted`/`whenScaled` appear nowhere in the shipped chapter. Distractor C can't be evaluated without that vocabulary. Reword to the fact Ch 11 shipped, or drop the tag.

**Guardrails** — the book has a ratified no-frequency-claims convention (`chapter-12:1873`, `chapter-14:34`, `chapter-15:411`, `chapter-lineup:184`). Three lines cross it: "What gets tested here is not flag syntax", "the fact the exam reaches for", "the shape the exam favors". §3's "the constraints are exam material" is fine — `chapter-11:559` uses the same construction.

**The draft's own "distroless" AUTHOR-REVIEW is wrong.** It says the term has no ledger owner; B7 assigns it to **Ch 16 §3**, and since it appears in no shipped chapter, this is also its first appearance in the book. Delete the comment before stage 14 chases it.

**Glossary/ledger:** `Init:N/M` family is the priority — it appears in no shipped chapter (Ch 13 uses `PodInitializing`), yet Bearings 1 Q2 and Practice Q3 both grade it. Also termination message, the PVC retention field names, distroless, Telepresence.

**Safe Harbor placement** — Ch 16 puts 🏆 before the §8 Zenith; Ch 10, 11, 12, 13 all put it after, unanimously. Author's call.

## Answering the draft's open questions

- **Frontmatter is not this stage's gap.** `ch-13/draft-v2.md` also has none; shipped Ch 13 does. The revision was right to leave it. The real item: Ch 13's note at `:21` names Ch 16 as the D3.2 twin, so `D3.2` is required; whether `D2.3` must also appear needs a ruling before stage 14 writes the block.
- **PSA refusing a debug container is backed by shipped canon** — `chapter-12:1342` states it and points at Ch 16 §3. Reciprocal and consistent; Practice Q9 is safe on integration grounds.
- **Margin-icon density (16) is in family** — shipped chapters run 5–17, Ch 11 is also 16. Not a finding.
- Ordinal-count convention, heading form, Zenith marking, "The Voyage Ahead", and the Soundings all check out.

Want me to write the file? Approving the write to `.pipeline-state/ch-16/integration.md` is all it needs.
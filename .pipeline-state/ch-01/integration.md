# Integration Check — KCNA Chapter 1

## Summary

- Terminology consistency: **pass** — no internal contradictions; 4 canon-setting conventions should be locked here, since Chapter 1 is the first chapter and establishes them for the other nineteen
- Callbacks to earlier chapters: **n/a** — Chapter 1 is the first chapter; there are zero backward references. Forward cross-bearings checked instead: **14 correct / 2 incorrect**
- Retrieval-practice accuracy: **pass** — 0 retrieval items, which is correct (Stage B3 excludes Ch 1 from the retrieval schedule entirely). One forward *commitment* made in prose is verified against B3 below
- Glossary coverage: **35 concepts surfaced, 11 defined or characterized in-chapter (5 fully / 6 partially), 30 require book-level glossary entries**
- Contradictions with earlier canon: **3 flagged** (against ratified book-outline artifacts, not against earlier chapters — none exist)
- Ethical guardrails (skill Part 14): **pass**, with 3 items referred for author decision

**Sources consulted for this check:** `.pipeline-state/book-outline/chapter-lineup.md` (B2, ratified), `.pipeline-state/book-outline/retrieval-architecture.md` (B3 — see operator note), `.pipeline-state/ch-01/outline.md`, `.pipeline-state/ch-01/diagnostics/question-quality.md`, `.pipeline-state/ch-01/diagnostics/structural.md`. No knowledge-base shards were tagged, which is expected: Chapter 1 is the first chapter drafted and the shard set is empty by construction, not by omission.

---

## Terminology consistency

There are no earlier chapters, so nothing here is *drift* in the usual sense. Chapter 1 is instead the chapter that **sets** canonical form for the rest of the book. That makes these items higher-leverage than they look: whatever ships here becomes the reference every subsequent chapter is linted against.

| Term | Canonical form (as established here) | Occurrences | Drift? |
|---|---|---|---|
| KCNA / Kubernetes and Cloud Native Associate | Full name once, on first use; `KCNA` thereafter | ~13 | No |
| CNCF / Cloud Native Computing Foundation | Full name on first use; `CNCF` thereafter | 6 | No |
| Linux Foundation | `the Linux Foundation` (no "The" mid-sentence) | 6 | No |
| cloud native (adjective) | Unhyphenated, lowercase in prose; Title Case only inside domain names | ~14 | No — matches CNCF's own style |
| Kubernetes Fundamentals / Container Orchestration / Cloud Native Application Delivery / Cloud Native Architecture | Full Title Case domain names | ~20 | **Yes, minor** — see (a) |
| `kubectl` | Lowercase, code font | 2 | **Yes** — see (b) |
| Pod / Service / StatefulSet | Capitalized (Kubernetes docs convention) | 4 | No |
| domain vs competency | `domain` = one of four weighted blocks; `competency` = a named topic inside a domain | ~25 | No — used precisely throughout, and this distinction is load-bearing for the whole book |
| blueprint vs curriculum | Mixed | blueprint ~11, curriculum 2 | **Yes, minor** — see (c) |
| Weight quad `44 / 28 / 16 / 12` | Three notations in use | 6 | **Yes, cosmetic** — see (d) |
| Branded markers (🧭 ☆ ★ ⚠ — 🏆 ☀️) | Skill v5.7 names and symbols | Legend + in-text | No — all correct, including `☀️ Zenith` and `⚠ Navigational Hazards` |
| Voyage Progress `🗺️→🌊→🌅` | Skill v5.6 progression | 1 | No — correct symbols, but see (e) |
| `The Voyage Ahead` | Locked 2026-04-19 | 1 | No |

**(a) `Cloud Native App Delivery` in `ch01-fig01`.** The ASCII figure abbreviates the domain name to fit column width. The domain name is a published CNCF string and the book will repeat it ~40 times; an abbreviation appearing in the book's *first* figure risks propagating. The rendered SVG has width the ASCII doesn't, so this is fixable in `image-specs.md` without touching prose. Prose shorthand ("Application Delivery") is fine and should stay.

**(b) `kubectl` formatting.** Appears once in code font ("drilling `kubectl` commands") and once bare ("not a kubectl drill book"), within four lines of each other. Lock code font everywhere; the linter can enforce it from Chapter 2 onward, and Chapter 8 is where `kubectl` gets its real treatment.

**(c) `blueprint` vs `curriculum`.** The chapter subtitle and the §3 heading both say *curriculum*; the body says *blueprint* eleven times. B2 uses both. Recommend an explicit convention: **`curriculum` = the CNCF-published document** (`KCNA_Curriculum.pdf`), **`blueprint` = the domain-and-weight structure it describes**. Chapter 1's body already follows this; only the two titles diverge, and they can stay as rhetorical titles if the convention is stated once in the front matter. Chapters 19 and 20 both reason about this document repeatedly and will diverge without it.

**(d) Weight-quad notation.** `44%, 28%, 16%, 12%` (prose), `44 · 28 · 16 · 12` (🪢 Mnemonic), `44 / 28 / 16 / 12` (checkpoint answer, Chapter Summary). Not wrong anywhere; just three shapes for the single most-repeated fact in the book, which will also appear in `the-lodestar.md`, every Part opener, and Chapter 20's weighting note. Recommend `44 / 28 / 16 / 12` as the canonical shorthand and leave the middot form to the mnemonic, where the visual difference is doing work.

**(e) Voyage Progress is used but not in the legend.** §5's marker table lists seven block-level markers and four inline glyphs, but omits the Voyage Progress strip. The reader then meets `🗺️ Chart → 🌊 Passage → 🌅 Dawn` two sections later, at Safe Harbor, with no explanation. Add a row. (`☀️ Zenith` has the inverse issue — legended but never demonstrated — which is correct here: orientation chapters carry no Zenith per Part 18.10 and the outline explicitly forbids inventing one. No action.)

---

## Callback correctness

**No backward callbacks exist.** Chapter 1 references no prior material, correctly.

Sixteen forward cross-bearings were checked against the ratified chapter lineup (B2). Fourteen point at the right chapter. Two do not.

### ✗ Incorrect: `[cross-bearing: see Ch 3 §4 — the Container Runtime Interface]` (Soundings, answer 2)

Per B2, the Container Runtime Interface is **Chapter 2** material: Ch 2 (`D1.4`) covers "OCI runtime/image/distribution specs, runC, **CRI**, containerd, CRI-O, RuntimeClass." Chapter 3 covers control-plane components, node components, addons, controllers, and the control loop — CRI is not in its objective list. B2's own Zenith note confirms the home chapter, citing "CRI (Ch 2)" when describing Chapter 17's extension-points synthesis.

There is a defensible reading — Chapter 3 does teach the container runtime as a *node component* — so the author has two clean fixes:
- **Repoint:** `see Ch 2 §N — the Container Runtime Interface`, or
- **Relabel:** keep Ch 3 and change the label to `see Ch 3 §4 — node components and the container runtime`, letting Ch 2 own the CRI acronym.

The first is preferable: the answer's payload is "a separate container runtime does the work," and Chapter 2 is where a reader who wants that answer immediately will actually find it.

### ✗ Incorrect: `[cross-bearing: see Ch 12 §2 — StatefulSets and stable identity]` (§5, marker explanation)

Chapter 12 is "Locks, Keys, and Watchstanders" — `D2.2` security: RBAC, ServiceAccounts, Secrets, Pod Security Standards, supply chain, policy engines. StatefulSets appear nowhere in it. Per B2, StatefulSet is introduced in **Chapter 6** (with its sibling workload controllers, taught at the level of *why it is different* — Pods are not interchangeable, each paired with durable storage) and completed in **Chapter 11** (the PV pairing). "Stable identity" is precisely Chapter 6's angle.

This one matters more than its position suggests. It is the *illustrative* cross-bearing — the example used to teach the reader what a cross-bearing is. It is the first one a reader is invited to follow deliberately, and it lands in the security chapter. Recommend `see Ch 6 §N — StatefulSets and stable identity`.

### ✓ Correct (chapter-level)

| Cross-bearing | Target per B2 | Verdict |
|---|---|---|
| Ch 2 §1 — what a container actually is | Ch 2 = containers vs VMs, `D1.4` | ✓ |
| Ch 17 §2 — CNCF governance and the project lifecycle | Ch 17 = maturity levels, Governing Board / TOC / TAGs | ✓ |
| Ch 17 §1 — the CNCF cloud native definition (×3 uses) | Ch 17 = "CNCF cloud native definition v1.1 and its characteristics," listed first | ✓ |
| Ch 4 §1 — declarative versus imperative | Ch 4 = "Records of Intent" | ✓ |
| Ch 17 §4 — the cloud native certification landscape | Ch 17 = "the CNCF certification ladder" | ✓ chapter; §4 low-confidence, see below |
| Ch 20 §1 — how the mock exam is sized | Ch 20 = Full Mock Exam | ✓ |
| Ch 19 §3 — pacing and time discipline | Ch 19 = "exam-day pacing" | ✓ |
| Ch 19 §5 — using The Lodestar | Ch 19 = "The Lodestar walkthrough" | ✓ |
| Ch 18 §1 — observability under the current blueprint | Ch 18 = `D4.1` observability | ✓ |
| Ch 14–16 — the Application Delivery domain in full | Part IV = Ch 14–16 = `D3` | ✓ |
| Ch 8, Ch 12, Ch 17 — the developer reader's gaps | Administration / Security / Ecosystem | ✓ and well-chosen |

Unbracketed forward references also check out: "Chapter 2 opens with a shipping container" matches Ch 2's ratified subtitle *"Why the shipping container beat the ship"*; "Chapters 2, 4, 5, and 6 will feel familiar" to a developer maps exactly onto containers / objects / Pods / Deployments; "44% of your exam begins on the next page" matches Part II opening at Ch 2; "Chapter 9's Soundings… 1 out of 8" is consistent with the 8-questions-per-content-chapter rule and Ch 9 being a content chapter.

### Section numbers are unverifiable and need a sweep

Every `§N` in this chapter points into a chapter that does not exist yet. Chapter-level targets are all now verifiable against B2; section-level targets are guesses that happened to be made first. Two look shaky on their face — `Ch 17 §4` for the certification ladder, when Ch 17 carries roughly twenty topics across two competencies and the ladder is listed last; and `Ch 20 §1` for mock-exam sizing, which may live in front matter rather than a numbered section.

This is not a Chapter 1 defect, it is a book-level bookkeeping requirement: **`pipeline/reconcile.py` must sweep every cross-bearing section number once the target chapters exist**, and the same will be true of Chapters 2–18. Worth confirming the reconciliation pass validates `§N` and not just `Ch N` before the book is a dozen chapters deep and the sweep is expensive.

---

## Retrieval-practice accuracy

**No `[retrieval: chN]`-tagged questions exist in this chapter, and none should.** Stage B3 excludes Chapter 1 from the retrieval schedule entirely (Ch 1 is orientation at 0% weight; the ramp begins at Ch 3 drawing 10% from Ch 2). The question-quality audit already confirmed 0%/0% compliance. Nothing to re-check.

Two integration items do arise, both forward-looking.

### The chapter makes a concrete, bindable promise about Chapter 13 — and it holds

§5 tells the reader, in plain text: *"Chapter 13's checkpoint will ask you something from Chapter 8."* Checkpoint question QC2.2 then makes the same pairing the subject of a whole question, and its distractor C asserts that "Chapter 13 does not necessarily depend on Chapter 8."

Both claims are verified against ratified canon:
- **The retrieval exists by design.** B3 places Chapter 8's version-skew material into Chapter 13 deliberately, as a troubleshooting cause — B3 identifies version skew as "the densest pure-recall material in the book, taught at the 40% mark and otherwise never revisited before exam day." Ch 13 ← Ch 8 is exactly 5 chapters back, satisfying B3's spacing floor ("from Ch 8 on, at least one item must come from ≥4 chapters back").
- **The non-dependency is accurate.** B2 lists Chapter 13's prerequisites as 5, 7, 9, 11. Chapter 8 is not among them. Distractor C's correction is factually right.

**Action for Stage 13 on Chapter 13:** this is now a hard contract, not a stylistic preference. If Chapter 13's checkpoint ships without a Chapter 8 retrieval item, Chapter 1 has told the reader something false about the book, in a section whose entire purpose is teaching them to trust the mechanism. Flag it in Chapter 13's chapter-state so it isn't lost fifteen chapters from now.

### A ★ Fixed Point that is never retrieved

Chapter 1 designates `44 / 28 / 16 / 12` as the chapter's single ★ Fixed Point and tells the reader to memorize it above everything else. B3 then excludes Chapter 1 from retrieval entirely and lists "Ch 1 mechanics" among the four things that must *not* be retrieved anywhere in the book.

The net effect: the book's most emphatically flagged must-memorize fact is the one fact never retrieval-tested. That is defensible — the weights are reinforced structurally (Parts II–V are named for the domains, `the-lodestar.md` carries them, Ch 19 synthesizes against them, Ch 20 is weighted to them), and the alternative is exam-mechanics trivia questions the book is right to refuse. But it sits oddly beside §5, where Chapter 1 spends four paragraphs selling retrieval as "the single highest-leverage thing this book does structurally."

**Referred for author decision.** Cheapest resolution if it bothers you: let the domain weights be retrieved *instrumentally* rather than as trivia — a Ch 19 item that requires the reader to allocate remaining study time across domains uses the weights without testing them as facts, and stays inside B3's exclusion.

---

## Glossary coverage

Chapter 1 is orientation, so it teaches almost no technical content — but it *names* a great deal of it. Roughly twenty Kubernetes and cloud-native terms appear in this chapter and are used without definition, which is appropriate (they are labels for chapters to come, not concepts being taught) with one exception noted below.

| Concept/command surfaced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| KCNA / Kubernetes and Cloud Native Associate | yes | yes |
| CNCF / Cloud Native Computing Foundation | yes | yes |
| Linux Foundation | partial | yes |
| CKA / Certified Kubernetes Administrator | partial | yes |
| LFS250, THRIVE-ONE | no | optional (product names) |
| exam blueprint | no | yes |
| domain (exam) | no | yes |
| competency (exam) | no | yes |
| container | partial (Soundings A1) | yes — full treatment Ch 2 |
| virtual machine | partial (contrast only) | yes — Ch 2 |
| container orchestration / orchestrator | partial (Soundings A2) | yes — Ch 3 |
| container runtime | partial (Soundings A2) | yes — Ch 2 |
| Container Runtime Interface (CRI) | no (named in a cross-bearing label only) | yes — Ch 2 |
| **cloud native** | **deliberately not** — negative claim only | **yes, with a caveat — see below** |
| CNCF Cloud Native Definition v1.1 | named, not quoted | yes — Ch 17 |
| Pod | no | yes — Ch 5 |
| Service | no | yes — Ch 9 |
| StatefulSet | no (cross-bearing label only) | yes — Ch 6 |
| scheduler / scheduling | no | yes — Ch 7 |
| `kubectl` | no | yes — Ch 8 |
| observability | no | yes — Ch 18 |
| metrics / traces | no | yes — Ch 18 |
| Prometheus | no | yes — Ch 18 |
| PromQL | no | yes — Ch 18 |
| exporter | no | yes — Ch 18 |
| scrape (pull) model | no | yes — Ch 18 |
| OpenTelemetry | no | yes — Ch 18 |
| GitOps | no | yes — Ch 15 |
| Helm | no | yes — Ch 14 |
| deployment strategy | no | yes — Ch 15 |
| declarative vs imperative | no | yes — Ch 4 |
| Terraform / Ansible / CloudFormation | no | no (external tools, not exam terms) |
| The Lodestar (book artifact) | yes | optional |
| Branded markers (7 block-level + 4 inline + 2 sidebar types + cross-bearing) | yes (§5 legend) | no |
| Difficulty indicators ⚪🔵🟡🔴 | yes | no |

**Totals: 35 surfaced · 5 fully defined in-chapter · 6 partially · 30 require book-level glossary entries · 2 optional · 3 none.**

### Three things Stage 14 needs decided here, because Chapter 1 forces them

**1. The `cloud native` glossary entry collides with §4's central pedagogical device.** §4 deliberately withholds the definition for four hundred pages and asks the reader to carry the question open until Chapter 17 — the chapter's most distinctive move, and the Extended Analogy exists to justify it. But the book ships a required glossary, alphabetized, in which `cloud native` will sit near the front. Any reader who consults it during Chapters 1–16 gets handed exactly what §4 spent a section withholding.

This is a real cross-artifact contradiction, and it needs an author call rather than a default. Options, in rough order of preference:
- **Deferring entry:** *"Cloud native — a set of characteristics describing how a system is built and operated; explicitly not a statement about where it runs. Defined in full at Chapter 17 §1, where the CNCF definition is examined characteristic by characteristic."* Preserves the negative claim (which §4 states outright anyway), withholds the positive one, and reads as a pointer rather than a dodge.
- **Full entry, accept the spoil.** Defensible — glossary lookups are self-selected, and a reader who goes looking has opted out of the device.
- **Omit from the glossary.** Not recommended; the term is in the credential's name and two domain names, and its absence would read as an error.

**2. What does a glossary cross-reference point at — first mention or definition?** Chapter 1 name-drops ~20 terms it does not define. Under the skill's Part 16 requirement ("Cross-reference to chapter of introduction"), `Prometheus` first *appears* in Chapter 1 and is *taught* in Chapter 18. Recommend locking the convention now: **cite the chapter of definition, not first mention.** Otherwise a third of the glossary points at the orientation chapter, which teaches none of it. Worth adding to `structural-contract.yaml` so the linter can check it.

**3. `commands: []` in the outline frontmatter is stale.** The draft uses `kubectl`. It is named rather than taught, so no change to the chapter is needed, but the KB tagging should reflect that `kubectl` first surfaces here if Stage 14 builds a command index from those tags.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims** — with one referral, below. This chapter is unusually scrupulous on the primary axis: it explicitly refuses to present the widely-repeated "60 questions, 75%" figures as published, prices are dated to the snapshot, and every blueprint number carries a source tag.
- [x] **Fear-based content uses real examples** — the only fear-adjacent content is the ⚠ Navigational Hazards block on pacing (sourced, proportionate, and paired with a concrete correction) and the Logbook Entry (in which the candidate passes). No fear-mongering.
- [x] **Simplification acknowledged** — §2 carries a Dead Reckoning block; §2 names its own silence ("Where the page is silent, I'll say so"); §4 is an explicit uncertainty signal that tells the reader precisely what is being withheld and why. This is the strongest guardrail compliance in the chapter.
- [x] **Authority claims cite legitimate sources** — every exam fact carries a `[source: …]` tag. Two classes of unsourced claim remain; see referrals 1 and 2.
- [x] **"Frequently tested" claims verifiable** — the chapter makes no frequency claim about individual topics. "One exam question in six" is a proportion derived from the published 16%, not a question count, and is therefore consistent with §2's own argument that the count is unpublished.
- [x] **No strawmanning of alternative study methods** — genuinely careful. "The material isn't fraudulent and its authors aren't careless." "Some of it is excellent." "Use it for facts if you like." The ⚓ block softens its criticism of hands-on-first study to "partially misdirected." See referral 3 for two small exceptions.
- [x] **Subject dignity (v5.7)** — all wry beats are aimed at the practitioner's own experience (the reader's anxiety about failing, the colleague's ten minutes of recalibration). Nothing is aimed at harms borne by third parties.

### Referred for author decision

**1. The Logbook Entry is presented as a real, first-person anecdote.** *"A colleague of mine sat the KCNA earlier this year…"* — stated as fact, with specific detail (studied from a 2024-recorded course, drilled Prometheus, passed, spent ten minutes recalibrating). If the anecdote is real, no issue. If it is authored illustration, it is a fabricated factual claim in a chapter whose §2 teaches readers to distinguish what is attested from what is merely repeated — and Part 14 draws exactly this line ("Real breach stories with actual consequences" / not "Fabricated fear scenarios").

The skill's own sidebar spec invites the genre ("anecdote, war story, real-world example"), so the fix is framing, not deletion. Something like *"Here is a pattern worth expecting"* or *"Picture a candidate who…"* costs the passage almost nothing — its persuasive force comes from the mechanism it illustrates, not from its being a specific person.

**This is the first Logbook Entry in the book, so whichever posture is chosen becomes canon for nineteen more chapters.** That is the reason to settle it now rather than per-chapter.

**2. Three unsourced empirical claims about reader and candidate behavior**, stated flatly and in two cases superlatively:
- *"Chapter 17's community and collaboration material is what technically strong candidates under-study most consistently."* This traces to B1's domain analysis, where it appears as the analyst's judgment ("the competency most likely to be under-studied by technically strong candidates"), not as a sourced finding. B2 then instructs, explicitly: *"Inferred traps stay labelled as inferred… chapters must describe those as 'easy to confuse,' never 'frequently tested' — the distinction Ethical Guardrail #8 requires."* Chapter 1 hardens an inferred claim into a superlative statement of fact. Recommend hedging to authorial observation.
- *"That is the assumption almost everyone arrives with"* and *"the assumption almost every candidate arrives with"* (cloud native = public cloud), twice.
- *"repeated across dozens of study sites, videos, and forum threads"* and *"widely and consistently reported by third parties."* This one has a particular sting: the chapter's central credibility move is teaching readers to ask whether a number is published or inherited, and its own claim about how widely those numbers circulate is itself uncited. Either cache two or three representative third-party pages during a research pass and tag them, or drop the quantifier ("dozens") and let the qualitative claim stand.

Recommend settling one hedging posture for reader-behavior claims across the whole book, since every chapter will make them.

**3. Two small competitor characterizations.** *"Anyone quoting you a precise number ('Pass in 14 days!') is selling something"* imputes motive rather than describing an error, and *"the disclosure that separates this book from most of its competitors"* is an unverified comparative. Neither is a strawman — the underlying reasoning in both cases is sound and stated — and both are defensible as written. Flagged only because Chapter 1 sets tone for the series; a light rewording keeps the point without the motive attribution.

---

## Recommended fixes

**Already addressed — no action.** Every finding in the Chapter 1 question-quality audit has been carried into this revision: the Soundings rubric is rebanded over the four scoreable items with Q5 declared unscored; QC1.2 is inverted to the "*is* published" stem with the question count and study-hours distractors; QC1.3-D is replaced with the growth-rate-vs-exam-share trap; QC2.1-D is replaced with the "says nothing about how to read the chapter" option; Soundings A2 no longer spends Chapter 3's control loop; Soundings A3 is trimmed; and the `cloud-native-framing` coverage gap is closed by the new QC2.3. The three open `AUTHOR-REVIEW` comments in the draft (the retired-blueprint weight provenance, the passing-score FAQ snapshot, the learning-science citations) are correctly left for the author and are not re-raised here.

### Blocking — wrong destination, fix before the gate

1. **`Ch 3 §4` → Chapter 2** for the Container Runtime Interface cross-bearing (Soundings, answer 2). Or relabel to "node components and the container runtime" and keep Ch 3.
2. **`Ch 12 §2` → Chapter 6** for the StatefulSet cross-bearing (§5). Chapter 12 is the security chapter; this is the example that teaches the reader what a cross-bearing is.

### Contradictions against ratified canon — author decision

3. **`ch01-fig02` uses different Part names than B2 ratified.** The figure labels the six Parts *Orientation / Kubernetes Fundamentals / Container Orchestration / Application Delivery / Cloud Native Architecture / Departure*. B2's ratified titles are *I — Taking Departure · II — Ship, Cargo, and Company · III — Underway · IV — Dispatches · V — The Wider Sea · VI — Making Port*, chosen to carry the Communications Officer role family's atmospheric register.

   Beyond the divergence, the figure's own labels have an internal problem: it calls Part **VI** "Departure," while Chapter 1 is itself titled "Taking Departure" and B2's Part **I** carries that name. A departure at the *end* of the voyage reads backwards, and B2's Part VI is "Making Port" for exactly that reason.

   Two clean resolutions: print both (`II — Ship, Cargo, and Company · Kubernetes Fundamentals · 44%`), which is probably strongest since the figure's whole argument is that Parts map onto domains; or print the ratified titles alone and let the domain column carry the mapping. Either way the figure needs a matching update in `image-specs.md` before the diagram pipeline renders it.

4. **Competency count: the chapter is right and the book outline is wrong.** Chapter 1's table enumerates 13 competencies (4 + 4 + 2 + 3), matching the cached CNCF curriculum snapshot verbatim and matching B1's own `D1.1`–`D4.3` identifier scheme, which yields 13 identifiers. But `chapter-lineup.md` states "12 competencies" and "twelve named competencies," twice. **Correct B2 to thirteen** before Chapter 19's synthesis, the blueprint appendix, or the front-matter disclosure inherits the wrong figure. No change to Chapter 1.

5. **Chapter 1's outline frontmatter no longer matches the chapter.** `question_budget` still reads `taking_your_bearings: 5` (3 + 2) and `total_this_chapter: 10`. The revised draft carries **6** Bearings questions across 3 + 3, total **11** — which is the correct outcome, and exactly what the question-quality audit's recommended option 1 called for ("amend the outline"). The amendment was never made. Update to `6` / `11` so the book-level question-budget rollup and Stage 14's KB update read live numbers.

### Non-blocking — lock the convention here

6. Add a **Voyage Progress** row to §5's marker legend; the strip appears at Safe Harbor unexplained.
7. Set `kubectl` in code font in both occurrences.
8. Expand `Cloud Native App Delivery` to the full domain name in `ch01-fig01` (the SVG has the width the ASCII doesn't).
9. Adopt `44 / 28 / 16 / 12` as the canonical weight-quad shorthand; leave the middot form to the mnemonic.
10. State the `curriculum` (the CNCF document) vs `blueprint` (the structure) convention once, in front matter.
11. Decide the glossary cross-reference rule — **chapter of definition, not first mention** — and the `cloud native` deferring-entry form, before Stage 14 builds the glossary.

### Operator notes, not chapter defects

12. **`book-outline/retrieval-architecture.md` is not the B3 document.** The file on disk contains a permission-denied message and a prose summary of what B3 concluded; the artifact itself was never written. The summary is detailed enough that this check could verify the Ch 13 ← Ch 8 commitment against it, but every subsequent chapter's retrieval planning will read a file that is a stage-failure notice. Re-run B3 with write access to `.pipeline-state/`, or persist the composed document, before Chapter 3 — which is where the retrieval schedule actually starts.
13. **Stage 4's `output_path` registration still points at a nonexistent `draft-voice.md`.** Flagged by the question-quality audit as non-blocking; it recurs for every chapter and every downstream diagnostic reading from state. Worth fixing before Chapter 2 runs.
14. **`diagnostics/structural.md` reports `0 fail, 0 warn, 0 pass`.** Zero *passes* means the linter evaluated no checks, so this chapter has no independent structural corroboration. Also noted by the question-quality audit; both that audit's counts and this one's were taken by hand.
15. **The `[retrieval: chN]` tag's rendered form is still unresolved** — reader-visible or draft-only annotation. Chapter 1 correctly carries none, but §5 describes the mechanism to readers in prose, so the decision has a reader-facing dimension. Chapter 3 is the first chapter that needs it settled.
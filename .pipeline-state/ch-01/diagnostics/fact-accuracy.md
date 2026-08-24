# Fact-Accuracy Audit — Chapter 1

## Input note (read first)

The stage prompt declared `draft-v2.md` and fell back to `draft-voice.md`; **neither file exists** in `Book-KCNA/.pipeline-state/ch-01/`. The audit was run against the current post-voice draft on disk, `draft-v1.md` (481 lines, written 2026-08-24 00:04, with `draft-v1-prevoice.md` as the pre-voice backup). Line numbers below refer to that file. If the orchestrator's stage-input mapping expects a `draft-v2.md` at this point in the graph, that mapping is stale for this book.

## Summary

- Total factual claims inspected: **53**
- Tagged claims verified: **23**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — all six cited snapshot slugs resolve to cached sources
- **Untagged factual claims (FAIL): 9**
- **Contradicted claims (FAIL): 1**
- Minor discrepancies (WARN): 14

Mode detected: **standard**. The draft carries 23 inline `[source: ...]` tags and the cached-source set is populated.

Overall: the exam-facts spine of this chapter is unusually clean. Every published figure — price tiers, duration, attempt count, validity, both blueprints' domain weights, the "not published" disclosure — matches its snapshot exactly, including the hedges ("no earlier than," "commonly reported, not official"). The failures cluster in two predictable places: conceptual claims outside the exam-facts sections (Soundings answers, the "cloud native" section), and learning-science claims for which **no source was ever cached**.

---

## FAIL — Untagged factual claims

### Line ~56: "The host's **kernel**. A virtual machine boots its own operating system on virtualized hardware; a container is a process on the host that has been given an isolated view of the system."

**Why it's a factual claim:** asserts the technical isolation boundary of containers vs. VMs — a definitional claim the exam tests directly under D1 Containerization.
**Fix:** Tag `[source: k8s-docs-overview-2026-08-23]`. Note the snapshot phrases it as sharing the **operating system** ("Containers are similar to VMs, but they have relaxed isolation properties to share the Operating System (OS) among the applications"), not specifically the *kernel*. The draft's "kernel" is more precise and more correct, but it is not what the cached snapshot says — either soften to match, or accept the sharpening and note it.

### Line ~58: "Kubernetes is an **orchestrator**… A separate **container runtime** on each machine does the work of actually starting containers."

**Why it's a factual claim:** asserts the division of responsibility between Kubernetes and the CRI runtime.
**Fix:** Tag `[source: k8s-docs-cluster-architecture-2026-08-23]` (or `k8s-docs-containers-2026-08-23`), both of which support "Kubernetes relies on a container runtime" / "Container runtime — Software responsible for running containers." See also WARN on the word "orchestrator."

### Line ~90: "The hands-on Kubernetes certifications, the ones that drop you into a live terminal with a broken cluster and a running clock, measure whether you can *do* the thing."

**Why it's a factual claim:** states the format of third-party certifications (CKA/CKAD/CKS).
**Fix:** One-token repair — the supporting tag already appears four lines later at line ~94. Add `[source: lf-cloud-native-certification-catalog-2026-08-23]` here; the snapshot states "the CKA/CKAD/CKS exams are hands-on, performance-based exams in a live terminal."

### Line ~203: "**the CNCF publishes weights at the domain level only.** There is no published per-competency or per-topic weighting."

**Why it's a factual claim:** an assertion about what the certifying body does and does not publish — and it is load-bearing, because the chapter uses it to justify the book's own emphasis decisions.
**Fix:** Mirror the tag used at line ~325 for the identical claim: `[source: lf-kcna-exam-page-2026-08-23]`. Consider also `[source: cncf-kcna-curriculum-pdf-2026-08-23]`, which likewise lists competencies unweighted. This is the chapter's own "know which facts are published" standard applied to itself — it should be visibly met at first statement, not only at restatement.

### Line ~281: "**it does not mean 'runs in a public cloud.'** … A rack of hardware in your own building can be thoroughly cloud native. A fleet of rented cloud instances can fail every characteristic of the term."

**Why it's a factual claim:** asserts the scope of the CNCF's published definition of "cloud native." This is the chapter's central conceptual hook and it is entirely untagged.
**Fix:** Tag `[source: cncf-cloud-native-definition-2026-08-23]`. The snapshot supports it directly: "deploy workloads in computing environments (public, private, hybrid cloud)."

### Line ~283: "The CNCF maintains a published definition with named characteristics."

**Why it's a factual claim:** asserts the existence and structure of a specific authoritative document.
**Fix:** Tag `[source: cncf-cloud-native-definition-2026-08-23]` (CNCF Cloud Native Definition v1.1, `github.com/cncf/toc/blob/main/DEFINITION.md`). Naming the document version here would also let Chapter 17 quote it without re-establishing provenance.

### Line ~358: "Pre-testing improves subsequent learning even when you get the answers wrong, because attempting a question primes you to notice its answer when you meet it."

**Why it's a factual claim:** cites published cognitive-science research (the pretesting / errorful-generation effect) as established fact, in order to justify a structural feature of the book.
**Fix:** **No cached snapshot covers learning science.** This cannot be verified from the current source set. Open a research gap in `research-manifest.md` for a learning-science authority (e.g. Richland/Kornell/Kao on pretesting, or Bjork's desirable-difficulties work) and tag it. If the gap won't be filled, downgrade the sentence to authorial framing ("this book is built on the assumption that…") so it stops claiming external authority.

### Lines ~360 and ~428: "Retrieving a fact after you've had time to partly forget it strengthens the memory far more than rereading it would. **That's a well-established effect**…" / "Retrieval practice. Recalling something after a delay… builds a substantially more durable memory than rereading the same passage would."

**Why it's a factual claim:** the phrase "a well-established effect" is an explicit appeal to external scientific consensus, made twice, and used to instruct the reader not to skip a book mechanism.
**Fix:** Same gap as above — no snapshot exists for the testing/spacing effect. Open one research gap covering both pretesting and retrieval practice (Roediger & Karpicke 2006 is the canonical citation) and tag both instances from it. Of all the advisories here, this is the one most worth actually sourcing: the chapter spends §2 teaching readers to distinguish published facts from inherited ones, then makes an unsourced appeal to research two sections later.

### Lines ~446–458: the **Chapter Summary** table — entire block untagged

**Why it's a factual claim:** the table restates the chapter's most quotable exam facts with no provenance: "90 minutes · no prerequisites · 12-month eligibility window · 2 attempts included · valid 2 years · $250 exam-only as of 2026-08-23"; the four domain weights; "Effective no earlier than 2025-11-24. Five domains → four… App Delivery doubled (8% → 16%). Orchestration +6 points"; "'60 questions, 75%' is commonly reported, not official"; "CNCF publishes domain-level weights only."
**Fix:** Every figure in the table is verified against its snapshot elsewhere in the chapter — the content is correct, the provenance is missing. Add a single source line beneath the table: `[source: lf-kcna-exam-page-2026-08-23] [source: lf-kcna-program-changes-2026-08-23]`. This is the highest-value fix in the report: summary tables are the part of a chapter most likely to be photographed, quoted, and separated from the surrounding prose.

---

## FAIL — Contradicted claims

### Line ~281: "It's in the credential's name. **It's in three of the four domain names.**"

**Tag:** untagged, but contradicts the tagged domain table at lines ~150–157 and `[source: lf-kcna-exam-page-2026-08-23]`.
**Snapshot says:** "Kubernetes Fundamentals — 44% … Container Orchestration — 28% … Cloud Native Application Delivery — 16% … Cloud Native Architecture — 12%"
**Draft says:** "It's in three of the four domain names."
**Analysis:** "Cloud Native" appears in **two** of the four current domain names — Cloud Native Application Delivery and Cloud Native Architecture. Kubernetes Fundamentals and Container Orchestration do not contain the phrase. Three is the count for the **retired five-domain blueprint** (Cloud Native Architecture, Cloud Native Observability, Cloud Native Application Delivery), which suggests this sentence is a survival from old-blueprint reasoning.
**Recommended fix:** Change to "It's in two of the four domain names." If the larger number is wanted, it is available and defensible via the competency list: "Cloud Native" also opens two of Cloud Native Architecture's three competencies (Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration) — but that must be stated as competencies, not domains.
**Note for the revision stage:** this error sits four sections after the chapter teaches readers to spot stale material by counting domains. It should be treated as the priority correction in this chapter.

---

## WARN — Minor discrepancies

1. **Line ~60 — "It was donated by Google in 2015."** The snapshot (`k8s-history-ten-years-2026-08-23`) dates the *CNCF's founding* to 2015 and says Kubernetes "was donated by Google to the newly formed Cloud Native Computing Foundation (founded 2015 under the Linux Foundation) as its first project." The donation year is strongly implied but not stated as such. Low risk; consider "donated by Google to the newly formed CNCF in 2015."

2. **Line ~84 — "The Linux Foundation, which administers it on behalf of the CNCF."** No snapshot states this administrative relationship in these terms. `cncf-who-we-are-2026-08-23` says "CNCF offers certifications including the Kubernetes certifications (KCNA, KCSA, CKA, CKAD, CKS)"; the exam page is hosted by the Linux Foundation; CNCF "is part of the nonprofit Linux Foundation." The inference is sound but the phrasing asserts a division of labor no source spells out.

3. **Line ~84 — "the entry point to the cloud native certification family."** `lf-cloud-native-certification-catalog-2026-08-23` lists ten certifications at the beginner/associate tier (KCNA, KCSA, CNPA, CBA, PCA, OTCA, CGOA, CAPA, CCA, KCA). KCNA is *an* entry point and arguably the canonical one, but "the" overstates what the catalog shows. Suggest "the usual entry point."

4. **Line ~58 — "Kubernetes is an **orchestrator**."** `k8s-docs-overview-2026-08-23` explicitly pushes back on this framing: "Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration. The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C. In contrast, Kubernetes comprises a set of independent, composable control processes." The KCNA blueprint itself names a "Container Orchestration" domain, so the word is exam-correct and should stay — but a chapter this attentive to precision may want a forward pointer noting that the Kubernetes docs draw a finer distinction.

5. **Line ~90 — "Given **four** plausible-sounding statements about how the scheduler decides where a Pod goes."** The option count per question is not published on the exam page; the snapshot confirms only "multiple-choice." The chapter's own thesis is about not treating inherited format details as published ones. Suggest "a set of plausible-sounding statements," or flag the four-option model explicitly as the book's practice convention.

6. **Lines ~179, ~244, ~386 — the effective-date hedge relaxes.** Line ~138 states it correctly: "effective **no earlier than** November 24, 2025," matching `lf-kcna-program-changes-2026-08-23` ("will be updated no earlier than November 24, 2025"), and the summary table at line ~452 preserves it. But the figure caption says "The **2025** KCNA blueprint restructure," the answer explanation at line ~244 says "the blueprint **retired in November 2025**," and the Logbook Entry at line ~386 places a colleague's sitting "in early 2026" under the new blueprint. The current four-domain blueprint on the exam page (fetched 2026-08-23) is strong evidence the change did land, but none of the three snapshots confirms the actual effective date. Recommend softening line ~244 to "the blueprint retired in the 2025 restructure."

7. **Line ~185 — "This is the single largest proportional change in the restructure."** By proportion: App Delivery 8→16 is +100%; Container Orchestration 22→28 is +27%; Architecture 16→12 is −25%; Fundamentals 46→44 is −4%. But Cloud Native Observability went 8→0, a −100% change that ties or exceeds it. The chapter treats Observability's disappearance as a separate structural fact, which is defensible, but the superlative is arguable as written. Suggest "the largest proportional change among the domains that survived."

8. **Line ~260 — false distractor premise left uncorrected.** Distractor D reads "Prioritize Cloud Native Architecture, since it contains the most named competencies." Per the blueprint, Cloud Native Architecture has **three** competencies while Kubernetes Fundamentals and Container Orchestration have **four** each — so D's premise is factually false, not merely bad reasoning. The explanation rebuts the reasoning ("Competency *count* is not weight") and states CNA "has three named competencies and the smallest weight," but never tells the reader the premise was wrong. A reader who picked D leaves believing CNA has the most competencies. Add one clause: "and it doesn't have the most anyway — Fundamentals and Orchestration have four each."

9. **Line ~62 — "That is the near-universal assumption."** An unverifiable claim about what readers believe. No snapshot bears on it, and none could. Retained as authorial framing; noted only because the same sentence sits adjacent to a sourceable claim about the CNCF definition.

10. **Line ~185 — "it's the one most third-party material serves worst" / "most guides gave it a thin chapter."** Characterizations of the third-party study-material market with no cached source and no realistic way to source them. Low exam risk, but they are assertions about identifiable third parties stated as fact. Consider hedging to "material built for the old blueprint will under-serve it," which follows directly from the sourced weight change.

11. **Lines ~474, ~476 — the shipping-container history.** "the sort that **stacks eight high** on a vessel" and "The intermodal shipping container changed global trade… by being a box that every crane, truck bed, railcar, and ship's hold in the world agreed to handle identically." These are real-world historical/logistics claims with no cached snapshot. They function as an analogy vehicle (rule 3 territory) and carry no exam weight, so no action is required — but the "eight high" figure is the kind of specific number a reader may repeat. Either soften it or source it when Chapter 2's research pass runs.

12. **Lines ~244–252 and ~266 — untagged restatements inside tagged sections.** The checkpoint bullet "✓ The four current domains and their weights — 44 / 28 / 16 / 12" and the answer bullets ("90 minutes is published"; "two attempts are published"; "Container Orchestration's four competencies are Networking, Security, Troubleshooting, and Storage") all restate figures verified elsewhere in the same section. Lower risk than the Chapter Summary block (the governing tag is within a screen's reach), but the same class of gap. No action needed if the Chapter Summary fix lands.

13. **Line ~11 vs. the Attention Budget table — internal arithmetic.** Header states "Total time: ~35 minutes"; the section rows sum to 39 minutes (6+4+5+8+4+2+4+3+3). Not an external-fact issue and likely `structural_lint`'s territory, but it is a wrong number in the first table a reader meets. Either round the header to "~40 minutes" or trim the section estimates.

14. **Lines ~386–392 — Logbook Entry is unverifiable by construction.** Flagged for completeness only. The sidebar is a practice anecdote, not a sourced claim, and every exam fact it leans on (old standalone 8% Observability domain; App Delivery now 16%) is independently tagged earlier in the chapter. No fix required; noted so the pattern is recorded — Logbook Entries should continue to restate only facts sourced elsewhere, never introduce new ones.

---

## PASS — Verified claims

All 23 tagged assertions were checked against their cited snapshots. Every one resolved to a cached source and matched.

| Line | Claim | Snapshot | Verdict |
|---|---|---|---|
| ~60 | CNCF hosts Kubernetes; CNCF is part of the nonprofit Linux Foundation | `cncf-who-we-are` | Exact |
| ~60 | Built by tens of thousands of contributors across thousands of companies | `k8s-history-ten-years` ("over 88,000 contributors from more than 8,000 companies") | Match |
| ~84 | "a user's foundational knowledge and skills in Kubernetes and the wider cloud native ecosystem" | `lf-kcna-exam-page` | Verbatim |
| ~84 | Experience level beginner; prerequisites none | `lf-kcna-exam-page` | Exact |
| ~88 | Multiple-choice, online, proctored | `lf-kcna-exam-page` | Exact |
| ~94 | CKA is a hands-on exam taken in a live terminal | `lf-cloud-native-certification-catalog` | Match |
| ~104 | Duration 90 minutes | `lf-kcna-exam-page` | Exact |
| ~104 | 12-month eligibility window; two attempts; exam preparation handbook | `lf-kcna-exam-page` | Exact |
| ~104 | Certification valid for 2 years | `lf-kcna-exam-page` | Exact |
| ~104 | $250 exam only; $299 exam + LFS250; $495 exam + THRIVE-ONE | `lf-kcna-exam-page` | All three tiers correct, correctly paired |
| ~112 | Figures current as of 2026-08-23 | snapshot `fetched_at` 2026-08-23 | Match |
| ~116 | LF does not publish question count or passing score | `lf-kcna-exam-page` ("Not stated on this page") | Exact |
| ~118 | "60 questions, 75%" is widely reported by third parties, not published by the certifying body | `lf-kcna-exam-page` ("treat those as commonly reported, not official") | Exact, hedge preserved |
| ~138 | Restructure effective **no earlier than** November 24, 2025 | `lf-kcna-program-changes` | Exact, hedge preserved |
| ~144 | Four domains: 44 / 28 / 16 / 12 | `lf-kcna-exam-page` | Exact |
| ~150–157 | Full competency table for all four domains | `lf-kcna-exam-page` + `cncf-kcna-curriculum-pdf` | All 13 competencies correct; draft correctly uses the LF page's spelling rather than the CNCF PDF's "Could Native" typo |
| ~159 | Retired blueprint: KF 46, CO 22, CNA 16, Observability 8, CNAD 8 | `lf-kcna-program-changes` | Exact; sums to 100 |
| ~183 | Observability folded in as a competency under Cloud Native Architecture | `lf-kcna-program-changes` | Exact |
| ~185 | App Delivery 8% → 16% | `lf-kcna-program-changes` | Exact |
| ~187 | Container Orchestration 22% → 28% | `lf-kcna-program-changes` | Exact |
| ~189 | Kubernetes Fundamentals 46% → 44% | `lf-kcna-program-changes` | Exact |
| ~242 | Observability is a competency under Cloud Native Architecture | `lf-kcna-program-changes` | Exact |
| ~248 | Passing score and question count not published on the exam page | `lf-kcna-exam-page` | Exact |
| ~325 | CNCF publishes weights at the domain level only | `lf-kcna-exam-page` | Supported by absence of sub-domain weights in both blueprint snapshots |

Derived arithmetic also checked and correct: 90 min ÷ 60 questions = 90 s/question (~124); 44 + 28 = 72% (~201); 16 + 12 = 28% (~201); weights descend with no ties (~201); an even 25% split gives Cloud Native Architecture 2.08× its 12% share, i.e. "more than twice" (~259); 16% ≈ one question in six (~185); 28% > a quarter (~187); Part chapter counts sum to 20 (~299 vs. the map at ~307–315).

---

## Recommended research-manifest additions

Two gaps block full verification and should be opened for Chapter 1:

1. **Learning-science authority for pretesting and retrieval practice** — needed for lines ~358, ~360, ~428. Suggested: Roediger & Karpicke (2006) on the testing effect; Bjork on desirable difficulties; Richland, Kornell & Kao (2009) on pretesting. This gap will recur in every chapter, since Soundings and cross-chapter retrieval are book-wide mechanisms — worth caching once at book level rather than per chapter.
2. **Intermodal shipping-container history** — needed for lines ~474, ~476, and load-bearing for all of Chapter 2's opening. Suggested: Levinson, *The Box*, or ISO 668 container-standard documentation.
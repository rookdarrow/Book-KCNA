Audit complete. Emitting `diagnostics/curriculum-alignment.md` (line citations are against `.pipeline-state/ch-17/draft-v1.md`, 1660 lines):

```markdown
# Curriculum-Alignment Audit — KCNA Chapter 17

## Authority note (read before the tables)

The cached objectives snapshot for this exam is `cncf-kcna-certification-page-2026-08-23.md`.
It publishes **four domain weights and no sub-competency enumeration**: Kubernetes
Fundamentals 44% · Container Orchestration 28% · Cloud Native Application Delivery 16% ·
**Cloud Native Architecture 12%**. There is no line-item objective list in the corpus —
`cncf-curriculum-repo-kcna-versions-2026-08-23.md` is recorded as an open gap in
`provenance-kcna-60-questions-2026-08-23.md`, and B1 carries the same gap as G33.

Consequence for this audit: the finest-grained authoritative contract available is
**domain-level (D4 = 12%)**. The competency IDs D4.1 / D4.2 / D4.3 are the book's own
naming of the three competencies inside D4, not published objective IDs. Per rule 3 this is
a research-stage gap, noted and moved past; the audit is therefore conducted against
(a) the domain weight, and (b) the outline's per-section objective claims and
`kb_tags.concepts`, which are the binding contract the draft was written to.

---

## Objectives the outline claims to cover

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D4.2 | Cloud Native Ecosystem and Principles | YES — all 9 sections | appropriate overall; **four sub-areas over-deep** (see Depth mismatches) |
| D4.3 | Cloud Native Community and Collaboration | YES in prose (§2, §8) — **under-assessed in graded text** | prose appropriate; **graded coverage shallow** — 4 of 21 practice items against the outline's derived 6 |
| D4.1 | Cloud Native Observability | Not covered — Ch 18's | — correctly deferred; no drift into it |

**Section-level objective claims, verified against the draft:**

| § | Outline claims | Draft delivers | Line |
|---|---|---|---|
| §1 | D4.2 | Definition v1.1 verbatim, five characteristics as ★, non-exhaustive clause, CNCF-as-institution | 145 |
| §2 | D4.3 + D4.2 | Maturity ladder ★, lifecycle, Board/TOC/TAGs/End User TAB, Landscape | 220 |
| §3 | D4.2 | Microservices, loose coupling, immutable infrastructure, declarative APIs + the connecting argument | 334 |
| §4 | D4.2 | Four interfaces ★, documentation's six extension points as a table, aggregation layer, device plugins | 472 |
| §5 | D4.2 | Mesh definition ★, two planes ★, Envoy, sidecar/ambient, mTLS, zero trust, boundary table | 569 |
| §6 | D4.2 | Serverless ★, Knative Serving/Eventing/Functions, scale to zero | 831 |
| §7 | D4.2 | Horizontal/vertical ★, HPA, VPA, Cluster Autoscaler, Karpenter, KEDA | 933 |
| §8 | D4.3 | Four principles, SIG/WG/Committee ★, Steering, subprojects, ladder, KEPs, cadence ★, CoC, cert ladder | 1066 |
| §9 | D4.2 | Pluggability synthesis, no new material, short as designed (48 lines) | 1334 |

All 48 `kb_tags.concepts` are present. One is minimal: **`kubecon-cloudnativecon`** gets a
single clause (line 1217) with no detail. Proportionate to its exam value; recorded, not
flagged.

**Binding constraints verified as honored:**

- Metadata line reads **12%**, with the 7/5 authored-allocation disclosure in prose (lines 5, 7, 121). Outline OQ12 / G33 satisfied.
- `kb_tags.commands: []` honored — `kubectl` appears only as mentions inside stems and prose, never as a demonstration. Outline OQ9 satisfied; integration-check should not read the empty list as a tagging failure.
- No `Ch 1 §N` emitted anywhere (OQ10 satisfied). Only `Ch 3 §2` is used, correctly.
- Soundings spoiler constraints held: Q1's answer is the three-row acronym→layer table and nothing more (line 74); Q5's answer does not mention VPA (line 86); Q2's rationale does not enumerate the five characteristics (line 80).
- Barred content absent: the 60-question and 75% figures, PodDisruptionBudget, ABAC, SRE, descheduler, eBPF. Cluster Proportional Autoscaler is named-not-taught and explicitly marked ungraded (line 1034).
- ☆ checkpoint retrieval is exactly **4 of 16 = 25.0%** across 6/5/5, hitting the arc ceiling on the nose.

---

## Objectives covered in the draft but NOT in the outline

Every item below is source-backed; none is fabricated. The risk is not accuracy, it is
**altitude**: B1 sets D4's depth band at *recall and recognition*, and these additions
collectively pull the chapter toward reference depth on the exam's smallest domain.
Author decision on each.

| # | Material | Line | Outline mandate | Assessment |
|---|---|---|---|---|
| 1 | **Archived as a fourth maturity category** | 265, plus fig05 annotation, plus distractors at 445 / 1584 / 1628 | Outline plans a three-rung ladder; the source's own drafting note recommended "one clause naming it as the terminal state" | Expanded to a full paragraph + figure line + three graded appearances. Good pedagogy, over the sanctioned budget. **Lean keep**, trim to the figure note plus one clause. |
| 2 | **Project-lifecycle procedural mechanics** — 5–7 adopters, TOC sponsor, kickoff, 1-week internal comment, 2-week public comment, 2/3 supermajority | 275 | Outline mandates the *levels*, the *process* in outline, and *where criteria live* (trap #98) | The four numerals are the deepest procedural detail in the chapter and no cached source ties any of them to an exam objective. **Over-covered.** |
| 3 | **VPA's three internal components** (recommender / updater / admission webhook) | 969 | §7 plan lists axis, add-on status, in-place trap — not internals | **Over-covered** for associate tier. One clause or a Closer Look. |
| 4 | **HPA sync interval, default 15 s** | 955, load-bearing again at Q18's D rationale | Not planned | Tuning detail of the same class the Ch 2 §4 snapshot's scope warning barred. The DaemonSet exclusion beside it is legitimate and should stay. **Mild over-coverage.** |
| 5 | **mTLS four-component architecture (CA / config API server / PEPs) and the four-step handshake** | 707, 711 | §5 owns "mTLS and zero trust"; guardrail is "teach what a mesh *is* and what it *buys*" | Not configuration, so inside the letter of the guardrail; the deepest single mechanism in the chapter. **Watch-item**, defensible. |
| 6 | **Linkerd named and given a maturity level** | 730 | Not in `kb_tags` | One name. Interacts with #7 below. |
| 7 | **Eleven projects given a CNCF maturity level**, against the outline's cap of six | 260 (the six: containerd, CoreDNS, etcd, Helm, Prometheus, Argo) + Kubernetes at 260, Istio & Linkerd at 730, Knative at 843, KEDA at 1023 | OQ4: "name **at most six** graduated projects the reader has already met" | The extras are each source-backed and each sits in the section that owns them, but they erode §2's own "do not memorize the roster" instruction (line 258). **Flag for author decision.** |
| 8 | **Google Summer of Code and Outreachy** | 1213 | §8 plan lists LFX mentorship only | Sourced, warm, cheap. **Lean keep.** |
| 9 | **KCSA and CNF certification** | 1239 | Inside `cncf-certification-ladder` | Low risk. Keep. |
| 10 | **KPA-vs-HPA option in Knative** | 929 | The snapshot's drafting note called this optional and "arguably above associate tier" | Taken as a §6→§7 bridge, which is what the note said it was good for. Keep. |

---

## Depth mismatches

Published weight is domain-level only. D4 = **12%**; this book allocates ≈7 of those points
to Ch 17 and ≈5 to Ch 18 (authored, not published). Within Ch 17 the only quantified
depth contract is the outline's own item allocation, derived in §7 of the outline from B4's
weight-proportional formula and from B1's under-study warning.

| Objective / area | Weight signal | Draft depth | Mismatch |
|---|---|---|---|
| D4.2 overall | ~7 authored points, recall-and-recognition band | 7 sections, 17 of 21 practice items, 11 of 16 ☆ items | OK in aggregate |
| **D4.3 overall** | Outline derives **6 of 21** items (28.6%) from B1's "most reliably under-studied competency" | **4 of 21 (19.0%)** — Q4, Q5, Q6, Q21 | **UNDER-COVERED — the chapter's headline finding.** Prose is complete; assessment is not. |
| **§8** (D4.3's larger home) | Outline: **3 practice items** | **1** (Q21, line 1567) | **UNDER-COVERED.** §8 is 179 lines of prose carrying eleven concepts and is tested by one question. |
| §4 | Outline: 3 practice items | **4** (Q8–Q11) | Over-allocated by one |
| §5 | Outline: 3 practice items | **4** (Q12–Q15) | Over-allocated by one — and §5 is already the chapter's longest section (167 lines) for one item in a list the definition calls non-exhaustive |
| §1, §2, §3, §6, §7 | 3 / 3 / 1 / 2 / 3 | 3 / 3 / 1 / 2 / 3 | OK |
| §2 lifecycle mechanics | no objective anchors it | four exact procedural numerals | Over-covered (drift #2) |
| §7 autoscaler internals | recall-band | VPA component list, HPA sync period | Over-covered (drift #3, #4) |
| §9 Zenith | Outline OQ8: "draft it short — under a fifth of §4's length" | 48 lines vs §4's 97 — **~half**, not a fifth | Over length against its own instruction, but it does not restate the four names and it does argue rather than map. **Accept**; the constraint's purpose is met. |

**Retrieval ceiling breached in the Practice Questions.** The outline sets the same 25%
ceiling on practice retrieval as on the Bearings — ≈5 of 21. The draft tags **7**
(Q9, Q10, Q13, Q14, Q18, Q19, Q21) = **33.3%**. Related defect: **Q9 carries a bare
`[retrieval]` with no chapter list** (line 1483), the only tag in the chapter in that form.

**Two surplus items are internally redundant**, which is what makes the rebalance clean
rather than lossy:

- **Q11** (line 1497, aggregation vs CRDs) tests the exact discrimination **Q9's A-distractor rationale** already teaches three questions earlier (line 1594 region: "aggregation proxies to a service you run").
- **Q14** (line 1518, mTLS vs encryption at rest) is **Q13's C-distractor** promoted to a full item — Q13's rationale already reads "confuses transit with rest."

**§8 material with zero graded coverage anywhere** (Soundings excluded, being a pre-test):
the contributor ladder and its Member requirements; KEPs; the Code of Conduct's scope
sentence; the certification ladder — **which Ch 1:182 deferred to this chapter by name**;
subprojects; the four community principles; the vertical/horizontal/project-support SIG
orientations; LFX/CNCG/Ambassadors.

**Attention Budget arithmetic (cross-stage, flagged here because it is a depth signal).**
The row times sum to **118 minutes**; the header at line 13 reads **"~95 minutes."** 95 is
exactly the running total through §7 — so the 23 minutes unaccounted for are §8, TYB 3 and
§9. The chapter's own thesis is that readers skip the D4.3 section, and its time budget
currently prices that section at zero.

---

## Gaps the research stage flagged

The outline's Open Question 2 listed five blocking fetches. All five closed, and the draft
cites each:

| Gap | Status | Evidence |
|---|---|---|
| Microservices / monoliths as defined terms | **CLOSED** | `cncf-glossary-microservices-monoliths-coupling-2026-08-31`, cited 5× in §3 |
| Istio beyond the overview (mTLS, zero trust at depth) | **CLOSED** | `istio-security-mtls-identity-2026-08-31` + `cncf-glossary-service-mesh-2026-08-31` + `cncf-glossary-zero-trust-architecture-2026-08-31`, all cited in §5 |
| Karpenter | **CLOSED** | `karpenter-concepts-2026-08-31`, cited at 1015 |
| Vendor-neutral serverless definition | **CLOSED** | `cncf-glossary-serverless-2026-08-31`, cited at 837 |
| G14 Kubernetes origin — *verify, and point at Ch 3 §1* | **PARTIAL** | Material correctly not restated, but **no `Ch 3 §1` cross-bearing exists** anywhere in the draft. The pointer half of the instruction was not delivered. |

**Handled correctly, and worth recording so a later stage does not "fix" them:**

- **VPA in-place resize source conflict** (manifest Notes 1). Three kubernetes.io pages disagree. The draft writes *to* the conflict, states the safe claim, and leaves an AUTHOR-REVIEW comment (lines 1046–1052). This is the right treatment.
- **The 15-week cadence conflict.** Draft teaches "approximately three times per year," flags the older 15-week snapshot in an AUTHOR-REVIEW comment (line ~1176). Right treatment.
- **OQ5, Karpenter's affiliation.** Draft names it as sponsored by SIG Autoscaling and explicitly asserts *no* CNCF maturity level, then turns the absence into a teaching point (line 1019). Exactly what the snapshot's drafting note asked for.
- **The trail-map framing.** The outline's §2 plan asks for it; `cncf-landscape-and-community-2026-08-23` lists `trail-map` in `concepts_covered` but its **body does not supply it**. The draft does not invent it. Correct — this is a research gap in the snapshot's own metadata, not a draft failure. Recommend the manifest's `concepts_covered` be corrected rather than the draft.

**G32 — cost management (FinOps / OpenCost / Kubecost) — still unresolved and now silently
resolved by omission.** The outline recommended out-of-chapter and asked for confirmation,
noting the alternative risk: "silently omitting a possibly-in-scope topic is a real risk on
a 12% domain." The draft omits it entirely and leaves **no AUTHOR-REVIEW record**, while
`opencost-overview-2026-08-23.md` sits in the corpus unused. Since no snapshot enumerates
D4's sub-objectives, this **cannot be settled by this audit** — but the decision should be
visible rather than invisible.

---

## Recommended fixes

**1 — Restore §8 to three practice items by converting the two redundant surplus items.**
Cut **Q11** (line 1497) and **Q14** (line 1518); each duplicates a distractor rationale
already carried by Q9 and Q13 respectively. Replace with two §8 items drawn from the
currently ungraded material — strongest candidates: the **contributor ladder's Member
requirements** (contributions + two sponsors from different companies, line 1196–1204,
which is also the section's most memorable fact), and the **certification ladder**
(KCNA multiple-choice → CKA/CKAD/CKS performance-based, line 1235–1242, deferred here by
name from Ch 1:182 and currently tested nowhere). This single edit lands §4=3, §5=3, §8=3,
D4.3 at **6 of 21 = 28.6%** — the outline's derived figure exactly — and drops practice
retrieval from 7 to 5 (23.8%), back under the ceiling. One edit, four defects.

**2 — Give Q9 a chapter list.** Line 1483 reads `[retrieval]`; every other tag in the
chapter names chapters. It should read `[retrieval: ch6]` (the answer, CRDs as the fourth
interface, lives in Ch 6 §8).

**3 — Trim the project-lifecycle mechanics to their shape.** Line 275: keep the sequence
(application → adopter interviews → due diligence → public comment → TOC vote) and the
argument that it is "not a rubber stamp"; drop or demote the four numerals (5–7 adopters,
one week, two weeks, two-thirds). If the two-thirds figure stays, remove its echo from the
Chapter Summary (line 1629) and from TYB 1 Q4's rationale, so a non-objective detail is not
reinforced three times.

**4 — Compress the two §7 over-depth items.** Line 969: reduce VPA's three components to
one clause or move to a Closer Look. Line 955: drop the 15-second sync interval, keep the
"runs intermittently, not continuous" characterization and the DaemonSet exclusion — both
of which are real exam surface. Q18's D-rationale (line ~1612) then needs the interval
reference softened to "runs intermittently."

**5 — Cap the maturity-level claims, or reconcile them explicitly.** Eleven projects
currently receive a CNCF level against the outline's cap of six. Either drop the levels from
Istio/Linkerd (line 730), Knative (843) and KEDA (1023) — each reads fine without the
adjective — or add half a clause at line 258 acknowledging that the chapter will name a few
more levels in passing and that the instruction not to memorize the roster still stands.
Recommend the former; it costs four words.

**6 — Add the missing G14 pointer.** One cross-bearing to `Ch 3 §1` for Kubernetes' origin,
in §2's institutional paragraph (around line 213) or §8's opening. The outline asked for a
pointer rather than a restatement; the restatement was correctly avoided and the pointer was
dropped with it.

**7 — Record the G32 decision instead of leaving it silent.** Add an AUTHOR-REVIEW comment
near §2's Landscape subsection stating that FinOps/OpenCost/Kubecost are deliberately out of
scope for this chapter, that `opencost-overview-2026-08-23.md` is available if the author
reverses it, and that D4's sub-objectives are unenumerated in the corpus (G33), so the call
is a judgment rather than a sourced exclusion. The natural minimal home if reversed is one
ungraded clause beside the Landscape's Observability and Analysis category.

**8 — Reduce the Archived treatment to its sanctioned budget.** Keep the figure annotation
(fig05) and one clause naming Archived as the terminal state; the paragraph at line 265 plus
three graded appearances (TYB 1 Q2 D, Practice Q4 D, Chapter Summary) is more reinforcement
than a non-rung warrants. Retaining one distractor is fine; retaining three teaches it as a
level.

### Out of scope — forwarded to other stages

- **Attention Budget total.** Line 13 says "~95 minutes"; the rows sum to 118. The missing 23 minutes are §8 + TYB 3 + §9. Structural/consistency stage, but noted here because the omission falls on the D4.3 section.
- **"One fact stated twice" vs "one fact stated three ways."** The §8 Fixed Point (line ~1155) says *twice*; the Chapter Summary (line 1640) says *three ways*. Consistency stage.
- **Outline OQ1**, the `chapter-03:350` pointer that sends governance-seeking readers to §1 — a shipped-text edit, not resolvable from inside Ch 17. Still open.
```

**Verdict in one line:** section-level objective coverage is complete and all five blocking research gaps closed, but **D4.3 is under-assessed** — §8 carries one practice item against a planned three, putting the competency B1 named as most under-studied at 19% of items instead of 28.6% — while §4 and §5 each carry a surplus item that duplicates a distractor rationale already present. Fix 1 corrects the allocation, the retrieval-ceiling breach, and the redundancy in a single edit.
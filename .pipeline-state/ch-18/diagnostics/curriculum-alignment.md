# Curriculum-Alignment Audit — KCNA Chapter 18

**Draft audited:** `.pipeline-state/ch-18/draft-v1.md` (1449 lines). Line citations are against that file.
**Objective authority:** `lf-kcna-program-changes-2026-08-23.md` — the only cached source that states the current blueprint.

## Authority and granularity — read before using this report

The cached blueprint gives **domain weights and competency names only**. It publishes no numbered sub-objectives and no per-competency weights. The IDs used below (`D4.1`, `D2.3`) are **book-internal**, derived from ordinal position in the LF announcement's competency lists; the Linux Foundation does not number them. Two consequences:

- This audit can verify coverage at **competency granularity**, not against a bulleted objective list. No such list is cached (B1 gap G33; LFS250 syllabus gap G37 unfetched). Anything finer is inference, and is labelled as such.
- ID resolution is confirmed, not assumed: `k8s-docs-logging-architecture-2026-08-23.md` tags itself `"D2 Troubleshooting"` and its 08-31 successor tags the same page `"D2.3"`. **D2.3 = Container Orchestration → Troubleshooting.** By the same list order, **D4.1 = Cloud Native Architecture → Observability.**

The draft never prints an objective ID to the reader (verified). Correct — these IDs are not LF's and must not ship.

---

## Objectives the outline claims to cover

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D4.1 | Cloud Native Architecture → **Observability** (domain published at 12%; competency weight unpublished) | **YES** — all 8 sections | appropriate |
| D2.3 | Container Orchestration → **Troubleshooting** (secondary "seam" tag on §3 and §6; owned by Ch 13) | partial — **by design** | shallow — appropriate |

D2.3's partial status is intended, not a gap: the outline dual-tagged §3/§6 as an honest record that they extend Ch 13 rather than open new territory. The draft honours that — §3 explicitly declines to re-teach the resource metrics pipeline (L354–L378) and §6 routes the `kubectl logs` limits back through Ch 13 §3/§4 cross-bearings. No re-teaching found.

### D4.1 coverage by concept cluster

All 47 terms in the outline's `kb_tags.concepts` resolve to draft text. Grouped:

| Cluster | § | Covered? | Depth |
|---|---|---|---|
| Observability vs monitoring; known/unknown unknowns | §1 | YES | appropriate — deepest treatment, and it is the chapter's spine |
| Instrumentation, telemetry, code-based vs zero-code | §1, §5 | YES | appropriate |
| OTel four signals + baggage + Collector | §2 | YES | appropriate |
| Metrics data model — time series, labels, cardinality | §3 | YES | appropriate (cardinality correctly non-graded) |
| Utilization relative to requests | §3 | YES | appropriate — paid off from the failure case, as the outline asked |
| metrics-server vs monitoring-system boundary | §3 | YES | appropriate |
| Prometheus — pull, scrape, SD, exporters, client libs, Pushgateway, PromQL, Alertmanager, Grafana | §4 | YES | appropriate; two local over-runs (below) |
| Distributed tracing — span, root span, IDs, context propagation, Jaeger | §5 | YES | appropriate; **Jaeger under-cited** (below) |
| Cluster logging — architectures, node agent, sidecar, rotation, Fluentd/Fluent Bit | §6 | YES | appropriate; **untagged**, two over-runs (below) |
| Reliability vocabulary — SLI/SLO/SLA, error budget, golden signals, RED/USE | §7 | YES | appropriate; error budget over-run (below) |
| Synthesis | §8 | n/a — introduces nothing, as planned | OK |

**Assessment allocation matches the outline exactly.** Practice distribution §1:2 / §2:2 / §3:3 / §4:4 / §5:2 / §6:2 / §7:2 = 17, identical to the plan. Bearings 3×5 = 15; retrieval 4/15 = 26.7% from Ch 5, 6, 10, 17. Practice retrieval 4/17 from Ch 5, 6, 13, 17. Soundings 8. Total 40, matching `question_budget`. Seven figures present, plus `ch13-fig04` retrieved by reference in §3 rather than redrawn. The 12%-not-5% metadata ruling is honoured (L4), and 5% is never presented as CNCF data.

---

## Objectives covered in the draft but NOT in the outline

**1. D4.2 — Cloud Native Architecture → Cloud Native Ecosystem and Principles (three touches, untagged).**
- L465–L556 §4: "Prometheus joined the CNCF in 2016 as the second hosted project" (authorized by the outline as trap #96).
- L557 §4: the Grafana / Loki / Tempo CNCF-membership Snag.
- L854 §6: Fluentd's CNCF acceptance and graduation, plus the maturity-levels Snag cross-beared to Ch 17 §2.

Each is individually authorized, and D4.2 is owned by Ch 17 — so this is not scope creep in substance. But the outline dual-tagged §3/§6 with D2.3 for exactly this "these are seams" reason, and the same honesty is not applied here. **Recommend adding `D4.2` as a secondary objective on §4 and §6**, so the question-writing and reconciliation stages can see that these items are legitimately interleaved rather than off-domain.

**2. Loki and Tempo (L557, L1142).** No objective, no ledger owner, no glossary entry. Present in one non-graded clause plus one trap-table clause — within Open Question #5's authorized fallback, and no item depends on them. No action needed on scope; see the sourcing finding below on how the clause is phrased.

**3. Fluent Bit's six-stage plugin pipeline (L860–L869).** In the outline ("one table, not a section") and delivered as exactly one table — so not outline drift. But see depth mismatches: this is deployment-level internals with no trap, no graded item, and no blueprint anchor.

**4. W3C TraceContext (§5) and the baggage security caution (§2 Closer Look).** Both outside exam surface by their own snapshots' notes; both named once, explicitly de-scoped in the prose ("You do not need the header format for this exam"; "Not exam surface"), both ungraded. **Compliant — no action.**

**5. Retrieval interleaving into D1/D2 objectives** (Ch 5 requests, Ch 6 DaemonSets, Ch 13 metrics-server, Ch 17 mesh/microservices). By design under B3's 25% ceiling, tagged inline in house form. **Not drift.**

---

## Depth mismatches

Per-competency exam weights are **not published** (G33). The proxy used below is B1's sourced-trap inventory plus graded-slot allocation, which is what the outline itself used.

| Objective / topic | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| D4.1 overall | D4 = 12% published; ~5% authored chapter share | 8 sections, 7 figures, 40 questions | **OK** — proportionate to an average chapter share |
| Prometheus (§4) | 4 of 10 sourced traps; 4 of 17 practice items | longest section | **OK** — the density is earned |
| Prometheus `target` / `endpoint` vocabulary (L465) | source snapshot calls target/endpoint/job/instance "scope creep for KCNA… do not teach the four as vocabulary" | two of the four bolded as defined terms | **over-covered** — and `**endpoint**` collides with the Kubernetes `Endpoints` object owned in the Services material (Ch 9, cross-beared two lines earlier) |
| Fluent Bit six-stage pipeline (L860–869) | no trap, no graded item, not named in the blueprint | 6-row table | **over-covered** — reads as memorizable structure the exam does not test |
| Fluentd footprint + plugin count (L854, L858) | snapshot guardrail: "detail, not surface. **One clause at most**" | ~3 clauses across two paragraphs (500+ plugins, 30–40MB, plus gloss) | **mildly over-covered** |
| Error budgets (§7, L911–917) | outline: "one glossed clause… keep it ungraded" | own `###` heading, 3 paragraphs, ~140 words, and a Q16 distractor | **over-covered** — the passage closes by calling itself "one clause and no more" while being three paragraphs |
| Container-log rotation defaults (L780, L1010) | kubelet configuration values; administration-level detail | stated in prose **and** required by a checkpoint model answer | **over-covered** — a model answer that names `containerLogMaxSize` 10Mi / `containerLogMaxFiles` 5 sets a memorization bar for config values |
| Jaeger (§5, L673) | named CNCF tracing backend; plausible D4.1 surface | 2 sentences, untagged, **ungraded** | **under-covered — and the stated reason is false** (see gaps) |
| Cost management / FinOps (OpenCost) | unresolved; no cached authority places it under D4.1 | absent, and **not flagged in-draft** | **under-covered — author decision required, last chance** |
| D2.3 (§3, §6) | owned by Ch 13 | extension only | **OK** — intended |

**On the FinOps decision.** `opencost-overview-2026-08-23.md` tags itself `D4 Cloud Native Ecosystem and Principles` — i.e. D4.2, Ch 17's competency, not D4.1. So its absence is **not** a Ch 18 objective failure, and the outline's recommendation to keep it omitted is defensible. What makes it worth raising at this gate rather than passing over: **Ch 18 is the last content chapter**, so the book ships with zero FinOps coverage once this gate clears, and the retired KCNA blueprint grouped cost management with observability closely enough that a candidate may reasonably expect it. The outline asked for the decision to be "visible in both chapters rather than silent in one" — Ch 17 carries an AUTHOR-REVIEW; **Ch 18 carries none**. That is the gap to close, not the coverage.

**Not in this stage's lane, reported because no later stage owns them.** Three internal count claims are arithmetically wrong and all three misdirect study time relative to exam surface:
- **L11** declares "Total time: ~85 minutes"; the Attention Budget rows sum to **123**.
- **L34** says §2 and §7 "carry four of this chapter's six high-priority exam topics." They carry **two** (four signals; SLI vs SLO). The section choice is defensible for a 16-minute triage; only the count is wrong.
- **L84** says §4 and §7 "carry six of this chapter's ten sourced traps." Against B1's ten, they carry **five**; against the draft's own 12-row Exam Alert table, six. The numerator and denominator come from different sets.
- **L449** "Four sections to go" — five remain; L764 and L1046 both correctly say "content sections."

---

## Gaps the research stage flagged

The research manifest (`research-manifest.md` L46–57) records three open gaps plus two carried forward. Handling in the draft:

| Gap | Draft handling | Verdict |
|---|---|---|
| **G-18a** — retired KCNA domain weights unextractable | §1 declines to restate the 8% figure and points at Ch 1 (L108–112) | **Correct.** The Ch 1 internal disagreement stays open at book level, as Open Question #6 routes it |
| **G-18c** — Collector receiver/processor/exporter not captured verbatim | §2 uses only "receive, process and export"; AUTHOR-REVIEW names the gap (L311) | **Correct** |
| **G-18b** — "Grafana is not a CNCF project" is an unsourceable negative | **Not honoured.** L557 asserts the flat negative in bold, and L1142 repeats it in the Exam Alert trap table. Manifest Note #4 supplied the safe framing (assert the positive; let the reader draw the negative) and it was not used | **NOT handled** |
| RED tier-4 authority | Named, contrasted, **ungraded**; Q17's RED/USE distractors are rejectable without knowing either method; AUTHOR-REVIEW records the caveat (L986) | **Correct.** G21 should be recorded substantially-but-not-fully closed |
| Loki / Tempo unowned | One non-graded clause; no item depends on them | **Correct on scope**, but the clause inherits the G-18b problem above |
| **G32** — FinOps / OpenCost unassigned | Omitted, consistent with Ch 17 — but with **no AUTHOR-REVIEW recorded** | **Partially handled** |
| Trap #99 — no item graded on current CNCF maturity level | Verified across all 40 items. Q15-A turns on CNCF *membership*, not maturity; L874's Snag explicitly warns the roster moves | **Correct** |

### Two gaps the draft asserts that do not exist

These are the two highest-value findings in this audit, and both were verified against the corpus rather than inferred.

**1. §6's foundational block is untagged, and every claim in it is already sourced.**
Lines L772, L780, L782, L784, L840, L844, L846 state — in the book's own voice, with no `[source:]` marker — that Kubernetes provides no native log storage, the rotation defaults, one-restart retention, eviction-destroys-logs, and the three cluster-logging architectures. This is the only untagged block of its size in an otherwise meticulously cited chapter, **and it is graded** (Checkpoint 3 Q1 at L1010 and Q2; Practice Q14's premise).

`k8s-docs-logging-architecture-2026-08-23.md` is in the corpus and carries **all of it**, including `containerLogMaxSize (default 10Mi)`, `containerLogMaxFiles (default 5)`, "only the latest log file's contents are available," "if a container restarts, the kubelet keeps one terminated container with its logs," "if a pod is evicted… all corresponding containers are also evicted, along with their logs," and the three-architecture list. This is a **citation failure, not a research gap** — nothing needs fetching.

Contributing cause worth fixing upstream: `k8s-docs-logging-architecture-2026-08-31.md` is **truncated at 25 lines** and its `supersedes_note` falsely claims it "carries the log-rotation defaults and the 'only the latest log file' note, both new." It carries neither. A drafting stage reading that frontmatter would conclude the material was sourced without finding the quotes.

**2. The draft declares a Jaeger research gap that is not real.**
The AUTHOR-REVIEW at L675 states: "no cached snapshot for Jaeger — the corpus has no jaegertracing.io capture." **`jaeger-overview-2026-08-23.md` exists**, sourced to `jaegertracing.io/docs/latest/`, authority "Jaeger project (CNCF graduated)," tagged `D4 Observability`. It supports every claim §5 makes at L673 and then some: the tracing backend "that receives tracing telemetry data and provides processing, aggregation, data mining, and visualizations"; "originally designed to support the OpenTracing standard"; "OpenTelemetry compatible; terminology and concepts map directly between the two data models"; and the exact OTel-instruments/Jaeger-receives division §5 and §8 both lean on. The research manifest's Gaps section does not list Jaeger — consistent with the snapshot being present all along.

The consequence is real under-coverage: because the draft believed Jaeger unsourced, it deliberately kept the treatment to two sentences and **routed no graded item to it**, leaving a named CNCF observability project ungraded in the chapter that owns Observability.

---

## Recommended fixes

Ordered by severity. Fixes 1–2 are ship-blocking for the gate; the rest are revision-stage work.

**1. §6 (L772–L846) — tag the cluster-logging block against `k8s-docs-logging-architecture-2026-08-23`.** Every claim is supported there. Use the 08-23 file, **not** the 08-31 one, which is truncated and does not contain the rotation defaults despite its frontmatter. Separately, correct that `supersedes_note` so a later stage does not cite the wrong file.

**2. §5 (L673–L675) — cite Jaeger and delete the false gap notice.** Tag the paragraph `[source: jaeger-overview-2026-08-23]`. Then either (a) leave the treatment at two sentences and record the citation-only change, or (b) since Jaeger is now sourced at CNCF-graduated authority, route one Practice item to "what is Jaeger, and what is OTel's relationship to it" — the OTel-exports / Jaeger-receives division is already the shape §8 pays off. **If (b), the item must not grade Jaeger's maturity level** (trap #99).

**3. §4 (L557) and Exam Alert (L1142) — restate the Grafana Snag per manifest Note #4.** Replace the asserted negative with the positive: Grafana is Grafana Labs' open-source product; the other projects in the paragraph — Prometheus, OpenTelemetry, Jaeger, Fluentd — each have a sourced CNCF status in the corpus. Let the contrast do the work. Same edit applies to the trap-table row, which currently asserts the negative for Loki and Tempo as well.

**4. §7 (L911–L917) — trim error budgets to the outline's one clause.** Drop the `###` heading and fold the passage under the SLO subsection; a standalone heading signals more exam weight than an ungraded, off-blueprint topic carries. Keep the velocity-vs-reliability tension and the "as long as there is error budget remaining — new releases can be pushed" quote. **Cut the reconstructed arithmetic at L913** ("If your SLO is 99.9%, then 0.1%…") — the source snapshot's guardrail explicitly forbids reconstructing the difference framing, because its antecedent was not captured.

**5. Q16-D (L1387) — remove the source tag from the derived number.** "the error budget would be the 0.05% of allowed failure derived *from* this objective [source: sre-book-error-budgets-2026-08-31]" attributes arithmetic the snapshot does not contain. Either drop the tag and the figure, or restate as "the allowance of failure derived from this objective, not the objective itself."

**6. §4 (L465) — demote `endpoint`.** Unbold it and fold it into the target sentence, or cut it. The source snapshot rates target/endpoint/job/instance as KCNA scope creep, and bolding `**endpoint**` with a Prometheus meaning two lines after a Ch 9 cross-bearing risks colliding with the Kubernetes `Endpoints` object. Keep `**target**` — the §4 figure depends on it. Verify against Ch 9's term ownership before landing.

**7. §6 (L860–L869) — cut the Fluent Bit pipeline table to one sentence,** or demote it to a 🔭 Closer Look so its non-surface status is visible. Nothing grades the six stages, and the chapter already carries three tables in §6's vicinity. While there, trim the Fluentd footprint material (L854, L858) toward the snapshot's "one clause at most" — the 500+ plugin count can go; the 30–40MB figure is the one that earns its place, because it is the sourced answer to "why are there two of these."

**8. Checkpoint 3 Q1 model answer (L1010) — drop the numeric defaults.** Keep "the kubelet rotates container logs, and only the latest log file is available through `kubectl logs`" as the graded mechanism. Leave 10Mi/5 in the §6 prose once it is tagged; do not require them in an answer.

**9. Frontmatter — add `D4.2` as a secondary objective on §4 and §6,** mirroring the D2.3 treatment on §3/§6, so the three ecosystem touches are recorded as seams rather than reading as untagged drift.

**10. §6 — add an AUTHOR-REVIEW recording the G32 / FinOps omission,** naming Ch 17's parallel note and stating that Ch 18 is the last content chapter, so the omission is now the book's final answer. The outline asked for this decision to be visible in both chapters; right now it is visible in one.

**11. Numeric-consistency sweep — four edits, one class of defect:**
- L11 — reconcile "~85 minutes" with the table's 123, in whichever direction the author prefers.
- L34 — "four of this chapter's six high-priority exam topics" → **two**. (Optionally strengthen: §2 and §7 also carry three of the twelve listed traps.)
- L84 — "six of this chapter's ten sourced traps" → "six of this chapter's twelve listed traps," matching the draft's own Exam Alert table.
- L449 — "Four sections to go" → "Four content sections to go," matching L764 and L1046.
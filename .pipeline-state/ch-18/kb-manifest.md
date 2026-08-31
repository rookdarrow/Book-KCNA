I read the existing KB tree, the binding scaffolding, and the source corpus before writing, and three of my checks changed the picture. Leading with those.

---

# Knowledge-Base Manifest — KCNA Chapter 18

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice, re-verified this run.** `Book-KCNA/knowledge-base/` **still does not exist on disk.** Seventeen manifests exist (`ch-01`…`ch-17`); none has been applied. Chapter 18 adds the eighteenth and last for a content chapter.
>
> **Ordering contract, inherited from Ch 12–17.** **APPEND** for the three shared registers and for every shard that already exists; **WRITE** only for slugs that collide with nothing. I enumerated every `concepts/*.md` slug emitted in a `WRITE`/`APPEND` block across `ch-01`–`ch-17` (196 blocks, 176 distinct slugs) and checked each proposed Ch 18 slug against it. **Three collisions found and deliberately not created** — see ⚑ C5.

---

## ⚑ Findings that change what downstream stages should do

### ⚑ C0. CRITICAL — Chapter 16's ⚑ I0 truncation fault **does extend past Ch 16's batch**, and Chapter 18's corpus contains an instance

Ch 16's manifest found eleven `2026-08-31` snapshots truncated at their first code fence with frontmatter asserting completeness, and asked later stages to check chapters 08–15. Ch 17 measured 22 of its own captures and found none, and concluded the fault "was confined to Ch 16's twelve-page debug batch, not a shared code path."

I measured eleven of Ch 18's load-bearing `2026-08-31` captures. Ten are healthy (39–63 lines, each ending in the researcher's own drafting-note prose). **One is not:**

`sources/k8s-docs-logging-architecture-2026-08-31.md` — **24 lines.** Its body stops at:

```
> "To fetch the logs, use the `kubectl logs` command, as follows:"
```

which is the sentence that introduces a code block on the live page. That is the ⚑ I0 signature exactly. And its frontmatter asserts the opposite:

```yaml
supersedes_note: "Fuller than k8s-docs-logging-architecture-2026-08-23.md (2.9KB).
  Carries the log-rotation defaults and the 'only the latest log file' note, both new."
```

**Neither the rotation defaults nor the "only the latest log file" note is in the file.** Both are in the *older*, prose-summarised `-2026-08-23` capture (line 13), which is the one Chapter 18 §6 actually cites — fourteen times, correctly.

Three things follow, and none of them is a Chapter 18 defect:

1. **Ch 18 is safe.** Every §6 claim resting on rotation, restart depth or eviction is tagged to `-2026-08-23`. Verified line by line.
2. **Ch 13 is safe.** It cites `-2026-08-31` three times (`ch13:663`, `:1352`, `:1436`), and all three quotes survive above the truncation point. Verified.
3. **The frontmatter must be corrected or the page re-fetched.** A future stage reading `supersedes_note` will re-point citations at the thinner file and silently lose the two facts §6 is built on. Ch 18's own fact-accuracy diagnostic noticed the file was thinner; it did not identify it as the I0 signature, so the corpus-level implication was not recorded anywhere until now.

**Revise ⚑ I0's scope:** the fault is not confined to Ch 16's batch. It reached at least one snapshot fetched during Ch 13's research run. Chapters 08–12 and 14–15 still need the check.

### ⚑ C1. The integration report's finding 4 asks for a register row that already exists

Integration finding 4 says of SRE: *"Add the register row and a glossary entry."* **The register row is already there** — `term-ownership.md:715`:

```
| SRE | Site Reliability Engineering | glossary-only — see **Orphans** |
```

with a full orphan ruling at `:817–821`: *"The provenance of SLIs, SLOs, error budgets, and the golden signals, but not itself an exam object… Not eligible for graded text."*

So only two of the three actions are outstanding: **the in-text expansion, and the glossary entry.** One refinement to where the expansion goes, which I verified rather than assumed: SRE occurs exactly twice in the chapter, at `L139` and `L928`. **L928 is inside a verbatim quotation** from `sre-book-error-budgets-2026-08-31` ("Meanwhile, SRE performance is evaluated based upon reliability of a service…"), which cannot be altered. **L139 is the only place the book uses the acronym in its own voice**, and it precedes L928. The expansion lands there and covers both:

> Google's own **Site Reliability Engineering (SRE)** text lists four reasons to monitor…

The ledger's "not eligible for graded text" ruling is honored: zero occurrences in any Soundings, Bearings or Practice item. Confirmed.

### ⚑ C2. CONFIRMED — the blocking ethical-guardrail finding, with the exact shipped form to copy

`draft-v2.md:1155` reads verbatim:

> `**Common Traps** — each of these has cost real candidates real points:`

I checked all eight shipped chapters that carry a Common Traps block. **No other chapter claims candidate scoring outcomes.** Two shipped forms are available:

- **Ch 15 (`:1404`), the conservative fix, and the one integration proposes** — note it ends in a period, not a colon:
  > `**Common Traps** — these are distinctions that are easy to confuse, and they are the ones this material rewards getting right.`
- **Ch 11 (`:1397`), which Ch 18 is also entitled to** — because all eleven of its traps are `[source]`-tagged in B1, unlike the frequency claim:
  > `**Common Traps** — these are documented targets in this book's domain analysis, not merely things that are easy to confuse:`

Either discharges guardrail #8. Ch 11's is the stronger sentence and is defensible here; Ch 15's is the safer default. Author's pick.

### ⚑ C3. CONFIRMED — `p99` reaches a graded question stem undefined

Verified: `95th-percentile` is glossed in prose at `L328`; the `pNN` notation first appears at `L370` (a §3 table row) and then at **`L386`, the Bearings Checkpoint 1 Q1 stem**. The ledger's standard is absolute — *"a term used in question text or an answer key may not be glossary-only."* The item is not answer-blocking (the dashboard list is scenery), but there is no lookup path. Cheapest fix is integration's: pair the forms at `L370`.

### ⚑ C4. CONFIRMED, with the placement the register dictates

`OTel` is never paired with `OpenTelemetry`. Its first reader-visible occurrence is `L302`, inside the §2 figure (`│  OTel COLLECTOR       │`); `L312` is an AUTHOR-REVIEW comment and invisible to the reader. The acronym register (`:691`) assigns `OTel` to **Ch 18 §2**, so the pairing belongs in §2's Collector paragraph *before* the figure, not in §1.

### ⚑ C5. Three slug collisions, all declined — Chapter 18's version of Ch 17's ⚑ C7

The outline's `kb_tags.concepts` names `cluster-logging-architecture`, `node-level-logging-agent` and `log-rotation`. Chapter 13 already sharded this territory:

- **`cluster-level-logging.md`** (ch-13) — the concept's existing home
- **`reading-container-logs.md`** (ch-13) — `kubectl logs` and its bounds

Creating `cluster-logging-architecture.md` beside `cluster-level-logging.md` would reproduce, at the chapter that *owns* the material, exactly the `pluggable-interface-pattern` / `pluggable-interfaces` split that has now cost three manifests a flag. **Chapter 18 appends to both ch-13 shards and creates neither new slug.** `log-rotation` folds into the `reading-container-logs.md` append.

Same ruling for §8's separability pattern: **no `producer-backend-separability.md`.** Its four instances append to `pluggable-interface-pattern.md` (the ch-02 original) and to `one-pluggability-story.md` (ch-17). **`pluggable-interfaces.md` gets no append** — ⚑ I2's merge-to-stub still stands, and this is the last content chapter that could have entrenched it further.

### ⚑ C6. `statefulset.md` still does not exist, and Chapter 18 grades against it

Ch 16 flagged that no `statefulset.md` shard exists anywhere in the tree, because `ch-06/kb-manifest.md` is a lean early run that sharded only `custom-resource.md` and `operator-pattern.md`. Re-verified this run: still absent. **Chapter 18 Practice Q14 option B grades StatefulSet ordinal identity as a distractor** and cross-bears to Ch 6 §6 to justify it. Ch 18 is the last content chapter that can flag this before Ch 19 reads the index and concludes the workload set is covered. **Create `statefulset.md` from shipped Ch 6 §6 at the replay.**

### ⚑ C7. The metadata-line ambiguity is real, and Ch 16 already shipped the fix

Integration finding 7 is correct and the outline corroborates it: `ch-18/outline.md:267` binds the metadata line to **12%, not 5%** ("This is the third chapter in a row to make this ruling and the first two shipped honoring it"). But Ch 17 displays 12% too, for a domain worth 12% in total, and two adjacent chapters showing the same figure reads as though either carries the whole domain. Ch 16's shipped form disambiguates *and* restores the `[source:]` tag that Ch 17 and Ch 18 both dropped:

```
**Domain Weight: 12% (Cloud Native Architecture) [source: cncf-kcna-curriculum-pdf-2026-08-23]
| Competency: Observability | Authored allocation for this chapter: ~5%**
```

### ⚑ C8. B7 ledger obligations — all discharged, verified against the ledger text

- **SLA orphan (`:805–809`) closed.** The ledger required Ch 18 §7 own it "as a one-clause contrast" and explicitly *not* glossary-only, because it serves as a distractor in Ch 18 and Ch 20 answer keys. §7 defines it with a sourced definition plus the "what happens if the SLOs aren't met?" procedure, and Practice Q16 option A uses it as the distractor. Fully resolved.
- **SRE orphan (`:817–821`) honored** — see ⚑ C1.
- **The `label` homonym rule (`:870`) honored.** Sense B is "metric label" at first use and in every sentence where a Kubernetes object is also present.
- **The `request` homonym rule (`:871`) honored.** §3 writes "resource request" in full at the denominator.
- **Trap #99 honored.** No graded item depends on a project's current CNCF maturity level; §6's Fluentd status carries the moving-roster caveat instead.

### ⚑ C9. The integration report's glossary count does not reconcile

Its summary says *"5 terms require glossary/register entries (2 of which surface in graded text)"*; its table lists **four** (SRE, `p99`, W3C TraceContext, OpenTracing). Of those four, only `p99` surfaces in graded text — SRE is prose-only in both occurrences (⚑ C1), and W3C TraceContext and OpenTracing each appear once, ungraded. So the parenthetical is also off by one. I verified the remaining candidates rather than guessing at a fifth: `metrics.k8s.io` is introduced in shipped Ch 13, and Treasure Data / HAProxy / StatsD / Graphite / PagerDuty / OpsGenie are proper nouns inside verbatim quotations. **Four is the right number.** No fifth term is missing.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

Two tiers, following Ch 11–17. Integration marked 4 terms as needing entries (⚑ C9); skill Part 16 requires every technical term the book introduces, so the **39 B7-owned Ch 18 rows** (`term-ownership.md:574–612`) are harvested alongside them, plus the eight acronym-register rows.

### Tier 1 — flagged, corrected, or carrying a guardrail

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **SRE (Site Reliability Engineering)** | Provenance of SLIs, SLOs, error budgets and the golden signals; not itself an exam object. ⚠ **Register row already exists at `term-ownership.md:715`** — only the in-text expansion at `L139` and this entry are outstanding (⚑ C1). Not eligible for graded text | Chapter 18 §1 |
| **`pNN` / p99** | ⚠ **Reaches a graded stem undefined** (Bearings 1 Q1, `L386`). Needs an **in-text gloss at `L370`**, not a glossary-only entry (⚑ C3). The 95th-percentile form is already glossed in prose at `L328` | Chapter 18 §3 |
| **W3C TraceContext** | The specification whose headers the default OpenTelemetry propagator uses `[source: opentelemetry-context-propagation-2026-08-31]`. ⚠ The snapshot's own guardrail: *"not exam surface at KCNA level. Name it at most once; do not grade it."* Chapter complies | Chapter 18 §5 |
| **OpenTracing** | The standard Jaeger "was originally designed to support" `[source: jaeger-overview-2026-08-23]`. Appears once, inside a quotation, ungraded | Chapter 18 §5 |
| **Observability** *(as a D4 competency)* | ⚑ Corrects Ch 17's carried note: the competency name is **"Observability,"** not "Cloud Native Observability" `[source: cncf-kcna-curriculum-pdf-2026-08-23]`. Chapter 18 uses the correct form throughout | Chapter 18 §1 |
| **Jaeger** | ⚑ **Deliberately ungraded.** No Soundings, Bearings or Practice item depends on it; the question budget closes exactly at 40 without it. Any future graded item must **not** grade its CNCF maturity level (trap #99) | Chapter 18 §5 |
| **RED method** | ⚑ **Tier-4 provenance.** Its only surviving authoritative source is a Grafana Labs post by Tom Wilkie, the method's originator; the original Weaveworks publication is dead and the CNCF whitepaper's link points at the dead host. Named and contrasted, carries no teaching weight, grades nothing. **B1 gap G21 is substantially-but-not-fully closed** | Chapter 18 §7 |
| **Grafana** | *"open source software that enables you to query, visualize, alert on, and explore your metrics, logs, and traces wherever they're stored"* `[source: grafana-introduction-2026-08-23]`. ⚠ **Gap G-18b:** its non-CNCF status is a negative and cannot be sourced. §4 gets its point by contrast with two projects whose own docs state a donation — never by asserting the negative | Chapter 18 §4 |

### Tier 2 — the 39 B7-owned Ch 18 rows, harvested per skill Part 16

observability · monitoring · known unknowns vs unknown unknowns · instrumentation · telemetry · health checking ≠ observability · OpenTelemetry / OTel · signal (the OTel sense) · trace · metric · log · **baggage** · OTel Collector · time series · sample · **metric label** · cardinality · utilization relative to requests · metrics-server vs a monitoring system · Prometheus · pull / scrape model · target · service discovery (Prometheus sense) · exporter · client library · Pushgateway · PromQL · Alertmanager · Grafana · distributed tracing · span · root span · trace ID · span ID · context propagation · Jaeger · zero-code vs code-based instrumentation · node-level logging agent · Fluentd · Fluent Bit · sidecar logging pattern · log rotation · reliability · SLI · SLO · SLA · error budget · the four golden signals · RED method · USE method.

**Acronym-register rows to enter** (`term-ownership.md:691–721`): OTel · PromQL · RED · SLA · SLI · SLO · SRE · USE.

---

## Concept shards at `Book-KCNA/knowledge-base/concepts/{slug}.md`

**Twenty-five created**, mapping the outline's 46 `kb_tags.concepts` with eight consolidations (where the discrimination *is* the content, per the `oomkilled-vs-evicted.md` / `tag-vs-digest.md` precedent) and **three deliberate non-creations** (⚑ C5).

| Slug | § | Note |
|---|---|---|
| `observability-vs-monitoring.md` | §1 | ★ **absorbs `unknown-unknowns`** — the discrimination is the file |
| `instrumentation-and-telemetry.md` | §1 | ★ the "don't need to add more instrumentation" bar |
| `health-checking-is-not-observability.md` | §1 | named ledger row; the probe exclusion; graded at Bearings 1 Q3e |
| `opentelemetry-four-signals.md` | §2 | ★ **absorbs `signals`, `traces`, `metrics`, `logs`** at signal level; carries the three-authority conflict |
| `baggage.md` | §2 | own file — the most-dropped item and the §8 payoff |
| `otel-collector.md` | §2 | ⚑ carries the **G-18c** receiver/processor/exporter guardrail |
| `time-series-and-metric-labels.md` | §3 | **absorbs `cardinality`**; carries the `label` homonym rule |
| `utilization-relative-to-requests.md` | §3 | ★ graded twice (Q5, Q6); the undefined-not-zero proof |
| `metrics-server-vs-monitoring-system.md` | §3 | ⚠ the boundary the exam actually tests |
| `prometheus.md` | §4 | ★ **absorbs `pull-model`, `scraping`, `service-discovery`** |
| `prometheus-components.md` | §4 | **absorbs `exporters`, `client-libraries`, `alertmanager`** — the code-boundary discrimination |
| `pushgateway.md` | §4 | own file — the one exception, graded at Q9 and Bearings 2 Q1 |
| `promql-and-the-read-path.md` | §4 | **absorbs `promql`, `grafana`**; carries the **G-18b** guardrail |
| `prometheus-non-fit.md` | §4 | ⚠ the highest-yield trap in the chapter; graded at Q10 and Q11 |
| `distributed-tracing.md` | §5 | ★ **absorbs `span`, `root-span`** — the containment relationship |
| `context-propagation.md` | §5 | **absorbs `trace-id`**; carries the W3C TraceContext guardrail |
| `jaeger.md` | §5 | ⚑ records *why* it is ungraded, so a later stage does not "fix" it |
| `zero-code-vs-code-based-instrumentation.md` | §5 | the mesh limit; graded at Bearings 2 Q5 |
| `fluentd-and-fluent-bit.md` | §6 | **absorbs `fluentd`, `fluent-bit`**; carries trap #99 |
| `reliability-the-question.md` | §7 | the sentence §8 is built on; own file |
| `sli-slo-sla.md` | §7 | ★ **consolidated** — the discrimination procedure is the content |
| `error-budget.md` | §7 | the velocity/reliability referee |
| `four-golden-signals.md` | §7 | ★ **absorbs `four-golden-signals`**; saturation's leading indicator |
| `red-and-use-methods.md` | §7 | **consolidated**; ⚑ carries RED's tier-4 provenance |
| `one-question-four-instruments.md` | §8 | **the Zenith.** Own file, per `one-pluggability-story.md` precedent |

**Not created — ⚑ C5.** `cluster-logging-architecture.md`, `node-level-logging-agent.md`, `producer-backend-separability.md`.

**Sixteen amended by append.** `cluster-level-logging.md` ⚑⚑ · `reading-container-logs.md` ⚑⚑ · `resource-metrics-pipeline.md` · `absent-component-pattern.md` ⚑ · `probe.md` · `resource-request.md` · `label-selector.md` · `service-mesh.md` · `oomkilled-vs-evicted.md` · `pluggable-interface-pattern.md` ⚑ · `one-pluggability-story.md` · `blueprint-change-2025-11-24.md` · `domain-weights-44-28-16-12.md` · `cncf-project-maturity-levels.md` · `factor-xi-logs-as-event-streams.md` · `control-loop-pointed-at-a-repository.md` ⚑.

**⚑ DO NOT APPEND: `pluggable-interfaces.md`** (ch-11). Merge to a stub at the replay.

Not shard-worthy, adequately carried by the glossary: sample · target · sidecar logging pattern · log rotation · W3C TraceContext · OpenTracing · Treasure Data · Alertmanager receivers.

---

## Infrastructure flags — the knowledge base itself

**⚑ I0 — CRITICAL, scope revised upward. See ⚑ C0.** The snapshot truncation is **not** confined to Ch 16's batch. `k8s-docs-logging-architecture-2026-08-31.md`, fetched during Ch 13's research run, is truncated at its first code fence with a `supersedes_note` asserting it carries facts it does not. Ch 13 and Ch 18 are both verified safe. **Correct the frontmatter or re-fetch, and check chapters 08–12 and 14–15.**

**⚑ I1 — HIGH, unchanged, now eighteen chapters expensive.** Re-verified by enumeration this run. `ch-01` emits **WRITE** for all three registers, which is correct — it creates them. `ch-03`, `ch-10` and `ch-11` also emit **WRITE**, which is destructive: replaying `ch-01`→`ch-18` in order discards everything written before each of those three points. `absent-component-pattern.md` is written as a full file twice (ch-03, ch-10). Additionally, **`ch-06` emits no `glossary.md` block at all** — only `objective-coverage.md` and `retrieval-log.md`. Chapter 18 adds only APPENDs. **Convert the three WRITE blocks to APPENDs before any replay.**

**⚑ I2 — MEDIUM, unchanged.** `pluggable-interface-pattern.md` (ch-02) and `pluggable-interfaces.md` (ch-11) remain one concept under two slugs. Chapter 18 appends to the former and declines the latter (⚑ C5). Merge at the replay.

**⚑ I3 — MEDIUM, unchanged, and now blocking Ch 19 directly.** `book-outline/retrieval-architecture.md` is **18 lines** of permissions-failure message plus the stage's own summary — verified again this run. Every B3 figure quoted below is recovered from that summary. Ch 19 is built by exactly the audit B3 was supposed to specify. **Re-run before Ch 19 drafts.**

**⚑ I6 — HIGH, unchanged from ch-16.** No `statefulset.md` exists anywhere in the tree, and Ch 18 grades against it (⚑ C6). Last content chapter to flag it.

**⚑ I7 — HIGH, unchanged from ch-17.** `ch-16/kb-manifest.md` describes 21 new shards and 16 appends and **emits exactly three blocks** — the shared registers. Re-counted this run: 3. Chapter 16's entire concept layer is documented but unwritten. **Re-emit before the replay.**

**⚑ I8 — LOW, unchanged.** `ch-15/kb-manifest.md:2605` contains a corrupt marker — `` === APPEND C:\dev\lodestar\cert``` `` — immediately followed by a correct duplicate at `:2606`. Re-verified. A naive parser will fail or write a garbage path. **Delete line 2605.**

**⚑ I10 — LOW, new.** `k8s-docs-logging-architecture-2026-08-23.md` carries `objectives_covered: ["D4 Observability", "D2 Troubleshooting"]` in the retired-blueprint's vocabulary — "D4 Observability" is no longer a domain. Its sibling `-2026-08-31` uses the current `["D2.3"]`. Retag the `-08-23` file to `["D4.1", "D2.3"]` so a search for D4.1 finds the capture the chapter actually depends on.

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Naming the limit of the thing you are about to teach** | "Here is the part most study guides will not say out loud: **you cannot dashboard your way out of a question you did not know to ask.** Every dashboard you have ever built is a set of answers to questions somebody chose in advance. That is genuinely useful. It is also, on the night that matters, beside the point: the thing that broke is the thing nobody drew a graph for." | **Strong candidate.** Opens a chapter by conceding what its own subject cannot do, before teaching any of it. Arousal and entropy from an admission rather than a hook. The catalog has nothing that establishes stakes by subtraction. |
| **A definition that indicts the reader's practice** | "Sit with that for a second. The bar is not 'we emit metrics.' The bar is: when something novel breaks, nobody has to ship a code change to find out what. **If your debugging procedure routinely begins with *let me add a log line and redeploy*, you have a monitoring system and an aspiration.**" | **Strong candidate.** Converts a sourced definition into a self-test the reader has already failed, without condescension. The closing clause is the brand's wry beat aimed squarely at the practitioner — skill v5.7 subject-dignity, executed. |
| **Reconciling authorities instead of picking one** | "Two authorities, three lists, and all of them correct about their own document. When a question names **OpenTelemetry**, it wants the four." | **Strong candidate.** Part 14's uncertainty-signalling guardrail as a single sentence. Refuses the false clean answer, prints the disagreement, and still leaves the reader with a decision procedure. Pairs with Ch 17's "what is each one for" ⚓. |
| **Building a section from the wall, not the vocabulary** | "Seven processes. All seven log correctly. All seven log *well* — structured JSON, accurate timestamps, sensible messages… And you cannot answer 'why did that request take four seconds.' Not because the data is missing. **Because nothing joins it.**" | **Strong candidate.** Generation effect (Part 10) at section scale — the reader feels the gap before meeting the word for it. The stipulation that everything is done *right* is what makes the failure structural rather than a competence story. |
| **The register used precisely enough to earn its keep** | "It is the oldest problem in navigation wearing new clothes: seven readings, and no way to fix a position from any of them, because a fix needs two lines drawn to the *same* landmark and nothing here agrees on what the landmark was." | **Strong candidate.** The maritime register carrying actual explanatory load rather than decoration — the cross-bearing convention's own mechanic used to explain why correlation IDs exist. Companion to Ch 17's "altitude is not a metaphor for importance." |
| **Closing a book's argument as a disposition, not a toolkit** | "This chapter is the payment, and it is not a set of tools. It is a *disposition*, the habit of asking, before an incident rather than during one, *what would I need to be emitting for this question to have an answer?* … **Nothing works in the other direction, which is why teams who start by buying a dashboard product are so often the ones who cannot explain their own outages.**" | **Strong candidate.** Last content chapter's closing move: identity transformation (Part 3) stated as a causal claim about practice rather than an exhortation. |
| **Two ecosystems converging, named as evidence** | "It turns out the observability ecosystem was built on the same conviction, by different people, for different reasons, arriving at the same architecture. **That is not a coincidence to file away as trivia. It is the reason both ecosystems are still standing.**" | **Moderate to strong.** Zenith synthesis that reaches across a chapter boundary and tells the reader what the pattern is *for*. Held at moderate only because it depends on shipped Ch 17 §4 to land. |
| **Dead Reckoning as a whole-chapter contract** | "> **Dead Reckoning:** Observability lets you understand a system from the outside by letting you ask questions about that system without knowing its inner workings… This chapter covers the four signals OpenTelemetry defines, the two dominant collection tools…, how logs get off a node, and the vocabulary for saying whether a service is behaving acceptably: SLI, SLO, and the four golden signals." | **Moderate.** A Dead Reckoning block doing double duty as the chapter's scope statement — every claim sourced, no metaphor, and the reader who wants only the map can stop there. Useful precedent for dense-vocabulary chapters. |

---

## Objective coverage log

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D4.1 — Observability** | **Chapter 18** | **deep — whole competency** | 2026-08-31 |
| D2.3 — Troubleshooting *(secondary, §3 and §6)* | Chapter 13 | reinforcement | 2026-08-31 |

**Domain 4 is now complete.** D4.1 here; D4.2 and D4.3 at Chapter 17. The curriculum's own ordering — *"Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration"* `[source: cncf-kcna-curriculum-pdf-2026-08-23]` — maps the split exactly.

**Unresolved and now unforwardable — AUTHOR-REVIEW `L567` item (1).** §4 and §6 each touch D4.2 (Prometheus's and Fluentd's CNCF status, and the project-maturity caveat), which Ch 17 owns. §3 and §6 already declare D2.3 as secondary for the same "these are seams" reason. **§4 and §6 should declare D4.2 the same way in frontmatter**, so question-writing and reconciliation read interleaving rather than untagged drift. Chapter 18 is the last content chapter; there is nowhere to defer this to.

**Frontmatter to write at materialisation** (confirmed here per integration item A, which correctly identifies the absent YAML block as normal pipeline behaviour rather than a regression):

- `chapter: 18` · `chapter_type: "content"` · `title: "Reading the Instruments"`
- `domain_weight_pct: 5` — **the authored allocation, not 12**, per Ch 17's frontmatter rule
- `objectives`: `["D4.1"]`, with `D2.3` and `D4.2` as secondary

---

## Retrieval-practice ledger

Seven tagged items, all verified against the shipped target chapter. Distribution 4/15 checkpoints (26.7%) and 3/17 practice (17.6%), combined 7/32 (21.9%) — inside skill Part 10's 20–25% band for Ch 6+, with Bearings at B3's ceiling.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| the absent-component pattern (`kubectl top` with no metrics-server) | ch 3 (phrase) · ch 10 §3 (named) | ch 18 Bearings 1 Q5 **[tagged]** |
| metrics-server scope vs Prometheus collection | ch 13 §7 | ch 18 Bearings 2 Q4 **[tagged]**, Practice Q7 **[tagged]** |
| mesh telemetry without code changes | ch 17 §5 | ch 18 Bearings 2 Q5 **[tagged]** |
| DaemonSet = one Pod per node | ch 6 §7 | ch 18 Bearings 3 Q5 **[tagged]**, Practice Q14 **[tagged]** |
| utilization undefined without a resource request | ch 5 §8 | ch 18 Practice Q6 **[tagged]** |

**Untagged retrieval carried by cross-bearing** — recorded so Ch 19's confusion-pair audit can see the real load, which is 15 of 40 items:

| Tested topic | Original chapter | Retested in |
|---|---|---|
| probes leave no record | ch 5 §7 | ch 18 Soundings Q1, §1, Bearings 1 Q3e |
| metrics-server keeps no history | ch 13 §7 | ch 18 Soundings Q2, §3 |
| `kubectl top` fails without its component | ch 13 §7 · 10 §3 | ch 18 Soundings Q3 |
| utilization relative to requests | ch 5 §8 · 17 §7 | ch 18 Soundings Q4, §3, Practice Q5 |
| log collection is a per-node job | ch 6 §7 · 13 §7 | ch 18 Soundings Q5, §6 |
| `kubectl logs` bounds — rotation, one-restart depth | ch 13 §3 | ch 18 Soundings Q6, §6, Bearings 3 Q1 |
| one request, many services | ch 17 §3 | ch 18 Soundings Q7, §5, §7 (RED's origin) |
| eviction destroys container logs | ch 13 §4 | ch 18 §6 |
| the scheduler does not place one-per-node | ch 7 §1 | ch 18 Bearings 3 Q5 |
| StatefulSet ordinal identity | ch 6 §6 | ch 18 Practice Q14 distractor — ⚑ **no shard exists**, see C6 |
| CRI is the kubelet↔runtime boundary | ch 2 §4 | ch 18 Practice Q8 distractor |
| etcd is the control plane's datastore | ch 3 §2 | ch 18 Practice Q11 distractor |
| ResourceQuota / LimitRange | ch 8 §3 | ch 18 Practice Q5, Q6 distractors |
| boundary, not implementation | ch 17 §4 | ch 18 §8 |
| CNCF maturity is a moving roster | ch 17 §2 | ch 18 §4, §6 |

**Correctly handled, not a defect.** draft-v1 carried 8 tags; v2 carries 7. The question-quality audit flagged v1's Practice Q13 `[retrieval: ch17]` as mis-tagged — *"'six microservices' is scenery, not a retrieval target"* — and prescribed dropping it while preserving the Bearings count by tagging the incoming §4 component item `[retrieval: ch13]`. The revision did exactly both, and the resulting drop in Practice density was anticipated by the audit. I checked this before recording it.

---

## Recommended actions, ranked

1. **Correct `k8s-docs-logging-architecture-2026-08-31.md` (⚑ C0)** — the `supersedes_note` asserts facts absent from the body, and ⚑ I0's scope was wrongly narrowed. Highest-consequence item here, because it misdirects future stages rather than any current chapter.
2. **Apply ⚑ C2** — one line, discharges the only failing ethical guardrail. Copy Ch 15's shipped form verbatim, or Ch 11's if the author prefers the stronger sentence.
3. **Gloss `p99` at `L370` (⚑ C3)** — it reaches a graded stem.
4. **Expand SRE at `L139` and write the glossary entry (⚑ C1)** — the register row is already there; do not add a second.
5. **Pair `OTel` with `OpenTelemetry` in §2 (⚑ C4)**, before the figure, per the register's ownership.
6. **Adopt Ch 16's metadata-line form (⚑ C7)** — disambiguates the twin 12% and restores the missing `[source:]` tag.
7. **Rule on AUTHOR-REVIEW `L567` item (2) at book level** — whether a cross-bearing to an audited chapter discharges the `[source:]` obligation for the seven Kubernetes claims. No new research either way, but no later chapter to defer to.
8. **Declare D4.2 secondary on §4 and §6** in frontmatter (item (1) of the same comment).
9. **Soften `L784` and `L1346`** — "worth more exam points than anything else" and "the majority of candidates" are unsupported quantifications of the same kind as ⚑ C2, one degree milder.
10. **Infrastructure, before any replay:** ⚑ I0 (corpus check for 08–12, 14–15), ⚑ I7 (re-emit Ch 16's shards), ⚑ I8 (delete `ch-15:2605`), ⚑ I1 (WRITE→APPEND ×3), ⚑ I2 (merge the duplicate slug), ⚑ I6 (create `statefulset.md`), ⚑ I3 (re-run B3 before Ch 19), ⚑ I10 (retag the logging snapshot).
11. **Still genuinely open, correctly:** G-18a / G33 retired blueprint weights; G-18b Grafana's non-membership as an unsourceable negative; G-18c the Collector's pipeline component names; G21 recorded as substantially-but-not-fully closed; G32 FinOps, whose omission is defensible on objective grounds and is now flagged in both Ch 17 and Ch 18 as the outline asked. §7's title capitalization is bound by B6 and is a cosmetic author call, not a defect.

---

Below are the write intentions. Registers first, then the sixteen shard appends, then the twenty-five new shards.

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

# Chapter 18 additions (2026-08-31)

## A

**Alertmanager** — Component that "takes in alerts, aggregates them into groups, de-duplicates, applies silences, throttles, and then sends out notifications" [source: prometheus-glossary-2026-08-31], routing "to the correct receiver integration such as email, PagerDuty, or OpsGenie" [source: prometheus-alertmanager-2026-08-31]. ⚠ It "handles alerts sent by client applications such as the Prometheus server" — so Prometheus PULLS from targets and PUSHES to Alertmanager. Not a contradiction of the pull model: collection and dispatch are different clauses. (Chapter 18 §4)

## B

**Baggage** — "contextual information that is passed between signals" [source: opentelemetry-signals-2026-08-23]; a key-value store letting you "propagate any data you like alongside context," whose purpose is to "include information typically available only at the start of a request further downstream" — account identification, user IDs, product IDs, origin IPs [source: opentelemetry-baggage-2026-08-31]. ★ The fourth OpenTelemetry signal, and the one candidates drop. It is NOT a span attribute: "baggage is a separate key-value store and is unassociated with attributes on spans, metrics, or logs without explicitly adding them" [source: opentelemetry-baggage-2026-08-31]. (Chapter 18 §2)

## C

**Cardinality (metric)** — "every unique combination of key-value label pairs represents a new time series, which can dramatically increase the amount of data stored" [source: prometheus-naming-labels-cardinality-2026-08-31]. Hence: "Do not use labels to store dimensions with high cardinality (many different label values), such as user IDs, email addresses, or other unbounded sets of values" [source: prometheus-naming-labels-cardinality-2026-08-31]. Not KCNA surface; the most common way real teams break their own metrics stack. (Chapter 18 §3)

**Client library (Prometheus)** — "a library in some language (e.g. Go, Java, Python, Ruby) that makes it easy to directly instrument your code" [source: prometheus-glossary-2026-08-31]. Goes INTO software you wrote. Contrast **exporter**. (Chapter 18 §4)

**Cluster-level logging** — Logs given "a separate storage and lifecycle independent of nodes, pods, or containers." Requires "a separate backend to store, analyze, and query logs. Kubernetes does not provide a native storage solution for log data" [source: k8s-docs-logging-architecture-2026-08-23]. (Chapter 13 §7; architectures at Chapter 18 §6)

**Code-based instrumentation** — Instrumentation written into the application, giving "deeper insight and rich telemetry from your application itself" [source: opentelemetry-instrumentation-2026-08-31]. The only kind that can see inside a request handler. (Chapter 18 §1, §5)

**Context** — "an object that contains the information for the sending and receiving service, or execution unit, to correlate one signal with another" [source: opentelemetry-context-propagation-2026-08-31]. (Chapter 18 §5)

**Context propagation** — The mechanism by which signals "be correlated with each other, regardless of where they are generated." Concretely: "Service A includes a trace ID and a span ID as part of the context. Service B uses these values to create a new span that belongs to the same trace." Allows traces "to build causal information about a system across services that are arbitrarily distributed across process and network boundaries" [source: opentelemetry-context-propagation-2026-08-31]. (Chapter 18 §5)

## D

**Distributed trace** — "records the paths taken by requests (made by an application or end-user) as they propagate through multi-service architectures, like microservice and serverless applications" [source: opentelemetry-observability-primer-2026-08-23]. See **trace**, **span**. (Chapter 18 §5)

## E

**Error budget** — The unreliability an SLO leaves room for. "As long as the uptime measured is above the SLO — in other words, as long as there is error budget remaining — new releases can be pushed" [source: sre-book-error-budgets-2026-08-31]. Exists to referee a structural tension: product development is evaluated on velocity, SRE on reliability [source: sre-book-error-budgets-2026-08-31]. (Chapter 18 §7)

**Errors (golden signal)** — "the rate of requests that fail, either explicitly (e.g., HTTP 500s), implicitly (for example, an HTTP 200 success response, but coupled with the wrong content), or by policy (for example, 'If you committed to one-second response times, any request over one second is an error')" [source: sre-book-four-golden-signals-2026-08-23]. (Chapter 18 §7)

**Exporter (Prometheus)** — "a binary running alongside the application you want to obtain metrics from" [source: prometheus-glossary-2026-08-31]. For software you did NOT write and cannot modify. It EXPOSES an endpoint Prometheus scrapes; it does not push. Contrast **client library**. (Chapter 18 §4)

## F

**Fluent Bit** — "an open source telemetry agent that processes logs, metrics, traces, and profiles," created in 2014 by Eduardo Silva "as a lightweight log processor, developed by the Fluentd team at Treasure Data for constrained environments such as embedded Linux"; "a sub-project of Fluentd" [source: fluent-bit-overview-2026-08-23]. Two words. (Chapter 18 §6)

**Fluentd** — A CNCF project implementing the unified logging layer: it "tries to structure data as JSON as much as possible: this allows Fluentd to unify all facets of processing log data," "connects dozens of data sources and data outputs," through "a flexible plugin system." Accepted into the CNCF November 2016; graduated 2019. A vanilla instance "runs on 30-40MB of memory" [source: fluentd-architecture-2026-08-31]. One word. ⚠ Maturity levels move; do not grade a current roster. (Chapter 18 §6)

**Four golden signals** — "latency, traffic, errors, and saturation" [source: sre-book-four-golden-signals-2026-08-23]. If you can instrument only four things on a user-facing system, these are the four. (Chapter 18 §7)

## G

**Grafana** — "open source software that enables you to query, visualize, alert on, and explore your metrics, logs, and traces wherever they're stored" [source: grafana-introduction-2026-08-23]. Reads Prometheus through its HTTP API; not part of Prometheus, and Prometheus does not depend on it. ⚠ Its CNCF non-membership is a negative and is NOT sourceable — see gap G-18b. (Chapter 18 §4)

## I

**Instrumentation** — The work of making a system emit signals. "For a system to be observable, it must be instrumented: that is, code from the system's components must emit signals" [source: opentelemetry-instrumentation-2026-08-31]. ★ The completeness bar: "An application is properly instrumented when developers don't need to add more instrumentation to troubleshoot an issue, because they have all of the information they need" [source: opentelemetry-observability-primer-2026-08-23]. (Chapter 18 §1)

## J

**Jaeger** — A distributed tracing backend: it "receives tracing telemetry data and provides processing, aggregation, data mining, and visualizations." "Originally designed to support the OpenTracing standard," and "OpenTelemetry compatible; terminology and concepts map directly between the two data models" [source: jaeger-overview-2026-08-23]. ⚑ Deliberately ungraded in this book. (Chapter 18 §5)

## K

**Known unknown** — A question you have thought of but do not yet have the answer to. Monitoring's territory: "Monitoring is called a system that can detect known unknowns" [source: cncf-tag-observability-whitepaper-2026-08-31]. (Chapter 18 §1)

## L

**Latency** — "the time it takes to service a request." ⚠ "It's important to distinguish between the latency of successful requests and the latency of failed requests," because a fast error makes overall latency look good — "a slow error is even worse than a fast error!" [source: sre-book-four-golden-signals-2026-08-23] "Latency increases are often a leading indicator of saturation." (Chapter 18 §7)

**Log** — "a recording of an event" [source: opentelemetry-signals-2026-08-23]. ⚠ Logs "are not extremely useful for tracking code execution on their own, as they typically lack contextual information; they become far more useful when they are included as part of a span, or when they are correlated with a trace and a span" [source: opentelemetry-observability-primer-2026-08-23]. (Chapter 18 §2, §6)

**Log rotation** — The kubelet rotates container log files, configured via `containerLogMaxSize` (default 10Mi) and `containerLogMaxFiles` (default 5); "only the contents of the latest log file are available through `kubectl logs`" [source: k8s-docs-logging-architecture-2026-08-23]. (Chapter 18 §6)

## M

**Metric** — "a measurement captured at runtime" [source: opentelemetry-signals-2026-08-23]. Answers WHETHER something is happening, and how much. (Chapter 18 §2, §3)

**Metric label** — A key-value dimension on a time series. "Every time series is uniquely identified by its metric name and optional key-value pairs called labels," and "the change of any label's value, including adding or removing labels, will create a new time series" [source: prometheus-data-model-2026-08-31]. ⚠ HOMONYM: not a Kubernetes label (Chapter 4 §5). Always written "metric label" on first use and wherever a Kubernetes object is also present. (Chapter 18 §3)

**Monitoring** — "collecting, processing, aggregating, and displaying real-time quantitative data about a system" [source: sre-book-monitoring-definitions-2026-08-31]. Detects **known unknowns** — indicators chosen in advance. Its four canonical purposes are long-term trends, alerting, building dashboards, and debugging [source: sre-book-monitoring-definitions-2026-08-31]. (Chapter 18 §1; named Chapter 1)

## N

**Node-level logging agent** — An agent running on every node, "typically as a DaemonSet," that reads the container log files the runtime already writes and forwards them to a backend [source: k8s-docs-logging-architecture-2026-08-23]. The default cluster-logging architecture, because it is the only one that works without the application's cooperation. (Chapter 18 §6; glossed Chapter 13 §7)

## O

**Observability** — "lets you understand a system from the outside by letting you ask questions about that system without knowing its inner workings," which is what lets you "troubleshoot and handle novel problems, that is, 'unknown unknowns'" [source: opentelemetry-observability-primer-2026-08-23]. "A system property," and "how observable a system is will significantly impact its operating and development costs" [source: cncf-glossary-observability-2026-08-31]. ★ Not a product you install. Under the current KCNA blueprint it is a competency inside Cloud Native Architecture, not a domain [source: lf-kcna-program-changes-2026-08-23]. (Chapter 18 §1; named Chapter 1)

**OpenTelemetry (OTel)** — The project defining the four signals, the instrumentation APIs and SDKs, and the Collector. (Chapter 18 §2)

**OpenTracing** — The standard Jaeger "was originally designed to support" [source: jaeger-overview-2026-08-23]. Named once, ungraded. (Chapter 18 §5)

**OpenTelemetry Collector** — "a vendor-agnostic implementation of how to receive, process and export telemetry data." It "removes the need to run, operate, and maintain multiple agents/collectors," supporting "open source observability data formats (e.g. Jaeger, Prometheus, Fluent Bit, etc.) sending to one or more open source or commercial backends," and is deployable "as an agent or collector with support for traces, metrics, and logs" from one codebase [source: opentelemetry-collector-2026-08-31]. ⚠ Gap G-18c: receiver / processor / exporter are NOT captured verbatim as named pipeline stages. Do not present them as a taxonomy. (Chapter 18 §2)

## P

**p99 / pNN** — The 99th (Nth) percentile of a measurement, most often latency. ⚠ Reaches a graded stem in this chapter; needs an in-text gloss at first use, not a glossary-only entry. (Chapter 18 §3)

**PromQL (Prometheus Query Language)** — "the Prometheus Query Language" [source: prometheus-glossary-2026-08-31], a functional language that "lets the user select and aggregate time series data in real time" [source: prometheus-promql-basics-2026-08-31]. Results are available in the Prometheus UI, and "other programs can fetch the result of a PromQL expression via the HTTP API." ⚠ Syntax is NOT KCNA surface and none is cached. (Chapter 18 §4)

**Prometheus** — "an open-source systems monitoring and alerting toolkit originally built at SoundCloud," which "joined the Cloud Native Computing Foundation in 2016 as the second hosted project, after Kubernetes." ★ "Time series collection happens via a pull model over HTTP," with targets "discovered via service discovery or static configuration" [source: prometheus-overview-2026-08-23]. (Chapter 18 §4; named Chapter 1)

**Pushgateway** — "an intermediary service which allows you to push metrics from jobs which cannot be scraped." ★ "The only valid use case for the Pushgateway is for capturing the outcome of a service-level batch job," where a service-level batch job is "one which is not semantically related to a specific machine or job instance" [source: prometheus-pushgateway-practices-2026-08-31]. Even here the arrow into Prometheus does not reverse: Prometheus scrapes the gateway. (Chapter 18 §4)

## R

**RED method** — Rate, Errors, Duration: "the number of requests per second," "the number of those requests that are failing," and "the amount of time those requests take" [source: red-method-tom-wilkie-2026-08-31]. Service-oriented. Its author: "The USE Method doesn't really apply to services; it applies to hardware, network disks, things like this. We really wanted a microservices-oriented monitoring philosophy, so we came up with the RED Method." ⚠ Tier-4 provenance; named and contrasted only, never graded. (Chapter 18 §7)

**Reliability** — Answers the question: "Is the service doing what users expect it to be doing?" [source: opentelemetry-observability-primer-2026-08-23] (Chapter 18 §7)

**Root span** — "The first span represents the root span; each root span represents a request from start to finish" [source: opentelemetry-observability-primer-2026-08-23]. Exactly one per trace. (Chapter 18 §5)

## S

**Sample** — An individual reading in a time series: a value plus a millisecond-precision timestamp [source: prometheus-data-model-2026-08-31]. (Chapter 18 §3)

**Saturation** — "how 'full' your service is. A measure of your system fraction, emphasizing the resources that are most constrained." "Many systems degrade in performance before they achieve 100% utilization, so having a utilization target is essential" [source: sre-book-four-golden-signals-2026-08-23]. (Chapter 18 §7)

**Scrape** — The act of a Prometheus server fetching a target's metrics endpoint over HTTP on an interval. A **target** is "the definition of an object to scrape" [source: prometheus-glossary-2026-08-31]. (Chapter 18 §4)

**Signal (OpenTelemetry)** — A system output describing the underlying activity of the platform and the applications on it — something you want to measure at a point in time, or an event moving through a distributed system that you would like to trace [source: opentelemetry-signals-2026-08-23]. ★ FOUR are defined on the Signals page: traces, metrics, logs, baggage. ⚠ The CNCF TAG Observability whitepaper enumerates a different five (metrics, logs, traces, profiles, dumps) [source: cncf-tag-observability-whitepaper-2026-08-31]; OTel's own primer names three in passing. Attribution decides which list a question wants. (Chapter 18 §2)

**SLA (Service Level Agreement)** — "an explicit or implicit contract with your users that includes consequences of meeting (or missing) the SLOs they contain" [source: sre-book-service-level-objectives-2026-08-31]. Discrimination procedure: "ask 'what happens if the SLOs aren't met?': if there is no explicit consequence, then you are almost certainly looking at an SLO." (Chapter 18 §7)

**SLI (Service Level Indicator)** — "represents a measurement of a service's behavior. A good SLI measures your service from the perspective of your users" [source: opentelemetry-observability-primer-2026-08-23]; "a carefully defined quantitative measure of some aspect of the level of service that is provided" [source: sre-book-service-level-objectives-2026-08-31]. ★ The MEASUREMENT. (Chapter 18 §7)

**SLO (Service Level Objective)** — "the means by which reliability is communicated to an organization/other teams. This is accomplished by attaching one or more SLIs to business value" [source: opentelemetry-observability-primer-2026-08-23]; "a target value or range of values for a service level that is measured by an SLI" [source: sre-book-service-level-objectives-2026-08-31]. ★ The OBJECTIVE. (Chapter 18 §7)

**Span** — "represents a unit of work or operation." Spans "track specific operations that a request makes, painting a picture of what happened during the time in which that operation was executed," and a span "contains name, time-related data, structured log messages, and other metadata (that is, attributes)" [source: opentelemetry-observability-primer-2026-08-23]. (Chapter 18 §5)

**SRE (Site Reliability Engineering)** — The practice from which SLIs, SLOs, error budgets and the four golden signals originate. Not itself an exam object and NOT eligible for graded text (B7 orphan ruling, term-ownership.md:817). (Chapter 18 §1)

## T

**Telemetry** — "data emitted from a system and its behavior" [source: opentelemetry-observability-primer-2026-08-23]. (Chapter 18 §1)

**Time series** — "streams of timestamped values belonging to the same metric and the same set of labeled dimensions" [source: prometheus-data-model-2026-08-31]. Not one number; a stream of them, shaped so aggregation over time is cheap. (Chapter 18 §3)

**Trace** — "the path of a request through your application" [source: opentelemetry-signals-2026-08-23]. ★ "A trace is made of one or more spans. The first span represents the root span; each root span represents a request from start to finish" [source: opentelemetry-observability-primer-2026-08-23]. One trace per request, not one per service. (Chapter 18 §2, §5)

**Traffic** — "a measure of how much demand is being placed on your system, measured in a high-level system-specific metric" — HTTP requests per second for a web service; network I/O rate or concurrent sessions for streaming; transactions and retrievals per second for a key-value store [source: sre-book-four-golden-signals-2026-08-23]. (Chapter 18 §7)

## U

**Unknown unknown** — A question you had not thought to ask until the moment you needed it. Observability's territory: observability "emphasizes being able to find and reason about unknown unknowns as well" [source: cncf-tag-observability-whitepaper-2026-08-31]. (Chapter 18 §1)

**USE method** — "the Utilization Saturation and Errors (USE) Method is a methodology for analyzing the performance of any system," directing "the construction of a checklist, which for server analysis can be used for quickly identifying resource bottlenecks or errors" [source: use-method-brendan-gregg-2026-08-31]. Resource-oriented. Its "utilization" is "the average time that the resource was busy servicing work" — a third distinct sense of the word in this book. (Chapter 18 §7)

**Utilization (Kubernetes autoscaling sense)** — "the controller calculates the utilization value as a percentage of the equivalent resource request on the containers in each Pod" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31]. ★ The denominator is the RESOURCE REQUEST — not node capacity, not the limit. "If some of the Pod's containers do not have the relevant resource request set, CPU utilization for the Pod will not be defined and the autoscaler will not take any action for that metric." Undefined, not zero. (Chapter 5 §8; settled at Chapter 18 §3)

## W

**W3C TraceContext** — The specification whose headers "the default propagator uses" for context propagation [source: opentelemetry-context-propagation-2026-08-31]. ⚠ Not KCNA surface; named once, never graded. (Chapter 18 §5)

## Z

**Zero-code instrumentation** — Instrumentation attached from outside the application, "great for getting started, or when you can't modify the application you need to get telemetry out of," providing telemetry "from libraries you use and/or the environment your application runs in" [source: opentelemetry-instrumentation-2026-08-31]. A service mesh is exactly that environment. ⚠ Sees what crosses the network, never what happens inside a request handler. (Chapter 18 §1, §5)

=== END WRITE ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

## Chapter 18 (2026-08-31)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D4.1 — Observability | Chapter 18 | deep — whole competency | 2026-08-31 |
| D2.3 — Troubleshooting (secondary, §3 and §6) | Chapter 13 | reinforcement | 2026-08-31 |

### Domain 4 is complete

D4.1 here; D4.2 and D4.3 at Chapter 17. The curriculum's own ordering corroborates
the split: "Observability; Cloud Native Ecosystem and Principles; Cloud Native
Community and Collaboration" [source: cncf-kcna-curriculum-pdf-2026-08-23].

Note the competency name is **Observability**, not "Cloud Native Observability" —
a correction Ch 17's manifest raised and Ch 18 ships correctly.

### ⚑ OPEN — a secondary-objective declaration with nowhere left to defer to

Ch 18 §4 and §6 each touch D4.2 (Prometheus's and Fluentd's CNCF status, and the
project-maturity caveat), which Chapter 17 owns. §3 and §6 already declare D2.3 as
secondary for exactly this "these are seams" reason. §4 and §6 should declare D4.2
the same way, so question-writing and reconciliation read interleaving rather than
untagged drift.

Chapter 18 is the last content chapter. There is no later chapter to defer this to.

### Frontmatter to write at materialisation

The absent YAML block in draft-v2.md is normal pipeline behaviour, not a regression
(Ch 16 and Ch 17 draft-v2 files are the same, and Ch 16's revision stage recorded
why). Chapter 18's block must carry:

  chapter: 18
  chapter_type: "content"
  title: "Reading the Instruments"
  domain_weight_pct: 5        # the AUTHORED allocation, not the published 12
  objectives: ["D4.1"]        # + D2.3 and D4.2 as secondary

The in-chapter metadata line carries the published 12%, per the rule Ch 16 and
Ch 17 both shipped. Use Ch 16's disambiguating form (ch16:227), which also restores
the [source:] tag Ch 17 and Ch 18 currently omit.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

## Chapter 18 (2026-08-31)

### Tagged retrieval items (7)

| Tested topic | Original chapter | Retested in |
|---|---|---|
| the absent-component pattern | ch 3 (phrase) · ch 10 §3 (named) | ch 18 Bearings 1 Q5 |
| metrics-server scope vs Prometheus collection | ch 13 §7 | ch 18 Bearings 2 Q4 |
| mesh telemetry without code changes | ch 17 §5 | ch 18 Bearings 2 Q5 |
| DaemonSet = one Pod per node | ch 6 §7 | ch 18 Bearings 3 Q5, Practice Q14 |
| utilization undefined without a resource request | ch 5 §8 | ch 18 Practice Q6 |
| metrics-server keeps no history | ch 13 §7 | ch 18 Practice Q7 |

### Untagged retrieval carried by cross-bearing (8 more)

Recorded so Ch 19's confusion-pair audit sees the real load, which is 15 of 40 items.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| probes leave no record | ch 5 §7 | ch 18 Soundings Q1, §1, Bearings 1 Q3e |
| kubectl top fails without its component | ch 13 §7 · 10 §3 | ch 18 Soundings Q3 |
| utilization relative to requests | ch 5 §8 · 17 §7 | ch 18 Soundings Q4, §3, Practice Q5 |
| log collection is a per-node job | ch 6 §7 · 13 §7 | ch 18 Soundings Q5, §6 |
| kubectl logs bounds — rotation, one-restart depth | ch 13 §3 | ch 18 Soundings Q6, §6, Bearings 3 Q1 |
| one request, many services | ch 17 §3 | ch 18 Soundings Q7, §5, §7 (RED's origin) |
| eviction destroys container logs | ch 13 §4 | ch 18 §6 |
| the scheduler does not place one-per-node | ch 7 §1 | ch 18 Bearings 3 Q5 |

### Distractors drawn from earlier chapters (5)

StatefulSet ordinal identity (ch 6 §6, Practice Q14) — ⚑ NO SHARD EXISTS, see below.
CRI as the kubelet-runtime boundary (ch 2 §4, Practice Q8).
etcd as the control plane's datastore (ch 3 §2, Practice Q11).
ResourceQuota and LimitRange (ch 8 §3, Practice Q5 and Q6).
CNCF maturity as a moving roster (ch 17 §2, §4 and §6 prose).

### Compliance against B3

B3 sets Chapter 18 at the 25% ceiling, "precisely because everything after this
point is assessment."

Measured: 4 of 15 checkpoint questions (26.7%) and 3 of 17 practice questions
(17.6%). Combined 7 of 32 graded items = 21.9%, inside skill Part 10's 20-25%
band for Ch 6+. Drawn from five chapters (5, 6, 10, 13, 17), three of them more
than four chapters back.

### The v1 -> v2 tag count change is a correctly handled diagnostic

draft-v1 carried 8 tags; draft-v2 carries 7. The question-quality audit flagged
v1's Practice Q13 [retrieval: ch17] as mis-tagged ("'six microservices' is
scenery, not a retrieval target") and prescribed dropping it while preserving the
Bearings count by tagging the incoming §4 component item [retrieval: ch13]. The
revision did exactly both. The drop in Practice density was anticipated. Do not
"restore" the eighth tag.

### ⚑ statefulset.md still does not exist

Flagged by ch-16's manifest, unrepaired. ch-06/kb-manifest.md is a lean early run
that sharded only custom-resource.md and operator-pattern.md, so Ch 6 §6's ordinal
identity was never sharded. Chapter 18 Practice Q14 option B grades it as a
distractor. Chapter 18 is the last content chapter that can flag this before Ch 19
reads the index and concludes the workload set is covered.

CREATE statefulset.md from shipped Ch 6 §6 at the replay.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cluster-level-logging.md ===

## Chapter 18 update (2026-08-31) — §6 is this concept's full treatment

⚑⚑ SLUG RULING. The Ch 18 outline nominated `cluster-logging-architecture` and
`node-level-logging-agent` as new concepts. BOTH ARE THIS FILE. Creating either
beside this shard would reproduce, at the chapter that owns the material, exactly
the pluggable-interface-pattern / pluggable-interfaces split that has now cost
three manifests a flag. Neither slug was created.

### The three architectures [source: k8s-docs-logging-architecture-2026-08-23]

1. A NODE-LEVEL LOGGING AGENT running on every node, typically as a DaemonSet,
   reading the container log files the runtime already writes.
2. A DEDICATED SIDECAR CONTAINER in the application Pod — either a streaming
   sidecar writing to its own stdout/stderr, or a sidecar running a logging agent
   configured to pick logs up from the application container.
3. THE APPLICATION PUSHES DIRECTLY to a backend from within the application.

### Why the node-level agent is the default answer

The discriminator, stated as a rule: node-level collection is the only option that
works WITHOUT THE APPLICATION'S COOPERATION. Container logs are already on the
node's filesystem for every container the node runs, whether the application team
did anything or not. Sidecars require a change to every Pod spec; direct push
requires a change to every application. A platform team does not control what
forty application teams write and cannot make forty deploys to fix logging.

The workload resource whose contract is one Pod per node is the DaemonSet.
See [[reading-container-logs]], [[fluentd-and-fluent-bit]].

### Agents

Fluentd and Fluent Bit "are commonly deployed on Kubernetes as node-level logging
agents (DaemonSets) that collect container logs from each node and forward them to
a backend" [source: fluent-bit-overview-2026-08-23]. See [[fluentd-and-fluent-bit]].

### ⚑ SOURCE HAZARD — do not re-point this shard's citations

Two captures of the same Kubernetes page exist:

  k8s-docs-logging-architecture-2026-08-23.md  (18 lines) <- THE FULLER ONE
  k8s-docs-logging-architecture-2026-08-31.md  (24 lines)  TRUNCATED

The 08-31 file's frontmatter claims it is "Fuller than" the 08-23 capture and
"Carries the log-rotation defaults and the 'only the latest log file' note, both
new." NEITHER FACT IS IN THAT FILE. Its body stops mid-page at the sentence that
introduces a code block. Both facts are in the 08-23 capture, which is what
Chapter 18 §6 cites, correctly, fourteen times.

Do not "modernise" these citations to the later date. See the manifest's ⚑ C0.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/reading-container-logs.md ===

## Chapter 18 update (2026-08-31) — kubectl logs is bounded three ways

⚑⚑ SLUG RULING. The outline's `log-rotation` concept folds in here rather than
becoming its own shard. See the ruling in [[cluster-level-logging]].

Ch 13 §3 taught the command. Ch 18 §6 teaches its LIMITS, because every one of them
is the reason cluster-level logging exists at all.

  ROTATION      The kubelet rotates container log files. Defaults:
                containerLogMaxSize 10Mi, containerLogMaxFiles 5. Critically,
                "only the contents of the latest log file are available through
                kubectl logs" [source: k8s-docs-logging-architecture-2026-08-23].
                A chatty container clears 10Mi in minutes.

  RESTART DEPTH "If a container restarts, the kubelet keeps one terminated
                container with its logs," which is what `kubectl logs --previous`
                retrieves [source: k8s-docs-logging-architecture-2026-08-23]. ONE.
                Not three, not "since the Pod was created."

  EVICTION      "If a pod is evicted from the node, all corresponding containers
                are also evicted, along with their logs"
                [source: k8s-docs-logging-architecture-2026-08-23].

## ⚠ The eviction bound is the load-bearing one

The other two are inconvenient. This one means the exact failure you most want to
investigate is the one that most reliably destroys its own evidence. That is the
whole argument for shipping lines off the node before you need them.
See [[oomkilled-vs-evicted]], [[cluster-level-logging]].

## The exam's discriminator

Any scenario involving *yesterday*, *across all replicas*, *searching for a
pattern*, or *a Pod that no longer exists* is describing cluster-level logging.
`kubectl logs` is the wrong answer. It is a live-tail-and-recent-history diagnostic
scoped to one container on one node.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-metrics-pipeline.md ===

## Chapter 18 update (2026-08-31) — the far side of the boundary

Ch 13 §7 established what metrics-server IS and what it is scoped to. Ch 18 §3
draws the line on the OTHER side, because that boundary is what the exam reaches
for — not either component's definition.

| Question | metrics-server | A monitoring system |
|---|---|---|
| What is this Pod using right now? | yes | yes |
| What was it using an hour ago? | no history kept | yes — time series |
| How many 500s did checkout return? | CPU and memory only | yes — arbitrary metrics |
| Page someone at 2% error rate | not its job | yes — alerting |
| p99 latency over a rolling 7 days | no query language | yes — query over time |

THE DISCRIMINATOR, one question: does answering this require history, alerting, or
a metric that is neither CPU nor memory? If yes, monitoring-system territory, and
metrics-server is wrong however much the question sounds like "metrics."

## These two coexist — do not overcorrect

Candidates who learn the boundary sometimes conclude Prometheus should REPLACE
metrics-server. Wrong. metrics-server feeds autoscaling decisions with current
readings, fast and cheaply. A monitoring system keeps history and answers arbitrary
questions. Different jobs; both installed on plenty of real clusters.

## Kubernetes states the absent-component pattern from the autoscaling side

metrics-server provides the `metrics.k8s.io` API and "needs to be launched
separately" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31] — the same
pattern the reader met from the `kubectl top` side.
See [[absent-component-pattern]], [[metrics-server-vs-monitoring-system]].

## No new figure

Ch 18 §3 deliberately retrieves ch13-fig04-metrics-pipeline-and-metrics-server
(chapter-13:1287) rather than redrawing it. There is no new architecture here,
only a boundary the reader can now see the far side of.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

## Chapter 18 update (2026-08-31) — the sixth instance, and a WORDING DATA POINT

Ch 18 §3 fires the pattern at metrics-server: `kubectl top` exists in every kubectl
binary ever shipped; whether anything answers it is a separate question about your
cluster. Kubernetes states the same thing from the autoscaling side — metrics-server
"needs to be launched separately"
[source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

## ⚑ WORDING: Chapter 18 uses VARIANT A, three times, verbatim

  L72   Soundings A3
  L360  §3
  L437  Bearings 1 answer 5

  "an object without its component does nothing"

Zero variants. This is a clean pass on the phrase most likely to drift, and it
shifts the count in favour of the standardisation Ch 17's manifest recommended:

  Variant A  ch 3 x2, ch 10 x12, ch 11 x4, ch 18 x3  = 21
  Variant B  ch 13 x3, ch 17 §7, B7 ledger row :339  = 5
  Variant C  ch 6 x2, B3 retrieval-architecture.md   = 3

STANDARDIZE ON VARIANT A. It is now 21 of 29 occurrences, it is the ★ Fixed Point,
it is inside a graded Ch 11 Practice option, and it is what the last content chapter
shipped. Correct B3, B7, Ch 6, Ch 13 and Ch 17 together, in one commit.

Attribution stays as Ch 11:811 states it: the phrase is Chapter 3's, and Chapter 10
§3 named it as a pattern.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/probe.md ===

## Chapter 18 update (2026-08-31) — what a probe is NOT

Ch 18 §1 uses probes as the negative space around observability, and the ledger
names this as its own owned concept: "health checking is not observability."

A liveness probe asks a container a yes/no question on a schedule. A readiness
probe asks a different yes/no question on a schedule. Both produce an immediate
action — restart the container, remove the Pod from endpoints — and then the answer
is spent.

WHAT A PROBE DOES NOT PRODUCE IS A RECORD. No trend. No queryable history. No way
to ask "how often did this endpoint fail its readiness check last Tuesday, and did
it correlate with the deploy?" The kubelet asked, got an answer, acted, moved on.

Health checking answers *is it up right now, according to one binary test I wrote
in advance*. That is not a different question from *why is this happening*. It is a
different KIND of question.

## Graded

Ch 18 Soundings Q1 and Bearings 1 Q3(e) both turn on this. Q3(e) is the sharper
one: it asks how many times an endpoint failed its readiness check during a deploy,
and the correct answer is that NOTHING in the chapter's toolkit records it — the
consequence (the endpoint leaving and rejoining the Service) is monitoring-system
work, but the probe result itself is on neither side of the boundary.

See [[health-checking-is-not-observability]], [[observability-vs-monitoring]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-request.md ===

## Chapter 18 update (2026-08-31) — the denominator, settled

Two earlier chapters (Ch 5 §8 and Ch 17 §7) pointed forward to Ch 18 §3 for one
number. §3 settles it, and it is the only place in the book that does.

"If a target utilization value is set, the controller calculates the utilization
value as a percentage of the equivalent resource request on the containers in each
Pod" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

Not node capacity. Not the container's limit. The REQUEST — what the Pod asked for
when it was scheduled.

## The proof is the failure case, not the formula

"If some of the Pod's containers do not have the relevant resource request set, CPU
utilization for the Pod will not be defined and the autoscaler will not take any
action for that metric" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

UNDEFINED. Not "computed against the node," not "defaults to something." A Pod with
no request has no utilization percentage at all, which is only possible if the
request is the denominator. Remove the denominator and the fraction ceases to exist.

## ⚠ The distractor this generates

"No data" and "zero" feel interchangeable and are not. The controller does not
compute a low value and scale down; it computes NO value and takes NO action on
that metric. A Pod scaled to minimum and a Pod the autoscaler is ignoring look
different in production and are graded differently on paper. Ch 18 Practice Q6
option B is built exactly there.

A LimitRange may DEFAULT a request at admission time — a separate mechanism acting
before the Pod exists, not the HPA improvising a denominator.
See [[utilization-relative-to-requests]], [[limit-range]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/label-selector.md ===

## Chapter 18 update (2026-08-31) — ⚠ HOMONYM WARNING

Ch 18 §3 introduces the book's second "label," and the B7 ledger (:870) governs it:

  Sense A  Kubernetes label — the universal join between objects and selectors
           (Ch 4 §5). THIS SHARD.
  Sense B  Prometheus metric label — a dimension on a time series (Ch 18 §3).
           See [[time-series-and-metric-labels]].

RULE: Sense B is always written "metric label" on first use in Ch 18 §3, and in any
sentence where a Kubernetes object is also present.

They are not related, not interchangeable, and reading a question quickly is exactly
how a candidate conflates them. Ch 18 §3 carries a 🪝 Snag saying so.

One residual, recorded rather than repaired: §3's first bolded use of "labels" sits
inside a verbatim Prometheus quotation and cannot be altered. The Snag immediately
following does the disambiguation explicitly. The §3 subheading "Labels, and the
cost of one" is bare — a one-word change to "Metric labels" would close it, at the
author's discretion.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/service-mesh.md ===

## Chapter 18 update (2026-08-31) — the mesh as a telemetry source, and its ceiling

Ch 17 §5 established that a mesh adds capabilities "without code changes." Ch 18 §5
cashes that out for observability and then names the limit, which Ch 17 could not.

A mesh injects a proxy alongside every workload; the proxy sees every request enter
and leave, so it can emit spans for traffic through an application whose source code
nobody touched. OpenTelemetry names the category: ZERO-CODE INSTRUMENTATION is
"great for getting started, or when you can't modify the application you need to get
telemetry out of," providing "rich telemetry from libraries you use and/or the
environment your application runs in" [source: opentelemetry-instrumentation-2026-08-31].
A mesh is precisely that environment.

## ⚠ THE CEILING — this is what Ch 18 adds

The proxy knows what crossed the network: this service called that service, it took
40ms, it returned a 503. It does NOT know which branch the code took, which cache
missed, or which of three database queries was slow. Those never cross the proxy.

Zero-code gives you the SHAPE of the request path for free. Code-based
instrumentation fills in the boxes. See [[zero-code-vs-code-based-instrumentation]].

## The phrase that signals which one a question means

"Without changing the application" is doing real work whenever it appears in an exam
scenario. Per-service latency in an uninstrumented app = the mesh. Visibility INSIDE
a service = code-based instrumentation. Ch 18 Bearings 2 Q5 grades exactly this.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/oomkilled-vs-evicted.md ===

## Chapter 18 update (2026-08-31) — eviction destroys the evidence

Ch 13 §4 taught the discrimination. Ch 18 §6 adds its observability consequence,
which is the reason cluster-level logging exists rather than a nice-to-have:

"If a pod is evicted from the node, all corresponding containers are also evicted,
along with their logs" [source: k8s-docs-logging-architecture-2026-08-23].

The Pod that was OOMKilled and evicted at 3 a.m. took its own logs with it. Rotation
and one-restart depth are inconvenient; this one means the exact failure you most
want to investigate is the one that most reliably erases its own record.

Retrieving that output requires an agent that shipped the lines to a backend BEFORE
the node discarded them. See [[cluster-level-logging]], [[reading-container-logs]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interface-pattern.md ===

## Chapter 18 update (2026-08-31) — the pattern turns up in a second ecosystem

⚑ SLUG RULING. Ch 18 §8's separability beat does NOT get its own slug. Creating
`producer-backend-separability.md` would be a third file for one shape, which is
exactly the drift ⚑ I2 records. It appends here and to [[one-pluggability-story]].

Ch 18 §8 names four instances, all inside observability, none of them Kubernetes:

  OpenTelemetry exports        ->  Jaeger receives
  Prometheus stores            ->  Grafana reads, through an HTTP API
                                   [source: prometheus-promql-basics-2026-08-31]
  The container runtime writes ->  an agent ships them
  container logs to the node       [source: k8s-docs-logging-architecture-2026-08-23]
  The OTel Collector receives  ->  "one or more open source or commercial backends"
  one set of signals               [source: opentelemetry-collector-2026-08-31]

Same shape every time: THE THING THAT PRODUCES TELEMETRY AND THE THING THAT STORES
IT ARE SEPARATE, AND EITHER CAN BE REPLACED WITHOUT THE OTHER NOTICING.

## Why this matters beyond trivia

Ch 17 §4 argued Kubernetes' durability comes from defining interfaces rather than
implementations. The observability ecosystem was built on the same conviction, by
different people, for different reasons, arriving at the same architecture. Ch 18 §8
states the conclusion: that is the reason both ecosystems are still standing.

## ⚑ DO NOT APPEND THIS TO pluggable-interfaces.md

That slug (ch-11) is a duplicate of this one. Merge it to a stub at the replay.
Chapter 18 is the last content chapter and deliberately did not entrench the split.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/one-pluggability-story.md ===

## Chapter 18 update (2026-08-31) — the argument recurs outside Kubernetes

Ch 17 §9's Zenith made the case that four pluggable interfaces are one story about
boundaries. Ch 18 §8 finds the same story running in a second ecosystem that
Kubernetes did not build — see the four instances recorded in
[[pluggable-interface-pattern]].

This is the strongest available corroboration for Ch 17's Zenith, and it arrives
from outside its own material, which is what makes it worth recording here: the
claim is not "Kubernetes is well designed" but "this is what durable systems
converge on."

Ch 19 §1 traces both as one cross-cutting thread. Do not let the Ch 18 instances
be re-derived there as though they were new.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/blueprint-change-2025-11-24.md ===

## Chapter 18 update (2026-08-31) — the observability consequence, stated plainly

Ch 18 §1 closes the loop Ch 1 opened for this specific competency, and it is the
last chapter that could:

Observability is no longer a standalone KCNA domain. It is a competency inside
CLOUD NATIVE ARCHITECTURE, weighted at 12% in total
[source: lf-kcna-program-changes-2026-08-23]. The Linux Foundation's own wording:
the domains remain mostly unchanged "except that observability will be rolled under
Cloud Native Architecture" [source: lf-kcna-program-changes-2026-08-23].

## ⚠ The reading that costs points

"Rolled under" is a REORGANIZATION, not a demotion. The material did not stop being
tested; it stopped being separately weighted, which is a different thing. A candidate
studying from pre-late-2025 material meets a contradiction here, and Ch 18 §1 names
it explicitly rather than letting the reader resolve it wrongly.

Ch 18's Exam Alert carries the trap row: "Expecting Observability as a standalone
domain." See [[domain-weights-44-28-16-12]], [[observability-vs-monitoring]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/domain-weights-44-28-16-12.md ===

## Chapter 18 update (2026-08-31) — the 12% is now split across two chapters

Cloud Native Architecture is 12% total, and TWO chapters display that figure:

  Ch 17  D4.2 + D4.3  authored allocation ~7%
  Ch 18  D4.1         authored allocation ~5%

Both correctly print the PUBLISHED 12% in the metadata line, per the rule Ch 16 and
Ch 17 shipped — the reader is calibrating against the blueprint, not against the
author's allocation. But two adjacent chapters showing "Domain Weight: 12%" reads as
though either one carries the whole domain.

Ch 16 already solved this, and its form is shipped (ch16:227):

  **Domain Weight: 12% (Cloud Native Architecture)
  [source: cncf-kcna-curriculum-pdf-2026-08-23] | Competency: Observability |
  Authored allocation for this chapter: ~5%**

That form also restores the [source:] tag on the published weight, which Ch 15 and
Ch 16 carry and which Ch 17 and Ch 18 currently omit.

## Domain 4 is now fully covered

D4.1 Observability (Ch 18) · D4.2 Ecosystem and Principles (Ch 17) · D4.3 Community
and Collaboration (Ch 17). The curriculum's own ordering matches
[source: cncf-kcna-curriculum-pdf-2026-08-23].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cncf-project-maturity-levels.md ===

## Chapter 18 update (2026-08-31) — trap #99 honored a second time, from a new angle

Ch 17 §2 taught the levels and refused the roster. Ch 18 §6 hits the same wall from
the logging side and handles it the same way:

Fluentd was accepted into the CNCF in November 2016 and graduated in 2019
[source: fluentd-architecture-2026-08-31]. Ch 18 states this as "CNCF graduated AS
OF THE SOURCE CACHED FOR THIS BOOK," and then names what is durable instead:
Fluentd is the CNCF project, Fluent Bit is its lighter sub-project, and both serve
as node-level agents.

## The contrast Ch 18 §4 uses, and why it is built that way

§4 needs to say Grafana is not a CNCF project, and CANNOT — that is a negative, and
proving it would mean citing a dated roster, which trap #99 and B3 both forbid
grading on (gap G-18b). So §4 states the contrast from the other side: Grafana is
Grafana Labs' own software, against two projects whose OWN documentation states a
donation — Prometheus in 2016 [source: prometheus-overview-2026-08-23] and Fluentd
in November 2016 [source: fluentd-architecture-2026-08-31].

"Carry the contrast, not a roster." That is the sourceable form of the point, and it
is the pattern any future chapter should copy when it needs to say a project is
outside the foundation.

NO GRADED ITEM in Ch 18 depends on any project's current maturity level.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/factor-xi-logs-as-event-streams.md ===

## Chapter 18 cross-link (2026-08-31) — who does the routing the factor forbids

Factor XI says an application should treat logs as an event stream and NOT concern
itself with routing or storage. Ch 15 taught the principle. Ch 18 §6 names the
machinery that makes it possible, which is the half the factor leaves unspecified.

The container runtime writes container logs to the node's filesystem; the kubelet
manages them there [source: k8s-docs-logging-architecture-2026-08-23]. A node-level
agent picks them up and ships them to a backend. The application wrote to stdout and
did nothing else — which is the factor, satisfied by infrastructure rather than by
discipline.

Note the third cluster-logging architecture, "the application pushes logs directly to
a backend," is the one that VIOLATES Factor XI: it couples application code to the
logging vendor. Ch 18 §6 names that cost without invoking the factor.

Recorded as a link, not as new canon. See [[cluster-level-logging]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop-pointed-at-a-repository.md ===

## Chapter 18 note (2026-08-31) — ⚑ the sanctioned count is REINFORCED, not extended

Ch 18's Voyage Ahead (L1467) previews Ch 19:

  "the control loop from Chapter 3, the operator pattern from Chapter 6, and the
   GitOps agent from Chapter 15 turn out to be one idea seen three times"

This names EXACTLY the three instances shipped Ch 6 sanctions when it tells the
reader they have seen the loop twice and "the third time is the one that matters" —
Ch 15 §7, the book's designated primary Zenith. Ch 18 adds no fourth.

⚑ FOR CH 19: this is a guardrail, not an invitation. Ch 19 §1 traces the control
loop as one of its nine threads and must not quietly promote a fourth instance into
the count, which would retroactively weaken Ch 15 §7's payoff. If a fourth is
genuinely wanted, it is an author decision that also requires editing Ch 6.

The book's ⛑ ordinal convention applies: state the pattern, never a running count,
except where the closed set is visible to the reader in the same breath — which is
what both Ch 6 and Ch 18 do here.

=== END APPEND ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/observability-vs-monitoring.md ===
# Concept: Observability vs monitoring

Absorbs `unknown-unknowns`. The discrimination IS the content; splitting them loses
the argument (the `oomkilled-vs-evicted` precedent).

## ★ Fixed Point

**Observability is the ability to ask questions of a running system that you did not
plan for in advance — to reason about *unknown unknowns*. Monitoring watches
indicators you chose ahead of time — *known unknowns*. The distinction is about what
you can ask, not about which tool you bought.**

## The sourced line

"Monitoring is called a system that can detect known unknowns — as opposed to
observability which emphasizes being able to find and reason about unknown unknowns
as well" [source: cncf-tag-observability-whitepaper-2026-08-31].

Monitoring's own definition assumes the choice has been made: "collecting, processing,
aggregating, and displaying real-time quantitative data about a system"
[source: sre-book-monitoring-definitions-2026-08-31]. Its four canonical purposes —
long-term trends, alerting, dashboards, debugging — are all questions somebody wrote
out before the incident.

Observability, from the other side: it "lets you understand a system from the outside
by letting you ask questions about that system without knowing its inner workings,"
which is what lets you handle "unknown unknowns"
[source: opentelemetry-observability-primer-2026-08-23]. It also answers "Why is this
happening?" as opposed to WHETHER it is happening, which a dashboard already covers.

## ⚠ THE misconception, and why "add a dashboard" is not the fix

The belief that observability is monitoring with better dashboards and a bigger
invoice. It is a TOOL-ACQUISITION misconception, and the correction is structural:
a Prometheus deployment with rich labels and an ad-hoc query language is doing
observability work; a pile of traces nobody can query is not. The posture is
upstream of the tool.

"Add another dashboard" responds to ONE unknown unknown after it has become known.
It does not fix the class, because there are more possible questions of that shape
than there are dashboards in the world.

## It is a property, not a product

"A system property," and "how observable a system is will significantly impact its
operating and development costs" [source: cncf-glossary-observability-2026-08-31].

## Graded

Ch 18 Bearings 1 Q1 (the 02:10 scenario) and Practice Q1. The tempting wrong answer
in both is "the dashboards are misconfigured."

See [[instrumentation-and-telemetry]], [[health-checking-is-not-observability]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/instrumentation-and-telemetry.md ===
# Concept: Instrumentation and telemetry

## The dependency, stated directly

"For a system to be observable, it must be instrumented: that is, code from the
system's components must emit signals" [source: opentelemetry-instrumentation-2026-08-31].

INSTRUMENTATION is the work of making a system emit those signals.
TELEMETRY is what comes out — "data emitted from a system and its behavior"
[source: opentelemetry-observability-primer-2026-08-23].

## ★ Fixed Point — the completeness test

**"An application is properly instrumented when developers don't need to add more
instrumentation to troubleshoot an issue, because they have all of the information
they need"** [source: opentelemetry-observability-primer-2026-08-23]**.**

The bar is not "we emit metrics." It is: when something novel breaks, nobody has to
ship a code change to find out what. If the debugging procedure routinely begins with
*let me add a log line and redeploy*, the application is not properly instrumented by
this definition, however many metrics it emits.

## Two kinds

CODE-BASED — written into the application; gives "deeper insight and rich telemetry
from your application itself."

ZERO-CODE — attaches from outside; "great for getting started, or when you can't
modify the application you need to get telemetry out of," pulling telemetry "from
libraries you use and/or the environment your application runs in"
[source: opentelemetry-instrumentation-2026-08-31].

See [[zero-code-vs-code-based-instrumentation]] for the ceiling on the second.

## ⚠ Distractors this generates

Ch 18 Practice Q2 offers three plausible wrong bars: emitting the four golden signals
(a monitoring prioritization heuristic, not a completeness bar); onboarding to a
graduated backend (a backend STORES telemetry, it does not produce it); and emitting
all four OTel signals (right four things, but thinly — the bar is sufficiency for
troubleshooting, not signal-type coverage).
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/health-checking-is-not-observability.md ===
# Concept: Health checking is not observability

A named B7 ledger row (term-ownership.md:579), owned by Ch 18 §1, with probes
explicitly excluded from the observability toolkit.

## The claim

A probe asks a yes/no question on a schedule and produces an immediate action —
restart the container, remove the Pod from endpoints. Then the answer is spent.

What a probe does not produce is a RECORD. No trend, no queryable history, no way to
ask "how often did this endpoint fail its readiness check last Tuesday, and did it
correlate with the deploy?"

Health checking answers *is it up right now, according to one binary test I wrote in
advance*. That is not merely a different question from *why is this happening*. It is
a different KIND of question — one whose answer is consumed at the moment it is
produced.

## 🪝 The Snag this generates

"We have liveness and readiness probes configured" is a true and useful statement
about a workload's self-healing. It is not an answer to "is this service observable."
A cluster full of perfect probes can still leave you unable to explain a single slow
request.

## Where a probe's consequence DOES become observable

The probe result is on neither side of the metrics-server / monitoring-system
boundary, because it is not a record at all. Getting an answer means recording the
CONSEQUENCE — the endpoint leaving and rejoining the Service, over time — which is
monitoring-system work. Ch 18 Bearings 1 Q3(e) grades exactly this distinction, and
"neither, as posed" is the correct answer.

See [[probe]], [[observability-vs-monitoring]], [[metrics-server-vs-monitoring-system]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/opentelemetry-four-signals.md ===
# Concept: The four OpenTelemetry signals

## ★ Fixed Point

**OpenTelemetry's Signals page defines FOUR signals: traces, metrics, logs, and
baggage** [source: opentelemetry-signals-2026-08-23]**. Candidates reliably name
three and drop baggage, because baggage is not itself a measurement — it is
contextual information passed between the other signals.**

| Signal | What it is | Answers | Cannot answer alone |
|---|---|---|---|
| Traces | "the path of a request through your application" | WHERE the time went, in what order | the aggregate picture |
| Metrics | "a measurement captured at runtime" | WHETHER, and how much | which specific request |
| Logs | "a recording of an event" | WHAT the code said happened | ordering across services |
| Baggage | "contextual information that is passed between signals" | — not a measurement; it is what lets the other three talk about the same request | anything by itself |

A signal generally is a system output describing the underlying activity of the
platform and the applications on it [source: opentelemetry-signals-2026-08-23].

## ⚠ "FOUR" IS OPENTELEMETRY'S COUNT — the attribution is the whole trap

Three authoritative lists exist and all are correct about their own document:

  OpenTelemetry Signals page  4  traces, metrics, logs, baggage
  CNCF TAG Observability wp   5  metrics, logs, traces, profiles, dumps
                                 [source: cncf-tag-observability-whitepaper-2026-08-31]
  OTel primer, in passing     3  traces, metrics, logs

When a question names OPENTELEMETRY, it wants the four. Ch 18 Practice Q3 offers all
three lists as options, which is why the attribution has to be taught, not just the
number. The whitepaper snapshot's own guardrail: do not write "the four signals" as
though it were a universal or CNCF-wide taxonomy.

## 🪢 Mnemonic

T-M-L-B. Three instruments and the thing that ties them together.

## The logs caveat, planted early

Logs "are not extremely useful for tracking code execution on their own, as they
typically lack contextual information; they become far more useful when they are
included as part of a span, or when they are correlated with a trace and a span"
[source: opentelemetry-observability-primer-2026-08-23].

See [[baggage]], [[distributed-tracing]], [[otel-collector]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/baggage.md ===
# Concept: Baggage

Own file, not a subsection of the signals shard, for two reasons: it is the item
candidates drop, and it is what Ch 18 §8's Zenith is built on.

## What it is

"Contextual information that is passed between signals"
[source: opentelemetry-signals-2026-08-23]. A key-value store letting you "propagate
any data you like alongside context," whose stated purpose is to "include information
typically available only at the start of a request further downstream" — account
identification, user IDs, product IDs, origin IPs
[source: opentelemetry-baggage-2026-08-31].

Service A knows which customer this is. Service E, four hops later, does not, unless
something carried it there.

## ★ Why it is a SEPARATE signal rather than a span property

"Baggage is a separate key-value store and is unassociated with attributes on spans,
metrics, or logs without explicitly adding them"
[source: opentelemetry-baggage-2026-08-31].

It rides alongside. Attaching it to a span is a DELIBERATE ACT. That separation is
exactly why it earns its own row — and exactly why people forget it.

## The payoff it enables

"Means you can pass data across services and processes, making it available to add to
traces, metrics, or logs in those services"
[source: opentelemetry-baggage-2026-08-31]. It is the signal that makes the other
three signals talk about THE SAME THING. Without it you have three readings of three
different things; with it you have one question examined at three resolutions.
See [[one-question-four-instruments]].

## Operational caution (not exam surface)

"Sensitive Baggage items can be shared with unintended resources, like third-party
APIs… making it visible to anyone inspecting your network traffic"
[source: opentelemetry-baggage-2026-08-31]. Customer identifiers are the classic case,
and the reason mature teams have a policy about what goes in baggage.

## Graded

Ch 18 Bearings 1 Q4, Practice Q3, Practice Q4. Q4's distractor A ("an attribute
automatically attached to every span") is the misconception the OTel docs pre-empt
by name.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/otel-collector.md ===
# Concept: The OpenTelemetry Collector

## What it is

"A vendor-agnostic implementation of how to receive, process and export telemetry
data" [source: opentelemetry-collector-2026-08-31].

Its value proposition is consolidation: it "removes the need to run, operate, and
maintain multiple agents/collectors," and supports "open source observability data
formats (e.g. Jaeger, Prometheus, Fluent Bit, etc.) sending to one or more open
source or commercial backends" [source: opentelemetry-collector-2026-08-31].

Deployable "as an agent or collector with support for traces, metrics, and logs" from
a single codebase — one implementation, several shapes, several signal types.

## The architectural idea, which recurs all chapter

One set of signals goes IN. Multiple swappable backends receive them going OUT. The
thing that produces telemetry and the thing that stores it are separate, and either
can be replaced without the other noticing.
See [[pluggable-interface-pattern]], [[one-question-four-instruments]].

## ⚑ GAP G-18c — DO NOT NAME THE PIPELINE STAGES

The words RECEIVER, PROCESSOR and EXPORTER are named as a taxonomy in OTel's docs but
were NOT captured verbatim in the cached snapshot. The snapshot carries an explicit
guardrail on this.

A chapter may say the Collector "receives, processes and exports" telemetry — that
phrasing IS verbatim. It must NOT present receivers/processors/exporters as a named
three-part taxonomy without a re-fetch.

Ch 18 §2 complies and carries an AUTHOR-REVIEW comment recording the constraint. If a
re-fetch closes G-18c, §2 could name them.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/time-series-and-metric-labels.md ===
# Concept: Time series, metric labels, and cardinality

Absorbs `cardinality`. The three are one mechanic stated as identity rather than as
three rules.

## What makes a metric different from a log line

Prometheus "fundamentally stores all data as time series: streams of timestamped
values belonging to the same metric and the same set of labeled dimensions"
[source: prometheus-data-model-2026-08-31]. Each individual reading is a SAMPLE — a
value plus a millisecond-precision timestamp.

That structure is what makes metrics cheap to keep and cheap to aggregate. You cannot
ask "what was the 95th-percentile latency across all of last week" of a pile of log
lines without reading all of them. You can ask it of a time series trivially, because
the shape of the data was chosen for that question.

## Identity is the metric name PLUS the label set

"Every time series is uniquely identified by its metric name and optional key-value
pairs called labels" [source: prometheus-data-model-2026-08-31]. So
`http_requests_total{status="200"}` and `http_requests_total{status="500"}` are two
distinct series that happen to share a name.

The consequence follows directly: "The change of any label's value, including adding
or removing labels, will create a new time series."

## 🔭 Cardinality is that identity rule, run forward

"Every unique combination of key-value label pairs represents a new time series, which
can dramatically increase the amount of data stored"
[source: prometheus-naming-labels-cardinality-2026-08-31]. Hence: "Do not use labels
to store dimensions with high cardinality (many different label values), such as user
IDs, email addresses, or other unbounded sets of values."

Add a `user_id` label to a busy endpoint's counter and you have not added a dimension.
You have multiplied your storage by your user count. Not KCNA surface; the single most
common way real teams break their own metrics stack.

## ⚠ HOMONYM — metric label vs Kubernetes label

B7 ledger rule (:870): sense B is always "metric label" on first use and wherever a
Kubernetes object is also present. They are unrelated and not interchangeable.
See [[label-selector]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/utilization-relative-to-requests.md ===
# Concept: Utilization is a percentage of the resource request

Two chapters (Ch 5 §8, Ch 17 §7) point forward to Ch 18 §3 for this one number. This
is where it is settled.

## ★ Fixed Point

**When an autoscaler or dashboard reports a Pod at "80% CPU utilization," the
denominator is THE CONTAINERS' RESOURCE REQUEST. Not the node's capacity. Not the
container's limit.**

"If a target utilization value is set, the controller calculates the utilization value
as a percentage of the equivalent resource request on the containers in each Pod"
[source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

## The proof is the failure case, not the formula

"If some of the Pod's containers do not have the relevant resource request set, CPU
utilization for the Pod will not be defined and the autoscaler will not take any
action for that metric" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

UNDEFINED. Not "computed against the node." Not "defaults to something." A Pod with no
request has no utilization percentage at all, which is only possible if the request is
the denominator. Remove the denominator and the fraction ceases to exist.

## 🪢 Mnemonic

Utilization is a fraction, and the bottom of the fraction is what you ASKED FOR, not
what you were STANDING ON. Request, not node. No request, no fraction.

## ⚠ THREE senses of "utilization" are live in this book

  Ch 18 §3      a percentage of the containers' resource request
                [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31]
  USE method    "the average time that the resource was busy servicing work"
                — a duration fraction [source: use-method-brendan-gregg-2026-08-31]
  Golden signals the nearest concept is SATURATION, how full the service is
                [source: sre-book-four-golden-signals-2026-08-23]

All three are correct in their own context. Check which system is speaking.

## Graded

Ch 18 Soundings Q4, Practice Q5, Practice Q6. Q5's strongest distractor is the LIMIT,
because limits are the more memorable number. Q6's is "0% and scales down," which
confuses no-data with zero.
See [[resource-request]], [[red-and-use-methods]], [[four-golden-signals]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/metrics-server-vs-monitoring-system.md ===
# Concept: metrics-server is not a monitoring system

The B7 ledger owns this as its own row (:587), separate from metrics-server itself,
which is Ch 13 §7. The BOUNDARY is the teaching object.

## ⚠ Navigational Hazards

The exam does not test whether you can define metrics-server. It tests WHICH SIDE OF
THE BOUNDARY a given question falls on.

THE DISCRIMINATOR, one question: does answering this require history, alerting, or a
metric that isn't CPU or memory? If yes, that is monitoring-system territory and
metrics-server is the wrong answer — no matter how much the words in the question
sound like "metrics."

## The four things metrics-server does not do

  history            it keeps none
  arbitrary metrics  CPU and memory only
  alerting           not its job
  query over time    no query language

## Both belong on a real cluster

metrics-server exists to feed autoscaling decisions with current readings, fast and
cheaply. A monitoring system exists to keep history and answer arbitrary questions
about it. Candidates who learn the boundary sometimes overcorrect into "replace
metrics-server with Prometheus," which is wrong.

## The pattern underneath

metrics-server provides the `metrics.k8s.io` API and "needs to be launched separately"
[source: k8s-docs-hpa-utilization-vs-requests-2026-08-31] — Kubernetes stating the
absent-component pattern from the autoscaling side, where the reader previously met it
from the `kubectl top` side. See [[absent-component-pattern]].

## Graded

Ch 18 Bearings 1 Q3 (a five-part sort), Bearings 1 Q5, Bearings 2 Q4, Practice Q7.
Q7's trap is option C, "increase metrics-server's retention configuration" — for
someone who thinks retention is a tuning knob rather than an out-of-scope capability.
See [[resource-metrics-pipeline]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/prometheus.md ===
# Concept: Prometheus and the pull model

Absorbs `pull-model`, `scraping`, `service-discovery`. Everything the exam wants turns
on one thing: WHICH WAY THE ARROW POINTS.

## ★ Fixed Point

**Prometheus PULLS. It scrapes metrics from targets over HTTP on an interval; targets
are found via service discovery or static configuration**
[source: prometheus-overview-2026-08-23]**. Pushing exists only through the
Pushgateway, and "the only valid use case for the Pushgateway is for capturing the
outcome of a service-level batch job"**
[source: prometheus-pushgateway-practices-2026-08-31]**.**

## What it is

"An open-source systems monitoring and alerting toolkit originally built at
SoundCloud," which "joined the Cloud Native Computing Foundation in 2016 as the SECOND
hosted project, after Kubernetes." Created at SoundCloud in 2012. "Time series
collection happens via a pull model over HTTP"
[source: prometheus-overview-2026-08-23].

⚠ SECOND, not first. Kubernetes was first. That swap is a real distractor.

## Targets and service discovery

A TARGET is "the definition of an object to scrape"
[source: prometheus-glossary-2026-08-31] — in practice one process exposing one source
of metrics. "Targets are discovered via service discovery or static configuration"
[source: prometheus-overview-2026-08-23].

In a Kubernetes cluster this matters enormously: Pods are not durable and their
addresses are not stable, so static configuration would be obsolete before you
finished writing it. Service discovery lets Prometheus ask the cluster what exists
right now.

## ⚠ The one place the arrow reverses, INSIDE Prometheus's own architecture

Alertmanager "handles alerts SENT BY client applications such as the Prometheus
server" [source: prometheus-alertmanager-2026-08-31]. So Prometheus PULLS from targets
and PUSHES to Alertmanager. Not a contradiction: the pull model describes how metrics
are COLLECTED, not how notifications are DISPATCHED. Keep the two clauses separate and
both facts fit.

## Graded

Ch 18 Bearings 2 Q1, Practice Q8. Practice Q8's most common wrong answer is "the
application POSTs metrics to Prometheus" — applications EXPOSE; Prometheus FETCHES.
See [[pushgateway]], [[prometheus-components]], [[prometheus-non-fit]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/prometheus-components.md ===
# Concept: Prometheus's components, and the code boundary

Absorbs `exporters`, `client-libraries`, `alertmanager`. Prometheus is a toolkit, not
a single binary [source: prometheus-overview-2026-08-23].

| Piece | What it is |
|---|---|
| Prometheus server | scrapes targets and stores the time series locally |
| Client library | "a library in some language (e.g. Go, Java, Python, Ruby) that makes it easy to directly instrument your code" [source: prometheus-glossary-2026-08-31] |
| Exporter | "a binary running alongside the application you want to obtain metrics from" [source: prometheus-glossary-2026-08-31] |
| Pushgateway | "persists the most recent push of metrics from batch jobs" [source: prometheus-glossary-2026-08-31] |
| Alertmanager | "takes in alerts, aggregates them into groups, de-duplicates, applies silences, throttles, and then sends out notifications" [source: prometheus-glossary-2026-08-31] |

Special-purpose exporters exist for services like HAProxy, StatsD and Graphite
[source: prometheus-overview-2026-08-23]. Alertmanager routes "to the correct receiver
integration such as email, PagerDuty, or OpsGenie"
[source: prometheus-alertmanager-2026-08-31].

## ⚓ The discrimination worth carrying into the exam

A CLIENT LIBRARY instruments code from the INSIDE: you added it, you own the code.
An EXPORTER is a SEPARATE BINARY that gets metrics out of something you did not write
and cannot change.

Same destination, opposite side of the code boundary. This is the same
instrumentation-versus-backend separation the OTel Collector shows in §2, appearing
again. See [[pluggable-interface-pattern]].

## ⚠ An exporter does NOT push

It EXPOSES an endpoint that Prometheus scrapes, exactly as a client library does. The
"exporter pushes to the server" option is a real distractor precisely because
exporters are real and widely used. Ch 18 Practice Q8 option C is built there.

## Graded

Ch 18 Bearings 2 Q4 (PostgreSQL you cannot modify + a Go service you wrote), Practice
Q8. Bearings 2 Q4's strongest distractor is the Pushgateway for PostgreSQL — correct
learning that the gateway handles what Prometheus cannot reach, over-generalized from
SHORT-LIVED to UNMODIFIABLE.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pushgateway.md ===
# Concept: The Pushgateway, and how narrow it is

## What it is

"An intermediary service which allows you to push metrics from jobs which cannot be
scraped" [source: prometheus-pushgateway-practices-2026-08-31].

Note INTERMEDIARY. Even here the metric does not land in Prometheus by being pushed.
It is pushed to the gateway, and Prometheus scrapes the gateway. THE ARROW INTO
PROMETHEUS NEVER REVERSES.

## ★ The licensed use, quoted because the wording is the whole trap

"We only recommend using the Pushgateway in certain limited cases," and "THE ONLY
VALID USE CASE for the Pushgateway is for capturing the outcome of a service-level
batch job" — where a service-level batch job is "one which is not semantically related
to a specific machine or job instance"
[source: prometheus-pushgateway-practices-2026-08-31].

The reason: a job that runs for eleven seconds and exits cannot be scraped on a
thirty-second interval. It is gone. Everything else — every long-running service, every
process with an address that stays put long enough to be visited — gets scraped.

## 🪝 The two distractors the source itself rules out

  "This service would RATHER push its metrics."
      A long-running web service CAN be scraped. Preference is not a criterion.
  "This job is tied to one specific machine."
      The source scopes the gateway to SERVICE-LEVEL batch jobs, which are the ones
      NOT semantically tied to a particular instance.

Both appear as options in Ch 18 Bearings 2 Q1 and Practice Q9. The stronger phrasing
("the only valid use case") is deliberately the one the Fixed Point carries, because
it builds the better distractor set.

## Not a delivery guarantee

It "persists the most recent push" [source: prometheus-glossary-2026-08-31]. It is not
an exactly-once mechanism, and it does not make sampling exact — routing per-request
events through it would not fix [[prometheus-non-fit]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/promql-and-the-read-path.md ===
# Concept: PromQL, the HTTP API, and Grafana

Absorbs `promql`, `grafana`. Storing time series is half of it; this is the other half.

## PromQL

"The Prometheus Query Language" [source: prometheus-glossary-2026-08-31], a functional
language that "lets the user select and aggregate time series data in real time"
[source: prometheus-promql-basics-2026-08-31].

⚑ SYNTAX IS NOT KCNA SURFACE, and none is cached. The outline deliberately excluded
PromQL from `kb_tags.commands` because it is a query language, not a kubectl verb. One
sentence is the whole obligation: a query language exists, it turns stored series into
answers, and the ability to write an ARBITRARY query is precisely what lifts a metrics
store toward the observability posture. Do not draft syntax.

## The read path

Results are available in the Prometheus UI, and "other programs can fetch the result of
a PromQL expression via the HTTP API" [source: prometheus-promql-basics-2026-08-31].

Grafana is one such consumer: "Grafana or other API consumers can be used to visualize
the collected data" [source: prometheus-overview-2026-08-23]. It reads THROUGH that
API. It is not part of Prometheus, and Prometheus does not depend on it — the
separability shape again. See [[pluggable-interface-pattern]].

## ⚑ GAP G-18b — do NOT assert Grafana is not a CNCF project

Nothing in the corpus or on grafana.com asserts non-membership, and proving a negative
would mean citing a dated CNCF roster, which trap #99 and B3 both forbid grading on.

The sourceable form is a CONTRAST, not a roster: Grafana is Grafana Labs' own software,
"open source software that enables you to query, visualize, alert on, and explore your
metrics, logs, and traces wherever they're stored"
[source: grafana-introduction-2026-08-23] — against two projects whose own docs state a
donation, Prometheus in 2016 [source: prometheus-overview-2026-08-23] and Fluentd in
November 2016 [source: fluentd-architecture-2026-08-31].

"Carry the contrast, not a roster." Copy this pattern anywhere the book needs to place
a project outside the foundation.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/prometheus-non-fit.md ===
# Concept: Where Prometheus explicitly does not fit

Own file, because knowing a tool's stated NON-fit is the kind of thing exams reward,
and this is the highest-yield trap in Chapter 18. Graded twice.

## ⚠ On accuracy — "reliability over completeness"

"Prometheus values reliability. If you need 100% accuracy, such as for per-request
billing, Prometheus is not a good choice as the collected data will likely not be
detailed and complete enough" [source: prometheus-overview-2026-08-23].

THE BILLING EXAMPLE IS THE DOCUMENTATION'S OWN. It is not the book's extrapolation.

This follows directly from the pull model: scraping samples STATE on an interval; it
does not observe EVENTS. If a counter increments 400 times between two scrapes,
Prometheus sees the difference, not the four hundred events.

⚠ Shortening the scrape interval does not converge on completeness. That is the belief
Ch 18 Practice Q10 option B targets. The trade is deliberate, not a tuning oversight.

## THE SENTENCE TO CARRY

A scenario mentioning billing, financial reconciliation, audit logs, or any phrase
implying every single event must be counted is telling you Prometheus is the WRONG
answer. Candidates who have learned "Prometheus is the metrics tool" pick it anyway,
because the question is about numbers. The question is about COMPLETENESS.

## On independence

"Each Prometheus server is standalone, not depending on network storage or other
remote services, so you can rely on it when other parts of your infrastructure are
broken." "No reliance on distributed storage — single server nodes are autonomous"
[source: prometheus-overview-2026-08-23].

A deliberate design trade, not an oversight. The moment your monitoring system depends
on your clustered storage, an outage in that storage takes down the thing that would
have told you about the outage.

## Graded

Ch 18 Bearings 2 Q2, Practice Q10, Practice Q11. Q11's distractors are Cassandra, etcd
and the Kubernetes API server — the last of which would be catastrophic for the control
plane and is worth naming as such.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/distributed-tracing.md ===
# Concept: Traces and spans

Absorbs `span`, `root-span`. The containment relationship is the exam's actual target.

## ★ Fixed Point

**A span is ONE unit of work. A trace is the WHOLE path a request took, and "a trace
is made of one or more spans." "The first span represents the root span; each root
span represents a request from start to finish"**
[source: opentelemetry-observability-primer-2026-08-23]**. Spans beneath the root
"provide a more in-depth context of what occurs during a request."**

## The definitions

SPAN — "represents a unit of work or operation." Spans "track specific operations that
a request makes, painting a picture of what happened during the time in which that
operation was executed," and a span "contains name, time-related data, structured log
messages, and other metadata (that is, attributes)"
[source: opentelemetry-observability-primer-2026-08-23].

TRACE (distributed trace) — "records the paths taken by requests (made by an
application or end-user) as they propagate through multi-service architectures, like
microservice and serverless applications"
[source: opentelemetry-observability-primer-2026-08-23].

## "One or more" — a trace is not defined by being multi-service

A single-service request produces a trace with exactly one span. A trace is defined by
being THE WHOLE REQUEST. Ch 18 Practice Q12 option D ("exactly one span per service the
request touches, never more") is wrong on both counts: a single service commonly emits
several spans for one request — the handler, a database call, a cache lookup.

## What the structure buys you that seven log files cannot

NESTING and DURATION. You can see that one downstream call accounts for nearly the
whole elapsed time, WITHOUT comparing timestamps across seven files and hoping the
clocks agree. The structure is the answer.

## 🪢 Mnemonic

A SPAN spans one operation. A TRACE traces the whole route. If you can point at a
single box on the diagram, it's a span; if you mean the entire picture, it's a trace.
And the picture always starts with one box that covers all the others — the root.

## 🪝 The register warning

"Span" and "trace" are used loosely and interchangeably in conversation, including by
people who know better. The exam does not use them loosely.

## Graded

Ch 18 Bearings 2 Q3, Practice Q12. See [[context-propagation]], [[jaeger]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/context-propagation.md ===
# Concept: Context propagation

Absorbs `trace-id`. This is the mechanism that closes the gap Ch 17 §3 opened.

## The problem it solves

Seven services, all logging correctly, all logging WELL — structured JSON, accurate
timestamps, sensible messages. And you still cannot answer "why did that request take
four seconds." Not because data is missing. Because NOTHING JOINS IT. There is no field
in service E's log line saying *I am part of the same request as that line in service A*.

## The definitions

CONTEXT — "an object that contains the information for the sending and receiving
service, or execution unit, to correlate one signal with another."
PROPAGATION — "the mechanism that moves context between services and processes."
Together they let signals "be correlated with each other, regardless of where they are
generated" [source: opentelemetry-context-propagation-2026-08-31].

## ★ The whole mechanism, in one sourced sentence

"Service A includes a trace ID and a span ID as part of the context. Service B uses
these values to create a new span that belongs to the same trace"
[source: opentelemetry-context-propagation-2026-08-31].

Repeat across seven hops and you have a chain that survives every process and network
boundary. Propagation "allows traces to build causal information about a system across
services that are ARBITRARILY DISTRIBUTED across process and network boundaries" — the
sentence that closes Ch 17's microservices loop.

## In-band, not reconstructed

The identifier travels in HTTP headers; "the default propagator uses the headers
specified by the W3C TraceContext specification"
[source: opentelemetry-context-propagation-2026-08-31].

⚠ W3C TraceContext is NOT exam surface at KCNA level. Name it at most once; do not
grade it. Ch 18 §5 complies.

What matters is that correlation rides WITH the request rather than being reconstructed
afterward by a clever log parser. Ch 18 Practice Q13 option A is exactly the
pre-tracing approach, and its unreliability across six independently clocked services
is why tracing exists.

## Baggage is the general form

"Baggage allows you to propagate arbitrary key-value pairs"
[source: opentelemetry-context-propagation-2026-08-31]. Trace and span IDs join the
WORK; baggage carries whatever else should travel with it. See [[baggage]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/jaeger.md ===
# Concept: Jaeger

## What it is

A distributed tracing backend: it "receives tracing telemetry data and provides
processing, aggregation, data mining, and visualizations". It "was originally designed
to support the OpenTracing standard," and is "OpenTelemetry compatible; terminology and
concepts map directly between the two data models"
[source: jaeger-overview-2026-08-23].

## The division of labor — this is the point, not the product

OpenTelemetry is the INSTRUMENTATION side: the APIs and SDKs that produce spans and
export them. Jaeger is the BACKEND: it receives them, stores them, draws the picture.
The OTel Collector supports Jaeger as one of its output formats
[source: opentelemetry-collector-2026-08-31].

Producer, wire format, consumer — all separable. Same shape as Prometheus stores /
Grafana reads. See [[pluggable-interface-pattern]], [[otel-collector]].

## ⚑ DELIBERATELY UNGRADED — do not "fix" this

No Soundings, Bearings or Practice item in Chapter 18 depends on Jaeger. The question
budget closes exactly at 40 (8 + 15 + 17) without it, and 17 Practice items is B4's
weight-proportional derivation, which must not change.

If the author wants Jaeger graded, the natural slot is one §5 Practice item on the
OTel-exports / Jaeger-receives division, taking §5 from 2 items to 3 and the chapter
from 17 Practice items to 18 — which requires re-deriving the budget.

⚠ ANY such item must NOT grade Jaeger's CNCF maturity level (trap #99), which the
snapshot states in frontmatter only.

## Provenance note

draft-v1 carried an AUTHOR-REVIEW claiming "the corpus has no jaegertracing.io
capture." That was wrong — `jaeger-overview-2026-08-23.md` exists, sourced to
jaegertracing.io/docs/latest/. The note was deleted at revision and the paragraph
tagged. Recorded so it is not re-raised.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/zero-code-vs-code-based-instrumentation.md ===
# Concept: Zero-code vs code-based instrumentation

## The two kinds

CODE-BASED — written into the application; gives "deeper insight and rich telemetry
from your application itself."

ZERO-CODE — attaches from outside; "great for getting started, or when you can't modify
the application you need to get telemetry out of," providing "rich telemetry from
libraries you use and/or the environment your application runs in"
[source: opentelemetry-instrumentation-2026-08-31].

A service mesh is precisely that environment: it injects a proxy alongside every
workload, and the proxy can emit spans for traffic through an application whose source
code nobody touched.

## ★ The ceiling, which is the graded part

The proxy knows what crossed the network: this service called that service, it took
40ms, it returned a 503. It does NOT know which branch the code took, which cache
missed, or which of three database queries was slow. Those never cross the proxy.

Zero-code gives you the SHAPE of the request path for free. Code-based instrumentation
fills in the boxes.

## The adoption order, which is not the documentation's order

Almost nobody starts with hand-instrumented traces. A team gets a mesh for mTLS or
traffic management, notices it now has per-service latency for free, and builds a
dashboard on it. That resolves a large fraction of incidents, because "the pricing
service is slow" is frequently all you needed.

The push to code-level instrumentation always comes from the same place: an incident
where "the pricing service is slow" was the BEGINNING of the question rather than the
end.

## The phrase that decides an exam item

"Without changing the application" is doing real work whenever it appears. Per-service
latency in an uninstrumented app = the mesh. Visibility INSIDE a service = code-based.

## Graded

Ch 18 Soundings Q8, Bearings 2 Q5. See [[service-mesh]], [[instrumentation-and-telemetry]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/fluentd-and-fluent-bit.md ===
# Concept: Fluentd and Fluent Bit

Consolidated — the RELATIONSHIP is the exam-adjacent detail, not either project alone.

## Fluentd

A CNCF project implementing the unified logging layer. It "tries to structure data as
JSON as much as possible: this allows Fluentd to unify all facets of processing log
data," it "connects dozens of data sources and data outputs," and it does so through "a
flexible plugin system that allows the community to extend its functionality." Accepted
into the CNCF November 2016; graduated 2019
[source: fluentd-architecture-2026-08-31].

## Fluent Bit

"An open source telemetry agent that processes logs, metrics, traces, and profiles,"
created in 2014 by Eduardo Silva "as a lightweight log processor, developed by the
Fluentd team at Treasure Data for constrained environments such as embedded Linux"; it
is "a SUB-PROJECT of Fluentd" [source: fluent-bit-overview-2026-08-23].

## Why two? Footprint.

A vanilla Fluentd instance "runs on 30-40MB of memory"
[source: fluentd-architecture-2026-08-31] — trivial on a server, less trivial across
every node in a large fleet, genuinely limiting on constrained hardware.

Both "are commonly deployed on Kubernetes as node-level logging agents (DaemonSets)
that collect container logs from each node and forward them to a backend"
[source: fluent-bit-overview-2026-08-23]. See [[cluster-level-logging]].

## 🪢 Mnemonic

Fluentd is ONE word. Fluent Bit is TWO. The parent is a single compound; the lightweight
child is "Fluent" plus a "Bit" of it. That asymmetry looks like a typo and is not, and a
question rendering one of them wrong is testing whether you noticed.

## ⚠ Trap #99 — the maturity level is a moving roster

Fluentd is CNCF graduated AS OF THE SOURCE CACHED FOR THIS BOOK. A question asking which
projects are CURRENTLY graduated is asking about a moving target. What is durable:
Fluentd is the CNCF project, Fluent Bit is its lighter sub-project, and both serve as
node-level agents. NO Ch 18 item grades the level.
See [[cncf-project-maturity-levels]].

## 🔭 What a log agent does between file and backend (not exam surface)

Fluent Bit's pipeline runs six stages: INPUT plugins gather; a PARSER structures; FILTERS
alter; a BUFFER stores in memory or on disk; a ROUTER directs via tags and matching
rules; OUTPUT plugins define destinations [source: fluent-bit-overview-2026-08-23].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/reliability-the-question.md ===
# Concept: Reliability — the question the instruments serve

Own file. This one sentence is the spine of Chapter 18 §7 and the whole of §8.

## The definition

**Reliability answers the question: "Is the service doing what users expect it to be
doing?"** [source: opentelemetry-observability-primer-2026-08-23]

## What it is NOT

Not "is CPU below 80%." Not "are all Pods Running." Not "did the probes pass."

Every one of those can be true while the service is failing the people using it, and
every one of them can be false while users are perfectly happy. That asymmetry is the
whole reason the SLI/SLO vocabulary exists — it turns "is it doing what users expect"
from a feeling into a number somebody can be held to.

## Why it belongs in a shard of its own

Ch 18 §8's Zenith is built entirely on this sentence: the four signals are not four
topics, they are four ways of asking this one question. Ask it of a metric and you get
WHETHER; of a trace, WHERE; of a log, WHAT; and baggage is what makes all three about
the same request.

A later chapter that treats §7 as "the SLI/SLO section" will miss that the section is
named for the question, not for the acronyms.
See [[one-question-four-instruments]], [[sli-slo-sla]], [[four-golden-signals]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/sli-slo-sla.md ===
# Concept: SLI, SLO, SLA

Consolidated — the discrimination IS the content. SLA is here by B7 orphan ruling
(term-ownership.md:805), which explicitly forbids routing it to the glossary alone
because it serves as a distractor in Ch 18 and Ch 20 answer keys.

## ★ Fixed Point

**An SLI is the MEASUREMENT. An SLO is the OBJECTIVE — a target value for that
measurement. The SLI is a number you observe; the SLO is a number you commit to.**

## In dependency order

SLI — "represents a measurement of a service's behavior. A GOOD SLI MEASURES YOUR
SERVICE FROM THE PERSPECTIVE OF YOUR USERS"
[source: opentelemetry-observability-primer-2026-08-23]; "a carefully defined
quantitative measure of some aspect of the level of service that is provided"
[source: sre-book-service-level-objectives-2026-08-31].

  The user-perspective clause has teeth. "Average CPU across the fleet" is a
  measurement and is not a useful SLI, because no user has ever cared about it. "The
  proportion of checkout requests that completed successfully in under 400ms" is one.

SLO — "the means by which reliability is communicated to an organization/other teams.
This is accomplished by attaching one or more SLIs to business value"
[source: opentelemetry-observability-primer-2026-08-23]; mechanically, "a target value
or range of values for a service level that is measured by an SLI"
[source: sre-book-service-level-objectives-2026-08-31].

SLA — "an explicit or implicit contract with your users that includes consequences of
meeting (or missing) the SLOs they contain"
[source: sre-book-service-level-objectives-2026-08-31]. External, contractual, with
teeth.

## THE DISCRIMINATION PROCEDURE — a test, not two definitions held side by side

"An easy way to tell the difference between an SLO and an SLA is to ask 'what happens
if the SLOs aren't met?': if there is no explicit consequence, then you are almost
certainly looking at an SLO"
[source: sre-book-service-level-objectives-2026-08-31].

⚠ PUBLICITY is not what makes an SLA. CONSEQUENCES are. Ch 18 Practice Q16 option A is
built on that confusion.

## 🪢 Mnemonic

I for Indicator — what you MEASURE. O for Objective — what you AIM AT. A for Agreement —
what you SIGN, with consequences attached. The containment runs the same direction as
the letters: an SLA contains SLOs, measured by SLIs.

## Graded

Ch 18 Bearings 3 Q3 (a three-way parse of one commitment), Practice Q16.
See [[error-budget]], [[reliability-the-question]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/error-budget.md ===
# Concept: Error budget

## What it is

The unreliability an SLO leaves room for. Its value is organizational rather than
mechanical: "as long as the uptime measured is above the SLO — in other words, as long
as there is error budget remaining — new releases can be pushed"
[source: sre-book-error-budgets-2026-08-31].

## Why it exists — a structural tension, not a metric

"Product development performance is largely evaluated on product velocity, which
creates an incentive to push new code as quickly as possible. Meanwhile, SRE
performance is evaluated based upon reliability of a service, which implies an
incentive to push back against a high rate of change"
[source: sre-book-error-budgets-2026-08-31].

The budget is the referee: a number both sides agreed to IN ADVANCE, in place of an
argument about judgment. That is what distinguishes it from a threshold.

## ⚠ It is not the objective

Ch 18 Practice Q16 option D offers "an error budget" for a statement that is plainly an
SLO. The budget is the ALLOWANCE the objective leaves room for, derived from it, not
the objective itself.

See [[sli-slo-sla]].
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/four-golden-signals.md ===
# Concept: The four golden signals

## ★ Fixed Point

**"The four golden signals of monitoring are latency, traffic, errors, and saturation"**
[source: sre-book-four-golden-signals-2026-08-23]**.** If you can instrument only four
things on a user-facing system, these are the four.

## The four, with the refinements that get tested

LATENCY — "the time it takes to service a request." ⚠ "It's important to distinguish
between the latency of successful requests and the latency of failed requests." An HTTP
500 from a dropped database connection "might be served very quickly," so folding 500s
into overall latency "might result in misleading calculations." And, memorably:
"A SLOW ERROR IS EVEN WORSE THAN A FAST ERROR!"

TRAFFIC — "a measure of how much demand is being placed on your system, measured in a
high-level system-specific metric." HTTP requests/second for a web service; network I/O
rate or concurrent sessions for streaming; transactions and retrievals/second for a
key-value store.

ERRORS — "the rate of requests that fail, either explicitly (e.g., HTTP 500s),
implicitly (for example, an HTTP 200 success response, but coupled with the wrong
content), or by policy (for example, 'If you committed to one-second response times,
any request over one second is an error')."

SATURATION — "how 'full' your service is. A measure of your system fraction, emphasizing
the resources that are most constrained." "Many systems degrade in performance before
they achieve 100% utilization, so having a utilization target is essential."

[all: source: sre-book-four-golden-signals-2026-08-23]

## ★ The one relationship worth carrying

**"Latency increases are often a leading indicator of saturation"**
[source: sre-book-four-golden-signals-2026-08-23]**.** Response times creeping up before
anything looks full is the system telling you it is about to be.

## 🪢 Mnemonic

L-T-E-S. Or as a sentence: HOW LONG, HOW MUCH, HOW BROKEN, HOW FULL.

## ⚠ Two different fours, and the exam will offer you the wrong one

The golden signals are MONITORING PRIORITIES. The four OpenTelemetry signals are SIGNAL
TYPES. Ch 18 Practice Q17 option D offers the OTel four for a golden-signals question,
and option A mixes RED's rate/errors/duration with the golden signals' saturation.
See [[opentelemetry-four-signals]], [[red-and-use-methods]].

## Graded

Ch 18 Bearings 3 Q4, Practice Q17.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/red-and-use-methods.md ===
# Concept: RED and USE

Consolidated — the value is the CONTRAST between them, not either one's details. Both
are named in the CNCF TAG Observability whitepaper
[source: cncf-tag-observability-whitepaper-2026-08-31], which references them without
defining either.

## USE — resource-oriented

"The Utilization Saturation and Errors (USE) Method is a methodology for analyzing the
performance of any system," directing "the construction of a checklist, which for server
analysis can be used for quickly identifying resource bottlenecks or errors"
[source: use-method-brendan-gregg-2026-08-31].

## RED — service-oriented

Rate, Errors, Duration: "the number of requests per second," "the number of those
requests that are failing," and "the amount of time those requests take"
[source: red-method-tom-wilkie-2026-08-31].

## The line, drawn by RED's own author

"The USE Method doesn't really apply to services; it applies to hardware, network disks,
things like this. We really wanted a microservices-oriented monitoring philosophy, so we
came up with the RED Method" [source: red-method-tom-wilkie-2026-08-31].

Note what produced it: RED exists BECAUSE one service became twenty. The architecture
changed and the measurement framing had to change with it — Chapter 18's thesis showing
up in the methodology literature rather than being asserted by the book.

## ⚑ PROVENANCE — RED is tier-4 and must stay ungraded

RED's only surviving authoritative source is a Grafana Labs blog post by Tom Wilkie, the
method's originator. The original Weaveworks publication is dead, and the CNCF TAG
Observability whitepaper's RED link now points at that dead host. No CNCF or LF source
defines RED.

That is the METHOD'S AUTHOR but is not official documentation. Per the outline's stated
posture, RED is named and contrasted, carries no teaching weight, and NO graded item in
Ch 18 depends on it. Practice Q17 option A uses RED's terms only as a distractor whose
correctness turns on the golden signals, which are fully sourced.

⚑ B1 gap G21 (golden signals + RED/USE together) should be recorded as
SUBSTANTIALLY-BUT-NOT-FULLY CLOSED: golden signals closed 2026-08-23, USE closed cleanly,
RED closed only at tier 4.

## ⚠ "Utilization" means three things — see [[utilization-relative-to-requests]]
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/one-question-four-instruments.md ===
# Concept: One question, four instruments (Chapter 18 Zenith)

The chapter's synthesis. Own file, per the `one-pluggability-story.md` /
`the-boundary-is-the-method.md` precedent. Introduces no new fact.

## The move

**The four signals are not four topics. They are four ways of asking one question.**

*Is the service doing what users expect it to be doing?*
[source: opentelemetry-observability-primer-2026-08-23]

  Ask it of a METRIC   -> WHETHER: the error rate crossed 2% at 02:07 and is climbing
  Ask it of a TRACE    -> WHERE:   3.65 of the 4 seconds were in one database call
  Ask it of a LOG      -> WHAT:    the line the code emitted when it gave up
  And BAGGAGE          -> what makes the first three about the SAME REQUEST rather
                          than three unrelated stories that co-occurred

## Why this makes dropping baggage worse than a memory slip

Without something carrying context across the boundary you have three readings of three
different things. With it you have one question examined at three resolutions. That is
the payoff of the fourth signal, and it is why the count matters.
See [[baggage]], [[opentelemetry-four-signals]], [[reliability-the-question]].

## The second beat — separability

Four instances of producer and backend being separable, all inside observability, none
of them Kubernetes. Recorded in [[pluggable-interface-pattern]] rather than duplicated
here, per the manifest's ⚑ C5 slug ruling. The conclusion Ch 18 draws is the part worth
keeping: two ecosystems, different people, different reasons, same architecture — and
that is the reason both are still standing.

## The disposition, which is the book's actual ask

Chapter 17 handed the reader a bill: everything that made the system easier to change
made it harder to see. Chapter 18 is the payment, and it is not a set of tools. It is
the habit of asking, BEFORE an incident rather than during one, *what would I need to be
emitting for this question to have an answer?*

The instruments follow from that. The dashboards follow from the instruments. Nothing
works in the other direction — which is why teams who start by buying a dashboard
product are so often the ones who cannot explain their own outages.

## ⚑ FOR CH 19

This is Domain 4's close and the last content chapter's close. Ch 19 §1 traces
observability as one of nine threads; it should retrieve this synthesis, not rebuild it.
=== END WRITE ===
```
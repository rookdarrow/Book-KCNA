Research complete. All four drafting-blocking gaps closed, plus SLA, error budget, cardinality — and one gap the outline hadn't flagged.

---

# Research Manifest — KCNA Chapter 18

**Stage 2 · Source Snapshot Research · run 2026-08-31**
Book: Kubernetes and Cloud Native Associate · Chapter 18 "Reading the Instruments" · D4.1 Observability (+ D2.3 seams)

**Starting corpus:** 276 files in `sources/`. Twelve were observability-relevant and were read before fetching, so nothing below duplicates existing coverage.

**Result:** 19 new snapshots. Stage 1's six sourcing gaps — including all four it marked drafting-blocking — are closed. Two gaps remain open (both non-blocking, both recorded below with the exact reason). One gap the outline did **not** flag was found and closed: **"utilization relative to requests" had no source anywhere in the 276-file corpus**, despite being pinned into §3 by two shipped chapters, one Soundings question, one Checkpoint item and one Practice item.

---

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `cncf-glossary-observability-2026-08-31.md` | CNCF Cloud Native Glossary | D4.1 | observability, actionable-insights, observability-tools |
| `cncf-tag-observability-whitepaper-2026-08-31.md` | CNCF TAG Observability | D4.1 | observability, monitoring, known-unknowns, unknown-unknowns, signals, metrics, logs, traces |
| `sre-book-monitoring-definitions-2026-08-31.md` | Google SRE book, ch. 6 | D4.1 | monitoring, white-box, black-box, alert, root-cause, why-monitor |
| `opentelemetry-instrumentation-2026-08-31.md` | OpenTelemetry (CNCF) | D4.1 | instrumentation, code-based, zero-code, signals |
| `opentelemetry-collector-2026-08-31.md` | OpenTelemetry (CNCF) | D4.1 | otel-collector, vendor-agnostic, agent-vs-collector, backends |
| `opentelemetry-baggage-2026-08-31.md` | OpenTelemetry (CNCF) | D4.1 | baggage, signals, propagation, span-attributes |
| `opentelemetry-context-propagation-2026-08-31.md` | OpenTelemetry (CNCF) | D4.1 | context-propagation, trace-id, span-id, w3c-tracecontext |
| `prometheus-data-model-2026-08-31.md` | Prometheus (CNCF) | D4.1 | time-series, metric-labels, sample, cardinality |
| `prometheus-naming-labels-cardinality-2026-08-31.md` | Prometheus (CNCF) | D4.1 | metric-labels, cardinality |
| `prometheus-glossary-2026-08-31.md` | Prometheus (CNCF) | D4.1 | exporters, client-libraries, pushgateway, alertmanager, target, endpoint, job, instance, sample, time-series, promql, silence |
| `prometheus-pushgateway-practices-2026-08-31.md` | Prometheus (CNCF) | D4.1 | pushgateway, pull-model, batch-jobs |
| `prometheus-alertmanager-2026-08-31.md` | Prometheus (CNCF) | D4.1 | alertmanager, grouping, inhibition, silencing, routing |
| `prometheus-promql-basics-2026-08-31.md` | Prometheus (CNCF) | D4.1 | promql, time-series |
| `k8s-docs-hpa-utilization-vs-requests-2026-08-31.md` | Kubernetes (kubernetes.io) | D4.1, D2.3 | utilization-relative-to-requests, metrics-api, metrics-server |
| `fluentd-architecture-2026-08-31.md` | Fluentd (CNCF graduated) | D4.1, D2.3 | fluentd, unified-logging-layer, plugins |
| `sre-book-service-level-objectives-2026-08-31.md` | Google SRE book, ch. 4 | D4.1 | sli, slo, sla |
| `sre-book-error-budgets-2026-08-31.md` | Google SRE book, ch. 3 | D4.1 | error-budget, reliability-vs-velocity |
| `use-method-brendan-gregg-2026-08-31.md` | Brendan Gregg (method's author) | D4.1 | use-method, utilization, saturation, errors |
| `red-method-tom-wilkie-2026-08-31.md` | Grafana Labs / Tom Wilkie — **tier caveat, see Notes #3** | D4.1 | red-method, rate, errors, duration |

### Coverage against `kb_tags`

Every concept in the outline's `kb_tags` now resolves. Newly closed by this stage: `otel-collector`, `context-propagation`, `time-series`, `metric-labels`, `cardinality`, `utilization-relative-to-requests`, `exporters`, `client-libraries`, `pushgateway`, `promql`, `alertmanager`, `fluentd`, `sla`, `error-budget`, `red-method`, `use-method`, plus a real definition of `monitoring`. `baggage` was upgraded from one sentence to five.

---

## Gaps

**G-18a · Retired KCNA domain weights (= B1 gap G33, Open Question #6). STILL OPEN.**
The retired five-domain curriculum PDF is reachable and was successfully downloaded this run from `https://github.com/cncf/curriculum/raw/master/old-versions/KCNA_Curriculum%20old.pdf` (151.9 KB). **Its text still could not be extracted** — the fetch tool returned the raw binary, the sandbox blocked the PDF-library check and the file copy, and `web.archive.org` is blocked outright for this session. This is a *different* failure from the 2026-08-23 attempt (which failed at retrieval); the file is now confirmed to exist and be retrievable, only the text layer is unreachable from here. **Do not draft the 8% figure from memory or from shipped Ch 1.** Author action if you want Open Question #6 resolved in favour of keeping Ch 1:272: open that PDF by hand and record its domain list. Otherwise sweep Ch 1:272 as the outline's second option.

**G-18b · "Grafana is not a CNCF project" is a negative and cannot be safely sourced.**
Nothing in the corpus or on grafana.com asserts non-membership; proving it would mean citing a dated CNCF project roster, which trap #99 and B3 both forbid grading on. See Notes #4 for the framing that gets §4's 🪝 Snag its point without asserting an unsourceable negative.

**G-18c · OTel Collector pipeline component names not captured verbatim (minor).**
The Collector snapshot carries the definition, the five design objectives and the deployment shape verbatim, which is everything §2 needs. The words *receiver*, *processor* and *exporter* as named pipeline stages came back only as summary, so they are **not** in the snapshot as quotable source text. §2 should say the Collector "receives, processes and exports" (that phrasing *is* verbatim) and stop there. Do not name the three component types as a taxonomy without a re-fetch.

**Unchanged from Stage 1, recorded so they stay visible:** Loki and Tempo still have no ledger owner and no source beyond the existing Grafana snapshot (Open Question #5 — recommendation stands: at most one non-graded clause, or omit). B1 gap G32 (FinOps / OpenCost / Kubecost) remains unassigned; `opencost-overview-2026-08-23.md` exists in the corpus but the outline's recommendation to keep it omitted, consistent with shipped Ch 17, is unaffected by anything found this run.

---

## Notes for the author

**1. The four-signals count is an OpenTelemetry claim specifically — and OTel's own primer says three.** This is the single most useful thing found this run, and it sharpens trap #89 considerably. `opentelemetry-signals-2026-08-23.md` lists four (traces, metrics, logs, baggage). But the already-cached `opentelemetry-observability-primer-2026-08-23.md` says "signals such as traces, metrics, and logs" and again "The data can come in the form of traces, metrics, and logs" — **three, twice, on the page §1 and §7 quote from most.** And the new CNCF TAG Observability whitepaper enumerates a *fifth* set: metrics, logs, traces, profiles and dumps. So: candidates drop baggage because the most-read OTel page drops it too. §2 should attribute the count to the Signals page by name rather than to "OpenTelemetry" generally, and the Fixed Point is defensible exactly as written — but a Practice distractor built on "profiles" would now also be sourced, which it was not before.

**2. The CNCF Glossary has no "Monitoring" entry.** Open Question #1's suggested fetch cannot be honoured as specified — `glossary.cncf.io/monitoring/` returns HTTP 404, and a search of the glossary confirms no standalone entry exists. The gap is closed from two better places instead: Google's SRE book ch. 6 gives a formal definition of monitoring, and the **CNCF TAG Observability whitepaper gives the exact known-unknowns / unknown-unknowns contrast §1 is built on, in CNCF's own voice** — which is a stronger citation for a CNCF exam than a glossary entry would have been. §1's central distinction is now sourced on both sides.

**3. RED is the weakest citation in this set — treat it as tier 4.** The method's original publication was the Weaveworks blog; Weaveworks is defunct and the CNCF TAG Observability whitepaper's link to it is to a dead host. The snapshot below is Grafana Labs' republication, written by Tom Wilkie, who created the method. That is the originating author on a vendor blog — it clears "not a third-party tutorial" but does not clear "official documentation." **USE is materially better sourced** (Brendan Gregg's own canonical page, which the CNCF whitepaper links as the live reference). Recommendation: the outline's fallback posture is still the right call — name RED and USE, keep them out of graded text, and let no Practice or Bearings item depend on either. If you want only one of them in prose, keep USE.

**4. Framing for §4's Grafana 🪝 Snag.** Assert the positive, not the negative: the cached Grafana snapshot says "Grafana is open source software" from Grafana Labs' own docs, and every *other* project named in that paragraph — Prometheus, Jaeger, Fluentd, Fluent Bit — has a sourced CNCF status in the corpus. Saying "Grafana is Grafana Labs' own open-source project, and unlike the four above it is not a CNCF project" would be asserting an unsourced negative in the second clause. Say the first clause, note that the CNCF projects in the paragraph are the ones the snapshots name as such, and let the reader draw it. Same reasoning that produced trap #99.

**5. "Utilization" means three different things in this chapter.** This is a drafting hazard and all three are now sourced, which makes it avoidable rather than invisible:
   - **Kubernetes:** a percentage of the containers' **resource request** (`k8s-docs-hpa-utilization-vs-requests`, new) — this is §3's payoff and what two shipped chapters point here for.
   - **Golden signals:** *saturation* is the "how full" signal, and the SRE book explicitly warns that "many systems degrade in performance before they achieve 100% utilization" (cached golden-signals snapshot).
   - **USE method:** *utilization* is "the average time that the resource was busy servicing work," a duration fraction, **not** a fraction of a request (`use-method-brendan-gregg`, new).

   §3 and §7 sit two sections apart and both use the word. Recommend §7 says "saturation" and never "utilization," so §3 keeps the word to itself.

**6. Three compatible but differently-worded definitions of observability are now cached.** OTel's primer ("understand a system from the outside… without knowing its inner workings… unknown unknowns"), the CNCF Glossary ("a system property that defines the degree to which the system can generate actionable insights"), and CNCF TAG ("a measure of how well internal states of a system can be inferred from knowledge of its external outputs"). **§1 should stay on the OTel primer's wording** — it is the one §7 and §8 pay off, and swapping in the glossary's phrasing would break the Zenith. The other two are available if §1 wants a second citation for the "it's a property, not a tool" beat, which the TAG whitepaper states directly.

**7. The error-budget quote has an uncaptured antecedent.** The verbatim sentence is "The difference between these two numbers is the 'budget'…" and the two numbers it refers to were not captured. **Do not paraphrase the antecedent.** The outline's fallback — error budget as one glossed clause after SLO — is now comfortably supported by the three *other* verbatim sentences in that snapshot, none of which has this problem. Use those.

**8. Fluentd's own CNCF-status sentence is grammatically broken.** fluentd.org prints "is at the Graduated project maturity level on 2019". It is verbatim and it is what the source says, but do not put it in reader-facing prose as a quote. State the graduation as fact, cite the snapshot, and write the sentence yourself. Also note this snapshot names a maturity level, so trap #99's prohibition applies: it may support prose, never a graded item.

**9. Pushgateway is narrower than the outline assumed, and this strengthens trap #93.** Prometheus's own practices page says "The only valid use case for the Pushgateway is for capturing the outcome of a service-level batch job" and separately warns "We only recommend using the Pushgateway in certain limited cases." The outline's phrasing ("short-lived jobs") comes from the overview page and is also verbatim, so both are defensible — but the practices page's "only valid use case" is the sharper sentence and makes a cleaner distractor set. Both are now cached; §4 can cite either.

**10. `prometheus-glossary` is the highest-yield single file here.** It closes exporter, client library, target, endpoint, job, instance, sample, time series, silence and notification in one page. §4 was flagged as the densest section in the chapter; it is now the best-sourced one.

---

### A1 · `cncf-glossary-observability-2026-08-31.md` (new)

```markdown
---
source_url: "https://glossary.cncf.io/observability/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary"
objectives_covered: ["D4.1"]
concepts_covered: ["observability", "actionable-insights", "observability-tools", "monitoring"]
---
# Observability — CNCF Cloud Native Glossary

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Definition

> "Observability is a system property that defines the degree to which the system can generate
> actionable insights. It allows users to understand a system's state from these external outputs
> and take (corrective) action."

## What is observed

> "Computer systems are measured by observing low-level signals such as CPU time, memory, disk
> space, and higher-level and business signals, including API response times, errors, transactions
> per second, etc. These observable systems are observed (or monitored) through specialized tools,
> so-called observability tools."

## Why it matters

> "Observable systems yield meaningful, actionable data to their operators, allowing them to
> achieve favorable outcomes (faster incident response, increased developer productivity) and less
> toil and downtime."

> "Consequently, how observable a system is will significantly impact its operating and development
> costs."

## Drafting guardrail

This entry treats "observed (or monitored)" as near-synonyms and is therefore **NOT** the source for
Ch 18 §1's observability-vs-monitoring distinction. Use the OTel primer for observability and
`cncf-tag-observability-whitepaper-2026-08-31.md` / `sre-book-monitoring-definitions-2026-08-31.md`
for monitoring. This snapshot is here for the "property of the system, not a tool" beat and for the
operating-cost consequence, both of which the other sources do not state as plainly.

## Not on this page

There is no standalone "Monitoring" entry in the CNCF Cloud Native Glossary.
`https://glossary.cncf.io/monitoring/` returned HTTP 404 on 2026-08-31.
```

---

### A2 · `cncf-tag-observability-whitepaper-2026-08-31.md` (new)

```markdown
---
source_url: "https://github.com/cncf/tag-observability/blob/main/whitepaper.md"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Cloud Native Computing Foundation — Technical Advisory Group (TAG) Observability, Observability Whitepaper"
objectives_covered: ["D4.1"]
concepts_covered: ["observability", "monitoring", "known-unknowns", "unknown-unknowns", "signals", "metrics", "logs", "traces", "profiles", "dumps", "red-method", "use-method"]
---
# CNCF TAG Observability — Observability Whitepaper

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Observability

> "observability is a measure of how well internal states of a system can be inferred from
> knowledge of its external outputs."

> "observability is not just using all the pretty and shiny tools."

> "You must be conscious about what outputs are coming out of your system."

## Monitoring, and the distinction — THE LOAD-BEARING PASSAGE FOR Ch 18 §1

> "Monitoring is called a system that can detect known unknowns -- as opposed to observability
> which emphasizes being able to find and reason about unknown unknowns as well."

> "Monitoring, traditionally, was a system admin or human operator (ops) concern"

> "ops folks had to infer the state of the system from external signals"

## Signals

The whitepaper enumerates **five** primary signals: metrics, logs, traces, profiles and dumps.
Of these it says:

> "they are commonly mentioned and probably what you're going to start with"

Individual definitions given:

> "Metrics are numeric representations of data."

> "Logs are one or more textual entries describing usage patterns, activities, and operations."

> "Distributed tracing is the technique of understanding what happened during a distributed
> transaction."

## ⚠ SIGNAL-COUNT DISAGREEMENT — read before drafting §2

This CNCF document's signal list (metrics, logs, traces, profiles, dumps) **differs from
OpenTelemetry's** (traces, metrics, logs, baggage — see `opentelemetry-signals-2026-08-23.md`),
and also differs from the OTel primer's own passing list of three (traces, metrics, logs).

Ch 18 §2's Fixed Point "four signals, not three" is a claim about **OpenTelemetry's Signals page
specifically** and must be attributed that way. Do not write "the four signals" as though it were a
universal or CNCF-wide taxonomy — this snapshot shows it is not. A distractor built on "profiles"
is now sourced.

## RED and USE

The whitepaper references both methods by name and links out to them. It does **not** define
either. Its RED link points to the Weaveworks blog (host now defunct); its USE link points to
`https://www.brendangregg.com/usemethod.html`. See `use-method-brendan-gregg-2026-08-31.md` and
`red-method-tom-wilkie-2026-08-31.md`.
```

---

### A3 · `sre-book-monitoring-definitions-2026-08-31.md` (new)

```markdown
---
source_url: "https://sre.google/sre-book/monitoring-distributed-systems/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Google Site Reliability Engineering book, ch. 6 'Monitoring Distributed Systems' (O'Reilly, CC BY-NC-ND)"
objectives_covered: ["D4.1"]
concepts_covered: ["monitoring", "white-box-monitoring", "black-box-monitoring", "alert", "root-cause", "why-monitor"]
---
# Monitoring — definitions (Site Reliability Engineering, ch. 6)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Companion snapshot to `sre-book-four-golden-signals-2026-08-23.md`, which is the same chapter.
This one carries the chapter's **Definitions** section, cached to close the Ch 18 §1 gap: the
corpus previously had a sourced definition of observability and none of monitoring.

## Definitions

> **Monitoring** — "Collecting, processing, aggregating, and displaying real-time quantitative data
> about a system"

> **White-box monitoring** — "Monitoring based on metrics exposed by the internals of the system,
> including logs, interfaces"

> **Black-box monitoring** — "Testing externally visible behavior as a user would see it"

> **Alert** — "A notification intended to be read by a human and that is pushed to a system such as
> a bug or ticket queue"

> **Root cause** — "A defect in a software or human system that, if repaired, instills confidence
> that this event won't happen again"

**Excerpt note.** The Monitoring definition as printed continues past "about a system" with a list
of examples. That continuation was not captured. Quote only as far as the text above runs; do not
extend it from memory.

## Why Monitor?

The chapter gives four reasons, each illustrated by a question:

> **Long-term trends** — "How big is my database and how fast is it growing?"

> **Alerting** — "Something is broken, and somebody needs to fix it right now!"

> **Building dashboards** — "Dashboards should answer basic questions about your service"

> **Debugging** — "Our latency just shot up; what else happened around the same time?"

## Drafting note for §1

These four reasons are the sharpest available support for the chapter's curiosity gap. Every one
of them is a question **chosen in advance** — which is precisely the property §1 contrasts against
observability's "unknown unknowns." The contrast is available without editorialising: monitoring's
own canonical text defines it by the questions you decided to ask.
```

---

### A4 · `opentelemetry-instrumentation-2026-08-31.md` (new)

```markdown
---
source_url: "https://opentelemetry.io/docs/concepts/instrumentation/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["instrumentation", "code-based-instrumentation", "zero-code-instrumentation", "signals", "telemetry"]
---
# OpenTelemetry — Instrumentation

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Instrumentation as the precondition for observability

> "For a system to be observable, it must be instrumented: that is, code from the system's
> components must emit signals."

## Two kinds

> **Code-based** — "Allow you to get deeper insight and rich telemetry from your application
> itself"

> **Zero-code** — "Great for getting started, or when you can't modify the application you need to
> get telemetry out of"

> Zero-code instrumentation "provide[s] rich telemetry from libraries you use and/or the
> environment your application runs in"

## Drafting note for §1 and §5

The zero-code sentence is the clean, sourced bridge to Ch 17 §5's mesh telemetry: it is OTel's own
statement that useful telemetry can come from a system the application did not opt into. §5's
mandatory Ch 17 anchor ("sometimes you get spans without instrumenting anything") can lean on this
rather than on the mesh material alone.

Ch 18 §1's ★ Fixed Point candidate on "properly instrumented" is in the **primer**
(`opentelemetry-observability-primer-2026-08-23.md`), not here — that page carries the sentence
about developers not needing to add more instrumentation to troubleshoot. Use the primer for that
beat and this snapshot for the precondition and the two kinds.
```

---

### A5 · `opentelemetry-collector-2026-08-31.md` (new)

```markdown
---
source_url: "https://opentelemetry.io/docs/collector/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["otel-collector", "vendor-agnostic", "telemetry-pipeline", "agent-vs-collector", "backends"]
---
# OpenTelemetry Collector

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Cached to close Ch 18 §2's blocking gap. Shipped Ch 17's Voyage Ahead already promised the reader
"one collector," so the term is not droppable.

## What it is

> "The OpenTelemetry Collector offers a vendor-agnostic implementation of how to receive, process
> and export telemetry data."

> "Vendor-agnostic way to receive, process and export telemetry data."

## Why use one

> "Removes the need to run, operate, and maintain multiple agents/collectors"

> "Supports open source observability data formats (e.g. Jaeger, Prometheus, Fluent Bit, etc.)
> sending to one or more open source or commercial backends"

> "In general we recommend using a collector alongside your service, since it allows your service
> to offload data quickly and the collector can take care of additional handling like retries,
> batching, encryption or even sensitive data filtering."

## Design objectives

> **Usability** — "Reasonable default configuration, supports popular protocols, runs and collects
> out of the box."

> **Performance** — "Highly stable and performant under varying loads and configurations."

> **Observability** — "An exemplar of an observable service."

> **Extensibility** — "Customizable without touching the core code."

> **Unification** — "Single codebase, deployable as an agent or collector with support for traces,
> metrics, and logs."

## ⚠ NOT CAPTURED — do not name the pipeline components

The words **receiver**, **processor** and **exporter** as named pipeline stages were not captured
verbatim from this page. §2 may say the Collector "receives, processes and exports" telemetry —
that phrasing is verbatim above — but must **not** present receivers/processors/exporters as a
named three-part taxonomy without a re-fetch. See manifest gap G-18c.

## Drafting note for §2 and §8

The Unification objective is the sourced version of §8's second synthesis beat: one codebase, three
signal types, deployable in two shapes. And "sending to one or more open source or commercial
backends" is the sourced separability claim — instrumentation and backend are different things,
which is the shape §8 says recurred all chapter (OTel exports / Jaeger receives; Prometheus stores /
Grafana reads; kubelet writes / agent ships).
```

---

### A6 · `opentelemetry-baggage-2026-08-31.md` (new)

```markdown
---
source_url: "https://opentelemetry.io/docs/concepts/signals/baggage/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["baggage", "signals", "context-propagation", "span-attributes"]
---
# OpenTelemetry — Baggage

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Baggage is Ch 18's Fixed Point 2 (the fourth signal, the one candidates drop) and a graded element
in Checkpoint 2. The corpus previously carried one sentence on it. This snapshot is the page.

## Definition

> "Contextual information that is passed between signals."

> Baggage is "a key-value store, which means it lets you propagate any data you like alongside
> context."

## What it is for

> "Baggage is best used to include information typically available only at the start of a request
> further downstream."

Examples the page gives: > "Account Identification, User IDs, Product IDs, and origin IPs."

## Propagation

> "Baggage means you can pass data across services and processes, making it available to add to
> traces, metrics, or logs in those services."

## Baggage is NOT span attributes

> "An important thing to note about baggage is that it is a separate key-value store and is
> unassociated with attributes on spans, metrics, or logs without explicitly adding them."

## Security caution

> "Sensitive Baggage items can be shared with unintended resources, like third-party APIs...making
> it visible to anyone inspecting your network traffic."

## Drafting note for §2 and §5

The "unassociated with attributes... without explicitly adding them" sentence is the sourced answer
to *why* baggage is a separate signal rather than a property of spans — which is exactly the fact
that makes trap #89 defensible rather than arbitrary. It is also the cleanest way to make §5's
return of baggage land: the thing being propagated is a store, not a field on the span.

The security caution is **not** exam surface and should not be graded. It is available if §2 wants
one concrete beat to keep a naming section from reading as a list.
```

---

### A7 · `opentelemetry-context-propagation-2026-08-31.md` (new)

```markdown
---
source_url: "https://opentelemetry.io/docs/concepts/context-propagation/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["context-propagation", "context", "propagation", "trace-id", "span-id", "w3c-tracecontext", "baggage"]
---
# OpenTelemetry — Context Propagation

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Cached to close Ch 18 §5's blocking gap. Context propagation is the mechanism the whole section
rests on: it is the answer to Soundings Q7 (what five independent log files cannot do between them).

## Context

> "Context is an object that contains the information for the sending and receiving service, or
> execution unit, to correlate one signal with another."

## Propagation

> "Propagation is the mechanism that moves context between services and processes."

## Context propagation

> "With context propagation, signals (traces, metrics, and logs) can be correlated with each other,
> regardless of where they are generated."

> "Context propagation allows traces to build causal information about a system across services
> that are arbitrarily distributed across process and network boundaries."

## How the correlation is carried

> "Service A includes a trace ID and a span ID as part of the context. Service B uses these values
> to create a new span that belongs to the same trace."

## The wire format

> "The default propagator uses the headers specified by the W3C TraceContext specification."

The page gives the header shape as `<version>-<trace-id>-<parent-id>-<trace-flags>`.

## Baggage

> "Baggage allows you to propagate arbitrary key-value pairs."

## Drafting note for §5

"Arbitrarily distributed across process and network boundaries" is the sourced sentence that closes
the loop shipped Ch 17 opened ("Break a monolith into microservices and one request becomes
twenty"). The Service A / Service B sentence is concrete enough to carry the mechanism without a
code sample, which matters because B1 rates D4 recall-and-recognition and §5 must not drift into
implementation.

W3C TraceContext is **not** exam surface at KCNA level. Name it at most once; do not grade it.
```

---

### A8 · `prometheus-data-model-2026-08-31.md` (new)

```markdown
---
source_url: "https://prometheus.io/docs/concepts/data_model/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["time-series", "metric-labels", "sample", "cardinality"]
---
# Prometheus — Data model

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Time series

> "Prometheus fundamentally stores all data as time series: streams of timestamped values belonging
> to the same metric and the same set of labeled dimensions."

## Identity — the sourced basis for Ch 18 §3's cardinality mechanic

> "Every time series is uniquely identified by its metric name and optional key-value pairs called
> labels."

> "The change of any label's value, including adding or removing labels, will create a new time
> series."

## Samples

> "Each sample consists of: a float64 or native histogram value [and] a millisecond-precision
> timestamp."

## Drafting note for §3

These two sentences together *are* the cardinality mechanic, stated as identity rather than as a
warning: a metric plus its label set defines the series, so changing a label value defines a
different one. §3 can teach cardinality as a consequence of the data model rather than as a rule to
memorise — which is the difference between a 🔭 Closer Look that earns its place and one that reads
as trivia. The operational warning is in
`prometheus-naming-labels-cardinality-2026-08-31.md`.
```

---

### A9 · `prometheus-naming-labels-cardinality-2026-08-31.md` (new)

```markdown
---
source_url: "https://prometheus.io/docs/practices/naming/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — metric and label naming practices"
objectives_covered: ["D4.1"]
concepts_covered: ["metric-labels", "cardinality"]
---
# Prometheus — Metric and label naming (LABELS section)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Closes Ch 18 §3's cardinality gap (Stage 1 Open Question #1, row 6 — non-blocking, now closed).

## The cost of a label

> "Every unique combination of key-value label pairs represents a new time series, which can
> dramatically increase the amount of data stored."

## High cardinality

> "Do not use labels to store dimensions with high cardinality (many different label values), such
> as user IDs, email addresses, or other unbounded sets of values."

## Redundant naming

> "Do not put the label names in the metric name, as this introduces redundancy and will cause
> confusion if the respective labels are aggregated away."

## Drafting note for §3

The outline's posture was: keep cardinality as a 🔭 Closer Look, not graded, unless this fetch
landed. It landed, with the concrete unbounded-set examples (user IDs, email addresses) that make
the idea teachable in two sentences. The Closer Look call is still the right one — cardinality is
not on the KCNA exam surface and B1 lists no trap for it — but it is now a sourced Closer Look
rather than an inferred one, which matters for Ethical Guardrail #8.

The redundant-naming line is **out of scope** for Ch 18. Cached only so the section is complete.
```

---

### A10 · `prometheus-glossary-2026-08-31.md` (new)

```markdown
---
source_url: "https://prometheus.io/docs/introduction/glossary/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — official glossary"
objectives_covered: ["D4.1"]
concepts_covered: ["exporters", "client-libraries", "pushgateway", "alertmanager", "target", "endpoint", "job", "instance", "sample", "time-series", "promql", "silence", "notification"]
---
# Prometheus — Glossary

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Highest-yield single page for Ch 18 §4, which the outline rates the densest sourced section in the
chapter. Ten of §4's introduced terms are defined here in the project's own words.

## Components

> **Exporter** — "An exporter is a binary running alongside the application you want to obtain
> metrics from."

> **Client library** — "A client library is a library in some language (e.g. Go, Java, Python,
> Ruby) that makes it easy to directly instrument your code."

> **Pushgateway** — "The Pushgateway persists the most recent push of metrics from batch jobs."

> **Alertmanager** — "The Alertmanager takes in alerts, aggregates them into groups, de-duplicates,
> applies silences, throttles, and then sends out notifications."

## What gets scraped

> **Target** — "A target is the definition of an object to scrape."

> **Endpoint** — "A source of metrics that can be scraped, usually corresponding to a single
> process."

> **Job** — "A collection of targets with the same purpose, for example monitoring a group of like
> processes replicated for scalability or reliability, is called a job."

> **Instance** — "An instance is a label that uniquely identifies a target in a job."

## Data

> **Sample** — "A sample is a single value at a point in time in a time series."

> **Time series** — "Prometheus time series are streams of timestamped values belonging to the same
> metric and the same set of labeled dimensions."

> **PromQL** — "PromQL is the Prometheus Query Language."

## Alerting

> **Silence** — "A silence in the Alertmanager prevents alerts, with labels matching the silence,
> from being included in notifications."

> **Notification** — "A notification represents a group of one or more alerts, and is sent by the
> Alertmanager to email, Pagerduty, Slack etc."

## Drafting note for §4

**Exporter vs client library is the discrimination worth teaching**, and this page makes it in one
line each: a client library instruments *your* code from the inside; an exporter is a separate
binary that gets metrics out of something you did not write. That is the same instrumentation /
backend separability §8 pays off, appearing a third time.

**Target, endpoint, job and instance are scope creep for KCNA.** They are cached for accuracy if
§4's figure needs correct labels (`ch18-fig04-prometheus-pull-architecture` shows Prometheus
scraping targets). Do not teach the four as vocabulary and do not grade them.
```

---

### A11 · `prometheus-pushgateway-practices-2026-08-31.md` (new)

```markdown
---
source_url: "https://prometheus.io/docs/practices/pushing/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — pushing metrics practices"
objectives_covered: ["D4.1"]
concepts_covered: ["pushgateway", "pull-model", "batch-jobs", "scraping"]
---
# Prometheus — When to use the Pushgateway

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

This is the sharp version of Ch 18 Fixed Point 3 and trap #93. The already-cached
`prometheus-overview-2026-08-23.md` says pushing "is supported via an intermediary gateway"; this
page says how narrow that is, in the project's own voice.

## What it is

> "The Pushgateway is an intermediary service which allows you to push metrics from jobs which
> cannot be scraped."

## How narrow the use case is

> "We only recommend using the Pushgateway in certain limited cases."

> "The only valid use case for the Pushgateway is for capturing the outcome of a service-level
> batch job."

> "A 'service-level' batch job is one which is not semantically related to a specific machine or job
> instance."

## Drafting note for §4

"The only valid use case" is a stronger and more quotable claim than the overview's "short-lived
jobs," and it builds a better distractor set: an item can now offer *plausible* push scenarios
(a long-running service that would rather push; a job tied to one specific machine) that the source
itself rules out. Both phrasings are cached and both are verbatim; §4 may use either, but the Fixed
Point should carry this one.

The figure spec for `ch18-fig04-prometheus-pull-architecture` calls for Pushgateway drawn as a
"visibly narrow" single inbound path. This snapshot is the justification for that visual choice —
it is not stylistic emphasis, it is what the source says.
```

---

### A12 · `prometheus-alertmanager-2026-08-31.md` (new)

```markdown
---
source_url: "https://prometheus.io/docs/alerting/latest/alertmanager/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — Alertmanager documentation"
objectives_covered: ["D4.1"]
concepts_covered: ["alertmanager", "grouping", "inhibition", "silencing", "routing", "receivers"]
---
# Prometheus — Alertmanager

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## What it does

> "The Alertmanager handles alerts sent by client applications such as the Prometheus server. It
> takes care of deduplicating, grouping, and routing them to the correct receiver integration such
> as email, PagerDuty, or OpsGenie. It also takes care of silencing and inhibition of alerts."

## The four functions

> **Grouping** — "Grouping categorizes alerts of similar nature into a single notification."

> **Inhibition** — "Inhibition is a concept of suppressing notifications for certain alerts if
> certain other alerts are already firing."

> **Silencing** — "Silences are a straightforward way to simply mute alerts for a given time."

> **Routing** — notifications are directed to "the correct receiver integration such as email,
> PagerDuty, or OpsGenie."

## Drafting note for §4

**Direction of the arrow, again.** The opening sentence says Alertmanager "handles alerts *sent by*
client applications such as the Prometheus server" — so Prometheus **pushes** to Alertmanager, while
it **pulls** from targets. §4 is organised around arrow direction; this is the one place inside
Prometheus's own architecture where the arrow reverses, and a reader who has just learned "Prometheus
pulls" can be tripped by it. Worth one explicit sentence so it reads as a distinction rather than a
contradiction.

Grouping / inhibition / silencing are **below KCNA surface**. Name Alertmanager and what it is for;
do not teach the four functions and do not grade them.
```

---

### A13 · `prometheus-promql-basics-2026-08-31.md` (new)

```markdown
---
source_url: "https://prometheus.io/docs/prometheus/latest/querying/basics/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["promql", "time-series"]
---
# Prometheus — Querying basics (PromQL)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## What PromQL is

> "Prometheus provides a functional query language called PromQL (Prometheus Query Language) that
> lets the user select and aggregate time series data in real time."

## Where results go

> "In the Prometheus UI, the 'Table' tab is for instant queries and the 'Graph' tab for range
> queries."

> "Other programs can fetch the result of a PromQL expression via the HTTP API."

## Drafting guardrail

The outline is explicit that PromQL is **not** on this chapter's teaching surface: it was
deliberately excluded from `kb_tags.commands` because it is a query language, not a kubectl verb,
and §4 teaches that it exists and what it is for, not syntax. **No PromQL syntax is cached in this
snapshot and none should be drafted.** One sentence — a query language for selecting and
aggregating time series — is the whole of §4's obligation.

The HTTP API sentence is the sourced link to Grafana: Grafana reads what Prometheus stores through
that API rather than being part of Prometheus. That is §8's separability shape appearing again,
and it is worth one clause.
```

---

### A14 · `k8s-docs-hpa-utilization-vs-requests-2026-08-31.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D4.1", "D2.3"]
concepts_covered: ["utilization-relative-to-requests", "metrics-api", "metrics-server", "hpa", "resource-requests"]
---
# HorizontalPodAutoscaler — utilization is a percentage of the *request*

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

> **WHY THIS SNAPSHOT EXISTS.** Stage 1 did not flag this as a gap, but a corpus search found that
> **"utilization relative to requests" had no source anywhere in the 276 cached files.** It is
> pinned into Ch 18 §3 by two shipped chapters (`chapter-05:969`, `chapter-17:1387`), and it is
> graded three times — Soundings Q4, Checkpoint 1 item 4 (`*[retrieval: ch5]*`), and one of the
> four interleaved Practice items. It was about to be drafted from memory. It is now sourced.

## The denominator

> "Then, if a target utilization value is set, the controller calculates the utilization value as a
> percentage of the equivalent resource request on the containers in each Pod."

*(Editorial: inline documentation links removed from the sentence above; wording otherwise
unaltered.)*

## What happens with no request set

> "Please note that if some of the Pod's containers do not have the relevant resource request set,
> CPU utilization for the Pod will not be defined and the autoscaler will not take any action for
> that metric."

## Where the numbers come from

> "The common use for HorizontalPodAutoscaler is to configure it to fetch metrics from aggregated
> APIs (`metrics.k8s.io`, `custom.metrics.k8s.io`, or `external.metrics.k8s.io`). The
> `metrics.k8s.io` API is usually provided by an add-on named Metrics Server, which needs to be
> launched separately."

## The scaling algorithm

> `desiredReplicas = ceil[ currentReplicas × ( currentMetricValue / desiredMetricValue ) ]`

## Drafting note for §3

**The second quote is the payoff.** The outline asks §3 to pay off the denominator "concretely: the
number an autoscaler and a dashboard both report is a ratio, and the denominator is what the Pod
*asked for*, not what the node has." The no-request-set sentence proves it from the other side — a
Pod with no request has **no defined utilization at all**, which is only possible if the request is
the denominator. That is a better teaching move than restating the ratio, and it is sourced.

**The third quote is a bonus for §3's other half.** "which needs to be launched separately" is
Kubernetes' own statement of the Ch 10 §3 named pattern, arriving from the autoscaling side rather
than the `kubectl top` side. §3 may use it, but the pattern phrase itself —
***an object without its component does nothing*** — is the book's and must be quoted verbatim from
the ledger, never paraphrased from this page. See the B7 errata block.

**Do not draft the algorithm.** Cached for accuracy only. It is not KCNA surface and the outline
lists no objective for it.
```

---

### A15 · `fluentd-architecture-2026-08-31.md` (new)

```markdown
---
source_url: "https://www.fluentd.org/architecture"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Fluentd project (CNCF graduated)"
objectives_covered: ["D4.1", "D2.3"]
concepts_covered: ["fluentd", "unified-logging-layer", "plugins", "log-collection", "cncf-graduated"]
---
# Fluentd — Architecture

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

The corpus had Fluent Bit but not Fluentd. Ch 18 §6 introduces both and the B7 ledger flags the
surface-form asymmetry (Fluentd one word, Fluent Bit two) as itself exam-adjacent, so the parent
project needed its own snapshot.

## Unified logging layer

> "Fluentd tries to structure data as JSON as much as possible: this allows Fluentd to unify all
> facets of processing log data"

## Sources and outputs

> Fluentd "connects dozens of data sources and data outputs"

## Plugin system

> "Fluentd has a flexible plugin system that allows the community to extend its functionality."

> "Our 500+ community-contributed plugins"

## Footprint

> "The vanilla instance runs on 30-40MB of memory and can process 13,000 events/second/core"

## CNCF status

> "Fluentd was accepted to Cloud Native Computing Foundation on November 8, 2016 and is at the
> Graduated project maturity level on 2019"

## ⚠ TWO GUARDRAILS ON THAT LAST QUOTE

1. **Do not print it as a quote.** The sentence is verbatim and it is what fluentd.org says, but the
   grammar is broken ("is at the Graduated project maturity level on 2019"). State the graduation as
   fact in the book's own voice and cite this snapshot.
2. **Trap #99 applies.** This snapshot names a current maturity level. Per B3 and the outline's
   §7 Practice constraint, **no item may be graded on a project's current CNCF maturity level.** The
   status may support prose. It may not support a question.

## Drafting note for §6

The already-cached `fluent-bit-overview-2026-08-23.md` states the relationship from the child's
side — Fluent Bit created 2014, a sub-project of Fluentd, both commonly deployed as node-level
DaemonSets. Between the two snapshots §6 has the full picture without needing a third fetch. The
footprint numbers are the sourced reason a *lightweight* agent exists at all, which is the honest
answer to "why are there two of these" — but they are detail, not surface. One clause at most.
```

---

### A16 · `sre-book-service-level-objectives-2026-08-31.md` (new)

```markdown
---
source_url: "https://sre.google/sre-book/service-level-objectives/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Google Site Reliability Engineering book, ch. 4 'Service Level Objectives' (O'Reilly, CC BY-NC-ND)"
objectives_covered: ["D4.1"]
concepts_covered: ["sli", "slo", "sla", "reliability"]
---
# SLI, SLO, SLA — definitions (Site Reliability Engineering, ch. 4)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Closes Stage 1 **Open Question #2**: SLA had no cached source, and the B7 ledger rules it
"not glossary-only" precisely because it will appear as a distractor — a distractor the reader
cannot look up is a badly built distractor. It can now be looked up.

## The three terms

> **SLI** — "An SLI is a service level indicator—a carefully defined quantitative measure of some
> aspect of the level of service that is provided."

> **SLO** — "An SLO is a service level objective: a target value or range of values for a service
> level that is measured by an SLI."

> **SLA** — "Finally, SLAs are service level agreements: an explicit or implicit contract with your
> users that includes consequences of meeting (or missing) the SLOs they contain."

## The discriminating test — trap #92's answer, in one sentence

> "An easy way to tell the difference between an SLO and an SLA is to ask 'what happens if the SLOs
> aren't met?': if there is no explicit consequence, then you are almost certainly looking at an
> SLO."

## Drafting note for §7

**Use the OTel primer for SLI and SLO; use this page for SLA and for the discrimination.** The
primer's definitions are the ones §7 is built on ("a good SLI measures your service from the
perspective of your users"; an SLO is "the means by which reliability is communicated to an
organization") and they carry the user-perspective framing the section needs. This page's SLI/SLO
definitions are cached alongside them for cross-checking, not to replace them — the two sources
agree in substance and differ in emphasis, and mixing the wording mid-section would muddy both.

The consequence test is the single best asset here. It gives §7 a *procedure* for the SLO/SLA
distinction rather than two definitions to hold side by side, and it converts trap #92 from a
memory item into a reasoning item. The outline gives SLA "one clause, by contrast" — this sentence
is that clause.

Note that the SLA definition contains "the SLOs they contain," which makes the dependency direction
explicit: an SLA is built out of SLOs, which are built out of SLIs. §7's stated dependency order is
correct and now sourced end to end.
```

---

### A17 · `sre-book-error-budgets-2026-08-31.md` (new)

```markdown
---
source_url: "https://sre.google/sre-book/embracing-risk/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Google Site Reliability Engineering book, ch. 3 'Embracing Risk' (O'Reilly, CC BY-NC-ND)"
objectives_covered: ["D4.1"]
concepts_covered: ["error-budget", "reliability-vs-velocity", "slo"]
---
# Error budgets (Site Reliability Engineering, ch. 3)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Closes Stage 1 Open Question #1, row 5 (non-blocking). The outline's fallback was to keep error
budgets as one glossed clause after SLO. That remains the right call — this snapshot makes it a
*sourced* clause.

## The tension the budget resolves

> "Product development performance is largely evaluated on product velocity, which creates an
> incentive to push new code as quickly as possible. Meanwhile, SRE performance is evaluated based
> upon reliability of a service, which implies an incentive to push back against a high rate of
> change."

## What the budget permits

> "As long as the uptime measured is above the SLO—in other words, as long as there is error budget
> remaining—new releases can be pushed."

## Spending it

> "If a problem causes us to fail 0.0002% of the expected queries for the quarter, the problem
> spends 20% of the service's quarterly error budget."

## ⚠ ONE QUOTE WITH AN UNCAPTURED ANTECEDENT — do not paraphrase

> "The difference between these two numbers is the 'budget' of how much 'unreliability' is remaining
> for the quarter."

**"These two numbers" was not captured.** Do not write out what they refer to, and do not
reconstruct the arithmetic from memory. If §7 wants the budget-as-a-difference framing, re-fetch the
page first. Everything §7 actually needs is in the three quotes above, none of which has this
problem — in particular, **"as long as there is error budget remaining—new releases can be pushed"**
is self-contained and is the whole idea in one clause.

## Drafting note for §7

The velocity/reliability quote is the sourced answer to *why* an error budget exists, and it is the
only sentence in this chapter's whole corpus that connects observability back to how organisations
actually behave. That makes it a strong candidate for §7's one-clause treatment — better than
defining the budget mechanically, because the mechanism is exactly the part that is not KCNA
surface.

**Keep it ungraded.** B1 lists no trap for error budgets and the outline routes no item to them.
```

---

### A18 · `use-method-brendan-gregg-2026-08-31.md` (new)

```markdown
---
source_url: "https://www.brendangregg.com/usemethod.html"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Brendan Gregg — author and originator of the USE Method; the reference linked by the CNCF TAG Observability whitepaper"
objectives_covered: ["D4.1"]
concepts_covered: ["use-method", "utilization", "saturation", "errors", "resource-bottlenecks"]
---
# The USE Method

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

**Authority note.** This is the method's originating publication by its author, and it is the live
link the CNCF TAG Observability whitepaper points to for USE. It is a personal technical site rather
than vendor or standards documentation — tier 3 by the stage's priority order. Better sourced than
RED (see `red-method-tom-wilkie-2026-08-31.md`).

## What it is

> "The Utilization Saturation and Errors (USE) Method is a methodology for analyzing the
> performance of any system."

## The three terms

> **Utilization** — "the average time that the resource was busy servicing work"

> **Saturation** — "the degree to which the resource has extra work which it can't service, often
> queued"

> **Errors** — "the count of error events"

## What it is for

> "It directs the construction of a checklist, which for server analysis can be used for quickly
> identifying resource bottlenecks or errors."

> "The USE Method helps you identify which metrics to use"

## Origin

> "I developed the USE Method to teach others how to solve common performance issues quickly,
> without overlooking important areas."

## ⚠ VOCABULARY COLLISION — read before drafting §7

**"Utilization" now means three different things inside Chapter 18, and all three are sourced:**

| Meaning | Source | Section |
|---|---|---|
| A percentage of the containers' **resource request** | `k8s-docs-hpa-utilization-vs-requests-2026-08-31.md` | §3 |
| The **golden signal** "saturation" — how full the service is; latency rises before 100% | `sre-book-four-golden-signals-2026-08-23.md` | §7 |
| **The average time a resource was busy** — a duration fraction | this snapshot | §7 |

§3 and §7 sit two sections apart. **Recommendation: §7 says "saturation" and never "utilization,"**
so §3 keeps the word to itself and the reader's §3 encoding is not overwritten forty minutes later.
The USE method's own U is unavoidable if USE is named — which is a further argument for the
outline's fallback posture of naming it only, in one non-graded clause.

Per the outline: no Practice or Bearings item may depend on USE.
```

---

### A19 · `red-method-tom-wilkie-2026-08-31.md` (new)

```markdown
---
source_url: "https://grafana.com/blog/the-red-method-how-to-instrument-your-services/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Grafana Labs, article by Tom Wilkie — the method's originator. TIER-4 CAVEAT: vendor blog, not official documentation. See guardrail below."
objectives_covered: ["D4.1"]
concepts_covered: ["red-method", "rate", "errors", "duration", "use-method"]
---
# The RED Method

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## ⚠ AUTHORITY GUARDRAIL — READ FIRST

**This is the weakest citation in Chapter 18's corpus.** RED's original publication was on the
Weaveworks blog; Weaveworks is defunct and the CNCF TAG Observability whitepaper's RED link now
points to a dead host. What survives is Grafana Labs' republication, **written by Tom Wilkie, who
created the method**. That clears the stage's "not a third-party tutorial" bar — it is the
originating author — but it does **not** clear "official documentation," and no CNCF or Linux
Foundation source defines RED.

**Consequence, per the outline's stated fallback posture:** name RED, do not build teaching weight
on it, and **let no Practice question, Taking Your Bearings item, or Soundings question depend on
it.** If §7 keeps only one of the two methods in prose, keep USE — it is better sourced.

## The three metrics

> **Rate** — "the number of requests per second"

> **Errors** — "the number of those requests that are failing"

> **Duration** — "the amount of time those requests take"

## Why it exists alongside USE

> "The USE Method doesn't really apply to services; it applies to hardware, network disks, things
> like this. We really wanted a microservices-oriented monitoring philosophy, so we came up with
> the RED Method."

## Origin

Tom Wilkie "created [the RED Method] in 2015" after "a new employee asked what his monitoring
philosophy was."

## Drafting note for §7

The USE/RED contrast quote is the most useful thing on this page and it is the one that justifies
mentioning both at all: **USE is for resources, RED is for services.** That is a one-sentence
complementarity the outline asks §7 to convey, and it comes from the person who drew the line. It
also lands the Ch 17 §3 microservices anchor a second time — RED exists *because* one service became
twenty.

B1 gap **G21** named golden signals and RED/USE together. Golden signals were closed on 2026-08-23;
USE closed cleanly this run; **RED is closed only at tier 4.** G21 should be recorded as
substantially-but-not-fully closed rather than closed.
```
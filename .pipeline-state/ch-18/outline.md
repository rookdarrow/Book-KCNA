I have everything I need. Here is the Stage 1 output.

I read both binding contracts, the arc-outline block, B1's D4.1 concept and trap inventories, B4's budget, B3's retrieval architecture, and every observability snapshot in the 168-file corpus. I verified all eight inbound cross-bearings into Ch 18 by line number against shipped Chapters 1–17. **Three sections are pinned by number** (§1 ×2, §3 ×3, §6 ×2); §6 additionally has its B6 title quoted verbatim by a shipped pointer. Six sourcing gaps are drafting-blocking and are carried to Open Questions rather than planned around silently.

````
---
chapter: 18
chapter_type: "content"
title: "Reading the Instruments"
subtitle: "Four signals, and the question they exist to answer"
exam_domain: "Cloud Native Architecture (competency: Observability)"
domain_weight_pct: 5
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE — CHANGED FROM B2/B3, and the change is forced.
#-- The arc outline proposes "Four signals, one question: is the service
#-- doing what users expect?" — eleven words, over this stage's ten-word
#-- limit. Two things also argue against it independently of length:
#--   (a) "is the service doing what users expect" is the OpenTelemetry
#--       primer's VERBATIM definition of reliability [source:
#--       opentelemetry-observability-primer-2026-08-23], which §7 owns and
#--       §8 pays off. Printing it on the title page spends the Zenith.
#--   (b) B6 titles §8 "One Question, Four Instruments." A subtitle that
#--       already IS that sentence leaves §8 with nothing to land.
#-- The replacement keeps the "four signals" frame (§2 material, and
#-- already promised to the reader by shipped Ch 17's Voyage Ahead: "Four
#-- signals, one collector, a database that pulls instead of being pushed
#-- to") and withholds the question itself. Nine words.
#-- No shipped chapter quotes this subtitle, so it is free to change.

#-- EXAM_DOMAIN — ONE DOMAIN, ONE COMPETENCY.
#-- D4 Cloud Native Architecture has three competencies; shipped Ch 17
#-- carries two and hands this one over by name in its Voyage Ahead. The
#-- competency names ARE sourced, contrary to a stale note in shipped
#-- Ch 17 — see Open Questions #7. lf-kcna-program-changes-2026-08-23
#-- lists "Cloud Native Architecture - 12%": Observability; Cloud Native
#-- Ecosystem and Principles; Cloud Native Community and Collaboration.
#--
#-- ⚠ THE IN-CHAPTER METADATA LINE MUST CARRY 12%, NOT 5%.
#-- 12% is the published weight of D4 [source: cncf-kcna-certification-
#-- page-2026-08-23]. The 5% above is this book's AUTHORED allocation of
#-- that 12% between Ch 17 and Ch 18 (7 + 5). CNCF publishes four domain
#-- weights and no competency weights — B1 gap G33, B2 disclosure #1.
#-- Shipped Ch 16 and Ch 17 both made this ruling and both honor it in
#-- prose. Match that treatment exactly; do not present 5% as CNCF data.

#-- COMPLEXITY — "mixed". B1 rates D4 "recall and recognition: lots of
#-- names, few mechanics, the highest breadth-to-depth ratio in the exam,"
#-- which argues procedural-adjacent. But §5 (a request becoming a tree of
#-- spans across process boundaries) and §1 (unknown unknowns) are genuine
#-- model-building, and §4 has real mechanics in the pull model. Mixed is
#-- the honest tag. The practical consequence for drafting: §2, §6 and the
#-- naming half of §7 need memorable STRUCTURE, not scaffolding; §1 and §5
#-- need scaffolding and are the two places to spend it.

#-- NOVELTY — "moderate". Nothing here is paradigm-shifting for a reader
#-- who has reached Chapter 18, and one thing is close to familiar: the
#-- metrics pipeline was taught in Ch 13 §7. The genuinely new idea is
#-- §1's — that you can ask a system a question you did not plan for.

#-- PREREQ — heavy, and heavier than the arc outline's "standard" depth
#-- band implies. Depth band and prerequisite load are different axes: the
#-- material is shallow, the dependency graph is not. This is the LAST
#-- content chapter, B3 sets retrieval at the 25% CEILING here (most
#-- accumulated decay in the book), and NOTHING in this chapter is taught
#-- from zero. Five mandatory named anchors, from five different chapters:
#--   Ch 5 §7  probes = health checking, NOT observability      -> §1
#--   Ch 5 §8  requests as the denominator of "utilization"     -> §3
#--   Ch 13 §7 metrics-server, and its stated autoscaling-only
#--            scope; ch13-fig04 is RETRIEVED, not redrawn      -> §3
#--   Ch 6 §7  node-level log agents ship as DaemonSets         -> §6
#--   Ch 17 §5 mesh telemetry, generated without code changes   -> §5
#-- Plus the book's most-reinforced retrieval phrase, BY NAME:
#--   Ch 10 §3 "an object without its component does nothing"   -> §3
#-- That last one is quoted VERBATIM in all 24 of its uses across Ch 3, 6,
#-- 10, 11, 13 and 17, including a graded Practice option. It is not
#-- paraphrasable here. See the B7 errata block: getting this wording wrong
#-- is the clearest case in the commission of a ledger defect reaching
#-- shipped text.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "standard" — 5
#-- points, one competency, six arcs. Planning signal only, NOT a target.
#--
#-- SECTION NUMBERING: three sections are pinned by published pointers.
#--   chapter-01:272  -> Ch 18 §1   observability under the current blueprint
#--   chapter-05:860  -> Ch 18 §1   health checking is not observability
#--   chapter-05:969  -> Ch 18 §3   utilization relative to requests
#--   chapter-13:1336 -> Ch 18 §3   metrics-server versus a monitoring system
#--   chapter-17:1387 -> Ch 18 §3   utilization relative to requests
#--   chapter-13:1354 -> Ch 18 §6   node-level logging agents
#--   chapter-15:526  -> Ch 18 §6   lines from everywhere   << TITLE QUOTED
#--   chapter-06:890  -> Ch 18      node-level log collection  (no §; free)
#-- chapter-15:526 quotes B6's §6 title as its pointer text, which fixes
#-- the TITLE as well as the number. "Lines From Everywhere" is immovable.
#-- §2, §4, §5, §7 and §8 are unpinned and take B6's titles unchanged.
#--
#-- HEADING FORM: `## <difficulty> §N — Title`, per B6 recommendation #3
#-- and matching shipped Ch 5–8 and Ch 13/17. Zenith section carries ☀️
#-- per B6 recommendation #4 and shipped Ch 13/17 practice.

sections:
  - name: "What You Can Ask, and What You Already Know"
    objectives: ["D4.1"]
    requires_figure: true
    figure_anchor: "ch18-fig01-monitoring-vs-observability"
    checkpoint_after: false

  - name: "Four Signals"
    objectives: ["D4.1"]
    requires_figure: true
    figure_anchor: "ch18-fig02-otel-four-signals"
    checkpoint_after: false

  - name: "Numbers Over Time"
    objectives: ["D4.1", "D2.3"]
    requires_figure: false      #-- RETRIEVES ch13-fig04, does not redraw it
    figure_anchor: null
    checkpoint_after: true

  - name: "Pulling, Not Being Pushed"
    objectives: ["D4.1"]
    requires_figure: true
    figure_anchor: "ch18-fig04-prometheus-pull-architecture"
    checkpoint_after: false

  - name: "Following One Request"
    objectives: ["D4.1"]
    requires_figure: true
    figure_anchor: "ch18-fig03-trace-spans-across-services"
    checkpoint_after: true

  - name: "Lines From Everywhere"
    objectives: ["D4.1", "D2.3"]
    requires_figure: true
    figure_anchor: "ch18-fig06-cluster-logging-architectures"
    checkpoint_after: false

  - name: "Is the Service Doing What Users Expect"
    objectives: ["D4.1"]
    requires_figure: true
    figure_anchor: "ch18-fig05-sli-slo-golden-signals"
    checkpoint_after: true

  - name: "One Question, Four Instruments"
    objectives: ["D4.1"]
    requires_figure: true
    figure_anchor: "ch18-zenith-instruments-answer-one-question"
    checkpoint_after: false

#-- §3 and §6 carry a second objective tag deliberately. Both k8s.io
#-- snapshots they rest on (resource-metrics-pipeline, logging-architecture)
#-- are tagged D2.3 in their own frontmatter, and Ch 13 owns D2.3. The dual
#-- tag is the honest record that these two sections are seams, not new
#-- territory, and it tells the question-writing stage that items drawn
#-- from them are legitimately interleaved rather than off-domain.

# --- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ---
soundings_planned:
  question_count: 8
  topics:
    - "probes as a yes/no signal to the kubelet, producing no history (Ch 5 §7)"
    - "what metrics-server is scoped to, and what it keeps no record of (Ch 13 §7)"
    - "why `kubectl top` fails on a cluster that is otherwise healthy (Ch 13 §7 / Ch 10 §3)"
    - "what 'utilization' is measured against when an autoscaler reads it (Ch 5 §8 / Ch 17 §7)"
    - "why log collection is a per-node job rather than a per-app one (Ch 6 §7 / Ch 13 §7)"
    - "why `kubectl logs` stops being able to answer a question (Ch 13 §3)"
    - "what one service's logs cannot tell you when a request crosses five (Ch 17 §3)"
    - "what a mesh sidecar can report on without the app knowing (Ch 17 §5)"

# --- Skill v5.3 Part 8: practice-question budget ---
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 17
  total_this_chapter: 40
#-- B4's table says 10 Bearings. B4 also says, in the same file, that "the
#-- 10 is a contract to exceed, not a target to hit," and shipped Ch 13
#-- (budgeted at 10) carries three checkpoints of six. Eight sections and
#-- three distinct arcs cannot be served by two checkpoints without leaving
#-- §4–§7 untested until the end. 15 across three, at the skill's five-per-
#-- checkpoint floor, is the smallest structure that covers the chapter.
#-- Practice stays at 17 exactly: B4's weight-proportional derivation,
#-- 15 + 2 x (5 - 4) = 17. Do not change it — the derivation reproduces the
#-- published 44/28/16/12 split to within 1.1 points and Ch 18 is one of
#-- its terms.

kb_tags:
  objectives: ["D4.1"]
  concepts:
    - "observability"
    - "monitoring"
    - "unknown-unknowns"
    - "instrumentation"
    - "telemetry"
    - "opentelemetry"
    - "signals"
    - "traces"
    - "metrics"
    - "logs"
    - "baggage"
    - "otel-collector"
    - "time-series"
    - "metric-labels"
    - "cardinality"
    - "metrics-server-vs-monitoring"
    - "utilization-relative-to-requests"
    - "prometheus"
    - "pull-model"
    - "scraping"
    - "service-discovery"
    - "exporters"
    - "client-libraries"
    - "pushgateway"
    - "promql"
    - "alertmanager"
    - "grafana"
    - "distributed-tracing"
    - "span"
    - "root-span"
    - "trace-id"
    - "context-propagation"
    - "jaeger"
    - "cluster-logging-architecture"
    - "node-level-logging-agent"
    - "fluentd"
    - "fluent-bit"
    - "sidecar-logging"
    - "log-rotation"
    - "reliability"
    - "sli"
    - "slo"
    - "sla"
    - "error-budget"
    - "four-golden-signals"
    - "red-method"
    - "use-method"
  commands:
    - "kubectl-top"        #-- RETRIEVED from Ch 13 §7, not introduced here
    - "kubectl-logs"       #-- RETRIEVED from Ch 13 §3, not introduced here
#-- Both commands are already owned. They appear so the research stage
#-- resolves the right shards; they are not this chapter's teaching surface.
#-- PromQL is a query language, not a kubectl verb, and is deliberately not
#-- listed here — §4 teaches that it exists and what it is for, not syntax.

figures_planned:
  - "ch18-fig01-monitoring-vs-observability"
  - "ch18-fig02-otel-four-signals"
  - "ch18-fig03-trace-spans-across-services"
  - "ch18-fig04-prometheus-pull-architecture"
  - "ch18-fig05-sli-slo-golden-signals"
  - "ch18-fig06-cluster-logging-architectures"   #-- ADDED beyond B3's list
  - "ch18-zenith-instruments-answer-one-question"
---
````

# Chapter 18 Outline — Reading the Instruments

## Chapter-type note (read first)

`content`. Full contract applies: witty subtitle, Attention Budget, epigraph, Soundings, Why This Chapter Matters, What You'll Learn, ≥2 Taking Your Bearings, Exam Alert + Practice Questions, Chapter Summary, The Voyage Ahead. One Zenith illustration, exactly one, at §8.

Two chapter-level facts the drafting stage must not lose:

- **The metadata line carries 12%, not 5%.** See the frontmatter comment. This is the third chapter in a row to make this ruling and the first two shipped honoring it.
- **This is the last content chapter.** The Voyage Ahead hands off to Ch 19 (synthesis), not to more material. Its job is to close Domain 4 and turn the reader toward review — B3 sets retrieval at the 25% ceiling here precisely because everything after this point is assessment.

---

## 1. Why This Chapter Matters

Shipped Ch 17 already opened the loop, in its own Voyage Ahead: *"Every architectural choice in this chapter made systems easier to change and harder to see. Break a monolith into microservices and one request becomes twenty. Replace machines instead of patching them and the machine you want to inspect is gone. Scale to zero and the thing you want to ask a question about is not running."* That is this chapter's curiosity gap, already primed, and the drafting stage should pick it up rather than open a new one.

The stakes are the reader's own experience of the previous chapter. Everything in Ch 17 was a trade: loose coupling bought changeability and spent visibility. Ch 18 is the bill arriving. The identity frame follows from that — practitioners do not add observability because a framework told them to; they add it because at some point they were asked a question about a running system and had no way to answer it. That is the moment the chapter is about.

The curiosity gap that carries the chapter itself: **you cannot dashboard your way out of a question you did not know to ask.** Open it in the first 500 words, leave it open through §2–§6 while the reader accumulates four instruments, and resolve it at §7 where reliability turns out to be one question, and at §8 where the four instruments turn out to be four ways of asking it. Do not resolve it early.

One honesty note belongs here and not in the Exam Alert: the reader arriving from third-party prep has been told observability is a domain of its own. It is not, on the current blueprint. Say so plainly, point at Ch 1 for what changed, and say that the material did not stop being tested — it stopped being separately weighted. Getting the tone right matters; this reads as a demotion and is not one.

---

## 2. What You'll Learn

Four to six outcomes, active verbs. Draft from these:

- **Distinguish** observability from monitoring by what each one lets you ask, not by which tool implements it
- **Name** all four OpenTelemetry signals — and know which one candidates drop
- **Explain** why Prometheus pulls, and the one narrow case in which anything pushes
- **Trace** a single request across service boundaries, and say what a span is that a trace is not
- **Distinguish** an SLI from an SLO, and state the four golden signals
- **Choose** the right instrument for a question, rather than reaching for the one you know (the wry outcome; it is also the Zenith)

---

## 3. Soundings plan — 8 questions

Content chapter, so 8. Per B3, every question sources from B2's Prerequisites column, which makes each one a free spaced-retrieval event as well as a calibration instrument. All eight are answerable from shipped chapters; none requires this chapter.

| # | Topic | Tests | Why it earns its place as a pre-test |
|---|---|---|---|
| 1 | A probe reports a container unhealthy. What record of that does the cluster keep? | Ch 5 §7 — probes are a yes/no signal to the kubelet | The reader who thinks probes are monitoring will read §1 differently once they've noticed a probe produces no history |
| 2 | What can you not ask metrics-server? | Ch 13 §7 — its stated autoscaling-only scope | Surfaces the §3 distinction as a *gap the reader already has*, rather than a new fact |
| 3 | `kubectl top` returns an error on a healthy cluster. Why? | Ch 13 §7 + the Ch 10 §3 named pattern | The book's most-reinforced retrieval phrase, tested cold at the 90% mark. If this one misses, the whole pattern has decayed |
| 4 | An autoscaler reports a Pod at "80% utilization." Eighty percent of what? | Ch 5 §8 — requests as the denominator | Two shipped chapters point at §3 for this. Pre-testing it tells the reader whether §3 is revision or repair |
| 5 | Why does cluster log collection run one agent per node instead of one per application? | Ch 6 §7 + Ch 13 §7 | Sets up §6 from the workload-resource side the reader already owns |
| 6 | You need a container's logs from three restarts ago. Can `kubectl logs` give them to you? | Ch 13 §3 | The reader who says yes has not yet met the reason §6 exists |
| 7 | A request crosses five services. Each logs independently. What question can the five log files not answer between them? | Ch 17 §3 — microservices | The strongest pre-test in the set: it makes the reader *feel* the gap §5 fills, without naming a single §5 term |
| 8 | A mesh sidecar reports per-service latency for an app that was never instrumented. How? | Ch 17 §5 — telemetry without code changes | Distinguishes "the platform can see it" from "the application reports it," which §5 needs |

### FIXED-POINT SPOILER CHECK

The chapter's five Fixed Points are:

1. Observability is asking questions you did not plan for; monitoring watches indicators you chose in advance (§1)
2. Four signals, not three — traces, metrics, logs, **and baggage** (§2)
3. Prometheus **pulls**; pushing exists only through the Pushgateway, for short-lived jobs (§4)
4. A span is one unit of work; a trace is the whole path, one or more spans, beginning at the root span (§5)
5. SLI is the measurement; SLO is the objective (§7)

Checked one by one against the eight questions above: **none is revealed.** Q1 and Q7 come closest and are the two to watch during drafting.

- **Q1** approaches FP1 from the probe side and asks what the cluster *records*. It must not use the words "observability" or "monitoring" in the stem, and the answer rationale must stop at "a probe produces no history" without stating the distinction. The distinction is §1's to make.
- **Q7** approaches FP4 from the microservices side. It must not use "span," "trace," or "root span" in the stem or the answer. It asks what five log files *cannot* answer; the name for the thing that can is §5's.
- **Q2** and **Q4** test material shipped Ch 13 and Ch 5 already taught, so they are genuine "did you arrive knowing" questions rather than reveals. §3's job is to extend both, not to introduce either.

Rubric is the standard 6+ / 3–5 / 0–2 tiering. Worth a sentence in the 0–2 branch pointing at Ch 13 §7 and Ch 17 §3 specifically — those two are the load-bearing prerequisites, and a reader who is short here is short there.

---

## 4. Section plan

### `## ⚪ §1 — What You Can Ask, and What You Already Know`

**PINNED ×2** — `chapter-01:272` and `chapter-05:860` both point here by number.

Owns the observability/monitoring distinction, framed as unknown unknowns versus known unknowns; instrumentation and telemetry as terms; the explicit exclusion of health checking; and observability's status under the 2025-11-24 blueprint. Opens with the distinction rather than a definition parade — the reader has heard both words and thinks they are synonyms, and trap #88 is exactly "observability is monitoring with better dashboards."

Three things must land, in this order. First, observability as the OTel primer defines it: understanding a system from the outside, asking questions without knowing its internals, handling "unknown unknowns," answering "why is this happening?" Second, instrumentation as the precondition — properly instrumented means developers *do not need to add more instrumentation to troubleshoot*, which is the definition's own sharpest edge and a good ★ Fixed Point candidate on its own. Third, the exclusion: a probe answers a yes/no question for the kubelet's benefit and produces no history, no trend, no measurement. Shipped Ch 5 §7 promised this section by name; honor the promise explicitly rather than by implication.

The blueprint paragraph is short and factual. **Do not restate a retired weight.** `lf-kcna-program-changes-2026-08-23` says observability "will be rolled under Cloud Native Architecture" and lists D4 at 12% with Observability as the first of three competencies; it says nothing about what observability was weighted before, and its own header records that the previous structure is not on the page. Point at Ch 1 for the change narrative — that is what shipped Ch 17 does, and consistency matters more here than completeness. See Open Questions #6.

- **Objectives:** D4.1
- **Introduces:** observability · monitoring · unknown unknowns vs known unknowns · instrumentation · telemetry
- **Retrieves:** Ch 5 §7 (probes) — mandatory anchor
- **Figure:** `ch18-fig01-monitoring-vs-observability`
- **Checkpoint after:** no

---

### `## ⚪ §2 — Four Signals`

Owns the four OpenTelemetry signals and the collector. Short, structural, memorable — this is a naming section and B1 rates it pure recall. The failure mode is over-scaffolding: the reader needs the four names in an order they can reproduce under time pressure, plus one sentence each on what the signal answers and what it cannot.

The load-bearing fact is that there are **four**, and the fourth is baggage — contextual information passed *between* signals, which is why candidates drop it (it is not itself a measurement). Trap #89. State the count before the list, so the count is what gets encoded.

Two honest limits belong here rather than later. Logs "are not extremely useful for tracking code execution on their own" because they lack context, and become useful inside a span or correlated with a trace — that is trap #91 and it also plants §5 and §6 simultaneously. And a signal is an output, not a system: the collector receives, processes and exports, which is why the same four signals reach different backends in §4, §5 and §6. That framing is what makes §8 possible.

- **Objectives:** D4.1
- **Introduces:** signal · traces · metrics · logs · baggage · OTel Collector
- **Figure:** `ch18-fig02-otel-four-signals`
- **Checkpoint after:** no
- ⚠ **The collector is unsourced.** See Open Questions #1. Shipped Ch 17's Voyage Ahead has already promised the reader "one collector," so this is not droppable.

---

### `## 🔵 §3 — Numbers Over Time`

**PINNED ×3** — `chapter-05:969`, `chapter-13:1336` and `chapter-17:1387` all point here by number. The heaviest inbound load of any section in the chapter.

Owns metrics as time series; labels and cardinality; utilization relative to requests; and metrics-server versus a monitoring system. This is the seam section, and its whole difficulty is knowing what *not* to re-teach.

Ch 13 §7 already defined the resource metrics pipeline and already quoted metrics-server's own scope note — that it is "meant only for autoscaling purposes," keeps no history, and cannot be queried for what happened an hour ago. **Do not restate that.** §3's job is the other half of the sentence: what a monitoring system does that metrics-server does not. History, arbitrary queries over time, alerting, and metrics that are not CPU and memory. The two coexist and answer different questions; the exam tests the boundary, not either side.

Utilization relative to requests is retrieved twice-over and must be paid off concretely: the number an autoscaler and a dashboard both report is a ratio, and the denominator is what the Pod *asked for*, not what the node has. Two shipped chapters send readers here for it.

`kubectl top` on a cluster without metrics-server is where the named pattern lands. Quote it exactly — ***an object without its component does nothing*** — and cross-bear to Ch 10 §3. Per the B7 book-level convention, **name the pattern and do not number it.** No ordinal, no "the fourth time you have seen this."

Cardinality is the one genuinely new mechanic: a metric plus its label set defines a distinct time series, so a label with unbounded values multiplies storage without adding insight. Treat it as a 🔭 Closer Look rather than graded material unless Open Questions #4 closes.

- **Objectives:** D4.1, D2.3
- **Introduces:** time series · metric label · cardinality · the metrics-server/monitoring-system boundary
- **Retrieves:** Ch 13 §7 (mandatory) · Ch 5 §8 (mandatory) · Ch 10 §3 (by name, verbatim)
- **Figure:** none new — **retrieves `ch13-fig04-metrics-pipeline-and-metrics-server`.** Redrawing it would teach the reader that this is new material, which is the opposite of what §3 is for
- **Checkpoint after:** ☆ **YES — Checkpoint 1**

---

### `## 🔵 §4 — Pulling, Not Being Pushed`

Owns Prometheus end to end: the pull/scrape model, service discovery, exporters, client libraries, Pushgateway and its narrow correct use, PromQL, Alertmanager, Grafana as the dashboard layer, and where Prometheus fits and does not. Densest sourced section in the chapter, and the one carrying the most B1 traps (#93 through #96, all `[source]`).

Structure it around the direction of the arrow, because that is what the traps turn on. Prometheus scrapes over HTTP; targets are found by service discovery or static configuration; nothing pushes except short-lived jobs that cannot be scraped, and those push to an intermediary gateway rather than to Prometheus. Then the components in one pass: server, client libraries, exporters, Pushgateway, Alertmanager. Then the query language, and Grafana as a separate thing that reads what Prometheus stores.

Two fit statements are exam-relevant and both are quotable. Each server is standalone and autonomous, *deliberately*, so it works when the rest of the infrastructure is broken — reliability over completeness. And it is explicitly the wrong tool where 100% accuracy is required, per-request billing being the source's own example. Trap #94 rewards a reader who knows a tool's stated non-fit.

Prometheus joined CNCF in 2016 as the second hosted project, after Kubernetes (trap #96). State it once, sourced. **Grafana is not a CNCF project** — a 🪝 Snag is the right home for that, because the surrounding paragraph will name four CNCF projects and the reader will generalize. Loki and Tempo appear in the Grafana source; name them at most in passing and keep them out of graded text (no ledger owner — Open Questions #5).

- **Objectives:** D4.1
- **Introduces:** Prometheus · pull/scrape model · service discovery · exporter · client library · Pushgateway · PromQL · Alertmanager · Grafana
- **Figure:** `ch18-fig04-prometheus-pull-architecture`
- **Checkpoint after:** no

---

### `## 🟡 §5 — Following One Request`

Owns distributed tracing: spans, root spans, trace and span IDs, context propagation across services, and Jaeger. The most abstract section in the chapter and the only 🟡 — B1's sequencing implication #8 exists for this section specifically, and reversing Ch 17 and Ch 18 would have made it vocabulary drill.

Build it from the Soundings Q7 gap rather than from definitions. One request enters, crosses five services, and each service's logs are individually complete and collectively useless because nothing joins them. What joins them is an identifier carried across the boundary. Then the vocabulary lands on a need the reader already feels: a span is a unit of work carrying a name, timing, structured log messages and attributes; a trace is the path the request took, made of one or more spans; the first span is the root span and represents the request start to finish. Trap #90 is span-versus-trace and it is worth a discriminating question rather than a definition.

Context propagation is the mechanism and needs a source (Open Questions #2). Baggage from §2 returns here as the thing being propagated, which is the cleanest way to make the fourth signal stick.

Jaeger closes the section: a tracing *backend* that receives, processes, aggregates and visualizes, originally built for OpenTracing and now OpenTelemetry-compatible with concepts mapping directly across. Keep the OTel/Jaeger division of labor explicit — OTel is APIs and SDKs that export; Jaeger is what receives. That division is the same shape as §4's Prometheus/Grafana split, and noticing the repetition is what §8 pays off.

Mesh telemetry is the mandatory Ch 17 §5 anchor and belongs at the end as a one-paragraph "and sometimes you get spans without instrumenting anything," pointing back rather than re-teaching.

- **Objectives:** D4.1
- **Introduces:** distributed tracing · span · root span · trace ID and span ID · context propagation · Jaeger
- **Retrieves:** Ch 17 §5 (mandatory) · Ch 17 §3 (the multi-service model this section presupposes)
- **Figure:** `ch18-fig03-trace-spans-across-services`
- **Checkpoint after:** ☆ **YES — Checkpoint 2**

---

### `## 🔵 §6 — Lines From Everywhere`

**PINNED, TITLE AND NUMBER** — `chapter-15:526` points here and quotes B6's title verbatim as its pointer text. `chapter-13:1354` pins the number. `chapter-06:890` points at the chapter without a section and is free.

Owns the cluster logging architecture, node-level agents as DaemonSets, Fluentd and Fluent Bit, sidecar logging, log rotation, and why `kubectl logs` is not archival.

The organizing fact is a limit, and it is worth stating before any of the tooling: Kubernetes provides no native storage for log data, so cluster-level logging requires a separate backend. Everything downstream follows from that. Then the three architectures the docs name — a node-level agent on every node (typically a DaemonSet), a dedicated sidecar in the application Pod, or the application pushing directly to a backend — with the first as the default answer and the reason stated.

Why `kubectl logs` is not archival is mechanical and satisfyingly concrete: the kubelet rotates container logs (`containerLogMaxSize` 10Mi, `containerLogMaxFiles` 5 by default), only the latest log file's contents are available through `kubectl logs`, the kubelet keeps one terminated container's logs on restart, and an evicted Pod's containers are evicted with their logs. That last clause is why the whole architecture exists, and shipped Ch 13 §3 set it up.

Fluentd and Fluent Bit: Fluent Bit is a lightweight telemetry agent created in 2014 as a sub-project of Fluentd, which is CNCF graduated; both are commonly deployed as node-level agents. The six-stage pipeline — input, parser, filter, buffer, router, output — is one table, not a section. **Watch the surface forms:** Fluentd is one word, Fluent Bit is two, and the ledger flags that asymmetry as itself exam-adjacent.

The Ch 6 §7 DaemonSet retrieval is mandatory and lands naturally: this is the canonical DaemonSet example the shipped chapter promised.

- **Objectives:** D4.1, D2.3
- **Introduces:** cluster-level logging · node-level logging agent · sidecar logging · Fluentd · Fluent Bit · log rotation
- **Retrieves:** Ch 6 §7 (mandatory) · Ch 13 §3
- **Figure:** `ch18-fig06-cluster-logging-architectures` — **added beyond B3's list**, see Open Questions #3
- **Checkpoint after:** no

---

### `## 🔵 §7 — Is the Service Doing What Users Expect`

Owns reliability, SLI, SLO, SLA by contrast, error budgets, the four golden signals, and RED and USE as complementary framings. The section title is the OTel primer's verbatim definition of reliability, which is the point: the whole chapter has been assembling instruments, and this is where the question they answer gets named.

Reliability first, then the measurement vocabulary in dependency order. An SLI is a measurement of a service's behavior, and a good one measures from the user's perspective. An SLO attaches one or more SLIs to business value and is how reliability is communicated to an organization. SLA is the externally committed contractual number — one clause, by contrast, and it exists in this section chiefly because it is the natural distractor in any SLI/SLO item (trap #92). The ledger routes it here for exactly that reason.

The four golden signals are fully sourced and should be given verbatim weight: latency, traffic, errors, saturation, with the source's own sharp observations — that failed-request latency must be tracked separately because a fast error is still an error and a slow error is worse, and that latency increases are often a leading indicator of saturation. That second one is the section's best 🪢 Mnemonic hook.

RED, USE and error budgets are all unsourced (Open Questions #1). Recommended posture if the fetches do not land: keep error budgets as one glossed clause following SLO, drop RED and USE to a named-only mention, and let no graded item depend on any of the three. B1 gap G21 named golden signals *and* RED/USE together; only the golden-signals half has been closed.

- **Objectives:** D4.1
- **Introduces:** reliability · SLI · SLO · SLA · error budget · four golden signals · RED · USE
- **Figure:** `ch18-fig05-sli-slo-golden-signals`
- **Checkpoint after:** ☆ **YES — Checkpoint 3**

---

### `## ☀️ §8 — One Question, Four Instruments`

Zenith. Owns no new material.

The synthesis is that the four signals are not four topics but four ways of asking §7's one question, and that each answers it at a different resolution: a metric says *whether*, a trace says *where*, a log says *what*, and baggage is what lets the first three talk about the same request. The reader has spent six sections acquiring instruments one at a time and has not yet been shown that they point at the same thing.

The second beat — quieter, and the one that closes Domain 4 — is that the same shape recurred all chapter: OTel exports and Jaeger receives; Prometheus stores and Grafana reads; the kubelet writes and an agent ships. Instrumentation and backend are separable everywhere, which is why you can change either one. That is Ch 17 §4's pluggability argument arriving in a domain the reader did not expect it in. Back-bear to it; **do not restate it, and do not assert a count** — Ch 17 §9 already owns the collected version and the B7 convention forbids adding to the tally.

Close with the reliability question restated as the reader's own, then hand to Ch 19.

- **Objectives:** D4.1
- **Introduces:** nothing
- **Figure:** `ch18-zenith-instruments-answer-one-question` — the chapter's single Zenith illustration
- **Checkpoint after:** no

---

## 5. ☆ Taking Your Bearings checkpoints

Three checkpoints, five questions each, 15 total. B3 sets this chapter at the **25% retrieval ceiling** — the last content chapter, most accumulated decay — so four of the fifteen draw from earlier chapters, tagged inline in house form as `*[retrieval: chN]*`. B3's spacing floor (at least one item from ≥4 chapters back) is satisfied three times over.

### Checkpoint 1 — after §3
**"What You Can Ask, and What the Numbers Report Against"** · 5 questions · 2 retrieval (40%)

- Observability vs monitoring, tested as a *scenario* rather than a definition (trap #88)
- Instrumentation — what "properly instrumented" means
- The metrics-server / monitoring-system boundary: given a question, which one can answer it
- *[retrieval: ch5]* Utilization relative to requests — the denominator
- *[retrieval: ch10]* `kubectl top` on a cluster without metrics-server, graded on naming the pattern

### Checkpoint 2 — after §5
**"Pull, Push, and the Path One Request Took"** · 5 questions · 1 retrieval (20%)

- Prometheus pull vs push, with Pushgateway as the only correct push path (trap #93)
- Prometheus non-fit — the billing case (trap #94)
- Span vs trace vs root span, as a discriminating question (trap #90)
- The four signals, with baggage as the graded element (trap #89)
- *[retrieval: ch17]* Mesh telemetry without code changes — what the sidecar can report and what it still cannot

### Checkpoint 3 — after §7
**"Lines, Signals, and the Question They Answer"** · 5 questions · 1 retrieval (20%)

- Why `kubectl logs` cannot answer a question about three restarts ago
- The three cluster-logging architectures, and which is the default answer
- SLI vs SLO, with SLA as the distractor (trap #92)
- The four golden signals, named
- *[retrieval: ch6]* Why the node-level log agent is a DaemonSet and not a Deployment

Retrieval total: 4 of 15 = **26.7%**, at the ceiling. Drawn from Ch 5, 6, 10 and 17 — four different chapters, three of them more than four chapters back.

---

## 6. Exam Alert plan

**High-priority topics** — every one of these is `[source]`-tagged in B1 and every one is a discrimination rather than a recall:

1. **The four signals.** Traces, metrics, logs, baggage. The count is the exam surface; baggage is the one dropped.
2. **Prometheus pulls.** Push exists only via Pushgateway, only for short-lived jobs.
3. **Span vs trace.** A span is one unit of work; a trace is the path, one or more spans, from a root span.
4. **SLI vs SLO.** Measurement versus objective. SLA is the third term and the usual distractor.
5. **Observability vs monitoring.** New questions vs pre-chosen indicators — not "dashboards vs no dashboards."
6. **metrics-server is not a monitoring system.** Its own docs say so; the exam tests the boundary.

**Common traps, in loss-aversion framing** — B1 numbers in brackets, all `[source]`:

| Trap | Correct understanding |
|---|---|
| "Observability is monitoring with better dashboards" [88] | Observability handles unknown unknowns — asking questions you did not plan for |
| Naming three signals [89] | Four. Baggage is contextual information passed *between* signals |
| Span and trace used interchangeably [90] | One unit of work vs the whole request path |
| "Logs are the richest signal" [91] | Logs lack context on their own; they get rich inside a span or correlated with a trace |
| SLI/SLO swapped [92] | SLI measures; SLO commits |
| "Prometheus pushes" [93] | It scrapes over HTTP. Pushgateway is an intermediary for jobs too short to scrape |
| "Prometheus for billing" [94] | Explicitly not — it trades completeness for reliability |
| "Prometheus needs clustered storage" [95] | Each server is standalone by design, so it works when other infrastructure is broken |
| "Prometheus was CNCF's first project" [96] | Kubernetes was first; Prometheus second, 2016 |
| Expecting Observability as its own domain [113] | It is competency material inside Cloud Native Architecture. Point at Ch 1; do not restate a retired weight |

Two constraints on framing. Every trap above is `[source]`, so "commonly missed" language is defensible for these — but **not** for anything added during drafting from intuition; Ethical Guardrail #8 requires "easy to confuse" for inferred traps. And the last row must not assert what observability used to be weighted; see §1 and Open Questions #6.

---

## 7. Practice Questions plan

**Target: 17**, per `question_budget.practice_questions` and B4's weight-proportional derivation (5% chapter weight → 15 + 2×(5−4) = 17). Do not adjust — the derivation is what reproduces the published domain split.

**Distribution across sections**, weighted to exam surface rather than section length:

| Source | Qs |
|---|---|
| §1 observability / monitoring / instrumentation | 2 |
| §2 the four signals | 2 |
| §3 metrics, metrics-server boundary, utilization | 3 |
| §4 Prometheus | 4 |
| §5 tracing | 2 |
| §6 logging architecture | 2 |
| §7 SLI/SLO/golden signals | 2 |
| **Retrieval, interleaved** | **4 of the above, tagged** |

§4 gets four because it carries four sourced traps and the largest concept count in the chapter. §5 gets two despite being the hardest section — B1 rates D4 recall-and-recognition, and tracing's exam surface is genuinely span-vs-trace plus "what is Jaeger," not mechanism.

**Interleaving strategy.** This is the last content chapter and the last chance to interleave before Ch 19 does nothing else, so the four retrieval items should each join *two* chapters rather than testing one in isolation:

- Ch 5 §8 requests × §3 utilization — the ratio and its denominator
- Ch 13 §7 metrics-server × §4 Prometheus — same word "metrics," two systems, one boundary
- Ch 17 §3 microservices × §5 tracing — why the request path needs a name
- Ch 6 §7 DaemonSets × §6 log agents — the workload resource and the canonical use of it

**Trap-answer construction.** Distractors come from the B1 rows above, which means each one targets a documented misconception rather than a random wrong option. Why-wrong explanations required for all four options on every item, per the contract. **One prohibition carried from B3:** no item may be graded on a project's current CNCF maturity level (trap #99 — the roster is a dated snapshot). Naming Prometheus as CNCF's second hosted project in 2016 is a sourced historical fact and is fine; asking which projects are *currently* graduated is not.

---

## 8. Required figures

Seven. Six concept diagrams plus exactly one Zenith, per skill Part 18.10. Each attaches to a specific concept; none is decorative; all must read in grayscale and at 400px width, and all should be authored near 3:4 per the reflow check.

| Anchor | § | Purpose | Rough content |
|---|---|---|---|
| `ch18-fig01-monitoring-vs-observability` | §1 | Distinguish two similar-sounding things by *what you can ask*, not by tooling | Two panels sharing one system. Left: a fixed set of pre-chosen indicators with a dial on each — the questions were decided in advance. Right: the same system with an open query path — a question arriving that nobody pre-registered. Label the axis explicitly as known unknowns / unknown unknowns. **Anti-pattern to avoid:** do not draw this as "Prometheus vs OpenTelemetry." It is not a tool comparison |
| `ch18-fig02-otel-four-signals` | §2 | Dual-code the count and the odd one out | Four labeled lanes — traces, metrics, logs — plus baggage rendered *across* the other three rather than beside them, because it is contextual information passed between signals. One line each on what the signal answers. Max 7 labels |
| `ch18-fig04-prometheus-pull-architecture` | §4 | Make the arrow direction unforgettable | Prometheus server at center with arrows pointing *outward* to instrumented targets and exporters. Pushgateway shown as the single inbound path, visibly narrow, labeled "short-lived jobs only." Alertmanager and Grafana as downstream consumers. Service discovery as the mechanism finding targets |
| `ch18-fig03-trace-spans-across-services` | §5 | Spatial-temporal structure prose cannot carry | One request crossing five services, rendered as a span tree over a time axis. Root span spanning the full width; children nested and offset. Trace ID annotated as the thing crossing every boundary. This figure *is* the span-vs-trace distinction |
| `ch18-fig06-cluster-logging-architectures` | §6 | Distinguish three similar alternatives — **added, see Open Questions #3** | Three side-by-side node diagrams: node-level agent as a DaemonSet (marked as the default), sidecar in the application Pod, application pushing directly. Same backend in all three so the difference is visibly *where collection happens* |
| `ch18-fig05-sli-slo-golden-signals` | §7 | Separate two terms readers fuse, and anchor four names | Left: one measurement (SLI) feeding one commitment (SLO), with SLA shown outside the boundary as the external contract. Right: the four golden signals as four gauges — latency, traffic, errors, saturation — with saturation annotated as the leading indicator of the other three |
| `ch18-zenith-instruments-answer-one-question` | §8 | The synthesis beat | Four instruments converging on one question. The composition should visually rhyme with `ch18-fig02` so the reader recognizes the four signals returning — this is a *recognition* payoff and it fails if it looks like a new diagram |

**Retrieved, not redrawn:** `ch13-fig04-metrics-pipeline-and-metrics-server` in §3. Reference the existing anchor.

---

## 9. Open questions for the author

**1. Six sourcing gaps, four of them drafting-blocking.** The observability corpus is nine snapshots and covers §1, §2's signal list, §4 and §5 well. It does not cover:

| Missing | Needed by | Suggested fetch | Blocking? |
|---|---|---|---|
| A definition of **monitoring** as distinct from observability | §1 — half the chapter's central distinction | CNCF Glossary "Monitoring" and "Observability" entries | **Yes.** §1 currently has a sourced definition of one term and none of the other |
| **OpenTelemetry Collector** | §2 | `opentelemetry.io/docs/collector/` | **Yes.** Shipped Ch 17's Voyage Ahead already promised the reader "one collector" |
| **Context propagation** | §5 | `opentelemetry.io/docs/concepts/context-propagation/` | **Yes.** It is the mechanism the whole section rests on |
| **RED and USE methods** | §7 | Weaveworks RED / Brendan Gregg USE, or an OTel-adjacent restatement | **Yes** if they stay in §7. B1 gap G21 named them alongside golden signals; only golden signals got closed |
| **Error budget** | §7 | Google SRE book ch. 3 | No — droppable to a glossed clause |
| **Metric label cardinality** | §3 | `prometheus.io/docs/practices/naming/` or instrumentation practices | No — droppable to a 🔭 Closer Look |

Recommendation: fetch the first four before drafting. If any does not land, the fallback posture is stated in the section blocks; nothing in this outline collapses without them, but §1 and §5 both get noticeably weaker.

**2. SLA has no cached source.** The B7 ledger assigns it to §7 as a one-clause contrast and explicitly rules it "not glossary-only" because it will appear as a distractor — and a distractor the reader cannot look up is a badly built distractor. The CNCF glossary snapshots cached so far do not include an SLA entry. Either fetch one, or state SLA as a definitional contrast without a source tag and accept that it is the one untagged term in the section. Recommendation: fetch it with the monitoring/observability glossary entries — same page family, one request.

**3. One figure added beyond B3's list.** `ch18-fig06-cluster-logging-architectures`. B3 planned six anchors and left §3 and §6 figureless. §3 correctly has none (it retrieves `ch13-fig04`), but §6 teaches three parallel alternatives that the Kubernetes docs themselves render as three figures — exactly the comparative-illustration case in skill Part 18.9. Flagged rather than assumed; drop it if you would rather hold the diagram pipeline to B3's count.

**4. Bearings at 15, against B4's table figure of 10.** Justified in the frontmatter and consistent with shipped Ch 13 and Ch 17, both of which exceeded. Raises the chapter total to 40. If you want the table honored literally, the cut is Checkpoint 2 → merged into 1 and 3, which leaves §4 and §5 untested until the end and which I would not recommend.

**5. Grafana, Loki and Tempo are not CNCF projects and have no ledger owner.** Grafana is owned by §4 in the ledger and is fine. Loki and Tempo appear only inside the Grafana snapshot; they have no owner, no acronym-register row, and no glossary entry. Recommendation: name them at most in one non-graded clause, or omit. No question may depend on them.

**6. Shipped Ch 1 asserts a retired domain weight this chapter cannot support.** `chapter-01:272` says "the 8% once reserved for observability alone now shares a 12% domain." The 8% is not in `lf-kcna-program-changes-2026-08-23` — that snapshot's own header records that the previous structure was removed from the page as unsourced — and shipped Ch 17 was revised at its gate specifically to stop making comparative claims of this shape. So §1 will point at Ch 1 rather than restate the figure, which leaves the book holding a number in Chapter 1 that Chapters 17 and 18 both decline to repeat. **Author's call:** either close gap G33 by caching the CNCF curriculum repo's KCNA version history, which would make the 8% sourceable and let all three chapters say it; or sweep Ch 1:272 to match Ch 17's narrowed framing. Not load-bearing for this chapter either way, but it is a visible internal disagreement.

**7. Ledger and shipped-text errata found at this gate.**
   - Shipped `chapter-17:296` carries an AUTHOR-REVIEW note asserting that "No cached snapshot supports the count or the names" of D4's three competencies. That is now false: `lf-kcna-program-changes-2026-08-23` lists all three under "Cloud Native Architecture – 12%". Shipped Ch 17's line 411 Dead Reckoning states the names untagged as a result. Recommend tagging it and retiring the note.
   - B7's Ch 18 row for **node-level logging agent** gives its first appearance as "Ch 13 §7 †" (projected). It is now shipped and verified at `chapter-13:1354`. Cosmetic.
   - B1 gap **G32 (FinOps / OpenCost / Kubecost)** remains open and unassigned. Shipped Ch 17 omitted it deliberately with a recorded AUTHOR-REVIEW, naming its Landscape paragraph as the minimal home if reversed. Ch 18 is the other candidate, since cost management sat adjacent to the retired standalone Observability domain. **Recommendation: keep it omitted**, consistent with Ch 17, unless the LFS250 syllabus fetch (G37) shows it in scope. Recorded so the decision is visible in both chapters rather than silent in one.

**8. Two B6 recommendations adopted here, both cosmetic-with-consequences.** Heading form `## <difficulty> §N — Title` (rec. #3) and `☀️` on the Zenith section (rec. #4). Both match shipped Ch 5–8, 13 and 17. Noted because adopting them in Ch 18 completes the majority and makes the eventual retrofit of Ch 2/3/4 a smaller sweep.
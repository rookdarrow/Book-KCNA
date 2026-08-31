# Chapter 18: Reading the Instruments
## *"Four signals, and the question they exist to answer"*

**Domain Weight: 12% (Cloud Native Architecture) | Competency: Observability**
**Complexity: Mixed | Novelty: Moderate**

---

## Attention Budget

**Total time: ~85 minutes | Recommended: Split across 2 sessions**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| 🧭 Soundings | 8 min | Low | Anytime |
| §1 What You Can Ask, and What You Already Know | 10 min | Medium | Mid-session |
| §2 Four Signals | 6 min | Low | Anytime |
| §3 Numbers Over Time | 10 min | Medium | Mid-session |
| ☆ Taking Your Bearings (1) | 6 min | Medium | After brief break |
| §4 Pulling, Not Being Pushed | 14 min | Medium | When alert |
| §5 Following One Request | 12 min | High | Peak attention |
| ☆ Taking Your Bearings (2) | 6 min | Medium | After brief break |
| §6 Lines From Everywhere | 10 min | Medium | Mid-session |
| §7 Is the Service Doing What Users Expect | 10 min | Medium | When alert |
| ☆ Taking Your Bearings (3) | 6 min | Medium | After brief break |
| §8 One Question, Four Instruments | 5 min | Low | Anytime |
| Exam Alert + Practice Questions | 20 min | High | Peak attention |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*If you only have 15 minutes: read §2 and §7, then take Checkpoint 3. Those two sections carry four of this chapter's six high-priority exam topics between them.*

---

> *"You must be conscious about what outputs are coming out of your system."*
> — CNCF TAG Observability, *Observability Whitepaper*

---

## 🧭 Soundings

*Before reading, take depth.*

Eight questions. None of them requires this chapter — every one is answerable from a chapter you have already finished. Your score tells you how to read what follows.

1. A liveness probe fails and the kubelet restarts the container. What record of that failure does the cluster hold an hour later?

2. Name one question about your workloads that metrics-server is not built to answer.

3. `kubectl top pods` returns an error on a cluster whose Pods are all `Running` and healthy. What is the most likely cause, and what is the general pattern it belongs to?

4. An autoscaler reports that a Pod is at 80% CPU utilization. Eighty percent of *what*?

5. Why does cluster log collection typically run one agent per node rather than one agent per application?

6. You need a container's log output from three restarts ago. Can `kubectl logs` give it to you?

7. A single user request crosses five services. Each of the five writes its own complete, well-formatted log file. What question can those five log files not answer between them?

8. A service mesh reports per-service latency for an application whose source code was never touched. How is that possible?

<details>
<summary>Answers + reading strategy</summary>

1. **None.** A probe is a yes/no signal to the kubelet, evaluated and acted on immediately. The restart itself surfaces as a container-state reason and a restart count, and an Event that expires; the probe result itself is not stored, trended, or queryable. *[cross-bearing: see Ch 5 §7 — three probes, three jobs]*

2. **Anything historical, and anything that isn't CPU or memory.** metrics-server holds current resource readings for autoscaling decisions. It does not keep a record of what those readings were an hour ago, and it does not collect application-level measurements. *[cross-bearing: see Ch 13 §7 — the resource metrics pipeline]*

3. **metrics-server is not installed.** The `kubectl top` command exists in every kubectl binary; the component that answers it does not exist in every cluster. This is the pattern *an object without its component does nothing* — the API surface being present tells you nothing about whether anything is behind it. *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*

4. **Eighty percent of the container's resource request** — not of the node's capacity, and not of the container's limit. *[cross-bearing: see Ch 5 §8 — what a Pod is owed]*

5. **Because container logs are written to the node's filesystem**, by the container runtime, for every container the node runs. Collecting them is a per-node job, and the workload resource that puts exactly one Pod on every node is the DaemonSet. *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]*

6. **No.** `kubectl --previous` reaches one termination back, and the current log file is subject to rotation. Three restarts ago is gone from the node. *[cross-bearing: see Ch 13 §3 — looking inside]*

7. **What order things happened in, and where the time went.** Each file is internally complete and the five have nothing joining them — no shared identifier, no common clock the reader can trust, no way to know which line in service D corresponds to which line in service A. *[cross-bearing: see Ch 17 §3 — small pieces, replaced whole]*

8. **The traffic passes through a proxy the platform injected**, not through code the application team wrote. The proxy sees every request enter and leave, and reports on what it sees. *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*

**If you got 6+ right:** skim. Read §1's distinction carefully, memorize the four signals in §2, and spend your real attention on §4 and §7 — those two carry six of this chapter's ten sourced traps. Take all three checkpoints.

**If you got 3–5 right:** read at normal pace. This chapter builds almost entirely on chapters you have already finished, and the questions you missed point at exactly which section will feel like new material rather than extension.

**If you got 0–2 right:** read carefully, and read two things first. Ch 13 §7 (the resource metrics pipeline and metrics-server) and Ch 17 §3 (microservices) are the load-bearing prerequisites for this chapter. Almost everything here extends one or the other. Twenty minutes there will save you an hour here.

</details>

---

## Why This Chapter Matters

Chapter 17 ended by handing you a bill.

Every architectural choice in that chapter made systems easier to change and harder to see. Break a monolith into microservices and one request becomes twenty. Replace machines instead of patching them and the machine you want to inspect is gone. Scale to zero and the thing you want to ask a question about is not running.

This is the chapter where the bill arrives.

Here is the thing that makes it interesting, and it is not a thing most study guides say out loud: **you cannot dashboard your way out of a question you did not know to ask.** Every dashboard you have ever built is a set of answers to questions somebody chose in advance. That is genuinely useful. It is also, on the night that matters, frequently beside the point — because the thing that broke is the thing nobody drew a graph for.

Practitioners do not add observability because a framework told them to. They add it because at some point they were asked a question about a running system and had no way to answer it. Somebody said *why was checkout slow between 2:10 and 2:14 for users in one region*, and there was no path from that sentence to an answer. Not a missing dashboard — a missing *capability*. That is the moment this chapter is about, and by the end of it you will have four instruments for it and a clear sense of which one to reach for.

> **Dead Reckoning:** Observability is a property of a system: the degree to which you can understand its internal state from its external outputs [source: cncf-glossary-observability-2026-08-31]. To produce those outputs, the system must be instrumented — code in its components must emit signals [source: opentelemetry-instrumentation-2026-08-31]. This chapter covers the four signals OpenTelemetry defines, the two dominant collection tools (Prometheus for metrics, Jaeger for traces), how logs get off a node, and the vocabulary for saying whether a service is behaving acceptably: SLI, SLO, and the four golden signals.

One honest note before you start, because you may have met a contradiction already.

If you have been studying with material published before late 2025, you were probably told that Observability is its own KCNA domain with its own weight. On the current blueprint it is not. Observability is now a competency inside **Cloud Native Architecture**, a domain weighted at 12% [source: lf-kcna-program-changes-2026-08-23]. The Linux Foundation's own announcement puts it plainly: the domains remain mostly unchanged "except that observability will be rolled under Cloud Native Architecture" [source: lf-kcna-program-changes-2026-08-23].

Read that as a reorganization, not a demotion. The material did not stop being tested. It stopped being *separately weighted*, which is a different thing entirely — and a candidate who reads "rolled under" as "de-emphasized" and skims this chapter will find that out expensively. *[cross-bearing: see Ch 1 — the curriculum that moved under everyone's feet]*

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Distinguish** observability from monitoring by what each one lets you *ask*, not by which tool implements it
- **Name** all four OpenTelemetry signals — including the one most candidates drop
- **Explain** why Prometheus pulls, and the one narrow case in which anything pushes
- **Trace** a single request across service boundaries, and say what a span is that a trace is not
- **Distinguish** an SLI from an SLO, and name the four golden signals
- **Choose** the right instrument for a question, instead of reaching for the one you happen to know

*You'll also stop treating "we have monitoring" as an answer to "can we find out?" — which is the shift that separates people who fix outages from people who watch them.*

---

## ⚪ §1 — What You Can Ask, and What You Already Know

Start with the confusion, because you almost certainly have it.

Most people use *monitoring* and *observability* as synonyms, with a vague sense that observability is the newer, more expensive one — monitoring with nicer dashboards and a vendor invoice attached. That is the single most common misconception in this domain, and it will cost you a question.

The difference is not tooling. It is not dashboards. It is **what you are able to ask**.

Monitoring, in its canonical definition, is "collecting, processing, aggregating, and displaying real-time quantitative data about a system" [source: sre-book-monitoring-definitions-2026-08-31]. Notice what that sentence assumes: somebody already decided *which* quantitative data. Google's own SRE text lists four reasons to monitor, and every one of them is a question chosen in advance [source: sre-book-monitoring-definitions-2026-08-31]:

- **Long-term trends** — "How big is my database and how fast is it growing?"
- **Alerting** — "Something is broken, and somebody needs to fix it right now!"
- **Building dashboards** — "Dashboards should answer basic questions about your service"
- **Debugging** — "Our latency just shot up; what else happened around the same time?"

Those are good questions. They are also, all four, questions somebody sat down and wrote out before the incident. A monitoring system is an instrument built to answer a fixed set of questions very well.

Observability is the other thing. The CNCF's TAG Observability whitepaper draws the line in one sentence: "Monitoring is called a system that can detect known unknowns — as opposed to observability which emphasizes being able to find and reason about unknown unknowns as well" [source: cncf-tag-observability-whitepaper-2026-08-31].

A **known unknown** is a question you have thought of but do not yet have the answer to. *Is the database near capacity?* You knew to ask; you built a graph; the graph tells you. An **unknown unknown** is a question you had not thought to ask until the moment you needed it. *Why did requests from one specific customer's mobile client start failing at 2:10, but only when they hit the region-two cache?* Nobody built that graph. Nobody could have — there are more possible questions of that shape than there are dashboards in the world.

> **★ Fixed Point**
>
> **Observability is the ability to ask questions of a running system that you did not plan for in advance — to reason about *unknown unknowns*. Monitoring watches indicators you chose ahead of time — *known unknowns*. The distinction is about what you can ask, not about which tool you bought.**

OpenTelemetry's own framing says the same thing from the other side: observability "lets you understand a system from the outside by letting you ask questions about that system without knowing its inner workings," which is what lets you "troubleshoot and handle novel problems, that is, 'unknown unknowns'" [source: opentelemetry-observability-primer-2026-08-23]. It also helps you answer the question "Why is this happening?" — as opposed to *whether* it is happening, which a dashboard can already tell you.

<!-- FIGURE: ch18-fig01-monitoring-vs-observability -->
```
              THE SAME SYSTEM, TWO POSTURES

  MONITORING                        OBSERVABILITY
  known unknowns                    unknown unknowns

  ┌───────────────────┐             ┌───────────────────┐
  │  questions chosen │             │  question arrives │
  │   IN ADVANCE      │             │   AT 02:10 AM     │
  └─────────┬─────────┘             └─────────┬─────────┘
            │                                 │
     ┌──────┴──────┐                          │  "why were
     ▼      ▼      ▼                          │   requests
   ┌───┐  ┌───┐  ┌───┐                        │   from one
   │CPU│  │mem│  │5xx│   <- fixed             │   client
   └─┬─┘  └─┬─┘  └─┬─┘      indicators        │   slow in
     └──────┼──────┘                          │   region 2?"
            ▼                                 ▼
     ┌─────────────┐                   ┌─────────────┐
     │  DASHBOARD  │                   │  OPEN QUERY │
     │ answers the │                   │  over rich  │
     │  4 questions│                   │  telemetry  │
     │  you picked │                   │             │
     └──────┬──────┘                   └──────┬──────┘
            ▼                                 ▼
     ┌───────────────────────────────────────────────┐
     │        T H E   R U N N I N G   S Y S T E M    │
     └───────────────────────────────────────────────┘

  Both read the same system. The difference is upstream:
  one has a fixed question set, one does not.
```

Note what that figure is *not*. It is not "Prometheus versus OpenTelemetry." Those are both tools, and both of them serve both postures. A Prometheus deployment with rich, well-labeled metrics and an ad-hoc query language is doing observability work; a pile of OpenTelemetry traces nobody can query is not. The posture is upstream of the tool.

### Instrumentation is the precondition

None of this happens for free. A system is observable only to the degree it emits something worth reading.

The OpenTelemetry docs state the dependency directly: "For a system to be observable, it must be instrumented: that is, code from the system's components must emit signals" [source: opentelemetry-instrumentation-2026-08-31]. **Instrumentation** is the work of making a system emit those signals. **Telemetry** is the data that comes out — "data emitted from a system and its behavior" [source: opentelemetry-observability-primer-2026-08-23].

And here is the sharpest available test of whether you have done enough of it:

> **★ Fixed Point**
>
> **An application is properly instrumented when developers don't need to add more instrumentation to troubleshoot an issue, because they already have all of the information they need** [source: opentelemetry-observability-primer-2026-08-23]**.**

Sit with that for a second. The bar is not "we emit metrics." The bar is: when something novel breaks, nobody has to ship a code change to find out what. If your debugging procedure routinely begins with *let me add a log line and redeploy*, you have a monitoring system and an aspiration.

Instrumentation comes in two kinds. **Code-based** instrumentation is written into the application and gives "deeper insight and rich telemetry from your application itself." **Zero-code** instrumentation attaches from outside and is "great for getting started, or when you can't modify the application you need to get telemetry out of," pulling telemetry "from libraries you use and/or the environment your application runs in" [source: opentelemetry-instrumentation-2026-08-31]. Hold onto that second kind — it returns in §5.

> 🔭 **Closer Look:** The CNCF glossary makes a point the other sources leave implicit: observability is "a system property," and consequently "how observable a system is will significantly impact its operating and development costs" [source: cncf-glossary-observability-2026-08-31]. It is not a product you install. It is a characteristic your system either has or lacks, and the cost of lacking it is paid in engineer-hours during incidents.

### What a probe is not

You have already met something in this book that looks like observability, sits close to it, and is emphatically not it.

Probes.

A liveness probe asks a container a yes/no question on a schedule. A readiness probe asks a different yes/no question on a schedule. Both produce an immediate action — restart the container, remove the Pod from endpoints — and then the answer is spent. *[cross-bearing: see Ch 5 §7 — three probes, three jobs]*

What a probe does not produce is a **record**. There is no trend. There is no history you can query. There is no way to ask "how often did this endpoint fail its readiness check last Tuesday, and did it correlate with the deploy?" The kubelet asked, got an answer, acted, and moved on. Health checking answers *is it up right now, according to one binary test I wrote in advance* — which is not just a different question from *why is this happening*, it is a different **kind** of question.

> 🪝 **Snag:** "We have liveness and readiness probes configured" is a true and useful statement about a workload's self-healing. It is not an answer to "is this service observable." A cluster full of perfect probes can still leave you unable to explain a single slow request. Health checking is not observability.

Everything from here on is about building the records that probes do not keep.

---

## ⚪ §2 — Four Signals

This section is short and it is a naming section. What you need out of it is a list you can reproduce cold, under time pressure, with the right number of items in it.

**The number is four.**

OpenTelemetry — the CNCF project that defines the vendor-neutral standard for telemetry data — currently supports four signals [source: opentelemetry-signals-2026-08-23]:

| Signal | What it is | What it answers | What it cannot answer alone |
|---|---|---|---|
| **Traces** | "the path of a request through your application" | *Where* did the time go, and in what order? | What the numbers looked like in aggregate |
| **Metrics** | "a measurement captured at runtime" | *Whether* something is happening, and how much | Which specific request was affected |
| **Logs** | "a recording of an event" | *What* the code said happened | Nothing about ordering across services, on its own |
| **Baggage** | "contextual information that is passed between signals" | — it is not a measurement; it is what lets the other three talk about the same request | Anything by itself |

A **signal**, generally, is a system output describing the underlying activity of the platform and the applications on it — something you want to measure at a point in time, or an event moving through a distributed system that you would like to trace [source: opentelemetry-signals-2026-08-23].

> **★ Fixed Point**
>
> **OpenTelemetry defines FOUR signals: traces, metrics, logs, and baggage** [source: opentelemetry-signals-2026-08-23]**. Candidates reliably name three and drop baggage, because baggage is not itself a measurement — it is contextual information passed between the other signals.**

> 🪢 **Mnemonic:** **T-M-L-B** — *Traces, Metrics, Logs, Baggage.* Or, if letters won't stick: three instruments and the thing that ties them together. The three you'd name unprompted are the measurements; the fourth is the string running through them.

### Why baggage counts

Baggage is a key-value store that travels with a request, letting you "propagate any data you like alongside context" [source: opentelemetry-baggage-2026-08-31]. Its purpose is specific: "include information typically available only at the start of a request further downstream" — things like account identification, user IDs, product IDs, and origin IPs [source: opentelemetry-baggage-2026-08-31]. Service A knows which customer this is. Service E, four hops later, does not, unless something carried it there.

The detail that makes baggage a *separate* signal rather than a property of spans is this: "baggage is a separate key-value store and is unassociated with attributes on spans, metrics, or logs without explicitly adding them" [source: opentelemetry-baggage-2026-08-31]. It rides alongside. Attaching it to a span is a deliberate act. That separation is exactly why it earns its own row — and exactly why people forget it.

Baggage "means you can pass data across services and processes, making it available to add to traces, metrics, or logs in those services" [source: opentelemetry-baggage-2026-08-31]. Which is to say: it is the signal that makes the other three signals talk about *the same thing*. Hold that. §8 is built on it.

> 🔭 **Closer Look:** Baggage travels over the wire, which has a consequence worth one sentence of operational caution: "Sensitive Baggage items can be shared with unintended resources, like third-party APIs… making it visible to anyone inspecting your network traffic" [source: opentelemetry-baggage-2026-08-31]. Customer identifiers are the classic case. Not exam surface — but it is the reason mature teams have a policy about what goes in baggage.

### One limit, stated early

Logs deserve an honest caveat before you meet them properly in §6, because it plants two later sections at once.

Logs "are not extremely useful for tracking code execution on their own, as they typically lack contextual information; they become far more useful when they are included as part of a span, or when they are correlated with a trace and a span" [source: opentelemetry-observability-primer-2026-08-23].

That is not a claim that logs are bad. It is a claim about what a log line *is*: a timestamped message from one process, which — unlike a trace — is not "necessarily associated with any particular user request or transaction" [source: opentelemetry-observability-primer-2026-08-23]. One line, no context about the journey it belonged to. Which is exactly the situation Soundings Q7 put you in, and exactly what §5 exists to fix.

### The collector

One more piece of vocabulary, because a signal is an *output*, not a system. Something has to receive the outputs.

The **OpenTelemetry Collector** is "a vendor-agnostic implementation of how to receive, process and export telemetry data" [source: opentelemetry-collector-2026-08-31]. Its value proposition is consolidation: it "removes the need to run, operate, and maintain multiple agents/collectors," and it supports "open source observability data formats (e.g. Jaeger, Prometheus, Fluent Bit, etc.) sending to one or more open source or commercial backends" [source: opentelemetry-collector-2026-08-31].

Read that second quote slowly, because it contains the architectural idea this whole chapter keeps re-encountering. One set of signals goes *in*. Multiple, swappable backends receive them going *out*. The thing that produces telemetry and the thing that stores it are separate, and either can be replaced without the other noticing.

<!-- FIGURE: ch18-fig02-otel-four-signals -->
```
              F O U R   S I G N A L S

   ┌─────────────────────────────────────────────────┐
   │  BAGGAGE — contextual info passed BETWEEN the   │  <- rides across
   │  others; a separate key-value store, not a      │     all three
   │  measurement. Carries user/account/origin IDs.  │
   └───────┬─────────────┬─────────────┬─────────────┘
           :             :             :
   ════════╪═════════════╪═════════════╪════════════
           ▼             ▼             ▼
   ┌──────────────┐┌──────────────┐┌──────────────┐
   │   TRACES     ││   METRICS    ││    LOGS      │
   │ path of a    ││ a measurement││ a recording  │
   │ request      ││ at runtime   ││ of an event  │
   │              ││              ││              │
   │ answers      ││ answers      ││ answers      │
   │  WHERE       ││  WHETHER     ││  WHAT        │
   └──────┬───────┘└──────┬───────┘└──────┬───────┘
          └───────────────┼───────────────┘
                          ▼
              ┌───────────────────────┐
              │  OTel COLLECTOR       │
              │  receive · process ·  │
              │  export               │
              └───────────┬───────────┘
                          ▼
                 one or more backends
```

The Collector is deployable "as an agent or collector with support for traces, metrics, and logs" from a single codebase [source: opentelemetry-collector-2026-08-31] — one implementation, several shapes, several signal types.

<!-- AUTHOR-REVIEW: the Collector's pipeline stages (receiver / processor / exporter) are named as a taxonomy in OTel's docs but were NOT captured verbatim in the cached snapshot (see the explicit guardrail in opentelemetry-collector-2026-08-31). This section deliberately uses only the verbatim "receive, process and export" phrasing and does not present the three as named components. If a re-fetch closes manifest gap G-18c, §2 could name them. -->

---

## 🔵 §3 — Numbers Over Time

You already know most of this section. That is the point of it.

Chapter 13 taught you the resource metrics pipeline: metrics-server, `kubectl top`, and the reason both exist. *[cross-bearing: see Ch 13 §7 — numbers nobody collects by default]* This section is not going to re-teach that. It is going to draw the boundary on the *other* side of it — what a monitoring system does that metrics-server does not — because that boundary is what the exam actually reaches for.

### A metric is a number with a shape

Start with what makes a metric different from a log line.

Prometheus "fundamentally stores all data as time series: streams of timestamped values belonging to the same metric and the same set of labeled dimensions" [source: prometheus-data-model-2026-08-31]. A **time series** is not one number — it is a stream of them, each stamped with when it was taken. Each individual reading is a **sample**, consisting of a value and a millisecond-precision timestamp [source: prometheus-data-model-2026-08-31].

That structure is what makes metrics cheap to keep and cheap to aggregate. You cannot ask "what was the 95th-percentile latency across all of last week" of a pile of log lines without reading all of them. You can ask it of a time series trivially, because the shape of the data was chosen for exactly that question.

### Labels, and the cost of one

Time series are identified by more than a name.

"Every time series is uniquely identified by its metric name and optional key-value pairs called **labels**" [source: prometheus-data-model-2026-08-31]. So `http_requests_total{method="GET", status="200"}` and `http_requests_total{method="GET", status="500"}` are not one series with two flavors. They are two distinct series that happen to share a name.

> 🪝 **Snag:** A *metric label* and a *Kubernetes label* are different things that share a word. Kubernetes labels are the universal join between objects and selectors *[cross-bearing: see Ch 4 §5 — the universal join]*. Metric labels are dimensions on a time series. They are not related, they are not interchangeable, and reading a question quickly is exactly how you conflate them.

The identity rule has a consequence that follows directly from it: "The change of any label's value, including adding or removing labels, will create a new time series" [source: prometheus-data-model-2026-08-31].

> 🔭 **Closer Look — cardinality.** Because the label set *is* the identity, "every unique combination of key-value label pairs represents a new time series, which can dramatically increase the amount of data stored" [source: prometheus-naming-labels-cardinality-2026-08-31]. Hence the standing advice: "Do not use labels to store dimensions with high cardinality (many different label values), such as user IDs, email addresses, or other unbounded sets of values" [source: prometheus-naming-labels-cardinality-2026-08-31]. Add a `user_id` label to a busy endpoint's request counter and you have not added a dimension — you have multiplied your storage by your user count. This is not KCNA exam surface; it is the single most common way real teams break their own metrics stack, which is why it's here.

### The denominator

Two earlier chapters sent you here for one number, so let's settle it.

When an autoscaler or a dashboard tells you a Pod is at "80% CPU utilization," the denominator is **the containers' resource request**. Kubernetes states it directly: "if a target utilization value is set, the controller calculates the utilization value as a percentage of the equivalent resource request on the containers in each Pod" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

Not the node's capacity. Not the container's limit. The request — the amount the Pod *asked for* when it was scheduled. *[cross-bearing: see Ch 5 §8 — what a Pod is owed]*

The cleanest proof of this comes from the failure case rather than the formula. "If some of the Pod's containers do not have the relevant resource request set, CPU utilization for the Pod will not be defined and the autoscaler will not take any action for that metric" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

Read that again. Not "utilization will be computed against the node." Not "it defaults to something." **Undefined.** A Pod with no request has no utilization percentage at all — which is only possible if the request is the denominator. Remove the denominator and the fraction ceases to exist.

> 🪢 **Mnemonic:** Utilization is a fraction, and the bottom of the fraction is what you **asked for**, not what you were **standing on**. Request, not node. No request, no fraction.

### The boundary that gets tested

Now the other half.

metrics-server is the add-on that provides the `metrics.k8s.io` API, and Kubernetes notes it "needs to be launched separately" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31] — which is the Kubernetes documentation stating, from the autoscaling side, the same pattern you met from the `kubectl top` side: ***an object without its component does nothing***. *[cross-bearing: see Ch 10 §3 — the object is not the implementation]* The `kubectl top` verb is in every kubectl binary ever shipped. Whether anything answers it is a separate question about your cluster.

Chapter 13 established what metrics-server is for and, just as importantly, what it is scoped to. What it is **not** is a monitoring system. A monitoring system, in the sense this chapter means, does four things metrics-server does not:

| Question | metrics-server | A monitoring system |
|---|---|---|
| What is this Pod using *right now*? | ✅ yes | ✅ yes |
| What was it using an hour ago? | ❌ no history kept | ✅ yes — time series |
| How many 500s did the checkout endpoint return? | ❌ CPU and memory only | ✅ yes — arbitrary metrics |
| Page someone when error rate crosses 2% | ❌ not its job | ✅ yes — alerting |
| Compute p99 latency over a rolling 7 days | ❌ no query language | ✅ yes — query over time |

These two coexist. That is worth stating plainly, because candidates who learn the boundary sometimes overcorrect into "so you should replace metrics-server with Prometheus," which is wrong. metrics-server exists to feed autoscaling decisions with current readings, fast and cheaply. A monitoring system exists to keep history and answer arbitrary questions about it. Different jobs; both installed on plenty of real clusters.

> **⚠ Navigational Hazards**
>
> The exam does not test whether you can define metrics-server. It tests whether you know **which side of the boundary a given question falls on**. When you read a scenario, ask one thing: *does answering this require history, alerting, or a metric that isn't CPU or memory?* If yes, that is monitoring-system territory and metrics-server is the wrong answer — no matter how much the words in the question sound like "metrics."

The pipeline itself you have already seen. *[cross-bearing: see Ch 13 §7 — the resource metrics pipeline, figure `ch13-fig04-metrics-pipeline-and-metrics-server`]* Go back and look at it again if it has faded; there is no new diagram here, because there is no new architecture here. There is only a boundary you can now see the far side of.

---

## ☆ Taking Your Bearings: What You Can Ask, and What the Numbers Report Against

Five questions. Two of them test material from earlier chapters — that is deliberate, and it will keep happening for the rest of the book.

**1.** Your team has thorough dashboards: CPU, memory, request rate, error rate, and p99 latency per service, all with 90 days of history and alerting configured. At 02:10 a single enterprise customer reports that image uploads are failing, but only from their mobile app, and only in one region. None of the dashboards show anything unusual. Which best describes the situation?

- A) The dashboards are misconfigured; correctly configured monitoring would have caught this
- B) This is a known unknown that the alerting thresholds were set too high for
- C) This is an unknown unknown — a question nobody pre-registered, which no fixed dashboard set can answer
- D) The team has observability but lacks monitoring

**2.** A developer says: "Our app is properly instrumented — we emit metrics for request count and latency on every endpoint." By OpenTelemetry's own standard, what would actually establish that the application is properly instrumented?

**3.** For each question below, say whether metrics-server can answer it or whether it requires a monitoring system:

- (a) How much memory is this Pod using at this instant?
- (b) Did this Deployment's memory use climb steadily over the past six hours?
- (c) How many requests did the payments service reject last night?
- (d) Which node currently has the most CPU consumed by Pods?

**4.** *[retrieval: ch5]* A Pod's containers declare `limits: cpu: 1000m` but declare no `requests` at all. The node has 8 CPUs. An HPA is configured to target 70% CPU utilization for this Deployment. What does the HPA do?

- A) Scales based on 70% of 1000m
- B) Scales based on 70% of the node's 8 CPUs, divided across Pods
- C) Takes no action on that metric, because CPU utilization is undefined
- D) Defaults the request to the limit and scales on 70% of 1000m

**5.** *[retrieval: ch10]* You run `kubectl top nodes` on a freshly provisioned cluster. Every node is `Ready`, every Pod is `Running`, and the command returns an error. Name the cause, and name the general pattern this is an instance of — using the book's exact phrase for it.

---

**Answers with Explanations:**

**1. C.**

- **A is wrong**, and it is the tempting one. The dashboards are not misconfigured — they are correctly answering the five questions somebody chose. The failure is that this incident is not one of those five, and there is no configuration of a fixed dashboard set that anticipates every possible question. "Add another dashboard" is a response to a *specific* unknown unknown after it becomes known; it does not fix the class.
- **B is wrong** because a known unknown is a question you thought of. Nobody thought of "uploads from one customer's mobile client in one region." That is what makes it unknown.
- **C is correct.** This is precisely the "unknown unknowns" case [source: cncf-tag-observability-whitepaper-2026-08-31] — a novel question arriving unbidden, requiring the ability to interrogate the system rather than read a pre-built answer.
- **D is wrong** and inverts the situation. They clearly *have* monitoring: real-time quantitative data, displayed, with alerting [source: sre-book-monitoring-definitions-2026-08-31]. What they lack is the ability to ask the new question.

**2.** The standard is not about which metrics you emit. It is: **developers don't need to add more instrumentation to troubleshoot an issue, because they already have all of the information they need** [source: opentelemetry-observability-primer-2026-08-23]. Request count and latency per endpoint is a good start and tells you *whether* something is wrong. It does not tell you *why*. If the team's debugging procedure routinely begins with adding a log line and redeploying, the application is not properly instrumented by this definition — however many metrics it emits.

**3.**
- **(a) metrics-server.** Current resource reading, CPU/memory. Exactly its scope.
- **(b) Monitoring system.** Requires history. metrics-server keeps none.
- **(c) Monitoring system.** Requires both history *and* an application-level metric that is neither CPU nor memory.
- **(d) metrics-server.** Current, resource-level, no history required — this is what `kubectl top nodes` reports.

The discriminator is the one in the Navigational Hazards box: history, alerting, or a non-resource metric ⇒ monitoring system.

**4. C.** With no resource request set on the containers, "CPU utilization for the Pod will not be defined and the autoscaler will not take any action for that metric" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

- **A is wrong** — the denominator is the request, not the limit. This is the most common wrong answer because limits are the number people remember.
- **B is wrong** — node capacity is never the denominator for Pod CPU utilization.
- **D is wrong** — Kubernetes does not silently substitute the limit as a request for this calculation. The utilization is undefined, full stop. (LimitRange can *default* a request at admission time, but that is a different mechanism acting before the Pod exists, not the HPA improvising. *[cross-bearing: see Ch 8 §3 — dividing a shared cluster]*)

**5.** **The cause:** metrics-server is not installed. The `metrics.k8s.io` API has no provider, so the command has nothing to query [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].

**The pattern:** ***an object without its component does nothing***. The API surface existing tells you nothing about whether anything is behind it. *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*

---

**Checkpoint: You've Now Mastered**

✓ The observability/monitoring distinction, stated as what you can *ask*
✓ What "properly instrumented" actually means, and why most teams fail the test
✓ The metrics-server / monitoring-system boundary and the question that discriminates them
✓ Utilization's denominator — request, never limit, never node

Four sections to go, and the next one has more sourced exam traps in it than any other section in this chapter.

---

## 🔵 §4 — Pulling, Not Being Pushed

Everything the exam wants from you about Prometheus turns on one thing: **which way the arrow points.**

Get that right and four separate traps stop working on you. Get it wrong and they all land.

### The arrow

Prometheus is "an open-source systems monitoring and alerting toolkit originally built at SoundCloud" [source: prometheus-overview-2026-08-23]. It collects and stores metrics as time series — values with timestamps, plus optional key-value labels [source: prometheus-overview-2026-08-23], exactly the data model §3 described.

The collection mechanism is the part to memorize: "time series collection happens via a **pull model over HTTP**" [source: prometheus-overview-2026-08-23].

Prometheus reaches out. Your application does not report in. On an interval, the Prometheus server makes an HTTP request to each target's metrics endpoint and takes what it finds — this is called **scraping**. A **target** is "the definition of an object to scrape," and an **endpoint** is "a source of metrics that can be scraped, usually corresponding to a single process" [source: prometheus-glossary-2026-08-31].

How does it know what to scrape? "Targets are discovered via **service discovery** or static configuration" [source: prometheus-overview-2026-08-23]. In a Kubernetes cluster this matters enormously, because Pods are not durable and their addresses are not stable *[cross-bearing: see Ch 9 §2 — the address that doesn't last]*. Static configuration would be obsolete before you finished writing it. Service discovery lets Prometheus ask the cluster what exists right now, and scrape that.

> **★ Fixed Point**
>
> **Prometheus PULLS. It scrapes metrics from targets over HTTP on an interval; targets are found via service discovery or static configuration** [source: prometheus-overview-2026-08-23]**. Pushing exists only through the Pushgateway, and "the only valid use case for the Pushgateway is for capturing the outcome of a service-level batch job"** [source: prometheus-pushgateway-practices-2026-08-31]**.**

### The one exception, and how narrow it is

There is exactly one sanctioned way for something to push into Prometheus, and the project's own documentation goes out of its way to fence it in.

The **Pushgateway** is "an intermediary service which allows you to push metrics from jobs which cannot be scraped" [source: prometheus-pushgateway-practices-2026-08-31]. Note *intermediary* — even here, the metric does not land in Prometheus by being pushed. It is pushed to the gateway, and Prometheus scrapes the gateway. The arrow into Prometheus never reverses.

And the licensed use is narrow to the point of being brusque: "We only recommend using the Pushgateway in certain limited cases," and "the only valid use case for the Pushgateway is for capturing the outcome of a service-level batch job" — where a service-level batch job is "one which is not semantically related to a specific machine or job instance" [source: prometheus-pushgateway-practices-2026-08-31].

The reason is straightforward once you see it: a job that runs for eleven seconds and exits cannot be scraped on a thirty-second interval. It is gone. Everything else — every long-running service, every process with an address that stays put long enough to be visited — gets scraped.

> 🪝 **Snag:** "This service would rather push its metrics" is not a Pushgateway use case. Neither is "this job is tied to one specific machine" — the source explicitly scopes the Pushgateway to *service-level* batch jobs, which are the ones **not** semantically tied to a particular instance [source: prometheus-pushgateway-practices-2026-08-31]. Distractors are built from exactly these two plausible-sounding scenarios.

<!-- FIGURE: ch18-fig04-prometheus-pull-architecture -->
```
                    ARROWS OUT, NOT IN

   ┌──────────────┐                  ┌──────────────────┐
   │ SERVICE      │◄─── scrape ──────┤                  │
   │ DISCOVERY    │                  │                  │
   │ (finds       │  "what exists?"  │                  │
   │  targets)    │◄─────────────────┤                  │
   └──────────────┘                  │                  │
                                     │   PROMETHEUS     │
   ┌──────────────┐                  │     SERVER       │
   │ instrumented │◄─── scrape ──────┤                  │
   │ app          │      HTTP        │   scrapes  +     │
   │ (client lib) │                  │   stores locally │
   └──────────────┘                  │                  │
                                     │   standalone,    │
   ┌──────────────┐                  │   autonomous     │
   │ EXPORTER     │◄─── scrape ──────┤                  │
   │ (binary next │      HTTP        │                  │
   │  to a thing  │                  │                  │
   │  you didn't  │                  │                  │
   │  write)      │                  │                  │
   └──────────────┘                  │                  │
                                     │                  │
   ┌──────────────┐                  │                  │
   │ PUSHGATEWAY  │◄─── scrape ──────┤                  │
   │              │                  │                  │
   │  ▲ push      │                  │                  │
   │  │ ONLY from │                  └────┬───────┬─────┘
   │  │ service-  │                       │       │
   │  │ level     │                 push  │       │ HTTP API
   │  │ BATCH     │                alerts │       │ (read)
   │  │ jobs      │                       ▼       ▼
   │ ┌┴────────┐  │              ┌────────────┐ ┌──────────┐
   │ │short job│  │              │ALERTMANAGER│ │ GRAFANA  │
   │ └─────────┘  │              │ routes to  │ │ dashboards│
   └──────────────┘              │ email/pager│ │(NOT CNCF)│
      one narrow                 └────────────┘ └──────────┘
      inbound path

   Every arrow into Prometheus is Prometheus reaching out.
```

### The pieces

Prometheus is a toolkit, not a single binary. Its main components [source: prometheus-overview-2026-08-23]:

**The Prometheus server** — scrapes targets and stores the time series data locally.

**Client libraries** — "a library in some language (e.g. Go, Java, Python, Ruby) that makes it easy to directly instrument your code" [source: prometheus-glossary-2026-08-31]. You add this to software *you* wrote, and it exposes a metrics endpoint for Prometheus to scrape.

**Exporters** — "a binary running alongside the application you want to obtain metrics from" [source: prometheus-glossary-2026-08-31]. This is for software you *didn't* write and can't modify. Prometheus ships special-purpose exporters for things like HAProxy, StatsD, and Graphite [source: prometheus-overview-2026-08-23]. The exporter speaks whatever the application speaks on one side and Prometheus's scrape format on the other.

**Pushgateway** — the narrow inbound path above. It "persists the most recent push of metrics from batch jobs" [source: prometheus-glossary-2026-08-31].

**Alertmanager** — "takes in alerts, aggregates them into groups, de-duplicates, applies silences, throttles, and then sends out notifications" [source: prometheus-glossary-2026-08-31], routing "to the correct receiver integration such as email, PagerDuty, or OpsGenie" [source: prometheus-alertmanager-2026-08-31].

> ⚓ **Worth Securing:** Client library versus exporter is the discrimination worth carrying into the exam. A **client library** instruments code from the *inside* — you added it, you own the code. An **exporter** is a *separate binary* that gets metrics out of something you did not write and cannot change. Same destination, opposite side of the code boundary. That is the same instrumentation-versus-backend separation you met with the Collector in §2, appearing again.

> 🪝 **Snag — the arrow reverses exactly once, inside Prometheus's own architecture.** Alertmanager "handles alerts **sent by** client applications such as the Prometheus server" [source: prometheus-alertmanager-2026-08-31]. So Prometheus *pulls* from targets and *pushes* to Alertmanager. That is not a contradiction of the pull model — the pull model describes how metrics are **collected**, not how notifications are **dispatched**. Keep the two clauses separate and both facts fit.

### Asking questions of what you collected

Storing time series is only half of it. **PromQL** — "the Prometheus Query Language" [source: prometheus-glossary-2026-08-31] — is the functional query language that "lets the user select and aggregate time series data in real time" [source: prometheus-promql-basics-2026-08-31].

That is the whole of what you need. PromQL syntax is not KCNA surface; what matters is knowing that a query language exists, that it is the thing turning stored series into answers, and that the ability to write an *arbitrary* query is precisely what lifts a metrics store from "shows the dashboards we built" toward the §1 posture.

Results are available in the Prometheus UI, and "other programs can fetch the result of a PromQL expression via the HTTP API" [source: prometheus-promql-basics-2026-08-31]. Which brings us to the dashboard layer.

**Grafana** is the visualization tool most commonly paired with Prometheus — "Grafana or other API consumers can be used to visualize the collected data" [source: prometheus-overview-2026-08-23]. It reads through that HTTP API. It is not part of Prometheus, and Prometheus does not depend on it.

> 🪝 **Snag:** **Grafana is not a CNCF project.** This paragraph names Prometheus, OpenTelemetry, Jaeger and Fluentd — all CNCF — and it is very easy to sweep Grafana in with them. It is an open-source product from Grafana Labs. Related products from the same company (Loki for logs, Tempo for traces) are likewise outside CNCF and outside this exam's scope.

### Where Prometheus fits, and where it does not

Two statements from the project's own documentation are worth memorizing, because knowing a tool's stated *non*-fit is the kind of thing exams reward.

**On independence:** "Each Prometheus server is standalone, not depending on network storage or other remote services, so you can rely on it when other parts of your infrastructure are broken" [source: prometheus-overview-2026-08-23].

That is a deliberate design trade, not a limitation someone forgot to fix. The moment your monitoring system depends on your clustered storage, an outage in that storage takes down the thing that would have told you about the outage. Prometheus chooses to work alone so that it still works when nothing else does.

**On accuracy:** "Prometheus values reliability. If you need 100% accuracy, such as for per-request billing, Prometheus is not a good choice as the collected data will likely not be detailed and complete enough" [source: prometheus-overview-2026-08-23].

This follows directly from the pull model. Scraping samples state on an interval; it does not observe every event. If a counter increments 400 times between two scrapes, Prometheus sees the difference, not the four hundred events. For alerting, dashboards, and capacity work, that is exactly right and vastly cheaper. For invoicing a customer per API call, it is unacceptable — and the project says so itself.

> **⚠ Navigational Hazards**
>
> **"Reliability over completeness" is the sentence to carry.** A scenario that mentions billing, financial reconciliation, audit logs, or any phrase implying every single event must be counted is telling you that Prometheus is the *wrong* answer. Candidates who have learned "Prometheus is the metrics tool" pick it anyway, because the question is about numbers. The question is about *completeness*, and Prometheus explicitly trades that away for the ability to keep working during an outage.

> ⚓ **Worth Securing:** Prometheus "joined the Cloud Native Computing Foundation in 2016 as the **second** hosted project, after Kubernetes" [source: prometheus-overview-2026-08-23]. It was created at SoundCloud in 2012 [source: prometheus-overview-2026-08-23]. Second, not first — Kubernetes was first, and swapping those two is a real distractor.

---

## 🟡 §5 — Following One Request

This is the hardest section in the chapter, so let's build it the way you actually hit the problem — not from the vocabulary down, but from the wall you run into.

You met the wall in Soundings Q7.

### The wall

One user request enters your system. It hits the API gateway, which calls the auth service, which calls the user store; the gateway then calls the catalog service, which calls the pricing service, which calls a cache and then a database.

Seven processes. All seven log correctly. All seven log *well* — structured JSON, accurate timestamps, sensible messages. You have every log line from every service for the four seconds in question.

And you cannot answer "why did that request take four seconds."

Not because the data is missing. Because **nothing joins it**. There is no field in service E's log line that says *I am part of the same request as that line in service A*. You have seven complete stories about seven different subjects, and no way to know they were all about one customer pressing one button.

That is the gap. Everything in this section is one idea for closing it: **carry an identifier across the boundary**.

### Context, and moving it

**Context** is "an object that contains the information for the sending and receiving service, or execution unit, to correlate one signal with another" [source: opentelemetry-context-propagation-2026-08-31]. **Propagation** is "the mechanism that moves context between services and processes" [source: opentelemetry-context-propagation-2026-08-31]. Together, **context propagation** is what lets signals "be correlated with each other, regardless of where they are generated."

The concrete version is one sentence, and it is worth reading slowly because it is the whole mechanism: "Service A includes a trace ID and a span ID as part of the context. Service B uses these values to create a new span that belongs to the same trace" [source: opentelemetry-context-propagation-2026-08-31].

That is it. Service A stamps an identifier onto the outbound call. Service B reads it and stamps its own work as *belonging to that same identifier*. Repeat across seven hops and you have a chain that survives every process and network boundary in between. As OpenTelemetry puts it, context propagation "allows traces to build causal information about a system across services that are arbitrarily distributed across process and network boundaries" [source: opentelemetry-context-propagation-2026-08-31].

*Arbitrarily distributed.* That is the sentence closing the loop Chapter 17 opened. Break a monolith into twenty services and the request path becomes a thing you can no longer hold in your head — so you make the system carry the thread for you.

The identifier travels in HTTP headers; "the default propagator uses the headers specified by the W3C TraceContext specification" [source: opentelemetry-context-propagation-2026-08-31]. You do not need the header format for this exam. You need to know that the correlation rides *with the request*, in-band, rather than being reconstructed afterward by a clever log parser.

And baggage — the fourth signal from §2 — is the general form of the same trick: "Baggage allows you to propagate arbitrary key-value pairs" [source: opentelemetry-context-propagation-2026-08-31]. Trace and span IDs join the *work*. Baggage carries whatever else you want to travel with it: the customer ID, the origin IP, the feature-flag cohort.

### Span and trace

Now the vocabulary lands on a need you can feel.

A **span** "represents a unit of work or operation." Spans "track specific operations that a request makes, painting a picture of what happened during the time in which that operation was executed," and a span "contains name, time-related data, structured log messages, and other metadata (that is, attributes) to provide information about the operation it tracks" [source: opentelemetry-observability-primer-2026-08-23].

A **trace** — formally a distributed trace — "records the paths taken by requests (made by an application or end-user) as they propagate through multi-service architectures, like microservice and serverless applications" [source: opentelemetry-observability-primer-2026-08-23].

And the join between them, which is the exam's actual target:

> **★ Fixed Point**
>
> **A span is ONE unit of work. A trace is the WHOLE path a request took, and "a trace is made of one or more spans." "The first span represents the root span; each root span represents a request from start to finish"** [source: opentelemetry-observability-primer-2026-08-23]**. Spans beneath the root "provide a more in-depth context of what occurs during a request."**

Note "one or more." A single-service request produces a trace with exactly one span in it. A trace is not defined by being multi-service — it is defined by being *the whole request*.

<!-- FIGURE: ch18-fig03-trace-spans-across-services -->
```
   ONE TRACE = the whole request path.  ONE SPAN = one unit of work.
   trace ID: 4bf92f...  (crosses every boundary below)

   time ──────────────────────────────────────────────────────►
        0ms                                              4000ms

   ┌────────────────────────────────────────────────────────┐
   │ ROOT SPAN   api-gateway: POST /checkout      4000ms    │  request
   └─┬──────────────────────────────────────────────────────┘  start→finish
     │
     ├─┌──────────────┐
     │ │ auth-svc      120ms                                  │
     │ └─┬────────────┘
     │   └─┌────────────┐
     │     │ user-store   85ms                                │
     │     └────────────┘
     │
     └─────┌──────────────────────────────────────────────┐
           │ catalog-svc                        3700ms    │
           └─┬────────────────────────────────────────────┘
             │
             ├─┌───────┐
             │ │ cache   8ms                                  │
             │ └───────┘
             │
             └─┌──────────────────────────────────────────┐
               │ pricing-svc → database         3650ms    │ ◄── here
               └──────────────────────────────────────────┘

   Seven services. Seven sets of logs, each internally complete.
   Only the trace ID makes them one story — and only then does
   "where did the 4 seconds go?" have an answer.
```

Look at what that figure gives you that seven log files cannot: **nesting** and **duration**. You can see that pricing-svc's database call accounts for nearly the entire four seconds, and you can see it *without* comparing timestamps across seven files and hoping the clocks agree. The structure is the answer.

> 🪢 **Mnemonic:** A **span** *spans* one operation. A **trace** *traces* the whole route. If you can point at a single box on the diagram, it's a span; if you mean the entire picture, it's a trace. And the picture always starts with one box that covers all the others — the root.

> 🪝 **Snag:** "Span" and "trace" are used loosely and interchangeably in conversation all the time, including by people who know better. The exam does not use them loosely. If a question describes a single operation with a name and a duration, that is a span; if it describes the full journey of a request, that is a trace.

### Jaeger

Spans have to go somewhere.

**Jaeger** is a distributed tracing backend: it receives, processes, aggregates and visualizes trace data. It was originally built for OpenTracing and is now OpenTelemetry-compatible, with concepts mapping directly across the two.

<!-- AUTHOR-REVIEW: no cached snapshot for Jaeger — the corpus has no jaegertracing.io capture. The B7 ledger assigns Jaeger to this section and the outline requires it, so it is stated here untagged and deliberately kept to the minimum (what it is, what it receives, its OpenTracing origin and OTel compatibility). Research gap: fetch jaegertracing.io/docs/latest/architecture/ or the CNCF project page. Every other factual claim in §5 is tagged. -->

Keep the division of labor explicit, because it is going to matter in three paragraphs' time. OpenTelemetry is the *instrumentation* side — the APIs and SDKs that produce spans and export them. Jaeger is the *backend* — the thing that receives them, stores them, and draws the picture above. The OTel Collector supports Jaeger as one of its output formats [source: opentelemetry-collector-2026-08-31], which is exactly the arrangement: producer, wire format, consumer, all separable.

If that shape feels familiar, it should. Prometheus stores and Grafana reads. OTel exports and Jaeger receives. Two different corners of this chapter, same architecture.

### Spans you didn't ask for

One last thing, and it is the closing of a loop from Chapter 17.

A service mesh injects a proxy alongside every workload, and that proxy sees every request enter and leave. Because it sits in the path, it can emit spans for traffic that passes through it — for an application whose source code nobody touched. *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*

OpenTelemetry names this category directly: **zero-code instrumentation** is "great for getting started, or when you can't modify the application you need to get telemetry out of," and it provides "rich telemetry from libraries you use and/or the environment your application runs in" [source: opentelemetry-instrumentation-2026-08-31]. The environment your application runs in is precisely what a mesh is.

There is a real limit to it, though, and it is the difference between the two kinds of instrumentation from §1. The proxy knows what crossed the network: this service called that service, it took 40 milliseconds, it returned a 503. It does not know what happened *inside* — which branch the code took, which cache missed, which of three database queries was the slow one. Zero-code instrumentation gives you the shape of the request path for free. Code-based instrumentation is what fills in the boxes.

> **Logbook Entry:** The order in which teams typically adopt this is worth knowing, because it is not the order the documentation implies.
>
> Almost nobody starts with hand-instrumented traces. A team gets a mesh for mTLS or traffic management, notices they now have latency data per service for free, and builds a dashboard on it. That gets them to *which service is slow* — which resolves a large fraction of incidents, because "the pricing service is slow" is frequently all you needed.
>
> The push to real, code-level instrumentation comes later, and it always comes from the same place: an incident where "the pricing service is slow" was the *beginning* of the question rather than the end. Somebody has to know which of the four things pricing-svc does was the slow one, the mesh cannot say, and that afternoon somebody adds an OpenTelemetry SDK.
>
> The order matters for how you read exam scenarios. A question describing per-service latency in an uninstrumented app is describing the mesh. A question describing visibility *inside* a service is describing code-based instrumentation. The word "without changing the application" is doing real work whenever it appears.

---

## ☆ Taking Your Bearings: Pull, Push, and the Path One Request Took

Five questions. One draws on Chapter 17.

**1.** A team wants their long-running web service to report metrics to Prometheus. A developer proposes: "We'll have the service POST its metrics to the Pushgateway every 15 seconds — that way Prometheus doesn't have to reach into our network." Evaluate this proposal.

**2.** Your company bills customers per API call and needs the count to be exact for invoicing. An architect proposes Prometheus, reasoning that request counting is the canonical metrics use case. What is wrong with this, and what does the Prometheus documentation itself say?

**3.** A request enters your system, is handled by three services, and completes. Assuming full instrumentation, which is true?

- A) Three traces are produced, one per service, each containing one span
- B) One trace is produced, containing three or more spans, the first of which is the root span
- C) One span is produced, containing three traces
- D) Three root spans are produced and correlated afterward by timestamp

**4.** Name all four OpenTelemetry signals. For the one that is *not* a measurement, state what it is and why it is nonetheless a signal.

**5.** *[retrieval: ch17]* A service mesh is deployed and the platform team now has per-service latency and error rates for applications that were never instrumented. An engineer investigating a slow endpoint asks: "Which of the three database queries in that handler is slow?" Can the mesh telemetry answer that? Why or why not?

---

**Answers with Explanations:**

**1.** The proposal is wrong, and it is wrong for a reason more specific than "Prometheus pulls."

Prometheus collects "via a pull model over HTTP" [source: prometheus-overview-2026-08-23], and the Pushgateway is not a general-purpose bypass for that. It is "an intermediary service which allows you to push metrics from jobs which cannot be scraped," and "the only valid use case for the Pushgateway is for capturing the outcome of a service-level batch job" [source: prometheus-pushgateway-practices-2026-08-31].

A long-running web service **can** be scraped — that is the entire distinction. The correct design is a client library exposing a metrics endpoint, plus service discovery so Prometheus finds it. Note also that even the Pushgateway does not reverse the arrow into Prometheus: Prometheus scrapes *the gateway*.

**2.** The architect has matched on the word "metrics" and missed the requirement, which is **completeness**, not measurement.

Prometheus states its own non-fit: "If you need 100% accuracy, such as for per-request billing, Prometheus is not a good choice as the collected data will likely not be detailed and complete enough" [source: prometheus-overview-2026-08-23]. The billing example is the documentation's own. This falls out of the pull model — scraping samples state on an interval rather than observing every event.

The trade is deliberate: "Prometheus values reliability" [source: prometheus-overview-2026-08-23], and each server is standalone specifically so it works "when other parts of your infrastructure are broken." Billing needs an event stream that captures every transaction, which is a different system.

**3. B.** "A trace is made of one or more spans. The first span represents the root span; each root span represents a request from start to finish" [source: opentelemetry-observability-primer-2026-08-23]. One request, one trace, spans beneath the root for each unit of work.

- **A is wrong** and is the answer someone gives who is thinking in log files — one artifact per service. Traces are per-*request*, which is exactly what makes them useful across service boundaries.
- **C is wrong** and inverts the containment. Traces contain spans, not the reverse.
- **D is wrong** twice over. There is one root span per trace, and correlation comes from propagated trace and span IDs, not from comparing timestamps after the fact [source: opentelemetry-context-propagation-2026-08-31]. Timestamp correlation is precisely the fragile thing tracing exists to replace.

**4. Traces, metrics, logs, and baggage** [source: opentelemetry-signals-2026-08-23].

The one that is not a measurement is **baggage**: "contextual information that is passed between signals" [source: opentelemetry-signals-2026-08-23], a key-value store that propagates data — user IDs, account identifiers, origin IPs — from the start of a request to services further downstream [source: opentelemetry-baggage-2026-08-31].

It counts as a signal because it is a distinct thing the system emits and propagates, with its own store: "baggage is a separate key-value store and is unassociated with attributes on spans, metrics, or logs without explicitly adding them" [source: opentelemetry-baggage-2026-08-31]. It is not a field on a span; it rides alongside, which is what makes it separable and what makes it forgettable.

**5. No.**

The mesh proxy sits in the network path and reports on what crosses it: which service called which, how long the call took, what status came back. Database queries *inside* a handler never cross the proxy, so the proxy has no knowledge of them at all.

This is the boundary between zero-code and code-based instrumentation. Zero-code is "great for getting started, or when you can't modify the application," providing telemetry "from libraries you use and/or the environment your application runs in" [source: opentelemetry-instrumentation-2026-08-31] — but seeing inside a request handler requires instrumentation *in* the handler. Answering this engineer's question means code-based instrumentation. *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*

---

**Checkpoint: You've Now Mastered**

✓ The direction of the arrow, and the one narrow exception to it
✓ Prometheus's components, and where the project says it does *not* fit
✓ Span versus trace versus root span, as a containment relationship
✓ All four signals, including the one you'd otherwise drop
✓ What mesh-generated telemetry can and cannot see

Two content sections left. The next one is the most mechanical in the chapter, and the one after it names the question all of this has been in service of.

---

## 🔵 §6 — Lines From Everywhere

Start with the limit, because everything downstream is a consequence of it.

**Kubernetes provides no native storage for log data.** Container logs are written to the node's filesystem by the container runtime; the kubelet manages them there; and that is the end of the platform's involvement. If you want logs that outlive the node, the Pod, or the rotation window, you need a separate backend — and something to get the lines to it.

That is what cluster-level logging is: an architecture bolted alongside Kubernetes, not a feature inside it.

### Why `kubectl logs` is not an archive

You have used `kubectl logs` since Chapter 13. *[cross-bearing: see Ch 13 §3 — looking inside]* It is a diagnostic, and it is bounded in three separate ways.

**Rotation.** The kubelet rotates container log files. The defaults are `containerLogMaxSize` of 10Mi and `containerLogMaxFiles` of 5 — and critically, **only the contents of the latest log file are available through `kubectl logs`**. A chatty container blows through 10Mi in minutes, and the lines you wanted are in a rotated file the command will not read.

**Restarts.** The kubelet keeps the logs of one terminated container so that `kubectl logs --previous` can reach one restart back. One. Not three, not "since the Pod was created."

**Eviction.** When a Pod is evicted, its containers are evicted with their logs. *[cross-bearing: see Ch 13 §4 — pods that start and then don't stay]* The Pod that got OOMKilled and evicted at 3 a.m. took the evidence with it.

That last one is the reason the whole architecture exists. Every other limit is inconvenient; this one means the exact failure you most want to investigate is the one that most reliably destroys its own logs.

> **⚠ Navigational Hazards**
>
> The mistake is treating `kubectl logs` as a log store because it is the log command you know. It is a live-tail-and-recent-history diagnostic scoped to one container on one node. Any scenario involving *yesterday*, *across all replicas*, *searching for a pattern*, or *a Pod that no longer exists* is describing cluster-level logging, and `kubectl logs` is the wrong answer.

### The three architectures

The Kubernetes documentation describes three approaches to getting logs off a node and into a backend.

<!-- FIGURE: ch18-fig06-cluster-logging-architectures -->
```
   THREE WAYS TO COLLECT.  Same backend in all three;
   the difference is WHERE collection happens.

   ┌─ 1. NODE-LEVEL AGENT ────────┐  ← the default answer
   │  NODE                        │
   │  ┌──────┐ ┌──────┐ ┌──────┐  │
   │  │ Pod  │ │ Pod  │ │ Pod  │  │
   │  └──┬───┘ └──┬───┘ └──┬───┘  │
   │     └────────┼────────┘      │
   │        node filesystem       │
   │              ▼               │
   │      ┌───────────────┐       │
   │      │ AGENT (Daemon │───────┼──────┐
   │      │ Set: 1/node)  │       │      │
   │      └───────────────┘       │      │
   └──────────────────────────────┘      │
                                          │
   ┌─ 2. SIDECAR IN THE POD ──────┐      │
   │  NODE                        │      │
   │  ┌────────────────────────┐  │      │
   │  │ Pod                    │  │      ▼
   │  │ ┌─────┐  ┌───────────┐ │  │  ┌────────┐
   │  │ │ app │─►│ sidecar   │─┼──┼─►│ LOGGING│
   │  │ └─────┘  │ collector │ │  │  │ BACKEND│
   │  │          └───────────┘ │  │  │        │
   │  └────────────────────────┘  │  │(outside│
   │   one collector PER POD      │  │  k8s)  │
   └──────────────────────────────┘  │        │
                                      │        │
   ┌─ 3. APP PUSHES DIRECTLY ─────┐  │        │
   │  NODE                        │  │        │
   │  ┌────────────────────────┐  │  │        │
   │  │ Pod                    │  │  │        │
   │  │ ┌─────────────────┐    │  │  │        │
   │  │ │ app w/ logging  │────┼──┼──┼───────►│
   │  │ │ library         │    │  │  └────────┘
   │  │ └─────────────────┘    │  │
   │  └────────────────────────┘  │   app must know
   │   no collector at all        │   about the backend
   └──────────────────────────────┘
```

**1. A node-level logging agent.** One agent per node, reading the container log files the runtime already writes, forwarding them to a backend. This is the default answer, and the reason is structural: the logs are already on the node's filesystem, for every container the node runs, whether or not the application cooperated. One agent covers everything.

The workload resource for "exactly one Pod on every node" is the **DaemonSet** *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]*, and node-level log collection is its canonical example. When a new node joins the cluster, it gets the agent automatically, because that is what a DaemonSet does.

**2. A dedicated sidecar container** in the application Pod, collecting that application's logs. Useful when an application writes to a file inside the container rather than to stdout, or needs per-application processing. The cost is one extra container per Pod rather than one per node — which, on a node running forty Pods, is a meaningfully different resource bill.

**3. The application pushes directly** to a logging backend from within the application. No collector at all; the app knows the backend's address and speaks its protocol. Simple, and it couples your application code to your logging vendor.

> ⚓ **Worth Securing:** "Which architecture?" almost always answers **node-level agent as a DaemonSet**, and the discriminator is worth stating as a rule: node-level collection is the only option that works *without the application's cooperation*. That is exactly why platform teams choose it — the platform team does not control what forty application teams write, and cannot make forty deploys to fix logging.

### Fluentd and Fluent Bit

Two agents dominate this slot, and the exam-adjacent detail is their relationship.

**Fluentd** is a CNCF graduated project. Its design idea is the unified logging layer: it "tries to structure data as JSON as much as possible: this allows Fluentd to unify all facets of processing log data" [source: fluentd-architecture-2026-08-31], and it "connects dozens of data sources and data outputs" [source: fluentd-architecture-2026-08-31] through "a flexible plugin system that allows the community to extend its functionality" [source: fluentd-architecture-2026-08-31] — over 500 community-contributed plugins [source: fluentd-architecture-2026-08-31]. Fluentd was accepted into the CNCF in November 2016 and graduated in 2019 [source: fluentd-architecture-2026-08-31].

**Fluent Bit** is "an open source telemetry agent that processes logs, metrics, traces, and profiles," created in 2014 by Eduardo Silva "as a lightweight log processor, developed by the Fluentd team at Treasure Data for constrained environments such as embedded Linux"; it is "a sub-project of Fluentd" [source: fluent-bit-overview-2026-08-23].

Why two? Footprint. A vanilla Fluentd instance "runs on 30-40MB of memory" [source: fluentd-architecture-2026-08-31] — trivial on a server, less trivial multiplied across every node in a large fleet, and genuinely limiting on constrained hardware. Fluent Bit is the lightweight answer. Both "are commonly deployed on Kubernetes as node-level logging agents (DaemonSets) that collect container logs from each node and forward them to a backend" [source: fluent-bit-overview-2026-08-23].

Fluent Bit's pipeline has six stages, in order [source: fluent-bit-overview-2026-08-23]:

| Stage | What it does |
|---|---|
| **Input** | Plugins gather information from sources — log files, OS metrics |
| **Parser** | Converts unstructured data to structured data |
| **Filter** | Alters collected data before delivery |
| **Buffer** | Stores data, in memory or on the filesystem |
| **Router** | Routes data through filters and on to one or more destinations, using tags and matching rules |
| **Output** | Plugins define destinations — remote services, local filesystems, standard interfaces |

> 🪢 **Mnemonic:** **Fluentd** is one word. **Fluent Bit** is two. The parent is a single compound; the lightweight child is "Fluent" plus a "Bit" of it. That asymmetry looks like a typo and is not — and a question that renders one of them wrong is testing whether you noticed.

> 🪝 **Snag:** Fluentd is CNCF graduated *as of the source cached for this book*. Project maturity levels change, and a question asking which projects are *currently* graduated is asking about a moving roster rather than a durable fact. What is durable and worth knowing: Fluentd is the CNCF project, Fluent Bit is its lighter sub-project, and both serve as node-level agents. *[cross-bearing: see Ch 17 §2 — sandbox, incubating, graduated, and who decides]*

---

## 🔵 §7 — Is the Service Doing What Users Expect

Six sections of instruments. Here is the question they exist to answer.

**Reliability answers the question: "Is the service doing what users expect it to be doing?"** [source: opentelemetry-observability-primer-2026-08-23]

That is the whole thing. Not "is CPU below 80%." Not "are all Pods `Running`." Not "did the probes pass." Every one of those can be true while the service is failing the people using it, and every one of them can be false while users are perfectly happy.

The rest of this section is vocabulary for making that question answerable — turning "is it doing what users expect" from a feeling into a number somebody can be held to.

### Three letters that get swapped

Take them in dependency order, because the dependency order is the memory hook.

**An SLI — Service Level Indicator — "represents a measurement of a service's behavior. A good SLI measures your service from the perspective of your users"** [source: opentelemetry-observability-primer-2026-08-23]. Google's definition is complementary: "a carefully defined quantitative measure of some aspect of the level of service that is provided" [source: sre-book-service-level-objectives-2026-08-31].

The user-perspective clause is the part with teeth. "Average CPU across the fleet" is a measurement, and it is not an SLI in any useful sense, because no user has ever cared about it. "The proportion of checkout requests that completed successfully in under 400ms" is an SLI. The difference is whose experience is being measured.

**An SLO — Service Level Objective — "is the means by which reliability is communicated to an organization/other teams. This is accomplished by attaching one or more SLIs to business value"** [source: opentelemetry-observability-primer-2026-08-23]. Or, mechanically: "a target value or range of values for a service level that is measured by an SLI" [source: sre-book-service-level-objectives-2026-08-31].

The SLI is the measurement. The SLO is the *target you commit to* on that measurement. 99.5% of checkout requests under 400ms, over a rolling 30 days — that is an SLO, and it takes an SLI as its input.

> **★ Fixed Point**
>
> **An SLI is the MEASUREMENT. An SLO is the OBJECTIVE — a target value for that measurement. The SLI is a number you observe; the SLO is a number you commit to.**

**An SLA — Service Level Agreement** — is the third term, and it is here mostly because it is the distractor. SLAs are "an explicit or implicit contract with your users that includes consequences of meeting (or missing) the SLOs they contain" [source: sre-book-service-level-objectives-2026-08-31]. External, contractual, with teeth.

The discrimination has a procedure rather than requiring you to hold two definitions side by side: "An easy way to tell the difference between an SLO and an SLA is to ask 'what happens if the SLOs aren't met?': if there is no explicit consequence, then you are almost certainly looking at an SLO" [source: sre-book-service-level-objectives-2026-08-31].

> 🪢 **Mnemonic:** **I** for **I**ndicator — what you *measure*. **O** for **O**bjective — what you *aim at*. **A** for **A**greement — what you *sign*, with consequences attached. And the containment runs the same direction as the letters: an SLA contains SLOs, which are measured by SLIs.

> 🪝 **Snag:** SLI and SLO get swapped constantly, in the wild and on exams. When a question describes *a number being observed*, that is the SLI. When it describes *a threshold being committed to*, that is the SLO. When it mentions penalties, credits, or a customer contract, that is the SLA.

### Error budgets, in one clause

If your SLO is 99.9%, then 0.1% of unreliability is not a failure — it is a budget. That is the whole idea, and its value is organizational rather than mechanical: "as long as the uptime measured is above the SLO — in other words, as long as there is error budget remaining — new releases can be pushed" [source: sre-book-error-budgets-2026-08-31].

The reason this exists is a structural tension. "Product development performance is largely evaluated on product velocity, which creates an incentive to push new code as quickly as possible. Meanwhile, SRE performance is evaluated based upon reliability of a service, which implies an incentive to push back against a high rate of change" [source: sre-book-error-budgets-2026-08-31]. Two teams, opposed incentives, no shared referee.

The error budget is the referee. It converts an argument about judgment into a number both sides agreed to in advance. That is not a monitoring mechanism; it is a decision-making one, which is why it is worth one clause and no more here.

### The four golden signals

If you can instrument only four things on a user-facing system, these are the four [source: sre-book-four-golden-signals-2026-08-23]:

**Latency** — "the time it takes to service a request." With one crucial refinement: "It's important to distinguish between the latency of successful requests and the latency of failed requests." An HTTP 500 caused by a dropped database connection "might be served very quickly," so folding 500s into overall latency "might result in misleading calculations." And, memorably: "a slow error is even worse than a fast error!" [source: sre-book-four-golden-signals-2026-08-23]

**Traffic** — "a measure of how much demand is being placed on your system, measured in a high-level system-specific metric." Usually HTTP requests per second for a web service; network I/O rate or concurrent sessions for audio streaming; transactions and retrievals per second for a key-value store [source: sre-book-four-golden-signals-2026-08-23].

**Errors** — "the rate of requests that fail, either explicitly (e.g., HTTP 500s), implicitly (for example, an HTTP 200 success response, but coupled with the wrong content), or by policy (for example, 'If you committed to one-second response times, any request over one second is an error')" [source: sre-book-four-golden-signals-2026-08-23].

**Saturation** — "how 'full' your service is. A measure of your system fraction, emphasizing the resources that are most constrained." And the operational warning: "many systems degrade in performance before they achieve 100% utilization, so having a utilization target is essential" [source: sre-book-four-golden-signals-2026-08-23].

<!-- FIGURE: ch18-fig05-sli-slo-golden-signals -->
```
  MEASUREMENT → COMMITMENT → CONTRACT     THE FOUR GOLDEN SIGNALS

  ┌─────────────────────────────┐        ┌──────────┐ ┌──────────┐
  │  INTERNAL                   │        │ LATENCY  │ │ TRAFFIC  │
  │                             │        │ time to  │ │ demand   │
  │   ┌─────┐    measures       │        │ serve a  │ │ on the   │
  │   │ SLI │  ──────────┐      │        │ request  │ │ system   │
  │   │     │            │      │        │          │ │          │
  │   │ the │            ▼      │        │ track OK │ │ req/sec, │
  │   │ mea-│      ┌──────────┐ │        │ and FAIL │ │ sessions │
  │   │sure-│      │   SLO    │ │        │ separate │ │          │
  │   │ ment│      │ the      │ │        └──────────┘ └──────────┘
  │   └─────┘      │ target   │ │        ┌──────────┐ ┌──────────┐
  │                │ you      │ │        │  ERRORS  │ │SATURATION│
  │  from the      │ commit to│ │        │ rate of  │ │ how FULL │
  │  USER's        └────┬─────┘ │        │ failed   │ │ the svc  │
  │  perspective        │       │        │ requests │ │ is       │
  └─────────────────────┼───────┘        │          │ │          │
                        │                │ explicit,│ │ degrades │
        ══════ boundary ══════            │ implicit,│ │ BEFORE   │
                        │                │ or by    │ │ 100%     │
  ┌─────────────────────▼───────┐        │ policy   │ │          │
  │  EXTERNAL                   │        └──────────┘ └────▲─────┘
  │        ┌──────────┐         │                          │
  │        │   SLA    │         │        latency increases ─┘
  │        │ contract │         │        are often a LEADING
  │        │ w/ CONSE-│         │        INDICATOR of saturation
  │        │ QUENCES  │         │
  │        └──────────┘         │
  │  "what happens if the SLO   │
  │   isn't met?" No consequence│
  │   = it's an SLO, not an SLA │
  └─────────────────────────────┘
```

> 🪢 **Mnemonic:** **L-T-E-S.** Latency, Traffic, Errors, Saturation. Or read the figure as a sentence: *how long, how much, how broken, how full.*

And the one relationship among the four that is worth carrying: **"Latency increases are often a leading indicator of saturation"** [source: sre-book-four-golden-signals-2026-08-23]. Response times creeping up before anything looks full is the system telling you it is about to be. Treat that as the early warning it is.

### RED and USE

Two other framings appear alongside the golden signals, and both are named in the CNCF TAG Observability whitepaper [source: cncf-tag-observability-whitepaper-2026-08-31]. Their value here is the contrast between them, not their details.

**USE** — "the Utilization Saturation and Errors (USE) Method is a methodology for analyzing the performance of any system," directing "the construction of a checklist, which for server analysis can be used for quickly identifying resource bottlenecks or errors" [source: use-method-brendan-gregg-2026-08-31]. It is oriented at **resources**.

**RED** — Rate, Errors, Duration: "the number of requests per second," "the number of those requests that are failing," and "the amount of time those requests take" [source: red-method-tom-wilkie-2026-08-31]. It is oriented at **services**.

The person who created RED drew the line himself: "The USE Method doesn't really apply to services; it applies to hardware, network disks, things like this. We really wanted a microservices-oriented monitoring philosophy, so we came up with the RED Method" [source: red-method-tom-wilkie-2026-08-31].

That is the whole complementarity, and note what produced it. RED exists *because* one service became twenty. *[cross-bearing: see Ch 17 §3 — small pieces, replaced whole]* The architecture changed, and the measurement framing had to change with it — which is this chapter's thesis showing up in the methodology literature.

> 🔭 **Closer Look — one word, three meanings.** "Utilization" now means three different things in this chapter, and all three are correct in their own context. In §3, utilization is **a percentage of the containers' resource request** [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31]. In the USE method, utilization is "the average time that the resource was busy servicing work" [source: use-method-brendan-gregg-2026-08-31] — a duration fraction. And the golden-signals concept nearest to both is **saturation**, how full the service is [source: sre-book-four-golden-signals-2026-08-23]. When you meet the word in a question, check which system is speaking.

<!-- AUTHOR-REVIEW: RED's only surviving authoritative source is a Grafana Labs blog post by Tom Wilkie, the method's originator — the original Weaveworks publication is dead, and the CNCF TAG Observability whitepaper's RED link now points to that dead host. That is the method's author but is not official documentation, and no CNCF/LF source defines RED. Per the outline's stated posture, RED is named and contrasted here but carries no teaching weight, and no graded item in this chapter depends on it. B1 gap G21 should be recorded as substantially-but-not-fully closed. -->

---

## ☆ Taking Your Bearings: Lines, Signals, and the Question They Answer

Five questions. One draws on Chapter 6.

**1.** A Pod has restarted four times over the past hour. You need to see what the container printed before its *first* crash. Can you get it with `kubectl logs`? Explain, naming the specific mechanisms involved.

**2.** Name the three cluster-logging architectures. Which is the default answer for a platform team, and what is the structural reason?

**3.** A team commits: "99.9% of API requests will complete successfully within 300ms, measured over a rolling 30 days. If we miss this in a calendar quarter, affected enterprise customers receive a 10% service credit." Identify the SLI, the SLO, and the SLA in that statement.

**4.** Name the four golden signals. For one of them, state a relationship it has to another that makes it useful as an early warning.

**5.** *[retrieval: ch6]* Your log-collection agent must run on every node in the cluster, including nodes added tomorrow. Which workload resource, and why not a Deployment with `replicas` set to the node count?

---

**Answers with Explanations:**

**1.** No, on two independent grounds, and you should be able to name both.

**Rotation:** the kubelet rotates container logs — `containerLogMaxSize` 10Mi and `containerLogMaxFiles` 5 by default — and only the *latest* log file's contents are available through `kubectl logs`. Even within a single container run, older output can already be out of reach.

**Restart depth:** the kubelet retains the logs of *one* terminated container, which is what `kubectl logs --previous` reads. One restart back, not four.

Four restarts ago is gone from the node. Retrieving it requires cluster-level logging — an agent that shipped those lines to a backend before the node discarded them. *[cross-bearing: see Ch 13 §3 — looking inside]*

**2.** The three: **a node-level logging agent** (typically a DaemonSet), **a dedicated sidecar container** in the application Pod, and **the application pushing directly** to a backend.

The default is the **node-level agent**, and the structural reason is that it works *without the application's cooperation*. Container logs are already written to the node's filesystem for every container the node runs, whether the application team did anything or not. One agent per node covers all of them, including workloads owned by teams the platform team has never spoken to. Sidecars require a change to every Pod spec; direct push requires a change to every application.

**3.**
- **SLI:** the proportion of API requests completing successfully within 300ms. This is the measurement, and it is user-perspective — it measures what a caller experiences [source: opentelemetry-observability-primer-2026-08-23].
- **SLO:** 99.9% of them, over a rolling 30 days. The target value attached to the SLI [source: sre-book-service-level-objectives-2026-08-31].
- **SLA:** the 10% service credit. Apply the test — "what happens if the SLOs aren't met?" [source: sre-book-service-level-objectives-2026-08-31] There is an explicit consequence, so this clause is the agreement, not the objective.

**4. Latency, traffic, errors, saturation** [source: sre-book-four-golden-signals-2026-08-23].

The relationship worth naming: **"Latency increases are often a leading indicator of saturation"** [source: sre-book-four-golden-signals-2026-08-23]. Because many systems degrade before reaching 100% utilization, rising response times frequently appear *before* any saturation metric looks alarming.

(Also acceptable: latency's relationship to errors — failed-request latency must be tracked separately, because a fast 500 makes overall latency look good while "a slow error is even worse than a fast error" [source: sre-book-four-golden-signals-2026-08-23].)

**5. A DaemonSet.**

A DaemonSet's semantics are "one Pod per node," maintained by the controller. When a node joins the cluster, it gets a Pod automatically; when a node leaves, the Pod goes with it. *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]*

A Deployment with `replicas: 12` gives you twelve Pods, placed by the scheduler according to feasibility and scoring. Nothing guarantees one per node — the scheduler may well put two on a roomy node and none on a constrained one *[cross-bearing: see Ch 7 §1 — one decision, made once]*. And the count is a number *you* set, which is stale the moment the cluster scales. Log collection is a per-node job, so it needs the resource whose contract is per-node.

---

**Checkpoint: You've Now Mastered**

✓ Why `kubectl logs` is a diagnostic and not an archive — rotation, restart depth, eviction
✓ The three cluster-logging architectures, and why one is the default
✓ SLI, SLO, and SLA, with a procedure for telling the last two apart
✓ The four golden signals, and saturation's early warning

One section left. It introduces nothing.

---

## ☀️ §8 — One Question, Four Instruments

You have four instruments now. Here is the thing nobody said while you were collecting them.

**They are not four topics. They are four ways of asking §7's one question.**

*Is the service doing what users expect it to be doing?* [source: opentelemetry-observability-primer-2026-08-23]

Ask it of a **metric** and you get *whether* — a number over time, aggregated, that tells you the error rate crossed 2% at 02:07 and is still climbing. Ask it of a **trace** and you get *where* — the request took four seconds and 3.65 of them were in one database call inside pricing-svc. Ask it of a **log** and you get *what* — the specific line the code emitted at the moment it gave up, with the exception and the parameters. And **baggage** is what lets the first three be about the same request rather than three unrelated stories that happened to occur at the same time.

That is the payoff of the fourth signal, and it is why dropping it from the list is worse than a memory slip. Without something carrying context across the boundary, you have three instruments pointed at three different things. With it, you have one question examined at three resolutions.

<!-- FIGURE: ch18-zenith-instruments-answer-one-question -->
```
                    ┌───────────────────────────┐
                    │   "Is the service doing   │
                    │   what users expect       │
                    │   it to be doing?"        │
                    └─────────────▲─────────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                   │
       ┌──────┴──────┐     ┌──────┴──────┐     ┌──────┴──────┐
       │   METRIC    │     │    TRACE    │     │     LOG     │
       │             │     │             │     │             │
       │  WHETHER    │     │   WHERE     │     │    WHAT     │
       │             │     │             │     │             │
       │ error rate  │     │ 3.65s of 4s │     │ the line    │
       │ crossed 2%  │     │ in pricing- │     │ the code    │
       │ at 02:07    │     │ svc's query │     │ actually    │
       │             │     │             │     │ emitted     │
       └──────┬──────┘     └──────┬──────┘     └──────┬──────┘
              │                   │                   │
              └───────────────────┼───────────────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │  BAGGAGE — what makes all │
                    │  three about THE SAME     │
                    │  REQUEST rather than      │
                    │  three separate stories   │
                    └───────────────────────────┘

           Not four topics. One question, four resolutions.
```

### The other thing that kept happening

There is a second pattern in this chapter, quieter than the first, and you have now seen it four times.

OpenTelemetry exports; Jaeger receives. Prometheus stores; Grafana reads, through an HTTP API [source: prometheus-promql-basics-2026-08-31]. The kubelet writes container logs to the node; an agent ships them somewhere else. The OTel Collector receives one set of signals and exports to "one or more open source or commercial backends" [source: opentelemetry-collector-2026-08-31].

Every one of those is the same shape: **the thing that produces telemetry and the thing that stores it are separate, and either can be replaced without the other noticing.** Swap Jaeger for a commercial tracing vendor and your instrumented services do not change. Swap Fluentd for Fluent Bit and your applications do not change. Point the Collector at a different backend and nothing upstream of it knows.

You have met this argument before, in a domain you would not have expected it in. *[cross-bearing: see Ch 17 §4 — every place Kubernetes lets you in]* Chapter 17 made the case that Kubernetes' durability comes from defining interfaces rather than implementations, so that pieces can be replaced without the whole being redesigned. It turns out the observability ecosystem was built on the same conviction — by different people, for different reasons, arriving at the same architecture. That is not a coincidence you should file away as trivia. It is the reason both ecosystems are still standing.

### Where that leaves you

Chapter 17 handed you a bill: everything that made the system easier to change made it harder to see.

This chapter is the payment, and it is not a set of tools. It is a *disposition* — the habit of asking, before an incident rather than during one, *what would I need to be emitting for this question to have an answer?* The instruments follow from that. The dashboards follow from the instruments. Nothing works in the other direction, which is why teams who start by buying a dashboard product are frequently the ones who cannot explain their own outages.

You know what the four signals are. You know which one tells you whether, which tells you where, which tells you what, and which makes them agree on the subject. You know that Prometheus reaches out rather than being reported to, that a trace is the whole path and a span is one piece of it, that logs leave the node by a route Kubernetes does not provide, and that all of it is in service of a single sentence about users.

The question was never "do we have monitoring." The question is: *is the service doing what users expect?* — and now you can find out.

---

## Exam Alert! 🚨

**High-Priority Topics:**

1. **The four signals.** Traces, metrics, logs, **baggage**. The count is what gets tested; baggage is what gets dropped.
2. **Prometheus pulls.** It scrapes over HTTP. Push exists only via the Pushgateway, only for service-level batch jobs.
3. **Span vs trace.** A span is one unit of work. A trace is the whole path — one or more spans, starting at the root span.
4. **SLI vs SLO.** Measurement versus objective. SLA is the third term and the usual distractor.
5. **Observability vs monitoring.** New questions versus pre-chosen indicators. Not "dashboards versus no dashboards."
6. **metrics-server is not a monitoring system.** The exam tests the boundary, not either side.

**Common Traps** — each of these has cost real candidates real points:

| The trap | The correct understanding |
|---|---|
| "Observability is monitoring with better dashboards" | Observability handles **unknown unknowns** — questions you did not plan for. Monitoring detects known unknowns [source: cncf-tag-observability-whitepaper-2026-08-31] |
| Naming three signals | **Four.** Baggage is contextual information passed *between* signals [source: opentelemetry-signals-2026-08-23] |
| Using "span" and "trace" interchangeably | One unit of work versus the whole request path [source: opentelemetry-observability-primer-2026-08-23] |
| "Logs are the richest signal, so lead with them" | Logs "are not extremely useful for tracking code execution on their own, as they typically lack contextual information" [source: opentelemetry-observability-primer-2026-08-23] |
| SLI and SLO swapped | SLI **measures**; SLO **commits**. If there's a consequence attached, it's an SLA [source: sre-book-service-level-objectives-2026-08-31] |
| "Prometheus pushes" / "apps report to Prometheus" | It **scrapes over HTTP**. Pushgateway is an intermediary for jobs too short to scrape [source: prometheus-pushgateway-practices-2026-08-31] |
| "Prometheus for per-request billing" | Explicitly not — "if you need 100% accuracy… Prometheus is not a good choice" [source: prometheus-overview-2026-08-23] |
| "Prometheus needs clustered/network storage" | Each server is **standalone by design**, so it works "when other parts of your infrastructure are broken" [source: prometheus-overview-2026-08-23] |
| "Prometheus was CNCF's first project" | **Second**, in 2016. Kubernetes was first [source: prometheus-overview-2026-08-23] |
| Expecting Observability as a standalone domain | It is competency material inside **Cloud Native Architecture** [source: lf-kcna-program-changes-2026-08-23]. *[cross-bearing: see Ch 1 — the curriculum that moved under everyone's feet]* |
| "Grafana is a CNCF project" | It is not. Neither are Loki or Tempo. Prometheus, OpenTelemetry, Jaeger and Fluentd are |
| `kubectl logs` as a log archive | Rotation, one-restart depth, and eviction all bound it. Anything historical needs cluster-level logging |

---

## Practice Questions

Seventeen questions. Four are interleaved with earlier chapters and tagged. Explanations follow all seventeen; resist the urge to scroll.

---

**Q1.** Which statement best captures the difference between monitoring and observability?

- A) Monitoring is open-source; observability requires commercial tooling
- B) Monitoring detects known unknowns; observability additionally lets you find and reason about unknown unknowns
- C) Monitoring covers infrastructure; observability covers applications
- D) Monitoring is real-time; observability is historical

---

**Q2.** By OpenTelemetry's stated definition, an application is properly instrumented when:

- A) It emits at least the four golden signals
- B) It has been onboarded to a CNCF-graduated observability backend
- C) Developers do not need to add more instrumentation to troubleshoot an issue, because they already have the information they need
- D) It emits all four OpenTelemetry signals, including baggage

---

**Q3.** Which is the complete list of signals OpenTelemetry currently supports?

- A) Traces, metrics, logs
- B) Traces, metrics, logs, baggage
- C) Metrics, logs, traces, profiles, dumps
- D) Traces, metrics, logs, alerts

---

**Q4.** Baggage is best described as:

- A) An attribute automatically attached to every span in a trace
- B) A separate key-value store propagated between services, carrying contextual data that the other signals can incorporate
- C) The buffered queue of telemetry awaiting export by the Collector
- D) The metadata section of a log record

---

**Q5.** A dashboard shows a Pod at "85% CPU utilization." That percentage is calculated against:

- A) The node's total allocatable CPU
- B) The container's CPU limit
- C) The equivalent CPU resource request on the containers in the Pod
- D) The namespace's ResourceQuota for CPU

---

**Q6.** *[retrieval: ch5]* A Deployment's Pod template sets CPU limits but no CPU requests. An HPA targets 60% CPU utilization for it. What happens?

- A) The HPA scales against the limit as the denominator
- B) The HPA scales against node allocatable, divided by Pod count
- C) CPU utilization is undefined for the Pod and the HPA takes no action on that metric
- D) The Pod is rejected at admission until a request is set

---

**Q7.** *[retrieval: ch13]* Your team needs to answer: "What was the memory usage of the `payments` Deployment at 3 a.m. last Tuesday, and did it correlate with the error spike?" The cluster runs metrics-server. What is required?

- A) Nothing further; `kubectl top` with a timestamp flag answers this
- B) A monitoring system with time-series storage — metrics-server retains no history and does not collect application error metrics
- C) Increase metrics-server's retention configuration
- D) Enable the metrics-server aggregation layer for historical queries

---

**Q8.** How does the Prometheus server obtain metrics from an instrumented, long-running application?

- A) The application POSTs metrics to Prometheus on an interval
- B) Prometheus scrapes an HTTP endpoint on the application, on an interval
- C) The application writes to a shared volume Prometheus reads
- D) The kubelet forwards metrics to Prometheus via the CRI

---

**Q9.** Which scenario is the documented, valid use of the Pushgateway?

- A) A high-traffic web API that prefers outbound connections to inbound ones
- B) A nightly database-maintenance batch job, not tied to a specific machine, whose outcome must be recorded
- C) A stateful application requiring exactly-once metric delivery
- D) Any workload behind a firewall Prometheus cannot reach

---

**Q10.** A company needs an exact count of every API call for per-customer invoicing. What does the Prometheus documentation say about this use case?

- A) It is well suited; counters are the canonical Prometheus use case
- B) It is suitable with the `--storage.tsdb.exact-counting` flag enabled
- C) It is explicitly a poor fit — Prometheus does not guarantee 100% accuracy, naming per-request billing as an example
- D) It is suitable if the Pushgateway is used for every request

---

**Q11.** Which statement about Prometheus's storage architecture is correct?

- A) It requires a clustered backend such as Cassandra for durability
- B) Each server is standalone and does not depend on network storage or other remote services, so it works when other infrastructure is broken
- C) It uses etcd, sharing the cluster's control-plane datastore
- D) It stores data in the Kubernetes API server as custom resources

---

**Q12.** Which correctly describes the relationship between traces and spans?

- A) A span contains one or more traces; the first trace is the root trace
- B) A trace contains one or more spans; the first span is the root span, representing the request from start to finish
- C) Traces and spans are synonyms in OpenTelemetry
- D) A trace contains exactly one span per service the request touches, never more

---

**Q13.** *[retrieval: ch17]* A request crosses six microservices. How do the spans emitted by service six come to be associated with the trace begun at service one?

- A) The tracing backend correlates them by comparing timestamps after ingestion
- B) Each service includes a trace ID and span ID in the context passed to the next, which uses those values to create a span belonging to the same trace
- C) Each service queries a central trace registry for the active trace
- D) The service mesh control plane assigns trace IDs from a shared pool

---

**Q14.** *[retrieval: ch6]* A logging agent must run on every node, including nodes added after deployment. Which workload resource is correct?

- A) A Deployment with `replicas` equal to the current node count
- B) A StatefulSet with one ordinal per node
- C) A DaemonSet
- D) A CronJob that reconciles node coverage every five minutes

---

**Q15.** Which correctly describes the relationship between Fluentd and Fluent Bit?

- A) Fluent Bit is a fork of Fluentd maintained by a different foundation
- B) Fluent Bit is a lightweight telemetry agent and a sub-project of Fluentd, created for constrained environments; both are commonly deployed as node-level agents
- C) Fluentd is the lightweight agent; Fluent Bit is the full-featured aggregator
- D) They are unrelated projects that happen to share a name prefix

---

**Q16.** A team commits: "99.95% of search requests will return in under 200ms, measured monthly." No penalty is attached. This statement is:

- A) An SLA, because it is a public commitment
- B) An SLI, because it describes a measurement
- C) An SLO — a target value on an SLI, with no explicit consequence attached
- D) An error budget

---

**Q17.** Which are the four golden signals of monitoring?

- A) Rate, errors, duration, saturation
- B) Latency, traffic, errors, saturation
- C) Utilization, saturation, errors, latency
- D) Traces, metrics, logs, baggage

---

### Answers and Explanations

**Q1 — B.**
- **A** is wrong: both are postures toward a system, not licensing models. Prometheus (open source) supports both; commercial vendors sell both.
- **B** is correct. "Monitoring is called a system that can detect known unknowns — as opposed to observability which emphasizes being able to find and reason about unknown unknowns as well" [source: cncf-tag-observability-whitepaper-2026-08-31].
- **C** is wrong: the split is not by layer. You can monitor an application and observe infrastructure.
- **D** is wrong and inverts things if anything — monitoring is defined by "displaying **real-time** quantitative data" [source: sre-book-monitoring-definitions-2026-08-31], and observability is not restricted to historical questions.

**Q2 — C.** "An application is properly instrumented when developers don't need to add more instrumentation to troubleshoot an issue, because they have all of the information they need" [source: opentelemetry-observability-primer-2026-08-23].
- **A** is wrong: the golden signals are a monitoring prioritization heuristic, not an instrumentation completeness bar.
- **B** is wrong: a backend stores telemetry; it does not produce it. Instrumentation is upstream of any backend.
- **D** is tempting because it names the right four things, but emitting all four signals thinly still fails the test. The bar is *sufficiency for troubleshooting*, not signal-type coverage.

**Q3 — B.** OpenTelemetry currently supports traces, metrics, logs, and baggage [source: opentelemetry-signals-2026-08-23].
- **A** is the three-signal answer the majority of candidates give. It is the OTel primer's *passing* list, not the Signals page's list.
- **C** is the CNCF TAG Observability whitepaper's five-signal enumeration — metrics, logs, traces, profiles and dumps [source: cncf-tag-observability-whitepaper-2026-08-31]. Genuine, and a genuinely different taxonomy from a different document. The question asks what **OpenTelemetry** supports.
- **D** is wrong: alerts are an output of a monitoring system acting on metrics, not a signal type.

**Q4 — B.** Baggage is "contextual information that is passed between signals" [source: opentelemetry-signals-2026-08-23] — a key-value store letting you "propagate any data you like alongside context" [source: opentelemetry-baggage-2026-08-31].
- **A** is precisely the misconception the OTel docs pre-empt: "baggage is a separate key-value store and is unassociated with attributes on spans, metrics, or logs without explicitly adding them" [source: opentelemetry-baggage-2026-08-31]. Adding baggage to a span is a deliberate act.
- **C** is wrong: buffering is a Collector implementation concern, not what baggage is.
- **D** is wrong: baggage propagates across service boundaries and is independent of any one log record.

**Q5 — C.** "The controller calculates the utilization value as a percentage of the equivalent resource request on the containers in each Pod" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].
- **A** is wrong: node capacity is not the denominator for Pod utilization.
- **B** is the most common wrong answer, because limits are the more memorable number. Requests are what the Pod asked for, and requests are the denominator.
- **D** is wrong: a ResourceQuota caps namespace-wide consumption *[cross-bearing: see Ch 8 §3 — dividing a shared cluster]*; it is not an input to per-Pod utilization.

**Q6 — C.** "If some of the Pod's containers do not have the relevant resource request set, CPU utilization for the Pod will not be defined and the autoscaler will not take any action for that metric" [source: k8s-docs-hpa-utilization-vs-requests-2026-08-31].
- **A** is wrong: limits are never the denominator.
- **B** is wrong: node allocatable is not the denominator either.
- **D** is wrong: a Pod with limits and no requests is admitted normally. (A LimitRange *may* default a request at admission, which is a separate mechanism operating before the Pod exists — not the HPA improvising a denominator.)

**Q7 — B.** The question needs two things metrics-server does not provide: **history** and a **non-resource metric** (error counts). *[cross-bearing: see Ch 13 §7 — numbers nobody collects by default]*
- **A** is wrong: no such flag exists, and `kubectl top` reports current readings by design.
- **C** is wrong and is the trap for someone who thinks retention is a tuning knob. metrics-server is scoped to current resource readings for autoscaling; historical retention is not a setting it withholds.
- **D** is wrong: metrics-server registers with the aggregation layer to serve `metrics.k8s.io`; that is how it is reached, not a history feature.

**Q8 — B.** "Time series collection happens via a pull model over HTTP" [source: prometheus-overview-2026-08-23], with targets found by service discovery or static configuration.
- **A** is the single most common Prometheus misconception. Applications expose; Prometheus fetches.
- **C** is wrong: no shared-volume mechanism exists.
- **D** is wrong: the CRI is the kubelet↔runtime boundary *[cross-bearing: see Ch 2 §4 — the container runtime interface]* and has nothing to do with Prometheus.

**Q9 — B.** "The only valid use case for the Pushgateway is for capturing the outcome of a service-level batch job," where service-level means "not semantically related to a specific machine or job instance" [source: prometheus-pushgateway-practices-2026-08-31]. A nightly maintenance job is exactly this: too short-lived to be scraped, and not tied to one instance.
- **A** is wrong: a long-running web API *can* be scraped, which disqualifies it. Preference is not a criterion.
- **C** is wrong: the Pushgateway "persists the most recent push" [source: prometheus-glossary-2026-08-31]; it is not a delivery-guarantee mechanism.
- **D** is wrong: network topology is a routing problem, not a Pushgateway use case. Its documentation recommends it only "in certain limited cases" [source: prometheus-pushgateway-practices-2026-08-31].

**Q10 — C.** "If you need 100% accuracy, such as for per-request billing, Prometheus is not a good choice as the collected data will likely not be detailed and complete enough" [source: prometheus-overview-2026-08-23] — the documentation's own example.
- **A** is the answer given by someone matching on "counting requests" and missing "exact."
- **B** is a fabricated flag.
- **D** is wrong twice: the Pushgateway is for batch-job outcomes, not per-request events, and routing events through it would not make sampling exact.

**Q11 — B.** "No reliance on distributed storage — single server nodes are autonomous" [source: prometheus-overview-2026-08-23], and "each Prometheus server is standalone, not depending on network storage or other remote services, so you can rely on it when other parts of your infrastructure are broken" [source: prometheus-overview-2026-08-23]. Independence is a deliberate reliability choice.
- **A** inverts the design.
- **C** is wrong: Prometheus stores scraped samples locally and has nothing to do with etcd *[cross-bearing: see Ch 3 §2 — the control plane]*.
- **D** is wrong: the API server stores API objects, not time series, and using it as a metrics store would be catastrophic for the control plane.

**Q12 — B.** "A trace is made of one or more spans. The first span represents the root span; each root span represents a request from start to finish" [source: opentelemetry-observability-primer-2026-08-23].
- **A** inverts the containment, which is exactly the confusion the question tests.
- **C** is wrong: they name different things — one unit of work versus the whole path.
- **D** is wrong on "exactly one per service." A single service commonly emits several spans for one request (the handler, a database call, a cache lookup), and "one or more" is the documented relationship.

**Q13 — B.** "Service A includes a trace ID and a span ID as part of the context. Service B uses these values to create a new span that belongs to the same trace" [source: opentelemetry-context-propagation-2026-08-31]. This is context propagation, which "allows traces to build causal information about a system across services that are arbitrarily distributed across process and network boundaries" [source: opentelemetry-context-propagation-2026-08-31].
- **A** is the *pre-tracing* approach and its failure is why tracing exists. Timestamp correlation across six independently clocked services under concurrent load is unreliable at best.
- **C** is wrong: there is no central registry; the correlation rides in-band with the request.
- **D** is wrong: a mesh may *inject* headers, but the mechanism is still in-band propagation of a trace ID with the request, not central assignment from a pool.

**Q14 — C.** A DaemonSet's contract is one Pod per node, maintained as nodes join and leave. *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]* This is the canonical DaemonSet use case, and node-level log collection is the canonical example of it.
- **A** is wrong on two counts: the scheduler does not guarantee one Pod per node, and the replica count goes stale the moment the cluster scales.
- **B** is wrong: StatefulSets provide stable ordinal identity *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*, not per-node placement.
- **D** is wrong: a CronJob runs work that ends. Log collection is continuous, and reconciling coverage on a timer reinvents, badly, what a controller already does.

**Q15 — B.** Fluent Bit is "an open source telemetry agent," created in 2014 "as a lightweight log processor, developed by the Fluentd team at Treasure Data for constrained environments such as embedded Linux"; it is "a sub-project of Fluentd," and both "are commonly deployed on Kubernetes as node-level logging agents (DaemonSets)" [source: fluent-bit-overview-2026-08-23].
- **A** is wrong: sub-project, not fork, and both sit under the CNCF.
- **C** inverts them. Fluentd is the parent and heavier — "30-40MB of memory" for a vanilla instance [source: fluentd-architecture-2026-08-31].
- **D** is wrong: the shared prefix reflects a real parent-child relationship.

**Q16 — C.** A target value on a measurement, with no consequence attached. Apply the test: "ask 'what happens if the SLOs aren't met?': if there is no explicit consequence, then you are almost certainly looking at an SLO" [source: sre-book-service-level-objectives-2026-08-31].
- **A** is wrong: an SLA is a contract "that includes consequences of meeting (or missing) the SLOs they contain" [source: sre-book-service-level-objectives-2026-08-31]. Publicity is not what makes an SLA; consequences are.
- **B** is wrong but close, and worth being precise about. The **SLI** is the underlying measurement — the proportion of search requests returning under 200ms. The statement quoted adds a *target* (99.95%) and a *window* (monthly), which is what makes it an objective.
- **D** is wrong: the error budget would be the 0.05% of allowed failure derived *from* this objective [source: sre-book-error-budgets-2026-08-31], not the statement itself.

**Q17 — B.** "The four golden signals of monitoring are latency, traffic, errors, and saturation" [source: sre-book-four-golden-signals-2026-08-23].
- **A** mixes RED's rate/errors/duration [source: red-method-tom-wilkie-2026-08-31] with the golden signals' saturation. Plausible, and wrong.
- **C** is the USE method's three terms — utilization, saturation, errors [source: use-method-brendan-gregg-2026-08-31] — with latency appended. USE is a *resource*-oriented methodology; the golden signals are a user-facing-service list.
- **D** names the four OpenTelemetry signals [source: opentelemetry-signals-2026-08-23], which are signal *types*, not monitoring priorities. Two different fours, and the exam will happily offer you the wrong one.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **Observability** | Asking questions you did not plan for — unknown unknowns. A property of the system, not a product |
| **Monitoring** | Collecting and displaying real-time data about indicators chosen in advance — known unknowns |
| **Instrumentation** | The precondition. Properly instrumented = you don't need to add more instrumentation to troubleshoot |
| **Probes ≠ observability** | A yes/no signal to the kubelet, acted on and discarded. No history, no trend, no query |
| **The four signals** | Traces, metrics, logs, **baggage**. Four, not three |
| **Baggage** | A separate key-value store propagated between services. Not a span attribute unless you make it one |
| **OTel Collector** | Receives, processes, exports. One input, swappable backends |
| **Time series** | Timestamped values sharing a metric name and label set. Change any label value, get a new series |
| **Utilization's denominator** | The container's **resource request**. No request, no defined utilization |
| **metrics-server vs monitoring** | Current resource readings for autoscaling vs history, arbitrary metrics, alerting, and queries over time |
| **Prometheus** | **Pulls.** Scrapes HTTP endpoints found via service discovery. CNCF's second project, 2016 |
| **Pushgateway** | The only push path, and only for service-level batch jobs too short to scrape |
| **Prometheus non-fit** | Not for 100% accuracy — per-request billing is the documentation's own counter-example |
| **Span vs trace** | A span is one unit of work. A trace is the whole path: one or more spans, starting at the root span |
| **Context propagation** | Service A passes trace ID + span ID; service B creates a span in the same trace |
| **Jaeger** | The tracing backend. OTel instruments and exports; Jaeger receives and visualizes |
| **`kubectl logs`** | Not an archive. Rotation, one-restart depth, and eviction all bound it |
| **Logging architectures** | Node-level agent (DaemonSet — the default), sidecar, or app pushes directly |
| **Fluentd / Fluent Bit** | Fluentd is CNCF; Fluent Bit is its lightweight sub-project. One word, two words |
| **Reliability** | "Is the service doing what users expect it to be doing?" |
| **SLI / SLO / SLA** | Measurement / objective / contract-with-consequences. "What happens if it's missed?" |
| **Four golden signals** | Latency, traffic, errors, saturation. Latency rising is a leading indicator of saturation |
| **RED vs USE** | RED is service-oriented; USE is resource-oriented |

---

## 🏆 Safe Harbor

Domain 4 is complete, and so is every content chapter in this book.

You started at Chapter 1 with a curriculum that had moved under everyone's feet, and you have now covered all four domains: Kubernetes Fundamentals, Container Orchestration, Cloud Native Application Delivery, and Cloud Native Architecture. Twenty-two thousand words ago in this chapter you could name three signals; now you can name four and say why the fourth is the one that makes the other three cohere.

That is the last new thing this book has to teach you. Everything from here is consolidation.

---

## The Voyage Ahead

Chapter 19 does not add material. It re-sees what you already have.

You have learned this book domain by domain, because that is how the exam is structured and because knowledge has to enter in some order. But that is not how it will be *tested*. A question does not announce which chapter it came from. It describes a situation and asks what is true, and answering it well means holding several chapters at once — the control loop from Chapter 3 and the operator pattern from Chapter 6 and the GitOps agent from Chapter 15 turn out to be one idea seen three times, and a question can approach it from any of them.

So the next chapter runs the book the other way. Nine cross-cutting themes traced through twenty chapters. The confusion pairs that cost points, each with a question that discriminates between them. Ninety minutes of pacing, and what to do with a question you do not immediately know. A map of where the weight actually is, checked against your own Soundings and Bearings history rather than against a generic study plan. How to use The Lodestar in the last hour before you sit down. And a dated plan for the final week.

You have the instruments. Chapter 19 is where you take your bearings before making landfall.

> *"The instruments do not tell you where you are. They tell you what you can find out."*
> — Lodestar Ledgers
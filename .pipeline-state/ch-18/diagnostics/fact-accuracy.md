# Fact-Accuracy Audit — Chapter 18

**Mode detected: STANDARD.** The draft carries 173 inline `[source:]` tags across 137 lines, and the cached-source section is populated (26 snapshots). Untagged factual claims are therefore FAIL.

Line numbers cite `draft-v1.md` (1,435 lines), per the pipeline note — `draft-v2.md` does not exist at this stage.

> **⚠ READ THIS BEFORE ACTING ON ANY FIX BELOW.** The source bundle handed to this stage contains only the 26 snapshots "referenced by this chapter's pipeline-state files." A direct read of `../Book-KCNA/sources/` shows the corpus **also holds four snapshots that answer most of this chapter's untagged claims**:
>
> | Snapshot present in `sources/` but absent from this stage's bundle | What it closes |
> |---|---|
> | `jaeger-overview-2026-08-23.md` | The entire §5 Jaeger paragraph — **the draft's AUTHOR-REVIEW comment claiming "no cached snapshot for Jaeger" is factually wrong** |
> | `k8s-docs-logging-architecture-2026-08-23.md` | Every untagged claim in §6 — rotation defaults, restart depth, eviction, the three architectures |
> | `k8s-docs-logging-architecture-2026-08-31.md` | Same page, thinner body (25 lines); the 08-23 capture is the fuller one despite the `supersedes_note` |
> | `grafana-introduction-2026-08-23.md` | Grafana's identity — though **not** the non-CNCF claim (see FAIL-U3) |
>
> Consequence: most FAILs below are fixed by **adding a tag**, not by opening a research gap. Two are not.

---

## Summary

- Total factual claims inspected: **191**
- Tagged claims verified: **168**
- Tagged claims unverifiable (tag points to a missing/empty snapshot): **0** — all 25 distinct snapshot names cited resolve to snapshots present in the bundle. (`opencost-overview-2026-08-23` is bundled but never cited, consistent with the outline's decision to omit OpenCost.)
- **Untagged factual claims (FAIL): 21**, grouped into 5 findings
- **Contradicted claims (FAIL): 1**
- Minor discrepancies (WARN): **12**

---

## FAIL — Untagged factual claims

### FAIL-U1 · Line 400–405, 434, 1198–1202, 1337: the "limits set, no requests" scenario — **highest priority, two graded items depend on it**

**The claim.** Line 400 (Bearings 1, Q4): *"A Pod's containers declare `limits: cpu: 1000m` but declare no `requests` at all… What does the HPA do?"* — keyed to **C) Takes no action on that metric, because CPU utilization is undefined**. Line 1198 (Practice Q6) repeats the scenario with 60% target and the same key. Line 434 defends it: *"Kubernetes does not silently substitute the limit as a request for this calculation. The utilization is undefined, full stop."*

**Why it's a factual claim:** it asserts Kubernetes admission and HPA behaviour for a specific resource-spec shape, and it is the answer key for two graded items.

**Why it fails.** The tagged snapshot licenses only a narrower claim. `k8s-docs-hpa-utilization-vs-requests-2026-08-31` says:

> "if some of the Pod's containers do not have the relevant resource request set, CPU utilization for the Pod will not be defined and the autoscaler will not take any action for that metric"

That is conditioned on **the request not being set**. Whether "limits set, requests omitted" *results in* an unset request is a separate question, and **nothing in the corpus answers it.** I checked: `k8s-docs-resource-management-2026-08-23.md` is the snapshot of the exact page that governs this (`manage-resources-containers/`), and its capture covers requests/limits semantics, throttling, OOM kill, resource types and units — but **does not capture the request-defaulting paragraph.** Line 434's sentence is therefore an *unsourced negative* filling that hole.

It is very likely the wrong way round. Kubernetes' documented behaviour on that page is that when a limit is specified and no request is, the limit is copied and used as the requested value — in which case the request *is* set, utilization *is* defined, and the keyed answer C is wrong for both items (A becomes correct). I cannot confirm this from the corpus, which is precisely the problem: **the draft resolved an uncached question by assertion, in graded text.**

**Fix — two options, in order of preference:**

1. **Re-fetch and re-capture** `https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/`, specifically the "Resource requests and limits of Pod and container" section, into `k8s-docs-resource-management-2026-08-31.md`. Then re-key both items against what it actually says. Open this as manifest gap **G-18d (BLOCKING for §3's graded items)**.
2. **Interim fix that needs no fetch:** change both scenarios to declare **neither requests nor limits**, which matches the cached sentence exactly. Q4 line 400 → *"A Pod's containers declare no CPU `requests` and no `limits` at all."* Q6 line 1198 → *"A Deployment's Pod template sets no CPU requests."* Then delete line 434's second sentence ("Kubernetes does not silently substitute…") and drop Q4 option D and Q6 option A, which only exist to bait the limit-as-denominator confusion the changed scenario no longer raises.

Line 1337's parenthetical — *"A LimitRange may default a request at admission"* — is correct and separately sourceable to `k8s-docs-limit-range-2026-08-24` ("the LimitRange admission controller applies default request and limit values for all Pods (and their containers) that do not set compute resource requirements"). Tag it.

---

### FAIL-U2 · Lines 76, 78, 772, 780, 782, 784, 794, 842, 844, 846, 1010, 1016, 1099, 1142: the whole of §6 is untagged — and all of it is already cached

**Why they're factual claims:** kubelet configuration defaults with specific values, retention depth, eviction behaviour, and a taxonomy explicitly attributed to "the Kubernetes documentation" (line 794).

Eleven distinct assertions carry no tag. Every one is supported verbatim by `k8s-docs-logging-architecture-2026-08-23.md`, which is in `sources/` but was not passed to this stage:

| Line | Draft says | Snapshot says |
|---|---|---|
| 772 | "Kubernetes provides no native storage for log data." | "Kubernetes does not provide a native storage solution for log data." |
| 772 | "Container logs are written to the node's filesystem by the container runtime; the kubelet manages them there" | "The container runtime handles and redirects any output generated to a containerized application's stdout and stderr streams; the kubelet manages the logs using the CRI logging format." |
| 780, 1010 | "`containerLogMaxSize` of 10Mi and `containerLogMaxFiles` of 5"; "only the contents of the latest log file are available through `kubectl logs`" | "configured via containerLogMaxSize (default 10Mi) and containerLogMaxFiles (default 5)"; "only the latest log file's contents are available" |
| 782 | "The kubelet keeps the logs of one terminated container so that `kubectl logs --previous` can reach one restart back." | "By default, if a container restarts, the kubelet keeps one terminated container with its logs"; "`kubectl logs --previous` retrieves logs from a previous instantiation of a container" |
| 784 | "When a Pod is evicted, its containers are evicted with their logs." | "If a pod is evicted from the node, all corresponding containers are also evicted, along with their logs." |
| 794, 842, 844, 846, 1016 | The three architectures | "Use a node-level logging agent that runs on every node (typically a DaemonSet)…"; "Include a dedicated sidecar container for logging in an application pod…"; "Push logs directly to a backend from within an application." |
| 76 | "container logs are written to the node's filesystem, by the container runtime" | as above |

**Fix:** add `[source: k8s-docs-logging-architecture-2026-08-23]` at lines 76, 772, 780, 782, 784, 794, 842, 844, 846, 1010, 1016, and to the `kubectl logs` row of the Exam Alert trap table (line 1142). No research gap needed. Also register this snapshot in the chapter's research-manifest so it ships in the next stage's bundle. See WARN-6 and WARN-7 for two defects inside this block that a tag alone will not fix.

---

### FAIL-U3 · Lines 522, 557, 1142: "Grafana is not a CNCF project" — an unsourceable negative the research stage explicitly forbade

**The claim.** Line 557: *"**Grafana is not a CNCF project.** … It is an open-source product from Grafana Labs. Related products from the same company (Loki for logs, Tempo for traces) are likewise outside CNCF and outside this exam's scope."* Repeated in the §4 figure at line 522 (`(NOT CNCF)`) and in the Exam Alert trap table at line 1142: *"It is not. Neither are Loki or Tempo. Prometheus, OpenTelemetry, Jaeger and Fluentd are."*

**Why it's a factual claim:** it asserts (and denies) foundation membership for three named projects, in a table the reader will study as exam guidance.

**Why it fails.** This chapter's own research manifest raised it as gap **G-18b** and told the drafting stage not to write it:

> "**G-18b · 'Grafana is not a CNCF project' is a negative and cannot be safely sourced.** Nothing in the corpus or on grafana.com asserts non-membership; proving it would mean citing a dated CNCF project roster, which trap #99 and B3 both forbid grading on."

And Note #4 gave the replacement framing verbatim: *"Assert the positive, not the negative… Say the first clause, note that the CNCF projects in the paragraph are the ones the snapshots name as such, and let the reader draw it."* The draft asserted the negative anyway, three times, and extended it to Loki and Tempo — which manifest Open Question #5 records as having **no ledger owner and no source at all**.

The cached `grafana-introduction-2026-08-23.md` supports only: *"Grafana is open source software that enables you to query, visualize, alert on, and explore your metrics, logs, and traces wherever they're stored,"* from Grafana Labs' own docs. It says nothing about CNCF.

**Fix:** rewrite line 557 to the manifest's prescribed shape, e.g.: *"Grafana is Grafana Labs' own open-source software — 'open source software that enables you to query, visualize, alert on, and explore your metrics, logs, and traces wherever they're stored' [source: grafana-introduction-2026-08-23]. Every other project named in this section has a CNCF donation the sources state directly: Prometheus joined in 2016 [source: prometheus-overview-2026-08-23], Fluentd in November 2016 [source: fluentd-architecture-2026-08-31], Jaeger on donation by Uber [source: jaeger-overview-2026-08-23]. Grafana's docs make no such claim."* Delete `(NOT CNCF)` from the figure at line 522. Delete the Loki/Tempo sentence entirely, or reduce it to one non-graded clause naming them as Grafana Labs products. **Remove row 11 from the Exam Alert trap table (line 1142)** — a roster claim must not be graded surface.

---

### FAIL-U4 · Line 673 (+ the AUTHOR-REVIEW comment at 675): the Jaeger paragraph is untagged on a false premise

**The claim.** *"**Jaeger** is a distributed tracing backend: it receives, processes, aggregates and visualizes trace data. It was originally built for OpenTracing and is now OpenTelemetry-compatible, with concepts mapping directly across the two."*

**Why it's a factual claim:** project function, standards lineage, and compatibility assertion about a third-party CNCF project.

**Why it fails.** Untagged — and the AUTHOR-REVIEW comment at line 675 justifies that with *"no cached snapshot for Jaeger — the corpus has no jaegertracing.io capture."* **That is incorrect.** `sources/jaeger-overview-2026-08-23.md` exists, captures `https://www.jaegertracing.io/docs/latest/`, and supports every clause:

> "the Jaeger project is primarily the tracing backend that receives tracing telemetry data and provides processing, aggregation, data mining, and visualizations… Jaeger was originally designed to support the OpenTracing standard… Jaeger is OpenTelemetry compatible; terminology and concepts map directly between the two data models."

**Fix:** append `[source: jaeger-overview-2026-08-23]` to line 673 and **delete the AUTHOR-REVIEW comment at line 675** — it will otherwise send a later stage chasing a fetch that is already in the corpus. Tag the Chapter Summary row at line 1415 the same way. Two cautions when tagging: (a) the snapshot also says Jaeger is "a graduated project," which **trap #99 forbids grading on** — keep that out of the trap table and the practice items, where it currently does not appear; (b) the snapshot's "released as open source by Uber Technologies in 2016" is available if §5 wants provenance, but the outline gives Jaeger no such surface.

---

### FAIL-U5 · Untagged Kubernetes claims carried by cross-bearing (7 claims)

These assert Kubernetes behaviour with no tag, relying on a `[cross-bearing: …]` pointer to a shipped chapter to carry the sourcing:

| Line | Claim | Pointer |
|---|---|---|
| ~64–66 | A liveness probe restart surfaces as a container-state reason, a restart count, and an Event that expires; the probe result is not stored | Ch 5 §7 |
| ~218–226 | Liveness restarts the container; readiness removes the Pod from endpoints; neither produces a record | Ch 5 §7 |
| 68 | metrics-server holds current readings only, CPU/memory only | Ch 13 §7 |
| 76, 842, 1043 | A DaemonSet places exactly one Pod per node and covers nodes added later | Ch 6 §7 |
| ~1046 | A Deployment's replicas are placed by the scheduler with no per-node guarantee | Ch 7 §1 |
| ~1310 | "the CRI is the kubelet↔runtime boundary" | Ch 2 §4 |
| ~1391 | StatefulSets provide stable ordinal identity, not per-node placement | Ch 6 §6 |

**Why they're factual claims:** all are assertions about Kubernetes behaviour, several inside graded answer keys.

**Fix:** this is a convention question the revision stage should settle once rather than per-line. If the book's rule is that a cross-bearing to an audited chapter discharges the tagging obligation, these are all fine and this finding closes — but say so in the chapter's diagnostics so the next audit does not re-raise it. If not, tag them: the DaemonSet claims resolve to `k8s-docs-logging-architecture-2026-08-23` ("a node-level logging agent that runs on every node (typically a DaemonSet)"); the CRI and probe claims will need their Ch 2 / Ch 5 snapshots pulled forward into this chapter's bundle. **No new research is required for any of them.**

---

## FAIL — Contradicted claims

### Line 106: the Dead Reckoning definition of observability is tagged to the wrong snapshot

**Tag:** `[source: cncf-glossary-observability-2026-08-31]`

**Draft says:** "Observability is a property of a system: the degree to which you can understand its **internal state** from its **external outputs**."

**Snapshot says (the whole of its definition section):**
> "Observability is a system property that defines the degree to which the system can generate **actionable insights**. It allows users to understand a system's state from these external outputs and take (corrective) action."

The glossary entry says *"a system's state,"* never *"internal state,"* and its load-bearing noun is *actionable insights*, which the draft drops. The "internal states… inferred from… external outputs" formulation is **a different cached snapshot's wording** — `cncf-tag-observability-whitepaper-2026-08-31`:

> "observability is a measure of how well internal states of a system can be inferred from knowledge of its external outputs."

So the sentence is a blend of two sources under one tag, and the tag names the source it matches less well. The chapter's own research manifest (Note #6) flagged this exact hazard, recording all three cached definitions and recommending **§1 stay on the OTel primer's wording** because §7 and §8 pay that wording off.

**Recommended fix:** either (a) re-tag to the whitepaper, whose wording the draft actually used — `…understand its internal state from its external outputs [source: cncf-tag-observability-whitepaper-2026-08-31]`; or (b) preferred, follow manifest Note #6 and restate on the primer: *"Observability lets you understand a system from the outside, by letting you ask questions about it without knowing its inner workings [source: opentelemetry-observability-primer-2026-08-23] — a property of the system rather than a tool you install [source: cncf-glossary-observability-2026-08-31]."* Option (b) keeps the glossary tag doing the one job its own drafting guardrail assigns it ("the 'property of the system, not a tool' beat") and preserves the §8 payoff.

---

## WARN — Minor discrepancies

**WARN-1 · Lines 204, 420 — a word inserted into a bolded standard.** Both render the instrumentation bar as *"because they **already** have all of the information they need."* The snapshot reads *"because they have all of the information they need"* (`opentelemetry-observability-primer-2026-08-23`). Neither line uses quotation marks, so this is not a misquote — but line 204 is a ★ Fixed Point and line 420 is an answer key, both of which readers memorise verbatim, and the Practice Q2 explanation at ~1288 quotes it correctly *without* "already." Drop the word in all three for consistency.

**WARN-2 · Line 234 — "OpenTelemetry — the CNCF project that defines the vendor-neutral standard for telemetry data."** Untagged, and over-broad. No snapshot body asserts OTel's CNCF membership; it appears only in research-stage frontmatter `authority:` fields, which the corpus header rules out as quotable source text. "Vendor-agnostic" is verbatim in `opentelemetry-collector-2026-08-31` but scoped to *the Collector*, not to OTel as a whole. Narrow to what is sourced, or cite the Collector snapshot for the vendor-agnostic clause only.

**WARN-3 · Line 234, line ~250 (★ Fixed Point), chapter subtitle (line 2), Exam Alert #1 — "four signals" is not attributed to the page that says four.** `cncf-tag-observability-whitepaper-2026-08-31` carries an explicit drafting instruction:

> "Ch 18 §2's Fixed Point 'four signals, not three' is a claim about **OpenTelemetry's Signals page specifically** and must be attributed that way. Do not write 'the four signals' as though it were a universal or CNCF-wide taxonomy."

The draft handles this **well** in Practice Q3's explanations — it names the primer's three-item passing list and the whitepaper's five-item enumeration, and asks specifically what *OpenTelemetry* supports. §2's body does not: line 234 and the Fixed Point both attribute to "OpenTelemetry" generally, on a page where OTel's own primer says three. Fix: *"OpenTelemetry's Signals page lists four…"* and *"**OpenTelemetry's Signals page defines FOUR signals**…"* Not strictly wrong; one clause from being airtight.

**WARN-4 · Line 537 — "Prometheus **ships** special-purpose exporters for things like HAProxy, StatsD, and Graphite."** The snapshot lists these under Components as *"special-purpose exporters for services like HAProxy, StatsD, Graphite, etc."* — an ecosystem inventory, not a statement that the project distributes them. Soften to "Special-purpose exporters exist for services like…".

**WARN-5 · Line 555 — "Grafana is the visualization tool **most commonly paired** with Prometheus."** The snapshot says only *"Grafana or other API consumers can be used to visualize the collected data."* The superlative is unsourced. Drop "most commonly" or attribute it as the book's observation.

**WARN-6 · Line 1099 contradicts line 772 on who writes container logs.** §8: *"The **kubelet** writes container logs to the node."* §6 line 772: *"Container logs are written to the node's filesystem by the **container runtime**; the kubelet manages them there."* The snapshot backs §6: *"The container runtime handles and redirects any output… the kubelet manages the logs using the CRI logging format."* Fix line 1099 to "the runtime writes container logs to the node; an agent ships them somewhere else" — the §8 sentence is making a producer/consumer point that works either way.

**WARN-7 · Line 78 — `kubectl --previous` is not a command.** Soundings answer 6 reads *"`kubectl --previous` reaches one termination back."* The flag belongs to `kubectl logs`; the snapshot has *"`kubectl logs --previous` retrieves logs from a previous instantiation of a container."* §6 line 782 and Bearings answer line 1012 both get it right, so this is an isolated slip in the first thing the reader encounters. Fix to `kubectl logs --previous`.

**WARN-8 · Line 34 — the arithmetic in the 15-minute triage does not hold.** *"read §2 and §7… Those two sections carry **four** of this chapter's six high-priority exam topics between them."* The Exam Alert's six high-priority topics map to: (1) four signals → §2; (2) Prometheus pulls → §4; (3) span vs trace → §5; (4) SLI vs SLO → §7; (5) observability vs monitoring → §1; (6) metrics-server boundary → §3. §2 and §7 carry **two**, not four. Either fix the count to two, or change the recommended sections to §2 and §4 (topics 1, 2 — still two). This is checkable by any reader who reaches the Exam Alert.

**WARN-9 · Line 84 — "§4 and §7… carry **six** of this chapter's ten sourced traps."** The "ten sourced" figure checks out precisely: the Exam Alert table has 12 rows, of which 10 carry source tags (rows 11 and 12 do not) — nice work. But §4 owns 4 tagged trap rows (Prometheus pushes, per-request billing, clustered storage, first-vs-second project) and §7 owns 1 (SLI/SLO swapped) = **five**. The sixth is only reachable by counting the untagged Grafana row, which FAIL-U3 recommends deleting. Change to "five of this chapter's ten sourced traps."

**WARN-10 · Line 4 — untagged domain weight in the chapter header.** *"Domain Weight: 12% (Cloud Native Architecture) | Competency: Observability."* Correct per `lf-kcna-program-changes-2026-08-23` ("Cloud Native Architecture – 12%": … Observability …) and tagged properly at line ~112. Flagging only so the revision stage confirms that headers are exempt by convention; if they are not, tag it.

**WARN-11 · Line 844 — the sidecar architecture is glossed, not described.** Draft: *"Useful when an application writes to a file inside the container rather than to stdout, or needs per-application processing."* The snapshot describes two distinct sidecar shapes: *"either a streaming sidecar that writes logs to its own stdout/stderr, or a sidecar container with a logging agent configured to pick up logs from an application container."* The draft's gloss is a fair reading of the second shape and silently drops the first. Acceptable for KCNA surface (the outline gives sidecars one paragraph), but the sentence should not imply the file-on-disk case is the only motivation.

**WARN-12 · Lines ~110–112 — the retired-blueprint framing is an inference, correctly handled.** *"you were probably told that Observability is its own KCNA domain with its own weight."* The cached page states only that domains "remain mostly unchanged except that observability will be rolled under Cloud Native Architecture," and the snapshot explicitly records that **it does not display the previous domain structure or weights**; manifest gap **G-18a** (retired weights) is still open. The draft prints **no retired percentage**, which is exactly right. No change needed — logged so the next audit does not mistake the inference for a sourced figure, and so nobody "helpfully" adds the 8%.

---

## PASS — Verified claims (sampled for coverage evidence)

Checked verbatim against the named snapshot; all match.

**§1 (lines 106–228).** Monitoring definition (SRE ch. 6, exact through "about a system," correctly stopping where the snapshot's excerpt note requires) · all four "Why Monitor?" reasons · the known-unknowns/unknown-unknowns contrast (TAG whitepaper, verbatim; `--` normalised to an em dash) · the primer's "without knowing its inner workings" framing · "For a system to be observable, it must be instrumented" · code-based and zero-code definitions · the glossary's "system property" and operating-cost consequence · "data emitted from a system and its behavior."

**§2 (lines 234–308).** All four signal definitions, exactly as the Signals page words them · the general definition of a signal · five consecutive baggage quotes, including the load-bearing "unassociated with attributes on spans, metrics, or logs without explicitly adding them" and the security caution (correctly kept non-graded) · the logs caveat and "not necessarily associated with any particular user request" · four Collector quotes including the Unification objective. **Guardrail compliance confirmed:** §2 says the Collector "receives, processes and exports" and never presents receiver/processor/exporter as a named taxonomy, exactly as manifest gap G-18c requires.

**§3 (lines 316–390).** Time-series definition · label identity and "the change of any label's value… will create a new time series" · sample composition · both cardinality quotes with the unbounded-set examples · the HPA utilization-vs-request sentence · the no-request-set sentence (used, correctly, as the proof rather than the algorithm) · "needs to be launched separately." **Guardrail compliance:** the scaling algorithm is not drafted, per the snapshot's instruction; the ***an object without its component does nothing*** phrase is quoted from the ledger, not paraphrased from the K8s page.

**§4 (lines 470–580).** SoundCloud origin and 2012 inception · "pull model over HTTP" · service-discovery-or-static-configuration · target and endpoint definitions · all four Pushgateway quotes including "the only valid use case" · client library and exporter definitions · both Alertmanager quotes, with the arrow-reversal handled as the snapshot's drafting note asks · PromQL definition and the HTTP API sentence · standalone-server and 100%-accuracy quotes · "second hosted project, after Kubernetes." **Guardrail compliance:** no PromQL syntax appears; grouping/inhibition/silencing are named nowhere and graded nowhere.

**§5 (lines 590–700).** Context, propagation, and context-propagation definitions · "arbitrarily distributed across process and network boundaries" · the Service A / Service B sentence · W3C TraceContext named once and ungraded, as instructed · span and trace definitions with "one or more spans" and the root-span sentence · the zero-code quotes reused for the mesh bridge.

**§6 (lines 850–900).** Fluentd's JSON/unified-logging quote · "connects dozens of data sources and data outputs" · the plugin-system quote and "500+" · the 30–40MB footprint · all Fluent Bit quotes and the six-stage pipeline table. **Guardrail compliance, both traps honoured:** the broken-grammar CNCF-graduation sentence is stated in the book's voice and never quoted; and no graded item turns on a maturity level — the §6 Snag at line ~880 explicitly warns that the roster moves, and Practice Q15's key rests on the sub-project relationship, not on graduation status.

**§7 (lines 910–984).** The reliability question · SLI, SLO and SLA definitions from both the primer and SRE ch. 4, kept in the manifest-prescribed division of labour · the "what happens if the SLOs aren't met?" test · both error-budget quotes, with the uncaptured-antecedent sentence correctly left alone · all four golden signals with their qualifying clauses, including "a slow error is even worse than a fast error!" and the leading-indicator relationship · USE's three terms and purpose · RED's three terms and the USE/RED complementarity quote. **Guardrail compliance:** the utilization collision is addressed head-on in the 🔭 Closer Look rather than left to trip the reader; and **no Practice, Bearings or Soundings item depends on RED or USE** — Q17 keys to the golden signals and merely uses RED/USE terms as distractors, which does not require the candidate to know either method. The AUTHOR-REVIEW note at line 986 correctly records G21 as substantially-but-not-fully closed.

**Structural counts, all verified against the draft.** "Seventeen questions… four are interleaved" → Q1–Q17 with `[retrieval:]` on Q6, Q7, Q13, Q14 ✓ · Bearings 1 "two of them test material from earlier chapters" → Q4 (ch5), Q5 (ch10) ✓ · Bearings 2 "one draws on Chapter 17" → Q5 ✓ · Bearings 3 "one draws on Chapter 6" → Q5 ✓ · Soundings "eight questions" ✓ · error-budget arithmetic at line ~940 (99.9% → 0.1%) and in Q16 option D (99.95% → 0.05%) ✓.
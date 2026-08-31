Draft located at `.pipeline-state/ch-18/draft-v1.md`; all citations below are line-accurate against it.

```markdown
# Question-Quality Audit — Chapter 18

## Summary

- Chapter type: **content**
- Total questions inspected: **40**
  - 🧭 Soundings questions: **8** (L49–L63)
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints — L380, L701, L990)
  - Practice questions: **17** (L1153–L1305)
- Question budget compliance: **met** (all four categories exact)
- Weak distractors (WARN): **4**
- Trap answers that don't target real misconceptions (WARN): **2** (subset of the 4 above)
- Ambiguous items — distractor may be defensibly correct (FAIL): **1**
- Missing or incomplete why-wrong explanations (FAIL): **0**
- Duplicate / near-duplicate item pairs (WARN): **2**
- Mis-tagged retrieval items (WARN): **1**
- Checkpoints missing a low-score revision prompt (WARN): **3 of 3**
- Retrieval-practice spacing: **compliant**
- Soundings spoiler check: **clean** — 0 of 8 reveal a ★ Fixed Point

**Headline:** the answer-key architecture is the strongest in the commission to date — 20 of 20
multiple-choice items carry complete four-option why-wrong explanations, which is a clean sweep and
rare. Three problems are worth fixing before the gate: one item whose D option may be the true answer
(CP1 Q4), a **§4 component-vocabulary blind spot** where six introduced concepts including an
explicitly-flagged "worth carrying into the exam" discrimination go entirely untested, and two
duplicate pairs that spend budget the §4 gap needs. A single edit closes all three at once — see
**Priority fix** at the end.

## Question-budget compliance

Compare actual counts to `question_budget` in outline frontmatter:

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 15 | 15 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 (outline: 3) | 3 (5 + 5 + 5) | **met** |
| Practice Questions | 17 | 17 | **met** |
| **Chapter total** | **40** | **40** | **met** |

Practice-question distribution also matches the outline's §-level plan exactly: §1→2 (P1–P2),
§2→2 (P3–P4), §3→3 (P5–P7), §4→4 (P8–P11), §5→2 (P12–P13), §6→2 (P14–P15), §7→2 (P16–P17).
The outline's deviation from B4's table figure of 10 Bearings (justified in frontmatter, consistent
with shipped Ch 13 and Ch 17) is honoured in the draft rather than quietly reverted.

**Format-mix observation (WARN, checkpoint-level).** Only **3 of 15** Bearings questions are
multiple-choice (CP1 Q1 L384, CP1 Q4 L400, CP2 Q3 L709). Checkpoint 3 (L990) has **zero**. Eleven
are open-response. Free recall is a legitimate and arguably superior desirable difficulty, so this is
not a failure — but skill Part 11 and the Part 17 checklist both scope trap answers to *all*
self-assessment checkpoints, and an open-response item cannot carry a trap. The practical cost is
that §6 and §7 — the last material before the exam — get no misconception-detection at checkpoint
level at all, and the reader's first and only MC exposure to SLI/SLO and the golden signals is P16/P17.
**Recommend:** convert CP3 Q4 (L1000, golden signals) to four-option MC, reusing P17's distractor
logic in shortened form. That leaves ten open-response items, which is still a free-recall-dominant
checkpoint set.

## Soundings spoiler check

The draft carries **six** ★ Fixed Points, not the five the outline enumerated — §1 has two (L152
observability/monitoring; L202 properly-instrumented). All six checked against all eight Soundings
stems *and* all eight answer rationales:

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 (L49) | Probe leaves no record | **no** — nearest miss, correctly handled | Stem avoids "observability"/"monitoring"; answer (L68) stops at "not stored, trended, or queryable" and does **not** state the FP1 distinction. The outline's specific constraint on this question was met verbatim. |
| 2 (L51) | metrics-server scope | **no** | The metrics-server/monitoring boundary is taught as ⚠ Navigational Hazards (L370) and a summary row, not a ★ Fixed Point. Prerequisite material owned by Ch 13 §7. |
| 3 (L53) | `kubectl top` failure | **no** | Names *an object without its component does nothing* — a retrieved Ch 10 §3 pattern, not a Ch 18 Fixed Point. Verbatim casing correct. |
| 4 (L55) | Utilization denominator | **no** | Denominator is taught as a 🪢 Mnemonic (L358), not a Fixed Point. Owned by Ch 5 §8, so answering from prerequisites is the intended path. |
| 5 (L57) | Per-node log agent | **no** | §6's default-architecture ruling is ⚓ Worth Securing (L862), not a Fixed Point. DaemonSet is Ch 6 §7 material. |
| 6 (L59) | `kubectl logs` depth | **no** | Rotation/restart-depth is taught as ⚠ Navigational Hazards (L790), not a Fixed Point. |
| 7 (L61) | Five logs, no join | **no** — second nearest miss, correctly handled | Neither stem nor answer (L80) uses "span", "trace", or "root span". Answer says "no shared identifier", which describes the gap without naming FP5's vocabulary. Constraint met. |
| 8 (L63) | Mesh telemetry | **no** | Ch 17 §5 material; zero-code instrumentation is named in §1/§5 prose but is not a Fixed Point. |

**Result: clean.** Both questions the outline singled out as spoiler risks (Q1 → FP1, Q7 → FP5) were
drafted under the stated constraint and hold.

**Rubric check (rule 8): PASS.** The 6+ / 3–5 / 0–2 reading-strategy rubric is present at L84–L88,
and the 0–2 branch names Ch 13 §7 and Ch 17 §3 specifically as the load-bearing prerequisites — the
outline asked for exactly that and got it.

**Answer disclosure (rule 9): PASS.** Answers are inside `<details><summary>Answers + reading
strategy</summary>` opening at L65.

**Pre/post pairing (skill Part 11 rule 1) — one gap.** Seven of eight Soundings questions have a
post-test partner in a checkpoint: Q2→CP1 Q3, Q3→CP1 Q5, Q4→CP1 Q4, Q5→CP3 Q5, Q6→CP3 Q1, Q7→CP2 Q3,
Q8→CP2 Q5. **Soundings Q1 (probes) has no partner** — nothing in any checkpoint or practice question
re-tests the "health checking is not observability" exclusion. This is the same gap the coverage table
records below, seen from the pre-test side.

## Per-question findings

### CP1 Q4 (L400): "A Pod's containers declare `limits: cpu: 1000m` but declare no `requests` at all… What does the HPA do?"

**Issue:** **Option D may be defensibly correct**, which makes this an ambiguous item. Skill
Part 10B lists "ambiguous questions with multiple defensible answers" as *undesirable* difficulty —
the category the design explicitly excludes. This is the highest-severity finding in the chapter.

**Distractor analysis:**
- A) `70% of 1000m` — **strong.** Targets limit-as-denominator, the documented most-common error.
- B) `70% of node's 8 CPUs / Pod count` — **plausible.** Targets node-capacity-as-denominator.
- C) *(correct)* Utilization undefined, no action.
- D) "Defaults the request to the limit and scales on 70% of 1000m" — **ambiguity risk.** Kubernetes
  has a documented behaviour in which a container specifying a limit and no request has the request
  populated from the limit. If that behaviour applies here, D describes the real outcome and C does
  not, and the item has two defensible answers. Note the draft is *aware* of adjacent defaulting
  machinery — P6's explanation (L1337) volunteers the LimitRange caveat — but neither answer key
  addresses the limit→request path that option D actually names.

**Why-wrong explanation status:** present and specific for all four (L430–L434). D's rebuttal —
"Kubernetes does not silently substitute the limit as a request for this calculation" — is the exact
claim in dispute, so the explanation does not resolve the ambiguity; it asserts against it.

**Recommended fix:** two steps. (1) Refer the factual determination to the fact-accuracy audit —
that stage owns whether the limit→request default applies. (2) Regardless of that finding, **retire
this item** and reuse the slot (see Priority fix). The corollary it tests is already carried by
Practice Q6, which asks the same thing with a clean D option. Retiring CP1 Q4 removes the ambiguity
and the duplication in one edit.

---

### CP1 Q4 (L400) ↔ Practice Q6 (L1198): duplicate pair

**Issue:** near-identical items. Both: workload with CPU limits and no CPU requests, HPA targeting a
CPU utilization percentage, "what happens." Same correct answer, same three-of-four distractor logic
(limit-as-denominator, node-as-denominator, admission-time defaulting). Both tagged `[retrieval: ch5]`.

Combined with Soundings Q4 (L55) and Practice Q5 (L1189), the utilization denominator is examined
**four times** in one chapter. The outline justified emphasis here — two shipped chapters point at §3
for it — but emphasis was meant to be *depth*, and this is repetition of one question at one
difficulty. Meanwhile §4's component vocabulary is tested zero times.

**Recommended fix:** keep P5 (denominator) and P6 (undefined-case corollary, clean options); retire
CP1 Q4 per the finding above.

---

### CP3 Q5 (L1002) ↔ Practice Q14 (L1270): near-duplicate pair

**Issue:** same scenario (log agent must run on every node including future nodes), same answer
(DaemonSet), same rejection reasoning against a replica-counted Deployment. One is open-response, one
is MC. With Soundings Q5 (L57) this makes **three** passes at DaemonSet-for-log-collection.

**Severity:** lower than the pair above. Open-response → MC across a section boundary is a defensible
spaced-retrieval structure, and the format change does real work. No fix required if budget is tight.

**Recommended fix (optional):** re-point CP3 Q5 at the *sidecar* architecture — "an application
writes logs to a file inside the container rather than stdout; which of the three architectures, and
what does it cost you?" — which tests §6's second and third architectures, currently reached only via
CP3 Q2's enumeration.

---

### Practice Q13 (L1261): "A request crosses six microservices. How do the spans emitted by service six come to be associated with the trace begun at service one?"

**Issue:** **mis-tagged as `[retrieval: ch17]`.** Nothing from Chapter 17 is tested. The correct
answer and all three distractors are pure §5 material (context propagation, L594–L610). "Six
microservices" is scenery, not a retrieval target — a reader with no memory of Ch 17 answers this at
full marks.

The outline specified this slot as "Ch 17 §3 microservices × §5 tracing", a genuine two-chapter join.
The item as drafted delivers the §5 half only.

**Effect on the count:** practice-section retrieval drops from 4/17 (23.5%) to **3/17 (17.6%)** if
this tag is disallowed. Still inside the 10–25% band, so no threshold breach — the tag is inaccurate,
not budget-breaking.

**Recommended fix:** either drop the tag, or make the join real by adding a clause the Ch 17 reader
needs: *"…and the six services were decomposed from a monolith that previously answered this question
from a single stack trace. Which property of the decomposition made propagation necessary?"* The
cheaper fix is dropping the tag; CP2 Q5 (L718) already carries a genuine Ch 17 join.

---

### Practice Q10 (L1234): "A company needs an exact count of every API call for per-customer invoicing…"

**Issue:** option B is a **fabricated CLI flag** — `--storage.tsdb.exact-counting`. Its own answer key
(L1357) calls it "a fabricated flag." It targets no identifiable misconception: a candidate with
hands-on Prometheus exposure rejects it instantly, and one without it has no basis to evaluate it.
The item is effectively three options.

**Distractor analysis:**
- A) "Well suited; counters are the canonical use case" — **strong.** The word-matching trap.
- B) `--storage.tsdb.exact-counting` — **weak, fails trap fidelity.** Invented for symmetry.
- C) *(correct)* Explicitly a poor fit; billing is the docs' own example.
- D) "Suitable if the Pushgateway is used for every request" — **good.** Cross-links to the §4
  Pushgateway trap and is the answer of someone who half-fixed the problem.

**Why-wrong explanation status:** present and specific for all four.

**Recommended fix:** replace B with a real misconception — *"It is suitable if the scrape interval is
reduced to 1 second."* That targets the genuine belief that sampling frequency converges on
completeness, which is precisely what the pull model cannot deliver, and it makes the answer key
teach rather than dismiss.

---

### Practice Q8 (L1216): "How does the Prometheus server obtain metrics from an instrumented, long-running application?"

**Issue:** option C is filler.

**Distractor analysis:**
- A) "The application POSTs metrics to Prometheus on an interval" — **strong.** The single most
  common Prometheus misconception, and the answer key says so.
- B) *(correct)* Prometheus scrapes an HTTP endpoint on an interval.
- C) "The application writes to a shared volume Prometheus reads" — **weak, fails trap fidelity.**
  Nobody holds this belief in an identifiable form; the answer key can only say "no shared-volume
  mechanism exists," which teaches nothing.
- D) "The kubelet forwards metrics to Prometheus via the CRI" — **good.** Targets a real conflation of
  the resource metrics pipeline with Prometheus, and the rebuttal usefully re-anchors the CRI.

**Why-wrong explanation status:** present for all four; C's is thin by necessity.

**Recommended fix:** replace C with *"An exporter running beside the application pushes its metrics to
the Prometheus server."* That is a real and specific misconception — it correctly identifies the
exporter's existence and inverts its arrow — and it would give §4's otherwise-untested exporter
concept its only appearance in a graded item.

---

### Practice Q1 (L1153): "Which statement best captures the difference between monitoring and observability?"

**Issue:** option A is weak.

**Distractor analysis:**
- A) "Monitoring is open-source; observability requires commercial tooling" — **weak.** There *is* a
  real misconception nearby ("observability is what vendors sell you"), but rendered as a licensing
  claim it becomes internally implausible: no coherent belief holds that monitoring is definitionally
  open-source. The pairing is what breaks it, not the sentiment.
- B) *(correct)* Known unknowns vs unknown unknowns.
- C) "Monitoring covers infrastructure; observability covers applications" — **strong.** The infra-
  monitoring-vs-APM split is a widely held real misreading.
- D) "Monitoring is real-time; observability is historical" — **strong.**

**Why-wrong explanation status:** present and specific for all four.

**Recommended fix:** rewrite A to carry the real version of the belief: *"Observability is what you
get when you add distributed tracing to your monitoring stack."* That targets the tool-acquisition
misconception the §1 figure caption (L191) already pre-empts — "do not draw this as Prometheus vs
OpenTelemetry" — and makes the distractor and the figure reinforce each other.

---

### Practice Q7 (L1207): option A — borderline

**Issue:** "Nothing further; `kubectl top` with a timestamp flag answers this" is the milder cousin of
the P10 problem — it gestures at a flag that does not exist rather than naming one. It survives on the
strength of the misconception it targets ("the tool I know probably does this"), which is real.

**Recommended fix:** none required. Flagged for the record so the pattern is visible: two of seventeen
practice items lean on non-existent CLI surface. Two is tolerable; a third would be a trend.

---

### Practice Q3 (L1171): "Which is the complete list of signals OpenTelemetry currently supports?"

**Issue:** option C is an **excellent** distractor drawn from material the chapter never teaches.

C is "Metrics, logs, traces, profiles, dumps" — the CNCF TAG Observability whitepaper's five-signal
enumeration, correctly sourced in the answer key (L1322). As a trap it is first-rate: a genuine rival
taxonomy from a genuine authority, disambiguated fairly by a stem that names OpenTelemetry explicitly.
It is not a reading-comprehension trick.

The architecture problem is placement. §2 (L228–L312) teaches four signals and never mentions that a
different CNCF document enumerates five. So a reader who picks C is not being *corrected against
taught material* — they are meeting the rival taxonomy for the first time in an answer key. That
inverts the self-correction design: traps should detect misconceptions in what the chapter taught.

**Recommended fix:** add one clause to §2, immediately after the four-signal Fixed Point (L245): *"The
CNCF TAG Observability whitepaper enumerates a different five — metrics, logs, traces, profiles and
dumps. Two authorities, two taxonomies; when a question names OpenTelemetry, it wants the four."* One
sentence converts a surprise into a discrimination the reader was prepared for, and it strengthens
rather than weakens the item.

---

### All three checkpoints (L380, L701, L990): no low-score revision prompt

**Issue:** skill Part 11 specifies a score-banded revision prompt with a specific section reference
for readers who score 0–2, and the Ethical Checkpoint lists "revision prompts included for low
checkpoint scores." All three checkpoints close with a "**Checkpoint: You've Now Mastered**" block
(L442, L756, L1039) — a competence signal per Part 13 — and none carries a score band or a
back-pointer for a reader who missed most of it.

The Soundings block has its rubric (L84–L88), so the chapter demonstrates the pattern and then does
not apply it to the post-tests, where the diagnostic value is higher.

**Recommended fix:** add two lines above each ✓ list. For CP1: *"0–2 correct: re-read §3 before
continuing — §4 assumes the metrics-server boundary. 3–4: review your misses. 5: move on."* CP2 →
§4 and §5. CP3 → §6 and §7. This is adjacent to my six audit dimensions rather than inside them, and
is reported as a WARN, not a gate-blocker.

## Retrieval-practice spacing

- Chapter 18 target: **20–25%** of checkpoint questions from earlier chapters (skill Part 10,
  "Chapter 6+"); B3 sets this chapter at the **25% ceiling** as the last content chapter.
- Actual, checkpoints: **26.7%** (4 of 15 tagged `[retrieval: chN]`) —
  CP1 Q4 `[ch5]` L400 · CP1 Q5 `[ch10]` L407 · CP2 Q5 `[ch17]` L718 · CP3 Q5 `[ch6]` L1002
- Actual, practice: **23.5%** (4 of 17) — P6 `[ch5]` · P7 `[ch13]` · P13 `[ch17]` · P14 `[ch6]`
- Actual, all graded items: **25.0%** (8 of 32)
- Status: **compliant**

Two notes on the arithmetic, both in the draft's favour:

**On the 26.7%.** Fifteen questions cannot express 25% — the grid is 3/15 = 20.0% or 4/15 = 26.7%.
Four is the correct choice for a chapter B3 placed at the ceiling; three would land it at the floor of
the band. The outline's phrase "at the ceiling" is a rounding, not an error, and I am not scoring the
1.7-point overshoot as non-compliance.

**On tag accuracy.** Three of the four checkpoint tags test genuinely earlier material and one
(P13, practice) does not — see the per-question finding. Verified individually:

| Tagged item | Claims | Actually tests earlier material? |
|---|---|---|
| CP1 Q4 `[ch5]` | Ch 5 §8 requests | **yes** — the denominator is Ch 5's |
| CP1 Q5 `[ch10]` | Ch 10 §3 pattern | **yes** — graded on the verbatim phrase |
| CP2 Q5 `[ch17]` | Ch 17 §5 mesh | **yes** — requires knowing what the sidecar sees |
| CP3 Q5 `[ch6]` | Ch 6 §7 DaemonSet | **yes** |
| P6 `[ch5]` | Ch 5 §8 requests | **yes** |
| P7 `[ch13]` | Ch 13 §7 metrics-server | **yes** |
| P13 `[ch17]` | Ch 17 §3 microservices | **NO** — pure §5; scenery only |
| P14 `[ch6]` | Ch 6 §7 DaemonSet | **yes** |

**Spacing distribution: exceeds the floor comfortably.** Retrieval draws from **five** distinct
chapters — 5, 6, 10, 13, 17. B3's floor is at least one item from ≥4 chapters back; four of the five
source chapters (5, 6, 10, 13) qualify, and Ch 10 is eight chapters back. No two retrieval items in
the same checkpoint draw from the same chapter.

**Uncounted strength.** All **8** Soundings questions are retrieval by construction — every one sources
from a prerequisite in a shipped chapter (Ch 5 ×2, Ch 6, Ch 10, Ch 13 ×2, Ch 17 ×2). They sit outside
the checkpoint percentage by design, but the chapter's true spaced-retrieval load is 16 of 40 items.

**Recommended additions:** none — the chapter is at target. If CP1 Q4 is retired per the Priority fix,
replace its retrieval tag by tagging the incoming §4 component item `[retrieval: ch13]` and framing it
against the metrics-server/Prometheus boundary the outline named as an interleaving target ("same word
'metrics,' two systems, one boundary"). That preserves 4/15 and delivers a join the chapter currently
gets only from P7.

## Coverage vs concepts

Every concept the chapter *introduces* (retrieved concepts excluded), against whether any graded item
— checkpoint or practice — tests it. Soundings-only coverage is marked separately, because a pre-test
confirms arrival knowledge rather than encoding.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| Observability (unknown unknowns) | yes (CP1 Q1, P1) |
| Monitoring (known unknowns) | yes (CP1 Q1, P1) |
| Instrumentation / "properly instrumented" | yes (CP1 Q2, P2) |
| Telemetry | yes — implicit (P2) |
| Code-based vs zero-code instrumentation | yes (CP2 Q5) |
| **Probes are not observability** (§1, L217) | **NO** — Soundings Q1 only; no graded item |
| Signal (definition) | yes (CP2 Q4, P3) |
| The four signals / the count | yes (CP2 Q4, P3) |
| Baggage | yes (CP2 Q4, P4) |
| **Logs lack context on their own** (§2, L288) | **NO** — Soundings Q7 only; no graded item, despite being Exam Alert trap #91 |
| **OpenTelemetry Collector** (§2, L300) | **NO** |
| Time series | yes — implicit (P5) |
| **Metric labels / series identity** (§3, L332) | **NO** |
| Cardinality (§3, L338) | **NO** — *intentional*; draft states it is not exam surface |
| Utilization relative to requests | yes (CP1 Q4, P5, P6) — over-tested, 3 graded items |
| metrics-server vs monitoring system | yes (CP1 Q3, P7) |
| *An object without its component does nothing* | yes (CP1 Q5) |
| Prometheus pull / scrape model | yes (CP2 Q1, P8) |
| Pushgateway and its narrow use | yes (CP2 Q1, P9) |
| **Service discovery** (§4, L463) | **NO** — named inside P8's correct answer, never tested |
| **Client libraries** (§4, L505) | **NO** |
| **Exporters** (§4, L509) | **NO** — despite ⚓ Worth Securing (L515) calling the client-library/exporter discrimination "worth carrying into the exam" |
| **Alertmanager** (§4, L519) | **NO** |
| **PromQL** (§4, L529) | **NO** |
| **Grafana / not-a-CNCF-project** (§4, L539) | **NO** — carried as an Exam Alert trap (L1140) with no item behind it |
| Prometheus non-fit (100% accuracy) | yes (CP2 Q2, P10) |
| Prometheus standalone / no distributed storage | yes (P11) |
| **Prometheus = CNCF's second project, 2016** (§4, L575) | **NO** — Exam Alert trap (L1139) with no item behind it |
| Span / trace / root span | yes (CP2 Q3, P12) |
| Trace ID, span ID, context propagation | yes (P13) |
| **Jaeger** (§5, L657) | **NO** — outline named it explicit exam surface ("span-vs-trace plus 'what is Jaeger'") |
| No native log storage in Kubernetes | yes — implicit (CP3 Q2) |
| `kubectl logs` bounds (rotation, depth, eviction) | yes (CP3 Q1) |
| Three cluster-logging architectures | yes (CP3 Q2) |
| Node-level agent as DaemonSet | yes (CP3 Q5, P14) |
| Sidecar logging | yes — enumeration only (CP3 Q2) |
| Fluentd / Fluent Bit relationship | yes (P15) |
| **Fluent Bit six-stage pipeline** (§6, L960) | **NO** — a full table with no item behind it |
| Reliability ("is the service doing what users expect") | **NO** — chapter thesis; framing, not a fact. Acceptable |
| SLI / SLO | yes (CP3 Q3, P16) |
| SLA (as contrast/distractor) | yes (CP3 Q3, P16) |
| Error budget | distractor only (P16 option D) — *acceptable*, draft de-weights it deliberately |
| Four golden signals | yes (CP3 Q4, P17) |
| Latency as leading indicator of saturation | yes (CP3 Q4) |
| RED / USE | distractor + explanation only (P17 A, C) — **correct posture**; the outline required that no graded item *depend* on RED, and none does |
| Observability's placement under Cloud Native Architecture | **NO** — Exam Alert trap #113 (L1142) with no item behind it |

**The §4 blind spot is the substantive coverage finding.** §4 is the chapter's densest section, it
receives the largest practice allocation (4 of 17, per the outline's own weighting), and all four items
— P8 pull, P9 Pushgateway, P10 non-fit, P11 storage — test *the arrow and the fit*. Not one tests
*the components*. Six §4 concepts go untested: service discovery, client libraries, exporters,
Alertmanager, PromQL, Grafana. The client-library/exporter pair is the sharpest miss, because the
draft itself tells the reader at L515 that the discrimination is "worth carrying into the exam" and
then never asks for it — an emphasis signal the question set does not honour.

Three further untested items are carried in the Exam Alert trap table (L1131–L1145) as things that
"cost real candidates real points": Grafana-is-not-CNCF, Prometheus-was-second-not-first, and the
domain-placement change. A trap the chapter names and never tests is a claim the reader cannot check.
(Note that Prometheus-second-in-2016 is testable without breaching the outline's prohibition, which
covers only a project's *current* maturity level, not sourced history.)

## Priority fix

One edit closes four findings at once, at zero budget cost:

> **Retire CP1 Q4 (L400) and spend the slot on §4 component vocabulary.**

That single move: (1) removes the chapter's only ambiguous item; (2) breaks the CP1 Q4 ↔ P6 duplicate
pair; (3) reduces denominator testing from four passes to three; and (4) gives §4's component
vocabulary its first graded appearance. Suggested replacement, four-option MC, tagged
`[retrieval: ch13]` to preserve 4/15 spacing and deliver the metrics-server × Prometheus join the
outline asked for:

> *Your team runs a PostgreSQL instance you cannot modify and a Go service you wrote. Both must appear
> in Prometheus. Which pairing is correct?*
> A) A client library for both — B) An exporter for both — C) **A client library in the Go service, an
> exporter alongside PostgreSQL** — D) The Pushgateway for PostgreSQL, a client library for the Go service

D is the strongest distractor available: it targets the reader who has correctly learned that the
Pushgateway handles "things Prometheus can't reach into" and over-generalises from short-lived jobs to
unmodifiable software — a real misconception the chapter's own Pushgateway emphasis makes more likely,
not less.

Secondary fixes, in descending value: P8 option C → exporter-push-inversion (adds a second exporter
touch); P10 option B → scrape-interval misconception (removes the fabricated flag); one clause in §2
naming the TAG whitepaper's five (prepares P3's best distractor); P13 retrieval tag dropped or made
real; three checkpoint revision prompts added.
```

**Verdict: WARN, no gate-blocking FAIL.** Why-wrong coverage is complete across all 20 multiple-choice items, budget is met exactly in all four categories, the Soundings spoiler check is clean against all six Fixed Points, and retrieval spacing is at the intended ceiling drawing from five chapters. One item (CP1 Q4) is ambiguous and should be retired; the factual question underneath it — whether Kubernetes copies a limit into an unset request — belongs to the fact-accuracy audit, and I've routed it there rather than ruling on it. The one structural finding worth the author's attention is that §4's component vocabulary is taught with an explicit "worth carrying into the exam" flag and then never tested, while §3's denominator is tested four times.
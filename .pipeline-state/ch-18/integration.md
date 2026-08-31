All checks complete. Producing the report.

```markdown
# Integration Check — KCNA Chapter 18

## Summary

- Terminology consistency: **pass** (3 low-severity acronym/register items, no drift in canonical forms)
- Callbacks to earlier chapters: **52 correct / 0 incorrect** (39 cross-bearing instances across 21 distinct targets, + 13 prose chapter callbacks)
- Retrieval-practice accuracy: **pass** (7 tagged items, all correctly attributed; 26.7% of Bearings, at the ceiling B3 set for this chapter)
- Glossary coverage: **47 ledger-owned concepts introduced, 47 defined in-chapter, 5 terms require glossary/register entries** (2 of which surface in graded text and need an in-text gloss instead)
- Contradictions with earlier canon: **none**
- Ethical guardrails (skill Part 14): **fail** — 1 of 8 items (#8, "frequently tested" vs "might be tested"), one line, one-phrase fix

**Note on method.** The knowledge-base shards were empty for this stage (`[no knowledge-base shards tagged]`). Rather than guess, I verified every callback and cross-bearing against the **shipped chapter files** in `../Book-KCNA/`, which now contain Chapters 1–17 — the B6 skeleton still lists Ch 12–17 as `[PLANNED]`, but they have since materialized. Every claim below is line-accurate against `draft-v2.md` and the shipped files.

---

## Terminology consistency

Verified against the B7 ledger's **Canonical forms** and **Acronym register**.

| Term | Canonical form | Occurrences | Drift? |
|---|---|---|---|
| Prometheus | `Prometheus` | 89 | No |
| metrics-server | `metrics-server` (lowercase, hyphenated) | 34 | No |
| baggage / Baggage | lowercase in prose; capitalized sentence-initially and in figures | 32 / 12 | No — all 12 capitalized uses are sentence-initial, heading, or figure |
| OpenTelemetry | `OpenTelemetry` · `OTel` | 30 / 5 | **Minor** — see finding 6 |
| Pushgateway | `Pushgateway` | 24 | No |
| Fluentd | `Fluentd` (one word) | 22 | No |
| Fluent Bit | `Fluent Bit` (two words) | 15 | No — asymmetry correctly preserved, and made explicit by a 🪢 Mnemonic |
| Jaeger | `Jaeger` | 16 | No |
| DaemonSet | `DaemonSet` (CamelCase) | 16 | No |
| kubelet | `kubelet` (lowercase) | 12 | No |
| Grafana | `Grafana` | 7 | No |
| Alertmanager | `Alertmanager` (one word) | 3 | No |
| StatefulSet | `StatefulSet` | 3 | No |
| ResourceQuota / LimitRange | CamelCase | 2 / 1 | No — both carry cross-bearings to Ch 8 §3 |
| cloud native | never hyphenated | — | No — **0 hyphenated instances**, against 16 in shipped Ch 1–8 (ledger flag ⚑8). This chapter is clean. |
| Kubernetes | spelled out; no `K8s` in prose | — | No — the 28 `k8s` matches are all `[source: k8s-docs-*]` snapshot IDs |
| Pod / pod | capitalized for the object | — | No — the 2 lowercase uses are `kubectl top pods` (a command) and a verbatim Kubernetes quotation at L816 |
| **metric label** vs Kubernetes label | homonym; sense B qualified | — | **Acceptable.** The bolded first use (L~322) is bare *inside a verbatim source quote*, which cannot be altered; the 🪝 Snag immediately after does the disambiguation explicitly. The §3 subheading "Labels, and the cost of one" is bare — optional one-word fix to "Metric labels". |
| **control plane** | bare = the cluster's (Ch 3 §2) | 1 | No — sole use is the Q11 explanation, correct sense, with a Ch 3 §2 pointer |
| **resource request** vs API request | qualified where ambiguous | — | No — §3 uses "resource request" in full at the denominator; §5/§7 use "request" only in the request-path sense, unambiguous in context |

### The named pattern — verbatim

The ledger's errata flags this as the book's most-reinforced retrieval phrase, and records that a wording defect in the ledger itself once propagated into shipped Ch 6/13/17. Ch 18 uses it **three times, all verbatim**:

- L72 (Soundings A3), L360 (§3), L437 (Bearings 1 A5) — `an object without its component does nothing`

No variants. This is a clean pass on the item most likely to fail.

### The ordinal convention

The ⛑ book-level convention ("state the pattern, never the count") is honored. §8's "you have now seen it four times" is immediately followed by the four enumerated instances, which is the sanctioned exception (a closed set the reader can see). No running ordinal is asserted for control loops or pluggable interfaces.

---

## Callback correctness

### Cross-bearings — 39 instances, 21 distinct targets, all resolve

Every `Ch N §M` pointer was checked against the **shipped chapter headings**, not the skeleton alone. All 21 targets exist with matching content:

| Target | Shipped heading | Uses |
|---|---|---|
| Ch 2 §4 | The Container Runtime Interface | 1 |
| Ch 3 §2 | The Control Plane | 1 |
| Ch 4 §5 | The Universal Join | 1 |
| Ch 5 §7 | Three Probes, Three Jobs | 3 |
| Ch 5 §8 | What a Pod Is Owed | 2 |
| Ch 6 §6 | When Pods Are Not Interchangeable | 1 |
| Ch 6 §7 | One Per Node, and Work That Ends | 4 |
| Ch 7 §1 | One Decision, Made Once | 1 |
| Ch 8 §3 | Dividing a Shared Cluster | 2 |
| Ch 9 §2 | The Address That Doesn't Last | 1 |
| Ch 10 §3 | The Object Is Not the Implementation | 3 |
| Ch 13 §3 | Looking Inside | 3 |
| Ch 13 §4 | Pods That Start and Then Don't Stay | 1 |
| Ch 13 §7 | Numbers Nobody Collects by Default | 5 |
| Ch 17 §2 | Sandbox, Incubating, Graduated, and Who Decides | 2 |
| Ch 17 §3 | Small Pieces, Replaced Whole | 2 |
| Ch 17 §4 | Every Place Kubernetes Lets You In | 1 |
| Ch 17 §5 | A Network That Knows What It's Carrying | 3 |
| Ch 1 (heading name, no §) | The Curriculum That Moved Under Everyone's Feet | 2 |

**Two items worth recording as verified rather than assumed:**

- **The Ch 1 pointers are correctly formed.** B6 Collision #1 requires Ch 1 be addressed by heading name only, because it carries no `§N` anchors. Both uses comply.
- **The figure pointer resolves.** L~378 cites `ch13-fig04-metrics-pipeline-and-metrics-server`. That anchor exists at `chapter-13-when-the-cluster-won-t-answer.md:1287`, inside §7 (L1263–L1469). Retrieved, not redrawn, exactly as the outline specified.

### Inbound pointers — all 8 land

Ch 18 is the last content chapter, so every forward promise made to it must be honored here. All eight resolve:

| From | Promise | Honored by |
|---|---|---|
| Ch 1:272 | Ch 18 §1 — observability under the current blueprint | §1, closing paragraphs |
| Ch 5:860 | Ch 18 §1 — health checking is not observability | §1, "What a probe is not" |
| Ch 5:969 | Ch 18 §3 — utilization relative to requests | §3, "The denominator" |
| Ch 6:890 | Ch 18 — node-level log collection | §6 |
| Ch 13:1336 | Ch 18 §3 — metrics-server versus a monitoring system | §3, "The boundary that gets tested" |
| Ch 13:1354 | Ch 18 §6 — node-level logging agents | §6 |
| Ch 15:526 | Ch 18 §6 — lines from everywhere | §6 (title matches verbatim) |
| Ch 17:1387 | Ch 18 §3 — utilization relative to requests | §3 |

§3's line "Two earlier chapters sent you here for one number" is **arithmetically exact**: Ch 5 §8 and Ch 17 §7 are the only two inbound pointers for that fact.

### Prose callbacks — 13, all correct

| Line | Claim | Verified |
|---|---|---|
| L96, L1134 | "Chapter 17 ended by handing you a bill" | ✓ Ch 17's Voyage Ahead makes exactly this argument |
| L320 | "Chapter 13 taught you the resource metrics pipeline: metrics-server, `kubectl top`" | ✓ Ch 13 §7 |
| L362 | "Chapter 13 established what metrics-server is for… and what it is scoped to" | ✓ Ch 13:1336 states "It is not a monitoring system, it keeps no history" |
| L619 | "the sentence closing the loop Chapter 17 opened" | ✓ Ch 17 §3 microservices |
| L697 | mesh telemetry "closes a loop from Chapter 17" | ✓ Ch 17 §5 |
| L810 | "You have used `kubectl logs` since Chapter 13" | ✓ ledger: first appears Ch 13 §3 |
| L1130 | "Chapter 17 made the case that Kubernetes' durability comes from defining interfaces rather than implementations" | ✓ Ch 17 §4/§9 |
| L1457 | the four domain names | ✓ verbatim match to Ch 17's sourced list |
| L1465–1471 | Ch 19's six sections | ✓ matches B6 skeleton in order |

**L1467 deserves an explicit clearance,** because it is the one place a callback could have collided with a reserved payoff. It reads: "the control loop from Chapter 3, the operator pattern from Chapter 6, and the GitOps agent from Chapter 15 turn out to be one idea seen three times." Shipped Ch 6 tells the reader they have seen the loop twice and that "the third time is the one that matters" — Ch 15 §7, the book's designated primary Zenith. Ch 18 names **exactly those three instances and no fourth**. It reinforces the sanctioned count rather than adding to it. Correct.

**One observation, not a defect.** L96–L100 reproduces three consecutive sentences from Ch 17's Voyage Ahead **verbatim** ("Break a monolith into microservices and one request becomes twenty…"). The framing sentence ("Chapter 17 ended by handing you a bill") signals it as deliberate recapitulation, and a reader turning the page will recognize it. Flagging only so the author can confirm the verbatim echo is intended rather than paraphrase drift.

---

## Retrieval-practice accuracy

Seven tagged items. Every tag was checked against the shipped target chapter.

| Item | Tag | Topic | Correct? |
|---|---|---|---|
| Bearings 1 Q5 (L405) | `ch10` | `kubectl top` failing; naming the absent-component pattern | ✓ Ch 10 §3 is the pattern's naming home |
| Bearings 2 Q4 (L730) | `ch13` | metrics-server's scope vs Prometheus collection | ✓ Ch 13 §7 |
| Bearings 2 Q5 (L739) | `ch17` | mesh telemetry without code changes | ✓ Ch 17 §5 |
| Bearings 3 Q5 (L1021) | `ch6` | DaemonSet vs Deployment for per-node placement | ✓ Ch 6 §7 |
| Practice Q6 (L1224) | `ch5` | no CPU request → utilization undefined | ✓ Ch 5 §8, which states requests are "the denominator when monitoring reports 'utilization'" |
| Practice Q7 (L1233) | `ch13` | metrics-server keeps no history | ✓ Ch 13 §7 |
| Practice Q14 (L1296) | `ch6` | DaemonSet for log collection | ✓ Ch 6 §7 |

**Counts.** Bearings 4/15 = 26.7% (the ceiling B3 assigned this chapter as the last content chapter with the most accumulated decay). Practice 3/17 = 17.6%. Combined 7/32 = 21.9%, inside skill Part 10's 20–25% band for Ch 6+. Drawn from five chapters (5, 6, 10, 13, 17), three of them more than four chapters back.

**The v1→v2 change is correct and needs no action.** draft-v1 carried 8 tags; v2 carries 7. The question-quality audit flagged v1's Practice Q13 `[retrieval: ch17]` as **mis-tagged** — "Nothing from Chapter 17 is tested… 'six microservices' is scenery, not a retrieval target" — and recommended the tag be "dropped or made real," with the Bearings count preserved by tagging the incoming §4 component item `[retrieval: ch13]`. The revision did precisely both. The resulting drop to 17.6% in Practice was explicitly anticipated by the audit. I checked this before flagging it, and it is a correctly handled diagnostic, not a defect.

**Soundings.** All 8 questions are retrieval by construction and none requires this chapter; each answer carries a pointer to the owning section. All eight pointers resolve. The chapter's true spaced-retrieval load is 15 of 40 items.

---

## Glossary coverage

47 ledger-owned concepts, all defined in-chapter. Listing only the terms that need action:

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| observability · monitoring · known/unknown unknowns · instrumentation · telemetry | yes | no |
| signal · trace · metric · log · baggage · OTel Collector | yes | no |
| time series · sample · metric label · cardinality | yes | no |
| Prometheus · scrape/pull · target · service discovery · exporter · client library · Pushgateway · PromQL · Alertmanager · Grafana | yes | no |
| distributed tracing · span · root span · trace ID · span ID · context propagation · Jaeger | yes | no |
| node-level logging agent · Fluentd · Fluent Bit · sidecar logging · log rotation | yes | no |
| reliability · SLI · SLO · SLA · error budget · four golden signals · RED · USE | yes | no |
| **SRE** (L139, L928) | **no** | **yes** — plus expansion at first use; see finding 4 |
| **p99 / `pNN` notation** (L370, L386) | **no** | **no — needs an in-text gloss**; it reaches graded text; see finding 5 |
| **W3C TraceContext** (L621) | no (explicitly deprioritized) | yes — register row + entry; ungraded |
| **OpenTracing** (L687) | no (inside a quotation) | yes — register row + entry; ungraded |
| HAProxy · StatsD · Graphite · PagerDuty · OpsGenie | n/a — product names inside sourced quotes | no |

**Two book-level ledger items are discharged by this chapter:**

- **SLA orphan closed.** The B7 orphan list required Ch 18 §7 to own SLA "as a one-clause contrast," and required it *not* be glossary-only because it serves as a distractor. §7 defines it with a sourced definition and the "what happens if the SLOs aren't met?" discrimination procedure, and Q16 option A uses it as the distractor. Fully resolved.
- **No forbidden orphan terms appear.** Verified zero occurrences of PodDisruptionBudget/PDB, ABAC, descheduler, eBPF, PodSecurityPolicy/PSP, LTS, and the legacy capitalized `Endpoints` — all of which the ledger restricts from graded text pending author decisions.

---

## Ethical guardrails check

- [x] No fabricated statistics or claims — every factual sentence carries a `[source:]` tag; scenario numbers (4 seconds, 99.9%, 02:10) are transparently hypothetical
- [x] Fear-based content uses real examples — stakes are operational (the 3 a.m. incident), never invented breach scenarios
- [x] Simplification acknowledged — Dead Reckoning present; §2's Snag openly reconciles three conflicting authoritative signal counts rather than hiding the disagreement; §4 states where Prometheus does *not* fit; §7's Closer Look names one word carrying three meanings
- [x] Authority claims cite legitimate sources — CNCF, OpenTelemetry, Prometheus, Kubernetes, Google SRE
- [ ] **"Frequently tested" claims are verifiable against the curriculum snapshot — FAIL, see finding 1**
- [x] No strawmanning of alternative study methods
- [x] **Subject dignity (skill v5.7)** — every wry beat is aimed at practitioners ("you have a monitoring system and an aspiration"; "teams who start by buying a dashboard product are so often the ones who cannot explain their own outages"). No humor is directed at users harmed by outages. Clean.

---

## Recommended fixes

The revision stage addressed the diagnostics: all three checkpoints now carry low-score revision prompts, the ambiguous CP1 Q4 was retired, the mis-tagged retrieval item was corrected with the prescribed compensating tag, and the §4 component-vocabulary gap is now tested at Bearings 2 Q4 and Practice Q8/Q4. The structural audit was already 0 fail / 0 warn, and all seven planned figure anchors survive revision unchanged. The findings below are new at this gate.

**1. [BLOCKING — Ethical Guardrail #8] L1155 asserts exam-performance data the book does not have.**

> `**Common Traps** — each of these has cost real candidates real points:`

This phrasing appears **nowhere else in the book** — I grepped all 17 shipped chapters. It claims observed candidate scoring outcomes across eleven traps. B1 gap **G35** states plainly: *"No official sample questions in the cached set. No published item bank, no disclosed difficulty mix, no question-type breakdown."* Four binding documents (`arc-outline.md:397`, `chapter-lineup.md:184`, `domain-analysis.md:498` and G35, `retrieval-architecture.md:19`) forbid framing traps as exam frequency, and `section-skeleton.md:302` binds Ch 19 §2 to the same rule — which this chapter's own Exam Alert would then contradict.

Note the traps themselves are fine: all eleven are `[source]`-tagged in B1, and #89 even states "Baggage is the one candidates drop." What is unsupported is the claim about *scoring outcomes*. Fix by adopting the form Ch 15 already ships:

> `**Common Traps** — these are distinctions that are easy to confuse, and they are the ones this material rewards getting right:`

**2. [Ethical Guardrail #8, soft] L784** — "Those two are worth more exam points than anything else in this chapter." The book has domain-level weights only (44/28/16/12); no sub-domain point allocation is published. Suggest "worth the most of anything in this chapter" or "the two most reliably tested ideas here."

**3. [Ethical Guardrail #8, soft] L1346** — "the three-signal answer the majority of candidates give." B1 #89 supports *"candidates drop baggage"*; it does not support a majority (>50%) quantification. Drop "majority" to "commonly."

**4. [Acronym register] L139 — SRE is unexpanded on its first appearance in the entire book.** Zero occurrences in Chapters 1–17. The register rule is absolute ("expanded on its first use in the book, without exception"). Fix: "Google's own Site Reliability Engineering (SRE) text". Add the register row and a glossary entry; the ledger already routes SRE to glossary-only, and it correctly stays out of graded text here.

**5. [Graded-text lookup] `p99` is used in a graded question stem and never defined.** L328 glosses "95th-percentile" in prose, but the `pNN` notation first appears at L370 (a table) and then at **L386, the Bearings Checkpoint 1 Q1 stem**. The ledger's own standard: *"a term used in question text or an answer key may not be glossary-only."* The item is not answer-blocking — the dashboard list is scenery — but the reader has no lookup path. Cheapest fix: pair the forms at L370, e.g. `Compute p99 (99th-percentile) latency over a rolling 7 days`.

**6. [Acronym register] `OTel` is never paired with `OpenTelemetry` in prose.** Its first reader-visible use is inside the §2 figure at L302 (`OTel COLLECTOR`). Both forms are sanctioned by the ledger; only the pairing is missing. Fix: one parenthetical at the first `OpenTelemetry` in §1, or at §2's Collector paragraph.

**7. [Metadata ambiguity — author's call] L4 displays the same 12% Ch 17 displays, for a domain worth 12% in total.** Ch 17's frontmatter records the authored split as 7 + 5, and mandates that the in-chapter line carry the published 12% rather than the allocation — so Ch 18's `12%` is *correct by that rule*, but two adjacent chapters each showing "Domain Weight: 12%" can read as though either one carries the whole domain. **Ch 16 already solved this**, and its form is shipped:

> `**Domain Weight: 12% (Cloud Native Architecture) [source: cncf-kcna-curriculum-pdf-2026-08-23] | Competency: Observability | Authored allocation for this chapter: ~5%**`

That also restores the `[source:]` tag on the published weight, which Ch 15 and Ch 16 carry and Ch 17 and Ch 18 currently omit.

**8. [Glossary/register, low] W3C TraceContext (L621) and OpenTracing (L687).** Both appear once, both inside quotations, neither graded, and the chapter explicitly tells the reader the header format is out of scope. Queue register rows and glossary entries at the glossary build; no in-text change needed.

**9. [Low, optional] §7's title capitalizes "Service."** Under the ledger's rule, capital-S `Service` denotes the Kubernetes object; here it denotes a running application. The heading is title-cased and comes verbatim from the binding B6 skeleton, so the draft is correct to follow it — but as this is the last gate, the author may prefer lowercasing it (the book already grants `kubectl` a title-case exception by rule). The chapter's prose is clean: the one capital-S `Service` in body text (Bearings 1 A3e, "the endpoint leaving and rejoining the Service") is the correct object sense.

### Carried to stage 14 — not defects

**A. Frontmatter.** `draft-v2.md` opens at the H1 with no YAML block. I verified this is **normal pipeline behavior**, not a regression: Ch 16's and Ch 17's draft-v2 files are the same, and Ch 16's revision stage left an AUTHOR-REVIEW explaining that frontmatter is deliberately not added at revision ("two YAML blocks would be worse than none") and asking the integration gate to confirm its contents. Confirming here — Ch 18's block must carry:

- `chapter: 18` · `chapter_type: "content"` · `title: "Reading the Instruments"`
- `domain_weight_pct: 5` — **the authored allocation, not 12**, per Ch 17's frontmatter rule
- `objectives`: D4.1 (Observability) **plus D4.2 as secondary**, which is item (1) of the unresolved AUTHOR-REVIEW at L567

**B. Five AUTHOR-REVIEW comments remain live** (L312, L567, L693, L898, L1005). Four are self-contained records. **L567 item (2) is the one that cannot wait**, because Ch 18 is the last content chapter: it asks for a book-level ruling on whether a cross-bearing to an already-audited chapter discharges the `[source:]` tagging obligation for seven Kubernetes claims (probe semantics, metrics-server scope, DaemonSet placement, scheduler placement, the CRI boundary, StatefulSet identity). If the answer is yes, record the rule at book level so each chapter's fact audit stops re-raising it. If no, those seven need their Ch 2/5/6/7 snapshots pulled into this chapter's bundle. Either way it requires no new research — but there is no later chapter to defer it to.
```
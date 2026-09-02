# Image Specifications — KCNA Chapter 18

*Generated from `draft-v1.md` (draft-voice.md does not exist at this stage; line numbers cite `draft-v1.md`). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Reconciliation:** 7 figure anchors found (lines 158, 277, 485, 627, 796, 931, 1062); 7 fenced blocks found (lines 159–190, 278–306, 486–527, 628–661, 797–838, 932–966, 1063–1093). Anchors and blocks pair 1:1. **No unanchored diagrams.**

---

## UNANCHORED DIAGRAMS

None. Every fenced block in `draft-v1.md` is immediately preceded by a `<!-- FIGURE: … -->` anchor.

---

## ANCHOR FLAGS

**1. Non-conforming anchor ID (rule 4).**
`ch18-zenith-instruments-answer-one-question` (draft-v1.md:1062) does not match `ch{NN}-fig{MM}-{kebab-slug}` — it carries no `figMM` segment. It is preserved verbatim below as the join key (rule 6); renaming is an author-review decision. If the author renames it, the natural value is `ch18-fig07-instruments-answer-one-question`, and the anchor must be changed in the draft, here, and in the book-level index in one sweep.

**2. Anchor numbering is non-monotonic in document order.**
Document order is fig01 (§1), fig02 (§2), **fig04** (§4), **fig03** (§5), fig06 (§6), **fig05** (§7), zenith (§8). All six `figMM` numbers are used exactly once, so nothing collides and nothing is missing — but figure numbers do not ascend with the reader. Not a rule violation; flagged because the book-level aggregator sorts by anchor ID and will present these out of reading order.

**3. Two open author decisions are embedded in the specs below** (marked `AUTHOR-DECISION`) and should be resolved before render:
- `ch18-fig01` — three indicator boxes vs. "the 4 questions you picked" caption.
- `ch18-fig04` — the "scrape" label on the service-discovery connector, and the direction/labelling of the Grafana connector.

---

## Figure: ch18-fig01-monitoring-vs-observability

**Anchor ID:** `ch18-fig01-monitoring-vs-observability`
**Purpose:** Makes §1's ★ Fixed Point visible — monitoring and observability differ in *when the question was chosen*, not in tooling or in which system they read.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-column comparison diagram converging on a shared base (concept map)

**Content specification:**
A landscape figure with a centred title, "THE SAME SYSTEM, TWO POSTURES". Two equal-width vertical columns sit side by side above a single wide base box spanning the full width, labelled "THE RUNNING SYSTEM" (letter-spaced, as in the source). The left column is headed "MONITORING" with the subhead "known unknowns"; the right column is headed "OBSERVABILITY" with the subhead "unknown unknowns". Left column, top to bottom: a box reading "questions chosen IN ADVANCE"; a single stem descending from it that fans into exactly three small boxes labelled "CPU", "mem" and "5xx", annotated to one side "fixed indicators"; those three converge into a box reading "DASHBOARD / answers the 4 questions you picked"; one arrow down into the shared base. Right column, top to bottom: a box reading "question arrives AT 02:10 AM"; a single unbroken vertical line descending past a quoted callout set to its right — "why were requests from one client slow in region 2?" — and into a box reading "OPEN QUERY / over rich telemetry"; one arrow down into the shared base. Two caption lines beneath: "Both read the same system. The difference is upstream: one has a fixed question set, one does not."
**The point of the figure is the asymmetry**: the right column has no intermediate fixed-indicator layer, and the empty vertical run is the argument. Do not balance the composition by inventing right-hand boxes.

**Visual style:**
- Palette: inherit book default (brand navy line-art on paper white)
- Size (pixels): 1200x780 landscape
- Font: inherit book default (Roboto Slab for the title and column heads, Fira Sans for box and caption text)
- Accent color for highlighted elements: Brass `#B58B3E` on the right-hand column's unbroken stem and the OPEN QUERY box
- Glyph policy: glyph-free — not a stack or pipeline family figure (style-decisions 2026-08-25)

**Critical details (non-negotiable accuracy):**
- MONITORING is the LEFT column, OBSERVABILITY the RIGHT. Reversing them inverts the argument.
- "known unknowns" attaches to monitoring; "unknown unknowns" attaches to observability. These are not interchangeable.
- Both columns terminate at **one** shared system box. This is one system seen two ways — never two systems.
- The right column must contain **no** fixed-indicator layer. Its emptiness is load-bearing.
- The 02:10 callout stays in quotation marks; it is a question a person asks, not a system label.
- `AUTHOR-DECISION`: the source draws three indicator boxes (CPU, mem, 5xx) but the dashboard box reads "the 4 questions you picked" — the four there are the SRE book's four reasons to monitor, not the three indicators. A reader will try to count them and fail. Resolve before render: either reword the box to "answers the questions you picked", or accept the mismatch deliberately. Do not silently change "4" to "3"; that would break the tie to the four-reasons list in §1's prose.

**Source ASCII (for designer reference):**
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

**Proposed filename:** `ch18-fig01-monitoring-vs-observability.png`

```yaml-figure-spec
anchor_id: ch18-fig01-monitoring-vs-observability
diagram_type: concept_map
source_ascii: |4
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
vendor_terms: []
complexity_hint:
  node_count: 8
  edge_count: 10
  label_count: 13
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, fixed_point, spatial_structure]
  learning_outcome: "Distinguish observability from monitoring by when the question was chosen, not by tooling"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The right column's unbroken stem from the 02:10 question straight to OPEN QUERY, with no fixed-indicator layer between them"
accessibility:
  alt_text_seed: "Two columns above one shared system box. The monitoring column passes through three fixed indicators labelled CPU, memory and 5xx into a dashboard. The observability column runs straight from a question that arrives at 2:10 a.m. into an open query, with no indicator layer in between."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic monitoring/observability concepts; no vendor product, mark or published diagram reproduced."
```

---

## Figure: ch18-fig02-otel-four-signals

**Anchor ID:** `ch18-fig02-otel-four-signals`
**Purpose:** Fixes the count at **four** by giving baggage a visually distinct position — riding across the other three rather than standing beside them — which is exactly why candidates drop it.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** layered component diagram (band over a peer row, converging into a single component)

**Content specification:**
Title across the top: "FOUR SIGNALS" (letter-spaced, as in the source). Immediately beneath, a single wide band spanning the full width of the three columns below it, labelled "BAGGAGE — contextual info passed BETWEEN the others; a separate key-value store, not a measurement. Carries user/account/origin IDs." A short annotation sits to the right of the band: "rides across all three". From the band, three **dotted or dashed** connectors drop to a horizontal rule (drawn as a double line in the source) and continue into three equal-width, adjacent boxes in a row. Left to right the boxes are: "TRACES / path of a request / answers WHERE"; "METRICS / a measurement at runtime / answers WHETHER"; "LOGS / a recording of an event / answers WHAT". The three boxes converge with solid connectors into a single box beneath them labelled "OTel COLLECTOR / receive · process · export". One arrow leaves the Collector downward to a plain text label, "one or more backends".
The dashed-versus-solid contrast is the mechanism of the figure: baggage *accompanies* the three signals, while the three signals *flow into* the Collector. Those are different relationships and must not be drawn with the same line.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1100x850 landscape
- Font: inherit book default (Fira Sans; "OTel COLLECTOR" in Roboto Slab)
- Accent color for highlighted elements: Brass `#B58B3E` on the BAGGAGE band and its three dashed connectors
- Glyph policy: `AUTHOR-CONFIRM` — this is a plausible **pipeline-family** figure under style-decisions 2026-08-25, which would make it eligible for Lucide glyphs from `certcomp-diagrams/assets/glyph-ledger.yaml`. Author to confirm family before render; default to glyph-free if unresolved.

**Critical details (non-negotiable accuracy):**
- **The Collector box must read "receive · process · export" as a single phrase.** Do NOT render receiver / processor / exporter as three named sub-components or pipeline stages. §2 carries an explicit AUTHOR-REVIEW note (draft-v1.md, after the figure) recording that the named taxonomy was not captured verbatim in the cached snapshot and is deliberately withheld; manifest gap G-18c. Introducing it in the figure would state something the prose refuses to state.
- Baggage is **not** a fourth peer box in the row. It sits above and across. A reader must be unable to count only three signals.
- Answer-word mapping is fixed: traces = WHERE, metrics = WHETHER, logs = WHAT. Do not shuffle.
- Left-to-right order is TRACES, METRICS, LOGS.
- Baggage's connectors must be visually distinct (dashed/dotted) from the signal→Collector connectors (solid).
- The backend destination is plural and unnamed. Do not name Jaeger, Prometheus or any commercial vendor here — the swappability is the point.

**Source ASCII (for designer reference):**
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

**Proposed filename:** `ch18-fig02-otel-four-signals.png`

```yaml-figure-spec
anchor_id: ch18-fig02-otel-four-signals
diagram_type: component_diagram
source_ascii: |5
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
vendor_terms: [opentelemetry, otel-collector]
complexity_hint:
  node_count: 6
  edge_count: 7
  label_count: 12
pedagogy:
  part_18_criteria_met: [vendor_taxonomy, spatial_structure, fixed_point]
  learning_outcome: "Name all four OpenTelemetry signals and place baggage correctly as context carried between the other three"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The BAGGAGE band and its three dashed connectors crossing to traces, metrics and logs"
accessibility:
  alt_text_seed: "A wide baggage band spans the top, connected by dashed lines to three boxes below it labelled traces, metrics and logs, which answer where, whether and what. The three converge into an OpenTelemetry Collector that receives, processes and exports to one or more backends."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1100
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "OpenTelemetry signal taxonomy redrawn in Lodestar style; project name used nominatively, no logo or published diagram reproduced."
```

---

## Figure: ch18-fig04-prometheus-pull-architecture

**Anchor ID:** `ch18-fig04-prometheus-pull-architecture`
**Purpose:** Makes the direction of every arrow the visual subject, so that "Prometheus pulls" is remembered as a picture rather than a sentence — and so the four traps built on the pull model stop working.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** component/data-flow architecture with a directional thesis

**Content specification:**
Title across the top: "ARROWS OUT, NOT IN". A tall central box on the right-of-centre, labelled "PROMETHEUS SERVER", with three stacked sub-labels inside it: "scrapes + stores locally", "standalone,", "autonomous". Four boxes stack down the left side, each connected to the Prometheus server by an arrow whose **arrowhead points at the left-hand box**, i.e. away from Prometheus. Top to bottom the left boxes are: "SERVICE DISCOVERY (finds targets)"; "instrumented app (client lib)"; "EXPORTER (binary next to a thing you didn't write)"; "PUSHGATEWAY". Scrape connectors are labelled "scrape" and, on two of them, "HTTP". The service-discovery box carries a second connector labelled "what exists?". Inside or immediately beneath the Pushgateway box sits a small box labelled "short job", connected **upward** into the Pushgateway with an arrow annotated "push ONLY from service-level BATCH jobs", and the whole assembly annotated "one narrow inbound path". From the bottom of the Prometheus server, two connectors run down-right to two boxes: "ALERTMANAGER / routes to email/pager", labelled "push alerts", and "GRAFANA dashboards (NOT CNCF)", labelled "HTTP API (read)". A closing caption sits under the figure: "Every arrow into Prometheus is Prometheus reaching out."
**The whole figure fails if arrowheads are drawn casually.** Every scrape arrowhead lands on the left-hand target; the only arrowhead landing on a left-hand box from below is the short job's push into the Pushgateway.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x900 landscape
- Font: inherit book default (Fira Sans; component names in Roboto Slab)
- Accent color for highlighted elements: Brass `#B58B3E` on the four scrape arrows and their arrowheads
- Glyph policy: glyph-free — component architecture, not a stack or pipeline family figure (style-decisions 2026-08-25)

**Critical details (non-negotiable accuracy):**
- **Every scrape arrowhead points at the target, not at Prometheus.** This is the entire pedagogical payload of the figure.
- The short job → Pushgateway push is the *only* inbound arrow on the left side, and Prometheus still scrapes the Pushgateway. The arrow into Prometheus never reverses.
- The Pushgateway annotation must retain "ONLY from **service-level** BATCH jobs". Dropping "service-level" destroys the §4 snag about jobs tied to a specific machine.
- The "(NOT CNCF)" annotation on Grafana is load-bearing — it backs an explicit exam-trap row. Preserve it.
- Alertmanager receives a **push** from Prometheus. This is the one place the arrow reverses, and it must read as notification dispatch, not metric collection — label it "push alerts" and draw it in a visibly different weight or style from the scrape arrows.
- The client-library box and the exporter box are distinct and must stay distinct: client library = code you wrote, exporter = a separate binary next to code you didn't. §4 tests this discrimination directly.
- `AUTHOR-DECISION (accuracy)`: the source labels the service-discovery connector "scrape". Prometheus **queries** service discovery for a target list; it does not scrape it for metrics. Recommend dropping the "scrape" label on that connector and keeping only "what exists?", or merging the two connectors into one labelled "queries: what exists?". As drawn, a careful reader learns something false in a figure whose entire subject is what gets scraped.
- `AUTHOR-DECISION (accuracy)`: the Grafana connector is drawn as an arrow *from* Prometheus, labelled "HTTP API (read)". That is correct as data flow but risks being read as "Prometheus pushes to Grafana" in a figure about arrow direction. Recommend either labelling it "Grafana queries the HTTP API" or drawing the request direction (Grafana → Prometheus) with the data returning — and in either case rendering it in a different line style from the scrape arrows.

**Source ASCII (for designer reference):**
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

**Proposed filename:** `ch18-fig04-prometheus-pull-architecture.png`

```yaml-figure-spec
anchor_id: ch18-fig04-prometheus-pull-architecture
diagram_type: data_flow
source_ascii: |5
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
vendor_terms: [prometheus, alertmanager, pushgateway, grafana]
complexity_hint:
  node_count: 8
  edge_count: 8
  label_count: 16
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Explain that Prometheus pulls by scraping targets over HTTP, and identify the single narrow inbound path through the Pushgateway"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The four scrape arrows, all originating at the Prometheus server and pointing outward at their targets"
accessibility:
  alt_text_seed: "A central Prometheus server reaches out with four scrape arrows to service discovery, an instrumented app, an exporter and a pushgateway. Only a short batch job pushes inward, into the pushgateway, which Prometheus then scrapes. Prometheus pushes alerts to Alertmanager and serves Grafana over an HTTP API."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf, grafana-labs]
  clearance: own_interpretation
  notes: "Component names used nominatively in a redrawn architecture; no logos or published diagrams reproduced. Re-evaluate to licensed_icon_set if the renderer substitutes vendor icon-pack assets for any box."
```

---

## Figure: ch18-fig03-trace-spans-across-services

**Anchor ID:** `ch18-fig03-trace-spans-across-services`
**Purpose:** Shows what seven log files cannot give you — nesting and duration — so that "a trace is the whole path, a span is one unit of work" becomes a shape rather than a definition.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** trace waterfall (Gantt-style nested span timeline on a shared time axis)

**Content specification:**
Two header lines at the top: "ONE TRACE = the whole request path.  ONE SPAN = one unit of work." and "trace ID: 4bf92f…  (crosses every boundary below)". Beneath them, a horizontal time axis running left to right with an arrowhead at the right end, ticked "0ms" at the left and "4000ms" at the right. Below the axis, six horizontal bars laid out as a waterfall, indented to show parent-child nesting, each bar carrying its service name and its duration as an inline label. The top bar spans the full axis width and reads "ROOT SPAN   api-gateway: POST /checkout   4000ms", annotated to its right "request start→finish". Indented one level beneath it: "auth-svc 120ms". Indented one further level beneath auth-svc: "user-store 85ms". Back at the first indent level: "catalog-svc 3700ms". Indented one level beneath catalog-svc: "cache 8ms", then "pricing-svc → database 3650ms", the latter marked with a pointer annotation reading "here". Three caption lines close the figure: "Seven services. Seven sets of logs, each internally complete. / Only the trace ID makes them one story — and only then does / 'where did the 4 seconds go?' have an answer."
**Bar width must be proportional to duration and bar x-position must reflect start offset.** The source ASCII is a sketch and is not to scale — its 120ms bar is drawn far wider than 3% of the root. In the rendered figure the pricing-svc→database bar must visually dominate at roughly 91% of the root's width, because "where the time went" is the answer the figure delivers.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x800 landscape
- Font: inherit book default — service names and the trace ID in **Fira Mono** (they are identifiers), captions in Fira Sans
- Accent color for highlighted elements: Brass `#B58B3E` fill on the pricing-svc → database bar
- Glyph policy: glyph-free — not a stack or pipeline family figure (style-decisions 2026-08-25)

**Critical details (non-negotiable accuracy):**
- Nesting must be exact: root (api-gateway) → auth-svc → user-store; root → catalog-svc → { cache, pricing-svc → database }. user-store is a child of auth-svc, **not** a sibling; cache and pricing-svc are children of catalog-svc, **not** of the root.
- Durations are exact and must not be rounded: root 4000ms, auth-svc 120ms, user-store 85ms, catalog-svc 3700ms, cache 8ms, pricing-svc → database 3650ms.
- **Six span bars for seven named services** — pricing-svc's database call is drawn as a single span. Do not add a seventh bar to make the caption's "seven" arithmetic work.
- Exactly one root span, spanning the full width. A second full-width bar would contradict "the first span represents the root span".
- The trace ID appears once, at the top, and is presented as the thing that crosses every boundary. It is the join key, not decoration.
- The "here" pointer attaches to the pricing-svc → database bar and nothing else.
- `RENDERER INPUT — start offsets are inferred, not authored.` The draft supplies durations only. A Gantt renderer needs start times. Suggested layout, which preserves all authored durations and all nesting, for author confirmation: root 0→4000; auth-svc 0→120; user-store 20→105; catalog-svc 150→3850; cache 160→168; pricing-svc→database 180→3830. Any alternative is acceptable provided every child sits wholly inside its parent's interval and the authored durations are unchanged.

**Source ASCII (for designer reference):**
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

**Proposed filename:** `ch18-fig03-trace-spans-across-services.png`

```yaml-figure-spec
anchor_id: ch18-fig03-trace-spans-across-services
diagram_type: gantt
source_ascii: |
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
vendor_terms: []
complexity_hint:
  node_count: 6
  edge_count: 5
  label_count: 14
pedagogy:
  part_18_criteria_met: [temporal_structure, quantitative_relationships, fixed_point]
  learning_outcome: "Distinguish a span from a trace and read where a request's time was spent from a nested span timeline"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The pricing-svc to database span at 3650ms, which accounts for almost the whole 4000ms root span"
accessibility:
  alt_text_seed: "A trace waterfall on a four-second time axis. A root span for the API gateway spans the full width; nested beneath it are auth-svc at 120 milliseconds with user-store at 85 milliseconds inside it, and catalog-svc at 3700 milliseconds containing a cache call of 8 milliseconds and a pricing service database call of 3650 milliseconds, which accounts for almost all of the elapsed time."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Invented service names and timings; the trace ID is a truncated W3C TraceContext-format example. No vendor IP."
```

---

## Figure: ch18-fig06-cluster-logging-architectures

**Anchor ID:** `ch18-fig06-cluster-logging-architectures`
**Purpose:** Sets the three cluster-logging architectures side by side so the discriminator is visible — the difference is *where collection happens*, and only one option works without the application's cooperation.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** three-panel comparative Kubernetes deployment diagram sharing one destination

**Content specification:**
Two header lines: "THREE WAYS TO COLLECT.  Same backend in all three; the difference is WHERE collection happens." Three stacked panels occupy the left two-thirds of the figure; a single tall box on the right, spanning all three panels' vertical extent, is labelled "LOGGING BACKEND (outside k8s)". All three panels connect to that one box.
Panel 1, titled "1. NODE-LEVEL AGENT" and annotated "← the default answer": a NODE frame containing three small "Pod" boxes in a row; all three connect downward into a labelled band reading "node filesystem"; an arrow from the filesystem down into a box "AGENT (DaemonSet: 1/node)"; from the agent, a connector leaves the node frame and runs to the shared backend.
Panel 2, titled "2. SIDECAR IN THE POD": a NODE frame containing a single Pod frame, and inside that Pod two adjacent containers, "app" and "sidecar collector", with an arrow from app to sidecar; from the sidecar a connector leaves both frames and runs to the shared backend. Annotation beneath the panel: "one collector PER POD".
Panel 3, titled "3. APP PUSHES DIRECTLY": a NODE frame containing a single Pod frame containing one container, "app w/ logging library"; a connector runs from the app directly out to the shared backend, passing no collector. Two annotations: "no collector at all" beneath the panel, and "app must know about the backend" beside the connector.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1000x1300 portrait
- Font: inherit book default (panel titles in Roboto Slab, box labels in Fira Sans, `DaemonSet` in Fira Mono)
- Accent color for highlighted elements: Brass `#B58B3E` on panel 1's agent box and its connector to the backend
- Glyph policy: `AUTHOR-CONFIRM` — arguably a **pipeline-family** figure (collection path) under style-decisions 2026-08-25; if confirmed, Pod / node / DaemonSet glyphs come from `glyph-ledger.yaml`. Default to glyph-free if unresolved.

**Critical details (non-negotiable accuracy):**
- All three panels terminate at **one shared backend box**. Same destination, different collection point — drawing three separate backends destroys the comparison.
- In panel 1, the Pods do **not** connect to the agent directly. They write to the node filesystem; the agent reads from there. That indirection is precisely why node-level collection works without the application's cooperation, and it is the §6 ⚓ Worth Securing point.
- Panel 1's agent box must retain "(DaemonSet: 1/node)". The workload-resource name is the answer to a graded question.
- In panel 2, the sidecar is **inside** the Pod boundary, adjacent to the app container — not on the node beside the Pod. One collector per Pod.
- Panel 3 has **no collector box of any kind**. The absence is the point.
- The backend annotation "(outside k8s)" must survive.
- Panel order and numbering (1, 2, 3) must be preserved; panel 1 is labelled the default.
- Do not name Fluentd or Fluent Bit inside the figure. §6 names them in prose as agents that *fill* the panel-1 slot; putting a product name in the box would narrow an architecture diagram into a product diagram.

**Source ASCII (for designer reference):**
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
   │  ┌────────────────────────┐  │      ▼
   │  │ Pod                    │  │  ┌────────┐
   │  │ ┌─────┐  ┌───────────┐ │  │  │ LOGGING│
   │  │ │ app │─►│ sidecar   │─┼──┼─►│ BACKEND│
   │  │ └─────┘  │ collector │ │  │  │        │
   │  │          └───────────┘ │  │  │(outside│
   │  └────────────────────────┘  │  │  k8s)  │
   │   one collector PER POD      │  │        │
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

**Proposed filename:** `ch18-fig06-cluster-logging-architectures.png`

```yaml-figure-spec
anchor_id: ch18-fig06-cluster-logging-architectures
diagram_type: k8s_architecture
source_ascii: |
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
     │  ┌────────────────────────┐  │      ▼
     │  │ Pod                    │  │  ┌────────┐
     │  │ ┌─────┐  ┌───────────┐ │  │  │ LOGGING│
     │  │ │ app │─►│ sidecar   │─┼──┼─►│ BACKEND│
     │  │ └─────┘  │ collector │ │  │  │        │
     │  │          └───────────┘ │  │  │(outside│
     │  └────────────────────────┘  │  │  k8s)  │
     │   one collector PER POD      │  │        │
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
vendor_terms: [kubernetes-node, kubernetes-pod, daemonset]
complexity_hint:
  node_count: 14
  edge_count: 8
  label_count: 20
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, vendor_taxonomy]
  learning_outcome: "Name the three cluster-logging architectures and justify the node-level DaemonSet agent as the default"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "Panel 1's agent box, labelled DaemonSet one-per-node, and its connector out to the shared backend"
accessibility:
  alt_text_seed: "Three stacked panels, all feeding one logging backend on the right. In the first, three Pods write to the node filesystem and a DaemonSet agent reads it and forwards. In the second, a sidecar collector inside each Pod forwards the app's logs. In the third, the app pushes straight to the backend with no collector."
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes logging architectures redrawn in Lodestar style; resource names used nominatively, no logo or published diagram reproduced."
```

---

## Figure: ch18-fig05-sli-slo-golden-signals

**Anchor ID:** `ch18-fig05-sli-slo-golden-signals`
**Purpose:** Carries §7's two graded distinctions in one image — the measurement→commitment→contract chain across an internal/external boundary, and the four golden signals with the one relationship worth remembering.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel concept map (containment chain on the left, a 2×2 attribute grid on the right)

**Content specification:**
Two panels side by side under a two-part header: "MEASUREMENT → COMMITMENT → CONTRACT" over the left panel and "THE FOUR GOLDEN SIGNALS" over the right.
**Left panel:** an upper frame labelled "INTERNAL" containing two boxes — "SLI / the measurement", annotated below it "from the USER's perspective", and "SLO / the target you commit to". An arrow runs from SLI to SLO, labelled "measures". A second arrow leaves SLO downward and crosses a heavy horizontal rule labelled "boundary" into a lower frame labelled "EXTERNAL", which contains one box: "SLA / contract w/ CONSEQUENCES". Beneath, inside the external frame, a caption: "'what happens if the SLO isn't met?' No consequence = it's an SLO, not an SLA".
**Right panel:** a 2×2 grid of four equal cells. Top-left "LATENCY / time to serve a request / track OK and FAIL separate". Top-right "TRAFFIC / demand on the system / req/sec, sessions". Bottom-left "ERRORS / rate of failed requests / explicit, implicit, or by policy". Bottom-right "SATURATION / how FULL the svc is / degrades BEFORE 100%". A curved arrow runs from the latency cell to the saturation cell, captioned "latency increases are often a LEADING INDICATOR of saturation".
The two panels are related but must not be read as one chain: the visual gutter between them has to be wide enough that "saturation" is never taken as a fourth step after SLA.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x820 landscape
- Font: inherit book default (SLI/SLO/SLA and the four signal names in Roboto Slab, definitions in Fira Sans)
- Accent color for highlighted elements: Brass `#B58B3E` on the SLI→SLO "measures" arrow, and on the latency→saturation leading-indicator arrow
- Glyph policy: glyph-free — not a stack or pipeline family figure (style-decisions 2026-08-25)

**Critical details (non-negotiable accuracy):**
- SLI and SLO are **inside** the INTERNAL frame; SLA is **inside** the EXTERNAL frame, below the boundary rule. The boundary is the whole discrimination.
- The chain runs SLI → SLO → SLA and is never reversed. The "measures" label belongs on the SLI→SLO arrow only.
- The SLI's "from the USER's perspective" annotation must survive — it is the clause separating an SLI from any other measurement, and §7 leans on it.
- Exactly four golden-signal cells: LATENCY, TRAFFIC, ERRORS, SATURATION. Not three, not five.
- The leading-indicator arrow runs **from latency to saturation**, not the reverse.
- Latency's "track OK and FAIL separate" and saturation's "degrades BEFORE 100%" are the two operational refinements the practice questions test. Keep both.
- **Do not add RED or USE terms to this figure.** §7 names both in prose, but they are deliberately outside the figure — RED's only surviving authoritative source is a blog post by its originator (see the AUTHOR-REVIEW note at the end of §7), and no graded item depends on it. Adding "rate / duration" cells would give RED teaching weight the chapter withholds.
- The word "utilization" must not appear in this figure. §7 flags it as carrying three different meanings in this chapter; the golden-signals concept here is **saturation**.

**Source ASCII (for designer reference):**
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

**Proposed filename:** `ch18-fig05-sli-slo-golden-signals.png`

```yaml-figure-spec
anchor_id: ch18-fig05-sli-slo-golden-signals
diagram_type: concept_map
source_ascii: |
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
vendor_terms: []
complexity_hint:
  node_count: 9
  edge_count: 3
  label_count: 15
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Distinguish an SLI from an SLO from an SLA, and name the four golden signals with latency as a leading indicator of saturation"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The SLI to SLO arrow labelled 'measures' — the step from an observed number to a committed target"
accessibility:
  alt_text_seed: "On the left, an internal frame holds an SLI, measured from the user's perspective, feeding an SLO target; below a labelled boundary, an external frame holds an SLA contract with consequences. On the right, a two-by-two grid of latency, traffic, errors and saturation, with an arrow from latency to saturation marking latency increases as a leading indicator of saturation."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [google]
  clearance: own_interpretation
  notes: "SLI/SLO/SLA and four-golden-signals terminology originate in Google's SRE book; taxonomy redrawn in Lodestar style, terms used nominatively, and all quoted definitions cited to the cached snapshot in the surrounding prose. No figure reproduced."
```

---

## Figure: ch18-zenith-instruments-answer-one-question

**Anchor ID:** `ch18-zenith-instruments-answer-one-question`
*(Anchor does not match the `ch{NN}-fig{MM}-{slug}` pattern — see ANCHOR FLAGS above. Preserved verbatim as the join key.)*
**Purpose:** The chapter's ☀️ Zenith figure — collapses six sections of instruments into one claim: they are not four topics but four resolutions of a single question, with baggage as what makes them agree on the subject.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** convergence concept map (three answers up into one question, one substrate beneath)

**Content specification:**
A single box at the top, containing a quoted question across three lines: "Is the service doing what users expect it to be doing?" Beneath it, three equal boxes in a row, each connected **upward** into the question box by an arrow with the arrowhead at the question. Left to right: "METRIC / WHETHER / error rate crossed 2% at 02:07"; "TRACE / WHERE / 3.65s of 4s in pricing-svc's query"; "LOG / WHAT / the line the code actually emitted". Beneath the three, a single wide box connected to all three from below, reading "BAGGAGE — what makes all three about THE SAME REQUEST rather than three separate stories". A closing caption, centred: "Not four topics. One question, four resolutions."
Composition is symmetric and vertical: question at the apex, three instruments in the middle band, baggage as the base. The three connectors above and the three below must be visibly different in weight or style — the upper three carry answers, the lower three carry identity.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x900 landscape
- Font: inherit book default (the quoted question in Roboto Slab, set larger than the box labels; `pricing-svc` in Fira Mono)
- Accent color for highlighted elements: Brass `#B58B3E` on the BAGGAGE box and its three connectors
- Glyph policy: glyph-free — synthesis concept map, not a stack or pipeline family figure (style-decisions 2026-08-25)

**Critical details (non-negotiable accuracy):**
- The question is at the **top** and all three instrument arrows point **up into it**. The instruments answer the question; the question does not flow down into the instruments. Reversing this inverts the chapter's thesis.
- Baggage is at the **bottom**, joined to all three. It is the substrate that makes them one story — not a fourth answer, and not a peer in the instrument row.
- Word mapping is fixed: METRIC = WHETHER, TRACE = WHERE, LOG = WHAT.
- The three worked examples must survive verbatim; they are callbacks to earlier figures in this chapter, and losing them turns a synthesis into a definition list.
- The question renders inside quotation marks, exactly as written. It is quoted material carrying a citation in the surrounding prose.
- `AUTHOR-DECISION (consistency)`: this figure orders the instruments **METRIC, TRACE, LOG**, while `ch18-fig02` orders them **TRACES, METRICS, LOGS**. Both orders are in the draft. Harmonizing would strengthen the callback; leaving them is defensible since §8 orders by the whether/where/what sequence its prose uses. Author to decide before render — this is a draft-text change as well as a figure change.

**Source ASCII (for designer reference):**
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

**Proposed filename:** `ch18-zenith-instruments-answer-one-question.png`

```yaml-figure-spec
anchor_id: ch18-zenith-instruments-answer-one-question
diagram_type: concept_map
source_ascii: |9
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
vendor_terms: []
complexity_hint:
  node_count: 5
  edge_count: 6
  label_count: 13
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure, distinguishing_alternatives]
  learning_outcome: "Choose the right signal for a question — whether, where or what — and explain why baggage is what makes the three cohere"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The BAGGAGE box at the base, joined to all three instruments"
accessibility:
  alt_text_seed: "One question at the top asks whether the service is doing what users expect. Three boxes below point up into it: a metric answering whether, a trace answering where, and a log answering what. A baggage box beneath connects to all three, making them about the same request rather than three separate stories."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Quoted reliability question and the OpenTelemetry signal names are cited to cached snapshots in the surrounding prose; diagram is an original synthesis, no vendor logo or published figure reproduced."
```
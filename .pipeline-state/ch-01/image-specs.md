`draft-voice.md` wasn't in the context pack because the orchestrator's post-voice swap had already moved it into `draft-v1.md` (with the pre-voice copy preserved as `draft-v1-prevoice.md`). I read the voiced draft from `../Book-KCNA/.pipeline-state/ch-01/draft-v1.md` and extracted against that. Two anchored figures, no unanchored diagrams.

---

# Image Specifications — KCNA Chapter 1

*Generated from the voiced draft at `.pipeline-state/ch-01/draft-v1.md` (the orchestrator's post-voice swap target; `draft-voice.md` no longer exists on disk after the swap). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

*Anchors found: 2. Fenced blocks found: 2. Unanchored diagrams: none.*

---

## Figure: ch01-fig01-blueprint-change-2025

**Anchor ID:** `ch01-fig01-blueprint-change-2025`
**Purpose:** Shows the reader exactly how the 2025 KCNA blueprint restructure moved weight between domains, so they can recognize study material built for the retired five-domain chart and reallocate their own study time to the current four.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Two-column before/after mapping diagram (labeled flow between a "retired" set and a "current" set, with per-domain change annotations)

**Content specification:**

Render two labeled columns side by side. The left column is headed **RETIRED (five domains)**; the right column is headed **CURRENT (four domains)**. Each column contains one box per domain, and each box carries the domain name plus its percentage weight.

Left column boxes, top to bottom, in exactly this order: `Kubernetes Fundamentals 46%`, `Container Orchestration 22%`, `Cloud Native Application Delivery 8%`, `Cloud Native Architecture 16%`, `Cloud Native Observability 8%`. The order is deliberately *not* descending by weight — each left box sits at the vertical position of the right-hand box it maps to.

Right column boxes, top to bottom: `Kubernetes Fundamentals 44%`, `Container Orchestration 28%`, `Cloud Native Application Delivery 16%`, `Cloud Native Architecture 12%`.

Draw five arrows left-to-right. Three are one-to-one: Fundamentals → Fundamentals, Orchestration → Orchestration, Application Delivery → Application Delivery. The remaining two converge: both `Cloud Native Architecture 16%` and `Cloud Native Observability 8%` join and arrive together at `Cloud Native Architecture 12%`. Draw that convergence as an explicit merge — the two lines meet at a junction before the single arrowhead lands on the right-hand box — because the merge is the point of the whole figure.

Annotate each of the top three arrows with its change, set apart from the box labels: `−2` on Fundamentals, `+6` on Orchestration, `×2` on Application Delivery. Beside the merge junction, place a short annotation: *"Observability folded in as a competency, not a standalone domain."* Beneath the `Cloud Native Observability 8%` box on the left, place the note *"[domain no longer exists]"*.

The two elements that must dominate the reader's eye are (a) the `×2` on Application Delivery and (b) the disappearance of Observability as a domain. Everything else is context for those two facts.

**Visual style:**
- Palette: inherit book default (professional blue/gray, Lodestar Ledgers navy family)
- Size (pixels): 1100x600 landscape
- Font: inherit book default (Fira Sans body, Fira Mono for the percentage figures)
- Accent color for highlighted elements: Brass `#B58B3E` on the four current-column weight values and on the `×2` annotation. Render the retired column at reduced emphasis (lighter stroke weight, muted fill) so the eye lands on the current column first.

**Critical details (non-negotiable accuracy):**
- Retired is on the **left**, current on the **right**. Reversing them inverts the chapter's argument.
- The retired column has **five** boxes; the current column has **four**. This count difference is the fastest visual read of the figure and must survive at thumbnail size.
- Weights must be exact: retired 46 / 22 / 8 / 16 / 8; current 44 / 28 / 16 / 12. Current weights sum to 100.
- `Cloud Native Application Delivery` went **8% → 16%** (doubled). It did not go 16% → 8%. This is the most consequential single fact in the figure and the one most likely to be transposed.
- `Cloud Native Architecture` went **16% → 12%** — it *lost* weight while *gaining* the observability competency. Do not draw or annotate anything implying 16 + 8 = 24, and **do not render this as a Sankey or any proportional-flow diagram**: band widths would have to conserve, and this restructure does not conserve. The merge is structural absorption, not arithmetic.
- `Cloud Native Observability` must be shown as a former **domain**, not as a deleted topic. The "folded in as a competency" annotation is required; without it the figure implies observability was removed from the exam, which is wrong and is the exact trap the chapter's checkpoint question 1 tests.
- The left column's vertical ordering aligns each retired domain with its destination. Do not re-sort it into descending weight order.
- The ASCII abbreviates "Cloud Native App Delivery" for width. The rendered figure should spell out **Cloud Native Application Delivery** in full. Domain names are otherwise verbatim from the published CNCF/Linux Foundation blueprint and must not be paraphrased.

**Source ASCII (for designer reference):**
```
     RETIRED (five domains)                  CURRENT (four domains)
     ─────────────────────────               ──────────────────────────

     Kubernetes Fundamentals    46%  ──────► Kubernetes Fundamentals    44%   (−2)

     Container Orchestration    22%  ──────► Container Orchestration    28%   (+6)

     Cloud Native App Delivery   8%  ──────► Cloud Native App Delivery  16%   (×2)

     Cloud Native Architecture  16%  ──┐
                                       ├───► Cloud Native Architecture  12%
     Cloud Native Observability  8%  ──┘        (Observability folded in
                                                 as a competency, not a
          [domain no longer exists]              standalone domain)
```

**Proposed filename:** `ch01-fig01-blueprint-change-2025.png`

```yaml-figure-spec
anchor_id: ch01-fig01-blueprint-change-2025
diagram_type: flowchart
source_ascii: |
       RETIRED (five domains)                  CURRENT (four domains)
       ─────────────────────────               ──────────────────────────

       Kubernetes Fundamentals    46%  ──────► Kubernetes Fundamentals    44%   (−2)

       Container Orchestration    22%  ──────► Container Orchestration    28%   (+6)

       Cloud Native App Delivery   8%  ──────► Cloud Native App Delivery  16%   (×2)

       Cloud Native Architecture  16%  ──┐
                                         ├───► Cloud Native Architecture  12%
       Cloud Native Observability  8%  ──┘        (Observability folded in
                                                   as a competency, not a
            [domain no longer exists]              standalone domain)
vendor_terms: []
complexity_hint:
  node_count: 9
  edge_count: 5
  label_count: 16
pedagogy:
  part_18_criteria_met: [temporal_structure, quantitative_relationships, distinguishing_alternatives, fixed_point]
  learning_outcome: "State the four current KCNA domain weights and identify which topics moved in the 2025 restructure, so that stale five-domain study material can be recognized and discounted"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The four current-column weight values — 44 / 28 / 16 / 12"
accessibility:
  alt_text_seed: "Two-column diagram comparing the retired five-domain KCNA blueprint on the left with the current four-domain blueprint on the right. Kubernetes Fundamentals moves from 46 percent to 44 percent, Container Orchestration from 22 to 28 percent, Cloud Native Application Delivery from 8 to 16 percent. Cloud Native Architecture at 16 percent and Cloud Native Observability at 8 percent merge into a single Cloud Native Architecture domain at 12 percent, with Observability folded in as a competency rather than remaining a standalone domain."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Domain names and published weights are factual exam-blueprint data from the CNCF/Linux Foundation exam page; the comparison layout and change annotations are Lodestar's own construction. No CNCF logos, marks, or reproduced page layout."
```

---

## Figure: ch01-fig02-book-map-parts-to-domains

**Anchor ID:** `ch01-fig02-book-map-parts-to-domains`
**Purpose:** Establishes that Parts II–V of the book correspond one-to-one with the four exam domains, so the reader can read their position in the book directly as their coverage of the blueprint without translating between the two.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Correspondence map — a structured four-column table with explicit linkage drawn between the book-Part column and the exam-domain column

**Content specification:**

Render a six-row map with four columns, headed **PART**, **CHAPTERS**, **EXAM DOMAIN**, and **WEIGHT**. A horizontal rule sits under the header row and another closes the body.

The six rows, in order:

| PART | CHAPTERS | EXAM DOMAIN | WEIGHT |
|---|---|---|---|
| I — Orientation | Ch 1 | (none — orientation) | — |
| II — Kubernetes Fundamentals | Ch 2–8 | Kubernetes Fundamentals | 44% |
| III — Container Orchestration | Ch 9–13 | Container Orchestration | 28% |
| IV — Application Delivery | Ch 14–16 | Cloud Native Application Delivery | 16% |
| V — Cloud Native Architecture | Ch 17–18 | Cloud Native Architecture | 12% |
| VI — Departure | Ch 19–20 | (synthesis + mock exam) | — |

Rows II through V are the payload. Bind them visually as a contiguous band: draw an explicit connector (a bracket, a tie-line, or four short horizontal links) between the PART cell and the EXAM DOMAIN cell of each of those four rows, and enclose the band so it reads as one block distinct from rows I and VI. Rows I and VI must be rendered at lower emphasis — muted fill, lighter type — with the em-dash in their WEIGHT cell clearly legible as "no exam weight," not as a missing value.

Below the closing rule, set two footnote lines in smaller type: *"Parts II–V map one-to-one onto the four exam domains."* and *"Parts I and VI carry no exam weight — which is itself worth knowing."*

The point of the diagram is the visible one-to-one alignment across the middle four rows. A designer who renders this as a plain table without the linkage has produced a table of contents; the connector band is what makes it a figure.

**Visual style:**
- Palette: inherit book default (professional blue/gray, Lodestar Ledgers navy family)
- Size (pixels): 1200x640 landscape
- Font: inherit book default (Fira Sans for names, Fira Mono for chapter ranges and percentages so the numeric columns align on a common grid)
- Accent color for highlighted elements: Brass `#B58B3E` on the four connectors binding Parts II–V to their domains, and on the four weight values. Rows I and VI in muted gray.

**Critical details (non-negotiable accuracy):**
- Six Parts, twenty chapters. Chapter ranges are exact and contiguous with no gaps or overlaps: I = Ch 1; II = Ch 2–8; III = Ch 9–13; IV = Ch 14–16; V = Ch 17–18; VI = Ch 19–20.
- Weights are 44 / 28 / 16 / 12 and must match `ch01-fig01-blueprint-change-2025` exactly. These two figures are checked against each other by any attentive reader.
- Parts I and VI carry **no** weight. Do not assign them 0%, and do not leave their WEIGHT cell blank — an em-dash is the required treatment, because "carries no exam weight" is a stated fact, not an omission.
- Part IV is titled **Application Delivery** in the book but maps to the domain **Cloud Native Application Delivery**. The two strings differ; reproduce both as given. Do not normalize the Part title to match the domain name or vice versa.
- Part V's book title and its domain name are both "Cloud Native Architecture" — identical strings. This is correct, not a duplication error.
- The mapping is one-to-one across Parts II–V: exactly four connectors, no crossings, no Part linked to two domains and no domain fed by two Parts.
- Row order is fixed (I through VI). Do not sort by weight.
- The Part V row is misaligned by one character in the source ASCII (the long title pushes the CHAPTERS column). That is an artifact of monospace width, not a semantic offset — align all columns cleanly in the render.

**Source ASCII (for designer reference):**
```
  PART                          CHAPTERS      EXAM DOMAIN                        WEIGHT
  ─────────────────────────────────────────────────────────────────────────────────────
  I    Orientation              Ch 1          (none — orientation)                  —

  II   Kubernetes Fundamentals  Ch 2–8        Kubernetes Fundamentals              44%

  III  Container Orchestration  Ch 9–13       Container Orchestration              28%

  IV   Application Delivery     Ch 14–16      Cloud Native Application Delivery    16%

  V    Cloud Native Architecture Ch 17–18     Cloud Native Architecture            12%

  VI   Departure                Ch 19–20      (synthesis + mock exam)               —
  ─────────────────────────────────────────────────────────────────────────────────────
       Parts II–V map one-to-one onto the four exam domains.
       Parts I and VI carry no exam weight — which is itself worth knowing.
```

**Proposed filename:** `ch01-fig02-book-map-parts-to-domains.png`

```yaml-figure-spec
anchor_id: ch01-fig02-book-map-parts-to-domains
diagram_type: concept_map
source_ascii: |
    PART                          CHAPTERS      EXAM DOMAIN                        WEIGHT
    ─────────────────────────────────────────────────────────────────────────────────────
    I    Orientation              Ch 1          (none — orientation)                  —

    II   Kubernetes Fundamentals  Ch 2–8        Kubernetes Fundamentals              44%

    III  Container Orchestration  Ch 9–13       Container Orchestration              28%

    IV   Application Delivery     Ch 14–16      Cloud Native Application Delivery    16%

    V    Cloud Native Architecture Ch 17–18     Cloud Native Architecture            12%

    VI   Departure                Ch 19–20      (synthesis + mock exam)               —
    ─────────────────────────────────────────────────────────────────────────────────────
         Parts II–V map one-to-one onto the four exam domains.
         Parts I and VI carry no exam weight — which is itself worth knowing.
vendor_terms: []
complexity_hint:
  node_count: 10
  edge_count: 4
  label_count: 30
pedagogy:
  part_18_criteria_met: [spatial_structure, quantitative_relationships]
  learning_outcome: "Locate any chapter of this book within the KCNA exam blueprint, and read progress through the book as progress through the domains"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The four connectors binding Parts II–V to their corresponding exam domains"
accessibility:
  alt_text_seed: "A map of the book's six Parts against the four KCNA exam domains. Part one, Orientation, covers Chapter 1 and carries no exam weight. Part two, Kubernetes Fundamentals, covers Chapters 2 to 8 and maps to the Kubernetes Fundamentals domain at 44 percent. Part three, Container Orchestration, covers Chapters 9 to 13 and maps to Container Orchestration at 28 percent. Part four, Application Delivery, covers Chapters 14 to 16 and maps to Cloud Native Application Delivery at 16 percent. Part five, Cloud Native Architecture, covers Chapters 17 to 18 and maps to Cloud Native Architecture at 12 percent. Part six, Departure, covers Chapters 19 to 20 for synthesis and the mock exam, and carries no exam weight. Parts two through five map one to one onto the four exam domains."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Exam domain names and weights are factual CNCF blueprint data; the Part structure, chapter allocation, and correspondence layout are Lodestar's own editorial work."
```

---

*No UNANCHORED DIAGRAMS section: the draft contains exactly two fenced blocks, both immediately preceded by a conforming `<!-- FIGURE: chNN-figMM-slug -->` anchor. Both anchor IDs match the `ch{NN}-fig{MM}-{kebab-slug}` pattern.*
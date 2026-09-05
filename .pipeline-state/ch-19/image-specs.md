# Image Specifications — KCNA Chapter 19

*Generated from `draft-v1.md` (pipeline note in the stage input confirms `draft-voice.md` does not exist yet; line references below cite `draft-v1.md`). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Anchor audit:** 3 anchors found, 3 fenced ASCII diagrams found, 3 matched pairs. No unanchored diagrams. All three anchor IDs conform to `ch{NN}-fig{MM}-{kebab-slug}`.

**Note for the author-review gate:** the §5 HTML comment about `the-lodestar.md` is an `AUTHOR-REVIEW` marker, not a `FIGURE` anchor, and correctly produces no entry here.

---

## Figure: ch19-fig01-cross-domain-integration-map

**Anchor ID:** `ch19-fig01-cross-domain-integration-map`
**Purpose:** Show at a glance that the book is nine reusable patterns distributed across eighteen chapters rather than eighteen independent topics — and let the reader *see* which threads are densest, because density predicts which patterns will appear in a question stem that never names them.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Presence matrix (grid of threads × chapters), grouped into three labelled tiers

**Content specification:**

The figure is a presence matrix: nine named cross-cutting threads on one axis, seventeen chapters (2 through 18) on the other, with a filled mark at every intersection where that thread is built or extended in that chapter. **Render it transposed relative to the source ASCII** — chapters running vertically down the left as rows, the nine threads running horizontally as columns. The source ASCII is landscape with seventeen columns; at e-reader width that scales to unreadable type, and the transposed form fits a portrait canvas near 3:4 with the same information (see *Critical details*).

Group the nine thread columns into three labelled bands, exactly as the prose does: **Structural** (threads 1–3), **Interface** (threads 4–6), **Policy** (threads 7–9). Draw a thin vertical rule between bands and set the band names as a header row above the thread names. Thread column headers, in order, are: `1 control loop`, `2 scope boundary`, `3 absent component`, `4 declarative`, `5 label join`, `6 pluggability`, `7 identity`, `8 requests/limits`, `9 additive/allow`.

Chapter rows are labelled with the bare chapter number, `2` through `18`, top to bottom. Do not add chapter titles — the figure is a density read, not a table of contents, and titles would triple its width.

Each intersection is either a filled dot or empty. Do not connect the dots with rules or lines; the source ASCII uses `──` connectors purely as a character-cell drawing artifact, and reproducing them would falsely imply an ordered path through the chapters. A thread is a *set* of chapters, not a sequence.

The point of the figure is column density. A reader should be able to sweep the nine columns and see immediately that three or four of them are heavily populated and the rest are sparse. Thread 3's column carries the Brass accent (see below) because it is the chapter's ★ Fixed Point.

**Visual style:**
- Palette: book default (brand navy on cream/white), plus the Brass accent
- Size (pixels): 900×1200 portrait
- Font: inherit book default (Fira Sans for labels, Fira Mono for chapter numbers)
- Accent color for highlighted elements: Brass `#B58B3E` for the entire thread-3 column — its header, its dots, and a light Brass column tint
- **No Lucide glyphs.** Per style-decisions `[LOCKED 2026-08-25]`, semantic glyphs are carried only by stack and pipeline figures; this is a matrix and stays glyph-free.
- Marks must be distinguishable in greyscale: use a filled dot for presence and nothing for absence — never two colours of dot

**Critical details (non-negotiable accuracy):**

- **The ASCII grid is not column-aligned and must not be traced.** Row 5 (`label join`) is one cell short of the other rows, and several rows drift against the `Ch:` header. Take the mark positions from the §1 prose paths, transcribed below, not from the character grid.
- The authoritative mark sets, derived from the thread paths in §1 of the draft:
  - Thread 1 control loop → Ch **3, 4, 6, 11, 15, 17**
  - Thread 2 scope boundary → Ch **4, 8, 12**
  - Thread 3 absent component → Ch **3, 10, 11, 13, 17, 18**
  - Thread 4 declarative → Ch **4, 6, 14, 15**
  - Thread 5 label join → Ch **4, 6, 7, 9, 10, 12**
  - Thread 6 pluggability → Ch **2, 6, 9, 11, 17**
  - Thread 7 identity → Ch **5, 12, 15**
  - Thread 8 requests/limits → Ch **5, 7, 13, 17, 18**
  - Thread 9 additive/allow → Ch **10, 12**
- Total marks: **40**. Count them after rendering.
- Thread order is fixed and numbered 1–9. Do not reorder by density; the numbers are referenced by name throughout §2 ("this is thread 3", "thread 8 arriving from the other direction") and in the Practice Questions answer keys.
- The tier bands are a reading aid, and the draft says so explicitly. Style them lighter than the thread labels so they do not read as taxonomy.
- Chapter range is 2–18 inclusive. Chapter 1 and Chapters 19–20 are deliberately absent.

> **AUTHOR-REVIEW — two reconciliations needed before render.**
> 1. **Density claim disagrees with the derived data.** The prose beneath the figure states "threads 3, 5 and 6 touch the most chapters." On the paths as written, threads **1, 3 and 5** tie at six chapters each and thread 6 has five. Either the prose sentence or one of the thread paths needs adjusting. The figure will visibly contradict the sentence if rendered from the paths as-is.
> 2. **Chapter 16 receives zero marks.** No thread in §1 routes through Ch 16, so its row will be entirely empty. That is defensible (Ch 16 is application-scope troubleshooting, and §2's D3 table is where it appears) but an all-empty row reads as a rendering error. Either add the thread that legitimately touches Ch 16 or accept the empty row with intent.
>
> Neither blocks the illustrator from starting layout; both must be settled before final art.

**Source ASCII (for designer reference):**
```
              Ch:   2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18

  STRUCTURAL TIER
1 control loop      ·  ●  ●  ·  ●  ·  ·  ·  ·  ●  ·  ·  ·  ●  ·  ●  ·
2 scope boundary    ·  ·  ●  ·  ·  ·  ●  ·  ·  ·  ●  ·  ·  ·  ·  ·  ·
3 absent component  ·  ●  ·  ·  ·  ·  ·  ·  ●  ●  ·  ●  ·  ·  ·  ●  ●

  INTERFACE TIER
4 declarative       ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ·  ·  ●  ●  ·  ·  ·
5 label join        ·  ·  ●  ·  ●  ●  ·  ●  ●  ·  ●  ·  ·  ·  ●  ·  ·
6 pluggability      ●  ·  ·  ·  ●  ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ●  ·

  POLICY TIER
7 identity          ·  ·  ·  ●  ·  ·  ·  ·  ·  ·  ●  ·  ·  ●  ·  ·  ·
8 requests/limits   ·  ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ●  ·  ·  ·  ●  ●
9 additive/allow    ·  ·  ·  ·  ·  ·  ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ·
```

**Proposed filename:** `ch19-fig01-cross-domain-integration-map.png`

```yaml-figure-spec
anchor_id: ch19-fig01-cross-domain-integration-map
diagram_type: concept_map
source_ascii: |2
                Ch:   2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18

    STRUCTURAL TIER
  1 control loop      ·  ●  ●  ·  ●  ·  ·  ·  ·  ●  ·  ·  ·  ●  ·  ●  ·
  2 scope boundary    ·  ·  ●  ·  ·  ·  ●  ·  ·  ·  ●  ·  ·  ·  ·  ·  ·
  3 absent component  ·  ●  ·  ·  ·  ·  ·  ·  ●  ●  ·  ●  ·  ·  ·  ●  ●

    INTERFACE TIER
  4 declarative       ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ·  ·  ●  ●  ·  ·  ·
  5 label join        ·  ·  ●  ·  ●  ●  ·  ●  ●  ·  ●  ·  ·  ·  ●  ·  ·
  6 pluggability      ●  ·  ·  ·  ●  ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ●  ·

    POLICY TIER
  7 identity          ·  ·  ·  ●  ·  ·  ·  ·  ·  ·  ●  ·  ·  ●  ·  ·  ·
  8 requests/limits   ·  ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ●  ·  ·  ·  ●  ●
  9 additive/allow    ·  ·  ·  ·  ·  ·  ·  ·  ●  ·  ●  ·  ·  ·  ·  ·  ·
vendor_terms: []
complexity_hint:
  node_count: 26
  edge_count: 40
  label_count: 29
pedagogy:
  part_18_criteria_met: [spatial_structure, zenith]
  learning_outcome: "Recognize the book as nine reusable cross-cutting patterns distributed across eighteen chapters, and identify which threads are dense enough to appear in question stems that never name them"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The thread 3 column (absent component) — the chapter's stated Fixed Point"
accessibility:
  alt_text_seed: "Presence matrix of nine cross-cutting themes against chapters 2 to 18, grouped into structural, interface and policy tiers; the absent-component thread is highlighted and, with the control-loop and label-join threads, spans the most chapters"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 900
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Original Lodestar synthesis of the book's own thematic structure; depicts no vendor diagram, logo or trademarked artwork"
```

---

## Figure: ch19-fig02-confusion-pair-matrix

**Anchor ID:** `ch19-fig02-confusion-pair-matrix`
**Purpose:** Give the reader a single drillable card of every confusion pair in the book paired with its one-line discriminator, so that §2 can be worked actively (cover the right column, answer, uncover) rather than read passively.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Two-column reference card, banded into four exam-domain groups

**Content specification:**

Two columns. Left column: the confusion pair, written as `A / B`. Right column: the discriminator, always phrased as a question in quotation marks. A single arrow glyph (`→`) sits between them, repeated on every row — it is the visual spine of the figure and signals "this pair resolves to this question."

Twenty-three rows total, in four bands separated by horizontal rules. Band labels sit above each group and name the exam domain: **D1**, **D2**, **D3**, **D4**. In the source ASCII the domain tag is repeated on every row; in the rendered figure lift it to a band header instead and drop the per-row repetition, which recovers horizontal space for the discriminator text.

Set the column header once at the top: left `PAIR`, right `DISCRIMINATOR (the question to ask)`.

The whole design intent is coverability. The right column must be a clean vertical block with a hard left edge, so a reader can lay a finger or a card down it and hide every answer at once without hiding any part of the left column. Do not stagger, indent, or centre the right column. Do not add connecting dot-leaders between the columns — they would defeat the cover.

Left-column entries are terse by design and use the same abbreviations as the source (`ClusterIP/NodePort/LB`, `RWO / RWOP`, `mesh CP / cluster CP`, `HPA / VPA`, `SLI / SLO / SLA`, `TOC / Governing Board`). Keep them verbatim; the expanded forms live in the §2 tables immediately below the figure and repeating them here would double the figure's height.

**Visual style:**
- Palette: book default (brand navy type on cream/white)
- Size (pixels): 1000×1300 portrait
- Font: inherit book default; Fira Mono for the left column's API identifiers (`RWO`, `RWOP`, `OutOfSync`, `ClusterIP`) and Fira Sans for the discriminator questions
- Accent color for highlighted elements: Brass `#B58B3E` on the `→` arrow column and the `DISCRIMINATOR` header — the arrow is the figure's argument, that a pair resolves to a *procedure* and not to a second definition
- **No Lucide glyphs.** Not a stack or pipeline figure; glyph-free per `[LOCKED 2026-08-25]`.
- The four band rules must be visible in greyscale; use weight, not colour, to separate bands

**Critical details (non-negotiable accuracy):**

- **Twenty-three rows, in this exact band distribution: D1 = 6, D2 = 6, D3 = 4, D4 = 7.** Verify the count after typesetting.
- **Every right-column entry must remain a question.** The discriminators are procedures, not definitions — the draft is explicit that "two definitions side by side is what caused the collapse in the first place." A discriminator rewritten as a statement destroys the figure's function.
- Reproduce the discriminator wording exactly. These are memorization targets carried forward into `the-lodestar.md` (§5) and drilled again in §6. In particular: `"Restart it, or stop sending traffic?"`, `"Does replica 0 need to BE replica 0?"`, `"What scope is the BINDING?"`, `"Whose history is being rewound?"`, `"Where do the credentials live?"`, `"One hop, or the whole journey?"` The capitalized emphasis on **BE** and **BINDING** is deliberate and must survive.
- Band order is D1 → D2 → D3 → D4, matching the domain sequence and the descending domain weights (44/28/16/12). Do not reorder.
- Row order within each band is fixed; §2's prose tables follow the same sequence.
- `RWO / RWOP` and `NetworkPolicy default` are two of the four counter-intuitive hazards called out in the ⚠ Navigational Hazards block. Do not accent them individually — the hazards get their own treatment in prose, and accenting two of twenty-three rows here would imply the other twenty-one are safe.

**Source ASCII (for designer reference):**
```
   PAIR                          →  DISCRIMINATOR (the question to ask)
   ───────────────────────────────────────────────────────────────────
   D1  Pod phase / container state → "Lifecycle, or one container?"
   D1  liveness / readiness        → "Restart it, or stop sending traffic?"
   D1  labels / annotations        → "Does anything select on it?"
   D1  ConfigMap / Secret          → "Would you mind this in a log?"
   D1  Deployment / StatefulSet    → "Does replica 0 need to BE replica 0?"
   D1  OCI / CRI                   → "Artifact format, or kubelet's API?"
   ───────────────────────────────────────────────────────────────────
   D2  ClusterIP/NodePort/LB       → "Reachable from where?"
   D2  Ingress object / controller → "The record, or the thing that acts?"
   D2  NetworkPolicy default       → "Is this Pod selected by any policy?"
   D2  Role / ClusterRole binding  → "What scope is the BINDING?"
   D2  PV / PVC                    → "Supply, or demand?"
   D2  RWO / RWOP                  → "One node, or one Pod?"
   ───────────────────────────────────────────────────────────────────
   D3  chart / release / revision  → "Package, install, or version of it?"
   D3  rollout undo / helm rollback→ "Whose history is being rewound?"
   D3  push / pull delivery        → "Where do the credentials live?"
   D3  OutOfSync                   → "Difference, or failure?"
   ───────────────────────────────────────────────────────────────────
   D4  mesh CP / cluster CP        → "Whose control plane?"
   D4  sidecar / ambient           → "Proxy per Pod, or per node?"
   D4  HPA / VPA                   → "More replicas, or bigger ones?"
   D4  observability / monitoring  → "New questions, or known ones?"
   D4  span / trace                → "One hop, or the whole journey?"
   D4  SLI / SLO / SLA             → "Measure, target, or consequence?"
   D4  TOC / Governing Board       → "Technical, or business?"
```

**Proposed filename:** `ch19-fig02-confusion-pair-matrix.png`

```yaml-figure-spec
anchor_id: ch19-fig02-confusion-pair-matrix
diagram_type: concept_map
source_ascii: |5
     PAIR                          →  DISCRIMINATOR (the question to ask)
     ───────────────────────────────────────────────────────────────────
     D1  Pod phase / container state → "Lifecycle, or one container?"
     D1  liveness / readiness        → "Restart it, or stop sending traffic?"
     D1  labels / annotations        → "Does anything select on it?"
     D1  ConfigMap / Secret          → "Would you mind this in a log?"
     D1  Deployment / StatefulSet    → "Does replica 0 need to BE replica 0?"
     D1  OCI / CRI                   → "Artifact format, or kubelet's API?"
     ───────────────────────────────────────────────────────────────────
     D2  ClusterIP/NodePort/LB       → "Reachable from where?"
     D2  Ingress object / controller → "The record, or the thing that acts?"
     D2  NetworkPolicy default       → "Is this Pod selected by any policy?"
     D2  Role / ClusterRole binding  → "What scope is the BINDING?"
     D2  PV / PVC                    → "Supply, or demand?"
     D2  RWO / RWOP                  → "One node, or one Pod?"
     ───────────────────────────────────────────────────────────────────
     D3  chart / release / revision  → "Package, install, or version of it?"
     D3  rollout undo / helm rollback→ "Whose history is being rewound?"
     D3  push / pull delivery        → "Where do the credentials live?"
     D3  OutOfSync                   → "Difference, or failure?"
     ───────────────────────────────────────────────────────────────────
     D4  mesh CP / cluster CP        → "Whose control plane?"
     D4  sidecar / ambient           → "Proxy per Pod, or per node?"
     D4  HPA / VPA                   → "More replicas, or bigger ones?"
     D4  observability / monitoring  → "New questions, or known ones?"
     D4  span / trace                → "One hop, or the whole journey?"
     D4  SLI / SLO / SLA             → "Measure, target, or consequence?"
     D4  TOC / Governing Board       → "Technical, or business?"
vendor_terms: [kubernetes, helm]
complexity_hint:
  node_count: 27
  edge_count: 23
  label_count: 50
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure]
  learning_outcome: "Separate every confusion pair in the book using a one-line procedural test rather than two competing definitions held side by side"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The arrow column and the DISCRIMINATOR header — the figure's claim that a pair resolves to a question, not to a second definition"
accessibility:
  alt_text_seed: "Two-column reference card listing twenty-three confusion pairs from the book, each paired with a one-line question that separates them, banded into the four exam domains"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: false
  max_width_px: 1000
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Discriminator questions are original Lodestar phrasing; API object names are functional terms, not reproduced vendor artwork"
```

---

## Figure: ch19-fig03-exam-day-pacing

**Anchor ID:** `ch19-fig03-exam-day-pacing`
**Purpose:** Make the two-pass pacing rule visually memorable, because the exam permits no scratch paper and the plan has to be executable from memory once the clock starts.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Horizontal time-budget bar (single timeline, split into two labelled phases)

**Content specification:**

A single horizontal bar spanning the ninety-minute exam, divided at the 54-minute mark into two unequal segments. Time labels sit above the bar at three points: `0` at the left end, `54 min` at the division, `90 min` at the right end. The left segment is 60% of the bar's length and the right segment 40% — the proportions must be true to scale, because the proportion *is* the rule.

Left segment header: **FIRST PASS**. Beneath it, four lines:
- `every question, once`
- `answer everything`
- `flag freely`
- `rate = 0.6 × clock ÷ count`

Right segment header: **SECOND PASS**. Beneath it, three lines:
- `flagged questions only`
- `full discriminator work`
- `change only with a reason`
- `reserve = 0.4 × clock`

Two callouts point at the bar from below with short leader arrows. The first points at the `0` end and reads: *read the count off the screen and divide — do not memorize a seconds-per-question number*. The second points at the `90 min` end and reads: *submit with time on the clock*.

The division at 54 minutes is the whole figure. Give it a heavier vertical rule than any other line, and let the two segments differ in fill weight so the 60/40 split reads instantly at thumbnail size.

**Visual style:**
- Palette: book default (brand navy). First-pass segment in a lighter navy tint, second-pass segment in a deeper navy or a hatched fill
- Size (pixels): 1200×450 landscape
- Font: inherit book default; Fira Mono for the time markers and the two formula lines, Fira Sans for the phase descriptions and callouts
- Accent color for highlighted elements: Brass `#B58B3E` on the 54-minute division rule and its label
- **No Lucide glyphs.** Not a stack or pipeline figure; glyph-free per `[LOCKED 2026-08-25]`.
- The 60/40 split must be legible in greyscale from fill weight or hatching alone, not from hue

**Critical details (non-negotiable accuracy):**

- **The split is at 54 minutes of 90, and the segments must be drawn to scale.** A figure that draws the two passes as equal halves teaches the wrong rule. 54 is exactly 60% of 90.
- **90 minutes is the published Linux Foundation multiple-choice duration** [source: `lf-mc-exam-faq-2026-08-31`]. Do not round, adjust, or genericize it.
- **Do not put a question count or a seconds-per-question number anywhere on the figure.** The draft is explicit that the rule is memorized and the arithmetic is not — the reader reads the count off the exam screen and divides on the day. Adding "60 questions" or "90 seconds each" to the art would contradict the ★ Fixed Point directly above it. The 60-question figure appears in the prose as a worked example only.
- Both formulas use the *clock*, not a fixed minute value: `rate = 0.6 × clock ÷ count` and `reserve = 0.4 × clock`. Reproduce them verbatim, including the multiplication and division signs.
- Direction of travel is left to right, and the second pass returns only to flagged questions. Do not draw a return arrow sweeping back across the first-pass segment — the draft's third named time-sink is re-litigating settled answers, and a backward arrow would depict exactly the behaviour the section forbids.
- The two callout texts are instructions, not captions. Keep the imperative phrasing.

**Source ASCII (for designer reference):**
```
  0                              54 min                        90 min
  ├───────────── FIRST PASS ───────┼──── SECOND PASS ────────────┤
  │                                │                             │
  │  every question, once          │  flagged questions only     │
  │  answer everything             │  full discriminator work    │
  │  flag freely                   │  change only with a reason  │
  │                                │                             │
  │  rate = 0.6 × clock ÷ count    │  reserve = 0.4 × clock      │
  │                                │                             │
  └────────────────────────────────┴─────────────────────────────┘
     ▲                                                    ▲
     read the count off the screen                   submit with
     and divide — do not memorize                    time on the clock
     a seconds-per-question number
```

**Proposed filename:** `ch19-fig03-exam-day-pacing.png`

```yaml-figure-spec
anchor_id: ch19-fig03-exam-day-pacing
diagram_type: timeline
source_ascii: |4
    0                              54 min                        90 min
    ├───────────── FIRST PASS ───────┼──── SECOND PASS ────────────┤
    │                                │                             │
    │  every question, once          │  flagged questions only     │
    │  answer everything             │  full discriminator work    │
    │  flag freely                   │  change only with a reason  │
    │                                │                             │
    │  rate = 0.6 × clock ÷ count    │  reserve = 0.4 × clock      │
    │                                │                             │
    └────────────────────────────────┴─────────────────────────────┘
       ▲                                                    ▲
       read the count off the screen                   submit with
       and divide — do not memorize                    time on the clock
       a seconds-per-question number
vendor_terms: []
complexity_hint:
  node_count: 5
  edge_count: 3
  label_count: 14
pedagogy:
  part_18_criteria_met: [temporal_structure, fixed_point]
  learning_outcome: "Execute a two-pass pacing plan on a ninety-minute closed-book exam from memory, banking the first pass at sixty percent of the clock"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The 54-minute division rule separating the first and second passes"
accessibility:
  alt_text_seed: "Ninety-minute exam timeline split at fifty-four minutes; the longer first-pass segment answers and flags every question, and the shorter reserved second-pass segment revisits only flagged ones"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "The ninety-minute duration is a published factual figure; the two-pass allocation and both formulas are original Lodestar guidance"
```
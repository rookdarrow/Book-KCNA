# Image Specifications — KCNA Chapter 6

*Generated from the voiced draft of Chapter 6 ("Fleets, Not Vessels"). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Anchors found:** 6 · **Entries below:** 6 · **Unanchored fenced blocks reviewed:** 3 (1 flagged, 2 excluded as command transcripts)

---

## FLAGS FOR AUTHOR REVIEW

### F1 — Non-conforming anchor ID

`<!-- FIGURE: ch06-zenith-control-loop-instantiated -->` (§9) does not match the required `ch{NN}-fig{MM}-{kebab-slug}` pattern. It has no `fig{MM}` segment. Per Rule 6 the ID is **preserved unchanged** in this document and in the `yaml-figure-spec` block below; renaming is an author-review decision. Suggested conforming ID if the author elects to rename: `ch06-fig06-control-loop-instantiated`. Note that renaming requires a matching edit to the draft anchor, or the join key breaks.

### F2 — Anchor sequence disagrees with caption numbers

Anchor IDs and in-draft caption numbers are transposed for the fourth and fifth figures:

| Document order | Anchor ID | Draft caption |
|---|---|---|
| 1 | `ch06-fig01-deployment-replicaset-pod-ownership` | Figure 6.1 ✓ |
| 2 | `ch06-fig02-rolling-update-maxsurge-maxunavailable` | Figure 6.2 ✓ |
| 3 | `ch06-fig03-recreate-vs-rolling` | Figure 6.3 ✓ |
| 4 | `ch06-fig05-statefulset-vs-deployment-identity` | Figure 6.4 ✗ |
| 5 | `ch06-fig04-workload-resource-decision-tree` | Figure 6.5 ✗ |
| 6 | `ch06-zenith-control-loop-instantiated` | Figure 6.6 (see F1) |

Both IDs are well-formed; only their ordering relative to the captions is inverted. Not corrected here (Rule 6). The Exam Alert refers to "Figure 6.5" as the decision tree, which is consistent with the *caption* numbering, so the caption numbers are the load-bearing reference and the anchor IDs are the outlier.

### F3 — `ch06-fig02` carries an unresolved arithmetic dispute

The draft's own AUTHOR-REVIEW comment records that the outline specifies a ceiling of **12** for ten replicas at defaults, while the cached source (`k8s-docs-deployment-spec-fields-2026-08-24`) specifies `maxSurge` rounds **up**, giving 3 and a ceiling of **13**. The draft uses 13 throughout, and this spec is written to 13. **If the author resolves in favor of 12, this figure must be regenerated** — the ceiling value is drawn on the canvas, not just in the caption.

### F4 — Line numbers unavailable

The unanchored-diagram convention asks for `~Line N` against `draft-v1.md`. Line numbers are **not cited** in this document because the draft was reconstructed from `.draft-v1.md.progress.log`; the on-disk `draft-v1.md` is 4,050 bytes and begins mid-table-row, so any line number cited against it would be wrong. Locations below are given by section and adjacent prose instead.

---

## UNANCHORED DIAGRAMS

The following fenced block appears in the draft without a preceding anchor comment. It will not be in the book-level image index until anchored.

### §4 — "Work one example, once", immediately after *"Ten replicas. Both fields left at their defaults."*

```
  maxSurge        = 25% of 10 = 2.5  →  round UP   →  3
  maxUnavailable  = 25% of 10 = 2.5  →  round DOWN →  2

  ceiling on total Pods      = 10 + 3 = 13
  floor on available Pods    = 10 − 2 =  8
```

Suggested anchor: `ch06-fig07-rolling-update-arithmetic` — **author to confirm before adding to draft.**

**Recommendation, stated for the author to overrule:** this is a worked calculation, not a diagram, and it is fully subsumed by `ch06-fig02`, which renders the same two numbers as lines on a chart. The cheaper resolution is to typeset it as a display-math / monospace block in production rather than render it as a figure, which needs no anchor at all. If the author disagrees and wants it rendered, it routes as `diagram_type: other` and the four rows must keep the opposite rounding arrows adjacent so the asymmetry is visible at a glance.

### Excluded — command transcripts, not figures

Two fenced blocks in §2 are shell transcripts (`kubectl get pods` / `kubectl delete pod` / `kubectl get pods`, and `kubectl scale deployment/web --replicas=5`). Per the illustration standards' ban on unannotated screenshots and the general treatment of terminal output as code samples, these are **not** flagged as unanchored diagrams and need no anchor. Listed here so the structural audit's duplicate flag can be dismissed without re-investigation.

---

## Figure: ch06-fig01-deployment-replicaset-pod-ownership

**Anchor ID:** `ch06-fig01-deployment-replicaset-pod-ownership`
**Draft caption:** Figure 6.1 — the ownership chain
**Purpose:** Establishes that there are three layers between the reader and a running container, not two, so that §4's two-simultaneous-ReplicaSets mechanism has somewhere to live in the reader's mental model.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hierarchical tree, three tiers, top-down, with per-node property annotations

**Content specification:**
Three tiers stacked vertically. The top tier is a single wide box labeled `Deployment "web"` containing three annotated property rows: `Pod template` annotated "what a replacement is", `strategy` annotated "how replacements are made", and `replicas: 3` annotated "the count you write". The middle tier is a single wide box of the same width labeled `ReplicaSet "web-7d4b9c6f8"` containing two annotated property rows: `replicas: 3` annotated "the count it enforces", and `selector` annotated "how it finds its Pods". The bottom tier is three small identical boxes side by side, each labeled `Pod`. A single arrow runs from the Deployment box down to the ReplicaSet box, labeled "owns · sets the count on". Three arrows fan out from the bottom of the ReplicaSet box to the three Pod boxes, each labeled "owns". Beneath the whole structure, a single caption-weight line reads "intent flows DOWN · existence is reported back UP". The point of the figure is the *middle tier's existence* and the split of the two `replicas:` rows across two altitudes — the property annotations are what make that split legible, so they must survive at ebook rendering size rather than being dropped as decoration.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on parchment/white; slate for secondary rules)
- Size (pixels): 900x760 portrait
- Font: inherit book default — Fira Sans for annotations, Fira Mono for the API-literal tokens (`replicas: 3`, `selector`, `Pod template`, `strategy`) and for the object names in quotes
- Accent color for highlighted elements: Brass #B58B3E on the ReplicaSet's `replicas: 3 — the count it enforces` row

**Critical details (non-negotiable accuracy):**
- The Deployment is at the **top** and Pods at the **bottom**. Intent flows down; do not invert.
- The ReplicaSet tier must be present and visually co-equal to the Deployment tier. Collapsing it into a connector or a small annotation destroys the figure's only argument.
- Exactly **three** Pod boxes, matching `replicas: 3`. Not two, not four, not an ellipsis.
- `replicas: 3` appears **twice** — once on the Deployment, once on the ReplicaSet — with *different* annotations. This duplication is deliberate and must not be tidied away as a redundancy.
- The ReplicaSet's name is a hash-suffixed derivative of the Deployment's name (`web` → `web-7d4b9c6f8`). Keep the relationship visible; do not substitute an unrelated name.
- **No Node appears anywhere in this chain.** A Node is where Pods run, not what owns them; Practice Question Q1 distractor D depends on the figure not implying otherwise.
- The Pod boxes are unlabeled beyond `Pod` — no names, no hashes. Their anonymity is the point that §6's contrast figure later reverses.
- The bottom line ("intent flows DOWN · existence is reported back UP") is part of the figure, not the caption.

**Source ASCII (for designer reference):**
```
        ┌──────────────────────────────────────────────────┐
        │  Deployment  "web"                               │
        │                                                  │
        │    Pod template   ──  what a replacement is       │
        │    strategy       ──  how replacements are made   │
        │    replicas: 3    ──  the count you write         │
        └───────────────────────────┬──────────────────────┘
                                    │  owns · sets the count on
                                    ▼
        ┌──────────────────────────────────────────────────┐
        │  ReplicaSet  "web-7d4b9c6f8"                     │
        │                                                  │
        │    replicas: 3    ──  the count it enforces       │
        │    selector       ──  how it finds its Pods       │
        └───────┬───────────────┬───────────────┬──────────┘
                │ owns          │ owns          │ owns
                ▼               ▼               ▼
          ┌──────────┐    ┌──────────┐    ┌──────────┐
          │   Pod    │    │   Pod    │    │   Pod    │
          └──────────┘    └──────────┘    └──────────┘

     intent flows DOWN  ·  existence is reported back UP
```

**Proposed filename:** `ch06-fig01-deployment-replicaset-pod-ownership.png`

```yaml-figure-spec
anchor_id: ch06-fig01-deployment-replicaset-pod-ownership
diagram_type: hierarchy_tree
source_ascii: |2
          ┌──────────────────────────────────────────────────┐
          │  Deployment  "web"                               │
          │                                                  │
          │    Pod template   ──  what a replacement is       │
          │    strategy       ──  how replacements are made   │
          │    replicas: 3    ──  the count you write         │
          └───────────────────────────┬──────────────────────┘
                                      │  owns · sets the count on
                                      ▼
          ┌──────────────────────────────────────────────────┐
          │  ReplicaSet  "web-7d4b9c6f8"                     │
          │                                                  │
          │    replicas: 3    ──  the count it enforces       │
          │    selector       ──  how it finds its Pods       │
          └───────┬───────────────┬───────────────┬──────────┘
                  │ owns          │ owns          │ owns
                  ▼               ▼               ▼
            ┌──────────┐    ┌──────────┐    ┌──────────┐
            │   Pod    │    │   Pod    │    │   Pod    │
            └──────────┘    └──────────┘    └──────────┘

       intent flows DOWN  ·  existence is reported back UP
vendor_terms: [Deployment, ReplicaSet, Pod]
complexity_hint:
  node_count: 5
  edge_count: 4
  label_count: 15
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "Trace the ownership chain from a Deployment down to a running Pod and say which layer holds the template and which enforces the count"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The ReplicaSet's `replicas: 3 — the count it enforces` row, the layer where the count is acted on"
accessibility:
  alt_text_seed: "Three-tier ownership diagram: a Deployment box holding a Pod template, an update strategy and replicas 3 owns a ReplicaSet box holding replicas 3 and a selector, which in turn owns three identical Pod boxes; intent flows downward and existence is reported upward"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original redrawing of publicly documented Kubernetes object ownership; no CNCF logo, icon or artwork reproduced."
```

---

## Figure: ch06-fig02-rolling-update-maxsurge-maxunavailable

**Anchor ID:** `ch06-fig02-rolling-update-maxsurge-maxunavailable`
**Draft caption:** Figure 6.2 — the two bounds are opposite in kind
**Purpose:** Shows that `maxSurge` and `maxUnavailable` bound two *different quantities* in two *different directions*, which is the single most transposable pair of facts in the chapter.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** annotated count-versus-time band chart with two horizontal bound lines

**Content specification:**
A single chart with a vertical axis labeled "count" and a horizontal axis labeled "time" running left to right with an arrowhead; neither axis carries units or tick values beyond the three labeled levels. Three horizontal reference lines span the plot: a dashed line at **13** labeled "CEILING on total" with a second annotation line reading "= desired + maxSurge (10 + 3)"; a solid line at **10** labeled "DESIRED = 10"; and a dashed line at **8** labeled "FLOOR on available" with a second annotation reading "= desired − maxUnavailable (10 − 2)". Between the lines, two populations are drawn as horizontal bands progressing left to right: an "old" band, drawn in a heavy solid fill, starting full and stepping down toward zero; and a "new" band, drawn in a light stipple or hatch fill, starting near zero and stepping up toward full. The two bands overlap through the middle of the timeline — the combined height of old plus new rises above the DESIRED line but never crosses the CEILING, while the portion of the population that is available never drops below the FLOOR. Below the plot, two summary lines read "old + new never rises above the CEILING" and "available never falls below the FLOOR". The point of the figure is the *opposition*: one bound is a ceiling on a total, the other is a floor on a subset, and they are drawn on opposite sides of the desired line for exactly that reason.

**Visual style:**
- Palette: inherit book default; old population in navy solid, new population in slate stipple
- Size (pixels): 1200x520 landscape
- Font: inherit book default — Fira Mono for `maxSurge` and `maxUnavailable` where they appear in annotations, Fira Sans elsewhere
- Accent color for highlighted elements: Brass #B58B3E on both dashed bound lines (treated as one paired accent), navy/slate for everything else

**Critical details (non-negotiable accuracy):**
- Ceiling is **13**, not 12. `maxSurge` is 25% of 10 = 2.5 rounded **UP** to 3. See flag **F3** above — this value is pending author confirmation against the outline.
- Floor is **8**. `maxUnavailable` is 25% of 10 = 2.5 rounded **DOWN** to 2.
- The ceiling bounds **total Pods (old + new)**. The floor bounds **available Pods**. These are two different quantities and the labels must say so; a render that implies both lines bound the same series destroys the figure.
- The ceiling sits **above** the desired line and the floor **below** it. Never swap.
- The old band must actually reach zero by the right edge, and the new band must reach full. The update completes.
- The combined old + new height must visibly exceed 10 during the middle of the timeline — otherwise the surge has no visual referent.
- Both dashed lines must remain distinguishable from the solid DESIRED line in grayscale, by dash pattern rather than color alone.
- The two summary lines below the plot are part of the figure, not the caption.

**Source ASCII (for designer reference):**
```
  count
        │
   13   ┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈  CEILING on total
        │                                          = desired + maxSurge (10 + 3)
        │  old ███████████  ████████  █████  ██
   10   ─┼──────────────────────────────────────  DESIRED = 10
        │  new ░░       ░░░░░░    ░░░░░░░  ░░░░░░░░░░
    8   ┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈  FLOOR on available
        │                                          = desired − maxUnavailable (10 − 2)
        └────────────────────────────────────────▶  time

      old + new  never rises above the CEILING
      available  never falls below the FLOOR
```

**Proposed filename:** `ch06-fig02-rolling-update-maxsurge-maxunavailable.png`

```yaml-figure-spec
anchor_id: ch06-fig02-rolling-update-maxsurge-maxunavailable
diagram_type: xy_chart
source_ascii: |2
    count
          │
     13   ┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈  CEILING on total
          │                                          = desired + maxSurge (10 + 3)
          │  old ███████████  ████████  █████  ██
     10   ─┼──────────────────────────────────────  DESIRED = 10
          │  new ░░       ░░░░░░    ░░░░░░░  ░░░░░░░░░░
      8   ┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈  FLOOR on available
          │                                          = desired − maxUnavailable (10 − 2)
          └────────────────────────────────────────▶  time

        old + new  never rises above the CEILING
        available  never falls below the FLOOR
vendor_terms: []
complexity_hint:
  node_count: 5
  edge_count: 1
  label_count: 14
pedagogy:
  part_18_criteria_met: [quantitative_relationships, temporal_structure, distinguishing_alternatives]
  learning_outcome: "Predict a rolling update's ceiling on total Pods and floor on available Pods from maxSurge, maxUnavailable and the replica count"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The paired dashed bound lines at 13 and 8, accented identically to show they are two halves of one rule"
accessibility:
  alt_text_seed: "Count-versus-time chart for a ten-replica rolling update: a dashed ceiling line at thirteen marks desired plus maxSurge, a solid line at ten marks the desired count, and a dashed floor line at eight marks desired minus maxUnavailable; an old Pod population declines while a new population rises, their total never crossing the ceiling and the available count never falling below the floor"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Abstract count-versus-time chart; API field names are factual identifiers, no vendor IP depicted."
```

---

## Figure: ch06-fig03-recreate-vs-rolling

**Anchor ID:** `ch06-fig03-recreate-vs-rolling`
**Draft caption:** Figure 6.3 — the gap is the whole point
**Purpose:** Makes the cost of `Recreate` visible as a literal gap in availability, so the reader can treat the strategy choice as a deliberate trade rather than a right/wrong answer.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel comparative availability timeline

**Content specification:**
Two stacked panels sharing an identical left-to-right time axis, each with an arrowhead at the right and the label "time". The upper panel is headed `Recreate`; the lower panel is headed `RollingUpdate`. Each panel has a single horizontal series labeled "available". In the **Recreate** panel the availability bar runs solid from the left, stops abruptly, leaves a wide empty gap, and resumes solid to the right edge; the gap is bracketed and labeled "ZERO AVAILABLE", with two beneath-axis annotations reading "all old killed" positioned under the start of the gap and "then new created" positioned under its end. In the **RollingUpdate** panel the availability bar is continuous from left to right with no break, but its fill changes across three regions: solid (all old), a mixed or transitional fill in the middle, then a light stipple (all new), annotated "never reaches zero" above the middle, with "old and new overlap throughout" beneath the axis. The point of the figure is the presence versus absence of the gap; everything else is supporting structure, and the two panels must be vertically aligned so the eye compares the same horizontal position in both.

**Visual style:**
- Palette: inherit book default; old-version fill navy solid, new-version fill slate stipple, transitional region hatched
- Size (pixels): 1200x480 landscape
- Font: inherit book default — Fira Mono for `Recreate` and `RollingUpdate` (they are literal `.spec.strategy.type` values), Fira Sans elsewhere
- Accent color for highlighted elements: Brass #B58B3E on the "ZERO AVAILABLE" bracket and gap boundary only

**Critical details (non-negotiable accuracy):**
- The Recreate gap must reach **actual zero availability** — an empty region, not a thinner bar. All existing Pods are killed before any new Pod is created.
- The RollingUpdate bar must **never break**. Not a narrow gap, not a dotted segment. Continuity is the claim.
- Both panels must use the same time axis direction and scale so the comparison is honest.
- Old and new fills must be distinguishable by **pattern**, not by color alone, so the overlap region reads on E-ink.
- Do not add a value judgment to the render — no red for Recreate, no warning glyphs, no "✗". The surrounding prose is explicit that `Recreate` is a legitimate choice with a stated cost, and a render that editorializes contradicts it.
- The Recreate panel's two beneath-axis annotations must sit under the correct edges of the gap: "all old killed" at its start, "then new created" at its end.

**Source ASCII (for designer reference):**
```
  Recreate
    available  ██████████                    ██████████
                          └── ZERO AVAILABLE ─┘
               ────────────────────────────────────────▶ time
                   all old killed        then new created


  RollingUpdate
    available  ██████████▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░██████████
                        never reaches zero
               ────────────────────────────────────────▶ time
                   old and new overlap throughout
```

**Proposed filename:** `ch06-fig03-recreate-vs-rolling.png`

```yaml-figure-spec
anchor_id: ch06-fig03-recreate-vs-rolling
diagram_type: xy_chart
source_ascii: |2
    Recreate
      available  ██████████                    ██████████
                            └── ZERO AVAILABLE ─┘
                 ────────────────────────────────────────▶ time
                     all old killed        then new created


    RollingUpdate
      available  ██████████▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░██████████
                          never reaches zero
                 ────────────────────────────────────────▶ time
                     old and new overlap throughout
vendor_terms: []
complexity_hint:
  node_count: 4
  edge_count: 2
  label_count: 11
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, temporal_structure]
  learning_outcome: "Explain why Recreate exists, what it costs, and when choosing it deliberately is correct"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The bracketed ZERO AVAILABLE gap in the Recreate panel"
accessibility:
  alt_text_seed: "Two stacked availability timelines: the Recreate strategy shows a solid bar, then a bracketed gap labelled zero available while all old Pods are killed before new ones are created, then a solid bar again; the RollingUpdate strategy shows an unbroken bar whose fill shifts from old to new through an overlapping middle region, never reaching zero"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Abstract availability timelines; strategy names are factual API values, no vendor IP depicted."
```

---

## Figure: ch06-fig05-statefulset-vs-deployment-identity

**Anchor ID:** `ch06-fig05-statefulset-vs-deployment-identity`
**Draft caption:** Figure 6.4 — the storage belongs to the identity, not to the Pod *(see flag F2 — anchor number and caption number disagree)*
**Purpose:** Replaces the "writes to disk → StatefulSet" misconception with the correct criterion by showing that what survives a StatefulSet Pod's death is a *named slot* with storage attached to it, not the Pod.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel comparative component diagram with replacement flow

**Content specification:**
Two stacked panels, each with a heading. The upper panel is headed "Deployment — Pods are interchangeable" and shows three Pod boxes in a row, labeled with hash-suffixed generated names: `web-7d4b-x9k2`, `web-7d4b-mn4p`, `web-7d4b-qq81`. The middle Pod carries a "✗ dies" mark; an arrow drops from it and turns right to a fourth Pod box labeled `web-7d4b-z7rt`, annotated with two lines: "new name, new UID." and "Nothing depended on which one it was." No storage appears in this panel at all. The lower panel is headed "StatefulSet — identity is sticky, and the storage belongs to the identity" and shows three Pod boxes labeled `db-0`, `db-1`, `db-2` in a row, each with a short connector dropping to its own storage element labeled `vol db-0`, `vol db-1`, `vol db-2` respectively. The `db-0` Pod carries a "✗ dies" mark; a return arrow curves from it back up to the same `db-0` position, annotated "db-0 reattaches here", "same name, same volume." and "The identity outlived the Pod." The point of the figure is the contrast between the two arrows: in the upper panel the arrow ends somewhere *new*, in the lower panel it ends *where it started*. Draw the storage as attached to the labeled slot position, not nested inside the Pod box.

**Visual style:**
- Palette: inherit book default; Pod boxes navy outline, storage elements drawn as a distinct shape (cylinder or open-topped rectangle) in slate
- Size (pixels): 1000x900 portrait
- Font: inherit book default — Fira Mono for all Pod and volume names, Fira Sans for headings and annotations
- Accent color for highlighted elements: Brass #B58B3E on the lower panel's reattachment arrow and the `db-0` ↔ `vol db-0` link

**Critical details (non-negotiable accuracy):**
- StatefulSet ordinals are **zero-indexed**: `db-0`, `db-1`, `db-2`. Never `db-1` through `db-3`.
- The replacement in the upper panel has a **different** name (`web-7d4b-z7rt` ≠ `web-7d4b-mn4p`). The replacement in the lower panel has the **same** name (`db-0`). This asymmetry is the entire figure.
- The volume must be drawn attached to the **identity slot**, positioned so it is visibly outside the Pod box. If the volume is drawn inside the Pod, the figure asserts the opposite of what the caption claims.
- Each `db-N` has exactly **one** volume, and volumes are not shared between members. Do not draw a single shared store.
- **Do not introduce PersistentVolumeClaim, PersistentVolume or StorageClass terminology into the render.** The labels stay `vol db-0` etc. Those terms are not introduced until Chapter 11, and the draft explicitly defers them.
- No storage element appears in the Deployment panel. Deployment Pods can mount volumes — the prose says so — but drawing one here would blunt the contrast the figure exists to make.
- The lower panel's arrow returns to the **same position** it left. Do not route it to a fourth slot.

**Source ASCII (for designer reference):**
```
  Deployment — Pods are interchangeable

     web-7d4b-x9k2      web-7d4b-mn4p      web-7d4b-qq81
                             ✗ dies
                               │
                               └──▶  web-7d4b-z7rt
                                     new name, new UID.
                                     Nothing depended on which one it was.


  StatefulSet — identity is sticky, and the storage belongs to the identity

     db-0 ──┐           db-1 ──┐           db-2 ──┐
            │                  │                  │
        [ vol db-0 ]       [ vol db-1 ]       [ vol db-2 ]
       ✗ dies  ▲
         │     │
         └──▶ db-0 reattaches here
              same name, same volume.
              The identity outlived the Pod.
```

**Proposed filename:** `ch06-fig05-statefulset-vs-deployment-identity.png`

```yaml-figure-spec
anchor_id: ch06-fig05-statefulset-vs-deployment-identity
diagram_type: component_diagram
source_ascii: |2
    Deployment — Pods are interchangeable

       web-7d4b-x9k2      web-7d4b-mn4p      web-7d4b-qq81
                               ✗ dies
                                 │
                                 └──▶  web-7d4b-z7rt
                                       new name, new UID.
                                       Nothing depended on which one it was.


    StatefulSet — identity is sticky, and the storage belongs to the identity

       db-0 ──┐           db-1 ──┐           db-2 ──┐
              │                  │                  │
          [ vol db-0 ]       [ vol db-1 ]       [ vol db-2 ]
         ✗ dies  ▲
           │     │
           └──▶ db-0 reattaches here
                same name, same volume.
                The identity outlived the Pod.
vendor_terms: [Deployment, StatefulSet, Pod]
complexity_hint:
  node_count: 11
  edge_count: 5
  label_count: 18
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Distinguish a StatefulSet from a Deployment by whether the Pods are interchangeable, not by whether the application writes to disk"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The reattachment arrow returning db-0 to its own volume, showing the identity outlived the Pod"
accessibility:
  alt_text_seed: "Two-panel comparison: in the Deployment panel three hash-named Pods sit side by side, one dies and is replaced by a Pod with a different name and UID, with no storage shown; in the StatefulSet panel three Pods named db-0, db-1 and db-2 each attach to their own volume, and when db-0 dies the replacement takes the same name and reattaches to the same volume"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original redrawing of documented StatefulSet identity semantics; no CNCF logo, icon or artwork reproduced."
```

---

## Figure: ch06-fig04-workload-resource-decision-tree

**Anchor ID:** `ch06-fig04-workload-resource-decision-tree`
**Draft caption:** Figure 6.5 — ask about the work before you ask about the application *(see flag F2 — anchor number and caption number disagree)*
**Purpose:** Collapses all three of the chapter's resource-selection misconceptions into one traversable decision, by putting the questions about the *shape of the work* ahead of any question about the software.
**Replaces ASCII:** yes
**Mandatory:** yes — the Exam Alert names this "the single highest-value artifact in this chapter"
**Type:** binary decision tree, top-down, four decision nodes and five terminal nodes

**Content specification:**
A top-down binary tree. The root decision node reads "Does the work END?" and branches left on "yes", right on "no". The left "yes" branch leads to a decision node reading "Does it repeat on a schedule?", which branches left on "yes" to the terminal `CronJob` and right on "no" to the terminal `Job`. The right "no" branch from the root leads to a decision node reading "Must it run on EVERY node?", which branches left on "yes" to the terminal `DaemonSet` and right on "no" to a fourth decision node reading "Are the Pods INTERCHANGEABLE?". That node branches left on "yes" to the terminal `Deployment`, annotated in smaller type "(which manages a ReplicaSet)", and right on "no" to the terminal `StatefulSet`. Every edge carries an explicit "yes" or "no" label. Decision nodes and terminal nodes must be visually distinct in shape — for example diamonds or rounded rectangles for questions and plain rectangles for resources — so a reader scanning the figure without reading it can see how many decisions there are. The point of the figure is the *ordering* of the four questions, so the depth of the tree must be visible; do not flatten it into a table or a two-column list.

**Visual style:**
- Palette: inherit book default; decision nodes slate outline, terminal resource nodes navy outline with heavier weight
- Size (pixels): 1200x760 landscape
- Font: inherit book default — Fira Mono for the five resource names, Fira Sans for the questions and branch labels
- Accent color for highlighted elements: Brass #B58B3E on the root node "Does the work END?"

**Critical details (non-negotiable accuracy):**
- The question order is **END → schedule → every node → interchangeable**. Reordering the tree breaks the pedagogical claim stated in the caption and in the Navigational Hazards block that follows it.
- The root question is about the **work**, not the application. Do not soften it to "Is it a long-running service?" or similar.
- `CronJob` sits on the "yes" branch of the schedule question and `Job` on the "no" branch. `CronJob` is not a child of `Job`.
- `Deployment` carries the annotation "(which manages a ReplicaSet)". **`ReplicaSet` is not a terminal option** in this tree and must not appear as a selectable leaf.
- `StatefulSet` is the **"no"** answer to interchangeable. `Deployment` is the "yes".
- Exactly five terminal resources: CronJob, Job, DaemonSet, Deployment, StatefulSet. No sixth leaf.
- Every edge is labeled "yes" or "no" explicitly; branch position alone is not sufficient for accessibility.
- The words END, EVERY and INTERCHANGEABLE are emphasized in the source and should carry typographic emphasis (weight or small caps) in the render — they are the discriminating words.

**Source ASCII (for designer reference):**
```
                        Does the work END?
                    ┌──────────┴──────────┐
                  yes                     no
                   │                       │
        Does it repeat on          Must it run on
          a schedule?               EVERY node?
        ┌─────┴─────┐              ┌─────┴─────┐
      yes           no           yes           no
       │             │            │             │
   CronJob         Job        DaemonSet   Are the Pods
                                          INTERCHANGEABLE?
                                          ┌─────┴─────┐
                                        yes           no
                                         │             │
                                    Deployment    StatefulSet
                                  (which manages
                                   a ReplicaSet)
```

**Proposed filename:** `ch06-fig04-workload-resource-decision-tree.png`

```yaml-figure-spec
anchor_id: ch06-fig04-workload-resource-decision-tree
diagram_type: flowchart
source_ascii: |2
                          Does the work END?
                      ┌──────────┴──────────┐
                    yes                     no
                     │                       │
          Does it repeat on          Must it run on
            a schedule?               EVERY node?
          ┌─────┴─────┐              ┌─────┴─────┐
        yes           no           yes           no
         │             │            │             │
     CronJob         Job        DaemonSet   Are the Pods
                                            INTERCHANGEABLE?
                                            ┌─────┴─────┐
                                          yes           no
                                           │             │
                                      Deployment    StatefulSet
                                    (which manages
                                     a ReplicaSet)
vendor_terms: [Deployment, StatefulSet, DaemonSet, Job, CronJob, ReplicaSet]
complexity_hint:
  node_count: 9
  edge_count: 8
  label_count: 18
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, fixed_point, vendor_taxonomy]
  learning_outcome: "Pick the correct workload resource by asking about the shape of the work before asking about the nature of the application"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The root decision node 'Does the work END?', whose position ahead of every other question is the figure's argument"
accessibility:
  alt_text_seed: "Decision tree for choosing a Kubernetes workload resource: if the work ends, ask whether it repeats on a schedule, giving CronJob for yes and Job for no; if the work does not end, ask whether it must run on every node, giving DaemonSet for yes, and otherwise ask whether the Pods are interchangeable, giving Deployment for yes and StatefulSet for no"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original decision aid over documented Kubernetes workload taxonomy; no CNCF logo, icon or artwork reproduced."
```

---

## Figure: ch06-zenith-control-loop-instantiated

**Anchor ID:** `ch06-zenith-control-loop-instantiated` *(non-conforming — see flag F1; preserved verbatim as the join key)*
**Draft caption:** Figure 6.6 — one loop, six desired states
**Purpose:** Delivers the chapter's ☀️ Zenith by drawing the control loop exactly once and showing that all six resources differ only in what is plugged into "desired state" — the recognition Chapter 15 depends on.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** cyclic flow diagram with an attached substitution table

**Content specification:**
Two vertically stacked components in a single canvas. The upper component is a control loop drawn **once**: a box labeled "DESIRED STATE" at the top, an arrow down labeled "compare", a box labeled "CURRENT STATE" below it, an arrow down labeled "act on the gap", and a return path that curves back up to DESIRED STATE, labeled "(and again, forever)". "compare" and "act on the gap" are edge labels, not boxes. The lower component is a two-column substitution list under the heading "Change only what you plug into DESIRED STATE, and you have named every controller in this chapter:". The left column holds the desired state and the right column the controller, in this exact order: "a number" → `ReplicaSet`; "a template + an update policy" → `Deployment`; "one per matching node" → `DaemonSet`; "completion" → `Job`; "a Job existing at each scheduled time" → `CronJob`; "whatever its author decided" → "your operator". The two columns are joined by leader dots or a light rule so each pairing is unambiguous. A visual connection — a bracket, a thin rule, or a callout line — should run from the DESIRED STATE box down to the left column of the list, making it explicit that the list is what gets substituted into that one box. The point of the figure is the singularity of the loop: it is drawn once and only once, and the caption says so.

**Visual style:**
- Palette: inherit book default; loop in navy, substitution list in slate
- Size (pixels): 900x900 portrait
- Font: inherit book default — Fira Mono for the six controller names in the right column, Fira Sans for the loop labels and left column
- Accent color for highlighted elements: Brass #B58B3E on the return arrow and its "(and again, forever)" label

**Critical details (non-negotiable accuracy):**
- The loop is drawn **once**. Do not render six loops, six variants, or a small-multiples grid. A render that repeats the loop per resource asserts the exact opposite of the Zenith.
- The cycle must close — the return path goes from the act-on-the-gap step back to DESIRED STATE, not to a terminal node.
- "compare" and "act on the gap" are labels **on the arrows**, not process boxes. Promoting them to boxes turns a two-state loop into a four-step pipeline and loses the desired/current pairing.
- All six substitution rows are required, in the order given. The sixth, "your operator", is the payoff and must not be dropped as an outlier.
- `ReplicaSet` — not `Deployment` — is paired with "a number". `Deployment` is paired with the template-plus-policy row.
- The substitution list is **part of the figure**, inside the frame. It is not caption text and must not be demoted to a table beneath the image, because the visual link from the DESIRED STATE box to the list is what carries the argument.
- No arrow, box or annotation may be added to accommodate any particular controller. The prose states that nothing was added to the loop for any of them, and the figure must be able to survive that claim.

**Source ASCII (for designer reference):**
```
                    ┌───────────────────────────┐
                    │      DESIRED STATE        │
                    └─────────────┬─────────────┘
                                  │
                               compare
                                  │
                    ┌─────────────▼─────────────┐
                    │      CURRENT STATE        │
                    └─────────────┬─────────────┘
                                  │
                          act on the gap
                                  │
                                  └──────▶ (and again, forever)


   Change only what you plug into DESIRED STATE, and you have
   named every controller in this chapter:

        a number ............................  ReplicaSet
        a template + an update policy .......  Deployment
        one per matching node ...............  DaemonSet
        completion ..........................  Job
        a Job existing at each scheduled time  CronJob
        whatever its author decided .........  your operator
```

**Proposed filename:** `ch06-zenith-control-loop-instantiated.png`

```yaml-figure-spec
anchor_id: ch06-zenith-control-loop-instantiated
diagram_type: flowchart
source_ascii: |2
                      ┌───────────────────────────┐
                      │      DESIRED STATE        │
                      └─────────────┬─────────────┘
                                    │
                                 compare
                                    │
                      ┌─────────────▼─────────────┐
                      │      CURRENT STATE        │
                      └─────────────┬─────────────┘
                                    │
                            act on the gap
                                    │
                                    └──────▶ (and again, forever)


     Change only what you plug into DESIRED STATE, and you have
     named every controller in this chapter:

          a number ............................  ReplicaSet
          a template + an update policy .......  Deployment
          one per matching node ...............  DaemonSet
          completion ..........................  Job
          a Job existing at each scheduled time  CronJob
          whatever its author decided .........  your operator
vendor_terms: [ReplicaSet, Deployment, DaemonSet, Job, CronJob]
complexity_hint:
  node_count: 2
  edge_count: 3
  label_count: 14
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure, vendor_taxonomy]
  learning_outcome: "Recognize that all six workload controllers are one control loop differing only in desired state, which is the precursor to Chapter 15's GitOps synthesis"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The return arrow closing the cycle, labelled 'and again, forever'"
accessibility:
  alt_text_seed: "A single control loop drawn once: a desired state box compares down to a current state box, an act-on-the-gap step follows, and an arrow returns to the desired state forever; beneath it a substitution list pairs six desired states with their controllers — a number with ReplicaSet, a template plus update policy with Deployment, one per matching node with DaemonSet, completion with Job, a Job at each scheduled time with CronJob, and whatever its author decided with your operator"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original synthesis diagram over documented controller semantics; no CNCF logo, icon or artwork reproduced."
```
# Image Specifications — KCNA Chapter 8

*Generated from `draft-v2.md` (draft-voice.md does not exist at this stage; all line citations are against `.pipeline-state/ch-08/draft-v2.md`). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Figure count:** 6 anchors, 6 fenced ASCII blocks, 6 entries. Every fenced block in the file is anchored.

---

## UNANCHORED DIAGRAMS

**None.** The draft contains exactly six fenced code blocks (L148–161, L266–274, L349–363, L470–482, L706–719, L891–904), and each is immediately preceded by a `<!-- FIGURE: ... -->` anchor comment. No ASCII diagram is orphaned.

---

## ANCHOR ANOMALIES — author to resolve before commissioning

Flagged per Rule 4. **No anchor is renamed in this document** (Rule 6); all six are preserved verbatim as the join key.

### 1. Non-conforming anchor form: `ch08-zenith-consequences-not-rules` (L890)

The anchor carries no `figMM` segment, so it does not match Rule 4's `ch{NN}-fig{MM}-{kebab-slug}` form. It *is* valid against `structural-contract.yaml`'s `anchor_id_pattern`, which accepts `ch\d{2}-(fig\d{2}|zenith)-[a-z0-9-]+`, so the structural linter passes it and no lint failure will surface. Flagged here because the two rule sets disagree, and because the caption reads "Figure 8.6" — a figure number the anchor does not carry.

**Recommendation:** either reconcile Rule 4 in `10_image_spec_extraction.md` to match the contract's zenith exemption, or renumber the anchor to `ch08-fig06-consequences-not-rules`. This document assumes the anchor stands.

### 2. Anchor fig numbers are not in draft order

| Draft order | Anchor | Caption | Line |
|---|---|---|---|
| 1st | `ch08-fig01-kubectl-verb-resource-grammar` | Figure 8.1 | 147 |
| 2nd | `ch08-fig02-three-api-gates` | Figure 8.2 | 265 |
| 3rd | **`ch08-fig05`**`-quota-vs-limitrange` | **Figure 8.3** | 348 |
| 4th | `ch08-fig04-node-lifecycle-cordon-drain` | Figure 8.4 | 469 |
| 5th | **`ch08-fig03`**`-version-skew-window` | **Figure 8.5** | 705 |
| 6th | `ch08-zenith-consequences-not-rules` | Figure 8.6 | 890 |

`fig05` and `fig03` are transposed relative to their captions. Nothing breaks — the anchor is the join key and the caption is the reader-facing label — but a designer reading filenames will build `ch08-fig03-version-skew-window.png` and find it captioned "Figure 8.5", which is a live source of misfiling during figure review.

**Recommendation:** renumber to draft order in **one sweep across draft and image-specs together**, before any figure is commissioned. Do not renumber one file alone; the anchors are the only join and a half-sweep silently orphans figures. The draft's own author-review note at L907 records the same recommendation.

---

## Figure: ch08-fig01-kubectl-verb-resource-grammar

**Anchor ID:** `ch08-fig01-kubectl-verb-resource-grammar`
**Draft location:** L147–161 (anchor L147, block L148–161, caption L163)
**Purpose:** Show that five commands the reader has already run share one four-slot grammar, and make the case-sensitivity asymmetry between TYPE and NAME visually unmissable — the examinable half of §1.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** annotated syntax table (column-aligned grid with two callout pointers)

**Content specification:**

A five-column grid with a header row reading, left to right: `kubectl`, `[command]`, `[TYPE]`, `[NAME]`, `[flags]`. Each of the four bracketed slot labels sits above a short horizontal rule; the leading `kubectl` label does not (it is fixed, not a slot). Below the header sit five data rows, each a real command decomposed into those columns, with **empty cells left visibly empty** — the emptiness is the teaching point and must not be filled with dashes, ditto marks, or "n/a":

| row | command | TYPE | NAME | flags |
|---|---|---|---|---|
| 1 | `cordon` | *(empty)* | `node-7` | *(empty)* |
| 2 | `get` | `pods` | *(empty)* | *(empty)* |
| 3 | `apply` | *(empty)* | *(empty)* | `-f deploy.yaml` |
| 4 | `scale` | `deployment` | `web` | `--replicas=5` |
| 5 | `describe` | `node` | `worker-3` | *(empty)* |

Beneath the grid, two upward-pointing arrows rise from the TYPE column and the NAME column respectively. The TYPE arrow is annotated over two lines: `case-INsensitive` / `pod = pods = po`. The NAME arrow is annotated over two lines: `case-SENSITIVE` / `node-7 ≠ Node-7`. Render the `IN` of "case-INsensitive" and the `SENSITIVE` of "case-SENSITIVE" in the emphasis treatment used for the accent (small caps or bold in the accent colour) so the opposition reads at a glance. The two annotation blocks must be visually paired and adjacent — they are one contrast, not two facts. All command tokens, resource types, resource names and flags are set in the monospace face; the annotation text is set in the body face.

**Visual style:**
- Palette: inherit book default (Lodestar navy on cream; brass accent)
- Size (pixels): 1200x800 landscape
- Font: inherit book default — Fira Mono for all command tokens, Fira Sans for annotations, Roboto Slab for the slot labels
- Accent color for highlighted elements: Brass `#B58B3E` on the two case-sensitivity annotations and their arrows only

**Critical details (non-negotiable accuracy):**
- Slot order is `kubectl` → command → TYPE → NAME → flags. Never reorder; the whole figure is about position.
- Row 1 (`cordon node-7`) has **no TYPE**. Row 3 (`apply -f deploy.yaml`) has **no TYPE and no NAME**. These gaps are load-bearing and the caption points at them explicitly.
- The asymmetry must not be flattened: TYPE is case-**in**sensitive, NAME is case-**sensitive**. Reversing this teaches the exam's most common distractor (Practice Q1 option C).
- `node-7 ≠ Node-7` must use a real not-equals glyph, not `!=`, and must not be "corrected" to an equals sign by a well-meaning designer.
- `pod = pods = po` shows singular / plural / abbreviated. Keep all three forms.
- Do not add slots. There are four, and NAME and flags are the optional two.

**Source ASCII (for designer reference):**
```
  kubectl   [command]        [TYPE]        [NAME]      [flags]
            ─────────        ──────        ──────      ───────

  kubectl   cordon                         node-7
  kubectl   get              pods
  kubectl   apply                                      -f deploy.yaml
  kubectl   scale            deployment    web         --replicas=5
  kubectl   describe         node          worker-3

                                ▲             ▲
                    case-INsensitive     case-SENSITIVE
                    pod = pods = po      node-7 ≠ Node-7
```

**Proposed filename:** `ch08-fig01-kubectl-verb-resource-grammar.png`

```yaml-figure-spec
anchor_id: ch08-fig01-kubectl-verb-resource-grammar
diagram_type: other
source_ascii: |
    kubectl   [command]        [TYPE]        [NAME]      [flags]
              ─────────        ──────        ──────      ───────

    kubectl   cordon                         node-7
    kubectl   get              pods
    kubectl   apply                                      -f deploy.yaml
    kubectl   scale            deployment    web         --replicas=5
    kubectl   describe         node          worker-3

                                  ▲             ▲
                      case-INsensitive     case-SENSITIVE
                      pod = pods = po      node-7 ≠ Node-7
vendor_terms: [kubectl]
complexity_hint:
  node_count: 25
  edge_count: 2
  label_count: 27
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Decompose any kubectl command into its four slots, and state which slots are case-sensitive"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The paired annotations under the TYPE and NAME columns: case-INsensitive versus case-SENSITIVE"
accessibility:
  alt_text_seed: "A five-column table aligning five kubectl commands on the slots kubectl, command, TYPE, NAME and flags; some cells are empty because those commands omit those slots; two arrows below point up at the TYPE column labelled case-insensitive and the NAME column labelled case-sensitive"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes command syntax redrawn as an original alignment grid; no vendor artwork or icons reproduced."
```

---

## Figure: ch08-fig02-three-api-gates

**Anchor ID:** `ch08-fig02-three-api-gates`
**Draft location:** L265–274 (anchor L265, block L266–274, caption L276)
**Purpose:** Show the three access-control gates as an ordered pipeline and make gate three's unique second exit — rewriting the request rather than refusing it — the visually dominant feature.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** horizontal flow diagram with branch exits

**Content specification:**

A left-to-right pipeline of three boxes of equal size, labelled in order **Authentication**, **Authorization**, **Admission**, each with a small superscript-style header above it reading `gate 1`, `gate 2`, `gate 3`. An arrow enters gate 1 from the left, labelled `request`. Arrows connect gate 1 → gate 2 → gate 3. An arrow exits gate 3 to the right, terminating at a label reading `persisted to etcd`.

Each of the three gates drops a **downward** arrow to a terminal label reading `REJECT`. Three REJECT terminals, one per gate, all on the same baseline, all identical in treatment — they are the same outcome three times.

Gate 3 alone drops a **second** exit. This one does not terminate: it is a return path, routed below the pipeline and curving back up to rejoin the flow between gate 3 and the `persisted to etcd` terminal, labelled `REWRITTEN`. This is the single element the whole figure exists for. It must be the visually heaviest line in the diagram — thicker stroke, accent colour, and clearly a *loop back into the forward path* rather than a fourth exit off the side. A reader who glances at this figure for two seconds should come away with "the third box has an extra arrow that goes back in."

Do not add a mutating/validating phase split inside gate 3, do not add webhook boxes, and do not add a read path. Gate three is one box.

**Visual style:**
- Palette: inherit book default (Lodestar navy on cream; brass accent)
- Size (pixels): 1200x700 landscape
- Font: inherit book default — Roboto Slab for gate names, Fira Sans for arrow labels
- Accent color for highlighted elements: Brass `#B58B3E` for the REWRITTEN return path and its label; the three REJECT arrows stay in a muted neutral so they recede

**Critical details (non-negotiable accuracy):**
- Order is **Authentication → Authorization → Admission**. Never reordered; the order is Exam Alert priority topic #1 and Practice Q2's entire content.
- All three gates can REJECT. Only gate three can REWRITE. Giving the rewrite power to any other gate reproduces Practice Q2's distractor B.
- The REWRITTEN path rejoins the *forward* flow. It must not read as an exit, a retry, or a return to the client.
- The terminal is `persisted to etcd` — the write happens *after* gate three, not before or between.
- Three gates, not two and not four. Auditing is discussed adjacently in the prose but is **not** a gate and must not appear as a fourth box.

**Source ASCII (for designer reference):**
```
                gate 1              gate 2              gate 3
           ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
 request ─►│Authentication├──►│Authorization ├──►│  Admission   ├──► persisted
           └──────┬───────┘   └──────┬───────┘   └──┬───────┬───┘     to etcd
                  │                  │             │       │              ▲
                  ▼                  ▼             ▼       │              │
               REJECT             REJECT        REJECT     └── REWRITTEN ─┘
```

**Proposed filename:** `ch08-fig02-three-api-gates.png`

```yaml-figure-spec
anchor_id: ch08-fig02-three-api-gates
diagram_type: flowchart
source_ascii: |3
                  gate 1              gate 2              gate 3
             ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
   request ─►│Authentication├──►│Authorization ├──►│  Admission   ├──► persisted
             └──────┬───────┘   └──────┬───────┘   └──┬───────┬───┘     to etcd
                    │                  │             │       │              ▲
                    ▼                  ▼             ▼       │              │
                 REJECT             REJECT        REJECT     └── REWRITTEN ─┘
vendor_terms: [etcd, kube-apiserver]
complexity_hint:
  node_count: 8
  edge_count: 8
  label_count: 11
pedagogy:
  part_18_criteria_met: [temporal_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Trace a request through authentication, authorization and admission in order, and identify admission as the only gate that can modify the request"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The REWRITTEN return path from gate three that rejoins the forward flow"
accessibility:
  alt_text_seed: "Three boxes in a row labelled Authentication, Authorization and Admission, with a request arrow entering on the left and persistence to etcd on the right; each box has a downward arrow to a REJECT outcome, and the Admission box has an additional arrow labelled REWRITTEN that loops back into the forward path"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original depiction of the documented API access-control sequence; no vendor artwork reproduced."
```

---

## Figure: ch08-fig05-quota-vs-limitrange

**Anchor ID:** `ch08-fig05-quota-vs-limitrange` *(captioned "Figure 8.3" in the draft — see ANCHOR ANOMALIES above)*
**Draft location:** L348–363 (anchor L348, block L349–363, caption L365)
**Purpose:** Make the ResourceQuota/LimitRange discrimination structural rather than verbal — one draws a boundary around a namespace, the other does not — and prove the difference by showing the two mechanisms failing differently on the same arriving Pod.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** side-by-side comparison, containment versus per-object constraint

**Content specification:**

Two panels of equal width, side by side, under headers **ResourceQuota** (left) and **LimitRange** (right).

*Left panel.* A single large bordered container labelled `namespace: team-atlas`. Inside it sit four small boxes each labelled `Pod`, in a row. Below the four Pods, still inside the container, two stacked horizontal bars: the upper reads `namespace total`, the lower reads `AT CAP`. The container border is the point — the constraint has a boundary and the Pods are inside it. Beneath the panel, an upward arrow with a three-line annotation: `5th Pod arrives:` / `REJECTED` / `the namespace total is reached`.

*Right panel.* **No container, and this absence must be conspicuous.** Directly under the LimitRange header, set the parenthetical `(no namespace boundary)` in the position where the left panel's container border would be — the reader must register a deliberate absence, not an omission. Four independent Pod boxes sit in a row with nothing enclosing them. Each Pod box carries its own two-line internal constraint reading `min ≤` / `≤ max` — the constraint is *inside each object*, which is the entire structural contrast. Beneath the panel, an upward arrow with a three-line annotation: `5th Pod arrives declaring nothing:` / `ACCEPTED — with` / `defaults FILLED IN`.

The two outcome words — `REJECTED` and `ACCEPTED` — must be typographically parallel and equally weighted so the reader compares them directly. Keep the two panels on a shared baseline so the four Pods on the left align horizontally with the four Pods on the right; the only difference the eye should find between the two Pod rows is the presence or absence of the surrounding boundary.

**Visual style:**
- Palette: inherit book default (Lodestar navy on cream; brass accent)
- Size (pixels): 1200x900 landscape
- Font: inherit book default — Roboto Slab for panel headers, Fira Mono for `namespace: team-atlas` and `min ≤ ≤ max`, Fira Sans for outcome annotations
- Accent color for highlighted elements: Brass `#B58B3E` on the left panel's namespace container border and on both outcome labels (`REJECTED`, `ACCEPTED — with defaults FILLED IN`)

**Critical details (non-negotiable accuracy):**
- **The namespace boundary appears on the LEFT panel only.** Drawing a boundary on the right destroys the figure; the absence *is* the content.
- The quota is an **aggregate ceiling on the namespace**. It must never be depicted as a per-Pod bound.
- The LimitRange constraint sits **inside each individual Pod**. It must never be depicted as a namespace-wide bar.
- Left outcome is refusal; right outcome is acceptance-with-modification. Swapping these reproduces Practice Q5's distractor A, the section's only real error.
- Four Pods per panel, with a fifth arriving in each. Keep the counts equal — the panels differ by mechanism, not by scale.
- Do not add quota scopes, scope selectors, priority-class quota, or a countable-resource roster. All are above associate tier and explicitly out of scope per the draft's §3 scope guard.

**Source ASCII (for designer reference):**
```
        ResourceQuota                          LimitRange
   ┌──────────────────────────┐          (no namespace boundary)
   │ namespace: team-atlas    │
   │  ┌────┐┌────┐┌────┐┌────┐│           ┌─────┐┌─────┐┌─────┐┌─────┐
   │  │Pod ││Pod ││Pod ││Pod ││           │ Pod ││ Pod ││ Pod ││ Pod │
   │  └────┘└────┘└────┘└────┘│           │min ≤││min ≤││min ≤││min ≤│
   │  ═══ namespace total ═══ │           │≤ max││≤ max││≤ max││≤ max│
   │  ═══════ AT CAP ════════ │           └─────┘└─────┘└─────┘└─────┘
   └──────────────────────────┘
             ▲                                       ▲
      5th Pod arrives:                    5th Pod arrives declaring
        REJECTED                          nothing:  ACCEPTED — with
   the namespace total is reached           defaults FILLED IN
```

**Proposed filename:** `ch08-fig05-quota-vs-limitrange.png`

```yaml-figure-spec
anchor_id: ch08-fig05-quota-vs-limitrange
diagram_type: component_diagram
source_ascii: |5
          ResourceQuota                          LimitRange
     ┌──────────────────────────┐          (no namespace boundary)
     │ namespace: team-atlas    │
     │  ┌────┐┌────┐┌────┐┌────┐│           ┌─────┐┌─────┐┌─────┐┌─────┐
     │  │Pod ││Pod ││Pod ││Pod ││           │ Pod ││ Pod ││ Pod ││ Pod │
     │  └────┘└────┘└────┘└────┘│           │min ≤││min ≤││min ≤││min ≤│
     │  ═══ namespace total ═══ │           │≤ max││≤ max││≤ max││≤ max│
     │  ═══════ AT CAP ════════ │           └─────┘└─────┘└─────┘└─────┘
     └──────────────────────────┘
               ▲                                       ▲
        5th Pod arrives:                    5th Pod arrives declaring
          REJECTED                          nothing:  ACCEPTED — with
     the namespace total is reached           defaults FILLED IN
vendor_terms: [ResourceQuota, LimitRange, Pod, namespace]
complexity_hint:
  node_count: 12
  edge_count: 2
  label_count: 14
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Distinguish ResourceQuota from LimitRange by scope — namespace aggregate versus individual object — and by failure mode"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The namespace boundary present on the left panel and conspicuously absent on the right"
accessibility:
  alt_text_seed: "Two panels compared side by side: on the left, four Pods enclosed in a bordered namespace box with a namespace total bar marked at cap, and a fifth arriving Pod rejected; on the right, four unenclosed Pods each carrying its own minimum and maximum bounds, and a fifth arriving Pod that declares nothing being accepted with defaults filled in"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original scope comparison of two Kubernetes API objects; no vendor artwork reproduced."
```

---

## Figure: ch08-fig04-node-lifecycle-cordon-drain

**Anchor ID:** `ch08-fig04-node-lifecycle-cordon-drain`
**Draft location:** L469–482 (anchor L469, block L470–482, caption L484)
**Purpose:** Defuse the chapter's most consequential confusion by showing that a cordoned node is not an empty node — the running Pods are pixel-identical between panels one and two, and the node does not empty until `drain`.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** four-panel state progression with labelled transitions

**Content specification:**

Four equal-sized node panels in a single left-to-right row, with state headers above them reading, in order: `SCHEDULABLE`, `CORDONED`, `DRAINED`, `SCHEDULABLE`. Transition arrows run between consecutive panels, labelled beneath the arrow: `cordon` (panel 1→2), `drain` (panel 2→3), `uncordon` (panel 3→4).

Panel 1 contains three small Pod tokens labelled `A`, `B`, `C`. **Panel 2 contains the same three Pod tokens, rendered identically** — same position, same size, same treatment, no fading, no dimming, no strikethrough, no greying. Any visual softening of A, B and C in panel 2 inverts the figure's entire meaning and must be treated as a correctness error, not a style choice. Panel 3 is empty and labelled `(empty)`. Panel 4 is empty.

Below the row, arriving-Pod annotations. Under panel 1: an upward arrow with the label `new Pod admitted`. Under panel 2: a cross/rejection mark (✗) with the label `new Pod turned away`. Under panel 4: an upward arrow with the label `new Pod admitted`. Panel 3 gets no arriving-Pod annotation. The contrast between the panel-1 arrow and the panel-2 cross is the only thing that changes across the cordon transition, and it should read that way.

Beneath the whole figure, set the two-line assertion as an integral part of the artwork, not as caption text: `A, B and C are UNCHANGED between panel 1 and panel 2.` / `They are still running. That is what cordon does and does not do.`

**Visual style:**
- Palette: inherit book default (Lodestar navy on cream; brass accent)
- Size (pixels): 1200x700 landscape
- Font: inherit book default — Roboto Slab for state headers, Fira Mono for `cordon` / `drain` / `uncordon`, Fira Sans for annotations
- Accent color for highlighted elements: Brass `#B58B3E` on the three Pod tokens A/B/C in **both** panel 1 and panel 2 (identical treatment in each), and on the panel-2 rejection cross

**Critical details (non-negotiable accuracy):**
- **Pods A, B and C must be visually identical in panels 1 and 2.** This is the single most important instruction in this document. `cordon` does not affect existing Pods; a designer's instinct to fade them is exactly the misconception the figure exists to kill.
- The node does not empty until `drain` (panel 3). Emptying at panel 2 reproduces Practice Q8's distractor C, the chapter's headline trap.
- Transition order is cordon → drain → uncordon. Reversing cordon and drain reproduces distractor A.
- The arriving Pod is turned away in panel 2 only. Panels 1 and 4 admit; panel 3 has no arrival shown.
- Panel 4 is empty — `uncordon` restores *schedulability*, it does not restore the evicted Pods.
- Do not depict the DaemonSet toleration exception here; it is prose in §4 and adding it muddies the four-panel line.

**Source ASCII (for designer reference):**
```
   SCHEDULABLE            CORDONED             DRAINED           SCHEDULABLE
  ┌────────────┐        ┌────────────┐      ┌────────────┐      ┌────────────┐
  │ [A][B][C]  │        │ [A][B][C]  │      │            │      │            │
  │            │──────► │            │─────►│  (empty)   │─────►│            │
  └────────────┘ cordon └────────────┘ drain└────────────┘uncord└────────────┘
        ▲                     ✗                                        ▲
     new Pod              new Pod                                   new Pod
     admitted            turned away                                admitted

        A, B and C are UNCHANGED between panel 1 and panel 2.
        They are still running. That is what cordon does and does not do.
```

**Proposed filename:** `ch08-fig04-node-lifecycle-cordon-drain.png`

```yaml-figure-spec
anchor_id: ch08-fig04-node-lifecycle-cordon-drain
diagram_type: state_machine
source_ascii: |4
     SCHEDULABLE            CORDONED             DRAINED           SCHEDULABLE
    ┌────────────┐        ┌────────────┐      ┌────────────┐      ┌────────────┐
    │ [A][B][C]  │        │ [A][B][C]  │      │            │      │            │
    │            │──────► │            │─────►│  (empty)   │─────►│            │
    └────────────┘ cordon └────────────┘ drain└────────────┘uncord└────────────┘
          ▲                     ✗                                        ▲
       new Pod              new Pod                                   new Pod
       admitted            turned away                                admitted

          A, B and C are UNCHANGED between panel 1 and panel 2.
          They are still running. That is what cordon does and does not do.
vendor_terms: [kubectl, Pod, Node]
complexity_hint:
  node_count: 10
  edge_count: 6
  label_count: 13
pedagogy:
  part_18_criteria_met: [temporal_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Predict what happens to the Pods on a node at each step of cordon, drain and uncordon"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "Pods A, B and C rendered identically in the SCHEDULABLE and CORDONED panels"
accessibility:
  alt_text_seed: "Four node panels in a row labelled schedulable, cordoned, drained and schedulable, connected by transitions labelled cordon, drain and uncordon; the same three Pods A, B and C appear unchanged in the first two panels and are gone from the third, while an arriving Pod is admitted in panels one and four and turned away in panel two"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original four-panel depiction of the documented node maintenance sequence; no vendor artwork reproduced."
```

---

## Figure: ch08-fig03-version-skew-window

**Anchor ID:** `ch08-fig03-version-skew-window` *(captioned "Figure 8.5" in the draft — see ANCHOR ANOMALIES above)*
**Draft location:** L705–719 (anchor L705, block L706–719, caption L721)
**Purpose:** Convert a five-row memorisation table into one picture whose shape carries the rule — every bar stops at the API server's version except one, and `kubectl` is the one that crosses.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** horizontal range chart on a relative minor-version axis

**Content specification:**

A horizontal axis running left to right with tick positions labelled `-3`, `-2`, `-1`, `0`, `+1`. Above the axis, a header spanning it reads `older ◄── kube-apiserver ──► newer`, with the words `older` and `newer` at the left and right extremes and `kube-apiserver` centred over the `0` tick. **The axis is deliberately relative — it carries no concrete version numbers, and none must be added.**

At the `0` tick, a **double vertical line** running the full height of the plot. This is the API server's own minor version and it functions as a wall. Render it heavier than the other four tick guides.

Six labelled horizontal bars, one per row, stacked in this order top to bottom with their labels flush left: `kubelet`, `kube-proxy`, `controller-manager`, `scheduler`, `cloud-ctrl-manager`, `kubectl`. Each bar has a filled round cap at its older end and a flat perpendicular terminator where it meets the wall.

- `kubelet` — spans `-3` to `0`.
- `kube-proxy` — spans `-3` to `0`.
- `controller-manager` — spans `-1` to `0`.
- `scheduler` — spans `-1` to `0`.
- `cloud-ctrl-manager` — spans `-1` to `0`.
- `kubectl` — spans `-1` through the wall to `+1`, with round caps at *both* ends. It is the only bar that penetrates the double line, and it must be drawn as passing *through* the wall rather than stopping at it and restarting.

Below the `kubectl` bar, an upward pointer annotated `the only bar that crosses`, aimed at the segment to the right of the wall.

The five API-server-bounded bars stack above `kubectl` and share a uniform muted treatment so that the wall reads as a hard edge across all five simultaneously. `kubectl` alone breaks the edge. If a reader takes one thing from this figure it should be the ragged left edge and the single flat right edge with one bar poking through it.

**Visual style:**
- Palette: inherit book default (Lodestar navy on cream; brass accent)
- Size (pixels): 1200x900 landscape
- Font: inherit book default — Fira Mono for the six component names, Fira Sans for axis labels and the annotation
- Accent color for highlighted elements: Brass `#B58B3E` for the `kubectl` bar and the "only bar that crosses" pointer; the `0` wall in a heavy neutral

**Critical details (non-negotiable accuracy):**
- kubelet and kube-proxy extend to **-3**. controller-manager, scheduler and cloud-controller-manager extend to **-1**. These are different numbers and must not be normalised to each other.
- **`kubectl` is the only bar crossing to the right of 0**, and it reaches only `+1`. Extending it further, or letting any other bar cross, destroys the section's central exception.
- `kubectl`'s left extent is `-1`, not `-3`. Its window is one minor in *both* directions — symmetric — which is what makes it the only symmetric bar in the chart.
- The axis carries **no concrete version numbers**. The prose is explicit that the current roster will have changed by the reader's exam date; putting 1.36 on the axis dates the figure and contradicts the caption.
- **The HA kube-apiserver rule is not a bar and must not be added as one.** It is a mutual bound between two API servers, not a bound relative to one, and the caption calls this out. A seventh bar here would be a factual error.
- Six bars exactly. Do not add etcd, the container runtime, or CNI plugins.

**Source ASCII (for designer reference):**
```
                  older ◄───────── kube-apiserver ─────────► newer
                    -3      -2      -1       0       +1
                     │       │       │       ║       │

  kubelet            ●━━━━━━━━━━━━━━━━━━━━━━━┫
  kube-proxy         ●━━━━━━━━━━━━━━━━━━━━━━━┫
  controller-manager                 ●━━━━━━━┫
  scheduler                          ●━━━━━━━┫
  cloud-ctrl-manager                 ●━━━━━━━┫
  kubectl                            ●━━━━━━━╬━━━━━━━●
                                             ║
                                    ▲ the only bar that crosses
```

**Proposed filename:** `ch08-fig03-version-skew-window.png`

```yaml-figure-spec
anchor_id: ch08-fig03-version-skew-window
diagram_type: other
source_ascii: |4
                    older ◄───────── kube-apiserver ─────────► newer
                      -3      -2      -1       0       +1
                       │       │       │       ║       │

    kubelet            ●━━━━━━━━━━━━━━━━━━━━━━━┫
    kube-proxy         ●━━━━━━━━━━━━━━━━━━━━━━━┫
    controller-manager                 ●━━━━━━━┫
    scheduler                          ●━━━━━━━┫
    cloud-ctrl-manager                 ●━━━━━━━┫
    kubectl                            ●━━━━━━━╬━━━━━━━●
                                               ║
                                      ▲ the only bar that crosses
vendor_terms: [kube-apiserver, kubelet, kube-proxy, kube-controller-manager, kube-scheduler, cloud-controller-manager, kubectl]
complexity_hint:
  node_count: 6
  edge_count: 6
  label_count: 13
pedagogy:
  part_18_criteria_met: [quantitative_relationships, distinguishing_alternatives, fixed_point]
  learning_outcome: "State which Kubernetes components may disagree about their version, by how much, and in which direction"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The kubectl bar, the only one crossing the double line to the right of the API server's version"
accessibility:
  alt_text_seed: "A horizontal range chart on a relative axis from minus three to plus one minor versions, with the API server's version marked by a double line at zero; bars for kubelet and kube-proxy reach back three versions, bars for the controller manager, scheduler and cloud controller manager reach back one, and all five stop at the double line, while the kubectl bar alone extends one version past it"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original chart rendering of the published version skew policy; no vendor artwork reproduced and no concrete release numbers shown."
```

---

## Figure: ch08-zenith-consequences-not-rules

**Anchor ID:** `ch08-zenith-consequences-not-rules` *(captioned "Figure 8.6" in the draft; non-conforming anchor form — see ANCHOR ANOMALIES above)*
**Draft location:** L890–904 (anchor L890, block L891–904, caption L906)
**Purpose:** Carry the chapter's ☀️ Zenith claim in one image — every administrative act is a write through one door, reconciled by a controller the reader already met — and show visually that no arrow reaches a controller directly.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hub-and-spoke convergence/divergence diagram

**Content specification:**

A three-zone composition. Left zone header: `administrative acts` with a subhead `(§1, §3, §4)`. Right zone header: `controllers you already met`. Between them, a single tall central box labelled across four stacked lines: `the` / `API` / `server`, with `ONE DOOR` set at its foot in a distinct heavier treatment.

Four arrows converge from the left into the central box, each labelled with an administrative act, top to bottom:
- `kubectl cordon`
- `kubectl apply -f quota.yaml`
- `kubectl apply -f deploy.yaml`
- `kubelet self-registration`

Four arrows diverge from the right of the central box, each terminating at a controller with its chapter attribution set in a lighter weight immediately after the name, top to bottom:
- `scheduler` `(Ch 7)`
- `node controller` `(Ch 4/8)`
- `workload controllers` `(Ch 6)`
- `the control loop` `(Ch 3)`

*(Note: the ASCII abbreviates this third label as `workload contrls` for column fit. **Set it in full as `workload controllers` in the rendered figure** — the abbreviation is an artefact of monospace width, not authorial intent.)*

From the bottom of the central box, a single downward arrow to a terminal labelled `etcd`.

The composition's argument is geometric: **every left-hand arrow terminates at the central box and nothing else.** No arrow may bypass the box, and no arrow may run diagonally from a left-hand act to a right-hand controller. A reader tracing any path with a finger must be forced through the door. Leave generous whitespace in the corridors above and below the box so the absence of side channels is legible as absence rather than as clutter.

The four chapter attributions on the right are the caption's stated payoff — the reader is meant to see that nothing on the right is new. Keep them aligned in their own column so they scan vertically as a list of chapters already read.

**Visual style:**
- Palette: inherit book default (Lodestar navy on cream; brass accent)
- Size (pixels): 1200x900 landscape
- Font: inherit book default — Roboto Slab for the central box and zone headers, Fira Mono for the four command labels, Fira Sans for controller names and chapter attributions
- Accent color for highlighted elements: Brass `#B58B3E` for the central box's border and the `ONE DOOR` label; arrows in navy; chapter attributions in a muted neutral

**Critical details (non-negotiable accuracy):**
- **No arrow bypasses the central box.** This is the figure's entire claim and Practice Q10's correct answer; a single diagonal shortcut refutes the chapter.
- Direction is left-to-right through the hub, then down to etcd. etcd sits *behind* the door, not beside it and not on the input side.
- `kubelet self-registration` belongs on the **left** with the administrative acts, not on the right with the controllers. §4's point is that a kubelet joining a cluster arrives at the same door an operator does.
- Chapter attributions are exact: scheduler = Ch 7, node controller = Ch 4/8, workload controllers = Ch 6, the control loop = Ch 3. These are the caption's payoff and a wrong number breaks the reader's back-reference.
- Four in, four out, one down. Do not add components; this is deliberately Chapter 3's architecture unchanged.
- Render `workload controllers` in full, not the ASCII's `workload contrls`.

**Source ASCII (for designer reference):**
```
  administrative acts                                 controllers you
  (§1, §3, §4)                    ┌───────────┐       already met
                                  │           │
  kubectl cordon ────────────►    │    the    │ ──►  scheduler            (Ch 7)
  kubectl apply -f quota.yaml ►   │    API    │ ──►  node controller    (Ch 4/8)
  kubectl apply -f deploy.yaml►   │  server   │ ──►  workload contrls    (Ch 6)
  kubelet self-registration ─►    │           │ ──►  the control loop     (Ch 3)
                                  │ ONE DOOR  │
                                  └─────┬─────┘
                                        │
                                        ▼
                                      etcd
```

**Proposed filename:** `ch08-zenith-consequences-not-rules.png`

```yaml-figure-spec
anchor_id: ch08-zenith-consequences-not-rules
diagram_type: k8s_architecture
source_ascii: |
    administrative acts                                 controllers you
    (§1, §3, §4)                    ┌───────────┐       already met
                                    │           │
    kubectl cordon ────────────►    │    the    │ ──►  scheduler            (Ch 7)
    kubectl apply -f quota.yaml ►   │    API    │ ──►  node controller    (Ch 4/8)
    kubectl apply -f deploy.yaml►   │  server   │ ──►  workload contrls    (Ch 6)
    kubelet self-registration ─►    │           │ ──►  the control loop     (Ch 3)
                                    │ ONE DOOR  │
                                    └─────┬─────┘
                                          │
                                          ▼
                                        etcd
vendor_terms: [kubectl, kube-apiserver, kubelet, kube-scheduler, etcd]
complexity_hint:
  node_count: 10
  edge_count: 9
  label_count: 15
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure]
  learning_outcome: "Recognise every administrative act in the chapter as a write through one door, reconciled by a controller already met"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The central ONE DOOR box that every arrow must pass through"
accessibility:
  alt_text_seed: "Four administrative actions on the left — kubectl cordon, applying a quota, applying a deployment, and kubelet self-registration — all converge on a single central box labelled the API server, one door; four arrows leave it to the scheduler from chapter seven, the node controller from chapters four and eight, the workload controllers from chapter six, and the control loop from chapter three, with a single arrow running down from the box to etcd"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original hub-and-spoke restatement of the documented hub-and-spoke API pattern; no vendor artwork or icons reproduced."
```
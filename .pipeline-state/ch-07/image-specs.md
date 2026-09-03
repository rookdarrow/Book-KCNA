# Image Specifications — KCNA Chapter 7

*Generated from the voiced draft (`.pipeline-state/ch-07/draft-v1.md`, voice pass applied 2026-08-24; `draft-v1-prevoice.md` preserved). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Anchors found:** 5 · **Entries below:** 5 · **Unanchored diagrams:** 0 · **Anchor-ID format exceptions:** 1

---

## ANCHOR ID FORMAT EXCEPTIONS

One anchor in the draft does not match the locked `ch{NN}-fig{MM}-{kebab-slug}` pattern:

| Line | Anchor as written | Issue |
|---|---|---|
| 838 | `ch07-zenith-berth-assignment` | Missing the `fig{MM}` segment. Reads as a marker-typed anchor (`zenith`) rather than a sequenced figure anchor. |

Per rule 6 the ID is **preserved unrenamed** in this document — it remains the join key as-is. Author decision required: if renamed, the natural value is `ch07-fig05-filter-or-score` and both the draft anchor and this file must change in the same commit. Until then the book-level aggregator will sort this figure out of sequence.

---

## UNANCHORED DIAGRAMS

None. Two bare fenced blocks in the draft carry no figure anchor and correctly should not — both are `kubectl` command listings, not diagrams:

- **~Line 332** — `kubectl get nodes --show-labels` / `kubectl label nodes …` (§3, node label commands)
- **~Line 426** — `kubectl taint nodes node1 …` and its trailing-minus removal form (§4, taint commands)

No action needed; recorded here so the structural audit's fence count reconciles (7 fenced blocks, 5 diagrams, 2 command listings).

---

## Figure: ch07-fig01-filter-score-bind

**Anchor ID:** `ch07-fig01-filter-score-bind`
**Purpose:** Establishes the scheduler's three-stage pipeline and — the harder half — shows that binding terminates at the API server, so the reader stops believing the scheduler starts containers.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** horizontal three-stage flow diagram in two bands, with a deliberately disconnected lower band

**Content specification:**
Draw a left-to-right process diagram in two horizontal bands separated by a dashed rule. In the top band, place a small box at upper-left headed `UNBOUND POD` containing the field name `spec.nodeName`, with the annotation *"(empty — this is what the scheduler watches for)"* set to its right in de-emphasised type; a short downward arrow runs from this box into the first stage. The three stage boxes are equal width, side by side, labelled `1. FILTER`, `2. SCORE`, `3. BIND`, joined left-to-right by two arrows. Inside FILTER, list five node rows — node-a keep, node-b drop, node-c keep, node-d drop, node-e keep — with the kept rows visually distinct from the dropped ones (weight or fill, not colour alone), and a footer line `= FEASIBLE SET`. Inside SCORE, list only the three survivors with their scores — node-a 72, node-c 91, node-e 68 — with node-c's 91 given the accent and the caption `highest wins` below. Inside BIND, stack `kube-scheduler` above `kube-apiserver` joined by a short downward arrow, with the quoted payload `"this Pod: node-c"` beneath. The lower band, under a dashed rule captioned *"separate actor, separate moment, separate arrow"*, holds one detached box containing `kubelet on node-c` with a downward arrow to `container runtime → containers`. The point of the figure is that the third arrow lands on the API server and that **no arrow crosses the dashed rule** — the gap is the teaching, so the two bands must read as visually separate systems rather than as a continuous four-stage flow.

**Visual style:**
- Palette: inherit book default — Navy `#0B1E3B` primary stroke, Teal `#1F4A4E` diagram accents, Cream `#F5EFE4` ground, Fog `#8A8D90` for the parenthetical and the dropped node rows
- Size (pixels): 1200x760 landscape
- Font: inherit book default (Fira Sans labels, Fira Mono for `spec.nodeName`, `kube-scheduler`, `kube-apiserver`, node names and scores)
- Accent color for highlighted elements: Brass `#B58B3E` on the `kube-scheduler → kube-apiserver` arrow and on node-c's score of 91

**Critical details (non-negotiable accuracy):**
- The bind arrow terminates at **`kube-apiserver`** — never at node-c, never at the kubelet. This is the single most reversible fact in the figure.
- **No arrow connects the lower band to the upper band.** The kubelet acts on a recorded decision it observed; it is not told. Adding a connector destroys the figure's purpose.
- The dropped nodes (node-b, node-d) must **not** appear in the SCORE box. Only the three feasible survivors are scored.
- Scores are 72 / 91 / 68 and node-c must hold the highest. Do not renumber.
- Stage order is FILTER → SCORE → BIND, left to right, never reordered — fig05 reuses this exact strip and the reader must recognise it.
- `spec.nodeName` is shown **empty**. Do not populate it.
- `kube-scheduler`, `kube-apiserver`, and `kubelet` are single lowercase tokens; do not title-case or space them.

**Source ASCII (for designer reference):**
```
   UNBOUND POD
   ┌───────────────┐
   │ spec.nodeName │   (empty — this is what the scheduler watches for)
   └───────┬───────┘
           │
           ▼
 ┌──────────────────┐    ┌──────────────────┐    ┌───────────────────────┐
 │  1. FILTER       │    │  2. SCORE        │    │  3. BIND              │
 │                  │    │                  │    │                       │
 │  node-a   keep   │    │  node-a ..... 72 │    │  kube-scheduler       │
 │  node-b   drop   │───▶│  node-c ..... 91 │───▶│         │             │
 │  node-c   keep   │    │  node-e ..... 68 │    │         ▼             │
 │  node-d   drop   │    │                  │    │  kube-apiserver       │
 │  node-e   keep   │    │  highest wins    │    │  "this Pod: node-c"   │
 │                  │    │                  │    │                       │
 │  = FEASIBLE SET  │    │                  │    │                       │
 └──────────────────┘    └──────────────────┘    └───────────────────────┘

     ─ ─ ─ ─ ─  separate actor, separate moment, separate arrow  ─ ─ ─ ─ ─

                     ┌────────────────────────────────────┐
                     │  kubelet on node-c                 │
                     │         │                          │
                     │         ▼                          │
                     │  container runtime → containers    │
                     └────────────────────────────────────┘
```

**Proposed filename:** `ch07-fig01-filter-score-bind.png`

```yaml-figure-spec
anchor_id: ch07-fig01-filter-score-bind
diagram_type: flowchart
source_ascii: |3
     UNBOUND POD
     ┌───────────────┐
     │ spec.nodeName │   (empty — this is what the scheduler watches for)
     └───────┬───────┘
             │
             ▼
   ┌──────────────────┐    ┌──────────────────┐    ┌───────────────────────┐
   │  1. FILTER       │    │  2. SCORE        │    │  3. BIND              │
   │                  │    │                  │    │                       │
   │  node-a   keep   │    │  node-a ..... 72 │    │  kube-scheduler       │
   │  node-b   drop   │───▶│  node-c ..... 91 │───▶│         │             │
   │  node-c   keep   │    │  node-e ..... 68 │    │         ▼             │
   │  node-d   drop   │    │                  │    │  kube-apiserver       │
   │  node-e   keep   │    │  highest wins    │    │  "this Pod: node-c"   │
   │                  │    │                  │    │                       │
   │  = FEASIBLE SET  │    │                  │    │                       │
   └──────────────────┘    └──────────────────┘    └───────────────────────┘

       ─ ─ ─ ─ ─  separate actor, separate moment, separate arrow  ─ ─ ─ ─ ─

                       ┌────────────────────────────────────┐
                       │  kubelet on node-c                 │
                       │         │                          │
                       │         ▼                          │
                       │  container runtime → containers    │
                       └────────────────────────────────────┘
vendor_terms: [kube-scheduler, kube-apiserver, kubelet, container-runtime]
complexity_hint:
  node_count: 8
  edge_count: 5
  label_count: 22
pedagogy:
  part_18_criteria_met: [spatial_structure, temporal_structure, fixed_point]
  learning_outcome: "Trace a Pod from creation to placement through filter, score, bind — and identify the kubelet, not the scheduler, as the component that starts containers"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the arrow from kube-scheduler to kube-apiserver inside the BIND stage"
accessibility:
  alt_text_seed: "Three-stage scheduler pipeline: FILTER keeps three of five nodes, SCORE ranks them with node-c highest at 91, BIND draws an arrow from kube-scheduler to kube-apiserver. A separate, unconnected panel below shows the kubelet on node-c starting containers."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original redraw of scheduler behaviour documented in the Kubernetes docs; no CNCF artwork or trade dress reproduced."
```

---

## Figure: ch07-fig02-nodeselector-vs-affinity

**Anchor ID:** `ch07-fig02-nodeselector-vs-affinity`
**Purpose:** Breaks the common misreading that node affinity is a single upgrade path from `nodeSelector`, by showing hardness and expressiveness as two independent axes with only one soft cell among six.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-by-three comparison matrix with a labelled horizontal axis

**Content specification:**
Draw a 2-row × 3-column grid of equal cells. Above the columns, run a horizontal arrow spanning the full grid width labelled `EXPRESSIVENESS`, arrowhead at the right. Column headers, left to right: `nodeSelector`, `required node affinity`, `preferred node affinity` (the second and third set on two lines as in the source). Row labels sit outside the grid on the left: top row `HARD` with the sub-label *"the rule must be met"*; bottom row `SOFT` with *"the rule is a wish"*. Populate exactly three of the six cells. Top-left: *"exact matches, all of them (implicit AND)"*, then a rule-line gap, then *"no match → no placement"*. Top-middle: the operator list *"In, NotIn, Exists, DoesNotExist, Gt, Lt"*, then *"no match → no placement"*. Bottom-right: *"same operators"*, then *"no match → placed anyway"*. The remaining three cells — top-right, bottom-left, bottom-middle — are rendered as visibly empty with a centred em-dash. Beneath the grid, a single caption line: *"Hardness and expressiveness are independent. Only ONE of the six cells is soft."* The two identical `no match → no placement` strings in the top row are the argument that `nodeSelector` and required affinity fail the same way; set them in identical type so the eye pairs them.

**Visual style:**
- Palette: inherit book default — Navy `#0B1E3B` cell borders and header type, Teal `#1F4A4E` for the expressiveness axis arrow, Cream `#F5EFE4` ground, Fog `#8A8D90` for the em-dashes in empty cells
- Size (pixels): 1100x620 landscape
- Font: inherit book default (Fira Sans for headers and prose, Fira Mono for `nodeSelector` and the six operator names)
- Accent color for highlighted elements: Brass `#B58B3E` on the bottom-right cell border and on `placed anyway`

**Critical details (non-negotiable accuracy):**
- Six cells; exactly **three** populated. The three empty cells must be drawn as present-and-empty, not omitted — the emptiness carries the argument that the axes are independent.
- The **only** soft cell is bottom-right (preferred node affinity). There is no soft `nodeSelector` and no soft required-affinity.
- The two HARD-row failure strings must stay word-identical: `no match → no placement`.
- Operator list is exactly six values with this capitalisation: `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt`. `nodeSelector`'s single implicit "equals" is not in this list.
- Expressiveness runs left → right; hardness is the vertical axis. Do not transpose the matrix.
- `nodeSelector` is one word, lower-camel. Do not render as "node selector".

**Source ASCII (for designer reference):**
```
                    EXPRESSIVENESS  ────────────────────────────────▶

                  nodeSelector          required node        preferred node
                                          affinity              affinity
               ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
    HARD       │ exact matches,   │  │ In, NotIn,       │  │                  │
    the rule   │ all of them      │  │ Exists,          │  │        —         │
    must be    │ (implicit AND)   │  │ DoesNotExist,    │  │                  │
    met        │                  │  │ Gt, Lt           │  │                  │
               │ no match →       │  │ no match →       │  │                  │
               │ no placement     │  │ no placement     │  │                  │
               └──────────────────┘  └──────────────────┘  └──────────────────┘
               ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
    SOFT       │                  │  │                  │  │ same operators   │
    the rule   │        —         │  │        —         │  │                  │
    is a wish  │                  │  │                  │  │ no match →       │
               │                  │  │                  │  │ placed anyway    │
               └──────────────────┘  └──────────────────┘  └──────────────────┘

    Hardness and expressiveness are independent. Only ONE of the six cells is soft.
```

**Proposed filename:** `ch07-fig02-nodeselector-vs-affinity.png`

```yaml-figure-spec
anchor_id: ch07-fig02-nodeselector-vs-affinity
diagram_type: other
source_ascii: |6
                      EXPRESSIVENESS  ────────────────────────────────▶

                    nodeSelector          required node        preferred node
                                            affinity              affinity
                 ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
      HARD       │ exact matches,   │  │ In, NotIn,       │  │                  │
      the rule   │ all of them      │  │ Exists,          │  │        —         │
      must be    │ (implicit AND)   │  │ DoesNotExist,    │  │                  │
      met        │                  │  │ Gt, Lt           │  │                  │
                 │ no match →       │  │ no match →       │  │                  │
                 │ no placement     │  │ no placement     │  │                  │
                 └──────────────────┘  └──────────────────┘  └──────────────────┘
                 ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
      SOFT       │                  │  │                  │  │ same operators   │
      the rule   │        —         │  │        —         │  │                  │
      is a wish  │                  │  │                  │  │ no match →       │
                 │                  │  │                  │  │ placed anyway    │
                 └──────────────────┘  └──────────────────┘  └──────────────────┘

      Hardness and expressiveness are independent. Only ONE of the six cells is soft.
vendor_terms: []
complexity_hint:
  node_count: 6
  edge_count: 1
  label_count: 13
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, fixed_point]
  learning_outcome: "Choose between nodeSelector, required node affinity, and preferred node affinity by treating hardness and expressiveness as two independent axes rather than one upgrade path"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the single soft cell — preferred node affinity, bottom-right"
accessibility:
  alt_text_seed: "A two-by-three matrix. Columns are nodeSelector, required node affinity, preferred node affinity, increasing in expressiveness. Rows are hard and soft. Only three cells are filled, and only the bottom-right preferred-affinity cell is soft."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original classification of documented Kubernetes API field behaviour; no vendor artwork involved."
```

---

## Figure: ch07-fig03-taints-tolerations-effects

**Anchor ID:** `ch07-fig03-taints-tolerations-effects`
**Purpose:** Fixes which object owns which half of the mechanism (taint on the node, toleration on the Pod) and isolates `NoExecute` as the only effect that reaches a Pod already running.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** composite — repulsion schematic above a three-by-three outcome matrix

**Content specification:**
Two stacked halves in one figure. **Upper half:** a wide box spanning the figure labelled `NODE`, containing the line `taint:  key=value:EFFECT` with a short right-pointing arrow to the word `repels`; in the right margin, outside the box, the annotation *"refusal originates HERE"* pointing at the node box. Below the node, three Pod markers approach or sit: Pod A (arriving, no toleration) and Pod B (arriving, matching toleration) are drawn below the box with upward arrows into it; Pod C (already aboard, no toleration) is drawn as a filled dot **on or inside** the node's lower edge with no approach arrow, so it reads as already resident. Label each marker with its name and condition. Under the arrows, the caption *"(tolerations belong to the POD)"*. **Lower half:** a table, three data rows by four columns. Header row: `EFFECT` | `Pod A — arriving, no toleration` | `Pod B — arriving, tolerating` | `Pod C — already running, no toleration`. Rows: `NoSchedule` → not placed / may be placed / unaffected. `PreferNoSchedule` → avoided where possible / may be placed / unaffected. `NoExecute` → not placed / may be placed / **EVICTED**. A footer caption below the table reads: *"'may be placed' — never 'is placed.' The other filters and scores still run."* The `EVICTED` cell is the only outcome in the Pod C column that differs from the others and is the visual focus of the whole figure.

**Visual style:**
- Palette: inherit book default — Navy `#0B1E3B` for the node box, table rules and headers; Teal `#1F4A4E` for the Pod markers and their arrows; Cream `#F5EFE4` ground; Fog `#8A8D90` for the two `unaffected` cells and the footer caption
- Size (pixels): 1100x780 landscape
- Font: inherit book default (Fira Mono for `NoSchedule`, `PreferNoSchedule`, `NoExecute`, `key=value:EFFECT`; Fira Sans elsewhere)
- Accent color for highlighted elements: Oxblood `#7A2E2E` fill behind the `EVICTED` cell and on the `NoExecute` row rule — plus a heavier row weight so the emphasis survives greyscale; Brass `#B58B3E` on the `taint:` line in the node box

**Critical details (non-negotiable accuracy):**
- The **taint sits on the NODE**; the **tolerations belong to the Pods**. Reversing this inverts the entire section and is the most common error in this material.
- Only the `NoExecute` row evicts. `NoSchedule` and `PreferNoSchedule` both leave the already-running Pod C **unaffected** — two of three rows do not touch it.
- Pod B's outcome is `may be placed` in all three rows — never "is placed" or "placed". A toleration removes a veto; it does not guarantee placement.
- Pod A under `PreferNoSchedule` is `avoided where possible`, **not** `not placed`. This is the soft effect and it loses when nothing better is available.
- Pod C must be depicted as already resident on the node, not approaching it — otherwise the eviction row reads as a placement refusal rather than as an action reaching backwards onto a running Pod.
- Effect names are exact and case-sensitive: `NoSchedule`, `PreferNoSchedule`, `NoExecute`.

**Source ASCII (for designer reference):**
```
        ┌────────────────────────────────────────────────┐
        │  NODE                                          │
        │  taint:  key=value:EFFECT   ───▶  repels       │  refusal originates HERE
        └────────────────────────────────────────────────┘
             ▲                ▲                  ●
             │                │                  └─ Pod C: already aboard, no toleration
             │                └───────────────────  Pod B: arriving, matching toleration
             └────────────────────────────────────  Pod A: arriving, no toleration
                        (tolerations belong to the POD)

   ┌──────────────────┬────────────────┬─────────────────┬─────────────────────┐
   │ EFFECT           │ Pod A          │ Pod B           │ Pod C               │
   │                  │ arriving,      │ arriving,       │ already running,    │
   │                  │ no toleration  │ tolerating      │ no toleration       │
   ├──────────────────┼────────────────┼─────────────────┼─────────────────────┤
   │ NoSchedule       │ not placed     │ may be placed   │ unaffected          │
   │ PreferNoSchedule │ avoided where  │ may be placed   │ unaffected          │
   │                  │ possible       │                 │                     │
   │ NoExecute        │ not placed     │ may be placed   │ EVICTED             │
   └──────────────────┴────────────────┴─────────────────┴─────────────────────┘

   "may be placed" — never "is placed." The other filters and scores still run.
```

**Proposed filename:** `ch07-fig03-taints-tolerations-effects.png`

```yaml-figure-spec
anchor_id: ch07-fig03-taints-tolerations-effects
diagram_type: other
source_ascii: |5
          ┌────────────────────────────────────────────────┐
          │  NODE                                          │
          │  taint:  key=value:EFFECT   ───▶  repels       │  refusal originates HERE
          └────────────────────────────────────────────────┘
               ▲                ▲                  ●
               │                │                  └─ Pod C: already aboard, no toleration
               │                └───────────────────  Pod B: arriving, matching toleration
               └────────────────────────────────────  Pod A: arriving, no toleration
                          (tolerations belong to the POD)

     ┌──────────────────┬────────────────┬─────────────────┬─────────────────────┐
     │ EFFECT           │ Pod A          │ Pod B           │ Pod C               │
     │                  │ arriving,      │ arriving,       │ already running,    │
     │                  │ no toleration  │ tolerating      │ no toleration       │
     ├──────────────────┼────────────────┼─────────────────┼─────────────────────┤
     │ NoSchedule       │ not placed     │ may be placed   │ unaffected          │
     │ PreferNoSchedule │ avoided where  │ may be placed   │ unaffected          │
     │                  │ possible       │                 │                     │
     │ NoExecute        │ not placed     │ may be placed   │ EVICTED             │
     └──────────────────┴────────────────┴─────────────────┴─────────────────────┘

     "may be placed" — never "is placed." The other filters and scores still run.
vendor_terms: [kubernetes-node, kubernetes-pod]
complexity_hint:
  node_count: 5
  edge_count: 4
  label_count: 24
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, temporal_structure, fixed_point]
  learning_outcome: "Predict what each of the three taint effects does to an arriving Pod and to a Pod already running on the node, and place the taint on the node and the toleration on the Pod"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the EVICTED cell at the intersection of the NoExecute row and the Pod C column"
accessibility:
  alt_text_seed: "A node carrying a taint repels three Pods: two arriving and one already resident. A table below shows that NoSchedule and PreferNoSchedule leave the resident Pod unaffected, while NoExecute evicts it."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original tabulation of taint-effect behaviour described in the Kubernetes docs; no vendor artwork reproduced."
```

---

## Figure: ch07-fig04-pod-affinity-anti-affinity-topology

**Anchor ID:** `ch07-fig04-pod-affinity-anti-affinity-topology`
**Purpose:** Shows that `topologyKey` is a variable, not a synonym for "node" — the same rule over the same cluster admits six Pods or two depending on which node label names the domain.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** side-by-side cluster topology comparison (identical cluster, two domain definitions)

**Content specification:**
A two-panel comparison under a shared two-line title: *"SAME CLUSTER. SAME RULE: 'no two Pods labelled app=web in one domain.'"* and *"THE ONLY DIFFERENCE IS THE topologyKey."* Each panel carries a two-line header: left = `topologyKey: kubernetes.io/hostname` over *"a domain = one node"*; right = `topologyKey: topology.kubernetes.io/zone` over *"a domain = one zone"*. Each panel contains two stacked bordered boxes labelled `zone-a` (top) and `zone-b` (bottom). Inside `zone-a` sit three node tokens `n1 n2 n3`; inside `zone-b`, `n4 n5 n6`. In the **left** panel, every one of the six nodes carries a `[web]` Pod tag. In the **right** panel, only `n1` and `n4` carry a `[web]` tag; `n2`, `n3`, `n5`, `n6` are bare. Below each panel, a result line: left *"6 domains → up to 6 Pods placed"*; right *"2 domains → at most 2 Pods placed"*. A single footer line spans both panels: *"One label key changed. The rule's meaning changed with it."* The reader must be able to see at a glance that the two panels contain the identical cluster and that only the density of `[web]` tags differs.

**Visual style:**
- Palette: inherit book default — Navy `#0B1E3B` for zone borders and node tokens, Teal `#1F4A4E` for the panel headers and the `topologyKey` strings, Cream `#F5EFE4` ground, Fog `#8A8D90` for the bare (untagged) nodes in the right panel
- Size (pixels): 1200x680 landscape
- Font: inherit book default (Fira Mono for `topologyKey`, the two label keys, `app=web`, node names and `[web]` tags; Fira Sans for prose)
- Accent color for highlighted elements: Brass `#B58B3E` on every `[web]` Pod tag, so the six-versus-two count reads as a density difference at a glance

**Critical details (non-negotiable accuracy):**
- Both panels depict the **same** cluster: six nodes `n1`–`n6`, three per zone, two zones. Do not vary node count, zone count, or node naming between panels.
- Left panel: **all six** nodes carry `[web]`. Right panel: **exactly one node per zone** carries `[web]` — `n1` and `n4`. Not two per zone, not one total.
- The two label keys must be exact and are easy to mistype: `kubernetes.io/hostname` and `topology.kubernetes.io/zone`.
- Domain counts: **6** on the left, **2** on the right. The result lines read "up to 6" and "at most 2" — both are ceilings, not guarantees.
- The rule text appears **once**, above both panels. Do not repeat it per panel in any form that implies two different rules were applied.
- Zone membership: `n1 n2 n3` in `zone-a`, `n4 n5 n6` in `zone-b`, in both panels.

**Source ASCII (for designer reference):**
```
   SAME CLUSTER. SAME RULE: "no two Pods labelled app=web in one domain."
   THE ONLY DIFFERENCE IS THE topologyKey.

   topologyKey: kubernetes.io/hostname       topologyKey: topology.kubernetes.io/zone
   a domain = one node                       a domain = one zone

   ┌── zone-a ──────────────────┐            ┌── zone-a ──────────────────┐
   │  n1 [web]   n2 [web]       │            │  n1 [web]   n2      n3     │
   │  n3 [web]                  │            │                            │
   └────────────────────────────┘            └────────────────────────────┘
   ┌── zone-b ──────────────────┐            ┌── zone-b ──────────────────┐
   │  n4 [web]   n5 [web]       │            │  n4 [web]   n5      n6     │
   │  n6 [web]                  │            │                            │
   └────────────────────────────┘            └────────────────────────────┘

   6 domains  →  up to 6 Pods placed         2 domains  →  at most 2 Pods placed

   One label key changed. The rule's meaning changed with it.
```

**Proposed filename:** `ch07-fig04-pod-affinity-anti-affinity-topology.png`

```yaml-figure-spec
anchor_id: ch07-fig04-pod-affinity-anti-affinity-topology
diagram_type: k8s_architecture
source_ascii: |5
     SAME CLUSTER. SAME RULE: "no two Pods labelled app=web in one domain."
     THE ONLY DIFFERENCE IS THE topologyKey.

     topologyKey: kubernetes.io/hostname       topologyKey: topology.kubernetes.io/zone
     a domain = one node                       a domain = one zone

     ┌── zone-a ──────────────────┐            ┌── zone-a ──────────────────┐
     │  n1 [web]   n2 [web]       │            │  n1 [web]   n2      n3     │
     │  n3 [web]                  │            │                            │
     └────────────────────────────┘            └────────────────────────────┘
     ┌── zone-b ──────────────────┐            ┌── zone-b ──────────────────┐
     │  n4 [web]   n5 [web]       │            │  n4 [web]   n5      n6     │
     │  n6 [web]                  │            │                            │
     └────────────────────────────┘            └────────────────────────────┘

     6 domains  →  up to 6 Pods placed         2 domains  →  at most 2 Pods placed

     One label key changed. The rule's meaning changed with it.
vendor_terms: [kubernetes-node, kubernetes-pod]
complexity_hint:
  node_count: 16
  edge_count: 0
  label_count: 22
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, quantitative_relationships]
  learning_outcome: "Explain how changing topologyKey changes the meaning of an unchanged inter-Pod anti-affinity rule, and why zone-level spread is dramatically stricter than node-level spread"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the [web] Pod tags — six of them in the left panel, two in the right"
accessibility:
  alt_text_seed: "Two panels showing the same six-node, two-zone cluster. With topologyKey set to hostname, all six nodes host a web Pod. With topologyKey set to zone, only one node per zone does — six placements become two."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original worked example using well-known Kubernetes node label keys; no vendor artwork or trade dress."
```

---

## Figure: ch07-zenith-berth-assignment

> **Anchor ID format exception** — this anchor omits the `fig{MM}` segment required by the locked pattern. Preserved verbatim here as the join key; see the exceptions section at the top of this file.

**Anchor ID:** `ch07-zenith-berth-assignment`
**Purpose:** Carries the chapter's ☀️ Zenith — collapses six placement vocabularies into two slots in the §1 pipeline, and isolates `spec.nodeName` as the one mechanism that fits neither.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** horizontal three-stage flow diagram with two feeder columns and one bypass arrow

**Content specification:**
Two collector boxes sit side by side across the top. The left is headed `FILTERS — remove nodes` and lists seven entries in order: *requests vs allocatable; nodeSelector; required node affinity; untolerated NoSchedule; untolerated NoExecute; required inter-Pod rules; DoNotSchedule spread*. The right is headed `SCORES — rank what remains` and lists five: *preferred node affinity; PreferNoSchedule; preferred inter-Pod rules; ScheduleAnyway spread; other scoring plugins*. A downward arrow drops from each collector into its corresponding stage of a three-stage strip below: `1. FILTER` → `2. SCORE` → `3. BIND`, joined left to right — the same strip, in the same order, as fig01. A downward arrow from `3. BIND` lands on a small box labelled `a node`. Separately, at the lower left and clearly outside the pipeline, place `spec.nodeName` with a long horizontal arrow that runs beneath the three stages, touching none of them, and terminates directly on the `a node` box. Beneath that arrow, the caption *"neither a filter nor a score — it deletes the choice."* The two-column split is the payload: seven filters, five scores, and one thing that is neither.

**Visual style:**
- Palette: inherit book default — Navy `#0B1E3B` for the pipeline strip and the FILTERS column, Teal `#1F4A4E` for the SCORES column, Cream `#F5EFE4` ground, Fog `#8A8D90` for the bypass caption
- Size (pixels): 1200x820 landscape
- Font: inherit book default (Fira Mono for `nodeSelector`, `NoSchedule`, `NoExecute`, `PreferNoSchedule`, `DoNotSchedule`, `ScheduleAnyway`, `spec.nodeName`; Fira Sans for headers and prose)
- Accent color for highlighted elements: Oxblood `#7A2E2E` on the `spec.nodeName` bypass arrow, drawn heavier and dashed so it reads as an exception in greyscale; Brass `#B58B3E` on the two collector-box headers

**Critical details (non-negotiable accuracy):**
- The `spec.nodeName` arrow **bypasses all three stages** and lands on `a node` directly. It must not touch, pass through, or terminate at FILTER, SCORE, or BIND. If it appears to enter the pipeline, the Zenith is destroyed.
- Left column carries exactly **seven** filter entries; right column exactly **five** score entries. Reproduce both lists verbatim and in order.
- `NoSchedule` and `NoExecute` belong on the **filter** side; `PreferNoSchedule` belongs on the **score** side. Do not group the three taint effects together — separating them is the whole point.
- `DoNotSchedule` spread is a filter; `ScheduleAnyway` spread is a score. Same for required (filter) versus preferred (score) node affinity and inter-Pod rules.
- Stage order and labelling must match fig01 exactly — `1. FILTER` → `2. SCORE` → `3. BIND`. The reader is meant to recognise the strip from the first page of the chapter.
- `spec.nodeName` is written with the dotted field path, in mono. Not "nodeName field", not "node name".

**Source ASCII (for designer reference):**
```
  FILTERS — remove nodes                     SCORES — rank what remains
  ┌────────────────────────────────┐         ┌────────────────────────────────┐
  │ requests vs allocatable        │         │ preferred node affinity        │
  │ nodeSelector                   │         │ PreferNoSchedule               │
  │ required node affinity         │         │ preferred inter-Pod rules      │
  │ untolerated NoSchedule         │         │ ScheduleAnyway spread          │
  │ untolerated NoExecute          │         │ other scoring plugins          │
  │ required inter-Pod rules       │         │                                │
  │ DoNotSchedule spread           │         │                                │
  └───────────────┬────────────────┘         └────────────────┬───────────────┘
                  │                                           │
                  ▼                                           ▼
          ┌──────────────┐       ┌──────────────┐      ┌──────────────┐
          │  1. FILTER   │ ────▶ │  2. SCORE    │ ───▶ │  3. BIND     │
          └──────────────┘       └──────────────┘      └──────┬───────┘
                                                              │
                                                              ▼
                                                        ┌───────────┐
  spec.nodeName ────────────────────────────────────────▶│  a node   │
  neither a filter nor a score — it deletes the choice   └───────────┘
```

**Proposed filename:** `ch07-zenith-berth-assignment.png`

```yaml-figure-spec
anchor_id: ch07-zenith-berth-assignment
diagram_type: flowchart
source_ascii: |4
    FILTERS — remove nodes                     SCORES — rank what remains
    ┌────────────────────────────────┐         ┌────────────────────────────────┐
    │ requests vs allocatable        │         │ preferred node affinity        │
    │ nodeSelector                   │         │ PreferNoSchedule               │
    │ required node affinity         │         │ preferred inter-Pod rules      │
    │ untolerated NoSchedule         │         │ ScheduleAnyway spread          │
    │ untolerated NoExecute          │         │ other scoring plugins          │
    │ required inter-Pod rules       │         │                                │
    │ DoNotSchedule spread           │         │                                │
    └───────────────┬────────────────┘         └────────────────┬───────────────┘
                    │                                           │
                    ▼                                           ▼
            ┌──────────────┐       ┌──────────────┐      ┌──────────────┐
            │  1. FILTER   │ ────▶ │  2. SCORE    │ ───▶ │  3. BIND     │
            └──────────────┘       └──────────────┘      └──────┬───────┘
                                                                │
                                                                ▼
                                                          ┌───────────┐
    spec.nodeName ────────────────────────────────────────▶│  a node   │
    neither a filter nor a score — it deletes the choice   └───────────┘
vendor_terms: []
complexity_hint:
  node_count: 7
  edge_count: 6
  label_count: 20
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, zenith, fixed_point]
  learning_outcome: "Classify every placement mechanism in the chapter as either a filter or a score, and recognise spec.nodeName as the one mechanism that is neither"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the spec.nodeName bypass arrow running past all three stages straight into 'a node'"
accessibility:
  alt_text_seed: "Seven filter mechanisms feed the FILTER stage and five score mechanisms feed the SCORE stage of the filter-score-bind pipeline, which ends at a chosen node. A separate arrow from spec.nodeName bypasses all three stages and reaches the node directly."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original synthesis classifying documented Kubernetes scheduling mechanisms into the two scheduler stages; no vendor artwork."
```
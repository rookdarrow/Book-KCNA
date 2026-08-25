# Image Specifications — KCNA Chapter 8

*Generated from draft-v1.md (draft-voice.md does not exist at this stage). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Figure count:** 6 anchors, 6 ASCII blocks, 0 unanchored.
**Entry order:** draft order of appearance, not anchor-number order — see the anchor-ID flags below for why those two orders disagree.

---

## UNANCHORED DIAGRAMS

None. Every fenced ASCII block in this draft carries a `<!-- FIGURE: ... -->` comment on the line immediately preceding it. No action required.

---

## ANCHOR ID FLAGS (author-review required)

Rule 4 requires anchor IDs to match `ch{NN}-fig{MM}-{kebab-slug}` exactly, and Rule 6 forbids renaming them in this document. Three issues, flagged and left in place:

**1. Malformed anchor — missing the `figMM` segment.**

| Anchor as written | Location | Caption in draft |
|---|---|---|
| `ch08-zenith-consequences-not-rules` | §8, after the ☀️ Zenith callout | "Figure 8.6" |

There is no `fig{MM}` segment. This will not sort into the book-level image index alongside its siblings, and the diagram pipeline's D1 router keys on the segment. Suggested correction: `ch08-fig06-zenith-consequences-not-rules`. **Author to confirm before the draft is edited** — the anchor is the join key and changing it here without changing the draft would break the join.

**2. Anchor numbering and caption numbering disagree.** Anchor `fig{MM}` values were not assigned in draft order, so three of the six figures have an anchor number that does not match the "Figure 8.N" caption a reader sees:

| Draft position | Anchor | Caption | Agrees? |
|---|---|---|---|
| 1 (§1) | `ch08-fig01-kubectl-verb-resource-grammar` | Figure 8.1 | yes |
| 2 (§2) | `ch08-fig02-three-api-gates` | Figure 8.2 | yes |
| 3 (§3) | `ch08-fig05-quota-vs-limitrange` | **Figure 8.3** | **no** |
| 4 (§4) | `ch08-fig04-node-lifecycle-cordon-drain` | Figure 8.4 | yes |
| 5 (§6) | `ch08-fig03-version-skew-window` | **Figure 8.5** | **no** |
| 6 (§8) | `ch08-zenith-consequences-not-rules` | **Figure 8.6** | **no** (and malformed) |

This is cosmetic for the render pipeline (the anchor string is the join key and is internally consistent) but it is a live hazard for any human cross-referencing prose against filenames — `ch08-fig05-*.png` renders as "Figure 8.3". Recommend renumbering anchors to draft order in one sweep, draft and specs together, before any figure is commissioned.

**3. No figure exists for the Capacity → Allocatable relationship (§4).** Noted here rather than as an omission: the draft's AUTHOR-REVIEW comment at §4 records that the upstream source expresses this relationship *only* as an image (`node-capacity.svg`) with no text equivalent, and that the arithmetic was deliberately not extracted. A figure here would have to assert the arithmetic the prose declines to assert. **Do not commission one** until that source gap is closed. Flagged so the absence reads as a decision rather than an oversight.

---

## Figure: ch08-fig01-kubectl-verb-resource-grammar

**Anchor ID:** `ch08-fig01-kubectl-verb-resource-grammar`
**Purpose:** Shows that five commands the reader has already typed across four chapters all decompose into the same four slots, and carries the case-sensitivity asymmetry that is this section's examinable content.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** annotated syntax-decomposition table (four aligned columns with two callout pointers beneath)

**Content specification:**

Render a four-column grid. The column headers, left to right, are `[command]`, `[TYPE]`, `[NAME]`, `[flags]`, each set in monospace with a rule beneath it; the literal word `kubectl` sits to the left of the header row and to the left of every data row, outside the four columns, as a fixed prefix. Five data rows follow, each one a real command from earlier chapters, and their cells must be aligned to the columns so the empty cells are visually obvious: `cordon` / `node` / `node-7` / —; `get` / `pods` / — / —; `apply` / — / — / `-f deploy.yaml`; `scale` / `deployment` / `web` / `--replicas=5`; `describe` / `node` / `worker-3` / —. **The empty cells are load-bearing and must read as deliberately empty, not as a layout accident** — do not collapse, centre, or close up the gaps; the caption points at them.

Beneath the grid, two callout pointers rise from the TYPE column and the NAME column respectively. The TYPE pointer reads `case-INsensitive` with `pod = pods = po` beneath it. The NAME pointer reads `case-SENSITIVE` with `node-7 ≠ Node-7` beneath it. **The asymmetry between these two callouts is the point of the figure** — they must be visually parallel in placement and weight so that the *only* difference a reader registers is the word itself. Set the `IN` of `case-INsensitive` and the whole of `case-SENSITIVE` in the accent treatment so the contrast survives a glance. The `≠` must be a true not-equal glyph, not a struck-through equals.

**Visual style:**
- Palette: inherit book default (Lodestar navy/slate line-art, monospace for all command text — Fira Mono per the locked typography pairing)
- Size (pixels): 1000x420 landscape
- Font: inherit book default; all grid content monospace, callout labels in body face
- Accent color for highlighted elements: Brass #B58B3E on the two case-sensitivity callouts and their pointers only

**Critical details (non-negotiable accuracy):**
- Slot order is `command`, `TYPE`, `NAME`, `flags`, left to right. Reversing or reordering breaks the section's entire premise.
- `kubectl get pods` must show **two** empty cells (NAME and flags). `kubectl apply -f deploy.yaml` must show TYPE and NAME empty with content only in flags.
- The TYPE callout says case-**IN**sensitive; the NAME callout says case-**SENSITIVE**. Swapping these inverts the one fact the figure exists to teach.
- `node-7 ≠ Node-7` — the hyphenated lowercase form is the valid one; do not "tidy" the capitalisation.
- `pod = pods = po` — three forms, singular/plural/abbreviated, in that order.
- `kubectl` is a prefix outside the four slots, not the contents of the first slot.

**Source ASCII (for designer reference):**
```
  kubectl   [command]        [TYPE]        [NAME]      [flags]
            ─────────        ──────        ──────      ───────

  kubectl   cordon           node          node-7
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
source_ascii: |2
    kubectl   [command]        [TYPE]        [NAME]      [flags]
              ─────────        ──────        ──────      ───────

    kubectl   cordon           node          node-7
    kubectl   get              pods
    kubectl   apply                                      -f deploy.yaml
    kubectl   scale            deployment    web         --replicas=5
    kubectl   describe         node          worker-3

                                  ▲             ▲
                      case-INsensitive     case-SENSITIVE
                      pod = pods = po      node-7 ≠ Node-7
vendor_terms: [kubectl]
complexity_hint:
  node_count: 9
  edge_count: 2
  label_count: 23
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Decompose any kubectl invocation into its four slots, and apply the case-sensitivity rule that differs between TYPE and NAME"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the paired case-INsensitive / case-SENSITIVE callouts beneath the TYPE and NAME columns"
accessibility:
  alt_text_seed: "A four-column table headed command, TYPE, NAME and flags, with five example kubectl commands aligned to the columns and several cells deliberately empty; two callouts beneath mark the TYPE column as case-insensitive and the NAME column as case-sensitive"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes CLI syntax redrawn in Lodestar style; no upstream figure reproduced, command names are project terminology"
```

---

## Figure: ch08-fig02-three-api-gates

**Anchor ID:** `ch08-fig02-three-api-gates`
**Purpose:** Establishes that a request passes three gates in a fixed order, and — the whole reason the figure exists — that only the third gate has an exit other than forward-or-refuse.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** horizontal flow diagram with per-stage rejection branches and one rewrite loop-back

**Content specification:**

A left-to-right flow. An inbound arrow labelled `request` enters the first of three boxes, arranged in a horizontal row and labelled above as `gate 1`, `gate 2`, `gate 3`. The boxes themselves are labelled `Authentication`, `Authorization`, `Admission`, in that order. A forward arrow connects each box to the next, and a final forward arrow leaves gate 3 to a terminal labelled `persisted to etcd`.

Beneath each of the three boxes, a downward arrow leads to a terminal reading `REJECT`. Three of them, one per gate, identical in treatment.

Gate 3 has a **fourth** connection the other two lack: a second downward path labelled `REWRITTEN` that turns and rejoins the forward path into `persisted to etcd`. This is the single most important element in the figure. It must be immediately visible that gates 1 and 2 have exactly two exits each (forward, or down to REJECT) while gate 3 has three (forward, down to REJECT, and the rewrite path that goes down, across, and back into the forward flow). Render the REWRITTEN path in the accent colour and, because colour alone must not carry it, at a distinctly heavier weight or with a distinct dash pattern from the REJECT arrows. Do not let the rewrite path terminate anywhere except back into `persisted to etcd` — the semantic point is that a rewritten request *proceeds*, altered, rather than being refused.

**Visual style:**
- Palette: inherit book default (navy/slate line-art)
- Size (pixels): 1200x420 landscape
- Font: inherit book default; gate labels in body face, `persisted to etcd` in body face
- Accent color for highlighted elements: Brass #B58B3E on the REWRITTEN path and its rejoin arrow only; REJECT arrows stay in the base line colour

**Critical details (non-negotiable accuracy):**
- Order is Authentication → Authorization → Admission. Any other order is factually wrong and the chapter's Fixed Point, Practice Question 2 and the Exam Alert all depend on it.
- Admission is **third**, after authorization, and before persistence. Not first, not parallel, not after the write.
- Only gate 3 has the REWRITTEN exit. Giving a rewrite path to gates 1 or 2 destroys the distinction the whole section is built on.
- The REWRITTEN path rejoins the forward flow and reaches `persisted to etcd`. It must not terminate at a REJECT or dead-end.
- All three REJECT terminals are equivalent — do not differentiate them or imply a hierarchy of refusal.
- Everything flows through one door. No element may bypass the gate chain and reach etcd directly.

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
source_ascii: |2
                  gate 1              gate 2              gate 3
             ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
   request ─►│Authentication├──►│Authorization ├──►│  Admission   ├──► persisted
             └──────┬───────┘   └──────┬───────┘   └──┬───────┬───┘     to etcd
                    │                  │             │       │              ▲
                    ▼                  ▼             ▼       │              │
                 REJECT             REJECT        REJECT     └── REWRITTEN ─┘
vendor_terms: [kube-apiserver, etcd]
complexity_hint:
  node_count: 9
  edge_count: 9
  label_count: 10
pedagogy:
  part_18_criteria_met: [temporal_structure, spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Trace a request through authentication, authorization and admission in order, and identify admission as the only gate that can modify rather than merely accept or refuse"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the REWRITTEN path leaving gate 3 and rejoining the forward flow into etcd"
accessibility:
  alt_text_seed: "A request flows left to right through three gates labelled Authentication, Authorization and Admission before being persisted to etcd; each gate has a downward arrow to REJECT, and the third gate alone has an additional REWRITTEN path that loops back into the forward flow"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Access-control sequence redrawn from documentation prose; no upstream figure reproduced"
```

---

## Figure: ch08-fig05-quota-vs-limitrange

**Anchor ID:** `ch08-fig05-quota-vs-limitrange`
*(Caption in draft reads "Figure 8.3" — see ANCHOR ID FLAGS above. Do not rename here.)*
**Purpose:** Separates ResourceQuota from LimitRange by scope, and proves the separation by showing that the two mechanisms fail in visibly different ways against the identical arriving Pod.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel side-by-side comparison (containment box vs. unbounded per-object constraints)

**Content specification:**

Two panels, side by side, headed `ResourceQuota` (left) and `LimitRange` (right).

The left panel draws a closed boundary box labelled `namespace: team-atlas`. Inside it sit four small boxes each labelled `Pod`, and beneath them two horizontal bars: the upper reads `namespace total`, the lower reads `AT CAP`. The boundary is the point — the quota is a statement about everything inside that box, in aggregate.

The right panel has **no enclosing boundary at all**, and this absence must be as visible as the left panel's boundary is present. Add the parenthetical `(no namespace boundary)` beneath the heading. Four `Pod` boxes float unenclosed; each one carries the constraint `min ≤ ... ≤ max` written on the Pod itself, because the LimitRange constrains each object individually rather than the group.

Beneath each panel, an upward pointer to a fifth arriving Pod and its outcome. Left: `5th Pod arrives: REJECTED — the namespace total is reached`. Right: `5th Pod arrives declaring nothing: ACCEPTED — with defaults FILLED IN`. **The two outcomes are the payload of the figure.** Set `REJECTED` and `ACCEPTED — with defaults FILLED IN` in the accent treatment, and differentiate them by more than colour (weight, or a refusal glyph versus a fill glyph), because the identical arriving Pod meeting two different fates is what makes the scope distinction stick.

**Visual style:**
- Palette: inherit book default (navy/slate line-art)
- Size (pixels): 1100x600 landscape
- Font: inherit book default; `namespace: team-atlas` and `min ≤ ≤ max` in monospace
- Accent color for highlighted elements: Brass #B58B3E on the two fifth-Pod outcome labels and their pointers

**Critical details (non-negotiable accuracy):**
- The left panel has a namespace boundary. The right panel has none. Adding a boundary to the right panel destroys the figure.
- ResourceQuota = aggregate ceiling on the namespace. LimitRange = per-object constraint. Swapping the two panels' headings inverts the one discrimination this section teaches, and is the exact error the Practice Questions defuse.
- The left outcome is **rejection**; the right outcome is **acceptance with modification**. The right Pod is not refused.
- The right panel's fifth Pod declares **nothing** — it arrives with no resource fields at all, and is accepted anyway because the defaults are supplied for it.
- Four existing Pods per panel, fifth arriving. Do not change the counts; the "AT CAP" bar depends on four already being present.
- Both objects are namespaced; the right panel's lack of a drawn boundary indicates the *constraint's* scope, not that LimitRange is cluster-scoped. Do not add a caption implying otherwise.

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
diagram_type: k8s_architecture
source_ascii: |2
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
  node_count: 13
  edge_count: 2
  label_count: 12
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Distinguish ResourceQuota from LimitRange by what each constrains and at what scope, using their differing failure modes as the proof"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the two fifth-Pod outcomes — REJECTED on the left, ACCEPTED with defaults filled in on the right"
accessibility:
  alt_text_seed: "Two panels compared: on the left a ResourceQuota draws a boundary around a namespace holding four Pods with an at-cap total bar, and a fifth arriving Pod is rejected; on the right a LimitRange has no namespace boundary, four Pods each carry a min-to-max constraint, and a fifth Pod declaring nothing is accepted with defaults filled in"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Conceptual scope comparison drawn from documentation prose; no upstream figure reproduced"
```

---

## Figure: ch08-fig04-node-lifecycle-cordon-drain

**Anchor ID:** `ch08-fig04-node-lifecycle-cordon-drain`
**Purpose:** Makes visible that a cordoned node is not an empty node — the chapter's single most consequential confusion, and the one with a real operational cost attached.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** four-panel state progression with labelled transitions

**Content specification:**

Four panels left to right, each a node box, headed `SCHEDULABLE`, `CORDONED`, `DRAINED`, `SCHEDULABLE`. Transitions between them are labelled `cordon`, `drain`, `uncordon` respectively.

Panel 1 contains three Pods labelled `[A]`, `[B]`, `[C]`. **Panel 2 contains the identical three Pods, drawn identically.** This is the entire figure. Nothing about A, B or C may change between panel 1 and panel 2 — not their position, not their fill, not their weight, not their opacity. Any visual softening of the Pods in the cordoned panel would teach the wrong thing. Panel 3 is empty, marked `(empty)`. Panel 4 is empty and ready to accept work.

Beneath panels 1, 2 and 4, an arriving-Pod annotation. Panel 1: `new Pod — admitted`. Panel 2: `new Pod — turned away`, marked with a refusal glyph (✗). Panel 4: `new Pod — admitted`. Only the arriving Pod's fate differs between panels 1 and 2, and the accent should sit on that refusal glyph, not on the resident Pods.

Beneath the whole strip, set the reinforcing note as running text within the figure: *A, B and C are UNCHANGED between panel 1 and panel 2. They are still running. That is what cordon does and does not do.*

**Visual style:**
- Palette: inherit book default (navy/slate line-art)
- Size (pixels): 1200x480 landscape
- Font: inherit book default; state headings in display face small-caps or equivalent, transition verbs in monospace
- Accent color for highlighted elements: Brass #B58B3E on the ✗ refusal glyph and the "turned away" label under panel 2

**Critical details (non-negotiable accuracy):**
- Pods A, B and C are pixel-identical between panels 1 and 2. Fading, greying, or shrinking them in the CORDONED panel would state the opposite of the fact being taught.
- The node does not empty until `drain`. Panel 2 is full; panel 3 is empty.
- Transition verbs in order: `cordon`, then `drain`, then `uncordon`. The maintenance sequence needs the first two.
- Panel 2's *arriving* Pod is refused. Panel 2's *resident* Pods are untouched. Both facts must be simultaneously legible.
- Panel 4 shows the node schedulable and empty — `uncordon` restores scheduling, it does not restore the evicted Pods to that node.
- Three resident Pods, not two or four; the §5 Bearings item and Practice Question 8 both reference "three services".

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
source_ascii: |2
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
  node_count: 7
  edge_count: 6
  label_count: 14
pedagogy:
  part_18_criteria_met: [temporal_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Predict what happens to Pods already on a node at each step of cordon, drain and uncordon — specifically that cordon leaves running Pods untouched"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the refusal glyph and 'turned away' label under the CORDONED panel, set against three resident Pods that are unchanged"
accessibility:
  alt_text_seed: "Four node panels in sequence: schedulable with three Pods A B and C, cordoned with the same three Pods still present but an arriving Pod turned away, drained and empty, then schedulable again; transitions are labelled cordon, drain and uncordon"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Node maintenance lifecycle drawn from documentation prose; no upstream figure reproduced"
```

---

## Figure: ch08-fig03-version-skew-window

**Anchor ID:** `ch08-fig03-version-skew-window`
*(Caption in draft reads "Figure 8.5" — see ANCHOR ID FLAGS above. Do not rename here.)*
**Purpose:** Converts the five-row version-skew table into one picture with one rule visible in it — every bar stops at the API server's version except `kubectl`, which is the only bar that crosses.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** horizontal span chart on a relative offset axis, with a hard wall at zero

**Content specification:**

A horizontal axis of minor-version offsets **relative to kube-apiserver**, with tick marks at `-3`, `-2`, `-1`, `0`, `+1`. Label the axis ends `older` (left, with a left-pointing arrow) and `newer` (right, with a right-pointing arrow), and label the zero position `kube-apiserver`.

At the `0` position, draw a **vertical wall** — heavier and visually distinct from the ordinary tick marks, rendered as a double rule in the source ASCII. It runs the full height of the chart.

Six labelled horizontal bars, one per row, stacked in this order top to bottom: `kubelet`, `kube-proxy`, `controller-manager`, `scheduler`, `cloud-ctrl-manager`, `kubectl`. Each bar has a round cap at its oldest permitted offset and terminates at the wall:

- `kubelet` — spans `-3` to `0`, stops dead at the wall
- `kube-proxy` — spans `-3` to `0`, stops dead at the wall
- `controller-manager` — spans `-1` to `0`, stops dead at the wall
- `scheduler` — spans `-1` to `0`, stops dead at the wall
- `cloud-ctrl-manager` — spans `-1` to `0`, stops dead at the wall
- `kubectl` — spans `-1` **through the wall** to `+1`, with round caps at both ends

An annotation beneath the `kubectl` bar, pointing up at the crossing point, reads *the only bar that crosses*. **That crossing is the whole figure.** Set the `kubectl` bar and its crossing annotation in the accent treatment, and give the bar a distinct weight or pattern so the crossing is legible in greyscale.

**Visual style:**
- Palette: inherit book default (navy/slate line-art)
- Size (pixels): 1100x520 landscape
- Font: inherit book default; component names in monospace
- Accent color for highlighted elements: Brass #B58B3E on the `kubectl` bar, its `+1` cap, and the crossing annotation. The wall at zero stays in the base colour but at heavier weight than the ticks.

**Critical details (non-negotiable accuracy):**
- The axis is **relative offsets**, not absolute version numbers. Do not substitute 1.33/1.34/1.35/1.36/1.37 — the draft explicitly says the axis is relative so the figure does not expire, and the accompanying prose warns that the current roster changes.
- `kubectl` is the **only** bar extending past `0`, and it reaches exactly `+1`. Not `+2`, not `+3`.
- `kubelet` and `kube-proxy` reach exactly `-3`. `controller-manager`, `scheduler` and `cloud-ctrl-manager` reach exactly `-1`. `kubectl`'s left cap is `-1`.
- No bar other than `kubectl` may cross or even touch the right side of the wall.
- `kube-proxy`'s ±3 allowance relative to the *kubelet* is deliberately **not** shown here; this axis is relative to the API server only, where kube-proxy is older-only. Do not add a rightward extension to kube-proxy.
- The HA kube-apiserver-to-kube-apiserver one-minor rule is **not** a row in this figure. Do not add a seventh bar for it.
- Bar order top to bottom must match the source; `kubectl` sits last, immediately above its annotation.

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
diagram_type: gantt
source_ascii: |2
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
  edge_count: 0
  label_count: 15
pedagogy:
  part_18_criteria_met: [quantitative_relationships, distinguishing_alternatives, fixed_point]
  learning_outcome: "State which Kubernetes components may disagree about their version, by how much, and in which direction — and identify kubectl as the sole component permitted to be newer than the API server"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the kubectl bar crossing the wall at offset zero to reach plus one"
accessibility:
  alt_text_seed: "A horizontal chart of minor-version offsets relative to kube-apiserver, from minus three to plus one, with a wall at zero; bars for kubelet and kube-proxy extend from minus three to the wall, bars for controller-manager, scheduler and cloud-controller-manager from minus one to the wall, and the kubectl bar alone crosses the wall to reach plus one"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Version-skew policy re-expressed as a relative-offset span chart in Lodestar style; factual policy data, not a reproduced upstream figure"
```

---

## Figure: ch08-zenith-consequences-not-rules

**Anchor ID:** `ch08-zenith-consequences-not-rules`
⚠ **Anchor does not conform to `ch{NN}-fig{MM}-{slug}` — flagged above. Caption in draft reads "Figure 8.6". Left unrenamed per Rule 6; author to resolve.**
**Purpose:** Carries the chapter's Zenith claim visually — every administrative act is a write through one door, reconciled by a controller the reader already met, with no side channels anywhere on the diagram.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hub-and-spoke architecture diagram (converging inputs, single hub, diverging outputs, one terminal store)

**Content specification:**

Three vertical zones. On the left, headed `administrative acts (§1, §3, §4)`, four labelled inputs stacked vertically: `kubectl cordon`, `kubectl apply -f quota.yaml`, `kubectl apply -f deploy.yaml`, `kubelet self-registration`. Each has an arrow pointing right.

In the centre, a single large box labelled `the API server` with `ONE DOOR` set beneath the name inside the same box. **All four left-hand arrows terminate at this box.** Not one of them may pass around, behind, or through it to reach the right-hand zone directly — the absence of side channels is the argument the figure is making.

On the right, headed `controllers you already met`, four labelled outputs, each reached by an arrow leaving the API server box: `scheduler (Ch 7)`, `node controller (Ch 4/8)`, `workload controllers (Ch 6)`, `the control loop (Ch 3)`. The chapter references in parentheses are part of the labels and must be rendered — they are what make the "you already met these" claim checkable at a glance.

Below the API server box, a single downward arrow to a terminal labelled `etcd`.

The centre box is the emphasis. Set `ONE DOOR` in the accent treatment. Keep the left and right zones in the base line colour so that the eye lands on the hub and the reader registers the convergence before the detail.

**Visual style:**
- Palette: inherit book default (navy/slate line-art)
- Size (pixels): 1200x560 landscape
- Font: inherit book default; commands on the left in monospace, controller names and chapter references on the right in body face
- Accent color for highlighted elements: Brass #B58B3E on the `ONE DOOR` label and the API server box border

**Critical details (non-negotiable accuracy):**
- **No arrow may connect a left-hand act to a right-hand controller directly.** Every path routes through the API server box. This is the one thing the figure exists to assert, and Practice Question 10's distractor D is precisely the belief it dismantles.
- Four inputs and four outputs, matched to the labels given. Do not add or drop entries.
- `kubelet self-registration` belongs on the **left**, with the administrative acts — the point is that a kubelet joining a cluster does the same thing a human does: it writes an object through the API server.
- Chapter references stay attached to their controllers: scheduler (Ch 7), node controller (Ch 4/8), workload controllers (Ch 6), the control loop (Ch 3).
- `etcd` sits **below** the API server, reached only from it. Nothing else touches etcd.
- The source ASCII abbreviates `workload contrls` for column width; render the full `workload controllers` in the figure.

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
*(Rename to `ch08-fig06-zenith-consequences-not-rules.png` if the anchor flag is resolved in favour of conforming.)*

```yaml-figure-spec
anchor_id: ch08-zenith-consequences-not-rules
diagram_type: k8s_architecture
source_ascii: |2
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
vendor_terms: [kube-apiserver, kubectl, kubelet, etcd, kube-scheduler, kube-controller-manager]
complexity_hint:
  node_count: 10
  edge_count: 9
  label_count: 14
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure, fixed_point]
  learning_outcome: "Recognise every administrative act in the chapter as a write through the API server, reconciled by a controller already introduced — and that no side channels exist"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the central API server box carrying the ONE DOOR label, through which every left-hand act must pass"
accessibility:
  alt_text_seed: "Four administrative acts on the left — kubectl cordon, applying a quota, applying a deployment, and kubelet self-registration — all converge on a single central box labelled the API server and ONE DOOR, which then fans out to four controllers introduced in earlier chapters and writes down to etcd; no act reaches a controller directly"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Hub-and-spoke restatement of the chapter's own synthesis; component names are project terminology, no upstream figure reproduced"
```
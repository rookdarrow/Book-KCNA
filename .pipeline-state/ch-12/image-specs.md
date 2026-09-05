# Image Specifications — KCNA Chapter 12

*Generated from `draft-v1.md` (line numbers below are against that file — `draft-voice.md` does not exist at this stage). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Chapter:** 12 — Locks, Keys, and Watchstanders
**Anchors found:** 6 · **Entries below:** 6 · **Unanchored ASCII diagrams:** 0 · **Non-conforming anchor IDs:** 1

**Series conventions applied to this chapter.** Per the ratified glyph decision (2026-08-25), only *stack* and *pipeline* family figures carry semantic Lucide glyphs; every other family stays glyph-free. Of the six figures here, only `ch12-fig05-supply-chain-checkpoints` is a pipeline figure, and it is the only entry with a populated `vendor_terms` list. The other five are conceptual maps, derivations and flows and must render glyph-free — their `vendor_terms` are deliberately empty so the D1 router does not reach for a vendor icon pack.

Entries are ordered by position in the draft, not by figure number. See the conformance flags immediately below for why those two orders differ.

---

## ANCHOR CONFORMANCE FLAGS

### Flag 1 — non-conforming anchor ID (blocking for the book-level index)

**Anchor:** `ch12-zenith-additive-never-deny` — draft-v1.md line 1337

Rule 4 requires `ch{NN}-fig{MM}-{kebab-slug}`. This anchor carries `zenith` where `fig{MM}` belongs, so it has no figure number and will not sort or join correctly in the book-level image index. The ID is **preserved unchanged** in the entry below, per rule 6 — renaming is an author-review decision.

**Suggested replacement:** `ch12-fig06-additive-never-deny` — author to confirm. If accepted, the anchor comment in `draft-v1.md:1337`, the entry heading here, the `anchor_id` in its `yaml-figure-spec`, and the proposed filename all change together.

**Note for the author:** the slug is genuinely useful information — this figure carries the chapter's ☀️ Zenith. That intent is preserved without breaking the ID scheme by `pedagogy.part_18_criteria_met: [zenith, ...]` in the structured block, which is where the diagram pipeline looks for it.

### Flag 2 — figure numbering runs out of order (non-blocking)

The anchors appear in the draft in this sequence:

| Draft line | Anchor | Position |
|---|---|---|
| 193 | `ch12-fig01-4cs-and-lifecycle-phases` | §1 |
| 293 | `ch12-fig03-serviceaccount-token-flow` | §2 |
| 398 | `ch12-fig02-rbac-four-way-matrix` | §3 |
| 876 | `ch12-fig04-pod-security-standards-levels` | §6 |
| 1063 | `ch12-fig05-supply-chain-checkpoints` | §7 |
| 1337 | `ch12-zenith-additive-never-deny` | §9 |

`fig03` precedes `fig02` in reading order. Every ID matches the required pattern, so this is not a rule-4 violation and nothing is renamed here — but a reader following figure numbers through the chapter will meet 1, 3, 2, 4, 5. Author to decide whether to renumber (swap `fig02` and `fig03`) or leave it. If renumbering, both the draft anchors and this file change together.

---

## UNANCHORED DIAGRAMS

**None.** All six fenced ASCII diagrams in `draft-v1.md` carry a preceding `<!-- FIGURE: ... -->` anchor.

One further fenced block was inspected and is **not** a diagram, recorded here so a later structural audit has the rationale rather than re-deriving it:

### ~Line 1005–1009 — not a diagram, no anchor needed

```
pod-security.kubernetes.io/enforce: baseline
pod-security.kubernetes.io/warn: restricted
pod-security.kubernetes.io/audit: restricted
```

This is three literal namespace labels inside the stem of Taking Your Bearings #2, question 4. It is quoted configuration the reader must parse as text, not a figure. It needs no anchor and must **not** be converted to an image — a rendered image of a question's input would be unreadable at reflow and unsearchable. Leave as a fenced code block.

---

## Figure: ch12-fig01-4cs-and-lifecycle-phases

**Anchor ID:** `ch12-fig01-4cs-and-lifecycle-phases`
**Draft location:** `draft-v1.md:193` (anchor), fenced block `194–229`, §1 — Four Layers and Four Phases
**Purpose:** Establishes that every Kubernetes security control has two independent coordinates — a lifecycle phase (*when* it acts) and a 4Cs layer (*where* it acts) — so the reader can place any control on both maps and recognise which of the two an exam question is actually asking about.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Three-panel composite — linear process flow with a three-way fork, nested containment diagram, and a plotting table

**Content specification:**

A single composite figure in three stacked panels, each introduced by a small-caps panel title above a full-width hairline rule. **Panel 1, "THE PHASES — when a control acts":** four boxes in a left-to-right row labelled DEVELOP, DISTRIBUTE, DEPLOY, RUNTIME, joined by three right-pointing arrows; from RUNTIME alone a stem drops and forks into three downward arrows terminating in three labels — ACCESS, COMPUTE, STORAGE. **Panel 2, "THE LAYERS — where a control acts":** four concentric rectangles, each fully containing the next, labelled inside their own top-left border in this order outermost-to-innermost — CLOUD, CLUSTER, CONTAINER, CODE — with the innermost CODE box drawn empty. **Panel 3, "FIVE CONTROLS, PLOTTED ON BOTH":** a three-column table under the headers *control / phase / layer*, with five rows: RBAC | runtime / access | Cluster; ServiceAccount | runtime / access | Cluster; securityContext | runtime / compute | Container; encryption at rest | runtime / storage | Cloud → Cluster; image signing | distribute | Container.

The point of the figure lives in panel 3: the *phase* and *layer* columns are independent coordinates, and the designer should give those two column headers matched accent treatment so the eye reads them as a pair of axes rather than as one classification refined by another. Nothing in panels 1 and 2 should be joined by any line, arrow, or shared colour ramp to panel 3 — the figure asserts two separate maps of the same territory, and drawing connectors between them would assert the opposite.

**Visual style:**
- Palette: inherit book default (Lodestar brand navy line work on the book's paper tone)
- Size (pixels): 900 × 1200 portrait (3:4 — do not author taller; per `check_reflow.py`, figures much taller than 3:4 scale down until type is illegible on a six-inch screen)
- Font: inherit book default — Roboto Slab for panel titles, Fira Sans for annotation, Fira Mono for the control names in panel 3's first column
- Accent colour for highlighted elements: Brass `#B58B3E` on the *phase* and *layer* column headers only

**Critical details (non-negotiable accuracy):**
- The layers nest in exactly this order, outermost to innermost: Cloud ⊃ Cluster ⊃ Container ⊃ Code. Reversing the nesting inverts the chapter's argument that Code cannot compensate for a weak base layer.
- The CODE box is drawn empty. Do not place content, an icon, or a label inside it.
- The phase sequence is DEVELOP → DISTRIBUTE → DEPLOY → RUNTIME, in that order and no other.
- Only RUNTIME forks. The fork has exactly three arms — ACCESS, COMPUTE, STORAGE — not four, and they hang off RUNTIME alone.
- The "encryption at rest" row's layer cell reads `Cloud → Cluster` with the arrow inside the cell: it starts at Cloud and extends into Cluster. It is not a single layer.
- "image signing" is the only row whose phase is not runtime. Its phase is `distribute` and its layer is Container. Both must be correct; getting one right and one wrong destroys the figure's argument.
- Panels 1 and 2 must not be visually merged, superimposed, or connected. Two maps, side by side, never combined.

**Source ASCII (for designer reference):**
```
   THE PHASES — when a control acts
   ─────────────────────────────────────────────────────────────────

   DEVELOP  ────▶  DISTRIBUTE  ────▶  DEPLOY  ────▶  RUNTIME
                                                       │
                                          ┌────────────┼────────────┐
                                          │            │            │
                                        ACCESS      COMPUTE      STORAGE


   THE LAYERS — where a control acts
   ─────────────────────────────────────────────────────────────────

   ┌─ CLOUD ──────────────────────────────────────────────┐
   │  ┌─ CLUSTER ─────────────────────────────────────┐   │
   │  │  ┌─ CONTAINER ────────────────────────────┐   │   │
   │  │  │  ┌─ CODE ──────────────────────────┐   │   │   │
   │  │  │  │                                 │   │   │   │
   │  │  │  └─────────────────────────────────┘   │   │   │
   │  │  └────────────────────────────────────────┘   │   │
   │  └───────────────────────────────────────────────┘   │
   └──────────────────────────────────────────────────────┘


   FIVE CONTROLS, PLOTTED ON BOTH
   ─────────────────────────────────────────────────────────────────

   control                    phase                layer
   ──────────────────────────────────────────────────────────────
   RBAC                       runtime / access     Cluster
   ServiceAccount             runtime / access     Cluster
   securityContext            runtime / compute    Container
   encryption at rest         runtime / storage    Cloud → Cluster
   image signing              distribute           Container
```

**Proposed filename:** `ch12-fig01-4cs-and-lifecycle-phases.png`

```yaml-figure-spec
anchor_id: ch12-fig01-4cs-and-lifecycle-phases
diagram_type: concept_map
source_ascii: |2
     THE PHASES — when a control acts
     ─────────────────────────────────────────────────────────────────

     DEVELOP  ────▶  DISTRIBUTE  ────▶  DEPLOY  ────▶  RUNTIME
                                                         │
                                            ┌────────────┼────────────┐
                                            │            │            │
                                          ACCESS      COMPUTE      STORAGE


     THE LAYERS — where a control acts
     ─────────────────────────────────────────────────────────────────

     ┌─ CLOUD ──────────────────────────────────────────────┐
     │  ┌─ CLUSTER ─────────────────────────────────────┐   │
     │  │  ┌─ CONTAINER ────────────────────────────┐   │   │
     │  │  │  ┌─ CODE ──────────────────────────┐   │   │   │
     │  │  │  │                                 │   │   │   │
     │  │  │  └─────────────────────────────────┘   │   │   │
     │  │  └────────────────────────────────────────┘   │   │
     │  └───────────────────────────────────────────────┘   │
     └──────────────────────────────────────────────────────┘


     FIVE CONTROLS, PLOTTED ON BOTH
     ─────────────────────────────────────────────────────────────────

     control                    phase                layer
     ──────────────────────────────────────────────────────────────
     RBAC                       runtime / access     Cluster
     ServiceAccount             runtime / access     Cluster
     securityContext            runtime / compute    Container
     encryption at rest         runtime / storage    Cloud → Cluster
     image signing              distribute           Container
vendor_terms: []
complexity_hint:
  node_count: 16
  edge_count: 9
  label_count: 32
pedagogy:
  part_18_criteria_met: [spatial_structure, temporal_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Place any Kubernetes security control on both maps at once — which lifecycle phase it acts in and which of the 4C layers it protects — and recognise the two coordinates as independent"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the 'phase' and 'layer' column headers in the five-control table, accented as a matched pair of independent axes"
accessibility:
  alt_text_seed: "Three-panel figure: four lifecycle phases in sequence from develop to runtime with runtime branching into access, compute and storage; four nested layers from Cloud outermost to Code innermost; and a table plotting five security controls against both a phase and a layer"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "The 4Cs model and the develop/distribute/deploy/runtime phases are Kubernetes documentation concepts, redrawn in Lodestar's visual language; no CNCF diagram, logo or mark is reproduced."
```

---

## Figure: ch12-fig03-serviceaccount-token-flow

**Anchor ID:** `ch12-fig03-serviceaccount-token-flow`
**Draft location:** `draft-v1.md:293` (anchor), fenced block `294–328`, §2 — Who You Are
**Purpose:** Draws the chapter's central Fixed Point — that identity and permission are two different things in two different objects — by tracing a ServiceAccount token all the way to a *successful* authentication and then showing the authorization gate standing conspicuously empty.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Vertical flow diagram with side annotations and one deliberately empty terminal node

**Content specification:**

A single top-to-bottom flow of five stages down the left, each an outlined box, with right-hand annotation text set outside the box in a lighter weight. **Stage 1:** a two-line box reading "ServiceAccount" / "ns/my-app", annotated to its right "a namespaced object in the API server — an IDENTITY, and nothing more". An arrow down, labelled `spec.serviceAccountName: my-app`. **Stage 2:** "TokenRequest API", annotated "short-lived, automatically rotating". Arrow down. **Stage 3:** a wider box labelled "Pod", containing an indented line "projected volume" and beneath it a further-indented "token", with a short left-pointing arrow into "token" labelled "mounted, rotated". Arrow down, labelled "API request, bearing the token". **Stage 4:** a two-line box "GATE 1" / "AUTHENTICATION", annotated with the question `"who are you?"` and the result `✔ you are ns/my-app`. Arrow down. **Stage 5:** a two-line box "GATE 2" / "AUTHORIZATION", annotated with the question `"what may you do?"` — and this box is drawn **empty**, an ellipsis sitting where its content would be, with a small callout box to its right joined by a left-pointing arrow reading "nothing here yet. see §3."

That emptiness is the entire argument of the figure and must survive redrawing. A designer's instinct will be to fill, balance, or tidy Gate 2 so the composition resolves; resisting that instinct is the job. Gate 1 carries a checkmark and a result; Gate 2 carries a question and nothing else.

**Visual style:**
- Palette: inherit book default (brand navy line work); the Gate 2 box uses the same stroke weight as Gate 1 — it is empty, not faded or provisional
- Size (pixels): 900 × 1200 portrait (3:4). Lay the five stages out to fill that frame; do not produce a thin tall column, which reflows badly and forces the type below legibility
- Font: inherit book default — Fira Mono for `spec.serviceAccountName: my-app`, `ns/my-app`, and the object names; Fira Sans for annotation prose
- Accent colour for highlighted elements: Brass `#B58B3E` on the empty GATE 2 box and its "nothing here yet" callout

**Critical details (non-negotiable accuracy):**
- The ServiceAccount box is labelled as an identity **and nothing more**. Do not add a Role, ClusterRole, RoleBinding, or any permission object anywhere in this figure. The figure's argument is that none exists yet.
- GATE 2 must be visibly empty. Do not add a verdict glyph, a cross, a deny symbol, a red mark, or a "403". Authorization has not been described at this point in the chapter; a cross would state an outcome the figure is not entitled to state.
- Gate order is authentication first, then authorization. Never reversed.
- The token reaches the Pod by **projection** from the TokenRequest API. Do not draw a Secret object anywhere in this figure — §2 is explicit that the Secret-backed token is the legacy path and is not what this depicts.
- The `✔` belongs to GATE 1 only.
- The namespace-qualified name `ns/my-app` must be spelled identically in the ServiceAccount box and in the Gate 1 result line — that identity is the same string in both places, and the repetition is the point.
- The word "rotated" appears on the token arrow. Do not drop it; token rotation is a tested fact in this section.

**Source ASCII (for designer reference):**
```
   ┌──────────────────────┐
   │  ServiceAccount      │      a namespaced object in the API server
   │  ns/my-app           │      — an IDENTITY, and nothing more
   └──────────┬───────────┘
              │
              │  spec.serviceAccountName: my-app
              ▼
   ┌──────────────────────┐
   │  TokenRequest API    │      short-lived, automatically rotating
   └──────────┬───────────┘
              │
              ▼
   ┌──────────────────────────────────────────┐
   │  Pod                                     │
   │    projected volume                      │
   │      └── token  ◀── mounted, rotated     │
   └──────────┬───────────────────────────────┘
              │
              │  API request, bearing the token
              ▼
   ┌──────────────────────┐
   │  GATE 1              │      "who are you?"
   │  AUTHENTICATION      │      ✔ you are ns/my-app
   └──────────┬───────────┘
              │
              ▼
   ┌──────────────────────┐
   │  GATE 2              │      "what may you do?"
   │  AUTHORIZATION       │
   │                      │      ┌─────────────────────────┐
   │      ...             │◀─────┤  nothing here yet.      │
   │                      │      │  see §3.                │
   └──────────────────────┘      └─────────────────────────┘
```

**Proposed filename:** `ch12-fig03-serviceaccount-token-flow.png`

```yaml-figure-spec
anchor_id: ch12-fig03-serviceaccount-token-flow
diagram_type: flowchart
source_ascii: |2
     ┌──────────────────────┐
     │  ServiceAccount      │      a namespaced object in the API server
     │  ns/my-app           │      — an IDENTITY, and nothing more
     └──────────┬───────────┘
                │
                │  spec.serviceAccountName: my-app
                ▼
     ┌──────────────────────┐
     │  TokenRequest API    │      short-lived, automatically rotating
     └──────────┬───────────┘
                │
                ▼
     ┌──────────────────────────────────────────┐
     │  Pod                                     │
     │    projected volume                      │
     │      └── token  ◀── mounted, rotated     │
     └──────────┬───────────────────────────────┘
                │
                │  API request, bearing the token
                ▼
     ┌──────────────────────┐
     │  GATE 1              │      "who are you?"
     │  AUTHENTICATION      │      ✔ you are ns/my-app
     └──────────┬───────────┘
                │
                ▼
     ┌──────────────────────┐
     │  GATE 2              │      "what may you do?"
     │  AUTHORIZATION       │
     │                      │      ┌─────────────────────────┐
     │      ...             │◀─────┤  nothing here yet.      │
     │                      │      │  see §3.                │
     └──────────────────────┘      └─────────────────────────┘
vendor_terms: []
complexity_hint:
  node_count: 7
  edge_count: 7
  label_count: 16
pedagogy:
  part_18_criteria_met: [temporal_structure, fixed_point]
  learning_outcome: "Distinguish a workload identity from a permission by tracing a ServiceAccount token to a successful authentication and finding authorization still empty"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the empty GATE 2 / AUTHORIZATION box together with its 'nothing here yet. see §3.' callout"
accessibility:
  alt_text_seed: "Vertical flow from a ServiceAccount object through the TokenRequest API to a Pod's projected token volume, then to gate one authentication which succeeds, then to gate two authorization which is drawn empty with a note reading nothing here yet"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes object and API names appear as text only; the flow, framing and the empty-gate device are the book's own."
```

---

## Figure: ch12-fig02-rbac-four-way-matrix

**Anchor ID:** `ch12-fig02-rbac-four-way-matrix`
**Draft location:** `draft-v1.md:398` (anchor), fenced block `399–446`, §3 — What You May Do
**Purpose:** Replaces the memorised two-by-two RBAC table with a derivation: the reader starts from the namespaced/cluster-scoped boundary they already hold from Chapter 4, asks two independent questions, and watches the four object combinations fall out — including the one that does not exist.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Three-panel derivation diagram — two independent decision forks, an outcome list, and a rule banner

**Content specification:**

Three stacked panels under small-caps titles, closed by a full-width banner.

**Panel 1, "THE BOUNDARY YOU ALREADY HAVE (Ch 4 §3)":** two columns side by side. Left column heads "NAMESPACED resource", subtitled "lives inside a namespace", with the example list "Pod, Service, Secret, Deployment, ConfigMap". Right column heads "CLUSTER-SCOPED resource", subtitled "lives in NO namespace", with "Node, PersistentVolume, StorageClass, Namespace". A long downward arrow descends from each column — the left annotated "a Role's scope has room for it", the right annotated "a Role has nowhere to put it" — terminating in two boxes: left reads "Role / or ClusterRole", right reads "ClusterRole / FORCED". Between the two boxes sits a short horizontal annotation, `◀── either ──`, its arrowhead pointing at the *left* box, marking that case as a free choice while the right case is compelled.

**Panel 2, "THE SECOND, INDEPENDENT QUESTION":** the question "where should the grant apply?" at the top, a stem dropping and forking into two branches labelled "one namespace" and "every namespace", each descending to a box — "RoleBinding" and "ClusterRoleBinding" respectively.

**Panel 3, "THE FOUR COMBINATIONS FALL OUT":** four rows, each pairing two objects with a right arrow to its result. Role + RoleBinding → those rules, in that namespace. ClusterRole + RoleBinding → those rules, in that ONE namespace (with ONE emphasised). ClusterRole + ClusterRoleBinding → those rules, everywhere. Role + ClusterRoleBinding → ✗ does not exist, followed by the reason "A Role's rules are namespace-local; there is nothing cluster-wide to grant."

Beneath all three panels, a full-width bordered banner carrying a right-pointing marker and the sentence "THE BINDING DETERMINES THE SCOPE OF THE GRANT." This banner is the section's ★ Fixed Point and takes the Brass accent.

**Visual style:**
- Palette: inherit book default (brand navy line work); the two-column split in panel 1 uses spacing and rule weight, not two different hues
- Size (pixels): 900 × 1200 portrait (3:4 — three stacked panels plus a banner; do not exceed 3:4 height)
- Font: inherit book default — Fira Mono for every object name (Role, ClusterRole, RoleBinding, ClusterRoleBinding) and every resource name; Fira Sans for the annotations and results; Roboto Slab for the panel titles and the banner
- Accent colour for highlighted elements: Brass `#B58B3E` on the banner; a second, lighter accent weight (not a second hue) on the word FORCED and on the ✗ row

**Critical details (non-negotiable accuracy):**
- The fourth combination — Role + ClusterRoleBinding — must be marked as **non-existent** (✗) with its reason attached. It is not a discouraged option or an anti-pattern; there is no such object pairing. Do not render panel 3 as a 2×2 grid with a shaded fourth cell, which reads as "valid but inadvisable."
- Panels 1 and 2 must **not** be redrawn as a single sequential decision tree. They are two independent questions, and the whole pedagogical point is that the second does not depend on the answer to the first. Keep them as separate, visually parallel panels with no connector between them.
- The right branch of panel 1 says ClusterRole is **FORCED**, not preferred or recommended. Keep the word.
- The example resources are correctly sorted and must not be moved across columns: Pod, Service, Secret, Deployment, ConfigMap are namespaced; Node, PersistentVolume, StorageClass, Namespace are cluster-scoped.
- `Namespace` itself belongs in the **cluster-scoped** column. This looks like an error and is not — a Namespace object is not in a namespace.
- The emphasis on ONE in "those rules, in that ONE namespace" must survive redrawing; that word is what distinguishes row two from row three.
- The `◀── either ──` arrowhead points **left**, at the Role-or-ClusterRole box. Reversing it says the forced case is the free one.

**Source ASCII (for designer reference):**
```
   THE BOUNDARY YOU ALREADY HAVE  (Ch 4 §3)
   ─────────────────────────────────────────

   NAMESPACED resource                       CLUSTER-SCOPED resource
   lives inside a namespace                  lives in NO namespace
   Pod, Service, Secret,                     Node, PersistentVolume,
   Deployment, ConfigMap                     StorageClass, Namespace
        │                                            │
        │                                            │
        │  a Role's scope has room for it            │  a Role has nowhere
        │                                            │  to put it
        ▼                                            ▼
   ┌─────────────────────┐                  ┌─────────────────────┐
   │ Role                │                  │ ClusterRole         │
   │  or ClusterRole     │  ◀── either ──   │  FORCED             │
   └─────────────────────┘                  └─────────────────────┘


   THE SECOND, INDEPENDENT QUESTION
   ─────────────────────────────────────────

        where should the grant apply?
                  │
        ┌─────────┴──────────┐
        ▼                    ▼
   one namespace        every namespace
        │                    │
        ▼                    ▼
   ┌──────────────┐    ┌─────────────────────┐
   │ RoleBinding  │    │ ClusterRoleBinding  │
   └──────────────┘    └─────────────────────┘


   THE FOUR COMBINATIONS FALL OUT
   ─────────────────────────────────────────

   Role      + RoleBinding         → those rules, in that namespace
   ClusterRole + RoleBinding       → those rules, in that ONE namespace
   ClusterRole + ClusterRoleBinding→ those rules, everywhere
   Role      + ClusterRoleBinding  → ✗ does not exist. A Role's rules
                                       are namespace-local; there is
                                       nothing cluster-wide to grant.

   ┌───────────────────────────────────────────────────────────────┐
   │  ▶  THE BINDING DETERMINES THE SCOPE OF THE GRANT.            │
   └───────────────────────────────────────────────────────────────┘
```

**Proposed filename:** `ch12-fig02-rbac-four-way-matrix.png`

```yaml-figure-spec
anchor_id: ch12-fig02-rbac-four-way-matrix
diagram_type: flowchart
source_ascii: |2
     THE BOUNDARY YOU ALREADY HAVE  (Ch 4 §3)
     ─────────────────────────────────────────

     NAMESPACED resource                       CLUSTER-SCOPED resource
     lives inside a namespace                  lives in NO namespace
     Pod, Service, Secret,                     Node, PersistentVolume,
     Deployment, ConfigMap                     StorageClass, Namespace
          │                                            │
          │                                            │
          │  a Role's scope has room for it            │  a Role has nowhere
          │                                            │  to put it
          ▼                                            ▼
     ┌─────────────────────┐                  ┌─────────────────────┐
     │ Role                │                  │ ClusterRole         │
     │  or ClusterRole     │  ◀── either ──   │  FORCED             │
     └─────────────────────┘                  └─────────────────────┘


     THE SECOND, INDEPENDENT QUESTION
     ─────────────────────────────────────────

          where should the grant apply?
                    │
          ┌─────────┴──────────┐
          ▼                    ▼
     one namespace        every namespace
          │                    │
          ▼                    ▼
     ┌──────────────┐    ┌─────────────────────┐
     │ RoleBinding  │    │ ClusterRoleBinding  │
     └──────────────┘    └─────────────────────┘


     THE FOUR COMBINATIONS FALL OUT
     ─────────────────────────────────────────

     Role      + RoleBinding         → those rules, in that namespace
     ClusterRole + RoleBinding       → those rules, in that ONE namespace
     ClusterRole + ClusterRoleBinding→ those rules, everywhere
     Role      + ClusterRoleBinding  → ✗ does not exist. A Role's rules
                                         are namespace-local; there is
                                         nothing cluster-wide to grant.

     ┌───────────────────────────────────────────────────────────────┐
     │  ▶  THE BINDING DETERMINES THE SCOPE OF THE GRANT.            │
     └───────────────────────────────────────────────────────────────┘
vendor_terms: []
complexity_hint:
  node_count: 14
  edge_count: 11
  label_count: 30
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Derive which of Role, ClusterRole, RoleBinding and ClusterRoleBinding a situation calls for from the namespaced/cluster-scoped boundary, rather than from a memorised matrix"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the closing banner reading THE BINDING DETERMINES THE SCOPE OF THE GRANT"
accessibility:
  alt_text_seed: "Three-panel derivation: namespaced resources permit either a Role or a ClusterRole while cluster-scoped resources force a ClusterRole; a separate question of where the grant applies selects a RoleBinding or a ClusterRoleBinding; four combinations follow, of which Role plus ClusterRoleBinding does not exist; a banner states that the binding determines the scope of the grant"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes RBAC object names appear as text only; the two-question derivation and the banner are the book's own framing, not reproduced from Kubernetes documentation."
```

---

## Figure: ch12-fig04-pod-security-standards-levels

**Anchor ID:** `ch12-fig04-pod-security-standards-levels`
**Draft location:** `draft-v1.md:876` (anchor), fenced block `877–928`, §6 — Three Levels, Three Modes
**Purpose:** Lets the reader read a namespace's Pod Security labels and a Pod's `securityContext` together and predict the outcome, by laying the three levels out field by field against the three modes and showing they are independent axes.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Three-panel composite — comparison matrix, a three-way outcome list, and a label-syntax callout with worked example

**Content specification:**

Three stacked panels, each under a small-caps title above a **double** rule (the ASCII uses `═` for these headings and a single `─` for the matrix's internal header rule; preserve that distinction in weight).

**Panel 1, "THE LEVELS — what gets checked":** a matrix whose first column lists a `securityContext` field and whose remaining three columns are headed *privileged*, *baseline*, *restricted*. Fourteen field rows, exactly as in the source. Cells reading "✗ forbidden" must be visually distinct from cells reading "allowed"; cells reading "—" mean the level says nothing about that field and should read as neutral, not as permission. Beneath the matrix, one summary line — "cumulative: privileged ⊃ baseline ⊃ restricted" — with the parenthetical gloss "(restricted includes every baseline requirement, plus the rows below the line)".

**Panel 2, "THE MODES — what happens when a check fails":** three lines, each an arrow from a mode name to its consequence — enforce ──▶ the Pod is REJECTED; audit ──▶ recorded in the audit log; the Pod runs; warn ──▶ user-facing warning; the Pod runs.

**Panel 3, "APPLIED PER NAMESPACE, BY LABEL":** the label form `pod-security.kubernetes.io/<MODE>: <LEVEL>` set prominently in monospace, then a three-line worked example (`enforce: baseline`, `warn: restricted`, `audit: restricted`), then an upward-pointing marker with the note "all three, on one namespace, at two different levels. This is not a contradiction. It is a migration."

The Brass accent goes on the two panel subtitles — "what gets checked" and "what happens when a check fails" — because the independence of level and mode is the ★ Fixed Point this figure carries, and those two phrases are where the reader's eye should land first.

**Visual style:**
- Palette: inherit book default (brand navy). The three level columns must be distinguishable by column rule and cell treatment; do not encode the three levels in three hues alone
- Size (pixels): 900 × 1200 portrait (3:4). The matrix is the tallest element; if it will not fit legibly at 3:4, reduce the leading rather than exceeding the aspect ratio
- Font: inherit book default — **Fira Mono for every field name, value, level name, mode name, and label key** (they are all API terminology and read as code); Fira Sans for prose annotation; Roboto Slab for the three panel titles
- Accent colour for highlighted elements: Brass `#B58B3E` on the phrases "what gets checked" and "what happens when a check fails"

**Critical details (non-negotiable accuracy):**
- Three levels only — `privileged`, `baseline`, `restricted` — and three modes only — `enforce`, `audit`, `warn`. No term appears in both lists. A designer must not swap or borrow a term across panels to balance a column.
- Only `enforce` rejects. Both `audit` and `warn` let the Pod run; that clause must appear on both lines.
- The `⊃` in "privileged ⊃ baseline ⊃ restricted" reads as "permits a superset of": privileged is the most permissive, restricted the least. Do not reverse the symbol, reorder the three names, or "correct" it to point the other way.
- `capabilities.add` under restricted is `NET_BIND_SERVICE` only. That spelling — with no `CAP_` prefix — is correct and required; §5 establishes that manifests omit the prefix.
- `runAsUser` under restricted reads "must be non-zero **or unset**". Both halves. Dropping "or unset" states a rule the standard does not impose.
- The `<MODE>` and `<LEVEL>` placeholders keep their angle brackets in the label-form line; the three lines beneath substitute real values for them.
- The worked example deliberately carries all three modes at **two different levels**. This is a migration pattern, not an error, and must not be normalised to a single level.
- The restricted volume list is illustrative and ends with an ellipsis: "(configMap, csi, emptyDir, secret, projected, pvc, …)". Keep the ellipsis; the list is not exhaustive.

**Source ASCII (for designer reference):**
```
   THE LEVELS — what gets checked
   ══════════════════════════════════════════════════════════════════

   securityContext field          privileged   baseline    restricted
   ──────────────────────────────────────────────────────────────────
   privileged: true               allowed      ✗ forbidden ✗ forbidden
   hostNetwork/hostPID/hostIPC    allowed      ✗ forbidden ✗ forbidden
   hostPath volumes               allowed      ✗ forbidden ✗ forbidden
   hostPort                       allowed      restricted  restricted
   capabilities.add               allowed      known list  only
                                                           NET_BIND_SERVICE
   capabilities.drop              —            —           must include ALL
   seccompProfile.type            allowed      not          RuntimeDefault
                                               Unconfined   or Localhost
   appArmorProfile.type           allowed      Runtime      Runtime
                                               Default or   Default or
                                               Localhost    Localhost
   allowPrivilegeEscalation       allowed      —           must be false
   runAsNonRoot                   —            —           must be true
   runAsUser                      any          any         must be non-zero
                                                           or unset
   volume types                   any          any         safe list only
                                                           (configMap, csi,
                                                           emptyDir, secret,
                                                           projected, pvc, …)

   cumulative:  privileged  ⊃  baseline  ⊃  restricted
                (restricted includes every baseline requirement,
                 plus the rows below the line)


   THE MODES — what happens when a check fails
   ══════════════════════════════════════════════════════════════════

           enforce  ──▶  the Pod is REJECTED
           audit    ──▶  recorded in the audit log; the Pod runs
           warn     ──▶  user-facing warning; the Pod runs


   APPLIED PER NAMESPACE, BY LABEL
   ══════════════════════════════════════════════════════════════════

           pod-security.kubernetes.io/<MODE>: <LEVEL>

   e.g.    pod-security.kubernetes.io/enforce: baseline
           pod-security.kubernetes.io/warn:    restricted
           pod-security.kubernetes.io/audit:   restricted

           ▲ all three, on one namespace, at two different levels.
             This is not a contradiction. It is a migration.
```

**Proposed filename:** `ch12-fig04-pod-security-standards-levels.png`

```yaml-figure-spec
anchor_id: ch12-fig04-pod-security-standards-levels
diagram_type: other
source_ascii: |2
     THE LEVELS — what gets checked
     ══════════════════════════════════════════════════════════════════

     securityContext field          privileged   baseline    restricted
     ──────────────────────────────────────────────────────────────────
     privileged: true               allowed      ✗ forbidden ✗ forbidden
     hostNetwork/hostPID/hostIPC    allowed      ✗ forbidden ✗ forbidden
     hostPath volumes               allowed      ✗ forbidden ✗ forbidden
     hostPort                       allowed      restricted  restricted
     capabilities.add               allowed      known list  only
                                                             NET_BIND_SERVICE
     capabilities.drop              —            —           must include ALL
     seccompProfile.type            allowed      not          RuntimeDefault
                                                 Unconfined   or Localhost
     appArmorProfile.type           allowed      Runtime      Runtime
                                                 Default or   Default or
                                                 Localhost    Localhost
     allowPrivilegeEscalation       allowed      —           must be false
     runAsNonRoot                   —            —           must be true
     runAsUser                      any          any         must be non-zero
                                                             or unset
     volume types                   any          any         safe list only
                                                             (configMap, csi,
                                                             emptyDir, secret,
                                                             projected, pvc, …)

     cumulative:  privileged  ⊃  baseline  ⊃  restricted
                  (restricted includes every baseline requirement,
                   plus the rows below the line)


     THE MODES — what happens when a check fails
     ══════════════════════════════════════════════════════════════════

             enforce  ──▶  the Pod is REJECTED
             audit    ──▶  recorded in the audit log; the Pod runs
             warn     ──▶  user-facing warning; the Pod runs


     APPLIED PER NAMESPACE, BY LABEL
     ══════════════════════════════════════════════════════════════════

             pod-security.kubernetes.io/<MODE>: <LEVEL>

     e.g.    pod-security.kubernetes.io/enforce: baseline
             pod-security.kubernetes.io/warn:    restricted
             pod-security.kubernetes.io/audit:   restricted

             ▲ all three, on one namespace, at two different levels.
               This is not a contradiction. It is a migration.
vendor_terms: []
complexity_hint:
  node_count: 17
  edge_count: 4
  label_count: 60
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Read a namespace's Pod Security labels together with a Pod's securityContext and predict whether the Pod is admitted, warned about, or refused"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the two panel subtitles 'what gets checked' and 'what happens when a check fails', accented as the level axis against the mode axis"
accessibility:
  alt_text_seed: "A matrix of fourteen securityContext fields checked against the privileged, baseline and restricted Pod Security levels, noted as cumulative; a list of the three modes enforce, audit and warn with what each does when a check fails; and the per-namespace label form with a worked example carrying all three modes at two different levels"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Pod Security Standards field, level and mode names are Kubernetes API terminology quoted as text; the matrix layout, the mode panel and the migration note are the book's own composition."
```

---

## Figure: ch12-fig05-supply-chain-checkpoints

**Anchor ID:** `ch12-fig05-supply-chain-checkpoints`
**Draft location:** `draft-v1.md:1063` (anchor), fenced block `1064–1090`, §7 — Trusting What You Ship
**Purpose:** Traces an image from build to running container, names the checkpoint at each handoff, and — the section's whole argument — marks the single point at which the cluster stops trusting somebody else's word and checks for itself.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Horizontal pipeline with a trust boundary, per-step annotations, a tool row, and one callout

**Content specification:**

A single horizontal pipeline runs left to right across the upper third: BUILD → SCAN → SIGN → RECORD → RESTRICT → VERIFY → RUN, joined by six right-pointing arrows. A prominent vertical boundary line crosses the whole figure between RESTRICT and VERIFY, headed "OUTSIDE THE CLUSTER" on the left and "INSIDE" on the right; the pipeline arrow passes cleanly *through* the boundary rather than stopping at it. Beneath six of the seven steps, a short downward tick leads to an annotation: BUILD → "image / +digest / +SBOM"; SCAN → "known CVEs"; SIGN → "binds to the DIGEST"; RECORD → "append-only log"; RESTRICT → "private registry"; VERIFY → "admission controller". A callout box sits below the BUILD–SIGN span, joined by an upward arrow to the word DIGEST, reading "the artifact's identity — the same digest — is carried the whole length of the chain".

A bottom row places tool names under their own step: "Trivy, Harbor scanners" under SCAN; "Cosign, Notation, Fulcio" under SIGN; "Rekor" under RECORD; "Harbor, imagePullSecrets" under RESTRICT; "Kyverno, Gatekeeper, Policy Controller" under VERIFY. A final left-pointing note runs along the bottom left: "everything left of the line happened somewhere else, under somebody else's control, possibly months ago. VERIFY is the first checkpoint the cluster performs itself."

The vertical boundary is the point of the figure and takes the accent. It must read as a threshold being crossed, not as a decorative panel divider — heavier than any other rule on the page.

**Visual style:**
- Palette: inherit book default (brand navy); the left/outside region may carry a very light tone wash to separate it from the inside region, provided the wash survives greyscale as a value difference
- Size (pixels): 1200 × 750 landscape. This is the one wide figure in the chapter; landscape is correct here and reflows acceptably
- Font: inherit book default — Fira Mono for `imagePullSecrets` and for the project names in the tool row; Fira Sans for the step annotations and the closing note; Roboto Slab for the seven step names
- Accent colour for highlighted elements: Brass `#B58B3E` on the vertical cluster boundary and on the VERIFY step

**Critical details (non-negotiable accuracy):**
- Step order is exactly BUILD, SCAN, SIGN, RECORD, RESTRICT, VERIFY, RUN. Scanning precedes signing (you do not attest to content you have not examined) and recording follows signing (the transparency log records signing events). Reordering either pair states something the chapter explicitly marks as a wrong answer.
- The boundary falls **between RESTRICT and VERIFY**. VERIFY and RUN are the only two steps inside the cluster; the other five are outside it.
- The digest callout attaches to **SIGN**, via an arrow to the word DIGEST. It does not attach to BUILD, to RECORD, or to the pipeline as a whole.
- Tool names sit under the correct step. **Harbor appears twice** — under SCAN as a scanner and under RESTRICT as a private registry — and that repetition is deliberate; do not de-duplicate it.
- BUILD has no tool names beneath it. Do not invent any to fill the column.
- This is the chapter's only pipeline-family figure, so per the series glyph decision it is the only one permitted semantic Lucide glyphs — one glyph, one meaning, per `certcomp-diagrams/assets/glyph-ledger.yaml`. The other five figures in this chapter stay glyph-free.
- **Set every project name as plain text in the book's own faces.** Do not substitute a vendor logo or wordmark for any of Trivy, Harbor, Cosign, Notation, Fulcio, Rekor, Kyverno, Gatekeeper or Policy Controller — doing so changes the copyright clearance recorded below and requires re-review before render.

**Source ASCII (for designer reference):**
```
   OUTSIDE THE CLUSTER                              │   INSIDE
   ═════════════════════════════════════════════════╪═══════════
                                                    │
   BUILD ──▶ SCAN ──▶ SIGN ──▶ RECORD ──▶ RESTRICT ─┼─▶ VERIFY ──▶ RUN
     │         │        │         │          │      │      │
     │         │        │         │          │      │      │
     ▼         ▼        ▼         ▼          ▼      │      ▼
   image     known    binds     append-    private  │   admission
   +digest   vulns    to the    only log   registry │   controller
   +SBOM              DIGEST                        │
                        ▲                           │   ▲
     ┌──────────────────┴─────────────┐             │   │
     │  the artifact's identity —     │             │   │
     │  the same digest — is carried  │             │   │
     │  the whole length of the chain │             │   │
     └────────────────────────────────┘             │   │
                                                    │   │
   Harbor,          Cosign     Rekor    Harbor,     │  Kyverno,
   image scanners   Notation            imagePull-  │  Gatekeeper,
                    Fulcio              Secrets     │  Policy
                                                    │  Controller
                                                    │
   ◀── everything left of the line happened somewhere else,
       under somebody else's control, possibly months ago.
       VERIFY is the first checkpoint the cluster performs itself.
```

**Proposed filename:** `ch12-fig05-supply-chain-checkpoints.png`

```yaml-figure-spec
anchor_id: ch12-fig05-supply-chain-checkpoints
diagram_type: data_flow
source_ascii: |2
     OUTSIDE THE CLUSTER                              │   INSIDE
     ═════════════════════════════════════════════════╪═══════════
                                                      │
     BUILD ──▶ SCAN ──▶ SIGN ──▶ RECORD ──▶ RESTRICT ─┼─▶ VERIFY ──▶ RUN
       │         │        │         │          │      │      │
       │         │        │         │          │      │      │
       ▼         ▼        ▼         ▼          ▼      │      ▼
     image     known    binds     append-    private  │   admission
     +digest   vulns    to the    only log   registry │   controller
     +SBOM              DIGEST                        │
                          ▲                           │   ▲
       ┌──────────────────┴─────────────┐             │   │
       │  the artifact's identity —     │             │   │
       │  the same digest — is carried  │             │   │
       │  the whole length of the chain │             │   │
       └────────────────────────────────┘             │   │
                                                      │   │
     Harbor,          Cosign     Rekor    Harbor,     │  Kyverno,
     image scanners   Notation            imagePull-  │  Gatekeeper,
                      Fulcio              Secrets     │  Policy
                                                      │  Controller
                                                      │
     ◀── everything left of the line happened somewhere else,
         under somebody else's control, possibly months ago.
         VERIFY is the first checkpoint the cluster performs itself.
vendor_terms: [trivy, harbor, cosign, notation, fulcio, rekor, kyverno, gatekeeper, sigstore-policy-controller]
complexity_hint:
  node_count: 21
  edge_count: 13
  label_count: 32
pedagogy:
  part_18_criteria_met: [temporal_structure, spatial_structure, fixed_point]
  learning_outcome: "Trace an image from build to running container, name the checkpoint at each handoff, and identify verification at admission as the first checkpoint the cluster performs itself"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the vertical cluster boundary falling between RESTRICT and VERIFY, together with the VERIFY step immediately to its right"
accessibility:
  alt_text_seed: "A left-to-right supply chain pipeline of build, scan, sign, record, restrict, verify and run, crossed by a vertical boundary between restrict and verify that separates work done outside the cluster from work done inside it; each step is annotated with what it produces and with the tools that perform it, and a callout notes that the artifact's digest is carried the whole length of the chain"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf, openssf, aqua-security]
  clearance: own_interpretation
  notes: "Project names (Trivy, Harbor, Cosign, Notation, Fulcio, Rekor, Kyverno, Gatekeeper, Policy Controller) appear as plain text set in the book's own faces; no logo or wordmark is reproduced. Substituting any vendor logo or icon-pack mark changes this clearance and must be re-reviewed before render."
```

---

## Figure: ch12-zenith-additive-never-deny

> ⚠ **Anchor ID does not conform to `ch{NN}-fig{MM}-{kebab-slug}`.** See Flag 1 at the head of this document. The ID is preserved verbatim below as the join key; renaming is an author-review decision, with `ch12-fig06-additive-never-deny` suggested.

**Anchor ID:** `ch12-zenith-additive-never-deny`
**Draft location:** `draft-v1.md:1337` (anchor), fenced block `1338–1369`, §9 — Additive, Never Deny
**Purpose:** Carries the chapter's ☀️ Zenith — that RBAC and NetworkPolicy, built by different people at different layers for unrelated problems, converged independently on the same design — by drawing both as the same picture and letting the reader see the sameness before reading either label.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Twin parallel flow diagram — two structurally identical panels with a shared caption

**Content specification:**

Two panels of **identical geometry**, side by side, each a bordered box with a two-line header separated from the body by an internal rule. Left header: "RBAC" / "the API layer". Right header: "NETWORKPOLICY" / "the network layer".

Each body carries the same vertical flow. A start label (left "identity", right "Pod"), arrow down. An event label (left "API request", right "connection"), arrow down. A small bordered decision box (left "grant?", right "allow rule?"). From the decision, a stem forks into two downward branches: the left branch terminates immediately at the word "allow"; the right branch reaches a parenthesised "(nothing)" and *continues*, arrow down, to a two-line outcome "denied by" / "ABSENCE". At the foot of each panel sits an identical small bordered box reading "no deny rule exists".

Beneath and centred under both panels, two lines of caption: "different layer.  different object.  different decade." then, on its own line, "the same shape."

The figure's entire argument is carried by symmetry. The two panels must be geometrically identical — same box dimensions, same positions, same arrow lengths, same baselines — so a reader registers *these are the same picture* before reading a single label. Any asymmetry introduced for visual balance, and any attempt to differentiate the two panels by colour, weight, or ornament, destroys the point the section spent two chapters setting up.

**Visual style:**
- Palette: inherit book default (brand navy). **Both panels use identical treatment** — no per-panel hue, tint, or border weight difference. They are the same drawing twice
- Size (pixels): 1200 × 900 landscape (4:3). Two panels side by side; keep generous gutter between them so they read as two objects, not one wide box
- Font: inherit book default — Roboto Slab for the two panel headers, Fira Sans for the flow labels, Fira Mono for "RBAC" and "NETWORKPOLICY"; the caption in Fira Sans italic
- Accent colour for highlighted elements: Brass `#B58B3E` on both "ABSENCE" labels, applied identically in each panel. (This figure carries a ☀️ Zenith rather than a ★ Fixed Point; the structured block flags it as `zenith` in `part_18_criteria_met` while still using the `fixed_point_emphasis` field to nominate the accented element.)

**Critical details (non-negotiable accuracy):**
- The two panels must be structurally identical. **Only six text labels differ:** RBAC / NETWORKPOLICY, "the API layer" / "the network layer", "identity" / "Pod", "API request" / "connection", "grant?" / "allow rule?". Everything else — every box, every arrow, every position — is the same in both.
- "(nothing)" stays parenthesised and stays a bare label, never a box. It represents the absence of a rule, and boxing it would make absence look like a thing.
- The "denied by ABSENCE" outcome hangs **only** from the "(nothing)" branch. The "allow" branch terminates immediately and has no further arrow beneath it.
- Neither panel may contain a deny path, a deny box, a red X, or a rejection glyph. There is no deny in either system; drawing one contradicts the entire section.
- The caption is two lines, centred under both panels, belonging to neither. Do not attach it to one panel or split it between them.
- "ABSENCE" is set in the same emphasis in both panels — same weight, same accent, same size.

**Source ASCII (for designer reference):**
```
   ┌─────────────────────────────┐   ┌─────────────────────────────┐
   │  RBAC                       │   │  NETWORKPOLICY              │
   │  the API layer              │   │  the network layer          │
   ├─────────────────────────────┤   ├─────────────────────────────┤
   │                             │   │                             │
   │       identity              │   │          Pod                │
   │          │                  │   │           │                 │
   │          ▼                  │   │           ▼                 │
   │      API request            │   │      connection             │
   │          │                  │   │           │                 │
   │          ▼                  │   │           ▼                 │
   │   ┌─────────────┐           │   │   ┌─────────────┐           │
   │   │ grant?      │           │   │   │ allow rule? │           │
   │   └──────┬──────┘           │   │   └──────┬──────┘           │
   │          │                  │   │          │                  │
   │     ┌────┴────┐             │   │     ┌────┴────┐             │
   │     ▼         ▼             │   │     ▼         ▼             │
   │   allow    (nothing)        │   │   allow    (nothing)        │
   │              │              │   │              │              │
   │              ▼              │   │              ▼              │
   │          denied by          │   │          denied by          │
   │          ABSENCE            │   │          ABSENCE            │
   │                             │   │                             │
   │   ┌──────────────────────┐  │   │   ┌──────────────────────┐  │
   │   │  no deny rule exists │  │   │   │  no deny rule exists │  │
   │   └──────────────────────┘  │   │   └──────────────────────┘  │
   └─────────────────────────────┘   └─────────────────────────────┘

              different layer.  different object.  different decade.
                            the same shape.
```

**Proposed filename:** `ch12-zenith-additive-never-deny.png` *(becomes `ch12-fig06-additive-never-deny.png` if Flag 1's rename is accepted)*

```yaml-figure-spec
anchor_id: ch12-zenith-additive-never-deny
diagram_type: flowchart
source_ascii: |2
     ┌─────────────────────────────┐   ┌─────────────────────────────┐
     │  RBAC                       │   │  NETWORKPOLICY              │
     │  the API layer              │   │  the network layer          │
     ├─────────────────────────────┤   ├─────────────────────────────┤
     │                             │   │                             │
     │       identity              │   │          Pod                │
     │          │                  │   │           │                 │
     │          ▼                  │   │           ▼                 │
     │      API request            │   │      connection             │
     │          │                  │   │           │                 │
     │          ▼                  │   │           ▼                 │
     │   ┌─────────────┐           │   │   ┌─────────────┐           │
     │   │ grant?      │           │   │   │ allow rule? │           │
     │   └──────┬──────┘           │   │   └──────┬──────┘           │
     │          │                  │   │          │                  │
     │     ┌────┴────┐             │   │     ┌────┴────┐             │
     │     ▼         ▼             │   │     ▼         ▼             │
     │   allow    (nothing)        │   │   allow    (nothing)        │
     │              │              │   │              │              │
     │              ▼              │   │              ▼              │
     │          denied by          │   │          denied by          │
     │          ABSENCE            │   │          ABSENCE            │
     │                             │   │                             │
     │   ┌──────────────────────┐  │   │   ┌──────────────────────┐  │
     │   │  no deny rule exists │  │   │   │  no deny rule exists │  │
     │   └──────────────────────┘  │   │   └──────────────────────┘  │
     └─────────────────────────────┘   └─────────────────────────────┘

                different layer.  different object.  different decade.
                              the same shape.
vendor_terms: []
complexity_hint:
  node_count: 16
  edge_count: 10
  label_count: 20
pedagogy:
  part_18_criteria_met: [zenith, distinguishing_alternatives, spatial_structure]
  learning_outcome: "Recognise that RBAC and NetworkPolicy converged independently on additive-only policy with no deny rule, and predict that same shape in an unfamiliar access-control system"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the word ABSENCE in both panels, accented identically so the two outcomes read as one shape"
accessibility:
  alt_text_seed: "Two structurally identical panels side by side, one labelled RBAC at the API layer and one labelled NetworkPolicy at the network layer; in each, a request reaches a check that either allows it or finds nothing, and finding nothing means denied by absence, with a note in both panels that no deny rule exists; the caption reads different layer, different object, different decade, the same shape"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "RBAC and NetworkPolicy named as text only; the twin-panel symmetry device and the caption are the book's own argument, not sourced from any Kubernetes documentation diagram."
```
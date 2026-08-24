Source verified. Now producing the Stage 10 output.

# Image Specifications — KCNA Chapter 6

*Generated from `../Book-KCNA/.pipeline-state/ch-06/draft-v1-prevoice.md`. Every ASCII diagram in the draft has an entry here; every entry corresponds to an anchor in the draft.*

---

## ⚠ SOURCE NOTE — READ BEFORE USING THIS DOCUMENT

**The stage input named in the prompt (`draft-voice.md`) does not exist on disk for any KCNA chapter.** The Stage 9 voice pass writes *in place*: `draft-v1.md` is the voiced text, `draft-v1-prevoice.md` is the preserved pre-voice copy. This is the same condition Chapter 5's Stage 10 documented, and the prompt template's input reference is stale.

**For Chapter 6 there is a second, more serious problem.** The voiced `draft-v1.md` is **truncated**: 24,189 bytes against the pre-voice draft's 119,467. It begins mid-word (`ognition exam can ask about…`) at what is roughly the chapter's Exam Alert section, and it contains **zero** `<!-- FIGURE: -->` anchors and zero fenced diagram blocks. Stage 4 (`2026-08-24T12:13:09Z → 12:24:51Z`) recorded `status: completed` with no error, so the pipeline does not currently know this chapter's voiced draft is a fragment. Sibling chapters do not show this: ch-04 is 104,386 / 104,322 and ch-05 is 109,592 / 109,606 (voiced / pre-voice), i.e. near-parity as expected.

**This document was therefore extracted from `draft-v1-prevoice.md`, which is complete.** That substitution is sound for Stage 10 specifically: figure anchors and ASCII blocks are authored at Stage 3 and are not touched by the voice pass. Verified on Chapter 5, where the anchor count is identical across `draft-v1-prevoice.md`, `draft-v1.md`, and `draft-v2.md` (6 / 6 / 6). Line numbers cited below index the pre-voice draft.

**Action required outside this stage:** re-run Stage 4 for ch-06 before Stage 11. Downstream stages that consume the voiced draft as *prose* — integration check, kb-manifest, draft-v2 — will silently operate on 20% of the chapter until that happens.

---

**Anchor census:** 6 anchor comments, 6 fenced diagram blocks, 1:1 adjacency confirmed (anchors at draft lines 139, 373, 422, 626, 742, 916; fences open at 140, 374, 423, 627, 743, 917). Two further fenced blocks exist (lines 215–224, 234–237) and are terminal transcripts, not diagrams — see below.

---

## UNANCHORED DIAGRAMS

None. Every fenced **diagram** block in the draft is immediately preceded by a `<!-- FIGURE: ... -->` anchor comment.

For completeness, the draft's two remaining fenced blocks were assessed and are **not** diagrams — they are verbatim shell transcripts reproduced as monospace listings, and they require no figure entry:

### ~Line 215 — `kubectl delete pod` / `kubectl get pods` transcript

```
$ kubectl delete pod web-7d4b9c-x8k2q
pod "web-7d4b9c-x8k2q" deleted

$ kubectl get pods
NAME                     READY   STATUS              AGE
web-7d4b9c-4mnzp         1/1     Running             12m
web-7d4b9c-9tvw6         1/1     Running             12m
web-7d4b9c-qh7bl         0/1     ContainerCreating   2s
```

Command output. Renders as a code listing in production, not as art. No anchor needed.

### ~Line 234 — `kubectl scale` transcript

```
$ kubectl scale deployment/web --replicas=5
deployment.apps/web scaled
```

Command output. No anchor needed.

---

## MALFORMED ANCHORS

The following anchor does not conform to the locked `ch{NN}-fig{MM}-{kebab-slug}` format ([LOCKED 2026-04-18], Visuals / Figures).

### `ch06-zenith-control-loop-instantiated` — draft line 916

Missing the `fig{MM}` segment. It reads `ch06-` + `zenith-…` where the format requires `ch06-figMM-…`. Per rule 6 the ID is **preserved unrenamed** in this document so the join key stays stable; renaming is an author-review decision.

**Suggested correction:** `ch06-fig06-control-loop-instantiated` — author to confirm, then update the draft anchor and this document together in one edit so the join key never diverges.

**Note for the book-level index:** this is the *second* consecutive chapter to emit a `ch{NN}-zenith-…` anchor for its ☀️ Zenith figure (ch-05 line 819 produced `ch05-zenith-smallest-deployable-unit`). Two instances is a pattern, not a slip — the drafting prompt appears to encourage naming the Zenith figure after its marker. Worth a one-line clarification in `pipeline/prompts/03_draft.md` that the `fig{MM}` segment is mandatory regardless of which branded marker the figure sits under, rather than fixing this chapter-by-chapter forever.

---

## ANCHOR ORDERING NOTE (advisory, not a format violation)

Figure numbers do not run in document order: `fig01` (line 139) → `fig02` (373) → `fig03` (422) → **`fig05` (626)** → **`fig04` (742)** → *zenith* (916). `fig05` precedes `fig04` in the text.

The likely cause is visible in the prose: `fig04` is the §7 decision tree, which the draft calls "the most practically useful artifact in the chapter," while `fig05` is the §6 StatefulSet contrast. The decision tree was probably numbered first as the chapter's centrepiece, then the §6 figure was inserted ahead of it. Not a lint failure, but the book-level index will read out of sequence. If the author renumbers, `fig04`↔`fig05` and the malformed Zenith anchor should be fixed in the same edit, since all three touch join keys.

---

## Figure: ch06-fig01-deployment-replicaset-pod-ownership

**Anchor ID:** `ch06-fig01-deployment-replicaset-pod-ownership`
**Purpose:** Establishes the chapter's structural key — that the ownership chain has *three* layers, not two, and that the template and the count live on different layers — which §4 and §5 both depend on entirely.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hierarchical ownership tree, three tiers, one-to-one then one-to-many fan-out

**Content specification:**
Draw three vertical tiers connected by downward "owns" arrows. The top tier is a single wide rectangle labelled **`Deployment: web`**, carrying two indented content lines inside it: **`Pod template`** annotated **"what a Pod looks like"**, and **`Update strategy`** annotated **"how to change them"**. A single arrow descends from the bottom edge of that box, labelled **`owns`**, to the second tier: a rectangle of the same width labelled **`ReplicaSet: web-7d4b9c`**, carrying one indented content line, **`replicas: 3`**, annotated **"how many should exist"**. From the bottom edge of the ReplicaSet box, **three** arrows fan out, each labelled **`owns`**, descending to three identical small boxes on the third tier, each labelled **`Pod`** with the sub-label **`(copy of template)`**. Beneath the whole structure, running the full width, place two opposed captions: **`intent flows DOWN`** on the left and **`existence is reported UP`** on the right. The element that is "the point" is the **separation of concerns between tier 1 and tier 2** — the template and update policy on the Deployment, the replica count on the ReplicaSet. That split must be legible at a glance, because it is what makes a rolling update possible (a Deployment can hold two ReplicaSets) and what makes a revision mean what it means (the template lives one layer above the count). Do not draw an arrow from the Deployment directly to any Pod; that inversion is precisely the misreading the section exists to prevent.

**Visual style:**
- Palette: inherit book default (Lodestar Ledgers navy/slate line-art register)
- Size (pixels): 900x680 portrait
- Font: inherit book default (Fira Sans for prose labels, Fira Mono for identifiers such as `web-7d4b9c` and `replicas: 3`)
- Accent color for highlighted elements: Brass `#B58B3E` on the two content lines that carry the split — `Pod template` / `Update strategy` in the Deployment box, and `replicas: 3` in the ReplicaSet box

**Critical details (non-negotiable accuracy):**
- The chain is **Deployment → ReplicaSet → Pod**, in that order, top to bottom. Any render that connects the Deployment to Pods directly contradicts the ★ Fixed Point at draft line 173 and must be rejected.
- **`replicas: 3` sits on the ReplicaSet, never on the Deployment.** This is the single most consequential label placement in the figure.
- **`Pod template` and `Update strategy` sit on the Deployment, never on the ReplicaSet.**
- Exactly **three** Pod boxes, matching `replicas: 3`. A mismatch between the stated count and the drawn count undermines the figure's own arithmetic.
- The ReplicaSet name is a Deployment name plus a hash suffix (`web` → `web-7d4b9c`). Preserve that relationship; it is reused in fig05 and in the §2 transcript, where the Pod names extend the same stem.
- The three Pods are drawn identically. Their interchangeability is a load-bearing fact that fig05 later contrasts against.

**Source ASCII (for designer reference):**
```
        ┌──────────────────────────────────────────────┐
        │  Deployment: web                             │
        │                                              │
        │    Pod template ......  what a Pod looks like│
        │    Update strategy ...  how to change them   │
        └───────────────────────┬──────────────────────┘
                                │ owns
                                ▼
        ┌──────────────────────────────────────────────┐
        │  ReplicaSet: web-7d4b9c                      │
        │                                              │
        │    replicas: 3 ......  how many should exist │
        └───────┬──────────────┬──────────────┬────────┘
                │ owns         │ owns         │ owns
                ▼              ▼              ▼
        ┌──────────┐   ┌──────────┐   ┌──────────┐
        │   Pod    │   │   Pod    │   │   Pod    │
        │ (copy of │   │ (copy of │   │ (copy of │
        │ template)│   │ template)│   │ template)│
        └──────────┘   └──────────┘   └──────────┘

     intent flows DOWN          existence is reported UP
```

**Proposed filename:** `ch06-fig01-deployment-replicaset-pod-ownership.png`

```yaml-figure-spec
anchor_id: ch06-fig01-deployment-replicaset-pod-ownership
diagram_type: hierarchy_tree
source_ascii: |
          ┌──────────────────────────────────────────────┐
          │  Deployment: web                             │
          │                                              │
          │    Pod template ......  what a Pod looks like│
          │    Update strategy ...  how to change them   │
          └───────────────────────┬──────────────────────┘
                                  │ owns
                                  ▼
          ┌──────────────────────────────────────────────┐
          │  ReplicaSet: web-7d4b9c                      │
          │                                              │
          │    replicas: 3 ......  how many should exist │
          └───────┬──────────────┬──────────────┬────────┘
                  │ owns         │ owns         │ owns
                  ▼              ▼              ▼
          ┌──────────┐   ┌──────────┐   ┌──────────┐
          │   Pod    │   │   Pod    │   │   Pod    │
          │ (copy of │   │ (copy of │   │ (copy of │
          │ template)│   │ template)│   │ template)│
          └──────────┘   └──────────┘   └──────────┘

       intent flows DOWN          existence is reported UP
vendor_terms: [deployment, replicaset, pod]
complexity_hint:
  node_count: 5
  edge_count: 4
  label_count: 9
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "Recall that the ownership chain is Deployment to ReplicaSet to Pod, and that the Deployment holds the Pod template and update policy while the ReplicaSet holds the replica count"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the layer split — Pod template and Update strategy on the Deployment, replicas: 3 on the ReplicaSet"
accessibility:
  alt_text_seed: "A three-tier ownership tree: a Deployment named web, holding the Pod template and update strategy, owns a ReplicaSet named web-7d4b9c, which holds replicas equals three, which in turn owns three identical Pods each a copy of the template; intent flows down the tree and existence is reported up"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: false
  max_width_px: 900
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Ownership chain redrawn from Kubernetes Deployment and ReplicaSet concept docs; no vendor artwork reproduced"
```

---

## Figure: ch06-fig02-rolling-update-maxsurge-maxunavailable

**Anchor ID:** `ch06-fig02-rolling-update-maxsurge-maxunavailable`
**Purpose:** Makes `maxSurge` and `maxUnavailable` spatially non-confusable by showing them as a ceiling above and a floor below the desired replica count, so the reader stops transposing two fields with identical defaults.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** quantitative time-series area chart — stacked old/new Pod counts against a time axis, with two horizontal reference lines and one baseline

**Content specification:**
A chart with Pod count on the vertical axis and time on the horizontal. Three horizontal reference lines span the plot: a **dashed line at 12** labelled **`surge ceiling (10 + 25%)`**, a **solid line at 10** labelled **`desired: 10`**, and a **dashed line at 8** labelled **`availability floor (10 − 25%)`**. Between them, a stacked area shows the rollout: an **old-version** band that begins at full height and shrinks monotonically to zero from left to right, and a **new-version** band that begins at zero and grows to full height, stacked on top of the old band so their **sum** is what the surge ceiling constrains. The combined height briefly rises above the `desired: 10` line — peaking under but near the ceiling — then settles back to 10 as the old band vanishes. The old band's height must never dip below the availability floor early in the sequence. A legend below the plot reads **`██ old version`** and **`░░ new version`**. Two summary captions sit beneath the legend: **`total (old + new) never rises above the surge ceiling`** and **`available never falls below the availability floor`**. The point of the figure is the **vertical relationship between the two bounds and the desired line** — surge is the region *above* 10, unavailability is the region *below* 10. Both bands must be distinguishable by fill pattern (solid versus stipple/hatch), not by hue alone. Axis ticks at 0, 8, 10, 12 only; no other gridlines.

**Visual style:**
- Palette: inherit book default; old version in the darker navy, new version in a lighter slate or hatched fill
- Size (pixels): 1100x620 landscape
- Font: inherit book default (Fira Sans for axis and captions, Fira Mono for `maxSurge` / `maxUnavailable` if named in the render)
- Accent color for highlighted elements: Brass `#B58B3E` on the two dashed bound lines (ceiling and floor) and their labels; the `desired: 10` line stays in the base ink

**Critical details (non-negotiable accuracy):**
- **The surge ceiling is 12 and the availability floor is 8**, from 10 replicas at the 25% defaults. These are not symmetric by accident: `maxSurge` rounds **up** (25% of 10 = 2.5 → 3, total may reach 13) and `maxUnavailable` rounds **down** (2.5 → 2, at least 8 available). If the render labels the ceiling numerically, `10 + 25%` as drawn is the conservative reading; do **not** relabel the floor as 7 or the ceiling as 13 without an author decision, since the source ASCII and the worked arithmetic in the prose sit at slightly different precision.
- **Surge is above the desired line; unavailable is below it.** A render that inverts this destroys the entire mnemonic at draft line 412 and the ★ Fixed Point at 414.
- The **stacked total** is what the ceiling bounds — not either band alone.
- The old band must **shrink** left-to-right and the new band must **grow**. Reversed direction reverses the rollout.
- Both defaults are **25%**. Do not render one as 25% and the other as some other figure to make the chart prettier; their identical defaults are exactly what makes them confusable and is therefore the pedagogical content.
- Time is unitless and unlabelled beyond the arrow. Do not invent durations.

**Source ASCII (for designer reference):**
```
  Pods
   12 ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  surge ceiling (10 + 25%)
      │        ███░░░
   10 ┼────────███░░░───────────────────────  desired: 10
      │  █████████░░░░░░
      │  ██████░░░░░░░░░░░░
    8 ┄┄│┄┄██████┄┄┄┄░░░░░░░░░░┄┄┄┄┄┄┄┄┄┄┄┄┄  availability floor (10 − 25%)
      │  ██████         ░░░░░░░░░
      │  ██████             ░░░░░░░░░░
    0 └──────────────────────────────────────▶ time

        ██ old version        ░░ new version

     total (old + new)  never rises above the surge ceiling
     available          never falls below the availability floor
```

**Proposed filename:** `ch06-fig02-rolling-update-maxsurge-maxunavailable.png`

```yaml-figure-spec
anchor_id: ch06-fig02-rolling-update-maxsurge-maxunavailable
diagram_type: xy_chart
source_ascii: |
    Pods
     12 ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  surge ceiling (10 + 25%)
        │        ███░░░
     10 ┼────────███░░░───────────────────────  desired: 10
        │  █████████░░░░░░
        │  ██████░░░░░░░░░░░░
      8 ┄┄│┄┄██████┄┄┄┄░░░░░░░░░░┄┄┄┄┄┄┄┄┄┄┄┄┄  availability floor (10 − 25%)
        │  ██████         ░░░░░░░░░
        │  ██████             ░░░░░░░░░░
      0 └──────────────────────────────────────▶ time

          ██ old version        ░░ new version

       total (old + new)  never rises above the surge ceiling
       available          never falls below the availability floor
vendor_terms: [deployment, replicaset, pod]
complexity_hint:
  node_count: 2
  edge_count: 3
  label_count: 7
pedagogy:
  part_18_criteria_met: [quantitative_relationships, temporal_structure, fixed_point]
  learning_outcome: "Distinguish maxSurge from maxUnavailable by position relative to the desired replica count — surge bounds the total above the line, unavailable bounds availability below it — and compute both from the 25% defaults"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the two dashed bound lines at 12 and 8 flanking the solid desired line at 10"
accessibility:
  alt_text_seed: "A chart of Pod count against time during a rolling update; a dashed surge ceiling sits at twelve Pods, a solid desired line at ten, and a dashed availability floor at eight; a shrinking band of old-version Pods and a growing band of new-version Pods are stacked so their total briefly exceeds ten without reaching the ceiling, while the available count never drops below the floor"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Chart authored from documented maxSurge/maxUnavailable semantics and defaults; no vendor artwork reproduced"
```

---

## Figure: ch06-fig03-recreate-vs-rolling

**Anchor ID:** `ch06-fig03-recreate-vs-rolling`
**Purpose:** Shows that `Recreate` produces a real availability gap and `RollingUpdate` does not, so the reader can treat `Recreate` as a strategy with a known cost rather than as an error.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** paired comparative timeline — two stacked Gantt-style strips sharing a common time direction

**Content specification:**
Two labelled panels stacked vertically, each a timeline running left to right. The **upper panel**, headed **`Recreate`**, shows an **`old`** bar occupying the left portion of the timeline, then **a gap containing no bar at all**, then a **`new`** bar occupying the right portion. Beneath the gap, a bracket or caret cluster points up into the empty region, annotated on two lines: **`NOTHING IS AVAILABLE`** and **`(this window is the whole point)`**. Segment brackets beneath the axis divide the upper timeline into three phases — old running, the empty window, new running. The **lower panel**, headed **`RollingUpdate`**, shows an **`old`** bar on the left and a **`new`** bar starting *before the old bar ends*, so the two visibly **overlap**. Beneath the overlap region, a caret cluster is annotated **`both versions serving`**. A single unbroken bracket spans the lower timeline — there is no phase division, because there is no gap. Below both panels sits the closing caption **`available count never reaches zero`**, which applies to the RollingUpdate panel. The point of the figure is the **presence of the empty window in the upper panel and its absence in the lower** — the two panels must share the same horizontal scale and alignment so that the eye compares them directly. Use the same old/new fills as fig02 for continuity (solid for old, stipple for new).

**Visual style:**
- Palette: inherit book default; old version solid navy, new version stippled/hatched slate — matching fig02
- Size (pixels): 1000x560 landscape
- Font: inherit book default (Fira Sans for annotations, Fira Mono for the strategy names `Recreate` and `RollingUpdate`)
- Accent color for highlighted elements: Brass `#B58B3E` on the `NOTHING IS AVAILABLE` window in the upper panel — the empty region's boundary markers and its caption only

**Critical details (non-negotiable accuracy):**
- Under **`Recreate`, all existing Pods are killed before any new one is created.** The old and new bars must **not** overlap, and there must be a visible gap between them. Any overlap in the upper panel contradicts the API reference quoted at draft line 420.
- Under **`RollingUpdate`, the old and new bars must overlap.** Both versions serve simultaneously; that is the mechanism.
- The gap in the upper panel is **downtime**, and the figure must present it as deliberate rather than as a fault. No error styling, no red-alert iconography, no "✗" marks — the prose at line 444 argues explicitly that `Recreate` is sometimes the correct answer.
- The lower panel has **no gap anywhere**. The available count never reaches zero.
- Both panels share one horizontal scale. Skewing them defeats the comparison.
- `RollingUpdate` is the **default**; `Recreate` is the opt-in. If the render labels either as default, only `RollingUpdate` may carry that label.

**Source ASCII (for designer reference):**
```
  Recreate
  ────────
   old  ██████████
   new                        ░░░░░░░░░░░░░░░
        ├────────┤ ├────────┤ ├─────────────┤
                   ▲▲▲▲▲▲▲▲▲
                   NOTHING IS AVAILABLE
                   (this window is the whole point)

  RollingUpdate
  ─────────────
   old  ██████████████
   new           ░░░░░░░░░░░░░░░░░░░░░░░░░░░░
        ├──────────────────────────────────┤
                  ▲▲▲▲▲▲▲▲
                  both versions serving

        available count never reaches zero
```

**Proposed filename:** `ch06-fig03-recreate-vs-rolling.png`

```yaml-figure-spec
anchor_id: ch06-fig03-recreate-vs-rolling
diagram_type: gantt
source_ascii: |
    Recreate
    ────────
     old  ██████████
     new                        ░░░░░░░░░░░░░░░
          ├────────┤ ├────────┤ ├─────────────┤
                     ▲▲▲▲▲▲▲▲▲
                     NOTHING IS AVAILABLE
                     (this window is the whole point)

    RollingUpdate
    ─────────────
     old  ██████████████
     new           ░░░░░░░░░░░░░░░░░░░░░░░░░░░░
          ├──────────────────────────────────┤
                    ▲▲▲▲▲▲▲▲
                    both versions serving

          available count never reaches zero
vendor_terms: [deployment]
complexity_hint:
  node_count: 4
  edge_count: 0
  label_count: 9
pedagogy:
  part_18_criteria_met: [temporal_structure, distinguishing_alternatives]
  learning_outcome: "Predict that Recreate produces a window in which no Pods are available while RollingUpdate keeps both versions serving, and treat the Recreate window as a chosen cost rather than a fault"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the empty NOTHING IS AVAILABLE window between the old and new bars in the Recreate panel"
accessibility:
  alt_text_seed: "Two stacked timelines. Under Recreate, an old-version bar ends, a gap follows in which nothing is available, and only then does a new-version bar begin. Under RollingUpdate, the new-version bar starts before the old-version bar ends so the two overlap and both versions serve; the available count never reaches zero"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1100
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Timelines authored from documented Recreate and RollingUpdate strategy semantics; no vendor artwork reproduced"
```

---

## Figure: ch06-fig05-statefulset-vs-deployment-identity

**Anchor ID:** `ch06-fig05-statefulset-vs-deployment-identity`
**Purpose:** Replaces the reader's incoming heuristic ("if it writes to disk, use a StatefulSet") with the correct one — interchangeability — by showing what survives a Pod's death under each resource.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** paired comparative diagram — two labelled panels, each showing three Pods and one replacement event

**Content specification:**
Two panels stacked vertically, each headed by a rule and a title. The **upper panel** is headed **`DEPLOYMENT — Pods are interchangeable`**. It shows three Pod labels in a row: **`web-7d4b9c-4mnzp`**, **`web-7d4b9c-9tvw6`**, **`web-7d4b9c-x8k2q`**. The third carries the annotation **`dies`**, and a downward arrow from it leads to a *new* label, **`web-7d4b9c-qh7bl`**, with the parenthetical **`(different name, different UID)`** beneath. The first two Pods have plain vertical lines descending with nothing attached to them. A caption under the panel reads **`nothing depended on which one it was`**. The **lower panel** is headed **`STATEFULSET — Pods have identity`**. It shows three Pod labels in a row: **`db-0`**, **`db-1`**, **`db-2`**, with `db-2` annotated **`dies`**. Beneath **each** of the three, a short line descends into a small box labelled **`PVC`** with the matching ordinal — **`PVC 0`**, **`PVC 1`**, **`PVC 2`**. To the right of the PVC row, an annotation reads **`storage belongs to the IDENTITY, not to the Pod`**. Below `PVC 2`, an upward arrow rises from a replacement label reading **`db-2 (replacement reattaches)`**, annotated **`same name, same claim`**. The point of the figure is the **contrast between the two replacement events**: in the upper panel the replacement has a *different* name and nothing was attached; in the lower panel the replacement has the *same* name and reattaches to the same claim. Those two arrows are the whole argument and should be the most visually salient elements in their respective panels.

**Visual style:**
- Palette: inherit book default (Lodestar Ledgers navy/slate line-art register)
- Size (pixels): 1000x760 portrait
- Font: inherit book default (Fira Mono for all Pod names, PVC labels, and ordinals; Fira Sans for annotations and captions)
- Accent color for highlighted elements: Brass `#B58B3E` on the lower panel's `db-2` name in **all three** of its appearances (original, PVC-2 binding, replacement) plus the `same name, same claim` arrow — the persistence of that one identifier across the death event is the point

**Critical details (non-negotiable accuracy):**
- **Deployment replacement gets a NEW name and a NEW UID.** `web-7d4b9c-x8k2q` is replaced by `web-7d4b9c-qh7bl` — a different Pod, not the old one recovered. This matches the §2 transcript exactly; keep the names consistent with it.
- **StatefulSet replacement keeps the SAME name.** `db-2` is replaced by `db-2`. If the render gives the replacement a hash suffix or any new identifier, it inverts the concept.
- **Hostnames follow `$(statefulset name)-$(ordinal)`, zero-indexed.** Three replicas produce `db-0`, `db-1`, `db-2` — never `db-1`, `db-2`, `db-3`.
- **Each StatefulSet Pod has its own PVC, bound by ordinal.** `db-0`↔`PVC 0`, `db-1`↔`PVC 1`, `db-2`↔`PVC 2`. Do not draw a shared volume; do not cross the bindings.
- **The Deployment panel must show no storage at all.** This is the subtle trap: the prose at line 658 is explicit that a Deployment's Pod *can* mount a volume, so the figure must not appear to claim otherwise. It shows that nothing *depended on which Pod it was* — absence of dependency, not absence of disk. Do not add a "no storage" ✗ marker or any negation glyph.
- The deciding property is **interchangeability, not disk**, per the ★ Fixed Point at line 654. No label in the render may frame the contrast as stateless-versus-stateful.

**Source ASCII (for designer reference):**
```
  DEPLOYMENT — Pods are interchangeable
  ─────────────────────────────────────
     web-7d4b9c-4mnzp   web-7d4b9c-9tvw6   web-7d4b9c-x8k2q
          │                  │                  │  dies
          │                  │                  ▼
          │                  │            web-7d4b9c-qh7bl
          │                  │            (different name,
          │                  │             different UID)
     nothing depended on which one it was


  STATEFULSET — Pods have identity
  ────────────────────────────────
        db-0              db-1              db-2  dies
         │                 │                 │
      ┌──┴──┐           ┌──┴──┐           ┌──┴──┐
      │ PVC │           │ PVC │           │ PVC │   ← storage belongs
      │  0  │           │  1  │           │  2  │     to the IDENTITY,
      └─────┘           └─────┘           └─────┘     not to the Pod
                                             ▲
                                             │ same name, same claim
                                          db-2 (replacement reattaches)
```

**Proposed filename:** `ch06-fig05-statefulset-vs-deployment-identity.png`

```yaml-figure-spec
anchor_id: ch06-fig05-statefulset-vs-deployment-identity
diagram_type: k8s_architecture
source_ascii: |
    DEPLOYMENT — Pods are interchangeable
    ─────────────────────────────────────
       web-7d4b9c-4mnzp   web-7d4b9c-9tvw6   web-7d4b9c-x8k2q
            │                  │                  │  dies
            │                  │                  ▼
            │                  │            web-7d4b9c-qh7bl
            │                  │            (different name,
            │                  │             different UID)
       nothing depended on which one it was


    STATEFULSET — Pods have identity
    ────────────────────────────────
          db-0              db-1              db-2  dies
           │                 │                 │
        ┌──┴──┐           ┌──┴──┐           ┌──┴──┐
        │ PVC │           │ PVC │           │ PVC │   ← storage belongs
        │  0  │           │  1  │           │  2  │     to the IDENTITY,
        └─────┘           └─────┘           └─────┘     not to the Pod
                                               ▲
                                               │ same name, same claim
                                            db-2 (replacement reattaches)
vendor_terms: [deployment, statefulset, pod, persistentvolumeclaim, pvc]
complexity_hint:
  node_count: 11
  edge_count: 8
  label_count: 14
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Select Deployment versus StatefulSet on the basis of whether Pods are interchangeable — a Deployment replacement arrives with a new name and nothing depended on it, a StatefulSet replacement arrives with the same name and reattaches to the same claim"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the db-2 identifier persisting across the death event, from original Pod to PVC 2 to replacement"
accessibility:
  alt_text_seed: "Two panels. In the Deployment panel three Pods with hashed names are shown; the third dies and is replaced by a Pod with a different name and different UID, and nothing depended on which one it was. In the StatefulSet panel three Pods named db-0, db-1 and db-2 each have their own PersistentVolumeClaim numbered to match; db-2 dies and its replacement, also named db-2, reattaches to the same claim, because the storage belongs to the identity rather than to the Pod"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: false
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Identity and claim-binding semantics redrawn from Kubernetes StatefulSet concept docs; no vendor artwork reproduced"
```

---

## Figure: ch06-fig04-workload-resource-decision-tree

**Anchor ID:** `ch06-fig04-workload-resource-decision-tree`
**Purpose:** Collapses three separate documented exam confusions into one rule by fixing the *order* in which the reader asks questions — shape of the work first, nature of the application last.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** binary decision flowchart — four decision nodes, five terminal resource nodes

**Content specification:**
A top-down binary decision tree. The **root** decision node reads **`Does the work END?`**. Its **yes** branch descends left; its **no** branch descends right. On the **left (yes)** branch sits a decision node reading **`Does it repeat on a schedule?`**, whose **yes** branch terminates at **`CronJob`** and whose **no** branch terminates at **`Job`**. On the **right (no)** branch sits a decision node reading **`Must it run on EVERY node?`**, whose **yes** branch terminates at **`DaemonSet`** and whose **no** branch descends to a further decision node reading **`Are the Pods INTERCHANGEABLE?`**, whose **yes** branch terminates at **`Deployment`** — that terminal box carries the sub-label **`(manages a ReplicaSet)`** — and whose **no** branch terminates at **`StatefulSet`**. Every branch edge is labelled **`yes`** or **`no`**; none may be left unlabelled. Decision nodes and terminal nodes must be visually distinct in shape or weight (e.g. decision nodes as plain rectangles with question text, terminals as heavier-ruled boxes holding a resource name). The words **`END`**, **`EVERY`**, and **`INTERCHANGEABLE`** appear in caps in the source and that emphasis carries the question order — preserve it. The point of the figure is the **question order itself**: the tree asks about the shape of the work before the nature of the application, and a tree that opened with "is it stateful?" would reproduce the trap it exists to defuse. The prose at line 770 tells the reader this figure is worth photographing and belongs on their one-page reference, so it must be legible standalone at reduced size and on a phone screen.

**Visual style:**
- Palette: inherit book default (Lodestar Ledgers navy/slate line-art register)
- Size (pixels): 1200x820 landscape
- Font: inherit book default (Fira Sans for question text and branch labels, Fira Mono for the five resource names)
- Accent color for highlighted elements: Brass `#B58B3E` on the **root node** `Does the work END?` and on the third decision node `Are the Pods INTERCHANGEABLE?` — the first and last questions are what the ordering argument rests on

**Critical details (non-negotiable accuracy):**
- **Question order is the pedagogy and must not be rearranged.** `Does the work END?` → `Must it run on EVERY node?` → `Are the Pods INTERCHANGEABLE?`. Promoting the interchangeability question up the tree destroys the figure's entire purpose.
- **`DaemonSet` has no replica count.** Its branch is reached by "must it run on every node," never by any question about how many copies. Do not annotate the DaemonSet terminal with a count.
- **CronJob is reached through Job's parent branch** — both sit under "the work ends." A CronJob creates Jobs on a schedule; do not draw them as unrelated peers on separate branches of the root.
- **`Deployment` carries `(manages a ReplicaSet)`** — ReplicaSet is not a separate terminal in this tree. Adding a sixth terminal box for ReplicaSet would contradict fig01's ownership chain and the §1 guidance that you author the Deployment, not the ReplicaSet.
- The StatefulSet terminal is reached by **`no` on interchangeability** — not by any question about disk, state, or databases.
- Five terminals exactly: CronJob, Job, DaemonSet, Deployment, StatefulSet. The prose says "four questions, six resources"; the sixth resource is the ReplicaSet named inside the Deployment terminal. Do not resolve that by adding a box.
- Both `yes`/`no` labels on every edge. An unlabelled branch makes the tree unreadable at reference size.

**Source ASCII (for designer reference):**
```
                    ┌─────────────────────────┐
                    │  Does the work END?     │
                    └───────┬─────────┬───────┘
                       yes  │         │  no
              ┌─────────────┘         └──────────────┐
              ▼                                      ▼
   ┌──────────────────────┐            ┌───────────────────────────┐
   │ Does it repeat on    │            │ Must it run on EVERY node?│
   │ a schedule?          │            └──────┬──────────────┬─────┘
   └────┬────────────┬────┘               yes │              │ no
    yes │            │ no                     ▼              ▼
        ▼            ▼               ┌─────────────┐  ┌──────────────────┐
  ┌──────────┐  ┌──────────┐         │  DaemonSet  │  │ Are the Pods     │
  │ CronJob  │  │   Job    │         └─────────────┘  │ INTERCHANGEABLE? │
  └──────────┘  └──────────┘                          └───┬──────────┬───┘
                                                      yes │          │ no
                                                          ▼          ▼
                                              ┌────────────────┐ ┌─────────────┐
                                              │   Deployment   │ │ StatefulSet │
                                              │ (manages a     │ └─────────────┘
                                              │  ReplicaSet)   │
                                              └────────────────┘
```

**Proposed filename:** `ch06-fig04-workload-resource-decision-tree.png`

```yaml-figure-spec
anchor_id: ch06-fig04-workload-resource-decision-tree
diagram_type: flowchart
source_ascii: |
                      ┌─────────────────────────┐
                      │  Does the work END?     │
                      └───────┬─────────┬───────┘
                         yes  │         │  no
                ┌─────────────┘         └──────────────┐
                ▼                                      ▼
     ┌──────────────────────┐            ┌───────────────────────────┐
     │ Does it repeat on    │            │ Must it run on EVERY node?│
     │ a schedule?          │            └──────┬──────────────┬─────┘
     └────┬────────────┬────┘               yes │              │ no
      yes │            │ no                     ▼              ▼
          ▼            ▼               ┌─────────────┐  ┌──────────────────┐
    ┌──────────┐  ┌──────────┐         │  DaemonSet  │  │ Are the Pods     │
    │ CronJob  │  │   Job    │         └─────────────┘  │ INTERCHANGEABLE? │
    └──────────┘  └──────────┘                          └───┬──────────┬───┘
                                                        yes │          │ no
                                                            ▼          ▼
                                                ┌────────────────┐ ┌─────────────┐
                                                │   Deployment   │ │ StatefulSet │
                                                │ (manages a     │ └─────────────┘
                                                │  ReplicaSet)   │
                                                └────────────────┘
vendor_terms: [cronjob, job, daemonset, deployment, statefulset, replicaset]
complexity_hint:
  node_count: 9
  edge_count: 8
  label_count: 17
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, vendor_taxonomy, spatial_structure]
  learning_outcome: "Select the correct workload resource by asking about the shape of the work before the nature of the application, resolving the Deployment/StatefulSet, DaemonSet-as-count, and Job/CronJob confusions with one rule"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the root question 'Does the work END?' together with the final question 'Are the Pods INTERCHANGEABLE?'"
accessibility:
  alt_text_seed: "A decision tree. First question: does the work end? If yes, ask whether it repeats on a schedule — yes gives CronJob, no gives Job. If no, ask whether it must run on every node — yes gives DaemonSet, no leads to a final question, are the Pods interchangeable, where yes gives Deployment, which manages a ReplicaSet, and no gives StatefulSet"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original Lodestar selection heuristic over documented Kubernetes workload resources; no vendor artwork reproduced"
```

---

## Figure: ch06-zenith-control-loop-instantiated

> ⚠ **Anchor ID does not conform to `ch{NN}-fig{MM}-{kebab-slug}`.** See MALFORMED ANCHORS above. Preserved unrenamed here per rule 6; suggested correction `ch06-fig06-control-loop-instantiated` pending author review.

**Anchor ID:** `ch06-zenith-control-loop-instantiated`
**Purpose:** Delivers the chapter's ☀️ Zenith — that the six workload resources the reader just learned are one control loop with six different definitions of "desired," not six mechanisms.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** radial concept map — one central vertical loop with six labelled inputs converging on a single node

**Content specification:**
A single vertical spine occupies the centre: three stacked nodes reading, top to bottom, **`DESIRED`** → **`compare`** → **`CURRENT`**, connected by downward arrows. Converging on the **`DESIRED`** node from above are three diagonal in-leads, each carrying a phrase and no box of its own: **`a number`** (entering vertically from directly above), **`a template + an update policy`** (entering from the upper right), and **`"whatever its author decided"`** (entering from the upper left). Diverging below the **`CURRENT`** node are three further diagonal leads carrying: **`a Job existing at each scheduled time`** (lower left), **`completion`** (directly below), and **`one per matching node`** (lower right). The six phrases are the six controllers' definitions of desired state and must read as *variations on one input*, not as six separate loops. **There is exactly one loop drawn.** That singularity is the argument — the prose at line 949 states it directly: "The loop is drawn once because there is only one." Under no circumstances render six loops, six diagrams, or a repeated motif. The six phrases should sit at roughly equal visual weight around the single spine, unboxed, so the centre reads as the invariant and the periphery as the variable. Optionally the six phrases may be tagged with their owning controller (ReplicaSet, Deployment, DaemonSet, Job, CronJob, operator) in a lighter weight, but if tagging crowds the figure, omit the tags — the body list immediately below the figure supplies the mapping.

**Visual style:**
- Palette: inherit book default (Lodestar Ledgers navy/slate line-art register); this is a ☀️ Zenith figure and may carry slightly more atmospheric weight than the chapter's mechanical diagrams
- Size (pixels): 1000x820 portrait
- Font: inherit book default (Fira Sans throughout; the six input phrases in italic to mark them as variable)
- Accent color for highlighted elements: Brass `#B58B3E` on the central three-node spine `DESIRED` → `compare` → `CURRENT` — the invariant, not the variations

**Critical details (non-negotiable accuracy):**
- **Exactly one loop.** Six loops would state the opposite of the section's thesis.
- The spine order is **`DESIRED` → `compare` → `CURRENT`**, matching Chapter 3's control loop as previously taught. Do not reorder or rename these three nodes.
- The six phrases are **definitions of desired state**, all feeding the same `DESIRED` node conceptually — the source ASCII splits them above and below for layout reasons only. A designer may rebalance them radially around the spine, but must not reassign any phrase to `CURRENT` or to `compare`.
- **`one per matching node`** belongs to the DaemonSet and is a count the *cluster computes*, not one the author writes. If the render tags it, it must not be tagged with a numeral.
- **`completion`** belongs to the Job; **`a Job existing at each scheduled time`** belongs to the CronJob. Keep them distinct — their relationship is that a CronJob's output is Jobs.
- **`a number`** is the ReplicaSet's; **`a template + an update policy`** is the Deployment's. This must stay consistent with fig01's layer split.
- The figure is forward-referenced: Chapter 15 tells the reader to come back and confirm "it will be the same figure." Do not stylise it so distinctively that a Chapter 15 callback would need a redraw.

**Source ASCII (for designer reference):**
```
                    a number
                        │
    "whatever its       │        a template
     author decided"    │        + an update policy
              ╲         │         ╱
               ╲        ▼        ╱
                ╲  ┌─────────┐  ╱
                 ╲ │ DESIRED │ ╱
                   └────┬────┘
                        │
                   ┌────▼────┐
                   │ compare │
                   └────┬────┘
                        │
                   ┌────▼────┐
                   │ CURRENT │
                   └─────────┘
                 ╱     │      ╲
                ╱      │       ╲
   a Job existing      │        one per matching node
   at each             │
   scheduled time    completion
```

**Proposed filename:** `ch06-zenith-control-loop-instantiated.png`
*(If the author accepts the suggested anchor correction, this becomes `ch06-fig06-control-loop-instantiated.png` — rename anchor, filename, and this document's join key together in one edit.)*

```yaml-figure-spec
anchor_id: ch06-zenith-control-loop-instantiated
diagram_type: concept_map
source_ascii: |
                      a number
                          │
      "whatever its       │        a template
       author decided"    │        + an update policy
                ╲         │         ╱
                 ╲        ▼        ╱
                  ╲  ┌─────────┐  ╱
                   ╲ │ DESIRED │ ╱
                     └────┬────┘
                          │
                     ┌────▼────┐
                     │ compare │
                     └────┬────┘
                          │
                     ┌────▼────┐
                     │ CURRENT │
                     └─────────┘
                   ╱     │      ╲
                  ╱      │       ╲
     a Job existing      │        one per matching node
     at each             │
     scheduled time    completion
vendor_terms: [replicaset, deployment, daemonset, job, cronjob, operator]
complexity_hint:
  node_count: 9
  edge_count: 8
  label_count: 9
pedagogy:
  part_18_criteria_met: [zenith, concept_map, spatial_structure]
  learning_outcome: "Recognize that all six workload controllers are one control loop differing only in what desired state means, so that later controllers — including GitOps in Chapter 15 — are recognized rather than learned"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the single central spine DESIRED to compare to CURRENT, drawn once because there is only one loop"
accessibility:
  alt_text_seed: "A single control loop drawn once: a DESIRED node feeds a compare node which feeds a CURRENT node. Six phrases converge on it as alternative definitions of desired state — a number, a template plus an update policy, whatever its author decided, a Job existing at each scheduled time, completion, and one per matching node — one for each of the six workload controllers"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: false
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original Lodestar synthesis figure over the documented Kubernetes controller pattern; no vendor artwork reproduced"
```

---

## HANDOFF NOTES

1. **Blocking on the source problem above.** Do not commission or render final art from this document until Stage 4 is re-run for ch-06 and the voiced draft is confirmed complete. The figures themselves are stable — they are Stage 3 artifacts and the voice pass does not touch them — but a re-run could in principle alter surrounding prose that these specs quote (the §4 mnemonic, the §7 "worth photographing" line). Re-diff this document against the repaired voiced draft before art goes out.

2. **`fig04` is a reference-card candidate.** Draft line 770 states the decision tree "belongs on your one-page reference." It should be produced at two sizes: the in-chapter render specified above, and a reduced variant legible on `the-lodestar.md`'s single page. Flag to the author whether that variant is in scope for the diagram pipeline or is a separate design task.

3. **`fig02` carries an unresolved precision question.** The ASCII labels the surge ceiling `10 + 25%` and draws it at 12, while the prose works the arithmetic to `maxSurge` = 3 (total may reach 13) because percentages round **up**. Both are defensible — the chart is schematic, the prose is exact — but a designer rendering numeric axis ticks will have to pick one. Author decision required before render; the critical-details bullet above holds the line at the conservative reading in the meantime.

4. **`fig01`, `fig05`, and the Zenith figure share identifiers with each other and with the §2 transcript** (`web-7d4b9c`, the Pod-name stem, the layer split). Render them as a set so the names stay consistent; a per-figure hand-off risks divergent examples across one chapter.

5. **Unresolved `AUTHOR-REVIEW` at draft line 778** concerns cross-bearing section numbers in shipped Chapters 1 and 2 pointing at this chapter. It does not affect any figure in this document and is noted only so it is not lost.
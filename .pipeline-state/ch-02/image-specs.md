# Image Specifications — KCNA Chapter 2

*Generated from the voiced draft at `../Book-KCNA/.pipeline-state/ch-02/draft-v1.md`. Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Stage input note.** The stage prompt referenced `draft-voice.md`, which does not exist in `ch-02/`. The voice stage writes in place: the voiced draft is `draft-v1.md` (mtime 01:41, matching the tail of `.draft-voice.md.progress.log`) and the pre-voice snapshot is preserved as `draft-v1-prevoice.md`. This document was extracted from `draft-v1.md`. Line numbers cited below are from that file.

**Extraction summary:** 6 figure anchors, 5 ASCII diagrams, 0 unanchored diagrams. Two anchors need author decisions before the diagram pipeline runs — see flags immediately below.

---

## AUTHOR-REVIEW FLAGS (resolve before handing this file to certcomp-diagrams)

**No unanchored diagrams.** All five fenced ASCII blocks in the draft (lines 138–156, 197–215, 394–414, 469–479, 582–597) are immediately preceded by a `<!-- FIGURE: -->` anchor. All box-drawing characters in the file fall inside those five blocks; there is no stray diagram art in prose.

### FLAG 1 — malformed anchor ID (rule 4 violation)

`ch02-zenith-standard-crate` (draft line 721) does not match the required `ch{NN}-fig{MM}-{kebab-slug}` pattern — it has no `fig{MM}` segment. Its prose caption numbers it **Figure 2-6**, so the conforming ID is `ch02-fig06-zenith-standard-crate`. Renaming is an author-review decision (rule 6), so the non-conforming ID is preserved verbatim below as the join key. The structural linter will flag this independently.

### FLAG 2 — anchor numbering does not match document order or caption numbering

| Document order | Anchor ID | Prose caption |
|---|---|---|
| 1 (line 137) | `ch02-fig01-vm-vs-container-stack` | Figure 2-1 |
| 2 (line 196) | `ch02-fig02-image-layers-and-digests` | Figure 2-2 |
| 3 (line 393) | `ch02-fig04-cri-runtime-chain` | **Figure 2-3** |
| 4 (line 468) | `ch02-fig03-oci-three-specs` | **Figure 2-4** |
| 5 (line 581) | `ch02-fig05-imagepullpolicy-decision` | Figure 2-5 |
| 6 (line 721) | `ch02-zenith-standard-crate` | Figure 2-6 |

`fig03` and `fig04` are transposed relative to both document order and caption numbering: the CRI chain is `fig04` but captioned Figure 2-3, and the OCI specs figure is `fig03` but captioned Figure 2-4. The captions are internally consistent with each other and are cross-referenced by number in prose (line 493: *"Lay Figure 2-3 and Figure 2-4 side by side"*; line 428: *"the pluggable position in the middle of Figure 2-3"*). So the **captions are correct and the anchor IDs are the drift.** Author to decide: renumber the two anchors to match (recommended — one edit to the draft's two anchor comments, no prose change), or accept the mismatch permanently. Entries below are ordered by document order, not by anchor number.

### FLAG 3 — BLOCKING scope decision on `ch02-fig02`

The draft carries an unresolved AUTHOR-REVIEW comment at line 219 that names this stage explicitly:

> *"…accept the narrowed scope, in which case ch02-fig02 should be reduced to its digest half and renamed in image-specs.md BEFORE Stage 10. Recommendation (a) — layers are load-bearing for both the digest concept and the Chapter 12 supply-chain material."*

That decision has not been recorded, so the figure is specified below **as drawn** (both panels). The dependency: resolution (a) requires Stage 2 to fetch a layer/build-practices source; only resolution (b) shrinks the figure. If the author picks (b), the left panel is cut, the anchor is renamed to something like `ch02-fig02-tag-vs-digest`, and this entry must be regenerated. Do not commission this figure until that is settled.

### FLAG 4 — `ch02-zenith-standard-crate` is illustration, not a renderable diagram

It has no ASCII block. Its caption marks it *"to be commissioned"* and it routes to the human illustrator, not to D2/Mermaid/PlantUML. Its `yaml-figure-spec` block is emitted for index completeness with `diagram_type: other`. The draft's caption also demands a register check against `illustrator-brief.md` before commissioning; KCNA's era placement is not stated in the draft and is not invented here.

---

## Figure: ch02-fig01-vm-vs-container-stack

**Anchor ID:** `ch02-fig01-vm-vs-container-stack`
**Draft location:** line 137 (anchor), 138–156 (ASCII), 158 (caption "Figure 2-1")
**Purpose:** Make the single architectural difference between VMs and containers visible as a row that repeats on one side and is absent on the other, so the reader can derive start-up time, image size, and density rather than memorizing them.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Side-by-side comparative layer-stack diagram (two panels, shared baseline)

**Content specification:**
Two panels of equal width, side by side, each a stack of layers built upward from a common bottom. Panel titles across the top: **VIRTUAL MACHINES** (left), **CONTAINERS** (right). Left panel, bottom to top: a full-width box `hardware`; above it a full-width box `host OS`; above it a full-width box `hypervisor`; above that the stack splits into three equal columns, each column being a two-box tower of `Guest OS` (lower) and `App` (upper). Three lines rise from the hypervisor's top edge, one into each Guest OS box. Left panel footer text: **THREE OS COPIES · three apps**. Right panel, bottom to top: a full-width box `hardware`; above it a full-width box `host OS`; above it a full-width box `container runtime`; above that three free-standing `App` boxes in a row, each connected downward to the container runtime by a single line. There is deliberately **no** box between `App` and `container runtime` on the right. Right panel footer text: **ONE OS · three apps**. The point of the figure is the *guest-OS row* — it appears three times on the left and zero times on the right; that row and its absence carry the accent. Both panels use identical box geometry, line weight, and vertical rhythm so the reader's eye reads the difference as a missing row rather than as two unrelated drawings.

**Visual style:**
- Palette: inherit book default (Lodestar)
- Size (pixels): 1200x620 landscape
- Font: inherit book default (Fira Sans for labels, Fira Mono for any literal identifiers)
- Accent color for highlighted elements: Brass `#B58B3E` on the three `Guest OS` boxes on the left; the corresponding empty region on the right gets a light Brass-tinted dashed outline or a thin Brass leader line labelled *no guest OS* — the absence must be as legible as the presence.

**Critical details (non-negotiable accuracy):**
- VMs are on the **left**, containers on the **right** — not reversed. Prose and caption both refer to "the duplication on the left."
- On the container side there is **exactly one** OS box, and it is labelled `host OS`. Do not add a per-container OS, minimal OS, or "guest" layer of any kind; the surrounding prose (line 176) hinges on an image containing no kernel.
- `hypervisor` sits **above** `host OS` on the VM side, not below it and not replacing it.
- `container runtime` sits directly above `host OS` on the container side and directly below the apps — nothing between.
- Three apps on **each** side. The comparison is only fair at equal workload count, and both footer lines say "three apps."
- Both panels must share the same baseline: `hardware` is the bottom row in each, drawn at the same height.
- Label the OS layer `host OS`, not "Linux", "kernel", or any distribution name. The kernel-sharing precision note is prose (line 133), not this figure's job.
- No vendor logos, no product names anywhere in this figure. It is deliberately generic.

**Source ASCII (for designer reference):**
```
        VIRTUAL MACHINES                       CONTAINERS

   ┌──────┐ ┌──────┐ ┌──────┐          ┌──────┐ ┌──────┐ ┌──────┐
   │ App  │ │ App  │ │ App  │          │ App  │ │ App  │ │ App  │
   ├──────┤ ├──────┤ ├──────┤          └──┬───┘ └──┬───┘ └──┬───┘
   │Guest │ │Guest │ │Guest │             │        │        │
   │  OS  │ │  OS  │ │  OS  │          ┌──┴────────┴────────┴──┐
   └──┬───┘ └──┬───┘ └──┬───┘          │   container runtime    │
      │        │        │              ├────────────────────────┤
   ┌──┴────────┴────────┴──┐           │        host OS         │
   │      hypervisor        │          ├────────────────────────┤
   ├────────────────────────┤          │       hardware         │
   │        host OS         │          └────────────────────────┘
   ├────────────────────────┤
   │       hardware         │           ONE OS · three apps
   └────────────────────────┘
    THREE OS COPIES · three apps
```

**Proposed filename:** `ch02-fig01-vm-vs-container-stack.png`

```yaml-figure-spec
anchor_id: ch02-fig01-vm-vs-container-stack
diagram_type: deployment_diagram
source_ascii: |2
          VIRTUAL MACHINES                       CONTAINERS

     ┌──────┐ ┌──────┐ ┌──────┐          ┌──────┐ ┌──────┐ ┌──────┐
     │ App  │ │ App  │ │ App  │          │ App  │ │ App  │ │ App  │
     ├──────┤ ├──────┤ ├──────┤          └──┬───┘ └──┬───┘ └──┬───┘
     │Guest │ │Guest │ │Guest │             │        │        │
     │  OS  │ │  OS  │ │  OS  │          ┌──┴────────┴────────┴──┐
     └──┬───┘ └──┬───┘ └──┬───┘          │   container runtime    │
        │        │        │              ├────────────────────────┤
     ┌──┴────────┴────────┴──┐           │        host OS         │
     │      hypervisor        │          ├────────────────────────┤
     ├────────────────────────┤          │       hardware         │
     │        host OS         │          └────────────────────────┘
     ├────────────────────────┤
     │       hardware         │           ONE OS · three apps
     └────────────────────────┘
      THREE OS COPIES · three apps
vendor_terms: []
complexity_hint:
  node_count: 15
  edge_count: 6
  label_count: 19
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Derive every VM-versus-container difference from the single fact that containers share the host kernel instead of booting a guest OS"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the repeated Guest OS row on the VM side, and its absence on the container side"
accessibility:
  alt_text_seed: "Two stacks side by side. On the left, virtual machines: hardware, host OS, then a hypervisor, then three columns each containing a guest OS with an app above it — three operating system copies for three apps. On the right, containers: hardware, host OS, then a single container runtime with three apps sitting directly on it — one operating system for three apps. The guest OS row present three times on the left is absent entirely on the right."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "No vendor marks or logos in the figure; all labels generic. Well-known prior art exists in the kubernetes.io deployment-evolution graphic (CC-BY-4.0), so composition is deliberately different — two-panel VM/container comparison rather than a three-era progression."
```

---

## Figure: ch02-fig02-image-layers-and-digests

**Anchor ID:** `ch02-fig02-image-layers-and-digests`
**Draft location:** line 196 (anchor), 197–215 (ASCII), 217 (caption "Figure 2-2")
**Purpose:** Hold two ideas in one frame — that layers are shared between images built from a common base, and that a tag is an attachment that can be re-attached while a digest cannot — so §3's tag-versus-digest Fixed Point lands with a picture already in place.
**Replaces ASCII:** yes
**Mandatory:** yes — **but see FLAG 3 above.** The left panel's scope is an unresolved author decision; do not commission until it is settled.
**Type:** Two-panel composite — layer stack (left) plus pointer/identity semantics over time (right)

**Content specification:**
Two panels of roughly equal width under the titles **LAYERS** (left) and **IDENTITY** (right), separated by a rule or generous gutter so they read as two ideas rather than one continuous drawing. Left panel: two small stacks side by side, captioned `image A` and `image B`. Each stack is two boxes: `shared base` at the bottom and `app` on top. The two `shared base` boxes are joined by a horizontal double-line connector indicating they are the *same* layer, not two copies. Annotation beneath the left panel, three short lines: `both manifests name` / `the SAME base layer` / `→ stored once`. Right panel: a prominent card at the top holding three lines — `sha256:9f2c…be41`, `digest = content hash`, `immutable`. Below the card, two identical small boxes each labelled `:v2`, captioned `today` (left) and `next week` (right). An arrow rises from each `:v2` box to the digest card: the `today` arrow is **solid**, the `next week` arrow is **dashed**, and the two arrows terminate at different points on the card to show they resolve to different content. Small labels `solid` and `dashed` sit beside the respective arrows. Footer text under the right panel, two lines: `a tag is a LABEL — it can be` / `moved to point at a different image`. The point of the figure is the **dashed arrow**: same tag string, different target, one week apart.

**Visual style:**
- Palette: inherit book default (Lodestar)
- Size (pixels): 1200x560 landscape
- Font: inherit book default; `sha256:9f2c…be41` and `:v2` must be set in Fira Mono — they are literal references and must look like literals
- Accent color for highlighted elements: Brass `#B58B3E` on the dashed `next week → digest` arrow. The solid arrow stays in the neutral body color so the contrast between them is the visual event.

**Critical details (non-negotiable accuracy):**
- The base layer is drawn as **one shared thing**, not two identically-labelled copies. The claim being illustrated (line 194) is that the layer is stored and transferred once.
- `shared base` is at the **bottom** of each stack, `app` on top. A base layer under-lies; reversing it inverts the concept.
- Both tag boxes read exactly `:v2` — identical strings. If the two tags differ, the entire figure collapses.
- The digest is **immutable** and the tag is **movable** — never the reverse. This is the chapter's most-recited Fixed Point (draft line 271).
- The digest string must be shown truncated with an ellipsis (`sha256:9f2c…be41`), never as a plausible-looking full 64-hex-character digest. A fabricated complete hash would read as a real image identifier.
- The arrows point **from tag to image/digest**, not from digest to tag. A tag references content; content does not reference its labels.
- Solid versus dashed must be distinguishable without color — the dashed arrow carries meaning on e-ink.
- Do not depict layer counts, ordering rules, cache-invalidation behavior, or build stages. The draft (line 219) deliberately stops at "a stack with a shared base named by the manifest"; anything more would be unsourced.

**Source ASCII (for designer reference):**
```
        LAYERS                                 IDENTITY

   image A      image B                ┌──────────────────────────┐
  ┌─────────┐  ┌─────────┐             │   sha256:9f2c…be41       │
  │   app   │  │   app   │             │   digest = content hash  │
  ├─────────┤  ├─────────┤             │   immutable              │
  │ shared  │══│ shared  │             └──────────────────────────┘
  │  base   │  │  base   │                  ▲                ▲
  └─────────┘  └─────────┘            ───────┘         ┄┄┄┄┄┄┄┘
                                      solid            dashed
   both manifests name               ┌──────┐         ┌──────┐
   the SAME base layer               │ :v2  │         │ :v2  │
   → stored once                     └──────┘         └──────┘
                                      today          next week

                                  a tag is a LABEL — it can be
                                  moved to point at a different image
```

**Proposed filename:** `ch02-fig02-image-layers-and-digests.png`

```yaml-figure-spec
anchor_id: ch02-fig02-image-layers-and-digests
diagram_type: concept_map
source_ascii: |2
          LAYERS                                 IDENTITY

     image A      image B                ┌──────────────────────────┐
    ┌─────────┐  ┌─────────┐             │   sha256:9f2c…be41       │
    │   app   │  │   app   │             │   digest = content hash  │
    ├─────────┤  ├─────────┤             │   immutable              │
    │ shared  │══│ shared  │             └──────────────────────────┘
    │  base   │  │  base   │                  ▲                ▲
    └─────────┘  └─────────┘            ───────┘         ┄┄┄┄┄┄┄┘
                                        solid            dashed
     both manifests name               ┌──────┐         ┌──────┐
     the SAME base layer               │ :v2  │         │ :v2  │
     → stored once                     └──────┘         └──────┘
                                        today          next week

                                    a tag is a LABEL — it can be
                                    moved to point at a different image
vendor_terms: []
complexity_hint:
  node_count: 7
  edge_count: 3
  label_count: 15
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Distinguish a movable tag from an immutable content digest, and explain why images built from a common base share that layer"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the dashed arrow from next week's :v2 tag, resolving to different content than today's"
accessibility:
  alt_text_seed: "Left: two image stacks, image A and image B, each with an app layer above a shared base layer, the two base layers joined to show they are one stored layer named by both manifests. Right: a card showing a truncated digest sha256:9f2c...be41 labelled content hash and immutable, with two identical :v2 tag boxes below it — one labelled today connected by a solid arrow, one labelled next week connected by a dashed arrow to a different point, showing that a tag is a label that can be moved to point at a different image."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic layer and tag semantics; no vendor marks, no registry product names, digest string is truncated placeholder rather than a real image identifier."
```

---

## Figure: ch02-fig04-cri-runtime-chain

**Anchor ID:** `ch02-fig04-cri-runtime-chain`
**Draft location:** line 393 (anchor), 394–414 (ASCII), 416 (caption **"Figure 2-3"** — see FLAG 2)
**Purpose:** Render the CRI as a boundary line with a socket rather than as a box, so the chapter's most-reused Fixed Point — Kubernetes defines the interface and implements nothing below it — is a spatial fact the reader can see.
**Replaces ASCII:** yes
**Mandatory:** yes — the ★ Fixed Point at draft line 418 and the Exam Alert both depend on this chain, and prose at line 428 and line 493 refers to this figure by number.
**Type:** Vertical layered architecture diagram with an emphasized interface boundary and a socket receptacle

**Content specification:**
A single vertical column, top to bottom, four stations. Top: a box labelled `kubelet`, with the side annotation `the node agent Kubernetes ships`. A short connector descends from it to a **horizontal boundary line spanning the full figure width**, drawn heavier and in a visually distinct treatment (double rule) from every other line in the figure. The boundary is labelled `C R I` at its center, with `interface boundary` at its right end and a two-line annotation to the right of the descending connector: `Kubernetes DEFINES this line` / `and implements nothing below it`. Below the boundary, an arrow descends into a **socket**: an outer box containing an inner receptacle drawn with a distinctly different border treatment (heavy/blocked in the ASCII) to read as a slot rather than a component. Inside the receptacle, three stacked lines: `containerd`, `— or —`, `CRI-O`. To the right of the socket, a three-line annotation: `socket:` / `exactly one conformant` / `CRI runtime plugs in here`. From the bottom of the socket box, an arrow descends to a box labelled `runC`, and from `runC` a horizontal arrow points right to a box labelled `running process`. The point of the figure is the **socket** — containerd and CRI-O must read as two things that fit one opening, never as two parallel branches of a fork. Do not draw a diamond, a split, or two edges leaving the kubelet.

**Visual style:**
- Palette: inherit book default (Lodestar)
- Size (pixels): 800x900 portrait
- Font: inherit book default; `kubelet`, `containerd`, `CRI-O`, and `runC` in Fira Mono — they are component names
- Accent color for highlighted elements: Brass `#B58B3E` on the CRI boundary line and its `C R I` label. The socket's inner receptacle gets a secondary treatment (Brass at reduced weight, or a Brass-keyed hatch) so the boundary reads as primary and the socket as its consequence.

**Critical details (non-negotiable accuracy):**
- Order top to bottom is exactly: `kubelet` → CRI boundary → CRI runtime (containerd **or** CRI-O) → `runC` → running process. No station may be transposed.
- containerd and CRI-O occupy **one** position joined by "or" — they are alternatives filling a single slot, not two coexisting paths. Two arrows out of the kubelet would contradict the caption at line 416 and the `⚓ Worth Securing` callout.
- `runC` sits **below** the CRI runtime, not beside it and not above it. It is the OCI runtime the CRI runtime invokes.
- The kubelet is **above** the boundary (Kubernetes side); everything below the boundary is ecosystem-supplied. The Fixed Point is that Kubernetes implements nothing below that line.
- The CRI is a **line**, not a box. Drawing it as a component destroys the figure's argument.
- Spell the names as the draft does: `kubelet` lowercase, `containerd` lowercase, `CRI-O` with a hyphen and capitals, `runC` with a capital C.
- The figure must be readable side by side with `ch02-fig03-oci-three-specs` in the same visual grammar — prose at line 493 instructs the reader to lay the two together and see that they are different planes. Same box style, same line weight, same label treatment across both.
- Nothing in this figure is an OCI specification. Keep spec names out of it entirely; `runC` appears as a component, not as `runtime-spec`.

**Source ASCII (for designer reference):**
```
  ┌───────────┐
  │  kubelet  │   the node agent Kubernetes ships
  └─────┬─────┘
        │
  ══════╪══════════  C R I  ═══════════════════  interface boundary
        │            Kubernetes DEFINES this line
        │            and implements nothing below it
        ▼
  ┌──────────────────────────┐
  │ ▛▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▜ │    socket:
  │ ▌      containerd     ▐ │    exactly one conformant
  │ ▌       — or —        ▐ │    CRI runtime plugs in here
  │ ▌        CRI-O        ▐ │
  │ ▙▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▟ │
  └────────────┬─────────────┘
               ▼
        ┌────────────┐       ┌──────────────────┐
        │    runC    │  ──►  │ running process  │
        └────────────┘       └──────────────────┘
```

**Proposed filename:** `ch02-fig04-cri-runtime-chain.png`

```yaml-figure-spec
anchor_id: ch02-fig04-cri-runtime-chain
diagram_type: k8s_architecture
source_ascii: |2
    ┌───────────┐
    │  kubelet  │   the node agent Kubernetes ships
    └─────┬─────┘
          │
    ══════╪══════════  C R I  ═══════════════════  interface boundary
          │            Kubernetes DEFINES this line
          │            and implements nothing below it
          ▼
    ┌──────────────────────────┐
    │ ▛▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▜ │    socket:
    │ ▌      containerd     ▐ │    exactly one conformant
    │ ▌       — or —        ▐ │    CRI runtime plugs in here
    │ ▌        CRI-O        ▐ │
    │ ▙▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▟ │
    └────────────┬─────────────┘
                 ▼
          ┌────────────┐       ┌──────────────────┐
          │    runC    │  ──►  │ running process  │
          └────────────┘       └──────────────────┘
vendor_terms: [kubelet, containerd, cri-o, runc]
complexity_hint:
  node_count: 5
  edge_count: 4
  label_count: 9
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "Recall the kubelet to CRI to containerd-or-CRI-O to runC chain, and state that Kubernetes defines the CRI without implementing anything below it"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the CRI boundary line — the socket Kubernetes defines and does not implement"
accessibility:
  alt_text_seed: "A vertical chain. At the top, the kubelet, the node agent Kubernetes ships. A connector descends across a heavy horizontal boundary labelled CRI, annotated: Kubernetes defines this line and implements nothing below it. Below the boundary, a socket into which exactly one conformant CRI runtime plugs — containerd or CRI-O. Below the socket, runC, which starts a running process."
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 800
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes, containerd and CRI-O are CNCF marks and runC is a Linux Foundation/OCI project; they appear as text labels only, redrawn in Lodestar style. If the renderer substitutes official project logos for any of these boxes, re-evaluate clearance as licensed_icon_set before release."
```

---

## Figure: ch02-fig03-oci-three-specs

**Anchor ID:** `ch02-fig03-oci-three-specs`
**Draft location:** line 468 (anchor), 469–479 (ASCII), 481 (caption **"Figure 2-4"** — see FLAG 2)
**Purpose:** Map each of the OCI's three specifications onto the one stage of the artifact lifecycle it governs, and show — by the total absence of Kubernetes from the frame — that OCI and CRI are different planes.
**Replaces ASCII:** yes
**Mandatory:** yes — the `⚠ Navigational Hazards` callout at line 485 instructs the reader to lay this figure beside Figure 2-3, and the 🪢 Mnemonic depends on the column order.
**Type:** Two-register diagram — governance band above, left-to-right artifact lifecycle below, with vertical governs-relations between them

**Content specification:**
Upper register: three boxes in a row, equal width, each a specification. Left box header `image-spec`, body `the FORMAT of the artifact`. Center box header `distribution-spec`, body `the API for MOVING it over the wire`. Right box header `runtime-spec`, body `how to RUN a filesystem bundle`. Lower register: a left-to-right flow of three boxes plus a terminal. First box `OCI Image`; an arrow labelled `pull` points right to a box `unpack`; an unlabelled arrow points right to a box `filesystem bundle`; a final arrow points right to the terminal word `run`. Between the registers, three vertical arrows descend, one from each specification box to the lifecycle stage it governs: `image-spec` → `OCI Image`, `distribution-spec` → the pull/`unpack` transition, `runtime-spec` → `filesystem bundle`/`run`. The columns must align so each spec sits directly above what it governs — the column alignment *is* the content. The point of the figure is that the three specs are documents governing an artifact's life, and that Kubernetes appears nowhere.

**Visual style:**
- Palette: inherit book default (Lodestar)
- Size (pixels): 1200x520 landscape
- Font: inherit book default; `image-spec`, `distribution-spec`, `runtime-spec` in Fira Mono — the draft sets them as literals
- Accent color for highlighted elements: Brass `#B58B3E` on the `distribution-spec` column (box plus its descending arrow). Rationale: the 🔭 Closer Look at line 495 tells the reader the exam is likeliest to ask which specification governs the registry API, and that it is the one that arrived last.

**Critical details (non-negotiable accuracy):**
- Column order left to right is `image-spec`, `distribution-spec`, `runtime-spec` — build it, ship it, run it. The 🪢 Mnemonic at line 483 is this order; any transposition breaks it.
- The mapping is strict: image-spec governs the format, distribution-spec governs movement over the wire, runtime-spec governs execution of the unpacked bundle. Never cross these wires.
- Lifecycle order is: OCI Image → **pull** → unpack → filesystem bundle → run. The bundle is what gets run, and the bundle exists only *after* unpacking. Unpacking before running is the sourced sequence (draft line 466).
- **Kubernetes, the kubelet, CRI, containerd, CRI-O, and Pods must not appear anywhere in this figure.** The caption's "what to notice" is that nothing here is Kubernetes; a single Kubernetes label destroys the figure's entire function.
- Specifications go on **top**, artifacts underneath — governance above, governed below.
- Use the same box style, line weight, and label treatment as `ch02-fig04-cri-runtime-chain`. Prose instructs the reader to compare the two; the shared grammar is what makes "different planes" legible rather than "different drawings."
- Do not add spec version numbers to the boxes. The v1.0-May-2020 date for distribution-spec lives in prose, and putting a version on one box but not the others would imply the others are unversioned.
- Do not draw the OCI itself as a component or a container around the three specs. It is a governance body, not software (Fixed Point, line 454).

**Source ASCII (for designer reference):**
```
  ┌── image-spec ────┐  ┌── distribution-spec ─┐  ┌── runtime-spec ───┐
  │ the FORMAT of    │  │ the API for MOVING   │  │ how to RUN a      │
  │ the artifact     │  │ it over the wire     │  │ filesystem bundle │
  └────────┬─────────┘  └──────────┬───────────┘  └─────────┬─────────┘
           │                       │                        │
           ▼                       ▼                        ▼
   ┌──────────────┐         ┌────────────┐        ┌──────────────────┐
   │  OCI Image   │ ──pull─►│   unpack   │ ──────►│ filesystem bundle│──► run
   └──────────────┘         └────────────┘        └──────────────────┘
```

**Proposed filename:** `ch02-fig03-oci-three-specs.png`

```yaml-figure-spec
anchor_id: ch02-fig03-oci-three-specs
diagram_type: data_flow
source_ascii: |2
    ┌── image-spec ────┐  ┌── distribution-spec ─┐  ┌── runtime-spec ───┐
    │ the FORMAT of    │  │ the API for MOVING   │  │ how to RUN a      │
    │ the artifact     │  │ it over the wire     │  │ filesystem bundle │
    └────────┬─────────┘  └──────────┬───────────┘  └─────────┬─────────┘
             │                       │                        │
             ▼                       ▼                        ▼
     ┌──────────────┐         ┌────────────┐        ┌──────────────────┐
     │  OCI Image   │ ──pull─►│   unpack   │ ──────►│ filesystem bundle│──► run
     └──────────────┘         └────────────┘        └──────────────────┘
vendor_terms: [oci-image-spec, oci-distribution-spec, oci-runtime-spec]
complexity_hint:
  node_count: 7
  edge_count: 6
  label_count: 11
pedagogy:
  part_18_criteria_met: [spatial_structure, temporal_structure, fixed_point]
  learning_outcome: "Name the OCI's three specifications and identify which stage of an image's life each one governs"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the distribution-spec column, the specification governing the registry API"
accessibility:
  alt_text_seed: "Three specification boxes across the top: image-spec, the format of the artifact; distribution-spec, the API for moving it over the wire; runtime-spec, how to run a filesystem bundle. Each has an arrow descending to the stage it governs in the flow beneath: an OCI Image is pulled, then unpacked, becoming a filesystem bundle, which is then run. Kubernetes appears nowhere in the figure."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: [oci]
  clearance: own_interpretation
  notes: "Specification names are those published by the Open Container Initiative (Linux Foundation) and appear as text labels only; no OCI logo, no spec text reproduced, diagram composed for this book."
```

---

## Figure: ch02-fig05-imagepullpolicy-decision

**Anchor ID:** `ch02-fig05-imagepullpolicy-decision`
**Draft location:** line 581 (anchor), 582–597 (ASCII), 599 (caption "Figure 2-5")
**Purpose:** Show that the four `imagePullPolicy` defaults are reached by *not* setting the field, so the reader sees that a reference form chosen for identity reasons silently chose a pull behavior too.
**Replaces ASCII:** yes
**Mandatory:** yes — Exam Alert item 4 is these four defaults, and this is the highest-value-per-minute material in the chapter.
**Type:** Two-branch decision tree with an enumerated-outcome fan on one branch

**Content specification:**
A single root question at the top, centered: `was imagePullPolicy set explicitly?` Two branches descend, labelled `YES` (left) and `NO` (right). The **YES** branch terminates in one panel listing the three explicit policies and their behavior, each on its own row: `Always` → `resolve to digest; reuse cache if match`; `IfNotPresent` → `pull only if absent`; `Never` → `never fetch; fail if absent`. The **NO** branch descends to a second question, `reference form?`, which fans into four columns. Left to right the four reference forms are `@digest`, `:latest`, `no tag`, `:other`, and each has an arrow descending to its resulting default, in order: `IfNotPresent`, `Always`, `Always`, `IfNotPresent`. The four outcomes should read as leaves of the tree, not as a table. The point of the figure is the asymmetry between the branches: the left branch is a decision the reader made; the right branch is four decisions made *for* them by a naming choice. Give the right-hand side visual weight at least equal to the left, and consider a light band or label across the four leaves reading to the effect of *reached by not deciding* — the caption's whole argument is that the default path is the one nobody chose.

**Visual style:**
- Palette: inherit book default (Lodestar)
- Size (pixels): 1200x700 landscape
- Font: inherit book default; `imagePullPolicy`, `Always`, `IfNotPresent`, `Never`, `@digest`, `:latest`, `:other` all in Fira Mono — every one of these is a literal API value the reader will type
- Accent color for highlighted elements: Brass `#B58B3E` on the `:latest` → `Always` path (the reference-form node, its arrow, and its outcome). That single path is the trap §3 opened and §6 closes.

**Critical details (non-negotiable accuracy):**
- The four defaults must be exactly: digest → `IfNotPresent`; `:latest` → `Always`; no tag → `Always`; any other tag → `IfNotPresent`. Two of the four are `Always` and two are `IfNotPresent`; a designer "tidying" this into an alternating or all-different pattern would falsify the exam answer.
- `Always` must be described as *resolve to digest, reuse the local cache on a match* — **not** as "always download." The draft (line 603) calls the download reading a favorite distractor. If space forces a shortening, shorten to "always re-resolve" and never to "always pull."
- `Never` means the kubelet does not fetch at all, and startup **fails** if the image is absent locally. Do not soften to "may fail."
- `IfNotPresent` pulls **only if absent** — not "prefers local," not "checks first."
- The three explicit policies live on the YES branch; the four reference forms live on the NO branch. Never mix a policy name into the reference-form row.
- `@digest` must display with the `@` sigil and `:latest` / `:other` with the leading colon — the sigils are how the reader recognizes the form in a manifest.
- Exactly three policies and exactly four default cases. Do not add a fifth policy or a fifth reference form.
- Do not put `ImagePullBackOff`, the 300-second back-off limit, or Pod lifecycle states in this figure. They are prose in the same section and would overload the tree.

**Source ASCII (for designer reference):**
```
                    was imagePullPolicy set explicitly?
                          │                    │
                         YES                   NO
                          │                    │
        ┌─────────────────┴───────┐            │
        │ Always                  │      reference form?
        │  → resolve to digest;   │            │
        │    reuse cache if match │   ┌────────┼────────┬──────────┐
        │ IfNotPresent            │   │        │        │          │
        │  → pull only if absent  │ @digest :latest   no tag    :other
        │ Never                   │   │        │        │          │
        │  → never fetch; fail if │   ▼        ▼        ▼          ▼
        │    absent               │ IfNot-  Always   Always    IfNot-
        └─────────────────────────┘ Present                    Present
```

**Proposed filename:** `ch02-fig05-imagepullpolicy-decision.png`

```yaml-figure-spec
anchor_id: ch02-fig05-imagepullpolicy-decision
diagram_type: flowchart
source_ascii: |2
                      was imagePullPolicy set explicitly?
                            │                    │
                           YES                   NO
                            │                    │
          ┌─────────────────┴───────┐            │
          │ Always                  │      reference form?
          │  → resolve to digest;   │            │
          │    reuse cache if match │   ┌────────┼────────┬──────────┐
          │ IfNotPresent            │   │        │        │          │
          │  → pull only if absent  │ @digest :latest   no tag    :other
          │ Never                   │   │        │        │          │
          │  → never fetch; fail if │   ▼        ▼        ▼          ▼
          │    absent               │ IfNot-  Always   Always    IfNot-
          └─────────────────────────┘ Present                    Present
vendor_terms: [imagePullPolicy, kubelet]
complexity_hint:
  node_count: 11
  edge_count: 10
  label_count: 16
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure]
  learning_outcome: "State the three imagePullPolicy values and predict the default policy from an image reference's form"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the :latest to Always path — the default nobody chooses on purpose"
accessibility:
  alt_text_seed: "A decision tree. Root question: was imagePullPolicy set explicitly? On the YES branch, three policies: Always, which resolves the name to a digest and reuses the local cache on a match; IfNotPresent, which pulls only if the image is absent; and Never, which never fetches and fails if the image is absent. On the NO branch, a second question asks the reference form, fanning to four outcomes: a digest defaults to IfNotPresent, the :latest tag defaults to Always, no tag defaults to Always, and any other tag defaults to IfNotPresent."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Reproduces Kubernetes API field names and documented default behavior as text labels; no logos or documentation artwork, tree composed for this book."
```

---

## Figure: ch02-zenith-standard-crate

> **⚠ Anchor ID does not conform to `ch{NN}-fig{MM}-{kebab-slug}` (FLAG 1).** Preserved verbatim as the join key; the conforming form is `ch02-fig06-zenith-standard-crate`. Author to rename in the draft and here together.

**Anchor ID:** `ch02-zenith-standard-crate`
**Draft location:** line 721 (anchor), 722 (caption "Figure 2-6 (Zenith illustration — to be commissioned)")
**Purpose:** Carry the chapter's ☀️ Zenith synthesis — that the win came from standardizing the interface, not from improving the box — as an image, so the recognition lands before the Extended Analogy explains it.
**Replaces ASCII:** no — there is no ASCII block for this anchor. It is a commissioned illustration.
**Mandatory:** yes — the draft references it as Figure 2-6 and the ☀️ Zenith beat at line 713 is built around it.
**Type:** Commissioned narrative illustration (not a generated diagram — routes to the human illustrator, not to D2/Mermaid/PlantUML)

**Content specification:**
Identical standardized crates moving between visibly incompatible carriers — the carriers differ in kind, the crates do not. Each carrier is evidently purpose-built once, against a published specification, and handles any crate presented to it. No carrier opens a crate; no crate's contents are shown, implied, or hinted at. The contents never mattering *is* the subject. Composition is from the Communications Officer's vantage; the narrator is not depicted (brand architectural rule — narrator face never illustrated). Minimal labels by design: two or three at most, and the labels should name the *fitting* or the *specification*, not the cargo. The register test the draft sets: a reader who sees only an attractive freight scene has received a decorative illustration, which the brand's Part 18 framework bans. The image must read as being **about interfaces**. The mechanism of the transfer — the standardized fitting, the lifting point, the geometry that lets a carrier built once handle a crate that did not exist when it was built — is what should draw the eye, more than the vehicles or the setting.

**Visual style:**
- Palette: inherit book default (Lodestar); illustration palette per `illustration-standards.md`
- Size (pixels): full-width plate, 1200px wide, aspect ratio at the illustrator's discretion
- Font: any in-image labels inherit book default (Roboto Slab display / Fira Sans)
- Accent color for highlighted elements: at the illustrator's discretion within the locked palette; the standardized fitting is the natural place for a Brass `#B58B3E` note if one is used

**Critical details (non-negotiable accuracy):**
- **Narrator not depicted** — no face, no figure identifiable as the narrator. World seen from their vantage.
- **Era placement must be confirmed against `illustrator-brief.md` before commissioning.** The draft explicitly warns against defaulting to a 20th-century dockside. KCNA's era placement is not stated in the draft and is not assumed here; CLAUDE.md places the sibling CKA book in the early-interstellar register and KCNA in the same Communications Officer family, but the book's own placement must be read from the brief rather than inferred. **This is a blocking input.**
- Crates must be **identical** to each other. Variation in the crates inverts the entire point.
- Carriers must be **visibly different in kind** from one another. If the carriers look alike, there is no incompatibility for the standard to have bridged.
- No crate is open, transparent, or labelled with its contents.
- Two or three labels maximum. This is a synthesis plate, not a diagram.
- No decorative-only rendering: per the Part 18 framework and the locked illustration decisions, the figure must attach to the concept in the surrounding text — the interface, not the freight.
- Not a diagram-pipeline target. Do not route to D2, Mermaid, or PlantUML.

**Source ASCII (for designer reference):**
*None — this anchor has no ASCII block in the draft. The prose caption at draft line 722 is the commissioning brief.*

**Proposed filename:** `ch02-fig06-zenith-standard-crate.png` *(filename uses the conforming ID; reconcile with the anchor rename in FLAG 1)*

```yaml-figure-spec
anchor_id: ch02-zenith-standard-crate
diagram_type: other
source_ascii: ""
vendor_terms: []
complexity_hint:
  node_count: 0
  edge_count: 0
  label_count: 3
pedagogy:
  part_18_criteria_met: [zenith]
  learning_outcome: "Recognize that standardizing the interface, not improving the artifact, is what made containers and Kubernetes indifferent to their workloads"
  fixed_point_emphasis: false
  fixed_point_emphasis_target: ""
accessibility:
  alt_text_seed: "Identical standardized crates moving between carriers of visibly different kinds, each carrier built once against a published specification and handling any crate presented to it. No crate is opened; the contents are never shown and never matter."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Original commissioned illustration; no vendor IP. Not a renderable diagram — routes to the human illustrator, and blocked on era-placement confirmation against illustrator-brief.md."
```
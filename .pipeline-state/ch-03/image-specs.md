# Image Specifications — KCNA Chapter 3

*Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Source draft:** `../Book-KCNA/.pipeline-state/ch-03/draft-v1.md` (post-voice; the pre-voice copy is preserved alongside it as `draft-v1-prevoice.md`).

---

## Stage notes (author review)

<!-- AUTHOR-REVIEW: three items below. The third is a release blocker for ch03-fig04. -->

**1. Input path mismatch — the stage prompt received no draft.** This stage was invoked with the voiced draft interpolated as `[file not available: draft-voice.md]`. No file named `draft-voice.md` exists in `.pipeline-state/ch-03/`; the voice stage's output landed at `draft-v1.md` (the pre-voice draft having been rotated to `draft-v1-prevoice.md`). Specs below were extracted by reading `draft-v1.md` directly. **The stage-10 input resolver needs to read the recorded voice output path rather than assuming `draft-voice.md`, or this stage will keep receiving an empty draft on every chapter.**

**2. Figure numbering does not follow document order.** Anchors appear in the draft in the sequence fig03 → fig01 → fig04 → fig02 (draft lines 130, 218, 471, 603). Anchor IDs are format-valid (`chNN-figMM-slug`), so this is not a lint failure, but printed figure numbers will read "Figure 3.3, Figure 3.1, Figure 3.4, Figure 3.2" down the chapter. Renumbering is an author decision — per rule 6, the IDs are preserved verbatim here and in the `yaml-figure-spec` join keys. If they are renumbered, both the draft anchors and this file must be swept together. Entries below are ordered by **draft position**, not by figure number.

**3. BLOCKING: ch03-fig04 rests on an unsourced claim.** The draft carries an `AUTHOR-REVIEW` block at line 490 flagging that no cached source supports (a) *only* the API server talks to etcd, or (b) components never communicate laterally. Both assertions are the entire point of ch03-fig04 — the figure's caption tells the reader "look for the arrows that aren't drawn." Per the draft's own instruction, Stage 2 must fetch `kubernetes.io/docs/concepts/architecture/control-plane-node-communication/`. **Do not commission ch03-fig04 for render until that source is cached or the figure is redrawn without the no-lateral-arrows assertion.**

## UNANCHORED DIAGRAMS

None. The draft contains exactly four fenced blocks (draft lines 131–149, 219–243, 472–487, 604–620), and each is immediately preceded by a well-formed `<!-- FIGURE: ... -->` anchor comment. All four anchor IDs match `ch{NN}-fig{MM}-{kebab-slug}`.

---

## Figure: ch03-fig03-deployment-eras-timeline

**Anchor ID:** `ch03-fig03-deployment-eras-timeline`
**Draft position:** §1 "How the Cluster Got the Shape It Has" — after the three era paragraphs (draft line 130)
**Purpose:** Show that what changes across the three deployment eras is not the application but *what the application shares* with everything else on the machine — the observation §1 uses to motivate why container-era management is a different problem.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** three-panel comparative layer-stack diagram (left-to-right chronological progression)

**Content specification:**
Three vertically-stacked-layer panels side by side, left to right, under the headings **TRADITIONAL**, **VIRTUALIZED**, and **CONTAINER**. Left panel: a three-layer stack, bottom to top — `Hardware`, `OS`, `App` — one application only. Middle panel: bottom to top — `Hardware`, `Host OS`, `Hypervisor`, then two side-by-side `Guest OS` blocks, each carrying its own `App` block on top; the two guest stacks are separate columns above a shared hypervisor. Right panel: bottom to top — `Hardware`, `Shared OS`, then **three** small `App` blocks sitting directly on the shared OS layer, side by side with no intervening per-app OS layer. Beneath each panel, a one-line annotation in smaller type: left = *"shares: nothing (one app per box)"*; middle = *"shares: hardware (own OS per VM)"*; right = *"shares: the OS kernel."* Those three annotations are the point of the figure and must be visually tied together — set them on a common baseline across all three panels so the eye reads them as a row. A faint left-to-right progression cue (a thin rule or chevron along the top, behind the era headings) may indicate chronology, but no dates, no years, and no "time" axis label — the eras are not to scale and the figure must not imply they are. The App blocks should be identically sized and colored in all three panels, reinforcing that the application is the constant.

**Visual style:**
- Palette: inherit book default (Lodestar navy/slate line-art on cream)
- Size (pixels): 1200x520 landscape
- Font: inherit book default (Fira Sans labels, Fira Mono for component names)
- Accent color for highlighted elements: Brass #B58B3E on the three "shares:" annotation lines and the shared-layer blocks they describe (the single `OS` in panel 1, `Hardware`/`Hypervisor` band in panel 2, `Shared OS` in panel 3)

**Critical details (non-negotiable accuracy):**
- In the CONTAINER panel the App blocks sit directly on `Shared OS` — there must be **no** per-container OS layer. Drawing a guest OS inside a container is the single most damaging error this figure could make.
- In the VIRTUALIZED panel each VM has its **own** `Guest OS`, and `Hypervisor` sits between the guest stacks and the `Host OS`. Order bottom-to-top is Hardware → Host OS → Hypervisor → Guest OS → App. Do not omit `Host OS`.
- The container panel's shared layer is labelled **"Shared OS"** in the box and the annotation reads **"shares: the OS kernel."** The draft carries an open `AUTHOR-REVIEW` at line 128 about "operating system" vs "operating system kernel" wording across Ch 1/2/3; if that resolves to plain "operating system," this figure's annotation must be swept with the prose.
- Left panel shows exactly one App. Middle shows exactly two. Right shows exactly three. The increasing density is deliberate.
- Traditional era is one app *per physical server* — do not draw two apps sharing the left panel's OS.

**Source ASCII (for designer reference):**
```
   TRADITIONAL              VIRTUALIZED                CONTAINER
   ───────────              ───────────                ─────────

   ┌───────────┐          ┌─────┐ ┌─────┐            ┌───┐┌───┐┌───┐
   │    App    │          │ App │ │ App │            │App││App││App│
   ├───────────┤          ├─────┤ ├─────┤            └───┘└───┘└───┘
   │    OS     │          │Guest│ │Guest│            ┌─────────────┐
   ├───────────┤          │ OS  │ │ OS  │            │  Shared OS  │
   │ Hardware  │          ├─────┴─┴─────┤            ├─────────────┤
   └───────────┘          │  Hypervisor │            │  Hardware   │
                          ├─────────────┤            └─────────────┘
   shares: nothing        │  Host OS    │
   (one app per box)      ├─────────────┤            shares: the OS
                          │  Hardware   │            kernel
                          └─────────────┘
                          shares: hardware
                          (own OS per VM)
```

**Proposed filename:** `ch03-fig03-deployment-eras-timeline.png`

```yaml-figure-spec
anchor_id: ch03-fig03-deployment-eras-timeline
diagram_type: deployment_diagram
source_ascii: |
     TRADITIONAL              VIRTUALIZED                CONTAINER
     ───────────              ───────────                ─────────

     ┌───────────┐          ┌─────┐ ┌─────┐            ┌───┐┌───┐┌───┐
     │    App    │          │ App │ │ App │            │App││App││App│
     ├───────────┤          ├─────┤ ├─────┤            └───┘└───┘└───┘
     │    OS     │          │Guest│ │Guest│            ┌─────────────┐
     ├───────────┤          │ OS  │ │ OS  │            │  Shared OS  │
     │ Hardware  │          ├─────┴─┴─────┤            ├─────────────┤
     └───────────┘          │  Hypervisor │            │  Hardware   │
                            ├─────────────┤            └─────────────┘
     shares: nothing        │  Host OS    │
     (one app per box)      ├─────────────┤            shares: the OS
                            │  Hardware   │            kernel
                            └─────────────┘
                            shares: hardware
                            (own OS per VM)
vendor_terms: []
complexity_hint:
  node_count: 15
  edge_count: 0
  label_count: 21
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, temporal_structure, spatial_structure]
  learning_outcome: "Explain what each deployment era shares at the machine level, and why the container era changes the management problem"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the bottom row of shares: annotations, read across all three panels"
accessibility:
  alt_text_seed: "Three side-by-side layer stacks comparing traditional, virtualized, and container deployment; traditional runs one app on an OS on hardware, virtualized adds a hypervisor and a guest OS per virtual machine, and containers place three apps directly on one shared operating system"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Concept and era names come from the kubernetes.io overview page (CC BY 4.0, Linux Foundation/CNCF); redrawn from the ASCII in Lodestar's own visual language, not traced from the upstream figure."
```

---

## Figure: ch03-fig01-control-plane-and-node-components

**Anchor ID:** `ch03-fig01-control-plane-and-node-components`
**Draft position:** §2 "The Control Plane" — immediately after the cluster-shape paragraph, before the component walkthrough (draft line 218)
**Purpose:** Give the reader the complete component census on one page, split across the control-plane/node line, with the two optional components visually marked — the ★ Fixed Point at draft line 325 depends on this split.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** k8s cluster architecture diagram — two labelled regions with component boxes, plus a legend

**Content specification:**
An upper region bordered and titled **CONTROL PLANE** containing five component boxes: `kube-apiserver`, `etcd`, `kube-scheduler` on the first row; `kube-controller-manager` and `cloud-controller-manager` on the second. Below it, two separate regions each bordered and titled **NODE**, side by side, each containing three boxes: `kubelet`, `kube-proxy`, and `container runtime`. Both node regions must be drawn **complete and identical** — the source ASCII clips the right-hand node with an ellipsis purely to fit terminal width; the rendered figure has room and must show node B in full. Border treatment carries the meaning: solid border = always present; dashed border = optional. Dashed boxes are exactly two: `cloud-controller-manager` in the control plane, and `kube-proxy` in *each* node. Every other box is solid. A legend sits below the diagram showing one solid-bordered swatch reading "always present" and one dashed-bordered swatch reading "OPTIONAL (see §4)." No arrows anywhere in this figure — it is a census, not a communication diagram; the arrows are ch03-fig04's job and drawing any here would pre-empt §5. Give `container runtime` a subtly different fill or a small footnote marker: it is the one box in the figure that is not Kubernetes software.

**Visual style:**
- Palette: inherit book default (Lodestar navy/slate line-art on cream)
- Size (pixels): 1200x700 landscape
- Font: inherit book default (Fira Mono for component names — these are literal binary names and should read as such)
- Accent color for highlighted elements: Brass #B58B3E for the two dashed (optional) borders and the legend's dashed swatch

**Critical details (non-negotiable accuracy):**
- `etcd` is inside the CONTROL PLANE region. It is not a node component and not a separate tier in this figure.
- `kubelet`, `kube-proxy`, and `container runtime` are node components and appear in **both** node regions. They never appear in the control plane.
- Exactly two component *names* are dashed: `cloud-controller-manager` and `kube-proxy`. `kube-proxy` being dashed in both nodes still counts as one optional name. Nothing else is dashed — in particular `etcd` and `container runtime` are solid.
- Dashed does not mean "sometimes runs on some nodes." When kube-proxy runs, it runs on every node; it may not run at all. The border treatment must not suggest per-node variation — draw it dashed identically in both nodes.
- Eight component names total, no more. Do not add addons (CoreDNS, dashboard, metrics-server) to this figure; §4 handles addons separately and mixing them here destroys the census.
- Control plane above, nodes below. Do not invert or set them side by side — later chapters retrieve this spatial arrangement.

**Source ASCII (for designer reference):**
```
┌─── CONTROL PLANE ────────────────────────────────────────────┐
│                                                              │
│   ┌────────────────┐   ┌────────┐   ┌──────────────────┐     │
│   │ kube-apiserver │   │  etcd  │   │  kube-scheduler  │     │
│   └────────────────┘   └────────┘   └──────────────────┘     │
│                                                              │
│   ┌─────────────────────────┐   ╭─────────────────────────╮  │
│   │ kube-controller-manager │   ╎ cloud-controller-manager╎  │
│   └─────────────────────────┘   ╰─────────────────────────╯  │
└──────────────────────────────────────────────────────────────┘

┌─── NODE ─────────────────────────┐  ┌─── NODE ──────────────┐
│                                  │  │                       │
│  ┌─────────┐  ╭────────────╮     │  │  ┌─────────┐  ╭─────  │
│  │ kubelet │  ╎ kube-proxy ╎     │  │  │ kubelet │  ╎ kube-  ...
│  └─────────┘  ╰────────────╯     │  │  └─────────┘  ╰─────  │
│  ┌───────────────────┐           │  │  ┌──────────────      │
│  │ container runtime │           │  │  │ container run ...
│  └───────────────────┘           │  │  └──────────────      │
└──────────────────────────────────┘  └───────────────────────┘

  ┌───┐ solid border = always present
  ╭╌╌╌╮ dashed border = OPTIONAL (see §4)
```

**Proposed filename:** `ch03-fig01-control-plane-and-node-components.png`

```yaml-figure-spec
anchor_id: ch03-fig01-control-plane-and-node-components
diagram_type: k8s_architecture
source_ascii: |
  ┌─── CONTROL PLANE ────────────────────────────────────────────┐
  │                                                              │
  │   ┌────────────────┐   ┌────────┐   ┌──────────────────┐     │
  │   │ kube-apiserver │   │  etcd  │   │  kube-scheduler  │     │
  │   └────────────────┘   └────────┘   └──────────────────┘     │
  │                                                              │
  │   ┌─────────────────────────┐   ╭─────────────────────────╮  │
  │   │ kube-controller-manager │   ╎ cloud-controller-manager╎  │
  │   └─────────────────────────┘   ╰─────────────────────────╯  │
  └──────────────────────────────────────────────────────────────┘

  ┌─── NODE ─────────────────────────┐  ┌─── NODE ──────────────┐
  │                                  │  │                       │
  │  ┌─────────┐  ╭────────────╮     │  │  ┌─────────┐  ╭─────  │
  │  │ kubelet │  ╎ kube-proxy ╎     │  │  │ kubelet │  ╎ kube-  ...
  │  └─────────┘  ╰────────────╯     │  │  └─────────┘  ╰─────  │
  │  ┌───────────────────┐           │  │  ┌──────────────      │
  │  │ container runtime │           │  │  │ container run ...
  │  └───────────────────┘           │  │  └──────────────      │
  └──────────────────────────────────┘  └───────────────────────┘

    ┌───┐ solid border = always present
    ╭╌╌╌╮ dashed border = OPTIONAL (see §4)
vendor_terms: [kube-apiserver, etcd, kube-scheduler, kube-controller-manager, cloud-controller-manager, kubelet, kube-proxy, containerd]
complexity_hint:
  node_count: 14
  edge_count: 0
  label_count: 16
pedagogy:
  part_18_criteria_met: [spatial_structure, vendor_taxonomy, distinguishing_alternatives]
  learning_outcome: "Place any Kubernetes component on the correct side of the control-plane/node line and name the two that are optional"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the two dashed-border boxes, cloud-controller-manager and kube-proxy"
accessibility:
  alt_text_seed: "Cluster component census: a control plane region holding kube-apiserver, etcd, kube-scheduler, kube-controller-manager and a dashed optional cloud-controller-manager, above two node regions each holding kubelet, a dashed optional kube-proxy, and a container runtime"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Component names are upstream Kubernetes binary names (factual, not protectable); layout and the solid/dashed optionality convention are Lodestar's own, not the upstream components figure."
```

---

## Figure: ch03-fig04-request-path-through-apiserver

**Anchor ID:** `ch03-fig04-request-path-through-apiserver`
**Draft position:** §5 "The Only Door In" — after the three-facts paragraph, before "What follows from a hub" (draft line 471)
**Purpose:** Show the cluster's communication shape as a hub rather than a chain of command, so the reader can see that the *absent* edges — scheduler-to-kubelet, node-to-node, anything-to-etcd — are what the architecture is made of.
**Replaces ASCII:** yes
**Mandatory:** yes
**⚠ Render status:** BLOCKED pending source resolution — see Stage note 3 above and the draft's `AUTHOR-REVIEW` at line 490.
**Type:** hub-and-spoke data-flow diagram

**Content specification:**
`kube-apiserver` sits at the centre, drawn as the largest box in the figure. Five peripheral actors surround it: across the top, `kubectl`, `kube-scheduler`, and `kube-controller-manager`; at the lower left and lower right, `kubelet (node A)` and `kubelet (node B)`. Each of those five connects to the central box with a single edge. Directly below `kube-apiserver`, and connected only to it, sits `etcd`. Edge directions: the three top actors have arrows pointing *into* the API server; the two kubelets have arrows pointing *into* the API server; the API server has one arrow pointing *down into* etcd. Every edge terminates at the API server except the single API-server-to-etcd edge. Draw the etcd edge bidirectional (read and write) or as a single double-headed line — the API server both reads and writes the store. Nothing else touches etcd. There must be **no** edge between any two peripheral actors: no scheduler-to-kubelet line, no kubelet-to-kubelet line, no controller-manager-to-etcd line. Leave visible whitespace along those non-paths so the missing edges are legible as absence rather than as crowding — the caption instructs the reader to look for them. Consider a very faint dotted "no path" indicator between node A and node B with a small ✗, but only if it can be done without reading as a real connection; if in doubt, leave the space empty.

**Visual style:**
- Palette: inherit book default (Lodestar navy/slate line-art on cream)
- Size (pixels): 1100x750 landscape
- Font: inherit book default (Fira Mono for component names, Fira Sans for the "(node A)" / "(node B)" qualifiers)
- Accent color for highlighted elements: Brass #B58B3E for the `kube-apiserver` box border and the single API-server↔etcd edge

**Critical details (non-negotiable accuracy):**
- `kube-apiserver` is the only box with an edge to `etcd`. This is the entire assertion of the figure — and the assertion currently lacking a cached source. Do not render until Stage 2 resolves it.
- `kubectl` is outside the cluster's component set — it is the tool the reader types into. Distinguish it visually from the four in-cluster components (lighter weight border, or set slightly apart) so nobody reads it as a cluster component.
- Zero peripheral-to-peripheral edges. If the illustrator adds a "helpful" scheduler→kubelet arrow, the figure teaches the opposite of §5.
- Two kubelets on two different nodes, labelled `(node A)` and `(node B)`. They are not connected to each other.
- No arrow from `etcd` outward to anything except back to `kube-apiserver`.
- The figure shows *paths*, not sequence. Do not number the edges or imply an order of operations — the submission story that follows in prose is where ordering gets taught.

**Source ASCII (for designer reference):**
```
    kubectl          kube-scheduler       kube-controller-manager
       │                    │                        │
       │                    │                        │
       └──────────┐         │         ┌──────────────┘
                  ▼         ▼         ▼
              ┌───────────────────────────┐
              │      kube-apiserver       │
              └───────────────────────────┘
                  ▲         │         ▲
       ┌──────────┘         │         └──────────────┐
       │                    ▼                        │
       │              ┌──────────┐                   │
   kubelet            │   etcd   │               kubelet
   (node A)           └──────────┘               (node B)
```

**Proposed filename:** `ch03-fig04-request-path-through-apiserver.png`

```yaml-figure-spec
anchor_id: ch03-fig04-request-path-through-apiserver
diagram_type: data_flow
source_ascii: |
      kubectl          kube-scheduler       kube-controller-manager
         │                    │                        │
         │                    │                        │
         └──────────┐         │         ┌──────────────┘
                    ▼         ▼         ▼
                ┌───────────────────────────┐
                │      kube-apiserver       │
                └───────────────────────────┘
                    ▲         │         ▲
         ┌──────────┘         │         └──────────────┐
         │                    ▼                        │
         │              ┌──────────┐                   │
     kubelet            │   etcd   │               kubelet
     (node A)           └──────────┘               (node B)
vendor_terms: [kubectl, kube-apiserver, kube-scheduler, kube-controller-manager, kubelet, etcd]
complexity_hint:
  node_count: 7
  edge_count: 6
  label_count: 9
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "Recognize the cluster as a hub around the API server, and identify which component pairs never communicate directly"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the kube-apiserver box and its sole edge to etcd"
accessibility:
  alt_text_seed: "Hub diagram with kube-apiserver at the center; kubectl, kube-scheduler, kube-controller-manager, and two kubelets each connect only to the API server, and the API server alone connects to etcd, with no direct links between any of the surrounding components"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1100
copyright_clearance:
  rights_holders: [cncf]
  clearance: flagged_for_legal_review
  notes: "Not an IP concern — flagged because the depicted architecture is not yet supported by a cached source (draft AUTHOR-REVIEW line 490); clearance downgrades to own_interpretation once control-plane-node-communication is fetched."
```

---

## Figure: ch03-fig02-control-loop-desired-vs-current

**Anchor ID:** `ch03-fig02-control-loop-desired-vs-current`
**Draft position:** §6 "Controllers and the Control Loop" — after the thermostat passage and the controllers definition (draft line 603)
**Purpose:** Render the control loop as a genuinely closed cycle with no entry point and no terminus, so the reader stops picturing controllers as procedures that start, run, and finish — the ★ Fixed Point at draft line 641 and six later chapters retrieve this.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** cyclic flowchart (closed loop, no start or end node)

**Content specification:**
Four nodes arranged around a closed cycle: `DESIRED STATE`, `CURRENT STATE`, `COMPARE`, and `ACT TO CLOSE THE GAP`. The cycle reads: `COMPARE` reads both `DESIRED STATE` and `CURRENT STATE`; a gap between them drives `ACT TO CLOSE THE GAP`; acting changes the world, which changes `CURRENT STATE`; and the loop returns to `COMPARE`. Draw it so the eye can traverse the cycle continuously without finding a place to enter or exit. There must be **no** start node, no stop node, no terminator shape, no numbered steps, and no arrow entering the figure from outside or leaving it. Below the loop, set the line **"no start. no end. no exit condition."** as figure text (not caption) in the same weight as the node labels — it is part of the diagram's argument. Because `DESIRED STATE` and `CURRENT STATE` are the two inputs to `COMPARE`, place them symmetrically on either side of it so their parity is visible; `ACT TO CLOSE THE GAP` sits on the return path from `COMPARE` back to `CURRENT STATE`.

*Note to the author before render:* the source ASCII's edge directions are ambiguous — it appears to show `COMPARE → CURRENT STATE`, which inverts the causality (COMPARE observes current state; it does not produce it). The specification above states the semantically correct edges. Confirm this reading before the illustrator commits, since the redrawn figure will not match the ASCII arrow-for-arrow.

**Visual style:**
- Palette: inherit book default (Lodestar navy/slate line-art on cream)
- Size (pixels): 900x750 portrait-ish square
- Font: inherit book default (Fira Sans, small caps or uppercase for the four node labels as in the ASCII)
- Accent color for highlighted elements: Brass #B58B3E on the cycle edges themselves — the closed path, not any single box, is what earns emphasis here

**Critical details (non-negotiable accuracy):**
- The loop is closed. A single stray entry arrow ruins the figure's only teaching point; the caption explicitly says "a loop drawn with a beginning teaches the wrong thing."
- `COMPARE` takes two inputs — desired and current. Both edges into COMPARE must be drawn; dropping either makes it look like a one-sided check.
- The action changes `CURRENT STATE`, not `DESIRED STATE`. Nothing in this loop writes to desired state — that comes from outside, and the figure deliberately does not show it.
- No thermostat imagery, no temperature dial, no furnace. The thermostat is prose analogy only; the figure is the abstract loop. A literal thermostat would make readers file this as "the HVAC diagram" and fail to retrieve it in Chapter 15.
- Four nodes exactly. Do not add "watch," "reconcile," or "requeue" — those are vocabulary the chapter has not introduced.
- The "no start. no end. no exit condition." line stays inside the image, so it survives if the figure is viewed apart from its caption.

**Source ASCII (for designer reference):**
```
              ┌──────────────────┐
       ┌─────▶│  DESIRED STATE   │──────┐
       │      └──────────────────┘      │
       │                                ▼
  ┌─────────┐                     ┌──────────┐
  │ CURRENT │◀────────────────────│ COMPARE  │
  │  STATE  │                     └──────────┘
  └─────────┘                           │
       ▲                                ▼
       │      ┌──────────────────┐      │
       └──────│  ACT TO CLOSE    │◀─────┘
              │     THE GAP      │
              └──────────────────┘

        no start.  no end.  no exit condition.
```

**Proposed filename:** `ch03-fig02-control-loop-desired-vs-current.png`

```yaml-figure-spec
anchor_id: ch03-fig02-control-loop-desired-vs-current
diagram_type: flowchart
source_ascii: |
                ┌──────────────────┐
         ┌─────▶│  DESIRED STATE   │──────┐
         │      └──────────────────┘      │
         │                                ▼
    ┌─────────┐                     ┌──────────┐
    │ CURRENT │◀────────────────────│ COMPARE  │
    │  STATE  │                     └──────────┘
    └─────────┘                           │
         ▲                                ▼
         │      ┌──────────────────┐      │
         └──────│  ACT TO CLOSE    │◀─────┘
                │     THE GAP      │
                └──────────────────┘

          no start.  no end.  no exit condition.
vendor_terms: []
complexity_hint:
  node_count: 4
  edge_count: 4
  label_count: 5
pedagogy:
  part_18_criteria_met: [temporal_structure, fixed_point]
  learning_outcome: "Describe a controller as a non-terminating loop that compares desired to current state and acts on the difference, rather than as a procedure that runs to completion"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the closed cycle path itself — no entry arrow, no terminus"
accessibility:
  alt_text_seed: "A closed four-step cycle with no beginning or end: compare reads desired state and current state, acting to close the gap changes current state, and comparison begins again; captioned no start, no end, no exit condition"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 900
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Desired/current-state control-loop concept is from the kubernetes.io controllers page (CC BY 4.0); the closed-cycle rendering with the no-start-no-end assertion is Lodestar's own pedagogical framing."
```
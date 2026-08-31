# Image Specifications — KCNA Chapter 17

*Generated from `draft-v1.md` (draft-voice.md does not exist at this stage). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Figures found: 8. Unanchored ASCII diagrams: 0.**

---

## ANCHOR FLAGS (author review)

**1. One anchor does not match the `ch{NN}-fig{MM}-{kebab-slug}` convention.**

| Anchor as written in draft | Problem | Location |
|---|---|---|
| `ch17-zenith-one-pluggability-story` | No `fig{MM}` segment. Reads `ch17-zenith-...` where the contract requires `ch17-figMM-...`. | §9, the ☀️ Zenith section |

Suggested conforming ID: `ch17-fig08-one-pluggability-story`. **Not renamed here** — anchor IDs are the join key and renaming is an author-review decision (draft prose and this document must change together, in one commit). Its full entry appears below under the ID as currently written.

**2. Figure numbers are contiguous but appear out of document order.**

Document order is: `fig01`, `fig05`, `fig02`, `fig03`, `fig07`, `fig04`, `fig06`, then the zenith anchor. The set 01–07 is complete with no gaps and no duplicates, so nothing is missing — but any reader-facing numbering ("Figure 17.1, 17.2…") derived from document position will disagree with the anchor IDs. Author to decide whether to renumber the anchors to match reading order or to suppress printed figure numbers for this chapter.

**3. No unanchored diagrams.** Every fenced block in the draft is preceded by a `<!-- FIGURE: -->` comment. Nothing to flag under UNANCHORED DIAGRAMS.

---

## Figure: ch17-fig01-cloud-native-definition-characteristics

**Anchor ID:** `ch17-fig01-cloud-native-definition-characteristics`
**Purpose:** Fix in memory that the five characteristics of cloud native are *attached to* loosely coupled systems rather than floating free — the exact structure the exam quotes back.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hierarchical fan-out (one root, five annotated leaves)

**Content specification:**
A single wide root box sits centred at the top, containing two lines of type: **LOOSELY COUPLED SYSTEMS** on the first line (large, emphatic) and *that interoperate in a manner that is:* on the second (smaller, lighter — it is a connective phrase, not a title). A single short stem descends from the centre of that box to a horizontal distributor rule. Five evenly spaced vertical drops descend from that rule to five leaf labels, left to right: **SECURE**, **RESILIENT**, **MANAGEABLE**, **SUSTAINABLE**, **OBSERVABLE**. Beneath each leaf label, set in noticeably smaller and lighter type, is a short gloss of two to four lines: *verified at every boundary, not just at the edge* / *survives the loss of any one part* / *changeable without rebuilding it* / *affordable to keep running, in people and in power* / *you can ask it what it is doing, and it will answer*. The point of the figure is the attachment — the five words are children of the loose coupling, and a designer must not redraw this as a flat list of five equal peers. The root box carries the accent; the five leaves are uniform with each other, because no one characteristic outranks another.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream)
- Size (pixels): 1200x700 landscape
- Font: inherit book default (Roboto Slab display, Fira Sans body)
- Accent color for highlighted elements: Brass `#B58B3E` on the root "LOOSELY COUPLED SYSTEMS" box only

**Critical details (non-negotiable accuracy):**
- Exactly **five** characteristics, in the definition's own order: secure, resilient, manageable, sustainable, observable. Not four, not six, and not reordered — the order is quoted from CNCF Cloud Native Definition v1.1 and the prose beside the figure quotes it verbatim.
- The five must hang **from** the root, not sit beside it. A flat five-box row destroys the figure's argument.
- The five characteristic words are CNCF's; the glosses beneath them are this book's. They must be visually subordinate (smaller, lighter) so no reader mistakes the gloss for quoted definition text.
- "SUSTAINABLE" means affordable to keep running (people and power), not environmentally sustainable as a separate claim. Do not add a leaf/recycling glyph — it would assert something the source does not.
- No CNCF logo, no cloud iconography anywhere in the figure. The whole point of the surrounding section is that *cloud native* is not about clouds.

**Source ASCII (for designer reference):**
```
                  LOOSELY COUPLED SYSTEMS
                  that interoperate in a manner that is:
                              |
    +---------+---------+-----+-----+---------+-----------+
    |         |         |           |         |           |
 SECURE   RESILIENT  MANAGEABLE  SUSTAINABLE      OBSERVABLE

 verified   survives   changeable   affordable    you can ask
 at every   the loss   without       to keep      it what it
 boundary,  of any     rebuilding    running,     is doing,
 not just   one part   it            in people    and it will
 at the                              and in       answer
 edge                                power
```

**Proposed filename:** `ch17-fig01-cloud-native-definition-characteristics.png`

```yaml-figure-spec
anchor_id: ch17-fig01-cloud-native-definition-characteristics
diagram_type: hierarchy_tree
source_ascii: |2
                    LOOSELY COUPLED SYSTEMS
                    that interoperate in a manner that is:
                                |
      +---------+---------+-----+-----+---------+-----------+
      |         |         |           |         |           |
   SECURE   RESILIENT  MANAGEABLE  SUSTAINABLE      OBSERVABLE
  
   verified   survives   changeable   affordable    you can ask
   at every   the loss   without       to keep      it what it
   boundary,  of any     rebuilding    running,     is doing,
   not just   one part   it            in people    and it will
   at the                              and in       answer
   edge                                power
vendor_terms: []
complexity_hint:
  node_count: 6
  edge_count: 5
  label_count: 11
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "State the five characteristics of cloud native and recognise that they are properties of loosely coupled systems, not a free-standing list"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the root box reading LOOSELY COUPLED SYSTEMS"
accessibility:
  alt_text_seed: "A single root box labelled LOOSELY COUPLED SYSTEMS branches down to five characteristics: secure, resilient, manageable, sustainable, and observable, each with a short explanatory gloss beneath it"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Structure redrawn in Lodestar style over the five characteristic terms of CNCF Cloud Native Definition v1.1; short quotation, cited in adjacent prose, no marks reproduced."
```

---

## Figure: ch17-fig05-cncf-maturity-levels

**Anchor ID:** `ch17-fig05-cncf-maturity-levels`
**Purpose:** Fix the maturity ladder in the correct order, make each rung's *assertion* the memorable thing rather than the project roster, and put Archived visibly off the ladder.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** ascending staircase / stacked progression with a detached terminal state

**Content specification:**
Three nested, ascending steps drawn as a staircase rising left-to-right, bottom-to-top. The widest and lowest step is **SANDBOX**, captioned *experimental; not yet widely tested in production; bleeding edge*. Sitting on top of it and inset from the left is **INCUBATING**, captioned *in production use by a small number of users; healthy pool of contributors*. Sitting on top of that and inset again is **GRADUATED**, captioned *stable, widely adopted, production ready*. The steps must read as one continuous climb — each rung resting on the one below it, not three detached boxes — because "you cannot skip a rung" is part of what the shape asserts. Below the staircase, an upward-pointing caret with a single annotation line reads: *the criteria for each step live with the TOC, in the project lifecycle documentation — NOT on the projects page*. Set apart from the staircase entirely, in a bracketed side note with clearly different treatment (dashed border, greyed, offset to one side, no structural connection to any rung), is: *ARCHIVED is not a rung. It is where projects go when they stop.* The GRADUATED step carries the accent. No project names appear anywhere on this figure — deliberately, and the caption in the draft says so.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream)
- Size (pixels): 1000x750 landscape
- Font: inherit book default
- Accent color for highlighted elements: Brass `#B58B3E` on the GRADUATED step; the ARCHIVED side note in muted grey, deliberately un-accented

**Critical details (non-negotiable accuracy):**
- Order is **Sandbox → Incubating → Graduated**, ascending. Reversing it, or putting Sandbox at the top, inverts the section's single most examinable fact.
- **Archived must never touch the staircase.** No arrow from Graduated to Archived, no fourth step, no ghosted rung. It is a terminal state reachable from anywhere, and drawing it as a step is the exact error the figure exists to prevent.
- The criteria annotation must say the criteria live with the **TOC / project lifecycle documentation**, not on the projects page. This distinction is a graded question in the chapter.
- Zero project names, logos, or counts. The roster changes faster than a printed book; the caption in the draft commits to this omission explicitly.
- Rung captions are close paraphrases of CNCF's published level descriptions — keep the load-bearing words ("small number of users", "healthy pool of contributors", "widely adopted", "bleeding edge") intact if the designer reflows the text.

**Source ASCII (for designer reference):**
```
                                    +--------------------+
                                    |     GRADUATED      |
                                    |  stable, widely    |
                                    |  adopted,          |
                                    |  production ready  |
                    +---------------+--------------------+
                    |    INCUBATING                      |
                    |  in production use by a small       |
                    |  number of users; healthy pool      |
                    |  of contributors                    |
    +---------------+-------------------------------------+
    |    SANDBOX                                          |
    |  experimental; not yet widely tested in             |
    |  production; bleeding edge                          |
    +-----------------------------------------------------+

    ^ the criteria for each step live with the TOC, in the
      project lifecycle documentation -- NOT on the projects page

    ( ARCHIVED is not a rung. It is where projects go when
      they stop. See below. )
```

**Proposed filename:** `ch17-fig05-cncf-maturity-levels.png`

```yaml-figure-spec
anchor_id: ch17-fig05-cncf-maturity-levels
diagram_type: flowchart
source_ascii: |2
                                      +--------------------+
                                      |     GRADUATED      |
                                      |  stable, widely    |
                                      |  adopted,          |
                                      |  production ready  |
                      +---------------+--------------------+
                      |    INCUBATING                      |
                      |  in production use by a small       |
                      |  number of users; healthy pool      |
                      |  of contributors                    |
      +---------------+-------------------------------------+
      |    SANDBOX                                          |
      |  experimental; not yet widely tested in             |
      |  production; bleeding edge                          |
      +-----------------------------------------------------+
  
      ^ the criteria for each step live with the TOC, in the
        project lifecycle documentation -- NOT on the projects page
  
      ( ARCHIVED is not a rung. It is where projects go when
        they stop. See below. )
vendor_terms: []
complexity_hint:
  node_count: 4
  edge_count: 3
  label_count: 8
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Order the CNCF maturity levels and state what each one asserts, while recognising Archived as a terminal state rather than a rung"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the GRADUATED step at the top of the staircase"
accessibility:
  alt_text_seed: "An ascending three-step staircase labelled Sandbox at the bottom, Incubating in the middle, and Graduated at the top, each step captioned with what that level asserts, with a separate detached note explaining that Archived is not a rung"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Level names and short descriptions paraphrase the public CNCF projects page; redrawn structure, no logos or project marks."
```

---

## Figure: ch17-fig02-extension-points-map

**Anchor ID:** `ch17-fig02-extension-points-map`
**Purpose:** Show the book's four pluggable interfaces as four instances of one shape, each at the layer it serves, with the chapter that taught it — the single most reused idea in the book, and the setup for §9's Zenith.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** layered architecture stack with annotated extension sockets

**Content specification:**
A vertical stack of three horizontal bands, drawn as one contiguous slab with heavy double rules between bands. Top band: **THE KUBERNETES API SURFACE**. Middle band: **CONTROL PLANE** (thin, unadorned — it is a spacer that establishes vertical position, and it has no socket). Bottom band: **THE NODE**, and it is the tallest, because it holds three entries. Inside the top band, one entry reads **CRDs** with a dotted leader running right to *new object kinds*. Inside the bottom band, three entries stacked with generous spacing: **CRI** … *running containers*; **CNI** … *pod networking*; **CSI** … *attaching storage*. On the left edge of the slab, level with each of those four entries, sits a socket glyph — a small circle with a short connector stub running left out of the slab — and immediately to the left of each socket, in small type, the chapter reference: `Ch 6 §8` for CRDs, `Ch 2 §4` for CRI, `Ch 9 §1` for CNI, `Ch 11 §5` for CSI. A legend below the slab reads: *(o) = a socket. Kubernetes defines the shape. Somebody else supplies the plug.* All four sockets must be drawn **identically** — the visual sameness of four sockets at three different layers is the entire argument, and any variation between them undermines it. Use the same socket glyph again in the §9 Zenith figure so the two read as one family.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream)
- Size (pixels): 900x1150 portrait (authored near 3:4 for e-reader column fit)
- Font: inherit book default; monospace (Fira Mono) for the interface acronyms and chapter references
- Accent color for highlighted elements: Brass `#B58B3E` on all four socket glyphs — uniformly, never on just one

**Critical details (non-negotiable accuracy):**
- **CRDs sit at the API surface (top). CRI, CNI and CSI sit at the node (bottom).** Placing CRDs down among the node plugins destroys the figure's information; placing CRI/CNI/CSI at the API surface is factually wrong.
- The control-plane band has **no socket**. It is present to establish that the API surface and the node are separated, not to add a fifth extension point.
- Chapter references must be exact: CRDs `Ch 6 §8`, CRI `Ch 2 §4`, CNI `Ch 9 §1`, CSI `Ch 11 §5`. These are verified against the book's section skeleton and are the figure's navigation value.
- All four sockets identical in size, shape and weight. Sameness *is* the content.
- Descriptions must stay as written: CRI = running containers, CNI = pod networking, CSI = attaching storage, CRDs = new object kinds. Do not "improve" CSI to "storage provisioning" — attachment is the verb the chapter uses.
- No implementation names (containerd, Calico, Cilium, vendor drivers) on the figure. The plugs are deliberately absent; that is what the empty sockets mean.

**Source ASCII (for designer reference):**
```
            +==================================================+
            |          THE KUBERNETES API SURFACE              |
            |                                                  |
    (o)-----|  CRDs                     ..... new object kinds |
   Ch 6 §8  |                                                  |
            +==================================================+
            |               CONTROL PLANE                      |
            +==================================================+
            |               THE NODE                           |
            |                                                  |
    (o)-----|  CRI          ............. running containers   |
   Ch 2 §4  |                                                  |
            |                                                  |
    (o)-----|  CNI          ............. pod networking       |
   Ch 9 §1  |                                                  |
            |                                                  |
    (o)-----|  CSI          ............. attaching storage    |
   Ch 11 §5 |                                                  |
            +==================================================+

            (o) = a socket. Kubernetes defines the shape.
                  Somebody else supplies the plug.
```

**Proposed filename:** `ch17-fig02-extension-points-map.png`

```yaml-figure-spec
anchor_id: ch17-fig02-extension-points-map
diagram_type: k8s_architecture
source_ascii: |2
              +==================================================+
              |          THE KUBERNETES API SURFACE              |
              |                                                  |
      (o)-----|  CRDs                     ..... new object kinds |
     Ch 6 §8  |                                                  |
              +==================================================+
              |               CONTROL PLANE                      |
              +==================================================+
              |               THE NODE                           |
              |                                                  |
      (o)-----|  CRI          ............. running containers   |
     Ch 2 §4  |                                                  |
              |                                                  |
      (o)-----|  CNI          ............. pod networking       |
     Ch 9 §1  |                                                  |
              |                                                  |
      (o)-----|  CSI          ............. attaching storage    |
     Ch 11 §5 |                                                  |
              +==================================================+
  
              (o) = a socket. Kubernetes defines the shape.
                    Somebody else supplies the plug.
vendor_terms: [kubernetes]
complexity_hint:
  node_count: 7
  edge_count: 4
  label_count: 12
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "State the shape CRI, CNI, CSI and CRDs have in common, and place each at the layer of the cluster it serves"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the four identical socket glyphs on the left edge"
accessibility:
  alt_text_seed: "A three-band Kubernetes stack: the API surface at the top holding CRDs for new object kinds, a control plane band in the middle, and the node at the bottom holding CRI for running containers, CNI for pod networking, and CSI for attaching storage; four identical sockets on the left edge mark each extension point with its chapter reference"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 900
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Depicts Kubernetes interface names and architecture concepts only; original diagram, no upstream figure reproduced, no project logos."
```

---

## Figure: ch17-fig03-mesh-data-vs-control-plane

**Anchor ID:** `ch17-fig03-mesh-data-vs-control-plane`
**Purpose:** Defuse the chapter's most dangerous vocabulary collision by drawing the mesh's two planes and the cluster's control plane as three separate things in one frame, and show sidecar and ambient as two arrangements of one data plane.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** layered component diagram with a two-column comparison in the lower register

**Content specification:**
Three registers, top to bottom, with the separation between the first and second doing the pedagogical work. **Top register:** a box drawn in a visibly *different* treatment from everything else — heavier or hatched border, clearly a foreign object — labelled **THE CLUSTER'S CONTROL PLANE (Ch 3 §2)**, listing *kube-apiserver · etcd · scheduler · controller-manager* and the line *Manages: Kubernetes OBJECTS*. Directly beneath it, in small italics, the aside *(a different thing entirely)*, followed by a generous band of white space and no connecting line of any kind. **Middle register:** a box labelled **THE MESH'S CONTROL PLANE**, reading *Distributes policy + certificates to the proxies* and *Manages: PROXIES*. Three arrows descend from its lower edge into the register below. **Bottom register:** a wide band headed **THE MESH'S DATA PLANE — the proxies themselves**, with the subhead *Every byte between services passes through here*, split by a vertical divider into two columns. Left column, headed **SIDECAR MODE**: two Pod boxes, each containing *app ↔ [E]*. Right column, headed **AMBIENT MODE**: two Pod boxes each containing only *app*, with lines running out of the column down to two labelled components outside the Pods — *[ztunnel] per-NODE L4* and *[waypoint] per-NS L7 (Envoy)*. Beneath the left column: *one Envoy per Pod*. A legend closes the figure: *[E] = Envoy. Both columns are the SAME data plane, arranged two ways — not two products.*

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream)
- Size (pixels): 1000x1300 portrait (authored near 3:4)
- Font: inherit book default; monospace for component names (ztunnel, waypoint, kube-apiserver, etcd)
- Accent color for highlighted elements: Brass `#B58B3E` on every Envoy instance — the `[E]` markers in sidecar mode and the waypoint proxy in ambient mode — so the shared engine is visible at a glance. The cluster's control plane box gets no accent at all; it is deliberately the odd one out.

**Critical details (non-negotiable accuracy):**
- **No line, arrow, or bracket may connect the cluster's control plane to either mesh plane.** The visual disconnection is the entire point of including it. If a designer "tidies" the layout by joining them, the figure teaches the opposite of what the section says.
- Arrows run **downward** from the mesh's control plane to the data plane. The control plane configures the proxies; the proxies do not configure the control plane.
- **Both columns use Envoy.** The waypoint proxy must be labelled as Envoy. Rendering ambient mode as Envoy-free is the exact misconception the ⚠ Navigational Hazards block beside this figure exists to correct.
- Ambient-mode Pods contain **only the app** — no proxy inside the Pod boundary. ztunnel and waypoint sit outside the Pods.
- ztunnel is **per-node, L4**. Waypoint is **per-namespace, L7**, and optional. Swapping those layers or scopes is a factual error.
- The two columns are two arrangements, not two products, and not a before/after. Avoid arrows between the columns and avoid any "→" implying migration.

**Source ASCII (for designer reference):**
```
   ############################################################
   #  THE CLUSTER'S CONTROL PLANE            ( Ch 3 §2 )      #
   #  kube-apiserver . etcd . scheduler . controller-manager  #
   #  Manages: Kubernetes OBJECTS                             #
   ############################################################
                    (a different thing entirely)


   +----------------------------------------------------------+
   |  THE MESH'S CONTROL PLANE                                |
   |  Distributes policy + certificates to the proxies        |
   |  Manages: PROXIES                                        |
   +----------------------------------------------------------+
              |                 |                 |
              v                 v                 v
   ------------------------------------------------------------
     THE MESH'S DATA PLANE  -- the proxies themselves
     Every byte between services passes through here

     SIDECAR MODE                 |  AMBIENT MODE
                                  |
     +--------------+             |  +--------------+
     | Pod          |             |  | Pod          |
     |  app <-> [E] |             |  |  app         |
     +--------------+             |  +--------------+
     +--------------+             |  +--------------+
     | Pod          |             |  | Pod          |
     |  app <-> [E] |             |  |  app         |
     +--------------+             |  +--------------+
                                  |         |
     one Envoy per Pod            |    [ztunnel]  per-NODE L4
                                  |    [waypoint] per-NS  L7 (Envoy)
   ------------------------------------------------------------

     [E] = Envoy.  Both columns are the SAME data plane,
           arranged two ways -- not two products.
```

**Proposed filename:** `ch17-fig03-mesh-data-vs-control-plane.png`

```yaml-figure-spec
anchor_id: ch17-fig03-mesh-data-vs-control-plane
diagram_type: k8s_architecture
source_ascii: |2
     ############################################################
     #  THE CLUSTER'S CONTROL PLANE            ( Ch 3 §2 )      #
     #  kube-apiserver . etcd . scheduler . controller-manager  #
     #  Manages: Kubernetes OBJECTS                             #
     ############################################################
                      (a different thing entirely)
  
  
     +----------------------------------------------------------+
     |  THE MESH'S CONTROL PLANE                                |
     |  Distributes policy + certificates to the proxies        |
     |  Manages: PROXIES                                        |
     +----------------------------------------------------------+
                |                 |                 |
                v                 v                 v
     ------------------------------------------------------------
       THE MESH'S DATA PLANE  -- the proxies themselves
       Every byte between services passes through here
  
       SIDECAR MODE                 |  AMBIENT MODE
                                    |
       +--------------+             |  +--------------+
       | Pod          |             |  | Pod          |
       |  app <-> [E] |             |  |  app         |
       +--------------+             |  +--------------+
       +--------------+             |  +--------------+
       | Pod          |             |  | Pod          |
       |  app <-> [E] |             |  |  app         |
       +--------------+             |  +--------------+
                                    |         |
       one Envoy per Pod            |    [ztunnel]  per-NODE L4
                                    |    [waypoint] per-NS  L7 (Envoy)
     ------------------------------------------------------------
  
       [E] = Envoy.  Both columns are the SAME data plane,
             arranged two ways -- not two products.
vendor_terms: [istio, envoy, ztunnel, waypoint, kubernetes, etcd, kube-apiserver]
complexity_hint:
  node_count: 10
  edge_count: 7
  label_count: 16
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Distinguish a service mesh's data plane from its control plane, and both from the cluster's control plane; recognise sidecar and ambient as two arrangements of one data plane"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "every Envoy instance — the [E] sidecars and the ambient waypoint — accented identically to show one engine in both modes"
accessibility:
  alt_text_seed: "Three separate layers: the cluster's control plane drawn apart at the top with no connection to anything, the mesh's control plane below it sending arrows down to the mesh's data plane, and the data plane split into a sidecar column with an Envoy proxy inside each Pod and an ambient column where Pods hold only the app and proxying happens in a per-node ztunnel and an optional per-namespace Envoy waypoint"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Istio and Envoy are CNCF projects; architecture redrawn from published descriptions in Lodestar style, no upstream figure traced and no project logos used."
```

---

## Figure: ch17-fig07-scale-to-zero-and-the-knative-service

**Anchor ID:** `ch17-fig07-scale-to-zero-and-the-knative-service`
**Purpose:** Kill the "serverless means no containers" misconception by drawing the containers and Pods that exist at every populated step of a scale-to-zero cycle.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** temporal cycle / lifecycle flow with nested container detail

**Content specification:**
A left-to-right progression across three labelled stages along the top, then a return path along the bottom, forming a closed cycle. **Stage 1, IDLE:** a Knative Service box reading *replicas: 0*, and beneath it an empty dashed outline captioned *(nothing running)* — genuinely empty, no ghosted Pod. **Stage 2, REQUEST ARRIVES:** a Knative Service box reading *replicas: 0 → N* with the parenthetical *(KPA scales up)*, and beneath it one Pod box drawn as an outer rounded rectangle labelled **Pod** containing a distinct inner rectangle labelled **container**. **Stage 3, SERVING:** a Knative Service box reading *replicas: N*, with two Pod boxes beneath it — the first drawn in full with its inner container visible, the second abbreviated as *Pod …* to imply the rest. From stage 3 a return path descends and runs right-to-left along the bottom, labelled **TRAFFIC STOPS**, through an arrow annotated *KPA scales down* and a node reading *replicas: N → 0*, back to the idle Knative Service at the left. A closing caption sits under the whole cycle: *The containers and Pods are real at every populated step. "Serverless" describes the LIFECYCLE, not their absence.* The nested container-inside-Pod rendering is not decoration — it is the section's ★ Fixed Point, and must survive any simplification the designer applies elsewhere.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream)
- Size (pixels): 1200x800 landscape
- Font: inherit book default; monospace for `replicas: 0`, `replicas: N`, and KPA
- Accent color for highlighted elements: Brass `#B58B3E` on the inner container rectangles — the thing the reader is being told is still there

**Critical details (non-negotiable accuracy):**
- Every populated stage must show a **container drawn inside a Pod**, two nested boundaries. Flattening the Pod and container into one box removes the only reason this figure exists.
- The idle state is genuinely **zero replicas** — an empty region, not one greyed-out or dimmed Pod. "Not one idle replica burning memory" is the sentence the figure illustrates.
- The scaler is the **KPA (Knative Pod Autoscaler)**, named on both the up and down transitions. Do not label it HPA; the HPA is an alternative configuration the prose mentions but the default is KPA.
- The object is a **Knative Service**, written in full every time it appears. A bare "Service" would collide with the Kubernetes Service of Ch 9 §2, which the surrounding ⚓ Worth Securing block warns about explicitly.
- The cycle must close — traffic stopping returns to the same idle state it started from. An open-ended left-to-right ramp implies scale-up is permanent.
- Do not add cloud, lambda, or function-symbol iconography. The chapter's argument is that nothing exotic is happening underneath.

**Source ASCII (for designer reference):**
```
   IDLE                REQUEST ARRIVES         SERVING
   ----                ---------------         -------

   Knative Service     Knative Service         Knative Service
   replicas: 0    -->  replicas: 0 -> N   -->  replicas: N
                       (KPA scales up)

   ( nothing            +------------+          +------------+
     running )          |  Pod       |          |  Pod       |
                        | +--------+ |          | +--------+ |
                        | |contain-| |          | |contain-| |
                        | |  er    | |          | |  er    | |
                        | +--------+ |          | +--------+ |
                        +------------+          +------------+
                                                +------------+
                                                |  Pod  ...  |
                                                +------------+

                                                     |
              TRAFFIC STOPS                          |
              -------------                          v
                                                +------------+
   Knative Service        <-- KPA scales down --|  replicas  |
   replicas: 0                                  |   N -> 0   |
                                                +------------+

   The containers and Pods are real at every populated step.
   "Serverless" describes the LIFECYCLE, not their absence.
```

**Proposed filename:** `ch17-fig07-scale-to-zero-and-the-knative-service.png`

```yaml-figure-spec
anchor_id: ch17-fig07-scale-to-zero-and-the-knative-service
diagram_type: flowchart
source_ascii: |2
     IDLE                REQUEST ARRIVES         SERVING
     ----                ---------------         -------
  
     Knative Service     Knative Service         Knative Service
     replicas: 0    -->  replicas: 0 -> N   -->  replicas: N
                         (KPA scales up)
  
     ( nothing            +------------+          +------------+
       running )          |  Pod       |          |  Pod       |
                          | +--------+ |          | +--------+ |
                          | |contain-| |          | |contain-| |
                          | |  er    | |          | |  er    | |
                          | +--------+ |          | +--------+ |
                          +------------+          +------------+
                                                  +------------+
                                                  |  Pod  ...  |
                                                  +------------+
  
                                                       |
                TRAFFIC STOPS                          |
                -------------                          v
                                                  +------------+
     Knative Service        <-- KPA scales down --|  replicas  |
     replicas: 0                                  |   N -> 0   |
                                                  +------------+
  
     The containers and Pods are real at every populated step.
     "Serverless" describes the LIFECYCLE, not their absence.
vendor_terms: [knative, kubernetes]
complexity_hint:
  node_count: 7
  edge_count: 4
  label_count: 11
pedagogy:
  part_18_criteria_met: [temporal_structure, fixed_point]
  learning_outcome: "Explain that serverless workloads on Kubernetes are still containers in Pods, and that the serverless property is the request-driven lifecycle including scale to zero"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the container rectangles nested inside each Pod box"
accessibility:
  alt_text_seed: "A closed cycle: an idle Knative Service at zero replicas with nothing running, a request arriving and the Knative Pod Autoscaler scaling from zero to N with a container visible inside a Pod, a serving state with several such Pods, then traffic stopping and the autoscaler scaling back down to zero replicas"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Knative is a CNCF Graduated project; lifecycle redrawn from published documentation, original diagram, no logos."
```

---

## Figure: ch17-fig04-autoscaler-landscape

**Anchor ID:** `ch17-fig04-autoscaler-landscape`
**Purpose:** Convert four autoscalers from four things to memorize into a small reconstructible grid, by separating "what moves" from "what triggers it" and flagging the one that is not installed.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** comparison matrix (4 rows × 3 columns) with two flagged cells

**Content specification:**
A four-row, three-column matrix with a header row reading **AUTOSCALER | WHAT MOVES | WHAT TRIGGERS IT**. Row 1: **HPA** *(ships with K8s)* | replica count | observed utilization. Row 2: **KEDA** | replica count | external EVENT (queue depth; schedule via Cron). Row 3: **VPA** | per-replica resources (CPU, memory) | observed usage (needs metrics-server). Row 4: **Cluster Autoscaler / Karpenter** | the NODE POOL | unschedulable Pods (provision); underutilized nodes (consolidate). Two cells carry markers and most of the figure's exam value. The VPA row carries a `[!]` flag and the standout annotation **ADD-ON. NOT SHIPPED.** — this should be the loudest thing in the figure. The KEDA row carries a `[*]` flag with an annotation pointing up at the "replica count" cell above it, reading *same axis as HPA* — the two "replica count" cells must be visually aligned and ideally tied together with a bracket or tint so a reader sees the overlap without being told. A two-line footnote closes the figure: *[!] VPA is the one that is NOT there by default.* / *[\*] KEDA shares HPA's axis with a different trigger. Axis and trigger are two separate questions.* Redraw this as a properly typeset table with real rules and cell padding; do not reproduce the ASCII pipes as artwork.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream); header row in a light navy tint
- Size (pixels): 1100x750 landscape
- Font: inherit book default; monospace for autoscaler names (HPA, KEDA, VPA, Karpenter)
- Accent color for highlighted elements: Brass `#B58B3E` on the VPA "ADD-ON. NOT SHIPPED." flag, and a lighter Brass tint linking the two "replica count" cells

**Critical details (non-negotiable accuracy):**
- **VPA does not ship with Kubernetes.** This is the single most examinable fact in the section and the reason the row is flagged. Do not soften it to "optional."
- **HPA does ship.** The `(ships with K8s)` qualifier under HPA must survive.
- HPA and KEDA both move the **replica count**. Four autoscalers, three axes — the overlap is intentional and must be visible, not smoothed away by giving KEDA its own axis name.
- VPA moves **per-replica resources (CPU, memory)**, never replica count. Swapping horizontal and vertical here is the most common error in the material.
- Cluster Autoscaler and Karpenter share **one row** — they do the same job. Splitting them into two rows implies a distinction the source explicitly denies.
- The node-autoscaler trigger has two halves: unschedulable Pods (provision) *and* underutilized nodes (consolidate). Keep both; consolidation is separately tested.
- VPA's dependency on metrics-server must stay in the trigger cell.
- Do not add a CNCF maturity level for Karpenter anywhere on this figure — the ⚓ block beside it warns that no official source assigns it one.

**Source ASCII (for designer reference):**
```
   +-------------------+------------------+---------------------+
   | AUTOSCALER        | WHAT MOVES       | WHAT TRIGGERS IT    |
   +-------------------+------------------+---------------------+
   | HPA               | replica count    | observed            |
   | (ships with K8s)  |                  | utilization         |
   +-------------------+------------------+---------------------+
   | KEDA          [*] | replica count    | external EVENT      |
   |                   |    ^^^ same axis | (queue depth,       |
   |                   |    as HPA        |  schedule via Cron) |
   +-------------------+------------------+---------------------+
   | VPA          [!]  | per-replica      | observed usage      |
   | ** ADD-ON.        |   resources      | (needs metrics-     |
   | NOT SHIPPED. **   |   (CPU, memory)  |  server)            |
   +-------------------+------------------+---------------------+
   | Cluster Auto-     | the NODE POOL    | unschedulable Pods  |
   | scaler            |                  | (provision);        |
   | / Karpenter       |                  | underutilized nodes |
   |                   |                  | (consolidate)       |
   +-------------------+------------------+---------------------+

   [!] VPA is the one that is NOT there by default.
   [*] KEDA shares HPA's axis with a different trigger.
       Axis and trigger are two separate questions.
```

**Proposed filename:** `ch17-fig04-autoscaler-landscape.png`

```yaml-figure-spec
anchor_id: ch17-fig04-autoscaler-landscape
diagram_type: other
source_ascii: |2
     +-------------------+------------------+---------------------+
     | AUTOSCALER        | WHAT MOVES       | WHAT TRIGGERS IT    |
     +-------------------+------------------+---------------------+
     | HPA               | replica count    | observed            |
     | (ships with K8s)  |                  | utilization         |
     +-------------------+------------------+---------------------+
     | KEDA          [*] | replica count    | external EVENT      |
     |                   |    ^^^ same axis | (queue depth,       |
     |                   |    as HPA        |  schedule via Cron) |
     +-------------------+------------------+---------------------+
     | VPA          [!]  | per-replica      | observed usage      |
     | ** ADD-ON.        |   resources      | (needs metrics-     |
     | NOT SHIPPED. **   |   (CPU, memory)  |  server)            |
     +-------------------+------------------+---------------------+
     | Cluster Auto-     | the NODE POOL    | unschedulable Pods  |
     | scaler            |                  | (provision);        |
     | / Karpenter       |                  | underutilized nodes |
     |                   |                  | (consolidate)       |
     +-------------------+------------------+---------------------+
  
     [!] VPA is the one that is NOT there by default.
     [*] KEDA shares HPA's axis with a different trigger.
         Axis and trigger are two separate questions.
vendor_terms: [kubernetes, keda, karpenter, cluster-autoscaler, metrics-server]
complexity_hint:
  node_count: 12
  edge_count: 0
  label_count: 17
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure]
  learning_outcome: "Say which axis each autoscaler moves and what triggers it, and identify which one does not ship with Kubernetes"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the VPA row's ADD-ON, NOT SHIPPED flag"
accessibility:
  alt_text_seed: "A four-row comparison table of autoscalers: HPA moves replica count on observed utilization and ships with Kubernetes; KEDA moves replica count on external events and schedules; VPA moves per-replica CPU and memory on observed usage and is flagged as an add-on that is not shipped; Cluster Autoscaler and Karpenter move the node pool in response to unschedulable Pods and underutilized nodes"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Original comparison matrix built from kubernetes.io documentation prose; no vendor marks, and Karpenter deliberately carries no CNCF maturity claim."
```

---

## Figure: ch17-fig06-cncf-and-k8s-governance

**Anchor ID:** `ch17-fig06-cncf-and-k8s-governance`
**Purpose:** Present the two governance structures side by side so the CNCF/Kubernetes vocabulary collision (TAGs vs SIGs, Board vs Steering) resolves by placement rather than by memorization.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** paired hierarchical org charts with a hard vertical divider

**Content specification:**
Two org charts sharing one frame, separated by an unmistakable vertical divider running the full height. **Left column, headed `==== CNCF ====`** with the subhead *(the foundation — 227+ projects)*: a top box **GOVERNING BOARD** (*marketing, business oversight, budget*), a downward arrow labelled **sets the scope**, then **TOC** (*technical vision; approves projects within that scope*), a downward arrow labelled **aligns**, then **TAGs** (*5 of them, restructured 2025. Bridge projects ↔ TOC*). Detached below and to the side, connected to the TOC by an upward arrow, sits **END USER TAB** (*voice of end users; feeds the TOC*). **Right column, headed `== KUBERNETES ==`** with the subhead *(ONE of those projects)*: a top box **STEERING COMMITTEE** (*overall project governance*), a downward arrow labelled **charters**, then a **COMMITTEES** box marked with an `[X]` and listing *Code of Conduct, Security Response, Steering*, annotated **[X] NOT open membership**. Below it, two unconnected boxes: **SIGs** (*durable, topic-scoped. ~24 of them*) and **WORKING GROUPS** (*time-bounded, cross-SIG*). A closing caption spans the full width: *TAGs are CNCF-wide. SIGs are Kubernetes-internal. Different organizations, different scopes.* The subheads carry the relationship the figure most wants to land — the foundation holds many projects; Kubernetes is one of them — so keep them prominent rather than treating them as fine print.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream); the two columns share the palette rather than being colour-coded, so no reader infers that one side is "the good one"
- Size (pixels): 1200x900 landscape
- Font: inherit book default
- Accent color for highlighted elements: Brass `#B58B3E` on the COMMITTEES box's `[X] NOT open membership` marker only — the section's sharpest exam item

**Critical details (non-negotiable accuracy):**
- The vertical divider must be unambiguous. Any layout that lets a reader trace a line from the CNCF column into the Kubernetes column asserts a reporting relationship that does not exist.
- **The Board sets the scope; the TOC approves projects within it.** The arrow direction and its "sets the scope" label carry this. Reversing it is the most commonly examined inversion in §2.
- **TAGs appear only on the CNCF side. SIGs and Working Groups appear only on the Kubernetes side.** Never both.
- Committees: exactly **three** — Code of Conduct, Security Response, Steering — and Steering is both a committee and the body that charters the other two. Both facts must be readable.
- Committees are the closed-membership body. SIGs and Working Groups are open; do not mark them with the `[X]`.
- SIGs are durable and topic-scoped; Working Groups are time-bounded and cross-SIG. Do not draw Working Groups as children of a single SIG — crossing SIG lines is their defining property.
- Keep "~24" on the SIG count approximate as written; the roster moves.
- No CNCF or Kubernetes logos. Text boxes only.

**Source ASCII (for designer reference):**
```
   ==================== CNCF ====================    ====== KUBERNETES ======
   ( the foundation -- 227+ projects )              ( ONE of those projects )

   +-------------------------+                      +----------------------+
   |    GOVERNING BOARD      |                      | STEERING COMMITTEE   |
   |  marketing, business    |                      |  overall project     |
   |  oversight, budget      |                      |  governance          |
   +-----------+-------------+                      +-----------+----------+
               | sets the scope                                 | charters
               v                                                v
   +-------------------------+                      +----------------------+
   |          TOC            |                      |  COMMITTEES  [X]     |
   |  technical vision;      |                      |  Code of Conduct     |
   |  approves projects      |                      |  Security Response   |
   |  within that scope      |                      |  Steering            |
   +-----------+-------------+                      |  [X] NOT open        |
               | aligns                             |      membership      |
               v                                    +----------------------+
   +-------------------------+
   |         TAGs            |                      +----------------------+
   |  5 of them, restruc-    |                      |  SIGs                |
   |  tured 2025. Bridge     |                      |  durable, topic-     |
   |  projects <-> TOC       |                      |  scoped. ~24 of them |
   +-------------------------+                      +----------------------+
                                                    +----------------------+
   +-------------------------+                      |  WORKING GROUPS      |
   |    END USER TAB         |                      |  time-bounded,       |
   |  voice of end users;    |                      |  cross-SIG           |
   |  feeds the TOC          |                      +----------------------+
   +-------------------------+

   TAGs are CNCF-wide.  SIGs are Kubernetes-internal.
   Different organizations, different scopes.
```

**Proposed filename:** `ch17-fig06-cncf-and-k8s-governance.png`

```yaml-figure-spec
anchor_id: ch17-fig06-cncf-and-k8s-governance
diagram_type: hierarchy_tree
source_ascii: |2
     ==================== CNCF ====================    ====== KUBERNETES ======
     ( the foundation -- 227+ projects )              ( ONE of those projects )
  
     +-------------------------+                      +----------------------+
     |    GOVERNING BOARD      |                      | STEERING COMMITTEE   |
     |  marketing, business    |                      |  overall project     |
     |  oversight, budget      |                      |  governance          |
     +-----------+-------------+                      +-----------+----------+
                 | sets the scope                                 | charters
                 v                                                v
     +-------------------------+                      +----------------------+
     |          TOC            |                      |  COMMITTEES  [X]     |
     |  technical vision;      |                      |  Code of Conduct     |
     |  approves projects      |                      |  Security Response   |
     |  within that scope      |                      |  Steering            |
     +-----------+-------------+                      |  [X] NOT open        |
                 | aligns                             |      membership      |
                 v                                    +----------------------+
     +-------------------------+
     |         TAGs            |                      +----------------------+
     |  5 of them, restruc-    |                      |  SIGs                |
     |  tured 2025. Bridge     |                      |  durable, topic-     |
     |  projects <-> TOC       |                      |  scoped. ~24 of them |
     +-------------------------+                      +----------------------+
                                                      +----------------------+
     +-------------------------+                      |  WORKING GROUPS      |
     |    END USER TAB         |                      |  time-bounded,       |
     |  voice of end users;    |                      |  cross-SIG           |
     |  feeds the TOC          |                      +----------------------+
     +-------------------------+
  
     TAGs are CNCF-wide.  SIGs are Kubernetes-internal.
     Different organizations, different scopes.
vendor_terms: [cncf, kubernetes]
complexity_hint:
  node_count: 8
  edge_count: 4
  label_count: 18
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Name which body does what in CNCF and in Kubernetes, and keep CNCF TAGs distinct from Kubernetes SIGs"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the COMMITTEES box's NOT open membership marker"
accessibility:
  alt_text_seed: "Two org charts side by side separated by a divider. On the CNCF side, the Governing Board sets the scope for the TOC, which aligns the five TAGs, with an End User TAB feeding the TOC. On the Kubernetes side, the Steering Committee charters three committees marked as not having open membership, alongside separate boxes for durable topic-scoped SIGs and time-bounded cross-SIG Working Groups"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Governance structures described in the public CNCF charter and Kubernetes community docs; original chart, no logos or trademarked marks reproduced."
```

---

## Figure: ch17-zenith-one-pluggability-story

> **⚑ ANCHOR ID FLAG:** this ID does not match the required `ch{NN}-fig{MM}-{kebab-slug}` pattern — it carries no `fig{MM}` segment. Suggested conforming ID: `ch17-fig08-one-pluggability-story`. Preserved as written here; renaming is an author decision that must land in the draft and this file together.

**Anchor ID:** `ch17-zenith-one-pluggability-story`
**Purpose:** The chapter's ☀️ Zenith — collapse the four sockets of `ch17-fig02` into the single relation they were always instances of, so the reader sees one decision made four times rather than four facts.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-part concept map (abstract relation on the left, evidence column on the right)

**Content specification:**
The frame is split into two labelled halves by a light rule, headed **THE SHAPE** on the left and **THE EVIDENCE** on the right, each heading underscored. **Left half:** two stacked boxes joined by a single vertical arrow. The upper box reads *Kubernetes defines* / **WHAT MUST BE TRUE**. The lower box reads *Somebody else* / **SUPPLIES THE THING**. The connecting arrow is annotated at its midpoint with the parenthetical *(the socket)*, and the socket glyph used here must be the identical glyph from `ch17-fig02` — the visual rhyme between the two figures is the mechanism by which the Zenith lands. **Right half:** a plain four-line list, monospaced and unboxed, reading `CRI ( Ch 2 §4 )`, `CNI ( Ch 9 §1 )`, `CSI ( Ch 11 §5 )`, `CRDs ( Ch 6 §8 )`. Beneath that list, set as two short pieces of display text with air around them: *Four instances. Not four decisions.* and *One decision, made four times, because it was right four times.* A closing annotation runs along the bottom: *the four sockets of ch17-fig02, collapsed into the single relation they were always instances of.* This figure must feel emptier and quieter than `ch17-fig02` — the altitude gain is carried by how much has been taken away, so resist adding structure, boxes, or ornament to the evidence column.

**Visual style:**
- Palette: inherit book default (Lodestar navy line-art on cream), with more white space than any other figure in the chapter
- Size (pixels): 1000x700 landscape
- Font: inherit book default; monospace (Fira Mono) for the four interface names and chapter references
- Accent color for highlighted elements: Brass `#B58B3E` on the connecting arrow and its *(the socket)* annotation — the relation itself is the Zenith, not either box

**Critical details (non-negotiable accuracy):**
- The socket glyph must be **visually identical** to the one in `ch17-fig02`. If the two figures use different glyphs, the recognition the chapter has been building for fifteen chapters does not fire.
- Chapter references must match `ch17-fig02` exactly: CRI `Ch 2 §4`, CNI `Ch 9 §1`, CSI `Ch 11 §5`, CRDs `Ch 6 §8`. Any disagreement between the two figures is a reader-visible defect.
- The arrow runs from **"Kubernetes defines what must be true"** down to **"somebody else supplies the thing"** — definition first, implementation second. Reversing it inverts the chapter's thesis.
- The four names on the right are **evidence, not structure**. Do not box them, connect them to the left half with arrows, or arrange them as a fifth diagram. Their plainness is the point.
- Keep both display lines. "Four instances. Not four decisions." and "One decision, made four times" are the same claim at two levels, and the chapter's closing argument needs both.
- No implementation or vendor names. This figure is one altitude above products.

**Source ASCII (for designer reference):**
```
              THE SHAPE                    THE EVIDENCE
              ---------                    ------------

     +-------------------------+           CRI    ( Ch 2 §4 )
     |   Kubernetes defines    |           CNI    ( Ch 9 §1 )
     |   WHAT MUST BE TRUE     |           CSI    ( Ch 11 §5 )
     +-----------+-------------+           CRDs   ( Ch 6 §8 )
                 |
            (the socket)                   Four instances.
                 |                         Not four decisions.
     +-----------v-------------+
     |   Somebody else         |           One decision,
     |   SUPPLIES THE THING    |           made four times
     +-------------------------+           because it was
                                           right four times.

     ^ the four sockets of ch17-fig02, collapsed into
       the single relation they were always instances of
```

**Proposed filename:** `ch17-zenith-one-pluggability-story.png`

```yaml-figure-spec
anchor_id: ch17-zenith-one-pluggability-story
diagram_type: concept_map
source_ascii: |2
                THE SHAPE                    THE EVIDENCE
                ---------                    ------------
  
       +-------------------------+           CRI    ( Ch 2 §4 )
       |   Kubernetes defines    |           CNI    ( Ch 9 §1 )
       |   WHAT MUST BE TRUE     |           CSI    ( Ch 11 §5 )
       +-----------+-------------+           CRDs   ( Ch 6 §8 )
                   |
              (the socket)                   Four instances.
                   |                         Not four decisions.
       +-----------v-------------+
       |   Somebody else         |           One decision,
       |   SUPPLIES THE THING    |           made four times
       +-------------------------+           because it was
                                             right four times.
  
       ^ the four sockets of ch17-fig02, collapsed into
         the single relation they were always instances of
vendor_terms: [kubernetes]
complexity_hint:
  node_count: 6
  edge_count: 1
  label_count: 10
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure]
  learning_outcome: "Recognise CRI, CNI, CSI and CRDs as four instances of one architectural decision rather than four separate mechanisms"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the single arrow labelled (the socket) joining the two boxes"
accessibility:
  alt_text_seed: "Two halves: on the left, a box reading Kubernetes defines what must be true connected by one arrow labelled the socket to a box reading somebody else supplies the thing; on the right, a plain list of CRI, CNI, CSI and CRDs with their chapter references, captioned four instances, not four decisions"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Abstract restatement of Kubernetes interface naming; wholly original composition, no upstream figure or vendor IP."
```
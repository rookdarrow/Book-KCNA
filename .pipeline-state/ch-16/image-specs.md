# Image Specifications — KCNA Chapter 16

*Generated from draft-v1.md (draft-voice.md does not exist at this stage; line references are against draft-v1.md). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Figures in this chapter: 6.** All six replace an ASCII diagram; all six are mandatory.

---

## UNANCHORED DIAGRAMS

**None.** Every fenced block in the draft that renders a diagram carries a `<!-- FIGURE: ... -->` anchor on the line immediately preceding it. The remaining fenced blocks in the chapter are command snippets (`kubectl ...`), one shell error transcript, and one YAML fragment (`spec.ports`) — none of these are diagrams and none require anchors.

---

## FLAGS FOR AUTHOR REVIEW

### 1. Anchor ID does not match the required pattern

`<!-- FIGURE: ch16-zenith-mine-or-the-platforms -->` (§8) does not conform to `ch{NN}-fig{MM}-{kebab-slug}` — it carries no `fig{MM}` segment. **Not renamed here** (rule 6: renaming is an author-review decision). The entry below preserves the anchor verbatim as the join key.

Suggested conforming ID: `ch16-fig06-mine-or-the-platforms` — author to confirm before editing the draft, and the change must land in the draft anchor and this file in the same commit or the join key breaks.

### 2. Figure numbers appear out of sequence in the draft

Document order is `fig01` (§1) → `fig05` (§2) → `fig02` (§3) → `fig04` (§4) → `fig03` (§5) → `zenith` (§8). No numbers are missing or duplicated, so the join keys are sound, but any consumer that assumes anchor number == document position will mis-order these. This document lists figures in **draft order**, not numeric order. Author to decide whether to renumber at revision; if so, renumber in draft and here together.

### 3. Accuracy flag inherited from the draft — `ch16-fig03-portforward-vs-service-path`

The draft carries an AUTHOR-REVIEW comment immediately after this figure stating that no cached snapshot documents the full port-forward request path; specifically **the kubelet hop is inferred from general architecture and is not directly sourced**. The figure draws `kubectl ──▶ API server ──▶ kubelet ──▶ Pod:port`. Two resolutions are open: source the kubelet hop against a dated snapshot, or redraw the figure to stop at the API server. **Do not render this figure to final until that resolves** — the middle node of the lower path is the disputed element. The spec below documents both variants.

---

## Figure: ch16-fig01-application-scope-triage

**Anchor ID:** `ch16-fig01-application-scope-triage`
**Purpose:** Shows the reader that Chapter 13's platform-scope diagnosis terminates in a handoff, and that everything downstream of that handoff decomposes into exactly four questions mapped to specific sections.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hierarchical tree (single-root, four-leaf fan-out with an inbound handoff arrow)

**Content specification:**
A vertical tree read top to bottom. At the top, a plain text label — not a box — reading `FROM CH 13 — platform scope discharged`, with a downward arrow into the diagram proper. That arrow terminates in a single wide rectangle, the root of the tree, labelled on two lines: `APPLICATION SCOPE` on the first, `(this book, this chapter, your problem)` on the second. From the bottom edge of that rectangle a single stem descends and then splits into four branches fanning out left to right, each terminating in a downward arrowhead above one leaf. The four leaves are text labels, not boxes, each with a section reference beneath it: `RUNNING?` / `(§2)`, then `HEALTHY? CONFIGURED?` / `(§3)`, then `REACHABLE?` / `(§4 → §5)`, then `PER-REPLICA?` / `(§6)`. The second leaf carries two question words because it is deliberately one question with two halves — set both words on the same leaf, not as two leaves. The visual weight belongs to the `APPLICATION SCOPE` rectangle: it is the only enclosed shape in the figure, and everything above it is inbound from another chapter while everything below it is this chapter's contents. The inbound label at the top should read as arriving from outside the frame — set it lighter, or above a thin rule, so the reader sees a handoff rather than a first step.

**Visual style:**
- Palette: inherit book default (brand navy on cream)
- Size (pixels): 1200x620 landscape
- Font: inherit book default (Roboto Slab display / Fira Sans labels / Fira Mono for `§` refs is optional — plain sans is fine)
- Accent color for highlighted elements: Brass (#B58B3E) on the `APPLICATION SCOPE` rectangle's border and on the inbound arrow from Ch 13

**Critical details (non-negotiable accuracy):**
- Four leaves, not three and not five. The doubling of "is it configured" is expressed by putting two question words on the **second** leaf, not by adding a fifth branch.
- Leaf order left to right is RUNNING → HEALTHY/CONFIGURED → REACHABLE → PER-REPLICA. That order is the elimination order the chapter argues for; reversing or alphabetizing it destroys the point.
- Section references must read exactly `§2`, `§3`, `§4 → §5`, `§6`. The third leaf spans two sections and the arrow between them is part of the label.
- The Ch 13 label is *above* the application-scope box and flows *into* it. It is not a sibling branch and not a leaf.
- `APPLICATION SCOPE` is the only box in the figure.

**Source ASCII (for designer reference):**
```
        FROM CH 13 — platform scope discharged
                        │
                        ▼
        ┌───────────────────────────────────┐
        │   APPLICATION SCOPE  (this book,  │
        │   this chapter, your problem)     │
        └───────────────┬───────────────────┘
                        │
     ┌──────────┬───────┴───────┬─────────────┐
     ▼          ▼               ▼             ▼
  RUNNING?   HEALTHY?       REACHABLE?    PER-REPLICA?
   (§2)     CONFIGURED?     (§4 → §5)        (§6)
              (§3)
```

**Proposed filename:** `ch16-fig01-application-scope-triage.png`

```yaml-figure-spec
anchor_id: ch16-fig01-application-scope-triage
diagram_type: hierarchy_tree
source_ascii: |2
          FROM CH 13 — platform scope discharged
                          │
                          ▼
          ┌───────────────────────────────────┐
          │   APPLICATION SCOPE  (this book,  │
          │   this chapter, your problem)     │
          └───────────────┬───────────────────┘
                          │
       ┌──────────┬───────┴───────┬─────────────┐
       ▼          ▼               ▼             ▼
    RUNNING?   HEALTHY?       REACHABLE?    PER-REPLICA?
     (§2)     CONFIGURED?     (§4 → §5)        (§6)
                (§3)
vendor_terms: []
complexity_hint:
  node_count: 6
  edge_count: 5
  label_count: 6
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Decompose an application-scope fault into four triage questions, asked in the order that eliminates the most ground first"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the APPLICATION SCOPE box — the point where Ch 13's handoff lands and this chapter's method begins"
accessibility:
  alt_text_seed: "A tree diagram. An arrow labelled 'from Chapter 13, platform scope discharged' enters a single box labelled 'Application scope: this book, this chapter, your problem'. Below the box, four branches fan out to four questions: is it running (section 2), is it healthy and configured (section 3), is it reachable (sections 4 then 5), and is it per-replica (section 6)."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Abstract triage tree; no vendor marks, product names, or reproduced diagrams."
```

---

## Figure: ch16-fig05-init-sequence-debug-points

**Anchor ID:** `ch16-fig05-init-sequence-debug-points`
**Purpose:** Maps the `Init:N/M` status string onto a position in the init sequence, so the reader can read a Pod's status and know which container to point `-c` at — and pairs each of the three init failure signatures with its diagnosis.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** horizontal flow diagram with a status gutter and a signature legend

**Content specification:**
Three zones stacked vertically. **Top zone:** a left-to-right chain of four nodes with arrows between them — `init-1` → `init-2` → `init-3` → `app containers`. The first three are visually identical (they are peers); the fourth is set apart — different fill, or a gap in the chain before it — because it is the destination the reader is trying to reach, not another init container. **Middle zone:** directly beneath each of the four nodes, a downward tick into a status label reading `STATUS: Init:0/3`, `STATUS: Init:1/3`, `STATUS: Init:2/3`, and `STATUS: Running` respectively. The vertical alignment is the entire content of this figure — the reader must be able to drop a plumb line from a status string to the container it names. **Bottom zone:** a legend in two parts. First, two command lines set in monospace: `READ WITH: kubectl logs <pod> -c <init-name>` and `ALSO READ: kubectl describe pod <pod>` with the parenthetical `(exit codes, order, state)`. Second, a three-row signature table, each row pairing a symptom with a diagnosis: `STUCK, NO ERROR` → `ordering deadlock — what is it waiting for?`; `FAILS ONLY ON RESTART` → `non-idempotent — it assumed a clean slate`; `EXITS NON-ZERO, LOUDLY` → `config error — read the message, it's telling you`. Render the leader dots of the ASCII as a rule, a column gap, or aligned columns — do not reproduce literal dot leaders.

**Visual style:**
- Palette: inherit book default (brand navy on cream)
- Size (pixels): 1200x700 landscape
- Font: inherit book default; the two command lines and every `Init:N/M` string set in Fira Mono
- Accent color for highlighted elements: Brass (#B58B3E) on the status labels only — the alignment between chain and status is the thing being taught

**Critical details (non-negotiable accuracy):**
- `Init:0/3` sits under **init-1**, `Init:1/3` under **init-2**, `Init:2/3` under **init-3**. The counter names *completed* init containers, so it is always one less than the ordinal of the container currently executing. Getting this off by one inverts the chapter's central teaching and contradicts Practice Question Q3.
- The denominator is `3` in all three init statuses and matches the three init containers drawn. If the designer changes the container count, every denominator changes with it.
- The fourth node's status is `Running` — not `Init:3/3`. Once init completes, the Pod's status string changes vocabulary entirely.
- Init containers run strictly one at a time, in order. Do not draw them in parallel, stacked, or as a pool.
- `-c` in the command line is a flag, not a placeholder. Reproduce the commands character for character.

**Source ASCII (for designer reference):**
```
  init-1 ──────▶ init-2 ──────▶ init-3 ──────▶ app containers
    │              │              │                  │
    ▼              ▼              ▼                  ▼
 STATUS:        STATUS:        STATUS:            STATUS:
 Init:0/3       Init:1/3       Init:2/3           Running

 READ WITH:  kubectl logs <pod> -c <init-name>
 ALSO READ:  kubectl describe pod <pod>   (exit codes, order, state)

 STUCK, NO ERROR ......... ordering deadlock — what is it waiting for?
 FAILS ONLY ON RESTART ... non-idempotent — it assumed a clean slate
 EXITS NON-ZERO, LOUDLY .. config error — read the message, it's telling you
```

**Proposed filename:** `ch16-fig05-init-sequence-debug-points.png`

```yaml-figure-spec
anchor_id: ch16-fig05-init-sequence-debug-points
diagram_type: flowchart
source_ascii: |2
    init-1 ──────▶ init-2 ──────▶ init-3 ──────▶ app containers
      │              │              │                  │
      ▼              ▼              ▼                  ▼
   STATUS:        STATUS:        STATUS:            STATUS:
   Init:0/3       Init:1/3       Init:2/3           Running

   READ WITH:  kubectl logs <pod> -c <init-name>
   ALSO READ:  kubectl describe pod <pod>   (exit codes, order, state)

   STUCK, NO ERROR ......... ordering deadlock — what is it waiting for?
   FAILS ONLY ON RESTART ... non-idempotent — it assumed a clean slate
   EXITS NON-ZERO, LOUDLY .. config error — read the message, it's telling you
vendor_terms: [kubectl, init-container, pod]
complexity_hint:
  node_count: 8
  edge_count: 7
  label_count: 13
pedagogy:
  part_18_criteria_met: [temporal_structure, distinguishing_alternatives]
  learning_outcome: "Read an Init:N/M status string to identify which init container to inspect, and match an init failure's signature to its cause"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the row of Init:N/M status labels and their alignment beneath the containers they name"
accessibility:
  alt_text_seed: "A left-to-right sequence of three init containers followed by the app containers. Beneath each, the Pod status it produces: Init:0/3 under the first init container, Init:1/3 under the second, Init:2/3 under the third, and Running under the app containers. Below, the commands for reading init container logs, and three failure signatures paired with their causes: stuck with no error means an ordering deadlock, failing only on restart means non-idempotency, and exiting non-zero means a configuration error."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes API object names and kubectl command strings only; no CNCF logos, icons, or reproduced documentation figures."
```

---

## Figure: ch16-fig02-ephemeral-container-debug

**Anchor ID:** `ch16-fig02-ephemeral-container-debug`
**Purpose:** Separates `kubectl debug`'s three shapes visually so the reader picks by question rather than by habit — and shows that only one of the three touches the running Pod.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** three-panel comparison (component diagram, stacked panels)

**Content specification:**
Three labelled panels stacked vertically, each showing a different target and each closing with the question it answers. **Panel (A) — `EPHEMERAL CONTAINER — into the running Pod`:** one Pod boundary labelled `Pod (unchanged)` containing two adjacent container boxes, `app: distroless` and `debug: busybox`, with a `+` or seam between them showing the second was added to the first. An annotation arrow points at the debug container reading `added, cannot be removed`. Beneath the panel: `ASKS: "what does the running process see right now?"` **Panel (B) — `--copy-to — a NEW Pod, original untouched`:** two Pod boundaries side by side with clear space between them and no arrow, line, or connector joining them. The left is `Pod (running, untouched)` containing `app: crashing on startup`; the right is `Pod-copy` containing `app: entrypoint replaced`. The separation is the content of this panel — the two Pods must not appear related by anything except adjacency. Beneath: `ASKS: "what would happen if I changed something?"` **Panel (C) — `node/ — the host, not the workload`:** one boundary labelled `Node`, containing `debug Pod, host filesystem mounted`, with an annotation reading `PLATFORM SCOPE`. Beneath: `ASKS: "is the machine itself the problem?" (see Ch 13 §5)`. Panel (C) must be visually demoted relative to A and B — greyed, dashed border, or set behind a rule — because the chapter argues it steps back across the scope boundary this book has spent two chapters drawing.

**Visual style:**
- Palette: inherit book default (brand navy on cream); panel (C) desaturated
- Size (pixels): 1000x1100 portrait
- Font: inherit book default; container labels and `--copy-to` / `node/` in Fira Mono
- Accent color for highlighted elements: Brass (#B58B3E) on panel (B)'s gap — the untouched original beside its copy

**Critical details (non-negotiable accuracy):**
- In (A) the debug container is **inside** the same Pod boundary as the app container. An ephemeral container is not a sidecar Pod and not a separate Pod.
- In (B) the two Pods are **not connected**. No arrow, no dotted line, no "copies to" relationship drawn between them. The original is untouched and the copy is a separate object; any connector implies a live relationship that does not exist.
- In (B) the *original* is the one crashing and the *copy* is the one with the replaced entrypoint. Reversing this inverts the mechanism.
- In (C) the boundary is a **Node**, not a Pod. The debug Pod sits inside the node.
- Panel order is A, B, C. It runs from least invasive to furthest out of scope.
- `--copy-to` and `node/` are literal kubectl syntax including the leading dashes and trailing slash.

**Source ASCII (for designer reference):**
```
  (A) EPHEMERAL CONTAINER — into the running Pod
      ┌─────────── Pod (unchanged) ───────────┐
      │  [app: distroless]  + [debug: busybox]│  ← added, cannot be removed
      └───────────────────────────────────────┘
      ASKS: "what does the running process see right now?"

  (B) --copy-to — a NEW Pod, original untouched
      ┌─── Pod (running, untouched) ───┐   ┌─── Pod-copy ────────┐
      │  [app: crashing on startup]    │   │  [app: entrypoint   │
      │                                │   │        replaced]    │
      └────────────────────────────────┘   └─────────────────────┘
      ASKS: "what would happen if I changed something?"

  (C) node/ — the host, not the workload
      ┌─── Node ───────────────────────────────┐
      │  [debug Pod, host filesystem mounted]  │  ← PLATFORM SCOPE
      └────────────────────────────────────────┘
      ASKS: "is the machine itself the problem?"   (see Ch 13 §5)
```

**Proposed filename:** `ch16-fig02-ephemeral-container-debug.png`

```yaml-figure-spec
anchor_id: ch16-fig02-ephemeral-container-debug
diagram_type: component_diagram
source_ascii: |2
    (A) EPHEMERAL CONTAINER — into the running Pod
        ┌─────────── Pod (unchanged) ───────────┐
        │  [app: distroless]  + [debug: busybox]│  ← added, cannot be removed
        └───────────────────────────────────────┘
        ASKS: "what does the running process see right now?"

    (B) --copy-to — a NEW Pod, original untouched
        ┌─── Pod (running, untouched) ───┐   ┌─── Pod-copy ────────┐
        │  [app: crashing on startup]    │   │  [app: entrypoint   │
        │                                │   │        replaced]    │
        └────────────────────────────────┘   └─────────────────────┘
        ASKS: "what would happen if I changed something?"

    (C) node/ — the host, not the workload
        ┌─── Node ───────────────────────────────┐
        │  [debug Pod, host filesystem mounted]  │  ← PLATFORM SCOPE
        └────────────────────────────────────────┘
        ASKS: "is the machine itself the problem?"   (see Ch 13 §5)
vendor_terms: [kubectl, busybox, pod, node]
complexity_hint:
  node_count: 9
  edge_count: 2
  label_count: 12
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, fixed_point]
  learning_outcome: "Choose among kubectl debug's three shapes by the question each one answers, and recognize that --copy-to leaves the original Pod untouched"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "panel B's gap between the untouched original Pod and its copy"
accessibility:
  alt_text_seed: "Three panels comparing kubectl debug's shapes. Panel A: an ephemeral debug container added inside an unchanged Pod alongside a distroless app container, annotated as unable to be removed; it asks what the running process sees now. Panel B: two unconnected Pods side by side, the original still running and crashing on startup, and a separate copy with its entrypoint replaced; it asks what would happen if something changed. Panel C, shown as platform scope: a debug Pod on a Node with the host filesystem mounted; it asks whether the machine itself is the problem."
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes object names and kubectl flags; busybox named as a generic debug image, no logo or icon reproduced."
```

---

## Figure: ch16-fig04-service-break-points

**Anchor ID:** `ch16-fig04-service-break-points`
**Purpose:** Places the four ways a Service request breaks at their actual positions on the request path, so the reader can tell an empty endpoint list (upstream) from a populated list with a failed request (downstream).
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** annotated data-flow chain with callout boxes and a positional legend

**Content specification:**
A single horizontal request chain across the top, six nodes with arrows between them: `client` → `DNS name` → `Service` → `EndpointSlice` → `Pod` → `container port`. Below the chain, three callout boxes drop from three specific points on it, each connected by a short vertical leader to the node it belongs to. From `DNS name` drops `BREAK 4 — name doesn't resolve to this Service`. From `EndpointSlice` drops `BREAK 1+2 — LIST EMPTY`, itself listing two numbered causes: `1 selector mismatch` and `2 not Ready`. From `container port` drops `BREAK 3 — port ≠ targetPort`, with the parenthetical `(list is POPULATED)` set inside the box. Beneath the callouts, a three-row legend keyed on position rather than number: `UPSTREAM of the list` → `breaks 1 and 2 → EMPTY LIST`; `DOWNSTREAM of the list` → `break 3 → POPULATED LIST, request still fails`; `BESIDE the whole path` → `break 4 → you never reached this Service at all`. The organizing idea is spatial: the reader should be able to see, without reading a word of the legend, that two breaks live at the endpoint list, one lives past it, and one lives off to the side before the Service is ever involved. Render the leader dots as aligned columns or a rule, not literal dots.

**Visual style:**
- Palette: inherit book default (brand navy on cream)
- Size (pixels): 1200x760 landscape
- Font: inherit book default; `port`, `targetPort`, `EndpointSlice` in Fira Mono
- Accent color for highlighted elements: Brass (#B58B3E) on the `BREAK 1+2 / LIST EMPTY` box and its leader — the empty list is the section's Fixed Point

**Critical details (non-negotiable accuracy):**
- Chain order is exactly `client → DNS name → Service → EndpointSlice → Pod → container port`. The EndpointSlice sits between the Service and the Pod; it is not a branch off the Service and not an endpoint of the chain.
- Break 4 attaches to `DNS name`, **not** to `Service`. It is the failure where the client never reached this Service at all.
- Breaks 1 and 2 attach to `EndpointSlice` — the same point, because both produce the same symptom (empty list) and are distinguished by cause, not by position.
- Break 3 attaches to `container port`, downstream of the list, and its box must carry `(list is POPULATED)`. That contrast is the section's whole diagnostic value.
- `port ≠ targetPort` — keep the inequality symbol and both field names spelled exactly. Reversing which one the container listens on contradicts §4 and Practice Question Q11.
- Three callout boxes, not four: breaks 1 and 2 share one box.

**Source ASCII (for designer reference):**
```
  client ──▶ DNS name ──▶ Service ──▶ EndpointSlice ──▶ Pod ──▶ container port
               │                          │                        │
               │                          │                        │
          ┌────┴────┐              ┌──────┴──────┐          ┌──────┴──────┐
          │ BREAK 4 │              │  BREAK 1+2  │          │   BREAK 3   │
          │ name    │              │  LIST EMPTY │          │ port ≠      │
          │ doesn't │              │  1 selector │          │ targetPort  │
          │ resolve │              │    mismatch │          │             │
          │ to this │              │  2 not Ready│          │ (list is    │
          │ Service │              │             │          │  POPULATED) │
          └─────────┘              └─────────────┘          └─────────────┘

  UPSTREAM of the list ....... breaks 1 and 2 → EMPTY LIST
  DOWNSTREAM of the list ..... break 3 → POPULATED LIST, request still fails
  BESIDE the whole path ...... break 4 → you never reached this Service at all
```

**Proposed filename:** `ch16-fig04-service-break-points.png`

```yaml-figure-spec
anchor_id: ch16-fig04-service-break-points
diagram_type: data_flow
source_ascii: |2
    client ──▶ DNS name ──▶ Service ──▶ EndpointSlice ──▶ Pod ──▶ container port
                 │                          │                        │
                 │                          │                        │
            ┌────┴────┐              ┌──────┴──────┐          ┌──────┴──────┐
            │ BREAK 4 │              │  BREAK 1+2  │          │   BREAK 3   │
            │ name    │              │  LIST EMPTY │          │ port ≠      │
            │ doesn't │              │  1 selector │          │ targetPort  │
            │ resolve │              │    mismatch │          │             │
            │ to this │              │  2 not Ready│          │ (list is    │
            │ Service │              │             │          │  POPULATED) │
            └─────────┘              └─────────────┘          └─────────────┘

    UPSTREAM of the list ....... breaks 1 and 2 → EMPTY LIST
    DOWNSTREAM of the list ..... break 3 → POPULATED LIST, request still fails
    BESIDE the whole path ...... break 4 → you never reached this Service at all
vendor_terms: [service, endpointslice, pod, dns]
complexity_hint:
  node_count: 9
  edge_count: 8
  label_count: 12
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Locate a Service failure at its position on the request path, and distinguish an empty endpoint list from a populated list with a failing request"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the BREAK 1+2 / LIST EMPTY callout at the EndpointSlice — a Service with no endpoints is working exactly as written"
accessibility:
  alt_text_seed: "A request path runs left to right from client, to DNS name, to Service, to EndpointSlice, to Pod, to container port. Three callouts drop from it. From the DNS name: break four, the name does not resolve to this Service. From the EndpointSlice: breaks one and two, the list is empty, caused either by a selector mismatch or by Pods not being Ready. From the container port: break three, port does not equal targetPort, and here the list is populated. A legend notes that upstream breaks empty the list, the downstream break leaves it populated while the request still fails, and break four means this Service was never reached."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes API object names only; no CNCF icons or reproduced documentation figures."
```

---

## Figure: ch16-fig03-portforward-vs-service-path

**Anchor ID:** `ch16-fig03-portforward-vs-service-path`
**Purpose:** Shows that the port-forward path and the Service path share no step except the Pod itself, which is what makes a working port-forward beside a failing Service call an elimination step rather than a clean bill of health.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-path comparison (parallel data flows, stacked)

> **⚠ RENDER BLOCKED PENDING AUTHOR REVIEW — see Flag 3 above.** The lower path's middle node (`kubelet`) is not directly sourced in any cached snapshot. Do not produce final art until the author either sources the kubelet hop or elects the shortened variant described under Critical details.

**Content specification:**
Two horizontal paths stacked with a clear band of white space between them — the separation carries the argument, so do not let the two chains share a lane, a gridline, or any node position. **Upper path, headed `THE SERVICE PATH (what your users travel)`:** `client` → `DNS` → `Service (ClusterIP)` → `service proxy` → `Pod:targetPort`. Two annotations drop beneath it: under `Service (ClusterIP)`, the words `selector, endpoints`; under `service proxy`, the words `kube-proxy rules`. A bracketed note runs beneath both: `[ §4 breaks 1-4 all live on this path ]`. **Lower path, headed `THE PORT-FORWARD PATH (what you travel)`:** `kubectl` → `API server` → `kubelet` → `Pod:port`, with one annotation dropping beneath `API server` reading `pods/portforward subresource`, and a bracketed note beneath: `[ shares NO step with the path above except the Pod itself ]`. The two paths terminate at nodes that both name the same Pod but by different ports — that convergence at the right edge is the only thing the two paths have in common, and the design should make the reader see it. Consider drawing the two terminal Pod nodes vertically aligned so the shared destination is unmistakable while every step leading to it differs.

**Visual style:**
- Palette: inherit book default (brand navy on cream)
- Size (pixels): 1200x640 landscape
- Font: inherit book default; `Pod:targetPort`, `Pod:port`, `kubectl`, `kube-proxy`, `pods/portforward` in Fira Mono
- Accent color for highlighted elements: Brass (#B58B3E) on the two terminal Pod nodes — the single shared step

**Critical details (non-negotiable accuracy):**
- The two paths must share **no** intermediate node. If the designer merges, aligns, or connects any middle step, the figure asserts the opposite of the section's Fixed Point.
- The Service path terminates at `Pod:targetPort`; the port-forward path terminates at `Pod:port`. Different port labels on the same Pod are deliberate — §5's Worth Securing turns on exactly this distinction.
- `pods/portforward` is an API subresource path. Reproduce it with the slash and no spaces.
- The port-forward path does **not** pass through the Service, the ClusterIP, or the service proxy. That omission is the figure's argument.
- **Open on the kubelet node:** the draft's AUTHOR-REVIEW comment states this hop is inferred, not sourced. Two acceptable outputs — (a) keep `kubectl → API server → kubelet → Pod:port` once a dated snapshot supports the kubelet hop, or (b) render the shortened variant `kubectl → API server → Pod:port` and drop the kubelet node entirely. Either satisfies the figure's purpose; the shortened variant is the safe default if the sourcing question does not resolve before render. Do not ship variant (a) unsourced.

**Source ASCII (for designer reference):**
```
  THE SERVICE PATH (what your users travel)
  client ──▶ DNS ──▶ Service (ClusterIP) ──▶ service proxy ──▶ Pod:targetPort
                          │                        │
                     selector, endpoints      kube-proxy rules
                     [ §4 breaks 1-4 all live on this path ]

  THE PORT-FORWARD PATH (what you travel)
  kubectl ──▶ API server ──▶ kubelet ──▶ Pod:port
                    │
            pods/portforward subresource
            [ shares NO step with the path above except the Pod itself ]
```

**Proposed filename:** `ch16-fig03-portforward-vs-service-path.png`

```yaml-figure-spec
anchor_id: ch16-fig03-portforward-vs-service-path
diagram_type: data_flow
source_ascii: |2
    THE SERVICE PATH (what your users travel)
    client ──▶ DNS ──▶ Service (ClusterIP) ──▶ service proxy ──▶ Pod:targetPort
                            │                        │
                       selector, endpoints      kube-proxy rules
                       [ §4 breaks 1-4 all live on this path ]

    THE PORT-FORWARD PATH (what you travel)
    kubectl ──▶ API server ──▶ kubelet ──▶ Pod:port
                      │
              pods/portforward subresource
              [ shares NO step with the path above except the Pod itself ]
vendor_terms: [kubectl, kube-apiserver, kubelet, kube-proxy, service, pod]
complexity_hint:
  node_count: 9
  edge_count: 7
  label_count: 14
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Explain why a working port-forward beside a failing Service call localizes the fault to the Service path rather than clearing the application"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the two terminal Pod nodes — the only step the two paths share"
accessibility:
  alt_text_seed: "Two separate request paths. The Service path, travelled by users, runs from client to DNS to the Service's ClusterIP to the service proxy to the Pod's targetPort, annotated with selector and endpoints at the Service and kube-proxy rules at the proxy; all four of section four's break points live on this path. The port-forward path, travelled by the engineer, runs from kubectl to the API server via the pods/portforward subresource and on to the Pod's port. The two paths share no step except the Pod itself."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes component and subresource names only; no CNCF icons. Technical accuracy of the kubelet node is flagged for author review before render."
```

---

## Figure: ch16-zenith-mine-or-the-platforms

**Anchor ID:** `ch16-zenith-mine-or-the-platforms`
**Purpose:** The chapter's synthesis moment — shows that Chapters 13 and 16 are two halves of one narrowing method meeting at an ownership boundary, and that the boundary *is* the method rather than a subject divider.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** mirrored concept map with a central axis

> **Anchor ID does not conform to `ch{NN}-fig{MM}-{slug}` — see Flag 1 above. Preserved verbatim as the join key; renaming is an author-review decision.**

**Content specification:**
A symmetrical two-column composition with a single strong vertical line down the centre. That line is the subject of the figure and should be the heaviest element on the page. **Left column, headed `PLATFORM SCOPE` with `(Ch 13)` beneath:** a sequence reading `phase ──▶ conditions ──▶ events ──▶ logs ──▶ node`, wrapping to a second line as the ASCII does or set as one flowing chain. **Right column, headed `APPLICATION SCOPE` with `(Ch 16)` beneath:** a sequence reading `running? ──▶ healthy? ──▶ reachable? ──▶ configured? ──▶ which replica?`, likewise wrapping or flowing. Below both columns, two long horizontal arrows point **inward toward the central line** — the left arrow travelling rightward, the right arrow travelling leftward — each labelled `narrowing`. Beneath the point where they meet, two lines of centred text: `THE BOUNDARY` and, smaller, `( this line is the method )`. The two halves must be visually equal in weight; neither scope is subordinate. The reader's eye should be drawn to the centre by the convergence of the two narrowing arrows, arriving at the line itself as the answer.

**Visual style:**
- Palette: inherit book default (brand navy on cream). This is a ☀️ Zenith figure — give it more white space and a lighter hand than the working diagrams in this chapter; it is a moment of synthesis, not a reference chart.
- Size (pixels): 1200x780 landscape
- Font: inherit book default. `( this line is the method )` set in italic; the two chains may be set lighter than the headers.
- Accent color for highlighted elements: Brass (#B58B3E) on the central vertical line and the two inward `narrowing` arrows

**Critical details (non-negotiable accuracy):**
- The central line runs the full height of the figure and is the heaviest stroke on the page. Everything else defers to it.
- Left is platform scope / Ch 13; right is application scope / Ch 16. This orientation matches `ch16-fig01`, where Ch 13 hands off *into* this chapter, and matches the chapter title's own order — "Your Application, Their Cluster" notwithstanding, the reading order here is chronological by chapter.
- Both narrowing arrows point **inward**, toward the boundary. They do not point at each other's columns, and neither crosses the line.
- The two columns are equal in visual weight. Do not make the application side dominant because this is the application chapter.
- Left chain order: phase, conditions, events, logs, node. Right chain order: running, healthy, reachable, configured, which replica. Both are the diagnostic orders their chapters teach.
- Question marks belong on the right-hand terms and not on the left-hand ones — the asymmetry is in the source and is meaningful.

**Source ASCII (for designer reference):**
```
   PLATFORM SCOPE                    │                 APPLICATION SCOPE
   (Ch 13)                           │                 (Ch 16)
                                     │
   phase ──▶ conditions ──▶ events   │   running? ──▶ healthy? ──▶ reachable?
        ──▶ logs ──▶ node            │        ──▶ configured? ──▶ which replica?
                                     │
              ─────────────────────▶ │ ◀─────────────────────
                   narrowing         │        narrowing
                                     │
                            THE BOUNDARY
                    ( this line is the method )
```

**Proposed filename:** `ch16-zenith-mine-or-the-platforms.png`

```yaml-figure-spec
anchor_id: ch16-zenith-mine-or-the-platforms
diagram_type: concept_map
source_ascii: |2
     PLATFORM SCOPE                    │                 APPLICATION SCOPE
     (Ch 13)                           │                 (Ch 16)
                                       │
     phase ──▶ conditions ──▶ events   │   running? ──▶ healthy? ──▶ reachable?
          ──▶ logs ──▶ node            │        ──▶ configured? ──▶ which replica?
                                       │
                ─────────────────────▶ │ ◀─────────────────────
                     narrowing         │        narrowing
                                       │
                              THE BOUNDARY
                      ( this line is the method )
vendor_terms: []
complexity_hint:
  node_count: 10
  edge_count: 10
  label_count: 16
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure]
  learning_outcome: "Recognize platform-scope and application-scope diagnosis as one narrowing method meeting at an ownership boundary, rather than two separate subjects"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the central vertical boundary line, with both narrowing arrows converging on it"
accessibility:
  alt_text_seed: "A symmetrical diagram divided by a heavy vertical line. On the left, platform scope from Chapter 13: phase, then conditions, then events, then logs, then node. On the right, application scope from Chapter 16: is it running, is it healthy, is it reachable, is it configured, and which replica. Below each column, a long arrow points inward toward the centre line, each labelled narrowing. At the centre, the caption reads: the boundary, this line is the method."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Abstract method map; generic diagnostic vocabulary only, no vendor marks or product names."
```
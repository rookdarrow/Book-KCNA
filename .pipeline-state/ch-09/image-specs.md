# Image Specifications — KCNA Chapter 9

*Generated from `draft-v1.md` (Stage 10 note: `draft-voice.md` does not yet exist; this extraction was run against the current draft). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Chapter:** 9 — *Every Pod Has an Address*
**Book:** KCNA · **Role family:** The Communications Officer · **Era register:** early interstellar
**Figure count:** 6 anchored, 0 unanchored diagrams, 1 anchor-ID format violation

---

## ANCHOR ID FORMAT VIOLATIONS

Rule 4 requires anchor IDs of the exact form `ch{NN}-fig{MM}-{kebab-slug}`. One anchor in this draft does not conform:

| Anchor as written in draft | Problem | Suggested conforming ID |
|---|---|---|
| `ch09-zenith-stable-name-over-churn` | Missing the `fig{MM}` segment. Sorts unpredictably in the book-level index and will not match the aggregator's figure-numbering regex. | `ch09-fig06-zenith-stable-name-over-churn` |

**Not renamed here.** Per rule 6 the anchor ID is the join key and renaming is an author-review decision. The entry below preserves `ch09-zenith-stable-name-over-churn` verbatim in both the prose header and the `yaml-figure-spec` block. If the author accepts the rename, it must be changed in **three** places in the same commit: the draft's anchor comment, this file's `Anchor ID` line, and this file's `anchor_id` field — plus the proposed filename.

Note also that this figure carries a **☀️ Zenith** marker in the prose, and the slug is doing double duty as a marker tag. If the pipeline wants marker-tagged figures as a category, that is a `pedagogy.part_18_criteria_met: [zenith]` concern, not a slug concern — the slug should still carry `fig06`.

---

## UNANCHORED DIAGRAMS

**None.** All six ASCII figures in the draft carry a preceding `<!-- FIGURE: ... -->` anchor comment.

One additional fenced block exists without an anchor, assessed and deliberately **excluded** rather than flagged:

- **§4 — "Looking at the list"**, a single-line shell command:
  ```
  kubectl get endpointslices -l kubernetes.io/service-name=<service-name>
  ```
  This is a command, not an ASCII diagram. It requires no figure and no anchor. Flagging here for the record so the structural audit's inevitable second sighting of it resolves against a documented decision rather than being re-litigated.

Line numbers are cited by section rather than by line index in this file. The pipeline note directs line citations against `draft-v1.md`, but the draft was received as a stage payload rather than read from disk, so absolute line offsets could not be verified. Section anchors are stable and unambiguous here.

---

## Figure: ch09-fig01-network-model-four-rules

**Anchor ID:** `ch09-fig01-network-model-four-rules`
**Purpose:** Make the four rules of the Kubernetes network model visible as one spatial claim — that every Pod is directly reachable from every other Pod, across node boundaries, with nothing in between.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Network topology — two peer node containers, side by side, with Pod children and direct connection lines

**Content specification:**

Draw two large rounded rectangles side by side, equal size, captioned above (not inside) as `node: worker-3` on the left and `node: worker-11` on the right. Inside the left node, place three child boxes: a Pod labelled `Pod 10.244.1.7` at top, a Pod labelled `Pod 10.244.1.8` in the middle, and a smaller box labelled `kubelet` at bottom. Inside the right node, place two child boxes: `Pod 10.244.4.2` at top and `Pod 10.244.4.3` below it.

The top-left Pod (`10.244.1.7`) is the only Pod drawn with internal structure: it contains two small side-by-side container boxes labelled `ctr a` and `ctr b`, joined by a short bidirectional arrow whose edge label is `localhost`. That inner arrow must be visually *inside* the Pod's boundary — it is the only connection in the diagram that does not cross a Pod wall, and the whole point of drawing it is that it is different in kind from every other line.

Three connection lines then run between Pods. One connects `10.244.1.7` to `10.244.1.8` (same node). One connects `10.244.1.7` to `10.244.4.2` and must visibly cross both node boundaries (different nodes). One connects `kubelet` to `10.244.1.8` (node agent to local Pod). Every one of these lines is drawn as a plain direct edge — no intermediate box, no gateway node, no router glyph, no label on the line other than what is specified. The absence of any intermediate element is the figure's argument.

Below the two nodes, set the caption line: *Every line above is a direct connection. Nothing sits between the Pods.*

The cross-node edge (`10.244.1.7` ↔ `10.244.4.2`) is "the point" and takes the accent treatment.

**Visual style:**
- Palette: inherit book default (Lodestar Ledgers palette, `illustration-standards.md`)
- Size (pixels): 1200x700 landscape
- Font: inherit book default (Fira Sans for labels, Fira Mono for IP addresses and `localhost`)
- Accent color for highlighted elements: Brass `#B58B3E` on the cross-node Pod-to-Pod edge; all other edges in the default line weight/color

**Critical details (non-negotiable accuracy):**
- The IP address label belongs to the **Pod** box, never to a container box. `ctr a` and `ctr b` carry **no** address of their own. This figure exists partly to defuse the "each container gets an IP" trap and would actively teach the trap if a container were labelled with an address.
- All addresses are Pod-network addresses in the `10.244.x.x` range. Do not substitute node IPs, cluster IPs, or `10.96.x.x` values — `10.96.0.42` is the cluster-IP example used in fig04 and must not appear here.
- Nothing is drawn between any two Pods. No switch, router, gateway, NAT box, proxy, bridge, or tunnel glyph anywhere in the figure, including on the cross-node edge. Overlay encapsulation is a real implementation detail, but it is explicitly *not* what this figure depicts, and adding it inverts the lesson.
- The `localhost` edge is inside the Pod boundary and connects two containers. It must not be confused with, or drawn in the same style as, the Pod-to-Pod edges.
- The `kubelet` box is inside the `worker-3` node boundary and connects only to a Pod on *that* node. Do not draw kubelet reaching across to `worker-11`.
- Node addresses are not shown and must not be invented. The draft gives node *names* only.
- Both nodes are peers — same size, same weight, no control-plane styling. Neither is a master, and no control-plane component appears in this figure.

**Source ASCII (for designer reference):**
```
        node: worker-3                         node: worker-11
   ┌──────────────────────────┐          ┌──────────────────────────┐
   │                          │          │                          │
   │  ┌────────────────────┐  │          │  ┌────────────────────┐  │
   │  │ Pod  10.244.1.7    │  │          │  │ Pod  10.244.4.2    │  │
   │  │ ┌──────┐  ┌──────┐ │  │          │  │                    │  │
   │  │ │ ctr  │↔ │ ctr  │ │  │          │  │                    │  │
   │  │ │  a   │lo│  b   │ │  │          │  │                    │  │
   │  │ └──────┘  └──────┘ │  │          │  │                    │  │
   │  └─────────┬──────────┘  │          │  └─────────┬──────────┘  │
   │            │             │          │            │             │
   │            ├─────────────┼──────────┼────────────┘             │
   │            │             │          │                          │
   │  ┌─────────┴──────────┐  │          │  ┌────────────────────┐  │
   │  │ Pod  10.244.1.8    │  │          │  │ Pod  10.244.4.3    │  │
   │  └────────────────────┘  │          │  └────────────────────┘  │
   │       ▲                  │          │                          │
   │  ┌────┴────┐             │          │                          │
   │  │ kubelet │             │          │                          │
   │  └─────────┘             │          │                          │
   └──────────────────────────┘          └──────────────────────────┘

   Every line above is a direct connection. Nothing sits between the Pods.
```

**Proposed filename:** `ch09-fig01-network-model-four-rules.png`

```yaml-figure-spec
anchor_id: ch09-fig01-network-model-four-rules
diagram_type: k8s_architecture
source_ascii: |2
          node: worker-3                         node: worker-11
     ┌──────────────────────────┐          ┌──────────────────────────┐
     │                          │          │                          │
     │  ┌────────────────────┐  │          │  ┌────────────────────┐  │
     │  │ Pod  10.244.1.7    │  │          │  │ Pod  10.244.4.2    │  │
     │  │ ┌──────┐  ┌──────┐ │  │          │  │                    │  │
     │  │ │ ctr  │↔ │ ctr  │ │  │          │  │                    │  │
     │  │ │  a   │lo│  b   │ │  │          │  │                    │  │
     │  │ └──────┘  └──────┘ │  │          │  │                    │  │
     │  └─────────┬──────────┘  │          │  └─────────┬──────────┘  │
     │            │             │          │            │             │
     │            ├─────────────┼──────────┼────────────┘             │
     │            │             │          │                          │
     │  ┌─────────┴──────────┐  │          │  ┌────────────────────┐  │
     │  │ Pod  10.244.1.8    │  │          │  │ Pod  10.244.4.3    │  │
     │  └────────────────────┘  │          │  └────────────────────┘  │
     │       ▲                  │          │                          │
     │  ┌────┴────┐             │          │                          │
     │  │ kubelet │             │          │                          │
     │  └─────────┘             │          │                          │
     └──────────────────────────┘          └──────────────────────────┘

     Every line above is a direct connection. Nothing sits between the Pods.
vendor_terms: [kubernetes, pod, node, kubelet]
complexity_hint:
  node_count: 9
  edge_count: 4
  label_count: 11
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "State that every Pod has a unique cluster-wide IP and that all Pods reach all Pods directly, on the same node or across nodes, without NAT or proxies"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the cross-node edge joining Pod 10.244.1.7 to Pod 10.244.4.2, which crosses both node boundaries with nothing in between"
accessibility:
  alt_text_seed: "Two worker nodes side by side, each containing Pods labelled with 10.244.x.x addresses. One Pod contains two containers joined over localhost. Direct lines connect a Pod to another Pod on the same node, to a Pod on the other node, and to the local kubelet, with no intermediate device on any line."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes component names only; all shapes redrawn in the locked Lodestar line-art style rather than using the CNCF icon set."
```

---

## Figure: ch09-fig02-service-types-ladder

**Anchor ID:** `ch09-fig02-service-types-ladder`
**Purpose:** Show that ClusterIP, NodePort and LoadBalancer are additive layers of one mechanism, and that ExternalName is categorically not on that ladder.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Nested containment diagram (three concentric labelled frames) plus a detached, rule-separated panel below

**Content specification:**

The upper two-thirds of the figure is a set of three concentric rectangles, each labelled on its top edge and each containing a short reachability caption.

Outermost frame: header `LoadBalancer`, body text on three lines — `reachable from: the internet`, `(external LB supplied by your cloud provider,`, `NOT by Kubernetes)`. Middle frame: header `NodePort`, body text on two lines — `reachable from: anything that can reach a node`, `<node-ip>:<static-port>, on every node`. Innermost frame: header `ClusterIP`, body text on two lines — `reachable from: inside the cluster only`, `(the default type)`.

Nesting must be unmistakable containment, not adjacency: each inner frame is fully enclosed by its parent with visible margin on all four sides. Below the outermost frame, set the caption on two lines: *Each ring ADDS to the ones inside it. Asking for an outer ring does not remove the inner ones.*

Then a hard break. Draw a full-width double horizontal rule, a band of text reading `NOT ON THE LADDER. NOT A FOURTH RING. SEPARATE MECHANISM.`, and a second full-width double rule beneath it. This separator band is the single most important element in the figure and should be the heaviest visual object on the page.

Below the separator, in a deliberately different visual idiom from the nested frames — no enclosing box, left-aligned, plain — set the label `ExternalName`, then a single horizontal relation reading `my-svc ──── CNAME ────► api.foo.bar.example`, then the qualifier line `no cluster IP · no endpoints · no proxying of any kind`.

The ExternalName block must not be enclosed in anything, must not touch the concentric frames, and must not be positioned in a way that reads as a fourth ring, a sibling ring, or a continuation of the stack. Whitespace between the separator band and both neighbours should be generous.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1100x900 landscape
- Font: inherit book default (Fira Mono for `<node-ip>:<static-port>`, `my-svc`, `api.foo.bar.example`, and `CNAME`)
- Accent color for highlighted elements: Brass `#B58B3E` on the double-rule separator band and its text. The three concentric frames use graduated default-palette weights, lightest innermost, so the nesting reads in grayscale by line weight as well as by color.

**Critical details (non-negotiable accuracy):**
- Nesting order, innermost to outermost: **ClusterIP → NodePort → LoadBalancer**. Reversing this teaches the exact misconception the figure defuses.
- ClusterIP carries the `(the default type)` note. Neither of the other two rings may be labelled as default.
- The LoadBalancer frame's parenthetical must retain the word **NOT** in `NOT by Kubernetes`. This is the figure's second defusal and the draft sets it in caps; keep the emphasis.
- **Do not add port fields.** No `port`, `targetPort`, or `nodePort` labels; no port-number examples; no default NodePort range (`30000-32767` or otherwise). An `AUTHOR-REVIEW` comment in §3 records that these facts are uncached and deliberately unstated in the prose. Adding them to the figure would introduce an unsourced claim through the back door and would make the figure contradict its own chapter.
- ExternalName has **no** cluster IP, **no** endpoints, and **no** proxying. Do not draw an address for it, a Pod behind it, an arrow into the cluster, or any glyph implying traffic passes through Kubernetes.
- The relation from `my-svc` to `api.foo.bar.example` is a **CNAME** — a name-to-name mapping. Do not render it as a traffic arrow, a request, or a connection; it is a DNS answer.
- Nothing in the figure may suggest four rings, four tiers, or an ordered progression of four. Three plus one, with a wall between.

**Source ASCII (for designer reference):**
```
   ┌─ LoadBalancer ─────────────────────────────────────────┐
   │  reachable from: the internet                          │
   │  (external LB supplied by your cloud provider,         │
   │   NOT by Kubernetes)                                   │
   │                                                        │
   │  ┌─ NodePort ───────────────────────────────────────┐  │
   │  │  reachable from: anything that can reach a node   │ │
   │  │  <node-ip>:<static-port>, on every node           │ │
   │  │                                                   │ │
   │  │  ┌─ ClusterIP ─────────────────────────────────┐  │ │
   │  │  │  reachable from: inside the cluster only    │  │ │
   │  │  │  (the default type)                         │  │ │
   │  │  └─────────────────────────────────────────────┘  │ │
   │  └───────────────────────────────────────────────────┘ │
   └────────────────────────────────────────────────────────┘

   Each ring ADDS to the ones inside it. Asking for an outer ring
   does not remove the inner ones.


   ════════════════════════════════════════════════════════════
   NOT ON THE LADDER. NOT A FOURTH RING. SEPARATE MECHANISM.
   ════════════════════════════════════════════════════════════

        ExternalName
        my-svc ──── CNAME ────► api.foo.bar.example
        no cluster IP · no endpoints · no proxying of any kind
```

**Proposed filename:** `ch09-fig02-service-types-ladder.png`

```yaml-figure-spec
anchor_id: ch09-fig02-service-types-ladder
diagram_type: hierarchy_tree
source_ascii: |2
     ┌─ LoadBalancer ─────────────────────────────────────────┐
     │  reachable from: the internet                          │
     │  (external LB supplied by your cloud provider,         │
     │   NOT by Kubernetes)                                   │
     │                                                        │
     │  ┌─ NodePort ───────────────────────────────────────┐  │
     │  │  reachable from: anything that can reach a node   │ │
     │  │  <node-ip>:<static-port>, on every node           │ │
     │  │                                                   │ │
     │  │  ┌─ ClusterIP ─────────────────────────────────┐  │ │
     │  │  │  reachable from: inside the cluster only    │  │ │
     │  │  │  (the default type)                         │  │ │
     │  │  └─────────────────────────────────────────────┘  │ │
     │  └───────────────────────────────────────────────────┘ │
     └────────────────────────────────────────────────────────┘

     Each ring ADDS to the ones inside it. Asking for an outer ring
     does not remove the inner ones.


     ════════════════════════════════════════════════════════════
     NOT ON THE LADDER. NOT A FOURTH RING. SEPARATE MECHANISM.
     ════════════════════════════════════════════════════════════

          ExternalName
          my-svc ──── CNAME ────► api.foo.bar.example
          no cluster IP · no endpoints · no proxying of any kind
vendor_terms: []
complexity_hint:
  node_count: 6
  edge_count: 1
  label_count: 14
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Choose among ClusterIP, NodePort, LoadBalancer and ExternalName, and identify which three are additive layers of one mechanism and which one is a separate mechanism entirely"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the double-ruled separator band reading NOT ON THE LADDER, which divides the three additive rings from ExternalName"
accessibility:
  alt_text_seed: "Three concentric labelled frames: ClusterIP innermost reachable inside the cluster only and the default type, NodePort around it reachable from any node address and port, LoadBalancer outermost reachable from the internet via a provider-supplied load balancer. Below a heavy double-ruled separator marked not on the ladder, ExternalName is shown separately as a CNAME from my-svc to api.foo.bar.example with no cluster IP, no endpoints and no proxying."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Depicts Kubernetes Service API type names as text only; no vendor marks, logos or icons reproduced."
```

---

## Figure: ch09-fig03-service-endpointslice-selector-path

**Anchor ID:** `ch09-fig03-service-endpointslice-selector-path`
**Purpose:** Trace the full path from a Service's selector to the addresses traffic actually reaches, and make readiness visible as a gate between matching and membership.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Left-to-right data-flow diagram with a filtering gate, three columns plus a controller callout

**Content specification:**

Three columns, left to right. **Column one, upper left:** a box headed `Service: database` containing two lines of monospace, `selector:` and indented `app: db`. A downward arrow leaves this box, labelled `query`, and points into column one's lower element: a stacked list of four Pod entries, drawn as one bordered column divided by internal rules. The four entries, top to bottom, are `Pod app: db / 10.244.1.7`, `Pod app: db / 10.244.4.2`, `Pod app: db / 10.244.4.9`, and `Pod app: cache / 10.244.1.9`.

**Column two, centre:** a tall gate element headed `Ready?`, drawn as a physical gate — the ASCII uses a double-ruled block to suggest a barrier and labels the body `GATE`.

**Arrows from the Pod list into the gate.** The first three Pods each get a horizontal arrow labelled `matches`, with a secondary label beneath: `✓ Ready` for `10.244.1.7`, `✓ Ready` for `10.244.4.2`, and `✗ NOT Ready` for `10.244.4.9`. The first two arrows pass *through* the gate and continue into column three. The third arrow **stops at the gate face** and is annotated `✗ STOPPED at gate`.

The fourth Pod, `app: cache / 10.244.1.9`, gets **no arrow at all**. It carries an inline annotation to its right: `✗ never matched the selector` and, on a second line, `(different failure — different file)`. The visual difference between "stopped at the gate" and "never entered the diagram's flow" is the figure's second lesson and must survive rendering — a stopped arrow and an absent arrow are not the same failure.

**Column three, upper right:** a box headed `EndpointSlice` containing exactly two monospace lines, `10.244.1.7:5432` and `10.244.4.2:5432`. The two surviving arrows terminate here.

**Below and centred:** a callout box reading `EndpointSlice controller` with a second line `(in kube-controller-manager)`, and a leader line pointing at it annotated `watches Services + Pods, writes the slice`. This box has no traffic arrows in or out — it is an actor annotation, not a stage in the flow.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x800 landscape
- Font: inherit book default (Fira Mono for addresses, ports, label keys/values and `app: db`)
- Accent color for highlighted elements: Brass `#B58B3E` on the gate element and on the `✗ STOPPED at gate` arrow terminus. Passing arrows in the default line color; the stopped arrow in a visibly distinct weight and a terminating cross-bar, not merely a different hue.

**Critical details (non-negotiable accuracy):**
- The EndpointSlice contains exactly **two** entries. Three Pods match the selector; only two are Ready. If the rendered slice shows three entries the figure teaches the wrong rule.
- Endpoint entries are `address:port` pairs — `10.244.1.7:5432` and `10.244.4.2:5432`. Do not strip the port and do not vary it between entries.
- Pod `10.244.4.9` **matches the selector** and is stopped by readiness. Pod `10.244.1.9` **never matched** — its label is `app: cache`, not `app: db`. These are two different failures with two different fixes, and the draft's Snag callout depends on them being visually distinguishable. Do not draw them the same way.
- The selector box holds the **query** (`app: db`), never a list of addresses. The EndpointSlice holds the **answer**. The Service does not store endpoints; that is Practice Question 11's distractor A.
- The writer is the **EndpointSlice controller**, running inside kube-controller-manager. It is not kube-proxy, not CoreDNS, not the kubelet, and not the Service. No other component may appear in this figure.
- The controller callout must not sit on the traffic path. It watches and writes; it is not a hop.
- Direction of the controller's arrow: it writes *into* the EndpointSlice. Do not draw the EndpointSlice feeding the controller.

**Source ASCII (for designer reference):**
```
  Service: database                                    EndpointSlice
  ┌────────────────────┐                              ┌──────────────────┐
  │ selector:          │                              │ 10.244.1.7:5432  │
  │   app: db          │                              │ 10.244.4.2:5432  │
  └─────────┬──────────┘                              └────────▲─────────┘
            │                                                  │
            │ query                       ┌───────────┐        │
            ▼                             │  Ready?   │        │
   ┌──────────────────┐                   │  ╔═════╗  │        │
   │ Pod  app: db     │ ──── matches ────►│  ║ === ║  ├────────┘
   │      10.244.1.7  │      ✓ Ready      │  ╚═════╝  │
   ├──────────────────┤                   │   GATE    │
   │ Pod  app: db     │ ──── matches ────►│           ├────────┘
   │      10.244.4.2  │      ✓ Ready      │           │
   ├──────────────────┤                   │           │
   │ Pod  app: db     │ ──── matches ────►│ ✗ STOPPED │
   │      10.244.4.9  │      ✗ NOT Ready  │  at gate  │
   ├──────────────────┤                   └───────────┘
   │ Pod  app: cache  │  ✗ never matched the selector
   │      10.244.1.9  │     (different failure — different file)
   └──────────────────┘

            ┌─────────────────────────────┐
            │  EndpointSlice controller   │ ◄── watches Services + Pods,
            │  (in kube-controller-manager)│     writes the slice
            └─────────────────────────────┘
```

**Proposed filename:** `ch09-fig03-service-endpointslice-selector-path.png`

```yaml-figure-spec
anchor_id: ch09-fig03-service-endpointslice-selector-path
diagram_type: data_flow
source_ascii: |2
    Service: database                                    EndpointSlice
    ┌────────────────────┐                              ┌──────────────────┐
    │ selector:          │                              │ 10.244.1.7:5432  │
    │   app: db          │                              │ 10.244.4.2:5432  │
    └─────────┬──────────┘                              └────────▲─────────┘
              │                                                  │
              │ query                       ┌───────────┐        │
              ▼                             │  Ready?   │        │
     ┌──────────────────┐                   │  ╔═════╗  │        │
     │ Pod  app: db     │ ──── matches ────►│  ║ === ║  ├────────┘
     │      10.244.1.7  │      ✓ Ready      │  ╚═════╝  │
     ├──────────────────┤                   │   GATE    │
     │ Pod  app: db     │ ──── matches ────►│           ├────────┘
     │      10.244.4.2  │      ✓ Ready      │           │
     ├──────────────────┤                   │           │
     │ Pod  app: db     │ ──── matches ────►│ ✗ STOPPED │
     │      10.244.4.9  │      ✗ NOT Ready  │  at gate  │
     ├──────────────────┤                   └───────────┘
     │ Pod  app: cache  │  ✗ never matched the selector
     │      10.244.1.9  │     (different failure — different file)
     └──────────────────┘

              ┌─────────────────────────────┐
              │  EndpointSlice controller   │ ◄── watches Services + Pods,
              │  (in kube-controller-manager)│     writes the slice
              └─────────────────────────────┘
vendor_terms: [kubernetes, service, endpointslice, pod, kube-controller-manager]
complexity_hint:
  node_count: 8
  edge_count: 6
  label_count: 16
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Trace the path from a Service selector to the addresses traffic reaches, and state that a Pod must both match the selector and be Ready to appear in the EndpointSlice"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the Ready? gate, and specifically the arrow from Pod 10.244.4.9 terminating against the gate face"
accessibility:
  alt_text_seed: "A Service named database holds the selector app equals db. Four Pods are listed; three carry the label app db and one carries app cache. The three matching Pods send arrows toward a gate labelled Ready. Two Ready Pods pass through into an EndpointSlice containing 10.244.1.7 port 5432 and 10.244.4.2 port 5432. The third matching Pod, not Ready, is stopped at the gate. The cache Pod never matched the selector and sends no arrow. Beneath, the EndpointSlice controller in kube-controller-manager watches Services and Pods and writes the slice."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes object and component names as text; shapes redrawn in the locked Lodestar style, no CNCF icon assets embedded."
```

---

## Figure: ch09-fig04-kube-proxy-modes

**Anchor ID:** `ch09-fig04-kube-proxy-modes`
**Purpose:** Show that the cluster IP is a forwarding rule rather than a listening socket — traffic passes *through* it, is never delivered *to* it — and name the modes kube-proxy uses to program that rule.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Data-flow diagram with a control-plane band above a node boundary and a packet path descending through a rules layer

**Content specification:**

Divide the canvas horizontally. **Above the divider (control plane / API objects):** two boxes side by side. Left box headed `Service` with body `10.96.0.42`. Right box headed `EndpointSlice` with body lines `10.244.1.7:5432` and `10.244.4.2:5432`. To the left of the Service box, the label `kube-proxy` with an arrow into it annotated `watches`. From beneath both boxes, arrows descend and cross the divider; the arrow from the Service box is labelled `programs`.

**The divider itself** is a heavy horizontal rule labelled at its left end `node: worker-3`. It represents the node boundary, and the two arrows from the control plane pierce it. The rule continues down the right edge of the figure as a vertical boundary, enclosing everything below-left as "inside worker-3".

**Below the divider, the packet path, top to bottom:**

1. A box labelled `frontend Pod` on the left, with an arrow to the right annotated `to 10.96.0.42`.
2. That arrow points at a **dashed, hollow, ghost box** — drawn in a lighter weight than everything else — containing `10.96.0.42` and, beneath it, `(nothing is here)`. To its right, a leader annotation reads: `the cluster IP. no process. no socket. an address with nothing at it.`
3. From the ghost box, a **dotted** line descends into a heavy bordered band labelled `R U L E S   L A Y E R`, letterspaced. Inside the band, below a dashed internal rule, the mode list on three lines: `mode: iptables (default) ·`, `IPVS · nftables ·`, `kernelspace (Windows)`. To the right of the band, an annotation reads `traffic passes THROUGH, is not delivered TO`.
4. From the bottom of the rules band, **two** arrows descend, jointly labelled `readdressed`, terminating in two boxes: `10.244.1.7` on the left, and `10.244.4.2 (on worker-11)` on the right. The right-hand box touches the vertical node boundary, showing that this endpoint lies outside worker-3.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x950 landscape
- Font: inherit book default (Fira Mono for all addresses, ports and mode names; the `R U L E S   L A Y E R` band letterspaced in the display face)
- Accent color for highlighted elements: Brass `#B58B3E` on the dashed ghost box and its `(nothing is here)` annotation. The rules band is the heaviest weight in the figure but stays in the default palette so the Brass reads as the single emphasis.

**Critical details (non-negotiable accuracy):**
- The cluster IP box is **hollow and dashed**. Nothing is drawn inside it but the address and the parenthetical. No process glyph, no server icon, no port, no socket, no daemon. If the ghost box renders as a solid box like its neighbours, the figure teaches the opposite of its own caption.
- kube-proxy **watches Service and EndpointSlice objects** — those two, and not Pods. Do not draw kube-proxy watching Pods; the EndpointSlice controller does that, and Bearings #3 item 1 turns on the distinction.
- kube-proxy **programs the rules layer**. It does not sit in the packet path. Do not place the kube-proxy label between the frontend Pod and the rules band, and do not draw the traffic arrow entering kube-proxy.
- The mode list is exactly four values: **iptables (the default)**, IPVS, nftables — Linux — and kernelspace — Windows. `iptables` is the one marked default. Do not add `userspace` (retired) or `eBPF` (a plugin data plane, not a kube-proxy mode); both are named distractors in Practice Question 18.
- Backend endpoints are Pod addresses in `10.244.x.x`; the virtual address is `10.96.0.42`. Keeping the two ranges visibly distinct is what makes "readdressed" legible.
- `10.244.4.2` is annotated `(on worker-11)` and must sit at or across the node boundary. The rules layer on worker-3 redirects to an endpoint on another node — that is the point of including it.
- The line from the ghost box into the rules layer is dotted in the source, deliberately: it marks a path that is not a delivery. Keep it visually weaker than the solid traffic arrows.

**Source ASCII (for designer reference):**
```
                       ┌──────────────┐    ┌──────────────────┐
        kube-proxy ───►│   Service    │    │  EndpointSlice   │
        watches        │  10.96.0.42  │    │ 10.244.1.7:5432  │
                       └──────────────┘    │ 10.244.4.2:5432  │
                              │            └──────────────────┘
                              │ programs           │
   ═══ node: worker-3 ════════▼════════════════════▼══════════════════
                                                                     ║
   ┌──────────┐        ┌ ─ ─ ─ ─ ─ ─ ─ ┐                             ║
   │ frontend │        ╎ 10.96.0.42    ╎  ◄── the cluster IP.        ║
   │   Pod    │───────►╎  (nothing is  ╎      no process. no socket. ║
   └──────────┘  to    ╎   here)       ╎      an address with        ║
             10.96.0.42└ ─ ─ ─ ─ ─ ─ ─ ┘      nothing at it.         ║
                              ┊                                      ║
              ┏━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━┓                     ║
              ┃   R U L E S   L A Y E R        ┃ ◄─ traffic passes   ║
              ┃  ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  ┃    THROUGH, is not   ║
              ┃  mode: iptables (default) ·    ┃    delivered TO      ║
              ┃        IPVS · nftables ·       ┃                     ║
              ┃        kernelspace (Windows)   ┃                     ║
              ┗━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━┛                     ║
                        │ readdressed  │                             ║
                        ▼              ▼                             ║
                 ┌────────────┐   ┌──────────────────────────────────╨──┐
                 │ 10.244.1.7 │   │ 10.244.4.2  (on worker-11)          │
                 └────────────┘   └─────────────────────────────────────┘
```

**Proposed filename:** `ch09-fig04-kube-proxy-modes.png`

```yaml-figure-spec
anchor_id: ch09-fig04-kube-proxy-modes
diagram_type: data_flow
source_ascii: |2
                         ┌──────────────┐    ┌──────────────────┐
          kube-proxy ───►│   Service    │    │  EndpointSlice   │
          watches        │  10.96.0.42  │    │ 10.244.1.7:5432  │
                         └──────────────┘    │ 10.244.4.2:5432  │
                                │            └──────────────────┘
                                │ programs           │
     ═══ node: worker-3 ════════▼════════════════════▼══════════════════
                                                                       ║
     ┌──────────┐        ┌ ─ ─ ─ ─ ─ ─ ─ ┐                             ║
     │ frontend │        ╎ 10.96.0.42    ╎  ◄── the cluster IP.        ║
     │   Pod    │───────►╎  (nothing is  ╎      no process. no socket. ║
     └──────────┘  to    ╎   here)       ╎      an address with        ║
               10.96.0.42└ ─ ─ ─ ─ ─ ─ ─ ┘      nothing at it.         ║
                                ┊                                      ║
                ┏━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━┓                     ║
                ┃   R U L E S   L A Y E R        ┃ ◄─ traffic passes   ║
                ┃  ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  ┃    THROUGH, is not   ║
                ┃  mode: iptables (default) ·    ┃    delivered TO      ║
                ┃        IPVS · nftables ·       ┃                     ║
                ┃        kernelspace (Windows)   ┃                     ║
                ┗━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━┛                     ║
                          │ readdressed  │                             ║
                          ▼              ▼                             ║
                   ┌────────────┐   ┌──────────────────────────────────╨──┐
                   │ 10.244.1.7 │   │ 10.244.4.2  (on worker-11)          │
                   └────────────┘   └─────────────────────────────────────┘
vendor_terms: [kubernetes, kube-proxy, service, endpointslice, iptables, ipvs, nftables]
complexity_hint:
  node_count: 8
  edge_count: 7
  label_count: 17
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point, distinguishing_alternatives]
  learning_outcome: "Explain that a cluster IP is a forwarding rule programmed on every node rather than an address anything listens on, and name kube-proxy's four modes with iptables as the Linux default"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the dashed hollow box holding 10.96.0.42 and the words nothing is here"
accessibility:
  alt_text_seed: "Above a node boundary, kube-proxy watches a Service object holding cluster IP 10.96.0.42 and an EndpointSlice holding two Pod addresses with port 5432, and programs rules below the boundary. Inside worker-3, a frontend Pod sends traffic to 10.96.0.42, drawn as a dashed empty box marked nothing is here — no process, no socket. The traffic descends through a heavy rules layer listing modes iptables as default, IPVS, nftables and Windows kernelspace, then is readdressed to two backend Pods, one local and one on worker-11."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Component and Linux subsystem names as text only; iptables, IPVS and nftables appear as mode labels, not as project marks or logos."
```

---

## Figure: ch09-fig05-dns-record-shapes

**Anchor ID:** `ch09-fig05-dns-record-shapes`
**Purpose:** Put all five cluster-DNS name shapes in one aligned four-column grid so that the invariant labels, the one varying literal, and the two structurally identical Service rows are visible at a glance.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Aligned comparison matrix — five labelled rows across four positional columns, with a resolution outcome in a detached right-hand gutter

**Content specification:**

A grid of four columns, headed `1`, `2`, `3`, `4` in a header strip across the top. To the left of column 1, a row-label gutter carrying the record kind. To the right of column 4, separated by whitespace and a horizontal rule per row (not by a table border), an outcome gutter carrying an arrow and the resolution.

The five rows, in order:

| Row label | Col 1 | Col 2 | Col 3 | Col 4 | Outcome |
|---|---|---|---|---|---|
| `Service (normal)` | `my-svc` | `my-namespace` | `svc` | `cluster.local` | `→ the cluster IP` |
| `Service (headless)` | `my-svc` | `my-namespace` | `svc` | `cluster.local` | `→ ALL the Pod IPs` |
| `SRV (named port)` | `_http._tcp.` above `my-svc`, with the row-label continuation `prefixed with →` | `my-namespace` | `svc` | `cluster.local` | `→ the named port` |
| `Pod (by address)` | `172-17-0-3` above `(dots→dashes)` | `my-namespace` | `pod` | `cluster.local` | `→ that Pod` |
| `Pod (hostname + subdomain)` | `hostname.` above `subdomain` | `namespace` | `svc` | `cluster.local` | `→ that Pod, by a stable name` |

In the `Pod (by address)` row, column 3 carries a triple-caret underline mark (`▲▲▲` in the source) drawing the eye to `pod` as the one cell in column 3 that is not `svc`.

Beneath the grid, three caption lines: *Columns 2 and 4 are identical in every row.* / *Column 3 is `svc` for everything except the Pod-by-address record.* / *The top two rows are the SAME NAME. Only the answer differs.*

Column alignment is the entire pedagogical payload. Every cell in a column shares a left edge and a width; a reader scanning down column 4 must see one repeated string with no ragged edges. If the renderer's auto-layout sizes columns to content and breaks that alignment, the figure has failed regardless of how it looks.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x700 landscape
- Font: inherit book default — **Fira Mono for every cell in columns 1–4** (these are DNS labels and must read as literals), Fira Sans for row labels, outcome gutter and captions
- Accent color for highlighted elements: Brass `#B58B3E` binding the two Service rows — a bracket, tint band, or shared rule spanning rows 1 and 2 across columns 1–4, showing them as one identical name. Secondary emphasis, in default palette weight only, on the `pod` cell in column 3.

**Critical details (non-negotiable accuracy):**
- Rows 1 and 2 are **character-for-character identical** across columns 1–4. This is the figure's central claim. Any variation introduced by the renderer — different casing, a suffix, an added marker in one row — destroys it.
- Column 3 is the literal `svc` in four of five rows and `pod` in the `Pod (by address)` row only. It is a fixed literal in the name, not a variable and not an abbreviation of anything in the reader's cluster.
- The Pod-by-address example is `172-17-0-3` with **dashes**, not dots. The `(dots→dashes)` note must accompany it.
- The SRV prefix is `_http._tcp.` — leading underscores on both labels, trailing dot — and it is **prefixed onto** the Service's four labels, which remain intact. Do not draw SRV as a five-column row; it is a four-column row with a prefix.
- The last row's column 1 holds `hostname.subdomain` across two lines. This shape additionally requires that a headless Service exist named for the subdomain; that precondition lives in the prose Dead Reckoning table and must not be silently implied away by the figure.
- Column 4 is `cluster.local` throughout. The prose sources it as `cluster-domain.example`, commonly `cluster.local`; the figure uses the common form. Do not mix the two forms across rows.
- Record types (A / AAAA / SRV) are **not** in this figure and must not be added. The prose Dead Reckoning table carries them; adding a fifth column here would break the four-label alignment that the figure exists to demonstrate.

**Source ASCII (for designer reference):**
```
                    ┌───────────────┬──────────────┬───────┬─────────────────┐
                    │       1       │      2       │   3   │        4        │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Service (normal)  │    my-svc     │ my-namespace │  svc  │ cluster.local   │  → the cluster IP
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Service (headless)│    my-svc     │ my-namespace │  svc  │ cluster.local   │  → ALL the Pod IPs
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  SRV (named port)  │ _http._tcp.   │ my-namespace │  svc  │ cluster.local   │  → the named port
     prefixed with →│    my-svc     │              │       │                 │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Pod (by address)  │  172-17-0-3   │ my-namespace │  pod  │ cluster.local   │  → that Pod
                    │  (dots→dashes)│              │  ▲▲▲  │                 │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Pod (hostname +   │   hostname.   │  namespace   │  svc  │ cluster.local   │  → that Pod, by a
     subdomain)     │   subdomain   │              │       │                 │     stable name
  ──────────────────┴───────────────┴──────────────┴───────┴─────────────────┘  ─────────────────────────

  Columns 2 and 4 are identical in every row.
  Column 3 is `svc` for everything except the Pod-by-address record.
  The top two rows are the SAME NAME. Only the answer differs.
```

**Proposed filename:** `ch09-fig05-dns-record-shapes.png`

```yaml-figure-spec
anchor_id: ch09-fig05-dns-record-shapes
diagram_type: other
source_ascii: |2
                      ┌───────────────┬──────────────┬───────┬─────────────────┐
                      │       1       │      2       │   3   │        4        │
    ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
    Service (normal)  │    my-svc     │ my-namespace │  svc  │ cluster.local   │  → the cluster IP
    ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
    Service (headless)│    my-svc     │ my-namespace │  svc  │ cluster.local   │  → ALL the Pod IPs
    ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
    SRV (named port)  │ _http._tcp.   │ my-namespace │  svc  │ cluster.local   │  → the named port
       prefixed with →│    my-svc     │              │       │                 │
    ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
    Pod (by address)  │  172-17-0-3   │ my-namespace │  pod  │ cluster.local   │  → that Pod
                      │  (dots→dashes)│              │  ▲▲▲  │                 │
    ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
    Pod (hostname +   │   hostname.   │  namespace   │  svc  │ cluster.local   │  → that Pod, by a
       subdomain)     │   subdomain   │              │       │                 │     stable name
    ──────────────────┴───────────────┴──────────────┴───────┴─────────────────┘  ─────────────────────────

    Columns 2 and 4 are identical in every row.
    Column 3 is `svc` for everything except the Pod-by-address record.
    The top two rows are the SAME NAME. Only the answer differs.
vendor_terms: [kubernetes, coredns]
complexity_hint:
  node_count: 5
  edge_count: 5
  label_count: 30
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Write the DNS name of a Service in another namespace, and recognise that the normal and headless Service name forms are identical while their answers differ"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the two Service rows, normal and headless, bound together to show columns one through four are identical"
accessibility:
  alt_text_seed: "A four-column grid of cluster DNS name shapes. Normal Service and headless Service occupy identical rows — my-svc, my-namespace, svc, cluster.local — resolving to the cluster IP and to all the Pod IPs respectively. An SRV row prefixes underscore http underscore tcp onto the same four labels. A Pod-by-address row uses 172-17-0-3 with dots converted to dashes and the literal pod in column three instead of svc. A final row uses hostname dot subdomain for a Pod's stable name. Columns two and four are identical in every row."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Documented DNS name grammar rendered as a typographic table; no vendor marks or icons."
```

---

## Figure: ch09-zenith-stable-name-over-churn

> ⚠ **Anchor ID does not conform to rule 4.** See the *ANCHOR ID FORMAT VIOLATIONS* section at the top of this file. The ID is preserved verbatim below per rule 6; author review decides whether to renumber to `ch09-fig06-zenith-stable-name-over-churn`.

**Anchor ID:** `ch09-zenith-stable-name-over-churn`
**Purpose:** Carry the chapter's ☀️ Zenith — that a Service is a label query with a name, and that the virtual IP, the endpoint list and the DNS record are three control loops publishing one query's current answer while nothing underneath survives.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** Two-register synthesis diagram — a temporal churn band above a stable banner, and a one-to-three publication fan-out below

**Content specification:**

**Top register — the stable thing.** A single wide double-ruled banner spanning nearly the full width, containing one line: `database.production.svc.cluster.local · 10.96.0.42`. This banner is unchanging and is the visual constant of the figure.

**Second register — the churn.** Four small boxes in a row beneath the banner, each connected upward to the banner by its own arrow. Each arrow is time-labelled, left to right: `t₀`, `t₁`, `t₂`, `t₃`. Each box holds three Pod addresses and three glyphs marking Pod generation. The contents, in order:

- `t₀`: glyphs `▲ ▲ ▲`, addresses `.1.7`, `.4.2`, `.4.3`
- `t₁`: glyphs `▲ ● ●`, addresses `.1.7`, `.2.8`, `.2.9`
- `t₂`: glyphs `● ■ ■`, addresses `.2.8`, `.5.1`, `.5.4`
- `t₃`: glyphs `◆ ◆ ◆`, addresses `.7.3`, `.8.9`, `.9.0`

The glyph shape encodes generation and is load-bearing: at `t₀` all three Pods are the same generation; by `t₁` one original survives beside two newcomers; by `t₃` nothing from `t₀` remains. Under the four boxes, the caption: *(nothing survives from t₀ to t₃ — not one Pod, not one address)*.

**Third register — the mechanism.** A wide bordered strip containing a left-to-right chain: `query` → `answer` → `publish`, with `(app: db)` set beneath `query` and `(EndpointSlice)` beneath `answer`.

**Fourth register — the fan-out.** From `publish`, three arrows descend and diverge to three terminal boxes, evenly spaced: `rules layer (§6)` on the left, drawn in the heaviest border weight to echo fig04's rules band; `endpoint list (§4)` in the centre; `DNS record (§7)` on the right. Beneath them, the closing caption: *three readers · one answer · one question that never changed*.

The figure's whole argument is vertical: everything below the banner changes, and the banner does not.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x900 landscape
- Font: inherit book default (Fira Mono for the FQDN, the cluster IP, all `.x.y` address fragments and `app: db`; Fira Sans for captions and the `§` cross-references)
- Accent color for highlighted elements: Brass `#B58B3E` on the double-ruled banner. This is the ☀️ Zenith figure and the banner is the synthesis object; nothing else in the figure takes Brass.

**Critical details (non-negotiable accuracy):**
- The banner text is **stable across all four time steps** and must be drawn once, spanning them. Do not repeat it per time step; repetition would imply it is being re-established rather than persisting.
- **No address recurs between `t₀` and `t₃`.** A designer tidying the address fragments must not reuse a value across the first and last boxes — the caption asserts total turnover and the boxes must bear it out. The one deliberate overlap is `.1.7` surviving from `t₀` into `t₁`, and `.2.8` from `t₁` into `t₂`; those are partial-rollover evidence and must be preserved exactly.
- Glyph shapes (`▲ ● ■ ◆`) encode Pod generation and must remain **four distinct shapes**, not four colors. This figure is explicitly grayscale-critical; if generation is conveyed by hue alone it disappears on E-ink.
- Each time-step box holds exactly **three** Pods. The replica count is constant while the membership turns over; varying it would introduce a scaling story the chapter does not tell.
- The chain reads `query → answer → publish`, in that order, once. There is **one** query and **one** answer feeding **three** consumers. Do not draw three separate queries, three answers, or any arrow from a terminal box back to the query.
- The three terminals are `rules layer`, `endpoint list`, `DNS record`. Their section tags `(§6)`, `(§4)`, `(§7)` are part of the labels and must survive — they are the retrieval hooks back into the chapter, and the sections are deliberately out of numeric order left to right. Do not reorder them into §4, §6, §7.
- The cluster IP shown is `10.96.0.42`, matching fig04. Keep it consistent across the two figures; the reader is meant to recognise it.
- The FQDN is `database.production.svc.cluster.local` — the chapter's running example Service in the `production` namespace. Do not substitute `my-svc.my-namespace` here; fig05 owns the generic form and this figure owns the concrete one.

**Source ASCII (for designer reference):**
```
   ╔═══════════════════════════════════════════════════════════════════════╗
   ║        database.production.svc.cluster.local   ·   10.96.0.42         ║
   ╚═══════════════════════════════════════════════════════════════════════╝
        ▲                    ▲                    ▲                   ▲
        │  t₀                │  t₁                │  t₂               │  t₃
   ┌────┴─────┐        ┌─────┴────┐         ┌─────┴────┐        ┌─────┴────┐
   │ ▲  ▲  ▲  │        │ ▲  ●  ●  │         │ ●  ■  ■  │        │ ◆  ◆  ◆  │
   │.1.7 .4.2 │        │.1.7 .2.8 │         │.2.8 .5.1 │        │.7.3 .8.9 │
   │   .4.3   │        │    .2.9  │         │    .5.4  │        │    .9.0  │
   └──────────┘        └──────────┘         └──────────┘        └──────────┘
     (nothing survives from t₀ to t₃ — not one Pod, not one address)

   ┌───────────────────────────────────────────────────────────────────────┐
   │   query  ────────►  answer  ────────►  publish                        │
   │  (app: db)        (EndpointSlice)          │                          │
   └────────────────────────────────────────────┼──────────────────────────┘
                     ┌──────────────────────────┼──────────────────────────┐
                     ▼                          ▼                          ▼
              ┏━━━━━━━━━━━━┓           ┌──────────────┐           ┌────────────────┐
              ┃ rules layer┃           │ endpoint list│           │  DNS record    │
              ┃   (§6)     ┃           │     (§4)     │           │     (§7)       │
              ┗━━━━━━━━━━━━┛           └──────────────┘           └────────────────┘
                three readers · one answer · one question that never changed
```

**Proposed filename:** `ch09-zenith-stable-name-over-churn.png`
*(Filename tracks the anchor ID. If the author accepts the `fig06` renumbering, this becomes `ch09-fig06-zenith-stable-name-over-churn.png`.)*

```yaml-figure-spec
anchor_id: ch09-zenith-stable-name-over-churn
diagram_type: concept_map
source_ascii: |2
     ╔═══════════════════════════════════════════════════════════════════════╗
     ║        database.production.svc.cluster.local   ·   10.96.0.42         ║
     ╚═══════════════════════════════════════════════════════════════════════╝
          ▲                    ▲                    ▲                   ▲
          │  t₀                │  t₁                │  t₂               │  t₃
     ┌────┴─────┐        ┌─────┴────┐         ┌─────┴────┐        ┌─────┴────┐
     │ ▲  ▲  ▲  │        │ ▲  ●  ●  │         │ ●  ■  ■  │        │ ◆  ◆  ◆  │
     │.1.7 .4.2 │        │.1.7 .2.8 │         │.2.8 .5.1 │        │.7.3 .8.9 │
     │   .4.3   │        │    .2.9  │         │    .5.4  │        │    .9.0  │
     └──────────┘        └──────────┘         └──────────┘        └──────────┘
       (nothing survives from t₀ to t₃ — not one Pod, not one address)

     ┌───────────────────────────────────────────────────────────────────────┐
     │   query  ────────►  answer  ────────►  publish                        │
     │  (app: db)        (EndpointSlice)          │                          │
     └────────────────────────────────────────────┼──────────────────────────┘
                       ┌──────────────────────────┼──────────────────────────┐
                       ▼                          ▼                          ▼
                ┏━━━━━━━━━━━━┓           ┌──────────────┐           ┌────────────────┐
                ┃ rules layer┃           │ endpoint list│           │  DNS record    │
                ┃   (§6)     ┃           │     (§4)     │           │     (§7)       │
                ┗━━━━━━━━━━━━┛           └──────────────┘           └────────────────┘
                  three readers · one answer · one question that never changed
vendor_terms: [kubernetes, service, endpointslice]
complexity_hint:
  node_count: 12
  edge_count: 9
  label_count: 24
pedagogy:
  part_18_criteria_met: [temporal_structure, spatial_structure, zenith]
  learning_outcome: "Recognise a Service as a label query with a name, whose current answer three control loops publish as a forwarding rule, an endpoint list and a DNS record, while the Pods behind it turn over completely"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the double-ruled banner carrying database.production.svc.cluster.local and 10.96.0.42, which is the one element that does not change across t0 to t3"
accessibility:
  alt_text_seed: "A single unchanging banner reads database.production.svc.cluster.local and cluster IP 10.96.0.42. Beneath it, four time-step boxes labelled t0 through t3 each hold three Pods, drawn with different generation glyphs and different address fragments; no Pod or address from t0 remains at t3. Below, a chain reads query on the label app equals db, then answer as an EndpointSlice, then publish, fanning out to three consumers: the rules layer from section six, the endpoint list from section four, and the DNS record from section seven. The caption reads three readers, one answer, one question that never changed."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes object names and DNS grammar as text; abstract synthesis composition original to Lodestar Ledgers."
```

---

## Extraction notes (for author review, not for the illustrator)

- **All six figures are `Mandatory: yes` and `Replaces ASCII: yes`.** None of the ASCII blocks in this chapter is intended to survive into the rendered book; each is a design placeholder that the diagram pipeline should replace.
- **Two figures deliberately withhold facts the chapter also withholds.** fig02 must not gain port fields, and fig04 must not gain `userspace` or `eBPF` modes. Both restrictions trace to `AUTHOR-REVIEW` comments and to Practice Question distractors in the draft; a well-meaning designer "completing" either figure would put an unsourced claim into the book through the figure layer, where the source-tag audit does not look.
- **Cross-figure consistency contracts.** `10.96.0.42` is the cluster IP in both fig04 and the Zenith figure. `10.244.1.7` and `10.244.4.2` are the two Ready backends in fig01, fig03 and fig04. The Pod-network range is `10.244.x.x` and the Service range is `10.96.x.x` throughout. Any renderer that regenerates example addresses independently per figure will break the reader's ability to follow one example across the chapter, which is the chapter's stated structure ("each section will hand it to the next").
- **`grayscale_critical: true` on all six.** Distribution is ebook-primary but E-ink is a real target, and in every figure here at least one distinction — a stopped arrow, a hollow ghost box, a generation glyph, a bound pair of rows — is doing pedagogical work that must not depend on hue alone.
- **`diagram_type: other` on fig05** is deliberate rather than a gap. The controlled vocabulary has no value for an aligned comparison matrix; per the field guidance, `other` routes to D2, which can hold the column alignment the figure depends on. If the vocabulary grows a `comparison_matrix` or `table_grid` value, fig05 should be retagged.
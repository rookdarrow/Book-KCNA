# Image Specifications — KCNA Chapter 5

*Generated from the voiced draft at `../Book-KCNA/.pipeline-state/ch-05/draft-v1.md`. (The Stage 9 voice pass writes in place: `draft-v1.md` is the voiced text; `draft-v1-prevoice.md` is the preserved pre-voice copy. There is no `draft-voice.md` on disk for this chapter.) Every ASCII diagram in the draft has an entry here; every entry corresponds to an anchor in the draft.*

**Anchor census:** 6 anchor comments, 6 fenced diagram blocks, 1:1 adjacency confirmed (anchors at draft lines 139, 218, 387, 594, 710, 819; fences open at 140, 219, 388, 595, 711, 820).

---

## UNANCHORED DIAGRAMS

None. Every fenced diagram block in the draft is immediately preceded by a `<!-- FIGURE: ... -->` anchor comment.

---

## MALFORMED ANCHORS

The following anchor does not conform to the locked `ch{NN}-fig{MM}-{kebab-slug}` format ([LOCKED 2026-04-18], Visuals / Figures).

### `ch05-zenith-smallest-deployable-unit` — draft line 819

Missing the `fig{MM}` segment. It reads `ch05-` + `zenith-...` where the format requires `ch05-figMM-...`. Per rule 6 the ID is **preserved unrenamed** in this document so the join key stays stable; renaming is an author-review decision.

**Suggested correction:** `ch05-fig06-smallest-deployable-unit` — author to confirm, then update the draft anchor and this document together in one edit so the join key never diverges.

---

## ANCHOR ORDERING NOTE (advisory, not a format violation)

Figure numbers do not run in document order: `fig01` (line 139) → `fig03` (line 218) → `fig02` (line 387) → `fig04` → `fig05` → *zenith*. This suggests §3's figure was added after §5's was numbered. Not a lint failure, but the book-level index will read out of sequence. Author may wish to renumber `fig02`↔`fig03` at the same time as the malformed-anchor fix above, since both edits touch the same join keys.

---

## Figure: ch05-fig01-pod-shared-network-namespace

**Anchor ID:** `ch05-fig01-pod-shared-network-namespace`
**Purpose:** Establishes the chapter's load-bearing fact — the IP address belongs to the Pod boundary, not to any container inside it — which every subsequent section depends on.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** nested containment diagram (three levels: Node → Pod → containers), with a bidirectional intra-Pod link and a shared-storage node

**Content specification:**
Draw three levels of nesting as concentric rounded rectangles. The outermost box is labelled **Node**. Inside it, indented, sits a box labelled **Pod**, and the Pod box carries the label **`IP: 10.42.1.7`** with a short pointer or bracket tying that label unambiguously to the *Pod's* border — an annotation reading "one address, on the Pod" sits beside it. Inside the Pod box sit two sibling boxes side by side, left labelled **`container: app`** and right labelled **`container: helper`**, connected by a horizontal double-headed arrow whose caption reads **`via localhost`**. Below the two containers, centred between them, sits a third smaller box labelled **`shared volume`**, with a line descending from each container and joining before entering the volume box — the two containers reach the same volume. Neither container box carries an IP address of its own; that absence is deliberate and must be visually obvious. The single element that is "the point" of this figure is the **placement of the IP label on the Pod border**, and it is the element the surrounding prose explicitly directs the reader to look at ("Note where the IP address is attached in that figure… That placement is the pedagogy, not decoration"). Do not add a Node IP, a kubelet box, or any other node-level component; the Node box exists only to establish that the Pod sits on one machine.

**Visual style:**
- Palette: inherit book default (Lodestar Ledgers navy/slate line-art register)
- Size (pixels): 900x520 landscape
- Font: inherit book default (Fira Sans body, Fira Mono for identifiers such as `localhost` and the IP)
- Accent color for highlighted elements: Brass `#B58B3E` on the Pod's border and the `IP: 10.42.1.7` label only

**Critical details (non-negotiable accuracy):**
- The IP address attaches to the **Pod**, never to a container. A render that puts an IP on either container box inverts the chapter's central fact and must be rejected.
- The `localhost` arrow is **between the two containers**, not from a container out to the Node or to any external network.
- The shared volume is drawn **inside** the Pod boundary — this figure depicts an intra-Pod shared volume, not persistent storage (Ch 11 material).
- Exactly two containers. The figure argues that a Pod *can* hold more than one, not that it must; a one-container render loses the `localhost` teaching entirely.
- The nesting order is Node ⊃ Pod ⊃ containers. Any flattening into side-by-side peers destroys the point.

**Source ASCII (for designer reference):**
```
┌─ Node ──────────────────────────────────────────────────┐
│                                                          │
│   ┌─ Pod ─────────────────────────────────────────┐      │
│   │  IP: 10.42.1.7   ← one address, on the Pod    │      │
│   │                                                │      │
│   │   ┌─ container: app ─┐   ┌─ container: helper┐ │      │
│   │   │                  │◄─►│                   │ │      │
│   │   │                  │   │                   │ │      │
│   │   └────────┬─────────┘   └────────┬──────────┘ │      │
│   │            │   via localhost      │            │      │
│   │            └───────┬──────────────┘            │      │
│   │                    │                            │      │
│   │            ┌───────▼────────┐                   │      │
│   │            │ shared volume  │                   │      │
│   │            └────────────────┘                   │      │
│   └────────────────────────────────────────────────┘      │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Proposed filename:** `ch05-fig01-pod-shared-network-namespace.png`

```yaml-figure-spec
anchor_id: ch05-fig01-pod-shared-network-namespace
diagram_type: k8s_architecture
source_ascii: |2
  ┌─ Node ──────────────────────────────────────────────────┐
  │                                                          │
  │   ┌─ Pod ─────────────────────────────────────────┐      │
  │   │  IP: 10.42.1.7   ← one address, on the Pod    │      │
  │   │                                                │      │
  │   │   ┌─ container: app ─┐   ┌─ container: helper┐ │      │
  │   │   │                  │◄─►│                   │ │      │
  │   │   │                  │   │                   │ │      │
  │   │   └────────┬─────────┘   └────────┬──────────┘ │      │
  │   │            │   via localhost      │            │      │
  │   │            └───────┬──────────────┘            │      │
  │   │                    │                            │      │
  │   │            ┌───────▼────────┐                   │      │
  │   │            │ shared volume  │                   │      │
  │   │            └────────────────┘                   │      │
  │   └────────────────────────────────────────────────┘      │
  │                                                            │
  └────────────────────────────────────────────────────────────┘
vendor_terms: [pod, node, container, volume]
complexity_hint:
  node_count: 5
  edge_count: 3
  label_count: 7
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "Identify that a Pod holds one cluster-wide IP shared by all its containers, which reach each other over localhost"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the IP: 10.42.1.7 label bound to the Pod border"
accessibility:
  alt_text_seed: "A Node contains one Pod; the Pod carries a single IP address on its own boundary and holds two containers, app and helper, which communicate over localhost and both read and write a shared volume inside the Pod"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Generic boxes redrawn in Lodestar line-art style; revise to licensed_icon_set if the renderer substitutes official Kubernetes/CNCF icons"
```

---

## Figure: ch05-fig03-init-containers-sequence

**Anchor ID:** `ch05-fig03-init-containers-sequence`
**Purpose:** Contrasts the strictly sequential execution of init containers against the parallel start of app containers, and shows that an init failure means the app containers never start at all.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel temporal flow diagram (success path above, failure path below) with a fork on the success path

**Content specification:**
Two stacked panels sharing a left-to-right time axis, each panel headed by its own label. The upper panel is headed **SUCCESS PATH**: a horizontal time arrow runs left to right beneath the heading, and along it sit three stages — a box labelled **`init-1`**, an arrow captioned **`exit 0`**, a box labelled **`init-2`**, a second arrow captioned **`exit 0`**, and then a fork that splits into two parallel horizontal tracks, upper labelled **`app-a`** and lower labelled **`app-b`**, both continuing rightward to open arrowheads. A small annotation under the init stages reads **"(sequential, one at a time)"**; a matching annotation under the fork reads **"(parallel, together)"**. The lower panel is headed **FAILURE PATH** and repeats the same time axis: **`init-1`** → **`exit 0`** → **`init-2`** → but here the outgoing arrow is captioned **`exit 1`** and leads to a terminal note reading **"(restart per restartPolicy)"**. A second branch drops downward from `init-2` to a strongly-set terminal statement: **"app containers: NEVER STARTED"**. Nothing continues past that point on the failure panel — the absence of any onward arrow is itself the teaching. The two elements that carry the section are the **sequential-versus-parallel contrast** in the upper panel and the **dead end** in the lower one; both must be legible at a glance without reading captions.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1100x620 landscape
- Font: inherit book default (Fira Mono for `init-1`, `init-2`, `app-a`, `app-b`, `exit 0`, `exit 1`, `restartPolicy`)
- Accent color for highlighted elements: Brass `#B58B3E` on the `exit 1` arrow and the "app containers: NEVER STARTED" terminal

**Critical details (non-negotiable accuracy):**
- Init containers are **sequential**, one at a time, each gated on the previous one's successful exit. They must never be drawn side by side or forked.
- App containers are **parallel** — they start together. They must never be drawn in a chain.
- `exit 0` = success and advances the sequence; `exit 1` (any non-zero) = failure. Do not swap these.
- On the failure path the app containers are **not started at all** — not started-then-killed, not started-then-crashed. Never started.
- The restart on failure is governed by the Pod's `restartPolicy`; the figure names the field but must not assert a specific policy value.
- Both panels share one left-to-right time direction. Do not mirror the failure panel.

**Source ASCII (for designer reference):**
```
SUCCESS PATH
  time ──────────────────────────────────────────────────────►

  [ init-1 ]──exit 0──►[ init-2 ]──exit 0──►┌─[ app-a ]────────►
                                             └─[ app-b ]────────►
   (sequential, one at a time)                (parallel, together)


FAILURE PATH
  time ──────────────────────────────────────────────────────►

  [ init-1 ]──exit 0──►[ init-2 ]──exit 1──►(restart per
                                              restartPolicy)
                            │
                            └──► app containers: NEVER STARTED
```

**Proposed filename:** `ch05-fig03-init-containers-sequence.png`

```yaml-figure-spec
anchor_id: ch05-fig03-init-containers-sequence
diagram_type: activity
source_ascii: |2
  SUCCESS PATH
    time ──────────────────────────────────────────────────────►

    [ init-1 ]──exit 0──►[ init-2 ]──exit 0──►┌─[ app-a ]────────►
                                               └─[ app-b ]────────►
     (sequential, one at a time)                (parallel, together)


  FAILURE PATH
    time ──────────────────────────────────────────────────────►

    [ init-1 ]──exit 0──►[ init-2 ]──exit 1──►(restart per
                                                restartPolicy)
                              │
                              └──► app containers: NEVER STARTED
vendor_terms: [pod, init-container, container]
complexity_hint:
  node_count: 9
  edge_count: 8
  label_count: 13
pedagogy:
  part_18_criteria_met: [temporal_structure, distinguishing_alternatives]
  learning_outcome: "Predict that init containers run sequentially to completion before app containers start in parallel, and that an init failure leaves app containers never started"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the 'app containers: NEVER STARTED' terminal on the failure path"
accessibility:
  alt_text_seed: "Two timelines: on the success path init-1 exits zero then init-2 exits zero, after which app-a and app-b start together in parallel; on the failure path init-2 exits non-zero, restart is governed by restartPolicy, and the app containers are never started"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Concept redrawn from Kubernetes init-container ordering semantics; no vendor artwork reproduced"
```

**Handoff note:** the prose this figure supports carries an unresolved `AUTHOR-REVIEW` at draft line 216 — the init-container ordering semantics are currently untagged because `kubernetes.io/docs/concepts/workloads/pods/init-containers/` was not fetched at research time. The figure's content is not in dispute, but do not render final art until that source gap closes, in case the fetched source changes the wording of the restart behaviour.

---

## Figure: ch05-fig02-pod-phases-and-container-states

**Anchor ID:** `ch05-fig02-pod-phases-and-container-states`
**Purpose:** Makes the phase-versus-state distinction spatial — container states are drawn *inside* the Pod because one genuinely contains the other — and then proves with a worked overlay that a Pod can report `Running` while a container inside it sits in `Waiting`.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel nested state diagram (schematic panel above, worked instance panel below)

**Content specification:**
Two stacked panels. The **upper panel** is a large box labelled **POD**. Along its top runs the Pod-scoped vocabulary on one line: **`status.phase:`** followed by a transition chain **`Pending → Running → Succeeded`**, with a second branch dropping from `Running` to **`Failed`**, and a third entry beneath reading **`(any) → Unknown`** to show that Unknown is reachable from anywhere. Below that, still *inside* the POD box, sit two nested sub-boxes: **`container: app`** and **`container: helper`**. Each nested box carries its own separate vocabulary line: **`state: Waiting → Running → Terminated`**. Under the `app` box's chain only, add the per-state payload annotations aligned beneath their states — **`(+Reason)`** under Waiting, **`(+startedAt)`** under Running, **`(+exitCode)`** under Terminated. The **lower panel** is headed **"WORKED OVERLAY — both readings are legitimate"** and shows one concrete instant: a POD box labelled **`phase: Running`** containing two boxes, **`app  state: Running`** and **`helper  state: Waiting   Reason: CrashLoopBackOff`**. The pedagogy is the **nesting**: phase and state must never appear as side-by-side peer lists, because the surrounding prose says explicitly that a side-by-side reading means "the figure has failed and so has the model." The lower panel's job is to make the apparent contradiction — Pod `Running`, container `Waiting` — look obviously non-contradictory once the scopes are nested.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1000x760 portrait
- Font: inherit book default (Fira Mono for every phase and state value, and for `CrashLoopBackOff`, `Reason`, `startedAt`, `exitCode`, `status.phase`)
- Accent color for highlighted elements: Brass `#B58B3E` on the lower panel's `phase: Running` label

**Critical details (non-negotiable accuracy):**
- **Five phase values, and only these five:** Pending, Running, Succeeded, Failed, Unknown. Phase is Pod-scoped.
- **Three container state values, and only these three:** Waiting, Running, Terminated. State is per-container.
- The two vocabularies are **not interchangeable**. `Waiting` is never a phase; `Pending` is never a container state. A render that mixes a term across scopes is a hard reject.
- Container state boxes are drawn **inside** the Pod box. Not adjacent, not below as a peer, not in a separate legend.
- A Pod with two containers has **one** phase and **two** states. The count asymmetry must be visible.
- The payload annotations are per-state and correct as paired: Waiting carries a `Reason`, Running carries `startedAt`, Terminated carries an exit code (plus reason and start/finish times).
- In the worked overlay the Pod is `Running` while a container is `Waiting`. This is the single most consequential fact in the chapter and must not be "tidied" into agreement.
- The Waiting reason in the overlay is `CrashLoopBackOff`, never `ImagePullBackOff` (revised 2026-09-04): an image that was never pulled means a container that was never created, and the chapter's quoted definition of `Running` requires every container to have been created — that Pod is `Pending`. CrashLoopBackOff is a created container waiting between restarts, the one pairing the prose licenses.
- The source ASCII at draft line 408 contains a stray hyphen in a box border (`────-┘`). That is a drafting artifact; do not reproduce it.

**Source ASCII (for designer reference):**
```
┌─ POD ──────────────────────────────────────────────────────┐
│  status.phase:  Pending → Running → Succeeded              │
│                                   └→ Failed                │
│                  (any) → Unknown                            │
│                                                             │
│   ┌─ container: app ────────────────────────────────────┐   │
│   │  state:  Waiting → Running → Terminated             │   │
│   │          (+Reason)  (+startedAt)  (+exitCode)        │   │
│   └─────────────────────────────────────────────────────┘   │
│                                                             │
│   ┌─ container: helper ─────────────────────────────────┐   │
│   │  state:  Waiting → Running → Terminated             │   │
│   └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘

WORKED OVERLAY — both readings are legitimate:

┌─ POD  phase: Running ──────────────────────────────────────┐
│   ┌─ app     state: Running                             ┐  │
│   └─────────────────────────────────────────────────────┘  │
│   ┌─ helper  state: Waiting   Reason: CrashLoopBackOff   ┐  │
│   └─────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

**Proposed filename:** `ch05-fig02-pod-phases-and-container-states.png`

```yaml-figure-spec
anchor_id: ch05-fig02-pod-phases-and-container-states
diagram_type: state_machine
source_ascii: |2
  ┌─ POD ──────────────────────────────────────────────────────┐
  │  status.phase:  Pending → Running → Succeeded              │
  │                                   └→ Failed                │
  │                  (any) → Unknown                            │
  │                                                             │
  │   ┌─ container: app ────────────────────────────────────┐   │
  │   │  state:  Waiting → Running → Terminated             │   │
  │   │          (+Reason)  (+startedAt)  (+exitCode)        │   │
  │   └─────────────────────────────────────────────────────┘   │
  │                                                             │
  │   ┌─ container: helper ─────────────────────────────────┐   │
  │   │  state:  Waiting → Running → Terminated             │   │
  │   └─────────────────────────────────────────────────────┘   │
  └─────────────────────────────────────────────────────────────┘

  WORKED OVERLAY — both readings are legitimate:

  ┌─ POD  phase: Running ──────────────────────────────────────┐
  │   ┌─ app     state: Running                             ┐  │
  │   └─────────────────────────────────────────────────────┘  │
  │   ┌─ helper  state: Waiting   Reason: CrashLoopBackOff   ┐  │
  │   └─────────────────────────────────────────────────────┘  │
  └─────────────────────────────────────────────────────────────┘
vendor_terms: [pod, container]
complexity_hint:
  node_count: 17
  edge_count: 8
  label_count: 20
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, temporal_structure]
  learning_outcome: "Distinguish a Pod's phase from a container's state by scope, and accept that a Pod may be Running while a container inside it is Waiting"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the 'phase: Running' label in the worked overlay panel"
accessibility:
  alt_text_seed: "A Pod box shows five phase values Pending, Running, Succeeded, Failed and Unknown, and nested inside it two container boxes each show three states Waiting, Running and Terminated; a second panel shows a real instant where the Pod's phase is Running while its helper container's state is Waiting with reason CrashLoopBackOff"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Phase and state vocabularies are factual API field values; layout and nesting are our own interpretation"
```

---

## Figure: ch05-fig04-three-probes-compared

**Anchor ID:** `ch05-fig04-three-probes-compared`
**Purpose:** Isolates the one asymmetry the exam tests — two probes kill without de-registering, one de-registers without killing — by giving each probe an explicit "does *not*" column.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** three-row comparison matrix rendered as a figure (four columns: probe name, what it asks, on failure, what it does *not* do)

**Content specification:**
A four-column table with a header row and three body rows, rendered as a designed figure rather than body-text markup. The leftmost column holds the row labels **`liveness`**, **`readiness`**, **`startup`** in monospace. Column two is headed **ASKS** and holds, in order: "Is the container running?", "Can the container respond to requests?", "Has the application started?". Column three is headed **ON FAILURE** and holds: "kubelet **KILLS** the container → restart policy applies", "Pod IP **REMOVED** from endpoints of all matching Services", "kubelet **KILLS** the container → restart policy applies". Column four is headed **DOES *NOT*** and holds: "remove it from Service endpoints", "kill or restart anything — the container keeps running", "run alongside the others — it **SUPPRESSES** them until it succeeds". The fourth column is the one doing the teaching and must be visually weighted to say so — the surrounding prose states this outright. Give column four a tinted or ruled background so the eye lands there, and set the verbs KILLS, REMOVED and SUPPRESSES in a heavier weight throughout. The liveness and startup rows should read as visually similar to each other and visibly different from the readiness row, because that grouping *is* the fact: readiness is the odd one out.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x480 landscape
- Font: inherit book default (Fira Mono for `liveness`, `readiness`, `startup`; Fira Sans for cell prose)
- Accent color for highlighted elements: Brass `#B58B3E` on the readiness row's "Pod IP REMOVED from endpoints" cell

**Critical details (non-negotiable accuracy):**
- **Liveness failure → the kubelet kills the container**, which is then subject to the Pod's restart policy. Liveness does **not** remove the Pod from Service endpoints.
- **Readiness failure → the endpoints controller removes the Pod's IP from the endpoints of all matching Services.** Nothing is killed and nothing is restarted; the container keeps running.
- **Startup failure → the kubelet kills the container** and the restart policy applies — same consequence as liveness, not same as readiness.
- **A configured startup probe disables the other two probes until it succeeds.** It does not run alongside them. This suppression is the startup probe's entire reason for existing.
- The actor differs by row and must not be smoothed over: the **kubelet** kills; the **endpoints controller** removes. Do not attribute the endpoint removal to the kubelet.
- Three probe types only. Do not add the four check *mechanisms* (`exec`, `httpGet`, `tcpSocket`, `grpc`) to this figure — the prose deliberately keeps mechanisms and types in separate compartments, and merging them here would undo that.

**Source ASCII (for designer reference):**
```
             │ ASKS                    │ ON FAILURE           │ DOES *NOT*
─────────────┼─────────────────────────┼──────────────────────┼──────────────────────
 liveness    │ Is the container        │ kubelet KILLS the    │ remove it from
             │ running?                │ container → restart  │ Service endpoints
             │                         │ policy applies       │
─────────────┼─────────────────────────┼──────────────────────┼──────────────────────
 readiness   │ Can the container       │ Pod IP REMOVED from  │ kill or restart
             │ respond to requests?    │ endpoints of all     │ anything — the
             │                         │ matching Services    │ container keeps running
─────────────┼─────────────────────────┼──────────────────────┼──────────────────────
 startup     │ Has the application     │ kubelet KILLS the    │ run alongside the
             │ started?                │ container → restart  │ others — it SUPPRESSES
             │                         │ policy applies       │ them until it succeeds
```

**Proposed filename:** `ch05-fig04-three-probes-compared.png`

```yaml-figure-spec
anchor_id: ch05-fig04-three-probes-compared
diagram_type: other
source_ascii: |2
               │ ASKS                    │ ON FAILURE           │ DOES *NOT*
  ─────────────┼─────────────────────────┼──────────────────────┼──────────────────────
   liveness    │ Is the container        │ kubelet KILLS the    │ remove it from
               │ running?                │ container → restart  │ Service endpoints
               │                         │ policy applies       │
  ─────────────┼─────────────────────────┼──────────────────────┼──────────────────────
   readiness   │ Can the container       │ Pod IP REMOVED from  │ kill or restart
               │ respond to requests?    │ endpoints of all     │ anything — the
               │                         │ matching Services    │ container keeps running
  ─────────────┼─────────────────────────┼──────────────────────┼──────────────────────
   startup     │ Has the application     │ kubelet KILLS the    │ run alongside the
               │ started?                │ container → restart  │ others — it SUPPRESSES
               │                         │ policy applies       │ them until it succeeds
vendor_terms: [kubelet, pod, service, endpoints]
complexity_hint:
  node_count: 12
  edge_count: 0
  label_count: 15
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, fixed_point]
  learning_outcome: "Predict the distinct consequence of each probe's failure, and identify readiness as the only probe that de-registers without restarting"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the readiness row's 'Pod IP REMOVED from endpoints' cell"
accessibility:
  alt_text_seed: "A three-row comparison of Kubernetes probes: liveness asks whether the container is running and on failure the kubelet kills it without removing it from Service endpoints; readiness asks whether the container can respond and on failure the Pod IP is removed from matching Service endpoints without killing or restarting anything; startup asks whether the application has started, on failure the kubelet kills the container, and while configured it suppresses the other two probes"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Comparison matrix authored by Lodestar from Kubernetes pod-lifecycle documentation; no vendor artwork reproduced"
```

**Router note:** this is a comparison matrix rather than a node-and-edge diagram, so no controlled-vocabulary value fits; `other` routes it to the D2 fallback, which handles grid/table shapes well. Column four needs differential emphasis — a plain uniform table render loses the figure's entire purpose.

---

## Figure: ch05-fig05-requests-limits-qos-classes

**Anchor ID:** `ch05-fig05-requests-limits-qos-classes`
**Purpose:** Renders request and limit as two marks on one continuous resource axis, so that "request is a floor, limit is a ceiling" becomes a spatial fact rather than a definition to memorise — and attaches each mark to the component that acts on it.
**Replaces ASCII:** yes
**Mandatory:** yes — **but currently BLOCKED**, see the source-gap note below
**Type:** annotated range band (single horizontal axis divided into three zones) with component attributions and a two-row enforcement comparison beneath

**Content specification:**
A single horizontal band runs left to right, representing one container's consumption of one resource. It carries three tick marks: **`0`** at the far left, **`request`** partway along, and **`limit`** further right, with the band continuing past `limit` as a dashed or faded extension. The band is divided into three visually distinct zones. Zone one, from `0` to `request`, is labelled **"reserved for this container"**. Zone two, from `request` to `limit`, is labelled **"allowed IF the node has spare capacity"** and should be rendered with a different fill weight from zone one — it is permitted but not reserved. Zone three, past `limit`, is labelled **"NOT ALLOWED"** and must read as clearly out of bounds. Beneath the band, two leader lines rise to their marks: one under the `0`–`request` zone reading **"read by kube-SCHEDULER (chooses the node)"**, and one under the `limit` mark reading **"enforced by the KUBELET (+ the kernel)"**. Below the band sits a two-row block headed **"ENFORCEMENT DIFFERS BY RESOURCE"**: row one, **`cpu`** → "THROTTLED at the limit (hard, immediate, you get slow)"; row two, **`memory`** → "OOM-KILLED past it (reactive, under node memory pressure — you get slow, then dead)". A final reserved strip at the bottom is labelled **"QoS CLASS: derived from how request and limit were filled in"** and is, in the current draft, deliberately empty of content pending a research fetch. The element that is "the point" is the **`limit` mark** — it is the only boundary in the figure that cannot be crossed, and it is where the two enforcement mechanisms diverge.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1000x620 landscape
- Font: inherit book default (Fira Mono for `cpu`, `memory`, `request`, `limit`, `0`)
- Accent color for highlighted elements: Brass `#B58B3E` on the `limit` tick mark and its boundary rule

**Critical details (non-negotiable accuracy):**
- **A request is a floor, not a ceiling.** Exceeding the request on a node with spare capacity is normal, permitted behaviour — zone two must not be styled as a warning zone.
- **A container is never allowed past its limit.** Zone three is the only out-of-bounds region.
- **The kube-scheduler reads the request** (at placement time, once). **The kubelet, with the kernel, enforces the limit** (continuously, at runtime). These attributions must not be swapped or merged.
- **CPU limits throttle; memory limits kill.** CPU enforcement is hard and immediate — the container keeps running and gets slow, and nothing in the Pod's status changes. Memory enforcement is **reactive**: the kill arrives when the kernel detects memory pressure, not necessarily at the moment the limit is crossed.
- The band depicts **one container's** consumption of **one resource type**. Do not draw multiple containers or stack resource types on one axis.
- The QoS strip must remain a labelled placeholder. Do **not** let the renderer fill in Guaranteed / Burstable / BestEffort definitions — see the blocker below.

**Source ASCII (for designer reference):**
```
A SINGLE CONTAINER'S RESOURCE BAND

  0                request                    limit
  ├──────────────────┤═══════════════════════════┤ ─ ─ ─ ─ ─ ─►
  │                  │                           │
  │   reserved for   │   allowed IF the node     │  NOT ALLOWED
  │   this container │   has spare capacity      │
  │                  │                           │
  └── read by ───────┘                           └── enforced by
      kube-SCHEDULER                                 the KUBELET
      (chooses the node)                             (+ the kernel)

  ENFORCEMENT DIFFERS BY RESOURCE:
     cpu    → THROTTLED at the limit  (hard, immediate, you get slow)
     memory → OOM-KILLED past it      (reactive, under node memory
                                        pressure — you get slow, then dead)

  QoS CLASS: [ derived from how request and limit were filled in ]
             ── see AUTHOR-REVIEW above; unsourced pending research fetch
```

**Proposed filename:** `ch05-fig05-requests-limits-qos-classes.png`

```yaml-figure-spec
anchor_id: ch05-fig05-requests-limits-qos-classes
diagram_type: other
source_ascii: |2
  A SINGLE CONTAINER'S RESOURCE BAND

    0                request                    limit
    ├──────────────────┤═══════════════════════════┤ ─ ─ ─ ─ ─ ─►
    │                  │                           │
    │   reserved for   │   allowed IF the node     │  NOT ALLOWED
    │   this container │   has spare capacity      │
    │                  │                           │
    └── read by ───────┘                           └── enforced by
        kube-SCHEDULER                                 the KUBELET
        (chooses the node)                             (+ the kernel)

    ENFORCEMENT DIFFERS BY RESOURCE:
       cpu    → THROTTLED at the limit  (hard, immediate, you get slow)
       memory → OOM-KILLED past it      (reactive, under node memory
                                          pressure — you get slow, then dead)

    QoS CLASS: [ derived from how request and limit were filled in ]
               ── see AUTHOR-REVIEW above; unsourced pending research fetch
vendor_terms: [kube-scheduler, kubelet, pod, container]
complexity_hint:
  node_count: 8
  edge_count: 4
  label_count: 12
pedagogy:
  part_18_criteria_met: [quantitative_relationships, distinguishing_alternatives, fixed_point]
  learning_outcome: "Choose between a request and a limit for a given requirement, name which component acts on each, and predict that CPU limits throttle while memory limits kill reactively"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the limit tick mark and the boundary rule at it"
accessibility:
  alt_text_seed: "A horizontal band for one container's use of one resource, marked at zero, at the request, and at the limit; the zone up to the request is reserved and read by the kube-scheduler, the zone between request and limit is allowed when the node has spare capacity, and the zone past the limit is not allowed and is enforced by the kubelet with the kernel; a note beneath states that CPU is throttled at the limit while memory is OOM-killed reactively under node memory pressure"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Resource-band abstraction authored by Lodestar from Kubernetes resource-management documentation; no vendor artwork reproduced"
```

**BLOCKER — do not render final art.** Draft line 708 carries a `BLOCKING SOURCE GAP` author-review comment: Quality of Service classes (Guaranteed / Burstable / BestEffort) are absent from the cached source set because `kubernetes.io/docs/concepts/workloads/pods/pod-qos/` was not fetched, and per the Ch 5 outline's Open question #2 they must not be drafted from memory. **The lower strip of this figure is blocked on the same gap.** The upper band (requests, limits, and the two enforcement mechanisms) is fully sourced and stable; the QoS strip is a placeholder. Two consequences for the diagram pipeline: (1) the renderer must not invent QoS content, and (2) the figure's final dimensions will change once the strip is filled, so hold production until the research stage closes the gap. The anchor slug already promises `qos-classes`, so the slug does not need revising when the content lands.

---

## Figure: ch05-zenith-smallest-deployable-unit

**Anchor ID:** `ch05-zenith-smallest-deployable-unit` *(malformed — see MALFORMED ANCHORS above; preserved unrenamed as the join key)*
**Purpose:** The chapter's Zenith figure — collapses six separately-memorised facts into consequences of one design decision, so the reader carries one idea out of the chapter instead of six.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** single-root hierarchy tree (one root claim fanning to six consequences) with one forward-reference branch

**Content specification:**
A single emphasised root box sits centred at the top, containing the chapter's thesis across three lines: **"THE UNIT OF SCHEDULING WRAPS CONTAINERS — IT IS NOT ONE OF THEM."** A single vertical stem descends from it to a horizontal distribution bar, from which six equal-weight branches drop to six leaf boxes arranged left to right. The leaves, in order, read: (1) **"THE POD HAS THE IP"**; (2) **"CONTAINERS REACH EACH OTHER ON `localhost`"**; (3) **"`restartPolicy` is Pod-level"**; (4) **"PHASE is Pod-level; STATE is per-container"**; (5) **"IDENTITY is per-Pod"**; (6) **"SCHEDULE is per-Pod"**. Beneath each leaf, in a lighter weight, sits its section citation: **§1**, **§1,§2**, **§5**, **§5**, **§6**, **§8** respectively. From the first leaf only, a single further line descends and turns right into a wider terminal statement: **"SERVICES WILL SELECT PODS, NOT CONTAINERS  (→ Ch 9)"**. The six leaves must be visually equal to one another — none is more important than the others, because the argument is that all six are the *same* fact wearing six costumes. All the visual weight belongs to the root. This is a Zenith figure: it should feel like an arrival, and it should be readable in about four seconds by someone who has just finished the chapter.

**Visual style:**
- Palette: inherit book default
- Size (pixels): 1200x600 landscape
- Font: inherit book default (Fira Mono for `localhost` and `restartPolicy`; small caps or heavier Fira Sans for the leaf statements)
- Accent color for highlighted elements: Brass `#B58B3E` on the root box border and text — the root only, nowhere else

**Critical details (non-negotiable accuracy):**
- Exactly **one** root and **six** leaves. The forward-reference to Chapter 9 is a seventh statement but hangs off leaf 1, not off the root — it is a consequence of the Pod owning the IP.
- Direction of implication runs **root → leaves**. Every leaf is a consequence of the root, never the other way round. An arrowhead pointing up inverts the chapter's argument.
- The section tags are correct as given and let a reader jump back: §1, §1+§2, §5, §5, §6, §8. Do not renumber them.
- `restartPolicy` and phase are **Pod-level**; state is **per-container**. This leaf compresses the chapter's most-tested distinction into one box and must not be paraphrased into something looser.
- The six leaves are peers. Do not sub-nest them, order them by importance, or vary their box weights.
- The Chapter 9 pointer is a **forward** reference — style it as a forward plant (lighter, arrow-led), not as a seventh consequence of equal standing.

**Source ASCII (for designer reference):**
```
                    ┌───────────────────────────┐
                    │   THE UNIT OF SCHEDULING  │
                    │    WRAPS CONTAINERS —     │
                    │    IT IS NOT ONE OF THEM  │
                    └─────────────┬─────────────┘
                                  │
      ┌───────────┬───────────┬───┴───┬───────────┬───────────┐
      │           │           │       │           │           │
  ┌───▼────┐ ┌────▼─────┐ ┌───▼───┐ ┌─▼──────┐ ┌──▼─────┐ ┌───▼────┐
  │ THE POD│ │CONTAINERS│ │restart│ │ PHASE  │ │IDENTITY│ │SCHEDULE│
  │ HAS THE│ │  REACH   │ │Policy │ │is Pod- │ │is per- │ │ is per-│
  │   IP   │ │EACH OTHER│ │is Pod-│ │ level; │ │  Pod   │ │  Pod   │
  │        │ │ON local- │ │ level │ │STATE is│ │        │ │        │
  │        │ │   host   │ │       │ │per-ctr │ │        │ │        │
  └───┬────┘ └────┬─────┘ └───┬───┘ └───┬────┘ └───┬────┘ └───┬────┘
      §1          §1,§2       §5        §5         §6         §8
      │
      └──────────────► SERVICES WILL SELECT PODS, NOT CONTAINERS  (→ Ch 9)
```

**Proposed filename:** `ch05-zenith-smallest-deployable-unit.png` *(rename to `ch05-fig06-smallest-deployable-unit.png` if and when the author approves the anchor correction — filename and anchor must change together)*

```yaml-figure-spec
anchor_id: ch05-zenith-smallest-deployable-unit
diagram_type: hierarchy_tree
source_ascii: |4
                      ┌───────────────────────────┐
                      │   THE UNIT OF SCHEDULING  │
                      │    WRAPS CONTAINERS —     │
                      │    IT IS NOT ONE OF THEM  │
                      └─────────────┬─────────────┘
                                    │
        ┌───────────┬───────────┬───┴───┬───────────┬───────────┐
        │           │           │       │           │           │
    ┌───▼────┐ ┌────▼─────┐ ┌───▼───┐ ┌─▼──────┐ ┌──▼─────┐ ┌───▼────┐
    │ THE POD│ │CONTAINERS│ │restart│ │ PHASE  │ │IDENTITY│ │SCHEDULE│
    │ HAS THE│ │  REACH   │ │Policy │ │is Pod- │ │is per- │ │ is per-│
    │   IP   │ │EACH OTHER│ │is Pod-│ │ level; │ │  Pod   │ │  Pod   │
    │        │ │ON local- │ │ level │ │STATE is│ │        │ │        │
    │        │ │   host   │ │       │ │per-ctr │ │        │ │        │
    └───┬────┘ └────┬─────┘ └───┬───┘ └───┬────┘ └───┬────┘ └───┬────┘
        §1          §1,§2       §5        §5         §6         §8
        │
        └──────────────► SERVICES WILL SELECT PODS, NOT CONTAINERS  (→ Ch 9)
vendor_terms: [pod, container, service, serviceaccount]
complexity_hint:
  node_count: 8
  edge_count: 7
  label_count: 14
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure]
  learning_outcome: "Explain six separately-taught Pod facts as consequences of one design decision — that the unit of scheduling wraps containers rather than being one"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the root box reading 'THE UNIT OF SCHEDULING WRAPS CONTAINERS — IT IS NOT ONE OF THEM'"
accessibility:
  alt_text_seed: "A tree whose single root reads that the unit of scheduling wraps containers rather than being one, branching to six equal consequences: the Pod has the IP, containers reach each other on localhost, restartPolicy is Pod-level, phase is Pod-level while state is per-container, identity is per-Pod, and scheduling is per-Pod; a further branch from the first leaf notes that Services will select Pods, not containers, in Chapter 9"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Synthesis diagram authored entirely by Lodestar; the argument structure is our own, not reproduced from any vendor source"
```

---

## Handoff summary for the diagram pipeline

| Anchor | Type | Router target | Status |
|---|---|---|---|
| `ch05-fig01-pod-shared-network-namespace` | `k8s_architecture` | D2 | ready |
| `ch05-fig03-init-containers-sequence` | `activity` | Mermaid | hold — untagged source at draft L216 |
| `ch05-fig02-pod-phases-and-container-states` | `state_machine` | Mermaid | ready |
| `ch05-fig04-three-probes-compared` | `other` | D2 fallback | ready |
| `ch05-fig05-requests-limits-qos-classes` | `other` | D2 fallback | **BLOCKED** — QoS source gap, draft L708 |
| `ch05-zenith-smallest-deployable-unit` | `hierarchy_tree` | D2 | ready — anchor ID malformed, author decision pending |

Three of six figures are clear to render now. One is held pending a source tag that is unlikely to change its content. One is hard-blocked on a research fetch that will change its dimensions. One is clear to render but carries an anchor ID that should be corrected in the draft and here in the same edit.

**RESOLVED 2026-08-24 (author review):** `ch05-zenith-smallest-deployable-unit` is the arc outline's prescribed Zenith form (precedent: ch02-zenith-standard-crate). The fig06 rename proposal above is struck; keep the zenith anchor.

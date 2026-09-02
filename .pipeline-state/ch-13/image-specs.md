# Image Specifications — KCNA Chapter 13

*Generated from draft-v1.md (draft-voice.md does not exist at this stage; positions are cited by section rather than line number). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Anchor inventory:** 7 anchors, 7 ASCII diagrams, 7 entries. No unanchored diagrams.

**Entries below appear in draft order, not numeric order.** The draft's `figMM` numbering is out of sequence: `fig04` (metrics pipeline) appears in §7, after `fig05` (§4) and `fig06` (§5). Anchor IDs are preserved exactly as authored — renumbering is an author-review decision, not this stage's. Flagged below.

---

## ANCHOR FORMAT EXCEPTIONS

Rule 4 requires `ch{NN}-fig{MM}-{kebab-slug}`. One anchor does not conform:

| Anchor as written | Location | Problem | Suggested |
|---|---|---|---|
| `ch13-zenith-read-the-phase-first` | §8 (☀️ Zenith section) | No `fig{MM}` segment — uses `zenith` where the figure number belongs. Will not sort or join with the rest of the chapter's figures in the book-level index. | `ch13-fig07-zenith-read-the-phase-first` — author to confirm; if approved, the draft anchor must be edited in the same pass so the join key stays consistent. |

Second, non-blocking observation for the same author-review pass: `ch13-fig04-metrics-pipeline-and-metrics-server` is the sixth figure in reading order. If the chapter's figures are ever renumbered to match reading order, `fig04` ↔ `fig05` ↔ `fig06` all move. Until then, **do not** assume figure number implies position.

---

## UNANCHORED DIAGRAMS

None.

Six fenced code blocks in the draft carry no figure anchor and correctly should not: they are command listings, not diagrams. Recorded here so the structural audit can reconcile the count of fenced blocks (13) against the count of figures (7).

- §3 — `kubectl describe pod <pod-name>`
- §3 — `kubectl events --for pod/<pod-name>` / `kubectl get events --sort-by=...`
- §3 — the four `kubectl logs` invocations
- §5 — `kubectl get nodes` / `kubectl describe node <node-name>`
- §5 — `crictl ps` / `crictl logs <id>`
- §7 — `kubectl top pod myapp`

---

## Figure: ch13-fig01-two-audience-split

**Anchor ID:** `ch13-fig01-two-audience-split`
**Purpose:** Establishes the chapter's governing boundary — platform scope versus application scope — and the single one-way test that tells the reader which side of it they are on.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-column comparison with a single directional handoff arrow

**Content specification:**
Two vertical columns of equal width, side by side, separated by generous whitespace (no dividing rule — the whitespace is the divider). The left column is headed **PLATFORM SCOPE** with the subhead *(this chapter)* beneath it in smaller type; the right column is headed **APPLICATION SCOPE** with the subhead *(Chapter 16)*. Under each heading sits a list of five questions, set as plain lines with no bullets, vertically aligned row-for-row so that each left question sits at the same baseline as its right counterpart. Left column, top to bottom: "Did the Pod get scheduled?", "Did the image pull?", "Did the container start?", "Is the node healthy?", "Did something kill it?". Right column, top to bottom: "Is the process doing the right thing?", "Is it reading the right config?", "Is it reaching its dependencies?", "Is it returning correct results?", "Is it selected by its Service?". Below both lists, a single arrow runs **from the left column to the right column and only in that direction**: it descends from beneath the left column, travels horizontally right, and terminates in an arrowhead pointing **upward** into the base of the right column. The label riding on that arrow, set in quotation marks across two lines, reads: *"the Pod is Running and Ready, and the behavior is still wrong"*. That arrow and its label are the point of the figure — everything else is context for it.

**Visual style:**
- Palette: inherit book default (brand navy line-art on paper white)
- Size (pixels): 1200x620 landscape
- Font: inherit book default (Fira Sans for labels; Fira Mono for the code-ish tokens `Running` and `Ready` inside the arrow label)
- Accent color for highlighted elements: Brass `#B58B3E` on the handoff arrow and its label only
- Glyph policy: **glyph-free.** This is not a stack or pipeline figure; per the 2026-08-25 semantic-glyph decision, no Lucide glyphs.

**Critical details (non-negotiable accuracy):**
- The arrow is **one-way, left to right.** An investigation crosses from platform scope into application scope; it never crosses back. A double-headed arrow inverts the chapter's argument.
- The left column is PLATFORM and the right is APPLICATION — not reversed. The book reads left-to-right as "first, then."
- The arrow's condition is a **conjunction of three things**: `Running` AND `Ready` AND behavior still wrong. Dropping `Ready` makes the test wrong.
- Five questions per column, paired row-for-row. Do not add, drop, or reorder them.
- No box or border around either column. The columns are lists, not containers; boxing them implies a system boundary that does not exist.

**Source ASCII (for designer reference):**
```
        PLATFORM SCOPE                    APPLICATION SCOPE
        (this chapter)                    (Chapter 16)

   Did the Pod get scheduled?        Is the process doing the right thing?
   Did the image pull?               Is it reading the right config?
   Did the container start?          Is it reaching its dependencies?
   Is the node healthy?              Is it returning correct results?
   Did something kill it?            Is it selected by its Service?

        │                                         ▲
        │      "the Pod is Running and Ready,     │
        └──────  and the behavior is still  ──────┘
                       wrong"
```

**Proposed filename:** `ch13-fig01-two-audience-split.png`

```yaml-figure-spec
anchor_id: ch13-fig01-two-audience-split
diagram_type: concept_map
source_ascii: |5
          PLATFORM SCOPE                    APPLICATION SCOPE
          (this chapter)                    (Chapter 16)

     Did the Pod get scheduled?        Is the process doing the right thing?
     Did the image pull?               Is it reading the right config?
     Did the container start?          Is it reaching its dependencies?
     Is the node healthy?              Is it returning correct results?
     Did something kill it?            Is it selected by its Service?

          │                                         ▲
          │      "the Pod is Running and Ready,     │
          └──────  and the behavior is still  ──────┘
                         wrong"
vendor_terms: []
complexity_hint:
  node_count: 12
  edge_count: 1
  label_count: 13
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure]
  learning_outcome: "Decide whether a failure is the platform's problem or the application's before spending time on either"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the one-way handoff arrow and its 'Running and Ready, and still wrong' label"
accessibility:
  alt_text_seed: "Two columns of diagnostic questions side by side, platform scope on the left and application scope on the right, joined by a single arrow that runs only from left to right, labelled with the condition that the Pod is Running and Ready and the behavior is still wrong"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic diagnostic questions; names API object kinds only, reproduces no vendor mark, logo, or icon."
```

---

## Figure: ch13-fig02-pod-failure-signature-map

**Anchor ID:** `ch13-fig02-pod-failure-signature-map`
**Purpose:** Converts the never-started failure family from a list of error strings into a decision tree keyed on questions the reader can actually ask the cluster, so an unfamiliar signature still lands in the right branch.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** top-down decision tree (binary at the root, then three-way at the leaf level)

**Content specification:**
A top-down tree. The root is a question, not a state: **"Does the Pod object exist?"**, set in a box at top center. Two branches descend from it, labelled **NO** (left) and **YES** (right). The NO branch terminates immediately in a leaf reading "Admission refused it. Read the CREATE error, not the Pod." with a smaller cross-reference line beneath: *(Ch 12 §6)*. The YES branch descends into a second question node, **"What's the phase?"**, which splits two ways: **Pending** (left) and **Running** (right, with the qualifier *(containers Waiting)* set beneath it in smaller type). Under **Pending** sits the leaf "Not scheduled yet. Read: describe → Events from the scheduler." with cross-references *(Ch 7 §2, §4)* — note the source ASCII places those references in the leftmost leaf column; the designer should attach them to the Pending leaf where they belong. Under **Running / containers Waiting** sits "Scheduled; can't start. Read: container Reason", which fans out into a three-way split of container-state reasons, left to right: (1) `ErrImagePull` / `ImagePullBackOff` → "Registry said no, or was never asked properly." *(Ch 2 §3, §6)*; (2) `CreateContainerConfigError` → "Named ConfigMap or Secret doesn't exist." *(Ch 4 §4)*; (3) `ImageInspectError` / `ErrImageNeverPull` → "Image is broken, or policy Never with no local image." *(Ch 2 §6)*. All signature strings are set in monospace; all explanatory text in the body face; all chapter cross-references in a smaller, lighter weight. The root question is the emphasized element — it is the branch everyone skips.

**Visual style:**
- Palette: inherit book default (brand navy line-art)
- Size (pixels): 1200x820 landscape
- Font: inherit book default; Fira Mono for every signature string, Fira Sans for prose, Fira Sans small/light for `(Ch N §M)` references
- Accent color for highlighted elements: Brass `#B58B3E` on the root node "Does the Pod object exist?" and its NO branch
- Glyph policy: **glyph-free.** Decision-tree family.

**Critical details (non-negotiable accuracy):**
- The root question is about the **existence of the Pod object**, not about the error. Rewriting the root as "What's the error?" destroys the figure's argument.
- The NO branch must make clear there is **no Pod to describe** — the reader is sent to the CREATE response, not to `kubectl describe pod`.
- `ErrImagePull` and `ImagePullBackOff` sit in **one** leaf together. They are the same diagnosis at two moments, not two branches.
- `CreateContainerConfigError` hangs off the **Running / containers Waiting** side, not off `Pending`. The Pod was scheduled and the image pulled; only configuration failed.
- The phase split is `Pending` versus `Running (containers Waiting)`. Do not label the right branch simply "Running" without the qualifier — a plain `Running` Pod is not in this tree at all.
- Spell the signature strings exactly, including capitalization: `ErrImagePull`, `ImagePullBackOff`, `CreateContainerConfigError`, `ImageInspectError`, `ErrImageNeverPull`.

**Source ASCII (for designer reference):**
```
                    Does the Pod object exist?
                              │
              ┌───────────────┴───────────────┐
              NO                              YES
              │                                │
    Admission refused it.                 What's the phase?
    Read the CREATE error,                     │
    not the Pod.                    ┌──────────┴──────────┐
    (Ch 12 §6)                   Pending                Running
                                    │                  (containers Waiting)
                          Not scheduled yet.                 │
                          Read: describe → Events    Scheduled; can't start.
                          from the scheduler.        Read: container Reason
                                                            │
                              ┌─────────────────────────────┼────────────────────┐
                     ErrImagePull /                CreateContainerConfigError    ImageInspectError /
                     ImagePullBackOff                        │                   ErrImageNeverPull
                              │                    Named ConfigMap or Secret            │
                    Registry said no, or               doesn't exist.            Image is broken, or
                    was never asked properly.          (Ch 4 §4)                 policy Never with no
                    (Ch 2 §3, §6)                                                local image. (Ch 2 §6)
```

**Proposed filename:** `ch13-fig02-pod-failure-signature-map.png`

```yaml-figure-spec
anchor_id: ch13-fig02-pod-failure-signature-map
diagram_type: flowchart
source_ascii: |6
                      Does the Pod object exist?
                                │
                ┌───────────────┴───────────────┐
                NO                              YES
                │                                │
      Admission refused it.                 What's the phase?
      Read the CREATE error,                     │
      not the Pod.                    ┌──────────┴──────────┐
      (Ch 12 §6)                   Pending                Running
                                      │                  (containers Waiting)
                            Not scheduled yet.                 │
                            Read: describe → Events    Scheduled; can't start.
                            from the scheduler.        Read: container Reason
                                                              │
                                ┌─────────────────────────────┼────────────────────┐
                       ErrImagePull /                CreateContainerConfigError    ImageInspectError /
                       ImagePullBackOff                        │                   ErrImageNeverPull
                                │                    Named ConfigMap or Secret            │
                      Registry said no, or               doesn't exist.            Image is broken, or
                      was never asked properly.          (Ch 4 §4)                 policy Never with no
                      (Ch 2 §3, §6)                                                local image. (Ch 2 §6)
vendor_terms: [kubectl, configmap, secret]
complexity_hint:
  node_count: 11
  edge_count: 10
  label_count: 16
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Route an unfamiliar never-started failure to the correct cause family by asking two questions in order"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the root node 'Does the Pod object exist?' and its NO branch"
accessibility:
  alt_text_seed: "A decision tree beginning with the question of whether the Pod object exists; the No branch leads to admission refusal, and the Yes branch splits by phase into Pending, meaning not scheduled, and Running with containers waiting, which fans out into the image-pull, configuration, and image-policy failure reasons"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes container-state reason strings and object kinds, redrawn as an original decision tree; no CNCF artwork reproduced."
```

---

## Figure: ch13-fig03-phase-before-logs-flow

**Anchor ID:** `ch13-fig03-phase-before-logs-flow`
**Purpose:** Gives the chapter's triage order a spatial form — five stages, each with the commands that serve it and the question it answers — so that "logs last" is visible as a position rather than asserted as advice.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** vertical staged flow, three columns (stage name / commands / question answered)

**Content specification:**
Five stages stacked vertically, connected top to bottom by a single spine of downward arrows. Each stage occupies one row divided into three columns. Column one holds the stage name in small caps: **SCOPE**, **PHASE**, **CONDITIONS**, **EVENTS**, **LOGS**, in that order top to bottom. Column two holds the commands for that stage, in monospace, one or two lines per stage: SCOPE → `kubectl config current-context`; PHASE → `kubectl get pods` and `kubectl get pod <name> -o wide`; CONDITIONS → `kubectl describe pod <name>` and `kubectl describe node <node>`; EVENTS → `kubectl events --for pod/<name>` and `kubectl get events --sort-by=...`; LOGS → `kubectl logs <name> -c <container>` and `kubectl logs <name> --previous`. Column three holds the question each stage answers, in the body face: SCOPE → "Right cluster? Right namespace?"; PHASE → "Pending? Running? Restarts > 0?" and "Which node? Which IP?"; CONDITIONS → "Container state + Reason." and "Node conditions, if suspect."; EVENTS → "What did the components SAY?" and "Chronology, when object unknown."; LOGS → "Only meaningful once you know the container actually ran." The arrows run only downward, in the left margin, connecting stage to stage. The LOGS row is the emphasized element: it sits last, and its right-hand caption is the reason it sits last.

**Visual style:**
- Palette: inherit book default (brand navy line-art)
- Size (pixels): 1200x800 landscape
- Font: inherit book default; Fira Mono for column two throughout, Fira Sans small caps for the stage names, Fira Sans for column three
- Accent color for highlighted elements: Brass `#B58B3E` on the LOGS row (stage name and its right-hand caption)
- Glyph policy: **glyph-free.** Staged-flow family, not the pipeline family — no Lucide glyphs.

**Critical details (non-negotiable accuracy):**
- Order is fixed and load-bearing: **SCOPE → PHASE → CONDITIONS → EVENTS → LOGS.** Reordering any stage contradicts the chapter and the S-P-C-E-L mnemonic that names it.
- LOGS is **last**. This is the whole figure.
- `--previous` must appear in the LOGS row. It is the flag the chapter builds a Fixed Point around.
- Arrows point downward only. This is a narrowing sequence, not a cycle.
- Commands must be transcribed exactly, including the placeholder angle brackets `<name>`, `<node>`, `<container>` and the `-o wide`, `-c`, `--for pod/`, `--sort-by=` fragments.
- Do not merge columns two and three. The separation of "what you type" from "what it tells you" is the reason the figure is three columns wide.

**Source ASCII (for designer reference):**
```
  SCOPE      kubectl config current-context      Right cluster? Right namespace?
    │
    ▼
  PHASE      kubectl get pods                    Pending? Running? Restarts > 0?
    │        kubectl get pod <name> -o wide      Which node? Which IP?
    ▼
CONDITIONS   kubectl describe pod <name>         Container state + Reason.
    │        kubectl describe node <node>        Node conditions, if suspect.
    ▼
  EVENTS     kubectl events --for pod/<name>     What did the components SAY?
    │        kubectl get events --sort-by=...    Chronology, when object unknown.
    ▼
   LOGS      kubectl logs <name> -c <container>  Only meaningful once you know
             kubectl logs <name> --previous      the container actually ran.
```

**Proposed filename:** `ch13-fig03-phase-before-logs-flow.png`

```yaml-figure-spec
anchor_id: ch13-fig03-phase-before-logs-flow
diagram_type: flowchart
source_ascii: |2
    SCOPE      kubectl config current-context      Right cluster? Right namespace?
      │
      ▼
    PHASE      kubectl get pods                    Pending? Running? Restarts > 0?
      │        kubectl get pod <name> -o wide      Which node? Which IP?
      ▼
  CONDITIONS   kubectl describe pod <name>         Container state + Reason.
      │        kubectl describe node <node>        Node conditions, if suspect.
      ▼
    EVENTS     kubectl events --for pod/<name>     What did the components SAY?
      │        kubectl get events --sort-by=...    Chronology, when object unknown.
      ▼
     LOGS      kubectl logs <name> -c <container>  Only meaningful once you know
               kubectl logs <name> --previous      the container actually ran.
vendor_terms: [kubectl]
complexity_hint:
  node_count: 5
  edge_count: 4
  label_count: 15
pedagogy:
  part_18_criteria_met: [temporal_structure, spatial_structure]
  learning_outcome: "Run the triage commands in the order that narrows the problem, with logs last"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the LOGS stage in final position, with its 'only meaningful once you know the container ran' caption"
accessibility:
  alt_text_seed: "A five-stage vertical sequence — scope, phase, conditions, events, logs — each stage listing its kubectl commands and the question those commands answer, with logs in the final position"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "kubectl command invocations and object kinds; original layout, no CNCF artwork."
```

---

## Figure: ch13-fig05-oomkilled-vs-evicted

**Anchor ID:** `ch13-fig05-oomkilled-vs-evicted`
**Purpose:** Separates the chapter's most confusable pair by walking both failures down parallel tracks that disagree at every one of four steps, so the reader remembers a divergence rather than two definitions.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** parallel two-track comparison flow (two vertical chains, aligned row-for-row)

**Content specification:**
Two vertical chains side by side, each with its own heading and each descending through five aligned stages. The left chain is headed **OOMKilled**; the right chain is headed **Evicted**. Each heading carries a short horizontal rule directly beneath it (as in the source ASCII). The two chains are aligned row-for-row so the reader's eye can travel horizontally to compare at each stage, and each chain is connected internally by downward arrows. Row 1 — trigger: left, "Container exceeds ITS OWN limit"; right, "NODE runs low on a resource". Row 2 — actor: left, "Kernel cgroup enforcement kills that one process"; right, "kubelet chooses victims by QoS class and terminates Pods". Row 3 — what you see: left, "Container state: Terminated / Reason: OOMKilled"; right, "Pod phase: Failed / Reason: Evicted". Row 4 — outcome: left, "Restarted IN PLACE on the same node, per restartPolicy. Restart count increments."; right, "Pod is GONE from this node. A controller creates a REPLACEMENT elsewhere." Row 5 — the summary axes, set apart from the flow: left, "Scope: ONE container" and "Trigger: this Pod's own limit"; right, "Scope: THE WHOLE POD" and "Trigger: the node's pressure". Words the source sets in capitals (ITS OWN, NODE, IN PLACE, GONE, REPLACEMENT, ONE, THE WHOLE POD) must retain that emphasis, rendered as small caps or bold rather than shouted capitals if the house style prefers. The final row is the emphasized element — it is the pair of statements the exam tests.

**Visual style:**
- Palette: inherit book default (brand navy line-art)
- Size (pixels): 960x1200 portrait (authored near 3:4 so it does not scale down to unreadable type on a 6-inch screen)
- Font: inherit book default; Fira Mono for `OOMKilled`, `Evicted`, `Terminated`, `Failed`, `restartPolicy`; Fira Sans elsewhere
- Accent color for highlighted elements: Brass `#B58B3E` on the final Scope/Trigger row of both chains
- Glyph policy: **glyph-free.** Comparison family.

**Critical details (non-negotiable accuracy):**
- The killers are different and must not be blurred: **the kernel** (cgroup enforcement) kills on OOM; **the kubelet** evicts under node pressure.
- The triggers are different: OOMKilled is triggered by **the container's own limit**; eviction is triggered by **the node's** resource pressure.
- The scopes are different: OOMKilled is **one container**; eviction is **the whole Pod**.
- The outcomes are different: OOMKilled restarts **in place on the same node** and increments the restart count; an evicted Pod is **gone from that node** and a controller creates a **new, different** Pod elsewhere. The evicted Pod is never moved — Kubernetes does not relocate a Pod.
- The reporting surfaces differ and must be labelled precisely: `OOMKilled` is a **container state** reason (`Terminated`); `Evicted` accompanies a **Pod phase** of `Failed`.
- The two chains must stay visually parallel and row-aligned. Staggering them defeats the comparison.

**Source ASCII (for designer reference):**
```
        OOMKilled                              Evicted
        ─────────                              ───────

  Container exceeds ITS OWN limit        NODE runs low on a resource
              │                                    │
              ▼                                    ▼
  Kernel cgroup enforcement kills        kubelet chooses victims by
  that one process                       QoS class and terminates Pods
              │                                    │
              ▼                                    ▼
  Container state: Terminated            Pod phase: Failed
  Reason: OOMKilled                      Reason: Evicted
              │                                    │
              ▼                                    ▼
  Restarted IN PLACE on the              Pod is GONE from this node.
  same node, per restartPolicy.          A controller creates a
  Restart count increments.              REPLACEMENT elsewhere.
              │                                    │
              ▼                                    ▼
  Scope: ONE container                   Scope: THE WHOLE POD
  Trigger: this Pod's own limit          Trigger: the node's pressure
```

**Proposed filename:** `ch13-fig05-oomkilled-vs-evicted.png`

```yaml-figure-spec
anchor_id: ch13-fig05-oomkilled-vs-evicted
diagram_type: flowchart
source_ascii: |4
          OOMKilled                              Evicted
          ─────────                              ───────

    Container exceeds ITS OWN limit        NODE runs low on a resource
                │                                    │
                ▼                                    ▼
    Kernel cgroup enforcement kills        kubelet chooses victims by
    that one process                       QoS class and terminates Pods
                │                                    │
                ▼                                    ▼
    Container state: Terminated            Pod phase: Failed
    Reason: OOMKilled                      Reason: Evicted
                │                                    │
                ▼                                    ▼
    Restarted IN PLACE on the              Pod is GONE from this node.
    same node, per restartPolicy.          A controller creates a
    Restart count increments.              REPLACEMENT elsewhere.
                │                                    │
                ▼                                    ▼
    Scope: ONE container                   Scope: THE WHOLE POD
    Trigger: this Pod's own limit          Trigger: the node's pressure
vendor_terms: [kubelet]
complexity_hint:
  node_count: 10
  edge_count: 8
  label_count: 12
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure]
  learning_outcome: "Distinguish OOMKilled from Evicted by killer, scope, trigger, and outcome"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the final row: Scope one container versus the whole Pod, Trigger own limit versus node pressure"
accessibility:
  alt_text_seed: "Two parallel vertical chains compared row by row: OOMKilled, where a container exceeds its own limit and the kernel kills it and the kubelet restarts it in place, against Evicted, where the node runs low on a resource and the kubelet terminates the whole Pod so a controller replaces it elsewhere"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 960
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes reason strings and kubelet behavior, redrawn as an original comparison; no CNCF artwork."
```

---

## Figure: ch13-fig06-diagnostic-layer-stack

**Anchor ID:** `ch13-fig06-diagnostic-layer-stack`
**Purpose:** Locates `crictl` below the API boundary, so the reader understands it as a different vantage point — the node's own view — rather than as a more powerful `kubectl`.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** layered stack diagram with an emphasized boundary rule and marginal annotations

**Content specification:**
A single vertical stack of five stacked cells, drawn as one bordered column subdivided by horizontal rules, from top to bottom: **kubectl** *[terminal]*, **kube-apiserver** *[server]*, **kubelet** *[agent]*, **CRI** *[contract]*, **containerd / CRI-O** *[runtime]*. Each cell carries its component name flush left and its role tag flush right in brackets, in smaller, lighter type. The rule between **kubelet** and **CRI** is drawn differently from the others — heavier, or doubled — and is labelled in the right margin as **the API boundary**, with an arrow pointing at it. Two further right-margin annotations sit outside the stack: one spanning the top three cells reading "Everything above this line is the cluster's RECORDED view of itself."; one pointing at the bottom cell reading "crictl attaches HERE, to the runtime directly, bypassing everything above." The heavy boundary rule is the point of the figure; the annotations exist to explain it.

**Visual style:**
- Palette: inherit book default (brand navy line-art)
- Size (pixels): 1200x560 landscape
- Font: inherit book default; Fira Mono for `kubectl`, `kube-apiserver`, `kubelet`, `CRI`, `containerd`, `CRI-O`, `crictl`; Fira Sans for annotations and role tags
- Accent color for highlighted elements: Brass `#B58B3E` on the API-boundary rule and the `crictl attaches HERE` annotation
- Glyph policy: **stack family — semantic Lucide glyphs apply.** Per the 2026-08-25 decision, one glyph per layer drawn from `certcomp-diagrams/assets/glyph-ledger.yaml`; one glyph, one meaning, series-wide. Do not invent glyphs outside the ledger; if a layer has no ledger entry, leave that layer glyph-free rather than improvising.

**Critical details (non-negotiable accuracy):**
- Layer order top to bottom is **kubectl → kube-apiserver → kubelet → CRI → containerd/CRI-O.** Inverting the stack or swapping the kubelet and the API server misstates the architecture.
- The API boundary sits **between kubelet and CRI** — not between kubectl and kube-apiserver, and not between CRI and the runtime.
- **CRI is a contract, not a process.** Its role tag must read `[contract]`; drawing it as a daemon or a server is wrong.
- `containerd / CRI-O` are alternatives on one layer, not two stacked layers. Keep them in a single cell separated by a slash.
- `crictl` attaches to the **runtime**, and the arrow must land at the bottom cell, not at CRI and not at the kubelet.
- The stack is a layering, not a message sequence. Do not add request/response arrows between cells.

**Source ASCII (for designer reference):**
```
   ┌──────────────────────────────────────────────┐
   │  kubectl                          [terminal] │   Everything above this
   ├──────────────────────────────────────────────┤   line is the cluster's
   │  kube-apiserver                     [server] │   RECORDED view of itself.
   ├──────────────────────────────────────────────┤
   │  kubelet                             [agent] │
   ═══════════════════════════════════════════════   ◄── the API boundary
   │  CRI                              [contract] │
   ├──────────────────────────────────────────────┤   crictl attaches HERE,
   │  containerd / CRI-O               [runtime]  │ ◄── to the runtime directly,
   └──────────────────────────────────────────────┘   bypassing everything above.
```

**Proposed filename:** `ch13-fig06-diagnostic-layer-stack.png`

```yaml-figure-spec
anchor_id: ch13-fig06-diagnostic-layer-stack
diagram_type: component_diagram
source_ascii: |
     ┌──────────────────────────────────────────────┐
     │  kubectl                          [terminal] │   Everything above this
     ├──────────────────────────────────────────────┤   line is the cluster's
     │  kube-apiserver                     [server] │   RECORDED view of itself.
     ├──────────────────────────────────────────────┤
     │  kubelet                             [agent] │
     ═══════════════════════════════════════════════   ◄── the API boundary
     │  CRI                              [contract] │
     ├──────────────────────────────────────────────┤   crictl attaches HERE,
     │  containerd / CRI-O               [runtime]  │ ◄── to the runtime directly,
     └──────────────────────────────────────────────┘   bypassing everything above.
vendor_terms: [kubectl, kube-apiserver, kubelet, cri, containerd, cri-o, crictl]
complexity_hint:
  node_count: 5
  edge_count: 2
  label_count: 8
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Recognize when to drop below the Kubernetes API to crictl, and what question that answers"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the doubled API-boundary rule between kubelet and CRI"
accessibility:
  alt_text_seed: "A five-layer stack from kubectl at the top through kube-apiserver and kubelet, then a heavy rule marking the API boundary, then CRI and the containerd or CRI-O runtime at the bottom, annotated to show that everything above the boundary is the cluster's recorded view and that crictl attaches directly to the runtime below it"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes and CNCF project names (containerd, CRI-O, crictl) as text labels only; layering redrawn in house style, no vendor logos."
```

---

## Figure: ch13-fig04-metrics-pipeline-and-metrics-server

**Anchor ID:** `ch13-fig04-metrics-pipeline-and-metrics-server`
**Purpose:** Shows that every part of the resource-metrics pipeline is already running except the one addon nobody installed, which is why `kubectl top` fails on a healthy cluster.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** vertical data-flow pipeline with one deliberately absent (dashed) stage

**Content specification:**
A pipeline reading top to bottom. The top band holds three boxes in a horizontal row, connected left to right by solid arrows: **container runtime** → **cAdvisor** → **kubelet**. A right-margin annotation for that band reads "in the kubelet binary, on EVERY node, always present". From the kubelet box a single arrow descends, labelled `/metrics/resource`, into the next stage: **metrics-server (cluster addon)**, which is drawn **with a dashed border** — the only dashed element in the figure — and annotated in the right margin with "NOT INSTALLED BY DEFAULT. This gap is the whole reason `kubectl top` fails." From metrics-server a further arrow descends, labelled `metrics.k8s.io`, into a solid box: **API server**. From the API server, two arrows fan out downward to two consumer boxes side by side: **HPA** (left) and **kubectl top** (right). Every box except metrics-server is solid-bordered, signalling "already present on your cluster"; metrics-server alone is dashed, signalling "absent". The dashed box is the emphasized element and the reason the figure exists.

**Visual style:**
- Palette: inherit book default (brand navy line-art)
- Size (pixels): 900x1200 portrait (authored near 3:4 so the labels survive small-screen reflow)
- Font: inherit book default; Fira Mono for `/metrics/resource`, `metrics.k8s.io`, `kubectl top`, `metrics-server`, `cAdvisor`; Fira Sans for annotations
- Accent color for highlighted elements: Brass `#B58B3E` on the dashed metrics-server box, its border, and its "NOT INSTALLED BY DEFAULT" annotation
- Glyph policy: **pipeline family — semantic Lucide glyphs apply.** One glyph per stage from `certcomp-diagrams/assets/glyph-ledger.yaml`, one glyph one meaning series-wide. The dashed metrics-server stage takes its glyph in the same dashed/ghosted treatment as its box, so absence reads consistently.

**Critical details (non-negotiable accuracy):**
- **metrics-server is the only dashed box.** Dashing anything else, or drawing metrics-server solid, inverts the lesson.
- cAdvisor is **inside the kubelet binary** — the annotation must make that clear. Do not draw cAdvisor as a separately installed component.
- The edge labels are the API surfaces and must be exact: `/metrics/resource` between kubelet and metrics-server; `metrics.k8s.io` between metrics-server and the API server.
- Both consumers — **HPA** and **kubectl top** — read through the **API server**, not directly from the kubelet or from metrics-server. Drawing either consumer straight to a kubelet is wrong and undoes the section's HPA point.
- Flow direction is one-way, upward through the stack of components and downward on the page: runtime → cAdvisor → kubelet → metrics-server → API server → consumers.
- Spell it `metrics-server` (hyphenated, lowercase) and `cAdvisor` (lowercase c, capital A).

**Source ASCII (for designer reference):**
```
  ┌───────────┐   ┌──────────┐   ┌─────────┐
  │ container │──▶│ cAdvisor │──▶│ kubelet │   in the kubelet binary,
  │  runtime  │   │          │   │         │   on EVERY node, always present
  └───────────┘   └──────────┘   └────┬────┘
                                      │  /metrics/resource
                                      ▼
                         ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
                            metrics-server        ◄── NOT INSTALLED BY DEFAULT.
                         │  (cluster addon)     │      This gap is the whole
                         └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘      reason `kubectl top` fails.
                                      │  metrics.k8s.io
                                      ▼
                              ┌───────────────┐
                              │  API server   │
                              └───┬───────┬───┘
                                  │       │
                          ┌───────▼──┐  ┌─▼──────────┐
                          │   HPA    │  │kubectl top │
                          └──────────┘  └────────────┘
```

**Proposed filename:** `ch13-fig04-metrics-pipeline-and-metrics-server.png`

```yaml-figure-spec
anchor_id: ch13-fig04-metrics-pipeline-and-metrics-server
diagram_type: data_flow
source_ascii: |
    ┌───────────┐   ┌──────────┐   ┌─────────┐
    │ container │──▶│ cAdvisor │──▶│ kubelet │   in the kubelet binary,
    │  runtime  │   │          │   │         │   on EVERY node, always present
    └───────────┘   └──────────┘   └────┬────┘
                                        │  /metrics/resource
                                        ▼
                           ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
                              metrics-server        ◄── NOT INSTALLED BY DEFAULT.
                           │  (cluster addon)     │      This gap is the whole
                           └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘      reason `kubectl top` fails.
                                        │  metrics.k8s.io
                                        ▼
                                ┌───────────────┐
                                │  API server   │
                                └───┬───────┬───┘
                                    │       │
                            ┌───────▼──┐  ┌─▼──────────┐
                            │   HPA    │  │kubectl top │
                            └──────────┘  └────────────┘
vendor_terms: [kubelet, cadvisor, metrics-server, kube-apiserver, kubectl, hpa]
complexity_hint:
  node_count: 7
  edge_count: 6
  label_count: 10
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "Explain why kubectl top fails on a stock cluster: every stage exists except the metrics-server addon"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the dashed metrics-server box marked NOT INSTALLED BY DEFAULT"
accessibility:
  alt_text_seed: "A metrics pipeline flowing from the container runtime through cAdvisor to the kubelet, then over the slash metrics slash resource endpoint to a metrics-server box drawn with a dashed border and marked not installed by default, then over metrics.k8s.io to the API server, which serves both the horizontal pod autoscaler and kubectl top"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 900
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "CNCF component names as text labels; pipeline redrawn in house style from the documented resource metrics pipeline, no CNCF artwork reproduced."
```

---

## Figure: ch13-zenith-read-the-phase-first

**Anchor ID:** `ch13-zenith-read-the-phase-first` *(non-conforming — see ANCHOR FORMAT EXCEPTIONS above; preserved verbatim as the join key)*
**Purpose:** The chapter's synthesis figure: collapses nine memorized error strings into one lookup keyed on the phase, so the reader leaves with a method rather than a glossary.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hierarchical tree, one root fanning to four terminal signature groups

**Content specification:**
A single root at top center reading **ONE KEY: the phase**, from which the whole tree descends. Four branches fan out beneath it. Branch 1: **no Pod object** → "the ADMISSION gate stopped it" → "read the CREATE response" with the cross-reference *(Ch 12 §6)*; this branch has no signature leaf. Branch 2: **Pending** → "the SCHEDULER never placed it" → "read the SCHEDULER's events" with *(Ch 7 §2, §4)*; also no signature leaf. Branches 3 and 4 both descend from an intermediate node reading **scheduled to a node**, which splits into "containers never ran" (left) and "containers ran, then ended" (right). The never-ran branch continues: "the KUBELET couldn't start it" → a leaf list of five signatures in monospace: `ErrImagePull`, `ImagePullBackOff`, `ImageInspectError`, `ErrImageNeverPull`, `CreateContainerConfigError`. The ran-then-ended branch continues: "the KUBELET or the KERNEL ended it" → a leaf list of four items: `CrashLoopBackOff`, `OOMKilled`, `Evicted`, and "probe failures" (the last in the body face, since it is a category rather than a signature string). A closing caption sits centered below the tree, set apart: **"Nine signatures. One lookup. The key is always the phase."** The root node is the emphasized element.

**Visual style:**
- Palette: inherit book default (brand navy line-art)
- Size (pixels): 1200x850 landscape
- Font: inherit book default; Fira Mono for all nine signature strings, Fira Sans for the tree's prose nodes, Fira Sans italic or small caps for the closing caption
- Accent color for highlighted elements: Brass `#B58B3E` on the root node "ONE KEY: the phase" and the closing caption
- Glyph policy: **glyph-free.** Hierarchy family, not stack or pipeline.

**Critical details (non-negotiable accuracy):**
- The root is **the phase**, and every path descends from it. A version of this figure with multiple roots, or with the signatures as the organizing level, is the glossary the chapter argues against.
- Four branches: **no Pod object / Pending / never ran / ran then ended.** The last two both sit under "scheduled to a node" — they are siblings, not peers of the first two.
- Each branch names its **owning component** before it names any signature: admission gate, scheduler, kubelet, kubelet-or-kernel. That middle rank is the method and must not be collapsed out to save space.
- The signature lists must land on the correct side. Never-ran: `ErrImagePull`, `ImagePullBackOff`, `ImageInspectError`, `ErrImageNeverPull`, `CreateContainerConfigError`. Ran-then-ended: `CrashLoopBackOff`, `OOMKilled`, `Evicted`, probe failures. Moving `CreateContainerConfigError` to the right, or `CrashLoopBackOff` to the left, reverses the chapter's central distinction.
- The two left branches deliberately have **no signature leaves.** Do not invent strings to balance the composition.
- Nine signatures total across both leaf lists — the caption's count must match what is drawn.

**Source ASCII (for designer reference):**
```
                      ONE KEY:  the phase
                            │
    ┌───────────────────────┼───────────────────────────────┐
    │                       │                               │
 no Pod object          Pending                    scheduled to a node
    │                       │                               │
    ▼                       ▼                   ┌───────────┴───────────┐
 the ADMISSION         the SCHEDULER        containers            containers
 gate stopped it       never placed it      never ran             ran, then ended
    │                       │                   │                       │
    ▼                       ▼                   ▼                       ▼
 read the CREATE       read the             the KUBELET           the KUBELET or
 response              SCHEDULER's          couldn't start it     the KERNEL ended it
 (Ch 12 §6)            events                  │                       │
                       (Ch 7 §2, §4)           ▼                       ▼
                                          ErrImagePull            CrashLoopBackOff
                                          ImagePullBackOff        OOMKilled
                                          ImageInspectError       Evicted
                                          ErrImageNeverPull       probe failures
                                          CreateContainerConfigError

              Nine signatures. One lookup. The key is always the phase.
```

**Proposed filename:** `ch13-zenith-read-the-phase-first.png` *(rename to `ch13-fig07-zenith-read-the-phase-first.png` only if the author approves the anchor correction; filename and anchor must change together)*

```yaml-figure-spec
anchor_id: ch13-zenith-read-the-phase-first
diagram_type: hierarchy_tree
source_ascii: |3
                        ONE KEY:  the phase
                              │
      ┌───────────────────────┼───────────────────────────────┐
      │                       │                               │
   no Pod object          Pending                    scheduled to a node
      │                       │                               │
      ▼                       ▼                   ┌───────────┴───────────┐
   the ADMISSION         the SCHEDULER        containers            containers
   gate stopped it       never placed it      never ran             ran, then ended
      │                       │                   │                       │
      ▼                       ▼                   ▼                       ▼
   read the CREATE       read the             the KUBELET           the KUBELET or
   response              SCHEDULER's          couldn't start it     the KERNEL ended it
   (Ch 12 §6)            events                  │                       │
                         (Ch 7 §2, §4)           ▼                       ▼
                                            ErrImagePull            CrashLoopBackOff
                                            ImagePullBackOff        OOMKilled
                                            ImageInspectError       Evicted
                                            ErrImageNeverPull       probe failures
                                            CreateContainerConfigError

                Nine signatures. One lookup. The key is always the phase.
vendor_terms: [kubelet]
complexity_hint:
  node_count: 13
  edge_count: 12
  label_count: 20
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure, fixed_point]
  learning_outcome: "Collapse nine failure signatures into a single lookup keyed on the Pod phase, and name the component that owns each stage"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the root node 'ONE KEY: the phase'"
accessibility:
  alt_text_seed: "A tree rooted in one key, the Pod phase, branching to four outcomes — no Pod object stopped at admission, Pending never placed by the scheduler, scheduled but containers never ran, and scheduled with containers that ran and then ended — each branch naming the component that owns it before listing its failure signatures, nine in total"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes container-state and phase reason strings as text; the tree structure and the component-ownership rank are original to this book."
```
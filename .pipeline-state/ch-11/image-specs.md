# Image Specifications — KCNA Chapter 11

*Generated from `draft-v1.md` (the pipeline note in the source confirms `draft-voice.md` does not exist at this stage). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Anchor inventory:** 6 figure anchors, 6 ASCII diagram blocks, 1:1 correspondence. No unanchored diagrams. One anchor ID is non-conforming — see below.

**Not diagrams (recorded so a later audit does not flag them):** the chapter contains two fenced ```yaml``` blocks — the `low-latency` StorageClass manifest in §3 and the `volumeClaimTemplates` excerpt in §6. Both are code listings quoted from source documents, not ASCII diagrams. They require no figure anchor and no entry here.

---

## ⚠ NON-CONFORMING ANCHOR ID

Rule 4 requires anchor IDs to match `ch{NN}-fig{MM}-{kebab-slug}` exactly. One anchor in the draft does not:

| Anchor as written in draft | Problem | Suggested correction |
|---|---|---|
| `ch11-zenith-outliving-the-pod` | Missing the `fig{MM}` segment; uses `zenith` where the ordinal belongs | `ch11-fig06-outliving-the-pod` |

**Not renamed here.** Per rule 6 the anchor ID is the join key and renaming is an author-review decision. The entry below preserves the ID exactly as the draft carries it. If the author accepts the correction, the change must be made in **both** places in the same commit (draft anchor + this document + the `yaml-figure-spec` `anchor_id`), or the join breaks.

---

## Figure: ch11-fig01-volume-lifetime-ladder

**Anchor ID:** `ch11-fig01-volume-lifetime-ladder`
**Purpose:** Establishes the chapter's organizing structure — three storage lifetimes separated by two destruction boundaries — so the reader can locate every later volume type on a rung.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** nested containment diagram (three concentric boxes representing widening lifetime scopes)

**Content specification:**
Three rectangles, strictly nested one inside another, drawn concentrically so the innermost is fully enclosed by the middle and the middle fully enclosed by the outer. The innermost box is labelled **CONTAINER WRITABLE LAYER** with the parenthetical `(rung 1)` right-aligned in its header, and a subtitle beneath: *survives nothing*. The middle box is labelled **POD-SCOPED VOLUME** `(rung 2)` with the subtitle *survives a container restart*. The outer box is labelled **CLUSTER-SCOPED STORAGE** `(rung 3)` with the subtitle *survives the Pod's deletion*. Two boundary annotations are the point of the figure and must be visually dominant: an upward-pointing arrow sitting on the *top edge of the innermost box*, labelled **boundary: CONTAINER RESTART** with a secondary line *(data below this line is discarded)*; and a second upward-pointing arrow on the *top edge of the middle box*, labelled **boundary: POD CEASES TO EXIST** with the same secondary line. Both arrows point outward/upward, away from the region that gets destroyed. Along the bottom inside edge of the outermost box, a closing statement in the same weight as the subtitles: *nothing in a Pod's lifecycle crosses this outer boundary*. Containment is the semantics here — do not redraw this as three side-by-side boxes or as a flowchart; the nesting *is* the argument that each rung's scope contains the one below it.

**Visual style:**
- Palette: inherit Lodestar book default (navy line-work on cream/white ground); the two boundary annotations in Brass
- Size (pixels): 1000x620 landscape
- Font: inherit book default (Roboto Slab display / Fira Sans body / Fira Mono for the rung labels and the literal `emptyDir`-class terms if any are added)
- Accent color for highlighted elements: Brass #B58B3E on both boundary arrows and their labels

**Critical details (non-negotiable accuracy):**
- Nesting order is fixed: container writable layer is **innermost**, cluster-scoped storage is **outermost**. Inverting this inverts the chapter.
- There are exactly **two** boundaries, not three. The outer box has no boundary arrow on it — the absence is deliberate and is stated in the closing line.
- The boundary arrows sit on the *top edge* of the box whose contents are destroyed, and point outward. The arrow labelled CONTAINER RESTART belongs to rung 1; the arrow labelled POD CEASES TO EXIST belongs to rung 2.
- "Rung 1 / 2 / 3" numbering must be preserved verbatim — the prose refers to rungs by number for the rest of the chapter.
- The wording *survives nothing* (rung 1) is exact and load-bearing. Do not soften to "does not persist."

**Source ASCII (for designer reference):**
```
   ┌──────────────────────────────────────────────────────────────┐
   │  CLUSTER-SCOPED STORAGE                          (rung 3)    │
   │  survives the Pod's deletion                                 │
   │                                                              │
   │   ┌────────────────────────────────────────────────────┐     │
   │   │  POD-SCOPED VOLUME                     (rung 2)    │     │
   │   │  survives a container restart                      │     │
   │   │                                                    │     │
   │   │   ┌──────────────────────────────────────────┐     │     │
   │   │   │  CONTAINER WRITABLE LAYER    (rung 1)    │     │     │
   │   │   │  survives nothing                        │     │     │
   │   │   └──────────────────────────────────────────┘     │     │
   │   │        ▲                                           │     │
   │   │        └── boundary: CONTAINER RESTART             │     │
   │   │            (data below this line is discarded)     │     │
   │   └────────────────────────────────────────────────────┘     │
   │            ▲                                                 │
   │            └── boundary: POD CEASES TO EXIST                 │
   │                (data below this line is discarded)           │
   │                                                              │
   │   nothing in a Pod's lifecycle crosses this outer boundary   │
   └──────────────────────────────────────────────────────────────┘
```

**Proposed filename:** `ch11-fig01-volume-lifetime-ladder.png`

```yaml-figure-spec
anchor_id: ch11-fig01-volume-lifetime-ladder
diagram_type: hierarchy_tree
source_ascii: |2
     ┌──────────────────────────────────────────────────────────────┐
     │  CLUSTER-SCOPED STORAGE                          (rung 3)    │
     │  survives the Pod's deletion                                 │
     │                                                              │
     │   ┌────────────────────────────────────────────────────┐     │
     │   │  POD-SCOPED VOLUME                     (rung 2)    │     │
     │   │  survives a container restart                      │     │
     │   │                                                    │     │
     │   │   ┌──────────────────────────────────────────┐     │     │
     │   │   │  CONTAINER WRITABLE LAYER    (rung 1)    │     │     │
     │   │   │  survives nothing                        │     │     │
     │   │   └──────────────────────────────────────────┘     │     │
     │   │        ▲                                           │     │
     │   │        └── boundary: CONTAINER RESTART             │     │
     │   │            (data below this line is discarded)     │     │
     │   └────────────────────────────────────────────────────┘     │
     │            ▲                                                 │
     │            └── boundary: POD CEASES TO EXIST                 │
     │                (data below this line is discarded)           │
     │                                                              │
     │   nothing in a Pod's lifecycle crosses this outer boundary   │
     └──────────────────────────────────────────────────────────────┘
vendor_terms: []
complexity_hint:
  node_count: 3
  edge_count: 2
  label_count: 9
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point]
  learning_outcome: "Trace a file outward from the container filesystem and name which of two boundaries destroys it"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the two boundary arrows labelled CONTAINER RESTART and POD CEASES TO EXIST"
accessibility:
  alt_text_seed: "Three nested rectangles showing widening storage lifetimes: an innermost container writable layer that survives nothing, a middle Pod-scoped volume that survives a container restart, and an outermost cluster-scoped storage box that survives the Pod's deletion; two arrows mark the boundaries at container restart and at Pod deletion"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic containment concepts; no vendor marks or icons reproduced."
```

---

## Figure: ch11-fig02-pv-pvc-storageclass-binding

**Anchor ID:** `ch11-fig02-pv-pvc-storageclass-binding`
**Purpose:** Fixes the supply/demand split and the single most-tested routing fact in the chapter — that a Pod's reference terminates at the PersistentVolumeClaim and never reaches the PersistentVolume.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-column supply-and-demand component diagram converging on a central binding node

**Content specification:**
Two columns at the top, left and right, each with a three-line header stack. Left column header: **SUPPLY** / *(cluster-scoped)* / *created by an admin*. Right column header: **DEMAND** / *(namespaced)* / *created by a user*. Beneath the left header, a box titled **PersistentVolume** containing four lines: `pv-fast-01`, `50Gi   RWO`, and a bracketed backing-store list `[NFS / EBS / Ceph / …]`. Beneath the right header, a box titled **PersistentVolumeClaim** containing `"data"`, `requests 20Gi`, `requests RWO`, `ns: production`. Both boxes drop a connector downward and inward to a central box labelled **BINDING control loop**, whose body reads *watches for new PVCs, / finds a matching PV, / binds them together* — the left connector enters it with a right-pointing arrowhead, the right connector with a left-pointing arrowhead, so the loop is visibly the convergence point. A single connector leaves the binding box downward, carrying the edge label **EXCLUSIVE, ONE-TO-ONE**, into a result box reading **PVC "data" is BOUND to PV pv-fast-01**. To the *left* of that result box sits a small box labelled **Pod**, with an arrow pointing right into the result box. Below the Pod box, an upward-pointing callout: *the Pod's line terminates HERE, at the claim. It never reaches the PersistentVolume.* Finally, isolated in the lower-left with no connectors at all, a small box labelled **StorageClass**, annotated *a third object, off to one side. Not explained yet. See §3.* — its disconnection is intentional and must survive the redraw.

**Visual style:**
- Palette: inherit Lodestar book default; supply column and demand column may take two distinct tints of the navy family, but the distinction must also read by position and header text alone
- Size (pixels): 900x950 portrait
- Font: inherit book default; object names (`pv-fast-01`, `"data"`, `ns: production`) in Fira Mono
- Accent color for highlighted elements: Brass #B58B3E on the Pod→claim arrow and its "terminates HERE" callout

**Critical details (non-negotiable accuracy):**
- The Pod arrow terminates at the **claim/bound-claim** box. It must not touch, cross, or visually continue toward the PersistentVolume box. This is the entire point of the figure.
- PersistentVolume is on the **supply/left/cluster-scoped/admin** side; PersistentVolumeClaim is on the **demand/right/namespaced/user** side. Reversing these reverses the chapter's central distinction and is the exam's documented trap.
- The claim requests **20Gi** against a **50Gi** volume, and the binding is still exclusive — do not "tidy" the numbers to match. The mismatch is deliberate: it sets up the "big enough, so it fits" trap corrected in the checkpoint.
- The **EXCLUSIVE, ONE-TO-ONE** edge label must be preserved on the binding→bound connector.
- StorageClass has **zero** connecting lines in this figure. Do not helpfully wire it to anything.
- `NFS / EBS / Ceph` appear as plain text inside a bracketed placeholder list. Render as text only — no vendor logos, no product icons.

**Source ASCII (for designer reference):**
```
        SUPPLY                                   DEMAND
   (cluster-scoped)                            (namespaced)
   created by an admin                       created by a user

   ┌───────────────────┐                  ┌────────────────────┐
   │ PersistentVolume  │                  │ PersistentVolume-  │
   │   pv-fast-01      │                  │   Claim  "data"    │
   │   50Gi   RWO      │                  │   requests 20Gi    │
   │   [NFS / EBS /    │                  │   requests RWO     │
   │    Ceph / …]      │                  │   ns: production   │
   └─────────┬─────────┘                  └─────────┬──────────┘
             │                                      │
             │      ┌────────────────────────┐      │
             └─────▶│   BINDING control loop │◀─────┘
                    │  watches for new PVCs, │
                    │  finds a matching PV,  │
                    │  binds them together   │
                    └───────────┬────────────┘
                                │
                       EXCLUSIVE, ONE-TO-ONE
                                │
                                ▼
                    ┌────────────────────────┐
   ┌──────────┐     │   PVC "data" is BOUND  │
   │   Pod    │────▶│   to PV pv-fast-01     │
   └──────────┘     └────────────────────────┘
        ▲
        └── the Pod's line terminates HERE, at the claim.
            It never reaches the PersistentVolume.

   ┌──────────────┐
   │ StorageClass │  ← a third object, off to one side.
   └──────────────┘     Not explained yet. See §3.
```

**Proposed filename:** `ch11-fig02-pv-pvc-storageclass-binding.png`

```yaml-figure-spec
anchor_id: ch11-fig02-pv-pvc-storageclass-binding
diagram_type: k8s_architecture
source_ascii: |2
          SUPPLY                                   DEMAND
     (cluster-scoped)                            (namespaced)
     created by an admin                       created by a user

     ┌───────────────────┐                  ┌────────────────────┐
     │ PersistentVolume  │                  │ PersistentVolume-  │
     │   pv-fast-01      │                  │   Claim  "data"    │
     │   50Gi   RWO      │                  │   requests 20Gi    │
     │   [NFS / EBS /    │                  │   requests RWO     │
     │    Ceph / …]      │                  │   ns: production   │
     └─────────┬─────────┘                  └─────────┬──────────┘
               │                                      │
               │      ┌────────────────────────┐      │
               └─────▶│   BINDING control loop │◀─────┘
                      │  watches for new PVCs, │
                      │  finds a matching PV,  │
                      │  binds them together   │
                      └───────────┬────────────┘
                                  │
                         EXCLUSIVE, ONE-TO-ONE
                                  │
                                  ▼
                      ┌────────────────────────┐
     ┌──────────┐     │   PVC "data" is BOUND  │
     │   Pod    │────▶│   to PV pv-fast-01     │
     └──────────┘     └────────────────────────┘
          ▲
          └── the Pod's line terminates HERE, at the claim.
              It never reaches the PersistentVolume.

     ┌──────────────┐
     │ StorageClass │  ← a third object, off to one side.
     └──────────────┘     Not explained yet. See §3.
vendor_terms: [persistentvolume, persistentvolumeclaim, storageclass, pod, nfs, ebs, ceph]
complexity_hint:
  node_count: 6
  edge_count: 4
  label_count: 13
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Distinguish PersistentVolume from PersistentVolumeClaim and identify which object a Pod references"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the Pod-to-claim arrow and its callout that the Pod's line terminates at the claim"
accessibility:
  alt_text_seed: "A supply column holding a cluster-scoped PersistentVolume and a demand column holding a namespaced PersistentVolumeClaim, both feeding a central binding control loop that produces an exclusive one-to-one bound pair; a Pod arrow points at the bound claim and stops there, and a disconnected StorageClass box sits to one side"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes API objects redrawn in Lodestar style; vendor names appear as plain text only. Re-evaluate to licensed_icon_set if the renderer substitutes official Kubernetes resource icons."
```

---

## Figure: ch11-fig03-static-vs-dynamic-provisioning

**Anchor ID:** `ch11-fig03-static-vs-dynamic-provisioning`
**Purpose:** Distinguishes static from dynamic provisioning as two branches of one decision, and makes the silent-failure third outcome — the claim that waits forever — as visually prominent as the two success paths.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** decision flowchart, two decision nodes, three terminal outcomes, top-to-bottom

**Content specification:**
Entry node at the top: **A PVC IS CREATED**, flowing down into the first decision: *Does a matching PV already exist and is it Available?* Two labelled exits: **YES** to the left, **NO** to the right. The YES branch is banner-labelled **═════ STATIC ═════** and carries the annotation *admin pre-created a PV carrying the real storage details*, then flows down into a process box **binder matches claim ↔ PV**. The NO branch enters a second decision node: *Does the claim name a StorageClass, AND is a provisioner configured for that class?* Its two exits are labelled **BOTH TRUE** and **EITHER MISSING**. BOTH TRUE is banner-labelled **═══ DYNAMIC ═══** with the annotation *provisioner creates a PV for this claim*, flowing into a process box **binder matches claim ↔ new PV**. EITHER MISSING flows into a distinct terminal box — visually different from the process boxes, ideally a heavier or hatched outline — reading **CLAIM WAITS, INDEFINITELY**, with body lines *Pod stays in Pending.* and *No error event that says so.* To that terminal box's right, an inbound annotation arrow carrying the italic maxim **an object without its component does nothing**. Both success paths (static and dynamic) converge on a single terminal box at the bottom: **PVC is BOUND / Pod can mount**. The failing path does **not** converge — it dead-ends.

**Visual style:**
- Palette: inherit Lodestar book default; the STATIC and DYNAMIC banner labels rendered as rules/banners rather than boxes, matching the ASCII's double-line treatment
- Size (pixels): 950x1050 portrait
- Font: inherit book default; `Pending` in Fira Mono
- Accent color for highlighted elements: Brass #B58B3E on the EITHER MISSING branch and the CLAIM WAITS terminal box

**Critical details (non-negotiable accuracy):**
- The second decision is a **conjunction**, not a choice: the claim must name a class **AND** the class must be configured to provision. The "AND" must be legible; do not split it into two sequential decision nodes with separate exits, which would imply either condition alone suffices.
- There are **three** terminal states, not two. The failure terminal must not be shrunk or footnoted; it carries as much exam weight as the success paths.
- The failure terminal's copy *No error event that says so* is the point — do not replace it with an error/warning glyph, which would contradict the text.
- Dynamic provisioning is reached only when **no** matching PV exists. The NO branch leading to dynamic is correct and must not be flipped.
- Static and dynamic both converge on the same bound state. Draw the convergence explicitly.

**Source ASCII (for designer reference):**
```
                        A PVC IS CREATED
                               │
                               ▼
              ┌────────────────────────────────┐
              │ Does a matching PV already     │
              │ exist and is it Available?     │
              └───────┬────────────────┬───────┘
                      │ YES            │ NO
                      ▼                ▼
        ═════ STATIC ═════      ┌─────────────────────────┐
                                │ Does the claim name a   │
   admin pre-created a PV       │ StorageClass, AND is a  │
   carrying the real storage    │ provisioner configured  │
   details                      │ for that class?         │
              │                 └───┬─────────────────┬───┘
              │                     │ BOTH            │ EITHER
              │                     │ TRUE            │ MISSING
              ▼                     ▼                 ▼
     ┌─────────────────┐  ═══ DYNAMIC ═══     ┌──────────────────┐
     │  binder matches │                      │  CLAIM WAITS,    │
     │  claim ↔ PV     │  provisioner creates │  INDEFINITELY    │
     └────────┬────────┘  a PV for this claim │                  │
              │                    │          │  Pod stays in    │
              │                    ▼          │  Pending.        │
              │           ┌─────────────────┐ │  No error event  │
              │           │  binder matches │ │  that says so.   │
              │           │  claim ↔ new PV │ └──────────────────┘
              │           └────────┬────────┘        ▲
              │                    │                 │
              └────────┬───────────┘        an object without its
                       ▼                    component does nothing
              ┌─────────────────┐
              │   PVC is BOUND  │
              │  Pod can mount  │
              └─────────────────┘
```

**Proposed filename:** `ch11-fig03-static-vs-dynamic-provisioning.png`

```yaml-figure-spec
anchor_id: ch11-fig03-static-vs-dynamic-provisioning
diagram_type: flowchart
source_ascii: |2
                          A PVC IS CREATED
                                 │
                                 ▼
                ┌────────────────────────────────┐
                │ Does a matching PV already     │
                │ exist and is it Available?     │
                └───────┬────────────────┬───────┘
                        │ YES            │ NO
                        ▼                ▼
          ═════ STATIC ═════      ┌─────────────────────────┐
                                  │ Does the claim name a   │
     admin pre-created a PV       │ StorageClass, AND is a  │
     carrying the real storage    │ provisioner configured  │
     details                      │ for that class?         │
                │                 └───┬─────────────────┬───┘
                │                     │ BOTH            │ EITHER
                │                     │ TRUE            │ MISSING
                ▼                     ▼                 ▼
       ┌─────────────────┐  ═══ DYNAMIC ═══     ┌──────────────────┐
       │  binder matches │                      │  CLAIM WAITS,    │
       │  claim ↔ PV     │  provisioner creates │  INDEFINITELY    │
       └────────┬────────┘  a PV for this claim │                  │
                │                    │          │  Pod stays in    │
                │                    ▼          │  Pending.        │
                │           ┌─────────────────┐ │  No error event  │
                │           │  binder matches │ │  that says so.   │
                │           │  claim ↔ new PV │ └──────────────────┘
                │           └────────┬────────┘        ▲
                │                    │                 │
                └────────┬───────────┘        an object without its
                         ▼                    component does nothing
                ┌─────────────────┐
                │   PVC is BOUND  │
                │  Pod can mount  │
                └─────────────────┘
vendor_terms: [persistentvolume, persistentvolumeclaim, storageclass, pod]
complexity_hint:
  node_count: 10
  edge_count: 10
  label_count: 14
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Predict whether a claim binds statically, triggers dynamic provisioning, or waits unbound indefinitely"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the EITHER MISSING branch and its CLAIM WAITS, INDEFINITELY terminal box"
accessibility:
  alt_text_seed: "A flowchart starting at PVC creation, branching on whether a matching PersistentVolume already exists; yes leads to static binding, no leads to a second decision requiring both a named StorageClass and a configured provisioner, whose true branch is dynamic provisioning and whose false branch dead-ends at a claim that waits indefinitely with the Pod stuck in Pending"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Decision logic redrawn from Kubernetes documented behaviour; no vendor artwork reproduced."
```

---

## Figure: ch11-fig04-access-modes-and-reclaim-policies

**Anchor ID:** `ch11-fig04-access-modes-and-reclaim-policies`
**Purpose:** Puts the two highest-yield enumerations in the chapter side by side and marks the single row where the counting unit changes from nodes to Pods.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel reference comparison — a four-row mode matrix beside a three-row policy table

**Content specification:**
Two panels of equal height, side by side, each with its title set into the top border rule. Left panel title: **WHAT YOU MAY DO**, subtitle lines *access modes* and *UNIT = NODES (except RWOP)*. It contains four rows, each of three parts: the abbreviation, a small glyph group, and a plain-English gloss. Row 1: `RWO` / one filled square followed by two dots / *1 node, r/w*. Row 2: `ROX` / three filled squares / *many, r/o*. Row 3: `RWX` / three filled squares / *many, r/w*. Row 4: `RWOP` / one **circled/distinct** mark followed by two dots / *1 POD, r/w*. An upward arrow rises from beneath the RWOP glyph into a two-line callout: *the unit changes HERE, and only here*. Right panel title: **WHAT HAPPENS AFTER**, subtitle lines *reclaim policies* and *when the claim is deleted*. It contains a three-column table with the column headers `PV obj`, `asset`, `data` and three policy rows: `Retain` → kept / kept / kept; `Delete` → gone / gone / gone; `Recycle` (struck through, with *(deprecated)* beneath) → em-dash in all three columns. Beneath the table, a two-line footer: *DEFAULT for dynamically provisioned volumes: Delete*.

**Visual style:**
- Palette: inherit Lodestar book default; the two panels equal in weight — neither is subordinate
- Size (pixels): 1200x460 landscape
- Font: inherit book default; the mode abbreviations and policy names in Fira Mono
- Accent color for highlighted elements: Brass #B58B3E on the RWOP row (glyph, label, and the "unit changes HERE" callout)

**Critical details (non-negotiable accuracy):**
- The RWOP glyph must be **visually distinct in shape**, not merely in colour, from the RWO glyph. This is the one row a greyscale or E-ink reader must still be able to pick out.
- `ROX` is *read-only* many; `RWX` is *read-write* many. Their glyph groups are identical (three marks) and only the r/o vs r/w gloss separates them — the gloss text must not be abbreviated away.
- `Recycle` is struck through **and** labelled deprecated. Both treatments, not one.
- The `Delete` row means the PV object, the backing storage asset, **and** the data are all gone. All three columns say gone; do not split.
- The default called out in the footer applies to **dynamically provisioned** volumes only. The word "dynamically" is load-bearing — manually created PVs default to `Retain`, which this panel deliberately does not show.
- `UNIT = NODES (except RWOP)` must stay in the left panel's header. It is the correction for the chapter's single most common misconception.

**Source ASCII (for designer reference):**
```
 ┌─ WHAT YOU MAY DO ────────────┐  ┌─ WHAT HAPPENS AFTER ───────────┐
 │  access modes                │  │  reclaim policies              │
 │  UNIT = NODES (except RWOP)  │  │  when the claim is deleted     │
 │                              │  │                                │
 │  RWO   ▣ · ·   1 node, r/w   │  │           PV obj  asset  data  │
 │  ROX   ▣ ▣ ▣   many, r/o     │  │  Retain     kept   kept   kept │
 │  RWX   ▣ ▣ ▣   many, r/w     │  │  Delete     gone   gone   gone │
 │  RWOP  ◉ · ·   1 POD, r/w    │  │  ~Recycle~   —      —      —   │
 │        ↑                     │  │   (deprecated)                 │
 │        └─ the unit changes   │  │                                │
 │           HERE, and only     │  │  DEFAULT for dynamically       │
 │           here               │  │  provisioned volumes: Delete   │
 └──────────────────────────────┘  └────────────────────────────────┘
```

**Proposed filename:** `ch11-fig04-access-modes-and-reclaim-policies.png`

```yaml-figure-spec
anchor_id: ch11-fig04-access-modes-and-reclaim-policies
diagram_type: other
source_ascii: |2
   ┌─ WHAT YOU MAY DO ────────────┐  ┌─ WHAT HAPPENS AFTER ───────────┐
   │  access modes                │  │  reclaim policies              │
   │  UNIT = NODES (except RWOP)  │  │  when the claim is deleted     │
   │                              │  │                                │
   │  RWO   ▣ · ·   1 node, r/w   │  │           PV obj  asset  data  │
   │  ROX   ▣ ▣ ▣   many, r/o     │  │  Retain     kept   kept   kept │
   │  RWX   ▣ ▣ ▣   many, r/w     │  │  Delete     gone   gone   gone │
   │  RWOP  ◉ · ·   1 POD, r/w    │  │  ~Recycle~   —      —      —   │
   │        ↑                     │  │   (deprecated)                 │
   │        └─ the unit changes   │  │                                │
   │           HERE, and only     │  │  DEFAULT for dynamically       │
   │           here               │  │  provisioned volumes: Delete   │
   └──────────────────────────────┘  └────────────────────────────────┘
vendor_terms: []
complexity_hint:
  node_count: 9
  edge_count: 1
  label_count: 22
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, fixed_point]
  learning_outcome: "Read an access mode as a node count, identify RWOP as the sole Pod-scoped mode, and state what each reclaim policy destroys"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the RWOP row and the callout reading 'the unit changes HERE, and only here'"
accessibility:
  alt_text_seed: "Two side-by-side reference panels: the left lists four access modes with the unit being nodes except for ReadWriteOncePod, which is highlighted as the only Pod-scoped mode; the right tabulates three reclaim policies showing Retain keeps the PV object, asset and data, Delete destroys all three, and Recycle is deprecated, with a footer noting Delete is the default for dynamically provisioned volumes"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Enumerated API values presented as an original reference layout; no vendor artwork reproduced."
```

---

## Figure: ch11-fig05-statefulset-pvc-pairing

**Anchor ID:** `ch11-fig05-statefulset-pvc-pairing`
**Purpose:** Shows one claim per Pod minted from a template, and then holds that pairing fixed across two disturbances — a reschedule and a deletion — to prove the claim is bound to the ordinal name rather than to the node or the workload.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** three-band state comparison; each band shows the same three Pod/claim pairs under a different condition

**Content specification:**
A header line spans the top: **StatefulSet "web" · volumeClaimTemplates: [ www ] · replicas: 3**. Below it, three horizontally-ruled bands stacked vertically, each showing the same three columns.

*Band 0 (unlabelled baseline):* three Pod boxes across the top — `web-0`, `web-1`, `web-2` — each dropping a downward arrow into its own PVC box below: `www-web-0`, `www-web-1`, `www-web-2`. Strictly one arrow per column; no crossing lines.

*Band 1, titled* **STATE 1: web-1 is RESCHEDULED to a different node**: a node label sits above each column, reading `node-a`, `node-c`, `node-b` left to right. The three Pods are still `web-0`, `web-1`, `web-2` in that order, and the middle Pod carries a leftward-pointing annotation *moved from node-b*. The three claim lines still run straight down to `www-web-0`, `www-web-1`, `www-web-2`, with the annotation *the claim line FOLLOWS the Pod* set between the Pod row and the claim row.

*Band 2, titled* **STATE 2: web-1 is DELETED**: the middle Pod box is replaced by an ✕ mark with the caption *(Pod gone)*. Its connector to `www-web-1` is drawn as a **dashed/dotted** line where the other two are solid. All three claim boxes are still present. An upward callout points at `www-web-1`: *THE CLAIM REMAINS. Nothing cleans it up.*

**Visual style:**
- Palette: inherit Lodestar book default; band separators as thin rules with the state titles set into them
- Size (pixels): 900x1100 portrait
- Font: inherit book default; every object name (`web-0`, `www-web-1`, `node-c`) in Fira Mono
- Accent color for highlighted elements: Brass #B58B3E on the surviving `www-web-1` claim in STATE 2 and its callout

**Critical details (non-negotiable accuracy):**
- **The source ASCII has a defect the redraw must fix.** In STATE 1 the third column's Pod box is missing its `web-2` label row — the annotation *◀── moved from node-b* overwrote it. The rendered figure must show **three** Pods in STATE 1: `web-0`, `web-1`, `web-2`.
- STATE 1 node labels are `node-a`, `node-c`, `node-b` in that left-to-right order, and this is **not** a typo. `web-1` has moved *onto* `node-c`; `web-2` is still on `node-b`, which is the node `web-1` came from. Do not "correct" the ordering to a-b-c.
- Claim names follow `<template>-<statefulset>-<ordinal>`, giving `www-web-0`, `www-web-1`, `www-web-2`. The template name comes **first**. Reversing it to `web-www-0` would falsify a fact the practice questions test directly.
- Pairing is strictly one-to-one down each column, in all three bands. No claim is shared, and no line ever crosses to a different column.
- In STATE 2 all three claim boxes remain. Removing or greying `www-web-1` out of existence inverts the figure's argument.
- The Pod's name is preserved across the reschedule: it is still `web-1` in STATE 1, not a new ordinal.

**Source ASCII (for designer reference):**
```
   StatefulSet "web"  ·  volumeClaimTemplates: [ www ]  ·  replicas: 3

     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │  web-0  │        │  web-1  │        │  web-2  │
     └────┬────┘        └────┬────┘        └────┬────┘
          │                  │                  │
          ▼                  ▼                  ▼
     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │ PVC     │        │ PVC     │        │ PVC     │
     │ www-    │        │ www-    │        │ www-    │
     │ web-0   │        │ web-1   │        │ web-2   │
     └─────────┘        └─────────┘        └─────────┘

   ── STATE 1: web-1 is RESCHEDULED to a different node ──────────

     node-a              node-c              node-b
     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │  web-0  │        │  web-1  │◀── moved from node-b
     └────┬────┘        └────┬────┘        └────┬────┘
          │                  │  the claim line   │
          ▼                  ▼  FOLLOWS the Pod  ▼
     [www-web-0]        [www-web-1]        [www-web-2]

   ── STATE 2: web-1 is DELETED ──────────────────────────────────

     ┌─────────┐             ✕             ┌─────────┐
     │  web-0  │        (Pod gone)         │  web-2  │
     └────┬────┘             ╎             └────┬────┘
          │                  ╎                  │
          ▼                  ▼                  ▼
     [www-web-0]        [www-web-1]        [www-web-2]
                        ↑ THE CLAIM REMAINS.
                          Nothing cleans it up.
```

**Proposed filename:** `ch11-fig05-statefulset-pvc-pairing.png`

```yaml-figure-spec
anchor_id: ch11-fig05-statefulset-pvc-pairing
diagram_type: k8s_architecture
source_ascii: |2
     StatefulSet "web"  ·  volumeClaimTemplates: [ www ]  ·  replicas: 3

       ┌─────────┐        ┌─────────┐        ┌─────────┐
       │  web-0  │        │  web-1  │        │  web-2  │
       └────┬────┘        └────┬────┘        └────┬────┘
            │                  │                  │
            ▼                  ▼                  ▼
       ┌─────────┐        ┌─────────┐        ┌─────────┐
       │ PVC     │        │ PVC     │        │ PVC     │
       │ www-    │        │ www-    │        │ www-    │
       │ web-0   │        │ web-1   │        │ web-2   │
       └─────────┘        └─────────┘        └─────────┘

     ── STATE 1: web-1 is RESCHEDULED to a different node ──────────

       node-a              node-c              node-b
       ┌─────────┐        ┌─────────┐        ┌─────────┐
       │  web-0  │        │  web-1  │◀── moved from node-b
       └────┬────┘        └────┬────┘        └────┬────┘
            │                  │  the claim line   │
            ▼                  ▼  FOLLOWS the Pod  ▼
       [www-web-0]        [www-web-1]        [www-web-2]

     ── STATE 2: web-1 is DELETED ──────────────────────────────────

       ┌─────────┐             ✕             ┌─────────┐
       │  web-0  │        (Pod gone)         │  web-2  │
       └────┬────┘             ╎             └────┬────┘
            │                  ╎                  │
            ▼                  ▼                  ▼
       [www-web-0]        [www-web-1]        [www-web-2]
                          ↑ THE CLAIM REMAINS.
                            Nothing cleans it up.
vendor_terms: [statefulset, persistentvolumeclaim, pod, kubernetes]
complexity_hint:
  node_count: 18
  edge_count: 9
  label_count: 26
pedagogy:
  part_18_criteria_met: [spatial_structure, temporal_structure, fixed_point]
  learning_outcome: "Explain why a StatefulSet's per-replica claim follows the Pod across a reschedule and survives the Pod's deletion"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the www-web-1 claim box that remains in STATE 2 after its Pod is deleted"
accessibility:
  alt_text_seed: "Three stacked bands showing a three-replica StatefulSet named web, each Pod paired one-to-one with its own PersistentVolumeClaim named www-web-0 through www-web-2; in the second band web-1 has moved to a different node and keeps its claim, and in the third band web-1 is deleted while its claim remains in place"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes workload objects redrawn in Lodestar style. Re-evaluate to licensed_icon_set if official Kubernetes resource icons are substituted for the Pod and PVC boxes."
```

---

## Figure: ch11-zenith-outliving-the-pod

**⚠ Anchor ID does not conform to `ch{NN}-fig{MM}-{slug}` — see the NON-CONFORMING ANCHOR ID section at the top of this document. Preserved verbatim here as the join key; suggested correction is `ch11-fig06-outliving-the-pod`, pending author review.**

**Anchor ID:** `ch11-zenith-outliving-the-pod`
**Purpose:** Carries the chapter's ☀️ Zenith moment visually — the Pod's existence is discontinuous across nodes while its storage is one unbroken line, which is the chapter title stated as a picture.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-lane persistence timeline (horizontal swimlanes sharing one time axis)

**Content specification:**
Two horizontal lanes sharing a single left-to-right time axis. The upper lane is labelled **Pod** at its left margin and contains **three separate bounded segments** with visible gaps between them; each segment is labelled `web-1` on its bar with a node annotation beneath: `(node-b)`, then `(node-e)`, then `(node-e)`. The segment boundaries must read as start and end caps — the Pod is repeatedly destroyed and recreated. The lower lane is labelled **Storage** at its left margin and is a **single unbroken heavy rule** running the full width of the figure and terminating in a right-pointing arrowhead, captioned beneath: `www-web-1 — one continuous line, never broken`. From each Pod segment, a light vertical connector drops to the storage lane, each labelled *claims*. A time axis runs along the bottom, labelled **time** with a right-pointing arrow. The whole argument is the visual contrast between three interrupted segments above and one continuous line below — the gaps in the upper lane must be unmistakable at ebook thumbnail size.

**Visual style:**
- Palette: inherit Lodestar book default; the storage line noticeably heavier in weight than the Pod segments
- Size (pixels): 1200x360 landscape
- Font: inherit book default; `web-1`, `www-web-1`, `node-b`, `node-e` in Fira Mono
- Accent color for highlighted elements: Brass #B58B3E on the unbroken storage line

**Critical details (non-negotiable accuracy):**
- The storage lane is **one continuous line with no break of any kind**, including beneath the gaps in the Pod lane. Any segmentation destroys the figure's meaning.
- The Pod lane has **three** segments with **visible gaps** between them. Butting the segments together would imply continuity the chapter explicitly denies.
- Node annotations read `(node-b)`, `(node-e)`, `(node-e)` in that order. The last two are the **same** node — the Pod restarted in place — and this repetition is intentional, not a duplication error.
- The Pod is named `web-1` in all three segments. The name is stable; the Pod is not.
- The claim name `www-web-1` matches the same-named claim in `ch11-fig05-statefulset-pvc-pairing`. The two figures must stay consistent.
- Connectors point from Pod **down to** storage, labelled *claims*. Direction matters: the Pod claims the storage, not the reverse.

**Source ASCII (for designer reference):**
```
   Pod    ├──web-1──┤        ├──web-1──┤    ├──web-1──┤
           (node-b)           (node-e)       (node-e)
              ╎                  ╎              ╎
              ╎ claims           ╎ claims       ╎ claims
              ▼                  ▼              ▼
 Storage ═══════════════════════════════════════════════════▶
          www-web-1 — one continuous line, never broken

                    time ──────────────────────────────────▶
```

**Proposed filename:** `ch11-zenith-outliving-the-pod.png`
*(If the author accepts the anchor correction, this becomes `ch11-fig06-outliving-the-pod.png`.)*

```yaml-figure-spec
anchor_id: ch11-zenith-outliving-the-pod
diagram_type: other
source_ascii: |2
     Pod    ├──web-1──┤        ├──web-1──┤    ├──web-1──┤
             (node-b)           (node-e)       (node-e)
                ╎                  ╎              ╎
                ╎ claims           ╎ claims       ╎ claims
                ▼                  ▼              ▼
   Storage ═══════════════════════════════════════════════════▶
            www-web-1 — one continuous line, never broken

                      time ──────────────────────────────────▶
vendor_terms: [pod, persistentvolumeclaim]
complexity_hint:
  node_count: 4
  edge_count: 3
  label_count: 9
pedagogy:
  part_18_criteria_met: [temporal_structure, zenith]
  learning_outcome: "State that storage outlives the Pod that asked for it, because a claim is a record of intent that outlives the thing acting on it"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the unbroken storage line labelled www-web-1 running the full width beneath the interrupted Pod lane"
accessibility:
  alt_text_seed: "A two-lane timeline: the upper Pod lane shows three separate segments each labelled web-1, on node-b then node-e then node-e, with visible gaps between them; the lower Storage lane is a single unbroken line labelled www-web-1 running the full width, with claim connectors dropping from each Pod segment to the storage line"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Original temporal illustration of the chapter's synthesis; no vendor IP reproduced."
```
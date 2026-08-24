# Image Specifications — KCNA Chapter 4

*Generated from the voiced draft (`.pipeline-state/ch-04/draft-v1.md` — the voice-swap stage moved `draft-voice.md` into the canonical `draft-v1.md` slot; `draft-v1-prevoice.md` holds the pre-voice text). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Chapter:** 4 — *Records of Intent* · `chapter_type: content` · Kubernetes Fundamentals (Kubernetes Core Concepts)
**Anchors found:** 6 · **Entries below:** 6 · **Unanchored ASCII diagrams:** 0

---

## ANCHOR FLAGS (author review required)

Two anchor issues. Neither is renamed here — anchor IDs are the join key, and renaming is an author-review decision (rule 6). Both are recorded so the book-level aggregator and the diagram pipeline see the same IDs the draft carries.

**1. Malformed anchor ID — `ch04-zenith-declaration-not-order`** (draft line 744).
Does not match the required `ch{NN}-fig{MM}-{kebab-slug}` pattern: the `fig{MM}` segment is missing entirely, replaced by `zenith`. Every other anchor in this chapter conforms. Suggested correction: **`ch04-fig06-declaration-not-order`** — it is the sixth figure in document order and the slug is already clean. If the author confirms, the change must be made in the draft *and* here in the same pass, or the join key breaks.

**2. Figure numbering does not follow document order.**
Anchors appear in the draft in the sequence `fig01` (L203) → `fig02` (L250) → `fig04` (L364) → `fig05` (L491) → `fig03` (L613) → `zenith` (L744). `ch04-fig03-labels-selectors-join` is the fifth figure a reader encounters but carries the third number. This is not an error the linter will catch — the IDs are all well-formed and unique — but it will read oddly in the book-level image index, where figures sort by ID. Author to decide whether to renumber (`fig03` ↔ `fig05`, cascading) or accept. **Entries below are listed in document order, not ID order.**

---

## Figure: ch04-fig01-object-anatomy-spec-status

**Anchor ID:** `ch04-fig01-object-anatomy-spec-status`
**Purpose:** Establishes the four author-written top-level fields of a Kubernetes object and separates them, visually and permanently, from the one field the system writes — the distinction the ★ Fixed Point three paragraphs later depends on.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel labeled structure diagram, split by a horizontal authorship boundary

**Content specification:**
Two stacked rectangular panels of equal width, separated by a heavy horizontal double rule that spans the full width and carries the centered label **"authorship boundary."** The upper panel is headed **"YOU AUTHOR THIS"** and lists, in fixed-width type, four top-level YAML field names with a right-hand gloss column: `apiVersion` → "which API version"; `kind` → "what kind of object"; `metadata` → "which one, specifically"; `spec` → "what it should look like". Nested one indent level under `metadata`, show three sub-keys — `name:`, `uid:`, and `namespace:` — with `namespace:` carrying the parenthetical `(optional)`. Nested one indent level under `spec`, show an ellipsis placeholder. The lower panel is headed **"THE SYSTEM AUTHORS THIS"** and contains exactly one field, `status`, glossed "what is actually true", with an ellipsis placeholder nested beneath it. The visual weight must be deliberately asymmetric: four fields above, one below. The point of the figure is the boundary rule itself, not either panel — it should be the heaviest stroke on the page, heavier than the panel borders. Dotted leader lines connect each field name to its gloss so the two columns read as paired.

**Visual style:**
- Palette: book default — Navy `#0B1E3B` panel strokes and field names, Fog `#8A8D90` for the gloss column and leader dots, Cream `#F5EFE4` panel fill
- Size (pixels): 900x560 landscape
- Font: inherit book default (Fira Mono for field names and the gloss column; Fira Sans small-caps for the two panel headers)
- Accent color for highlighted elements: Brass `#B58B3E` for the authorship boundary rule and its label — the single accented element in the figure

**Critical details (non-negotiable accuracy):**
- `spec` is **above** the boundary and `status` is **below** it. Reversing these inverts the chapter's central Fixed Point.
- `namespace` is marked optional; `name` and `uid` are not. Do not mark all three optional or all three required.
- `namespace` sits **nested under `metadata`**, not as a fifth top-level field. This is a common misreading and the figure must not license it.
- Exactly four top-level fields above the line. Do not add `status` to the upper panel "for symmetry," and do not add any field the draft does not name (no `labels`, no `annotations` — those are deferred to §5).
- The gloss text is the four questions the mnemonic at draft line 197 depends on, in this order: which API version / what kind / which one / what it should look like. Order is load-bearing.
- `status` must not be drawn with an input arrow from the reader or from any user-facing element. Nothing in this figure points *into* `status`.

**Source ASCII (for designer reference):**
```
        ┌──────────────────────────────────────────────────────┐
        │  YOU AUTHOR THIS                                     │
        │                                                      │
        │  apiVersion: ...........  which API version          │
        │  kind: .................  what kind of object        │
        │  metadata:                which one, specifically    │
        │    name: ...                                         │
        │    uid: ...                                          │
        │    namespace: ...        (optional)                  │
        │  spec:                    what it should look like   │
        │    ...                                               │
        └──────────────────────────────────────────────────────┘
        ═══════════════ authorship boundary ═══════════════════
        ┌──────────────────────────────────────────────────────┐
        │  THE SYSTEM AUTHORS THIS                             │
        │                                                      │
        │  status:                  what is actually true      │
        │    ...                                               │
        └──────────────────────────────────────────────────────┘
```

**Proposed filename:** `ch04-fig01-object-anatomy-spec-status.png`

```yaml-figure-spec
anchor_id: ch04-fig01-object-anatomy-spec-status
diagram_type: component_diagram
source_ascii: |2
          ┌──────────────────────────────────────────────────────┐
          │  YOU AUTHOR THIS                                     │
          │                                                      │
          │  apiVersion: ...........  which API version          │
          │  kind: .................  what kind of object        │
          │  metadata:                which one, specifically    │
          │    name: ...                                         │
          │    uid: ...                                          │
          │    namespace: ...        (optional)                  │
          │  spec:                    what it should look like   │
          │    ...                                               │
          └──────────────────────────────────────────────────────┘
          ═══════════════ authorship boundary ═══════════════════
          ┌──────────────────────────────────────────────────────┐
          │  THE SYSTEM AUTHORS THIS                             │
          │                                                      │
          │  status:                  what is actually true      │
          │    ...                                               │
          └──────────────────────────────────────────────────────┘
vendor_terms: [apiVersion, kind, metadata, spec, status]
complexity_hint:
  node_count: 2
  edge_count: 1
  label_count: 11
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point, distinguishing_alternatives]
  learning_outcome: "Name the four top-level fields of any Kubernetes object and state which of spec/status the author writes and which the system writes"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the authorship boundary rule separating the spec panel from the status panel"
accessibility:
  alt_text_seed: "Two stacked panels split by a heavy horizontal line labelled authorship boundary. The upper panel, headed YOU AUTHOR THIS, lists apiVersion, kind, metadata with nested name, uid and optional namespace, and spec. The lower panel, headed THE SYSTEM AUTHORS THIS, contains only status."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 900
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes API field names are functional identifiers; layout and the authorship-boundary framing are Lodestar's own."
```

---

## Figure: ch04-fig02-apply-round-trip

**Anchor ID:** `ch04-fig02-apply-round-trip`
**Purpose:** Traces a single declaration from a file on disk through the API server and etcd to a controller that watches, compares, and acts — showing that the loop at the end never terminates.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** vertical flowchart with a terminating perpetual cycle

**Content specification:**
A top-to-bottom flow beginning with a document-shaped node labeled **`manifest.yaml`**. A downward arrow leaves it, labeled **`kubectl apply -f`**, and enters a rectangular component box labeled **`kube-apiserver`**. From that box, a horizontal right-pointing arrow labeled **"writes the record"** connects to a second component box labeled **`etcd`**, drawn as a datastore (cylinder or rounded rectangle). From `etcd`, a line descends and then turns left, joining a left-pointing arrow labeled **"a controller watches"** that feeds back beneath `kube-apiserver` — the watch originates at the store side and terminates at the controller, not at the user. Below that, a downward arrow leads to an unboxed process step: **"the controller compares `spec` vs `status`"**. A downward arrow labeled **"they differ → it acts"** leads to a final step, **"reality changes ──► status is updated"**. From that step, a return path runs back up to the compare step, forming a closed cycle; the cycle carries the caption **"and it watches again, forever"** placed at the bottom of the loop. The loop must be visually closed and must have no exit arrow — no terminal node, no "done" state. That absence is the entire point of the figure.

**Visual style:**
- Palette: book default — Navy `#0B1E3B` for component boxes and primary flow arrows, Teal `#1F4A4E` for the watch edge and the compare step, Fog `#8A8D90` for edge labels, Cream `#F5EFE4` background
- Size (pixels): 800x780 portrait
- Font: inherit book default (Fira Mono for component names and field names; Fira Sans for edge labels and prose steps)
- Accent color for highlighted elements: Brass `#B58B3E` for the closed return loop and the "and it watches again, forever" caption

**Critical details (non-negotiable accuracy):**
- The controller **watches the API server**. It does not receive a message from `kubectl`, and it does not receive one from the reader. No arrow may originate at `manifest.yaml` or at the user and terminate at the controller — this is the exact misconception the 🔭 Closer Look at draft line 276 exists to correct.
- `kubectl apply -f` targets **`kube-apiserver`**, not `etcd`. Only the API server writes to etcd.
- Direction of the write edge: `kube-apiserver` → `etcd`, never reversed.
- The bottom loop is **closed and unterminated**. Do not add a completion state, a success checkmark, or an exit branch.
- The compare step reads `spec` vs `status` in that order, matching fig01's vertical arrangement.
- This figure is explicitly contrasted in its caption against Chapter 3's request-path figure. Keep component-box styling consistent with that earlier figure so readers can see they are the same components viewed differently, but do not reproduce Chapter 3's layout.

**Source ASCII (for designer reference):**
```
     manifest.yaml
          │
          │  kubectl apply -f
          ▼
    ┌──────────────┐  writes the record   ┌──────────┐
    │ kube-apiserver├─────────────────────►│   etcd   │
    └──────┬───────┘                       └────┬─────┘
           │                                    │
           │  a controller watches ◄────────────┘
           ▼
    the controller compares  spec  vs  status
           │
           │  they differ → it acts
           ▼
    reality changes ──► status is updated ──┐
           ▲                                │
           └────────────────────────────────┘
                    and it watches again, forever
```

**Proposed filename:** `ch04-fig02-apply-round-trip.png`

```yaml-figure-spec
anchor_id: ch04-fig02-apply-round-trip
diagram_type: flowchart
source_ascii: |2
       manifest.yaml
            │
            │  kubectl apply -f
            ▼
      ┌──────────────┐  writes the record   ┌──────────┐
      │ kube-apiserver├─────────────────────►│   etcd   │
      └──────┬───────┘                       └────┬─────┘
             │                                    │
             │  a controller watches ◄────────────┘
             ▼
      the controller compares  spec  vs  status
             │
             │  they differ → it acts
             ▼
      reality changes ──► status is updated ──┐
             ▲                                │
             └────────────────────────────────┘
                      and it watches again, forever
vendor_terms: [kube-apiserver, etcd, kubectl]
complexity_hint:
  node_count: 5
  edge_count: 6
  label_count: 11
pedagogy:
  part_18_criteria_met: [temporal_structure, spatial_structure]
  learning_outcome: "Trace what happens to a single object after kubectl apply, and explain why the reconciliation loop never terminates"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the closed return loop and its caption, and it watches again, forever"
accessibility:
  alt_text_seed: "A vertical flow from manifest.yaml through kubectl apply into kube-apiserver, which writes the record to etcd. A controller watches the API server, compares spec against status, acts when they differ, and reality changes so status is updated; an arrow returns to the compare step, forming a loop that never ends."
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 800
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Component names are Kubernetes project identifiers; the round-trip framing and loop emphasis are Lodestar's own composition."
```

---

## Figure: ch04-fig04-namespaced-vs-cluster-scoped

**Anchor ID:** `ch04-fig04-namespaced-vs-cluster-scoped`
**Purpose:** Shows that namespace scoping is a containment boundary some resources sit inside and others cannot, and that identical resource names in two different namespaces are legal.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** nested containment diagram (cluster boundary enclosing two namespace boundaries)

**Content specification:**
One large outer container with a heavy double border, headed **CLUSTER SCOPE**. In the upper region of that container, outside any inner box, place four cluster-scoped resource type names in a single row or two: **Node**, **PersistentVolume**, **StorageClass**, and **Namespace** — with a parenthetical beside the last reading *(the namespace objects themselves live out here)*. Beneath them, side by side inside the cluster container, draw two equally sized inner boxes with lighter borders, labeled **`namespace: team-a`** and **`namespace: team-b`**. Each inner box contains an identical list of four entries: `Deployment "database"`, `Service "database"`, `ConfigMap "settings"`, `Secret "creds"`. The two lists must be visually identical, aligned row-for-row so the eye immediately reads them as the same four names appearing twice. There is no arrow anywhere in this figure and no connection between the two namespace boxes — the whole content is containment. The four cluster-scoped names in the outer region must be clearly outside both inner boxes, with enough whitespace that no reader could mistake them for belonging to either.

**Visual style:**
- Palette: book default — Navy `#0B1E3B` for the outer cluster border and headings, Teal `#1F4A4E` for the two namespace borders and their labels, Fog `#8A8D90` for the parenthetical gloss, Cream `#F5EFE4` fill throughout
- Size (pixels): 1000x520 landscape
- Font: inherit book default (Fira Mono for resource type names and quoted object names; Fira Sans for the CLUSTER SCOPE heading)
- Accent color for highlighted elements: Brass `#B58B3E` on the two identical `"database"` name pairs, drawing the eye to the fact that the same name appears in both boxes

**Critical details (non-negotiable accuracy):**
- **Namespace objects themselves are cluster-scoped.** `Namespace` must appear in the outer region, never inside an inner box. This is the detail examiners use and the one designers most often "tidy up" incorrectly.
- Node, PersistentVolume, and StorageClass are cluster-scoped. Do not place any of them inside a namespace box.
- Deployment, Service, ConfigMap, and Secret are namespaced. Do not place any of them in the outer region.
- The namespace boxes must be **siblings, not nested**. Namespaces cannot be nested inside one another — a figure showing containment between them would contradict draft line 348 directly.
- The two inner boxes contain **the same four names**, not similar ones. Do not differentiate them ("database-a" / "database-b") for visual variety; the identity of the names is the fact being taught.
- Exactly one level of nesting: cluster → namespace. No third tier.
- No arrows. Nothing in this figure flows.

**Source ASCII (for designer reference):**
```
 ╔══════════════════════════════════════════════════════════════════╗
 ║  CLUSTER SCOPE                                                   ║
 ║                                                                  ║
 ║   Node        PersistentVolume        StorageClass               ║
 ║   Namespace  (the namespace objects themselves live out here)    ║
 ║                                                                  ║
 ║   ┌────────────────────────────┐  ┌────────────────────────────┐ ║
 ║   │  namespace: team-a         │  │  namespace: team-b         │ ║
 ║   │                            │  │                            │ ║
 ║   │    Deployment "database"   │  │    Deployment "database"   │ ║
 ║   │    Service    "database"   │  │    Service    "database"   │ ║
 ║   │    ConfigMap  "settings"   │  │    ConfigMap  "settings"   │ ║
 ║   │    Secret     "creds"      │  │    Secret     "creds"      │ ║
 ║   └────────────────────────────┘  └────────────────────────────┘ ║
 ╚══════════════════════════════════════════════════════════════════╝
```

**Proposed filename:** `ch04-fig04-namespaced-vs-cluster-scoped.png`

```yaml-figure-spec
anchor_id: ch04-fig04-namespaced-vs-cluster-scoped
diagram_type: k8s_architecture
source_ascii: |2
   ╔══════════════════════════════════════════════════════════════════╗
   ║  CLUSTER SCOPE                                                   ║
   ║                                                                  ║
   ║   Node        PersistentVolume        StorageClass               ║
   ║   Namespace  (the namespace objects themselves live out here)    ║
   ║                                                                  ║
   ║   ┌────────────────────────────┐  ┌────────────────────────────┐ ║
   ║   │  namespace: team-a         │  │  namespace: team-b         │ ║
   ║   │                            │  │                            │ ║
   ║   │    Deployment "database"   │  │    Deployment "database"   │ ║
   ║   │    Service    "database"   │  │    Service    "database"   │ ║
   ║   │    ConfigMap  "settings"   │  │    ConfigMap  "settings"   │ ║
   ║   │    Secret     "creds"      │  │    Secret     "creds"      │ ║
   ║   └────────────────────────────┘  └────────────────────────────┘ ║
   ╚══════════════════════════════════════════════════════════════════╝
vendor_terms: [Node, PersistentVolume, StorageClass, Namespace, Deployment, Service, ConfigMap, Secret]
complexity_hint:
  node_count: 15
  edge_count: 0
  label_count: 15
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Distinguish namespaced from cluster-scoped resources, and explain why identical resource names in two namespaces do not collide"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the four cluster-scoped resource names sitting outside both namespace boxes"
accessibility:
  alt_text_seed: "A cluster boundary containing Node, PersistentVolume, StorageClass and Namespace in its outer region, and two side-by-side namespace boxes, team-a and team-b, each holding an identical set of four objects: a Deployment and Service both named database, a ConfigMap named settings, and a Secret named creds."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kubernetes resource kind names are functional identifiers; the team-a/team-b illustration is Lodestar's own construction."
```

---

## Figure: ch04-fig05-configmap-secret-contrast

**Anchor ID:** `ch04-fig05-configmap-secret-contrast`
**Purpose:** Sets ConfigMap against Secret on four dimensions so the reader sees that the two differ in intent and handling but are stored identically — the row that produces the chapter's most confident wrong answers.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-column comparison matrix (contrast table)

**Content specification:**
A four-row, two-column comparison matrix with a row-label gutter on the left. Column headers: **ConfigMap** and **Secret**. Row labels, top to bottom: **Intended contents**, **Consumed by a Pod as**, **Stored**, **What it adds**. Cell contents, verbatim in substance: Row 1 — ConfigMap: "non-confidential key-value data"; Secret: "small amounts of sensitive data (password, token, key)". Row 2 — both columns carry the same four-item list: "command and args", "environment variables", then the columns diverge by one word only: ConfigMap says "file in a read-only volume" where Secret says "file in a volume", and both close with "read via the Kubernetes API". Row 3 — ConfigMap: "unencrypted, in etcd"; Secret: "unencrypted, in etcd (by default)". Row 4 — ConfigMap: "nothing — the docs state plainly that it provides no secrecy or encryption"; Secret: "a distinct object type, a distinct access-control surface, and a defined place to attach encryption at rest". A horizontal rule sits directly beneath the column headers. **Row 3 must be given visual emphasis** — a tinted band, a heavier rule, or a marginal marker — because its two cells are substantively the same and that identity is what the reader is meant to carry away. Row 2's single-word divergence ("read-only volume" vs "volume") should be subtly marked so it is findable but does not compete with row 3 for attention.

**Visual style:**
- Palette: book default — Navy `#0B1E3B` for column headers and row labels, body text in standard body color, Fog `#8A8D90` for the parentheticals, Cream `#F5EFE4` background with a slightly deeper cream tint on the emphasized row
- Size (pixels): 1000x620 landscape
- Font: inherit book default (Fira Sans for cell prose, Fira Mono for the object type names in the headers)
- Accent color for highlighted elements: Brass `#B58B3E` on the row-3 band and on the word "unencrypted" in both row-3 cells

**Critical details (non-negotiable accuracy):**
- **Row 3 is identical on both sides.** A Secret is *not* encrypted at rest by default. Any treatment that softens, hedges, or differentiates this row defeats the figure's purpose and contradicts the ⚠ Navigational Hazards block immediately following it.
- Row 4's ConfigMap cell must say the object adds **nothing** in terms of secrecy. Do not soften to "less" or "minimal."
- Row 2's ConfigMap volume entry is **read-only**; the Secret entry is not qualified as read-only. This asymmetry is in the source documentation and must survive.
- Do not add a lock glyph, shield, key, or any security iconography to the Secret column. The figure's argument is that the visual instinct to do exactly that is the misconception.
- Four rows, no more. Do not append size limits, immutability, or namespace rules — those are handled in the adjacent Navigational Hazards block, not here.
- The two columns must be given equal visual weight. Do not style Secret as "the important one."

**Source ASCII (for designer reference):**
```
                        ConfigMap                    Secret
 ─────────────────────────────────────────────────────────────────────────
 Intended contents      non-confidential             small amounts of
                        key-value data               sensitive data
                                                     (password, token, key)

 Consumed by a Pod as   command and args             command and args
                        environment variables        environment variables
                        file in a read-only volume   file in a volume
                        read via the Kubernetes API  read via the Kubernetes API

 Stored                 unencrypted, in etcd         unencrypted, in etcd
                                                     (by default)

 What it adds           nothing — the docs state     a distinct object type,
                        plainly that it provides     a distinct access-control
                        no secrecy or encryption     surface, and a defined
                                                     place to attach
                                                     encryption at rest
```

**Proposed filename:** `ch04-fig05-configmap-secret-contrast.png`

```yaml-figure-spec
anchor_id: ch04-fig05-configmap-secret-contrast
diagram_type: other
source_ascii: |2
                          ConfigMap                    Secret
   ─────────────────────────────────────────────────────────────────────────
   Intended contents      non-confidential             small amounts of
                          key-value data               sensitive data
                                                       (password, token, key)

   Consumed by a Pod as   command and args             command and args
                          environment variables        environment variables
                          file in a read-only volume   file in a volume
                          read via the Kubernetes API  read via the Kubernetes API

   Stored                 unencrypted, in etcd         unencrypted, in etcd
                                                       (by default)

   What it adds           nothing — the docs state     a distinct object type,
                          plainly that it provides     a distinct access-control
                          no secrecy or encryption     surface, and a defined
                                                       place to attach
                                                       encryption at rest
vendor_terms: [ConfigMap, Secret, etcd, Pod]
complexity_hint:
  node_count: 8
  edge_count: 0
  label_count: 14
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, vendor_taxonomy]
  learning_outcome: "State how ConfigMap and Secret differ in intent and handling, and that neither is encrypted at rest by default"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the Stored row, whose two cells are substantively identical"
accessibility:
  alt_text_seed: "A four-row comparison of ConfigMap and Secret covering intended contents, how a Pod consumes them, how they are stored, and what each adds. The storage row reads unencrypted in etcd for both, with by default noted on the Secret side."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Cell text paraphrases Kubernetes documentation (CC BY 4.0); the four-dimension contrast and the emphasis on the identical storage row are Lodestar's editorial framing."
```

---

## Figure: ch04-fig03-labels-selectors-join

**Anchor ID:** `ch04-fig03-labels-selectors-join`
**Purpose:** Shows that a selector resolves to a *set* rather than a folder, by displaying four labeled Pods whose selected sets overlap — one Pod in two sets, one Pod in none.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-register mapping diagram (labeled objects above, selector-to-set resolutions below)

**Content specification:**
Two horizontal registers separated by generous whitespace and a section label each. Upper register, headed **"OBJECTS, each carrying labels"**: four identical card-shaped boxes in a row, labeled `Pod A`, `Pod B`, `Pod C`, `Pod D`. Each card carries two label rows beneath its name, in fixed-width type: Pod A → `tier=fe`, `env=prod`; Pod B → `tier=fe`, `env=dev`; Pod C → `tier=be`, `env=prod`; Pod D → `tier=be`, `env=dev`. Lower register, headed **"SELECTORS, each resolving to a set"**: four rows, each showing a selector expression on the left, a right-pointing arrow, and a set-notation result on the right. Row 1: `tier = fe` → `{ A , B }`. Row 2: `env = prod` → `{ A , C }`. Row 3: `env in (prod, qa)` → `{ A , C }`. Row 4: `tier = be , env = prod` → `{ C }`. The set results must be **column-aligned by member position**, so that A, B, C and D each occupy a fixed horizontal slot across all four rows and absent members leave visible gaps. That alignment is what makes the overlap readable at a glance: the A column is populated in three of four rows, the D column in none. Optionally, faint vertical guide lines may connect each Pod card in the upper register down to its column position in the lower register; if used they must be Fog-weight and clearly subordinate to the cards and the selector rows.

**Visual style:**
- Palette: book default — Navy `#0B1E3B` for Pod card borders and names, Teal `#1F4A4E` for selector expressions and the resolution arrows, Fog `#8A8D90` for the two register headings and any guide lines, Cream `#F5EFE4` fill
- Size (pixels): 1000x640 landscape
- Font: inherit book default (Fira Mono throughout for labels, selector expressions, and set notation; Fira Sans for the two register headings)
- Accent color for highlighted elements: Brass `#B58B3E` on every occurrence of `A` in the set results, marking the Pod that belongs to more than one selected set

**Critical details (non-negotiable accuracy):**
- Rows 2 and 3 resolve to **the same set**, `{ A , C }`. `env = prod` and `env in (prod, qa)` select identically here because no Pod carries `env=qa`. Differentiating these two results would teach a falsehood about set-based operators.
- Row 4 uses a comma, and the comma means **AND**. `tier = be , env = prod` yields `{ C }` alone. Do not render the comma as an OR, and do not render the result as `{ C , D }`.
- **Pod D appears in no set.** Do not "balance" the figure by giving D a row. Its absence is deliberate — the caption at draft line 631 depends on it.
- **Pod A appears in three of the four sets.** The overlap is the argument; do not redraw as a clean partition.
- Label values are abbreviated exactly as in the draft: `fe` and `be`, not `frontend` and `backend`. The abbreviations keep the cards narrow; expanding them breaks the column alignment the figure depends on.
- No containment. The Pods must not be drawn inside the sets, and the sets must not be drawn as boxes enclosing Pods — that would render exactly the folder structure the figure exists to refute.
- Set notation uses braces. Do not substitute bullet lists or arrows-to-groups.

**Source ASCII (for designer reference):**
```
  OBJECTS, each carrying labels

    ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐
    │  Pod A    │   │  Pod B    │   │  Pod C    │   │  Pod D    │
    │ tier=fe   │   │ tier=fe   │   │ tier=be   │   │ tier=be   │
    │ env=prod  │   │ env=dev   │   │ env=prod  │   │ env=dev   │
    └───────────┘   └───────────┘   └───────────┘   └───────────┘

  SELECTORS, each resolving to a set

    tier = fe                ──►   { A , B }
    env  = prod              ──►   { A ,     C }
    env in (prod, qa)        ──►   { A ,     C }
    tier = be , env = prod   ──►   {         C }
```

**Proposed filename:** `ch04-fig03-labels-selectors-join.png`

```yaml-figure-spec
anchor_id: ch04-fig03-labels-selectors-join
diagram_type: concept_map
source_ascii: |2
    OBJECTS, each carrying labels

      ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐
      │  Pod A    │   │  Pod B    │   │  Pod C    │   │  Pod D    │
      │ tier=fe   │   │ tier=fe   │   │ tier=be   │   │ tier=be   │
      │ env=prod  │   │ env=dev   │   │ env=prod  │   │ env=dev   │
      └───────────┘   └───────────┘   └───────────┘   └───────────┘

    SELECTORS, each resolving to a set

      tier = fe                ──►   { A , B }
      env  = prod              ──►   { A ,     C }
      env in (prod, qa)        ──►   { A ,     C }
      tier = be , env = prod   ──►   {         C }
vendor_terms: [Pod]
complexity_hint:
  node_count: 12
  edge_count: 4
  label_count: 20
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Explain that a label selector describes a set by attribute, so selected sets may overlap and need not partition the objects"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "Pod A, which appears in three of the four resolved sets"
accessibility:
  alt_text_seed: "Four Pod cards labelled A through D, each carrying a tier and an env label. Below them, four selectors resolve to sets: tier equals fe gives A and B; env equals prod gives A and C; env in prod or qa also gives A and C; tier equals be and env equals prod gives C alone. Pod A appears in three sets and Pod D in none."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Label keys follow the documentation's example vocabulary; the four-Pod worked example and its overlap are Lodestar's own construction."
```

---

## Figure: ch04-zenith-declaration-not-order

**Anchor ID:** `ch04-zenith-declaration-not-order` ⚠ *non-conforming ID — see ANCHOR FLAGS above. Preserved verbatim as the join key; do not rename without author sign-off.*
**Purpose:** Carries the chapter's ☀️ Zenith — that a filed declaration is read repeatedly, by many independent hands, at unrelated times, and that no hand ever receives an instruction.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** one-to-many fan-out diagram with temporal annotations on each branch

**Content specification:**
A single prominent box at the top, centered, headed **THE FILED DECLARATION** with the subordinate line *(what should be true)*. From its base, one line descends to a horizontal distribution bar, from which five branches drop to five terminals arranged in a row. Each branch carries a two-line annotation stacked along it: the word **"consulted"** above, and a timestamp below. The five timestamps, left to right: **09:00**, **09:04**, **09:04**, **11:20**, **03:17**. Each branch terminates at a rounded or parenthetical-styled terminal naming a reader: **a scheduler**, **a controller**, **a kubelet**, **a controller**, **a controller**. Beneath the row of terminals, set two lines of closing text across the full width, in body type rather than diagram type: **"No hand receives an instruction."** and **"Every hand reads the record, observes the world, and closes the gap."** The five terminals are deliberately unremarkable and equal in weight — none is the "main" consumer. The two repeated 09:04 timestamps must be visibly identical, and 03:17 must be visibly out of sequence relative to its neighbours; the disorder of the times is the content, not noise to be tidied.

**Design note for author review (not a rendering instruction):** in the source ASCII the arrows point *downward*, from the declaration to the five hands, which reads as a chain of command — the precise reading the caption at draft line 763 rejects ("every arrow is a reading"). The rendered figure should resolve this: either reverse the arrowheads so each hand reads *up* to the record, or use plain undirected connectors with the word "consulted" carrying the semantics. Recommend the undirected treatment, since reversed arrowheads on a fan-out read as aggregation. **This changes arrow semantics relative to the draft ASCII and therefore needs author sign-off before render.**

**Visual style:**
- Palette: book default — Navy `#0B1E3B` for the declaration box and the distribution structure, Teal `#1F4A4E` for the five terminals, Fog `#8A8D90` for the "consulted" annotations and timestamps, Cream `#F5EFE4` background
- Size (pixels): 1100x540 landscape
- Font: inherit book default (Fira Sans for the declaration heading and the two closing lines; Fira Mono for timestamps and terminal names)
- Accent color for highlighted elements: Brass `#B58B3E` for the declaration box border and heading — the record is the fixed thing every branch returns to, and it should be the only accented element

**Critical details (non-negotiable accuracy):**
- **Five branches, five distinct consultations.** Three of the five terminals are controllers; do not collapse them into one terminal with a multiplier, because the repetition is the argument.
- Timestamps are not ordered and two of them collide. Keep 09:00, 09:04, 09:04, 11:20, 03:17 exactly, in that left-to-right arrangement. Do not sort them; do not deduplicate 09:04.
- The declaration box is **singular**. There is exactly one record and it does not change across the five readings.
- No arrow in this figure may be styled as a command, dispatch, or message-send. No envelope glyphs, no "sends", no numbered steps.
- The terminals are roles, not instances: "a scheduler", "a controller", "a kubelet" — indefinite articles preserved. Do not name them `kube-scheduler` or `kubelet` as proper component names; the generality is deliberate at this point in the chapter.
- The two closing lines are part of the figure, not a caption. They must render inside the image, since the figure's separate italic caption sits beneath and says something different.

**Source ASCII (for designer reference):**
```
                    ┌─────────────────────────────┐
                    │    THE FILED DECLARATION    │
                    │    (what should be true)    │
                    └──────────────┬──────────────┘
                                   │
          ┌────────────┬───────────┼───────────┬────────────┐
          │            │           │           │            │
      consulted    consulted   consulted   consulted    consulted
       at 09:00     at 09:04    at 09:04    at 11:20     at 03:17
          │            │           │           │            │
          ▼            ▼           ▼           ▼            ▼
     ( a scheduler )( a controller )( a kubelet )( a controller )( a controller )

     No hand receives an instruction.
     Every hand reads the record, observes the world, and closes the gap.
```

**Proposed filename:** `ch04-zenith-declaration-not-order.png`

```yaml-figure-spec
anchor_id: ch04-zenith-declaration-not-order
diagram_type: concept_map
source_ascii: |2
                      ┌─────────────────────────────┐
                      │    THE FILED DECLARATION    │
                      │    (what should be true)    │
                      └──────────────┬──────────────┘
                                     │
            ┌────────────┬───────────┼───────────┬────────────┐
            │            │           │           │            │
        consulted    consulted   consulted   consulted    consulted
         at 09:00     at 09:04    at 09:04    at 11:20     at 03:17
            │            │           │           │            │
            ▼            ▼           ▼           ▼            ▼
       ( a scheduler )( a controller )( a kubelet )( a controller )( a controller )

       No hand receives an instruction.
       Every hand reads the record, observes the world, and closes the gap.
vendor_terms: [kubelet, scheduler, controller]
complexity_hint:
  node_count: 6
  edge_count: 5
  label_count: 13
pedagogy:
  part_18_criteria_met: [zenith, temporal_structure, spatial_structure]
  learning_outcome: "Explain that the author supplies the loop's reference rather than participating in it: one filed record is read repeatedly by independent components at unrelated times"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the single THE FILED DECLARATION box that all five branches return to"
accessibility:
  alt_text_seed: "A single box labelled THE FILED DECLARATION, what should be true, connected to five separate readers below it: a scheduler, a controller, a kubelet, and two more controllers, each annotated as consulting the record at a different time — 09:00, 09:04, 09:04, 11:20 and 03:17. Text beneath reads: no hand receives an instruction; every hand reads the record, observes the world, and closes the gap."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1100
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Component roles are generic Kubernetes terms; the consulted-at-times framing and the closing two lines are original Lodestar prose."
```

---

## UNANCHORED DIAGRAMS

**None.** All six ASCII diagrams in the draft carry a preceding `<!-- FIGURE: ... -->` anchor comment.

Three further fenced code blocks appear in the draft and were reviewed and **excluded** as code/data listings rather than diagrams. They require no anchor and no image spec; recording them here so a later audit does not re-open the question:

- **~L593–599** — a plain listing of the documentation's five example label key/value vocabularies (`release`, `environment`, `tier`, `partition`, `track`). Tabular data in a fence, not a figure. Renders as monospace inline; no illustration warranted.
- **~L681–684** — a two-line `matchLabels` YAML fragment inside Taking Your Bearings question 2. Question stimulus, not a diagram.
- **~L704–709** — the four-line `matchExpressions` YAML fragment in that question's answer. Answer text, not a diagram.
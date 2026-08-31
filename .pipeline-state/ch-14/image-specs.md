# Image Specifications — KCNA Chapter 14

*Generated from `draft-v1.md` (Stage 10 ran before `draft-voice.md` existed; the pipeline note at the head of the draft directs citation against `draft-v1.md`). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Six figure anchors found. Six entries below. One anchor is non-conforming (see immediately below). One unanchored fenced block found, classified as a code listing rather than a diagram — author to confirm.**

---

## NON-CONFORMING ANCHOR IDS

Rule 4 requires anchors to match `ch{NN}-fig{MM}-{kebab-slug}` exactly. One anchor does not:

| Anchor as written in draft | Problem | Suggested conforming ID |
|---|---|---|
| `ch14-zenith-package-not-template` | Missing the `fig{MM}` segment. Reads as `ch14-` + `zenith` where `fig06` belongs. | `ch14-fig06-package-not-template` |

**Not renamed here.** Per rule 6 the anchor ID is the join key and renaming is an author-review decision. The entry below preserves `ch14-zenith-package-not-template` verbatim in both the prose heading and the `anchor_id:` field. If the author approves the rename, it must change in **three** places in lockstep: the draft's anchor comment, this document's heading, and this document's `yaml-figure-spec` block. Until then, downstream tooling that validates anchor-ID shape will flag it.

Note the ID is *semantically* meaningful — this is the chapter's ☀️ Zenith figure — so the author may prefer a form that keeps the word, e.g. `ch14-fig06-zenith-package-not-template`. Either conforms; the bare `ch14-zenith-...` does not.

---

## UNANCHORED DIAGRAMS

### ~§2 — `templates/` — what gets created (fenced block following "Here is a fragment of a Deployment template beside what it renders to:")

```
Template (in templates/deployment.yaml):

    spec:
      replicas: {{ .Values.replicaCount }}

With values.yaml containing `replicaCount: 3`, this renders to:

    spec:
      replicas: 3
```

Suggested anchor: **none — recommend leaving unanchored.** This is a two-part code listing (template fragment beside rendered output), not a spatial or structural diagram. It has no boxes, no arrows, and no relationships that a redrawn figure would clarify; setting it as a figure would spend an illustration on YAML that the reader can read directly, which Part 18 forbids (decorative / no distinct spatial contribution). Flagged here only because rule 3 asks for every unanchored fenced block to surface. **Author to confirm "no figure" before the structural audit treats the absence as an error.**

If the author disagrees and wants it rendered, the natural form is a two-panel before/after with the `{{ .Values.replicaCount }}` token and the resolved `3` both in Brass — but the recommendation stands against it.

---

## BLOCKING AUTHOR-REVIEW CARRIED FORWARD

The draft carries an `AUTHOR-REVIEW` comment immediately below **ch14-fig03** that constrains the figure's content. It is reproduced in that figure's Critical Details and repeated here because it is the single highest-risk item in this chapter's figure set:

> The cached corpus does not establish whether a `helm rollback` is itself recorded as a new numbered revision. Figure ch14-fig03 deliberately shows the fourth box as `rev 4 / ???`. **A designer or renderer must not "clean up" the `???` by writing `rollback` into that box.** Doing so asserts a fact the book has not sourced, and would contradict the prose, which declines to state the counter behaviour.

A second `AUTHOR-REVIEW` sits at the end of §5 (Kustomize corpus is thin). It bears on **ch14-fig04**: the `configMapGenerator` name-hash-suffix behaviour is deliberately absent from the prose and **must not appear in the figure** either.

---

## Figure: ch14-fig01-manifest-to-package-progression

**Anchor ID:** `ch14-fig01-manifest-to-package-progression`
**Purpose:** Show the reader the exact moment a folder of manifests stops working — one cluster is fine, three clusters produce near-duplicate directories with unmarked differences — and name the packaged alternative as the destination, supporting §1's "failure one: environment variation."
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** three-panel comparative progression (left-to-right), each panel a small file-tree-and-target composition

**Content specification:**
Three vertical panels side by side, separated by generous whitespace, each under its own heading rule: **ONE CLUSTER**, **THREE CLUSTERS**, **WHAT YOU WANT**. The left panel shows a single folder labelled `manifests/` containing three file labels (`deployment.yaml`, `service.yaml`, `configmap.yaml`), a single downward arrow, and one box labelled `cluster`; beneath it, in body type, the caption *"Correct. Keep doing this."* — this panel must read as endorsed, not as a strawman. The centre panel shows three folders stacked vertically — `manifests-dev/`, `manifests-staging/`, `manifests-prod/` — each containing the identical three file labels; a single tall brace or bracket spans all three on their right, annotated *"95% identical, and nothing marks the 5%"*. Below the centre panel, running its full width, a band reading **THIS IS WHERE MOST TEAMS LIVE** — this band is the point of the figure and must be the first thing the eye lands on. The right panel shows one box labelled `package v1.2.0` with the sub-label *"(one copy, versioned)"*, three small value-file labels beneath it (`+ dev-values`, `+ staging-values`, `+ prod-values`), and a three-way fan of arrows down to three small cluster boxes labelled `dev`, `stg`, `prd`. The visual argument is carried by count: three full directories in the centre versus one package plus three thin value files on the right.

**Visual style:**
- Palette: brand navy on off-white; inherit book default
- Size (pixels): 1200 x 760 landscape
- Font: inherit book default (Roboto Slab for panel headings, Fira Sans for captions, Fira Mono for all filenames and directory names)
- Accent color for highlighted elements: Brass (#B58B3E) for the "THIS IS WHERE MOST TEAMS LIVE" band and for the 95%-identical bracket. Everything else navy/grey.

**Critical details (non-negotiable accuracy):**
- Panel order is left-to-right **ONE CLUSTER → THREE CLUSTERS → WHAT YOU WANT**. Reversing or reordering destroys the argument.
- The left panel must not be styled as an error state. The prose explicitly says this arrangement "is correct, and you should keep doing this." No red, no warning glyph, no strike-through.
- The centre panel's three directories must contain **identical** filename lists. The whole point is that nothing distinguishes them visually — do not helpfully differentiate them.
- Directory names are exactly `manifests/`, `manifests-dev/`, `manifests-staging/`, `manifests-prod/`. Files are exactly `deployment.yaml`, `service.yaml`, `configmap.yaml`.
- The right panel is labelled `package v1.2.0` — a generic package, **not** a Helm chart. Helm has not been introduced at this point in the chapter. Do not add a Helm logo, the word "chart", or `Chart.yaml`.
- Three clusters on the right, labelled `dev` / `stg` / `prd`, matching the three overlay-value labels one-to-one.
- The source ASCII contains an alignment artifact — a stray `│` at the end of the "and nothing" line, and a partial `┌──────┼──────┐` fragment that belongs to the right panel's fan. The redrawn figure should render the intended structure (bracket on the centre panel, three-way fan on the right panel) and drop the artifact.

**Source ASCII (for designer reference):**
```
  ONE CLUSTER                THREE CLUSTERS                  WHAT YOU WANT
  ───────────                ──────────────                  ─────────────

  manifests/                 manifests-dev/     ◄─┐          package v1.2.0
    deployment.yaml            deployment.yaml    │            (one copy,
    service.yaml               service.yaml       │             versioned)
    configmap.yaml             configmap.yaml     │
                                                  │          + dev-values
       │                     manifests-staging/   │          + staging-values
       ▼                       deployment.yaml    ├─ 95%      + prod-values
   ┌────────┐                  service.yaml       │  identical
   │cluster │                  configmap.yaml     │  and nothing              │
   └────────┘                                     │  marks the 5%      ┌──────┼──────┐
                             manifests-prod/      │                    ▼      ▼      ▼
   Correct. Keep              deployment.yaml     │                 ┌───┐  ┌───┐  ┌───┐
   doing this.                service.yaml        │                 │dev│  │stg│  │prd│
                              configmap.yaml    ◄─┘                 └───┘  └───┘  └───┘

                             ▲▲▲ THIS IS WHERE MOST TEAMS LIVE ▲▲▲
```

**Proposed filename:** `ch14-fig01-manifest-to-package-progression.png`

```yaml-figure-spec
anchor_id: ch14-fig01-manifest-to-package-progression
diagram_type: concept_map
source_ascii: |2
    ONE CLUSTER                THREE CLUSTERS                  WHAT YOU WANT
    ───────────                ──────────────                  ─────────────

    manifests/                 manifests-dev/     ◄─┐          package v1.2.0
      deployment.yaml            deployment.yaml    │            (one copy,
      service.yaml               service.yaml       │             versioned)
      configmap.yaml             configmap.yaml     │
                                                    │          + dev-values
         │                     manifests-staging/   │          + staging-values
         ▼                       deployment.yaml    ├─ 95%      + prod-values
     ┌────────┐                  service.yaml       │  identical
     │cluster │                  configmap.yaml     │  and nothing              │
     └────────┘                                     │  marks the 5%      ┌──────┼──────┐
                               manifests-prod/      │                    ▼      ▼      ▼
     Correct. Keep              deployment.yaml     │                 ┌───┐  ┌───┐  ┌───┐
     doing this.                service.yaml        │                 │dev│  │stg│  │prd│
                                configmap.yaml    ◄─┘                 └───┘  └───┘  └───┘

                               ▲▲▲ THIS IS WHERE MOST TEAMS LIVE ▲▲▲
vendor_terms: []
complexity_hint:
  node_count: 12
  edge_count: 6
  label_count: 22
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Recognize that a folder of manifests cannot express environment variation, and that the answer is one versioned package plus per-environment values"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The centre panel's 'THIS IS WHERE MOST TEAMS LIVE' band and the 95%-identical bracket beside the three near-duplicate directories"
accessibility:
  alt_text_seed: "Three-panel comparison: one manifests directory deploying to one cluster, labelled correct; three near-identical directories for dev, staging and production bracketed as ninety-five percent identical with nothing marking the difference, labelled as where most teams live; and one versioned package plus three per-environment value files fanning out to three clusters"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic directory names, filenames and cluster boxes only; no vendor mark, logo or product name appears."
```

---

## Figure: ch14-fig02-helm-chart-anatomy

**Anchor ID:** `ch14-fig02-helm-chart-anatomy`
**Purpose:** Give the reader a labelled anatomy of a Helm chart directory in which each entry is annotated with *what it is for* rather than what it is, and in which the `charts/`-is-not-a-repository trap is called out at the point of confusion.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** annotated hierarchical tree (single root, callout annotations to the right)

**Content specification:**
A left-aligned directory tree rooted at `wordpress/`, rendered with conventional tree connectors, with a callout column to its right. Five root-level entries carry full annotations, each introduced by a horizontal leader line into a short annotation block: `Chart.yaml` → **WHO THIS CHART IS.** *"Name, version, description. Every chart must have this file."*; `values.yaml` → **THE KNOBS, AND THEIR DEFAULTS.** *"Everything the installer is allowed to change, with a working value for each."*; `templates/` → **WHAT GETS CREATED.** *"Combined with values, generates valid Kubernetes manifests."*; `charts/` → **CHARTS THIS CHART DEPENDS ON.** followed by the emphasised line **NOT A REPOSITORY.** and then *"A directory, inside this chart, holding other charts. See §4 for repositories."*; `crds/` → **DEFINITIONS THAT MUST EXIST FIRST.** *"Not templated. Installed before the templates render. See §6 for why."* Nested one level under `templates/` are four children: `deployment.yaml`, `service.yaml`, `NOTES.txt`, `_helpers.tpl`. Two root entries, `LICENSE` and `README.md`, sit at the bottom unannotated. `NOTES.txt`, `_helpers.tpl`, `LICENSE` and `README.md` are set in a muted grey with parenthetical sub-labels — grey here means "does not become a Kubernetes object and/or is optional," and that greying is load-bearing, not decorative. The **NOT A REPOSITORY** line is the emphasised element of the whole figure.

**Visual style:**
- Palette: brand navy on off-white; muted grey (approximately 45% navy) for the four de-emphasised entries; inherit book default otherwise
- Size (pixels): 900 x 1150 portrait
- Font: inherit book default (Fira Mono for every path and filename, Roboto Slab for the all-caps annotation headers, Fira Sans for the annotation bodies)
- Accent color for highlighted elements: Brass (#B58B3E) for the **NOT A REPOSITORY** line only. One Brass element in this figure, no more.

**Critical details (non-negotiable accuracy):**
- The root directory is `wordpress/` — the chart's directory name is the chart's name, with no version in it. Do not write `wordpress-15.2.0/`.
- `NOTES.txt` and `_helpers.tpl` are **inside** `templates/`, indented one level. They are not root-level entries.
- `crds/` and `charts/` are **root-level siblings** of `templates/`, not children of it.
- The grey treatment marks *optional or non-manifest*; it must survive greyscale rendering as a visible weight/tone difference, since the parentheticals carry the same information redundantly.
- `_helpers.tpl` is annotated "partials, not manifests" — it must not be shown as producing objects. `NOTES.txt` is annotated "usage notes printed on install."
- The section pointers "See §4 for repositories" and "See §6 for why" refer to sections of **this chapter** and must be reproduced exactly. If chapter section numbering changes, this figure needs regenerating.
- `Chart.yaml` and `values.yaml` are files at the root; `templates/`, `charts/`, `crds/` are directories and should carry the trailing slash.
- Do not add entries the source does not show (no `Chart.lock`, no `templates/tests/`, no `.helmignore`). The figure's completeness claim is bounded by what the prose covers.

**Source ASCII (for designer reference):**
```
  wordpress/
  │
  ├── Chart.yaml ─────────► WHO THIS CHART IS.
  │                         Name, version, description. Every chart
  │                         must have this file.
  │
  ├── values.yaml ────────► THE KNOBS, AND THEIR DEFAULTS.
  │                         Everything the installer is allowed to
  │                         change, with a working value for each.
  │
  ├── templates/ ─────────► WHAT GETS CREATED.
  │                         Combined with values, generates valid
  │                         Kubernetes manifests.
  │     ├── deployment.yaml
  │     ├── service.yaml
  │     ├── NOTES.txt          (grey: usage notes printed on install)
  │     └── _helpers.tpl       (grey: partials, not manifests)
  │
  ├── charts/ ────────────► CHARTS THIS CHART DEPENDS ON.
  │                         *** NOT A REPOSITORY. ***
  │                         A directory, inside this chart, holding
  │                         other charts. See §4 for repositories.
  │
  ├── crds/ ──────────────► DEFINITIONS THAT MUST EXIST FIRST.
  │                         Not templated. Installed before the
  │                         templates render. See §6 for why.
  │
  ├── LICENSE                  (grey: optional)
  └── README.md                (grey: optional)
```

**Proposed filename:** `ch14-fig02-helm-chart-anatomy.png`

```yaml-figure-spec
anchor_id: ch14-fig02-helm-chart-anatomy
diagram_type: hierarchy_tree
source_ascii: |2
    wordpress/
    │
    ├── Chart.yaml ─────────► WHO THIS CHART IS.
    │                         Name, version, description. Every chart
    │                         must have this file.
    │
    ├── values.yaml ────────► THE KNOBS, AND THEIR DEFAULTS.
    │                         Everything the installer is allowed to
    │                         change, with a working value for each.
    │
    ├── templates/ ─────────► WHAT GETS CREATED.
    │                         Combined with values, generates valid
    │                         Kubernetes manifests.
    │     ├── deployment.yaml
    │     ├── service.yaml
    │     ├── NOTES.txt          (grey: usage notes printed on install)
    │     └── _helpers.tpl       (grey: partials, not manifests)
    │
    ├── charts/ ────────────► CHARTS THIS CHART DEPENDS ON.
    │                         *** NOT A REPOSITORY. ***
    │                         A directory, inside this chart, holding
    │                         other charts. See §4 for repositories.
    │
    ├── crds/ ──────────────► DEFINITIONS THAT MUST EXIST FIRST.
    │                         Not templated. Installed before the
    │                         templates render. See §6 for why.
    │
    ├── LICENSE                  (grey: optional)
    └── README.md                (grey: optional)
vendor_terms: [helm, wordpress]
complexity_hint:
  node_count: 12
  edge_count: 16
  label_count: 17
pedagogy:
  part_18_criteria_met: [spatial_structure, vendor_taxonomy, fixed_point]
  learning_outcome: "Read a Helm chart's directory layout and say what each entry is for, and distinguish the in-chart charts/ directory from a chart repository"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The 'NOT A REPOSITORY.' line annotating the charts/ directory"
accessibility:
  alt_text_seed: "Directory tree of a Helm chart named wordpress, with Chart.yaml, values.yaml, templates, charts and crds each annotated with its purpose; the charts directory is marked emphatically as not a repository but a directory inside the chart holding its dependencies"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 900
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Helm chart layout redrawn in Lodestar style from the project's documented structure; no logos or vendor artwork. 'wordpress' appears as a directory name in nominative use, following Helm's own documentation example."
```

---

## Figure: ch14-fig03-release-vs-chart-vs-revision

**Anchor ID:** `ch14-fig03-release-vs-chart-vs-revision`
**Purpose:** Separate the three words §3 exists to keep apart — chart, Helm release, release revision — by showing one chart installing twice into two independent releases, one of which carries its own numbered revision history.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hierarchical fan-out with a horizontal revision timeline attached to one branch

**Content specification:**
Top centre: a single wide box labelled **CHART: wordpress 15.2.0**, with the parenthetical body text *"a package. on the shelf. installed zero times so far in this diagram."* From its bottom edge, a single stem splits into two arrows fanning down-left and down-right, each labelled `helm install`. The left arrow lands on a box labelled **RELEASE: "marketing"** with two sub-lines, `namespace: marketing` and `values: 12 replicas`. The right arrow lands on a box labelled **RELEASE: "docs"** with sub-lines `namespace: docs` and `values: 2 replicas`; immediately to the right of or beneath the docs box, in italic body type, the annotation *"its own history, untouched by anything done to 'marketing'"* — the docs branch deliberately stops there, with no revision chain, which is itself the point. From the bottom of the marketing box, a single arrow descends to a horizontal chain of four small equal boxes reading `rev 1 / install`, `rev 2 / upgrade`, `rev 3 / upgrade`, `rev 4 / ???`, connected left-to-right by three arrows. A curved arrow rises from below and points at the **rev 2** box, labelled *"helm rollback marketing 2 — returns the release to revision 2's state."* The fourth box's `???` is intentional and must be preserved literally.

**Visual style:**
- Palette: brand navy on off-white; inherit book default. The two release boxes get identical treatment — neither is "the main one."
- Size (pixels): 1100 x 900 landscape
- Font: inherit book default (Fira Mono for `helm install`, `helm rollback marketing 2`, release names, namespaces and `rev N`; Fira Sans for the italic annotations)
- Accent color for highlighted elements: Brass (#B58B3E) for the two divergent `helm install` arrows fanning from the single chart box — the one-chart-many-releases move is the figure's argument.

**Critical details (non-negotiable accuracy):**
- **The `rev 4 / ???` box must ship with the `???` intact.** The draft's `AUTHOR-REVIEW` comment states the cached corpus does not establish whether a `helm rollback` is itself recorded as a new numbered revision. Writing `rollback`, `rev 4 = rev 2`, or anything else into that box asserts an unsourced fact and contradicts the prose, which deliberately declines to state the counter behaviour. **This is a blocking constraint, not a style preference.** If the author later resolves it from a fetched source, this figure regenerates.
- The rollback arrow points at **rev 2**, not at rev 4 and not at rev 1. It represents `helm rollback marketing 2`.
- The `docs` release has **no** revision chain drawn. Adding one would undercut the "untouched by anything done to marketing" annotation.
- The chart box says "installed zero times so far in this diagram" — the chart is a package, not an installation. Do not draw the chart inside a cluster, and do not draw a cluster in this figure at all.
- Replica counts are asymmetric on purpose: marketing 12, docs 2. Do not normalise them.
- Namespaces match release names in this example (`marketing` in namespace `marketing`, `docs` in namespace `docs`). Preserve that.
- Chart version `15.2.0` is illustrative; keep it as written so it matches nothing else in the chapter and cannot be mistaken for an `appVersion`.
- Revision boxes read left-to-right in ascending order. Time flows right; the rollback arrow moving *backward* against that flow is what makes the rollback legible.

**Source ASCII (for designer reference):**
```
                        ┌──────────────────────────────┐
                        │   CHART:  wordpress 15.2.0   │
                        │   (a package. on the shelf.  │
                        │    installed zero times so   │
                        │    far in this diagram.)     │
                        └───────────┬──────────────────┘
                                    │
              helm install ─────────┴───────── helm install
                     │                              │
                     ▼                              ▼
        ┌─────────────────────────┐   ┌─────────────────────────┐
        │ RELEASE: "marketing"    │   │ RELEASE: "docs"         │
        │ namespace: marketing    │   │ namespace: docs         │
        │ values: 12 replicas     │   │ values: 2 replicas      │
        └───────────┬─────────────┘   └─────────────────────────┘
                    │                    (its own history,
                    │                     untouched by anything
                    │                     done to "marketing")
                    ▼
    ┌───────┐   ┌───────┐   ┌───────┐   ┌───────┐
    │ rev 1 │──►│ rev 2 │──►│ rev 3 │──►│ rev 4 │
    │install│   │upgrade│   │upgrade│   │  ???  │
    └───────┘   └───────┘   └───────┘   └───────┘
                                ▲
                                └─ helm rollback marketing 2
                                   returns the release to
                                   revision 2's state.
```

**Proposed filename:** `ch14-fig03-release-vs-chart-vs-revision.png`

```yaml-figure-spec
anchor_id: ch14-fig03-release-vs-chart-vs-revision
diagram_type: hierarchy_tree
source_ascii: |2
                          ┌──────────────────────────────┐
                          │   CHART:  wordpress 15.2.0   │
                          │   (a package. on the shelf.  │
                          │    installed zero times so   │
                          │    far in this diagram.)     │
                          └───────────┬──────────────────┘
                                      │
                helm install ─────────┴───────── helm install
                       │                              │
                       ▼                              ▼
          ┌─────────────────────────┐   ┌─────────────────────────┐
          │ RELEASE: "marketing"    │   │ RELEASE: "docs"         │
          │ namespace: marketing    │   │ namespace: docs         │
          │ values: 12 replicas     │   │ values: 2 replicas      │
          └───────────┬─────────────┘   └─────────────────────────┘
                      │                    (its own history,
                      │                     untouched by anything
                      │                     done to "marketing")
                      ▼
      ┌───────┐   ┌───────┐   ┌───────┐   ┌───────┐
      │ rev 1 │──►│ rev 2 │──►│ rev 3 │──►│ rev 4 │
      │install│   │upgrade│   │upgrade│   │  ???  │
      └───────┘   └───────┘   └───────┘   └───────┘
                                  ▲
                                  └─ helm rollback marketing 2
                                     returns the release to
                                     revision 2's state.
vendor_terms: [helm, wordpress]
complexity_hint:
  node_count: 7
  edge_count: 6
  label_count: 13
pedagogy:
  part_18_criteria_met: [spatial_structure, temporal_structure, fixed_point]
  learning_outcome: "Separate chart from Helm release from release revision, and see that one chart installs many times with independent histories"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The two divergent helm install arrows fanning from the single chart box to two independently-named releases"
accessibility:
  alt_text_seed: "One Helm chart at the top installs twice, producing two independent releases named marketing and docs in separate namespaces with different replica counts; the marketing release has a left-to-right chain of numbered revisions, and a rollback arrow points back at revision two"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Helm release model redrawn in Lodestar style from project documentation; no logos. 'wordpress' is a nominative chart-name example."
```

---

## Figure: ch14-fig04-kustomize-base-overlay

**Anchor ID:** `ch14-fig04-kustomize-base-overlay`
**Purpose:** Show that a Kustomize overlay declares only its deltas and *references* an unmodified base, replacing the reader's default assumption that the base is copied or edited — the single most common wrong model of Kustomize.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** component diagram — two peers referencing one shared component, then diverging into two applied outcomes

**Content specification:**
Two boxes across the top, left and right, headed `overlays/staging/` and `overlays/prod/`. Each contains a `kustomization.yaml` label followed by four indented field lines in monospace: the staging box reads `resources:` / `- ../../base` / `namePrefix: stg-` / `replicas: 2` / `patches: [...]`; the prod box reads the same with `namePrefix: prod-` and `replicas: 12`. Each box closes with the emphasised line **ONLY THE DELTAS**. From the bottom of each overlay box, one arrow runs down and inward to a single centred box headed `base/`, containing `kustomization.yaml`, `deployment.yaml`, `service.yaml`, and then three emphasised lines: **NEVER EDITED. NEVER COPIED. ONE OF IT.** These two inbound arrows must be labelled — "references" or "resources:" — because they mean *this overlay points at that base*, not *content flows downward*. Below the base box, a separate flow: a stem descends and splits into two, each branch labelled with a command in monospace, `kubectl apply -k overlays/staging` and `kubectl apply -k overlays/prod`, each descending to a result label — `stg- objects, 2 replicas` on the left, `prod- objects, 12 replicas` on the right. The centre base box is the emphasised element; the visual claim is that there is exactly one of it and both overlays point at the same one.

**Visual style:**
- Palette: brand navy on off-white; inherit book default. Staging and prod branches get identical weight — neither is primary.
- Size (pixels): 1200 x 900 landscape
- Font: inherit book default (Fira Mono for all paths, field names, field values and commands; Roboto Slab for the emphasised all-caps lines)
- Accent color for highlighted elements: Brass (#B58B3E) for the `base/` box border and its NEVER EDITED / NEVER COPIED / ONE OF IT lines.

**Critical details (non-negotiable accuracy):**
- There is exactly **one** base box. Drawing two, or drawing a copy of the base inside each overlay, inverts the figure's entire meaning and reproduces failure one from §1.
- The overlay→base arrows mean **reference**, not data flow. Label them. The source ASCII's arrowheads point *into* the base, which reads ambiguously; the redrawn figure should disambiguate with an edge label.
- `namePrefix` values are `stg-` and `prod-` with the trailing hyphen. The outcome labels correspondingly read `stg- objects` and `prod- objects` — the prefix appearing in the outcome is the "and references" behaviour paying off.
- Replica counts are 2 (staging) and 12 (prod), and they must match between the overlay field and the outcome label.
- The relative path is `../../base` — two levels up, because overlays live at `overlays/<name>/`. Do not simplify to `../base`.
- The command is `kubectl apply -k` (lowercase `-k`), pointed at the **overlay** directory, never at the base. This is the "built into kubectl" claim made visible.
- `patches: [...]` is deliberately elided. Do not expand it into a worked patch; §5's patch-style discussion is prose, not figure.
- **Do not add `configMapGenerator`, and do not depict the generated-name hash suffix.** The draft's §5 `AUTHOR-REVIEW` records that behaviour as unsourced and deliberately omitted from the prose; it must stay out of the figure too.
- No Helm elements anywhere in this figure. No `values.yaml`, no chart, no rendering step — the absence of a template engine is the point.

**Source ASCII (for designer reference):**
```
        overlays/staging/                                overlays/prod/
        ┌────────────────────┐                       ┌────────────────────┐
        │ kustomization.yaml │                       │ kustomization.yaml │
        │  resources:        │                       │  resources:        │
        │    - ../../base    │                       │    - ../../base    │
        │  namePrefix: stg-  │                       │  namePrefix: prod- │
        │  replicas: 2       │                       │  replicas: 12      │
        │  patches: [...]    │                       │  patches: [...]    │
        │                    │                       │                    │
        │  ONLY THE DELTAS   │                       │  ONLY THE DELTAS   │
        └─────────┬──────────┘                       └──────────┬─────────┘
                  │                                             │
                  │          base/                              │
                  │      ┌───────────────────────┐              │
                  └─────►│ kustomization.yaml    │◄─────────────┘
                         │ deployment.yaml       │
                         │ service.yaml          │
                         │                       │
                         │  NEVER EDITED.        │
                         │  NEVER COPIED.        │
                         │  ONE OF IT.           │
                         └───────────┬───────────┘
                                     │
                  ┌──────────────────┴──────────────────┐
                  ▼                                     ▼
        kubectl apply -k overlays/staging     kubectl apply -k overlays/prod
                  │                                     │
                  ▼                                     ▼
           stg- objects, 2 replicas            prod- objects, 12 replicas
```

**Proposed filename:** `ch14-fig04-kustomize-base-overlay.png`

```yaml-figure-spec
anchor_id: ch14-fig04-kustomize-base-overlay
diagram_type: component_diagram
source_ascii: |2
          overlays/staging/                                overlays/prod/
          ┌────────────────────┐                       ┌────────────────────┐
          │ kustomization.yaml │                       │ kustomization.yaml │
          │  resources:        │                       │  resources:        │
          │    - ../../base    │                       │    - ../../base    │
          │  namePrefix: stg-  │                       │  namePrefix: prod- │
          │  replicas: 2       │                       │  replicas: 12      │
          │  patches: [...]    │                       │  patches: [...]    │
          │                    │                       │                    │
          │  ONLY THE DELTAS   │                       │  ONLY THE DELTAS   │
          └─────────┬──────────┘                       └──────────┬─────────┘
                    │                                             │
                    │          base/                              │
                    │      ┌───────────────────────┐              │
                    └─────►│ kustomization.yaml    │◄─────────────┘
                           │ deployment.yaml       │
                           │ service.yaml          │
                           │                       │
                           │  NEVER EDITED.        │
                           │  NEVER COPIED.        │
                           │  ONE OF IT.           │
                           └───────────┬───────────┘
                                       │
                    ┌──────────────────┴──────────────────┐
                    ▼                                     ▼
          kubectl apply -k overlays/staging     kubectl apply -k overlays/prod
                    │                                     │
                    ▼                                     ▼
             stg- objects, 2 replicas            prod- objects, 12 replicas
vendor_terms: [kustomize, kubectl]
complexity_hint:
  node_count: 7
  edge_count: 6
  label_count: 21
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives, fixed_point]
  learning_outcome: "Explain that a Kustomize overlay declares only deltas against a base that is neither edited nor copied, and that apply -k needs no engine installed"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The single centred base/ box carrying the lines NEVER EDITED, NEVER COPIED, ONE OF IT"
accessibility:
  alt_text_seed: "Two Kustomize overlay directories for staging and production, each listing only its own deltas, both referencing a single shared base directory that is never edited and never copied; applying each overlay with kubectl apply -k produces prefixed objects with different replica counts"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Kustomize base/overlay arrangement redrawn in Lodestar style from project documentation; no logos or vendor artwork."
```

---

## Figure: ch14-fig05-templating-vs-overlay-decision

**Anchor ID:** `ch14-fig05-templating-vs-overlay-decision`
**Purpose:** Put Helm and Kustomize side by side on five axes and then close with the one distinction the choice actually turns on, so the reader leaves §6 with a decision rule rather than a preference.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-column comparison matrix with a full-width decision band beneath it (no direct entry in the controlled vocabulary — `diagram_type: other`, router falls back to D2)

**Content specification:**
A five-row comparison table with a header row and two content columns. Header: blank stub cell, then **HELM**, then **KUSTOMIZE**. Row stubs down the left, in this order: *What varies*, *The unit*, *Distribution*, *Lifecycle*, *Where the engine lives*. Helm column cells, in order: "values, filling holes in templates"; "a versioned chart (version REQUIRED)"; "chart repository, or an OCI registry"; "releases and revisions; install / upgrade / rollback as single acts"; "a CLI you install". Kustomize column cells, in order: "patches, applied to a complete base"; "a directory. no version (nothing requires one)"; "none. it's your repo."; "none. apply is apply. no installed-state record of its own"; "in kubectl. `apply -k` Nothing to install." Beneath the table, spanning its full width as a single merged band, a heading **WHAT THE CHOICE ACTUALLY TURNS ON:** followed by two lines, each ending in a long arrow to a right-aligned verdict: *"Distributing to strangers who won't read it"* → **HELM**; *"Adapting what you already have, for yourself"* → **KUSTOMIZE**. That closing band is the figure — the table above it is supporting evidence.

**Visual style:**
- Palette: brand navy rules and header fill on off-white; alternating row tint optional but must remain legible in greyscale; inherit book default
- Size (pixels): 1200 x 820 landscape
- Font: inherit book default (Roboto Slab for the two column headers and the decision band heading, Fira Sans for cell text, Fira Mono for `apply -k`)
- Accent color for highlighted elements: Brass (#B58B3E) for the decision band's two arrows and the two verdict words HELM and KUSTOMIZE within that band only. The table's own HELM / KUSTOMIZE headers stay navy, so the eye distinguishes the evidence from the verdict.

**Critical details (non-negotiable accuracy):**
- Both columns must read as legitimate. The Kustomize column contains four instances of the word "none," and those are *scope statements, not deficiencies* — §6 says explicitly that this is "a smaller tool solving the subset of the problem that occurs when there is nobody to distribute to." Do not style the Kustomize column with warning colour, greyed text, or ✗ marks.
- Row order must not be rearranged. It runs mechanism → unit → distribution → lifecycle → engine location, ending on the practical fact that leads into the decision.
- "version REQUIRED" is capitalised for emphasis in the Helm cell and "nothing requires one" is the Kustomize counterpart. Both are load-bearing: a version is required on every chart, and nothing requires one of a directory.
- The engine row is the practical asymmetry: Helm is a CLI you install; Kustomize is in kubectl. Reversing this is a factual error.
- The decision band's two lines map one-to-one: *distributing → Helm*, *adapting → Kustomize*. Do not soften either into "usually" or "often."
- `apply -k` must be set in monospace and must keep the lowercase `-k`.
- The table has no third column, no "both" column, and no verdict row inside the table. The combined-use case is prose in §6, not this figure.

**Source ASCII (for designer reference):**
```
  ┌────────────────────┬──────────────────────────┬──────────────────────────┐
  │                    │  HELM                    │  KUSTOMIZE               │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ What varies        │  values, filling holes   │  patches, applied to a   │
  │                    │  in templates            │  complete base           │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ The unit           │  a versioned chart       │  a directory. no version │
  │                    │  (version REQUIRED)      │  (nothing requires one)  │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ Distribution       │  chart repository, or    │  none. it's your repo.   │
  │                    │  an OCI registry         │                          │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ Lifecycle          │  releases and revisions; │  none. apply is apply.   │
  │                    │  install/upgrade/rollback│  no installed-state      │
  │                    │  as single acts          │  record of its own       │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ Where the engine   │  a CLI you install       │  in kubectl. `apply -k`  │
  │ lives              │                          │  Nothing to install.     │
  ├────────────────────┴──────────────────────────┴──────────────────────────┤
  │  WHAT THE CHOICE ACTUALLY TURNS ON:                                      │
  │  Distributing to strangers who won't read it  ─────────────►  HELM       │
  │  Adapting what you already have, for yourself ─────────────►  KUSTOMIZE  │
  └──────────────────────────────────────────────────────────────────────────┘
```

**Proposed filename:** `ch14-fig05-templating-vs-overlay-decision.png`

```yaml-figure-spec
anchor_id: ch14-fig05-templating-vs-overlay-decision
diagram_type: other
source_ascii: |2
    ┌────────────────────┬──────────────────────────┬──────────────────────────┐
    │                    │  HELM                    │  KUSTOMIZE               │
    ├────────────────────┼──────────────────────────┼──────────────────────────┤
    │ What varies        │  values, filling holes   │  patches, applied to a   │
    │                    │  in templates            │  complete base           │
    ├────────────────────┼──────────────────────────┼──────────────────────────┤
    │ The unit           │  a versioned chart       │  a directory. no version │
    │                    │  (version REQUIRED)      │  (nothing requires one)  │
    ├────────────────────┼──────────────────────────┼──────────────────────────┤
    │ Distribution       │  chart repository, or    │  none. it's your repo.   │
    │                    │  an OCI registry         │                          │
    ├────────────────────┼──────────────────────────┼──────────────────────────┤
    │ Lifecycle          │  releases and revisions; │  none. apply is apply.   │
    │                    │  install/upgrade/rollback│  no installed-state      │
    │                    │  as single acts          │  record of its own       │
    ├────────────────────┼──────────────────────────┼──────────────────────────┤
    │ Where the engine   │  a CLI you install       │  in kubectl. `apply -k`  │
    │ lives              │                          │  Nothing to install.     │
    ├────────────────────┴──────────────────────────┴──────────────────────────┤
    │  WHAT THE CHOICE ACTUALLY TURNS ON:                                      │
    │  Distributing to strangers who won't read it  ─────────────►  HELM       │
    │  Adapting what you already have, for yourself ─────────────►  KUSTOMIZE  │
    └──────────────────────────────────────────────────────────────────────────┘
vendor_terms: [helm, kustomize, kubectl]
complexity_hint:
  node_count: 18
  edge_count: 2
  label_count: 20
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, vendor_taxonomy]
  learning_outcome: "Choose between Helm and Kustomize for a given situation and state what the choice turns on"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The full-width decision band beneath the table: distributing to strangers points to Helm, adapting what you already have points to Kustomize"
accessibility:
  alt_text_seed: "Comparison table of Helm and Kustomize across five rows — what varies, the unit, distribution, lifecycle, and where the engine lives — closing with a decision band stating that distributing to strangers who will not read it points to Helm, while adapting what you already have for yourself points to Kustomize"
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Comparison authored by Lodestar from each project's documented properties; product names in nominative use, no logos or vendor artwork."
```

---

## Figure: ch14-zenith-package-not-template

> **⚠ Non-conforming anchor ID** — missing the `fig{MM}` segment; see the NON-CONFORMING ANCHOR IDS section at the top of this document. Preserved verbatim here as the join key pending author decision. Suggested conforming ID: `ch14-fig06-package-not-template`.

**Anchor ID:** `ch14-zenith-package-not-template`
**Purpose:** Carry the chapter's ☀️ Zenith — two mechanisms that could not be more different converge on the same destination, and the destination, not the mechanism, is the point.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** convergent flow — two symmetric parallel paths merging into one node, then a single step to a terminal node

**Content specification:**
Two parallel columns, left and right, each headed by a word in display type with a heavy rule beneath it: **RENDER** on the left, **PATCH** on the right. Under RENDER: the label `templates/ + values`, a short connector down into a process box reading *"fill in holes"*, then a connector continuing down and inward. Under PATCH, mirrored: the label `base/ + overlay/`, a process box reading *"merge deltas"*, then a connector down and inward. The two inward connectors meet a single large centred box, entered from left and right by opposing arrowheads, reading across three lines: **ONE NAMED, VERSIONED, INSTALLABLE UNIT**. From the bottom of that box, one arrow descends to a small terminal box labelled `cluster`. Beneath the whole composition, centred in italic body type, three short lines: *"The mechanisms could not be more different. / The destination is the same one. / The destination is the point."* Symmetry is the argument: the left and right paths must be mirror images in weight, spacing and box size, so that the eye reads them as equals and the only asymmetry in the figure is the single shared destination.

**Visual style:**
- Palette: brand navy on off-white; the two paths rendered identically, differentiated only by their headers; inherit book default
- Size (pixels): 1000 x 900 near-square
- Font: inherit book default (Roboto Slab for RENDER / PATCH and for the central box's three lines, Fira Mono for `templates/ + values`, `base/ + overlay/` and `cluster`, Fira Sans italic for the closing three lines)
- Accent color for highlighted elements: Brass (#B58B3E) for the central ONE NAMED, VERSIONED, INSTALLABLE UNIT box — border and type. This is the chapter's Zenith figure; the Brass belongs to the convergence point and to nothing else in the frame.

**Critical details (non-negotiable accuracy):**
- The two paths must be **visually symmetric and equally weighted**. Any styling that makes one look preferred contradicts the section's entire claim.
- Neither column may be labelled "Helm" or "Kustomize." The source deliberately labels them by *mechanism* — RENDER and PATCH — because the Zenith is that the tool names are the less interesting layer. Do not add product names or logos.
- The two arrows into the central box point **inward from opposite sides**, meeting there. Converging arrows are the whole visual grammar; parallel arrows or a Y-merge above the box weaken it.
- There is exactly one destination box and exactly one `cluster` below it. Do not draw two clusters or two units.
- The closing three lines are part of the figure and must be typeset within it, not dropped as a caption. They are the Zenith stated plainly.
- `templates/ + values` pairs with "fill in holes"; `base/ + overlay/` pairs with "merge deltas". Do not cross them.
- No revision chain, no repository, no registry, no `values.yaml` file icon. This figure is deliberately the sparsest in the chapter; added detail dilutes it.

**Source ASCII (for designer reference):**
```
        RENDER                                          PATCH
        ══════                                          ═════

   templates/ + values                          base/ + overlay/
          │                                            │
     ┌────┴────┐                                  ┌────┴────┐
     │ fill in │                                  │  merge  │
     │  holes  │                                  │  deltas │
     └────┬────┘                                  └────┬────┘
          │                                            │
          │        ┌──────────────────────┐            │
          └───────►│                      │◄───────────┘
                   │   ONE NAMED,         │
                   │   VERSIONED,         │
                   │   INSTALLABLE UNIT   │
                   │                      │
                   └──────────┬───────────┘
                              │
                              ▼
                        ┌──────────┐
                        │ cluster  │
                        └──────────┘

        The mechanisms could not be more different.
        The destination is the same one.
        The destination is the point.
```

**Proposed filename:** `ch14-zenith-package-not-template.png`
*(If the author approves the anchor rename, this becomes `ch14-fig06-package-not-template.png`.)*

```yaml-figure-spec
anchor_id: ch14-zenith-package-not-template
diagram_type: flowchart
source_ascii: |2
          RENDER                                          PATCH
          ══════                                          ═════

     templates/ + values                          base/ + overlay/
            │                                            │
       ┌────┴────┐                                  ┌────┴────┐
       │ fill in │                                  │  merge  │
       │  holes  │                                  │  deltas │
       └────┬────┘                                  └────┬────┘
            │                                            │
            │        ┌──────────────────────┐            │
            └───────►│                      │◄───────────┘
                     │   ONE NAMED,         │
                     │   VERSIONED,         │
                     │   INSTALLABLE UNIT   │
                     │                      │
                     └──────────┬───────────┘
                                │
                                ▼
                          ┌──────────┐
                          │ cluster  │
                          └──────────┘

          The mechanisms could not be more different.
          The destination is the same one.
          The destination is the point.
vendor_terms: []
complexity_hint:
  node_count: 6
  edge_count: 6
  label_count: 10
pedagogy:
  part_18_criteria_met: [zenith, distinguishing_alternatives, spatial_structure]
  learning_outcome: "Recognize that templating versus patching is an argument about mechanism between two tools that already agree on the goal: one named, versioned, installable unit"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The central box reading ONE NAMED, VERSIONED, INSTALLABLE UNIT, where both paths converge"
accessibility:
  alt_text_seed: "Two symmetric paths, one labelled render that fills in holes from templates and values, one labelled patch that merges deltas from a base and overlay, converging with opposing arrows on a single highlighted box reading one named, versioned, installable unit, which then flows to a cluster"
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1000
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Abstract mechanism comparison; no product names, marks or logos appear in the figure."
```
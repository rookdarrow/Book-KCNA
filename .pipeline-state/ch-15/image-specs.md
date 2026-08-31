# Image Specifications — KCNA Chapter 15

*Generated from `draft-v1.md` (draft-voice.md does not exist at this stage; all line numbers cite `../Book-KCNA/.pipeline-state/ch-15/draft-v1.md`). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Anchors found:** 7 (lines 175, 287, 412, 473, 610, 812, 968).
**Fenced blocks found:** 7 (lines 176–189, 288–313, 413–434, 474–494, 611–639, 813–837, 969–997).
**Anchor-to-block correspondence:** 1:1. Every fence opens on the line immediately after its anchor.

---

## UNANCHORED DIAGRAMS

None. All seven fenced blocks in the draft carry a preceding `<!-- FIGURE: ... -->` anchor.

---

## FIGURE-CONTRACT FLAGS

Anchor IDs are the join key and are **not** renamed in this document. Each item below is an author-review decision.

**F-1 — Anchor ID does not match the required pattern.**
`ch15-zenith-control-loop-pointed-at-a-repo` (line 968) substitutes `zenith` for `fig{MM}`. Rule 4 requires `ch{NN}-fig{MM}-{kebab-slug}`; the other six anchors in the chapter conform. The conforming form would be `ch15-fig07-zenith-control-loop-pointed-at-a-repo`. Until this is resolved the book-level aggregator will either drop the figure or index it under a non-conforming key. The spec below uses the ID as written.

**F-2 — Anchor ordinals and printed caption numbers are transposed.**
`ch15-fig05-opengitops-four-principles` (line 473) is captioned **Figure 15.4**; `ch15-fig04-argocd-sync-states-and-hooks` (line 610) is captioned **Figure 15.5**. The anchors also appear in the draft in the order 05-then-04. Independently caught by the fact-accuracy diagnostic (item 13). The anchor is the join key, so swapping the two printed caption numbers is the cheaper fix; renumbering the anchors is the other. Author's call.

**F-3 — A slug promises content its figure does not contain.**
`ch15-fig04-argocd-sync-states-and-hooks` depicts sync states only. Hooks are in `ch15-fig06-sync-waves-and-hook-phases`. The spec below is written to the drawn content, not to the slug. **Do not add hook nodes to satisfy the slug.**

**F-4 — The Zenith figure's pairing claim does not hold against the shipped Chapter 3. Do not render unresolved.**
Two separate problems, one cosmetic and one load-bearing.

(a) Figure 15.7's caption instructs the reader to "Lay this beside Figure 3.2." Chapter 3 as shipped (`chapter-03-the-ship-s-company.md`) carries no numbered figure captions at all — only chapters 6 and 8 use that convention. **"Figure 3.2" has no referent in the book.** The figure meant is anchor `ch03-fig02-control-loop-desired-vs-current` (`chapter-03-the-ship-s-company.md:762`).

(b) The two drawings are not the same drawing. Chapter 3's loop is `DESIRED STATE → COMPARE → ACT TO CLOSE THE GAP → CURRENT STATE`: four boxes, no controller node, no API server. Chapter 15's is `DESIRED STATE → CONTROLLER → API SERVER → CURRENT STATE`. Figure 15.7's caption asserts that "the controller sits in the same place, the API server is still the only door in, and the arrows run in the same directions. One box changed contents." Against the shipped Chapter 3 figure that is not true — `COMPARE` and `ACT TO CLOSE THE GAP` have no counterpart in Chapter 15's, and `CONTROLLER` and `API SERVER` have no counterpart in Chapter 3's. The chapter's entire Zenith payoff depends on the claim being literally checkable by a reader who flips back.

Three resolutions, in descending order of what they preserve: redraw `ch03-fig02` onto the Chapter 15 chassis and reflow the Chapter 3 prose around it (preserves the payoff; costs a Chapter 3 edit); redraw `ch15-fig07` onto Chapter 3's chassis (cheaper, but loses the API-server node that §3's Navigational Hazards block depends on); or soften Figure 15.7's caption to a family resemblance. **Whichever is chosen, the two figures must be commissioned and rendered as a pair, on one chassis, so they superimpose.**

**F-5 — Figure 15.2's key contradicts its own bars.**
The key at line 312 reads `█ = new version serving   ░ = old version serving / absent`. But in every cell, the row labelled `old` uses `█` for the interval in which the *old* version is serving. The intended semantics are per-row, not per-version. Render as "filled = this row's version is serving traffic; empty = it is not," and correct the draft's key line at the revision stage.

**F-6 — Emoji inside a figure.**
`ch15-fig03` uses 🔑 (U+1F511) at lines 418 and 429. Harmless in source — the fence is replaced by the rendered asset at build — but the *rendered* asset must use a drawn key, never the emoji. Astral-plane glyphs render as empty boxes on Kindle.

**F-7 — Figure budget, recorded not flagged.**
Seven mandatory figures ties chapter 13 for the highest in the book; the modal chapter carries six. Not a defect. Recorded so the illustration budget is visible when the book-level index is assembled.

---

## Figure: ch15-fig01-twelve-factor-in-kubernetes

**Anchor ID:** `ch15-fig01-twelve-factor-in-kubernetes`
**Draft location:** line 175 · printed caption **Figure 15.1**
**Purpose:** Converts a numbered list nobody can hold in memory into a division of labour the reader can reason with — which factors the platform satisfies for you, which it merely makes reachable, and which remain the application's own problem. It sets up §1's Fixed Point, which states that Kubernetes cannot implement the application side.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** three-column classification / responsibility sort (no edges)

**Content specification:**
Three side-by-side columns of equal width, no connecting arrows anywhere. Each column has a two-line header set in the display face: left, "THE PLATFORM GIVES YOU THIS"; centre, "THE PLATFORM MAKES THIS EASY"; right, "STILL YOUR APPLICATION'S PROBLEM". Beneath each header, the factors assigned to that column, each rendered as a Roman numeral in a fixed-width gutter followed by the factor name. Left column, in order: III Config, VI Processes, VIII Concurrency, IX Disposability, XI Logs. Centre column: IV Backing services, V Build/release/run, X Dev/prod parity. Right column: I Codebase, II Dependencies, VII Port binding, XII Admin processes. Below each column, separated by a hairline rule, a footer band set smaller and lighter giving the concrete instances: left, "ConfigMaps, Secrets, Deployments, SIGTERM, stdout collection"; centre, "Services, image tags, namespaces per env"; right, "Your repo, your Dockerfile, your code". The point of the diagram is that all twelve numerals appear exactly once across the three columns — the sort is exhaustive and disjoint, which is what makes it an argument rather than a summary. The right-hand column carries the accent, because it names what the platform will never do for you.

**Visual style:**
- Palette: book default (Lodestar navy line-art on white)
- Size (pixels): 1200×700 landscape
- Font: book default — Roboto Slab for column headers, Fira Sans for factor names, Fira Mono for the Roman-numeral gutter and the object names in the footer bands
- Accent color for highlighted elements: Brass `#B58B3E` on the right-hand column header and its rule
- Glyphs: none. Per [LOCKED 2026-08-25], only the stack and pipeline families carry Lucide glyphs; this is neither.

**Critical details (non-negotiable accuracy):**
- All twelve Roman numerals I–XII appear exactly once. Counts are 5 / 3 / 4. No factor in two columns, none omitted.
- Numeral-to-name pairings must be exact: III Config · VI Processes · VIII Concurrency · IX Disposability · XI Logs · IV Backing services · V Build/release/run · X Dev/prod parity · I Codebase · II Dependencies · VII Port binding · XII Admin processes.
- Column order left to right is platform-gives / platform-makes-easy / still-yours. Reversing it inverts the argument.
- **No arrows or edges.** This is a sort, not a flow. Any connector implies a sequence the material does not claim.
- "Dev/prod parity" belongs in the *centre* column, not the left. The caption's point — Kubernetes makes parity achievable, not automatic — depends on it.
- Each footer band belongs to its own column and must not read as a fourth row spanning all three.

**Source ASCII (for designer reference):**
```
   THE PLATFORM GIVES        THE PLATFORM MAKES       STILL YOUR APPLICATION'S
   YOU THIS                  THIS EASY                PROBLEM

   III  Config               IV   Backing services    I    Codebase
   VI   Processes            V    Build/release/run   II   Dependencies
   VIII Concurrency          X    Dev/prod parity     VII  Port binding
   IX   Disposability                                 XII  Admin processes
   XI   Logs

   ConfigMaps, Secrets,      Services, image tags,    Your repo, your
   Deployments, SIGTERM,     namespaces per env       Dockerfile, your
   stdout collection                                  code
```

**Proposed filename:** `ch15-fig01-twelve-factor-in-kubernetes.png`

```yaml-figure-spec
anchor_id: ch15-fig01-twelve-factor-in-kubernetes
diagram_type: concept_map
source_ascii: |2
     THE PLATFORM GIVES        THE PLATFORM MAKES       STILL YOUR APPLICATION'S
     YOU THIS                  THIS EASY                PROBLEM

     III  Config               IV   Backing services    I    Codebase
     VI   Processes            V    Build/release/run   II   Dependencies
     VIII Concurrency          X    Dev/prod parity     VII  Port binding
     IX   Disposability                                 XII  Admin processes
     XI   Logs

     ConfigMaps, Secrets,      Services, image tags,    Your repo, your
     Deployments, SIGTERM,     namespaces per env       Dockerfile, your
     stdout collection                                  code
vendor_terms: [configmap, secret, deployment, kubernetes-service]
complexity_hint:
  node_count: 15
  edge_count: 0
  label_count: 18
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Sort the twelve factors by who satisfies them, and name the ones Kubernetes cannot satisfy for you"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the third column header, STILL YOUR APPLICATION'S PROBLEM"
accessibility:
  alt_text_seed: "Three columns sorting the twelve factors by who satisfies each. The platform gives you config, processes, concurrency, disposability and logs. The platform makes backing services, build/release/run and dev-prod parity easy. Codebase, dependencies, port binding and admin processes remain the application's problem."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Factor names are the twelve-factor methodology's published terms; the three-column responsibility sort is this book's own."
```

---

## Figure: ch15-fig02-deployment-strategies-compared

**Anchor ID:** `ch15-fig02-deployment-strategies-compared`
**Draft location:** line 287 · printed caption **Figure 15.2**
**Purpose:** Draws the line §2's Fixed Point states — two of these four are values of a field on a Deployment, two are architectures something above the Deployment must implement — and shows what each one demands before you can use it at all.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** four-panel comparison matrix in two labelled enclosures, each cell carrying a proportional old/new traffic timeline

**Content specification:**
Two stacked enclosures, one above the other, each a bordered container with its title set into the top border. Upper title: "FIELDS ON A DEPLOYMENT". Lower title: "PATTERNS NEEDING TOOLING ABOVE IT". Each enclosure holds two cells side by side — upper-left Recreate, upper-right RollingUpdate, lower-left Blue/Green, lower-right Canary. Every cell contains, top to bottom: the strategy name; two horizontal bars stacked and labelled at their left edge; two short prose lines; a "needs:" line.

The bars run left to right as time, and every bar is the same length. Recreate: the `old` bar is filled for roughly the first 40% then empty; the `new` bar is empty for roughly the first 60% then filled; between them, an interval where neither is filled, marked by a bracket labelled "gap". RollingUpdate: `old` ramps from filled to empty across the full width while `new` ramps from empty to filled, using a mid-tone for the transition, so that at every vertical slice the two together sum to a full bar. Blue/Green: `blue` filled for the first ~80% then empty, `green` empty then filled, with a single vertical rule crossing both bars at the changeover, labelled "switch". Canary: `old` steps down and `new` steps up in four discrete stages, labelled beneath as "5% → 25% → 50% → 100%".

Prose lines, one per cell: Recreate "downtime; never two versions" / "needs: nothing". RollingUpdate "no downtime; both versions live at once" / "needs: nothing". Blue/Green "test before any user arrives" / "needs: 2x capacity". Canary "small slice meets it first; metrics decide" / "needs: traffic splitting + metric analysis". A key sits beneath the whole figure. The point of the diagram is the two enclosures: a reader who cannot see at a glance which pair is a field value and which pair is an architecture has got the opposite of what the figure is for.

**Visual style:**
- Palette: book default (Lodestar navy line-art on white); a light tint ground on the lower enclosure to separate the two groups
- Size (pixels): 1200×1250 portrait
- Font: book default — Fira Mono for `Recreate`, `RollingUpdate` and the percentage steps; Fira Sans for prose lines
- Accent color for highlighted elements: Brass `#B58B3E` on the lower enclosure's title band
- Glyphs: none

**Critical details (non-negotiable accuracy):**
- Recreate's two bars must **not** overlap, and a visible interval where neither is filled must be present and marked. That gap is the strategy's defining cost and its defining guarantee.
- RollingUpdate's two bars must overlap throughout. At no vertical slice is total capacity zero, and at no slice is only one version present.
- Blue/Green's cutover is a **single vertical line**, not a ramp. Both environments exist simultaneously; only one is taking traffic.
- Canary's transitions are **discrete steps**, ascending, carrying the four labelled percentages. Drawing canary as a smooth ramp collapses it into RollingUpdate.
- The two enclosures must be unmistakably distinct groupings. This is the figure's entire point and §2's Fixed Point.
- The lower enclosure's title must not be shortened; "needing tooling above it" is the claim.
- "needs: nothing" appears on **both** upper cells. The asymmetry against "2x capacity" and "traffic splitting + metric analysis" is the practical decision criterion the ⚓ Worth Securing callout turns on.
- **The source key is wrong — see FLAG F-5.** Render the key as "filled = this row's version is serving traffic; empty = it is not." Do not reproduce the draft's key line as written.
- Fills must be distinguishable in greyscale by pattern or weight, not tone alone.

**Source ASCII (for designer reference):**
```
  ┌─ FIELDS ON A DEPLOYMENT ──────────────────────────────────────┐
  │                                                               │
  │  Recreate            RollingUpdate                            │
  │  old ████░░░░░░      old ████▓▓▒▒░░░░                          │
  │  new ░░░░░░████      new ░░░░▒▒▓▓████                          │
  │      └gap┘                                                    │
  │  downtime; never     no downtime; both                        │
  │  two versions        versions live at once                    │
  │  needs: nothing      needs: nothing                           │
  └───────────────────────────────────────────────────────────────┘

  ┌─ PATTERNS NEEDING TOOLING ABOVE IT ───────────────────────────┐
  │                                                               │
  │  Blue/Green          Canary                                   │
  │  blue  ████████│░░   old ████████▓▓▓▓░░░░                      │
  │  green ░░░░░░░░│██   new ░░░░▒▒▒▒▓▓▓▓████                      │
  │            switch          5% → 25% → 50% → 100%              │
  │  test before any     small slice meets it                     │
  │  user arrives        first; metrics decide                    │
  │  needs: 2x capacity  needs: traffic splitting                 │
  │                             + metric analysis                 │
  └───────────────────────────────────────────────────────────────┘

  █ = new version serving   ░ = old version serving / absent
```

**Proposed filename:** `ch15-fig02-deployment-strategies-compared.png`

```yaml-figure-spec
anchor_id: ch15-fig02-deployment-strategies-compared
diagram_type: other
source_ascii: |2
    ┌─ FIELDS ON A DEPLOYMENT ──────────────────────────────────────┐
    │                                                               │
    │  Recreate            RollingUpdate                            │
    │  old ████░░░░░░      old ████▓▓▒▒░░░░                          │
    │  new ░░░░░░████      new ░░░░▒▒▓▓████                          │
    │      └gap┘                                                    │
    │  downtime; never     no downtime; both                        │
    │  two versions        versions live at once                    │
    │  needs: nothing      needs: nothing                           │
    └───────────────────────────────────────────────────────────────┘

    ┌─ PATTERNS NEEDING TOOLING ABOVE IT ───────────────────────────┐
    │                                                               │
    │  Blue/Green          Canary                                   │
    │  blue  ████████│░░   old ████████▓▓▓▓░░░░                      │
    │  green ░░░░░░░░│██   new ░░░░▒▒▒▒▓▓▓▓████                      │
    │            switch          5% → 25% → 50% → 100%              │
    │  test before any     small slice meets it                     │
    │  user arrives        first; metrics decide                    │
    │  needs: 2x capacity  needs: traffic splitting                 │
    │                             + metric analysis                 │
    └───────────────────────────────────────────────────────────────┘

    █ = new version serving   ░ = old version serving / absent
vendor_terms: [deployment]
complexity_hint:
  node_count: 6
  edge_count: 0
  label_count: 22
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, temporal_structure, fixed_point]
  learning_outcome: "Separate the two Deployment strategy field values from the two release patterns that require tooling above the Deployment, and state what each costs"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the lower enclosure's title band, PATTERNS NEEDING TOOLING ABOVE IT"
accessibility:
  alt_text_seed: "Four release strategies in two groups. The upper group, fields on a Deployment, holds Recreate with a gap where neither version serves, and RollingUpdate with both versions overlapping throughout. The lower group, patterns needing tooling above it, holds blue/green with a single switch line and two-times capacity, and canary stepping five to twenty-five to fifty to one hundred percent and needing traffic splitting plus metric analysis."
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic release-strategy shapes redrawn from prose definitions; no vendor diagram traced and no marks reproduced."
```

---

## Figure: ch15-fig03-cicd-push-vs-gitops-pull

**Anchor ID:** `ch15-fig03-cicd-push-vs-gitops-pull`
**Draft location:** line 412 · printed caption **Figure 15.3**
**Purpose:** Show that push and pull differ in exactly one thing — which side of the cluster boundary the credential sits on — so that the four consequences §3 then lists read as consequences rather than as a separate list of claims.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel trust-boundary topology comparison, mirrored

**Content specification:**
Two panels stacked, PUSH above and PULL below, drawn on an identical chassis so the pair reads as one drawing with one thing reversed. In both panels a dashed rectangle labelled "cluster boundary" occupies the right two-thirds of the frame at the same x-position and the same width, and a node labelled "API server" sits inside it at the same position in both.

PUSH: a solid box labelled "pipeline" sits outside the boundary on the left and carries a key glyph. One arrow runs from the pipeline, across the dashed boundary, to the API server, arrowhead at the API server. A short callout below the pipeline points up at it with the caption "the key lives OUT HERE".

PULL: a box labelled "repo" sits outside the boundary on the left and carries **no** key. A box labelled "agent" sits inside the boundary, and the key glyph is on the agent. Two arrows leave the agent: one runs left, across the boundary, to the repo, with the arrowhead **at the repo**; one runs right to the API server. A callout from below the boundary points up at the agent with the caption "the key lives IN HERE".

The point of the diagram is the mirror. The boundary does not move, the API server does not move, the arrow reverses, and the key changes sides. Everything in §3 — where credentials sit, what a compromise reaches, what happens between deploys, what "the truth" means — is a reading of that one difference.

**Visual style:**
- Palette: book default (Lodestar navy line-art on white); the cluster boundary as a dashed navy rule at reduced weight
- Size (pixels): 1200×900 landscape
- Font: book default — Fira Mono for the node labels `pipeline`, `repo`, `agent`, `API server`; Fira Sans for the two "the key lives …" captions, set in small caps or letterspaced caps for OUT HERE / IN HERE
- Accent color for highlighted elements: Brass `#B58B3E` on the two key glyphs, which should be the only Brass in the figure
- Glyphs: the key is a drawn line-art key, not a Lucide semantic glyph and not an emoji. No other glyphs.

**Critical details (non-negotiable accuracy):**
- The cluster boundary must sit at the **identical** position and width in both panels, as must the API server. If the two panels do not superimpose, the figure has no argument left.
- PUSH: the key is **outside** the boundary. PULL: the key is **inside**. Reversing this inverts §3 entirely and contradicts every Bearings and Practice Question that depends on it.
- In PULL the repo carries **no key**. The agent holds credentials to the repository; the repository holds nothing.
- In PULL the arrow between agent and repo points **at the repo** — the agent reaches outward and fetches. An arrow pointing from repo to agent draws a push, which is the opposite of principle 3.
- In both panels every arrow that crosses into the cluster terminates at the API server. Nothing crosses the boundary to anything else.
- Exactly one key per panel.
- Render the key as line art. **Never the 🔑 emoji** — see FLAG F-6.
- Must remain legible in greyscale: the key's position, not its colour, carries the meaning.

**Source ASCII (for designer reference):**
```
  PUSH
                    ┌ ─ ─ ─ cluster boundary ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
   ┌──────────┐     │                                          │
   │ pipeline │──── │ ────────────────►  API server            │
   │   🔑     │     │                                          │
   └──────────┘     │                                          │
    ▲               └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘
    │
   the key lives OUT HERE


  PULL
                    ┌ ─ ─ ─ cluster boundary ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
   ┌──────────┐     │  ┌─────────┐                             │
   │   repo   │◄─── │ ─│  agent  │────────►  API server        │
   │          │     │  │   🔑    │                             │
   └──────────┘     │  └─────────┘                             │
                    │       ▲                                  │
                    └ ─ ─ ─ │ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
                    the key lives IN HERE
```

**Proposed filename:** `ch15-fig03-cicd-push-vs-gitops-pull.png`

```yaml-figure-spec
anchor_id: ch15-fig03-cicd-push-vs-gitops-pull
diagram_type: security_topology
source_ascii: |2
    PUSH
                      ┌ ─ ─ ─ cluster boundary ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
     ┌──────────┐     │                                          │
     │ pipeline │──── │ ────────────────►  API server            │
     │   🔑     │     │                                          │
     └──────────┘     │                                          │
      ▲               └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘
      │
     the key lives OUT HERE


    PULL
                      ┌ ─ ─ ─ cluster boundary ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
     ┌──────────┐     │  ┌─────────┐                             │
     │   repo   │◄─── │ ─│  agent  │────────►  API server        │
     │          │     │  │   🔑    │                             │
     └──────────┘     │  └─────────┘                             │
                      │       ▲                                  │
                      └ ─ ─ ─ │ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
                      the key lives IN HERE
vendor_terms: [kube-apiserver]
complexity_hint:
  node_count: 7
  edge_count: 3
  label_count: 9
pedagogy:
  part_18_criteria_met: [spatial_structure, distinguishing_alternatives]
  learning_outcome: "Locate cluster-write credentials relative to the cluster boundary under push and under pull, and derive the blast-radius difference from that one placement"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the key glyph in each panel, and which side of the cluster boundary it sits on"
accessibility:
  alt_text_seed: "Two mirrored panels sharing one cluster boundary. In push, a pipeline outside the boundary holds the key and reaches inward to the API server. In pull, a repository outside the boundary holds no key while an agent inside the boundary holds the key, reaching outward to fetch from the repository and inward to the API server."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic trust-boundary topology; API server named as a component only, with no CNCF marks, logos or vendor icons reproduced."
```

---

## Figure: ch15-fig05-opengitops-four-principles

**Anchor ID:** `ch15-fig05-opengitops-four-principles`
**Draft location:** line 473 · printed caption **Figure 15.4** — see FLAG F-2
**Purpose:** Show that only one of the four OpenGitOps principles is new material, and pre-load §7's Zenith by tagging the other three with the chapter that already taught them.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** 2×2 principle grid with back-reference tags

**Content specification:**
Four boxes of equal size in a 2×2 grid, read left to right then top to bottom, numbered 1 through 4. Each box carries a numbered heading in caps, a one-line gloss set in body type beneath it, and a tag in the lower-left prefixed by a left-pointing triangle.

Box 1: "1 DECLARATIVE" / "desired state expressed declaratively" / tag "◄ you know this: Ch 4 §1".
Box 2: "2 VERSIONED & IMMUTABLE" / "stored so as to enforce immutability, versioning, complete history" / tag "◄ NEW HERE".
Box 3: "3 PULLED AUTOMATICALLY" / "agents automatically pull desired state from source" / tag "◄ you know this: Ch 3 §5".
Box 4: "4 CONTINUOUSLY RECONCILED" / "agents continuously observe actual state and apply desired state" / tag "◄ you know this: Ch 3 §6".

The point of the diagram lives entirely in the asymmetry among the four tags: three say "you know this", one says "NEW HERE". Set the three "you know this" tags in a lighter weight and the "NEW HERE" tag in Brass, so a reader scanning the figure sees the odd one out before reading a word of it.

**Visual style:**
- Palette: book default (Lodestar navy line-art on white)
- Size (pixels): 1200×900 landscape
- Font: book default — Roboto Slab for the numbered headings, Fira Sans for glosses and tags
- Accent color for highlighted elements: Brass `#B58B3E` on box 2's "NEW HERE" tag only
- Glyphs: none

**Critical details (non-negotiable accuracy):**
- Principle order 1, 2, 3, 4 must be preserved and must read left to right, top to bottom. This is the published order and the Exam Alert asks for it in order.
- **Only box 2 is tagged NEW HERE.** A second such tag contradicts §7's claim that three of the four were already the reader's.
- Chapter pointers are exact — Ch 4 §1, Ch 3 §5, Ch 3 §6 — and must be verified against the section skeleton before render.
- The words "pulled" in heading 3 and "continuously" in heading 4 carry the definition. Headings must not be abbreviated or reflowed in a way that drops them.
- "VERSIONED & IMMUTABLE" keeps both terms.
- **No arrows between boxes.** The four are a set, not a sequence, despite being numbered.
- The source ASCII's box 4 has a one-column right-border misalignment at line 488. That is an artifact of the ASCII, not content. Do not reproduce it.

**Source ASCII (for designer reference):**
```
  ┌────────────────────────────┐  ┌────────────────────────────┐
  │ 1  DECLARATIVE             │  │ 2  VERSIONED & IMMUTABLE   │
  │                            │  │                            │
  │ desired state expressed    │  │ stored so as to enforce    │
  │ declaratively              │  │ immutability, versioning,  │
  │                            │  │ complete history           │
  │      ◄ you know this:      │  │      ◄ NEW HERE            │
  │        Ch 4 §1             │  │                            │
  └────────────────────────────┘  └────────────────────────────┘

  ┌────────────────────────────┐  ┌────────────────────────────┐
  │ 3  PULLED AUTOMATICALLY    │  │ 4  CONTINUOUSLY RECONCILED │
  │                            │  │                            │
  │ agents automatically pull  │  │ agents continuously observe │
  │ desired state from source  │  │ actual state and apply     │
  │                            │  │ desired state              │
  │      ◄ you know this:      │  │      ◄ you know this:      │
  │        Ch 3 §5             │  │        Ch 3 §6             │
  └────────────────────────────┘  └────────────────────────────┘
```

**Proposed filename:** `ch15-fig05-opengitops-four-principles.png`

```yaml-figure-spec
anchor_id: ch15-fig05-opengitops-four-principles
diagram_type: concept_map
source_ascii: |2
    ┌────────────────────────────┐  ┌────────────────────────────┐
    │ 1  DECLARATIVE             │  │ 2  VERSIONED & IMMUTABLE   │
    │                            │  │                            │
    │ desired state expressed    │  │ stored so as to enforce    │
    │ declaratively              │  │ immutability, versioning,  │
    │                            │  │ complete history           │
    │      ◄ you know this:      │  │      ◄ NEW HERE            │
    │        Ch 4 §1             │  │                            │
    └────────────────────────────┘  └────────────────────────────┘

    ┌────────────────────────────┐  ┌────────────────────────────┐
    │ 3  PULLED AUTOMATICALLY    │  │ 4  CONTINUOUSLY RECONCILED │
    │                            │  │                            │
    │ agents automatically pull  │  │ agents continuously observe │
    │ desired state from source  │  │ actual state and apply     │
    │                            │  │ desired state              │
    │      ◄ you know this:      │  │      ◄ you know this:      │
    │        Ch 3 §5             │  │        Ch 3 §6             │
    └────────────────────────────┘  └────────────────────────────┘
vendor_terms: []
complexity_hint:
  node_count: 4
  edge_count: 0
  label_count: 12
pedagogy:
  part_18_criteria_met: [spatial_structure, zenith]
  learning_outcome: "State the four OpenGitOps principles in order and identify which one is not already implied by Kubernetes architecture"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "box 2's NEW HERE tag"
accessibility:
  alt_text_seed: "Four boxes in a two-by-two grid, one per OpenGitOps principle. Declarative is tagged you know this, chapter 4 section 1. Versioned and immutable is tagged NEW HERE. Pulled automatically is tagged chapter 3 section 5. Continuously reconciled is tagged chapter 3 section 6. Only the second principle is new."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Principle names and one-line glosses paraphrased from OpenGitOps v1.0.0 per snapshot opengitops-principles-v1-2026-08-31; no logos and no verbatim long-form text reproduced."
```

---

## Figure: ch15-fig04-argocd-sync-states-and-hooks

**Anchor ID:** `ch15-fig04-argocd-sync-states-and-hooks`
**Draft location:** line 610 · printed caption **Figure 15.5** — see FLAGS F-2 and F-3
**Purpose:** Show that `Synced` and `OutOfSync` are the two possible answers to one comparison that never stops running, and that the ordinary cause of `OutOfSync` is a person, not a failure — which is §4's Fixed Point and the trap the Exam Alert names.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-scenario three-column data-flow comparison, plus a separate operation node

**Content specification:**
Three column headings across the top, each on two lines: left "TARGET STATE (Git repository)", centre "AGENT (controller)", right "LIVE STATE (cluster)". Two scenario rows beneath them, drawn identically except where noted.

Row 1, the agreeing case: a left box reading "deployment.yml / replicas: 3", a right box reading "Deployment / replicas: 3", and a centre box labelled "compare". Both outer boxes have arrows pointing **inward** to the compare box. A short stem drops from the compare box to the word "Synced", with "the two agree" beneath it.

Row 2, the disagreeing case: the same left box, "deployment.yml / replicas: 3"; the right box now reads "Deployment / replicas: 5"; the same inward arrows to a compare box. The stem drops to "OutOfSync", with "the two do not agree" beneath. A separate annotation arrow enters the right-hand box from below, captioned "someone ran kubectl scale on Friday".

Below row 2, a further arrow drops from the OutOfSync stem into a box labelled "SYNC (operation)", with a side note "apply target state → live matches again".

The point of the diagram is that the only thing that differs between the two rows is one number in the right-hand box, and that the number was changed from outside the system by a person. Set both `replicas:` values in mono, and give the mismatched value and the `OutOfSync` label the accent.

**Visual style:**
- Palette: book default (Lodestar navy line-art on white)
- Size (pixels): 1200×1400 portrait
- Font: book default — Fira Mono for `deployment.yml`, `Deployment`, `replicas:` values, `kubectl scale`, `Synced` and `OutOfSync`; Fira Sans for the explanatory lines
- Accent color for highlighted elements: Brass `#B58B3E` on the `replicas: 5` value and the `OutOfSync` label
- Glyphs: none

**Critical details (non-negotiable accuracy):**
- Both comparison arrows point **inward**, to the agent. The agent observes both operands. There is no arrow between the repository and the cluster; they never talk to each other.
- The left-hand box is **identical** in both rows (`replicas: 3`). Only the right-hand value differs, 3 versus 5. Changing the left value too would teach the wrong cause.
- **`OutOfSync` must not be styled as an error.** No red, no warning triangle, no exclamation, no alert colouring. It is a status field. Brass or plain navy at the same weight as `Synced`.
- The "SYNC (operation)" box is a separate node reached only from the OutOfSync branch. Sync is an operation, not a status; it must not sit in the status row alongside `Synced` and `OutOfSync`.
- The "someone ran kubectl scale on Friday" annotation points at the **cluster** box, not the repository. The edit happened to live state.
- Do **not** add hook nodes to match the slug — see FLAG F-3. Hooks belong to `ch15-fig06`.
- Both column headings keep their parenthetical: "(Git repository)" and "(cluster)". The whole substitution the chapter turns on is where the target state lives.

**Source ASCII (for designer reference):**
```
      TARGET STATE                 AGENT                LIVE STATE
      (Git repository)          (controller)             (cluster)

    ┌───────────────┐         ┌────────────┐         ┌───────────────┐
    │ deployment.yml│────────►│            │◄────────│ Deployment    │
    │  replicas: 3  │         │  compare   │         │  replicas: 3  │
    └───────────────┘         │            │         └───────────────┘
                              └─────┬──────┘
                                    │
                                 Synced
                            the two agree

    ┌───────────────┐         ┌────────────┐         ┌───────────────┐
    │ deployment.yml│────────►│            │◄────────│ Deployment    │
    │  replicas: 3  │         │  compare   │         │  replicas: 5  │
    └───────────────┘         │            │         └───────────────┘
                              └─────┬──────┘              ▲
                                    │                     │
                              OutOfSync            someone ran
                        the two do not agree     kubectl scale
                                    │              on Friday
                                    │
                                    ▼
                            ┌──────────────┐
                            │     SYNC     │  apply target state
                            │  (operation) │  → live matches again
                            └──────────────┘
```

**Proposed filename:** `ch15-fig04-argocd-sync-states-and-hooks.png`

```yaml-figure-spec
anchor_id: ch15-fig04-argocd-sync-states-and-hooks
diagram_type: data_flow
source_ascii: |2
        TARGET STATE                 AGENT                LIVE STATE
        (Git repository)          (controller)             (cluster)

      ┌───────────────┐         ┌────────────┐         ┌───────────────┐
      │ deployment.yml│────────►│            │◄────────│ Deployment    │
      │  replicas: 3  │         │  compare   │         │  replicas: 3  │
      └───────────────┘         │            │         └───────────────┘
                                └─────┬──────┘
                                      │
                                   Synced
                              the two agree

      ┌───────────────┐         ┌────────────┐         ┌───────────────┐
      │ deployment.yml│────────►│            │◄────────│ Deployment    │
      │  replicas: 3  │         │  compare   │         │  replicas: 5  │
      └───────────────┘         │            │         └───────────────┘
                                └─────┬──────┘              ▲
                                      │                     │
                                OutOfSync            someone ran
                          the two do not agree     kubectl scale
                                      │              on Friday
                                      │
                                      ▼
                              ┌──────────────┐
                              │     SYNC     │  apply target state
                              │  (operation) │  → live matches again
                              └──────────────┘
vendor_terms: [argo-cd, kubectl, deployment]
complexity_hint:
  node_count: 9
  edge_count: 8
  label_count: 14
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, fixed_point]
  learning_outcome: "Read OutOfSync as a drift signal rather than a failure, and name a cause of it in which nothing went wrong"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the mismatched replicas: 5 value and the OutOfSync label"
accessibility:
  alt_text_seed: "Two scenarios comparing target state in a Git repository against live state in a cluster, with an agent between them observing both. In the first, both say replicas three and the status is Synced. In the second, the repository still says three but the cluster says five because someone ran kubectl scale, and the status is OutOfSync; a separate sync operation applies the target state and the two match again."
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Argo CD's comparison model redrawn from the cached documentation prose; no Argo CD screenshot, logo or upstream diagram reproduced."
```

---

## Figure: ch15-fig06-sync-waves-and-hook-phases

**Anchor ID:** `ch15-fig06-sync-waves-and-hook-phases`
**Draft location:** line 812 · printed caption **Figure 15.6**
**Purpose:** Show the two nested orderings a sync obeys — phases along one axis, waves along the other — using the namespace-then-CRD-then-custom-resource case §5 opens with, so the reader can see that ordering is a real problem GitOps has and a bare `kubectl apply` merely ignores.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** staged pipeline (horizontal) with a nested ordered sequence (vertical) inside the middle stage

**Content specification:**
A horizontal axis arrow across the top of the frame, labelled "PHASE", running left to right. Beneath it, three containers side by side: "PreSync" (narrow), "Sync" (roughly three times as wide), "PostSync" (narrow). PreSync holds one item, "db migration". PostSync holds one item, "smoke test".

The Sync container carries its own vertical axis down its left inside edge, labelled "WAVE" with a downward arrow. Three rows sit against that axis, each a small labelled box: "wave -1" → box "Namespace"; "wave 0" → box "CRD"; "wave 1" → box "custom resource".

Beneath each of the three containers, a footer note set smaller and lighter: under PreSync, "must finish before anything is applied"; under Sync, "within the phase, lower wave numbers land first (default 0; negatives run before that)"; under PostSync, "runs only if everything succeeded and is Healthy". A single line runs beneath the whole figure: "ordering precedence: phase → wave → kind → name".

The point of the diagram is that the two axes are perpendicular and nested. The horizontal ordering is coarse and gated on success; the vertical ordering is fine and applies only inside a phase.

**Visual style:**
- Palette: book default (Lodestar navy line-art on white); a light tint ground inside the Sync container to make the nesting legible
- Size (pixels): 1200×850 landscape
- Font: book default — Fira Mono for `PreSync`, `Sync`, `PostSync`, `Namespace`, `CRD`, and the wave numbers; Fira Sans for footer notes
- Accent color for highlighted elements: Brass `#B58B3E` on the WAVE axis and its three ordered rows
- Glyphs: this is the chapter's one pipeline-family figure, so semantic Lucide glyphs are permitted here and only here, per [LOCKED 2026-08-25]. Confirm against `certcomp-diagrams/assets/glyph-ledger.yaml` before assigning any; if the ledger holds no entry for phase or wave semantics, render glyph-free rather than inventing one.

**Critical details (non-negotiable accuracy):**
- Phases run left to right in exactly this order: PreSync, Sync, PostSync.
- The fourth phase, SyncFail, is deliberately **absent** from this figure. Do not add it; the draft does not teach it here.
- Wave order runs top to bottom, lowest first: −1 Namespace, 0 CRD, 1 custom resource. Namespace before CRD before custom resource. Inverting this depicts exactly the failure the section exists to explain.
- The WAVE axis lives **inside** the Sync container. Waves order resources within a phase; an axis spanning all three containers is wrong and contradicts the precedence line.
- "default 0" and "negatives run before that" must survive into the render. Both are answered directly in Taking Your Bearings 3 and in Q19.
- The precedence line carries four terms in order: phase → wave → kind → name.
- PostSync's footer must keep "and is Healthy". The health gate — not mere completion — is the distinguishing fact and the answer to Q20.
- The Sync container must be visibly wider than the other two, so the nesting reads as containment rather than as a fourth peer stage.

**Source ASCII (for designer reference):**
```
   PHASE ──────────────────────────────────────────────────────────►

   ┌───────────┐   ┌───────────────────────────────┐   ┌───────────┐
   │  PreSync  │   │            Sync               │   │ PostSync  │
   │           │   │                               │   │           │
   │  db       │   │  W  wave -1 ┌───────────┐     │   │  smoke    │
   │  migration│   │  A          │ Namespace │     │   │  test     │
   │           │   │  V          └───────────┘     │   │           │
   │           │   │  E   wave 0 ┌───────────┐     │   │           │
   │           │   │             │    CRD    │     │   │           │
   │           │   │  │          └───────────┘     │   │           │
   │           │   │  ▼   wave 1 ┌───────────┐     │   │           │
   │           │   │             │  custom   │     │   │           │
   │           │   │             │ resource  │     │   │           │
   │           │   │             └───────────┘     │   │           │
   └───────────┘   └───────────────────────────────┘   └───────────┘

   must finish     within the phase, lower wave        runs only if
   before          numbers land first (default 0;      everything
   anything        negatives run before that)          succeeded and
   is applied                                          is Healthy

   ordering precedence:  phase → wave → kind → name
```

**Proposed filename:** `ch15-fig06-sync-waves-and-hook-phases.png`

```yaml-figure-spec
anchor_id: ch15-fig06-sync-waves-and-hook-phases
diagram_type: flowchart
source_ascii: |2
     PHASE ──────────────────────────────────────────────────────────►

     ┌───────────┐   ┌───────────────────────────────┐   ┌───────────┐
     │  PreSync  │   │            Sync               │   │ PostSync  │
     │           │   │                               │   │           │
     │  db       │   │  W  wave -1 ┌───────────┐     │   │  smoke    │
     │  migration│   │  A          │ Namespace │     │   │  test     │
     │           │   │  V          └───────────┘     │   │           │
     │           │   │  E   wave 0 ┌───────────┐     │   │           │
     │           │   │             │    CRD    │     │   │           │
     │           │   │  │          └───────────┘     │   │           │
     │           │   │  ▼   wave 1 ┌───────────┐     │   │           │
     │           │   │             │  custom   │     │   │           │
     │           │   │             │ resource  │     │   │           │
     │           │   │             └───────────┘     │   │           │
     └───────────┘   └───────────────────────────────┘   └───────────┘

     must finish     within the phase, lower wave        runs only if
     before          numbers land first (default 0;      everything
     anything        negatives run before that)          succeeded and
     is applied                                          is Healthy

     ordering precedence:  phase → wave → kind → name
vendor_terms: [argo-cd, custom-resource-definition, namespace]
complexity_hint:
  node_count: 9
  edge_count: 4
  label_count: 14
pedagogy:
  part_18_criteria_met: [temporal_structure, spatial_structure]
  learning_outcome: "Order a sync correctly: phases gate on success left to right, and waves order resources within a phase, lowest number first"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the WAVE axis and its three ordered rows inside the Sync container"
accessibility:
  alt_text_seed: "Three sync phases run left to right: PreSync holding a database migration, Sync, then PostSync holding a smoke test. Inside the Sync phase a vertical wave axis orders three resources lowest first: wave minus one Namespace, wave zero CustomResourceDefinition, wave one custom resource. Ordering precedence is phase, then wave, then kind, then name."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: false
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Phase and wave ordering redrawn from the cached Argo CD documentation prose; no upstream diagram traced and no marks reproduced."
```

---

## Figure: ch15-zenith-control-loop-pointed-at-a-repo

**Anchor ID:** `ch15-zenith-control-loop-pointed-at-a-repo` — **non-conforming, see FLAG F-1**
**Draft location:** line 968 · printed caption **Figure 15.7**
**Purpose:** The chapter's Zenith. Show that the GitOps control loop is Chapter 3's control loop with exactly one box's contents replaced — which is the whole technical delta between "Kubernetes" and "GitOps," and the recognition the chapter was built to produce.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** closed-cycle control loop, no entry point and no terminus

**Content specification:**
A four-node cycle. At the top, a container labelled "DESIRED STATE" holding an inner double-ruled box reading "Git repository". A callout to the right of that inner box reads "◄── the ONLY substitution (was: etcd)".

From DESIRED STATE, an arrow runs down into "CONTROLLER" at the centre, labelled "observe". From CONTROLLER, an arrow runs right and down into "API SERVER", labelled "act to close the gap"; the API SERVER node carries the sub-line "(still the only door in)". From API SERVER an arrow runs left into "CURRENT STATE", which carries the sub-line "what is actually true". From CURRENT STATE an arrow runs up and right, back into CONTROLLER, labelled "observe". Beneath the whole figure, one line: "and then it does it again. forever."

The point of the diagram is what is *not* annotated. Only one element carries a callout, and it is the Git repository. Everything else is Chapter 3's drawing, unchanged, and the figure has to look unchanged for the Zenith to land.

**Visual style:**
- Palette: book default (Lodestar navy line-art on white)
- Size (pixels): 1000×1300 portrait — or, if `ch03-fig02-control-loop-desired-vs-current` has already been rendered, match its dimensions and node positions exactly
- Font: book default — Roboto Slab for the node labels in caps, Fira Sans for arrow labels and sub-lines, Fira Mono for "Git repository" and "etcd"
- Accent color for highlighted elements: Brass `#B58B3E` on the double-ruled Git repository box and its callout, and nowhere else in the figure
- Glyphs: none

**Critical details (non-negotiable accuracy):**
- **Pairing constraint, blocking.** See FLAG F-4. This figure and `ch03-fig02-control-loop-desired-vs-current` must be commissioned and rendered as a pair, on one chassis — same node positions, same arrow directions, same proportions — so that a reader who flips back can superimpose them. As currently authored the two ASCII diagrams have different node sets, and the caption's claim that "one box changed contents" is not checkable. Do not render this figure until the author has resolved which drawing moves.
- **No entry arrow, no terminus, no start or stop node.** Chapter 3's figure carries the line "no start. no end. no exit condition." and the same must be true here.
- Exactly four boxes. Do not add etcd as a fifth node; it appears only inside the callout text, as the thing that was replaced.
- "(was: etcd)" must survive into the render. It *is* the substitution, stated.
- API SERVER stays on the loop, between the controller's action and current state. Drawing the controller writing to CURRENT STATE directly contradicts the ⚠ Navigational Hazards block in §3 and the trap table in the Exam Alert.
- The API SERVER sub-line "(still the only door in)" is retained. It is a direct callback to Ch 3 §5.
- Arrow labels are fixed: "observe" appears twice (desired-state→controller and current-state→controller), "act to close the gap" once (controller→API server). Do not relabel or consolidate.
- Exactly one Brass element. A second accent destroys the "only substitution" claim.
- The closing line "and then it does it again. forever." is part of the figure, not a caption. Keep it inside the asset.

**Source ASCII (for designer reference):**
```
                        ┌─────────────────┐
                        │  DESIRED STATE  │
                        │                 │
                        │  ╔═══════════╗  │   ◄── the ONLY substitution
                        │  ║    Git    ║  │       (was: etcd)
                        │  ║ repository║  │
                        │  ╚═══════════╝  │
                        └────────┬────────┘
                                 │
                                 │  observe
                                 ▼
                        ┌─────────────────┐
                        │                 │
             ┌─────────►│   CONTROLLER    │──────────┐
             │          │                 │          │
             │          └─────────────────┘          │  act to
             │                                       │  close the gap
             │  observe                              │
             │                                       ▼
    ┌────────┴────────┐                     ┌─────────────────┐
    │ CURRENT STATE   │◄────────────────────│   API SERVER    │
    │                 │                     │  (still the     │
    │  what is        │                     │   only door in) │
    │  actually true  │                     └─────────────────┘
    └─────────────────┘

              and then it does it again. forever.
```

**Proposed filename:** `ch15-zenith-control-loop-pointed-at-a-repo.png` *(becomes `ch15-fig07-zenith-control-loop-pointed-at-a-repo.png` if FLAG F-1 is resolved by renaming)*

```yaml-figure-spec
anchor_id: ch15-zenith-control-loop-pointed-at-a-repo
diagram_type: flowchart
source_ascii: |2
                          ┌─────────────────┐
                          │  DESIRED STATE  │
                          │                 │
                          │  ╔═══════════╗  │   ◄── the ONLY substitution
                          │  ║    Git    ║  │       (was: etcd)
                          │  ║ repository║  │
                          │  ╚═══════════╝  │
                          └────────┬────────┘
                                   │
                                   │  observe
                                   ▼
                          ┌─────────────────┐
                          │                 │
               ┌─────────►│   CONTROLLER    │──────────┐
               │          │                 │          │
               │          └─────────────────┘          │  act to
               │                                       │  close the gap
               │  observe                              │
               │                                       ▼
      ┌────────┴────────┐                     ┌─────────────────┐
      │ CURRENT STATE   │◄────────────────────│   API SERVER    │
      │                 │                     │  (still the     │
      │  what is        │                     │   only door in) │
      │  actually true  │                     └─────────────────┘
      └─────────────────┘

                and then it does it again. forever.
vendor_terms: [kube-apiserver, etcd, git]
complexity_hint:
  node_count: 4
  edge_count: 4
  label_count: 9
pedagogy:
  part_18_criteria_met: [zenith, spatial_structure, fixed_point]
  learning_outcome: "Recognise the GitOps agent as Chapter 3's control loop with the desired-state store relocated, and name everything that did not change"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "the double-ruled Git repository box inside DESIRED STATE"
accessibility:
  alt_text_seed: "A closed control loop with no beginning and no end. Desired state, now a Git repository rather than etcd and marked as the only substitution, is observed by a controller; the controller acts to close the gap through the API server, still the only door in; the API server changes current state, what is actually true, which the controller observes in turn. And then it does it again, forever."
rendering_hints:
  preferred_orientation: portrait
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: [cncf]
  clearance: own_interpretation
  notes: "Control-loop model redrawn from Kubernetes documentation prose and paired with this book's own Chapter 3 figure; no upstream diagram traced and no marks reproduced."
```
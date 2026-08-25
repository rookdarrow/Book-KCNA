# Image Specifications — KCNA Chapter 10

*Generated from the current draft (`draft-v1.md`; `draft-voice.md` does not exist at this stage). Every ASCII diagram in the draft must have an entry here; every entry must correspond to an anchor in the draft.*

**Extraction summary:** 4 figure anchors found, 4 ASCII diagrams found, all 4 diagrams anchored. No unanchored diagrams. One anchor deviates from the `ch{NN}-fig{MM}-{slug}` convention — flagged below and preserved verbatim as the join key.

---

## ANCHOR-FORMAT EXCEPTIONS

Flagged per rule 4. **IDs are not renamed here** — that is an author-review decision (rule 6). Both notes are for the author, not the designer.

1. **`ch10-zenith-nothing-without-a-controller`** does not match `ch{NN}-fig{MM}-{kebab-slug}`. It substitutes the segment `zenith` for `fig{MM}`. The figure sits inside the `☀️ Zenith` block in §8, so the deviation reads as deliberate semantic naming rather than a typo. If the book-level index sorts or validates on `fig{MM}`, this anchor will not sort with its siblings and may fail a strict-format check. Suggested normalisation if the author wants conformance: `ch10-fig05-nothing-without-a-controller`. **Do not change the draft and this document independently** — the anchor is the join key and must move in both places at once.

2. **No `ch10-fig01` exists.** Figure numbering in this chapter begins at `fig02` and runs `fig02`, `fig03`, `fig04`, then the zenith anchor. Either a first figure was cut during drafting and the numbers were never closed up, or the numbering was seeded from an outline that assumed one. Not an error in itself — the anchors are unique and internally consistent — but a book-level index will show a gap for Chapter 10.

---

## UNANCHORED DIAGRAMS

None. Every fenced block in the draft is either a YAML manifest (code, not a figure) or an ASCII diagram carrying a `<!-- FIGURE: ... -->` anchor on the line immediately preceding it.

---

## Figure: ch10-fig02-ingress-fanout-and-name-based-hosts

**Anchor ID:** `ch10-fig02-ingress-fanout-and-name-based-hosts`
**Purpose:** Makes the single examinable discriminator between simple fanout and name-based virtual hosting visible in one glance — both put many Services behind one IP address, and they differ *only* in which part of the HTTP request the routing rule reads.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** two-panel comparative traffic-flow diagram (stacked panels, shared visual grammar)

**Content specification:**
Two stacked panels of identical construction, one above the other, separated by clear whitespace and each carrying a small-caps title. The upper panel is titled **SIMPLE FANOUT — split by PATH**; the lower is titled **NAME-BASED VIRTUAL HOSTING — split by HOST**. In each panel, traffic flows strictly left to right: two HTTP request stanzas on the left (rendered in monospace, two lines each: a request line and a `Host:` line), an inbound arrow into a single box labelled `203.0.113.10`, an arrow from that box into a second box labelled `reads: path` (upper panel) or `reads: host` (lower panel), and then a fork from that second box to two Service boxes stacked on the right. In the upper panel the requests are `GET /catalog HTTP/1.1` / `Host: shop.example.com` and `GET /checkout HTTP/1.1` / `Host: shop.example.com` — note both carry the *same* host — and the fork edges are labelled `path = /catalog` (to the `catalog Service` box) and `path = /checkout` (to the `checkout Service` box). In the lower panel both requests are `GET / HTTP/1.1` — the *same* path — with hosts `shop.example.com` and `blog.example.com`, and the fork edges are labelled `host = shop…` (to `shop Service`) and `host = blog…` (to `blog Service`). The single most important visual element is the emphasis rule that underlines the exact fragment of each request the rule matched on: in the upper panel it underlines the path (`/catalog`, `/checkout`); in the lower panel it underlines the hostname (`shop.example.com`, `blog.example.com`). That underline replaces the ASCII's `▲▲▲` carets and must be rendered as a weighted Brass rule beneath the matched characters, tight to the monospace glyphs, not as a separate callout. A two-line caption sits beneath both panels: *"Same address in both. Same number of Services in both."* and a legend line explaining that the underline marks the part of the request the rule matched on.

**Visual style:**
- Palette: Lodestar book default — navy line-art on cream, slate fills for boxes, monospace set in Fira Mono
- Size (pixels): 1100x900 landscape
- Font: inherit book default (Roboto Slab for panel titles, Fira Sans for edge labels and caption, Fira Mono for request stanzas and box contents)
- Accent color for highlighted elements: Brass `#B58B3E` for the match-emphasis underline and for the `reads:` box border

**Critical details (non-negotiable accuracy):**
- **The IP address `203.0.113.10` is identical in both panels, and must be visibly identical.** If a designer varies it, the figure's entire argument collapses.
- **Upper panel: both requests carry the same `Host`. Lower panel: both requests carry the same path (`/`).** These are the controls in the comparison; changing either one destroys the point.
- The emphasis underline must fall on the **path** in the upper panel and the **hostname** in the lower panel. Reversed, the figure teaches the exact misconception it exists to prevent.
- Both panels have **two** Service boxes. Not three, not one. The Service count is held constant across the comparison on purpose.
- Panel order is fixed: fanout on top, virtual hosting below. It matches the order of the two manifests in §2 and the order of the Fixed Point that precedes the figure.
- Request stanzas must remain valid HTTP request-line syntax (`GET /catalog HTTP/1.1`), not prose paraphrase.
- The `reads: path` / `reads: host` boxes are decision points, not servers. Do not render them with a server, load-balancer, or cloud icon.

**Source ASCII (for designer reference):**
```
                    SIMPLE FANOUT — split by PATH

   GET /catalog HTTP/1.1                     ┌──────────────────┐
   Host: shop.example.com                    │  catalog Service │
        ▲▲▲▲▲▲▲▲                             └──────────────────┘
                                                      ▲
        ┌──────────────┐    ┌──────────────┐          │ path = /catalog
   ───▶ │ 203.0.113.10 │───▶│ reads: path  │──────────┤
        └──────────────┘    └──────────────┘          │ path = /checkout
                                                      ▼
   GET /checkout HTTP/1.1                    ┌──────────────────┐
   Host: shop.example.com                    │ checkout Service │
        ▲▲▲▲▲▲▲▲▲                            └──────────────────┘


           NAME-BASED VIRTUAL HOSTING — split by HOST

   GET / HTTP/1.1                            ┌──────────────────┐
   Host: shop.example.com                    │   shop Service   │
         ▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲                    └──────────────────┘
                                                      ▲
        ┌──────────────┐    ┌──────────────┐          │ host = shop…
   ───▶ │ 203.0.113.10 │───▶│ reads: host  │──────────┤
        └──────────────┘    └──────────────┘          │ host = blog…
                                                      ▼
   GET / HTTP/1.1                            ┌──────────────────┐
   Host: blog.example.com                    │   blog Service   │
         ▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲                    └──────────────────┘

   Same address in both. Same number of Services in both.
   ▲▲▲ marks the part of the request the rule matched on.
```

**Proposed filename:** `ch10-fig02-ingress-fanout-and-name-based-hosts.png`

```yaml-figure-spec
anchor_id: ch10-fig02-ingress-fanout-and-name-based-hosts
diagram_type: data_flow
source_ascii: |2
                      SIMPLE FANOUT — split by PATH

     GET /catalog HTTP/1.1                     ┌──────────────────┐
     Host: shop.example.com                    │  catalog Service │
          ▲▲▲▲▲▲▲▲                             └──────────────────┘
                                                        ▲
          ┌──────────────┐    ┌──────────────┐          │ path = /catalog
     ───▶ │ 203.0.113.10 │───▶│ reads: path  │──────────┤
          └──────────────┘    └──────────────┘          │ path = /checkout
                                                        ▼
     GET /checkout HTTP/1.1                    ┌──────────────────┐
     Host: shop.example.com                    │ checkout Service │
          ▲▲▲▲▲▲▲▲▲                            └──────────────────┘


             NAME-BASED VIRTUAL HOSTING — split by HOST

     GET / HTTP/1.1                            ┌──────────────────┐
     Host: shop.example.com                    │   shop Service   │
           ▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲                    └──────────────────┘
                                                        ▲
          ┌──────────────┐    ┌──────────────┐          │ host = shop…
     ───▶ │ 203.0.113.10 │───▶│ reads: host  │──────────┤
          └──────────────┘    └──────────────┘          │ host = blog…
                                                        ▼
     GET / HTTP/1.1                            ┌──────────────────┐
     Host: blog.example.com                    │   blog Service   │
           ▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲                    └──────────────────┘

     Same address in both. Same number of Services in both.
     ▲▲▲ marks the part of the request the rule matched on.
vendor_terms: [ingress, service]
complexity_hint:
  node_count: 12
  edge_count: 10
  label_count: 16
pedagogy:
  part_18_criteria_met: [distinguishing_alternatives, spatial_structure, fixed_point]
  learning_outcome: "Distinguish simple fanout from name-based virtual hosting by identifying which part of the HTTP request the Ingress rule reads"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The underline beneath the matched request fragment — the path in the upper panel, the hostname in the lower — together with the two 'reads:' decision boxes"
accessibility:
  alt_text_seed: "Two stacked panels comparing Ingress routing. In the upper panel, two HTTP requests share the host shop.example.com but differ by path; a single IP address 203.0.113.10 feeds a box labelled 'reads: path' that forks to a catalog Service and a checkout Service. In the lower panel, two requests share the path slash but differ by host; the same IP address feeds a box labelled 'reads: host' that forks to a shop Service and a blog Service. The matched fragment of each request is underlined."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Generic boxes, plain text, and example-range addresses (203.0.113.0/24, RFC 5737) only; no CNCF icon assets reproduced. If the renderer substitutes a Kubernetes icon pack, re-evaluate as licensed_icon_set."
```

---

## Figure: ch10-fig03-gateway-api-role-split

**Anchor ID:** `ch10-fig03-gateway-api-role-split`
**Purpose:** Shows that Gateway API's resource model is a direct consequence of its role-oriented design — each of the three organisational roles owns exactly one resource kind — and encodes the examinable cardinality (one GatewayClass per Gateway; many Routes per Gateway) into the same picture.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** hierarchical tree drawn inside three horizontal ownership bands (swimlane hierarchy)

**Content specification:**
Three full-width horizontal bands stacked vertically, each with its role name set in small caps at the upper-left inside the band. Top band: **INFRASTRUCTURE PROVIDER**, containing a single centred box labelled `GatewayClass`. Middle band: **CLUSTER OPERATOR**, containing a single centred box labelled `Gateway`. Bottom band: **APPLICATION DEVELOPER**, containing three side-by-side boxes each labelled `HTTPRoute`. A single edge runs vertically from the `Gateway` box up through the band boundary to the `GatewayClass` box, labelled **`exactly 1`**. Three edges fan from the three `HTTPRoute` boxes up through the band boundary to the `Gateway` box, collectively labelled **`many (parentRefs)`** with the label placed once, near the middle edge, rather than repeated three times. The bands are the point of the figure: they are ownership boundaries, and the edges deliberately cross them, which is what makes the seams between roles visible. A caption beneath the lowest band reads: *"Bands are ownership boundaries, not runtime layers."* — this caption is mandatory and must not be dropped for space, because without it a reader will misread the bands as a north-south request path. Vertical ordering is fixed (provider on top, developer at the bottom) and reflects ownership scope, not traffic direction.

**Visual style:**
- Palette: Lodestar book default — navy borders, three bands distinguished by graduated slate tints (lightest at the top or bottom, consistently graduated), resource boxes in cream with navy rule
- Size (pixels): 1000x850 landscape
- Font: inherit book default (Roboto Slab small caps for band/role names, Fira Mono for resource kind names, Fira Sans for edge labels and caption)
- Accent color for highlighted elements: Brass `#B58B3E` for the two cardinality labels (`exactly 1`, `many (parentRefs)`) and their edges

**Critical details (non-negotiable accuracy):**
- **Role-to-resource mapping is the whole content and must be exact:** GatewayClass → infrastructure provider; Gateway → cluster operator; HTTPRoute → application developer. Any swap makes the figure teach a false fact that the chapter tests twice (Bearings #2 Q3, Practice Q12).
- **Cardinality must read correctly in both directions:** exactly one GatewayClass per Gateway; many HTTPRoutes attached to one Gateway. Exactly three HTTPRoute boxes is the intended rendering of "many" — do not reduce to two (reads as a pair) or expand to a crowd.
- The `parentRefs` label belongs on the route-to-Gateway edges, because that is the field an HTTPRoute uses to attach to its parent. It must not migrate to the Gateway-to-GatewayClass edge, which is `gatewayClassName`.
- **Do not add GRPCRoute to this figure.** §5 names four stable kinds but the figure intentionally depicts only the three role-mapped kinds the chapter teaches. There is an open `AUTHOR-REVIEW` note in the draft about snapshot drift on the stable-kind count (three vs four); if revision resolves that toward depicting all four, this figure changes and this spec must be regenerated. Until then, three.
- Bands must not be drawn with arrows between them, gradients suggesting flow, or any labelling that implies a request traverses them top to bottom.
- "Cluster operator" is a job role here, not the Kubernetes operator pattern. No gear, robot, or controller iconography on that band.

**Source ASCII (for designer reference):**
```
  ┌───────────────────────────────────────────────────────────┐
  │  INFRASTRUCTURE PROVIDER                                  │
  │                                                           │
  │                   ┌──────────────┐                        │
  │                   │ GatewayClass │                        │
  │                   └──────────────┘                        │
  └──────────────────────────▲────────────────────────────────┘
                             │ exactly 1
  ┌──────────────────────────┼────────────────────────────────┐
  │  CLUSTER OPERATOR        │                                │
  │                   ┌──────┴───────┐                        │
  │                   │   Gateway    │                        │
  │                   └──────────────┘                        │
  └───────────▲──────────────▲──────────────▲─────────────────┘
              │              │              │  many (parentRefs)
  ┌───────────┼──────────────┼──────────────┼─────────────────┐
  │  APPLICATION DEVELOPER   │              │                 │
  │     ┌─────┴─────┐  ┌─────┴─────┐  ┌─────┴─────┐           │
  │     │ HTTPRoute │  │ HTTPRoute │  │ HTTPRoute │           │
  │     └───────────┘  └───────────┘  └───────────┘           │
  └───────────────────────────────────────────────────────────┘

  Bands are ownership boundaries, not runtime layers.
```

**Proposed filename:** `ch10-fig03-gateway-api-role-split.png`

```yaml-figure-spec
anchor_id: ch10-fig03-gateway-api-role-split
diagram_type: hierarchy_tree
source_ascii: |2
    ┌───────────────────────────────────────────────────────────┐
    │  INFRASTRUCTURE PROVIDER                                  │
    │                                                           │
    │                   ┌──────────────┐                        │
    │                   │ GatewayClass │                        │
    │                   └──────────────┘                        │
    └──────────────────────────▲────────────────────────────────┘
                               │ exactly 1
    ┌──────────────────────────┼────────────────────────────────┐
    │  CLUSTER OPERATOR        │                                │
    │                   ┌──────┴───────┐                        │
    │                   │   Gateway    │                        │
    │                   └──────────────┘                        │
    └───────────▲──────────────▲──────────────▲─────────────────┘
                │              │              │  many (parentRefs)
    ┌───────────┼──────────────┼──────────────┼─────────────────┐
    │  APPLICATION DEVELOPER   │              │                 │
    │     ┌─────┴─────┐  ┌─────┴─────┐  ┌─────┴─────┐           │
    │     │ HTTPRoute │  │ HTTPRoute │  │ HTTPRoute │           │
    │     └───────────┘  └───────────┘  └───────────┘           │
    └───────────────────────────────────────────────────────────┘

    Bands are ownership boundaries, not runtime layers.
vendor_terms: [gatewayclass, gateway, httproute]
complexity_hint:
  node_count: 8
  edge_count: 4
  label_count: 11
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point, quantitative_relationships]
  learning_outcome: "Name the Gateway API resources and the organisational role each one belongs to, and state the cardinality between them"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The two cardinality labels and their edges — 'exactly 1' from Gateway up to GatewayClass, and 'many (parentRefs)' from the three HTTPRoutes up to Gateway"
accessibility:
  alt_text_seed: "Three stacked ownership bands. The top band, infrastructure provider, contains a GatewayClass box. The middle band, cluster operator, contains a Gateway box joined upward to GatewayClass by an edge labelled 'exactly 1'. The bottom band, application developer, contains three HTTPRoute boxes joined upward to the Gateway by edges labelled 'many, parentRefs'. A caption notes the bands are ownership boundaries, not runtime layers."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Kubernetes API kind names set as plain text in plain boxes; no CNCF logo, badge, or icon-pack asset reproduced. Re-evaluate as licensed_icon_set if the renderer substitutes vendor icons."
```

---

## Figure: ch10-fig04-networkpolicy-additive-selectors

**Anchor ID:** `ch10-fig04-networkpolicy-additive-selectors`
**Purpose:** Shows that two NetworkPolicies selecting the same Pod produce the **union** of what they permit, and — critically — shows the excluded peer as simply *ungranted* rather than *denied*, because the API has no deny rule to draw.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** concept diagram — two-source convergence into a single permitted set, with an explicitly unconnected element

**Content specification:**
The left third of the figure carries two policy stanzas, one above the other, set in monospace. The upper is labelled `POLICY A` with two lines beneath it: `podSelector: role=db` and `ingress from: app=web`. The lower is labelled `POLICY B` with `podSelector: role=db` and `ingress from: app=batch`. From each stanza's `podSelector` line, a **heavy double-rule edge** runs to a central box labelled across two lines `Pod` / `role=db` — one edge entering from above, one from below. These two heavy edges mean "chooses the subject." From the central Pod box, a single normal-weight arrow runs rightward into a rounded blob on the right labelled **PERMITTED SET**, containing three stacked lines: `app=web`, `+`, `app=batch`, and beneath them in smaller type the gloss `(one set, two grants)`. Below and to the right, deliberately separated by whitespace, sits a fourth, unconnected box labelled `app=other`, with a short annotation beside or beneath it reading: *no arrow. not denied — simply never granted.* A two-line legend in the lower left explains the edge weights: heavy double rule = `podSelector` (chooses the SUBJECT); normal rule = peer selector (chooses WHO MAY CONNECT). The single most important instruction for the illustrator is negative: **there is no denial mark anywhere in this figure.** No barrier, no crossed-out arrow, no red X, no slash, no lock, no shield near `app=other`. Its exclusion is rendered purely as the absence of a connection, which is the fact the surrounding Fixed Point asserts.

**Visual style:**
- Palette: Lodestar book default — navy line-art, slate box fills, the permitted-set blob in a soft cream/slate wash with a rounded (non-rectangular) outline to distinguish "a set" from "an object"
- Size (pixels): 1200x650 landscape
- Font: inherit book default (Fira Mono for selector expressions and labels, Fira Sans for the legend and annotation)
- Accent color for highlighted elements: Brass `#B58B3E` for the permitted-set blob outline and the `+` between its two grants

**Critical details (non-negotiable accuracy):**
- **No denial iconography of any kind.** A red X or blocked arrow on `app=other` directly contradicts the Fixed Point the figure illustrates ("there is no deny rule") and would be a factual error, not a style choice.
- **Both policies carry the same `podSelector: role=db`.** That identity is why they combine; if a designer varies one, the union no longer follows.
- The permitted set must render as **one set containing two grants**, not as two separate sets or two separate arrows to two destinations. The `+` and the `(one set, two grants)` gloss both carry this.
- Edge weights are semantic and must survive greyscale: `podSelector` edges are visibly heavier than peer-selector edges. This is the distinction Chapter 4 set up — one mechanism, two jobs — and the legend must remain attached.
- `app=other` must be visibly detached: no edge, no dotted edge, no ghosted edge. A dotted line reading as "attempted connection" would reintroduce the denial framing.
- Label text is case- and format-sensitive: `role=db`, `app=web`, `app=batch`, `app=other` are label selectors, not prose. Keep the `key=value` form.

**Source ASCII (for designer reference):**
```
   POLICY A                                          PERMITTED SET
   podSelector: role=db  ─────┐                    ╭───────────────╮
   ingress from: app=web      │                    │               │
                              ▼                    │   app=web     │
                        ┌───────────┐              │      +        │
                        │  Pod      │─────────────▶│   app=batch   │
                        │  role=db  │              │               │
                        └───────────┘              │  (one set,    │
                              ▲                    │   two grants) │
   POLICY B                   │                    ╰───────────────╯
   podSelector: role=db  ─────┘
   ingress from: app=batch
                                                     ┌───────────┐
   ═══▶  podSelector (chooses the SUBJECT)            │ app=other │
   ───▶  peer selector (chooses WHO MAY CONNECT)      └───────────┘
                                                       no arrow.
                                                       not denied —
                                                       simply never
                                                       granted.
```

**Proposed filename:** `ch10-fig04-networkpolicy-additive-selectors.png`

```yaml-figure-spec
anchor_id: ch10-fig04-networkpolicy-additive-selectors
diagram_type: concept_map
source_ascii: |2
     POLICY A                                          PERMITTED SET
     podSelector: role=db  ─────┐                    ╭───────────────╮
     ingress from: app=web      │                    │               │
                                ▼                    │   app=web     │
                          ┌───────────┐              │      +        │
                          │  Pod      │─────────────▶│   app=batch   │
                          │  role=db  │              │               │
                          └───────────┘              │  (one set,    │
                                ▲                    │   two grants) │
     POLICY B                   │                    ╰───────────────╯
     podSelector: role=db  ─────┘
     ingress from: app=batch
                                                       ┌───────────┐
     ═══▶  podSelector (chooses the SUBJECT)            │ app=other │
     ───▶  peer selector (chooses WHO MAY CONNECT)      └───────────┘
                                                         no arrow.
                                                         not denied —
                                                         simply never
                                                         granted.
vendor_terms: [networkpolicy, pod]
complexity_hint:
  node_count: 5
  edge_count: 3
  label_count: 14
pedagogy:
  part_18_criteria_met: [spatial_structure, fixed_point, distinguishing_alternatives]
  learning_outcome: "Predict the permitted set when multiple NetworkPolicies select the same Pod, and recognise exclusion as absence of a grant rather than denial"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "The permitted-set blob showing app=web plus app=batch as one unioned set"
accessibility:
  alt_text_seed: "Two NetworkPolicy stanzas, A and B, both selecting Pods labelled role equals db, one permitting ingress from app equals web and the other from app equals batch. Heavy edges run from both stanzas to a single Pod box, and a single arrow runs from that Pod to a rounded blob labelled permitted set containing app equals web plus app equals batch, glossed as one set with two grants. A fourth box labelled app equals other sits unconnected, annotated as not denied but simply never granted."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Abstract label-selector expressions and generic shapes; no vendor IP or icon assets present."
```

---

## Figure: ch10-zenith-nothing-without-a-controller

**Anchor ID:** `ch10-zenith-nothing-without-a-controller`
**Purpose:** Collects the chapter's four instances of *an object without its component does nothing* into one comparative view, and lands the asymmetry the Zenith turns on — three of the four failures announce themselves, and the fourth is silent.
**Replaces ASCII:** yes
**Mandatory:** yes
**Type:** four-column comparison matrix (parallel panels, three shared rows)

**Content specification:**
Four equal-width vertical panels side by side, each divided into three horizontal registers by full-width rules, so the registers read across as rows. **Row 1 — the object.** Each panel names a valid object in solid navy rule: panel 1 `Service` with `type: LoadBal.` beneath it; panel 2 `Service` with `selector: {}`; panel 3 `Ingress` with `host+path`; panel 4 `NetworkPolicy` with `podSelector`. Each carries a checkmark line reading `✓ valid`. **Row 2 — the missing component.** Each panel contains an inner box drawn in a **dashed or ghosted outline** naming the absent thing, with `( none )` beneath it: panel 1 `provider`, panel 2 `matching Pods`, panel 3 `Ingress controller`, panel 4 `network plugin`. The dashed treatment is the visual grammar for absence and must differ unmistakably from the solid rule of row 1. **Row 3 — the outcome.** All four panels read `nothing`. Panel 4 alone carries two additional lines beneath its `nothing`: `…and nothing tells you`. A single centred caption sits beneath all four panels in the chapter's canonical wording: *"An object without its component does nothing."* The figure's argument is the sameness of the first three rows across all four columns combined with the one difference in panel 4's third register — so the four panels must be visually identical in construction, spacing, and weight, with panel 4's extra lines as the only asymmetry. Do not decorate any panel to make it stand out beyond that.

**Visual style:**
- Palette: Lodestar book default — navy solid rule for present objects, ghosted slate dashed rule for absent components, cream ground
- Size (pixels): 1200x620 landscape
- Font: inherit book default (Fira Mono for object and component names, Fira Sans for `( none )`, the outcome row, and the caption)
- Accent color for highlighted elements: Brass `#B58B3E` on panel 4's `…and nothing tells you` lines only

**Critical details (non-negotiable accuracy):**
- **The four object/component pairings are the chapter's four collected instances and must not be reordered or resubstituted:** LoadBalancer Service → no provider; Service with empty selector → no matching Pods; Ingress → no Ingress controller; NetworkPolicy → no network plugin. The order is chronological in the reader's experience (two from Ch 9, then two from Ch 10) and Practice Q17 asks for them in that order.
- **All four objects are marked valid.** The failure is never in the object. A designer instinct to mark the failing panels with an error state would invert the chapter's central point.
- **The dashed/ghosted treatment on row 2 means "absent," not "optional" or "greyed out because unimportant."** It must read as a gap where something should be.
- **Panel 4 is the only panel with the extra outcome lines.** That single asymmetry is the whole payload. Three panels announce themselves; one does not.
- The caption is a verbatim brand-load-bearing sentence — *An object without its component does nothing* — retrieved from Chapter 3 and restated in Chapter 17. Do not paraphrase, shorten, or re-punctuate it.
- `selector: {}` in panel 2 must render as literal empty-map YAML, not as an empty box or a blank.

**Source ASCII (for designer reference):**
```
  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
  │   Service   │  │   Service   │  │   Ingress   │  │NetworkPolicy│
  │type:LoadBal.│  │selector: {} │  │  host+path  │  │ podSelector │
  │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │
  ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│
  │  provider   │  │matching Pods│  │ Ingress     │  │  network    │
  │   ( none )  │  │   ( none )  │  │ controller  │  │  plugin     │
  │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│  │  ( none )   │  │  ( none )   │
  │             │  │             │  │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│
  ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
  │   nothing   │  │   nothing   │  │   nothing   │  │   nothing   │
  │             │  │             │  │             │  │ …and nothing│
  │             │  │             │  │             │  │  tells you  │
  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘

           An object without its component does nothing.
```

**Proposed filename:** `ch10-zenith-nothing-without-a-controller.png`

```yaml-figure-spec
anchor_id: ch10-zenith-nothing-without-a-controller
diagram_type: concept_map
source_ascii: |2
    ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
    │   Service   │  │   Service   │  │   Ingress   │  │NetworkPolicy│
    │type:LoadBal.│  │selector: {} │  │  host+path  │  │ podSelector │
    │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │
    ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
    │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│
    │  provider   │  │matching Pods│  │ Ingress     │  │  network    │
    │   ( none )  │  │   ( none )  │  │ controller  │  │  plugin     │
    │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│  │  ( none )   │  │  ( none )   │
    │             │  │             │  │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│
    ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
    │   nothing   │  │   nothing   │  │   nothing   │  │   nothing   │
    │             │  │             │  │             │  │ …and nothing│
    │             │  │             │  │             │  │  tells you  │
    └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘

             An object without its component does nothing.
vendor_terms: [service, ingress, networkpolicy]
complexity_hint:
  node_count: 12
  edge_count: 0
  label_count: 16
pedagogy:
  part_18_criteria_met: [zenith, distinguishing_alternatives, spatial_structure]
  learning_outcome: "Recognise the object-without-its-component pattern across four unrelated objects, and identify which instance fails silently"
  fixed_point_emphasis: true
  fixed_point_emphasis_target: "Panel four's outcome lines, '…and nothing tells you'"
accessibility:
  alt_text_seed: "Four side-by-side panels, each with three rows. The top row names a valid object: a LoadBalancer Service, a Service with an empty selector, an Ingress with host and path rules, and a NetworkPolicy with a pod selector. The middle row of each panel shows a dashed, ghosted box naming an absent component — provider, matching Pods, Ingress controller, network plugin — each marked none. The bottom row reads nothing in all four panels; the fourth panel adds the words and nothing tells you. A caption reads: an object without its component does nothing."
rendering_hints:
  preferred_orientation: landscape
  grayscale_critical: true
  max_width_px: 1200
copyright_clearance:
  rights_holders: []
  clearance: own_interpretation
  notes: "Kubernetes API kind names as plain text in plain panels; no CNCF icon or logo assets reproduced."
```
`Write` to the diagnostics path was denied, so — per the precedent in `ch-09/diagnostics/curriculum-alignment.md`, which hit the same block — I'm emitting the deliverable to stdout for orchestrator capture.

**The finding that dominates it:** `research-manifest.md` Notes #3 pre-emptively warned about one specific sentence — the out-of-scope list's *"the model for NetworkPolicies are deny by default"* — and said "do not quote nine's parenthetical anywhere in the chapter," because it reads as the exact inverse of §6's Fixed Point. The draft quotes it three times (lines 1017, 1028, 1331) and at 1028 asserts it is "the same fact" as §6's additivity. It is not: §6 describes an *unselected* Pod's default posture; the source describes the rule algebra *inside* a policy that has already selected one. This re-arms trap #48, the chapter's own designated worst misconception.

---

```markdown
# Curriculum-Alignment Audit — KCNA Chapter 10

**Chapter:** 10 — *Traffic from Beyond the Cluster*
**Claimed objectives:** D2.1 (Container Orchestration → Networking), D2.2 boundary (→ Security)
**Draft audited:** `draft-v1.md`, 1401 lines (no `draft-voice.md` at this stage)
**Authority:** `cncf-kcna-curriculum-pdf-2026-08-23.md`
**Run date:** 2026-08-25

---

## ⚠ Headline — read before the tables

**Stage 2 wrote an explicit, pre-emptive warning about exactly one sentence. The draft quotes that sentence three times and asserts it means the same thing as the §6 Fixed Point it contradicts.**

`research-manifest.md` Notes #3 (lines 915–919) flagged bullet nine of the NetworkPolicy out-of-scope list — *"the model for NetworkPolicies are deny by default, with only the ability to add allow rules"* — and said, in terms:

> Read cold, "deny by default" is the exact opposite of §6's ★ Fixed Point that **a Pod is non-isolated in both directions by default**. […] **Recommendation:** state the ten items flat, as planned, but **drop the parentheticals** […] **Do not quote nine's parenthetical anywhere in the chapter.**

The draft quotes it three times:

| Line | Where | Form |
|---|---|---|
| **1017** | §7 `Dead Reckoning`, bullet 9 | parenthetical retained in full |
| **1028** | §7 "No explicit deny" prose | re-quoted, **and asserted to be "the same fact"** as §6's additivity |
| **1331** | Practice Q15 answer key | re-quoted a third time |

Line 1028 is the sharpest of the three. It says the out-of-scope list *"states the same fact as a limitation"* — but it is **not** the same fact. §6 (line 874) teaches the default posture of an **unselected** Pod: nothing is restricted. The source's phrase describes the rule algebra **inside a policy that has already selected a Pod**: no deny verb exists, only allows. The draft asserts an equivalence the source does not support, and does so 154 lines after teaching the opposite.

**Why this is a curriculum finding and not a prose nit.** Trap #48 — *"A Pod with no NetworkPolicy is closed by default"* — is the chapter's own designated most-consequential misconception (§6 Navigational Hazards, Bearings #3 item 2, Exam Alert row 6), and the entire Soundings question 4 → §6 arc exists to dislodge it. §7 then hands the reader the phrase "deny by default" three times, unqualified, as the chapter's closing statement on NetworkPolicy. A reader who studies §7 last re-arms the trap the chapter spent fourteen minutes defusing. That is a coverage failure of D2.1's `non-isolated-default` objective, not a stylistic preference.

Three edits close it. See **R1**.

**Second-order note on Stage 2 compliance.** Of the manifest's ten author notes, seven were adopted cleanly and three were not: **Note #3** (above), **Note #4** (hostname wildcards were told to omit and are taught at line 384), and **Note #1** (the Gateway Fixed Point rephrase). Nothing was invented to fill a gap, and the two hardest sourcing disciplines in the chapter — the unsourceable "silent failure" inference and the refusal to quantify trap frequency — are handled exemplarily. The failures are all *over*-inclusion against explicit advice to trim, which is the opposite failure mode from Chapter 9's.

---

## Objectives the outline claims to cover

CNCF publishes **four domain weights and a competency list** — no objective IDs below competency level and no competency weights. `D2.1` / `D2.2` and the lettered decomposition below are **authored Lodestar constructs**, taken from `outline.md` § Arc-outline inheritance ("Covers") plus the B6 section assignments. They are audited as the chapter's own declared contract, not as CNCF objectives.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D2.1-a | Exposure ceiling; the L4/L7 layer boundary | YES (§1, 136–150) | appropriate |
| D2.1-b | North-south / east-west traffic | YES (§1, 152–158) | appropriate |
| D2.1-c | Edge router; cluster network; nodes not on the public internet | YES (§1, 160–172) | appropriate |
| D2.1-d | Ingress — definition; HTTP/HTTPS-only remit | YES (§2, 186–202) | appropriate |
| D2.1-e | The four Ingress capabilities | YES (§2, 192) | appropriate |
| D2.1-f | Single-service Ingress; `defaultBackend` | YES (§2, 206–216 · 382) | appropriate |
| D2.1-g | Simple fanout (routes by URI) | YES (§2, 218–246) | appropriate |
| D2.1-h | Name-based virtual hosting (routes by host) | YES (§2, 250–288) | appropriate |
| D2.1-i | TLS termination via a `kubernetes.io/tls` Secret; cleartext onward | YES (§2, 320–352) | appropriate |
| D2.1-j | DNS discovery **vs** virtual hosting — opposite sides of the connection | YES (§2, 354–362) | appropriate |
| D2.1-k | Ingress rule structure — host, paths, `service.name`/`.port` | YES (§2, 364–369) | appropriate |
| D2.1-l | `pathType` — three values, required-ness, element-wise `Prefix` | YES (§2, 370–381) | **over-covered** — precedence rule beyond plan |
| D2.1-m | Hostname wildcards | YES (§2, 384) | **over-covered** — Stage 2 said omit; not in `kb_tags` |
| D2.1-n | Ingress controller — the prerequisite; what it configures | YES (§3, 396–412) | appropriate |
| D2.1-o | IngressClass; `ingressClassName`; the default-class annotation | YES (§3, 434–450) | appropriate |
| D2.1-p | Reference specification; controllers "operate slightly differently" | YES (§3, 452–462) | appropriate |
| D2.1-q | The Ingress freeze — **both** halves | YES (§4, 525–553) | appropriate |
| D2.1-r | `deprecated` as a formal Kubernetes status, contrasted | YES (§4, 555–570) | appropriate |
| D2.1-s | Gateway API — role-oriented design; the three roles | YES (§5, 583–597) | appropriate |
| D2.1-t | Resource model + cardinality (1 GatewayClass, many Routes) | YES (§5, 599–612) | **conflicted** — see R2 |
| D2.1-u | Gateway request flow, six steps, `Host:` header | YES (§5, 700–716) | appropriate |
| D2.1-v | Gateway API is an add-on / custom resources; not in a default cluster | YES (§5, 726–731) | appropriate |
| D2.1-w | NetworkPolicy scope — L3/L4, application-centric, one-or-both-ends | YES (§6, 793–812) | appropriate |
| D2.1-x | Three identifiers; subject-vs-peer selectors; `ipBlock` / CIDR | YES (§6, 814–858) | appropriate |
| D2.1-y | Ingress/egress isolation; non-isolated default; `policyTypes` | YES (§6, 860–878) | appropriate |
| D2.1-z | Additive semantics; no deny rule; order-independent | YES (§6, 880–886) | **undercut by §7** — see Headline |
| D2.1-aa | Both ends must allow the connection | YES (§6, 913–919) | appropriate |
| D2.1-ab | Default-deny by construction; empty `podSelector` | YES (§6, 925–960) | appropriate |
| D2.1-ac | The two unconditional exceptions (self, node-local) | YES (§6, 962–968) | appropriate |
| D2.1-ad | Plugin dependency; the silently-inert policy | YES (§7, 971–1005) | appropriate |
| D2.1-ae | The out-of-scope list, ten items | YES (§7, 1007–1030) | appropriate — **but see Headline** |
| **D2.2** | Security boundary: NetworkPolicy taught **once**, here; `securityContext` / RBAC deferred | YES, by design (§6, 806–812) | appropriate |
| — | `kubectl-describe-ingress` (declared in `outline.md` `kb_tags.commands`) | **NO** | — see note |

**Note on the absent command.** `kb_tags.commands` declares three; the draft ships `kubectl get ingress` (472, 494) and `kubectl get networkpolicy` (987). `kubectl describe ingress` appears nowhere — the only `kubectl describe` in the chapter is the source's own NetworkPolicy advice at line 858. The §3 plan wanted it "as the way you see that nothing has been assigned," but §3's own prohibition against building an Ingress troubleshooting workflow, plus Ch 16's ownership of application-side Service debugging, makes its absence defensible. **Trim the tag rather than add the command** — leaving it declared over-reports coverage to the book-level objective map.

**Note on the D2.1 / D2.2 seam.** B2's ordering rule #6 (teach NetworkPolicy once, in Networking; cross-bear from Security) is honoured exactly. §6 states the scope boundary, cross-bears back to Ch 2 §7 and forward to Ch 12 §5, and — correctly — declines to make Ch 12 §9's RBAC-parallel argument, spending only a forward bearing at line 967. Nothing falls in the seam.

---

## Objectives covered in the draft but NOT in the outline

Scope drift is real but bounded, and every item is sourced. Ranked by severity.

**1. GRPCRoute, named and glossed as a fourth stable kind (line 606).**
`outline.md` §5 carries an explicit ⚠: *"Do not teach GRPCRoute, TCPRoute, TLSRoute, ReferenceGrant, or the GAMMA initiative."* The 08-24 depth re-fetch states four stable kinds, so the draft is factually correct and self-flags the deviation in an `AUTHOR-REVIEW` at line 608. But Stage 2's actual recommendation (Notes #1) was narrower than what shipped: *"keep teaching the same three, but stop counting them… One clause in §5 acknowledging that other route kinds exist for other protocols costs nothing."* A full bullet in the same list is not one clause. **Retain the fact, downgrade the treatment — see R2.**

**2. Hostname wildcards (line 384).**
Sourced, but Stage 2 Notes #4 named it and said **"Recommendation: omit"** — "§2 is already the chapter's largest section and this is below the associate tier." Not in `kb_tags`. Three sentences plus a Chapter Summary implication.

**3. `pathType` precedence — longest match wins, `Exact` breaks ties (line 378, restated in Chapter Summary line 1366).**
Stage 2 Notes #4 approved the three values and required-ness and said **"do not teach the full matching table… One Fixed Point and one example."** The draft correctly omits the ten-row table but keeps the tie-break rule, which is table-adjacent reference material.

**4. The `namespaceSelector` / `podSelector` AND-vs-OR YAML distinction (line 858 `🪝 Snag`).**
Sourced from the depth snapshot, absent from the outline's §6 beats and from `kb_tags`. This is genuine YAML-authoring subtlety — "one YAML hyphen is the difference" — and is CKA-tier rather than associate-tier. The most defensible of the four expansions on pedagogical merit and the least defensible on tier.

**5. The `allow-all-ingress` inverse construct (line 947).**
Sourced. §6's seventh beat planned default-deny only. Cheap (two sentences) and it does real work — it demonstrates that union semantics cut both ways. **Recommend keeping.**

**6. `ipBlock`'s `except` field (line 832), shown but never explained.**
Appears inside the §6 teaching manifest with no prose gloss anywhere. Sourced (it is in the source's own example), so this is an exposition gap rather than drift: a field in a manifest the reader is asked to read closely, with no explanation of what it does. One clause fixes it, or drop the two lines from the manifest.

**7. Minor sourced elaborations, no curriculum action.** `policyTypes` defaults when omitted (876); reply traffic implicitly allowed / connection-aware (870); the "once a NetworkPolicy is created for a pod…" summary sentence (958). All three were either recommended by Stage 2 (Notes #5) or are load-bearing for facts already in scope. **Retain.**

**Correctly handled, recorded so downstream stages do not re-flag:**

- The **"silent failure" inference** (989) is presented exactly as Stage 2's Gaps table required — tagged claim and untagged inference in separate sentences, using the `chapter-03` line 597 idiom, explicitly labelled *"still an inference."* Best-in-book handling of an unsourceable claim.
- The **frequency refusal** (Exam Alert, "A note on frequency") declines to quantify trap incidence and says why. Per Part 14 guardrail #8 and **[B3]**.
- **No specific Ingress controller products** and **no specific CNI plugins** are named anywhere, per both the outline and Stage 2 Gaps.
- **North-south / east-west** (154) carries a `[source:]` tag to the blog snapshot with project attribution, exactly as Stage 2 Notes #6 permitted. The blog-vs-normative-docs tier distinction is not surfaced to the reader, which Stage 2 explicitly said was defensible. **No action.**
- **All four Ingress manifests** are the raw-example-verified versions (`foo.bar.com`, `service1`/`service2`, `https-example.foo.com`), not the fabricated variants Stage 2 Notes #9 caught. The ASCII figures at 290 and 616 are the book's own construction and are never presented as quoted source — the specific hazard Stage 2 Gaps flagged.
- **`endPort`**, the ten-row `pathType` table, `Resource` backends, and the `kubernetes.io/metadata.name` namespace-targeting label are all correctly absent.

---

## Depth mismatches

CNCF publishes no sub-topic weights. "Exam weight" below is the **authored allocation** — 5 points of a published 28% domain, ≈5% of the exam, the smallest allocation in Part III — apportioned by the chapter's own salience signals: the Exam Alert high-priority ordering and the "if you only have 15 minutes: **§3, §4, §6**" guidance. Draft depth is share of the 71 minutes of section time and share of the 17 practice questions.

| Objective | Chapter's own salience | Draft depth | Mismatch |
|---|---|---|---|
| D2.1-a/b/c — ceiling, layers, edge router | Scaffolding; outline: "keep this section short" | §1 ≈ 8% time · 2 Q | OK — instruction honoured |
| D2.1-d/e — Ingress remit, HTTP/HTTPS-only | **Highest** (Exam Alert #1; trap #43) | §2 · 2 Q (Q2, Q3) | OK |
| D2.1-g/h — fanout vs virtual hosting | High (Exam Alert #5) | §2 · 1 Q (Q4) | OK |
| D2.1-i — TLS termination | High (Exam Alert #6) | §2 prose, well sourced | **assessment thin** — carried only inside Q3's capability list |
| D2.1-l/m — `pathType`, wildcards, precedence | **Not in the Exam Alert at all**; wildcards not in `kb_tags` | ≈ ⅓ of §2 · 1 Q (Q5) | **over-covered** |
| D2.1-n/p — controller prerequisite, spec drift | **Highest** (Exam Alert #2; the chapter spine; 15-min path) | §3 ≈ 11% · 3 Q | OK |
| D2.1-o — IngressClass | Not in the high-priority list (was a blocked gap at outline time) | §3 · 1 Q (Q6) | graded item on an un-alerted fact — minor |
| D2.1-q/r — frozen vs deprecated | **Highest** (Exam Alert #3; 15-min path; pre-sold by Ch 9) | §4 ≈ 8% · 2 Q | **OK — best-calibrated section in the chapter** |
| D2.1-s…v — Gateway API | High (Exam Alert #4, #11); the API the project *recommends* | §5 ≈ 17% time · **1 Q** | **under-covered in assessment** (planned 2) |
| D2.1-w…ac — NetworkPolicy semantics | **Highest** (Exam Alert #7–#9, #12; six of ten traps) | §6 ≈ 20% · **3 Q** | **under-covered in assessment** (planned 4) |
| D2.1-ad/ae — plugin dependency, out-of-scope | **Highest** (Exam Alert #10) | §7 ≈ 11% · 2 Q | OK |
| §8 synthesis / Zenith | Cross-cutting theme #3 | ≈ 7% · 1 Q (Q17) | OK |

### The structural finding

Prose depth is well calibrated at the section level with one exception, and the exception has an ironic shape:

**§2 spends roughly a third of its twelve minutes on field-level configuration detail for the API the chapter simultaneously teaches is frozen and superseded — while §5, covering the API the Kubernetes project actually recommends, carries a single graded practice item.**

`pathType` element-wise matching, the `/aaa/bb` vs `/aaa/bbb` case, the longest-match/`Exact` tie-break, and hostname wildcard single-label semantics are configuration-authoring facts. KCNA is an associate-tier, knowledge-level credential; the CNCF curriculum names *Networking* as a competency and descends no further. Stage 2 reviewed exactly this material and recommended teaching the three values and required-ness and stopping. The draft went two steps past that recommendation and one step past it again with wildcards.

This is not an argument for gutting §2. The three `pathType` values, the required-ness, and one worked non-matching example are correctly in scope and well taught. The recommendation is to stop at the point Stage 2 named.

### The assessment-distribution finding

Actual practice-block distribution against `outline.md` § 7:

| Block | Planned | Actual | Delta |
|---|---|---|---|
| §1 ceiling / layer boundary | 2 | 2 (Q1, Q2) | — |
| §2 the Ingress object | 3 | 3 (Q3–Q5) | — |
| §3 the controller | 3 | **4** (Q6–Q9) | **+1** |
| §4 frozen | 2 | 2 (Q10, Q11) | — |
| §5 Gateway API | 2 | **1** (Q12) | **−1** |
| §6 NetworkPolicy semantics | 4 | **3** (Q13–Q15) | **−1** |
| §7 the limits | 1 | **2** (Q16, Q17) | **+1** |

Three outline requirements follow from those deltas, and two are unmet:

- **Retrieval budget: 6 of 32 = 18.75%**, against a 20% **[B3]** target and a planned 7 (3 Bearings + 4 Practice). Bearings deliver all three (#1 item 1 → Ch 9, #1 item 5 → Ch 3, #3 item 1 → Ch 4). Practice delivers three of four: Q2 → Ch 9, Q7 → Ch 3, Q17 → Ch 3. **The missing item is the planned Ch 4 §5 labels-and-selectors retrieval in the §6 block** — which is also, not coincidentally, where §6 lost its fourth question.
- **"At least four questions must require two sections at once."** Three qualify: Q11 (§2+§4), Q12 (§2+§5), Q17 (§3+§7+§8). **The missing one is the planned §6+§7 interleaving** — *"a policy that looks correct, traffic that flows anyway, and three candidate explanations of which two are in this chapter and one is not."* Q16 gives one explanation and does not reach into §6's exceptions. Bearings #3 item 5 carries the two-explanation version, but that is a checkpoint, not the practice set.
- **"Trap #42 must appear in two different question shapes."** Weakly met. Q8 is the clean shape ("nothing is wrong with the object"); Q17 names the instance inside a recall list. Substantively covered across the assessment set via Bearings #1 item 3; noted because the practice-set-internal requirement is not.

### Verified as meeting target — no action

- **≥4-back spacing floor: met with margin.** Bearings #3 item 1 (Ch 4, six back) is the floor item; Bearings #1 item 5 (Ch 3, seven back) and Practice Q7/Q17 (Ch 3) are redundancy. **The retrieval shortfall above is a budget miss, not a floor miss** — revision should not treat it as urgent for that reason.
- **Question budget:** 8 Soundings + 15 Bearings (5+5+5) + 17 Practice = 40. Matches plan exactly; Bearings exceed B4's floor of 10 as intended.
- **Trap coverage: complete.** All ten B1 traps (#42–#45, #47–#52) plus the four non-B1 additions appear in the Exam Alert table with named corrections — fourteen rows, matching the plan exactly.
- **Fixed Points:** ten across §1–§7, at least one in every section the frontmatter contract names.
- **Dead Reckoning:** present, §7, ten items, complete and in source order (though see the Headline on bullet nine's parenthetical).
- **Domain-weight disclosure:** the metadata line (4–6) carries the 28% figure with its CNCF source tag and the authored-allocation disclaimer, in the shipped house form. No competency weight is invented anywhere.

---

## Gaps the research stage flagged

| Gap / note | Stage 2 status | Draft handling | Verdict |
|---|---|---|---|
| **G25 — Gateway API detail** | **CLOSED** by the 08-23 snapshot and the 08-24 depth re-fetch | §5 teaches roles, resources, cardinality, request flow, installation, all sourced | **Correct** |
| **OQ #2 — IngressClass uncached** (blocking) | **CLOSED** — field, resource, manifest, default-class annotation all sourced | §3 lines 434–450, fully cited | **Correct** |
| **OQ #3 — `pathType` / default backend uncached** (blocking) | **CLOSED**, with an explicit "do not teach the full matching table" | Three values ✓, required-ness ✓, table omitted ✓ — **but precedence and wildcards added** | **Over-consumed** — see R3 |
| **OQ #7 — empty `podSelector`, default-deny manifest** | **CLOSED**; recommendation: *derive, name the idiom, still don't show the manifest* | Derives ✓, names the idiom with source ✓, adds the recommended "once a NetworkPolicy is created…" sentence ✓ — **and shows `default-deny-all`** | **Substantially correct**; manifest is a low-priority deviation |
| **Notes #1 — four stable kinds, not three** | Recommendation: teach the same three, **stop counting them**; one clause on other route kinds | Full GRPCRoute bullet; body says "four"; Fixed Point still bare-lists three; `AUTHOR-REVIEW` at 608 | **Partially handled** — see R2 |
| **Notes #3 — bullet nine's parenthetical** | Recommendation: **do not quote it anywhere** | Quoted at 1017, 1028, 1331; equivalence asserted at 1028 | **Not handled — the headline finding** |
| **Notes #4 — hostname wildcards** | Recommendation: **omit** | Taught at 384; implied in Chapter Summary 1366 | **Not handled** |
| **Notes #6 — north-south is blog-sourced, not normative** | Recommendation: soften the disclaimer, source tag defensible | Line 154 attributes to the project and tags A6 | **Correct** |
| **Notes #7 — deprecation policy sharpens §4** | Recommendation: use Rule #4a to make deprecation a *formal status* Ingress was not given | §4 lines 555–570 do exactly this, quoting Rule #4a | **Correct — model compliance** |
| **Notes #8 — quote the cleartext clause** | Recommendation: quote it verbatim | §2 quotes it; the `⚓ Worth Securing` marker cites it | **Correct** |
| **Notes #9 — fabricated YAML hazard** | Every manifest re-verified against raw example files | Draft uses the verified variants throughout | **Correct** |
| **Notes #10 — cardinality wording drift** | "No action unless a later audit flags it" | Line 610 presents "many" as a fair reading with a source tag | **Noted, not raised** — consistent with Stage 2 |
| **Gaps — "silent failure" unsourceable** | Confirmed unsourceable | Line 989 separates tagged claim from untagged inference, explicitly | **Correct — exemplary** |
| **Gaps — trap frequency** | No source exists | Exam Alert explicitly refuses to quantify and says why | **Correct** |
| **Gaps — `Prefix` final sentence extracted unreliably** | "Teach `Prefix` from the Examples table"; do not quote the omitted sentence | Line 375 uses only the clean transcribed text; the omitted sentence is not quoted | **Correct** |
| **Gaps — book coinages get no `[source:]` tags** | `exposure-ceiling`, `l4-l7-boundary`, `frozen-not-deprecated`, `absent-component-pattern` | Line 148's Fixed Point carries no source tag; line 549 tags the sourced facts, not the coined phrase | **Correct** |
| **Outline OQ #4 — Ch 3 already named the pattern** | Editorial, not a source gap | §3 (420–432) retrieves Chapter 3's phrase verbatim; §8 promotes rather than coins | **Correct** |

**Two `AUTHOR-REVIEW` comments remain open in the draft and both are correctly placed:** line 608 (three-vs-four kinds, addressed by R2) and line 1032 (the version-templated *"as of Kubernetes {{< skew currentVersion >}}"* rendered as "as of the current release", addressed by R6). Neither was papered over.

---

## Recommended fixes

Ordered by severity. **R1 is the only one that changes what a reader will believe about an exam-weighted fact.**

**R1 — §7: remove bullet nine's parenthetical and delete the equivalence claim.** Three edits, per Stage 2 Notes #3:

- **Line 1017** — cut the parenthetical. The Dead Reckoning bullet becomes *"The ability to explicitly deny policies."* The plan's requirement ("the ten out-of-scope items, stated flat, complete, in the source's own order") is satisfied by the bare items; Stage 2 confirmed the parentheticals are elaboration, not list content. Keep the parentheticals on bullets 3, 4 and 10, which are genuinely useful and carry no contradiction.
- **Line 1028** — delete *"the out-of-scope list states the same fact as a limitation, in the documentation's own words: the model is deny by default with only the ability to add allow rules."* It is not the same fact. Replace with the limitation stated in the book's own words: *you go looking for a deny rule, and the API has none — §6's union semantics, met from the side you will actually encounter them on.* The paragraph's existing final sentence already lands this without the quotation.
- **Line 1331** — same cut in the Q15 answer key. The preceding clause ("policies are additive and combine by union… the ability to explicitly deny policies is on the published out-of-scope list") carries the answer on its own.

If the author wants the phrase for its own sake, it needs an explicit reconciling clause — *the source means that once a policy selects a Pod, everything not allowed is denied; it does not mean an unselected Pod starts closed* — but cutting is cheaper, and Stage 2's advice was to cut.

**R2 — §5: stop counting the resources in the Fixed Point.** One edit at **line 612**. Per Stage 2 Notes #1, rephrase to *"the three resources this chapter uses — GatewayClass, Gateway, HTTPRoute — and the role each belongs to"*, so the Fixed Point does not read as a count that line 601 contradicts eleven lines above. Bearings #2 item 3 (741) already adopted the fix — "the three **role-mapped** resources" is exactly right — so this brings the Fixed Point into line with an item the draft got correct. Then demote **line 606** from a full bullet to a trailing clause on line 605 (*"…and GRPCRoute does the same for gRPC"*), which honours the outline's ⚠ while keeping the count honest. Exam Alert #11 and Chapter Summary line 1371 map roles to resources rather than counting and need no change. Retire the line-608 `AUTHOR-REVIEW`.

**R3 — §2: trim to the depth Stage 2 authorised.** Two cuts, ≈5 lines, no sourced fact lost that the exam plausibly reaches for:

- **Cut hostname wildcards entirely (line 384).** Stage 2 named it and said omit; it is not in `kb_tags`; nothing else in the chapter depends on it.
- **Cut the precedence rule (line 378) and the matching half of Chapter Summary line 1366.** Keep the three `pathType` values, the required-ness, and the `/aaa/bb` vs `/aaa/bbb` `🪝 Snag` at 380 — that is Stage 2's "one Fixed Point and one example," and the Snag is the one genuinely trap-shaped fact in the block.

The Chapter Summary row becomes: *`Exact`, `Prefix`, `ImplementationSpecific`. `Prefix` matches element by element, not by string prefix.*

**R4 — Rebalance the practice set, restoring both unmet requirements.** Three edits, growing 17 → 18:

- **Convert Q9** (§3, "should you expect identical behaviour under two controllers") into the **§6-block Ch 4 retrieval item** the outline specifies: *a single NetworkPolicy contains three selectors — one chooses the Pods the policy governs, two choose peers. Which is which, and what happens to the policy's effect if someone relabels a Pod the first selector was matching?* (Correct answer: relabelling removes it from the policy's subjects entirely, which — because policies are the only thing that isolates — makes it *less* restricted, not more.) Q9's fact survives at Bearings #1 item 4 and in the Exam Alert trap table. This single edit restores §6 to 4, §3 to 3, and the retrieval budget to 7 of 33 = **21.2%**.
- **Reshape Q16** into the planned **§6+§7 interleaving**: keep the silent-failure core, but require three candidate explanations of which two are in the chapter (unsupporting plugin; one of §6's unconditional exceptions) and one is not. That restores the fourth required two-section item without adding a question, and it differs from Bearings #3 item 5 in the discriminating move — rejecting a plausible-but-wrong candidate rather than listing two right ones.
- **Add one §5 item**, restoring the planned 2. Cardinality or the request flow are both clean multiple-choice shapes; the outline's own note ("neither should require memorising the four design principles as a list") still binds. Growing to 18 is consistent with the chapter's posture on B4 figures as floors to exceed — Bearings already went 10 → 15.

Net: §1 2 · §2 3 · §3 3 · §4 2 · §5 2 · §6 4 · §7 2 = **18**. Every block at or above plan; §7's +1 is Q17, which the outline itself over-subscribed and wanted positioned last.

**R5 — §6: gloss or drop `ipBlock`'s `except` (line 832).** One clause — *`except` carves ranges back out of the CIDR block* — or delete the two lines from the manifest. As it stands the reader is walked carefully through a manifest containing a field the chapter never mentions.

**R6 — §7: resolve the version-anchor `AUTHOR-REVIEW` (line 1032).** The out-of-scope list's *"as of the current release"* is faithful to a version-templated source but leaves the reader no decay anchor. Recommend a short lead-in naming the snapshot date rather than pinning a Kubernetes version the source does not actually state — pinning a version would assert more than the source does. Then retire the comment.

**R7 — Trim `outline.md` `kb_tags`.** Drop `kubectl-describe-ingress` (not shipped, and correctly not shipped). If R3 is accepted, also drop `path-type`'s precedence coverage from any book-level objective map; `path-type` itself stays. Leaving them declared over-reports coverage the draft does not have.

**R8 — Low priority, author's call: §6's `default-deny-all` manifest (lines 934–945).** Stage 2 Notes #5 recommended deriving without showing the YAML. The draft derives *first* and then shows it, which honours the pedagogical intent — the reader reasons to the answer before seeing it. Ten lines. **Recommend keeping**; recorded only so a later stage does not re-raise it as an unnoticed deviation.

**R9 — Out of remit, noticed.** The Attention Budget claims *"Total time: ~85 minutes"*; its thirteen rows sum to **124**. Section rows alone plus Soundings sum to 81. Chapter 9 carried the same discrepancy (95 claimed / 99 summed), so this looks systemic rather than local. Structural-lint territory, not curriculum — flagged here so it reaches someone.

---

## Verdict

**Conditional pass, blocked on R1.**

Against its own declared contract the draft is materially complete: **thirty-three of thirty-three sub-topics are addressed**, both blocking source gaps (IngressClass, `pathType`) closed cleanly, G25 closed, prose depth tracks the chapter's stated salience in seven sections of eight, all ten B1 traps carry named corrections, the ≥4-back spacing floor is met with margin, and the two hardest sourcing disciplines in the chapter — the unsourceable "silent failure" inference and the refusal to quantify trap frequency — are handled better than anywhere else in Part III so far. Nothing was invented to fill a gap.

Three things hold it back.

**First, and blocking: §7 hands the reader "deny by default" three times**, unqualified, as the chapter's closing word on NetworkPolicy — after §6 spent fourteen minutes establishing the opposite, and after Stage 2 flagged that exact sentence and said not to quote it anywhere. Line 1028 compounds it by asserting the two statements are the same fact. This actively re-arms trap #48, the chapter's own designated most-consequential misconception. R1 closes it in three cuts.

**Second, the chapter is deepest where the exam is shallowest and thinnest where the exam is likely deepest.** §2 spends a third of its time on field-level configuration detail for a frozen API — past the point Stage 2 explicitly authorised, and including one item Stage 2 said to omit outright — while §5, covering the API the project recommends, carries one graded practice question, and §6, carrying six of the chapter's ten traps, carries three against a planned four. R3 and R4 correct both directions in five edits.

**Third, two requirements the outline set are unmet in the practice set**: the Ch 4 retrieval item (leaving the budget at 18.75% against 20%) and the §6+§7 interleaving. Both are restored by R4, and both by editing existing questions rather than by growing the set beyond 18.

None of this is a drafting-judgement failure. The draft flagged its own two riskiest calls in `AUTHOR-REVIEW` comments and got the hard sourcing questions right. The pattern in what it missed is consistent and easy to state: **it consumed the newly-fetched depth wholesale where Stage 2 had told it to consume selectively.** That is a one-pass correction.
```

---

**What I could not do:** write the file. `Write` to `.pipeline-state/ch-10/diagnostics/curriculum-alignment.md` was denied, so the artifact is above rather than on disk. To land it, either re-run this stage through `pipeline/orchestrator.py` so the orchestrator captures stdout, or grant write access and I'll write it directly. I created no partial files.

**Three things worth your attention beyond the headline:**

1. **The failure mode is the inverse of Chapter 9's.** Ch 9 was under-covered because a Stage 2 write failure left it working from a stale corpus. Ch 10's Stage 2 landed everything *and* gave explicit trim guidance — and the draft consumed the new depth wholesale. Notes #3, #4 and #1 all said "less"; the draft did "more" in each case. If that pattern recurs on Ch 11, the research prompt's advisory notes may need to read as constraints rather than recommendations.

2. **`pathType` and Gateway API are inverted relative to exam value.** A third of §2 goes to configuration detail for the frozen API; the recommended API gets one graded question. Fixing both is five edits and no net question growth beyond 17 → 18.

3. **The `except:` field at line 832 is in a manifest the reader is told to read closely, and the chapter never says what it does.** Small, but it's the kind of thing a careful reader stops on.
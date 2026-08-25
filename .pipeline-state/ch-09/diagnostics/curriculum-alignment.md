Write is refused by the same guard Stage 2 hit, and this session is non-interactive so the prompt can't be answered. Emitting the deliverable to stdout for orchestrator capture, per the pipeline's design.

**Before the artifact — the finding that dominates it:** Stage 2 closed all three of this chapter's source gaps on 2026-08-24, but its snapshots were never written to `sources/` (same write block). The draft's three `AUTHOR-REVIEW` comments all say the fetches "have not landed," and it cites none of them. The snapshot bodies survive verbatim inside `research-manifest.md` §§1–3. So §1, §3 and §4 are under-covered against authority that already exists — which Rule 3 does *not* excuse.

---

```markdown
# Curriculum-Alignment Audit — KCNA Chapter 9

**Chapter:** 9 — *Every Pod Has an Address*
**Claimed objective:** D2.1 (Container Orchestration → Networking)
**Draft audited:** `draft-v1.md` (no `draft-voice.md` at this stage)
**Authority:** `cncf-kcna-curriculum-pdf-2026-08-23.md`, corroborated by `lf-kcna-exam-page-2026-08-23.md`
**Run date:** 2026-08-24

---

## ⚠ Headline — read before the tables

**Stage 2 closed all three of this chapter's source gaps. The draft consumed none of them.**

`research-manifest.md` records three targeted fetches completed on 2026-08-24, closing G11 (CNI), Open question #3 (Service port mechanics) and Open question #4 (EndpointSlice's own documentation). The draft carries three `AUTHOR-REVIEW` comments — at lines 192, 322 and 501 — each stating that the fetch **has not landed**, and writes to the weaker cached-source strength accordingly. `grep` for the three new snapshot IDs in `draft-v1.md` returns **zero** citations.

Cause: the Stage 2 run could not write to disk (its own closing note, `research-manifest.md` line 539, records every write path refused). The snapshot bodies survive **verbatim inside `research-manifest.md` §§1–3**, but the files `k8s-docs-network-plugins-2026-08-24.md`, `k8s-docs-endpointslices-2026-08-24.md` and `k8s-docs-service-ports-2026-08-24.md` **do not exist in `../Book-KCNA/sources/`**. The corpus assembled for this stage was keyed to the draft's citations, so it also omits them.

**Audit consequence.** Per Rule 3, an objective with no authoritative snapshot is a research-stage gap, not an alignment failure. That rule does **not** cover this chapter: the snapshots exist, so the resulting shortfalls in §1, §3 and §4 are genuine coverage findings against available authority — and they are the three highest-value fixes below.

This appears to be the failure mode commit `ae74aff` ("Research prompt: mandate the harvester's snapshot embed format") was written to prevent.

---

## Objectives the outline claims to cover

CNCF publishes **four domain weights and a competency list** — no objective IDs below competency level and no competency weights. The `D2.1` identifier and the sub-topic decomposition below are **authored Lodestar constructs**, taken from `outline.md` § Arc-outline inheritance ("Covers"). They are audited as the chapter's own declared contract, not as CNCF objectives.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D2.1-a | The Kubernetes network model — four rules | YES | appropriate |
| D2.1-b | Pod IP and the shared network namespace | YES | appropriate |
| D2.1-c | CNI / network plugin | YES | **reduced** — claim written to superseded source strength |
| D2.1-d | Service — the object and its motivation | YES | appropriate |
| D2.1-e | ClusterIP (and default-type behaviour) | YES | appropriate |
| D2.1-f | NodePort (incl. additivity) | partial | **shallow** — type only; port mechanics absent |
| D2.1-g | LoadBalancer (incl. "Kubernetes supplies none") | YES | appropriate |
| D2.1-h | ExternalName | YES | over-covered (2 of 21 practice items on one fact) |
| D2.1-i | Headless Services | YES | appropriate |
| D2.1-j | Services without selectors | YES | appropriate |
| D2.1-k | EndpointSlice | partial | **shallow** — conditions declined as uncached; source now exists |
| D2.1-l | The service proxy | YES | appropriate |
| D2.1-m | kube-proxy modes | YES | appropriate |
| D2.1-n | CoreDNS / cluster DNS addon | YES | appropriate |
| D2.1-o | Service and Pod DNS records | YES | prose appropriate; **assessment under-weighted** |
| D2.1-p | FQDN vs bare name | YES | prose appropriate; **assessment under-weighted** |
| — | `kubectl get services`, `kubectl describe service` (declared in `kb_tags`) | **NO** | — see note |

**Note on the two absent commands.** `outline.md` `kb_tags.commands` declares three; the draft ships only `kubectl get endpointslices`. This is **correct handling, not a gap** — `research-manifest.md` Gaps #2 records that neither of the other two appears with output in any cached page, and that no sample output may be invented. The `kb_tags` block over-declares. Trim the tags so the book-level objective map does not report coverage the draft does not have.

**Note on the D2.1 seam with Chapter 10.** The CNCF competency named "Networking" is broader than this chapter. NetworkPolicy, Ingress and the Gateway API are deferred to Ch 10 by explicit design, and service mesh to Ch 17; `research-manifest.md` Gaps #3 confirms the deferral and forbids mining the cached `network-policies` and `ingress` snapshots here. Every deferred item has a named destination, so **nothing falls in the seam** — but the ~7% authored allocation is only defensible if Ch 10 carries the remainder, and the book-level objective map should record the split explicitly.

---

## Objectives covered in the draft but NOT in the outline

Scope drift is modest. The draft tracks the outline's section plan closely; the four items below are unplanned expansions, ranked by severity.

**1. Comparative performance of CNI plugins vs kube-proxy — unsourced, and self-contradicting.**
§6's `Closer Look` states Cilium can replace kube-proxy "usually with better performance characteristics at scale." No cached or fetched source makes any performance claim about any plugin or mode. The chapter's **own** Bearings #3 item 3 answer key, ~15 pages later, explicitly disclaims exactly this: *"it makes no claim about which mode is faster, more scalable, or better... neither does this book."* The outline mandated that discipline for modes; the draft honoured it for modes and broke it for plugins. Outside the competency at associate tier regardless.

**2. EndpointSlice `serving` condition (§4 `Closer Look`).**
Sourced from `k8s-docs-pod-termination-2026-08-24.md`, so factually sound — but the outline's Open question #4 told the drafter not to reach for "the conditions vocabulary" without the endpoint-slices fetch. Now moot: the fetch landed and the conditions are properly sourced. **Retain and formalise** rather than trim (see R4).

**3. Cloud cost of LoadBalancer addresses (§3).**
"In most clouds each of those addresses is a billable resource with its own lifecycle." Plausible, hedged, and entirely unsourced. Commercial-model content is not in the Networking competency.

**4. Minor unsourced elaborations.**
`ping` behaviour against cluster IPs (§6 `Worth Securing`); "userspace... a retired mode" (Q18 explanation); "overlay-based plugins do encapsulate the traffic" (Bearings #1 item 1 explanation). All three are correct and all three sit in explanatory positions where the book's own reasoning is appropriate. Flagged for the fact-accuracy stage; **no curriculum action**.

**Correctly handled, recorded so downstream stages do not re-flag:** the "nothing is listening on the cluster IP" claim is presented as the book's own explanation and is never quoted — exactly as `research-manifest.md` Notes #8 requires. `dnsPolicy` appears only in a §7 `Closer Look`, absent from the Exam Alert and from every question, per the outline's recommendation. Dual-stack and Windows specifics are held to sourced clauses with nothing built on them.

---

## Depth mismatches

CNCF publishes no sub-topic weights, so "exam weight" below is the **authored allocation** (~7% of a published 28% domain) apportioned by the chapter's own priority ordering — its Exam Alert high-priority list and its "if you only have 15 minutes" guidance, which names **§3 and §7** as the two exam-point concentrations. Draft depth is measured as share of the 81 minutes of section time and share of the 21 practice questions.

| Objective | Chapter's own salience | Draft depth | Mismatch |
|---|---|---|---|
| D2.1-a/b — network model, Pod IP | High (Exam Alert #1, #2) | §1 ≈ 15% time · 4 Q | OK |
| D2.1-c — CNI | Medium (Exam Alert #12) | share of §1 · 1 Q | **under-covered** — claim at reduced strength, source now available |
| D2.1-e/f/g/h — the type ladder | **Highest** (Exam Alert #3–#6) | §3 ≈ 20% time · 5 Q | OK on types; **port mechanics 0%** |
| D2.1-f — port/targetPort/nodePort, range | Newly sourced; MC-exam-shaped | **absent** | **under-covered** |
| D2.1-h — ExternalName | High | 2 of 5 §3 questions | **over-covered in assessment** (Q8/Q9 test one fact) |
| D2.1-k — EndpointSlice, readiness gate | High (Exam Alert #11) | §4 ≈ 15% time · **6 Q** | **over-covered in assessment** (planned 4) |
| — terminating-endpoint retention | Marked "deeper than the exam requires" | prose + `Closer Look` + **graded Q13** | **over-covered** — above-tier fact carries a graded item |
| D2.1-i/j — headless, selectorless | Medium | §5 ≈ 11% time · 2 Q | OK |
| D2.1-l/m — kube-proxy, modes | Medium (Exam Alert #10) | §6 ≈ 9% time · 3 Q | OK |
| D2.1-n/o/p — CoreDNS, records, FQDN | **Highest** (Exam Alert #9; named in the 15-minute path) | §7 ≈ 17% time · **1 Q** | **under-covered in assessment** (planned 3) |
| §8 synthesis / Zenith method | Outline: "the only question that tests the Zenith" | §8 ≈ 6% time · **0 Q** | **under-covered** — required item absent |

### The assessment-distribution finding

Prose depth tracks salience well. **The practice set does not.** Actual block distribution against the outline's plan:

| Block | Planned | Actual | Delta |
|---|---|---|---|
| §1–§2 model, CNI, why-a-Service | 4 | 4 (Q1–Q4) | — |
| §3 type ladder | 5 | 5 (Q5–Q9) | — |
| §4 selector / EndpointSlice / readiness | 4 | **6** (Q10–Q15) | **+2** |
| §5 headless, selectorless | 2 | 2 (Q16–Q17) | — |
| §6 kube-proxy | 3 | 3 (Q18–Q20) | — |
| §7 DNS and names | 3 | **1** (Q21) | **−2** |

Two unmet outline requirements follow directly:

- **"At least one [§7 item] must require the reader to *write* a name rather than recognise one."** No practice question constructs an FQDN. Q21 asks for the mechanism behind the search list. Bearings #3 item 4 does construct a name, but that is a checkpoint, not the practice set.
- **"At least five questions must require two sections at once."** Approximately three qualify (Q13, Q17, Q20). The two most distinctive planned interleavings — *Types + DNS* and the *§8 Zenith method* item — are both absent.

The chapter's densest pure-recall material (five DNS name shapes — the format multiple-choice exams favour most) carries **one** graded item, while material the chapter itself labels above-tier carries a graded item that turns entirely on it.

### Verified as meeting target — no action

- **Retrieval budget: 7 of 36 = 19.4%** against a 20% target. Bearings 3 (items #1.2 ch5, #1.4 ch6, #2.1 ch6) + Practice 4 (Q2 ch5, Q10 ch4, Q12 ch5, Q21 ch4). Exactly the planned 3/4 split.
- **≥4-back spacing floor:** met by Ch 5 at Bearings #1 item 2 (four back), with Ch 4 redundancy at Q10 (five back), as specified.
- **Question budget:** 8 Soundings + 15 Bearings (5+5+5) + 21 Practice = 44. Matches plan; exceeds B4's Bearings floor of 10 as intended.
- **Trap coverage:** all eight B1 traps (#35–#41, #46) plus six non-B1 traps appear in the Exam Alert table, each with a named defusal site. The each-container-gets-an-IP misconception appears as a distractor (Q1-C, Q2) in addition to its Bearings appearance, as required. The "nothing is wrong" §4 item is present (Q15).
- **Domain-weight disclosure:** the metadata line carries the authored-allocation disclaimer in the shipped house form.

**One caveat on trap #37.** The outline required it "at least twice in two different question shapes." Its exact wrong form appears once in the practice set (Q6 distractor A); the additivity *rule* is exercised a second time at Q5 distractor C and again at Bearings #1 item 3. Substantively met across the assessment set; noted because the practice-set-internal requirement is not.

### One unsourced weighting claim

"Why This Chapter Matters" asserts *"Networking is the largest of Domain 2's four competencies."* No source supports this — `research-manifest.md` Notes #9 confirms CNCF names the competencies without weights, and `outline.md` Open question #12 concedes the point. The claim is also **internally inconsistent** with the chapter's own ~7% allocation, which is precisely 28% ÷ 4, the even split. Either the competency is the largest and the allocation should exceed 7%, or the allocation is right and the claim must go.

---

## Gaps the research stage flagged

| Gap | Stage 2 status | Draft handling | Verdict |
|---|---|---|---|
| **G11 — CNI** | **CLOSED.** Sourced: *"A CNI plugin is required to implement the Kubernetes network model."* | `AUTHOR-REVIEW` at line 192 says fetch not landed; Fixed Point written to weaker cached strength | **Not handled** — stale. Fix available |
| **G13 — CoreDNS / DNS** | Confirmed already closed | Fully sourced; five record shapes, search-list mechanism, addon-manager sentence | **Correct** |
| **G24 — kube-proxy modes** | Confirmed already closed | Four modes, default identified, version parenthetical, no question turns on it | **Correct** |
| **OQ #3 — Service port mechanics** | **RESOLVED** in favour of teaching (option a) | `AUTHOR-REVIEW` at line 322 says fetch not landed; §3 stays silent | **Not handled** — silence was the right fallback, but the fallback is now unnecessary |
| **OQ #4 — EndpointSlice's own shape** | **RESOLVED** | `AUTHOR-REVIEW` at line 501 lists what is not asserted; §4 infers from five snapshots | **Not handled** — stale |
| **CoreDNS customisation scope-out** | Not a gap | `AUTHOR-REVIEW` at line 834 records the omission as deliberate | **Correct** |

**Gap-handling discipline is otherwise good.** Every gap sits behind an `AUTHOR-REVIEW` comment at the exact point of the claim, each stating what is and is not asserted, and no gap was filled by invention. The failure is upstream plumbing, not drafting judgement — the drafter did the right thing with the information it had.

**Two Stage 2 author notes the draft did not act on**, both flagged in the manifest and both landing on the section-pinned §1/§4:

1. **⚠ Route to fact-accuracy — §1's "the kubelet executes" is superseded.** §1 states CNI plugins are *"external programs that the kubelet executes."* `research-manifest.md` Notes #1 records that two official pages disagree, and that the specific, more recent page states CNI management was **removed from the kubelet in Kubernetes 1.24**, with the container runtime loading the plugins. The draft leans on the stale general page. Not adjudicated here — this is the fact-accuracy stage's call — but it lands on a pinned claim and Stage 2's recommendation is on file (name the runtime, or name no executor at all).

2. **"endpoints controller" and "EndpointSlice controller" appear as two names with no reconciliation.** §4 uses "the EndpointSlice controller"; §5 uses "the endpoints controller" (quoting the Service page); Q12's answer uses "the endpoints controller" while Bearings #2 item 1's answer uses "the EndpointSlice controller." `research-manifest.md` Notes #6 warned the draft "must not imply these are two different controllers." It does not reconcile them anywhere. A reader who met the controller list in Ch 3 will read the second name as a second component.

---

## Recommended fixes

Ordered by dependency. **R1 blocks R2–R5.**

**R1 — Land the three Stage 2 snapshots before revision runs.** Extract §§1–3 of `research-manifest.md` (they are complete, verbatim, with frontmatter) into `../Book-KCNA/sources/` as `k8s-docs-network-plugins-2026-08-24.md`, `k8s-docs-endpointslices-2026-08-24.md`, `k8s-docs-service-ports-2026-08-24.md`. Until these are on disk the revision stage cannot cite them and will reproduce the same three `AUTHOR-REVIEW` comments. Then re-run corpus assembly for this chapter.

**R2 — §1: strengthen the CNI Fixed Point to sourced full weight.** Replace *"A CNI network plugin implements it"* with *"A CNI plugin is **required** to implement the Kubernetes network model"* — verbatim-defensible from the new snapshot, and normatively stronger than the "ships none by default" clause the outline originally wanted. Update Exam Alert high-priority #12 and the trap-table row "Kubernetes ships the network" to match ("ships the *requirements*; a CNI plugin is *required* to implement them"). Retire the line-192 `AUTHOR-REVIEW`. Do **not** add the packaging claim; it remains unsourced.

**R3 — §1: remove "the kubelet executes."** Per Stage 2's recommendation, name the container runtime or name no executor. Naming none is safer at associate tier and costs the pinned CNI argument nothing. Route the adjudication to the fact-accuracy stage; flag here so it is not missed.

**R4 — §4: state the three EndpointSlice conditions as a documented set.** `ready` / `serving` / `terminating` are now properly sourced, giving §4 the clean chain it wants: readiness probe → Pod `Ready` → EndpointSlice `serving` → (absent termination) `ready`. Keep `publishNotReadyAddresses` out — it is a genuine exception to the readiness gate that would undercut the Fixed Point. Keep the 100-endpoints-per-slice default and `--max-endpoints-per-slice` out of the body entirely. Retire the line-501 `AUTHOR-REVIEW`.

**R5 — §3: add the port-mechanics block.** Place it where the draft's line-322 `AUTHOR-REVIEW` already identifies as its natural home, after the decision list: `port` / `targetPort` / `nodePort`, and the `--service-node-port-range` default of 30000–32767. Consider Stage 2's bonus — the *"NodePort and LoadBalancer are supersets of ClusterIP"* sentence states §3's additivity rule for both upper rungs at once, which is exactly what Bearings #1 item 3's answer-key requirement asks for. **Paraphrase rather than quote:** the manifest records transcription variance on that sentence, though the fact is corroborated verbatim by the older Service snapshot. Retire the line-322 `AUTHOR-REVIEW`.

**R6 — §4/§5: add one reconciling clause on the controller's two names.** One sentence at the §5 quotation is enough — the Service page's "endpoints controller" and Chapter 3's "EndpointSlice controller" name one job. Preserves §4's back-bearing to Ch 3 §3, which is what makes that cross-bearing land.

**R7 — Rebalance the practice set from §4 to §7, and restore the two required items.** Four edits, holding at 21 or growing to 22:

- **Retire Q13** (terminating-endpoint count). It is the only graded item turning on a fact the chapter itself labels above the exam's tier. Reuse the slot for a §7 item that requires the reader to **construct** an FQDN for a cross-namespace Service — the outline's unmet "write a name" requirement.
- **Convert Q8** (definitional "which type sets up no proxying"). Redundant with Q9, which tests the same fact in better scenario shape. Reuse the slot for the *Types + DNS* interleaving: same name form, normal vs headless, different answer — which restores a required interleaving and a §7 item at once.
- **Convert Q4** (why a Pod IP is a poor thing to store). Already tested at Soundings #3 and Bearings #1 item 4; the weakest item in its block. Reuse for the **§8 Zenith method** item the outline specifies as "the only question in the set that tests the Zenith," currently absent.
- **Add one §3 port-mechanics item** once R5 lands — `targetPort` semantics or the NodePort range, both plausible multiple-choice shapes. Growing the set 21 → 22 is consistent with the chapter's own posture on B4 figures as floors to exceed (Bearings already went 10 → 15). If the author prefers to hold at 21, this item displaces Q5, whose default-type fact is separately carried by Exam Alert #3 and the Chapter Summary.

Net effect: §1–§2 3 · §3 6 · §4 5 · §5 2 · §6 3 · §7 3 = 22.

**R8 — §6: delete the Cilium performance clause.** Cut "usually with better performance characteristics at scale." Unsourced, outside the competency, and contradicted by the chapter's own Bearings #3 item 3 answer key.

**R9 — Why This Chapter Matters: remove or source the "largest competency" claim.** Recommend cutting it. The structural argument that follows — Ch 10 needs the type ladder, Ch 13 needs the endpoint list — is sourced by the book's own cross-bearing map and carries the paragraph without it.

**R10 — §3: cut "a billable resource with its own lifecycle."** Unsourced commercial claim. The scaling argument ("expensive and awkward for fifty") survives intact and is what Ch 10 actually needs.

**R11 — Trim `outline.md` `kb_tags.commands`.** Drop `kubectl-get-services` and `kubectl-describe-service`, or accept their absence explicitly. Per Stage 2 Gaps #2, no cached page shows either with output and none may be invented. Leaving them tagged over-reports coverage to the book-level objective map.

**R12 — Record the D2.1 split in the book-level objective map.** Chapter 9 covers the model, Services, EndpointSlice, the service proxy and DNS; Chapter 10 carries NetworkPolicy, Ingress and Gateway API; Chapter 17 carries service mesh. Every item has a home today, but only in prose cross-bearings. Making the split explicit prevents a later restructure from orphaning one.

**R13 — Minor, out of scope but noticed.** The Attention Budget states "~95 minutes"; its rows sum to 99. R5 and R7 will add to that. Recheck the total during revision. Structural-lint territory, not curriculum.

---

## Verdict

**Conditional pass, blocked on R1.**

Against the outline's own declared contract the draft is close to complete: sixteen of sixteen sub-topics are addressed, prose depth tracks the chapter's stated salience, retrieval and spacing targets are met exactly, and every trap in the plan has a named defusal site. Gap handling is disciplined — nothing was invented to fill a hole.

Two things hold it back. First, **three topics are under-covered against sources that already exist** (CNI's strength, port mechanics entirely, EndpointSlice conditions) because a Stage 2 write failure left the draft working from a stale corpus; that is an alignment failure, not a research gap, and R1–R5 close it. Second, **the practice set drifted two questions from §7 to §4**, leaving the chapter's densest exam-shaped recall material with one graded item, the "write a name" requirement unmet, and the Zenith untested — while an explicitly above-tier fact carries a graded item; R7 closes that in four edits without growing the set beyond 22.

Neither problem is a drafting-judgement failure. Both are recoverable in one revision pass.
```

---

**What I could not do:** write the file. `Write` to `.pipeline-state/ch-09/diagnostics/curriculum-alignment.md` was refused and the session is non-interactive, so the permission prompt can't be answered — the same block Stage 2 reported. To land it, either re-run this stage through `pipeline/orchestrator.py` so the orchestrator captures stdout, or grant write access and I'll write it directly. I created no partial files.

**The three findings worth your attention beyond the headline:**

1. **`research-manifest.md` is currently the only copy of three snapshots.** It holds them verbatim with frontmatter in §§1–3. Extracting them to `sources/` is mechanical and unblocks the whole revision pass — R1 is genuinely blocking for R2–R5.

2. **The practice set is two questions off-plan in the worst direction.** §4 has 6 (planned 4), §7 has 1 (planned 3). §7 carries the five DNS name shapes — the most multiple-choice-shaped material in the chapter — and the outline's "write a name" requirement is unmet in the practice set. Meanwhile Q13 grades a fact the chapter's own `Closer Look` labels "deeper than the exam requires."

3. **Two self-contradictions the draft doesn't notice.** §6 makes a Cilium performance claim that Bearings #3 item 3 explicitly disclaims fifteen pages later; and "Networking is the largest of Domain 2's four competencies" sits beside an allocation of exactly 28% ÷ 4. Both are one-line cuts.
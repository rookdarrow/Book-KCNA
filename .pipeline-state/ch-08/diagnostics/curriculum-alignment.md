I have everything I need. Emitting the stage document to stdout (Write is stripped from this stage's tools, per the pipeline contract — the orchestrator captures stdout to `diagnostics/curriculum-alignment.md`).

---

I am the `curriculum_alignment_audit` stage. Per the pipeline contract the orchestrator writes my stdout to `diagnostics/curriculum-alignment.md`, so I emit the document rather than writing the file myself.

Two resolutions before the audit. The stage prompt's corpus note said the KCNA curriculum snapshot was not in this chapter's cached set; it **is** in the corpus at `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`, and I read it there rather than treating the authority as missing. And `draft-voice.md` does not exist because the voice stage writes **in place** — the voiced draft is `draft-v1.md` (1131 lines), with `draft-v1-prevoice.md` as the backup. All line cites are against `draft-v1.md`.

---

# Curriculum-Alignment Audit — KCNA Chapter 8

**Draft audited:** `.pipeline-state/ch-08/draft-v1.md` (voiced, 1131 lines, 2026-08-24T19:25)
**Objective authority:** `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`, corroborated by `sources/lf-kcna-exam-page-2026-08-23.md`
**Objective decomposition:** `book-outline/domain-analysis.md` §D1.2 (17 concept rows) + `book-outline/arc-outline.md` §Chapter 8 *Covers* (11 further mechanisms)

**Numbering caveat, stated once.** CNCF publishes **four domain weights and twelve named competencies, with no numbering and no sub-competency weights**. `D1.2` is a Lodestar convention declared as such at `domain-analysis.md:33`, and gap **G33** records that no authoritative basis exists for splitting D1's 44% across its four competencies. The `D1.2-NN` sub-IDs below are **this audit's** decomposition, not a CNCF taxonomy, and must not leak into shipped text. The draft's metadata line (L4–6) and its inline disclaimer handle the disclosure correctly.

**Headline: coverage is complete; the problem is upstream, not in the draft.** Of 28 auditable sub-objectives, **27 are covered and 1 is partial. None is uncovered.** Every `kb_tags.concepts` entry appears in the draft, and every one of the outline's out-of-scope boundaries holds (verified by search: Konnectivity, SSH tunnels, feature gates, `kubectl top`/`events`/`port-forward`/`debug`, PodDisruptionBudgets, `--ignore-daemonsets`, metrics-server, and RBAC/PSS/encryption-at-rest detail are all absent; the three matches for Ch 12 material are cross-bearing pointers, which the outline authorized).

The dominant finding is structural. **The research stage completed its fetches but never landed them on disk.** `research-manifest.md` opens with a write-blocker notice (L1–7) and carries all ten new snapshots as string literals inside an unexecuted Python writer script. `sources/` contains none of them. The drafting stage therefore drafted §2, §3, §4 and §7 against the pre-research corpus and flagged the shortfalls honestly in `AUTHOR-REVIEW` comments. **Both of the outline's BLOCKING gaps are closed in content and open on disk.** Three sub-objectives are consequently drafted at pre-research depth, and one stated answer key is unsourceable. The highest-leverage fix in this audit is running a script, not rewriting a chapter.

---

## Objectives the outline claims to cover

The outline claims exactly one competency: **D1.2 — Administration** (frontmatter `objectives: ["D1.2"]`, applied uniformly to all eight sections).

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.2-01 | Cluster planning axes — local vs HA, hosted vs self-managed, on-prem vs IaaS, bare metal vs VM, user vs contributor | YES (§5 L511–521) | appropriate |
| D1.2-02 | Managed vs self-hosted — who owns the control plane | YES (§5 L523–530, L539–553) | appropriate |
| D1.2-03 | Resource quota — per-namespace division of cluster resources | YES (§3 L309, L319–325) | **shallow — source-bounded** |
| D1.2-04 | Controlling access to the API — the three **sequential** gates | YES (§2 L216–246) | appropriate — **but the sequencing is asserted unsourced** |
| D1.2-05 | Authentication — establishing *who* | YES (§2 L226–231) | appropriate |
| D1.2-06 | Authorization — may this identity perform this action | YES (§2 L232–237) | appropriate |
| D1.2-07 | Admission controllers — intercept before persistence; may mutate or reject | YES (§2 L238–284) | appropriate — mutating/validating phase split absent |
| D1.2-08 | Auditing — recording the sequence of activities affecting the cluster | **PARTIAL** (§2 L285–291) | **shallow — named, not defined** |
| D1.2-09 | TLS bootstrapping — how a kubelet obtains its client certificate | YES (§2 L226–231) | appropriate (one clause) |
| D1.2-10 | Control-plane ↔ node communication — hub-and-spoke, one door | YES (§2 L293–301) | appropriate |
| D1.2-11 | Semantic versioning — `x.y.z` | YES (§6 L620–621) | appropriate |
| D1.2-12 | Supported versions — three minor branches, ~1 year patch support | YES (§6 L622–624) | appropriate |
| D1.2-13 | Version skew — kubelet (never newer; up to three older) | YES (§6 L638–648) | deep — justified |
| D1.2-14 | Version skew — kube-proxy | YES (§6 L638–648) | appropriate |
| D1.2-15 | Version skew — controller-manager / scheduler / CCM | YES (§6 L638–648) | appropriate |
| D1.2-16 | Version skew — kubectl (one minor, either direction) | YES (§6 L638–648, L668–681) | deep — justified |
| D1.2-17 | Version skew — HA apiservers within one minor | YES (§6 L638–648) | appropriate |
| D1.2-18 | `kubectl` syntax and verbs (arc *Covers*; gap **G1**) | YES (§1 L127–189) | deep — justified |
| D1.2-19 | kubeconfig and its precedence (arc *Covers*; **G1**) | YES (§1 L190–197) | appropriate |
| D1.2-20 | In-cluster authentication and the ServiceAccount namespace (**G1**) | YES (§1 L198–205) | appropriate |
| D1.2-21 | Bootstrap tooling — kubeadm, minikube, kind, k3s (**G28**) | YES (§5 L523–537) | appropriate |
| D1.2-22 | LimitRange — per-object constraint and defaulting (arc *Covers*) | YES (§3 L311, L319–351) | **shallow — source-bounded** |
| D1.2-23 | Node lifecycle — cordon / drain / uncordon (**G26**) | YES (§4 L430–460) | deep — justified |
| D1.2-24 | Node conditions — Ready (three-valued), Disk/Memory/PID/Network | YES (§4 L461–482) | appropriate |
| D1.2-25 | Node heartbeats — `.status` updates and `kube-node-lease` Leases | YES (§4 L483–492) | appropriate |
| D1.2-26 | Node registration and the node controller's three jobs | YES (§4 L422–429, L483–492) | appropriate |
| D1.2-27 | Release cadence — ~3 minor releases/year, ~15 weeks, monthly patches | YES (§6 L626–635) | appropriate |
| D1.2-28 | etcd backup and restore (**G27**) | YES (§7 L694–737) | appropriate |

**Note on D1.2-22 (LimitRange).** It is **not** in `domain-analysis.md`'s D1.2 concept map — B1 attests only "Resource quota." It enters via `arc-outline.md` §Chapter 8 *Covers* and via two published cross-bearings (`chapter-04` L590, `chapter-07` L430). That is a legitimate outline-authorized addition, not drift, and the reason B1 omitted it is now visible: **across all 137 files in `sources/`, LimitRange is substantively named in exactly one — `k8s-docs-cloud-native-security-2026-08-23.md`, in a single sentence** (verified by corpus-wide search). The draft's §3 is built on that one sentence, which is why it reads thin.

---

## Objectives covered in the draft but NOT in the outline

Drift is genuinely low — lower than Chapter 7's. Four items, ranked by the attention they deserve.

**1. Node `Capacity` / `Allocatable` — §4 L493–503. The one item worth an author decision.**
Three problems compound here. *Scope:* the primary snapshot `k8s-docs-node-allocatable-2026-08-24.md` is tagged `objectives_covered: ["D1.3"]` — Scheduling, not Administration — while the research stage tagged the same source page D1.2 for this chapter. The material sits on the competency boundary and is now taught in both chapters. *Duplication:* Chapter 7's own curriculum audit logged its §2 Capacity/Allocatable block (Ch 7 L227–229) as a mild over-run on an explicitly bounded concession; Chapter 8 now spends eleven more lines on the same pair. *Sourcing:* the load-bearing sentence — *"The two differ because some of the machine has to be reserved…"* — is unsourced, and the draft's own `AUTHOR-REVIEW` at L499 says so. This is authorized in principle (the outline's Open Question #6 recommended option (b)) but currently pays the Ch 7 promise with an assertion rather than a citation. The research has since closed it; see Recommended fixes #4.

**2. Verb-table column mislabel — §1 L168–180.** The column head is *"Where you met it"*, and the `logs` and `exec` rows are filled with **"Ch 13"** — a chapter four ahead. The verbs themselves are correctly sourced from the operations table and are not the ones the outline banned (`top`, `events`, `port-forward`, `debug` are all absent, verified). This is a label bug, not a scope breach, but it produces exactly the effect the outline warned against: a retrospective column that promises coverage the reader has not had.

**3. `Extended Analogy` in §2 (harbour pilot / harbourmaster / customs officer), L~264–270.** Not in the outline's planned marker list for §2 (Fixed Point, Mnemonic, Navigational Hazards, Closer Look). It introduces no objective content and it carries the mutate-vs-reject distinction well. **Marker inventory is the theming-density stage's lane — no action here.**

**4. DaemonSet toleration *mechanism* — §4 L436.** The outline planned "one exception worth naming"; the draft adds the mechanism (the DaemonSet controller automatically adds the `node.kubernetes.io/unschedulable` toleration), cited to `k8s-docs-daemonset-2026-08-24`. Sourced, one clause, and it is the payoff for a Ch 6 retrieval. **Keep.**

Nothing else reaches beyond the outline. §8's use of the D1.3-tagged taints snapshot, Practice Q7's crossing into requests/limits, and the Voyage Ahead's D2.1 preview are all outline-specified retrieval or structural handoff.

---

## Depth mismatches

CNCF publishes no sub-weights, so the weight column states the published signal (D1 = 44%) alongside the only fine-grained signals that exist: the chapter's own Attention Budget minutes (L15–27) and its Exam Alert priority list (L862–871), which declares where the chapter believes its points are.

| Objective | Exam weight signal | Draft depth | Mismatch |
|---|---|---|---|
| D1.2-03 / -22 quota + LimitRange | §3 = 12 min (8%); carries **2 published cross-bearings**, [B3]'s namespaces anchor, and the hinge Ch 12 derives RBAC from | 63 lines total, ~38 of prose — the thinnest teaching block in the chapter | **under-covered — source-bounded, now closed upstream** |
| D1.2-08 auditing | 1 of 12 named D1.2 concepts; comprehension tier | 2 sentences, no definition asserted | **under-covered — deliberate, and now over-cautious** |
| D1.2-04 three gates | §2 = 20 min (13%), **high**; carries priority topics #1 and #2 | appropriate prose depth | **OK in depth — the sequencing claim is unsourced, not shallow** |
| D1.2-13…-17 version skew | §6 = 20 min (13%), **high**; carries priority topics **#3, #4, #5** — four of ten | prose deep and correctly *derived* rather than printed | **prose OK — assessment layer under-built, see below** |
| D1.2-18 kubectl surface | §1 = 12 min (8%), rated **low**; excluded from the *"if you only have 15 minutes"* route | 89 lines — the longest teaching section | **deep — justified; hold.** G1 is a book-wide dependency and the verb table is Ch 13/16's inventory |
| Capacity / Allocatable | D1.3-tagged; Ch 7 already covered it | 11 lines, one unsourced sentence | **over-covered across two chapters** |
| D1.2-23 cordon/drain | §4 = 18 min (12%); priority topic #6, the one trap with an operational cost | deep, with figure and Hazard | **OK** |

**The assessment-layer mismatch, which is the sharpest depth finding in this audit.** The outline set the Practice distribution explicitly *by exam-point density rather than section count*. The draft's actual distribution inverts it in the two places that matter:

| Block | Outline | Draft | Delta |
|---|---|---|---|
| §1–§2 (incl. the §8 method item) | 5 | 5 | — |
| §3 quota / LimitRange | 2 (→3 if the fetch landed) | 3 | +1, licensed |
| §4 node lifecycle | 3 | **4** | **+1** |
| §5 ownership | 2 | 2 | — |
| §6 versions and skew | **4** | **2** | **−2** |
| §7 etcd | 1 | 1 | — |

§6 carries four of the chapter's ten declared priority topics and receives **two** of seventeen questions. The outline's specific requirement — *"#28 … must appear at least twice in two different question shapes, because applying the kubelet rule to `kubectl` is the chapter's most durable error"* — is **unmet**: trap #28 appears once in the Practice set, as distractor A in Q15. The outline's second §6 requirement (*"at least 2 must require applying a rule to a scenario"*) is half-met: Q14 applies, Q15 recognises. The Bearings #3 block carries §6 well, so the reader is not left unprepared — but the Practice set, which is the chapter's exam-simulation surface, under-weights its densest examinable section by half.

Everything else in the assessment layer checks out: Soundings 8/8, Bearings 15/15 across three checkpoints of five, Practice 17/17, chapter total 40. Retrieval lands at **7 of 32 items = 21.9%**, matching the outline's arithmetic and [B3]'s 20% target for this chapter. The **≥4-back spacing floor is satisfied twice** — Bearings #2 item 4 reaches Ch 2 (six back) and Practice Q11 reaches Ch 3 (five back) — which is what [B3] asked for at the floor's first live chapter. All four interleaving requirements are met (Q4, Q8, Q13, Q17).

---

## Gaps the research stage flagged

The manifest declares five gaps, **G-8A** through **G-8F**, plus ten *Notes for the author*. The draft could act on none of the closures, because none of the sources reached disk. Handling is therefore judged on what the drafting stage could see.

| Gap | Manifest instruction | Draft handling | Verdict |
|---|---|---|---|
| **G-8A** — no single source connects `kubectl cordon` to the `node.kubernetes.io/unschedulable` taint. **"AFFECTS A STATED ANSWER KEY."** Recommended (a): reword to ask what *marks a node unschedulable* | Bearings #2 item 1 ships unchanged (L559), answer key unchanged (L572), **no `AUTHOR-REVIEW` flag** | ❌ **not handled** — the one live correctness item |
| **G-8B** — citation drift: `k8s-docs-nodes-2026-08-23` carries the conditions table under a URL that no longer hosts it | Cite the new node-status file for conditions, Capacity/Allocatable and Info | §4 L461–482 cites the 08-23 file throughout | ⚠️ **pending the landing** — will read as a false positive to the fact-accuracy stage |
| **G-8C** — quota row descriptions not verbatim-verified | May enumerate what a quota counts; must not quote row descriptions | §3 enumerates nothing (the source never landed) | ✅ moot, and will bind once §3 is rebuilt |
| **G-8D** — audit *level* definitions not captured | Below budget; no re-fetch recommended | §2 asserts no level names | ✅ correct |
| **G-8E** — Capacity→Allocatable arithmetic remains unextractable (published only as `node-capacity.svg`) | Name `kube-reserved` / `system-reserved`; state no equation | §4 states no equation ✅, but names neither reservation ❌, substituting an unsourced paraphrase | ⚠️ **half-correct** |
| **G-8F** — deliberate non-fetches (Konnectivity, SSH tunnels, feature gates, RBAC/PSS detail, Ch 13/16 verbs, quota scopes, kubeadm runbooks) | Recorded so the audit does not read them as oversights | All absent from the draft, verified by search | ✅ correct |

**The two BLOCKING gaps the arc outline named are closed in content.** Open Question #2 is closed better than the outline hoped: `controlling-access` supplies *"Admission Control modules are software modules that can modify or reject requests"*, *"When multiple admission controllers are configured, they are called in order"*, and the persistence-order sentence *"Once a request passes all admission controllers, it is validated … and then written to the object store."* Open Question #3 is closed on both halves, including the rule §3 most needs — *"If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients **must** specify either `requests` or `limits`."* Neither is on disk, so the draft's §2 `AUTHOR-REVIEW` (L224) and §3 `AUTHOR-REVIEW` (L313) are accurate as written and correctly refuse to assert past the landed corpus. **Per Rule 3 this is a research-stage delivery failure, not a curriculum-alignment failure** — but it is the reason three sub-objectives sit at shallow depth, so it heads the fixes.

**Three manifest findings the draft could not have acted on, all now actionable:** `node-monitor-grace-period` has a documented default of **50 seconds** (§4 L481 currently declines to give one, correctly under the old instruction); *"cordoned nodes are marked Unschedulable in their spec"* converts §8's strongest demonstration (L~808) and Practice Q10 from reasoned inference to sourced claim; and *"`SchedulingDisabled` is not a Condition in the Kubernetes API"* is a ready-made Snag for §4.

**One internal inconsistency, introduced by the gap rather than by carelessness.** The §3 figure block (L327–351) draws each Pod as `min ≤ … ≤ max`, asserting a min/max bound structure that the prose deliberately withholds and that the `AUTHOR-REVIEW` at L313 names as *"NOT cached and therefore NOT asserted."* The figure teaches what the prose declines to. The landed `limit-range` snapshot resolves this in the figure's favour — *"Enforce minimum and maximum compute resources usage per Pod or Container in a namespace"* — so the fix is to bring the prose up, not the figure down.

---

## Recommended fixes

Ordered by leverage. One per issue.

**1. Land the research stage's ten snapshots before any revision work begins.** *(unblocks fixes 2, 3, 4 and the G-8B citation correction)*
`research-manifest.md` L21–842 is a complete, self-contained writer script; running it writes ten files into `sources/` and replaces the manifest with the real manifest. Nothing in this chapter's §2, §3, §4 or §7 should be edited before it runs, because every edit would be made against a corpus that is two stages stale. The write blocker the research stage hit is the same one this stage hits — `Write` is stripped from stage tools by design — so the script needs to be run by the orchestrator or by hand, not re-attempted from inside a stage.

**2. Rebuild §3 to the depth its two published cross-bearings promise.** *(D1.2-03, D1.2-22 — under-covered)*
§3 is the thinnest teaching block in the chapter and it is discharging `chapter-04` L590, `chapter-07` L430, [B3]'s namespaces anchor, and the scope hinge Chapter 12 *derives* the RBAC four-way matrix from. Four sourced additions, all inside the outline's scope guard: **what a quota counts** (compute totals, object counts, storage — names only, per G-8C); **the 403 rejection**; **the rule that makes a valid Pod stop being valid** (in a quota'd namespace, every new Pod must specify requests or limits — this is the single most examinable fact in the section and it is the causal link between §3's two mechanisms); and **LimitRange's min/max/default structure** plus *"validations occur only at Pod admission stage, not on running Pods."* Do **not** take quota scopes, scope selectors, priority-class quota, or the full countable-resource roster. The `AUTHOR-REVIEW` at L313 then comes out, and the figure at L327–351 stops asserting more than the prose.

**3. Source §2's sequencing and mutation claims.** *(D1.2-04, D1.2-07)*
The Fixed Point at L246 and Figure 8.2's fourth arrow are the chapter's most examinable single fact and are currently asserted with no citation, as the `AUTHOR-REVIEW` at L224 states. Once `controlling-access` lands, all four sub-claims cite directly. Two free upgrades worth taking while there: the **quorum contrast** the manifest surfaced (authorization is *any module approves and the request proceeds*; admission is *any module rejects and the request is refused immediately*) is a sharper Navigational Hazard than the one at L~258 and the source draws the contrast itself; and **admission does not see reads**, which is one clause and forecloses a plausible misreading. The mutating/validating **phase** split is genuinely optional at this tier — the outline never asked for it, and Chapter 12 does not need it.

**4. Pay the Chapter 7 promise with sources instead of an assertion — §4 L493–503.** *(over-covered, and the one unsourced sentence in the section)*
Replace the paraphrase at L~498 with the two verbatim facts the reservation page supplies: `kube-reserved` and `system-reserved` as the reservations that make Capacity and Allocatable differ, plus the motivation sentence — *"Pods can consume all the available capacity on a node by default. This is an issue because nodes typically run quite a few system daemons that power the OS and Kubernetes itself"* — which is precisely what Chapter 7 promised. **State no arithmetic** (G-8E stands). Two sentences discharge the promise honestly and the block gets shorter, not longer, which also relieves the duplication against Chapter 7 §2.

**5. Fix Bearings #2 item 1's answer key — L559 and L572.** *(the audit's one live correctness item)*
The question asks what command applies the `node.kubernetes.io/unschedulable` taint; the key answers `kubectl cordon`; **no source says that**, and the taints reference pulls the other way (*"The taint will be added to a node when initializing the node to avoid race condition"*). Take the manifest's recommendation (a): reword to ask **what command marks a node unschedulable**. The answer stays `kubectl cordon`, becomes fully sourced, and the Chapter 7 identity the item exists to test still lands through the spec field — which is now sourced outright by *"cordoned nodes are marked Unschedulable in their spec."* This also strengthens §8's strongest demonstration and Practice Q10, both of which currently rest on the same inference.

**6. Rebalance the Practice set toward §6.** *(assessment-layer depth mismatch)*
§6 carries four of ten priority topics and two of seventeen questions. Move one item from the §4 block (which runs 4 against a planned 3 — Q9 and Q10 overlap in what they test) into §6, and write the new item so that **trap #28 appears in a second, different shape** — the outline requires it twice and it currently appears once. Full restoration to the planned 4 would require reverting §3 to two questions, which the research now argues against; **three is the right reconciled target for §6**, and the second appearance of #28 is the non-negotiable part. While there: Practice Q14's explanation should carry the same currency caveat Bearings #3 item 1's key already carries — that the rules, not the roster, are what is being tested.

**7. Upgrade auditing from named to defined — §2 L285–291.** *(D1.2-08, partial)*
The outline chose option (b) — name it, assert nothing — *"unless the fetch is already cheap."* It was, and it landed. Take the definition (*"Kubernetes auditing provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster"*) plus one clause the manifest recommends and I endorse: auditing lives **inside the kube-apiserver**, which is the single-door architecture stated a fourth way and costs nothing in a section built on that architecture. Stages, levels and backends stay out — they are above budget, and G-8D confirms the level definitions were not verbatim-captured anyway.

**8. Low priority — relabel the §1 verb table's third column (L168).** *"Where you met it"* is wrong for the `logs` and `exec` rows, which point to Chapter 13. *"Where it lives in this book"* or splitting met/forthcoming both fix it. No objective impact.

**Explicitly not recommended, so the revision stage does not "fix" them.** §1's length (89 lines) — it is deep and justified: G1 is a book-wide dependency, `chapter-04` L316 promised *"kubectl, in full"*, and the verb table is Chapter 13's and 16's inventory. §6's prose — deriving four of five rows from one rule before printing the table is exactly the durable-encoding treatment [B3] asked for, and Bearings #3 item 2 tests which encoding happened. §2's Extended Analogy — theming-density's lane, and it carries the section's hardest distinction well. §4's refusal to state a `node-monitor-grace-period` value — the 50-second default may now be added *as a dated illustration, never as a rule*, per the outline's own standing instruction, but the examinable fact stays "Unknown means the control plane has not heard from the node." And the chapter's out-of-scope discipline is intact at every boundary the outline drew; nothing in the Exam Alert or Practice set reaches into Chapters 12, 13, 16 or 17.

---

**Summary for the orchestrator:** 28 sub-objectives, 27 covered, 1 partial, 0 uncovered. Drift low and mostly authorized. One live correctness item (G-8A, Bearings #2 item 1). One assessment-layer imbalance (§6 under-weighted 2:4). Three sub-objectives at shallow depth for a single upstream reason — **the ch-08 research stage's ten snapshots exist only inside `research-manifest.md` and have never been written to `sources/`.** Fix 1 gates fixes 2, 3, 4 and 7, and should run before the revision stage is dispatched.
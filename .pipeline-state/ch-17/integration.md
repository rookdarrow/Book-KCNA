Write permission wasn't granted — which matches the pipeline's own design (CLAUDE.md notes `Write` is removed from stage tooling so output flows through stdout). Emitting the document here instead; it's ready to save to `../Book-KCNA/.pipeline-state/ch-17/integration.md`.

---

# Integration Check — KCNA Chapter 17

**Method note.** The stage input carried no knowledge-base shards (`[no knowledge-base shards tagged]`), but Chapters 1–16 are all materialised at the book repo root, so every callback and terminology claim below was verified against shipped text rather than inferred. Cross-bearings were checked mechanically against the B6 section skeleton. Facts were not re-audited against snapshots.

## Summary

- Terminology consistency: **fail** (1 material, 3 minor)
- Callbacks to earlier chapters: **14 correct / 1 incorrect / 1 partial**
- Retrieval-practice accuracy: **pass** (10 / 10 tags aligned)
- Glossary coverage: **~45 concepts introduced, 43 defined in the chapter, 4 require glossary entries** (1 of them used in graded text with no definition anywhere in the book)
- Contradictions with earlier canon: **2 flagged**
- Ethical guardrails (skill Part 14): **pass**

Cross-bearings: **52 outbound pointers, all resolve.** 51 carry `Ch N §M` and every one names a section the skeleton grants that chapter, with the topic the skeleton assigns it; the 52nd addresses Chapter 1 by heading name, which is the correct form given Ch 1 has no `§N` anchors (B6 Collision #1). Reciprocally, **37 inbound pointers from 14 chapters all land** — see "Inbound delivery" below.

---

## Terminology consistency

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| The absent-component pattern | **"An object without its component does nothing."** — Chapter 3's phrase; named as a pattern at Ch 10 §3 | 1 quoted (L1005), 2 paraphrased (L1098 region, Exam Alert trap row) | **YES — material. See F1.** |
| operator | the operator *pattern* only; never a human (write "cluster administrator") | 2 — L554 (pattern), L126 (human) | **YES — minor. See F2.** |
| KEDA | register: "Kubernetes Event-Driven Autoscaling" | 1 expansion: "Kubernetes Event Driven Autoscaler" | **YES — minor. See F3.** |
| CKAD, CKS | register requires expansion at first use in the book | 3 bare uses; never expanded here or in Ch 1–16 | **YES — minor. See F4.** |
| ambient mode / ambient mesh | ledger headword is "Ambient mesh"; Istio's own term is "ambient mode" | 11, all "ambient mode" | Ledger-side, not draft-side. See F5. |
| cloud native | unhyphenated, always | 9 hyphenated hits — **all inside the snapshot filename `cncf-cloud-native-definition-2026-08-23` or the figure anchor `ch17-fig01-…`** | **No.** Ch 17 does not inherit the ⚑8 debt that Ch 1–8 carry. |
| Knative Service | full two words, never bare | all uses full; a ⚓ Worth Securing enforces it explicitly | No |
| control plane (mesh vs cluster) | sense B always marked as the mesh's, with an explicit disclaimer | ★ Fixed Point states "Neither of them is the cluster's control plane from Chapter 3" | No |
| Sandbox (level) vs sandboxed runtime | level capitalised, always beside a sibling level; runtime adjectival only | conforms | No |
| immutable infrastructure | always the full two-word phrase; distinct from image immutability | conforms; a 🪝 Snag draws the distinction | No |
| plugin | never bare, always qualified by its interface | 11, all qualified | No |
| the four pluggable interfaces | the book's phrase; not "the four extension points" | conforms — and §4 reconciles Ch 2's "API extensions" wording explicitly, per the B6 drafting note | No |
| Kubernetes / kubectl / etcd / containerd / CRI-O | spelled/cased per ledger | conforms; no `K8s` | No |
| Taking Your Bearings | never "Bearings" alone in reader-facing text | conforms | No |

Also checked and clear: the chapter asserts **no running ordinals**. "Four times" everywhere refers to the closed set of four pluggable interfaces the reader can see in the figure, which the ledger's 2026-08-30 convention explicitly sanctions. No control-loop count is asserted, so Ch 15 §7's designated primary Zenith is not spent early.

### F1 — The named pattern is quoted with the wrong sentence and the wrong coiner *(material)*

Draft line 1005:

> Chapter 10 §3 christened it: **the object exists; nothing happens without the component.**

Both halves are wrong against shipped text.

**The wording.** The book's canonical sentence is **"An object without its component does nothing."** It appears ~15 times across three chapters: as a ★ Fixed Point and a ⚓ Worth Securing in Ch 10 §3, inside `ch10-fig…`, in a Ch 10 `[retrieval: ch3]` question *and its answer key*, in the Ch 10 Chapter Summary, in three places in Ch 11 including a graded Practice option ("The absent-component pattern — *an object without its component does nothing*"), and in the Ch 3 Chapter Summary under the headword **"Absent-component pattern."** A reader who memorised the Fixed Point will not recognise the sentence Ch 17 hands back.

**The attribution.** Ch 10 §3 line 626 says: *"Chapter 3 gave you a sentence and asked you to keep it: **An object without its component does nothing.**"* Ch 11 line 811 says: *"The phrase is Chapter 3's, and Chapter 10 §3 named it as a pattern."* So "Chapter 10 §3 christened it" contradicts two shipped chapters.

**Why this one matters more than its size.** Ch 10 line 341 promises the reader outright: *"You'll use it in Chapter 13, in Chapter 17, and on things this book never gets to."* Ch 13 uses neither the sentence nor the alternate name anywhere (verified: zero hits in Ch 12–16). Chapter 17 §7 is therefore the **only** place the promised retrieval can still land, and it currently lands in unrecognisable words.

**Origin, in fairness to the draft:** the B7 ledger's own row reads *"The object exists; nothing happens without the component" (the named pattern) | Ch 10 §3* — wrong wording, wrong coiner. The draft followed a binding contract faithfully. The ledger row is the defect's source and should be corrected alongside the chapter.

**Fix (L1005):**

> You have met this shape before, and you have met it under a name. Chapter 3 gave you the sentence and Chapter 10 §3 named it as a pattern: **an object without its component does nothing.**

The three sentences that follow it need no change — they are three good instances. The paraphrases at L1098 ("the object can exist while nothing acts on it") and in the Exam Alert trap row are fine *once* the canonical sentence has been stated at L1005.

### F2 — "operator" used in the human sense *(minor)*

L126: "you have been a competent **operator** of somebody else's software" — in a chapter that also prints "the operator pattern" at L554. The ledger forbids the human sense precisely because of this collision. One-word fix: *"a competent user of somebody else's software"*, or recast to "you have been running somebody else's software competently."

### F3 — KEDA expansion disagrees with the register *(minor)*

Draft: "the Kubernetes Event Driven Autoscaler." Register: "Kubernetes Event-Driven Autoscaling." Align the draft to the register, or amend the register — author's call, but the book should not carry two expansions.

### F4 — CKAD and CKS are never expanded anywhere in the book *(minor, but Ch 17 owns it)*

CKA *is* expanded, once, at Ch 1 line 180 ("the Certified Kubernetes Administrator"). CKAD and CKS are expanded nowhere in Chapters 1–17. Ch 17 §8 is the acronym register's owning section for all three. Add the expansions at their first appearance in §8's certification-ladder paragraph.

Related, and already flagged by the draft's own AUTHOR-REVIEW: KCSA's expansion is unsourced. Separately, **SIG is first used in the book at Ch 8 line 861 ("a SIG Release team") unexpanded** — a pre-existing Ch 8 debt, not this chapter's defect. Ch 17 correctly expands SIG at its own first use (Soundings answer 7).

### F5 — Ledger-side, no draft change wanted

The ledger headword is "Ambient mesh (sidecar-less)"; the draft says "ambient mode" throughout, which is Istio's own documented term and is what the sources say. **Recommend correcting the ledger to "ambient mode"** rather than touching the chapter.

---

## Callback correctness

Verified against shipped text. Line numbers are the target chapter's.

| # | Ch 17 claim | Verdict |
|---|---|---|
| 1 | Ch 1 quoted: *"Chapter 17's community and collaboration material is, in my experience, what technically strong candidates skip most often. It looks like soft content next to the technical chapters."* | **✓ verbatim** (ch01:466) |
| 2 | Ch 1 said "cloud native" does not mean "runs in a public cloud" and deferred the definition here | ✓ (ch01:559, 374, 535) |
| 3 | Ch 1 introduced the CNCF as credential issuer / blueprint publisher | ✓ |
| 4 | Ch 2 §8 promised "recognition rather than a fourth list" | **✓ verbatim** (ch02:914) |
| 5 | Ch 2 §8 named this the *first* of four; §4 must reconcile Ch 2's "API extensions" against "CRDs" | ✓ — ch02:914 confirms the plant; §4's "A note on the fourth interface's two names" discharges the B6 drafting note |
| 6 | "Chapters 3 and 10 both told you the VPA is not shipped by default and pointed here" | ✓ (ch03:606, ch10:678, ch10:1811) |
| 7 | Ch 3 §7's forward promise — the control loop "turns out to be one of the things 'cloud native' means" (ch03:972, 980) | ✓ delivered at L382 and in §1's practices clause |
| 8 | Ch 5 promised the sidecar would return in Ch 17 | ✓ (ch05:386, "see Ch 17 — the mesh data plane") |
| 9 | Ch 6 gave the HPA in one sentence and deferred the landscape here | ✓ (ch06:426) |
| 10 | Ch 7 quoted: *"a standing, machine-readable statement that the cluster is short of somewhere to put work. Something could be watching for exactly that."* | **✓ verbatim** (ch07:428) |
| 11 | Ch 8 §6 "warned you that the version-skew numbers were the most forgettable material in the book" | ✓ near-verbatim — Ch 8 says *"among the most forgettable material in this book"* (ch08:1009). Optional: restore "among the most". |
| 12 | Ch 10 §7 — NetworkPolicy cannot encrypt; TLS terminates at the Ingress | ✓ |
| 13 | Ch 13 named metrics-server as what an HPA reads | ✓ (ch13:1318, same source line) |
| 14 | Ch 14 §6 — charts have a `crds/` directory because definitions must precede the objects that use them | ✓ **and consistent with Ch 14 canon** (ch14:987 *"the declaration must be registered before any resources of that CRDs kind(s) can be used"*; ch14:989 "no ordering guarantee, and one case where the absence of a guarantee is fatal") |
| 15 | Ch 10 §3 "christened it: the object exists; nothing happens without the component" | **✗ incorrect — F1** |
| 16 | Ch 15 §6 is "where you last met a Graduated project being named as such" | **~ partial — F6** |

### F6 — "a Graduated project being named as such" overstates Ch 15 *(minor)*

Ch 15 §6 (line 1193) says *"Two graduated projects, four shared principles, opposite defaults"* — lowercase, adjectival, and it never states a CNCF maturity level as such. The reader did meet the word; they did not meet the level being assigned. Either soften Ch 17 ("where you last saw two projects called graduated") or capitalise in Ch 15 §6. Low priority, but note the second-order effect: once §2 teaches **Graduated** as a level with a capital G, Ch 15's lowercase use becomes a drift candidate for the final sweep.

### Inbound delivery — reciprocal check

All 37 inbound `see Ch 17` pointers from Chapters 1–16 land on a section that delivers what they promise. The one known exception is a shipped-text defect, not a Ch 17 defect, and the draft has substantially neutralised it:

- **ch03:350 → `Ch 17 §1 — the CNCF, its governance, and the cloud native definition`.** Governance is §2, so this pointer lands one section early (B6 Collision #2 — two other pointers put governance at §2 and outvote it). **As drafted this is now survivable:** §1's closing subsection "The institution behind the document" covers the CNCF as an institution and hands off explicitly — *"§2 is about the structure that makes it true."* The recommended retarget to `§1–§2` is therefore optional rather than required.

---

## Retrieval-practice accuracy

10 tags, all aligned. Distribution is 4/16 checkpoint questions (25%) and 6/21 practice questions (29%), against the skill's 20–25% target for chapters 6+ — at or slightly above target, which is the right side to be on.

| Location | Tag | Topic | Owner per skeleton/ledger | Verdict |
|---|---|---|---|---|
| L437 | `ch2` | image immutability vs immutable infrastructure | Ch 2 §2 | ✓ |
| L770 | `ch2, ch6, ch9, ch11` | the four interfaces | Ch 2 §4 / 6 §8 / 9 §1 / 11 §5 | ✓ all four |
| L786 | `ch10` | NetworkPolicy does not encrypt | Ch 10 §6–§7 | ✓ |
| L1314 | `ch8` | release cadence & support window | Ch 8 §6 | ✓ |
| L1546 | `ch6` | CRD vs aggregation layer | Ch 6 §8 | ✓ |
| L1553 | `ch14` | Helm `crds/` ordering | Ch 14 §6 | ✓ — verified against shipped Ch 14 |
| L1567 | `ch10` | TLS termination + mTLS gap | Ch 10 §2, §6–§7 | ✓ |
| L1595 | `ch13` | metrics-server / `kubectl top` | Ch 13 §7 | ✓ |
| L1602 | `ch7` | `Pending`, unschedulable, preemption | Ch 7 §2 | ✓ (preemption is in Ch 7's own answer key, so it is fair game) |
| L1616 | `ch8` | cadence + SIG Release | Ch 8 §6 | ✓ |

---

## Glossary coverage

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| **CloudEvents** | **no** — named twice, never defined | **YES — and it is in graded text. See F7.** |
| ztunnel | yes (sourced) | yes — appears in two graded items; give the mock exam a lookup path |
| waypoint proxy | yes (sourced) | yes — same reason |
| FaaS | **not used at all** | See F8 |
| cloud native (v1.1), five characteristics | yes, verbatim | yes (headword) |
| Sandbox / Incubating / Graduated / Archived | yes | yes |
| Governing Board, TOC, TAG, End User TAB, CNCF Landscape | yes | yes |
| microservices, monolith, loose coupling, immutable infrastructure | yes | yes |
| extension point, API aggregation layer, `APIService`, device plugin | yes | yes |
| service mesh, data plane, mesh control plane, Envoy, sidecar proxy | yes | yes |
| mTLS, zero trust, permissive mode, secure overlay | yes | mTLS, zero trust yes; the other two no |
| serverless, Knative, Serving, Eventing, Functions, scale to zero, KPA | yes | yes |
| HPA, VPA, Cluster Autoscaler, Karpenter, KEDA, in-place vertical resize | yes | yes |
| SIG, Working Group, Committee, Steering, subproject, KEP, SIG Release | yes | yes |
| contributor ladder (Member/Reviewer/Approver/Subproject Owner) | yes | yes |
| Code of Conduct, KubeCon, CNCG, CNCF Ambassadors, LFX/GSoC/Outreachy | yes (sourced) | Code of Conduct and KubeCon yes; the rest no |
| KCNA / KCSA / CKA / CKAD / CKS | named; KCSA expanded, CKAD/CKS not | yes — with expansions (F4) |
| node group, consolidation, Cluster Proportional Autoscaler | named, non-graded | no |
| metrics-server, Metrics API | referred with pointer to Ch 13 §7, not redefined | owned by Ch 13 §7 — no new entry |

### F7 — CloudEvents reaches graded text undefined *(medium)*

"CloudEvents" appears nowhere in Chapters 1–16 and is never defined here. The reader gets only Knative's phrasing — *"a CloudEvents-over-HTTP asynchronous routing layer"* — which tells them Eventing routes events over CloudEvents without telling them what CloudEvents is. It then carries **Practice Q14's correct answer** and its explanation.

This is the eBPF precedent from the Ch 9 gate with the polarity reversed: there the ledger had ruled the term out of graded text and the distractor was rebuilt. Here the term sits in a *correct* answer. Two clean options, author's call:

1. One clause in §6 — "CloudEvents, a vendor-neutral specification for describing event data" — plus a glossary entry and an acronym-register row. Cheapest, and the term is genuinely ecosystem vocabulary.
2. Leave the prose and drop "CloudEvents-over-HTTP" from Q14's option C, since the discriminating content of that item is sync-vs-async, not the wire format.

I'd take option 1: the phrase is quoted from the Knative source, so removing it from the option while keeping it in the body would make the two disagree.

### F8 — FaaS is assigned to §6 but never used

The ledger gives "FaaS (Functions as a Service)" to Ch 17 §6 and the acronym register carries a row for it. The draft never uses the term, which leaves an orphaned register row. Either add one clause in §6 (Knative Functions is the natural hook) or retire the row. No graded material depends on it either way.

---

## Contradictions with earlier canon

**C1 — the named pattern's wording and coiner.** Detailed at F1. Counted here because Ch 11 puts the canonical sentence in a graded Practice option, so the two chapters would be teaching the reader two different sentences for the same ★-marked rule.

**C2 — the release cadence, and an open promise Ch 17 declines to close.**

Shipped Ch 8 §6 states, sourced: *"Since 2021 the project ships **three minor releases per year**, approximately every fifteen weeks"* (ch08:861, from `k8s-releases-cadence-2026-08-23`). It then commits to this chapter **twice**:

- ch08:865 — "You will meet the cadence again there… Make the connection now."
- ch08:1009 — "where SIG Release and the KEP process explain **where those fifteen weeks go**."

Ch 17 §8 teaches "approximately three times per year" from the newer snapshot and, per its own AUTHOR-REVIEW, deliberately declines the 15-week figure. The number "fifteen" appears nowhere in the chapter. So a reader arrives holding a specific promise about a specific number and is never handed it — even though §8's phase walk-through (Enhancements Freeze ~week 4, Code Freeze from ~week 12 for ~2 weeks, post-release from week 14) is *exactly* the accounting Ch 8 promised.

The draft's AUTHOR-REVIEW flagged the snapshot conflict but could not have known Ch 8 shipped the figure twice with a forward promise attached. **Recommended fix — one clause in §8 after the phase list**, which closes the loop without asserting the disputed cadence phrasing:

> That is where the fifteen weeks Chapter 8 gave you actually go.

Both halves stay true: the cadence is ~3/year per the current page, and the cycle Ch 8 measured at ~15 weeks is the one just described. If the author would rather not reconcile, the alternative is a one-line retrofit to Ch 8 §6 dropping "those fifteen weeks" from ch08:1009 — more expensive, since it edits shipped text.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Every figure carries a snapshot tag. The chapter goes further than required: an AUTHOR-REVIEW removed a comparative weights claim ("Container Orchestration rose to 28%, Application Delivery doubled to 16%") on discovering its only support was a syndicated community post whose own header forbids citation. That is the guardrail working as designed.
- [x] **Fear-based content uses real examples.** None present. "Trust is a vulnerability" is quoted from the CNCF glossary with the lateral-movement mechanism explained, not gestured at.
- [x] **Simplification acknowledged.** Repeatedly and unusually well: §4 flags its own four-interface grouping as *"this book's, and honesty requires saying so"* and prints the documentation's six-point list beside it; the in-place-resize material is written **to** a three-way source conflict rather than through it; §2 tells the reader to learn the levels and not the roster, and says why; §3 quotes the CNCF arguing *against* microservices.
- [x] **Authority claims cite legitimate sources.** Governance and definition claims are anchored to the charter, the TOC repo, and the projects page — and §2 correctly separates what the projects page asserts from where the criteria actually live.
- [x] **"Frequently tested" claims are verifiable.** The chapter does not claim frequency. The two `[inferred]` trap rows are marked *"(Easy to confuse …)"* per the B1/B7 convention, never "frequently tested." The one experiential claim — that strong candidates skip this material — is attributed to Ch 1's hedged "in my experience."
- [x] **No strawmanning of alternative study methods.** Older prep is criticised only on a dated, sourced curriculum change, and sympathetically: *"you may well arrive holding it."*
- [x] **Subject dignity (v5.7).** Wry beats stay aimed at practitioners. No third-party harm is used for humour.

---

## Recommended fixes

The revision stage's diagnostics were addressed; everything below is new at this gate. Ranked.

**1. Fix the named-pattern sentence and attribution at L1005 (F1/C1).** Ship-blocking in the sense that matters — it is the single most reinforced retrieval phrase in the book, it was explicitly promised to land here, and Ch 13 already missed it. Text supplied above. **Correct the B7 ledger row at the same time** (wrong wording *and* wrong coiner), or the next stage will re-introduce the error.

**2. Close the fifteen-weeks loop in §8 (C2).** One clause. Cheaper than editing shipped Ch 8.

**3. Resolve CloudEvents (F7).** Prefer the one-clause definition + glossary entry + register row.

**4. Tag the Helm `crds/` claim.** The draft's own AUTHOR-REVIEW asks whether a Helm snapshot exists to tag against and proposes reusing Ch 14's as the cheap option. **It exists: `helm-crd-best-practices-2026-08-31`**, and shipped Ch 14 §6 uses it for this exact claim (ch14:987, 991). The ordering claim in §4 and in Practice Q10 is consistent with Ch 14's canon. Apply the tag; no research gap needs opening.

**5. Expand CKAD and CKS at first use in §8 (F4).**

**6. Minor sweep:** "operator" → "user" at L126 (F2); reconcile the KEDA expansion (F3); optionally restore "among the most forgettable" at L1210.

**7. Ledger/skeleton corrections to record, no chapter edit:**
   - The absent-component pattern row: canonical sentence is *"An object without its component does nothing"*; the phrase is Chapter 3's, named as a pattern at Ch 10 §3. The row also claims retrieval "by name at Ch 13 §7" — Ch 13 does not use it at all.
   - `VPA | First appears Ch 17 §7 †` is wrong. VPA first appears in shipped Ch 3 (line 606) and Ch 10 (lines 678, 1811).
   - Headword "Ambient mesh" → "ambient mode" (F5).
   - FaaS register row is currently orphaned (F8).

**8. Author decisions the draft raised and this gate does not overrule:** the omission of cost management/FinOps from §2; the figure-anchor numbering (contiguous fig01–fig07 but out of reading order — renumber anchors *and* `image-specs.md` in one commit, or suppress printed figure numbers for this chapter); and the `ch17-zenith-…` anchor form, which is **valid** — `structural-contract.yaml`'s `anchor_id_pattern` sanctions the `zenith` segment explicitly, so no change is needed there.

**Conventions honoured, checked and clear:** heading form `## <difficulty> §N — Title` (B6 recommendation #3); `☀️` on the closing synthesis section (recommendation #4); no invented section numbers for undrafted chapters; Ch 1 addressed by heading name only; the two-competency structure with §2 and §8 as D4.3's own numbered sections.

---

**Two things worth your attention before the knowledge-base stage runs:**

The chapter is in good shape structurally — all 52 outbound cross-bearings resolve, all 37 inbound pointers land, retrieval tags are 10/10, and the ethical checklist passes cleanly. The material finding is **F1**: §7 hands back the book's most-reinforced retrieval phrase in words the reader has never seen, and credits the wrong chapter with coining it. Chapter 10 promised this retrieval would land in Ch 13 and Ch 17; Ch 13 missed it entirely, so this is the last chance. The B7 ledger caused it, so fix both or it comes back.

**C2** is the one I'd have missed without the shipped text: Chapter 8 says "fifteen weeks" twice and promises Chapter 17 will explain where they go. Ch 17's own AUTHOR-REVIEW consciously declined that number without knowing about the promise — and §8 already contains the accounting, so it's a one-clause fix.

I couldn't write the file (permission denied). Save the document above to `../Book-KCNA/.pipeline-state/ch-17/integration.md`, or grant Write and I'll place it.
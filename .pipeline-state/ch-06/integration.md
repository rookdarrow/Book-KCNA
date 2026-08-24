Verification complete. `Write` is blocked in this session (same permission gap the question-quality stage hit), so I'm emitting the artifact here for capture rather than retrying the write to `.pipeline-state/ch-06/integration.md`.

---

```markdown
# Integration Check — KCNA Chapter 6

<!-- The knowledge-base shards supplied to this stage were empty ("[no matching
     knowledge-base shards found]"). Rather than declare the chapter unverifiable,
     this check was run against the published chapter files on disk in
     C:\dev\lodestar\Book-KCNA\ — chapters 01, 02, 03, 04, 05 and 07 are all
     committed, so every backward callback AND the Chapter 7 forward pointers are
     directly verifiable. Book-level scaffolding (.pipeline-state/book-outline/)
     was also read. Every finding below cites a file and line. -->

## Summary

- Terminology consistency: **fail** — 3 flagged, all heading/marker form. Domain terminology itself is clean.
- Callbacks to earlier chapters: **17 verified / 1 incorrect / 1 imprecise** (outbound). Inbound: 8 §-numbered pointers into Ch 6, **6 correct / 2 broken**.
- Retrieval-practice accuracy: **pass** — 9 tagged items, all topics confirmed present in the named chapter. Spacing 20.6%, inside the 20–25% band.
- Glossary coverage: **38 concepts introduced, 30 defined in the chapter, 8 require glossary entries.**
- Contradictions with earlier canon: **3 flagged.**
- Ethical guardrails (skill Part 14): **pass**, with 1 claim to verify and 1 disclosure to tighten.

**Gate recommendation: HOLD for four one-token edits, then pass.** The chapter itself is in strong shape — the reasoning, sourcing and answer-key discipline are the best in Part II. Everything below is bookkeeping at the seams between chapters, which is exactly what this stage exists to find. Nothing requires re-drafting prose.

---

## Terminology consistency

Domain terminology is clean. Every Kubernetes noun Ch 6 shares with an earlier chapter is spelled identically, capitalized identically, and used in the same sense. Spot-checked against the chapter that introduced each.

| Term | Canonical form | Occurrences in this chapter¹ | Drift? |
|---|---|---|---|
| Pod | `Pod` (Ch 5) | 134 | No. Lowercase `pod` appears only inside `kubectl` output, `kubectl delete pod`, and one direct quotation of upstream docs — all correct. |
| Deployment | `Deployment` (introduced here; forward-named Ch 4:415) | 106 | No |
| ReplicaSet | `ReplicaSet` (forward-named Ch 4:415, 834) | 83 | No |
| DaemonSet | `DaemonSet` | 29 | No |
| StatefulSet | `StatefulSet` (forward-named Ch 1:436) | 27 | No |
| custom resource | `custom resource` lowercase; `CustomResourceDefinition` / `CRD` for the object | 20 | No — the noun/object distinction is held consistently, and it is load-bearing for §8's Fixed Point |
| control loop | `control loop` (Ch 3 §6) | 18 | No. Never "reconciliation loop." |
| control plane | `control plane` (noun) / `control-plane` (attributive) | 12 | No — matches Ch 3's own hyphenation rule |
| desired state / current state | Ch 3 §6 | throughout | No |
| workload resource | `workload resource` (Ch 5:501) | throughout | No |
| owner reference | `owner reference` | throughout | No |
| horizontal pod autoscaling | lowercase for the feature, `HorizontalPodAutoscaler` for the object | — | No — mirrors upstream usage |
| **Headless Service** | `headless Service` (Ch 9 lineup entry) | 2 | **Yes — minor.** Ch 6:870 uses `Headless Service` and `headless Service` in the *same sentence*. Pick one before Ch 9 sets the canonical form. |

¹ Matching-line counts from ripgrep, not per-token counts.

### Heading-form drift — the three actual failures

These are not domain terms, but they are branded-section names, and Ch 6 is the outlier in each case. None were caught by the structural linter (which passed 30/30 checks on everything but the figure anchor), because the structural contract does not encode heading form.

| Item | Ch 6 | Rest of book | Skill Part 15 |
|---|---|---|---|
| Exam Alert heading | `## Exam Alert` (line 1153) | `## Exam Alert! 🚨` (Ch 3:962, Ch 4:998, Ch 5:1101, Ch 7:1044); `## Exam Alert 🚨` (Ch 2:918) | `## Exam Alert! 🚨` |
| Checkpoint headings | `## ☆ Taking Your Bearings #1` / `#2` / `#3` — **no topic** (490, 735, 1041) | Every other chapter carries a topic: `#1: What a Pod Is` (Ch 5), `#1 — How the Decision Is Made` (Ch 7) | `## ☆ Taking Your Bearings: [Topic]` |
| Section-heading order | `## ⚪ §1 —` (difficulty first) | Ch 5, Ch 7 match Ch 6. **Ch 2, 3, 4 use `## §1 — ⚪`** (§ first) | not specified |

The first two are Ch 6 defects and should be fixed here. **The third is a book-level split (3 chapters each way), not a Ch 6 defect** — Ch 6 matches its immediate neighbours, which is the right side to be on. Flagging it for a one-pass sweep, not for this chapter.

Ch 6 uses `⚠ Navigational Hazards`, `☀️ Zenith`, and `🗺️ Chart → 🌊 Passage → 🌅 Dawn` correctly — no v5.5/v5.6 legacy markers (`Shoals Ahead`, `Landfall`, `⚓→★→🏆`) anywhere in the chapter.

---

## Callback correctness

### Outbound — Ch 6 pointing at other chapters

**Verified correct (15):**

| Ch 6 claim | Target | Verified against |
|---|---|---|
| "Chapter 5 ended on a question it refused to answer… who does the replacing?" | — | Ch 5:1460, **verbatim**: *"If Pods are designed to be replaced, who does the replacing?"* |
| `see Ch 5 §4 — a Pod is replaced, never rescheduled` | Ch 5 §4 | Ch 5:525 — *"§4 — Scheduled Once, Replaced Never"* ✓ |
| `see Ch 5 §5 — the five Pod phases` | Ch 5 §5 | Ch 5:563 — *"Pod Phases and Container States"* ✓ |
| `see Ch 5 §7 — liveness, readiness, and startup probes` | Ch 5 §7 | Ch 5:785 — *"Three Probes, Three Jobs"* ✓ |
| "Chapter 5 told you a Pod that never reports ready never receives traffic" | — | Ch 5:858, **verbatim** — and Ch 5 forward-bears to Ch 6 §4 for exactly this ✓ |
| "Chapter 5 taught you five Pod phases" | — | Ch 5:575 defines `Succeeded` in the same words Ch 6 uses ✓ |
| `see Ch 4 §2 — apiVersion, kind, metadata, spec` | Ch 4 §2 | Ch 4:334 — *"The Anatomy of a Record"* ✓ |
| `see Ch 4 §5 — labels and selectors, the universal join` | Ch 4 §5 | Ch 4:776 — *"The Universal Join"* ✓ |
| "Chapter 4… listed the places they get used" | — | Ch 4:834 lists **exactly four** (ReplicaSet, Service, node scheduling, NetworkPolicy). Ch 6 §3 correctly claims to be "the first one collected" ✓ |
| "Chapter 3 promised you a control loop you could watch working in real time" | — | Ch 3:950, **verbatim**: *"where a ReplicaSet lets you watch it work in real time"* ✓ |
| "Chapter 3 closed by promising you controllers you configure yourself" | — | Ch 3:956, **verbatim** cross-bearing: *"see Ch 6 — controllers you configure yourself"* ✓ |
| "Chapter 2 named custom resources as the fourth socket" | — | Ch 2:600 carries the four-interface framing and points at Ch 6 for CRDs ✓ |
| `see Ch 7 §1 — …sometimes it can't be` | Ch 7 §1 | Ch 7:289–299 — *"One Decision, Made Once"*, incl. *"If the list is empty, that Pod isn't yet schedulable"* ✓ |
| The Voyage Ahead's DaemonSet question | Ch 7 | Ch 7:696 answers it exactly ✓ |
| `see Ch 6 §1 — the ownership chain` (intra-chapter, §4→§1) | self | Legal, but note `reconcile.py` flags same-chapter cross-bearings as self-references (it flagged 3 in Proxmox ch2). Expect one hit. |

**Incorrect (1) — fix required:**

> **Ch 6 §7 closes with `*[cross-bearing: see Ch 7 §5 — a DaemonSet's Pods still go through scheduling, and taints are how a node opts out]*`. It should be §4.**
>
> Ch 7 §5 is *"Placing Pods Relative to Each Other"* (pod affinity/anti-affinity, Ch 7:784). Taints and tolerations are Ch 7 §4, *"When the Berth Refuses You"* (Ch 7:580–720) — and the DaemonSet toleration material Ch 6 is pointing at sits at **Ch 7:696, inside §4**. This is a broken pointer into a *published* chapter, so it is verifiable now and will mis-route a reader on day one.
>
> **Fix: `§5` → `§4`.** One token, in this chapter.

**Imprecise (1) — author's call:**

> `*[cross-bearing: see Ch 3 §6 — the control loop, and why nobody is in charge]*`. The target §6 is correct for the control loop (Ch 3:750). But *"why nobody is in charge"* is Ch 3 **§7** (Ch 3:908, *"Nobody Is in Charge"*). The pointer sends a reader to §6 for something that pays off one section later. Either trim the tail to *"the control loop"* or make it `§6–§7`.

### Inbound — other chapters pointing at Ch 6

Eight §-numbered pointers resolve into this chapter. **Six are correct** (Ch 5:551 §1 ✓, Ch 5:858 §4 ✓, Ch 5:1464 §1 ✓, Ch 7:696 §7 ✓, Ch 7:792 §1 ✓). Chapter 4's three pointers (353, 415, 834) carry **no section number at all** and resolve trivially ✓.

**Two are broken — already flagged in the draft's AUTHOR-REVIEW comments, verified on disk, still open:**

| File | Line | Says | Should be |
|---|---|---|---|
| `chapter-01-taking-departure.md` | 436 | `see Ch 6 §3 — StatefulSets and stable identity` | **§6** |
| `chapter-02-cargo-in-standard-crates.md` | 600 | `see Ch 6 §3 — CRDs and extending the API` | **§8** |

Both need a one-token edit in shipped text; neither is fixable from inside Ch 6. The recommended edits in the draft's AUTHOR-REVIEW comments are correct.

> **⚠ But the stated *reason* is now stale, and this matters.** The ch-06 frontmatter (lines 18–30) and outline (§3, line 407) both assert that "**§3 is pinned by `chapter-04` line 688**" and therefore cannot move. **Chapter 4 was re-drafted in the most recent commit (`73fd066`) and dropped every section number from its Ch 6 pointers.** There is no longer any pin on §3 from Chapter 4. The recommended fix doesn't change — §6 and §8 are where that material genuinely lives — but the constraint is weaker than the outline records, and the outline's numbering warning should be corrected so a future session doesn't reason from it.

**One inbound *characterization* is wrong (Ch 7's defect, not Ch 6's):**

> `chapter-07-assigning-the-berth.md:696` opens: *"Chapter 6 told you that DaemonSets keep running on nodes where nothing else will, and said you'd already met the mechanism in disguise."*
>
> Chapter 6 says neither of those things. The phrases *"nothing else will"* and *"in disguise"* appear nowhere in chapter-06. What Ch 6 actually does is raise the question, unanswered, in The Voyage Ahead: *"a DaemonSet is supposed to run on every node, so what happens when a node has been marked as one that workloads should stay off?"*
>
> Ch 7 was drafted against the truncated Ch 6 that was later withdrawn (`2bb971b`), which is how this happened. **Fix in Ch 7:** replace the opening clause with a hand-back to the question — e.g. *"Chapter 6 left you with a question: a DaemonSet is supposed to run on every node, so what happens when a node is marked as one that workloads should stay off? Here is the answer."*

> ✅ **This closes an open item in Chapter 7.** The AUTHOR-REVIEW at `chapter-07:1293` asks for both Ch 6 back-bearings to be re-verified once the ch-06 harvest was re-run. Done: **§1 and §7 are both correct** against final numbering. Only the line-696 characterization needs the edit; the pointers stand.

---

## Retrieval-practice accuracy

**Pass.** Nine tagged items; every one's topic confirmed present in the chapter named.

| Item | Tag | Topic | Verified in |
|---|---|---|---|
| Soundings 7 | ch3 | control loop: two states + action | Ch 3 §6 (750) ✓ |
| Soundings 8 | ch5 | Pod replaced, not rescheduled | Ch 5 §4 (525) ✓ |
| Bearings #1 · 4 | ch3 | desired/current state, the action | Ch 3 §6 ✓ |
| Bearings #1 · 5 | ch4 | two selectors over one Pod | Ch 4 §5 (776) ✓ — see note |
| Bearings #2 · 4 | ch5 | readiness probes | Ch 5 §7 (785) ✓ |
| Q2 | ch4 | `spec` vs `status` | Ch 4 §2 ✓ — and Ch 4:419 explicitly says *"Chapter 6 reads it against a replica count"* |
| Q5 | ch5 | replacement gets a new UID | Ch 5 §4 ✓ |
| Q16 | ch5 | five Pod phases, `Succeeded` | Ch 5:575 ✓ (Ch 5 also tests it at 1313/1317) |
| Q19 | ch3 | controllers, read spec → act → write status | Ch 3 §6 ✓ |

Spacing computes to **20.6%** across Bearings + Practice (7 of 34), inside the 20–25% band the retrieval architecture sets for Ch 6. This matches the question-quality stage's independent figure exactly.

**One note, low severity.** Bearings #1 item 5 is tagged `ch4`, and its stem *is* Ch 4 §5 material. But the load-bearing content of its answer key — *"ownership is exclusive; selection is not"* — is **Ch 6 §3's own teaching**, not Ch 4's. It works as written; it is just doing less retrieval work than the tag implies.

**One dropped retrieval opportunity.** The outline (line 420) specified that §3 should *refer to `ch04-fig03-labels-selectors-join` by name* rather than redraw the join — *"which is also a spacing-effect retrieval at zero cost."* The figure exists (`chapter-04:806`). **Chapter 6 never mentions it.** Recovering it costs one clause in §3 and buys a free retrieval event.

---

## Glossary coverage

**38 concepts introduced · 30 defined in-chapter · 8 require glossary entries.**

Defined in-chapter, no entry required (30): workload resource · ReplicaSet · Deployment · Pod template · ReplicationController · owner reference · cascading deletion · orphan · adoption · rolling update · `maxSurge` · `maxUnavailable` · `Recreate` · `minReadySeconds` · `progressDeadlineSeconds` · revision · `revisionHistoryLimit` · rollback (Deployment sense) · StatefulSet · ordinal identity · DaemonSet · Job · CronJob · HorizontalPodAutoscaler · horizontal scaling · custom resource · CustomResourceDefinition/CRD · custom controller · operator pattern · dynamic registration.

Used without definition — these need stage-14 entries:

| Concept, introduced here | Defined in-chapter? | Needs glossary entry? | Note |
|---|---|---|---|
| **EndpointSlice** | no | **yes — priority** | Used twice in Bearings #1 answer 5, never defined, **no cross-bearing**. A reader meets a new object type inside an answer explanation with nowhere to go. Cheapest fix: add `*[cross-bearing: see Ch 9 — EndpointSlice]*`. |
| **RBAC** | no | **yes — priority** | Ch 6:981 and Q18 option A. No cross-bearing to Ch 12, where it lives. |
| **nodeSelector / node affinity** | no | **yes — priority** | §7 DaemonSet prose and Q14 stem. Ch 7 material, no cross-bearing at point of use (the §7 closing pointer is about taints, not selectors). |
| headless Service | no | yes | Deferred deliberately, cross-beared to Ch 9 §5 ✓ |
| PersistentVolume | no | yes | Deferred deliberately, cross-beared to Ch 11 §4 ✓ |
| PersistentVolumeClaim | no | yes | Same |
| volume claim template | no | yes | §6, no definition and no pointer |
| API-server aggregation | partial | yes | Characterized ("more flexibility, more machinery") but not defined |

The three marked *priority* differ from the rest: the others are conscious deferrals with a pointer attached, which is good pedagogy. Those three are simply loose.

> Stage 14 note: a KCNA glossary will almost certainly want entries for the six workload resources regardless of in-chapter definition, since they're the book's most-looked-up nouns. Rule 4 doesn't *require* them; the book probably wants them.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Ch 6 makes almost no numeric claims. Every `maxSurge`/`maxUnavailable`/`revisionHistoryLimit` default carries a `[source:]` tag. The fact-accuracy stage owns the source audit; nothing here contradicts it. **One item to verify — see below.**
- [x] **Fear-based content uses real examples.** The overlapping-selector Logbook Entry (§3) is a composite scenario, but every *consequence* it asserts is sourced to upstream docs, and it's framed hypothetically rather than as a war story presented as fact. The stalled-rollout Snag (*"Nothing will page you unless you asked something to"*) is accurate operational reality, not manufactured dread. Clean.
- [x] **Simplification acknowledged.** Strong pass, and better than the checklist requires. §1 runs the full Order/Truth pattern explicitly — *"The simple version… The full picture is that the number is written twice."* §4 carries a proper `Dead Reckoning` block. §6's *"A loop left open on purpose"* tells the reader outright that the storage half is deferred **and that the deferral is deliberate rather than an omission**, which is precisely guardrail #5.
- [x] **Authority claims cite legitimate sources.** Uniform `[source: k8s-docs-*]` tagging.
- [~] **"Frequently tested" claims verifiable.** The Exam Alert is carefully framed — *"in descending order of how much of this chapter depends on them"* — which is a **dependency** claim, not an exam-frequency claim. That is the ethically correct construction and it should be preserved verbatim. **However**, see the flagged item below.
- [x] **No strawmanning of alternative study methods.** Ch 6 doesn't discuss study methods.

**One claim to verify before ship.** The chapter repeatedly makes unsourced claims about *reader populations*: "the most common wrong answer in this chapter" (Q1 key), "you are in the majority" (Bearings #2 · 2), "it is the one most people arrive with" (Bearings #3 · 1), "you are in good company" (Bearings #2 key). These are soft empirical assertions about candidate behaviour. B2 is explicit that inferred traps "must [be described] as 'easy to confuse,' never 'frequently tested'" (chapter-lineup:184), and that 14 of B1's 114 traps are `[inferred]` rather than `[source]`.

The disk-vs-StatefulSet misconception is **B1 trap #21**, which B2 cites by number (chapter-lineup:83). **Action: check whether trap #21 is labelled `[source]` or `[inferred]` in B1.** If `[source]`, "the one most people arrive with" stands. If `[inferred]`, soften to "easy to arrive with." Same test for the Q1 and Bearings #2 population claims. This is a five-minute check against B1, not a rewrite.

**One disclosure to tighten** — carried over into Contradictions below, since it's both.

---

## Contradictions with earlier canon

**1. The 6% is described as a share of *the book*; every other chapter calls it a share of *the exam*.** (Medium — semantic, and it touches the required disclosure.)

| Chapter | Metadata line |
|---|---|
| Ch 3:146 | `Domain Weight: ~6% of exam (authored estimate)` |
| Ch 4:162 | `Estimated chapter weight: ~6%` |
| Ch 5:190 | `Estimated share of the exam: ~7% (authored allocation — CNCF publishes domain weights, not competency weights [source]; see front matter)` |
| Ch 7:174 | `Authored weight: 5%` |
| **Ch 6:189** | **`Authored weight: ~6% of this book`** |

Ch 6 also says in Why This Chapter Matters: *"roughly six percent of the book's authored allocation."* B2's weight table sums to **100 across exam domains** (chapter-lineup:55), so the 6 is an authored estimate of **exam** share — the same quantity Ch 5 calls "~7% of the exam." Relabelling it "of this book" makes a different claim.

Either it's an error, or it's an intentional hedge to avoid implying a CNCF figure. If the latter, it's a good instinct pointed at the wrong words — **Ch 5:190 is the model to copy**, because it keeps "of the exam" *and* discloses the authored basis inline with a source tag. That form satisfies B2's mandatory disclosure #1 (chapter-lineup:143); Ch 6's current form only gestures at it with the word "Authored."

> Note for the AUTHOR-REVIEW comment at Ch 6:191, which instructs: *"Match the exact disclosure phrasing used in the metadata lines of Chapters 2–5."* **That instruction is not executable — Chapters 2–5 use four different phrasings and Ch 2 has no Domain line in this pattern at all.** There is no canonical form to match; one has to be chosen. Recommend adopting Ch 5:190's form book-wide. Ch 6 is also the only chapter carrying a `[source:]` tag *inside* the domain half of the metadata line.

✅ Separately: removing `D1.1` from the reader-facing metadata line was **correct and now verified complete**. Objective IDs appear only in YAML frontmatter (`objectives:`) across Ch 2, 3, 4 — never in reader-facing prose. Ch 6 now matches.

**2. Chapter 7 attributes to Chapter 6 a statement Chapter 6 does not make.** Detailed under Callback correctness. Fix lands in Ch 7:696.

**3. Forward cross-bearings collide across chapters.** (Medium — systemic, and Ch 6 is a participant, not the cause.)

Section numbers assigned to *unwritten* chapters are not coordinated, so published and pending chapters point different readers at different sections for the same content:

| Destination | Assigned by | …and by | Conflict |
|---|---|---|---|
| Ch 9 §1 | Ch 2: *CNI and pod networking* | Ch 6: *why something needs a stable name* | same section, two subjects |
| CNI in Ch 9 | Ch 2: **§1** | Ch 6: **§7** | same subject, two sections |
| Ch 13 §2 | Ch 2/Ch 5: *ImagePullBackOff / Pod won't start* | Ch 6: *`kubectl top` without metrics-server* | conflict |
| Ch 13 §3 | Ch 5: *logs from a multi-container Pod* | Ch 6: *diagnosing a stuck rollout* | conflict |
| Ch 13 §4 | Ch 5: *OOMKilled and Evicted* | Ch 6: *metrics-server is what an HPA reads* | conflict |
| Ch 15 §4 | Ch 5: *the delivery agent's identity* | Ch 6: *blue/green, canary, A/B* | conflict |
| Ch 17 §4 | Ch 1: *certification landscape* | Ch 2 (×2): *the four pluggable interfaces* | conflict |
| extension-points synthesis | Ch 2: **Ch 17 §4** | Ch 6: **Ch 17 §6** | same subject, two sections |
| Ch 18 §3 | Ch 5: *utilization relative to requests* | Ch 6: *node-level log collection* | conflict |

**Ch 6 also disagrees with itself once:** §2 points at `Ch 13 §4 — metrics-server is what an HPA reads`, while §8 points at `Ch 13 §2 — kubectl top without metrics-server`. Same component, two sections, one chapter.

> **Recommended systemic fix — and the book has already started adopting it.** Drop the `§` from cross-bearings that point into chapters not yet drafted; keep `*[cross-bearing: see Ch N — topic]*`. Evidence this is the house direction: Chapter 4's most recent re-draft (`73fd066`) stripped section numbers from **all three** of its Ch 6 pointers, and Chapter 2's most recent commit is literally titled *"Ch-02: drop §3 from the Ch 7 pointer."* Section numbers can be added by `reconcile.py` once a destination chapter is final. Backward pointers into published chapters should keep their `§` — they're verifiable, and Ch 6's are (with the one Ch 7 §5 exception) correct.

---

## Recommended fixes

Ordered by cost-to-fix against risk-if-shipped. Items 1–4 are one-token edits.

**Fix in Chapter 6 (blocking):**

1. **§7 closing cross-bearing: `Ch 7 §5` → `Ch 7 §4`.** Broken pointer into a published chapter; taints are Ch 7 §4, and the DaemonSet material Ch 6 is aiming at is at Ch 7:696, inside §4.
2. **`## Exam Alert` → `## Exam Alert! 🚨`.** Ch 6 is the only chapter with no 🚨.
3. **Add topics to the three checkpoint headings.** Every other chapter carries one; the skill template requires one.
4. **Metadata line: adopt Ch 5:190's form** — "share of the exam," with the authored-allocation disclosure inline. Also update the Why-This-Chapter-Matters sentence ("six percent of the book's authored allocation").

**Fix in Chapter 6 (recommended):**

5. Resolve the internal metrics-server split (§2 `Ch 13 §4` vs §8 `Ch 13 §2`) — or drop both `§`s per the systemic fix.
6. Add cross-bearings at first use for **EndpointSlice** (→ Ch 9), **RBAC** (→ Ch 12), and **nodeSelector/node affinity** (→ Ch 7). Three inline brackets.
7. Recover the dropped `ch04-fig03-labels-selectors-join` reference in §3 — a free retrieval event the outline specified and drafting lost.
8. Trim the `Ch 3 §6` cross-bearing tail, or extend it to `§6–§7`.

**Fix in other chapters (author decision — outside this chapter's scope):**

9. `chapter-01:436` — `Ch 6 §3` → **`§6`**. *(Already flagged in draft AUTHOR-REVIEW; verified on disk; still open.)*
10. `chapter-02:600` — `Ch 6 §3` → **`§8`**. *(Same.)*
11. `chapter-07:696` — rewrite the opening clause; Ch 6 poses the DaemonSet/taint question, it doesn't answer it. **This discharges the open AUTHOR-REVIEW at chapter-07:1293 — both of its Ch 6 pointers are now verified correct.**
12. Correct the stale numbering warning in `ch-06/outline.md` (§3 header, line 407) and the chapter frontmatter (lines 18–30): §3 is **no longer pinned by chapter-04**, which dropped its section numbers in `73fd066`.
13. Book-level sweep, low priority: settle `## §N — ⚪` (Ch 2, 3, 4) vs `## ⚪ §N —` (Ch 5, 6, 7).

**Verify before ship:**

14. Check whether **B1 trap #21** is labelled `[source]` or `[inferred]`. If inferred, soften Ch 6's reader-population claims ("the one most people arrive with," "you are in the majority," "the most common wrong answer") to non-frequency phrasing, per B2's instruction at chapter-lineup:184.

**Already caught upstream — not re-flagged here.** The draft's AUTHOR-REVIEW comments and the four diagnostics between them already cover: the `D1.1` removal (verified complete), the 13-vs-12 rolling-update arithmetic, the fig04/fig05 anchor–caption transposition, the `ch06-zenith-*` anchor pattern, the hedged DaemonSet `replicas` phrasing, the two Ch 11 facts cut from §6, the Q3/Q7 re-cuts, and the three untested concepts (HPA, overlapping selectors, CronJob idempotency). Those were handled correctly; nothing above duplicates them.

**Not an issue.** The chapter's reasoning, sourcing discipline and answer-key completeness are the strongest in Part II — every one of the 23 multiple-choice items carries full per-option why-wrong treatment, and §1's "the number is written twice" and §6's "a loop left open on purpose" are exactly the kind of honest simplification-flagging guardrail #5 asks for. The integration defects are all at the seams, and none of them require touching the prose.
```

---

A few things worth surfacing directly, since they change what you'd otherwise do:

**The `Ch 7 §5` pointer is a real broken link, and it's newly checkable.** Chapter 7 got drafted and committed, so I could resolve Ch 6's forward pointers instead of deferring them. §1 is right; §5 should be §4.

**Chapter 4's re-draft invalidated the outline's numbering constraint.** The ch-06 frontmatter says §3 is pinned by `chapter-04:688`. That pin is gone — commit `73fd066` stripped section numbers from all three of Chapter 4's Ch 6 pointers. The recommended §6/§8 fixes for ch01/ch02 are still correct, but the *reasoning* recorded in the outline is stale and will mislead the next session.

**The forward-cross-bearing collisions are a book-level problem, not a Ch 6 problem.** Nine conflicts across chapters 9, 13, 15, 17, 18. Chapters 2 and 4 have already independently started dropping `§` from forward pointers — that convention looks like the fix, and it would retire the whole class.

I couldn't verify one thing: whether B1 trap #21 is `[source]` or `[inferred]`. That determines whether the chapter's "most people arrive with this" phrasing is allowed under B2's own rule, and B1 wasn't in the material I had access to.
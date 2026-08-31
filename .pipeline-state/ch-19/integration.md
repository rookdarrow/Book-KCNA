All 43 distinct section pointers resolve. I have what I need.

```markdown
# Integration Check — KCNA Chapter 19

## Summary

- Terminology consistency: **pass**
- Callbacks to earlier chapters: **45 correct / 0 incorrect** (43 distinct `Ch N §M` pointers + 2 in the `17 §2` shorthand; all resolve against the section skeleton)
- Retrieval-practice accuracy: **pass** (5 tagged checkpoint questions + 10 Practice answer-key attributions, all verified)
- Glossary coverage: **0 new exam concepts introduced by design; 1 untaught claim introduced in error; 2 terms require glossary entries** (both carried forward from the Ch 17 gate, not created here)
- Contradictions with earlier canon: **4 flagged** — one of them requires a retrofit to *shipped Chapter 1*
- Ethical guardrails (skill Part 14): **pass** (notably strong)

The chapter's integration work is the best in the commission so far: 45 cross-references, zero broken. The findings below are concentrated in three places — a shipped-Ch-1 fact that Ch 19 correctly supersedes, a promise ("nothing new") that one table row breaks, and a blocking artifact gap Ch 1 has already sold to the reader.

---

## Terminology consistency

Swept the draft against the B7 canonical-forms table and the shipped text of Ch 1–18. Drift patterns searched for explicitly: `cloud-native`, `ArgoCD`, `Argo-CD`, `Kubelet`, `Etcd`, `Stateful Set`, `Network Policy`, `Service Account`, `Config Map`, `Cluster IP`, `kube-api-server`, `Minion`, `FluxCD`, `12-factor`, `ambient mesh`, `Shoals Ahead`, `Road Ahead`. **Zero hits on any of them.**

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| absent-component pattern (the sentence) | *An object without its component does nothing* | 5 | **No** — byte-identical to all 28 shipped uses across Ch 3/6/10/11/13/17/18 |
| absent-component pattern (the label) | `absent-component` | 4 | No — established in shipped Ch 3/10/11/17 (11 uses); not a Ch 19 coinage |
| cloud native | unhyphenated | 12 | No — 0 hyphenated instances (Ch 1–8 carry 16; Ch 19 does not add to the debt) |
| Argo CD | two words | 3 | No |
| ambient mode | not "ambient mesh" | 3 | No — matches the Ch 17 gate erratum and Ch 17's own 11 uses |
| Pod / kubectl / etcd / Kubernetes | Pod capitalized; other three lowercase | many | No |
| Object names (StatefulSet, DaemonSet, EndpointSlice, PersistentVolumeClaim, CustomResourceDefinition, IngressClass, ResourceQuota, LimitRange, NetworkPolicy, ServiceAccount, RuntimeClass…) | exact CamelCase, unspaced | many | No |
| Endpoints (legacy object) | reserved; no chapter teaches it | 0 capitalized-bare | No — lowercase `endpoints` used correctly for backend addresses |
| namespace / control plane / sandbox / revision / rollback / label / request / binding / release / Service / immutable / operator | homonyms, each marked | homonym table + inline | No — every second sense is explicitly qualified |
| The Voyage Ahead | locked section name | 1 | No — correct; not "The Road Ahead" |
| Landfall | **retired marker name** [LOCKED 2026-04-20] | 2 (H1 title + its own AUTHOR-REVIEW) | **See Contradiction 1** |

Three naming choices are *consistent within the chapter* but diverge from the ledger headword and from Ch 18's shipped handoff. None is drift in the mechanical sense; each is a headword that needs ratifying one way or the other:

| Ch 19 uses | Ledger headword | Shipped Ch 18 handoff uses |
|---|---|---|
| **thread** (§1 heading + all nine subheads) | Cross-cutting theme | "Nine **cross-cutting themes** traced through twenty chapters" (line 1721) |
| **discriminator** | Discriminating question | "each with **a question that discriminates** between them" (line 1721) |
| **volume** homonym = Pod-spec volume vs PersistentVolume | ledger's `volume` homonym is Kubernetes volume vs *Docker* volume | — |

Ch 19 uses "cross-cutting themes" exactly once (What You'll Learn) and "thread" everywhere else, so a reader crossing the Ch 18 → Ch 19 boundary meets a renamed concept with no bridge. The volume row is a *better* distinction than the ledger's for this reader — both senses are owned in Ch 11 and the Docker sense is banned — but it is an unsanctioned homonym pair and should be added to Canonical forms rather than left to a single chapter.

---

## Callback correctness

Every `Ch N §M` pointer was checked mechanically against the section skeleton, not against my reading of the target chapter.

**43 distinct pointers, all resolving.** Full list verified: Ch 2 §3, §4 · Ch 3 §4, §6 · Ch 4 §1, §3, §5 · Ch 5 §5, §6, §8 · Ch 6 §2, §3, §4, §8 · Ch 7 §2, §3, §4 · Ch 8 §3 · Ch 9 §1, §4 · Ch 10 §3, §6, §7 · Ch 11 §1, §2, §4, §5 · Ch 12 §2, §3, §4, §9 · Ch 13 §2, §4, §7 · Ch 14 §6 · Ch 15 §2, §4, §7 · Ch 16 §3, §4 · Ch 17 §4, §7 · Ch 18 §3. Plus `17 §2` and `17 §8` in the Practice answer keys, both valid.

Spot-checks on the riskiest ones, against shipped text rather than the skeleton alone:

- **Ch 3 §4 coins the phrase** — confirmed; the pattern sentence appears in shipped Ch 3, and Ch 10 §3 names it as a pattern, exactly as thread 3 describes.
- **Ch 10 §7 = NetworkPolicy inert on a non-implementing CNI** — confirmed; matches the ledger row *Policy inertness on an unsupporting CNI plugin*.
- **Ch 15 §2 owns the strategy vocabulary, Ch 6 §4 the mechanics** — the draft states this split explicitly and correctly.
- **Ch 12 §9 names RBAC and NetworkPolicy as one semantic** — confirmed against the skeleton's "Additive, Never Deny".
- **Practice Q9's stem names SIG Node, SIG Network, SIG Storage** — confirmed named in shipped Ch 17 (line 1479), so the stem is grounded, not decorative.
- **§2 D4's TAG/SIG naming-origin row** — confirmed; shipped Ch 17 line 1477 carries "later to be renamed".

Two Ch 1 conventions are honored: **no `Ch 1 §N` pointer is emitted anywhere** (Ch 1 has no numbered sections), and **Ch 20 is addressed by name only**.

**Two callbacks that should exist and don't.** Not defects — opportunities that matter because of the ruling in Recommended Fixes #5:

- The **liveness/readiness/startup** row (§2 D1) has no pointer to Ch 5 §7, which owns all three probes.
- The **Ingress frozen vs deprecated** row (§2 D2) and checkpoint Q4 have no pointer to **Ch 10 §4**, whose title is literally "Frozen, Not Deprecated".

---

## Retrieval-practice accuracy

All five `[retrieval: chN]` tags verified against the skeleton and, where the claim was load-bearing, against shipped text.

| Question | Tag | Verdict |
|---|---|---|
| Q1 — CRD with no operator | `ch3, ch6, ch10, ch13, ch17` | **Correct**, all five. Ch 3 §4 coins · Ch 6 §8 CRDs/operators · Ch 10 §3 names the pattern · Ch 13 §7 `kubectl top` · Ch 17 §7 VPA. The answer key's five example instances each map to a real owning section. |
| Q2 — RoleBinding + ClusterRole | `ch4, ch12` | **Correct.** Ch 4 §3 scope, Ch 12 §3 matrix. The key derives from Ch 4 rather than reciting Ch 12, which is what the stem asks for. |
| Q3 — `Pending`, wrong instrument | `ch5, ch7, ch13` | **Correct.** Ch 5 §5 phase/state · Ch 7 §2 Pending as scheduling outcome · Ch 13 §2 diagnosing a Pod that will not start. |
| Q4 — frozen vs deprecated | `ch10` | **Correct.** Ch 10 §4. |
| Q5 — revision/rollback homonym | `ch6, ch14` | **Correct.** Ch 6 §5 and Ch 14 §3, the two owners the ledger names for the collision. |

The ten Practice answer keys each close with a chapter attribution line. All ten check out, including the two that reach across three chapters (Q9: Ch 17 §8 plus Ch 2/9/11 for the three interfaces; Q10: Ch 5 and Ch 12 for identity plus Ch 15 for push/pull).

Retrieval spacing is 100% by design for a synthesis chapter, which is correct and already recorded by the question-quality stage.

---

## Glossary coverage

Ch 19 is a review chapter and introduces no new exam vocabulary by design. The table records the exceptions.

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| cross-cutting theme / **thread** | yes (§1) | no — book apparatus; headword needs ratifying (see Terminology) |
| **confusion pair** | yes (§2) | no — apparatus |
| **discriminator** / discriminating question | yes (§2) | no — apparatus; headword needs ratifying |
| **the second pass** | yes (§3) | no — apparatus |
| flagging / marking a question | yes (§3, hedged) | no |
| the absent-component pattern (label) | retrieved, not introduced | no — but add as a sanctioned variant under the pattern's Canonical-forms row |
| **waypoint proxy** | no — appears only inside a quoted Istio definition | **yes** — 11 uses in shipped Ch 17, 1 here, and **no ledger row exists**. Carried forward, not created here. |
| **CloudEvents** | no — appears only inside a quoted Knative definition | **yes** — already queued by the Ch 17 gate erratum; re-recorded so it is not lost |
| SLI / SLO / SLA | yes, via sourced quotations | no — Ch 18 §7 owns all three; the SLA orphan assignment was honored (15 uses in shipped Ch 18) |
| Deployment `restartPolicy` must be `Always` | asserted, not taught | **see Contradiction 3** — this one needs an owner and a source, or removal |

---

## Contradictions with earlier canon

### 1. The chapter title revives a retired marker name — *author decision, already self-flagged*

`Bearings Before **Landfall**`. "Landfall" was retired as a branded-marker name [LOCKED 2026-04-20] with the note "any future 'Landfall' in drafts is drift," and the chapter's own §1 uses ☀️ Zenith correctly. The draft flags this itself and declines to retitle because the name is fixed by the skeleton. Confirmed: "Landfall" appears exactly twice in the draft — the H1 and its own AUTHOR-REVIEW comment — so the reader-facing exposure is the title alone. The structural linter has no rule for retired marker *names*, so this gate is the only thing that sees it. The draft's two suggested alternatives both work; "Two Landmarks" pays off the epigraph and §2's opening line.

### 2. Shipped Chapter 1 is now factually wrong, and Chapter 19 is what makes it visible — **requires a Ch 1 retrofit**

This is the significant finding. Ch 19 §3 states that the Linux Foundation **publishes** the 60-question figure in its candidate handbook. **Shipped Ch 1 states the opposite, in four places, two of them graded:**

| Ch 1 | Text |
|---|---|
| line 202 | "The question count is published nowhere: not on the exam page, not in the FAQ, not in the CNCF curriculum." |
| line 204 | "…a question count that **travels on repetition alone**." |
| line 341 | *(checkpoint answer key)* "The question count is not on the exam page — **or anywhere else the certifying body writes**." |
| line 554 | *(Chapter Summary table)* "The question count (**published nowhere**)" |

**Ch 19 is correct.** `provenance-kcna-60-questions-2026-08-31` explicitly supersedes the 08-23 file, states "THAT STATEMENT IS FALSE and must not be relied on by any drafting or revision stage," and names two of Ch 1's exact phrasings as forbidden: *"The question count travels on repetition alone"* and *"The question count is not anywhere the certifying body writes."* The figure is published on the LF T&C DOCS page "Multiple Choice Exams: Important Instructions." The fact-accuracy stage independently confirmed Ch 19's phrasing matches the mandated wording, including the class-level hedge.

Three consequences, all needing an author decision:

1. **Ch 1 lines 202, 204, 211, 215, 341–342, 554 need a retrofit.** The lesson survives — it changes from *whether* the authority publishes the figure to *where* — which is the framing Ch 19's ⚓ Worth Securing already uses, so Ch 1 can adopt Ch 19's language rather than inventing new. The Ch 1 hazard at line 211–213 (pace by proportion, not by question number) stays correct and is exactly what Ch 19 §3's ★ Fixed Point implements; **do not touch that part.**
2. **The section skeleton's Ch 20 block is now stale.** It instructs that block to say "the question count is **commonly reported**… rather than matched to a published figure," and that the Scoring Rubric "**does not state a pass mark as fact** — the 75% figure is unpublished." Both figures are published, for MC exams as a class. Ch 20 must not be drafted against the stale instruction.
3. **Found while verifying: shipped Ch 1 line 215 emits `*[cross-bearing: see Ch 20 §1 — how the mock exam is sized, and why]*`.** This is the only `Ch 20 §N` pointer in the book and the skeleton forbids it outright — Ch 20 has no numbered sections. Not Ch 19's defect, recorded because the *same sentence* carries the now-false "commonly-reported format" framing, so one edit repairs both.

### 3. "This chapter contains nothing new" is broken by one table row

Ch 19's Why This Chapter Matters says, in bold: "**it contains nothing new.** Every fact in it was taught somewhere in Chapters 2 through 18." Shipped **Ch 18 line 1717** makes the same promise to the reader on the way in: "Chapter 19 does not add material. It re-sees what you already have."

The §2 Domain 1 `restartPolicy` row breaks it: *"Note also that a Deployment's Pod template cannot use `Never` at all; the API requires `Always` there."*

Searched all eighteen shipped chapters for any statement of the Deployment-side restriction: **no matches.** Shipped Ch 6 line 906 teaches only the *Job* side ("a Job's Pod template may only use a `restartPolicy` of `Never` or `OnFailure`," sourced). The Deployment converse is untaught, unsourced, and has no owner in the ledger.

Context, because it changes the fix: the fact-accuracy stage flagged draft-v1's version of this row as describing a configuration that cannot exist, and the revision stage answered by *adding this sentence*. That resolved the factual defect and created an integration one. The fix is not to revert. Either (a) cut the clause and let the row illustrate the container-vs-Pod scope with a Job or bare Pod, which is what the fact-accuracy stage actually recommended and which stays inside taught material; or (b) keep it, source it, and accept that the chapter's "nothing new" claim and Ch 18's handoff both need softening.

### 4. "Twenty chapters" is now a three-way disagreement

The draft retitled §1 to "Nine Threads Through **Eighteen** Chapters," flagging that the skeleton's "Twenty" is wrong and recommending the skeleton be corrected. The draft did not have the whole picture: **shipped Ch 18 line 1721 also says twenty** — "Nine cross-cutting themes traced through twenty chapters."

So the count is: skeleton says twenty, shipped Ch 18 says twenty, Ch 19 draft says eighteen. The draft's reasoning is sound on the merits (the threads terminate at Ch 18, and the body prose says "eighteen chapters" consistently). But correcting only the skeleton leaves shipped Ch 18 promising a number the next page contradicts. Whichever way the author goes, **two of the three must move together.** Cheapest coherent fix: keep Ch 19 at "Eighteen," edit the skeleton, and change one word in Ch 18 line 1721.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Every number carries a source tag. §3 goes further than the checklist requires: where the LF publishes nothing about console navigation, the chapter says so and names the four pages it confirmed silent, then restructures the advice to work either way. That is the correct handling of legitimate uncertainty (guardrail 4).
- [x] **Fear-based content uses real examples.** §4's blueprint-change warning is grounded in the published 2025-11-24 change and its sourced "the only date that matters is the date you sit." §6's Logbook Entry defuses anxiety rather than manufacturing it.
- [x] **Simplification acknowledged.** Dead Reckoning blocks in Why This Chapter Matters and §4. §4's Dead Reckoning does something better than the checklist asks: it separates the *published* domain weights from the *editorial* chapter mapping and labels which is which.
- [x] **Authority claims cite legitimate sources.** LF handbook, CNCF charter, Kubernetes docs, Istio docs, Prometheus docs, the Google SRE book.
- [x] **"Frequently tested" claims are verifiable.** Searched for `frequently tested`, `commonly tested`, `always appears`, `guaranteed to`, `most candidates`, `% of candidates/test-takers`: **zero hits.** §4 explicitly refuses the frequency claim — "stated as arithmetic rather than as a claim about how often it is tested" — and argues from bounded surface area instead. This is the strongest handling of guardrail 8 in the commission.
- [x] **No strawmanning of alternative study methods.** §4 and §6 disparage re-reading and last-minute source-acquisition, but on the evidence base the skill itself endorses (testing effect, consolidation) and aimed at the reader's own behavior, not at a competitor. The pre-2025 third-party-material warning is factual and sourced, and gives a checkable tell rather than a blanket dismissal.
- [x] **Subject dignity (guardrail 9).** Humor is oriented at the practitioner throughout — the day-four bad session, the one unanswerable question. No third-party harm is treated as amusing.

---

## Recommended fixes

The diagnostics were worked hard: the answer-key `B`-clustering, the missing taints/tolerations pair, the missing ResourceQuota-vs-LimitRange pair, the §1 chapter count, and the `restartPolicy` factual defect were all addressed in revision. The items below are what this gate adds.

**Blocking**

1. **`the-lodestar.md` does not exist**, and this is worse than the draft's own AUTHOR-REVIEW knew. Shipped **Ch 1 line 452** already promises it to the reader by name — "a single page holding the exam-critical facts… Chapter 19 walks you through using it" — and emits `*[cross-bearing: see Ch 19 §5 — using The Lodestar]*`. So §5 cannot be cut, deferred, or reshaped around the absence; the artifact must be written. The six block names in §5 are provisional and become factual claims the moment it exists. Write the file, then reconcile §5 against it. Restore §5's opening to present tense at the same time.

**Author decisions**

2. **Retrofit shipped Ch 1's provenance passage** (Contradiction 2). Highest-value item here: it repairs a graded answer key that currently teaches the reader something false, and it unblocks Ch 20's Instructions and Scoring blocks. While in that sentence, retarget the forbidden `Ch 20 §1` pointer to address Ch 20 by name.
3. **Decide the `restartPolicy` clause** (Contradiction 3) — cut, or source-and-own.
4. **Decide the chapter count** (Contradiction 4) — two of {skeleton, Ch 18 line 1721, Ch 19 §1 title} must move together.
5. **Decide the title** (Contradiction 1).

**Corrections to the draft's own AUTHOR-REVIEW blocks — these reduce the author's workload**

6. **The consolidated research-gap block in §2 is a false alarm, and its premise is wrong.** It says a cluster of claims is uncovered by "this chapter's 31-file corpus" and asks for six research passes. The book's corpus is **199 files**, and every one of the six is already cached:

   | Draft's requested fetch | Already in `sources/` |
   |---|---|
   | 1. RBAC reference | `k8s-docs-rbac-2026-08-23`, `k8s-docs-rbac-depth-2026-08-31`, `k8s-docs-rbac-good-practices-2026-08-31` (cited 58× in Ch 12) |
   | 2. NetworkPolicy concept | `k8s-docs-network-policies-2026-08-23`, `k8s-docs-network-policies-depth-2026-08-24` |
   | 3. Ingress concept | `k8s-docs-ingress-2026-08-23`, `k8s-docs-ingress-controllers-2026-08-24`, `k8s-docs-ingress-depth-2026-08-24` |
   | 4. Pod lifecycle | `k8s-docs-pod-lifecycle-2026-08-23` |
   | 5. CNCF maturity levels | `cncf-project-maturity-levels-2026-08-23` |
   | 6. ConfigMap/Secret, Helm charts, OTel traces | `k8s-docs-configmap-2026-08-23`, `k8s-docs-secret-2026-08-23`, `helm-charts-2026-08-31`, `opentelemetry-signals-2026-08-23` |

   More to the point, **the book-level ruling ratified at the Ch 18 gate already discharges this entire class**: "a cross-bearing to the owning chapter discharges the `[source:]` obligation for a retrieved claim," provided the pointer names the owning *section* and the claim is not strengthened. Every one of these is taught and source-tagged in its owner. So the fix is **add cross-bearings to the §2 rows that carry them** — starting with the two named under Callback correctness (Ch 5 §7 for the probes row, Ch 10 §4 for the frozen/deprecated row) — not commission six research passes. Delete the block once the pointers are in.

   The one item in that block that is *not* discharged is the `restartPolicy` claim, because it has no owner. That is Contradiction 3.

7. **The §4 AUTHOR-REVIEW's retired-blueprint gap is correctly stated — leave it.** The draft was right to strip the five-domain and "Cloud Native Observability" details and rest the tell only on the sourced fact that observability moved under Cloud Native Architecture. Its suggested fix (retrieve `old-versions/KCNA_Curriculum old.pdf`) is a genuine open gap and would benefit Ch 20 as well as Ch 19.

**Fidelity repairs — cheap, and each one lands in drill material**

8. **The `Running` definition drops "or restarting."** Ch 5 §5 (line 574) defines it as "at least one container is still running, **or is in the process of starting or restarting**," and builds a ★ Fixed Point on the restarting case: "a crash-looping Pod reports the phase `Running`." Ch 19 says "at least one is running or starting" in all three places it states the definition — §2 D1 row, the ⚠ hazard, and the Chapter Summary — which technically excludes the CrashLoopBackOff case that is the hazard's whole point. Two-word insertion, three times.
9. **The second-default-IngressClass hazard is weaker than what Ch 10 taught.** Ch 19 says two defaults is "an ambiguous configuration." Shipped Ch 10 (lines 720, 724) gives the actual consequence: a second default "removes it, and the Ingress can no longer be created at all… They take away the one chance it had." Since this is one of only four hazards the reader is told to drill, it should carry Ch 10's outcome, not a softer paraphrase. Ch 10 sources it at `k8s-docs-ingress-controllers-2026-08-24`, so no research is needed.
10. **Ratify the headwords** — thread vs cross-cutting theme, discriminator vs discriminating question — and either align Ch 19 to Ch 18's handoff language or add a one-clause bridge in §1. Add the Pod-spec-volume vs PersistentVolume pair to Canonical forms as a sanctioned homonym.

**Ledger errata to record at the glossary build**

11. `Flagging and skipping | First appears Ch 1 | gloss in one clause + pointer` is wrong. Ch 1 does not gloss it; its only forward reference is `Ch 19 §3 — pacing and time discipline`. Ch 19 §3 is the first appearance, and it deliberately declines to promise the console supports it — which, usefully, means **there is no Ch 1 promise for that hedge to contradict.**
12. **`waypoint proxy`** needs a register row and a glossary entry (11 uses in Ch 17, 1 here, no ledger row).
13. **`CloudEvents`** glossary entry and register row — already queued at the Ch 17 gate, re-recorded here so it survives to stage 14.
14. Add **`absent-component pattern`** as a sanctioned label variant under the pattern's Canonical-forms row; it is established in four shipped chapters but the row currently only sanctions the sentence.
```
I audited all 45 questions against the outline's `question_budget`, the ★ Fixed Points in the draft, and the skill's self-correction rules. Emitting the stage artifact to stdout (per the pipeline's stdout-capture contract) rather than writing to a path relative to `certcomp/`:

---

```markdown
# Question-Quality Audit — Chapter 17

## Summary

- Chapter type: content
- Total questions inspected: 45
  - 🧭 Soundings questions: 8
  - ☆ Taking Your Bearings questions: 16 (across 3 checkpoints)
  - Practice questions: 21
- Question budget compliance: **met** (45/45, every category exact)
- Weak distractors (WARN): **5**
- Trap answers that don't target real misconceptions (WARN): **4** (one overlaps the above)
- Missing or incomplete why-wrong explanations (FAIL): **1**
- Retrieval-practice spacing: **compliant** — checkpoints land at exactly 25.0%, the ceiling the outline designed for
- Soundings spoiler check: **clean** — 8/8, including both edges the outline flagged as watched

**Three findings outrank everything in the per-question list, and two of them are chapter-wide rather than local:**

1. **FAIL — answer-key position and length bias.** 30 of 37 multiple-choice answers are **B**. Zero are **A**. Zero are **D**. Practice Q5–Q18 is a run of **fourteen consecutive B answers**. Compounding it, the correct option is the longest option in roughly 28 of 37 items and conspicuously longest in ~14. A reader who knows nothing and always picks the long B scores ~81%. This is the single largest defect in the chapter and it is mechanical to fix.
2. **FAIL — no revision prompts on any checkpoint.** All three ☆ blocks end with "Checkpoint: You've Now Mastered" and no scoring bands and no "if you scored 0–2, re-read §N" guidance. Skill Part 11 requires it; skill Part 15's template calls for it explicitly; the outline §5 states it as a per-checkpoint requirement ("a revision prompt naming a **section** for 0–2 scorers"). Delivered in the Soundings, absent from the Bearings.
3. **WARN — §8 is under-tested by two practice items, and the shortfall lands exactly on the most under-studied material in the book.** The outline allocated 3 practice questions to §8; the draft ships 1 (Q21). The surplus went to §4 and §5, which already have 4 each. Six §8 concepts are introduced and never tested: the contributor ladder, KEPs, subprojects, the Code of Conduct, KubeCon, and the certification ladder — the last of which the draft itself calls "the examinable part."

Everything else is in good shape. Distractor construction is otherwise strong, why-wrong coverage is near-total and source-tagged, the Soundings honors both drafting constraints the outline imposed, and TYB 2 Q1 delivers the integrated four-interface stem the outline demanded instead of the matching exercise it forbade.

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 16 | 16 | met |
| Taking Your Bearings (checkpoints) | ≥2 | 3 (6 + 5 + 5) | met |
| Practice Questions | 21 | 21 | met |
| **Chapter total** | **45** | **45** | **met** |

Checkpoint sizes are 6 / 5 / 5, all at or above the skill's 5-question floor, which is the arithmetic the outline's frontmatter note argued for when it set Bearings at 16 rather than the arc band's 12–15. That argument holds up: 16 across three checkpoints is the smallest configuration that puts retrieval at exactly 25.0% without rounding past the ceiling.

**Internal distribution has drifted, though the total has not.** Practice questions by section:

| Section | Outline target | Actual | Delta |
|---|---|---|---|
| §1 definition | 3 | 3 (Q1–Q3) | — |
| §2 maturity/governance/Landscape | 3 | 3 (Q4–Q6) | — |
| §3 microservices/immutability | 1 | 1 (Q7) | — |
| §4 four interfaces | 3 | 4 (Q8–Q11) | **+1** |
| §5 service mesh | 3 | 4 (Q12–Q15) | **+1** |
| §6 serverless | 2 | 2 (Q16–Q17) | — |
| §7 autoscaling | 3 | 3 (Q18–Q20) | — |
| §8 governance/ladder/KEPs/certs | 3 | **1** (Q21) | **−2** |

The outline budgeted D4.3 at 6 of 21 practice items (28.6%) and justified the over-allocation from B1: it is the competency technically strong candidates most reliably under-study. Actual D4.3 practice coverage is 4 of 21 (19.0%) — Q4, Q5, Q6, Q21 — which is below D4.3's share of the chapter's section count, and inverts the outline's whole rationale.

TYB 3 does meet its floor: Q3 (SIG/WG/Committee) and Q4 (SIG Release/cadence) are both D4.3, satisfying "TYB 3 must carry at least two D4.3 items." It meets it exactly, with no margin.

## Soundings spoiler check

Chapter Fixed Points, for reference: (FP1) the five characteristics; (FP2) Sandbox→Incubating→Graduated; (FP3) the four pluggable interfaces and the interface-and-implementation shape; (FP4) mesh features without code changes; (FP5) mesh data plane / mesh control plane / cluster control plane; (FP6) serverless as lifecycle, still containers in Pods; (FP7) horizontal vs vertical; (FP8) SIG / Working Group / Committee; (FP9) three releases a year and three supported minors are one fact.

All 8 Soundings questions are open-response, so there are no distractors to evaluate — spoiler risk lives entirely in the stems and the `<details>` answer text.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | CRI/CNI/CSI → layer mapping (Ch 2 §4, 9 §1, 11 §5) | **no — watched edge, constraint honored** | Answer is exactly the three-row acronym→layer table the outline mandated. Never says *interface*, *pluggable*, *extension* or *implementation*; never mentions CRDs; asks for the mapping, not the shape. FP3 survives intact for §4/§9. |
| 2 | What the published definition is about (Ch 1 plant) | **no** | Answer refuses to enumerate: "Hold whatever sentence you wrote. §1 opens with the published definition verbatim, and you will be able to measure your answer against it word for word." The outline's constraint — no characteristic named in the rationale line — is honored exactly. FP1 untouched. |
| 3 | Supported minor versions (Ch 8 §6) | **no** | Answer gives the support-window half only ("Three... release branches for the most recent three minor releases"). The cadence half and the identity claim that makes FP9 a Fixed Point are withheld for §8. |
| 4 | What a sidecar is and shares (Ch 5 §1–2) | **no** | Pod-level model only: network namespace, `localhost`, shared volumes. No mesh, no proxy, no Envoy. FP4/FP5 untouched. |
| 5 | HPA with no metrics-server (Ch 6 §2, 13 §7) | **no — watched edge, constraint honored** | Answer text does not mention VPA, as the outline required. The absent-component pattern is stated in generic terms ("The object exists; the component that would act on it does not") without pre-spending §7's VPA payoff. FP7 untouched. |
| 6 | Pending Pod and what it states (Ch 7 §2) | **no** | Names no autoscaler. Closes at "a standing, machine-readable statement that the cluster is short of somewhere to put work" — the exact half Ch 7 planted, with §7's answer withheld. |
| 7 | SIG / cross-SIG group name | **partial — deliberate, and within the outline's ratification** | Answer discloses "SIG" and "Working Group" as names. This is the pretesting effect the outline explicitly sanctioned. FP8's discriminating content — Committees, closed membership, chartering by Steering — is entirely absent from stem and answer. Note for the record: the stem supplies the adjectives *durable*, *topic-focused*, and *across several of them*, so what §8 has left to confirm for SIG/WG is the vocabulary rather than the distinction. Acceptable; the genuinely new material is untouched. |
| 8 | What protects Ingress→Pod after TLS terminates | **no** | Establishes the gap and stops: "Nothing, by default… NetworkPolicy… cannot encrypt anything." No mesh, no mTLS, no zero trust, no proxy. FP4 and FP5 both survive for §5. This is a textbook generation-effect setup. |

**Rubric check:** PASS. The three branches (6+ / 3–5 / 0–2) are all present, and the 0–2 branch names sections rather than chapters ("re-read **Chapter 2 §8** and **Chapter 11 §5**… Not alongside this chapter; before it"), which is what the outline specified.

**Answer disclosure check:** PASS. `<details><summary>Click for answers + reading strategy</summary>` wraps the full answer block.

## Chapter-wide answer-key defects

These are not per-question problems; they are properties of the set.

### Answer-position bias — FAIL

| Letter | TYB 1 | TYB 2 | TYB 3 | Practice | Total (of 37) |
|---|---|---|---|---|---|
| A | 0 | 0 | 0 | 0 | **0** |
| B | 5 | 4 | 3 | 18 | **30 (81%)** |
| C | 1 | 1 | 2 | 3 | **7 (19%)** |
| D | 0 | 0 | 0 | 0 | **0** |

Practice Q5 through Q18 is an unbroken run of **fourteen B answers**. Option A is never correct anywhere in the chapter; neither is option D. A reader who marks B on every item scores 30/37 without opening the book.

This is not a cosmetic complaint. Skill Part 10B lists "trick questions that test reading comprehension, not knowledge" among *undesirable* difficulties, and the mirror-image failure — a key that can be gamed without knowledge — defeats the testing effect the whole checkpoint architecture is built on. It also means the chapter's measured scores are not diagnostic: a reader scoring 26/37 cannot tell whether they know the material or found the pattern.

**Recommended fix:** shuffle correct-answer positions to roughly uniform (target ~9/9/9/10 across A/B/C/D) and cap consecutive repeats at two. This is a mechanical edit that does not touch a single stem, distractor, or explanation — only the option ordering and the letters in the key. Do it as a scripted pass so the why-wrong bullets are relettered in lockstep; hand-editing 37 keys is where relettering errors get introduced.

### Answer-length cue — FAIL, and it compounds the above

The correct option is the longest option in roughly 28 of 37 items, and is conspicuously longest (≥1.5× the mean distractor length) in about 14. Worst offenders, where the correct answer carries two or three clauses against one-clause distractors:

- TYB 2 Q5 — B is three clauses; A/C/D are one each
- TYB 3 Q3 — C is two clauses; A/B/D are one each
- TYB 3 Q4 — C is three clauses with two source facts; A/B/D are one each
- TYB 3 Q5 — B is three clauses; A/C/D are one each
- Practice Q5, Q6, Q7, Q10, Q11, Q15, Q16, Q20, Q21 — same shape

The mechanism is understandable: the correct answer is the one that has to be precise, so it accretes qualifiers. But paired with the B-bias it makes the set close to free.

**Recommended fix:** pull the qualifiers out of the correct option and into the why-wrong explanation, where they belong and where they are already mostly duplicated. Where the correct answer genuinely needs the length, lengthen one distractor to match — the trap distractor is the natural candidate, since a *long, plausible, wrong* option is the strongest thing you can put in front of a test-wise reader.

Three questions already do this correctly and are the model: **Practice Q1** (four parallel five-item lists), **Practice Q9** (four parallel one-clause options), and **Practice Q12** (the correct answer, "Without requiring code changes," is the *shortest* option on the page). **TYB 1 Q5** and **TYB 2 Q2** likewise have the shortest option correct.

### Missing revision prompts — FAIL

None of the three checkpoints carries scoring bands or low-score guidance. Each ends with a "Checkpoint: You've Now Mastered" list and a forward transition.

Required by skill Part 11 ("Revision Prompts… provide clear guidance"), skill Part 13 ("Micro-Progress After Checkpoints" — the 5/5, 3–4, 0–2 pattern), skill Part 15's checkpoint template ("[If scored 0-2: revision prompt with specific section reference]"), and the outline §5 in as many words: "Every checkpoint carries… a revision prompt naming a **section** for 0–2 scorers."

The Soundings does this well, which makes the omission look like a drafting oversight rather than a decision. Suggested targets, using the outline's own section-not-chapter rule:

- **TYB 1, 0–2:** re-read §1's characteristics clause and §2's three rungs before continuing; §4 assumes both.
- **TYB 2, 0–2:** re-read §4 in full. If the four-interface item (Q1) was the miss specifically, go back to Ch 2 §8 and Ch 11 §5 first — §9 will not land otherwise.
- **TYB 3, 0–2:** re-read §7's autoscaler grid and §8's three groups. These are the chapter's two highest-density recall blocks.

## Per-question findings

### Q[TYB 1] 5: "The CNCF Cloud Native Definition lists containers, service meshes, multi-tenancy, microservices, immutable infrastructure, serverless, and declarative APIs. What does the definition say about this list?"

**Issue:** Two of three distractors are fabricated for symmetry, and the answer key says so itself. Functionally a two-option question.

**Distractor analysis:**
- A) These seven are the complete set of cloud native technologies — **plausible; targets a real misconception.** An authoritative seven-item list reads as an enumeration. This is trap #114 and it is the reason the question exists.
- B) The list is non-exhaustive — correct.
- C) A system must use at least four of the seven to be cloud native — **implausible.** No reader holds a "four of seven" threshold. The key concedes it: "C invents a threshold that appears nowhere."
- D) The list is ordered by importance — **borderline.** Readers do sometimes treat lists as ranked, so this has a thin claim to plausibility, but the key also concedes it as an invention.

**Why-wrong explanation status:** present and specific.

**Recommended fix:** replace C with a misconception that is actually in circulation. Two good candidates from the chapter's own material: *"Every cloud native system uses containers"* (the strongest real belief in this space, and refuted by the same non-exhaustive clause) or *"The list defines what CNCF will host as a project"* (conflates the definition with the Landscape's category criteria, taught two sections later). Either turns a filler slot into a second discriminating trap. Leave D; it is weak but not empty.

### Q[Practice] 7: "The CNCF glossary argues that a well-designed monolith 'can uphold lean principles by being the simplest way to get an application up and running.' What is the reasoning?"

**Issue:** Two distractors are eliminable without knowing the material — one by the absolute-word heuristic, one by contradiction with a passage quoted verbatim four sections earlier.

**Distractor analysis:**
- A) Monoliths always outperform microservices at scale — **weak.** "Always" is a standing giveaway; test-wise readers strike absolutes on sight. The underlying belief (monoliths can outperform) is real, but the phrasing hands it away.
- B) Microservices increase operational overhead, and building a microservices-based app before it has proven valuable may be premature spending of engineering effort — correct.
- C) Microservices are incompatible with cloud native architecture — **weak.** §1 quotes the definition in full, and microservices are in its technology list. The chapter refutes this option on its own page 1. Nobody who has read to Q7 can hold it.
- D) Monoliths are easier to make immutable — **plausible.** §3 sits immutable infrastructure next to microservices, so the conflation is available. Keep.

**Why-wrong explanation status:** present and specific.

**Recommended fix:** drop the absolute in A ("Monoliths outperform microservices at scale" — now a real, defensible-sounding claim the glossary does not make). Replace C with a misconception that survives §1: *"Microservices reduce total system complexity"* — a genuinely widespread belief and precisely what the glossary's "increases its operational overhead" refutes, so the correct answer stays the discriminator.

### Q[Practice] 14: "A team encrypts service-to-service traffic with mTLS via a mesh, and separately enables encryption at rest for etcd. What do these two measures protect, respectively?"

**Issue:** Option A is ambiguous enough to be arguable, and option C is fabricated.

**Distractor analysis:**
- A) Both protect the same data at different times — **ambiguous.** A Secret in transit and the same Secret at rest arguably *is* "the same data at different times," which makes A defensible on a literal reading. The key's rebuttal ("A obscures the distinction") is a rhetorical objection, not a factual one. Skill Part 10B names "ambiguous questions with multiple defensible answers" as an undesirable difficulty.
- B) mTLS protects data in transit between workloads; encryption at rest protects the stored contents of the cluster's datastore. Neither substitutes for the other — correct.
- C) mTLS protects Secrets; encryption at rest protects ConfigMaps — **implausible.** No object-type split of this kind exists in anyone's mental model.
- D) Encryption at rest makes mTLS redundant, since traffic originates from encrypted storage — **strong.** This is the real misconception and the reason the question earns its slot.

**Why-wrong explanation status:** present and specific.

**Recommended fix:** rewrite A to be unambiguously wrong while staying tempting — *"Both protect data in transit; encryption at rest additionally protects backups"* — which targets a real conflation without being half-true. Replace C with the ConfigMap/Secret misconception that actually exists: *"mTLS protects data in transit; encryption at rest means Secrets are encrypted before they reach etcd"* (which is wrong about *where* the encryption happens and is a genuine Ch 12 §4 trap).

### Q[Practice] 16: "Knative Serving and Knative Eventing answer different questions. Which pairing is correct?"

**Issue:** One dead distractor, **and the chapter's only incomplete why-wrong explanation.**

**Distractor analysis:**
- A) Serving handles asynchronous events; Eventing handles synchronous HTTP — **strong.** The straight swap, and the exact error a reader who knows both names but not their jobs will make. This is trap #83.
- B) Serving is an HTTP-triggered autoscaling container runtime including scale to zero; Eventing is a CloudEvents-over-HTTP asynchronous routing layer — correct.
- C) Serving handles ingress routing; Eventing handles logging — **implausible.** "Eventing handles logging" corresponds to no belief anyone holds; it is not even adjacent to the real confusion.
- D) Serving is for stateful workloads; Eventing is for stateless ones — **plausible and better than it looks.** Serving is explicitly for *stateless* HTTP services, so D inverts a stated fact and deserves a specific rebuttal.

**Why-wrong explanation status:** **present but vague — the one FAIL in the chapter.** The key collapses two options into four words: "**C** and **D** invent roles for both." That tells a reader who chose D nothing about what is wrong with D, and D is the option whose error is most worth naming. Every other key in the chapter's 37 items rebuts each option individually and cites a source; this is the sole exception.

**Recommended fix:** split the rebuttal. For **D** specifically: *"D inverts a stated property. Knative Serving manages 'the complete lifecycle of stateless HTTP services' [source: knative-overview-2026-08-23] — stateless is Serving's own description of its workloads, not Eventing's. Neither component is distinguished by statefulness."* Then replace **C** with a live confusion: *"Serving runs the workload; Eventing is the autoscaler that scales it"* — which targets a reader who has met KPA and mis-files it.

### Q[Practice] 9: "A team needs the kube-apiserver to recognize and store a new object kind, served through the standard API so `kubectl get` works, without running any additional API server process. Which mechanism, and which of the four pluggable interfaces does it represent?"

**Issue:** Near-verbatim duplicate of TYB 2 Q2, and its retrieval tag is malformed.

TYB 2 Q2: *"A team wants to add a new API to their cluster that Kubernetes will store and serve for them, so that `kubectl get` works on their new object type without them running any additional API server. Which extension mechanism fits?"*

Same constraint, same correct answer (CRD), same trap (the aggregation layer as option A), same discriminating knowledge. Q9's added clause — "and which of the four pluggable interfaces does it represent" — does not change what a reader must know, because both parts are settled by the same §4 paragraph. This spends one of 21 practice slots re-asking a checkpoint item in a chapter where §8 is short by two.

**Distractor analysis:** the options themselves are well built and length-balanced — A (aggregation layer, the documentation's own named near-miss), C (mutating webhook), D (scheduler plugin) are all real mechanisms at wrong layers. No defect here.

**Why-wrong explanation status:** present and specific.

**Secondary issue:** the tag reads `[retrieval]` with no chapter, where every other tagged item in the chapter uses `[retrieval: chN]`. Downstream stages that count tags by chapter will not see this one.

**Recommended fix:** reallocate Q9 to §8 and close part of the D4.3 gap. The contributor ladder is the strongest candidate, because it has a concrete, source-backed, counterintuitive fact that nothing currently tests — *sponsorship by two reviewers from different companies*. A stem such as: *"An engineer has six merged PRs, 2FA enabled, and is subscribed to the dev list. Two reviewers from their own employer offer to sponsor their Kubernetes membership. What is missing?"* — with distractors covering "nothing, they qualify," "a subproject owner's nomination" (that is the Approver rung), and "twenty reviewed PRs" (that is the Reviewer rung). That tests the ladder's structure and its one structural safeguard in a single item.

### Q[Practice] 17: "How does Knative relate to Kubernetes?"

**Issue:** substantial overlap with TYB 3 Q5, which is four pages earlier.

TYB 3 Q5 asks the reader to correct "we're not running containers any more"; its correct answer is *"Knative builds on the Kubernetes Pod abstraction and Serving and Eventing are implemented as CRDs — the workloads are still containers in Pods."* Q17's correct answer is *"Knative is Kubernetes-based, builds on the Pod abstraction, and Serving and Eventing are implemented as CustomResourceDefinitions."* Same two source facts, same source citation, differently framed stem.

This is milder than the Q9/TYB2-Q2 duplication — the framings differ (correct-the-colleague vs. state-the-relationship) and FP6 is the chapter's most-warned-about misconception, so deliberate reinforcement is defensible. Flagging it because it is the second of only two practice slots spent re-covering checkpoint ground, and §6 already has its full 2-item budget.

**Distractor analysis:** A (replaces the control plane), C (runs containers outside Pods), D (a fork) are all plausible readings of "serverless." C in particular is the misconception in mechanical dress. No defect.

**Why-wrong explanation status:** present and specific. The combined "A and D both assert replacement or forking; Knative does neither" is acceptable — unlike Q16's, it names the shared error and refutes it.

**Recommended fix:** optional. If §8's shortfall is being closed by reallocation, Q17 is the second-best donor after Q9. A replacement testing the Code of Conduct's scope would be well earned, since the draft flags that scope statement as "the examinable part" and nothing tests it: *"A CNCF contributor makes harassing remarks about another contributor on a personal social media account, outside any project or event space. Does the CNCF Code of Conduct apply?"* — correct answer yes, because the code covers conduct "in other spaces when an individual CNCF community participant's words or actions are directed at… another CNCF community participant in the context of a CNCF activity."

### Q[Practice] 20: "Which correctly pairs each autoscaler with the axis it moves?"

**Issue:** one filler distractor; the question is otherwise the section's best.

**Distractor analysis:**
- A) HPA → resources; VPA → replicas; Cluster Autoscaler → node pool — **strong.** The horizontal/vertical swap is the named trap and the most common error in this material.
- B) HPA → replicas; VPA → resources; Cluster Autoscaler → nodes; KEDA → replicas — correct.
- C) HPA → node pool; KEDA → resources; VPA → replicas — **implausible.** A three-way scramble matching no coherent misconception. Nobody thinks the HPA provisions machines.
- D) All four move the replica count, differing only in what triggers them — **strong, and subtle.** Targets a reader who over-learned §7's KEDA/HPA axis overlap and generalized it. Excellent trap fidelity.

**Why-wrong explanation status:** present and specific.

**Recommended fix:** replace C with the other real error in this material — the Pod/node confusion the Exam Alert names: *"HPA → replicas; VPA → resources; KEDA → node pool"*, which catches a reader who knows KEDA is "the external one" and files it with the cloud-provider autoscalers. Note also that B is the only option naming four autoscalers where A/C name three, which is a length cue on top of the position bias; adding KEDA to A and C removes it.

## Retrieval-practice spacing

**Checkpoints — compliant, and precisely engineered.**

- Chapter 17 target: 20–25% (skill Part 10, "Chapter 6+"); the outline designates this a *ceiling* chapter and targets exactly 25%
- Actual: **25.0% (4 of 16)**
- Status: **compliant, at ceiling**

| Checkpoint | Item | Tag | Answer lives in |
|---|---|---|---|
| TYB 1 | Q6 | `[retrieval: ch2]` | Ch 2 §2 — image immutability. **15 chapters back.** |
| TYB 2 | Q1 | `[retrieval: ch2, ch6, ch9, ch11]` | Ch 2 §4 / 6 §8 / 9 §1 / 11 §5, as one integrated item |
| TYB 2 | Q3 | `[retrieval: ch10]` | Ch 10 §6–§7 — what NetworkPolicy cannot do |
| TYB 3 | Q4 | `[retrieval: ch8]` | Ch 8 §6 — three supported minors. **9 chapters back.** |

The ≥4-back floor is met four times over. TYB 2 Q1 is the strongest single question in the chapter: it delivers the integrated scenario stem the outline demanded instead of the acronym-matching exercise it forbade, and its answer genuinely requires all four chapters.

**One spacing caveat on TYB 2 Q1.** As the chapter's designated synthesis item it lands roughly four pages after §4's Fixed Point states the answer almost verbatim. That measures recency, not retrieval — the four-interface *shape* is fresh, so only the four *mappings* are being retrieved. The item is correctly built; it is placed where it is cheapest. If a later chapter's checkpoint can carry it (Ch 18 or Ch 19 would be ideal, and Ch 19 is the natural home), the same question would test what it was designed to test. Not a defect in this chapter — an opportunity flagged for the book-level pass.

**Practice questions — tagging is imprecise, substance is fine.**

Tagged: 7 of 21 (33.3%), above the 25% ceiling the outline set for practice items. But the outline also defines retrieval narrowly, and binds the drafting stage to that definition: *"A retrieval question is one whose **answer** lives in an earlier chapter."* Applying that rule:

| Item | Tag | Assessment |
|---|---|---|
| Q10 | `[retrieval: ch14]` | **Clean.** The `crds/` ordering rationale is Ch 14 §6's. |
| Q18 | `[retrieval: ch13]` | **Clean.** metrics-server and the Metrics API are Ch 13 §7's. |
| Q13 | `[retrieval: ch10]` | **Legitimate mixed.** Two of the three facts B requires are Ch 10 §2 and §7. |
| Q14 | `[retrieval: ch12]` | **Legitimate mixed.** The discriminating half — encryption at rest on etcd — is Ch 12 §4. |
| Q21 | `[retrieval: ch8]` | **Legitimate mixed.** The three-supported-minors half is Ch 8 §6. |
| Q19 | `[retrieval: ch7]` | **Over-tagged.** The answer — node autoscalers provision for unschedulable Pods — is this chapter's §7. Ch 7 supplies the setup, not the answer. |
| Q9 | `[retrieval]` | **Over-tagged and malformed.** The answer is §4's; Ch 6 supplies the CRD definition. Tag carries no chapter number. |

The outline's substantive floor — "at least five of the 21 must draw their answer from Ch 2/6/7/8/9/11/13/14" — is **met** (Q10, Q13, Q14, Q18, Q21). The problem is that the tag count overstates by two and one tag is unparseable, so any downstream stage counting `[retrieval: chN]` gets 7 where the honest number is 5. Status: **substantively compliant, mechanically imprecise.**

**Recommended fixes:** drop the tag on Q19; drop or fix the tag on Q9 (moot if Q9 is reallocated to §8 per the finding above); leave Q13, Q14 and Q21 tagged.

**Interleaving check** — the outline required at least six cross-domain stems. Five are delivered clean: Q13 (mesh + NetworkPolicy, D2.1), Q14 (mTLS + encryption at rest, D2.2), Q19 (node autoscaler + Pending Pod, D1.3), Q18 (HPA + missing metrics-server, D2.3), Q10 (CRDs + Helm `crds/`, D3.1). The sixth — "release cadence with a version-skew *symptom*" (D1.2) — is only half delivered: Q21 tests the cadence and the support window but never puts a skew symptom in front of the reader. Minor; a one-clause stem revision would close it.

## Coverage vs concepts

Against the 48 entries in the outline's `kb_tags.concepts`. `kb_tags.commands` is empty, correctly and by design (outline Open Question 9), so there is no command coverage to check.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| cloud-native-definition-v1-1 | yes (TYB1.1, P1, P2, P3) |
| cloud-native-characteristics | yes (TYB1.1, P1) |
| loose-coupling | weak — embedded in the characteristics stem only; never the discriminating fact |
| cncf-mission-and-vendor-neutrality | **NO** |
| cncf-project-maturity-levels | yes (TYB1.2, P4) |
| cncf-project-lifecycle | partial — TYB1.3 tests *where* criteria live; the process itself (5–7 adopter interviews, two-week public comment, two-thirds supermajority) is taught in detail and untested |
| cncf-governing-board | yes (TYB1.4, P5) |
| cncf-toc | yes (TYB1.4, P5) |
| cncf-tags | yes (P6) |
| end-user-technical-advisory-board | distractor-only (TYB1.4-C, P6-D) — never a correct answer |
| cncf-landscape | **NO** — six layered categories taught at length; appears only as TYB1.3 distractor B |
| microservices | yes (P7) |
| immutable-infrastructure | yes (TYB1.6) |
| declarative-api-as-a-characteristic | **NO** |
| extension-point | yes (TYB2.1, P9, P11) |
| four-pluggable-interfaces | yes (TYB2.1, P8, P9) |
| api-aggregation-layer | yes (TYB2.2, P11) |
| device-plugin | distractor-only (TYB2.2-C, P8-D) — GPU/NIC/FPGA and kubelet registration taught, never correct |
| service-mesh | yes (TYB2.4, P12, P13) |
| mesh-data-plane | yes (TYB2.4, P15) |
| mesh-control-plane | yes (TYB2.4) |
| envoy | yes (TYB2.5, P15) |
| sidecar-mode | yes (TYB2.5, P15) |
| ambient-mode | yes (TYB2.5, P15) |
| mutual-tls | yes (P13, P14) |
| zero-trust | **NO** — "never trust, always verify," trust-as-vulnerability, and lateral movement are taught at length and supply the chapter's closing epigraph; no question tests any of it |
| serverless | yes (TYB3.5, P17) |
| knative-serving | yes (TYB3.5, P16) |
| knative-eventing | yes (P16) |
| knative-functions | weak — named only inside a why-wrong rebuttal (P17-C) |
| scale-to-zero | weak — named inside P16's correct option, never the discriminating fact |
| horizontal-vs-vertical-autoscaling | yes (TYB3.2, P20) |
| vertical-pod-autoscaler | yes (TYB3.2, P20) |
| cluster-autoscaler | yes (P19, P20) |
| karpenter | yes (P19, P20) |
| keda-event-driven-autoscaling | yes (TYB3.1, P20) |
| node-autoscaling | yes (P19, P20) |
| kubernetes-sig | yes (TYB3.3, P21) |
| kubernetes-working-group | yes (TYB3.3) |
| kubernetes-committee | yes (TYB3.3) |
| steering-committee | yes (TYB3.3) |
| subproject | **NO** |
| contributor-ladder | **NO** — full four-rung table with specific numeric requirements; zero questions |
| kubernetes-enhancement-proposal | **NO** — purpose, when required, alpha→beta→stable; zero questions |
| sig-release-and-release-cadence | yes (TYB3.4, P21) |
| kubecon-cloudnativecon | **NO** |
| code-of-conduct | **NO** — the draft calls its scope statement "the examinable part"; zero questions |
| cncf-certification-ladder | **NO** — KCNA/CKA/CKAD/CKS/KCSA and the multiple-choice vs performance-based split; zero questions |

**Totals: 34 tested, 10 untested, 2 distractor-only, 4 weakly covered (loose-coupling, knative-functions, scale-to-zero, cncf-project-lifecycle).**

**Six of the ten untested concepts are D4.3 §8 material** — subproject, contributor ladder, KEPs, KubeCon, Code of Conduct, certification ladder. This is the same finding as the §8 practice shortfall seen from the other side, and it is the audit's most consequential coverage result: the chapter argues at length, in Why This Chapter Matters and again in §8's difficulty note, that this is the material technically strong candidates skip and forfeit points on — and then does not give them a single opportunity to confirm encoding on any of it.

**Recommended additions, in priority order.** Closing the §8 gap needs two items; three would be better and the budget supports it if Q9 and Q17 are reallocated:

1. **Contributor ladder** (replacing P Q9) — the two-sponsors-from-different-companies requirement, per the stem sketched above. Highest value: it is concrete, counterintuitive, source-backed, and it is the section's stated invitation.
2. **Code of Conduct scope** (replacing P Q17) — conduct outside project and event spaces when directed at a community participant. The draft itself flags this as examinable.
3. **KEPs or the certification ladder** — if a third slot opens. The certification ladder has a clean discriminator the chapter already frames as a mnemonic: KCNA is the only one of the four that is multiple-choice; CKA, CKAD and CKS are performance-based.

Two smaller additions worth considering if any slot frees up elsewhere:

4. **Zero trust** — "never trust, always verify" and trust-as-vulnerability. Currently the chapter's most heavily taught untested idea, and it closes the book's chapter on its own quotation.
5. **CNCF Landscape** — the layered categories, which §2 develops at length and then only uses as a wrong answer.
```

**Three things worth your attention before this goes to the revision stage:**

The B-bias is the headline. 30 of 37 correct answers are B, none are A or D, and Practice Q5–Q18 is fourteen consecutive Bs. It is entirely mechanical to fix and touches no prose — but it must be scripted, not hand-edited, or the relettering will drift out of sync with the why-wrong bullets.

The missing revision prompts are an unambiguous miss against an explicit outline requirement, not a judgment call. The Soundings has its rubric; the three checkpoints have nothing.

The §8 shortfall is the one that costs the reader points. The chapter argues twice that D4.3 is where strong candidates forfeit the cheapest marks, then ships one practice question for §8 against a budgeted three, leaving the contributor ladder, KEPs, the Code of Conduct and the certification ladder entirely untested. Q9 duplicates a checkpoint question almost verbatim, so the budget to fix this already exists inside the chapter.
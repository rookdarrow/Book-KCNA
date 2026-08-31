I read both binding contracts, the arc-outline block, B1's D4 entries, B4's budget, and verified every inbound pointer into Ch 17 by line number against chapters 01–16. **Seven of nine sections are pinned by number** — twenty-six published cross-bearings land here, more than any other chapter in the book. Only §6 and §9 are free. Four inbound pointers quote a B6 section title *verbatim*, which fixes those titles as well as their numbers. One inbound pointer contradicts two others (B6 Collision #2) and is carried to Open Questions rather than silently honored.

```
---
chapter: 17
chapter_type: "content"
title: "The Fleet and Its Charts"
subtitle: "Meshes, functions, autoscalers, and the foundation that keeps the map"
exam_domain: "Cloud Native Architecture (competencies: Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration)"
domain_weight_pct: 7
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE — UNCHANGED FROM B2/B3. Ten words exactly, at this stage's
#-- limit rather than over it, so no Ch 16-style substitution is needed.
#-- Spoiler check: "the foundation that keeps the map" names the CNCF and
#-- the Landscape, both of which are §2 subject matter the reader already
#-- half-owns from Ch 1. It does NOT name the chapter's synthesis (the
#-- shared shape of the four pluggable interfaces), which is what §9 is
#-- for. No shipped chapter quotes the subtitle, so it is free either way.

#-- EXAM_DOMAIN — ONE DOMAIN, TWO COMPETENCIES.
#-- D4 Cloud Native Architecture has three competencies. D4.1
#-- Observability is Ch 18's. This chapter carries the other two, and it
#-- is the only chapter in the book that carries two whole competencies.
#-- The house string form (ch-04/-09/-10/-11/-12/-13/-16) is one domain
#-- per chapter, preserved here; both competencies appear in
#-- kb_tags.objectives.
#--
#-- ⚠ THE IN-CHAPTER METADATA LINE MUST CARRY 12%, NOT 7%.
#-- 12% is the published weight of D4 [source: cncf-kcna-certification-page-
#-- 2026-08-23]. The 7% above is this book's AUTHORED allocation of that
#-- 12% between Ch 17 and Ch 18 (7 + 5). CNCF publishes four domain
#-- weights and no sub-competency weights — B1 gap G33, B2 disclosure #1.
#-- Do NOT present 7% as CNCF data. Ch 16's outline made the identical
#-- ruling and shipped Ch 16 honors it; match that treatment exactly.

#-- COMPLEXITY — "mixed", and the call is worth recording because a
#-- reader of this outline may expect "abstract". This chapter has almost
#-- no procedural surface (see kb_tags.commands, which is empty and
#-- correctly so), which argues for abstract. But the skill reserves
#-- "abstract" for material needing heavy scaffolding to build a model —
#-- security models, frameworks. B1's stated depth for D4 is "recall and
#-- recognition": lots of names, few mechanics, the highest
#-- breadth-to-depth ratio in the exam. Naming and placing is not
#-- abstraction. "mixed" is the honest tag, and it matters because the
#-- drafting stage will otherwise over-scaffold §2 and §8 — the two
#-- sections that need the LEAST scaffolding and the most memorable
#-- structure.

#-- PREREQ — heavy, and heavy in a shape unique to this chapter. Ch 13
#-- and Ch 16 are heavy because they APPLY prior material. This chapter is
#-- heavy because it COLLECTS it. Nine chapters feed it, and the arc
#-- outline sets retrieval at the 25% CEILING with six mandatory named
#-- anchors:
#--   Ch 2 §4 CRI + Ch 9 §1 CNI + Ch 11 §5 CSI + Ch 6 §8 CRDs -> §4, §9
#--        ** the four-way retrieval that IS the secondary Zenith **
#--   Ch 8 §6 version skew + three-supported-minors               -> §8
#--   Ch 7 §2 unschedulable Pods as Cluster Autoscaler's trigger  -> §7
#--   Ch 13 §7 metrics-server as the HPA's input                  -> §7
#--   Ch 10 §3 "object without its component" -> VPA, BY NAME     -> §7
#--   Ch 14 §6 CRDs shipped as chart content                      -> §4
#-- The first is not optional and is not a pointer. If the reader cannot
#-- produce all four interfaces unprompted, §9 has nothing to synthesize
#-- and degrades into a fifth list — which is the exact failure shipped
#-- Ch 2 §8 promised the reader would not happen ("meant to feel like
#-- recognition rather than a fourth list").

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "substantial" — 7
#-- points, two competencies, six arcs, the secondary Zenith. Planning
#-- signal only, NOT a target.
#--
#-- ⚠ SECTION NUMBERING IS THE MOST CONSTRAINED IN THE BOOK. Twenty-six
#-- published cross-bearings point here. TWENTY name a section by number,
#-- covering SEVEN of the nine sections:
#--   chapter-01:146  -> Ch 17 §1   the CNCF definition of cloud native
#--   chapter-01:374  -> Ch 17 §1   the definition and its characteristics
#--   chapter-01:535  -> Ch 17 §1   the definition and its characteristics
#--   chapter-03:350  -> Ch 17 §1   "the CNCF, its GOVERNANCE, and the
#--                                  cloud native definition"  ** CONFLICT,
#--                                  see Open Question 1 **
#--   chapter-01:144  -> Ch 17 §2   CNCF governance and the project lifecycle
#--   chapter-02:671  -> Ch 17 §2   CNCF governance and project maturity
#--   chapter-15:1215 -> Ch 17 §2   "sandbox, incubating, graduated, and
#--                                  who decides"  ** quotes the title **
#--   chapter-15:532  -> Ch 17 §3   "small pieces, replaced whole"
#--                                  ** quotes the title **
#--   chapter-02:600  -> Ch 17 §4   the four pluggable interfaces, collected
#--   chapter-02:914  -> Ch 17 §4   (same wording)
#--   chapter-09:391  -> Ch 17 §4   (same wording)
#--   chapter-10:959  -> Ch 17 §4   CRDs as one of the four
#--   chapter-10:1896 -> Ch 17 §4   (same wording) + the two-maps promise
#--   chapter-11:1101 -> Ch 17 §4   "every place Kubernetes lets you in"
#--                                  ** quotes the title **
#--   chapter-12:1605 -> Ch 17 §4   (same wording)
#--   chapter-14:1007 -> Ch 17 §4   the four pluggable interfaces, collected
#--   chapter-09:998  -> Ch 17 §5   sidecar or ambient interception
#--   chapter-10:394  -> Ch 17 §5   layer 7 for east-west
#--   chapter-10:570  -> Ch 17 §5   what a mesh adds inside the cluster
#--   chapter-10:1262 -> Ch 17 §5   service mesh, mTLS, what a mesh adds
#--   chapter-12:1048 -> Ch 17 §5   "a network that knows what it's
#--                                  carrying"  ** quotes the title **
#--   chapter-15:576  -> Ch 17 §5   (same wording)
#--   chapter-10:678  -> Ch 17 §7   VPA is an addon, not there by default
#--   chapter-10:1372 -> Ch 17 §7   the autoscaling landscape
#--   chapter-13:1332 -> Ch 17 §7   the autoscaling landscape
#--   chapter-08:865  -> Ch 17 §8   SIG Release, KEPs, how a release is made
#--   chapter-08:1009 -> Ch 17 §8   SIG Release and the release cycle
#--   chapter-13:1259 -> Ch 17 §8   SIG Release and the release cadence
#-- Seven more are unnumbered and pin by TOPIC only:
#--   chapter-01:182  -> Ch 17      the cloud native certification landscape
#--   chapter-01:466  -> Ch 17      one of three chapters this reader needs
#--   chapter-03:606  -> Ch 17      VPA is an addon, not shipped by default
#--   chapter-03:980  -> Ch 17      the control loop, named as a principle
#--   chapter-05:386  -> Ch 17      the mesh data plane
#--   chapter-05:969  -> Ch 17      autoscaling targets
#--   chapter-06:426  -> Ch 17      the autoscaling landscape
#--   chapter-06:1032 -> Ch 17      CRI/CNI/CSI/CRDs resolved into one story
#--   chapter-07:428  -> Ch 17      reacting to unschedulable Pods
#--   chapter-07:921  -> Ch 17      the cluster's extension points
#-- §1, §2, §3, §4, §5, §7 and §8 are FIXED, and four of their TITLES are
#-- fixed too because a shipped pointer quotes them word for word.
#-- §6 and §9 are free; §9 is structurally fixed as the Zenith.
#-- All twenty numbered pins match the B6 skeleton, except chapter-03:350.
#-- Verified 2026-08-31 against chapters 01-16.
sections:
  - name: "What \"Cloud Native\" Actually Names"
    objectives: ["D4.2"]
    requires_figure: true
    figure_anchor: "ch17-fig01-cloud-native-definition-characteristics"
    checkpoint_after: false

  - name: "Sandbox, Incubating, Graduated, and Who Decides"
    objectives: ["D4.3", "D4.2"]
    requires_figure: true
    figure_anchor: "ch17-fig05-cncf-maturity-levels"
    checkpoint_after: false

  - name: "Small Pieces, Replaced Whole"
    objectives: ["D4.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true

  - name: "Every Place Kubernetes Lets You In"
    objectives: ["D4.2"]
    requires_figure: true
    figure_anchor: "ch17-fig02-extension-points-map"
    checkpoint_after: false

  - name: "A Network That Knows What It's Carrying"
    objectives: ["D4.2"]
    requires_figure: true
    figure_anchor: "ch17-fig03-mesh-data-vs-control-plane"
    checkpoint_after: true

  - name: "Code Without a Server to Put It On"
    objectives: ["D4.2"]
    requires_figure: true
    figure_anchor: "ch17-fig07-scale-to-zero-and-the-knative-service"
    checkpoint_after: false

  - name: "Four Things That Scale"
    objectives: ["D4.2"]
    requires_figure: true
    figure_anchor: "ch17-fig04-autoscaler-landscape"
    checkpoint_after: false

  - name: "How the Project Actually Runs, and How You'd Join"
    objectives: ["D4.3"]
    requires_figure: true
    figure_anchor: "ch17-fig06-cncf-and-k8s-governance"
    checkpoint_after: true

  - name: "One Pluggability Story"
    objectives: ["D4.2"]
    requires_figure: true
    figure_anchor: "ch17-zenith-one-pluggability-story"
    checkpoint_after: false

#-- Skill Part 11: Soundings pre-chapter diagnostic ----------------------
#-- Content chapter, so 8. FOUR are decay probes whose repair is a named
#-- section. ONE is a generation-effect setup. ONE covers D4.3, which the
#-- arc outline requires explicitly ("D4.3 gets ... its own Soundings
#-- coverage inside this chapter") because B1 names it the competency
#-- technically-strong candidates most reliably under-study.
soundings_planned:
  question_count: 8
  topics:
    - "Which layer of the cluster each of CRI, CNI and CSI serves (Ch 2 §4, Ch 9 §1, Ch 11 §5) — decay probe"
    - "What the published definition of \"cloud native\" is actually about, if not \"runs in a public cloud\" (Ch 1, the plant)"
    - "How many minor releases the project supports at once (Ch 8 §6) — primary decay probe"
    - "What makes a container a sidecar, and what it shares with the container beside it (Ch 5 §1, §2)"
    - "What an HPA does on a cluster with no metrics-server installed (Ch 6 §2, Ch 13 §7) — decay probe"
    - "The phase of a Pod no node can satisfy, and what its existence states about the cluster (Ch 7 §2) — decay probe"
    - "What Kubernetes calls its primary durable topic-focused contributor group, and what it would call a group spanning several of them — D4.3 pre-test, general open-source knowledge"
    - "What protects the leg from Ingress to Pod once TLS has terminated at the edge (Ch 10 §2, Ch 12 §4) — generation-effect setup for §5"

#-- Skill Part 8: practice-question budget ------------------------------
#-- B4 allocated 8 / 10 / 21 = 39; the arc outline raised Bearings to
#-- 12-15 across three checkpoints. This outline sets 16, which is ONE
#-- above the arc band, for the arithmetic reason Ch 16 documented and
#-- which binds harder here: this chapter sits AT the 25% retrieval
#-- ceiling, and 16 is the smallest count that lets retrieval land at
#-- EXACTLY 25.0% across three checkpoints of >= 5. At 15 the ceiling
#-- lands on 3.75 and must be rounded past or under it; at 12 the three
#-- checkpoints fall below the skill's 5-question floor. New total 45.
question_budget:
  soundings: 8
  taking_your_bearings: 16             # across 3 checkpoints (6 + 5 + 5)
  practice_questions: 21
  total_this_chapter: 45

#-- Concept / objective / command tagging -------------------------------
#-- Per the Ch 13 AUTHOR-REVIEW housekeeping note carried forward by
#-- Ch 16: this list claims only what the chapter actually demonstrates.
#--
#-- ⚠ commands IS DELIBERATELY EMPTY, and this is the only content
#-- chapter in the book where that is correct. Ch 17 demonstrates no
#-- command surface: `kubectl scale` is Ch 6 §2's, `kubectl top` is
#-- Ch 13 §7's, and every autoscaler here is discussed as an object and a
#-- controller, not as a verb. Do not pad this list to make the chapter
#-- look like its neighbors, and do not let the drafting stage introduce
#-- a command demonstration to justify an entry.
kb_tags:
  objectives: ["D4.2", "D4.3"]
  concepts:
    - "cloud-native-definition-v1-1"
    - "cloud-native-characteristics"
    - "loose-coupling"
    - "cncf-mission-and-vendor-neutrality"
    - "cncf-project-maturity-levels"
    - "cncf-project-lifecycle"
    - "cncf-governing-board"
    - "cncf-toc"
    - "cncf-tags"
    - "end-user-technical-advisory-board"
    - "cncf-landscape"
    - "microservices"
    - "immutable-infrastructure"
    - "declarative-api-as-a-characteristic"
    - "extension-point"
    - "four-pluggable-interfaces"
    - "api-aggregation-layer"
    - "device-plugin"
    - "service-mesh"
    - "mesh-data-plane"
    - "mesh-control-plane"
    - "envoy"
    - "sidecar-mode"
    - "ambient-mode"
    - "mutual-tls"
    - "zero-trust"
    - "serverless"
    - "knative-serving"
    - "knative-eventing"
    - "knative-functions"
    - "scale-to-zero"
    - "horizontal-vs-vertical-autoscaling"
    - "vertical-pod-autoscaler"
    - "cluster-autoscaler"
    - "karpenter"
    - "keda-event-driven-autoscaling"
    - "node-autoscaling"
    - "kubernetes-sig"
    - "kubernetes-working-group"
    - "kubernetes-committee"
    - "steering-committee"
    - "subproject"
    - "contributor-ladder"
    - "kubernetes-enhancement-proposal"
    - "sig-release-and-release-cadence"
    - "kubecon-cloudnativecon"
    - "code-of-conduct"
    - "cncf-certification-ladder"
  commands: []

figures_planned:
  - "ch17-fig01-cloud-native-definition-characteristics"
  - "ch17-fig05-cncf-maturity-levels"
  - "ch17-fig02-extension-points-map"
  - "ch17-fig03-mesh-data-vs-control-plane"
  - "ch17-fig07-scale-to-zero-and-the-knative-service"
  - "ch17-fig04-autoscaler-landscape"
  - "ch17-fig06-cncf-and-k8s-governance"
  - "ch17-zenith-one-pluggability-story"
---
```

# Chapter 17 Outline — The Fleet and Its Charts

## Chapter-type note (read first)

`content`. Full structural contract applies: witty subtitle, Attention Budget, epigraph, 🧭 Soundings, Why This Chapter Matters, What You'll Learn, ≥2 ☆ Taking Your Bearings, Exam Alert, Practice Questions, Chapter Summary, The Voyage Ahead.

**Heading form:** `## <difficulty> §N — Title`, the Ch 5–8 majority form B6 recommends for Ch 9–19 and that shipped Ch 9–16 use. **The closing section takes `☀️` in place of a difficulty glyph**, per B6 recommendation #4.

**Position note.** First chapter of Part V. Its Why-This-Chapter-Matters receives a handoff that shipped Ch 16 has already written: *"Part V steps back from the failing workload in front of you to the ecosystem the workload lives in ... Chapter 17 finally answers the question Chapter 1 planted and left standing on purpose."* Two promises, both due in §1 and §4.

**Ordinal rule — book-level convention, ratified at the Ch 8 gate.** Name the pattern; never assert a running ordinal. The one sanctioned exception is a closed set the reader can see in front of them, and **the four pluggable interfaces are exactly that set** — so §4 and §9 may count to four and must not count to anything else. Specifically: do **not** re-open the Ch 9 §8 "second instance" versus Ch 10/11 "three of four" arithmetic. Shipped Ch 10 already reconciled it in a half-clause; this chapter inherits a reconciled reader.

---

## 1. Why This Chapter Matters

Two chapters have just handed the reader a boundary and a method. This one changes altitude instead of subject. Everything from Chapter 2 forward has been *inside* one cluster — its components, its objects, its traffic, its storage, its failures. This chapter is about the thing the cluster is an instance of, and it opens by paying a debt that has been outstanding since page one.

The curiosity gap was opened deliberately in Chapter 1 and left standing for four hundred pages. Chapter 1 named the phrase *cloud native*, said the near-universal reading — "it runs in a public cloud" — is not what it means, declined to define it, and pointed here three separate times. That is the longest-running open loop in the book, and §1 closes it with the actual published document rather than a paraphrase. But the chapter's real withheld question is larger and quieter, and it was planted in Chapter 2: *why does Kubernetes keep doing the same thing?* Four times now the reader has watched Kubernetes define an interface and hand the implementation to somebody else — runtimes, networking, storage, object types — and each time it looked like a local design choice about that one problem. §4 puts the four side by side and §9 says what they are evidence of. Shipped Chapter 2 §8 promised the reader this would feel like recognition rather than a fourth list. That promise is this chapter's to keep, and it is the only way to keep it: the reader must arrive already holding all four.

The identity frame is a change in standing. Up to here the reader has been a competent operator of somebody else's software. This chapter positions them inside the community that produces it — a community with a published definition of its own terms, a graduation ladder its projects climb, a technical committee that decides what belongs, a contributor ladder anyone reading this could start climbing on a Tuesday afternoon, and a release train that explains why the version numbers behave the way Chapter 8 said they do. That last connection is the chapter's quietest payoff: three minor releases a year and three supported minor versions are not two facts, they are one fact stated twice, and a reader who sees that will never lose either half again.

The stakes are unusually specific and worth stating plainly rather than dramatizing. D4 is the smallest domain at 12%, and it has the highest ratio of names to mechanics on the exam — which makes it the cheapest points available and the most commonly forfeited. Shipped Chapter 1 already told one class of reader this to their face: *"Chapter 17's community and collaboration material is, in my experience, what technically strong candidates skip most often. It looks like soft content next to the technical chapters."* §2 and §8 exist because of that sentence, and they carry ⚪ Foundation difficulty markers for the same reason — not because the material is easy, but because the signal a reader scanning the left margin needs to receive is *everyone needs this*, not *optional depth*.

**Voice guardrail.** Skill Part 14, subject dignity. Wry beats stay oriented at the practitioner's experience — the study guide still teaching a blueprint that changed, the acronym that turns out to be the same acronym at a different layer, the candidate who can recite the scheduler's scoring phase and cannot name a single CNCF body. Nothing wry at the expense of contributors, maintainers, vendors, or the governance process itself; this is a chapter about people doing unpaid organizational work, and the register is respect with a light touch. Do not editorialize on foundation politics, corporate sponsorship, or which projects deserved graduation.

---

## 2. What You'll Learn

- **Quote** the CNCF's published definition of *cloud native* and name the five characteristics it attaches to loosely coupled systems
- **Place** any CNCF project on the maturity ladder — and, more usefully, say who decides and where the criteria live
- **State** the shape that CRI, CNI, CSI and CRDs have in common, without being given the four names first
- **Distinguish** a service mesh's data plane from its control plane, and both from the control plane you have been reading about since Chapter 3
- **Say** which axis each autoscaler moves — replicas, resources, or nodes — and which of them the cluster does not ship
- **Name** the difference between a SIG, a Working Group and a Committee, and explain why three releases a year and three supported versions are the same fact

*You'll also stop treating the ecosystem as trivia around the edges of the technology, which is the habit that costs well-prepared candidates the most points on the smallest domain.*

---

## 3. Soundings plan — 8 questions

Content chapter, so 8. Every question is answerable from Chapters 1–16 or from general professional knowledge, and none can be answered only from this chapter. Four are **decay probes** whose repair is a named section, so the reader's own wrong answer becomes the argument for that section. One is a **generation-effect setup**. One covers **D4.3**, which the arc outline requires by name.

| # | Topic | Tests | Why it earns its place as a pre-test |
|---|---|---|---|
| 1 | For each of CRI, CNI and CSI: which layer of the cluster does it serve? | Ch 2 §4, Ch 9 §1, Ch 11 §5 | **Primary decay probe, and the most important of the eight.** The three were taught in three different Parts, hundreds of pages apart. If the reader cannot produce the mapping, §4 must re-teach three chapters and §9 has nothing to synthesize. Asks for the *mapping*, deliberately not for what they have in common — see the spoiler check. |
| 2 | Chapter 1 said the common reading of *cloud native* — "it runs in a public cloud" — is not what the term means. In one sentence, and without looking: what do you think the published definition is actually about? | Ch 1 (the plant) | Textbook pretesting on the book's longest-running open loop. Open-ended by design; almost every reader will be partly wrong, and being wrong here is what makes §1's opening sentence land instead of skim. |
| 3 | How many minor releases does the Kubernetes project support at any one time? | Ch 8 §6 | **Second decay probe, and B3 designed it.** Ch 8 §6 is flagged as the densest pure-recall material in the book, taught at the 40% mark. §8 pairs it with the cadence so the two numbers explain each other. Tests only the support-window half — the cadence half is §8's to supply. |
| 4 | What makes a container a *sidecar*, and what does it share with the container beside it? | Ch 5 §1, §2 | Ch 5:386 planted this pointer explicitly and said "here, the word is enough." §5 spends it. Tests the Pod-level model the mesh data plane is built on, without naming a mesh. |
| 5 | An HPA is created on a cluster where metrics-server was never installed. What happens? | Ch 6 §2, Ch 13 §7 | **Third decay probe.** Shipped Ch 13:1332 taught exactly this as an instance of the absent-component pattern. §7 needs the reader holding it, because §7's VPA fact is the *same* pattern one layer over and lands as recognition only if this one is intact. |
| 6 | A Pod that no node can satisfy: what phase is it in, and what does its continued existence state about the cluster? | Ch 7 §2 | **Fourth decay probe.** Ch 7:428 planted the second half word for word — "a standing, machine-readable statement that the cluster is short of somewhere to put work. Something could be watching for exactly that" — and pointed here. §7 names the something. The stem names no autoscaler. |
| 7 | Kubernetes organizes contributors into named groups. What would you guess the primary, durable, topic-focused unit is called — and what would you call a group formed to work *across* several of them? | General open-source professional knowledge | **The D4.3 pre-test the arc outline requires.** Fair as a pre-test because "SIG" is common industry vocabulary and the second half is a reasonable inference. Most readers get half. That half-score is the argument for §8, delivered by the reader to themselves. |
| 8 | TLS terminates at the Ingress. What protects the leg from there to the Pod? | Ch 10 §2, Ch 12 §4 | **Generation-effect setup for §5.** The correct answer is "nothing, by default," and shipped Ch 10 said so twice (10:570, 10:1262) while explicitly refusing to name the remedy. This produces §5's problem statement in the reader's own words without mentioning mTLS, zero trust, or a mesh. |

### FIXED-POINT SPOILER CHECK

The chapter's candidate Fixed Points, and confirmation that no Soundings question states one:

| Candidate ★ Fixed Point | Spoiled by any Soundings question? |
|---|---|
| Cloud native is characterized by loosely coupled systems that interoperate **securely, resiliently, manageably, sustainably, and observably**. | **No.** Q2 asks the reader what they *think* it is about and stops. No stem or answer supplies a characteristic. Drafting must not let Q2's rationale line enumerate the five — the rationale should say only that the reader's own answer will be measured against §1's opening quotation. |
| **Sandbox → Incubating → Graduated**, in that order, and the criteria live in the TOC's project-lifecycle documentation, not the projects page. | **No.** No stem mentions maturity, graduation, or a project roster. Deliberately: Ch 15:1215 already gave this reader the word *graduated* and its meaning, so a stem naming even one level would hand over the structure. |
| At every one of the four pluggable interfaces, Kubernetes defines an interface and hands the implementation to somebody else. | **Partly at risk, and permitted — the same watched edge Ch 16 accepted.** Q1 asks the reader to place three of the four by *layer*. It does not ask what they have in common, does not mention CRDs, and does not use the words *interface*, *pluggable*, *extension* or *implementation* in either the stem or the answer. The shape is what §4 sells and §9 pays off; the mapping is a Chapter 2/9/11 prior. **Drafting constraint: Q1's answer text is a three-row table of acronym → layer, nothing more.** |
| A service mesh delivers zero-trust security, observability and traffic management **without application code changes**. | **No.** Q8 establishes the *gap* (the unencrypted leg) and stops. No stem mentions a mesh, a proxy, or code changes. |
| A mesh's **data plane** is the proxies; its **control plane** configures them — and it is not the control plane from Chapter 3. | **No.** Neither phrase appears in any stem. Q4 tests the Pod-level sidecar model, which is the vehicle, not the distinction. |
| Serverless workloads are still containers in Pods. The serverless property is the lifecycle, not the absence of containers. | **No.** Serverless, Knative and scale-to-zero appear in no stem. §6 is the one section with zero Soundings exposure, which is correct — it is also the section with no inbound cross-bearing, so nothing in the book has pre-committed to it. |
| Horizontal changes the **number** of replicas; vertical changes the **resources** of each; node autoscaling changes the **node pool**. HPA ships; VPA does not. | **No.** Q5 tests the *HPA/metrics-server* instance, which is shipped Ch 13 material. **Drafting constraint: Q5's answer text must not mention VPA.** The VPA fact is §7's, it is the payoff of a pointer laid in Ch 3:606 and repeated in Ch 10:678, and pre-empting it in a Soundings answer would spend it. |
| A **SIG** is durable and topic-scoped; a **Working Group** crosses SIG lines and is short-lived; a **Committee** has closed membership. | **Partly at risk, and this one is deliberate.** Q7 asks the reader to *guess* the first two, which is precisely the pretesting effect B1's under-study warning calls for. It does not mention Committees, closed membership, the Steering Committee, or CNCF TAGs — so the trap that actually costs points (#109, #112) is untouched. |
| Three minor releases a year and three supported minor versions are one fact stated twice. | **No.** Q3 asks only the support-window half. The cadence half appears in no stem, and shipped Ch 13:1255 records that the cadence claim was deliberately *removed* from Ch 13 for want of a tag — so the reader has not met it. |

Clean, with two watched edges (Q1, Q5), each carrying an explicit drafting constraint above.

**Rubric branches (all three mandatory):** 6+ → skim, but read §2 and §8 properly; they are the sections a strong technical score predicts nothing about. 3–5 → normal pace; this chapter is calibrated for you. 0–2 → **re-read Ch 2 §8 and Ch 11 §5 before starting**, not alongside — name the sections, not the chapters. Those two are where the four-interface thread was last picked up, and §4 is unreadable without it.

---

## 4. Section plan

### `## ⚪ §1 — What "Cloud Native" Actually Names`

Closes the book's longest-running open loop. Presents the **CNCF Cloud Native Definition v1.1 verbatim** — the actual document, not a paraphrase — then walks its parts: the practices clause (develop, build and deploy workloads across public, private and hybrid environments, at scale, programmatically and repeatably), the **five characteristics** attached to loosely coupled systems (secure, resilient, manageable, sustainable, observable), the **non-exhaustive** technology list, and the payoff clause about high-impact changes made frequently and predictably with minimal toil. Also owns **what the CNCF is as an institution** and its mission of vendor-neutral, open-source stewardship — distinct from the Ch 1 sense, which was CNCF-as-exam-sponsor.

The section's most useful move is negative and the reader has been primed for it since Chapter 1: *cloud native* is not a synonym for *public cloud*. The definition says "public, private, hybrid" in its first sentence, and the reader who notices that has retired the misconception without being lectured.

- **Objectives:** D4.2
- **Introduces:** cloud-native-definition-v1-1; cloud-native-characteristics; loose-coupling; cncf-mission-and-vendor-neutrality
- **Figure:** `ch17-fig01-cloud-native-definition-characteristics`
- **Cross-bearings out:** `Ch 2 §1 — what a container actually is`; `Ch 4 §1 — you file a declaration`; `Ch 17 §3 — small pieces, replaced whole`
- **Guardrail — the definition is a quotation, not a summary.** Three shipped pointers promise this reader "the actual document, unabridged, each characteristic examined" (Ch 1:374). Reproduce it under a `[source: cncf-cloud-native-definition-2026-08-23]` tag and then examine it. A paraphrase breaks a promise made in three places.
- **Guardrail — trap #114.** The technology list is explicitly non-exhaustive in the source. Say so in the same breath as the list, because the natural reader error is to treat seven items as a closed set — and this chapter spends §4 teaching a set that genuinely *is* closed, so the contrast needs marking.
- **Ledger guardrail:** *cloud native* is written **unhyphenated** everywhere, including attributively. Sixteen hyphenated instances survive in shipped Ch 1–8 (B7 ⚑8); this chapter quotes the CNCF's own unhyphenated wording and must not add to the drift.
- **Checkpoint:** none

### `## ⚪ §2 — Sandbox, Incubating, Graduated, and Who Decides`

Two shipped pointers quote this title word for word, so the title is fixed. Owns the **maturity levels in order** with what each one asserts (Sandbox: experimental, bleeding edge; Incubating: production use by a small number of users with a healthy contributor pool; Graduated: stable, widely adopted, production-ready), the **project lifecycle** as the process that moves a project between them, **where the criteria live** (the TOC's project-lifecycle documentation, not the projects page — trap #98), and **CNCF governance**: the Governing Board sets the scope, the TOC approves projects within it and owns technical vision and architecture, TAGs are TOC-aligned groups by technical area, and the End User Technical Advisory Board feeds requirements in. Closes with the **CNCF Landscape** as the map of the terrain, including its layered categories and the trail-map framing.

- **Objectives:** D4.3 (governance, lifecycle), D4.2 (Landscape, ecosystem)
- **Introduces:** cncf-project-maturity-levels; cncf-project-lifecycle; cncf-governing-board; cncf-toc; cncf-tags; end-user-technical-advisory-board; cncf-landscape
- **Figure:** `ch17-fig05-cncf-maturity-levels`
- **Cross-bearings out:** `Ch 2 §5 — the Open Container Initiative`; `Ch 15 §6 — the other agent`; `Ch 17 §8 — how the project actually runs`
- **Guardrail — hard, and B3 states it as an exclusion.** **Do not build retrieval on the graduated-project roster.** The roster changes between this book's printing and the reader's exam. Name at most six graduated projects the reader has already met by name in this book, tag them, state the snapshot date explicitly, and tell the reader in as many words not to memorize the list — the *levels* are the durable fact. Shipped Ch 15:1215 already modeled this exact treatment; match it.
- **Guardrail — trap #111, and it is live.** The TAG list was **restructured in 2025**. Current: Developer Experience, Infrastructure, Operational Resilience, Security and Compliance, Workloads Foundation. The pre-2025 list (App Delivery, Contributor Strategy, Environmental Sustainability, Network, Observability, Runtime, Security, Storage) appears throughout older study material, which means a reader may arrive holding it. Name both, mark which is current, and date the claim.
- **Difficulty note:** ⚪ is a deliberate signal, not an assessment of ease. This is a section a technically-strong reader will be tempted to skim, and the left-margin glyph is the cheapest available intervention.
- **Checkpoint:** none

### `## 🔵 §3 — Small Pieces, Replaced Whole`

Ch 15:532 quotes this title verbatim, so it is fixed. Owns **microservices** (loosely coupled, distributed, elastic services, each independently deployable), **immutable infrastructure** (replaced rather than modified in place), and **declarative APIs** as a named cloud native characteristic — and, more importantly, the argument that these three are not a list but a mutually reinforcing set: you can only replace a piece whole if it is small and independently deployable, and you can only do that safely if the thing you replace it with is described rather than commanded.

Deliberately the shortest content section in the chapter. Everything it names is *owned* elsewhere in substance — the declarative model at Ch 4 §1, image immutability at Ch 2 §2, loose coupling at §1 above — and this section owns only the framing that connects them.

- **Objectives:** D4.2
- **Introduces:** microservices; immutable-infrastructure; declarative-api-as-a-characteristic
- **Figure:** none. Every candidate figure here restates one that Ch 2 §1–§2 or Ch 4 §1 already owns, and Part 18.4's coherence principle forbids a visual that adds nothing. A monolith-versus-microservices diagram in particular would be the most generic figure in the book.
- **Cross-bearings out:** `Ch 2 §2 — what's inside an image`; `Ch 4 §1 — you file a declaration`; `Ch 5 §4 — scheduled once, replaced never`; `Ch 15 §1 — twelve factors`
- **Ledger guardrail:** **immutable infrastructure** is always the full two-word phrase, and this section **back-bears** to Ch 2 §2's image immutability rather than re-deriving it. Two different immutabilities, one sanctioned surface form each (B7 Canonical forms).
- **Guardrail — do not re-teach twelve-factor.** Ch 15:532 promises the reader that "several of them are these factors under newer names." Deliver that as a sentence of recognition with a pointer, not as a second pass through Chapter 15's material.
- **Checkpoint:** **☆ TYB 1** falls here.

### `## 🔵 §4 — Every Place Kubernetes Lets You In`

Two shipped pointers quote this title verbatim; eight point at this section by number. **The most cross-referenced section in the book.** Owns the collection of **the four pluggable interfaces** — CRI (Ch 2 §4), CNI (Ch 9 §1), CSI (Ch 11 §5), CRDs and the operator pattern (Ch 6 §8) — plus the wider documented extension surface: API aggregation, admission webhooks (Ch 8 §2), device plugins, and scheduler plugins (Ch 7 §6). **This section collects. It does not redefine.** If drafting finds itself explaining what CSI *is*, it has crossed a line six chapters back.

Two obligations are load-bearing and both were created by shipped text:

**The two maps, side by side.** Ch 10:1896 made the reader an explicit promise: *"The four pluggable interfaces* is this book's phrase and this book's grouping. The documentation's own map is larger than ours and cut differently: six extension points, five plugin types under infrastructure alone, and custom resources filed under a different heading entirely. Chapter 17 sets both maps side by side." That is a delivery obligation, not a nicety. The book's four go in the figure; the documentation's six extension points go in a table beside it, tagged. What makes our four a set is a *judgment* — at each of them Kubernetes defines an interface and hands the implementation to somebody else — and the section must say the judgment is ours while the four interfaces are each sourced where the reader met them.

**The fourth interface's two names.** B6 records the collision and the ruling. Shipped Ch 2 §4 and §8 call the set "CRI, CNI, CSI and **API extensions**"; the B7 ledger, shipped Ch 6 §8, Ch 10 and Ch 11 §5 all call it "**CRDs**." Three sources to one, so **CRDs is canonical** and §4 names CRDs. Ch 2:600 already links its "API extensions" slot to `Ch 6 §8 — CRDs`, so the two forms are reconciled in shipped text and neither is wrong. §4 may note in one clause that the wider surface is sometimes called API extensions — which is also true, and is exactly why the table beside the figure lists aggregation, webhooks, device plugins and scheduler plugins.

- **Objectives:** D4.2
- **Introduces:** extension-point; four-pluggable-interfaces; api-aggregation-layer; device-plugin
- **Figure:** `ch17-fig02-extension-points-map`
- **Cross-bearings out:** `Ch 2 §4 — the container runtime interface`; `Ch 6 §8 — the control loop, extended`; `Ch 9 §1 — four rules and a plugin`; `Ch 11 §5 — who actually provides the storage`; `Ch 8 §2 — three gates and a logbook`; `Ch 7 §6 — overruling the scheduler, and replacing it`; `Ch 14 §6 — which one, when`; `Ch 12 §8 — rules that watch`
- **Guardrail — the ordinal rule.** Count to four, because four is a closed set the reader can see. Assert no other running count, and do not re-open Ch 9 §8's "second instance" versus Ch 10/11's "three of four." Shipped Ch 10 reconciled it; the reader arrives reconciled.
- **Guardrail — altitude.** §4 lays the four out and names the shape. §9 says what the shape means. If §4 delivers the philosophical claim, §9 has nothing left and the chapter's Zenith collapses into a summary. **§4 shows; §9 argues.**
- **Checkpoint:** none

### `## 🟡 §5 — A Network That Knows What It's Carrying`

Two shipped pointers quote this title verbatim; six point here. Owns **service mesh**: the definition (an infrastructure layer delivering zero-trust security, observability and advanced traffic management **without application code changes**), the **data plane / control plane** split, **Envoy** as the proxy both Istio data-plane modes use, **sidecar mode** versus **ambient mode**, **mTLS** and **zero trust**, and mesh-generated telemetry. Also owns the negative boundary the reader has been walking toward since Chapter 10: what a mesh adds over Service (Ch 9) plus NetworkPolicy (Ch 10 §6), and specifically that the Ingress-to-Pod leg NetworkPolicy cannot encrypt is the leg a mesh does.

This section carries the book's single most dangerous vocabulary collision, and it is not an accident of naming — the two control planes genuinely do the same *kind* of job at different layers, which is why the collision is worth teaching rather than merely warning about.

- **Objectives:** D4.2
- **Introduces:** service-mesh; mesh-data-plane; mesh-control-plane; envoy; sidecar-mode; ambient-mode; mutual-tls; zero-trust
- **Figure:** `ch17-fig03-mesh-data-vs-control-plane`
- **Cross-bearings out:** `Ch 3 §2 — the control plane`; `Ch 5 §2 — more than one container aboard`; `Ch 9 §6 — the component that makes it real`; `Ch 10 §6 — allowing, never denying`; `Ch 10 §7 — what NetworkPolicy cannot do`; `Ch 12 §4 — secrets are not encrypted`; `Ch 15 §2 — ways to replace what's running`
- **Ledger guardrail — mandatory, and the chapter fails without it.** Sense B is always written **"the mesh's control plane"** or **"the service mesh control plane"** on first use, and the section must state in one clause that this is a *different* control plane from Ch 3 §2's. Bare "control plane" always means the cluster's. Trap #101 is `[source]`-backed and this is where it is either defused or manufactured.
- **Guardrail — trap #102.** Do not write "a service mesh means sidecars." Istio supports both sidecar and ambient modes and both use Envoy. Ch 5:386 promised this reader they would "meet the sidecar again in Chapter 17"; deliver the promise and then complicate it.
- **Guardrail — scope.** This is an associate exam. Teach what a mesh *is* and what it *buys*. Do not teach VirtualService, DestinationRule, Gateway resources, or Istio configuration. If a paragraph names an Istio CRD, it has left the tier.
- **Checkpoint:** **☆ TYB 2** falls here.

### `## 🔵 §6 — Code Without a Server to Put It On`

The only section with no inbound cross-bearing, and therefore the only one free to be shaped entirely by its material. Owns **serverless**, **Knative** and its three components (**Serving** — the HTTP-triggered autoscaling container runtime with **scale to zero**; **Eventing** — CloudEvents-over-HTTP asynchronous routing enabling loose coupling between producers and consumers; **Functions** — the simplified stateless-function experience built on the other two), and how a Knative Service relates to the Deployment the reader already knows.

The section's whole job is one correction. "Serverless" sounds like the absence of the thing this book has spent sixteen chapters on, and it is not: Knative builds on the Pod abstraction and is implemented as CRDs. The serverless property is a *lifecycle* — request-driven, scaled to zero when idle — not the absence of containers or servers.

- **Objectives:** D4.2
- **Introduces:** serverless; knative-serving; knative-eventing; knative-functions; scale-to-zero
- **Figure:** `ch17-fig07-scale-to-zero-and-the-knative-service` — **new, not in the arc stub list.** Justified: this is the section's only Fixed Point and it is a *lifecycle* claim, which is the one thing prose is worst at and a diagram is best at. It also kills trap #84 visually by showing containers in Pods at both ends of the cycle.
- **Cross-bearings out:** `Ch 6 §1 — the resource that holds the intent`; `Ch 6 §8 — the control loop, extended`; `Ch 5 §1 — the Pod as the unit of scheduling`; `Ch 17 §7 — four things that scale`
- **Ledger guardrail:** a **Knative Service** is always written in full, never bare "Service." Ch 9 §2 owns the Kubernetes Service and the two are one paragraph apart in the reader's memory (B7 Canonical forms).
- **Guardrail — trap #83.** Serving and Eventing answer different questions: synchronous HTTP with autoscaling versus asynchronous event routing. A reader who can only say "Knative does serverless" will lose the item. One clean sentence each, contrasted.
- **Checkpoint:** none

### `## 🔵 §7 — Four Things That Scale`

Three shipped pointers land here by number and three more by topic. Owns **the autoscaling landscape**: which axis each named autoscaler moves. The HPA *concept* is Ch 6 §2's one-sentence treatment and this section completes it rather than restating it.

**On the title, so drafting does not contradict it.** Four autoscalers, three axes. HPA moves the **replica count** on observed utilization. VPA moves the **resources of each replica**. Cluster Autoscaler — and Karpenter as a second implementation of the same idea — move the **node pool**. KEDA moves the replica count like the HPA does, but on an **external event** such as queue depth rather than on utilization, with schedule-based scaling via its Cron scaler. That fourth row shares an axis with the first and that is not a flaw in the taxonomy: it is trap #107 rendered structurally, and the section should say so rather than smooth it over. Cluster Proportional Autoscaler gets one clause as a completeness note and is not graded.

Three retrieval anchors converge here and each is a payoff of a pointer laid chapters ago:

- **VPA is an add-on, not shipped by default** — retrieved **by name** as the absent-component pattern Ch 3 §4's Worth Securing box christened and Ch 10 §3 formalized. Ch 3:606 and Ch 10:678 both pointed here for it. Name the pattern, do not re-derive it.
- **metrics-server is what an HPA reads** — Ch 13 §7 owns the pipeline; Ch 13:1332 pointed here.
- **An unschedulable Pod is what a Cluster Autoscaler watches for** — Ch 7:428 planted the observation and withheld the answer. This is the second half of that sentence.

- **Objectives:** D4.2
- **Introduces:** horizontal-vs-vertical-autoscaling; vertical-pod-autoscaler; cluster-autoscaler; karpenter; keda-event-driven-autoscaling; node-autoscaling
- **Figure:** `ch17-fig04-autoscaler-landscape`
- **Cross-bearings out:** `Ch 5 §8 — what a Pod is owed`; `Ch 6 §2 — a loop you can watch working`; `Ch 7 §2 — what makes a node feasible`; `Ch 10 §3 — the object is not the implementation`; `Ch 13 §7 — numbers nobody collects by default`; `Ch 18 §3 — utilization relative to requests`
- **Guardrail — trap #105, and it is a dated claim.** In-place Pod vertical scaling is stable as of a stated Kubernetes version, *and VPA does not yet support it directly*. Both halves, one source tag, one version number. Do not write "VPA now resizes in place."
- **Guardrail — Karpenter's affiliation.** The cached source names Karpenter only as a node autoscaler alongside Cluster Autoscaler. **Do not assert a CNCF maturity level for it.** KEDA and Knative are stated as graduated in the sources; Karpenter is not. See Open Question 5.
- **Checkpoint:** none

### `## ⚪ §8 — How the Project Actually Runs, and How You'd Join`

Three shipped pointers land here by number, all three for SIG Release and the cadence. Owns **Kubernetes governance** — the four community principles (open; welcoming and respectful; transparent and accessible; merit), **SIGs** as the primary durable unit with their vertical / horizontal / project-support orientations, chairs and subprojects, **Working Groups** as short-lived and cross-SIG, **Committees** as closed-membership bodies formed by Steering for topics requiring discretion, and the **Steering Committee** holding overall governance. Then the participation half: the **contributor ladder** (member, reviewer, approver), **KEPs** as how a change becomes a change, **SIG Release** and the **release cadence**, **KubeCon + CloudNativeCon**, Cloud Native Community Groups and Ambassadors, LFX mentorship, and the **Code of Conduct**. Closes with the **CNCF certification ladder** — KCNA as the pre-professional credential that grounds CKA, CKAD and CKS — which Ch 1:182 deferred here by name.

**The chapter's quietest Fixed Point lives here.** Three minor releases a year, roughly every fifteen weeks, and three supported minor versions giving roughly a year of patch support are *one fact stated twice*. Chapter 8 gave the reader the support window and warned the trio of numbers was the most forgettable material in the book. Chapter 13 wanted the cadence, found no tag for it, and removed the clause rather than ship it from memory (recorded at chapter-13:1255). This section is where both halves finally sit in one paragraph with one tag, and Ch 8:865 and Ch 8:1009 have already told the reader to expect exactly that.

- **Objectives:** D4.3
- **Introduces:** kubernetes-sig; kubernetes-working-group; kubernetes-committee; steering-committee; subproject; contributor-ladder; kubernetes-enhancement-proposal; sig-release-and-release-cadence; kubecon-cloudnativecon; code-of-conduct; cncf-certification-ladder
- **Figure:** `ch17-fig06-cncf-and-k8s-governance`
- **Cross-bearings out:** `Ch 8 §6 — versions that are allowed to disagree`; `Ch 13 §6 — versions that don't agree`; `Ch 17 §2 — sandbox, incubating, graduated, and who decides`; `Ch 2 §5 — the Open Container Initiative`
- **Guardrail — traps #109 and #112, in that order.** Committees are the one community group that is *not* open, and that asymmetry is the whole item. CNCF **TAGs** and Kubernetes **SIGs** are different organizations at different scopes with similar-sounding functions — but #112 is `[inferred]`, not `[source]`, so it may be described as *easy to confuse* and **never** as *frequently tested* (Ethical Guardrail #8). The figure carries this contrast; the prose names it once.
- **Difficulty note:** ⚪, same signaling rationale as §2, and doubly load-bearing here because shipped Ch 1:466 told this reader in as many words that this is the material they skip.
- **Guardrail — register.** This is a section about volunteers doing organizational work. Warm, specific, non-cynical. The "how you'd join" half is a genuine invitation and should read as one; it is also, incidentally, the most memorable possible frame for material that would otherwise be an org chart.
- **Checkpoint:** **☆ TYB 3** falls here.

### `## ☀️ §9 — One Pluggability Story`

**SECONDARY ZENITH.** Owns no new material. §4 laid four interfaces side by side and named the shape; this section says what having that shape *means* — that Kubernetes is not a system that happens to be extensible in four places, but a system built on the premise that it should not be the one implementing the parts that vary. Back-bears explicitly to all four interface chapters and to the Ch 2 §8 promise that this would feel like recognition rather than a fourth list.

- **Objectives:** D4.2
- **Figure:** `ch17-zenith-one-pluggability-story`
- **Cross-bearings out:** `Ch 2 §8 — the crate, not the cargo`; `Ch 6 §9 — nobody sails one pod`; `Ch 9 §8 — a query with a name`; `Ch 11 §7 — outliving the pod that asked`
- **Guardrail — do not out-stage the primary Zenith.** Ch 15 §7 is the book's primary: the control loop pointed at a repository. Shipped Ch 6 closes by telling the reader they have seen the loop twice and "the third time is the one that matters," which is a promissory note payable at Ch 15 §7 and at nowhere else. This chapter's Zenith is about **pluggability**, a different thread entirely, so there is no collision — but the register must stay one notch below Ch 15 §7's. Do not reach for the control loop here to make the moment bigger.
- **Guardrail — the two-altitudes risk.** §4 and §9 are the same synthesis at two heights, which is exactly the shape that reads as repetition if the split is sloppy. The discipline: §4 is a **map** and answers *where*; §9 is a **claim** and answers *so what*. §9 should be short. A long Zenith is a Zenith that did not land.
- **Checkpoint:** none

---

## 5. ☆ Taking Your Bearings checkpoints

Three checkpoints, 16 questions, **4 retrieval questions = exactly 25.0%**, the arc outline's ceiling. See the frontmatter note for why 16 rather than the arc's 12–15.

**Retrieval is defined narrowly, and the drafting stage must hold the line.** A retrieval question is one whose *answer* lives in an earlier chapter. A question about the mesh data plane that merely leans on Ch 5's sidecar model is a **chapter** question. This chapter would otherwise score 80% retrieval and the number would mean nothing. Ch 13 and Ch 16 both made this ruling; it binds identically here.

| # | Falls after | Topic | Qs | Retrieval | Drawn from |
|---|---|---|---|---|---|
| TYB 1 | §3 | The definition, the ladder, and who decides | 6 | 1 | Ch 2 §2 — image immutability, contrasted with immutable infrastructure |
| TYB 2 | §5 | Extension points, and the layer that knows what it's carrying | 5 | 2 | Ch 2 §4 / Ch 9 §1 / Ch 11 §5 / Ch 6 §8 — the four interfaces, as one integrated item; Ch 10 §7 — what NetworkPolicy cannot do |
| TYB 3 | §8 | Scaling, serverless, and how the project runs | 5 | 1 | Ch 8 §6 — the three-supported-minors rule, paired with the cadence |

**The ≥4-back floor is satisfied three times over.** B3 requires at least one item from four or more chapters back; TYB 1 draws from Ch 2 (fifteen back), TYB 2 from Ch 2/6/9/11, TYB 3 from Ch 8 (nine back).

**TYB 2's four-interface item is the chapter's most important single question and must not be a matching exercise.** Its answer lives in four different chapters, and the shape it asks for is what §9 is about to argue. Build it as one integrated stem — a scenario in which a cluster needs a capability Kubernetes does not implement — rather than as "match the acronym to the layer," which Soundings Q1 already did and which tests the wrong thing.

**TYB 3 must carry at least two D4.3 items.** B1 names D4.3 the most under-studied competency on the exam and B2's mitigation is explicit treatment. A checkpoint falling immediately after §8 that tests only autoscalers would undo the section's whole design.

Every checkpoint carries trap answers targeting the misconceptions tabulated in the Exam Alert, why-wrong explanations for **all** options, and a revision prompt naming a **section** for 0–2 scorers.

---

## 6. Exam Alert plan

**High-priority topics.** Five, and the first is this chapter's own synthesis rather than a curriculum line:

1. **The four pluggable interfaces as one shape.** CRI, CNI, CSI, CRDs — and the ability to state what they have in common without being given the list. This is the chapter's Zenith and the book's most reused idea.
2. **The maturity ladder in order, and where the criteria live.** Sandbox → Incubating → Graduated. Criteria in the TOC's project-lifecycle documentation. The *levels* are examinable; the *roster* is dated data.
3. **Data plane versus control plane, twice.** A mesh's data plane is the proxies; its control plane configures them; neither is the cluster's control plane. Same vocabulary, different layer.
4. **Which autoscaler moves which axis, and which ones ship.** Replicas (HPA, KEDA), resources (VPA), nodes (Cluster Autoscaler, Karpenter). HPA is built in; VPA is an add-on.
5. **SIG, Working Group, Committee, Steering — and TAG is none of them.** Durable and topic-scoped; cross-SIG and short-lived; closed-membership; overall governance. TAGs are CNCF-wide, SIGs are Kubernetes-internal.

**Common traps** — ⚠ Navigational Hazards, loss-aversion framing. Every row is `[source]`-backed unless marked:

| Trap | The correct understanding |
|---|---|
| Reading *cloud native* as "runs in a public cloud" | The definition's first sentence says public, private **and** hybrid. The term is about how you build and operate, not where it runs. |
| Treating the CNCF technology list as exhaustive | The definition says outright that the list is non-exhaustive. |
| Ordering the maturity levels wrong | Sandbox → Incubating → Graduated. Sandbox is bleeding-edge; Incubating is production use by a small number of users; Graduated is stable and widely adopted. |
| Looking for graduation criteria on the projects page | They live in the TOC's project-lifecycle documentation. |
| Memorizing which projects are graduated | The roster changes. Learn the levels and what each asserts. |
| Confusing the TOC with the Governing Board | The Board sets the scope; the TOC approves projects **within** it and owns technical vision, architecture and lifecycle. |
| Using the pre-2025 TAG list | TAGs were restructured in 2025. The old list is all over older study material. |
| Treating CNCF TAGs and Kubernetes SIGs as the same thing | Different organizations at different scopes. *(easy to confuse — `[inferred]`, not a frequency claim)* |
| Confusing a SIG with a Working Group | SIGs are the primary, durable unit for a topic. Working Groups cross SIG lines and are short-lived. |
| Assuming every community group is open | Committees are not. They are formed by Steering for topics requiring discretion, and do not always operate in the open. |
| "A service mesh needs application code changes" | The defining property is delivering zero-trust security, observability and traffic management **without** them. |
| Confusing the mesh's data plane with its control plane — or with the cluster's | Data plane = the proxies mediating service-to-service traffic. Control plane = what configures them. Neither is Chapter 3's control plane. |
| "Service mesh means sidecars" | Sidecar mode puts an Envoy proxy beside each Pod; ambient mode uses per-node L4 proxies plus optional per-namespace Envoy proxies. Both use Envoy. |
| "Knative replaces Kubernetes" | Knative is Kubernetes-based, builds on the Pod abstraction, and is implemented as CRDs. |
| Confusing Knative Serving with Eventing | Serving: HTTP-triggered autoscaling container runtime with scale to zero. Eventing: CloudEvents-over-HTTP asynchronous routing. |
| "Serverless means no containers" | The workloads are still containers in Pods. The serverless property is the lifecycle. *(easy to confuse — `[inferred]`)* |
| Confusing horizontal with vertical scaling | Horizontal changes the **number** of replicas. Vertical changes the **resources** available to each. |
| "VPA ships with Kubernetes" | VPA is an add-on, not included by default. The object can exist while nothing acts on it — the same pattern as `kubectl top` without metrics-server. |
| "In-place vertical resize means VPA now works in place" | In-place Pod vertical scaling is stable as of the stated release; VPA does not yet support it directly. |
| Confusing Pod autoscaling with node autoscaling | HPA, VPA and KEDA scale **workloads**. Cluster Autoscaler and Karpenter scale the **node pool**. |
| "KEDA is a CPU autoscaler" | KEDA is event-driven — queue depth and similar external signals — and does schedule-based scaling through its Cron scaler. |
| Studying to the five-domain blueprint | Observability is no longer a standalone domain, Container Orchestration rose to 28%, and Application Delivery doubled to 16%. Much third-party prep still targets the old split. |

---

## 7. Practice Questions plan

**Target: 21**, per `question_budget.practice_questions` and B4's weight-proportional derivation (7% chapter weight → 15 + 2×(7−4) = 21).

| Section | Items | Rationale |
|---|---|---|
| §1 definition and characteristics | 3 | The chapter's headline and a `[source]`-quotable document; the five characteristics are the single most quotable thing in D4.2 |
| §2 maturity, lifecycle, CNCF governance, Landscape | 3 | Four `[source]` traps in one section, and D4.3's first home |
| §3 microservices, immutable infrastructure, declarative APIs | 1 | Proportionate. §3 owns framing, not substance; its content is better tested through §1's characteristics and §4's synthesis than through standalone recall |
| §4 the four interfaces, collected | 3 | The chapter's synthesis and the book's most cross-referenced section |
| §5 service mesh | 3 | Six inbound pointers and the book's most dangerous vocabulary collision |
| §6 serverless and Knative | 2 | Three named traps, two of them `[source]` |
| §7 the autoscaling landscape | 3 | Five named autoscalers, four `[source]` traps, three inbound retrieval anchors |
| §8 Kubernetes governance, ladder, KEPs, cadence, certifications | 3 | D4.3's second and larger home; five `[source]` traps |

**D4.3 receives 6 of 21 items (28.6%)**, above its share of the chapter's section count. That is deliberate and traceable to B1: it is the competency technically-strong candidates most reliably under-study, and B2's mitigation was explicit treatment rather than a separate chapter.

**Interleaving strategy.** At least six stems cross domains: one pairs a mesh with the NetworkPolicy limitation it addresses (D2.1), one pairs mTLS with encryption at rest (D2.2), one pairs a Cluster Autoscaler with a Pending Pod (D1.3), one pairs an HPA with a missing metrics-server (D2.3), one pairs CRDs with a Helm chart's `crds/` directory (D3.1), and one pairs the release cadence with a version-skew symptom (D1.2). Per skill Part 10, wrong options are built to catch the specific misconceptions tabulated above, and every option gets a why-wrong explanation.

**Retrieval-practice items** carry the same 25% ceiling as the Bearings and count separately from them; **at least five** of the 21 must draw their *answer* from Ch 2, 6, 7, 8, 9, 11, 13 or 14.

**Barred from all graded text in this chapter** (restated so no item quietly adopts one):

- **The dated graduated-project roster.** B3 excludes it from retrieval by name. No item may require the reader to know a specific project's current level.
- **The 60-question and 75% figures.** Unpublished; retrieving them would teach them as fact.
- From the term ledger's Part 2 rulings: **PodDisruptionBudget** (unowned, ⚑3), **ABAC**, **SRE**, **descheduler**, **eBPF**, and any item hinging on the absence of a Kubernetes LTS.
- **`[inferred]` traps** — #84 (serverless ≠ no containers) and #112 (TAGs vs SIGs) — may appear, framed as *easy to confuse*, never as *frequently tested*.
- **Cluster Proportional Autoscaler**, which §7 names in a completeness clause and does not teach.

---

## 8. Required figures

Eight anchors: seven concept diagrams plus one Zenith, at the top of skill Part 18.10's 2–8 band — appropriate for the chapter with the most distinct arcs in the book.

| Anchor | § | Type | Purpose and content |
|---|---|---|---|
| `ch17-fig01-cloud-native-definition-characteristics` | §1 | Annotated structure | The definition's clauses laid out with the **five characteristics** — secure, resilient, manageable, sustainable, observable — as the visual payload, each annotated with one clause of what it asks of a system. Not a word cloud and not the technology list. ≤7 labels: five characteristics plus the loose-coupling spine. |
| `ch17-fig05-cncf-maturity-levels` | §2 | Progression | Sandbox → Incubating → Graduated as a ladder, each rung annotated with what the level *asserts* (bleeding edge · production use by a small number of users · stable and widely adopted) and a marker showing that the criteria live with the TOC. **No project names on the figure** — the roster is dated data and a figure is the hardest artifact to update. |
| `ch17-fig02-extension-points-map` | §4 | Stack | The cluster in layers with **four sockets** marked — runtime, network, storage, API — each labeled with its interface and the chapter it was taught in. ≤7 labels, which means the four sockets plus a spine and no more; **the documentation's wider six-extension-point list goes in a table beside the figure, not into it.** That table is how Ch 10:1896's two-maps promise gets kept. Likely **stack family, so Lucide glyphs** per style-decisions 2026-08-25 — confirm at the image-specs stage. |
| `ch17-fig03-mesh-data-vs-control-plane` | §5 | Comparative | Services with their proxies (data plane) beneath a configuring layer (mesh control plane), with **the cluster's own control plane drawn as a clearly separate third element** and visually differentiated. The separation *is* the figure's argument — trap #101 is defused here or nowhere. Sidecar and ambient shown as two arrangements of the same data plane, not two products. ≤7 labels. |
| `ch17-fig07-scale-to-zero-and-the-knative-service` | §6 | Pipeline | A request arriving at an idle Knative Service, replicas going 0 → N, serving, and returning to 0. **Containers in Pods must be visible at both ends of the cycle** — that visual is the section's Fixed Point and the refutation of "serverless means no containers." **New, not in the arc stub list.** Pipeline family, so glyphs; confirm at image-specs. |
| `ch17-fig04-autoscaler-landscape` | §7 | Comparative matrix | Rows are the named autoscalers; columns are **what moves** (replica count · per-replica resources · node pool) and **what triggers it** (observed utilization · external event · unschedulable Pods). Two cells must be visually marked: **VPA as not-shipped-by-default**, and **KEDA sharing HPA's axis with a different trigger**. Those two marks carry three of the section's four traps. |
| `ch17-fig06-cncf-and-k8s-governance` | §8 | Comparative | Two structures side by side — **CNCF**: Governing Board, TOC, TAGs, End User TAB; **Kubernetes**: Steering Committee, SIGs, Working Groups, Committees. The point is the *pairing*, so it lives in §8 where both halves exist rather than being split across §2 and §8. Committees visually marked as closed-membership. ≤7 labels per side; if that breaches, drop the End User TAB to prose. |
| `ch17-zenith-one-pluggability-story` | §9 | Dramatic synthesis | The four sockets from `fig02` collapsed into a **single** interface-and-implementation relation, with the four instances arrayed as evidence rather than as the subject. **Must visually rhyme with `ch17-fig02`** the way `ch15-zenith` must rhyme with `ch03-fig02` — same vocabulary, one altitude higher, four things becoming one shape. Exactly one Zenith per content chapter, per Part 18.10. |

**Numbering note, so no downstream stage reads it as an error.** Document order runs fig01, fig05, fig02, fig03, fig07, fig04, fig06, zenith. This is deliberate and follows the Ch 13 and Ch 16 precedent: the six arc-outline stub IDs are preserved exactly as stubbed so the join key with `image-specs.md` and the diagram pipeline's `figures-metadata.yaml` stays stable, and the one new figure takes the next free number. Anchor IDs are identifiers, not an ordering contract; the structural contract's `anchor_id_pattern` imposes no sequence. No arc stub was dropped or moved section.

**The one section without a figure, and why.** §3 gets none. Every candidate — monolith versus microservices, mutate-versus-replace, declarative versus imperative — restates a figure already owned by Ch 2 §1, Ch 2 §2 or Ch 4 §1, and Part 18.4's coherence principle forbids a visual that adds nothing. A generic microservices diagram would additionally be the single most templated-looking image in the book, which Part 18.12 bans outright.

---

## 9. Open questions for the author

**1. One published pointer contradicts two others (B6 Collision #2).** Shipped `chapter-03:350` reads *"see Ch 17 §1 — the CNCF, its governance, and the cloud native definition."* Governance is §2; the definition is §1. Two other shipped pointers — `chapter-01:144` and `chapter-02:671` — correctly send governance-seeking readers to §2, and `chapter-15:1215` quotes §2's title verbatim. Three to one. **Recommendation: retarget `chapter-03:350` to `Ch 17 §1–§2`**, which is honest (the reader wants both halves) and costs one line in a shipped chapter. Do **not** move governance into §1 to satisfy it — §1 is already the busiest anchor in the chapter with four inbound pointers, and moving governance there would break three pointers to fix one. Adjacent sections make the current state survivable if the author would rather not touch shipped text; flagged, not taken silently.

**2. Blocking research — Stage 2 must fetch these before drafting.** The cached corpus for this chapter is unusually thin: every one of the twelve Ch 17-relevant snapshots runs 10–23 lines. They are dense summaries rather than truncations, which is better than Ch 16's situation, but they are index-level for a nine-section chapter carrying two whole competencies. B1 names gaps G10, G11, G14, G15, G16, G17, G31 and G32 as this chapter's. Assessed against what is actually on disk:

*Substantially closed already — verify only:* G15 (CNCF Landscape) and G17 (Code of Conduct, KubeCon, Ambassadors, community groups, LFX) are both well covered by `cncf-landscape-and-community-2026-08-23.md`. G16 is covered across `k8s-community-membership-ladder`, `k8s-keps-and-feature-stages` and `k8s-releases-cadence`. G31 is covered by `cncf-kcna-certification-page-2026-08-23.md`, which states the CKA/CKAD/CKS relationship in quotable form.

*Still open, and needed:*
- **Microservices as a defined term.** No snapshot defines it beyond the CNCF definition's one-word appearance in a technology list. §3 owns the concept and cannot draft it from a list item. Fetch `glossary.cncf.io/microservices-architecture/` and `glossary.cncf.io/monolithic-apps/`.
- **Istio beyond the one-page overview.** `istio-service-mesh-2026-08-23.md` is 18 lines and is the *only* mesh source. It supports the definition, the data/control-plane split, Envoy, and sidecar-versus-ambient — which is genuinely most of what §5 needs — but nothing in it supports mTLS mechanics or the zero-trust framing at more than slogan depth. Fetch `istio.io/latest/docs/concepts/security/` for the workload-identity and mTLS claims, and `glossary.cncf.io/service-mesh/` for a vendor-neutral definition to quote beside Istio's.
- **Karpenter.** Named in exactly one clause of one snapshot. If §7 is to name it as a distinct thing rather than a synonym for Cluster Autoscaler, fetch `karpenter.sh/docs/` — and see Open Question 5 on its affiliation.
- **Kubernetes origin and history (G14).** Ch 3 §1 shipped this material, so it is sourced; **verify** rather than re-fetch, and have §2 or §8 point at Ch 3 §1 rather than restate.
- **A vendor-neutral serverless definition.** `knative-overview` is strong on Knative and silent on what serverless *is*. Fetch `glossary.cncf.io/serverless/`.

**3. G32 — is cost management still in scope?** B1 flags it as unresolved: FinOps, OpenCost and KubeCost sat adjacent to the old standalone Observability domain, and whether they survive into the revised D4 is not determinable from the sources. Nothing in the cached corpus covers them, and neither B6 nor B2 gives them a section. **Recommendation: out of this chapter entirely.** If the author wants them, the natural home is §2 alongside the Landscape's Observability and Analysis category, at one clause, ungraded — not a section. Confirm, because the alternative (silently omitting a possibly-in-scope topic) is a real risk on a 12% domain.

**4. The graduated-project roster — how many names, and how framed?** B3 excludes the roster from retrieval and instructs that the *levels* be retrieved instead. But §2 without a single named project is abstract to the point of unmemorability. **Recommendation: name at most six graduated projects the reader has already met by name in this book** — containerd, CoreDNS, etcd, Helm, Prometheus, Argo — with an explicit snapshot date, a source tag, and a sentence telling the reader not to memorize the list. Shipped Ch 15:1215 modeled this exact treatment for Argo and Flux and it reads well. Confirm the count and the selection.

**5. Karpenter's affiliation must not be written from memory.** `k8s-docs-autoscaling-2026-08-23.md` names Karpenter as a node autoscaler and says nothing about its governance. KEDA and Knative *are* stated as CNCF graduated in the cached sources; Karpenter is not. Given that §2 has just taught the maturity ladder, an unsourced maturity claim about a project named in §7 is exactly the error a careful reader will catch. **Recommendation: name Karpenter as a node autoscaler alongside Cluster Autoscaler and make no affiliation or maturity claim at all** unless the research pass returns a tagged source. Confirm.

**6. §7's title reads "four things that scale" and the honest count is four autoscalers across three axes.** The section plan above resolves this by making the shared axis (KEDA and HPA both move replica count, on different triggers) an explicit teaching point rather than an embarrassment — it is trap #107 rendered structurally. The title is fixed by B6 and no shipped pointer quotes it, so it *could* be changed. **Recommendation: keep the title and teach the mismatch.** Confirm, because the alternative — retitling to something like "Three Axes, Four Autoscalers" — is defensible and would cost nothing.

**7. Bearings at 16, one above the arc outline's stated 12–15 band.** The arithmetic is in the frontmatter note: 16 is the smallest count that puts retrieval at exactly 25.0% across three checkpoints of ≥5. Ch 16 made the identical move against B4's number and documented it. **Recommendation: accept 16, chapter total 45.** If the author prefers to hold the arc band, 15 is workable at 20% retrieval (3 items) — but this chapter is designated a ceiling chapter precisely because retrieval is its method, and dropping below the ceiling here costs more than in any other chapter.

**8. §4 and §9 are the same synthesis at two altitudes, and that is the chapter's biggest craft risk.** B6 designed it this way and the section plan gives each a distinct job (§4 maps and answers *where*; §9 claims and answers *so what*). It can still fail as repetition. **Recommendation: draft §9 last, and draft it short** — under a fifth of §4's length. If the revision stage finds §9 restating the four names, cut it to three paragraphs and let `ch17-zenith` carry the recognition. Flagged so the drafting stage treats §9's brevity as a feature rather than an omission to fill.

**9. `commands` is empty and that is correct.** This is the only content chapter in the book with no command surface. Recorded here so the integration-check stage does not read the empty list as a tagging failure, and so no reviewer adds a `kubectl` demonstration to make the chapter resemble its neighbors. Everything the reader might reach for here — `kubectl scale`, `kubectl top`, `kubectl api-resources` — is owned by Ch 6 §2, Ch 13 §7 or Ch 6 §8 respectively.

**10. Ch 1 remains unaddressable by section number** (B6 Collision #1). Two shipped pointers land here from Ch 1 (182, 466) and both are correctly unnumbered. Nothing in this chapter should emit `Ch 1 §N`. Restated only so the drafting stage does not invent one when §1 pays off Ch 1's plant and §8 pays off Ch 1's certification deferral.

**11. Glossary and acronym-register additions.** Queue for the glossary build: **Envoy**, **ambient mode**, **CloudEvents**, **Karpenter**, **KEDA** (register row exists; needs a glossary entry), **LFX mentorship**, **Cloud Native Community Group**, **Ambassador**, and **TAB** (registered, but this chapter is its first and only reader-facing use, so expand it in place at §2). Also still open from earlier gates and not this chapter's to fix: `reverse proxy` and `SNI` (Ch 10), `static Pod` and `mirror Pod` and `crictl` (Ch 13), `distroless` and `ephemeral container` (Ch 16), `NFS`/`LUN`/`iSCSI`/`EBS`/`finalizer`/`CSIDriver` (Ch 11), `CNAME`/`BGP`/`eBPF` (Ch 9).

**12. The in-chapter metadata line must read 12%, not 7%.** Restated from the frontmatter because it is the single most likely thing for a drafting stage to get wrong on this chapter: 12% is the published weight of D4 and takes a source tag; 7% is this book's authored allocation between Ch 17 and Ch 18 and must be labeled as such, per B1 gap G33 and B2 disclosure #1. Shipped Ch 16 honors the identical ruling for D3's 16%.

---

*Stage 1 complete. Nine sections, seven of them pinned by number and four by title; 26 inbound cross-bearings verified against chapters 01–16; one published pointer flagged as contradicting two others; 45 questions budgeted; eight figures, one of them new; twelve open questions, two of which (research fetches, and the 12%-not-7% metadata line) block drafting.*
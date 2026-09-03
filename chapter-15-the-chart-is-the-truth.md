---
chapter: 15
chapter_type: "content"
title: "The Chart Is the Truth"
subtitle: "GitOps is the control loop you already learned, pointed at a repository"
exam_domain: "Cloud Native Application Delivery (competency: Application Delivery)"
domain_weight_pct: 7
complexity: "mixed"
novelty: "paradigm-shifting"
prereq_factor: "heavy"

#-- SUBTITLE NOTE. Eleven words, from the arc outline and the chapter lineup,
#-- carried forward unmodified. It is one word over the ≤10 guideline; the
#-- overrun is accepted because this string is quoted verbatim in two upstream
#-- contracts and because it IS the §7 Zenith claim. Subtitle and synthesis
#-- therefore agree by construction (the Ch 12 / Ch 13 / Ch 14 pattern).
#--
#-- ⚠ But note what that costs, because it is unusual: this subtitle states
#-- the chapter's PRIMARY ZENITH on the chapter's second line. Ch 14's
#-- subtitle did the same for a smaller payoff. The consequence is that §7
#-- cannot rely on surprise — it must earn the recognition by DEMONSTRATION,
#-- having announced the claim 25 pages earlier. Drafting should treat the
#-- subtitle as a promissory note the chapter spends seven sections redeeming,
#-- not as a spoiler to work around. See Open Question 6.

#-- EXAM_DOMAIN NOTE. D3.1 Application Delivery, in the house form shipped by
#-- ch-04/-09/-10/-11/-12/-13/-14. The published domain weight is 16%
#-- [source: cncf-kcna-curriculum-pdf-2026-08-23]; the metadata line states
#-- that figure with its tag, followed by the house disclaimer that the split
#-- across Ch 14-16 is an authored allocation (B1 gap G33, B2 disclosure #1).
#-- Do NOT present 7% as published.
#--
#-- ⚠ HONESTY CONSTRAINT — inherited from Ch 14, and SHARPER here.
#-- Verified 2026-08-31 against cncf-kcna-curriculum-pdf-2026-08-23 (line 15):
#-- CNCF publishes the competency name "Application Delivery" and nothing
#-- else. The snapshot contains no occurrence of "GitOps", "Argo", "Flux",
#-- "Helm", "twelve-factor", or "canary". This chapter's ENTIRE topic list is
#-- authored inference. Unlike Ch 14, there is not even an LFS250 syllabus
#-- snapshot to lean on — no cached source enumerates that course's modules.
#-- What the corpus DOES support: Argo and Flux are both CNCF **graduated**
#-- projects [source: cncf-project-maturity-levels-2026-08-23] and OpenGitOps
#-- is a CNCF project [source: opengitops-principles-2026-08-23]. That is the
#-- honest basis for the inference and it should be the basis stated.
#-- Binding consequences:
#--   * Ch 14 already made this beat at length in Why This Chapter Matters.
#--     DO NOT repeat it at length — that is channel redundancy (skill Part 7).
#--     One short back-bearing to Ch 14's statement, then move on.
#--   * No GitOps / Argo CD / Flux / strategy fact may be framed as
#--     "frequently tested", "commonly appears", or any frequency claim.
#--     Skill Part 14, Ethical Guardrail #8.
#--   * B1 traps 73-81 are [source]-tagged and are real confusions, so they
#--     may be called "easy to confuse." They may NOT be called common exam
#--     material. The tag licenses the confusion, not the frequency.
#-- See Open Question 7.

#-- NOVELTY NOTE. `paradigm-shifting`, and this is a considered call rather
#-- than the default. B1 trap 74 — "missing 'pulled', assuming a pipeline
#-- pushes to the cluster" — is not a vocabulary error. It is a reader whose
#-- entire model of deployment is a pipeline that reaches into a cluster,
#-- meeting a definition that inverts the direction of travel. That is a
#-- paradigm mismatch, and it is the same shape as Ch 3's imperative-to-
#-- declarative shift. Rated accordingly.

#-- PREREQ NOTE. `heavy` — the heaviest prerequisite load in the book, and
#-- the reason the Soundings is doing more work here than anywhere else:
#--   Ch 3 §6 (the control loop; desired vs current; reconciliation) -> §3, §4, §7  ** the big one **
#--   Ch 3 §5 (the API server as sole mutator)                       -> §3, §4
#--   Ch 4 §1 (declarative; the object as an artifact of intent)      -> §1, §3
#--   Ch 4 §2 (spec vs status)                                       -> §4  ** OutOfSync depends on it **
#--   Ch 4 §4 (ConfigMap/Secret as externalized config)              -> §1
#--   Ch 4 §5 (labels; the `release: stable|canary` example at :788)  -> §2
#--   Ch 5 §6 (ServiceAccount as identity)                           -> §4
#--   Ch 6 §4 (rolling-update mechanics; maxSurge/maxUnavailable)     -> §2
#--   Ch 6 §5 (revisions; `kubectl rollout undo`)                     -> §4
#--   Ch 6 §8 (custom resources, CRDs, the operator pattern)          -> §4, §6
#--   Ch 10 §3 (the object-without-a-component pattern, BY NAME)      -> §4
#--   Ch 12 §2-§3 (ServiceAccounts as RBAC subjects; grants)          -> §4
#--   Ch 12 §4 (Secrets are not encrypted)                            -> §3
#--   Ch 14 §2 (a chart as a source of manifests)                     -> §4
#-- Ch 3 §6 and Ch 4 §2 are the two that cannot be missing. §7's entire
#-- payoff is a retrieval of Ch 3 §6; a reader who has lost the loop
#-- experiences the Zenith as a seventh list. And OutOfSync is literally
#-- "status does not match spec, where spec lives in Git" — unreadable
#-- without Ch 4 §2. Both get a Soundings question and both appear in the
#-- 0-2 rubric branch by SECTION number.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "substantial" — 7
#-- points, and it carries the book's primary Zenith. Planning signal only,
#-- NOT a target.
#--
#-- ⚠ SECTION NUMBERING — FOUR NUMBERS ARE PINNED. This is the second-most
#-- constrained chapter in the book after Ch 13. Verified 2026-08-31 by line
#-- number against chapters 01-14:
#--   chapter-05:781  -> "see Ch 15 §4 - the delivery agent's identity"
#--   chapter-09:1249 -> "see Ch 15 §7 - the control loop, generalized,
#--                       pointed at a Git repository"
#--   chapter-12:617  -> "see Ch 15 §4 - an agent that watches a repository"
#--   chapter-12:866  -> "see Ch 15 §5 - ordering the sync"
#--   chapter-14:571  -> "see Ch 15 §4 - an agent that watches a repository"
#--   chapter-14:653  -> "see Ch 15 §4 - an agent that watches a repository"
#--                       (the rollback-by-revert promise)
#--   chapter-14:1047 -> "see Ch 15 §3 - push, or pull"
#--   chapter-14:1117 -> "see Ch 15 §3 - push, or pull"
#--   chapter-14:1309 -> "see Ch 15 §3 - push, or pull"
#-- §3, §4, §5 and §7 are IMMOVABLE. Nine numbered pointers from five
#-- chapters; §4 alone carries four of them.
#--
#-- Eight further chapter-level (unnumbered) pointers also land here and are
#-- promises this chapter owes:
#--   chapter-03:655  -> "the same shape, with a Git repository where etcd sits"
#--   chapter-03:832  -> "the same loop, with a Git repository holding desired state"
#--   chapter-03:957  -> "the loop, pointed somewhere unexpected"
#--   chapter-04:453  -> "the same declaration, kept in a repository"
#--   chapter-04:722  -> "the twelve factors, and which ones Kubernetes hands
#--                       you for free"                          -> §1
#--   chapter-05:559  -> "the twelve factors" (disposability)     -> §1
#--   chapter-06:665  -> "blue/green, canary, and A/B, and the tooling that
#--                       implements them"                       -> §2
#--   chapter-06:721  -> "and a third thing, again wearing it" (rollback) -> §4
#--   chapter-06:1037 -> "a delivery tool that is, structurally, a controller
#--                       acting on custom resources"            -> §4
#--   chapter-06:1145 -> "a controller whose desired state lives in a Git
#--                       repository, and why that is the same technology
#--                       rather than a new one"                 -> §7
#--   chapter-12:485  -> "push, or pull"                          -> §3
#-- The skeleton's seven sections are adopted unchanged, in order, with no
#-- renumbering. No section may be merged or split.
sections:
  - name: "Twelve Factors, and the Ones Kubernetes Already Solved"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch15-fig01-twelve-factor-in-kubernetes"
    checkpoint_after: false

  - name: "Ways to Replace What's Running"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch15-fig02-deployment-strategies-compared"
    checkpoint_after: true

  - name: "Push, or Pull"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch15-fig03-cicd-push-vs-gitops-pull"
    checkpoint_after: false

  - name: "An Agent That Watches a Repository"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch15-fig04-argocd-sync-states-and-hooks"
    checkpoint_after: true

  - name: "Ordering the Sync"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch15-fig06-sync-waves-and-hook-phases"
    checkpoint_after: false

  - name: "The Other Agent, and More Than One Cluster"
    objectives: ["D3.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true

  - name: "The Control Loop, Pointed at a Repository"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch15-zenith-control-loop-pointed-at-a-repo"
    checkpoint_after: false

#-- SECOND FIGURE IN §3. `ch15-fig05-opengitops-four-principles` also renders
#-- inside §3, per the B6 skeleton's explicit instruction. The schema above
#-- carries one anchor per section, so fig05 is recorded in `figures_planned`
#-- and in § "Required figures" rather than in `sections[]`. This is the same
#-- accommodation the schema needs anywhere a section earns two figures; it
#-- is not drift. See Open Question 5.

#-- Skill Part 11: Soundings pre-chapter diagnostic ----------------------
soundings_planned:
  question_count: 8
  topics:
    - "What a controller does with desired state and current state, and how often it does it (Ch 3 §6) — the chapter's load-bearing decay probe"
    - "Which field of an object you write and which one the system writes, and what it means when they disagree (Ch 4 §2)"
    - "What a Deployment's default update strategy does, and what `maxSurge` and `maxUnavailable` control (Ch 6 §4)"
    - "You install a CRD. What can now exist that could not before, and what still has to be true for anything to happen? (Ch 6 §8 + Ch 10 §3 by name)"
    - "A process running inside the cluster needs to create and delete objects across several namespaces. What does it need, and what decides how much it may do? (Ch 5 §6 + Ch 12 §2-§3)"
    - "Where environment-specific configuration belongs, and why baking it into the image is the wrong answer (Ch 4 §4 + Ch 2 §2)"
    - "General professional knowledge: somebody makes a change directly on a production system, outside whatever process the team normally uses. What goes wrong afterward, and when do you find out?"
    - "General professional knowledge: you have a repository whose commit history records what was intended. What can you do with that history that you cannot do with the current state of a running server?"

#-- Skill Part 8: practice-question budget ------------------------------
#-- B4 allocated 8 / 10 / 21 = 39. Bearings raised to 16 across three
#-- checkpoints (6+5+5), following the Ch 13 precedent exactly. Reason,
#-- identical to Ch 13's: this chapter's arc-outline retrieval target is the
#-- **25% ceiling**, and 16 is the smallest count that lets retrieval land at
#-- EXACTLY 25.0% (4 of 16) across three checkpoints of >= 5. At B4's 10, a
#-- 25% target rounds to 2.5 and the ceiling cannot be hit cleanly; at 15
#-- (the Ch 5-12 shape) it rounds to 3.75. Practice stays at B4's 21.
#-- New total 45. B4 explicitly sanctions this: "Outlines should treat the 10
#-- as a contract to exceed, not a target to hit," and names multi-arc
#-- chapters as the case. This chapter carries three arcs (§1-§2 the
#-- application and its releases; §3-§4 push/pull and the agent; §5-§6
#-- ordering and the alternatives).
question_budget:
  soundings: 8
  taking_your_bearings: 16             # across 3 checkpoints (6 + 5 + 5)
  practice_questions: 21
  total_this_chapter: 45

#-- Concept / objective / command tagging -------------------------------
kb_tags:
  objectives: ["D3.1"]
  concepts:
    - "twelve-factor-app"
    - "factor-iii-config-in-environment"
    - "factor-vi-stateless-processes"
    - "factor-ix-disposability"
    - "factor-xi-logs-as-event-streams"
    - "deployment-strategy-vocabulary"
    - "recreate-strategy"
    - "blue-green-deployment"
    - "canary-deployment"
    - "progressive-delivery"
    - "push-based-delivery"
    - "pull-based-delivery"
    - "cicd"
    - "gitops"
    - "opengitops-four-principles"
    - "declarative-principle"
    - "versioned-and-immutable-principle"
    - "pulled-automatically-principle"
    - "continuously-reconciled-principle"
    - "blast-radius"
    - "argo-cd"
    - "argo-cd-application-resource"
    - "source-of-truth"
    - "manifest-source"
    - "tracking-branch-tag-commit"
    - "synced-outofsync"
    - "sync-operation"
    - "self-heal"
    - "drift-detection"
    - "rollback-by-revert"
    - "delivery-agent-identity"
    - "sync-hook-phases"
    - "sync-wave"
    - "flux"
    - "flux-controller-set"
    - "flux-bootstrap"
    - "multi-cluster-delivery"
  commands: []

#-- COMMANDS NOTE — DELIBERATELY EMPTY, and this is the right call rather
#-- than an omission. Ch 13's materialisation raised an AUTHOR-REVIEW because
#-- its outline listed commands the draft correctly declined to teach; Ch 14
#-- responded by listing only what would actually be demonstrated. Applied
#-- here, the list is empty: this chapter teaches an ARCHITECTURE and a set
#-- of PRINCIPLES, not a CLI. `argocd app sync`, `argocd app rollback`,
#-- `flux bootstrap`, `flux reconcile` are all deliberately ABSENT — a
#-- reader who can recite them has learned nothing the exam asks for, and
#-- teaching them would misrepresent an associate credential as a tool
#-- tutorial. If drafting genuinely needs one to make a point concrete, add
#-- it here rather than letting the concept index under-claim. `git revert`
#-- is the single plausible exception; see § "Section plan", §4.

figures_planned:
  - "ch15-fig01-twelve-factor-in-kubernetes"
  - "ch15-fig02-deployment-strategies-compared"
  - "ch15-fig03-cicd-push-vs-gitops-pull"
  - "ch15-fig04-argocd-sync-states-and-hooks"
  - "ch15-fig05-opengitops-four-principles"
  - "ch15-fig06-sync-waves-and-hook-phases"
  - "ch15-zenith-control-loop-pointed-at-a-repo"
---

# Chapter 15: The Chart Is the Truth
## *"GitOps is the control loop you already learned, pointed at a repository"*

**Domain Weight: 16% (Cloud Native Application Delivery) [source: cncf-kcna-curriculum-pdf-2026-08-23] | Complexity: Mixed | Novelty: Paradigm-shifting**

*This domain **doubled** in the 2025-11-24 revision, from 8% to 16% [source: lf-kcna-program-changes-2026-08-23] — the largest proportional change on the blueprint, and the reason a great deal of third-party prep under-serves it. CNCF publishes two competencies under this domain — Application Delivery and Debugging — and no topic list beneath either [source: cncf-kcna-curriculum-pdf-2026-08-23]. The allocation of that 16% across Chapters 14, 15, and 16 is this book's authored judgment, not a published split.*

---

## Attention Budget

**Total time: ~100 minutes | Recommended: Split across 2 sessions**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| 🧭 Soundings | 8 min | Medium | Before you start |
| §1 Twelve Factors, and the Ones Kubernetes Already Solved | 10 min | Low | Anytime |
| §2 Ways to Replace What's Running | 12 min | Medium | Mid-session |
| ☆ Taking Your Bearings 1 | 6 min | Medium | After a short break |
| §3 Push, or Pull | 15 min | High | Peak attention |
| §4 An Agent That Watches a Repository | 15 min | High | Peak attention |
| ☆ Taking Your Bearings 2 | 5 min | Medium | After a short break |
| §5 Ordering the Sync | 8 min | Medium | Anytime |
| §6 The Other Agent, and More Than One Cluster | 8 min | Low | Anytime |
| ☆ Taking Your Bearings 3 | 5 min | Medium | Immediately before §7 |
| §7 The Control Loop, Pointed at a Repository | 8 min | Medium | Peak attention |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*Session break suggested after ☆ Taking Your Bearings 1. Sections 3 and 4 carry the chapter's argument and deserve a fresh head.*

*If you only have 15 minutes: read §3, then read §7. Those two sections are the chapter.*

---

> *"Every deploy is a claim about what should be true. Most of them are never checked again."*
> — Lodestar Ledgers

<!-- RESOLVED 2026-08-31 (integration gate): the callback was verbatim, and it was not the
     only one -- this chapter's opening paragraph also restates Ch 14's closing paragraph
     nearly word for word, so together roughly 60 words of Ch 14's last page were reproduced
     on Ch 15's first. Same information, same channel, immediately adjacent: the negative
     kind of redundancy under skill Part 7, landing exactly where arousal has to be
     established. The prose recap does real structural work (it sets up the two-halves
     split), so the epigraph was the cheaper cut and is now a new line on intent vs.
     outcome. -->

---

## 🧭 Soundings

Before reading this chapter, try these questions. Your score determines how to approach the content — no shame in any score, just different reading strategies.

This chapter leans harder on what came before than any other in the book. Two of these questions are load-bearing: miss them and the last section will not land, and no amount of careful reading here will fix that. Better to find out now.

1. A controller holds a recorded target and observes what actually exists. What does it do when the two differ, and how often does it check?

2. A Kubernetes object has one field you write and one the system writes. Which is which, and what does it mean when the two disagree?

3. What does a Deployment's default update strategy actually do, and what do `maxSurge` and `maxUnavailable` control?

4. You install a CustomResourceDefinition on a cluster. What can now exist that could not exist before, and what still has to be true before anything actually happens?

5. A process running inside the cluster needs to create and delete objects across several namespaces. What does it need in order to be allowed to, and what decides how much it may do?

6. Where does environment-specific configuration belong, and why is baking it into the container image the wrong answer?

7. General professional knowledge, no Kubernetes required: somebody makes a change directly on a production system, outside whatever process the team normally uses. What goes wrong afterward, and when do you find out?

8. General professional knowledge: you have a repository whose commit history records what was intended. What can you do with that history that you cannot do with the current state of a running server?

<details>
<summary>Click for answers + reading strategy</summary>

1. It acts to close the gap. It takes whatever action moves current state toward desired state, and it does this continuously, in a loop that never ends, not once at creation time. *(Ch 3 §6)*

2. You write `spec`; the system writes `status`. A disagreement between them means the system has not yet reached, or can no longer reach, what you asked for. It is a report, not necessarily a fault. *(Ch 4 §2)*

3. `RollingUpdate` replaces Pods gradually, standing up new ones while taking old ones down, so the application stays available throughout. `maxSurge` caps how many Pods may exist above the desired replica count during the update; `maxUnavailable` caps how many may be missing below it. *(Ch 6 §4)*

4. A new *kind* of object can now be created and stored through the API server: the API is extended. But storage is all you get. Nothing acts on those objects unless a controller is running and watching for them. *(Ch 6 §8, and the pattern named at Ch 10 §3)*

5. It needs an identity, a ServiceAccount, and it needs RBAC grants bound to that identity. The Role or ClusterRole defines what verbs on what resources are permitted; the binding attaches that permission set to the ServiceAccount. Permissions are additive, and there is no deny rule. *(Ch 5 §6, Ch 12 §2–§3)*

6. Outside the image, in ConfigMaps and Secrets, injected at runtime. Baking it in means one image per environment, which destroys the property that makes images useful: the artifact you tested is not the artifact you ship. *(Ch 4 §4, Ch 2 §2)*

7. The system now differs from whatever the team's records say it contains, and nothing announces this. You find out later, from the wrong direction: at the next deployment, when the change is silently overwritten, or when a new person reads the records and acts on a description that stopped being true weeks ago.

8. You can see what was intended and when, who intended it, what it replaced, and — critically — you can return to any previous intent exactly, because the history is complete and each entry is fixed. A running server tells you only what is true right now. It does not tell you what anybody meant.

---

**If you got 6+ right:** Skim §1 and §2. They name things you already do. Read §3, §4, and §7 properly; that is where the chapter's argument lives, and it is an argument rather than a vocabulary list.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Before you start, re-read **Ch 3 §6** (controllers and the control loop) and **Ch 4 §2** (spec versus status). Not alongside this chapter. Before it. Those two sections are the foundation this entire chapter stands on, and §7's payoff is a retrieval of Ch 3 §6 specifically. If you missed **question 1** in particular, that re-read is not optional. Everything else here will make sense without it. The last section will not.

</details>

---

## Why This Chapter Matters

The previous chapter left you holding a package and a complaint.

You have a unit now: a chart, a set of overlays, something with a version number that installs the same way twice. It has bought you less than it should have, because the unit still gets applied by a person. Somebody with cluster credentials on a laptop, running a command from a machine nobody audits, at a moment nobody records. They apply the version they believe is current. Afterward, nothing keeps watch.

That complaint has two halves, and this chapter answers them in order.

The first half is **who applies it**. That sounds procedural, the sort of thing settled in a runbook and forgotten. It isn't. The answer determines where cluster credentials physically live, who can reach them, and how large a single mistake gets before something catches it. Change the answer and you change the security posture of the whole delivery path. We take that up in §3.

The second half is **what happens afterward**. "Afterward, nothing keeps watch" is the actual defect, and it should strike you as strange, because you have spent thirteen chapters inside a system whose entire architecture is things that keep watch. A ReplicaSet keeps watch. The scheduler keeps watch. The node controller keeps watch. Kubernetes is, structurally, a collection of processes that notice a gap and close it, forever.

So you already own the answer to the second half. You have not yet been shown that you own it. That is what §7 is for, and it is why this chapter's subtitle gives the answer away on the second line: the recognition is worth more than the surprise.

**A shift in what you are.** Up to now you have been someone who *makes changes to a cluster*. This chapter asks you to become someone who *maintains a claim about what a cluster should contain*, and then never touches the cluster again.

That is genuinely uncomfortable, and it should be said plainly rather than sold. Thirteen chapters of your growing competence have been measured in `kubectl` fluency: knowing the verb, knowing the flag, knowing which object to reach for. This chapter asks you to give up the terminal as the instrument of change. Not as an instrument of *inspection*; you will read the cluster constantly, and Chapters 13 and 16 are built on it. But as the thing you use to make something different, the terminal goes away. What replaces it is a file, a commit, and a review.

In my experience, practitioners who make this shift describe the same two feelings in sequence: first that it is slower, then that they cannot go back.

The stakes here were banked in Chapter 1, and one clause will do: this domain doubled in the 2025-11-24 blueprint revision. Chapter 14 cashed the first half. This is the second.

<!-- RESOLVED 2026-08-31 (integration gate): Chapter 1 does carry the pre-revision blueprint,
     sourced to lf-kcna-program-changes-2026-08-23 (ch01:246, ch01:259 — "Cloud Native App
     Delivery 8% -> 16% (x2)"). Figure restored here on that tag, as this note directed. No
     archived curriculum PDF needed. -->

**About what CNCF actually publishes.** Chapter 14 made this statement at length and it covers this chapter too, so one back-bearing rather than a repetition: the published curriculum gives two competency names under this domain and no list of topics beneath either *[cross-bearing: see Ch 14 — Why This Chapter Matters]*. What supports the inference that GitOps belongs here is positive rather than speculative. Argo and Flux are both CNCF **graduated** projects [source: cncf-project-maturity-levels-2026-08-23], and OpenGitOps is a CNCF project [source: opengitops-principles-v1-2026-08-31]. A CNCF exam asking about application delivery is asking about the delivery model CNCF's own graduated projects implement. That is the basis. It is a good one, and it is honest about being an inference.

One consequence runs through the rest of the chapter without further comment: nothing here is described as "frequently tested" or "commonly appears." Those claims would require a published sub-topic list, and there isn't one. What you will see instead is "easy to confuse" and "this is the distinction the material rewards," which are claims this book can actually stand behind.

> **Dead Reckoning:** GitOps is a set of four principles about how desired state is stored and applied. The desired state is declarative; it lives in a version-controlled store that keeps a complete history; software agents pull it from that store rather than having it pushed to them; and those agents continuously compare actual state against it and act to close the difference [source: opengitops-principles-v1-2026-08-31]. Argo CD and Flux are two implementations. Both are Kubernetes controllers: Argo CD's application controller "is a Kubernetes controller" [source: argocd-architecture-2026-08-31], and Flux ships as a set of "Flux Controllers" [source: flux-concepts-2026-08-31]. Continuous integration is not part of the definition.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Name** the twelve factors, and say which ones Kubernetes hands you and which remain your application's problem
- **Distinguish** the two update strategies a Deployment implements from the release patterns that need tooling above it — blue/green and canary
- **State** the four OpenGitOps principles, and explain why a pipeline that pushes to a cluster satisfies none of the last two
- **Read** a delivery agent as what it structurally is: a controller, with its desired state in an unusual place
- **Explain** what `OutOfSync` reports, why it is a signal rather than an error, and why a person can cause one without anything failing
- **Say** what Argo CD does by default when it detects drift, and why that default is the right one
- **Recognize** the control loop from Chapter 3 wearing different clothes, and say exactly what changed and what did not

*You'll also stop thinking of GitOps as a deployment tool, which is the misreading this chapter exists to prevent.*

---

## ⚪ §1 — Twelve Factors, and the Ones Kubernetes Already Solved

Two chapters ago you were promised a methodology's word for a thing you already do. Chapter 4 promised it about configuration *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*, and Chapter 5 promised it about shutdown *[cross-bearing: see Ch 5 §4 — scheduled once, replaced never]*. Both promises point here.

The **twelve-factor app** is a methodology for building software delivered as a service. Its own summary is that a twelve-factor app uses declarative formats for setup automation, keeps a clean contract with the underlying operating system for portability, is suitable for deployment on modern cloud platforms, minimizes divergence between development and production, and can scale up without significant changes to tooling or architecture [source: twelve-factor-app-2026-08-23].

Read that list again and notice something: it predates Kubernetes and describes Kubernetes exactly.

<!-- AUTHOR-REVIEW: the previous draft said the methodology was "published in 2011", "drawn from experience running a large number of applications on a shared platform", and that it "predates Kubernetes by three years." None of those three facts appears in any cached snapshot — twelve-factor-app-2026-08-23 begins at "In the modern era, software is commonly delivered as a service" and carries no date, authorship, or provenance, and no snapshot carries Kubernetes's release date either. The claim has been reduced to the bare precedence relation, which the surrounding argument still supports. To restore the specifics, cache 12factor.net's Background section and a dated Kubernetes release reference. -->

That is not coincidence and it is not prophecy. Both came out of the same problem, running many applications reliably on shared infrastructure, and arrived at the same conclusions about what an application must do to be run that way.

Here are the twelve:

| | Factor | In one line |
|---|---|---|
| I | Codebase | One codebase tracked in revision control, many deploys |
| II | Dependencies | Explicitly declare and isolate dependencies |
| III | Config | Store config in the environment |
| IV | Backing services | Treat backing services as attached resources |
| V | Build, release, run | Strictly separate build and run stages |
| VI | Processes | Execute the app as one or more stateless processes |
| VII | Port binding | Export services via port binding |
| VIII | Concurrency | Scale out via the process model |
| IX | Disposability | Maximize robustness with fast startup and graceful shutdown |
| X | Dev/prod parity | Keep development, staging, and production as similar as possible |
| XI | Logs | Treat logs as event streams |
| XII | Admin processes | Run admin/management tasks as one-off processes |

[source: twelve-factor-app-2026-08-23]

Twelve numbered rules is a poor thing to memorize and a good thing to sort. The useful question is not "what is factor VII" but **who solves this**: the platform, or you.

<!-- FIGURE: ch15-fig01-twelve-factor-in-kubernetes -->
![Three columns sorting the twelve factors by who satisfies each. The platform gives you config, processes, concurrency, disposability and logs. The platform makes backing services, build/release/run and dev-prod parity easy. Codebase, dependencies, port binding and admin processes remain the application's problem.](figures/ch15-fig01-twelve-factor-in-kubernetes.svg)

<!-- ASCII-FALLBACK
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
-->

**Figure 15.1 — The twelve factors, sorted by who solves them.** The three columns are the argument: twelve unrelated-looking rules resolve into things the platform already does for you, things it removes the friction from, and things that remain entirely yours. The middle column is where most of the disappointment lives — Kubernetes makes dev/prod parity *achievable*, not automatic.

Four of these deserve development, because each one is a name for something you have already been taught.

### Factor III — Config

*"An app's config is everything that is likely to vary between deploys (staging, production, developer environments, etc)."* [source: twelve-factor-iii-config-2026-08-31]

The methodology's test for whether you have done this correctly is unusually sharp: *"A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials"* [source: twelve-factor-iii-config-2026-08-31]. That is a test you can run against your own repository this afternoon, and it is more honest than most compliance checklists.

The instruction is "store config in the environment," and this is where readers slip. It does **not** mean "put it in a config file." The document is explicit that a config file is an improvement over hard-coded constants but *"still has weaknesses: it's easy to mistakenly check in a config file to the repo"* [source: twelve-factor-iii-config-2026-08-31]. The prescription is environment variables, precisely because they live outside the codebase and are far less likely to be committed by accident. The methodology's own phrasing is that there is *"little chance of them being checked into the code repo accidentally"* [source: twelve-factor-iii-config-2026-08-31].

Kubernetes gives you this in the form you already know: ConfigMaps and Secrets, mounted as environment variables or as files *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. The object model was designed for factor III.

> 🪝 **Snag:** "Store config in the environment" is a claim about *where config lives relative to your code*, not about the literal `env:` block. A ConfigMap mounted as a file satisfies factor III perfectly well: the file is supplied by the deploy environment, not checked into the repository. Readers who take the phrase literally conclude that mounted-file config violates the methodology. It doesn't.

One more piece of factor III catches people, and it is worth carrying. The methodology objects to grouping variables into named environments: *"In a twelve-factor app, env vars are granular controls, each fully orthogonal to other env vars. They are never grouped together as 'environments', but instead are independently managed for each deploy"* [source: twelve-factor-iii-config-2026-08-31]. If you have ever watched a `staging` config bundle acquire a permanent, load-bearing difference from `production` that nobody remembers introducing, you have seen why.

### Factors VI and VIII — Processes and Concurrency

*"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service, typically a database"* [source: twelve-factor-vi-processes-2026-08-31].

This is the assumption underneath Deployments. A Deployment can replace any Pod with any other Pod because the methodology's constraint holds: no Pod is carrying anything the next one will need. Scale out by adding processes, which is factor VIII, and any process can serve any request.

The methodology bans one thing by name here: *"Sticky sessions are a violation of twelve-factor and should never be used or relied upon"* [source: twelve-factor-vi-processes-2026-08-31].

And when the constraint genuinely does not hold, when the replicas are *not* interchangeable, Kubernetes has a different object for you. It is a different object precisely because it is stepping outside this factor *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*.

### Factor IX — Disposability

Chapter 5 taught you `terminationGracePeriodSeconds` and the SIGTERM-then-SIGKILL sequence, and told you the word was coming. Here it is.

*"The twelve-factor app's processes are disposable, meaning they can be started or stopped at a moment's notice"* [source: twelve-factor-ix-disposability-2026-08-31]. The two halves are startup and shutdown. On startup: *"Processes should strive to minimize startup time. Ideally, a process takes a few seconds from the time the launch command is executed until the process is up and ready to receive requests or jobs."* On shutdown: *"Processes shut down gracefully when they receive a SIGTERM signal from the process manager"* [source: twelve-factor-ix-disposability-2026-08-31].

And a third clause, which is the one that matters most on a real cluster: *"Processes should also be robust against sudden death, in the case of a failure in the underlying hardware"* [source: twelve-factor-ix-disposability-2026-08-31]. Graceful shutdown is a courtesy the platform extends when it can. A node that loses power extends nothing.

> 🪢 **Mnemonic:** Disposability has two speeds and a floor. **Fast up** (seconds, not minutes). **Clean down** (handle SIGTERM). **Survive the floor dropping** (be correct even when neither happens).

### Factor XI — Logs

*"Logs are the stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services"* [source: twelve-factor-xi-logs-2026-08-31].

The rule is that the application does not participate in log management at all: *"A twelve-factor app never concerns itself with routing or storage of its output stream. Each running process writes its event stream, unbuffered, to stdout"* [source: twelve-factor-xi-logs-2026-08-31]. The execution environment captures the stream, collates it with every other stream from the app, and routes it onward [source: twelve-factor-xi-logs-2026-08-31].

That is exactly why `kubectl logs` works on every container without any container being configured for it, and it is why cluster-wide log collection can be a node-level concern rather than an application concern *[cross-bearing: see Ch 18 §6 — lines from everywhere]*.

> ★ **Fixed Point**
>
> **The twelve-factor app is a set of constraints an application accepts in exchange for being run by a platform. Kubernetes implements the platform side — config injection, stateless replication, graceful termination, log collection. It cannot implement the application side. An application that writes its own log files, keeps session state in memory, or takes ninety seconds to start is not made twelve-factor by being containerized.**

Twelve-factor is also a predecessor of vocabulary you will meet later. When Chapter 17 lists the characteristics of cloud native systems, several of them are these factors under newer names *[cross-bearing: see Ch 17 §3 — small pieces, replaced whole]*.

---

## 🔵 §2 — Ways to Replace What's Running

Chapter 6 taught you the mechanics of replacing a running fleet: `RollingUpdate` and `Recreate`, `maxSurge` and `maxUnavailable`, pause and resume *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*. This section does not restate any of it. What it adds is the vocabulary: the names practitioners use for release patterns, the trade-off each one makes, and one line that readers persistently get wrong.

The line is this.

> ★ **Fixed Point**
>
> **`RollingUpdate` and `Recreate` are values of a field on a Deployment. Blue/green and canary are patterns that require tooling above the Deployment object. A Deployment cannot express either one on its own.**

Chapter 6 named the second group and deferred them. They arrive now.

### The umbrella: progressive delivery

The term that covers the whole family is **progressive delivery**: *"the process of releasing updates of a product in a controlled and gradual manner, thereby reducing the risk of the release, typically coupling automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23].

Note the two halves of that definition. *Gradual* is the visible part. *Metric analysis driving automated promotion or rollback* is the part that makes it more than a slow deploy: the release watches itself.

### The four, and what each costs

**Recreate.** *"A Recreate deployment deletes the old version of the application before bringing up the new version. As a result, this ensures that two versions of the application never run at the same time, but there is downtime during the deployment"* [source: argo-rollouts-strategies-2026-08-23].

The trade is stated in the definition: you accept downtime and you get the guarantee that two versions never coexist. That guarantee is not a consolation prize. If the new version runs a schema migration the old version cannot read, coexistence is the failure mode, and Recreate is the correct choice rather than the lazy one.

**RollingUpdate.** *"A RollingUpdate slowly replaces the old version with the new version. As the new version comes up, the old version is scaled down in order to maintain the overall count of the application. This is the default strategy of the Deployment object"* [source: argo-rollouts-strategies-2026-08-23].

No downtime, and the exact inverse guarantee: both versions serve traffic simultaneously, for the duration. Your application must tolerate that.

**Blue/green.** Two complete environments. CNCF's glossary describes the operator maintaining two environments, "blue" and "green," with one serving live production traffic while the other is updated; after testing on the inactive environment, traffic switches via load balancer [source: cncf-glossary-blue-green-deployment-2026-08-31]. Argo's description agrees and adds the reason: *"During this time, only the old version of the application will receive production traffic. This allows the developers to run tests against the new version before switching the live traffic to the new version"* [source: argo-rollouts-strategies-2026-08-23].

The cost is capacity. You run two full copies. What you buy is the ability to test the new version *in production, with production configuration and production backing services*, before a single user reaches it. The cutover is one moment rather than a gradual mix, which means the rollback is also one moment.

CNCF's glossary adds an assessment worth reading, because it is more critical than most vendor material: blue/green *"is an appropriate strategy for non-cloud native software that needs to be updated with minimal downtime. However, its use is normally a 'smell' that legacy software needs to be re-engineered so that components can be updated individually"* [source: cncf-glossary-blue-green-deployment-2026-08-31]. The glossary notes the term is typically applied to whole systems with multiple services updated in lockstep, and is sometimes misapplied to individual services [source: cncf-glossary-blue-green-deployment-2026-08-31].

**Canary.** *"A Canary deployment exposes a subset of users to the new version of the application while serving the rest of the traffic to the old version. Once the new version is verified to be correct, the new version can gradually replace the old version"* [source: argo-rollouts-strategies-2026-08-23]. Argo Rollouts states the same idea from the operator's side: *"a canary rollout is a deployment strategy where the operator releases a new version of their application to a small percentage of the production traffic"* [source: argo-rollouts-canary-2026-08-31].

CNCF's glossary is blunt about why anyone bothers: *"No matter how thorough the testing strategy, there are always some bugs discovered in production. Shifting 100% of traffic from one version of an app to another can lead to more impactful failures"* [source: cncf-glossary-canary-deployment-2026-08-31].

The cost is infrastructure. Canary needs something that can split traffic by proportion, and something that can judge whether the small proportion is going well. Argo's comparison states this directly: canary strategies *"offer greater flexibility but demand more infrastructure (traffic-splitting via a service mesh or ingress controller) and metric analysis; Blue/Green needs no traffic provider and suits workloads such as queue workers"* [source: argo-rollouts-strategies-2026-08-23].

That last clause is the practical answer to "which one." A queue worker has no inbound traffic to split. Canary is not a better blue/green; it is a different tool that needs a request path to work on *[cross-bearing: see Ch 10 §3 — the object is not the implementation]* *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*.

<!-- FIGURE: ch15-fig02-deployment-strategies-compared -->
![Four release strategies in two groups. The upper group, fields on a Deployment, holds Recreate with a gap where neither version serves, and RollingUpdate with both versions overlapping throughout. The lower group, patterns needing tooling above it, holds blue/green with a single switch line and two-times capacity, and canary stepping five to twenty-five to fifty to one hundred percent and needing traffic splitting plus metric analysis.](figures/ch15-fig02-deployment-strategies-compared.svg)

<!-- ASCII-FALLBACK
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

  filled = that row's version is serving traffic;  empty = it is not
```
-->

**Figure 15.2 — Four ways to replace what's running.** The two enclosures carry the point: the top pair are values you set on a Deployment, and the bottom pair are patterns something else has to implement for you. The footer rows are the actual decision criteria — what each strategy demands before you can use it at all.

> ⚓ **Worth Securing:** My own read, from watching teams choose: blue/green usually wins over canary for infrastructure reasons rather than risk reasons. And the mechanical half of that is not opinion. If there is no service mesh and no metrics pipeline wired to the release, canary is not on the menu at all, because canary *"demand[s] more infrastructure (traffic-splitting via a service mesh or ingress controller) and metric analysis"* [source: argo-rollouts-strategies-2026-08-23]. Knowing *why* a team runs blue/green tells you more about their platform than about their risk appetite.

### One term this book will not teach you

You may have heard **A/B testing** listed alongside these four. This book leaves it out deliberately, and the reason is a real distinction rather than an omission.

A/B testing appears in Argo's documentation not as a rollout strategy but as a use of a separate resource: *"A user can use experiments to enable A/B/C testing by launching multiple experiments with a different version of their application for a long duration"* [source: argo-rollouts-experiments-2026-08-31]. It is product experimentation. You are measuring which version users prefer, over a long duration, on purpose. The four strategies above are release mechanics: you are measuring whether the new version is *broken*, for as short a duration as you can manage. Delivery tooling can implement both, which is why they end up in the same lists, but they answer different questions.

Nothing in this chapter's questions turns on A/B testing.

> 🔭 **Closer Look:** One vocabulary note, for readers with a good memory. Chapter 6 called these "release strategies" *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*. This book's headword is **deployment strategy**, and the reason is crowding: "release" already carries two other meanings here, a Kubernetes minor version and a Helm release *[cross-bearing: see Ch 14 §3 — chart, release, revision]*. Three senses of one word across two adjacent chapters is one too many. Both phrases name the same thing; if you meet "release strategy" in the field, it is this.

---

## ☆ Taking Your Bearings 1: The Application, and the Shapes of a Release

Six questions. Two of them reach back to earlier chapters. Those are marked, and they are marked because they are the point.

**1.** An application stores uploaded files on the local filesystem of whichever Pod handled the upload. Which twelve-factor factor does this violate, and what does it break in Kubernetes specifically?

**2.** A team stores its production database password in a file called `config/production.yml`, committed to the application repository, and reads it at startup. Apply the twelve-factor litmus test. What does it say?

**3.** [retrieval: ch4] Your application needs a different API endpoint URL in staging than in production, and the same container image must run in both. Name two Kubernetes mechanisms that deliver that URL to the running container, and say where the value physically lives in each case.

**4.** [retrieval: ch6] During a `RollingUpdate` on a Deployment with 10 replicas, `maxSurge: 2` and `maxUnavailable: 1`. What is the maximum number of Pods that may exist at any moment during the update, and the minimum number that may be available?

**5.** A team wants to release a new version to 5% of users, watch error rates for twenty minutes, and automatically abort if errors rise. Their workload is an HTTP API behind an Ingress. Which strategy is this, and what must already exist in the cluster for it to be possible?

**6.** Which of these is a value you can set on a Deployment's update-strategy field, and which requires additional tooling: `Recreate`, blue/green, `RollingUpdate`, canary?

---

<details>
<summary>Answers with explanations</summary>

**1. Factor VI (Processes — stateless and share-nothing).** The twelve-factor rule is that *"any data that needs to persist must be stored in a stateful backing service"* [source: twelve-factor-vi-processes-2026-08-31]. What it breaks in Kubernetes: a Deployment replaces any Pod with any other Pod, and a request that retrieves the file may land on a replica that never had it. Worse, the Pod's writable layer is destroyed when the Pod is, so the data is not merely misplaced. It is gone at the next rollout, node drain, or eviction.

**Why not "factor IX, disposability"?** Tempting, and adjacent. A Pod holding unique data is certainly not disposable. But IX is about *startup and shutdown behavior*; the root violation is holding state at all, which is VI.

**2. It fails.** The test is whether *"the codebase could be made open source at any moment, without compromising any credentials"* [source: twelve-factor-iii-config-2026-08-31]. Publishing this repository publishes the production database password. The methodology anticipates exactly this: a config file is better than a hard-coded constant, but *"it's easy to mistakenly check in a config file to the repo"* [source: twelve-factor-iii-config-2026-08-31] — and here it wasn't even a mistake, it was the design.

**3. [retrieval: ch4] ConfigMap and Secret.** Either can be surfaced to the container as environment variables or mounted as files. Where the value lives: in the cluster, as an object in etcd, entirely outside the image. The image is identical in both environments; the object differs. That separation is what allows one tested artifact to run everywhere *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*.

**Common wrong answer:** "build two images with different baked-in values." This is the failure factor III exists to name. You are now shipping an artifact you did not test, because the thing you tested was the other image.

**4. Maximum 12 Pods; minimum 9 available.** `maxSurge: 2` permits two Pods above the desired count of 10. `maxUnavailable: 1` permits one below it. The two are independent caps, not a single budget: the controller may be simultaneously two over and one unavailable, which is what makes the update proceed at all *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*.

**Why "11 and 10" is wrong:** that reads `maxSurge` and `maxUnavailable` as if only one could be in effect. Both apply throughout.

**5. Canary.** The tell is the *proportion* of traffic plus *automated abort on a metric*. That is progressive delivery's definition, *"coupling automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23].

What must already exist: something that can split traffic by weight, a service mesh or an ingress controller, and a metrics system the release logic can query [source: argo-rollouts-strategies-2026-08-23]. Without traffic splitting there is no way to send 5% anywhere; without metrics there is nothing to abort on.

**6. `Recreate` and `RollingUpdate` are Deployment strategy values. Blue/green and canary require tooling above the Deployment.** This is the section's Fixed Point and the distinction most likely to be tested from this material. `RollingUpdate` *"is the default strategy of the Deployment object"* [source: argo-rollouts-strategies-2026-08-23]; the other two are patterns implemented by controllers that manage Deployments or replace them.

---

**If you got 5–6:** You have the application layer. §3 changes subject entirely: it stops asking what to deploy and starts asking who does it.

**If you got 3–4:** Solid. Re-read the answer to whichever you missed; the reasoning matters more than the fact.

**If you got 0–2:** Re-read **§1's factor III** and **§2's Fixed Point** before continuing. Those two ideas get used again in §3 and §4 without reintroduction.

</details>

---

## 🔵 §3 — Push, or Pull

This is the chapter's central argument, and it begins with a fact that clears the ground.

Kubernetes *"does not deploy source code and does not build your application. Continuous Integration, Delivery, and Deployment (CI/CD) workflows are determined by organization cultures and preferences as well as technical requirements"* [source: k8s-docs-overview-2026-08-23].

That is the documentation's own list of what Kubernetes is not, and it settles something. The cluster is indifferent to who builds your artifact and how. It receives objects through its API and reconciles them. Everything before that — compiling, testing, packaging, tagging — happens elsewhere, by arrangement. Chapter 4 told you this in passing *[cross-bearing: see Ch 4 §1 — you file a declaration]*; here it becomes load-bearing.

### The three letters, expanded

The abbreviation bundles three practices that are worth separating, since the exam-relevant distinctions live in the gaps between them.

**CI — continuous integration.** *"The practice of integrating code changes as regularly as possible"* [source: cncf-glossary-continuous-integration-2026-08-31]. In practice this means a server that checks every commit merges cleanly, runs quality checks and tests, and, as CNCF puts it, *"allows software teams to turn every code commit into either a concrete failure or a viable release candidate"* [source: cncf-glossary-continuous-integration-2026-08-31].

**CD — continuous delivery.** *"A set of practices in which code changes are automatically deployed into an acceptance environment (or, in the case of continuous deployment, into production)"* [source: cncf-glossary-continuous-delivery-2026-08-31]. It includes procedures ensuring software is adequately tested before deployment, and a way to roll changes back if needed [source: cncf-glossary-continuous-delivery-2026-08-31].

**CD — continuous deployment.** *"Goes a step further than continuous delivery by deploying finished software directly to production"* [source: cncf-glossary-continuous-deployment-2026-08-31].

> 🪝 **Snag:** CNCF abbreviates *both* continuous delivery and continuous deployment as "CD" [source: cncf-glossary-continuous-delivery-2026-08-31] [source: cncf-glossary-continuous-deployment-2026-08-31]. This is genuinely ambiguous in the field, not just on paper. When the distinction matters, and it matters when the question is whether a human approves the production step, spell the word out.

### The architectural question

Now the question this section exists for. An artifact has been built. Something must apply it to a cluster. There are two arrangements, and they differ in a way that is not a matter of taste.

**Push.** A pipeline runs outside the cluster. It holds credentials *to the cluster*. When it finishes building, it reaches inward across the cluster boundary and applies the manifests. This is what most teams do first, because it is the obvious extension of a build pipeline: the pipeline already has the artifact, so give it the ability to install the artifact.

**Pull.** An agent runs *inside* the cluster. It holds credentials *to a repository*. It reaches outward, fetches the desired state, and applies it locally. Nothing outside the cluster holds cluster credentials, because nothing outside the cluster needs them.

<!-- FIGURE: ch15-fig03-cicd-push-vs-gitops-pull -->
![Two mirrored panels sharing one cluster boundary. In push, a pipeline outside the boundary holds the key and reaches inward to the API server. In pull, a repository outside the boundary holds no key while an agent inside the boundary holds the key, reaching outward to fetch from the repository and inward to the API server.](figures/ch15-fig03-cicd-push-vs-gitops-pull.svg)

<!-- ASCII-FALLBACK
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
-->

**Figure 15.3 — Push and pull, mirrored.** The cluster boundary is the same line in both panels and the arrow is the only thing that reverses. Watch the key: in push it sits outside the boundary, in a system the cluster does not control. In pull it sits inside, in a Pod the cluster does control. Everything else in this section is a consequence of that one difference.

Four consequences follow, and none of them is subtle once you look.

**A note on what follows.** The four consequences below are **this book's reading** of principle 3 combined with the two projects' documented credential storage, not a comparison any cached source makes in these terms. No CNCF or vendor document in this chapter's corpus argues push-versus-pull as a security question. Where a consequence can be anchored to a source, it is tagged; where it cannot, it is the book's argument and you should weigh it as such.

**Where the credentials sit.** In push, a set of cluster-write credentials lives in your CI system: in its secret store, readable by its jobs, and often by anyone who can edit a pipeline definition. In pull, they live in a Kubernetes Secret in the cluster they apply to. Argo CD, for instance, *"stores the credentials of the external cluster as a Kubernetes Secret in the argocd namespace"* [source: argocd-security-cluster-credentials-2026-08-31] *[cross-bearing: see Ch 12 §4 — secrets are not encrypted]*.

There is one thing the corpus does say in this neighborhood, and it is worth having. Argo CD's best-practices page argues for separating the config repository from the source repository partly on access grounds: *"The developers who are developing the application, may not necessarily be the same people who can/should push to production environments"* [source: argocd-best-practices-2026-08-31]. That is the access-separation instinct that push-based delivery tends to collapse and pull-based delivery tends to preserve.

**What a compromise gets.** This is the sharper version of the same point, and it is entirely the book's inference. Compromise a push pipeline and you have write access to every cluster it deploys to, which for a shared CI system may be all of them. Compromise a pull agent and you have one cluster, the one you were already inside. This book calls that reach the **blast radius**: how far the damage from a single compromise extends. Pull does not prevent compromise. It bounds it.

**What happens between deploys.** In push, nothing. The pipeline runs, exits, and the cluster is on its own until the next commit. In pull, the agent is still running. It is still comparing. CNCF's glossary names exactly this as the problem GitOps addresses, listing configuration drift first among them and observing that *"configuration drift can be hard to detect and resolve without a source of truth governing it"* [source: cncf-glossary-gitops-2026-08-31]. This is the difference that turns out to matter most, and §4 is about what an agent does with the comparison.

**What "the truth" means.** In push, the authoritative answer to "what is supposed to be running" is whatever the last pipeline applied, a fact you must reconstruct from build logs. In pull, it is a file, in a repository, that anyone can read, with a history showing every previous answer.

> **Logbook Entry:** There is a version of this story on every platform team.
>
> The incident is small. A service is misbehaving on Friday afternoon, somebody with cluster access finds the cause, and fixes it directly: one field, one `kubectl edit`, thirty seconds. The service recovers. It is genuinely the right call in the moment; the alternative is a code review at 6pm.
>
> The fix is correct and it is also invisible. It exists nowhere except in the cluster's own state. Nobody writes it down, because writing it down was the slow path they were avoiding.
>
> Six weeks later somebody deploys a routine change to the same service. The deployment applies the manifests from the repository, which have never known about the Friday fix. The field reverts. The original problem returns, now with six weeks of distance between cause and effect, and a change log pointing at an unrelated commit.
>
> Push-based delivery has no mechanism that would have caught this. The pipeline was not running for those six weeks and had nothing to compare against if it had been. The gap between what the repository said and what the cluster contained was real, persistent, and completely silent.
>
> Keep this story in mind through §4. The mechanism that catches it has a name, and it is not an alarm.

### GitOps

**GitOps** is the name for the pull arrangement done rigorously. The definition is not a vendor's; it comes from OpenGitOps, a CNCF project, and it is four principles rather than a description of tooling.

*"GitOps is a set of principles for operating and managing software systems."* The desired state of a GitOps-managed system must be:

1. **Declarative** — *"A system managed by GitOps must have its desired state expressed declaratively."*
2. **Versioned and Immutable** — *"Desired state is stored in a way that enforces immutability, versioning and retains a complete version history."*
3. **Pulled Automatically** — *"Software agents automatically pull the desired state declarations from the source."*
4. **Continuously Reconciled** — *"Software agents continuously observe actual system state and attempt to apply the desired state."*

[source: opengitops-principles-v1-2026-08-31]

<!-- FIGURE: ch15-fig05-opengitops-four-principles -->
![Four boxes in a two-by-two grid, one per OpenGitOps principle. Declarative is tagged you know this, chapter 4 section 1. Versioned and immutable is tagged NEW HERE. Pulled automatically is tagged chapter 3 section 5. Continuously reconciled is tagged chapter 3 section 6. Only the second principle is new.](figures/ch15-fig05-opengitops-four-principles.svg)

<!-- ASCII-FALLBACK
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
-->

**Figure 15.4 — The four principles, and where you already met three of them.** The markers in each block are the figure's real content. Only principle 2 is new to you. The rest is Chapter 4's declarative model and Chapter 3's watch-and-reconcile architecture, restated with the desired state living somewhere else. Hold that thought; §7 collects on it.

Two of the four carry the weight, and both are places readers go wrong.

**Principle 3 is why push-based CD is not GitOps.** The word is *pulled*. Agents fetch the declarations; nothing hands the declarations to them. OpenGitOps states it as an active property of the agent: *"Software agents automatically pull the desired state declarations from the source"* [source: opengitops-1-0-announcement-2026-08-31]. A pipeline that stores manifests in Git and then pushes them into a cluster satisfies principles 1 and 2 and fails 3 and 4 completely. It is a perfectly reasonable thing to build. It is not GitOps, and calling it GitOps loses the distinction that the term exists to make.

The project is unusually explicit that this precision was deliberate: *"The wording of each principle and linked glossary item was very carefully chosen"* [source: opengitops-1-0-announcement-2026-08-31].

**Principle 4 is why GitOps is not a deploy-time event.** *Continuously* observe. Not "observe at deploy time," not "observe when triggered." The agent is described as having an ongoing obligation: *"The GitOps software agents have to be aware of the actual state of a system under management and attempt to apply the desired state"* [source: opengitops-1-0-announcement-2026-08-31].

OpenGitOps names the thing this catches. **Drift** is *"when a system's actual state has moved or is in the process of moving away from the desired state…"* [source: opengitops-glossary-2026-08-31] — the ellipsis is the snapshot's, and the definition it carries is partial. **Reconciliation** is *"the process of ensuring the actual state of a system matches its desired state"* [source: opengitops-glossary-2026-08-31].

CNCF's own glossary entry for GitOps names drift first among the problems the practice addresses, alongside failed deployments, inconsistent environments, and difficulty tracking historical changes [source: cncf-glossary-gitops-2026-08-31].

> 🔭 **Closer Look:** "GitOps" names Git, but the principles do not require it. OpenGitOps says so: *"many version control systems can be used in GitOps as long as they meet those two basic requirements and teams use them in a conformant manner"* [source: opengitops-1-0-announcement-2026-08-31]. The announcement does not restate which two requirements it means; on this book's reading they are principle 2's immutability and complete version history, which is the only pair the principles state about the store itself. Git is, in practice, the overwhelmingly common choice. The definition is about the properties, not the tool.

### One thing GitOps does not do

Before §4 makes this concrete, kill a misreading that the phrase "the repository is the source of truth" invites.

> ⚠ **Navigational Hazards**
>
> A GitOps agent does **not** write to the cluster's datastore directly, and does not bypass the API server.
>
> Chapter 3 made a claim about this architecture that has held for twelve chapters: the API server is the only thing that mutates cluster state, and every actor — kubectl, the scheduler, every controller — goes through it *[cross-bearing: see Ch 3 §5 — the only door in]*. A delivery agent is an API client like any other. Its requests pass through authentication, then authorization, then admission, in that order, exactly as yours do *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*.
>
> **Where this goes wrong:** readers hear "the repository is the source of truth" and picture the repository *replacing* etcd, as though desired state now lives in Git instead of in the cluster. It does not. etcd still holds every object. What Git holds is the *authored* desired state, upstream of the cluster, and the agent's job is to keep the two in agreement by making ordinary API calls.
>
> The consequence you can act on: an agent that lacks RBAC permission to create a resource will fail to create it, with an ordinary authorization error. GitOps grants no exemption from any cluster control. If anything it is *more* constrained than a human operator, because its permissions are written down.

Which raises the question §4 opens with: what is this agent, exactly?

---

## 🔵 §4 — An Agent That Watches a Repository

**Argo CD** is a *"declarative, GitOps continuous delivery tool for Kubernetes"* [source: argocd-overview-2026-08-23]. You have met the name once already, in Chapter 3, where it appeared as a promise about a sentence this chapter would retrieve *[cross-bearing: see Ch 3 §5 — the only door in]*.

Here is that sentence, and it is the most important one in the section.

The Argo CD application controller *"is a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the repo)"* [source: argocd-architecture-2026-08-31].

Read it as three separate claims:

- *is a Kubernetes controller* — the thing Chapter 3 §6 defined
- *continuously monitors and compares current against desired* — the thing Chapter 3 §6 said controllers do
- *desired target state as specified in the repo* — the only part that is new

Chapter 6 told you that anyone can write a controller acting on custom resources *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. Somebody did. This is what it looks like.

> ★ **Fixed Point**
>
> **A GitOps delivery agent is a controller. Its desired state lives in a repository instead of in etcd. Nothing else about the architecture is different — not the API server's position, not the watch-based coordination, not the shape of the loop.**

### The object model

Argo CD's own glossary defines the pieces, and the vocabulary is worth getting exactly right because the words are ordinary English used precisely.

**Application** — *"A group of Kubernetes resources as defined by a manifest. This is a Custom Resource Definition (CRD)"* [source: argocd-core-concepts-2026-08-31]. More precisely: *"The Application CRD is the Kubernetes resource object representing a deployed application instance in an environment"* [source: argocd-declarative-setup-2026-08-31].

An `Application` is defined by two pieces of information: a *"source reference to the desired state in Git (repository, revision, path, environment)"* and a *"destination reference to the target cluster and namespace"* [source: argocd-declarative-setup-2026-08-31]. That is the whole contract: *this content, from there, goes there*.

**Target state** — *"The desired state of an application, as represented by files in a Git repository."*
**Live state** — *"The live state of that application. What pods etc are deployed."*
**Sync status** — *"Whether or not the live state matches the target state. Is the deployed application the same as Git says it should be?"*
**Sync** — *"The process of making an application move to its target state. E.g. by applying changes to a Kubernetes cluster."*
**Refresh** — *"Compare the latest code in Git with the live state. Figure out what is different."*

[source: argocd-core-concepts-2026-08-31]

Notice that refresh and sync are separate words. Refresh compares. Sync acts. A system can know it is out of agreement without doing anything about it, and whether it acts is a policy decision, which, as you are about to see, has a documented default that surprises people.

> ⚓ **Worth Securing:** If you find yourself confusing *live state* and *target state* under pressure, anchor them to Chapter 4. **Target state is `spec`, kept outside the cluster. Live state is what `status` reports.** Argo CD's central comparison is the one you have been reading since Chapter 4, with one operand relocated *[cross-bearing: see Ch 4 §2 — the anatomy of a record]*.

### Where the manifests come from

An `Application`'s source is a repository path, but the content at that path need not be plain YAML. Argo CD accepts manifests specified *"in several ways: kustomize applications; helm charts; jsonnet files; plain directory of YAML/json manifests; any custom config management tool configured as a config management plugin"* [source: argocd-overview-2026-08-23].

Argo CD's glossary has a word for this choice: the **application source type** is *"which Tool is used to build the application,"* where a **tool** is *"a tool to create manifests from a directory of files. E.g. Kustomize"*, and a **configuration management plugin** is simply *"a custom tool"* [source: argocd-core-concepts-2026-08-31].

This is where the previous chapter's work gets collected. A Helm chart is a manifest source for a GitOps agent *[cross-bearing: see Ch 14 §2 — what a chart contains]*. So is a Kustomize overlay *[cross-bearing: see Ch 14 §5 — patching instead of templating]*. Chapter 14 gave you packaging; this chapter gives packaging somewhere to go. The agent renders the chart or builds the overlay, and compares the *result* against the cluster.

> 🪝 **Snag:** "Argo CD only deploys plain YAML" is a common and confident mistake, and it usually comes from having seen one tutorial. The tool's whole design assumes a rendering step: a dedicated component, the repository server, *"maintains a local cache of the Git repository holding the application manifests"* and is responsible for *"generating and returning the Kubernetes manifests"* given a repository URL, a revision, a path, and template-specific configuration [source: argocd-architecture-2026-08-31]. Rendering is not an add-on. It is a whole component.

### What it tracks

An `Application` names a revision as well as a repository, and there are three kinds of thing that revision can be. Argo CD's tracking documentation is precise about the difference, and the difference is about stability.

A **branch or symbolic reference** (including `HEAD`): *"Argo CD will continually compare live state against the resource manifests defined at the tip of the specified branch or the resolved commit of the symbolic reference"* [source: argocd-tracking-strategies-2026-08-31]. The tip moves; so does your target.

A **tag**: *"If a tag is specified, the manifests at the specified Git tag will be used to perform the sync comparison."* Tags are *"generally considered more stable, and less frequently updated"* than branches [source: argocd-tracking-strategies-2026-08-31].

A **pinned commit**: *"If a Git commit SHA is specified, the app is effectively pinned to the manifests defined at the specified commit."* And the consequence: *"Since commit SHAs cannot change meaning, the only way to change the live state of an app which is pinned to a commit, is by updating the tracking revision in the application to a different commit containing the new manifests"* [source: argocd-tracking-strategies-2026-08-31].

That last sentence is principle 2, versioned and immutable, showing up as an operational property rather than an abstraction. Argo CD's own best-practices documentation makes the same argument against tracking an unstable revision: *"Since this is not a stable target, the manifests for this kustomize application can suddenly change meaning, even without any changes to your own Git repository. A better version would be to use a Git tag or commit SHA"* [source: argocd-best-practices-2026-08-31].

> 🪢 **Mnemonic:** **Branch moves. Tag rarely moves. Commit never moves.** Pick according to how much you want the deck under your production cluster to shift without a commit of your own.

### Synced, and OutOfSync

Now the section's second Fixed Point, and the one most likely to be tested from this material.

*"A deployed application whose live state deviates from the target state is considered OutOfSync"* [source: argocd-overview-2026-08-23]. Argo CD *"reports and visualizes the differences, while providing facilities to automatically or manually sync the live state back to the desired target state"* [source: argocd-overview-2026-08-23].

> ★ **Fixed Point**
>
> **`OutOfSync` means live state deviates from the target state in Git. It is a drift signal, not an error. Nothing has necessarily failed. A person editing an object by hand produces an `OutOfSync` application, and so does a commit that has not been applied yet.**

Argo CD's glossary keeps these on separate lines for exactly this reason. **Sync status** answers *"is the deployed application the same as Git says it should be?"* A separate item, **sync operation status**, answers *"whether or not a sync succeeded"* [source: argocd-core-concepts-2026-08-31]. Two questions. Two answers. A sync can succeed and leave the application `OutOfSync`; the documentation says so outright: *"It is possible for an application to be `OutOfSync` even immediately after a successful Sync operation"* [source: argocd-diffing-outofsync-2026-08-31].

<!-- AUTHOR-REVIEW: argocd-diffing-outofsync-2026-08-31 quotes the claim above but its capture note says the page's enumerated causes (unknown fields, pruning disabled, mutating controllers/webhooks, Helm template functions, HPA metric reordering) were returned as summary rather than quotation and must not be attributed to that snapshot. The claim is therefore stated without its causes, which weakens it. A fetch of the full diffing page would let §4 name at least one concrete cause. -->

Return to the Logbook Entry in §3. Friday afternoon, one field, thirty seconds, invisible for six weeks. Under a GitOps agent, that edit produces an `OutOfSync` status within one reconciliation interval. Not an alert, not a page, not a failure. A status field, changed, saying *these two things no longer agree*. The mechanism that catches the story is not an alarm. It is a comparison that never stops running.

<!-- FIGURE: ch15-fig04-argocd-sync-states-and-hooks -->
![Two scenarios comparing target state in a Git repository against live state in a cluster, with an agent between them observing both. In the first, both say replicas three and the status is Synced. In the second, the repository still says three but the cluster says five because someone ran kubectl scale, and the status is OutOfSync; a separate sync operation applies the target state and the two match again.](figures/ch15-fig04-argocd-sync-states-and-hooks.svg)

<!-- ASCII-FALLBACK
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
-->

**Figure 15.5 — The comparison, and the two answers it produces.** The lower panel shows the cause readers do not expect: nothing failed, no deploy went wrong, a person changed the cluster. `OutOfSync` reports the disagreement. Sync is the separate operation that closes it — and, by default, a separate *decision*.

### Doing something about it

Reporting a difference and correcting it are separate decisions, and Argo CD keeps them separate, including in what it does when you say nothing.

*"Argo CD has the ability to automatically sync an application when it detects differences between the desired manifests in Git, and the live state in the cluster"* [source: argocd-auto-sync-policy-2026-08-31]. That ability is configured declaratively, which is itself in keeping, since the agent's own behavior is a field on an object in the repository.

Now the part that catches people, and it is the strongest evidence in the chapter for the Fixed Point you just read.

> ⚠ **Navigational Hazards**
>
> **Out of the box, Argo CD reports drift. It does not revert it.**
>
> Two behaviors that readers assume are automatic are documented as opt-in:
>
> - **Self-healing is off by default.** *"By default, changes that are made to the live cluster will not trigger automated sync"* [source: argocd-auto-sync-policy-2026-08-31]. **Self-heal** is the name for the agent correcting drift it detects in the cluster, rather than only responding to new commits, and until you enable it, a hand-edited object stays hand-edited.
> - **Pruning is off by default.** *"By default (and as a safety mechanism), automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git"* [source: argocd-auto-sync-policy-2026-08-31]. Delete a manifest from the repository and the object stays on the cluster until pruning is enabled.
>
> Two further facts worth carrying. Automated sync fires only on a difference: *"An automated sync will only be performed if the application is `OutOfSync`"* [source: argocd-auto-sync-policy-2026-08-31]. And the cadence is not instantaneous: the automated sync interval *"defaults to `120s` with added jitter of `60s` for a maximum period of 3 minutes"* [source: argocd-auto-sync-policy-2026-08-31].
>
> **Where people get confused:** §6 will tell you that Flux *"promptly reverts"* a manual `kubectl` change [source: flux-concepts-2026-08-31], and it is tempting to generalize that into "GitOps agents revert manual edits." Two graduated implementations of the same four principles ship with different defaults here. Principle 4 requires continuous *observation*; what the agent then *does* about a difference is configuration, and the two projects choose oppositely out of the box.

That default is worth pausing on rather than merely noting, because it is the Fixed Point's best proof. If `OutOfSync` were an error, a tool would not sit there reporting it. Argo CD's out-of-the-box behavior treats it as exactly what the Fixed Point says it is: a report that two things differ, handed to a human who decides what that means.

Beyond automated sync sit two related behaviors, both named in the feature list: **automated configuration drift detection and visualization**, and **automated or manual syncing of applications to its desired state** [source: argocd-overview-2026-08-23]. CNCF's glossary lists self-healing among GitOps's characteristic benefits, alongside *"transparency and traceability of changes, reliability and security through declarative states, and rollback, revert"* [source: cncf-glossary-gitops-2026-08-31], which brings us to the third thing in this book to wear a familiar word.

### Rollback, for the third time

Chapter 6 promised you this. When it taught `kubectl rollout undo`, it said the word would appear twice more, and that the second occasion would be a delivery tool *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*. Chapter 14 spent the first *[cross-bearing: see Ch 14 §3 — chart, release, revision]*. This is the second and last.

Argo CD offers *"rollback/roll-anywhere to any application configuration committed in Git repository"* [source: argocd-overview-2026-08-23].

Look at what is actually happening. You do not invoke a rollback subsystem. You change what the repository says, typically with `git revert`, producing a new commit whose content is the old content, and the agent does what it has been doing continuously since it started: it notices the target moved, and it closes the gap. The rollback mechanism *is* the sync mechanism. There is no second code path.

| | What moves | Where the previous state was kept |
|---|---|---|
| `kubectl rollout undo` (Ch 6 §5) | The Deployment's Pod template | In the old ReplicaSet, on the cluster |
| `helm rollback` (Ch 14 §3) | The Helm release to a prior revision | In Helm's release history, on the cluster |
| **Rollback by revert** (here) | A commit in the repository | In the repository's history |

Three mechanisms, one English word. This book writes the third as **rollback by revert**, always in that three-word form, so that it cannot be confused with the other two.

> 🪝 **Snag:** Do not call the thing you revert a "revision." In this book, *revision* has two owners already: a Deployment revision *[cross-bearing: see Ch 6 §5 — every rollout is a revision]* and a Helm release revision *[cross-bearing: see Ch 14 §3 — chart, release, revision]*. A Git revision is a **commit**. Argo CD's own API field happens to be called `revision`, which is why this needs saying rather than assuming.

### The agent's own identity

One thing remains, and two earlier chapters pointed at it explicitly *[cross-bearing: see Ch 5 §6 — a Pod's identity]* *[cross-bearing: see Ch 12 §2 — who you are]*.

A delivery agent is a Pod. A Pod that talks to the API server needs an identity, and in Kubernetes that identity is a ServiceAccount. The Kubernetes documentation lists this among the reasons non-human identities exist at all: *"an external service needs to communicate with the Kubernetes API server (CI/CD pipelines)"* [source: k8s-docs-service-accounts-2026-08-23].

Then ask what this particular Pod does for a living. It creates, updates, and deletes objects — Deployments, Services, ConfigMaps, RBAC objects, custom resources — across many namespaces, on behalf of whatever is committed to a repository. Its grants must be broad, because "apply whatever the repository says" is a broad job description.

Argo CD's security documentation states the default plainly: *"By default, Argo CD uses a clusteradmin level role in order to: 1. watch & operate on cluster state 2. deploy resources to the cluster"* [source: argocd-security-cluster-credentials-2026-08-31].

The same documentation immediately supplies the reduction: *"Although Argo CD requires cluster-wide read privileges to resources in the managed cluster to function properly, it does not necessarily need full write privileges to the cluster."* Operators may edit the ClusterRole of `argocd-manager-role` *"such that write privileges are limited to only the namespaces and resources that you wish Argo CD to manage"* [source: argocd-security-cluster-credentials-2026-08-31].

Note the asymmetry, because it is the interesting part: cluster-wide **read** is structural, since the agent cannot detect drift in something it cannot see, while broad **write** is a default, not a requirement.

For clusters other than the one it runs in, the credentials are ordinary Kubernetes objects: *"To manage external clusters, Argo CD stores the credentials of the external cluster as a Kubernetes Secret in the argocd namespace,"* comprising *"the K8s API bearer token associated with the `argocd-manager` ServiceAccount created during `argocd cluster add`, along with connection options to that API server"* [source: argocd-security-cluster-credentials-2026-08-31].

> ⚠ **Navigational Hazards**
>
> A delivery agent is not exempt infrastructure. It is a Pod with a ServiceAccount and, by default, cluster-admin-equivalent grants [source: argocd-security-cluster-credentials-2026-08-31], which makes it one of the highest-value subjects in the entire cluster *[cross-bearing: see Ch 12 §3 — what you may do]*.
>
> **Where people get confused:** the reasoning goes "GitOps is more secure than push, therefore the agent is a security improvement, therefore I do not need to think about it." The first clause is this book's blast-radius argument from §3, and it is an argument rather than a documented finding. The conclusion does not follow from it in any case. Pull moves the credentials *inside* the cluster; it does not make them smaller. Anyone who can commit to the tracked repository can, transitively, do whatever the agent may do.
>
> Which means: in a mature GitOps setup, the repository's branch-protection rules *are* an access-control mechanism, and they are exactly as load-bearing as your RBAC policy. That is not a metaphor. Commit access to the tracked branch is cluster access, mediated by an agent that will faithfully apply whatever it finds.

Two structural points before moving on, both of which discharge promises.

First: Argo CD's `Application` is a custom resource, and installing its CRD extends the API so that `Application` objects can *exist*. Whether anything *happens* to them depends entirely on whether the application controller is running, which is the pattern Chapter 10 named, and it has no cleaner instance in this book *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*. An `Application` on a cluster with no Argo CD controller is a stored document. It describes a deployment that will never occur.

Second: this is a controller acting on custom resources, which is precisely the thing Chapter 6 said you could build *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. It is not a new category of technology. It is the category you were taught, aimed somewhere unexpected.

---

## ☆ Taking Your Bearings #2 — Push, Pull, Ordering, and the Other Agent

Eight questions on §3 through §6. Two reach back — one into Ch 12, one into Ch 3.

**1.** A team stores all manifests in Git. Their CI pipeline, running on a hosted service, builds an image and then runs `kubectl apply -f manifests/` against the production cluster using credentials stored in the CI system's secret store. Which of the four OpenGitOps principles does this satisfy, and which does it fail?

**2.** An Argo CD application shows `OutOfSync`. The most recent sync operation completed successfully. Give two explanations that require nothing to have failed, and say where a *failure* would have been reported instead.

**3.** Two teams run identical workloads. Team A uses push-based CD from a shared CI system that also deploys to eleven other clusters. Team B runs an in-cluster agent per cluster. An attacker obtains full control of the CI system. Describe the difference in what they can now reach, using the term this book gives it.

**4.** [retrieval: ch12] A delivery agent needs to create Deployments and Services in namespaces it does not own, and — where pruning is enabled — delete resources that have been removed from the repository. Name the two kinds of object that must exist before any of that is permitted, and say which one determines the *scope* across namespaces.

**5.** A repository contains a CustomResourceDefinition and a custom resource that uses it. Applied together with no ordering, the custom resource is rejected. Which object must land first, what mechanism expresses that, and what ordering value does a resource with no ordering annotation receive?

**6.** Describe the structural difference between Argo CD's and Flux's design posture in one sentence each, and name one consequence of that difference for a team adopting either.

**7.** A colleague fixes a production incident with `kubectl patch` on a cluster managed by Flux. They do not commit the change. What happens, and which OpenGitOps principle is responsible? Then say why the same edit on an out-of-the-box Argo CD installation behaves differently.

**8.** [retrieval: ch3] In your own words: what does a controller do, what two things does it compare, and how often does it do it? Answer without mentioning Git, repositories, or delivery.

---

<details>
<summary>Answers with explanations</summary>

**1. Satisfies 1 (Declarative) and 2 (Versioned and Immutable). Fails 3 (Pulled Automatically) and 4 (Continuously Reconciled).**

Manifests are declarative and stored in Git with history, so the first two hold. Principle 3 requires that *"software agents automatically pull the desired state declarations from the source"* [source: opengitops-principles-v1-2026-08-31]; here the pipeline pushes, from outside. Principle 4 requires agents to *continuously* observe and apply; this pipeline runs once per commit and exits, leaving nothing observing between runs.

This is a working delivery system, but not GitOps — Git storage is necessary, not sufficient.

**2. Two benign explanations:** a person changed the cluster directly with `kubectl` — live state now deviates from target, so the status is `OutOfSync` [source: argocd-overview-2026-08-23], and by default *"changes that are made to the live cluster will not trigger automated sync"* [source: argocd-auto-sync-policy-2026-08-31]. Or: a new commit landed and hasn't synced yet — the target moved, live hasn't caught up. Nothing has failed; the docs confirm *"it is possible for an application to be `OutOfSync` even immediately after a successful Sync operation"* [source: argocd-diffing-outofsync-2026-08-31].

**Where a failure would show:** sync operation status, which answers *"whether or not a sync succeeded,"* as against sync status, which answers *"is the deployed application the same as Git says it should be?"* [source: argocd-core-concepts-2026-08-31].

**3. Blast radius**, this book's term for how far one compromise reaches. Compromising Team A's CI system yields write credentials to twelve clusters, because that's what the system holds to do its job. Compromising Team B's equivalent yields the ability to build and publish images — a real supply-chain problem, but not cluster-write credentials, since Team B's clusters hold their own credentials internally.

Pull doesn't prevent the compromise. It bounds what one compromise reaches.

**4. [retrieval: ch12] A ServiceAccount and an RBAC binding (with its Role or ClusterRole). The ClusterRoleBinding determines cross-namespace scope.**

The ServiceAccount is the identity; the binding attaches permissions to it. Because the work spans namespaces the agent doesn't own, the grant must be cluster-scoped *[cross-bearing: see Ch 12 §3 — what you may do]*. Argo CD's own docs confirm the shape: an `argocd-manager` ServiceAccount, reduced by editing the ClusterRole `argocd-manager-role` [source: argocd-security-cluster-credentials-2026-08-31]. And permission to delete isn't configuration to delete: *"by default... automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git"* [source: argocd-auto-sync-policy-2026-08-31].

**5. The CustomResourceDefinition must land first**, because a custom resource of a kind the API server doesn't yet recognize is rejected. The mechanism is **sync waves** — resources sync *"lower values first"* within a phase, and negative waves let you run something before everything else [source: argocd-sync-phases-and-waves-2026-08-31]. Give the CRD a lower wave than the custom resource; only relative order matters.

A resource with no annotation lands in **wave 0**: *"Hooks and resources are assigned to wave 0 by default"* [source: argocd-sync-phases-and-waves-2026-08-31]. Waves are a sort key, not absolute positions — `-5` and `0` order exactly as `0` and `1` do.

**6. Argo CD is integrated** — one product, one `Application` resource binding source to destination, one UI over the whole thing. **Flux is composable** — *"a collection of specialized tools, Flux Controllers, composable APIs"* [source: flux-concepts-2026-08-31].

Any of these earns credit: Flux lets you adopt or replace pieces independently, while Argo CD is more nearly all-or-nothing; Argo CD gives one console showing every application, while Flux's state is spread across controllers. "Composable" isn't "less capable" — Argo CD's own integration sits on three distinct components: an API server, a repository server, and an application controller [source: argocd-architecture-2026-08-31].

**7. The change is reverted, by principle 4 (Continuously Reconciled).**

Flux states it directly: *"if you make any changes to the cluster using `kubectl edit/patch/delete`, they will be promptly reverted"* [source: flux-concepts-2026-08-31]. Principle 4 requires that *"software agents continuously observe actual system state and attempt to apply the desired state"* [source: opengitops-principles-v1-2026-08-31]; the uncommitted patch isn't the desired state, so it's not what the agent applies.

**Why Argo CD differs out of the box:** self-healing is opt-in. *"By default, changes that are made to the live cluster will not trigger automated sync"* [source: argocd-auto-sync-policy-2026-08-31] — the edit produces `OutOfSync` and stays put. Both projects implement principle 4's *observation*; they differ on what they do about what they observe. Under reconciliation with self-heal on, an emergency fix must be committed to survive — the tool is doing the job it was installed for.

**8. [retrieval: ch3] A controller compares desired state against current state, and acts to close the gap — continuously, in a loop, indefinitely**, not once at creation and not only when triggered. If the two disagree it takes whatever action moves current toward desired, then checks again *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*.

**A common wrong answer:** describing the loop as event-driven — "it runs when something changes." That inverts the architecture: the controller isn't woken by a notification, it observes and decides for itself whether a gap exists.

If that came back clean, keep it loaded — the next section is one substitution away from it. If it didn't, **re-read Ch 3 §6 now, before §7**: the final section owns no new material, only a change made to the thing you just tried to state.

</details>

---

**If you got 6–8:** You have the chapter's core — push/pull, reconciliation, ordering, and the two agents' postures. What remains is synthesis.

**If you got 3–5:** Re-read §3's four principles, §4's `OutOfSync` Fixed Point, and Ch 12 §3 on what an agent may do.

**If you got 0–2:** Go back to **§3** and read it properly before continuing. §5 and §6 assume the push/pull distinction as settled ground, and Ch 3 §6's control loop is load-bearing for everything after it.

## ☀️ §7 — The Control Loop, Pointed at a Repository

This section teaches nothing new.

That is not modesty and it is not a warning; it is the design. Everything below has already been taught, most of it in Chapter 3, some of it as recently as four pages ago. What happens here is a single substitution, performed slowly, in front of you.

Here is the loop, as Chapter 3 gave it to you.

A controller holds a **desired state**, a record of what should be true. It observes the **current state**, what is actually true. When the two differ, it takes action to close the gap. Then it checks again. It does not stop. There is no completion condition, no final state, no moment at which the controller decides its work is finished and exits.

In Chapter 3, the desired state was in etcd, reached through the API server.

Now move it. Take the desired state out of etcd and put it in a Git repository.

<!-- FIGURE: ch15-zenith-control-loop-pointed-at-a-repo -->
![A closed control loop with no beginning and no end. Desired state, now a Git repository rather than etcd and marked as the only substitution, is observed by a controller; the controller acts to close the gap through the API server, still the only door in; the API server changes current state, what is actually true, which the controller observes in turn. And then it does it again, forever.](figures/ch15-zenith-control-loop-pointed-at-a-repo.svg)

<!-- ASCII-FALLBACK
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
-->

**Figure 15.7 — The control loop, pointed at a repository.** Lay this beside Chapter 3's control-loop figure and the point is that it is the same loop. The controller sits in the same place, the API server is still the only door in, and the arrows run in the same directions. One box changed contents.

<!-- RESOLVED 2026-08-31 (integration gate): ch03-fig02 has been redrawn onto this
     figure's chassis, so the caption's "lay this beside Chapter 3's" instruction is now
     checkable by a reader who actually flips back. The two are a matched pair and must
     be regenerated together at the diagram pass. -->

Look at what did *not* move.

**The API server is still the only mutator.** The agent writes to the cluster the way everything else does: as an API client, through authentication, authorization, and admission *[cross-bearing: see Ch 3 §5 — the only door in]*.

**The coordination is still watching, not telling.** Nothing pushes work to the controller. It observes and decides. Chapter 3 called this out as the architecture's central property, and said it would be retrieved: the same architecture, with a different thing in the hub position.

**The controller is still shaped the same way.** Compare, act, repeat. No new lifecycle, no new mechanism, no new category of component.

**Reconciliation is still endless.** A ReplicaSet does not finish. Neither does this.

One box changed contents. That is the entire technical delta between "Kubernetes" and "GitOps."

### The four principles, re-read

Now the four principles from §3, which looked like a list when you met them and are not one.

**1. Declarative.** This is Chapter 4. You file a declaration; the system's job is to make it true *[cross-bearing: see Ch 4 §1 — you file a declaration]*. Nothing added.

**2. Versioned and immutable.** This is the only genuinely new thing in the whole model, and it is a property of the *store*, not of Kubernetes. etcd holds the current desired state. A repository holds every desired state there has ever been, in order, each one fixed. That difference is what makes rollback by revert possible at all: you cannot return to a state your store did not keep.

**3. Pulled automatically.** This is Chapter 3's watch *[cross-bearing: see Ch 3 §5 — the only door in]*. Agents observe a source and fetch from it. The direction of travel was never inward.

**4. Continuously reconciled.** This is the loop itself. Word for word, it is what Chapter 3 §6 told you a controller does.

Three of the four were already yours. You have been running GitOps-shaped machinery since Chapter 3; the principles simply name what happens when the desired-state store is one a human can read, review, and revert.

Which kills the misreading this chapter was built to prevent.

> ★ **Fixed Point**
>
> **GitOps is not "running CI from Git." None of the four principles mentions integration, building, testing, or a pipeline. All four are about desired state — how it is expressed, how it is stored, how it is obtained, and how it is applied. The build is somebody else's job, and Kubernetes said so in its own documentation: it *"does not deploy source code and does not build your application"* [source: k8s-docs-overview-2026-08-23].**

### Why the chapter is called what it is

The chart is the truth, but not because a file is inherently authoritative. Files are only ever claims. A YAML manifest on somebody's laptop is a claim nothing enforces; a repository full of manifests that nothing watches is a folder of hopeful documents, which is precisely what Chapter 14 left you holding.

The chart is the truth because **something is continuously making it true.** The authority is not in the file. It is in the loop that never stops comparing the file to the world and acting on the difference.

That is what you have been building toward since Chapter 3, whether or not it looked like it. And it is why Chapter 6 said what it said when it finished teaching the control loop: that when you met this, it would look like a new idea for about ten seconds *[cross-bearing: see Ch 6 §9 — nobody sails one pod]*.

Ten seconds is about right.

---

## 🏆 Safe Harbor

**Checkpoint: You've Now Mastered**

✓ The twelve factors, sorted by who solves them — and the four that matter most in a cluster
✓ Deployment strategy vocabulary, and the line between a Deployment field and a pattern needing tooling
✓ Push versus pull as an architectural question about where credentials sit and how far one compromise reaches
✓ The four OpenGitOps principles, and why "pulled" and "continuously" carry the definition
✓ Argo CD as a controller: `Application`, manifest sources, tracking targets, `Synced` and `OutOfSync`
✓ What Argo CD does by default when it sees drift — report it, not revert it — and why that is the Fixed Point's best proof
✓ Rollback by revert, and why it is the third mechanism to wear that word
✓ The delivery agent's identity, its default grants, and why commit access is cluster access
✓ Sync phases and waves, and the ordering problem they exist for
✓ Flux's composable posture, self-bootstrap, and the opposite default it ships with
✓ The control loop, pointed at a repository — and everything about it that did not change

---

## Exam Alert! 🚨

**High-Priority Topics**

**1. The four OpenGitOps principles, in order, with the words that matter.** Declarative; versioned and immutable; **pulled** automatically; continuously reconciled [source: opengitops-principles-v1-2026-08-31]. *Pulled* and *continuously* carry the distinction. A definition missing either one describes something that is not GitOps.

**2. `OutOfSync` is a drift signal, not an error.** It reports that live state deviates from the target state in Git [source: argocd-overview-2026-08-23]. A person editing the cluster produces it. Nothing failed, and out of the box Argo CD reports it rather than reverting it [source: argocd-auto-sync-policy-2026-08-31].

**3. Argo CD is a Kubernetes controller.** It *"continuously monitors running applications and compares the current, live state against the desired target state"* [source: argocd-architecture-2026-08-31]. It does not bypass the API server, and it is not a new category of technology.

**4. Deployment strategy vocabulary versus Deployment fields.** `RollingUpdate` and `Recreate` are values on a Deployment [source: argo-rollouts-strategies-2026-08-23]. Blue/green and canary are patterns implemented by tooling above it.

---

**Common Traps** — these are distinctions that are easy to confuse, and they are the ones this material rewards getting right.

| The trap | The correct understanding |
|---|---|
| "GitOps means running CI from Git" | GitOps is four principles about *desired state*. Continuous integration is not one of them, and the cluster does not care who built the artifact. |
| Assuming a pipeline pushes to the cluster | Principle 3 is explicit: agents **pull** desired-state declarations from the source [source: opengitops-principles-v1-2026-08-31]. Push-based CD is not GitOps, whatever its manifests are stored in. |
| Treating reconciliation as a deploy-time event | Principle 4 is **continuous** and indefinite, the same property that makes a ReplicaSet recreate a Pod you deleted last Tuesday. |
| "Every GitOps agent reverts manual changes" | Flux does, promptly [source: flux-concepts-2026-08-31]. Argo CD, by default, does not — *"changes that are made to the live cluster will not trigger automated sync"* [source: argocd-auto-sync-policy-2026-08-31]. Same principles, opposite defaults. |
| "`OutOfSync` means the sync failed" | Sync status and sync *operation* status are two different fields answering two different questions [source: argocd-core-concepts-2026-08-31]. An application can be `OutOfSync` immediately after a successful sync [source: argocd-diffing-outofsync-2026-08-31]. |
| "Argo CD only deploys plain YAML" | Kustomize applications, Helm charts, Jsonnet, plain YAML/JSON directories, and custom config-management plugins [source: argocd-overview-2026-08-23]. |
| "Argo CD can only track a branch" | Branches, tags, or a **pinned Git commit** [source: argocd-tracking-strategies-2026-08-31]. |
| Assuming a GitOps agent writes to the datastore directly | It is an API client like any other, subject to authentication, authorization, and admission. Chapter 3's claim about the only door in is not suspended *[cross-bearing: see Ch 3 §5 — the only door in]*. |
| Assuming a delivery agent needs no identity because it is "infrastructure" | It is a Pod with a ServiceAccount and, by default, cluster-admin-level grants [source: argocd-security-cluster-credentials-2026-08-31] — one of the highest-value subjects in the cluster. |
| Collapsing the third rollback into one of the first two | `rollout undo` restores a Pod template. `helm rollback` returns a release to a prior revision. **Rollback by revert** changes a commit and lets the agent reconcile. Three mechanisms, one word. |
| Assuming a Deployment can express blue/green or canary by itself | Both need something above the Deployment; canary additionally needs traffic splitting and metric analysis [source: argo-rollouts-strategies-2026-08-23]. |

---

## Practice Questions

Twenty-one questions. Several present a situation rather than asking for a definition; those are the ones worth slowing down for, because a glossary cannot answer them.

---

**Q1.** An application writes its logs to `/var/log/app.log` inside the container and rotates them itself with a background thread. Which twelve-factor factor does this violate, and what capability does it break?

**Q2.** According to the twelve-factor methodology, which of the following is the *strongest* evidence that an application has correctly factored out its config?

A) It has no configuration at all; every value is a compile-time constant
B) Its codebase could be made open source at any moment without compromising credentials
C) It has separate configuration bundles named `staging` and `production`
D) It reads all settings from a `config.yaml` file at startup

**Q3.** A team argues that because their application is containerized and deployed by a Deployment, it is twelve-factor compliant. The application holds user session state in process memory. Evaluate the claim.

**Q4.** Which strategy guarantees that two versions of an application never run simultaneously, and what does it cost?

A) `RollingUpdate` — costs additional capacity
B) Canary — costs traffic-splitting infrastructure
C) `Recreate` — costs downtime
D) Blue/green — costs double capacity

**Q5.** A team runs a queue-consuming worker with no inbound HTTP traffic. They want to validate a new version against production configuration before it processes real work. Which strategy fits, and why is canary a poor choice here?

**Q6.** A team tells you they have configured blue/green deployment "in the Deployment spec." Without seeing their manifests, what do you already know is wrong with that description, and what must actually exist for them to be running blue/green?

**Q7.** Progressive delivery is defined as releasing updates in a controlled and gradual manner, *"typically coupling automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23]. Which half of that definition distinguishes progressive delivery from simply deploying slowly, and why?

**Q8.** A colleague who has just installed Argo CD says: "so this is a new kind of thing — a deployment engine that sits outside the normal Kubernetes machinery and pushes state in." Correct them in structural terms. What *category* of component is the Argo CD application controller, what two things does it compare, and what single element of the Chapter 3 architecture is different?

**Q9.** Which statement about push-based delivery is accurate?

A) It requires the cluster's API server to be reachable from the public internet
B) It stores cluster-write credentials outside the cluster
C) It is incompatible with storing manifests in Git
D) It bypasses the Kubernetes API server

**Q10.** Explain "blast radius" as this book uses it, using a compromised CI system as the example. Say what pull-based delivery does and does not change about it, and note what part of the argument is the book's rather than a documented finding.

**Q11.** Which principle is violated by a system that stores declarative manifests in Git, has an in-cluster agent fetch them, applies them on each new commit, and then does nothing until the next commit?

A) Declarative
B) Versioned and immutable
C) Pulled automatically
D) Continuously reconciled

**Q12.** Kubernetes documentation states that it *"does not deploy source code and does not build your application"* [source: k8s-docs-overview-2026-08-23]. What does this establish about the relationship between CI and GitOps?

**Q13.** An Argo CD `Application` reports `OutOfSync`, and the most recent sync operation reports success. Which is true?

A) The report is contradictory; one of the two must be stale
B) Sync status and sync operation status answer different questions, and both readings are valid simultaneously
C) `OutOfSync` overrides the operation status; the sync did not actually complete
D) The application will self-heal automatically, so the report can be disregarded

**Q14.** An Argo CD `Application` points at a repository path containing a Helm chart. A colleague says this cannot work because "Argo CD is a YAML tool, and Helm is a separate deployment mechanism." Correct them, naming the component involved.

**Q15.** A team pins an `Application` to a Git commit SHA. Their build pipeline pushes new commits to the tracked branch daily. What happens to the cluster, and what would have to change for it to update?

**Q16.** [cross-domain: D2.2] A GitOps agent must create Deployments and Services in twelve namespaces it does not own, and — with pruning enabled — delete resources removed from the repository. What must exist for this to be permitted, and why is a Role in each namespace a poor answer?

**Q17.** [cross-domain: D1.1] An engineer describes `OutOfSync` as "the status field not matching the spec field." Is this a good analogy? Explain precisely what is being compared and where each operand lives.

**Q18.** Three things in this book are called rollback. Name the mechanism each one uses and where each keeps the state it returns to.

**Q19.** A repository contains a namespace, a CustomResourceDefinition, and a custom resource of the type that CRD defines. Applied simultaneously, this fails. What must land in what order, what mechanism expresses that ordering, and what happens to an object with no ordering annotation?

**Q20.** Which hook phase runs *"after all Sync hooks completed and were successful, a successful application, and all resources in a Healthy state"* [source: argocd-sync-phases-and-waves-2026-08-31], and what does that make it suitable for?

**Q21.** Flux describes itself as a GitOps Toolkit — *"a collection of specialized tools, Flux Controllers, composable APIs"* [source: flux-concepts-2026-08-31] — while Argo CD presents as an integrated product with a single `Application` resource. Name one practical consequence of this difference for a team adopting either; name the thing Flux does at install time that Argo CD does not; and describe how their documented positions on drift correction differ.

---

<details>
<summary>Answers with full explanations</summary>

**Q1. Factor XI (Logs — treat logs as event streams).** The rule is that *"a twelve-factor app never concerns itself with routing or storage of its output stream"*; each process writes unbuffered to stdout and the execution environment captures it [source: twelve-factor-xi-logs-2026-08-31].

What it breaks: `kubectl logs` returns nothing useful, because the container's stdout is empty. Node-level log collection sees nothing. The logs exist only in the container's writable layer and are destroyed with the Pod, which means the logs from the crash you are investigating died with the thing that crashed.

**Q2. B.** *"A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials"* [source: twelve-factor-iii-config-2026-08-31].

**A is wrong**, and it targets a real confusion: factor III is about *where config lives*, not about having less of it. An application with no configuration cannot vary between deploys at all, which fails factor III's own definition of config as *"everything that is likely to vary between deploys"* [source: twelve-factor-iii-config-2026-08-31], and it fails factor X, dev/prod parity, in the other direction. **C is wrong**, and is in fact a named anti-pattern: env vars *"are never grouped together as 'environments', but instead are independently managed for each deploy"* [source: twelve-factor-iii-config-2026-08-31]. **D is wrong** — a config file is explicitly called out as an improvement that *"still has weaknesses: it's easy to mistakenly check in a config file to the repo"* [source: twelve-factor-iii-config-2026-08-31].

**Q3. The claim fails.** In-memory session state violates factor VI: *"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service"* [source: twelve-factor-vi-processes-2026-08-31]. The methodology bans the usual workaround by name — *"Sticky sessions are a violation of twelve-factor and should never be used or relied upon"* — and suggests a time-expiring datastore instead [source: twelve-factor-vi-processes-2026-08-31].

The general point matters more than this instance: containerization and Deployments implement the *platform* side of twelve-factor. They cannot implement the application side. Packaging a stateful process in a container produces a containerized stateful process.

**Q4. C.** *"A Recreate deployment deletes the old version of the application before bringing up the new version. As a result, this ensures that two versions of the application never run at the same time, but there is downtime during the deployment"* [source: argo-rollouts-strategies-2026-08-23].

**A is wrong** — `RollingUpdate` guarantees the opposite: both versions run concurrently by design, which is what avoids the downtime. **D is wrong** — blue/green does run both versions simultaneously; only one *receives production traffic* [source: argo-rollouts-strategies-2026-08-23], which is a different guarantee and does not help with, say, an incompatible schema migration. **B is wrong** — canary deliberately runs both against real traffic.

**Q5. Blue/green.** Both versions run, only the old receives production traffic, and *"this allows the developers to run tests against the new version before switching the live traffic"* [source: argo-rollouts-strategies-2026-08-23], against production configuration and production backing services.

Canary is a poor fit for a specific mechanical reason: it works by proportioning *traffic*, and a queue worker has no inbound traffic to proportion. Argo's own comparison makes the pairing: canary demands traffic-splitting via a service mesh or ingress controller, while blue/green *"needs no traffic provider and suits workloads such as queue workers"* [source: argo-rollouts-strategies-2026-08-23].

**Q6. What is wrong: a Deployment's update-strategy field takes only two values, `Recreate` and `RollingUpdate` [source: argo-rollouts-strategies-2026-08-23]. Blue/green is not among them and cannot be expressed there.** Whatever they have configured, it is not blue/green in the Deployment spec, most likely a `RollingUpdate` they are describing loosely, or a second Deployment they are switching between by hand.

What must actually exist: **two complete environments running simultaneously**, and **something that controls which one receives production traffic** — a Service selector, a load balancer, or an ingress rule — plus something that flips it. CNCF's description turns on exactly that: two environments, one live, traffic switched via load balancer after testing the inactive one [source: cncf-glossary-blue-green-deployment-2026-08-31]. A Deployment object has no concept of a second environment and no control over traffic routing, which is why the pattern needs tooling above it. This is §2's Fixed Point in its consequential form.

**Q7. The metric-analysis half.** *Gradual* alone is just a slower deployment: a `RollingUpdate` with a small `maxSurge` is gradual and is not progressive delivery. What the definition adds is *"automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23]. The release evaluates itself against measurements and decides whether to continue or reverse. Gradual buys time; metric analysis is what uses the time.

**Q8. It is a Kubernetes controller — not a new category of component, and not outside the normal machinery.** The documentation says so in the terms Chapter 3 taught: the application controller *"is a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the repo)"* [source: argocd-architecture-2026-08-31].

**What it compares:** live state (what is actually deployed) against target state (what the repository says should be) [source: argocd-core-concepts-2026-08-31].

**What is different:** one thing only — where the desired state is kept. In Chapter 3, desired state lived in etcd, reached through the API server. Here it lives in a repository. Everything else holds: the loop is the same loop, the controller occupies the same position, and it writes through the API server as an ordinary API client subject to authentication, authorization, and admission *[cross-bearing: see Ch 3 §5 — the only door in]*.

**The "pushes state in" half of the colleague's description is wrong twice over.** The agent runs inside the cluster and *pulls* from the repository, which is principle 3 [source: opengitops-principles-v1-2026-08-31]; and it does not push into anything, it makes ordinary API calls like every other controller.

**Q9. B.** In push-based delivery the pipeline lives outside the cluster and must hold credentials to it, which is the arrangement this chapter contrasts with pull.

**A is wrong**, and it is the confusion most worth clearing: push versus pull is about *where the credentials live*, not about network topology. A self-hosted runner inside the network, a VPN, or a private CI instance all push to an API server that is not publicly reachable. Nothing about push requires exposure. **C is wrong** — many push pipelines apply manifests from Git; that is precisely the arrangement Q8 and TYB 2 Q1 describe, and it is what makes the distinction subtle. **D is wrong** — nothing bypasses the API server, in either model *[cross-bearing: see Ch 3 §5 — the only door in]*.

**Q10. Blast radius is this book's term for how far the damage from a single compromise reaches.** A shared CI system holding write credentials for a dozen clusters has a blast radius of a dozen clusters: whoever controls the pipeline controls every cluster it deploys to. Under pull-based delivery, each cluster's agent holds credentials only to its own cluster, so compromising the CI system yields the ability to build and publish artifacts, a serious supply-chain problem, but not direct cluster-write access anywhere.

**What pull does not change:** it does not prevent compromise, and it does not make the agent's own credentials smaller. Argo CD's default is *"a clusteradmin level role"* [source: argocd-security-cluster-credentials-2026-08-31]. Anyone who can commit to the tracked branch can, transitively, do whatever the agent may do.

**What is sourced and what is not:** the credential *locations* are documented — Argo CD stores external-cluster credentials as a Secret in the `argocd` namespace [source: argocd-security-cluster-credentials-2026-08-31], and its best-practices page argues for access separation on the grounds that *"the developers who are developing the application, may not necessarily be the same people who can/should push to production environments"* [source: argocd-best-practices-2026-08-31]. The *comparison* between push and pull as a security posture is this book's reading of principle 3 and those documented placements. No CNCF or vendor source in this chapter's corpus makes it in these terms.

**Q11. D.** Principle 4 requires that agents *"continuously observe actual system state and attempt to apply the desired state"* [source: opengitops-principles-v1-2026-08-31]. A system that acts only on new commits satisfies principle 3, since it does pull, but has no answer to drift introduced any other way. A manual `kubectl edit` would persist indefinitely, which is exactly the failure GitOps exists to close.

**A, B, and C are all satisfied** by the described system: the manifests are declarative, they are in a versioned store, and the agent pulls them. C is the closest call and the most useful distractor — readers who conflate "pulls" with "keeps checking" pick it. Pulling on a trigger is still pulling; principle 3 is about *direction*, principle 4 is about *cadence*.

**Q12. It establishes that CI and GitOps are orthogonal concerns, not stages of one thing.** The cluster does not build your application and does not care who did; CI/CD workflows are *"determined by organization cultures and preferences as well as technical requirements"* [source: k8s-docs-overview-2026-08-23]. GitOps starts after a deployable artifact exists, and concerns itself only with how desired state is stored and applied. A team can have excellent CI and no GitOps, or GitOps with a build process that is entirely manual.

This is why "GitOps means running CI from Git" is wrong at the level of category, not just detail.

**Q13. B.** Sync status answers *"is the deployed application the same as Git says it should be?"* while sync **operation** status answers *"whether or not a sync succeeded"* — two separate glossary entries, two separate questions [source: argocd-core-concepts-2026-08-31]. The documentation states the combination outright: *"it is possible for an application to be `OutOfSync` even immediately after a successful Sync operation"* [source: argocd-diffing-outofsync-2026-08-31].

**A is wrong** — it assumes the two fields report one fact, which is exactly the collapse the glossary's separate entries exist to prevent. **C is wrong**, and it is the misconception Exam Alert #2 names: reading `OutOfSync` as a failure report. It is a drift signal; a person editing the cluster produces one with nothing having failed [source: argocd-overview-2026-08-23]. **D is wrong on two counts.** First, self-healing is not on by default: *"by default, changes that are made to the live cluster will not trigger automated sync"* [source: argocd-auto-sync-policy-2026-08-31], so nothing is guaranteed to happen on its own. Second, a drift report is information, not noise — the whole point of the status is that somebody reads it.

**Q14. The colleague is wrong on both counts.** Argo CD accepts manifests *"in several ways: kustomize applications; helm charts; jsonnet files; plain directory of YAML/json manifests; any custom config management tool configured as a config management plugin"* [source: argocd-overview-2026-08-23].

The component: the **repository server**, which *"maintains a local cache of the Git repository holding the application manifests"* and is responsible for *"generating and returning the Kubernetes manifests"* given a repository URL, revision, path, and template-specific configuration [source: argocd-architecture-2026-08-31]. Rendering is a dedicated component, not an afterthought. Argo CD's glossary even names the choice: the **application source type** is *"which Tool is used to build the application"* [source: argocd-core-concepts-2026-08-31].

**Q15. Nothing happens to the cluster.** *"If a Git commit SHA is specified, the app is effectively pinned to the manifests defined at the specified commit"* [source: argocd-tracking-strategies-2026-08-31]. New commits on the branch are irrelevant; the `Application` is not looking at the branch.

To update: *"the only way to change the live state of an app which is pinned to a commit, is by updating the tracking revision in the application to a different commit containing the new manifests"* [source: argocd-tracking-strategies-2026-08-31]. Somebody must change the `Application`'s own revision field, which is itself typically a commit in a repository, and therefore itself reviewable. That is the point of pinning.

**Q16. [cross-domain: D2.2] A ServiceAccount, and a ClusterRole bound by a ClusterRoleBinding.** The ServiceAccount is the identity the agent's Pod runs as; the ClusterRole enumerates permitted verbs on resources; the ClusterRoleBinding attaches the permission set to the identity across the whole cluster *[cross-bearing: see Ch 12 §3 — what you may do]*.

**Why per-namespace Roles are a poor answer:** they work, and they break. Every new namespace the repository introduces requires a new Role and RoleBinding before the agent can act in it, which means the agent cannot create a namespace and populate it in one sync, and the failure appears as a permissions error at exactly the moment someone adds a namespace. Argo CD's own model uses a cluster-scoped role for this reason, noting that it *"requires cluster-wide read privileges to resources in the managed cluster to function properly"* even when write is narrowed [source: argocd-security-cluster-credentials-2026-08-31].

**On the pruning qualifier in the stem:** permission and configuration are separate. Deleting requires the `delete` verb in the grant, but the grant does not cause deletion — *"by default (and as a safety mechanism), automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git"* [source: argocd-auto-sync-policy-2026-08-31].

**Q17. [cross-domain: D1.1] It is a good analogy and worth being precise about.** Argo CD compares **target state** — *"the desired state of an application, as represented by files in a Git repository"* — against **live state** — *"the live state of that application. What pods etc are deployed"* [source: argocd-core-concepts-2026-08-31].

The mapping to Chapter 4: target state plays the role of `spec` (what was asked for), and live state is observed from the cluster, which is what `status` reports on *[cross-bearing: see Ch 4 §2 — the anatomy of a record]*.

The one refinement: the operands live in different places. In an ordinary object, `spec` and `status` are two fields of one record in etcd. Under GitOps, the authored `spec` lives outside the cluster entirely, and the cluster's copy is downstream of it. That relocation is the whole substitution, and it is why an object's own `spec` can be perfectly satisfied while the application is `OutOfSync`, if somebody changed the `spec` itself by hand.

**Q18. Three mechanisms:**

- **`kubectl rollout undo`** (Ch 6 §5) — restores a Deployment's Pod template. Prior state lives in the old ReplicaSet, on the cluster.
- **`helm rollback`** (Ch 14 §3) — returns a Helm release to a prior revision. Prior state lives in Helm's release history, on the cluster.
- **Rollback by revert** (this chapter) — changes a commit in the repository; the agent reconciles as it always does. Prior state lives in the repository's history. Argo CD describes the capability as *"rollback/roll-anywhere to any application configuration committed in Git repository"* [source: argocd-overview-2026-08-23].

The structural point worth carrying: the third has no dedicated rollback code path. You move the target and the loop does the rest, the same loop that handles every ordinary change.

**Q19. Order: namespace, then CustomResourceDefinition, then the custom resource.** The namespace must exist before namespaced objects can be placed in it, and the CRD must be registered before the API server will accept a custom resource of that kind.

**The mechanism is sync waves**, which order resources within a phase, *"lower values first"* [source: argocd-sync-phases-and-waves-2026-08-31]. What matters is the relative order, not the absolute numbers: `-2, -1, 0` and `0, 1, 2` behave identically. The full precedence puts the phase first and the wave second, with deterministic tie-breaks after those [source: argocd-sync-phases-and-waves-2026-08-31].

**An object with no ordering annotation lands in wave 0:** *"Hooks and resources are assigned to wave 0 by default. The wave can be negative, so you can create a wave that runs before all other resources"* [source: argocd-sync-phases-and-waves-2026-08-31]. That negative-wave capability is what makes waves an ordering system rather than a queue — you can always insert something ahead of the default without renumbering everything else.

**Q20. PostSync**, and the quoted condition is what makes it distinctive: it requires not just completion but *"all resources in a Healthy state"* [source: argocd-sync-phases-and-waves-2026-08-31].

Suitable for: smoke tests, notifications, and traffic cutover, anything that should happen only once the new state is both applied and demonstrably working. Argo CD ties the hook mechanism to release patterns explicitly, describing hooks as supporting *"complex application rollouts (e.g. blue/green and canary upgrades)"* [source: argocd-overview-2026-08-23].

**Why not PreSync:** PreSync runs *"prior to the application of the manifests"* [source: argocd-sync-phases-and-waves-2026-08-31], before the thing you would be testing exists.

**Q21. Practical consequence** (any one earns credit): Flux's composability means a team can adopt the source and Kustomize controllers without the Helm or image-automation ones, and can replace pieces independently; Argo CD's integration means fewer objects to learn and a single UI showing every application's state, at the cost of being more nearly all-or-nothing. Flux's design surfaces as many custom resources across several controllers [source: flux-components-2026-08-31]; Argo CD's surfaces mainly as `Application` objects [source: argocd-core-concepts-2026-08-31].

**What Flux does at install time that Argo CD does not: it installs itself in a GitOps manner.** *"The process of installing the Flux components in a GitOps manner is called a bootstrap. The manifests are applied to the cluster, a `GitRepository` and `Kustomization` are created for the Flux components, then the manifests are pushed to an existing Git repository"* [source: flux-concepts-2026-08-31] — so that, as the earlier capture puts it, *"Flux manages itself like any other resource"* [source: flux-concepts-2026-08-23]. Upgrading Flux is a commit.

**Drift correction — the documented positions differ.** Flux states that manual `kubectl edit/patch/delete` changes *"will be promptly reverted"* [source: flux-concepts-2026-08-31]. Argo CD's automated sync policy states the opposite default: *"by default, changes that are made to the live cluster will not trigger automated sync"* [source: argocd-auto-sync-policy-2026-08-31], and pruning is likewise opt-in — *"by default (and as a safety mechanism), automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git"* [source: argocd-auto-sync-policy-2026-08-31]. Two graduated projects implementing the same four principles, shipping with opposite answers to "what do I do about drift I detect."

**On multi-cluster:** Argo CD documents managing multiple clusters from one control point — the feature list includes the *"ability to manage and deploy to multiple clusters"* [source: argocd-overview-2026-08-23], with each remote cluster's credentials stored as a Secret in the `argocd` namespace [source: argocd-security-cluster-credentials-2026-08-31]. Flux's documented position is narrower: its reconciling controllers run in the cluster they reconcile [source: flux-security-2026-08-31] and bootstrap installs it into a cluster against a repository [source: flux-concepts-2026-08-31]. Credit an answer that states the Argo CD side accurately and does not over-claim the Flux side.

</details>

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| Twelve-factor app | Constraints an application accepts so a platform can run it. Kubernetes implements the platform half; the application half is still yours. |
| Factor III (Config) | Config is what varies between deploys. The test: could you open-source the repo today without leaking a credential? |
| Factor IX (Disposability) | Fast startup, graceful SIGTERM shutdown, correct even on sudden death. |
| `Recreate` / `RollingUpdate` | Values of a field on a Deployment. Downtime with no version overlap, versus no downtime with overlap. |
| Blue/green | Two full environments; only one takes traffic; test before the switch. Costs capacity, needs no traffic provider. |
| Canary | A slice of real traffic meets the new version first. Needs traffic splitting and metric analysis. |
| Progressive delivery | Gradual *plus* metric analysis driving automated promotion or rollback. Gradual alone is just slow. |
| Push | Pipeline outside the cluster holds cluster credentials and reaches in. Nothing watches between runs. |
| Pull | Agent inside the cluster holds repository credentials and reaches out. Never stops watching. |
| Blast radius | This book's term for how far one compromise reaches. Pull bounds it; it does not shrink the agent's own grants. |
| The four principles | Declarative · versioned and immutable · **pulled** automatically · **continuously** reconciled. |
| Argo CD | A Kubernetes controller comparing live state against target state in a repository. |
| `Application` | The custom resource: a source (repo, revision, path) and a destination (cluster, namespace). |
| Manifest sources | Kustomize, Helm charts, Jsonnet, plain YAML/JSON, config-management plugins. |
| Tracking | Branch (moves), tag (rarely moves), pinned commit (never moves). |
| `OutOfSync` | Live state deviates from target state. A drift signal, not an error. A person can cause one. |
| Self-heal and prune | Both opt-in in Argo CD. Out of the box it reports drift and does not revert or delete. |
| Rollback by revert | Change the commit; the loop does the rest. No second code path. Third mechanism to wear the word. |
| Agent identity | A Pod, a ServiceAccount, broad grants by default. Commit access to the tracked branch is cluster access. |
| Sync phases | PreSync → Sync → PostSync, each gated on the previous succeeding; SyncFail runs when a sync fails. |
| Sync waves | Integer ordering within a phase, lower first, default 0, negatives allowed. |
| Flux | A composable toolkit of controllers. Bootstraps itself. Reverts manual `kubectl` changes — the opposite default from Argo CD. |
| The Zenith | The control loop, with a Git repository where etcd sat. Nothing else moved. |

---

## The Voyage Ahead

You now hold a delivery model in which nobody touches the cluster and something never stops watching it.

Which is exactly when you find out that the thing being watched is not the thing you thought.

The agent reports `Synced`. Every object matches the repository, every replica is present, the rollout completed and the health checks pass. And the application does not work. Users get errors, or timeouts, or the wrong data, and nothing in the delivery path has anything to say about it, because the delivery path did its job perfectly. It applied what you asked for. You asked for the wrong thing, or the right thing configured wrongly, and no amount of reconciliation can tell the difference.

Chapter 13 taught you to diagnose a cluster that will not run your Pod. It ended by handing something back: the case where the platform is fine and the problem is yours. That handoff comes due next.

The next chapter is about the Pod that is running, healthy, `Synced`, and wrong, and about the tools that let you get inside a container that was built with nothing in it to help you.

> *"Reconciliation will make the cluster match your intention exactly. It has no opinion about your intention."*

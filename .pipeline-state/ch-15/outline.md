I have both binding contracts, the arc-outline block, B1's D3.1 concept and trap tables, B4's budget, the five cached D3.1 snapshots, and every published cross-bearing into Ch 15 verified by line number against chapters 01–14. Three findings shape this outline: **four section numbers are pinned by shipped text** (§3, §4, §5, §7), **Argo CD's first appearance in the book is Chapter 3, not this chapter**, and **the two sections carrying the chapter's most specific promises — §4's agent identity and §5's sync ordering — have no cached source at all**.

```
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
```

# Chapter 15 Outline — The Chart Is the Truth

## Chapter-type note (read first)

`content`. Full structural contract applies: witty subtitle, Attention Budget, epigraph, 🧭 Soundings, Why This Chapter Matters, What You'll Learn, ≥2 ☆ Taking Your Bearings, Exam Alert, Practice Questions, Chapter Summary, The Voyage Ahead.

**Heading form:** `## <difficulty> §N — Title`, the Ch 5–8 majority form that B6 recommends for Ch 9–19 and that shipped Ch 9–14 use. **Closing section takes `☀️` in place of a difficulty glyph**, per B6 recommendation #4.

**Position.** Mid-Part IV — Dispatches. Ch 14 opened the Part; no part-boundary orientation beat is owed here. What *is* owed is a handoff: Ch 14's Voyage Ahead (line 1349ff) wrote this chapter's opening paragraph already, and the draft should take it rather than invent a new one.

---

## 1. Why This Chapter Matters

**Take Ch 14's handoff verbatim, in the first paragraph.** Ch 14 closed on this and the promise is due immediately: *"You have a unit now… And it has bought you less than it should have, because the unit still gets applied by a person. Somebody with cluster credentials on their laptop, running a command, from a machine nobody audits, at a moment nobody records. They apply the version they believe is current. Afterward, nothing keeps watch."* That paragraph is the curiosity gap, fully formed, and rewriting it would waste a handoff the previous chapter built deliberately.

The gap has two halves and the chapter answers them in order. The first is **who applies it** — which sounds procedural and is not, because the answer determines where cluster credentials live and how large a single mistake can get before something catches it. The second is **what happens afterward** — because "nothing keeps watch" is the actual defect, and the reader has spent thirteen chapters inside a system whose entire architecture is things that keep watch. They already own the answer. They have not yet been shown that they own it.

The identity frame is a promotion in scope. Up to Ch 14 the reader has been someone who *makes changes to a cluster*. This chapter makes them someone who *maintains a claim about what a cluster should contain* — and never touches the cluster again. That is the actual working posture of a platform engineer, and it is a genuinely uncomfortable shift for a reader whose competence has so far been measured in `kubectl` fluency. Say so plainly. The discomfort is the point: the chapter is asking them to give up the terminal as the instrument of change.

The stakes are already banked and should be recalled in one clause, not re-argued: Ch 1:274 told the reader this domain doubled from 8% to 16%. Ch 14 cashed the first half. This is the second.

**Honesty beat — one back-bearing, NOT a repeat.** Ch 14 stated at length that CNCF publishes the competency name and no sub-topic list, and that Helm's presence is authored inference. That statement holds here and covers this chapter too. Repeating it at length is channel redundancy (skill Part 7) and would read as anxiety. One sentence, back-bearing to Ch 14, plus the one thing Ch 14 could not say: **Argo and Flux are CNCF graduated projects** [source: cncf-project-maturity-levels-2026-08-23], which is the honest basis for inferring what a CNCF exam means by "Application Delivery." Then enforce the no-frequency-claims rule silently for the rest of the chapter. See Open Question 7.

**Voice guardrail.** The wry beats belong to the practitioner's own habits — the fix applied directly to production at 2 a.m. that nobody wrote down, the staging environment that has been three commits ahead for a year, the runbook step that says "and then apply the manifests." Never at users harmed by a bad deploy or by an outage. Skill Part 14, subject dignity. This chapter's subject matter makes that guardrail easy to trip: "blast radius" is a term of art here and the temptation to make the blast funny is real.

**Register guardrail.** `structural-contract.yaml` forbids `chart a course`, `set sail`, `smooth sailing`, `weather the storm`, `all hands on deck`. **"Chart" is a technical term in this chapter and the one before it**, which makes `chart a course` the single easiest accident in the book — Ch 14's outline flagged it and the risk is higher here because the chapter title contains the word. US spelling throughout.

---

## 2. What You'll Learn

- **Name** the twelve factors, and say which ones Kubernetes hands you and which remain your application's problem
- **Distinguish** the two update strategies a Deployment implements from the release patterns that need tooling above it — blue/green, canary, A/B
- **State** the four OpenGitOps principles, and explain why a pipeline that pushes to a cluster satisfies none of the last two
- **Read** a delivery agent as what it structurally is: a controller, with its desired state somewhere unusual
- **Explain** what `OutOfSync` reports, why it is a signal rather than an error, and what makes it different from a failure
- **Recognize** the control loop from Chapter 3 wearing different clothes, and say what actually changed and what did not

*You'll also stop thinking of GitOps as a deployment tool, which is the misreading this chapter exists to prevent.*

---

## 3. Soundings plan — 8 questions

Content chapter, so 8. Every question is answerable from Chapters 1–14 or from general professional knowledge. This chapter's Soundings carries more diagnostic load than any other in the book, because `prereq_factor` is `heavy` and because **two questions gate the chapter's payoff rather than merely its comprehension**.

| # | Topic | Tests | Why it earns its place as a pre-test |
|---|---|---|---|
| 1 | A controller holds a recorded target and observes what actually exists. What does it do when they differ, and how often does it check? | Ch 3 §6 | **The load-bearing one, and a deliberate decay probe.** Taught at the 15% mark, retrieved here at 75%. §7's entire payoff is the recognition that a delivery agent is this loop; a reader who has lost the loop experiences the Zenith as a seventh list to memorize. A wrong answer here must send them back to **Ch 3 §6** before §3, not alongside it. |
| 2 | An object has one field you write and one the system writes. Which is which, and what does it mean when they disagree? | Ch 4 §2 | **Second load-bearing.** `OutOfSync` is precisely "status does not match spec, where spec lives in Git." A reader without a clean spec/status model reads §4's central concept as new vocabulary instead of as a familiar comparison with one substitution. |
| 3 | What does a Deployment's default update strategy actually do, and what do `maxSurge` and `maxUnavailable` control? | Ch 6 §4 | §2 adds *vocabulary* on top of mechanics the reader already owns. If the mechanics are gone, §2 degenerates into four names with no substrate. **Must not mention blue/green, canary, or A/B** — Ch 6:665 already named those as deferred, and repeating them in a stem starts the section early. |
| 4 | You install a CRD. What can now exist that could not before — and what still has to be true before anything actually happens? | Ch 6 §8 + Ch 10 §3 | Pre-tests both halves of §4's structural claim in Ch 6/Ch 10 vocabulary. The second clause deliberately reaches for the named pattern from Ch 10 §3 without naming it, so §4 can retrieve the name rather than supply the idea. **Does not mention delivery, agents, or Git.** |
| 5 | A process inside the cluster needs to create and delete objects across several namespaces. What does it need in order to be allowed to, and what decides how much it may do? | Ch 5 §6 + Ch 12 §2–§3 | Discharges the pre-test half of the §4 identity pin — the promise made twice, at chapter-05:781 and chapter-12:617. The reader constructs the requirement themselves; §4 then only has to say "that thing you just described is what a delivery agent is." |
| 6 | Where does environment-specific configuration belong, and why is baking it into the image wrong? | Ch 4 §4 + Ch 2 §2 | §1's factor III is this idea with a name attached. Testing it first lets §1 present the twelve factors as a vocabulary for things the reader already does, which is the only framing under which a list of twelve survives contact with an adult professional. |
| 7 | Somebody makes a change directly on a production system, outside whatever process the team normally uses. What goes wrong afterward, and when do you find out? | General professional knowledge | **Generation effect** (skill Part 10). Every honest answer is drift, and the sting in the tail — *you find out at the next deploy, from the wrong direction* — is the reader arriving at the problem §4 solves. Answerable with zero Kubernetes. |
| 8 | You have a repository whose commit history records what was intended. What can you do with that history that you cannot do with the current state of a running server? | General professional knowledge | Sets up principle 2 (versioned and immutable) and `rollback by revert` without naming either. Adult professionals own this answer completely; the chapter's job is to show them it was a deployment strategy the whole time. |

### FIXED-POINT SPOILER CHECK

The chapter's candidate Fixed Points, and the confirmation that no Soundings question states one:

| Candidate ★ Fixed Point | Spoiled by any Soundings question? |
|---|---|
| GitOps is four principles about desired state — declarative, versioned and immutable, **pulled** automatically, continuously reconciled. Continuous integration is not one of them. | **No.** No stem contains "GitOps", "CI", "pipeline", or any of the four principle names. Q7 and Q8 approach two of the four from the outside, as consequences, without stating any principle. |
| `OutOfSync` means live state deviates from the target state in Git. It is a drift signal, not an error, and a human editing the cluster produces it. | **No** — **and this is the watch item.** Q7 gets closest: it asks what goes wrong when someone edits production directly. It stops at *consequence*. If drafting sharpens Q7 toward "what would you want a tool to tell you about that," it becomes a spoiler. **Keep Q7 about the consequence, never about the detection.** |
| Push and pull differ in where the credentials live and how large a single mistake gets before something catches it. | **No.** No stem mentions delivery, pipelines, or credentials for a cluster. Q5 asks about an in-cluster identity, which is the opposite direction. |
| A delivery agent is a controller. Git is where its desired state lives. Nothing else about the architecture changed. | **No.** Q1 tests the loop and Q4 tests custom resources, in isolation, in their own chapters' terms. Neither joins them, and neither mentions Git or repositories. **The subtitle states this Fixed Point on the chapter's second line** — see the subtitle note in the frontmatter. That is the subtitle's job and is not a license to relax this table. |
| Rolling and Recreate are fields on a Deployment. Blue/green, canary, and A/B are patterns that require tooling above it. | **No.** Q3 asks only what the default strategy does. It does not hint that other patterns exist or that a Deployment cannot express them. |

Clean, with one explicit watch item recorded (Q7).

**Rubric branches (all three mandatory):**
- **6+** → skim §1 and §2; read §3, §4, and §7 properly. The vocabulary is the fast part; the argument is not.
- **3–5** → normal pace.
- **0–2** → **re-read Ch 3 §6 and Ch 4 §2 before starting**, not alongside. Name the sections, not the chapters. If Q1 specifically was missed, that one is not optional — the chapter's last section will not land without it.

---

## 4. Section plan

### `## ⚪ §1 — Twelve Factors, and the Ones Kubernetes Already Solved`

Owns the **twelve-factor app** as a named methodology, discharging two chapter-level promises: chapter-04:722 (*"the twelve factors, and which ones Kubernetes hands you for free"*) and chapter-05:559 (*"Chapter 15 will hand you the methodology's word for it, disposability"*). All twelve factors get named — the reader is owed the list — but the section's argument is a **partition, not a recitation**: which factors the platform already implements, which it makes easy, and which remain entirely the application's problem. Trap 85 is pre-empted structurally by teaching the factors in clusters rather than in order.

The four that carry real weight here, each tied to something already shipped: **III Config** (ConfigMaps and Secrets, Ch 4 §4 — trap 86 lives here, and "store config in the environment" does *not* mean "use a config file"); **VI Processes / VIII Concurrency** (stateless scale-out, which is why Deployments work and why StatefulSet is the exception, Ch 6 §1 and §6); **IX Disposability** (fast startup and graceful shutdown — Ch 5 already taught `terminationGracePeriodSeconds` and explicitly deferred the *word* to this chapter); **XI Logs as event streams** (why node-level collection works at all, with a forward pointer to Ch 18 §6).

- **Objectives:** D3.1 (Application Delivery — the twelve-factor app)
- **Introduces:** twelve-factor-app; factor-iii-config-in-environment; factor-vi-stateless-processes; factor-ix-disposability; factor-xi-logs-as-event-streams
- **Figure:** `ch15-fig01-twelve-factor-in-kubernetes`
- **Cross-bearings out:** `Ch 4 §4 — configuration kept outside the image`; `Ch 5 §4 — scheduled once, replaced never` (disposability); `Ch 6 §1 — the resource that holds the intent`; `Ch 6 §6 — when Pods are not interchangeable`; `Ch 18 §6 — lines from everywhere` (logs)
- **⚑ Ledger guardrail:** the ledger gives §1 factor III explicitly and gives Ch 17 §3 the cloud-native *characteristics*. §1 must not drift into microservices, loose coupling, or immutable infrastructure — those are Ch 17 §3's and the reader meets them there. Naming twelve-factor as a **predecessor** of that vocabulary is fine and is a good forward pointer; teaching the vocabulary is not.
- **Depth ruling:** twelve names, four developed. Do not write a paragraph per factor. The cached source gives one line per factor and that is the correct associate-tier depth for the other eight.
- **Checkpoint:** none

### `## 🔵 §2 — Ways to Replace What's Running`

Owns the **deployment strategy vocabulary**, and owns *only* the vocabulary — B6 is explicit that the mechanics of rolling and Recreate stay at Ch 6 §4. This section's job is to give names and trade-offs to a mechanism the reader already operates, and to draw the line the reader most needs: **`RollingUpdate` and `Recreate` are values of a field on a Deployment. Blue/green, canary, and A/B are patterns that require tooling above the Deployment object.** That line discharges chapter-06:665 exactly as it was promised — *"patterns with names, implemented with tooling that sits above the Deployment object."*

Owns **progressive delivery** as the umbrella term, and the trade-off axis that makes the four comparable rather than a list: how much of your user base meets the new version before you know whether it works, against how much infrastructure the strategy demands. Canary needs traffic splitting — a service mesh or an Ingress controller — and metric analysis; blue/green needs neither and suits queue workers [source: argo-rollouts-strategies-2026-08-23]. That is the concrete reason a team picks one, and it is the answer a well-built question wants.

- **Objectives:** D3.1 (deployment strategies)
- **Introduces:** deployment-strategy-vocabulary; recreate-strategy; blue-green-deployment; canary-deployment; progressive-delivery
- **Figure:** `ch15-fig02-deployment-strategies-compared`
- **Cross-bearings out:** `Ch 6 §4 — changing the fleet under way` (mandatory — the mechanics live there and this section must visibly decline to restate them); `Ch 4 §5 — the universal join` (the `release: stable | canary` label values at chapter-04:788 — the reader has already *seen* a canary without being told); `Ch 10 §3 — the object is not the implementation` (canary's traffic-splitting requirement); `Ch 17 §5 — a network that knows what it's carrying` (mesh-based traffic splitting)
- **⚑ CANONICAL-FORM guardrail — a real collision, flagged for the author.** Shipped chapter-06:665 calls these *"release strategies."* The ledger's row calls them **"deployment strategy."** The ledger also reserves **"release"** for two other senses (a Kubernetes minor version; a Helm release) and Ch 14's own ⚠ block told the reader to qualify the word. **Recommendation: use "deployment strategy" as the headword throughout, and name "release strategy" exactly once as the synonym Ch 6 used**, so the reader who remembers Ch 6's phrase is not stranded. See Open Question 3.
- **⚠ RESEARCH-BLOCKED, in part.** `argo-rollouts-strategies-2026-08-23` covers RollingUpdate, Recreate, Blue-Green and Canary in usable detail. **It does not mention A/B testing at all**, and no other cached source does. B6, B2 and the arc outline all list A/B. See Open Question 2 — fetch or drop, but do not write it from memory.
- **Checkpoint:** **☆ TYB 1** — closes the application-and-its-releases arc (§1–§2)

### `## 🔵 §3 — Push, or Pull`

**PINNED §3.** Three published pointers land here, all from Ch 14 (:1047, :1117, :1309), plus chapter-12:485. Owns the chapter's central argument.

Opens with **CI/CD**, and opens with the fact that makes the whole section possible: Kubernetes *"does not deploy source code and does not build your application"* [source: k8s-docs-overview-2026-08-23]. CI/CD is somebody else's job, always was, and the cluster is indifferent to who does it — which is exactly what Ch 4's 🔭 Closer Look at :453 already told the reader. Then **push versus pull** as an architectural question rather than a preference: in push, a pipeline outside the cluster holds credentials to the cluster and reaches in. In pull, an agent inside the cluster holds credentials to a repository and reaches out. The consequences are concrete and should be developed concretely — where the credentials sit, what an attacker who compromises the pipeline gets, what happens between deploys, and what "the truth" means about a running system.

Then **GitOps**, defined by the four OpenGitOps principles verbatim [source: opengitops-principles-2026-08-23], with **principle 3 (Pulled Automatically)** given the emphasis it earns: it is what makes push-based CD *not GitOps*, and B1 trap 74 is exactly a reader who missed it. **Principle 4 (Continuously Reconciled)** carries the section's other trap (75): reconciliation is not a deploy-time event, it is continuous and indefinite — and a reader who spent Ch 3 §6 learning that sentence about controllers should feel the echo here without being told to. Do not tell them. §7 is for that.

- **Objectives:** D3.1 (CI/CD vs GitOps; the four OpenGitOps principles)
- **Introduces:** cicd; push-based-delivery; pull-based-delivery; gitops; opengitops-four-principles; declarative-principle; versioned-and-immutable-principle; pulled-automatically-principle; continuously-reconciled-principle; blast-radius
- **Figures:** `ch15-fig03-cicd-push-vs-gitops-pull` **and** `ch15-fig05-opengitops-four-principles` — two figures in one section, per B6's explicit instruction
- **Cross-bearings out:** `Ch 4 §1 — you file a declaration`; `Ch 3 §5 — the only door in`; `Ch 12 §4 — secrets are not encrypted` (where the pipeline's cluster credentials live); `Ch 12 §1 — four layers and four phases` (the deploy phase, discharging chapter-12:485)
- **⚑ Ledger guardrail — GitOps and CI/CD are both name-only-with-pointer in earlier chapters, and this is where the pointers are redeemed.** GitOps appears in shipped Ch 1:274, Ch 6:729, Ch 12:485 and Ch 14:679/:1028, always name-only. Verify during drafting that none of those quietly defined it; a reader arriving here must be meeting the definition for the first time.
- **⚠ Ch 3 §5 hazard — write this explicitly, it is the section's best ⚠ Navigational Hazards.** GitOps does **not** bypass the API server. The agent is another API client, subject to the same three gates (Ch 8 §2). A reader who takes "the repository is the source of truth" to mean the repository writes to the cluster directly has inverted Ch 3's central claim.
- **⚠ RESEARCH-BLOCKED.** The four principles are fully sourced. **The push/pull credential and blast-radius argument is not sourced anywhere in the corpus** and it is this section's core. See Open Question 1.
- **Checkpoint:** none

### `## 🔵 §4 — An Agent That Watches a Repository`

**PINNED §4, and the most-pointed-at section in the chapter — four numbered pointers from three chapters, plus two chapter-level ones.** Owns **Argo CD**, and owns it as a worked instance of §3's abstraction rather than as a product tour.

The structural claim first, because it discharges chapter-06:1037: Argo CD *"is implemented as a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state"* [source: argocd-overview-2026-08-23]. That is a controller, doing what Ch 3 §6 said controllers do, over a custom resource, exactly as Ch 6 §8 said anyone could write. Owns the **`Application` custom resource**, **source of truth**, **manifest sources** (Kustomize, Helm charts, Jsonnet, plain YAML/JSON directories, config-management plugins — trap 77, and the payoff on Ch 14:571's promise), and **tracking targets** (branch, tag, or a pinned commit — trap 78).

Then **`Synced` / `OutOfSync`**, which is the chapter's second Fixed Point and the section's most careful writing. `OutOfSync` means live state deviates from the target state in Git. **It is a drift signal, not an error** (trap 76), and the reader should be shown the case that proves it: a human edits an object by hand, nothing failed, and the application goes `OutOfSync`. Ch 4 §2's spec/status vocabulary is the whole explanation — this is status disagreeing with spec, where spec lives outside the cluster. Owns **sync operation**, **self-heal**, and **drift detection**.

Then **rollback by revert**, which discharges chapter-06:721 (*"and a third thing, again wearing it"*) and Ch 14:653. Argo CD offers *"rollback/roll-anywhere to any application configuration committed in Git"* [source: argocd-overview-2026-08-23]. This is the third mechanism wearing the word: not a Pod template restored from a ReplicaSet (Ch 6 §5), not a Helm release returned to a prior revision (Ch 14 §3), but a **commit reverted in a repository**, after which the agent does what it always does.

Then **the agent's identity**, which is the pin from chapter-05:781 and chapter-12:617 and must not be treated as a footnote. A delivery agent is a Pod. It has a ServiceAccount. Its job is to create, update and delete objects across namespaces, so its grants are broad — which makes it exactly the high-value subject Ch 12 §3 warned about. The corpus supports the shape directly: the ServiceAccount documentation names *"an external service needs to communicate with the Kubernetes API server (CI/CD pipelines)"* among the reasons non-human identities exist [source: k8s-docs-service-accounts-2026-08-23], and the push/pull distinction is precisely whether that identity lives inside or outside the cluster.

- **Objectives:** D3.1 (Argo CD — controller model, sync states, manifest sources, tracking, rollback)
- **Introduces:** argo-cd; argo-cd-application-resource; source-of-truth; manifest-source; tracking-branch-tag-commit; synced-outofsync; sync-operation; self-heal; drift-detection; rollback-by-revert; delivery-agent-identity
- **Figure:** `ch15-fig04-argocd-sync-states-and-hooks`
- **Cross-bearings out:** `Ch 3 §6 — controllers and the control loop`; `Ch 4 §2 — the anatomy of a record` (spec vs status, mandatory); `Ch 6 §8 — the control loop, extended` (custom resources); `Ch 6 §5 — every rollout is a revision`; `Ch 14 §2 — what a chart contains` (**MANDATORY B3 ANCHOR** — this is one of only two anchors standing between Ch 14 and never being retrieved); `Ch 14 §3 — chart, release, revision`; `Ch 12 §2 — who you are`; `Ch 12 §3 — what you may do`; `Ch 5 §6 — a Pod's identity`; `Ch 10 §3 — the object is not the implementation` (**recommended, by name** — an `Application` resource on a cluster with no Argo CD controller is the pattern's cleanest instance in the book, and the ledger licenses referring to it by name)
- **⚑ CANONICAL-FORM guardrails — four, all hard.** (1) **"Argo CD", two words, both capitalized** — never `ArgoCD`, never `Argo-CD`. (2) **"rollback by revert", that exact three-word form**, per the ledger and per Ch 14's integration finding that its own draft drifted to two variants in one section. (3) **Never bare "rollback"** where any of the three senses could be meant. (4) **Never "revision" for a Git commit** — say *commit*. Ch 6 §5 owns the unqualified word and Ch 14 §3 owns the Helm sense; a third unqualified use here would undo two chapters of discipline.
- **⛑ CONVENTION guardrail.** The book-level "state the pattern, never the count" rule applies. §4 may say a delivery agent is a controller and may back-bear to Ch 3 §6. It may **not** assert an ordinal — not "the fourth control loop", not "the third thing to wear this word" as a number. Ch 6:719 published a closed set for *rollback* ("twice more in this book"), so §4 **may** say it is discharging the second of those two. It may not invent any other count.
- **⚠ RESEARCH-BLOCKED — the worst gap in the chapter.** `argocd-overview-2026-08-23` is 20 lines. It names `OutOfSync`, sync, drift detection and rollback in a features list, and **never once uses the word `Application`** — the custom resource this section is built on. Self-heal, sync policy and prune are absent entirely. See Open Question 1; this section cannot be drafted from cache.
- **Checkpoint:** **☆ TYB 2** — closes the push/pull-and-the-agent arc (§3–§4)

### `## 🟡 §5 — Ordering the Sync`

**PINNED §5**, by chapter-12:866 — the RBAC binding that cannot be retargeted, *"under a system that reconciles a cluster against a repository, a delete-and-create rather than an update."* Owns **sync hooks** (`PreSync` / `Sync` / `PostSync`) and **sync waves**.

The section's reason to exist, stated as a problem before any mechanism: `kubectl apply -f` over a directory gave no ordering guarantee, and Ch 14 §1 named that as one of the four failures a package solves. GitOps does not inherit the fix. An agent reconciling a whole repository faces the same problem at a larger scale — a database migration that must run before the new version starts, a CRD that must exist before the custom resource using it, a namespace before its contents — and hooks and waves are the answer. Argo CD's own documentation ties hooks directly to §2's vocabulary: *"PreSync, Sync, PostSync hooks to support complex application rollouts (e.g. blue/green and canary upgrades)"* [source: argocd-overview-2026-08-23], which is the mechanism §2 promised but could not supply.

Discharges Ch 12:866 explicitly: a RoleBinding that must be deleted and recreated rather than updated is a real ordering constraint in a reconciled system, and it is the kind of case waves exist for.

- **Objectives:** D3.1 (sync hooks, sync waves, ordering)
- **Introduces:** sync-hook-phases; sync-wave
- **Figure:** `ch15-fig06-sync-waves-and-hook-phases` — **new; not in the arc stub list.** See Required figures and Open Question 5.
- **Cross-bearings out:** `Ch 12 §3 — what you may do` (mandatory — the binding-immutability case is the pin); `Ch 14 §1 — why a folder of YAML stops working` (the ordering failure, returning); `Ch 14 §6 — which one, when` (the `crds/` ordering solution, and why an agent needs its own); `Ch 6 §8 — the control loop, extended`
- **Depth ruling — 🟡 Advanced, and hold the line.** Hooks and waves are almost certainly deeper than an associate exam reaches. They are here because a published pointer put them here and because they answer a question the chapter genuinely raises. Teach the *shape* — phases run in order; waves order resources within a phase — and **do not teach annotation syntax**. A reader who can name the three phases and say why ordering is a problem GitOps has has learned everything this section owes them.
- **⚠ RESEARCH-BLOCKED.** Hook phases are named in one clause of the cached features list with no semantics. **Sync waves do not appear in the corpus at all.** See Open Question 1.
- **Checkpoint:** none

### `## 🔵 §6 — The Other Agent, and More Than One Cluster`

Owns **Flux**, closing blocking gap G18, and owns **multi-cluster delivery**. Flux is a **GitOps Toolkit** — *"a set of composable APIs and specialized tools"* [source: flux-concepts-2026-08-23] — which is a genuinely different design posture from Argo CD's integrated application-and-UI model, and that contrast is the section's teaching content. Owns the **controller set** (Source, Kustomize, Helm, Notification, Image Automation) and **sources** as a first-class concept (`GitRepository`, `OCIRepository`, `HelmRepository`, `Bucket`) — which back-bears neatly to Ch 14 §4's OCI-registries-hold-charts fact.

Two facts from the cache earn their place. First, Flux's Kustomization *"reconciles Kubernetes resources from a source into the cluster (every five minutes by default); changes made with kubectl are reverted unless reconciliation is suspended"* — the single most concrete statement of principle 4 available anywhere in the corpus, and worth a ⚓ **Worth Securing**. Second, **bootstrap**: Flux installs itself in a GitOps manner, pushing its own manifests to a repository so that *"Flux manages itself like any other resource."* That is a self-application the reader should be allowed to enjoy for a sentence, and it is the natural bridge into §7.

Multi-cluster delivery closes the section: where does desired state live when there are twenty clusters, and what does each model do about it. Argo CD manages and deploys to multiple clusters from one control point; Flux's model is a Flux per cluster, each pulling. Both are honest answers to the same question.

- **Objectives:** D3.1 (Flux; multi-cluster delivery)
- **Introduces:** flux; flux-controller-set; flux-bootstrap; multi-cluster-delivery
- **Cross-bearings out:** `Ch 14 §4 — where charts come from` (OCI as a source); `Ch 14 §5 — patching instead of templating` (Flux's Kustomize controller); `Ch 6 §8 — the control loop, extended`; `Ch 8 §5 — who owns the control plane` (multi-cluster)
- **Figure:** none, deliberately. An Argo-vs-Flux comparison table is better as a table — it is a vocabulary contrast with no spatial or temporal structure, which is Part 18.9's explicit *does-not-warrant* case. `ch15-fig02` and `ch15-fig04` already carry this chapter's comparison load.
- **⚑ CANONICAL-FORM guardrail:** **"Flux"**, never `FluxCD`. Write "Flux v2" only where disambiguation from v1 is genuinely needed, which at associate tier it is not.
- **⚠ GRADED-USE restriction.** Argo and Flux's CNCF **graduated** status may be stated once, tagged and dated [source: cncf-project-maturity-levels-2026-08-23]. B3 bars retrieving the dated graduated roster: **no question in this chapter or in Ch 20 may turn on which projects are graduated.** The maturity *levels* are Ch 17 §2's and are the durable retrieval target.
- **Checkpoint:** **☆ TYB 3** — closes the ordering-and-alternatives arc (§5–§6)

### `## ☀️ §7 — The Control Loop, Pointed at a Repository`

**PINNED §7 by chapter-09:1249, and the book's PRIMARY ZENITH.** Three chapter-level pointers from Ch 3 (:655, :832, :957), one from Ch 4 (:453), one from Ch 6 (:1145), and Ch 14's Voyage Ahead all converge here. This is the section the whole of Part IV was ordered to set up.

**Owns no new material.** Everything in it has been taught. The section's entire content is a substitution performed in front of the reader: take the loop from Ch 3 §6 — desired state, current state, an action closing the gap, repeating without end — and move the desired state out of etcd and into a Git repository. Nothing else changes. Not the API server's position, not the watch-don't-tell coordination, not the controller's shape. Ch 3 said it at :653 and told the reader this chapter would retrieve it: *"the coordination mechanism in Kubernetes is watching, not telling… the same architecture, with a different thing in the hub position."* §7 retrieves exactly that sentence.

Then the four principles, re-read as the loop: **declarative** is Ch 4 §1; **versioned and immutable** is what a repository adds that etcd does not; **pulled automatically** is the watch; **continuously reconciled** is the loop itself. Trap 73 dies here — GitOps is not "running CI from Git" because none of the four principles mentions integration, building, or a pipeline. The payoff sentence is the chapter title arriving as a conclusion: the chart is the truth because something is continuously making it true.

Closes on Ch 6:1145's promise, which was written to be redeemed here: *"When you meet that, it will look like a new idea for about ten seconds."*

- **Figure:** `ch15-zenith-control-loop-pointed-at-a-repo`
- **Cross-bearings out:** `Ch 3 §6 — controllers and the control loop` (mandatory, and the figure must rhyme with it); `Ch 4 §1 — you file a declaration`; `Ch 17 §3 — small pieces, replaced whole` (declarative APIs as a cloud native characteristic); `Ch 17 §4 — the four pluggable interfaces, collected`
- **⛑ CONVENTION guardrail — read before drafting, this is the sharpest constraint in the chapter.** Ch 14's integration pass (item 5) flagged that shipped Ch 6 closes by telling the reader they have seen the loop *twice* and *"the third time is the one that matters"* — meaning this section — while Ch 7 and Ch 11 added sightings afterward, so a reader counting literally arrives here at four-or-more. The ledger's **"state the pattern, never the count"** rule resolves it: **§7 must assert no number.** Not "the third time," not "the sixth loop," not "you have now seen this four times." Say that it is the same loop and demonstrate the substitution. The recognition does the work; arithmetic can only undermine it. See Open Question 6.
- **⚠ Zenith-integrity note.** The subtitle already states this section's claim. §7 therefore cannot rely on surprise and must not be written as though it can. Its move is **demonstration**, not revelation: perform the substitution, show that nothing else moved, and let the reader verify a claim they were handed 25 pages ago. That is a legitimate and arguably stronger Zenith shape, but it is a different one, and drafting that reaches for a reveal will produce a flat section.

---

## 5. ☆ Taking Your Bearings checkpoints

Three checkpoints, **16 questions, 4 retrieval = exactly 25.0%** — the arc outline's ceiling for this chapter, which it shares with Ch 13, 16, 17 and 18.

**Retrieval is defined narrowly**, per the Ch 13 and Ch 14 precedent, and drafting must hold the line: a retrieval question is one whose *answer* lives in an earlier chapter. A question about `OutOfSync` that merely leans on the reader knowing what `status` is remains a chapter question.

| # | Falls after | Topic | Qs | Retrieval | Drawn from |
|---|---|---|---|---|---|
| TYB 1 | §2 | The application, and the shapes of a release | 6 | 2 | **Ch 4 §4** — what "store config in the environment" concretely means in Kubernetes (≥4-back floor, satisfied by eleven chapters); **Ch 6 §4** — what `maxSurge` and `maxUnavailable` actually control, asked so the answer is the Deployment's mechanics and not §2's vocabulary |
| TYB 2 | §4 | Push, pull, and the agent | 5 | 1 | **Ch 12 §3** — what an in-cluster subject needs before it may create objects in a namespace it does not own; the item asks about the delivery agent but the *answer* is RBAC, which is what makes it retrieval |
| TYB 3 | §6 | Ordering, and the other agent | 5 | 1 | **Ch 3 §6** — the control loop, stated in its own terms. **Placed here deliberately, immediately before §7**, so the reader arrives at the Zenith having just retrieved the thing the Zenith is about. This is the single most important retrieval item in the chapter. |

The arc outline requires draws "from all previous" at 25% with a ≥4-back floor; Ch 3, Ch 4, Ch 6 and Ch 12 satisfy both comfortably, and the Ch 9–13 window is covered by TYB 2's Ch 12 draw.

Every checkpoint carries trap answers targeting the misconceptions in the Exam Alert below, why-wrong explanations for **all** options, and a revision prompt naming a **section** for 0–2 scorers.

**TYB 2 must include the `OutOfSync`-is-not-an-error item.** That is B1 trap 76, it is the chapter's second Fixed Point, and it is the single distinction most likely to be tested from this material. A checkpoint that omits it is not doing its job.

---

## 6. Exam Alert plan

**High-priority topics.** Four, and the chapter is these four:

1. **The four OpenGitOps principles, in order, with the words that matter.** Declarative; versioned and immutable; **pulled** automatically; continuously reconciled. "Pulled" and "continuously" are the two words that carry the distinction — a definition missing either describes something that is not GitOps.
2. **`OutOfSync` is a drift signal, not an error.** It reports that live state deviates from the target state in Git. A human editing the cluster by hand produces it. Nothing failed.
3. **Argo CD is a Kubernetes controller.** It reconciles a custom resource against desired state that happens to live outside the cluster. It does not bypass the API server, and it is not a new kind of technology.
4. **Deployment strategy vocabulary versus Deployment fields.** `RollingUpdate` and `Recreate` are values on a Deployment. Blue/green, canary and A/B are patterns implemented by tooling above it.

**Common traps** — ⚠ Navigational Hazards, loss-aversion framing. Origins noted, because six are B1 `[source]` traps and the rest are derived:

| Trap | The correct understanding | Origin |
|---|---|---|
| "GitOps means running CI from Git" | GitOps is four principles about *desired state*. Continuous integration is not one of them, and the cluster does not care who built the artifact. | B1 #73 |
| Assuming a pipeline pushes to the cluster | Principle 3 is explicit: agents **pull** desired-state declarations from the source. Push-based CD is not GitOps, whatever it is stored in. | B1 #74 |
| Treating reconciliation as a deploy-time event | Principle 4 is **continuous** observation and application, indefinitely — the same property that makes a ReplicaSet recreate a Pod you deleted last Tuesday. | B1 #75 |
| "`OutOfSync` means the sync failed" | It means live state deviates from the Git target state, including because a person changed something. Signal, not error. | B1 #76 |
| "Argo CD only deploys plain YAML" | Kustomize applications, Helm charts, Jsonnet, plain YAML/JSON directories, and custom config-management plugins. | B1 #77 |
| "Argo CD can only track a branch" | Branches, tags, or a **pinned Git commit**. | B1 #78 |
| Assuming a GitOps agent writes to the cluster's datastore directly | It is an API client like any other, subject to authentication, authorization and admission. Chapter 3's claim about the only door in is not suspended. | Derived, §3 + Ch 3 §5 |
| Assuming a delivery agent needs no identity because it is "infrastructure" | It is a Pod with a ServiceAccount and broad grants, which makes it one of the highest-value subjects in the cluster. | Derived, §4 + Ch 12 §3 |
| Collapsing the third rollback into one of the first two | Ch 6's `rollout undo` restores a Pod template. Ch 14's `helm rollback` returns a release to a prior revision. **Rollback by revert** changes a commit and lets the agent reconcile. Three mechanisms, one word. | Derived, §4 + Ch 6 §5 + Ch 14 §3 |
| Assuming a Deployment can express blue/green or canary by itself | Both need something above the Deployment; canary additionally needs traffic splitting and metric analysis. | B1-adjacent, §2 |

**Framing constraint, restated because Exam Alerts are where it slips:** none of these may be described as "frequently tested" or "commonly appears." CNCF publishes no sub-topic list for this competency and does not name GitOps, Argo CD, or Flux anywhere. "Easy to confuse" and "the distinction the material rewards" are the available registers. See Open Question 7.

---

## 7. Practice Questions plan

**Target: 21**, per `question_budget.practice_questions` and B4, unmodified.

| Section | Items | Rationale |
|---|---|---|
| §1 twelve-factor | 3 | Factor III and the platform/application partition; recall-shaped and cheap |
| §2 strategies | 4 | Four named patterns, and the field-versus-pattern line that trips readers |
| §3 push/pull and the principles | 5 | The chapter's densest exam material; traps 73, 74, 75 all live here |
| §4 Argo CD | 5 | Traps 76, 77, 78, plus the identity pin and the three-rollback discrimination |
| §5 ordering | 2 | 🟡 depth; two well-built items, no more — the section is deliberately shallow |
| §6 Flux and multi-cluster | 2 | Contrast items only; no roster recall |

**Interleaving strategy.** At least six stems present a *situation* and ask what the reader would conclude or reach for, rather than asking for a definition — the shape a glossary cannot answer. Four stems cross domains deliberately: one pairs a GitOps agent with RBAC grants (D2.2 security), one pairs `OutOfSync` with spec/status (D1.1 core concepts), one pairs canary with traffic splitting (D2.1 networking), one pairs a chart as manifest source with the release/revision distinction (D3.1 back into Ch 14). Per skill Part 10, wrong options are built to catch the specific misconceptions tabulated in the Exam Alert, and every option gets a why-wrong explanation.

**Barred from all graded text in this chapter:**

- **Knative, serverless, scale to zero, service mesh, the CNCF cloud native definition, and the autoscaling landscape.** All Ch 17's, and B1 traps 82–84 belong there. §2 may *name* a mesh as canary's traffic-splitting requirement with a pointer; a question testing meshes takes Ch 17's material.
- **`kubectl debug`, ephemeral containers, and application-scope triage.** Ch 16's, one chapter away.
- **Helm chart anatomy, `charts/` versus a chart repository, and `helm rollback` as a standalone subject.** Ch 14's, and B1 traps 79–81 are its. Ch 15 may test the *three-way rollback discrimination*, because that is this chapter's contribution and Ch 6 published the promise; it may not test what a `Chart.yaml` contains.
- **Which CNCF projects are graduated.** B3 bars retrieval of the dated roster; the maturity levels are Ch 17 §2's.
- **PodDisruptionBudget** — unowned book-wide (⚑3 in the ledger), barred everywhere including here, and worth naming explicitly because a chapter about controlled rollouts is exactly where it would drift in.
- **ABAC, SRE, descheduler, eBPF** — glossary-only with graded-use restrictions.
- **A/B testing**, unless Open Question 2 is resolved by a fetch. If it is not, A/B may not appear in a stem, a key, or a distractor.
- **Any item requiring Argo CD or Flux CLI syntax, or hook/wave annotation syntax.** `kb_tags.commands` is empty by design; a question that needs a command the chapter never taught exceeds both the chapter and the credential.

---

## 8. Required figures

Seven anchors: six concept diagrams plus one Zenith, inside skill Part 18.10's 2–8 band. Five are the arc-outline stubs at their exact IDs; one is added.

| Anchor | § | Type | Purpose and content |
|---|---|---|---|
| `ch15-fig01-twelve-factor-in-kubernetes` | §1 | Partition, three columns | The twelve factors sorted into three columns by *who solves this*: **the platform gives you this** (III, VI, VIII, IX, XI), **the platform makes this easy** (IV, V, X), **still your application's problem** (I, II, VII, XII). Each factor is a Roman numeral plus a two-word label; the column headings carry the argument. The visual claim is the sort itself — twelve unrelated rules become three groups with a reason. **Label discipline:** twelve numerals is more than Part 18.12's ~7-label guidance allows for a *diagram*, but this is a sorted table rendered as a figure and the numerals are read as a set, not individually. Stage 10 should confirm against the anti-pattern list. **Glyph-free** — partition family. |
| `ch15-fig02-deployment-strategies-compared` | §2 | Comparative, four panels | Four small panels on one shared timeline axis, each showing old-version and new-version instances against traffic: **Recreate** (all old down, gap, all new up — the visible downtime), **RollingUpdate** (staggered replacement, no gap), **Blue/Green** (both full sets alive, traffic switch as a single moment), **Canary** (a small slice of traffic to new, the rest to old, then widening). A footer row states what each demands: nothing extra · nothing extra · double capacity · traffic splitting plus metrics. **The panel borders carry the chapter's line:** the first two panels are drawn inside one enclosure labeled *fields on a Deployment*, the last two inside another labeled *patterns needing tooling above it*. That enclosure is the figure's real payload. ≤7 labels per panel. **Glyph-free** — comparison family. |
| `ch15-fig03-cicd-push-vs-gitops-pull` | §3 | Comparative, two panels, mirrored | Top: **push.** A pipeline outside the cluster boundary, an arrow crossing inward, and a key icon drawn *outside* the boundary. Bottom: **pull.** An agent inside the boundary, an arrow reaching outward to a repository, and the key drawn *inside*. The cluster boundary is the same line in both panels and the arrow is the only thing that reverses. **The key's position is the figure's whole argument** and should be its most visually emphasized element — everything else is scaffolding for it. ≤7 labels. **Glyph-free.** |
| `ch15-fig04-argocd-sync-states-and-hooks` | §4 | State + comparison | Git target state on one side, live cluster state on the other, and the agent between them holding both. Two states rendered as the comparison's outcome: **`Synced`** (the two agree) and **`OutOfSync`** (they do not), with the `OutOfSync` panel showing the cause a reader will not expect — *a person edited the cluster* — rather than a failed deploy. A sync operation is drawn as the action that closes the gap. ≤7 labels. **Glyph-free.** **Slug note, recorded so no downstream stage reads it as drift:** the arc stub's ID says "and-hooks", but hooks belong to §5 and a figure spanning two sections violates spatial contiguity (Part 18.6). This figure renders **sync states only**; the hooks half of the stub's promise is discharged by `ch15-fig06` in §5. See Open Question 5. |
| `ch15-fig05-opengitops-four-principles` | §3 | Enumeration, four blocks | The four principles as four labeled blocks, each with its one-line definition verbatim from the source and — critically — **a small marker showing which earlier chapter already taught it**: declarative → Ch 4, versioned and immutable → *new here*, pulled automatically → Ch 3, continuously reconciled → Ch 3. Those markers are what make this more than a list, and they are the visual seed §7 harvests. **Renders inside §3 per B6's explicit instruction**, alongside `fig03`. ≤7 labels. **Glyph-free.** |
| `ch15-fig06-sync-waves-and-hook-phases` | §5 | Sequence, two axes | **New — not in the arc stub list.** A horizontal phase axis (`PreSync` → `Sync` → `PostSync`) crossed by a vertical wave axis inside the `Sync` phase, showing three resources landing in ordered waves — namespace, then CRD, then the custom resource that needs it. **Added because ordering is temporal structure, which is Part 18.9's strongest illustrate-this criterion, and because prose describing two nested orderings is exactly the divided-attention failure Part 5 forbids.** ≤7 labels. **Glyph policy provisional — glyph-free recommended.** This sequences, but Stage 10 should confirm against `glyph-ledger.yaml` whether it reads as the pipeline family (which carries glyphs) or as an ordering diagram (which does not); the Ch 13 and Ch 14 precedents both distinguished staged-flow from pipeline. |
| `ch15-zenith-control-loop-pointed-at-a-repo` | §7 | Dramatic synthesis | **The book's most consequential figure, and it has one job: rhyme with `ch03-fig02-control-loop-desired-vs-current`.** Same composition, same shapes, same arrow geometry, same visual weight — with the desired-state store swapped from etcd to a Git repository, and that one element visually marked as the only substitution. If a reader cannot lay the two figures side by side and see them as the same drawing, the Zenith has failed and no amount of prose recovers it. **The arc outline records this as a hard requirement**, and `ch03-fig02` was designed for re-presentation at three altitudes (Ch 6, Ch 15, Ch 17) precisely so this could work. Stage 10 must open `ch03-fig02`'s source before writing this spec. Exactly one Zenith per content chapter, per Part 18.10. |

**Deviations from the arc-outline stub list, recorded so no downstream stage reads them as drift.** One figure added (`ch15-fig06`) with the rationale above; all five original stubs are retained at their original anchor IDs. **Figure numbers are not in document order** — `fig05` renders in §3 while `fig04` renders in §4 — because the B6 skeleton explicitly pins `ch15-fig05-opengitops-four-principles` inside §3. That pin is binding text in a binding contract and is not renumbered around. **§6 is deliberately figure-free**; its content is a vocabulary contrast with no spatial or temporal structure, and Part 18.9 names that as a does-not-warrant case.

---

## 9. Open questions for the author

**1. Blocking research — Stage 2 must fetch these, and two of them gate sections that carry published promises.** The corpus holds roughly 93 lines across five snapshots on this chapter's entire subject: `opengitops-principles` (17), `argocd-overview` (20), `flux-concepts` (18), `twelve-factor-app` (23), `argo-rollouts-strategies` (15). That is better proportioned than Ch 14's 33 lines, but it is concentrated in the wrong places — the four OpenGitOps principles are fully sourced while **§4's `Application` resource and §5's sync waves have no source at all**. Every factual sentence in this book carries a `[source:]` tag. Required snapshots, in priority order:

- `argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/` (or `.../core_concepts/`) — **the critical one.** The `Application` custom resource, `AppProject`, and the object model §4 is built on. The cached overview never uses the word "Application."
- `argo-cd.readthedocs.io/en/stable/user-guide/auto_sync/` — automated sync policy, **self-heal**, and prune. §4 names all three and cache supports none.
- `argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/` — **hooks and waves, §5's entire content.** `PreSync`/`Sync`/`PostSync` semantics and wave ordering. Sync waves appear nowhere in the corpus.
- Argo CD or Flux **security/architecture** documentation covering where the agent's credentials live and what its ServiceAccount must hold — **§4's identity pin, promised twice in shipped text** (chapter-05:781, chapter-12:617). `k8s-docs-service-accounts-2026-08-23:16` supports the shape but not the specifics.
- `opengitops.dev/faq` or the OpenGitOps principles repository — **§3's push/pull credential and blast-radius argument**, which is the section's core and is currently unsourced.
- `fluxcd.io/flux/components/` — the controller set beyond names, for §6.
- Argo Rollouts or an equivalent on **A/B testing** — see item 2.

**2. A/B testing has no source anywhere in the corpus — fetch or drop.** B2, B6 and the arc outline all list A/B alongside rolling, Recreate, blue/green and canary. `argo-rollouts-strategies-2026-08-23` covers the other four in usable detail and **never mentions A/B**. Recommendation: **fetch a source, or cut A/B from §2 and from all graded text.** Writing it from memory would put an untagged factual claim in the chapter that most explicitly defines its own terms, and A/B is genuinely ambiguous in this space — it is a product-experimentation technique that release tooling can implement, not a deployment strategy in the same sense as the other four. If the fetch fails, cutting it costs the chapter very little and an outline note can record why. **Confirm.**

**3. "Deployment strategy" versus "release strategy" — a genuine collision, recommendation firm.** Shipped chapter-06:665 calls these *"release strategies."* The B7 ledger's row calls the concept **"Deployment strategy"** and assigns it to §2. The ledger separately reserves **"release"** for a Kubernetes minor version and for a Helm release, and shipped Ch 14:679 already instructed the reader to qualify the word. Three senses of "release" in two adjacent chapters is one too many. **Recommendation: "deployment strategy" is the headword throughout §2; name "release strategy" exactly once as the synonym Ch 6 used, so a reader holding Ch 6's phrase is not stranded.** Cheap, and it keeps the book's own discipline. **Confirm.**

**4. Argo CD's first appearance is Chapter 3, not this chapter — recorded, no action needed.** The B7 ledger projects Argo CD's first appearance as `Ch 15 §3 †` with an empty "Earlier chapters must" column. Shipped **chapter-03:653** names it: *"the sentence Chapter 15 will retrieve when a controller called Argo CD watches a Git repository that sits outside the cluster"* [source: argocd-overview-2026-08-23]. This falsifies a projection; it violates nothing, because the ledger required nothing of earlier chapters and the use is name-only with an explicit forward pointer. **Two consequences worth carrying into drafting:** (a) §4 may not treat "Argo CD" as a word the reader has never seen; (b) Ch 3 pre-framed this chapter's Zenith in that same paragraph — *"the same architecture, with a different thing in the hub position"* — which means §7 is retrieving a sentence, not proposing one. Recorded here so the term-ownership stage can correct the projection at its next run.

**5. Figure `ch15-fig04`'s slug names content it will not carry — recommendation, low stakes.** The arc stub is `ch15-fig04-argocd-sync-states-and-hooks`, but hooks belong to §5 and one figure cannot render in two sections without breaking spatial contiguity. This outline keeps the stub ID unchanged (it is named in a binding contract), narrows the figure's content to sync states, and adds `ch15-fig06` for §5's ordering. **Recommendation: leave the ID as-is unless the diagram pipeline requires slug/content agreement, in which case Stage 10 renames it to `ch15-fig04-argocd-application-and-sync-states` and records the rename.** No shipped text and no `image-specs.md` references any `ch15-*` anchor — verified 2026-08-31 — so a rename is free if wanted. **Confirm which.**

**6. §7's Zenith shape — the constraint is unusual and worth your eye.** Two things collide. First, the subtitle states the Zenith's claim on the chapter's second line, so §7 cannot be written as a reveal. Second, Ch 14's integration pass flagged that shipped Ch 6 promised *"the third time is the one that matters"* while Ch 7 and Ch 11 subsequently added control-loop sightings, so a reader counting literally arrives here mis-counted — and the book-level convention forbids §7 from asserting any number to fix it. The resulting shape is a **demonstration**: perform the substitution in front of the reader, show that nothing else in the architecture moved, and let them verify a claim they were handed 25 pages earlier. That is a legitimate Zenith and arguably a stronger one than a reveal, but it is not the shape the other Zeniths in this book use, and drafting that reaches for surprise will produce a flat section. **Recorded for your awareness rather than as a question needing an answer — unless you would prefer the subtitle changed**, which is the only other lever and would cost agreement with two upstream contracts.

**7. The honesty framing — confirmation wanted, recommendation firm.** Verified against `cncf-kcna-curriculum-pdf-2026-08-23` line 15: CNCF publishes *"Cloud Native Application Delivery: Application Delivery; Debugging"* and nothing else. The snapshot contains no occurrence of GitOps, Argo, Flux, twelve-factor, or canary. Unlike Ch 14, there is not even an LFS250 syllabus snapshot to lean on — no cached source enumerates that course's modules. What the corpus *does* support is that Argo and Flux are CNCF graduated projects and OpenGitOps is a CNCF project, which is the honest basis for the inference. **Recommendation: one short back-bearing to Ch 14's fuller statement plus that one sentence of positive basis, then enforce the no-frequency-claims rule silently.** Repeating Ch 14's paragraph at length here would be channel redundancy and would read as anxiety rather than candor. **Confirm.**

**8. Two facts that must not be written from memory.** (a) **Whether Argo CD's self-heal is on by default.** §4's account of drift is materially different depending on the answer, and the difference is exactly the kind of detail a well-built question turns on. (b) **Flux's five-minute default reconciliation interval** — the cached source states it and it is this chapter's most concrete instance of principle 4, but confirm it has not moved before writing it as a ⚓ Worth Securing. If either is unpinned after the fetches, write the shape and drop the specific, per house practice.

**9. Section-count sanity, recorded pre-emptively.** Seven sections against 7 weight points, matching Ch 11 and Ch 14 in shape. Not inflation: §7 is the Zenith and owns no new material, §5 is deliberately shallow at 🟡, and §6 is short. The teaching load is genuinely in §2, §3 and §4. No compression is recommended and four sections cannot move regardless — §3, §4, §5 and §7 are pinned by nine published pointers.

**10. Acronym register.** One new expansion is owed: **CI/CD** — *Continuous Integration, Delivery, and Deployment* — which the ledger assigns to Ch 15 §3 and which the corpus already expands [source: k8s-docs-overview-2026-08-23]. The ledger's register also lists **CD** and **CI** as separate rows owned here; expand all three at first use in §3, once. No other new acronyms are expected. **OCI** is registered to Ch 2 §5 and **CRD** to Ch 6 §8, both already expanded. Recorded for the glossary build alongside the existing Ch 9/10/11/13/14 debts.

**11. Epigraph.** The material invites a quote about intent versus outcome, about records as truth, or about the difference between saying what should be and making it so. Preference order per skill Part 15: a real practitioner or engineering figure over a Lodestar original. **One strong candidate is already in the book:** Ch 14's closing quote — *"The chart is what you meant. The cluster is what happened. The interesting question is who keeps them the same"* — is a Lodestar original that states this chapter's thesis and its title. Reusing it verbatim as this chapter's epigraph would be a deliberate and legible callback rather than a repetition, and it would bind the two chapters of Part IV's delivery arc. **Flagged as an option, not a recommendation** — an epigraph that the reader met eight pages ago carries less arousal than a new one, and the structural contract's preference is for outside voices. Author's call.

---

*Stage 1 complete for Chapter 15. Seven sections adopted unchanged from the B6 skeleton, four of them pinned by nine published cross-bearings from five shipped chapters. Three checkpoints (16 Bearings, 4 retrieval = exactly the 25% ceiling), 8 Soundings, 21 Practice Questions, 45 total. Seven figures — five arc stubs retained at their IDs, one added, one deliberate out-of-document-order pin honored. Two blocking research gaps that gate sections carrying published promises (§4's `Application` model and agent identity; §5's sync waves), one unsourced topic recommended for cutting if a fetch fails (A/B testing), and one falsified term-ledger projection recorded (Argo CD first appears in Chapter 3).*
I have everything I need — B4's budget, the arc-outline figure stubs, the D2.3 concept list, and all nine section-pinned cross-bearings verified against shipped text. Here is the outline.

---

I have both binding contracts, the arc-outline block, B1's D2.3 concept table, and every published cross-bearing into Ch 13 verified by line number against chapters 01–12. **Six of eight sections are pinned by number** — more than B6's skeleton recorded, because Ch 8 and Ch 10 also pin §6 and §7. Only §1 and §8 are free. Three research gaps are blocking, and G2 is B1's highest-risk single gap in the book.

```
---
chapter: 13
chapter_type: "content"
title: "When the Cluster Won't Answer"
subtitle: "Read the phase before you read the logs"
exam_domain: "Container Orchestration (competency: Troubleshooting)"
domain_weight_pct: 4
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE NOTE. Seven words, from the arc outline and the chapter
#-- lineup, carried forward unmodified. It states the chapter's thesis
#-- and is also the §8 Zenith heading, so subtitle and synthesis agree by
#-- construction — the Ch 12 pattern. It states a Fixed Point, which is
#-- the subtitle's job and NOT a licence for the Soundings. See the
#-- FIXED-POINT SPOILER CHECK below.

#-- EXAM_DOMAIN NOTE. D2.3 Troubleshooting, in the house form shipped by
#-- ch-04/-09/-10/-11/-12. No competency ambiguity: this chapter is
#-- platform scope only. Its twin — D3.2 Debugging, application scope —
#-- is Ch 16, and the two are bound by reciprocal cross-bearings rather
#-- than by shared material.
#--
#-- The 4% figure is the chapter's AUTHORED allocation, not CNCF data.
#-- CNCF publishes four domain weights (44/28/16/12) and no
#-- sub-competency weights — B1 gap G33, B2 disclosure #1. The in-chapter
#-- metadata line must carry the published 28% for D2 with its source tag
#-- and the authored-allocation disclaimer, matching the shipped house
#-- form. Do NOT present 4% as published. 4 is the smallest allocation in
#-- Part III, and the chapter still runs eight sections — see the
#-- SECTION-COUNT note below before anyone tries to compress it.

#-- PREREQ NOTE. `heavy`, and heavy in a shape no other chapter has:
#-- this chapter is mostly APPLIED prior material. The arc outline's
#-- words — "retrieval IS this chapter's method, not a tax on it."
#-- The load-bearing seven:
#--   Ch 2 §6 (imagePullPolicy, :latest)   -> §2
#--   Ch 4 §4 (ConfigMap/Secret)           -> §2
#--   Ch 5 §5 (phase vs container state)   -> §1, §2, §4  ** the big one **
#--   Ch 5 §8 (requests, limits, QoS)      -> §4
#--   Ch 7 §2/§4 (Pending, taints)         -> §2   ** Ch 7 decay-fix **
#--   Ch 8 §6 (version skew)               -> §6   ** Ch 8 decay-fix **
#--   Ch 10 §3 (nothing without the component) -> §7  ** by name **
#-- Ch 5 §5 is not optional. The whole chapter is a lookup keyed on the
#-- phase; a reader who has lost the phase/state taxonomy cannot receive
#-- §1's method, and every section after it degrades to a list of strings
#-- to memorize — which is exactly the failure mode this chapter exists
#-- to prevent.
#--
#-- Consequence for drafting: the Soundings 0-2 branch names Ch 5 §5 as
#-- the one section to re-read BEFORE starting, not alongside. Ch 11/Ch 12
#-- precedent.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "focused" — 4
#-- points. Planning signal only, NOT a target. Note that "focused" and
#-- eight sections are not in tension here: see SECTION-COUNT below.
#--
#-- ⚠ SECTION NUMBERING IS LOAD-BEARING. Fourteen published cross-bearings
#-- point at this chapter. NINE name a section by number, and they cover
#-- SIX of the eight sections:
#--   chapter-11:588  -> Ch 13 §2   Pods that never start (PVC never binds)
#--   chapter-12:1099 -> Ch 13 §2   pods that never start (missing Secret)
#--   chapter-12:1340 -> Ch 13 §2   pods that never start (PSA refusal)
#--   chapter-05:392  -> Ch 13 §3   reading logs from a multi-container Pod
#--   chapter-06:778  -> Ch 13 §3   reading events for ProgressDeadlineExceeded
#--   chapter-05:1027 -> Ch 13 §4   OOMKilled and Evicted
#--   chapter-03:451  -> Ch 13 §5   crictl, and why a node-level tool exists
#--   chapter-08:923  -> Ch 13 §6   version skew as a cause you'd misdiagnose
#--   chapter-10:677  -> Ch 13 §7   kubectl top with no metrics-server
#-- All nine match the B6 skeleton exactly. §2, §3, §4, §5, §6 and §7 are
#-- FIXED. Only §1 and §8 are free — and both are structurally pinned
#-- anyway, §1 by chapter-07:426 ("Chapter 13's whole opening move") and
#-- §8 by the Ch 16 §1 handoff.
#-- Verified 2026-08-31 against chapters 01-12.
#--
#-- SECTION-COUNT note. Eight sections against 4 weight points is the
#-- book's highest section-to-weight ratio, and B6 already ruled on it:
#-- it is correct, because six shipped chapters point INTO this one and
#-- each signature family needs an addressable home. Do not compress to
#-- chase the "focused" depth band. Depth per section is what "focused"
#-- constrains; the section count is fixed by inbound pointers.
sections:
  - name: "Whose Problem Is This, and What to Read First"
    objectives: ["D2.3"]
    requires_figure: true
    figure_anchor: "ch13-fig01-two-audience-split"
    checkpoint_after: false

  - name: "Pods That Never Start"
    objectives: ["D2.3"]
    requires_figure: true
    figure_anchor: "ch13-fig02-pod-failure-signature-map"
    checkpoint_after: false

  - name: "Looking Inside"
    objectives: ["D2.3"]
    requires_figure: true
    figure_anchor: "ch13-fig03-phase-before-logs-flow"
    checkpoint_after: true

  - name: "Pods That Start and Then Don't Stay"
    objectives: ["D2.3"]
    requires_figure: true
    figure_anchor: "ch13-fig05-oomkilled-vs-evicted"
    checkpoint_after: false

  - name: "When the Node Is the Problem"
    objectives: ["D2.3"]
    requires_figure: true
    figure_anchor: "ch13-fig06-diagnostic-layer-stack"
    checkpoint_after: true

  - name: "Versions That Don't Agree"
    objectives: ["D2.3"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false

  - name: "Numbers Nobody Collects by Default"
    objectives: ["D2.3"]
    requires_figure: true
    figure_anchor: "ch13-fig04-metrics-pipeline-and-metrics-server"
    checkpoint_after: true

  - name: "Read the Phase First"
    objectives: ["D2.3"]
    requires_figure: true
    figure_anchor: "ch13-zenith-read-the-phase-first"
    checkpoint_after: false

#-- Skill Part 11: Soundings pre-chapter diagnostic ----------------------
soundings_planned:
  question_count: 8
  topics:
    - "Pod phase versus container state — which taxonomy a Reason string belongs to (Ch 5 §5)"
    - "Why a Pod sits in Pending, as a scheduling outcome rather than an error (Ch 7 §2, §4)"
    - "imagePullPolicy defaults and the :latest interaction (Ch 2 §6)"
    - "Deriving a QoS class from a Pod's requests and limits (Ch 5 §8)"
    - "What a node condition of Ready=False actually reports (Ch 8 §4)"
    - "The version-skew support window — a deliberate decay probe (Ch 8 §6)"
    - "Getting logs out of a Pod that holds more than one container (Ch 5 §2)"
    - "What happens to an object whose controller is not installed (Ch 10 §3, by name)"

#-- Skill Part 8: practice-question budget ------------------------------
#-- B4 allocated 8 / 10 / 15 = 33. Bearings raised to 16 across three
#-- checkpoints (6+5+5), the Ch 12 precedent for raising B4's Bearings
#-- figure. Reason: 16 is the smallest count that lets retrieval land at
#-- EXACTLY the 25% ceiling (4 of 16) across three checkpoints of >= 5.
#-- At B4's 10, a 25% target rounds to 2.5 and the ceiling cannot be hit
#-- cleanly. Practice stays at B4's 15. New total 39.
question_budget:
  soundings: 8
  taking_your_bearings: 16             # across 3 checkpoints (6 + 5 + 5)
  practice_questions: 15
  total_this_chapter: 39

#-- Concept / objective / command tagging -------------------------------
kb_tags:
  objectives: ["D2.3"]
  concepts:
    - "platform-scope-vs-application-scope"
    - "triage-flow"
    - "pod-failure-signature-map"
    - "pending-diagnosis"
    - "imagepullbackoff-diagnosis"
    - "errimagepull"
    - "createcontainerconfigerror"
    - "imageinspecterror"
    - "admission-rejection-versus-pod-failure"
    - "kubernetes-events"
    - "event-retention-window"
    - "crashloopbackoff"
    - "restart-backoff-curve"
    - "oomkilled-signature"
    - "evicted"
    - "node-pressure-eviction"
    - "eviction-order-by-qos-class"
    - "probe-failure-signatures"
    - "node-conditions-as-diagnostic"
    - "kubelet-health"
    - "node-lease-heartbeat"
    - "node-death-handling"
    - "crictl"
    - "version-skew-symptoms"
    - "release-known-issues"
    - "resource-metrics-pipeline"
    - "metrics-server"
    - "kubectl-top"
    - "cluster-log-architecture"
  commands:
    - "kubectl-describe"
    - "kubectl-events"
    - "kubectl-get-events"
    - "kubectl-logs"
    - "kubectl-logs-previous"
    - "kubectl-get-pod-o-wide"
    - "kubectl-top"
    - "crictl-ps"
    - "crictl-pods"
    - "crictl-logs"
    - "crictl-inspect"

figures_planned:
  - "ch13-fig01-two-audience-split"
  - "ch13-fig02-pod-failure-signature-map"
  - "ch13-fig03-phase-before-logs-flow"
  - "ch13-fig05-oomkilled-vs-evicted"
  - "ch13-fig06-diagnostic-layer-stack"
  - "ch13-fig04-metrics-pipeline-and-metrics-server"
  - "ch13-zenith-read-the-phase-first"
---
```

# Chapter 13 Outline — When the Cluster Won't Answer

## Chapter-type note (read first)

`content`. Full structural contract applies: witty subtitle, Attention Budget, epigraph, 🧭 Soundings, Why This Chapter Matters, What You'll Learn, ≥2 ☆ Taking Your Bearings, Exam Alert, Practice Questions, Chapter Summary, The Voyage Ahead.

**Heading form:** `## <difficulty> §N — Title`, the Ch 5–8 majority form that B6 recommends for Ch 9–19 and that shipped Ch 9–12 use. **Closing section takes `☀️` in place of a difficulty glyph**, per B6 recommendation #4.

---

## 1. Why This Chapter Matters

Every chapter before this one described a system working. This one is about the twenty minutes after it stops, and it is the first chapter where the reader is asked to *use* what they know rather than accumulate more of it.

The curiosity gap is the chapter's own thesis, withheld. Open on the reader's actual instinct — a Pod is broken, so read its logs — and show that instinct failing. A Pod stuck in `Pending` has no logs, because it has no container. A Pod in `CrashLoopBackOff` has logs, but they are the *current* container's, which has not started yet, so `kubectl logs` returns nothing and the reader concludes the application is silent when in fact it has already died five times. A Pod that was `Evicted` is gone from the node entirely. In three of the most common failure shapes on the exam, the first thing everyone reaches for is the wrong thing. The question the chapter withholds and then answers is: *what do you read first, and why is it always the same thing?*

The identity frame is the one shipped Ch 7 already set up at line 426 — going and asking. Practitioners do not recognize error strings; they narrow. The phase tells you which stage of the platform's own sequence stopped, and the stage tells you which component to interrogate. That is not a lookup table, it is a method, and it is transferable to failures that have no name yet. Frame the reader as someone who is about to stop guessing.

The stakes are honest and worth stating plainly: B1 records this as the book's highest-risk single gap — the named Pod failure signatures are the most likely troubleshooting question material on the exam, and they are the material most study guides reduce to a glossary. This chapter refuses to.

**Voice guardrail.** Do not moralize about production incidents, and keep the wry beats oriented at the practitioner's own experience (staring at empty log output; discovering the events expired) rather than at anyone harmed by an outage. Skill Part 14, subject dignity.

---

## 2. What You'll Learn

- **Separate** a platform-scope failure from an application-scope one before spending time on either
- **Read** a Pod's phase and container-state `Reason` as the first two coordinates of a diagnosis, not as error messages
- **Distinguish** the failure signatures that mean *never started* from those that mean *started and did not stay*
- **Run** `kubectl describe`, `kubectl events`, and `kubectl logs --previous` in the order that actually narrows the problem
- **Recognize** when the node, rather than the workload, is the thing that is broken — and when to drop below the Kubernetes API to `crictl`
- **Explain** why `kubectl top` returns an error on a cluster nobody has finished building

*You'll also stop reading logs first, which is the single habit that separates a practitioner from someone who has read about Kubernetes.*

---

## 3. Soundings plan — 8 questions

Content chapter, so 8. Every question is answerable from Chapters 1–12 or from general professional knowledge. This chapter's Soundings does more work than most: two questions (Q5, Q6) are deliberate **decay probes** whose repair is a named section, so the reader's own wrong answer becomes the motivation for §5 and §6.

| # | Topic | Tests | Why it earns its place as a pre-test |
|---|---|---|---|
| 1 | Given a container-state `Reason` string, say whether `Reason` belongs to the Pod phase or the container state | Ch 5 §5 taxonomy | The chapter is a lookup keyed on phase. If this is gone, §1's method cannot land, and the 0–2 rubric needs to say so by section. |
| 2 | A Pod has sat in `Pending` for ten minutes. Is a component retrying it? | Ch 7 §2, §4 | Ch 7's shipped ⚠ said `Pending` is a state, not an error, and no timer converts it. **Primary Ch 7 decay probe.** Surfaces the "something will fix it eventually" misconception before §2 corrects it. |
| 3 | Effect of `imagePullPolicy` and the `:latest` interaction on when a pull happens | Ch 2 §6 | §2's pull-failure family is unreadable without it. Tests priors, not the diagnosis. |
| 4 | Derive the QoS class of a Pod from its requests and limits | Ch 5 §8 | Required for §4. **Deliberately does NOT ask about eviction order** — that is chapter material. Derivation only. |
| 5 | What `Ready=False` on a node reports, and who publishes it | Ch 8 §4 | **Ch 8 decay probe (conditions half).** §5 retrieves the conditions as a diagnostic and must not restate Ch 8's table — this measures whether that is safe. |
| 6 | The supported version-skew window between control plane and kubelet | Ch 8 §6 | **Ch 8 decay probe (skew half), and the chapter's most valuable question.** Ch 8 line 923 explicitly promised the reader this material returns "in a form where you have to use it rather than recite it." A wrong answer here IS the argument for §6. |
| 7 | How you ask for the logs of one container in a three-container Pod | Ch 5 §2 | Ch 5 line 392 handed this to §3 by name. Constrain the stem to `-c`; it must not touch `--previous`, which is §3's to teach. |
| 8 | An Ingress object is created on a cluster with no Ingress controller. What happens? | Ch 10 §3, by name | The strongest of the eight. It pre-tests the *transfer* §7 depends on, using the pattern the reader already owns, without mentioning metrics or `top`. |

### FIXED-POINT SPOILER CHECK

The chapter's candidate Fixed Points, and the confirmation that no Soundings question states one:

| Candidate ★ Fixed Point | Spoiled by any Soundings question? |
|---|---|
| Read the phase before the logs | **No.** Q1 tests the taxonomy's *existence*, never the reading order. |
| `CrashLoopBackOff` means the container started and exited — the image was fine | **No.** The string appears in no stem. |
| `OOMKilled` is the limit; `Evicted` is the node. Different killer, different scope | **No.** Q4 derives a QoS class and stops there. |
| `kubectl top` requires metrics-server, which a stock cluster does not have | **No.** Q8 uses an Ingress controller, deliberately. |
| Events expire; the absence of an event is not evidence | **No.** Events appear in no stem. |

Clean. The subtitle states Fixed Point #1 on the chapter's second line — that is the subtitle's job and is not a licence to relax the above.

**Rubric branches (all three mandatory):** 6+ → skim, but read §6 and §7 properly, since those two are where prior chapters left debts. 3–5 → normal pace. 0–2 → **re-read Ch 5 §5 before starting**, not alongside; name the section, not the chapter.

---

## 4. Section plan

### `## ⚪ §1 — Whose Problem Is This, and What to Read First`

Owns the **two-audience split** (platform scope vs application scope) and the **ordered triage flow**: scope → phase → conditions → events → logs. Must argue *why* the phase precedes the logs rather than asserting it — the three-way demonstration from Why-This-Chapter-Matters (no container, wrong container, no Pod) is the argument, and it is the chapter's opening move that Ch 7 line 426 promised. Opens the two-chapter arc; states the boundary in one paragraph and points at Ch 16 §1 for the far side.

- **Objectives:** D2.3 (Two audiences; Pod phase as first signal)
- **Introduces:** platform-scope-vs-application-scope; triage-flow
- **Figure:** `ch13-fig01-two-audience-split`
- **Cross-bearings out:** `Ch 16 §1 — when the Pod is fine and the application isn't`; `Ch 5 §5 — Pod phase and container state`
- **Guardrail:** name `kubectl debug`, `exec` and `port-forward` as *the other chapter's* tools in one clause with a pointer to Ch 16 §3 and §5. B1 lists them under D2.3, so a reader studying to the blueprint must not think the book skipped them. Do not teach them here.
- **Checkpoint:** none

### `## 🔵 §2 — Pods That Never Start`

The book's highest-risk section (B1 gap G2). Owns the **never-started signature family**: `Pending`; `ErrImagePull` → `ImagePullBackOff`; `CreateContainerConfigError`; `ImageInspectError` / `ErrImageNeverPull`; init-container failure from the platform side. Three shipped chapters point here with three *different* never-started causes, and all three must be discharged: a PVC that never binds (Ch 11:588), a referenced Secret that does not exist (Ch 12:1099), and a Pod the admission gate refused outright (Ch 12:1340). The last of those is not a Pod failure at all — there is no Pod object — and Ch 12 already told the reader it "shows up at a different point in the triage flow," so §2 must say where.

- **Objectives:** D2.3 (Troubleshooting Applications — determining Pod failure reasons; Container Waiting `Reason`)
- **Introduces:** pending-diagnosis; imagepullbackoff-diagnosis; errimagepull; createcontainerconfigerror; imageinspecterror; admission-rejection-versus-pod-failure
- **Figure:** `ch13-fig02-pod-failure-signature-map`
- **Cross-bearings out:** `Ch 7 §2 — feasible nodes, and why a Pod stays Pending`; `Ch 7 §4 — taints and tolerations`; `Ch 2 §3 — tags and digests`; `Ch 2 §6 — imagePullPolicy and image pull secrets`; `Ch 4 §4 — ConfigMaps and Secrets`; `Ch 5 §3 — init containers`; `Ch 11 §2 — PV and PVC binding`; `Ch 12 §6 — Pod Security Admission`
- **⚑2 guardrail:** the `ImagePullBackOff` **string and its taxonomic slot** are owned by Ch 2 §6 and Ch 5 §5. §2 owns **diagnosis only** and must not re-teach the phase/state taxonomy.
- **Ch 7 decay-fix anchor:** the `Pending` material is the primary repair for Ch 7's decay risk. Retrieve filters *and* taints by name; a shortage of capacity and a taint look identical from outside until you read the events, which is exactly what Ch 7 line 726 promised.
- **Checkpoint:** none

### `## ⚪ §3 — Looking Inside`

Owns the **command surface** and the **Event object**. `kubectl describe`; `kubectl events` and the retention window; `kubectl logs` with `-c`, `--all-containers`, and `--previous`. Argues events as a first-class diagnostic surface rather than a footer on `describe` output. Two shipped promises fall due: reading logs from a multi-container Pod (Ch 5:392), and reading events to find which of the six causes fired a `ProgressDeadlineExceeded` (Ch 6:778) — the second is specific and must be discharged with an actual worked example, not a generality. Also owns the short "troubleshooting kubectl" beat from B1: before trusting any output, confirm which cluster and which context you are talking to.

- **Objectives:** D2.3 (Troubleshooting Clusters — troubleshooting kubectl; Container Waiting `Reason`)
- **Introduces:** kubernetes-events; event-retention-window; `kubectl describe`; `kubectl events`; `kubectl logs --previous`
- **Figure:** `ch13-fig03-phase-before-logs-flow` — **relocated here from §1** (see Required figures)
- **Cross-bearings out:** `Ch 5 §2 — multi-container Pods`; `Ch 8 §1 — kubeconfig and contexts`; `Ch 8 §2 — auditing`; `Ch 6 §4 — rolling updates and progress deadlines`; `Ch 16 §3 — getting inside a container`
- **Ledger note:** `Event` is glossed with a pointer at Ch 8 §2 and **defined here**. Auditing stays at Ch 8 §2 — refer, do not restate.
- **Checkpoint:** ☆ TYB 1

### `## 🔵 §4 — Pods That Start and Then Don't Stay`

Owns the **started-then-gone family**: `CrashLoopBackOff` and its backoff curve; `OOMKilled` as a signature; `Evicted` and node-pressure eviction; **eviction order by QoS class**; and the **probe failure signatures** from B1 — liveness failure produces a restart loop, readiness failure produces a Pod that is `Running` and `0/1 Ready` and has been silently dropped from its Service's endpoints. The last is the chapter's quietest failure and the one a reader will otherwise misread as an application bug.

- **Objectives:** D2.3 (determining Pod failure reasons; Probe failure signatures)
- **Introduces:** crashloopbackoff; restart-backoff-curve; oomkilled-signature; evicted; node-pressure-eviction; eviction-order-by-qos-class; probe-failure-signatures
- **Figure:** `ch13-fig05-oomkilled-vs-evicted`
- **Cross-bearings out:** `Ch 5 §4 — restartPolicy and restart backoff`; `Ch 5 §7 — liveness, readiness, and startup probes`; `Ch 5 §8 — requests, limits, and QoS classes`; `Ch 9 §4 — readiness and Service endpoint membership`; `Ch 16 §4 — is anything even selected`
- **Ledger notes:** the `OOMKilled` **mechanism** is Ch 5 §8 and already defers here for the diagnosis — §4 owns the signature, not the mechanism. **Expand OOM (Out Of Memory) on first use**; the acronym register assigns it to this section and it has never been spelled out in the book.
- **⚑3 guardrail — hard.** **PodDisruptionBudget is currently unowned** and barred from graded material book-wide. §4 must not reach for it when explaining `Evicted`, and must not use it in any Practice or Bearings item. See Open Question 2.
- **Checkpoint:** none

### `## 🟡 §5 — When the Node Is the Problem`

Owns node-level diagnosis: reading **node conditions as a diagnostic**, kubelet health, **node lease heartbeats**, **node death handling** (Pods on a dead node marked for deletion after a timeout, replacements created by higher-level controllers), and **`crictl`** — what it is, the two or three commands worth knowing, and above all *why a node-level tool exists below the Kubernetes API at all*. Ch 3 line 451 pinned that framing here by name.

- **Objectives:** D2.3 (Troubleshooting Clusters — node health, crictl; Node lease heartbeats; Node death handling)
- **Introduces:** node-conditions-as-diagnostic; kubelet-health; node-lease-heartbeat; node-death-handling; crictl
- **Figure:** `ch13-fig06-diagnostic-layer-stack`
- **Cross-bearings out:** `Ch 8 §4 — node conditions, cordon and drain`; `Ch 3 §3 — the kubelet`; `Ch 2 §4 — the Container Runtime Interface`; `Ch 8 §7 — etcd backup`
- **⚑1 guardrail:** node conditions are **defined at Ch 8 §4**. §5 retrieves them as a diagnostic and **must not restate the conditions table**. The new material here is what a given condition tells you to do next.
- **Depth ruling:** associate tier. Name `crictl`, show `crictl ps` and `crictl logs`, explain the layer argument. Do not teach its surface. See Open Question 5.
- **Checkpoint:** ☆ TYB 2

### `## 🟡 §6 — Versions That Don't Agree`

Owns **version skew as a cause of failures that are otherwise misdiagnosed** — the symptom shapes of a skewed kubelet and of a skewed client — and **release-specific known-issue lists** as a legitimate step in the triage path. Ch 8 line 923 promised the reader this material would return "in a form where you have to use it rather than recite it," so §6 must be built as applied diagnosis: here is a symptom, here is why skew explains it, here is how you would have ruled it out.

- **Objectives:** D2.3 (Known issues)
- **Introduces:** version-skew-symptoms; release-known-issues
- **Figure:** none, deliberately — a figure here would tempt a restatement of Ch 8 §6's table
- **Cross-bearings out:** `Ch 8 §6 — the version-skew window and the three-minor rule`; `Ch 17 §8 — SIG Release and the release cadence`
- **Guardrail:** **primary decay-fix anchor for Ch 8 §6.** Retrieve the rule; do not restate the table. If the drafting stage finds itself reprinting skew numbers, it has taken the wrong turn.
- **Checkpoint:** none

### `## 🔵 §7 — Numbers Nobody Collects by Default`

**Definition home for metrics-server**, `kubectl top`, and the **resource metrics pipeline**. Owns the argument that a stock cluster collects no usage numbers at all, retrieved *by name* as the pattern Ch 10 §3 established — "the object exists; nothing happens without the component." Also owns **cluster log architecture** at platform scope: where container logs actually live on the node, why `kubectl logs` is not archival, and a **one-clause gloss** of node-level logging agents pointing at Ch 18 §6.

- **Objectives:** D2.3 (Resource metrics pipeline; Logging architecture; monitoring tools)
- **Introduces:** resource-metrics-pipeline; metrics-server; `kubectl top`; cluster-log-architecture
- **Figure:** `ch13-fig04-metrics-pipeline-and-metrics-server`
- **Cross-bearings out:** `Ch 10 §3 — the object exists; nothing happens without the component`; `Ch 3 §4 — addons, and what else is optional`; `Ch 6 §2 — the HPA in one sentence`; `Ch 6 §7 — DaemonSets`; `Ch 17 §7 — the autoscaling landscape`; `Ch 18 §3 — metrics-server versus a monitoring system`; `Ch 18 §6 — node-level logging agents`
- **Ledger guardrails:** node-level logging agent is **owned by Ch 18 §6** — one clause plus a pointer, nothing more. metrics-server is owned **here**, and Ch 17 §7 and Ch 18 §3 both refer back, so the definition must be complete enough to be referred to rather than re-derived.
- **Debts discharged:** Ch 3:605 (`kubectl top` with no metrics-server), Ch 6:426 (metrics-server is what an HPA reads), Ch 10:677 (the pinned pointer).
- **Checkpoint:** ☆ TYB 3

### `## ☀️ §8 — Read the Phase First`

Zenith. The recognition is that the chapter was never a list of nine error strings: it was **one lookup with one key**, and the key is the phase. The phase says which stage of the platform's sequence stopped; the stage says which component to ask; and — the turn that closes §1 — the phase also answers *whose problem this is*, which is why the question §1 opened with and the answer §8 arrives at are the same question. Closes by handing the reader to Ch 16 §1 explicitly.

- **Figure:** `ch13-zenith-read-the-phase-first`
- **Cross-bearings out:** `Ch 16 §1 — when the Pod is fine and the application isn't`; `Ch 3 §6 — the control loop`
- **⛑ CONVENTION guardrail — read before drafting.** §8 may observe in a clause that a Pod stuck in `Pending` is a loop that has not converged, and may back-bear to Ch 3 §6. It **must not** assert a running ordinal — no "the sixth control loop," no "the third time you've seen this." Shipped Ch 6 already promised the reader that "the third time is the one that matters," and that payoff is reserved for **Ch 15 §7, the book's primary Zenith**. State the pattern, never the count. This chapter's Zenith is its own — diagnosis as a lookup keyed on the phase — and it does not need to borrow Ch 15's.

---

## 5. ☆ Taking Your Bearings checkpoints

Three checkpoints, 16 questions, **4 retrieval questions = exactly 25.0%**, the arc outline's ceiling.

**Retrieval is defined narrowly here**, and the drafting stage must hold the line: a retrieval question is one whose *answer* lives in an earlier chapter. A question about diagnosing `ImagePullBackOff` that merely leans on `imagePullPolicy` is a **chapter** question, not a retrieval question — otherwise this chapter would score 90% retrieval and the number would mean nothing.

| # | Falls after | Topic | Qs | Retrieval | Drawn from |
|---|---|---|---|---|---|
| TYB 1 | §3 | Pods that never start, and the commands that tell you why | 6 | 1 | Ch 2 §3 — tag versus digest as image identity |
| TYB 2 | §5 | Started, then gone — and the node beneath | 5 | 1 | Ch 5 §8 — deriving a QoS class |
| TYB 3 | §7 | Skew, metrics, and what isn't there | 5 | 2 | Ch 8 §6 — the skew window; Ch 10 §3 — the named component pattern |

**TYB 3 runs 40% retrieval locally, and that is deliberate**, not drift: §6 and §7 are the book's designated decay-fix anchors for Ch 8 and Ch 10, and the checkpoint that follows them is where the repair gets verified. The chapter average is at the ceiling, which is the number that governs.

Every checkpoint carries trap answers targeting the misconceptions in the Exam Alert below, why-wrong explanations for all options, and a revision prompt naming a **section** for 0–2 scorers.

---

## 6. Exam Alert plan

**High-priority topics.** These are the four the exam can reach most directly:

1. **The never-started / started-then-died split**, and which signature belongs to which. This is the chapter in one line.
2. **`CrashLoopBackOff` means the container ran.** The image pulled, the config resolved, the process started — and exited. It is a restart-throttling state, not a start failure.
3. **`OOMKilled` versus `Evicted`.** Different killer (kernel cgroup enforcement vs the kubelet), different scope (one container vs the whole Pod), different trigger (this Pod's limit vs the node's pressure), different outcome (restart in place vs reschedule elsewhere).
4. **`kubectl top` requires metrics-server**, and no cluster ships one by default.

**Common traps** — ⚠ Navigational Hazards, loss-aversion framing:

| Trap | The correct understanding |
|---|---|
| Reading `CrashLoopBackOff` as an image problem | It is the opposite signal. The image was fine; that is what "Loop" implies. |
| `kubectl logs` on a crash-looping Pod returns nothing, so the app is silent | You are reading a container that has not started. `--previous` reads the one that died. |
| Treating the absence of an event as evidence | Events expire. An empty event list on a Pod that failed an hour ago means nothing. |
| Assuming a *request* protects a container from being killed | The **limit** is what gets you OOM-killed. The **QoS class** — which requests help determine — is what orders eviction. Two different mechanisms. |
| "BestEffort is the safest because it asks for nothing" | BestEffort is evicted first. |
| `Pending` means something is retrying with looser constraints | Nothing is. `Pending` is a stable, honest report. Go and ask. |
| Diagnosing an omitted `-c` as an application failure on a multi-container Pod | Confirm which container you are reading before concluding anything. |
| Expecting `kubectl` to see a container the kubelet never registered | That is precisely the case `crictl` exists for. |
| Assuming a Pod that "won't start" always exists as an object | An admission gate refusal means there is no Pod at all. Different triage step — Ch 12:1340 already flagged this to the reader. |

---

## 7. Practice Questions plan

**Target: 15**, per `question_budget.practice_questions` and B4. Weighted toward the two signature families, since B1 records those as the single highest-risk gap in the book.

| Section | Items | Rationale |
|---|---|---|
| §1 triage method | 1 | Method, not recall; better tested by scenario stems elsewhere |
| §2 never started | 5 | G2, three inbound pointers, the largest signature family |
| §3 commands and events | 2 | Includes the `--previous` trap |
| §4 started then gone | 4 | `OOMKilled`/`Evicted` is the chapter's top confusion pair |
| §5 node-level | 1 | Associate-tier depth; one is proportionate |
| §6 skew and known issues | 1 | Applied, not recall |
| §7 metrics and logs | 1 | The pattern transfer, not the component list |

**Interleaving strategy.** At least four stems present a *symptom* and require the reader to choose the diagnostic step rather than name the string — the shape the exam favors and the shape a glossary cannot answer. Three stems cross domains deliberately: one pairs a Pending Pod with a taint (D1.3 scheduling), one pairs a never-started Pod with a missing Secret (D2.2 security), one pairs a stalled rollout with its events (D1.1 workloads). Per skill Part 10, wrong options are built to catch the specific misconceptions tabulated in the Exam Alert, and every option gets a why-wrong explanation.

**Barred from all graded text in this chapter:** PodDisruptionBudget (unowned, ⚑3), ABAC, SRE, descheduler, eBPF (glossary-only with graded-use restrictions), and any question hinging on the absence of a Kubernetes LTS (see Open Question 3).

---

## 8. Required figures

Seven anchors: six concept diagrams plus one Zenith, inside skill Part 18.10's 2–8 band.

| Anchor | § | Type | Purpose and content |
|---|---|---|---|
| `ch13-fig01-two-audience-split` | §1 | Comparative | Two columns — platform scope and application scope — listing what each owns, with a single labeled handoff arrow to Ch 16. Establishes the chapter's boundary visually before any prose argues it. ≤7 labels. |
| `ch13-fig02-pod-failure-signature-map` | §2 | Decision tree | **Scope narrowed from the arc stub to the never-started branch only.** Root: the Pod's phase. Four to five leaves — Pending / ErrImagePull→ImagePullBackOff / CreateContainerConfigError / no Pod object at all — each labeled with what to read next. Narrowed because a tree covering all nine signatures runs ~10 labels and breaches Part 18.12's over-labeling limit; §4 gets its own figure instead. |
| `ch13-fig03-phase-before-logs-flow` | §3 | Process flow | The triage order rendered as a flow with the *command* at each step: scope → phase → conditions → events → logs. **Relocated from §1 to §3** — §1 owns the order as an argument, but the figure's payload is commands, and spatial contiguity puts it where the commands are taught. |
| `ch13-fig05-oomkilled-vs-evicted` | §4 | Comparative | Two kill paths side by side: container exceeds its limit → kernel OOM kill → `Terminated`/`OOMKilled` → restarted in place; versus node under pressure → kubelet evicts by QoS order → Pod `Failed`/`Evicted` → rescheduled elsewhere. The chapter's top confusion pair, and Part 18.9's clearest case for a comparative figure. **New — not in the arc stub list.** |
| `ch13-fig06-diagnostic-layer-stack` | §5 | Stack | kubectl → API server → kubelet → CRI → containerd, with `crictl` attaching *below* the API line. Makes the "why a node-level tool exists" argument visually in a way prose labors at. **Stack family, so it carries Lucide glyphs** per style-decisions 2026-08-25. **New.** |
| `ch13-fig04-metrics-pipeline-and-metrics-server` | §7 | Pipeline | kubelet/cAdvisor → metrics-server → `metrics.k8s.io` → `kubectl top` and the HPA, with the metrics-server box drawn as *absent by default*. **Pipeline family, so glyphs.** |
| `ch13-zenith-read-the-phase-first` | §8 | Dramatic synthesis | The chapter's nine signatures collapsed onto one axis keyed by phase — the visual claim that this was one lookup, not nine facts. Exactly one Zenith per content chapter, per Part 18.10. |

**Numbering note, so no downstream stage reads it as an error.** `ch13-fig04` is deliberately out of document order. The arc outline records that this specific anchor is retrieved twice by name — Ch 17 §7 (metrics-server as autoscaler input) and Ch 18 §3 (metrics pipeline versus monitoring) — so its ID is preserved exactly as stubbed rather than renumbered to §7's position. Anchor IDs are identifiers, not an ordering contract; the structural contract's `anchor_id_pattern` imposes no sequence. Two arc stubs changed: `ch13-fig02` is narrowed in scope, and `ch13-fig03` moves from §1 to §3. Two are new: `ch13-fig05` and `ch13-fig06`.

---

## 9. Open questions for the author

**1. Blocking research — Stage 2 must fetch these before drafting.** B1 flags G1 and G2 as blocking for this chapter, and G2 is the highest-risk single gap in the book. Not one Pod failure signature appears in the cached 168-file corpus, and this chapter is built on them. Required snapshots:

- `kubernetes.io/docs/tasks/debug/debug-application/debug-pods/` — **G2, the critical one**
- `kubernetes.io/docs/reference/kubectl/` and the kubectl cheat sheet — **G1**
- `kubernetes.io/docs/tasks/debug/debug-cluster/` and `.../debug-cluster/crictl/`
- `kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/`
- `kubernetes.io/docs/concepts/cluster-administration/logging/`
- `kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/`
- `kubernetes.io/docs/concepts/architecture/nodes/` — conditions, leases, node-death timeout

**2. ⚑3 PodDisruptionBudget — author decision required.** PDB is unowned book-wide; B6 assigned it to Ch 8 §4 but shipped Ch 8 contains zero occurrences of the term. §4 here would benefit from one clause on why a drain stalls, and it is the natural place a reader asks. Options: (a) retrofit one clause into Ch 8 §4 and let §4 refer to it, or (b) leave it out entirely. Until (a) happens, this outline treats PDB as barred from §4 and from all graded text.

**3. LTS hazard — author decision.** §6 is exactly where a reader arriving from a distribution with long-term support will ask "is there a Kubernetes LTS?" The answer (there is none; support is three minor versions) belongs to Ch 8 §6 per the term ledger, and shipped Ch 8 §6 does not say it. Either retrofit it there as a ⚠ Navigational Hazards line and let §6 retrieve it, or accept that §6 cannot raise the question and no item may hinge on it.

**4. Two facts that must not be written from memory.** The **event retention default** (`kube-apiserver --event-ttl`) and the **CrashLoopBackOff backoff schedule and its reset behavior** have both changed across recent releases. Both must carry a `[source:]` tag against a dated snapshot. If the snapshot does not pin a number, write the shape ("on the order of an hour", "doubling to a cap of a few minutes") rather than a figure. The same applies to the node-death eviction timeout, which moved from `--pod-eviction-timeout` to taint-based eviction with a `tolerationSeconds` default.

**5. `crictl` depth.** Recommendation: name it, show `crictl ps` and `crictl logs`, and spend the words on *why* a tool below the API exists rather than on its surface. Ch 3 line 451 pinned the framing, not the command set, and this is an associate exam. Confirm.

**6. `journalctl -u kubelet` in §5.** Reading the kubelet's own service logs is Linux-host territory rather than Kubernetes, but it is the honest next step when the kubelet is the suspect. Recommendation: one mention, clearly marked as leaving the Kubernetes API behind. Confirm.

**7. Acronym-register additions.** **OOM** is expanded for the first time in the book at §4 (the register already assigns it here). **TTL** has no register row and will appear if §3 names `--event-ttl`. Add TTL to the register, or avoid the flag name and describe the behavior. Recorded for the glossary build alongside the existing Ch 9/10/11 debts.

**8. Epigraph.** The chapter's material invites a diagnosis-before-treatment quote. Preference order per skill Part 15: a real practitioner or engineering figure over a Lodestar original. Flagging only because the epigraph is `expected` in the structural contract and this chapter's register — calm, methodical, faintly weary — narrows the field.
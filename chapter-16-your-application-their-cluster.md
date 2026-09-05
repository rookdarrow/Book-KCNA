---
chapter: 16
chapter_type: "content"
title: "Your Application, Their Cluster"
subtitle: "Four questions that separate your bug from theirs"
exam_domain: "Cloud Native Application Delivery (competency: Debugging)"
domain_weight_pct: 4
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE NOTE — CHANGED FROM THE ARC OUTLINE. See Open Question 1.
#-- B2 and B3 both carry *"Four questions that separate 'my code is
#-- broken' from 'the platform is broken'"* — thirteen words, against this
#-- stage's own <= 10 constraint, and the only subtitle in the book that
#-- breaches it. The form above is eight words, keeps the four questions,
#-- keeps the scope split, and reads correctly against the title ("theirs"
#-- = the cluster's, i.e. the platform's). No shipped chapter quotes the
#-- long form; grep of chapters 01-15 returns nothing. Author's call,
#-- flagged rather than taken silently.
#--
#-- The subtitle names the chapter's STRUCTURE (four questions) rather
#-- than a Fixed Point, which is the opposite of Ch 13's subtitle and is
#-- correct here — this chapter's Fixed Points are about tools, and a
#-- subtitle naming one would spoil §3.

#-- EXAM_DOMAIN NOTE — TWO OBJECTIVES, DELIBERATELY.
#-- Shipped chapter-13 line 392 left this stage an explicit instruction:
#--
#--   "kubectl exec, kubectl debug / ephemeral containers, kubectl
#--    port-forward, and Service/EndpointSlice debugging are all on the
#--    authored D2.3 Troubleshooting list and are all deferred to Ch 16 ...
#--    Unless Ch 16's frontmatter carries objectives: ["D3.2", "D2.3"],
#--    the book's objective index will show a substantial slice of D2.3
#--    with no owning chapter."
#--
#-- Discharged: kb_tags.objectives below carries both. `exam_domain`
#-- stays single-valued and names D3.2, because that is the domain whose
#-- WEIGHT this chapter draws against (Part IV, D3, 16%) and the house
#-- string form shipped by ch-04/-09/-10/-11/-12/-13 is one domain. The
#-- in-chapter metadata line must carry the published **16%** for D3 with
#-- its source tag and the authored-allocation disclaimer.
#--
#-- The 4% figure is this chapter's AUTHORED allocation, not CNCF data.
#-- CNCF publishes four domain weights (44/28/16/12) and no
#-- sub-competency weights — B1 gap G33, B2 disclosure #1. Do NOT present
#-- 4% as published.

#-- PREREQ NOTE — heavy, and heavy in the same shape as Ch 13: this
#-- chapter is mostly APPLIED prior material, at the arc outline's 25%
#-- retrieval CEILING. Five mandatory anchors, all named by B3:
#--   Ch 13 §1/§8 (the handoff)        -> §1   ** the opening move **
#--   Ch 5 §3 (the init sequence)      -> §2
#--   Ch 5 §5/§7 (phase, probes)       -> §1, §4
#--   Ch 9 §3/§4/§7 (Service -> slice -> Pod, DNS) -> §4
#--   Ch 6 §6 + Ch 11 §6 (StatefulSet identity + PVC) -> §6
#-- Ch 13 §1 is not optional. This chapter's first sentence is the far
#-- side of a handoff the reader was given three chapters ago; a reader
#-- who has lost the scope test cannot receive §1, and §1 is what makes
#-- the other seven sections a method rather than a tool list.
#--
#-- Consequence for drafting: the Soundings 0-2 branch names Ch 13 §1 as
#-- the one section to re-read BEFORE starting, not alongside.
#-- Ch 11/Ch 12/Ch 13 precedent.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "focused" — 4
#-- points, high retrieval load. Planning signal only, NOT a target.
#--
#-- ⚠ SECTION NUMBERING IS LOAD-BEARING. Eleven published cross-bearings
#-- point at this chapter. NINE name a section by number, covering FIVE of
#-- the eight sections:
#--   chapter-05:676  -> Ch 16 §1   when the Pod is fine and the app isn't
#--   chapter-13:388  -> Ch 16 §1   (same wording)
#--   chapter-13:1828 -> Ch 16 §1   (same wording, the Voyage Ahead)
#--   chapter-05:448  -> Ch 16 §2   debugging init containers
#--   chapter-13:566  -> Ch 16 §2   debugging init containers
#--   chapter-12:1342 -> Ch 16 §3   getting inside, and adding what isn't there
#--   chapter-13:390  -> Ch 16 §3   getting inside a container
#--   chapter-09:766  -> Ch 16 §4   a Service whose endpoint list is empty
#--   chapter-13:972  -> Ch 16 §4   is anything even selected
#--   chapter-13:390  -> Ch 16 §5   bypassing the Service on purpose
#-- Two more are unnumbered and pin by TOPIC only:
#--   chapter-06:872  -> Ch 16      debugging StatefulSets and their claims
#--   chapter-08:364  -> Ch 16      `exec`, in the kubectl verb table
#-- §1, §2, §3, §4 and §5 are FIXED. §6 is pinned by topic (Ch 6:872) and
#-- takes StatefulSets. §7 and §8 are free; §8 is structurally fixed as the
#-- Zenith and as the far end of the Ch 13 §8 arc.
#-- All ten numbered pins match the B6 skeleton exactly.
#-- Verified 2026-08-31 against chapters 01-15.
sections:
  - name: "Handed Back"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig01-application-scope-triage"
    checkpoint_after: false

  - name: "When It Never Got Started"
    objectives: ["D3.2"]
    requires_figure: true
    figure_anchor: "ch16-fig05-init-sequence-debug-points"
    checkpoint_after: false

  - name: "Getting Inside, and Adding What Isn't There"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig02-ephemeral-container-debug"
    checkpoint_after: true

  - name: "Is Anything Even Selected"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig04-service-break-points"
    checkpoint_after: false

  - name: "Bypassing the Service on Purpose"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig03-portforward-vs-service-path"
    checkpoint_after: false

  - name: "When Each Replica Is Its Own"
    objectives: ["D3.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false

  - name: "Before You Ship It"
    objectives: ["D3.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true

  - name: "Mine, or the Platform's"
    objectives: ["D3.2"]
    requires_figure: true
    figure_anchor: "ch16-zenith-mine-or-the-platforms"
    checkpoint_after: false

#-- Skill Part 11: Soundings pre-chapter diagnostic ----------------------
soundings_planned:
  question_count: 8
  topics:
    - "The scope test from Ch 13 §1 — Running, Ready, confined to one workload, still wrong (Ch 13 §1)"
    - "What a failed init container does to the rest of the init sequence (Ch 5 §3)"
    - "Where a Running, 0/1 Ready Pod goes in its Service's endpoint list (Ch 5 §7, Ch 9 §4)"
    - "Which of port and targetPort names the port the container listens on (Ch 9 §3)"
    - "The shape of a Service's in-cluster DNS name (Ch 9 §7)"
    - "What is stable about a StatefulSet Pod when it is rescheduled (Ch 6 §6)"
    - "Whether deleting a StatefulSet replica deletes its PVC — a decay probe (Ch 11 §6)"
    - "What is actually inside a minimal image, and what a shell would require (Ch 2 §2)"

#-- Skill Part 8: practice-question budget ------------------------------
#-- B4 allocated 8 / 10 / 15 = 33. Drafting raised Bearings to 16 (6+5+5);
#-- the 2026-09-03 checkpoint merge left two checkpoints carrying 14 (6 + 8). Four of the 14 are retrieval-tagged (28.6%, above
#-- the arc outline's 25% ceiling; recorded at the 2026-09-04 audit, not
#-- changed there). Practice runs 17 after revision added Q16 and Q17 (B4
#-- floor is 15). Actual total 8 + 14 + 17 = 39; the question_budget block
#-- below is maintained by the central pass.
question_budget:
  soundings: 8
  taking_your_bearings: 14             # across 2 checkpoints (6 + 8)
  practice_questions: 17
  total_this_chapter: 39

#-- Concept / objective / command tagging -------------------------------
#-- Per the Ch 13 AUTHOR-REVIEW housekeeping note: this list must claim
#-- only what the chapter actually demonstrates. Every command below is
#-- shown in a named section; nothing is listed on the strength of being
#-- adjacent to the topic.
kb_tags:
  objectives: ["D3.2", "D2.3"]
  concepts:
    - "application-scope-triage"
    - "four-triage-questions"
    - "scope-handoff-boundary"
    - "init-container-debugging"
    - "init-container-ordering-and-idempotency"
    - "config-errors-visible-at-init"
    - "distroless-image-debugging"
    - "ephemeral-containers"
    - "debug-profiles"
    - "debug-copy-to"
    - "debug-node"
    - "service-selector-mismatch"
    - "empty-endpointslice-as-symptom"
    - "port-versus-targetport"
    - "readiness-gating-endpoints"
    - "service-dns-name-shape"
    - "port-forward-as-diagnostic"
    - "service-path-versus-api-path"
    - "statefulset-application-debugging"
    - "per-replica-pvc-debugging"
    - "headless-service-dns-names"
    - "local-development-loop"
    - "in-cluster-only-reproduction"
    - "termination-message"
    - "silently-dropped-manifest-field"
  commands:
    - "kubectl-logs-c-init-container"
    - "kubectl-exec"
    - "kubectl-debug"
    - "kubectl-debug-copy-to"
    - "kubectl-debug-node"
    - "kubectl-port-forward"
    - "kubectl-get-endpointslices"
    - "kubectl-describe-service"

figures_planned:
  - "ch16-fig01-application-scope-triage"
  - "ch16-fig05-init-sequence-debug-points"
  - "ch16-fig02-ephemeral-container-debug"
  - "ch16-fig04-service-break-points"
  - "ch16-fig03-portforward-vs-service-path"
  - "ch16-zenith-mine-or-the-platforms"
---

# Chapter 16: Your Application, Their Cluster
## *"Four questions that separate your bug from theirs"*

**Domain Weight: 16% (Cloud Native Application Delivery) [source: cncf-kcna-curriculum-pdf-2026-08-23] | Competency: Debugging | Authored allocation for this chapter: ~4%**
**Complexity: Mixed | Novelty: Moderate | Prerequisites: Heavy**

<!-- AUTHOR-REVIEW: the "~4%" figure is this book's own allocation across the two D3 chapters, not a CNCF-published number. CNCF publishes four domain weights (44/28/16/12) and no sub-competency weights. The metadata line above labels it as authored. THE LABEL MUST SURVIVE — stripped of the qualifier, "~4%" sits beside a genuinely CNCF-sourced 16% and reads as a published number. -->

---

## Attention Budget

**Total time: ~80 minutes | Recommended: Single session, or split after §5**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 Handed Back | 6 min | Low | Anytime |
| §2 When It Never Got Started | 9 min | Medium | Mid-session |
| §3 Getting Inside, and Adding What Isn't There | 17 min | High | Peak attention |
| ☆ Taking Your Bearings (1) | 6 min | Medium | After a brief break |
| §4 Is Anything Even Selected | 12 min | High | Peak attention |
| §5 Bypassing the Service on Purpose | 7 min | Low | Anytime |
| §6 When Each Replica Is Its Own | 7 min | Medium | Mid-session |
| §7 Before You Ship It | 5 min | Low | Anytime |
| ☆ Taking Your Bearings (2) | 8 min | Medium | After a brief break |
| §8 Mine, or the Platform's | 3 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*If you only have 15 minutes: read §1 and §4, then take the second Taking Your Bearings checkpoint.*

---

> *"The first step in troubleshooting is triage. What is the problem? …"*
> — Kubernetes documentation, *Debug Pods* [source: k8s-docs-debug-pods-2026-08-31]

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Every one of them is answerable from Chapters 1–15 or from general professional knowledge; none requires anything this chapter is about to teach you. Your score determines how to approach the content. No shame in any score; different scores just call for different reading strategies.

1. A Pod is `Running`. It reports `1/1 Ready`. Its restart count is zero, its node is healthy, and no other workload in the namespace is affected. The response it returns is still wrong. Whose problem is this — the platform's or the application's?

2. A Pod declares three init containers. The second one exits non-zero. What happens to the third init container, and what happens to the app containers?

3. A Pod is `Running` but reports `0/1 READY`. What has happened to its standing as a target for traffic through its Service?

4. Of `port` and `targetPort` on a Service, which one names the port the container is actually listening on?

5. Write out the in-cluster DNS name a Pod would use to reach a Service named `api` in the namespace `payments`.

6. A StatefulSet Pod is rescheduled onto a different node. Name one thing about it that does not change.

7. You delete the Pod `web-2` from a three-replica StatefulSet. What happens to its PersistentVolumeClaim?

8. An image is built from a minimal base — no package manager, no `/bin/sh`, nothing but the application binary and its libraries. What happens when you run `kubectl exec <pod> -- sh` against it?

<details>
<summary>Answers + reading strategy</summary>

1. **The application's.** The mechanical test from Chapter 13 is: if the Pod is running and ready, and the fault is confined to one workload, the platform has done its job and the problem is yours. *[cross-bearing: see Ch 13 §1 — whose problem is this, and what to read first]*

2. **The second one is retried; the third does not start; the app containers do not start.** Init containers run in order and each must complete successfully before the next begins, and *"if a Pod's init container fails, the kubelet repeatedly restarts that init container until it succeeds"* [source: k8s-docs-init-containers-2026-08-24]. The Pod stays `Pending` with the `Initialized` condition false [source: k8s-docs-init-containers-2026-08-24]. *[cross-bearing: see Ch 5 §3 — everything that must happen first]*

3. **It is still listed behind the Service, but marked as not ready.** Readiness maps onto the endpoint's own condition, and an endpoint that is not serving is not one that should be used as a target for Service traffic [source: k8s-docs-endpointslices-2026-08-24]. Readiness does not delete the endpoint; it disqualifies it. *[cross-bearing: see Ch 9 §4 — the list behind the name]*

4. **`targetPort`.** `port` is the port the Service itself is reachable on; `targetPort` is the port on the Pod that traffic is delivered to. *[cross-bearing: see Ch 9 §3 — four ways to be reachable]*

5. **`api.payments.svc.cluster.local`** — the general form is `<service>.<namespace>.svc.<cluster-domain>` [source: k8s-docs-dns-pod-service-2026-08-23]. A Pod in the `payments` namespace could also just say `api`. *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*

6. **Any of: its hostname, its ordinal, its DNS name, or its PersistentVolumeClaim.** All four are part of the sticky identity a StatefulSet maintains — *"each has a persistent identifier that it maintains across any rescheduling"* [source: k8s-docs-statefulset-2026-08-24]. *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*

7. **Nothing. The PVC survives.** *"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted"*, and *"the default for policies is Retain"* for both the scale-down and the delete case [source: k8s-docs-statefulset-storage-2026-08-25]. *[cross-bearing: see Ch 11 §6 — Pods that are not interchangeable, revisited]*

8. **It fails.** There is no shell in the image to execute. An image contains exactly what was put into it and nothing else. There is no ambient operating system underneath waiting to supply the missing pieces. *[cross-bearing: see Ch 2 §2 — what's inside an image]*

**If you got 6+ right:** Skim, but read §3 and §6 properly. Those two carry material with no analog anywhere earlier in the book, and skimming them will cost you.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Before you start this chapter, go back and re-read **Chapter 13 §1** — not the whole chapter, that one section. This chapter's opening move is receiving a handoff that Chapter 13 §1 made. Without it, everything here reads as a list of commands instead of a method.

</details>

---

## Why This Chapter Matters

Three chapters ago, the platform finished its work and handed you back your own problem.

That is where this chapter starts. Not with an introduction — with the far side of a handoff you were given in Chapter 13 and have been carrying ever since. The Pod is `Running`. It is `1/1 Ready`. The restart count is zero, the node is healthy, the events are quiet, and the thing your users are complaining about is still happening.

Chapter 13 taught you to stop reaching for the logs and read the phase first. The phase, here, has nothing left to say. Every instrument you have trusted for two hundred pages reads fair, and the system is broken anyway.

So what do you actually look at?

The answer is a different set of four questions and a different set of tools, and there is a reason those tools were withheld until now: every one of them requires a running container. `exec` needs a process to enter. An ephemeral container needs a Pod to attach to. `port-forward` needs something listening on the other end. All of them assume the condition Chapter 13 spent its whole length helping you establish.

There is also a shift in who you are while you use them. Chapter 13's reader stood outside somebody else's platform and interrogated it, asking whether the cluster had done its job. This chapter's reader is the person who shipped the thing, working inside a cluster they do not own, with permissions they did not grant themselves, on an image that may not contain a shell. That is the actual posture of an application engineer on Kubernetes, and it is what the chapter title names.

> **Dead Reckoning:** When a Pod is `Running` and `Ready` and the application is still wrong, the platform's own signals keep reporting "fine," because from the platform's point of view everything is. The diagnostic surface you need is inside the container, in the Service that routes to it, and in the configuration the process actually read. The platform inspects none of those on your behalf. The tools for reaching them are `kubectl exec`, `kubectl debug`, `kubectl port-forward`, and `kubectl get endpointslices`. Each answers a different question. Knowing which question you are asking is most of the work.

The stakes are specific. Cloud Native Application Delivery is 16% of the KCNA exam [source: cncf-kcna-curriculum-pdf-2026-08-23], and Debugging is one of its two competencies. That weight doubled when the curriculum changed: the retired five-domain blueprint gave the domain 8% [source: cncf-kcna-curriculum-retired-2026-09-04], and the current four-domain one gives it 16% [source: cncf-kcna-curriculum-pdf-2026-08-23], so study material built against the older shape gives this material half the attention it now earns. The competency is not flag syntax. It is which verb answers which question, and no glossary can teach you that: the verbs are only distinguishable by the question each one is for.

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Take** the handoff from platform scope and state, mechanically, which side of the boundary a failure is on
- **Ask** the four questions that localize an application fault — is it running, is it healthy, is it reachable, is it configured — in the order that clears the most water first
- **Read** a failing init container from the application side, and recognize the ordering and re-run assumptions that break one
- **Get inside** a running container with `exec`, and get inside one with no shell at all using an ephemeral container and `kubectl debug`
- **Diagnose** a Service that exists, selects nothing, and is therefore working exactly as written
- **Prove** where a break is by deliberately bypassing the Service path with `port-forward`
- **Ask** all four questions of a single StatefulSet replica, when the replicas are not interchangeable

*You'll also stop asking "is Kubernetes broken?" as your first question, which is the habit that costs application engineers the most time on somebody else's cluster.*

---

## ⚪ §1 — Handed Back

Here is the sentence Chapter 13 ended on, restated from this side: **the Pod is fine and the application isn't.**

That is not a failure of the platform's diagnostics. It is what a successful platform diagnosis looks like. The kubelet started your container. The scheduler placed it. The probes passed. Nothing crashed. The cluster has taken its own bearings and found nothing out of position. The fault is somewhere the cluster does not look.

The Kubernetes documentation draws the same line at the top of its own application-debugging guide: *"This guide is to help users debug applications that are deployed into Kubernetes and not behaving correctly. This is* not *a guide for people who want to debug their cluster."* [source: k8s-docs-debug-pods-2026-08-31] Two audiences, two sets of tools, one boundary between them.

You already have the mechanical test for which side you are on: scope first, then phase, then conditions, then events, then logs, and a fault that is *not* confined to a single workload is still the platform's *[cross-bearing: see Ch 13 §1 — whose problem is this, and what to read first]*. What is new here is the direction of travel, and one honest addition to the test.

The addition is this: on somebody else's cluster, you will frequently be *unable* to check the platform side yourself. You may not have permission to read node conditions, or to list Pods in `kube-system`, or to see the events on a node you don't own. The boundary is therefore not only a statement about where the fault is. It is also a statement about what you are allowed to see. The practical consequence: make your case for "this is platform-side" from evidence you *can* gather, because the person who can check the other half is going to ask you for it.

None of which makes the platform team an adversary. "Their cluster" in this chapter's title is a statement of scope, not of blame. They own the machinery; you own the workload; the boundary is where those two responsibilities meet, and the entire value of being able to place a fault on the correct side is that neither of you spends an afternoon on the other's half.

### The four questions

Everything after this section is one of four questions, asked in an order chosen to clear the most water first:

**Is it running?** — Not "does the Deployment exist," but did this container's process actually get to the point of executing your code. A Pod that never cleared its init sequence has never run a line of your application.

**Is it healthy — and is it configured the way you think?** — The process is up. Is it doing what you told it, with the values you believe you gave it? These two are one question because the answer to both lives in the same place: inside the running container.

**Is it reachable?** — Something is listening. Can the traffic get to it, through the Service that is supposed to route it?

**Is it configured?** — Which appears twice, deliberately. Read on.

<!-- FIGURE: ch16-fig01-application-scope-triage -->
![A tree diagram. An arrow labeled 'from Chapter 13, platform scope discharged' enters a root box labeled 'Application scope: this book, this chapter, your problem'. From the root, a bracket connects to four question boxes stacked to its right: Running? (section 2), Healthy? Configured? (section 3), Reachable? (sections 4 then 5), and Per-replica? (section 6). A legend identifies the root and the triage questions and reads: top to bottom, each question eliminates ground before the next.](figures/ch16-fig01-application-scope-triage.svg)

<!-- ASCII-FALLBACK
```
        FROM CH 13 — platform scope discharged
                        │
                        ▼
        ┌───────────────────────────────────┐
        │   APPLICATION SCOPE  (this book,  │
        │   this chapter, your problem)     │
        └───────────────┬───────────────────┘
                        │
     ┌──────────┬───────┴───────┬─────────────┐
     ▼          ▼               ▼             ▼
  RUNNING?   HEALTHY?       REACHABLE?    PER-REPLICA?
   (§2)     CONFIGURED?     (§4 → §5)        (§6)
              (§3)
```
-->

The mapping to sections is direct, with one wrinkle:

| Question | Answered in |
|---|---|
| Is it running? | §2 |
| Is it healthy — and is it configured the way you think? | §3 |
| Is it reachable? | §4, then §5 |
| *(all four, for workloads whose replicas are not interchangeable)* | §6 |

**Note the doubling.** "Is it configured" gets answered in two places, because a configuration fault surfaces at two different times. A missing ConfigMap key can stop a Pod before it ever starts, and that shows up at init (§2). A *present* key with the wrong value gets read cleanly by a running process that then does the wrong thing, and that shows up only when you go in and look (§3). Same class of bug, two entirely different signatures, two different sections. Four questions, eight sections: the arithmetic works out because the questions overlap, not because anything is missing.

> ⚓ **Worth Securing:** Ask the questions in order. Each one, answered, deletes a large region of the search area. The temptation is to jump to whichever tool you learned most recently, usually `exec`, and start poking. That is how a fifteen-minute diagnosis becomes an afternoon: you can spend a very long time inside a container that was never going to work because its init container failed forty minutes ago.

---

## 🔵 §2 — When It Never Got Started

A Pod that is stuck before its first application container has run is the easiest fault in this chapter to misdiagnose, because the symptom — "nothing is happening" — is the least informative reading any instrument can give you. It looks identical to a dozen other things.

You have the model already. Init containers run before app containers, in the order written, one at a time, each to completion *[cross-bearing: see Ch 5 §3 — everything that must happen first]*. What Chapter 5 deliberately did not give you was the method for reading one when it goes wrong. And Chapter 13 owned the platform-side half of this failure: an init container whose *image* cannot be pulled is a platform-scope problem with a platform-scope signature *[cross-bearing: see Ch 13 §2 — pods that never start]*. What is left, and what this section owns, is the case where the init container runs perfectly well and does the wrong thing.

### Reading the state

Start with the Pod's status, which tells you which init container you are looking at:

```
kubectl get pod <pod-name>
```

The `STATUS` column carries a specific vocabulary for this case [source: k8s-docs-debug-init-containers-2026-09-04]. A Pod mid-sequence reports `Init:N/M` — *"The Pod has `M` Init Containers, and `N` have completed so far"* [source: k8s-docs-debug-init-containers-2026-09-04]. A Pod whose init container is failing reports `Init:Error` (*"An Init Container has failed to execute"*) or `Init:CrashLoopBackOff` (*"An Init Container has failed repeatedly"*) [source: k8s-docs-debug-init-containers-2026-09-04]. That is already a lot of information: `Init:1/3` tells you the first one succeeded and you should be looking at the second.

The Pod's phase is `Pending` throughout, with the `Initialized` condition false — *"a Pod that is initializing is in the `Pending` state but should have a condition `Initialized` set to false"* [source: k8s-docs-init-containers-2026-08-24] *[cross-bearing: see Ch 5 §5 — Pod phase and container state]*. This is why "read the phase first" alone does not finish the job here. Every Pod in this state has the same phase, and the discriminating detail is in the status string and the container list.

One more thing the status is telling you: a failing init container is not simply abandoned. *"If a Pod's init container fails, the kubelet repeatedly restarts that init container until it succeeds. However, if the Pod has a `restartPolicy` of Never, and an init container fails during startup of that Pod, Kubernetes treats the overall Pod as failed."* [source: k8s-docs-init-containers-2026-08-24] That is why `Init:CrashLoopBackOff` exists as a status at all, and it is why a Pod can sit at this station indefinitely rather than resolving to `Failed`.

### Reading the logs

Here is where people lose time:

```
kubectl logs <pod-name>
```

This returns nothing useful. The plain form targets the Pod's app container, and the app container has not started, so there is nothing to print. What you need is the `-c` flag naming the specific init container — *"Pass the Init Container name along with the Pod name to access its logs"* [source: k8s-docs-debug-init-containers-2026-09-04]:

```
kubectl logs <pod-name> -c <init-container-name>
```

The `-c` flag is not new to you *[cross-bearing: see Ch 13 §3 — reading logs from a multi-container Pod]*; what is new is that here it is not optional. A multi-container Pod at least gives you *a* log stream when you omit `-c`. An initializing Pod gives you an error or an empty result, and the reader who reads that as "the init container isn't logging anything" has just concluded something false about a container that is loudly complaining into a stream nobody asked for.

> 🪝 **Snag:** `kubectl logs <pod>` on a Pod stuck in init tells you nothing, and the nothing is misleading. Always name the init container with `-c`. If you don't know its name, `kubectl describe pod <pod>` lists the init containers in order, each with its state, its reason, its exit code, and its restart count [source: k8s-docs-debug-init-containers-2026-09-04].

### The three ways an init container is wrong

**Ordering.** Init containers are the mechanism Kubernetes gives you for holding an application back until a precondition is met: *"init containers offer a mechanism to block or delay app container startup until a set of preconditions are met"* [source: k8s-docs-init-containers-2026-08-24]. The most common failure is an init container waiting for something that cannot arrive until this Pod is up.

A classic shape, which follows directly from the sequencing rules above: an init container that blocks until a Service has endpoints, for a Service whose only backend is *this* Pod. The init container waits. The app container cannot start until the init container exits. The Pod cannot become ready until the app container starts. The Service cannot gain a ready endpoint until the Pod is ready. Two lines, each waiting for the other to take up the slack, and the deadlock is perfectly stable. Nothing in the platform will tell you this; the platform is doing exactly what you asked.

The tell is an `Init:0/1` Pod that has sat there for twenty minutes with no error, no restarts, and a log stream saying something calm and patient like "waiting for dependency."

**Non-idempotency.** An init container will be re-run. Not might — will. If the Pod restarts, every init container executes again from the beginning [source: k8s-docs-init-containers-2026-08-24]. An init container that assumes a clean slate — that creates a directory without checking, that runs a migration without a guard, that appends to a file that should have one line — works perfectly the first time and fails on every restart after. This produces one of the more maddening signatures in Kubernetes: a workload that comes up fine on a fresh deploy and refuses to come back after any disruption at all.

> ⚓ **Worth Securing:** Write init containers as though they will run five times, because eventually they will. Idempotency is not a nicety here; it is a correctness requirement imposed by the restart semantics. If your init container's job is "create X," its actual job is "ensure X exists."

**Configuration errors visible at init.** This one is practitioner observation rather than documented behavior. Init containers are frequently where a config problem first becomes visible, because the init container is usually the first thing that reads the mounted configuration. A ConfigMap key that does not exist, a Secret whose value is base64-decoded into something the wrong shape, a mount path that collides with something in the image: these surface as an init container exiting non-zero with a message that names the actual problem *[cross-bearing: see Ch 4 §4 — ConfigMaps and Secrets]*.

That last point is worth dwelling on, because it is the good news in this section. A config error caught at init gives you a clean, specific, non-mysterious failure with the reason printed in a log. The *same* config error that gets past init, because the value is present but wrong, becomes §3's problem, and §3's problem is much harder.

<!-- FIGURE: ch16-fig05-init-sequence-debug-points -->
![A left-to-right sequence of three init containers followed by the app containers. Beneath each, the Pod status it produces: Init:0/3 under the first init container, Init:1/3 under the second, Init:2/3 under the third, and Running under the app containers. Below, the commands for reading init container logs, and three failure signatures paired with their causes: stuck with no error means an ordering deadlock, failing only on restart means non-idempotency, and exiting non-zero means a configuration error.](figures/ch16-fig05-init-sequence-debug-points.svg)

<!-- ASCII-FALLBACK
```
  init-1 ──────▶ init-2 ──────▶ init-3 ──────▶ app containers
    │              │              │                  │
    ▼              ▼              ▼                  ▼
 STATUS:        STATUS:        STATUS:            STATUS:
 Init:0/3       Init:1/3       Init:2/3           Running

 READ WITH:  kubectl logs <pod> -c <init-name>
 ALSO READ:  kubectl describe pod <pod>   (init containers and their states)

 STUCK, NO ERROR ......... ordering deadlock — what is it waiting for?
 FAILS ONLY ON RESTART ... non-idempotent — it assumed a clean slate
 EXITS NON-ZERO, LOUDLY .. config error — read the message, it's telling you
```
-->

There is one more diagnostic surface here worth knowing. A container can write to a **termination message** file at `/dev/termination-log`, and Kubernetes surfaces the contents in the Pod's status [source: k8s-docs-determine-reason-pod-failure-2026-08-31]. The docs describe the purpose plainly: *"Termination messages provide a way for containers to write information about fatal events to a location where it can be easily retrieved and surfaced by tools like dashboards and monitoring software."* [source: k8s-docs-determine-reason-pod-failure-2026-08-31] For an init container that fails in a way that logs don't capture well, writing a one-line reason to the termination log makes the failure legible from `kubectl describe` alone.

---

## 🔵 §3 — Getting Inside, and Adding What Isn't There

The Pod is running. Your code is executing. And you have run out of what can be read from outside the hull.

This section is about getting inside a container, and about what to do when there is no inside to get into. It is the densest material in the chapter, and it has no analog anywhere earlier in the book. Chapter 8's kubectl verb table pointed here explicitly for `exec` *[cross-bearing: see Ch 8 §1 — the grammar of a command]*, and Chapter 12 pointed here for the debug-container case *[cross-bearing: see Ch 12 §6 — three levels, three modes]*. This is where both debts come due. If you are following one of those pointers and it said "getting inside a container" while another said "getting inside, and adding what isn't there" — same section, both phrasings, you are in the right place.

### `kubectl exec`

The direct move is to run a command inside a container that is already running:

```
kubectl exec -it <pod-name> -- /bin/bash
```

The docs describe it exactly this way: *"This page shows how to use `kubectl exec` to get a shell to a running container"* [source: k8s-docs-get-shell-running-container-2026-08-31]. For a multi-container Pod, name the container with `-c`, the same flag you have been using with `logs`:

```
kubectl exec -it <pod-name> -c <container-name> -- /bin/sh
```

The double dash matters: *"The double dash (`--`) separates the arguments you want to pass to the command from the kubectl arguments."* [source: k8s-docs-get-shell-running-container-2026-09-04] Everything after `--` is the command run inside the container; everything before it belongs to kubectl. Omit it and kubectl will try to interpret your command's flags as its own.

What you are actually doing in there, most of the time, is answering the second half of the second question: **is it configured the way you think?** Not "does the ConfigMap say what I meant"; you can read the ConfigMap from outside. The question is what the *process* got. Environment variables can be shadowed, mounted files can be masked by another mount, a default in the application code can quietly win over an empty string, and a value can be correct in the manifest and absent in the container because a mount path was one character off.

```
kubectl exec <pod-name> -- env | grep DATABASE
kubectl exec <pod-name> -- cat /etc/config/app.yaml
kubectl exec <pod-name> -- ls -la /etc/config/
```

That third one catches more bugs than the other two combined. A directory that is empty, or that contains a file named something you did not expect, is a mount that did not land the way the manifest reads.

> 🪝 **Snag:** The gap between "what the manifest says" and "what the process read" is where a large share of application-scope bugs live, and it is invisible from `kubectl get -o yaml`. The manifest is a statement of intent; the container's filesystem and environment are the outcome. When they disagree, `exec` is the only place you find out.

> 🪝 **Snag:** There is a second way the manifest and reality disagree, and `exec` cannot see this one at all, because the field never reached the server. *"Often a section of the pod description is nested incorrectly, or a key name is typed incorrectly, and so the key is ignored"* [source: k8s-docs-debug-pods-2026-08-23]. The apply succeeded. Nothing errored. The field is simply absent from what the API server stored, and the container is faithfully running the spec that actually exists rather than the one you wrote. The move is a round trip: apply, then read back what the server kept and compare it against your file. The docs prescribe exactly that, comparing `kubectl get pods/mypod -o yaml` against the original [source: k8s-docs-debug-pods-2026-08-23].

### The image with nothing in it

Now the problem.

```
kubectl exec -it <pod-name> -- /bin/sh
```
```
OCI runtime exec failed: exec failed: unable to start container process:
exec: "/bin/sh": stat /bin/sh: no such file or directory
```

There is no shell. There is no `cat`, no `ls`, no `env` binary, no package manager to install one with. The image contains your application binary, the libraries it links against, and nothing else. This is a **distroless** image, and it is not a mistake. It is a deliberate hardening choice. The Kubernetes documentation is direct about the trade: *"…distroless images enable you to deploy minimal container images that reduce attack surface and exposure to bugs and vulnerabilities. Since distroless images do not include a shell or any debugging utilities, it's difficult to troubleshoot distroless images using `kubectl exec` alone."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

Your first instinct is probably right and also unavailable: add a second container to the Pod with the tools in it. You cannot.

> ★ **Fixed Point:**
>
> **You cannot add a container to a Pod once the Pod has been created.** The Pod's container list is fixed at creation. That single fact is the entire reason ephemeral containers exist as a separate mechanism, and it is the fact worth carrying into a question about them.

The documentation states the constraint and the consequence together: *"Since Pods are intended to be disposable and replaceable, you cannot add a container to a Pod once it has been created. Instead, you usually delete and replace Pods in a controlled fashion using deployments."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31] And then the exception: *"Sometimes it's necessary to inspect the state of an existing Pod, however, for example to troubleshoot a hard-to-reproduce bug. In these cases you can run an ephemeral container in an existing Pod to inspect its state and run arbitrary commands."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

### Ephemeral containers

An ephemeral container is a container that runs temporarily inside an existing Pod, added through a dedicated API path rather than by editing the Pod's spec. The documentation is explicit that it is not editable through the normal route: *"Ephemeral containers are created using a special `ephemeralcontainers` handler in the API rather than by adding them directly to `pod.spec`, so it's not possible to add an ephemeral container using `kubectl edit`."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

They are deliberately constrained, and the constraints are exam material [source: k8s-docs-ephemeral-containers-concept-2026-08-31]:

- **No ports, no probes.** *"Ephemeral containers may not have ports, so fields such as `ports`, `livenessProbe`, `readinessProbe` are disallowed."*
- **No resource requests or limits.** *"Pod resource allocations are immutable, so setting `resources` is disallowed."*
- **No removal, no change.** *"Like regular containers, you may not change or remove an ephemeral container after you have added it to a Pod."*
- **No restarts.** *"Ephemeral containers differ from other containers in that they lack guarantees for resources or execution, and they will never be automatically restarted, so they are not appropriate for building applications."*
- **Not on static Pods.** *"Note: Ephemeral containers are not supported by static pods."* *[cross-bearing: see Ch 13 §5 — when the node is the problem]*

Read those five together and the design intent is obvious: this is an instrument, not a workload. It gets no guarantees because it is not supposed to be part of your application, and it cannot be removed because a Pod's container list, even the ephemeral part of it, is append-only.

> 🪢 **Mnemonic:** An ephemeral container is a **tool passed through the hatch**, not a compartment added to the hull. No resources reserved for it, no probes watching it, no restart if it dies, and once it's through the hatch you cannot take it back.

### `kubectl debug`

`kubectl debug` is the verb that puts one there. In its simplest form it attaches an ephemeral container to a running Pod, using an image you choose, one that has the tools the target image lacks:

```
kubectl debug -it <pod-name> --image=busybox:1.28 --target=<container-name>
```

`--target` names the container you want the debug container to be able to see into: *"The `--target` parameter targets the process namespace of another container."* [source: k8s-docs-debug-running-pod-2026-09-04] The principle behind it: *"When using ephemeral containers, it's helpful to enable process namespace sharing so you can view processes in other containers."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31] Without a shared view of the target's processes, an ephemeral container is a separate process tree in the same Pod, and most of what you wanted to inspect is invisible from it. One caveat the docs attach: the container runtime has to support it, and where it does not, *"the Ephemeral Container may not be started, or it may be started with an isolated process namespace so that `ps` does not reveal processes in other containers"* [source: k8s-docs-debug-running-pod-2026-09-04].

That is one of three shapes. The other two answer different questions.

### `--copy-to`: a copy, not a repair

The second shape makes a **copy** of the Pod and modifies the copy:

```
kubectl debug <pod-name> -it --image=ubuntu --share-processes --copy-to=<new-pod-name>
```

The documentation's framing: *"Sometimes Pod configuration options make it difficult to troubleshoot in certain situations. For example, you can't run `kubectl exec` to troubleshoot your container if your container image does not include a shell or if your application crashes on startup. In these situations you can use `kubectl debug` to create a copy of the Pod with configuration values changed to aid debugging."* [source: k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31]

> ★ **Fixed Point:**
>
> **`--copy-to` makes a copy. The original Pod is not touched — and that is the feature, not a limitation.** You get a new Pod with whatever changes you need (a different command, an extra container, a shell as the entrypoint) while the broken Pod keeps running exactly as it was, still serving traffic, still available for the platform team to look at, still in the state that produced the bug.

This is the part most readers get backwards on first encounter. The mental model people arrive with is that a debugging tool operates on the thing being debugged: you attach a debugger to the process, you modify the running system. `--copy-to` does the opposite, and on a cluster you do not own, running a workload you did not deploy, that inversion is the whole point. You can experiment freely on a copy. You cannot experiment freely on production.

The copy is also the answer to a case `exec` can never handle: a container that crashes on startup. There is no running process to enter, and by the time you type the command it is gone again. Copy the Pod, change the entrypoint to a shell, and now you have a container built from the same image, with the same config, that sits still while you look at it.

> ⚓ **Worth Securing:** A copy is a real Pod. It consumes resources and it will sit there until you delete it. Clean up after yourself — `kubectl delete pod <copy-name>`. One detail that matters on a shared cluster: by default the copy is created *without* the original Pod's labels — the `--keep-labels` flag exists to opt back in, described as *"If true, keep the original pod labels"* [source: k8s-docs-kubectl-debug-reference-2026-09-04] — so a Service selecting the original's labels does not pick the copy up, and the copy does not start receiving live traffic.

### `kubectl debug node/`: stepping back over the line

The third shape targets a node rather than a Pod:

```
kubectl debug node/<node-name> -it --image=ubuntu
```

This creates a Pod on the target node with access to the node's filesystem and host namespaces: *"The root filesystem of the Node will be mounted at `/host`"* and *"the container runs in the host IPC, Network, and PID namespaces"* [source: k8s-docs-debug-running-pod-2026-09-04]. It is genuinely useful and it is, unmistakably, the moment you step back across the boundary §1 drew. A node is not application scope. If you find yourself reaching for `debug node/`, you have either concluded that the fault is platform-side — in which case the right move is usually to hand it to whoever owns the platform, with the evidence you gathered — or you *are* the person who owns the platform, wearing a different hat.

Which makes it an argument for the boundary rather than an exception to it. The tool exists, it is on the same documentation page as the others, and the reason it feels out of place here is that it *is* out of place here. Notice the feeling. It is the boundary doing its job. Node-level diagnosis, including the node-local tooling below the Kubernetes API, belongs to the platform-scope chapter *[cross-bearing: see Ch 13 §5 — when the node is the problem]*.

> ⚠ **Navigational Hazards**
>
> **A debug container is a container, and admission can refuse it.**
>
> You have RBAC permission to run `kubectl debug`. You run it. It fails — not with a permissions error on the verb, but with a rejection from admission control. This is not a bug and it is not RBAC.
>
> The ephemeral container you are injecting is a container in that namespace, and Pod Security Admission *"places requirements on a Pod's Security Context and other related fields according to the three levels defined by the Pod Security Standards"* [source: k8s-docs-pod-security-admission-2026-08-31] *[cross-bearing: see Ch 12 §6 — three levels, three modes]*. Those Standards name ephemeral containers explicitly: the restricted fields for each control cover `spec.containers[*]`, `spec.initContainers[*]`, and `spec.ephemeralContainers[*]` alike, including `securityContext.privileged` and, under `restricted`, `securityContext.runAsNonRoot` [source: k8s-docs-pod-security-standards-2026-09-04]. In a namespace enforcing the `restricted` standard, a debug image that wants to run as root, or wants elevated capabilities, or wants host namespace access, has asked for more than the namespace permits. A container that would not be allowed to exist there does not become allowed by being ephemeral.
>
> This is an easy failure to misread as "I don't have permission to debug." You do. The *container you asked for* doesn't meet the namespace's standard. Try a debug image that runs as non-root, or ask the namespace's owner what the enforcement level is.

### Debug profiles

`kubectl debug` also accepts a `--profile` flag that sets a bundle of security-related properties on the debug container: *"specific properties such as securityContext are set, allowing for adaptation to various scenarios"* [source: k8s-docs-debug-running-pod-2026-09-04]. The generated CLI reference for the current release lists five profiles — `general`, `baseline`, `restricted`, `netadmin`, and `sysadmin` — with `general` as the default [source: k8s-docs-kubectl-debug-reference-2026-09-04]. The task page still documents a sixth, `legacy`, as the default in earlier releases and marks it for deprecation [source: k8s-docs-debug-running-pod-2026-09-04]. The default, in other words, has moved between releases; do not memorize it.

The shape to remember, rather than the list: a profile is a preset for how much privilege the debug container asks for, and asking for more than the namespace allows is what triggers the admission refusal in the Hazard above. The `restricted` profile exists as the low-privilege end of that range, which is the end you want in a namespace enforcing the restricted standard.

<!-- FIGURE: ch16-fig02-ephemeral-container-debug -->
![Three panels comparing kubectl debug's shapes. Panel A: an ephemeral debug container added inside an unchanged Pod alongside a distroless app container, annotated as unable to be removed; it asks what the running process sees now. Panel B: two unconnected Pods side by side, the original still running and crashing on startup, and a separate copy with its entrypoint replaced; it asks what would happen if something changed. Panel C, shown as platform scope: a debug Pod on a Node with the host filesystem mounted; it asks whether the machine itself is the problem.](figures/ch16-fig02-ephemeral-container-debug.svg)

<!-- ASCII-FALLBACK
```
  (A) EPHEMERAL CONTAINER — into the running Pod
      ┌─────────── Pod (unchanged) ───────────┐
      │  [app: distroless]  + [debug: busybox]│  ← added, cannot be removed
      └───────────────────────────────────────┘
      ASKS: "what does the running process see right now?"

  (B) COPY-TO — a NEW Pod, original untouched
      ┌─── Pod (running, untouched) ───┐   ┌─── Pod-copy ────────┐
      │  [app: crashing on startup]    │   │  [app: entrypoint   │
      │                                │   │        replaced]    │
      └────────────────────────────────┘   └─────────────────────┘
      ASKS: "what would happen if I changed something?"

  (C) node/ — the host, not the workload
      ┌─── Node ───────────────────────────────┐
      │  [debug Pod, host filesystem access]   │  ← PLATFORM SCOPE
      └────────────────────────────────────────┘
      ASKS: "is the machine itself the problem?"   (see Ch 13 §5)
```
-->

Three shapes, three questions. They are not interchangeable, and choosing the wrong one is how you spend twenty minutes in a copy of a Pod investigating a problem that only exists in the original.

---

## ☆ Taking Your Bearings: Taking the Handoff, and Getting Inside

Six questions on §1 through §3. One of them tests material from an earlier chapter.

**1.** A Pod is `Running`, reports `1/1 Ready`, has zero restarts, and its node shows no adverse conditions. Two other workloads in the same namespace are behaving normally. The application returns HTTP 500 on one endpoint. What does the scope test tell you?

- A) Platform scope — a 500 indicates a runtime failure the kubelet should have caught
- B) Application scope — the fault is confined to one workload and every platform signal is clean
- C) Indeterminate — you need node-level access before you can decide
- D) Platform scope — readiness probes passing means the platform is asserting the app is correct

**2.** A Pod shows `STATUS: Init:1/3`. Which command gives you the most useful next piece of information?

- A) `kubectl logs <pod>`
- B) `kubectl logs <pod> -c <second-init-container-name>`
- C) `kubectl exec -it <pod> -- sh`
- D) `kubectl port-forward <pod> 8080:8080`

**3.** Why do ephemeral containers exist as a separate API mechanism rather than as an ordinary edit to a Pod's spec?

- A) Because ephemeral containers must be declared before the Pod is scheduled
- B) Because a Pod's container list cannot be added to once the Pod exists
- C) Because ephemeral containers are scheduled to a different node
- D) Because RBAC cannot grant `update` on Pods

**4.** You run `kubectl debug <pod> --copy-to=<pod>-debug --image=ubuntu`. Immediately afterward, what is the state of the original Pod?

- A) Terminated and replaced by the copy
- B) Running, but with the ubuntu container now attached to it
- C) Running, entirely unchanged
- D) Paused until the debug session ends

**5.** An init container's job is `mkdir /data/cache`. The workload deploys cleanly. Three weeks later the node is drained and the Pod is rescheduled; the Pod now fails to start. What is the most likely explanation?

- A) The PersistentVolume failed to reattach on the new node
- B) The init container is not idempotent and fails when the directory already exists
- C) The init container image was garbage-collected from the new node
- D) Init containers do not run on rescheduled Pods

**6.** `[retrieval: ch2]` You run `kubectl exec -it <pod> -- /bin/sh` and get `stat /bin/sh: no such file or directory`. What does this tell you about the image?

- A) The image is corrupted and needs to be repulled
- B) The container runtime does not support `exec`
- C) The image was built without a shell — it contains only what was put into it
- D) `/bin/sh` exists but the container is running as a user without execute permission on it

---

**Answers with Explanations:**

**1 — B.** Every element of the mechanical test points the same way: the workload is running, ready, and stable; the fault does not extend beyond it; and no platform signal is adverse.

- **A is wrong** because HTTP status codes are application output. The kubelet has no opinion about your response bodies, and a 500 is not a container failure. The container is working fine, returning exactly what your code told it to return.
- **C is wrong** and this is the important distractor. It is true that you may lack node-level access. It is not true that this makes the diagnosis indeterminate; §1's addition to the test says the opposite. You make the case from what you *can* see, and here what you can see is conclusive.
- **D is wrong** because a readiness probe asserts that the container is willing to receive traffic, not that it produces correct answers. A probe that hits `/healthz` and gets a 200 will pass happily while every other endpoint returns garbage *[cross-bearing: see Ch 5 §7 — liveness, readiness, and startup probes]*.

**2 — B.** `Init:1/3` means the first init container completed and the second is where you are. Name it with `-c` and read its output.

- **A is wrong** — the most common time-waster in this whole section. The plain form targets an app container that has not started; you get nothing useful, and the nothing looks like silence rather than like a misdirected question.
- **C is wrong** because there is no app container running to exec into. You would need `-c` here too, and even then, exec into a *running* init container is a narrow move that only helps if the init container is hanging rather than exiting.
- **D is wrong** because nothing is listening. `port-forward` requires a running process on the target port; this Pod has not reached its application yet.

**3 — B.** This is the Fixed Point stated as a question. The container list is fixed at Pod creation, so a mechanism to add a *temporary* container had to be built outside the normal spec-editing path — hence the dedicated `ephemeralcontainers` API handler [source: k8s-docs-ephemeral-containers-concept-2026-08-31].

- **A is wrong, and it inverts the mechanism.** The entire point of an ephemeral container is that it is added *after* the Pod exists: *"you can run an ephemeral container in an existing Pod to inspect its state"* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]. A container declared before scheduling is just an ordinary container.
- **C is wrong** — they run in the existing Pod, on the node the Pod is already on. That is the entire point; a container on another node would see none of the state you are trying to inspect.
- **D is wrong** because the constraint is architectural, not authorization-based. Even with unlimited permissions on Pods, you could not add a container to one that already exists, which is exactly what the Fixed Point says.

**4 — C.** Unchanged, still running, still serving. The copy is a separate Pod.

- **A is wrong** and is the misconception this option exists to catch. Nothing is deleted. If `--copy-to` terminated the original, it would be useless for its main purpose: debugging something you cannot afford to disturb.
- **B is wrong** — that describes the plain ephemeral-container form (`kubectl debug` without `--copy-to`), which is a different shape answering a different question.
- **D is wrong** — Kubernetes has no notion of pausing a Pod for inspection.

**5 — B.** A fresh deploy hits an empty volume and `mkdir` succeeds. A rescheduled Pod re-runs every init container [source: k8s-docs-init-containers-2026-08-24] against a volume where `/data/cache` already exists, `mkdir` exits non-zero, and the Pod is stuck. Classic non-idempotency.

- **A is possible in principle but is the wrong first answer** — and it is the wrong first answer in a specific, instructive way. A PV reattachment failure is platform scope, would produce a different signature (the Pod stuck on volume mounting, with events saying so), and would not be preceded by three weeks of clean operation followed by an init failure specifically. Reach for the application-scope explanation when the application-scope signature is what you're looking at.
- **C is wrong** — a garbage-collected image is repulled, and a pull failure has its own distinctive signature *[cross-bearing: see Ch 13 §2 — pods that never start]*.
- **D is wrong** and is the outright false statement in the set. *"If the Pod restarts, or is restarted, all init containers must execute again"* [source: k8s-docs-init-containers-2026-08-24], which is exactly what makes idempotency mandatory.

**6 — C.** An image contains exactly what was put into it. No shell in the image means no shell in the container; there is no host filesystem underneath supplying the gaps *[cross-bearing: see Ch 2 §2 — what's inside an image]*.

- **A is wrong** — a corrupt image fails at pull or at container creation, not with a clean "this specific path does not exist."
- **B is wrong** — the runtime supports `exec` fine. It attempted the exec and reported, accurately, that the binary you named is not there.
- **D is wrong** — a permission problem produces a permission error. `no such file or directory` is a statement about existence.

---

**How'd You Do?**

**If you scored 0–2:** Stop here rather than pressing on. §4 assumes the boundary is settled and the tools are in hand, and it will read as a list of commands if either is shaky. Re-read **§2** and **§3**. If question 1 was among the misses, re-read **Chapter 13 §1** first — the scope test is the thing everything after it rests on.

**If you scored 3–4:** Solid footing. Read the why-wrong explanation for each one you missed — most of the value in this checkpoint is in the wrong answers — then continue.

---

**Checkpoint: You've Now Mastered**

✓ Placing a fault on the correct side of the scope boundary, including when you cannot see the other side
✓ The four triage questions and why "is it configured" appears twice
✓ Reading a failing init container, and the three ways one goes wrong
✓ `exec` for the container that has a shell, and the two places the manifest and reality diverge
✓ Ephemeral containers, `kubectl debug`, and the three shapes it takes

Two questions remain: is it reachable, and what changes when the replicas aren't interchangeable. The next section is the one where a perfectly correct Service does nothing at all.

---

## 🔵 §4 — Is Anything Even Selected

You have a Service. It exists. `kubectl get service` returns it, complete with a ClusterIP. It is a name on the chart pointing at a position, and requests to it fail.

Chapter 9 gave you the model: a Service is a name and a selector, and behind the name is a list of endpoints assembled by matching that selector against Pod labels *[cross-bearing: see Ch 9 §4 — the list behind the name]*. Chapter 9 also told you, in as many words, that this chapter owns the troubleshooting workflow and would come back for those facts by name. Here we are.

The single most useful command in this section is the one that reads the list:

```
kubectl get endpointslices -l kubernetes.io/service-name=<service-name>
```

That label is not arbitrary. Every EndpointSlice the control plane creates for a Service carries a `kubernetes.io/service-name` label, and the docs say it exists precisely to enable *"simple lookups of all EndpointSlices belonging to a Service"* [source: k8s-docs-endpointslices-2026-08-24] *[cross-bearing: see Ch 9 §4 — the list behind the name]*. And the interpretation is direct, from the docs: *"Make sure that the endpoints in the EndpointSlices match up with the number of pods that you expect to be members of your service. If they don't, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready."* [source: k8s-docs-debug-pods-2026-08-23]

> ★ **Fixed Point:**
>
> **A Service with no *ready* endpoints is not broken. It is working exactly as written, and finding nothing it is willing to send traffic to.** There are two causes, and they live in two different files: the selector does not match the Pod labels, or the Pods match but are not Ready.

That distinction is the whole diagnostic value of the reading. The Service object is fine. The controller is fine. Nothing has failed. Something is *mismatched*, and the mismatch is either in the label/selector relationship or in the readiness state, and knowing which of those two you are looking at tells you which file to open.

**And the slice itself tells you which.** This is worth getting exactly right, because the two causes leave different traces. The control plane *"automatically creates EndpointSlices for any Kubernetes Service that has a selector specified,"* and those slices *"include references to all the Pods that match the Service selector"* [source: k8s-docs-endpointslices-2026-08-24]. **All** the matching Pods — readiness is not a filter on membership. What readiness controls is a condition on each endpoint: the `serving` condition *"indicates that the endpoint is currently serving responses, and so it should be used as a target for Service traffic,"* and for endpoints backed by a Pod, *"this maps to the Pod's `Ready` condition"* [source: k8s-docs-endpointslices-2026-08-24].

So: a selector that matches nothing leaves the slice with no endpoints at all. Readiness that is failing leaves the endpoints exactly where they are, marked not ready, and service proxies skip them. Same practical outcome for your traffic; two different readings on the screen, and the difference is the diagnosis.

<!-- AUTHOR-REVIEW (figure, still open at the 2026-09-04 audit): the rendered ch16-fig04 (SVG/PNG dated 2026-09-01) still labels breaks 1+2 as LIST EMPTY and its legend says upstream breaks empty the list. The prose above and the corrected ASCII-FALLBACK below say otherwise: a selector mismatch leaves the slice empty, but Pods that match and are not Ready stay in the slice marked ready:false. The image-specs entry must be re-synced to the ASCII below and the figure re-rendered; the alt text describes the current render and must be rewritten when the render changes. -->

### Four break points, and two of them are not about the list

Here is where the section has to be careful, because four things can break a request to a Service and only two of them are about whether anything is selected.

<!-- FIGURE: ch16-fig04-service-break-points -->
![A request path runs left to right from client, to DNS name, to Service, to EndpointSlice, to Pod, to container port. Three callouts drop from it. From the DNS name: break four, the name does not resolve to this Service. From the EndpointSlice: breaks one and two, no ready endpoints — a selector mismatch leaves the slice empty, while Pods that are not Ready stay listed with ready false. From the container port: break three, port does not equal targetPort, and here the endpoints are ready. A legend notes that breaks one and two sit upstream of readiness and yield no ready endpoints, break three sits downstream with ready endpoints and a failing request, and break four means this Service was never reached.](figures/ch16-fig04-service-break-points.svg)

<!-- ASCII-FALLBACK
```
  client ──▶ DNS name ──▶ Service ──▶ EndpointSlice ──▶ Pod ──▶ container port
               │                          │                        │
               │                          │                        │
          ┌────┴────┐              ┌──────┴──────┐          ┌──────┴──────┐
          │ BREAK 4 │              │  BREAK 1+2  │          │   BREAK 3   │
          │ name    │              │  NO READY   │          │ port ≠      │
          │ doesn't │              │  ENDPOINTS  │          │ targetPort  │
          │ resolve │              │             │          │             │
          │ to this │              │ 1 selector  │          │ (endpoints  │
          │ Service │              │   mismatch  │          │  ARE ready) │
          │         │              │   → slice   │          │             │
          │         │              │     empty   │          │             │
          │         │              │ 2 not Ready │          │             │
          │         │              │   → ready:  │          │             │
          │         │              │     false   │          │             │
          └─────────┘              └─────────────┘          └─────────────┘

  UPSTREAM of readiness ...... breaks 1 and 2 → NO READY ENDPOINTS
  DOWNSTREAM of readiness .... break 3 → ENDPOINTS READY, request still fails
  BESIDE the whole path ...... break 4 → you never reached this Service at all
```
-->

**Break 1 — selector/label mismatch.** The Service's `spec.selector` and the Pod template's `metadata.labels` are written in two different places, frequently in two different files, and they drift. Someone renames `app: web` to `app: web-frontend` in the Deployment and does not touch the Service. Everything applies cleanly. Nothing errors. The slice goes empty and stays that way.

The docs treat it as a routine check — *"Now let's check that the Pods you ran are actually being selected by the Service"* — and name the signature: *"If the `ENDPOINTS` column is `<none>`, you should check that the `spec.selector` field of your Service actually selects for `metadata.labels` values on your Pods. A common mistake is to have a typo or other error"* [source: k8s-docs-debug-service-2026-09-04]. Check both sides:

```
kubectl describe service <service-name>        # what does it select?
kubectl get pods -l <selector-from-above>      # does anything match?
kubectl get pods --show-labels                 # what do the Pods actually carry?
```

**Break 2 — not Ready.** The Pods match perfectly. The selector is correct. They are all in the slice. And every one of them is `0/1 READY`, so every endpoint in that slice is marked not ready and no service proxy will send it anything. Readiness does not remove an endpoint; it disqualifies it *[cross-bearing: see Ch 9 §4 — the list behind the name]*.

This is the quiet one, and it is quiet because the Pods look alive. `kubectl get pods` shows `Running`. The restart count is zero. Nothing is crashing. The `READY` column is the only place the truth is printed, and it is a column people's eyes slide past *[cross-bearing: see Ch 13 §4 — pods that start and then don't stay]*. If nothing is receiving traffic and the selector checks out, look at the readiness state before you look at anything else.

> 🪝 **Snag:** No ready endpoints has exactly two causes, and the slice itself separates them. **Zero endpoints in the slice** means nothing matched the selector, a label problem, and the labels live in the Deployment's Pod template. **Endpoints present but not ready** means readiness is holding them back, and that lives in the probe definition. If your tooling only shows you a ready count, `kubectl get pods -l <the-service-selector>` settles it the same way in one command: nothing returned is a mismatch, Pods returned is a readiness problem.

**Break 3 — `port` vs `targetPort`.** Now a different failure shape entirely. The selector matches. The Pods are ready. The endpoints are ready. And requests still fail, because the Service is delivering traffic to a port nothing is listening on.

`port` is the port the Service is reachable at; `targetPort` is *"the port on the container to send traffic to"* [source: k8s-docs-service-ports-2026-08-24], and it is the one that has to match what the container actually binds *[cross-bearing: see Ch 9 §3 — four ways to be reachable]*. The docs' checklist under *"Is the Service defined correctly?"* asks it in one line: *"Is the `targetPort` correct for your Pods (some Pods use a different port than the Service)?"* [source: k8s-docs-debug-service-2026-09-04]

```yaml
spec:
  ports:
  - port: 80          # clients connect here
    targetPort: 8080  # the container must be listening HERE
```

If the container listens on 8080 and `targetPort` says 80, everything selects correctly and every request lands on a closed port.

**Break 4 — the name.** And the fourth one is not about this Service at all: the DNS name the client is using does not resolve to the Service you have been staring at. A typo in the namespace, a name that resolves in the client's own namespace to something else, a hardcoded name from a different environment. Normal Services get a record *"of the form my-svc.my-namespace.svc.cluster-domain.example"*, and *"by default, a client Pod's DNS search list includes the Pod's own namespace"*, so a short name resolves relative to the *client's* namespace, not the service's [source: k8s-docs-dns-pod-service-2026-08-23] *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*.

The docs' first debugging move for this is to run a Pod in the cluster and look from where the client looks: *"For many steps here you will want to see what a Pod running in the cluster sees. The simplest way is to run an interactive busybox Pod:"* [source: k8s-docs-debug-service-2026-08-31] From inside that Pod, resolve the name and see what comes back, or whether anything does.

> ⚓ **Worth Securing:** Keep breaks 1–2 and breaks 3–4 on separate pages of the log. Breaks 1 and 2 produce **no ready endpoints**. Break 3 produces **ready endpoints and a failed request**. Break 4 means you never reached this Service in the first place. If you conflate them, you will go hunting for a label mismatch behind a Service whose endpoints are all ready, and the slice was telling you the answer the whole time.

---

## ⚪ §5 — Bypassing the Service on Purpose

There is a move available at this point that is more useful than it looks.

```
kubectl port-forward <pod-name> 8080:80
```

This opens a tunnel from a port on your local machine to a port on a Pod in the cluster. The docs describe the mechanism plainly: *"`kubectl port-forward` allows using resource name, such as a pod name, to select a matching pod to port forward to."* [source: k8s-docs-port-forward-2026-08-31] It is commonly used for convenience — reaching a database or an admin interface from a laptop without exposing it — and that use is real and fine and not what this section is about.

What this section is about is what happens when you use it as an experiment.

### Two paths that share almost nothing

<!-- FIGURE: ch16-fig03-portforward-vs-service-path -->
![Two separate request paths. The Service path, traveled by users, runs from client to DNS to the Service's ClusterIP to the service proxy, kube-proxy or its equivalent, to the Pod's targetPort, annotated with selector and endpoints at the Service; all four of section four's break points live on this path. The port-forward path, traveled by the engineer, runs from kubectl to the API server via the pods/portforward subresource and on to the Pod's port. The two paths share no step except the Pod itself.](figures/ch16-fig03-portforward-vs-service-path.svg)

<!-- ASCII-FALLBACK
```
  THE SERVICE PATH (what your users travel)
  client ──▶ DNS ──▶ Service (ClusterIP) ──▶ service proxy ──▶ Pod:targetPort
                          │                        │
                     selector, endpoints    kube-proxy or its equivalent
                     [ §4 breaks 1-4 all live on this path ]

  THE PORT-FORWARD PATH (what you travel)
  kubectl ──▶ API server ──▶ Pod:port
                    │
            pods/portforward subresource
            [ shares NO step with the path above except the Pod itself ]
```
-->

<!-- AUTHOR-REVIEW (revision stage — figure redrawn): draft-v1 drew the lower path as `kubectl → API server → kubelet → Pod`. No cached snapshot states the full port-forward request path; `k8s-docs-port-forward-authorization-2026-08-31`'s own significance note records that "the full path (API server -> kubelet -> Pod) is still NOT stated on any page found." The API-server hop IS established, by the `pods/portforward` subresource. The kubelet hop was inference. The figure now stops at the API server, which is what the evidence supports and is entirely sufficient for the section's argument. The upper path's proxy label is also now generic — `k8s-docs-cluster-architecture-2026-08-23` marks kube-proxy optional ("if you use a network plugin that implements packet forwarding for Services by itself... you do not need to run kube-proxy"). The image-specs entry documents both variants; re-sync it to this one. -->

The port-forward path is an API-server operation, not a networking one. The authorization requirements make this concrete: *"To use `kubectl port-forward`, a user must have permission to access the target resource (for example, a Pod or Service) and the `portforward` subresource. Typical required permissions include `get` on `pods` and `create` on `pods/portforward`."* [source: k8s-docs-port-forward-authorization-2026-08-31] You are not routing traffic through the cluster's Service machinery. You are asking the API server to open a channel to a Pod, and it does.

The same documentation notes the security consequence, which is also the diagnostic consequence: *"Cluster administrators should carefully restrict these permissions, as port-forwarding can provide direct network access to workloads and may bypass network-level controls."* [source: k8s-docs-port-forward-authorization-2026-08-31]

"May bypass network-level controls" is, from the diagnostic side, the entire point. If the path skipped nothing, the experiment would prove nothing.

### The inference, and the trap inside it

So: your Service call fails. You port-forward straight to a Pod behind that Service. It works. The application responds correctly.

The instinct at this moment is relief — *the app is fine.* And that instinct, left alone, is where the diagnosis stops being useful, because "the app is fine" is not a conclusion. It is half of one.

> ★ **Fixed Point:**
>
> **A working `port-forward` beside a failing Service call does not mean the application is fine. It means the application is fine *and the Service path is not.*** It is a narrowing step, not a clean bill of health — and the thing it narrows to is exactly the four break points in §4.

Read it as an elimination. The port-forward path shares nothing with the Service path except the Pod itself. If traffic arriving directly at the Pod produces a correct response, then the process is running, listening, and serving correctly, and every remaining candidate lives on the path you just skipped: the DNS name, the selector, the endpoints, the service proxy, the port pairing.

> 🪢 **Mnemonic:** Port-forward is a **second approach to the same anchorage**. If the boat can be reached from seaward but not up the channel, the boat is fine and the channel is the problem. You have not fixed anything. You have halved the map.

And the negative case is just as informative. If the port-forward *also* fails — connection refused, or a hang, or the same wrong response — then the Service path is exonerated and the fault is inside the container. That sends you back to §3: exec in, check what the process is actually bound to, check what config it actually read.

> ⚓ **Worth Securing:** Note which port you forwarded to. `kubectl port-forward pod/x 8080:80` reaches container port 80. If the container is listening on 8080 and you happened to forward to 8080, you have accidentally routed around break 3 as well, and a successful port-forward on the *right* port while the Service points at the *wrong* one is precisely the `port`/`targetPort` signature. Forward to the port the container claims to use, then compare that number against the `targetPort` the Service declares — `kubectl describe service <name>` prints it.

One clarifying note on scope: `port-forward` is a diagnostic here, and only a diagnostic. It is not how applications reach each other in a cluster and it is not an exposure mechanism; the Service machinery for that is Chapter 9's *[cross-bearing: see Ch 9 §6 — the component that makes it real]*, and exposure from outside the cluster is Chapter 10's. Also: *"`kubectl port-forward` is implemented for TCP ports only"* [source: k8s-docs-port-forward-2026-09-04], and it terminates when you stop the command.

---

## 🟡 §6 — When Each Replica Is Its Own

Everything so far has assumed something that is usually true and sometimes catastrophically false: that your replicas are interchangeable. That if you diagnose one, you have diagnosed all of them.

For a Deployment, that assumption holds. Three replicas of a stateless service are three instances of the same thing; whichever one you exec into will tell you the same story. For a StatefulSet it does not hold at all, and the four questions have to be asked of a *particular* replica rather than of the workload.

Three things make this different, and each is a retrieval you already have with a diagnostic turn on it.

### Find out which one

A StatefulSet's Pods have stable ordinal identity — `web-0`, `web-1`, `web-2` — and *"each has a persistent identifier that it maintains across any rescheduling"* [source: k8s-docs-statefulset-2026-08-24] *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*. The diagnostic consequence: **"the app is broken" is very frequently "`web-2` is broken, and `web-0` and `web-1` are fine."**

So the first move is not to investigate. It is to find out which replica you are investigating.

```
kubectl get pods -l app.kubernetes.io/name=MyApp
```

The docs give exactly this form for listing a StatefulSet's Pods by label [source: k8s-docs-debug-statefulset-2026-09-04]. Look at the whole list before you pick one. A single unhealthy ordinal among healthy siblings is a completely different diagnosis from all three being unhealthy: the first says something is wrong with that replica's *state*, the second says something is wrong with the *workload*.

The docs also flag one specific case worth knowing: *"If you find that any Pods listed are in `Unknown` or `Terminating` state for an extended period of time, refer to the Deleting StatefulSet Pods task for instructions on how to deal with them."* [source: k8s-docs-debug-statefulset-2026-09-04] The reason such a Pod matters more here than in a Deployment is the controller's ordering guarantees: *"Before a scaling operation is applied to a Pod, all of its predecessors must be Running and Ready"* and *"Before a Pod is terminated, all of its successors must be completely shut down"* [source: k8s-docs-statefulset-2026-08-24]. A StatefulSet that seems frozen mid-rollout usually has one Pod in one of those states, and the freeze is the controller obeying its own rules *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*.

### The state that survives everything you try

This is the one that most looks like a platform fault and is not.

Each StatefulSet replica gets its own PersistentVolumeClaim from `volumeClaimTemplates` — *"for each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim"*, and *"the same PersistentVolumeClaim will be bound to a Pod throughout its lifecycle"* [source: k8s-docs-statefulset-2026-08-24] *[cross-bearing: see Ch 11 §6 — Pods that are not interchangeable, revisited]*. The claim is not deleted when the Pod is deleted. The default retention policy is `Retain` for both the scale-down and the delete case: *"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted"* and *"The default for policies is Retain, matching the StatefulSet behavior before this new feature."* [source: k8s-docs-statefulset-storage-2026-08-25] And for the involuntary case: *"if a Pod associated with a StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch."* [source: k8s-docs-statefulset-storage-2026-08-25]

Now put that next to the most common debugging reflex in the industry.

Your application writes a corrupt record. `web-2` starts failing. You delete `web-2`. The controller recreates it, with the same name, the same DNS record, and **the same volume, containing the same corrupt record.** It fails again, identically. You delete it again. Same result.

> ⚠ **Navigational Hazards**
>
> **"Turn it off and on again" does not clear a StatefulSet replica's state, and the failure it leaves behind looks exactly like a platform bug.**
>
> The symptom is a replica that fails, gets deleted, comes back, and fails in precisely the same way — repeatedly, deterministically, immune to every restart. That signature reads as "something in the cluster is broken," and engineers have spent days on it from that angle.
>
> It is not the cluster. The PVC survived, by design, because throwing away a stateful workload's data on a restart would be the worse failure by a wide margin. The state is the thing that is broken, and no amount of restarting will touch it. Go look at the data: exec into the replica and inspect what is on the volume, or mount the PVC into a debug Pod and read it there.
>
> The diagnostic tell that separates this from a genuine platform fault: **it is deterministic and it is confined to one ordinal.** A platform problem would not preferentially afflict `web-2` and leave `web-0` and `web-1` untouched across repeated rescheduling.

### Peers that find each other by name

The third difference is discovery. A StatefulSet uses a headless Service to give each Pod its own DNS name *[cross-bearing: see Ch 9 §5 — when you don't want a single address]*, and the form is `$(podname).$(governing service domain)` — for example `web-0.nginx.default.svc.cluster.local` [source: k8s-docs-statefulset-2026-08-24]. Replicas use these names to find each other: a database forming a cluster, a queue electing a leader, a cache building a ring.

That creates failure modes a ClusterIP workload never sees. If `web-1` cannot resolve `web-2`'s name, the peer relationship fails while both Pods look perfectly healthy from outside. And there is a genuine timing trap here, which the docs call out directly: *"Depending on how DNS is configured in your cluster, you may not be able to look up the DNS name for a newly-run Pod immediately. This behavior can occur when other clients in the cluster have already sent queries for the hostname of the Pod before it was created. Negative caching (normal in DNS) means that the results of previous failed lookups are remembered and reused, even after the Pod is running, for at least a few seconds."* [source: k8s-docs-statefulset-2026-08-24]

So a peer that came up, failed to resolve a sibling that did not exist yet, cached the negative result, and gave up is a real and reproducible failure that has nothing to do with your code and everything to do with startup ordering. The diagnostic move is to resolve the peer names from inside a replica and see what comes back:

```
kubectl exec -it web-1 -- nslookup web-2.nginx
```

> 🪝 **Snag:** A headless Service is required for a StatefulSet's network identity, and **you are responsible for creating it** — *"StatefulSets currently require a Headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service"* [source: k8s-docs-statefulset-2026-08-24]. Which means a `serviceName` pointing at a Service nobody created leaves you with Pods that run and cannot find each other, and nothing in a Pod's own status says why.

The unifying point across all three: for a StatefulSet, "which replica" is a question you have to answer before any of the other four questions mean anything.

---

## 🟡 §7 — Before You Ship It

The fastest debugging loop is the one that runs on your own machine, where you have a debugger, an IDE, and a rebuild that takes two seconds instead of a container build and a rollout.

The judgment call is knowing when that loop is worth building and when the reproduction is worthless before you start.

### The dividing line

Some things about your application exist only in the cluster. Not "are easier in the cluster" — exist only there, and cannot be reproduced locally by definition:

- **Cluster-supplied identity.** The ServiceAccount token projected into the Pod, and everything it authorizes *[cross-bearing: see Ch 12 §2 — who you are]*.
- **Cluster DNS.** Any name resolution through `svc.cluster.local`, including peer discovery.
- **Injected configuration.** ConfigMaps and Secrets mounted or projected into the container. You can copy the values locally, but you are then testing a copy, and if the bug is that the value *isn't what you think*, you have just reproduced your own misunderstanding.
- **Admission mutation.** Anything a mutating webhook or a sidecar injector added to your Pod after you submitted it. Your local process was never mutated *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*.
- **Service routing.** Everything in §4. A local process is not behind a Service, has no selector, and appears in no endpoint list.

Everything else — your business logic, your parsing, your request handling, your math — usually reproduces locally just fine, and reproducing it there is much faster than reproducing it in a cluster.

> ⚓ **Worth Securing:** Before you build a local reproduction, ask one question: *does the failing behavior depend on anything the cluster supplies?* If yes, a local reproduction will either fail to reproduce the bug or reproduce a different one, and either outcome is worse than not trying, because both are misleading. That question takes ten seconds and routinely saves an afternoon.

### The pattern that resolves it

There is a third option between "reproduce it locally" and "debug it in the cluster," and it is the one worth knowing by shape: **proxy a local process into the cluster, so that your code runs on your machine with your debugger attached, while seeing the cluster's real dependencies.**

The Kubernetes documentation describes the motivation exactly: *"Kubernetes applications usually consist of multiple, separate services, each running in its own container. Developing and debugging these services on a remote Kubernetes cluster can be cumbersome, requiring you to get a shell on a running container in order to run debugging tools."* [source: k8s-docs-local-debugging-telepresence-2026-08-31] The tool the docs walk through for this is **Telepresence**, described as *"a tool to ease the process of developing and debugging services locally while proxying the service to a remote Kubernetes cluster,"* which *"allows you to use custom tools, such as a debugger and IDE, for a local service and provides the service full access to ConfigMap, secrets, and the services running on the remote cluster."* [source: k8s-docs-local-debugging-telepresence-2026-08-31]

That last clause is the whole pattern in one line: your process, their cluster's dependencies. The list above stops being a list of things you cannot reproduce, because you are not reproducing them. You are using the real ones.

Telepresence is one instance of the pattern and the one the Kubernetes docs happen to document. The tooling in this space changes; the pattern does not. Learn the shape — a local process, proxied into the cluster's network and configuration — and you will recognize whichever tool is current when you need one.

That closes the practical arc. Four questions, five tools, one boundary, and one thing left to say about why the boundary was the point all along.

---

## ☆ Taking Your Bearings #2 — Reachability, Identity, and What a Laptop Can't Reproduce

Eight questions on §4 through §7. Three of them reach back into earlier chapters.

**1.** `kubectl get endpointslices -l kubernetes.io/service-name=api` returns a slice with three endpoints, every one of them showing `ready: false`. `kubectl get pods -l app=api` returns three Pods, all `Running`, all `0/1 READY`. What is the cause?

- A) A selector/label mismatch between the Service and the Pod template
- B) Readiness is disqualifying every endpoint behind the Service
- C) A `port`/`targetPort` mismatch on the Service
- D) The EndpointSlice controller has failed

**2.** `[retrieval: ch9]` A Service is defined with `port: 80` and `targetPort: 8080`. Which port must the container inside the Pod be listening on?

- A) 80
- B) 8080
- C) Either — Kubernetes tries both
- D) Neither; the container port is set by `containerPort` and is independent of the Service

**3.** You port-forward directly to a Pod behind a failing Service and the application responds correctly. What have you established?

- A) The application is working, so the incident is resolved
- B) The application serves correctly, and the fault lies somewhere on the Service path
- C) The Service is correctly configured but the Pod is unhealthy
- D) Nothing — port-forward and the Service path are equivalent

**4.** `[retrieval: ch5]` A Pod is `Running` with a restart count of 0, and its readiness probe is failing. What is the state of its liveness probe, and what does that combination mean for traffic?

- A) Liveness must also be failing; the container will be restarted shortly
- B) Liveness is passing (or absent) — the container is not restarted, but it receives no Service traffic
- C) Liveness is irrelevant to readiness; the Pod receives traffic normally
- D) Readiness failure forces liveness failure after the failure threshold

**5.** A three-replica StatefulSet has one failing Pod, `db-1`. You delete it. The controller recreates `db-1`, which fails identically. You delete it twice more with the same result. What is the most likely cause?

- A) A node-level fault on whichever node `db-1` keeps landing on
- B) Corrupt or unexpected state on `db-1`'s PersistentVolumeClaim, which survives every deletion
- C) The StatefulSet's image is broken and needs to be repulled
- D) A validating admission webhook is rejecting `db-1` specifically

**6.** `[retrieval: ch11]` Chapter 11 taught what happens to a StatefulSet's PersistentVolumeClaim when a replica is deleted (`whenDeleted`) or scaled away (`whenScaled`). What is the default retention policy for each case?

- A) `Delete` for both
- B) `Retain` for both
- C) `Retain` for `whenDeleted`, `Delete` for `whenScaled`
- D) There is no default; the field must be set explicitly

**7.** A StatefulSet's Pods run normally, but the replicas cannot discover each other and the cluster never forms. All Pods are `Running` and `Ready`, and they have been up for two hours. What should you check first?

- A) DNS negative caching from lookups issued before the peers existed
- B) The headless Service named by `serviceName`, and whether per-Pod DNS names resolve
- C) The `port`/`targetPort` pairing on the workload's ClusterIP Service
- D) The PersistentVolumeClaims for each ordinal

**8.** Which of these is genuinely reproducible on a laptop, without any cluster or proxy?

- A) A ServiceAccount token's permissions against the API server
- B) A parsing error in the application's handling of a malformed request body
- C) A Service selector that fails to match its Pods
- D) Peer discovery through headless-Service DNS names

---

**Answers with Explanations:**

**1 — B.** The slice holds three endpoints, so the selector matched; a match failure leaves the slice empty, not populated with unready entries [source: k8s-docs-endpointslices-2026-08-24]. `ready: false` across the board, matching `0/1 READY`, means readiness is disqualifying all three. **A** is wrong — Pods were returned by the label query and the slice isn't empty. **C** is wrong — a port mismatch leaves endpoints ready and fails further downstream; it can't mark an endpoint not-ready. **D** is wrong — the controller found the Pods and reported their condition faithfully. That's it working, not failing.

**2 — B.** `targetPort` is where the Service delivers traffic, so the container must listen on 8080; `port: 80` is only what clients use to reach the Service *[cross-bearing: Ch 9 §3]*. **A** inverts the two. **C** is wrong — there's no fallback. **D** is the trap: `containerPort` is informational, but `targetPort` is not independent of where the container listens — if they disagree, the request fails.

**3 — B.** Port-forward and the Service path share only the Pod. A correct response proves the process itself is healthy and pushes every remaining suspect onto the Service path. **A** is wrong — users travel the Service path, which you just proved is broken. **C** inverts the finding. **D** is wrong — the paths differ almost entirely, which is exactly what makes the test useful.

**4 — B.** A restart count of 0 rules out a failing liveness probe, since that would restart the container and increment the count. Liveness is passing or absent; readiness independently withholds the Pod from Service traffic *[cross-bearing: Ch 5 §7]*. **A** is wrong — restarts and the zero count rule it out directly. **C** is wrong — readiness gates whether a Pod is a valid target at all. **D** is wrong — neither probe's result influences the other's.

**5 — B.** The PVC follows the ordinal and survives Pod deletion by default [source: k8s-docs-statefulset-storage-2026-08-25], so recreating `db-1` reattaches the same volume with the same contents — a state-caused failure reproduces exactly, every time. **A** is wrong: a node fault wouldn't follow one ordinal across reschedules. **C** is wrong: a broken image would fail all three replicas, since they share a template. **D** is wrong: an admission rejection would block creation entirely — a different signature, and one that doesn't discriminate by ordinal.

**6 — B.** `Retain` for both [source: k8s-docs-statefulset-storage-2026-08-25] — exactly why deleting a replica doesn't clear its storage, and why question 5's failure survives repeated deletions. **A** would be a dangerous default: silent data loss on scale-down. **C** is a real configuration some teams choose, but it isn't the default — assume it and you'll misdiagnose question 5. **D** is wrong; the field has documented defaults.

**7 — B.** Peer discovery runs on per-Pod DNS names from the headless Service named in `serviceName`, which you're responsible for creating yourself [source: k8s-docs-statefulset-2026-08-24]. Missing or misnamed, the Pods run fine and simply never find each other. **A** is a real failure, but negative caching clears in "at least a few seconds" [source: k8s-docs-statefulset-2026-08-24] — the stem says two hours; that's structural, not timing. **C** is wrong — this is Pod-to-Pod traffic by individual name, not client traffic through a ClusterIP. **D** is wrong — a storage fault shows as a replica failing, not as healthy replicas unable to see each other.

**8 — B.** Parsing logic runs on your code and your input, with no cluster dependency anywhere in the path. **A, C, and D** all depend on something only a cluster supplies — API-server authorization, real Pod labels for selection, and cluster DNS, respectively.

---

**How'd You Do?**

**If you scored 0–3:** Re-read **§4**, **§6**, and **Chapter 9 §4** ("the list behind the name") — most misses at this checkpoint trace back to that chapter's model, not this one's. If question 6 was among the misses, add **Chapter 11 §6** on the retention policy.

**If you scored 4–6:** Re-read the why-wrong for whatever you missed, and check whether it clusters around reachability (1–4) or identity, storage, and reproduction (5–8) — the two halves fail for different reasons.

---

**Checkpoint: You've Now Mastered**

✓ Reading an EndpointSlice, and what "no ready endpoints" actually means
✓ Telling the two causes apart from the slice itself — empty means selector, not-ready means readiness
✓ Keeping upstream breaks (nothing ready) separate from downstream ones (ready endpoints, failed request)
✓ Using `port-forward` as an elimination step rather than a verdict
✓ Asking "which replica" before asking anything else about a StatefulSet
✓ The surviving-PVC signature, and why it impersonates a platform fault
✓ Headless-Service peer DNS as a failure surface that ClusterIP workloads never have
✓ Which failures a local reproduction can and cannot reach, and the proxy pattern for the rest

🏆 **Safe Harbor reached** — the practical material of this chapter is behind you. One section remains, and it is about what the last two chapters were actually for.

🗺️ Chart → **🌊 Passage** → 🌅 Dawn

---

## ☀️ §8 — Mine, or the Platform's

Here is the thing that has been true since Chapter 13 opened and has not been said outright until now.

These were never two chapters about two subjects. **The boundary is the method.**

Chapter 13 taught you to read the phase first, and the phase's last and most valuable answer, the one it works toward, is *"this is no longer mine."* Every signature in that chapter was a way of narrowing until the platform's contribution was fully accounted for. Chapter 16 taught you four questions, and their real function is not to find the bug either. It is to keep narrowing until the bug has nowhere left to be.

Same move. Different altitude.

<!-- FIGURE: ch16-zenith-mine-or-the-platforms -->
![A symmetrical diagram divided by a heavy vertical line. On the left, platform scope from Chapter 13: phase, then conditions, then events, then logs, then node. On the right, application scope from Chapter 16: is it running, is it healthy, is it reachable, is it configured, and which replica. Below each column, a long arrow points inward toward the center line, each labeled narrowing. At the center, the caption reads: the boundary, this line is the method.](figures/ch16-zenith-mine-or-the-platforms.svg)

<!-- ASCII-FALLBACK
```
   PLATFORM SCOPE                    │                 APPLICATION SCOPE
   (Ch 13)                           │                 (Ch 16)
                                     │
   phase ──▶ conditions ──▶ events   │   running? ──▶ healthy? ──▶ reachable?
        ──▶ logs ──▶ node            │        ──▶ configured? ──▶ which replica?
                                     │
              ─────────────────────▶ │ ◀─────────────────────
                   narrowing         │        narrowing
                                     │
                            THE BOUNDARY
                    ( this line is the method )
```
-->

<!-- AUTHOR-REVIEW: this anchor does not match the contract's `ch{NN}-fig{MM}-{slug}` pattern — it carries no `fig{MM}` segment. Preserved verbatim because it is the join key into image-specs. If renamed (suggested: `ch16-fig06-mine-or-the-platforms`), the draft anchor and the image-specs entry must change in the same commit or the join breaks. Author's call. Note also that document order runs fig01 → fig05 → fig02 → fig04 → fig03 → zenith; no numbers are missing or duplicated, but any consumer assuming anchor number equals document position will mis-order them. -->

Look at what each half of the arc did with its tools. Chapter 13's tools — `describe`, `events`, `logs --previous`, the node conditions — all answer questions about whether the cluster kept its promises. This chapter's tools — `exec`, `debug`, `port-forward`, `get endpointslices` — all answer questions about whether *you* kept yours. Neither set can answer the other's questions, and the reason the tools were split across two chapters is that the questions are split across one line.

The practitioner move is not knowing more commands. It is placing a failure on the correct side of that line quickly, and then staying on that side until the evidence moves you. Ninety seconds of scope triage saves an afternoon of confidently investigating the wrong half, and an engineer who does that reliably is doing the thing that separates someone who works with Kubernetes from someone who has read about it.

This is a shape you have met before in this book: narrowing by elimination, applied until only one candidate is left. A fix taken on two landmarks is worth more than a confident guess made from one. What is different here is that the narrowing crosses an ownership boundary, which means the last step is not "I found it" but "I know whose it is." On somebody else's cluster, those are equally valuable outcomes, and knowing which one you have reached, and being able to show your work for it, is what makes you good to work with.

The chapter title is "Your Application, Their Cluster." Both halves are true at once, permanently, and the whole skill is knowing which half you are standing on.

---

## Exam Alert! 🚨

**High-Priority Topics:**

1. **Which verb answers which question.** This is the shape this book organizes the competency around. `logs` for what it said. `exec` for what it can see. `debug` for when there is nothing to exec into. `port-forward` for where the break is. `describe service` and `get endpointslices` for whether anything is even selected. You are being tested on the mapping, not on flag syntax.

2. **Ephemeral containers exist because a Pod's container list is immutable.** That single fact explains the entire mechanism — why it needs a dedicated API handler, why `kubectl edit` cannot do it, why the container cannot be removed once added [source: k8s-docs-ephemeral-containers-concept-2026-08-31].

3. **`kubectl debug` has three shapes.** Inject into the running Pod; `--copy-to` a copy; `node/` for the host. Each answers a different question and they are not interchangeable.

4. **No ready endpoints has two causes** — selector mismatch, or Pods not Ready — and they live in two different files [source: k8s-docs-debug-pods-2026-08-23]. The slice distinguishes them: a mismatch leaves it empty, while a readiness failure leaves the endpoints in place and marked not ready [source: k8s-docs-endpointslices-2026-08-24].

---

## Practice Questions

**1.** An application's Pod is `Running`, `1/1 Ready`, has zero restarts, and sits on a node reporting no adverse conditions. The application returns stale data. Three other Deployments in the namespace are unaffected. Which is the correct first move?

A) File a platform ticket; every application-side signal is clean
B) Treat it as application scope and begin the four triage questions
C) Delete the Pod to force a reschedule onto a different node
D) Check node conditions across the whole cluster before deciding

**2.** You are on a cluster where you cannot list nodes or read events in `kube-system`. A single workload of yours is failing while everything else in your namespace runs normally. What does §1's addition to the scope test say you should do?

A) Escalate immediately, because the scope test cannot be completed without node access
B) Make the application-scope case from the evidence you can gather, and be ready to show it if you later need the platform team
C) Assume platform scope by default, since the unverifiable half is the platform's
D) Request node access before starting any diagnosis

**3.** A Pod reports `STATUS: Init:2/4`. What is true?

A) Two init containers have completed and the third is running or failing
B) Two of four app containers have started
C) Two init containers failed and two remain
D) The Pod is `Running` with two containers ready

**4.** An init container runs `git clone` into a mounted volume. The workload deploys successfully. After the Pod is evicted and rescheduled, it will not start. What is the most likely cause?

A) The volume failed to reattach on the new node
B) The init container is not idempotent — the clone target already exists
C) The git repository became unreachable
D) Init containers are skipped on rescheduled Pods, so setup never ran

**5.** A Pod sits at `Init:0/1` for twenty minutes. No errors, no restarts, and the init container's log reads `waiting for service endpoint...`. The Service it is waiting on selects only this workload's Pods. What is happening?

A) A DNS failure is preventing the lookup
B) An ordering deadlock — the init container waits for an endpoint that only this Pod could provide
C) The init container image is being pulled slowly
D) The readiness probe on the init container is failing

**6.** You need to inspect the filesystem of a running container built from a distroless image. Which is correct?

A) `kubectl exec -it <pod> -- /bin/sh`
B) `kubectl debug -it <pod> --image=busybox --target=<container>`
C) `kubectl logs <pod> --previous`
D) `kubectl cp <pod>:/ ./local-copy`

**7.** Which statement about ephemeral containers is correct?

A) They may define a readinessProbe to report when the debug tooling is ready
B) They may set resource requests so the debug session is guaranteed CPU
C) They cannot be removed or changed once added to a Pod
D) They are automatically restarted if the debug process exits

**8.** An application container crashes immediately on startup, before you can exec into it. Which `kubectl debug` shape is designed for this case?

A) An ephemeral container injected into the running Pod
B) `--copy-to`, creating a copy of the Pod with the entrypoint changed
C) `debug node/<node>` to inspect the host
D) None — a crashing container cannot be debugged with `kubectl debug`

**9.** You run `kubectl debug` in a namespace enforcing the `restricted` Pod Security Standard, using a debug image that runs as root. The command is refused. You have verified you hold RBAC permission for the operation. What happened?

A) RBAC permissions do not cover the ephemeral containers subresource separately
B) The debug container was rejected by admission, because it is a container and must meet the namespace's enforced standard
C) `kubectl debug` is disabled in namespaces with Pod Security Admission enabled
D) The node lacked capacity for an additional container

**10.** `kubectl get endpointslices -l kubernetes.io/service-name=web` returns a slice with zero endpoints. `kubectl get pods -l <the Service's selector>` returns no Pods at all. What is the cause?

A) The Pods are running but not Ready
B) The Service's selector does not match any Pod's labels
C) `targetPort` does not match the container's listening port
D) The EndpointSlice controller is not running

**11.** A Service's EndpointSlice holds three endpoints, all of them ready. Requests to the Service fail with connection refused. Which break point is most likely?

A) A selector/label mismatch
B) The client is resolving a DNS name that does not point at this Service
C) A `port`/`targetPort` mismatch delivering traffic to a closed port
D) The EndpointSlice controller has stopped reconciling

**12.** `[retrieval: ch9]` A Service `cache` in namespace `data` has three ready endpoints. A client Pod in namespace `web` calls `http://cache:6379` and gets nothing. What is the most likely cause?

A) The Service's Pods are not Ready
B) The short name resolves relative to the client's namespace, so `cache` resolves in `web`, not `data`
C) `port` and `targetPort` are mismatched
D) Redis requires a headless Service

**13.** `[retrieval: ch9]` A Service `web` declares `port: 80` and `targetPort: 80`. Requests through the Service fail. You run `kubectl port-forward pod/web-7f4d 8080:8080` and the application answers correctly on your local port 8080. What have you established?

A) The application is healthy and the Service is correctly configured
B) The container is listening on 8080, so the Service's `targetPort` of 80 delivers traffic to a closed port
C) The Pod is not Ready, so its endpoint was never a valid target
D) Nothing — port-forward and the Service path deliver traffic identically

**14.** `[retrieval: ch11]` A three-replica StatefulSet has one replica, `queue-0`, that fails on start. You delete it; the recreated `queue-0` fails identically. `queue-1` and `queue-2` are healthy. What should you investigate first?

A) The Pod template, since all replicas share it
B) The contents of `queue-0`'s PersistentVolumeClaim, which survived the deletion
C) The node `queue-0` was scheduled onto
D) The StatefulSet's image tag

**15.** A bug reproduces only in the cluster. The failing code path reads a config value mounted from a ConfigMap, and you suspect the mounted value differs from what the manifest declares. Which approach actually tests the hypothesis?

A) Copy the ConfigMap's declared value into a local environment variable and run the app locally
B) Exec into the running container and read the mounted file directly
C) Re-apply the ConfigMap and restart the Deployment
D) Reproduce in a local kind cluster using the same manifests

**16.** Three workloads owned by three different teams are all failing, and every one of them is on the same node; Pods rescheduled off that node recover immediately. You hold cluster-admin. Which move fits the evidence?

A) `kubectl debug <pod> --image=busybox --target=<container>` against one of the failing Pods
B) `kubectl debug <pod> --copy-to=<pod>-debug --image=ubuntu`
C) `kubectl debug node/<node> -it --image=ubuntu`
D) `kubectl port-forward` to one of the failing Pods

**17.** Two workloads have the same class of bug: a wrong value for a key their configuration depends on. Workload A's Pod is stuck at `Init:0/1`, its init container exiting non-zero and printing the offending key's name. Workload B's Pod is `Running`, `1/1 Ready`, and returns wrong answers. Which is the harder diagnosis, and why?

A) A — a Pod that will not start gives you nothing to inspect
B) B — the value was present and read cleanly, so nothing failed and no signal names the problem
C) Neither; both produce the same signature and the same diagnosis
D) A — an init container's logs are not retrievable until the Pod reaches `Running`

---

**Answers with Explanations:**

**1 — B.** Every element of the mechanical test resolves to application scope: running, ready, stable, confined to one workload, no adverse platform signal.

- **A is wrong** because "application-side signals are clean" is a misreading. Those signals are *platform* signals reporting on your workload, and their cleanliness is what hands the problem to you.
- **C is wrong** — deleting a Pod to see what happens is the reflex the four questions exist to replace. Stale data is not a placement problem, and you would have destroyed the state you needed to inspect.
- **D is wrong** because a fault confined to one workload is already answered by the scope test; a cluster-wide node sweep is effort spent on the half you have already eliminated.

**2 — B.** The addition is that the boundary is also a statement about what you can see, and the practical response is to build the application-scope case from available evidence.

- **A is wrong** — the test completes fine here. Confinement to one workload plus clean workload-level signals is sufficient.
- **C is wrong** and is the failure mode this guidance exists to prevent: defaulting to "must be the platform" whenever you cannot check something. That reasoning would make every fault platform-scope on a restricted cluster.
- **D is wrong** — waiting on an access request before diagnosing is how a fifteen-minute problem becomes a two-day one.

**3 — A.** `Init:N/M` counts *completed init containers* out of the total [source: k8s-docs-debug-init-containers-2026-09-04]. `Init:2/4` means two are done and the third is where your attention belongs.

- **B is wrong** — the counter refers to init containers only. App containers have not started; the Pod is still `Pending`.
- **C is wrong** — the status does not count failures, and a failing init container reports `Init:Error` or `Init:CrashLoopBackOff` instead.
- **D is wrong** — *"a Pod that is initializing is in the `Pending` state but should have a condition `Initialized` set to false"* [source: k8s-docs-init-containers-2026-08-24] *[cross-bearing: see Ch 5 §5 — Pod phase and container state]*.

**4 — B.** A clone into a directory that already contains a clone fails. Every init container runs again on every Pod start [source: k8s-docs-init-containers-2026-08-24], and the volume persisted across the reschedule, so the second run hits a populated target.

- **A is possible but is not the *most likely* given the stated sequence**, and the discriminator is available: a volume reattachment failure produces a Pod stuck on mounting with events saying so, not a Pod whose init container ran and exited non-zero.
- **C is possible in principle** but would have been equally likely on the first deploy. Nothing in the timeline points at the repository.
- **D is a factual error** — init containers run on every start, which is the entire reason B is the answer.

**5 — B.** The circular wait. The init container blocks until the Service has a ready endpoint; the Service cannot have one until this Pod's app container is ready; the app container cannot start until the init container exits. Perfectly stable, no error, waits indefinitely.

- **A is wrong** — a DNS failure produces resolution errors in the log, not a calm "waiting" message.
- **C is wrong** — an image pull in progress reports `Init:ImagePullBackOff` or a pulling event, and the init container's log would not exist yet *[cross-bearing: see Ch 13 §2 — pods that never start]*.
- **D is wrong** on its facts: regular init containers *"do not support the `lifecycle`, `livenessProbe`, `readinessProbe`, or `startupProbe` fields"* [source: k8s-docs-init-containers-2026-08-24].

**6 — B.** A distroless image has no shell to exec into, so the move is to inject an ephemeral container that *does* have tools, targeting the container you want to inspect [source: k8s-docs-ephemeral-containers-concept-2026-08-31].

- **A is wrong** — that is the command that fails, and the failure is why this whole section exists.
- **C is wrong** — `logs --previous` returns the previous container instance's output. Useful for a crash loop, useless for inspecting a filesystem.
- **D is wrong** for a reason worth carrying: `kubectl cp` copies files *out* of the container rather than giving you a live view of the running process, and it depends on tooling inside the image that a distroless image does not have — the reference is explicit: *"Requires that the 'tar' binary is present in your container image. If 'tar' is not present, 'kubectl cp' will fail."* [source: k8s-docs-kubectl-cp-reference-2026-09-04]

**7 — C.** *"Like regular containers, you may not change or remove an ephemeral container after you have added it to a Pod."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

- **A is wrong** — probes are explicitly disallowed, because ephemeral containers may not have ports [source: k8s-docs-ephemeral-containers-concept-2026-08-31].
- **B is wrong** — *"Pod resource allocations are immutable, so setting `resources` is disallowed."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]
- **D is wrong** — they *"will never be automatically restarted"* [source: k8s-docs-ephemeral-containers-concept-2026-08-31], which is one of the reasons they are unsuitable for building applications.

**8 — B.** *"you can't run `kubectl exec` to troubleshoot your container if your container image does not include a shell or if your application crashes on startup. In these situations you can use `kubectl debug` to create a copy of the Pod with configuration values changed to aid debugging."* [source: k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31] Copy it, replace the entrypoint, and now the container sits still.

- **A is wrong** — an ephemeral container needs a Pod to attach to, and while the Pod exists, the *target container* is gone again before you can look at it.
- **C is wrong** — the node is not the problem, and that shape steps across the scope boundary for no reason.
- **D is wrong** — this is exactly the case `--copy-to` was built for.

**9 — B.** An ephemeral container is a container in that namespace, and admission enforces the namespace's standard against it; the Standards' restricted fields name `spec.ephemeralContainers[*].securityContext.runAsNonRoot` alongside the regular and init container fields [source: k8s-docs-pod-security-standards-2026-09-04]. A root-running debug image has asked for more than `restricted` permits *[cross-bearing: see Ch 12 §6 — three levels, three modes]*.

- **A is wrong** — the stem states RBAC is verified, and the refusal comes from a later gate. Authentication, then authorization, then admission *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*.
- **C is wrong** — a debug container that *meets* the standard is admitted normally. That is what the profile mechanism is for: a `--profile` is a preset for how much privilege the debug container asks for, and asking for less is what gets you through the gate.
- **D is wrong** — a capacity problem produces a scheduling failure with a distinct signature, not an admission refusal.

**10 — B.** The label query returned nothing, which means no Pod carries the labels the Service selects. Nothing matched, so nothing was placed in the slice.

- **A is wrong,** and this is the discriminator the section is built on. Not-ready Pods would still *appear* in a label query and would still be *in the slice*, marked not ready [source: k8s-docs-endpointslices-2026-08-24]. Zero endpoints alongside zero matching Pods is the selector's signature, not readiness'.
- **C is wrong** — a port mismatch does not affect slice membership at all. It is downstream of readiness.
- **D is wrong** and is the reflexive platform-blame answer. The empty slice is the controller reporting correctly that nothing matched.

**11 — C.** Three ready endpoints means selection and readiness are both fine. The remaining candidate on that path is the port pairing: traffic arriving at a port nothing is bound to.

- **A is wrong** — a selector mismatch leaves the slice with no endpoints, and the stem says there are three.
- **B is wrong,** and it is the option that survives the stem's facts longest, which is why it is here. But the stem places you at the Service you are querying and reading endpoints from; a name resolving somewhere else means you never reached *this* Service, and the endpoints you are looking at would be irrelevant rather than informative. Break 4 is a failure to arrive, not a failure at the destination.
- **D is wrong** — a stalled controller would leave a stale or empty slice, not a correct one.

**12 — B.** A short name resolves through the client's search domains, which include the client's own namespace [source: k8s-docs-dns-pod-service-2026-08-23]. From `web`, `cache` means `cache.web.svc.cluster.local`, which is not the Service in question *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*.

- **A is wrong** — the stem states three ready endpoints, ruling readiness out.
- **C is wrong** — a port mismatch produces a connection failure against a real target, a different signature from a name that resolves elsewhere or not at all.
- **D is wrong** — a headless Service is for per-Pod DNS identity; a Redis client reaching a single ClusterIP Service needs no such thing.

**13 — B.** The port numbers are the whole story. The container answers on 8080, so 8080 is what it binds; the Service declares `targetPort: 80`, so every request through the Service is delivered to a closed port. Read the Service's declared `targetPort` with `kubectl describe service web` and compare it against the port you just forwarded to successfully. When those two numbers disagree and the forward works, you are looking at break 3 *[cross-bearing: see Ch 9 §3 — four ways to be reachable]*.

- **A is wrong,** and it is the §5 trap in its most seductive form: a successful port-forward feels like an all-clear. Users travel the Service path, which you have just shown is broken.
- **C is wrong** — readiness would keep the Pod out of the Service path but has no effect on a port-forward, so it cannot explain a working forward. It also does not explain the port asymmetry, which is the actual evidence in the stem.
- **D is wrong** — port-forward is an API-server operation on the `pods/portforward` subresource [source: k8s-docs-port-forward-authorization-2026-08-31] and does not travel the Service path at all. If the two were equivalent, both would have failed.

**14 — B.** The PVC survives Pod deletion by default and reattaches to the recreated replica [source: k8s-docs-statefulset-storage-2026-08-25]. Deterministic failure confined to one ordinal, immune to restart, is the surviving-state signature.

- **A is wrong** — a Pod template problem would fail all three replicas, and two are healthy.
- **C is wrong** — the replacement Pod is not guaranteed to land on the same node, so a node fault would not track the ordinal so faithfully.
- **D is wrong** — the image is shared by all three replicas.

**15 — B.** The hypothesis is that the mounted value differs from the declared one. The only way to test it is to read what is actually mounted, in the running container.

- **A is wrong** and is the most instructive distractor: copying the *declared* value locally tests your assumption rather than the system. If the declared and mounted values differ, this reproduces the wrong one and passes.
- **C is wrong** — restarting may make the symptom vanish without ever telling you what was wrong, which means the next occurrence starts from zero.
- **D is wrong** for the same reason as A, at larger scale: a local cluster with the same manifests reproduces what the manifests *say*, not what the target cluster's mount actually produced.

**16 — C.** The scope test has already spoken: the fault is not confined to one workload, and it tracks a machine rather than an application *[cross-bearing: see Ch 13 §1 — whose problem is this, and what to read first]*. `debug node/` is the shape built for the host, and cluster-admin is what makes it available to you.

- **A is wrong** — an ephemeral container inspects one container's view of one Pod. Three teams' workloads failing together is the signature that sends you across the boundary, not deeper into one of them.
- **B is wrong** for the same reason, with an added defect: the copy may be scheduled somewhere else entirely, taking it away from the only thing the evidence implicates.
- **D is wrong** — `port-forward` is an application-scope elimination step. It can tell you whether a Service path is broken; it says nothing about a host.

*Worth noticing about this question: the correct answer is the one this chapter spends a section arguing is out of scope. That is not a contradiction. `debug node/` is correct here precisely because the evidence has already moved you across the line, and on a cluster you did not own, the equally correct move would be handing the same evidence to whoever does *[cross-bearing: see Ch 13 §5 — when the node is the problem]*.*

**17 — B.** Same class of bug, two entirely different signatures, which is exactly why this chapter answers "is it configured" in two separate places. Workload A failed loudly and named the problem. Workload B read a value that was present and well-formed and simply wrong, so nothing errored, no probe fired, and no status string is going to tell you anything.

- **A is wrong,** and it inverts the difficulty. A failing init container is the *easy* case: it exits non-zero, prints the reason, and `kubectl logs <pod> -c <init-name>` retrieves it [source: k8s-docs-debug-init-containers-2026-09-04].
- **C is wrong** — if both produced the same signature, §2 and §3 would be one section. The whole doubling in §1's table exists because they do not.
- **D is wrong** on its facts: an init container's logs are readable with `-c` while the Pod is still `Pending`, which is the entire point of that flag in this context [source: k8s-docs-debug-init-containers-2026-09-04].

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| The scope boundary | Running + ready + confined to one workload = yours. On someone else's cluster, it is also a statement about what you can see. |
| The four questions | Running (§2), healthy/configured (§3), reachable (§4→§5), and for StatefulSets, *which replica* (§6). |
| Init container logs | `kubectl logs <pod> -c <init-name>`. The plain form returns nothing useful and the nothing is misleading. |
| The three init failures | Ordering deadlock (waits indefinitely, no error) · non-idempotency (fails only on restart) · config error (exits loudly, tells you why). |
| A failing init container is retried | The kubelet restarts it until it succeeds — unless `restartPolicy: Never`, in which case the Pod is treated as failed. That is why `Init:CrashLoopBackOff` exists. |
| Termination messages | A container can write a one-line fatal reason to `/dev/termination-log`; Kubernetes surfaces it in Pod status, so the failure stays legible from `describe` alone. |
| `exec` | Answers "what did the *process* actually read," which is where the manifest and reality diverge. |
| The field that never arrived | A misnested or misspelled key is silently dropped at apply. `exec` cannot find what the server never stored — read the object back with `-o yaml` and compare it against your file. |
| The distroless problem | No shell in the image means no shell in the container. Hardening win, debugging cost. |
| Ephemeral containers | Exist because you cannot add a container to a running Pod. No resources, no probes, no restart, no removal. |
| `kubectl debug`'s three shapes | Inject (what does it see now?) · `--copy-to` (what if I changed something?) · `node/` (is the machine the problem? — platform scope). |
| `--copy-to` | Makes a copy. The original is untouched, and that is the feature. |
| Debug profiles | A preset for how much privilege the debug container asks for. Asking for more than the namespace enforces is what gets it refused at admission. |
| No ready endpoints | Two causes, two files — and the slice separates them: **empty** means the selector matched nothing; **present but not ready** means readiness. |
| Ready endpoints, failed request | Not a selection problem. Look at `port` vs `targetPort` — `targetPort` is the one the container listens on. |
| `port-forward` | Bypasses the Service path via the API server. A working forward beside a failing Service *localizes* the fault; it does not clear the app. |
| StatefulSet debugging | Ask "which ordinal" first. The PVC survives deletion by default, so a bad write is immune to restarts and impersonates a platform fault. |
| Headless-Service peer DNS | You create the headless Service, not the controller. Missing one means healthy Pods that cannot find each other. |
| Local reproduction | Anything cluster-supplied — identity, DNS, injected config, admission mutation, Service routing — is not reproducible locally. Everything else usually is. |

---

## The Voyage Ahead

Part IV closes here, and with it the two-chapter arc that began when the platform handed you back your own problem.

You now have both halves of a single skill: reading a cluster's report on your workload, and reading your workload once the cluster has nothing left to say. That skill is worth more than any individual command in either chapter, because commands change between releases and the boundary does not.

What comes next is a change of altitude. Part V steps back from the failing workload in front of you to the ecosystem the workload lives in: what "cloud native" actually names, who decides what belongs under that word, and the four places Kubernetes deliberately lets somebody else's software in. Chapter 17 finally answers the question Chapter 1 planted and left standing on purpose, and it collects a set of interfaces you have been meeting one at a time since Chapter 2 without ever seeing them side by side.

After that, the instruments. You have spent this chapter finding out what went wrong *after* someone told you something was wrong. Chapter 18 is about the systems that tell you first.

> *"The boundary is not a wall between two crews. It is the line on the chart that tells each of them where to look."*

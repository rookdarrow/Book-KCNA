---
chapter: 6
chapter_type: "content"
title: "Fleets, Not Vessels"
subtitle: "Nobody sails one Pod"
exam_domain: "Kubernetes Fundamentals (competency: Kubernetes Core Concepts)"
domain_weight_pct: 6
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band for this chapter:
#-- "standard-plus" - 6 points, but this is the control loop's first
#-- instantiation and it closes Part II's trunk. Planning signal only,
#-- NOT a target.
#--
#-- WARNING - SECTION NUMBERING IS CONTESTED. Seven published cross-bearings
#-- point into this chapter. Five agree; three collide on the same number.
#--   chapter-04 line 269  -> *[see Ch 6 §1 - Deployments and ReplicaSets]*
#--   chapter-05 line 553  -> *[see Ch 6 §1 - the resource that holds the surviving intent]*
#--   chapter-05 line 1455 -> *[see Ch 6 §1 - Deployments, ReplicaSets, and the Pod template]*
#--   chapter-05 line 860  -> *[see Ch 6 §4 - what makes a rolling update safe]*
#--   chapter-04 line 688  -> *[see Ch 6 §3 - a controller's selector and the Pods it owns]*
#--   chapter-01 line 435  -> *[see Ch 6 §3 - StatefulSets and stable identity]*   <-- COLLIDES
#--   chapter-02 line 600  -> *[see Ch 6 §3 - CRDs and extending the API]*         <-- COLLIDES
#-- §1, §3 and §4 below honor the first five. The two collisions cannot be
#-- honored by any numbering; they require a two-token edit in shipped text.
#-- See § Open questions #1 for the exact edits and the reasoning.
#-- Do not renumber without re-checking all seven.
sections:
  - name: "The Resource That Holds the Intent"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig01-deployment-replicaset-pod-ownership"
    checkpoint_after: false
  - name: "A Loop You Can Watch Working"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "How a Controller Knows Its Own"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Changing the Fleet Under Way"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig02-rolling-update-maxsurge-maxunavailable"
    checkpoint_after: false
  #-- §4 also carries ch06-fig03-recreate-vs-rolling. The schema allows one
  #-- anchor per section; both are specified in § Required figures and both
  #-- appear in figures_planned. Do not drop fig03 on a schema technicality.
  - name: "Every Rollout Is a Revision"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "When Pods Are Not Interchangeable"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig05-statefulset-vs-deployment-identity"
    checkpoint_after: false
  - name: "One Per Node, and Work That Ends"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig04-workload-resource-decision-tree"
    checkpoint_after: false
  - name: "The Control Loop, Extended"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Nobody Sails One Pod"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-zenith-control-loop-instantiated"
    checkpoint_after: false

#-- Nine sections, matching Chapter 5's count. §2 and §7 are deliberately
#-- short. See § Open questions #9 for the fold options considered.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "keeping N copies of a process alive without watching a terminal - what has to be written down in advance"
    - "replacing a running service with a new version while it stays reachable"
    - "identifying a set of things by an explicit list of names versus by a property they share"
    - "a two-node database where the members are not interchangeable - what breaks if you swap them"
    - "running an agent on every machine in a fleet, including machines that do not exist yet"
    - "work that finishes versus work that is supposed to never finish - how an init system treats each"
    - "retrieval from Ch 3 - the two states a control loop compares, and what it does with the gap"
    - "retrieval from Ch 5 - a Pod's node dies; Ch 5 said it is not rescheduled, so what did it say happens"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 19 = 37. Bearings raised 10 -> 15 across 3
#-- checkpoints (5 + 5 + 5), matching the precedent set in Ch 3, Ch 4 and
#-- Ch 5, all of which shipped three checkpoints. See § Taking Your Bearings.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 19
  total_this_chapter: 42

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.1"]
  concepts:
    - "workload-resource"
    - "deployment"
    - "replicaset"
    - "replicationcontroller-legacy"
    - "pod-template"
    - "podtemplatespec"
    - "ownership-chain"
    - "owner-reference"
    - "controller-adoption"
    - "orphaning"
    - "cascading-deletion"
    - "replicas"
    - "desired-replica-count"
    - "manual-horizontal-scaling"
    - "horizontal-scaling"
    - "vertical-scaling"
    - "horizontalpodautoscaler"
    - "label-selector"
    - "matchlabels"
    - "matchexpressions"
    - "selector-template-agreement"
    - "overlapping-selectors"
    - "deployment-strategy"
    - "rolling-update"
    - "recreate-strategy"
    - "maxsurge"
    - "maxunavailable"
    - "minreadyseconds"
    - "readiness-gated-rollout"
    - "rollout"
    - "revision"
    - "rollout-history"
    - "rollback"
    - "revision-history-limit"
    - "pause-rollout"
    - "resume-rollout"
    - "stuck-rollout"
    - "statefulset"
    - "stable-pod-identity"
    - "pod-interchangeability"
    - "daemonset"
    - "node-local-facility"
    - "job"
    - "run-to-completion"
    - "cronjob"
    - "cronjob-schedule"
    - "custom-resource"
    - "customresourcedefinition"
    - "custom-controller"
    - "operator-pattern"
    - "declarative-api"
    - "dynamic-registration"
  commands:
    - "kubectl-get"
    - "kubectl-describe"
    - "kubectl-apply"
    - "kubectl-scale"
    - "kubectl-rollout-status"
    - "kubectl-rollout-history"
    - "kubectl-rollout-undo"
    - "kubectl-rollout-pause"
    - "kubectl-rollout-resume"
    - "kubectl-delete"

figures_planned:
  - "ch06-fig01-deployment-replicaset-pod-ownership"
  - "ch06-fig02-rolling-update-maxsurge-maxunavailable"
  - "ch06-fig03-recreate-vs-rolling"
  - "ch06-fig04-workload-resource-decision-tree"
  - "ch06-fig05-statefulset-vs-deployment-identity"
  - "ch06-zenith-control-loop-instantiated"
---

<!-- AUTHOR-REVIEW (pipeline): the Stage 3 draft for this chapter exceeded one `max_tokens` window and stdout capture kept only the final assistant message, leaving `draft-v1.md` truncated. The chapter was recovered by concatenating both assistant blocks from `.draft-v1.md.progress.log` (the seam is clean) and that reconstruction is what was voiced and revised here. The pipeline fix is to accumulate text across ALL assistant messages when `stop_reason == max_tokens`, not to re-draft. This will hit any chapter whose draft exceeds one window. -->

# Chapter 6: Fleets, Not Vessels
## *"Nobody sails one Pod"*

**Domain: Kubernetes Fundamentals — Kubernetes Core Concepts [source: cncf-kcna-curriculum-pdf-2026-08-23] | Estimated share of the exam: ~6% (authored allocation — CNCF publishes domain weights, not competency weights [source: cncf-kcna-curriculum-pdf-2026-08-23]; see front matter) 
**Complexity: Mixed | Novelty: Moderate | Prerequisites: Chapters 3, 4, 5**

<!-- AUTHOR-REVIEW: two disclosure items on the metadata line above. (1) The competency ID `D1.1` has been REMOVED. CNCF publishes four domain weights and twelve named competencies with no numbering and no sub-weights [source: cncf-kcna-curriculum-pdf-2026-08-23]; `D1.1` is a Lodestar-internal decomposition (declared as such at book-outline/domain-analysis.md:33) and must not read as a CNCF taxonomy ID in shipped text. (2) The ~6% figure is this book's authored allocation, not a published CNCF weight. Match the exact disclosure phrasing used in the metadata lines of Chapters 2–5 before this ships. -->

---

## Attention Budget

**Total time: ~2 hours | Recommended: split across two sessions**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 — The Resource That Holds the Intent | 10 min | Medium | Mid-session |
| §2 — A Loop You Can Watch Working | 7 min | Low | Anytime |
| §3 — How a Controller Knows Its Own | 12 min | Medium | Mid-session |
| ☆ Taking Your Bearings #1 | 5 min | Medium | After a brief pause |
| §4 — Changing the Fleet Under Way | 18 min | **High** | Peak attention |
| §5 — Every Rollout Is a Revision | 11 min | Medium | Peak attention |
| ☆ Taking Your Bearings #2 | 5 min | Medium | After a brief pause |
| §6 — When Pods Are Not Interchangeable | 9 min | Medium | Mid-session |
| §7 — One Per Node, and Work That Ends | 10 min | Low | Anytime |
| §8 — The Control Loop, Extended | 12 min | Medium-high | Peak attention |
| ☆ Taking Your Bearings #3 | 5 min | Medium | After a brief pause |
| §9 — Nobody Sails One Pod (the chapter's ☀️ Zenith) | 4 min | Low | Anytime |
| Exam Alert + Practice Questions | 25 min | Medium | Separate session |

**Attention Cost Key:**
- **Low:** concrete, familiar concepts. Study anytime.
- **Medium:** new concepts requiring focus. Study when alert.
- **High:** abstract or dense material with arithmetic. Study at peak attention.

**Recommended split point:** after ☆ Taking Your Bearings #2. Sections 1 through 5 are the Deployment arc from end to end. Sections 6 through 9 are the rest of the family and what the pattern turns into.

*If you only have 15 minutes: read §1, jump to the decision tree at the close of §7, then work ☆ Taking Your Bearings #3. That is the highest-leverage route through this chapter.*

---

> *"A standing order outlives the watch that received it. That is the whole reason you write it down."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before you read this chapter, work these eight. Your score tells you how to read. No shame attached to any score; the three tiers are three reading plans, not three grades. Every question here is answerable from Chapters 3 through 5 or from operational experience you already have. None of them require anything this chapter teaches.

1. You want three copies of a process running on a machine at all times. One of them dies at 3 a.m. What would have to be written down *in advance* for something else to restore it without waking you up?

2. You need to replace a running service with a new version while it stays reachable the entire time. Describe how you have done this, or how you would do it, with tools you already know.

3. There are two ways to identify a group of things: an explicit list of names, or a rule about a property they share. What does each approach cost you when the group changes while you are not looking?

4. A two-member database: one primary, one replica, each with its own data on disk. What actually breaks if you swap which machine is which? Hostnames, storage, and all.

5. A log-collection agent has to run on every machine in your fleet, including the machines that will be added next Tuesday. How would you express that requirement, as opposed to "run six copies"?

6. Your init system supervises two things: a web server that should never exit, and a nightly backup script that should exit. How does it treat them differently, and what does "healthy" mean for each?

7. **[retrieval: ch3]** A control loop compares two things and acts on the difference. Name both, and say what the loop does when they match.

8. **[retrieval: ch5]** A Pod's node dies. Chapter 5 was emphatic that the Pod is not rescheduled. What did it say happens instead, and what did it say was left unanswered?

<details>
<summary>Answers + reading strategy</summary>

1. **The count and the recipe.** Something has to know how many copies you wanted and what a copy looks like, or it cannot tell that one is missing or build a replacement. *Count it right if your answer named both — a quantity and a description.*

2. **Any overlap-based answer is correct.** Add new instances to a load-balancer pool before removing old ones; drain and swap one at a time; run two environments and flip DNS. The common shape is that old and new coexist for a window.

3. **A list is exact but goes stale;** you must maintain it by hand every time membership changes. **A rule stays current** but can silently capture things you did not intend, because you never enumerated what it would match. *Count it right if you named a cost on both sides.*

4. **Nearly everything.** Hostnames the replica uses to find the primary, the on-disk data each one expects to open, replication position, client connection strings. The two machines are not copies of each other. They hold different roles and different bytes. *Count it right if you named storage as well as naming.*

5. **Express it as a property of the machine, not as a number:** "one agent per host" rather than "six agents."

6. **The web server exiting is a failure; the backup script exiting is success.** For the web server, healthy means still running. For the backup, healthy means finished with a zero exit status and gone. *Count it right if you inverted the meaning of "exited" between the two.*

7. **Desired state and current state.** When they match, the loop does nothing, and keeps watching. Doing nothing is a valid output of a control loop, not a pause in it. *Count it right only if you named both states.*

8. **Chapter 5 said the Pod is replaced, not moved:** a new, near-identical Pod with a different UID. What it left unanswered was *who does the replacing.* That is the question this chapter opens on. *Count it right if you named the replacement and the open question.*

**If you got 6 or more right:** skim. Read the ★ Fixed Points, the ⚠ Navigational Hazards blocks, and §4 in full. The two rolling-update bounds and their defaults are the easiest pair in this chapter to get backwards. Then work all three ☆ Taking Your Bearings checkpoints.

**If you got 3 to 5 right:** read at normal pace. This chapter is calibrated for you. Do not skip §3; it is short and everything after it depends on it.

**If you got 0 to 2 right:** read carefully, and take the recommended split after ☆ Taking Your Bearings #2. **If questions 7 and 8 were among your misses, re-read Chapter 3 §6 and Chapter 5 §4 before you start §2.** Those two sections are the debts this chapter collects, and §2 will read as a vocabulary drill without them.

</details>

---

## Why This Chapter Matters

Chapter 5 ended on a question it refused to answer: if Pods are designed to be replaced rather than repaired, who does the replacing? Here is the answer, and it is stranger than "a thing called a Deployment." Kubernetes has no special replacement machinery at all. It has the same control loop you met in Chapter 3, handed a count to hold and a template to copy from. Rolling updates, rollbacks, one-agent-per-node, scheduled batch work, and the operator that runs your database are all that one loop with different desired state plugged into it. This chapter has fewer ideas in it than its table of contents suggests. By §9 you will be able to see that.

What actually changes here is what kind of person you are at a terminal. Chapter 5 made you someone who can read what infrastructure is telling you. This chapter makes you someone who states what should be true and hands the system responsibility for it. That is the real difference between someone new to Kubernetes and someone who isn't. Newcomers reach for the Pod, then for a script that recreates the Pod, then for a cron entry that checks whether the script ran. Practitioners write down the count and the template and go home. That is a standing order: set down once, carried out by whoever has the watch, long after the person who wrote it has gone below. If you have ever written one of those scripts instead, you already know what it costs to maintain.

The stakes, flat: this competency is roughly six percent of the exam, by this book's authored allocation, and that number understates the chapter twice. First, this is where the book's spine passes through. Chapter 3 introduced the control loop, this chapter instantiates it, and Chapter 15 generalizes it to a loop whose desired state lives in a Git repository. A reader who does not feel the shape here will meet Chapter 15's synthesis as a fifth list to memorize instead of as a recognition. Second, the workload-resource decision (Deployment or StatefulSet or DaemonSet or Job) reduces to a handful of questions asked in the right order, and the three misconceptions that surround it can all be defused by one figure and one rule.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Trace** the ownership chain from a Deployment down to a running Pod, and say which layer holds the count and which holds the template.
- **Explain** how a controller knows which Pods belong to it, what the API does when you get that wrong, and what happens to Pods that end up belonging to nobody.
- **Predict** what a cluster does during a rolling update, given `maxSurge` and `maxUnavailable`, and name the thing that makes the update safe rather than merely gradual.
- **Distinguish** the six workload resources by the one property that separates each from its nearest neighbor.
- **State** what actually creates a new revision, what looks like it should but doesn't, and what you give up when you stop retaining revisions.
- **Define** a custom resource, a custom controller, and the pattern that is the two of them together.

*You'll also stop reaching for `kubectl run`, which is a smaller change than it sounds and is the point of the whole chapter.*

---

## ⚪ §1 — The Resource That Holds the Intent

Who does the replacing? Something that already knows how many Pods you wanted and what one of them looks like.

Here is the answer in the documentation's own words, and it is worth reading twice: you don't need to manage each Pod directly. Instead, you use workload resources that manage a set of Pods on your behalf, and these resources configure controllers that make sure the right number of the right kind of Pod are running, to match the state you specified [source: k8s-docs-workloads-2026-08-23]. That sentence is this entire chapter in miniature. The rest of §1 is the unpacking.

*[cross-bearing: see Ch 5 §4 — a Pod is replaced, never rescheduled]* Chapter 5 handed you this question deliberately, and this is where it gets discharged. The Pod that vanished with its node is not recovered. Something notices it is gone and builds another one from a stored description.

### Three layers, not two

The workload resource you will reach for most often — and the one the documentation recommends over managing ReplicaSets yourself [source: k8s-docs-replicaset-2026-08-24] — is the **Deployment**. A Deployment manages a set of Pods to run an application workload, usually one that doesn't maintain state, and it provides declarative updates for Pods *and ReplicaSets* [source: k8s-docs-deployment-2026-08-23]. That second half is the part readers skim past, and it is the structural key to the next four sections.

There are three layers between you and a running container, not two. You create a Deployment; the Deployment creates a **ReplicaSet**; the ReplicaSet creates Pods in the background [source: k8s-docs-deployment-2026-08-23]. Usually you define a Deployment and let it manage ReplicaSets automatically. The documentation's own recommendation is that you may never need to manipulate a ReplicaSet object directly [source: k8s-docs-replicaset-2026-08-24].

<!-- FIGURE: ch06-fig01-deployment-replicaset-pod-ownership -->
```
        ┌──────────────────────────────────────────────────┐
        │  Deployment  "web"                               │
        │                                                  │
        │    Pod template   ──  what a replacement is       │
        │    strategy       ──  how replacements are made   │
        │    replicas: 3    ──  the count you write         │
        └───────────────────────────┬──────────────────────┘
                                    │  owns · sets the count on
                                    ▼
        ┌──────────────────────────────────────────────────┐
        │  ReplicaSet  "web-7d4b9c6f8"                     │
        │                                                  │
        │    replicas: 3    ──  the count it enforces       │
        │    selector       ──  how it finds its Pods       │
        └───────┬───────────────┬───────────────┬──────────┘
                │ owns          │ owns          │ owns
                ▼               ▼               ▼
          ┌──────────┐    ┌──────────┐    ┌──────────┐
          │   Pod    │    │   Pod    │    │   Pod    │
          └──────────┘    └──────────┘    └──────────┘

     intent flows DOWN  ·  existence is reported back UP
```

**Figure 6.1 — the ownership chain.** Notice what lives where. The Deployment is the layer that knows what a Pod should look like and how to replace one; the ReplicaSet is the layer that keeps a specific number of a specific kind alive. When §4 has two ReplicaSets running at once, this division is the reason it works.

> ★ **Fixed Point:**
>
> **The chain is Deployment → ReplicaSet → Pod. The Deployment owns the Pod template and the update strategy. The ReplicaSet owns a replica count and enforces it. The Pods run.**
>
> You write the count on the Deployment. The Deployment sets it on the ReplicaSet it currently considers current — §4 shows what happens when there are two. Both objects carry a `replicas` field [source: k8s-docs-deployment-spec-fields-2026-08-24] [source: k8s-docs-replicaset-2026-08-24], but only one of them is the layer where the count is *acted on*, and that is the ReplicaSet.

That last clarification matters more than it looks. `.spec.replicas` on a Deployment is an optional field specifying the number of desired Pods, defaulting to 1 [source: k8s-docs-deployment-spec-fields-2026-08-24]. `.spec.replicas` on a ReplicaSet specifies how many Pods should run concurrently, and the ReplicaSet creates or deletes its Pods to match that number, also defaulting to 1 [source: k8s-docs-replicaset-2026-08-24]. Same field name, two altitudes: one is where you express the wish, the other is where the wish is enforced. The simple version, Deployment holds the template and ReplicaSet holds the count, is the version to carry into §4 and §5. The full picture is that the number is written twice, and the Deployment is the author of the second copy.

### The template

A ReplicaSet is defined with a selector that specifies how to identify Pods it can acquire, a number of replicas indicating how many Pods it should be maintaining, and a **Pod template** specifying the data of new Pods it should create; when it needs to create a new Pod, it uses that template [source: k8s-docs-replicaset-2026-08-24].

Everything Chapter 4 taught you about an object's four required fields is unchanged. Everything Chapter 5 taught you about a Pod's `spec` is unchanged. It has simply moved one nesting level down: a Pod template has exactly the same schema as a Pod, except that it is nested and carries no `apiVersion` or `kind` of its own — the DaemonSet page states that rule in those words [source: k8s-docs-daemonset-2026-08-24]. You do not need that developed. You need it *located*. *[cross-bearing: see Ch 4 §2 — apiVersion, kind, metadata, spec]*

<!-- AUTHOR-REVIEW: the identical nesting rule for a Deployment's / ReplicaSet's `.spec.template` is not in the cached corpus — the Deployment API reference says only "Template describes the pods that will be created." The sentence above is therefore attributed visibly to the DaemonSet page. To state it as a general rule, cache `k8s-api-replicaset-v1-*` / `k8s-api-deployment-v1-*` (see recommended research gap 3). -->

### The reframe

Here is the sentence this section exists to deliver. The Pod you spent all of Chapter 5 learning is an object you will almost never create directly. Not because Pods are unimportant. They are still the only thing that actually runs. But being the thing that gets created *for* you is what a Pod is for. A ReplicaSet replaces Pods that are deleted or terminated for any reason, such as node failure or disruptive node maintenance like a kernel upgrade; a Pod you created by hand does not get that [source: k8s-docs-replicaset-2026-08-24].

> ⚓ **Worth Securing:** If you find yourself writing a bare Pod manifest for anything other than a one-off experiment, you have picked the wrong object. The question to ask is not "how do I run this container" but "what should stay true about this container."

One piece of vocabulary you may meet in older material: **ReplicationController**. It is the legacy API for managing workloads that can scale horizontally, superseded by the Deployment and ReplicaSet APIs; a Deployment that configures a ReplicaSet is now the recommended way to set up replication [source: k8s-docs-replicationcontroller-2026-08-24]. ReplicaSets are its successors, serving the same purpose and behaving similarly, except that a ReplicationController does not support set-based selector requirements [source: k8s-docs-replicaset-2026-08-24]. Recognize the word, know it is superseded, move on.

*[cross-bearing: see Ch 14 — a Helm chart's job is to template this object]*

---

## ⚪ §2 — A Loop You Can Watch Working

Chapter 3 promised you a control loop you could watch working in real time. This is it.

A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time; it is often used to guarantee the availability of a specified number of identical Pods [source: k8s-docs-replicaset-2026-08-24]. Set that against what Chapter 3 taught: a controller tracks at least one Kubernetes resource type, those objects have a `spec` field representing desired state, and the controller is responsible for making the current state come closer to that desired state [source: k8s-docs-controllers-2026-08-23].

Fill in the blanks and you have a ReplicaSet. Desired state is `.spec.replicas`. Current state is how many matching Pods actually exist. When they differ, the ReplicaSet creates or deletes Pods until they don't [source: k8s-docs-replicaset-2026-08-24]. That is Chapter 3's thermostat with the numbers filled in.

*[cross-bearing: see Ch 3 §6–§7 — the control loop, and why nobody is in charge]*

### The demonstration

Here is the part worth doing rather than reading. Delete a Pod that a ReplicaSet owns:

```
$ kubectl get pods
NAME                   READY   STATUS    RESTARTS   AGE
web-7d4b9c6f8-mn4pq    1/1     Running   0          6m
web-7d4b9c6f8-qq8jz    1/1     Running   0          6m
web-7d4b9c6f8-x9k2r    1/1     Running   0          6m

$ kubectl delete pod web-7d4b9c6f8-mn4pq
pod "web-7d4b9c6f8-mn4pq" deleted

$ kubectl get pods
NAME                   READY   STATUS              RESTARTS   AGE
web-7d4b9c6f8-qq8jz    1/1     Running             0          6m
web-7d4b9c6f8-x9k2r    1/1     Running             0          6m
web-7d4b9c6f8-z7rtc    0/1     ContainerCreating   0          2s
```

Nobody triggered that. No job ran. No alert fired and no runbook was consulted. A gap appeared between what you asked for and what existed, and a loop that had been watching the whole time closed it. The new Pod is not the old Pod recovered. It is a different Pod with a different name and a different UID *[cross-bearing: see Ch 5 §4 — replacement, not recovery]*, built from the same template.

Worth noticing about the mechanics: the controller does not create that Pod itself. More commonly in Kubernetes, a controller sends messages to the API server that have useful side effects [source: k8s-docs-controllers-2026-08-23], and other components act on the new information. The "nobody is in charge" property Chapter 3 established holds at this altitude too. The ReplicaSet controller writes a wish to the API server and something else does the work.

### Scaling is the same operation

A ReplicaSet can be scaled up or down by simply updating the `.spec.replicas` field; the controller ensures that the desired number of Pods with a matching label selector are available and operational [source: k8s-docs-replicaset-2026-08-24]. `kubectl scale` is a first-class verb for exactly that, updating the size of the specified deployment [source: k8s-docs-kubectl-overview-2026-08-23]:

```
$ kubectl scale deployment/web --replicas=5
deployment.apps/web scaled
```

Now look at what the loop just did. It saw a gap of two between desired and current, and it closed it. That is precisely what it did sixty seconds ago when you deleted a Pod, except the gap that time was one and it appeared for a different reason. **The loop cannot tell the difference.** "You asked for five and there are three" and "you asked for three and one died" are the same input.

> ⚓ **Worth Securing:** Self-healing and scaling are not two features. They are one loop, seeing the same kind of gap, taking the same action. If you can hold that, you have most of what this chapter teaches.

Horizontal scaling means that the response to increased load is to deploy more Pods [source: k8s-docs-hpa-2026-08-24]. When it isn't you writing that number, it is usually a **HorizontalPodAutoscaler**: an API resource plus a controller, running in the control plane, that periodically adjusts the desired scale of its target to match observed metrics such as average CPU utilization [source: k8s-docs-hpa-2026-08-24]. Kubernetes implements it as a control loop that runs intermittently rather than continuously [source: k8s-docs-hpa-2026-08-24]. A ReplicaSet can be an HPA target directly, though in practice you point one at a Deployment [source: k8s-docs-replicaset-2026-08-24].

One sentence is all the HPA gets here. Where its metrics come from and what else can autoscale are later problems. *[cross-bearing: see Ch 13 — metrics-server is what an HPA reads]* *[cross-bearing: see Ch 17 — the autoscaling landscape]*

One last observation from Chapter 3, now with teeth. Your cluster could be changing at any point as work happens and control loops automatically fix failures, which means that potentially your cluster never reaches a stable state; and as long as the controllers are running and able to make useful changes, it doesn't matter whether the overall state is stable [source: k8s-docs-controllers-2026-08-23]. Kubernetes is not trying to arrive anywhere. It is trying to keep closing gaps.

*[cross-bearing: see Ch 7 §1 — the Pod this loop just created still has to be placed on a node, and sometimes it can't be]*
*[cross-bearing: see Ch 9 — this churn is exactly why something needs a stable name]*

---

## 🔵 §3 — How a Controller Knows Its Own

Chapter 4 taught you label selectors as the universal join and listed the places they get used. This is the first one collected, and it comes with a consequence Chapter 4 did not state.

### Membership is a query

A ReplicaSet does not track its Pods by name and does not hold a list. Chapter 4 drew this join once already — figure `ch04-fig03-labels-selectors-join` — and the picture here is the same one, now with an owner on one side. It has a `.spec.selector`, a label selector, using the labels that identify potential Pods to acquire [source: k8s-docs-replicaset-2026-08-24]. The machinery is exactly what Chapter 4 gave you: set-based requirements are expressed through `matchExpressions`, and `matchLabels` is the equality-shaped shorthand, equivalent to `matchExpressions` with the operator `In`; newer resources such as Job, Deployment, ReplicaSet and DaemonSet support both [source: k8s-docs-labels-selectors-2026-08-23]. Nothing new to learn, one new place to apply it. *[cross-bearing: see Ch 4 §5 — labels and selectors, the universal join]*

Its Pods are whichever Pods match. Not "the Pods it made." The ones that match, right now, whoever made them.

> **Before reading on:** the labels in the Pod template do not match the selector. The controller creates a Pod from the template, and then cannot see it. Work out what happens next before you read the answer. It takes about ten seconds and the answer is worth deriving yourself.

You got a runaway. Create a Pod, fail to see it, notice the count is still short, create another, and keep going, with no condition that ever stops it. That outcome is so obviously bad that Kubernetes refuses to let you build it. In a ReplicaSet, `.spec.template.metadata.labels` **must** match `spec.selector` or the object will be rejected by the API [source: k8s-docs-replicaset-2026-08-24]. Same for a Deployment: `.spec.selector` must match `.spec.template.metadata.labels`, or it will be rejected by the API [source: k8s-docs-deployment-spec-fields-2026-08-24]. Same for a DaemonSet: configuration with those two not matching is rejected [source: k8s-docs-daemonset-2026-08-24].

This is worth sitting with. It is one of the few validations Kubernetes performs by refusing the object outright rather than accepting it and reconciling toward it, and the reason is simple: what you wrote has no reachable steady state at all.

<!-- AUTHOR-REVIEW: the outline (§3, Bearings #1 item 3) assumes a selector/template mismatch produces a live runaway in the cluster. All three cached sources state the API rejects the object outright. Section teaches the rejection with the runaway as the *reason* for it, and Bearings #1 item 3 plus Practice Q3's replacement are aligned to that reading. Confirmed against the corpus by the fact-accuracy stage; retained here for the record. -->

> ★ **Fixed Point:**
>
> **A controller's Pods are the Pods matching its selector. Membership is a query, not a list. Because it is a query, the Pod template's labels must satisfy the selector, and the API rejects any workload object where they don't.**

### Ownership is a separate mechanism

Selectors answer "which Pods are mine right now." Owner references answer "who is responsible for this object." They are not the same thing, and the documentation is explicit that ownership is different from the labels and selectors mechanism [source: k8s-docs-garbage-collection-2026-08-24].

A ReplicaSet is linked to its Pods via the Pods' `metadata.ownerReferences` field, which specifies what resource the current object is owned by; all Pods acquired by a ReplicaSet carry the owning ReplicaSet's identifying information there, and it is through this link that the ReplicaSet knows the state of the Pods it maintains [source: k8s-docs-replicaset-2026-08-24]. Many objects in Kubernetes link to each other this way; owner references tell the control plane which objects are dependent on others, and Kubernetes manages them automatically in most cases [source: k8s-docs-garbage-collection-2026-08-24].

That link is what makes deletion tidy. Kubernetes checks for and deletes objects that no longer have owner references, like the Pods left behind when you delete a ReplicaSet, in a process called **cascading deletion**, and background cascading deletion is the default [source: k8s-docs-garbage-collection-2026-08-24]. In practice: delete the Deployment and its ReplicaSets and their Pods go too. To delete a ReplicaSet and all of its Pods you just use `kubectl delete`; the garbage collector automatically removes the dependent Pods by default [source: k8s-docs-replicaset-2026-08-24].

The opposite outcome has a name too. Dependents that survive their owner are called **orphan** objects, and by default Kubernetes deletes dependents rather than leaving them behind [source: k8s-docs-garbage-collection-2026-08-24]. The way you produce orphans by accident is by changing a selector, so that Pods a controller used to claim stop matching it and nothing is left holding them. That route is hazardous enough that a DaemonSet's `.spec.selector` cannot be mutated at all once the object is created, precisely because mutating a pod selector can lead to the unintentional orphaning of Pods [source: k8s-docs-daemonset-2026-08-24].

### Where the selector actually bites

The API stops you from misconfiguring a single controller. It does not stop two controllers from claiming the same Pods, and it does not stop a controller from claiming a Pod you made yourself.

A ReplicaSet identifies new Pods to acquire using its selector: if a Pod has no owner reference, or an owner reference that is not a controller, and it matches the selector, it will be immediately acquired [source: k8s-docs-replicaset-2026-08-24]. A ReplicaSet is not limited to owning Pods produced by its own template [source: k8s-docs-replicaset-2026-08-24]. So if you hand-create a Pod carrying labels that match some ReplicaSet's selector, that ReplicaSet adopts it; and if adopting it puts the ReplicaSet over its desired count, the newly adopted Pod is immediately terminated [source: k8s-docs-replicaset-2026-08-24].

> 🪝 **Snag:** You create a debugging Pod with `app: web` on it, because that is what the other Pods have. It is adopted by the ReplicaSet and killed within seconds. Nothing errors. Nothing warns you. Your Pod was simply surplus to a count somebody else was holding.

The documentation's own advice for the template is blunt: be careful not to overlap with the selectors of other controllers, lest they try to adopt this Pod [source: k8s-docs-replicaset-2026-08-24].

> **Logbook Entry:** Overlapping selectors fail in two directions, and neither direction announces itself as a configuration mistake, which is what makes them expensive.
>
> Somebody ships a second workload and copies the first one's manifest as a starting point, including its labels. Neither controller is misconfigured in any way the API can see; each one's template agrees with its own selector, which is all the API validates. But each is now querying for Pods the other created. The documented consequence is adoption: a Pod that matches a selector and has no controller owning it is immediately acquired, and if that acquisition puts the acquirer over its desired count, the Pod is immediately terminated [source: k8s-docs-replicaset-2026-08-24].
>
> Then somebody notices the collision and fixes it the obvious way, by editing one of the selectors. That is the other direction. Pods the edited controller used to claim stop matching it, and nothing is left holding them — the unintentional orphaning the DaemonSet page warns about, and the reason a DaemonSet forbids the edit outright [source: k8s-docs-daemonset-2026-08-24].
>
> The prevention is a single habit, and it costs nothing: give every workload one label that is genuinely unique to it, and never hand-write a selector by copying somebody else's.

*[cross-bearing: see Ch 9 — a Service selects its backends with the same mechanism, which is a different controller reading the same labels]*
*[cross-bearing: see Ch 12 — deleting a workload does not delete everything it referenced]*

---

## ☆ Taking Your Bearings #1: Intent, Loops, and Ownership

Five questions on what holds the intent and how it finds its Pods. Two of them reach back to earlier chapters.

**1.** ⚪ Name the three layers between a Deployment and a running container process, and say which layer holds the replica count and which holds the Pod template.

A) Deployment → Pod. The Deployment holds both.
B) Deployment → ReplicaSet → Pod. The Deployment holds the template and strategy; the ReplicaSet holds and enforces the count.
C) Deployment → ReplicaSet → Pod. The ReplicaSet holds the template; the Deployment holds the count.
D) Deployment → ReplicaSet → Pod. The Deployment holds both the count and the template; the ReplicaSet only watches and reports.

**2.** ⚪ You delete a Pod that a ReplicaSet owns. Describe what happens next and what caused it.

**3.** ⚪ You write a Deployment manifest in which the Pod template's labels do not match the Deployment's selector, and you `kubectl apply` it. What happens?

A) The Deployment is created and produces a growing population of Pods it cannot see.
B) The Deployment is created but reports zero replicas forever.
C) The API rejects the object.
D) The selector is silently rewritten to match the template.

**4.** ⚪ **[retrieval: ch3]** Chapter 3 gave you a loop with two states and an action. Fill all three in for a ReplicaSet, using the actual field name for the desired state.

**5.** 🔵 **[retrieval: ch4]** In Chapter 9 you will meet a Service, which finds its backend Pods the same way a ReplicaSet does. What would it mean for one Pod to be selected by both at once?

---

**Answers with Explanations**

**1. B.**

- **A is wrong**, and it is the most consequential wrong answer in this chapter. If you believe a Deployment owns Pods directly, §4 will be incomprehensible, because a rolling update works by having *two* ReplicaSets alive at once, one shrinking and one growing, with the Deployment holding both. Delete the middle layer from your mental model and the mechanism has nowhere to live.
- **C is wrong** because it swaps the layers. The Deployment provides declarative updates for Pods and ReplicaSets [source: k8s-docs-deployment-2026-08-23]; the template and the update strategy are its business. The ReplicaSet is the layer whose whole purpose is maintaining a stable set of replica Pods [source: k8s-docs-replicaset-2026-08-24].
- **D is wrong** because it makes the ReplicaSet passive, which is the half-understanding worth naming. The ReplicaSet is not a bookkeeping record of what the Deployment did; it is the running controller that creates and deletes Pods to reach its own `.spec.replicas` [source: k8s-docs-replicaset-2026-08-24]. The Deployment does not touch Pods at all.
- Note the nuance from §1: `replicas` appears on both the Deployment and the ReplicaSet. B is right because the ReplicaSet is where the count is *enforced*.

**2.** The ReplicaSet's desired count and its current count no longer agree, so it creates a Pod from its template to close the gap. **The correct answer turns on nothing having been triggered.** No scheduled task ran, no alert fired, no operator intervened. A loop that was already running observed a difference and acted on it, the same thing it does when you scale up, for the same reason [source: k8s-docs-replicaset-2026-08-24].

If your answer was "the Pod restarts" or "Kubernetes brings it back," soften that wording now, because it will cost you in §6. Nothing came back. A *different* Pod, with a different name and a different UID, was built from the same template [source: k8s-docs-pod-lifecycle-2026-08-23]. That distinction is the entire reason StatefulSets exist.

**3. C.** The API rejects it. In a ReplicaSet, `.spec.template.metadata.labels` must match `spec.selector` [source: k8s-docs-replicaset-2026-08-24]; on a Deployment, `.spec.selector` must match `.spec.template.metadata.labels` [source: k8s-docs-deployment-spec-fields-2026-08-24]. Both sources say it in the same words: it will be rejected by the API.

- **A is wrong, but it is the *right* intuition.** The runaway is exactly what would happen if the object were accepted, which is why the API refuses it. If you picked A, you understood the mechanism and did not know about the validation. That is a good place to be missing a point from.
- **B is wrong** because it imagines the controller doing nothing. A selector query returning zero results is not an error condition; the controller would create Pods, not sit still.
- **D is wrong** because Kubernetes does not repair your intent by editing it. It either accepts a record of intent or rejects it.

**4.** Desired state: `.spec.replicas`. Current state: the number of Pods currently matching the ReplicaSet's selector. Action: create or delete Pods until the two agree [source: k8s-docs-replicaset-2026-08-24]. If your answer for current state was "the number of Pods it created," look again at §3. Membership is a query, and a Pod it never created can count toward the total.

**5.** Nothing unusual. They are independent queries over the same labels, and the Pod is simply a member of two sets. The ReplicaSet is asking "is this one of the Pods I am responsible for keeping alive"; the Service is asking "is this one of the Pods I should send traffic to." Neither query knows about the other and neither one owns the Pod on the other's behalf. The documentation draws this distinction explicitly for a related case: a Service uses labels to determine which EndpointSlice objects are used for it, and *in addition* each EndpointSlice carries an owner reference, because ownership and selection are different mechanisms doing different jobs [source: k8s-docs-garbage-collection-2026-08-24]. *[cross-bearing: see Ch 9 — EndpointSlice, the object behind a Service's endpoints]*

If you answered that this is a conflict, or that one of them must win, or that the Pod needs to be released by one before the other can have it, go back to §3's closing distinction. **Ownership is exclusive; selection is not.** A Pod can satisfy any number of independent queries, and none of them own it by doing so. Holding the wrong version of this makes Chapter 9's Services look like they are fighting the workload controller, which they never are.

---

**Checkpoint: you've now mastered**

✓ The ownership chain, and which layer holds which piece of intent
✓ Why a deleted Pod comes back without anyone doing anything
✓ That a controller finds its Pods by query, and what the API does when the query can't work
✓ That ownership and selection are two mechanisms, not one, and what a Pod belonging to nobody is called

☐ How a running fleet gets replaced with a different one (next)
☐ What gets recorded when it does

---

## 🔵 §4 — Changing the Fleet Under Way

This is the densest section in the chapter. It is also the one that pays a promise Chapter 5 made in its closing pages.

### The mechanism

You declare the new state of the Pods by updating the Pod template on the Deployment. A new ReplicaSet is created, and the Deployment manages moving Pods from the old ReplicaSet to the new one at a controlled rate [source: k8s-docs-deployment-2026-08-23].

Read that again with §1's figure in front of you, because this is where the three-layer chain earns its keep. Two ReplicaSets exist simultaneously. The old one is being scaled down. The new one is being scaled up. Both are owned by the same Deployment, and each is doing nothing more exotic than what §2 showed you: holding a count and closing gaps. The Deployment's entire contribution is deciding, moment to moment, what those two counts should be.

A reader who has the ownership chain finds the rolling update obvious. A reader who does not finds it magic. *[cross-bearing: see Ch 6 §1 — the ownership chain]*

### The two bounds

`.spec.strategy` specifies the strategy used to replace old Pods with new ones. `.spec.strategy.type` can be `Recreate` or `RollingUpdate`, and **`RollingUpdate` is the default** [source: k8s-docs-deployment-2026-08-23]. A rolling update is shaped by two fields, and these are the two facts in this chapter most easily transposed:

**`maxUnavailable`** is the maximum number of Pods that can be unavailable during the update. The value can be an absolute number or a percentage of desired Pods. **The absolute number is calculated from a percentage by rounding down. The default value is 25%.** [source: k8s-docs-deployment-spec-fields-2026-08-24]

**`maxSurge`** is the maximum number of Pods that can be created *over* the desired number of Pods. The value can be an absolute number or a percentage. **The absolute number is calculated from a percentage by rounding up. The default value is 25%.** [source: k8s-docs-deployment-spec-fields-2026-08-24]

Neither one can be zero if the other is zero [source: k8s-docs-deployment-spec-fields-2026-08-24], which makes sense the moment you say it aloud, because a rollout that may neither exceed the desired count nor drop below it has no legal move to make.

### Work one example, once

Ten replicas. Both fields left at their defaults.

| Field | 25% of 10 | Rounding direction | Absolute value |
|---|---|---|---|
| `maxSurge` | 2.5 | **up** | 3 |
| `maxUnavailable` | 2.5 | **down** | 2 |

Ceiling on total Pods = 10 + 3 = **13**. Floor on available Pods = 10 − 2 = **8**.

At most thirteen Pods exist at any instant during the update, counting old and new together. At least eight are available at any instant. Do that arithmetic once by hand and the two names stop being interchangeable.

Notice the asymmetry in the rounding, because it is not arbitrary. Surge rounds up: Kubernetes will give you *more* headroom above the line than the percentage strictly buys. Unavailable rounds down: it will allow *fewer* Pods to be missing than the percentage strictly permits. Both defaults round in the direction of keeping more capacity online. That is a design decision you can read straight off the field descriptions.

<!-- AUTHOR-REVIEW: the outline's worked example (§4, fig02 spec, and Bearings #2 item 1) states the ceiling for 10 replicas at defaults is 12. The cached source specifies maxSurge rounds UP from a percentage, giving ceil(2.5) = 3 and a ceiling of 13; the fact-accuracy stage confirmed 13 against both the concept page and the API reference. Draft uses 13 throughout, including fig02, Bearings #2 and Practice Q8's independent six-replica case. The outline's 12 must be corrected before it propagates to The Lodestar. -->

<!-- AUTHOR-REVIEW: the worked-arithmetic block above was a fenced ASCII block in draft-v1 and tripped the structural linter's figure-anchor check (it is a calculation, not a diagram, and is fully subsumed by ch06-fig02 which renders the same two numbers as lines on a chart). It is now typeset as a table, which needs no anchor. If the author would rather have it rendered as a figure, it needs an anchor (`ch06-fig07-rolling-update-arithmetic`) and a matching image-specs entry; the two rounding rows must stay adjacent either way so the asymmetry is visible at a glance. -->

<!-- FIGURE: ch06-fig02-rolling-update-maxsurge-maxunavailable -->
```
  count
        │
   13   ┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈  CEILING on total
        │                                          = desired + maxSurge (10 + 3)
        │  old ███████████  ████████  █████  ██
   10   ─┼──────────────────────────────────────  DESIRED = 10
        │  new ░░       ░░░░░░    ░░░░░░░  ░░░░░░░░░░
    8   ┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈  FLOOR on available
        │                                          = desired − maxUnavailable (10 − 2)
        └────────────────────────────────────────▶  time

      old + new  never rises above the CEILING
      available  never falls below the FLOOR
```

**Figure 6.2 — the two bounds are opposite in kind.** `maxSurge` is a ceiling on how many Pods exist. `maxUnavailable` is a floor on how many are usable. They are not two settings of the same knob.

> 🪢 **Mnemonic:** Surge is above the line. Unavailable is below it.

### Recreate

The other strategy is the contrast that makes the first one legible. With `Recreate`, all existing Pods are killed before new ones are created [source: k8s-docs-deployment-2026-08-23].

<!-- FIGURE: ch06-fig03-recreate-vs-rolling -->
```
  Recreate
    available  ██████████                    ██████████
                          └── ZERO AVAILABLE ─┘
               ────────────────────────────────────────▶ time
                   all old killed        then new created


  RollingUpdate
    available  ██████████▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░██████████
                        never reaches zero
               ────────────────────────────────────────▶ time
                   old and new overlap throughout
```

**Figure 6.3 — the gap is the whole point.** `Recreate` has a window in which nothing is serving. That window is not a bug; it is the thing you chose.

And it *is* a legitimate choice, not a mistake. Some applications genuinely cannot have two versions running at once: a schema migration that the old code cannot read, an exclusive lock on a resource, a license that permits one active instance. For those, downtime is not a failure of the deployment strategy; it is the cost of correctness, taken deliberately and scheduled. Treating `Recreate` as always-wrong is its own trap.

> **Dead Reckoning:** A Deployment's `.spec.strategy.type` is either `Recreate` or `RollingUpdate`; `RollingUpdate` is the default [source: k8s-docs-deployment-2026-08-23]. With `Recreate`, all existing Pods are terminated before any new Pod is created [source: k8s-docs-deployment-2026-08-23]. With `RollingUpdate`, changing `.spec.template` causes a new ReplicaSet to be created and the Deployment to move Pods from the old ReplicaSet to the new one at a controlled rate [source: k8s-docs-deployment-2026-08-23]. That rate is bounded by two optional fields under `.spec.strategy.rollingUpdate`. `maxUnavailable` is the maximum number of Pods that may be unavailable during the update; percentages round down; default 25%. `maxSurge` is the maximum number of Pods that may exist over the desired count; percentages round up; default 25%. Neither may be 0 if the other is 0. [source: k8s-docs-deployment-spec-fields-2026-08-24]

> ★ **Fixed Point:**
>
> **`RollingUpdate` is the default strategy. `Recreate` kills every old Pod before creating any new one. `maxSurge` and `maxUnavailable` both default to 25%.**
>
> The discriminator between the two bounds is the rounding, and it runs in opposite directions: **surge rounds up, unavailable rounds down** [source: k8s-docs-deployment-spec-fields-2026-08-24]. Both defaults therefore err toward keeping more capacity online, which is the sentence to memorize if you can only keep one — you can rebuild both rules from it.

### What makes it safe

A gradual replacement is not automatically a safe one. Replacing ten broken Pods two at a time still ends with ten broken Pods; it just takes longer.

What makes it safe is availability. Kubernetes marks a Deployment as progressing when, among other things, new Pods become ready or available, where available means ready for at least `minReadySeconds` [source: k8s-docs-deployment-spec-fields-2026-08-24]. `.spec.minReadySeconds` is the minimum number of seconds for which a newly created Pod should be ready without any of its containers crashing for it to be considered available; it defaults to 0, meaning a Pod counts as available the moment it is ready [source: k8s-docs-deployment-spec-fields-2026-08-24].

And "ready" is Chapter 5's word. A readiness probe indicates whether the container is ready to respond to requests; when it fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod [source: k8s-docs-pod-lifecycle-2026-08-23].

Put those together and you have the property Chapter 5 promised you. The relief comes aboard before the old watch is dismissed, and nobody is dismissed until the relief has actually reported fit. A new Pod that never reports ready never becomes available. A rollout that cannot accumulate available new Pods cannot proceed to remove old ones without breaching the `maxUnavailable` floor. So it doesn't. **The rollout stalls instead of taking down the service.** Readiness probe failures are listed by name among the reasons a Deployment gets stuck trying to deploy its newest ReplicaSet without ever completing [source: k8s-docs-deployment-spec-fields-2026-08-24], alongside image pull errors, insufficient quota, insufficient permissions, limit ranges, and application runtime misconfiguration.

This is the moment probes stop being a health-checking feature and become a release-safety mechanism. Chapter 5 told you a Pod that never reports ready never receives traffic. §4 tells you the larger consequence: a *version* that never reports ready never replaces the version that works. *[cross-bearing: see Ch 5 §7 — liveness, readiness, and startup probes]*

> 🪝 **Snag:** A stalled rollout is not a failed one. The Deployment sits there with both ReplicaSets alive, the old Pods still serving traffic, waiting for a new Pod that will never become ready. Your users see nothing. Your dashboard sees nothing. `kubectl get deployments` shows a ready count that has stopped moving. Nothing will page you unless you asked something to.

The clock on that is `.spec.progressDeadlineSeconds`, the number of seconds to wait for the Deployment to progress before the system reports back that it has failed to progress, surfaced as a condition with `type: Progressing`, `status: "False"` and `reason: ProgressDeadlineExceeded`. It defaults to 600, and the controller keeps retrying regardless [source: k8s-docs-deployment-spec-fields-2026-08-24]. Note what it does and does not do: it produces a *signal*. It does not roll anything back. Reading that signal, and finding out which of the six causes you hit, is a diagnosis skill. *[cross-bearing: see Ch 13 — diagnosing a stuck rollout]*

Rolling updates are the mechanism. There is a whole vocabulary of *release strategies* built on top of them: patterns with names, implemented with tooling that sits above the Deployment object. That vocabulary needs machinery this chapter has not introduced yet. *[cross-bearing: see Ch 15 — blue/green, canary, and A/B, and the tooling that implements them]*

---

## 🔵 §5 — Every Rollout Is a Revision

Every time the Deployment moves Pods from one ReplicaSet to another, something gets written down. That record is what makes going back possible.

### The rule, stated exactly

A Deployment's revision is created when a rollout is triggered, and **a new revision is created if and only if the Deployment's Pod template (`.spec.template`) is changed.** Other updates, such as scaling the Deployment, do not create a revision [source: k8s-docs-deployment-2026-08-23].

That "if and only if" is the whole content of this section, and it is precisely the kind of boundary that is easy to get backwards, because the intuitive answer is wrong and the correct answer fits in one clause. The intuitive answer is "any change to the Deployment creates a revision." It doesn't. Change the replica count and you have changed the Deployment, changed the cluster, and changed nothing about the revision history.

> ★ **Fixed Point:**
>
> **A revision is created if and only if `.spec.template` changes. Scaling does not create a revision.**
>
> The corollary catches people: `kubectl rollout undo` will not reverse a scale. There is no revision to go back to, because scaling never made one.

Why does the rule work this way? Because a revision is really a ReplicaSet. Each new ReplicaSet updates the revision of the Deployment [source: k8s-docs-deployment-2026-08-23], and a new ReplicaSet is only created when the template changes: a different template is a different kind of Pod, which needs a different ReplicaSet to hold it. Scaling changes a number on the ReplicaSet you already have. Nothing new was created, so nothing new was recorded.

### The verbs

The command surface here is small and closed. `kubectl rollout` manages the rollout of one or many resources, and the valid resource types are deployments, daemonsets and statefulsets [source: k8s-docs-kubectl-rollout-2026-08-24]. Six subcommands:

| Command | What it does |
|---|---|
| `kubectl rollout status` | Show the status of the rollout [source: k8s-docs-kubectl-rollout-2026-08-24] |
| `kubectl rollout history` | View rollout history [source: k8s-docs-kubectl-rollout-2026-08-24] |
| `kubectl rollout undo` | Undo a previous rollout [source: k8s-docs-kubectl-rollout-2026-08-24] |
| `kubectl rollout pause` | Mark the provided resource as paused [source: k8s-docs-kubectl-rollout-2026-08-24] |
| `kubectl rollout resume` | Resume a paused resource [source: k8s-docs-kubectl-rollout-2026-08-24] |
| `kubectl rollout restart` | Restart a resource [source: k8s-docs-kubectl-rollout-2026-08-24] |

`kubectl rollout history deployment/<name>` shows the revisions. `kubectl rollout undo deployment/<name>` rolls back to the previous revision, and `--to-revision=<n>` goes to a specific one [source: k8s-docs-deployment-2026-08-23].

**Pause and resume** are the pair that reads as arbitrary until you know why they exist. When you update a Deployment, or plan to, you can pause rollouts before you trigger one or more updates, then resume when you are ready to apply the changes, which lets you apply multiple fixes in between pausing and resuming without triggering unnecessary rollouts [source: k8s-docs-deployment-2026-08-23]. Without pause, three edits to the template are three rollouts, each one moving real Pods and each one interrupting the last. With pause, they are one.

> ⚓ **Worth Securing:** Pause before a batch of template edits. It is the difference between one rollout and four, and the four are not independent: each one restarts the work of the one before it.

### What is kept

By default, all of a Deployment's rollout history is kept in the system so that you can roll back any time you want, and you can change that by modifying the revision history limit [source: k8s-docs-deployment-2026-08-23]. Precisely: `.spec.revisionHistoryLimit` is the number of old ReplicaSets to retain to allow rollback, and it defaults to 10 [source: k8s-docs-deployment-spec-fields-2026-08-24]. Those old ReplicaSets consume space in etcd and crowd the output of `kubectl get rs`, which is why the field exists; and setting it to zero cleans up all old ReplicaSets with zero replicas, with the consequence that a new rollout **cannot be undone**, since its revision history has been cleaned up [source: k8s-docs-deployment-spec-fields-2026-08-24].

"Can I still roll back?" is a real question at a real moment, and the default answer is yes, ten deep.

### What a rollback actually is

This matters more than it looks, because you are going to meet the word "rollback" twice more in this book attached to entirely different mechanisms.

Rolling back a Deployment is not undoing an edit, and it is not restoring a backup. It is setting the Pod template to a previous revision's value and letting the same rolling update from §4 run in the other direction: same two ReplicaSets, same `maxSurge` and `maxUnavailable`, same readiness gate, opposite direction of travel. The ReplicaSet holding the old template has been riding at anchor the whole time with nobody aboard, which is exactly why the operation is fast and exactly why deleting the revision history removes the ability to do it.

Same loop. Same mechanics. Opposite direction.

*[cross-bearing: see Ch 14 — Helm rollback and Deployment rollback are different mechanisms wearing the same word]*
*[cross-bearing: see Ch 15 — and a third thing, again wearing it]*

> ⚠ **Navigational Hazards**
>
> **"I scaled it and now `rollout history` shows nothing new."** Correct. Scaling is not a template change, so no revision was created [source: k8s-docs-deployment-2026-08-23]. The intuitive model, "the Deployment changed, so the history should record it," is the wrong model. The history records *kinds of Pod*, not *states of Deployment*.
>
> **"I'll just `rollout undo` to get back to three replicas."** You cannot. `undo` restores a Pod template. Your replica count is not in a Pod template. If you scaled from three to six and want three back, scale to three.
>
> **"I set `revisionHistoryLimit: 0` to keep etcd clean."** You also removed your ability to roll back; the documentation says so in the same paragraph that describes the field [source: k8s-docs-deployment-spec-fields-2026-08-24]. There is a defensible reason to do this in a GitOps environment where the previous state lives somewhere else entirely. There is no defensible reason to do it because the `kubectl get rs` output was untidy.
>
> **"The rollout failed."** Usually it stalled. See §4: a Deployment that cannot get new Pods to available does not fail over to the old version. It stops, holding both ReplicaSets, with the old Pods still serving. The distinction matters because "failed" implies something ended and "stalled" means something is still waiting for you.

---

## ☆ Taking Your Bearings #2: Changing the Fleet Under Way

Five questions on changing the fleet and what a change gets recorded as. One reaches back.

**1.** 🔵 A Deployment with ten replicas is updated using the default strategy settings. What is the largest number of Pods that may exist at any instant during the update, and the smallest number that must be available?

A) 12 and 8
B) 13 and 8
C) 13 and 7
D) 11 and 9 — the 25% is a single budget split between surge and unavailability

**2.** 🟡 **This one is meant to be hard. If you miss it, you are far from alone, and the miss is worth more to you than a correct guess would have been.** You scale a Deployment from three replicas to six, then run `kubectl rollout history`. How many new revisions do you see, and why?

**3.** 🔵 Your application cannot run two versions at once, because the new version applies a schema migration the old version cannot read. Which strategy do you choose, and what exactly are you accepting when you choose it?

**4.** 🔵 **[retrieval: ch5]** You push a broken image. The new Pods start, but their readiness probes never succeed. Describe what the Deployment does, and what the users of the service experience.

**5.** 🔵 You need to change the image, an environment variable, and the resource limits on one Deployment, and you want one rollout rather than three. How do you do it, and what are the two commands?

---

**Answers with Explanations**

**1. B — 13 and 8.**

Both fields default to 25% [source: k8s-docs-deployment-spec-fields-2026-08-24]. 25% of 10 is 2.5 in both cases, but they round in opposite directions: `maxSurge` rounds **up** to 3, `maxUnavailable` rounds **down** to 2. Ceiling on total = 10 + 3 = 13. Floor on available = 10 − 2 = 8.

- **A is wrong** because it rounds `maxSurge` down. This is the most defensible wrong answer and the one worth understanding: if you got here, you had the right structure and the wrong rounding rule.
- **C is wrong** because it rounds `maxUnavailable` up. Same error, other field.
- **D is wrong** because it treats 25% as a single allowance shared between the two fields and splits it — one Pod of surge, one Pod of unavailability, giving 11 and 9. They are independent fields bounding independent quantities: one bounds how many Pods *exist*, the other bounds how many are *usable*, and each gets its own 25%.

**2. None.** Scaling changes `.spec.replicas`. It does not change `.spec.template`. A new revision is created if and only if the Pod template is changed; other updates, such as scaling, do not create a revision [source: k8s-docs-deployment-2026-08-23].

If you answered "one," you are far from alone, and you now have the rule in a form you will not lose, because you paid for it. The underlying reason is worth carrying: a revision *is* a ReplicaSet, and a new ReplicaSet is only needed when the kind of Pod changes. Six copies of the same Pod need the same ReplicaSet that three copies needed.

**3. `Recreate`, and you are accepting a window of complete unavailability.** All existing Pods are killed before new ones are created [source: k8s-docs-deployment-2026-08-23]. The important half of this answer is the second half. You are not making a mistake; you are trading availability for correctness, because a rolling update would put old code and migrated data in the same room. Schedule it, announce it, and choose it on purpose.

If your answer was "a rolling update with `maxSurge: 0`," that is the near-miss worth naming: it removes the *extra* Pods but not the overlap. With `maxSurge: 0` and `maxUnavailable: 1`, old and new versions still coexist while the update walks through the fleet, which is exactly what a schema migration forbids. Only `Recreate` guarantees no overlap.

**4.** The rollout stalls. New Pods that never report ready never become available [source: k8s-docs-deployment-spec-fields-2026-08-24]; a rollout that cannot accumulate available new Pods cannot scale the old ReplicaSet down past the `maxUnavailable` floor. So both ReplicaSets stay alive, the old Pods keep serving, and, because a failing readiness probe removes a Pod's IP from the endpoints of all Services matching it [source: k8s-docs-pod-lifecycle-2026-08-23], no traffic is ever sent to the broken new Pods.

**Users experience nothing.** That is the entire value of the mechanism, and it is why Chapter 5 spent as long as it did on probes.

After `progressDeadlineSeconds` (600 by default), the Deployment surfaces a `Progressing` condition with `reason: ProgressDeadlineExceeded` [source: k8s-docs-deployment-spec-fields-2026-08-24]. Naming that signal is this chapter's job. Reading the events, finding which of the six causes fired, and fixing it is Chapter 13's. *[cross-bearing: see Ch 13 §3]*

**5.** `kubectl rollout pause deployment/<name>`, then make all three edits, then `kubectl rollout resume deployment/<name>`. Pausing before you trigger updates lets you apply multiple fixes in between pausing and resuming without triggering unnecessary rollouts [source: k8s-docs-deployment-2026-08-23]. Without it, each of the three template edits triggers its own rollout, and each one interrupts and supersedes the last: you get three rollouts' worth of Pod churn to arrive at one final state.

---

**Checkpoint: you've now mastered**

✓ What a rolling update actually does, and the two bounds that shape it
✓ Why `Recreate` exists and when choosing it is correct
✓ What makes a gradual replacement a safe one
✓ The exact rule for what creates a revision, what a rollback is, and what `revisionHistoryLimit` buys you

🗺️ Chart → 🌊 **Passage** → 🌅 Dawn — you are past the halfway point, and past the hardest section.

☐ The rest of the workload family (next)
☐ What happens when anyone can write a controller

---

## 🔵 §6 — When Pods Are Not Interchangeable

Everything so far has quietly rested on one assumption, and it is time to name it.

A Deployment is a good fit for managing a stateless application workload where **any Pod in the Deployment is interchangeable** and can be replaced if needed [source: k8s-docs-workloads-2026-08-23]. That is why a count plus a template is a sufficient description of the whole workload. If any Pod can stand in for any other, then "three of these" says everything there is to say. It is also why §2's demonstration was unremarkable: the replacement Pod had a different name and a different UID and nothing cared, because nothing was depending on *which one it was*.

Now ask Soundings question 4 again. What if they are not interchangeable? What if this one is the primary and that one is the replica, each holding data that belongs to it specifically, each reachable at an address the others have written down?

### The resource

A **StatefulSet** runs a group of Pods and maintains a sticky identity for each of them, which is useful for managing applications that need persistent storage or a stable, unique network identity [source: k8s-docs-statefulset-2026-08-24]. The pivotal sentence: like a Deployment, a StatefulSet manages Pods based on an identical container spec, but unlike a Deployment, it maintains a sticky identity for each Pod, and **these Pods are created from the same spec but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling** [source: k8s-docs-statefulset-2026-08-24].

That identity is concrete, not conceptual. For a StatefulSet with N replicas, each Pod is assigned an integer ordinal unique across the set — by default, from 0 through N−1 — and each Pod derives its hostname from the StatefulSet's name and its own ordinal. The pattern is `$(statefulset name)-$(ordinal)`, so a three-replica StatefulSet named `web` produces `web-0`, `web-1` and `web-2` [source: k8s-docs-statefulset-2026-08-24].

Storage sticks to the identity too. For each volume claim template defined in a StatefulSet, each Pod receives one PersistentVolumeClaim, and **the same claim will be bound to that Pod throughout its lifecycle**; when the Pod is rescheduled onto a different node, its mounts follow [source: k8s-docs-statefulset-2026-08-24]. This is what the workloads overview means when it says a StatefulSet matches each Pod with a PersistentVolume, and that code running in those Pods can replicate data to other Pods in the same StatefulSet to improve overall resilience [source: k8s-docs-workloads-2026-08-23].

And the ordering is guaranteed rather than incidental: for a StatefulSet with N replicas, Pods are created sequentially in order from 0 to N−1 and terminated in reverse order from N−1 to 0, and before a scaling operation is applied to a Pod, all of its predecessors must be Running and Ready [source: k8s-docs-statefulset-2026-08-24].

<!-- FIGURE: ch06-fig05-statefulset-vs-deployment-identity -->
```
  Deployment — Pods are interchangeable

     web-7d4b-x9k2      web-7d4b-mn4p      web-7d4b-qq8j
                             ✗ dies
                               │
                               └──▶  web-7d4b-z7rt
                                     new name, new UID.
                                     Nothing depended on which one it was.


  StatefulSet — identity is sticky, and the storage belongs to the identity

     db-0 ──┐           db-1 ──┐           db-2 ──┐
            │                  │                  │
        [ vol db-0 ]       [ vol db-1 ]       [ vol db-2 ]
       ✗ dies  ▲
         │     │
         └──▶ db-0 reattaches here
              same name, same volume.
              The identity outlived the Pod.
```

**Figure 6.4 — the storage belongs to the identity, not to the Pod.** Look at the lower row carefully. The volume is not drawn attached to a Pod; it is drawn attached to `db-0`, which is a slot that Pods pass through. That is the claim, and Chapter 11 is where it gets completed.

<!-- AUTHOR-REVIEW (figure bookkeeping, two items, neither corrected here because both would break the image-specs join key):
     (1) Anchor IDs and caption numbers are transposed for the fourth and fifth figures. `ch06-fig05-statefulset-vs-deployment-identity` carries caption "Figure 6.4"; `ch06-fig04-workload-resource-decision-tree` carries caption "Figure 6.5". Caption numbering is internally consistent (6.1–6.6) and every in-text reference — including the Exam Alert's "Figure 6.5" for the decision tree — matches the captions, so the captions are load-bearing and the anchor IDs are the outlier. Fixing means swapping the two `figNN` tokens in BOTH the draft anchors and image-specs.md in one edit.
     (2) `ch06-zenith-control-loop-instantiated` (§9) does not match the `ch{NN}-fig{MM}-{slug}` pattern; the contract also permits `chNN-zenith-slug`, so it is legal, but if the author prefers sequence conformance the ID would become `ch06-fig06-control-loop-instantiated`, again requiring a matching image-specs edit. -->

> ★ **Fixed Point:**
>
> **The property that distinguishes a StatefulSet from a Deployment is whether the Pods are interchangeable, not whether the application writes to disk.**
>
> StatefulSet is for related Pods with stable, sticky identities, each typically paired with its own durable storage that follows the identity rather than the Pod.

> 🪝 **Snag:** "It writes to disk, so it needs a StatefulSet." No. A stateless web server can write to disk (caches, temp files, uploaded images on a shared volume) and a Deployment's Pods can mount volumes perfectly well. The question is never *does it write*. The question is: **if I destroyed this Pod and a differently-named Pod appeared in its place, would anything be broken?** If the answer is no, it is a Deployment, disk or no disk.

> **Extended Analogy:** A Deployment's Pods are a watch rotation. Any qualified hand can stand any watch; the roster says "three on deck," not "these three on deck," and when someone goes below you send up whoever is next. The order is a number and a qualification.
>
> A StatefulSet's Pods are a pilot who knows this harbor. The order is not "one pilot." It is *this* pilot, who has the approach notes for this specific entrance, whose knowledge is not transferable by handing someone else the same job title. If that pilot is relieved, the relief has to be given the same approach notes, the same depths, and the same name on the manifest, or the ship goes aground while everyone insists the roster is full.
>
> Both are legitimate ways to staff a task. Confusing them costs you in exactly one direction: treat interchangeable crew as irreplaceable and you carry unnecessary machinery; treat irreplaceable crew as interchangeable and you lose data.

### A loop left open on purpose

You have now been told that a StatefulSet's Pods each get their own persistent storage, and you have not been told how that storage is provisioned, requested, sized, reclaimed, or shared. That is deliberate, and you should know it is deliberate rather than wonder what got skipped.

The storage half of this — PersistentVolume, PersistentVolumeClaim, StorageClass, access modes, and the provisioning path — is a chapter of its own, and it needs vocabulary this chapter has not built.

<!-- AUTHOR-REVIEW: two Chapter 11 facts were cut from this paragraph in revision, per the curriculum-alignment stage and research-manifest note 8 — that a StatefulSet's storage must be provisioned by a PV provisioner from the requested storage class or pre-provisioned by an admin, and that deleting or scaling down a StatefulSet does NOT delete the associated volumes [source: k8s-docs-statefulset-2026-08-24]. The second one should move into ch06-fig05's DESIGN BRIEF (not the reader's prose), where it is the cleanest evidence for the figure's requirement that storage belongs to the identity rather than to the Pod. -->

*[cross-bearing: see Ch 11 — PersistentVolumes, claims, and how a Pod's storage follows its identity]*

One more open thread, smaller: StatefulSets currently require a headless Service to be responsible for the network identity of the Pods, and you are responsible for creating it [source: k8s-docs-statefulset-2026-08-24]. What a headless Service is belongs with the rest of Services. *[cross-bearing: see Ch 9 — headless Services and stable DNS names]*

*[cross-bearing: see Ch 16 — debugging StatefulSets and their claims]*

<!-- AUTHOR-REVIEW: chapter-01 line 435 carries a published cross-bearing reading "*[see Ch 6 §3 — StatefulSets and stable identity]*". StatefulSet is §6 in this chapter, and §3 is pinned by chapter-04 line 688 (selectors and ownership), which cannot move. Per the outline's Open Question #1, the recommended fix is a one-token edit in chapter-01: §3 → §6. Not fixable from inside this draft. -->

---

## ⚪ §7 — One Per Node, and Work That Ends

Three more resources, one defining property each, and then the figure that collects all six.

### DaemonSet — one per node

A **DaemonSet** ensures that all (or some) nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them; as nodes are removed, those Pods are garbage collected. Deleting the DaemonSet cleans up the Pods it created [source: k8s-docs-daemonset-2026-08-24].

Read the first clause again, because the whole resource is in it: *as nodes are added, Pods are added to them.* You never revisit the DaemonSet when the cluster grows. The order was written about the station, not about the number of hands standing it.

The workloads overview puts the purpose well: a DaemonSet defines Pods that provide facilities local to nodes, and each Pod performs a job similar to a system daemon on a classic Unix or POSIX server [source: k8s-docs-workloads-2026-08-23]. The typical uses are all recognizably that shape: running a cluster storage daemon on every node, a log-collection daemon on every node, a node-monitoring daemon on every node [source: k8s-docs-daemonset-2026-08-24]. A DaemonSet might be fundamental to the operation of the cluster, such as a plugin to run cluster networking; it might help you manage the node; or it might provide optional behavior that enhances the platform [source: k8s-docs-workloads-2026-08-23].

Two of those come back later. Cluster networking plugins ship as DaemonSets *[cross-bearing: see Ch 9 — CNI plugins and how Pod networking gets implemented]*, and node-level log agents are the canonical observability example *[cross-bearing: see Ch 18 — node-level log collection]*.

The Pod count is a consequence, not a setting. If you specify a node selector or node affinity in the template, the DaemonSet controller creates Pods on nodes matching it; if you specify neither, it creates Pods on all nodes [source: k8s-docs-daemonset-2026-08-24]. The controller creates a Pod for each eligible node [source: k8s-docs-daemonset-2026-08-24]. Supporting this from another direction: horizontal pod autoscaling does not apply to objects that can't be scaled, and the documentation's own example of such an object is a DaemonSet [source: k8s-docs-hpa-2026-08-24]. *[cross-bearing: see Ch 7 §3 — nodeSelector and node affinity]*

One more thing to bank, because Chapter 7 collects it. DaemonSets keep running on nodes where nothing else will — nodes the cluster has fenced off from ordinary workloads entirely. And you have already met the mechanism that makes this possible, in disguise: it has been holding those networking and logging agents in place on every node since you first saw them running everywhere in Chapter 3's census. Chapter 7 unmasks it *[cross-bearing: see Ch 7 §4 — taints, tolerations, and the fence DaemonSets step over]*.

<!-- AUTHOR-REVIEW: no cached sentence states in so many words that a DaemonSet has no `replicas` field. The claim is supported by (a) "creates a Pod for each eligible node" [k8s-docs-daemonset-2026-08-24] and (b) the HPA page naming DaemonSet as an object that can't be scaled [k8s-docs-hpa-2026-08-24]. Prose here, in the §7 Fixed Point, and in the Chapter Summary all use the hedged form — the count is a consequence of node eligibility — rather than asserting field absence. The stronger form needs the DaemonSet API reference fetched (research gap G-6A). -->

### Job — work that ends

Jobs represent one-off tasks that run to completion and then stop. A Job creates one or more Pods and continues to retry execution until a specified number of them successfully terminate; as Pods complete, the Job tracks the successful completions, and when the specified number is reached the Job is complete. Deleting a Job cleans up the Pods it created [source: k8s-docs-job-2026-08-24].

The simple case is one Job object reliably running one Pod to completion, and the Job will start a new Pod if the first one fails or is deleted, for example due to node hardware failure or a node reboot [source: k8s-docs-job-2026-08-24]. Note the shape of that: it is still the control loop. The desired state is just *completion* rather than *a count of running things*.

Chapter 5 taught you five Pod phases and gave you an immediate use for three of them. Here are the other two. `Succeeded` means all containers in the Pod terminated in success and will not be restarted; `Failed` means all containers terminated and at least one terminated in failure [source: k8s-docs-pod-lifecycle-2026-08-23]. For everything in §1 through §6, those two phases were terminal states you hoped never to see. For a Job, `Succeeded` is the *point*. *[cross-bearing: see Ch 5 §5 — the five Pod phases]*

Consistent with that, a Job's Pod template may only use a `restartPolicy` of `Never` or `OnFailure` [source: k8s-docs-job-2026-08-24]. `Always` is not permitted, and once you have the concept, that restriction writes itself: a Pod that is always restarted can never complete.

### CronJob — work that ends, repeatedly

A **CronJob** creates Jobs on a repeating schedule, and one CronJob object is like one line of a crontab file on a Unix system [source: k8s-docs-cronjob-2026-08-24]. It is meant for regular scheduled actions such as backups and report generation [source: k8s-docs-cronjob-2026-08-24].

The `.spec.schedule` field is required and follows standard Cron syntax, five fields, minute through day-of-week, so `0 3 * * 1` means weekly on a Monday at 3 a.m. [source: k8s-docs-cronjob-2026-08-24]. You can set `.spec.timeZone` to a valid time zone name to control how the schedule is interpreted [source: k8s-docs-cronjob-2026-08-24]. The `.spec.jobTemplate` defines the Jobs it creates and has exactly the same schema as a Job, nested, without its own `apiVersion` or `kind` [source: k8s-docs-cronjob-2026-08-24]: the same nesting move you saw with Pod templates in §1, one level further up.

One caution that is worth its space because it bites in production: a CronJob creates a Job **approximately** once per execution time of its schedule. The scheduling is approximate because there are circumstances where two Jobs might be created, or none. Kubernetes tries to avoid those situations but does not completely prevent them, therefore the Jobs you define **should be idempotent** [source: k8s-docs-cronjob-2026-08-24]. Write the nightly report generator so that running it twice produces one report, not two.

### The decision

Six resources. Four questions. Get the questions in the right order and the three most common wrong turns disappear.

<!-- FIGURE: ch06-fig04-workload-resource-decision-tree -->
```
                        Does the work END?
                    ┌──────────┴──────────┐
                  yes                     no
                   │                       │
        Does it repeat on          Must it run on
          a schedule?               EVERY node?
        ┌─────┴─────┐              ┌─────┴─────┐
      yes           no           yes           no
       │             │            │             │
   CronJob         Job        DaemonSet   Are the Pods
                                          INTERCHANGEABLE?
                                          ┌─────┴─────┐
                                        yes           no
                                         │             │
                                    Deployment    StatefulSet
                                  (which manages
                                   a ReplicaSet)
```

**Figure 6.5 — ask about the work before you ask about the application.** The first question is about the shape of the work, not the nature of the software. That ordering is deliberate, and the next block explains why.

The documentation offers the same guidance from the ReplicaSet's side, phrased as alternatives: use a Job instead of a ReplicaSet for Pods expected to terminate on their own; use a DaemonSet instead of a ReplicaSet for Pods providing a machine-level function such as machine monitoring or machine logging; and use a Deployment when you want ReplicaSets, since Deployments own and manage them for you [source: k8s-docs-replicaset-2026-08-24].

> ★ **Fixed Point:**
>
> **DaemonSet: one Pod per eligible node, added automatically as nodes join. The count is a consequence of the cluster, not a setting.**
> **Job: runs a task to completion, once.**
> **CronJob: creates the same Job repeatedly, on a schedule.**

> ⚠ **Navigational Hazards**
>
> Three misconceptions cluster around this section, and they share one root cause, so learn the root cause instead of memorizing three corrections.
>
> **The root cause: people choose a workload resource by what the application *is*, rather than by how its Pods need to be *managed*.** Every one of the following is that mistake wearing a different coat.
>
> **"It's a database, so it needs a StatefulSet."** The application being a database is not the criterion. Interchangeability is. A single-replica read-only cache backed by an ephemeral volume is fine as a Deployment even though it is technically a datastore; a three-member quorum where each member has a distinct identity needs a StatefulSet even if the data is tiny. Ask what happens when one Pod is replaced by a differently-named one, and let the answer decide.
>
> **"I need six copies for capacity, so I'll use a DaemonSet."** A DaemonSet does not express a number. It creates a Pod for each eligible node [source: k8s-docs-daemonset-2026-08-24], so you get however many nodes are eligible: possibly three, possibly sixty, and different tomorrow. If you want six, you want a Deployment with `replicas: 6`. Use a DaemonSet when the requirement is genuinely *per host*, which usually means the Pod is doing something to or about the machine it is sitting on.
>
> **"Job and CronJob both run scheduled work."** No. A Job runs a task to completion once [source: k8s-docs-job-2026-08-24]. A CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24]. The CronJob is not a kind of Job. It is a thing that *makes* Jobs, the way a Deployment is not a kind of ReplicaSet but a thing that makes ReplicaSets. Once you notice that both pairs have the same shape, the distinction stops being something to memorize.
>
> Run the tree in Figure 6.5 in order and none of these three can happen, because the tree asks about the work before it asks about the software.

*[cross-bearing: see Ch 7 §4 — a DaemonSet's Pods still go through scheduling, and taints are how a node opts out]*

---

## 🟡 §8 — The Control Loop, Extended

Chapter 3 closed by promising you controllers you configure yourself. Chapter 2 named custom resources as the fourth socket in the pattern where Kubernetes defines an interface and lets the ecosystem implement it. Both promises come due here.

<!-- AUTHOR-REVIEW: chapter-02 line 600 carries a published cross-bearing reading "*[see Ch 6 §3 — CRDs and extending the API]*". CRDs are §8 in this chapter; §3 is pinned by chapter-04 line 688 and cannot move, and CRDs cannot move earlier than §8 without teaching API extension before the reader has met a built-in controller. Per the outline's Open Question #1, the recommended fix is a one-token edit in chapter-02: §3 → §8. Not fixable from inside this draft. -->

### Start with the word "resource"

A resource is an endpoint in the Kubernetes API that stores a collection of API objects of a certain kind; the built-in `pods` resource contains a collection of Pod objects [source: k8s-docs-custom-resources-2026-08-23]. You have been using resources all book. `kubectl get pods` talks to one. `kubectl get deployments` talks to another.

A **custom resource** is an extension of the Kubernetes API that is not necessarily available in a default Kubernetes installation; it represents a customization of a particular installation. Custom resources can appear and disappear in a running cluster through **dynamic registration**, and cluster admins can update them independently of the cluster itself [source: k8s-docs-custom-resources-2026-08-23].

Here is the clause that makes it click: once a custom resource is installed, users create and access its objects using `kubectl`, **just as they do for built-in resources like Pods** [source: k8s-docs-custom-resources-2026-08-23]. Nothing about the tooling changes. `kubectl get`, `kubectl describe`, `kubectl apply`, labels, selectors, namespaces, RBAC, all of it works on the new kind, because the new kind lives in the same API. *[cross-bearing: see Ch 12 — RBAC, where this permission model is taught]*

### The object that does the installing

The **CustomResourceDefinition**, the CRD, is the API resource that lets you define custom resources. Defining a CRD object creates a new custom resource with a name and schema that you specify, and the Kubernetes API then serves and handles the storage of it for you. This frees you from writing your own API server, though the generic nature of the implementation means you have less flexibility than with API-server aggregation [source: k8s-docs-custom-resources-2026-08-23].

Many core Kubernetes functions are now built using custom resources, which is part of what makes Kubernetes modular [source: k8s-docs-custom-resources-2026-08-23]. This is not an exotic corner of the platform. It is one of the main ways the platform grows.

### The honest limitation

**On their own, custom resources let you store and retrieve structured data.** That is all [source: k8s-docs-custom-resources-2026-08-23].

Sit with that for a second, because it is the thing that surprises people. A CRD by itself is a shape in a database. You can create objects of that kind, list them, label them, and delete them. Nothing else happens. No Pods appear. No infrastructure is provisioned. You have defined a noun and taught the API server to store it.

> ★ **Fixed Point:**
>
> **A custom resource on its own stores and retrieves structured data. A custom resource combined with a custom controller is the operator pattern.**

When you combine a custom resource with a custom controller, custom resources provide a true declarative API. The Kubernetes declarative API enforces a separation of responsibilities: you declare the desired state of your resource, and the controller keeps the current state of Kubernetes objects in sync with your declared desired state. This is in contrast to an imperative API, where you instruct a server what to do [source: k8s-docs-custom-resources-2026-08-23].

That is Chapter 3's control loop, written by someone who is not the Kubernetes project. The published description of the controller extension pattern makes the shape explicit: controllers are client programs that read and/or write to the Kubernetes API, following a control loop, reading an object's `.spec`, possibly doing things, and then updating the object's `.status` [source: k8s-docs-extending-kubernetes-2026-08-23]. Read `.spec`, act, write `.status`. Nothing about that sentence is privileged. Anyone can write a program that does it.

> 🪝 **Snag:** "We installed the CRD, created an object of the new kind, and nothing happened." That is the correct behavior. There is no controller. You gave the cluster a new noun and no verb.
>
> **Name this shape, because you are going to meet it again.** *An object without its component does nothing.* An Ingress with no ingress controller is the same shape. `kubectl top` with no metrics-server is the same shape. A vertical autoscaler that isn't shipped by default is the same shape. It is not four gotchas. It is one rule with four instances, and the rule is that Kubernetes will happily accept a record of intent that nothing in the cluster is currently able to act on. *[cross-bearing: see Ch 10 — Ingress without an ingress controller]* *[cross-bearing: see Ch 13 — `kubectl top` without metrics-server]*

### The pattern, named

The **operator pattern** combines custom resources and custom controllers [source: k8s-docs-custom-resources-2026-08-23].

What it is for is more interesting than what it is. The pattern aims to capture the key aim of a human operator who is managing a service, someone with deep knowledge of how the system ought to behave, how to deploy it, and how to react if there are problems, and to write that knowledge as code that automates a task beyond what Kubernetes itself provides [source: k8s-docs-operator-pattern-2026-08-23]. The mechanism is unglamorous and precise: operators are clients of the Kubernetes API that act as controllers for a custom resource, and the pattern lets you extend the cluster's behavior without modifying the code of Kubernetes itself [source: k8s-docs-operator-pattern-2026-08-23].

The published list of things people automate this way is the fastest way to make it concrete [source: k8s-docs-operator-pattern-2026-08-23]:

- deploying an application on demand
- taking and restoring backups of that application's state
- handling upgrades of the application code alongside related changes such as database schemas or extra configuration settings
- publishing a Service so applications that don't support Kubernetes APIs can discover them
- simulating failure in all or part of a cluster to test its resilience
- choosing a leader for a distributed application that has no internal election process

Every one of those is somebody's 2 a.m. runbook, turned into a loop that never sleeps.

And now the closing turn, which is the reason §8 sits after §1 rather than before it. The most common way to deploy an operator is to add the CustomResourceDefinition and its associated controller to your cluster, and **the controller will normally run outside of the control plane, much as you would run any containerized application: for example, as a Deployment** [source: k8s-docs-operator-pattern-2026-08-23].

The thing that extends Kubernetes is itself deployed *by* Kubernetes, using the first resource in this chapter. The operator that manages your database is three replicas of a container image, held at a count by a ReplicaSet, held at a template by a Deployment. It is not a plugin. It is not privileged. It sails under the same standing orders as everything else in the fleet, and everything §1 through §5 told you about workloads applies to it unchanged.

### The fourth socket

Chapter 2 showed you the move: Kubernetes defines an interface and lets the ecosystem implement it. You met it with the container runtime, with networking, and with storage, and you were told you would meet it once more at the API layer. This is that. The published extension points list **API extensions, Custom Resource Definitions (CRDs) and the API aggregation layer,** as one of six categories, alongside controllers, scheduling extensions, API access extensions, kubectl plugins, and infrastructure extensions [source: k8s-docs-extending-kubernetes-2026-08-23].

Four sockets, one pattern. Collecting them into a single statement about what kind of system Kubernetes is belongs later, when you have met all four in their own contexts. *[cross-bearing: see Ch 17 — CRI, CNI, CSI and CRDs, resolved into one story]*

> 🔭 **Closer Look:** CRDs are not the only route to a custom API. The other is API-server aggregation, which offers more flexibility at the cost of writing and operating more of the API machinery yourself [source: k8s-docs-custom-resources-2026-08-23]. For this book's purposes: CRD is the common path, aggregation is the rarer one, and knowing that both exist is enough.

*[cross-bearing: see Ch 14 — why Helm charts have a `crds/` directory]*
*[cross-bearing: see Ch 15 — a delivery tool that is, structurally, a controller acting on custom resources]*

---

## ☆ Taking Your Bearings #3: The Rest of the Fleet, and Extending It

Five questions on the rest of the family and the pattern extended.

**1.** 🔵 An application writes to a local disk. Does that mean it needs a StatefulSet? Answer in one sentence, and name the property that actually decides.

**2.** 🔵 You need six copies of a service running for capacity. A colleague suggests a DaemonSet. What is wrong with that suggestion, and what determines a DaemonSet's Pod count?

**3.** 🔵 Nightly at 02:00, a report has to be generated, and the process must exit when it is done. Name the resource you would create, and name the resource it creates each time it fires.

**4.** 🔵 You install a CRD for a resource called `Backup`, then create a `Backup` object. `kubectl get backup` shows it. Nothing else happens: no Pods, no snapshots, no events. Is the cluster broken?

A) Yes — the CRD's schema is misconfigured.
B) Yes — custom resources have to be created in `kube-system`.
C) No — a custom resource on its own only stores structured data; nothing acts on it without a controller.
D) No — CRD objects take up to ten minutes to register.

**5.** 🟡 An operator manages a database. Where does the operator's own controller run, and using which of this chapter's resources?

---

**Answers with Explanations**

**1.** No. The deciding property is whether the Pods are **interchangeable**. A Deployment's Pods can mount volumes and write to them; what a Deployment assumes is that any Pod in it can be replaced by any other [source: k8s-docs-workloads-2026-08-23]. A StatefulSet exists for Pods that are created from the same spec but are *not* interchangeable, each carrying a persistent identifier across rescheduling [source: k8s-docs-statefulset-2026-08-24].

The wrong version of this answer, "yes, disk means StatefulSet," is worth naming because it is an easy one to arrive with, and it fails in both directions. It puts unnecessary machinery around stateless services that happen to cache to disk, and it leaves genuinely identity-dependent workloads in Deployments, where a routine Pod replacement quietly returns the wrong data.

**2.** A DaemonSet does not express a count. The controller creates a Pod for each eligible node [source: k8s-docs-daemonset-2026-08-24], so the Pod count is a consequence of how many nodes match, which is a property of the cluster and changes as nodes join and leave [source: k8s-docs-daemonset-2026-08-24]. On a nine-node cluster you would get nine, not six, and on a cluster that grew to twenty you would get twenty. Supporting evidence from another angle: horizontal pod autoscaling explicitly does not apply to a DaemonSet, because it is not an object that can be scaled [source: k8s-docs-hpa-2026-08-24].

For six copies, use a Deployment with `replicas: 6`.

**3.** A **CronJob**, which creates a **Job** at each scheduled time. A CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24]; the Job is the thing that actually runs to completion and stops [source: k8s-docs-job-2026-08-24]. The schedule for 02:00 daily is `0 2 * * *` in the standard five-field Cron syntax [source: k8s-docs-cronjob-2026-08-24].

If your answer was "a Job with a schedule on it," re-read §7's hazards block. The relationship between CronJob and Job is the same relationship as between Deployment and ReplicaSet: the outer object makes the inner one.

**4. C.** Nothing is broken. On their own, custom resources let you store and retrieve structured data [source: k8s-docs-custom-resources-2026-08-23]. You have taught the API server a new kind of object and given it nowhere to go. What makes a custom resource *do* something is combining it with a custom controller, which is what turns it into a true declarative API [source: k8s-docs-custom-resources-2026-08-23].

- **A is wrong** because a misconfigured schema would have shown up at CRD creation or at object creation. Your object was accepted and is retrievable; the API layer is working exactly as designed.
- **B is wrong** because namespace has nothing to do with it. Custom resource objects live wherever their scope allows, and `kube-system` confers no special activation.
- **D is wrong** because registration is not delayed; custom resources appear and disappear in a running cluster through dynamic registration [source: k8s-docs-custom-resources-2026-08-23]. Waiting longer will not help.

**Name the pattern, because you will retrieve it by name:** *an object without its component does nothing.* You will meet this exact shape at least three more times in this book. Each time, the first instinct will be "something is misconfigured," and each time the answer will be "something is not installed."

**5.** Outside the control plane, as an ordinary containerized workload, **normally a Deployment** [source: k8s-docs-operator-pattern-2026-08-23]. The operator is a client of the Kubernetes API acting as a controller for a custom resource [source: k8s-docs-operator-pattern-2026-08-23]; it has no privileged position in the architecture and no special deployment mechanism. It is a container image, held at a replica count by a ReplicaSet, held at a template by a Deployment, exactly like everything else you have run this chapter.

If you answered "in the control plane," or "as a static Pod on the control-plane nodes," or "it's installed into the API server," that is the misconception this item exists to catch, and it is worth spending thirty seconds on. An operator is not a component of Kubernetes; it is a *client* of it, with exactly the access its RBAC grants and exactly the deployment story any other container has. Carrying the wrong version of this makes Chapter 15's central move — a delivery tool that is structurally just another controller — read as a special case instead of as the ordinary case.

This item required §1 and §8 together, and it is the direct precursor to a recognition Chapter 15 depends on. Hold onto it.

---

**Checkpoint: you've now mastered**

✓ The property that separates a StatefulSet from a Deployment
✓ Three sibling resources, each by its one defining property
✓ The decision tree, and why its question order matters
✓ Custom resources, custom controllers, and the pattern that is both

---

## ☀️ §9 — Nobody Sails One Pod

Nothing new here. Just one thing seen properly.

Take Chapter 3's control loop, the one you retrieved in Soundings question 7 and filled in for a ReplicaSet in ☆ Taking Your Bearings #1, and plug this chapter's controllers into it one at a time.

<!-- FIGURE: ch06-zenith-control-loop-instantiated -->
```
                    ┌───────────────────────────┐
                    │      DESIRED STATE        │
                    └─────────────┬─────────────┘
                                  │
                               compare
                                  │
                    ┌─────────────▼─────────────┐
                    │      CURRENT STATE        │
                    └─────────────┬─────────────┘
                                  │
                          act on the gap
                                  │
                                  └──────▶ (and again, forever)


   Change only what you plug into DESIRED STATE, and you have
   named every controller in this chapter:

        a number ............................  ReplicaSet
        a template + an update policy .......  Deployment
        one per matching node ...............  DaemonSet
        completion ..........................  Job
        a Job existing at each scheduled time  CronJob
        whatever its author decided .........  your operator
```

**Figure 6.6 — one loop, six desired states.** The loop is drawn once. That is the argument.

> ☀️ **Zenith:** Six resources. One shape. You have been looking at the same diagram for the entire chapter.
>
> The ReplicaSet's desired state is a number. The Deployment's is a template plus a policy for changing it. The DaemonSet's is *one per matching node*: a number, but one the cluster computes rather than one you write. The Job's is *completion*. The CronJob's is *a Job existing at each scheduled time*. The operator's is whatever its author decided a database, or a certificate, or a message queue ought to look like.
>
> Nothing was added to the loop to accommodate any of them. Nothing needed to be.

And now the part that carries forward. That shape is not a Kubernetes implementation detail, a way the maintainers happened to build some controllers. It is what Kubernetes *is*. §8 already showed you that anyone can write a controller: read an object's `.spec`, do things, write its `.status` [source: k8s-docs-extending-kubernetes-2026-08-23]. There is no line in the architecture separating the loops Kubernetes ships from the loops you write.

Which means the last question left is where the desired state lives. So far it has always lived in the cluster: an object you created with `kubectl apply`, stored by the API server, watched by a controller. There is no rule that says it has to. *[cross-bearing: see Ch 15 — a controller whose desired state lives in a Git repository, and why that is the same technology rather than a new one]*

When you meet that, it will look like a new idea for about ten seconds.

Which returns you to the title. Nobody sails one Pod, not because a single Pod is forbidden, and not because Pods are unimportant. A single Pod is a statement about right now. Every resource in this chapter is a statement about what should keep being true. That is the whole difference, and it is why you will stop reaching for `kubectl run` without ever making a decision to stop.

---

## Exam Alert! 🚨

**High-priority topics, in descending order of how much of this chapter depends on them.**

1. **The workload-resource decision.** Which resource for which shape of work. Figure 6.5 is the single highest-value artifact in this chapter; it collapses three separate misconceptions into one traversal.
2. **Deployment versus StatefulSet is about interchangeability, not disk.** A StatefulSet's Pods are created from the same spec but are not interchangeable [source: k8s-docs-statefulset-2026-08-24]; a Deployment suits workloads where any Pod is interchangeable [source: k8s-docs-workloads-2026-08-23].
3. **DaemonSet is one Pod per eligible node,** added automatically as nodes join [source: k8s-docs-daemonset-2026-08-24]. The count is a consequence of the cluster.
4. **Job runs to completion once; CronJob creates Jobs on a schedule** [source: k8s-docs-job-2026-08-24] [source: k8s-docs-cronjob-2026-08-24].
5. **The ownership chain: Deployment → ReplicaSet → Pod,** and which layer holds the template and which enforces the count [source: k8s-docs-deployment-2026-08-23] [source: k8s-docs-replicaset-2026-08-24].
6. **`RollingUpdate` is the default strategy; `maxSurge` and `maxUnavailable` both default to 25%; `Recreate` kills all old Pods before creating any new one** [source: k8s-docs-deployment-2026-08-23] [source: k8s-docs-deployment-spec-fields-2026-08-24].
7. **A revision is created if and only if the Pod template changes.** Scaling does not create one [source: k8s-docs-deployment-2026-08-23].
8. **A CRD alone stores structured data; a CRD plus a custom controller is the operator pattern** [source: k8s-docs-custom-resources-2026-08-23].

**Common traps.**

| Trap | The correction |
|---|---|
| "StatefulSet is for apps that write to disk" | The property is interchangeability. Deployment Pods can write to disk. |
| "Use a DaemonSet to run several copies" | A DaemonSet expresses *per node*, not a number. Six copies is a Deployment. |
| "Job and CronJob are two ways to schedule work" | A Job runs once. A CronJob *creates Jobs*. Same relationship as Deployment → ReplicaSet. |
| "Scaling creates a revision" | Only a `.spec.template` change does. |
| `maxSurge` and `maxUnavailable` transposed | Surge bounds *total*. Unavailable bounds *available*. Surge rounds up, unavailable rounds down. |
| "`Recreate` is a mistake" | It is a supported strategy with a stated cost. Choosing it deliberately is correct engineering. |
| "Installing a CRD makes something happen" | It defines a noun. Nothing acts on it until a controller exists. |
| "`revisionHistoryLimit: 0` just tidies up" | It also removes the ability to undo the next rollout. |

**The single most useful thing to internalize:** all three of the resource-selection traps are the same error. People choose a workload resource by what the application *is* rather than by how its Pods need to be *managed*. Run Figure 6.5's questions in order (does the work end, must it run on every node, are the Pods interchangeable) and you cannot arrive at any of the three.

---

## Practice Questions

Nineteen questions. Answers and explanations follow the full set, so work them all first.

<!-- AUTHOR-REVIEW (question coverage, for the author to rule on): Q3 and Q7 were re-cut in revision because each duplicated a ☆ Taking Your Bearings item (Q3 ≡ Bearings #1 item 3; Q7 ⊂ Bearings #2 item 1). The two freed slots now close the `revisionHistoryLimit` gap and the "neither bound may be 0 if the other is 0" gap. THREE taught concepts remain untested and cannot be covered without raising the chapter's question budget above the outline's 42: (a) HorizontalPodAutoscaler — taught in §2, in the Chapter Summary, cited in Q14's key, never the object of a question; (b) overlapping selectors — a full Logbook Entry sidebar in §3 with no retrieval path (Q4 tests bare-Pod adoption, which is adjacent but not the same mechanism); (c) CronJob idempotency and the five-field `.spec.schedule` syntax — flagged with emphasis in §7, source-backed, untested. `kubectl rollout status` is likewise the only verb in §5's table with no question behind it. The book is under its 300-question floor, so a raise from 42 to 45 is affordable if the author wants these closed. -->

---

**Q1.** ⚪ You create a Deployment with `replicas: 3`. Which object actually creates the three Pods?

A) The Deployment
B) The ReplicaSet the Deployment creates
C) The scheduler
D) The kubelet on each node

---

**Q2.** ⚪ **[retrieval: ch4]** On a Deployment, where does the number of replicas you *asked for* live, and where does the number *currently running* live?

A) Both in `spec`
B) Both in `status`
C) The requested count in `spec`; the running count in `status`
D) The requested count in `metadata`; the running count in `spec`

---

**Q3.** 🔵 You set `.spec.revisionHistoryLimit: 0` on a Deployment to stop old ReplicaSets accumulating in `etcd` and crowding `kubectl get rs`. What else have you given up?

A) Nothing — the field only controls how many entries `kubectl rollout history` prints
B) The ability to undo a new rollout, because its revision history is cleaned up
C) The ability to pause and resume a rollout
D) Rollbacks to revisions older than the previous one, but `rollout undo` with no arguments still works

---

**Q4.** 🔵 A ReplicaSet has `replicas: 3` and a selector of `app=web`. You manually create a bare Pod carrying the label `app=web`. What is the most likely outcome?

A) Nothing; bare Pods are never touched by controllers
B) The ReplicaSet adopts the Pod, is now over its desired count, and terminates a Pod
C) The API rejects the bare Pod for label conflict
D) The ReplicaSet scales up to four to accommodate it

---

**Q5.** 🔵 **[retrieval: ch5]** A ReplicaSet replaces a Pod that was deleted. What is true of the replacement, and why does it matter?

A) It is the same Pod restarted, retaining its UID and IP
B) It is a new Pod with a new UID; anything that recorded the old Pod's identity is now stale
C) It is the same Pod moved to a different node, retaining its name
D) It is a new Pod that reuses the old Pod's name but receives a new UID

---

**Q6.** ⚪ You run `kubectl delete deployment/web`. What happens to the ReplicaSets and Pods beneath it, and by what mechanism?

A) Nothing; they are independent objects and must be deleted individually
B) They are deleted by cascading deletion, driven by owner references
C) They are deleted because the selector no longer matches anything
D) They remain until the next garbage-collection window, which runs hourly

---

**Q7.** 🔵 A Deployment has eight replicas, with `maxSurge: 0` and `maxUnavailable: 1` set explicitly. What are the ceiling on total Pods and the floor on available Pods, and is this configuration legal?

A) Ceiling 8, floor 7; legal — the prohibition is only on setting *both* to 0
B) Ceiling 8, floor 7; illegal — `maxSurge` may never be 0
C) Ceiling 9, floor 7; legal — `maxSurge: 0` still permits one surge Pod for the swap
D) Ceiling 8, floor 8; legal — with no surge allowed, nothing may become unavailable either

---

**Q8.** 🔵 A Deployment has **six** replicas, with `maxSurge` and `maxUnavailable` both left at their defaults. What are the ceiling on total Pods and the floor on available Pods?

A) Ceiling 8, floor 5
B) Ceiling 7, floor 5
C) Ceiling 8, floor 4
D) Ceiling 7, floor 4

---

**Q9.** 🔵 Which of the following is the correct reason to choose `Recreate` over `RollingUpdate`?

A) It is faster, because Pods are not replaced one at a time
B) The application cannot tolerate two versions running simultaneously
C) It needs no spare capacity, because no surge Pods are ever created
D) It avoids the need for readiness probes

---

**Q10.** 🔵 You make two changes to a Deployment on Monday: you update the container image, and you scale from four replicas to eight. How many new revisions appear in `kubectl rollout history`?

A) Zero
B) One
C) Two
D) One, but only if the image change is applied second

---

**Q11.** 🔵 You run `kubectl rollout undo deployment/web`. Which statement best describes what the cluster does?

A) It restores a snapshot of the Deployment object taken before the last change
B) It sets the Pod template to the previous revision's value and runs the same rolling update in the other direction
C) It deletes the current ReplicaSet and recreates Pods from a backup
D) It reverses every field change made since the last rollout, including replica count

---

**Q12.** 🔵 You deploy a new image. The Pods start, but a bug means their readiness probes never succeed. Sixty seconds later, what is the state of the service and the Deployment?

A) The service is down; all Pods have been replaced with broken ones
B) The old Pods are still serving; the rollout has stalled with both ReplicaSets alive
C) The Deployment has automatically rolled back to the previous revision
D) The Pods are killed and restarted repeatedly until the image is fixed

---

**Q13.** 🔵 Which of these workloads most clearly requires a StatefulSet rather than a Deployment?

A) A web front end that caches rendered pages to a local disk
B) A message consumer that must never have two instances processing the queue simultaneously
C) A three-member clustered datastore whose members address each other by stable hostname and each own distinct data
D) A batch importer that writes its output to object storage

---

**Q14.** ⚪ Your cluster has twelve worker nodes. You create a DaemonSet with no node selector and no affinity. How many Pods will it produce, and what happens when three more nodes join?

A) One Pod; three more nodes changes nothing
B) Twelve Pods; three more nodes produces fifteen
C) Whatever `replicas` is set to; three more nodes changes nothing
D) Twelve Pods; three more nodes requires you to scale the DaemonSet

---

**Q15.** ⚪ A data pipeline must run once, process a file, and exit. A second pipeline must run the same processing every night at midnight. Which resources do you create?

A) Two Jobs, one with a schedule field set
B) A Job for the first; a CronJob for the second
C) A CronJob for both, with the first set to run once
D) A Deployment with `replicas: 1` for the first; a CronJob for the second

---

**Q16.** ⚪ **[retrieval: ch5]** Chapter 5 taught five Pod phases. Which phase indicates a Job's Pod has done its work correctly, and what does that phase mean?

A) `Running` — the container is still executing, which for a Job means progress
B) `Succeeded` — all containers terminated in success and will not be restarted
C) `Completed` — a Job-specific phase not available to other Pods
D) `Failed` — all containers terminated, at least one in failure

---

**Q17.** 🟡 A StatefulSet's Pods all match its label selector, exactly as a Deployment's do. A StatefulSet nevertheless guarantees something about its Pods that no selector could express. What is it, and what carries it?

A) That they are all running — carried by the readiness probe
B) That each Pod keeps a stable ordinal identity and hostname across rescheduling — carried by the Pod's ordinal and derived name, not by the selector
C) That there are exactly `.spec.replicas` of them — carried by the selector's match count
D) That they share a namespace — carried by the selector's scope

---

**Q18.** 🟡 You install a CRD defining a resource called `Certificate`, and you create a `Certificate` object. `kubectl get certificate` returns it. No certificate is issued. What is the minimum missing piece?

A) RBAC permissions granting access to the new resource
B) A controller that watches `Certificate` objects and acts on them
C) API aggregation, which CRDs require to function
D) A `status` subresource, without which nothing can act on the object

---

**Q19.** 🟡 **[retrieval: ch3]** What does a custom controller written by a third party have in common with a built-in controller such as the Deployment controller, and where does each of them run?

A) Nothing structural — custom controllers use a separate API and run as privileged processes inside the control plane
B) Both follow the same control loop — read `.spec`, act, write `.status` — but built-ins ship with the control plane while a custom controller normally runs as an ordinary Deployment
C) Both run inside the API server; the only difference is which resources each one watches
D) Both are registered with the API server through a CustomResourceDefinition, which is what makes a controller discoverable

---

### Answers & Explanations

**Q1 — B.** The Deployment creates a ReplicaSet, and the ReplicaSet creates Pods in the background [source: k8s-docs-deployment-2026-08-23]. **A** is the most common wrong answer and it collapses the middle layer; if you hold it, rolling updates become unexplainable, because they work by having two ReplicaSets alive at once. **C** is wrong: the scheduler decides *where* an existing Pod runs, not whether it exists. **D** is wrong for the same reason at a lower level: the kubelet runs containers for Pods already assigned to its node.

**Q2 — C.** Almost every Kubernetes object has a `spec` describing desired state, which you set at creation, and a `status` describing current state, supplied and updated by the system [source: k8s-docs-objects-2026-08-23]. The documentation uses this exact example: set the Deployment `spec` to three replicas, and Kubernetes starts three instances and updates the `status` to match [source: k8s-docs-objects-2026-08-23]. **A** and **B** each collapse the distinction that makes control loops possible; you cannot compare two states stored in one field. **D** is wrong because `metadata` holds identity, not intent.

**Q3 — B.** `.spec.revisionHistoryLimit` is the number of old ReplicaSets retained to allow rollback, defaulting to 10; setting it to zero means all old ReplicaSets with 0 replicas are cleaned up, and in that case a new Deployment rollout **cannot be undone**, since its revision history is cleaned up [source: k8s-docs-deployment-spec-fields-2026-08-24]. **A is wrong**, and it is the tempting one: the old ReplicaSets *are* the history. Deleting them removes the mechanism, not merely the display — which is why §5 insists that a revision is a ReplicaSet, not a log entry. **C is wrong** because pause and resume act on an in-flight rollout [source: k8s-docs-deployment-2026-08-23] and have nothing to do with retained ReplicaSets. **D is wrong** in the most useful way: `undo` with no arguments goes to the *previous* revision, and that is precisely the revision that no longer exists.

**Q4 — B.** A ReplicaSet identifies new Pods to acquire using its selector, and a Pod with no controller owner reference that matches will be immediately acquired [source: k8s-docs-replicaset-2026-08-24]. If the acquisition puts the ReplicaSet over its desired count, the newly acquired Pod is immediately terminated [source: k8s-docs-replicaset-2026-08-24]. **A** is wrong and dangerous: a ReplicaSet is explicitly not limited to owning Pods produced by its own template [source: k8s-docs-replicaset-2026-08-24]. **C** is wrong; labels are not unique keys and nothing at the API layer objects. **D** is wrong because the desired count is your declaration, not something the controller revises upward to accommodate surprises.

**Q5 — B.** A Pod is never rescheduled to a different node; it is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23], and higher-level controllers such as Deployments create those replacements [source: k8s-docs-pod-lifecycle-2026-08-23]. Why it matters: anything that recorded the old Pod's name, UID or IP address is now pointing at something that does not exist. **A** and **C** both preserve identity across replacement, which is exactly the thing that does not happen, and holding either of them is what makes Chapter 9's Services look like unnecessary machinery. **D is the trap worth understanding**, because it is *true of a different resource*: a StatefulSet's Pods do keep their ordinal-derived names across replacement [source: k8s-docs-statefulset-2026-08-24]. The stem says ReplicaSet, whose Pods carry generated names, so the replacement gets a new name as well as a new UID. Which resource is holding the Pods decides which answer is right.

**Q6 — B.** Owner references tell the control plane which objects depend on others, and Kubernetes deletes objects that no longer have owner references, like the Pods left behind when you delete a ReplicaSet, in a process called cascading deletion, with background cascading deletion as the default [source: k8s-docs-garbage-collection-2026-08-24]. **A** is wrong: the whole point of the owner-reference link is that dependents don't have to be tracked by hand. **C** confuses the two mechanisms; selection finds Pods, ownership governs deletion, and the documentation is explicit that ownership is different from labels and selectors [source: k8s-docs-garbage-collection-2026-08-24]. **D** invents a schedule; cascading deletion is not a periodic sweep.

**Q7 — A, ceiling 8 and floor 7, and it is legal.** `maxSurge` is the maximum number of Pods that may exist over the desired count, so 8 + 0 = 8; `maxUnavailable` is the maximum that may be unavailable, so 8 − 1 = 7 [source: k8s-docs-deployment-spec-fields-2026-08-24]. The legality turns on one clause: neither value may be 0 **if the other is 0** [source: k8s-docs-deployment-spec-fields-2026-08-24]. Here `maxUnavailable` is 1, so `maxSurge: 0` is permitted — and this is the configuration you reach for on a capacity-constrained cluster where there is no room for extra Pods. **B** overstates the rule into a blanket prohibition; the constraint is on the *pair*, because a rollout that may neither exceed nor drop below the desired count has no legal move. **C** invents a floor of one surge Pod; 0 means 0. **D** invents a coupling between the two fields, which is exactly the misconception §4's figure exists to kill: they bound different quantities in different directions.

**Q8 — A, ceiling 8, floor 5.** `maxSurge` = 25% of 6 = 1.5, rounded **up** to 2, so the ceiling is 6 + 2 = 8. `maxUnavailable` = 25% of 6 = 1.5, rounded **down** to 1, so the floor is 6 − 1 = 5 [source: k8s-docs-deployment-spec-fields-2026-08-24]. **B** rounds surge down. **C** rounds unavailable up. **D** rounds both the wrong way. Both defaults round in the direction of keeping more capacity online; if you can remember that sentence you can rebuild both rules from it.

**Q9 — B.** `Recreate` kills all existing Pods before new ones are created [source: k8s-docs-deployment-2026-08-23], which is the correct choice precisely when two versions must not coexist: a schema migration, an exclusive lock, a single-instance license. **A** is a rationalization: speed is not the reason, and the cost is a window of zero availability. **C is the best distractor here, and it is materially true** — `Recreate` does surge nothing, and people do reach for it on clusters with no headroom. It is still the wrong *reason*, because `maxSurge: 0` (with a non-zero `maxUnavailable`) gets you a zero-headroom rollout without the downtime window [source: k8s-docs-deployment-spec-fields-2026-08-24]. Choose `Recreate` for correctness, not for capacity. **D** is false and inverts the risk: with `Recreate` you have less protection, not more, because there is no overlap window in which a failing new version can be caught before the old one is gone.

**Q10 — B, one.** The image change modifies `.spec.template` and creates a revision. The scale changes `.spec.replicas`, and other updates such as scaling do not create a revision [source: k8s-docs-deployment-2026-08-23]. **A** ignores the image change. **C** is the intuitive answer, two edits and two entries, and it is the one this chapter exists to correct. **D** invents an ordering dependency; the rule is about *which field* changed, not about sequence.

**Q11 — B.** `kubectl rollout undo` rolls back to the previous revision [source: k8s-docs-deployment-2026-08-23], and a revision is a ReplicaSet holding a previous Pod template. Restoring it sets the template back and lets the same rolling update run in the other direction, bounded by the same `maxSurge` and `maxUnavailable` and gated by the same readiness checks. **A** is wrong because there is no snapshot of the whole object; the old ReplicaSets are what the history consists of, which is why `revisionHistoryLimit: 0` removes the ability to undo [source: k8s-docs-deployment-spec-fields-2026-08-24]. **C** invokes a backup system that does not exist here. **D** is wrong and is the practical trap: `undo` restores a Pod template, so it will not reverse a replica-count change.

**Q12 — B.** New Pods that never report ready never count as available [source: k8s-docs-deployment-spec-fields-2026-08-24], so the rollout cannot scale the old ReplicaSet down past the `maxUnavailable` floor. Both ReplicaSets stay alive; the old Pods keep serving. Readiness probe failures are named explicitly among the reasons a Deployment gets stuck without completing [source: k8s-docs-deployment-spec-fields-2026-08-24]. Meanwhile the failing readiness probe removes each broken Pod's IP from the endpoints of every matching Service [source: k8s-docs-pod-lifecycle-2026-08-23], so no traffic reaches them. **A** describes what happens *without* readiness probes, which is the point of having them. **C** is wrong: Kubernetes surfaces a `ProgressDeadlineExceeded` condition after `progressDeadlineSeconds` and keeps retrying [source: k8s-docs-deployment-spec-fields-2026-08-24]; it does not roll back for you. **D** describes a liveness-probe failure, which is a different probe doing a different job.

**Q13 — C.** Members that address each other by stable hostname and own distinct data are, by definition, not interchangeable, which is the criterion [source: k8s-docs-statefulset-2026-08-24]. **A** is the disk misconception: the cache writes to disk and is nonetheless perfectly happy in a Deployment, because replacing one Pod with a differently-named one breaks nothing. **B targets a different error — "singleton, therefore StatefulSet."** "Only one instance may run" is not the same claim as "the instances are not interchangeable." A Deployment with `replicas: 1` expresses it, and if you must guarantee no overlap even during a rollout, the strategy field is where you say so: `Recreate` [source: k8s-docs-deployment-2026-08-23]. Nothing in the requirement needs a sticky identity. **D** writes durable output but holds no identity; the importer could run as any Pod, or as a Job, and nothing downstream would notice.

**Q14 — B.** With neither a node selector nor node affinity specified, the DaemonSet controller creates Pods on all nodes [source: k8s-docs-daemonset-2026-08-24], so twelve. As nodes are added to the cluster, Pods are added to them [source: k8s-docs-daemonset-2026-08-24], so three new nodes gives you fifteen, automatically. **A** confuses a DaemonSet with a single-replica workload. **C** and **D** both assume a `replicas` field you would have to manage; the Pod count is a consequence of node eligibility [source: k8s-docs-daemonset-2026-08-24], and horizontal autoscaling explicitly does not apply to a DaemonSet because it is not a scalable object [source: k8s-docs-hpa-2026-08-24].

**Q15 — B.** A Job defines a task that runs to completion, once [source: k8s-docs-job-2026-08-24]. A CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24]. **A** invents a schedule field on the Job; the schedule lives on the CronJob, which then creates Jobs [source: k8s-docs-cronjob-2026-08-24]. **C** is over-engineering: a CronJob whose schedule fires once is a scheduled thing pretending to be a one-off, and it will surprise whoever inherits it. **D** is wrong in a way worth noticing: a Deployment with `replicas: 1` would treat the process exiting as a failure and restart it forever, which is the precise opposite of what "runs once and exits" means.

**Q16 — B.** `Succeeded` means all containers in the Pod have terminated in success and will not be restarted [source: k8s-docs-pod-lifecycle-2026-08-23]. **A** confuses in-progress with done. **C** invents a phase; there are five, and `Completed` is not among them [source: k8s-docs-pod-lifecycle-2026-08-23] — though `Completed` is a word you will meet in tooling output, which is exactly why the distractor works. **D** is the failure phase: all containers terminated and at least one terminated in failure [source: k8s-docs-pod-lifecycle-2026-08-23].

**Q17 — B.** A selector identifies a *set*. It can answer "is this Pod one of yours"; it cannot answer "which one is this." A StatefulSet's Pods carry identity through their ordinal and derived hostname, `$(statefulset name)-$(ordinal)`, giving `web-0`, `web-1`, `web-2`, and that identity sticks to the Pod across rescheduling [source: k8s-docs-statefulset-2026-08-24]. The identity is a *separate* mechanism layered over selection, which is why the StatefulSet controller also adds a per-Pod name label, `statefulset.kubernetes.io/pod-name`, so you can attach a Service to one specific member [source: k8s-docs-statefulset-2026-08-24]. **A is wrong** because readiness is a property the probe reports on the Pod's status; it is not a guarantee the StatefulSet makes about its members, and it is equally available to a Deployment. **C is wrong** because `.spec.replicas` is the count, and a selector's match count is a *current observation*, not a guarantee — a controller mid-scale has a match count that disagrees with the desired one, which is the whole reason the loop exists. **D is wrong** because namespace scoping comes from the request, not from anything the StatefulSet guarantees, and it is the same for every workload resource.

**Q18 — B.** On their own, custom resources let you store and retrieve structured data; combining a custom resource with a custom controller is what provides a true declarative API [source: k8s-docs-custom-resources-2026-08-23]. **A is wrong, and it is the first thing most people check, which is why it is here:** your object was accepted and `kubectl get certificate` returned it, so access is demonstrably not the problem — a permissions failure would have shown up at the request, not as silence afterwards. **C** is backwards: a CRD is the alternative to API aggregation, and defining a CRD means the Kubernetes API serves and stores your resource without you writing an API server [source: k8s-docs-custom-resources-2026-08-23]. **D** is a real feature attached to a false claim; nothing about a `status` subresource is what makes something act on an object. A controller is.

**Q19 — B.** Controllers are client programs that read and/or write the Kubernetes API, following a control loop: read an object's `.spec`, possibly do things, then update the object's `.status` [source: k8s-docs-extending-kubernetes-2026-08-23]. That description covers both. The difference is deployment, not architecture: an operator's controller normally runs outside the control plane, much as you would run any containerized application, for example as a Deployment [source: k8s-docs-operator-pattern-2026-08-23], while the controllers Kubernetes ships run in the control plane — as the horizontal pod autoscaling controller does [source: k8s-docs-hpa-2026-08-24]. **A** is wrong on both counts: operators are ordinary clients of the Kubernetes API [source: k8s-docs-operator-pattern-2026-08-23], not privileged processes. **C** is wrong; controllers talk *to* the API server, and a built-in controller sends messages to the API server that have useful side effects [source: k8s-docs-controllers-2026-08-23] rather than running inside it. **D** conflates the noun with the verb, which is the exact confusion §8's Fixed Point exists to correct: a CRD registers a *resource*, not a controller. Nothing about installing a CRD makes any program discoverable or runnable, which is why installing one and creating an object of the new kind produces silence.

---

## Chapter Summary

| Concept | Remember this |
|---|---|
| **Workload resource** | You don't manage Pods directly. A workload resource holds the intent and configures a controller to keep it true [source: k8s-docs-workloads-2026-08-23]. |
| **Ownership chain** | Deployment → ReplicaSet → Pod. Template and strategy above, count enforced in the middle, containers at the bottom. |
| **ReplicaSet** | Maintains a stable set of replica Pods [source: k8s-docs-replicaset-2026-08-24]. `.spec.replicas` is the desired state; the loop closes the gap. |
| **Scaling vs self-healing** | Same operation. The loop cannot tell why the gap appeared. |
| **HorizontalPodAutoscaler** | An API resource plus a controller that periodically adjusts the replica count to match observed metrics [source: k8s-docs-hpa-2026-08-24]. |
| **Selector** | Membership is a query, not a list. The template's labels must satisfy the selector or the API rejects the object [source: k8s-docs-replicaset-2026-08-24]. |
| **Owner references** | A separate mechanism from selection. They drive cascading deletion [source: k8s-docs-garbage-collection-2026-08-24]. |
| **Orphans** | Dependents that outlive their owner. Kubernetes deletes dependents by default; mutating a selector is how you make orphans by accident [source: k8s-docs-garbage-collection-2026-08-24] [source: k8s-docs-daemonset-2026-08-24]. |
| **Rolling update** | Template change → new ReplicaSet → Pods moved at a controlled rate [source: k8s-docs-deployment-2026-08-23]. Two ReplicaSets alive at once. |
| **`maxSurge` / `maxUnavailable`** | Both default to 25%. Surge is a ceiling on total, rounding up. Unavailable is a floor on available, rounding down [source: k8s-docs-deployment-spec-fields-2026-08-24]. Neither may be 0 if the other is 0. |
| **`Recreate`** | Kills all old Pods before creating new ones [source: k8s-docs-deployment-2026-08-23]. Downtime chosen deliberately. |
| **What makes it safe** | Readiness. A version that never reports ready never becomes available, so the rollout stalls instead of taking the service down. |
| **Revision** | Created if and only if `.spec.template` changes. Scaling does not create one [source: k8s-docs-deployment-2026-08-23]. |
| **Rollback** | Restore a previous template and run the same rolling update backwards. Ten old ReplicaSets retained by default; `revisionHistoryLimit: 0` removes the ability to undo [source: k8s-docs-deployment-spec-fields-2026-08-24]. |
| **StatefulSet** | Sticky identity per Pod; Pods created from the same spec but not interchangeable [source: k8s-docs-statefulset-2026-08-24]. Interchangeability decides, not disk. |
| **DaemonSet** | One Pod per eligible node, added as nodes join [source: k8s-docs-daemonset-2026-08-24]. The count is a consequence of the cluster, not a setting. |
| **Job / CronJob** | Job runs to completion once [source: k8s-docs-job-2026-08-24]. CronJob creates Jobs on a repeating schedule, approximately, so write them idempotent [source: k8s-docs-cronjob-2026-08-24]. |
| **Custom resource** | An API endpoint that is not necessarily present in a default install, registered dynamically, accessed with `kubectl` like anything else [source: k8s-docs-custom-resources-2026-08-23]. |
| **CustomResourceDefinition** | Defines a custom resource with a name and schema; the API then serves and stores it for you [source: k8s-docs-custom-resources-2026-08-23]. |
| **Operator pattern** | Custom resource + custom controller [source: k8s-docs-custom-resources-2026-08-23]. The controller normally runs outside the control plane, as a Deployment [source: k8s-docs-operator-pattern-2026-08-23]. |
| **The one shape** | Six resources, one control loop. Only the desired state differs. |

---

## The Voyage Ahead

The loop noticed a gap and created a Pod. That Pod does not yet run anywhere.

Between "this Pod object exists" and "this container is executing on a machine" sits a decision nobody in this chapter made. Something has to look at a Pod with no node assigned to it, look at every node in the cluster, and choose. It has to know how much memory the Pod asked for and how much each node has left. It has to respect that some nodes are reserved, some are draining, and some are deliberately hostile to workloads that have not been told they are welcome.

Most of the time this happens in milliseconds and you never think about it. You think about it on the morning a Pod sits in `Pending`, nothing you do to the Deployment changes anything, and the reason is one layer down: the Deployment's job ended the moment the Pod object existed. That Pod is a record of intent with nowhere to go, and the reason it has nowhere to go is written in the resource requests you set in Chapter 5 and the node properties you have not met yet.

Chapter 7 introduces the scheduler: how a Pod gets placed, what it is actually weighing, and the four mechanisms (`nodeSelector`, affinity, taints, and tolerations) you use to influence a decision you do not make yourself. It also settles a question this chapter raised and walked away from: a DaemonSet is supposed to run on every node, so what happens when a node has been marked as one that workloads should stay off?

You know how a fleet is described. Next you find out how a berth is assigned.

> *"You can write the standing order in an afternoon. Finding the water to carry it out is the other half of the work."*
> — Lodestar Ledgers

---

## 🏆 Safe Harbor

Chapter 6 complete. Take the measure of what changed.

You arrived able to read what a Pod was telling you. You leave able to state what should be true about a group of them and hand the maintenance of that statement to something that never sleeps and never forgets. That is not a larger vocabulary. It is a different job.

Specifically, you can now:

✓ Trace intent from a Deployment through a ReplicaSet to a running container, and say which layer owns which piece
✓ Explain why a deleted Pod comes back with nobody having done anything
✓ Predict a rolling update's ceiling and floor from two fields and a replica count, and say when a bound of zero is legal
✓ Name the thing that makes a rollout safe rather than merely gradual, and know it was already in your hands at the end of Chapter 5
✓ State the revision rule exactly, including the part that catches people, and what retaining no revisions costs you
✓ Pick the right workload resource by asking about the work before asking about the software
✓ Define a custom resource, a custom controller, and the pattern that is both, and know why installing one without the other does nothing

And one thing that is not a bullet point: you have seen the control loop twice now, at two altitudes, and recognized it the second time. Hold onto that recognition. You are going to need it once more, and the third time is the one that matters.

🗺️ Chart → 🌊 Passage → 🌅 **Dawn** — Part II's trunk is behind you.

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

The input to this stage is damaged, not just rough: it begins mid-sentence (the chapter head — frontmatter, Soundings, §1–§8 body prose — is absent), and the tail appears **three times**, with the second and third copies coming from a *later* 21-question revision that was spliced in by a harvester artifact (`(If the block above contains [file not available]...`). I've voice-revised the recoverable content, de-duplicated it, and kept the 19-question set (the only internally complete one), while adopting the later revision's sharper factual wordings where they map cleanly — flagged in-file.

<!-- VOICE-FLAG: input-truncated — the draft handed to stage 4 begins mid-sentence. Chapter head (YAML frontmatter, Attention Budget, epigraph, Why This Chapter Matters, What You'll Learn, §1–§8 body prose, Taking Your Bearings checkpoints, Exam Alert heading) was NOT present in the input and has not been reconstructed. Re-harvest draft-v1.md before stage 5. -->
<!-- VOICE-FLAG: input-duplicated — input carried three copies of the Chapter Summary / Voyage Ahead / Safe Harbor tail plus a spliced fragment of a 21-question revision. De-duplicated here to the 19-question set, which matches the Practice Questions header and the retrieval/interleave tallies. Refinements adopted from the later fragment: DaemonSet count-as-consequence framing (A15), Pod-phase vs Job-`Complete` distinction (A16), and the fuller Chapter Summary table. -->

1. <!-- VOICE-FLAG: truncated-fragment -->…ognition exam can ask about in a single sentence. If you memorize one figure, memorize the decision tree.
2. **Deployment versus StatefulSet is about interchangeability**, not about whether the app writes to disk.
3. **DaemonSet is one Pod per matching node**, added automatically as nodes join. There is no replica count. The count is a consequence of node eligibility, not a field you set.
4. **Job runs to completion once; CronJob creates the same Job on a schedule.**
5. **The ownership chain** Deployment → ReplicaSet → Pod, and which layer holds the count and which holds the template.
6. **`RollingUpdate` is the default strategy;** `maxSurge` and `maxUnavailable` both default to **25%**; `Recreate` kills all old Pods before creating any new ones.
7. **A revision is created if and only if the Pod template changes.** Scaling does not create one.
8. **A CRD alone stores structured data; CRD plus custom controller is the operator pattern.**

---

**Common Traps** — these are documented confusions, not invented ones:

- **"Deployment versus StatefulSet is about whether the app writes to disk."** It isn't. It's about whether the Pods are interchangeable. Defused in §6.
- **"I need several copies, so I'll use a DaemonSet."** A DaemonSet has no count. Defused in §7.
- **"Job and CronJob do the same thing."** A CronJob's output is Jobs. Defused in §7.
- **"Scaling creates a revision."** Only a `.spec.template` change does [source: k8s-docs-deployment-2026-08-23]. This is mechanically checkable, and therefore exactly the shape a multiple-choice item is built from.
- **`maxSurge` and `maxUnavailable` transposed.** The names are symmetrical and the defaults are identical, which is precisely what makes them confusable. Surge is above the line; unavailable is below it. They round in opposite directions too: surge up, unavailable down [source: k8s-docs-deployment-spec-fields-2026-08-24].
- **"`Recreate` is a mistake."** It's a supported strategy with a stated cost. Treating it as an error is its own trap.
- **"Installing a CRD makes something happen."** It doesn't. That's the design, and it's one instance of a rule you'll meet four times.

The first three share a single root cause: **choosing a resource by what the application *is*, rather than by how its Pods need to be *managed*.** Ask the questions in the right order and three memorizations collapse into one rule.

---

## Practice Questions

*Nineteen questions. Four reach back to Chapters 3, 4, and 5. Five require two sections at once.*

---

**1.** A Deployment named `api` has `replicas: 4`. Which object holds the number 4?

A) The Deployment
B) The ReplicaSet the Deployment manages
C) Each Pod, in its own spec
D) The Pod template

**2.** *[retrieval: ch4]* You run `kubectl get deployment api -o yaml` and see both a `spec` block and a `status` block. Where does the replica count you *asked for* live, and where does the number *actually running* live?

A) Both in `spec`; `status` only reports errors
B) The requested count in `spec`, the running count in `status`
C) The requested count in `status`, the running count in `spec`
D) Both in `status`; `spec` is write-only

**3.** A ReplicaSet has `replicas: 3` and three matching Pods. You add a label to a bare, unowned Pod so that it now matches the ReplicaSet's selector. What happens?

A) Nothing — the ReplicaSet only manages Pods it created
B) The ReplicaSet adopts it and then terminates one Pod, because it is now over count
C) The ReplicaSet's replica count silently increases to 4
D) The API rejects the label change

**4.** *[retrieval: ch5]* A node fails. A Deployment's Pod on that node is replaced. Which statement about the replacement is correct?

A) It is the same Pod, moved to a new node, with the same UID
B) It is a new Pod with a different UID, created from the same template
C) It is the same Pod object with a new UID assigned
D) It retains the original Pod's name so that clients can reconnect

**5.** Two Deployments in the same namespace were written by different teams, and both selectors match the label `tier: web`. What is the most likely observed symptom?

A) The second Deployment fails to create with a duplicate-selector error
B) Both Deployments show replica counts that fluctuate, with no error reported
C) Kubernetes merges them into a single Deployment
D) The older Deployment takes exclusive ownership and the newer one idles

**6.** Which of these is the correct reason a Deployment's `.spec.template.metadata.labels` must match its `.spec.selector`?

A) So that `kubectl get pods --show-labels` renders consistently
B) So that the scheduler can find a node for the Pods
C) Because the controller finds its Pods by querying for the selector, so Pods it creates must satisfy that query
D) Because the API server uses labels to assign owner references

**7.** A Deployment has `replicas: 8` and default strategy settings. During a rolling update, what is the maximum total number of Pods and the minimum available?

A) 10 max, 6 min
B) 10 max, 6 min — with both values rounded up
C) 8 max, 6 min
D) 10 max, 8 min

**8.** A Deployment sets `maxSurge: 0`. What must be true of `maxUnavailable`?

A) It must also be 0
B) It must be greater than 0
C) It is ignored when `maxSurge` is 0
D) It must be expressed as a percentage

**9.** Which change to a Deployment creates a new revision?

A) Increasing `replicas` from 2 to 5
B) Changing `maxSurge` from 25% to 50%
C) Changing the container image in `.spec.template`
D) Changing `revisionHistoryLimit` from 10 to 3

**10.** You scaled a Deployment from 3 to 9 replicas, then later changed the image and immediately ran `kubectl rollout undo`. After the rollback completes, how many replicas are running?

A) 3 — the rollback restores the state from before the scale
B) 9 — the replica count is not part of the Pod template
C) 6 — the rollback averages the two counts
D) Indeterminate, until you run `kubectl scale`

**11.** *[interleaved: §1 + §4]* Midway through a rolling update, `kubectl get rs` shows two ReplicaSets, one with 6 Pods and one with 5. Which is which, and why do two exist?

A) The Deployment created a temporary copy; only one is real
B) The old ReplicaSet is scaling down and the new one is scaling up; both exist because the Deployment layer manages both
C) One belongs to the Deployment and the other belongs to a Service
D) The second was created by the scheduler to hold unschedulable Pods

**12.** *[interleaved: Ch 5 §7 + §4]* From the *probe's* side: why does a readiness probe failing on every new Pod stop a rolling update rather than merely slow it?

A) A failed readiness probe causes the kubelet to kill the container, so no new Pods ever exist
B) A Pod that is not ready does not count as available, so the Deployment cannot scale the old ReplicaSet down further without breaching `maxUnavailable`
C) The Deployment controller stops on the first probe failure and requires manual intervention
D) The scheduler refuses to place additional Pods until the existing ones report ready

**13.** An application acquires an exclusive database lock at startup and cannot tolerate a second instance. Which strategy, and what is the consequence?

A) `RollingUpdate` with `maxSurge: 0` — no downtime, no overlap
B) `Recreate` — a period of zero availability, accepted deliberately
C) `RollingUpdate` with `maxUnavailable: 0` — no downtime, no overlap
D) A StatefulSet, because locks imply state

**14.** *[interleaved: §3 + §6]* A StatefulSet's Pods are also selected by labels. What does the selector *not* tell you about them?

A) Which Pods belong to the StatefulSet
B) That the Pods are not interchangeable with one another
C) How many Pods the StatefulSet maintains
D) Which namespace the Pods are in

**15.** A cluster has 5 nodes. You create a DaemonSet with no `nodeSelector`. Two nodes are then added. How many DaemonSet Pods exist?

A) 5 — the count was fixed at creation
B) 7 — a Pod is scheduled onto each new matching node as it joins
C) 1 — a DaemonSet runs one Pod cluster-wide
D) Whatever `replicas` is set to

**16.** *[retrieval: ch5]* A Job's Pod finishes its work and exits with status 0. Which Pod phase does it reach, and why does that phase matter here specifically?

A) `Running` — Jobs keep their Pods running for inspection
B) `Succeeded` — all containers terminated in success and will not be restarted, which is precisely what "completion" means for a Job
C) `Failed` — exiting is always a failure for a supervised Pod
D) `Unknown` — the Job controller stops reporting once work is done

**17.** A CronJob with schedule `0 4 * * *` has been running for a week. What objects has it created?

A) Seven Pods, directly
B) Seven Jobs, each of which created one or more Pods
C) One Job, restarted seven times
D) Seven CronJob revisions

**18.** *[retrieval: ch3, interleaved with §8]* What does a custom controller have in common with the built-in controllers running inside kube-controller-manager?

A) Nothing — custom controllers use a separate extension API
B) Both are compiled into the control plane binary
C) Both watch a resource whose `spec` is desired state and act to bring current state closer to it
D) Both require cluster-admin privileges by design

**19.** *[interleaved: §8 + §1]* An operator that manages message queues has been installed. Which statement about the operator's own controller process is correct?

A) It runs as a control-plane component alongside kube-scheduler
B) It runs as an ordinary containerized workload in the cluster, normally a Deployment
C) It runs on the client machine, alongside `kubectl`
D) It is embedded inside the CustomResourceDefinition object

---

### Answers & Explanations

**1 — B.** The ReplicaSet holds the count [source: k8s-docs-replicaset-2026-08-24]; the Deployment holds the template and the update strategy [source: k8s-docs-deployment-2026-08-23]. **A** is the near-miss: you *set* `replicas` on the Deployment, and the Deployment propagates it to the ReplicaSet it manages. But the object whose job is maintaining that many Pods is the ReplicaSet, and during a rollout there are two of them holding different numbers. **C** is wrong because a Pod has no concept of how many peers it has. **D** confuses the template (what a Pod looks like) with the count (how many).

**2 — B.** You set `spec` when you create the object; it describes the state you want. `status` describes the state that is, and Kubernetes supplies and updates it [source: k8s-docs-objects-2026-08-23]. The docs use this exact example: you set the Deployment spec to three replicas, the system starts three instances and updates status to match [source: k8s-docs-objects-2026-08-23]. **C** inverts the two. **A** and **D** read `status` as a log rather than as a description of current state.

**3 — B.** A ReplicaSet acquires any Pod that matches its selector and carries no controller owner reference, and it does so immediately [source: k8s-docs-replicaset-2026-08-24]. The count was already satisfied, so the adopted Pod puts it over, and one Pod is terminated. **A** is the intuition this question exists to break: membership is a query, not a record of what the controller created. **C** would mean the controller changed its own desired state, which is not something controllers do. **D** is wrong: labels are freely mutable, and the API does not police cross-object overlap.

**4 — B.** A Pod is never rescheduled to a different node; it is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23], and controllers create the replacement from the Pod template [source: k8s-docs-pods-2026-08-24]. **A** describes migration, which Kubernetes does not do at the Pod level. **C** is incoherent: a UID identifies an object over its whole lifetime, so a new UID *is* a new object. **D** is wrong, and it matters: the name changes too, which is exactly why something else has to supply a stable address.

**5 — B.** Each controller watches a Pod population that keeps changing for reasons it didn't cause, and each acts on what it sees. The docs warn about overlapping selectors precisely because of adoption behavior [source: k8s-docs-replicaset-2026-08-24]. **A** is the answer people hope for; there is no such validation. **C** is not a thing Kubernetes does. **D** implies an ownership arbitration mechanism that doesn't exist. Both controllers keep acting, which is what makes this expensive.

**6 — C.** The controller's Pods are whichever Pods match its selector [source: k8s-docs-replicaset-2026-08-24], so Pods it creates must satisfy that query or it can never see them. The API enforces the match [source: k8s-docs-deployment-spec-fields-2026-08-24], but the enforcement exists *because* of C, not the other way around. **D** inverts the relationship: owner references are set by the controller and are documented as a mechanism distinct from labels and selectors [source: k8s-docs-garbage-collection-2026-08-24]. **A** and **B** are unrelated to selector semantics.

**7 — A.** `maxSurge` = 25% of 8 = 2, so max total 10. `maxUnavailable` = 25% of 8 = 2, so min available 6 [source: k8s-docs-deployment-spec-fields-2026-08-24]. (With 8 replicas both values come out whole, so rounding never bites. That is why **B** fails as a *rule* even though its numbers happen to land: surge rounds up, unavailable rounds down.) **C** forgets surge headroom entirely. **D** transposes the bounds.

**8 — B.** `maxSurge` cannot be 0 if `maxUnavailable` is 0, and vice versa [source: k8s-docs-deployment-spec-fields-2026-08-24]. With no headroom above the desired count and no slack below it, there is no legal state transition: nothing can start, because nothing may stop. **A** would deadlock the rollout, which is why it's prohibited. **C** and **D** invent behavior.

**9 — C.** A new revision is created if and only if `.spec.template` changes [source: k8s-docs-deployment-2026-08-23]. The image lives in the template. **A** is the most tempting distractor, and the docs name scaling explicitly as an update that does *not* create a revision. **B** changes `.spec.strategy`, a sibling of `.spec.template` rather than part of it. **D** changes retention policy, not the template.

**10 — B.** `rollout undo` restores a previous Pod template. The replica count is not in the Pod template; that's the same fact as question 9, seen from the other side. You rolled back the image; you did not roll back the scale. **A** is what most people expect, which is why the trap is worth a question. **C** is invented. **D** implies the count becomes undefined, which it does not.

**11 — B.** Updating the PodTemplateSpec creates a new ReplicaSet, and the Deployment manages moving Pods from the old to the new at a controlled rate [source: k8s-docs-deployment-2026-08-23]. Two ReplicaSets is the normal mid-rollout state, and it's only expressible because the Deployment layer sits above the ReplicaSet layer: §1's chain doing its actual job. **A** misreads a normal state as a transient artifact. **C** confuses ownership with selection; a Service selects Pods and owns nothing. **D** invents a scheduler behavior.

**12 — B.** A newly created Pod counts as available only once it is ready, and stays ready for `minReadySeconds` [source: k8s-docs-deployment-spec-fields-2026-08-24]; readiness failure also removes the Pod's address from matching Service endpoints [source: k8s-docs-pod-lifecycle-2026-08-23]. With no new Pods becoming available, scaling the old ReplicaSet down any further would breach `maxUnavailable`, so the Deployment stops, old version still serving. **A** describes a *liveness* probe, which kills and restarts the container; readiness does not [source: k8s-docs-pod-lifecycle-2026-08-23]. **C** implies a fail-fast abort; the controller keeps retrying. **D** attributes the behavior to the scheduler rather than the Deployment controller.

**13 — B.** `Recreate` kills all existing Pods before creating new ones [source: k8s-docs-deployment-2026-08-23], guaranteeing the two versions never coexist, at the cost of a window with nothing available. **A** and **C** are the interesting wrong answers: setting one bound to 0 does not prevent overlap, it only constrains *how much* overlap, and per question 8, one of them being 0 forces the other to be non-zero. **D** confuses "holds a lock" with "Pods have identity"; a single-replica Deployment with `Recreate` is a perfectly ordinary answer.

**14 — B.** The selector tells you membership and nothing else. Two Pods matching the same selector may be freely substitutable (Deployment), or may each hold a distinct identity and its own storage (StatefulSet). The docs are explicit that StatefulSet Pods are created from the same spec but are not interchangeable [source: k8s-docs-statefulset-2026-08-24]. That distinction lives in the resource kind, not in the labels. **A** is exactly what the selector *does* tell you. **C** is `.spec.replicas`. **D** is `metadata.namespace`.

**15 — B.** Every time you add a node matching the DaemonSet's specification, the control plane schedules a Pod for that DaemonSet onto the new node [source: k8s-docs-workloads-2026-08-23]; with no `nodeSelector`, the controller creates Pods on all nodes [source: k8s-docs-daemonset-2026-08-24]. **A** treats the count as fixed, which is the opposite of the resource's purpose. **C** describes something closer to a single-replica Deployment. **D** is the trap: the count is a consequence of node eligibility rather than a field you choose, which is also why HPA does not apply to DaemonSets [source: k8s-docs-hpa-2026-08-24].

**16 — B.** `Succeeded` means all containers terminated in success and will not be restarted [source: k8s-docs-pod-lifecycle-2026-08-23], and a Job continues retrying until a specified number of Pods successfully terminate [source: k8s-docs-job-2026-08-24]. This is where that phase finally earns its place: for a long-running service, `Succeeded` would be a malfunction; for a Job, it's the goal. Note the level the question asks about. `Succeeded` is a *Pod* phase; the Job object itself finishes as `Complete` [source: k8s-docs-job-2026-08-24]. **C** is the mirror-image error: it's `Failed` that means at least one container terminated in failure. **A** contradicts run-to-completion. **D** confuses reporting with phase.

**17 — B.** A CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24], and each Job creates the Pods that do the work [source: k8s-docs-job-2026-08-24]. Seven firings, seven Jobs, at least seven Pods. **A** skips the Job layer, which is the misconception the Job-versus-CronJob distinction exists to prevent. **C** contradicts run-to-completion. **D** imports revision vocabulary from Deployments, where it doesn't belong. (Note the docs' caveat that scheduling is approximate and two Jobs might occasionally be created, or none [source: k8s-docs-cronjob-2026-08-24], which is why Jobs should be idempotent.)

**18 — C.** A controller tracks at least one Kubernetes resource type whose objects have a `spec` field representing desired state, and the controller is responsible for making current state come closer to it [source: k8s-docs-controllers-2026-08-23]. A custom controller does exactly this, on a custom resource, providing a true declarative API when paired with one [source: k8s-docs-custom-resources-2026-08-23]. Same shape, different resource type, different author. **B** is false: a custom controller normally runs outside the control plane [source: k8s-docs-operator-pattern-2026-08-23]. **A** denies the whole point of §8. **D** confuses privilege with mechanism.

**19 — B.** The operator's controller normally runs outside the control plane, much as you would run any containerized application, for example as a Deployment [source: k8s-docs-operator-pattern-2026-08-23]. **A** is the intuitive-but-wrong answer: extending Kubernetes doesn't require *being* Kubernetes. **C** describes a client-side tool, but operators are long-running API clients that must keep watching. **D** misunderstands a CRD as executable rather than as a schema.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **Workload resource** | You don't manage Pods; you declare intent and a controller manages Pods for you |
| **Ownership chain** | Deployment → ReplicaSet → Pod. Deployment holds template + strategy; ReplicaSet maintains the count |
| **ReplicaSet** | Maintains a stable set of replica Pods. The control loop, with `.spec.replicas` as desired state |
| **Scaling vs self-healing** | The same operation. The loop can't tell "you asked for more" from "one died" |
| **Selector** | Membership is a query, not a list. Template labels must satisfy the selector |
| **Owner reference** | What makes cascading deletion work, and what adoption sets on Pods a controller acquires |
| **Overlapping selectors** | Two controllers fighting over one Pod population. Documented as a hazard to design around, not as a configuration the API rejects |
| **`RollingUpdate`** | The default. New ReplicaSet up, old one down, at a controlled rate |
| **`maxSurge` / `maxUnavailable`** | Both default to 25%. Surge is above the line (rounds up); unavailable is below (rounds down) |
| **`Recreate`** | All old Pods killed first. Downtime, deliberately chosen, for apps that can't run two versions |
| **What makes a rollout safe** | Readiness. A Pod that never reports ready never counts as available, so it never displaces the old one |
| **Revision** | Created if and only if `.spec.template` changes. Scaling does not create one |
| **Rollback** | Sets the Pod template to a previous value and runs the same rolling update backwards |
| **StatefulSet** | For Pods that are *not interchangeable*. Stable ordinal identity, stable network name, own storage |
| **Stable identity** | `db-1`'s replacement is also `db-1`, and it reattaches to the same claim. The storage belongs to the identity |
| **The disk trap** | "Writes to disk" does not mean StatefulSet. Interchangeability decides |
| **DaemonSet** | One Pod per matching node, automatically as nodes join. The count is a consequence of node eligibility, not a setting |
| **Job** | Runs to completion, once. Its Pods reach phase `Succeeded` or `Failed`; the Job itself finishes as `Complete` or `Failed` |
| **CronJob** | Creates the same Job repeatedly on a cron schedule. Its output is Jobs |
| **Custom resource** | A new API endpoint. On its own, it only stores structured data |
| **Operator pattern** | Custom resource + custom controller. The controller normally runs as a Deployment |
| **The recurring rule** | The object exists, but nothing happens without the component |

---

## The Voyage Ahead

You can now write down what should be true and hand the responsibility to a loop. There is one thing that loop cannot do for you.

It creates a Pod. It does not decide *where the Pod goes*. Every replacement in this chapter, every surge Pod during a rolling update, every DaemonSet Pod on a newly joined node — each one arrives in the world unplaced, and something else has to find it a machine with room. Usually that works so smoothly you never think about it. Sometimes it doesn't, and a Pod sits in `Pending` while the count it was supposed to satisfy stays unsatisfied, and the loop that created it goes on cheerfully wanting one more.

Chapter 7 is about the component that makes that decision, the two-step process it uses, and the vocabulary you have for influencing it: how a Pod expresses what it needs from a machine, and how a machine expresses what it will accept. You've already met the mechanism in disguise. The DaemonSet's tolerations in §7 were a node saying "not for general traffic" and a controller saying "this one's an exception."

> *"You may declare what should exist. Where it exists is a separate question, and the sea does not always have room where you wanted it."*

---

🏆 **Safe Harbor**

Chapter 6 complete. You came in able to read a Pod and left able to author a fleet: six workload resources, one control loop, and the beginning of the recognition that the loop is the whole system rather than a feature of it.

**Voyage Progress:** 🗺️ → 🌊 → 🌅
*Part II, Chapter 6 of 18. The trunk of the book is behind you.*

---

Two things worth acting on before stage 5 runs:

1. **Re-harvest the input.** Roughly the first 70% of the chapter never reached this stage. The harvester's `<details>`-extraction fix (commit `821f1ef`) appears to be grabbing overlapping snapshot regions and concatenating them — the triplicated tail plus the spliced `(If the block above contains [file not available]…` marker is a harvester artifact, not draft content.
2. **Resolve 19 vs 21 questions.** The spliced fragment implies a later revision with 21 items. I kept 19 because that set is complete and its header tallies match; if the 21-question version is the real draft-v1, this whole pass needs rerunning against it.

empotent.
> [source: k8s-docs-cronjob-2026-08-24]

Write the nightly report generator so that running it twice produces one report, not two.

⚑ **Flagged with emphasis in the chapter, source-backed, and never tested.** One of three
untested taught concepts (with the HPA and overlapping selectors). Closing it would require
raising the chapter's question budget above the outline's 42; the book is under its
300-question floor, so a raise to 45 is affordable if the author wants it.

⚑ **`concurrencyPolicy` is deliberately out of scope** and returns zero hits. Do not add it.

## Related

[[job]] · [[workload-resource]] · [[control-loop]] · [[pod-template]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/custom-resource.md ===
# Concept: Custom resources and the CRD

**Home:** Chapter 6 §8 · **Competency:** D1.1 · **Status:** canonical
**⚑ Contains the book's first retrieval of TWO stalled cross-cutting themes.**

## Start with "resource"

> A resource is **an endpoint in the Kubernetes API that stores a collection of API objects
> of a certain kind**; the built-in `pods` resource contains a collection of Pod objects.
> [source: k8s-docs-custom-resources-2026-08-23]

Defined here for the first time in the book, six chapters after the reader started typing
`kubectl get <resource>`. It has to be defined before *custom* resource can mean anything.

## Definition (verbatim)

> A **custom resource** is an extension of the Kubernetes API that is not necessarily
> available in a default Kubernetes installation; it represents a customization of a
> particular installation. Custom resources can appear and disappear in a running cluster
> through **dynamic registration**, and cluster admins can update them independently of the
> cluster itself. [source: k8s-docs-custom-resources-2026-08-23]

The clause that makes it click: once installed, "users create and access its objects using
`kubectl`, **just as they do for built-in resources like Pods**." Nothing about the tooling
changes — `get`, `describe`, `apply`, labels, selectors, namespaces, RBAC — "because the new
kind lives in the same API."

## The CustomResourceDefinition

> Defining a CRD object **creates a new custom resource with a name and schema that you
> specify, and the Kubernetes API then serves and handles the storage of it for you.** This
> frees you from writing your own API server, though the generic nature of the
> implementation means you have less flexibility than with API-server aggregation.
> [source: k8s-docs-custom-resources-2026-08-23]

"Many core Kubernetes functions are now built using custom resources, which is part of what
makes Kubernetes modular." **Not an exotic corner — one of the main ways the platform grows.**

## ★ Fixed Point (verbatim — do not reword)

> **A custom resource on its own stores and retrieves structured data. A custom resource
> combined with a custom controller is the operator pattern.**

The limitation is the surprising half and it is verbatim: "**On their own, custom resources
let you store and retrieve structured data.**" That is all. A CRD by itself is a shape in a
database. **You have defined a noun and taught the API server to store it.**

## ⚑ CANON CONFLICT — the absent-component pattern has two canonical strings

§8's 🪝 Snag is **the first retrieval of `absent-component-pattern.md` in the book**, four
chapters after Chapter 3 named it:

> "We installed the CRD, created an object of the new kind, and nothing happened." That is
> the correct behavior. There is no controller. **You gave the cluster a new noun and no
> verb.**
>
> **Name this shape, because you are going to meet it again.** *The object exists but
> nothing happens without the component.*

**That string is B3's** (`retrieval-architecture.md:15`), not the shard's. The shard carries
a capitalised **"USE THIS NAME. DO NOT RE-COIN IT."** for *"absent-component pattern"* /
*"an object without its component does nothing."* Two authorities, two "retrieve it by name"
instructions, two strings — and Chapter 6 has now shipped B3's, twice, in reader-facing prose
and in a graded answer key.

**Do not resolve by overwriting either.** B3's phrase reads naturally in prose; the shard's is
the only one of the two that works as a noun in a Chapter 17 synthesis. **Author's call, and
now urgent** — Chapters 10, 13 and 17 each owe a by-name retrieval.

**The instance roster is also now five members across three different four-item lists.**
Chapter 6 supplies a **new** instance (CRD with no controller — the only one where the reader
*creates* the orphaned object themselves) and drops NetworkPolicy-on-a-non-enforcing-CNI.
Chapter 6's four: CRD, Ingress without a controller, `kubectl top` without metrics-server, a
vertical autoscaler not shipped by default.

## ⚑ The fourth socket — first named recurrence of Chapter 2's theme

> Chapter 2 showed you the move: Kubernetes defines an interface and lets the ecosystem
> implement it. You met it with the container runtime, with networking, and with storage, and
> you were told you would meet it once more at the API layer. **This is that.**

Published extension points: "**API extensions, Custom Resource Definitions (CRDs) and the API
aggregation layer**," one of six categories alongside controllers, scheduling extensions, API
access extensions, kubectl plugins, and infrastructure extensions
[source: k8s-docs-extending-kubernetes-2026-08-23].

**The Chapter 5 and Chapter 7 ledgers both recorded this theme as "still zero named
recurrences."** §8 lands it, as a payoff rather than a reminder, and it is the only retrieval
in the book of a theme originating in Chapter 2 — the chapter with no ledger.

⚑ **Collision, and it is the highest-stakes one in the chapter.** Ch 6 pins the synthesis at
`Ch 17 §6`; Chapter 2 published `Ch 17 §4` for the same convergence.

## 🔭 Closer Look — the other route

API-server aggregation "offers more flexibility at the cost of writing and operating more of
the API machinery yourself" [source: k8s-docs-custom-resources-2026-08-23]. Scoped correctly:
"CRD is the common path, aggregation is the rarer one, and knowing that both exist is enough."

⚑ **B2 assigns aggregation no owner chapter.** It may never need one — record the decision.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 10** | Ingress without an ingress controller — the same shape, **by name** |
| **Ch 13** | `kubectl top` without metrics-server — ⚑ Ch 6 pins `§2`; Ch 2/Ch 5 pin `§2` for `ImagePullBackOff` |
| **Ch 14** | ⚑ **NEW:** why Helm charts have a `crds/` directory (`Ch 14 §6`) |
| **Ch 15** | A delivery tool that is structurally a controller acting on custom resources (`Ch 15 §3`) |
| **Ch 17** | The four-socket synthesis. **Section number contested** |

⚑ **OLM and Kubebuilder are deliberately out of scope** and return zero hits. Do not add them.

## Related

[[operator-pattern]] · [[control-loop]] · [[absent-component-pattern]] ·
[[kubernetes-object]] · [[spec]] · [[status]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/operator-pattern.md ===
# Concept: The operator pattern

**Home:** Chapter 6 §8 · **Competency:** D1.1 · **Status:** canonical
**⚑ Direct precursor to Chapter 15's central recognition.**

## Definition (verbatim)

> The **operator pattern combines custom resources and custom controllers.**
> [source: k8s-docs-custom-resources-2026-08-23]

## What it is for is more interesting than what it is

> The pattern aims to capture the key aim of **a human operator who is managing a service**,
> someone with deep knowledge of how the system ought to behave, how to deploy it, and how to
> react if there are problems, and to write that knowledge as code that automates a task
> beyond what Kubernetes itself provides. [source: k8s-docs-operator-pattern-2026-08-23]

The mechanism is unglamorous and precise: operators "are clients of the Kubernetes API that
act as controllers for a custom resource," and the pattern "lets you extend the cluster's
behavior without modifying the code of Kubernetes itself."

## The published list, which is the fastest way to make it concrete

Deploying an application on demand · taking and restoring backups of that application's state
· handling upgrades of the application code alongside related changes such as database schemas
or extra configuration settings · publishing a Service so applications that don't support
Kubernetes APIs can discover them · simulating failure in all or part of a cluster to test its
resilience · choosing a leader for a distributed application that has no internal election
process. [source: k8s-docs-operator-pattern-2026-08-23]

> Every one of those is somebody's 2 a.m. runbook, turned into a loop that never sleeps.

## The controller contract — nothing about it is privileged

> Controllers are **client programs that read and/or write to the Kubernetes API, following
> a control loop, reading an object's `.spec`, possibly doing things, and then updating the
> object's `.status`.** [source: k8s-docs-extending-kubernetes-2026-08-23]

**Read `.spec`, act, write `.status`.** That description covers built-in controllers and
third-party ones equally. Practice Q19 grades it on two axes at once — what they share
(the contract) and where each runs (the difference).

## ⚑ The closing turn, and the misconception that matters most

> The most common way to deploy an operator is to add the CustomResourceDefinition and its
> associated controller to your cluster, and **the controller will normally run outside of
> the control plane, much as you would run any containerized application: for example, as a
> Deployment.** [source: k8s-docs-operator-pattern-2026-08-23]

**The thing that extends Kubernetes is itself deployed *by* Kubernetes, using the first
resource in this chapter.** "The operator that manages your database is three replicas of a
container image, held at a count by a ReplicaSet, held at a template by a Deployment. It is
not a plugin. It is not privileged."

**The misconception this shard exists to kill:** that an operator runs *in* the control plane,
or as a static Pod on control-plane nodes, or is installed into the API server. Bearings #3 Q5
exists to catch it and says why it matters: "Carrying the wrong version of this makes Chapter
15's central move — a delivery tool that is structurally just another controller — read as a
special case instead of as the ordinary case."

**This is why §8 sits after §1 rather than before it.** The section order is an argument.

## Downstream obligations — binding

| Chapter | Obligation |
|---|---|
| **Ch 15** | ⚑ **The book's primary Zenith depends on this shard.** §9 publishes the promise outright: "a controller whose desired state lives in a Git repository, and why that is the same technology rather than a new one," and the Safe Harbor tells the reader "the third time is the one that matters." **Chapter 6 has promised the reader, in print, that Chapter 15 delivers a recognition rather than a fifth list** |
| **Ch 15 §3** | A delivery tool that is, structurally, a controller acting on custom resources |
| **Ch 17** | Where the operator sits among the extension points |

## Related

[[custom-resource]] · [[control-loop]] · [[deployment]] · [[replicaset]] · [[status]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 6 update (2026-08-24)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.1** | **Chapter 6** *(controller layer — closes the competency)* | **deep** | **2026-08-24** |

**⚑ REGISTRY ROW CHANGE — the first competency in the book to open and close.**
`D1.1 | Kubernetes Core Concepts | Ch 3, 4, 5, 6 | not yet covered` → **"complete — closed
at Ch 6, 2026-08-24."** B2 assigns D1.1 four consecutive chapters and Chapter 6 is the last.
There is no later chapter to absorb a gap.

### Chapter 6 — D1.1 coverage detail

`kb_tags.objectives: ["D1.1"]`, applied uniformly to all nine sections.

Curriculum-alignment audited **36 sub-objectives: 35 covered, 1 absent, 0 partial**, and the
one absent (**D1.1-16, orphaning**) was remediated in revision. **The shipped chapter is
36 / 36.**

| Sub-topic | Depth |
|---|---|
| Workload resource — the resource configures a controller | **deep — closes Ch 5's reservation** |
| Deployment — declarative updates for Pods *and ReplicaSets* | deep |
| ReplicaSet — maintains a stable set of replica Pods | deep |
| Ownership chain Deployment → ReplicaSet → Pod | **deep — the structural key; six later chapters depend on it** |
| Pod template; same schema, nested, no `apiVersion`/`kind` | appropriate — ⚑ sourced only for DaemonSet |
| ReplicationController — legacy, superseded | recognition — correctly scoped |
| **The control loop instantiated** | **deep — discharges `control-loop.md`'s Ch 6 obligation, the theme's first PLANNED retrieval** |
| `.spec.replicas` on both objects; where the count is enforced | deep |
| `kubectl scale`; manual horizontal scaling | appropriate |
| HorizontalPodAutoscaler — concept only | appropriate — ⚑ taught, never tested |
| Label selector as the ReplicaSet→Pod join | **deep — discharges `label-selector.md`'s Ch 6 obligation, first of four** |
| Selector–template agreement; the API **rejects** a mismatch | deep |
| Owner references — distinct from selection | **deep — "ownership is exclusive; selection is not"** |
| Cascading deletion (background is the default) | appropriate |
| Controller adoption of bare Pods | appropriate |
| **Orphaning** | ✅ **covered — remediated after the audit** |
| Overlapping selectors | appropriate — ⚑ a full sidebar with no retrieval path |
| Deployment strategy; `RollingUpdate` default; `Recreate` | deep |
| `maxSurge` / `maxUnavailable`, 25% defaults, asymmetric rounding | **deep — ⚑ the outline's ceiling of 12 is wrong; it is 13** |
| `minReadySeconds` / readiness-gated availability | **deep — pays Ch 5's probes forward as release safety** |
| Stuck rollout; `progressDeadlineSeconds` as a signal | appropriate |
| Revision rule — created **iff** `.spec.template` changes | deep |
| `kubectl rollout` verb surface (all six) | appropriate — ⚑ `status` untested |
| Rollback semantics | **deep — and pre-emptively disambiguated against Helm and Ch 15** |
| `revisionHistoryLimit`, default 10; `0` removes undo | appropriate |
| StatefulSet — same spec, **not interchangeable** | deep |
| Stable Pod identity — ordinal, hostname, sticky | appropriate |
| Per-Pod PVC bound for the Pod's lifecycle | recognition — **correctly deferred to Ch 11** |
| StatefulSet ordering guarantees | appropriate |
| DaemonSet — one per eligible node, added as nodes join | deep |
| Node-local facility framing | appropriate |
| Job — runs to completion once; `restartPolicy` restriction | appropriate |
| CronJob — creates Jobs on a schedule; `.spec.schedule` | appropriate — ⚑ idempotency untested |
| Custom resource; CRD; dynamic registration | deep |
| Custom controller; declarative vs imperative API | deep |
| **Operator pattern; where the controller runs** | **deep — the precursor to Ch 15's Zenith** |

**Scope discipline is the strongest in Part II.** All eleven out-of-scope boundaries the
outline set are held — `concurrencyPolicy`, `parallelism`, `backoffLimit`, Indexed Jobs,
job-history limits, TTL, proportional scaling, `--cascade=orphan`, finalizers,
OLM/Kubebuilder, and Knative/Argo-by-name all return **zero** hits. Blue/green, canary and
A/B appear exactly once, inside the single authorized forward bearing.

---

## ✅ The domain-allocation alarm is resolved, and Chapter 8's number is now known

Chapter 5's ledger raised this as blocking and projected **16 points** for Chapter 6.
Chapter 7's ledger revised it to eleven. Chapter 6 claimed **~6%**, and the domain now closes:

| Chapter | Claimed | Objective |
|---|---|---|
| Ch 2 — Containerization | ~9% | D1.4 |
| Ch 3 — Cluster architecture | ~6% | D1.1 |
| Ch 4 — Objects | ~6% | D1.1 |
| Ch 5 — Pods | 7% | D1.1 |
| **Ch 6 — Controllers** | **~6%** | **D1.1 (closes)** |
| Ch 7 — Scheduling | 5% | D1.3 |
| **Claimed** | **39% of 44%** | |
| **Residual for D1.2 / Ch 8 (Administration)** | **5%** | |

**D1.1 totals 25% across four chapters.** Five points remain for Chapter 8 — tight but
defensible, and unlike the 16-point projection it is a number Chapter 8 can be drafted *to*.
**Chapter 8 is the next chapter to draft; this is the input its outline needs, and it is the
first chapter in the book whose allocation is determined rather than chosen.**

### ⚑ The disclosure form is now six phrasings deep and nobody has ruled

Chapter 6 invented a sixth: `Authored weight: ~6% of this book` — which makes a **different
claim** than every other chapter ("of the exam"). Chapter 5's ledger, Chapter 7's ledger and
Stage 13 now all independently recommend the same resolution: adopt `chapter-05:190`'s form
(share **of the exam**, with the authored-allocation disclosure and source tag inline), and
make that the pattern `reconcile.py` sweeps the other five to. The competency separator drifts
three ways as well (`— competency: X` / `— X` / `(X)`); pick one at the same time.

⚑ **Chapter 6's own AUTHOR-REVIEW instruction is not executable.** It says "match the exact
disclosure phrasing used in the metadata lines of Chapters 2–5." Those four chapters use four
different phrasings and Chapter 2 has no line in that pattern. **There is no form to match;
one has to be chosen.**

---

## ⚑ COMPETENCY COUNT — 13, not 12. A shipped error, source-tagged.

Chapter 1's ledger flagged this and asked for B2 to be corrected "before Chapter 19's
synthesis." It wasn't, and the error has left the outline and entered print.

`sources/cncf-kcna-curriculum-pdf-2026-08-23.md` enumerates 4 + 4 + 2 + 3 = **13**.

- **B2** (`chapter-lineup.md:7, :11`) says 12, twice. **Wrong.**
- **`chapter-05:448` ships**, in reader-facing prose: *"one of the twelve named KCNA
  competencies **[source: cncf-kcna-curriculum-pdf-2026-08-23]**."* A factual error about a
  certifying body, source-tagged to the document that disproves it. It arrived as a Stage 6
  *remediation* (finding C2) that inherited B2's bad number.
- **Chapter 6** repeats it in a metadata AUTHOR-REVIEW comment — not reader-facing, materially
  lower severity, but a third propagation.
- **ch-06's curriculum-alignment audit** states it as fact, so the audit instrument and this
  ledger now disagree.

**Fix order:** B2 (one token, twice) → `chapter-05:448` (one word, shipped text) → strike the
count from ch-06's AUTHOR-REVIEW. Outside Stage 14's write scope.

---

## ⚑ Ethical-guardrail status — Chapter 6, and one open item CLOSED

| Chapter | Guardrail #3 | Guardrail #8 |
|---|---|---|
| Ch 1 | pass | pass |
| Ch 2 | pass | pass — models the compliant phrasing |
| Ch 3 | pass | **FAIL — open** |
| Ch 4 | pass | BORDERLINE |
| Ch 5 | pass | BORDERLINE |
| Ch 7 | ⚑ **FAIL — open** (competitor-pedagogy claim, L1113) | BORDERLINE |
| **Ch 6** | **pass** | **BORDERLINE — improved: four unbacked claims, down from ten** |

**✅ First chapter since Chapter 2 to ship zero exam-frequency claims**, and it got there by
remediation: Stage 6's F-2 caught six and all six were fixed. The Exam Alert's replacement
framing — *"in descending order of how much of this chapter depends on them"* — is a
**dependency** claim about the book, not a frequency claim about the exam. **Recommend it as
the pattern for the other chapters' Exam Alert headings.**

**✅ Stage 13's open verification item #14 is CLOSED, favourably.** B1 trap **#21** is
`[source]`, not `[inferred]` (`domain-analysis.md:524`) — and so are **#22** (:525) and **#23**
(:526). All three of §7's ⚠ Navigational Hazards traps are source-backed, so B2's constraint
at `chapter-lineup:184` does not bind them. **No edit needed.**

**Four claims remain unbacked**, the same practitioner-prevalence register Chapters 4, 5 and 7
carry: "the most consequential wrong answer in this chapter," "the most common wrong answer,"
"you are in the majority"/"you are in good company," and "the first thing most people check."
None maps to a numbered B1 trap. **Guardrail #8 is four chapters running after Chapter 3's
open FAIL; Chapter 7's ledger already established that the overdue thing is the ruling, not
the edit.**

**Guardrail #3 clean, and instructive given Chapter 7's fresh FAIL.** Chapter 6 makes no claim
about other study guides. Its one adversarial move — *"Treating `Recreate` as always-wrong is
its own trap"* — is aimed at a practice, defended with three concrete cases, and re-framed as
correct engineering. **That is the construction Chapter 7's L1113 needed.**

**Three Part 14 items pass unusually well.** Zero statistics anywhere. The **Order/Truth
balance is the best in the book so far**, in three places: §1's "the number is written twice";
§4's `Dead Reckoning` block; and §6's *"A loop left open on purpose,"* which tells the reader
the deferral is deliberate rather than an omission. And the **v5.7 subject-dignity guardrail is
clean** — every wry beat lands on the practitioner, and §4's stalled-rollout Snag, the one
place a consequence narrative could have drifted toward third parties, closes on *"Users
experience nothing."*

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 6 update (2026-08-24)

**7 tagged in-budget items · graded pool 34 (15 Bearings + 19 Practice) · rate = 20.6%.**
B3's rung for Chapter 6 is **20%. Cleared — by the thinnest margin in the book** (Ch 5:
21.1%, Ch 7: 21.9%). Two further tagged items sit in Soundings (Q7, Q8), excluded from the
budget by B3 but doing the spacing work. Independently computed; matches question-quality.

**Chapter 6 draws from three predecessors** — Ch 3, 4 and 5. Chapter 5 also drew from three;
Chapter 7 from four. The breadth plateaued here and resumed climbing after.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| the control loop — two states and an action | ch 3 §6 | **ch 6** — Soundings Q7 *(excluded)* |
| a Pod is replaced, not rescheduled; who replaces it was left open | ch 5 §4 | **ch 6** — Soundings Q8 *(excluded)* |
| desired state, current state, the action — with the field name | ch 3 §6 | **ch 6** — Bearings #1 Q4 |
| two independent selectors over one Pod | ch 4 §5 | **ch 6** — Bearings #1 Q5 |
| readiness probes; a Pod that never reports ready | ch 5 §7 | **ch 6** — Bearings #2 Q4 |
| `spec` holds what you asked for, `status` what is running | ch 4 §2 | **ch 6** — Practice Q2 |
| the replacement Pod gets a new UID; recorded identity goes stale | ch 5 §4 | **ch 6** — Practice Q5 |
| the five Pod phases; `Succeeded` = all terminated in success | ch 5 §5 | **ch 6** — Practice Q16 |
| a controller reads `.spec`, acts, writes `.status` | ch 3 §6 | **ch 6** — Practice Q19 |

### Quality notes

- **Practice Q5 is the strongest retrieval item in the chapter.** Its distractor D is *true of
  a different resource* — StatefulSet Pods keep their ordinal-derived names — and the key says
  so: "Which resource is holding the Pods decides which answer is right." It converts a
  retrieval item into a discrimination item using material from later in the same chapter.
- **Practice Q19 is the best structural item.** Two axes in one answer (what built-in and
  third-party controllers share; where each runs), and it is the direct precursor to Chapter
  15's central recognition. Bearings #3 Q5 sets it up; Q19 grades it.
- **✅ Chapter 7's improvement was inherited, not lost.** Chapter 5's ledger recorded tags on
  stems but not in keys; Chapter 7 fixed it. Chapter 6 does the same — Q2's key names Chapter
  4's own forward bearing, Q5's names Chapter 9's stake, Q16's names Chapter 5's phase table.
- **⚑ Bearings #1 Q5 is tagged `ch4` but its load-bearing content is Chapter 6's own.** The
  stem is Ch 4 §5; the answer's actual teaching — "ownership is exclusive; selection is not" —
  is §3's. Same pattern Chapter 5's ledger recorded for *its* Bearings #1 Q5, which suggests a
  drafting habit rather than a one-off.
- **⚑ One prescribed anchor dropped at zero benefit.** The outline (line 420) asked §3 to
  reference `ch04-fig03-labels-selectors-join` **by name** rather than redraw the join —
  "which is also a spacing-effect retrieval at zero cost." The figure exists at
  `chapter-04:806` and its caption is load-bearing. Chapter 6 never mentions it. **One clause
  recovers a free retrieval on the exact theme Chapter 6 was told to retrieve.**

---

## ⚑ Chapter 7's six-item Chapter 6 debt — DISCHARGED, with one correction

| # | Assumption | Verdict |
|---|---|---|
| 1 | Ch 6 §1 covers Deployments/ReplicaSets and create-the-missing-Pod | ✅ discharged (§1 the chain, §2 the demonstration) |
| 2 | Ch 6 §7 covers DaemonSets, one-per-node | ✅ discharged |
| 3 | Ch 6's Voyage Ahead ends on the scheduler gap | ✅ discharged |
| 4 | Ch 6 §7 plants the DaemonSet-tolerations tease "in disguise" | ✅ **discharged — see the correction below** |
| 5 | Ch 6 exists as the third of "Chapters 4 through 6" | ✅ discharged |
| 6 | Ch 7 §7's "same shape as every controller in Chapter 6" | ✅ **now a stronger claim** — §9's Zenith *is* that figure. Ch 3 §6 remains the better anchor for the loop's *definition*; **downgrade from blocking to optional** |

### ⚑ DO NOT APPLY Stage 13's Fix #11. Chapter 7:696 is accurate.

Stage 13 reports that "Chapter 6 says neither of those things" and that *"nothing else will"*
and *"in disguise"* "appear nowhere in chapter-06," and recommends rewriting Chapter 7's line
696 into a hand-back.

**Both phrases are in one sentence at `ch-06:894`**, which also carries the **correct**
`Ch 7 §4` pointer. Chapter 7's callback is a faithful paraphrase. Applying Fix #11 would
replace a correct callback with a weaker one and discard the setup Chapter 7 pays off. Likely
cause of the miss: Stage 13's grep matched line 894 and reported it as omitted — the
long-line/compound-emoji failure mode CLAUDE.md warns about.

**Stage 13's Fix #1 targets a different pointer and is correct:** `ch-06:965`, closing §7,
says `Ch 7 §5`. Ch 7 §4 is *When the Berth Refuses You* (taints); §5 is *Placing Pods Relative
to Each Other*. **Chapter 6 currently points at two different Chapter 7 sections for the same
material.**

---

## Cross-cutting themes — ⚑ §8 is the first landing site for two stalled themes

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **The control loop** (B3 headline) | Ch 3 §6 | Ch 4 · Ch 5 · ✅ **Ch 6 — FIRST PLANNED retrieval, and it lands as the Zenith** · Ch 7 | **Ch 11 (still unbeared)**, Ch 15, Ch 17 |
| **Labels/selectors as the universal join** | Ch 4 §5 | Ch 5 · Ch 7 ×2 · ✅ **Ch 6 ×3 — the planned Ch 6 retrieval lands** | Ch 9, Ch 10 |
| **The absent-component pattern** | Ch 3 §4, named | ✅ **Ch 6 §8 — FIRST retrieval in the book, and by name** ⚑ but with a rival string | Ch 10 ×2, Ch 13, Ch 17 |
| **"Kubernetes defines an interface, the ecosystem implements it"** | Ch 2 §4, named | ✅ **Ch 6 §8 — FIRST named recurrence in the book** | Ch 9 (CNI), Ch 11 (CSI), Ch 17 |
| **Namespaced vs cluster-scoped** | Ch 4 §3 | Ch 5 §6 — ⚑ **Ch 6 walked past a free one** | Ch 12 §3, Ch 10, Ch 11 |

**§8 is the highest-value 1,200 words in the book so far, measured by theme architecture.** The
Chapter 5 and Chapter 7 ledgers both recorded the absent-component pattern and the
interface/ecosystem pattern as **"still zero"** — two of B3's nine themes, both named in print,
neither ever retrieved. §8 lands both, in one section, both explicitly by name.

**⚑ The absent-component landing carries a canon conflict.** §8 uses B3's canonical string
(`retrieval-architecture.md:15`) — *"the object exists but nothing happens without the
component"* — while `absent-component-pattern.md` carries a capitalised **"USE THIS NAME. DO
NOT RE-COIN IT"** for *"absent-component pattern."* **Chapter 6 is not re-coining; the shard
is the artifact that invented a competing string.** Both are legitimate; B3's reads better in
prose, the shard's is the only one that works as a noun in a Chapter 17 synthesis. **Author's
call, now urgent** — three chapters owe by-name retrievals and one shipped chapter has set a
precedent.

The instance roster is also now **five members across three different four-item lists**.
Chapter 6 adds CRD-with-no-controller (the only instance where the reader creates the orphaned
object themselves) and drops NetworkPolicy-on-a-non-enforcing-CNI.

**⚑ Still retrieved by paraphrase, and this is now four chapters.** §3 does the universal-join
work without `label-selector.md`'s canonical string ("the label selector is the core grouping
primitive in Kubernetes"). Chapter 5 paraphrased the namespaced/cluster-scoped string; Chapter
7 paraphrased the universal-join string; Chapter 6 paraphrased one and published a rival
coinage of another. **The deadline Chapter 7's ledger set — before Chapter 10 drafts — now has
three chapters left, and the cost of deciding has risen from a convention call to a
shipped-text edit.**

**⚑ A free retrieval Chapter 6 walked past.** Practice Q18's option-B rebuttal reads *"namespace
has nothing to do with it. Custom resource objects live wherever their scope allows."* Custom
resources are declared namespaced **or** cluster-scoped, which makes this the most natural site
the book will offer for retrieving Chapter 4 §3 — the fact is *demonstrable* here rather than
assertable, the same property Chapter 7's ledger identified for the Nodes case. One clause.
This theme still has **one** retrieval in six chapters, by paraphrase.

**⚑ `reconciliation` — the line held for a second chapter.** Chapter 7 used the word zero
times. Chapter 6 uses it once, in §1's Fixed Point discussion ("accepting it and reconciling
toward it"), and **never in an answer key**. The gap has not closed but has not grown for two
chapters, and both demonstrate the mechanism can be described without the term. The
one-appositive fix at Chapter 3's ★ Fixed Point remains the right close.

---

## ⚑ §N reservation collisions — nine new, plus one Chapter 6 has with itself

| Destination | Claimants | Status |
|---|---|---|
| **Ch 13 §2** | Ch 2 / Ch 5 (`ImagePullBackOff`) · **Ch 6 §8** (`kubectl top`) | ⚑ conflict |
| **Ch 13 §4** | Ch 5 (`OOMKilled`/`Evicted`) · **Ch 6 §2** (metrics-server) | ⚑ conflict |
| **Ch 13 §3** | Ch 5 (multi-container logs) · **Ch 6 §4** (stuck rollout) | ⚑ conflict |
| **Ch 6 internal** | §2 → `Ch 13 §4` · §8 → `Ch 13 §2` | ⚑ **two sections for metrics-server, one chapter** |
| **Ch 9 §1** | Ch 2 (CNI) · Ch 5 (why a Service is necessary) · **Ch 6 §2** | ⚑ **three-deep**; Ch 2 has precedence |
| **CNI's home in Ch 9** | Ch 2 → §1 · **Ch 6 → §7** | ⚑ same subject, two sections |
| **Ch 15 §4** | Ch 5 (delivery agent identity) · **Ch 6 §4** (blue/green, canary, A/B) | ⚑ conflict |
| **Ch 17 synthesis** | Ch 2 → §4 · **Ch 6 → §6** | ⚑ **highest-stakes** — four chapters' theme converges there |
| **Ch 18 §3** | Ch 5 (utilization vs requests) · **Ch 6 §7** (node-level logs) | ⚑ conflict |

**✅ The house has already started fixing this, twice, independently.** Chapter 4's re-draft
(`73fd066`) stripped section numbers from **all three** of its Chapter 6 pointers, and Chapter
2's most recent commit is titled *"Ch-02: drop §3 from the Ch 7 pointer."* **Recommend
ratifying the convention:** no `§N` in forward bearings into undrafted chapters; keep it on
backward bearings into published ones, where it is verifiable. Nine conflicts and one
self-contradiction retire in one pass.

### ⚑ The outline's numbering warning is stale and will mislead the next session

`ch-06/outline.md` lines 18–30 and the chapter frontmatter both record that **§3 is pinned by
`chapter-04:688`** and that the Chapter 1 / Chapter 2 collisions therefore cannot be resolved
by renumbering. **That pin no longer exists** — Chapter 4's re-draft dropped the number. The
fixes are unchanged (`chapter-01:436` → `§6`; `chapter-02:600` → `§8`), but the *constraint* is
gone. Correct § Open questions #1 and the frontmatter at reconcile. `label-selector.md` carries
the same stale three-way claim.

---

## Forward commitments — two discharged, one overdue, eight new

| # | Commitment | Status |
|---|---|---|
| 1 | Ch 13 must carry a Ch 8 retrieval item (version skew) | **OPEN** |
| 2 | Ch 11 must retrieve the control loop | ⚑ **OPEN, five chapters overdue.** Ch 6 bears to Ch 11 §4 and **does not carry the loop.** Ch 3, 4, 5, 6, 7 have each passed it forward |
| 4 | Ch 12 must **derive** the RBAC 2×2 from the namespaced boundary | **OPEN.** Ch 6 surfaces RBAC twice with no bearing |
| 5 | Ch 9 must retrieve the Pod IP / shared namespace | **OPEN.** Ch 6 §2 bears to Ch 9 §1 on *stable names*, not the IP |
| 6 | Ch 13's method must be "read the phase before you read the logs" | **OPEN** |
| 7 | Ch 6 must open on "if Pods are designed to be replaced, who does the replacing?" | ✅ **DISCHARGED, three ways** — the opening quotes `chapter-05:1460` verbatim, §1 re-opens on it in four words, and Soundings Q8 grades the handoff. **The book's cleanest cross-chapter seam** |
| 8 | Ch 7, 13, 17, 18 must each retrieve requests/limits | Ch 7 discharged; **Ch 13, 17, 18 OPEN.** Ch 6 does not touch it, correctly |
| 9–12 | Ch 7's four (filter-vs-score, capacity-vs-taint, Ch 17's scheduler socket, Ch 8's `unschedulable`) | **OPEN, unchanged** |
| 13 | **Ch 15 must be the third sighting of the control loop, desired state in Git** | **NEW, and the largest.** §9 publishes it outright, and the Safe Harbor tells the reader "the third time is the one that matters." B3 calls this the book's primary Zenith; **Chapter 6 has now promised it in print** |
| 14 | **Ch 15 §4 owns blue/green, canary and A/B** | **NEW.** Ch 6's single authorized bearing is the chapter's only mention and it names the section |
| 15 | **Ch 11 must complete the StatefulSet storage half** | **NEW.** §6 names what is owed: PV, PVC, StorageClass, access modes, provisioning |
| 16 | **Ch 9 must define the headless Service** as StatefulSet network identity | **NEW.** §6 says "you are responsible for creating it" and defines nothing |
| 17 | **Ch 13 §3 must diagnose a stuck rollout and name which of the six causes fired** | **NEW.** §4 publishes the full list and assigns the diagnosis |
| 18 | **Ch 17 must resolve CRI, CNI, CSI and CRD into one story** | **NEW.** ⚑ Ch 6 pins §6; Ch 2 published §4 |
| 19 | **Ch 14 §6 must explain why Helm charts have a `crds/` directory** | **NEW.** Cheap, and it is a `custom-resource.md` consequence rather than a Helm fact |
| 20 | **Ch 10, 13 and 17 must retrieve the absent-component pattern using ONE string** | **NEW, blocking on the author.** Chapter 6 has shipped a rival canonical phrasing |

=== END APPEND ===

---

## The headline for you

**Chapter 6 is the best-audited chapter in the book, and §8 is the most valuable section the book has produced.** Fact-accuracy inspected 236 claims with **zero contradictions**, raised five FAIL findings, and **all five were actually fixed** — plus half the WARNs and the one absent sub-objective. Every one of the 23 multiple-choice items carries complete per-option why-wrong treatment, a first. And §8 lands **two cross-cutting themes that had been dead since Chapters 2 and 3** — the absent-component pattern and "Kubernetes defines an interface, the ecosystem implements it" — in the same 1,200 words, both by name.

**Four things need your decision, in rough order of cost-if-ignored:**

1. **Don't apply Stage 13's Fix #11.** Chapter 7:696 is accurate — both phrases Stage 13 reported missing are in `ch-06:894`, in one sentence, with a correct `Ch 7 §4` pointer. Its Fix #1 (the *other* pointer, at `ch-06:965`, which says `§5`) is right and should be applied.
2. **`chapter-05:448` ships a factual error about CNCF, source-tagged to the document that disproves it.** The curriculum enumerates **13** competencies; Chapter 5 says twelve. It came in as a Stage 6 remediation that inherited B2's bad number, and Chapter 6 propagated it into an AUTHOR-REVIEW comment and the ch-06 audit. One word in shipped text, one token twice in B2.
3. **The absent-component pattern has two canonical names, and Chapter 6 published B3's.** The Chapter 3 shard forbids re-coining while itself being the coinage that diverged. Three chapters still owe by-name retrievals — this is cheapest to settle now.
4. **The outline's "§3 is pinned by chapter-04" warning is stale** — Chapter 4's re-draft dropped that pin. The `§3 → §6` and `§3 → §8` fixes for chapters 1 and 2 are still right; the *reasoning* recorded in the outline and in `label-selector.md` will send the next session down a dead end.

**Two things I closed that were left open elsewhere:** B1 trap #21 is `[source]`, not `[inferred]` (so are #22 and #23) — Stage 13's verification item #14 needs no edit. And **Chapter 8's allocation is now determined: 5%, D1.2 Administration**, the residual after six chapters of Kubernetes Fundamentals. That is the number its outline needs before it drafts.

**Unchanged and still broken:** the KB write path. Sixth manifest. Nothing in `certcomp` parses `=== WRITE`, `certcomp/tools/` doesn't exist, and `Book-KCNA/knowledge-base/` is still empty. Replay order is now **ch-01 → ch-03 → ch-04 → ch-05 → ch-06 → ch-07**; the materializer is above.
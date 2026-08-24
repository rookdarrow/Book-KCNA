I have everything I need — the arc-outline brief, the retrieval schedule, the trap inventory, the cached sources, and (critically) two **published cross-bearings that pin this chapter's section numbering**. Emitting `outline.md`:

---

```
---
chapter: 4
chapter_type: "content"
title: "Records of Intent"
subtitle: "You don't give Kubernetes orders. You file a declaration."
exam_domain: "Kubernetes Fundamentals (competency: Kubernetes Core Concepts)"
domain_weight_pct: 6
complexity: "mixed"
novelty: "paradigm-shifting"
prereq_factor: "standard"

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band for this chapter:
#-- "standard-plus" - 6 points, but two of the book's nine cross-cutting
#-- themes originate here (namespaced-vs-cluster-scoped; labels/selectors as
#-- the universal join). Planning signal only, NOT a target.
#--
#-- WARNING SECTION NUMBERING IS LOAD-BEARING AND ALREADY PUBLISHED. Two
#-- shipped chapters name sections of this chapter by number:
#--   chapter-01 line 150 -> *[cross-bearing: see Ch 4 §1 - declarative versus imperative]*
#--   chapter-02 line 459 -> *[cross-bearing: see Ch 4 §4 - Secrets, and the `dockerconfigjson` type]*
#-- §1 and §4 below honor those. §4 is the reason ConfigMaps/Secrets sit
#-- ahead of labels/selectors rather than after them. Do not renumber
#-- without editing both published chapters.
#--
#-- NOTE Frontmatter comments use "#--" with no following space. This was a
#-- defensive mitigation for the runner's slugifier (see Ch 3 Open questions
#-- #4); commit 5f1a1d2 now derives the slug from `title`, so the mitigation
#-- is belt-and-braces rather than load-bearing. Retained; costs nothing.
sections:
  - name: "You File a Declaration"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "The Anatomy of a Record"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch04-fig01-object-anatomy-spec-status"
    checkpoint_after: true
  - name: "Where a Name Lives"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch04-fig04-namespaced-vs-cluster-scoped"
    checkpoint_after: false
  - name: "Configuration Kept Outside the Image"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch04-fig05-configmap-secret-contrast"
    checkpoint_after: true
  - name: "The Universal Join"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch04-fig03-labels-selectors-join"
    checkpoint_after: true
  - name: "A Declaration, Not an Order"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch04-zenith-declaration-not-order"
    checkpoint_after: false

#-- ch04-fig02-apply-round-trip also lands in §2, as that section's closing
#-- beat. §2 is the only section carrying two figures; justification in
#-- § Required figures. §1 deliberately carries none.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "a file describing what infrastructure should look like, versus a script that builds it"
    - "why a configuration file format carries a version or schema field at the top"
    - "the two halves of the control loop, in the reader's own words"
    - "which component receives a submitted description, and what actually stores it"
    - "one container image, two environments - where the differing configuration comes from"
    - "whether base64 is encryption"
    - "how you select a subset of things by attribute in systems the reader already knows"
    - "two teams, one shared system, and the same name wanted twice"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 19 = 37. Bearings raised 10 -> 13; see
#-- § "Taking Your Bearings checkpoints" for justification and B4's sanction.
question_budget:
  soundings: 8
  taking_your_bearings: 13             # across 3 checkpoints (5 + 4 + 4)
  practice_questions: 19
  total_this_chapter: 40

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.1"]
  concepts:
    - "kubernetes-object"
    - "record-of-intent"
    - "persistent-entity"
    - "declarative-configuration"
    - "imperative-command"
    - "imperative-object-configuration"
    - "declarative-object-configuration"
    - "manifest"
    - "yaml-by-convention"
    - "apiversion"
    - "kind"
    - "metadata"
    - "object-name"
    - "object-uid"
    - "spec"
    - "status"
    - "desired-state"
    - "current-state"
    - "actual-state-reconciliation"
    - "namespace"
    - "scope-for-names"
    - "initial-namespaces"
    - "default-namespace"
    - "kube-system"
    - "kube-public"
    - "kube-node-lease"
    - "namespaced-resource"
    - "cluster-scoped-resource"
    - "namespace-not-nested"
    - "namespace-dns-form"
    - "configmap"
    - "configmap-size-limit"
    - "configmap-consumption-paths"
    - "immutable-configmap"
    - "decoupling-configuration"
    - "secret"
    - "secret-types"
    - "opaque-secret"
    - "dockerconfigjson"
    - "service-account-token-secret"
    - "tls-secret"
    - "secret-storage-default"
    - "secret-hardening"
    - "encryption-at-rest"
    - "label"
    - "label-selector"
    - "equality-based-selector"
    - "set-based-selector"
    - "matchlabels"
    - "matchexpressions"
    - "annotation"
  commands:
    - "kubectl-apply"
    - "kubectl-get"
    - "kubectl-create"
    - "kubectl-explain"
    - "kubectl-api-resources"

figures_planned:
  - "ch04-fig01-object-anatomy-spec-status"
  - "ch04-fig02-apply-round-trip"
  - "ch04-fig03-labels-selectors-join"
  - "ch04-fig04-namespaced-vs-cluster-scoped"
  - "ch04-fig05-configmap-secret-contrast"
  - "ch04-zenith-declaration-not-order"
---

# Chapter 4 Outline — Records of Intent

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 4: Records of Intent` | required | top |
| `## *"You don't give Kubernetes orders. You file a declaration."*` | required | line 2 |
| Metadata line (weight / complexity / novelty) | required | after subtitle |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings` ×3 | **required, min 2** | after §2, §4, §5 |
| `★ Fixed Point` ×4 | **required, min 1** | §2, §3, §4, §5 |
| `**Dead Reckoning:**` ×1 min | **required** | §2 (the four fields, plainly) |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §4 (the secrecy misconception), §5 (labels vs annotations) |
| `☀️ Zenith` | expected | §6 |
| `## Exam Alert` | **required** | after §6 |
| `## Practice Questions` | **required** | 19 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19 |
| `🏆 Safe Harbor` | expected | chapter close |

**Zenith:** exactly one, per Part 18.10. `ch04-zenith-declaration-not-order` in §6. This chapter carries five concept diagrams, which is at the upper end of the 2–8 band; none of them may be dressed as a second Zenith.

**Attention Budget guidance for drafting.** Four attention costs, and they are genuinely different: §1 low (reframing, mostly prose), §2 medium (new vocabulary, four field names, one abstraction), §3 medium (a boundary and a list), §4 medium-high (two objects, eight Secret types, four consumption paths, and a misconception to dismantle), §5 medium (one primitive, two syntaxes), §6 low (synthesis). The "if you only have 15 minutes" line should point at **§2 plus Bearings #1** — spec/status is the field-name payoff of the whole first quarter of the book.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 4 — Records of Intent". Carried forward without modification:

- **Covers**: **D1.1** — objects; spec/status; manifests; `apiVersion`/`kind`/`metadata`/`spec`; `kubectl apply`; labels; selectors (equality and set-based); annotations; namespaces; initial namespaces; **namespaced vs cluster-scoped**; ConfigMaps; Secrets (definition and contrast).
- **Prerequisites**: Ch 3 — control loop, kube-apiserver, etcd as state of record.
- **Retrieval targets**: **15%** **[B3]** — from Ch 2–3. Named anchors: the control loop (*what does the controller compare `spec` against?*), image references inside a Pod spec, the apiserver's role in `apply`.
- **Question budget**: 8 Soundings · 10 Bearings · 19 Practice · 37 total. Bearings raised to 13 below.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: standard-plus.

**What this chapter inherits — and one debt Chapter 3 deliberately left unpaid.**

Chapter 3 Open question #3 asked whether §6 should use the word `spec`. It resolved in favor of deferring: the published Chapter 3 teaches the control loop entirely in plain language — *"Those objects carry a field that represents the desired state"* — and closes with `*[cross-bearing: see Ch 4 — the field that holds desired state, and its status counterpart]*` (line 834). Its Voyage Ahead makes the promise explicit: *"that field has a name, and a counterpart that reports what actually is true, and a set of conventions for how you write both. Chapter 4 gives them to you."*

That is a debt with a due date, and §2 is where it comes due. Draft §2 knowing the reader has been told to expect exactly this. Naming `spec` and `status` should land as a promise kept, not as new vocabulary arriving unannounced — one clause acknowledging the handoff is enough, and more than one is a callback that has started admiring itself.

**What this chapter owes forward.** Two of the book's nine cross-cutting themes originate here, and one figure is load-bearing for a chapter eight ahead:

| Concept | Retrieved at | Contract |
|---|---|---|
| **Namespaced vs cluster-scoped** (theme 2) | Ch 8 (ResourceQuota, admission), Ch 12 (**the RBAC four-way matrix**) | **[B3]**: Ch 12 must *derive* Role/ClusterRole × RoleBinding/ClusterRoleBinding from this boundary, not memorize it as a table. `ch04-fig04` is the artifact that makes the derivation possible |
| **Labels and selectors as the universal join** (theme 5) | Ch 6 (ReplicaSet→Pod), Ch 7 (node labels), Ch 9 (Service→Pod), Ch 10 (**≥4-back floor**, NetworkPolicy→Pod), Ch 12 (the contrast: RBAC uses subjects, not selectors) | Named anchor five times. The single most reused *mechanism* in the book, as the control loop is the most reused *idea* |
| **Declarative desired state vs imperative command** (theme 4) | Ch 6, Ch 14 (Helm), Ch 15 (GitOps) | §1 is the origin. Ch 15's OpenGitOps principle "declarative" retrieves it by name |
| `spec` / `status` | Ch 5 (**named anchor** — spec/status read against Pod phase), Ch 6, Ch 13 | The vocabulary every later chapter assumes |
| ConfigMap / Secret | Ch 5 (as env and volume sources), Ch 11 (**named anchor** — as volume types), Ch 12 (Secret hardening, the full security treatment), Ch 15 (**reciprocal pair** — twelve-factor factor III) | Ch 4 defines and contrasts; Ch 12 secures. Do not pre-empt Ch 12 |
| `kubectl apply` | Ch 8 (full command surface), Ch 14 (**≥4-back floor** — `apply` vs `helm install`) | Ch 4 teaches one verb because objects are unteachable without it; Ch 8 teaches the surface |

**Scope boundary with Chapter 8 — state it once and hold it.** Chapter 8 owns kubectl: syntax, verbs, kubeconfig, in-cluster auth, the three API access gates. Chapter 4 uses `kubectl apply -f` because you cannot teach a record of intent without showing the reader how a record gets submitted, and it uses `kubectl get`, `kubectl explain`, and `kubectl api-resources` at the same minimal altitude. It teaches none of them as commands. If a paragraph starts explaining flags, it belongs in Chapter 8.

**Reader positioning**: Communications Officer role family, **junior tier**. Single unified brand voice; only atmospheric register and reader rank differ.

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**The curiosity gap: nothing in this chapter is a verb.** The reader has spent three chapters learning about a system that runs software, and is now going to spend a chapter learning to write files that describe what should be true and then hand them to something that never receives an instruction. Open the gap on the asymmetry: you will not, anywhere in this chapter, tell Kubernetes to do anything. You will state what you want to exist. Something else — the loops from Chapter 3 — does the doing, and you never address it directly. Readers arriving from imperative operations tooling find this genuinely strange for about a chapter, and the strangeness is worth naming rather than smoothing over. Keep it open through §2–§5 and pay it off in §6.

**The identity frame is authorship, not command.** Chapter 3 gave the reader a system to look at; Chapter 4 gives them something to write. That is the shift from reading an architecture to operating one, and it is the point at which the control loop stops being a diagram — the published Chapter 3 Voyage Ahead says exactly this, so §1 can lean on it rather than re-argue it. The practitioner's version: someone who has this chapter can be handed any Kubernetes YAML they have never seen, for a resource type they do not know, and still parse it — because the four top-level fields are the same four fields every time, and `kubectl explain` covers the rest. That transfers to resource types that did not exist when this book was printed, which is the honest reason it matters more than its six points suggest.

**The stakes are structural and should be stated without inflation.** Six points on this book's authored judgment (CNCF publishes no sub-competency weights — see § Open questions #7). But this is the chapter every later chapter reads *through*: Chapter 5's Pod is an object with a spec, Chapter 6's controllers select by label, Chapter 9's Service selects by label, Chapter 12's RBAC is a namespaced-versus-cluster-scoped problem wearing a costume. A reader who leaves able to recite the four fields but unable to explain what `status` is *for* will re-learn this chapter four times in worse conditions. Say that calmly, once. No manufactured urgency — this reader is an adult professional and Part 14 forbids it.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Five outcomes, active verbs:

- **Read** any Kubernetes manifest you have never seen before, name its four required fields, and say what each one is doing.
- **Distinguish** `spec` from `status` — who writes each, which one you set, and which one the system maintains — and connect both to the control loop you already know.
- **Predict** whether a given resource is namespaced or cluster-scoped, and explain why the answer determines who can be given permission over it.
- **Select** a set of objects by label using both equality-based and set-based syntax, and explain why an annotation cannot be selected on.
- **Choose** between a ConfigMap and a Secret for a piece of configuration — and state precisely what protection the Secret does and does not add.

*You'll also stop reading YAML as an opaque wall of configuration and start reading it as four fields, one of which is the interesting one.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Chapter 4's prerequisite set is Chapter 3's control loop, kube-apiserver, and etcd-as-state-of-record, plus general IT literacy. Six questions test **priors the reader arrives with**; two are deliberate retrieval from Chapter 3. **[B3]** Soundings are excluded from the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column — Chapter 4's entire prerequisite column is Chapter 3, so this block is doing more spacing work than Chapter 3's did.

**Fixed Points this chapter teaches, which Soundings must therefore not reveal:** (1) `spec` and `status` are the control loop's two halves and who writes which; (2) namespaced versus cluster-scoped, and the named exceptions; (3) neither ConfigMap nor Secret encrypts anything; (4) the label selector is the core grouping primitive and annotations cannot be selected on. Each question below is checked against that list.

| # | Question topic | What it tests | Spoiler check |
|---|---|---|---|
| 1 | A file that describes what infrastructure *should* look like, versus a script that performs the steps — what is that distinction called, and what does the first buy you? | The declarative prior, in its general form | Published Ch 1 Soundings Q5 asked the *self-report* version ("have you written Terraform/Ansible/CloudFormation?") and forward-pointed here explicitly. This asks the **knowledge** form. §1's teaching is Kubernetes-specific — the object as a persistent record of intent, and the three object-management techniques — so a general prior spoils nothing |
| 2 | When a configuration file format puts a version or schema field at the very top, what problem is that solving? | An `apiVersion` prior from any versioned config format the reader has met | Names no Kubernetes field. §2 teaches what `apiVersion` selects and why Kubernetes needs it per-object rather than per-file |
| 3 | **Retrieval from Ch 3 §6** — a control loop has two states in it. Name them, and name the third thing that closes the gap. | **[B3]**'s designated control-loop anchor, in its pre-test position | This is the anchor's *setup*, not its payoff. The Fixed Point is that these two states have field names, one of which you write and one of which you never do. Retrieving desired/current state reveals none of that — and the reader who cannot answer gets a clear signal to re-read Ch 3 §6 before §2, which is exactly the calibration Soundings exists for |
| 4 | **Retrieval from Ch 3 §5** — you submit a description of something you want to exist. Which component receives it, and what actually stores it? | **[B3]**'s "apiserver in `apply`" anchor | kube-apiserver and etcd are Chapter 3's Fixed Points, not this chapter's. §1 places the reader's new artifact into that flow; it does not reveal the flow |
| 5 | The same container image runs in development and in production, and needs a different database address in each. Where does the difference come from? | The externalized-configuration prior (and the twelve-factor instinct, if the reader has it) | §4's Fixed Point is that neither ConfigMap nor Secret provides secrecy, plus the 1 MiB ceiling, the four consumption paths, and immutability. A reader who answers "environment variables" has the prior and still learns all of that |
| 6 | Is base64 encoding a form of encryption? If not, what is it for? | A general-IT prior — and the chapter's most valuable pre-test | **The single best question in this block.** It surfaces the misconception *before* §4 corrects it, which is the pretesting effect working exactly as Richland describes. It never mentions Secrets, so it cannot spoil the Fixed Point; it just ensures the correction lands against a mental model the reader has already been made to notice |
| 7 | In a system you already know — SQL, cloud resource tags, a ticketing system — how do you ask for "all the things with this attribute"? | The selector prior by analogy | §5 teaches Kubernetes' specific two-syntax implementation and the annotation contrast. The general prior is the ramp |
| 8 | Two teams share one system and both want to call something `database`. What would you expect a well-designed multi-tenant system to offer them? | The namespace prior | §3's Fixed Point is the namespaced/cluster-scoped **boundary** and its named exceptions — plus the docs' explicit warning that namespaces are the wrong tool for separating versions of one application. "Namespaces exist" is not the teaching |

**Rubric**: standard 6+ / 3–5 / 0–2 per `branded-terms.yaml`. The 0–2 branch here has a specific and useful instruction rather than a generic one: **if questions 3 and 4 were the misses, re-read Chapter 3 §5–§6 before starting §2** — those two are the load-bearing prerequisites and this chapter builds directly on top of them.

---

## 4. Section plan

Six sections. **§1 and §4 are pinned by published cross-bearings** (see the frontmatter warning); the ordering below is built around that constraint and is better for it — see the note under §5 for why config-before-labels turns out to be the right sequence anyway.

### §1 — ⚪ You File a Declaration

The reframing section, and short. Start where the documentation starts: Kubernetes objects are **persistent entities** that represent the state of your cluster — what is running and where, what resources are available to it, and the policies around how it behaves. Then the phrase the chapter is named for, quoted and dwelt on: an object is a **"record of intent"**, and once you create it, the system will constantly work to ensure that the object exists. Draw the consequence explicitly, because it is the whole chapter: creating an object is not a request that gets serviced and completed; it is a statement that gets *maintained*. Then the mechanics at the coarsest possible altitude — objects are worked with through the Kubernetes API, and `kubectl` makes those API calls for you, which is the reader's first sight of the tool they will use for the rest of the book sitting in the position Chapter 3 built for it. Close by naming the distinction Chapter 1 promised: imperative means you supply the steps, declarative means you supply the outcome, and Kubernetes' object model is the second. Name that the three management techniques exist (imperative commands, imperative object configuration, declarative object configuration) and that `kubectl apply` is the declarative one — then stop, because §2 needs the reader wanting to know what is *in* the file.

- **Objectives**: D1.1
- **Concepts introduced**: `kubernetes-object`, `record-of-intent`, `persistent-entity`, `declarative-configuration`, `imperative-command`, `imperative-object-configuration`, `declarative-object-configuration`
- **Sources**: `k8s-docs-objects-2026-08-23.md` (persistent entities; the three things objects describe; "record of intent"; desired state; the API as the way to work with objects; kubectl makes the calls). `k8s-docs-kubectl-overview-2026-08-23.md` (the `apply` verb — "apply a configuration change to a resource from a file or stdin"). ⚠ **The three-management-techniques taxonomy is not in the cached set** — see § Open questions #1
- **Figure**: none, deliberately. The reframing is verbal and a diagram of "declarative versus imperative" would be decoration, which Part 18.4 forbids. `ch04-fig02` is the visual argument for this section's claim and it lands one section later, once the reader has the vocabulary to read it
- **Checkpoint after**: no
- **Markers planned**:
  - `> **Extended Analogy:**` — the chapter's one sidebar, and it belongs here. Records of intent as ship's papers: a declaration filed with the harbormaster does not instruct anyone to do anything; it states what is aboard and where the vessel is bound, and it is the standing reference every subsequent action is checked against. **Density constraint:** one sidebar; the metaphor stays inside it and does not leak into §2–§5's body prose. Per B2's density guidance the rest of the chapter runs plain
  - `> 🔭 **Closer Look:**` — the three object-management techniques, with the honest note that mixing them on one object causes trouble and that Chapter 8 covers the command surface properly. Gated on § Open questions #1
- **Cross-bearings**: back to Ch 1 §5's Soundings answer (**mandatory — this is the pinned payoff**; the reader was told this section would name the distinction, so name it and say so); back to Ch 3 §5 (the API server as the only door in — the record goes *through* it); forward to Ch 15 (the same word, "declarative", as an OpenGitOps principle)
- ⚠ **Do not teach `apply` versus `create` versus `replace` semantics here.** One sentence establishing that `apply` is the declarative verb is the budget. Server-side apply and field management are above associate tier and appear in no cached source
- ⚠ **Precision guard.** "You never give Kubernetes orders" is the subtitle's claim and it is not literally true — `kubectl delete`, `kubectl scale`, and `kubectl exec` are all imperative and all normal. §1 should not overclaim; the accurate framing is that the *object model* is declarative and imperative commands work by mutating declarations. §6 handles this properly; §1 just must not dig a hole §6 has to climb out of

### §2 — ⚪ The Anatomy of a Record

The chapter's core, and the section that pays Chapter 3's debt. Two movements. **First, the shape:** when you create an object you provide a description of its desired state plus basic identifying information, most often in a file called a **manifest**, which is YAML by convention. Four fields, every time, on every object the reader will ever meet — `apiVersion` (which version of the API you are using to create this object), `kind` (what kind of object), `metadata` (data that uniquely identifies it: a name string, a UID, an optional namespace), and `spec` (what state you desire). Apply it with `kubectl apply -f`. Land the transferability point from § Why This Chapter Matters here: this is the *only* structural knowledge needed to read an unfamiliar manifest, and it does not expire.

**Second, the payoff:** almost every object has two nested fields, and they are not symmetrical. You set `spec` when you create the object — the characteristics you want. `status` describes the *current* state, **supplied and updated by the Kubernetes system and its components**, and the control plane continually and actively manages every object's actual state to match the desired state you supplied. Then the documentation's own worked example, which is worth using verbatim in structure because it is a control loop the reader can already read: a Deployment spec says three replicas; the system reads it and starts three; one fails, which is a *status* change; the system responds to the difference between spec and status by starting a replacement. Say plainly what that means — Chapter 3's "field that says what should be true" is `spec`, its counterpart is `status`, and the gap between them is the thing every controller in the cluster is closing. End with `ch04-fig02`.

- **Objectives**: D1.1
- **Concepts introduced**: `manifest`, `yaml-by-convention`, `apiversion`, `kind`, `metadata`, `object-name`, `object-uid`, `spec`, `status`, `desired-state`, `current-state`, `actual-state-reconciliation`, `kubectl-apply`, `kubectl-explain`
- **Sources**: `k8s-docs-objects-2026-08-23.md` — nearly the whole snapshot, which covers this material completely (spec/status asymmetry, the Deployment three-replica example including the status-change-and-correction beat, the four required fields with their definitions, manifests-are-YAML-by-convention, `kubectl apply -f`). `k8s-docs-controllers-2026-08-23.md` for the loop connection
- **Figures**: **`ch04-fig01-object-anatomy-spec-status`** (first movement) and **`ch04-fig02-apply-round-trip`** (second movement, closing beat). The only section carrying two; justified in § Required figures
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — **`spec` is what you want; `status` is what is. You write `spec`. The system writes `status`. Every controller in the cluster exists to close the distance between them.** Phrase this to be quotable verbatim in Chapters 5, 6, and 13, because all three retrieve it. First and most important Fixed Point of the chapter
  - `> **Dead Reckoning:**` — the four required fields, listed flat, no metaphor, one line each. This is the chapter's required facts-only block and this is the right place for it: the reader who wants the reference and not the argument should be able to stop reading at this box
  - `> 🪢 **Mnemonic:**` — a hook for the four fields in order. *Which API, which kind of thing, which one specifically, and what it should look like.* Four questions, always the same four, always that order
  - `> 🪝 **Snag:**` — `status` is not something you write. Editing it in a manifest does not make it true; the system overwrites it. Readers coming from imperative tooling try this
- **Cross-bearings**: back to Ch 3 §6 (**mandatory — the debt**; the field now has a name); back to Ch 3 §5 (`apply` goes to the API server, which writes etcd — the retrieval anchor); forward to Ch 5 (a Pod's `spec` and its `status.phase`); forward to Ch 6 (`spec.replicas` as the number a loop is watching); forward to Ch 8 (the full `kubectl` surface); forward to Ch 13 (reading `status` before reading logs)
- ⚠ **Scope boundary with Ch 5 — narrow but real.** The Deployment example is the documentation's own and should be kept, but Deployment is Chapter 6's resource and Pod is Chapter 5's. Use the example for its *structure* (a number in spec, a reality in status, a correction) without teaching what a Deployment is. One sentence of "you will meet this properly in Chapter 6" is the right handling
- ⚠ **Do not teach `metadata` exhaustively.** Name, UID, optional namespace — that is what the source gives and what the exam tests at this tier. Labels and annotations also live in `metadata` and must be *named here as living there* with a forward cross-bearing to §5; teaching them here would strand §5 with nothing to introduce and would put selection mechanics in the middle of the anatomy lesson. Finalizers, ownerReferences, resourceVersion, and generation are all out of scope and appear in no cached source

### §3 — 🔵 Where a Name Lives

Scoping, and the origin of cross-cutting theme 2. Namespaces isolate groups of resources within a single cluster; the core property is that **names must be unique within a namespace but not across namespaces** — a namespace is a scope for names. Give the practical guidance the docs actually give, which is more restrained than most prep material: for clusters with a few to tens of users you should not need to create or think about namespaces at all, and you should start using them when you need what they provide. State the constraints: namespaces cannot be nested, and each resource lives in exactly one. Then the two corrections that carry exam weight. **First:** do not use multiple namespaces to separate slightly different resources such as different versions of the same software — use labels for that (forward-bear to §5; this is a deliberate setup). **Second, and this is the section's Fixed Point:** namespace scoping applies only to namespaced objects. Nodes, PersistentVolumes, and StorageClasses are not in any namespace, and namespace objects are not themselves namespaced. Name `kubectl api-resources --namespaced=true|false` as the way to settle the question for any resource, which converts a memorization problem into a lookup. Cover the four initial namespaces with what each is *for* — `default` (so you can start without creating one), `kube-system` (objects created by the system), `kube-public` (readable by all clients including unauthenticated ones, by convention rather than requirement), `kube-node-lease` (Lease objects for node heartbeats). Note the production advice to avoid `default`. Close with the DNS form as a *plant only*.

- **Objectives**: D1.1
- **Concepts introduced**: `namespace`, `scope-for-names`, `initial-namespaces`, `default-namespace`, `kube-system`, `kube-public`, `kube-node-lease`, `namespaced-resource`, `cluster-scoped-resource`, `namespace-not-nested`, `namespace-dns-form`, `kubectl-api-resources`
- **Sources**: `k8s-docs-namespaces-2026-08-23.md` — the entire snapshot, which is complete for this section (isolation, uniqueness-within-not-across, the when-to-use guidance, no nesting, one namespace per resource, the labels-not-namespaces-for-versions warning, all four initial namespaces with their purposes, the DNS form and FQDN requirement, the not-all-objects-are-namespaced passage with Nodes and PersistentVolumes named, and the `api-resources` flag)
- **Figure**: **`ch04-fig04-namespaced-vs-cluster-scoped`** — required, and load-bearing eight chapters out
- **Checkpoint after**: no. §3 and §4 are one cognitive arc (scoping and the objects that live inside it) and splitting them costs an alternating-attention switch for no gain — Bearings #2 covers both
- **Markers planned**:
  - `★ **Fixed Point:**` — **not everything lives in a namespace.** Nodes, PersistentVolumes, StorageClasses, and namespaces themselves are cluster-scoped. Phrase it so Chapter 12 can quote it while deriving the RBAC matrix — that is the specific downstream use and it should read as though written for it
  - `> 🪝 **Snag:**` — namespaces cannot be nested. Readers arriving from cloud IAM hierarchies or Linux cgroup trees assume they can
  - `> ⚓ **Worth Securing:**` — `kubectl api-resources --namespaced=false` answers the question for any resource, including ones invented after this book was printed. A lookup beats a memorized list, and the exam's list is short enough that you will remember it anyway once you have run the command twice
- **Cross-bearings**: forward to §5 (**mandatory** — the labels-not-namespaces correction lands its second half there); forward to Ch 8 (ResourceQuota as the mechanism that divides resources between namespaces — named here, taught there); forward to Ch 9 (the `<service-name>.<namespace>.svc.cluster.local` form, and why a bare service name only resolves locally); forward to Ch 12 (**the RBAC derivation** — say explicitly that this boundary is about to become a permissions boundary)
- ⚠ **Plant the DNS form; do not teach it.** One sentence and a cross-bearing. Chapter 9 owns CoreDNS, Service records, Pod records, and FQDN resolution, and it needs the arrival to feel new
- ⚠ **`kube-public` precision.** The docs say the public aspect is *only a convention, not a requirement*. Prep material routinely states it as a hard property. Keep the hedge — it is exactly the kind of distinction this exam rewards

### §4 — 🔵 Configuration Kept Outside the Image

**Pinned by a published Chapter 2 cross-bearing** — Chapter 2 §4 deferred `imagePullSecrets` to "Ch 4 §4 — Secrets, and the `dockerconfigjson` type", so this section must deliver both, by name, and the `dockerconfigjson` type in particular must be visible rather than buried in a table.

Open with the problem, not the object: the same image should run in development and in production, and the thing that differs is configuration, so configuration must live somewhere other than the image. That is what a **ConfigMap** is for — an API object storing **non-confidential** data in key-value pairs, which decouples environment-specific configuration from the image and makes the application portable. Then the four facts that carry weight: the 1 MiB ceiling (with the docs' own guidance to use a volume, database, or file service beyond it); the four consumption paths (container command and args, environment variables, a file in a read-only volume, or code inside the Pod reading the Kubernetes API); the crucial asymmetry among them — **for the first three the kubelet uses the data when it launches the containers, and only the fourth lets an application subscribe to updates**; and immutability (available since v1.19, irreversible once set, delete-and-recreate only). Also: the Pod and the ConfigMap must be in the same namespace, which is §3 paying rent one section later.

Then **Secret**, taught as a contrast rather than a fresh start: an object holding a small amount of sensitive data — a password, a token, a key — that would otherwise end up in a Pod specification or an image. *Similar to ConfigMaps but specifically intended to hold confidential data.* Then the section's Fixed Point, and it needs to be exact rather than dramatic: Secrets are **by default stored unencrypted in the API server's underlying data store**; anyone with API access can retrieve or modify one, so can anyone with etcd access, and **anyone authorized to create a Pod in a namespace can use that access to read any Secret in that namespace — including indirectly, by creating a Deployment**. Give the four hardening steps the docs give (enable encryption at rest; least-privilege RBAC on Secrets; restrict access to specific containers; consider an external Secret store) and hand every one of them to Chapter 12. Cover the built-in types as a table, with `Opaque` marked as the default, `kubernetes.io/dockerconfigjson` called out as the answer to Chapter 2's deferred question, and `kubernetes.io/service-account-token` named with its v1.22 note and immediately deferred to Chapters 5 and 12.

- **Objectives**: D1.1
- **Concepts introduced**: `configmap`, `configmap-size-limit`, `configmap-consumption-paths`, `immutable-configmap`, `decoupling-configuration`, `secret`, `secret-types`, `opaque-secret`, `dockerconfigjson`, `service-account-token-secret`, `tls-secret`, `secret-storage-default`, `secret-hardening`, `encryption-at-rest`
- **Sources**: `k8s-docs-configmap-2026-08-23.md` (all of it — definition, the no-secrecy caution, the DATABASE_HOST motivation, the 1 MiB note, same-namespace requirement, four consumption paths with the kubelet-at-launch versus subscribe-to-updates split, immutability since v1.19). `k8s-docs-secret-2026-08-23.md` (definition, the full storage caution including the create-a-Pod-reads-any-Secret consequence, the four hardening steps, uses, and the eight built-in types). `twelve-factor-app-2026-08-23.md` for the forward bearing only. ⚠ **The base64 claim is not in the cached set** — see § Open questions #2
- **Figure**: **`ch04-fig05-configmap-secret-contrast`** — required
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2** (covers §3 and §4 together)
- **Markers planned**:
  - `★ **Fixed Point:**` — **neither object encrypts anything.** A ConfigMap provides no secrecy or encryption; a Secret is stored unencrypted by default and adds *handling* — a different object type, different RBAC surface, and a place to attach encryption at rest — not cryptography. The difference is intent and treatment
  - `> ⚠ **Navigational Hazards**` — the whole cluster of misconceptions around this pair. B1 traps #16 through #20 all live here and this is the chapter's densest trap concentration: the secrecy assumption, the propagate-to-a-running-container assumption, the reversible-immutability assumption, the size ceiling, and the cross-namespace assumption. Five traps, one section
  - `> 🪝 **Snag:**` — you changed the ConfigMap and the running application did not notice. Three of the four paths are applied by the kubelet at container launch; only the API-reading path subscribes. This is the one readers hit in practice on day one
  - `> 🔭 **Closer Look:**` — the Pod-creation escalation path (create a Pod in a namespace, read any Secret in it) as the reason RBAC on Pod creation is a Secrets question. Deep enough to mark as optional; it is exactly the thread Chapter 12 picks up
- **Cross-bearings**: back to Ch 2 §4 (**mandatory — the pinned payoff**; `imagePullSecrets` and the `dockerconfigjson` type, closing a loop the reader was explicitly told would close here); back to §3 (same-namespace requirement); forward to Ch 5 (as env sources and volume mounts on a Pod, and ServiceAccount as Pod identity); forward to Ch 11 (**named anchor** — ConfigMap and Secret as volume types); forward to Ch 12 (**the entire hardening list**, encryption at rest, and least-privilege RBAC — say explicitly that this section is defining and Chapter 12 is securing); forward to Ch 15 (**reciprocal pair** — config in the environment as twelve-factor factor III)
- ⚠ **Hard scope boundary with Ch 12, and this section will want to violate it.** The Secret material is genuinely alarming and the temptation to teach the fix here is strong. Do not. §4 states the default behavior and names the four steps; Chapter 12 teaches them, alongside RBAC, Pod Security Standards, and the 4Cs. A reader who gets the full security treatment here arrives at Chapter 12 with nothing new, and Chapter 12 is a 7-point chapter
- ⚠ **Ethical framing — this is the chapter's one Part 14 exposure.** The Secret default *is* a real hazard, and saying so plainly is correct. But no fabricated breach anecdotes, no invented percentages, and no fear-framing beyond what the documentation's own Caution block supports. The source's language is strong enough on its own; quote it and let it do the work

### §5 — 🔵 The Universal Join

Cross-cutting theme 5, and the mechanism the next six chapters run on. **Labels** are key/value pairs attached to objects, intended to specify identifying attributes that are meaningful to users but that **do not directly imply semantics to the core system** — that clause is worth slowing down on, because it is why labels are so widely useful. They can be attached at creation and modified any time; keys must be unique per object. Give the syntax at the depth the exam tests: the optional-prefix/name form, 63 characters for the name segment, the reserved `kubernetes.io/` and `k8s.io/` prefixes, values of 63 characters or fewer and possibly empty. Give the documentation's own example labels (`release`, `environment`, `tier`, `partition`, `track`) — they are how practitioners actually label things and they make the abstract concrete for free.

Then the **label selector**, and give it the emphasis the docs give it: *the core grouping primitive in Kubernetes*. Two supported types. **Equality-based** (`=`, `==`, `!=`). **Set-based** (`in`, `notin`, `exists` and its negation), which is more expressive; multiple requirements are ANDed with commas. Then the bridge to what the reader will meet everywhere: newer resources — Job, Deployment, ReplicaSet, DaemonSet — support set-based requirements through `matchLabels` and `matchExpressions`, and **`matchLabels` is exactly equivalent to a `matchExpressions` entry with operator `In`**. That equivalence is the kind of precise, checkable fact this exam likes.

Close on **annotations**, defined by contrast and defined narrowly: non-identifying metadata, for information you want to attach but never select on. The rule is one sentence — *if you might ever want to find objects by it, it is a label; if you only want to record it, it is an annotation* — and it is the whole distinction. Then return to §3's deferred correction and finish it: this is why the docs tell you to separate versions of the same software with labels rather than namespaces. Namespaces partition names; labels partition *sets*, and sets are what everything in Kubernetes actually operates on.

- **Objectives**: D1.1
- **Concepts introduced**: `label`, `label-selector`, `equality-based-selector`, `set-based-selector`, `matchlabels`, `matchexpressions`, `annotation`, `kubectl-get` (with a selector flag)
- **Sources**: `k8s-docs-labels-selectors-2026-08-23.md` — the whole snapshot (definition and the no-semantics-to-the-core-system clause, motivation with example labels, syntax and character set, both selector types with operators, the ANDed-requirements rule, the newer-resources bridge, and the `matchLabels` ≡ `matchExpressions`+`In` equivalence). `k8s-docs-namespaces-2026-08-23.md` for the labels-not-namespaces callback. ⚠ **Annotations have one clause of cached coverage** — see § Open questions #3
- **Figure**: **`ch04-fig03-labels-selectors-join`** — required
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — **the label selector is the core grouping primitive.** Labels are selectable; annotations are not. Nearly every "which objects does this apply to?" question in Kubernetes is answered by a selector over labels. Write this to be retrieved five times
  - `> ⚠ **Navigational Hazards**` — B1 traps #13 and #15 together: labels versus annotations, and namespaces-versus-labels for versioning. They are the same underlying error — reaching for the wrong partitioning tool — and pairing them in one callout teaches the shape rather than two facts
  - `> ⚓ **Worth Securing:**` — once you internalize that everything is a selector over labels, ReplicaSet, Service, NetworkPolicy, and node affinity stop being four mechanisms and become one mechanism pointed at four things. Frame this as the payoff it is
- **Cross-bearings**: back to §3 (**mandatory** — the deferred correction, now completed); back to §2 (labels live in `metadata`, as promised); forward to Ch 6 (a ReplicaSet's selector is how it knows which Pods are *its* Pods); forward to Ch 7 (node labels and `nodeSelector` — the same primitive pointed at nodes); forward to Ch 9 (**named anchor** — a Service selects its backing Pods, which is why Pod churn is survivable); forward to Ch 10 (**≥4-back floor** — NetworkPolicy selects both its subject and its peers); forward to Ch 12 (**the contrast that matters** — RBAC does *not* use selectors; it names subjects and resources. Say this explicitly, because a reader who has just learned that everything is a selector will assume RBAC is too, and it is not)
- ⚠ **Section-ordering note (answers the obvious objection).** Labels are arguably more fundamental than ConfigMaps and would conventionally precede them. They sit at §5 for a hard reason — Chapter 2's published cross-bearing pins Secrets to §4 — and for a good one: this ordering ends the chapter's teaching on the mechanism the next six chapters consume, rather than on a pair of storage objects. §3's deferred labels-versus-namespaces correction is what stitches the two halves together, so build that handoff deliberately in both directions
- ⚠ **Do not teach field selectors.** They are named once in the objects snapshot as a related concept and nothing more is cached. One passing mention at most; do not confuse them with label selectors on the way past

### §6 — 🟡 A Declaration, Not an Order

The Zenith, and short — the work was done in §1 through §5 and this is where it resolves. The reader has now written five kinds of thing and given none of them an instruction. Put it together: every object in this chapter is a **noun**. `spec` says what should exist; `status` reports what does; the four fields are how you say it; namespaces say where the name lives; labels say which set it belongs to; ConfigMaps and Secrets say what it should be configured with. Not one of them contains a step. Then the documentation's own sentence, which is the chapter's thesis and should be quoted rather than paraphrased: **the Kubernetes control plane continually and actively manages every object's actual state to match the desired state you supplied.** Pay off Chapter 3 explicitly — the loop the reader was shown as an architecture diagram now has an input they know how to write, which is precisely what Chapter 3's Voyage Ahead promised. Then say what this buys, because the reader should leave with a reason and not only a distinction: a system that takes descriptions rather than commands can accept the same description twice with no harm done, can be told what should be true by someone who does not know the current state, and can keep the description in a file that outlives the session that wrote it. Do not name GitOps. Let the reader feel the shape of the argument and meet its name in Chapter 15, where it is the book's primary Zenith.

- **Objectives**: D1.1
- **Concepts introduced**: none new — synthesis only
- **Sources**: `k8s-docs-objects-2026-08-23.md` (the record-of-intent framing and the control-plane-continually-manages sentence), `k8s-docs-controllers-2026-08-23.md` (the loop)
- **Figure**: **`ch04-zenith-declaration-not-order`** — required, and the chapter's only Zenith
- **Checkpoint after**: no. Exam Alert follows
- **Markers planned**:
  - `☀️ **Zenith**` — the synthesis moment, marked
  - `🏆 **Safe Harbor**` — chapter close
- **Cross-bearings**: back to Ch 3 §6 and Ch 3's Voyage Ahead (the promise, now kept — one clause, not a paragraph); back to Ch 1 §5's Soundings answer (the reader who had written Terraform now knows what the resemblance was and where it stops); forward to Ch 6 (a controller enforcing a declaration you wrote); forward to Ch 15 (**the primary Zenith** — the same declaration, kept in a repository)
- ⚠ **Precision constraint — the subtitle is stronger than the truth, and this section must be more careful than its heading.** Kubernetes accepts plenty of imperative instruction. `kubectl delete` deletes. `kubectl scale` scales. `kubectl exec` and `kubectl port-forward` are pure imperatives with no declarative reading at all. The accurate and better claim is narrower: **the objects are declarations, and the imperative commands work by changing declarations** — `kubectl scale` edits a number in a spec and then something else notices. Draft §6 to the narrow claim and let the heading be the heading. This is the same discipline Chapter 3 §7 applied to "nobody is in charge," and the two sections should feel like the same author making the same kind of honest correction
- ⚠ **Do not name GitOps, Argo CD, or Flux.** Chapter 15's Zenith depends on the reader *recognizing* this shape in an unfamiliar place. Naming the destination here converts a recognition into a reminder and costs the book its best beat

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 13 questions total.** B4 allocates 10; this outline raises it to 13 on B4's own instruction that the 10 is *"a contract to exceed, not a target to hit."* Chapter 4 carries four distinct conceptual arcs — the declarative reframe plus object anatomy (§1–§2), scoping (§3), configuration objects (§4), and selection (§5) — and they are different cognitive modes. Anatomy is structural recall; scoping is boundary reasoning; the ConfigMap/Secret block is misconception correction; selection is syntax plus discrimination. Folding them into two checkpoints would put unrelated modes in one block for a needless alternating-attention cost (skill Part 4). Practice Questions stay at 19 and Soundings at 8, so the chapter total moves 37 → 40 against a book carrying 715 questions against a 300 floor.

**Retrieval-practice content: 15%** **[B3]** — drawn from **Chapters 2 and 3 only**. Chapter 1 is excluded from the retrieval schedule entirely and no item may test exam mechanics. Against a combined Bearings-plus-Practice pool of 32, the 15% target is ~5 items, allocated **2 in Bearings and 3 in Practice** (5 of 32 = 15.6%). Each of B3's three named anchors has exactly one section where it belongs, and none is placed arbitrarily:

| **[B3]** named anchor | Placement | Why here |
|---|---|---|
| **The control loop** — what does the controller compare `spec` against? | Bearings #1, item 5 | §2 has just given both field names. This is the first moment in the book where the Chapter 3 answer can be given in Chapter 4's vocabulary, and that translation *is* the retrieval |
| **The apiserver's role in `apply`** | Practice Questions, §1–§2 block | Needs the full round trip (`ch04-fig02`) in place, and it is a better discriminator with distractors than as an open checkpoint item |
| **Image references inside a Pod spec** | Bearings #2, item 4 | §4 has just delivered `dockerconfigjson` and closed Chapter 2's deferred `imagePullSecrets` thread. The retrieval and the payoff are the same beat |

### ☆ Taking Your Bearings #1 — after §2

- **Topic**: the declarative frame and object anatomy
- **Questions**: 5
- **Retrieval from earlier chapters**: 1 of 5 (20% of this checkpoint; contributes to the chapter's 15.6%)
- **Difficulty**: mostly ⚪, with item 5 at 🔵

  1. Given an unfamiliar manifest for a resource type not covered in the book, name the four top-level fields and say what each is doing. **Tests transferability, which is the section's actual claim.**
  2. Which of the two nested fields do you write, and which does the system write? Trap answer available for "both."
  3. A manifest is applied and the object appears, but `status` does not match `spec`. Is this a failure? **Correct answer: not necessarily — it is the normal condition during reconciliation.** This item is doing real work; it is the misconception Chapter 13 depends on the reader not having.
  4. What does `apiVersion` select, and why is it per-object rather than per-file?
  5. **Retrieval from Ch 3 §6 — the control loop.** Chapter 3 said a controller compares desired state against current state. Name both fields, and name the component that stores them. This is the chapter's designated control-loop anchor and it is deliberately the checkpoint's hardest item.

- **Answer-key requirement**: item 3 needs a full why-wrong treatment for the "yes, it's a failure" option, because that misconception is load-bearing for Chapter 13.

### ☆ Taking Your Bearings #2 — after §4

- **Topic**: scoping, and the two configuration objects
- **Questions**: 4
- **Retrieval from earlier chapters**: 1 of 4 (25% of this checkpoint)
- **Difficulty**: 🔵 throughout

  1. Name three resources that are not namespaced, and say what they have in common. Trap answers drawn from B1 trap #14.
  2. Two versions of one application need to run in one cluster. Do you use two namespaces or two label values, and why? **Deliberately unresolved until §5 — the reader should be able to answer from §3's warning alone, and §5 will complete it.**
  3. A ConfigMap is updated. Under which of the four consumption paths does the running application see the change? Trap answers cover all four paths (B1 trap #17).
  4. **Retrieval from Ch 2 §4 — image references.** Chapter 2 named five ways to give a cluster access to a private registry and deferred the most common one. Which Secret type implements it, and what file does it serialize? **This is the pinned Chapter 2 payoff appearing as an assessment item, which is the strongest possible way to close that loop.**

### ☆ Taking Your Bearings #3 — after §5

- **Topic**: labels, selectors, and annotations
- **Questions**: 4
- **Retrieval from earlier chapters**: 0. The chapter's 15% is met by Bearings #1 item 5, Bearings #2 item 4, and three Practice items; loading a third retrieval here would push this checkpoint above its own topic
- **Difficulty**: 🔵, with item 4 at 🟡

  1. Write the equality-based and the set-based form of the same requirement. Tests both syntaxes in one item.
  2. Given a `matchLabels` block, write the equivalent `matchExpressions`. Tests the equivalence directly.
  3. Something needs recording on an object but will never be searched on. Label or annotation, and why?
  4. 🟡 **Interleaved with §3.** A selector matches objects in one namespace but not in another where identically-labelled objects exist. What is happening? **Correct answer: selectors operate within a namespace scope; a namespaced query does not cross the boundary.** This item requires §3 and §5 together and it previews the reasoning Chapter 10 needs for NetworkPolicy.

---

## 6. Exam Alert plan

**High-priority topics** — the six most likely to be tested directly, in descending order of confidence:

1. **The four required manifest fields**, by name, and what each supplies. The most mechanically checkable fact in D1.1.
2. **`spec` versus `status`** — which you set, which the system supplies and updates.
3. **Namespaced versus cluster-scoped**, with Nodes, PersistentVolumes, and StorageClasses as the named cluster-scoped examples, and namespaces themselves as the one people miss.
4. **The four initial namespaces** and what each is for — `kube-node-lease` is the one that gets forgotten, and its purpose (node heartbeat Leases) connects to Chapter 8's node conditions.
5. **Labels versus annotations**: identifying and selectable versus non-identifying and not.
6. **ConfigMap versus Secret**: intent and handling, not encryption.

**Common traps to call out** — all eight are `[source]`-tagged in B1's D1 table, so all may be described as things candidates get wrong. None are `[inferred]`, so **no hedging is required here** — but equally, none may be framed with invented frequency figures (Part 14 guardrail #8):

| B1 # | Trap | Where it is defused |
|---|---|---|
| 13 | Using a namespace to separate two versions of the same software | §3 warning + §5 completion |
| 14 | "Everything lives in a namespace" | §3 Fixed Point |
| 15 | Confusing labels with annotations | §5 Navigational Hazards |
| 16 | "ConfigMaps are for config, Secrets are for *secure* config" | §4 Fixed Point |
| 17 | Assuming a ConfigMap change propagates to a running container | §4 Snag + Bearings #2 item 3 |
| 18 | "Immutable ConfigMaps can be un-marked" | §4 |
| 19 | Missing the 1 MiB ConfigMap ceiling | §4 |
| 20 | Assuming a ConfigMap can be referenced across namespaces | §4, resting on §3 |

Traps 16–20 are five of the chapter's eight and all live in §4. That concentration is the reason §4 carries the chapter's `⚠ Navigational Hazards` block rather than distributing warnings evenly.

---

## 7. Practice Questions plan

**19 questions** (B4 allocation, unchanged). Distribution follows section weight, not section count:

| Block | Questions | Notes |
|---|---|---|
| §1–§2 — declarative frame and anatomy | 5 | Includes **2 retrieval items** |
| §3 — namespaces and scoping | 4 | |
| §4 — ConfigMap and Secret | 5 | The chapter's trap concentration; at least 3 must carry trap answers targeting B1 #16–#20 |
| §5 — labels, selectors, annotations | 5 | Includes both selector syntaxes and the `matchLabels` equivalence |

**Retrieval allocation: 3 of the 19 draw from Chapters 2–3**, allocated *within* this count and not added to it:

- **The apiserver's role in `apply`** (Ch 3 §5) — §1–§2 block. B3 named anchor.
- **The control loop as the consumer of `spec`** (Ch 3 §6) — §1–§2 block, framed differently from Bearings #1 item 5 so it is a second retrieval rather than a repeat: this one asks what happens to the *loop* when you apply a changed manifest.
- **Image immutability** (Ch 2) — §4 block, as the same replace-don't-mutate instinct that produces immutable ConfigMaps. The parallel is real and worth drawing.

**Interleaving strategy.** At least **four** questions must require two sections at once, because single-section questions do not build the discrimination this exam tests:

- ConfigMap + namespace (the same-namespace requirement).
- Selector + namespace scope (the Bearings #3 item 4 pattern, in multiple-choice form with distractors).
- Annotation + controller behavior (why a controller cannot act on an annotation the way it acts on a label).
- `spec`/`status` + labels (given a Deployment-shaped manifest, which field determines *which* Pods are managed, and which determines *how many*).

**Trap-answer requirement** (skill Part 11): every wrong option must target a specific misconception, and the answer key must explain why each is wrong. For the §4 block, wrong options should be drawn directly from B1 traps #16–#20 rather than invented — those are documented misconceptions and they make better distractors than plausible-sounding fabrications.

---

## 8. Required figures

Six anchors, exactly as the arc outline specifies. §1 deliberately carries none; §2 carries two.

**Why §2 carries two.** They are different claims at different altitudes and merging them would produce an over-labelled diagram that violates Part 18.12's ~7-label ceiling. `ch04-fig01` is static anatomy — the shape of one object. `ch04-fig02` is a process over time — what happens to that object after you submit it. A reader needs the first to read the second, which is also the order the section teaches them in.

### `ch04-fig01-object-anatomy-spec-status`

- **Purpose**: the chapter's first Fixed Point, dual-coded. The reader's structural template for every manifest they will ever read.
- **Content**: one object, four labelled top-level fields in order (`apiVersion`, `kind`, `metadata`, `spec`), plus `status` shown attached but visually *outside* the authored region.
- **Design requirement — the authorship boundary is the pedagogy.** The figure must make it visible at a glance that you write four fields and the system writes the fifth. A border, a fill, a divider — the treatment is the illustrator's call, but it must survive grayscale (Part 18.11) and it must be carried in the legend. A figure that renders all five fields identically teaches the exact thing the section is correcting.
- **Label count**: five fields plus one boundary label. Comfortably within budget.

### `ch04-fig02-apply-round-trip`

- **Purpose**: the answer to "what actually happens when you apply a file," and the visual argument for §1's claim.
- **Content**: the path of one declaration — manifest → `kubectl` → kube-apiserver → stored state → a controller observing → action → `status` updated → observable again. A cycle, not a line.
- **Design requirement — must not resemble `ch03-fig04-request-path-through-apiserver`.** Chapter 3's figure is **topological**: which components talk to the API server, and (the pedagogy) which arrows are absent. This one is **temporal**: what happens to one object, in sequence, over time. If the two converge visually the reader will read this as a repeat and skip it — the same failure mode flagged for `ch03-fig03` versus `ch02-fig01`. Flag both pairs for the diagram pipeline to review together.
- **Secondary requirement**: the loop portion should be recognizably the *same shape* as `ch03-fig02-control-loop-desired-vs-current`, which is the book's most reused figure and is explicitly designed for three-altitude reuse. This is that reuse's first instance, and getting it right here is a rehearsal for Chapter 15's Zenith.
- **Label count**: six or fewer. Resist annotating the arrows.

### `ch04-fig03-labels-selectors-join`

- **Purpose**: cross-cutting theme 5, made visible once so it can be retrieved five times.
- **Content**: a set of objects carrying label key/value pairs, and two or three selectors resolving to different overlapping subsets of them. The overlap is the point — a reader who sees that one object can be in several selected sets at once understands labels; a reader who sees a clean partition has learned a taxonomy instead.
- **Design requirement — build it for reuse.** Chapters 6, 9, 10, and 12 all retrieve this mechanism. Record the slot structure in the figure spec so those chapters can re-present the same geometry with a ReplicaSet, a Service, or a NetworkPolicy in the selector position rather than commissioning four new diagrams. Same discipline as `ch03-fig02`.
- **Label count**: keep the object count low — four or five objects with two label keys each reads clearly; eight does not.

### `ch04-fig04-namespaced-vs-cluster-scoped`

- **Purpose**: §3's Fixed Point, and **the most downstream-load-bearing figure in this chapter**. B3 specifies that Chapter 12's RBAC four-way matrix must be *derived* from this boundary rather than memorized as a table; this figure is what makes the derivation possible.
- **Content**: two namespace regions containing namespaced resources (Deployments, Services, Pods, ConfigMaps, Secrets), and a surrounding cluster region containing the cluster-scoped ones (Nodes, PersistentVolumes, StorageClasses) — plus the namespace objects themselves shown in the cluster region, since that is the exception everyone misses.
- **Design requirement — the containment relationship must be unambiguous.** A reader must be able to point at any resource in the figure and say which region it is in without reading the caption. Two namespaces rather than one, so that "names unique within, not across" is visible: the same name appearing in both regions, legitimately.
- **Design requirement — Chapter 12 inherits this geometry.** Record the region structure in the figure spec. Chapter 12's RBAC figure should be this figure with permission scopes overlaid, so the reader recognizes it and derives the matrix instead of memorizing it.
- **Label count**: at the ceiling. Consider labelling resource *categories* rather than every individual resource if the count runs long.

### `ch04-fig05-configmap-secret-contrast`

- **Purpose**: §4's Fixed Point, and specifically the part readers get wrong.
- **Content**: the two objects side by side across the axes that actually differ — intended contents, the four consumption paths, storage treatment, and the RBAC/hardening surface.
- **Design requirement — the figure must not imply a security boundary that does not exist.** This is the whole reason the figure exists. A lock icon on the Secret side would teach B1 trap #16 in visual form and would be worse than no figure at all. The honest visual is that the two objects are structurally near-identical and differ in *how they are treated*, and the figure should make that near-identity uncomfortable rather than resolving it. If a design draft makes the Secret look protected, reject it.
- **Label count**: four comparison axes × two columns. Tabular rather than illustrative is acceptable and probably better here.

### `ch04-zenith-declaration-not-order`

- **Purpose**: the chapter's single dramatic synthesis illustration, per Part 18.10.
- **Content**: the filed declaration as the standing reference — a document lodged at a station, referred to repeatedly by many hands over time, none of them receiving instruction and all of them checking against it. The visual argument is a record that outlasts and outranks the moment it was written.
- **Design requirement**: must not read as *bureaucratic*. The register is authority and permanence — a chart annotated and consulted — not paperwork and process. A figure that reads as red tape illustrates the opposite of the chapter's argument.
- **Design requirement**: no narrator face, per the locked architectural rule. Hands and vantage only.
- **Register note**: Communications Officer role family, junior tier. Per the arc outline this book's era placement is early interstellar; the "declaration filed" imagery should read in that register rather than as pure age-of-sail, and it should sit consistently with Chapters 2 and 3's established treatment. Atmospheric only — the prose voice does not change.

---

## 9. Open questions for the author

1. **BLOCKING for §1 — the object-management taxonomy is unsourced, and B2's gap routing says otherwise.** `chapter-lineup.md` § Gap routing lists **"Ch 4 Objects & configuration — (cached coverage sufficient)."** That judgment predates the section plan and is wrong on one point: nothing in `sources/` covers `kubernetes.io/docs/concepts/overview/working-with-objects/object-management/` — the page that defines imperative commands, imperative object configuration, and declarative object configuration, and that gives the tradeoffs among them. §1 is **pinned by a published Chapter 1 cross-bearing** promising to name the declarative/imperative distinction, so it cannot be quietly narrowed. **Recommendation:** Stage 2 fetches that page. **If the fetch fails**, §1 narrows to the sourced claim — the object is a record of intent worked with through the API, and `kubectl apply` submits a configuration from a file — and the three-technique taxonomy plus the §1 `🔭 Closer Look` are cut. The pinned cross-bearing still resolves, because "declarative versus imperative" is nameable from the objects snapshot alone; only the taxonomy is lost.

2. **BLOCKING for a Fixed Point — the base64 claim is not in the cached set.** B1's glossary states Secrets are "base64-encoded, not encrypted by default" and tags it `[source]`, and trap #16 depends on it. But `k8s-docs-secret-2026-08-23.md` is an abridged capture that supports only the *stronger and more important* half: stored **unencrypted** in etcd, retrievable by anyone with API access, etcd access, or Pod-creation rights in the namespace. **Recommendation:** Stage 2 re-fetches the full Secret page for the `data`-field base64 statement. **If it fails**, §4's Fixed Point drops the base64 clause entirely and rests on the unencrypted-storage claim, which is fully sourced and lands harder anyway. Do not carry the base64 assertion into a draft on B1's glossary alone — a fact about the security properties of a security object is exactly where the source-tag discipline exists to protect us.

3. **Non-blocking — annotations have one clause of cached coverage.** The only cached statement is the labels page's *"Non-identifying information should be recorded using annotations"* plus a passing mention in the objects page's related-concepts list. That is technically enough for the §5 contrast and for trap #15, but it is thin for a topic the arc outline lists in "Covers." **Recommendation:** Stage 2 fetches `working-with-objects/annotations/` opportunistically. If it does not, §5 teaches annotations purely as the contrast to labels and does not attempt the conventional-use examples.

4. **Section numbering is pinned in two places and must not drift.** Chapter 1 line 150 → §1; Chapter 2 line 459 → §4. Both are published. This is the constraint that puts ConfigMaps and Secrets ahead of labels and selectors, which is not the conventional ordering. **I think the constraint produced the better chapter** — see the §5 ordering note — but the author should confirm rather than inherit. Reordering means editing two shipped files.

5. **How hard should §2 lean on the Chapter 3 callback?** Chapter 3 built this up deliberately: it withheld the word `spec` for a whole section, cross-beared forward twice, and promised the payoff in its Voyage Ahead. The temptation is to open §2 with a flourish. **Recommendation: one clause, then move on.** The reader remembers; the callback works better acknowledged than performed. Flagging it because the setup is strong enough to invite over-collection.

6. **ServiceAccount token Secrets — confirm the plant-only boundary.** `kubernetes.io/service-account-token` appears in the Secret types table and cannot be omitted from it. But ServiceAccount-as-Pod-identity is planted in Chapter 5 and fully taught in Chapter 12 (cross-cutting theme 7). §4 should name the type, note the v1.22 shift to short-lived TokenRequest tokens, and stop. **Confirm that one sentence is the right budget** — the alternative, omitting the row, would make the types table wrong.

7. **Per-chapter weight (6%) is authored judgment, not CNCF data** (B1 gap G33, B2 disclosure #1). CNCF publishes four domain weights and no sub-competency weights. The metadata line, the Attention Budget, and the Practice Questions count all inherit this estimate. Front matter carries the disclosure; §1 should not repeat it.

8. **Carried from the arc outline, unresolved and not this chapter's to resolve:** the LFS250 syllabus (G37) is still unfetched. If it lands and materially changes D1's internal weighting, this chapter's 6% and its 19 Practice Questions are among the figures that would need revisiting. The section plan and its ordering are dependency-driven and would not change.
```
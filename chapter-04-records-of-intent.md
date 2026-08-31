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

# Chapter 4: Records of Intent
## *"You don't give Kubernetes orders. You file a declaration."*

**Domain: Kubernetes Fundamentals — Kubernetes Core Concepts | Estimated chapter weight: ~6%**
**Complexity: Mixed | Novelty: Paradigm-shifting | Prerequisites: Chapter 3**

*The published domain weight is Kubernetes Fundamentals at 44% of the exam [source: cncf-kcna-certification-page-2026-08-23]. CNCF does not publish weights for individual competencies inside a domain [source: cncf-kcna-curriculum-pdf-2026-08-23]; the ~6% above is this book's estimate, and the front matter explains how every such estimate was derived.*

---

## Attention Budget

**Total time: ~115 minutes | Recommended: split across two sessions (§1–§3, then §4–§6)**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 You File a Declaration | 12 min | Low | Anytime |
| §2 The Anatomy of a Record | 20 min | Medium | When alert |
| ☆ Taking Your Bearings #1 | 8 min | Medium | After a brief pause |
| §3 Where a Name Lives | 15 min | Medium | When alert |
| §4 Configuration Kept Outside the Image | 25 min | High | Peak attention |
| ☆ Taking Your Bearings #2 | 7 min | Medium | After a brief pause |
| §5 The Universal Join | 20 min | Medium | When alert |
| ☆ Taking Your Bearings #3 | 7 min | Medium | After a brief pause |
| §6 A Declaration, Not an Order | 6 min | Low | Anytime |
| Practice Questions | 28 min | High | Peak attention |

**Attention Cost Key:**
- **Low:** concrete, familiar concepts. Study anytime.
- **Medium:** new concepts requiring focus. Study when alert.
- **High:** abstract or dense material, or a misconception that needs dismantling. Study at peak attention.

*If you only have 15 minutes: read §2 and take Bearings #1. The two field names in that section are the vocabulary every remaining chapter of this book assumes you have.*

---

> *"It shouldn't matter how you get from A to C."*
> — Kubernetes documentation, *Overview* [source: k8s-docs-overview-2026-08-23]

---

## 🧭 Soundings

Eight questions before you begin. Your score picks the reading strategy and nothing else; no result here is a bad one. Nothing below requires material from this chapter. It is all either general IT knowledge or something Chapters 2 and 3 already gave you.

1. Some tools ask you to describe what your infrastructure *should* look like; others ask you to write a script that performs the steps to build it. What is that distinction usually called, and what does the first approach buy you that the second doesn't?

2. Many configuration file formats put a version or schema identifier at the very top of the file. What problem is that field solving?

3. A control loop has two states in it, and a third thing that closes the gap between them. Name all three.

4. You submit a description of something you want to exist in a Kubernetes cluster. Which component receives that submission, and what actually stores it?

5. The same container image runs in development and in production, and needs a different database address in each. Where does the difference come from?

6. Is base64 encoding a form of encryption? If not, what is it for?

7. In a system you already know well — SQL, cloud resource tags, a ticketing system, a mail client — how do you ask for "all the things that have this attribute"?

8. Two teams share one system, and both want to call something `database`. What would you expect a well-designed multi-tenant system to offer them?

<details>
<summary>Answers + reading strategy</summary>

1. **Declarative versus imperative.** Declarative buys you idempotency (applying the same description twice is harmless), the ability to state an outcome without knowing the current state, and a description that outlives the session that produced it.

2. **Schema evolution.** The version field lets the consumer know which set of rules to parse the document under, so old documents keep working when the format changes.

3. **Desired state, current state, and the controller** (or loop, or reconciler) that observes the difference and acts to close it.

4. **The kube-apiserver receives it; etcd stores it.** Every write to cluster state goes through the API server, and etcd is the backing store.

5. **From outside the image:** an environment variable, or a file placed into the container when it launches. If the difference lived *inside* the image you'd need two images, which defeats the point of having one.

6. **No.** Base64 is a transport encoding: a way to represent arbitrary binary data using a restricted set of text characters. It is trivially reversible by anyone, requires no key, and provides no confidentiality whatsoever. Hold onto that answer; §4 will want it.

7. **A query with a predicate over an attribute:** `WHERE environment = 'production'`, a tag filter, a saved search. The general shape is that things carry attributes, and you name a subset by describing the attributes rather than listing the members.

8. **A scope for names:** a namespace, a tenant, a project, a schema. Something that makes "database" mean different things in different contexts without either team having to rename anything.

**If you got 6+ right:** skim this chapter. Focus on the ★ Fixed Points and the ⚠ Navigational Hazards callouts, and take all three Taking Your Bearings checkpoints at full effort. You have the priors; this chapter is giving them Kubernetes-specific names and one genuinely counterintuitive detail in §4.

**If you got 3–5 right:** read at normal pace. The material is well within reach and this chapter is calibrated for you.

**If you got 0–2 right:** read carefully, and take the sections in order: §2 depends on §1, and §5 depends on §3. **If questions 3 and 4 were among your misses, re-read Chapter 3 §5–§6 before you start §2.** Those two are the load-bearing prerequisites for this entire chapter, and §2 in particular assumes them.

</details>

---

## Why This Chapter Matters

Here is something unusual about the chapter you are starting: **nothing in it is a verb.**

You have spent three chapters learning about a system that runs software. You will spend this one writing files that describe what *should be true*, then handing them to something that never receives an instruction. You will not, anywhere in the pages ahead, tell Kubernetes to do anything. You will state what you want to exist. Something else does the doing, and you never address it directly. If you arrived from imperative operations tooling, from a world of scripts and runbooks and commands that execute and finish, this is genuinely strange for about a chapter. Better to name the strangeness than smooth it over, so we name it now, live with it through §2 to §5, and resolve it in §6.

Chapter 3 gave you a system to look at. Chapter 4 gives you something to write, and that is the moment the control loop stops being a diagram on a page. It is also, in practical terms, the moment you become able to read Kubernetes configuration you have never seen before. Hand someone who has finished this chapter a manifest for a resource type they have never heard of, one that did not exist when this book was printed, and they can still parse it, because the four top-level fields are the same four fields every single time. That transferability is the honest reason this material matters more than its estimated six points suggest.

The stakes here are structural, and they only need saying once. Every chapter after this one reads *through* this one. Chapter 5's Pod is an object with a spec. Chapter 6's controllers select their workloads by label. Chapter 9's Service selects its backends by label. Chapter 12's role-based access control is, underneath the terminology, a namespaced-versus-cluster-scoped problem wearing a costume. A reader who leaves this chapter able to recite the four required fields but unable to explain what `status` is *for* will re-learn this chapter four more times, in worse conditions, under exam pressure. So take §2 slowly. It is the cheapest hour in the book.

> **Dead Reckoning:** A Kubernetes object is a persistent record stored by the cluster that describes something you want to exist. You write it as a file, usually YAML, with four top-level fields, and submit it with `kubectl apply -f`. The cluster stores it and then works continuously to make reality match it. This chapter covers the shape of that record, where its name lives, how you group records into sets, and two specific record types that hold configuration.

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Read** any Kubernetes manifest you have never seen before, name its four required fields, and say what each one is doing.
- **Distinguish** `spec` from `status` (who writes each, which one you set, which one the system maintains) and connect both to the control loop you already know.
- **Name** the three techniques `kubectl` offers for managing an object, and say why an object should be managed with only one of them.
- **Predict** whether a given resource is namespaced or cluster-scoped, and explain why that answer determines who can be given permission over it.
- **Select** a set of objects by label using both equality-based and set-based syntax, and explain why an annotation cannot be selected on.
- **Choose** between a ConfigMap and a Secret for a piece of configuration, and state precisely what protection the Secret does and does not add.

*You'll also stop reading YAML as an opaque wall of configuration and start reading it as four fields, one of which is the interesting one.*

---

## §1 — ⚪ You File a Declaration

Start where the documentation starts.

Kubernetes objects are **persistent entities** in the Kubernetes system, and the cluster uses them to represent its own state. Specifically, they describe three things: what containerized applications are running and on which nodes; the resources available to those applications; and the policies around how those applications behave, meaning restart policies, upgrades, and fault-tolerance [source: k8s-docs-objects-2026-08-23].

Then the phrase this chapter is named for:

> A Kubernetes object is a **"record of intent"** — once you create the object, the Kubernetes system will constantly work to ensure that the object exists [source: k8s-docs-objects-2026-08-23].

Read that second clause again, because the whole chapter follows from it. *Constantly.* Not once. Creating an object is not a request that gets serviced and then completed. It is a statement that gets **maintained**. When you create an object, you are effectively telling the Kubernetes system what you want your cluster's workload to look like, and that is your cluster's desired state [source: k8s-docs-objects-2026-08-23].

The mechanics, at the coarsest altitude: to work with Kubernetes objects, whether to create, modify, or delete them, you use the Kubernetes API. When you use the `kubectl` command-line interface, the CLI makes the necessary API calls for you [source: k8s-docs-objects-2026-08-23]. That is the tool you will use for the rest of this book, and notice where it sits: not beside the cluster, but in front of the one door Chapter 3 showed you *[cross-bearing: see Ch 3 §5 — the API server as the only way in]*. Your file does not reach the cluster. It reaches the API server, which reaches the cluster.

Which brings us to the distinction Chapter 1 promised this section would name *[cross-bearing: see Ch 1 🧭 Soundings A5 — the distinction this section names]*.

An **imperative** interface is one where you instruct the server what to do. A **declarative** interface is one where you declare the desired state of your resource, and a controller keeps the current state of objects in sync with your declared desired state [source: k8s-docs-custom-resources-2026-08-23]. Kubernetes' object model is the second kind. The documentation is blunt about how far this goes:

> Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration. The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C. In contrast, Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the provided desired state. It shouldn't matter how you get from A to C [source: k8s-docs-overview-2026-08-23].

### Three ways to manage an object

That distinction is not just philosophical. It shows up as three concrete techniques, and the documentation names all three [source: k8s-docs-object-management-2026-08-24]:

| Management technique | Operates on | Recommended environment | Supported writers |
|---|---|---|---|
| **Imperative commands** | Live objects | Development projects | 1+ |
| **Imperative object configuration** | Individual files | Production projects | 1 |
| **Declarative object configuration** | Directories of files | Production projects | 1+ |

**Imperative commands.** A user operates directly on live objects in a cluster, providing operations to `kubectl` as arguments or flags. `kubectl create deployment nginx --image nginx` runs an instance of the nginx container by creating a Deployment object [source: k8s-docs-object-management-2026-08-24]. Notice that the documentation is not sniffy about this. It calls imperative commands *the recommended way to get started or to run a one-off task in a cluster*, and it names the cost precisely: because the technique operates directly on live objects, **it provides no history of previous configurations** [source: k8s-docs-object-management-2026-08-24].

**Imperative object configuration.** The command specifies the operation (`create`, `replace`, and so on), optional flags, and at least one file name. The file must contain a full definition of the object in YAML or JSON [source: k8s-docs-object-management-2026-08-24]. You said what to do *and* handed over the document.

**Declarative object configuration.** The user operates on configuration files stored locally, but **does not define the operations to be taken on them.** Create, update, and delete operations are automatically detected per-object by `kubectl` [source: k8s-docs-object-management-2026-08-24]. This is the technique that gives you `kubectl apply -f configs/` over a whole directory, and it is the one the rest of this chapter assumes.

And one warning, stated by the documentation in its own alarmed voice:

> A Kubernetes object should be managed using only one technique. Mixing and matching techniques for the same object results in undefined behavior [source: k8s-docs-object-management-2026-08-24].

The verb you will use to submit a record is `kubectl apply`, which applies a configuration change to a resource from a file or standard input [source: k8s-docs-kubectl-overview-2026-08-23]. That sentence is the entire treatment `apply` gets in this chapter. You cannot teach a record of intent without showing how a record gets filed, so `apply` appears here; the full command surface, its verbs, its flags, how it authenticates, belongs to Chapter 8 *[cross-bearing: see Ch 8 — kubectl, in full]*.

> 🔭 **Closer Look:** The three techniques differ in one thing that matters more than syntax: **where the record of what you wanted lives.** With an imperative command it lives only in the cluster, which is why the documentation says the technique gives you no history. With object configuration it lives in a file, which can go into source control, be reviewed before it is pushed, and serve as a template for the next object [source: k8s-docs-object-management-2026-08-24]. The trade-off is stated just as plainly in the other direction: object configuration requires a basic understanding of the object schema and the additional step of writing a YAML file. Nothing here is free, and the documentation does not pretend otherwise.

One precision note before we go on, because the chapter subtitle is a slogan and slogans overclaim. Kubernetes accepts plenty of imperative instruction. `kubectl delete` deletes. `kubectl scale` updates the size of a workload. `kubectl exec` executes a command inside a running container and has no declarative reading at all [source: k8s-docs-kubectl-overview-2026-08-23]. The accurate claim is narrower and more interesting than the slogan: **the objects are declarations, and the imperative commands work by changing declarations.** We will make that precise in §6. For now, hold the narrow version.

> **Extended Analogy:** Think about the papers a vessel files before departure.
>
> A declaration lodged with the harbormaster is not an instruction to anyone. It does not tell the pilot to steer, the loading crew to load, or the watch officer to stand a watch. It is a statement of fact and intent: this is what is aboard, this is how deep she sits, this is where we are bound, these are the hazards we carry. It gets signed once and then it sits there.
>
> But everything that happens afterward is checked against it. The pilot consults it before boarding. The loading officer consults it while loading, and again when the manifest is queried three days later. The port authority consults it during an inspection nobody scheduled. If what's in the hold stops matching what's on the paper, the paper does not change. The hold does. And critically, none of those people received an order from you. They read a record, compared it to what they observed, and acted on the difference.
>
> That is the entire relationship between you and a Kubernetes cluster. You file the papers. Independent parties consult them, indefinitely, and correct reality toward them. The record outranks the moment it was written, and it outlasts the session that produced it.

You now know what an object *is*. §2 tells you what is inside one.

---

## §2 — ⚪ The Anatomy of a Record

Chapter 3 owed you something. This is where it comes due.

That chapter taught the control loop in plain language, *those objects carry a field that represents the desired state*, and deliberately withheld the field's name, closing with a promise that Chapter 4 would supply it *[cross-bearing: see Ch 3 §6 — the field that holds desired state, and its status counterpart]*. Here it is. But first, the shape of the document it lives in.

### The four fields

When you create an object in Kubernetes, you must provide the object spec that describes its desired state, plus some basic information about the object, such as a name. Most often you provide that information to `kubectl` in a file known as a **manifest**, and by convention, manifests are YAML [source: k8s-docs-objects-2026-08-23].

In the manifest file for the object you want to create, you set values for four fields [source: k8s-docs-objects-2026-08-23]:

- **`apiVersion`**: which version of the Kubernetes API you're using to create this object
- **`kind`**: what kind of object you want to create
- **`metadata`**: data that helps uniquely identify the object, including a name string, a UID, and an optional namespace
- **`spec`**: what state you desire for the object

Then you apply it: `kubectl apply -f <manifest>` [source: k8s-docs-objects-2026-08-23].

That is the complete structural vocabulary. Not a starting subset that gets extended for advanced resources. The complete thing. A Pod manifest has those four fields — a Pod, for now, being the unit Kubernetes schedules and runs; it is Chapter 5's whole subject. A NetworkPolicy manifest has those four fields. A custom resource for a database operator that some vendor shipped last week has those four fields. This is why the transferability claim from *Why This Chapter Matters* is not marketing: the structure does not vary by resource type, and it does not expire. *[cross-bearing: see Ch 6 — custom resources and operators]*

> **Dead Reckoning:** Four top-level fields to know — required on almost every object; the documentation's own hedge is *"for objects that have a `spec`"* [source: k8s-docs-objects-2026-08-23].
>
> `apiVersion`: which version of the Kubernetes API you're using to create this object. Selects the schema.
> `kind`: a string naming the resource type. Selects what is being created.
> `metadata`: an object holding identity. `name` (you supply), `uid` (the system supplies), and an optional `namespace`. Selects which specific instance.
> `spec`: an object holding the desired state. Its internal shape is defined by `kind`.
>
> Submit with `kubectl apply -f <file>`. Nothing else is structurally required — though a few configuration-holding types (ConfigMap, Secret) carry their payload in `data` instead of a `spec` [source: k8s-api-ref-secret-v1-2026-08-24]. §4 cashes that asterisk.

> 🪢 **Mnemonic:** The four fields answer four questions, always in the same order. **Which API? Which kind of thing? Which one, specifically? What should it look like?** If you can hold those four questions, you can read any manifest, because reading a manifest is just answering them in order.

### The two halves of identity

`metadata` carries two different kinds of identity, and the difference is worth ten seconds.

A **name** is a client-provided string that refers to an object in a resource URL. Only one object of a given kind can have a given name at a time, but if you delete the object, you can make a new one with the same name [source: k8s-docs-names-and-uids-2026-08-24]. Names are reusable. That is the point of them.

A **UID** is a system-generated string, and it is not reusable at all. Every object created over the whole lifetime of a Kubernetes cluster has a distinct UID, and the documentation states its purpose exactly: it is **intended to distinguish between historical occurrences of similar entities** [source: k8s-docs-names-and-uids-2026-08-24]. That phrase is doing quiet work. It means the cluster can tell the difference between the `web-1` you deleted this morning and the `web-1` you created this afternoon, even though the name is identical. Hold onto it; it comes back on the last page of this chapter.

`metadata` holds more than name and UID. Two of its other residents, **labels** and **annotations**, are load-bearing enough to get their own section, so they are named here and deferred *[cross-bearing: see Ch 4 §5 — labels, selectors, and annotations]*. Everything else that can appear in `metadata` sits above associate tier.

Here is what one object looks like, laid out. Note the boundary running through the middle of it, because that boundary is the second half of this section.

<!-- FIGURE: ch04-fig01-object-anatomy-spec-status -->
```
        ┌──────────────────────────────────────────────────────┐
        │  YOU AUTHOR THIS                                     │
        │                                                      │
        │  apiVersion: ...........  which API version          │
        │  kind: .................  what kind of object        │
        │  metadata:                which one, specifically    │
        │    name: ...                                         │
        │    uid: ...  (system fills)                          │
        │    namespace: ...        (optional)                  │
        │  spec:                    what it should look like   │
        │    ...                                               │
        └──────────────────────────────────────────────────────┘
        ═══════════════ authorship boundary ═══════════════════
        ┌──────────────────────────────────────────────────────┐
        │  THE SYSTEM AUTHORS THIS                             │
        │                                                      │
        │  status:                  what is actually true      │
        │    ...                                               │
        └──────────────────────────────────────────────────────┘
```

*Figure: the anatomy of a Kubernetes object. The line through the middle is not decoration; it is the distinction the rest of this section is about. Four fields above it are yours. The field below it is not.*

### The two fields that matter most

Almost every Kubernetes object includes two nested object fields that govern the object's configuration: the object **spec** and the object **status**. They are not symmetrical, and the asymmetry is the point.

For objects that have a spec, you have to set this when you create the object, providing a description of the characteristics you want the resource to have: its desired state. The status describes the current state of the object, **supplied and updated by the Kubernetes system and its components**. The Kubernetes control plane continually and actively manages every object's actual state to match the desired state you supplied [source: k8s-docs-objects-2026-08-23].

A ship's log carries two kinds of entry, and they are never made by the same hand: what the master intends, and what the watch actually observed. Both live in the same book. Neither one is allowed to be written in the other's column.

The documentation's own worked example is the cleanest illustration available, and you can already read it. A Deployment is an object that can represent an application running on your cluster. When you create the Deployment, you might set its spec to specify that you want three replicas of the application running. The Kubernetes system reads the spec and starts three instances, updating the status to match. If one of those instances fails (*a status change*), the system responds to the difference between spec and status by making a correction: starting a replacement instance [source: k8s-docs-objects-2026-08-23].

That is a control loop, described in field names. Chapter 3 told you a controller compares desired state against current state and acts on the difference [source: k8s-docs-controllers-2026-08-23]. Now the two states have names. Desired state is `spec`; you wrote it. Current state is `status`; the system wrote it. The difference between them is the thing every controller in the cluster exists to close.

*(Deployment is Chapter 6's resource and the instances it manages are Chapter 5's. Take the example for its shape — a number in a spec, a reality in a status, a correction — and meet the resource properly later. [cross-bearing: see Ch 6 — Deployments and ReplicaSets])*

> ★ **Fixed Point:** **`spec` is what you want. `status` is what is. You write `spec`. The system writes `status`. Every controller in the cluster exists to close the distance between them.**

That is the most reused sentence in this book. Chapter 5 reads it against a Pod's phase, Chapter 6 reads it against a replica count, Chapter 13 reads it as the first thing you check when something is wrong. Learn it in that exact shape.

> 🪝 **Snag:** `status` is not something you write. The documentation's word on authorship is plain: `status` is supplied and updated by the system and its components [source: k8s-docs-objects-2026-08-23] — so anything you type into a `status` block is not what the object will report. It is a report, not a request. Practitioners arriving from imperative tooling try this at least once, usually at two in the morning, while trying to make a stuck object look healthy.

### What actually happens when you apply

Put the pieces together. You have a file. You have a verb. You have a component that receives it, a store that keeps it, and a loop that reads it. Here is the round trip.

<!-- FIGURE: ch04-fig02-apply-round-trip -->
```
     manifest.yaml
          │
          │  kubectl apply -f
          ▼
    ┌──────────────┐  writes the record   ┌──────────┐
    │ kube-apiserver├─────────────────────►│   etcd   │
    └──────┬───────┘                       └────┬─────┘
           │                                    │
           │  a controller watches ◄────────────┘
           ▼
    the controller compares  spec  vs  status
           │
           │  they differ → it acts
           ▼
    reality changes ──► status is updated ──┐
           ▲                                │
           └────────────────────────────────┘
                    and it watches again, forever
```

*Figure: one declaration, in sequence, over time. The loop at the bottom never terminates. That is not a diagram convention; it is the actual behavior. Compare this to Chapter 3's request-path figure, which showed which components talk to the API server; this one shows what happens to a single object after they do.*

Nothing in that path is a command. You submitted a description; the API server stored it; a controller noticed it; the controller acted; the result was reported back into the same object you wrote. The object is the medium and the message both.

> 🔭 **Closer Look:** Notice where the controller gets its information. It does not receive a message from you, and it does not receive one from `kubectl`. It watches the API server. This is why the same declaration can be applied by a person at a terminal, a CI pipeline, or a tool that reconciles from a Git repository, and the cluster behaves identically in all three cases. The cluster cannot tell the difference and does not care. That indifference is a design choice with consequences we will pick up much later *[cross-bearing: see Ch 15 — the same declaration, kept in a repository]*.

One more command earns a mention here, because it converts a memorization problem into a lookup one: `kubectl explain` gets documentation for resources [source: k8s-docs-kubectl-overview-2026-08-23]. The four top-level fields you now know are the map. `kubectl explain` is how you read the territory inside `spec` for any resource type you have not memorized, which at associate tier is most of them, and that is fine.

---

## ☆ Taking Your Bearings #1: The Declarative Frame and Object Anatomy

Five questions. The last one is the hardest on purpose.

**1.** ⚪ You are handed a manifest for a resource type this book never covers — `kind: CronTab`, from some vendor's operator. Name the four top-level fields you expect to find, and say what each one is doing.

**2.** ⚪ Of the two nested fields that govern an object's configuration, which do you write, and which does the system write?

A) You write `spec`; the system writes `status`
B) You write `status`; the system writes `spec`
C) You write both; the system reads both
D) The system writes both; you read both

**3.** 🔵 You apply a manifest. The object appears. You read it back and `status` does not match `spec`. Is this a failure?

A) Yes — a mismatch means the apply was rejected
B) Yes — `status` is the authoritative record, so a mismatch means your manifest was invalid
C) Not necessarily — a gap between `spec` and `status` is the normal condition while the system reconciles
D) Not necessarily — but only for objects that have no controller watching them

**4.** ⚪ What does `apiVersion` select, and why does it live on each object rather than once per file?

**5.** 🔵 **[retrieval: ch3]** Chapter 3 said a controller compares desired state against current state and acts on the difference. Name both fields those states live in, and name the component that stores the object containing them.

---

**Answers with Explanations**

**1.** `apiVersion` (which version of the API this object belongs to; selects the schema), `kind` (what kind of object, here `CronTab`), `metadata` (identity: a name, a UID, an optional namespace), and `spec` (the desired state, whose internal shape is defined by `kind`) [source: k8s-docs-objects-2026-08-23]. You will not know what belongs inside `spec` for an unfamiliar resource; that is what `kubectl explain` is for. You will always know the four fields wrapping it. That is the whole claim of this section.

**2. Answer: A.**
- **B is wrong** and it is the diagnostic miss: it means the direction of authorship hasn't landed yet. Re-read the Fixed Point.
- **C is wrong** because `status` is not yours to write — it is supplied and updated by the system [source: k8s-docs-objects-2026-08-23]; what you typed is not what the object will report.
- **D is wrong** because `spec` is precisely the field you must set when you create the object [source: k8s-docs-objects-2026-08-23].

**3. Answer: C.**
- **A is wrong** because rejection happens at submission. A rejected apply produces an error and no object. An object that exists was accepted.
- **B is wrong** and inverts the authority relationship. `spec` is authoritative for intent; `status` merely reports observation.
- **D is wrong:** the presence of a controller is what *closes* the gap, not what causes it. Objects with no controller watching them are the ones where a gap would persist.
- **C is right** because the control plane "continually and actively manages every object's actual state to match the desired state you supplied" — the continuous gap-closing Chapter 3 named **reconciliation** [source: k8s-docs-objects-2026-08-23]. Continual management implies there are moments when the states differ. That is not breakage; that is the system working. Hold onto this one. Chapter 13 depends on your not having the opposite instinct, because a practitioner who reads every `spec`/`status` gap as a fault will spend a lot of time investigating perfectly healthy clusters *[cross-bearing: see Ch 13 — reading status before reading logs]*.

**4.** `apiVersion` selects which version of the Kubernetes API you are using to create this object [source: k8s-docs-objects-2026-08-23]: effectively, which schema the rest of the document should be parsed under. It is per-object rather than per-file because a single file can contain several objects of different kinds, and different resource types are versioned independently. A Pod and a NetworkPolicy in one file do not share a version, and there is no sensible file-level answer.

**5. [retrieval: ch3]** Desired state lives in `spec`; current state lives in `status`. The object is stored by **etcd**, reached through the **kube-apiserver**. Every read and write of cluster state goes through the API server, and etcd is the backing store for all cluster data [source: k8s-docs-cluster-architecture-2026-08-23]. If you named the fields but not the components, re-read Chapter 3 §5 before continuing; §3 of this chapter assumes it.

---

**Checkpoint: You've Now Mastered**
✓ The four required fields of every Kubernetes manifest
✓ The three techniques for managing an object, and why you pick one and stay with it
✓ Who writes `spec`, who writes `status`, and why that asymmetry exists
✓ The full path a declaration takes from your file to a controller's attention
☐ Where an object's name lives, and what limits its uniqueness (next)
☐ How to name a *set* of objects rather than one

You now have the shape of the record. Two questions follow immediately from it, and this chapter answers both. Where does the name in `metadata` have to be unique? And how do you refer to fifty objects at once without listing fifty names?

---

## §3 — 🔵 Where a Name Lives

In Kubernetes, **namespaces** provide a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces [source: k8s-docs-namespaces-2026-08-23].

That is the whole of the core idea: a namespace is a **scope for names**. Two teams can both have a Service called `database` and neither has to rename anything, because the two names never collide. They sit in different scopes. Two ships on two different registries can carry the same name, and neither registry has to care.

The documentation's guidance on when to use them is more restrained than you might expect, and the restraint is itself testable. Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, **you should not need to create or think about namespaces at all**. Start using them when you need the features they provide [source: k8s-docs-namespaces-2026-08-23]. Namespaces are not a maturity badge; they are a tool with a specific job.

Two structural constraints, both short and both testable. **Namespaces cannot be nested inside one another**, and **each Kubernetes resource can only be in one namespace** [source: k8s-docs-namespaces-2026-08-23].

> 🪝 **Snag:** Namespaces do not nest. If you have arrived from cloud IAM (management groups containing subscriptions containing resource groups) or from Linux control-group trees, the instinct to build a hierarchy is strong and the platform will not accommodate it. There is exactly one level.

### The correction most guides skip

Here is a piece of official guidance that reliably surprises people: it is **not** necessary to use multiple namespaces to separate slightly different resources, such as different versions of the same software. Use labels to distinguish resources within the same namespace [source: k8s-docs-namespaces-2026-08-23].

Sit with that, because it cuts against a very common habit. A namespace-per-version, or namespace-per-environment-flavor, feels tidy. The documentation says that is the wrong tool, and it names the right one. We will finish this thought in §5, once you have the right tool in hand *[cross-bearing: see Ch 4 §5 — why labels, and not namespaces, partition versions]*.

### Not everything lives in a namespace

Now the part that carries real exam weight, and that pays dividends eight chapters from now.

Namespace-based scoping is applicable **only for namespaced objects** (Deployments, Services, and so on) and **not for cluster-wide objects**, such as StorageClasses, Nodes, and PersistentVolumes. Most Kubernetes resources are in some namespace. However, namespace resources are not themselves in a namespace, and low-level resources such as nodes and persistent volumes are not in any namespace [source: k8s-docs-namespaces-2026-08-23]. *[cross-bearing: see Ch 11 — PersistentVolumes and StorageClasses]*

<!-- FIGURE: ch04-fig04-namespaced-vs-cluster-scoped -->
```
 ╔══════════════════════════════════════════════════════════════════╗
 ║  CLUSTER SCOPE                                                   ║
 ║                                                                  ║
 ║   Node        PersistentVolume        StorageClass               ║
 ║   Namespace  (the namespace objects themselves live out here)    ║
 ║                                                                  ║
 ║   ┌────────────────────────────┐  ┌────────────────────────────┐ ║
 ║   │  namespace: team-a         │  │  namespace: team-b         │ ║
 ║   │                            │  │                            │ ║
 ║   │    Deployment "database"   │  │    Deployment "database"   │ ║
 ║   │    Service    "database"   │  │    Service    "database"   │ ║
 ║   │    ConfigMap  "settings"   │  │    ConfigMap  "settings"   │ ║
 ║   │    Secret     "creds"      │  │    Secret     "creds"      │ ║
 ║   └────────────────────────────┘  └────────────────────────────┘ ║
 ╚══════════════════════════════════════════════════════════════════╝
```

*Figure: two namespaces inside one cluster. The identical names in both boxes are legal and unremarkable; that is what "unique within, not across" means. The four resource types in the outer region are not inside either box, and cannot be put inside one.*

> ★ **Fixed Point:** **Not everything lives in a namespace.** Nodes, PersistentVolumes, and StorageClasses are cluster-scoped, and so are namespace objects themselves. Namespace scoping applies only to namespaced objects [source: k8s-docs-namespaces-2026-08-23]. Any question about who may act on a resource has to start by asking which side of this boundary the resource is on.

That last sentence is a bearing taken now and plotted later. Chapter 12 is where the two lines cross: Kubernetes' permission model has two role types and two binding types, and the four combinations are not a table to memorize. They are a direct consequence of this boundary. A permission over a namespaced resource can be granted inside one namespace; a permission over a cluster-scoped resource cannot be, because there is no namespace to grant it in *[cross-bearing: see Ch 12 — deriving Role, ClusterRole, RoleBinding, and ClusterRoleBinding from this boundary]*.

> ⚓ **Worth Securing:** You do not have to memorize which resources are namespaced. `kubectl api-resources --namespaced=true` and `kubectl api-resources --namespaced=false` list them [source: k8s-docs-namespaces-2026-08-23], and the answer is authoritative for *your* cluster, including resource types installed by operators that did not exist when this book was printed. Run it twice and you will remember the short exam-relevant list anyway, which is the pleasant thing about lookups: they teach you while you use them.

### The four initial namespaces

Kubernetes starts with four namespaces, and each exists for a specific reason [source: k8s-docs-namespaces-2026-08-23]:

| Namespace | What it is for |
|---|---|
| `default` | So that you can start using a new cluster without first creating a namespace |
| `kube-system` | The namespace for objects created by the Kubernetes system |
| `kube-public` | Readable by all clients, including those not authenticated. Mostly reserved for cluster usage, for resources that should be visible and readable publicly throughout the whole cluster |
| `kube-node-lease` | Holds the Lease objects associated with each node. Node leases allow the kubelet to send heartbeats so that the control plane can detect node failure |

Two details in that table are the ones examiners like.

**`kube-public` is a convention, not an enforcement.** The documentation is explicit: *the public aspect of this namespace is only a convention, not a requirement* [source: k8s-docs-namespaces-2026-08-23]. It is often repeated as a hard property of the namespace; it is not one. It is not; it is a norm about what people put there, and norms make poor access control.

**`kube-node-lease` is the one people forget**, and it connects forward. Those Lease objects are how the control plane knows a node is still alive; when the heartbeats stop, the node controller marks the node's condition and eventually acts *[cross-bearing: see Ch 8 — node conditions and heartbeats]* [source: k8s-docs-nodes-2026-08-23].

For a production cluster, the documentation suggests not using the `default` namespace: make other namespaces and use those [source: k8s-docs-namespaces-2026-08-23].

Finally, one plant, deliberately shallow. When you create a Service, it gets a corresponding DNS entry of the form `<service-name>.<namespace-name>.svc.cluster.local`. A container using only `<service-name>` resolves to the Service local to its own namespace; reaching across namespaces requires the fully qualified domain name [source: k8s-docs-namespaces-2026-08-23]. That is one sentence's worth of the topic. The mechanism behind it, what serves those records, what else gets one, how resolution actually proceeds, is Chapter 9's *[cross-bearing: see Ch 9 — cluster DNS, Service records, and FQDNs]*.

Namespaces are also the unit by which cluster resources get divided between multiple users, via resource quota [source: k8s-docs-namespaces-2026-08-23]. Named here; taught in Chapter 8 *[cross-bearing: see Ch 8 — ResourceQuota]*.

---

## §4 — 🔵 Configuration Kept Outside the Image

Start with the problem, not the object.

You have one container image. It needs to run in development and in production. Chapter 2 established that a running container is not edited in place: you build a new image and recreate the container [source: k8s-docs-containers-2026-08-23]. So if the two environments need different settings, and the image cannot differ, the settings must live somewhere other than the image. One hull, two ports of call, two sets of papers waiting on the quay. You do not build a second vessel to satisfy the second harbor.

Here is the documentation's own framing of the situation. Imagine you are developing an application you can run on your own computer for development and in the cloud to handle real traffic. You write the code to look in an environment variable named `DATABASE_HOST`. Locally you set that variable to `localhost`. In the cloud you set it to refer to a Service that exposes the database component to your cluster [source: k8s-docs-configmap-2026-08-23]. One image. Two values. The values are not in the image.

That is exactly what a ConfigMap is for.

### ConfigMap

A **ConfigMap** is an API object used to store **non-confidential** data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume. A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable [source: k8s-docs-configmap-2026-08-23].

Four facts about ConfigMaps carry weight.

**The size ceiling.** A ConfigMap is not designed to hold large chunks of data; the data stored in a ConfigMap cannot exceed **1 MiB**. For settings larger than that, the guidance is to mount a volume, or use a separate database or file service [source: k8s-docs-configmap-2026-08-23].

**The namespace requirement.** The Pod and the ConfigMap must be in the same namespace [source: k8s-docs-configmap-2026-08-23]. That is §3's scope-for-names rule showing up one section later in the place you actually trip over it: a Pod naming a ConfigMap is naming it inside its own scope.

**The four consumption paths, and the asymmetry among them.** There are four different ways to use a ConfigMap to configure a container inside a Pod: inside a container command and args; as environment variables for a container; as a file in a read-only volume for the application to read; or by writing code that runs inside the Pod and uses the Kubernetes API to read the ConfigMap. **For the first three methods, the kubelet uses the data from the ConfigMap when it launches the container(s) for a Pod. The fourth method lets the application subscribe to updates whenever the ConfigMap changes** [source: k8s-docs-configmap-2026-08-23].

> 🪝 **Snag:** You edited the ConfigMap. The running application did not notice. In my experience this is the most common day-one surprise with ConfigMaps, and it is not a bug: three of the four consumption paths are applied by the kubelet *at container launch*. Only the fourth, where your code reads the Kubernetes API itself, subscribes to changes [source: k8s-docs-configmap-2026-08-23]. If you want the first three to pick up a change, something has to cause the containers to be launched again.

**Immutability.** Starting from v1.19 you can add an `immutable` field to a ConfigMap definition. Once a ConfigMap is marked as immutable, **it is not possible to revert this change**, nor to mutate the contents of its `data` or `binaryData` fields. You can only delete and recreate the ConfigMap [source: k8s-docs-configmap-2026-08-23]. Notice the shape of that: the same replace-don't-mutate instinct that governs container images, applied to configuration. Notice also that `immutable: true` is a one-way door, and the platform will not ask whether you meant it.

And one caution stated in the documentation with unusual directness, which sets up the rest of this section: **ConfigMap does not provide secrecy or encryption.** If the data you want to store are confidential, use a Secret rather than a ConfigMap, or use additional third-party tools to keep your data private [source: k8s-docs-configmap-2026-08-23].

Which raises the obvious question. What, exactly, does a Secret do about that?

### Secret

A **Secret** is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image; using a Secret means you don't need to include confidential data in your application code. **Secrets are similar to ConfigMaps but are specifically intended to hold confidential data** [source: k8s-docs-secret-2026-08-23].

Read that last clause carefully: *intended to hold*. Intent is doing a great deal of work in that sentence, and the documentation's very next block explains why.

> Kubernetes Secrets are, by default, stored **unencrypted** in the API server's underlying data store (etcd). Anyone with API access can retrieve or modify a Secret, and so can anyone with access to etcd. Additionally, **anyone who is authorized to create a Pod in a namespace can use that access to read any Secret in that namespace** — this includes indirect access such as the ability to create a Deployment [source: k8s-docs-secret-2026-08-23].

### Base64 is not a lock

Soundings question 6 asked whether base64 encoding is a form of encryption, and told you to hold the answer. Collect it now, because a Secret is where the misconception does damage.

A Secret's `data` field holds arbitrary data **encoded using base64**; the serialized form of the secret data is a base64-encoded string [source: k8s-docs-secret-config-file-2026-08-24] [source: k8s-api-ref-secret-v1-2026-08-24]. That is the first thing people notice about a Secret manifest, and it is the first thing people misread. The documentation removes the ambiguity in one sentence:

> Base64 encoding is *not* an encryption method, it provides no additional confidentiality over plain text [source: k8s-docs-secrets-good-practices-2026-08-24].

Both halves of the situation now sit in one place, stated by the project itself: *Secret values are encoded as base64 strings and are stored unencrypted by default, but can be configured to be encrypted at rest* [source: k8s-docs-secrets-good-practices-2026-08-24]. Encoded, not encrypted. Unencrypted by default, not unencryptable.

One practical consequence worth carrying: if you configure a Secret through a manifest with the data base64-encoded, sharing that file or checking it into a source repository means the secret is available to everyone who can read the manifest [source: k8s-docs-secrets-good-practices-2026-08-24]. The encoding does not make the file safe to commit. It only makes the file *look* safe to commit, which is worse.

> ★ **Fixed Point:** **Neither object encrypts anything.** A ConfigMap provides no secrecy or encryption. A Secret's values are base64-*encoded*, which is not encryption and adds no confidentiality over plain text, and are stored *unencrypted* by default, readable by anyone with API access, etcd access, or the ability to create a Pod in the namespace. What a Secret adds is *handling*: a distinct object type, a distinct surface for access-control rules, and a defined place to attach encryption at rest. The difference between the two is intent and treatment, not cryptography [source: k8s-docs-configmap-2026-08-23] [source: k8s-docs-secret-2026-08-23] [source: k8s-docs-secrets-good-practices-2026-08-24].

The documentation follows its caution with four steps to take in order to use Secrets safely: enable Encryption at Rest for Secrets; enable or configure RBAC rules with least-privilege access to Secrets; restrict Secret access to specific containers; and consider using external Secret store providers [source: k8s-docs-secret-2026-08-23].

Every one of those four is Chapter 12's, and this section is going to hand them over without teaching a single one. That restraint is deliberate: the material above is alarming enough that the pull toward "and here's how to fix it" is strong, but Chapter 12 is where encryption at rest, least-privilege access rules, and the broader security posture get the room they need *[cross-bearing: see Ch 12 — hardening Secrets, and the access-control model behind it]*. A Secret is a strongbox stowed in the same hold as everything else. The lock is Chapter 12's; this chapter is only telling you the box did not ship with one fitted.

> 🔭 **Closer Look:** The third item in that caution, *anyone authorized to create a Pod in a namespace can read any Secret in that namespace, including indirectly via a Deployment*, inverts an intuition, and it repays turning over slowly.
>
> You might reasonably assume that "can read Secrets" and "can create workloads" are separate permissions to be granted separately. They are separate permissions, and granting the second effectively grants the first: a Pod you create can mount any Secret in its namespace, and once mounted, its contents are yours to print. There is no way to create a Pod without that being true, because handing Secrets to Pods is what Secrets are for.
>
> The practical consequence is that permission to create Pods in a namespace is, in security terms, a Secrets question, and nothing in the name of the permission says so. This is exactly the thread Chapter 12 picks up.

### Types of Secret

Secrets carry a type, which signals what kind of data they hold and, per the API reference, exists to *facilitate programmatic handling of secret data* [source: k8s-api-ref-secret-v1-2026-08-24]. The built-in types [source: k8s-docs-secret-2026-08-23]:

| Built-in type | Usage |
|---|---|
| `Opaque` | Arbitrary user-defined data — **the default type** |
| `kubernetes.io/service-account-token` | ServiceAccount token (a legacy long-lived credential) |
| `kubernetes.io/dockercfg` | Serialized `~/.dockercfg` file |
| `kubernetes.io/dockerconfigjson` | Serialized `~/.docker/config.json` file |
| `kubernetes.io/basic-auth` | Credentials for basic authentication |
| `kubernetes.io/ssh-auth` | Credentials for SSH authentication |
| `kubernetes.io/tls` | Data for a TLS client or server |
| `bootstrap.kubernetes.io/token` | Bootstrap token data |

Three rows need a sentence each.

**`Opaque` is the default, and "arbitrary user-defined data" is exactly what it means.** A Secret holding your application's API key, with no `type` set, is `Opaque`. The type is a signal to whatever reads the object, not a constraint on what you may store.

**`kubernetes.io/dockerconfigjson` closes a loop Chapter 2 opened.** That chapter listed five ways to give a cluster access to a private registry (configuring nodes to authenticate to the registry, a kubelet credential provider that fetches credentials dynamically, pre-pulled images, specifying `imagePullSecrets` on a Pod, and vendor-specific extensions) and deferred the most common one to this section [source: k8s-docs-images-2026-08-23] *[cross-bearing: see Ch 2 §3 — five ways to reach a private registry]*. Here it is: an `imagePullSecret` is a Secret of type `kubernetes.io/dockerconfigjson`, and what it holds is a serialized `~/.docker/config.json`, the same credential file your local tooling writes, filed as a cluster object [source: k8s-docs-images-2026-08-23] [source: k8s-docs-secret-2026-08-23]. If a Pod is stuck unable to pull an image from a private registry, this is the object that is missing or wrong.

**`kubernetes.io/service-account-token` is named here and then left alone.** It is a legacy long-lived credential; since v1.22 the recommended approach is short-lived, automatically rotating tokens obtained through the TokenRequest API [source: k8s-docs-secret-2026-08-23] [source: k8s-docs-service-accounts-2026-08-23]. The identity model those tokens belong to (what a ServiceAccount *is*, how a Pod gets one, and what it is allowed to do) is Chapter 5's introduction and Chapter 12's full treatment *[cross-bearing: see Ch 5 §6 — a Pod's identity]*.

### Side by side

<!-- FIGURE: ch04-fig05-configmap-secret-contrast -->
```
                        ConfigMap                    Secret
 ─────────────────────────────────────────────────────────────────────────
 Intended contents      non-confidential             small amounts of
                        key-value data               sensitive data
                                                     (password, token, key)

 Consumed by a Pod as   command and args             environment variables
                        environment variables        files in a volume
                        file in a read-only volume   credentials the kubelet
                        read via the Kubernetes API  uses to pull images

 Stored                 unencrypted, in etcd         unencrypted, in etcd
                        (by default)                 (by default)

 What it adds           nothing — the docs state     a distinct object type,
                        plainly that it provides     a distinct access-control
                        no secrecy or encryption     surface, and a defined
                                                     place to attach
                                                     encryption at rest
```

*Figure: the two objects differ in intent and in treatment, not in cryptography. The third row is identical on both sides, and that is the row people get wrong.* [source: k8s-docs-configmap-2026-08-23] [source: k8s-docs-secret-2026-08-23] [source: k8s-docs-volumes-2026-08-23]

> ⚠ **Navigational Hazards**
>
> In my experience, this pair produces more confident wrong answers than anything else in this chapter. Six of them, all in one place:
>
> **"ConfigMaps are for configuration; Secrets are for *secure* configuration."** The first half is fine. The second half is the misconception. A Secret is not encrypted by default and is readable by several categories of principal you may not have thought about [source: k8s-docs-secret-2026-08-23]. It is a *differently handled* object, and the handling is what you must configure.
>
> **"The value is base64, so it's protected."** Base64 is not an encryption method and provides no additional confidentiality over plain text [source: k8s-docs-secrets-good-practices-2026-08-24]. Anyone who can read the object can decode the value in one command.
>
> **"Update the ConfigMap and the running container picks it up."** Only if the application reads the Kubernetes API directly. The other three consumption paths are applied by the kubelet at container launch [source: k8s-docs-configmap-2026-08-23].
>
> **"Immutable can be turned back off."** It cannot. Marking a ConfigMap immutable is irreversible; delete and recreate is the only route back [source: k8s-docs-configmap-2026-08-23].
>
> **"A ConfigMap is a fine place for that file."** Up to 1 MiB of data. Past that, use a volume, a database, or a file service [source: k8s-docs-configmap-2026-08-23].
>
> **"Pods in `team-a` can reference the ConfigMap in `team-b`."** They cannot. The Pod and the ConfigMap must be in the same namespace [source: k8s-docs-configmap-2026-08-23]. That is §3's scope-for-names rule showing up where you actually trip over it.

One forward pointer before we move on. "Store config in the environment" is the third of the twelve factors [source: twelve-factor-app-2026-08-23], a methodology these two objects implement almost exactly. We will name that connection properly when we look at what cloud native application delivery actually assumes about your application *[cross-bearing: see Ch 15 — the twelve factors, and which ones Kubernetes hands you for free]*. Both objects also appear again as volume types, mounted into a Pod's filesystem *[cross-bearing: see Ch 11 — ConfigMap and Secret volumes]* [source: k8s-docs-volumes-2026-08-23].

---

## ☆ Taking Your Bearings #2: Scoping and Configuration Objects

Four questions, covering §3 and §4 together.

**1.** 🔵 Name three Kubernetes resources that are **not** namespaced, and say what they have in common.

A) Deployment, Service, Pod
B) Node, PersistentVolume, StorageClass
C) ConfigMap, Secret, ServiceAccount
D) Node, ConfigMap, Namespace

**2.** 🔵 Two versions of one application need to run in one cluster. Do you separate them with two namespaces, or with two label values — and why?

**3.** 🔵 A ConfigMap is updated. Under which consumption path does the running application see the change?

A) Environment variables — the kubelet refreshes them on change
B) A file in a read-only volume — the file is rewritten and the app re-reads it automatically
C) Container command and args — the container is re-executed with the new values
D) Code inside the Pod that reads the ConfigMap through the Kubernetes API

**4.** 🟡 **[retrieval: ch2]** An `imagePullSecret` is a Secret of type `kubernetes.io/dockerconfigjson`, holding a serialized `~/.docker/config.json`. That is one of the five mechanisms Chapter 2 listed for giving a cluster access to a private image registry. **Name two of the other four**, and say why the Secret is the one this chapter covers.

---

**Answers with Explanations**

**1. Answer: B.** What they have in common is that they are cluster-scoped. They exist outside any namespace and cannot be placed inside one [source: k8s-docs-namespaces-2026-08-23].
- **A is wrong**: all three are namespaced, and they are the documentation's own examples of namespaced objects.
- **C is wrong**: all three are namespaced. ServiceAccounts in particular are explicitly bound to a namespace, with every namespace getting a `default` one on creation [source: k8s-docs-service-accounts-2026-08-23].
- **D is the interesting trap.** Two of the three are correct: Nodes and Namespaces are both cluster-scoped, and Namespace is the one people most often miss, since namespace resources are not themselves in a namespace. But ConfigMap is namespaced, which is exactly why §4's same-namespace rule exists.

**2.** **Two label values, in one namespace.** The documentation is explicit that it is not necessary to use multiple namespaces to separate slightly different resources such as different versions of the same software, and directs you to use labels to distinguish resources within the same namespace [source: k8s-docs-namespaces-2026-08-23]. The *why* is what §5 is about. Hold your answer and check it again in a few pages.

**3. Answer: D.** Only the API-reading path lets the application subscribe to updates whenever the ConfigMap changes [source: k8s-docs-configmap-2026-08-23].
- **A, B, and C are all wrong for the same reason**, which is why they make a good set: for all three of those methods, the kubelet uses the data from the ConfigMap *when it launches the containers* for a Pod. The data is read once, at launch, and then it is simply what the container has.
<!-- RESEARCH GAP (2026-08-24): the hedge below is accurate but uncited — the cached configmap snapshot stops short of the "Mounted ConfigMaps are updated automatically" section. Re-snapshot kubernetes.io/docs/concepts/configuration/configmap/ and tag; do not delete the hedge. -->
- **B is the most seductive** of the three because a volume feels live in a way an environment variable does not, and in some configurations the projected file content does eventually change on disk. The application still has to be written to notice, though, and a container using a ConfigMap as a `subPath` volume mount will not receive updates at all [source: k8s-docs-volumes-2026-08-23] *[cross-bearing: see Ch 11 — ConfigMap and Secret volumes, and the `subPath` exception]*. Treating "it's a volume, so it's live" as a rule will burn you.

**4. [retrieval: ch2]** Any two of: **configuring the nodes themselves to authenticate to the private registry**; **a kubelet credential provider that fetches credentials dynamically**; **pre-pulled images already present on the node**; **vendor-specific or local extensions** [source: k8s-docs-images-2026-08-23]. The Secret path is the one this chapter covers because it is the only one of the five that is itself a Kubernetes object you write, submit, and version. The other four are properties of the node, the kubelet, or the platform. If you could not produce two, re-read Chapter 2 §3; the list is short and it is exam-relevant.

---

**Checkpoint: You've Now Mastered**
✓ Namespaces as a scope for names, and the resources that live outside every scope
✓ The four initial namespaces and what each one is actually for
✓ ConfigMaps and Secrets — what they hold, how they are consumed, and what protection they do not provide
✓ Why base64 in a Secret manifest is an encoding and not a lock
☐ How to name a set of objects by describing them (next, and it is the one you will use most)

---

## §5 — 🔵 The Universal Join

Everything so far has been about one object at a time. This section is about how you talk about many.

**Labels** are key/value pairs that are attached to objects. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but that **do not directly imply semantics to the core system**. They can be used to organize and to select subsets of objects. Labels can be attached to objects at creation time and subsequently added and modified at any time. Each object can have a set of key/value labels defined, and each key must be unique for a given object [source: k8s-docs-labels-selectors-2026-08-23].

Slow down on that middle clause: *do not directly imply semantics to the core system*. Kubernetes does not know what `tier: frontend` means. It has no built-in concept of a frontend. That ignorance is precisely why labels are useful everywhere: because the system attaches no meaning to them, you are free to attach yours, and the system's grouping machinery works identically regardless of what you meant. A label is closer to a signal flag than to a filing category. The flag means whatever your fleet agreed it means; the machinery that reads it only cares that it is flying. Labels let you map your own organizational structures onto system objects in a loosely coupled fashion, without requiring clients to store those mappings [source: k8s-docs-labels-selectors-2026-08-23].

The documentation's own example labels are the ones practitioners actually use, and they make the abstraction concrete for free [source: k8s-docs-labels-selectors-2026-08-23]:

```
release:      stable | canary
environment:  dev | qa | production
tier:         frontend | backend | cache
partition:    customerA | customerB
track:        daily | weekly
```

The syntax, at the depth this exam tests. Valid label keys have two segments: an optional prefix and a name, separated by a slash. The name segment is required and must be **63 characters or less**, beginning and ending with an alphanumeric character, with dashes, underscores, dots, and alphanumerics between. The prefix is optional; if specified it must be a DNS subdomain no longer than 253 characters, followed by a slash. The **`kubernetes.io/` and `k8s.io/` prefixes are reserved** for Kubernetes core components. Valid label values must be 63 characters or less, and can be empty [source: k8s-docs-labels-selectors-2026-08-23].

### The label selector

Via a label selector, a client or user can identify a set of objects. The documentation gives it a title, and the title is the one line to memorize verbatim: **the label selector is the core grouping primitive in Kubernetes** [source: k8s-docs-labels-selectors-2026-08-23].

The API supports two types.

**Equality-based** selectors use `=`, `==`, and `!=`. For example, `environment = production`, or `tier != frontend` [source: k8s-docs-labels-selectors-2026-08-23].

**Set-based** selectors use `in`, `notin`, and `exists` (plus its negation). For example, `environment in (production, qa)`, `tier notin (frontend, backend)`, `partition` (meaning: has the key at all), and `!partition` (meaning: does not have the key). Set-based requirements are **more expressive** than equality-based ones, and multiple requirements are **ANDed** together with commas [source: k8s-docs-labels-selectors-2026-08-23].

<!-- FIGURE: ch04-fig03-labels-selectors-join -->
```
  OBJECTS, each carrying labels

    ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────┐
    │  Pod A    │   │  Pod B    │   │  Pod C    │   │  Pod D    │
    │ tier=fe   │   │ tier=fe   │   │ tier=be   │   │ tier=be   │
    │ env=prod  │   │ env=dev   │   │ env=prod  │   │ env=dev   │
    └───────────┘   └───────────┘   └───────────┘   └───────────┘

  SELECTORS, each resolving to a set

    tier = fe                ──►   { A , B }
    env  = prod              ──►   { A ,     C }
    env in (prod, qa)        ──►   { A ,     C }
    tier = be , env = prod   ──►   {         C }
```

*Figure: sets, not a taxonomy. Pod A belongs to two selected sets at once and Pod D to none of them, and that overlap is the entire reason this mechanism is useful. If the four Pods had partitioned cleanly into four boxes you would be looking at a folder structure, not a selector.*

### The bridge to what you will actually see

Some resource types accept only equality-based selectors. Newer resources (**Job, Deployment, ReplicaSet, and DaemonSet**) support set-based requirements through two structured fields, `matchLabels` and `matchExpressions`. And the relationship between them is exact: **`matchLabels` is a map of `{key, value}` pairs equivalent to a `matchExpressions` entry with operator `In`** [source: k8s-docs-labels-selectors-2026-08-23].

That equivalence is the kind of precise, checkable fact this exam rewards. `matchLabels: {tier: frontend}` and `matchExpressions: [{key: tier, operator: In, values: [frontend]}]` are the same requirement written two ways. `matchLabels` is not a weaker feature; it is shorthand.

> ★ **Fixed Point:** **The label selector is the core grouping primitive in Kubernetes** [source: k8s-docs-labels-selectors-2026-08-23]. Labels are selectable. Annotations are not. Nearly every question in Kubernetes of the form *"which objects does this apply to?"* is answered by a selector over labels.

Write that one down, because you are about to meet it constantly. A ReplicaSet knows which Pods are *its* Pods by selector *[cross-bearing: see Ch 6 — a controller's selector and the Pods it owns]*. A Service identifies the set of Pods behind it by selector, which is what makes Pod churn survivable [source: k8s-docs-service-2026-08-23] *[cross-bearing: see Ch 9 — a Service selects its backends]*. Node scheduling constraints use labels on nodes; the recommended approaches all use label selectors to facilitate the selection [source: k8s-docs-assign-pod-node-2026-08-23] *[cross-bearing: see Ch 7 — node labels and nodeSelector]*. A NetworkPolicy uses a selector to specify what traffic is allowed to and from the Pods that match [source: k8s-docs-network-policies-2026-08-23] *[cross-bearing: see Ch 10 — NetworkPolicy selects both its subject and its peers]*.

> ⚓ **Worth Securing:** Once you internalize that all of those are the same mechanism pointed at different things, four chapters get considerably easier. ReplicaSet, Service, NetworkPolicy, and node affinity are not four mechanisms to learn. They are one mechanism, *describe a set by its attributes*, aimed at four problems. Learn the primitive once and you spend the later chapters learning what each resource *does* with its set, which is the interesting part.

There is one important exception, and it goes in now precisely because you have just been told that everything is a selector. Kubernetes' permission model is not. Role-based access control names its subjects and its resources explicitly — an explicit list, where everything else in this section is a query [source: k8s-docs-rbac-2026-08-23]. A reader who leaves this section assuming otherwise will make a specific, confident, wrong prediction in Chapter 12 *[cross-bearing: see Ch 12 — why RBAC names subjects instead of selecting them]*.

*(Kubernetes also has field selectors — the name is worth recognizing, and recognition is all this chapter needs [source: k8s-docs-objects-2026-08-23]. Different thing, different syntax, not a substitute. Noted so that you recognize the name; nothing here depends on it.)*

### Annotations, by contrast

**Annotations** are the other half of `metadata`'s user-supplied data. The documentation's opening line is the whole definition: you use annotations to attach **arbitrary non-identifying metadata** to objects, and clients such as tools and libraries can retrieve it [source: k8s-docs-annotations-2026-08-24].

The contrast with labels is stated directly, and it is the sentence to keep:

> Labels can be used to select objects and to find collections of objects that satisfy certain conditions. In contrast, annotations are **not used to identify and select objects** [source: k8s-docs-annotations-2026-08-24].

The rule fits in one sentence, and it is the whole distinction:

**If you might ever want to find objects by it, it is a label. If you only want to record it, it is an annotation.**

A build identifier that a deployment tool wants to select on is a label. A build identifier that exists so a human can read it during an incident is an annotation. Same string, different job.

**What people actually put in them.** The documentation's own list is the best answer to "like what?": build, release, or image information such as timestamps, release IDs, git branch, PR numbers, image hashes, and registry addresses; pointers to logging, monitoring, analytics, or audit repositories; client library or tool information used for debugging, such as name, version, and build; lightweight rollout-tool metadata such as config or checkpoints; and phone or pager numbers of the people responsible, or a directory entry pointing at the team's web site [source: k8s-docs-annotations-2026-08-24]. Notice the shape of that list. Every item is something a human or a tool reads *after* it has already found the object. None of them is something you would search on.

**The syntax difference is the sharper version of the rule.** Annotation keys follow exactly the same two-segment rules as label keys, an optional DNS-subdomain prefix and a required name segment of 63 characters or less, and `kubernetes.io/` and `k8s.io/` are reserved for core components in both cases [source: k8s-docs-annotations-2026-08-24]. The *values* are where they part company:

| | Label value | Annotation value |
|---|---|---|
| Character set | Constrained — values capped at 63 characters; not free-form the way annotation values are [source: k8s-docs-annotations-2026-08-24] | **No restrictions** — any string, including special characters, whitespace, and structured data such as JSON or YAML |
| Length | 63 characters or less | No per-value cap; **all annotations on one object must total ≤ 256 KiB** |
| Selectable | Yes | No |

[source: k8s-docs-labels-selectors-2026-08-23] [source: k8s-docs-annotations-2026-08-24]

That table is the distinction restated as engineering. Labels are constrained *because* they are indexed and selected on. Annotations are unconstrained *because* nothing has to search them. For annotations, the keys and the values in the map must be strings — no numbers, booleans, or lists [source: k8s-docs-annotations-2026-08-24]; label values are strings as well, under the tighter syntax above.

> ⚠ **Navigational Hazards**
>
> Two mistakes live here, and they are the same mistake twice.
>
> **Recording something as an annotation and then trying to select on it.** Selectors operate over labels. An annotation cannot be selected on, not because it is a less capable field, but because that is the definition of the two [source: k8s-docs-annotations-2026-08-24]. A controller that needs to find its objects cannot find them by annotation.
>
> **Using a namespace to separate two versions of the same software.** §3 flagged this and deferred the reason. Here it is: namespaces partition *names*. Labels partition *sets*. Nearly everything in Kubernetes operates over sets, every controller and every Service and every policy, so partitioning by namespace when you meant to partition by set leaves the mechanism that would have grouped your objects unable to see across the line you drew. The documentation's advice to use labels for different versions of the same software is not a stylistic preference [source: k8s-docs-namespaces-2026-08-23]; it is the difference between a distinction the system can act on and one it cannot.
>
> Both errors are the same shape: reaching for the wrong partitioning tool. Learn the shape, not the two facts.

---

## ☆ Taking Your Bearings #3: Labels, Selectors, and Annotations

Four questions. The last one requires two sections at once.

**1.** 🔵 Write the equality-based form and the set-based form of the same requirement: *objects whose `environment` label is `production`.*

**2.** 🔵 You are looking at a workload resource with this selector:

```
matchLabels:
  tier: frontend
```

Write the equivalent using `matchExpressions`.

**3.** 🔵 Your deployment tooling needs to attach the originating Git commit hash to every object it creates. In one case, a controller will later need to find all objects from a given commit. In the other, the hash exists purely so a human can read it during an incident. Label or annotation, in each case, and why?

**4.** 🟡 A selector matches several objects in one namespace, but matches nothing in another namespace where identically labeled objects demonstrably exist. What is happening?

A) Labels are cluster-scoped, so the same label key cannot carry different values in two namespaces
B) A namespaced query operates within its namespace scope; it does not cross the boundary [source: k8s-docs-namespaces-2026-08-23]
C) Set-based selectors work across namespaces but equality-based ones do not
D) The objects in the second namespace must be missing the `kubernetes.io/` prefix on their label keys

---

**Answers with Explanations**

**1.** Equality-based: `environment = production` (or `environment == production`). Set-based: `environment in (production)` [source: k8s-docs-labels-selectors-2026-08-23]. They express the same requirement; set-based syntax is simply more expressive in general, since it can also express membership in several values, key existence, and their negations.

**2.**
```
matchExpressions:
  - key: tier
    operator: In
    values: [frontend]
```
`matchLabels` is a map of `{key, value}` pairs equivalent to `matchExpressions` with operator `In` [source: k8s-docs-labels-selectors-2026-08-23]. If you wrote operator `Equals`, that is not one of the set-based operators. The set-based vocabulary is `In`, `NotIn`, `Exists`, and `DoesNotExist`.

**3.** The first case is a **label**: a controller needs to *find* objects by it, which is exactly what labels are for and exactly what a selector operates over. The second is an **annotation**: annotations attach arbitrary non-identifying metadata, and are not used to identify and select objects [source: k8s-docs-annotations-2026-08-24]. Note that the *content* is identical in both cases, the same forty-character hash. What determines the answer is not the data, it is whether anything will ever need to select on it. Build and release information sits on the documentation's own list of things people record in annotations [source: k8s-docs-annotations-2026-08-24], so the default assumption is that a commit hash is *recorded*; it becomes a label only when something has to search on it.

**4. Answer: B.**
- **A is wrong.** Labels are per-object, not cluster-scoped; the same key can carry different values on every object in the cluster, in any namespace.
- **C is wrong.** Both selector types behave identically with respect to namespace scope; the difference between them is expressiveness [source: k8s-docs-labels-selectors-2026-08-23].
- **D is wrong**, and inverts the rule: `kubernetes.io/` and `k8s.io/` prefixes are *reserved for core components*, not required of yours [source: k8s-docs-labels-selectors-2026-08-23].
- **B is right**, and it is the item to carry forward. Selection is a set operation; namespace is a scope. A query issued inside one namespace considers the objects in that namespace. This combination, a selector plus a namespace boundary, is the exact reasoning Chapter 10 needs for network policy, where the question *which Pods does this apply to?* has to be answered on both sides of a namespace line [source: k8s-docs-network-policies-2026-08-23].

---

**Checkpoint: You've Now Mastered**
✓ Labels, their syntax, and why the system's indifference to their meaning is a feature
✓ Both selector syntaxes, and the exact `matchLabels` ≡ `matchExpressions` + `In` equivalence
✓ Annotations, what people actually record in them, and the one-sentence rule that separates them from labels
✓ Why versions of one application belong in one namespace under different labels

---

## §6 — 🟡 A Declaration, Not an Order

Count what you have written in this chapter.

An object, with four fields. A namespace, which scopes a name. A ConfigMap, which holds configuration. A Secret, which holds configuration that is treated differently. A set of labels, and a selector that names a set by describing it.

Not one of them contains a step.

Every object in this chapter is a **noun**. `spec` says what should exist. `status` reports what does. The four fields are how you say it. A namespace says where the name lives. Labels say which sets it belongs to. ConfigMaps and Secrets say what it should be configured with. There is no verb anywhere in the pile: no *then*, no *next*, no *if that failed, retry*. You described a state of affairs and filed it.

And yet things happen. Here is why:

> The Kubernetes control plane continually and actively manages every object's actual state to match the desired state you supplied [source: k8s-docs-objects-2026-08-23].

<!-- FIGURE: ch04-zenith-declaration-not-order -->
```
                    ┌─────────────────────────────┐
                    │    THE FILED DECLARATION    │
                    │    (what should be true)    │
                    └──────────────┬──────────────┘
                                   │
          ┌────────────┬───────────┼───────────┬────────────┐
          │            │           │           │            │
      consulted    consulted   consulted   consulted    consulted
       at 09:00     at 09:04    at 09:04    at 11:20     at 03:17
          │            │           │           │            │
          ▼            ▼           ▼           ▼            ▼
     ( a scheduler )( a controller )( a kubelet )( a controller )( a controller )

     No hand receives an instruction.
     Every hand reads the record, observes the world, and closes the gap.
```

*Figure: the record outranks the moment it was written. Nothing in this figure is a command being passed down a chain; every arrow is a reading.*

### ☀️ Zenith

> ☀️ **Zenith:** The loop Chapter 3 showed you as an architecture diagram now has an input you know how to write. That was the promise at the end of Chapter 3 *[cross-bearing: see Ch 3 §6 — the control loop, and the field it compares against]*, and this is the shape of it: **you do not participate in the loop. You supply its reference.**
>
> The system reads your declaration and observes the world. Wherever they disagree, it acts. It does this at 09:00 and at 03:17 and on the fourteen-thousandth iteration, with exactly the same logic, without you present, without needing to know what you did last time, without a workflow to resume. Your record is not a message that was delivered. It is the standing answer to a question the cluster asks itself continuously.

Go back to the harbormaster's desk from §1. The declaration you lodged is still sitting there, unchanged, in the same hand you wrote it in. Everything that has happened since happened because someone read it and did not like what they saw out the window.

Name what that architecture buys you, because a distinction without a payoff is just trivia.

A system that takes descriptions rather than commands can accept the same description twice with no harm done: the second submission describes the same world as the first, so there is nothing to correct. It can be told what should be true by someone who does not know what is currently true, because working out the difference is the system's job, not the author's. And it can keep that description in a file, which means the description outlives the terminal session that produced it, the person who typed it, and the incident that prompted it. Chapter 3 put it in the documentation's words and it lands harder now: *it shouldn't matter how you get from A to C* [source: k8s-docs-overview-2026-08-23].

Those three properties compose into something, and this book will spend a later chapter on it. Not yet.

### The honest correction

One more time, precisely, because §1 promised it and because slogans deserve auditing.

`kubectl scale` updates the size of a workload [source: k8s-docs-kubectl-overview-2026-08-23], which is to say it edits a number in a `spec`, and then something else notices. The imperative command did not scale anything. It amended a record, and the loop did the rest.

**The objects are declarations, and the imperative commands work by changing declarations.** That is the accurate claim, narrower than the chapter subtitle and better. It is the same discipline Chapter 3 applied to "nobody is in charge": both statements are true in the way that matters and false if you press them literally, and knowing which is which is the difference between understanding a system and reciting a slogan about it.

---

## Exam Alert! 🚨

**High-Priority Topics**

1. **The four required manifest fields:** `apiVersion`, `kind`, `metadata`, `spec`. By name, and what each supplies. The most mechanically checkable fact in this competency.
2. **`spec` versus `status`:** which you set, which the system supplies and updates.
3. **Namespaced versus cluster-scoped**, with Nodes, PersistentVolumes, and StorageClasses as the named cluster-scoped examples, and namespace objects themselves as the one that is easy to overlook.
4. **The four initial namespaces** and what each is for. `kube-node-lease` is the forgotten one, and its purpose (Lease objects for node heartbeats) is the detail worth pinning down. `kube-public`'s public aspect is a *convention*.
5. **Labels versus annotations:** identifying, constrained, and selectable, versus non-identifying, unconstrained, and not.
6. **ConfigMap versus Secret:** a difference of intent and handling, not of encryption. Base64 is an encoding.
7. **What a declaration actually is:** the objects are declarations, and the imperative commands work by changing declarations.

**Common Traps**

| Trap | Correct understanding |
|---|---|
| Using a namespace to separate two versions of the same software | Use labels within one namespace. Namespaces scope names; labels partition sets [source: k8s-docs-namespaces-2026-08-23] |
| "Everything lives in a namespace" | Nodes, PersistentVolumes, StorageClasses, and namespaces themselves do not [source: k8s-docs-namespaces-2026-08-23] |
| "`kube-public` is enforced as publicly readable" | The public aspect is only a convention, not a requirement [source: k8s-docs-namespaces-2026-08-23] |
| Confusing labels with annotations | Labels identify and can be selected on; annotations record and cannot [source: k8s-docs-annotations-2026-08-24] |
| "ConfigMaps hold config; Secrets hold *secure* config" | Secrets are stored unencrypted by default [source: k8s-docs-secret-2026-08-23]. The difference is treatment, not cryptography |
| "The value is base64, so it's protected" | Base64 is not an encryption method and provides no additional confidentiality over plain text [source: k8s-docs-secrets-good-practices-2026-08-24] |
| Assuming a ConfigMap change reaches a running container | Only via the API-reading path. The other three are applied by the kubelet at container launch [source: k8s-docs-configmap-2026-08-23] |
| "An immutable ConfigMap can be un-marked" | It cannot be reverted. Delete and recreate [source: k8s-docs-configmap-2026-08-23] |
| Forgetting the ConfigMap size ceiling | 1 MiB [source: k8s-docs-configmap-2026-08-23] |
| Referencing a ConfigMap across namespaces | The Pod and the ConfigMap must be in the same namespace [source: k8s-docs-configmap-2026-08-23] |

Six of those ten live in §4, which is why that section carries the chapter's densest warning block and its highest attention cost. If you are budgeting revision time, §4 is where it goes.

---

## Practice Questions

Twenty-one questions. Four test material from earlier chapters and are tagged as such. Four require two sections at once, because single-section recall is not what this exam is measuring.

---

**Q1.** ⚪ **[retrieval: ch3]** You run `kubectl apply -f deployment.yaml`. Which component receives the request, and where does the resulting object live?

A) The kube-apiserver receives it and etcd stores it
B) The kubelet receives it and writes the object to disk on the node
C) The kube-scheduler receives it and holds it in its scheduling queue
D) The kube-controller-manager receives it directly and stores it in memory

**Q2.** 🔵 **[retrieval: ch3]** You change one number in a manifest's `spec` and re-apply it. What happens to the control loop as a result?

A) The loop is restarted with the new value as its starting condition
B) Nothing until you also run a command telling the controller to reconcile
C) The controller now observes a difference between `spec` and `status` and acts to close it
D) The previous loop terminates and a new loop is created for the new desired state

**Q3.** 🟡 **[retrieval: ch3]** Chapter 3 used the built-in Job controller as its worked example of the controller pattern. When the Job controller determines that Pods are needed to carry out a task, what does it actually do?

A) It starts the Pods itself, on a node it selects
B) It instructs the kubelet on each chosen node to start the containers
C) It writes the new Pod objects into etcd directly, since it is a control-plane component
D) It tells the API server to create the Pods, and other components in the control plane act on that new information

**Q4.** ⚪ Which of the following is **not** one of the four fields you must set in a manifest?

A) `apiVersion`
B) `kind`
C) `status`
D) `metadata`

**Q5.** 🔵 Which statement about `apiVersion` is correct?

A) It names the version of the Kubernetes cluster the object was created on
B) It names the version of the API being used to create this object, and it appears once per object
C) It names the version of the API being used, and applies to the whole file
D) It is optional for built-in resource types and required only for custom resources

**Q6.** 🟡 `kubectl scale deployment/web --replicas=5` is an imperative command. In the terms this chapter has established, what does it actually do?

A) It instructs the kubelet on each node to start the additional containers
B) It bypasses the object model and operates directly on the running Pods
C) It is rejected, because Kubernetes accepts declarative input only
D) It edits a number in the Deployment's `spec`; a controller then observes the difference and acts

---

**Q7.** ⚪ Which of these is cluster-scoped?

A) PersistentVolume
B) ConfigMap
C) ServiceAccount
D) Deployment

**Q8.** 🔵 Your team wants to run `v2.3` and `v2.4` of the same application side by side in one cluster. What does the Kubernetes documentation direct you to do?

A) Create a namespace per version — this is the documented use of namespaces
B) Create a namespace per version and nest both inside a parent namespace
C) Create one namespace per version, then use a ResourceQuota to link them
D) Keep both in one namespace and distinguish them with labels

**Q9.** 🔵 Which statement about Kubernetes' four initial namespaces is correct?

A) `kube-public` enforces public readability — unauthenticated readability is a property of the namespace itself
B) `kube-system` is where the cluster places objects whose manifests did not specify a namespace
C) `kube-node-lease` holds the Lease objects associated with each node, which let the kubelet send heartbeats so the control plane can detect node failure
D) `default` is the recommended namespace for production workloads, since using it requires no additional configuration

**Q10.** 🔵 Which statement about namespaces is correct?

A) Namespaces can be nested up to three levels deep
B) A resource can belong to multiple namespaces if it is referenced from both
C) Namespaces cannot be nested, and each resource is in exactly one namespace
D) Namespaces cannot be nested, but cluster-scoped resources belong to all of them simultaneously

---

**Q11.** 🔵 What does using a Secret instead of a ConfigMap give you?

A) Encryption of the data at rest, enabled by default
B) Encryption in transit between the API server and the kubelet, which ConfigMaps do not get
C) Automatic redaction, so that no principal with API access can read the contents
D) A distinct object type and access-control surface, with no encryption by default

**Q12.** ⚪ An application reads a setting from an environment variable populated by a ConfigMap. An operator edits the ConfigMap. What does the running application see?

A) The old value — the kubelet used the ConfigMap data when it launched the container
B) The new value immediately
C) The new value after a short kubelet resync interval
D) The new value, but only if the application re-reads the environment variable rather than caching it at startup

**Q13.** 🟡 **[retrieval: ch2]** ConfigMaps gained an immutability property in v1.19. Which statement about it is correct?

A) Immutability makes the ConfigMap behave like a container image layer: already-running containers keep the old contents, and newly launched containers get the new ones
B) Once marked immutable, the change cannot be reverted and the data cannot be mutated — you can only delete and recreate the ConfigMap
C) Immutability can be toggled off if the ConfigMap has no Pods consuming it
D) Immutability applies to the `data` field but the `binaryData` field remains editable

**Q14.** 🔵 You need to make a 4 MB reference data file available to a containerized application. What does the documentation direct you to do?

A) Use a volume, a separate database, or a file service — ConfigMap data cannot exceed 1 MiB
B) Split it across four ConfigMaps and mount all four
C) Store it in a Secret, which has no size limit
D) Store it in a ConfigMap — the 1 MiB figure is a recommendation, not a limit

**Q15.** 🔵 A Pod in namespace `team-a` needs configuration that already exists in a ConfigMap named `settings` in namespace `team-b`. What is your option?

A) Reference it as `team-b/settings` from the Pod's manifest
B) Reference it by its fully qualified name, `settings.team-b.svc.cluster.local`
C) Create a ConfigMap named `settings` in `team-a` — the Pod and the ConfigMap must be in the same namespace
D) Grant the Pod's ServiceAccount read access to `team-b` and reference it normally

**Q16.** 🔵 A Secret is created to hold an application's API key. The manifest sets no `type` field. What type does the Secret carry?

A) `kubernetes.io/basic-auth` — the type is inferred from the key names in `data`
B) `Opaque` — arbitrary user-defined data, which is the default type
C) None — `type` is a required field, so the object is rejected
D) `kubernetes.io/service-account-token` — the default for any Secret not bound to a Pod

---

**Q17.** 🔵 Which of these is a valid **set-based** selector?

A) `environment != production`
B) `environment in (production, qa)`
C) `environment = production, tier != frontend`
D) `environment == production`

**Q18.** 🔵 Given `matchLabels: {app: web}`, which `matchExpressions` entry is exactly equivalent?

A) `{key: app, operator: In, values: [web]}`
B) `{key: app, operator: Equals, values: [web]}`
C) `{key: app, operator: Exists, values: [web]}`
D) `{key: app, operator: In, values: []}`

**Q19.** 🔵 A controller is written to manage every object carrying a particular attribute. The attribute has been recorded as an annotation. What happens?

A) The controller finds them, but more slowly than if a label had been used
B) The controller finds them only if the annotation key uses the `kubernetes.io/` prefix
C) The controller finds them only within its own namespace
D) The controller cannot select them — selectors operate over labels, and annotations are non-identifying by definition

**Q20.** 🟡 Which of the following is a valid **user-defined** label?

A) key `kubernetes.io/tier`, value `frontend`
B) key with a 120-character name segment and no prefix, value `frontend`
C) key `example.com/tier`, value `frontend`
D) key `tier`, value a 200-character description string

**Q21.** 🔵 You are looking at a workload manifest that contains both a `spec.replicas` field and a `spec.selector.matchLabels` block. Which field determines *which* objects the workload manages, and which determines *how many* it maintains?

A) `replicas` determines which; `matchLabels` determines how many
B) `matchLabels` determines which; `replicas` determines how many
C) `matchLabels` determines both — `replicas` is reported in `status` only
D) Neither — both are set by the system and reported in `status`

---

### Answers and Explanations

**Q1. Answer: A.** Every read and write of cluster state goes through the kube-apiserver [source: k8s-docs-control-plane-node-communication-2026-08-24], and etcd is the consistent, highly-available key-value store used as Kubernetes' backing store for all cluster data [source: k8s-docs-cluster-architecture-2026-08-23].
- **B** confuses the kubelet's role: it runs containers on a node from PodSpecs provided to it, and it is not a store of record.
- **C** picks a real control-plane component with the wrong job; the scheduler watches for Pods with no assigned node and selects nodes for them [source: k8s-docs-cluster-architecture-2026-08-23]. It receives nothing from `kubectl`.
- **D** describes the shape of the misconception that controllers are messaged directly. They are not; they watch the API server.

**Q2. Answer: C.** A controller compares desired state against current state and acts on the difference [source: k8s-docs-controllers-2026-08-23]; the difference is what changed, so the change is what it responds to.
- **A** and **D** both imagine the loop as something with a lifecycle tied to your action. It has neither a start you trigger nor an end. It is described as a non-terminating loop that regulates the state of a system [source: k8s-docs-controllers-2026-08-23].
- **B** is the imperative instinct at its purest, and it is the single most useful wrong answer in this chapter. There is no such command, and needing one would defeat the entire architecture. Nobody tells the controller. The controller is already watching.

**Q3. [retrieval: ch3] Answer: D.** The documentation is unusually direct about this: *the Job controller does not run any Pods or containers itself. Instead, the Job controller tells the API server to create or remove Pods. Other components in the control plane act on the new information* [source: k8s-docs-controllers-2026-08-23].
- **A** is the intuitive picture of a controller as a worker. Built-in controllers manage state by interacting with the cluster API server; they are not execution engines.
- **B** invents a controller-to-kubelet channel. Chapter 3's hub-and-spoke pattern rules it out: all API usage from nodes (or the Pods they run) terminates at the API server, and none of the other control-plane components is designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24].
- **C** is the one that survives longest for people who half-remember the architecture. Being a control-plane component does not grant direct access to the store. Ideally only the API server has access to etcd, since access to etcd is equivalent to root permission in the cluster [source: k8s-docs-etcd-access-control-2026-08-24].
- **D** is also the shape of §2 of this chapter: everything, including a controller's own writes, goes through the same door.

**Q4. Answer: C.** The four fields to set are `apiVersion`, `kind`, `metadata`, and `spec` (for objects that have a `spec` — which a Pod is) [source: k8s-docs-objects-2026-08-23]. `status` is supplied and updated by the Kubernetes system and its components; writing it accomplishes nothing.
- **A is a required field:** `apiVersion` names which version of the API you are using to create this object, and so selects the schema the rest of the document is parsed under.
- **B is a required field:** `kind` names the resource type, and it is what determines the internal shape of `spec`.
- **D is a required field:** `metadata` carries identity, the name, the UID, and the optional namespace, which is how the cluster tells this object from every other object of the same kind.

**Q5. Answer: B.** `apiVersion` is which version of the Kubernetes API you're using to create this object [source: k8s-docs-objects-2026-08-23], and it is one of the fields set per object.
- **A** conflates the API version of a resource type with the version of the cluster software. Those move independently; a resource's API version can remain stable across many cluster releases.
- **C** is the file-level assumption, and it fails because a single file can hold several objects of different kinds, each versioned independently.
- **D** is wrong: the four required fields are required for every object, built-in or custom.

**Q6. Answer: D.** `kubectl scale` updates the size of a workload [source: k8s-docs-kubectl-overview-2026-08-23]. It amends a number in the object's `spec`, and the control plane then continually and actively manages the actual state to match the desired state you supplied [source: k8s-docs-objects-2026-08-23]. The command changed a declaration; the loop did the work.
- **A** invents a direct command channel to the kubelet. Nothing in the object model works that way.
- **B** is the plausible-sounding version of the same error, and it is the one to reason your way out of: there is no "acting on running Pods" that skips the objects, because the objects *are* how the cluster knows what should be running.
- **C** is the over-correction this chapter's §1 precision note exists to prevent. Kubernetes accepts imperative commands all day; the documentation names imperative commands the recommended way to get started or to run a one-off task [source: k8s-docs-object-management-2026-08-24]. The claim is not "no imperatives." The claim is "the imperatives work by editing declarations."

**Q7. Answer: A.** Low-level resources such as nodes and persistent volumes are not in any namespace [source: k8s-docs-namespaces-2026-08-23].
- **B** and **D** are among the documentation's own examples of namespaced objects, and ConfigMap in particular is namespaced enough that §4's same-namespace rule exists because of it.
- **C** is namespaced too, and pointedly so. ServiceAccounts are bound to a namespace, and every namespace gets a `default` one on creation [source: k8s-docs-service-accounts-2026-08-23].

**Q8. Answer: D.** It is not necessary to use multiple namespaces to separate slightly different resources, such as different versions of the same software; use labels to distinguish resources within the same namespace [source: k8s-docs-namespaces-2026-08-23].
- **A** is the intuitive habit the documentation specifically corrects.
- **B** additionally fails on nesting: namespaces cannot be nested inside one another [source: k8s-docs-namespaces-2026-08-23].
- **C** misuses ResourceQuota, which divides cluster resources between namespaces rather than linking them.

**Q9. Answer: C.** `kube-node-lease` holds Lease objects associated with each node; node leases allow the kubelet to send heartbeats so that the control plane can detect node failure [source: k8s-docs-namespaces-2026-08-23].
- **A is the trap this item exists for.** The documentation says plainly that *the public aspect of this namespace is only a convention, not a requirement* [source: k8s-docs-namespaces-2026-08-23]. `kube-public` is readable by all clients including unauthenticated ones, but that is a fact about how the cluster is configured and what people put there, not an enforcement the namespace performs.
- **B** invents a fallback behavior. `kube-system` is the namespace for objects created by the Kubernetes system; an object whose manifest omits a namespace lands in whichever namespace the request context supplies — `default` on a fresh kubeconfig, the ServiceAccount's namespace when `kubectl` runs inside the cluster [source: k8s-docs-kubectl-overview-2026-08-23] — and `default` exists precisely so that you can start using a new cluster without first creating one [source: k8s-docs-namespaces-2026-08-23].
- **D** inverts the documentation's advice: for a production cluster, consider *not* using the `default` namespace, make other namespaces and use those [source: k8s-docs-namespaces-2026-08-23].

**Q10. Answer: C.** Namespaces cannot be nested inside one another, and each Kubernetes resource can only be in one namespace [source: k8s-docs-namespaces-2026-08-23].
- **A** and **B** contradict those two rules directly.
- **D** is the subtle one and it is still wrong: cluster-scoped resources do not belong to every namespace. They belong to none. That distinction matters enormously for permissions, because "in all namespaces" and "in no namespace" imply very different things about who can be granted access *[cross-bearing: see Ch 12]*.

**Q11. Answer: D.** Kubernetes Secrets are, by default, stored unencrypted in the API server's underlying data store; anyone with API access can retrieve or modify one, as can anyone with etcd access or the ability to create a Pod in the namespace [source: k8s-docs-secret-2026-08-23]. What the object type gives you is a place to apply the four recommended protections, not the protections themselves.
- **A** is the misconception this chapter exists to correct. Secret values are stored unencrypted by default, though they *can* be configured to be encrypted at rest [source: k8s-docs-secrets-good-practices-2026-08-24], which is a configuration you perform, not a default you inherit.
- **B** is wrong on the premise: API traffic is TLS-protected as a matter of cluster configuration [source: k8s-docs-cloud-native-security-2026-08-23], and that protection is not specific to Secrets.
- **C** contradicts the documented behavior outright. Anyone with API access can retrieve the Secret; base64 encoding of the stored value provides no additional confidentiality over plain text [source: k8s-docs-secrets-good-practices-2026-08-24].

**Q12. Answer: A.** For the environment-variable path, as for command-and-args and read-only volume file paths, the kubelet uses the data from the ConfigMap when it launches the containers for a Pod [source: k8s-docs-configmap-2026-08-23]. Only the API-reading path subscribes to updates.
- **B** and **C** both assume a propagation mechanism that does not exist for this path.
- **D** is the most instructive miss, because half of it is a real belief: applications genuinely do differ in whether they cache configuration at startup. It does not help here. The environment the container was launched with is fixed at launch; re-reading it returns the same value the kubelet supplied. The application's diligence is irrelevant when the source never changes.

**Q13. [retrieval: ch2] Answer: B.** Once a ConfigMap is marked as immutable, it is not possible to revert this change nor to mutate the contents of the `data` or `binaryData` fields; you can only delete and recreate the ConfigMap [source: k8s-docs-configmap-2026-08-23].
- **A is the ch2 discrimination**, and it fails on Chapter 2's own rule. Image layers are immutable, but the way a change reaches a container is *not* by the object quietly serving new contents to new containers. It is by building a new image and recreating the container [source: k8s-docs-containers-2026-08-23]. An immutable ConfigMap works the same way: you delete and recreate, and consumers are relaunched. There is no dual-contents state in either mechanism.
- **C** is the most tempting wrong answer because it sounds like a reasonable safety valve. There is no such escape hatch.
- **D** is wrong: both fields are covered.

**Q14. Answer: A.** The data stored in a ConfigMap cannot exceed 1 MiB; for larger settings, consider mounting a volume or using a separate database or file service [source: k8s-docs-configmap-2026-08-23].
- **B** is a workaround for a limit that exists precisely because ConfigMaps are not designed to hold large chunks of data; it fights the design rather than following the guidance.
- **C** is wrong on its premise: a Secret is described as holding *a small amount* of sensitive data [source: k8s-docs-secret-2026-08-23], and is not the escape hatch for size.
- **D** misreads the limit as advisory.

**Q15. Answer: C.** The Pod and the ConfigMap must be in the same namespace [source: k8s-docs-configmap-2026-08-23]. The configuration has to exist in `team-a`.
- **A** invents a cross-namespace reference syntax that the field does not accept.
- **B** borrows the Service DNS form, which addresses Services over the network [source: k8s-docs-namespaces-2026-08-23]. A ConfigMap is not reached over the network by a Pod's config machinery, and these are two mechanisms that look similar and are not.
- **D** is the closest to plausible and still wrong: permission to read an object is not the same as the ability to reference it as a config source. Access control governs *who may*, not *what the field accepts*.

**Q16. Answer: B.** `Opaque` is arbitrary user-defined data and is the default type [source: k8s-docs-secret-2026-08-23]. The `type` field exists to facilitate programmatic handling of the secret data [source: k8s-api-ref-secret-v1-2026-08-24]: it tells consumers what shape to expect, and `Opaque` is the honest answer of "no particular shape."
- **A** invents inference from key names. Nothing infers a Secret's type; `kubernetes.io/basic-auth` is a type you choose deliberately when you are storing basic-authentication credentials.
- **C** is wrong twice over. `type` IS a real top-level Secret field — just not a required one; it defaults to `Opaque` [source: k8s-docs-secret-2026-08-23]. And a Secret is one of the types that carries `data` rather than a `spec` [source: k8s-api-ref-secret-v1-2026-08-24], so "the four required fields" is the wrong frame for this object entirely.
- **D** confuses a specific legacy type with a default. `kubernetes.io/service-account-token` is a ServiceAccount token, a legacy long-lived credential superseded since v1.22 by short-lived tokens from the TokenRequest API [source: k8s-docs-secret-2026-08-23] [source: k8s-docs-service-accounts-2026-08-23].

**Q17. Answer: B.** Set-based selectors use `in`, `notin`, and `exists` [source: k8s-docs-labels-selectors-2026-08-23].
- **A** and **D** are equality-based: `=`, `==`, and `!=` are the equality-based operators. `!=` in particular reads like a set operation and is not one.
- **C** is the item's best distractor, because the comma makes it *look* set-based. It is two equality-based requirements ANDed together; commas AND multiple requirements regardless of which selector type they use [source: k8s-docs-labels-selectors-2026-08-23]. The comma tells you nothing about the operator; the operators are what you read.

**Q18. Answer: A.** `matchLabels` is a map of `{key, value}` pairs equivalent to `matchExpressions` with operator `In` [source: k8s-docs-labels-selectors-2026-08-23].
- **B** uses an operator that does not exist in this vocabulary; the operators are `In`, `NotIn`, `Exists`, and `DoesNotExist`.
- **C** is a real operator with a different meaning: `Exists` tests for the key regardless of value, so it would also match `app: api`.
- **D** is `In` with an empty value list, which matches nothing.

**Q19. Answer: D.** Annotations attach arbitrary non-identifying metadata, and in contrast to labels are *not used to identify and select objects* [source: k8s-docs-annotations-2026-08-24]; selection is a label operation, and the label selector is the core grouping primitive [source: k8s-docs-labels-selectors-2026-08-23]. The fix is not to work around the selector. It is to record the attribute as a label, because wanting to select on it is what makes it identifying.
- **A** implies a performance difference where there is a capability difference.
- **B** inverts the prefix rule: `kubernetes.io/` and `k8s.io/` are reserved for core components in both labels and annotations, not required of user keys [source: k8s-docs-annotations-2026-08-24].
- **C** describes namespace scoping, which is real but is not what stops the controller here.

**Q20. Answer: C.** A label key may carry an optional prefix that is a DNS subdomain followed by a slash; `example.com/` is exactly that, and `tier` is a valid name segment [source: k8s-docs-labels-selectors-2026-08-23].
- **A is invalid for a user-defined label:** the `kubernetes.io/` and `k8s.io/` prefixes are reserved for Kubernetes core components [source: k8s-docs-labels-selectors-2026-08-23].
- **B is invalid on length:** the name segment must be 63 characters or less [source: k8s-docs-labels-selectors-2026-08-23]. The 253-character allowance applies to the *prefix*, which is a different segment, and mixing the two limits is the specific slip this option targets.
- **D is invalid on the value:** valid label values must be 63 characters or less [source: k8s-docs-labels-selectors-2026-08-23]. A 200-character description belongs in an annotation, whose values carry no character-set restriction and are bounded only by a 256 KiB total per object [source: k8s-docs-annotations-2026-08-24]. That is §5's rule in miniature: if it does not fit in a label value, it was probably never something you wanted to select on.

**Q21. Answer: B.** `matchLabels` is a selector, and the label selector is the core grouping primitive; it answers *which objects* [source: k8s-docs-labels-selectors-2026-08-23]. `replicas` sits in `spec` and states desired state: how many should exist, which is exactly the documentation's own worked example of a Deployment spec specifying three replicas [source: k8s-docs-objects-2026-08-23].
- **A** inverts the two.
- **C** and **D** both misplace authorship: `replicas` is something you set in `spec`, not something reported to you in `status`. `status` reports how many *currently* exist, which is the other half of the pair and the thing the controller compares against.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| Kubernetes object | A persistent entity, a "record of intent." Create it and the system constantly works to ensure it exists [source: k8s-docs-objects-2026-08-23] |
| The four fields | `apiVersion`, `kind`, `metadata`, `spec`. Every object. Every time. Which API, which kind, which one, what it should look like |
| `spec` | What you want. You write it |
| `status` | What is. The system writes it. Every controller exists to close the distance between the two |
| Manifest | The file you write the object in. YAML by convention. Submit with `kubectl apply -f` |
| Three management techniques | Imperative commands (live objects, no history), imperative object configuration (files, you name the operation), declarative object configuration (directories, kubectl detects the operation). Use only one per object [source: k8s-docs-object-management-2026-08-24] |
| Name vs UID | A name is reusable after deletion; a UID is distinct across the cluster's whole lifetime and distinguishes historical occurrences of similar entities [source: k8s-docs-names-and-uids-2026-08-24] |
| Namespace | A scope for names. Unique within, not across. Cannot be nested. One namespace per resource |
| Initial namespaces | `default` (start without creating one), `kube-system` (system objects), `kube-public` (readable by all — by convention, not enforcement), `kube-node-lease` (node heartbeat Leases) |
| Cluster-scoped | Nodes, PersistentVolumes, StorageClasses, and namespace objects themselves. `kubectl api-resources --namespaced=false` settles it |
| ConfigMap | Non-confidential key-value data, ≤1 MiB, same namespace as the Pod. Four consumption paths; only the API-reading one sees updates. Immutability is irreversible |
| Secret | Same shape, different intent and treatment. Values base64-*encoded*; stored *unencrypted* by default. Readable by anyone with API access, etcd access, or Pod-creation rights in the namespace |
| Base64 | An encoding, not an encryption method. No additional confidentiality over plain text [source: k8s-docs-secrets-good-practices-2026-08-24] |
| `Opaque` | The default Secret type: arbitrary user-defined data |
| `dockerconfigjson` | The Secret type behind `imagePullSecrets`, a serialized `~/.docker/config.json` |
| Label | Key/value identifying attribute. Selectable, and constrained (values ≤63 chars). Means nothing to the core system, which is why it works everywhere |
| Label selector | **The core grouping primitive in Kubernetes.** Equality-based (`=`, `==`, `!=`) and set-based (`in`, `notin`, `exists`), ANDed with commas |
| `matchLabels` | Exactly equivalent to `matchExpressions` with operator `In` |
| Annotation | Arbitrary non-identifying metadata. Unconstrained values (≤256 KiB total per object), not selectable. If you might search on it, it's a label |

---

## 🏆 Safe Harbor

**Voyage Progress:** 🗺️ → 🌊 → 🌅 — Chapter 4 of 20 complete. You have crossed from *watching the system* to *writing to it*, which is the largest single step in this book.

You can now read a manifest you have never seen. You know which of its fields you author and which one is a report. You know where its name has to be unique and which resources have no name-scope at all. You know how to describe a set of objects rather than list one. And you know the exact thing a Secret does and does not do, which is a piece of knowledge something plenty of working practitioners, in my experience, have wrong.

---

## The Voyage Ahead

You have written declarations for five kinds of thing. You have not yet written one for the thing that actually runs.

Chapter 5 is about the Pod: the object that represents a set of one or more running containers on your cluster, and the unit that everything else in Kubernetes ultimately arranges [source: k8s-docs-workloads-2026-08-23]. Everything you learned here applies to it unchanged: four fields, a `spec` you write, a `status` you read. But a Pod's `status` has something the objects in this chapter did not: a **phase**, a small vocabulary of words describing where in its short life the Pod currently is. And that vocabulary is the first thing you look at when something is wrong.

There is a second thing to watch for, and §2 already handed you the tool for it. A Pod is described in the documentation as *relatively ephemeral rather than durable*, and it is never rescheduled to a different node. If the node it is on dies, it is not moved; it is replaced by a new, near-identical Pod with **a different UID** [source: k8s-docs-pod-lifecycle-2026-08-23], which is exactly what UIDs are for: distinguishing between historical occurrences of similar entities [source: k8s-docs-names-and-uids-2026-08-24]. Same name, different object, and the cluster knows the difference even when you don't.

Hold that against what you learned in §1. If the thing that runs your application is designed to be replaced rather than repaired, then a declaration that names a specific Pod is a declaration about something disposable, and something else must be holding the intent that survives it.

Chapter 5 introduces the disposable thing. Chapter 6 introduces what holds the intent.

> *"You have stopped issuing orders. Everything after this is learning what reads them."*

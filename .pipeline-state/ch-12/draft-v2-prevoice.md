# Chapter 12: Locks, Keys, and Watchstanders
## *"RBAC has no deny rule, and Secrets aren't encrypted"*

**Domain: Container Orchestration (D2) — 28% of the exam** [source: cncf-kcna-curriculum-pdf-2026-08-23] **| Chapter allocation: ~7% | Complexity: Mixed | Novelty: Moderate**

> **A note on that 7%.** The CNCF publishes weights for the four domains and for nothing below them [source: cncf-kcna-curriculum-pdf-2026-08-23]. There is no published figure for how much of Domain 2 is security, and anyone who gives you one is guessing. The ~7% above is this book's own allocation, derived from the competency list and the shape of the published objectives. It is a planning number for your study time, not a fact about the exam. Treat it the way you would treat any estimate: useful for deciding what to read next, useless for arguing with.

<!-- AUTHOR-REVIEW: this chapter's outline declares D2.2 only, but §1, §7 and §8 teach from snapshots tagged D4 (Cloud Native Ecosystem and Principles) — the 4Cs page, the CNCF Policy-as-Code glossary entry, Sigstore, in-toto, TUF, Harbor, Kyverno and Falco. That is under-declaration, not scope creep, but D4 is 12% of the exam and this is one of the few chapters teaching its ecosystem content. Recommend adding D4 to the chapter's declared objectives so the book-close coverage report does not raise a phantom "D4 under-covered" finding. -->

---

## Attention Budget

**Total time: ~155 minutes of reading, plus about 35 more for the exam alert, the practice questions and the summary | Recommended: split the reading across two sessions**

The natural seam is after Checkpoint #2. Sections 1 through 6 are the Kubernetes API and the workload; sections 7 through 9 leave the cluster, go looking at what you shipped, and come back. They are genuinely different material and a break between them costs you nothing.

| Block | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| 🧭 Soundings | 10 min | Medium | Before you start reading |
| Why This Chapter Matters / What You'll Learn | 6 min | Low | Anytime |
| §1 Four Layers and Four Phases | 10 min | Low | Anytime |
| §2 Who You Are | 12 min | Medium | When alert |
| §3 What You May Do | 22 min | High | Peak attention |
| ☆ Taking Your Bearings #1 | 8 min | Medium | After a brief break |
| §4 Secrets Are Not Encrypted | 14 min | Medium | When alert |
| §5 What a Pod May Do to Its Node | 16 min | High | Peak attention |
| §6 Three Levels, Three Modes | 12 min | Medium | When alert |
| ☆ Taking Your Bearings #2 | 8 min | Medium | After a brief break |
| **— session break —** | | | |
| §7 Trusting What You Ship | 14 min | Medium | Anytime |
| §8 Rules That Watch | 8 min | Low | Anytime |
| ☆ Taking Your Bearings #3 | 8 min | Medium | After a brief break |
| §9 Additive, Never Deny | 6 min | Low | When you can think, not when you can grind |
| Exam Alert | 4 min | Low | Anytime |
| Practice Questions (23) | 28 min | High | A separate sitting from the reading |
| Chapter Summary / The Voyage Ahead | 4 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** concrete, familiar concepts — study anytime.
- **Medium:** new concepts requiring focus — study when alert.
- **High:** abstract or dense material — study at peak attention.

*If you only have fifteen minutes: read §3 and take Checkpoint #1. It is the densest section in the chapter and the highest-yield material in the domain.*

---

> *"The RBAC API prevents users from escalating privileges by editing roles or role bindings. Because this is enforced at the API level, it applies even when the RBAC authorizer is not in use."*
> — Kubernetes documentation, *Using RBAC Authorization*

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score sets your reading strategy. There is no wrong score, only different approaches.

Six of these test material from earlier chapters. Two — questions 6 and 7 — ask you to reason from professional intuition you may have built outside Kubernetes entirely. Answer both kinds honestly; the second kind is doing more work than it looks like.

1. A resource is cluster-scoped rather than namespaced. Can a permission over it be granted "inside one namespace"? Is your answer a matter of policy, or is it forced by something structural?

2. A Pod's manifest names no ServiceAccount. What identity does the Pod run as, and where did that identity come from?

3. A Secret's values are base64-encoded. What does base64 do to those values, and — stated as plainly as Chapter 4 stated it — what does it *not* do?

4. Name the three gates an API request passes through, in order. Which of the three runs last?

5. Can one NetworkPolicy deny traffic that a different NetworkPolicy allows?

6. Think of a permission system you have actually used: Unix file modes, a cloud IAM policy, a Windows ACL, a firewall ruleset. In that system, can one rule *subtract* access that another rule grants?

7. A software release is signed. What does that signature prove, and what does it not prove? Would a signature that covers a *tag* mean the same thing as one that covers a *digest*?

8. A process is running as root inside a container. Is that the same root as the node's? What does Chapter 2 §1 tell you that bears on the answer?

<details>
<summary>Answers + reading strategy</summary>

**1.** No — and the answer is forced, not chosen. A cluster-scoped resource belongs to no namespace at all, so there is no namespace inside which the grant could be made. *[cross-bearing: see Ch 4 §3 — namespaced and cluster-scoped]*

**2.** The `default` ServiceAccount for its namespace. Every namespace gets one at creation, and Kubernetes assigns it to any Pod that does not name another. *[cross-bearing: see Ch 5 §6 — a Pod's identity]*

**3.** Base64 makes the value transport-safe as text. It does not encrypt, obscure, or protect it: anyone who can read the encoded string can decode it in one command. *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*

**4.** Authentication, then authorization, then admission. Admission runs last. *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*

**5.** No. NetworkPolicies are additive: each one allows, and the effect of several is the union of what they allow. There is no way to write a policy that takes away traffic another policy permits. *[cross-bearing: see Ch 10 §6 — allowing, never denying]*

**6.** Almost certainly yes. Unix has no explicit deny, but cloud IAM does, Windows ACLs do, and firewall rulesets are built out of it, with the order-dependence that comes along for the ride. Hold on to that expectation. This chapter is going to violate it twice.

**7.** A signature proves that some specific bytes were signed by the holder of some specific key, and nothing more. It does not prove the software is safe, correct, or free of vulnerabilities. On the second half: if your instinct was that a signature over a tag and a signature over a digest are not the same statement, hold that answer — §7 shows what signing tools actually do about it. *[cross-bearing: see Ch 2 §3 — registries, tags, and digests]*

**8.** Chapter 2 §1 gives you the material: a container is a process in a set of Linux namespaces and cgroups, sharing the host's kernel. That points both ways at once. The process is *isolated* from the host's view of things, but it is running against the same kernel. Which of those two facts dominates is exactly what §5 is about.

---

**If you got 6 or more right:** skim. Read the ★ Fixed Points, the ⚠ Navigational Hazards, and §3 and §9 in full: §3 because it is where most of this chapter's traps live, §9 because it makes an argument you cannot get from a summary. Then go straight to the Practice Questions.

**If you got 3 to 5 right:** read at normal pace. The chapter is calibrated for you.

**If you got 0 to 2 right:** read carefully, and re-read **Chapter 4 §3 before you start this chapter** — not alongside it, before it. Section 3 below is built as a derivation from that boundary, and two earlier chapters have already promised you it would be. The others can wait until you reach the section that needs them: Ch 5 §6 (a Pod's identity) before §2, Ch 8 §2 (the three gates) before §6, Ch 10 §6 (allowing, never denying) before §9.

</details>

---

## Why This Chapter Matters

Chapter 11 left you holding a question and refused to answer it: **what is a workload allowed to do, and who decided?**

That question stays open for the next eight sections. Chapter 11 also gave you something deliberately, as a tell: the permission system you are about to learn has no way to say no. None. You now know one other system with the same property, because you met it in Chapter 10 and it surprised you then. What you have not been told is *why*, and this chapter owes you that. Sections 2 through 8 are the evidence. Section 9 is the argument.

Something changes for you along the way. There is a line between an engineer who can *use* a cluster and an engineer who can be trusted with somebody else's, and this chapter is most of it. Every control in here answers a question a platform team gets asked in a room with an auditor in it: *Who can read the database password? What stops a compromised container from reading the node's kubelet credentials? How do you know the image running in production is the one your build system produced?* Naming which control answers which question is the job. Not reciting the controls: mapping them onto questions.

That is also why this chapter carries two framings rather than one, and why §1 spends its time on maps instead of features. The two maps answer different questions, and neither answer implies the other. A cluster with immaculate RBAC and an unsigned image from an unverified registry is not a secure cluster. It is a cluster with immaculate RBAC.

Two facts in this chapter are things a competent engineer will get wrong on a real cluster, today, without noticing. The first is that a Secret is protected because its values are base64-encoded. The second is that a namespace where somebody holds only a `view` RoleBinding is a safe place to let them look around. Both are wrong, both are wrong quietly, and both are wrong in a way that produces no error message and no alert. That is the honest stake here — not a story about a breach, just the plain observation that these two mistakes are invisible right up until they are not.

> **Dead Reckoning:** Security in Kubernetes is not one system. It is five systems that answer five different questions: *who are you*, *what may you do*, *what is stored where*, *what may your workload do to the machine it runs on*, and *what did you actually ship*. They were built at different times by different people. They do not check each other's work. None of them substitutes for another, and the failure of any one of them is not detected by the other four.

> **Extended Analogy:** A ship carries locks, keys, and watchstanders, and the reason all three exist is that no one of them does the others' work.
>
> The **key** is not the permission. A key is a credential, a piece of metal that proves you are the person the quartermaster issued it to. What *opens* a particular door is the ship's manifest of who holds which key, kept somewhere else entirely, revisable without touching the key itself. Kubernetes keeps these in two different objects on purpose, and confusing them is the most common conceptual error in this chapter: a ServiceAccount is a key, and it opens nothing at all until something else says it does.
>
> The **strongbox is not the safe.** A strongbox keeps papers together, dry, and in one identifiable place. It does not make them unreadable to anyone who opens it. Kubernetes Secrets are a strongbox: a distinct object type with its own handling, its own access rules, and its own storage path. The mistake is assuming the box came with a lock fitted. It did not, and Chapter 4 told you so.
>
> And the **watch does not prevent anything.** A lookout at the masthead has no authority to alter course. The watch's entire function is to see, and to report what it saw to someone who can act. That distinction is the whole of §8: some tools in this chapter refuse things at the gate, and one of them stands on deck and tells you what already happened. Confusing those two is how people end up believing they have a control when what they have is a log entry.

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Place** any Kubernetes security control on two maps at once — which layer it protects, and which lifecycle phase it acts in — and tell which of the two an exam question is actually asking about.
- **Distinguish** an identity from a permission, and name the two separate objects Kubernetes keeps them in.
- **Derive** which of Role, ClusterRole, RoleBinding and ClusterRoleBinding a situation calls for, from the namespaced/cluster-scoped boundary you already have, rather than from a memorized table.
- **State** what protects a Secret, what does not, and the three ways somebody reads one anyway — one of which is simply being allowed to create a Pod, which nobody thinks of as a permission to read secrets.
- **Read** a `securityContext` and a namespace's Pod Security labels together, and predict whether a given Pod is admitted, warned about, or refused outright.
- **Trace** an image from build to running container and name the checkpoint at each handoff, including which one a signature actually covers.

*You will also finish an argument Chapter 10 started and Chapter 11 refused to settle: why two Kubernetes systems built for entirely unrelated purposes both refuse to let you say no.*

---

## ⚪ §1 — Four Layers and Four Phases

Kubernetes security has two standard maps, and the reason to learn both is that they answer different questions. One tells you *where* a control sits. The other tells you *when* it acts.

### The phases: when

The Kubernetes documentation now frames cloud native security around the lifecycle phases defined in the CNCF's cloud native security whitepaper: **develop, distribute, deploy, and runtime** [source: k8s-docs-cloud-native-security-2026-08-23].

**Develop** is about the integrity of the development environment and the design of the application. The documentation names adopting an architecture such as zero trust that minimizes attack surface even against internal threats, defining a code review process that considers security, and building a threat model that identifies trust boundaries [source: k8s-docs-cloud-native-security-2026-08-23]. Nothing in this phase is a Kubernetes object. That is the point of having the phase.

**Distribute** is the supply chain, for your container images and for the cluster components themselves. The recommendations are concrete: scan container images and other artifacts for known vulnerabilities; ensure software distribution uses encryption in transit with a chain of trust for the software source; use validation mechanisms such as digital certificates for supply chain assurance; and restrict access to artifacts by placing container images in a private registry that only allows authorized clients to pull [source: k8s-docs-cloud-native-security-2026-08-23]. That list is §7's outline.

**Deploy** is about restrictions on *what* can be deployed, *who* can deploy it, and *where* it can go [source: k8s-docs-cloud-native-security-2026-08-23]. Read that sentence again with a slight squint and you have described GitOps before anyone has given you the word: a system whose entire job is to constrain what reaches the cluster, from where, on whose authority. *[cross-bearing: see Ch 15 — push, or pull]*

**Runtime** is where most of this chapter lives, and the documentation splits it into three areas: **access, compute, and storage** [source: k8s-docs-cloud-native-security-2026-08-23]. That split is this chapter's table of contents.

- **Runtime protection: access.** The Kubernetes API is what makes the cluster work, so protecting it is the core of cluster security — effective authentication and authorization for API access, ServiceAccounts to provide and manage security identities for workloads and cluster components, and TLS protecting API traffic including between nodes and the control plane [source: k8s-docs-cloud-native-security-2026-08-23]. That is §2 and §3.
- **Runtime protection: compute.** Enforce Pod Security Standards so applications run with only the privileges they need; run a specialized, typically read-only immutable node operating system; define ResourceQuotas and LimitRanges; **partition workloads across different nodes to improve isolation**; use a container runtime that provides security restrictions; and on Linux nodes use a security module such as AppArmor or seccomp [source: k8s-docs-cloud-native-security-2026-08-23]. That is §5 and §6, and note two familiar objects showing up in a new role. ResourceQuota and LimitRange were fairness controls when you met them; here they are security controls, because a workload that can exhaust a node is a workload that can affect every other workload on it. *[cross-bearing: see Ch 8 §3 — dividing a shared cluster]* And "partition workloads across different nodes" is the isolation use of node selection that Chapter 7 told you would come back. *[cross-bearing: see Ch 7 §4 — when the berth refuses you]*
- **Runtime protection: storage.** Integrate an external storage plugin providing encryption at rest for volumes; enable encryption at rest for API objects; protect durability with backups you have verified you can restore; authenticate connections between nodes and network storage; and encrypt data within the application itself [source: k8s-docs-cloud-native-security-2026-08-23]. That is §4.

Sandboxed runtimes sit in runtime/compute. The "container runtime that provides security restrictions" clause [source: k8s-docs-cloud-native-security-2026-08-23] is where RuntimeClass and the sandboxed runtimes belong on this map. *[cross-bearing: see Ch 2 §7 — not all isolation is equal]*

### The layers: where

The other framing is older. It is the one the Kubernetes project's own security overview carried in the v1.22 documentation, and it is still the framing most third-party material uses. **The 4Cs of Cloud Native security are Cloud, Clusters, Containers, and Code** [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31], and they nest: each layer of the model builds upon the next outermost layer, so the Code layer benefits from strong Cloud, Cluster and Container security beneath it. That page states the consequence bluntly — *"You cannot safeguard against poor security standards in the base layers by addressing security at the Code level"* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31].

**Cloud** is the trusted computing base. The page is direct: *"If the Cloud layer is vulnerable (or configured in a vulnerable way) then there is no guarantee that the components built on top of this base are secure"* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31]. Its concerns are network access to the API server and the nodes, the permissions the cluster holds against the cloud provider's own API, and access to etcd, including the recommendation that etcd's disk especially should be encrypted at rest, *since etcd holds the state of the entire cluster (including Secrets)* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31]. Hold that clause. §4 is going to need it.

**Cluster** splits into securing the configurable cluster components and securing the applications that run in the cluster, and the workload-security list reads like this chapter's index: RBAC authorization, authentication, application secrets management including encryption at rest, Pod Security Standards, resource management, network policies, and TLS for Ingress [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31].

**Container** covers vulnerability scanning as part of the image build, image signing and enforcement to maintain a system of trust, creating users inside containers with the least OS privilege necessary, and selecting container runtime classes that provide stronger isolation [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31].

**Code** is described as *"one of the primary attack surfaces over which you have the most control"* — TLS for everything in transit, limiting exposed port ranges, scanning third-party dependencies, static analysis, and dynamic probing against your own service [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31].

### Why both

A reasonable question at this point is why a book would teach you two maps of the same territory. The honest situation:

The current kubernetes.io security overview presents the lifecycle phases. It *replaced* the 4Cs framing on that page [source: k8s-docs-cloud-native-security-2026-08-23]. So the phases are the current framing from the primary authority, and if the exam draws from the current documentation, the phases are what it is drawing from.

But the 4Cs have not gone anywhere else. The framing predates the current page, and you will still meet it in third-party material and in internal security documentation written before the change. It is also genuinely useful, because it answers a question the phases do not.

Which brings us to the actual distinction, and it is worth more than either list.

> **★ Fixed Point**
>
> **The phases answer *when* a control acts. The layers answer *where* it acts.** Every control in this chapter has a position on both maps. A question that appears to be about one is frequently about the other.

Image signing sits in the **distribute** phase: it happens after the build, before anything reaches the cluster. It also sits at the **Container** layer, because what it protects is the container image. Neither of those statements is more true than the other and neither implies the other. RBAC is **runtime/access** on the phase map and **Cluster** on the layer map. `securityContext` is **runtime/compute** and **Container**. Encryption at rest is **runtime/storage** and **Cloud** (the etcd disk) shading into **Cluster** (the API objects).

The whole thing at once, then, with a few controls plotted on both.

<!-- FIGURE: ch12-fig01-4cs-and-lifecycle-phases -->
```
   THE PHASES — when a control acts
   ─────────────────────────────────────────────────────────────────

   DEVELOP  ────▶  DISTRIBUTE  ────▶  DEPLOY  ────▶  RUNTIME
                                                       │
                                          ┌────────────┼────────────┐
                                          │            │            │
                                        ACCESS      COMPUTE      STORAGE


   THE LAYERS — where a control acts
   ─────────────────────────────────────────────────────────────────

   ┌─ CLOUD ──────────────────────────────────────────────┐
   │  ┌─ CLUSTER ─────────────────────────────────────┐   │
   │  │  ┌─ CONTAINER ────────────────────────────┐   │   │
   │  │  │  ┌─ CODE ──────────────────────────┐   │   │   │
   │  │  │  │                                 │   │   │   │
   │  │  │  └─────────────────────────────────┘   │   │   │
   │  │  └────────────────────────────────────────┘   │   │
   │  └───────────────────────────────────────────────┘   │
   └──────────────────────────────────────────────────────┘


   FIVE CONTROLS, PLOTTED ON BOTH
   ─────────────────────────────────────────────────────────────────

   control                    phase                layer
   ──────────────────────────────────────────────────────────────
   RBAC                       runtime / access     Cluster
   ServiceAccount             runtime / access     Cluster
   securityContext            runtime / compute    Container
   encryption at rest         runtime / storage    Cloud → Cluster
   image signing              distribute           Container
```

Do not try to hold twelve controls on this map yet. Hold the *shape*: four phases in sequence, four layers nested, and the runtime phase split three ways. The sections that follow fill it in.

---

## ⚪ §2 — Who You Are

Every request that reaches the Kubernetes API arrives claiming to be somebody. This section is about who that somebody can be, and, as importantly, about what that claim is *not*.

### The object

A **ServiceAccount** is a type of non-human account that provides a distinct identity in a Kubernetes cluster. Application Pods, system components, and entities both inside and outside the cluster can use a ServiceAccount's credentials to identify as that ServiceAccount [source: k8s-docs-service-accounts-2026-08-23]. They exist as ServiceAccount objects in the API server. They are **namespaced**, bound to a Kubernetes namespace, with every namespace getting a `default` ServiceAccount on creation, and they are lightweight and portable [source: k8s-docs-service-accounts-2026-08-23].

You met the object in Chapter 5, where it was introduced as the identity a Pod runs as. *[cross-bearing: see Ch 5 §6 — a Pod's identity]* That chapter deliberately stopped there and deferred everything about permissions to here. This section collects that plant; it does not re-teach it.

What Chapter 5 could not tell you is the contrast that makes ServiceAccounts interesting. Service accounts are **different from user accounts**, which are authenticated human users in the cluster — and *"by default, user accounts don't exist in the Kubernetes API server"* [source: k8s-docs-service-accounts-2026-08-23].

Read that twice. Kubernetes has no User object. There is no `kubectl create user`. A human identity arrives at the API server from *outside the cluster*, and Kubernetes' job is to validate the claim, extract a username and a set of groups, and hand those strings to the next gate. It stores nothing. Usernames are just strings, and *"it is up to you as a cluster administrator to configure the authentication modules so that authentication produces usernames in the format you want"* [source: k8s-docs-rbac-depth-2026-08-31]. Groups likewise are strings, supplied by the authenticator, with the `system:` prefix reserved [source: k8s-docs-rbac-depth-2026-08-31].

<!-- AUTHOR-REVIEW: this chapter's corpus has no snapshot covering Kubernetes authentication *mechanisms* — X.509 client certificates, OIDC token authentication, authenticating proxies. The paragraph above therefore says only "from outside the cluster" rather than naming them, which is what the corpus supports. If the author wants the three named, it needs a fetch of https://kubernetes.io/docs/reference/access-authn-authz/authentication/. -->

That asymmetry — in-cluster identities are objects, human identities are not — surprises people, and it is the reason ServiceAccounts get their own section while users get a paragraph. Human identity is somebody else's system. Workload identity is Kubernetes'.

> 🔭 **Closer Look:** ServiceAccounts get names prefixed with `system:serviceaccount:` and belong to groups prefixed with `system:serviceaccounts:` [source: k8s-docs-rbac-depth-2026-08-31]. Singular for the account, plural for the group. That one-character difference is real, and it is exactly the sort of thing that is unpleasant to debug at 3 a.m.

### The default account, and what it can do

When you create a cluster, Kubernetes automatically creates a ServiceAccount named `default` for every namespace. If you delete it, the control plane replaces it. And if you deploy a Pod in a namespace without manually assigning it a ServiceAccount, Kubernetes assigns the namespace's `default` [source: k8s-docs-service-accounts-2026-08-23].

Now the part that matters:

> **The default service accounts in each namespace get no permissions by default other than the default API discovery permissions that Kubernetes grants to all authenticated principals if RBAC is enabled** [source: k8s-docs-service-accounts-2026-08-23].

API discovery means the endpoints that tell a client what API groups and versions the server supports. It is the read-only self-description every client needs before it can do anything at all. That is the entire budget.

> **★ Fixed Point**
>
> **An identity and a permission are two different things, kept in two different objects.** The `default` ServiceAccount is the proof: every Pod in the cluster has an identity, and almost none of them can do anything with it.

The sidebar's first panel was about exactly this. A key is stamped, issued, and unmistakably yours; what it opens is written down somewhere else entirely, and until somebody writes it there, the key turns nothing.

This is the single most useful sentence in the chapter for reasoning about the rest of it, and it is why §2 comes before §3 rather than merging with it. Creating a ServiceAccount grants nothing. Assigning it to a Pod grants nothing. The Pod authenticates successfully, arrives at the second gate, and is turned away — a completely different failure from not being recognized at all, and one that produces a different message. *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*

You assign one with `spec.serviceAccountName` in the Pod spec. The documented sequence is: create a ServiceAccount object; grant permissions to it using an authorization mechanism such as RBAC; and assign it to Pods at creation time via `spec.serviceAccountName` [source: k8s-docs-service-accounts-2026-08-23]. Three steps, and the middle one is §3.

The documented use cases read as a list of "why would a workload need to be somebody" [source: k8s-docs-service-accounts-2026-08-23]:

- Pods that need to talk to the Kubernetes API server — reading Secrets, cross-namespace access.
- Pods that need to talk to an external service that requires an identity.
- Authenticating to a private image registry using an `imagePullSecret`.
- An external service that needs to talk to the API server — a CI/CD pipeline, for instance.
- Third-party security software that relies on the ServiceAccount identity of different Pods to group them into contexts.

The fourth of those is worth pausing on. An agent running outside the cluster, or an agent running inside it whose job is to reconcile the cluster's contents against something, is a subject exactly like any Pod is a subject. It needs an identity, it needs grants, and because its job is broad its grants tend to be broad. That is a shape you will meet again. *[cross-bearing: see Ch 15 §4 — an agent that watches a repository]*

### The credential

An identity is not much use without something to prove it with. That something is a token, and the recommended way of getting one changed.

In Kubernetes v1.22 and later, Kubernetes gets a short-lived, automatically rotating token using the **TokenRequest** API and mounts the token as a **projected volume**. The recommended approach is the TokenRequest API or token volume projection. **Not** recommended: long-lived ServiceAccount token Secrets, which don't expire or rotate and pose a security risk [source: k8s-docs-service-accounts-2026-08-23].

You have already seen the delivery mechanism. When Chapter 11 walked the volume types, the projected volume was there, and what it was projecting into the Pod was precisely this. *[cross-bearing: see Ch 11 §1 — three lifetimes, and the volumes that have them]*

> 🪝 **Snag:** There is a Secret type called `kubernetes.io/service-account-token` [source: k8s-docs-secret-2026-08-23], and its existence makes it look like the current mechanism. It is the legacy one. A Secret of that type is a credential written to etcd that neither expires nor rotates, which means a copy of it taken today still works next year. If a question offers you "create a ServiceAccount token Secret" as the way to give a Pod credentials, that is the distractor. The token arrives by projection, and nothing durable is created.

The whole flow, then, and note what is deliberately missing from it.

<!-- FIGURE: ch12-fig03-serviceaccount-token-flow -->
```
   ┌──────────────────────┐
   │  ServiceAccount      │      a namespaced object in the API server
   │  ns/my-app           │      — an IDENTITY, and nothing more
   └──────────┬───────────┘
              │
              │  spec.serviceAccountName: my-app
              ▼
   ┌──────────────────────┐
   │  TokenRequest API    │      short-lived, automatically rotating
   └──────────┬───────────┘
              │
              ▼
   ┌──────────────────────────────────────────┐
   │  Pod                                     │
   │    projected volume                      │
   │      └── token  ◀── mounted, rotated     │
   └──────────┬───────────────────────────────┘
              │
              │  API request, bearing the token
              ▼
   ┌──────────────────────┐
   │  GATE 1              │      "who are you?"
   │  AUTHENTICATION      │      ✔ you are ns/my-app
   └──────────┬───────────┘
              │
              ▼
   ┌──────────────────────┐
   │  GATE 2              │      "what may you do?"
   │  AUTHORIZATION       │
   │                      │      ┌─────────────────────────┐
   │      ...             │◀─────┤  nothing here yet.      │
   │                      │      │  see §3.                │
   └──────────────────────┘      └─────────────────────────┘
```

The emptiness on the right is the Fixed Point drawn. The identity is complete. The token is valid. Authentication succeeds. And the account can do nothing, because nothing has been said about permissions yet.

### Identity outlives the workload

One more thing, easy to miss and directly consequential.

Kubernetes checks for and deletes objects that no longer have owner references, and owner references are what drive that garbage collection [source: k8s-docs-garbage-collection-2026-08-24]. When you delete a Deployment, cascading deletion removes what the Deployment owns. It does **not** remove the ServiceAccount those Pods ran as — because a ServiceAccount you created alongside a Deployment carries no owner reference back to it. Neither do the Secrets it referenced. Neither do the RoleBindings that granted it anything.

Chapter 6 told you that deleting a workload does not delete everything it referenced, and pointed here. *[cross-bearing: see Ch 6 §3 — how a controller knows its own]* This is the security consequence: **identity and grants outlive the workload that used them.** A cluster that has been in production for three years accumulates ServiceAccounts nobody remembers creating, still holding grants nobody remembers making, ready to be used by anything that can name them. Nobody deletes them, because nobody is certain what would break.

That is not an exotic attack. It is entropy, and cleaning it up is one clause of what least privilege means in practice — which brings us to the object that does the granting.

---

## 🔵 §3 — What You May Do

Before anything else, a word about a word.

This is the third distinct sense of **binding** you have met in six chapters, and you met the second one *last chapter*. The scheduler binds a Pod to a node: a one-time decision, filter then score then bind *[cross-bearing: see Ch 7 §1 — one decision, made once]*. A PersistentVolumeClaim binds to a PersistentVolume, exclusive and one-to-one *[cross-bearing: see Ch 11 §2 — the claim and the supply]*. Neither of those is what this section means. **Inside this section, a bare "binding" means the RBAC object and nothing else**, and the objects themselves are always written out in full: `RoleBinding`, `ClusterRoleBinding`. If you catch yourself expecting an RBAC binding to be exclusive or one-to-one because the last one you met was, it is not. A subject may hold any number of them and they all apply at once.

With that cleared: authorization.

### RBAC is *an* authorization mode

The Kubernetes API server does not have one authorization mechanism. It has a chain of them, and the documentation is precise about how the chain behaves: **"All parts of an API request must be allowed by some authorization mechanism in order to proceed"** and *"[each authorizer] is checked in sequence. If any authorizer approves or denies a request, that decision is immediately returned and no other authorizer is consulted. If all modules have no opinion on the request, then the request is denied"* [source: k8s-docs-authorization-2026-08-31].

The modules include **Node**, a special-purpose mode granting permissions to kubelets based on the pods they are scheduled to run; **ABAC**, an access control paradigm whereby access rights are granted to users through policies which combine attributes together; **RBAC**, which regulates access based on the roles of individual users within an enterprise; and **Webhook**, which makes a synchronous HTTP callout, blocking the request until the remote service responds [source: k8s-docs-authorization-2026-08-31]. Chapter 8 quoted that list at you and pointed here. *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*

So: RBAC is what essentially every cluster uses and what the curriculum teaches, but it is one mode among several rather than the mechanism. That one clause is all ABAC gets in this book, and it is enough. The fact worth holding is that other modes exist, not how they work.

RBAC uses the `rbac.authorization.k8s.io` API group to drive authorization decisions, allowing policies to be configured dynamically through the Kubernetes API [source: k8s-docs-rbac-2026-08-23]. Four object kinds: **Role, ClusterRole, RoleBinding and ClusterRoleBinding** [source: k8s-docs-rbac-2026-08-23].

### The two role objects

> **Dead Reckoning:** A Role or ClusterRole contains rules representing a set of permissions. A Role always sets permissions within a particular namespace, and you must specify that namespace when you create it. A ClusterRole is a non-namespaced resource. A RoleBinding grants a role's permissions to a list of subjects within a specific namespace; a ClusterRoleBinding grants that access cluster-wide. A RoleBinding may reference any Role in the same namespace, or may reference a ClusterRole and bind it into the RoleBinding's namespace. After you create a binding, you cannot change the Role or ClusterRole it refers to. The four default user-facing roles are `cluster-admin`, `admin`, `edit`, and `view`. [source: k8s-docs-rbac-2026-08-23]

That paragraph is the whole object model stated flat, and if you memorize nothing else from this section, memorize it. Now take it apart, because there is a derivation hiding in it that two earlier chapters have already promised you.

**Role** is namespaced. When you create one, you have to say which namespace it belongs in [source: k8s-docs-rbac-2026-08-23]. **ClusterRole**, by contrast, is a non-namespaced resource, and the documentation lists three distinct uses for one [source: k8s-docs-rbac-2026-08-23]:

1. Define permissions on **namespaced** resources and be granted access **within individual namespaces**.
2. Define permissions on **namespaced** resources and be granted access **across all namespaces**.
3. Define permissions on **cluster-scoped** resources.

Notice that only the third of those is about cluster-scoped resources. Two of the three uses of a ClusterRole concern namespaced resources, which means the object's name is actively misleading about two thirds of its job.

The rule the documentation gives for choosing is simple: *"If you want to define a role within a namespace, use a Role; if you want to define a role cluster-wide, use a ClusterRole"* [source: k8s-docs-rbac-2026-08-23].

### The two binding objects, and the derivation

A binding grants the permissions defined in a role to a user or set of users. It holds a list of **subjects** — users, groups, or service accounts — and a reference to the role being granted [source: k8s-docs-rbac-2026-08-23]. A RoleBinding grants permissions within a specific namespace; a ClusterRoleBinding grants that access cluster-wide.

And then the sentence that does the work:

> *"A RoleBinding may reference any Role in the same namespace. Alternatively, a RoleBinding can reference a ClusterRole and bind that ClusterRole to the namespace of the RoleBinding."* [source: k8s-docs-rbac-2026-08-23]

Four objects, and the natural reflex is to make a two-by-two table and memorize the cells. Chapter 4 told you not to. *[cross-bearing: see Ch 4 §3 — where a name lives]* Chapter 8 told you the same thing in nearly the same words. So: the derivation instead, and it needs exactly one thing you already have.

Chapter 4 established that some resources are namespaced and some are cluster-scoped. Put that beside two sentences you already have from the RBAC reference: *"A Role always sets permissions within a particular namespace"*, and *"ClusterRole, by contrast, is a non-namespaced resource"* [source: k8s-docs-rbac-2026-08-23]. A cluster-scoped resource belongs to no namespace, not to all of them — so **there is no namespace inside which a Role could hold a rule about it**. Not "should not." *Could not.* The difference between "no namespace" and "all namespaces" is the entire derivation.

<!-- AUTHOR-REVIEW: the consequence stated above — that a cluster-scoped rule has nowhere to land when a ClusterRole is bound by a namespace-scoped RoleBinding — follows from the two sourced sentences quoted immediately before it, but no page in this chapter's corpus states it outright. Four reader-facing conclusions rest on it: this paragraph, figure ch12-fig02's fourth row, Taking Your Bearings #1 answer 3, and Practice Question 5's option-B explanation. Recommend fetching the RBAC reference's RoleBinding/ClusterRoleBinding section to confirm before release; if it cannot be confirmed, all four sites need softening together, not individually. -->

Start from there and ask two independent questions.

**Question one: what does this permission cover?** If the resources are namespaced, a Role can hold the rules, because a Role's scope has room for them. If any resource is cluster-scoped, a Role cannot hold the rules, because a Role is defined within a namespace and the resource is not in one. So cluster-scoped resources force a **ClusterRole**. Not by convention, but by the structure of what a Role is.

**Question two: where should the grant apply?** If it should apply in one namespace, a **RoleBinding** in that namespace. If it should apply everywhere, a **ClusterRoleBinding**.

Those two questions are independent, which is why there are four objects rather than two. And the combination that surprises people, a ClusterRole bound by a RoleBinding, falls out immediately: you wrote the rules in a ClusterRole because you wanted them reusable, or because you needed cluster-scoped resources; you bound them with a RoleBinding because you wanted the grant to land in one namespace.

<!-- FIGURE: ch12-fig02-rbac-four-way-matrix -->
```
   THE BOUNDARY YOU ALREADY HAVE  (Ch 4 §3)
   ─────────────────────────────────────────

   NAMESPACED resource                       CLUSTER-SCOPED resource
   lives inside a namespace                  lives in NO namespace
   Pod, Service, Secret,                     Node, PersistentVolume,
   Deployment, ConfigMap                     StorageClass, Namespace
        │                                            │
        │                                            │
        │  a Role's scope has room for it            │  a Role has nowhere
        │                                            │  to put it
        ▼                                            ▼
   ┌─────────────────────┐                  ┌─────────────────────┐
   │ Role                │                  │ ClusterRole         │
   │  or ClusterRole     │  ◀── either ──   │  FORCED             │
   └─────────────────────┘                  └─────────────────────┘


   THE SECOND, INDEPENDENT QUESTION
   ─────────────────────────────────────────

        where should the grant apply?
                  │
        ┌─────────┴──────────┐
        ▼                    ▼
   one namespace        every namespace
        │                    │
        ▼                    ▼
   ┌──────────────┐    ┌─────────────────────┐
   │ RoleBinding  │    │ ClusterRoleBinding  │
   └──────────────┘    └─────────────────────┘


   THE FOUR COMBINATIONS FALL OUT
   ─────────────────────────────────────────

   Role      + RoleBinding         → those rules, in that namespace
   ClusterRole + RoleBinding       → those rules, in that ONE namespace
   ClusterRole + ClusterRoleBinding→ those rules, everywhere
   Role      + ClusterRoleBinding  → ✗ does not exist. A Role "always sets
                                       permissions within a particular
                                       namespace"; a ClusterRoleBinding
                                       grants access cluster-wide. There is
                                       nothing cluster-wide to grant.

   ┌───────────────────────────────────────────────────────────────┐
   │  ▶  THE BINDING DETERMINES THE SCOPE OF THE GRANT.            │
   └───────────────────────────────────────────────────────────────┘
```

If you cover the bottom of that figure, you should be able to rebuild it from the top. That is the test of whether you have the derivation or just the table.

> **★ Fixed Point**
>
> **The binding determines the scope of the grant.** A ClusterRole bound by a RoleBinding grants that ClusterRole's permissions *inside that one namespace only* — including `cluster-admin`, which is where this trips people.

That last clause is not hypothetical. The documentation says of `cluster-admin`: *"When used in a ClusterRoleBinding, it gives full control over every resource in the cluster and in all namespaces. When used in a RoleBinding, it gives full control over every resource in the role binding's namespace, including the namespace itself"* [source: k8s-docs-rbac-2026-08-23]. Same ClusterRole. Two completely different amounts of power, decided entirely by which binding object you reached for.

### Rules: verbs over resources

Inside a Role or ClusterRole, the rules name verbs and resources. The verbs the API recognizes are `get`, `list`, `create`, `update`, `patch`, `watch`, `delete`, and `deletecollection` [source: k8s-docs-authorization-2026-08-31]. Authorization decisions also consider the resource name, the subresource, the namespace, and the API group [source: k8s-docs-authorization-2026-08-31].

You can narrow further. *"You can also refer to resources by name for certain requests through the `resourceNames` list. When specified, requests can be restricted to individual instances of a resource"* [source: k8s-docs-rbac-depth-2026-08-31], so "may read the Secret named `db-password`, and no other Secret" is expressible. With limits: *"You cannot restrict deletecollection or top-level create requests by resource name. For create, this limitation is because the name of the new object may not be known at authorization time"* [source: k8s-docs-rbac-depth-2026-08-31]. Which is exactly right when you think about it: you cannot filter on a name that does not exist yet.

And a fact that costs one sentence and saves a lot of confusion later: **RBAC rules name custom resources exactly as they name built-in ones.** The documentation says so directly — aggregation *"lets you, as a cluster administrator, include rules for custom resources, such as those served by CustomResourceDefinitions or aggregated API servers, to extend the default roles"*, and *"You can assume that CronTab objects are named `"crontabs"` in URLs as seen by the API server"* [source: k8s-docs-rbac-depth-2026-08-31]. A CRD-backed resource lives in the same API, gets addressed the same way, and is granted the same way. Chapter 6 promised you that custom resources work with `kubectl get`, labels, selectors, namespaces, RBAC, all of it. *[cross-bearing: see Ch 6 §8 — the control loop, extended]* Nothing special is required here, and that is the whole point of putting custom resources in the API in the first place.

### Aggregated ClusterRoles

*"You can aggregate several ClusterRoles into one combined ClusterRole. A controller, running as part of the cluster control plane, watches for ClusterRole objects with an `aggregationRule` set. The `aggregationRule` defines a label selector that the controller uses to match other ClusterRole objects that should be combined into the `rules` field of this one"* [source: k8s-docs-rbac-depth-2026-08-31]. Create a new ClusterRole matching the selector and its rules get added to the aggregate automatically.

Which is a control loop — desired state expressed as a selector, a controller reconciling toward it — doing a job you have watched it do elsewhere. *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*

The default user-facing roles use aggregation, which is how a cluster administrator can extend `admin`, `edit` and `view` to cover custom resources [source: k8s-docs-rbac-depth-2026-08-31]. Define a ClusterRole with the right labels and the built-in roles quietly gain the rules.

### Subjects are named, not selected

Something here should stop you.

Chapter 4 taught you that Kubernetes joins things with **selectors**. A Deployment finds its Pods by selector. A Service finds its endpoints by selector. A NetworkPolicy finds the Pods it applies to by selector. An aggregated ClusterRole, two paragraphs ago, finds its member ClusterRoles by selector. The pattern is so consistent that Chapter 4 warned you specifically that assuming it holds here would produce *a specific, confident, wrong prediction in Chapter 12*. *[cross-bearing: see Ch 4 §5 — the universal join]*

This is that prediction. RBAC does not select its subjects. It **names** them. *"A RoleBinding or ClusterRoleBinding binds a role to subjects. Subjects can be group, users or ServiceAccounts"* [source: k8s-docs-rbac-depth-2026-08-31], and each is identified by a literal string: a username, a group name, a ServiceAccount name. There is no `subjectSelector`. You cannot write "everything labeled `team=payments`."

Why is the interesting question, and the documentation does not answer it, so here is the reading that makes sense of it.

<!-- AUTHOR-REVIEW: the docs state that subjects are named strings and never explain the design choice. The paragraphs below are the author's reasoning, not a sourced claim, and are marked as such in the prose. Flagging so a later stage does not attach a [source:] tag to them. -->

A selector is a *query*, evaluated continuously against a set that changes. That is a feature everywhere else in Kubernetes: a Deployment should pick up a Pod that starts matching, a Service should route to an endpoint that becomes ready. The set moving underneath you is the point.

Privilege is the one place where the set moving underneath you is a catastrophe. A grant defined by selector would silently expand the moment somebody added a label, and adding a label is one of the lowest-privilege operations in the entire system, something dozens of people and every controller in the cluster can do. You would have a permission system in which the answer to "who can read the production Secrets?" changed without anyone editing a permission, and could not be answered by reading the permission objects. Naming subjects means the list of who holds a grant is written down in the grant, and it changes only when somebody changes it.

> ⚓ **Worth Securing:** The general form of that argument shows up throughout security design: *dynamic membership is a feature for routing and a liability for authorization*. Cloud IAM systems that do support attribute-based group membership generally pair it with heavy audit tooling for exactly this reason, because the question "who currently has this?" stops being answerable by reading the policy. `[inferred]`

### The four default roles, and what each cannot do

Every cluster ships with four user-facing roles. Learning what each one *can* do is less useful than learning what each one *cannot*, because that is where the questions are.

**`cluster-admin`** — *"Allows super-user access to perform any action on any resource"* [source: k8s-docs-rbac-2026-08-23]. In a ClusterRoleBinding: everything, everywhere. In a RoleBinding: everything in that namespace, including the namespace object itself.

**`admin`** — intended to be granted within a namespace using a RoleBinding. *"If used in a RoleBinding, allows read/write access to most resources in a namespace, including the ability to create roles and role bindings within the namespace. This role does not allow write access to resource quota or to the namespace itself"* [source: k8s-docs-rbac-depth-2026-08-31]. So `admin` can delegate — it can make new Roles and bindings — but it cannot raise its own ceiling by editing the quota that constrains it.

**`edit`** — *"Allows read/write access to most objects in a namespace. This role does not allow viewing or modifying roles or role bindings"* [source: k8s-docs-rbac-2026-08-23]. That is the exam-relevant boundary: `edit` can run things, `edit` cannot re-grant. But read the rest of the documentation's own sentence, because it is doing something uncomfortable: *"However, this role allows accessing Secrets and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace"* [source: k8s-docs-rbac-depth-2026-08-31].

Sit with that. `edit` cannot edit RBAC, and it does not need to, because it can run a Pod as any ServiceAccount in the namespace, which means it can act with that account's permissions. The formal restriction is real and the practical ceiling is much higher. That is not a bug in `edit`; it is a fact about namespaces, and §4 is going to make it worse.

**`view`** — *"Allows read-only access to see most objects in a namespace. It does not allow viewing roles or role bindings. This role does not allow viewing Secrets, since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation)"* [source: k8s-docs-rbac-depth-2026-08-31].

`view` cannot read Secrets, and the documentation tells you exactly why: a Secret can be a credential, so reading Secrets is transitively the ability to *become* somebody. Remember this one specifically. §4 needs it in about ten minutes.

### Additive, with no deny

Chapter 11 gave this to you already, in its closing pages, as the tell for this chapter: the permission system you were about to learn has no way to say no. So this is a confirmation, not a reveal.

> *"Permissions are purely additive (there are no 'deny' rules)."* [source: k8s-docs-rbac-2026-08-23]

That is the whole rule, and it is one parenthetical in the documentation.

> **★ Fixed Point**
>
> **RBAC permissions are purely additive. There is no deny rule.** The effect of a subject's grants is the union of every rule in every role bound to them. Removing access means removing a grant — there is nothing else to do, and no rule you can write that subtracts.

> ⚠ **Navigational Hazards**
>
> Two things follow from the no-deny rule and both catch people.
>
> **You cannot carve an exception out of a grant.** If somebody holds `edit` in a namespace and you decide they should have everything `edit` gives except the ability to delete Deployments, there is no rule you can add to accomplish that. The only path is to stop granting `edit` and grant a narrower role you construct yourself. Any exam option offering a "deny" rule, a "deny" verb, or a rule that removes a permission is wrong on its face.
>
> **And a binding cannot be retargeted.** *"After you create a binding, you cannot change the Role or ClusterRole that it refers to"* [source: k8s-docs-rbac-2026-08-23]. If a RoleBinding points at the wrong role, you delete it and create a new one. That is a different operation with different consequences: a window during which the subject holds nothing, and, under a system that reconciles a cluster against a repository, a delete-and-create rather than an update. *[cross-bearing: see Ch 15 §5 — ordering the sync]*

### Escalation prevention, and least privilege

One more mechanism, because it explains a class of error message.

*"The RBAC API prevents users from escalating privileges by editing roles or role bindings. Because this is enforced at the API level, it applies even when the RBAC authorizer is not in use"* [source: k8s-docs-rbac-depth-2026-08-31].

Concretely: you can only create or update a role if you already have all the permissions it contains, at the same scope, *or* you have been granted the `escalate` verb on roles [source: k8s-docs-rbac-depth-2026-08-31]. And you can only create or update a binding if you already hold all the permissions in the referenced role, *or* you hold the `bind` verb on it [source: k8s-docs-rbac-depth-2026-08-31]. The example the documentation gives is exact: *"if `user-1` does not have the ability to list Secrets cluster-wide, they cannot create a ClusterRole containing that permission"* [source: k8s-docs-rbac-depth-2026-08-31].

Which means `admin`'s ability to create roles in its namespace is bounded by what `admin` itself holds. You cannot bootstrap yourself upward by writing a more generous role.

All of which is in service of one practice. *"Kubernetes RBAC is a key security control to ensure that cluster users and workloads have only the access to resources required to execute their roles"* [source: k8s-docs-rbac-good-practices-2026-08-31], and the documentation's general rules belong in one place [source: k8s-docs-rbac-good-practices-2026-08-31]:

- **Assign permissions at the namespace level where possible.** Use RoleBindings rather than ClusterRoleBindings to give rights only within a specific namespace.
- **Avoid wildcard permissions**, especially to all resources — *"providing wildcard access gives rights not just to all object types that currently exist in the cluster, but also to all object types which are created in the future."*
- **Do not use `cluster-admin` accounts except where specifically needed.**
- **Avoid adding users to the `system:masters` group.** Any member *"bypasses all RBAC rights checks and will always have unrestricted superuser access, which cannot be revoked by removing RoleBindings or ClusterRoleBindings."*

That last one deserves its own beat. `system:masters` membership is not an RBAC grant, so removing RBAC objects does not remove it. It is also invisible to any audit that reads RBAC objects. And if the cluster uses an authorization webhook, membership in that group bypasses the webhook too: requests from its members are never sent [source: k8s-docs-rbac-good-practices-2026-08-31].

> 🪢 **Mnemonic:** **Role says what. Binding says where. Subject says who.** Three objects, three questions, and every RBAC question you will be asked is one of those three in disguise.

You can check any of this from the command line: `kubectl auth can-i` queries the authorization layer directly to determine whether an action is permitted, and `--as` impersonates another principal, so an administrator can check what somebody else is allowed to do [source: k8s-docs-authorization-2026-08-31]. It is the fastest way to settle an argument about a grant, and it consults the real authorizer rather than your reading of the YAML.

---

## ☆ Taking Your Bearings #1

Five questions covering §1 through §3. Take them before continuing — the sections that follow assume you have this.

**1.** A cluster administrator enables encryption at rest for API objects stored in etcd. On the lifecycle-phase map and the 4Cs layer map, where does this control sit?

A) Distribute phase; Container layer
B) Runtime phase (storage); Cloud shading into Cluster layer
C) Runtime phase (storage); Container layer
D) Deploy phase; Cluster layer

**2.** A Pod is created in the `payments` namespace with no `serviceAccountName` field. The Pod starts successfully and its application immediately tries to list the Pods in its own namespace. What happens, and why?

A) The request succeeds — a Pod's own namespace is always readable by its ServiceAccount
B) The Pod fails to start, because no ServiceAccount was named
C) Authentication fails, because the `default` ServiceAccount has no token
D) Authentication succeeds and authorization fails, because the `default` ServiceAccount holds only API discovery permissions

**3.** *[retrieval: ch4]* Your team needs a group of engineers to be able to read `PersistentVolume` objects — which are cluster-scoped — as part of a read-only permission set you want to reuse. Which combination of objects does this call for, and what forces the choice?

A) A Role in each namespace where the engineers work, bound by a RoleBinding in each — Roles are the correct object for a team-scoped grant
B) A ClusterRole, bound by a RoleBinding in each namespace where the engineers work
C) A ClusterRole, bound by a ClusterRoleBinding — because the cluster-scoped resource forces the ClusterRole, and a permission over a resource that is in no namespace cannot be scoped to one
D) Either A or B, depending on how many namespaces are involved

**4.** A RoleBinding in the `staging` namespace currently references the ClusterRole `edit`. You need it to reference `view` instead. What do you do?

A) Update the RoleBinding's `roleRef` field with `kubectl edit`
B) Delete the RoleBinding and create a new one referencing `view`
C) Add a second RoleBinding referencing `view`; the more restrictive one wins
D) Patch the ClusterRole `edit` to remove write verbs

**5.** Which of the following is true of the default roles?

A) `view` can read Secrets but cannot modify them; `edit` cannot read Secrets at all
B) `edit` can create Roles and RoleBindings in its namespace; `admin` cannot
C) `view` cannot read Secrets, and `edit` cannot view or modify roles or role bindings
D) `cluster-admin` always confers cluster-wide power regardless of which binding object references it

---

**Answers with Explanations:**

**1. B.** Encryption at rest for API objects is squarely in the runtime phase's **storage** area; the documentation's runtime/storage list names "enable encryption at rest for API objects" directly [source: k8s-docs-cloud-native-security-2026-08-23]. On the layer map it starts at Cloud, where the 4Cs page recommends the etcd disk be encrypted at rest *"since etcd holds the state of the entire cluster (including Secrets)"* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31], and extends into Cluster, where the API-object encryption is configured.

**A** is the position of image signing — both coordinates wrong, and worth recognizing as a pair.
**C** has the phase right and the layer wrong. The Container layer covers the image and what runs from it; etcd is neither. This is the error you make if you reason "it's a Kubernetes thing, so it must be Container."
**D** has the layer half-right and the phase wrong. The deploy phase is about restrictions on what can be deployed, who can deploy it, and where [source: k8s-docs-cloud-native-security-2026-08-23]; encryption at rest governs data already in the datastore, which is runtime. This is the error you make if you reason "an operator configures it, so it must be a deploy-time act."

The point of the question is that both coordinates are required and neither implies the other.

**2. D.** Every namespace gets a `default` ServiceAccount, and Kubernetes assigns it to any Pod that does not name one [source: k8s-docs-service-accounts-2026-08-23]. The Pod gets a valid, projected, rotating token, so **authentication succeeds**. But the `default` account gets no permissions beyond API discovery [source: k8s-docs-service-accounts-2026-08-23], so **authorization fails**. **A** is the widespread and wrong assumption that a Pod can read its own namespace. **B** confuses identity assignment with a scheduling or admission failure; the Pod runs fine. **C** is the common misdiagnosis: people see a 403 and go looking at the token. The token is fine. This is the Fixed Point in question form.

**3. C.** Work it from the boundary. `PersistentVolume` is cluster-scoped, so it lives in no namespace, so a Role — which *"always sets permissions within a particular namespace"* [source: k8s-docs-rbac-2026-08-23] — has nowhere to put the rule. The **ClusterRole is forced**. Then the second, independent question: where should the grant apply? A resource that is in no namespace cannot have a permission over it scoped to one, so the binding must be a ClusterRoleBinding.

**A** fails at the first question — it reaches for the object whose scope cannot hold the rule.
**B** is the trap, and it is the most instructive wrong answer here. A RoleBinding *can* reference a ClusterRole, and doing so is correct and common [source: k8s-docs-rbac-2026-08-23] — but it binds that ClusterRole into the RoleBinding's namespace, and the `PersistentVolume` rule has no namespace to land in. The result looks configured and grants nothing. This is the misconception that a ClusterRole bound by a RoleBinding does everything a ClusterRoleBinding would, just in one place.
**D** treats a structural constraint as a matter of scale. The number of namespaces is irrelevant; a cluster-scoped resource is not in any of them.

**4. B.** *"After you create a binding, you cannot change the Role or ClusterRole that it refers to"* [source: k8s-docs-rbac-2026-08-23]. **A** fails; the API rejects the change to `roleRef`. **C** is the deny-rule misconception wearing a different hat: bindings are additive, so a second binding referencing `view` would add nothing that `edit` did not already include and would certainly not restrict anything. **D** would change the meaning of `edit` for every subject in the cluster, which is a much larger blast radius than the problem calls for, and the API's escalation-prevention rules may well refuse it anyway.

**5. C.** Both halves are documented: `view` *"does not allow viewing Secrets"* [source: k8s-docs-rbac-depth-2026-08-31], and `edit` *"does not allow viewing or modifying roles or role bindings"* [source: k8s-docs-rbac-2026-08-23]. **A** inverts both, and its second half is specifically wrong in a way worth remembering: `edit` *does* have access to Secrets [source: k8s-docs-rbac-depth-2026-08-31]. **B** inverts the delegation boundary; `admin` can create roles and bindings in its namespace, `edit` cannot. **D** is the `cluster-admin` trap: in a RoleBinding it is scoped to that binding's namespace [source: k8s-docs-rbac-2026-08-23].

---

**How'd You Do?**

**5/5:** move on. §4 will land cleanly.

**3–4:** re-read the section behind each miss before continuing. This chapter's sections are near-independent arcs, so a gap here does not close itself later — it just stays a gap.

**0–2:** stop and re-read §3 in full before starting §4. Not a skim: the four objects, the derivation, and the negative space of the four default roles. §4's central argument is built directly on the default roles and the additive rule, and it will read as a list of unrelated cautions without them.

---

**Checkpoint: You've Now Mastered**

✓ Placing a control on both the phase map and the layer map
✓ The separation of identity from permission, and what the `default` ServiceAccount proves
✓ Deriving the four RBAC objects from the namespaced/cluster-scoped boundary
✓ Additive permissions, no deny rule, and binding immutability
✓ The negative space of the four default roles

Three sections down. Next: the object you were told, eight chapters ago, did not ship with a lock fitted.

---

## 🔵 §4 — Secrets Are Not Encrypted

Chapter 4 introduced Secrets and did something unusual. It told you the object was not what it appeared to be, and then explicitly declined to fix it: *the lock is Chapter 12's; this chapter is only telling you the box did not ship with one fitted.* *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*

So this section is not going to re-alarm you. You have been appropriately alarmed since Chapter 4. This is the part where we say what to do about it.

### What you already hold

Two things, both from earlier chapters, both correct, both worth restating in one line each.

**Base64 is encoding.** *"Base64 encoding is not an encryption method, it provides no additional confidentiality over plain text"* [source: k8s-docs-secrets-good-practices-2026-08-24]. That is the documentation's own sentence and Chapter 4 gave you the same fact. Nothing has changed. Anyone who can read the encoded string can decode it, and there is no key involved because there is no cipher involved.

**Secrets get some handling ConfigMaps do not.** A Secret is only sent to a node if a Pod on that node requires it; the kubelet stores its copy in a temporary filesystem (tmpfs) rather than on durable storage; and once the Pods that depend on it are deleted, the local copies are removed [source: k8s-docs-secret-risks-2026-08-31]. Chapter 11 told you about the tmpfs part when it walked volume types, and said explicitly that you were being handed half an argument. *[cross-bearing: see Ch 11 §1 — three lifetimes, and the volumes that have them]* We will finish that argument shortly.

### The claim, and the three ways in

The whole problem, in the documentation's own words:

> **"Kubernetes Secrets are, by default, stored unencrypted in the API server's underlying data store (etcd). Anyone with API access can retrieve or modify a Secret, and so can anyone with access to etcd. Additionally, anyone who is authorized to create a Pod in a namespace can use that access to read any Secret in that namespace; this includes indirect access such as the ability to create a Deployment."** [source: k8s-docs-secret-2026-08-23]

Three sentences, three routes to the same object.

**Route one: API access.** Anyone the authorization layer permits to `get` a Secret reads it. That is the obvious one and the one an RBAC review catches. It is broader than `get`, though, and the documentation is explicit: *"`list` and `watch` access also effectively allow for users to reveal the Secret contents. For example, when a List response is returned (for example, via `kubectl get secrets -A -o yaml`), the response includes the contents of all Secrets"* [source: k8s-docs-rbac-good-practices-2026-08-31]. A grant of `list` on Secrets is a grant of read on every Secret in scope, and it does not look like one.

**Route two: etcd access.** Anyone who can read the etcd data store reads every Secret in the cluster, because that is where they are, unencrypted. This is where Chapter 8's backup guidance comes due. When Chapter 8 told you to back up etcd and to keep the backup encrypted, the encryption clause was not general caution — *[cross-bearing: see Ch 8 §7 — the one backup that matters]* **a backup of etcd is a copy of every Secret in the cluster, in the clear, sitting in whatever storage you put backups in.** Every password, every token, every TLS private key, in one file, protected by exactly whatever protects your backups. That is why the clause is in the sentence.

**Route three: the ability to create a Pod.** And this is the one nobody counts as a permission to read secrets.

The RBAC good-practices page states it in full: *"Permission to create workloads (either Pods, or workload resources that manage Pods) in a namespace implicitly grants access to many other resources in that namespace, such as Secrets, ConfigMaps, and PersistentVolumes that can be mounted in Pods. Additionally, since Pods can run as any ServiceAccount, granting permission to create workloads also implicitly grants the API access levels of any service account in that namespace"* [source: k8s-docs-rbac-good-practices-2026-08-31].

The mechanism is not subtle once you see it. A Pod spec can mount any Secret in its namespace. If you can create a Pod, you can create a Pod that mounts the Secret and prints it. You never asked for `get secrets`. You do not have `get secrets`. You have `create pods`, which is a permission everybody who deploys anything holds, and it is transitively equivalent.

And the second half is worse: because a Pod can name any ServiceAccount in the namespace, whoever can create Pods can act as any identity in that namespace. That is where §3's uncomfortable sentence about `edit` came from, and now you can see the full shape of it.

> **★ Fixed Point**
>
> **A Secret is stored unencrypted in etcd by default.** Encryption at rest is opt-in, and it is a cluster-operator decision made in the API server's configuration — not a field you can set on a manifest.

> **★ Fixed Point**
>
> **Anyone authorized to create a Pod in a namespace can read every Secret in that namespace** — including indirectly, by creating a Deployment, and including by running as any ServiceAccount that namespace holds.

> ⚠ **Navigational Hazards**
>
> This is the most consequential practical fact in the chapter, and the most invisible.
>
> An RBAC audit that greps for `get secrets` and finds nobody holding it will report the Secrets as safe. It is reading the wrong permission. In a namespace where a dozen engineers hold permission to deploy, a dozen engineers can read every Secret, and no line in any Role says so.
>
> The documentation draws the only correct conclusion: *"namespaces should be used to separate resources requiring different levels of trust or tenancy. It is still considered best practice to follow least privilege principles and assign the minimum set of permissions, but **boundaries within a namespace should be considered weak**"* [source: k8s-docs-rbac-good-practices-2026-08-31].
>
> That last clause is the design guidance. If two things must not read each other's Secrets, they go in different namespaces. There is no arrangement of Roles inside a single namespace that achieves it, because the escalation path does not run through the Secret permissions at all.

Recall from §3, one section ago, that `view` cannot read Secrets precisely because reading a Secret can mean becoming a ServiceAccount [source: k8s-docs-rbac-depth-2026-08-31]. Put that next to what you just read and the design intent is coherent throughout: Kubernetes treats "can read Secrets" and "can act as anybody in this namespace" as nearly the same permission, and it is right to.

### Encryption at rest, and what it buys

So enable encryption at rest. This is the lock finally being fitted to the strongbox — and it is worth being exact about which door it closes.

*"All of the APIs in Kubernetes that let you write persistent API resource data support at-rest encryption. For example, you can enable at-rest encryption for Secrets. This at-rest encryption is additional to any system-level encryption for the etcd cluster or for the filesystem(s) on hosts where you are running the kube-apiserver"* [source: k8s-docs-encrypt-data-2026-08-31]. And the default is unambiguous: *"By default, the API server stores plain-text representations of resources into etcd, with no at-rest encryption"* [source: k8s-docs-encrypt-data-2026-08-31].

The mechanism is a configuration file. *"The `kube-apiserver` process accepts an argument `--encryption-provider-config` that specifies a path to a configuration file. The contents of that file, if you specify one, control how Kubernetes API data is encrypted in etcd. If you are running the kube-apiserver without the `--encryption-provider-config` command line argument, you do not have encryption at rest enabled"* [source: k8s-docs-encrypt-data-2026-08-31]. The file holds an **`EncryptionConfiguration`** object in the `apiserver.config.k8s.io/v1` API group, naming the API kinds to encrypt and an ordered list of providers [source: k8s-docs-encrypt-data-2026-08-31].

One trap in the checking: even *with* the flag set, if the referenced file lists the `identity` provider first, you still do not have encryption enabled, because *"the default `identity` provider does not provide any confidentiality protection"* [source: k8s-docs-encrypt-data-2026-08-31]. A configuration file that looks configured is not the same as encryption that is on.

Note the scope carefully. *"This task covers encryption for resource data stored using the Kubernetes API. If you want to encrypt data in filesystems that are mounted into containers, you instead need to either: use a storage integration that provides encrypted volumes [or] encrypt the data within your own application"* [source: k8s-docs-encrypt-data-2026-08-31].

So the honest accounting of what encryption at rest gives you. It protects the object **as written to etcd**, which closes route two, the etcd-access and etcd-backup route, and closes it well. It does nothing whatsoever about routes one and three, because a caller the API server has authorized gets the object decrypted, in full, as normal. The lock is on the box; it says nothing about who is handed the box. That is not a shortcoming; it is the definition of the control. But an engineer who enables encryption at rest and believes the Secrets problem is now solved has closed one of three doors and stopped counting.

> 🔭 **Closer Look:** This is also the moment to draw a line you will need in a later chapter. **Encryption at rest and encryption in transit are separate decisions with separate mechanisms.** At rest is about bytes sitting in storage. In transit is about bytes moving across a network: TLS between components, and, at the workload layer, mutual TLS between services. Enabling one says nothing about the other. *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*

### The four hardening steps

Chapter 4 enumerated four things and deferred all of them. Here they are, in the documentation's own ordering:

> In order to safely use Secrets, take at least the following steps: **enable Encryption at Rest for Secrets; enable or configure RBAC rules with least-privilege access to Secrets; restrict Secret access to specific containers; consider using external Secret store providers.** [source: k8s-docs-secret-2026-08-23]

**Encryption at rest** we have just covered.

**Least-privilege RBAC on Secrets specifically.** The good-practices page gets granular: *"Components: Restrict `watch` or `list` access to only the most privileged, system-level components. Only grant `get` access for Secrets if the component's normal behavior requires it. Humans: Restrict `get`, `watch`, or `list` access to Secrets. Only allow cluster administrators to access `etcd`. This includes read-only access"* [source: k8s-docs-secrets-good-practices-2026-08-24]. And it adds an etcd management practice: consider wiping or shredding the durable storage etcd used once it is no longer in use, and configure encrypted TLS between etcd instances to protect Secret data in transit between them [source: k8s-docs-secrets-good-practices-2026-08-24].

**Restrict access to specific containers.** *"If you are defining multiple containers in a Pod, and only one of those containers needs access to a Secret, define the volume mount or environment variable configuration so that the other containers do not have access to that Secret"* [source: k8s-docs-secrets-good-practices-2026-08-24]. A Pod is not a trust boundary between its own containers unless you make it one. A sidecar you did not write and do not fully control sits inside the Pod's boundary; whether it can read the database password is a choice you make in the manifest.

**External secret store providers.** *"You can use third-party Secrets store providers to keep your confidential data outside your cluster and then configure Pods to access that information. The Kubernetes Secrets Store CSI Driver is a DaemonSet that lets the kubelet retrieve Secrets from external stores, and mount the Secrets as a volume into specific Pods that you authorize to access the data"* [source: k8s-docs-secrets-good-practices-2026-08-24]. Note the shape of that: a CSI driver *[cross-bearing: see Ch 11 §5 — who actually provides the storage]* delivered as a DaemonSet *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]*, doing a job through two interfaces you already know.

And one more, aimed at you rather than the cluster: *"If you configure a Secret through a manifest, with the secret data encoded as base64, sharing this file or checking it in to a source repository means the secret is available to everyone who can read the manifest"* [source: k8s-docs-secrets-good-practices-2026-08-24]. Base64 in a Git repository is a plaintext password in a Git repository with a costume on.

### File over environment variable

Chapter 11 handed you half an argument and told you it was half. Time to say which half and supply the rest.

**The half you hold:** the kubelet stores a Secret's local copy in tmpfs, memory-backed rather than durable storage, and removes it when the Pods depending on it are deleted [source: k8s-docs-secret-risks-2026-08-31]. That is a real property of the mount path.

**The half you were owed:** a mounted Secret stays current, and an environment variable does not. When a Secret is mounted as a volume, updates propagate to the Pod automatically, with one documented exception: *"A container using a Secret as a subPath volume mount does not receive automated Secret updates"* [source: k8s-docs-secret-risks-2026-08-31]. An environment variable, by contrast, is read at container start and is then a fixed string in the process's environment for the life of that process. Rotate the Secret and the running container keeps using the old value until something restarts it.

Add the third-container point from the hardening list — per-container mount control is expressible either way, but a volume mount is the more natural place to express it [source: k8s-docs-secrets-good-practices-2026-08-24] — and you have the argument.

<!-- AUTHOR-REVIEW: the widely-repeated claim that environment variables specifically leak into logs, `kubectl describe` output, and child processes is NOT stated anywhere in the cached kubernetes.io corpus; the search for it is recorded in k8s-docs-secret-risks-2026-08-31. The paragraph below therefore deliberately does not make that claim. If the author wants it, it needs a source or an [inferred] tag. -->

What the argument is *not*: a claim that environment variables leak somewhere volumes do not. You will read that in a great deal of prep material and it is plausible, but the Kubernetes documentation does not say it. What the documentation does say is symmetrical between the two mechanisms: *"Applications still need to protect the value of confidential information after reading it from an environment variable or volume. For example, your application must avoid logging the secret data in the clear or transmitting it to an untrusted party"* [source: k8s-docs-secrets-good-practices-2026-08-24]. That is a warning about your application's handling, and it applies to both.

So: prefer the file mount, on the grounds of rotation and tmpfs, and be precise about why. It is a better recommendation for being accurately argued.

### Secret types

Secrets carry a type, and the type tells consumers what shape of data to expect [source: k8s-docs-secret-2026-08-23]:

| Built-in type | Usage |
|---|---|
| `Opaque` | arbitrary user-defined data (the default) |
| `kubernetes.io/service-account-token` | ServiceAccount token — the **legacy** long-lived credential |
| `kubernetes.io/dockercfg` | serialized `~/.dockercfg` file |
| `kubernetes.io/dockerconfigjson` | serialized `~/.docker/config.json` file |
| `kubernetes.io/basic-auth` | credentials for basic authentication |
| `kubernetes.io/ssh-auth` | credentials for SSH authentication |
| `kubernetes.io/tls` | data for a TLS client or server |
| `bootstrap.kubernetes.io/token` | bootstrap token data |

Two of those connect to material you already have. `kubernetes.io/dockerconfigjson` holds a serialized `~/.docker/config.json` [source: k8s-docs-secret-2026-08-23], which is precisely what a workload needs for *"authenticating to a private image registry using an imagePullSecret"* [source: k8s-docs-service-accounts-2026-08-23]. Chapter 2 introduced pull secrets and flagged that they are a genuine security boundary rather than a convenience feature *[cross-bearing: see Ch 2 §6 — when Kubernetes pulls, and when it doesn't]*, and §7 will pick that up as the last checkpoint in the supply chain. And `kubernetes.io/service-account-token` is the legacy credential §2 warned you about.

A closing note for the next chapter: a Pod that references a Secret which does not exist does not get a running container. The kubelet cannot assemble the container's configuration, so the container sits waiting rather than starting and crashing — a recognizably different shape from a Pod that runs and then dies, and one of the first things to check when a Pod never comes up. *[cross-bearing: see Ch 13 §2 — pods that never start]*

<!-- AUTHOR-REVIEW: the missing-Secret startup behaviour above is not stated on any page in this chapter's corpus — the Secret concept page, the Secret risks page and the Secrets good-practices page were all checked and none of them describes what happens when a referenced Secret is absent. The wording has been kept deliberately non-specific (no reason string, no phase name) for that reason. Ch 13 §2 is planned to grade on this and The Voyage Ahead hands it forward, so it should be sourced before Ch 13 drafts: recommend the Secrets page's "Using a Secret" section or the Pod lifecycle documentation. -->

---

## 🔵 §5 — What a Pod May Do to Its Node

Chapter 10 drew you two axes and filled in one of them. NetworkPolicy governs which Pod may open a connection to which Pod: reachability, workload to workload. The other axis, it said, was what a Pod may do to the machine it is running on, and it was Chapter 12's. Chapter 11 pointed at the same place twice: once when it warned you about `hostPath` and called this *the workload-to-host boundary problem, and why an entire security apparatus exists to police it*, and once when it insisted that a volume access mode is not a permission system.

This is that axis, and that apparatus. It is also the boundary the chapter's title is actually about. Everything else here arranges who may ask the API for what; this section is about what a workload can do to the deck it is standing on.

You have in fact already seen the word. Chapter 11 quoted the storage documentation verbatim: *"it does not prevent an application from writing to the mounted volume if the Pod's securityContext allows write access."* You met `securityContext` inside a sourced quotation, doing exactly the job this section is about, with a pointer attached. Now it gets defined.

<!-- AUTHOR-REVIEW: the Ch 11 sentence re-quoted above is verbatim documentation, but no persistent-volumes snapshot is in this chapter's source set — the citation lives in Ch 11's corpus. Re-quoted documentation should carry its tag on every appearance. Recommend pulling Ch 11's access-modes snapshot into this chapter's set, or attributing the quote to Ch 11 explicitly rather than to "the storage documentation." -->

### The default position

Start with the uncomfortable baseline, because everything here is a departure from it.

A container is a process in a set of Linux namespaces and cgroups, sharing the host's kernel *[cross-bearing: see Ch 2 §1 — what a container actually is]*. That gives it an isolated *view*: its own filesystem, its own process table, its own network stack. It does not give it a different kernel or, by default, a different user database.

The Kubernetes documentation's own recommendation says so by implication: *"When you deploy a workload in Kubernetes, use the Pod specification to restrict that workload from running as the root user on the node"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. Note the phrasing — *root user on the node*, not "root in the container." The documentation treats those as the same thing, and the feature that separates them exists precisely because they otherwise are not separate: `hostUsers: false` lets you *"run containers as root users in the user namespace, but as non-root users in the host namespace on the node"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. Absent that, a process running as root inside a container is running as **UID 0 against the host's kernel**. The isolation is real and it is not the same thing as being unprivileged.

### The field

*"A security context defines privilege and access control settings for a Pod or Container"* [source: k8s-docs-security-context-2026-08-31]. The settings include, per the documentation's own list [source: k8s-docs-security-context-2026-08-31]:

- **Discretionary Access Control** — permission to access an object, like a file, based on user ID (UID) and group ID (GID).
- **SELinux** — objects assigned security labels.
- **Running as privileged or unprivileged.**
- **Linux Capabilities** — *"Give a process some privileges, but not all the privileges of the root user."*
- **AppArmor** — *"Use program profiles to restrict the capabilities of individual programs."*
- **Seccomp** — *"Filter a process's system calls."*
- **`allowPrivilegeEscalation`** — *"Controls whether a process can gain more privileges than its parent process. This bool directly controls whether the `no_new_privs` flag gets set on the container process."*
- **`readOnlyRootFilesystem`** — *"Mounts the container's root filesystem as read-only."*

### Two scopes, and which wins

`securityContext` appears in two places, and the relationship between them is exactly the sort of detail an exam is built on.

At **Pod scope**: *"To specify security settings for a Pod, include the `securityContext` field in the Pod specification. The `securityContext` field is a PodSecurityContext object. The security settings that you specify for a Pod apply to all Containers in the Pod"* [source: k8s-docs-security-context-2026-08-31].

At **container scope**: *"Security settings that you specify for a Container apply only to the individual Container, and they override settings made at the Pod level when there is overlap. Container settings do not affect the Pod's Volumes"* [source: k8s-docs-security-context-2026-08-31].

> 🪝 **Snag:** **The container's setting wins where both are set.** Pod scope is the default for everything in the Pod; container scope is a per-container override. And the tail of that sentence matters too: container settings do not affect the Pod's Volumes, so volume ownership behavior (`fsGroup`, for instance) is a Pod-level concern only.

Concretely at Pod scope: `runAsUser` specifies that all processes in any container run with a given user ID; `runAsGroup` specifies the primary group ID, and *"if this field is omitted, the primary group ID of the containers will be root(0)"*; `fsGroup` makes all container processes part of a supplementary group and sets the owner group for mounted volumes and files created in them [source: k8s-docs-security-context-2026-08-31]. That `runAsGroup` default is worth noticing: omitting it does not mean "no group," it means group 0.

### Capabilities

*"With Linux capabilities, you can grant certain privileges to a process without granting all the privileges of the root user"* [source: k8s-docs-security-context-2026-08-31]. Linux divides root's authority into categories, so a process can hold the specific privilege it needs — binding a low port, changing file ownership — without holding the rest.

You add or drop them via the `capabilities` field in a container's `securityContext`. *"Without specifying a `capabilities` field, containers receive default capabilities"*, which the container runtime decides [source: k8s-docs-security-context-2026-08-31]. And a syntax detail that catches everyone once: *"Linux capability constants have the form `CAP_XXX`. But when you list capabilities in your container manifest, you must omit the `CAP_` portion of the constant. For example, to add `CAP_SYS_TIME`, include `SYS_TIME` in your list of capabilities"* [source: k8s-docs-security-context-2026-08-31].

### seccomp and AppArmor

Two Linux security modules, doing related but distinct jobs. The documentation names three common kernel features Kubernetes lets you configure: **seccomp** (filter which system calls a process can make), **AppArmor** (restrict the access privileges of individual programs), and **SELinux** (assign security labels to objects for more manageable policy enforcement) [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. Whether a feature is available depends on the node's operating system enabling it in the kernel [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].

**seccomp** operates at the syscall layer. *"Each capability has a set of system calls (syscalls) that a process can make. seccomp lets you restrict these individual syscalls. It can be used to sandbox the privileges of a process, restricting the calls it is able to make from userspace into the kernel"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. Container runtimes usually include a default seccomp profile, and Kubernetes can apply profiles loaded onto a node to your Pods and containers [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. In the manifest: `seccompProfile` with a `type` of `RuntimeDefault`, `Unconfined`, or `Localhost` [source: k8s-docs-security-context-2026-08-31].

The documentation's own advice about writing custom profiles is refreshingly blunt: *"seccomp is a low-level security configuration that you should only configure yourself if you require fine-grained control over Linux syscalls"*, with named risks — configurations breaking during application updates, attackers still exploiting vulnerabilities through allowed syscalls, and profile management becoming challenging at scale. The recommendation: *"Use the default seccomp profile that's bundled with your container runtime. If you need a more isolated environment, consider using a sandbox, such as gVisor"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].

**AppArmor** operates on programs and resources rather than syscalls. *"AppArmor is a Linux kernel security module that supplements the standard Linux user and group based permissions to confine programs to a limited set of resources… It is configured through profiles tuned to allow the access needed by a specific program or container, such as Linux capabilities, network access, and file permissions. Each profile can be run in either enforcing mode, which blocks access to disallowed resources, or complain mode, which only reports violations"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].

Enforcing versus complain. Hold that shape. §6 is about to do the same thing at a different layer, and recognizing the pattern will save you memorizing it twice.

The two modules differ in how they identify what they are protecting: *"AppArmor uses profiles to define access to resources. SELinux uses policies that apply to specific labels"*, and *"In AppArmor, you define resources using file paths. SELinux uses the index node (inode) of a resource to identify the resource"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. A node's OS typically ships one or the other [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].

### Privileged containers

And now the field that undoes all of it.

*"Any container in a Pod can enable Privileged mode if you set the `privileged: true` field in the `securityContext` field for the container"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. What that does:

> *"Privileged containers override or undo many other hardening settings such as the applied seccomp profile, AppArmor profile, or SELinux constraints. Privileged containers are given all Linux capabilities, including capabilities that they don't require. For example, a root user in a privileged container might be able to use the `CAP_SYS_ADMIN` and `CAP_NET_ADMIN` capabilities on the node, bypassing the runtime seccomp configuration and other restrictions."* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]

Specifically: privileged containers run as the `Unconfined` seccomp profile, overriding any profile you specified; they ignore any applied AppArmor profiles; and they run as the `unconfined_t` SELinux domain [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].

> ⚠ **Navigational Hazards**
>
> `privileged: true` is not one more setting alongside the others. It is the setting that turns the others off.
>
> The Pod Security Standards define their most permissive level, `privileged`, as *"an absence of restrictions"* — a policy that *"is defined by an absence of restrictions"* and under which a Pod *"is able to bypass typical container isolation mechanisms (for example, access the node's host network)"* [source: k8s-docs-pod-security-standards-2026-08-23]. That is the documentation's own characterization and it needs no editorializing.
>
> The guidance is correspondingly direct: *"In most cases, you should avoid using privileged containers, and instead grant the specific capabilities required by your container using the `capabilities` field in the `securityContext` field. Only use privileged mode if you have a capability that you can't grant with the securityContext"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].
>
> And one consequence that belongs to §4 as much as here: **a container running with `privileged: true` can access all Secrets on that node** [source: k8s-docs-secret-risks-2026-08-31]. Not its namespace's Secrets. The node's. Every Secret that the kubelet has mounted for any Pod scheduled there.

> ⚓ **Worth Securing:** The RBAC good-practices page connects this back to who is allowed to create workloads at all: *"Users who can run privileged Pods can use that access to gain node access and potentially to further elevate their privileges"* [source: k8s-docs-rbac-good-practices-2026-08-31]. And it names the mitigation: where you do not fully trust a principal to create suitably secure Pods, enforce the Baseline or Restricted Pod Security Standard [source: k8s-docs-rbac-good-practices-2026-08-31]. Which is §6, and is why §6 comes next.

### The apparatus, not the field

The section's promise was an apparatus, so the rest of it: the controls that sit beside `securityContext` rather than inside it.

**Stronger isolation at the runtime layer.** If the shared-kernel model is not acceptable for a workload, you change the runtime rather than tuning the fields. The 4Cs page's Container-layer guidance is to *"select container runtime classes that provide stronger isolation"* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31], and the seccomp guidance points the same way: *"If you need a more isolated environment, consider using a sandbox, such as gVisor"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. That is Chapter 2's material and it is not re-taught here. *[cross-bearing: see Ch 2 §7 — not all isolation is equal]*

**Isolation at the placement layer.** Where a workload runs is a security control. The runtime/compute list says to *"partition workloads across different nodes to improve isolation"* [source: k8s-docs-cloud-native-security-2026-08-23], and the RBAC good-practices page is more specific: limit the number of nodes running powerful Pods, and *"avoid running powerful pods alongside untrusted or publicly-exposed ones. Consider using Taints and Toleration, NodeAffinity, or PodAntiAffinity to ensure pods don't run alongside untrusted or less-trusted Pods"* [source: k8s-docs-rbac-good-practices-2026-08-31]. Every mechanism in that sentence is Chapter 7's. *[cross-bearing: see Ch 7 §4 — when the berth refuses you]* Chapter 7 taught them as scheduling controls and told you they would come back as isolation controls. Here they are, unchanged, doing a different job.

**Avoid needing root at all.** *"Configuring the kernel security features on this page provides fine-grained control over the actions that processes in your cluster can take, but managing these configurations can be challenging at scale. Running containers as non-root, or in user namespaces if you need root privileges, helps to reduce the chance that you'll need to enforce your configured kernel security capabilities"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. The documentation's summarized recommendation: *"Unless necessary, run Linux workloads as non-root by setting specific user and group IDs in your Pod manifest and by specifying `runAsNonRoot: true`"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. There is also `hostUsers: false`, though the documentation notes it *"is still in early stages of development and might not have the level of support that you need"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].

**Watch what you assign.** One practical warning: *"Ensure that the user or group that you assign to the workload has the permissions required for the application to function correctly. Changing the user or group to one that doesn't have the correct permissions could lead to file access issues or failed operations"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. Setting `runAsUser: 1000` on an image built expecting root is a fast way to produce a container that starts and immediately fails on a permission error.

> **★ Fixed Point**
>
> **`securityContext` governs the workload-to-host axis. NetworkPolicy governs the workload-to-workload axis.** They are separate systems on separate objects at separate layers. They fail independently, and neither substitutes for the other: a Pod perfectly isolated by NetworkPolicy can still be `privileged: true` and read every Secret on its node.

Chapter 10 told you those were two axes. This section is the proof.

<!-- AUTHOR-REVIEW: this chapter's source set contains no NetworkPolicy snapshot, yet the Fixed Point above, §9's Zenith argument, Practice Q15 and Practice Q21 all rest on three NetworkPolicy claims: that it is additive with no deny rule, that it is implemented by a CNI plugin rather than the API server, and that it was designed against lateral movement in a flat network. Ch 10 carried those citations, and this chapter says so in prose, but the strongest single improvement available here is to pull Ch 10's NetworkPolicy snapshot into this chapter's set so §9 is verifiable in place. Recommended source: https://kubernetes.io/docs/concepts/services-networking/network-policies/ -->

---

## 🔵 §6 — Three Levels, Three Modes

Chapter 8 made you an unusually specific promise. It said that when you met Pod Security Admission four chapters later, *you will not be learning a new kind of thing. You will be learning one instance of the third gate.* *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*

So discharge that before anything else, because the derivation is the whole of what makes this section easy.

You already know that every request to the API server passes three gates in order: authentication, then authorization, then **admission**. Admission is the gate that inspects the object itself: after we know who you are and that you are allowed to do this in general, does this specific object pass the rules? Admission controllers are what run there, some compiled in and some reached by webhook.

**Pod Security Admission is a built-in admission controller.** That is the entire architectural statement. *"Kubernetes offers a built-in Pod Security admission controller to enforce the Pod Security Standards"* [source: k8s-docs-pod-security-admission-2026-08-31], stable since v1.25 [source: k8s-docs-pod-security-admission-2026-08-31]. Nothing new is happening. A Pod object arrives at the third gate, a controller examines it against a policy, and the gate does something about it.

What you need beyond that is the policy — three of them — and what "does something" means — three options. Hence the section title.

### The three levels

**The Pod Security Standards** define three policies covering the security spectrum. They are **cumulative** and range from highly permissive to highly restrictive [source: k8s-docs-pod-security-standards-2026-08-23].

| Profile | Description |
|---|---|
| **Privileged** | *"Unrestricted policy, providing the widest possible level of permissions. This policy allows for known privilege escalations."* |
| **Baseline** | *"Minimally restrictive policy which prevents known privilege escalations. Allows the default (minimally specified) Pod configuration."* |
| **Restricted** | *"Heavily restricted policy, following current Pod hardening best practices."* |

[source: k8s-docs-pod-security-standards-2026-08-23]

**Privileged** is *"purposely-open, and entirely unrestricted"*, aimed at system- and infrastructure-level workloads managed by privileged, trusted users [source: k8s-docs-pod-security-standards-2026-08-23]. Your CNI plugin's DaemonSet lives here, and legitimately so; it needs to configure the node's network.

**Baseline** is *"aimed at ease of adoption for common containerized workloads while preventing known privilege escalations"*, targeted at application operators and developers of non-critical applications [source: k8s-docs-pod-security-standards-2026-08-23]. Crucially, it allows the default minimally-specified Pod: a Pod spec with no `securityContext` at all passes Baseline.

**Restricted** is *"aimed at enforcing current Pod hardening best practices, at the expense of some compatibility"*, targeted at operators and developers of security-critical applications and at lower-trust users [source: k8s-docs-pod-security-standards-2026-08-23]. The "expense of some compatibility" is not a hedge: Restricted requires `runAsNonRoot: true` [source: k8s-docs-pod-security-standards-profiles-2026-08-31], and an image built to run as root cannot satisfy that without being changed.

The levels are the §5 fields with names on them. What each actually checks:

<!-- FIGURE: ch12-fig04-pod-security-standards-levels -->
```
   THE LEVELS — what gets checked
   ══════════════════════════════════════════════════════════════════

   securityContext field          privileged   baseline    restricted
   ──────────────────────────────────────────────────────────────────
   privileged: true               allowed      ✗ forbidden ✗ forbidden
   hostNetwork/hostPID/hostIPC    allowed      ✗ forbidden ✗ forbidden
   hostPath volumes               allowed      ✗ forbidden ✗ forbidden
   hostPort                       allowed      restricted  restricted
   capabilities.add               allowed      known list  only
                                                           NET_BIND_SERVICE
   capabilities.drop              —            —           must include ALL
   seccompProfile.type            allowed      not          RuntimeDefault
                                               Unconfined   or Localhost
   appArmorProfile.type           allowed      Runtime      Runtime
                                               Default or   Default or
                                               Localhost    Localhost
   allowPrivilegeEscalation       allowed      —           must be false
   runAsNonRoot                   —            —           must be true
   runAsUser                      any          any         must be non-zero
                                                           or unset
   volume types                   any          any         safe list only
                                                           (configMap, csi,
                                                           emptyDir, secret,
                                                           projected, pvc, …)

   cumulative — PERMITTED PODS:  privileged  ⊃  baseline  ⊃  restricted
                (restricted imposes every baseline requirement,
                 plus the rows below the line, so it admits fewer Pods)


   THE MODES — what happens when a check fails
   ══════════════════════════════════════════════════════════════════

           enforce  ──▶  the Pod is REJECTED
           audit    ──▶  recorded in the audit log; the Pod runs
           warn     ──▶  user-facing warning; the Pod runs


   APPLIED PER NAMESPACE, BY LABEL
   ══════════════════════════════════════════════════════════════════

           pod-security.kubernetes.io/<MODE>: <LEVEL>

   e.g.    pod-security.kubernetes.io/enforce: baseline
           pod-security.kubernetes.io/warn:    restricted
           pod-security.kubernetes.io/audit:   restricted

           ▲ all three, on one namespace, at two different levels.
             This is not a contradiction. It is a migration.
```

The rows in that figure are the Baseline and Restricted controls this chapter grades on, not the complete published list. Baseline forbids `privileged`, host namespaces (`hostNetwork`, `hostPID`, `hostIPC`), `hostPath` volumes, and unconfined seccomp; restricts `hostPort`, added capabilities to a known list, AppArmor and SELinux to approved values, `/proc` mount type to `Default`, and sysctls to a safe list. It also forbids Windows host access via `hostProcess` and, from v1.34, disallows direct host connections from probes and lifecycle hooks — two controls the figure omits because neither is Linux-workload material. Restricted adds every Baseline requirement plus: volumes limited to a safe list; `allowPrivilegeEscalation: false`; `runAsNonRoot: true`; `runAsUser` non-zero or unset; seccomp explicitly `RuntimeDefault` or `Localhost`; and capabilities dropping `ALL` with only `NET_BIND_SERVICE` addable back [source: k8s-docs-pod-security-standards-profiles-2026-08-31].

> 🔭 **Closer Look:** The Restricted capability rule rewards a precise reading: drop must include `ALL`, and add is limited to `undefined/nil` or `NET_BIND_SERVICE` [source: k8s-docs-pod-security-standards-profiles-2026-08-31]. `NET_BIND_SERVICE` is the exception because binding a port below 1024 is a common legitimate reason a container wants a scrap of root's authority, and refusing it would break otherwise-conformant images for no security gain.

There is no fourth level between Privileged and Baseline, and the FAQ explains why: *"The three profiles defined here have a clear linear progression from most secure (Restricted) to least secure (Privileged), and cover a broad set of workloads. Privileges required above the Baseline policy are typically very application specific, so we do not offer a standard profile in this niche"* [source: k8s-docs-pod-security-standards-profiles-2026-08-31].

### The three modes

The Standards are enforced by the built-in Pod Security Admission controller, which applies a policy **per namespace** via labels of the form `pod-security.kubernetes.io/<MODE>: <LEVEL>`, where MODE is **`enforce`** (violations are rejected), **`audit`** (violations are recorded in the audit log), or **`warn`** (violations trigger a user-facing warning), and LEVEL is `privileged`, `baseline`, or `restricted` [source: k8s-docs-pod-security-standards-2026-08-23].

> **Dead Reckoning:** Three levels: `privileged`, `baseline`, `restricted`. Three modes: `enforce`, `audit`, `warn`. They are applied to a namespace as labels of the form `pod-security.kubernetes.io/<MODE>: <LEVEL>`. A namespace may carry all three modes at once, at three different levels. The level names the policy to check against. The mode names what happens if the check fails.

<!-- AUTHOR-REVIEW: the claim that one namespace may carry all three mode labels simultaneously, at different levels, follows directly from the label grammar `pod-security.kubernetes.io/<MODE>: <LEVEL>` [k8s-docs-pod-security-standards-2026-08-23] but is not stated in so many words by any snapshot in this set. The Pod Security Admission snapshot (k8s-docs-pod-security-admission-2026-08-31) is TRUNCATED — it ends at the heading "Pod Security Admission labels for namespaces / The label form:" with the body missing — and that is exactly where the multi-label example lives. The migration argument below and Taking Your Bearings #2 question 4 both depend on it. Recommend re-fetching that snapshot in full, then tagging rather than rewriting. -->

> **★ Fixed Point**
>
> **Three levels × three modes, applied per namespace by label. The level says *what* is checked. The mode says *what happens* when the check fails.** They are independent axes. Confusing them is the most likely wrong answer in this chapter.

That independence is not a curiosity. It is the entire operational design. A cluster that wants to move to `restricted` sets `warn: restricted` and `audit: restricted` while keeping `enforce: baseline`. Nothing breaks. Developers see warnings when they submit non-conformant Pods and the audit log accumulates a list of exactly what would fail. When the list empties, you flip `enforce` to `restricted` and you already know it will hold. That is a migration path, expressible only because level and mode are orthogonal.

> 🪢 **Mnemonic:** **Level = what. Mode = when it hurts.** If an exam option describes `enforce` as a level or `restricted` as a mode, it is wrong at the grammar, before you get to the meaning.

### The namespace as a control surface

Notice what the label form implies. The unit of Pod Security policy is the **Namespace object**, which you have known since Chapter 4 as a scope for names and a boundary for namespaced resources. *[cross-bearing: see Ch 4 §3 — where a name lives]* Here it acquires a new job: it is the thing policy attaches to.

Which means the ability to label a namespace is a security-relevant permission. The RBAC good-practices page says so directly: *"Users who can perform patch operations on Namespace objects (through a namespaced RoleBinding to a Role with that access) can modify labels on that namespace. In clusters where Pod Security Admission is used, this may allow a user to configure the namespace for a more permissive policy than intended by the administrators"* [source: k8s-docs-rbac-good-practices-2026-08-31].

Patching a label is about as innocuous-looking as an operation gets. Here it is the ability to lower the security policy of everything deployed into that namespace. And the same paragraph notes the parallel case for NetworkPolicy: labels indirectly granting access an administrator did not intend [source: k8s-docs-rbac-good-practices-2026-08-31]. Two systems, same lever.

### PodSecurityPolicy

One clause, because you will meet it.

PodSecurityPolicy was the predecessor, and Pod Security Admission is what supersedes it. It is not the mechanism a current cluster uses, which makes its *absence* the load-bearing fact. If a question offers PodSecurityPolicy as a current mechanism, that is the distractor.

<!-- AUTHOR-REVIEW: the version in which PodSecurityPolicy was removed is deliberately NOT stated above. The Pod Security Admission snapshot declares `podsecuritypolicy-removed` in its concepts_covered frontmatter, but the snapshot body is truncated before any PSP text and contains none of it, so no source in this set supports a version number. Draft-v1 asserted "removed in Kubernetes 1.25" untagged, in two places; both have been softened to "superseded." Re-fetch k8s-docs-pod-security-admission-2026-08-31 in full, then restore the version if the page carries it. The Exam Alert trap row was softened to match. -->

### Two failure shapes, for later

Two things to carry forward.

A Pod refused by `enforce` **never starts**. It is not a Pod that starts and crashes; it is an object the API server declined to accept. That is a different diagnostic shape from anything in the crash-loop family, and it shows up at a different point in the triage flow. *[cross-bearing: see Ch 13 §2 — pods that never start]*

And a debug container is a container. In a namespace enforcing `restricted`, a debugging tool that tries to inject a container with elevated privileges can be refused by admission, which is a surprising thing to discover in the middle of an incident. *[cross-bearing: see Ch 16 §3 — getting inside, and adding what isn't there]*

---

## ☆ Taking Your Bearings #2

Five questions covering §4 through §6.

**1.** ⚠️ **This one is intentionally difficult.** Struggle is the point — it is the single most consequential practical question in the chapter, and getting it wrong here is much cheaper than getting it wrong on a cluster.

You are auditing a namespace called `payments`. You enumerate every Role, ClusterRole, RoleBinding and ClusterRoleBinding that touches it. No subject holds `get`, `list`, or `watch` on `secrets`. Eight engineers hold a custom `deployer` Role — `create`, `update`, `patch` and `delete` on `deployments`, `pods` and `services`, and nothing at all on `secrets` — bound by RoleBindings so they can ship. The Secrets in the namespace include the production database password.

Who can read that password, and what is the correct remediation?

A) Nobody — the audit is correct, since no subject holds any read verb on Secrets
B) Only cluster administrators, via etcd; enable encryption at rest to close it
C) All eight engineers, because permission to create workloads implicitly grants access to Secrets in the namespace; the remediation is to move the Secret and its consumers into a separate namespace
D) All eight engineers, but only because `deployer` grants `delete` on `pods`; removing that one verb closes the path

**2.** A cluster operator enables encryption at rest for Secrets with an `EncryptionConfiguration`. Which of the following is now true?

A) A user with `get secrets` permission receives an encrypted blob they must decrypt client-side
B) An etcd backup no longer contains readable Secret values, but an authorized API caller still receives the Secret in the clear
C) Secrets mounted into containers are now encrypted on the container filesystem
D) The kubelet's tmpfs copy on each node is now encrypted too, since it is derived from the encrypted object

**3.** A Pod spec sets `securityContext.runAsUser: 2000` at Pod scope. One of its two containers sets `securityContext.runAsUser: 3000` at container scope. What UID does each container's processes run as?

A) Both run as 2000; container-level settings are ignored for user IDs
B)B) Both run as 3000; the most restrictive setting applies to the whole Pod
C) The container with the override runs as 3000; the other runs as 2000
D) The Pod fails admission, because conflicting `runAsUser` values are rejected

**4.** A namespace carries these three labels:

```
pod-security.kubernetes.io/enforce: baseline
pod-security.kubernetes.io/warn: restricted
pod-security.kubernetes.io/audit: restricted
```

A developer submits a Pod that sets no `securityContext` at all and mounts no host paths. What happens?

A) The Pod is rejected, because it does not meet `restricted`
B) The Pod is rejected, because `enforce: baseline` requires an explicit `securityContext`
C) The Pod is created, and the developer sees a warning that it does not meet `restricted`; a violation is also recorded in the audit log
D) The Pod is created silently, because `enforce` is the only mode that produces any output

**5.** *[retrieval: ch8]* Explain, in terms of a mechanism you already know, where Pod Security Admission sits in the processing of an API request — and name one consequence of that position.

A) It runs before authorization, so a Pod can be refused for its contents before the API server has decided whether the requester may create Pods at all
B) It runs during authorization, alongside RBAC, so a Pod can be refused either for who submitted it or for what it contains
C) It runs at the admission gate — the third and last of the three gates — so it inspects the Pod object itself, and a rejected Pod never enters the cluster at all
D) It runs after the Pod is scheduled but before the kubelet starts the container, so a rejected Pod appears briefly in `Pending`

---

**Answers with Explanations:**

**1. C.** All eight, and not through any Secret permission. *"Permission to create workloads (either Pods, or workload resources that manage Pods) in a namespace implicitly grants access to many other resources in that namespace, such as Secrets, ConfigMaps, and PersistentVolumes that can be mounted in Pods"* [source: k8s-docs-rbac-good-practices-2026-08-31]. Anyone who can create a Pod can create one that mounts the Secret and prints it. The documentation's own remediation is the one in C: *"namespaces should be used to separate resources requiring different levels of trust or tenancy… boundaries within a namespace should be considered weak"* [source: k8s-docs-rbac-good-practices-2026-08-31].

**A** is the audit finding, and it is the whole point of the question. The audit is not sloppy — it enumerated every object correctly and read the permission it was looking for accurately. It is reading a permission that is not the relevant one.
**B** identifies a real route (etcd) and a real control (encryption at rest) but misses the route that is actually open here. Encryption at rest does nothing about an authorized API caller [source: k8s-docs-encrypt-data-2026-08-31].
**D** gets the population right and the mechanism exactly backwards. The escalation runs through **create**, not `delete`: a Pod spec can mount any Secret in its namespace, so the operative permission is the one that lets you bring a new Pod into existence. Strip `delete` from `deployer` and all eight engineers can still read the password by tomorrow morning. This distractor exists because people instinctively police the destructive verbs.

**2. B.** Encryption at rest protects the object as written to etcd [source: k8s-docs-encrypt-data-2026-08-31]. It closes the etcd and etcd-backup route completely and does nothing to the API route. **A** inverts the boundary; decryption happens server-side, transparently. **C** is the scope error the documentation explicitly heads off: encrypting data in filesystems mounted into containers requires a storage integration providing encrypted volumes, or application-level encryption [source: k8s-docs-encrypt-data-2026-08-31]. **D** invents a chain of custody. The kubelet receives the decrypted Secret and places its copy in tmpfs [source: k8s-docs-secret-risks-2026-08-31]; tmpfs is a separate protection with a separate rationale (it is memory-backed and removed with the Pod), not a downstream effect of at-rest encryption.

**3. C.** *"Security settings that you specify for a Container apply only to the individual Container, and they override settings made at the Pod level when there is overlap"* [source: k8s-docs-security-context-2026-08-31]. Pod scope is the default; container scope overrides it, per container. **A** inverts precedence. **B** invents a "most restrictive wins" rule that does not exist, and note 3000 is not obviously more restrictive than 2000 anyway. **D** invents a validation that does not exist; this configuration is entirely ordinary.

**4. C.** Level and mode are independent axes, and a namespace may carry all three modes at different levels [source: k8s-docs-pod-security-standards-2026-08-23]. `enforce: baseline` is the gate that can reject, and *"Baseline… allows the default (minimally specified) Pod configuration"* [source: k8s-docs-pod-security-standards-2026-08-23], so a Pod with no `securityContext` passes it. `warn: restricted` and `audit: restricted` both fire, because the Pod does not meet Restricted (which requires `runAsNonRoot: true`, `allowPrivilegeEscalation: false`, capabilities dropping `ALL`, and an explicit seccomp profile [source: k8s-docs-pod-security-standards-profiles-2026-08-31]), but neither of those modes rejects anything. **A** reads `warn`'s level as though `warn` enforced. **B** inverts Baseline's defining property — allowing the minimally specified Pod is precisely what distinguishes it from Restricted; it is the one level that asks for nothing. **D** is wrong about `warn` and `audit` being silent, which is precisely their purpose.

**5. C.** Pod Security Admission is *"a built-in Pod Security admission controller"* [source: k8s-docs-pod-security-admission-2026-08-31], and admission is the third and last of the three gates. The consequence that matters: it inspects the object, so it can make decisions no authorization rule could. RBAC can say "this subject may create Pods," but only admission can say "not *this* Pod." And a rejected Pod is never created, so it has no phase, no events, and no logs.

**A** puts admission before authorization. It is a coherent-sounding design and it is not this one — the order is authentication, authorization, admission, and it matters: admission is only ever reached for a request that has already been authorized, so a subject with no `create pods` grant never gets far enough for a Pod Security check to be relevant.
**B** collapses two gates into one. RBAC and PSA answer different questions at different stages; authorization reasons about verb, resource and namespace, and cannot see the object's field values at all.
**D** is the plausible-sounding wrong answer: it describes something that would look like a Pod stuck in `Pending`, which is a genuinely different failure and one you will diagnose in a later chapter.

---

**How'd You Do?**

**5/5:** take the session break and start §7 fresh.

**3–4:** re-read the section behind each miss now, while the material is warm. Question 1 is the one to be least comfortable missing.

**0–2:** re-read §5 before you go on to re-read §6. The three levels are a list of `securityContext` fields with names attached, and they are unmemorable — genuinely unmemorable, not just difficult — if the fields themselves are not yet familiar. Fields first, then levels.

---

**Checkpoint: You've Now Mastered**

✓ The three exposure paths to a Secret, and which control closes which
✓ What encryption at rest protects and what it leaves open
✓ `securityContext` at two scopes, and which one wins
✓ Three levels against three modes, and why they are independent
✓ Pod Security Admission as one instance of a gate you already knew

That is the API and the workload. **This is the natural place to stop if you are splitting this chapter across two sessions.** What follows leaves the cluster entirely.

---

## 🟡 §7 — Trusting What You Ship

Everything so far has been about a running cluster: who may call the API, what a workload may do once it is there. This section is about the question that comes first and gets asked least: **is the thing you are running the thing you built?**

Chapter 2 raised this twice and deferred both times. It called reproducible layers *the hinge on which supply-chain verification swings*, and it flagged `imagePullSecrets` as *a genuine security boundary rather than a convenience feature*. Both arguments were made there. This section completes them rather than repeating them.

There is a way to organize this material as a roster of projects, and it is the wrong way. There are five or six well-known tools here and they are not alternatives to each other; they occupy different positions in a sequence. So we will walk the sequence and name the tools where they sit.

<!-- FIGURE: ch12-fig05-supply-chain-checkpoints -->
```
   OUTSIDE THE CLUSTER                              │   INSIDE
   ═════════════════════════════════════════════════╪═══════════
                                                    │
   BUILD ──▶ SCAN ──▶ SIGN ──▶ RECORD ──▶ RESTRICT ─┼─▶ VERIFY ──▶ RUN
     │         │        │         │          │      │      │
     │         │        │         │          │      │      │
     ▼         ▼        ▼         ▼          ▼      │      ▼
   image     known    binds     append-    private  │   admission
   +digest   vulns    to the    only log   registry │   controller
   +SBOM              DIGEST                        │
                        ▲                           │   ▲
     ┌──────────────────┴─────────────┐             │   │
     │  the artifact's identity —     │             │   │
     │  the same digest — is carried  │             │   │
     │  the whole length of the chain │             │   │
     └────────────────────────────────┘             │   │
                                                    │   │
   Harbor,          Cosign     Rekor    Harbor,     │  Kyverno,
   image scanners   Notation            imagePull-  │  Gatekeeper,
                    Fulcio              Secrets     │  Policy
                                                    │  Controller
                                                    │
   ◀── everything left of the line happened somewhere else,
       under somebody else's control, possibly months ago.
       VERIFY is the first checkpoint the cluster performs itself.
```

That vertical line is the point of the figure. Every step but one happens outside the cluster, in a build system you may not administer, at a time that is not now. Admission is the cluster's gangway: the one place it gets to inspect the cargo before it comes aboard. Which is why §8 follows this section rather than preceding it.

### Scan

*"As part of an image build step, you should scan your containers for known vulnerabilities"* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31], and the distribute-phase guidance says the same: scan container images and other artifacts for known vulnerabilities [source: k8s-docs-cloud-native-security-2026-08-23]. A **CVE** — Common Vulnerabilities and Exposures — is an identifier attached to a publicly disclosed vulnerability, and a scanner's job is to enumerate what an image contains and report which of those components have known vulnerabilities against them.

The Code layer's parallel recommendation belongs alongside it: *"It is a good practice to regularly scan your application's third party libraries for known security vulnerabilities"* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31]. Same activity, different layer. Your dependencies and the image's base OS packages are both other people's code.

<!-- AUTHOR-REVIEW: two gaps in this subsection. (1) No snapshot in this corpus expands CVE or describes the program; the Linux-kernel-constraints page cites CVE-2022-0185 and CVE-2019-5736 by number only, and the CNCF glossary index (checked 2026-08-31) has no CVE entry. The expansion above is carried because B7 assigns CVE to this section and the book's acronym-register convention requires expansion at first use, but it is not sourced — needs a cve.org fetch or a glossary entry. (2) No cached source describes image scanning as a *practice* beyond the two one-line recommendations quoted above (gap G22, partially open); Harbor's page names "Security and vulnerability analysis" as a feature without describing how scanning works. This subsection is deliberately thin as a result. If the author wants scanner mechanics (SBOM-driven vs filesystem-walking, registry-integrated vs CI-stage), it needs a fetch. Trivy was named in draft-v1's figure and appeared in no snapshot; it has been removed. -->

### Sign

A scan tells you what is *in* an image. A signature tells you *who produced it*, and the two are independent. A signed image can be full of known vulnerabilities; a clean image can come from anywhere.

*"Sign container images to maintain a system of trust for the content of your containers"* [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31].

**Sigstore** is the project most of this ecosystem now runs through. It *"empowers software developers and consumers to securely sign and verify software artifacts such as release files, container images, binaries, software bills of materials (SBOMs), and more"*, operating as a free, public-good service under the Open Source Security Foundation [source: sigstore-overview-2026-08-23]. Its components divide the job [source: sigstore-overview-2026-08-23]:

- **Cosign** — the client tool for signing and verifying artifacts, including container images.
- **Fulcio** — the code-signing certificate authority, which issues **short-lived certificates bound to a verified identity** rather than long-lived keys.
- **Rekor** — an **immutable, append-only transparency log** that records signing events for public audit.
- **Policy Controller** — enforces signature verification policies within Kubernetes, as an admission controller.

**Keyless signing** is what ties them together, and it removes the worst problem in signing. Conventionally, signing means holding a private key, which means protecting a private key forever, which means that the compromise of that key retroactively invalidates everything it ever signed. Sigstore's flow instead: a Cosign client creates an **ephemeral** key pair and requests a certificate from Fulcio using an OpenID Connect identity token; Fulcio validates the token and issues a short-lived certificate linking the public key to the verified identity; the artifact is signed; **the private key is discarded after a single signing**; and the signature and certificate are recorded in Rekor [source: sigstore-overview-2026-08-23].

The key exists for seconds and is then gone. What persists is the certificate binding a public key to an identity, and the log entry proving when. There is no long-lived secret to steal.

**Notary Project** is the other signing standard you will meet: *"a set of specifications and tools intended to provide a cross-industry standard for securing software supply chains"*, focused on *"signing and validating software artifacts, ensure they have not been tampered with and provide security policies to determine which validated artifacts are allowed to be used in your systems"*, with **Notation** as its CLI [source: notary-project-signing-digest-2026-08-31]. It is CNCF incubating [source: notary-project-signing-digest-2026-08-31].

### What a signature covers — and this is the one

Chapter 2 taught you that a tag is a mutable pointer and a digest is identity, and it taught it as a matter of build hygiene: pin your digests so you know what you deployed.

It was not hygiene. Here is the Notary Project's own statement of what happens at signing time:

> *"Notation resolves the tag to the digest before signing if a tag is used to identify the container image."*
>
> *"Always reference and use the image digest instead of a tag since digest is immutable."* [source: notary-project-signing-digest-2026-08-31]

Read the first sentence carefully. Even if you hand the tool a tag, it does not sign the tag. It resolves the tag to a digest and signs *that*. The signature has nothing to say about the tag at all.

> **★ Fixed Point**
>
> **A signature binds to a digest, not a tag.** Chapter 2 taught you that a tag is a mutable pointer and a digest is content identity, and framed it as build hygiene. It was not hygiene. It is the reason a signature means anything at all.

Think about what a tag-covering signature would even assert. "I attest that whatever `myapp:v2` happens to point at is trustworthy" — a statement about a name, which anyone with push access can repoint at any moment, retroactively extending your attestation to bytes you have never seen. It would be worse than no signature, because it would look like one.

A digest is a cryptographic hash of content. Signing it says: *these exact bytes, and no others.* That is the only form of the statement that survives contact with a mutable registry. *[cross-bearing: see Ch 2 §3 — registries, tags, and digests]*

> 🪢 **Mnemonic:** **You sign the bytes, not the label on the box.**

### Record

*"Use validation mechanisms such as digital certificates for supply chain assurance"* [source: k8s-docs-cloud-native-security-2026-08-23], and the transparency log is what makes those mechanisms auditable rather than merely present. Rekor is *"an immutable, append-only transparency log that records signing events for public audit and verification"* [source: sigstore-overview-2026-08-23]. Append-only means entries cannot be removed or altered after the fact, so "was this artifact signed, by whom, and when?" is a question with a durable answer, including for artifacts signed with keys that no longer exist — which under keyless signing is all of them.

### Attestation, provenance, and SBOMs

**Attestation** generalizes signing. A signature says "I vouch for these bytes." An attestation says "I vouch for this *claim* about these bytes": that they were built by a particular pipeline from a particular commit, that they passed a particular test suite, that they contain a particular set of components.

<!-- AUTHOR-REVIEW: the attestation gloss above is the author's, not a citation. Both in-toto-overview-2026-08-31 and notary-project-signing-digest-2026-08-31 list `attestation` in concepts_covered, and neither body defines it; the in-toto page additionally warns that supply-chain layout, link metadata and steps/inspections are not covered there and must not be described. Draft-v1 flagged the parallel SBOM case in a comment and did not flag this one — the asymmetry is now closed. Either source it (in-toto.io/docs, or the SLSA attestation spec) or mark the gloss [inferred] in prose. -->

**in-toto** is the framework for the build-process half. It *"is designed to ensure the integrity of a software product from initiation to end-user installation. It does so by making it transparent to the user what steps were performed, by whom and in what order"* [source: in-toto-overview-2026-08-31]. That sentence — *what steps, by whom, in what order* — is in substance what **provenance** means: not just what the artifact is, but the verifiable record of how it came to be. SPDX names the same idea directly, listing *"Provenance and Integrity: Tracking the origin and history of components, including checksums and cryptographic hashes"* among what its standard covers [source: sbom-standards-spdx-cyclonedx-2026-08-31]. in-toto is a CNCF graduated project [source: in-toto-overview-2026-08-31].

<!-- AUTHOR-REVIEW: the in-toto landing page does not itself use the word "provenance" (its own snapshot records this). The SPDX tag above carries the term; the in-toto tag carries the what-steps-by-whom-in-what-order sentence. Verify that split is acceptable, or add an [inferred] marker to the equation between them. -->

An **SBOM** — Software Bill of Materials — is the components half. A bill of materials is a standardized record of what a software artifact is made of. The two dominant standards are **SPDX**, from the Linux Foundation, *"an open standard designed to facilitate the communication of Bill of Materials (BOM) information across diverse domains, including software, artificial intelligence (AI), datasets, and system components"*, covering metadata for packages, files and snippets, licensing information, and provenance and integrity [source: sbom-standards-spdx-cyclonedx-2026-08-31]; and **CycloneDX**, from OWASP, *"a full-stack Bill of Materials (BOM) standard that provides advanced supply chain capabilities for cyber risk reduction"* [source: sbom-standards-spdx-cyclonedx-2026-08-31].

And an SBOM is itself an artifact that can be signed; Sigstore names SBOMs explicitly among the artifact types it handles [source: sigstore-overview-2026-08-23]. Which closes a loop: a signed SBOM is a verifiable claim about what is inside a verifiable image, and the two together are what lets you answer "are we affected by this newly disclosed vulnerability?" without rebuilding anything.

<!-- AUTHOR-REVIEW: no source in the corpus defines "SBOM" in a single canonical sentence. CISA and NTIA, which carry the canonical definitions, refused automated retrieval (HTTP 403, 2026-08-31) and the CNCF glossary has no SBOM entry (index checked). The description above is assembled from what SPDX and CycloneDX say their standards cover, which is defensible but is not a quoted definition. Flagging so a later stage does not attach a definition-shaped [source:] tag to it. Note also: draft-v1 carried the ISO/IEC 5962:2021 and ECMA-424 standardization details; these have been trimmed per the curriculum-alignment finding that §7 is over-covered relative to its recognition-depth allocation. Both facts are sourced in sbom-standards-spdx-cyclonedx-2026-08-31 if the author wants them restored. -->

**TUF** — The Update Framework — belongs here too, though it operates one level up. It is *"a framework for securing software update systems"* that *"maintains the security of software update systems, providing protection even against attackers that compromise the repository or signing keys"* [source: tuf-overview-2026-08-31]. The attacks it names are the ones a naive signature check misses entirely [source: tuf-overview-2026-08-31]:

- *"An attacker keeps giving you the same file, so you never realize there is an update."*
- *"An attacker gives you an older, insecure version of a file that you already have and tricks you into thinking it's newer."*
- *"An attacker gives you a newer version of a file you have but it's still not the newest one."*
- *"An attacker compromises the key used to sign these files. Now you download a file that is properly signed, but is still malicious."*

Every one of those involves a *correctly signed* artifact. That is what makes TUF interesting: signing answers "did this come from who I think?" and answers nothing about freshness, ordering, or key compromise. TUF is CNCF graduated [source: tuf-overview-2026-08-31].

### Restrict

The distribute-phase list ends with a step that is not cryptographic at all: *"restrict access to artifacts — place container images in a private registry that only allows authorized clients to pull images"* [source: k8s-docs-cloud-native-security-2026-08-23].

**Harbor** is the CNCF graduated registry built for this. Its stated mission is *"to be the trusted cloud native repository for Kubernetes"*, and it *"is an open source registry that secures artifacts with policies and role-based access control, ensures images are scanned and free from vulnerabilities, and signs images as trusted"* [source: harbor-overview-2026-08-31]. Its feature list names security and vulnerability analysis, content signing and validation, and identity integration with role-based access control [source: harbor-overview-2026-08-31]. Which is to say it does scan, sign and restrict in one place — a useful thing to know when a question offers it as an answer.

And the cluster's side of the restriction is a Secret. An `imagePullSecret` holds registry credentials in a Secret of type `kubernetes.io/dockerconfigjson`, which is a serialized `~/.docker/config.json` [source: k8s-docs-secret-2026-08-23], and one of the documented ServiceAccount use cases is *"authenticating to a private image registry using an imagePullSecret"* [source: k8s-docs-service-accounts-2026-08-23]. Chapter 2 told you this was a security boundary rather than a convenience. Now you can see the whole boundary: the registry refuses unauthorized pulls, the credential to pull is a Secret, and the rules about who can read Secrets from §4 apply to it in full.

### Verify

The last checkpoint, and the first one the cluster performs itself. The deploy phase says: *"You can enforce measures from the distribute phase, such as verifying the cryptographic identity of container image artifacts"* [source: k8s-docs-cloud-native-security-2026-08-23]. The 4Cs Container layer says: *"Image Signing and Enforcement"* — signing *and* enforcement, two words, two activities [source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31].

Signing without verification is theater. A signature that nothing checks is a file in a registry. The check happens at admission: Sigstore's Policy Controller *"enforces signature verification policies within Kubernetes as an admission controller"* [source: sigstore-overview-2026-08-23], and Kyverno can *"verify container images and metadata for software supply chain security"* [source: kyverno-overview-2026-08-23].

Which is the third gate again, doing a third job. Same position, different question. And it hands us straight into §8.

> ⚓ **Worth Securing:** The one-sentence version of this whole section: **a signature tells you where something came from, a scan tells you what is wrong with it, an SBOM tells you what is in it, provenance tells you how it was made, and none of the four does any of the others' work.** Every real supply-chain question is asking which of those you need.

---

## 🔵 §8 — Rules That Watch

Section 6 gave you a controller that answers one question extremely well. Pod Security Admission checks a Pod against three fixed policies, at the admission gate, and does so without configuration beyond a namespace label. That is its strength and its limit: it is not extensible. If your organization's rule is "every Pod must carry a `cost-center` label," or "no image may come from outside our registry," or "every Namespace gets a default-deny NetworkPolicy on creation," PSS has nothing to say about any of it.

A **policy engine** answers arbitrary questions at that same gate.

The CNCF glossary gives the underlying idea a name: **"Policy as Code is the practice of storing the definition of policies as one or more files in machine-readable and processable form"** [source: cncf-glossary-policy-as-code-2026-08-31]. Codified policy gets consistent automated enforcement instead of manual review, and, because the files live in version control, a change history you can audit and revert [source: cncf-glossary-policy-as-code-2026-08-31].

The organizing question for this section is not *which engine* but **when does the rule run?**

### At admission

**Kyverno** — Greek for "govern" — is *"a cloud native policy engine"* originally built for Kubernetes and now usable outside clusters as a unified policy language. It *"allows platform engineers to automate security, compliance, and best practices validation and deliver secure self-service to application teams"* [source: kyverno-overview-2026-08-23].

Its policies can *"validate, mutate, generate, or clean up Kubernetes resources; verify container images and metadata for software supply chain security; and be applied as a Kubernetes admission controller (webhook) or as a CLI-based scanner"* [source: kyverno-overview-2026-08-23]. Policies are written in YAML using declarative rules and CEL, managed as Kubernetes resources, and version-controlled with Git [source: kyverno-overview-2026-08-23].

Those four verbs are worth separating, because they are not variations on one thing:

- **Validate** — refuse an object that breaks a rule. This is what PSS does, generalized.
- **Mutate** — change an object as it passes. Add a missing label, inject a sidecar, set a default.
- **Generate** — create *other* objects in response. A new Namespace appears; a default NetworkPolicy and a ResourceQuota appear with it.
- **Clean up** — remove objects meeting a condition.

<!-- AUTHOR-REVIEW: kyverno-overview-2026-08-23 lists the four verbs and defines none of them. The four glosses above, and the examples attached to them, are the author's reading of standard policy-engine semantics rather than product documentation. Either open a small research gap for kyverno.io/docs/policy-types/ or mark the four glosses [inferred] in prose. -->

Validate and mutate map exactly onto a distinction Chapter 8 drew: validating and mutating admission webhooks. *[cross-bearing: see Ch 8 §2 — three gates and a logbook]* Chapter 8 gave you the two webhook types as an abstraction. **A policy engine is one.** It is what people actually install into that extension point, and it is the cleanest possible payoff for having learned the distinction. *[cross-bearing: see Ch 17 §4 — every place Kubernetes lets you in]*

**OPA** — Open Policy Agent — is the other widely used engine, a CNCF graduated project, with its **Gatekeeper** admission controller for Kubernetes, expressing policy in the **Rego** language [source: kyverno-overview-2026-08-23]. The Pod Security Standards page itself names the third-party enforcement options: Kubewarden, Kyverno, and OPA Gatekeeper [source: k8s-docs-pod-security-standards-profiles-2026-08-31], alongside a framing worth keeping — *"Decoupling policy definition from policy instantiation allows for a common understanding and consistent language of policies across clusters, independent of the underlying enforcement mechanism"* [source: k8s-docs-pod-security-standards-profiles-2026-08-31]. The Standards are a *definition*; PSA and the policy engines are *instantiations* of it. That is why a third-party engine can enforce the same three levels PSA does.

The practical difference between Kyverno and OPA Gatekeeper, at the level a KCNA candidate needs: Kyverno's policies are Kubernetes resources written in YAML and CEL; OPA's are written in Rego, a purpose-built policy language. Both sit at the admission gate. Choosing between them is a team decision about language and ecosystem, not a security-model decision.

### At runtime

Everything above happens before an object exists. **Falco** answers a different question at a different time.

Falco *"is a cloud native security tool that provides runtime security across hosts, containers, Kubernetes, and cloud environments. It is designed to detect and alert on abnormal behavior and potential security threats in real-time"*, and it is a CNCF graduated project, originally created by Sysdig [source: falco-overview-2026-08-23].

How it works: *"Falco observes Linux kernel events (system calls) and data from plugins, enriches them with metadata from the container runtime and Kubernetes, evaluates the event stream against a rules engine, and emits real-time alerts when rules detect violations"* [source: falco-overview-2026-08-23].

Its default detections read like a list of things you now know to worry about [source: falco-overview-2026-08-23]:

- privilege escalation via privileged containers
- namespace manipulation
- unauthorized modifications to sensitive directories such as `/etc` or `/usr/bin`
- suspicious network connections
- shell or SSH binary execution inside containers
- unauthorized file ownership or permission changes
- symlink creation

Look at the first one against §5. A `privileged: true` Pod that got past admission — because the namespace was `enforce: privileged`, or because it predates the policy, or because someone granted an exception — is invisible to every control in §6. Falco sees the behavior after the fact.

> ⚠ **Navigational Hazards**
>
> **Falco detects. It does not prevent.** It observes, evaluates, and emits alerts [source: falco-overview-2026-08-23]. There is no step in that sequence that blocks anything.
>
> This is the watch at the masthead, and it pays to be precise about what that is worth. A control that reports is not a lesser version of a control that refuses; it answers a question refusal cannot. Admission-time controls can only reason about the object as submitted; they know nothing about what the process does at hour six. Runtime detection knows nothing about the object and everything about the behavior. You want both, and an exam question distinguishing them is asking whether you know they are different questions rather than different qualities of answer.

### The two positions, side by side

| | admission time | runtime |
|---|---|---|
| **What it examines** | the object, as submitted | process behavior, as it happens |
| **When** | before the object exists | after it is running |
| **What it can do** | refuse, or change | observe, and report |
| **Fixed question** | Pod Security Admission | — |
| **Arbitrary question** | Kyverno, OPA/Gatekeeper | Falco |

Three ways of covering the same territory: PSS answers a fixed question at the gate; a policy engine answers an arbitrary question at the same gate; Falco answers a different question entirely, later, and answers it by telling you rather than by stopping you.

<!-- AUTHOR-REVIEW: eBPF is deliberately not named here. B7 rules it glossary-only and not eligible for graded text, and the Falco source describes the mechanism as kernel events and syscalls without needing the word. -->

---

## ☆ Taking Your Bearings #3

Five questions covering §7 and §8, plus one deliberate long-spacing item back to §3.

**1.** *[retrieval: ch2]* A build pipeline signs the image reference `registry.example.com/myapp:v2`. Three weeks later, an attacker with push access to the registry pushes different content to that same tag. A cluster verifies signatures at admission. What happens when the new content is pulled, and why?

A) Verification passes, because the tag `v2` was signed and it is still `v2`
B) Verification fails, because the signature bound to the digest of the original content, and the new content has a different digest
C) Verification passes only if the attacker also re-signed; otherwise the image is pulled unverified
D) Verification is not possible, because signatures cannot be applied to tagged references at all

**2.** Put these supply-chain checkpoints in the order they occur, and identify which is the first one performed by the cluster itself: scan, verify, sign, restrict, record.

A) sign → scan → record → verify → restrict; the cluster performs *restrict*
B) scan → sign → record → restrict → verify; the cluster performs *verify*
C) scan → record → sign → verify → restrict; the cluster performs *verify*
D) scan → sign → record → restrict → verify; the cluster performs *restrict*

**3.** Your cluster already enforces the `baseline` Pod Security Standard in every namespace. Your organization now requires that every Pod carry a `cost-center` label, and that any Pod missing one be rejected. What do you reach for, and why can't Pod Security Admission do it?

A) Add a fourth Pod Security level; PSA supports custom levels via ConfigMap
B) A policy engine such as Kyverno or OPA Gatekeeper, because PSA evaluates only the fixed Pod Security Standards and cannot express an arbitrary rule
C) Falco, because it evaluates arbitrary rules against cluster objects
D) An RBAC rule denying `create` on Pods without the label; PSA is for `securityContext` only

**4.** A container in your cluster has been running for six hours. During hour six, a process inside it spawns a shell and writes to `/etc`. Which tool in this chapter is positioned to tell you, and what specifically will it do about it?

A) Pod Security Admission — it will terminate the Pod
B) A Kyverno validating policy — it will refuse the write, because the policy is evaluated against every action in the cluster
C) Falco — it will observe the kernel events, evaluate them against its rules, and emit an alert; it will not stop the process
D) The `restricted` Pod Security Standard — it will prevent the write, because `readOnlyRootFilesystem` is required

**5.** A team lead asks you to remove one specific permission from an engineer who currently holds the `edit` ClusterRole in a namespace: they should keep everything `edit` provides, except the ability to delete Deployments. What is your answer?

A) Add a Role with a deny rule for `delete` on `deployments`, bound in the same namespace
B) Patch the existing RoleBinding to exclude that verb
C) There is no way to subtract from a grant; stop granting `edit` and grant a custom Role built from the permissions they should have
D) Add a second RoleBinding to a more restrictive role; the intersection of the two applies

---

**Answers with Explanations:**

**1. B.** *"Notation resolves the tag to the digest before signing if a tag is used to identify the container image"* [source: notary-project-signing-digest-2026-08-31] — the signature never covered the tag, only the digest of the content the tag pointed at. New content has a new digest, so the existing signature does not verify against it, and admission refuses. **A** is the misconception the Fixed Point exists to kill, and it is the reason the documentation says *"Always reference and use the image digest instead of a tag since digest is immutable"* [source: notary-project-signing-digest-2026-08-31]. **C** gets the outcome accidentally right for the wrong reason and then adds a false claim: an unverified image is not "pulled unverified" under an enforcing policy, it is refused. **D** contradicts the quoted sentence; you may hand the tool a tag, it just does not sign one.

**2. B.** Scan and sign happen at build time; the signature is recorded in a transparency log; the artifact goes to a registry that restricts who may pull it; and the cluster verifies at admission before running it [source: k8s-docs-cloud-native-security-2026-08-23; sigstore-overview-2026-08-23]. **Verify** is the first step the cluster itself performs; everything before it happened elsewhere, possibly months earlier, under someone else's control.

**A** signs before scanning, which would attest to content you have not examined, and then names the wrong cluster-performed step.
**C** records before signing, which is backwards — the log records signing events [source: sigstore-overview-2026-08-23], so there is nothing to record yet.
**D** is the one to take slowly, because **the order is correct** and only the second half is wrong. Restricting who may pull is the registry's job, and the registry is not the cluster; the cluster's own first act on this artifact is verification at the admission gate. If you picked D, your model of the sequence is fine and your model of the boundary is not — which is exactly the distinction the figure's vertical line draws.

**3. B.** PSA enforces the Pod Security Standards and nothing else [source: k8s-docs-pod-security-admission-2026-08-31]; its three levels are fixed definitions about `securityContext` and related fields, with no mechanism for expressing an organizational rule about labels. Kyverno validates arbitrary conditions at the admission gate [source: kyverno-overview-2026-08-23], as does OPA Gatekeeper. **A** invents an extension mechanism PSA does not have. **C** puts a runtime detection tool at the admission gate; Falco emits alerts, it does not refuse objects [source: falco-overview-2026-08-23]. **D** misunderstands both systems: RBAC has no deny rules, and it authorizes on verb and resource, not on an object's field values. RBAC cannot see the label.

**4. C.** Falco *"observes Linux kernel events (system calls)… enriches them with metadata from the container runtime and Kubernetes, evaluates the event stream against a rules engine, and emits real-time alerts"*, and its default detections explicitly include unauthorized modifications to sensitive directories such as `/etc` and shell execution inside containers [source: falco-overview-2026-08-23]. It reports; it does not block.

**A** reaches six hours past admission's window and then invents a capability admission does not have. Admission accepts or refuses objects; it does not terminate running Pods.
**B** is the sharper version of the same error, and worth naming precisely: a policy engine's validating rules are evaluated against **API requests at the admission gate**, not against process behavior. A process writing a file generates no API request, so there is no admission event for the policy to fire on. Kyverno can also run as a CLI-based scanner [source: kyverno-overview-2026-08-23], but that scans manifests, not syscalls.
**D** is the closest to defensible and still wrong on two counts: `readOnlyRootFilesystem` is a `securityContext` field the Restricted level does not in fact mandate [source: k8s-docs-pod-security-standards-profiles-2026-08-31], and in any case a level constrains a Pod *at admission*, so it could have prevented the Pod from being created but has no role once it is running.

**5. C.** *"Permissions are purely additive (there are no 'deny' rules)"* [source: k8s-docs-rbac-2026-08-23]. There is no rule that subtracts, so the only path is to stop granting the role that includes the unwanted permission and grant something narrower. **A** invents deny rules. **B** would not work even if `roleRef` were mutable, which it is not [source: k8s-docs-rbac-2026-08-23], because a binding grants a role wholesale; it does not filter it. **D** is the most seductive because it sounds like how firewalls work: additive means *union*, not intersection, so a second binding can only add.

---

**How'd You Do?**

**5/5:** §9 will be a confirmation rather than a surprise, which is how it is meant to read.

**3–4:** review the miss and continue. §9 introduces no new object and depends on no single fact from this checkpoint.

**0–2:** re-read §7 before §8 — §8's whole framing is "the same gate, a different question," and it needs §7's picture of where that gate sits. If the miss was question 5, re-read §3's closing pages on the additive rule before you start §9, because §9 is an argument about that rule and nothing else.

---

**Checkpoint: You've Now Mastered**

✓ The supply chain as a sequence of checkpoints, and what each one buys
✓ What a signature binds to, and why a tag would be worthless
✓ Where a policy engine sits and what it does that PSS cannot
✓ Admission-time versus runtime, and why detection is a different question rather than a weaker answer

One section left, and it is the one Chapter 10 and Chapter 11 have both been pointing at.

---

## ☀️ §9 — Additive, Never Deny

Nothing new here. This section introduces no object, no field, and no tool. It makes an argument, and the argument is the thing the last two chapters have been building toward.

### The two systems

**RBAC** governs what an identity may ask the API server for. Its objects are Roles and bindings. It sits at the second of the three gates. It was designed for the problem of multi-tenant API access. *"Permissions are purely additive (there are no 'deny' rules)"* [source: k8s-docs-rbac-2026-08-23].

**NetworkPolicy** governs which Pod may open a connection to which Pod. Its objects are policies with selectors. It is implemented by a CNI plugin, not the API server. It was designed for the problem of lateral movement inside a flat network. It is additive: policies allow, and the effect of several is the union of what they allow. *[cross-bearing: see Ch 10 §6 — allowing, never denying]*

Those are two systems with essentially nothing in common. Different layers, different objects, different implementers, different problems, different decades. Chapter 10 told you NetworkPolicy allows and never denies, and told you to hold on to the phrasing about **subtraction**. Chapter 11 told you the permission system in this chapter would have no way to say no. Section 3 confirmed it.

<!-- FIGURE: ch12-zenith-additive-never-deny -->
```
   ┌─────────────────────────────┐   ┌─────────────────────────────┐
   │  RBAC                       │   │  NETWORKPOLICY              │
   │  the API layer              │   │  the network layer          │
   ├─────────────────────────────┤   ├─────────────────────────────┤
   │                             │   │                             │
   │       identity              │   │          Pod                │
   │          │                  │   │           │                 │
   │          ▼                  │   │           ▼                 │
   │      API request            │   │      connection             │
   │          │                  │   │           │                 │
   │          ▼                  │   │           ▼                 │
   │   ┌─────────────┐           │   │   ┌─────────────┐           │
   │   │ grant?      │           │   │   │ allow rule? │           │
   │   └──────┬──────┘           │   │   └──────┬──────┘           │
   │          │                  │   │          │                  │
   │     ┌────┴────┐             │   │     ┌────┴────┐             │
   │     ▼         ▼             │   │     ▼         ▼             │
   │   allow    (nothing)        │   │   allow    (nothing)        │
   │              │              │   │              │              │
   │              ▼              │   │              ▼              │
   │          denied by          │   │          denied by          │
   │          ABSENCE            │   │          ABSENCE            │
   │                             │   │                             │
   │   ┌──────────────────────┐  │   │   ┌──────────────────────┐  │
   │   │  no deny rule exists │  │   │   │  no deny rule exists │  │
   │   └──────────────────────┘  │   │   └──────────────────────┘  │
   └─────────────────────────────┘   └─────────────────────────────┘

              different layer.  different object.  different decade.
                            the same shape.
```

### The claim, and its status

> ☀️ **Zenith:** Two systems, built by different people for unrelated problems at different layers of the stack, arrived independently at the same design: rules that only ever grant, and the removal of access accomplished only by the removal of a grant. Neither has a deny rule. In both, subtraction is not an operation you can perform.

Chapter 11 promised you would understand *why*, and why it is a feature rather than an omission. So here is the honest situation, stated before the argument rather than after it.

**The documentation states the property and does not explain it.** The RBAC reference says permissions are purely additive with no deny rules, in a parenthetical [source: k8s-docs-rbac-2026-08-23]. Chapter 10's sources said the equivalent about NetworkPolicy. Neither offers a rationale, and no source in this book's corpus does either.

What follows is therefore **a reading, not a citation**. It is the interpretation that makes the best sense of what both systems do. Hold it more loosely than you hold the facts around it.

### The reading

A deny rule makes the effect of a grant **non-local**.

That is the whole argument, and everything else follows from it.

Consider a system with deny. You are handed a rule: *this subject may delete Deployments in this namespace.* What does the rule do? You cannot say. Somewhere else there may be a rule that denies it, and until you have read every rule that could possibly apply, you do not know the effect of the one in front of you. A deny rule is a correction pencilled onto somebody else's chart: the sheet in your hands is accurate and still does not tell you where you are, because the correction is on a sheet you have not seen.

Which forces a second thing: **evaluation order becomes semantics.** Once both allow and deny exist, "which one wins?" must be answered, and every real system answers it differently. Deny-overrides. First-match. Most-specific-wins. Explicit-beats-inherited. Each is defensible and none is obvious, and the choice is now part of what a policy *means*. Anyone reasoning about the system has to hold not just the rules but the resolution procedure.

Now add the two conditions that describe an actual Kubernetes cluster.

**Rules are written by many authors.** Platform engineering writes cluster-wide roles. Application teams write namespace-scoped ones. Every operator you install ships bindings for its own controllers. Helm charts arrive carrying RBAC objects nobody reads. A Kubernetes cluster's policy is not authored; it accretes, from a dozen sources, none of which coordinated with the others.

**The objects being governed change constantly, without anyone's involvement.** Pods appear and disappear. Namespaces get created. CRDs add resource types that did not exist when the roles were written, which is exactly why the documentation warns that wildcard access grants rights *"not just to all object types that currently exist in the cluster, but also to all object types which are created in the future"* [source: k8s-docs-rbac-good-practices-2026-08-31].

Under those two conditions, a deny rule is close to unusable. You would have a policy whose meaning could not be determined by reading any bounded subset of it, assembled by parties who never spoke, against a resource set that changes while you read.

**Additive-only is what makes a single rule readable in isolation.** With no deny, a grant means exactly what it says: it adds these permissions, unconditionally, and no rule anywhere can take them back. To know whether a subject can do something, you take the union of their grants — an operation that is order-independent, composable, and answerable without global knowledge. That property is not an accident of either system. It is the only property that survives the way these systems are actually used.

That, I think, is why two unrelated teams landed in the same place. They were not copying each other. They were solving the same shape of problem — distributed authorship, dynamic membership, composability required — and it has one clean answer.

### The cost, which is real

*"A feature rather than an omission"* should not be oversold, so name what it costs, because it is not nothing.

**You cannot carve an exception out of a grant.** Section 3's hazard was not a footnote. When somebody holds `edit` and should have everything except one verb on one resource, there is no rule to write. You stop granting `edit` and construct a role by hand from the permissions they should have, and you now maintain that role forever, updating it as the cluster acquires resource types the original author never anticipated. The clean composability comes out of the same property that makes exceptions expensive.

Sometimes an exception is exactly what you want. Additive-only says: then build the grant you actually mean, from the ground up. That is more work, and it is honestly more work, and the trade is that anyone can read the result and know what it does.

### What this is worth

You now have a thing that is more useful than either fact.

Faced with a Kubernetes access-control system you have never seen — one that ships in a future release, or in a project you meet next year — you can predict its shape. Additive. No deny. Removal by removing the grant. And you can say why: because that is what composability requires when many hands write the policy and the objects will not hold still.

That is not memorized. It is derived, and it will survive the next curriculum change.

---

## Exam Alert! 🚨

**High-Priority Topics**

1. **The four-way matrix, stated as a rule rather than a table.** *The binding determines the scope of the grant.* The highest-yield fact in the chapter, and the one most likely to be tested through a scenario rather than a definition. If you can derive the four combinations from the namespaced/cluster-scoped boundary, you do not need to remember them.

2. **RBAC is additive with no deny rule.** Every "how do you remove this one permission?" question resolves to *remove the grant*. There is no other answer.

3. **The four default roles and their negative space.** What each *cannot* do: `view` cannot read Secrets; `edit` cannot view or modify roles or bindings; `admin` cannot write the namespace's resource quota or the namespace itself; and `cluster-admin` in a RoleBinding is limited to that binding's namespace.

4. **Secrets are unencrypted in etcd by default**, and there are three exposure paths — API access, etcd access, and the ability to create a Pod.

5. **TokenRequest, not token Secrets.** Since v1.22 the recommended credential is a short-lived, automatically rotating projected token. Long-lived ServiceAccount token Secrets are the legacy risk.

6. **Three PSS levels × three PSA modes, applied per namespace by label.** Level = what is checked. Mode = what happens.

**Common Traps**

These are the specific wrong answers this material produces. Every one of them is a wrong answer somebody has confidently written down.

| The trap | The correct understanding |
|---|---|
| RBAC has deny rules | Purely additive. Removing access means removing the grant. [source: k8s-docs-rbac-2026-08-23] |
| ClusterRole is only for cluster-scoped resources | Two of its three documented uses are about namespaced resources — bound into one namespace, or across all. [source: k8s-docs-rbac-2026-08-23] |
| The four combinations must be memorized | They derive from one boundary. The binding sets the scope. |
| A binding can be retargeted | It cannot, after creation. Delete and recreate. [source: k8s-docs-rbac-2026-08-23] |
| `view` can read Secrets | It cannot — nor roles nor bindings. Reading Secrets is transitively becoming a ServiceAccount. [source: k8s-docs-rbac-depth-2026-08-31] |
| `edit` can manage RBAC in its namespace | It cannot; `admin` can. [source: k8s-docs-rbac-2026-08-23] |
| `cluster-admin` always means the whole cluster | In a RoleBinding it is scoped to that namespace. [source: k8s-docs-rbac-2026-08-23] |
| Removing every binding revokes anyone's access | Not for `system:masters` — that membership bypasses RBAC entirely and cannot be revoked by removing bindings. [source: k8s-docs-rbac-good-practices-2026-08-31] |
| Only `get` on Secrets reveals them | `list` and `watch` reveal the contents of every Secret in scope. [source: k8s-docs-rbac-good-practices-2026-08-31] |
| Secrets are encrypted | Unencrypted in etcd by default; encryption at rest is opt-in and is a control-plane configuration. [source: k8s-docs-secret-2026-08-23] |
| An RBAC audit showing no `get secrets` means Secrets are safe | Pod creation in the namespace reads any Secret in it, including via a Deployment. [source: k8s-docs-secret-2026-08-23] |
| Token Secrets are current best practice | TokenRequest, short-lived and rotating, since v1.22. [source: k8s-docs-service-accounts-2026-08-23] |
| PSS levels and PSA modes are the same axis | Levels say what is checked; modes say what happens. Independent. `[inferred]` |
| PodSecurityPolicy is a current control | Superseded by Pod Security Admission; not the mechanism a current cluster uses. |
| A signature covers the tag you signed | It resolves to the digest. Tags are mutable; signatures are not. [source: notary-project-signing-digest-2026-08-31] |
| A valid signature means the artifact is current | It means the bytes came from the signer. Freshness, ordering and key compromise are what TUF addresses. [source: tuf-overview-2026-08-31] |
| Falco prevents the behavior it detects | It observes and alerts. It does not block. [source: falco-overview-2026-08-23] |

One row above carries an `[inferred]` marker: the level/mode confusion. That mark means the row describes something *easy to confuse*, not something anyone has published as *frequently tested*. The distinction matters. This book will tell you when material is high-yield by reasoning about the published objectives, and it will not manufacture a statistic to make the point land harder.

---

## Practice Questions

Twenty-three questions. Five of them require material from earlier chapters, and several cannot be answered from any single section of this one.

---

**1.** Which statement correctly distinguishes the cloud native security lifecycle phases from the 4Cs?

A) The phases describe cloud environments; the layers describe on-premises environments
B) The phases answer *when* a control acts; the layers answer *where* it acts
C) The phases replaced the layers, which are now incorrect
D) The layers apply to Kubernetes; the phases apply to the application only

---

**2.** According to the runtime protection guidance, which of the following belongs to the **compute** area rather than access or storage?

A) Using ServiceAccounts to provide security identities for workloads
B) Enabling encryption at rest for API objects
C) Enforcing Pod Security Standards so applications run with only necessary privileges
D) Protecting the encryption keys used for API traffic

---

**3.** A cluster administrator wants to remove an engineer's superuser access. The engineer's credential places them in the `system:masters` group. The administrator deletes every ClusterRoleBinding and RoleBinding that names that engineer. What is the result?

A) Access is revoked — `system:masters` is bound to `cluster-admin` by a ClusterRoleBinding, which the administrator has now deleted
B) Access is unchanged; membership of `system:masters` bypasses all RBAC rights checks and cannot be revoked by removing bindings
C) Access is reduced to the default API discovery permissions granted to all authenticated principals
D) Access is unchanged until the API server next restarts, at which point the default bindings are reconciled and the bypass is removed

---

**4.** Which is the current recommended way for a Pod to obtain ServiceAccount credentials?

A) Create a Secret of type `kubernetes.io/service-account-token` and mount it
B) A short-lived, automatically rotating token from the TokenRequest API, mounted as a projected volume
C) Store the token in a ConfigMap and reference it as an environment variable
D) Have the application call the `TokenReview` API at startup to obtain a token for its own ServiceAccount

---

**5.** Your team needs a set of permissions over `Node` objects — a cluster-scoped resource. Which pair of objects can express this grant, and why?

A) Role + RoleBinding, in the `kube-system` namespace, since that is where node components live
B) ClusterRole + ClusterRoleBinding, because a Role cannot hold rules over a resource that is in no namespace
C) ClusterRole + RoleBinding, scoping the node access to one namespace
D) Either Role + RoleBinding or ClusterRole + ClusterRoleBinding, depending on preference

---

**6.** A ClusterRole named `secret-reader` grants `get` and `list` on `secrets`. It is referenced by a RoleBinding in the `staging` namespace. Which statement is true?

A) The subjects can read Secrets in every namespace, because the role is a ClusterRole
B) The RoleBinding is invalid; a RoleBinding cannot reference a ClusterRole
C) The subjects can read Secrets in `staging` only
D) Nothing is granted; a ClusterRole's rules take effect only when a ClusterRoleBinding references them

---

**7.** You need to allow a subject to read the ConfigMap named `app-config` in a namespace, and no other ConfigMap. Which mechanism expresses this?

A) A label selector on the Role's rule
B) The `resourceNames` list on the rule
C) A separate Role per ConfigMap, since RBAC cannot filter by name
D) A `fieldSelector` on the RoleBinding

---

**8.** *[retrieval: ch4]* A colleague proposes granting permissions to "every ServiceAccount labeled `tier=frontend`" so that new frontend workloads pick up the grant automatically. What is wrong with this proposal?

A) Nothing — this is what aggregated ClusterRoles are for
B) RBAC names subjects as literal strings; there is no subject selector, and a grant that expanded when someone added a label would not be auditable
C) It would work, but only for ServiceAccounts in the same namespace as the binding
D) It would work if the subjects were users rather than ServiceAccounts; only ServiceAccounts must be named literally

---

**9.** Which of these operations does the `admin` default role permit within its namespace?

A) Writing the namespace's ResourceQuota
B) Deleting the namespace object itself
C) Creating Roles and RoleBindings
D) Modifying cluster-scoped resources referenced from the namespace

---

**10.** A Secret's `data` field contains `cGFzc3dvcmQxMjM=`. What protection does this encoding provide?

A) It is encrypted with the cluster's default key
B) It provides no additional confidentiality over plain text
C) It is hashed, so the original value cannot be recovered
D) It is protected only while the Secret is at rest in etcd

---

**11.** Which single control closes the exposure path created by an unencrypted etcd backup?

A) A NetworkPolicy restricting access to the etcd Pods
B) Removing `get secrets` from all Roles and ClusterRoles
C) Encryption at rest, configured via `EncryptionConfiguration` on the API server
D) Mounting Secrets as files rather than environment variables

---

**12.** Which statement about mounting a Secret is correct?

A) A Secret mounted as a volume receives updates automatically, except when mounted as a `subPath`
B) A Secret consumed as an environment variable updates automatically when the Secret changes
C) Both mechanisms update automatically; the difference is only in file permissions
D) Neither mechanism receives updates; the Pod must be recreated in both cases

---

**13.** A Pod sets `securityContext.runAsNonRoot: true` at Pod scope. What does this accomplish?

A) It drops all Linux capabilities from every container
B) It requires that the containers do not run as the root user
C) It mounts the root filesystem read-only
D) It applies the `RuntimeDefault` seccomp profile

---

**14.** Which statement about `privileged: true` is correct?

A) It grants a single additional capability, `CAP_SYS_ADMIN`
B) It grants all Linux capabilities, but any seccomp or AppArmor profile you specified in the manifest remains in force
C) It overrides or undoes many other hardening settings, including the applied seccomp and AppArmor profiles, and grants all Linux capabilities
D) It is required in order to set `runAsUser: 0`

---

**15.** *[retrieval: ch10]* Which statement correctly describes the relationship between `securityContext` and NetworkPolicy?

A) NetworkPolicy governs the workload-to-host axis; `securityContext` governs workload-to-workload
B) They are two views of the same underlying enforcement mechanism
C) `securityContext` governs the workload-to-host axis; NetworkPolicy governs the workload-to-workload axis; they fail independently and neither substitutes for the other
D) NetworkPolicy supersedes `securityContext` on clusters using a CNI plugin that supports it

---

**16.** A namespace is labeled `pod-security.kubernetes.io/enforce: restricted`. A developer submits a Pod with no `securityContext`. What happens?

A) It is admitted, because Restricted allows the default minimally-specified Pod
B) It is rejected, because Restricted requires `runAsNonRoot: true`, `allowPrivilegeEscalation: false`, capabilities dropping `ALL`, and an explicit seccomp profile
C) It is admitted with a warning
D) It is admitted, and the missing fields are populated with Restricted-conformant defaults

---

**17.** Which pairing is correct?

A) `enforce` is a level; `baseline` is a mode
B) `warn` is a level; `restricted` is a mode
C) `restricted` is a level; `audit` is a mode
D) `privileged` is a mode; `enforce` is a level

---

**18.** *[retrieval: ch8]* Pod Security Admission and a Kyverno validating policy have something structural in common. What is it, and what distinguishes them?

A) Both run at the authorization gate; PSA is built in and Kyverno is not
B) Both run at the admission gate; PSA answers a fixed question about the Pod Security Standards, while a policy engine answers an arbitrary question
C) Both run at runtime; PSA inspects Pods and Kyverno inspects all objects
D) Both are authorization modes configured with `--authorization-mode`

---

**19.** *[retrieval: ch2]* What does a container image signature bind to?

A) The image tag, since that is what the signer typed
B) The image's digest — the tool resolves a tag to a digest before signing
C) The registry hostname and repository path
D) The image's SBOM, which in turn references the layers

---

**20.** A cluster verifies image signatures at admission. Which component performs the verification, and where does it sit relative to the rest of the supply chain?

A) The container runtime, at pull time, after everything else in the chain
B) An admission controller — such as Sigstore's Policy Controller or Kyverno — and it is the first checkpoint the cluster itself performs
C) The registry, before serving the image
D) The kubelet, immediately before starting the container

---

**21.** *[retrieval: ch10]* Which statement most accurately characterizes what RBAC and NetworkPolicy have in common?

A) Both are implemented by the API server and evaluated at the same gate
B) Both use label selectors to identify the subjects they govern
C) Both are purely additive: rules only grant, and removing access means removing a grant
D) Both were retrofitted with explicit deny rules in later API versions, which is why the additive behaviour is now the default rather than the only option

---

**22.** A namespace carries `pod-security.kubernetes.io/enforce: restricted`. A developer submits a Pod whose single container sets exactly this and nothing else:

```
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  allowPrivilegeEscalation: false
  capabilities:
    drop: ["ALL"]
```

What happens, and why?

A) Admitted — every Restricted requirement is satisfied by that block
B) Rejected — Restricted also requires an explicit seccomp profile of `RuntimeDefault` or `Localhost`, and none is set
C) Rejected — `runAsUser: 1000` conflicts with `runAsNonRoot: true`
D) Admitted with a warning, because `enforce` applies leniently to capability rules

---

**23.** An organization verifies image signatures at admission and rejects anything unsigned. An attacker with control of a registry serves a client an older image that is correctly signed by the organization's own build pipeline and that contains a vulnerability fixed two releases ago. Does signature verification catch this, and what addresses it?

A) Yes — the signature will not verify, because the older image's digest differs from the current one
B) No — the artifact is correctly signed, so verification passes; this is the class of attack The Update Framework exists to address
C) No — but an SBOM attached to the image would refuse to load, because its component list no longer matches the deployed release
D) Yes — Rekor will reject the lookup, because the older signing event has been superseded by a newer one

---

### Answers with Explanations

**1. B.** The two framings answer different questions, and a control has a position on both: image signing is `distribute`/Container, RBAC is `runtime`/Cluster. **A** invents a distinction neither framing makes. **C** overstates the situation. The current kubernetes.io page does present the phases in place of the 4Cs [source: k8s-docs-cloud-native-security-2026-08-23], but the 4Cs are not wrong, they are a different map, and they remain the framing most third-party material uses. **D** invents a scope split that neither framing has.

**2. C.** The runtime/compute list names enforcing Pod Security Standards *"for applications to help ensure they run with only the necessary privileges"* [source: k8s-docs-cloud-native-security-2026-08-23]. **A** and **D** are runtime/access; ServiceAccounts and TLS for API traffic both appear in that list. **B** is runtime/storage. The point of the question is that all three areas are runtime; naming the phase is not enough.

**3. B.** *"Avoid adding users to the `system:masters` group. Any user who is a member of this group bypasses all RBAC rights checks and will always have unrestricted superuser access, which cannot be revoked by removing RoleBindings or ClusterRoleBindings"* [source: k8s-docs-rbac-good-practices-2026-08-31]. Group membership is not an RBAC grant, so removing RBAC objects removes nothing.

**A** is the intuitive and wrong model — it treats group membership as though it were expressed through a binding that could be deleted.
**C** describes what would happen to an ordinary subject whose bindings were all removed: identity intact, permissions down to API discovery [source: k8s-docs-service-accounts-2026-08-23]. It is the right outcome for the wrong principal.
**D** invents a reconciliation that runs the wrong direction. The API server does reconcile default bindings at startup, but the bypass does not depend on any binding, so a restart restores nothing and removes nothing.

Two consequences worth carrying: this is invisible to any audit that reads RBAC objects, and if the cluster uses an authorization webhook, requests from members of that group are never sent to it at all [source: k8s-docs-rbac-good-practices-2026-08-31].

**4. B.** *"In Kubernetes v1.22 and later, Kubernetes gets a short-lived, automatically rotating token using the TokenRequest API and mounts the token as a projected volume"* [source: k8s-docs-service-accounts-2026-08-23]. **A** is the legacy mechanism; long-lived token Secrets *"don't expire or rotate and pose a security risk"* [source: k8s-docs-service-accounts-2026-08-23]. **C** puts a credential in the wrong object type entirely. **D** is the near-miss worth naming: `TokenRequest` and `TokenReview` are different APIs doing opposite jobs. TokenRequest *issues* a token; TokenReview *validates* one somebody has presented. And a workload that had to authenticate in order to fetch its own credential would have nothing to authenticate with — which is exactly the bootstrap problem the projected volume solves by delivering the token before the process starts.

**5. B.** `Node` is cluster-scoped, so a Role — which *"always sets permissions within a particular namespace"* [source: k8s-docs-rbac-2026-08-23] — has nowhere to put the rule, and the ClusterRole is forced. The grant must then be cluster-wide, because the resource is in no namespace to scope it to. **A** misunderstands what `kube-system` is: a namespace containing objects, not a namespace that contains the nodes. **C** is the seductive one. A ClusterRole *can* be bound by a RoleBinding, and doing so binds it into that namespace [source: k8s-docs-rbac-2026-08-23] — but the `Node` rule has no namespace to land in. **D** treats a structural constraint as a stylistic preference.

**6. C.** *"A RoleBinding can reference a ClusterRole and bind that ClusterRole to the namespace of the RoleBinding"* [source: k8s-docs-rbac-2026-08-23]. The binding determines the scope. **A** is the most common version of this trap and is the reason `cluster-admin` in a RoleBinding surprises people. **B** contradicts the documented behavior. **D** is A's mirror image: where A over-scopes the grant, D refuses it entirely. Both errors come from the same wrong premise — that a ClusterRole's scope is fixed by the role object rather than by the binding.

**7. B.** *"You can also refer to resources by name for certain requests through the `resourceNames` list. When specified, requests can be restricted to individual instances of a resource"* [source: k8s-docs-rbac-depth-2026-08-31]. **A** is the selector reflex again; there is no label selector on an RBAC rule. **C** is wrong about the capability existing, though it correctly identifies that RBAC's naming is literal rather than queried. **D** invents a field.

**8. B.** RBAC names subjects — users, groups, ServiceAccounts — as literal strings [source: k8s-docs-rbac-depth-2026-08-31]. There is no subject selector, and Chapter 4 specifically warned that assuming the selector pattern held here would produce a confident wrong prediction. **A** confuses two different uses of selectors: an aggregated ClusterRole uses a label selector to combine *ClusterRoles*, not to select subjects [source: k8s-docs-rbac-depth-2026-08-31]. **C** invents a namespace constraint on a mechanism that does not exist. **D** is a false symmetry, and worth being explicit about: all three subject kinds are named literally. There is no subject kind that RBAC selects rather than names.

**9. C.** *"If used in a RoleBinding, allows read/write access to most resources in a namespace, including the ability to create roles and role bindings within the namespace. This role does not allow write access to resource quota or to the namespace itself"* [source: k8s-docs-rbac-depth-2026-08-31]. **A** and **B** are the two things that sentence explicitly excludes, and the exclusions are principled: writing your own quota would let you raise your own ceiling. **D** confuses a namespaced role with cluster-scoped access.

**10. B.** *"Base64 encoding is not an encryption method, it provides no additional confidentiality over plain text"* [source: k8s-docs-secrets-good-practices-2026-08-24]. **A** invents a cluster key. **C** confuses encoding with hashing; base64 is trivially reversible, which is the entire point of an encoding. **D** confuses base64 with encryption at rest, a separate, opt-in mechanism.

**11. C.** Encryption at rest protects the object as written to etcd [source: k8s-docs-encrypt-data-2026-08-31], which is exactly the content of an etcd backup. **A** protects access to the running etcd over the network and does nothing about a backup file sitting in object storage. **B** addresses the API route, not the etcd route. **D** is a good practice for a different reason and does not touch etcd at all.

**12. A.** When a Secret is mounted as a volume, updates propagate automatically; *"A container using a Secret as a subPath volume mount does not receive automated Secret updates"* [source: k8s-docs-secret-risks-2026-08-31].

**B** inverts the asymmetry: an environment variable is read at container start and is then a fixed string in the process's environment, so a rotated Secret does not reach a running container.
**C** is wrong about where the difference lies. The two mechanisms differ in *update behaviour*; file permissions are a volume-only concern that has no environment-variable counterpart to differ from.
**D** generalizes the environment-variable behaviour to both, which erases the whole rotation half of the file-over-env-var argument.

**13. B.** `runAsNonRoot` requires that containers do not run as root — the Restricted level mandates `runAsNonRoot: true` for exactly this reason [source: k8s-docs-pod-security-standards-profiles-2026-08-31], and the documentation recommends it generally [source: k8s-docs-linux-kernel-security-constraints-2026-08-31]. **A** describes `capabilities.drop`. **C** describes `readOnlyRootFilesystem`. **D** describes `seccompProfile`. All four are `securityContext` fields, which is why this question is worth taking slowly.

**14. C.** *"Privileged containers override or undo many other hardening settings such as the applied seccomp profile, AppArmor profile, or SELinux constraints. Privileged containers are given all Linux capabilities, including capabilities that they don't require"* [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].

**A** dramatically understates it; the point is *all* capabilities, and the recommended alternative is to grant specific ones via the `capabilities` field [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].
**B** is the version of this misconception most worth killing: it assumes hardening layers stack independently, so that a seccomp profile you wrote would survive a privileged flag somebody else set. The documented behaviour is the opposite — privileged containers run as the `Unconfined` seccomp profile, overriding any profile specified in the manifest, and ignore any applied AppArmor profiles [source: k8s-docs-linux-kernel-security-constraints-2026-08-31].
**D** invents a dependency. Running as UID 0 inside a container needs no privileged flag at all; `privileged: true` is about capabilities and kernel-constraint bypass, not about which UID the process runs as.

**15. C.** Chapter 10 drew the two axes; this chapter filled in the second. `securityContext` constrains what a workload may do to its node; NetworkPolicy constrains which workloads may reach which. Different objects, different implementers, independent failure. **A** inverts them. **B** is false: one is a Pod spec field enforced by the runtime and kubelet, the other is an object enforced by a CNI plugin. **D** invents a supersession that would make no sense, since a NetworkPolicy has nothing to say about `privileged: true`.

**16. B.** Restricted requires `runAsNonRoot: true`, `allowPrivilegeEscalation: false`, capabilities dropping `ALL`, and an explicit `RuntimeDefault` or `Localhost` seccomp profile [source: k8s-docs-pod-security-standards-profiles-2026-08-31]. A Pod with no `securityContext` satisfies none of those, and `enforce` rejects. **A** describes **Baseline**, which *"Allows the default (minimally specified) Pod configuration"* [source: k8s-docs-pod-security-standards-2026-08-23]; that is the specific confusion this question tests. **C** describes `warn` behavior. **D** invents a mutation; PSA validates, it does not mutate.

**17. C.** `restricted` is one of the three levels; `audit` is one of the three modes [source: k8s-docs-pod-security-standards-2026-08-23]. Every other option crosses the axes, which is the single most likely wrong answer this chapter produces. Check the grammar before the meaning: `enforce`/`audit`/`warn` are modes, `privileged`/`baseline`/`restricted` are levels, and no term is both.

**18. B.** PSA is *"a built-in Pod Security admission controller"* [source: k8s-docs-pod-security-admission-2026-08-31], and Kyverno can be *"applied as a Kubernetes admission controller (webhook)"* [source: kyverno-overview-2026-08-23]. Same gate, and Chapter 8 promised you would recognize it. The distinction is the question each answers: PSA's is fixed to the Pod Security Standards, a policy engine's is arbitrary. **A** puts both at the wrong gate. **C** confuses admission with runtime. **D** confuses admission controllers with authorization modes, a real distinction the chapter draws in §3.

**19. B.** *"Notation resolves the tag to the digest before signing if a tag is used to identify the container image"* [source: notary-project-signing-digest-2026-08-31]. **A** is the misconception, and it matters because a tag-covering signature would attest to content the signer has never seen — Chapter 2's mutable-pointer lesson, arriving as a security consequence. **C** would attest to a location rather than to content. **D** inverts the relationship: an SBOM is a separate signable artifact that describes an image, not the thing a signature on the image binds to.

**20. B.** Sigstore's Policy Controller *"enforces signature verification policies within Kubernetes as an admission controller"* [source: sigstore-overview-2026-08-23], and Kyverno can *"verify container images and metadata"* [source: kyverno-overview-2026-08-23]. Verification at admission is the first checkpoint the cluster itself performs; everything before it (scan, sign, record, restrict) happened outside, under someone else's control.

**A** places verification at the runtime, at pull time. That is late by one gate and wrong about the actor: by the time anything is pulled, the object has already been accepted, so a refusal there would leave a Pod the API server has already admitted.
**C** places it at the registry. A registry can restrict *who may pull*, which is a real control [source: k8s-docs-cloud-native-security-2026-08-23], but it is not the cluster deciding whether to accept the object, and a registry you do not administer is exactly what verification exists to be independent of.
**D** is the most tempting: the kubelet does pull the image, and it is inside the cluster. But the enforcement decision is made at admission, before the object is accepted and long before any kubelet is involved.

**21. C.** Both are purely additive; in both, the only way to remove access is to remove a grant [source: k8s-docs-rbac-2026-08-23]. That is the shared semantic, and §9 argues it is not a coincidence. **A** is false on both halves: NetworkPolicy is enforced by a CNI plugin, not the API server, and not at the authorization gate. **B** is half true and therefore the best distractor here — NetworkPolicy does use selectors, and RBAC pointedly does not. **D** invents a version history. Neither system has ever had a deny rule, and §9's argument is that the additive design is load-bearing rather than a default somebody happened to pick.

**22. B.** Restricted's seccomp control requires the profile type to be `RuntimeDefault` or `Localhost` explicitly [source: k8s-docs-pod-security-standards-profiles-2026-08-31], and no `seccompProfile` is set. Everything else in that block conforms: `runAsNonRoot: true`, `runAsUser` non-zero, `allowPrivilegeEscalation: false`, and capabilities dropping `ALL`.

**A** is the near miss this question exists to produce — four of five requirements met, and the missing one is the least visible because it is the only one that is not obviously about root.
**C** invents a conflict. A non-zero `runAsUser` is precisely what Restricted's "Running as Non-root user" control asks for [source: k8s-docs-pod-security-standards-profiles-2026-08-31]; the two fields agree rather than collide.
**D** crosses the axes. `enforce` rejects, full stop — it is a mode, not a severity, and it does not apply differently to different controls. If you wanted the warning behaviour, that is a different label.

**23. B.** TUF names exactly this attack: *"An attacker gives you an older, insecure version of a file that you already have and tricks you into thinking it's newer"* [source: tuf-overview-2026-08-31]. Every attack in TUF's list involves a *correctly signed* artifact, which is what distinguishes freshness and ordering from authenticity — and why TUF *"maintains the security of software update systems, providing protection even against attackers that compromise the repository or signing keys"* [source: tuf-overview-2026-08-31].

**A** misunderstands what verification checks. A signature over the older digest is entirely valid for that older digest. Verification asks "did these bytes come from who I think?" and answers nothing about which version they are.
**C** invents an enforcement behaviour. An SBOM is a record of what an artifact contains, not a gate, and the older image's SBOM correctly describes the older image.
**D** inverts the transparency log's function. Rekor is append-only and records signing events for public audit [source: sigstore-overview-2026-08-23]; entries are never superseded or expired, and nothing about it is a freshness check performed at pull time.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| Phases vs layers | Phases = *when* a control acts (develop, distribute, deploy, runtime). Layers = *where* (Cloud ⊃ Cluster ⊃ Container ⊃ Code). Every control has both coordinates. |
| Runtime's three areas | Access (the API), compute (the workload on the node), storage (data at rest). This chapter's table of contents. |
| ServiceAccount | A namespaced identity object. Every namespace has a `default`; every Pod that names nothing gets it. |
| Identity ≠ permission | Two things, two objects. The `default` ServiceAccount has an identity and can do essentially nothing. |
| Credentials | TokenRequest, short-lived, rotating, projected. Long-lived token Secrets are legacy. |
| Users and groups | Not Kubernetes objects. They arrive from outside as strings the authenticator produces. |
| The four RBAC objects | Role (namespaced) / ClusterRole (not) hold rules. RoleBinding (one namespace) / ClusterRoleBinding (everywhere) grant them. |
| The derivation | Cluster-scoped resource → ClusterRole is forced. Where the grant applies → the binding decides. **The binding determines the scope of the grant.** |
| Additive, no deny | Permissions are the union of grants. To remove access, remove the grant. There is no other operation. |
| Binding immutability | `roleRef` cannot change after creation. Delete and recreate. |
| Subjects | Named as literal strings — users, groups and ServiceAccounts alike. There is no subject selector, and that is deliberate. |
| Escalation prevention | You cannot create a role holding permissions you do not have, absent the `escalate` verb; you cannot bind one, absent `bind`. |
| `system:masters` | Not an RBAC grant. Bypasses every rights check, cannot be revoked by deleting bindings, invisible to an RBAC audit. |
| Default roles | `view` cannot read Secrets. `edit` cannot touch RBAC. `admin` cannot write its quota or namespace. `cluster-admin` in a RoleBinding is namespace-scoped. |
| base64 | Encoding. Provides no confidentiality over plain text. |
| Secret storage | Unencrypted in etcd by default. Encryption at rest is opt-in, via `EncryptionConfiguration` on the API server. |
| Three exposure paths | API access (including `list` and `watch`) · etcd access, including backups · **the ability to create a Pod**. |
| The weak boundary | Boundaries within a namespace are weak. Separate trust levels with separate namespaces. |
| File over env var | A mounted Secret updates automatically (except via `subPath`); an environment variable is fixed at container start. |
| `securityContext` | Pod scope sets the default; container scope overrides it. Governs the workload-to-host axis. |
| `privileged: true` | Not one more setting — the setting that turns the others off. All capabilities; seccomp, AppArmor and SELinux constraints bypassed; every Secret on the node readable. |
| The three PSS levels | `privileged` (no restrictions) · `baseline` (prevents known escalations, allows the default Pod) · `restricted` (current hardening best practice). Cumulative in permitted Pods. |
| The three PSA modes | `enforce` (reject) · `audit` (log) · `warn` (tell the user). |
| Levels × modes | Independent axes, applied per namespace by label `pod-security.kubernetes.io/<MODE>: <LEVEL>`. Level = what. Mode = what happens. |
| The supply chain | build → scan → sign → record → restrict → **verify** → run. Verify is the first step the cluster performs itself. |
| Signatures | Bind to the **digest**. A tool handed a tag signs the digest it resolves to. |
| Sigstore | Cosign (client) · Fulcio (short-lived certs from a verified identity) · Rekor (append-only transparency log) · Policy Controller (admission-time verification). Keyless: the private key is discarded after one signing. |
| TUF | Freshness, ordering and key compromise — the attacks that use a *correctly signed* artifact. Signing alone does not address them. |
| Policy engines | Kyverno (YAML/CEL, validate/mutate/generate/clean up) and OPA Gatekeeper (Rego), both at admission. An arbitrary question where PSA answers a fixed one. |
| Falco | Runtime. Observes kernel events, evaluates rules, **emits alerts**. Detects; does not prevent. |
| The shared semantic | RBAC and NetworkPolicy both allow and never deny, from different layers for different reasons — because a deny rule makes a grant's effect non-local, and these policies are written by many hands against objects that will not hold still. |

---

## The Voyage Ahead

You have spent this chapter answering a question by refusing things. What is a workload allowed to do? Whatever a grant says, and nothing else. What may it do to its node? Whatever a `securityContext` permits and a Pod Security level tolerates. What may it run? Whatever survived verification at the gate.

Every one of those controls is a way of saying no by not saying yes. Which means every one of them can produce a workload that does not work, and none of them will tell you that is why.

That is the next chapter's problem. A Pod stuck in `Pending`. A Pod that starts and immediately dies. A Pod that does not appear at all because an admission controller you forgot about declined the object, which is a failure with no phase, no events, and no logs, because there is no Pod. A container that runs perfectly and cannot read the file it needs, because somebody set `runAsUser` on an image built expecting root. A Deployment that will not roll out because the Secret it references was renamed.

Chapter 13 is about reading those signatures. Not guessing at them — reading them, in a fixed order, starting with a question most people skip: *whose problem is this?* There is a triage flow, it has a specific sequence, and the sequence exists because the cheap checks eliminate whole categories of cause before you spend an hour reading logs that were never going to contain the answer.

Bring three things with you from this chapter. The first is the shape of a Pod that was *rejected* rather than one that *failed*: you now know that admission can refuse an object outright, and that a refused object leaves nothing behind to inspect. The second is the `securityContext` fields, because a container that cannot write where it expects to write is a permissions failure wearing an application error's clothing. The third is Secrets: a Pod that references one that does not exist never gets a running container, and it fails in a recognizable way rather than a mysterious one.

You have spent twelve chapters learning what the cluster does when everything works. The next two are about the other case, and the honest truth is that the second kind of knowledge is what people actually get paid for.

---

🏆 **Safe Harbor**

That is Domain 2's security competency, complete. Nine sections, five independent systems, and one argument that took two chapters to set up.

Take stock of what changed. You can now look at any Kubernetes security control and say which of five questions it answers — *who are you*, *what may you do*, *what is stored where*, *what may your workload do to the machine*, *what did you ship* — and you can say which of the other four it does not answer, which is the harder and more useful half. You can derive the RBAC matrix rather than recalling it. You can look at a namespace's labels and a Pod's spec together and predict the outcome. And you can name the exposure path that no RBAC audit will show you.

The last one is worth sitting with for a moment. Most of what separates a competent Kubernetes engineer from a trusted one is not knowing more controls. It is knowing what each control does *not* cover, and refusing to be reassured by a green check mark that was measuring the wrong thing.

Chart, passage, dawn: 🗺️ → 🌊 → 🌅

> *"A grant says what it says. That is the whole design, and it is worth what it costs."*
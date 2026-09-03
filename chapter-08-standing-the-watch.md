---
chapter: 8
chapter_type: "content"
title: "Standing the Watch"
subtitle: "The commands you'll actually type, and the versions that bite"
exam_domain: "Kubernetes Fundamentals (competency: Administration)"
domain_weight_pct: 5
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- SUBTITLE NOTE. The arc outline's working subtitle is "The commands
#-- you'll actually type, and the versions that will bite you" — twelve
#-- words, against this stage's ≤10-word constraint. Tightened above to
#-- ten by dropping "will ... you", which keeps both clauses, keeps the
#-- wry "actually", and keeps the rhythm. See § Open questions #1.

#-- COMPLEXITY NOTE. The arc outline's depth band is "standard — 5 points,
#-- but four unrelated conceptual arcs". `mixed` is the honest complexity
#-- value: §1, §4 and §7 are procedural; §2 and §8 are abstract; §6 is
#-- close to pure recall. No single label covers it. The four-arc problem
#-- is a *structural* difficulty, not a conceptual one, and it is solved
#-- by the spine in § Section plan rather than by a complexity label.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "standard". Planning
#-- signal only, NOT a target.
#--
#-- SECTION NUMBERING — eleven published cross-bearings point into this
#-- chapter. NONE carries a section number; every one is chapter-scoped
#-- ("see Ch 8 — kubectl, in full"). This chapter is therefore free to
#-- number its sections as it likes, which is unusual and worth using.
#-- Verified 2026-08-24 against chapter-01, -03, -04, -07. See § Debts.
sections:
  - name: "The Grammar of a Command"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig01-kubectl-verb-resource-grammar"
    checkpoint_after: false
  - name: "Three Gates and a Logbook"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig02-three-api-gates"
    checkpoint_after: false
  - name: "Dividing a Shared Cluster"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig05-quota-vs-limitrange"
    checkpoint_after: true
  - name: "Taking a Node Out of Service"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig04-node-lifecycle-cordon-drain"
    checkpoint_after: false
  - name: "Who Owns the Control Plane"
    objectives: ["D1.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Versions That Are Allowed to Disagree"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig03-version-skew-window"
    checkpoint_after: false
  - name: "The One Backup That Matters"
    objectives: ["D1.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Rules, or Consequences"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-zenith-consequences-not-rules"
    checkpoint_after: false

#-- Eight sections against Chapter 7's seven. One more section for the
#-- same 5 points, because the arc outline's "four unrelated arcs" is
#-- real and folding them produces sections that change subject halfway.
#-- The spine that makes eight sections read as one chapter is described
#-- in § Section plan opening. Fold options considered and rejected in
#-- § Open questions #9.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "a client tool that talks to a remote server — what it must know before it can talk, and what happens when there are two servers"
    - "retrieval from Ch 3 — which component is the only door into the cluster, and what that implies about who checks you at it"
    - "the distinct questions any server must answer about an incoming request before doing the work"
    - "retrieval from Ch 4 — what namespaces were for, and the mechanism Ch 4 named for dividing resources between teams"
    - "retrieval from Ch 7 — the built-in taint for a node about to be rebooted, and what it did to Pods already running there"
    - "retrieval from Ch 4 — the Lease objects in kube-node-lease, and what the control plane should conclude when they stop"
    - "two pieces of software in one system at different versions — which direction of mismatch is more dangerous, and why"
    - "running on a managed platform versus your own hardware — which operational duties move, and which stay yours"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 17 = 35, and names this chapter first on its
#-- list of chapters expected to exceed the Bearings minimum. Arc outline
#-- carries that forward as "12-15 Bearings (three checkpoints)". Set at
#-- 15 across three checkpoints of 5, matching the shape shipped by
#-- Chapters 3-7. Chapter total 35 -> 40.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 17
  total_this_chapter: 40

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.2"]
  concepts:
    - "kubectl"
    - "kubectl-syntax"
    - "verb-resource-grammar"
    - "resource-type-abbreviation"
    - "kubeconfig"
    - "kubeconfig-precedence"
    - "in-cluster-authentication"
    - "serviceaccount-token-file"
    - "namespace-override"
    - "api-access-gates"
    - "authentication"
    - "authorization"
    - "admission-control"
    - "admission-controller"
    - "mutating-admission"
    - "validating-admission"
    - "dynamic-admission-control"
    - "auditing"
    - "hub-and-spoke-api-pattern"
    - "tls-bootstrapping"
    - "resource-quota"
    - "limit-range"
    - "namespaced-vs-cluster-scoped"
    - "node-registration"
    - "node-self-registration"
    - "cordon"
    - "drain"
    - "uncordon"
    - "unschedulable-node"
    - "node-conditions"
    - "ready-condition"
    - "memorypressure"
    - "diskpressure"
    - "pidpressure"
    - "networkunavailable"
    - "node-heartbeats"
    - "node-lease"
    - "node-controller"
    - "api-initiated-eviction"
    - "node-monitor-grace-period"
    - "cluster-planning-axes"
    - "managed-kubernetes"
    - "self-hosted-cluster"
    - "kubeadm"
    - "minikube"
    - "kind"
    - "k3s"
    - "semantic-versioning"
    - "supported-releases"
    - "three-supported-minors"
    - "patch-support-window"
    - "version-skew"
    - "upgrade-order"
    - "release-cadence"
    - "etcd-backup"
    - "etcd-snapshot"
    - "etcd-access-equals-root"
    - "disaster-recovery"
  commands:
    - "kubectl-get"
    - "kubectl-describe"
    - "kubectl-explain"
    - "kubectl-config"
    - "kubectl-cordon"
    - "kubectl-drain"
    - "kubectl-uncordon"
    - "etcdctl-snapshot-save"
    - "etcdutl-snapshot-restore"

figures_planned:
  - "ch08-fig01-kubectl-verb-resource-grammar"
  - "ch08-fig02-three-api-gates"
  - "ch08-fig03-version-skew-window"
  - "ch08-fig04-node-lifecycle-cordon-drain"
  - "ch08-fig05-quota-vs-limitrange"
  - "ch08-zenith-consequences-not-rules"
---

# Chapter 8: Standing the Watch
## *"The commands you'll actually type, and the versions that bite"*

**Domain: Kubernetes Fundamentals — 44% of the exam** [source: cncf-kcna-curriculum-pdf-2026-08-23] **· Competency: Cluster Administration — ~5% (authored allocation) · Complexity: Mixed · Novelty: Moderate**

*The 44% is CNCF's published weight for one of its four domains* [source: cncf-kcna-certification-page-2026-08-23]. *The ~5% is this book's own allocation across the competencies inside that domain: the published curriculum carries a percentage against each of the four domains and none against the competencies listed within them* [source: cncf-kcna-curriculum-pdf-2026-08-23]. *The front matter explains how these allocations were derived.*

---

## Attention Budget

**Total time: ~150 minutes | Recommended: split across two sessions, breaking after ☆ Taking Your Bearings #2**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 — The Grammar of a Command | 12 min | Low | Anytime |
| §2 — Three Gates and a Logbook | 22 min | **High** | Peak attention |
| §3 — Dividing a Shared Cluster | 16 min | Medium | When alert |
| ☆ Taking Your Bearings #1 | 8 min | Medium | After a brief break |
| §4 — Taking a Node Out of Service | 18 min | Medium | When alert |
| §5 — Who Owns the Control Plane | 10 min | Low | Anytime |
| ☆ Taking Your Bearings #2 | 8 min | Medium | After a brief break |
| §6 — Versions That Are Allowed to Disagree | 20 min | **High** | Peak attention — start of a fresh session |
| §7 — The One Backup That Matters | 10 min | Medium | When alert |
| ☆ Taking Your Bearings #3 | 8 min | Medium | After a brief break |
| §8 — Rules, or Consequences | 8 min | Low | Anytime |
| Practice Questions | 25 min | Medium | When alert |

**Attention Cost Key:**
- **Low:** concrete, familiar concepts — study anytime
- **Medium:** new concepts requiring focus — study when alert
- **High:** abstract or dense material — study at peak attention

*If you only have 15 minutes: read §2's gate sequence and §6's skew table, then work ☆ Taking Your Bearings #3. That is where this chapter's exam points actually live. §1, §4 and §5 are recognition material you will mostly get right on instinct.*

**On the session split:** the recommended break after Bearings #2 puts the request path and the node in one session, and versions, disaster and synthesis in the other. It also isolates §6, the densest pure-recall block in this book, at the start of a fresh session, which is where it belongs.

---

> *"A watch is not a task you finish. It is a stretch of time during which the ship is your responsibility, and the log records what you did about it."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score determines how to approach the content; there is no shame in any score, only different reading strategies. Several of these ask you to reason rather than recall. Answer in your own words. One sentence is enough.

1. You have a command-line tool on your laptop that manages a server somewhere else. Before it can do anything at all, what does it need to know, and what changes when you become responsible for two of those servers instead of one?

2. Chapter 3 was emphatic that one component is the only way into a Kubernetes cluster — nothing else is designed to expose a remote service. Name that component, and say what that architecture implies about where you would put a security check.

3. A server receives a request to do something expensive. List the distinct questions it must answer before it does the work. Then say whether any of those questions could result in the request being *changed*, rather than simply accepted or refused.

4. Chapter 4 said namespaces are intended for environments with many users spread across teams or projects, and it named the mechanism by which cluster resources get divided between them. What was that mechanism called, and what do you think it constrains?

5. Chapter 7's built-in taint table included `node.kubernetes.io/unschedulable`, with a `NoSchedule` effect: a taint applied deliberately by an operator rather than automatically by a failing disk. Using Chapter 7's rule about that effect, what did it do to the Pods *already running* on the node?

6. Chapter 4 pointed at the `kube-node-lease` namespace and said the Lease objects in it are how the control plane knows a node is still alive. If those Leases stop being renewed, what *should* the control plane conclude, and what should it be careful not to conclude?

7. Two components of one system are running at different versions. One is a client, one is a server. Which direction of mismatch worries you more — a newer client talking to an older server, or an older client talking to a newer server — and why?

8. You run a service on a cloud provider's managed platform. A colleague runs the same service on hardware in a rack they own. Name one operational duty that sits with whoever operates the control plane in each case.

<details>
<summary>Answers + reading strategy</summary>

1. **An address and a credential, at minimum.** With two servers, *which* server becomes a piece of state you have to carry somewhere, which means the tool needs a notion of *current* target as well as *possible* targets.

2. **The kube-apiserver.** If every request in the cluster must pass through one component, that component is the natural and sufficient place to put access control. One door means one set of locks.

3. **Score this one correct if you produced three or more distinct questions, or if you answered "yes" to the "changed" clause.** Most readers produce two — *who are you*, and *are you allowed* — and say no. If that was you, score it incorrect and read §2 slowly: the third question is the one this chapter exists to give you, and the "changed" clause is the property that makes it a different kind of check rather than a third variation on "no."

4. **Resource quota.** Most readers will say it constrains "how much a team can use," which is right as far as it goes. Hold on to what you guessed; §3 will sharpen it.

5. **Nothing.** `NoSchedule` means no new Pods will be scheduled on the tainted node unless they have a matching toleration, and Pods currently running on the node are not evicted [source: k8s-docs-taints-tolerations-2026-08-23]. That raises an obvious follow-up question, which §4 answers.

6. **It should conclude that it cannot tell.** An absent heartbeat is evidence of a *communication* failure, which could be a dead node or could be a network partition. Concluding "the node is broken" claims more than the evidence supports.

7. **A newer client talking to an older server is the more dangerous direction:** the client can ask for things the server has never heard of. That intuition is correct in general and, for exactly one component in Kubernetes, wrong. §6 names it.

8. **Any duty that moves when somebody else runs the control plane counts.** Upgrade timing and etcd backup are the two this chapter can defend; which further duties move is a per-provider question rather than a documented split, so a broad answer is a pass here.

**If you got 6+ right:** skim. Read §2 and §6 properly — they carry this chapter's exam points — and work all three Taking Your Bearings checkpoints. The rest you can move through quickly.

**If you got 3–5 right:** read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** read carefully, and if questions 2, 4, 5 and 6 were among your misses, re-read *[cross-bearing: see Ch 3 §5 — the API server and the only door in]* and *[cross-bearing: see Ch 4 §3 — namespaces and cluster-scoped objects]* before you start §2. Those two sections are the prerequisite base for more than half this chapter. Without Chapter 3's single-door architecture in place, §2 will read as an arbitrary list of three words.

</details>

---

## Why This Chapter Matters

`kubectl cordon node-7`.

Three words, and a machine goes out of service without disturbing a single running process. Chapter 7 ended by naming the *act*, telling you the command was this chapter's opening move, and declining to give it. Here it is.

The shape is the more interesting thing, though. You have been typing commands in exactly this form since Chapter 3 (`kubectl apply -f`, `kubectl get pods`, `kubectl scale`) and nobody has told you what the form *is*. It worked anyway. That is precisely the condition under which a candidate walks into the exam room confident and then loses five points to a question about which component is permitted to be one minor version newer than which.

Chapters 2 through 7 made you someone who can describe what should run and where. This chapter makes you someone responsible for the thing it runs on. That is a different posture, and the vocabulary shifts with it: on watch, you think in three questions — what can I take out of service safely, what can I stop other people doing, and what can I not get back. You are about to acquire all three.

And here is the doubt worth carrying through the next eight sections. By the end of this chapter you will not have learned a single new mechanism. Every administrative act in it — taking a node out of service, capping a team's resource consumption, registering a machine, refusing a malformed request — is a write through a door you already know, reconciled by a controller you already met. That claim should be hard to believe right now, because what follows looks like four unrelated subjects wearing one chapter number. §8 will make the case. Until then, keep score.

The stakes, stated plainly: about five points on this book's allocation, which is not many. What the number understates is the *shape* of those points. §6's version-skew material is the single most mechanically checkable block in the entire curriculum. The rules are exact, the numbers are small, and there is no partial credit for nearly remembering them, which makes it the easiest place in the exam to lose points you had every opportunity to keep. That is the whole case for reading this chapter carefully, and it does not need inflating.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Decompose** any `kubectl` command into its four slots, and say where the tool found the cluster it just talked to.
- **Trace** a request through the three gates it passes before anything is written down, and say what each gate can and cannot do about it.
- **Distinguish** a ResourceQuota from a LimitRange by what each constrains and at what scope, and say which of the two can make a previously valid Pod stop being accepted.
- **Take** a node out of service and put it back, predicting what happens to the Pods on it at each step.
- **State** which Kubernetes components are permitted to disagree about their version, by how much, and in which direction.
- **Recognize** every administrative act in this chapter as a write through one door, reconciled by a controller you already know, which is the only thing you actually have to remember.

*You'll also stop reading the version-skew table as arbitrary trivia. That is a smaller change than it sounds, and it is worth more exam points than anything else in Part II.*

---

## ⚪ §1 — The Grammar of a Command

You have been typing these for four chapters.

`kubectl apply -f deployment.yaml`. `kubectl get pods`. `kubectl scale deployment web --replicas=5`. Every one of them worked. Nobody told you what the shape was, and you did not need to be told, which is exactly why it earns ten minutes now.

Here is the shape. Every `kubectl` invocation takes the form `kubectl [command] [TYPE] [NAME] [flags]` [source: k8s-docs-kubectl-overview-2026-08-23]. Four slots, and only the first is mandatory:

- **command** — the operation you want performed on one or more resources: `create`, `get`, `describe`, `delete` [source: k8s-docs-kubectl-overview-2026-08-23].
- **TYPE** — the resource type [source: k8s-docs-kubectl-overview-2026-08-23].
- **NAME** — the name of the specific resource. If the name is omitted, details for all resources are displayed [source: k8s-docs-kubectl-overview-2026-08-23].
- **flags** — optional. Flags you specify on the command line override default values and any corresponding environment variables [source: k8s-docs-kubectl-overview-2026-08-23].

Put five commands you have already run through those same four slots, and the shape appears retroactively.

<!-- FIGURE: ch08-fig01-kubectl-verb-resource-grammar -->
![A five-column table aligning five kubectl commands on the slots kubectl, command, TYPE, NAME and flags; some cells are empty because those commands omit those slots; two arrows below point up at the TYPE column labelled case-insensitive and the NAME column labelled case-sensitive](figures/ch08-fig01-kubectl-verb-resource-grammar.svg)

<!-- ASCII-FALLBACK
```
  kubectl   [command]        [TYPE]        [NAME]      [flags]
            ─────────        ──────        ──────      ───────

  kubectl   cordon                         node-7
  kubectl   get              pods
  kubectl   apply                                      -f deploy.yaml
  kubectl   scale            deployment    web         --replicas=5
  kubectl   describe         node          worker-3

                                ▲             ▲
                    case-INsensitive     case-SENSITIVE
                    singular = plural    node-7 ≠ Node-7
                    = abbreviated
```
-->

**Figure 8.1 —** Five commands you already know, aligned on the same four slots. What to notice is the empty columns: `kubectl get pods` omits NAME and flags, and gets every Pod as a result. What to notice second is the asymmetry at the bottom, which is the examinable half of this section.

That asymmetry earns its own sentence, because it is the exact shape of an exam distractor. Resource types are case-insensitive, and you may use the singular, plural, or abbreviated form [source: k8s-docs-kubectl-overview-2026-08-23]. Resource *names* are case-sensitive [source: k8s-docs-kubectl-overview-2026-08-23]. The tool is relaxed about what kind of thing you meant and exacting about which one.

> ★ **Fixed Point:** One grammar, four slots — `kubectl [command] [TYPE] [NAME] [flags]`. **Resource types are case-insensitive and abbreviable. Resource names are case-sensitive.**

### The verb surface

Here is the operations table. Read it as an inventory rather than a list of new things; you have met a third of it already.

| Verb | What it does | Where it lives in this book |
|---|---|---|
| `get` | List one or more resources | Ch 3, then throughout |
| `describe` | Display the detailed state of one or more resources | Ch 5, then throughout |
| `apply` | Apply a configuration change to a resource from a file or stdin | Ch 4 |
| `create` | Create one or more resources from a file or stdin | Ch 4 |
| `delete` | Delete resources from a file, stdin, or by label selector, name, or resource | Ch 4 |
| `logs` | Print the logs for a container in a Pod | ahead, in Ch 13 |
| `exec` | Execute a command against a container in a Pod | ahead, in Ch 16 |
| `scale` | Update the size of the specified replication controller / deployment | Ch 6 |
| `rollout` | Manage the rollout of a resource (deployments, daemonsets, statefulsets) | Ch 6 |
| `explain` | Get documentation of various resources | here |
| `config` | Modify kubeconfig files | here |

*(All verbs and descriptions: [source: k8s-docs-kubectl-overview-2026-08-23].)*

One entry deserves a sentence of its own. `explain` gets documentation of various resources [source: k8s-docs-kubectl-overview-2026-08-23], which makes it the only verb in the table that answers a question about *the resource type* rather than a question about *your cluster*.

> ⚓ **Worth Securing:** `kubectl explain` is the entry in this table that pays off longest. Because it returns documentation for a resource type rather than the contents of your cluster, it works on types you have never seen, including the CustomResourceDefinitions of Chapter 6 §8, installed by tools that did not exist when this book was written. Two years from now it will still be the fastest way to find out what a field does.

*[cross-bearing: see Ch 4 §1 — apply, and the declarative model]*. Chapter 4 gave `apply` a single sentence and sent you here for the rest. This table is that payoff, and Chapter 4's larger point stands unchanged: the objects are declarations, and the imperative verbs work by changing declarations. *[cross-bearing: see Ch 6 §2 — kubectl scale as a write to .spec.replicas]*.

### Where the cluster came from

The second real idea in this section is a question you have never had to ask, because the answer was already on your machine.

For configuration, `kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag [source: k8s-docs-kubectl-overview-2026-08-23]. That is the precedence, stated flat: a default location, an environment variable, and a flag. Per the general rule above — flags specified on the command line override default values and any corresponding environment variables — the flag wins over the environment variable [source: k8s-docs-kubectl-overview-2026-08-23].

If you answered Soundings question 1 with "an address and a credential," this is where that instinct lands. The file holds both, plus the answer to the two-server problem: which one you are currently talking to. That last part has a name — a **context** is one named bundle of cluster, user and namespace, and the **current context** is the one `kubectl` uses when you do not say otherwise. A kubeconfig can hold many; you are always working inside exactly one.

### The surprising case: `kubectl` inside a Pod

By default `kubectl` first determines whether it is running within a Pod, and thus inside a cluster. It starts by checking for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables, and for the existence of a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are found, in-cluster authentication is assumed [source: k8s-docs-kubectl-overview-2026-08-23]. And when `kubectl` runs in a cluster it acts against the namespace of the ServiceAccount, unless `--namespace` is given [source: k8s-docs-kubectl-overview-2026-08-23].

Chapter 4 used the second half of that fact once, in passing, in an answer key. Here it is in full: three environment checks, an assumed identity, and a different default namespace.

> 🪝 **Snag:** `kubectl` inside a Pod does not use your kubeconfig, is not you, and does not default to the `default` namespace. It authenticates as the Pod's ServiceAccount and looks in that ServiceAccount's namespace. Every practitioner who has ever run a debugging shell inside a cluster has been surprised by this at least once, usually by an empty `kubectl get pods` that they were certain should have returned something.

### The command that opens the chapter

`kubectl cordon node-7`.

Verb, resource name. The grammar, instantiated: the project's own reference gives the usage as `kubectl cordon NODE` with the synopsis "Mark node as unschedulable" [source: k8s-docs-kubectl-cordon-2026-08-24], which is the four-slot shape with TYPE and flags both empty. This is the thing Chapter 7 promised would be Chapter 8's opening move *[cross-bearing: see Ch 7 §4 — the built-in taint node.kubernetes.io/unschedulable]*. What it does is what Chapter 7 already told you: it marks a node unschedulable, preventing the scheduler from placing new Pods onto that Node, without affecting the existing Pods on the Node [source: k8s-docs-nodes-2026-08-23].

That is all this section will say about it. Everything else belongs to §4: what it writes, what it does *not* do, what the second command is, and what happens if you skip that second command *[cross-bearing: see Ch 8 §4 — taking a node out of service]*. Carry the question with you; three sections from now it will have a better answer than it would have here.

---

## 🔵 §2 — Three Gates and a Logbook

Soundings question 3 asked you to list the distinct questions a server must answer before doing expensive work. If you produced two — *who are you*, and *are you allowed* — you produced the answer nearly everyone produces, and you have just located a hole in your own model. That is a good place to start reading from, and it deserves naming rather than skipping past: a reader who has just discovered their model is incomplete is the most receptive reader this chapter gets.

There are three.

Chapter 3 named them in passing, at the point the API server was introduced, and pointed here for the treatment *[cross-bearing: see Ch 3 §5 — the API server and the only door in]*. The project's documentation is unambiguous that these are stages of one request path rather than three parallel checks: "When a request reaches the API, it goes through several stages" [source: k8s-docs-controlling-access-2026-08-24], and the page presents them as sequential sections — transport security, authentication, authorization, admission control, auditing [source: k8s-docs-controlling-access-2026-08-24]. The cluster-administration guidance on securing a cluster lists the same material in the same order — Controlling Access to the Kubernetes API, Authenticating, Authorization, Using Admission Controllers, and Auditing [source: k8s-docs-cluster-administration-2026-08-23] — and the project's extension-point taxonomy names three of them as the API access extensions: authentication, authorization, and dynamic admission control via webhooks [source: k8s-docs-extending-kubernetes-2026-08-23].

This chapter compresses that to three gates and a logbook. The project's own page opens with a fourth stage before any of them: transport security, in which the API server listens on port 6443 on the first non-localhost network interface, protected by TLS [source: k8s-docs-controlling-access-2026-08-24]. That is a real stage, and it is covered inside gate one below rather than given a box of its own.

### Gate one: authentication — *who are you?*

Authentication establishes the identity behind the request. The cluster creation script or cluster admin configures the API server to run one or more Authenticator modules [source: k8s-docs-controlling-access-2026-08-24], and the input to the authentication step is the entire HTTP request, though it typically examines the headers and/or client certificate [source: k8s-docs-controlling-access-2026-08-24]. The API server is configured to listen for remote connections on a secure HTTPS port, typically 443, with one or more forms of client authentication enabled [source: k8s-docs-control-plane-node-communication-2026-08-24].

Two facts about this gate are worth carrying. First, its failure mode is specific: if the request cannot be authenticated, it is rejected with HTTP status code 401 [source: k8s-docs-controlling-access-2026-08-24]. Second, a small surprise — while Kubernetes uses usernames for access control decisions and in request logging, it does not have a `User` object [source: k8s-docs-controlling-access-2026-08-24]. Identity here is a property of a request, not a record in the datastore.

The two identities you already have in the cluster arrive at this gate by different routes. Nodes should be provisioned with the public root certificate for the cluster, so that they can connect securely to the API server, along with valid client credentials; a good approach is for the kubelet's client credentials to take the form of a client certificate [source: k8s-docs-control-plane-node-communication-2026-08-24]. Automating the provisioning of those certificates is what kubelet TLS bootstrapping is for [source: k8s-docs-control-plane-node-communication-2026-08-24]. Pods, meanwhile, connect by leveraging a ServiceAccount: Kubernetes automatically injects the public root certificate and a valid bearer token into the Pod when it is instantiated [source: k8s-docs-control-plane-node-communication-2026-08-24]. That injected token is the same file `kubectl` looks for in §1 when it decides it is running inside a cluster.

### Gate two: authorization — *may you do this?*

Authorization decides whether the identity established at gate one is permitted to perform *this action* on *this object*. A request must include the username of the requester, the requested action, and the object affected by the action [source: k8s-docs-controlling-access-2026-08-24]. One or more forms of authorization should be enabled, especially if anonymous requests or ServiceAccount tokens are allowed [source: k8s-docs-control-plane-node-communication-2026-08-24]. Securing your cluster means implementing effective authentication *and* authorization for API access: the pair, not either alone [source: k8s-docs-cloud-native-security-2026-08-23].

RBAC is one authorizer among several — Kubernetes supports multiple authorization modules, such as ABAC mode, RBAC Mode, and Webhook mode [source: k8s-docs-controlling-access-2026-08-24] — and RBAC in full is Chapter 12's material *[cross-bearing: see Ch 12 §3 — Role, ClusterRole, and the binding model]*. For now, one fact about it is enough: it is a mechanism that lives at this gate, and this gate's inputs are an identity, a verb, and an object — not the contents of your YAML.

Note the gate's quorum rule, because §3 and the third gate both turn on the contrast: if any module authorizes the request, then the request can proceed; if all of the modules deny the request, then the request is denied, with HTTP status code 403 [source: k8s-docs-controlling-access-2026-08-24].

### Gate three: admission control — *should this, exactly as written, be allowed?*

This is the gate you did not have.

Admission control modules are software modules that can modify or reject requests [source: k8s-docs-controlling-access-2026-08-24], and unlike the first two gates they can access the contents of the object that is being created or modified [source: k8s-docs-controlling-access-2026-08-24]. They sit before persistence: once a request passes all admission controllers, it is validated using the validation routines for the corresponding API object, and then written to the object store [source: k8s-docs-controlling-access-2026-08-24].

And here is the property that makes them a genuinely different kind of thing rather than a third variation on "no." Authentication and authorization answer yes or no. Admission may answer yes, no, or *yes — but not as you wrote it*: admission controllers can also set complex defaults for fields [source: k8s-docs-controlling-access-2026-08-24].

> ★ **Fixed Point:** Authentication, then authorization, then admission. Authentication asks **who**. Authorization asks **may you**. Admission asks **should this, exactly as written, be allowed to happen** — and it is the only one of the three that can change your request instead of refusing it [source: k8s-docs-controlling-access-2026-08-24].

<!-- FIGURE: ch08-fig02-three-api-gates -->
![Three boxes in a row labelled Authentication, Authorization and Admission, with a request arrow entering on the left and persistence to etcd on the right; each box has a downward arrow to a REJECT outcome, and the Admission box has an additional arrow labelled REWRITTEN that loops back into the forward path](figures/ch08-fig02-three-api-gates.svg)

<!-- ASCII-FALLBACK
```
                gate 1              gate 2              gate 3
           ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
 request ─►│Authentication├──►│Authorization ├──►│  Admission   ├──► persisted
           └──────┬───────┘   └──────┬───────┘   └──┬───────┬───┘     to etcd
                  │                  │             │       │              ▲
                  ▼                  ▼             ▼       │              │
               REJECT             REJECT        REJECT     └── REWRITTEN ─┘
```
-->

**Figure 8.2 —** What to notice is the fourth arrow. Gates one and two have one way out other than forward: refusal. Gate three has two. It can refuse, or it can alter the request and let the altered version continue. The three questions, in order, are: *who are you*, *may you do this*, and *should this, as written, be allowed*.

> 🪢 **Mnemonic:** *Who, may, and how.* Three words, in order, one per gate. The third is the odd one because "how" is a question about the request rather than about you.

> ⚠ **Navigational Hazards:** Authorization and admission are not two names for the same check, and the sharpest proof is that they disagree about what counts as a decision. **Authorization is any-module-approves:** if any module authorizes the request, it proceeds; only if all modules deny is it refused [source: k8s-docs-controlling-access-2026-08-24]. **Admission is any-module-rejects:** unlike authentication and authorization modules, if any admission controller module rejects, the request is immediately rejected [source: k8s-docs-controlling-access-2026-08-24]. One gate is a vote you can win with a single supporter; the next is a veto any participant can exercise. A request can be fully authenticated, entirely authorized, and still be refused — or quietly rewritten — at the third gate.

> 🔭 **Closer Look:** Admission controllers act on requests that create, modify, delete, or connect to (proxy) an object. They do not act on requests that merely read objects [source: k8s-docs-controlling-access-2026-08-24] — reads bypass the admission control layer entirely [source: k8s-docs-admission-controllers-2026-08-24]. So the whole of this gate is invisible to `kubectl get`, which is deeper than the exam requires and explains a great deal of otherwise-baffling behavior the first time you install a policy engine.

> **Extended Analogy:** Think of a working commercial harbour rather than a locked building. A vessel arriving is met first by a pilot boat, whose only question is *which vessel is this*: papers, registration, identity. That is authentication. It has no view on your business here.
>
> Once identified, the harbourmaster consults the berth allocations: is this vessel entitled to a berth in this harbour today? That is authorization. The harbourmaster does not open a single crate. The question is about standing, not about cargo.
>
> Then, and only then, the customs officer comes aboard. This one *does* open crates. She may find something prohibited and turn the whole vessel around. But she has a third option the other two lack: she may say the vessel can dock provided a particular container stays sealed, or provided a declaration is completed and attached before unloading. The vessel proceeds — altered. That is admission control, and the third option is the entire reason it is a separate office rather than one more line on the harbourmaster's form.

### Two admission controllers you have already met

This is not an abstraction you have to take on faith. You have seen it work twice.

Chapter 7 introduced the **NodeRestriction** admission plugin, which prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix [source: k8s-docs-assign-pod-node-2026-08-23]: the reason you can trust node-isolation labels not to have been forged by the node they describe. It is an admission controller by name in the project's own plugin reference — NodeRestriction limits the Node and Pod objects a kubelet can modify [source: k8s-docs-admission-controllers-2026-08-24]. Chapter 7 stated the rule and pointed here for the enforcement *[cross-bearing: see Ch 7 §3 — node labels and the NodeRestriction plugin]*. This gate is the enforcement.

And the Pod Security Standards are enforced by the built-in Pod Security Admission controller [source: k8s-docs-pod-security-standards-2026-08-23]. That is one clause and no more; Chapter 12 owns the three profiles and the three modes *[cross-bearing: see Ch 12 §6 — Pod Security Standards and Pod Security Admission]*. What matters here is the derivation: when you meet Pod Security Admission four chapters from now, you will not be learning a new kind of thing. You will be learning one instance of the third gate.

The same is true of §3's material, arriving next. ResourceQuota is an admission controller that observes the incoming request and ensures that it does not violate any of the constraints enumerated in the ResourceQuota object [source: k8s-docs-admission-controllers-2026-08-24], and LimitRanger does the same for the constraints in a LimitRange object [source: k8s-docs-admission-controllers-2026-08-24]. Neither is a separate subsystem with its own enforcement path; both take effect at this gate.

> 🔭 **Closer Look:** Dynamic admission control means the cluster calls out to a webhook *you* supplied. Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend, and the documentation is candid that this adds a potential point of failure [source: k8s-docs-extending-kubernetes-2026-08-23]. Which is to say: once you install a validating webhook, your webhook being down is a thing that can stop your cluster accepting requests.

### And a logbook

Alongside the three gates, the cluster-administration guidance on securing a cluster lists **Auditing** [source: k8s-docs-cluster-administration-2026-08-23]. It sits in the same list, at the same level, as the three access-control pages.

Kubernetes auditing provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster [source: k8s-docs-audit-2026-08-24]. It allows cluster administrators to answer what happened, when it happened, who initiated it, on what it happened, where it was observed, from where it was initiated, and to where it was going [source: k8s-docs-audit-2026-08-24].

And one detail restates this section's architecture a fourth time: audit records begin their lifecycle inside the kube-apiserver component, and each request on each stage of its execution generates an audit event [source: k8s-docs-audit-2026-08-24]. The logbook is not a separate observer watching the door. It is kept *by* the door.

### Why three gates at one door is a complete story

Close on the architecture, because it is the reason this section is short enough to be learnable.

Kubernetes has a hub-and-spoke API pattern. All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24].

That is the load-bearing sentence. Three gates on one door would be an incomplete access-control story if there were other doors; you would be securing one entrance out of several. There are not. Chapter 3's single-door architecture is what makes a three-gate model *sufficient* rather than merely *present*, and it is why this chapter has a spine at all *[cross-bearing: see Ch 8 §8 — one door, and controllers behind it]*.

---

## 🔵 §3 — Dividing a Shared Cluster

Chapter 7 §2 left you with a complaint and an IOU. The complaint: nothing in what you had learned so far stops you booking the entire cluster with resource requests you will never actually use. The IOU: the mechanisms that stop *other people* doing that to *you* live here *[cross-bearing: see Ch 7 §2 — requests, and the cluster you could book by accident]*.

There are two of them, and the only mistake worth guarding against is swapping them.

### ResourceQuota — a ceiling on a namespace

When several users or teams share a cluster with a fixed number of nodes, there is a concern that one team could use more than its fair share of resources [source: k8s-docs-resource-quotas-2026-08-24]. A resource quota, defined by a ResourceQuota object, provides constraints that limit **aggregate resource consumption per namespace** [source: k8s-docs-resource-quotas-2026-08-24]. That is the sentence Chapter 4 gave you in outline — namespaces are a way to divide cluster resources between multiple users, via resource quota [source: k8s-docs-namespaces-2026-08-23] — now stated at full strength *[cross-bearing: see Ch 4 §3 — namespaces, and what they are for]*.

A cluster administrator creates at least one ResourceQuota for each namespace; users create resources in the namespace, and the quota system tracks usage to ensure it does not exceed hard resource limits [source: k8s-docs-resource-quotas-2026-08-24]. If creating or updating a resource violates a quota constraint, the control plane rejects that request with HTTP status code `403 Forbidden` [source: k8s-docs-resource-quotas-2026-08-24].

What can a quota count? Three families, and you need the shape rather than the roster:

- **Compute totals** — `requests.cpu`, `requests.memory`, `limits.cpu`, `limits.memory`, and `hugepages-<size>`, with `cpu` and `memory` as aliases for the two request forms [source: k8s-docs-resource-quotas-2026-08-24].
- **Storage** — `requests.storage` and `persistentvolumeclaims`, optionally scoped per StorageClass [source: k8s-docs-resource-quotas-2026-08-24].
- **Object counts** — written `count/<resource>` for core API group resources and `count/<resource>.<group>` otherwise; countable resources include `count/pods`, `count/services`, `count/secrets`, `count/configmaps` and `count/deployments.apps` [source: k8s-docs-resource-quotas-2026-08-24].

One quota rule is worth more exam points than the rest of the section combined, because it changes what a valid manifest is:

> ★ **Fixed Point:** **If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients must specify either `requests` or `limits` for that resource, for every new Pod you submit. If you don't, the control plane may reject admission for that Pod** [source: k8s-docs-resource-quotas-2026-08-24].

Read that as a consequence rather than a rule to memorize. A quota is a ceiling on a total; a total can only be computed if every contributor declares its share. A Pod that declares nothing is not a small Pod — it is an *uncountable* one, and the quota system cannot let it through.

Note also what a quota is not: ResourceQuotas are independent of the cluster capacity, so if you add nodes to your cluster, this does not automatically give each namespace the ability to consume more resources [source: k8s-docs-resource-quotas-2026-08-24].

### LimitRange — a rule about an object

A LimitRange is a policy to constrain the resource allocations — limits and requests — that you can specify for **each applicable object kind**, such as Pod or PersistentVolumeClaim, in a namespace [source: k8s-docs-limit-range-2026-08-24]. Four things it provides [source: k8s-docs-limit-range-2026-08-24]:

- enforce minimum and maximum compute resource usage per Pod or Container in a namespace;
- enforce minimum and maximum storage request per PersistentVolumeClaim;
- enforce a ratio between request and limit for a resource;
- **set default request/limit values for compute resources in a namespace and automatically inject them into Containers at runtime.**

The administrator creates a LimitRange in a namespace; users then create objects in that namespace [source: k8s-docs-limit-range-2026-08-24]. Two things happen in order: first, the LimitRange admission controller applies default request and limit values for all Pods (and their containers) that do not set compute resource requirements; second, the LimitRange tracks usage to ensure it does not exceed the resource minimum, maximum and ratio defined in any LimitRange present in the namespace [source: k8s-docs-limit-range-2026-08-24]. A violation fails with the same `403 Forbidden` a quota violation produces, plus a message explaining the constraint that has been violated [source: k8s-docs-limit-range-2026-08-24].

The timing is worth one sentence, because it is the mutate-versus-reject distinction of §2 arriving one gate later in the same request's life: **LimitRange validations occur only at Pod admission stage, not on running Pods** — if you add or modify a LimitRange, the Pods that already exist in that namespace continue unchanged [source: k8s-docs-limit-range-2026-08-24].

### The discrimination, made structural

Definitions are easy to swap. Questions are harder. If you can answer these two about a mechanism, you will never confuse them again:

**What is being counted?** The quota counts the namespace's aggregate total [source: k8s-docs-resource-quotas-2026-08-24]. The LimitRange counts one object's numbers [source: k8s-docs-limit-range-2026-08-24].

**What happens to a manifest that says nothing about resources?** In a quota'd namespace, the control plane may reject it [source: k8s-docs-resource-quotas-2026-08-24]. Under a LimitRange, the admission controller fills it in [source: k8s-docs-limit-range-2026-08-24].

> ★ **Fixed Point:** **ResourceQuota counts the namespace. LimitRange constrains the object.** One is a ceiling on a team; the other is a rule about a manifest.

<!-- FIGURE: ch08-fig05-quota-vs-limitrange -->
```
        ResourceQuota                            LimitRange
 ┌────────────────────────────┐      ┌────────────────────────────┐
 │ namespace: team-atlas      │      │ namespace: team-atlas      │
 │  ┌────┐┌────┐┌────┐┌────┐  │      │ ┌─────┐┌─────┐┌─────┐┌────┐│
 │  │Pod ││Pod ││Pod ││Pod │  │      │ │ Pod ││ Pod ││ Pod ││Pod ││
 │  └────┘└────┘└────┘└────┘  │      │ │min ≤││min ≤││min ≤││min≤││
 │  ═══ namespace total ════  │      │ │≤ max││≤ max││≤ max││≤max││
 │  ═══════ AT CAP ═════════  │      │ └─────┘└─────┘└─────┘└────┘│
 └────────────────────────────┘      └────────────────────────────┘
              ▲                                    ▲
       5th Pod arrives:                 5th Pod arrives declaring
         REJECTED 403                   nothing:  ACCEPTED — with
   the namespace total is reached         defaults FILLED IN
```

**Figure 8.3 —** Both mechanisms live inside one namespace; the boundary is the same on each side and is not the discrimination. What differs is what is being counted and how it fails. On the left, one aggregate total for the namespace, and a fifth Pod rejected at the cap. On the right, per-object bounds on each Pod, and a fifth Pod that declares nothing is not refused but modified.

> 🪝 **Snag:** A LimitRange that supplies a default request changes what your manifest means without changing your manifest. The Pod you get is not the Pod you wrote, and `kubectl get pod <name> -o yaml` is where you find out. Two aggravating details: a LimitRange does not check the consistency of the default values it applies [source: k8s-docs-limit-range-2026-08-24], and if two or more LimitRange objects exist in the namespace, it is not deterministic which default value will be applied [source: k8s-docs-limit-range-2026-08-24].

> ⚓ **Worth Securing:** The two are usually deployed together, and the sources make the reason explicit rather than leaving it to intuition. A quota'd namespace *forces* Pods to declare requests or limits [source: k8s-docs-resource-quotas-2026-08-24] — and you can use a LimitRange to automatically set a default request for these resources [source: k8s-docs-resource-quotas-2026-08-24]. The quota sets the ceiling and makes declaration compulsory; the LimitRange makes sure a developer who forgets still ends up with a Pod that is countable. That is why the Kubernetes security guidance names them in one breath: define ResourceQuotas to fairly allocate shared resources, and use LimitRanges to ensure that Pods specify their resource requirements [source: k8s-docs-cloud-native-security-2026-08-23].

*[cross-bearing: see Ch 5 §8 — requests and limits, the numbers a LimitRange defaults]*

### The hinge, and it is worth thirty seconds

ResourceQuota and LimitRange are namespaced objects. The Nodes that §4 is about to discuss are not.

Chapter 4 established this and you may already feel where it goes: namespace-based scoping is applicable only for namespaced objects — Deployments, Services and so on — and not for cluster-wide objects such as StorageClass, Nodes and PersistentVolumes [source: k8s-docs-namespaces-2026-08-23].

So the two halves of "stop people using too much" sit on opposite sides of a boundary you already know. **You can quota a team. You cannot quota a machine.** A quota is a statement about a namespace, and every resource it can count is a namespaced one; a Node is not in a namespace, so no ResourceQuota reaches it.

Say that out loud once, because Chapter 12 is going to *derive* the RBAC four-way matrix from exactly this boundary rather than asking you to memorize four combinations *[cross-bearing: see Ch 12 §3 — namespaced and cluster-scoped permissions]*.

And one closing observation, offered rather than promised: both of these mechanisms are admission controllers [source: k8s-docs-admission-controllers-2026-08-24]. Neither is a separate subsystem with its own enforcement path. That is the first installment of a claim §8 will finish.

---

## ☆ Taking Your Bearings #1 — The Path a Command Takes In

Five questions on §1 through §3. Answer in your own words before checking; the effort of retrieval is what makes this stick.

**1.** ⚪ Decompose `kubectl describe node worker-3` into its four slots and name each one. Then say which of the four you could change the capitalization of without breaking the command.

**2.** ⚪ You run `kubectl get pods` from a shell on your laptop, and again from inside a running Pod in the same cluster. Both succeed and return different results. Explain *both* differences — what identity each invocation used, and what namespace each looked in.

**3.** 🔵 Name the three gates a request passes, in order. Then say which of them can result in the request being *changed* rather than accepted or rejected.

**4.** 🔵 A request is refused. You are told that the identity was valid, and that the identity had permission to perform this action on this resource. Which gate refused it, and give one plausible reason.

**5.** 🔵 **[retrieval: ch4]** Chapter 4 said namespaces are the unit by which cluster resources get divided between users, and it named the mechanism. Name it, say what scope it constrains — and then say what the *other* mechanism in §3 constrains instead.

<details>
<summary>Answers + explanations</summary>

**1.** `kubectl` / `describe` (command) / `node` (TYPE) / `worker-3` (NAME); there are no flags. **You could capitalize the TYPE freely**, since resource types are case-insensitive and accept singular, plural or abbreviated forms. You could not capitalize the name; names are case-sensitive.

*Common wrong turns:* "both are case-insensitive" and "both are case-sensitive" are the two tempting symmetrical answers, and the asymmetry is the whole point. `Node worker-3` works. `node Worker-3` does not.

**2.** From your laptop: `kubectl` used the kubeconfig at `$HOME/.kube/config` (or whatever `KUBECONFIG`/`--kubeconfig` pointed at), authenticated as *you*, and looked in the namespace of the current context. From inside the Pod: `kubectl` found `KUBERNETES_SERVICE_HOST`, `KUBERNETES_SERVICE_PORT` and the ServiceAccount token file, assumed in-cluster authentication, authenticated as the **ServiceAccount**, and looked in the **ServiceAccount's namespace**. Two different identities, two different namespaces, one command.

**3.** **Authentication, then authorization, then admission control.** Only admission can change the request.

The reason this matters is not that the third gate has an extra feature. It is the *reason there are three gates rather than one*. Two of them are asking about you and answering yes or no; the third is asking about the request itself and has a third answer available: yes, in modified form. When you meet Pod Security Admission in Chapter 12, you will be meeting an instance of this gate, and you will not have to learn a new kind of thing.

*Common wrong turns:* a two-gate answer (the most common incomplete model, and the one Soundings question 3 was built to expose); the order reversed; and attributing the mutation power to authorization.

**4.** **Admission.** Both earlier gates already said yes — the identity was established and the action was permitted — so the refusal came from the gate that looks at the request's *contents*. A plausible reason: the Pod would have exceeded its namespace's ResourceQuota, or a policy plugin rejected something about the object as written.

One plausible cause is enough. There is no need to enumerate admission controllers; the full plugin surface is out of scope here and Chapter 12 owns the policy landscape.

**5.** **ResourceQuota**, which constrains **aggregate resource consumption per namespace**. The other mechanism is **LimitRange**, which constrains **each applicable object kind** in a namespace and supplies defaults so that Pods specify their resource requirements at all.

*Common wrong turn:* swapping them, which is the only real error available here. If you find the two blurring, hold the failure modes rather than the definitions: a quota's answer to an undeclared Pod is `403`; a LimitRange's answer is to fill the numbers in.

</details>

**How'd you do?**

**5/5:** You have the request path. Move on to §4 with confidence.
**3–4:** Solid. Review the ones you missed, particularly if question 3 was among them, since §4 through §8 all lean on the gate model.
**0–2:** No shame in it, but do not continue yet. Re-read §2 before §4, about ten minutes. If question 5 was a miss as well, spend five more on §3's hinge. Everything from here builds on the idea that administrative acts are ordinary writes that pass ordinary gates.

**Checkpoint: you've now mastered**
✓ The four-slot grammar, and the case-sensitivity asymmetry inside it
✓ Where `kubectl` finds its cluster — on a laptop and inside a Pod
✓ The three gates, in order, and which one can rewrite you
✓ ResourceQuota versus LimitRange, by scope and by failure mode
☐ Taking a node out of service (next)

---

## 🔵 §4 — Taking a Node Out of Service

You have been carrying an open question since §1. Here is the answer, and it takes three commands rather than one, which is the entire reason it was worth waiting for.

### Where nodes come from

First, two sentences you have never been given, because they are the node-side instance of a pattern §8 is going to lean on.

There are two main ways to have Nodes added to the API server: the kubelet on a node self-registers to the control plane, which is the default, or you (or another human user) manually add a Node object [source: k8s-docs-nodes-2026-08-23]. After you create a Node object, the control plane checks whether it is valid — whether a kubelet has registered with the API server matching the `metadata.name` field of the Node — and if the node is healthy, meaning the necessary services are running, then it is eligible to run a Pod [source: k8s-docs-nodes-2026-08-23]. The name of a Node object must be a valid DNS subdomain name and must be unique [source: k8s-docs-nodes-2026-08-23].

Note what a kubelet does when it joins a cluster: it writes an object through the API server. It does not open a private channel. It does the same thing you do.

### The three commands

Marking a node as unschedulable with `kubectl cordon $NODENAME` prevents the scheduler from placing new Pods onto that Node, but does not affect existing Pods on the Node; this is useful as a preparatory step before a node reboot or other maintenance [source: k8s-docs-nodes-2026-08-23]. You can use `kubectl drain` to safely evict all of your Pods from a node before you perform maintenance on it, such as a kernel upgrade or hardware maintenance [source: k8s-docs-safely-drain-node-2026-08-24]. `kubectl uncordon` restores scheduling [source: k8s-docs-nodes-2026-08-23] — and the drain documentation is explicit that this is a separate step you must take: you need to run `kubectl uncordon <node name>` afterwards to tell Kubernetes that it can resume scheduling new Pods onto the node [source: k8s-docs-safely-drain-node-2026-08-24].

Read the middle clause of that first sentence again. It is doing more work than its length suggests. `cordon` **deliberately leaves the running Pods alone.** That is not an oversight in the tool; it is the point of having a separate step. And it means the phrase "take a node out of service," which sounds like one action, is two.

> ★ **Fixed Point:** `cordon` stops arrivals and touches nothing already aboard. `drain` clears what is aboard. `uncordon` reopens. Three commands, three jobs — and **the maintenance sequence needs the first two.**

<!-- FIGURE: ch08-fig04-node-lifecycle-cordon-drain -->
![Four node panels in a row labelled schedulable, cordoned, drained and schedulable, connected by transitions labelled cordon, drain and uncordon; the same three Pods A, B and C appear unchanged in the first two panels and are gone from the third, while an arriving Pod is admitted in panels one and four and turned away in panel two](figures/ch08-fig04-node-lifecycle-cordon-drain.svg)

<!-- ASCII-FALLBACK
```
   SCHEDULABLE            CORDONED             DRAINED           SCHEDULABLE
  ┌────────────┐        ┌────────────┐      ┌────────────┐      ┌────────────┐
  │ [A][B][C]  │        │ [A][B][C]  │      │            │      │            │
  │            │──────► │            │─────►│  (empty)   │─────►│            │
  └────────────┘ cordon └────────────┘ drain└────────────┘uncord└────────────┘
        ▲                     ✗                                        ▲
     new Pod              new Pod                                   new Pod
     admitted            turned away                                admitted

        A, B and C are UNCHANGED between panel 1 and panel 2.
        They are still running. That is what cordon does and does not do.
```
-->

**Figure 8.4 —** What to notice is what does *not* change between the first two panels. The three Pods aboard the cordoned node are still running, still serving, still entirely unaffected. Only the arriving Pod's fate differs. The node does not empty until `drain`.

> ⚠ **Navigational Hazards:** **A cordoned node is not an empty node.** If you cordon a node and then reboot it for maintenance, every Pod still on that node goes down with the machine. This is the single most consequential confusion in this chapter, and unlike most exam traps it has a real operational cost attached. The instinct that "take out of service" means "empty" is a reasonable instinct. It is also wrong, and the fix is one more command.

> 🪢 **Mnemonic:** A cordon is a rope across a doorway. It stops people coming in. It does not remove the people already inside.

> 🔭 **Closer Look:** `drain` is not a special maintenance channel either. You can request eviction by calling the Eviction API directly, or programmatically using a client of the API server, like the `kubectl drain` command; this creates an `Eviction` object, which causes the API server to terminate the Pod [source: k8s-docs-api-eviction-2026-08-24]. Using the API to create an Eviction object for a Pod is like performing a policy-controlled `DELETE` operation on the Pod [source: k8s-docs-api-eviction-2026-08-24]. So `drain` is a client that writes objects through the one door — which is §8's whole claim, arriving early.

**One exception, and Chapter 7 §4 already joined these two for you.** Pods that are part of a DaemonSet tolerate being run on an unschedulable Node [source: k8s-docs-nodes-2026-08-23], because the DaemonSet controller automatically adds a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect to DaemonSet Pods [source: k8s-docs-daemonset-2026-08-24]. Chapter 6 taught DaemonSet as one-Pod-per-eligible-node; Chapter 7 taught the built-in condition tolerations and joined them *[cross-bearing: see Ch 7 §4 — the DaemonSet controller's automatic tolerations]* *[cross-bearing: see Ch 6 §7 — DaemonSet and node-local facilities]*. Here is what that join buys you during maintenance.

### Node conditions

A Node's status contains, among other fields: Addresses; Conditions; Capacity and Allocatable; and Info such as kernel version, Kubernetes version, container runtime details and the operating system [source: k8s-docs-node-status-2026-08-24]. `kubectl describe node <name>` shows them [source: k8s-docs-nodes-2026-08-23].

The `conditions` field describes the status of all `Running` nodes [source: k8s-docs-node-status-2026-08-24]:

| Condition | True when |
|---|---|
| `Ready` | The node is healthy and ready to accept Pods. **False** if the node is not healthy and is not accepting Pods. **Unknown** if the node controller has not heard from the node in the last `node-monitor-grace-period` (default is 50 seconds) |
| `DiskPressure` | Pressure exists on the disk size — that is, if the disk capacity is low |
| `MemoryPressure` | Pressure exists on the node memory — that is, if the node memory is low |
| `PIDPressure` | Pressure exists on the processes — that is, if there are too many processes on the node |
| `NetworkUnavailable` | The network for the node is not correctly configured |

*(All five conditions, the three `Ready` values, and the grace-period default: [source: k8s-docs-node-status-2026-08-24].)*

Four of those are two-valued. `Ready` is three-valued, and the third value is the interesting one.

`Unknown` is not a fourth failure mode. It is the control plane declining to guess. `False` means the node reported itself unhealthy: the node is *talking to you* and telling you something is wrong. `Unknown` means nobody has heard from it, which could equally be a dead machine or a network partition between the machine and the control plane. Those two situations call for different interventions, which is why the distinction is preserved rather than collapsed. If you answered Soundings question 6 with "it should conclude that it cannot tell," you reasoned your way to the shape of this answer without the vocabulary.

Treat the 50-second default as an illustration of the parameter rather than as the examinable fact. The parameter name is the durable thing; the number is configuration, and a cluster you meet may have been given a different one.

> 🪝 **Snag:** Print details of a cordoned node with a command-line tool and the Condition list includes `SchedulingDisabled`. **`SchedulingDisabled` is not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec** [source: k8s-docs-node-status-2026-08-24]. The thing `kubectl` shows you is not always a thing the API has — and the field that actually changed is one you write, not one the system reports. Hold that; §8 needs it.

### Heartbeats, and a control loop you already know

For nodes there are two forms of heartbeat: updates to the `.status` of a Node, and Lease objects within the `kube-node-lease` namespace, with each Node having an associated Lease object [source: k8s-docs-nodes-2026-08-23].

Chapter 4 pointed at exactly those Leases and said they were how the control plane detects node failure [source: k8s-docs-namespaces-2026-08-23] *[cross-bearing: see Ch 4 §3 — the four initial namespaces]*. That IOU is now settled: two heartbeat forms, one of them an object in a namespace you have already listed.

The node controller is a Kubernetes control plane component that manages several aspects of nodes: assigning a CIDR block to the node when it is registered; keeping its internal list of nodes up to date with the cloud provider's list of available machines; and monitoring the nodes' health — updating the `Ready` condition to `Unknown` when a node becomes unreachable, and triggering API-initiated eviction of all the Pods from the node if it stays unreachable [source: k8s-docs-nodes-2026-08-23].

Read that third job as a shape rather than as a list. It observes (heartbeats), it compares against what it expects, and it acts (condition update, then eviction). **The node controller is a control loop.** You met the pattern in Chapter 3 and you have met it in every chapter since *[cross-bearing: see Ch 3 §6 — the control loop]*. Noticing that costs one sentence and buys §8 half its argument.

### Capacity and Allocatable

Chapter 7 §2 told you that what makes Capacity and Allocatable differ, and how that is configured, is this chapter's material *[cross-bearing: see Ch 7 §2 — Capacity, Allocatable, and what the scheduler counts]*. Here is that promise, paid.

The fields in the capacity block indicate the total amount of resources that a Node has; the allocatable block indicates the amount of resources on a Node that is available to be consumed by normal Pods [source: k8s-docs-node-status-2026-08-24]. 'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods [source: k8s-docs-node-allocatable-2026-08-24]. The scheduler treats 'Allocatable' as the available capacity for Pods, and does not over-subscribe it [source: k8s-docs-node-allocatable-2026-08-24].

Why are they two different numbers? Because Kubernetes nodes can be scheduled to `Capacity`, and Pods can consume all the available capacity on a node by default — which is an issue, because nodes typically run quite a few system daemons that power the OS and Kubernetes itself [source: k8s-docs-reserve-compute-resources-2026-08-24]. Two reservations account for those daemons: `kubeReserved` captures resource reservation for Kubernetes system daemons like the kubelet and the container runtime, and `systemReserved` captures reservation for OS system daemons such as `sshd` and `udev` [source: k8s-docs-reserve-compute-resources-2026-08-24].

The configuration detail — how much is reserved, and the flags that set it — is above the associate tier and this book does not cover it. What the exam wants from you is the distinction: **Capacity is the machine's total; Allocatable is what the scheduler does arithmetic against.**

<!-- AUTHOR-REVIEW: deliberately no arithmetic. Both the node-allocatable and reserve-compute-resources snapshots state explicitly that the Capacity → reservations → Allocatable relationship is published only as an image (node-capacity.svg) with no text equivalent, so no equation is extractable. Do not add one in a later pass, even in words. -->

---

## ⚪ §5 — Who Owns the Control Plane

Everything so far in this chapter has been something you *do*. This section is about something you *own*, and the two are not the same question.

It is also, deliberately, the easiest reading in Part II. You have just come through the chapter's densest run and you have another one waiting in §6. Take this one slowly and without effort.

### The planning questions

Before choosing how to build a cluster, the documentation asks you to consider [source: k8s-docs-cluster-administration-2026-08-23]:

- Do you want to try out Kubernetes on your computer, or do you want to build a high-availability, multi-node cluster?
- Will you be using a hosted Kubernetes cluster, or hosting your own?
- Will your cluster be on-premises, or in the cloud?
- Will you be running Kubernetes on bare-metal hardware, or on virtual machines?
- Do you want to run a cluster, or do you expect to do active development of Kubernetes project code?

Five questions, and the honest observation is that in most working lives the answers arrive already decided: by budget, by a compliance requirement, by what the platform team standardized on two years ago. Knowing the axes still buys you something, because it tells you what was traded away.

### The tools, split by what they are for

**For learning.** If you are learning Kubernetes, use tools supported by the Kubernetes community or in the ecosystem to set up a cluster on a local machine: **minikube**, which runs a single- or multi-node local Kubernetes cluster, and **kind** — Kubernetes IN Docker — which runs local clusters using Docker containers as nodes [source: k8s-docs-setup-tooling-2026-08-23].

**For production.** When evaluating a solution for a production environment, consider which aspects of operating a cluster you want to manage yourself and which you prefer to hand off to a provider [source: k8s-docs-setup-tooling-2026-08-23]. The options are managed and turnkey certified Kubernetes services from cloud providers, and self-managed clusters bootstrapped with **kubeadm**, the officially supported tool for creating clusters, used to install the control plane and join nodes [source: k8s-docs-setup-tooling-2026-08-23]. Other ecosystem tools include **k3s**, a lightweight distribution [source: k8s-docs-setup-tooling-2026-08-23].

> ⚓ **Worth Securing:** kind and minikube are not two names for the same thing. kind runs its nodes as Docker containers, which makes clusters fast to create and destroy and makes it the usual choice inside CI pipelines. minikube runs a local cluster with a broader set of conveniences around it, which makes it the usual choice when a human is sitting in front of it. Choosing between them is really a question of whether a person or a pipeline is the user.

### One requirement none of these removes

Whichever route you take, a container runtime — containerd or CRI-O — must be installed on every node, and `kubectl` is the command-line tool for managing any cluster [source: k8s-docs-setup-tooling-2026-08-23].

That first clause is worth six chapters of your attention for one moment. Chapter 2 taught you the boundary between Kubernetes and the thing that actually starts containers, and taught it as an interface question *[cross-bearing: see Ch 2 §4 — the CRI, and what Kubernetes does not do itself]*. This is the first time in this book that boundary has had an operational consequence. `kubeadm` will build you a control plane and join your nodes to it, and a container runtime must be on those nodes regardless, because a container runtime is on the other side of a line the project deliberately drew.

And the second clause is quietly the reason this book works. However the cluster was built — laptop, rack, or a provider's console — the tool is the same one, and the grammar is the one from §1.

### What ownership actually means

Also collect one small debt here: scheduler profile configuration lives in the control plane's own component configuration, which is a thing you can reach only if you own the control plane *[cross-bearing: see Ch 7 §6 — scheduling profiles]*.

That is the general shape of the answer to Soundings question 8. Whoever operates the control plane holds the upgrade calendar and holds the etcd backup. If that is a provider, those are theirs. If it is you, they are yours.

Which is precisely why the next two sections exist. **§6 is which versions are allowed to disagree. §7 is what you cannot get back.** Those are the two duties that move.

<!-- AUTHOR-REVIEW: the managed/self-hosted duty split is deliberately narrow here and stays narrow. `k8s-docs-setup-tooling-2026-08-23` licenses only the EXISTENCE of a split ("consider which aspects of operating a Kubernetes cluster you want to manage yourself and which you prefer to hand off to a provider"); it does not enumerate sides, and kubernetes.io does not document commercial providers' responsibility models, so no fetch from that doc tree closes it. Recorded as research gap G-8G. Two duties are defensible on the architecture alone and are the only two asserted anywhere in this chapter: upgrade timing (§6) and etcd backup (§7). Do NOT restore a five-item duty list in Soundings A8, §5, or Practice Q13 without a vendor-neutral shared-responsibility source. -->

> **Logbook Entry:** The managed-versus-self-hosted decision is usually argued as a cost question, and cost is rarely what decides it in practice.
>
> A control plane is not expensive. Three modest machines will run one. What is expensive is the *calendar* attached to it: three minor releases a year, each with its own upgrade window, its own compatibility matrix, its own regression to discover in staging on a Thursday. Plus certificate expiries. Plus etcd backups you have to prove you can actually restore from, which is a different exercise from taking them. Plus the person who has to be reachable while all of that happens.
>
> Crews that self-host successfully are almost always crews that budgeted for that calendar deliberately, as a named piece of somebody's job. Crews that regret it are usually crews that priced the machines and not the Thursdays. Neither choice is the right one in general; plenty of organizations have excellent reasons to own the whole thing, and regulatory ones are only the most obvious. But the question worth asking out loud before you decide is not *can we run this*, it is *whose watch does this stand on*.

---

## ☆ Taking Your Bearings #2 — The Machine, the Skew, and What You Cannot Improvise

Seven questions on §4 through §7. Two of them reach back into earlier chapters.

**1.** 🔵 **[retrieval: ch7]** You cordon a node. Chapter 7 taught you a built-in taint whose effect matches what cordoning does: name that taint and its effect, then say what happens to the Pods already running on the node.

**2.** 🔵 A node stops responding. Its `Ready` condition changes. To what value — and what does that mean that `False` would not? Name the other four conditions a Node's status carries.

**3.** 🔵 **[retrieval: ch2]** You bootstrap a cluster with kubeadm. Before any node can run a Pod, one piece of software must be installed that kubeadm does not provide. Name it, name the two implementations the documentation names, and say which interface Kubernetes uses to talk to it.

**4.** 🟡 State the one rule that generates three of the five rows of the version-skew table. Then name the two rows it does not generate, and say why each is different.

**5.** 🔵 How many minor releases does the project maintain release branches for? Roughly how long is patch support for 1.19 and newer? Roughly how many minor releases ship per year? Say why those three numbers agree.

**6.** 🟡 You lose every control-plane node. Workers are untouched and applications are still serving traffic. What have you actually lost — and what single artifact gets it back?

**7.** 🔵 An etcd snapshot is sitting, unencrypted, on one of your control-plane nodes. Give two separate reasons this is wrong.

<details>
<summary>Answers + explanations</summary>

**1.** The taint is **`node.kubernetes.io/unschedulable`**, effect **`NoSchedule`**: no new Pods land without a matching toleration, and Pods already running are **not evicted** [source: k8s-docs-taints-tolerations-2026-08-23]. `cordon` itself only marks the node Unschedulable in its spec [source: k8s-docs-node-status-2026-08-24]; the relationship between that field and the built-in taint is left exactly where the documentation leaves it.

*Common wrong turn:* answering "evicted" — that's `NoExecute`'s behavior, not `NoSchedule`'s.

**2.** **`Unknown`** — the node controller hasn't heard from the node within the `node-monitor-grace-period`. `False` would mean the node reported itself unhealthy; `Unknown` means the control plane has no information at all, consistent with either a dead machine or a network partition.

The other four: **`DiskPressure`**, **`MemoryPressure`**, **`PIDPressure`**, **`NetworkUnavailable`** — three pressure conditions plus one about configuration.

*Common wrong turns:* `False` (intuitive, and wrong), `NotReady` (a display convenience, not an API value), and `SchedulingDisabled` (a kubectl display string, not a Condition).

**3.** A **container runtime** — **containerd** or **CRI-O** — reached through the **CRI**, the Container Runtime Interface. Chapter 2 drew this as an architectural boundary; here it turns operational: the officially supported bootstrapper builds you a control plane, but the runtime still has to be installed separately, because it lives on the other side of that interface.

**4.** The rule: **nothing may be newer than the API server.** It generates the kubelet row, the kube-proxy row, and the controller-manager/scheduler/cloud-controller-manager row.

The two exceptions, for two different reasons:

- **`kubectl`** — a user tool outside the cluster, not part of its internal consistency, so its window is symmetric: one release either direction, newer included.
- **The HA kube-apiserver row** — not a bound relative to "the" API server at all, but a mutual bound *between* API servers: newest and oldest instances must sit within one minor version of each other.

*Common wrong turn:* naming `kubectl` and stopping. The HA row is the one most readers miss, because it doesn't look like an exception until you notice it has no fixed point to measure from.

**5.** **Three** branches. **About a year** of patch support for 1.19 and newer. **About three** releases a year, roughly every fifteen weeks. They agree because three releases a year across three maintained branches is about twelve months of coverage — the branch count *is* the support window, expressed in releases rather than months.

*Common wrong turn:* "the last two releases" — it's three. You'll meet this cadence again in Chapter 17's release-governance material *[cross-bearing: see Ch 17 §8 — SIG Release and the release cycle]*; it's forgettable material, and that pass is its second look.

**6.** You've lost **the cluster's entire record of intent** — every object — since all Kubernetes objects live in etcd. Not the running workloads: kubelets keep running what they were last told, so traffic keeps flowing. What's gone is every declaration of what *should* be running, so nothing can be reconciled, changed, scheduled, healed, or scaled. The artifact that brings it back: **an etcd snapshot**.

The scenario is built so you notice that "running workloads" and "cluster state" are different things — most people's first answer to "we lost the control plane" is "the applications are down," and for a while, they are not.

**7.** **First:** it isn't stored outside the nodes it protects against losing — a snapshot living only on the machines it insures against doesn't survive the event it exists for. **Second:** access to etcd is root-equivalent for the cluster, and the snapshot holds all of it — every Secret, every config. Unencrypted, it's a complete compromise in one readable file.

Two reasons, two failure modes: one about availability, one about confidentiality.

</details>

**How'd you do?**

**7/7:** You own the node lifecycle and the two duties that cannot be improvised. Take the recommended break; §8 is short, and then Part II is done.
**5–6:** Good. If a skew-table or cordon item was among the misses, spend ten minutes with Figure 8.5 — it holds the exceptions better than the table does.
**0–4:** Re-read §4 and §6 before continuing. Don't memorize the skew table's five rows — derive them: one rule, three rows, two exceptions for two different reasons.

**Checkpoint: you've now mastered**
✓ How Node objects come into existence, and that a kubelet joins by writing one
✓ `cordon` / `drain` / `uncordon`, and which two the maintenance sequence needs
✓ The five node conditions, and why `Ready` has three values
✓ Two heartbeat forms, and the control loop watching them
✓ Capacity, Allocatable, and the two reservations that separate them
✓ The rule that generates the skew table, and the two rows that sit outside it
✓ Three branches, one year, three releases a year — and why those agree
✓ What losing every control-plane node does and does not cost you
✓ Why an etcd snapshot is both your recovery and your largest single risk
☐ Why none of this was new (next, and it is the point of the chapter)

---

One flag: the brief said the two checkpoints hold 20 questions total — they actually hold 10 (5 each). I merged from the real 10, dropping 3 (the cordon/drain challenge-scenario duplicate, the upgrade-ownership item, and the applied skew-table item whose ground the kept conceptual version already covers), landing on 7. Word count came to 1091, comfortably inside the 1350 budget.

## ⚪ §8 — Rules, or Consequences

You were asked to keep score. Here is the claim.

**You did not learn a single new mechanism in this chapter.**

Every administrative act in it is a write through the one door you met in Chapter 3, reconciled by a controller you had already been introduced to. Take them in order.

**§1.** `kubectl` is a client of the API server. Not a management console, not a privileged back channel: a command-line client that assembles an HTTP request and sends it to the same endpoint your Pods use. Chapter 3's single door, addressed from a terminal.

**§2.** The three gates are not a subsystem bolted onto the side. They are what the single door *does* before it writes anything down — and the documentation says so in one sentence: once a request passes all admission controllers, it is validated and then written to the object store [source: k8s-docs-controlling-access-2026-08-24]. Chapter 3 told you every request terminates at the API server; §2 is the "and then what" of that sentence. Even the audit log is kept inside the same component [source: k8s-docs-audit-2026-08-24].

**§3.** A ResourceQuota is an object. You `apply` it exactly as you apply a Deployment. It takes effect because an admission controller reads it when other requests arrive [source: k8s-docs-admission-controllers-2026-08-24], which means a quota is a **declaration that changes what other declarations are permitted to say.** Nothing about it is a special-case enforcement engine.

**§4, and this is the one that should land.** `kubectl cordon` has no private channel to the node. It does not connect to the machine. It writes a field on a Node object through the API server — cordoned nodes are marked Unschedulable in their spec [source: k8s-docs-node-status-2026-08-24] — and `spec` is the half of an object that *you* declare, as against `status`, which the system reports back. Chapter 4 taught you that distinction *[cross-bearing: see Ch 4 §2 — spec and status]*, and here it does real work: cordoning is an act of *declaring intent about a machine*, which is why it lives in `spec` and why `SchedulingDisabled`, the thing your terminal prints, is not a Condition in the API at all.

The scheduler then does what the scheduler always does: it checks taints, not node conditions, when it makes scheduling decisions [source: k8s-docs-taints-tolerations-depth-2026-08-24], and Chapter 7 already showed you a built-in `node.kubernetes.io/unschedulable` taint with a `NoSchedule` effect sitting in that table [source: k8s-docs-daemonset-2026-08-24]. Nothing here is a new mechanism. It is the object model and the scheduler you already have, with an operator's hand on the spec field.

**§4 again.** The node controller observes heartbeats, compares them against what it expects, and acts: updating a condition, then evicting. It is a control loop — the same loop, at the same altitude as Chapter 6's — and you could have predicted its structure without being told.

**§6.** The skew rules are the compatibility contract of that same one door. Read the table again with that in mind and three of the five rows are answering one question: *which clients will this door accept?*

**§7.** etcd is what is behind the door, and the reason only the API server should reach it is the same reason there is only one door in the first place.

> ☀️ **Zenith:** One door, and behind it controllers you have already met. Everything in this chapter is a write to the first, reconciled by the second.

<!-- FIGURE: ch08-zenith-consequences-not-rules -->
![Four administrative actions on the left — kubectl cordon, applying a quota, applying a deployment, and kubelet self-registration — all converge on a single central box labelled the API server, one door; four arrows leave it to the scheduler from chapter seven, the node controller from chapters four and eight, the workload controllers from chapter six, and the control loop from chapter three, with a single arrow running down from the box to etcd](figures/ch08-zenith-consequences-not-rules.svg)

<!-- ASCII-FALLBACK
```
  administrative acts                                 controllers you
  (§1, §3, §4)                    ┌───────────┐       already met
                                  │           │
  kubectl cordon ────────────►    │    the    │ ──►  scheduler            (Ch 7)
  kubectl apply -f quota.yaml ►   │    API    │ ──►  node controller    (Ch 4/8)
  kubectl apply -f deploy.yaml►   │  server   │ ──►  workload contrls    (Ch 6)
  kubelet self-registration ─►    │           │ ──►  the control loop     (Ch 3)
                                  │ ONE DOOR  │
                                  └─────┬─────┘
                                        │
                                        ▼
                                      etcd
```
-->

**Figure 8.6 —** What to notice is the chapter number beside each controller. This is Chapter 3's architecture diagram, unchanged, except that you have now put your own hands on the left-hand side of it, and every mechanism on the right-hand side is one you were taught somewhere in Part II. What to notice second is that no arrow on the left reaches a controller directly. There are no side channels.

### Rules, or consequences

Chapter 7 closed by saying this chapter is where the rules turn into consequences. That is the sentence to land on.

A list of administrative rules is among the least memorable material any study guide can put in front of you, and this chapter contained a great many of them. A set of consequences of a single architecture is a different thing entirely. If you can hold **one door, and controllers behind it**, you can regenerate most of this chapter without ever having memorized it, and you can go further than that. When you meet a Kubernetes administrative feature this book does not cover, the two questions that will get you most of the way are already in your hands.

> ⚓ **Worth Securing:** Faced with an unfamiliar Kubernetes administrative feature, ask two questions in this order: **what object does it write**, and **what controller is watching that object?** Those two questions answer most of them, and where they do not, they at least tell you what kind of thing you are looking at.

### Where the claim overreaches

One honest correction, because the claim as stated is slightly too neat and you would notice.

§5 and §6 are not consequences of the architecture. Which bootstrap tool is officially supported, how many release branches the project maintains, and how far a kubelet may lag: these are facts about a *project*, made by people in meetings, and no amount of understanding the single-door model will let you derive them. They have to be learned. That is exactly why §6 flagged them as memorization and gave you a derivation for three of the five rows anyway. The parts that can be reasoned about should be reasoned about, and the residue should be admitted as residue.

Chapter 4 §6 established this book's habit of narrowing a claim until it is true rather than leaving it broad and impressive *[cross-bearing: see Ch 4 §6 — the habit of narrowing a claim until it is true]*. So: **every administrative *act* in this chapter is a write through one door, reconciled by a controller you already know. The project's *policies* are not, and those are the parts you memorize.** That version survives contact with the exam.

---

## Exam Alert! 🚨

**High-priority topics**, in descending order of confidence:

1. **The three gates, in order** — authentication, then authorization, then admission control.
2. **Only admission can change the request.** The other two accept or refuse.
3. **kubelet may be up to three minor versions older than kube-apiserver, and must never be newer.**
4. **`kubectl` is the only component permitted to be newer** — within one minor version, in either direction.
5. **Three supported minor releases**, approximately one year of patch support (1.19+), approximately three minor releases per year.
6. **`cordon` stops arrivals; `drain` evicts.** A cordoned node is not an empty node.
7. **`Ready` is three-valued.** `Unknown` means the control plane has not heard from the node, which is not the same claim as `False`.
8. **ResourceQuota is namespace-aggregate; LimitRange is per-object** — and a quota'd namespace forces every new Pod to declare requests or limits.
9. **Upgrade the API server first**, because nothing may be newer than it.
10. **`kubectl [command] [TYPE] [NAME] [flags]`** — types case-insensitive and abbreviable, names case-sensitive.
11. **All objects live in etcd, and access to etcd is equivalent to root permission in the cluster.**

**Common traps.** Each of these catches real candidates. None of them is dressed up with an invented statistic, because nobody publishes one.

| Trap | The correct understanding |
|---|---|
| "kubelet must match the API server version" | It must not be *newer*. It may be up to three minors older. Matching is not required |
| Applying the kubelet skew rule to `kubectl` | Different rule, different number, different shape. kubelet: three, older only. `kubectl`: one, either direction |
| "Kubernetes supports the last two minor releases" | **Three** |
| "Everything lives in a namespace" | Nodes, PersistentVolumes and StorageClasses do not. This is why no quota can cap a team's Node consumption |
| "`cordon` takes the node out of service" | It stops new Pods. It does not move the ones already there. That is `drain` |
| "Authorization and admission are two words for the same check" | Authorization is any-module-approves and looks at identity, verb and object; admission is any-module-rejects and looks at the object's contents |
| "`Ready: False` is what an unreachable node reports" | An unreachable node shows `Unknown`. `False` is a node that reported *itself* unhealthy |
| "`SchedulingDisabled` is a node Condition" | It is a display string. Cordoned nodes are marked Unschedulable in their `spec` |
| "A ResourceQuota limits how big any one Pod can be" | That is LimitRange. A quota is an aggregate ceiling on the namespace |
| "A Pod with no resource fields is always valid" | Not in a namespace with a cpu or memory quota. Declare requests or limits, or let a LimitRange declare them for you |
| "`kubectl` inside a Pod behaves as it does on your laptop" | It detects in-cluster conditions, authenticates as the ServiceAccount, and defaults to that ServiceAccount's namespace |
| "Resource names are case-insensitive, because resource types are" | Types are. Names are not |
| "An etcd snapshot on the control-plane node is a backup" | It is a copy that goes down with the thing it was protecting — and, unencrypted, a root-equivalent credential |

---

## Practice Questions

Eighteen questions. Several require two sections at once; that is deliberate, because the exam does not organize itself by chapter section either. Answers and full explanations follow the set.

**1.** Which statement about `kubectl` command syntax is correct?

A) Both resource types and resource names are case-insensitive
B) Resource types are case-insensitive and may be given in singular, plural or abbreviated form; resource names are case-sensitive
C) Resource names are case-insensitive; resource types must be given in the plural
D) Both resource types and resource names are case-sensitive

**2.** In what order does a request pass the API server's access-control gates, and which of them can result in the request being modified rather than accepted or rejected?

A) Authorization → authentication → admission; only admission can modify
B) Authentication → authorization → admission; only authorization can modify
C) Authentication → authorization → admission; only admission can modify
D) Authentication → authorization → admission; any of the three can modify

**3.** A request to create a Deployment is refused. Investigation confirms that the client's identity was valid and that the identity was permitted to create Deployments in that namespace. Which gate refused it?

A) Authentication — the credential must have expired mid-request
B) Authorization — permission to create a Deployment does not imply permission to create this one
C) Admission control — the request's contents were evaluated and found unacceptable
D) None; a request that passes authentication and authorization is always persisted

**4.** A developer submits a Pod whose resource requests would push their namespace past its ResourceQuota. The Pod is rejected. Which gate rejected it, and would the outcome be different if a cluster administrator had submitted the identical manifest to the same namespace?

A) Authorization; yes — an administrator has broader permissions, so the quota would not apply
B) Admission control; no — the quota constrains the namespace, not the submitter
C) Admission control; yes — the quota applies to the namespace's owner, and an administrator's requests are attributed to the cluster rather than the namespace
D) Admission control; yes — quota enforcement is skipped for cluster-admin identities

**5.** Which pairing correctly describes ResourceQuota and LimitRange?

A) ResourceQuota bounds an individual Pod's resources; LimitRange caps a namespace's total
B) Both cap a namespace's aggregate consumption; LimitRange additionally supplies defaults
C) ResourceQuota caps a namespace's aggregate consumption; LimitRange constrains individual objects and supplies defaults
D) ResourceQuota applies to cluster-scoped objects; LimitRange applies to namespaced objects

**6. [retrieval: ch4]** A platform team wants to cap the number of Nodes that a particular application team may consume. Why can they not do this with a ResourceQuota?

A) ResourceQuota cannot count objects, only compute resources
B) Nodes are not namespaced objects, and a ResourceQuota constrains a namespace
C) ResourceQuota is evaluated at the authorization gate, which has no visibility into Nodes
D) They can; a ResourceQuota in the `kube-system` namespace applies cluster-wide

**7. [retrieval: ch5]** A namespace has a LimitRange that supplies a default CPU request. A developer submits a Pod manifest that declares no resource fields at all. The Pod is accepted, with the default filled in. What has changed about where this Pod can be placed, compared with the manifest as written?

A) Nothing — defaults are recorded for reporting but are not used in placement decisions
B) It can now be placed on fewer nodes, because it now books capacity against Allocatable that it did not book before
C) It can now be placed on more nodes, because a declared request lets the scheduler relax its filtering
D) Nothing — placement is decided from limits, not requests

**8.** You are told: "take node worker-3 out of service and clear it before the maintenance window." Using only the four-slot grammar, which commands accomplish this, and in what order?

A) `kubectl drain worker-3`, then `kubectl cordon worker-3`
B) `kubectl cordon worker-3`, then `kubectl drain worker-3`
C) `kubectl cordon worker-3` alone — draining is implied
D) `kubectl uncordon worker-3`, then `kubectl drain worker-3`

**9.** A node stops responding to the control plane. What value does its `Ready` condition take, and what does that value assert?

A) `False` — the node has reported that it is unhealthy and not accepting Pods
B) `NotReady` — a distinct value used only for unreachable nodes
C) `Unknown` — the node controller has not heard from the node within the grace period
D) `SchedulingDisabled` — the node controller has marked it ineligible for new Pods

**10. [retrieval: ch4]** When you run `kubectl cordon node-7`, which part of the Node object is written, and how can you tell?

A) `status` — cordoning reports an observed condition of the machine
B) `spec` — it is a statement of desired state, and `status` is written by the system rather than by you
C) `metadata` — cordoning applies a label to the Node object
D) Neither; `cordon` bypasses the object model and signals the kubelet directly

**11. [retrieval: ch3]** The node controller notices that a node has stopped reporting, updates a condition, and eventually evicts that node's Pods. Name the pattern, and name two earlier components in this book that work the same way.

A) A webhook; the Pod Security Admission controller and the NodeRestriction plugin
B) A control loop; the Deployment controller and the scheduler's watch on unscheduled Pods
C) A daemon; the kubelet and kube-proxy
D) A reconciliation batch job; the DaemonSet controller and etcd's compaction

**12.** Which statement about cluster bootstrap tooling is correct?

A) kubeadm is intended for local learning environments; kind is the officially supported production bootstrapper
B) kubeadm is the officially supported tool for creating clusters, installing the control plane and joining nodes; kind and minikube are for local learning environments
C) k3s is the officially supported tool for creating clusters; kubeadm is a lightweight distribution
D) kubeadm is the officially supported tool for creating clusters; it installs a container runtime on each node as part of joining them

**13.** Which pairing correctly separates a duty that sits with whoever operates the control plane from one that does not?

A) Taking etcd backups does not sit with the control-plane operator; installing a container runtime on each node does
B) Choosing which container images an application runs sits with the control-plane operator; taking etcd backups does not
C) Taking etcd backups sits with the control-plane operator; choosing which container images an application runs does not
D) Installing a container runtime on each node sits with the control-plane operator; taking etcd backups does not

**14.** Your cluster's API servers are at 1.36. Which of the following combinations is **not** supported?

A) kubelet at 1.33
B) `kubectl` at 1.37
C) kube-scheduler at 1.35
D) kube-proxy at 1.37

**15.** Which component is permitted to run at a *newer* minor version than kube-apiserver, and within what window?

A) kubelet, up to three minor versions
B) kube-proxy, up to three minor versions
C) `kubectl`, within one minor version
D) None; no component may ever be newer than kube-apiserver

**16.** In what order must a cluster's components be upgraded, and why?

A) kubelet first, because the nodes must be ready before the control plane restarts
B) kube-apiserver first, because nothing may be newer than it
C) etcd first, because the API server depends on it for storage
D) All components simultaneously, because no version skew is permitted between them

**17. [retrieval: ch6]** You drain a node for maintenance. Every Pod is evicted except one, which is still running afterwards. Chapter 6 introduced the controller responsible. Name it, and say what its Pods carry that lets them stay.

A) A StatefulSet; its Pods hold a stable ordinal identity that the eviction path preserves
B) A Deployment with a node selector; a placement constraint makes its Pods ineligible for eviction
C) A DaemonSet; the controller automatically adds a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect to its Pods
D) A Job; Pods running to completion are exempt from eviction until they finish

**18.** An operations team stores its nightly etcd snapshots, unencrypted, on the primary control-plane node. Which statement best describes the problem?

A) There is no problem, provided the node's filesystem permissions are correct
B) The snapshots should be encrypted, but their location is fine because that is where etcd runs
C) The snapshots should be stored outside the control-plane nodes and kept encrypted — otherwise they will not survive the disaster they exist for, and access to etcd data is equivalent to root permission in the cluster
D) The snapshots should be taken with `etcdutl snapshot save`; `etcdctl` is the restore utility

---

### Answers and Explanations

**1. B.**
Resource types are case-insensitive and accept singular, plural or abbreviated forms; names are case-sensitive. **A is wrong** because it flattens the asymmetry in the permissive direction, the single most common form of this error, because the tool's tolerance about types encourages the assumption. **C is wrong** on both counts and additionally invents a plural requirement that does not exist. **D is wrong** in the strict direction: `kubectl get PODS web-01` works perfectly well.

**2. C.**
Authentication, then authorization, then admission; only admission can modify. **A is wrong** on order alone — it names the correct modifying gate, so a reader who knows only that admission mutates cannot eliminate it, which is the point of the option. **B is wrong** on the modifying gate: authorization's inputs are the username, the requested action and the object affected, not the object's contents, so it has nothing to modify with. **D** gets the order right and then gives all three gates a power only the third has, which is the error that collapses three distinct gates into one undifferentiated "security check."

**3. C.**
Both earlier gates already returned yes, so the refusal came from the one that examines contents — and admission is the only gate that can access the contents of the object being created or modified. **A is wrong**: an unauthenticated request fails at gate one with a 401, and the question states the identity was valid. **B is wrong** because it misdescribes authorization; authorization decides whether an identity may perform an action on a resource, and the question stipulates that it did. **D is wrong** and is the trap for readers still working from a two-gate model: passing authentication and authorization is necessary, not sufficient.

**4. B.**
Quota enforcement happens at the admission gate — ResourceQuota is an admission controller that observes the incoming request — and a quota constrains aggregate consumption *per namespace*, regardless of who submitted the request. **A is wrong** twice: wrong gate, and it imports a rule that does not exist, since quota is not an identity-scoped check. **C is wrong** on a subtler misreading: it applies §3's scope hinge backwards, treating a namespaced constraint as if the submitter's identity could relocate the request's scope. Nothing about quota is attributed to a submitter. **D** gets the gate right and then invents an administrator exemption; the appeal of this distractor is that it *feels* like how permissions usually work, which is exactly why it is worth defusing.

**5. C.**
Quota provides constraints that limit aggregate resource consumption per namespace; LimitRange constrains the resource allocations you can specify for each applicable object kind, and supplies defaults so Pods declare their requirements. **A is wrong** because it swaps them, which is the only real mistake available in this section. **B is wrong** because it gives both mechanisms namespace-aggregate scope, losing the scope distinction that is the actual content. **D is wrong**: both are namespaced objects, and the scope difference between them is *within* a namespace, not across the namespaced/cluster-scoped boundary.

**6. B. [retrieval: ch4]**
Nodes are cluster-scoped, and a ResourceQuota is a statement about a namespace. Chapter 4 established the boundary; §3 turned it into an operational consequence. **A is wrong** as a claim about quota's capabilities — a quota counts objects perfectly well, in the `count/<resource>` form — and, more importantly, misses the point: the obstacle is scope, not counting. **C is wrong** on the gate: quota is enforced at admission, and authorization has no view of object scope in any case. **D is wrong**: `kube-system` is a namespace like any other, not a privileged scope from which cluster-wide policy can be issued.

**7. B. [retrieval: ch5]**
Chapter 5 established that when you specify the resource request for containers in a Pod, the kube-scheduler uses this information to decide which node to place the Pod on [source: k8s-docs-resource-management-2026-08-23], and §4 of this chapter established that the scheduler treats Allocatable as the available capacity for Pods and does not over-subscribe it. A Pod that previously declared nothing now books capacity, so nodes that would have accepted it may now fail to fit it. **A is wrong**: the defaulted value is a real field on a real object and is used exactly as if you had written it. **C inverts the effect**; declaring a request adds a constraint, it does not relax one. **D is wrong** on which of requests and limits the scheduler reads.

**8. B.**
`cordon` first to stop new arrivals, then `drain` to evict what is already there — `cordon` is documented as a preparatory step before a node reboot or other maintenance, which is precisely this sequence. Note the grammar: both take the node's name directly, without a preceding TYPE, because the verb already implies the resource type. **A reverses the documented order**, putting the preparatory step after the operation it prepares for. **C is the chapter's headline trap**: `cordon` does not empty anything, so rebooting after a bare cordon takes down every Pod still aboard — which is a real outage, not just a lost mark. **D begins by making the node schedulable again**, which is the opposite of the instruction; `uncordon` is the third command, run after maintenance.

**9. C.**
`Ready` becomes `Unknown` when the node controller has not heard from the node within the `node-monitor-grace-period`. **A is the intuitive wrong answer** and misstates the evidence: `False` means the node *told you* it is unhealthy, which requires the node to be talking. **B is wrong**: `NotReady` is a display convention in summary output, not one of the condition's three values. **D is wrong** on two counts — `SchedulingDisabled` is not a Condition in the Kubernetes API at all, and it describes a deliberately cordoned node rather than an unreachable one.

**10. B. [retrieval: ch4]**
Cordoned nodes are marked Unschedulable in their `spec`, which is exactly what Chapter 4's rule predicts: `spec` is what you declare, `status` is what the system reports back, and unschedulability is a decision you made about the machine rather than an observation of it. **A is wrong** for that reason. **C is wrong**: the mechanism is a spec field, not a label. **D is wrong** and is worth rejecting emphatically, because it is precisely the belief §8 exists to dismantle — and note that `SchedulingDisabled`, the string your terminal prints, is not in the API either, so even the output is not what it appears to be. There are no side channels.

**11. B. [retrieval: ch3]**
Observe, compare, act: it is a control loop, the same pattern as the ReplicaSet controller holding a replica count and the Job controller driving Pods to completion, both in Chapter 6. **A is wrong**: admission plugins act synchronously on inbound requests rather than reconciling observed state against declared state. **C is wrong**: the kubelet and kube-proxy are node agents, and "daemon" describes where they run rather than how they work. **D is wrong** on both the pattern and the examples; nothing here is batched, and etcd compaction is storage maintenance, not reconciliation.

**12. B.**
kubeadm is the officially supported tool for creating clusters, installing the control plane and joining nodes; kind and minikube are the documented local learning tools. **A swaps the two categories.** **C swaps kubeadm and k3s**: k3s is a lightweight distribution, not the official bootstrapper. **D** names the right bootstrapper and then attributes a duty to it that the CRI boundary explicitly excludes: a container runtime (containerd or CRI-O) must be installed on every node, and kubeadm does not supply it. That is the Chapter 2 interface boundary showing up as an operational requirement — the most attractive wrong answer here precisely because it *sounds* like something a complete bootstrapper would do.

**13. C.**
etcd backup sits with whoever operates the control plane; choosing container images is a workload-side decision made by whoever runs the workloads. **A inverts both halves** — it moves the backup off the control plane and puts node-level runtime installation on it. **B is wrong** on the first half: image selection is a Pod-spec author's decision, made by the users who create resources in a namespace, not by the control-plane operator. **D is the sharpest distractor**, because installing a runtime on each node *sounds* like platform work — but it is a node-provisioning duty, and it does not become the control-plane operator's just because both sound infrastructural. The half that gives it away is the second: etcd backup unambiguously belongs to whoever runs the control plane.

**14. D.**
kube-proxy must not be newer than kube-apiserver, so 1.37 against a 1.36 API server is unsupported. **A is supported**: kubelet may be up to three minor versions older. **B is supported**: `kubectl` is the one component permitted to be newer, within one minor. **C is supported**: the scheduler may be up to one minor older. Note that B and D differ only in which component is one version ahead, which is the whole of the distinction being tested.

**15. C.**
`kubectl`, within one minor version in either direction. This book's explanation for the exception — that `kubectl` is a user tool addressing the cluster from outside rather than a component inside it — is offered as reasoning rather than as documented rationale; the rule itself is what the policy states. **A is the chapter's most durable error**: the kubelet's three-minor window is generous, but it runs in one direction only. **B applies the same mistake to kube-proxy**, which is also older-only relative to the API server. **D states the general rule correctly and forgets that there is exactly one exception**, which is the answer of a candidate who learned the principle and not the table.

**16. B.**
kube-apiserver first, because nothing may be newer than it, and every other component's window is expressed relative to it. **A inverts the dependency**: a kubelet upgraded ahead of the API server would be newer than its server, which is the one thing the policy forbids outright. **C confuses a runtime dependency with an upgrade constraint** — the API server does store its data in etcd, but the skew policy governs Kubernetes components, and etcd's own upgrade is a separate procedure. **D is wrong** because skew is not merely permitted but *required* by the upgrade process: the one-minor allowance for the controller manager and scheduler exists specifically to allow live upgrades.

**17. C. [retrieval: ch6]**
A **DaemonSet**. Its Pods carry a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect, added automatically by the DaemonSet controller — the toleration half of this is Chapter 7 §4's *[cross-bearing: see Ch 7 §4 — the DaemonSet controller's automatic tolerations]* — which is why Kubernetes can run DaemonSet Pods on nodes marked unschedulable. **A confuses identity with immunity**: a StatefulSet's ordinal identity governs naming and ordering, not eviction. **B is the most plausible wrong answer** — it is true that placement constraints affect where a Pod *goes*, and false that they affect whether it can be *evicted*; those are different mechanisms, and Chapter 7's affinity material does nothing here. **D is wrong**: a Job's Pods are evicted like any others, and the Job controller's response is to create replacements elsewhere.

**18. C.**
Two independent failures. A backup stored only on the machines it insures against losing does not survive the event; and access to etcd data is equivalent to root permission in the cluster, so an unencrypted snapshot is a complete compromise in one readable file. **A is wrong** because filesystem permissions do not address either failure; they do not make the file survive the node's loss, and they are a thin defense for something this valuable. **B accepts the location** on a reasoning error: etcd running there is the reason the snapshot must *not* live there. **D inverts the two utilities**: `etcdctl snapshot save` takes the backup and `etcdutl snapshot restore` restores it, and the two names differ by two letters, which is exactly why the confusion is worth having a distractor for.

---

## Chapter Summary

| Concept | Remember this |
|---|---|
| `kubectl` grammar | `kubectl [command] [TYPE] [NAME] [flags]`. Types case-insensitive and abbreviable; **names case-sensitive** |
| kubeconfig | `$HOME/.kube/config` by default; `KUBECONFIG` or `--kubeconfig` override it, and the flag wins |
| `kubectl` in a Pod | Detects the two env vars plus the ServiceAccount token file; authenticates as the ServiceAccount; defaults to that ServiceAccount's namespace |
| The three gates | **Authentication → authorization → admission.** Who, may, and how |
| Admission's distinction | The only gate that can change the request instead of refusing it — and the only one where *any* module's rejection is final |
| Reads | Do not pass admission at all |
| Auditing | A chronological record of the sequence of actions in a cluster, kept inside the kube-apiserver |
| ResourceQuota | A ceiling on **aggregate consumption per namespace**; violation is `403` |
| The quota consequence | In a namespace with a cpu or memory quota, **every new Pod must declare requests or limits** |
| LimitRange | Constrains **each applicable object kind**, enforces min/max and ratio, and injects defaults at admission — never on running Pods |
| The scope hinge | You can quota a team. You cannot quota a machine — Nodes are not namespaced |
| Node registration | kubelet self-registration is the default; a human may also create the Node object |
| `cordon` | Stops new Pods. **Leaves running Pods entirely alone.** Writes `.spec.unschedulable` |
| `drain` | Evicts the Pods `cordon` left running, via the Eviction API |
| `uncordon` | Restores scheduling — a separate step you must run yourself |
| DaemonSet exception | DaemonSet Pods carry an automatic `unschedulable` toleration, so they tolerate a cordoned node |
| Node conditions | `Ready`, `DiskPressure`, `MemoryPressure`, `PIDPressure`, `NetworkUnavailable` |
| `Ready: Unknown` | The control plane has not heard from the node. Not "the node is broken" — "we cannot tell" |
| `SchedulingDisabled` | A display string, not a Condition in the API |
| Heartbeats | Two forms: `.status` updates, and Lease objects in `kube-node-lease` |
| node controller | Assigns a CIDR at registration, syncs with the cloud provider's machine list, monitors health. **A control loop** |
| Capacity vs Allocatable | Capacity is the machine's total; Allocatable is what is available for Pods, after `kubeReserved` and `systemReserved` account for the daemons. The scheduler does arithmetic against Allocatable |
| Bootstrap tooling | kubeadm officially supported for creating clusters; minikube and kind for learning; k3s lightweight |
| Everywhere | A container runtime — containerd or CRI-O — must be on every node |
| The generating rule | **Nothing may be newer than the API server** — three of the five rows |
| kubelet skew | Never newer; up to **three** minors older |
| `kubectl` skew | **One** minor, **either direction** — the sole component-level exception |
| HA API servers | Newest and oldest within one minor **of each other** — a mutual bound, not a bound relative to one |
| Supported releases | **Three** branches, ~1 year of patch support (1.19+), **~3** minor releases per year |
| Upgrade order | API server first, because nothing may be newer than it |
| etcd | Holds all Kubernetes objects. **Access to it is equivalent to root in the cluster** |
| Backup | `etcdctl snapshot save` or a volume snapshot. Keep it encrypted; store it outside the control-plane nodes |
| Restore | `etcdutl snapshot restore`, operating on the data files; control-plane components restart against the restored directory |
| The chapter's claim | One door, and controllers behind it. Every administrative *act* here is a write through the first, reconciled by the second — though the project's *policies* still have to be learned |

---

## 🏆 Safe Harbor

You started this chapter able to describe what should run and where. You end it able to take a machine out of service without dropping a request, stop a team consuming a cluster they share, say which of five components may lag the API server and by how much, and name the one file whose loss you cannot work around.

More usefully, you end it with a method. The two questions from §8 — *what object does it write, and what controller is watching* — will carry you through administrative features this book never mentions, which is a better return than any of the individual facts above.

Part II is complete. Ship, cargo, and company: the container, the cluster, the objects, the Pod, the controllers, the placement, and now the watch. That is the whole of what runs and how it is looked after.

---

## The Voyage Ahead

There is a question Part II has been carefully not asking.

You have spent seven chapters putting workloads onto machines and one chapter standing over the result, and in all of it, nothing has had to *reach* anything else. The Pods were placed. The nodes were managed. The quotas were enforced. Not once did a Pod on `worker-3` have to find a Pod on `worker-11`, or hold an address either of them could rely on, or survive that address changing when the Pod is rescheduled somewhere else forty seconds from now — which, given everything Chapter 6 taught you about controllers, it very well might be.

That last part is the difficulty, and it is worth feeling the shape of it before Chapter 9 answers it. Every Pod gets an address. Pods are also, as Chapter 6 established, disposable: a controller may replace one at any moment, and the replacement is a different Pod. So the cluster contains a large number of network endpoints, each perfectly valid, none of them stable, and applications that need to talk to each other anyway.

Part III is how that works: addresses, the abstraction that makes them survivable, how names resolve, and how anything outside the cluster gets in at all. You have just spent a chapter learning that everything administrative is a write through one door. Networking is where you find out what the cluster does with everything *behind* that door, and it is, by some distance, the part of Kubernetes that most rewards understanding over memorization.

Chapter 9 opens by giving every Pod an address, and then explaining why that is not enough.

> *"The chart tells you where the harbours are. It does not tell you how the water moves between them — and the water is what you are actually sailing on."*

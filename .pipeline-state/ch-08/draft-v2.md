# Chapter 8: Standing the Watch
## *"The commands you'll actually type, and the versions that bite"*

**Domain: Kubernetes Fundamentals — 44% of the exam · Competency: Cluster Administration — ~5% (authored allocation) · Complexity: Mixed · Novelty: Moderate**

*The 44% is CNCF's published domain weight. The ~5% is this book's own allocation across the competencies inside that domain: CNCF publishes weights for its four domains and not for the competencies within them. The front matter explains how these allocations were derived.*

<!-- AUTHOR-REVIEW: BLOCKING — three unattested claims on the metadata line above: (1) the 44% figure, (2) the domain NAME "Kubernetes Fundamentals", (3) the domain COUNT "four". The fact-accuracy audit confirms that the string "Kubernetes Fundamentals" appears in NO cached snapshot in this chapter's referenced set, and that `objectives_covered` fields across the 18 snapshots reference D1/D2/D4 — consistent with at least four domains but establishing no total. The curriculum-alignment audit reports the authority IS on disk at `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`, outside this chapter's referenced set. Resolution: add that snapshot to this chapter's referenced-snapshot set and tag all three facts against it — name, count, and percentage, not just the percentage. Do not ship this line untagged; it is the most consequential category of claim in a study guide. -->

---

## Attention Budget

**Total time: ~150 minutes | Recommended: split across two sessions, breaking after ☆ Taking Your Bearings #2**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 — The Grammar of a Command | 12 min | Low | Anytime |
| §2 — Three Gates and a Logbook | 20 min | **High** | Peak attention |
| §3 — Dividing a Shared Cluster | 12 min | Medium | When alert |
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

**On the session split:** the break after Bearings #2 puts the request path and the node in one session, and versions, disaster and synthesis in the other. It also isolates §6, the densest pure-recall block in this book, at the start of a fresh session, which is where it belongs.

---

> *"A watch is not a task you finish. It is a stretch of time during which the ship is your responsibility, and the log records what you did about it."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Eight questions before you begin. Your score picks your reading strategy, and no score is a bad one. Several of these ask you to reason rather than recall. Answer in your own words; one sentence is enough.

1. You have a command-line tool on your laptop that manages a server somewhere else. Before it can do anything at all, what does it need to know, and what changes when you become responsible for two of those servers instead of one?

2. Chapter 3 was emphatic that one component is the only way into a Kubernetes cluster — nothing else is designed to expose a remote service. Name that component, and say what that architecture implies about where you would put a security check.

3. A server receives a request to do something expensive. List the distinct questions it must answer before it does the work. Then say whether any of those questions could result in the request being *changed*, rather than simply accepted or refused.

4. Chapter 4 said namespaces are intended for environments with many users spread across teams or projects, and it named the mechanism by which cluster resources get divided between them. What was that mechanism called, and what do you think it constrains?

5. Chapter 7's built-in taint table included `node.kubernetes.io/unschedulable`, with a `NoSchedule` effect: a taint applied deliberately by an operator rather than automatically by a failing disk. Using Chapter 7's rule about that effect, what did it do to the Pods *already running* on the node?

6. Chapter 4 pointed at the `kube-node-lease` namespace and said the Lease objects in it are how the control plane knows a node is still alive. If those Leases stop being renewed, what *should* the control plane conclude, and what should it be careful not to conclude?

7. Two components of one system are running at different versions. One is a client, one is a server. Which direction of mismatch worries you more — a newer client talking to an older server, or an older client talking to a newer server — and why?

8. You run a service on a cloud provider's managed platform. A colleague runs the same service on hardware in a rack they own. Name two operational duties that are yours in one case and not in the other.

<details>
<summary>Answers + reading strategy</summary>

1. **An address and a credential, at minimum.** With two servers, *which* server becomes a piece of state you have to carry somewhere, which means the tool needs a notion of *current* target as well as *possible* targets.

2. **The kube-apiserver.** If every request in the cluster must pass through one component, that component is the natural and sufficient place to put access control. One door means one set of locks.

3. **Most people produce two questions: who are you, and are you allowed to do this.** If you produced two, that is the expected answer and you have just found the gap this chapter's §2 exists to fill. On the "changed" clause: if you said no, you are in the majority.

4. **Resource quota.** Most readers will say it constrains "how much a team can use," which is right as far as it goes. Hold on to what you guessed; §3 will sharpen it.

5. **Nothing.** `NoSchedule` governs new placements only, which raises an obvious follow-up question that §4 answers.

<!-- AUTHOR-REVIEW: the `NoSchedule`-governs-new-placements-only semantics is unverifiable against THIS chapter's referenced snapshot set. `k8s-docs-taints-tolerations-depth-2026-08-24` states in its own header that the core snapshot — `k8s-docs-taints-tolerations-2026-08-23` — "holds the core concept, the three effects and the four matching rules," and that snapshot is NOT among this chapter's 18. The depth cut deliberately does not restate effect semantics. Fix requires no fetch: add `k8s-docs-taints-tolerations-2026-08-23` to this chapter's referenced-snapshot set and tag this answer and Bearings #2 item 1's answer against it. The reference list is what is wrong, not the prose. -->

6. **It should conclude that it cannot tell.** An absent heartbeat is evidence of a *communication* failure, which could be a dead node or could be a network partition. Concluding "the node is broken" claims more than the evidence supports.

7. **A newer client talking to an older server is the more dangerous direction:** the client can ask for things the server has never heard of. That intuition is correct in general. §6 is where it stops being reliable.

8. **Common correct answers: patching and upgrades; backups; hardware replacement; capacity planning; certificate rotation.** Any two of these is a pass.

<!-- AUTHOR-REVIEW: the five-duty list above is unsourced. `k8s-docs-setup-tooling-2026-08-23` licenses only the EXISTENCE of a managed/self-hosted split ("consider which aspects of operating a Kubernetes cluster (or abstractions) you want to manage yourself and which you prefer to hand off to a provider"). It does not enumerate which duties sit on which side. kubernetes.io does not document commercial providers' responsibility models, so no fetch from that tree will close this. Either open a research gap for a vendor-neutral shared-responsibility source, or narrow to "which aspects move is a per-provider question." Same root cause as §5 L~"A managed control plane means…" and Practice Q13. -->

**If you got 6+ right:** skim. Read §2 and §6 properly — they carry this chapter's exam points — and work all three Taking Your Bearings checkpoints. The rest you can move through quickly.

**If you got 3–5 right:** read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** read carefully, and if questions 2, 4, 5 and 6 were among your misses, re-read *[cross-bearing: see Ch 3 §2 — the API server as the single door]* and *[cross-bearing: see Ch 4 §6 — namespaces and cluster-scoped objects]* before you start §2. Those two sections are the prerequisite base for more than half this chapter. Without Chapter 3's single-door architecture in place, §2 will read as an arbitrary list of three words.

</details>

---

## Why This Chapter Matters

`kubectl cordon node-7`.

Two words after the tool's name, and a machine goes out of service without disturbing a single running process. Chapter 7 ended by naming that command, telling you it was this chapter's opening move, and declining to explain it. Here it is.

The shape is the more interesting thing, though. You have been typing commands in exactly this form since Chapter 4 (`kubectl apply -f`, `kubectl get pods`, `kubectl scale`) and nobody has told you what the form *is*. It worked anyway. That is precisely the condition under which a candidate walks into the exam room confident and then loses five points to a question about which component is permitted to be one minor version newer than which.

Chapters 2 through 7 made you someone who can describe what should run and where. This chapter makes you someone responsible for the machine it runs on. That is a different posture, and the vocabulary shifts with it. On watch, you think in three questions: what can I take out of service safely, what can I stop other people doing, and what can I not get back. You are about to acquire all three.

And here is the doubt worth carrying through the next eight sections. By the end of this chapter you will not have learned a single new mechanism. Every administrative act in it — taking a node out of service, capping a team's resource consumption, registering a machine, refusing a malformed request — is a write through a door you already know, reconciled by a controller you already met. That claim should be hard to believe right now, because what follows looks like four unrelated subjects wearing one chapter number. §8 will make the case. Until then, keep score.

The stakes, stated plainly: about five points on this book's allocation, which is not many. What the number understates is the *shape* of those points. §6's version-skew material is the single most mechanically checkable block in the entire curriculum. The rules are exact, the numbers are small, and there is no partial credit for nearly remembering them, which makes it the easiest place in the exam to lose points you had every opportunity to keep. That is the whole case for reading this chapter carefully, and it does not need inflating.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Decompose** any `kubectl` command into its four slots, and say where the tool found the cluster it just talked to.
- **Trace** a request through the three gates it passes before anything is written down, and say what each gate can and cannot do about it.
- **Distinguish** a ResourceQuota from a LimitRange by what each constrains and at what scope, and say which of the two can make a previously valid Pod stop being accepted.
- **Take** a node out of service and put it back, predicting what happens to the Pods on it at each step.
- **Name** the two forms of node heartbeat and the control loop that watches them.
- **State** which Kubernetes components are permitted to disagree about their version, by how much, and in which direction — and derive the upgrade order from that one rule.
- **Recognise** every administrative act in this chapter as a write through one door, reconciled by a controller you already know, which is the only thing you actually have to remember.

*You'll also stop reading the version-skew table as arbitrary trivia. That is a smaller change than it sounds, and it is worth more exam points than anything else in Part II.*

---

## ⚪ §1 — The Grammar of a Command

You have been typing these for four chapters.

`kubectl apply -f deployment.yaml`. `kubectl get pods`. `kubectl scale deployment/web --replicas=5`. Every one of them worked. Nobody told you what the shape was, and you did not need to be told, which is exactly why it earns ten minutes now.

Here is the shape. Every `kubectl` invocation takes the form `kubectl [command] [TYPE] [NAME] [flags]` [source: k8s-docs-kubectl-overview-2026-08-23]. Four slots, of which NAME and flags are optional:

- **command** — the operation you want performed on one or more resources: `create`, `get`, `describe`, `delete` [source: k8s-docs-kubectl-overview-2026-08-23].
- **TYPE** — the resource type [source: k8s-docs-kubectl-overview-2026-08-23].
- **NAME** — the name of the specific resource. If the name is omitted, details for all resources are displayed [source: k8s-docs-kubectl-overview-2026-08-23].
- **flags** — optional. Flags you specify on the command line override default values and any corresponding environment variables [source: k8s-docs-kubectl-overview-2026-08-23].

Put five commands you have already run through those same four slots, and the shape appears retroactively.

<!-- FIGURE: ch08-fig01-kubectl-verb-resource-grammar -->
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
                    pod = pods = po      node-7 ≠ Node-7
```

**Figure 8.1 —** Five commands you already know, aligned on the same four slots. What to notice is the empty columns: `kubectl get pods` omits NAME and flags, and gets every Pod as a result; `kubectl cordon node-7` omits TYPE entirely, because the verb already implies what kind of thing it operates on. What to notice second is the asymmetry at the bottom, which is the examinable half of this section.

That asymmetry earns its own sentence, because it is the exact shape of an exam distractor. Resource types are case-insensitive, and you may use the singular, plural, or abbreviated form [source: k8s-docs-kubectl-overview-2026-08-23] — so `pod` and `pods` are the same thing. Resource *names* are case-sensitive [source: k8s-docs-kubectl-overview-2026-08-23]. The tool is relaxed about what kind of thing you meant and exacting about which one.

<!-- AUTHOR-REVIEW: the abbreviated form `po` is used in Figure 8.1's callout as an instantiation of the sourced singular/plural/abbreviated rule, but the specific string `po` appears in no cached snapshot. Near-certain and low-risk; flagged so a later pass can either source it or replace the callout's third form with `pods`. -->

> ★ **Fixed Point:** One grammar, four slots — `kubectl [command] [TYPE] [NAME] [flags]`. **Resource types are case-insensitive and abbreviable. Resource names are case-sensitive.**

### The verb surface

Here is the operations table. Read it as an inventory rather than a list of new things; you have met a third of it already.

| Verb | What it does | Where it lives in this book |
|---|---|---|
| `get` | List one or more resources | met in Ch 4 |
| `describe` | Display the detailed state of one or more resources | met in Ch 4 |
| `apply` | Apply a configuration change to a resource from a file or stdin | met in Ch 4 |
| `create` | Create one or more resources from a file or stdin | met in Ch 4 |
| `delete` | Delete resources from a file, stdin, or by label selector, name, or resource | met in Ch 4 |
| `scale` | Update the size of the specified replication controller / deployment | met in Ch 6 |
| `rollout` | Manage the rollout of a resource (deployments, daemonsets, statefulsets) | met in Ch 6 |
| `explain` | Get documentation of various resources | here |
| `config` | Modify kubeconfig files | here |
| `logs` | Print the logs for a container in a Pod | ahead, in Ch 13 |
| `exec` | Execute a command against a container in a Pod | ahead, in Ch 13 |

*(All verbs and descriptions: [source: k8s-docs-kubectl-overview-2026-08-23].)*

One entry deserves a sentence of its own. `explain` returns documentation for a resource type [source: k8s-docs-kubectl-overview-2026-08-23], which makes it one of only two verbs in the table that answers a question about something other than *your cluster* — `config`, which modifies kubeconfig files [source: k8s-docs-kubectl-overview-2026-08-23], is the other, and it answers a question about your laptop.

> ⚓ **Worth Securing:** `kubectl explain` is the entry in this table that pays off longest, because it queries the API's own documentation rather than your cluster's contents. Two years from now, when the resource types installed in your clusters are ones this book never heard of, it will still be the fastest way to find out what a field does.

<!-- AUTHOR-REVIEW: the previous draft's Worth Securing claimed explain "works on resource types you have never seen, including Custom Resource Definitions." The snapshot supports only "Get documentation of various resources (pods, nodes, services, etc.)"; nothing connects explain to CRDs. Narrowed above to what the source supports. If a kubectl-explain reference page is fetched later, the CRD claim can be restored. -->

*[cross-bearing: see Ch 4 §2 — apply, and the declarative model]*. Chapter 4 gave `apply` a single sentence and sent you here for the rest. This table is that payoff, and Chapter 4's larger point stands unchanged: the objects are declarations, and the imperative verbs work by changing declarations. *[cross-bearing: see Ch 6 — scale and rollout as workload operations]*.

### Where the cluster came from

The second real idea in this section is a question you have never had to ask, because the answer was already on your machine.

For configuration, `kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag [source: k8s-docs-kubectl-overview-2026-08-23]. That is the precedence, stated flat: a default location, an environment variable, and a flag. Per the general rule above, the flag wins over the environment variable [source: k8s-docs-kubectl-overview-2026-08-23].

If you answered Soundings question 1 with "an address and a credential," this is where that instinct lands. The file holds both, plus the answer to the two-server problem: which one you are currently talking to.

### The surprising case: `kubectl` inside a Pod

By default `kubectl` first determines whether it is running within a Pod, and thus inside a cluster. It starts by checking for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables, and for the existence of a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are found, in-cluster authentication is assumed [source: k8s-docs-kubectl-overview-2026-08-23]. And when `kubectl` runs in a cluster it acts against the namespace of the ServiceAccount, unless `--namespace` is given [source: k8s-docs-kubectl-overview-2026-08-23].

Chapter 4 used the second half of that fact once, in passing, in an answer key. Here it is in full: three environment checks, an assumed identity, and a different default namespace.

> 🪝 **Snag:** `kubectl` inside a Pod is not you, and does not look where you expect. It authenticates as the Pod's ServiceAccount and acts against that ServiceAccount's namespace [source: k8s-docs-kubectl-overview-2026-08-23]. Every practitioner who has ever run a debugging shell inside a cluster has been surprised by this at least once, usually by an empty `kubectl get pods` that they were certain should have returned something.

### The command that opens the chapter

`kubectl cordon node-7`.

Verb, name. No TYPE slot: the verb already implies what kind of thing it operates on, which is why the documented form is `kubectl cordon $NODENAME` [source: k8s-docs-nodes-2026-08-23] and not a three-token command. The grammar, instantiated, and the thing Chapter 7 promised would be Chapter 8's opening move *[cross-bearing: see Ch 7 §4 — the built-in taint node.kubernetes.io/unschedulable]*. What it does is what Chapter 7 already told you: it marks a node unschedulable, preventing the scheduler from placing new Pods onto that Node, without affecting the existing Pods on the Node [source: k8s-docs-nodes-2026-08-23].

That is all this section will say about it. Everything else belongs to §4: what it writes, what it does *not* do, what the second command is, and what happens if you skip that second command *[cross-bearing: see Ch 8 §4 — taking a node out of service]*. Carry the question with you; three sections from now it will have a better answer than it would have here.

---

## 🔵 §2 — Three Gates and a Logbook

Soundings question 3 asked you to list the distinct questions a server must answer before doing expensive work. If you produced two — *who are you*, and *are you allowed* — you produced the answer nearly everyone produces, and you have just located a hole in your own model. That is a good place to start reading from, and it deserves naming rather than skipping past: a reader who has just discovered their model is incomplete is the most receptive reader this chapter gets.

There are three.

Chapter 3 named them in passing, at the point the API server was introduced, and pointed here for the treatment *[cross-bearing: see Ch 3 §5 — the API server and what happens at its door]*. The Kubernetes documentation's own guidance on securing a cluster lists them in this relative order, among other entries — Controlling Access to the Kubernetes API, Authenticating, Authorization, Using Admission Controllers, and (further down the same list) Auditing [source: k8s-docs-cluster-administration-2026-08-23] — and the project's extension-point taxonomy names the same three as the API access extensions: authentication, authorization, and dynamic admission control via webhooks [source: k8s-docs-extending-kubernetes-2026-08-23].

<!-- AUTHOR-REVIEW: BLOCKING GAP, unchanged from draft-v1 and confirmed by the fact-accuracy audit as its largest cluster (19 instances). The three names and their relative order in a documentation table of contents are sourced (cluster-administration and extending-kubernetes, both tagged above). What is NOT sourced in any snapshot in this chapter's referenced set is the sequential-gate semantics this section is built on: (i) that a request passes the three IN ORDER, (ii) that admission runs AFTER authorization and BEFORE persistence, (iii) that admission controllers may MUTATE a request rather than only accept or reject it. All three are load-bearing for this section's Fixed Point, for ch08-fig02's fourth arrow, for Bearings #1 items 3 and 4, for Practice Q2/Q3/Q4, for two Exam Alert priority topics, and for Chapter 12's derivation of Pod Security Admission.

  The curriculum-alignment audit reports that the closing fetch was COMPLETED by the research stage but never landed on disk — `research-manifest.md` carries all ten new snapshots as string literals inside an unexecuted writer script, and `sources/` contains none of them. It reports the material as: "Admission Control modules are software modules that can modify or reject requests"; "When multiple admission controllers are configured, they are called in order"; and "Once a request passes all admission controllers, it is validated ... and then written to the object store." Those three sentences close (i), (ii) and (iii) outright.

  Resolution: run the research-manifest writer script so `k8s-docs-controlling-access-*` lands in sources/, then tag the Fixed Point below, Figure 8.2's caption, and the four affected answer keys against it. Two free upgrades available at the same time, both reported by the curriculum audit as present in that snapshot: the quorum contrast (authorization = any module approves and the request proceeds; admission = any module rejects and the request is refused immediately), which is a sharper Navigational Hazard than the one currently in this section; and "admission does not see reads," which is one clause and forecloses a plausible misreading. The mutating/validating PHASE split is optional at this tier — the outline never asked for it and Chapter 12 does not need it. Do not ship this section's ordering and mutation claims untagged. -->

### Gate one: authentication — *who are you?*

Authentication establishes the identity behind the request. The API server is configured to listen for remote connections on a secure HTTPS port, typically 443, with one or more forms of client authentication enabled [source: k8s-docs-control-plane-node-communication-2026-08-24].

The two identities you already have in the cluster arrive at this gate by different routes. Nodes should be provisioned with the public root certificate for the cluster, so that they can connect securely to the API server, along with valid client credentials; a good approach is for the kubelet's client credentials to take the form of a client certificate [source: k8s-docs-control-plane-node-communication-2026-08-24]. Automating the provisioning of those certificates is what kubelet TLS bootstrapping is for [source: k8s-docs-control-plane-node-communication-2026-08-24]. Pods, meanwhile, connect by leveraging a ServiceAccount: Kubernetes automatically injects the public root certificate and a valid bearer token into the Pod when it is instantiated [source: k8s-docs-control-plane-node-communication-2026-08-24]. That injected token is what `kubectl` is looking for in §1 when it checks for a ServiceAccount token file and decides it is running inside a cluster.

<!-- AUTHOR-REVIEW: the sentence above fuses two snapshots — kubectl-overview names the path /var/run/secrets/kubernetes.io/serviceaccount/token, and control-plane-node-communication says a bearer token is injected into the Pod. Neither states they are the same artefact. Near-certain; phrasing softened from "is the same file" to "is what kubectl is looking for" to stop short of asserting identity. Flagged for a later pass. -->

### Gate two: authorization — *may you do this?*

Authorization decides whether the identity established at gate one is permitted to perform *this action* on *this object*. One or more forms of authorization should be enabled, especially if anonymous requests or ServiceAccount tokens are allowed [source: k8s-docs-control-plane-node-communication-2026-08-24]. Securing your cluster means implementing effective authentication *and* authorization for API access: the pair, not either alone [source: k8s-docs-cloud-native-security-2026-08-23].

RBAC is Chapter 12's material in full *[cross-bearing: see Ch 12 — RBAC: Roles, ClusterRoles, and bindings]*. For now, one fact about it is enough: it is a mechanism that lives at this gate, and it has opinions about identities and verbs, not about the contents of your YAML.

<!-- AUTHOR-REVIEW: draft-v1 said "RBAC is one authorizer among several." The existence of multiple authorization modes is not established by any snapshot in this chapter's set — `extending-kubernetes` lists RBAC only as an example API resource ("such as ResourceQuota, NetworkPolicy and RBAC"). Clause removed above. The same controlling-access/ fetch flagged at the head of §2 closes this if the claim is wanted back. -->

### Gate three: admission control — *should this, exactly as written, be allowed?*

This is the gate you did not have.

Admission controllers see a request that has already been authenticated and authorized, and act on it before it is written down. And here is the property that makes them a genuinely different kind of thing rather than a third variation on "no":

Authentication and authorization answer yes or no. Admission may answer yes, no, or *yes — but not as you wrote it*.

> ★ **Fixed Point:** Authentication, then authorization, then admission. Authentication asks **who**. Authorization asks **may you**. Admission asks **should this, exactly as written, be allowed to happen** — and it is the only one of the three that can change your request instead of refusing it.

<!-- FIGURE: ch08-fig02-three-api-gates -->
```
                gate 1              gate 2              gate 3
           ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
 request ─►│Authentication├──►│Authorization ├──►│  Admission   ├──► persisted
           └──────┬───────┘   └──────┬───────┘   └──┬───────┬───┘     to etcd
                  │                  │             │       │              ▲
                  ▼                  ▼             ▼       │              │
               REJECT             REJECT        REJECT     └── REWRITTEN ─┘
```

**Figure 8.2 —** What to notice is the fourth arrow. Gates one and two have one way out other than forward: refusal. Gate three has two. It can refuse, or it can alter the request and let the altered version continue. The three questions, in order, are: *who are you*, *may you do this*, and *should this, as written, be allowed*.

> 🪢 **Mnemonic:** *Who, may, and how.* Three words, in order, one per gate. The third is the odd one because "how" is a question about the request rather than about you.

> ⚠ **Navigational Hazards:** Authorization and admission are not two names for the same check. **Authorization has no opinion about the contents of your request; admission has no opinion about your identity.** A request can be fully authenticated, entirely authorized, and still be rejected — or quietly rewritten — at the third gate. Candidates who collapse the two lose the diagnostic ability that makes this model useful: when a request you were definitely allowed to make is refused anyway, the gate model tells you where to look.

> **Extended Analogy:** Think of a working commercial harbour rather than a locked building. A vessel arriving is met first by a pilot boat, whose only question is *which vessel is this*: papers, registration, identity. That is authentication. It has no view on your business here.
>
> Once identified, the harbourmaster consults the berth allocations: is this vessel entitled to a berth in this harbour today? That is authorization. The harbourmaster does not open a single crate. The question is about standing, not about cargo.
>
> Then, and only then, the customs officer comes aboard. This one *does* open crates. She may find something prohibited and turn the whole vessel around. But she has a third option the other two lack: she may say the vessel can dock provided a particular container stays sealed, or provided a declaration is completed and attached before unloading. The vessel proceeds — altered. That is admission control, and the third option is the entire reason it is a separate office rather than one more line on the harbourmaster's form.

### Two admission controllers you have already met

This is not an abstraction you have to take on faith. You have seen it work twice.

Chapter 7 introduced the **NodeRestriction** admission plugin, which prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix [source: k8s-docs-assign-pod-node-2026-08-23]: the reason you can trust node-isolation labels not to have been forged by the node they describe. Chapter 7 stated the rule and pointed here for the enforcement *[cross-bearing: see Ch 7 §3 — node labels and the NodeRestriction plugin]*. This gate is the enforcement.

And the Pod Security Standards are enforced by the built-in Pod Security Admission controller [source: k8s-docs-pod-security-standards-2026-08-23]. That is one clause and no more; Chapter 12 owns the three profiles and the three modes *[cross-bearing: see Ch 12 — Pod Security Standards and Pod Security Admission]*. What matters here is the derivation: when you meet Pod Security Admission four chapters from now, you will not be learning a new kind of thing. You will be learning one instance of the third gate.

The same is true of §3's material, arriving next. ResourceQuota is one of the API resources used to configure a cluster [source: k8s-docs-extending-kubernetes-2026-08-23], and it takes effect at this gate rather than through a separate subsystem.

<!-- AUTHOR-REVIEW: no snapshot in this chapter's referenced set states that ResourceQuota and LimitRange are enforced by admission controllers. The claim is standard and near-certain, but unsourced here. Closed by the same controlling-access/ landing flagged at the head of §2, or by the admission-controllers reference page. -->

> 🔭 **Closer Look:** Dynamic admission control means the cluster calls out to a webhook *you* supplied. Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend, and the documentation is candid that this adds a potential point of failure [source: k8s-docs-extending-kubernetes-2026-08-23]. Which is to say: once you install a validating webhook, your webhook being down is a thing that can stop your cluster accepting requests. Deeper than the exam requires, and useful the first time you see a cluster that cannot create Pods for reasons that have nothing to do with Pods.

### And a logbook

Alongside the three gates, the cluster-administration guidance on securing a cluster lists **Auditing** [source: k8s-docs-cluster-administration-2026-08-23]. It sits in the same list, at the same level, as the three access-control pages.

For the exam's purposes, that placement is very nearly the whole of what you need: auditing exists, it is part of securing a cluster, and it is what tells you afterwards what happened.

<!-- AUTHOR-REVIEW: deliberately minimal, and now under-cautious rather than over-cautious. No snapshot in this chapter's referenced set defines what an audit record contains, what stages are recorded, or that auditing is policy-driven; the outline's Open Question #4 chose option (b) — name it, assert no definition — "unless the fetch is already cheap." The curriculum-alignment audit reports that the fetch WAS cheap and DID complete, and that the landed-but-unwritten snapshot carries: "Kubernetes auditing provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster." It also reports the clause "auditing lives inside the kube-apiserver," which is the single-door architecture stated a fourth way and costs nothing in a section built on that architecture. Once the research-manifest writer script runs, upgrade this from two sentences to three or four with those two facts tagged. Stages, levels and backends stay out — above budget, and G-8D confirms the level definitions were not verbatim-captured anyway. This is also the chapter's one PARTIAL objective (D1.2-08). -->

### Why three gates at one door is a complete story

Close on the architecture, because it is the reason this section is short enough to be learnable.

Kubernetes has a hub-and-spoke API pattern. All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24].

That is the load-bearing sentence. Three gates on one door would be an incomplete access-control story if there were other doors; you would be securing one entrance out of several. There are not. Chapter 3's single-door architecture is what makes a three-gate model *sufficient* rather than merely *present*, and it is why this chapter has a spine at all *[cross-bearing: see Ch 8 §8 — one door, and controllers behind it]*.

---

## 🔵 §3 — Dividing a Shared Cluster

Chapter 7 §2 left you with a complaint and an IOU. The complaint: nothing in what you had learned so far stops you booking the entire cluster with resource requests you will never actually use. The IOU: the mechanisms that stop *other people* doing that to *you* live here *[cross-bearing: see Ch 7 §2 — requests, and the cluster you could book by accident]*.

There are two of them, and the only mistake worth guarding against is swapping them.

**ResourceQuota.** Namespaces are a way to divide cluster resources between multiple users, via resource quota [source: k8s-docs-namespaces-2026-08-23]. That is the sentence Chapter 4 gave you and then deferred *[cross-bearing: see Ch 4 §6 — namespaces, and what they are for]*. A quota is a ceiling on a **namespace, in aggregate**: the team's total, not any one Pod's numbers.

**LimitRange.** The Kubernetes security guidance states the pair's purposes in a single sentence: define ResourceQuotas to fairly allocate shared resources, and use LimitRanges to ensure that Pods specify their resource requirements [source: k8s-docs-cloud-native-security-2026-08-23]. Read that carefully, because the two halves are doing different jobs. A quota *allocates*. A LimitRange *ensures Pods specify*, which is a constraint on **individual objects**, and a mechanism that has to be able to act on a manifest that says nothing at all.

<!-- AUTHOR-REVIEW: BLOCKING GAP, and the chapter's thinnest teaching block against the promises pointing at it. The snapshots in this chapter's referenced set support exactly two claims: that quota is the mechanism by which namespaces divide cluster resources among users (namespaces snapshot, tagged), and the functional contrast in the one cloud-native-security sentence (tagged). Everything about SCOPE, DEFAULTING, and WHAT A QUOTA COUNTS is unsourced — including the aggregate/per-object framing above, the Fixed Point below, Figure 8.3's `min ≤ … ≤ max` per-Pod bound, and Practice Q6's rebuttal of distractor A.

  The curriculum-alignment audit reports that both closing fetches COMPLETED and are sitting unwritten in `research-manifest.md`, and that they supply exactly what this section needs — including the single most examinable fact available here: "If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients **must** specify either `requests` or `limits`." That sentence is also the causal link between the section's two mechanisms and resolves the internal inconsistency flagged below. The limit-range snapshot supplies "Enforce minimum and maximum compute resources usage per Pod or Container in a namespace," which resolves Figure 8.3 in the FIGURE's favour — bring the prose up, do not cut the figure down. It also supplies "validations occur only at Pod admission stage, not on running Pods."

  Resolution: run the research-manifest writer script, then rebuild this section to take four things and no more — (1) what a quota counts (compute totals, object counts, storage — names only, per G-8C, which forbids quoting the row descriptions), (2) the 403 rejection, (3) the requests-must-be-specified rule, (4) LimitRange's min/max/default structure plus the admission-stage-only caveat. Scope guard, unchanged: do NOT take quota scopes, scope selectors, priority-class quota, or the full countable-resource roster — all above associate tier. -->

### The discrimination, made structural

Definitions are easy to swap. Questions are harder. If you can answer these two about a mechanism, you will never confuse them again:

**What is being counted?** The quota counts the namespace's total. The LimitRange counts one object's numbers.

**What happens to a manifest that says nothing about resources?** The quota may refuse it. The LimitRange may fill it in.

That second question is the sharper of the two, and it is not an accident that it echoes §2. This is the mutate-versus-reject distinction again, showing up one gate later in the same request's life.

> ★ **Fixed Point:** **ResourceQuota counts the namespace. LimitRange constrains the object.** One is a ceiling on a team; the other is a rule about a manifest.

<!-- FIGURE: ch08-fig05-quota-vs-limitrange -->
```
        ResourceQuota                          LimitRange
   ┌──────────────────────────┐          (no namespace boundary)
   │ namespace: team-atlas    │
   │  ┌────┐┌────┐┌────┐┌────┐│           ┌─────┐┌─────┐┌─────┐┌─────┐
   │  │Pod ││Pod ││Pod ││Pod ││           │ Pod ││ Pod ││ Pod ││ Pod │
   │  └────┘└────┘└────┘└────┘│           │min ≤││min ≤││min ≤││min ≤│
   │  ═══ namespace total ═══ │           │≤ max││≤ max││≤ max││≤ max│
   │  ═══════ AT CAP ════════ │           └─────┘└─────┘└─────┘└─────┘
   └──────────────────────────┘
             ▲                                       ▲
      5th Pod arrives:                    5th Pod arrives declaring
        REJECTED                          nothing:  ACCEPTED — with
   the namespace total is reached           defaults FILLED IN
```

**Figure 8.3 —** What to notice is that the two panels fail *differently*. On the left, a boundary is drawn around the namespace and the fifth Pod is refused. On the right, there is no namespace boundary at all — the constraints sit on individual Pods — and the fifth Pod is not refused but modified. Scope is the discrimination; the two failure modes are the proof.

> 🪝 **Snag:** A LimitRange that supplies a default request changes what your manifest means without changing your manifest. The Pod you get is not the Pod you wrote, and `kubectl get pod <name> -o yaml` is where you find out. If a Pod's scheduling behaviour surprises you in a namespace someone else configured, this is the first thing to check.

> ⚓ **Worth Securing:** The two are usually deployed together, and the reason is worth understanding rather than memorising: the quota sets the ceiling, and the LimitRange is what makes every team member's consumption legible to that ceiling. A quota alone constrains the total; it says nothing about whether any individual manifest declared what it intended to use.

<!-- AUTHOR-REVIEW: draft-v1's Worth Securing here said a quota with no LimitRange lets one request-less Pod consume the entire namespace allocation. The fact-accuracy audit flagged that as internally inconsistent with this section's own "the quota may refuse it" — if a quota refuses request-less manifests, that scenario cannot occur. Softened above to a claim that survives either resolution. The landed-but-unwritten resource-quotas snapshot settles it in favour of "the quota refuses it" (the requests-must-be-specified rule), at which point this callout can be rewritten to say so outright. Flagged as a PAIR with the "What happens to a manifest that says nothing" line above — whichever way the fetch resolves, both move together. -->

*[cross-bearing: see Ch 5 §8 — requests and limits, the numbers a LimitRange defaults]*

### The hinge, and it is worth thirty seconds

ResourceQuota and LimitRange are namespaced objects. The Nodes that §4 is about to discuss are not.

Chapter 4 established this and you may already feel where it goes: namespace-based scoping is applicable only for namespaced objects — Deployments, Services and so on — and not for cluster-wide objects such as StorageClass, Nodes and PersistentVolumes [source: k8s-docs-namespaces-2026-08-23].

So the two halves of "stop people using too much" sit on opposite sides of a boundary you already know. **You can quota a team. You cannot quota a machine.** There is no ResourceQuota that limits how many Nodes a group may consume, because a Node is not in a namespace and a quota is a statement about a namespace.

Say that out loud once, because Chapter 12 is going to *derive* the RBAC four-way matrix from exactly this boundary rather than asking you to memorise four combinations *[cross-bearing: see Ch 12 — namespaced and cluster-scoped permissions]*.

And one closing observation, offered rather than promised: both of these mechanisms take effect at the admission gate. Neither is a separate subsystem with its own enforcement path. That is the first instalment of a claim §8 will finish.

---

## ☆ Taking Your Bearings #1 — The Path a Command Takes In

Five questions on §1 through §3. Answer in your own words before checking; the effort of retrieval is what makes this stick.

**1.** ⚪ Decompose `kubectl describe node worker-3` into its four slots and name each one. Then say which of the four you could change the capitalisation of without breaking the command.

**2.** ⚪ You run `kubectl get pods` from a shell on your laptop, and again from inside a running Pod in the same cluster. Both succeed and return different results. Explain *both* differences — what identity each invocation used, and what namespace each looked in. Then say which source of configuration wins if both `KUBECONFIG` and `--kubeconfig` are set on your laptop.

**3.** 🔵 Name the three gates a request passes, in order. Then say which of them can result in the request being *changed* rather than accepted or rejected.

**4.** 🔵 A request is refused. You are told that the identity was valid, and that the identity had permission to perform this action on this resource. Which gate refused it, and give one plausible reason.

**5.** 🔵 **[retrieval: ch4]** Chapter 4 said namespaces are the unit by which cluster resources get divided between users, and it named the mechanism. Name it, say what scope it constrains — and then say what the *other* mechanism in §3 constrains instead.

<details>
<summary>Answers + explanations</summary>

**1.** `kubectl` / `describe` (command) / `node` (TYPE) / `worker-3` (NAME); there are no flags. **You could capitalise the TYPE freely**, since resource types are case-insensitive and accept singular, plural or abbreviated forms. You could not capitalise the name; names are case-sensitive.

*Common wrong turns:* "both are case-insensitive" and "both are case-sensitive" are the two tempting symmetrical answers, and the asymmetry is the whole point. `Node worker-3` works. `node Worker-3` does not.

**2.** From your laptop: `kubectl` used the kubeconfig at `$HOME/.kube/config` (or whatever `KUBECONFIG`/`--kubeconfig` pointed at), authenticated as *you*, and looked in the namespace of the current context. From inside the Pod: `kubectl` found `KUBERNETES_SERVICE_HOST`, `KUBERNETES_SERVICE_PORT` and the ServiceAccount token file, assumed in-cluster authentication, authenticated as the **ServiceAccount**, and acted against the **ServiceAccount's namespace**. Two different identities, two different namespaces, one command.

On precedence: **the flag wins.** Flags specified on the command line override default values and any corresponding environment variables, so `--kubeconfig` beats `KUBECONFIG`, which in turn beats the default `$HOME/.kube/config` location.

*Common wrong turns:* assuming the in-cluster invocation reads your kubeconfig anyway (it assumes in-cluster authentication instead); assuming it defaults to the `default` namespace (it uses the ServiceAccount's namespace, which may or may not be `default`); and answering the precedence half with "the environment variable, because it is set for the whole session" — the general rule runs the other way.

**3.** **Authentication, then authorization, then admission control.** Only admission can change the request.

The reason this matters is not that the third gate has an extra feature. It is the *reason there are three gates rather than one*. Two of them are asking about you and answering yes or no; the third is asking about the request itself and has a third answer available: yes, in modified form. When you meet Pod Security Admission in Chapter 12, you will be meeting an instance of this gate, and you will not have to learn a new kind of thing.

*Common wrong turns:* a two-gate answer (the most common incomplete model, and the one Soundings question 3 was built to expose); the order reversed; and attributing the mutation power to authorization.

**4.** **Admission.** Both earlier gates already said yes — the identity was established and the action was permitted — so the refusal came from the gate that looks at the request's *contents*. A plausible reason: the Pod would have exceeded its namespace's ResourceQuota, or a policy plugin rejected something about the object as written.

One plausible cause is enough. There is no need to enumerate admission controllers; the full plugin surface is out of scope here and Chapter 12 owns the policy landscape.

*Common wrong turns:* answering "authorization," which is the reflex answer and is ruled out by the question's own stipulation — you were told the identity had permission. Answering "authentication" makes the same mistake one gate earlier.

**5.** **ResourceQuota**, which constrains the **namespace in aggregate**. The other mechanism is **LimitRange**, which constrains **individual objects** and supplies defaults so that Pods specify their resource requirements at all.

*Common wrong turn:* swapping them — putting the aggregate ceiling on the Pod and the per-object rule on the namespace. This is the single most common error in this section, and the two diagnostic questions in §3 are the fix: *what is being counted*, and *what happens to a manifest that says nothing*.

</details>

**How'd you do?**

**5/5:** You have the request path. Move on to §4 with confidence.
**3–4:** Solid. Review the ones you missed, particularly if question 3 was among them, since §4 through §8 all lean on the gate model.
**0–2:** No shame in it, but do not continue yet. Re-read §2 before §4, about ten minutes. If question 5 was a miss as well, spend five more on §3's hinge. Everything from here builds on the idea that administrative acts are ordinary writes that pass ordinary gates.

**Checkpoint: you've now mastered**
✓ The four-slot grammar, and the case-sensitivity asymmetry inside it
✓ Where `kubectl` finds its cluster — on a laptop, inside a Pod, and which override wins
✓ The three gates, in order, and which one can rewrite you
✓ ResourceQuota versus LimitRange, by scope and by failure mode
☐ Taking a node out of service (next)

---

## 🔵 §4 — Taking a Node Out of Service

You have been carrying an open question since §1. Here is the answer, and it takes three commands rather than one, which is the entire reason it was worth waiting for.

### Where nodes come from

First, two sentences you have never been given, because they are the node-side instance of a pattern §8 is going to lean on.

There are two main ways to have Nodes added to the API server: the kubelet on a node self-registers to the control plane, which is the default, or you (or another human user) manually add a Node object [source: k8s-docs-nodes-2026-08-23]. After you create a Node object, the control plane checks whether it is valid — whether a kubelet has registered with the API server matching the `metadata.name` field of the Node — and if the node is healthy, meaning the necessary services are running, then it is eligible to run a Pod [source: k8s-docs-nodes-2026-08-23]. The name of a Node object must be a valid DNS subdomain name and must be unique [source: k8s-docs-nodes-2026-08-23].

Note what the two registration paths have in common. A kubelet joining a cluster and a human joining a machine to a cluster produce the same artefact: a Node object at the API server, which the control plane then validates. The kubelet does not open a private channel. It arrives at the same door you do.

### The three commands

Marking a node as unschedulable with `kubectl cordon $NODENAME` prevents the scheduler from placing new Pods onto that Node, but does not affect existing Pods on the Node; this is useful as a preparatory step before a node reboot or other maintenance [source: k8s-docs-nodes-2026-08-23]. `kubectl drain` evicts the Pods. `kubectl uncordon` restores scheduling [source: k8s-docs-nodes-2026-08-23].

Read the middle clause of that first sentence again. It is doing more work than its length suggests. `cordon` **deliberately leaves the running Pods alone.** That is not an oversight in the tool; it is the point of having a separate step. And it means the phrase "take a node out of service," which sounds like one action, is two.

> ★ **Fixed Point:** `cordon` stops arrivals and touches nothing already aboard. `drain` clears what is aboard. `uncordon` reopens. Three commands, three jobs — and **the maintenance sequence needs the first two.**

<!-- FIGURE: ch08-fig04-node-lifecycle-cordon-drain -->
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

**Figure 8.4 —** What to notice is what does *not* change between the first two panels. The three Pods aboard the cordoned node are still running, still serving, still entirely unaffected. Only the arriving Pod's fate differs. The node does not empty until `drain`.

> ⚠ **Navigational Hazards:** **A cordoned node is not an empty node.** If you cordon a node and then reboot it for maintenance, every Pod still on that node goes down with the machine. This is the single most consequential confusion in this chapter, and unlike most exam traps it has a real operational cost attached. The instinct that "take out of service" means "empty" is a reasonable instinct. It is also wrong, and the fix is one more command.

> 🪢 **Mnemonic:** A cordon is a rope across a doorway. It stops people coming in. It does not remove the people already inside.

**One exception, and you already have both halves of it.** Pods that are part of a DaemonSet tolerate being run on an unschedulable Node [source: k8s-docs-nodes-2026-08-23], because the DaemonSet controller automatically adds a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect to DaemonSet Pods [source: k8s-docs-daemonset-2026-08-24]. Chapter 6 taught DaemonSet as one-Pod-per-eligible-node; Chapter 7 taught the built-in condition tolerations. This is the point at which the two facts turn out to have been the same fact *[cross-bearing: see Ch 6 §7 — DaemonSet and node-local facilities]*.

### Node conditions

A Node's status contains Addresses (HostName, ExternalIP, InternalIP); Conditions; Capacity and Allocatable; and Info such as kernel version, container runtime and kubelet version [source: k8s-docs-nodes-2026-08-23]. `kubectl describe node <name>` shows them [source: k8s-docs-nodes-2026-08-23].

The conditions describe the status of all Running nodes [source: k8s-docs-nodes-2026-08-23]:

| Condition | True when |
|---|---|
| `Ready` | The node is healthy and ready to accept Pods. **False** if the node is not healthy and is not accepting Pods. **Unknown** if the node controller has not heard from the node in the last `node-monitor-grace-period` |
| `DiskPressure` | Pressure exists on the disk size |
| `MemoryPressure` | Pressure exists on the node memory |
| `PIDPressure` | Pressure exists on the processes |
| `NetworkUnavailable` | The network for the node is not correctly configured |

*(All five conditions and the three `Ready` values: [source: k8s-docs-nodes-2026-08-23].)*

Four of those you will meet as True or False. `Ready` is documented with three values, and the third one is the interesting one.

`Unknown` is not a fourth failure mode. It is the control plane declining to guess. `False` means the node reported itself unhealthy: the node is *talking to you* and telling you something is wrong. `Unknown` means nobody has heard from it, which could equally be a dead machine or a network partition between the machine and the control plane. Those two situations call for different interventions, which is why the distinction is preserved rather than collapsed. If you answered Soundings question 6 with "it should conclude that it cannot tell," you reasoned your way to the shape of this answer without the vocabulary.

Note the parameter named in the definition: `node-monitor-grace-period`. That is the window. This book will not give you a number for it, because the examinable fact is what `Unknown` *asserts*, not how many seconds preceded it, and a number you half-remember is worse than a parameter name you can look up.

<!-- AUTHOR-REVIEW: the curriculum-alignment audit reports that the landed-but-unwritten node-status snapshot documents a default of 50 seconds for node-monitor-grace-period. Per the outline's standing instruction, a value of this kind may be added as a DATED ILLUSTRATION and never as a rule. Optional; the section works without it and the examinable fact is unchanged either way. Same snapshot also supplies "SchedulingDisabled is not a Condition in the Kubernetes API," which is a ready-made 🪝 Snag for this subsection if the writer script is run. -->

### Heartbeats, and a control loop you already know

For nodes there are two forms of heartbeat: updates to the `.status` of a Node, and Lease objects within the `kube-node-lease` namespace, with each Node having an associated Lease object [source: k8s-docs-nodes-2026-08-23].

Chapter 4 pointed at exactly those Leases and said they were how the control plane detects node failure [source: k8s-docs-namespaces-2026-08-23] *[cross-bearing: see Ch 4 §6 — the four initial namespaces]*. That IOU is now settled: two heartbeat forms, one of them an object in a namespace you have already listed.

The node controller is a Kubernetes control plane component that manages several aspects of nodes: assigning a CIDR block to the node when it is registered; keeping its internal list of nodes up to date with the cloud provider's list of available machines; and monitoring the nodes' health — updating the `Ready` condition to `Unknown` when a node becomes unreachable, and triggering API-initiated eviction of all the Pods from the node if it stays unreachable [source: k8s-docs-nodes-2026-08-23].

Read that third job as a shape rather than as a list. It observes (heartbeats), it compares against what it expects, and it acts (condition update, then eviction). That is the control-loop pattern exactly: controllers read an object's `.spec`, possibly do things, and then update the object's `.status` [source: k8s-docs-extending-kubernetes-2026-08-23]. **The node controller is a control loop.** You met the pattern in Chapter 3, and you have seen five instances of it since *[cross-bearing: see Ch 3 §5 — the control loop]*. This is the sixth, and noticing that costs one sentence and buys §8 half its argument.

### Capacity and Allocatable

Chapter 7 §2 told you that what makes Capacity and Allocatable differ, and how that is configured, is this chapter's material *[cross-bearing: see Ch 7 §2 — Capacity, Allocatable, and what the scheduler counts]*. Here is the honest, partial payment.

'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods [source: k8s-docs-node-allocatable-2026-08-24]. The scheduler treats 'Allocatable' as the available capacity for Pods, and does not over-subscribe it [source: k8s-docs-node-allocatable-2026-08-24].

Capacity and Allocatable are two different numbers on the same Node object, and the second is the one the scheduler uses.

<!-- AUTHOR-REVIEW: draft-v1 stated here that "Capacity is the machine's total; Allocatable is what is left for your workloads after the node's own overheads are set aside," followed by an explanation of why they differ. The fact-accuracy audit correctly graded that as a CONTRADICTED claim rather than merely untagged: `k8s-docs-node-allocatable-2026-08-24`'s extraction note says outright that the Capacity → Allocatable relationship appears only as an image (node-capacity.svg) with no text equivalent, and instructs that "§2 must not state an arithmetic relationship between capacity and allocatable." "What is left after overheads are set aside" IS an arithmetic relationship, stated in words. The snapshot also never defines Capacity. Both sentences are cut above, leaving only the two verbatim-sourced facts plus a bare statement that the numbers differ.

  The Chapter 7 promise is therefore still unpaid. The curriculum-alignment audit reports the reserve-compute-resources snapshot completed and is sitting unwritten in research-manifest.md, carrying two facts that discharge it honestly: `kube-reserved` and `system-reserved` as the reservations that make the two numbers differ, and the motivation sentence "Pods can consume all the available capacity on a node by default. This is an issue because nodes typically run quite a few system daemons that power the OS and Kubernetes itself." Two sentences, no arithmetic (G-8E stands regardless), and the block gets shorter rather than longer — which also relieves the duplication the curriculum audit flags against Chapter 7 §2, where this pair was already covered once. If the script is not run, adjust Chapter 7's pointer to be chapter-scoped rather than section-pinned. Do NOT state an arithmetic relationship in any case. -->

The configuration detail — how much is reserved and by which flag — is above the associate tier and this book does not cover it. What the exam wants from you is the distinction: **Allocatable is the number the scheduler does arithmetic against.**

---

## ⚪ §5 — Who Owns the Control Plane

Everything so far in this chapter has been something you *do*. This section is about something you *own*, and the two are not the same question.

It is also, deliberately, the easiest reading in Part II. You have just come through the chapter's densest run and another one is waiting in §6. Read this one at an easy pace; nothing in it needs peak attention, and §6 will want all of yours.

### The planning questions

Before choosing how to build a cluster, the documentation asks you to consider [source: k8s-docs-cluster-administration-2026-08-23]:

- Do you want to try out Kubernetes on your computer, or do you want to build a high-availability, multi-node cluster?
- Will you be using a hosted Kubernetes cluster, or hosting your own?
- Will your cluster be on-premises, or in the cloud?
- Will you be running Kubernetes on bare-metal hardware, or on virtual machines?
- Do you want to run a cluster, or do you expect to do active development of Kubernetes project code?

Five questions, and the honest observation is that in most working lives the answers arrive already decided: by budget, by a compliance requirement, by what the platform team standardised on two years ago. Knowing the axes still buys you something, because it tells you what was traded away.

### The tools, split by what they are for

**For learning.** If you are learning Kubernetes, use tools supported by the Kubernetes community or in the ecosystem to set up a cluster on a local machine: **minikube**, which runs a single- or multi-node local Kubernetes cluster, and **kind** — Kubernetes IN Docker — which runs local clusters using Docker containers as nodes [source: k8s-docs-setup-tooling-2026-08-23].

**For production.** When evaluating a solution for a production environment, consider which aspects of operating a cluster you want to manage yourself and which you prefer to hand off to a provider [source: k8s-docs-setup-tooling-2026-08-23]. The options are managed and turnkey certified Kubernetes services from cloud providers, and self-managed clusters bootstrapped with **kubeadm**, the officially supported tool for creating clusters, used to install the control plane and join nodes [source: k8s-docs-setup-tooling-2026-08-23]. Other ecosystem tools include **k3s**, a lightweight distribution [source: k8s-docs-setup-tooling-2026-08-23].

> ⚓ **Worth Securing:** kind and minikube are not two names for the same thing, and the documented difference is architectural: kind runs its nodes as Docker containers, where minikube runs a single- or multi-node local cluster [source: k8s-docs-setup-tooling-2026-08-23]. Nodes-as-containers is what makes a kind cluster cheap to create and destroy.

<!-- AUTHOR-REVIEW: draft-v1's version of this callout asserted that kind is "the usual choice inside CI pipelines" and minikube "the usual choice when a human is sitting in front of it." Only the nodes-as-containers half is sourced; the prevailing-practice claims are unattested in any snapshot. Narrowed above to the documented architectural difference plus its direct consequence. If the ecosystem-practice claim is wanted, open a research gap or reframe it explicitly as the author's operational judgement rather than as documented fact. -->

### One requirement none of these removes

Whichever route you take, a container runtime — containerd or CRI-O — must be installed on every node, and `kubectl` is the command-line tool for managing any cluster [source: k8s-docs-setup-tooling-2026-08-23]. Kubernetes talks to that runtime through the CRI, the Container Runtime Interface, which exists precisely to support alternative container runtimes [source: k8s-docs-extending-kubernetes-2026-08-23].

That first clause is worth six chapters of your attention for one moment. Chapter 2 taught you the boundary between Kubernetes and the thing that actually starts containers, and taught it as an interface question *[cross-bearing: see Ch 2 — the CRI, and what Kubernetes does not do itself]*. This is the first time in this book that boundary has had an operational consequence. `kubeadm` will build you a control plane and join your nodes to it, and a container runtime must already be present on those nodes, because a container runtime is on the other side of a line the project deliberately drew.

<!-- AUTHOR-REVIEW: draft-v1 said kubeadm "will not put a container runtime on those nodes," which is an unsourced negative assertion about a tool's scope. The snapshot establishes the REQUIREMENT ("A container runtime (containerd or CRI-O) must be installed on every node") but not that kubeadm declines to satisfy it. Narrowed above to the sourced form, which carries the same pedagogical weight. Same fix applied to Bearings #2 item 4's key and Practice Q12's explanation D. -->

And the second clause is quietly the reason this book works. However the cluster was built — laptop, rack, or a provider's console — the tool is the same one, and the grammar is the one from §1.

### What ownership actually means

Also collect one small debt here: scheduler profiles are one of Kubernetes' scheduling extension points [source: k8s-docs-extending-kubernetes-2026-08-23], and configuring them means configuring a control-plane component *[cross-bearing: see Ch 7 §6 — scheduling profiles]*.

<!-- AUTHOR-REVIEW: draft-v1 asserted that scheduler profile configuration "lives in the control plane's own component configuration, which is a thing you can reach only if you own the control plane." `extending-kubernetes` names "scheduler plugins/profiles" as an extension point and stops there; both the location claim and the managed-platform-withholds claim are unsourced. Narrowed above to what the snapshot supports. Fetching .../docs/reference/scheduling/config/ would restore the fuller claim. -->

That is the general shape of the answer to Soundings question 8: some operational aspects sit with whoever runs the control plane, and which ones move is a per-provider question.

<!-- AUTHOR-REVIEW: BLOCKING. draft-v1 said here: "A managed control plane means the provider decides when you upgrade, and the provider holds the etcd backup. A self-hosted control plane means both are yours." The fact-accuracy audit grades this as untagged Cluster C (6 instances) and the curriculum-alignment audit concurs. `k8s-docs-setup-tooling-2026-08-23` licenses only the EXISTENCE of a split: "consider which aspects of operating a Kubernetes cluster (or abstractions) you want to manage yourself and which you prefer to hand off to a provider." It does not name upgrade timing and etcd custody as the two items on the managed side, and kubernetes.io does not document commercial providers' responsibility models, so no fetch from that tree closes this.

  The claim is load-bearing in three places: this paragraph, Bearings #2 item 5's key, and Practice Q13, whose correct answer B depends on it entirely. It is also §5's structural hinge into §6 and §7. Narrowed above to what the snapshot licenses, with the two specific duties demoted from assertion to the framing sentence below (which now reads as "the next two sections are about two such aspects" rather than "these are the two that move"). Resolution: either open a research gap for a vendor-neutral shared-responsibility source, or accept the narrowed form permanently and rewrite Practice Q13 so its key does not turn on the specific two. Same root cause as Soundings A8. -->

Which is precisely why the next two sections exist. **§6 is which versions are allowed to disagree. §7 is what you cannot get back.** Whoever owns the control plane owns both.

> **Logbook Entry:** The managed-versus-self-hosted decision is usually argued as a cost question, and cost is rarely what decides it in practice.
>
> A control plane is not, in itself, expensive hardware. What is expensive is the *calendar* attached to it: three minor releases a year, each with its own upgrade window, its own compatibility matrix, its own regression to discover in staging on a Thursday. Plus certificate expiries. Plus etcd backups you have to prove you can actually restore from, which is a different exercise from taking them. Plus the person who has to be reachable while all of that happens.
>
> Teams that self-host successfully are almost always teams that budgeted for that calendar deliberately, as a named piece of somebody's job. Teams that regret it are usually teams that priced the machines and not the Thursdays. Neither choice is the right one in general; plenty of organisations have excellent reasons to own the whole thing, and regulatory ones are only the most obvious. But the question worth asking out loud before you decide is not *can we run this*, it is *whose calendar does this go on*.

<!-- AUTHOR-REVIEW: draft-v1's Logbook Entry contained "Three modest machines will run one [control plane]" — an unattested operational sizing claim, and a number a reader might carry. Removed above; the paragraph's argument is unaffected. The "three minor releases a year" figure that remains is sourced in §6 [k8s-releases-cadence-2026-08-23]. -->

---

## ☆ Taking Your Bearings #2 — The Machine, and Whose It Is

Five questions on §4 and §5. Two of them reach back into earlier chapters.

**1.** 🔵 **[retrieval: ch7]** You cordon a node. Chapter 7 taught you a built-in taint with a `NoSchedule` effect that is applied deliberately by an operator rather than automatically by a failing component. Name that taint, and say what `cordon` therefore does — and does not do — to the Pods already running on the node.

**2.** 🟡 **Challenge item — this one is meant to be uncomfortable, and the intuition it breaks is a reasonable intuition.** An engineer cordons a node and immediately reboots it for maintenance. Three services go down. What did they skip, and why did the cordon not prevent it?

**3.** 🔵 A node stops responding. Its `Ready` condition changes. To what value — and what does that value mean that `False` would not?

**4.** 🔵 **[retrieval: ch2]** You bootstrap a cluster with kubeadm. Before any node in it can run a Pod, one piece of software must already be installed on that node. Name it, name the two implementations the documentation names, and say which interface Kubernetes uses to talk to it.

**5.** 🔵 §4 said the control plane learns a node is alive through two forms of heartbeat. Name both, and say which namespace holds the objects the second one uses.

<details>
<summary>Answers + explanations</summary>

**1.** The taint is **`node.kubernetes.io/unschedulable`**. `cordon` marks the node unschedulable, which prevents the scheduler from placing new Pods onto it — and **does not affect the Pods already running there.** They keep running.

The point of the question is the identity rather than the definition: `kubectl cordon` is not a special-purpose maintenance channel. It is Chapter 7's built-in taint arriving by an operator's hand instead of by a failing disk, and the scheduler then behaves exactly as Chapter 7 said it behaves.

*Common wrong turns:* answering **`drain`** to the command half — that is the command that *does* empty the node, and it is the next question. And answering that the running Pods are **evicted** — they are not; that is the whole content of §4's Navigational Hazard.

<!-- AUTHOR-REVIEW: this item was reworded per the research manifest's G-8A recommendation (a), which the curriculum-alignment audit flagged as the chapter's one LIVE CORRECTNESS ITEM. draft-v1's stem asked "what command APPLIES the node.kubernetes.io/unschedulable taint" and answered `kubectl cordon`. No cached source states that cordon applies that taint, and `k8s-docs-taints-tolerations-depth-2026-08-24` pulls the other way ("The taint will be added to a node when initializing the node to avoid race condition"). The stem now asks the reader to NAME the taint and say what cordon does, both of which are sourced. The Chapter 7 identity the item exists to test still lands. NOTE the second, separate gap: the `NoSchedule`-governs-new-placements-only semantics is not in this chapter's referenced snapshot set at all — fix by adding `k8s-docs-taints-tolerations-2026-08-23` to the reference list, per the note at Soundings A5. -->

**2.** They skipped **`kubectl drain`**. `cordon` stops new Pods arriving and deliberately leaves running Pods alone; the three services were still on that node when the machine went down.

If you got this wrong, you got it wrong for a sensible reason. "Take a node out of service" reads as one action, and in most operational vocabularies it *is* one action. Kubernetes splits it in two because there are real situations where you want arrivals stopped and the current occupants left in place: draining a node is disruptive, and you may want to cordon now and drain during a maintenance window. The split is a feature. It is also a trap, and the fix is one more command before the reboot.

**3.** **`Unknown`.** The node controller has not heard from the node within the `node-monitor-grace-period`. `False` would mean something different and more specific: the node reported *itself* unhealthy and not accepting Pods. `Unknown` is the control plane saying it has no current information, which is consistent with a dead machine and equally consistent with a network partition.

*Common wrong turns:* `False` (the intuitive answer, and the wrong one) and `NotReady` — which is not one of the condition's three documented values.

**4.** A **container runtime** — **containerd** or **CRI-O** — and Kubernetes talks to it through the **CRI**, the Container Runtime Interface.

*Common wrong turn:* **"Docker."** Chapter 2's whole point was that Kubernetes reaches a runtime through the CRI, and containerd and CRI-O are what the documentation names. Six chapters back that was an architectural point. This is the moment it becomes an operational one: the officially supported bootstrapper builds a control plane and joins nodes, and a runtime has to already be on those nodes, because it lives on the other side of the line.

**5.** The two forms are **updates to the `.status` of a Node**, and **Lease objects**. The Leases live in the **`kube-node-lease`** namespace, with each Node having an associated Lease object.

That second form is the payoff for Chapter 4's pointer at the four initial namespaces: `kube-node-lease` was listed there as the namespace holding Lease objects that let the kubelet send heartbeats so the control plane can detect node failure. Soundings question 6 pre-tested exactly this; if you answered "it should conclude that it cannot tell," you now have the mechanism underneath that instinct.

*Common wrong turns:* naming only one form (the `.status` update is the one most readers produce, and the Lease is the one that is easy to forget because it lives somewhere you have to have looked); and placing the Leases in `kube-system`, which is the namespace for objects created by the Kubernetes system generally, not the one dedicated to node leases.

</details>

**How'd you do?**

**5/5:** You own the node lifecycle. Take the recommended break here; §6 deserves a fresh start.
**3–4:** Good. If item 2 was a miss, re-read §4's Navigational Hazards before continuing; it is the one item in this chapter with an operational cost attached.
**0–2:** Re-read §4, about fifteen minutes, with Figure 8.4 open. Then take the break. §6 is the densest section in this book and it is not the place to arrive tired.

**Checkpoint: you've now mastered**
✓ How Node objects come into existence, and that both routes end at the same door
✓ `cordon` / `drain` / `uncordon`, and which two the maintenance sequence needs
✓ The five node conditions, and why `Ready` has three values
✓ Two heartbeat forms, where the Leases live, and the control loop watching them
✓ What you own when you own the control plane
☐ Which versions are permitted to disagree (next)

---

## 🟡 §6 — Versions That Are Allowed to Disagree

This section is a table. There is no honest way around that, and printing the table is the wrong way to teach it: a table you memorised in August is a table you have half-lost by October.

So take the rule first, before any numbers.

**Nothing in the cluster may be newer than the API server it talks to.**

Every component in a Kubernetes cluster is a client of one door. Chapter 3 established that; §2 built three gates on it. A client that is *newer* than its server is a client that may ask for things the server has never heard of: new fields, new resources, new behaviour that does not exist on the other end of the connection. That single sentence generates three of the five rows below. The numbers are then not five unrelated facts; they are the *sizes of the windows*.

### The vocabulary

Kubernetes versions are expressed as `x.y.z`, where x is the major version, y is the minor version, and z is the patch version, following Semantic Versioning terminology [source: k8s-version-skew-policy-2026-08-23].

The Kubernetes project maintains release branches for the most recent **three** minor releases [source: k8s-version-skew-policy-2026-08-23]. Kubernetes 1.19 and newer receive approximately one year of patch support; 1.18 and older received approximately nine months [source: k8s-releases-cadence-2026-08-23]. Applicable fixes, including security fixes, may be backported to those three release branches depending on severity and feasibility [source: k8s-version-skew-policy-2026-08-23].

### The cadence, which makes the branch count make sense

Since 2021 the project ships **three minor releases per year**, approximately every fifteen weeks, each following a release cycle led by a SIG Release team; patch releases are cut monthly from the supported branches [source: k8s-releases-cadence-2026-08-23].

Now put the two facts beside each other, because neither is memorable alone and together they are almost self-evident: three releases a year, across three supported branches, is close to a year of coverage, which is what the patch-support figure says. The three-branch rule is not an arbitrary number somebody picked. It is roughly what "about a year of support" costs at this release cadence.

*[cross-bearing: see Ch 17 — SIG Release, KEPs, and how a release gets made]*. You will meet the cadence again there, inside the governance material that explains why it is what it is. Make the connection now; it is the cheapest insurance this chapter offers against forgetting the number.

> 🪝 **Snag:** "Kubernetes supports the last two releases" is a common half-memory and it is wrong. It is **three**.

### The rules

> **Dead Reckoning:** The supported version skew, stated flat.
>
> | Component | Rule |
> |---|---|
> | **kube-apiserver** | In highly-available clusters, the newest and oldest kube-apiserver instances must be within **one** minor version of each other |
> | **kubelet** | Must not be newer than kube-apiserver. May be up to **three** minor versions older. (A kubelet older than 1.25 may only be up to two minor versions older.) With kube-apiserver at 1.36: kubelet at 1.36, 1.35, 1.34 or 1.33 |
> | **kube-proxy** | Must not be newer than kube-apiserver. May be up to three minor versions older than kube-apiserver, and up to three minor versions older *or newer* than the kubelet instance it runs alongside |
> | **kube-controller-manager, kube-scheduler, cloud-controller-manager** | Must not be newer than the kube-apiserver instances they communicate with. Expected to match the kube-apiserver minor version, but may be up to **one** minor version older, to allow live upgrades |
> | **kubectl** | Supported within **one** minor version, **older or newer**, of kube-apiserver. With kube-apiserver at 1.36: kubectl at 1.37, 1.36 or 1.35 |
>
> *(All five rules and both worked examples: [source: k8s-version-skew-policy-2026-08-23].)*

<!-- FIGURE: ch08-fig03-version-skew-window -->
```
                  older ◄───────── kube-apiserver ─────────► newer
                    -3      -2      -1       0       +1
                     │       │       │       ║       │

  kubelet            ●━━━━━━━━━━━━━━━━━━━━━━━┫
  kube-proxy         ●━━━━━━━━━━━━━━━━━━━━━━━┫
  controller-manager                 ●━━━━━━━┫
  scheduler                          ●━━━━━━━┫
  cloud-ctrl-manager                 ●━━━━━━━┫
  kubectl                            ●━━━━━━━╬━━━━━━━●
                                             ║
                                    ▲ the only bar that crosses
```

**Figure 8.5 —** The double line at 0 is the API server's minor version. For every component but one it is a wall: bars extend to the left and stop dead. `kubectl` is the single bar that crosses to the right. The axis is deliberately relative; the rules do not change when the version numbers do. Note that the HA kube-apiserver rule is not a bar here — it is a bound between two API servers rather than a bound relative to one.

### The exception, which is where the exam points are

`kubectl` is the only entry in that table permitted to be *newer* than the API server.

Everything in the first half of this section built an intuition — never newer, never newer, never newer — and for exactly one component that intuition is wrong. Worse, it is wrong in a way that looks like carelessness rather than like a rule, so candidates who half-remember the kubelet's generous three-minor window reach for it when the question is about `kubectl`, and lose the point twice over: wrong number, wrong direction.

There is a reason, and the reason is worth more than the fact. `kubectl` is a **user tool that addresses the cluster from outside**, not a component running as part of it. It is not participating in the cluster's internal consistency, so its compatibility window is about human convenience: you should be able to run one `kubectl` against a fleet of clusters that are not all on the same release. That is why it is the only symmetric window in the table.

> ★ **Fixed Point:** **Nothing may be newer than the API server.** kubelet may be up to **three** minors older. **`kubectl` is the single exception, in both directions, at one minor.**

> ⚠ **Navigational Hazards:** The kubelet rule and the `kubectl` rule are different rules, and candidates routinely apply the first to the second. **kubelet: three minors, older only. `kubectl`: one minor, either direction.** They are not the same number and they are not the same shape. If a question gives you a kubectl version, the number you want is one, and the direction is both.

> 🪢 **Mnemonic:** *Three back, three a year, three branches.* The kubelet's window, the release cadence, and the number of supported minor releases are all three. That is a coincidence, and it is a useful one: three of this chapter's numbers collapse into a single digit, which leaves you only one other number to hold, `kubectl`'s one, in both directions.

### What the rule implies about upgrade order

The order falls out of the rule and does not need memorising separately. If nothing may be newer than the API server, then the API server must be upgraded first; everything else follows behind it, within its permitted window. There is no second rule to learn here. Reverse the order and you would spend the upgrade window with components newer than the server they talk to, which the table forbids.

That is as far as this book goes. Writing an upgrade runbook is not in the curriculum, and the procedure differs by how the cluster was built anyway — which, as §5 noted, may not be a decision that was ever yours *[cross-bearing: see Ch 8 §5 — whose calendar the upgrade goes on]*.

**A note on the numbers in this section.** The rules above are stable. The specific releases are not: the roster supported at the time this book's sources were captured was 1.36, 1.35 and 1.34 [source: k8s-releases-cadence-2026-08-23], and by the time you sit the exam it will be a different three. Learn the rule and treat the numbers as an illustration of it. Nothing in this book's practice questions turns on which minor version is current, and nothing in the exam should either.

*[cross-bearing: see Ch 13 — version skew as a cause of failures you will otherwise misdiagnose]*. This material returns there, deliberately, in a form where you have to use it rather than recite it.

---

## 🔵 §7 — The One Backup That Matters

Short section. It is also the only material in this chapter where the consequence of getting it wrong cannot be undone afterwards, so read it at half speed.

Chapter 3 introduced etcd as a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data [source: k8s-docs-etcd-access-control-2026-08-24], and pointed here for what to do about that *[cross-bearing: see Ch 3 §2 — etcd, the cluster's memory]*.

All Kubernetes objects are stored in etcd [source: k8s-docs-etcd-backup-2026-08-23]. Every Deployment you have written in this book. Every ConfigMap and Secret. Every Service. Every Node object, including the ones a kubelet wrote itself in §4. All of it is one datastore's contents.

Which is why: periodically backing up the etcd cluster data is important to recover Kubernetes clusters under disaster scenarios, such as **losing all control plane nodes** [source: k8s-docs-etcd-backup-2026-08-23].

Sit with that scenario for a second, because it is more specific than "the cluster died." What that loss takes from you is not the objects' *effects*. It is the entire record of *intent*: every declaration that says what should be running, which is the only thing that lets the cluster put itself back together when something changes. Nothing can be reconciled, scheduled, scaled or healed against a record that no longer exists.

<!-- AUTHOR-REVIEW: draft-v1 asserted here that "Losing every control-plane node does not stop your worker nodes. The kubelets keep running the containers they were last told to run; traffic keeps being served." The fact-accuracy audit flags this as untagged Cluster E. `k8s-docs-etcd-backup-2026-08-23` names the disaster scenario and says nothing about what survives it; no snapshot in this chapter's referenced set describes kubelet behaviour when the API server is unreachable. The claim is near-certainly true and is exactly the kind of thing a reader benefits from knowing, but it is unsourced, and Bearings #3 item 4 was CONSTRUCTED around it ("you have to notice that 'running workloads' and 'cluster state' are different things"). Both this paragraph and that item's key are rewritten above and below to make the same pedagogical point WITHOUT asserting kubelet survival behaviour — the intent/effects distinction carries it. Resolution: open a research gap; kubernetes.io/docs/concepts/architecture/#kubelet or the static-pod / node-shutdown material are the likely closers. If it lands, restore the sharper original phrasing, which is better teaching. -->

### The mechanics

Backing up an etcd cluster can be accomplished in two ways: a built-in snapshot, `etcdctl snapshot save backup.db`, or a volume snapshot of etcd's storage [source: k8s-docs-etcd-backup-2026-08-23]. The `etcdctl` form takes optional `--endpoints`, `--cacert`, `--cert` and `--key` flags for a TLS-protected cluster [source: k8s-docs-etcd-backup-2026-08-23].

Restoring uses `etcdutl snapshot restore`, which operates directly on the etcd data files; after a restore, the control plane components are restarted against the restored data directory [source: k8s-docs-etcd-backup-2026-08-23].

<!-- AUTHOR-REVIEW: the TLS flags are named above because the backup snapshot lists them. No configuration guidance is given, deliberately: the etcd-access-control snapshot's note states that the source page's TLS configuration guidance was not verbatim-verified in that fetch. Do not expand this into how to configure etcd TLS without a fresh verified fetch. -->

> 🔭 **Closer Look:** Restore is not a command you run against a running cluster. `etcdutl snapshot restore` operates on the data files directly, and the control-plane components come back up against the restored directory afterwards. That is why restoring from a snapshot is a maintenance *event*, with a window, a plan, and somebody watching, rather than an operation you slip in between meetings.

### The fact that matters more than the commands

Two sentences, and read them together rather than separately.

The snapshot file contains all the Kubernetes state and critical information; keep it encrypted and store it outside the control plane nodes [source: k8s-docs-etcd-backup-2026-08-23].

Access to etcd is equivalent to root permission in the cluster, so ideally only the API server should have access to it [source: k8s-docs-etcd-access-control-2026-08-24].

Put them side by side and they say something you should feel rather than merely file away: **an unencrypted etcd snapshot sitting on a control-plane node is simultaneously your only disaster recovery and a complete compromise of the cluster, waiting for someone to copy it.** Not a credential *for* the cluster. Root *in* the cluster, in one file, at rest.

> ★ **Fixed Point:** Every object you have ever created lives in etcd. **Access to etcd is equivalent to root permission in the cluster.** A snapshot is therefore both your only route back from disaster and the most dangerous single file you own.

> ⚓ **Worth Securing:** "Store it outside the control plane nodes" is the entire point of that sentence, and it is the half people skip. A snapshot that lives only on the machines it exists to protect you against losing is not a backup. It is a copy that goes down with the original — the maritime word for which is *ballast*, not *lifeboat*.

Notice also that the second sentence is the single-door architecture stated from the other side. §2 said every request terminates at the API server. This says only the API server should reach the store behind it. Same claim, different direction *[cross-bearing: see Ch 8 §2 — one door, three gates]*.

And whose job is this? §5's answer applies: which operational aspects sit with a provider is a per-provider question, but on a self-hosted cluster this one is unambiguously yours, and it is the one duty in this chapter where doing it late is not the same as doing it.

*[cross-bearing: see Ch 12 — Secrets, and encryption at rest]*. Chapter 12 covers why "keep it encrypted" is not paranoia. It is the reason that clause is in the sentence.

---

## ☆ Taking Your Bearings #3 — The Two Things You Cannot Improvise

Five questions on §6 and §7. These carry the highest concentration of directly examinable material in the chapter.

**1.** 🔵 Your cluster's API servers are at 1.36. For each of the following, say whether it is supported: (a) a kubelet at 1.33; (b) a kubelet at 1.37; (c) a `kubectl` at 1.37; (d) a kube-scheduler at 1.34.

**2.** 🟡 State the one rule that generates three of the five rows of the skew table. Then name the two rows it does *not* generate, and say why each is different.

**3.** 🔵 How many minor releases does the project maintain release branches for? Roughly how long is patch support for 1.19 and newer? Roughly how many minor releases ship per year? Then say why those three numbers are consistent with each other.

**4.** 🟡 You lose every control-plane node. What have you actually lost — and what single artefact would let you get it back?

**5.** 🔵 An etcd snapshot is sitting, unencrypted, on one of your control-plane nodes. Give two *separate* reasons this is wrong.

<details>
<summary>Answers + explanations</summary>

**1.** (a) **Supported** — kubelet may be up to three minor versions older than kube-apiserver. (b) **Not supported** — kubelet must never be newer than kube-apiserver. (c) **Supported** — `kubectl` is permitted within one minor version in either direction, and this is the only component for which "newer" is allowed. (d) **Not supported** — kube-scheduler may be at most one minor version older than the API servers it talks to, and 1.34 is two behind 1.36.

Note carefully what this item is testing. It is not the version numbers; the roster will be different by the time you sit the exam. It is four rules, applied. Redo the question with the API servers at any minor version you like and the four answers stay in the same places.

**2.** The rule: **nothing may be newer than the API server.** It generates the kubelet row, the kube-proxy row, and the controller-manager/scheduler/cloud-controller-manager row.

The two rows it does not generate:

- **`kubectl`**, because `kubectl` is a user tool addressing the cluster from outside rather than a component running as part of it. It is not participating in the cluster's internal consistency, so its window is set by human convenience — one release either way, so that one installation can address clusters at slightly different versions.
- **The HA kube-apiserver row**, for a different reason: it is not a bound *relative to* an API server at all. It is a mutual bound *between* API servers — "the newest and oldest instances must be within one minor version of each other" — which is symmetric in both directions and so cannot be produced by a rule about what may be newer than the API server.

If you could answer this, you derived most of the table rather than memorising it, and that is the version of this knowledge that survives to exam day. The residue — two rows, both with reasons — is small enough to hold.

**3.** **Three** release branches. **Approximately one year** of patch support for 1.19 and newer. **Approximately three** minor releases per year, roughly every fifteen weeks.

They are consistent because three releases a year across three maintained branches comes close to twelve months of coverage: the branch count *is* the support window, expressed in releases instead of months. (Close, not exact — three fifteen-week cycles is about forty-five weeks, and the documented figure is "approximately 1 year.")

You will meet the cadence again in Chapter 17, inside the project's release-governance material, where SIG Release and the KEP process explain where those fifteen weeks go *[cross-bearing: see Ch 17 — SIG Release and the release cycle]*. That is not a throwaway pointer: this trio of numbers is among the most forgettable material in this book, and the Chapter 17 pass is when it gets its second look.

**4.** You have lost **the cluster's entire record of intent** — every object, since all Kubernetes objects are stored in etcd. Every declaration of what *should* be running is gone, which means nothing can be reconciled, changed, scheduled, healed or scaled.

The artefact that brings it back is **an etcd snapshot**.

The distinction the question is built on is between a system's *record of intent* and its *current effects*. Plenty of people's first answer to "we lost the control plane" is "everything is down," which conflates the two. What etcd holds is the declarations, and it is the declarations you cannot regenerate.

<!-- AUTHOR-REVIEW: this key was rewritten alongside §7's paragraph on the same claim. draft-v1's version said "Not the running workloads: kubelets keep running what they were last told to run, and traffic keeps flowing," which is unsourced in this chapter's referenced set (fact-accuracy Cluster E). The intent/effects framing above preserves the item's pedagogical construction without asserting kubelet survival behaviour. If a research gap closes the kubelet claim, restore the original — it is the sharper version of the same point. -->

**5.** **First:** it is not stored outside the nodes it protects against losing. The documented instruction is to store it outside the control plane nodes, precisely because a snapshot that lives only on the machines whose loss it insures against does not survive the event it exists for.

**Second:** access to etcd is equivalent to root permission in the cluster, and the snapshot contains all the Kubernetes state and critical information. An unencrypted snapshot is therefore a complete compromise of the cluster in a single readable file — every Secret, every configuration, everything — available to anyone who can read that disk.

Two reasons, two different failure modes: one about availability, one about confidentiality. A snapshot can fail you by not being there, or by being read.

</details>

**How'd you do?**

**5/5:** You have the two duties that cannot be improvised. §8 is a short read and then you are done with Part II.
**3–4:** Review your misses now rather than later. If item 1 or 2 was among them, spend ten minutes with Figure 8.5; the picture holds better than the table.
**0–2:** Re-read §6 with the derivation in mind: one rule, three rows, two rows with their own reasons. Do not try to memorise five rows flat. Then re-read §7, which is five minutes and has no numbers in it at all.

**Checkpoint: you've now mastered**
✓ The rule that generates most of the skew table, and the two rows it does not
✓ Three branches, one year, three releases a year — and why those agree
✓ What losing every control-plane node actually costs you
✓ Why an etcd snapshot is both your recovery and your largest single risk
☐ Why none of this was new (next, and it is the point of the chapter)

---

## ⚪ §8 — Rules, or Consequences

You were asked to keep score. Here is the claim.

**You did not learn a single new mechanism in this chapter.**

Every administrative act in it is a write through the one door you met in Chapter 3, reconciled by a controller you had already been introduced to. Take them in order.

**§1.** `kubectl` is a client of the API server. Not a management console, not a privileged back channel: a command-line client that assembles a request and sends it to the same endpoint your Pods use. Chapter 3's single door, addressed from a terminal.

**§2.** The three gates are not a subsystem bolted onto the side. They are what the single door *does* before it writes anything down. Chapter 3 told you every request terminates at the API server; §2 is the "and then what" of that sentence.

**§3.** A ResourceQuota is an object. You `apply` it exactly as you apply a Deployment. It takes effect because something reads it when other requests arrive, which means a quota is a **declaration that changes what other declarations are permitted to say.** Nothing about it is a special-case enforcement engine.

**§4, and this is the one that should land.** `kubectl cordon` has no private channel to the node. It does not connect to the machine. It is a write through the API server, and the scheduler then does what the scheduler always does: it checks taints when it makes scheduling decisions [source: k8s-docs-taints-tolerations-depth-2026-08-24], finds the node marked unschedulable, and places nothing there. Nothing about `cordon` is new. It is Chapter 7's mechanism with an operator's hand on it.

<!-- AUTHOR-REVIEW: this paragraph was narrowed. draft-v1 asserted that cordon "writes a field on a Node object" and that "Chapter 7's built-in taint machinery — the node.kubernetes.io/unschedulable taint — was already watching for exactly that." The fact-accuracy audit flags the causal link as unsourced (Cluster D): three separate facts are cached — cordon prevents scheduling new Pods [nodes]; node.kubernetes.io/unschedulable:NoSchedule exists as a built-in taint [daemonset, taints-depth]; the scheduler checks taints [taints-depth] — and NO cached sentence connects the first to the second. The word `spec` appears in no snapshot in this chapter's set in connection with node unschedulability, and taints-depth attributes automatic taint creation to node CONDITIONS, which unschedulability is not. Practice Q10 rests on the same inference and is narrowed to match.

  The curriculum-alignment audit reports the landed-but-unwritten node snapshot carries "cordoned nodes are marked Unschedulable in their spec" verbatim, which converts this from reasoned inference to sourced claim outright and is the single highest-leverage sentence for this section. Run the writer script, then restore the fuller derivation here AND in Practice Q10's key. Alternative if the script is not run: fetch the NodeSpec API reference for `.spec.unschedulable`. -->

**§4 again.** The node controller observes heartbeats, compares them against what it expects, and acts: updating a condition, then evicting. It is a control loop. It is the sixth one in this book, and you could have predicted its structure without being told.

**§6.** The skew rules are the compatibility contract of that same one door. Read the table again with that in mind and every row is answering one question: *which clients will this door accept?*

**§7.** etcd is what is behind the door, and the reason only the API server should reach it is the same reason there is only one door in the first place.

> ☀️ **Zenith:** One door, and behind it controllers you have already met. Everything in this chapter is a write to the first, reconciled by the second — which is why a chapter that looked like four unrelated subjects turns out to have a single spine, and why the horizon it opens onto is one you can already read.

<!-- FIGURE: ch08-zenith-consequences-not-rules -->
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

**Figure 8.6 —** What to notice is the chapter number beside each controller. This is Chapter 3's architecture diagram, unchanged, except that you have now put your own hands on the left-hand side of it, and every mechanism on the right-hand side is one you were taught somewhere in Part II. What to notice second is that no arrow on the left reaches a controller directly. There are no side channels.

<!-- AUTHOR-REVIEW: this anchor does not conform to the anchor_id_pattern's `ch{NN}-fig{MM}-{slug}` form — there is no figMM segment — and its caption reads "Figure 8.6". The structural contract's anchor_id_pattern accepts `ch\d{2}-(fig\d{2}|zenith)-[a-z0-9-]+`, so the zenith form is VALID and the linter passes it; the image-specs stage nonetheless flagged it, along with the broader problem that anchor fig numbers were not assigned in draft order (fig05 captions as Figure 8.3, fig03 captions as Figure 8.5). Anchors are the join key to image-specs.md and Rule 3 forbids changing them mid-revision, so all six are preserved verbatim. Recommend renumbering anchors to draft order in ONE sweep — draft and image-specs together — before any figure is commissioned. -->

### Rules, or consequences

Chapter 7 closed by saying this chapter is where the rules turn into consequences. That is the sentence to land on.

A list of administrative rules is among the least memorable material any study guide can put in front of you, and this chapter contained a great many of them. A set of consequences of a single architecture is a different thing entirely. If you can hold **one door, and controllers behind it**, you can regenerate most of this chapter without ever having memorised it, and you can go further than that. When you meet a Kubernetes administrative feature this book does not cover, the two questions that will get you most of the way are already in your hands.

> ⚓ **Worth Securing:** Faced with an unfamiliar Kubernetes administrative feature, ask two questions in this order: **what object does it write**, and **what controller is watching that object?** Those two questions answer most of them, and where they do not, they at least tell you what kind of thing you are looking at.

### Where the claim overreaches

One honest correction, because the claim as stated is slightly too neat and you would notice.

§5 and §6 are not consequences of the architecture. Which bootstrap tool is officially supported, how many release branches the project maintains, and how far a kubelet may lag: these are facts about a *project*, made by people in meetings, and no amount of understanding the single-door model will let you derive them. They have to be learned. That is exactly why §6 flagged them as memorisation and gave you a derivation for three of the five rows anyway. The parts that can be reasoned about should be reasoned about, and the residue should be admitted as residue.

Chapter 4 §6 established this book's habit of narrowing a claim until it is true rather than leaving it broad and impressive *[cross-bearing: see Ch 4 §6 — the habit of narrowing a claim until it is true]*. So: **every administrative *act* in this chapter is a write through one door, reconciled by a controller you already know. The project's *policies* are not, and those are the parts you memorise.** That version survives contact with the exam.

---

## Exam Alert! 🚨

**High-priority topics**, in descending order of this book's confidence about where the points sit — CNCF does not publish per-competency weights, so this ordering is authored judgement, not a published ranking:

1. **The three gates, in order** — authentication, then authorization, then admission control.
2. **Only admission can change the request.** The other two accept or refuse.
3. **kubelet may be up to three minor versions older than kube-apiserver, and must never be newer.**
4. **`kubectl` is the only component permitted to be newer** — within one minor version, in either direction.
5. **Three supported minor releases**, approximately one year of patch support (1.19+), approximately three minor releases per year.
6. **`cordon` stops arrivals; `drain` evicts.** A cordoned node is not an empty node.
7. **`Ready` is three-valued.** `Unknown` means the control plane has not heard from the node, which is not the same claim as `False`.
8. **ResourceQuota is namespace-aggregate; LimitRange is per-object.**
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
| "Authorization and admission are two words for the same check" | Authorization has no opinion about the request's contents; admission has no opinion about your identity |
| "`Ready: False` is what an unreachable node reports" | An unreachable node shows `Unknown`. `False` is a node that reported *itself* unhealthy |
| "A ResourceQuota limits how big any one Pod can be" | That is LimitRange. A quota is an aggregate ceiling on the namespace |
| "`kubectl` inside a Pod behaves as it does on your laptop" | It detects in-cluster conditions, authenticates as the ServiceAccount, and acts against that ServiceAccount's namespace |
| "Resource names are case-insensitive, because resource types are" | Types are. Names are not |
| "Upgrade the nodes first, then the control plane" | API server first. Reverse it and you spend the window with components newer than the server they talk to |
| "An etcd snapshot on the control-plane node is a backup" | It is a copy that goes down with the thing it was protecting — and, unencrypted, a root-equivalent credential |

---

## Practice Questions

Eighteen questions. Several require two sections at once; that is deliberate, because the exam does not organise itself by chapter section either. Answers and full explanations follow the set.

**1.** Which statement about `kubectl` command syntax is correct?

A) Both resource types and resource names are case-insensitive
B) Resource types are case-insensitive and may be given in singular, plural or abbreviated form; resource names are case-sensitive
C) Resource types are case-sensitive; resource names are case-insensitive
D) Both resource types and resource names are case-sensitive

**2.** In what order does a request pass the API server's access-control gates, and which of them can result in the request being modified rather than accepted or rejected?

A) Authorization → authentication → admission; only authentication can modify
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
C) Authentication; no — the API server rejects the request before identity is established
D) Admission control; yes — quota enforcement is skipped for cluster-admin identities

**5.** Which pairing correctly describes ResourceQuota and LimitRange?

A) ResourceQuota bounds an individual Pod's resources; LimitRange caps a namespace's total
B) Both cap a namespace's aggregate consumption; LimitRange additionally supplies defaults
C) ResourceQuota caps a namespace's aggregate consumption; LimitRange constrains individual objects and supplies defaults
D) ResourceQuota applies to cluster-scoped objects; LimitRange applies to namespaced objects

**6. [retrieval: ch4]** A platform team wants to cap the number of Nodes that a particular application team may consume. Why can they not do this with a ResourceQuota?

A) A ResourceQuota can only constrain objects the team creates, and the team does not create Nodes
B) Nodes are not namespaced objects, and a ResourceQuota constrains a namespace
C) ResourceQuota is evaluated at the authorization gate, which has no visibility into Nodes
D) They can; a ResourceQuota in the `kube-system` namespace applies cluster-wide

**7. [retrieval: ch5]** A namespace has a LimitRange that supplies a default CPU request. A developer submits a Pod manifest that declares no resource fields at all. The Pod is accepted, with the default filled in. What has changed about where this Pod can be placed, compared with the manifest as written?

A) Nothing — defaults are recorded for reporting but are not used in placement decisions
B) It can now be placed on fewer nodes, because it now books capacity against Allocatable that it did not book before
C) It can now be placed on more nodes, because a declared request lets the scheduler relax its filtering
D) Nothing — placement is decided from limits, not requests

**8.** You are told: "take node worker-3 out of service and clear it before the maintenance window." Which commands accomplish this, and in what order?

A) `kubectl drain worker-3`, then `kubectl cordon worker-3`
B) `kubectl cordon worker-3`, then `kubectl drain worker-3`
C) `kubectl cordon worker-3` alone — draining is implied
D) `kubectl uncordon worker-3`, then `kubectl drain worker-3`

**9.** A node stops responding to the control plane. What value does its `Ready` condition take, and what does that value assert?

A) `False` — the node has reported that it is unhealthy and not accepting Pods
B) `NotReady` — a distinct value used only for unreachable nodes
C) `Unknown` — the node controller has not heard from the node within the grace period
D) `Unreachable` — the node controller has confirmed a network failure

**10.** `kubectl cordon node-7` marks a node unschedulable. Which statement best describes how the effect reaches the scheduler?

A) `cordon` opens a direct connection to the kubelet on that node and instructs it to refuse new Pods
B) `cordon` is a write through the API server; the scheduler subsequently observes the node's marked state and places nothing there
C) `cordon` removes the Node object, so the scheduler no longer sees the node as a placement candidate
D) `cordon` reconfigures the scheduler's own component configuration to exclude that node

**11. [retrieval: ch3]** The node controller notices that a node has stopped reporting, updates a condition, and eventually evicts that node's Pods. Name the pattern, and name two earlier components in this book that work the same way.

A) A webhook; the Pod Security Admission controller and the NodeRestriction plugin
B) A control loop; the Deployment controller and the scheduler's watch on unscheduled Pods
C) A daemon; the kubelet and kube-proxy
D) A reconciliation batch job; the DaemonSet controller and etcd's compaction

**12.** Which statement about cluster bootstrap tooling is correct?

A) kubeadm is intended for local learning environments; kind is the officially supported production bootstrapper
B) kubeadm is the officially supported tool for creating clusters, installing the control plane and joining nodes; kind and minikube are for local learning environments
C) k3s is the officially supported tool for creating clusters; kubeadm is a lightweight distribution
D) minikube is the officially supported tool for creating clusters; kubeadm removes the need for a container runtime on each node

**13.** Two teams run the same application. Team A uses a cloud provider's managed Kubernetes service; Team B self-hosts on their own hardware. Which pairing correctly separates a duty that sits with whoever operates the control plane from one that does not?

A) Both duties sit with the control-plane operator: taking etcd backups, and writing the application's Deployment manifests
B) Neither duty sits with the control-plane operator: choosing container images, and setting resource requests
C) Taking etcd backups sits with the control-plane operator; setting the namespace's ResourceQuotas does not
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

**16.** A cluster is being upgraded from 1.35 to 1.36. Which component is upgraded first, and why does the rest of the order follow without needing to be separately specified?

A) The kubelets first, so that nodes are ready before the control plane expects the new API — the rest follows because kubelets may lag by three minors
B) kube-apiserver first, because nothing may be newer than it — every other component's window is expressed relative to the API server, so upgrading it first is the only order that never puts a component ahead of the server it talks to
C) `kubectl` first, because it is the only component allowed to be newer than the API server
D) The order is not derivable from the skew rules and must be memorised separately from the published upgrade runbook

**17.** An operations team stores its nightly etcd snapshots, unencrypted, on the primary control-plane node. Which statement best describes the problem?

A) There is no problem, provided the node's filesystem permissions are correct
B) The snapshots should be encrypted, but their location is fine because that is where etcd runs
C) They should be encrypted and stored off the control-plane nodes
D) The snapshots should be taken with `etcdutl` rather than `etcdctl`, which encrypts them automatically

**18.** You encounter a Kubernetes administrative feature this book has not covered. Based on §8's synthesis, what are the two most productive questions to ask about it first?

A) Which CNCF project maintains it, and what stage is it at?
B) What object does it write, and what controller is watching that object?
C) Which kubectl verb invokes it, and which flags does it take?
D) Which node does it run on, and which port does it listen on?

---

### Answers and Explanations

**1. B.**
Resource types are case-insensitive and accept singular, plural or abbreviated forms; names are case-sensitive. **A is wrong** because it flattens the asymmetry in the permissive direction, the single most common form of this error, because the tool's tolerance about types encourages the assumption. **C is wrong** because it inverts the asymmetry — the tempting answer for a reader who remembers that the two differ but not which way round, and `node Worker-3` failing while `Node worker-3` succeeds is the disproof. **D is wrong** in the strict direction: `kubectl get PODS web-01` works perfectly well.

**2. C.**
Authentication, then authorization, then admission; only admission can modify. **A is wrong** on both order and mutator: authentication establishes identity and has no view on the request's contents at all. **B** has the order right and attributes mutation to the wrong gate — authorization decides whether an identity may perform an action, and has no opinion about what the request says. **D** gets the order right and then gives all three gates a power only the third has, which is the error that collapses three distinct gates into one undifferentiated "security check."

**3. C.**
Both earlier gates already returned yes, so the refusal came from the one that examines contents. **A is wrong**: an expired credential fails at gate one, and the question states the identity was valid. **B is wrong** because it misdescribes authorization; authorization decides whether an identity may perform an action on a resource, and the question stipulates that it did. **D is wrong** and is the trap for readers still working from a two-gate model: passing authentication and authorization is necessary, not sufficient.

**4. B.**
Quota enforcement happens at the admission gate, and a quota constrains the namespace regardless of who submitted the request. **A is wrong** twice: wrong gate, and it imports a rule that does not exist, since quota is not an identity-scoped check. **C is wrong** because a quota violation cannot be detected before the request's contents are read, which is well after identity is established. **D** gets the gate right and then invents an administrator exemption; the appeal of this distractor is that it *feels* like how permissions usually work, which is exactly why it is worth defusing.

**5. C.**
Quota is the aggregate ceiling on the namespace; LimitRange constrains individual objects and supplies defaults so Pods declare their requirements. **A is wrong** because it swaps them, which is the only real mistake available in this section. **B is wrong** because it gives both mechanisms namespace-aggregate scope, losing the scope distinction that is the actual content. **D is wrong**: both are namespaced objects, and the scope difference between them is *within* a namespace, not across the namespaced/cluster-scoped boundary.

**6. B. [retrieval: ch4]**
Nodes are cluster-scoped, and a ResourceQuota is a statement about a namespace. Chapter 4 established the boundary; §3 turned it into an operational consequence. **A reaches the right conclusion by the wrong route** — it is true that the team does not create Nodes, but that is not why a quota cannot cap them. A quota is scoped to a namespace, and a Node is not in one; the obstacle is scope, not authorship. Notice that A's reasoning would also predict, wrongly, that a quota could cap Nodes if the team *did* create them. **C is wrong** on the gate. **D is wrong**: `kube-system` is a namespace like any other, not a privileged scope from which cluster-wide policy can be issued.

**7. B. [retrieval: ch5]**
Chapter 5 established that requests are the number the scheduler filters on, and §4 of this chapter established that the scheduler treats Allocatable as available capacity and does not over-subscribe it. A Pod that previously declared nothing now books capacity, so nodes that would have accepted it may now fail to fit it. **A is wrong**: the defaulted value is a real field on a real object and is used exactly as if you had written it. **C inverts the effect**; declaring a request adds a constraint, it does not relax one. **D is wrong** on which of requests and limits the scheduler reads.

<!-- AUTHOR-REVIEW: the "requests are the number the scheduler filters on" attribution to Chapter 5 is unverifiable in this chapter's referenced snapshot set. `k8s-docs-node-allocatable-2026-08-24`'s frontmatter lists `requests-as-scheduling-input` and `podfitsresources` under concepts_covered, but no transcribed sentence in the snapshot states it. The Allocatable half of the explanation IS sourced. Flagged for a later pass; the item's correct answer does not depend on the unverified half. -->

**8. B.**
`cordon` first to stop new arrivals, then `drain` to evict what is already there. Note the grammar: `cordon` and `drain` take the node's name directly, without a preceding TYPE, because the verb already implies the resource type. **A has the right two commands in the wrong order**, which would drain a node that is still accepting new Pods; the scheduler may place work onto it while you are clearing it. **C is the chapter's headline trap**: `cordon` does not empty anything. **D begins by making the node schedulable again**, which is the opposite of the instruction.

**9. C.**
`Ready` becomes `Unknown` when the node controller has not heard from the node within the `node-monitor-grace-period`. **A is the intuitive wrong answer** and misstates the evidence: `False` means the node *told you* it is unhealthy, which requires the node to be talking. **B is wrong**: `NotReady` is not one of the condition's three documented values. **D is wrong** and asserts a diagnosis the control plane deliberately declines to make; the whole value of `Unknown` is that it does not claim to know why.

**10. B.**
`cordon` is an ordinary write through the API server, and the scheduler subsequently declines to place Pods on the marked node. **A is wrong and is worth rejecting emphatically**, because it is precisely the belief §8 exists to dismantle: there is no private channel from your terminal to a node. **C is wrong**: the node is still there, still running its Pods, and `uncordon` restores it — none of which would be true if the object had been deleted. **D is wrong**: scheduler component configuration is a control-plane concern that has nothing to do with marking one node unschedulable, and a per-node maintenance action that required editing scheduler config would be unusable at any scale.

<!-- AUTHOR-REVIEW: this item was rewritten. draft-v1's version asked which PART of the Node object cordon writes, keyed to `spec`, with the explanation "cordon marks the node unschedulable, a statement of desired state, which lives in spec" and "the mechanism is a taint and an unschedulable marker, not a label." Neither `spec` nor the taint-mechanism link is sourced in this chapter's referenced snapshot set (fact-accuracy Cluster D). The rewritten item tests the same §8 synthesis — no side channels — using only what IS sourced. If the research-manifest writer script runs and "cordoned nodes are marked Unschedulable in their spec" lands, the original spec-vs-status framing can be restored, and it is the better item because it also discharges the Chapter 4 retrieval. NOTE: the `[retrieval: ch4]` tag was removed from this item along with the spec/status framing, and the retrieval count is held at 7/33 by the new Bearings #2 item 5 — see the retrieval note below the answer key. -->

**11. B. [retrieval: ch3]**
Observe, compare, act: it is a control loop, the same pattern as the workload controllers in Chapter 6 and the scheduler's watch in Chapter 7. Controllers read an object's `.spec`, possibly do things, and then update the object's `.status` — which is exactly the node controller's shape. **A is wrong**: admission plugins act synchronously on inbound requests rather than reconciling observed state against declared state. **C is wrong**: the kubelet and kube-proxy are node agents, and "daemon" describes where they run rather than how they work. **D is wrong** on the pattern and on the first example — nothing here is batched, and the DaemonSet controller is itself a control loop rather than a batch job.

**12. B.**
kubeadm is the officially supported tool for creating clusters, installing the control plane and joining nodes; kind and minikube are the documented local learning tools. **A swaps the two categories.** **C swaps kubeadm and k3s**: k3s is a lightweight distribution, not the official bootstrapper. **D is wrong twice**: minikube is not the production bootstrapper, and no bootstrapper removes the container-runtime requirement — a runtime must be installed on every node, which is the Chapter 2 boundary showing up as an operational requirement.

**13. C.**
Taking etcd backups is a control-plane duty; setting a namespace's ResourceQuotas is a workload-side concern that belongs to whoever runs the workloads, on either team. **A pairs one control-plane duty with one workload duty and calls both control-plane** — writing Deployment manifests is the application team's job whoever operates the cluster. **B calls both duties workload-side**, which is right about images and requests but names no control-plane duty at all, so it does not answer the question asked. **D inverts the pairing**: a container runtime must be installed on every node regardless of who operates the control plane, and etcd backup is the control-plane duty — this one is the sharpest distractor because both halves sound like platform work.

<!-- AUTHOR-REVIEW: this item was rewritten. draft-v1 asked which duties belong to the self-hosting team and not the managed-platform team, keyed to "deciding when the control plane is upgraded, and taking etcd backups." That key depends entirely on the managed/self-hosted duty split flagged as BLOCKING at §5 — no cached source names upgrade timing and etcd custody as the two items on the managed side, and kubernetes.io does not document commercial providers' responsibility models. The question-quality audit independently flagged the same item for its weak distractor set (option D was a throwaway; A and C were the same distractor twice).

  The rewrite changes the axis being tested from "which duties does a PROVIDER take over" (unsourceable) to "which duties belong to whoever operates the control plane" (sound on the architecture alone, and what §5 actually establishes). The four options are now a genuine four-way discrimination rather than a two-option question. If a vendor-neutral shared-responsibility source is ever landed, the original managed-vs-self-hosted framing is the better exam simulation and can be restored. -->

**14. D.**
kube-proxy must not be newer than kube-apiserver, so 1.37 against a 1.36 API server is unsupported. **A is supported**: kubelet may be up to three minor versions older. **B is supported**: `kubectl` is the one component permitted to be newer, within one minor. **C is supported**: the scheduler may be up to one minor older. Note that B and D differ only in which component is one version ahead, which is the whole of the distinction being tested. As with Bearings #3 item 1: the roster will have moved on by the time you sit the exam, and the four answers stay in the same places at any API server version you like.

**15. C.**
`kubectl`, within one minor version in either direction, because it is a user tool addressing the cluster from outside rather than a component running as part of it. **A is the chapter's most durable error**: the kubelet's three-minor window is generous, but it runs in one direction only. **B applies the same mistake to kube-proxy**, which is also older-only relative to the API server — note that kube-proxy *is* permitted to be newer than the *kubelet* alongside it, which is what makes this distractor tempting, but the question asks about the API server. **D states the general rule correctly and forgets that there is exactly one exception**, which is the answer of a candidate who learned the principle and not the table.

**16. B.**
Nothing may be newer than the API server, so the API server goes first, and the rest of the order is a consequence rather than a second rule. **A inverts it**, and the reasoning it offers is the trap: the kubelet's generous three-minor lag is a rule about how far behind a kubelet may be, not a licence to run one ahead. Upgrade the kubelets first and, for the duration of the window, they are newer than the API server — the one thing the table forbids outright. **C confuses "may be newer" with "should go first"**; `kubectl` is not part of the cluster's upgrade sequence at all, since it is the tool you run the upgrade *with*. **D is wrong** and is worth rejecting on principle: this is the one place in §6 where the material is genuinely derivable, and a candidate who reaches for memorisation here has learned the table without learning the rule.

**17. C.**
Two independent failures. A backup stored only on the machines it insures against losing does not survive the event; and access to etcd data is equivalent to root permission in the cluster, so an unencrypted snapshot is a complete compromise in one readable file. **A is wrong** because filesystem permissions do not address either failure; they do not make the file survive the node's loss, and they are a thin defence for something this valuable. **B accepts the location** on a reasoning error: etcd running there is the reason the snapshot must *not* live there. **D invents an encryption behaviour**; `etcdutl` is the restore tool, and no cached documentation attributes automatic encryption to either utility.

**18. B.**
What object does it write, and what controller is watching that object. Those two questions locate almost any Kubernetes feature within a model you already hold. **A is a reasonable second question** and a poor first one; provenance tells you about the feature's maturity, not about how it works. **C describes the surface** rather than the mechanism, and will leave you memorising verbs. **D asks about a process**, which is the wrong altitude: most administrative features are not processes at all, they are objects and the controllers that reconcile them.

<!-- AUTHOR-REVIEW: retrieval-practice accounting after this revision, for the audit trail. draft-v1 carried 7 tagged retrieval items across 32 Bearings+Practice questions (21.9%), against [B3]'s 20% target. This revision removes the `[retrieval: ch4]` tag from Practice Q10 (whose spec-vs-status framing was unsourceable) and adds one Bearings item (#2 item 5, heartbeats — untagged, since it tests §4's own material and merely completes the Ch 4 pointer) plus one Practice item (Q16, upgrade order — untagged). Tagged retrieval is therefore 6 of 34 = 17.6%, BELOW the 20% floor. Restoring Q10's spec-vs-status framing once the node snapshot lands returns it to 7 of 34 = 20.6% and closes this. If the snapshot does not land, add one `[retrieval: ch6]` item to the §4 block instead — the DaemonSet-tolerates-unschedulable fact is the natural candidate and is fully sourced [k8s-docs-daemonset-2026-08-24]. Both ≥4-back floor items are preserved: Bearings #2 item 4 (ch2, six back) and Practice Q11 (ch3, five back). -->

---

## Chapter Summary

| Concept | Remember this |
|---|---|
| `kubectl` grammar | `kubectl [command] [TYPE] [NAME] [flags]`. Types case-insensitive and abbreviable; **names case-sensitive** |
| kubeconfig | `$HOME/.kube/config` by default; `KUBECONFIG` or `--kubeconfig` override it, and per the general flags-override-environment rule, the flag wins |
| `kubectl` in a Pod | Detects the two env vars plus the ServiceAccount token file; authenticates as the ServiceAccount; acts against that ServiceAccount's namespace |
| The three gates | **Authentication → authorization → admission.** Who, may, and how |
| Admission's distinction | The only gate that can change the request instead of refusing it |
| Auditing | Named alongside the three gates as part of securing a cluster |
| ResourceQuota | A ceiling on a **namespace in aggregate** |
| LimitRange | Constrains **individual objects** and supplies defaults so Pods declare their requirements |
| The scope hinge | You can quota a team. You cannot quota a machine — Nodes are not namespaced |
| Node registration | kubelet self-registration is the default; a human may also create the Node object. Both routes end at the API server |
| `cordon` | Stops new Pods. **Leaves running Pods entirely alone** |
| `drain` | Evicts the Pods `cordon` left running |
| `uncordon` | Restores scheduling |
| DaemonSet exception | DaemonSet Pods tolerate an unschedulable node |
| Node conditions | `Ready`, `DiskPressure`, `MemoryPressure`, `PIDPressure`, `NetworkUnavailable` |
| `Ready: Unknown` | The control plane has not heard from the node. Not "the node is broken" — "we cannot tell" |
| Heartbeats | Two forms: `.status` updates, and Lease objects in `kube-node-lease` |
| Node controller | Assigns a CIDR at registration, syncs with the cloud provider's machine list, monitors health. **A control loop** |
| Allocatable | The compute available for Pods. The scheduler treats it as available capacity and does not over-subscribe it |
| Bootstrap tooling | kubeadm officially supported for creating clusters; minikube and kind for learning; k3s lightweight |
| Everywhere | A container runtime — containerd or CRI-O — must be on every node, reached through the CRI |
| The generating rule | **Nothing may be newer than the API server** |
| kubelet skew | Never newer; up to **three** minors older |
| `kubectl` skew | **One** minor, **either direction** — the sole exception |
| HA API servers | Newest and oldest within **one** minor of each other — a mutual bound, not a bound relative to the API server |
| Supported releases | **Three** branches, ~1 year of patch support (1.19+), **~3** minor releases per year |
| Upgrade order | API server first, because nothing may be newer than it. The rest follows without a second rule |
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

That last part is the difficulty, and it is worth feeling the shape of it before Chapter 9 answers it. Pods are, by design, disposable: a controller may replace one at any moment, and the replacement is a different Pod. So the cluster contains a large number of network endpoints, each perfectly valid, none of them stable, and applications that need to talk to each other anyway.

<!-- AUTHOR-REVIEW: this closing teaser previously asserted "Every Pod gets an address." That is Chapter 9's material and is unsourced in this chapter's referenced snapshot set (no networking snapshots are cached here). Removed above; the paragraph's tension survives without it, and Chapter 9 opens by establishing it properly. The remaining claim — that a controller may replace a Pod and the replacement is a different Pod — is Chapter 6 material the reader already has. -->

Part III is how that works: addresses, the abstraction that makes them survivable, how names resolve, and how anything outside the cluster gets in at all. You have just spent a chapter learning that everything administrative is a write through one door. Networking is where you find out what the cluster does with everything *behind* that door, and it is, by some distance, the part of Kubernetes that most rewards understanding over memorisation.

Chapter 9 opens by giving every Pod an address, and then explaining why that is not enough.

> *"The chart tells you where the harbours are. It does not tell you how the water moves between them — and the water is what you are actually sailing on."*
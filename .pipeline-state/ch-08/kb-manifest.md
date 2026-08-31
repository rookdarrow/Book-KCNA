I have what I need — every structural claim below was verified on disk, not inherited from the prior manifest.

```markdown
# Knowledge-Base Manifest — KCNA Chapter 8

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 8 — Standing the Watch
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-30

**Inputs consulted:** the finalized chapter (verified identical to `ch-08/draft-v2.md` — L523 and L1163 match the integration report's citations); `ch-08/integration.md`; `ch-08/outline.md` frontmatter (`kb_tags`: 58 concepts, 9 commands, `objectives: ["D1.2"]`); shipped `chapter-01` … `chapter-11`; the eleven prior `kb-manifest.md` files; `book-outline/term-ownership.md`, `section-skeleton.md`, `retrieval-architecture.md`; `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`; `certcomp/pipeline/context_packer.py` and `stages.py`.

---

## Structural findings — four, all re-verified rather than inherited

**1. ⚑ Nothing below reaches disk. The knowledge base still does not exist.**

`stages.py:228-229` gives stage 14 exactly one output, `{ch}/kb-manifest.md`. A repo-wide search of `certcomp` for `=== WRITE` / `=== APPEND` returns **one** file — `pipeline/prompts/14_knowledge_base_update.md`, the prompt itself. No parser consumes these blocks. `C:\dev\lodestar\Book-KCNA\knowledge-base\` does not exist.

I did not write the files directly, and the reason is not just the stdout convention. Replay order is load-bearing: `control-loop.md` is **created by ch-03 and appended to by ch-07, ch-08 and ch-09**. Writing Chapter 8's version first would install my append as the file's origin and delete ch-03's canonical ★ Fixed Point. That is precisely the drift Rule 6 forbids. **The correct fix is a replay harness that applies ch-01 → ch-11 in order, not eleven stages each writing what it can reach.**

**Twelve chapters' knowledge base now sits unapplied across eleven manifests** (ch-01 … ch-11; Chapter 12+ not yet drafted).

**2. ⚑ New finding — the prior manifest's shard filenames would not have resolved even if replayed.**

`context_packer.resolve_kb_shards` (lines 166-203) looks for exactly `{book_dir}/knowledge-base/{category}/{tag}.md`, where `tag` comes from the chapter outline's `kb_tags`. **A shard whose filename is not a `kb_tags` slug is never loaded by any stage.**

Chapter 7's manifest respects this — `taint.md`, `toleration.md`, `feasible-node.md`, `nodename.md` are all verbatim ch-07 `kb_tags` entries. The **prior ch-08 manifest does not**: `kubectl-grammar.md`, `resource-quota-and-limitrange.md`, `node-lifecycle.md`, `cluster-bootstrap-tooling.md` are none of them tagged by any chapter, and would have been written and then never read.

Every shard created below is named for a Chapter 8 `kb_tags` slug. The cost is that one body of treatment sometimes has to pick a slug (§4's three commands live under `cordon`); the benefit is that the shards actually load. A table of the tags left without an owner is at the end of the shard section.

**3. ✅ This manifest closes domain D1 — and one prior note saying otherwise is stale.**

ch-09's manifest records, as of 2026-08-25: *"STILL UNRECORDED, SEVENTH CHAPTER RUNNING: D1.4 (Chapter 2), because Chapter 2's Stage 14 never ran."* **Chapter 2's Stage 14 did run** — `ch-02/kb-manifest.md` exists (dated 2026-08-24 15:24) and records `| D1.4 | Chapter 2 | deep | 2026-08-24 |`, plus a correction to Ch 7's transcription of Ch 2 as D1.1. ch-03's original flag was correct when written and was overtaken.

With Chapter 8's row appended, **Kubernetes Fundamentals (44%) is fully recorded**: D1.1 Ch 3 (+Ch 4, object layer), **D1.2 Ch 8**, D1.3 Ch 7, D1.4 Ch 2. The domain-level audit ch-08 recommended and ch-09 called overdue can now actually be run.

**4. ⚑ Inherited caveat, still live.** The finalized chapter carries three `AUTHOR-REVIEW` comments recording deliberate non-assertions (the Capacity→Allocatable arithmetic, etcd TLS configuration, and research gap **G-8G**, the managed/self-hosted duty split). All three are accurate, not stale, and the glossary gap rows below depend on them. The integration report's eleven recommended fixes are also unapplied as of this stage.

---

## ⚑ Canon drift — one hard flag, and it is not the one the integration report found

### The control-loop ordinal is a three-way collision, not a two-way one

The integration report flags Chapter 8's "sixth control loop" against shipped Chapter 6's *"twice now… the third time is the one that matters."* Correct, and it is the finding I would fix first. **But the report checked backwards only, and the shard records a conflict it did not see.**

`concepts/control-loop.md` already carries an explicit instruction from ch-09's Stage 14:

> **⚑ NO ORDINAL IS RECORDED HERE, DELIBERATELY.** `chapter-09:1145` calls kube-proxy "the sixth control loop in this book, and you should count it." Shipped Chapter 8 already claimed "the sixth" twice… **Do not renumber to "seventh" without deciding whether Chapter 9 consumes one ordinal or two.**

Two things have changed since that was written, and both matter:

- **Chapter 9's revision already solved this, and solved it the right way.** `chapter-09:931` now reads: *"You have met that shape in **Chapters 3, 4, 6, 7 and 8**, and here it is again in a reference page about packet forwarding."* The ordinal is gone; a chapter list replaced it. That is the convention the integration report proposes for Chapter 8, already shipped in the next chapter. **Chapter 8 is now the only chapter in the book still counting.**
- **Chapter 9's list is itself wrong about Chapter 7,** which is a second-order defect nobody has flagged. Chapter 7 contains exactly one occurrence of the phrase, at `chapter-07:266`, and it is a *disavowal*: *"The last chapter ended on the one thing the control loop cannot do. It creates a Pod. It does not decide where the Pod goes."* Chapter 7 does not instantiate the loop; it defines itself against it.

**Three consequences for the author, in order of cost:**

1. Applying integration fix **[X1]** (drop Chapter 8's ordinal) is necessary and safe. Chapter 9's list names Chapter 8, so Chapter 8 must keep *a* control loop — the integration report's replacement wording does, and I have written the shard to match.
2. Integration fix **[R1]** — swapping Practice Q11's keyed example off the scheduler because Chapter 7 disowns it — is **more right than the report knew**, and it is in tension with `chapter-09:931`. Either Chapter 9's list drops Chapter 7, or Chapter 7 gains a loop instance. My recommendation is to drop it from Chapter 9's list: Chapter 7's disavowal is load-bearing for its own opening, and Chapters 3, 4, 6 and 8 are four solid instances without it.
3. **Running ordinals have now caused three collisions in this book** (Ch 8 vs Ch 6; Ch 8 vs Ch 9-as-drafted; Ch 9's list vs Ch 7). B6 recorded a fourth in the pluggable-interface count. This is past the threshold for a book-level convention: **state the pattern and name the chapters; never state the count.** Recorded in the shard append below.

The shard append records **no ordinal**, per ch-09's standing instruction, and adds the Chapter 7 finding.

### Not drift, recorded so a later stage does not "fix" it

- **`node-conditions.md` is created here and appended to by ch-09.** ch-09's append verifies `see Ch 8 §4 — node conditions` resolves and re-reads `NetworkUnavailable` through Chapter 9's model. No conflict; ordering only.
- **Competency name.** The chapter's metadata line says *"Competency: Cluster Administration."* The curriculum says **"Administration"** (`cncf-kcna-curriculum-pdf-2026-08-23.md:13`), and `chapter-09:192` uses its own competency name verbatim (*"Competency: Networking"*). Chapter 8 is the outlier. One-word fix; recorded on the objective-coverage row rather than silently normalized.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**52 terms contributed — 45 defined verbatim from the chapter · 7 recorded as gaps.**

Appended as a Chapter 8 block, not merged into a single A–Z. Re-transcribing prior chapters' prose to preserve one alphabet is exactly the definitional drift Rule 5 forbids; book assembly merges alphabets mechanically.

### Priority rows — the gaps Stage 13 flagged

Where the chapter defines nothing, the row records what the chapter *does* say and names the gap. It does not launder a paraphrase into canon.

| Term | What the chapter says | Status |
|---|---|---|
| **context (kubeconfig context)** | Nothing definitional. §1 describes the concept unnamed — the kubeconfig holds "the answer to the two-server problem: which one you are currently talking to" — and the word then appears **in graded text**: Bearings #1 A2, "looked in the namespace of the current context." | ⚑ **gap — highest priority.** B7 `term-ownership.md:269` assigns *Context (kubeconfig context)* to **Ch 8 §1** as both owner and first appearance. A term reaching an answer key may not be glossary-only. Integration fix **[G0]** supplies a one-sentence in-place definition; take it |
| **mutating / validating admission webhook** | Neither phrase appears. §2 defines the parent: dynamic admission control means "Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend," which "adds a potential point of failure" | ⚑ **gap — now unowned book-wide.** B7 claims first appearance at Ch 6 §8; shipped Ch 6 contains **zero** occurrences of "webhook." Curriculum-alignment deliberately excluded the phase split. **Ch 17 §4 collects admission webhooks among the extension points and does not define them** — so unless this closes, Ch 17 collects a term the book never taught |
| **CIDR** | Named, never expanded: "assigning a CIDR block to the node when it is registered" (§4), repeated in the Chapter Summary | ⚑ **gap.** Zero prior reader-facing occurrences in Ch 1–7; Ch 9's only instance is inside an `AUTHOR-REVIEW` comment. **Ch 8 §4 is first use book-wide**, which makes B7's acronym-register row (CIDR → Ch 10 §6) wrong. Expand in place |
| **kubelet TLS bootstrapping** | "Automating the provisioning of those certificates is what kubelet TLS bootstrapping is for" | **partial** — purpose stated, mechanism absent. Nothing else in the book defines it. Glossary entry suffices; does not reach graded text |
| **hugepages** | Named once, inside the quota compute-totals list (`hugepages-<size>`) | **partial** — glossary entry suffices |
| **Eviction API / `Eviction` object** | "this creates an `Eviction` object, which causes the API server to terminate the Pod"; "like performing a policy-controlled `DELETE` operation on the Pod" | **defined, thinly.** Entry recommended rather than required — the definition is real, it just sits in a 🔭 Closer Look |
| **bearer token** | "Kubernetes automatically injects the public root certificate and a valid bearer token into the Pod when it is instantiated" | ⚑ **gap — inherited, still open.** Used as a term of art here and undefined in every prior chapter |

### Chapter 8 contribution — terms the chapter defines

| Term | Definition (verbatim from chapter) | First appearance |
|---|---|---|
| **`kubectl` grammar** | "Every `kubectl` invocation takes the form `kubectl [command] [TYPE] [NAME] [flags]`" | Chapter 8 §1 |
| **command (kubectl slot)** | "the operation you want performed on one or more resources" | Chapter 8 §1 |
| **TYPE (kubectl slot)** | "the resource type" — "case-insensitive, and you may use the singular, plural, or abbreviated form" | Chapter 8 §1 |
| **NAME (kubectl slot)** | "the name of the specific resource. If the name is omitted, details for all resources are displayed" — "Resource *names* are case-sensitive" | Chapter 8 §1 |
| **flags (kubectl slot)** | "optional. Flags you specify on the command line override default values and any corresponding environment variables" | Chapter 8 §1 |
| **`kubectl explain`** | "Get documentation of various resources" — "the only verb in the table that answers a question about *the resource type* rather than a question about *your cluster*" | Chapter 8 §1 |
| **kubeconfig** | "`kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag" | Chapter 8 §1 |
| **in-cluster authentication** | "checking for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables, and for the existence of a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are found, in-cluster authentication is assumed" | Chapter 8 §1 |
| **ServiceAccount namespace default** | "when `kubectl` runs in a cluster it acts against the namespace of the ServiceAccount, unless `--namespace` is given" | Chapter 8 §1 |
| **transport security (API server)** | "the API server listens on port 6443 on the first non-localhost network interface, protected by TLS" | Chapter 8 §2 |
| **authentication (gate one)** | "Authentication establishes the identity behind the request." "the input to the authentication step is the entire HTTP request, though it typically examines the headers and/or client certificate" | Chapter 8 §2 |
| **401 (authentication failure)** | "if the request cannot be authenticated, it is rejected with HTTP status code 401" | Chapter 8 §2 |
| **no `User` object** | "while Kubernetes uses usernames for access control decisions and in request logging, it does not have a `User` object" | Chapter 8 §2 |
| **authorization (gate two)** | "A request must include the username of the requester, the requested action, and the object affected by the action" | Chapter 8 §2 |
| **authorization quorum rule** | "if any module authorizes the request, then the request can proceed; if all of the modules deny the request, then the request is denied, with HTTP status code 403" | Chapter 8 §2 |
| **authorization modules** | "Kubernetes supports multiple authorization modules, such as ABAC mode, RBAC Mode, and Webhook mode" | Chapter 8 §2 |
| **admission control (gate three)** | "Admission control modules are software modules that can modify or reject requests" — "unlike the first two gates they can access the contents of the object that is being created or modified" | Chapter 8 §2 |
| **admission rejection rule** | "unlike authentication and authorization modules, if any admission controller module rejects, the request is immediately rejected" | Chapter 8 §2 |
| **admission defaulting** | "admission controllers can also set complex defaults for fields" | Chapter 8 §2 |
| **admission write path** | "once a request passes all admission controllers, it is validated using the validation routines for the corresponding API object, and then written to the object store" | Chapter 8 §2 |
| **reads bypass admission** | "Admission controllers act on requests that create, modify, delete, or connect to (proxy) an object. They do not act on requests that merely read objects" | Chapter 8 §2 |
| **dynamic admission control** | "the cluster calls out to a webhook *you* supplied. Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend" | Chapter 8 §2 |
| **auditing** | "a security-relevant, chronological set of records documenting the sequence of actions in a cluster" — answering "what happened, when it happened, who initiated it, on what it happened, where it was observed, from where it was initiated, and to where it was going" | Chapter 8 §2 |
| **audit event** | "audit records begin their lifecycle inside the kube-apiserver component, and each request on each stage of its execution generates an audit event" | Chapter 8 §2 |
| **hub-and-spoke API pattern** | "All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services" | Chapter 8 §2 |
| **ResourceQuota** | "provides constraints that limit **aggregate resource consumption per namespace**" | Chapter 8 §3 |
| **quota violation** | "If creating or updating a resource violates a quota constraint, the control plane rejects that request with HTTP status code `403 Forbidden`" | Chapter 8 §3 |
| **quota declaration rule** | "If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients must specify either `requests` or `limits` for that resource, for every new Pod you submit. If you don't, the control plane may reject admission for that Pod" | Chapter 8 §3 |
| **`count/<resource>`** | object-count quota syntax — "`count/<resource>` for core API group resources and `count/<resource>.<group>` otherwise" | Chapter 8 §3 |
| **quota / capacity independence** | "ResourceQuotas are independent of the cluster capacity, so if you add nodes to your cluster, this does not automatically give each namespace the ability to consume more resources" | Chapter 8 §3 |
| **LimitRange** | "a policy to constrain the resource allocations — limits and requests — that you can specify for **each applicable object kind**, such as Pod or PersistentVolumeClaim, in a namespace" | Chapter 8 §3 |
| **LimitRange timing** | "LimitRange validations occur only at Pod admission stage, not on running Pods" | Chapter 8 §3 |
| **LimitRange non-determinism** | "if two or more LimitRange objects exist in the namespace, it is not deterministic which default value will be applied" | Chapter 8 §3 |
| **node self-registration** | "the kubelet on a node self-registers to the control plane, which is the default, or you (or another human user) manually add a Node object" | Chapter 8 §4 |
| **Node object naming** | "The name of a Node object must be a valid DNS subdomain name and must be unique" | Chapter 8 §4 |
| **`kubectl cordon`** | "Mark node as unschedulable" — "prevents the scheduler from placing new Pods onto that Node, but does not affect existing Pods on the Node; this is useful as a preparatory step before a node reboot or other maintenance" | Chapter 8 §1/§4 |
| **`kubectl drain`** | "safely evict all of your Pods from a node before you perform maintenance on it, such as a kernel upgrade or hardware maintenance" | Chapter 8 §4 |
| **`kubectl uncordon`** | "you need to run `kubectl uncordon <node name>` afterwards to tell Kubernetes that it can resume scheduling new Pods onto the node" | Chapter 8 §4 |
| **`Ready`** | "The node is healthy and ready to accept Pods. **False** if the node is not healthy and is not accepting Pods. **Unknown** if the node controller has not heard from the node in the last `node-monitor-grace-period`" | Chapter 8 §4 |
| **`DiskPressure` · `MemoryPressure` · `PIDPressure` · `NetworkUnavailable`** | disk capacity low · node memory low · too many processes on the node · "the network for the node is not correctly configured" | Chapter 8 §4 |
| **`node-monitor-grace-period`** | the interval after which an unheard-from node's `Ready` becomes `Unknown`; "default is 50 seconds" — the chapter treats the parameter name as durable and the number as configuration | Chapter 8 §4 |
| **`SchedulingDisabled`** | "not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec" | Chapter 8 §4 |
| **node heartbeat** | "two forms of heartbeat: updates to the `.status` of a Node, and Lease objects within the `kube-node-lease` namespace, with each Node having an associated Lease object" | Chapter 8 §4 |
| **node controller** | "manages several aspects of nodes: assigning a CIDR block to the node when it is registered; keeping its internal list of nodes up to date with the cloud provider's list of available machines; and monitoring the nodes' health" | Chapter 8 §4 |
| **`Capacity`** | "the total amount of resources that a Node has" | Chapter 8 §4 |
| **`Allocatable`** | "the amount of resources on a Node that is available to be consumed by normal Pods" — "The scheduler treats 'Allocatable' as the available capacity for Pods, and does not over-subscribe it" | Chapter 8 §4 |
| **`kubeReserved` / `systemReserved`** | "resource reservation for Kubernetes system daemons like the kubelet and the container runtime" / "reservation for OS system daemons such as `sshd` and `udev`" | Chapter 8 §4 |
| **kubeadm** | "the officially supported tool for creating clusters, used to install the control plane and join nodes" | Chapter 8 §5 |
| **minikube** | "runs a single- or multi-node local Kubernetes cluster" | Chapter 8 §5 |
| **kind** | "Kubernetes IN Docker — which runs local clusters using Docker containers as nodes" | Chapter 8 §5 |
| **k3s** | "a lightweight distribution" | Chapter 8 §5 |
| **semantic versioning (`x.y.z`)** | "x is the major version, y is the minor version, and z is the patch version, following Semantic Versioning terminology" | Chapter 8 §6 |
| **supported releases** | "The Kubernetes project maintains release branches for the most recent **three** minor releases" | Chapter 8 §6 |
| **patch-support window** | "Kubernetes 1.19 and newer receive approximately one year of patch support; 1.18 and older received approximately nine months" | Chapter 8 §6 |
| **release cadence** | "**three minor releases per year**, approximately every fifteen weeks… patch releases are cut monthly from the supported branches" | Chapter 8 §6 |
| **version skew (generating rule)** | "Nothing in the cluster may be newer than the API server it talks to" — kubelet ≤3 minors older; `kubectl` ±1 minor; controller-manager/scheduler/cloud-controller-manager ≤1 minor older; HA API servers within 1 minor **of each other** | Chapter 8 §6 |
| **upgrade order** | "the API server must be upgraded first; everything else follows behind it, within its permitted window" — labelled in-chapter as a derivation, not a documented rule | Chapter 8 §6 |
| **etcd snapshot** | "`etcdctl snapshot save backup.db`, or a volume snapshot of etcd's storage" | Chapter 8 §7 |
| **etcd restore** | "`etcdutl snapshot restore`, which operates directly on the etcd data files; after a restore, the control plane components are restarted against the restored data directory" | Chapter 8 §7 |
| **etcd access = root** | "Access to etcd is equivalent to root permission in the cluster, so ideally only the API server should have access to it" | Chapter 8 §7 |
| **snapshot handling** | "The snapshot file contains all the Kubernetes state and critical information; keep it encrypted and store it outside the control plane nodes" | Chapter 8 §7 |

---

## Concept shards added/updated

### Created — 18, each named for a Chapter 8 `kb_tags` slug so it resolves

| Shard | Slug is a `kb_tags` entry | Note |
|---|---|---|
| `concepts/verb-resource-grammar.md` | ✓ | four slots, the case asymmetry, the verb table |
| `concepts/kubeconfig.md` | ✓ | location + precedence; carries the **`context` gap** |
| `concepts/in-cluster-authentication.md` | ✓ | the three checks and the two surprises |
| `concepts/api-access-gates.md` | ✓ | the three-gate sequence and the two quorum rules |
| `concepts/admission-control.md` | ✓ | the mutation power; the instances the book already used |
| `concepts/auditing.md` | ✓ | **thin — under the 200-word bar.** Created anyway: `auditing` is a tagged concept with no other owner, and Ch 13/17 will want it |
| `concepts/resource-quota.md` | ✓ | replaces the prior manifest's unresolvable `resource-quota-and-limitrange.md` |
| `concepts/limit-range.md` | ✓ | ditto |
| `concepts/namespaced-vs-cluster-scoped.md` | ✓ | the §3 hinge — a B3 cross-cutting theme, and Ch 12's RBAC derivation depends on it |
| `concepts/node-registration.md` | ✓ | **de facto new owner** — B7 assigns this to Ch 3 §3, which does not teach it |
| `concepts/cordon.md` | ✓ | the three-command sequence and the chapter's costliest trap |
| `concepts/drain.md` | ✓ | Eviction API; the DaemonSet exception |
| `concepts/node-conditions.md` | ✓ | **ch-09's Stage-14 append targets this file — it must exist first** |
| `concepts/node-controller.md` | ✓ | three jobs; loop-shaped, **no ordinal** |
| `concepts/node-heartbeats.md` | ✓ | two forms; settles Ch 4 §3's IOU |
| `concepts/version-skew.md` | ✓ | one rule, five rows, two exceptions |
| `concepts/release-cadence.md` | ✓ | three/three/one-year, and why they agree |
| `concepts/etcd-backup.md` | ✓ | mechanics + the two-failure-modes argument |

### Updated — 11 appends to shards owned by earlier chapters

All are **appends**. Three of them (`control-loop`, `taint`, `resource-request`) carry prior decisions a naïve overwrite would delete.

| Shard | Owner | What Chapter 8 adds |
|---|---|---|
| `concepts/control-loop.md` | ch-03 | ⚑ **the ordinal conflict, extended.** No count recorded |
| `concepts/namespace.md` | ch-04 | quota named as *the* division mechanism; "you can quota a team, not a machine" |
| `concepts/cluster-scoped-resource.md` | ch-04 | Nodes as the worked consequence |
| `concepts/spec.md` | ch-04 | `cordon` writes `.spec.unschedulable` — the chapter's strongest use of the spec/status rule |
| `concepts/status.md` | ch-04 | the same boundary from the other side; `SchedulingDisabled` is in neither |
| `concepts/api-server-hub.md` | ch-03 | the gates and the audit log are things the door *does*; only the API server should reach etcd |
| `concepts/serviceaccount.md` | ch-05 | the SA as an *identity at gate one*, and the injected token as the file §1 looks for |
| `concepts/taint.md` | ch-07 | the `unschedulable` taint's relationship to the spec field, left where the docs leave it |
| `concepts/built-in-node-condition-taints.md` | ch-07 | the DaemonSet toleration, ⚑ with an attribution correction |
| `concepts/resource-request.md` | ch-05/07 | **Capacity vs Allocatable** — pays off Ch 7 §2's explicit IOU |
| `concepts/cri.md` | ch-02 | the CRI boundary's first *operational* consequence: kubeadm does not install a runtime |

### ⚑ Tagged concepts left without a shard — 31 of 58

These resolve to nothing when a later chapter tags them. Most are fine (they are single facts, better served by the glossary), but four are worth the author's attention because a later chapter is likely to tag them and get silence: **`mutating-admission`** and **`validating-admission`** (see the glossary gap — Ch 17 §4 will want these), **`uncordon`** (folded into `cordon.md`), and **`disaster-recovery`** (folded into `etcd-backup.md`). A three-line pointer stub fixes each; I have not emitted eighteen stub files to make the count look better.

---

## Voice-exemplar candidates nominated

Not written to `voice-exemplars.md`. The author ratifies exemplars explicitly (Rule 1).

| Function | Excerpt | Recommendation |
|---|---|---|
| **claim-narrowing / honest retraction** | §8: *"One honest correction, because the claim as stated is slightly too neat and you would notice… §5 and §6 are not consequences of the architecture… These have to be learned. That is exactly why §6 flagged them as memorization and gave you a derivation for three of the five rows anyway. The parts that can be reasoned about should be reasoned about, and the residue should be admitted as residue."* | **Strongest candidate in the chapter.** The book already runs this move (Ch 4 §1, Ch 4 §6, Ch 3), but this is the first instance where a chapter retracts *its own thesis* under a heading and survives it. No existing exemplar covers the function. **Nominate** |
| **stakes without fear-mongering** | §7: *"an unencrypted etcd snapshot sitting on a control-plane node is simultaneously your only disaster recovery and a complete compromise of the cluster, waiting for someone to copy it. Not a credential* for *the cluster. Root* in *the cluster, in one file, at rest."* | **Strong.** Two sourced sentences placed side by side; the alarm is entirely carried by the juxtaposition, with no invented statistic. Exactly the skill Part 14 line between real consequence and fabricated urgency. **Nominate** |
| **Logbook Entry (sidebar)** | §5: *"A control plane is not expensive. Three modest machines will run one. What is expensive is the* calendar *attached to it… Crews that self-host successfully are almost always crews that budgeted for that calendar deliberately… Crews that regret it are usually crews that priced the machines and not the Thursdays."* | **Strong**, and likely the book's first Logbook Entry nomination. Practitioner-facing wry register, subject dignity intact, and it closes on a question rather than a verdict (*"whose watch does this stand on"*). **Nominate** |
| **Extended Analogy (sidebar)** | §2: the harbour — pilot boat (identity), harbourmaster (standing, opens no crates), customs officer (opens crates, and *"may say the vessel can dock provided a particular container stays sealed"*) | **Strong on craft, ⚑ blocked on spelling.** The three-office structure earns the third gate's separateness better than the prose does. But it spells the role **`harbourmaster` ×3** where **Chapter 4 coined `harbormaster` ×2** — the analogy's central character, renamed against the chapter that introduced it, three sections from the brand-locked **🏆 Safe Harbor**. **Do not promote until the spelling is reconciled**; an exemplar is copied by later chapters |
| **perishability disclosure** | §6: *"The rules above are stable. The specific releases are not… Learn the rule and treat the numbers as an illustration of it. Nothing in this book's practice questions turns on which minor version is current, and nothing in the exam should either."* | **Moderate–strong.** A reusable pattern for every dated fact in a cert guide. Nominate if the author wants a "dated-fact handling" exemplar; it is a genre convention rather than a voice signature |
| **answer-key register** | Bearings #2 A2: *"If you got this wrong, you got it wrong for a sensible reason. 'Take a node out of service' reads as one action, and in most operational vocabularies it* is *one action… The split is a feature. It is also a trap."* | **Moderate.** Skill Part 10B's "normalize struggle" done without condescension. Nominate only if the exemplar file is thin on answer-key voice |

### ⚑ Spelling note attached to the nominations

Independent of the exemplar question: **Chapter 8 is the only chapter in the book carrying lint-flagged British spellings.** A grep of all eleven shipped chapters for the `structural_lint` British-spelling pattern returns **15 occurrences, all in Chapter 8; zero elsewhere.** The revision cuts that to **6** in the finalized text — `behaviour` ×3, `artefact` ×2, `defence` ×1.

The `harbour` family is a separate problem the linter **cannot** catch, because `harbour` is not in the pattern. Six occurrences in this chapter, and it has already spread: `harbour`/`harbours` now appear in Chapters 7, 9 and 10, and `harbourmaster` in Chapter 10. Chapter 4's `harbormaster` is now the minority spelling in its own book. Two options, and the author should pick one rather than let it drift further: add `harbour(s|master)?` to the lint pattern and sweep to US spelling, or ratify the British form and sweep Chapter 4 — noting that the second option leaves `🏆 Safe Harbor` spelled the other way, permanently, because that marker is brand-locked.

---

## Objective coverage log

`D1.2` is unclaimed by any prior manifest; this is first and only coverage.

## Retrieval-practice ledger

**8 tagged items / 33 graded items (15 Bearings + 18 Practice) = 24.2%** — inside B3's 20–25% band for Chapter 8, and up from draft-v1's 18.2%.

**✅ B3's spacing floor is met, which the integration report did not check.** `retrieval-architecture.md` sets a binding rule: *"from Ch 8 on, at least one item must come from ≥4 chapters back."* Chapter 8 has **five** such items — ch 2 (six back), ch 3 (five back), and ch 4 ×3 (exactly four back). Comfortable pass.

**✅ Both of B3's named forward anchors for this chapter's decay-prone material are in place.** B3 flagged §6 as *"the densest pure-recall material in the book, taught at the 40% mark and otherwise never revisited before exam day,"* and scheduled version skew into Ch 13 and release cadence into Ch 17. The chapter carries both cross-bearings (`Ch 13 §6`, `Ch 17 §8`), and Bearings #3 A3 tells the reader outright that the Ch 17 pass is when the numbers get their second look. Logged as forward obligations so a later chapter cannot quietly drop them.
```

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

# ═══ CHAPTER 8 — Standing the Watch (Administration, D1.2) ═══

*Contributed by ch-08 Stage 14, 2026-08-30. 52 terms: 45 defined verbatim from the chapter, 7 recorded as gaps. Definitions are the chapter's own wording — do not reword when merging alphabets.*

## Gaps — do not invent wording for these

**context (kubeconfig context)** — ⚑ **UNDEFINED IN CHAPTER.** B7 (`term-ownership.md:269`) assigns *Context (kubeconfig context)* to Ch 8 §1 as owner and first appearance. The chapter describes the concept without naming it ("the answer to the two-server problem: which one you are currently talking to") and then uses the word in graded text (Bearings #1 A2, "the namespace of the current context"). **Highest-priority glossary gap in this chapter.** (Chapter 8 §1)

**mutating admission webhook / validating admission webhook** — ⚑ **UNDEFINED BOOK-WIDE.** Parent concept only: dynamic admission control is where "the cluster calls out to a webhook *you* supplied," via "synchronous HTTP requests to a remote service, a webhook backend." B7 claims first appearance at Ch 6 §8; shipped Ch 6 has zero occurrences of "webhook." Ch 17 §4 collects admission webhooks among the extension points without defining them. (Chapter 8 §2)

**CIDR** — ⚑ **NAMED, NEVER EXPANDED.** "assigning a CIDR block to the node when it is registered." First reader-facing use in the book; B7's acronym register wrongly assigns it to Ch 10 §6. (Chapter 8 §4)

**kubelet TLS bootstrapping** — "Automating the provisioning of those certificates is what kubelet TLS bootstrapping is for." Purpose stated; mechanism undefined here and everywhere. (Chapter 8 §2)

**hugepages** — named only as `hugepages-<size>` in the quota compute-totals list. (Chapter 8 §3)

**bearer token** — ⚑ used as a term of art, undefined: "Kubernetes automatically injects the public root certificate and a valid bearer token into the Pod when it is instantiated." (Chapter 8 §2)

**managed vs self-hosted duty split** — ⚑ **permanently partial absent a new source.** The chapter asserts only the two duties the architecture decides (upgrade timing, etcd backup). Research gap G-8G: kubernetes.io does not document commercial providers' responsibility models, so no fetch from that doc tree closes it. Do not expand into a five-item list. (Chapter 8 §5)

## A

**Allocatable** — "the amount of resources on a Node that is available to be consumed by normal Pods." The scheduler "treats 'Allocatable' as the available capacity for Pods, and does not over-subscribe it." Contrast [[Capacity]]. (Chapter 8 §4)

**admission control** — the third gate. "Admission control modules are software modules that can modify or reject requests," and unlike the first two gates "they can access the contents of the object that is being created or modified." (Chapter 8 §2)

**admission rejection rule** — "unlike authentication and authorization modules, if any admission controller module rejects, the request is immediately rejected." Any-module-*rejects*, against authorization's any-module-*approves*. (Chapter 8 §2)

**admission defaulting** — "admission controllers can also set complex defaults for fields." The property that makes admission a different kind of check rather than a third variation on "no." (Chapter 8 §2)

**auditing** — "a security-relevant, chronological set of records documenting the sequence of actions in a cluster," which "allows cluster administrators to answer what happened, when it happened, who initiated it, on what it happened, where it was observed, from where it was initiated, and to where it was going." (Chapter 8 §2)

**audit event** — "audit records begin their lifecycle inside the kube-apiserver component, and each request on each stage of its execution generates an audit event." The logbook is kept by the door, not by an observer watching it. (Chapter 8 §2)

**authentication** — gate one. Establishes the identity behind the request; "the input to the authentication step is the entire HTTP request, though it typically examines the headers and/or client certificate." Failure returns **401**. (Chapter 8 §2)

**authorization** — gate two. "A request must include the username of the requester, the requested action, and the object affected by the action." Quorum rule: "if any module authorizes the request, then the request can proceed; if all of the modules deny the request, then the request is denied, with HTTP status code 403." (Chapter 8 §2)

**authorization modules** — "Kubernetes supports multiple authorization modules, such as ABAC mode, RBAC Mode, and Webhook mode." RBAC in full is Ch 12. (Chapter 8 §2)

## C

**Capacity** — "the total amount of resources that a Node has." Not the number the scheduler does arithmetic against; see [[Allocatable]]. (Chapter 8 §4)

**cordon** (`kubectl cordon NODE`) — "Mark node as unschedulable." It "prevents the scheduler from placing new Pods onto that Node, but does not affect existing Pods on the Node; this is useful as a preparatory step before a node reboot or other maintenance." **A cordoned node is not an empty node.** (Chapter 8 §1, §4)

**`count/<resource>`** — object-count quota syntax: `count/<resource>` for core API group resources, `count/<resource>.<group>` otherwise. Countable resources include `count/pods`, `count/services`, `count/secrets`, `count/configmaps`, `count/deployments.apps`. (Chapter 8 §3)

## D

**DiskPressure** — node condition, `True` when "pressure exists on the disk size — that is, if the disk capacity is low." (Chapter 8 §4)

**drain** (`kubectl drain`) — used "to safely evict all of your Pods from a node before you perform maintenance on it, such as a kernel upgrade or hardware maintenance." Works through the Eviction API, not a private channel. (Chapter 8 §4)

**dynamic admission control** — admission enforced by a webhook the operator supplied: "Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend," which "adds a potential point of failure." (Chapter 8 §2)

## E

**etcd access = root** — "Access to etcd is equivalent to root permission in the cluster, so ideally only the API server should have access to it." (Chapter 8 §7)

**etcd restore** — "`etcdutl snapshot restore`, which operates directly on the etcd data files; after a restore, the control plane components are restarted against the restored data directory." A maintenance event, not an in-place command. (Chapter 8 §7)

**etcd snapshot** — one of two backup routes: "a built-in snapshot, `etcdctl snapshot save backup.db`, or a volume snapshot of etcd's storage." Optional `--endpoints`, `--cacert`, `--cert`, `--key` for a TLS-protected cluster. (Chapter 8 §7)

**Eviction API / `Eviction` object** — requesting eviction "creates an `Eviction` object, which causes the API server to terminate the Pod"; doing so is "like performing a policy-controlled `DELETE` operation on the Pod." (Chapter 8 §4)

## F

**flags (kubectl slot)** — "optional. Flags you specify on the command line override default values and any corresponding environment variables." (Chapter 8 §1)

## H

**hub-and-spoke API pattern** — "All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services." This is what makes three gates on one door a *sufficient* access-control story rather than merely a present one. (Chapter 8 §2)

## I

**in-cluster authentication** — how `kubectl` detects it is running inside a Pod: "checking for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables, and for the existence of a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are found, in-cluster authentication is assumed." (Chapter 8 §1)

## K

**k3s** — "a lightweight distribution." (Chapter 8 §5)

**kind** — "Kubernetes IN Docker — which runs local clusters using Docker containers as nodes." (Chapter 8 §5)

**kubeadm** — "the officially supported tool for creating clusters, used to install the control plane and join nodes." Does **not** install a container runtime. (Chapter 8 §5)

**kubeconfig** — "`kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag." Precedence: default location < environment variable < flag. (Chapter 8 §1)

**`kubectl` grammar** — "Every `kubectl` invocation takes the form `kubectl [command] [TYPE] [NAME] [flags]`." Four slots; only the first is mandatory. (Chapter 8 §1)

**`kubectl explain`** — "Get documentation of various resources" — the only verb that answers a question about *the resource type* rather than about *your cluster*, which is why it works on types installed after this book was written. (Chapter 8 §1)

**kubeReserved** — "resource reservation for Kubernetes system daemons like the kubelet and the container runtime." (Chapter 8 §4)

## L

**LimitRange** — "a policy to constrain the resource allocations — limits and requests — that you can specify for **each applicable object kind**, such as Pod or PersistentVolumeClaim, in a namespace." Enforces min/max per Pod or Container, min/max storage per PVC, a request:limit ratio, and injects defaults. (Chapter 8 §3)

**LimitRange timing** — "LimitRange validations occur only at Pod admission stage, not on running Pods." Adding or modifying a LimitRange leaves existing Pods unchanged. (Chapter 8 §3)

**LimitRange non-determinism** — "if two or more LimitRange objects exist in the namespace, it is not deterministic which default value will be applied," and a LimitRange "does not check the consistency of the default values it applies." (Chapter 8 §3)

## M

**MemoryPressure** — node condition, `True` when "pressure exists on the node memory — that is, if the node memory is low." (Chapter 8 §4)

**minikube** — "runs a single- or multi-node local Kubernetes cluster." (Chapter 8 §5)

## N

**NAME (kubectl slot)** — "the name of the specific resource. If the name is omitted, details for all resources are displayed." **Resource names are case-sensitive.** (Chapter 8 §1)

**NetworkUnavailable** — node condition, `True` when "the network for the node is not correctly configured." (Chapter 8 §4)

**node condition** — the five entries in a Node's `conditions` field: `Ready`, `DiskPressure`, `MemoryPressure`, `PIDPressure`, `NetworkUnavailable`. Four are two-valued; `Ready` is three-valued. (Chapter 8 §4)

**node controller** — the control-plane component that "manages several aspects of nodes: assigning a CIDR block to the node when it is registered; keeping its internal list of nodes up to date with the cloud provider's list of available machines; and monitoring the nodes' health — updating the `Ready` condition to `Unknown` when a node becomes unreachable, and triggering API-initiated eviction of all the Pods from the node if it stays unreachable." (Chapter 8 §4)

**node heartbeat** — "two forms of heartbeat: updates to the `.status` of a Node, and Lease objects within the `kube-node-lease` namespace, with each Node having an associated Lease object." (Chapter 8 §4)

**`node-monitor-grace-period`** — the interval after which the node controller sets an unheard-from node's `Ready` condition to `Unknown`; "default is 50 seconds." The chapter treats the parameter name as the durable fact and the number as configuration. (Chapter 8 §4)

**Node object naming** — "must be a valid DNS subdomain name and must be unique." (Chapter 8 §4)

**node self-registration** — "the kubelet on a node self-registers to the control plane, which is the default, or you (or another human user) manually add a Node object." A kubelet joins by writing an object through the API server; it does not open a private channel. (Chapter 8 §4)

**no `User` object** — "while Kubernetes uses usernames for access control decisions and in request logging, it does not have a `User` object." Identity is a property of a request, not a record in the datastore. (Chapter 8 §2)

## P

**patch-support window** — "Kubernetes 1.19 and newer receive approximately one year of patch support; 1.18 and older received approximately nine months." (Chapter 8 §6)

**PIDPressure** — node condition, `True` when "pressure exists on the processes — that is, if there are too many processes on the node." (Chapter 8 §4)

## Q

**quota declaration rule** — "If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients must specify either `requests` or `limits` for that resource, for every new Pod you submit. If you don't, the control plane may reject admission for that Pod." A Pod that declares nothing is not a small Pod; it is an uncountable one. (Chapter 8 §3)

**quota / capacity independence** — "ResourceQuotas are independent of the cluster capacity, so if you add nodes to your cluster, this does not automatically give each namespace the ability to consume more resources." (Chapter 8 §3)

## R

**reads bypass admission** — "Admission controllers act on requests that create, modify, delete, or connect to (proxy) an object. They do not act on requests that merely read objects." (Chapter 8 §2)

**Ready** — node condition. `True`: "the node is healthy and ready to accept Pods." `False`: "the node is not healthy and is not accepting Pods." `Unknown`: "the node controller has not heard from the node in the last `node-monitor-grace-period`." `Unknown` is the control plane declining to guess, not a fourth failure mode. (Chapter 8 §4)

**release cadence** — "three minor releases per year, approximately every fifteen weeks, each following a release cycle led by a SIG Release team; patch releases are cut monthly from the supported branches." (Chapter 8 §6)

**ResourceQuota** — "provides constraints that limit **aggregate resource consumption per namespace**." Violation is rejected "with HTTP status code `403 Forbidden`." (Chapter 8 §3)

## S

**`SchedulingDisabled`** — ⚠ "not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec." A display string produced by command-line tools. (Chapter 8 §4)

**semantic versioning (`x.y.z`)** — "x is the major version, y is the minor version, and z is the patch version, following Semantic Versioning terminology." (Chapter 8 §6)

**snapshot handling** — "The snapshot file contains all the Kubernetes state and critical information; keep it encrypted and store it outside the control plane nodes." A snapshot stored only on the nodes it insures against losing is ballast, not a lifeboat. (Chapter 8 §7)

**supported releases** — "The Kubernetes project maintains release branches for the most recent **three** minor releases." Not two. (Chapter 8 §6)

**systemReserved** — "reservation for OS system daemons such as `sshd` and `udev`." (Chapter 8 §4)

## T

**transport security (API server)** — the stage before the three gates: "the API server listens on port 6443 on the first non-localhost network interface, protected by TLS." (Chapter 8 §2)

**TYPE (kubectl slot)** — "the resource type." **Case-insensitive**, and "you may use the singular, plural, or abbreviated form." Contrast NAME. (Chapter 8 §1)

## U

**uncordon** (`kubectl uncordon`) — restores scheduling. A separate step you must run: "you need to run `kubectl uncordon <node name>` afterwards to tell Kubernetes that it can resume scheduling new Pods onto the node." (Chapter 8 §4)

## V

**version skew** — the generating rule: **nothing may be newer than the API server.** kubelet: never newer, up to **three** minors older (two, for kubelets older than 1.25). kube-proxy: never newer than the API server; within three minors older or newer than its kubelet. controller-manager / scheduler / cloud-controller-manager: never newer, up to **one** minor older. `kubectl`: within **one** minor, **older or newer** — the sole exception. HA kube-apiservers: newest and oldest within one minor **of each other**. (Chapter 8 §6)

**upgrade order** — "the API server must be upgraded first; everything else follows behind it, within its permitted window." ⚑ Labelled in-chapter as a **derivation** from the skew rule, not a documented procedure. Preserve that hedge. (Chapter 8 §6)

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/verb-resource-grammar.md ===
# Concept: The four-slot `kubectl` grammar

**Home:** Chapter 8 §1 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `kubectl`, `kubectl-syntax`, `resource-type-abbreviation`

## ★ Fixed Point (verbatim — do not reword)

> One grammar, four slots — `kubectl [command] [TYPE] [NAME] [flags]`. **Resource types are case-insensitive and abbreviable. Resource names are case-sensitive.**

## The slots

- **command** — "the operation you want performed on one or more resources": `create`, `get`, `describe`, `delete`.
- **TYPE** — "the resource type." Case-insensitive; singular, plural or abbreviated all accepted.
- **NAME** — "the name of the specific resource. If the name is omitted, details for all resources are displayed." Case-sensitive.
- **flags** — optional. "Flags you specify on the command line override default values and any corresponding environment variables."

Only the first slot is mandatory. `kubectl cordon node-7` is the grammar with TYPE and flags both empty; the verb implies the type.

## The asymmetry is the examinable half

The tool is relaxed about *what kind of thing* you meant and exacting about *which one*. `kubectl get PODS web-01` works; `kubectl get pods Web-01` does not. Both symmetrical answers ("both case-insensitive," "both case-sensitive") are live distractors — the permissive one more often, because the tool's tolerance about types invites the generalization.

## `kubectl explain` is the long-payoff verb

"Get documentation of various resources" — the only verb in Chapter 8's table that answers a question about *the resource type* rather than about *your cluster*. It therefore works on types the reader has never seen, including CustomResourceDefinitions installed by tools that post-date the book.

## ⚑ Attribution correction carried from Stage 13

The chapter's verb table maps `get` and `describe` to Chapter 4. **Neither appears in Chapter 4.** `kubectl get` first appears in Ch 3, `kubectl describe` in Ch 5. B7 also records `kubectl describe` as first appearing at Ch 8 §4, which is wrong by three chapters. Fix the table cells before this shard is used to answer a "where was this taught" question.

## Related

[[kubeconfig]] · [[in-cluster-authentication]] · [[cordon]] · [[declarative-configuration]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubeconfig.md ===
# Concept: kubeconfig

**Home:** Chapter 8 §1 · **Competency:** D1.2 · **Status:** canonical, **one gap**

## What the chapter establishes

"For configuration, `kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag."

Precedence, stated flat: **default location → environment variable → flag**, with the flag winning, because the general rule is that "flags specified on the command line override default values and any corresponding environment variables."

The file answers three questions a client tool must have answered before it can do anything: **where** the cluster is, **who** you are to it, and — once there is more than one cluster — **which one** you are currently talking to.

## ⚑ GAP — `context` is used in graded text and never defined

B7 (`term-ownership.md:269`) assigns **Context (kubeconfig context)** to Ch 8 §1 as both owner and first appearance. The chapter describes the concept without naming it — "the answer to the two-server problem: which one you are currently talking to" — and then uses the word in an answer key (Bearings #1 A2: "looked in the namespace of the current context").

B7's own rule forbids a term reaching graded material without a definition. **Do not close this in the glossary alone.** Stage 13's fix [G0] adds one sentence to §1 after the precedence paragraph; that is the correct repair, and it costs nothing because the concept is already in the prose.

## Related

[[verb-resource-grammar]] · [[in-cluster-authentication]] · [[namespace]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/in-cluster-authentication.md ===
# Concept: In-cluster authentication (`kubectl` inside a Pod)

**Home:** Chapter 8 §1 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `serviceaccount-token-file`, `namespace-override`

## The three checks

"By default `kubectl` first determines whether it is running within a Pod, and thus inside a cluster. It starts by checking for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables, and for the existence of a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are found, in-cluster authentication is assumed."

## The two surprises, both examinable

1. **It is not you.** The invocation authenticates as the Pod's ServiceAccount, using the bearer token Kubernetes injected at instantiation — not the kubeconfig on anyone's laptop.
2. **It does not default to `default`.** "When `kubectl` runs in a cluster it acts against the namespace of the ServiceAccount, unless `--namespace` is given."

The practical signature is an empty `kubectl get pods` that the operator was certain should have returned something: right command, right cluster, wrong namespace, different identity.

## Why it belongs to the gate model

The injected token is the *same file* that gate one reads. §1 finds it and infers "I am inside"; §2 reads it and answers "who are you." One artifact, two readers — which is why this shard sits next to [[api-access-gates]] rather than being filed as a `kubectl` quirk.

## Related

[[kubeconfig]] · [[api-access-gates]] · [[serviceaccount]] · [[namespace]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-access-gates.md ===
# Concept: The three gates (and a logbook)

**Home:** Chapter 8 §2 · **Competency:** D1.2 · **Status:** canonical
**Depth here:** the chapter's spine, and the derivation Ch 12 depends on.

## ★ Fixed Point (verbatim — do not reword)

> Authentication, then authorization, then admission. Authentication asks **who**. Authorization asks **may you**. Admission asks **should this, exactly as written, be allowed to happen** — and it is the only one of the three that can change your request instead of refusing it.

These are stages of **one request path**, not three parallel checks: "When a request reaches the API, it goes through several stages." A fourth stage precedes all three — transport security, in which "the API server listens on port 6443 on the first non-localhost network interface, protected by TLS."

## Gate one — authentication

Establishes identity. "The input to the authentication step is the entire HTTP request, though it typically examines the headers and/or client certificate." Failure is **401**. Two facts worth carrying: Kubernetes "does not have a `User` object" — identity is a property of a request, not a stored record — and the cluster's two existing identities arrive here by different routes (kubelets by client certificate, provisioned or bootstrapped; Pods by injected ServiceAccount bearer token).

## Gate two — authorization

Decides whether *this identity* may perform *this action* on *this object*. "A request must include the username of the requester, the requested action, and the object affected by the action." Failure is **403**.

**Quorum rule: any module approves.** "If any module authorizes the request, then the request can proceed; if all of the modules deny the request, then the request is denied."

## Gate three — admission

See [[admission-control]]. **Quorum rule: any module rejects.** The contrast with gate two is the sharpest available proof that authorization and admission are not two names for one check: one gate is a vote a single supporter can win, the next is a veto any participant can exercise.

## The logbook

Auditing sits in the same cluster-administration list, at the same level. It "provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster," answering "what happened, when it happened, who initiated it, on what it happened, where it was observed, from where it was initiated, and to where it was going."

And it is kept *by* the door, not by an observer watching it: "audit records begin their lifecycle inside the kube-apiserver component, and each request on each stage of its execution generates an audit event."

## Why three gates on one door is a *complete* story

"All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services."

This is the load-bearing sentence. Three gates on one door would be an incomplete access-control model if there were other doors. Chapter 3's single-door architecture is what makes the three-gate model **sufficient** rather than merely present.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 12 §3 | RBAC as *one authorizer among several* at gate two — not as "the permissions system" |
| Ch 12 §6 | Pod Security Admission as **an instance of gate three**, not a new kind of thing |
| Ch 17 §4 | Collects authentication, authorization and dynamic admission webhooks as the API-access extension points. ⚑ Depends on the mutating/validating vocabulary that no chapter currently defines |

## Related

[[admission-control]] · [[auditing]] · [[api-server-hub]] · [[in-cluster-authentication]] · [[resource-quota]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/admission-control.md ===
# Concept: Admission control

**Home:** Chapter 8 §2 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `admission-controller`, `dynamic-admission-control`

## The definition, and the property that matters

"Admission control modules are software modules that can modify or reject requests." Unlike the first two gates, "they can access the contents of the object that is being created or modified."

They sit immediately before persistence: "once a request passes all admission controllers, it is validated using the validation routines for the corresponding API object, and then written to the object store."

**The distinguishing power:** authentication and authorization answer yes or no. Admission may answer yes, no, or *yes — but not as you wrote it*, because "admission controllers can also set complex defaults for fields."

**The rejection rule:** "unlike authentication and authorization modules, if any admission controller module rejects, the request is immediately rejected."

**Reads are exempt:** admission controllers "act on requests that create, modify, delete, or connect to (proxy) an object. They do not act on requests that merely read objects." The whole gate is invisible to `kubectl get`.

## Four instances the book has already used

The pedagogical value of this shard is that admission is never introduced as an abstraction — the reader has met it four times before it is named:

| Controller | Where | What it does |
|---|---|---|
| **NodeRestriction** | Ch 7 §3 | "limits the Node and Pod objects a kubelet can modify" — why `node-restriction.kubernetes.io/` labels cannot be forged by the node they describe |
| **ResourceQuota** | Ch 8 §3 | "observes the incoming request and ensures that it does not violate any of the constraints enumerated in the ResourceQuota object" |
| **LimitRanger** | Ch 8 §3 | the same, for LimitRange constraints — and the source of injected defaults |
| **Pod Security Admission** | Ch 12 §6 | enforces the Pod Security Standards |

When Chapter 12 arrives, PSA is not new machinery. It is one instance of this gate.

## Dynamic admission control

"Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend," which "adds a potential point of failure." Operationally: once a validating webhook is installed, the webhook being down is a thing that can stop the cluster accepting requests.

## ⚑ GAP — the mutating/validating split has no owner

Curriculum-alignment deliberately excluded the phase split from Chapter 8 (the outline never asked for it; Ch 12 does not need it). That call stands. But B7 assigns the pair a first appearance at **Ch 6 §8**, and shipped Chapter 6 contains **zero** occurrences of "webhook" — so the terms are now unowned book-wide, and **Ch 17 §4 collects admission webhooks among the extension points without defining them.** Either add two sentences here (this shard's Closer Look is the natural home, and it reinforces the chapter's own thesis — a mutating webhook is the third gate's rewrite power made configurable) or accept that Ch 17 collects an undefined term.

## Related

[[api-access-gates]] · [[resource-quota]] · [[limit-range]] · [[built-in-node-condition-taints]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/auditing.md ===
# Concept: Auditing

**Home:** Chapter 8 §2 · **Competency:** D1.2 · **Status:** canonical, **thin**

⚑ **Below the 200-word depth bar.** Created anyway because `auditing` is a tagged concept with no other owner in the book, and because Ch 13 (troubleshooting) and Ch 17 (governance) are both likely to reach for it.

## What the chapter establishes

Auditing appears in the cluster-administration list of things that secure a cluster, alongside — not beneath — the three access-control stages.

Kubernetes auditing "provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster." It "allows cluster administrators to answer what happened, when it happened, who initiated it, on what it happened, where it was observed, from where it was initiated, and to where it was going."

**Where it lives is the pedagogically load-bearing detail:** "audit records begin their lifecycle inside the kube-apiserver component, and each request on each stage of its execution generates an audit event."

The logbook is not a separate observer watching the door. It is kept *by* the door — which is the single-door architecture stated a fourth time, and the reason the chapter can treat "who did this" as an answerable question at all.

## Not covered

Audit policy, audit backends, log/webhook sinks, and the stage-level event granularity are all out of scope at associate tier and absent from the chapter. Do not infer them into this shard.

## Related

[[api-access-gates]] · [[api-server-hub]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-quota.md ===
# Concept: ResourceQuota

**Home:** Chapter 8 §3 · **Competency:** D1.2 · **Status:** canonical

> **Filename note:** this replaces the prior manifest's `resource-quota-and-limitrange.md`, which was not a `kb_tags` slug and would never have been loaded by `context_packer`.

## ★ Fixed Point (verbatim — do not reword)

> **ResourceQuota counts the namespace. LimitRange constrains the object.** One is a ceiling on a team; the other is a rule about a manifest.

## Definition

"When several users or teams share a cluster with a fixed number of nodes, there is a concern that one team could use more than its fair share of resources." A ResourceQuota "provides constraints that limit **aggregate resource consumption per namespace**."

This is Chapter 4's outline sentence — namespaces divide cluster resources between users *via resource quota* — stated at full strength.

Violation: "If creating or updating a resource violates a quota constraint, the control plane rejects that request with HTTP status code `403 Forbidden`."

## What it can count

- **Compute totals** — `requests.cpu`, `requests.memory`, `limits.cpu`, `limits.memory`, `hugepages-<size>`; `cpu` and `memory` alias the request forms.
- **Storage** — `requests.storage`, `persistentvolumeclaims`, optionally per StorageClass.
- **Object counts** — `count/<resource>` for core group resources, `count/<resource>.<group>` otherwise.

## The consequence worth more than the roster

> **"If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients must specify either `requests` or `limits` for that resource, for every new Pod you submit. If you don't, the control plane may reject admission for that Pod."**

Teach this as a derivation, not a rule: a quota is a ceiling on a total, a total can only be computed if every contributor declares its share, and a Pod that declares nothing is not a *small* Pod — it is an **uncountable** one.

## What a quota is not

"ResourceQuotas are independent of the cluster capacity, so if you add nodes to your cluster, this does not automatically give each namespace the ability to consume more resources."

And it is enforced at admission — ResourceQuota "is an admission controller that observes the incoming request." Not a separate enforcement engine. A quota is **a declaration that changes what other declarations are permitted to say.**

## Why it ships with a LimitRange

The pairing is sourced, not intuited: a quota'd namespace *forces* declaration, and "you can use a LimitRange to automatically set a default request for these resources." The quota sets the ceiling and makes declaring compulsory; the LimitRange makes sure a developer who forgets still produces a countable Pod.

## Related

[[limit-range]] · [[namespaced-vs-cluster-scoped]] · [[admission-control]] · [[namespace]] · [[resource-request]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/limit-range.md ===
# Concept: LimitRange

**Home:** Chapter 8 §3 · **Competency:** D1.2 · **Status:** canonical

## Definition

"A LimitRange is a policy to constrain the resource allocations — limits and requests — that you can specify for **each applicable object kind**, such as Pod or PersistentVolumeClaim, in a namespace."

Four things it provides:

1. minimum and maximum compute resource usage per Pod or Container in a namespace;
2. minimum and maximum storage request per PersistentVolumeClaim;
3. a ratio between request and limit for a resource;
4. **default request/limit values, automatically injected into Containers at runtime.**

## Order of operations

The LimitRange admission controller first "applies default request and limit values for all Pods (and their containers) that do not set compute resource requirements," then "tracks usage to ensure it does not exceed the resource minimum, maximum and ratio defined in any LimitRange present in the namespace." Violation returns `403 Forbidden` "plus a message explaining the constraint that has been violated."

## Timing — the mutate-versus-reject distinction, one gate later

"LimitRange validations occur only at Pod admission stage, not on running Pods." Add or modify a LimitRange and the Pods already in the namespace continue unchanged.

## The two aggravations

- "A LimitRange does not check the consistency of the default values it applies."
- "If two or more LimitRange objects exist in the namespace, it is not deterministic which default value will be applied."

Practical consequence: **the Pod you get is not the Pod you wrote**, and `kubectl get pod <name> -o yaml` is where you find out.

## The discrimination, made structural

Two questions settle it without memorizing definitions:

- **What is being counted?** The quota counts the namespace's aggregate. The LimitRange counts one object's numbers.
- **What happens to a manifest that says nothing about resources?** Under a quota, the control plane may reject it. Under a LimitRange, the admission controller fills it in.

## Downstream

A defaulted request is a real field on a real object, used exactly as if the author had written it — so a Pod that previously declared nothing now **books capacity against Allocatable** and may fit on fewer nodes than its manifest suggested. See [[resource-request]].

## Related

[[resource-quota]] · [[admission-control]] · [[resource-request]] · [[namespace]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespaced-vs-cluster-scoped.md ===
# Concept: The namespaced / cluster-scoped hinge

**Home:** Chapter 4 §3 (boundary) · **Operational payoff:** Chapter 8 §3 · **Status:** canonical
**B3 cross-cutting theme #2.** One of the nine themes the retrieval architecture runs the length of the book.

## The rule

"Namespace-based scoping is applicable only for namespaced objects — Deployments, Services and so on — and not for cluster-wide objects such as StorageClass, Nodes and PersistentVolumes."

## Chapter 8's contribution: the boundary acquires a consequence

Chapter 4 established the boundary as a fact about where names live. Chapter 8 §3 turns it into an operational limit, in one line worth saying out loud:

> **You can quota a team. You cannot quota a machine.**

Every resource a ResourceQuota can count is a namespaced one. A Node is not in a namespace, so no ResourceQuota reaches it — which means "stop people using too much" has two halves sitting on opposite sides of a boundary the reader already knows, and only one of them is solvable with a quota.

The chapter places this immediately before §4 deliberately: the reader meets the limit and then spends a section on the objects it excludes.

## Downstream obligation — this is why Ch 12 is cheap

**Ch 12 §3 derives the RBAC four-way matrix (Role / ClusterRole × RoleBinding / ClusterRoleBinding) from this boundary rather than asking the reader to memorize four combinations.** That derivation only works if the hinge is retrievable by then. Chapter 8 retrieves it three times — §3's closing, Bearings #1 Q5, and Practice Q6 — which is the retrieval schedule that makes Chapter 12's saving available.

## Related

[[namespace]] · [[cluster-scoped-resource]] · [[resource-quota]] · [[node-registration]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-registration.md ===
# Concept: Node registration

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical
**Sibling tag served:** `node-self-registration`

> ⚑ **Ownership correction.** B7 records this term as "Defined by Ch 3 §3." **Shipped Chapter 3 does not teach it** — `register`/`registration` appears there only as a distractor string, and no self-registration content exists anywhere in Ch 1–7. **Chapter 8 §4 is the de facto owner.** Do not strip it from Ch 8 on the strength of the stale ledger row.

## The two routes in

"There are two main ways to have Nodes added to the API server: the kubelet on a node self-registers to the control plane, which is the default, or you (or another human user) manually add a Node object."

After a Node object is created, "the control plane checks whether it is valid — whether a kubelet has registered with the API server matching the `metadata.name` field of the Node — and if the node is healthy, meaning the necessary services are running, then it is eligible to run a Pod."

The name "must be a valid DNS subdomain name and must be unique."

## Why this is more than a procedure

**A kubelet joins by writing an object through the API server.** It does not open a private channel; it does the same thing the operator does from a terminal. This is the node-side instance of the chapter's thesis, delivered before the thesis is stated, and it is what makes §8's claim ("no side channels") land as recognition rather than assertion.

## Related

[[api-server-hub]] · [[cordon]] · [[node-conditions]] · [[node-controller]] · [[spec]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cordon.md ===
# Concept: cordon / drain / uncordon

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `uncordon`, `unschedulable-node` (no separate shards; add stubs if a later chapter tags them)

## ★ Fixed Point (verbatim — do not reword)

> `cordon` stops arrivals and touches nothing already aboard. `drain` clears what is aboard. `uncordon` reopens. Three commands, three jobs — and **the maintenance sequence needs the first two.**

## The three commands

- **`kubectl cordon NODE`** — "Mark node as unschedulable." It "prevents the scheduler from placing new Pods onto that Node, but does not affect existing Pods on the Node; this is useful as a preparatory step before a node reboot or other maintenance."
- **`kubectl drain`** — "safely evict all of your Pods from a node before you perform maintenance on it, such as a kernel upgrade or hardware maintenance." See [[drain]].
- **`kubectl uncordon`** — restores scheduling, and is a step you must take yourself: "you need to run `kubectl uncordon <node name>` afterwards to tell Kubernetes that it can resume scheduling new Pods onto the node."

## ⚠ The chapter's costliest confusion

**A cordoned node is not an empty node.** Cordon a node and reboot it for maintenance, and every Pod still on it goes down with the machine. This is the one trap in Chapter 8 with a real operational cost attached rather than only a lost mark.

The instinct behind the error is sound and should be named rather than mocked: "take a node out of service" reads as one action, and in most operational vocabularies it *is* one. Kubernetes splits it because there are real situations where you want arrivals stopped and current occupants left in place — cordon now, drain during a window.

## What cordon actually writes

**`.spec.unschedulable`.** "Cordoned nodes are marked Unschedulable in their spec." Two consequences:

1. It is an act of **declaring intent about a machine**, which is why it lives in `spec` and not `status` — Chapter 4's rule doing real work.
2. `SchedulingDisabled`, the string command-line tools print in the Condition list, **is not a Condition in the Kubernetes API.** The thing the terminal shows is not a thing the API has.

There is no private channel to the node. `cordon` is a write through the one door.

## Related

[[drain]] · [[node-conditions]] · [[spec]] · [[status]] · [[taint]] · [[built-in-node-condition-taints]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/drain.md ===
# Concept: drain, and API-initiated eviction

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical
**Sibling tag served:** `api-initiated-eviction`

## What it is

"You can use `kubectl drain` to safely evict all of your Pods from a node before you perform maintenance on it, such as a kernel upgrade or hardware maintenance."

## It is not a special maintenance channel

"You can request eviction by calling the Eviction API directly, or programmatically using a client of the API server, like the `kubectl drain` command; this creates an `Eviction` object, which causes the API server to terminate the Pod." Using the API to create an Eviction "is like performing a policy-controlled `DELETE` operation on the Pod."

So `drain` is a client that writes objects through the one door — the chapter's §8 thesis, arriving four sections early.

## The DaemonSet exception

"Pods that are part of a DaemonSet tolerate being run on an unschedulable Node," because "the DaemonSet controller automatically adds a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect to DaemonSet Pods."

⚑ **Attribution:** this join was made in **Chapter 7 §4**, not first in Chapter 8. Chapter 8's re-statement is good structured redundancy and should stay, but the framing "this is the point at which the two facts turn out to have been the same fact" overstates it. Ch 7 §4 already said so in full.

## ⚑ Open — PodDisruptionBudget is unowned

B6 assigns "PodDisruptionBudget interaction" to Ch 8 §4. The chapter contains **zero** occurrences of `PodDisruptionBudget`, `PDB` or `disruption`, and says nothing about what can block or stall an eviction. This is **compliant** with B7's fallback branch (the term stays out of all graded material) and nothing is broken — but §4 is the only place in the book where the reader has a question a PDB answers, and the ledger's preferred fix was a one-clause gloss here. Author's call, unchanged since draft-v1.

## Related

[[cordon]] · [[node-conditions]] · [[built-in-node-condition-taints]] · [[api-server-hub]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-conditions.md ===
# Concept: Node conditions

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `ready-condition`, `memorypressure`, `diskpressure`, `pidpressure`, `networkunavailable`, `node-monitor-grace-period`

> **Replay note:** `ch-09/kb-manifest.md` appends to this file. **This shard must be created before ch-09's append is applied.**

## The five conditions

| Condition | `True` when |
|---|---|
| `Ready` | The node is healthy and ready to accept Pods. **False** if the node is not healthy and is not accepting Pods. **Unknown** if the node controller has not heard from the node in the last `node-monitor-grace-period` (default 50 seconds) |
| `DiskPressure` | Pressure exists on the disk size — the disk capacity is low |
| `MemoryPressure` | Pressure exists on the node memory — the node memory is low |
| `PIDPressure` | Pressure exists on the processes — there are too many processes on the node |
| `NetworkUnavailable` | The network for the node is not correctly configured |

Three of the four non-`Ready` conditions are pressure conditions (disk, memory, processes); the fourth is about configuration rather than exhaustion. That is the cheapest way to hold the set.

## ★ `Ready` has three values, and the third is the interesting one

`Unknown` is **not a fourth failure mode. It is the control plane declining to guess.**

- `False` — the node reported *itself* unhealthy. The node is talking to you and telling you something is wrong.
- `Unknown` — nobody has heard from it. Consistent with a dead machine *and* with a network partition between the machine and the control plane.

Those call for different interventions, which is why the distinction is preserved rather than collapsed. Treat the 50-second default as an illustration of the parameter; the **parameter name is the durable fact**, the number is configuration.

## ⚠ `SchedulingDisabled` is not a Condition

"`SchedulingDisabled` is not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec." Command-line tools display it in the Condition list anyway. `NotReady` is likewise a display convention in summary output, not one of the three `Ready` values.

## Node status also carries

Addresses; Conditions; Capacity and Allocatable; and Info — kernel version, Kubernetes version, container runtime details, operating system. `kubectl describe node <name>` shows them.

## Related

[[node-controller]] · [[node-heartbeats]] · [[cordon]] · [[status]] · [[resource-request]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-controller.md ===
# Concept: The node controller

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical

## Its three jobs

"A Kubernetes control plane component that manages several aspects of nodes:

- assigning a CIDR block to the node when it is registered;
- keeping its internal list of nodes up to date with the cloud provider's list of available machines;
- monitoring the nodes' health — updating the `Ready` condition to `Unknown` when a node becomes unreachable, and triggering API-initiated eviction of all the Pods from the node if it stays unreachable."

⚑ **`CIDR` is first used here, book-wide, and is never expanded.** Expand in place; B7's acronym register wrongly assigns first use to Ch 10 §6.

## It is loop-shaped — and NO ORDINAL IS RECORDED

Read the third job as a shape: it **observes** (heartbeats), **compares** against what it expects, and **acts** (condition update, then eviction). That is the pattern from Chapter 3, and the reader can predict its structure without being told.

**Do not record a count here.** See the ⚑ section of [[control-loop]] for why: three ordinal collisions have already occurred in this book, and shipped Chapter 9 has already replaced counting with a chapter list. State the pattern; name the chapters; never state the number.

## Related

[[control-loop]] · [[node-conditions]] · [[node-heartbeats]] · [[node-registration]] · [[cordon]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-heartbeats.md ===
# Concept: Node heartbeats

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical
**Sibling tag served:** `node-lease`

## Two forms

"For nodes there are two forms of heartbeat: updates to the `.status` of a Node, and Lease objects within the `kube-node-lease` namespace, with each Node having an associated Lease object."

## This settles a Chapter 4 IOU

Chapter 4 §3 pointed at the `kube-node-lease` namespace when listing the four initial namespaces and said the Lease objects in it are how the control plane detects node failure. That pointer is paid here: two heartbeat forms, one of them an object living in a namespace the reader has already enumerated.

The pedagogical value is the direction of travel. The reader met the *namespace* first as a piece of cluster furniture, and only now learns what the objects inside it are doing — which makes `kube-node-lease` retroactively meaningful rather than a fourth name to memorize.

## What an absent heartbeat licenses

An absent heartbeat is evidence of a **communication** failure. It does not license the conclusion "the node is broken" — that claims more than the evidence supports, which is exactly why the `Ready` condition has `Unknown` as a distinct value rather than folding it into `False`.

## Related

[[node-conditions]] · [[node-controller]] · [[namespace]] · [[status]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/version-skew.md ===
# Concept: Version skew

**Home:** Chapter 8 §6 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `semantic-versioning`, `upgrade-order`
**B3 note:** flagged as "the densest pure-recall material in the book," taught at the 40% mark. Re-anchored in **Ch 13 §6** as a cause of misdiagnosed failures.

## ★ Fixed Point (verbatim — do not reword)

> **Nothing may be newer than the API server.** kubelet may be up to **three** minors older. **`kubectl` is the single exception, in both directions, at one minor.**

## The generating rule, and why it is a derivation not a list

Every component is a client of one door. A client *newer* than its server can ask for things the server has never heard of — new fields, new resources, new behavior. That one sentence generates **three of the five rows.** The numbers are then not five unrelated facts; they are the sizes of the windows.

## The five rules

| Component | Rule |
|---|---|
| **kube-apiserver** | In HA clusters, newest and oldest instances within **one** minor version **of each other** |
| **kubelet** | Never newer. Up to **three** minors older (kubelets older than 1.25: two) |
| **kube-proxy** | Never newer than kube-apiserver; up to three minors older. Up to three minors older *or newer* than its co-resident kubelet |
| **kube-controller-manager, kube-scheduler, cloud-controller-manager** | Never newer. Expected to match, may be up to **one** minor older, to allow live upgrades |
| **`kubectl`** | Within **one** minor version, **older or newer** |

## The two rows the rule does not generate — for two different reasons

- **`kubectl`**, because it is a *user tool addressing the cluster from outside*, not a component participating in the cluster's internal consistency. Its window is symmetric for human convenience: one `kubectl` against a fleet of clusters on different releases. ⚑ **This explanation is the book's own reasoning, not documented rationale** — the version-skew policy states the rules without saying why. Preserve the hedge; it is a memory aid, not a fact the exam can ask for.
- **The HA kube-apiserver row**, because it is not a bound *relative to* the API server at all. It is a mutual bound *between* API servers. There is no fixed point to measure from — which is why most readers miss it when asked to name the exceptions.

## ⚠ The durable error

kubelet's rule and `kubectl`'s rule are different rules and candidates apply the first to the second. **kubelet: three, older only. `kubectl`: one, either direction.** Wrong number *and* wrong direction — it costs the point twice.

## Upgrade order

"The API server must be upgraded first; everything else follows behind it, within its permitted window." ⚑ **Labelled in-chapter as a derivation** — no cached documentation states an upgrade order in those words. Preserve that framing. Note also that skew is not merely tolerated but *required*: the one-minor allowance for controller-manager and scheduler exists specifically to allow live upgrades.

## Perishability

The specific roster (1.36 / 1.35 / 1.34 at capture) will be different by exam day. **Learn the rule; treat the numbers as illustration.** No practice question in this book turns on which minor is current.

## Related

[[release-cadence]] · [[api-server-hub]] · [[kubeadm]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/release-cadence.md ===
# Concept: Release cadence and supported releases

**Home:** Chapter 8 §6 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `supported-releases`, `three-supported-minors`, `patch-support-window`
**B3 note:** re-anchored in **Ch 17 §8**, where SIG Release and the KEP process explain where the fifteen weeks go. That second pass is scheduled precisely because this trio is among the most forgettable material in the book.

## The three numbers

- "The Kubernetes project maintains release branches for the most recent **three** minor releases."
- "Kubernetes 1.19 and newer receive approximately **one year** of patch support; 1.18 and older received approximately nine months."
- Since 2021, "**three minor releases per year**, approximately every fifteen weeks"; patch releases are cut monthly from the supported branches.

Applicable fixes, including security fixes, "may be backported to those three release branches depending on severity and feasibility."

## Why they are one fact, not three

Three releases a year across three maintained branches is roughly twelve months of coverage — which is exactly the patch-support figure. **The three-branch rule is not an arbitrary number somebody picked; it is what "about a year of support" costs at this release cadence.** Taught as a derivation, the trio survives; taught as three numbers, it does not.

## ⚠ The standard half-memory

"Kubernetes supports the last two releases" is wrong. It is **three**. The chapter's mnemonic — *three back, three a year, three branches* — collapses the kubelet skew window, the cadence and the branch count into one digit, leaving only `kubectl`'s **one, in both directions** to hold separately.

## ⚑ Orphan the ledger recommends and the chapter does not carry

B7 recommends a ⚠ Navigational Hazards line at Ch 8 §6: **"There is no Kubernetes LTS."** It is absent. This is a live misconception for readers arriving from distributions that do have LTS, and it sits directly against the three-minor window. Author's call, unchanged since draft-v1.

## Related

[[version-skew]] · [[kubeadm]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubeadm.md ===
# Concept: Cluster bootstrap tooling

**Home:** Chapter 8 §5 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `minikube`, `kind`, `k3s`, `managed-kubernetes`, `self-hosted-cluster`, `cluster-planning-axes`

> **Filename note:** named for the `kubeadm` slug (a `kb_tags` entry) rather than the prior manifest's unresolvable `cluster-bootstrap-tooling.md`.

## The tools, split by purpose

**For learning:** **minikube**, which "runs a single- or multi-node local Kubernetes cluster," and **kind** — Kubernetes IN Docker — which "runs local clusters using Docker containers as nodes."

**For production:** managed and turnkey certified services from cloud providers, or self-managed clusters bootstrapped with **kubeadm**, "the officially supported tool for creating clusters, used to install the control plane and join nodes." **k3s** is "a lightweight distribution."

The kind/minikube choice is really a question of whether a *pipeline* or a *person* is the user: kind's Docker-container nodes make clusters fast to create and destroy, which suits CI; minikube's conveniences suit a human at a keyboard.

## The requirement none of them removes

"A container runtime — containerd or CRI-O — must be installed on every node, and `kubectl` is the command-line tool for managing any cluster."

This is the first point in the book where Chapter 2's CRI boundary has an **operational** consequence rather than an architectural one. kubeadm will build a control plane and join nodes; a container runtime must be on those nodes regardless, because it lives on the other side of a line the project deliberately drew. It is also the most attractive wrong answer in the chapter's practice set, precisely because installing one *sounds* like something a complete bootstrapper would do.

## Ownership, and what it decides

Whoever operates the control plane holds **the upgrade calendar** and **the etcd backup**. On a managed platform those are the provider's; self-hosted, they are yours. Scheduler profile configuration also lives in control-plane component configuration, reachable only by whoever owns it.

⚑ **The duty split stops there, deliberately.** Research gap **G-8G**: kubernetes.io licenses only the *existence* of a split ("consider which aspects of operating a Kubernetes cluster you want to manage yourself and which you prefer to hand off to a provider") and does not enumerate sides; no vendor-neutral shared-responsibility source is cached. **Do not restore a five-item duty list** in this shard, in Ch 8, or in any later chapter without one.

## Related

[[cri]] · [[version-skew]] · [[etcd-backup]] · [[control-plane-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/etcd-backup.md ===
# Concept: etcd backup and restore

**Home:** Chapter 8 §7 · **Competency:** D1.2 · **Status:** canonical
**Sibling tags served:** `etcd-snapshot`, `etcd-access-equals-root`, `disaster-recovery`

## ★ Fixed Point (verbatim — do not reword)

> Every object you have ever created lives in etcd. **Access to etcd is equivalent to root permission in the cluster.** A snapshot is therefore both your only route back from disaster and the most dangerous single file you own.

## Why

"All Kubernetes objects are stored in etcd." Backing it up periodically "is important to recover Kubernetes clusters under disaster scenarios, such as **losing all control plane nodes**."

That scenario is more specific and more survivable than "the cluster died," and the distinction is the section's teaching point. Losing every control-plane node does not stop the worker nodes: kubelets keep running what they were last told to run, and traffic keeps being served. **What is lost is the entire record of *intent*** — every declaration of what should be running, which is the only thing that lets the cluster reconcile, scale, heal or change anything.

## Mechanics

- **Backup:** "a built-in snapshot, `etcdctl snapshot save backup.db`, or a volume snapshot of etcd's storage." Optional `--endpoints`, `--cacert`, `--cert`, `--key` for a TLS-protected cluster.
- **Restore:** "`etcdutl snapshot restore`, which operates directly on the etcd data files; after a restore, the control plane components are restarted against the restored data directory."

Restore is therefore a **maintenance event** — a window, a plan, somebody watching — not an operation slipped in between meetings. Note the two utilities differ by two letters (`etcdctl` saves, `etcdutl` restores), which is exactly why the confusion is worth a distractor.

⚑ **Do not expand into etcd TLS configuration guidance.** The `etcd-access-control` snapshot's own note records that the source page's TLS configuration guidance was not verbatim-verified in that fetch.

## The two sentences that matter more than the commands

- "The snapshot file contains all the Kubernetes state and critical information; **keep it encrypted and store it outside the control plane nodes.**"
- "**Access to etcd is equivalent to root permission in the cluster,** so ideally only the API server should have access to it."

Read together: an unencrypted snapshot on a control-plane node is simultaneously the only disaster recovery *and* a complete compromise of the cluster in one readable file. Not a credential *for* the cluster — root *in* it, at rest.

**Two independent failure modes, and both must be named:** a backup stored only on the machines it insures against losing does not survive the event (availability); an unencrypted one is a root-equivalent credential (confidentiality). A snapshot can fail you by not being there, or by being read.

## The architecture, from the other side

"Only the API server should have access to it" is the single-door claim stated in reverse. §2 says every request terminates at the API server; §7 says only the API server should reach the store behind it. Same claim, opposite direction.

## Related

[[api-server-hub]] · [[kubeadm]] · [[secret]] · [[control-plane-components]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

## Chapter 8 — the node controller, and the ordinal problem resolved

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 8 §4 identifies **one** control loop: the **node controller**. It observes (heartbeats), compares against what it expects, and acts (updating the `Ready` condition to `Unknown`, then triggering API-initiated eviction). §8 re-reads it as one of the chapter's five proofs that no administrative act is a new mechanism.

### ⚑ NO ORDINAL IS RECORDED HERE — and the conflict is now three-way

ch-09's Stage 14 left a standing instruction on this shard: record no count, and do not renumber without deciding whether Chapter 9 consumes one ordinal or two. **That instruction stands, and this chapter adds two facts to it.**

1. **Chapter 9's revision already solved this, the right way.** `chapter-09:931` now reads: *"You have met that shape in **Chapters 3, 4, 6, 7 and 8**, and here it is again in a reference page about packet forwarding."* The ordinal is gone; a chapter list replaced it. **Chapter 8 is now the only chapter in the book still counting** — it claims "the sixth" twice, and "five instances of it since [Chapter 3]" once, a figure not derivable from any reading of the shipped text.
2. **Chapter 9's list is itself wrong about Chapter 7.** Chapter 7 contains exactly one occurrence of "control loop," at `chapter-07:266`, and it is a disavowal: *"The last chapter ended on the one thing the control loop cannot do. It creates a Pod. It does not decide where the Pod goes."* Chapter 7 defines itself **against** the pattern; it does not instantiate it.

### The collision that actually threatens the book

Shipped Chapter 6 closes (`chapter-06:1465`): *"you have seen the control loop **twice now, at two altitudes**, and recognized it the second time. Hold onto that recognition. You are going to need it once more, and **the third time is the one that matters.**"*

`chapter-06:287` states why that sentence is load-bearing: *"Chapter 15 generalizes it to a loop whose desired state lives in a Git repository. A reader who does not feel the shape here will meet Chapter 15's synthesis as a fifth list to memorize instead of as a recognition."*

**Ch 15 §7 is the book's designated PRIMARY ZENITH.** "The third time is the one that matters" does not survive a reader who has been counting to six two chapters earlier. This is a Zenith-integrity problem, not a numbering nit.

### Recommended resolution — a book-level convention

**State the pattern. Name the chapters. Never state the count.**

- Chapter 8: drop both ordinals; keep the recognition (*"you could have predicted its structure without being told"*), which is the sentence doing the actual work.
- Chapter 9: drop **Chapter 7** from its list, leaving Chapters 3, 4, 6 and 8 — four instances that all survive inspection.
- Chapter 6: unchanged. Its "twice, at two altitudes" is a claim about altitudes, and it is the sentence Chapter 15 is banked against.

Running ordinals have now produced **three** collisions in this book (Ch 8 vs Ch 6; Ch 8 vs Ch 9-as-drafted; Ch 9's list vs Ch 7), plus a fourth recorded in B6 over the pluggable-interface count. That is past the threshold for a convention rather than four separate fixes.

### Incidental, carried forward from ch-09 and still unfixed

`chapter-08:713` points at `Ch 3 §5 — the control loop`; the B6 skeleton puts the control loop at **Ch 3 §6** (§5 is *The Only Door In*). Chapter 8's revision retargets most of its Ch 3 pointers correctly but this instance should be re-verified when [X1] is applied.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespace.md ===

## Chapter 8 — the division mechanism, named and bounded

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 4 said namespaces "are a way to divide cluster resources between multiple users, via resource quota" and deferred the mechanism. Chapter 8 §3 delivers it at full strength: a ResourceQuota "provides constraints that limit **aggregate resource consumption per namespace**." See [[resource-quota]].

Two additions this shard should carry:

- **The namespace is not the discrimination.** Both ResourceQuota and LimitRange are namespaced objects operating inside one namespace. What differs is *what is counted* — the namespace's aggregate, versus one object's numbers — not the boundary they sit in. Readers who file LimitRange as "the non-namespace one" have mis-learned it.
- **The limit of the abstraction.** **You can quota a team. You cannot quota a machine.** Every resource a quota can count is namespaced; a Node is not. See [[namespaced-vs-cluster-scoped]].

Chapter 8 also settles Chapter 4 §3's `kube-node-lease` pointer: the Lease objects in that namespace are one of the two node heartbeat forms. See [[node-heartbeats]].

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cluster-scoped-resource.md ===

## Chapter 8 — Nodes as the worked consequence

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 4 established the boundary; Chapter 8 §3 gives it its first operational consequence, in the one line the reader should be able to say out loud: **you can quota a team, you cannot quota a machine.**

The reason is entirely derivable from what the reader already has. A ResourceQuota is a statement about a namespace, every resource it can count is namespaced, and "namespace-based scoping is applicable only for namespaced objects… and not for cluster-wide objects such as StorageClass, Nodes and PersistentVolumes." No new rule is needed.

**Downstream:** Ch 12 §3 derives the RBAC four-way matrix from this boundary rather than asking the reader to memorize four combinations. Chapter 8's three retrievals of the hinge (§3 close, Bearings #1 Q5, Practice Q6) are what make that saving available.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/spec.md ===

## Chapter 8 — `cordon` writes a spec field, and that is the whole chapter

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 8 §8 makes this shard's rule do more work than anywhere else in the book. `kubectl cordon` has no private channel to the node and does not connect to the machine; it **writes a field on a Node object through the API server** — "cordoned nodes are marked Unschedulable in their spec."

The inference the reader is asked to make: `spec` is the half of an object *you* declare, against `status`, which the system reports. Cordoning therefore lives in `spec` **because it is an act of declaring intent about a machine**, not an observation of one. The reader can predict which half it lands in before being told.

The corollary is the sharper half: **`SchedulingDisabled`, the string the terminal prints, is not a Condition in the API at all.** What you declared and what your tool displays are two different things, and neither is `status`.

Practice Q10 tests exactly this, tagged `[retrieval: ch4]`.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/status.md ===

## Chapter 8 — the boundary from the other side

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 8 §4 supplies this shard's richest worked example: a Node's `status` carries Addresses, Conditions, Capacity and Allocatable, and Info — all of it reported *by* the system, none of it written by an operator.

Three refinements Chapter 8 adds:

1. **`status` can express uncertainty.** `Ready: Unknown` is the control plane declining to guess — an absent heartbeat is evidence of a communication failure, consistent with a dead machine *or* a network partition. A status field that reports "we cannot tell" is a design choice, not a gap.
2. **What a tool displays is not what status holds.** `SchedulingDisabled` appears in `kubectl`'s Condition list and is not a Condition in the API; `NotReady` appears in summary output and is not one of `Ready`'s three values.
3. **Heartbeats are status writes.** One of the two node heartbeat forms is literally "updates to the `.status` of a Node" — so `status` is not only read by controllers, it is the channel a node reports over.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-server-hub.md ===

## Chapter 8 — what the door *does*, and what is behind it

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 3 established that every request terminates at the API server. Chapter 8 supplies the "and then what," in four instalments this shard should carry:

1. **Three gates.** Authentication, authorization, admission — stages of one request path, ending in "once a request passes all admission controllers, it is validated… and then written to the object store." See [[api-access-gates]].
2. **The audit log is kept by the door.** "Audit records begin their lifecycle inside the kube-apiserver component, and each request on each stage of its execution generates an audit event." Not a separate observer watching the entrance.
3. **The hub-and-spoke sentence is what makes the model sufficient.** "All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services." Three gates on one door would be an incomplete access-control story if there were other doors. There are not.
4. **The store behind it.** "Access to etcd is equivalent to root permission in the cluster, so ideally only the API server should have access to it" — the single-door claim stated in reverse.

Chapter 8 §8's ⚑ honest correction belongs here too: the *acts* are consequences of this architecture; the *project's policies* (which bootstrapper is supported, how many branches are maintained, how far a kubelet may lag) are not derivable from it and must be learned.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serviceaccount.md ===

## Chapter 8 — the ServiceAccount as an identity at gate one

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 5 introduced the ServiceAccount as a Pod field. Chapter 8 shows what it is *for*: Pods "connect by leveraging a ServiceAccount: Kubernetes automatically injects the public root certificate and a valid bearer token into the Pod when it is instantiated."

The structural point worth recording is that **one artifact has two readers**. The injected token file at `/var/run/secrets/kubernetes.io/serviceaccount/token` is what §1's `kubectl` looks for when deciding it is running inside a cluster, and what §2's authentication gate reads when deciding who is asking. Detection and identity, same file.

Consequence the reader is most often surprised by: `kubectl` inside a Pod is **not you**, and does **not** default to the `default` namespace — it "acts against the namespace of the ServiceAccount, unless `--namespace` is given."

⚑ **bearer token** is used as a term of art here and is undefined in this chapter and every prior one. Glossary gap.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/taint.md ===

## Chapter 8 — what `cordon` writes, and what it does not

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 8 §4 is careful here and the care should be preserved on replay. **`cordon` writes a spec field** — "cordoned nodes are marked Unschedulable in their spec" — and the chapter deliberately does **not** assert that `cordon` applies the built-in `node.kubernetes.io/unschedulable` taint, because the cached sources do not join those two facts.

What the chapter *does* assert, and what Bearings #2 Q1 tests, is narrower and fully sourced: there exists a built-in taint whose **effect matches** what cordoning does, and Chapter 7's rule for that effect settles the consequence. `NoSchedule` means no new Pods are scheduled on the tainted node absent a matching toleration, and **Pods currently running on the node are not evicted.**

Separately, §8 records that the scheduler "checks taints, not node conditions, when it makes scheduling decisions" — which is the reason a *condition* list and a *taint* list are different things a reader must not merge.

**Do not tighten this into "cordon applies the taint" on a later pass** without a source that states it. The narrower claim is the one that survives.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/built-in-node-condition-taints.md ===

## Chapter 8 — the DaemonSet exception during maintenance

**Added by ch-08 Stage 14, 2026-08-30.**

"Pods that are part of a DaemonSet tolerate being run on an unschedulable Node," because "the DaemonSet controller automatically adds a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect to DaemonSet Pods."

Operational consequence Chapter 8 adds: drain a node and every Pod leaves **except** the DaemonSet's, which is the correct behaviour rather than a bug — node-local facilities should keep running while the node is being worked on.

⚑ **Attribution correction.** Chapter 8 §4 frames this as "the point at which the two facts turn out to have been the same fact." **Chapter 7 §4 already joined them, in full:** *"Because the controller sets the `node.kubernetes.io/unschedulable:NoSchedule` toleration automatically, Kubernetes can run DaemonSet Pods on nodes that are marked unschedulable."* Ch 8's restatement is good structured redundancy and should stay; only the claim of *first* joining is wrong. Stage 13 fix [C5] softens the framing and adds a `Ch 7 §4` cross-bearing.

Practice Q17 is tagged `[retrieval: ch6]`, but only its first half (the controller's name) is Chapter 6's — the toleration is Chapter 7 §4. Retag or credit in the answer key.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-request.md ===

## Chapter 8 — Capacity vs Allocatable, and requests that arrive by default

**Added by ch-08 Stage 14, 2026-08-30.**

**This settles Chapter 7 §2's explicit IOU** — what makes Capacity and Allocatable differ, and how it is configured, was deferred to Chapter 8.

- **Capacity** — "the total amount of resources that a Node has."
- **Allocatable** — "the amount of resources on a Node that is available to be consumed by normal Pods." The scheduler "treats 'Allocatable' as the available capacity for Pods, and does not over-subscribe it."

**Why two numbers:** nodes "can be scheduled to `Capacity`, and Pods can consume all the available capacity on a node by default — which is an issue, because nodes typically run quite a few system daemons that power the OS and Kubernetes itself." Two reservations account for them: **`kubeReserved`** (kubelet, container runtime) and **`systemReserved`** (`sshd`, `udev`).

**Exam-relevant distinction:** Capacity is the machine's total; **Allocatable is what the scheduler does arithmetic against.**

⚑ **No arithmetic, deliberately, and this must survive later passes.** Both the node-allocatable and reserve-compute-resources snapshots state explicitly that the Capacity → reservations → Allocatable relationship is published only as an image with no text equivalent, so no equation is extractable. **Do not add one, even in words.** Configuration flags are above associate tier and are out of scope.

### The second contribution: a defaulted request is a real request

A LimitRange default is not bookkeeping. Chapter 5 established that the scheduler uses a container's request to decide placement; Chapter 8 §4 establishes that it does arithmetic against Allocatable. So a Pod that previously declared nothing and now carries an injected default **books capacity it did not book before, and may fit on fewer nodes.** The manifest did not change; the Pod did. Practice Q7 tests this, tagged `[retrieval: ch5]`.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cri.md ===

## Chapter 8 — the boundary's first operational consequence

**Added by ch-08 Stage 14, 2026-08-30.**

Chapter 2 taught the CRI as an interface question — an architectural boundary between Kubernetes and the thing that actually starts containers. Chapter 8 §5 is the first point in the book where that boundary **costs someone a step**:

"A container runtime — containerd or CRI-O — must be installed on every node, and `kubectl` is the command-line tool for managing any cluster."

`kubeadm` is "the officially supported tool for creating clusters, used to install the control plane and join nodes" — and it does **not** supply a runtime, because a runtime sits on the other side of a line the project deliberately drew. The reader who understood Chapter 2 as architecture now meets it as a provisioning requirement.

This is also the chapter's most attractive distractor (Practice Q12 option D): a bootstrapper that installs everything *sounds* right, and only the interface boundary rules it out. Bearings #2 Q4 retrieves it directly at six chapters' distance — the longest retrieval span in the chapter, and one of the three items satisfying B3's ≥4-chapters-back spacing floor.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.2 — Kubernetes Fundamentals › Administration | Chapter 8 | deep | — |

<!--
D1.2 notes (Stage 14, ch-08, 2026-08-30):

- Competency name is "Administration", under domain D1 "Kubernetes Fundamentals"
  at 44%. Source: cncf-kcna-curriculum-pdf-2026-08-23.md:13 -- "44% - Kubernetes
  Fundamentals: Kubernetes Core Concepts; Administration; Scheduling;
  Containerization".

- CHAPTER METADATA DRIFT, one word. The chapter's metadata line reads "Competency:
  Cluster Administration". The curriculum says "Administration", and chapter-09:192
  uses its own competency name verbatim ("Competency: Networking"). Chapter 8 is the
  only chapter that renames its competency. Flagged, not silently normalized -- the
  fix belongs in the chapter, not in this ledger.

- ALL EIGHT SECTIONS carry objectives: ["D1.2"]. Single-competency chapter; no
  sub-objective is shared with another chapter, so this row closes D1.2 alone --
  unlike D2.1, which Ch 9 opens and Ch 10 completes.

- THIS ROW CLOSES DOMAIN D1 (44%): D1.1 Ch 3 (+Ch 4, object layer) / D1.2 Ch 8 /
  D1.3 Ch 7 / D1.4 Ch 2. The domain-level audit ch-08 recommended and ch-09 called
  "overdue" can now actually be run.

- CORRECTION TO ch-09's NOTE. ch-09 records D1.4 as "STILL UNRECORDED... because
  Chapter 2's Stage 14 never ran." Chapter 2's Stage 14 DID run (ch-02/kb-manifest.md,
  2026-08-24 15:24) and records "| D1.4 | Chapter 2 | deep | 2026-08-24 |", plus a
  correction to Ch 7's transcription of Ch 2 as D1.1. ch-03's original flag was
  correct when written and was overtaken. Do not carry it forward again.

- THE ~5% IS AN AUTHORED ALLOCATION. CNCF publishes DOMAIN weights only, never
  COMPETENCY weights; the chapter's metadata line and the front matter both disclose
  this. Unchanged since Ch 7.

- NO SUB-OBJECTIVE GAP. Draft-v1 shipped with auditing as PARTIAL (D1.2-08); the
  revision closes it -- §2 now carries the definition, the seven questions, and the
  kube-apiserver lifecycle fact, all source-tagged. Depth is "deep", not "deep
  (1 partial)".

- ONE SCOPE DECISION RECORDED, NOT A GAP: the managed/self-hosted duty split is
  asserted for exactly two duties (upgrade timing, etcd backup) because those are
  the two the architecture decides. Research gap G-8G: no vendor-neutral
  shared-responsibility source exists in the kubernetes.io doc tree, so no fetch
  closes it. Deliberate narrowing, recorded so a later audit does not read it as
  under-coverage.
-->
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

| Tested topic | Original chapter | Retested in |
|---|---|---|
| namespaces divide cluster resources via resource quota | ch 4 §3 | ch 8 — ☆ Bearings #1 item 5 |
| `node.kubernetes.io/unschedulable`, `NoSchedule`, and running Pods not evicted | ch 7 §4 | ch 8 — ☆ Bearings #2 item 1 |
| container runtime (containerd / CRI-O) and the CRI boundary | ch 2 §4 | ch 8 — ☆ Bearings #2 item 4 |
| Nodes are not namespaced objects | ch 4 §3 | ch 8 — Practice Q6 |
| a container's request is the scheduler's placement input | ch 5 §8 | ch 8 — Practice Q7 |
| `spec` is what you declare; `status` is what the system reports | ch 4 §2 | ch 8 — Practice Q10 |
| the control loop — observe, compare, act | ch 3 §6 | ch 8 — Practice Q11 |
| DaemonSet, one Pod per eligible node | ch 6 §7 | ch 8 — Practice Q17 |

<!--
Chapter 8 retrieval accounting (Stage 14, ch-08, 2026-08-30):

- 8 tagged items / 33 graded items (15 Bearings + 18 Practice) = 24.2%.
  B3 sets Ch 8 in the 20-25% band. IN BAND, at the top of it. Draft-v1 sat at
  18.2%; two items were added in revision and the shortfall is closed.

- B3 SPACING FLOOR MET. retrieval-architecture.md sets a binding rule: "from Ch 8
  on, at least one item must come from >=4 chapters back." Chapter 8 has FIVE --
  ch 2 (six back), ch 3 (five back), ch 4 x3 (exactly four back). Comfortable pass.
  Stage 13 did not check this; recorded here so the audit exists.

- TWO ITEMS CARRY QUALIFICATIONS, both raised by Stage 13 and both unfixed as of
  this stage:

  * Practice Q11's keyed answer offers "the scheduler's watch on unscheduled Pods"
    as a second example of the pattern. The watch language is genuinely Ch 7's,
    but chapter-07:266 frames the scheduler as what the control loop CANNOT do.
    Recommended swap: the Job controller (Ch 3's own documented example) or the
    ReplicaSet controller (Ch 6). See the control-loop shard -- this interacts with
    chapter-09:931, which lists Chapter 7 among the chapters where the reader met
    the shape. Both cannot stand.

  * Practice Q17 is tagged [retrieval: ch6], but only the controller's NAME is
    Chapter 6's. The toleration the answer turns on is Chapter 7 section 4.
    Retag ch6+ch7, or credit Ch 7 in the answer key -- the second converts an
    untagged dependency into a second retrieval hit at no cost.

- SOUNDINGS ARE EXCLUDED FROM THE BUDGET (B3 decision 2) but do the work anyway.
  Chapter 8's Soundings draw on Ch 3 (single door), Ch 4 (namespaces; kube-node-lease
  Leases) and Ch 7 (the unschedulable taint) -- four of eight items are prerequisite
  retrieval, and Q3 and Q7 are deliberately unanswerable reasoning items with the
  answer key saying so. Part 11 compliant.

- FORWARD OBLIGATIONS, both of B3's named anchors for this chapter's decay-prone
  material are in place and must not be dropped:
    * version skew  -> Ch 13 section 6 (as a cause of misdiagnosed failures)
    * release cadence -> Ch 17 section 8 (SIG Release / KEP, where the three-branch
      rule and the ~3/year cadence explain each other)
  Bearings #3 A3 tells the reader outright that the Ch 17 pass is the second look.
  B3 flagged section 6 as "the densest pure-recall material in the book, taught at
  the 40% mark and otherwise never revisited before exam day" -- these two anchors
  are the fix, and dropping either reopens the decay problem.

- NAMESPACED-VS-CLUSTER-SCOPED (B3 cross-cutting theme #2) is retrieved three times
  in this chapter -- section 3 close, Bearings #1 Q5, Practice Q6 -- which is what
  makes Ch 12 section 3's RBAC DERIVATION affordable instead of a four-way matrix
  the reader has to memorize.
-->
=== END APPEND ===

**Three things worth your attention, in order:**

**The control-loop ordinal is a three-way collision, not the two-way one the integration report found.** Chapter 9's revision already dropped its own ordinal and replaced it with a chapter list (`chapter-09:931` — "Chapters 3, 4, 6, 7 and 8"), which makes Chapter 8 the only chapter in the book still counting. Chapter 9's list is also wrong about Chapter 7, whose single mention of the pattern is a disavowal. Dropping Chapter 8's ordinal is still the right first fix; it just needs Chapter 9's list trimmed alongside it, and the book needs the convention — name the chapters, never the count.

**The prior manifest's shard filenames would not have loaded.** `context_packer.resolve_kb_shards` only reads `knowledge-base/{category}/{tag}.md` where `tag` comes from the chapter's `kb_tags`. Chapter 7's manifest respects that; ch-08's earlier one did not (`kubectl-grammar.md`, `resource-quota-and-limitrange.md`, `node-lifecycle.md` are none of them tagged anywhere). Every shard above is named for a real Chapter 8 tag, and I listed the 31 tags still without an owner rather than padding the count with stubs.

**Nothing here reached disk, and that is deliberate.** No parser for `=== WRITE` exists anywhere in `certcomp` — the only match is the prompt itself — and `Book-KCNA/knowledge-base/` still does not exist. I did not write the files directly: `control-loop.md` is created by ch-03 and appended to by ch-07, ch-08 and ch-09, so writing Chapter 8's version first would install my append as the file's origin and delete ch-03's canonical Fixed Point. Twelve chapters of knowledge base now need a replay harness that applies ch-01 → ch-11 in order, not eleven stages each writing what it can reach.
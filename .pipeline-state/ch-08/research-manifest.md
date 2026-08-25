I hit a hard blocker partway through, so here's the situation up front, then the complete work.

## Blocker: this session cannot write files

Every write path is refused — `Write`, PowerShell `Set-Content`, and Bash redirection, including into `C:\dev\lodestar\certcomp` itself, which the error message lists as an allowed directory. That's consistent with the orchestrator stripping `Write` from `--allowed-tools` (noted in `CLAUDE.md`), but here it also blocks shell writes, so the snapshots can't be landed from inside this run.

**The research is complete.** All fetches succeeded. Below is a single script that writes all 10 snapshots plus the manifest. Either run it yourself, or grant write access to `C:\dev\lodestar\Book-KCNA\` and I'll run it.

## What the research found

Both blocking gaps are closed, and three things turned up that the outline didn't anticipate:

- **Open Q #5 is resolved, not deferred.** `node-monitor-grace-period` *does* have a documented default — 50 seconds — on `/docs/reference/node/node-status/`. The outline's instruction ("if a later fetch supplies a default, it may be added as an illustration, never as a rule") now applies.
- **§8's headline claim is now sourceable.** The node-status reference says, verbatim: *"`SchedulingDisabled` is not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec."* That's exactly what §8's strongest demonstration item and the §1–§2 Practice retrieval item ("spec field or status field?") were asserting on inference.
- **A citation error in an existing snapshot.** `k8s-docs-nodes-2026-08-23.md` carries the node-conditions table under `source_url: .../concepts/architecture/nodes/`. As of today that content is no longer on that page — it lives at `/docs/reference/node/node-status/`. The new snapshot supersedes it for those facts.

One caution worth flagging now: **Bearings #2 item 1's stated correct answer is not sourceable as written.** It asks what command applies the `node.kubernetes.io/unschedulable` taint, answer `kubectl cordon`. No single cached or fetched source says cordon applies that taint. A two-source chain supports it (cordon sets `.spec.unschedulable` → "The node controller automatically taints a Node when certain conditions are true" → the taint list includes `unschedulable`), but it is an inference, not a quote. Details in the manifest's Gaps section.

## The writer script

```python
# write_ch08_sources.py  --  run from anywhere; adjust BOOK if your layout differs.
import os, sys
sys.stdout.reconfigure(encoding="utf-8")

BOOK = r"C:\dev\lodestar\Book-KCNA"
SRC  = os.path.join(BOOK, "sources")
MAN  = os.path.join(BOOK, ".pipeline-state", "ch-08")

FILES = {}

FILES["k8s-docs-controlling-access-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/concepts/security/controlling-access/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/security/controlling-access.md"
fetched_at: "2026-08-24T18:55:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["api-access-gates", "authentication", "authorization", "admission-control", "admission-controller", "mutating-admission", "auditing", "api-request-stages"]
closes_gap: "ch-08 outline Open Question #2 (BLOCKING). No previously cached source stated the sequential semantics of the three gates, that admission runs after authorization and before persistence, or that admission modules may MODIFY rather than only reject. All four sub-claims are closed below."
---
# Controlling Access to the Kubernetes API

> **Extraction note.** Passages marked **[VERBATIM]** are quoted character-for-character
> from the source and are safe to cite. Headings are the source's own. A claim available
> only as an observation about the page's structure is marked **[STRUCTURAL]** and must
> not be quoted as prose.

## Overview

**[VERBATIM]**

> "Users access the Kubernetes API using `kubectl`, client libraries, or by making REST requests."

> "When a request reaches the API, it goes through several stages."

The page carries a diagram of the request path. Its alt text is **[VERBATIM]**:

> "Diagram of request handling steps for Kubernetes API request"

**[STRUCTURAL]** The page presents the stages as sequential H2 sections in this order:
Transport security, Authentication, Authorization, Admission control, Auditing.

## Transport security

**[VERBATIM]**

> "the Kubernetes API server listens on port 6443 on the first non-localhost network interface, protected by TLS."

> "you need a copy of that CA certificate configured into your `~/.kube/config`"

## Authentication

**[VERBATIM]**

> "The cluster creation script or cluster admin configures the API server to run one or more Authenticator modules."

> "The input to the authentication step is the entire HTTP request; however, it typically examines the headers and/or client certificate."

> "While Kubernetes uses usernames for access control decisions and in request logging, it does not have a `User` object."

> "If the request cannot be authenticated, it is rejected with HTTP status code 401."

## Authorization

**[VERBATIM]**

> "A request must include the username of the requester, the requested action, and the object affected by the action."

> "Kubernetes supports multiple authorization modules, such as ABAC mode, RBAC Mode, and Webhook mode."

> "if any module authorizes the request, then the request can proceed. If all of the modules deny the request, then the request is denied (HTTP status code 403)."

## Admission control

**[VERBATIM]**

> "Admission Control modules are software modules that can modify or reject requests."

> "Admission Control modules can access the contents of the object that is being created or modified."

> "When multiple admission controllers are configured, they are called in order."

> "Unlike Authentication and Authorization modules, if any admission controller module rejects, the request is immediately rejected."

> "admission controllers can also set complex defaults for fields."

> "Admission controllers act on requests that create, modify, delete, or connect to (proxy) an object. Admission controllers do not act on requests that merely read objects."

The sentence establishing persistence order -- **[VERBATIM]**:

> "Once a request passes all admission controllers, it is validated using the validation routines for the corresponding API object, and then written to the object store."

## Auditing

**[VERBATIM]**

> "Kubernetes auditing provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster."

---

## What this snapshot licenses Chapter 8 sec.2 to assert

1. The three gates are **sequential**, not parallel. The page orders them as stages of one
   request path and states the object reaches the store only after passing all admission
   controllers.
2. **Admission is the only gate that can change the request.** Authentication rejects with
   401; authorization denies with 403; admission modules "can modify or reject requests" and
   "can access the contents of the object that is being created or modified."
3. **Admission is also the only gate with unanimous-reject semantics.** Authorization is
   any-module-approves; admission is any-module-rejects. The page draws this contrast itself
   ("Unlike Authentication and Authorization modules...").
4. **Admission runs before persistence.** Validation and the write to the object store follow it.
5. Admission does not see reads. `get`, `watch` and `list` do not pass this gate.

NOT IN THIS SNAPSHOT: the mutating/validating phase split (see
`k8s-docs-admission-controllers-2026-08-24.md`), the RBAC object model, Konnectivity or
SSH tunnels (deliberately omitted -- ch-08 outline Open Question #7).
"""

FILES["k8s-docs-admission-controllers-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/access-authn-authz/admission-controllers.md"
fetched_at: "2026-08-24T18:56:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["admission-controller", "mutating-admission", "validating-admission", "dynamic-admission-control", "resource-quota", "limit-range", "noderestriction"]
closes_gap: "ch-08 outline Open Question #2, secondary fetch. Supplies the mutating/validating distinction and the named built-in plugins sec.2 and sec.3 depend on."
---
# Admission Controllers Reference

> **Extraction note.** All passages below are **[VERBATIM]**.

## What are they?

> "Admission controllers are code within the Kubernetes API server that check the data arriving in a request to modify a resource."

> "Admission controllers apply to requests that create, delete, or modify objects."

> "Admission controllers do not (and cannot) block requests to read (get, watch or list) objects, because reads bypass the admission control layer."

> "Admission control mechanisms may be validating, mutating, or both. Mutating controllers may modify the data for the resource being modified; validating controllers may not."

## The two phases

> "In the first phase, mutating admission controllers are run. In the second phase, validating admission controllers are run."

> "If any of the controllers in either phase reject the request, the entire request is rejected immediately and an error is returned to the end-user."

## Why do I need them?

> "Several important features of Kubernetes require an admission controller to be enabled in order to properly support the feature. As a result, a Kubernetes API server that is not properly configured with the right set of admission controllers is an incomplete server and will not support all the features you expect."

## Selected built-in plugins

- **ResourceQuota** -- "This admission controller will observe the incoming request and ensure that it does not violate any of the constraints enumerated in the ResourceQuota object."
- **LimitRanger** -- "This admission controller will observe the incoming request and ensure that it does not violate any of the constraints enumerated in the LimitRange object."
- **NodeRestriction** -- "This admission controller limits the Node and Pod objects a kubelet can modify."
- **MutatingAdmissionWebhook** -- "This admission controller calls any mutating webhooks which match the request."
- **ValidatingAdmissionWebhook** -- "This admission controller calls any validating webhooks which match the request."

---

NOT IN THIS SNAPSHOT: the full plugin roster, plugin ordering, and enable/disable flag
syntax. All are above associate tier. The five entries above are the ones sec.2 and sec.3
name; the outline caps PSA and RBAC at one clause each.
"""

FILES["k8s-docs-resource-quotas-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/concepts/policy/resource-quotas/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/policy/resource-quotas.md"
fetched_at: "2026-08-24T18:57:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["resource-quota", "namespaced-vs-cluster-scoped", "admission-control", "compute-resource-quota", "object-count-quota", "storage-quota"]
closes_gap: "ch-08 outline Open Question #3 (BLOCKING), first half. Previously nothing cached stated what a quota counts, or the rule that a quota'd namespace forces Pods to declare requests/limits."
scope_note: "Quota scopes, scope selectors and priority-class quota were deliberately NOT extracted -- above associate tier, per the outline's scope guard."
---
# Resource Quotas

> **Extraction note.** Passages marked **[VERBATIM]** are safe to cite. The compute and
> storage resource-name lists are transcribed enumerations of the source's tables; the
> per-row DESCRIPTION cells were **not** verbatim-verified in this pass and are marked
> **[NAMES ONLY]**. Do not quote row descriptions as source sentences.

## What it is

**[VERBATIM]**

> "When several users or teams share a cluster with a fixed number of nodes, there is a concern that one team could use more than its fair share of resources."

> "A resource quota, defined by a ResourceQuota object, provides constraints that limit aggregate resource consumption per namespace."

## How it works

**[VERBATIM]**

> "A cluster administrator creates at least one ResourceQuota for each namespace."

> "Users create resources (pods, services, etc.) in the namespace, and the quota system tracks usage to ensure it does not exceed hard resource limits."

> "If creating or updating a resource violates a quota constraint, the control plane rejects that request with HTTP status code `403 Forbidden`."

> "If quotas are enabled in a namespace for resource such as `cpu` and `memory`, users must specify requests or limits for those values when they define a Pod."

## The rule that makes a valid Pod stop being valid

**[VERBATIM]**

> "If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients, **must** specify either `requests` or `limits` for that resource, for every new Pod you submit. If you don't, the control plane may reject admission for that Pod."

> "You can use a LimitRange to automatically set a default request for these resources."

## Enabling

**[VERBATIM]**

> "ResourceQuota support is enabled by default for many Kubernetes distributions. It is enabled when the API server `--enable-admission-plugins=` flag has `ResourceQuota` as one of its arguments."

> "A resource quota is enforced in a particular namespace when there is a ResourceQuota in that namespace."

## Compute Resource Quota -- [NAMES ONLY]

`limits.cpu`, `limits.memory`, `requests.cpu`, `requests.memory`, `hugepages-<size>`,
`cpu` (alias for `requests.cpu`), `memory` (alias for `requests.memory`)

## Quota for storage -- [NAMES ONLY]

`requests.storage`, `persistentvolumeclaims`,
`<storage-class-name>.storageclass.storage.k8s.io/requests.storage`,
`<storage-class-name>.storageclass.storage.k8s.io/persistentvolumeclaims`

## Quota on object count -- [NAMES ONLY]

Syntax: `count/<resource>.<group>` for non-core API groups; `count/<resource>` for core
API group resources.

Countable resources include: `count/pods`, `count/persistentvolumeclaims`,
`count/services`, `count/secrets`, `count/configmaps`, `count/deployments.apps`,
`count/replicasets.apps`, `count/statefulsets.apps`, `count/jobs.batch`,
`count/cronjobs.batch`

## Quota and Cluster Capacity

**[VERBATIM, with an elision in the fetch -- marked]**

> "ResourceQuotas are independent of the cluster capacity[...]if you add nodes to your cluster, this does *not* automatically give each namespace the ability to consume more resources."

---

NOT IN THIS SNAPSHOT: quota scopes and scope selectors, priority-class quota, the
cross-namespace pod affinity quota, and the full countable-resource roster. All are above
associate tier.
"""

FILES["k8s-docs-limit-range-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/concepts/policy/limit-range/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/policy/limit-range.md"
fetched_at: "2026-08-24T18:57:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["limit-range", "resource-quota", "admission-control", "default-requests", "namespaced-vs-cluster-scoped"]
closes_gap: "ch-08 outline Open Question #3 (BLOCKING), second half. Previously nothing cached described LimitRange's min/max/default structure or its per-object scope."
---
# Limit Ranges

> **Extraction note.** All passages below are **[VERBATIM]**.

## What it is

> "A LimitRange is a policy to constrain the resource allocations (limits and requests) that you can specify for each applicable object kind (such as Pod or PersistentVolumeClaim) in a namespace."

## What a LimitRange provides

> "Enforce minimum and maximum compute resources usage per Pod or Container in a namespace."

> "Enforce minimum and maximum storage request per PersistentVolumeClaim in a namespace."

> "Enforce a ratio between request and limit for a resource in a namespace."

> "Set default request/limit for compute resources in a namespace and automatically inject them to Containers at runtime."

## When it applies

> "Kubernetes constrains resource allocations to Pods in a particular namespace whenever there is at least one LimitRange object in that namespace."

> "LimitRange validations occur only at Pod admission stage, not on running Pods. If you add or modify a LimitRange, the Pods that already exist in that namespace continue unchanged."

> "A LimitRange does not check the consistency of the default values it applies."

## Constraints on resource limits and requests

> "The administrator creates a LimitRange in a namespace."

> "Users create (or try to create) objects in that namespace, such as Pods or PersistentVolumeClaims."

> "First, the LimitRange admission controller applies default request and limit values for all Pods (and their containers) that do not set compute resource requirements."

> "Second, the LimitRange tracks usage to ensure it does not exceed resource minimum, maximum and ratio defined in any LimitRange present in the namespace."

> "If you attempt to create or update an object (Pod or PersistentVolumeClaim) that violates a LimitRange constraint, your request to the API server will fail with an HTTP status code `403 Forbidden` and a message explaining the constraint that has been violated."

> "If you add a LimitRange in a namespace that applies to compute-related resources such as `cpu` and `memory`, you must specify requests or limits for those values. Otherwise, the system may reject Pod creation."

> "If two or more LimitRange objects exist in the namespace, it is not deterministic which default value will be applied."

---

## What this snapshot licenses Chapter 8 sec.3 to assert

- The **contrast** is now fully sourced on both sides. ResourceQuota "limit[s] aggregate
  resource consumption per namespace"; a LimitRange constrains "each applicable object kind
  ... in a namespace."
- The **mutate-vs-reject echo of sec.2** is sourced: a LimitRange "automatically inject[s]"
  defaults into Containers, and a quota violation is "reject[ed] ... with HTTP status code
  `403 Forbidden`." That is `ch08-fig05`'s design requirement, in the sources' own words.
- The sec.3 Snag ("the Pod you get is not the Pod you wrote") rests on "automatically
  inject them to Containers at runtime" plus "does not check the consistency of the default
  values it applies."

NOT IN THIS SNAPSHOT: the YAML examples, the per-container vs per-Pod limit type
distinction in detail, and PersistentVolumeClaim storage limit examples.
"""

FILES["k8s-docs-node-status-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/reference/node/node-status/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/node/node-status.md"
fetched_at: "2026-08-24T19:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["node-conditions", "ready-condition", "memorypressure", "diskpressure", "pidpressure", "networkunavailable", "node-monitor-grace-period", "node-capacity", "node-allocatable", "cordon", "unschedulable-node"]
supersedes_note: "CITATION CORRECTION. k8s-docs-nodes-2026-08-23.md carries the node conditions table and the three-valued Ready description under source_url .../concepts/architecture/nodes/. As of 2026-08-24 the concept page no longer carries that table -- it links out to this reference page. Chapter 8 sec.4 should cite THIS file for conditions, Capacity/Allocatable and Info. The 08-23 file remains correct for node registration, cordon/drain/uncordon, heartbeats and the node controller."
closes_gap: "ch-08 outline Open Question #5 (node-monitor-grace-period has a documented default) and the previously unsourced sec.8 claim that cordon writes a SPEC field."
---
# Node Status (reference)

> **Extraction note.** All passages below are **[VERBATIM]**.

## What a Node's status contains

> "A Node's status contains the following information: * Addresses * Conditions * Capacity and Allocatable * Info * Declared Features"

## Addresses

> "The usage of these fields varies depending on your cloud provider or bare metal configuration. * HostName: The hostname as reported by the node's kernel. Can be overridden via the kubelet `--hostname-override` parameter. * ExternalIP: Typically the IP address of the node that is externally routable (available from outside the cluster). * InternalIP: Typically the IP address of the node that is routable only within the cluster."

## Conditions

> "The `conditions` field describes the status of all `Running` nodes. Examples of conditions include:"

| Node Condition | Description (verbatim) |
|---|---|
| `Ready` | "`True` if the node is healthy and ready to accept pods, `False` if the node is not healthy and is not accepting pods, and `Unknown` if the node controller has not heard from the node in the last `node-monitor-grace-period` (default is 50 seconds)" |
| `DiskPressure` | "`True` if pressure exists on the disk size---that is, if the disk capacity is low; otherwise `False`" |
| `MemoryPressure` | "`True` if pressure exists on the node memory---that is, if the node memory is low; otherwise `False`" |
| `PIDPressure` | "`True` if pressure exists on the processes---that is, if there are too many processes on the node; otherwise `False`" |
| `NetworkUnavailable` | "`True` if the network for the node is not correctly configured, otherwise `False`" |

> "In the Kubernetes API, a node's condition is represented as part of the `.status` of the Node resource."

## The cordon note -- load-bearing for sec.8

> "If you use command-line tools to print details of a cordoned Node, the Condition includes `SchedulingDisabled`. `SchedulingDisabled` is not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec."

## Capacity and Allocatable

> "Describes the resources available on the node: CPU, memory, and the maximum number of pods that can be scheduled onto the node. The fields in the capacity block indicate the total amount of resources that a Node has. The allocatable block indicates the amount of resources on a Node that is available to be consumed by normal Pods."

## Info

> "Describes general information about the node, such as kernel version, Kubernetes version (kubelet and kube-proxy version), container runtime details, and which operating system the node uses."

---

## Notes for drafting

1. **`node-monitor-grace-period` now has a documented default: 50 seconds.** The ch-08
   outline instructed sec.4 to name the parameter and state no number, because no cached
   source carried one, and added: "If a later fetch supplies a default, it may be added as
   an illustration, never as a rule." This is that fetch. Recommended handling: name the
   parameter, then give "(default 50 seconds)" as a dated illustration, never as the
   examinable fact.
2. **`SchedulingDisabled` is not an API Condition.** It is a client-side display artifact.
   This is a ready-made Snag for sec.4 and it directly supports sec.8: what `cordon`
   actually changes is `.spec`, which is the reader's own declaration, not `.status`, which
   the system writes. That is the Practice-Questions retrieval item ("spec field or status
   field, and how do you know?") sourced rather than inferred.
3. "Declared Features" is a fifth status field on the current page. NOT extracted -- it is
   above associate tier and appears in no CNCF competency list.
"""

FILES["k8s-docs-kubectl-cordon-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_cordon/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/kubectl/generated/kubectl_cordon/_index.md"
fetched_at: "2026-08-24T18:58:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["cordon", "unschedulable-node", "verb-resource-grammar"]
---
# kubectl cordon (generated reference)

> **Extraction note.** All passages below are **[VERBATIM]**.

## Synopsis

> "Mark node as unschedulable."

## Usage

> `kubectl cordon NODE`

## Examples

> `kubectl cordon foo`

---

Useful to sec.1 as the grammar instantiation: the synopsis is one verb, one resource type,
one name -- `kubectl` / `cordon` / `NODE` -- which is the four-slot shape with the flags
slot empty. The chapter's opening command, in the project's own reference form.
"""

FILES["k8s-docs-safely-drain-node-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/administer-cluster/safely-drain-node.md"
fetched_at: "2026-08-24T18:58:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["drain", "cordon", "uncordon", "api-initiated-eviction", "node-maintenance"]
scope_note: "The outline caps sec.4's drain treatment at one clause ('it evicts') and BANS teaching PodDisruptionBudgets and --ignore-daemonsets. Those sentences are transcribed here as evidence for the fact-accuracy audit, NOT as a licence to teach them. See the drafting note at the foot of this file."
---
# Safely Drain a Node

> **Extraction note.** All passages below are **[VERBATIM]**.

## What drain does

> "You can use `kubectl drain` to safely evict all of your pods from a node before you perform maintenance on the node (e.g. kernel upgrade, hardware maintenance, etc.). Safe evictions allow the pod's containers to gracefully terminate and will respect the PodDisruptionBudgets you have specified."

## DaemonSet-managed Pods

> "If there are pods managed by a DaemonSet, you will need to specify `--ignore-daemonsets` with `kubectl` to successfully drain the node."

## After the drain returns

> "Once it returns (without giving an error), you can power down the node (or equivalently, if on a cloud platform, delete the virtual machine backing the node)."

> "you need to run `kubectl uncordon <node name>` afterwards to tell Kubernetes that it can resume scheduling new pods onto the node."

## Not on this page

No sentence on this page states that `kubectl drain` cordons the node as part of its
operation. The page discusses marking nodes unschedulable and later uses
`kubectl uncordon`, but the cordon-as-part-of-drain step is not asserted in prose.
**Chapter 8 must not claim it from this source.**

---

## Drafting note -- a tension the author should know about

The Nodes concept page states that "Pods that are part of a DaemonSet tolerate being run on
an unschedulable Node." This page states that draining a node with DaemonSet-managed Pods
requires `--ignore-daemonsets`. Both are true and they are about different things --
tolerating an unschedulable node is a *scheduling* fact, needing the flag is a *drain*
fact -- but a sharp reader who holds both may feel a contradiction. The outline bans
teaching `--ignore-daemonsets`. If the author wants the tension defused, one clause in
sec.4 is the ceiling; otherwise leave it, since sec.4 only asserts the scheduling fact.
"""

FILES["k8s-docs-api-eviction-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/api-eviction/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/scheduling-eviction/api-eviction.md"
fetched_at: "2026-08-24T18:58:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["api-initiated-eviction", "drain", "node-controller"]
---
# API-initiated Eviction

> **Extraction note.** Passages marked **[VERBATIM]** are safe to cite.

**[VERBATIM]**

> "You can request eviction by calling the Eviction API directly, or programmatically using a client of the API server, like the `kubectl drain` command. This creates an `Eviction` object, which causes the API server to terminate the Pod."

> "Using the API to create an Eviction object for a Pod is like performing a policy-controlled `DELETE` operation on the Pod."

> "API-initiated evictions respect your configured `PodDisruptionBudgets` and `terminationGracePeriodSeconds`."

> "the API server performs admission checks and responds in one of the following ways"

---

NOT VERBATIM-CAPTURED: the enumerated response outcomes following that last sentence
(200 OK / 429 / 500) were returned only as a gloss and must not be quoted. The page draws
no explicit contrast with node-pressure eviction; node-pressure eviction appears only as a
"what's next" link.

**Why this file exists.** The cached Nodes page says the node controller triggers
"API-initiated eviction of all the Pods from the node if it stays unreachable," and sec.4
lists `api-initiated-eviction` as a concept. This snapshot supplies the definition of the
term the Nodes page uses without defining. It is also the sourced link between `drain` and
eviction: drain is a client of the Eviction API, which is one more instance of sec.8's
claim -- an administrative command is a write through the one door.
"""

FILES["k8s-docs-audit-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/debug/debug-cluster/audit.md"
fetched_at: "2026-08-24T18:59:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["auditing", "audit-policy", "audit-stages", "audit-backends"]
closes_gap: "ch-08 outline Open Question #4. Auditing was a page title with no cached definition; the option (a) fetch was recommended as free if Stage 2 was already in this doc tree. It was."
---
# Auditing

> **Extraction note.** Passages marked **[VERBATIM]** are safe to cite.

## Overview

**[VERBATIM]**

> "Kubernetes _auditing_ provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster."

> "Auditing allows cluster administrators to answer the following questions: what happened? when did it happen? who initiated it? on what did it happen? where was it observed? from where was it initiated? to where was it going?"

## Where audit records come from

**[VERBATIM]**

> "Audit records begin their lifecycle inside the kube-apiserver component. Each request on each stage of its execution generates an audit event."

## Stages

**[VERBATIM]**

- `RequestReceived` -- "The stage for events generated as soon as the audit handler receives the request"
- `ResponseStarted` -- "Once the response headers are sent, but before the response body is sent"
- `ResponseComplete` -- "The response body has been completed and no more bytes will be sent"
- `Panic` -- "Events generated when a panic occurred"

## Audit policy

**[VERBATIM]**

> "Audit policy defines rules about what events should be recorded and what data they should include."

The four audit **levels** are named on the page as `None`, `Metadata`, `Request` and
`RequestResponse`. **[NAMES ONLY]** -- their one-line definitions were not verbatim-captured
in this pass and must not be quoted. See research-manifest Gaps, G-8D.

## Backends

**[VERBATIM, lightly joined -- the bracketed conjunction is the fetch's, not the source's]**

> "Out of the box, the kube-apiserver provides two backends: Log backend, which writes events into the filesystem [and] Webhook backend, which sends events to an external HTTP API."

---

## Drafting note

The ch-08 outline caps auditing at one or two sentences in sec.2 and says the exam-relevant
fact is that it exists and what it records. This snapshot supports exactly that, plus one
better sentence than the outline expected: auditing lives **inside the kube-apiserver** and
every request generates an event at every stage of its execution. That is the same
single-door architecture stated a fourth way, and it costs one clause. The stages, the
policy levels and the backends are all above what the outline budgets -- cached for the
audit, not for the draft.
"""

FILES["k8s-docs-reserve-compute-resources-2026-08-24.md"] = """---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/administer-cluster/reserve-compute-resources.md"
fetched_at: "2026-08-24T18:59:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["node-capacity", "node-allocatable", "kube-reserved", "system-reserved", "eviction-threshold"]
closes_gap: "ch-08 outline Open Question #6, at the recommended option (b) level. Chapter 7 line 408 promised 'what makes Capacity and Allocatable differ, and how it is configured'. The reservations are now nameable with verbatim definitions."
supersedes_note: "COMPLEMENTS k8s-docs-node-allocatable-2026-08-24.md, which is a deliberately shallow extraction of the SAME page for Chapter 7. Two snapshots share this source_url by design: the earlier file carries what Chapter 7 needed, this one carries the reservation model Chapter 7 deferred to Chapter 8."
---
# Reserve Compute Resources for System Daemons

> **Extraction note.** All passages below are **[VERBATIM]**.

## Why Capacity is not the number that matters

> "Kubernetes nodes can be scheduled to `Capacity`. Pods can consume all the available capacity on a node by default. This is an issue because nodes typically run quite a few system daemons that power the OS and Kubernetes itself."

## Node Allocatable

> "'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods."

## Kube Reserved

> "`kubeReserved` is meant to capture resource reservation for kubernetes system daemons like the `kubelet`, `container runtime`, etc. It is not meant to reserve resources for system daemons that are run as pods."

## System Reserved

> "`systemReserved` is meant to capture resource reservation for OS system daemons like `sshd`, `udev`, etc."

The section additionally states that `systemReserved` should "reserve `memory` for the
`kernel`", and that "reserving resources for user login sessions is also recommended."

## Eviction Thresholds

> "By reserving some memory via `evictionHard` setting, the `kubelet` attempts to evict pods whenever memory availability on the node drops below the reserved value."

---

## The arithmetic is still not extractable -- re-confirmed 2026-08-24

There is **no textual statement or equation** on this page relating Capacity,
`kube-reserved`, `system-reserved`, `eviction-threshold` and Allocatable. The relationship
is published only as an image (`node-capacity.svg`) with no text equivalent. This
re-confirms the extraction note in `k8s-docs-node-allocatable-2026-08-24.md`.

**Chapter 8 sec.4 must not state an arithmetic relationship.** What it may now say, and
what discharges the Chapter 7 promise at option (b): nodes run OS system daemons and
Kubernetes system daemons; `kube-reserved` and `system-reserved` are the reservations that
account for them; Allocatable is what is left for Pods. That is the "what makes the two
differ" half of the promise, honestly paid, with the "how it is configured" half left at
the two flag names -- which is where the associate tier stops.
"""

MANIFEST = """# Research Manifest -- KCNA Chapter 8

Stage 2 (Source Snapshot Research) for **Chapter 8 -- Standing the Watch**, competency D1.2.
Run 2026-08-24. Ten new snapshots; both of the outline's BLOCKING gaps are closed, plus
three Open Questions the outline had left for the author.

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-controlling-access-2026-08-24.md` | Kubernetes project | D1.2 | api-access-gates, authentication, authorization, admission-control, mutating-admission, auditing, api-request-stages |
| `k8s-docs-admission-controllers-2026-08-24.md` | Kubernetes project | D1.2 | admission-controller, mutating-admission, validating-admission, dynamic-admission-control, resource-quota, limit-range, noderestriction |
| `k8s-docs-resource-quotas-2026-08-24.md` | Kubernetes project | D1.2 | resource-quota, namespaced-vs-cluster-scoped, admission-control, compute-resource-quota, object-count-quota, storage-quota |
| `k8s-docs-limit-range-2026-08-24.md` | Kubernetes project | D1.2 | limit-range, resource-quota, admission-control, default-requests |
| `k8s-docs-node-status-2026-08-24.md` | Kubernetes project | D1.2 | node-conditions, ready-condition, memorypressure, diskpressure, pidpressure, networkunavailable, node-monitor-grace-period, node-capacity, node-allocatable, cordon |
| `k8s-docs-kubectl-cordon-2026-08-24.md` | Kubernetes project | D1.2 | cordon, unschedulable-node, verb-resource-grammar |
| `k8s-docs-safely-drain-node-2026-08-24.md` | Kubernetes project | D1.2 | drain, cordon, uncordon, api-initiated-eviction, node-maintenance |
| `k8s-docs-api-eviction-2026-08-24.md` | Kubernetes project | D1.2 | api-initiated-eviction, drain, node-controller |
| `k8s-docs-audit-2026-08-24.md` | Kubernetes project | D1.2 | auditing, audit-policy, audit-stages, audit-backends |
| `k8s-docs-reserve-compute-resources-2026-08-24.md` | Kubernetes project | D1.2 | node-capacity, node-allocatable, kube-reserved, system-reserved, eviction-threshold |

## Already cached and load-bearing for this chapter

Verified present and adequate; no re-fetch needed.

| Snapshot | Serves |
|---|---|
| `k8s-docs-kubectl-overview-2026-08-23.md` | sec.1 in full -- the four-slot grammar, case-sensitivity asymmetry, flag/env precedence, `$HOME/.kube/config`, the in-cluster detection triple, the ServiceAccount-namespace behaviour, the operations table |
| `k8s-docs-nodes-2026-08-23.md` | sec.4 -- self-registration vs manual creation, the `metadata.name` validity check, DNS-subdomain naming, cordon/drain/uncordon, DaemonSet tolerance, the two heartbeat forms, the node controller's three jobs. **See G-8B on the conditions table** |
| `k8s-docs-cluster-administration-2026-08-23.md` | sec.5 planning questions; sec.2 securing-a-cluster page titles |
| `k8s-docs-setup-tooling-2026-08-23.md` | sec.5 -- minikube, kind, kubeadm, k3s, managed/turnkey, the container-runtime requirement |
| `k8s-version-skew-policy-2026-08-23.md` | sec.6 -- all five skew rules, semver, three supported minors, ~1 year patch support |
| `k8s-releases-cadence-2026-08-23.md` | sec.6 -- three minor releases a year, ~15 weeks, monthly patches, the dated roster |
| `k8s-docs-etcd-backup-2026-08-23.md` | sec.7 -- disaster scenario, snapshot contents, `etcdctl snapshot save`, `etcdutl snapshot restore` |
| `k8s-docs-etcd-access-control-2026-08-24.md` | sec.7 -- "Access to etcd is equivalent to root permission in the cluster" |
| `k8s-docs-namespaces-2026-08-23.md` | sec.3 -- namespaces divide cluster resources via resource quota; namespaced vs cluster-scoped |
| `k8s-docs-cloud-native-security-2026-08-23.md` | sec.3 -- the ResourceQuota/LimitRange purpose pair; sec.2 -- API access authn/authz |
| `k8s-docs-control-plane-node-communication-2026-08-24.md` | sec.2 -- hub-and-spoke, all API usage terminates at the API server, TLS bootstrapping |
| `k8s-docs-assign-pod-node-2026-08-23.md` | sec.2 -- NodeRestriction and the `node-restriction.kubernetes.io/` prefix |
| `k8s-docs-taints-tolerations-depth-2026-08-24.md` | sec.4/sec.8 -- "The node controller automatically taints a Node when certain conditions are true"; the built-in taint key list |
| `k8s-docs-daemonset-2026-08-24.md` | sec.4 -- the DaemonSet toleration table including `node.kubernetes.io/unschedulable: NoSchedule` |
| `k8s-docs-node-allocatable-2026-08-24.md` | sec.4 -- Allocatable definition and the scheduler's use of it |
| `k8s-docs-pod-security-standards-2026-08-23.md` | sec.2 -- PSA named as a built-in admission controller, one clause only |
| `k8s-docs-extending-kubernetes-2026-08-23.md` | sec.2 -- dynamic admission control as an API-access extension point; webhooks as a point of failure |

## Gaps

**G-8A -- `kubectl cordon` is not connected to the `node.kubernetes.io/unschedulable` taint
by any single source. AFFECTS A STATED ANSWER KEY.**

Bearings #2 item 1, as specified in the outline, asks *"What command applies it"* -- the
taint -- with the correct answer `kubectl cordon`. **No cached or newly fetched source
asserts that.** What is now sourced is a two-link chain across two files:

1. `k8s-docs-node-status-2026-08-24.md`: "cordoned nodes are marked Unschedulable in their
   spec."
2. `k8s-docs-taints-tolerations-depth-2026-08-24.md`: "The node controller automatically
   taints a Node when certain conditions are true" -- and its key list includes
   `node.kubernetes.io/unschedulable`.

The reference page's own description of that taint pulls the other way: "The taint will be
added to a node when initializing the node to avoid race condition," which is about node
startup, not cordoning.

**Three options.** (a) Reword the item to ask what command *marks a node unschedulable* --
answer `kubectl cordon`, fully sourced, and the Chapter 7 identity still lands via the spec
field. (b) Keep the item and let the answer key show the two-link chain explicitly, which
is honest and is arguably a better item. (c) Fetch
`kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/` in full and look for
a sentence tying `spec.unschedulable` to the taint. **Recommendation: (a).** sec.8's claim
does not need the taint link -- "cordon writes a spec field, and the scheduler was already
watching" is stronger and is now fully sourced.

**G-8B -- citation drift in `k8s-docs-nodes-2026-08-23.md`. Not a content gap.**

That snapshot carries the node conditions table and the three-valued `Ready` description
under `source_url: https://kubernetes.io/docs/concepts/architecture/nodes/`. A re-fetch of
that page on 2026-08-24 shows the conditions detail is no longer there -- the concept page
links out to `/docs/reference/node/node-status/`. The facts are unchanged and are now
cached with the correct attribution in `k8s-docs-node-status-2026-08-24.md`. **sec.4 should
cite the new file for conditions, Capacity/Allocatable and Info**, and keep citing the
08-23 file for registration, cordon/drain/uncordon, heartbeats and the node controller. A
downstream fact-accuracy audit checking the 08-23 URL would otherwise report a false
positive.

**G-8C -- ResourceQuota per-row descriptions not verbatim-verified.** The compute, storage
and object-count resource NAMES are transcribed from the source's tables and are safe. The
description cells ("Across all pods in a non-terminal state, the sum of CPU limits cannot
exceed this value," etc.) were not verbatim-captured. sec.3 may enumerate what a quota can
count; it must not quote a row description as a source sentence.

**G-8D -- audit level definitions not captured.** `None`, `Metadata`, `Request` and
`RequestResponse` are confirmed present as level names; their one-line meanings were not
verbatim-captured. This is below the outline's budget for auditing anyway (one or two
sentences) so no re-fetch is recommended.

**G-8E -- Capacity-to-Allocatable arithmetic remains unextractable.** Re-confirmed on
2026-08-24 against the reservation page: the relationship is published only as
`node-capacity.svg`, with no text equivalent. sec.4 must name `kube-reserved` and
`system-reserved` without stating an equation.

**G-8F -- deliberately not fetched, recorded so the audit does not read these as oversights:**
Konnectivity and SSH tunnels (outline Open Q #7 -- above tier, and SSH tunnels are
deprecated); feature gates and the alpha/beta/stable stages (Open Q #8 -- Chapter 17 owns
them alongside KEPs); RBAC Roles and bindings, Pod Security Standards detail, encryption at
rest (Chapter 12); `kubectl top`, `events`, `port-forward`, `debug` (Chapters 13 and 16);
quota scopes, scope selectors and priority-class quota (above associate tier); kubeadm
upgrade runbooks (not in the curriculum).

## Notes for the author

**1. Open Question #2 is closed, and the sourcing is better than the outline hoped.** sec.2's
Fixed Point is fully citable: the gates are sequential, admission runs after authorization,
admission runs before persistence ("Once a request passes all admission controllers, it is
validated ... and then written to the object store"), and admission "can modify or reject
requests." A sharper Navigational Hazard than the outline planned is now available for free
-- the two gates differ in their *quorum rule*, not just their subject: authorization is
**any module approves and the request proceeds**; admission is **any module rejects and the
request is refused immediately**. The source draws the contrast itself. That is a better
discrimination than "authorization has no opinion about contents," and both can be used.

**2. Open Question #3 is closed on both halves.** sec.3 can now carry: quota "limit[s]
aggregate resource consumption per namespace"; violations are rejected with `403 Forbidden`;
in a quota'd namespace every new Pod **must** specify requests or limits; a LimitRange
"automatically inject[s]" defaults; LimitRange "validations occur only at Pod admission
stage, not on running Pods." The section as specified is now fully drafted-from-source and
can carry both published cross-bearings. The Practice allocation may rise from 2 to 3 as
the outline anticipated.

**3. `ch08-fig05`'s design requirement is now in the sources' own words.** The outline says
the two panels "must fail differently" -- left rejects, right modifies. The sources say
exactly that: quota "rejects that request with HTTP status code `403 Forbidden`"; LimitRange
"automatically inject[s] them to Containers at runtime." The figure brief can quote the
mechanism rather than assert the contrast.

**4. Open Question #5 is resolved the other way.** `node-monitor-grace-period` has a
documented default of **50 seconds** on the node-status reference. The outline's own rule
applies: illustration, never rule. Recommend sec.4 names the parameter, gives the default
parenthetically and dated, and keeps the examinable fact at "Unknown means the control plane
has not heard from the node."

**5. Open Question #6 pays at option (b), as recommended, and gets a bonus.** `kube-reserved`
and `system-reserved` now have verbatim definitions. The bonus is the *motivation* sentence,
which is what Chapter 7 actually promised: "Pods can consume all the available capacity on a
node by default. This is an issue because nodes typically run quite a few system daemons that
power the OS and Kubernetes itself." Two sentences discharge the promise honestly. The
arithmetic stays out.

**6. sec.8's strongest demonstration is no longer an inference.** "cordoned nodes are marked
Unschedulable in their spec" is the sentence the Zenith needs, and it also converts the
planned Practice retrieval item -- *"`kubectl cordon` writes something. Is it a `spec` field
or a `status` field, and how do you know?"* -- from a reasoned answer into a sourced one. The
adjacent sentence, "`SchedulingDisabled` is not a Condition in the Kubernetes API," is a
ready-made Snag for sec.4: the thing `kubectl` prints is not a thing the API has.

**7. Open Question #4: option (a) landed and was free.** Auditing now has a real definition,
the seven questions it answers, its location inside the kube-apiserver, four stages and two
backends. The outline's recommendation was (b) unless the fetch was cheap; it was in the same
doc tree. Recommend using the definition plus one clause -- auditing lives *inside the API
server* and every request generates an event at every stage -- because that is the
single-door architecture stated a fourth way and it costs nothing. The stages, levels and
backends are above budget.

**8. `kubectl drain` and DaemonSets carry a tension worth knowing about.** The Nodes page says
DaemonSet Pods tolerate an unschedulable node; the drain task page says draining a node with
DaemonSet Pods requires `--ignore-daemonsets`. Both are true and they concern different
mechanisms. The outline bans teaching the flag, so sec.4 is safe as planned -- but a reader
who has met both facts elsewhere may feel a contradiction. Flagging only; no change
recommended.

**9. sec.6's dated data is unchanged.** The version-skew and cadence snapshots still name
1.36 / 1.35 / 1.34 with EOL dates. The outline's discipline stands: teach the rule, illustrate
with the numbers marked as of the snapshot date, and let no Practice Question turn on a
specific minor version.

**10. No source conflicts were found.** Where two pages cover the same fact -- the Nodes
concept page and the node-status reference on conditions, the two etcd extractions, the two
extractions of the reservation page -- they agree, and each pair is cross-noted in
`supersedes_note` / `scope_note` frontmatter so a downstream audit can see the relationship
rather than reading it as duplication.
"""

def main():
    os.makedirs(SRC, exist_ok=True)
    os.makedirs(MAN, exist_ok=True)
    for name, body in FILES.items():
        path = os.path.join(SRC, name)
        with open(path, "w", encoding="utf-8", newline="\n") as fh:
            fh.write(body)
        print("wrote %s (%d bytes)" % (path, len(body.encode("utf-8"))))
    mpath = os.path.join(MAN, "research-manifest.md")
    with open(mpath, "w", encoding="utf-8", newline="\n") as fh:
        fh.write(MANIFEST)
    print("wrote %s (%d bytes)" % (mpath, len(MANIFEST.encode("utf-8"))))

if __name__ == "__main__":
    main()
```

## Summary of the stage

**Fetched, all from kubernetes.io (authority tier 2, the project's own docs):** controlling-access, admission-controllers, resource-quotas, limit-range, node-status, kubectl_cordon, safely-drain-node, api-eviction, audit, reserve-compute-resources. Ten snapshots.

**Gaps declared:** five, detailed in the manifest. The one that changes authored content is **G-8A** — Bearings #2 item 1's answer key asserts `kubectl cordon` applies the `unschedulable` taint, which no single source supports. My recommendation is to reword the question to ask what marks a node unschedulable; §8's argument is stronger without the taint link anyway, now that the spec-field sentence is sourced.

**Not done:** nothing was written to disk. Every file above is complete and ready to land — say the word and I'll run the script, or run it yourself.
# Research Manifest -- KCNA Chapter 8

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

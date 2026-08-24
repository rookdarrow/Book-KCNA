I now have the full picture. Stage 2 has no `Write` tool by design (`executor.py:157` grants only `WebFetch,WebSearch,Read`); snapshots reach `sources/` via `harvest_research_snapshots()` (`orchestrator.py:173`), which extracts fenced blocks from the manifest. My stdout *is* the artifact, so the manifest below carries the snapshots in harvest format.

# Research Manifest — KCNA Chapter 3

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-control-plane-node-communication-2026-08-24.md` **(new)** | Kubernetes project | D1.1 | api-server-as-front-end, hub-and-spoke-api-pattern, control-plane-node-communication |
| `k8s-docs-cluster-addons-2026-08-24.md` **(new)** | Kubernetes project | D1.1 | addons, cluster-dns, coredns, optional-components, kube-proxy-replacement |
| `k8s-docs-etcd-access-control-2026-08-24.md` **(new)** | Kubernetes project | D1.1 | etcd, etcd-access, api-server-as-front-end |
| `k8s-docs-dns-cluster-addon-2026-08-24.md` **(new)** | Kubernetes project | D1.1 | cluster-dns, addons, addon-manager |
| `etcd-io-what-is-etcd-2026-08-24.md` **(new)** | etcd project (CNCF Graduated) | D1.1 | etcd, strong-consistency |
| `k8s-docs-overview-2026-08-23.md` (cached) | Kubernetes project | D1.1 | deployment-eras, what-kubernetes-provides, what-kubernetes-is-not, orchestration-technical-definition, composable-control-processes, self-healing, automatic-bin-packing |
| `k8s-docs-cluster-architecture-2026-08-23.md` (cached) | Kubernetes project | D1.1 | cluster, control-plane, worker-node, all 8 components, highly-available-control-plane, node-controller, job-controller, endpointslice-controller, serviceaccount-controller |
| `k8s-docs-components-2026-08-23.md` (cached) | Kubernetes project | D1.1 | control-plane-components, node-components, addons |
| `k8s-docs-controllers-2026-08-23.md` (cached) | Kubernetes project | D1.1 | controller, control-loop, reconciliation, desired-state, current-state, control-via-api-server, direct-control |
| `k8s-history-ten-years-2026-08-23.md` (cached) | Kubernetes project blog | D1.1 | kubernetes-origin, borg, omega, helmsman-etymology, cncf-first-project |
| `cncf-who-we-are-2026-08-23.md` (cached) | CNCF | D1.1 | cncf-provenance (Linux Foundation) |
| `k8s-docs-kube-scheduler-2026-08-23.md` (cached) | Kubernetes project | D1.1 | kube-scheduler binding boundary (§2 scope note) |
| `k8s-docs-containers-2026-08-23.md` (cached) | Kubernetes project | D1.1 | container-runtime, cri, image-immutability (retrieval anchors) |

### A1 · `k8s-docs-control-plane-node-communication-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/architecture/control-plane-node-communication/"
fetched_at: "2026-08-24T03:10:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts", "D1 Administration"]
concepts_covered: ["api-server-as-front-end", "hub-and-spoke-api-pattern", "control-plane-node-communication", "kube-apiserver", "kubelet", "kube-proxy", "konnectivity", "ssh-tunnels"]
---
# Communication between Nodes and the Control Plane (kubernetes.io/docs/concepts/architecture/control-plane-node-communication/)

> **Snapshot note.** Transcribed from the page's canonical Markdown source at
> github.com/kubernetes/website/blob/main/content/en/docs/concepts/architecture/control-plane-node-communication.md
> and cross-checked against the rendered page. Wording is verbatim; only the source file's hard
> line wrapping has been reflowed into paragraphs, with Hugo front matter and shortcodes removed.
> The "SSH tunnels" and "Konnectivity service" sections are retained for completeness but are
> out of scope for Chapter 3 - they belong to the Chapter 8 API-access material.

## Node to Control Plane

Kubernetes has a "hub-and-spoke" API pattern. All API usage from nodes (or the pods they run) terminates at the API server. None of the other control plane components are designed to expose remote services. The API server is configured to listen for remote connections on a secure HTTPS port (typically 443) with one or more forms of client authentication enabled. One or more forms of authorization should be enabled, especially if anonymous requests or service account tokens are allowed.

Nodes should be provisioned with the public root certificate for the cluster such that they can connect securely to the API server along with valid client credentials. A good approach is that the client credentials provided to the kubelet are in the form of a client certificate. See kubelet TLS bootstrapping for automated provisioning of kubelet client certificates.

Pods that wish to connect to the API server can do so securely by leveraging a service account so that Kubernetes will automatically inject the public root certificate and a valid bearer token into the pod when it is instantiated. The `kubernetes` service (in `default` namespace) is configured with a virtual IP address that is redirected (via kube-proxy) to the HTTPS endpoint on the API server.

The control plane components also communicate with the API server over the secure port.

As a result, the default operating mode for connections from the nodes and pod running on the nodes to the control plane is secured by default and can run over untrusted and/or public networks.

## Control plane to node

There are two primary communication paths from the control plane (the API server) to the nodes. The first is from the API server to the kubelet process which runs on each node in the cluster. The second is from the API server to any node, pod, or service through the API server's _proxy_ functionality.

### API server to kubelet

The connections from the API server to the kubelet are used for:

* Fetching logs for pods.
* Attaching (usually through `kubectl`) to running pods.
* Providing the kubelet's port-forwarding functionality.

These connections terminate at the kubelet's HTTPS endpoint. By default, the API server does not verify the kubelet's serving certificate, which makes the connection subject to man-in-the-middle attacks and **unsafe** to run over untrusted and/or public networks.

To verify this connection, use the `--kubelet-certificate-authority` flag to provide the API server with a root certificate bundle to use to verify the kubelet's serving certificate.

If that is not possible, use SSH tunneling between the API server and kubelet if required to avoid connecting over an untrusted or public network.

Finally, Kubelet authentication and/or authorization should be enabled to secure the kubelet API.

### API server to nodes, pods, and services

The connections from the API server to a node, pod, or service default to plain HTTP connections and are therefore neither authenticated nor encrypted. They can be run over a secure HTTPS connection by prefixing `https:` to the node, pod, or service name in the API URL, but they will not validate the certificate provided by the HTTPS endpoint nor provide client credentials. So while the connection will be encrypted, it will not provide any guarantees of integrity. These connections **are not currently safe** to run over untrusted or public networks.

### SSH tunnels

Kubernetes supports SSH tunnels to protect the control plane to nodes communication paths. In this configuration, the API server initiates an SSH tunnel to each node in the cluster (connecting to the SSH server listening on port 22) and passes all traffic destined for a kubelet, node, pod, or service through the tunnel. This tunnel ensures that the traffic is not exposed outside of the network in which the nodes are running.

SSH tunnels are currently deprecated, so you shouldn't opt to use them unless you know what you are doing. The Konnectivity service is a replacement for this communication channel.

### Konnectivity service

As a replacement to the SSH tunnels, the Konnectivity service provides TCP level proxy for the control plane to cluster communication. The Konnectivity service consists of two parts: the Konnectivity server in the control plane network and the Konnectivity agents in the nodes network. The Konnectivity agents initiate connections to the Konnectivity server and maintain the network connections. After enabling the Konnectivity service, all control plane to nodes traffic goes through these connections.
```

**This closes the outline's one blocking gap (Open question #2)** — but not on the exact terms §5 assumed. See Notes #1 and #2 below before drafting §5 or commissioning `ch03-fig04`.

### A2 · `k8s-docs-cluster-addons-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/cluster-administration/addons/"
fetched_at: "2026-08-24T03:12:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["addons", "cluster-dns", "coredns", "optional-components", "kube-proxy-replacement", "dashboard"]
---
# Installing Addons (kubernetes.io/docs/concepts/cluster-administration/addons/)

> **Snapshot note.** Transcribed verbatim from the page's canonical Markdown source
> (github.com/kubernetes/website .../content/en/docs/concepts/cluster-administration/addons.md).
> The "Networking and Network Policy" list is long and mostly out of scope for Chapter 3; it has
> been trimmed to the entries that bear on kube-proxy optionality, with the elision marked.
> All retained text is verbatim, including original link syntax and emphasis (none added).

Add-ons extend the functionality of Kubernetes.

This page lists some of the available add-ons and links to their respective installation instructions. The list does not try to be exhaustive.

## Networking and Network Policy

[Entries for ACI, Antrea, Canal, CNI-Genie, Contiv, Contrail, Gateway API, Knitter, kube-router, Multus, OVN-Kubernetes, Nodus, NSX-T, Nuage, Romana, Spiderpool, Terway and Weave Net trimmed as out of scope for Chapter 3 - see the source URL for the full list.]

* [Calico](https://www.tigera.io/project-calico/) is a networking and network policy provider. Calico supports a flexible set of networking options so you can choose the most efficient option for your situation, including non-overlay and overlay networks, with or without BGP. Calico uses the same engine to enforce network policy for hosts, pods, and (if using Istio & Envoy) applications at the service mesh layer.
* [Cilium](https://github.com/cilium/cilium) is a networking, observability, and security solution with an eBPF-based data plane. Cilium provides a simple flat Layer 3 network with the ability to span multiple clusters in either a native routing or overlay/encapsulation mode, and can enforce network policies on L3-L7 using an identity-based security model that is decoupled from network addressing. Cilium can act as a replacement for kube-proxy; it also offers additional, opt-in observability and security features. Cilium is a [CNCF project at the Graduated level](https://www.cncf.io/projects/cilium/).
* [Flannel](https://github.com/flannel-io/flannel#deploying-flannel-manually) is an overlay network provider that can be used with Kubernetes.

## Service Discovery

* [CoreDNS](https://coredns.io) is a flexible, extensible DNS server which can be [installed](https://github.com/coredns/helm) as the in-cluster DNS for pods.

## Visualization & Control

* [Dashboard](https://github.com/kubernetes/dashboard#kubernetes-dashboard) is a dashboard web interface for Kubernetes.
* [Headlamp](https://headlamp.dev/) is an extensible Kubernetes UI that can be deployed in-cluster or used as a desktop application.

## Infrastructure

* [KubeVirt](https://kubevirt.io/user-guide/#/installation/installation) is an add-on to run virtual machines on Kubernetes. Usually run on bare-metal clusters.
* The [node problem detector](https://github.com/kubernetes/node-problem-detector) runs on Linux nodes and reports system issues as either [Events](/docs/reference/kubernetes-api/cluster-resources/event-v1/) or [Node conditions](/docs/concepts/architecture/nodes/#condition).

## Instrumentation

* [kube-state-metrics](/docs/concepts/cluster-administration/kube-state-metrics)

## Legacy Add-ons

There are several other add-ons documented in the deprecated [cluster/addons](https://git.k8s.io/kubernetes/cluster/addons) directory.

Well-maintained ones should be linked to here. PRs welcome!
```

The Cilium entry is the payoff here: *"Cilium can act as a replacement for kube-proxy"* is a named, documented instance of the kube-proxy optionality condition the architecture page states abstractly. That upgrades §4's Navigational Hazard and Bearings #2 item 1 from "the docs say a plugin could do this" to a concrete example — without naming a kube-proxy *mode*, so the Chapter 9 scope boundary holds.

### A3 · `k8s-docs-etcd-access-control-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/"
fetched_at: "2026-08-24T03:14:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Administration"]
concepts_covered: ["etcd", "etcd-access", "api-server-as-front-end", "control-plane"]
---
# Operating etcd clusters for Kubernetes - definition and access control (kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

> **Snapshot note.** This snapshot COMPLEMENTS and does not supersede
> `k8s-docs-etcd-backup-2026-08-23.md`, which covers the backup/restore portion of the SAME page.
> Two snapshots share this source_url by design: the 08-23 file carries the Chapter 8
> backup material, this 08-24 file carries the two sentences Chapter 3 sec.2/sec.5 depend on.
> Only sentences verified character-for-character against the rendered page are transcribed here.
> The page's TLS configuration guidance (peer/client certs, --client-cert-auth, --trusted-ca-file)
> was NOT transcribed - it is Chapter 8 material and was not verbatim-verified in this pass.

Opening definition:

"etcd is a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data."

From the securing/access-control guidance:

"Access to etcd is equivalent to root permission in the cluster so ideally only the API server should have access to it."
```

### A4 · `k8s-docs-dns-cluster-addon-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/"
fetched_at: "2026-08-24T03:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["cluster-dns", "addons", "addon-manager", "coredns"]
---
# Customizing DNS Service - cluster DNS as a built-in addon (kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/)

> **Snapshot note.** Narrow-scope snapshot. Only the introductory sentence bearing on Chapter 3
> Open question #8 (is cluster DNS effectively mandatory?) was transcribed, verified
> character-for-character against the rendered page. The remainder of the page is CoreDNS
> Corefile configuration, which is out of scope for Chapter 3 and Chapter 9.

"DNS is a built-in Kubernetes service launched automatically using the _addon manager_ [cluster add-on](https://github.com/kubernetes/kubernetes/blob/master/cluster/addons/addon-manager/README.md)."

The page's prerequisites additionally assume CoreDNS is already present in the cluster.
```

### A5 · `etcd-io-what-is-etcd-2026-08-24.md` (new)
```markdown
---
source_url: "https://etcd.io/"
fetched_at: "2026-08-24T03:16:00-0400"
authority: "etcd project (CNCF Graduated project) - official project site"
objectives_covered: ["D1.1"]
concepts_covered: ["etcd", "strong-consistency", "distributed-key-value-store"]
---
# What is etcd (etcd.io)

> **Snapshot note.** Fetched to address Chapter 3 Open question #9 (how much depth does the book
> owe on the word "consistent"?). This is the etcd project's own definition, and it is a DIFFERENT
> and slightly stronger formulation than the Kubernetes docs use ("consistent and highly-available
> key value store"). See the manifest Gaps section: neither source defines strong consistency in
> reader-facing terms, so any gloss on what consistency buys the reader is authorial.

"etcd is a strongly consistent, distributed key-value store that provides a reliable way to store data that needs to be accessed by a distributed system or cluster of machines."
```

## Gaps

Three items in the outline remain wholly or partly unsourceable. **The drafting stage must not manufacture facts for any of these.**

**G-A. "Operating system" vs "operating system kernel" (Open question #7) — UNSOURCED. Unchanged after this pass.**
`kubernetes.io/docs/concepts/overview/` says only *"containers ... have relaxed isolation properties to share the Operating System (OS) among the applications."* I searched for a Kubernetes-authored sentence using "kernel" in this sense and found none: `kubernetes.io/docs/concepts/windows/intro/` returned NOT PRESENT, and the cached `k8s-docs-containers-2026-08-23.md` does not use the word. **The book's sharpening to "kernel" is technically correct but is authorial precision, not documented fact.** Chapter 3 §1 must therefore either quote "Operating System (OS)" verbatim when citing, or make the sharpening visible as the book's own gloss. It cannot be presented as what the documentation says. This is now the third chapter to hit it and it is still open.

**G-B. A reader-facing gloss on etcd "consistent" (Open question #9) — PARTIALLY SOURCED.**
Sourceable: "consistent and highly-available key value store" (Kubernetes) and "strongly consistent, distributed key-value store that provides a reliable way to store data that needs to be accessed by a distributed system or cluster of machines" (etcd.io). **Not sourceable:** the recommended sentence "every component reads the same answer." I checked `etcd.io/docs/v3.5/learning/why/` specifically for a definition of strong/sequential consistency in those terms — NOT PRESENT; the page mentions "Linearizable Reads" only in a comparison table, with no sentence-length definition. Recommend the author write the gloss as plain-language explanation clearly framed as explanation, and cite etcd.io for "strongly consistent." Ceiling recommendation in the outline (no quorum, no Raft) is sound — nothing in the cached set supports going deeper anyway.

**G-C. "Cluster DNS is effectively mandatory" (Open question #8) — PARTIALLY SOURCED, better than before.**
Now sourceable: *"DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on."* That supports "built-in" and "launched automatically," which is most of what §4 wanted. **Still not sourceable:** "almost every cluster ships it" as an empirical claim. Note the current addons page lists CoreDNS under *Service Discovery* with no default/mandatory language, so the addons page alone will not carry this. Recommend §4 use the built-in/launched-automatically framing and drop the practice claim, or mark it as the author's observation.

**Not gaps** (confirmed adequately sourced, listed to save the drafting stage a re-check): all eight component names and their one-job descriptions; kube-proxy and cloud-controller-manager optionality; the controller-manager one-binary/one-process fact; the four named built-in controllers; the full control-loop treatment including thermostat, Job worked example, direct control, and the never-stable-state claim; the deployment eras; the what-Kubernetes-provides and what-Kubernetes-is-not lists including the full orchestration disclaimer; Borg/Omega/Go/2014-06-06/DockerCon/v1.0/CNCF-first-project/helmsman/K8s numeronym; the scheduler-selects-and-binds vs kubelet-starts boundary.

## Notes for the author

**1. §5's central claim is now sourced, but the two halves are sourced at different strengths — and the difference should shape the wording.**

- *"Components do not talk to each other directly"* — **strongly sourced.** "None of the other control plane components are designed to expose remote services" is close to an architectural invariant, and "All API usage from nodes (or the pods they run) terminates at the API server" plus "The control plane components also communicate with the API server over the secure port" completes it. §5 can state this flatly.
- *"Only the API server talks to etcd"* — **sourced as a recommendation, not an invariant.** The exact sentence is "Access to etcd is equivalent to root permission in the cluster so ideally only the API server should have access to it." The word is *ideally*. This is security guidance about how a cluster should be configured, not a statement that nothing else can reach etcd. §5 and the `ch03-fig04` caption should say the API server is the component that reads and writes etcd and that anything else with etcd access holds root-equivalent power — which is truer, more useful, and sets up Chapter 12's encryption-at-rest decision better than an absolute would.

**2. `ch03-fig04` needs a scope qualifier, and this is the most consequential finding in this pass.** The outline specifies the figure's pedagogy as the absent arrows — "nothing from scheduler to kubelet, nothing between nodes, nothing bypassing the API server to etcd." The scheduler→kubelet and node→node absences are correct and now well sourced. **But the newly fetched page documents two real control-plane→node paths**: API server → kubelet (for pod logs, `kubectl attach`, and port-forwarding) and API server → node/pod/service via the API server's proxy functionality. A figure captioned "nothing flows outward from the hub" would be factually wrong, and Chapter 13's debugging material will contradict it when `kubectl logs` appears. Recommend scoping the figure and §5 explicitly to the **state/API path** — how desired state gets in and how components learn about it — and adding one sentence acknowledging that the API server also opens connections to kubelets to serve logs and exec, cross-beared to Ch 13. The Zenith survives this intact: its claim is that no component *directs* another, and an API server fetching logs on a user's behalf is not direction.

**3. The Zenith's narrow claim is now directly quotable.** Beyond the overview page's orchestration passage, "None of the other control plane components are designed to expose remote services" is an unusually clean piece of evidence for §7's precise thesis — *there is no component that tells another component what to do* — precisely because it describes an absence of capability rather than a policy. Recommend it as supporting citation alongside the "eliminates the need for orchestration" passage. It also lets §7 honor its own precision constraint (the hub is real, the hub is critical, the hub does not direct) without hedging the beat.

**4. Bearings #2 item 4 is unblocked and can be written as designed.** The outline made it conditional on this fetch. Scheduler↔kubelet is a sound pairing and the correct answer is now sourced. Suggest the explanation quote "None of the other control plane components are designed to expose remote services" rather than the hub-and-spoke phrase alone, since it is the sentence that actually rules out the arrow.

**5. Source conflict worth knowing about, low stakes.** Kubernetes docs and etcd.io describe etcd differently — "consistent and highly-available" vs "strongly consistent, distributed." Not a contradiction, but if the book quotes both in the same section it will read as inconsistent. Per the stage's own priority rule, prefer the Kubernetes wording in exam-facing material (it is what the KCNA curriculum's vendor documentation says) and use etcd.io only if the author wants the stronger adjective for the §2 gloss.

**6. Open question #6 confirmed as a genuine, permanent gap.** The cached `cncf-kcna-curriculum-pdf-2026-08-23.md` publishes four domain weights (44/28/16/12) and competency *names* only — no sub-competency percentages. Nothing fetched this pass changes that. The chapter's 6% is authored judgment and the front-matter disclosure remains required.

**7. Stage 2 prompt/harness mismatch — a defect in the same family as the `run_chapters.sh` one the outline flagged.** `pipeline/prompts/02_research_snapshot.md:18` instructs this stage to "write it to `{{book_dir}}/sources/`", but `pipeline/executor.py:157` grants research stages only `WebFetch,WebSearch,Read` — no `Write`, no `Bash`. The prompt never mentions that snapshots actually reach `sources/` by being embedded as fenced blocks under a `### N · \`filename.md\`` heading and extracted by `harvest_research_snapshots()` (`pipeline/orchestrator.py:173`). A stage run that takes the prompt literally will burn its turn attempting blocked writes, and one that emits snapshots in any other layout will silently drop them — the harvester requires the fence to follow the heading and the body to begin with `---`, and skips anything else without warning. Recommend `02_research_snapshot.md` document the harvest convention explicitly, and that the harvester log skipped-but-snapshot-looking blocks rather than dropping them silently.

**8. Filename-collision note for the reconcile pass.** `k8s-docs-etcd-access-control-2026-08-24.md` deliberately shares a `source_url` with the existing `k8s-docs-etcd-backup-2026-08-23.md` (same page, different sections, different dates). If any downstream audit dedupes snapshots by `source_url` it will flag these as duplicates. They are not — both should be retained.
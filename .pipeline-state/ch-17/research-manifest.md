Research complete. Delivering the manifest with all snapshots inline.

---

# Research Manifest — KCNA Chapter 17

**Stage 2 · The Fleet and Its Charts · researched 2026-08-31**

The cached corpus was assessed first: **256 snapshots on disk**, of which 15 are Ch 17-relevant. The outline's Open Question 2 assessment was accurate — G15, G16, G17 and G31 are substantially closed by existing snapshots and were **verified, not re-fetched**. Twenty new snapshots close the remaining gaps and refresh three version-dependent claims that have drifted since 2026-08-23.

**Two findings change drafting guidance** and are detailed in Notes: the VPA in-place-resize claim (trap #105) is now contradicted *between three official kubernetes.io pages*, and the supported-version list in `k8s-releases-cadence-2026-08-23.md` is one release stale.

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts | § |
|---|---|---|---|---|
| `cncf-glossary-microservices-monoliths-coupling-2026-08-31.md` | CNCF Cloud Native Glossary | D4.2 | microservices, loose-coupling | §1, §3 |
| `cncf-glossary-immutable-infrastructure-2026-08-31.md` | CNCF Cloud Native Glossary | D4.2 | immutable-infrastructure | §3 |
| `cncf-glossary-service-mesh-2026-08-31.md` | CNCF Cloud Native Glossary | D4.2 | service-mesh, mesh-data-plane | §5 |
| `cncf-glossary-zero-trust-architecture-2026-08-31.md` | CNCF Cloud Native Glossary | D4.2 | zero-trust | §5 |
| `cncf-glossary-serverless-2026-08-31.md` | CNCF Cloud Native Glossary | D4.2 | serverless | §6 |
| `istio-security-mtls-identity-2026-08-31.md` | Istio project (CNCF graduated) | D4.2 | mutual-tls, zero-trust, mesh-control-plane | §5 |
| `istio-ambient-mode-2026-08-31.md` | Istio project (CNCF graduated) | D4.2 | ambient-mode, sidecar-mode, envoy | §5 |
| `envoy-what-is-envoy-2026-08-31.md` | Envoy project (CNCF graduated) | D4.2 | envoy, mesh-data-plane | §5 |
| `knative-serving-autoscaling-2026-08-31.md` | Knative project (CNCF graduated) | D4.2 | scale-to-zero, knative-serving | §6 |
| `k8s-docs-node-autoscaling-2026-08-31.md` | Kubernetes project | D4.2 | cluster-autoscaler, karpenter, node-autoscaling | §7 |
| `karpenter-concepts-2026-08-31.md` | Karpenter project | D4.2 | karpenter, node-autoscaling | §7 |
| `k8s-docs-autoscaling-and-vpa-2026-08-31.md` | Kubernetes project | D4.2 | vertical-pod-autoscaler, keda, horizontal-vs-vertical | §7 |
| `k8s-docs-api-aggregation-and-device-plugins-2026-08-31.md` | Kubernetes project | D4.2 | api-aggregation-layer, device-plugin, extension-point | §4 |
| `cncf-toc-project-lifecycle-process-2026-08-31.md` | CNCF TOC | D4.3, D4.2 | cncf-project-lifecycle, maturity-levels | §2 |
| `cncf-tags-current-structure-2026-08-31.md` | CNCF Contributors / CNCF blog | D4.3 | cncf-tags, cncf-toc | §2 |
| `cncf-charter-governance-bodies-2026-08-31.md` | CNCF (Linux Foundation charter) | D4.3 | cncf-governing-board, cncf-toc, end-user-tab, cncf-mission | §1, §2 |
| `k8s-sig-list-and-groups-2026-08-31.md` | Kubernetes project | D4.3 | kubernetes-sig, working-group, committee, steering-committee | §8 |
| `k8s-release-cycle-and-cadence-2026-08-31.md` | Kubernetes project | D4.3 | sig-release-and-release-cadence, subproject | §8 |
| `cncf-code-of-conduct-2026-08-31.md` | CNCF | D4.3 | code-of-conduct | §8 |
| `cncf-mentoring-and-community-groups-2026-08-31.md` | CNCF Contributors | D4.3 | lfx-mentorship, cloud-native-community-group | §8 |

## Snapshots verified, not re-fetched

Confirmed still on disk and still accurate. Cite these by their **existing** dated tags — the outline's guardrails name several of them literally.

| Existing snapshot | Covers | Verification |
|---|---|---|
| `cncf-cloud-native-definition-2026-08-23.md` | §1's headline quotation | **Re-checked against source today.** Still v1.1, "Approved by TOC/GB: 2024-02-26". Text matches word for word. The outline's `[source: cncf-cloud-native-definition-2026-08-23]` tag is correct — do not repoint it. |
| `cncf-project-maturity-levels-2026-08-23.md` | §2 ladder + graduated roster | Levels unchanged. Roster is dated data (see Notes 5). |
| `cncf-toc-and-tags-2026-08-23.md` | §2 TOC responsibilities, TAG list | Five current TAGs confirmed identical today. Trap #111 is safe. |
| `cncf-who-we-are-2026-08-23.md` | §1 mission, §2 bodies | Verified. |
| `cncf-landscape-and-community-2026-08-23.md` | §2 Landscape, §8 KubeCon/Ambassadors/CNCGs | G15 + G17 closed. |
| `k8s-docs-extending-kubernetes-2026-08-23.md` | §4 — the documentation's **six extension points** | This is the source that keeps Ch 10:1896's two-maps promise. Complete and current. |
| `k8s-community-governance-2026-08-23.md` | §8 SIG / WG / Committee / Steering | G16 closed. |
| `k8s-community-membership-ladder-2026-08-23.md` | §8 contributor ladder | G16 closed. |
| `k8s-keps-and-feature-stages-2026-08-23.md` | §8 KEPs | G16 closed. |
| `k8s-history-ten-years-2026-08-23.md` | G14 origin/history | **Verify-only per outline.** Ch 3 §1 shipped from this; §2/§8 should point at Ch 3 §1, not restate. |
| `cncf-kcna-certification-page-2026-08-23.md` | §8 certification ladder; D4's published 12% | G31 closed. **This is the tag for the 12%-not-7% metadata ruling.** |
| `istio-service-mesh-2026-08-23.md` | §5 definition, data/control split, sidecar vs ambient | Still the primary §5 source; now backed by five new snapshots. |
| `knative-overview-2026-08-23.md` | §6 Serving / Eventing / Functions, CRD implementation | Only source for **Knative Functions** — see Gaps. |
| `k8s-docs-hpa-2026-08-24.md`, `k8s-docs-resource-metrics-pipeline-2026-08-31.md`, `metrics-server-install-2026-08-31.md` | §7 HPA/metrics-server retrieval anchor | Ch 6/Ch 13 material, already sourced. |
| `k8s-docs-custom-resources-2026-08-23.md`, `k8s-docs-operator-pattern-2026-08-23.md`, `k8s-docs-cri-2026-08-24.md`, `k8s-docs-network-plugins-2026-08-24.md`, `csi-spec-objective-2026-08-25.md` | §4's four interfaces, each sourced where the reader met it | §4 **collects**; it does not redefine. These are the back-bearings. |
| `opencost-overview-2026-08-23.md` | G32 cost management | Retained; not expanded — see Gaps. |

---

### A1 · `cncf-glossary-microservices-monoliths-coupling-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/microservices-architecture/"
fetched_at: "2026-08-31T09:40:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["microservices", "loose-coupling", "monolithic-apps", "cloud-native-characteristics"]
---
# CNCF Cloud Native Glossary — Microservices, Monolithic Apps, Loosely Coupled Architecture

Three related glossary entries, fetched together because §3 teaches them as a
mutually reinforcing set rather than as separate definitions.

## Microservices Architecture (glossary.cncf.io/microservices-architecture/)

Definition, verbatim:

> "A microservices architecture is an architectural approach that breaks
> applications into individual independent (micro)services, with each service
> focused on a specific functionality."

Problem it addresses — verbatim fragment:

> "the entire app would have to be scaled to accommodate the increase — a very
> inefficient use of resources"

[Paraphrase of surrounding text, NOT verbatim: the entry states that the
traditional monolithic approach creates inefficiencies; that monoliths encourage
tight coupling and make it harder to enforce separation of concerns; and that
they require developers to understand the entire codebase before making changes.]

How it helps — verbatim fragments:

> "different teams to work simultaneously on a small part of a bigger application
> without inadvertently negatively impacting the rest of the app"

> "it also creates operational overhead — the things you need to deploy and keep
> track of increase by order of magnitude"

[Paraphrase, NOT verbatim: breaking functionality into separate services enables
independent deployment, updates, and scaling; the entry notes that many
cloud native technologies have emerged to address the operational challenges
inherent in microservices deployments.]

## Monolithic Apps (glossary.cncf.io/monolithic-apps/) — verbatim, complete

A monolithic application contains all functionality in a single deployable
program. This is often the simplest and easiest place to start when making an
application. However, once the application grows in complexity, monoliths can
become hard to maintain. With more developers working on the same codebase, the
likelihood of conflicting changes and the need for interpersonal communication
between developers increases.

**Problem it Addresses**

Devolving an application into microservices increases its operational overhead —
there are more things to test, deploy, and keep running. Early in a product's
lifecycle, it may be advantageous to defer this complexity and build a monolithic
application until the product is determined successful.

**How it Helps**

A well-designed monolith can uphold lean principles by being the simplest way to
get an application up and running. When the business value of the monolithic
application proves successful, it can be decomposed into microservices. Crafting
a microservices-based app before it has proven valuable may be premature spending
of engineering effort. If the application yields no value, that effort becomes
wasted.

## Loosely Coupled Architecture (glossary.cncf.io/loosely-coupled-architecture/) — verbatim, complete

Loosely coupled architecture is an architectural style where the individual
components of an application are built independently from one another (the
opposite paradigm of tightly coupled architectures). Each component, sometimes
referred to as a microservice, is built to perform a specific function in a way
that can be used by any number of other services. This pattern is generally
slower to implement than tightly coupled architecture but has a number of
benefits, particularly as applications scale.

Loosely coupled applications allow teams to develop features, deploy, and scale
independently, which allows organizations to iterate quickly on individual
components. Application development is faster and teams can be structured around
their competency, focusing on their specific application.
```

### A2 · `cncf-glossary-immutable-infrastructure-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/immutable-infrastructure/"
fetched_at: "2026-08-31T09:42:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["immutable-infrastructure", "declarative-api-as-a-characteristic"]
---
# CNCF Cloud Native Glossary — Immutable Infrastructure

Tags: Infrastructure, Property

Definition, verbatim:

> "Immutable Infrastructure refers to computer infrastructure (virtual machines,
> containers, network appliances) that cannot be changed once deployed."

[Paraphrase, NOT verbatim: the entry states this enforcement occurs either
through automated processes that overwrite unauthorized modifications, or through
systems that prevent changes altogether. Containers exemplify the concept —
persistent alterations require creating new container versions or recreating from
images.]

## Security and operational benefits

Verbatim:

> "Operating such a system becomes a lot more straightforward because
> administrators can make assumptions about it."

[Paraphrase, NOT verbatim: by blocking or detecting unauthorized modifications,
immutable systems help organizations identify and address security
vulnerabilities more effectively.]

## Integration with infrastructure as code

Verbatim:

> "This combination of immutability and version control means that there is a
> durable audit log of every authorized change to a system."

[Paraphrase, NOT verbatim: the approach complements infrastructure-as-code
practices, where automation scripts reside in version control systems like Git.]

---
DRAFTING NOTE (not from source): this entry's "cannot be changed once deployed"
is infrastructure immutability. It is a DIFFERENT immutability from the image
immutability Ch 2 §2 owns. B7's canonical-forms ruling requires the full two-word
phrase "immutable infrastructure" and a back-bearing to Ch 2 §2 rather than a
re-derivation.
```

### A3 · `cncf-glossary-service-mesh-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/service-mesh/"
fetched_at: "2026-08-31T09:40:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["service-mesh", "mesh-data-plane", "sidecar-mode", "microservices"]
---
# CNCF Cloud Native Glossary — Service Mesh (verbatim, complete)

This is the VENDOR-NEUTRAL definition, to be quoted beside Istio's. The two agree
on the substance and differ in framing: CNCF says "without requiring code
changes"; Istio says "without code changes".

## Service Mesh

In a microservices world, apps are broken down into multiple smaller services
that communicate over a network. Just like your wifi network, computer networks
are intrinsically unreliable, hackable, and often slow. Service meshes address
this new set of challenges by managing traffic (i.e., communication) between
services and adding reliability, observability, and security features uniformly
across all services.

## Problem it addresses

Having moved to a microservices architecture, engineers are now dealing with
hundreds, possibly even thousands of individual services, all needing to
communicate. That means a lot of traffic is going back and forth over the
network. On top of that, individual applications may need to encrypt
communications to support regulatory requirements, provide common metrics to
operations teams, or provide detailed insight into traffic to help diagnose
issues. If built into the individual applications, each one of these features
will cause friction between teams and slow down development of new features.

## How it helps

Service meshes add reliability, observability, and security features uniformly
across all services across a cluster without requiring code changes. Before
service meshes, that functionality had to be encoded into every single service,
becoming a potential source of bugs and technical debt.

The Sidecar Container model pairs each pod with a proxy. This per-pod proxy
intercepts and manages network traffic, enforces security policies, balances
workloads, and collects performance data for each service. While this approach
offers excellent control and service-specific traffic management, it also uses
more computing resources and becomes more complex to manage as your system grows.

A Sidecarless design, on the other hand, moves the aforementioned mesh
functionality to the operating system level by using kernel features like eBPF.
By doing away with per-pod proxies, this method drastically reduces resource
usage and removes unnecessary network hops, which lowers latency and boosts
performance. Because overhead remains constant regardless of pod count and there
are fewer agents to deploy, teams benefit from simplified operations and linear
scalability as workload increases.

---
DRAFTING NOTE (not from source): the final paragraph's "Sidecarless"/eBPF framing
is a THIRD model, distinct from Istio's sidecar-vs-ambient split. eBPF is barred
from graded text by the B7 Part 2 ruling (outline Open Question 11). §5 should
teach Istio's sidecar/ambient framing and may quote this entry's first three
paragraphs; do not import the eBPF sentence.
```

### A4 · `cncf-glossary-zero-trust-architecture-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/zero-trust-architecture/"
fetched_at: "2026-08-31T09:44:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["zero-trust", "mutual-tls", "service-mesh"]
---
# CNCF Cloud Native Glossary — Zero Trust Architecture (verbatim, complete)

Zero trust architecture prescribes to an approach to the design and
implementation of IT systems where trust is completely removed. The core
principle being "never trust, always verify", devices or systems themselves,
whilst communicating to other components of a system, always verify themselves
before doing so. In many networks today, within the corporate network, systems
and devices inside may freely communicate with each other as they are within the
trusted boundary of the corporate network perimeter. Zero trust architecture
takes the opposite approach where although inside the network perimeter,
components within the system first have to pass verification before any
communication is made.

## Problem it addresses

With the traditional trust based approach where systems and devices that exist
within a corporate network perimeter, the assumption is that because there is
trust, there is no problem. Zero trust architecture however, recognises that
trust is a vulnerability. In the event where an attacker has gained access to a
trusted device, depending on the level of trust and access that has been given to
that device, the system is now vulnerable to attack as the attacker is within the
"trusted" network perimeter and is able to move laterally throughout the system.
In a zero trust architecture, trust is removed, therefore reducing the attack
surface as an attacker is now forced to verify before going any further
throughout the system.

## How it helps

Adopting a zero trust architecture brings the principal benefit of increased
security with a reduction in the attack surface. Removing trust from your
corporate system now increases the number and strength of security gates that an
attacker has to go through to gain access to other areas of the system.

---
DRAFTING NOTE (not from source): this is the source that makes §5's Soundings Q8
payoff land. Q8 establishes that nothing protects the Ingress-to-Pod leg by
default; "trust is a vulnerability" and lateral movement inside the perimeter are
exactly what that unencrypted leg represents.
```

### A5 · `cncf-glossary-serverless-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/serverless/"
fetched_at: "2026-08-31T09:42:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["serverless", "scale-to-zero"]
---
# CNCF Cloud Native Glossary — Serverless

The vendor-neutral definition of serverless, which the cached
`knative-overview-2026-08-23.md` does not supply. Delivered as direct quotations;
the upstream fetch declined full-body reproduction.

## Definition — verbatim quotations

> "Serverless Computing abstracts servers away from the user."

> "Charges are based on a pay-per-use model."

> "Scaling and resource provisioning for computing, storage, or networking are
> automatically adjusted based on application demand without user intervention."

> "A serverless platform provider consolidates resources to serve multiple users
> on a single physical machine, ensuring isolation through virtualization."

## Problem it addresses — verbatim quotations

> "Users commit to a predefined capacity, resulting in charges for continuous
> server availability regardless of actual use."

> "Responsibility for adjusting server capacity to meet fluctuating demands falls
> on the user, maintaining active infrastructure even during idle periods."

## How it helps — verbatim quotations

> "Serverless architecture introduces a more efficient approach, activating
> services solely upon demand."

> "Serverless technology relieves developers of the burdens of scaling
> applications and managing server infrastructure."

> "Tasks such as operating system maintenance, security updates, load balancing,
> capacity planning, and monitoring are delegated to the cloud provider."

---
DRAFTING NOTE (not from source): "abstracts servers away from the USER" — not
"eliminates servers". Combined with `knative-overview-2026-08-23.md`'s statement
that Knative "builds on the Kubernetes Pod abstraction" and that Serving and
Eventing "are implemented as Kubernetes Custom Resource Definitions (CRDs)", this
is the full sourced refutation of trap #84. Note that trap #84 remains
`[inferred]` as a FREQUENCY claim; the factual half is now `[source]`-backed
twice over.
```

### A6 · `istio-security-mtls-identity-2026-08-31.md` (new)
```markdown
---
source_url: "https://istio.io/latest/docs/concepts/security/"
fetched_at: "2026-08-31T09:48:00-0400"
authority: "Istio project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["mutual-tls", "zero-trust", "mesh-control-plane", "mesh-data-plane", "envoy", "service-mesh"]
---
# Istio — Security concepts (istio.io/latest/docs/concepts/security/)

Closes the outline's gap: `istio-service-mesh-2026-08-23.md` supports mTLS and
zero trust only at slogan depth. Direct quotations follow.

## Goals of Istio security — verbatim

> "The goals of Istio security are: Security by default: no changes needed to
> application code and infrastructure; Defense in depth: integrate with existing
> security systems to provide multiple layers of defense; Zero-trust network:
> build security solutions on distrusted networks."

## High-level architecture — verbatim

> "Security in Istio involves multiple components: A Certificate Authority (CA)
> for key and certificate management; The configuration API server distributes to
> the proxies: authentication policies, authorization policies, secure naming
> information; Sidecar and perimeter proxies work as Policy Enforcement Points
> (PEPs) to secure communication between clients and servers."

## Istio identity — verbatim

> "The Istio identity model uses the first-class `service identity` to determine
> the identity of a request's origin. This model allows for great flexibility and
> granularity for service identities to represent a human user, an individual
> workload, or a group of workloads."

## Mutual TLS authentication — verbatim

> "When a workload sends a request to another workload using mutual TLS
> authentication, the request is handled as follows: 1) Istio re-routes the
> outbound traffic from a client to the client's local sidecar Envoy; 2) The
> client side Envoy starts a mutual TLS handshake with the server side
> Envoy... 3) The client side Envoy and the server side Envoy establish a mutual
> TLS connection; 4) The server side Envoy authorizes the request."

## Permissive mode — verbatim

> "With the permissive mode enabled, the server accepts both plaintext and mutual
> TLS traffic. The mode provides greater flexibility for the on-boarding process."

---
DRAFTING NOTE (not from source): "The configuration API server distributes to the
proxies" is the mesh's control plane doing its job, stated in the source's own
words. This sentence is the cleanest available defusal of trap #101 — the mesh's
control plane distributes policy TO PROXIES, which is visibly a different job
from the cluster control plane of Ch 3 §2. Scope guardrail still applies: teach
what a mesh is and buys. Do NOT teach PeerAuthentication, AuthorizationPolicy,
VirtualService or DestinationRule — permissive mode above is a *concept* the
prose may name in a clause, not a resource to configure.
```

### A7 · `istio-ambient-mode-2026-08-31.md` (new)
```markdown
---
source_url: "https://istio.io/latest/docs/ambient/overview/"
fetched_at: "2026-08-31T09:44:00-0400"
authority: "Istio project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["ambient-mode", "sidecar-mode", "envoy", "mesh-data-plane"]
---
# Istio — Ambient mode overview (istio.io/latest/docs/ambient/overview/)

The source for trap #102 ("a service mesh means sidecars"). Direct quotations.

## What ambient mode is — verbatim

> "In ambient mode, Istio implements its features using a per-node Layer 4 (L4)
> proxy, and optionally a per-namespace Layer 7 (L7) proxy."

## The ztunnel node proxy — verbatim

> "The ztunnel (Zero Trust tunnel) component is a purpose-built, per-node proxy
> that powers Istio's ambient data plane mode."

## The L4 secure overlay — verbatim

> "The term 'secure overlay' is used to collectively describe the set of L4
> networking functions implemented in an ambient mesh via the ztunnel proxy."

## The waypoint proxy and the L7 layer — verbatim

> "The waypoint proxy is a deployment of the Envoy proxy; the same engine that
> Istio uses for its sidecar data plane mode."

> Waypoint proxies enable "advanced traffic management and L7 networking
> features" and "L7 authorization, telemetry and VirtualService routing."

## Comparison with sidecar mode — verbatim

> "Pods and workloads using sidecar mode can co-exist within the same mesh as
> pods that use ambient mode."

> In ambient mode, "workload pods no longer require proxies running in sidecars
> in order to participate in the mesh".

---
DRAFTING NOTE (not from source): "the same engine that Istio uses for its sidecar
data plane mode" is the sourced sentence behind the outline's claim that BOTH
modes use Envoy — and it is what makes the figure's requirement work, that
sidecar and ambient be drawn as "two arrangements of the same data plane, not two
products". The quoted L7 fragment mentions VirtualService; the §5 scope guardrail
bars teaching Istio CRDs, so do not carry that word into prose.
```

### A8 · `envoy-what-is-envoy-2026-08-31.md` (new)
```markdown
---
source_url: "https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy"
fetched_at: "2026-08-31T09:44:00-0400"
authority: "Envoy project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["envoy", "mesh-data-plane", "service-mesh", "sidecar-mode"]
---
# Envoy — What is Envoy (envoyproxy.io/docs/envoy/latest/intro/what_is_envoy)

Envoy is named in kb_tags and in three §5 traps but had no snapshot of its own.

## What Envoy is — verbatim

> "Envoy is an L7 proxy and communication bus designed for large modern service
> oriented architectures."

## Out of process architecture — verbatim

> "Envoy is a self contained process that is designed to run alongside every
> application server. All of the Envoys form a transparent communication mesh in
> which each application sends and receives messages to and from localhost and is
> unaware of the network topology."

## Language independence — verbatim fragments

> "Envoy works with any application language"

> "Envoy can be deployed and upgraded quickly across an entire infrastructure
> transparently"

[Paraphrase, NOT verbatim: the document positions Envoy as a language-agnostic
proxy that operates alongside applications to form a service mesh.]

---
DRAFTING NOTE (not from source): "each application sends and receives messages to
and from localhost and is unaware of the network topology" is Envoy's own
statement of the without-code-changes property, from the data plane's side. It
pairs directly with Soundings Q4, which tests what a sidecar shares with the
container beside it — the answer being the Pod's network namespace, i.e. localhost.
```

### A9 · `knative-serving-autoscaling-2026-08-31.md` (new)
```markdown
---
source_url: "https://knative.dev/docs/serving/autoscaling/"
fetched_at: "2026-08-31T09:52:00-0400"
authority: "Knative project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["scale-to-zero", "knative-serving", "serverless"]
---
# Knative Serving — Autoscaling (knative.dev/docs/serving/autoscaling/)

Sources §6's Fixed Point (the scale-to-zero LIFECYCLE) and the figure
`ch17-fig07-scale-to-zero-and-the-knative-service`.

## What the autoscaler is — verbatim

> "Knative Serving provides automatic scaling, or _autoscaling_, for applications
> to match incoming demand."

## The default autoscaler — verbatim

> "This is provided by default, by using the Knative Pod Autoscaler (KPA)."

## Scale to zero — verbatim

> "If an application is receiving no traffic and scale to zero is enabled,
> Knative Serving scales the application down to zero replicas."

## Alternative autoscaler — verbatim fragment

> "Configure your Knative deployment to use the Kubernetes Horizontal Pod
> Autoscaler (HPA) instead of the default KPA."

## Not stated on this page

The page does not use the phrase "request-driven scaling model".

---
DRAFTING NOTE (not from source): the KPA-vs-HPA choice is a real fact but is
arguably above associate tier. It IS however a clean, sourced bridge from §6 to
§7 ("Ch 17 §7 — four things that scale" is already a listed cross-bearing out of
§6), and it reinforces §7's taxonomy rather than complicating it. Optional; see
Notes 8.
```

### A10 · `k8s-docs-node-autoscaling-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/"
fetched_at: "2026-08-31T09:50:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D4.2"]
concepts_covered: ["node-autoscaling", "cluster-autoscaler", "karpenter", "horizontal-vs-vertical-autoscaling"]
---
# Node Autoscaling (kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/)

The dedicated node-autoscaling page. `k8s-docs-autoscaling-2026-08-23.md` covers
node autoscaling in a single closing sentence; this is the substance behind it,
and it is where §7's Ch 7 §2 retrieval anchor is sourced.

## Opening definition — verbatim

> "Automatically provision and consolidate the Nodes in your cluster to adapt to
> demand and optimize cost."

## Provisioning, and what triggers it — verbatim

> "If there are Pods in a cluster that can't be scheduled on existing Nodes, new
> Nodes can be automatically added to the cluster—_provisioned_—to accommodate
> the Pods."

## Consolidation — verbatim

> "Nodes in your cluster can be automatically _consolidated_ in order to improve
> the overall Node utilization, and in turn the cost-effectiveness of the
> cluster. Consolidation happens through removing a set of underutilized Nodes
> from the cluster."

## Interaction with the cloud provider — verbatim

> "In addition to the Kubernetes API, autoscalers also need to interact with
> cloud provider APIs to provision and consolidate Nodes."

## Implementations — verbatim

> "[Cluster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler)
> and [Karpenter](https://github.com/kubernetes-sigs/karpenter) are the two Node
> autoscalers currently sponsored by
> [SIG Autoscaling](https://github.com/kubernetes/community/tree/main/sig-autoscaling)."

> "Cluster Autoscaler adds or removes Nodes to pre-configured _Node groups_."

> "From the perspective of a cluster user, both autoscalers should provide a
> similar Node autoscaling experience. Both will provision new Nodes for
> unschedulable Pods, and both will consolidate the Nodes that are no longer
> optimally utilized."

> "Different autoscalers may also provide features outside the Node autoscaling
> scope described on this page, and those additional features may differ between
> them."

## Not captured

The page's `#karpenter` subsection body was truncated by the fetch tool across
three attempts. Karpenter's own description is captured separately in
`karpenter-concepts-2026-08-31.md`.

---
DRAFTING NOTE (not from source): "Pods in a cluster that can't be scheduled on
existing Nodes" is the second half of the sentence Ch 7:428 left open. This
snapshot is the tag for that retrieval anchor. Note also that this page is the
sourced answer to Open Question 5 — Karpenter's affiliation is SIG AUTOSCALING,
a Kubernetes SIG. Nothing here or anywhere in the official corpus assigns
Karpenter a CNCF maturity level.
```

### A11 · `karpenter-concepts-2026-08-31.md` (new)
```markdown
---
source_url: "https://karpenter.sh/docs/concepts/"
fetched_at: "2026-08-31T09:50:00-0400"
authority: "Karpenter project (karpenter.sh; repository kubernetes-sigs/karpenter)"
objectives_covered: ["D4.2"]
concepts_covered: ["karpenter", "node-autoscaling", "cluster-autoscaler"]
---
# Karpenter — Documentation and Concepts (karpenter.sh/docs/, karpenter.sh/docs/concepts/)

Closes the outline's Karpenter gap. Karpenter was previously named in exactly one
clause of one snapshot.

## What Karpenter is — verbatim

> "Karpenter is an open-source node lifecycle management project built for
> Kubernetes."

## What Karpenter does — verbatim, the docs' own four bullets

> - "Watching for pods that the Kubernetes scheduler has marked as unschedulable"
> - "Evaluating scheduling constraints (resource requests, nodeselectors,
>   affinities, tolerations, and topology spread constraints) requested by the pods"
> - "Provisioning nodes that meet the requirements of the pods"
> - "Disrupting the nodes when the nodes are no longer needed"

## Summary statement — verbatim

> "Karpenter's job is to add nodes to handle unschedulable pods, schedule pods on
> those nodes, and remove the nodes when they are not needed."

## NodePool — verbatim

> "Karpenter defines a Custom Resource called a NodePool to specify configuration."

## Affiliation — what the source does and does not say

The site carries the footer "built with ❤️ at AWS" and "© 2026 Amazon.com, Inc.
or its affiliates." The upstream repository is `kubernetes-sigs/karpenter`.

**The site makes NO claim of CNCF membership, and states NO CNCF maturity level.**
The only governance statement located in any official source is on
kubernetes.io's node-autoscaling page: Karpenter and Cluster Autoscaler are "the
two Node autoscalers currently sponsored by SIG Autoscaling."

---
DRAFTING NOTE (not from source): this settles outline Open Question 5. Karpenter
may be named as a node autoscaler sponsored by Kubernetes SIG Autoscaling,
tagged to this snapshot and to `k8s-docs-node-autoscaling-2026-08-31.md`. It must
NOT be given a CNCF maturity level. Note also that "Karpenter defines a Custom
Resource called a NodePool" is a small, free bonus for §4/§9 — a fifth instance of
the pluggability shape, arriving in §7 — but the ordinal rule bars counting past
four, so if it is used at all it is used unnumbered.
```

### A12 · `k8s-docs-autoscaling-and-vpa-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/autoscaling/"
fetched_at: "2026-08-31T09:55:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — three pages, each attributed inline"
objectives_covered: ["D4.2"]
concepts_covered: ["vertical-pod-autoscaler", "keda-event-driven-autoscaling", "horizontal-vs-vertical-autoscaling", "cluster-autoscaler"]
---
# Autoscaling workloads, the VPA, and in-place resize — refreshed 2026-08-31

REFRESHES the version-dependent claims in `k8s-docs-autoscaling-2026-08-23.md`.
That snapshot's structural facts are unchanged; its VERSION NUMBER has moved and
its VPA-in-place claim is contradicted by two other official pages. Both are
recorded here. See the manifest's Notes 1.

## Source A — kubernetes.io/docs/concepts/workloads/autoscaling/ (verbatim)

### Vertical scaling

> "You can automatically scale a workload vertically using a
> VerticalPodAutoscaler (VPA). Unlike the HPA, the VPA doesn't come with
> Kubernetes by default, but is a an add-on that you or a cluster administrator
> may need to deploy before you can use it."

> "Once installed, it allows you to create CustomResourceDefinitions (CRDs) for
> your workloads which define _how_ and _when_ to scale the resources of the
> managed replicas."

> "Note: You will need to have the Metrics Server installed to your cluster for
> the VPA to work."

### In-place pod vertical scaling

> "Feature state: Stable since Kubernetes v1.35"

> "This is a stable feature in Kubernetes, and has been since version v1.35. It
> was first available in the v1.27 release. You can no longer disable or opt out
> of this feature or behavior (it is locked); if you explicitly set a value for
> the associated feature gate InPlacePodVerticalScaling, Kubernetes ignores it
> but does not report any error."

> "As of Kubernetes 1.37, VPA does not support resizing pods in-place, but this
> integration is being worked on."

*(The 2026-08-23 snapshot recorded this same sentence dated to v1.35. The claim
persists; only the version stamp has advanced.)*

### Event driven autoscaling

> "It is also possible to scale workloads based on events, for example using the
> _Kubernetes Event Driven Autoscaler_ (**KEDA**)."

> "KEDA is a CNCF-graduated project enabling you to scale your workloads based on
> the number of events to be processed, for example the amount of messages in a
> queue. There exists a wide range of adapters for different event sources to
> choose from."

### Autoscaling based on schedules

> "Another strategy for scaling your workloads is to **schedule** the scaling
> operations, for example in order to reduce resource consumption during off-peak
> hours."

> "Similar to event driven autoscaling, such behavior can be achieved using KEDA
> in conjunction with its `Cron` scaler. The `Cron` scaler allows you to define
> schedules (and time zones) for scaling your workloads in or out."

### Scaling cluster infrastructure

> "If scaling workloads isn't enough to meet your needs, you can also scale your
> cluster infrastructure itself."

> "Scaling the cluster infrastructure normally means adding or removing nodes."

## Source B — kubernetes.io/docs/concepts/workloads/autoscaling/vertical-pod-autoscale/ (verbatim)

> "In Kubernetes, a _VerticalPodAutoscaler_ automatically updates a workload
> management resource (such as a Deployment or StatefulSet), with the aim of
> automatically adjusting infrastructure resource requests and limits to match
> actual usage."

> "Unlike HorizontalPodAutoscaler, which is part of the core Kubernetes API, VPA
> must be installed separately in your cluster."

> "The VPA consists of three main components: The _recommender_, which analyzes
> resource usage and provides recommendations. The _updater_, that Pod resource
> requests either by evicting Pods or modifying them in place. And the VPA
> _admission controller_ webhook, which applies resource recommendations to new
> or recreated Pods."

Update modes listed on this page: `Off`, `Initial`, `Recreate`,
`InPlaceOrRecreate`, `InPlace`, `Auto` (deprecated).

## Source C — kubernetes.io/blog/2025/12/19/kubernetes-v1-35-in-place-pod-resize-ga/ (verbatim)

> "This release marks a major step: more than 6 years after its initial
> conception, the **In-Place Pod Resize** feature (also known as In-Place Pod
> Vertical Scaling), first introduced as alpha in Kubernetes v1.27, and graduated
> to beta in Kubernetes v1.33, is now **stable (GA)** in Kubernetes 1.35!"

> "In-Place Pod Resize makes CPU and memory requests and limits mutable, allowing
> you to adjust these resources within a running Pod, often without requiring a
> container restart."

> "Autoscalers are now empowered to adjust resources and with less impact. For
> example, Vertical Pod Autoscaler (VPA)'s `InPlaceOrRecreate` update mode, which
> leverages this feature, has graduated to beta. This allows resources to be
> adjusted automatically and seamlessly based on usage with minimal disruption."

---
⚠ SOURCE CONFLICT — see manifest Notes 1. Sources A, B and C are all
kubernetes.io and do not agree on whether VPA supports in-place resize. Trap #105
must be written to the conflict, not through it.
```

### A13 · `k8s-docs-api-aggregation-and-device-plugins-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/apiserver-aggregation/"
fetched_at: "2026-08-31T09:52:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — two pages, attributed inline"
objectives_covered: ["D4.2"]
concepts_covered: ["api-aggregation-layer", "device-plugin", "extension-point", "four-pluggable-interfaces"]
---
# The aggregation layer and device plugins — the two §4 extension points with no snapshot

`k8s-docs-extending-kubernetes-2026-08-23.md` names both in its six-extension-point
list but does not define either. Both are in this chapter's kb_tags and both
appear in the table that sits beside `ch17-fig02-extension-points-map`.

## Source A — API aggregation layer (kubernetes.io/docs/concepts/extend-kubernetes/api-extension/apiserver-aggregation/), verbatim

> "The aggregation layer allows Kubernetes to be extended with additional APIs,
> beyond what is offered by the core Kubernetes APIs."

> "The aggregation layer runs in-process with the kube-apiserver. Until an
> extension resource is registered, the aggregation layer will do nothing. To
> register an API, you add an _APIService_ object, which 'claims' the URL path in
> the Kubernetes API. At that point, the aggregation layer will proxy anything
> sent to that API path (e.g. `/apis/myextension.mycompany.io/v1/…`) to the
> registered APIService."

> "The aggregation layer is different from Custom Resource Definitions, which are
> a way to make the kube-apiserver recognise new kinds of object."

## Source B — Device plugins (kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/), verbatim

> "Device plugins let you configure your cluster with support for devices or
> resources that require vendor-specific setup, such as GPUs, NICs, FPGAs, or
> non-volatile main memory."

> "Kubernetes provides a device plugin framework that you can use to advertise
> system hardware resources to the Kubelet."

> "The targeted devices include GPUs, high-performance NICs, FPGAs, InfiniBand
> adapters, and other similar computing resources that may require vendor
> specific initialization and setup."

> "the device plugin sends the kubelet the list of devices it manages, and the
> kubelet is then in charge of advertising those resources to the API server as
> part of the kubelet node status update"

[Paraphrase, NOT verbatim: the kubelet exports a `Registration` gRPC service; a
device plugin registers itself through it, sending the name of its Unix socket,
the Device Plugin API version, and the `ResourceName` it wants to advertise,
following the extended-resource naming scheme `vendor-domain/resourcetype`.]

---
DRAFTING NOTE (not from source): the aggregation-layer page's closing sentence —
"The aggregation layer is different from Custom Resource Definitions" — is
load-bearing for §4. It is the documentation itself distinguishing the two
API-extension routes, which is precisely why Ch 2 §4's "API extensions" label and
Ch 6 §8's "CRDs" label are both defensible and neither is wrong. §4's
one-clause reconciliation can be written straight off this sentence. The device
plugin's "advertise system hardware resources to the Kubelet" is the same
interface-and-implementation shape as CRI/CNI/CSI, one layer over — useful for
§9 as evidence, but the ordinal rule still bars counting past four.
```

### A14 · `cncf-toc-project-lifecycle-process-2026-08-31.md` (new)
```markdown
---
source_url: "https://github.com/cncf/toc/blob/main/process/README.md"
fetched_at: "2026-08-31T09:48:00-0400"
authority: "Cloud Native Computing Foundation Technical Oversight Committee"
objectives_covered: ["D4.3", "D4.2"]
concepts_covered: ["cncf-project-lifecycle", "cncf-project-maturity-levels", "cncf-toc"]
---
# CNCF project lifecycle process (github.com/cncf/toc/blob/main/process/README.md)

**This is the document trap #98 is about.** The maturity LEVELS are described on
cncf.io/projects/; the CRITERIA and the process live here, in the TOC repository.

## The maturity levels, as this document names them — verbatim

> "Sandbox - Experimental or innovative projects early in their development"

> "Incubation - Projects gaining adoption, focusing on improving stability and
> maturity"

> "Graduated - Highly mature, robust projects whose adopters have demonstrated
> their production-readiness"

> "Archived - Inactive or low activity projects that are no longer supported"

## How a project moves between levels — verbatim

> "submit an incubation or graduation application issue on the TOC repo"

> "complete the Adopter Interview Form with 5-7 adopters willing to be interviewed"

[Paraphrase, NOT verbatim: applicants must also provide self-assessed technical
and governance reviews.]

## Due diligence — verbatim

> "an Application Kick off Meeting"

> "Due Diligence creation or refresh"

> "Adopter Interviews are conducted"

> "a TOC internal comment period, about 1 week, for other TOC members"

[Paraphrase, NOT verbatim: a TOC sponsor is assigned to conduct the evaluation
and crafts a PR evaluating the project's completion of the criteria.]

## Who decides — verbatim

> "The public comment period is open for two weeks."

> "the TOC opens voting on the PR using gitvote"

> "If the vote passes (2/3 supermajority vote of the TOC), the results are emailed"

---
DRAFTING NOTE (not from source): note the FOURTH level. This document names
**Archived** alongside Sandbox / Incubation / Graduated, and
`cncf-who-we-are-2026-08-23.md` independently counts projects "across the
Graduated, Incubating, Sandbox, and Archived categories." The outline's §2 plan,
its Exam Alert row, and `ch17-fig05-cncf-maturity-levels` all describe a
three-rung ladder. Archived is not a rung a project climbs — it is where projects
go when they stop — so the three-rung progression is correct as a PROGRESSION.
But a reader meeting "Archived" on cncf.io will wonder. One clause naming it as
the terminal state, outside the ladder, would be cheap insurance. Author's call;
recorded so the drafting stage does not silently pick one.

Note also the terminology: this document says "**Incubation**" for the process
and cncf.io/projects/ says "**Incubating**" for the level. B7 canonical casing
should pick one; the shipped Ch 15:1215 treatment and the outline's fixed §2
title both use "Incubating".
```

### A15 · `cncf-tags-current-structure-2026-08-31.md` (new)
```markdown
---
source_url: "https://contribute.cncf.io/community/tags/"
fetched_at: "2026-08-31T09:56:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Contributors site + CNCF blog)"
objectives_covered: ["D4.3"]
concepts_covered: ["cncf-tags", "cncf-toc", "kubernetes-sig"]
---
# CNCF Technical Advisory Groups — current structure, verified 2026-08-31

CONFIRMS `cncf-toc-and-tags-2026-08-23.md`. Trap #111 is live and the cached list
is correct. Note: **cncf.io/tags/ now returns HTTP 404**; the authoritative
current home is contribute.cncf.io/community/tags/.

## Source A — contribute.cncf.io/community/tags/ (verbatim)

> "Technical Advisory Groups (TAGs) are the primary organizational units within
> the CNCF that oversee and coordinate interests across projects, working groups,
> and the broader cloud native community."

> They "serve as bridges between CNCF projects, end users, and the Technical
> Oversight Committee (TOC)."

> "The current TAG structure was established in 2025 to better align with cloud
> native ecosystem needs."

### The five current TAGs, with the scopes this page states — verbatim

> "TAG Developer Experience" — "Databases, Microservices, Streaming, Messaging,
> API Management, Developer Frameworks"

> "TAG Infrastructure" — "Data, Storage, Network, DNS, Compute, Service Mesh,
> Infrastructure-as-Code, Edge, Sovereignty, Load Balancing"

> "TAG Operational Resilience" — "Observability, Management, Business Continuity,
> Resource Optimization, Cost Efficiency, Energy, Performance, Troubleshooting,
> Reliability, Day 2 Operations"

> "TAG Security and Compliance" — "Security Hygiene, Policy-as-Code, Compliance,
> Auditing, Threat Modeling, Secure Software Supply Chain"

> "TAG Workloads Foundation" — "Fundamental cloud native workload execution
> environments and lifecycle management"

## Source B — cncf.io/blog/2025/05/07/10-years-in-cloud-native-toc-restructures-technical-groups/ (verbatim)

> "In order to grow with the ecosystem, the TOC has approved a restructuring of
> the Technical Advisory Groups"

> "The TOC has been working with the existing TAGs for two years to identify
> these opportunities for improvement in the TAG structure"

On the origin of the groups — verbatim:

> "By June 2019, this number had grown to 37 projects and the TOC approved the
> creation of SIGs, later to be renamed Technical Advisory Groups."

[Paraphrase, NOT verbatim: the post frames the change against CNCF's growth from
4 projects in 2015–2016 to 223 contributed projects by 2025.]

---
DRAFTING NOTES (not from source), two of them, and both matter:

**1. Trap #111 is confirmed and dated.** Restructuring approved by the TOC,
announced 2025-05-07. The pre-2025 list (App Delivery, Contributor Strategy,
Environmental Sustainability, Network, Observability, Runtime, Security, Storage)
is in `cncf-toc-and-tags-2026-08-23.md`. Both lists are now sourced, the current
one twice.

**2. This is an unexpectedly good gift for trap #112 (TAGs vs SIGs) — and a
hazard.** The blog states that CNCF's groups were originally CALLED SIGs and were
"later renamed Technical Advisory Groups." That is the historical reason the two
are confusable, told in CNCF's own words, and it is far better teaching than a
warning. The hazard: #112 is `[inferred]` and Ethical Guardrail #8 bars framing it
as frequently tested. Naming the shared origin is a *causal explanation*, not a
frequency claim, so it stays inside the guardrail — but the sentence must not
drift into "which is why it's such a common exam trap."
```

### A16 · `cncf-charter-governance-bodies-2026-08-31.md` (new)
```markdown
---
source_url: "https://github.com/cncf/foundation/blob/main/charter.md"
fetched_at: "2026-08-31T09:56:00-0400"
authority: "Cloud Native Computing Foundation (charter) + cncf.io/enduser"
objectives_covered: ["D4.3", "D4.2"]
concepts_covered: ["cncf-mission-and-vendor-neutrality", "cncf-governing-board", "cncf-toc", "end-user-technical-advisory-board"]
---
# CNCF charter — mission and the governance bodies

The charter itself, sourcing the Governing-Board-versus-TOC distinction that §2's
Exam Alert row depends on.

## Source A — github.com/cncf/foundation/blob/main/charter.md (verbatim)

> "The Foundation's mission is to make cloud native computing ubiquitous."

> "The CNCF Governing Board will be responsible for marketing and other business
> oversight and budget decisions for the CNCF."

> "The TOC is expected to facilitate driving neutral consensus for: defining and
> maintaining the technical vision for the Cloud Native Computing Foundation..."

> "The End User TAB will serve as the voice of End Users in the CNCF community,
> advance topics of concern to End Users, and raise awareness about the needs and
> perspectives of end users."

## Source B — cncf.io/enduser (verbatim)

> "Where users of cloud native technology connect, collaborate, and lead."

> "The End User TAB serves as the voice of the end users in CNCF community
> decisions"

### Not stated on cncf.io/enduser

That page does NOT describe the End User TAB's relationship to the TOC. That
relationship is stated in `cncf-toc-and-tags-2026-08-23.md`, from the TOC's own
README: among the TOC's responsibilities is "accepting feedback from the end user
technical advisory board and mapping it to projects."

---
DRAFTING NOTE (not from source): "marketing and other business oversight and
budget decisions" versus "defining and maintaining the technical vision" is the
Board/TOC distinction in the charter's own words, and it is a cleaner
formulation than the outline's "the Board sets the scope; the TOC approves
projects within it". Both are true — the scope framing comes from the TOC README
("approving new projects within the scope of the CNCF set by the Governing
Board") — and the two together make the row unambiguous. Note the charter says
the TAB is the voice of end users in the COMMUNITY; the TOC README says the TOC
maps that feedback to projects. §2 needs both halves for the loop to close.
```

### A17 · `k8s-sig-list-and-groups-2026-08-31.md` (new)
```markdown
---
source_url: "https://github.com/kubernetes/community/blob/master/sig-list.md"
fetched_at: "2026-08-31T09:55:00-0400"
authority: "Kubernetes project (kubernetes/community)"
objectives_covered: ["D4.3"]
concepts_covered: ["kubernetes-sig", "kubernetes-working-group", "kubernetes-committee", "steering-committee", "subproject"]
---
# Kubernetes SIGs, Working Groups and Committees — the actual roster

`k8s-community-governance-2026-08-23.md` supplies the DEFINITIONS. This supplies
the ROSTER, which is what makes §8's three-way distinction concrete instead of
abstract — and it is the source for the D4.3 Soundings question (Q7).

## Framing — verbatim

> "Most community activity is organized into Special Interest Groups (SIGs) and
> time bounded Working Groups."

> "SIGs follow these guidelines although each of these groups may operate a
> little differently depending on their needs and workflow."

## Special Interest Groups, as listed on this page (2026-08-31)

API Machinery · Apps · Architecture · Auth · Autoscaling · CLI · Cloud Provider ·
Cluster Lifecycle · Contributor Experience · Docs · etcd · Instrumentation ·
K8s Infra · Multicluster · Network · Node · Release · Scalability · Scheduling ·
Security · Storage · Testing · UI · Windows

## Working Groups, as listed on this page (2026-08-31)

AI Gateway · Batch · Checkpoint Restore · Data Protection · Device Management ·
etcd Operator · Node Lifecycle · Workload-aware Scheduling

## Committees, as listed on this page (2026-08-31)

Code of Conduct · Security Response · Steering

---
DRAFTING NOTES (not from source):

**1. There are exactly three Committees, and Steering is one of them.** That is a
sharper structural fact than the outline's §8 plan assumes, which treats Steering
as a separate fourth body. Both framings are defensible — the governance doc says
Committees "are formed by the steering committee", which cannot be true of
Steering itself — but a reader who opens sig-list.md will see three Committees
with Steering among them. Recommend §8 says Committees are closed-membership
bodies, names all three, and notes that Steering holds overall governance and
charters the other two. That is both accurate and more memorable than an org
chart.

**2. Three SIGs in this list are ones the reader has already met by name in this
book** — Release (Ch 8, and §8 here), Autoscaling (§7 here, via Karpenter and
Cluster Autoscaler), Storage/Network/Node (Ch 9, Ch 11, Ch 2). §8's "how you'd
join" half becomes concrete for free: the reader can be told that the interfaces
they learned in Chapters 2, 9 and 11 each have a SIG behind them with a public
meeting. That is the cheapest possible bridge from §8 to §9's pluggability claim,
and it costs one sentence.

**3. "time bounded Working Groups"** is the source's own phrasing and is a
tighter formulation than "short-lived" for the SIG/WG contrast.
```

### A18 · `k8s-release-cycle-and-cadence-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/releases/release/"
fetched_at: "2026-08-31T09:56:00-0400"
authority: "Kubernetes project (kubernetes.io/releases + kubernetes/community sig-release charter)"
objectives_covered: ["D4.3"]
concepts_covered: ["sig-release-and-release-cadence", "kubernetes-enhancement-proposal", "subproject"]
---
# The Kubernetes release cycle and cadence — refreshed 2026-08-31

**This snapshot exists to source §8's Fixed Point** — that three minor releases a
year and three supported minor versions are one fact stated twice. Chapter 13
removed the cadence clause for want of a tag (recorded at chapter-13:1255). This
is that tag.

## Source A — kubernetes.io/releases/release/ (verbatim)

### Cadence

> "Kubernetes releases currently happen approximately three times per year."

### The three phases

> "The release process can be thought of as having three main phases:
> Enhancement Definition, Implementation, Stabilization"

### The cycle, in weeks

> "Normal Dev (Weeks 1-11)"

> "Code Freeze (Weeks 12-14)"

> "Post-Release (Weeks 14+)"

> "**Enhancements Freeze** starts ~4 weeks into release cycle."

> "**Code Freeze** starts in week ~12 and continues for ~2 weeks. Only critical
> bug fixes are accepted into the release codebase during this time."

### Who runs it

> "The process for shepherding enhancements, issues, and pull requests into a
> Kubernetes release spans multiple stakeholders: the enhancement, issue, and
> pull request owner(s); SIG leadership; the Release Team"

## Source B — kubernetes.io/releases/ (verbatim), refreshed

> "The Kubernetes project maintains release branches for the most recent three
> minor releases (1.37, 1.36, 1.35)."

> "Kubernetes 1.19 and newer receive approximately 1 year of patch support.
> Kubernetes 1.18 and older received approximately 9 months of patch support."

Supported releases and end-of-life dates as of this snapshot:
1.37 — End of Life 2027-10-28 · 1.36 — End of Life 2027-06-28 ·
1.35 — End of Life 2027-02-28

*(Supersedes the version list in `k8s-releases-cadence-2026-08-23.md`, which
recorded 1.36/1.35/1.34. See manifest Notes 2. The durable facts — three branches,
~1 year of patch support — are unchanged.)*

## Source C — kubernetes/community sig-release charter (verbatim)

> "Production of Kubernetes releases on a reliable schedule"

> "Ensure there is a consistent group of community members in place to support
> the release process across time."

> "Defining and staffing release roles to manage the resolution of release
> blocking criteria"

> "Defining and driving development processes (e.g. merge queues, cherrypicks)
> and release processes (e.g. burndown meetings, cutting pre-releases)"

> "Managing the creation of release specific artifacts, including: Code branches,
> Binary artifacts, Container Images, Release notes."

> the "Release Engineering subproject", which is "dedicated to the technical
> aspects of Kubernetes releases, for example its tooling and source code
> ownership"

---
DRAFTING NOTE (not from source): the arithmetic §8 needs is now fully sourced and
lands cleanly. Three releases a year × three maintained branches ≈ one year of
patch support — and "approximately 1 year of patch support" is stated
independently on the same page, so the reader's derivation is CONFIRMED by the
source rather than merely permitted by it. That is exactly the "one fact stated
twice" the outline asks for, and it can be shown rather than asserted.

⚠ ONE CAUTION: the "approximately every 15 weeks" figure lives ONLY in
`k8s-releases-cadence-2026-08-23.md`. Today's pages state "approximately three
times per year" and a cycle whose code freeze starts in week ~12 and whose
post-release phase begins at week 14+. If §8 wants a week count, "roughly
fourteen weeks" is what the live release-cycle page supports; "fifteen" must
carry the 08-23 tag. Simplest safe course: teach "three times a year", which is
current, sourced, and the half the exam would test.

The sig-release charter also gives §8 its "subproject" example for free — Release
Engineering — which the reader can hold next to the SIG/subproject definition in
`k8s-community-governance-2026-08-23.md`.
```

### A19 · `cncf-code-of-conduct-2026-08-31.md` (new)
```markdown
---
source_url: "https://github.com/cncf/foundation/blob/main/code-of-conduct.md"
fetched_at: "2026-08-31T09:56:00-0400"
authority: "Cloud Native Computing Foundation"
objectives_covered: ["D4.3"]
concepts_covered: ["code-of-conduct", "kubecon-cloudnativecon"]
---
# CNCF Community Code of Conduct v1.3

## Scope — verbatim

> "This code of conduct applies: within project and community spaces, in other
> spaces when an individual CNCF community participant's words or actions are
> directed at or are about a CNCF project, the CNCF community, or another CNCF
> community participant in the context of a CNCF activity."

## The pledge — verbatim

> "We are committed to making participation in the CNCF community a
> harassment-free experience for everyone, regardless of age, body size, caste,
> disability, ethnicity, level of experience, family status, gender, gender
> identity and expression, marital status, military or veteran status,
> nationality, personal appearance, race, religion, sexual orientation,
> socioeconomic status, tribe, or any other dimension of diversity."

## Reporting and administration — verbatim

> "For other projects, or for incidents that are project-agnostic or impact
> multiple CNCF projects, please contact the CNCF Code of Conduct Committee via
> conduct@cncf.io. Alternatively, you can contact any of the individual members
> of the CNCF Code of Conduct Committee to submit your report. You can expect a
> response within three business days."

---
DRAFTING NOTE (not from source): the scope sentence is the examinable part — the
Code of Conduct applies in project spaces AND at events AND to conduct outside
both when it is directed at the community. Note the register guardrail: this is a
section about volunteers doing organizational work, and the Code of Conduct is
the CNCF's own statement of how it wants people treated. Report it; do not
editorialize on it in either direction.
```

### A20 · `cncf-mentoring-and-community-groups-2026-08-31.md` (new)
```markdown
---
source_url: "https://contribute.cncf.io/contributors/"
fetched_at: "2026-08-31T09:58:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Contributors site)"
objectives_covered: ["D4.3"]
concepts_covered: ["lfx-mentorship", "cloud-native-community-group", "contributor-ladder", "cncf-ambassador"]
---
# CNCF contributor on-ramps — mentorship programs and community groups

Sources the "how you'd join" half of §8. `cncf-landscape-and-community-2026-08-23.md`
names LFX mentorship in a clause; this names the programs.

## Getting started — verbatim

> "Are you new to open source? If so, we recommend checking out our comprehensive
> guide, 'Start Contributing to Open Source'."

The guide covers "communities and projects, how to find them, how to conform to
community standards."

## Mentorship programs — verbatim descriptors

> **LFX Mentorship** — a "mentoring initiative by the Linux Foundation"

> **Google Summer of Code** — a "mentoring program for the open source beginners"

> **Outreachy** — a "mentoring initiative for the communities traditionally
> underrepresented in tech"

## Community groups — verbatim

> "The Cloud Native Computing Foundation supports the worldwide community of the
> Cloud Native Community Groups (CNCGs)."

> "CNCF is currently working on expanding the Cloud Native community worldwide."

CNCGs are listed on community.cncf.io.

## Not fetched

`contribute.cncf.io/mentoring/` returns HTTP 404. Program cadence and stipend
details appear only in CNCF blog posts, which are dated announcements rather than
reference documentation, and are not snapshotted here.

---
DRAFTING NOTE (not from source): §8's participation half now has three named,
sourced on-ramps — mentorship, community groups, and the Kubernetes contributor
ladder from `k8s-community-membership-ladder-2026-08-23.md`. That ladder's Member
requirement ("sponsored by 2 reviewers", "multiple contributions") is the most
concrete possible answer to "how you'd join", and it is genuinely reachable —
which is what makes the outline's "a contributor ladder anyone reading this could
start climbing on a Tuesday afternoon" a factual statement rather than a
rhetorical one. Keep the invitation specific; that is what makes it land.
```

---

## Gaps

Objectives and concepts in the outline for which **no authoritative source was found.** The drafting stage must not invent facts to fill these.

| Gap | Concept(s) | Status and instruction |
|---|---|---|
| **G32 — cost management in D4** | FinOps, OpenCost, KubeCost | **Unresolved, and not resolvable from sources.** No official page states whether cost management survives into the revised D4. The one new data point: TAG Operational Resilience's published scope includes "Resource Optimization, Cost Efficiency, Energy" — so the *topic* is live in CNCF's technical structure, but that says nothing about the exam blueprint. `opencost-overview-2026-08-23.md` remains the only snapshot. **The outline's recommendation (out of this chapter; at most one ungraded clause in §2 beside the Landscape's Observability and Analysis category) is sound and I did not expand the corpus to support more.** Author decision — outline Open Question 3. |
| **Knative Functions** | `knative-functions` | Only `knative-overview-2026-08-23.md` covers it, in one sentence: "leverages Serving and Eventing to provide a simplified experience for building and deploying stateless functions." Adequate for the outline's "one clean sentence each" requirement and for trap #83, which contrasts Serving with Eventing rather than with Functions. **Do not extend Functions beyond that sentence** — there is no deeper source on disk. |
| **KEDA, from KEDA's own docs** | `keda-event-driven-autoscaling` | keda.sh/docs concepts is unexpectedly thin: it defines KEDA and scalers but does **not** state CNCF graduation and does **not** mention scale-to-zero. Every KEDA claim in this chapter therefore rests on **kubernetes.io**, which is authoritative and states both the graduation and the Cron scaler. **Tag KEDA claims to `k8s-docs-autoscaling-and-vpa-2026-08-31.md`, not to keda.sh.** See Notes 4. |
| **Karpenter's CNCF status** | `karpenter` | **No source exists, because there is nothing to source.** Confirmed by absence across karpenter.sh, kubernetes.io and cncf.io/projects. Karpenter is sponsored by Kubernetes SIG Autoscaling; it has no CNCF maturity level. This is now a *resolved* gap — see Notes 3 — but it stays listed so no later stage reads the silence as an oversight and fills it. |
| **Cluster Proportional Autoscaler** | — | Covered in one line of `k8s-docs-autoscaling-2026-08-23.md`; deliberately not expanded. The outline gives it one completeness clause and bars it from graded text. Correct — leave it. |
| **The 60-question and 75% figures** | — | Still unpublished. `provenance-kcna-60-questions-2026-08-23.md` records the provenance. Barred from all graded text, unchanged. |
| **Sub-competency weights within D4** | — | **Confirmed still absent.** CNCF publishes four domain weights and no sub-competency weights. The 7% is this book's authored allocation; the 12% is CNCF's published figure. B1 gap G33 / B2 disclosure #1 stand exactly as the outline states. This is the outline's Open Question 12 and it is *not* a research gap to be closed — it is a permanent property of the source. |

---

## Notes for the author

**1. ⚠ Trap #105 has become a three-way conflict inside kubernetes.io, and the outline's guardrail as written can no longer be satisfied.**

The outline instructs: *"In-place Pod vertical scaling is stable as of a stated Kubernetes version, and VPA does not yet support it directly. Both halves, one source tag, one version number. Do not write 'VPA now resizes in place.'"*

Three official Kubernetes pages now say three different things:

- The **autoscaling overview** says: *"As of Kubernetes 1.37, VPA does not support resizing pods in-place, but this integration is being worked on."*
- The **VPA concept page** lists `InPlaceOrRecreate` and `InPlace` among the VPA's update modes.
- The **v1.35 GA blog** says: *"Vertical Pod Autoscaler (VPA)'s `InPlaceOrRecreate` update mode, which leverages this feature, has graduated to beta."*

The most likely reconciliation is that in-place resize is *stable in Kubernetes* while VPA's integration with it is *beta and incomplete* — but that reconciliation is mine, not the sources', and the guardrail forbids writing it as fact.

**Recommendation: narrow the claim to the half that is unanimous and examinable.** All three pages agree, and the VPA concept page states outright, that **"Unlike HorizontalPodAutoscaler, which is part of the core Kubernetes API, VPA must be installed separately in your cluster."** That is §7's actual Fixed Point, it is the payoff of the pointers laid at Ch 3:606 and Ch 10:678, and it is not in dispute. Drop the in-place claim from graded text entirely, or state only that in-place Pod resize is stable since v1.35 and stop there. This is an associate exam; VPA's update-mode maturity is well below the tier, and the conflict makes it the single most likely place for this chapter to ship a wrong sentence. Flagged rather than decided — outline Open Question guardrail, §7.

**2. Two cached snapshots have drifted, both harmlessly, and one is worth knowing about.**

`k8s-releases-cadence-2026-08-23.md` lists supported releases as 1.36 / 1.35 / 1.34. Today they are **1.37 / 1.36 / 1.35** — v1.37 "Garhwal" shipped 2026-08-26, five days ago. The durable facts §8 teaches (three maintained branches, ~1 year of patch support, three releases a year) are **unchanged**, which is itself the lesson: the *count* is stable, the *numbers* are not. `k8s-release-cycle-and-cadence-2026-08-31.md` carries the current list. If §8 names specific versions at all — and it need not — use the new tag.

Second drift: the autoscaling page's VPA sentence has re-dated from v1.35 to 1.37 while keeping its wording. Covered in Notes 1.

**3. Open Question 5 (Karpenter) is answered, and the answer is better than the outline's fallback.**

The outline recommended naming Karpenter as a node autoscaler with no affiliation claim *unless* research returned a tagged source. Research returned one: kubernetes.io states that **Cluster Autoscaler and Karpenter are "the two Node autoscalers currently sponsored by SIG Autoscaling."** So §7 can make a positive, sourced, correct statement — Karpenter is a Kubernetes SIG Autoscaling project — instead of a conspicuous silence. It still must make **no CNCF maturity claim**, because none exists in any official source. karpenter.sh carries an AWS copyright footer and the repository lives under `kubernetes-sigs`.

Small bonus for §8: SIG Autoscaling appearing in §7 and the SIG roster appearing in §8 means the reader meets the same organizational unit twice, in two registers, nine pages apart. That is free reinforcement for the competency B1 says is most under-studied.

**4. Every KEDA claim now rests on kubernetes.io, and that is the right call — but it should be a conscious one.**

keda.sh's own concepts documentation defines KEDA and its scalers but states neither CNCF graduation nor scale-to-zero. kubernetes.io states plainly: *"KEDA is a CNCF-graduated project."* Per the stage's priority order, vendor documentation outranks nothing here — both are official, and the Kubernetes docs are the stronger authority for a Kubernetes exam. Tag KEDA to `k8s-docs-autoscaling-and-vpa-2026-08-31.md`. Worth noting because it is mildly surprising that the project's own docs are the weaker source.

**5. Open Question 4 (the graduated roster) — the shape of the risk is now measurable.**

`cncf-who-we-are-2026-08-23.md` counts **227 projects** across four categories. `cncf-project-maturity-levels-2026-08-23.md` lists **38 graduated projects** as of 2026-08-23. The outline's proposed six — containerd, CoreDNS, etcd, Helm, Prometheus, Argo — are **all present on that list and all met by name earlier in this book**, so the recommendation is sound and executable as written. Two observations:

- Six of thirty-eight is visibly a sample, which is helpful: a reader shown six of thirty-eight is much less likely to mistake the six for the set than a reader shown six of an unstated total. **Consider naming the count (38) beside the six.** It costs four words and does most of the work the "don't memorize this" sentence is doing.
- **Istio, Envoy, Knative and KEDA are also on the graduated list**, and this chapter names all four in §5, §6 and §7. They arrive with their maturity already stated in their own snapshots. So §2's roster and §5–§7's projects will corroborate each other for an attentive reader — which is good, and worth not accidentally contradicting.

**6. §2's ladder has a fourth level the outline does not account for.**

The TOC's own process document names **Archived** alongside Sandbox, Incubation and Graduated, and `cncf-who-we-are-2026-08-23.md` independently counts projects across all four. The three-rung progression is still correct as a *progression* — Archived is a terminal state, not a rung climbed — but a reader who opens cncf.io/projects will see four categories and wonder whether the book left one out. One clause naming Archived as where projects go when they stop, explicitly outside the ladder, would close it cheaply. `ch17-fig05-cncf-maturity-levels` is a progression figure and should probably stay three-rung regardless. Author's call; recorded so it is not decided silently at drafting.

Minor, same section: the TOC process doc says "**Incubation**" (the process); cncf.io/projects says "**Incubating**" (the level). §2's title is fixed to *Incubating* by two shipped pointers, so that is settled — but the term ledger should record the pair so a later stage does not "correct" one to the other.

**7. §8's Committees: the roster is sharper than the outline's plan assumes.**

`sig-list.md` lists exactly **three** Committees — Code of Conduct, Security Response, and **Steering**. The outline's §8 plan treats Steering as a separate fourth body alongside SIGs, WGs and Committees. Both framings have textual support (the governance doc says Committees "are formed by the steering committee", which cannot apply to Steering itself), but a reader who checks will find Steering listed *as* a Committee.

**Recommendation: name all three Committees, mark them closed-membership, and note that Steering charters the other two and holds overall governance.** That is accurate under both framings, it is more concrete than an abstract four-way taxonomy, and — usefully — "Code of Conduct" and "Security Response" are self-evidently topics requiring discretion, which makes the closed-membership asymmetry *obvious* rather than merely asserted. Trap #109 is the chapter's cleanest item and this makes it teach itself.

**8. Two optional additions, both cheap, neither required.**

- **Knative Serving's default autoscaler is the KPA, not the HPA**, and Serving can be configured to use the HPA instead. Arguably above associate tier — but §6 already lists `Ch 17 §7 — four things that scale` as a cross-bearing out, and this is the actual mechanical link between the two sections. One clause would make that cross-bearing load-bearing instead of decorative.
- **The CNCF blog states that CNCF's technical groups were originally called SIGs and were "later renamed Technical Advisory Groups."** This is the historical *reason* TAGs and SIGs are confusable, in CNCF's own words, and it is far better teaching than a warning would be. It stays inside Ethical Guardrail #8 because it explains a cause rather than asserting a testing frequency — but the sentence must not slide into "which is why this is so commonly tested." Trap #112 is `[inferred]` and stays `[inferred]`.

**9. §5's scope guardrail survived contact with the sources, but two fetched quotations carry Istio CRD names.** The ambient-mode page's L7 description mentions `VirtualService`, and the security page describes permissive mode, which is configured via `PeerAuthentication`. Both are quoted in the snapshots because the snapshots are evidence and must be faithful. **Neither belongs in the chapter.** Permissive mode is safe to name as a *concept* in a clause; VirtualService is not, and the outline's rule — "if a paragraph names an Istio CRD, it has left the tier" — should be applied to the drafted prose regardless of what the snapshots contain.

**10. The CNCF glossary's service-mesh entry offers a third architectural model — "Sidecarless", built on eBPF — alongside Istio's sidecar and ambient modes.** It is quoted in `cncf-glossary-service-mesh-2026-08-31.md` for fidelity. eBPF is barred from graded text by the B7 Part 2 ruling (outline Open Question 11), and importing a third model would also break trap #102's clean two-mode contrast. **§5 uses Istio's sidecar/ambient framing.** The glossary entry's first three paragraphs are the quotable part and are the vendor-neutral definition the outline asked for.

**11. Two URL changes worth recording for future stages.** `cncf.io/tags/` now returns **HTTP 404**; the authoritative current TAG home is `contribute.cncf.io/community/tags/`. `contribute.cncf.io/mentoring/` also returns 404; contributor on-ramp material lives at `contribute.cncf.io/contributors/`. Neither affects a shipped chapter — no book text cites either URL — but a later research stage would otherwise rediscover both.

---

*Stage 2 complete. Twenty new snapshots; sixteen existing snapshots verified rather than re-fetched; four of the outline's five named research targets closed and the fifth (Kubernetes history, G14) confirmed already sourced. Two of the outline's twelve open questions are answered by the research — **Q5 (Karpenter's affiliation: SIG Autoscaling, no CNCF maturity level)** and, in the negative, **Q3 (no source resolves G32; the outline's out-of-scope recommendation stands)**. One new blocker is raised: **trap #105's in-place-resize claim is contradicted between three kubernetes.io pages and should be narrowed to the VPA-is-an-add-on half**, which is unanimous and is what §7 actually needs. Two smaller structural findings — the fourth maturity level (Archived) and Steering's listing as a Committee — are flagged for the author rather than decided.*
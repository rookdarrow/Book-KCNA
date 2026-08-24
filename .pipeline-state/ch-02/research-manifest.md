Writes are blocked in this session, so — as with Chapter 1 — the manifest below **is** the artifact, with snapshot bodies embedded ready to be written.

Research is complete. **G29 is now fully closed**, `ch02-fig02` is unblocked, and §4 gained the sourced sentence the whole Ch 17 Zenith rests on.

---

# Research Manifest — KCNA Chapter 2

> **Harness note.** This stage could not write files. `Write` was denied by permission
> prompt (non-interactive), and Bash redirection to `Book-KCNA/sources/` was blocked by
> the sandbox in both forward- and back-slash forms — despite `C:\dev\lodestar\Book-KCNA`
> appearing in the session's allowed-directory list. Same condition Chapter 1's Stage 2
> hit. **The 17 new snapshots in Appendix A must be written to `../Book-KCNA/sources/`
> before Stage 3 runs.**

## Existing snapshots reusable for Chapter 2

The book-outline stage cached 87 snapshots on 2026-08-23. Chapter 2 uses six, all verified as-is:

| Snapshot | Authority | Serves | Status |
|---|---|---|---|
| `k8s-docs-containers-2026-08-23.md` | Kubernetes | §1 repeatability/co-location, §2 immutability, §4 runtime responsibility | OK |
| `k8s-docs-images-2026-08-23.md` | Kubernetes | §3 naming/defaults/tag-vs-digest, §6 all policies + defaults + 300s cap | OK — carries §6 entire |
| `k8s-docs-overview-2026-08-23.md` | Kubernetes | §1 VM contrast; "not monolithic… optional and pluggable" | OK |
| `oci-overview-2026-08-23.md` | OCI (LF) | §5 founding, three specs, download→unpack→run, runC donation | OK |
| `k8s-docs-runtime-class-2026-08-23.md` | Kubernetes | §7 entire — motivation, Kata/gVisor, handlers, overhead | OK — G30 closed, confirmed |
| `buildpacks-concepts-2026-08-23.md` | CNB (CNCF graduated) | §2 build practices | OK |

`sigstore-overview-2026-08-23.md` remains cached and remains **Chapter 12's**, per the outline's scope boundary.

## New snapshots (Appendix A)

| # | Snapshot | Authority | Concepts |
|---|---|---|---|
| A1 | `k8s-docs-cri-2026-08-24.md` | Kubernetes | `cri`, `kubelet-runtime-boundary`, `pluggable-interfaces` |
| A2 | `k8s-docs-container-runtimes-setup-2026-08-24.md` | Kubernetes | `container-runtime`, `containerd`, `cri-o` |
| A3 | `k8s-blog-dockershim-faq-2026-08-24.md` | Kubernetes project | trap #34, `cri`, `oci` |
| A4 | `oci-image-spec-overview-2026-08-24.md` | OCI | `oci-image-spec`, `image-layers` |
| A5 | `oci-image-spec-layers-2026-08-24.md` | OCI | `image-layers` |
| A6 | `oci-image-spec-manifest-2026-08-24.md` | OCI | `image-layers`, `image-digest`, `base-image` |
| A7 | `oci-distribution-spec-2026-08-24.md` | OCI | `oci-distribution-spec`, `registry`, `image-digest` |
| A8 | `oci-runtime-spec-bundle-2026-08-24.md` | OCI | `filesystem-bundle`, `oci-runtime-spec` |
| A9 | `docker-docs-image-layers-2026-08-24.md` | Docker Inc. | `image-layers`, `immutability` |
| A10 | `docker-docs-build-cache-2026-08-24.md` | Docker Inc. | `image-layers` (caching/dedup) |
| A11 | `docker-docs-multi-stage-2026-08-24.md` | Docker Inc. | `base-image`, build practice |
| A12 | `docker-docs-build-best-practices-2026-08-24.md` | Docker Inc. | `base-image`, `image-digest` |
| A13 | `docker-docs-what-is-a-container-2026-08-24.md` | Docker Inc. | `shared-kernel-isolation`, `container-vs-virtual-machine` |
| A14 | `cncf-glossary-container-2026-08-24.md` | **CNCF (exam authority)** | `container`, `shared-kernel-isolation` |
| A15 | `cncf-glossary-container-image-2026-08-24.md` | **CNCF (exam authority)** | `container-image`, `immutability` |
| A16 | `cncf-glossary-containerization-2026-08-24.md` | **CNCF (exam authority)** | `container-vs-virtual-machine`, `immutability` |
| A17 | `containerd-cri-o-runc-2026-08-24.md` | containerd / CRI-O / runC projects | `containerd`, `cri-o`, `runc` |

---

## Findings that change the chapter

### 1. Open Question #1 resolves — and better than either option offered

The outline framed this as a binary: keep the "kernel" sharpening, or soften both chapters to the snapshot's "operating system." The evidence supports a third, stronger answer: **both registers are authoritative, and they differ by speaker.**

| Source | Authority tier | Wording |
|---|---|---|
| `glossary.cncf.io/container/` | **Exam authority** | "Containers share the same **operating system** and its machine resources" |
| `kubernetes.io/docs/concepts/overview/` | Vendor (subject) | "relaxed isolation properties to share the **Operating System (OS)** among the applications" |
| `docs.docker.com/.../what-is-a-container/` | Vendor | "they all share the same **kernel**" · "A VM is an entire operating system with its own kernel" |

So the sharpening is **no longer unsourced** — Docker's docs state it plainly, and Docker's VM sentence is the sharpest articulation of the contrast anywhere in the cache. But note this stage's own rule ("prefer the exam authority… the exam tests what the authority says"): the CNCF glossary says *operating system*, so exam items are likelier to use OS phrasing.

There is also an internal Kubernetes warrant for the kernel framing already sitting in the cache: `k8s-docs-runtime-class` says a sandboxed runtime uses "a **user-space kernel** (such as gVisor)" — phrasing that only makes sense if the ordinary case is the *host's* kernel. §1 and §7 can be made to agree on this without reaching outside the cache.

**Recommendation.** Keep the sharpening, cite A13 for it, and have §1 name both registers in one clause — kernel as the mechanism, "shares the OS" as the phrasing the reader will meet on the exam. That closes Chapter 1's live `AUTHOR-REVIEW` at line 140 by *sourcing* it rather than softening it, and it makes the two chapters agree. This is the one decision that should be made before drafting, because it is the chapter's most-quoted sentence.

### 2. G29 is fully closed — Open Question #2 resolves to option (a)

The outline's fallback (b) — narrow §2, describe layers qualitatively, reduce `ch02-fig02` to its digest half, rename the anchor before Stage 10 — **is no longer needed.** Do not rename the anchor.

Layer mechanics are now sourced from the standards body *and* the vendor:

- **What a layer is** — OCI: "a changeset that describes a container's filesystem" (A4); "One or more layers are applied on top of each other to create a complete filesystem" (A5); "Each layer in an image contains a set of filesystem changes - additions, deletions, or modifications" (A9)
- **Stacking and order** — OCI: "The array MUST have the base layer at index 0. Subsequent layers MUST then follow in stack order" and "The final filesystem layout MUST match the result of applying the layers to an empty directory" (A6)
- **Sharing / dedup** — Docker: "allows layers to be reused between images," which "reduce[s] the amount of storage and bandwidth required to distribute the images" (A9). **This is Soundings Q4's answer key, verbatim.**
- **Caching** — Docker: "Each instruction in this Dockerfile translates to a layer"; "Once a layer changes, then all downstream layers need to be rebuilt as well" (A10). This is the sourced warrant for the outline's "the order of build steps has consequences."
- **Multi-stage** — Docker: "each of them begins a new stage of the build"; "None of the build tools required to build the application are included in the resulting image" (A11)
- **Base-image selection** — Docker: "A small image with minimal dependencies can considerably lower the attack surface"; a minimal base "shrinks the size of your image and minimizes the number of vulnerabilities introduced through the dependencies" (A12). **This is the ⚓ Worth Securing beat §2 planned, now quotable.**

`ch02-fig02` can be specced in full, including the shared-base left half. Record option (a) as taken so Stage 10 doesn't re-litigate it.

**Bonus for the §2→§3 cross-bearing.** A12 also carries "To fully secure your supply chain integrity, you can pin the image version to a specific digest" — so §2's base-image material now hands off to §3's digest Fixed Point on a sourced sentence rather than an authorial pivot.

### 3. §4 was the thinnest-sourced section in the chapter. It is now the best-sourced.

Before this stage, the most-retrieved concept in the book — the CRI boundary, retrieved in Ch 3, Ch 8, Ch 17, and half the secondary Zenith — rested on **one clause** in `k8s-docs-containers` ("any other implementation of the Kubernetes CRI"). `kubernetes.io/docs/concepts/architecture/cri/` was never fetched.

It hands the chapter its thesis sentence, from the authority, verbatim:

> "The CRI is a plugin interface which enables the kubelet to use a wide variety of container runtimes, without having a need to recompile the cluster components."

That is cross-cutting theme 6 stated by Kubernetes itself. The outline asks §4 to "plant the *shape* — 'Kubernetes defines an interface and lets the ecosystem implement it' — as a named idea." **Quote this sentence to do it.** Naming the pattern on a sourced line rather than an authorial one is what will let Ch 9, Ch 11, and Ch 6 each say "same move again" and Ch 17 collect all four.

Also newly available for Fixed Point #2's chain: "The Container Runtime Interface (CRI) is the main protocol for the communication between the kubelet and Container Runtime" and "The kubelet acts as a client when connecting to the container runtime via gRPC."

⚠ **Scope caution — the CRI page will overfeed the drafting stage.** It also contains `--container-runtime-endpoint`, the v1-CRI-API requirement for v1.26+, gRPC's 16 MiB message limit, and an alpha `CRIListStreaming` feature gate. **None of that is KCNA material** for a junior-tier associate chapter. Take the plugin-interface sentence and the kubelet-as-client sentence; leave the rest in the snapshot. A2's cgroup-driver material is likewise sourced-but-out-of-scope.

### 4. The chapter's hardest discrimination now has a one-sentence anchor from a primary source

§5's ⚠ Navigational Hazards has to draw the OCI/CRI boundary. CRI-O's own front page draws it in a single sentence containing both acronyms, each in its correct plane:

> "CRI-O is an implementation of the Kubernetes CRI (Container Runtime Interface) to enable using OCI (Open Container Initiative) compatible runtimes."

Anchor the hazard on that rather than asserting the boundary in the book's voice. It is also the cleanest available answer to Bearings #2 question 3.

Two more gap-closers in A17:

- **containerd → runC is now sourced.** containerd's README: "Most interactions with the Linux and Windows container feature sets are handled via runc." Previously that hop in `ch02-fig04` rested only on OCI's "cornerstone" sentence about the donation — which establishes *provenance*, not *use*. Fixed Point #2's chain is now sourced end to end.
- **§5 → §7 gets a sourced bridge.** CRI-O: "Today it supports runc and Kata Containers as the container runtimes but any OCI-conformant runtime can be plugged in principle." Kata appears as an OCI runtime slotting under CRI — so §7 is visibly the *same socket* from §4, not a new mechanism. That is a better setup for §7 than the outline currently plans, and it costs one clause.

### 5. Trap #34's substance is `[source]`, not `[inferred]` — but the framing constraint still holds

The outline twice instructs that B1 trap #34 ("Docker is the container runtime Kubernetes uses") is `[inferred]`, so it must be written as "easy to confuse," never "frequently tested." **Keep that constraint** — it is a claim about *exam frequency*, and nothing found here speaks to frequency.

But the *misconception itself* is documented by the Kubernetes project, which published an FAQ about it (A3):

> "Early versions of Kubernetes only worked with a specific container runtime: Docker Engine."
> "Docker Engine doesn't implement that interface (CRI), so the Kubernetes project created special code to help with the transition, and made that *dockershim* code part of Kubernetes itself."
> "The dockershim code was always intended to be a temporary solution (hence the name: shim)."
> "Yes, the images produced from `docker build` will work with all CRI implementations. All your existing images will still work exactly the same."

So §4's 🪝 Snag can rest on documented history rather than assertion. And that last line is the single best one-line answer key for **Soundings Q5** — it answers "is Docker required?" with "no, and here is the reason it *looks* required," while quietly reinforcing §5: the build format is standardized, so the builder need not be the runtime.

⚠ Two cautions. The FAQ is dated **2022-02-17** and is a blog post, not current docs — authoritative but historical; drafting must not present dockershim as current. And it must not become a dockershim-removal history lesson: **B2 assigns the historical progression to Chapter 3.** One Snag, one Soundings answer line, stop.

### 6. §3 and §5 can now cite the specification instead of inferring from it

`oci-distribution-spec` (A7) supplies definitions §5 previously had to paraphrase — and one that is Fixed Point #1's other half, stated by the standards body:

> "**Digest**: a unique identifier created from a cryptographic hash of a Blob's content."
> "**Registry**: a service that handles the required APIs defined in this specification."
> "**Push**: the act of uploading blobs and manifests to a registry" · "**Pull**: the act of downloading blobs and manifests from a registry"

This upgrades §5's back-bearing to §3 from "distribution-spec standardizes the API for distributing images" to a spec-level definition of what a registry *is*. It also means §3's digest Fixed Point is corroborated by two independent authorities (Kubernetes' "a hash of the image's content" and OCI's "cryptographic hash of a Blob's content"), which is exactly the evidentiary weight a Fixed Point should carry.

`filesystem-bundle` is likewise no longer a bare phrase. A8: "a set of files organized in a certain way, and containing all the necessary data and metadata for any compliant runtime to perform all standard operations against it," with `config.json` REQUIRED at the bundle root. §5's three-beat flow now has a defined middle artifact.

### 7. One soft evidentiary problem: trap #30 is tagged `[source]` and no snapshot states it verbatim

B1 tags trap #30 ("a container image includes the OS kernel") as `[source]`, and §2 is built to defuse it. **No cached or newly-fetched snapshot says "a container image does not contain a kernel."**

The claim is sound and entailed — if containers share the host kernel (A13), the image needn't ship one; and CNCF's glossary enumerates image contents without a kernel (A15): "a single executable binary file, system libraries, system tools, environment variables, and other required platform settings." So §2 should **build** the negative space from the kernel-sharing sentence, not assert it as a quoted fact.

Flagging it because a downstream fact-accuracy audit checking §2 against the snapshots will go looking for a verbatim statement and not find one. B1's `[source]` tag on #30 is optimistic; treat it as entailed-from-source.

---

## Gaps

| Gap | Status | Effect on Chapter 2 |
|---|---|---|
| **G29 — layer mechanics, caching, multi-stage, base-image guidance** | **CLOSED** | A4–A6, A9–A12. `ch02-fig02` unblocked in full; anchor keeps its name. Open Question #2 → option (a). |
| **G30 — RuntimeClass motivation** | **CLOSED** (confirmed, no re-flag) | §7 drafts from cache. |
| **§4 CRI sourcing** | **CLOSED** — was an unlisted gap | A1, A2, A3, A17. Was one clause; now the best-sourced section. |
| **`filesystem-bundle` definition** | **CLOSED** — was an unlisted gap | A8. |
| **Trap #30 verbatim statement** | **OPEN — soft, non-blocking** | Entailed, not quoted. See finding 7. Do not cite as a quotation. |
| **Containerization sub-competency weight** | **OPEN — unchanged** | Confirms Open Question #8. The 9%, the "heavy" band, and 25 Practice Questions remain authored judgment, disclosed at book level. No in-chapter restatement needed. |
| **Epigraph source (Open Question #9)** | **OPEN — blocking the epigraph only** | See below. |

### Open Question #9 — the McLean epigraph could not be sourced

No authoritative direct quote from Malcom McLean was located. Every hit was a third-party commercial logistics blog, inadmissible under this stage's rules. `iso.org` returns **403** to WebFetch and the National Inventors Hall of Fame slug 404s, so neither institutional route closed either.

One genuinely apt claim surfaced repeatedly and **must not be drafted**: that McLean released the container patent royalty-free to ISO. If true it is a near-perfect §8 fact — the interface standardized and then given away — but it appears only in third-party sources and I could not verify it.

**Recommendation: use the original Lodestar epigraph.** Part 15 prefers attributed quotes, but Part 15 cannot prefer an unverifiable one, and the author's own note says "verify any attributed quote against a source before it ships." If you want the attributed route, the two-minute manual path is **ISO 668** (*Series 1 freight containers — Classification, dimensions and ratings*) from a browser session — a sourced standardization fact exactly parallel to OCI governing the image format, which would serve §8 better than a quote anyway.

---

## Notes for the author

**The exam authority's own glossary blurs the boundary §5 exists to draw.** A15 states that images are "downloaded and run as an isolated process using a Container Runtime Interface (CRI)." That is loose — CRI is the kubelet↔runtime protocol, not the thing that runs an image. **Do not quote that sentence.** Use A15 for the image *definition* ("an immutable, static file containing the dependencies for the creation of a container" is excellent Fixed Point support, and "must follow the standard schema defined by the Open Container Initiative (OCI)" is sourced §5 material from the authority itself). Source CRI from A1. Worth knowing that if an exam item ever leans on the glossary's phrasing, a reader who learned the precise boundary may second-guess a correct answer — §5's hazard should be crisp enough that they can recognize loose phrasing without doubting the mechanism.

**Two `[source]`-quality corroborations for §2's immutability beat**, beyond the cached `k8s-docs-containers` rule. A9: "container images are composed of layers. And each of these layers, once created, are immutable." A16, from the exam authority: containers "are always reset to their initial state which eliminates configuration drift," and VMs by contrast "can experience configuration drift, violating immutability principles." That second one is a sourced framing of *why* immutability matters — and it comes from CNCF, which makes it the strongest available support for the chapter's organizing principle.

**A16 also pre-empts a §1/Ch 3 scope collision.** The CNCF containerization entry frames the pre-container world as VMs on bare metal needing a hypervisor. That is close to Chapter 3's deployment-eras territory. §1 may use A16 for the *architectural* contrast; the timeline stays Chapter 3's, per the outline's own boundary.

**Extraction fidelity.** WebFetch summarizes through a small model. Every string I present inside quotation marks in Appendix A came back quoted from the fetch. A handful of passages came back paraphrased, and I have marked each one inline as `[EXTRACTOR SUMMARY — NOT VERBATIM]`. **Do not cite those as quotations without re-verifying against the live URL** — they are in the snapshots for orientation, not as evidence. Affected: A11 (partially), A12 (`apt-get` guidance), A16 ("Problem it addresses"), A9 (layer ordering), A17 (runC — only one fragment came back quoted).

**Depth available but almost certainly out of scope.** A5 carries whiteout files (`.wh.` prefix) and A9 carries union filesystems. Both are real and both are below KCNA's waterline. They would suit a `> 🔭 **Closer Look:**` if §2 has room, and should be cut without regret otherwise. Same judgment as the outline already applied to Buildpacks' reproducible-layer export.

**Unchanged by research.** §8 correctly needs no sources and must not acquire any. §6 is fully sourced from `k8s-docs-images` and needs nothing new. Open Questions #4 (figure ordinals), #5 (Bearings 10→12), #7 (era placement), and #10 (Ch 17 reciprocal) are editorial and organizational calls that research does not bear on. **#6 stands: re-run B3 before Ch 3's Stage 1.** Chapter 2 has no retrieval obligations, but Chapter 3 opens the schedule drawing two named anchors from this chapter, and both of those anchors — the CRI boundary and image immutability — are now well enough sourced that B3 has real material to schedule against.

---

## Appendix A — snapshot files to write

### A1 · `k8s-docs-cri-2026-08-24.md`

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/architecture/cri/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.4"]
concepts_covered: ["cri", "container-runtime", "kubelet-runtime-boundary", "pluggable-interfaces"]
---
# Container Runtime Interface (CRI) — kubernetes.io/docs/concepts/architecture/cri/

> CHAPTER 2 §4 PRIMARY SOURCE. This page was not fetched by the book-outline
> stage; before it, the CRI rested on one clause in k8s-docs-containers.

## The thesis sentence (use this one)

"The CRI is a plugin interface which enables the kubelet to use a wide variety of
container runtimes, without having a need to recompile the cluster components."

## Definition and requirement

"You need a working container runtime on each Node in your cluster, so that the
kubelet can launch Pods and their containers."

"The Container Runtime Interface (CRI) is the main protocol for the communication
between the kubelet and Container Runtime."

"The Kubernetes Container Runtime Interface (CRI) defines the main gRPC protocol
for the communication between the node components kubelet and container runtime."

## The API

FEATURE STATE: Kubernetes v1.23 [stable]

"The kubelet acts as a client when connecting to the container runtime via gRPC.
The runtime and image service endpoints have to be available in the container
runtime, which can be configured separately within the kubelet by using the
`--container-runtime-endpoint` command line flag."

"For Kubernetes v1.26 and later, the kubelet requires that the container runtime
supports the `v1` CRI API. If a container runtime does not support the `v1` API,
the kubelet will not register the node."

## Upgrading

"When upgrading the Kubernetes version on a node, the kubelet restarts. If the
container runtime does not support the `v1` CRI API, the kubelet will fail to
register and report an error."

## List streaming

FEATURE STATE: Kubernetes v1.36 [alpha] (disabled by default)

The standard CRI list RPCs (ListContainers, ListPodSandbox, ListImages) return all
results in a single unary response; with the `CRIListStreaming` feature gate the
kubelet uses server-side streaming RPCs. "If the container runtime does not support
streaming RPCs, the kubelet automatically falls back to the standard unary RPCs for
backward compatibility."

## SCOPE WARNING FOR DRAFTING

Chapter 2 is a junior-tier associate chapter. Use ONLY the thesis sentence, the
definition, and "the kubelet acts as a client". The following are sourced here but
are NOT KCNA material and must not reach the draft:
  - --container-runtime-endpoint
  - the v1 CRI API requirement / version skew
  - gRPC message size limits
  - the CRIListStreaming feature gate
```

### A2 · `k8s-docs-container-runtimes-setup-2026-08-24.md`

```markdown
---
source_url: "https://kubernetes.io/docs/setup/production-environment/container-runtimes/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.4"]
concepts_covered: ["container-runtime", "containerd", "cri-o", "cri"]
---
# Container Runtimes — kubernetes.io/docs/setup/production-environment/container-runtimes/

## Requirement

"You need to install a container runtime into each node in the cluster so that Pods
can run there."

Tooltip definition carried on that link: "The container runtime is the software that
is responsible for running containers."

"Kubernetes 1.36 requires that you use a runtime that conforms with the Container
Runtime Interface (CRI)."

## Runtimes documented on this page

containerd · CRI-O · Docker Engine · Mirantis Container Runtime

(Docker Engine appears here only via cri-dockerd; see
k8s-blog-dockershim-faq-2026-08-24.md for the history.)

## CRI socket paths

"On Linux the default CRI socket for containerd is `/run/containerd/containerd.sock`.
On Windows the default CRI endpoint is `npipe://./pipe/containerd-containerd`."

## Cgroup drivers — OUT OF SCOPE FOR CHAPTER 2, recorded for completeness

"Both the kubelet and the underlying container runtime need to interface with control
groups to enforce resource management for pods and containers and set resources such
as cpu/memory requests and limits. To interface with control groups, the kubelet and
the container runtime need to use a cgroup driver. It's critical that the kubelet and
the container runtime use the same cgroup driver and are configured the same."

DO NOT draft cgroup drivers into Chapter 2.
```

### A3 · `k8s-blog-dockershim-faq-2026-08-24.md`

```markdown
---
source_url: "https://kubernetes.io/blog/2022/02/17/dockershim-faq/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Kubernetes project (official project blog) — published 2022-02-17"
objectives_covered: ["D1.4"]
concepts_covered: ["cri", "containerd", "oci", "container-runtime"]
---
# Dockershim Removal FAQ — Kubernetes project blog

> HISTORICAL DOCUMENT, dated 2022-02-17. Authoritative (Kubernetes project
> publication) but NOT current documentation. Do not present dockershim as current.
> Serves Chapter 2 Soundings Q5, §4's Snag, and B1 trap #34.

## Why "Docker" looks like the runtime

"Early versions of Kubernetes only worked with a specific container runtime: Docker
Engine. Later, Kubernetes added support for working with other container runtimes.
The CRI standard was created to enable interoperability between orchestrators (like
Kubernetes) and many different container runtimes. Docker Engine doesn't implement
that interface (CRI), so the Kubernetes project created special code to help with the
transition, and made that dockershim code part of Kubernetes itself."

"The dockershim code was always intended to be a temporary solution (hence the name:
shim)."

## Docker is not the ecosystem

"Docker popularized the Linux containers pattern and has been instrumental in
developing the underlying technology, however containers in Linux have existed for a
long time. The container ecosystem has grown to be much broader than just Docker.
Standards like OCI and CRI have helped many tools grow and thrive in our ecosystem,
some replacing aspects of Docker while others enhance existing functionality."

## Images built with Docker still run — SOUNDINGS Q5 ANSWER KEY LINE

"Yes, the images produced from `docker build` will work with all CRI implementations.
All your existing images will still work exactly the same."

## Why dockershim was removed

"In fact, maintaining dockershim had become a heavy burden on the Kubernetes
maintainers."

"Additionally, features that were largely incompatible with the dockershim, such as
cgroups v2 and user namespaces are being implemented in these newer CRI runtimes.
Removing the dockershim from Kubernetes allows further development in those areas."

## FRAMING CONSTRAINT (unchanged)

B1 trap #34 remains [inferred] AS TO EXAM FREQUENCY. Nothing on this page speaks to
how often the exam tests it. Write "easy to confuse", never "frequently tested".
What this page DOES license is describing the confusion as documented and
historically grounded rather than merely asserted.

## SCOPE GUARD

B2 assigns the historical deployment progression to Chapter 3. Chapter 2 gets one
Snag and one Soundings answer line from this page. Not a history section.
```

### A4 · `oci-image-spec-overview-2026-08-24.md`

```markdown
---
source_url: "https://raw.githubusercontent.com/opencontainers/image-spec/main/spec.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Image Format Specification"
objectives_covered: ["D1.4"]
concepts_covered: ["oci-image-spec", "image-layers", "image-digest", "container-image"]
---
# OCI Image Format Specification — overview

## What the specification defines

"This specification defines an OCI Image, consisting of an image manifest, an image
index (optional), a set of filesystem layers, and a configuration."

## Understanding the specification — the components

- "Image Manifest - a document describing the components that make up a container image"
- "Image Index - an annotated list of manifests"
- "Image Layout - a filesystem layout representing the contents of an image"
- "Filesystem Layer - a changeset that describes a container's filesystem"
- "Image Configuration - a document determining layer ordering and configuration of
  the image suitable for translation into a runtime bundle"

## How they fit together

"At a high level the image manifest contains metadata about the contents and
dependencies of the image including the content-addressable identity of one or more
filesystem layer changeset archives that will be unpacked to make up the final
runnable filesystem. The image configuration includes information such as application
arguments, environments, etc. The image index is a higher-level manifest which points
to a list of manifests and descriptors."

## Note for §5

"suitable for translation into a runtime bundle" is the spec's own link from
image-spec to runtime-spec. See oci-runtime-spec-bundle-2026-08-24.md.
```

### A5 · `oci-image-spec-layers-2026-08-24.md`

```markdown
---
source_url: "https://raw.githubusercontent.com/opencontainers/image-spec/main/layer.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Image Format Specification, Image Layer Filesystem Changeset"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "oci-image-spec"]
---
# OCI Image Layer Filesystem Changeset

> CLOSES THE OPEN HALF OF G29 (layer mechanics). Chapter 2 §2 and ch02-fig02.

## What a layer is

"This document describes how to serialize a filesystem and filesystem changes like
removed files into a blob called a layer. One or more layers are applied on top of
each other to create a complete filesystem."

## Change types

"Types of changes that can occur in a changeset are: Additions, Modifications,
Removals. Additions and Modifications are represented the same in the changeset tar
archive."

## Tar archives and media types

"Layer Changesets for the media type `application/vnd.oci.image.layer.v1.tar` MUST be
packaged in tar archive."

"Layer Changesets for the media type `application/vnd.oci.image.layer.v1.tar` MUST NOT
include duplicate entries for file paths in the resulting tar archive."

"The media type `application/vnd.oci.image.layer.v1.tar+gzip` represents an
`application/vnd.oci.image.layer.v1.tar` payload which has been compressed with gzip."

## Applying changesets

"Layer Changesets of media type `application/vnd.oci.image.layer.v1.tar` are applied,
rather than simply extracted as tar archives. Applying a layer changeset requires
special consideration for the whiteout files."

## Whiteout files — DEPTH, likely out of scope

"A whiteout file is an empty file with a special filename that signifies a path should
be deleted. A whiteout filename consists of the prefix `.wh.` plus the basename of the
path to be deleted."

Below KCNA's waterline. Suitable for a 🔭 Closer Look at most; cut without regret.
```

### A6 · `oci-image-spec-manifest-2026-08-24.md`

```markdown
---
source_url: "https://raw.githubusercontent.com/opencontainers/image-spec/main/manifest.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Image Format Specification, Image Manifest"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "image-digest", "base-image", "oci-image-spec"]
---
# OCI Image Manifest Specification

## Stated goals

"content-addressable images, by supporting an image model where the image's
configuration can be hashed to generate a unique ID for the image and its components"

The manifest is also to be "translatable to the OCI Runtime Specification".

[EXTRACTOR SUMMARY — NOT VERBATIM] A third goal concerns multi-architecture images
via a "fat manifest" referencing platform-specific image manifests. Re-verify before
citing.

## Required fields

- schemaVersion: "This REQUIRED property specifies the image manifest schema version.
  For this version of the specification, this MUST be `2`"
- config: "This REQUIRED property references a configuration object for a container,
  by digest"
- layers: "Each item in the array MUST be a descriptor"
- mediaType: "the media type `application/vnd.oci.image.manifest.v1+json`"

## Layer ordering — ch02-fig02 SOURCE

"The final filesystem layout MUST match the result of applying the layers to an empty
directory."

"The array MUST have the base layer at index 0. Subsequent layers MUST then follow in
stack order."

## Note for §2 and §3

"content-addressable images … the image's configuration can be hashed to generate a
unique ID" is the standards-body statement of the identity half of Fixed Point #1.
Corroborates k8s-docs-images' "a hash of the image's content" independently.
```

### A7 · `oci-distribution-spec-2026-08-24.md`

```markdown
---
source_url: "https://raw.githubusercontent.com/opencontainers/distribution-spec/main/spec.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Distribution Specification"
objectives_covered: ["D1.4"]
concepts_covered: ["oci-distribution-spec", "registry", "image-digest"]
---
# OCI Distribution Specification

## What it defines

"The Open Container Initiative Distribution Specification (a.k.a. \"OCI Distribution
Spec\") defines an API protocol to facilitate and standardize the distribution of
content."

## Definitions

- Registry: "a service that handles the required APIs defined in this specification"
- Repository: "a scope for API calls on a registry for a collection of content
  (including manifests, blobs, and tags)."
- Blob: "the binary form of content that is stored by a registry, addressable by a
  digest"
- Manifest: "a JSON document uploaded via the manifests endpoint. A manifest may
  reference other manifests and blobs in a repository via descriptors."
- Digest: "a unique identifier created from a cryptographic hash of a Blob's content."

## Workflows

"Push: the act of uploading blobs and manifests to a registry"
"Pull: the act of downloading blobs and manifests from a registry"

## Note for §5

The Digest definition is Fixed Point #1's identity half stated by the standards body.
The Registry definition upgrades §5's back-bearing to §3 from "standardizes the API"
to a spec-level definition of what a registry IS. Version date (v1.0, May 2020) lives
in oci-overview-2026-08-23.md.
```

### A8 · `oci-runtime-spec-bundle-2026-08-24.md`

```markdown
---
source_url: "https://raw.githubusercontent.com/opencontainers/runtime-spec/main/bundle.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Runtime Specification, Filesystem Bundle"
objectives_covered: ["D1.4"]
concepts_covered: ["filesystem-bundle", "oci-runtime-spec"]
---
# OCI Runtime Specification — Filesystem Bundle

## Definition

A filesystem bundle is "a set of files organized in a certain way, and containing all
the necessary data and metadata for any compliant runtime to perform all standard
operations against it."

## Required contents of a Standard Container bundle

config.json — "contains configuration data. This REQUIRED file MUST reside in the root
of the bundle directory and MUST be named `config.json`."

A root filesystem — the directory referenced by `root.path` in config.json, when that
property is set.

## Storage structure

"while these artifacts MUST all be present in a single directory on the local
filesystem, that directory itself is not part of the bundle."

## Note for §5

Previously `filesystem-bundle` rested only on oci-overview's phrase "a 'filesystem
bundle' that is unpacked on disk". §5's download → unpack → run flow now has a defined
middle artifact.
```

### A9 · `docker-docs-image-layers-2026-08-24.md`

```markdown
---
source_url: "https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "immutability", "base-image"]
---
# Understanding image layers — Docker documentation

## Composition and immutability

"container images are composed of layers. And each of these layers, once created, are
immutable."

"Each layer in an image contains a set of filesystem changes - additions, deletions,
or modifications."

## Reuse and dedup — SOUNDINGS Q4 ANSWER KEY

"This is beneficial because it allows layers to be reused between images."

Reuse makes "builds faster and reduce the amount of storage and bandwidth required to
distribute the images."

## Union filesystem — DEPTH

"When you run a container from an image, a union filesystem is created where layers are
stacked on top of each other, creating a new and unified view."

"When the union filesystem is created, in addition to the image layers, a directory is
created specifically for the running container. This allows the container to make
filesystem changes while allowing the original image layers to remain untouched."

The second sentence is a strong, sourced support for §2's immutability argument: the
image layers are never mutated even by a running container.

## Layer ordering

[EXTRACTOR SUMMARY — NOT VERBATIM] The page demonstrates ordering with a five-layer
example, showing later layers (application code) depending on foundational layers
(the runtime). Re-verify before quoting.
```

### A10 · `docker-docs-build-cache-2026-08-24.md`

```markdown
---
source_url: "https://docs.docker.com/build/cache/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "base-image"]
---
# Docker build cache — Docker documentation

## Instructions map to layers

"Each instruction in this Dockerfile translates to a layer in your final image."

## Invalidation

"Whenever a layer changes, that layer will need to be re-built."

"If a layer changes, all other layers that come after it are also affected."

"Once a layer changes, then all downstream layers need to be rebuilt as well."

## Note for §2

This is the sourced warrant for the outline's claim that "the order of build steps has
consequences." Ordering guidance itself is NOT on this page — the extractor confirmed
it links out to separate "Optimize build cache" and "Cache invalidation" pages that
were not fetched. Do not attribute ordering advice to this URL; for ordering see
docker-docs-build-best-practices-2026-08-24.md.
```

### A11 · `docker-docs-multi-stage-2026-08-24.md`

```markdown
---
source_url: "https://docs.docker.com/build/building/multi-stage/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["base-image", "image-layers"]
---
# Multi-stage builds — Docker documentation

## Problem solved

"Multi-stage builds are useful to anyone who has struggled to optimize Dockerfiles
while keeping them easy to read and maintain."

## Mechanism

"With multi-stage builds, you use multiple FROM statements in your Dockerfile. Each
FROM instruction can use a different base, and each of them begins a new stage of the
build."

"You can selectively copy artifacts from one stage to another, leaving behind
everything you don't want in the final image."

## What does not ship

"None of the build tools required to build the application are included in the
resulting image."

"The Go SDK and any intermediate artifacts are left behind, and not saved in the final
image."

## Scope note

Multi-stage builds are almost certainly beyond KCNA's D1.4 surface. Recorded because
G29 named them explicitly. §2 may name the technique in a clause; it should not teach
Dockerfile syntax.
```

### A12 · `docker-docs-build-best-practices-2026-08-24.md`

```markdown
---
source_url: "https://docs.docker.com/build/building/best-practices/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["base-image", "image-digest", "image-layers"]
---
# Building best practices — Docker documentation

> CLOSES the base-image-selection half of G29. Chapter 2 §2's ⚓ Worth Securing beat.

## Choosing a base image

"Docker Official Images are a curated collection that have clear documentation,
promote best practices, and are regularly updated."

"Verified Publisher images are high-quality images published and maintained by the
organizations partnering with Docker."

## Minimal base images — THE ⚓ WORTH SECURING SOURCE

"When building your own image from a Dockerfile, ensure you choose a minimal base image
that matches your requirements. A smaller base image not only offers portability and
fast downloads, but also shrinks the size of your image and minimizes the number of
vulnerabilities introduced through the dependencies."

"A small image with minimal dependencies can considerably lower the attack surface."

On Alpine: "tightly controlled and small in size (under 6 MB), while still being a full
Linux distribution."

## Pinning to a digest — THE §2 → §3 BRIDGE

"To fully secure your supply chain integrity, you can pin the image version to a
specific digest."

"even if the publisher updates the `3.21` tag, your builds would still use the pinned
image version."

This is a sourced hand-off from §2's base-image material to §3's tag-vs-digest Fixed
Point. It is also an independent, non-Kubernetes statement that a tag can move.

## Build cache

"Understanding how the build cache works, and how cache invalidation occurs, is
critical for ensuring faster builds."

[EXTRACTOR SUMMARY — NOT VERBATIM] The page advises always combining `RUN apt-get
update` with `apt-get install` in the same RUN statement to avoid caching stale
packages. Re-verify before quoting; out of scope for Chapter 2 regardless.
```

### A13 · `docker-docs-what-is-a-container-2026-08-24.md`

```markdown
---
source_url: "https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["container", "shared-kernel-isolation", "container-vs-virtual-machine"]
---
# What is a container? — Docker documentation

> RESOLVES CHAPTER 2 OPEN QUESTION #1 and the live AUTHOR-REVIEW comment at
> chapter-01-taking-departure.md line 140. This is the source for the "kernel"
> sharpening. Read the wording note at the bottom before drafting §1.

## Definition

"Containers are isolated processes for each of your app's components."

"A container is simply an isolated process with all of the files it needs to run."

## What containers share — THE KERNEL SENTENCE

"If you run multiple containers, they all share the same kernel, allowing you to run
more applications on less infrastructure."

## The VM contrast

"A VM is an entire operating system with its own kernel, hardware drivers, programs,
and applications."

"Spinning up a VM only to isolate a single application is a lot of overhead."

## WORDING NOTE — READ BEFORE DRAFTING §1

Three authorities, two registers, no factual conflict:

  KERNEL  — this page (Docker, vendor): "they all share the same kernel"
  OS      — glossary.cncf.io/container/ (CNCF, THE EXAM AUTHORITY):
            "Containers share the same operating system and its machine resources"
  OS      — kubernetes.io/docs/concepts/overview/ (Kubernetes, vendor):
            "relaxed isolation properties to share the Operating System (OS)"

"Share the kernel" is the mechanism; "share the OS" is the looser formulation the exam
authority uses. Teach the mechanism, but ensure the reader recognizes OS phrasing on
the exam.

Internal corroboration already in cache: k8s-docs-runtime-class-2026-08-23.md says a
sandboxed runtime uses "a user-space kernel (such as gVisor)" — which presupposes that
the ordinary case is the HOST's kernel. §1 and §7 can agree on this without leaving
the cache.

DO NOT let Chapter 1 and Chapter 2 diverge on this sentence. The reconcile pass will
surface a mismatch.
```

### A14 · `cncf-glossary-container-2026-08-24.md`

```markdown
---
source_url: "https://glossary.cncf.io/container/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (EXAM AUTHORITY)"
objectives_covered: ["D1.4"]
concepts_covered: ["container", "shared-kernel-isolation"]
---
# Containers — CNCF Cloud Native Glossary

> Note the slug: /container/ (singular). /containers/ returns 404.
> This is the EXAM AUTHORITY's own definition. Weight accordingly.

## What it is

"A container is a running process with resource and capability constraints managed by
a computer's operating system."

## Problem it addresses

"Before containers were available, separate machines were necessary to run
applications. Each machine would require its own operating system, which takes CPU,
memory, and disk space, all for an individual application to function."

## How it helps

"Containers share the same operating system and its machine resources, spreading the
operating system's resource overhead and creating efficient use of the physical
machine."

## The isolation caveat — §7 SETUP

"Since containers share the same operating system, processes can be considered less
secure than alternatives."

This is the exam authority stating §1's tradeoff and §7's motivation in one sentence.
Strong support for the ⚓ Worth Securing beat in §1 ("relaxed isolation is a tradeoff,
not a deficiency") and for §7's existence.

## Absence noted

The extractor confirmed this page contains no direct sentence comparing containers to
virtual machines. For the VM contrast use k8s-docs-overview-2026-08-23.md,
cncf-glossary-containerization-2026-08-24.md, or
docker-docs-what-is-a-container-2026-08-24.md.

## Wording — see A13's note

This page says OPERATING SYSTEM, not kernel.
```

### A15 · `cncf-glossary-container-image-2026-08-24.md`

```markdown
---
source_url: "https://glossary.cncf.io/container-image/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (EXAM AUTHORITY)"
objectives_covered: ["D1.4"]
concepts_covered: ["container-image", "immutability", "registry", "oci"]
---
# Container Image — CNCF Cloud Native Glossary

## What it is

"A container image is an immutable, static file containing the dependencies for the
creation of a container."

Contents named: "a single executable binary file, system libraries, system tools,
environment variables, and other required platform settings."

## Problem it addresses

"application servers are configured per environment, and applications are deployed to
them. Any misconfiguration between environments is problematic and often leads to
downtime or failed deployments."

## How it helps

"Container images bundle an application with any of its runtime dependencies, such as
an application server. This provides consistency across all environments, including a
developer's machine."

"container images can be used to instantiate as many containers as needed, allowing for
greater scalability."

## OCI conformance — §5 SUPPORT FROM THE AUTHORITY

Images "must follow the standard schema defined by the Open Container Initiative (OCI)."

## ⚠ DO NOT QUOTE THIS SENTENCE

The page also states that images are "typically stored in container registries, where
they can be downloaded and run as an isolated process using a Container Runtime
Interface (CRI)."

That is loose: CRI is the kubelet-to-runtime protocol, not the thing that runs an
image. It blurs precisely the boundary §5 exists to draw — and it comes from the exam
authority's own glossary. Use this page for the IMAGE DEFINITION only. Source CRI from
k8s-docs-cri-2026-08-24.md.

## Note for trap #30

The contents list here does NOT include a kernel, which supports §2's negative-space
argument. But no source in the cache states verbatim that "an image does not contain a
kernel." B1 tags trap #30 as [source]; treat it as ENTAILED from the kernel-sharing
statement in A13, not as a quotable fact.
```

### A16 · `cncf-glossary-containerization-2026-08-24.md`

```markdown
---
source_url: "https://glossary.cncf.io/containerization/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (EXAM AUTHORITY)"
objectives_covered: ["D1.4"]
concepts_covered: ["container-vs-virtual-machine", "container-image", "immutability"]
---
# Containerization — CNCF Cloud Native Glossary

## What it is

"Containerization is the process of packaging of application code including libraries
and dependencies required to run the code into a single lightweight executable—called
container image."

## Problem it addresses

[EXTRACTOR SUMMARY — NOT VERBATIM. Re-verify before quoting any of this paragraph.]
Before containers, organizations used virtual machines on bare-metal hardware. VMs are
substantially larger than containers and need a hypervisor. VM template creation,
storage, and transfer are slow processes. Additionally, VMs can experience
configuration drift, violating immutability principles.

## How it helps

Container images are lightweight compared to traditional VMs. The containerization
process uses a dependency file that can be version controlled with automated builds.
Each container image has a unique identifier tied to its exact content and
configuration.

Verbatim fragment: when containers are scheduled and rescheduled, "they are always
reset to their initial state which eliminates configuration drift."

## Note for §2

The configuration-drift framing is the exam authority's own statement of WHY
immutability matters — the strongest available support for the chapter's organizing
principle. Pair with k8s-docs-containers' "build a new image … then recreate the
container" rule.

## ⚠ SCOPE BOUNDARY WITH CHAPTER 3

The "Problem it addresses" paragraph frames the pre-container world as VMs on bare
metal with a hypervisor. That is adjacent to Chapter 3's deployment-eras material
(B2 assigns the three eras and ch03-fig03 to Chapter 3). §1 may use this for the
ARCHITECTURAL contrast only. Do not narrate the timeline.
```

### A17 · `containerd-cri-o-runc-2026-08-24.md`

```markdown
---
source_url: "https://cri-o.io/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "CRI-O project (CNCF), containerd project (CNCF graduated), runC (Open Container Initiative) — three primary project sources, see per-section URLs"
objectives_covered: ["D1.4"]
concepts_covered: ["containerd", "cri-o", "runc", "cri", "oci", "kubelet-runtime-boundary"]
---
# containerd, CRI-O, and runC — primary project sources

> Three URLs in one snapshot because they document one chain. Each section carries its
> own source_url. Serves Chapter 2 §4 (ch02-fig04, Fixed Point #2) and §5's hazard.

## CRI-O — source_url: https://cri-o.io/

> THE OCI/CRI BOUNDARY SENTENCE. Anchor §5's ⚠ Navigational Hazards on this rather
> than asserting the boundary in the book's own voice. Both acronyms, correct planes,
> one sentence, from the project itself.

"CRI-O is an implementation of the Kubernetes CRI (Container Runtime Interface) to
enable using OCI (Open Container Initiative) compatible runtimes."

"It is a lightweight alternative to using Docker as the runtime for kubernetes."

"It allows Kubernetes to use any OCI-compliant runtime as the container runtime for
running pods."

"Today it supports runc and Kata Containers as the container runtimes but any
OCI-conformant runtime can be plugged in principle."

"CRI-O supports OCI container images and can pull from any container registry."

The Kata sentence is a sourced §5 → §7 bridge: Kata appears as an OCI runtime slotting
under CRI, so §7 is visibly the SAME socket from §4, not a new mechanism.

## containerd — source_url: https://raw.githubusercontent.com/containerd/containerd/main/README.md

"containerd is an industry-standard container runtime with an emphasis on simplicity,
robustness, and portability."

"It is available as a daemon for Linux and Windows, which can manage the complete
container lifecycle of its host system: image transfer and storage, container execution
and supervision, low-level storage and network attachments, etc."

"containerd is a member of CNCF with 'graduated' status."

> THE containerd → runC HOP, previously unsourced:

"Most interactions with the Linux and Windows container feature sets are handled via
runc and/or OS-specific libraries (e.g. hcsshim for Microsoft)."

Before this, ch02-fig04's containerd → runC arrow rested only on oci-overview's
"cornerstone" sentence — which establishes provenance of the donation, not use.
Fixed Point #2's chain is now sourced end to end.

## runC — source_url: https://raw.githubusercontent.com/opencontainers/runc/main/README.md

runc is "a CLI tool for spawning and running containers on Linux according to the OCI
specification".

[Only this fragment returned as a quotation. The extractor found no further verbatim
statement about runC's relationship to the runtime spec or libcontainer. Do not
attribute more to this URL without re-fetching.]
```

---

**Two decisions before Stage 3.** Open Question #1 (the kernel/OS wording — finding 1 gives you a better third option than either you listed, and it also closes Chapter 1's live comment), and Open Question #2, which I'd record as resolved to **(a)**: G29 is closed, `ch02-fig02` keeps its anchor and its shared-base half, and nothing needs renaming before Stage 10. Everything else in the outline stands as written — and §4, the section carrying the most weight forward, is now the best-sourced section in the chapter rather than the thinnest.
---
chapter: 2
chapter_type: "content"
title: "Cargo in Standard Crates"
subtitle: "Why the shipping container beat the ship"
exam_domain: "Kubernetes Fundamentals (competency: Containerization)"
domain_weight_pct: 9
complexity: "mixed"
novelty: "moderate"
prereq_factor: "light"

# --- Section plan (no word budgets) ---
# Length is content-driven. Arc-outline depth band for this chapter: "heavy" —
# largest single weight allocation (9 points), deepest root in the dependency
# graph, most new research. That is a relative planning signal, NOT a target.
#
# ⚠ Section NUMBERING IS LOAD-BEARING. Chapter 1 shipped with two published
# cross-bearings that name sections of this chapter by number:
#   ch01 Soundings A1 → *[cross-bearing: see Ch 2 §1 — what a container actually is]*
#   ch01 Soundings A2 → *[cross-bearing: see Ch 2 §4 — the Container Runtime Interface]*
# §1 and §4 below honor those. Do not renumber without editing chapter-01.
sections:
  - name: "What a Container Actually Is"
    objectives: ["D1.4"]
    requires_figure: true
    figure_anchor: "ch02-fig01-vm-vs-container-stack"
    checkpoint_after: false
  - name: "What's Inside an Image"
    objectives: ["D1.4"]
    requires_figure: true
    figure_anchor: "ch02-fig02-image-layers-and-digests"
    checkpoint_after: false
  - name: "Registries, Tags, and Digests"
    objectives: ["D1.4"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "The Container Runtime Interface"
    objectives: ["D1.4"]
    requires_figure: true
    figure_anchor: "ch02-fig04-cri-runtime-chain"
    checkpoint_after: false
  - name: "The Open Container Initiative"
    objectives: ["D1.4"]
    requires_figure: true
    figure_anchor: "ch02-fig03-oci-three-specs"
    checkpoint_after: true
  - name: "When Kubernetes Pulls, and When It Doesn't"
    objectives: ["D1.4"]
    requires_figure: true
    figure_anchor: "ch02-fig05-imagepullpolicy-decision"
    checkpoint_after: false
  - name: "Not All Isolation Is Equal: RuntimeClass"
    objectives: ["D1.4"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "The Crate, Not the Cargo"
    objectives: ["D1.4"]
    requires_figure: true
    figure_anchor: "ch02-zenith-standard-crate"
    checkpoint_after: false

# --- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ---
soundings_planned:
  question_count: 8
  topics:
    - "mutating a running container versus rebuilding the image"
    - "whether a repeated tag pull is guaranteed to be the same bytes"
    - "where an unqualified image name resolves from"
    - "whether a shared base image is stored once or many times"
    - "whether Docker specifically is required to run containers under Kubernetes"
    - "who owns the container image format"
    - "whether container isolation strength is fixed or selectable"
    - "whether a node re-downloads an image it already has"

# --- Skill v5.3 Part 8: practice-question budget ---
# B4 allocates 8 / 10 / 25 = 43. Bearings raised 10 → 12; see § "Taking Your
# Bearings checkpoints" for the justification and B4's own sanction of it.
question_budget:
  soundings: 8
  taking_your_bearings: 12             # across 3 checkpoints (4 + 4 + 4)
  practice_questions: 25
  total_this_chapter: 45

# --- Concept / objective / command tagging ---
kb_tags:
  objectives: ["D1.4"]
  concepts:
    - "container"
    - "container-vs-virtual-machine"
    - "shared-kernel-isolation"
    - "container-image"
    - "image-layers"
    - "immutability"
    - "base-image"
    - "buildpacks"
    - "registry"
    - "image-tag"
    - "image-digest"
    - "latest-tag"
    - "container-runtime"
    - "cri"
    - "containerd"
    - "cri-o"
    - "runc"
    - "kubelet-runtime-boundary"
    - "oci"
    - "oci-runtime-spec"
    - "oci-image-spec"
    - "oci-distribution-spec"
    - "filesystem-bundle"
    - "imagepullpolicy"
    - "imagepullbackoff"
    - "runtimeclass"
    - "sandboxed-runtime"
    - "pluggable-interfaces"
  commands: []

figures_planned:
  - "ch02-fig01-vm-vs-container-stack"
  - "ch02-fig02-image-layers-and-digests"
  - "ch02-fig03-oci-three-specs"
  - "ch02-fig04-cri-runtime-chain"
  - "ch02-fig05-imagepullpolicy-decision"
  - "ch02-zenith-standard-crate"
---

# Chapter 2 Outline — Cargo in Standard Crates

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 2: Cargo in Standard Crates` | required | top |
| `## *"Why the shipping container beat the ship"*` | required | line 2 |
| Metadata line (weight / complexity / novelty) | required | after subtitle |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings` ×3 | **required, min 2** | after §3, §5, §7 |
| `★ Fixed Point` ×3 | **required, min 1** | §3, §4, §5 |
| `**Dead Reckoning:**` ×1 min | **required** | §6 (the `imagePullPolicy` defaults) |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §3 (`:latest`), §5 (OCI ≠ CRI) |
| `☀️ Zenith` | expected | §8 |
| `## Exam Alert` | **required** | after §8 |
| `## Practice Questions` | **required** | 25 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19 |
| `🏆 Safe Harbor` | expected | chapter close |

**Zenith:** exactly one, per Part 18.10. `ch02-zenith-standard-crate` in §8. Do not add a second dramatic synthesis illustration.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 2 — Cargo in Standard Crates". Carried forward without modification:

- **Covers**: **D1.4** — containers vs VMs; images, layers, tags vs digests; registries; `imagePullPolicy`; immutability; OCI runtime/image/distribution specs; runC; CRI; containerd; CRI-O; RuntimeClass; image build practices.
- **Prerequisites**: none beyond Ch 1. First content chapter by design — the deepest root in the dependency graph.
- **Retrieval targets**: **none.** First content chapter, and **[B3]** excludes Ch 1 from the retrieval schedule entirely. The spacing ramp begins at Ch 3 (10%, drawn from this chapter).
- **Question budget**: 8 Soundings · 10 Bearings · 25 Practice · 43 total. Bearings raised to 12 below.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: heavy.

**What this chapter owes forward.** Three of its concepts are named anchors in later chapters' retrieval contracts, and drafting must teach them well enough to survive the wait:

| Concept | Retrieved at | Contract |
|---|---|---|
| The CRI boundary — which component actually talks to the runtime | Ch 3 (10%), Ch 8 (≥4-back floor), Ch 17 (Zenith) | Named anchor, three times |
| Image immutability | Ch 3 (10%) | Named anchor |
| `imagePullPolicy` | Ch 5 (20%) | Named anchor |
| `ImagePullBackOff` | Ch 13 (25%) | Named anchor — introduced **here**, diagnosed there |
| CRI as pluggable interface #1 of 4 | Ch 17 secondary Zenith (with CNI/Ch 9, CSI/Ch 11, CRDs/Ch 6) | Cross-cutting theme 6 |

CRI is the single most reused idea in this chapter. It is retrieved more often than anything else Chapter 2 teaches, and it is half of the book's secondary Zenith. Weight §4 accordingly.

**Reader positioning**: Communications Officer role family, **junior tier**. Single unified brand voice; only atmospheric register and reader rank differ.

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**The curiosity gap: Kubernetes cannot run a container. Not one, not ever, on any cluster.** That is a genuinely surprising sentence to a reader who has just been told that Kubernetes is the container platform, and it is literally true — every container on every node is started by software that is not Kubernetes, reached through an interface Kubernetes merely defines. Open the gap here, hold it through §1–§3, and pay it off in §4 at `ch02-fig04`. Chapter 1's Soundings already told this reader that an orchestrator is not a runtime; this chapter's job is to convert that one-line correction into a mechanism they can draw.

**The identity frame** is discrimination, which is the competence the whole exam measures (Ch 1 §1 established this and it should be reinforced, not restated). A practitioner who has this chapter can be handed any unfamiliar container tool — a new runtime, a new build system, a registry product — and place it on a map: does it produce images, distribute them, or run them, and which specification is it conforming to? That placement instinct is what separates someone who has memorized "containerd, CRI-O, runC" from someone who understands why those three names are not a list of alternatives.

**The stakes are structural and should be stated plainly, without inflation.** This is the first content chapter because containerization is the deepest root in the dependency graph, not because it is the easiest warm-up. Roughly nine points of the exam sit here on this book's authored judgment (CNCF publishes no sub-competency weights — see § Open questions #8), but the real exposure is downstream: a reader who leaves this chapter thinking "container" is an undefined primitive will find that Chapter 3's CRI boundary, Chapter 13's `ImagePullBackOff`, and Chapter 17's whole pluggability argument each land slightly wrong. Say that once, calmly, and move on. The brand's ethical guardrails forbid manufactured urgency and this reader is an adult professional.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Five outcomes, active verbs:

- **Distinguish** a container from a virtual machine by what each one shares with the host, and explain why that single difference produces every other difference people cite.
- **Explain** what a container image contains, what it deliberately does not contain, and why the correct response to a needed change is a new image rather than an edited container.
- **Predict** which bytes a given image reference resolves to — including when a tag will silently resolve to something different than it did last week, and when a digest guarantees it cannot.
- **Trace** the path from a Pod's image field to a running process, naming each component in the kubelet → CRI → runtime → runC chain and stating which specification governs each hop.
- **Choose** an `imagePullPolicy` deliberately, and state what Kubernetes will do by default when you don't.

*You'll also be able to look at an unfamiliar container tool and say what layer it operates at — which is how practitioners actually navigate this ecosystem.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Chapter 2's prerequisite set is "general IT literacy plus Chapter 1," so all eight test **priors the reader arrives with**. **[B3]** Soundings are excluded from the retrieval budget; here there is nothing earlier to retrieve anyway.

⚠ **Hard constraint discovered in the published Chapter 1.** `chapter-01-taking-departure.md` §Soundings answers **already give away** two of the three most obvious Chapter 2 pre-test questions:

- **A1** states the container/VM distinction ("the host's operating system kernel") and cross-bears to Ch 2 §1.
- **A2** states the orchestrator/runtime split and cross-bears to Ch 2 §4.

A reader arriving at Chapter 2 was told both answers roughly thirty pages ago. Re-asking either in its plain form produces a fake-high score and destroys the calibration. Neither appears below. Q5 approaches the runtime question from a genuinely different angle — whether *Docker specifically* is required — which Chapter 1 does not address.

| # | Topic (not wording) | Prerequisite / intuition tested | Why it is useful as a pre-test |
|---|---|---|---|
| 1 | Editing a file inside a running container versus rebuilding | Whether the reader holds the pets-vs-cattle instinct from any prior ops context | Immutability is the chapter's organizing principle and the hardest habit to dislodge in readers with VM-administration backgrounds. Surfacing the instinct before §2 means §2 corrects a live model rather than filling a void |
| 2 | Two pulls of the same tag a week apart — same bytes guaranteed? | Software-distribution literacy; whether "version string" and "identity" are already separate ideas | This is the chapter's sharpest Fixed Point and the one readers most reliably arrive wrong on. A wrong answer here is exactly the reader §3 is written for |
| 3 | Where an unqualified image name resolves from | Whether the reader knows that unnamespaced identifiers imply a default | Cheap, concrete, and it calibrates §3. Readers who have never pushed an image tend to assume the name is the whole address |
| 4 | Two images built on the same base — stored once or twice? | Storage/dedup intuition from any packaging or VM-template background | Gates the layer material in §2 and `ch02-fig02`. Readers who guess "twice" need §2 read slowly; readers who guess "once" can skim to the digest material |
| 5 | Is Docker specifically required to run containers under Kubernetes? | Whether the reader has absorbed the industry's Docker-means-containers shorthand | Not answered by Ch 1, which addressed orchestrator-vs-runtime generically. Sets up §4's chain and the pluggability plant. **Framing constraint:** B1 trap #34 is `[inferred]`, so the answer key says "easy to confuse," never "frequently tested" |
| 6 | Who owns the container image format | Standards-body literacy; whether the reader assumes a vendor format | Distinct from Ch 1 Q3, which asked who governs *Kubernetes*. Gates §5 and gives the D4.3-under-studying reader a second early signal that institutional questions are on this exam |
| 7 | Is container isolation strength fixed, or can it be varied per workload? | Security intuition; whether the reader thinks "container" names one isolation level | Almost every reader arrives assuming it's fixed. Sets up §7 (RuntimeClass, gVisor, Kata) — the chapter's most-skipped material because it sounds like an edge case |
| 8 | Does a node re-download an image it already has? | Caching intuition from package managers or CI systems | Gates §6. The honest answer is "it depends, and the default depends on how you wrote the tag," which is precisely the shape §6 teaches |

**Rubric** (standard 8-question scale, per `branded-terms.yaml`):

- **6+ right** — skim. Focus on `★ Fixed Points` and `⚠ Navigational Hazards`, and do not skip §5 (OCI) or §7 (RuntimeClass) regardless of score; those are the two sections that score well on intuition and still surprise people on the exam.
- **3–5 right** — read at normal pace. This chapter is calibrated for you.
- **0–2 right** — read carefully, in its own session. This is the chapter every later chapter rests on, and there is no shortcut through it. Nothing here is difficult; there is simply a lot of new vocabulary, and the book defines every term before using it.

**Fixed-Point spoiler check — passes.** The chapter's three Fixed Points are (a) tag-vs-digest identity, (b) the kubelet → CRI → runtime → runC chain, and (c) OCI as a three-specification governance body. Q2 *pre-tests the prior* behind (a) without stating the tag/digest mechanism; the answer key confirms "no, not guaranteed" in one line and cross-bears to §3 rather than explaining digests. Q5 and Q6 approach (b) and (c) from the outside — "is Docker required," "who owns the format" — and their answer keys name §4 and §5 as the destination without reciting the chain or the three specs.

⚠ **Answer-key discipline for drafting.** One line per question, then stop. Q2, Q5, and Q6 will each tempt a full explanation, and each of those explanations is a Fixed Point this chapter is about to spend properly. Spending it twice costs the payoff both times. Q4 and Q7 have the same risk at lower intensity.

---

## 4. Section plan

### §1 — ⚪ What a Container Actually Is

The chapter's foundation and the target of a published Chapter 1 cross-bearing. Establish the container as a repeatable, standardized unit that decouples an application from the host infrastructure — the standardization coming from having dependencies bundled, which is what makes behavior identical across environments. Then draw the VM contrast at the level that actually explains it: a container relaxes isolation to **share the host operating system**, which is why it is lightweight; a virtual machine boots a full guest OS on virtualized hardware. Every other cited difference (start-up time, image size, density) is downstream of that one architectural choice, and the section should say so rather than presenting a feature-comparison table. Close by noting that containers in a Pod are co-located and co-scheduled on one node — planted, not explained, because Pod is Chapter 5.

- **Objectives**: D1.4
- **Concepts introduced**: `container`, `container-vs-virtual-machine`, `shared-kernel-isolation`
- **Sources**: `k8s-docs-containers-2026-08-23.md` (repeatability, decoupling, co-location), `k8s-docs-overview-2026-08-23.md` (the VM contrast and the sharing language)
- **Figure**: **`ch02-fig01-vm-vs-container-stack`** — required
- **Checkpoint after**: no
- **Markers planned**: `> ⚓ **Worth Securing:**` on the "relaxed isolation is a *tradeoff*, not a deficiency" framing — it is the honest version and it seeds §7
- **Cross-bearings**: back to Ch 1 §Soundings A1 (reciprocal — Ch 1 promised this section by number); forward to Ch 5 (Pod, and the shared network namespace); forward to §7 (when relaxed isolation is not enough)
- ⚠ **Precision constraint, inherited from a live AUTHOR-REVIEW note in Chapter 1.** The cached snapshot phrases the sharing as "the Operating System (OS) among the applications," not specifically the *kernel*. Chapter 1's answer key sharpened this to "operating system kernel" and flagged the sharpening for review. **Chapter 2 must resolve it, not repeat it unexamined.** Either (a) keep the sharpening and carry it consistently in both chapters, or (b) soften both to the snapshot's wording. Do not let the two chapters diverge — this is the single most-quoted sentence in the chapter and the reconcile pass will surface the mismatch. Raised in § Open questions #1.
- ⚠ **Scope boundary with Ch 3.** B2 assigns the three deployment eras (traditional → virtualized → container) to **Chapter 3**, where they set up "what Kubernetes is." Chapter 2 owns the *architectural* contrast only. Do not narrate the historical progression here; §1 needs the VM comparison, not the timeline. `ch03-fig03-deployment-eras-timeline` is Chapter 3's figure and Chapter 3's beat.

### §2 — ⚪ What's Inside an Image

The image as a ready-to-run package: the code, any runtime it requires, application **and** system libraries, and default values for essential settings. Then the negative space, which is where the exam lives — an image does **not** carry a kernel, and understanding why closes the loop on §1. From there, layers: an image is assembled as a stack of filesystem layers, which is why two images sharing a base share storage and transfer, and why the order of build steps has consequences. Finish with build practices at the level this exam reaches: base-image selection as a real decision, and Cloud Native Buildpacks as the CNCF-graduated alternative to hand-authoring build files — a builder image combining buildpacks with a build-time base image and a lifecycle binary, running detect → build → export to produce a runnable OCI image.

- **Objectives**: D1.4
- **Concepts introduced**: `container-image`, `image-layers`, `immutability`, `base-image`, `buildpacks`
- **Sources**: `k8s-docs-containers-2026-08-23.md` (image contents; the immutability rule), `k8s-docs-images-2026-08-23.md` (image as binary data encapsulating app + dependencies), `buildpacks-concepts-2026-08-23.md` (builder, base images, stack, lifecycle phases)
- **Figure**: **`ch02-fig02-image-layers-and-digests`** — required
- **Checkpoint after**: no
- **Markers planned**:
  - `> ⚓ **Worth Securing:**` on base-image selection — smaller base, smaller attack surface, faster pull; the tradeoff is debuggability
  - `> 🔭 **Closer Look:**` optional, on Buildpacks' reproducible-layer export. Genuinely deeper than the exam requires; cut without regret if the section runs long
- **Cross-bearings**: forward to §5 (the OCI image-spec is what standardizes the layer serialization described here); forward to Ch 12 (image scanning, signing, and supply-chain provenance)
- ⚠ **Research gap — G29 is only partially closed.** The cached set now covers tags/digests/registries (`k8s-docs-images`) and Buildpacks (`buildpacks-concepts`), but **layer mechanics, layer caching and dedup, multi-stage builds, and base-image selection guidance are still not covered by any cached snapshot.** `oci-overview` gives one phrase — "filesystem layer serialization" — and nothing more. `ch02-fig02` depends on layer detail this book cannot currently source. Stage 2 must close it or §2 must narrow to what the snapshots support. See § Open questions #2.
- ⚠ **Scope boundary with Ch 12.** `sigstore-overview-2026-08-23.md` is cached and will look relevant while drafting build practices. It is not this chapter's. B2 routes supply-chain security (G22 — SBOM, signing, in-toto, TUF, Harbor, scanning) to **Chapter 12**. §2 may name the concern in one clause and cross-bear forward; it may not teach it.

### §3 — 🔵 Registries, Tags, and Digests

The chapter's densest exam surface and the home of its sharpest Fixed Point. Build the image reference from its parts: an optional registry hostname (and possibly a port), the image name, and then either a tag or a digest. Establish the defaults, because they are what the exam tests — omit the registry and Kubernetes assumes the Docker public registry; omit the tag and Kubernetes assumes `latest`; so `busybox` is exactly `docker.io/library/busybox:latest`. Then the distinction the whole section exists for: **a tag identifies a series and can be moved to point at a different image; a digest is a hash of the image's content and is immutable.** Two pulls of `myapp:v2` a week apart are not guaranteed to be the same bytes. Two pulls of an image by digest are. Close with registries as the distribution layer and private-registry credentials named but not taught.

- **Objectives**: D1.4
- **Concepts introduced**: `registry`, `image-tag`, `image-digest`, `latest-tag`
- **Sources**: `k8s-docs-images-2026-08-23.md` (naming, defaults, the tag/digest distinction, the `:latest` caution, private-registry credential paths)
- **Figure**: none new — this section *uses* `ch02-fig02`, whose right half carries the tag-as-movable-label / digest-as-content-hash relationship. Do not commission a second figure for tabular naming rules; §3's defaults are a table, and a table is the right instrument (Part 18.9)
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `**★ Fixed Point:**` — **Fixed Point #1.** A tag is a label that can move. A digest is the image's identity. This is the one sentence from §1–§3 the reader should be able to recite cold
  - `> ⚠ **Navigational Hazards**` — the `:latest` trap in full. The documented guidance is to avoid `:latest` in production because it is harder to know which version is running and harder to roll back properly. The hazard has a second half that §6 completes: the tag you choose silently changes the pull *policy*, so `:latest` is not only an identity problem
  - `> 🪝 **Snag:**` — a bare name is not a bare name. `busybox` is three defaults stacked
  - `> **Logbook Entry:**` — **the chapter's one sidebar.** The moved-tag incident: identical manifests, different bytes, and a rollback that rolled back to the same thing. **Subject-dignity check:** aim it squarely at the practitioner's own confusion — the afternoon spent proving the manifest hadn't changed. Do not narrate downstream user harm. Passes as scoped
- **Cross-bearings**: forward to §6 (the tag determines the default pull policy — the two halves of the `:latest` problem); forward to Ch 4 (`imagePullSecrets` is a Secret of type `kubernetes.io/dockerconfigjson`, and Secrets are Chapter 4); forward to Ch 12 (registry access as a security boundary)
- ⚠ **Do not teach `imagePullSecrets` here.** It requires Secrets, which the reader does not have until Chapter 4. Name the five credential paths from the snapshot in a sentence, point forward, and stop. A worked `imagePullSecrets` example in Chapter 2 imports a Chapter 4 concept the reader cannot yet hold.

### §4 — 🔵 The Container Runtime Interface

The payoff of the chapter's curiosity gap, the target of the second published Chapter 1 cross-bearing, and the most-retrieved idea in the chapter. Establish the container runtime as the per-node component responsible for managing the execution and lifecycle of containers — and then draw the chain end to end: the kubelet on each node speaks **CRI**, the Container Runtime Interface, to a conformant runtime; the runtime (containerd, CRI-O, or any other CRI implementation) manages images and container lifecycle; and beneath it a low-level runtime such as runC does the actual work of starting the process. Kubernetes defines the interface. It does not implement it. That is the whole answer to "Kubernetes cannot run a container," and it should land as a mechanism the reader can draw, not a slogan. Note that a cluster normally picks a default runtime and the reader will rarely think about it — which is exactly why §7 exists.

- **Objectives**: D1.4
- **Concepts introduced**: `container-runtime`, `cri`, `containerd`, `cri-o`, `runc`, `kubelet-runtime-boundary`, `pluggable-interfaces` (planted)
- **Sources**: `k8s-docs-containers-2026-08-23.md` (runtime responsibility; containerd, CRI-O, "any other implementation of the CRI"; default runtime and the RuntimeClass escape hatch), `k8s-docs-cluster-architecture-2026-08-23.md` / `k8s-docs-components-2026-08-23.md` (kubelet as the node agent), `oci-overview-2026-08-23.md` (runC as the donated runtime)
- **Figure**: **`ch02-fig04-cri-runtime-chain`** — required. The chapter's most load-bearing diagram
- **Checkpoint after**: no
- **Markers planned**:
  - `**★ Fixed Point:**` — **Fixed Point #2.** kubelet → CRI → containerd / CRI-O → runC. Kubernetes never starts a container itself
  - `> 🪝 **Snag:**` — "Docker" names a company, a CLI, a build format, and historically a runtime. When someone says "Kubernetes runs Docker containers," at least three of those four are doing no work. **Framing constraint:** B1 trap #34 is `[inferred]`; write it as "easy to confuse," never "frequently tested"
- **Cross-bearings**: back to Ch 1 §Soundings A2 (reciprocal — Ch 1 promised this section by number); forward to Ch 3 (the kubelet in its full node-component context); forward to Ch 13 (`crictl`, which reaches the runtime *below* the Kubernetes API — the payoff of knowing there is a below); forward to Ch 17 (**CRI as pluggable interface #1 of 4** — the secondary Zenith)
- ⚓ **Drafting note.** Cross-cutting theme 6 (`2 → 9 → 11 → 6 → 17`) begins in this section. Plant the *shape* — "Kubernetes defines an interface and lets the ecosystem implement it" — as a named idea here, so Ch 9 (CNI), Ch 11 (CSI), and Ch 6 (CRDs) can each say "this is the same move again" and Ch 17 can collect all four. Naming the pattern once here is what makes the Chapter 17 Zenith recognition rather than a fifth list.

### §5 — 🔵 The Open Container Initiative

The standards layer underneath everything the reader has just learned, positioned deliberately *after* CRI so the two can be told apart. The OCI is an **open governance structure** established in June 2015 by Docker and other container-industry leaders, for the express purpose of creating open industry standards around container formats and runtimes. It publishes three specifications, and each one retroactively explains an earlier section: **image-spec** defines the OCI Image Format — image manifest, filesystem layer serialization, image configuration — which is what §2's layers actually are; **distribution-spec**, which reached v1.0 in May 2020, standardizes the API for distributing images, which is what §3's registries actually speak; **runtime-spec** describes how to run a filesystem bundle unpacked on disk, which is what §4's runC actually does. Then the flow, in three beats: download an OCI Image → unpack it into an OCI Runtime filesystem bundle → run the bundle with an OCI Runtime. Close on runC: Docker donated it to the OCI as the cornerstone of the effort.

- **Objectives**: D1.4
- **Concepts introduced**: `oci`, `oci-image-spec`, `oci-distribution-spec`, `oci-runtime-spec`, `filesystem-bundle`
- **Sources**: `oci-overview-2026-08-23.md` (founding date and purpose, all three specs, the distribution-spec v1.0 date, the download→unpack→run flow, the runC donation)
- **Figure**: **`ch02-fig03-oci-three-specs`** — required
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `**★ Fixed Point:**` — **Fixed Point #3.** OCI is a governance body publishing three specifications. It is not a runtime, not a company, and not a product
  - `> ⚠ **Navigational Hazards**` — **the OCI/CRI boundary, stated explicitly.** CRI is how *Kubernetes* talks to a runtime. OCI is how *images* are formatted and distributed and how *bundles* are executed. Different layers, both abbreviations, both three letters, both involving the word "runtime." Draw the boundary on `ch02-fig03` and `ch02-fig04` in the same visual grammar so the reader can see the two planes. **Framing constraint:** B1 trap #33 is `[inferred]` — "easy to confuse," not "frequently tested"
  - `> 🪢 **Mnemonic:**` — the three specs in the order the flow uses them: **Image → Bundle → Run** (image-spec → distribution-spec moves it → runtime-spec runs it). Include only if it survives reading aloud; a forced mnemonic is worse than none
  - `> 🔭 **Closer Look:**` optional, on why distribution-spec arrived five years after the other two
- **Cross-bearings**: back to §2 (image-spec ⇒ layers), back to §3 (distribution-spec ⇒ registries), back to §4 (runtime-spec ⇒ runC); forward to Ch 17 (CNCF governance, and the general shape of foundation-hosted standards work)
- ⚠ **Ordering note for reviewers.** Figure ordinals do not run in section order here: `ch02-fig03` (OCI) sits in §5 and `ch02-fig04` (CRI) sits in §4. This is deliberate. §4 must be the CRI section because Chapter 1 ships a published cross-bearing to "Ch 2 §4 — the Container Runtime Interface," and teaching CRI *before* OCI is also the better sequence: it lets §5 land as "here are the standards underneath everything you just learned" and lets the OCI-vs-CRI boundary be drawn once, in the section that comes second. The anchor IDs are join keys for `image-specs.md` and the diagram pipeline, not ordinals, so they are kept verbatim from the arc outline. See § Open questions #4.

### §6 — 🟡 When Kubernetes Pulls, and When It Doesn't

The chapter's fiddliest material and the natural home for its required facts-only block. Three policies: **IfNotPresent** pulls only if the image is not already present locally; **Always** makes the kubelet query the registry every launch to resolve the name to a digest, using its cached copy if it already holds that exact digest and pulling otherwise; **Never** never fetches, starting the container only if the image somehow already exists locally. Then the defaults, which are the actual exam target and which nobody guesses correctly: omit `imagePullPolicy` and you get **IfNotPresent** with a digest, **Always** with the `:latest` tag, **Always** with no tag at all, and **IfNotPresent** with any other tag. That is where §3's `:latest` hazard completes — the tag you write silently sets the pull behavior. Add the two operational facts: once a Pod is created, `imagePullPolicy` is not updated if the image's tag or digest later changes; and a container that cannot pull sits in `ImagePullBackOff`, retrying with increasing delay up to a compiled-in limit of 300 seconds.

- **Objectives**: D1.4
- **Concepts introduced**: `imagepullpolicy`, `imagepullbackoff`
- **Sources**: `k8s-docs-images-2026-08-23.md` (all three policies, the full defaults table, the not-updated-after-creation rule, `ImagePullBackOff` and the 300-second cap)
- **Figure**: **`ch02-fig05-imagepullpolicy-decision`** — required
- **Checkpoint after**: no
- **Markers planned**:
  - `> **Dead Reckoning:**` — **satisfies the chapter's required Dead Reckoning block.** The three policies and the four defaults, flat, no metaphor, no framing. This is the single best home for it in the chapter: the material is literally a facts-only lookup table and the marker's function is exactly that. Do not spend the required Dead Reckoning anywhere else
  - `> 🪝 **Snag:**` — changing the tag on an image after the Pod exists does not change the Pod's pull policy
- **Cross-bearings**: back to §3 (the tag/policy coupling); forward to Ch 5 (`imagePullPolicy` is a named Ch 5 retrieval anchor, and the container `Waiting` state that `ImagePullBackOff` reports is Chapter 5's material); forward to Ch 13 (`ImagePullBackOff` as a diagnosed failure signature — a named Ch 13 anchor)
- ⚠ **Introduce `ImagePullBackOff`, do not diagnose it.** The arc's callback map makes Chapter 2 its origin and Chapter 13 its payoff. Chapter 2 owes the reader the name, the cause, and the back-off behavior. It does not owe them the diagnostic workflow, and it cannot give them one — Pod phases and container states are Chapter 5, and `kubectl describe` is Chapter 8. Name it, cross-bear forward twice, stop. **Do not narrate a container `Waiting` state as if the reader knows what a container state is.**

### §7 — 🟡 Not All Isolation Is Equal: RuntimeClass

The section readers skip and the exam does not. §1 established that containers share the host OS — a tradeoff, and tradeoffs can be renegotiated per workload. RuntimeClass is the feature for selecting the container runtime configuration used to run a Pod's containers. The motivation is the point: a workload deserving a high level of information-security assurance can be scheduled onto a runtime using **hardware virtualization** (Kata Containers) or a **user-space kernel** (gVisor), buying extra isolation at the cost of additional overhead. Same API, different floor. Cover the mechanism at the depth the exam reaches — the CRI implementation is configured on nodes with named handlers, RuntimeClass resources reference those handlers, and a Pod selects one with `runtimeClassName`; absent that, the default handler is used. Note that a RuntimeClass can also carry scheduling constraints and a Pod overhead so the scheduler accounts for the runtime's cost, and cross-bear forward rather than explaining scheduling here.

- **Objectives**: D1.4
- **Concepts introduced**: `runtimeclass`, `sandboxed-runtime`
- **Sources**: `k8s-docs-runtime-class-2026-08-23.md` (motivation, Kata and gVisor, handlers and setup, `runtimeClassName`, default handler, scheduling constraints and overhead)
- **Figure**: none. The mechanism is a two-step indirection best carried by prose plus a short list; a diagram here would restate the text (Part 18.7 redundancy) and the chapter already carries five figures plus a Zenith
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `> 🔭 **Closer Look:**` — hardware virtualization (Kata) versus user-space kernel (gVisor) as two genuinely different answers to the same question. Marked as depth: the exam is far more likely to ask *why RuntimeClass exists* than to ask which sandbox uses which technique
  - `> ⚓ **Worth Securing:**` — "container" names an interface, not an isolation level. This is the sentence that makes §7 stick
- **Cross-bearings**: back to §1 (the relaxed-isolation tradeoff, now renegotiated); forward to Ch 7 (the scheduling constraints and Pod overhead this section names but does not explain); forward to Ch 12 (sandboxed runtimes as a security control, in the security lifecycle)
- ⚓ **Why this section is not optional.** B1 flagged G30 as a blocking gap specifically because RuntimeClass was defined in the sources without its motivation, and a RuntimeClass taught without its motivation is unmemorable trivia. G30 is now **closed** — `k8s-docs-runtime-class-2026-08-23.md` carries the full motivation, both sandbox examples, and the overhead mechanism. Draft the motivation first and the mechanism second.

### §8 — 🔵 The Crate, Not the Cargo

Short, synthetic, and the chapter's one dramatic beat. The subtitle's promise comes due: the shipping container did not win because it was a better box. It won because the industry standardized the **interface** — the corner fittings, the dimensions, the lifting points — which meant a crane, a truck, a rail flatcar, and a ship's hold could each be built once against a published specification and then handle anything. The cargo stopped mattering. That is precisely what the reader has spent the chapter looking at from five angles: OCI standardized the format and the distribution API so any registry can serve any image; CRI standardized the Kubernetes-to-runtime contract so any conformant runtime can be swapped in; and the payoff is that Kubernetes never needed to know what is in the crate. Land it, then plant the forward hook: this is the first of four times the reader will see this move, and Chapter 17 will collect them.

- **Objectives**: D1.4 (synthesis)
- **Concepts introduced**: none new — this section connects, it does not teach
- **Sources**: none required. If drafting reaches for a source here, the section has drifted into teaching
- **Figure**: **`ch02-zenith-standard-crate`** — the chapter's one Zenith illustration
- **Checkpoint after**: no
- **Markers planned**:
  - `☀️ Zenith` — the standardization recognition
  - `> **Extended Analogy:**` — permitted **here and nowhere else in this chapter.** The intermodal-container argument, run at sidebar length. It is the chapter's title, its subtitle, and its closing beat, and running it anywhere else as well would be theme-dressing
  - `🏆 Safe Harbor` at the chapter close
- **Cross-bearings**: forward to Ch 17 (**the reciprocal back-bearing must be built** — Ch 17's extension-points Zenith cites this section by name); forward to Ch 3 (the next chapter opens the cluster that the runtime sits inside)
- ⚠ **Drift risk — flagged for the audit stage, highest in the book so far.** This chapter's organizing metaphor is a shipping container, and `structural-contract.yaml` `forbidden_patterns` bans a specific set of nautical clichés outright: *smooth sailing, weather the storm, all hands on deck, chart a course, set sail, batten down the hatches, uncharted waters, plain sailing.* A drafting stage writing enthusiastically about cargo and ships will reach for at least two of these. It must not. The theming-density target is 1–3 overt nautical metaphors per 1,000 words (style-decisions 2026-04-18), and §8 will consume most of the chapter's allowance in one place — which is the correct place to spend it. Sections §2 through §7 should read as plain technical prose.

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 12 questions total.** B4 allocates 10; this outline raises it to 12 on B4's own instruction: *"Outlines should treat the 10 as a contract to exceed, not a target to hit. Chapters carrying more than one major conceptual arc will run 3 checkpoints and land at 12–15."* Chapter 2 carries three: the image arc (§1–§3), the runtime-and-standards arc (§4–§5), and the operational arc (§6–§7). Folding these into two checkpoints would put the OCI material in the same block as `imagePullPolicy`, which are unrelated cognitive modes and a needless alternating-attention cost (skill Part 4). Practice Questions stay at 25 and Soundings at 8, so the chapter total moves 43 → 45 against a book with 415 questions of headroom.

**Retrieval-practice content: none.** Chapter 2 is the first content chapter, and **[B3]** excludes Chapter 1 from the retrieval schedule entirely. The callback map records Ch 2 as `—`. The spacing ramp begins at Chapter 3 (10%, drawn from here). **Do not manufacture retrieval questions about Chapter 1's exam mechanics to fill the slot** — that is explicitly forbidden by [B3]'s do-not-retrieve list #1.

Interleaving in this chapter is therefore **within-chapter**, across the three arcs, rather than across chapters. That is a real substitute, not a consolation: the chapter's two most valuable discriminations (tag-vs-digest and OCI-vs-CRI) both live at arc boundaries.

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: containers, images, and image identity
- **Count**: 4
- **Retrieval from earlier chapters**: 0% (n/a — first content chapter)
- **Question design**:
  1. **The VM boundary, applied rather than recited.** Give a symptom or constraint and ask what it implies about the container/VM choice. Trap answers should target the belief that an image ships a kernel (B1 trap #30)
  2. **Image contents.** What is and is not inside an image. The distractor set should include the kernel and at least one item that *is* included but feels like it shouldn't be (system libraries)
  3. **Tag versus digest — the Fixed Point.** Two pulls, one week apart, same tag. Trap answers target "the tag is the version so the bytes are the version" (the near-universal prior tested in Soundings Q2)
  4. **Reference defaults.** Given a bare image name, name the registry and tag it resolves to. Cheap, concrete, and it verifies the three-defaults-stacked point actually landed
- **Trap-answer targets**: kernel-in-the-image (#30); patching a running container (#31); tags as immutable identities; assuming an unqualified name has no implied registry
- **Why-wrong explanations**: required for every option, per the contract and the ethical checklist

### ☆ Taking Your Bearings #2 — after §5

- **Topic**: who runs the container, and who standardized it
- **Count**: 4
- **Retrieval from earlier chapters**: 0% (n/a)
- **Question design**:
  1. **The chain, in order.** Given the components, order them from kubelet to running process, or identify which one Kubernetes itself implements (none). This is Fixed Point #2 and the most-retrieved item in the chapter — it earns a question of its own
  2. **OCI is not a runtime.** Trap answers should offer OCI as a runtime, as a company, and as a product (B1 trap #32)
  3. **The OCI/CRI boundary.** Given a described function, name which of the two governs it. This is the chapter's hardest discrimination and the one Ch 17 depends on. **Framing constraint:** B1 trap #33 is `[inferred]` — the explanation says "easy to confuse," never "commonly missed on the exam"
  4. **Spec-to-artifact mapping.** Match one of the three specifications to the thing it governs (layers / registry API / bundle execution). Verifies that §5's retroactive-explanation structure worked
- **Trap-answer targets**: OCI-as-runtime (#32); OCI/CRI conflation (#33, `[inferred]`); Docker-as-the-runtime (#34, `[inferred]`); the belief that Kubernetes implements the runtime
- **⚓ Design note**: at least one of these four should require holding §4 and §5 together rather than either alone. That is this chapter's substitute for cross-chapter interleaving

### ☆ Taking Your Bearings #3 — after §7

- **Topic**: pull behavior and runtime selection
- **Count**: 4
- **Retrieval from earlier chapters**: 0% (n/a)
- **Question design**:
  1. **Default pull policy from a reference.** Give an image reference and ask what `imagePullPolicy` applies when the field is omitted. Rotate which of the four default cases is tested; the `:latest` and no-tag cases are the highest-value
  2. **`Always` does not mean "always download."** The kubelet resolves to a digest and reuses a cached image with that digest. Trap answers target "Always re-downloads the image every launch"
  3. **`ImagePullBackOff`.** What the status means and what the BackOff half implies. Scope discipline: this tests recognition, not diagnosis — the diagnostic workflow is Chapter 13's
  4. **RuntimeClass motivation.** Given a workload requirement, decide whether RuntimeClass is the right instrument and why. Trap answers should target "use RuntimeClass to pick a faster runtime for everything," which misses that the tradeoff runs both ways
- **Trap-answer targets**: `Always` as unconditional re-download; the belief that changing a tag updates an existing Pod's pull policy; treating sandboxed runtimes as free; treating `:latest` as merely a naming-hygiene issue rather than a behavior change
- ⚠ **Scope guard**: no question in this checkpoint may require Pod phases, container states, `kubectl describe`, or Secrets. All four are later chapters, and this is exactly the checkpoint where drafting will drift into them.

---

## 6. Exam Alert plan

**High-priority topics** — the four this chapter would defend as most worth the reader's memory:

1. **Tag versus digest.** A tag can move; a digest is content-addressed and cannot. Everything about reproducible deployment rests on it.
2. **The kubelet → CRI → containerd/CRI-O → runC chain.** The most-retrieved item in the chapter and half of the Chapter 17 Zenith.
3. **OCI's three specifications, and that OCI is a governance body rather than software.** image-spec (format), distribution-spec (the registry API, v1.0 May 2020), runtime-spec (running a filesystem bundle).
4. **`imagePullPolicy` defaults.** IfNotPresent with a digest; Always with `:latest`; Always with no tag; IfNotPresent with any other tag.

**Common traps to call out** — each carries its B1 number and evidence tag, and the `[inferred]` ones must be framed as "easy to confuse," never as exam frequency (Ethical Guardrail #8, and [B3] do-not-retrieve #4):

| B1 # | Trap | Tag | Where the chapter defuses it |
|---|---|---|---|
| 30 | "A container image includes the OS kernel" | `[source]` | §2, and Bearings #1 |
| 31 | "You patch a running container" | `[source]` | §2 immutability; Soundings Q1 surfaces the prior first |
| 32 | "OCI is a runtime" | `[source]` | §5 Fixed Point #3 |
| 33 | Conflating OCI with CRI | `[inferred]` | §5 ⚠ Navigational Hazards — the chapter's hardest discrimination |
| 34 | "Docker is the container runtime Kubernetes uses" | `[inferred]` | §4 🪝 Snag; Soundings Q5 pre-tests it |
| — | `:latest` as a naming-hygiene issue only | `[source]` (k8s-docs-images) | §3 ⚠ + §6 — the tag also sets the pull policy |
| — | "`Always` re-downloads every launch" | `[source]` (k8s-docs-images) | §6 Dead Reckoning; Bearings #3 |

**Do not include** in the Exam Alert: anything about Pod failure diagnosis beyond naming `ImagePullBackOff` (Chapter 13), image signing or SBOMs (Chapter 12), or the deployment-eras timeline (Chapter 3).

---

## 7. Practice Questions plan

**Target count: 25** — the highest per-chapter allocation in the book, from B4's weight-monotonic derivation `15 + 2 × (weight − 4)` at this chapter's 9 points. It is the ceiling of the skill's 15–25 per-chapter range; nothing is clipped.

**Distribution across sections**, proportional to conceptual load and exam surface:

| Section | Questions | Rationale |
|---|---|---|
| §1 container vs VM | 3 | Foundational, low ambiguity, small item space |
| §2 image contents, layers, build | 4 | Contents and layers; build practices lightly (see gap note) |
| §3 registries, tags, digests | 5 | Largest allocation — densest exam surface, carries Fixed Point #1 |
| §4 CRI chain | 4 | Most-retrieved concept in the chapter |
| §5 OCI three specs | 4 | High name-density, high discrimination value |
| §6 `imagePullPolicy` | 3 | Fiddly but small; the defaults table is the whole target |
| §7 RuntimeClass | 2 | Genuinely smaller surface; two well-built items beat four padded ones |
| **Total** | **25** | |

**Interleaving strategy.** With no earlier chapters to draw from, interleaving is cross-*section* within the chapter. **At least 6 of the 25 must require combining two sections**, and the highest-value pairings are already known:

- §3 + §6 — a tag choice that changes both identity *and* pull behavior. The single best integrative item in the chapter
- §4 + §5 — given a described function, name both the interface and the specification that govern it
- §2 + §5 — layers as the thing image-spec standardizes
- §1 + §7 — the isolation tradeoff, renegotiated
- §3 + §5 — registries as distribution-spec implementations

**Forward-compatibility constraints** (this chapter's items also become candidate sources for the Ch 20 mock, so they must not age into other chapters' territory):

- No item may depend on Pod phases, container states, Secrets, `kubectl` verbs, or scheduling. All are later chapters.
- Items testing `ImagePullBackOff` test recognition only; Chapter 13 owns diagnosis and will retrieve this item's concept by name.
- Every `[inferred]` trap used as a distractor gets a why-wrong explanation phrased as "these are easy to confuse," never as a frequency claim.
- Why-wrong explanations required for **all** options on all 25 items, per the contract and the ethical checklist.

---

## 8. Required figures

Six figures — five concept diagrams plus the chapter's one Zenith. All are stubs for Stage 10 `yaml-figure-spec` extraction and the sibling `certcomp-diagrams` pipeline. `diagram_enforcement.enabled` is `false` for this book, so the linter will not check for rendered artifacts yet. Anchor IDs are carried verbatim from the arc outline and must not be renamed — they are the join key.

### `ch02-fig01-vm-vs-container-stack`

- **Purpose**: make the §1 architectural contrast visible in one glance, so that every downstream difference (size, start time, density) reads as a consequence rather than a separate fact.
- **Content**: two stacks side by side. VM side: hardware → host OS → hypervisor → per-VM guest OS → app. Container side: hardware → host OS → container runtime → per-container app. The visual argument is the **repeated guest OS on one side and its absence on the other** — that duplication is the whole point and should be the most salient thing in the image.
- **Label budget**: ~9 labels. Within tolerance because the structure is two parallel stacks, not a network. Do not add per-layer annotations; the caption carries the "why."
- **Grayscale**: the two stacks must be distinguishable by position and layer count alone, never by fill color.
- **Copyright clearance**: `own_interpretation`. This is the most-drawn diagram in the container industry; the arrangement and emphasis must be ours, not a redraw of a recognizable vendor figure.

### `ch02-fig02-image-layers-and-digests`

- **Purpose**: carry two related ideas that the prose splits across §2 and §3 — that an image is a stack of layers, and that hashing that stack produces the digest which a tag merely *points at*.
- **Content**: left, a stacked set of filesystem layers with a shared base visibly shared between two images. Right, the assembled image resolving to a content hash, with one tag label attached by an arrow that is drawn to look **detachable** — and a second, ghosted arrow showing the same tag pointing elsewhere later. The movable-label affordance is the pedagogy; if a reviewer cannot see that the tag could move, the figure has failed.
- **Label budget**: ~8. At the threshold. If it crowds, drop the second image from the left half and keep base-layer sharing implicit in the caption.
- **Grayscale**: the ghosted "moved tag" arrow must remain distinguishable from the solid one without color — use dash pattern.
- **Dependency**: ⚠ **this figure is gated on the open half of G29.** The layer half cannot be specified beyond "a stack with a shared base" until Stage 2 returns a source covering layer mechanics. If G29 stays open, reduce this figure to the digest/tag half and rename the anchor in `image-specs.md` — a change that must be made *before* Stage 10, not after.
- **Copyright clearance**: `own_interpretation`.

### `ch02-fig03-oci-three-specs`

- **Purpose**: hold three specifications and their scopes in one image, and — jointly with `ch02-fig04` — make the OCI/CRI boundary visible rather than merely asserted.
- **Content**: the three specs as three bands over the artifact lifecycle: image-spec governing the image format, distribution-spec governing the transfer between registry and node, runtime-spec governing the unpacked bundle's execution. Overlay the three-beat flow — **download image → unpack to filesystem bundle → run bundle** — so the specs and the flow are the same picture.
- **Label budget**: ~9 (3 spec names + 3 flow stages + 3 scope labels). Acceptable as a linear pipeline. Do **not** add the v1.0 date or the founding date to the figure; those are prose facts.
- **Paired design**: must share visual grammar with `ch02-fig04` so a reader can lay them side by side and see two different planes. Commission them together, not separately.
- **Grayscale**: three bands must be separable by border weight or pattern, not hue.
- **Copyright clearance**: `own_interpretation`.

### `ch02-fig04-cri-runtime-chain`

- **Purpose**: the chapter's most load-bearing diagram. It answers the chapter's curiosity gap, carries Fixed Point #2, and is re-presented or back-beared in Ch 3, Ch 8, Ch 13, and Ch 17.
- **Content**: a single horizontal chain — kubelet → **CRI** (drawn as an *interface boundary*, not a box) → containerd / CRI-O shown as interchangeable alternatives → runC → the running process. The interchangeability of the middle position is the pedagogical payload; render the alternatives as slotting into one socket rather than as two parallel paths.
- **Label budget**: ~7. At the comfort threshold exactly. Resist adding the OCI specs to this figure — that is `ch02-fig03`'s job, and merging them is the fastest way to reintroduce the exact conflation §5 exists to prevent.
- **Reuse**: **design this for re-presentation.** Ch 17's secondary Zenith shows CRI, CNI, CSI, and CRDs as one pluggability story; if `ch17` can be built as four instances of this figure's socket motif, the reader gets the recognition beat for free. Establish the socket visual grammar here, deliberately, and tell the Ch 9 and Ch 11 outlines it exists.
- **Grayscale**: the interface boundary must read as a boundary in grayscale — use a distinct line treatment, not a color fill.
- **Copyright clearance**: `own_interpretation`.

### `ch02-fig05-imagepullpolicy-decision`

- **Purpose**: convert §6's defaults from a four-row lookup table into a decision the reader can walk, since the defaults are conditional on how the reference was written — a structure prose handles badly and a decision tree handles well.
- **Content**: a decision tree rooted at "was `imagePullPolicy` set explicitly?" → if no, branch on the reference form (digest / `:latest` / no tag / other tag) to the four defaults; if yes, the three policies and what each does. Terminal nodes should show the *behavior*, not just the policy name.
- **Label budget**: ~11. Above the ~7-label threshold, but a decision tree is traversed one branch at a time rather than held whole in working memory, so the effective load is low. Flag for the figure reviewer; if it reads as crowded, split the "set explicitly" half into the adjacent prose and keep only the defaults tree.
- **Redundancy check**: the Dead Reckoning block in §6 states the same facts. Per Part 18.7 the caption must add *what to notice* — that the tag silently sets the behavior — rather than restating the branches.
- **Grayscale**: fine as line art; no color dependency.
- **Copyright clearance**: `own_interpretation`.

### `ch02-zenith-standard-crate`

- **Purpose**: the chapter's single dramatic synthesis illustration (Part 18.10 — exactly one per content chapter). Fires at §8, where standardization-of-the-interface resolves into one idea.
- **Content**: the intermodal argument rendered in the book's register — identical crates moving between incompatible carriers, each carrier built once against a published specification, the contents never inspected and never mattering. The Communications Officer's vantage, per the locked architectural rule: **no narrator face.** The synthesis must be legible as being *about interfaces*, not about shipping — a reader who sees only a nice port scene has received a decorative illustration, which Part 18.4 bans.
- **Label budget**: minimal by design. A Zenith illustration is an arousal beat, not a diagram. If it needs more than two or three labels, it is trying to be a concept diagram and should be rethought.
- **Era placement**: this book is Communications Officer / early interstellar per the role-family register. The crate motif must work in that register rather than defaulting to age-of-sail — check against `illustrator-brief.md` before commissioning, since Ch 2's subtitle names a *shipping container*, a 20th-century object, and the book's era placement is not 20th century. Raised in § Open questions #7.
- **Copyright clearance**: `own_interpretation`.

---

## 9. Open questions for the author

1. **Resolve the kernel-versus-OS wording, and resolve it in both chapters at once.** `chapter-01-taking-departure.md` line 140 carries a live `AUTHOR-REVIEW` comment: the cached snapshot says containers share "the Operating System (OS) among the applications," and Chapter 1's answer key sharpened that to "operating system kernel," which is more precise and standard but not verbatim. §1 of this chapter is where that sentence gets its full treatment, so the decision cannot be deferred again. **Recommendation:** keep the sharpening — it is the technically correct and universally used formulation — but source-tag it to the snapshot with the softer phrasing intact nearby, and edit Chapter 1's comment out once both chapters agree. Whichever way it goes, the two chapters must match; the reconcile pass will catch it if they don't.

2. **G29 is only half-closed, and `ch02-fig02` depends on the open half.** Cached sources now cover tags, digests, registries, `imagePullPolicy`, and Buildpacks. They still do **not** cover layer mechanics, layer caching and dedup, multi-stage builds, or base-image selection guidance — `oci-overview` offers the single phrase "filesystem layer serialization." Options: (a) Stage 2 fetches a layer/build-practices source and §2 is drafted in full; (b) §2 narrows to image *contents* plus Buildpacks, layers are described qualitatively as "a stack with a shared base," and `ch02-fig02` reduces to its digest half. **Recommendation: (a)** — this is the heaviest-weighted chapter in the book and layers are load-bearing for both the digest concept and the Chapter 12 supply-chain material. But (b) is a legitimate scope cut if the fetch is expensive, and it must be decided **before** Stage 10, because it changes a figure anchor.

3. **G30 is closed — confirming so it isn't re-flagged.** `k8s-docs-runtime-class-2026-08-23.md` supplies the RuntimeClass motivation, both sandbox examples (Kata / gVisor), handler configuration, and Pod overhead. B1 listed G30 as blocking for this chapter; it no longer is. §7 can be drafted from cache.

4. **Section-to-figure ordinal mismatch — confirm the resolution.** `ch02-fig03` (OCI) sits in §5 and `ch02-fig04` (CRI) sits in §4, so the anchor ordinals do not run in section order. This outline keeps the arc-outline stub IDs verbatim because they are join keys for `image-specs.md` and the diagram pipeline, and because §4-must-be-CRI is forced by a published Chapter 1 cross-bearing. The alternative — renaming the two anchors to restore ordinal order — is cosmetic and costs a rename across the arc outline. **Recommendation: keep the IDs, accept the mismatch.** Flagged only so the Stage 10 reviewer doesn't read it as a planning error.

5. **Bearings raised 10 → 12.** Three conceptual arcs, three checkpoints, four questions each; chapter total moves 43 → 45. B4 explicitly sanctions exceeding the Bearings minimum and anticipates 12–15 for multi-arc chapters, though it named Ch 8, 12, and 17 rather than Ch 2. Confirm, or cut checkpoint #3 to two questions and fold `imagePullPolicy` into checkpoint #2 (not recommended — it pairs unrelated cognitive modes).

6. **B3 never produced its artifact, and this is the second chapter to work around it.** `.pipeline-state/book-outline/retrieval-architecture.md` contains B3's tool-permission failure message, not B3's document; the arc outline reconstructed six of nine cross-cutting themes from B2. **Chapter 2 is unaffected** — it has no retrieval obligations at all — so this chapter can be drafted without waiting. But Chapter 3 opens the retrieval schedule at 10% drawing from *this* chapter, with two named anchors (CRI boundary, image immutability), and every chapter after inherits the reconstruction. Re-running B3 is cheap now and expensive at Chapter 12. **Recommendation: re-run B3 before Ch 3's Stage 1.**

7. **Era placement versus the shipping-container metaphor.** The chapter title, subtitle, and Zenith all rest on a 20th-century intermodal shipping container, while the book's role-family register places KCNA in the early-interstellar era. These are reconcilable — standardized cargo units are era-universal and the argument is about interfaces, not about the 1950s — but the Zenith illustration has to actually resolve it, and the illustrator brief should be consulted before commissioning rather than after. Confirm the crate reads in-register.

8. **The 9% weight is authored judgment and G37 did not fix it.** `lf-lfs250-course-outline-2026-08-23.md` is cached, closing G37 as a *fetch* — but it turns out to be a seven-line course-module list with no sub-bullets and no weights. It does not firm up the sub-competency allocation that B1 flagged as G33/G36, so this chapter's 9 points, its "heavy" depth band, and its 25 Practice Questions all remain derived from concept count and prerequisite load rather than from published data. That is disclosed at book level (B2 disclosure #1) and needs no in-chapter restatement. Noted here so a later stage doesn't record G37 as having resolved the weighting question.

9. **Epigraph.** Not drafted, per the no-prose constraint. Two directions in the skill's Part 15 order of preference: a real quote on standardization or logistics — Malcolm McLean's containerization work is the obvious well and would be genuinely apt — or an original Lodestar epigraph about the crate outlasting the ship. The real quote is preferable here because Chapter 1 already spent an original, and Part 15 puts attributed quotes first. Author's call; verify any attributed quote against a source before it ships.

10. **Confirm the Ch 17 reciprocal.** §4 and §8 both forward-bear to Chapter 17's extension-points Zenith, and §4 establishes the socket visual grammar that `ch17` is meant to reuse four times. Chapter 17's outline does not exist yet. **Action:** when Ch 9 (CNI) and Ch 11 (CSI) reach Stage 1, their outlines must be told that `ch02-fig04` established a reusable motif — otherwise three chapters will independently invent three different ways to draw a pluggable interface, and the secondary Zenith loses most of its force.
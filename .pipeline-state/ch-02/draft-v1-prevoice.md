# Chapter 2: Cargo in Standard Crates
## *"Why the shipping container beat the ship"*

**Exam domain: Kubernetes Fundamentals (44% of the exam) — competency: Containerization** [source: cncf-kcna-certification-page-2026-08-23] **| Estimated share of the exam: ~9% (authored allocation — CNCF publishes domain weights, not competency weights; see front matter) | Complexity: Mixed | Novelty: Moderate**

---

## Attention Budget

**Total time: ~85 minutes | Recommended: single session if you're fresh; otherwise split at Taking Your Bearings #2**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 What a Container Actually Is | 8 min | Low | Anytime |
| §2 What's Inside an Image | 10 min | Low | Anytime |
| §3 Registries, Tags, and Digests | 14 min | Medium | When alert |
| ☆ Taking Your Bearings #1 | 6 min | Medium | After a short break |
| §4 The Container Runtime Interface | 12 min | Medium | When alert |
| §5 The Open Container Initiative | 10 min | Medium | When alert |
| ☆ Taking Your Bearings #2 | 6 min | Medium | After a short break |
| §6 When Kubernetes Pulls, and When It Doesn't | 9 min | High | Peak attention |
| §7 Not All Isolation Is Equal: RuntimeClass | 6 min | Medium | When alert |
| ☆ Taking Your Bearings #3 | 6 min | Medium | After a short break |
| §8 The Crate, Not the Cargo | 4 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime.
- **Medium:** New vocabulary requiring focus — study when alert.
- **High:** Conditional rules that must be recalled precisely — study at peak attention.

*If you only have 15 minutes: read §3 and §4, then take Taking Your Bearings #1 and #2. Those two sections carry two of the chapter's three Fixed Points and the largest share of its exam surface.*

---

> *"The crate outlives the ship. Standardize the crate."*
> — Lodestar Ledgers

<!-- AUTHOR-REVIEW: outline § Open questions #9 preferred a real attributed quote (Malcolm McLean on containerization was the suggested well). No cached snapshot contains a verifiable McLean quotation, and Part 15 plus Ethical Guardrail #2 forbid shipping an attribution we cannot source. An original Lodestar epigraph is used instead. If the author can verify a McLean line against a primary source, substitute it here. -->

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score decides how to approach the material — no shame in any score, just different reading strategies.

1. You have an application running in a container and you need to change one line of a configuration file inside it. Is editing the file in the running container the intended way to make that change persist, or is there a different intended workflow?

2. You pull an image reference — say `myapp:v2` — today, and someone on your team pulls the same reference next week. Are you guaranteed to have received the same bytes?

3. You write an image reference as just `nginx`, with no hostname in front of it. Where does that image get fetched from?

4. You build two images from the same starting point — the same base — and store both in the same place. Is that shared starting point stored once, or twice?

5. Kubernetes runs containers. Does that require Docker specifically to be installed on the machines running them?

6. The container image format — the layout of the artifact you push to a registry and pull onto a machine — is defined by whom? A single company, or something else?

7. Every container on a machine gets the same strength of isolation from every other container. True or false?

8. A machine has already downloaded a particular image. The next time it needs to start a container from that image, does it download it again?

<details>
<summary>Click for answers + reading strategy</summary>

1. **There's a different intended workflow.** The change belongs in a new image, not in a live container. §2 covers why this is the rule rather than a preference.

2. **No — not guaranteed.** *[cross-bearing: see Ch 2 §3 — tags, digests, and what an image reference actually resolves to]*

3. **From a default registry that Kubernetes assumes when you don't name one.** §3 names it and shows the other two defaults hiding in the same short string.

4. **Once.** Images are assembled from stacked layers, and a shared starting point is a shared layer. §2 has the structure.

5. **No.** Kubernetes talks to a runtime through an interface, and several different runtimes satisfy it. *[cross-bearing: see Ch 2 §4 — the Container Runtime Interface]*

6. **Not a single company.** The format is governed by a standards body. *[cross-bearing: see Ch 2 §5 — the Open Container Initiative]*

7. **False.** Isolation strength is selectable per workload. §7 covers the mechanism and, more importantly, why anyone would want it.

8. **It depends — and what it depends on will surprise you.** §6 has the four-case rule, and it hinges on how you wrote the reference, not on what you configured.

**If you got 6+ right:** skim. Focus on the ★ Fixed Points and ⚠ Navigational Hazards callouts, and take all three Taking Your Bearings checkpoints. Do not skip §5 (OCI) or §7 (RuntimeClass) regardless of your score — those two sections score well on intuition and still surprise people on the exam.

**If you got 3–5 right:** read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** read carefully, in its own session. This is the chapter every later chapter rests on, and there's no shortcut through it. Nothing here is difficult; there's simply a lot of new vocabulary, and every term is defined before it's used.

</details>

---

## Why This Chapter Matters

Here is a sentence that should stop you: **Kubernetes cannot run a container.** Not one, not ever, on any cluster you will ever touch. Every container on every node is started by software that is not Kubernetes, reached across a boundary that Kubernetes only defines. That is not a limitation someone forgot to fix. It is the design, it is deliberate, and by the time you finish §4 you will be able to draw it.

Chapter 1 told you that an orchestrator is not a runtime *[cross-bearing: see Ch 1 §Soundings A2 — orchestrator versus runtime]*. That was a one-line correction. This chapter turns it into a mechanism.

What you are actually building here is discrimination — the ability to tell near-identical things apart. That is the competence the whole exam measures, and it is the competence this chapter installs at the deepest level in the stack. A practitioner who has this chapter can be handed any unfamiliar container tool — a runtime they've never heard of, a new build system, somebody's registry product — and place it on a map in about ten seconds: does this thing *produce* images, *distribute* them, or *run* them, and which specification is it conforming to? That placement instinct is the difference between someone who has memorized the words "containerd, CRI-O, runC" and someone who understands why those three names are not a list of alternatives.

The stakes here are structural, and worth stating plainly once. This is the first content chapter because containerization is the deepest root in the book's dependency graph — not because it's an easy warm-up. Reader who leaves this chapter treating "container" as an undefined primitive will find that Chapter 3's runtime boundary, Chapter 13's failed-image-pull diagnosis, and Chapter 17's entire argument about how Kubernetes is extended each land slightly wrong. Not catastrophically. Just slightly, three times, in ways that are hard to trace back here. Better to spend the time now.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Distinguish** a container from a virtual machine by what each one shares with the host, and explain why that single difference produces every other difference people cite.
- **Explain** what a container image contains, what it deliberately does not contain, and why the correct response to a needed change is a new image rather than an edited container.
- **Predict** which bytes a given image reference resolves to — including when a tag will silently resolve to something different than it did last week, and when a digest guarantees that it cannot.
- **Trace** the path from a Pod's image field to a running process, naming each component in the chain and stating which specification governs each hop.
- **Choose** an `imagePullPolicy` deliberately, and state what Kubernetes will do by default when you don't.

*You'll also be able to look at an unfamiliar container tool and say what layer it operates at — which is how practitioners actually navigate this ecosystem.*

---

## §1 — ⚪ What a Container Actually Is

**If you remember nothing else:** a container is repeatable because everything it needs travels with it.

Start with what a container buys you, because the definition follows from the benefit. Each container that you run is repeatable; the standardization that comes from having dependencies included means that you get the same behavior wherever you run it [source: k8s-docs-containers-2026-08-23]. That's the whole proposition. Containers decouple applications from the underlying host infrastructure, which is what makes deployment easier across different cloud or operating-system environments [source: k8s-docs-containers-2026-08-23].

Notice what that claim is *not*. It is not "containers are fast." It is not "containers are small." Speed and size are consequences. The proposition is *sameness*: the thing that ran on your laptop is the thing that runs on the node, because the dependencies are not assumptions about the host — they're contents.

Now the comparison everyone reaches for, done at the level that actually explains it.

Virtualization lets you run multiple virtual machines on a single physical server's CPU, isolating applications between VMs so that one application's information cannot be freely accessed by another. Each VM is a full machine running all the components, including its own operating system, on top of virtualized hardware [source: k8s-docs-overview-2026-08-23]. Read that last clause again: *its own operating system*. Ten VMs on a host means ten operating systems booted, patched, and consuming memory before a single line of your application runs.

Containers are similar to VMs, but they have relaxed isolation properties in order to share the operating system among the applications — and *therefore* containers are considered lightweight. Similar to a VM, a container has its own filesystem, share of CPU, memory, process space, and more; because containers are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions [source: k8s-docs-overview-2026-08-23].

<!-- AUTHOR-REVIEW: outline § Open questions #1. The cached snapshot phrases the sharing as "share the Operating System (OS) among the applications." Chapter 1's Soundings answer key sharpened this to "operating system kernel," which is the standard and more precise formulation, and flagged the sharpening for author review. This draft carries BOTH: the snapshot's wording is quoted and tagged above, and the sharpened formulation appears below as an explicit editorial precision note rather than as a sourced claim. Decision needed: keep the sharpening in both chapters (recommended), or soften both to the snapshot wording. Whichever way it goes, edit Chapter 1's AUTHOR-REVIEW comment out once the two chapters agree — the reconcile pass will surface a mismatch. -->

A precision note, because you will meet this everywhere and should meet it correctly: when practitioners say a container "shares the OS," what is shared is the host's **kernel** — the part of the operating system that actually talks to hardware, schedules processes, and enforces boundaries. Everything above the kernel that the application needs — its libraries, its files, its view of the process table — comes from the container itself. That is why a container has its own filesystem and its own process space while still running on somebody else's kernel.

Now the single most useful move you can make with this material: stop memorizing the comparison table and derive it instead. Every difference between a container and a VM that anybody cites comes out of that one architectural choice.

<!-- FIGURE: ch02-fig01-vm-vs-container-stack -->
```
        VIRTUAL MACHINES                       CONTAINERS

   ┌──────┐ ┌──────┐ ┌──────┐          ┌──────┐ ┌──────┐ ┌──────┐
   │ App  │ │ App  │ │ App  │          │ App  │ │ App  │ │ App  │
   ├──────┤ ├──────┤ ├──────┤          └──┬───┘ └──┬───┘ └──┬───┘
   │Guest │ │Guest │ │Guest │             │        │        │
   │  OS  │ │  OS  │ │  OS  │          ┌──┴────────┴────────┴──┐
   └──┬───┘ └──┬───┘ └──┬───┘          │   container runtime    │
      │        │        │              ├────────────────────────┤
   ┌──┴────────┴────────┴──┐           │        host OS         │
   │      hypervisor        │          ├────────────────────────┤
   ├────────────────────────┤          │       hardware         │
   │        host OS         │          └────────────────────────┘
   ├────────────────────────┤
   │       hardware         │           ONE OS · three apps
   └────────────────────────┘
    THREE OS COPIES · three apps
```

**Figure 2-1.** The duplication on the left is the entire story. Notice what to look for: the guest-OS row repeats once per workload on the VM side and does not appear at all on the container side. Start-up time, image size, and how many workloads fit on a host are all downstream of that one row.

Derive it yourself. Booting a guest operating system takes time, so VMs start slowly and containers start quickly. A guest operating system occupies disk and memory, so VM images are large and containers are small. Three guest kernels on one host means three times the baseline resource cost, so container density is higher. You do not need three facts. You need one fact and the willingness to follow it.

> ⚓ **Worth Securing:** "Relaxed isolation" is a *tradeoff*, not a deficiency. The docs use exactly that word — *relaxed* — and being honest about it is what makes the rest of the picture coherent. You gave up a boundary in exchange for weight, and because it was a trade, it can be renegotiated per workload when a particular workload deserves the boundary back. *[cross-bearing: see Ch 2 §7 — when relaxed isolation is not enough]*

One forward plant, and then we move on. Containers in a Pod are co-located and co-scheduled to run on the same node [source: k8s-docs-containers-2026-08-23]. You do not need to know what a Pod is yet — it is Chapter 5's whole subject, and it comes with a shared network namespace and a lifecycle of its own *[cross-bearing: see Ch 5 §1 — the Pod as the unit of scheduling]*. For now, register only this: containers are not the unit Kubernetes schedules. Something wraps them.

---

## §2 — ⚪ What's Inside an Image

A container is a running thing. An image is the package it runs from, and it is worth being precise about the contents, because the exam tests the contents and — more usefully — because the negative space in that list explains §1 backwards.

A container image is a ready-to-run software package containing everything needed to run an application: the code and any runtime it requires, application **and** system libraries, and default values for any essential settings [source: k8s-docs-containers-2026-08-23]. Said another way, a container image represents binary data that encapsulates an application and all its software dependencies; images are executable software bundles that can run standalone and that make very well-defined assumptions about their runtime environment. You typically create a container image of your application and push it to a registry before referring to it in a Pod [source: k8s-docs-images-2026-08-23].

That phrase — *very well-defined assumptions about their runtime environment* — is doing quiet work. An image is not self-sufficient. It is *explicit* about what it expects from underneath. And the largest thing it expects from underneath is the one thing it does not carry.

**An image contains no kernel.** That isn't a separate fact to memorize; it's §1 read in reverse. If containers get the kernel by sharing the host's, the image cannot be shipping one — a shipped kernel would have to be booted, and booting it is precisely what a virtual machine does and a container does not. Every time you see a question implying that a container image bundles an operating system kernel, you are looking at the same misconception wearing a different hat.

System libraries, though, *are* included [source: k8s-docs-containers-2026-08-23] — which is where people get tangled, because system libraries feel like part of the OS. They are part of the operating system's userspace, and userspace is exactly what the image supplies. Kernel below, everything above it in the crate.

### Immutability, and why it's a rule rather than a preference

Containers are intended to be stateless and immutable: you should not change the code of a container that is already running. If you have a containerized application and want to make changes, the correct process is to build a new image that includes the change, then recreate the container to start from the updated image [source: k8s-docs-containers-2026-08-23].

Read the shape of that instruction. It does not say "editing a running container is discouraged." It says the *correct process* is different in kind: build, then recreate. Two steps, neither of which is "edit."

This is the habit that readers with virtual-machine or bare-metal backgrounds find hardest to break, and it's worth naming why, because the reason is honorable. If you have spent years administering long-lived servers, the skill you built was *repair* — log in, diagnose, fix in place, verify. That skill is genuinely valuable and it is genuinely the wrong instinct here. In a container world, the fix goes in the image and the container gets replaced. Repair-in-place produces a running thing that no image can reproduce, which forfeits the one property you adopted containers to get: sameness.

The payoff is concrete. Image immutability is exactly what makes quick and efficient rollbacks possible [source: k8s-docs-overview-2026-08-23]. You can go back to the previous version because the previous version still exists, unchanged, as a distinct artifact. Edit containers in place and there is nothing to go back to.

### Layers

An image is not a single opaque blob. The OCI Image Format encompasses the image manifest, **filesystem layer serialization**, and image configuration needed to launch applications on target platforms [source: oci-overview-2026-08-23]. In other words, the contents arrive as a set of filesystem layers, described by a manifest that names them, plus a configuration that says how to start the thing.

The immediate practical consequence is sharing. If two images are built starting from the same base, both of their manifests name that same base layer, and the layer is stored and transferred once rather than twice.

<!-- FIGURE: ch02-fig02-image-layers-and-digests -->
```
        LAYERS                                 IDENTITY

   image A      image B                ┌──────────────────────────┐
  ┌─────────┐  ┌─────────┐             │   sha256:9f2c…be41       │
  │   app   │  │   app   │             │   digest = content hash  │
  ├─────────┤  ├─────────┤             │   immutable              │
  │ shared  │══│ shared  │             └──────────────────────────┘
  │  base   │  │  base   │                  ▲                ▲
  └─────────┘  └─────────┘            ───────┘         ┄┄┄┄┄┄┄┘
                                      solid            dashed
   both manifests name               ┌──────┐         ┌──────┐
   the SAME base layer               │ :v2  │         │ :v2  │
   → stored once                     └──────┘         └──────┘
                                      today          next week

                                  a tag is a LABEL — it can be
                                  moved to point at a different image
```

**Figure 2-2.** Two ideas in one frame, because §3 depends on the right half. What to notice: the dashed arrow. The tag `:v2` is attached to the image, not part of it — and an attachment can be re-attached.

<!-- AUTHOR-REVIEW: outline § Open questions #2 — G29 is only half-closed. Cached sources cover image contents, tags, digests, registries, imagePullPolicy, and Buildpacks. They do NOT cover layer caching mechanics, storage deduplication behavior, multi-stage builds, or base-image selection guidance. `oci-overview` supplies only the phrase "filesystem layer serialization." This section therefore describes layers qualitatively — a stack with a shared base named by the manifest — and stops. It does not assert dedup implementation details, cache-invalidation ordering ("put the layers that change least at the bottom"), or multi-stage build guidance, all of which would be unsourced. Two resolutions: (a) Stage 2 fetches a layer/build-practices source and this subsection is expanded; (b) accept the narrowed scope, in which case ch02-fig02 should be reduced to its digest half and renamed in image-specs.md BEFORE Stage 10. Recommendation (a) — layers are load-bearing for both the digest concept and the Chapter 12 supply-chain material. -->

Note what the layer structure buys forward: the layers described here are precisely the thing that a specification standardizes, which is why any registry can serve any image and any conformant runtime can unpack one *[cross-bearing: see Ch 2 §5 — the OCI image specification]*.

### Building images without writing build files

You do not have to hand-author a build file to produce an image, and the exam's ecosystem awareness extends to knowing the alternative exists.

A **buildpack** is software that transforms application source code into runnable artifacts by analyzing the code and determining the best way to build it. A **builder** is an OCI image containing an ordered combination of buildpacks and a build-time base image, a lifecycle binary, and a reference to a runtime base image. The base images come in a pair: the *build image* is the environment in which the buildpacks run, and the *run image* is the base for the final application image; that pairing is called the **stack**. A **platform** — the `pack` CLI, or a CI system — orchestrates the process by invoking the lifecycle binary together with the buildpacks and the application source to produce a runnable OCI image. The lifecycle runs in phases: **detect** (determine which buildpacks apply), **build** (compile and assemble the application), and **export** (create the final OCI image with reproducible layers). Cloud Native Buildpacks is a CNCF graduated project [source: buildpacks-concepts-2026-08-23].

> ⚓ **Worth Securing:** The build-image / run-image split is the idea worth taking from Buildpacks even if you never use them. The environment that *compiles* your application and the environment that *runs* it do not have to be the same environment, and they usually shouldn't be — compilers, headers, and build tooling are attack surface that your production image has no use for. Buildpacks make that separation structural rather than a discipline you have to remember.

> 🔭 **Closer Look:** The export phase produces *reproducible* layers [source: buildpacks-concepts-2026-08-23] — meaning the same input reliably produces the same layer bytes rather than layers that differ run to run because of timestamps or file ordering. That property is deeper than the exam requires, but it's the hinge on which supply-chain verification swings: you cannot meaningfully attest to an artifact whose bytes change when nothing changed. *[cross-bearing: see Ch 12 §2 — signing, attestation, and the software supply chain]*

<!-- AUTHOR-REVIEW: no authoritative source in the cached set for base-image *selection* guidance (smaller base → smaller attack surface → faster pull, traded against debuggability). Outline §2 planned a ⚓ callout on exactly this; it has been replaced with the build/run-image split, which IS sourced. Restore the selection guidance only if Stage 2 closes the open half of G29. -->

Supply-chain security — scanning, signing, bills of materials — is a real concern that attaches to everything in this section, and it is not this chapter's. It gets a full treatment later *[cross-bearing: see Ch 12 §1 — securing the image supply chain]*.

---

## §3 — 🔵 Registries, Tags, and Digests

This is the densest exam surface in the chapter, and it hangs on one distinction that most practitioners carry wrong for years without consequence — right up until the afternoon it costs them.

### An image reference has parts

Container images are usually given a name such as `pause`, `example/mycontainer`, or `kube-apiserver`. Images can also include a registry hostname — for example `fictional.registry.example/imagename` — and possibly a port number as well. **If you don't specify a registry hostname, Kubernetes assumes that you mean the Docker public registry.** After the image name, you can add a tag or a digest. Tags let you identify different versions of the same series of images. **If you don't specify a tag, Kubernetes assumes you mean the tag `latest`.** So `busybox` is equivalent to `docker.io/library/busybox:latest` [source: k8s-docs-images-2026-08-23].

Here are the defaults as a table, because that is what a table is for:

| What you write | What it resolves to | Which default filled the gap |
|---|---|---|
| `busybox` | `docker.io/library/busybox:latest` | registry **and** tag |
| `busybox:1.36` | `docker.io/library/busybox:1.36` | registry |
| `registry.k8s.io/pause` | `registry.k8s.io/pause:latest` | tag |
| `registry.k8s.io/pause:3.5` | exactly that | none |
| `registry.k8s.io/pause@sha256:1ff6…` | exactly those bytes | none |

Those last two forms are both from the documentation's own examples [source: k8s-docs-images-2026-08-23].

> 🪝 **Snag:** A bare name is not a bare name. `busybox` is three defaults stacked in a trench coat — a registry you didn't name, a namespace you didn't name, and a tag you didn't name. Every one of the three is a decision somebody made on your behalf, and at least two of them will matter to you eventually.

### The distinction this section exists for

Tags let you identify different versions of the same series of images. Digests are a unique identifier for a specific version of an image — **a hash of the image's content** — and are immutable; **tags can be moved to point to different images** [source: k8s-docs-images-2026-08-23].

Sit with the asymmetry. A digest is *derived from* the image. Change one byte of the image and you get a different digest, necessarily, because that is what a content hash is. You cannot move a digest to point at different content, in the same way that you cannot move the number 4 to mean 5.

A tag is *attached to* the image. It is a label, and labels come off.

★ **Fixed Point:**

> **A tag identifies a series and can be moved to point at a different image. A digest is a hash of the image's content and is immutable. Two pulls of `myapp:v2` a week apart are not guaranteed to be the same bytes. Two pulls of an image by digest are.**

If you recite one sentence from §1 through §3 cold, recite that one.

> ⚠ **Navigational Hazards**
>
> You should avoid using the `:latest` tag when deploying containers in production, as it is harder to track which version of the image is running and more difficult to roll back properly. Instead, specify a meaningful tag such as `v1.42.0` and/or a digest [source: k8s-docs-images-2026-08-23].
>
> That is the documented guidance, and most candidates absorb it as a naming-hygiene rule — untidy, faintly unprofessional, not really *dangerous*. That reading is incomplete, and the incompleteness is the trap. The `:latest` problem has a second half that has nothing to do with naming: **the tag you write also silently determines when Kubernetes will go looking for a new copy of the image.** Same field, second effect, and nobody warns you. §6 completes it. *[cross-bearing: see Ch 2 §6 — the tag determines the default pull policy]*

> **Logbook Entry:**
>
> The failure looks like this from the inside, and it is worth knowing the shape of it before you meet it.
>
> A deployment goes out. It behaves badly in a way nobody can reproduce locally. The manifest is checked — unchanged, same commit, same image reference as the version that has been running quietly for three weeks. So the manifest is checked again, this time by two people, out loud, line by line, because the alternative explanations are all worse. It is genuinely unchanged. The reference says `:v2` and it said `:v2` before.
>
> Someone eventually proposes the rollback, which is when the afternoon turns philosophical: rolling back to the previous configuration produces the *same reference*, which produces the *same bytes*, which produces the same bad behavior. The rollback rolls back to exactly where you already are. There is a particular quality of silence in a room where four competent people have just realized that the thing they were treating as an identity was a label the whole time.
>
> Nobody moved the tag maliciously. Somebody upstream rebuilt `:v2` with a dependency bump, which is a completely reasonable thing to do to a tag, because a tag identifies a series. The manifest was never the problem. The mental model was — and the tell, in hindsight, was that we spent an hour proving the manifest hadn't changed instead of one minute asking whether an unchanged manifest guarantees unchanged bytes.

### Registries, briefly

A registry is where images live between being built and being run — you push there and nodes pull from there [source: k8s-docs-images-2026-08-23]. It is a distribution layer, and it speaks a standardized API for the purpose, which is a fact §5 will hand you *[cross-bearing: see Ch 2 §5 — the distribution specification]*.

Private registries may require credentials to read images from them. Credentials can be supplied by: configuring nodes to authenticate to the private registry; a kubelet credential provider that fetches credentials dynamically; pre-pulled images; specifying `imagePullSecrets` on a Pod, which references a Secret of type `kubernetes.io/dockerconfigjson`; or vendor-specific and local extensions [source: k8s-docs-images-2026-08-23].

Five paths, named and left there deliberately. The one you will actually use most — `imagePullSecrets` — requires understanding Secrets, which you do not have yet and which arrive with their own security caveats. *[cross-bearing: see Ch 4 §4 — Secrets, and the `dockerconfigjson` type]* Registry access is also a genuine security boundary rather than a convenience feature *[cross-bearing: see Ch 12 §3 — restricting who can pull what]*.

---

## ☆ Taking Your Bearings #1: Containers, Images, and Identity

Four questions on §1 through §3. Answer before reading on.

**1.** A team needs to run a workload that requires a different operating-system kernel version than the one on the host machines. Which of the following is true?

A) Use a container and specify the required kernel in the image
B) Use a container and set the kernel version in the container's configuration defaults
C) A container is the wrong instrument here; the workload needs a virtual machine or a host with the required kernel
D) Use a container, since kernel version is negotiated at start-up

**2.** Which of the following is included in a container image?

A) The host's kernel
B) System libraries the application depends on
C) The node's network configuration
D) The cluster's registry credentials

**3.** You deploy a manifest referencing `myapp:v2` in April. In May, you redeploy the identical manifest — no changes of any kind — to the same cluster. Which statement is correct?

A) The bytes are guaranteed identical, because the reference is identical
B) The bytes are guaranteed identical, because tags are immutable by specification
C) The bytes may differ, because a tag can be moved to point at a different image
D) The bytes may differ, because Kubernetes re-resolves tags on a random schedule

**4.** A Pod specifies the image `redis`. Nothing else. What does that reference resolve to?

A) `redis:latest` from the cluster's configured default registry, whatever that is
B) `docker.io/library/redis:latest`
C) `registry.k8s.io/redis:latest`
D) It fails to resolve; a registry hostname is mandatory

---

**Answers with Explanations**

**1 — C.** A container shares the host's kernel and its image carries no kernel of its own [source: k8s-docs-overview-2026-08-23], so a kernel-version requirement cannot be satisfied by the container. A virtual machine boots its own guest operating system on virtualized hardware [source: k8s-docs-overview-2026-08-23], which is exactly the capability needed.
- **A is wrong**, and it is the single most common misconception in this chapter: an image bundles application and system libraries, not a kernel [source: k8s-docs-containers-2026-08-23].
- **B is wrong** because the "default values for essential settings" an image carries are application settings, not kernel selection.
- **D is wrong** — nothing about kernel version is negotiated at container start-up. The kernel is simply the host's.

**2 — B.** A container image contains the code and any runtime it requires, application **and system** libraries, and default values for essential settings [source: k8s-docs-containers-2026-08-23]. System libraries feel like operating system, which is why this option feels wrong and is right.
- **A is wrong** — see question 1.
- **C is wrong.** Node network configuration belongs to the node, not the artifact.
- **D is wrong.** Registry credentials are supplied to the kubelet by one of five external mechanisms [source: k8s-docs-images-2026-08-23], never baked into the image being pulled.

**3 — C.** Tags can be moved to point to different images [source: k8s-docs-images-2026-08-23]. An identical reference is not a guarantee of identical content; only a digest gives you that, because a digest is a hash of the image's content and is immutable [source: k8s-docs-images-2026-08-23].
- **A is wrong** for exactly that reason — this is the prior most readers arrive with.
- **B is wrong** and inverts the specification: digests are immutable; tags are movable.
- **D is wrong.** There is no random re-resolution; the mechanism is a human or system moving a tag, which is a normal thing to do to a tag.

**4 — B.** Omitting the registry hostname means Kubernetes assumes the Docker public registry, and omitting the tag means it assumes `latest`; the documentation's own worked example is `busybox` ≡ `docker.io/library/busybox:latest` [source: k8s-docs-images-2026-08-23].
- **A is wrong** because the default is not a cluster-configurable "whatever that is" — the assumption is specific.
- **C is wrong.** `registry.k8s.io` hosts Kubernetes project images and is used in the docs' examples, but it is not the assumed default.
- **D is wrong** — the whole point is that the hostname is optional and defaulted.

---

**Checkpoint: You've Now Mastered**
✓ Why a container is lightweight, and why every other container-versus-VM difference follows from that
✓ What an image contains, what it cannot contain, and why immutability is the process rather than a preference
✓ The tag/digest distinction — the chapter's sharpest single fact
✓ The three defaults hiding inside a bare image name

**If you scored 0–2:** stop here and reread §3, specifically the ★ Fixed Point and the table of reference forms. §4 through §6 all assume you can look at an image reference and say what it resolves to. That is about eight minutes of rereading and it will save you the rest of the chapter.

Two components left in the stack, and then you'll be able to draw the whole path from a manifest to a running process.

---

## §4 — 🔵 The Container Runtime Interface

Time to pay off the opening. Kubernetes cannot run a container — and here is the machinery.

### The runtime is a node component

The container runtime is a fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment. Kubernetes supports container runtimes such as **containerd**, **CRI-O**, and **any other implementation of the Kubernetes CRI (Container Runtime Interface)** [source: k8s-docs-containers-2026-08-23] [source: k8s-docs-cluster-architecture-2026-08-23].

Read the third item in that list carefully, because it is not padding. It is a promise about the shape of the system: the list of supported runtimes is *open*. Two are named because two are widely deployed; the qualifying condition is conformance to an interface, not membership in a list.

The runtime is a **node** component. It runs on every machine that runs workloads, alongthe kubelet and (optionally) kube-proxy [source: k8s-docs-components-2026-08-23]. A container runtime — containerd or CRI-O — must be installed on every node [source: k8s-docs-setup-tooling-2026-08-23]. Not on the control plane's behalf, not centrally: on each node, because that is where containers actually run.

The **kubelet** is the agent that runs on each node in the cluster. It makes sure that containers are running in a Pod: the kubelet takes a set of PodSpecs provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. Notably, the kubelet doesn't manage containers which were not created by Kubernetes [source: k8s-docs-cluster-architecture-2026-08-23].

So the kubelet is the component that *wants* containers to exist. The runtime is the component that *makes* them exist. Between them is the interface.

### CRI is an interface, not an implementation

Kubernetes' extension points include, under infrastructure extensions, the "container runtime (CRI, the Container Runtime Interface, to support alternative container runtimes)" [source: k8s-docs-extending-kubernetes-2026-08-23]. That single parenthetical is the whole design in one line. CRI exists *in order to* support alternatives. It is a socket, and the socket is the product.

And beneath the CRI runtime there is one more hop. Docker donated its container runtime, **runC**, to the Open Container Initiative to serve as the cornerstone of that effort [source: oci-overview-2026-08-23], and an OCI runtime's job is defined by the runtime specification: it runs a filesystem bundle that has been unpacked on disk [source: oci-overview-2026-08-23]. That is the lowest hop — the one where a process actually starts.

<!-- FIGURE: ch02-fig04-cri-runtime-chain -->
```
  ┌───────────┐
  │  kubelet  │   the node agent Kubernetes ships
  └─────┬─────┘
        │
  ══════╪══════════  C R I  ═══════════════════  interface boundary
        │            Kubernetes DEFINES this line
        │            and implements nothing below it
        ▼
  ┌──────────────────────────┐
  │ ▛▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▜ │    socket:
  │ ▌      containerd     ▐ │    exactly one conformant
  │ ▌       — or —        ▐ │    CRI runtime plugs in here
  │ ▌        CRI-O        ▐ │
  │ ▙▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▟ │
  └────────────┬─────────────┘
               ▼
        ┌────────────┐       ┌──────────────────┐
        │    runC    │  ──►  │ running process  │
        └────────────┘       └──────────────────┘
```

**Figure 2-3.** What to notice is the socket, not the boxes. containerd and CRI-O are not two parallel paths through the system; they are two things that fit the same opening. Swap one for the other and the kubelet above does not change.

★ **Fixed Point:**

> **kubelet → CRI → containerd or CRI-O → runC → a running process.**
>
> **Kubernetes defines the CRI. It does not implement it. Kubernetes never starts a container itself.**

<!-- AUTHOR-REVIEW: the containerd/CRI-O → runC hop is not stated explicitly by any cached snapshot. What IS sourced: (a) containerd and CRI-O are CRI implementations responsible for managing container execution and lifecycle [k8s-docs-containers]; (b) runC is the container runtime Docker donated to the OCI as the cornerstone of the effort [oci-overview]; (c) an OCI runtime runs a filesystem bundle unpacked on disk [oci-overview]. The "low-level runtime beneath the CRI runtime executes the bundle" framing is the standard and correct description of the architecture, and the Fixed Point above depends on it — it is the chapter's single most-retrieved item (Ch 3, Ch 8, Ch 13, Ch 17). Stage 2 should fetch a source that states the CRI-runtime-invokes-OCI-runtime relationship directly (kubernetes.io/docs/setup/production-environment/container-runtimes/ or the containerd architecture docs), OR the Fixed Point should be softened to "kubelet → CRI → CRI runtime → OCI runtime → process" with the runC example attached at spec level rather than as a named link in the chain. -->

> 🪝 **Snag:** "Docker" is four things wearing one name — a company, a command-line tool, a build format, and, historically, a runtime. Docker's public debut was a five-minute lightning talk in March 2013 introducing an upcoming open source tool for creating and using Linux containers, and its popularity is what set the stage for orchestration at scale [source: k8s-history-ten-years-2026-08-23]. So when someone says "Kubernetes runs Docker containers," at least three of those four meanings are doing no work at all. These are easy to confuse, and the confusion is historical rather than careless — for years the shorthand was accurate enough. The precise statement now is: Kubernetes runs containers via a CRI-conformant runtime, of which several exist [source: k8s-docs-containers-2026-08-23].

Both of the runtimes named in the documentation — containerd and CRI-O — are CNCF **graduated** projects, meaning they are considered stable, widely adopted, and production ready [source: cncf-project-maturity-levels-2026-08-23]. That matters less as trivia than as evidence: the pluggable position in the middle of Figure 2-3 is not theoretical. It has two mature occupants.

Usually, you can allow your cluster to pick the default container runtime for a Pod. If you need more than one container runtime in your cluster, you can specify a RuntimeClass for a Pod to make sure Kubernetes runs those containers using a particular container runtime [source: k8s-docs-containers-2026-08-23]. Most of the time, then, the runtime is invisible to you — which is exactly why §7 exists, and why most candidates skip it.

### The pattern to name now

> ⚓ **Worth Securing:** Give this move a name in your head, because you are about to see it three more times: **Kubernetes defines an interface and lets the ecosystem implement it.** The published extension points include not just CRI for runtimes but CSI (the Container Storage Interface) for storage types and CNI (the Container Network Interface) for pod networking, alongside device plugins and API extensions [source: k8s-docs-extending-kubernetes-2026-08-23]. Four sockets, one design instinct. You are looking at the first.

That is not a stray observation; it is the spine of the book's closing argument. *[cross-bearing: see Ch 9 §1 — CNI and pod networking]* *[cross-bearing: see Ch 11 §2 — CSI and storage drivers]* *[cross-bearing: see Ch 6 §3 — CRDs and extending the API]* *[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*

Two more pointers, then §5. The kubelet gets its full treatment as one node component among several *[cross-bearing: see Ch 3 §3 — node components in context]*. And knowing there is a layer *below* the Kubernetes API is what makes a particular diagnostic tool make sense — `crictl` reaches the runtime directly, beneath Kubernetes, which is occasionally exactly what you need [source: k8s-docs-debug-overview-2026-08-23] *[cross-bearing: see Ch 13 §5 — debugging nodes with crictl]*.

---

## §5 — 🔵 The Open Container Initiative

You now know that Kubernetes talks to a runtime through an interface. Underneath *that* is a second question the interface does not answer: who decided what an image looks like, how it moves across a network, and what it means to run one? Not Kubernetes. Kubernetes is a consumer of those answers, not their author.

### What the OCI is

The Open Container Initiative is an **open governance structure** for the express purpose of creating open industry standards around container formats and runtimes. It was established in **June 2015** by Docker and other leaders in the container industry [source: oci-overview-2026-08-23], and it operates under the Linux Foundation [source: oci-overview-2026-08-23].

Governance structure. Not software. It publishes documents.

★ **Fixed Point:**

> **The OCI is a governance body that publishes three specifications: the image specification, the distribution specification, and the runtime specification. It is not a runtime, not a company, and not a product you install.**

### The three specifications, each explaining a section you already read

Here is the satisfying part. Each specification retroactively explains something from earlier in this chapter.

- The **Image Specification** (`image-spec`) defines the OCI Image Format, which encompasses the image manifest, filesystem layer serialization, and image configuration needed to launch applications on target platforms [source: oci-overview-2026-08-23]. That is §2's layers. The stack-with-a-shared-base is not a convention that happens to be widely followed; it is a published format.

- The **Distribution Specification** (`distribution-spec`) reached v1.0 in May 2020 and was introduced to standardize the API to distribute container images [source: oci-overview-2026-08-23]. That is §3's registries. The reason any registry can serve an image built by any tool is that the transfer protocol is specified.

- The **Runtime Specification** (`runtime-spec`) outlines how to run a "filesystem bundle" that is unpacked on disk [source: oci-overview-2026-08-23]. That is §4's bottom hop. runC's job description is a document.

And the flow that connects them, in three beats: at a high level, an OCI implementation would download an OCI Image, then unpack that image into an OCI Runtime **filesystem bundle**; at that point the bundle would be run by an OCI Runtime [source: oci-overview-2026-08-23].

<!-- FIGURE: ch02-fig03-oci-three-specs -->
```
  ┌── image-spec ────┐  ┌── distribution-spec ─┐  ┌── runtime-spec ───┐
  │ the FORMAT of    │  │ the API for MOVING   │  │ how to RUN a      │
  │ the artifact     │  │ it over the wire     │  │ filesystem bundle │
  └────────┬─────────┘  └──────────┬───────────┘  └─────────┬─────────┘
           │                       │                        │
           ▼                       ▼                        ▼
   ┌──────────────┐         ┌────────────┐        ┌──────────────────┐
   │  OCI Image   │ ──pull─►│   unpack   │ ──────►│ filesystem bundle│──► run
   └──────────────┘         └────────────┘        └──────────────────┘
```

**Figure 2-4.** Specifications on top, artifact lifecycle underneath, one column each. What to notice: nothing in this figure is Kubernetes. Compare it against Figure 2-3 — those are two different planes, and the next callout is about exactly that.

> 🪢 **Mnemonic:** **Build it, ship it, run it** — `image-spec`, `distribution-spec`, `runtime-spec`. Three specs, in the order the flow uses them.

> ⚠ **Navigational Hazards**
>
> **CRI and OCI are different layers, and conflating them is the hardest discrimination in this chapter.**
>
> **CRI** is how *Kubernetes* talks to a container runtime. It exists because Kubernetes wanted to support alternative runtimes [source: k8s-docs-extending-kubernetes-2026-08-23]. Its two endpoints are the kubelet and a runtime. It is a Kubernetes concern; a container system that has never heard of Kubernetes has no use for it.
>
> **OCI** is how *images* are formatted and distributed, and how *bundles* are executed [source: oci-overview-2026-08-23]. Its endpoints are build tools, registries, and runtimes. It is an industry concern; it would exist, unchanged, in a world where Kubernetes was never written.
>
> Two three-letter abbreviations. Both involve the word "runtime." Both sit underneath your Pod. They are easy to confuse — and the confusion is not carelessness, since a single component like containerd genuinely participates in both (it implements the CRI *and* handles OCI images). The discipline is to ask which *direction* you're looking: up toward Kubernetes, that's CRI; sideways toward the rest of the industry, that's OCI. Lay Figure 2-3 and Figure 2-4 side by side; the planes are drawn in the same grammar precisely so you can see that they are different planes.

> 🔭 **Closer Look:** Notice the dates. Two of the three specifications were part of the effort from its 2015 founding; the distribution specification did not reach v1.0 until May 2020 [source: oci-overview-2026-08-23]. Five years is a long gap in a fast-moving field, and it tells you something about which problems felt urgent: the industry standardized *what an image is* and *what it means to run one* first, and formalized *how it moves* considerably later. This is depth beyond what the exam asks. What the exam may well ask is which specification governs the registry API — and the answer is the one that arrived last.

runC closes the loop: Docker donated its container runtime, runC, to the OCI to serve as the cornerstone of this new effort [source: oci-overview-2026-08-23]. The company that popularized containers gave away the piece that runs them. That is what an open governance structure is *for*, and it is the same institutional instinct you will meet again when the book turns to how CNCF itself is governed *[cross-bearing: see Ch 17 §2 — CNCF governance and project maturity]*.

---

## ☆ Taking Your Bearings #2: Who Runs It, and Who Standardized It

Four questions on §4 and §5. At least one of them requires holding both sections at once.

**1.** Which component in a standard Kubernetes cluster actually creates and starts a container?

A) The kube-apiserver, via the control plane
B) The kubelet, directly
C) A CRI-conformant container runtime such as containerd or CRI-O
D) The kube-scheduler, at bind time

**2.** What is the Open Container Initiative?

A) A container runtime maintained by the Linux Foundation
B) An open governance structure that publishes specifications for container formats and runtimes
C) A company formed by Docker in 2015 to commercialize container tooling
D) A CNCF graduated project providing a registry implementation

**3.** A colleague describes a component as "the thing that defines how an unpacked filesystem bundle on disk gets executed." Which governs that, and what is the artifact called?

A) The CRI; the artifact is a container image
B) The CRI; the artifact is a filesystem bundle
C) The OCI runtime specification; the artifact is a filesystem bundle
D) The OCI image specification; the artifact is an image manifest

**4.** Match the concern to the specification that standardizes it: (i) the layout of image layers and the manifest, (ii) the API a node uses to fetch an image from a registry, (iii) executing an unpacked bundle.

A) i = runtime-spec, ii = image-spec, iii = distribution-spec
B) i = image-spec, ii = distribution-spec, iii = runtime-spec
C) i = distribution-spec, ii = runtime-spec, iii = image-spec
D) i = image-spec, ii = runtime-spec, iii = distribution-spec

---

**Answers with Explanations**

**1 — C.** The container runtime is responsible for managing the execution and lifecycle of containers, and Kubernetes supports containerd, CRI-O, and any other implementation of the CRI [source: k8s-docs-containers-2026-08-23].
- **A is wrong.** The API server exposes the Kubernetes HTTP API [source: k8s-docs-components-2026-08-23]; it is nowhere near a container process.
- **B is wrong**, and it is the most tempting distractor. The kubelet *ensures* that the containers described in PodSpecs are running and healthy [source: k8s-docs-cluster-architecture-2026-08-23] — it is the component that wants them to exist, not the one that creates them. It reaches a runtime across the CRI to do that.
- **D is wrong.** The scheduler assigns Pods to nodes [source: k8s-docs-components-2026-08-23] and then its work is finished.

**2 — B.** The OCI is an open governance structure for the express purpose of creating open industry standards around container formats and runtimes, established in June 2015 [source: oci-overview-2026-08-23].
- **A is wrong** — this is the most common misconception about the OCI. It publishes specifications; it does not ship a runtime. runC was *donated to* it [source: oci-overview-2026-08-23], which is a different relationship.
- **C is wrong.** Docker was a founding participant, along with other container-industry leaders, but the OCI is a governance structure rather than a company, and "commercialize" inverts its purpose.
- **D is wrong.** It is not a CNCF project and does not provide a registry; it specifies the *API* that registries implement.

**3 — C.** The runtime specification outlines how to run a filesystem bundle that is unpacked on disk [source: oci-overview-2026-08-23]. The term "filesystem bundle" is the specification's own.
- **A is wrong** on both counts: wrong governing body and wrong artifact (an image is what gets *unpacked into* a bundle).
- **B is wrong** on the governing body. This is the OCI/CRI conflation the ⚠ callout in §5 exists for — the artifact is right, the layer is not. The CRI governs how Kubernetes talks to a runtime, not how a bundle executes.
- **D is wrong.** The image specification defines the format of the image — manifest, layer serialization, configuration [source: oci-overview-2026-08-23] — not its execution.

**4 — B.** The image specification encompasses the image manifest, filesystem layer serialization, and image configuration; the distribution specification standardizes the API to distribute container images; the runtime specification outlines how to run a filesystem bundle [source: oci-overview-2026-08-23].
- **A, C, and D** each rotate at least one pairing. The check that catches all three: the specifications map onto the lifecycle in order — the image exists, then it moves, then it runs.

---

**Checkpoint: You've Now Mastered**
✓ The full path from a Pod's image field to a running process, and which component owns each hop
✓ That Kubernetes defines the CRI and implements nothing below it
✓ The OCI as a governance body with three specifications, and which artifact each one governs
✓ The CRI/OCI boundary — the discrimination that Chapter 17 will lean on

Two sections left, and both are about behavior rather than structure: when Kubernetes goes looking for an image, and how strong the walls around a container are.

---

## §6 — 🟡 When Kubernetes Pulls, and When It Doesn't

This is the fiddliest material in the chapter and the highest-value-per-minute. The rules are small, entirely conditional, and almost nobody guesses the defaults correctly.

> **Dead Reckoning:** Three pull policies. **IfNotPresent** — the image is pulled only if it is not already present locally. **Always** — every time the kubelet launches a container, it queries the container image registry to resolve the name to an image digest; if the kubelet has a container image with that exact digest cached locally, it uses its cached image, otherwise it pulls the image with the resolved digest. **Never** — the kubelet does not try fetching the image; if the image is somehow already present locally, the kubelet attempts to start the container, otherwise startup fails.
>
> Four defaults, applied when `imagePullPolicy` is omitted. With a **digest**: IfNotPresent. With the tag **`:latest`**: Always. With **no tag** specified: Always. With a tag **other than `:latest`**: IfNotPresent.
>
> Once a Pod is created, `imagePullPolicy` is not updated if the image's tag or digest changes later.
>
> When the kubelet cannot pull an image, the container sits in **`ImagePullBackOff`** — meaning the container could not start because Kubernetes could not pull the image, for reasons such as an invalid image name or pulling from a private registry without credentials. The **BackOff** part indicates that Kubernetes will keep trying, with an increasing back-off delay, up to a compiled-in limit of 300 seconds (5 minutes). [source: k8s-docs-images-2026-08-23]

That block is the whole exam surface for this section, stated flat. Now the two things worth saying about it.

<!-- FIGURE: ch02-fig05-imagepullpolicy-decision -->
```
                    was imagePullPolicy set explicitly?
                          │                    │
                         YES                   NO
                          │                    │
        ┌─────────────────┴───────┐            │
        │ Always                  │      reference form?
        │  → resolve to digest;   │            │
        │    reuse cache if match │   ┌────────┼────────┬──────────┐
        │ IfNotPresent            │   │        │        │          │
        │  → pull only if absent  │ @digest :latest   no tag    :other
        │ Never                   │   │        │        │          │
        │  → never fetch; fail if │   ▼        ▼        ▼          ▼
        │    absent               │ IfNot-  Always   Always    IfNot-
        └─────────────────────────┘ Present                    Present
```

**Figure 2-5.** What to notice, and it isn't the branches: the right-hand side of this tree is reached by *not making a decision*. The reference form you chose for identity reasons quietly chose your pull behavior too.

That is the second half of §3's `:latest` hazard, now complete *[cross-bearing: see Ch 2 §3 — the `:latest` naming caution]*. Writing `:latest` is not merely untidy. It flips the default from IfNotPresent to Always, which means the kubelet consults the registry on every container launch — so the tag that made you unsure which version is running is also the tag that maximizes the number of opportunities for the answer to change. Two problems, one field, and the documentation warns about only the first.

The `Always` behavior also deserves a careful reading, because its name oversells it. `Always` does not mean "always download." It means always *check*: resolve the name to a digest at the registry, and if the local cache already holds that exact digest, use the cached copy [source: k8s-docs-images-2026-08-23]. Always re-resolve; download only on a miss. This is a favorite distractor, and now you know why the distractor is wrong.

> 🪝 **Snag:** Once a Pod is created, `imagePullPolicy` is not updated if the image's tag or digest changes later [source: k8s-docs-images-2026-08-23]. The policy was resolved when the Pod was created, and moving the tag afterwards does not retroactively change how that existing Pod behaves. If you need new behavior, you need a new Pod — which is §2's immutability principle showing up in an unexpected place.

One name to bank and not chase. `ImagePullBackOff` is reported as a container in the **Waiting** state [source: k8s-docs-images-2026-08-23], and container states are Chapter 5's material *[cross-bearing: see Ch 5 §5 — Pod phases and container states]*. Diagnosing a stuck pull — reading the events, checking whether the image name is right and whether it was actually pushed [source: k8s-docs-debug-pods-2026-08-23] — is Chapter 13's *[cross-bearing: see Ch 13 §2 — diagnosing ImagePullBackOff]*. What Chapter 2 owes you is the name, the cause, and the retry behavior. You have all three.

---

## §7 — 🟡 Not All Isolation Is Equal: RuntimeClass

Readers skip this section. The exam does not.

§1 established that a container shares the host operating system, and the ⚓ callout there insisted that this was a *tradeoff* rather than a deficiency. Tradeoffs can be renegotiated. This is the renegotiation.

**RuntimeClass is a feature for selecting the container runtime configuration** used to run a Pod's containers [source: k8s-docs-runtime-class-2026-08-23].

Take the motivation before the mechanism, because the mechanism without the motivation is unmemorable trivia.

You can set a different RuntimeClass between different Pods to provide a balance of performance versus security. For example, if part of your workload deserves a high level of information-security assurance, you might choose to schedule those Pods so that they run in a container runtime that uses **hardware virtualization** (such as Kata Containers) or a **user-space kernel** (such as gVisor). You'd then benefit from the extra isolation of the alternative runtime, at the expense of some additional overhead. You can also use RuntimeClass to run different Pods with the same container runtime but with different settings [source: k8s-docs-runtime-class-2026-08-23].

Read what that makes possible. Two workloads, same cluster, same API, same manifests-shaped-the-same-way — and different isolation floors. The workload handling untrusted user-submitted code gets hardware virtualization. The internal batch job that nobody worries about gets the default, and doesn't pay for a boundary it doesn't need. This is the answer to a question that sounds unanswerable: "containers are less isolated than VMs, so how can I run genuinely untrusted code?" You change the floor for that workload.

> ⚓ **Worth Securing:** **"Container" names an interface, not an isolation level.** That sentence is what makes this section stick. Everything you learned in §1 through §6 — the image format, the pull behavior, the CRI socket — is unchanged whether the thing on the other end of the socket shares the host kernel directly, interposes a user-space kernel, or boots a lightweight virtual machine. The contract is stable; the strength of the walls is a parameter.

The mechanism, at the depth the exam reaches. Configure the CRI implementation on your nodes — each configuration has a corresponding **handler** name. Create the corresponding RuntimeClass resources (`apiVersion: node.k8s.io/v1`, `kind: RuntimeClass`, with a `handler` field). Once RuntimeClasses are configured for the cluster, specify a `runtimeClassName` in the Pod spec to use one; **if no `runtimeClassName` is specified, the default runtime handler is used** [source: k8s-docs-runtime-class-2026-08-23].

Two levels of indirection, which is the part worth holding: the Pod names a RuntimeClass, and the RuntimeClass names a handler that was configured on the nodes. The Pod author does not name a runtime. They name a *class of runtime configuration* that a cluster administrator has already established — which is why this works as a self-service mechanism rather than as a way for application teams to request arbitrary runtimes.

A RuntimeClass can also carry scheduling constraints (`nodeSelector`, `tolerations`) so that Pods land on nodes which actually support the handler, and a **Pod overhead** so the scheduler accounts for the runtime's resource cost [source: k8s-docs-runtime-class-2026-08-23]. Both of those are scheduling concepts, and scheduling has its own chapter *[cross-bearing: see Ch 7 §3 — node selection, tolerations, and accounting for overhead]*. Register that they exist; the reasoning behind them arrives later.

> 🔭 **Closer Look:** Kata Containers and gVisor are two genuinely different answers to the same question. Kata uses **hardware virtualization** — it puts a real virtualization boundary underneath the workload, which is roughly borrowing back the isolation model §1 traded away. gVisor uses a **user-space kernel** — it intercepts the workload's system calls and services them in a kernel implementation running as an ordinary process, so the host kernel is never the workload's direct interlocutor [source: k8s-docs-runtime-class-2026-08-23]. Different techniques, same goal, different overheads. This is depth: the exam is far more likely to ask *why RuntimeClass exists* than to ask which sandbox uses which technique. Know the motivation cold; know this as a bonus.

The security guidance is consistent with all of it: to protect compute at runtime, use a container runtime that provides security restrictions [source: k8s-docs-cloud-native-security-2026-08-23]. RuntimeClass is the Kubernetes-shaped way to say *which* one, per workload. Sandboxed runtimes come back as one control among several in the security lifecycle *[cross-bearing: see Ch 12 §4 — runtime protection for compute]*.

---

## ☆ Taking Your Bearings #3: Pull Behavior and Runtime Selection

Four questions on §6 and §7.

**1.** A Pod specifies `image: internal.registry.example/api-gateway` and does not set `imagePullPolicy`. What pull policy applies?

A) IfNotPresent, because a registry hostname was given explicitly
B) Always, because no tag was specified
C) IfNotPresent, because that is the global default
D) Never, because the image is from a private registry

**2.** A Pod's `imagePullPolicy` is set to `Always`. Which statement describes what happens each time the kubelet launches the container?

A) The image is downloaded from the registry every time, unconditionally
B) The kubelet queries the registry to resolve the name to a digest, and reuses its cached image if it already holds that exact digest
C) The kubelet checks whether the local image is older than the registry's copy by timestamp
D) The kubelet pulls only if the tag has changed since the last launch

**3.** A container reports `ImagePullBackOff`. Which of the following is the correct reading of that status?

A) The image was pulled but failed its integrity check, and Kubernetes has given up
B) The container could not start because the image could not be pulled, and Kubernetes will keep retrying with increasing delay up to 300 seconds
C) The image pull succeeded but the container crashed on start-up, and the kubelet is backing off before restarting it
D) The node has insufficient disk space, so the pull has been deferred indefinitely

**4.** A platform team must run customer-submitted code on the same cluster as internal services, and the customer workloads require a stronger isolation boundary than the internal ones. Which instrument fits, and why?

A) A separate cluster, because isolation strength is a cluster-level property
B) RuntimeClass, to run the customer Pods on a runtime using hardware virtualization or a user-space kernel, at the cost of extra overhead
C) RuntimeClass, applied cluster-wide so that all workloads get the strongest available runtime
D) `imagePullPolicy: Never` for customer workloads, to prevent them from fetching arbitrary images

---

**Answers with Explanations**

**1 — B.** If no tag is specified, the default `imagePullPolicy` is Always [source: k8s-docs-images-2026-08-23]. The reference names a registry and an image but no tag, so the no-tag case applies.
- **A is wrong.** The registry hostname has no bearing on pull policy; the *tag form* determines the default.
- **C is wrong.** There is no single global default — there are four conditional defaults, and IfNotPresent is only two of them (digest, and any tag other than `:latest`) [source: k8s-docs-images-2026-08-23].
- **D is wrong.** `Never` is only ever a policy you set explicitly; it is never a default, and privacy of the registry is unrelated.

**2 — B.** With `Always`, the kubelet queries the registry to resolve the name to a digest, and if it already has an image with that exact digest cached locally, it uses the cached image; otherwise it pulls [source: k8s-docs-images-2026-08-23].
- **A is wrong**, and it is the distractor the policy's name invites. `Always` means always *check*, not always *download*.
- **C is wrong.** The resolution is by digest, not by timestamp comparison.
- **D is wrong.** The kubelet does not track tag changes between launches; it re-resolves the reference each time.

**3 — B.** `ImagePullBackOff` means a container could not start because Kubernetes could not pull the image — invalid image name, or a private registry without credentials, for instance — and the BackOff indicates continued retries with increasing delay up to a compiled-in limit of 300 seconds [source: k8s-docs-images-2026-08-23].
- **A is wrong** twice: the pull did not succeed, and Kubernetes has not given up — retrying is what BackOff describes.
- **C is wrong.** That describes a different failure mode entirely; here the image never arrived.
- **D is wrong.** Disk pressure is a distinct node condition and is not what this status reports.

**4 — B.** RuntimeClass exists precisely to provide a balance of performance versus security: a workload deserving high information-security assurance can be scheduled onto a runtime using hardware virtualization (Kata Containers) or a user-space kernel (gVisor), benefiting from extra isolation at the expense of additional overhead [source: k8s-docs-runtime-class-2026-08-23].
- **A is wrong.** Isolation strength is selectable per Pod via `runtimeClassName`, which is the entire point of the feature. A separate cluster may be defensible for other reasons, but not because isolation is cluster-fixed.
- **C is wrong**, and it misses that the tradeoff runs both ways. The stronger runtime costs overhead; applying it to everything makes every workload pay for a boundary most of them don't need. Selectivity is the feature.
- **D is wrong.** `imagePullPolicy` governs when images are fetched, not how strongly running containers are isolated. Different axis entirely.

---

**Checkpoint: You've Now Mastered**
✓ The three pull policies and, more importantly, the four conditional defaults
✓ Why `Always` does not mean "always download"
✓ `ImagePullBackOff` — what it reports and what BackOff implies
✓ RuntimeClass, and the fact that isolation strength is a per-workload decision

Everything in this chapter is now on the table. One short section to see why it all has the shape it has.

---

## §8 — 🔵 The Crate, Not the Cargo

The subtitle comes due.

The intermodal shipping container did not win because it was a better box. Wooden crates were fine boxes. It won because the industry standardized the **interface** — the dimensions, the corner fittings, the lifting points — and once that interface was published, a crane could be designed once, a truck chassis could be designed once, a rail flatcar and a ship's hold could each be designed once, and every one of them could then handle anything. The cargo stopped mattering. Nobody at the crane has an opinion about what is inside.

☀️ **Zenith**

You have spent this chapter looking at that same move from five angles without necessarily seeing that it was one move.

The OCI standardized the image format, so any build tool can produce an artifact any runtime can unpack. It standardized the distribution API, so any registry can serve any image. It standardized bundle execution, so any conformant runtime can run one [source: oci-overview-2026-08-23]. And Kubernetes, for its part, standardized nothing about containers at all — it published an *interface*, the CRI, and let the ecosystem supply the implementations [source: k8s-docs-extending-kubernetes-2026-08-23].

Which is why Kubernetes never needed to know what is in the crate. It doesn't know what language your application is written in, what its dependencies are, which build tool produced it, or which of two mature runtimes will start it on any given node. It knows the shape of the fitting. That is the entire reason a system this large can be this indifferent to the workloads it runs — and the reason the answer to "can Kubernetes run *my* thing?" has been "if it runs in a container, yes" for a decade [source: k8s-docs-overview-2026-08-23].

<!-- FIGURE: ch02-zenith-standard-crate -->
**Figure 2-6 (Zenith illustration — to be commissioned).** Identical crates moving between incompatible carriers, each carrier built once against a published specification, the contents never inspected and never mattering. Rendered from the Communications Officer's vantage; narrator not depicted. The synthesis must read as being *about interfaces* — a reader who sees only an attractive freight scene has received a decorative illustration. Minimal labels by design; two or three at most. Register check against `illustrator-brief.md` required before commissioning: the crate motif must work in this book's era placement rather than defaulting to a 20th-century dockside.

> **Extended Analogy:**
>
> Consider what the world looks like before the standard, because that is the part usually skipped. A ship arrives. In the hold are barrels, sacks, crates of a dozen different sizes, machinery in wooden frames, loose timber. Every item is handled individually, by hand, and every item is handled *differently*, because there is no general procedure for a thing whose shape you cannot predict. Unloading takes days. Most of the ship's economic life is spent stationary, being emptied.
>
> Now consider what changed. Not the ship — ships were fine. Not the cargo — the cargo was always the point. What changed is that somebody wrote down the dimensions of a box and the geometry of the fittings at its corners, and enough of the industry agreed to it that building machinery against the specification became rational. A crane that can lift one standard container can lift every standard container that will ever exist, including ones holding goods that had not been invented when the crane was built. The crane's designer never had to think about the cargo. That is not a convenience; it is the whole gain, and it is *larger* than any improvement to the crane.
>
> Now read this chapter again in that light. An image is the crate: a published format with a manifest describing its contents, produced by any of a dozen build tools. A registry is the terminal: it moves crates according to a published API, without opening them. A CRI runtime is the crane: built once against an interface, able to handle any conformant crate, swappable for a different crane without redesigning the port. And Kubernetes is the port authority — coordinating, scheduling, deciding what goes where, and never once lifting anything itself.
>
> The failure mode of the pre-standard world is also worth keeping. It was not that ships were slow. It was that every combination of cargo and carrier was a bespoke problem, so effort spent solving one combination taught you nothing about the next. That is exactly the failure mode that a platform without published interfaces has, and it is exactly why the next four chapters keep finding the same design decision underneath different subjects.

And that is the plant. This is the **first** of four times you will see this move. Storage does it. Networking does it. The API itself does it. When those three have all landed, the book collects them, and the collecting is meant to feel like recognition rather than a fourth list *[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*.

---

## Exam Alert 🚨

**High-Priority Topics**

1. **Tag versus digest.** A tag identifies a series and can be moved. A digest is a hash of the image's content and is immutable [source: k8s-docs-images-2026-08-23]. Every claim anyone makes about reproducible deployment rests on this distinction.

2. **The kubelet → CRI → containerd/CRI-O → runC chain.** Kubernetes defines the interface and implements nothing below it [source: k8s-docs-containers-2026-08-23] [source: k8s-docs-extending-kubernetes-2026-08-23]. This is the most reused idea in the chapter.

3. **OCI's three specifications, and that the OCI is a governance body rather than software.** `image-spec` (format), `distribution-spec` (the registry API, v1.0 May 2020), `runtime-spec` (running a filesystem bundle) [source: oci-overview-2026-08-23].

4. **`imagePullPolicy` defaults.** IfNotPresent with a digest; Always with `:latest`; Always with no tag; IfNotPresent with any other tag [source: k8s-docs-images-2026-08-23]. Four cases, and the exam will give you a reference and ask for the behavior.

**Common Traps**

| Trap | Where this chapter defuses it |
|---|---|
| "A container image includes the OS kernel" | §2 — derived from §1's sharing model; Bearings #1 Q1 and Q2 |
| "You patch a running container" | §2 immutability — the correct process is build a new image, then recreate [source: k8s-docs-containers-2026-08-23] |
| "OCI is a runtime" | §5 ★ Fixed Point — it is a governance structure publishing three specifications |
| Conflating OCI with CRI | §5 ⚠ Navigational Hazards. These are easy to confuse: two three-letter abbreviations, both mentioning "runtime," both below your Pod. Ask which direction you're looking |
| "Docker is the container runtime Kubernetes uses" | §4 🪝 Snag. Also easy to confuse, for historical reasons — "Docker" names four things, and the supported set is defined by CRI conformance [source: k8s-docs-containers-2026-08-23] |
| "`:latest` is just a naming-hygiene issue" | §3 ⚠ plus §6 — the tag also sets the default pull policy [source: k8s-docs-images-2026-08-23] |
| "`Always` re-downloads the image every launch" | §6 Dead Reckoning — it re-resolves to a digest and reuses a matching cached image [source: k8s-docs-images-2026-08-23] |
| "Container isolation strength is fixed" | §7 — RuntimeClass selects it per Pod [source: k8s-docs-runtime-class-2026-08-23] |

Two of these traps — the OCI/CRI conflation and the Docker-as-runtime shorthand — are flagged here because they are conceptually slippery, not because this book has data on how often they appear. The book does not make frequency claims it cannot support.

---

## Practice Questions

Twenty-five questions. Six or more require combining two sections; those are marked. Explanations cover every option.

**1.** Which single architectural difference accounts for containers starting faster than virtual machines?

A) Containers use a more efficient filesystem format
B) Containers share the host operating system rather than booting their own
C) Containers are always smaller than virtual machine images
D) Containers skip hardware initialization by using paravirtualized drivers

> **B.** Containers have relaxed isolation properties in order to share the OS among the applications, and are therefore lightweight [source: k8s-docs-overview-2026-08-23]. A VM is a full machine running all components including its own OS on top of virtualized hardware [source: k8s-docs-overview-2026-08-23] — and booting an OS is what takes the time.
> **A** is wrong: filesystem format is not the mechanism, and containers have their own filesystem in both models. **C** is a consequence of B, not a cause, and stating it as the cause is the error the chapter's derivation exercise is designed to prevent. **D** is wrong: paravirtualized drivers are a virtualization technique and have nothing to do with why containers start quickly.

**2.** Which of these does a container have its own of?

A) Kernel
B) Hypervisor
C) Filesystem
D) Hardware

> **C.** Similar to a VM, a container has its own filesystem, share of CPU, memory, process space, and more [source: k8s-docs-overview-2026-08-23].
> **A** is wrong — the kernel is the shared thing; that sharing is the definition. **B** is wrong: a hypervisor belongs to the virtualization model, and no per-container hypervisor exists in the container model. **D** is wrong: hardware is the host's, in both models.

**3.** A workload is described as needing to be "portable across clouds and OS distributions." Which property of containers delivers that?

A) They are decoupled from the underlying infrastructure
B) They are scheduled by Kubernetes
C) They use a shared kernel
D) They can be restarted automatically

> **A.** Because containers are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions [source: k8s-docs-overview-2026-08-23]; the standardization from having dependencies included is what produces the same behavior wherever you run it [source: k8s-docs-containers-2026-08-23].
> **B** is wrong: portability is a property of containers themselves and holds without an orchestrator. **C** is a true statement about containers but the wrong causal link — kernel sharing produces lightness, not portability; in fact it is the *constraint* on portability across kernel families. **D** describes something an orchestrator provides [source: k8s-docs-overview-2026-08-23], not a source of portability.

**4.** Which is included in a container image?

A) Default values for essential settings
B) The cluster's kubeconfig
C) The node's kernel modules
D) The Pod specification that will run it

> **A.** An image is a ready-to-run package containing the code and any runtime it requires, application and system libraries, and default values for any essential settings [source: k8s-docs-containers-2026-08-23].
> **B** is wrong: kubeconfig is a client credential file used to reach a cluster's API [source: k8s-docs-kubectl-overview-2026-08-23], unrelated to image contents. **C** is wrong — no kernel, and therefore no kernel modules. **D** is wrong and inverts the relationship: a Pod spec *references* an image.

**5.** An application inside a running container needs a configuration change that must survive the container being replaced. What is the correct process?

A) Edit the file in the running container and take a snapshot
B) Build a new image that includes the change, then recreate the container from the updated image
C) Edit the file in the running container; changes persist by default
D) Mount the file from the host so the container never has to change

> **B.** Containers are intended to be stateless and immutable; if you want to make changes, the correct process is to build a new image that includes the change, then recreate the container to start from the updated image [source: k8s-docs-containers-2026-08-23].
> **A** is wrong — "edit then snapshot" produces an artifact whose provenance nobody can reproduce, forfeiting the repeatability that is the reason to use containers at all [source: k8s-docs-containers-2026-08-23]. **C** is wrong: the documentation says explicitly you should not change the code of a running container. **D** is a real technique for some problems but not the answer to "the application needs a different configuration baked in," and it trades away portability by binding the container to a particular host's contents.

**6.** Two images are built from the same base. What follows about storage and transfer?

A) The base is duplicated once per image
B) The base is a shared layer, named by both images' manifests
C) The images must be merged into one before they can share anything
D) Sharing only occurs if both images live in the same registry namespace

> **B.** An image is assembled from filesystem layers described by a manifest [source: oci-overview-2026-08-23]; two images built on the same base name the same base layer.
> **A** is wrong and is the intuition the chapter's Soundings Q4 pre-tests. **C** is wrong: layer sharing requires no merging; it is a property of how manifests reference layers. **D** is wrong: sharing is a function of layer identity, not naming conventions.
>
> <!-- AUTHOR-REVIEW: this item's correct answer relies on the layer-sharing consequence described qualitatively in §2. The cached sources establish that images consist of serialized filesystem layers named by a manifest [oci-overview] but do not describe deduplicated storage behavior directly. If G29's open half is not closed, consider reframing this item to test manifest structure rather than storage outcome. -->

**7.** Cloud Native Buildpacks: what does the **detect** phase do?

A) Scans the produced image for known vulnerabilities
B) Determines which buildpacks apply to the source code
C) Detects whether the target registry supports the distribution specification
D) Identifies the host kernel version to select a compatible base image

> **B.** The lifecycle runs in phases — detect (determine which buildpacks apply), build (compile and assemble the application), export (create the final OCI image with reproducible layers) [source: buildpacks-concepts-2026-08-23].
> **A** is vulnerability scanning, a supply-chain concern handled by other tools entirely [source: k8s-docs-cloud-native-security-2026-08-23]. **C** is invented; no lifecycle phase probes registry capabilities. **D** is wrong: no phase selects a base image by host kernel — the base images are part of the builder's configured stack.

**8.** In the Buildpacks model, what is a **builder**?

A) A CI system that runs the lifecycle
B) An OCI image containing an ordered combination of buildpacks and a build-time base image, a lifecycle binary, and a reference to a runtime base image
C) The final application image produced by the export phase
D) The pairing of a build image and a run image

> **B.** That is the definition verbatim in substance [source: buildpacks-concepts-2026-08-23].
> **A** describes the *platform*, which orchestrates by invoking the lifecycle [source: buildpacks-concepts-2026-08-23]. **C** describes the export phase's output, not the builder. **D** describes the *stack* — the build-image/run-image pairing [source: buildpacks-concepts-2026-08-23].

**9. [integrative: §2 + §5]** The layer structure of an image — manifest, serialized filesystem layers, configuration — is standardized by which specification?

A) The OCI runtime specification
B) The OCI image specification
C) The Container Runtime Interface
D) The OCI distribution specification

> **B.** The Image Specification defines the OCI Image Format, encompassing the image manifest, filesystem layer serialization, and image configuration needed to launch applications on target platforms [source: oci-overview-2026-08-23].
> **A** governs running an unpacked filesystem bundle, not the format of the artifact you unpack. **C** is a Kubernetes-to-runtime interface [source: k8s-docs-extending-kubernetes-2026-08-23] and standardizes nothing about image internals — this is the OCI/CRI conflation. **D** standardizes the API for distributing images, not their internal layout.

**10.** What does the reference `busybox` resolve to?

A) `busybox:latest` on whichever registry the node is configured to prefer
B) `docker.io/library/busybox:latest`
C) `docker.io/busybox:latest`
D) `registry.k8s.io/library/busybox:latest`

> **B.** The documentation gives this exact equivalence: `busybox` is equivalent to `docker.io/library/busybox:latest` [source: k8s-docs-images-2026-08-23].
> **A** is wrong: the assumed registry is specific, not a node preference. **C** drops the `library` namespace present in the documented equivalence. **D** names a different registry, which is not the assumed default.

**11.** Which is immutable?

A) A tag
B) A digest
C) Both
D) Neither

> **B.** Digests are a unique identifier for a specific version of an image — a hash of the image's content — and are immutable; tags can be moved to point to different images [source: k8s-docs-images-2026-08-23].
> **A** inverts it, which is the misconception this chapter's Fixed Point targets. **C** would make version pinning by tag safe, which is precisely what the documentation cautions against. **D** is wrong: a content hash cannot be re-pointed without changing the content.

**12.** Why does the documentation advise against `:latest` in production?

A) It is harder to know which version is running, and harder to roll back properly
B) `:latest` images are excluded from registry caching
C) `:latest` is reserved for the Kubernetes project's own images
D) `:latest` cannot be used with private registries

> **A.** You should avoid using the `:latest` tag when deploying containers in production as it is harder to track which version of the image is running and more difficult to roll back properly; specify a meaningful tag such as `v1.42.0` and/or a digest instead [source: k8s-docs-images-2026-08-23].
> **B** is invented; caching behavior is governed by pull policy, not by the tag's name. **C** is invented. **D** is invented — nothing about `:latest` interacts with registry privacy.

**13.** Which is a documented way to supply credentials for a private registry?

A) Embedding credentials in the image
B) Specifying `imagePullSecrets` on a Pod, referencing a Secret of type `kubernetes.io/dockerconfigjson`
C) Setting `imagePullPolicy: Always`, which prompts an interactive credential request
D) Adding the credentials to the image's tag

> **B.** Credentials can be provided by configuring nodes to authenticate, a kubelet credential provider, pre-pulled images, specifying `imagePullSecrets` on a Pod (a Secret of type `kubernetes.io/dockerconfigjson`), or vendor-specific and local extensions [source: k8s-docs-images-2026-08-23].
> **A** is circular: you would need the credentials to pull the image containing the credentials. **C** is invented — there is no interactive credential flow, and pull policy governs *when* to fetch, not *how* to authenticate. **D** is invented; tags are version labels [source: k8s-docs-images-2026-08-23].

**14. [integrative: §3 + §5]** A registry serves images to nodes over a standardized API. Which specification standardizes that API, and when did it reach v1.0?

A) `image-spec`, June 2015
B) `distribution-spec`, May 2020
C) `runtime-spec`, June 2015
D) The CRI, May 2020

> **B.** The Distribution Specification reached v1.0 in May 2020 and was introduced to OCI as an effort to standardize the API to distribute container images [source: oci-overview-2026-08-23].
> **A** names the wrong specification; June 2015 is the OCI's founding, not a specification's v1.0. **C** names the specification governing bundle execution. **D** conflates a Kubernetes interface with an OCI specification and attaches a date that belongs to the latter.

**15.** Which component is responsible for managing the execution and lifecycle of containers on a node?

A) The kubelet
B) kube-proxy
C) The container runtime
D) The kube-controller-manager

> **C.** The container runtime is responsible for managing the execution and lifecycle of containers within the Kubernetes environment [source: k8s-docs-containers-2026-08-23] [source: k8s-docs-cluster-architecture-2026-08-23].
> **A** is the closest wrong answer: the kubelet ensures that containers described in PodSpecs are running and healthy [source: k8s-docs-cluster-architecture-2026-08-23] — it drives, it does not execute. **B** maintains network rules on nodes to implement Services [source: k8s-docs-components-2026-08-23]. **D** runs controller processes in the control plane [source: k8s-docs-components-2026-08-23], not on the node's container path.

**16.** What is the CRI?

A) A container runtime maintained by the Kubernetes project
B) The interface Kubernetes defines so that alternative container runtimes can be used
C) An OCI specification for container images
D) The protocol nodes use to fetch images from registries

> **B.** Among Kubernetes' infrastructure extension points is the container runtime — "CRI, the Container Runtime Interface, to support alternative container runtimes" [source: k8s-docs-extending-kubernetes-2026-08-23]; Kubernetes supports containerd, CRI-O, and any other implementation of the CRI [source: k8s-docs-containers-2026-08-23].
> **A** is wrong and is the single most consequential misreading: Kubernetes defines the interface and ships no runtime. **C** and **D** are both OCI concerns (`image-spec` and `distribution-spec` respectively) [source: oci-overview-2026-08-23], which is the conflation §5's hazard callout addresses.

**17.** Which two runtimes does the Kubernetes documentation name as supported, and what qualifies any other?

A) Docker and containerd; any runtime with an OCI image
B) containerd and CRI-O; any other implementation of the CRI
C) runC and containerd; any runtime that supports the runtime specification
D) CRI-O and Kata; any runtime installed on the node

> **B.** Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI [source: k8s-docs-containers-2026-08-23]; a container runtime — containerd or CRI-O — must be installed on every node [source: k8s-docs-setup-tooling-2026-08-23].
> **A** names Docker, which is the historical shorthand rather than the documented set, and gets the qualifying condition wrong. **C** names runC, which is an OCI runtime donated to the OCI [source: oci-overview-2026-08-23] rather than one of the two CRI implementations the docs name. **D** names Kata, which is an example of a runtime reachable *through* RuntimeClass [source: k8s-docs-runtime-class-2026-08-23], and its qualifying condition ("installed on the node") omits conformance.

**18.** What was runC's origin?

A) It was written by the Kubernetes project as a reference CRI implementation
B) Docker donated it to the OCI to serve as the cornerstone of the effort
C) It was developed by the Linux Foundation alongside the runtime specification
D) It is the CNCF's graduated low-level runtime, donated by Google

> **B.** Docker donated its container runtime, runC, to the OCI to serve as the cornerstone of this new effort [source: oci-overview-2026-08-23].
> **A** is wrong: runC predates and sits below the CRI, and Kubernetes did not write it. **C** is wrong on origin — the OCI operates under the Linux Foundation [source: oci-overview-2026-08-23] but did not author runC; it received it. **D** is wrong on both donor and framing; the CNCF's graduated container runtimes are containerd and CRI-O [source: cncf-project-maturity-levels-2026-08-23].

**19.** What is the Open Container Initiative, and when was it established?

A) An open governance structure for container standards, established June 2015
B) A CNCF working group, established 2016
C) A Linux Foundation certification program, established May 2020
D) A container runtime project, established June 2015

> **A.** The OCI is an open governance structure for the express purpose of creating open industry standards around container formats and runtimes, established in June 2015 by Docker and other leaders in the container industry [source: oci-overview-2026-08-23].
> **B** is wrong on both body and date; the OCI is not part of the CNCF. **C** attaches the distribution specification's v1.0 date to the founding and misdescribes the body. **D** is the OCI-as-runtime misconception with a correct date attached — which is why the date alone won't save you on this item.

**20. [integrative: §4 + §5]** A colleague says, "containerd conforms to the CRI, so Kubernetes can use it, and it also handles OCI images." Is this coherent?

A) No — a component cannot participate in both the CRI and the OCI
B) Yes — the CRI governs how Kubernetes reaches the runtime; the OCI governs the image format and bundle execution the runtime works with
C) No — the CRI supersedes the OCI specifications for Kubernetes clusters
D) Yes, but only because containerd is a CNCF graduated project

> **B.** The CRI exists to let Kubernetes support alternative runtimes [source: k8s-docs-extending-kubernetes-2026-08-23]; the OCI specifications define the image format, its distribution, and how a filesystem bundle is executed [source: oci-overview-2026-08-23]. Different layers, and a runtime naturally sits at the intersection.
> **A** is wrong and states the conflation as a rule. **C** is wrong: a Kubernetes interface does not supersede industry specifications about artifact formats — they are not competing. **D** reaches a correct conclusion by an irrelevant route; maturity level [source: cncf-project-maturity-levels-2026-08-23] has no bearing on which specifications a component implements.

**21.** A Pod specifies `image: myapp@sha256:1ff6…` and omits `imagePullPolicy`. Which policy applies?

A) Always
B) IfNotPresent
C) Never
D) It is an error to omit the policy when using a digest

> **B.** If you omit `imagePullPolicy` and specify a digest, the default is IfNotPresent [source: k8s-docs-images-2026-08-23].
> **A** is wrong and confuses this case with the `:latest` and no-tag cases. **C** is never a default. **D** is invented — omitting the field is always legal; a default applies.

**22. [integrative: §3 + §6]** A team pins deployments with `:latest` "so we always know we're current." Which pair of consequences follows?

A) The image is easy to identify, and pulls are minimized
B) Version identity is unclear and rollback is harder, and the default pull policy becomes Always
C) The pull policy becomes Never, and the image must be pre-pulled
D) The digest is recomputed on each pull, guaranteeing freshness

> **B.** The documentation warns that `:latest` makes it harder to know which version is running and harder to roll back properly [source: k8s-docs-images-2026-08-23]; separately, the default policy when the tag is `:latest` is Always [source: k8s-docs-images-2026-08-23]. Two effects, one field.
> **A** inverts both halves. **C** describes a policy that is never a default. **D** garbles the mechanism: with Always the kubelet resolves the *name* to a digest at the registry and reuses a matching cached image [source: k8s-docs-images-2026-08-23]; it does not recompute a digest to establish freshness.

**23.** A Pod exists, running from `myapp:v3`. Someone moves the `:v3` tag to a new image. What happens to the existing Pod's pull policy?

A) It is recalculated from the new tag
B) It is unchanged — `imagePullPolicy` is not updated when the image's tag or digest changes later
C) It reverts to the cluster default
D) The Pod is evicted and recreated with the new policy

> **B.** Once a Pod is created, `imagePullPolicy` is not updated if the image's tag or digest changes later [source: k8s-docs-images-2026-08-23].
> **A** is wrong: the resolution happened at creation. **C** is wrong twice — nothing reverts, and there is no single cluster default policy, only four conditional ones. **D** is invented; moving a tag in a registry does not trigger eviction.

**24. [integrative: §1 + §7]** Which statement best characterizes container isolation in Kubernetes?

A) Isolation is fixed by the container model; stronger isolation requires abandoning containers
B) Isolation is relaxed by default to keep containers lightweight, and can be strengthened per Pod by selecting a runtime configuration via RuntimeClass
C) Isolation is configured per node, so all Pods on a node share one isolation level permanently
D) Isolation strength is determined by the image's base layer

> **B.** Containers have relaxed isolation properties in order to share the OS and are therefore lightweight [source: k8s-docs-overview-2026-08-23]; RuntimeClass lets you balance performance against security per Pod, scheduling security-sensitive workloads onto a runtime using hardware virtualization or a user-space kernel at the expense of some overhead [source: k8s-docs-runtime-class-2026-08-23].
> **A** is the belief §7 exists to dislodge. **C** is half-right in a misleading way: handlers *are* configured on nodes, but a Pod selects among them with `runtimeClassName`, and a RuntimeClass can carry scheduling constraints so Pods land on supporting nodes [source: k8s-docs-runtime-class-2026-08-23]. **D** is wrong: the base image supplies userspace contents, not isolation boundaries.

**25.** A Pod omits `runtimeClassName`. What runs it?

A) The Pod is rejected until a RuntimeClass is specified
B) The default runtime handler
C) The most secure available handler, as a safe default
D) A randomly selected configured handler

> **B.** If no `runtimeClassName` is specified, the default RuntimeHandler is used [source: k8s-docs-runtime-class-2026-08-23]; ordinarily you can allow your cluster to pick the default container runtime for a Pod [source: k8s-docs-containers-2026-08-23].
> **A** is wrong — specifying a RuntimeClass is optional, which is why most practitioners never think about runtimes. **C** is wrong and inverts the tradeoff: the stronger runtime costs overhead, so defaulting to it would make every workload pay for a boundary most don't need. **D** is invented; there is nothing random about handler selection.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| Container | Repeatable because dependencies travel with it; shares the host OS, which is why it's lightweight |
| Container vs VM | A VM boots its own guest OS on virtualized hardware; a container does not. Every other difference follows |
| Container image | Code, its runtime, application **and system** libraries, default settings. No kernel |
| Immutability | Don't change a running container. Build a new image, recreate the container |
| Layers | An image is serialized filesystem layers plus a manifest and a configuration. A shared base is a shared layer |
| Buildpacks | Source → runnable OCI image without hand-authored build files. detect → build → export. CNCF graduated |
| Image reference | `[registry[:port]/]name[:tag | @digest]`. Omit the registry → Docker public registry. Omit the tag → `latest` |
| Tag vs digest | **A tag is a movable label. A digest is a content hash and is immutable** |
| `:latest` | Two problems: unclear version identity *and* a default pull policy of Always |
| Container runtime | Per-node component that manages container execution and lifecycle. containerd, CRI-O, or any CRI implementation |
| kubelet | Node agent that ensures PodSpec containers are running and healthy. Drives; does not execute |
| CRI | The interface Kubernetes **defines** so alternative runtimes can be plugged in. Kubernetes implements nothing below it |
| runC | Donated by Docker to the OCI as the cornerstone of the effort. Runs a filesystem bundle |
| OCI | Governance structure, June 2015. **Three specifications**, not software |
| `image-spec` | The image format: manifest, layer serialization, configuration |
| `distribution-spec` | The API for distributing images. v1.0 May 2020 |
| `runtime-spec` | How to run a filesystem bundle unpacked on disk |
| OCI vs CRI | OCI = format, distribution, bundle execution (industry). CRI = Kubernetes-to-runtime (Kubernetes) |
| `imagePullPolicy` | Always (re-resolve, reuse matching cache), IfNotPresent, Never |
| Pull defaults | digest → IfNotPresent · `:latest` → Always · no tag → Always · other tag → IfNotPresent |
| `ImagePullBackOff` | Container can't start because the image couldn't be pulled. Retries with increasing delay, capped at 300s |
| RuntimeClass | Selects the runtime *configuration* per Pod. Kata (hardware virtualization) or gVisor (user-space kernel) buy isolation at the cost of overhead |
| The pattern | Kubernetes defines interfaces and lets the ecosystem implement them. CRI is the first of four |

---

## The Voyage Ahead

You can now describe a container without hand-waving, predict what an image reference resolves to, name every component between a manifest and a running process, and say which specification governs each hop. That is the bottom of the stack, and it is genuinely the hardest part to reconstruct later if it's shaky, because everything above it is described in terms of it.

Which raises the obvious next question. §4 put a runtime on every node and a kubelet beside it, and then said almost nothing about what else is on that node, or what is *above* the nodes deciding which containers should exist in the first place. There is a whole apparatus that has been quietly implied all chapter — something that holds the desired state, something that decides which node a workload lands on, something that notices when reality has drifted and corrects it. Chapter 3 opens the cluster that the runtime sits inside, and names every part of it.

You will also find the pattern from §4 waiting there. The kubelet you just met is one node component among several, and the reason it can talk to *any* conformant runtime turns out to be the same reason the cluster can use any conformant network plugin and any conformant storage driver. You have seen the move once. Watch for the second.

🏆 **Safe Harbor reached — Containerization complete.**

You've finished the deepest chapter in the book's dependency graph. Everything from here builds upward.

🗺️ Chart → **🌊 Passage** → 🌅 Dawn

> *"Standardize the fitting, and you stop needing to know what's inside. That is not indifference. That is leverage."*
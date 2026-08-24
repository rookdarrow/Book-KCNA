# Fact-Accuracy Audit — Chapter 2

**Mode detected: STANDARD.** The `sources/` directory is populated (87 snapshots), and the draft carries 143 inline `[source: ...]` tags. Untagged factual claims are therefore FAIL, not advisory.

## Input resolution (read this before acting on the findings)

Two conditions materially change what "unsourced" means in this report. Both are upstream of the draft.

**1. The draft path in this stage's prompt did not resolve.** `draft-v2.md` and `draft-voice.md` do not exist for `ch-02`. Stage 4 (voice) wrote **in place** to `draft-v1.md` and preserved `draft-v1-prevoice.md` as the backup — unlike `ch-01`, where Stage 4 emitted `draft-voice.md`. This audit was performed against `../Book-KCNA/.pipeline-state/ch-02/draft-v1.md` (1069 lines, mtime 01:41, post-voice). The stage-6 input glob should be widened, or Stage 4's output naming reconciled across chapters, before the next chapter runs.

**2. The 17 new snapshots this chapter was researched against were never written to disk.** `research-manifest.md` opens with a harness note: *"This stage could not write files… The 17 new snapshots in Appendix A must be written to `../Book-KCNA/sources/` before Stage 3 runs."* They were not. `sources/` contains only the 87 snapshots dated **2026-08-23**; nothing dated 2026-08-24 exists. Consistent with that, the draft contains **zero** `[source: *-2026-08-24]` tags — Stage 3 drafted from the six reusable 2026-08-23 snapshots and left `AUTHOR-REVIEW` comments describing gaps the manifest had already declared closed.

**Consequence for every finding below:** most of them are *not* research gaps. The evidence exists, quoted verbatim, inside `research-manifest.md` Appendix A (items A1–A17). The single highest-leverage fix is mechanical — extract A1–A17 from the manifest into `Book-KCNA/sources/` as files, then re-tag. Findings that genuinely need new research are marked **NEW RESEARCH REQUIRED**; there are two.

## Summary

- Total factual claims inspected: **148** (131 distinct tagged claims across 143 tag instances; 17 untagged factual assertions)
- Tagged claims verified against the cited snapshot: **126**
- Tagged claims unverifiable (tag points to a missing/empty snapshot): **0** — all 17 cited snapshots are present on disk
- **Tagged claims the cited snapshot does not support (FAIL): 5**
- **Untagged factual claims (FAIL): 10** — 6 unsupported by any cached snapshot, 4 fixable by adding a tag to a snapshot already cached
- **Contradicted claims (FAIL): 0** — no claim in this draft disagrees with a snapshot it cites
- Minor discrepancies (WARN): **13**

The chapter's factual spine is in unusually good shape: §3 (references, tags, digests), §6 (pull policies, the four defaults, the 300-second cap), and §7 (RuntimeClass) are quotation-tight against `k8s-docs-images` and `k8s-docs-runtime-class`, including the details books most often get wrong. Every failure below sits in one of four places, and three of the four are already documented in the draft's own `AUTHOR-REVIEW` comments.

---

## FAIL — Untagged factual claims

### Group A — untagged AND unsupported by any snapshot currently on disk

#### Line ~133: "what is shared is the host's **kernel**: the part of the operating system that actually talks to hardware, schedules processes, and enforces boundaries"

**Why it's a factual claim:** an architectural assertion about what a container shares with its host — the chapter's most-quoted sentence and the premise §2, §7, and four answer keys are built on.
**Cache state:** `k8s-docs-overview-2026-08-23` says containers "share the Operating System (OS) among the applications." No cached snapshot says *kernel*. The draft self-discloses this in the `AUTHOR-REVIEW` at line 131.
**Fix:** harvest **A13** (`docker-docs-what-is-a-container`), which per the manifest states "they all share the same **kernel**" and "A VM is an entire operating system with its own kernel," and **A14** (`cncf-glossary-container`, exam authority: "share the same **operating system** and its machine resources"). Manifest finding 1 recommends carrying both registers in one clause — kernel as the mechanism, "shares the OS" as the phrasing the exam will use. There is also an in-cache warrant available today: `k8s-docs-runtime-class-2026-08-23` says a sandboxed runtime uses "a **user-space kernel** (such as gVisor)," which is only coherent if the ordinary case is the *host's* kernel. Also resolves Chapter 1's parallel open comment.

#### Line ~176: "**An image contains no kernel.**"

**Why it's a factual claim:** a negative assertion about image contents, and the target of trap #30. Also restated untagged at line ~809 ("no kernel, and therefore no kernel modules").
**Cache state:** no snapshot states it. `k8s-docs-containers-2026-08-23` enumerates contents (code, its runtime, application and system libraries, default settings) without mentioning a kernel — absence of mention is not an assertion. Manifest finding 7 predicted this audit finding verbatim: *"B1's `[source]` tag on #30 is optimistic; treat it as entailed-from-source."*
**Fix:** keep the claim, but keep it visibly **entailed** rather than quoted — the draft's own framing ("it's §1 read in reverse") is the correct treatment and should not be upgraded to a `[source:]` tag. Harvest **A15** (`cncf-glossary-container-image`: "a single executable binary file, system libraries, system tools, environment variables, and other required platform settings") so the enumeration comes from the exam authority, and tag the *premise* (kernel sharing, per the previous finding) rather than the conclusion.

#### Line ~194: "the layer is **stored and transferred once rather than twice**" — and line ~71, Soundings answer 4: "**Once.**"

**Why it's a factual claim:** an assertion about registry/node storage and network behavior. It is also load-bearing: Practice Q6 (line ~821) is built on it, with distractor A ("The base is duplicated once per image") marked wrong.
**Cache state:** `oci-overview-2026-08-23` supplies only the phrase "filesystem layer serialization." Deduplication is nowhere in the cache. The draft flags this twice (lines 219, 831).
**Fix:** harvest **A9** (`docker-docs-image-layers`), which per manifest finding 2 states that the format "allows layers to be reused between images," which "reduce[s] the amount of storage and bandwidth required to distribute the images" — the manifest calls this "Soundings Q4's answer key, verbatim." Harvest **A6** for stack order ("The array MUST have the base layer at index 0"). Note that the manifest records **G29 as fully closed** and Open Question #2 as resolving to option (a): `ch02-fig02` keeps its name and its shared-base half. Once A9 lands, both `AUTHOR-REVIEW` comments and the Q6 reframing suggestion can be deleted rather than acted on.

#### Line ~178: "They are part of the operating system's **userspace**, and userspace is exactly what the image supplies."

**Why it's a factual claim:** asserts a kernel/userspace division of responsibility between host and image.
**Cache state:** unsupported; depends entirely on the kernel-sharing claim above.
**Fix:** resolves with A13/A14/A15. Do not fix independently.

#### Line ~493: "a single component like containerd genuinely participates in both: it implements the CRI **and** handles OCI images"

**Why it's a factual claim:** a capability claim about a named third-party project, and it is the hinge of the chapter's hardest discrimination (the ⚠ CRI-vs-OCI callout) as well as the answer key for Practice Q20.
**Cache state:** `k8s-docs-containers-2026-08-23` establishes containerd as a CRI implementation. Nothing in the cache says containerd handles OCI images.
**Fix:** harvest **A17**. Manifest finding 4 supplies a single primary-source sentence containing both acronyms in their correct planes — CRI-O's own front page: *"CRI-O is an implementation of the Kubernetes CRI (Container Runtime Interface) to enable using OCI (Open Container Initiative) compatible runtimes."* Anchor the hazard callout and Q20 on that quotation instead of asserting the intersection in the book's voice.

#### Lines ~711 and ~726–732: intermodal-container history — "It won because the industry standardized the **interface**, meaning the dimensions, the corner fittings, the lifting points"; "Unloading takes days"

**Why it's a factual claim:** these are checkable historical and engineering specifics about a real industry, not analogy furniture. Rule 3 exempts the *comparison* ("an image is the crate"); it does not exempt the assertion that standardization of specific fittings is what produced the gain, which is §8's entire argument and the Zenith's payload.
**Cache state:** no snapshot covers containerization history. The chapter has already applied the correct standard to itself once — the epigraph `AUTHOR-REVIEW` at line 38 refuses an unverifiable McLean attribution on exactly this principle.
**Fix — NEW RESEARCH REQUIRED (1 of 2):** the manifest's Open Question #9 already names the route and prefers it to a quotation: **ISO 668** (*Series 1 freight containers — Classification, dimensions and ratings*) and **ISO 1161** (corner fittings). The manifest notes `iso.org` returns 403 to WebFetch, so this needs a browser session or an alternate authoritative catalogue entry. Do **not** draft the "McLean released the patent royalty-free to ISO" claim — the manifest found it only in third-party commercial sources and could not verify it. Interim option if the gap stays open: mark the passage as declared analogy ("the usual telling of it is…") so it stops reading as sourced history.

### Group B — untagged, but a cached snapshot already supports it (tag-only fix, no research)

#### Line ~164: "it comes with a shared network namespace"

**Fix:** tag `k8s-docs-network-model-2026-08-23` — "A pod has its own private network namespace which is shared by all of the containers within the pod." Already on disk.

#### Line ~162: "The docs use exactly that word, *relaxed*"

**Fix:** verified true — `k8s-docs-overview-2026-08-23` reads "relaxed isolation properties." Tag it; a claim *about* the documentation's wording should cite the documentation.

#### Line ~229: "Compilers, headers, and build tooling are attack surface that your production image has no use for"

**Fix:** harvest **A11**/**A12**, which per manifest finding 2 state "None of the build tools required to build the application are included in the resulting image" and "A small image with minimal dependencies can considerably lower the attack surface." The manifest explicitly notes this restores the ⚓ Worth Securing beat §2 originally planned, which means the `AUTHOR-REVIEW` at line 233 can be closed by *addition* rather than by leaving the sourced build/run-image substitute in place.

#### Line ~4: "CNCF publishes domain weights, not competency weights"

**Fix:** tag `cncf-kcna-curriculum-pdf-2026-08-23`, which lists the four domains with percentages and their competencies **without** per-competency weights. Already on disk. (See also W1.)

---

## FAIL — Contradicted claims

**None.** No claim in this draft disagrees with a snapshot it cites. Every figure I could check against the cache is exact: 44% for Kubernetes Fundamentals; OCI established June 2015; `distribution-spec` v1.0 May 2020; `busybox` ≡ `docker.io/library/busybox:latest`; `registry.k8s.io/pause:3.5`; all three pull policies; all four conditional defaults; the 300-second (5-minute) `ImagePullBackOff` cap; `apiVersion: node.k8s.io/v1`; containerd and CRI-O both on the CNCF graduated list.

---

## FAIL — Tagged claims the cited snapshot does not support

Distinct from contradiction: the claim is not refuted by the cache, but the tag implies verbatim support that isn't there. These are the entries a reader checking your citations would catch.

### Lines ~337–338 (Bearings #1, Q1 explanation): "its image carries no kernel of its own"

**Tag:** `[source: k8s-docs-overview-2026-08-23]`; and "an image bundles application and system libraries, **not a kernel**" `[source: k8s-docs-containers-2026-08-23]`
**Snapshot says:** overview — "relaxed isolation properties to share the Operating System (OS) among the applications"; containers — "the code and any runtime it requires, application and system libraries, and default values for any essential settings."
**Draft says:** that the image carries no kernel, presented as sourced fact in an answer key.
**Recommended fix:** strip the `[source:]` tag from the negative half and derive it in the explanation from the tagged kernel-sharing premise, per manifest finding 7. The claim is sound; the citation form overstates it. Same treatment for line ~809 ("no kernel, and therefore no kernel modules").

### Line ~420 (★ Fixed Point) and ~744 (Exam Alert #2): "kubelet → CRI → containerd or CRI-O → **runC** → a running process"

**Tag:** `[source: k8s-docs-containers-2026-08-23]` `[source: k8s-docs-extending-kubernetes-2026-08-23]`
**Snapshot says:** containers — Kubernetes "supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI"; extending-kubernetes — "Container runtime (CRI, the Container Runtime Interface, to support alternative container runtimes)." `oci-overview` establishes that Docker *donated* runC to the OCI — provenance, not use. Neither snapshot states that a CRI runtime invokes an OCI runtime.
**Draft says:** a five-hop chain naming runC as a link, in the chapter's most-retrieved item (reused in Ch 3, 8, 13, 17).
**Recommended fix:** harvest **A17**. Manifest finding 4: containerd's README — "Most interactions with the Linux and Windows container feature sets are handled via **runc**" — closes the hop end to end. Also harvest **A1** (`k8s-docs-cri`), which supplies the sentence the manifest calls the chapter's thesis: "The CRI is a plugin interface which enables the kubelet to use a wide variety of container runtimes, without having a need to recompile the cluster components," plus "The kubelet acts as a client when connecting to the container runtime via gRPC." Both make the Fixed Point sourced rather than authored. The `AUTHOR-REVIEW` at line 424 offers softening to "CRI runtime → OCI runtime" as the fallback — with A17 harvested, take the named chain and delete the fallback. Heed the manifest's scope caution: take only those two sentences from A1; `--container-runtime-endpoint`, the v1-CRI-API requirement, gRPC message limits, and `CRIListStreaming` are not KCNA material.

### Line ~633 (🔭 Closer Look): gVisor "intercepts the workload's system calls and services them in a kernel implementation running as an ordinary process, so the host kernel is never the workload's direct interlocutor"

**Tag:** `[source: k8s-docs-runtime-class-2026-08-23]`
**Snapshot says:** only "a user-space kernel (such as gVisor)." The syscall-interception mechanism is not present. (The Kata half of the same callout — "hardware virtualization" — *is* supported.)
**Draft says:** a two-sentence mechanism description attributed to a snapshot that contains neither sentence.
**Recommended fix — NEW RESEARCH REQUIRED (2 of 2):** fetch `gvisor.dev/docs/` for the Sentry/syscall-interception description; A1–A17 do not cover it. Cheaper alternative, and defensible for a junior-tier chapter: cut to the snapshot's own phrase — gVisor supplies a user-space kernel, Kata supplies hardware virtualization, different overheads — and drop the mechanism. The callout's own closing line already concedes the exam is far likelier to ask *why* RuntimeClass exists, so the mechanism is the expendable half.

### Line ~495 (🔭 Closer Look): "**Two of the three specifications were part of the effort from its 2015 founding**; the distribution specification did not reach v1.0 until May 2020"

**Tag:** `[source: oci-overview-2026-08-23]`
**Snapshot says:** "Established in June 2015 by Docker and other leaders in the container industry, the OCI **currently** contains three specifications"; and that `distribution-spec` "reached v1.0 in May 2020 and was introduced to OCI as an effort to standardize the API." It gives no v1.0 date for `image-spec` or `runtime-spec` and does not say when either entered scope.
**Draft says:** a specific chronology ("from its 2015 founding," "Five years is a long gap") plus an inference about which problems the industry prioritized.
**Recommended fix:** reduce to what the snapshot carries — the OCI was founded June 2015 and the distribution specification reached v1.0 in May 2020, arriving after the other two — and drop "from its 2015 founding" and the five-year arithmetic. Alternatively source `image-spec`/`runtime-spec` v1.0 dates from opencontainers.org. The exam-relevant kernel of the callout (which specification governs the registry API) survives either edit intact. Same defect, smaller, in Practice Q14's explanation A — see W8.

### Line ~438: "`crictl` reaches the runtime **directly, beneath Kubernetes**, which is occasionally exactly what you need"

**Tag:** `[source: k8s-docs-debug-overview-2026-08-23]`
**Snapshot says:** under Troubleshooting Clusters, only the list item "debugging Kubernetes nodes with crictl." No description of what crictl talks to.
**Draft says:** a behavioral claim about the tool's position in the stack.
**Recommended fix:** the sentence's *purpose* here is a forward pointer to Ch 13, so the cheapest correct edit is to drop the mechanism and keep the pointer ("a diagnostic tool that operates at the node level, which Ch 13 §5 covers"). If the "beneath Kubernetes" framing is wanted — it does reinforce §4's boundary usefully — source it from `kubernetes.io/docs/tasks/debug/debug-cluster/crictl/`.

---

## WARN — Minor discrepancies

**W1 — Line ~4, tag selects the wrong snapshot for half the claim.** "Kubernetes Fundamentals (44% of the exam) — competency: Containerization `[source: cncf-kcna-certification-page-2026-08-23]`". That snapshot lists domain weights only; it does not enumerate competencies. Re-tag the competency half to `cncf-kcna-curriculum-pdf-2026-08-23` ("44% – Kubernetes Fundamentals: Kubernetes Core Concepts; Administration; Scheduling; **Containerization**") or `lf-kcna-exam-page-2026-08-23`. Both on disk. The 44% figure itself is correct and correctly tagged.

**W2 — Line ~4, the authored ~9% allocation.** Disclosed transparently and correctly ("authored allocation… see front matter"), and the manifest confirms the sub-competency weight gap remains OPEN with no in-chapter restatement needed. No change required; recorded here so the audit trail shows it was inspected rather than missed.

**W3 — Lines ~448 and ~951: "operates under the Linux Foundation."** Supported by `oci-overview-2026-08-23`'s `authority:` frontmatter ("Open Container Initiative (Linux Foundation)"), not by its body text. Acceptable if frontmatter counts as snapshot content; if the contract requires body-text support, this needs a sentence from opencontainers.org. Flagging the ambiguity rather than the claim, which is true.

**W4 — Line ~719: "for a decade."** Tagged `[source: k8s-docs-overview-2026-08-23]`, which carries the substance ("If an application can run in a container, it should run great on Kubernetes") but no time span. Add `k8s-history-ten-years-2026-08-23` (first commit June 6, 2014) or cut the clause.

**W5 — Unsourced exam-behavior and frequency claims, in tension with the chapter's own stated policy.** Line ~763 states plainly: *"The book does not make frequency claims it cannot support."* Nine passages sit at or over that line: "the largest share of its exam surface" (~31); "Those two sections score well on intuition and still surprise people on the exam" (~81); "the densest exam surface in the chapter" (~241); "What the exam may well ask is…" (~495); "the highest value per minute of anything in it" (~569); "Readers skip this section. The exam does not." (~613); "the exam is far more likely to ask *why* RuntimeClass exists" (~633); "the exam will give you a reference and ask for the behavior" (~748); and "The one you will actually use most, `imagePullSecrets`" (~297). None is sourceable — CNCF publishes weights, not item frequencies. The manifest's finding 5 applies the right standard to trap #34 ("easy to confuse," never "frequently tested"); apply the same standard here. Convert to authored-judgment framing or hedge. The §7 opener is the one worth keeping as-is if any are — it earns its rhetoric — but it should read as the author's counsel, not as data.

**W6 — Line ~231: gloss on "reproducible layers."** The tag supports the phrase; "the same input reliably produces the same layer bytes rather than layers that differ run to run because of timestamps or file ordering" is an authored definition. Either mark it as such or take A10/A11's build-cache language once harvested.

**W7 — Line ~160: the derivation block.** "VMs start slowly and containers start quickly… VM images are large and containers are small… container density is higher" is explicitly presented as reader-performed derivation from a tagged premise, which is the right pedagogy. Note only that A13/A16 would let the VM-boot contrast be quoted rather than derived, if Stage 11 wants it firmer.

**W8 — Line ~911 (Practice Q14, explanation A): "June 2015 is the OCI's founding, not a specification's v1.0."** The first half is sourced; the second is an absence claim the snapshot cannot support (it gives no `image-spec` v1.0 date). Trim to "June 2015 is the OCI's founding date, not the distribution specification's v1.0."

**W9 — Line ~951 (Practice Q18, explanation A): "runC predates and sits below the CRI."** A chronology claim with no snapshot behind it. "Sits below" is fixed by A17; "predates" should be cut unless sourced.

**W10 — Line ~426: "Docker's public debut."** The snapshot says the March 2013 lightning talk "introduced an upcoming open source tool called 'Docker'" — close, but "public debut" is the draft's characterization. The accompanying "four things wearing one name" enumeration is authored framing, not sourced; fine as framing, but it should not look like a documented taxonomy. Once A3 is harvested, manifest finding 5 lets this whole Snag rest on the Kubernetes project's own dockershim FAQ instead ("Early versions of Kubernetes only worked with a specific container runtime: Docker Engine"). Two cautions from the manifest apply: that FAQ is dated 2022-02-17 and must not be presented as current, and the dockershim *history* belongs to Chapter 3.

**W11 — Line ~252: `busybox:1.36`.** An invented version tag in the resolution table. The *rule* being illustrated is documented; the specific version is authored and unverified. Harmless, but exam guides get audited on invented version numbers — consider `busybox:1.36` → a plainly generic form, or reuse the documented `registry.k8s.io/pause:3.5` shape.

**W12 — Line ~601: untagged derivation.** "It flips the default from IfNotPresent to Always, which means the kubelet consults the registry on every container launch" is correct and follows directly from the Dead Reckoning block tagged 30 lines above. Low risk; a repeated tag would make the paragraph self-contained.

**W13 — Line ~293: "A registry is where images live between being built and being run. You push there and nodes pull from there."** The tag carries push-before-reference and (via the `Always` description) the kubelet querying the registry, so this is defensible. **A7** would upgrade it to spec-level definitions — "Registry: a service that handles the required APIs defined in this specification," "Push: the act of uploading blobs and manifests to a registry," "Pull: the act of downloading blobs and manifests from a registry" — and per manifest finding 6 would also give §3's digest Fixed Point a second independent authority ("a unique identifier created from a cryptographic hash of a Blob's content"). Recommended, not required.

---

## PASS — Verified claims (coverage evidence)

Sampled and matched against the cited snapshot, quotation-level:

**§1 / §2 — `k8s-docs-containers`, `k8s-docs-overview`, `oci-overview`, `buildpacks-concepts`**
repeatability from included dependencies (~121) · decoupling from host infrastructure (~121) · VMs isolate applications, each a full machine with its own OS on virtualized hardware (~127) · relaxed isolation, shared OS, lightweight, own filesystem/CPU share/memory/process space, portable across clouds and OS distributions (~129) · containers in a Pod co-located and co-scheduled (~164) · image contents including **application and system** libraries (~172, ~342, ~808) · "very well defined assumptions about their runtime environment," push to a registry before referring to it in a Pod (~172) · stateless and immutable, build-then-recreate as the correct process (~182, ~818) · quick and efficient rollbacks due to image immutability (~188) · OCI Image Format = manifest + filesystem layer serialization + configuration (~192, ~460, ~860) · buildpack, builder, build/run image, stack, platform (`pack` CLI or CI), lifecycle detect→build→export with reproducible layers, CNCF graduated (~227, ~840, ~850)

**§3 — `k8s-docs-images` (33 tag instances, the densest surface in the chapter; all verified)**
image-name forms with optional registry hostname and port (~245) · no hostname ⇒ Docker public registry (~245, ~352, ~870) · no tag ⇒ `latest` (~245) · `busybox` ≡ `docker.io/library/busybox:latest` including the `library` namespace (~245, ~866–871) · `registry.k8s.io/pause:3.5` and `registry.k8s.io/pause@sha256:1ff6…` as documentation examples (~255, ~257) · tags identify a series; digests are a content hash and immutable; tags can be moved (~263, ~271, ~880) · avoid `:latest` in production — harder to track the running version, harder to roll back; prefer `v1.42.0` and/or a digest (~277, ~890) · all five private-registry credential paths, with `imagePullSecrets` referencing a `kubernetes.io/dockerconfigjson` Secret (~295, ~345, ~900)

**§4 / §5 — `k8s-docs-containers`, `k8s-docs-cluster-architecture`, `k8s-docs-components`, `k8s-docs-setup-tooling`, `k8s-docs-extending-kubernetes`, `oci-overview`, `cncf-project-maturity-levels`, `k8s-history-ten-years`**
runtime responsible for container execution and lifecycle; containerd, CRI-O, or any other CRI implementation (~377, ~537, ~920) · runtime is a node component alongside kubelet and optional kube-proxy (~381) · a runtime must be installed on every node (~381, ~940) · kubelet ensures PodSpec containers are running and healthy, and does not manage containers it did not create (~383, ~539) · CRI named as an infrastructure extension point "to support alternative container runtimes" (~389, ~930) · CSI, CNI, device plugins, API extensions as the sibling extension points (~434) · March 2013 five-minute lightning talk, Docker's popularity setting the stage for orchestration at scale (~426) · containerd and CRI-O both CNCF **graduated**, with the graduated definition (~428, ~951) · cluster picks the default runtime; RuntimeClass for multiple runtimes (~430, ~1020) · OCI as an open governance structure, established June 2015 by Docker and other industry leaders (~448, ~542, ~960) · three specifications, with `distribution-spec` v1.0 May 2020 (~454, ~462, ~746, ~910) · `runtime-spec` governs running a filesystem bundle unpacked on disk (~464, ~547) · download image → unpack to filesystem bundle → run (~466) · runC donated by Docker as the effort's cornerstone (~391, ~497, ~950) · kube-apiserver exposes the HTTP API; scheduler assigns Pods to nodes; kube-proxy maintains node network rules; controller-manager runs controllers (~538, ~540, ~921)

**§6 — `k8s-docs-images`, `k8s-docs-debug-pods`**
all three pull policies verbatim, including `Always` = resolve to digest then reuse a digest-matching local cache (~571, ~603, ~680) · all four conditional defaults: digest ⇒ IfNotPresent, `:latest` ⇒ Always, no tag ⇒ Always, other tag ⇒ IfNotPresent (~573, ~675, ~748, ~980) · `imagePullPolicy` not updated when the tag or digest changes later (~575, ~605, ~1000) · `ImagePullBackOff` — cause, invalid-name and private-registry-without-secret examples, increasing back-off to the compiled-in 300-second (5-minute) limit (~577, ~685) · reported as a container in the **Waiting** state (~607) · stuck-pull triage: check the name, check that the image was pushed (~607)

**§7 — `k8s-docs-runtime-class`, `k8s-docs-cloud-native-security`**
RuntimeClass selects the container runtime *configuration* (~617) · performance-versus-security balance; hardware virtualization (Kata) or a user-space kernel (gVisor); extra isolation at the cost of overhead; also same runtime with different settings (~621, ~690, ~1010) · handler names configured per CRI implementation; `apiVersion: node.k8s.io/v1`, `kind: RuntimeClass`, `handler` field; `runtimeClassName` in the Pod spec; default handler when omitted (~627, ~1020) · RuntimeClass may carry `nodeSelector`/`tolerations` and a Pod overhead the scheduler accounts for (~631, ~1011) · "use a container runtime that provides security restrictions" as runtime compute protection (~635)

**Skipped as out of scope per rules 3 and 4:** the crate/crane/port-authority analogy structure itself, the Logbook Entry narrative, all ⚓/🪝/🪢 framing devices, the Figure 2-6 commissioning note, and prose quality throughout. §8's *historical specifics* were not skipped — see the Group A finding.

---

## Recommended order of operations for Stage 11

1. **Extract Appendix A (A1–A17) from `research-manifest.md` into `Book-KCNA/sources/` as 17 files.** Mechanical, no research, and it closes 6 of the 15 FAIL items outright. Verify the write actually landed this time — Stage 2's silent write failure is what produced most of this report. Chapter 1's Stage 2 hit the same condition, so this is a recurring harness fault worth fixing at the executor rather than per chapter.
2. **Re-tag, then delete rather than act on three `AUTHOR-REVIEW` comments.** Lines 219 and 233 (G29 layers and base-image selection) and line 424 (the runC hop) all describe gaps the manifest closed; with A1/A6/A9–A12/A17 on disk, the fallbacks they propose — narrowing §2, renaming `ch02-fig02`, softening the Fixed Point — should **not** be taken. Manifest finding 2 is explicit: do not rename the anchor.
3. **Downgrade two citation forms to entailment** (image-carries-no-kernel, at ~337 and ~809), per manifest finding 7.
4. **Trim four over-reaching glosses** to what their tags carry: gVisor's mechanism (~633), the OCI spec chronology (~495, ~911), crictl's position (~438), `runC` "predates" (~951).
5. **Two decisions that need the author, not a fetch:** whether to source §8's shipping-container history via ISO 668/1161 or reframe it as declared analogy (manifest Open Question #9, still open and blocking only the epigraph and §8's framing); and how far to hedge the exam-behavior claims in W5 given the chapter's own policy statement at line 763.
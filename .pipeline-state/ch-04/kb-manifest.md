I have everything I need. Emitting the manifest to stdout.

---

**Two facts that change what this stage could do, both verified on disk:**

1. **`Book-KCNA/knowledge-base/` still does not exist.** Chapter 1's and Chapter 3's Stage 14 both composed full write blocks; neither reached disk. My own `Write` and `Bash` attempts were denied here too, and the session is non-interactive.
2. **The root cause is not only permissions.** `=== WRITE` appears exactly once in the entire `certcomp` repo — in `pipeline/prompts/14_knowledge_base_update.md`, the prompt that asks for it. **No parser consumes these blocks anywhere in the pipeline.** Fixing permissions alone would not have landed Chapter 1's or Chapter 3's artifacts. A materializer is included below.

```markdown
# Knowledge-Base Manifest — KCNA Chapter 4

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 4 — Records of Intent
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24

**Inputs consulted:** the finalized chapter; `ch-04/integration.md` (Stage 13); `ch-04/outline.md` frontmatter (`kb_tags` — 52 concepts, 5 commands); `ch-03/kb-manifest.md` (read in full, 1,696 lines); `ch-01/kb-manifest.md` (block index); `book-outline/chapter-lineup.md` (B2); `ch-04/diagnostics/{structural,theming-density,fact-accuracy}.md`; `Book-KCNA/sources/` (115 files, enumerated).

## ⚑ Gate holes inherited, and one that closed

Carried forward, unresolved:

- **Chapter 4 has no fact-accuracy audit.** `diagnostics/fact-accuracy.md` is a BLOCKER notice: both `draft-v2.md` and `draft-voice.md` came through as `[file not available]`, so Stage 6 inspected **0 claims**. Its own text says the zeroes are "the absence of an audit, not a clean bill of health." Every glossary definition below inherits the chapter's wording verbatim per Rule 5, which is a *fidelity* guarantee, not an *accuracy* one. **Re-run Stage 6 against `draft-v2.md`.**
- **`diagnostics/structural.md` audited `draft-v1.md`** (0 fail / 0 warn / 30 pass). `draft-v2.md` is ~17 KB longer and unaudited.
- **`diagnostics/theming-density.md` also audited `draft-v1.md`.** It scores 0.4 metaphors per 1,000 words (band 1–3, *underseasoned*) and calls §6 "metaphor-free." That verdict is stale: the shipped §6 carries the harbormaster callback ("Go back to the harbormaster's desk from §1"), which is the exact fix the audit recommended. Re-run before acting on it. The audit's other observation stands and is worth the author's attention — **the chapter's only consistent figurative register is financial, not nautical** ("comes due," "collects on it," "collecting rent"), three instances against five maritime ones.
- **Chapter 2 still never ran Stages 13–14.** Eleven of its terms remain in Tier 4 with no definitions. Chapter 4 leans on two of them (`imagePullSecrets` lineage, image immutability) for retrieval items.

**Closed by observation — retire eight flags in Chapter 3's ledger:** Chapter 3's Stage 14 recorded `sources/` as "87 files, zero dated 08-24" and tagged eight glossary and shard entries `⚑ SNAPSHOT NOT ON DISK`. `sources/` now holds **115 files, 28 of them dated 2026-08-24**, including `k8s-docs-control-plane-node-communication`, `k8s-docs-etcd-access-control`, `k8s-docs-cluster-addons`, and `k8s-docs-dns-cluster-addon`. Chapter 4's research pass materialized them. **All eight of Chapter 3's missing-snapshot flags can be struck**, and all eight `-2026-08-24` tags Chapter 4 uses resolve to real files.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**41 terms contributed** — 34 defined, 5 partial, 2 status corrections. Appended as a Chapter 4 section rather than merged into the existing A–Z, because this file is append-only from here and re-transcribing 500 lines of Chapter 1 + Chapter 3 prose to preserve one alphabet is exactly the drift Rule 5 forbids. Book assembly merges alphabets.

Stage 13 marked **four** terms as needing entries (`kubectl apply`, `kubectl explain`, `kubectl api-resources`, `field selector`). All four are recorded as **partials with defining chapters**, not padded into full definitions. The other 37 are terms Chapter 4 defines outright.

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **Kubernetes object** | "persistent entities in the Kubernetes system… A Kubernetes object is a **'record of intent'** — once you create the object, the Kubernetes system will constantly work to ensure that the object exists" | Chapter 4 §1 |
| **manifest** | "a file known as a **manifest**, and by convention, manifests are YAML" | Chapter 4 §2 |
| **`apiVersion`** | "which version of the Kubernetes API you're using to create this object" | Chapter 4 §2 |
| **`kind`** | "what kind of object you want to create" | Chapter 4 §2 |
| **`metadata`** | "data that helps uniquely identify the object, including a name string, a UID, and an optional namespace" | Chapter 4 §2 |
| **`spec`** | "what state you desire for the object" | Chapter 4 §2 |
| **`status`** | "describes the current state of the object, supplied and updated by the Kubernetes system and its components" | Chapter 4 §2 |
| **name / UID** | name is "client-provided… reusable"; UID is "system-generated… intended to distinguish between historical occurrences of similar entities" | Chapter 4 §2 |
| **declarative / imperative interface** | imperative: "you instruct the server what to do"; declarative: "you declare the desired state… and a controller keeps the current state of objects in sync" | Chapter 4 §1 — **closes Chapter 1's reservation** |
| **namespace** | "a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces" | Chapter 4 §3 |
| **`kube-system`** | "The namespace for objects created by the Kubernetes system" | Chapter 4 §3 — **closes Chapter 3's reservation** |
| **ConfigMap** | "an API object used to store **non-confidential** data in key-value pairs" | Chapter 4 §4 |
| **Secret** | "an object that contains a small amount of sensitive data… **specifically intended to hold** confidential data" | Chapter 4 §4 |
| **base64 encoding** | "**not** an encryption method, it provides no additional confidentiality over plain text" | Chapter 4 §4 |
| **label** | "key/value pairs… identifying attributes… that **do not directly imply semantics to the core system**" | Chapter 4 §5 |
| **label selector** | ★ "**the core grouping primitive in Kubernetes**" | Chapter 4 §5 |
| **annotation** | "arbitrary **non-identifying** metadata… **not used to identify and select objects**" | Chapter 4 §5 |
| *(24 further rows — full text in the append block)* | | |

### Rule 6 — canon conflicts, recorded not resolved

Five. Two are new, two are carried forward, **one is now settled by observation.**

1. **⚑ `Lease` has three claimed owners — and B2 settles it.** Chapter 3's ledger recorded `Lease → Ch 5 / Ch 12`. Chapter 4 bears it to `Ch 8 §4`. `chapter-lineup.md` row 8 reads *"node lifecycle (…cordon/drain/uncordon, node conditions, **leases**)"* — **verified on disk, not inferred.** Chapter 4 is right and Chapter 3's row is stale. Recorded as a correction with the evidence line, not silently overwritten.
2. **✅ `PodSpec` Ch 4-vs-Ch 5 conflict — now resolved.** Chapter 3's prose said *"Chapter 4 gives it a proper treatment"* while its ledger recorded Ch 5. **Chapter 4 has shipped and does not mention PodSpec once.** The ledger assignment is confirmed correct by outcome; Chapter 3's prose is now demonstrably wrong and needs a one-word fix.
3. **⚑ `reconciliation` — the gap Chapter 3 opened is unkept at its first opportunity.** Chapter 3 promised the reader: *"when later chapters say **reconciliation**, this closing-the-gap work is exactly what the word names."* Chapter 4 is the first later chapter. It uses the word family three times (Soundings A3 "reconciler"; Bearings #1 Q3 "while the system reconciles"; §2 figure caption) and **never names the term.** Chapter 3 made a promise to the reader; Chapter 4 was where it came due.
4. **⚑ Convention 5 was proposed at Chapter 3 and broken at Chapter 4.** Chapter 3's ledger proposed *"No `§N` in cross-bearings that point into undrafted chapters"* and followed it for 18 of its 20 forward bearings. Chapter 4 pins §-numbers into eleven undrafted chapters, fifteen times. It was never ratified, so this is a governance decision, not a defect — but it is the direct cause of the next item.
5. **⚑ §N reservation collisions, now three-deep.** Chapter 4 adds claims that collide with already-shipped chapters: **Ch 12 §2/§3/§4** (Chapter 2 claimed all three for supply-chain topics; Chapter 4 claims them for access control) and **Ch 6 §3** (now claimed by Chapters 1, 2, and 4 for three different topics). Separately, **Chapter 4 is the correct party on `Ch 9 §4`** — B2 row 10 puts NetworkPolicy in Chapter 10, so `chapter-02:871` is the wrong pointer.

---

## Concept shards added at `Book-KCNA/knowledge-base/concepts/{slug}.md`

Ten created. Every slug is drawn from `outline.md`'s `kb_tags.concepts` so context-packer lookups round-trip.

- `concepts/kubernetes-object.md` — **created** (§1–§2; the four fields, name vs UID, the apply round trip)
- `concepts/declarative-configuration.md` — **created** (§1, §6; the three management techniques and the honest correction)
- `concepts/spec.md` — **created** (§2)
- `concepts/status.md` — **created** (§2) — *carries the "a gap is not a fault" rule Ch 13 depends on*
- `concepts/namespace.md` — **created** (§3)
- `concepts/cluster-scoped-resource.md` — **created** (§3) — **B3 cross-cutting theme, originates here**
- `concepts/configmap.md` — **created** (§4)
- `concepts/secret.md` — **created** (§4)
- `concepts/label-selector.md` — **created** (§5) — **B3 cross-cutting theme, originates here**
- `concepts/annotation.md` — **created** (§5)

**Not created, with reasons.** `manifest`, `record-of-intent`, `object-uid`, `matchlabels`, `matchexpressions` — folded into the shards above rather than fragmented; each is a paragraph, not a concept. `encryption-at-rest` and `secret-hardening` — **Chapter 12 owns these**, and Chapter 4 deliberately hands over all four hardening steps without teaching one; creating a shard here would pre-empt that chapter with a list Chapter 4 never explains. **No `commands/` shards** — Chapter 4's four `kubectl` verbs are one clause each and Chapter 8 owns the command surface; this follows Chapter 3's precedent of leaving `etcd` for Chapter 8. The four partial definitions are in the glossary now so nothing is lost.

---

## Voice-exemplar candidates nominated

**Not written to `voice-exemplars.md`** — Rule 1. Nominations only, for author ratification.

| Function | Excerpt | Recommendation |
|---|---|---|
| **chapter-opening / curiosity gap** | "Here is something unusual about the chapter you are starting: **nothing in it is a verb.** … If you arrived from imperative operations tooling, from a world of scripts and runbooks and commands that execute and finish, this is genuinely strange for about a chapter. Better to name the strangeness than smooth it over, so we name it now, live with it through §2 to §5, and resolve it in §6." | **Strongest in the chapter.** Opens the gap, names the reader's prior expertise as the *source* of the difficulty rather than a deficiency, and publishes the resolution schedule. Warm and confident without reassurance. |
| **Extended Analogy** | "A declaration lodged with the harbormaster is not an instruction to anyone… But everything that happens afterward is checked against it… If what's in the hold stops matching what's on the paper, the paper does not change. The hold does. And critically, none of those people received an order from you. They read a record, compared it to what they observed, and acted on the difference." | **Strong.** Every beat maps to a real mechanism (harbormaster → API server; independent parties consulting → controllers watching; the hold changes, not the paper → reconciliation direction). The theming audit rates it dense-by-design and recommends no trimming. |
| **★ Fixed Point** | "**`spec` is what you want. `status` is what is. You write `spec`. The system writes `status`. Every controller in the cluster exists to close the distance between them.**" | **Strong.** Five short clauses, no metaphor, exactly memorizable. The book's most-reused sentence by the chapter's own account. |
| **☀️ Zenith** | "**you do not participate in the loop. You supply its reference.** … It does this at 09:00 and at 03:17 and on the fourteen-thousandth iteration, with exactly the same logic, without you present… Your record is not a message that was delivered. It is the standing answer to a question the cluster asks itself continuously." | **Strong.** The one-sentence inversion followed by concrete times rather than an abstraction. |
| **self-correction / epistemic honesty** | "`kubectl scale` updates the size of a workload, which is to say it edits a number in a `spec`, and then something else notices. The imperative command did not scale anything. It amended a record… **The objects are declarations, and the imperative commands work by changing declarations.** That is the accurate claim, narrower than the chapter subtitle and better." | **Strong, and structurally important.** Deliberately mirrors Chapter 3 §7's audit of its own chapter title. Two chapters now perform the same move on their own most quotable line — that is a series-level voice signature worth locking. |
| **⚓ Worth Securing** | "ReplicaSet, Service, NetworkPolicy, and node affinity are not four mechanisms to learn. They are one mechanism, *describe a set by its attributes*, aimed at four problems. Learn the primitive once and you spend the later chapters learning what each resource *does* with its set, which is the interesting part." | **Strong.** Models §18.14 scope discipline and pays the reader in saved effort rather than exhortation. |
| **🪝 Snag / subject dignity** | "`status` is not something you write… It is a report, not a request. Practitioners arriving from imperative tooling try this at least once, usually at two in the morning, while trying to make a stuck object look healthy." | **Strong — nominate specifically as a Part 14 subject-dignity exemplar.** The wry beat lands on the practitioner's own 3 a.m. self-deception, which is exactly the orientation skill v5.7 licenses. |
| **🪢 Mnemonic** | "The four fields answer four questions, always in the same order. **Which API? Which kind of thing? Which one, specifically? What should it look like?**" | **Moderate–strong.** Converts memorization into a reading procedure; no acronym, no forced nautical dressing. |
| **why-wrong explanation** | *(Q12 distractor D)* "**D is the most instructive miss, because half of it is a real belief:** applications genuinely do differ in whether they cache configuration at startup. It does not help here… The application's diligence is irrelevant when the source never changes." | **Moderate–strong.** Credits the reasoning behind the wrong answer before dismantling it. |
| **Dead Reckoning** | "`apiVersion`: a string naming the API group and version this object belongs to. Selects the schema. `kind`: a string naming the resource type…" | **Moderate.** Correct facts-only register — four parallel clauses, zero framing. Mechanical by design, as it should be. |

**Deliberately not nominated:** every line carrying an unsourced prevalence superlative — "the single most common day-one surprise," "produces more confident wrong answers than anything else in this chapter," "a piece of knowledge a surprising number of working practitioners have wrong," "the detail that gets asked," "the one candidates miss" — plus §3's two claims about what "most preparation material admits." Chapter 3's Guardrail #8 remediation is still open, and promoting this register would ratify it into brand canon before the author has ruled on it. Same reasoning Chapter 3's Stage 14 applied to its Exam Alert.

---

## Objective coverage log

Chapter 4 covers **D1.1 — Kubernetes Core Concepts** at **deep** depth. D1.1 remains **in progress**: B2 assigns it four consecutive chapters (3–6), and Chapter 4 delivers the object layer.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.1 | Chapter 3 | deep (cluster layer) | 2026-08-24 |
| **D1.1** | **Chapter 4** | **deep (object layer)** | **2026-08-24** |

Authored weight estimate **~6%**, disclosed inline with the correct caveat — the chapter states the published figure (Kubernetes Fundamentals at 44%) and says plainly that CNCF publishes no per-competency weights. That is the compliant pattern; keep it.

**⚑ One factual contradiction to fix in the chapter:** Safe Harbor reads *"Chapter 4 of 15 complete."* `chapter-lineup.md` runs to **20** rows (row 19 synthesis, row 20 Full Mock Exam), and Chapters 1 and 3 both reference Chapter 17 by name in shipped text. Verified on disk.

---

## Retrieval-practice ledger

**6 tagged items. Graded pool 34 (13 Bearings + 21 Practice). Rate = 17.6%, clearing B3's 15% rung for Chapter 4.** Chapter 4 is the first chapter to draw from two predecessors.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| kube-apiserver receives the request; etcd stores the object | ch 3 §2, §5 | **ch 4** — Practice Q1 |
| a controller acts on the difference between desired and current state | ch 3 §6 | **ch 4** — Practice Q2 |
| the Job controller tells the API server; it does not run Pods itself | ch 3 §6 | **ch 4** — Practice Q3 |
| desired/current state fields, and the component that stores the object | ch 3 §5–§6 | **ch 4** — Bearings #1 Q5 |
| five mechanisms for private-registry credentials | ch 2 §3 | **ch 4** — Bearings #2 Q4 |
| image immutability — build a new image, then recreate the container | ch 2 §2 | **ch 4** — Practice Q13 (distractor A) |
| the control loop; API server and etcd | ch 3 §5–§6 | **ch 4** — Soundings Q3, Q4 *(excluded from budget by B3)* |

**Theme obligations discharged and opened:**

- **✅ The control-loop theme's Chapter 4 obligation is met.** `concepts/control-loop.md` required Chapter 4 to "deliver the `spec` field as *the field that holds desired state*, and `status` as its counterpart." Chapter 4 §2 does exactly that, reproducing Chapter 3's forward-bearing text verbatim. **This is the first cross-cutting theme retrieval in the book to land.** Remaining: Ch 6, **Ch 11 (still unbeared)**, Ch 15, Ch 17.
- **Two of B3's nine themes originate here** (per `outline.md`'s own planning note): **namespaced-vs-cluster-scoped** (§3) and **labels/selectors as the universal join** (§5). The selector theme is beared forward to all four of its downstream chapters, which is exemplary — Chapter 3 missed two of its equivalent bearings.
- **⚑ Neither new theme gets a retrievable *name*.** B3's stated rationale for naming the absent-component pattern was that "naming it once and retrieving it by name turns four gotchas into one rule." Chapter 4 gives both themes ★ Fixed Points but no coinage. The Fixed Point sentences are the best available handles — *"Not everything lives in a namespace"* and *"the label selector is the core grouping primitive in Kubernetes"* — and are recorded as the canonical retrieval strings so Chapters 6, 9, 10, 11, and 12 retrieve one phrase rather than five paraphrases.

**⚑ Practice-section count error:** the section intro says *"**Five** test material from earlier chapters and are tagged as such."* There are 21 questions, correct, but only **four** tagged items in that section (Q1, Q2, Q3, Q13). Either tag a fifth or change the word.

**Forward commitments — both still OPEN:** #1 Ch 13 must retrieve Ch 8's version skew (Chapter 1 promised this to the reader in prose). #2 Ch 11 must retrieve the control loop, and no chapter bears forward to it yet.

---

## Operator notes

1. **This stage could not write, and neither could the two before it — but the diagnosis has changed.** `Write` and `Bash` were both denied here. More importantly: **`=== WRITE` appears exactly once in the whole `certcomp` repo — in the Stage 14 prompt template that asks for it.** Nothing parses these blocks. Chapter 1's and Chapter 3's artifacts were never going to land regardless of permissions. A materializer is below; it is ~30 lines and replays all three manifests losslessly.
2. **Recovery order matters.** ch-01 blocks → ch-03 blocks → ch-04 blocks. Chapter 3's manifest writes *full merged* `glossary.md`, `objective-coverage.md`, and `retrieval-log.md` (Ch 1 + Ch 3); Chapter 4's are appends. Running them out of order silently discards Chapter 4's contributions.
3. **Chapter 4 shipped without a fact-accuracy gate.** That outranks everything else in this manifest.
4. **Append-only has a cost, stated plainly.** Three rows in Chapter 3's existing tables need *editing*, not appending — `Lease`'s owner, `kube-system`'s reserved status, and `declarative vs imperative`'s reserved status. They are recorded in the append block under "Status changes to existing rows" for the reconcile pass. A future Stage 14 that can write in place should apply them.

---

### Materializer (author runs once; replaces the missing parser)

```python
# save as certcomp/tools/replay_kb_blocks.py, then: python tools/replay_kb_blocks.py
import re, sys
from pathlib import Path
sys.stdout.reconfigure(encoding="utf-8")

BOOK = Path(r"C:\dev\lodestar\Book-KCNA")
MANIFESTS = [BOOK / ".pipeline-state" / c / "kb-manifest.md"
             for c in ("ch-01", "ch-03", "ch-04")]          # order is load-bearing

WRITE  = re.compile(r"^=== WRITE (?P<p>.+?) ===\r?\n(?P<b>.*?)^=== END WRITE ===\r?$",
                    re.MULTILINE | re.DOTALL)
APPEND = re.compile(r"^=== APPEND (?P<p>.+?) ===\r?\n(?P<b>.*?)^=== END APPEND ===\r?$",
                    re.MULTILINE | re.DOTALL)

for man in MANIFESTS:
    if not man.exists():
        print(f"SKIP (absent): {man}"); continue
    text = man.read_text(encoding="utf-8")
    for rx, mode in ((WRITE, "w"), (APPEND, "a")):
        for m in rx.finditer(text):
            tgt = Path(m.group("p").strip().replace("/", "\\")).resolve()
            tgt.parent.mkdir(parents=True, exist_ok=True)
            body = m.group("b")
            if not body.endswith("\n"):
                body += "\n"
            with open(tgt, mode, encoding="utf-8", newline="\n") as fh:
                fh.write(body)
            print(f"{'WROTE ' if mode=='w' else 'APPEND'} {tgt.relative_to(BOOK)}")
```

---

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 4 additions — Records of Intent (2026-08-24)

**Appended, not merged.** This file is append-only under the current pipeline, so
Chapter 4's terms are grouped here rather than interleaved into the A–Z above.
Re-transcribing 500 lines of Chapter 1 and Chapter 3 prose to preserve one alphabet
would risk exactly the definitional drift Rule 5 forbids. Book assembly merges
alphabets mechanically.

Terms contributed: **41** — 34 defined · 5 partial · 2 status corrections.

## ⚑ Status changes to EXISTING rows above (apply at reconcile — cannot be done by append)

| Row | Current text | Correction | Evidence |
|---|---|---|---|
| Tier 3 · **Lease** | "Ch 5 / Ch 12" | **Ch 8** | `chapter-lineup.md` row 8 (B2, ratified): *"node lifecycle (…cordon/drain/uncordon, node conditions, **leases**)"*. Verified on disk 2026-08-24. Chapter 4 §3 bears to Ch 8 and is correct. |
| Tier 3 · **`kube-system` namespace** | reserved → Ch 4 | **CLOSED — defined at Ch 4 §3** | See Tier 1 below |
| Tier 3 · **declarative vs imperative** (Ch 1 list) | reserved → Ch 4 | **CLOSED — defined at Ch 4 §1** | See Tier 1 below |
| Tier 1 · **PodSpec** (⚑ Ch 4-vs-Ch 5 note) | "Chapter 3's prose needs the fix" | **RESOLVED by outcome** — Chapter 4 shipped and does not mention PodSpec once. Ledger's Ch 5 assignment confirmed; Chapter 3's prose is demonstrably wrong. | The shipped chapter |
| **8 × `⚑ SNAPSHOT NOT ON DISK`** (etcd, hub-and-spoke, addons, DNS entries) | flagged missing | **STRIKE ALL EIGHT.** `sources/` now holds 115 files, 28 dated 2026-08-24, including `k8s-docs-control-plane-node-communication-2026-08-24.md`, `k8s-docs-etcd-access-control-2026-08-24.md`, `k8s-docs-cluster-addons-2026-08-24.md`, `k8s-docs-dns-cluster-addon-2026-08-24.md`. | Directory listing, 2026-08-24 |

---

## Tier 1 — Defined at Chapter 4 (prose inherited verbatim)

### A

**annotation** — "You use annotations to attach **arbitrary non-identifying metadata** to
objects, and clients such as tools and libraries can retrieve it." The contrast that
defines it: "Labels can be used to select objects and to find collections of objects that
satisfy certain conditions. In contrast, annotations are **not used to identify and select
objects**." Keys follow the same two-segment rules as label keys; **values have no
character-set restrictions** (any string, including whitespace and structured data such as
JSON), with **all annotations on one object bounded to ≤ 256 KiB total**. Both keys and
values must be strings — not numbers, booleans, or lists.
[source: k8s-docs-annotations-2026-08-24] (Ch 4 §5)
> The chapter's one-sentence rule, worth keeping verbatim: **"If you might ever want to
> find objects by it, it is a label. If you only want to record it, it is an annotation."**

**`apiVersion`** — "which version of the Kubernetes API you're using to create this
object." Effectively: which schema the rest of the document is parsed under. Per-object,
not per-file, because one file may hold several kinds and resource types are versioned
independently. [source: k8s-docs-objects-2026-08-23] (Ch 4 §2)

### B

**base64 encoding** — "Base64 encoding is *not* an encryption method, it provides no
additional confidentiality over plain text."
[source: k8s-docs-secrets-good-practices-2026-08-24] (Ch 4 §4, planted Soundings Q6)
> Practical consequence the chapter states: encoding does not make a Secret manifest safe
> to commit. "It only makes the file *look* safe to commit, which is worse."

### C

**cluster-scoped object** — an object to which namespace scoping does not apply. "Namespace-
based scoping is applicable **only for namespaced objects** (Deployments, Services, and so
on) and **not for cluster-wide objects**, such as StorageClasses, Nodes, and
PersistentVolumes… namespace resources are not themselves in a namespace."
[source: k8s-docs-namespaces-2026-08-23] (Ch 4 §3)
> ★ Fixed Point wording: **"Not everything lives in a namespace."** Recorded as the
> canonical retrieval string for B3's namespaced-vs-cluster-scoped theme. See
> `concepts/cluster-scoped-resource.md`.

**ConfigMap** — "an API object used to store **non-confidential** data in key-value pairs.
Pods can consume ConfigMaps as environment variables, command-line arguments, or as
configuration files in a volume. A ConfigMap allows you to decouple environment-specific
configuration from your container images, so that your applications are easily portable."
[source: k8s-docs-configmap-2026-08-23] (Ch 4 §4)

**ConfigMap — immutability** — "Starting from v1.19 you can add an `immutable` field to a
ConfigMap definition. Once a ConfigMap is marked as immutable, **it is not possible to
revert this change**, nor to mutate the contents of its `data` or `binaryData` fields. You
can only delete and recreate the ConfigMap." [source: k8s-docs-configmap-2026-08-23]

**ConfigMap — size ceiling** — "A ConfigMap is not designed to hold large chunks of data;
the data stored in a ConfigMap cannot exceed **1 MiB**." For more, "mount a volume, or use
a separate database or file service." [source: k8s-docs-configmap-2026-08-23]

**ConfigMap — the four consumption paths** — "inside a container command and args; as
environment variables for a container; as a file in a read-only volume for the application
to read; or by writing code that runs inside the Pod and uses the Kubernetes API to read
the ConfigMap. **For the first three methods, the kubelet uses the data from the ConfigMap
when it launches the container(s) for a Pod. The fourth method lets the application
subscribe to updates whenever the ConfigMap changes.**"
[source: k8s-docs-configmap-2026-08-23]

**current state** — *(Chapter 3 defined this at the loop level; Chapter 4 gives it a
field.)* See **`status`**.

### D

**declarative interface** — "one where you declare the desired state of your resource, and
a controller keeps the current state of objects in sync with your declared desired state."
[source: k8s-docs-custom-resources-2026-08-23] (Ch 4 §1)
> **CLOSES Chapter 1's reservation** ("declarative vs imperative → Ch 4", first surfaced
> Ch 1 Soundings Q5).

**declarative object configuration** — the management technique in which "the user operates
on configuration files stored locally, but **does not define the operations to be taken on
them.** Create, update, and delete operations are automatically detected per-object by
`kubectl`." Operates on directories of files; recommended for production; supports 1+
writers. [source: k8s-docs-object-management-2026-08-24] (Ch 4 §1)

**desired state** — See **`spec`**.

**`kubernetes.io/dockerconfigjson`** — the Secret type holding a "Serialized
`~/.docker/config.json` file"; the object behind `imagePullSecrets`.
[source: k8s-docs-secret-2026-08-23] [source: k8s-docs-images-2026-08-23] (Ch 4 §4)
> **CLOSES Chapter 2's open loop** at ch02:459, which listed five ways to reach a private
> registry and deferred the most common one to this section.

### F

**field selector** — selects "on an object's field values rather than its labels."
*Partial: Chapter 4 gives it one parenthetical gloss and explicitly marks it as
non-load-bearing.* [source: k8s-docs-objects-2026-08-23]
(Surfaced Ch 4 §5 · ⚑ **no owner chapter assigned in B2 — needs one**)

### I

**imperative commands** — the management technique in which "a user operates directly on
live objects in a cluster, providing operations to `kubectl` as arguments or flags."
Named by the documentation as "the recommended way to get started or to run a one-off task
in a cluster." The stated cost: because it operates directly on live objects, "**it provides
no history of previous configurations**."
[source: k8s-docs-object-management-2026-08-24] (Ch 4 §1)

**imperative interface** — "one where you instruct the server what to do."
[source: k8s-docs-custom-resources-2026-08-23] (Ch 4 §1)

**imperative object configuration** — the management technique in which "the command
specifies the operation (`create`, `replace`, and so on), optional flags, and at least one
file name. The file must contain a full definition of the object in YAML or JSON."
Operates on individual files; recommended for production; supports **1** writer.
[source: k8s-docs-object-management-2026-08-24] (Ch 4 §1)
> ⚠ **The rule that binds all three techniques:** "A Kubernetes object should be managed
> using only one technique. Mixing and matching techniques for the same object results in
> **undefined behavior**." [source: k8s-docs-object-management-2026-08-24]

### K

**`kind`** — "what kind of object you want to create." Determines the internal shape of
`spec`. [source: k8s-docs-objects-2026-08-23] (Ch 4 §2)

**`kube-node-lease`** — one of the four initial namespaces. "Holds the Lease objects
associated with each node. Node leases allow the kubelet to send heartbeats so that the
control plane can detect node failure."
[source: k8s-docs-namespaces-2026-08-23] (Ch 4 §3 · Leases **Ch 8**)

**`kube-public`** — one of the four initial namespaces. "Readable by all clients, including
those not authenticated. Mostly reserved for cluster usage, for resources that should be
visible and readable publicly throughout the whole cluster."
[source: k8s-docs-namespaces-2026-08-23] (Ch 4 §3)
> ⚠ **"The public aspect of this namespace is only a convention, not a requirement."**
> Preparation material routinely states it as an enforced property. It is not. Do not
> harden this downstream — this is the same class of precision as Chapter 3's *"ideally*
> only the API server should have access to etcd."

**`kube-system`** — one of the four initial namespaces. "The namespace for objects created
by the Kubernetes system." [source: k8s-docs-namespaces-2026-08-23] (Ch 4 §3)
> **CLOSES Chapter 3's reservation** (surfaced Ch 3 Bearings #1 Q3 as a distractor).

**`kubectl api-resources`** — lists resource types; `--namespaced=true` and
`--namespaced=false` partition them by scope, authoritatively for the cluster you are on,
including types installed by operators. *Partial: Chapter 4 shows the usage, not the
command's full surface.* [source: k8s-docs-namespaces-2026-08-23]
(Surfaced Ch 4 §3 · full treatment **Ch 8**)

**`kubectl apply`** — "applies a configuration change to a resource from a file or standard
input." *Partial by design: Chapter 4 states outright that this one clause is the entire
treatment `apply` gets there.* [source: k8s-docs-kubectl-overview-2026-08-23]
(Surfaced Ch 4 §1–§2 · full treatment **Ch 8**)

**`kubectl exec`** — "executes a command inside a running container." Named in Chapter 4
only as an example of a command with no declarative reading at all.
[source: k8s-docs-kubectl-overview-2026-08-23] (Ch 4 §1 · full treatment **Ch 8 / Ch 16**)

**`kubectl explain`** — "gets documentation for resources." *Partial.*
[source: k8s-docs-kubectl-overview-2026-08-23] (Surfaced Ch 4 §2 · full treatment **Ch 8**)
> The chapter's framing is worth preserving: the four top-level fields are the map,
> `kubectl explain` is how you read the territory inside `spec` for a resource type you
> have not memorized — "which at associate tier is most of them, and that is fine."

**`kubectl scale`** — "updates the size of a workload."
[source: k8s-docs-kubectl-overview-2026-08-23] (Ch 4 §1, §6 · full treatment **Ch 8**)
> Load-bearing for the chapter's Zenith: it *edits a number in a `spec`* and a controller
> does the rest. See `concepts/declarative-configuration.md` § The honest correction.

### L

**label** — "key/value pairs that are attached to objects. Labels are intended to be used
to specify identifying attributes of objects that are meaningful and relevant to users,
but that **do not directly imply semantics to the core system.** They can be used to
organize and to select subsets of objects. Labels can be attached to objects at creation
time and subsequently added and modified at any time. Each object can have a set of
key/value labels defined, and each key must be unique for a given object."
[source: k8s-docs-labels-selectors-2026-08-23] (Ch 4 §5)

**label — syntax** — keys have two segments: an optional prefix and a required name. The
**name segment must be ≤ 63 characters**, beginning and ending alphanumeric, with dashes,
underscores, dots, and alphanumerics between. The **prefix, if present, is a DNS subdomain
≤ 253 characters** followed by a slash. **`kubernetes.io/` and `k8s.io/` are reserved for
Kubernetes core components.** **Values must be ≤ 63 characters and may be empty.**
[source: k8s-docs-labels-selectors-2026-08-23]

**label selector** — ★ **Fixed Point.** "**The label selector is the core grouping
primitive in Kubernetes.**" Via a label selector, a client or user can identify a set of
objects. [source: k8s-docs-labels-selectors-2026-08-23] (Ch 4 §5)
> **Canonical retrieval string. Do not paraphrase.** B3 tracks labels/selectors as one of
> its nine cross-cutting themes, originating here. See `concepts/label-selector.md`.

**label selector — equality-based** — uses `=`, `==`, and `!=`. Example:
`environment = production`, `tier != frontend`.
[source: k8s-docs-labels-selectors-2026-08-23]

**label selector — set-based** — uses `in`, `notin`, and `exists` (plus negation). Example:
`environment in (production, qa)`, `partition`, `!partition`. Set-based requirements are
"**more expressive** than equality-based ones," and multiple requirements are **ANDed**
together with commas — a rule that applies to *both* selector types.
[source: k8s-docs-labels-selectors-2026-08-23]

### M

**manifest** — the file in which you write an object. "Most often you provide that
information to `kubectl` in a file known as a **manifest**, and by convention, manifests
are YAML." [source: k8s-docs-objects-2026-08-23] (Ch 4 §2)

**`matchLabels` / `matchExpressions`** — the two structured selector fields supported by
Job, Deployment, ReplicaSet, and DaemonSet. **"`matchLabels` is a map of `{key, value}`
pairs equivalent to a `matchExpressions` entry with operator `In`."** The set-based
operator vocabulary is `In`, `NotIn`, `Exists`, `DoesNotExist`.
[source: k8s-docs-labels-selectors-2026-08-23] (Ch 4 §5)
> `matchLabels` is **shorthand, not a weaker feature.** The equivalence is exact and is
> the kind of checkable fact this exam rewards.

**`metadata`** — "data that helps uniquely identify the object, including a name string, a
UID, and an optional namespace." Also the home of labels and annotations.
[source: k8s-docs-objects-2026-08-23] (Ch 4 §2)

### N

**name (object)** — "a client-provided string that refers to an object in a resource URL.
Only one object of a given kind can have a given name at a time, but **if you delete the
object, you can make a new one with the same name.**" Names are reusable by design.
[source: k8s-docs-names-and-uids-2026-08-24] (Ch 4 §2)

**namespace** — "In Kubernetes, namespaces provide a mechanism for isolating groups of
resources within a single cluster. **Names of resources need to be unique within a
namespace, but not across namespaces.**"
[source: k8s-docs-namespaces-2026-08-23] (Ch 4 §3)
> Two structural constraints, both testable: **namespaces cannot be nested inside one
> another**, and **each Kubernetes resource can only be in one namespace.**
>
> Guidance the chapter is careful to reproduce at its documented strength: namespaces are
> "intended for use in environments with many users spread across multiple teams, or
> projects. For clusters with a few to tens of users, **you should not need to create or
> think about namespaces at all.**" And: it is **not** necessary to use multiple
> namespaces to separate slightly different resources such as different versions of the
> same software — "use labels to distinguish resources within the same namespace."

**namespaced object** — an object to which namespace scoping applies (Deployments,
Services, ConfigMaps, Secrets, ServiceAccounts, and most other resources).
[source: k8s-docs-namespaces-2026-08-23] (Ch 4 §3)

### O

**`Opaque`** — "Arbitrary user-defined data — **the default** Secret type."
[source: k8s-docs-secret-2026-08-23] (Ch 4 §4)

### R

**record of intent** — the documentation's own name for a Kubernetes object, and this
chapter's title. See **Kubernetes object**.

### S

**Secret** — "an object that contains a small amount of sensitive data such as a password,
a token, or a key. Such information might otherwise be put in a Pod specification or in a
container image; using a Secret means you don't need to include confidential data in your
application code. **Secrets are similar to ConfigMaps but are specifically intended to hold
confidential data.**" [source: k8s-docs-secret-2026-08-23] (Ch 4 §4)

**Secret — default storage posture** — "Kubernetes Secrets are, by default, stored
**unencrypted** in the API server's underlying data store (etcd). Anyone with API access
can retrieve or modify a Secret, and so can anyone with access to etcd. Additionally,
**anyone who is authorized to create a Pod in a namespace can use that access to read any
Secret in that namespace** — this includes indirect access such as the ability to create a
Deployment." [source: k8s-docs-secret-2026-08-23]
> ★ Fixed Point wording: **"Neither object encrypts anything."** What a Secret adds is
> *handling* — a distinct object type, a distinct access-control surface, and a defined
> place to attach encryption at rest. "The difference between the two is intent and
> treatment, not cryptography."

**Secret — type** — a field that exists to "facilitate programmatic handling of secret
data." Built-in types: `Opaque`, `kubernetes.io/service-account-token`,
`kubernetes.io/dockercfg`, `kubernetes.io/dockerconfigjson`, `kubernetes.io/basic-auth`,
`kubernetes.io/ssh-auth`, `kubernetes.io/tls`, `bootstrap.kubernetes.io/token`.
[source: k8s-api-ref-secret-v1-2026-08-24] [source: k8s-docs-secret-2026-08-23] (Ch 4 §4)

**`kubernetes.io/service-account-token`** — "ServiceAccount token (a legacy long-lived
credential)." Since v1.22 the recommended approach is short-lived, automatically rotating
tokens obtained through the TokenRequest API.
[source: k8s-docs-secret-2026-08-23] [source: k8s-docs-service-accounts-2026-08-23]
(Named Ch 4 §4 · identity model **Ch 5 / Ch 12**)

**`spec`** — "what state you desire for the object." "For objects that have a spec, you
have to set this when you create the object, providing a description of the characteristics
you want the resource to have: its desired state."
[source: k8s-docs-objects-2026-08-23] (Ch 4 §2)

**`status`** — "describes the current state of the object, **supplied and updated by the
Kubernetes system and its components.** The Kubernetes control plane continually and
actively manages every object's actual state to match the desired state you supplied."
[source: k8s-docs-objects-2026-08-23] (Ch 4 §2)
> ★ **Fixed Point — the book's most reused sentence, per the chapter's own account:**
> **"`spec` is what you want. `status` is what is. You write `spec`. The system writes
> `status`. Every controller in the cluster exists to close the distance between them."**
>
> Corollary Chapter 13 depends on: **a gap between `spec` and `status` is the normal
> condition while the system reconciles, not a fault.** Do not let this drift.

### U

**UID** — "a system-generated string… Every object created over the whole lifetime of a
Kubernetes cluster has a distinct UID," and it is "**intended to distinguish between
historical occurrences of similar entities.**" Not reusable.
[source: k8s-docs-names-and-uids-2026-08-24] (Ch 4 §2)
> Load-bearing for Chapter 5: a replaced Pod carries the same name and **a different UID**
> [source: k8s-docs-pod-lifecycle-2026-08-23]. Chapter 4's closing page plants this
> deliberately.

### Y

**Kubernetes object** — "**persistent entities** in the Kubernetes system," used to
represent cluster state: what containerized applications are running and on which nodes,
the resources available to them, and the policies around their behavior (restart policies,
upgrades, fault tolerance). "A Kubernetes object is a **'record of intent'** — once you
create the object, the Kubernetes system will **constantly** work to ensure that the object
exists." [source: k8s-docs-objects-2026-08-23] (Ch 4 §1)
> Four required top-level fields, every object, every time: `apiVersion`, `kind`,
> `metadata`, `spec`. Not a starting subset extended for advanced resources — the complete
> structural vocabulary. See `concepts/kubernetes-object.md`.

---

## Tier 3 — Reserved at Chapter 4 (surfaced, NOT defined — no prose written)

| Term | Defining chapter | First surfaced | Note |
|---|---|---|---|
| **Pod** | Ch 5 | Ch 1 §1 · used **~80×** in Ch 4 | ⚑ See below — worse than at Chapter 3 |
| **Deployment / ReplicaSet** | Ch 6 | Ch 4 §2 (docs' own worked example) | ✅ explicit parenthetical deferral given |
| **DaemonSet / Job** | Ch 6 | Ch 4 §5 (`matchExpressions` support list) | name-dropped |
| **StatefulSet** | Ch 6 / Ch 11 | Ch 1 §5 | not surfaced in Ch 4 |
| **Service** | Ch 9 | Ch 4 §3, §5 | ✅ beared |
| **cluster DNS / FQDN form** | Ch 9 | Ch 4 §3 | ✅ beared, deliberately one sentence deep |
| **NetworkPolicy** | **Ch 10** | Ch 4 §2, §5 | ✅ beared — **and Ch 4 is the correct party**; `chapter-02:871` points at Ch 9 and is wrong |
| **PersistentVolume / StorageClass** | Ch 11 | Ch 4 §3, Fixed Point, Q7 | ⚑ **no bearing given** — used as the canonical cluster-scoped examples |
| **volume / `subPath`** | Ch 11 | Ch 4 §4 | ✅ beared |
| **ServiceAccount** | Ch 5 (planted) / Ch 12 (full) | Ch 3 §2 · Ch 4 §4, Bearings #2 Q1 | partial — §4 bears to Ch 5 §6, but Bearings #2 Q1 answer C asserts a ServiceAccount fact with no bearing |
| **RBAC / Role / ClusterRole / RoleBinding / ClusterRoleBinding** | Ch 12 | Ch 4 §3, §5 | ✅ beared — **and §5 records the exception: RBAC does *not* select by label** |
| **encryption at rest** | Ch 12 | Ch 4 §4 | ✅ beared |
| **TokenRequest API** | Ch 12 | Ch 4 §4 | ✅ beared |
| **ResourceQuota** | Ch 8 | Ch 4 §3 | ✅ beared |
| **Lease** | **Ch 8** | Ch 3 Bearings #1 Q4 · Ch 4 §3 | ⚑ **corrects Ch 3's ledger row** — see Status changes above |
| **node conditions / heartbeats** | Ch 8 | Ch 4 §3 | ✅ beared |
| **custom resource / operator / CRD** | Ch 6 | Ch 4 §2, Bearings #1 Q1 | ⚑ **no bearing given** — `kind: CronTab` "from some vendor's operator" is load-bearing for the transferability claim |
| **node labels / `nodeSelector` / affinity** | Ch 7 | Ch 4 §5 | ✅ beared |
| **twelve-factor app** | Ch 15 | Ch 4 §4 | ✅ beared |
| **field selector** | ⚑ **no owner in B2** | Ch 4 §5 | See Tier 1 partial |
| **reconciliation** | ⚑ **still open** | Ch 3 §6 promise · Ch 4 uses the word family 3× | ⚑ See below |

> ⚑ **`Pod` is now the book's most-used undefined primitive, and the gap widened.**
> Chapter 3's ledger recorded ~40 uses with the deferral never restated. Chapter 4 uses it
> **roughly 80 times** — the scheduler assigns Pods, controllers create Pods, a Pod
> references a ConfigMap, a Pod-creation permission is a Secrets question — and restates
> the deferral only in *The Voyage Ahead*, on the last page. Chapter 2 set the reader up
> correctly at ch02:318 ("It is Chapter 5's whole subject"). **The fix is the same one
> Chapter 3's ledger already recommended and nobody applied: one sentence at first use.**
> This ledger writes no definition (Rule 5).

> ⚑ **`reconciliation` — Chapter 3's promise came due at Chapter 4 and was not paid.**
> Chapter 3 §6 told the reader: *"when later chapters say **reconciliation**, this
> closing-the-gap work is exactly what the word names."* Chapter 4 is the first later
> chapter. It uses "reconciler" (Soundings A3), "reconciles" (Bearings #1 Q3 answer), and
> "reconciliation direction" (§2 figure caption) — and never names the term. §2 and §6
> both already *describe* the behavior; one appositive closes it. **B3 runs this theme
> through Ch 6, 11, 15, and 17. The word must be retrievable well before then.**

---

## Rule 6 — canon conflicts carried into Chapter 4's shards

No shard was overwritten (none of the ten existed). Conflicts recorded loudly inside the
shards that later chapters will read:

1. **`Lease` ownership** — three-way, settled by B2 in Chapter 8's favor. Evidence line
   quoted in `concepts/namespace.md` so Chapter 5's and Chapter 12's Stage 14 do not
   re-litigate it.
2. **Convention 5 broken.** Chapter 3's ledger proposed *"No `§N` in cross-bearings that
   point into undrafted chapters"* and followed it 18 times out of 20. Chapter 4 pins
   §-numbers into **eleven** undrafted chapters, **fifteen** times. Never ratified, so this
   is a governance call rather than a defect — but it is the direct cause of item 3.
3. **§N reservation register — now three-deep on two targets.** Recorded in
   `concepts/cluster-scoped-resource.md` (which carries the Ch 12 bearings) and
   `concepts/label-selector.md` (which carries the Ch 6 and Ch 9 ones):

   | Target | Claimed by | For |
   |---|---|---|
   | **Ch 12 §2** | ch 2 (L393) / ch 4 | signing & attestation · why RBAC names subjects instead of selecting them |
   | **Ch 12 §3** | ch 2 (L459) / ch 4 | restricting who can pull what · deriving Role/ClusterRole/RoleBinding/ClusterRoleBinding |
   | **Ch 12 §4** | ch 2 (L813) / ch 4 | runtime protection for compute · hardening Secrets |
   | **Ch 6 §3** | ch 1 (L435) / ch 2 (L600) / ch 4 | StatefulSets · CRDs · a controller's selector and the Pods it owns |
   | **Ch 9 §4** | ch 2 (L871) / ch 4 | NetworkPolicy · cluster DNS and FQDNs — **Ch 4 is right; B2 row 10 puts NetworkPolicy in Ch 10** |

   Cheapest resolution consistent with the proposed convention: demote Chapter 4's forward
   bearings to bare `Ch N` and let each target chapter's outline assign its own numbers.
   That also stops Chapter 5 from adding a fourth claim to `Ch 6 §3`.
4. **NEW canonical caution, not a conflict — RBAC is the exception to the selector rule.**
   Chapter 4 §5 teaches that nearly every *"which objects does this apply to?"* question is
   answered by a selector over labels, then states the exception explicitly: Kubernetes'
   permission model "names its subjects and its resources explicitly; it does not select
   them by label" [source: k8s-docs-rbac-2026-08-23]. Recorded in
   `concepts/label-selector.md` because a reader — or a later chapter — who generalizes the
   Fixed Point without the exception makes a confident wrong prediction in Chapter 12.
=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubernetes-object.md ===
# Concept: The Kubernetes object

**Home:** Chapter 4 §1–§2 · **Competency:** D1.1 · **Status:** canonical
**Depth here:** the structural vocabulary every later chapter reads through.

## The definition (verbatim)

> Kubernetes objects are **persistent entities** in the Kubernetes system. Kubernetes uses
> these entities to represent the state of your cluster: what containerized applications
> are running and on which nodes, the resources available to those applications, and the
> policies around how those applications behave — restart policies, upgrades, and
> fault-tolerance.
>
> A Kubernetes object is a **"record of intent"** — once you create the object, the
> Kubernetes system will **constantly** work to ensure that the object exists.
> [source: k8s-docs-objects-2026-08-23]

Chapter 4's gloss on *constantly*, which is the whole chapter in one move: "Creating an
object is not a request that gets serviced and then completed. It is a statement that gets
**maintained**."

## The four fields — complete, not a starting subset

| Field | What it is | What it selects |
|---|---|---|
| `apiVersion` | "which version of the Kubernetes API you're using to create this object" | the schema |
| `kind` | "what kind of object you want to create" | what is being created |
| `metadata` | "data that helps uniquely identify the object, including a name string, a UID, and an optional namespace" | which specific instance |
| `spec` | "what state you desire for the object" | what it should look like |

Submit with `kubectl apply -f <manifest>`. [source: k8s-docs-objects-2026-08-23]

**The transferability claim, and why it is not marketing:** the structure does not vary by
resource type and does not expire. "A Pod manifest has those four fields. A NetworkPolicy
manifest has those four fields. A custom resource for a database operator that some vendor
shipped last week has those four fields."

## 🪢 Mnemonic (verbatim — it is a reading procedure, not an acronym)

> The four fields answer four questions, always in the same order. **Which API? Which kind
> of thing? Which one, specifically? What should it look like?** If you can hold those four
> questions, you can read any manifest, because reading a manifest is just answering them
> in order.

## The two halves of identity — and why Chapter 5 needs this

**Name:** "a client-provided string that refers to an object in a resource URL. Only one
object of a given kind can have a given name at a time, but if you delete the object, you
can make a new one with the same name." **Reusable by design.**

**UID:** "a system-generated string… Every object created over the whole lifetime of a
Kubernetes cluster has a distinct UID," and it is "**intended to distinguish between
historical occurrences of similar entities.**"
[source: k8s-docs-names-and-uids-2026-08-24]

That last phrase is planted, not decorative. Chapter 4's closing page cashes it: a Pod is
never rescheduled; if its node dies it is replaced by a near-identical Pod with **a
different UID** [source: k8s-docs-pod-lifecycle-2026-08-23]. "Same name, different object,
and the cluster knows the difference even when you don't." **Chapter 5 must retrieve this.**

## The apply round trip

`manifest.yaml` → `kubectl apply -f` → **kube-apiserver** writes the record → **etcd**
stores it → a controller **watches**, compares `spec` against `status`, acts on the
difference → reality changes → `status` is updated → it watches again, without terminating.

"Nothing in that path is a command… The object is the medium and the message both."

**The consequence worth carrying:** the controller does not receive a message from you or
from `kubectl`. It watches the API server. "This is why the same declaration can be applied
by a person at a terminal, a CI pipeline, or a tool that reconciles from a Git repository,
and the cluster behaves identically in all three cases. The cluster cannot tell the
difference and does not care." That indifference is the seam Chapter 15 opens.

## Figures

- `ch04-fig01-object-anatomy-spec-status` — the authorship boundary through the middle of
  the object. Four fields above it are yours; `status` below it is not. **The line is the
  content, not decoration.**
- `ch04-fig02-apply-round-trip` — one declaration in sequence over time. "The loop at the
  bottom never terminates. That is not a diagram convention; it is the actual behavior."

⚑ **Two open figure items carried from Stage 10 and still unresolved at Stage 13:** the
anchor `ch04-zenith-declaration-not-order` is malformed (missing the `fig{MM}` segment;
`image-specs.md` L14 proposes `ch04-fig06-declaration-not-order`), and figure numbering does
not follow document order (`fig01 → fig02 → fig04 → fig05 → fig03 → zenith`). Draft and
specs must change in the same pass or the join key breaks.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 5 | A Pod is an object with a spec; its `status` carries a **phase**. Must retrieve the UID rule — replacement, not repair. |
| Ch 6 | Deployment and ReplicaSet as the objects that hold intent surviving a disposable Pod. |
| Ch 8 | `kubectl` in full: the verbs, flags, and auth this chapter names and defers. |
| every later chapter | Reads *through* this one. A reader who can recite the four fields but cannot say what `status` is *for* will re-learn Chapter 4 four more times under exam pressure. |

## Related

[[spec]] · [[status]] · [[declarative-configuration]] · [[namespace]] · [[label-selector]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/declarative-configuration.md ===
# Concept: Declarative configuration, and the three management techniques

**Home:** Chapter 4 §1 and §6 · **Competency:** D1.1 · **Status:** canonical
**Closes:** Chapter 1's reserved term "declarative vs imperative"

## The two interfaces (verbatim)

> An **imperative** interface is one where you instruct the server what to do. A
> **declarative** interface is one where you declare the desired state of your resource,
> and a controller keeps the current state of objects in sync with your declared desired
> state. [source: k8s-docs-custom-resources-2026-08-23]

And the documentation's blunt statement of how far it goes — the same passage Chapter 3
quoted three times, now with a manifest attached:

> Kubernetes is not a mere orchestration system. In fact, it eliminates the need for
> orchestration… Kubernetes comprises a set of independent, composable control processes
> that continuously drive the current state towards the provided desired state.
> **It shouldn't matter how you get from A to C.** [source: k8s-docs-overview-2026-08-23]

## The three techniques

| Technique | Operates on | Recommended environment | Supported writers |
|---|---|---|---|
| **Imperative commands** | Live objects | Development projects | 1+ |
| **Imperative object configuration** | Individual files | Production projects | 1 |
| **Declarative object configuration** | Directories of files | Production projects | 1+ |

[source: k8s-docs-object-management-2026-08-24]

**Imperative commands** are not disparaged by the documentation — they are "the recommended
way to get started or to run a one-off task in a cluster." The cost is named precisely:
"because the technique operates directly on live objects, **it provides no history of
previous configurations**."

**Declarative object configuration** is the one the rest of the chapter assumes: the user
operates on local configuration files but "**does not define the operations to be taken on
them.** Create, update, and delete operations are automatically detected per-object."

## ⚠ The rule in the documentation's own alarmed voice

> **A Kubernetes object should be managed using only one technique. Mixing and matching
> techniques for the same object results in undefined behavior.**
> [source: k8s-docs-object-management-2026-08-24]

## 🔭 What actually differs between them: where the record lives

Not syntax. **Where the record of what you wanted lives.** With an imperative command it
lives only in the cluster — which is why the docs say the technique gives you no history.
With object configuration it lives in a file, "which can go into source control, be
reviewed before it is pushed, and serve as a template for the next object." The trade-off
is stated just as plainly in the other direction: object configuration "requires a basic
understanding of the object schema and the additional step of writing a YAML file."

## ★ The honest correction — preserve this, it is a Part 14 exemplar

Chapter 4's subtitle is a slogan, and §1 flags it as one before §6 audits it:

> `kubectl scale` updates the size of a workload, **which is to say it edits a number in a
> `spec`, and then something else notices.** The imperative command did not scale anything.
> It amended a record, and the loop did the rest.
>
> **The objects are declarations, and the imperative commands work by changing
> declarations.** That is the accurate claim, narrower than the chapter subtitle and better.

The chapter then names the kinship explicitly: "It is the same discipline Chapter 3 applied
to 'nobody is in charge': both statements are true in the way that matters and false if you
press them literally, and knowing which is which is the difference between understanding a
system and reciting a slogan about it."

**This is now a two-chapter pattern and should be treated as a series voice signature.**
Chapter 3 §7 disarmed its own chapter title; Chapter 4 §6 disarms its own subtitle. Later
chapters with quotable titles (Ch 12 *"RBAC has no deny rule, and Secrets aren't
encrypted"*; Ch 15 *"GitOps is the control loop you already learned"*) should carry the
same audit. Nominated to `voice-exemplars.md`; author ratifies.

## What the architecture buys, per §6

Three properties, and the chapter is careful to state them as consequences rather than
slogans: **idempotency** (the same description applied twice describes the same world, so
there is nothing to correct), **state-independence** (you can say what should be true
without knowing what currently is — working out the difference is the system's job), and
**durability** (the description outlives the terminal session, the person, and the
incident). "Those three properties compose into something, and this book will spend a later
chapter on it. Not yet." → Chapter 15.

## Related

[[kubernetes-object]] · [[spec]] · [[status]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/spec.md ===
# Concept: `spec` — the field that holds desired state

**Home:** Chapter 4 §2 · **Competency:** D1.1 · **Status:** canonical
**Discharges:** the obligation `concepts/control-loop.md` placed on Chapter 3 → Chapter 4.

## Definition (verbatim)

> **`spec`**: what state you desire for the object. For objects that have a spec, you have
> to set this when you create the object, providing a description of the characteristics
> you want the resource to have: its desired state.
> [source: k8s-docs-objects-2026-08-23]

## The handoff from Chapter 3 — reproduce it, do not paraphrase

Chapter 3 §6 taught the control loop and **deliberately withheld the field's name**,
closing with a forward bearing. Chapter 4 §2 opens by naming the debt — "Chapter 3 owed you
something. This is where it comes due" — and reproduces Chapter 3's forward-bearing text
**verbatim**: *"those objects carry a field that represents the desired state."*

Stage 13 rated this the strongest cross-chapter seam in the book so far. **It is a model
for every deferred-term handoff that follows.** The receiving chapter quoting the
promising chapter's exact words is what makes the payoff legible to a reader who read the
two chapters a week apart.

## The connection to the loop, in field names

Chapter 3: a controller compares desired state against current state and acts on the
difference [source: k8s-docs-controllers-2026-08-23].

Chapter 4: **desired state is `spec`; you wrote it. Current state is `status`; the system
wrote it. The difference between them is the thing every controller in the cluster exists
to close.**

The documentation's own worked example is the cleanest available and Chapter 4 uses it
as-is: a Deployment spec specifying three replicas; the system starts three and updates
status; one fails (*a status change*); the system responds to the difference by starting a
replacement [source: k8s-docs-objects-2026-08-23]. Chapter 4 takes the example **for its
shape only** and defers the resource to Chapter 6 with an explicit parenthetical — the
right handling of a borrowed example.

## What is NOT in Chapter 4

The internal shape of `spec` for any given `kind`. That is defined by `kind`, is different
for every resource, and is what `kubectl explain` is for. Chapter 4 is explicit that at
associate tier you will not have memorized most of them, "and that is fine."

## Related

[[status]] · [[kubernetes-object]] · [[control-loop]] · [[declarative-configuration]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/status.md ===
# Concept: `status` — the field the system writes

**Home:** Chapter 4 §2 · **Competency:** D1.1 · **Status:** canonical

## Definition (verbatim)

> The status describes the current state of the object, **supplied and updated by the
> Kubernetes system and its components.** The Kubernetes control plane continually and
> actively manages every object's actual state to match the desired state you supplied.
> [source: k8s-docs-objects-2026-08-23]

## ★ Fixed Point (verbatim — the book's most reused sentence)

> **`spec` is what you want. `status` is what is. You write `spec`. The system writes
> `status`. Every controller in the cluster exists to close the distance between them.**

Chapter 4 states its own reuse plan: Chapter 5 reads it against a Pod's phase, Chapter 6
against a replica count, Chapter 13 as the first thing you check when something is wrong.
**Learn it in that exact shape.**

## The asymmetry is the point

"A ship's log carries two kinds of entry, and they are never made by the same hand: what
the master intends, and what the watch actually observed. Both live in the same book.
Neither one is allowed to be written in the other's column."

## 🪝 Snag (verbatim)

> `status` is not something you write. You can type a `status` block into a manifest and
> apply it; the system will simply overwrite it with what is actually true. It is a report,
> not a request. Practitioners arriving from imperative tooling try this at least once,
> usually at two in the morning, while trying to make a stuck object look healthy.

*Nominated as a Part 14 subject-dignity exemplar: the wry beat lands on the practitioner's
own 3 a.m. self-deception, which is exactly the orientation skill v5.7 licenses.*

## ⚑ The corollary Chapter 13 depends on — do not let this drift

**A gap between `spec` and `status` is the normal condition while the system reconciles.
It is not a fault.**

Chapter 4's Bearings #1 Q3 exists to install this, and its answer key says why: "Continual
management implies there are moments when the states differ. That is not breakage; that is
the system working… a practitioner who reads every `spec`/`status` gap as a fault will
spend a lot of time investigating perfectly healthy clusters."

Chapter 13's whole subtitle is *"Read the phase before you read the logs."* If a later
chapter teaches gap-as-fault, Chapter 13 inherits a reader with exactly the wrong instinct.

## The word this shard cannot supply

⚑ Chapter 3 promised the reader that later chapters saying **"reconciliation"** would mean
this closing-the-gap work. Chapter 4 describes the behavior three times and never names the
word. **One appositive at the Fixed Point closes it.** See `glossary.md` § reconciliation.
Rule 5 forbids inventing the sentence here.

## Related

[[spec]] · [[kubernetes-object]] · [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespace.md ===
# Concept: Namespaces — a scope for names

**Home:** Chapter 4 §3 · **Competency:** D1.1 · **Status:** canonical

## Definition (verbatim)

> In Kubernetes, **namespaces** provide a mechanism for isolating groups of resources
> within a single cluster. **Names of resources need to be unique within a namespace, but
> not across namespaces.** [source: k8s-docs-namespaces-2026-08-23]

Chapter 4's compression: **a namespace is a scope for names.** "Two ships on two different
registries can carry the same name, and neither registry has to care."

## Two structural constraints, both testable

**Namespaces cannot be nested inside one another**, and **each Kubernetes resource can only
be in one namespace.** [source: k8s-docs-namespaces-2026-08-23]

> 🪝 **Snag:** the instinct to build a hierarchy comes from cloud IAM (management groups →
> subscriptions → resource groups) and from Linux control-group trees. The platform will
> not accommodate it. **There is exactly one level.**

## The restraint the documentation actually states

Preparation material tends to present namespaces as a maturity signal. The documentation
does not: they are "intended for use in environments with many users spread across
multiple teams, or projects. For clusters with a few to tens of users, **you should not
need to create or think about namespaces at all.** Start using them when you need the
features they provide." For production, the guidance is to **not** use `default` — "make
other namespaces and use those."

## ⚠ The correction most guides skip

> It is **not** necessary to use multiple namespaces to separate slightly different
> resources, such as different versions of the same software. **Use labels to distinguish
> resources within the same namespace.** [source: k8s-docs-namespaces-2026-08-23]

Chapter 4 §5 supplies the *why*, and it is the sharpest sentence in the chapter on this
topic: **"Namespaces partition *names*. Labels partition *sets*."** Nearly everything in
Kubernetes operates over sets — every controller, every Service, every policy — "so
partitioning by namespace when you meant to partition by set leaves the mechanism that
would have grouped your objects unable to see across the line you drew."

This is a documented instruction, not a stylistic preference. Preserve it as such.

## The four initial namespaces

| Namespace | What it is for |
|---|---|
| `default` | so you can start using a new cluster without first creating a namespace |
| `kube-system` | the namespace for objects created by the Kubernetes system |
| `kube-public` | readable by all clients including unauthenticated ones; mostly reserved for cluster usage |
| `kube-node-lease` | holds the Lease objects associated with each node, which let the kubelet send heartbeats so the control plane can detect node failure |

**Two details examiners like.**

1. **`kube-public` is a convention, not an enforcement.** "The public aspect of this
   namespace is only a convention, not a requirement." Preparation material routinely
   states it as a hard property. **Do not harden this downstream** — same class of
   precision as Chapter 3's *"ideally* only the API server should have access to etcd."
2. **`kube-node-lease` is the one people forget**, and it connects forward to node
   heartbeats and failure detection.

## ⚑ RULE 6 — `Lease` ownership, settled

Chapter 3's ledger recorded `Lease → Ch 5 / Ch 12`. Chapter 4 bears it to Chapter 8.
**B2 settles it in Chapter 8's favor**, verified on disk 2026-08-24:

> `chapter-lineup.md` row 8 — *"**D1.2** — kubectl syntax and verbs, kubeconfig… node
> lifecycle (cordon/drain/uncordon, node conditions, **leases**), semantic versioning…"*

Chapter 3's ledger row is stale and is corrected in `glossary.md`. **Chapter 5's and
Chapter 12's Stage 14 should not re-litigate this.**

## Deliberately shallow here

The Service DNS form `<service-name>.<namespace-name>.svc.cluster.local` gets exactly one
sentence's worth of treatment — enough to explain why a bare `<service-name>` resolves
locally and crossing namespaces needs the FQDN. What serves those records and how
resolution proceeds is **Chapter 9's**. ResourceQuota is named and handed to **Chapter 8**.
Both deferrals are beared correctly.

## Related

[[cluster-scoped-resource]] · [[label-selector]] · [[configmap]] · [[kubernetes-object]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cluster-scoped-resource.md ===
# Concept: Namespaced vs cluster-scoped

**Home:** Chapter 4 §3 · **Competency:** D1.1 · **Status:** canonical
**B3 classification:** one of nine cross-cutting themes — **originates here.**

## ★ Fixed Point (verbatim — this is the canonical retrieval string)

> **Not everything lives in a namespace.** Nodes, PersistentVolumes, and StorageClasses are
> cluster-scoped, and so are namespace objects themselves. Namespace scoping applies only
> to namespaced objects. **Any question about who may act on a resource has to start by
> asking which side of this boundary the resource is on.**
> [source: k8s-docs-namespaces-2026-08-23]

Documentation wording: "Namespace-based scoping is applicable **only for namespaced
objects** (Deployments, Services, and so on) and **not for cluster-wide objects**, such as
StorageClasses, Nodes, and PersistentVolumes… namespace resources are not themselves in a
namespace, and low-level resources such as nodes and persistent volumes are not in any
namespace."

## ⚑ USE ONE PHRASE. Chapter 4 did not coin a name.

B3's stated rationale for naming the absent-component pattern was that "naming it once and
retrieving it by name turns four gotchas into one rule." Chapter 4 gives this theme a
★ Fixed Point but **no coinage.**

**Until the author rules otherwise, `"Not everything lives in a namespace"` is the
canonical retrieval string.** Chapters 10, 11, and 12 should retrieve *that sentence*
rather than five paraphrases of it. If the author prefers a coined name, it must be chosen
before Chapter 10 drafts.

## The payoff, eight chapters out

Chapter 4 states the bearing and refuses to teach it: Kubernetes' permission model "has two
role types and two binding types, and the four combinations are **not a table to memorize.
They are a direct consequence of this boundary.** A permission over a namespaced resource
can be granted inside one namespace; a permission over a cluster-scoped resource cannot be,
because there is no namespace to grant it in."

**Chapter 12 must derive Role / ClusterRole / RoleBinding / ClusterRoleBinding from this
boundary rather than presenting a 2×2.** That is the whole reason Chapter 4 plants it.

## The precision that separates "all namespaces" from "no namespace"

Chapter 4's Practice Q10 distractor D asserts that cluster-scoped resources "belong to all
of them simultaneously." The answer key is the sentence to preserve: "**They belong to
none.** That distinction matters enormously for permissions, because 'in all namespaces'
and 'in no namespace' imply very different things about who can be granted access."

## ⚓ The lookup that beats memorization

`kubectl api-resources --namespaced=true` / `--namespaced=false` list them, and the answer
is authoritative for *your* cluster — including types installed by operators that did not
exist when the book was printed. "Run it twice and you will remember the short exam-relevant
list anyway, which is the pleasant thing about lookups: they teach you while you use them."

## Figure

`ch04-fig04-namespaced-vs-cluster-scoped` — two namespaces inside one cluster with
**identical resource names in both boxes** (legal and unremarkable), and four resource
types in the outer region that cannot be put inside either.

## ⚑ §N reservation collisions carried by this shard's bearings

Chapter 4 pins `Ch 12 §2`, `§3`, and `§4` for access-control topics. **Chapter 2 already
claimed all three** for supply-chain topics (ch2 L393, L459, L813). Both cannot hold;
Chapter 12's outline must pick, and one shipped chapter needs editing. Cheapest fix
consistent with Chapter 3's proposed convention: demote to bare `Ch 12`.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 10 | NetworkPolicy answers *"which Pods does this apply to?"* on both sides of a namespace line — selector **plus** scope. Chapter 4's Bearings #3 Q4 sets this up explicitly. |
| Ch 11 | PersistentVolume and StorageClass are the canonical cluster-scoped examples used throughout Chapter 4 — ⚑ **and Chapter 4 gives them no forward bearing.** Add one. |
| Ch 12 | **Derive** the four RBAC combinations from this boundary. Do not present them as a table. |

## Related

[[namespace]] · [[label-selector]] · [[secret]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/configmap.md ===
# Concept: ConfigMap

**Home:** Chapter 4 §4 · **Competency:** D1.1 · **Status:** canonical
**Prerequisite:** Chapter 2 §2 (image immutability)

## The problem before the object

One image, two environments, and images are immutable — "you do not change a running
container's code; you build a new image and recreate the container"
[source: k8s-docs-containers-2026-08-23]. "So if the two environments need different
settings, and the image cannot differ, the settings must live somewhere other than the
image."

The documentation's own framing: code reads `DATABASE_HOST`; locally it is `localhost`, in
the cloud it names a Service. One image, two values, neither in the image.
[source: k8s-docs-configmap-2026-08-23]

## Definition (verbatim)

> A **ConfigMap** is an API object used to store **non-confidential** data in key-value
> pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or
> as configuration files in a volume. A ConfigMap allows you to decouple environment-
> specific configuration from your container images, so that your applications are easily
> portable. [source: k8s-docs-configmap-2026-08-23]

## The four facts that carry weight

1. **Size ceiling: 1 MiB.** "A ConfigMap is not designed to hold large chunks of data."
   Past that: mount a volume, or use a separate database or file service.
2. **Same namespace.** "The Pod and the ConfigMap must be in the same namespace." This is
   §3's scope-for-names rule surfacing where you actually trip over it.
3. **Four consumption paths, and the asymmetry among them.** Command and args; environment
   variables; a file in a read-only volume; or code inside the Pod reading the Kubernetes
   API. **"For the first three methods, the kubelet uses the data from the ConfigMap when
   it launches the container(s) for a Pod. The fourth method lets the application subscribe
   to updates whenever the ConfigMap changes."**
4. **Immutability is a one-way door.** Since v1.19: "Once a ConfigMap is marked as
   immutable, **it is not possible to revert this change**, nor to mutate the contents of
   its `data` or `binaryData` fields. You can only delete and recreate the ConfigMap."

[all: source: k8s-docs-configmap-2026-08-23]

## 🪝 The day-one surprise

> You edited the ConfigMap. The running application did not notice… three of the four
> consumption paths are applied by the kubelet **at container launch**. Only the fourth,
> where your code reads the Kubernetes API itself, subscribes to changes. If you want the
> first three to pick up a change, something has to cause the containers to be launched
> again.

**The volume path is the most seductive miss** and Chapter 4's Bearings #2 Q3 answer keeps
the nuance honest: a volume *feels* live, and in some configurations projected file content
does eventually change on disk — but the application still has to be written to notice, and
**a container using a ConfigMap as a `subPath` volume mount will not receive updates at
all** [source: k8s-docs-volumes-2026-08-23]. "Treating 'it's a volume, so it's live' as a
rule will burn you." Chapter 11 owns the exception.

## The line that sets up the next section

> **ConfigMap does not provide secrecy or encryption.** If the data you want to store are
> confidential, use a Secret rather than a ConfigMap, or use additional third-party tools
> to keep your data private. [source: k8s-docs-configmap-2026-08-23]

Note the shape of immutability: the same replace-don't-mutate instinct that governs
container images, applied to configuration. Chapter 4's Practice Q13 uses this deliberately
as a Chapter 2 discrimination item.

## Forward pointer

"Store config in the environment" is the third of the twelve factors
[source: twelve-factor-app-2026-08-23] — a methodology that predates Kubernetes and that
these two objects implement almost exactly. **Chapter 15** names the connection; Chapter 4
beared it correctly and did not teach it.

## Related

[[secret]] · [[namespace]] · [[kubernetes-object]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/secret.md ===
# Concept: Secret — and exactly what it does not do

**Home:** Chapter 4 §4 · **Competency:** D1.1 (security posture → **D2.2, Ch 12**)
**Status:** canonical

## Definition (verbatim)

> A **Secret** is an object that contains a small amount of sensitive data such as a
> password, a token, or a key… **Secrets are similar to ConfigMaps but are specifically
> intended to hold confidential data.** [source: k8s-docs-secret-2026-08-23]

Chapter 4 reads the operative words carefully: *intended to hold*. "Intent is doing a great
deal of work in that sentence, and the documentation's very next block explains why."

## The posture, in the project's own words

> Kubernetes Secrets are, by default, stored **unencrypted** in the API server's underlying
> data store (etcd). Anyone with API access can retrieve or modify a Secret, and so can
> anyone with access to etcd. Additionally, **anyone who is authorized to create a Pod in a
> namespace can use that access to read any Secret in that namespace** — this includes
> indirect access such as the ability to create a Deployment.
> [source: k8s-docs-secret-2026-08-23]

## ★ Fixed Point (verbatim)

> **Neither object encrypts anything.** A ConfigMap provides no secrecy or encryption. A
> Secret's values are base64-*encoded*, which is not encryption and adds no confidentiality
> over plain text, and are stored *unencrypted* by default, readable by anyone with API
> access, etcd access, or the ability to create a Pod in the namespace. What a Secret adds
> is *handling*: a distinct object type, a distinct surface for access-control rules, and a
> defined place to attach encryption at rest. **The difference between the two is intent
> and treatment, not cryptography.**

## Base64 is not a lock

> Base64 encoding is *not* an encryption method, it provides no additional confidentiality
> over plain text. [source: k8s-docs-secrets-good-practices-2026-08-24]

Both halves stated by the project in one place: *"Secret values are encoded as base64
strings and are stored unencrypted by default, but can be configured to be encrypted at
rest."* **Encoded, not encrypted. Unencrypted by default, not unencryptable.**

Practical consequence: sharing or committing a base64-encoded manifest "means the secret is
available to everyone who can read the manifest. The encoding does not make the file safe
to commit. **It only makes the file *look* safe to commit, which is worse.**"

*(Chapter 4 plants this at Soundings Q6 — "Hold onto that answer; §4 will want it" — and
collects it in §4. The plant-and-collect is clean and worth copying.)*

## 🔭 The inverted intuition — this is the thread Chapter 12 picks up

"Can read Secrets" and "can create workloads" *are* separate permissions, and **granting
the second effectively grants the first**: a Pod you create can mount any Secret in its
namespace, and once mounted its contents are yours to print. "There is no way to create a
Pod without that being true, because handing Secrets to Pods is what Secrets are for."

**Permission to create Pods in a namespace is, in security terms, a Secrets question, and
nothing in the name of the permission says so.**

## Built-in types

`Opaque` (**the default** — arbitrary user-defined data) · `kubernetes.io/service-account-token`
· `kubernetes.io/dockercfg` · `kubernetes.io/dockerconfigjson` · `kubernetes.io/basic-auth`
· `kubernetes.io/ssh-auth` · `kubernetes.io/tls` · `bootstrap.kubernetes.io/token`
[source: k8s-docs-secret-2026-08-23]

The `type` field exists to "facilitate programmatic handling of secret data"
[source: k8s-api-ref-secret-v1-2026-08-24] — a signal to whatever reads the object, not a
constraint on what you may store.

**`kubernetes.io/dockerconfigjson` closes Chapter 2's open loop.** ch02:459 listed five ways
to reach a private registry and deferred the most common one here. An `imagePullSecret` is a
Secret of this type holding a serialized `~/.docker/config.json` — "the same credential file
your local tooling writes, filed as a cluster object"
[source: k8s-docs-images-2026-08-23]. **If a Pod cannot pull from a private registry, this
is the object that is missing or wrong.**

## ⚑ Deliberate restraint — do not "improve" this

The documentation names four steps for using Secrets safely: enable encryption at rest;
configure RBAC with least-privilege access; restrict Secret access to specific containers;
consider external Secret store providers [source: k8s-docs-secret-2026-08-23].

**Chapter 4 hands over all four and teaches none.** The chapter says why: "the material
above is alarming enough that the pull toward 'and here's how to fix it' is strong, but
Chapter 12 is where encryption at rest, least-privilege access rules, and the broader
security posture get the room they need."

A later editor's instinct will be to add a paragraph of mitigation here. **Don't.** Chapter
12's subtitle is *"RBAC has no deny rule, and Secrets aren't encrypted"* — this is its
material. Chapter 4's image for the boundary: "A Secret is a strongbox stowed in the same
hold as everything else. The lock is Chapter 12's; this chapter is only telling you the box
did not ship with one fitted."

## ⚑ Guardrail note for Chapter 12

Chapter 4's §4 is the densest fear-adjacent passage in the book so far, and it passes
Part 14 cleanly: **every alarming clause is tagged to Kubernetes' own documentation**, and
there are no invented breach scenarios. Chapter 12 handles the same material at greater
length. **Hold it to the same standard** — sourced alarm, no fabricated stakes.

## Related

[[configmap]] · [[cluster-scoped-resource]] · [[kubernetes-object]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/label-selector.md ===
# Concept: Labels and selectors — the universal join

**Home:** Chapter 4 §5 · **Competency:** D1.1 · **Status:** canonical
**B3 classification:** one of nine cross-cutting themes — **originates here.**

## ★ Fixed Point (verbatim — canonical retrieval string)

> **The label selector is the core grouping primitive in Kubernetes.** Labels are
> selectable. Annotations are not. Nearly every question in Kubernetes of the form *"which
> objects does this apply to?"* is answered by a selector over labels.
> [source: k8s-docs-labels-selectors-2026-08-23]

The middle phrase is the documentation's own title for the mechanism. **Retrieve it by
these words**, not by paraphrase — B3's rationale for naming a pattern applies here.

## Labels

> **Labels** are key/value pairs that are attached to objects… intended to be used to
> specify identifying attributes of objects that are meaningful and relevant to users, but
> that **do not directly imply semantics to the core system.**
> [source: k8s-docs-labels-selectors-2026-08-23]

Chapter 4's gloss on why the system's ignorance is the feature: "Kubernetes does not know
what `tier: frontend` means. It has no built-in concept of a frontend. That ignorance is
precisely why labels are useful everywhere: because the system attaches no meaning to them,
you are free to attach yours, and the system's grouping machinery works identically
regardless of what you meant. A label is closer to a signal flag than to a filing category."

**Syntax, at the depth this exam tests.** Name segment **≤ 63 characters**, alphanumeric at
both ends. Optional prefix: a **DNS subdomain ≤ 253 characters** followed by a slash.
**`kubernetes.io/` and `k8s.io/` are reserved for core components.** Values **≤ 63
characters**, may be empty.

## The two selector syntaxes

| Type | Operators | Example |
|---|---|---|
| **Equality-based** | `=` `==` `!=` | `environment = production`, `tier != frontend` |
| **Set-based** | `in` `notin` `exists` (+ negation) | `environment in (production, qa)`, `partition`, `!partition` |

Set-based requirements are "**more expressive**." **Commas AND multiple requirements
together — regardless of which selector type they use.** (Chapter 4's Practice Q17 is built
on exactly that trap: a comma makes an expression *look* set-based and tells you nothing
about the operators.)

**The structured form** — supported by Job, Deployment, ReplicaSet, and DaemonSet:
**"`matchLabels` is a map of `{key, value}` pairs equivalent to a `matchExpressions` entry
with operator `In`."** Exact equivalence; `matchLabels` is shorthand, not a weaker feature.
Set-based operator vocabulary: `In`, `NotIn`, `Exists`, `DoesNotExist`.

## ⚓ Worth Securing — why this shard matters more than its section

> ReplicaSet, Service, NetworkPolicy, and node affinity are **not four mechanisms to
> learn. They are one mechanism** — *describe a set by its attributes* — aimed at four
> problems. Learn the primitive once and you spend the later chapters learning what each
> resource *does* with its set, which is the interesting part.

## ⚑ THE EXCEPTION — record it, or Chapter 12 inherits a wrong prediction

**Kubernetes' permission model is not a selector.** RBAC "names its subjects and its
resources explicitly; it does not select them by label"
[source: k8s-docs-rbac-2026-08-23].

Chapter 4 places this immediately after the Fixed Point, deliberately, "because you have
just been told that everything is a selector." A reader — or a later chapter — that
generalizes without the exception "will make a specific, confident, wrong prediction in
Chapter 12."

*(Also noted, not load-bearing: Kubernetes has **field selectors**, which select on an
object's field values rather than its labels. Different thing, different syntax, not a
substitute. ⚑ B2 assigns no owner chapter — needs one.)*

## Figure

`ch04-fig03-labels-selectors-join` — four Pods, two label keys, four selectors resolving to
overlapping sets. Caption is load-bearing: "**sets, not a taxonomy.** Pod A belongs to two
selected sets at once and Pod D to none of them, and that overlap is the entire reason this
mechanism is useful. If the four Pods had partitioned cleanly into four boxes you would be
looking at a folder structure, not a selector."

## ⚑ §N reservation collisions carried by this shard's bearings

`Ch 6 §3` is now claimed **three ways** — Chapter 1 (L435, StatefulSets), Chapter 2 (L600,
CRDs), Chapter 4 (a controller's selector and the Pods it owns). `Ch 9 §4` is claimed by
Chapter 2 (L871, NetworkPolicy) and Chapter 4 (cluster DNS) — **Chapter 4 is right;** B2
row 10 puts NetworkPolicy in Chapter 10, and Chapter 3's ledger independently recorded the
same. `chapter-02:871` should be retargeted.

## Downstream obligations — all four already beared from Chapter 4

| Chapter | Obligation |
|---|---|
| Ch 6 | A ReplicaSet knows which Pods are *its* Pods by selector. |
| Ch 7 | Node scheduling constraints use labels on nodes; the recommended approaches all use label selectors [source: k8s-docs-assign-pod-node-2026-08-23]. |
| Ch 9 | A Service identifies its backends by selector — "what makes Pod churn survivable" [source: k8s-docs-service-2026-08-23]. |
| Ch 10 | NetworkPolicy selects **both its subject and its peers**, across a namespace boundary [source: k8s-docs-network-policies-2026-08-23]. |
| Ch 12 | **The exception.** Explain why RBAC names rather than selects. |

Chapter 4 bears forward to all four. **This is the model Chapter 3 missed twice** (Ch 11
control loop, Ch 10 NetworkPolicy). Copy this discipline, not Chapter 3's.

## Related

[[annotation]] · [[cluster-scoped-resource]] · [[namespace]] · [[kubernetes-object]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/annotation.md ===
# Concept: Annotations

**Home:** Chapter 4 §5 · **Competency:** D1.1 · **Status:** canonical

## Definition (verbatim)

> You use **annotations** to attach **arbitrary non-identifying metadata** to objects, and
> clients such as tools and libraries can retrieve it.
>
> Labels can be used to select objects and to find collections of objects that satisfy
> certain conditions. In contrast, annotations are **not used to identify and select
> objects.** [source: k8s-docs-annotations-2026-08-24]

## The one-sentence rule (verbatim — this is the whole distinction)

> **If you might ever want to find objects by it, it is a label. If you only want to record
> it, it is an annotation.**

"A build identifier that a deployment tool wants to select on is a label. A build
identifier that exists so a human can read it during an incident is an annotation. **Same
string, different job.**"

## The syntax difference is the rule restated as engineering

| | Label value | Annotation value |
|---|---|---|
| Character set | constrained: alphanumerics, dashes, underscores, dots | **no restrictions** — any string, incl. whitespace and structured data (JSON/YAML) |
| Length | ≤ 63 characters | no per-value cap; **all annotations on one object ≤ 256 KiB total** |
| Selectable | yes | **no** |

Keys follow the **same** two-segment rules in both cases, and `kubernetes.io/` / `k8s.io/`
are reserved for core components in both. Both keys and values must be **strings** — not
numbers, booleans, or lists.
[source: k8s-docs-labels-selectors-2026-08-23] [source: k8s-docs-annotations-2026-08-24]

Chapter 4's reading of the table, worth keeping: "**Labels are constrained *because* they
are indexed and selected on. Annotations are unconstrained *because* nothing has to search
them.**"

## What people actually put in them

The documentation's own list, which is the best answer to "like what?": build/release/image
information (timestamps, release IDs, git branch, PR numbers, image hashes, registry
addresses); pointers to logging, monitoring, analytics, or audit repositories; client
library or tool information for debugging; lightweight rollout-tool metadata; and phone or
pager numbers of responsible people, or a directory entry for the team's site.
[source: k8s-docs-annotations-2026-08-24]

**Notice the shape of that list.** Every item is something a human or a tool reads *after*
it has already found the object. None is something you would search on.

## ⚠ Two mistakes that are the same mistake

1. **Recording something as an annotation and then trying to select on it.** Not a
   capability gap — it is the definition of the two.
2. **Using a namespace to separate two versions of the same software.** "Namespaces
   partition *names*. Labels partition *sets*."

"Both errors are the same shape: **reaching for the wrong partitioning tool.** Learn the
shape, not the two facts."

## Related

[[label-selector]] · [[namespace]] · [[kubernetes-object]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 4 update (2026-08-24)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.1** | Chapter 3 *(cluster layer)* | deep | 2026-08-24 |
| **D1.1** | **Chapter 4** *(object layer)* | **deep** | **2026-08-24** |

**Registry row change:** `D1.1 | Kubernetes Core Concepts | Ch 3, 4, 5, 6` →
status becomes **"in progress — Ch 3 and Ch 4 covered 2026-08-24"**.

### Chapter 4 — D1.1 coverage detail

`kb_tags.objectives: ["D1.1"]`; all six sections carry `objectives: ["D1.1"]`. Authored
weight estimate **~6%**, disclosed inline with the correct caveat: the chapter states the
published figure (Kubernetes Fundamentals at 44%) and says plainly that CNCF publishes no
weights for individual competencies inside a domain. **That is the compliant pattern — it
names the published number, marks the estimate as the book's, and points at the front
matter for the derivation. Copy it.**

| Sub-topic | Depth |
|---|---|
| The object model; "record of intent"; the four required fields | deep |
| `spec` vs `status`, and the authorship asymmetry | **deep — discharges Chapter 3's forward promise** |
| Declarative vs imperative; the three management techniques | deep — **closes Chapter 1's reserved term** |
| Object name vs UID | moderate — **plants Chapter 5's replacement rule** |
| Namespaces; the four initial namespaces; no nesting | deep |
| Namespaced vs cluster-scoped | **deep — B3 theme, originates here** |
| ConfigMap: size, scope, four consumption paths, immutability | deep |
| Secret: types, base64, default storage posture | deep |
| Labels, selectors, `matchLabels` ≡ `matchExpressions`+`In` | **deep — B3 theme, originates here** |
| Annotations, and the label/annotation rule | deep |
| Pod as a primitive | **still deferred to Ch 5** (⚠ used ~80× here, undefined) |
| PodSpec | **deferred to Ch 5 — confirmed by outcome; Ch 4 does not mention it** |
| Secret hardening / encryption at rest / RBAC | **deliberately deferred to Ch 12** |
| `kubectl` command surface | **deliberately deferred to Ch 8** |

---

## ⚑ Book-level fact to correct in the chapter

Chapter 4's Safe Harbor reads **"Chapter 4 of 15 complete."** The book has **20 chapters**
— `chapter-lineup.md` runs to row 20 (`Full Mock Exam`), with row 19 the synthesis chapter.
Verified on disk 2026-08-24. Chapters 1 (L376) and 3 (L950) both reference Chapter 17 by
name, so the figure is contradicted by shipped text as well as by the plan.

---

## ⚑ Ethical-guardrail status — Chapter 4

| Chapter | Guardrail #8 (frequency claims) | Note |
|---|---|---|
| Ch 1 | pass | |
| Ch 2 | pass | models the compliant phrasing |
| Ch 3 | **FAIL — open** | six unverifiable exam-frequency assertions |
| **Ch 4** | **BORDERLINE — five prevalence superlatives** | see below |

Chapter 4 avoids Chapter 3's specific failure mode — it makes **no** "frequently tested" or
"cheap points on exam day" claims about exam behavior. What it does carry are five
**practitioner-prevalence** superlatives stated as fact:

- §4 — "the single most common day-one surprise with ConfigMaps"
- §4 — "This pair produces more confident wrong answers than anything else in this chapter"
- Safe Harbor — "a piece of knowledge a surprising number of working practitioners have wrong"
- Exam Alert — "the detail that gets asked" · "the one candidates miss"

These sit in the register the brand licenses (experienced practitioner judgment) rather
than being fabricated statistics, and the underlying judgments are almost certainly right.
**"The single most common" is the one that overreaches** — it is a superlative about
population frequency, stated flat. Author call; hedging it costs one word.

**Separately, and outside guardrail #8:** §3 asserts twice that third-party preparation
material misstates `kube-public`. On the substance Chapter 4 is correct and the
documentation backs it. But it is an unsourced claim about competitors' accuracy, and
Part 14 forbids strawmanning alternative study methods. Adjacent rather than in breach —
flagged for the author, not marked failing.

**⚑ And the one that outranks both:** Chapter 4 **has no fact-accuracy audit at all.**
`diagnostics/fact-accuracy.md` is a BLOCKER notice — Stage 6 received `[file not available]`
for both drafts and inspected zero claims. Guardrail #1 ("no fabricated statistics or
claims") **cannot be certified for this chapter.** Re-run Stage 6 against `draft-v2.md`
before ship.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 4 update (2026-08-24)

**6 tagged items · graded pool 34 (13 Bearings + 21 Practice) · rate = 17.6%.**
B3's rung for Chapter 4 is **15%. Cleared.** Chapter 4 is the first chapter to draw from
two predecessors.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| kube-apiserver receives the request; etcd stores the object | ch 3 §2, §5 | **ch 4** — Practice Q1 |
| a controller acts on the difference between desired and current state | ch 3 §6 | **ch 4** — Practice Q2 |
| the Job controller tells the API server; it does not run Pods itself | ch 3 §6 | **ch 4** — Practice Q3 |
| desired/current state fields, and the component that stores the object | ch 3 §5–§6 | **ch 4** — Bearings #1 Q5 |
| five mechanisms for private-registry credentials | ch 2 §3 | **ch 4** — Bearings #2 Q4 |
| image immutability — build a new image, then recreate the container | ch 2 §2 | **ch 4** — Practice Q13 (distractor A) |
| the control loop; the API server and etcd | ch 3 §5–§6 | **ch 4** — Soundings Q3, Q4 *(excluded from budget by B3)* |

**Notes on quality, all favourable:**

- **Practice Q3 is exemplary spacing.** It re-tests the Job-controller fact that Chapter 3's
  own Bearings #3 Q2 tested — a correctly spaced *re-test*, not a duplicate, and the
  distractors do independent work (B invents a controller→kubelet channel; C tests whether
  the reader thinks a control-plane component may reach etcd directly).
- **Practice Q13's distractor A is a genuine Chapter 2 discrimination**, not decoration: it
  encodes ch2's "build a new image, then recreate the container" rule and requires the
  reader to notice that immutable-ConfigMap behaves the same way.
- **Soundings Q3 and Q4 are retrieval items in Soundings clothing.** Both are answerable
  only from Chapter 3. This is compliant — Part 11 requires Soundings be answerable from
  prerequisites, and Chapter 3 *is* the stated prerequisite — and the rubric handles it
  well by naming ch3 §5–§6 as the remediation. Noted because it shifts the pre-test's
  function toward continuity checking, which B3 anticipated (decision #2: source Soundings
  from B2's Prerequisites column, making the spacing free).

**⚑ Count error to fix in the chapter:** the Practice section intro says *"**Five** test
material from earlier chapters and are tagged as such."* Twenty-one questions is correct;
**four** are tagged in that section (Q1, Q2, Q3, Q13). Tag a fifth or change the word.

**⚑ Cross-reference defects that affect retrieval navigation** (Stage 13, blocking):
Bearings #2 Q4's answer sends readers to **`Ch 2 §4`**; the five-mechanism list is at
**ch2 §3** (L457), and ch2 §4 is *The Container Runtime Interface*. Chapter 1's Soundings A2
already routes readers to Ch 2 §4 for CRI, so as written a reader lands on the wrong
section expecting a credentials list. Same fix needed in §4 body. Separately, §1's
`Ch 1 §5` should be `Ch 1 🧭 Soundings A5` — Chapter 1 has no numbered sections, and
Chapter 3 already established the correct citation form at L932.

---

## Cross-cutting themes — status after Chapter 4

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **The control loop** (B3 headline) | Ch 3 §6 | ✅ **Ch 4** — first theme retrieval in the book to land | Ch 6 (ReplicaSet), **Ch 11 (still unbeared)**, Ch 15 (primary Zenith), Ch 17 |
| **The absent-component pattern** | Ch 3 §4, named | — | Ch 10 ×2 (Ingress; **NetworkPolicy — unbeared**), Ch 13, Ch 17 |
| **Namespaced vs cluster-scoped** | **Ch 4 §3**, ★ Fixed Point | — | **Ch 12 §3** (RBAC derivation — beared), Ch 10 (selector across a namespace line), Ch 11 (PV/StorageClass — ⚑ unbeared) |
| **Labels/selectors as the universal join** | **Ch 4 §5**, ★ Fixed Point | — | Ch 6, Ch 7, Ch 9, Ch 10 — **all four beared from Ch 4** |
| **"Kubernetes defines an interface and lets the ecosystem implement it"** | Ch 2 §4, named | ⚑ Ch 3 §3 hit the first recurrence and did not use the name | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §4 |

**✅ The control-loop theme's Chapter 4 obligation is discharged.** `concepts/control-loop.md`
required Chapter 4 to "deliver the `spec` field as *the field that holds desired state*, and
`status` as its counterpart." Chapter 4 §2 does exactly that **and reproduces Chapter 3's
forward-bearing wording verbatim.** That verbatim echo is why the payoff lands for a reader
who read the two chapters a week apart — model it for every deferred-term handoff that
follows.

**Chapter 4 bears forward to all four downstream chapters for the selector theme.** Chapter
3 missed two of its equivalent bearings. **Copy Chapter 4's discipline here, not Chapter 3's.**

**⚑ Neither new theme gets a retrievable name.** B3's stated rationale for naming the
absent-component pattern was that "naming it once and retrieving it by name turns four
gotchas into one rule." Chapter 4 gives both themes ★ Fixed Points but no coinage. **Until
the author rules otherwise, retrieve these exact strings:**

- *"Not everything lives in a namespace."*
- *"The label selector is the core grouping primitive in Kubernetes."*

If a coined name is preferred, it must be chosen **before Chapter 10 drafts** — that is the
first chapter needing both themes at once.

---

## Forward commitments — status

| # | Commitment | Status |
|---|---|---|
| 1 | Ch 13's checkpoint must carry a Ch 8 retrieval item (version skew) | **OPEN** — verify at Ch 13 Stage 13 |
| 2 | Ch 11 must retrieve the control loop | **STILL OPEN, and now overdue.** Ch 3 did not bear to Ch 11; **Ch 4 does not either.** Two chapters have now passed the obligation forward without anchoring it |
| 3 | Ch 5 must retrieve the UID rule | **NEW — opened by Ch 4.** Chapter 4's closing page states that a replaced Pod carries the same name and a different UID, and names it as "exactly what UIDs are for." Chapter 5 should retrieve `metadata.uid` explicitly rather than re-deriving it |
| 4 | Ch 12 must **derive** the four RBAC combinations from the namespaced/cluster-scoped boundary | **NEW — opened by Ch 4.** The chapter tells the reader the 2×2 is "not a table to memorize" but "a direct consequence of this boundary." If Ch 12 ships a 2×2 table, Chapter 4 told the reader something false about the book |

**Convention settled at Chapter 3 and honored at Chapter 4:** `[retrieval: chN]` tags render
**reader-visible**, bold-bracketed, in both stem and answer key. Two chapters of consistent
practice. Still recorded as OBSERVED PRACTICE pending author ratification — but the window
to change it cheaply is closing.
=== END APPEND ===
```

---

**The three things worth your attention, in order.**

**Chapter 4 shipped without a fact-accuracy gate.** Stage 6 got `[file not available]` for both drafts and inspected zero claims; its own report says the zeroes are the absence of an audit, not a clean bill of health. Every definition above is verbatim-faithful to the chapter, which guarantees fidelity, not correctness. Re-run Stage 6 against `draft-v2.md`.

**The write-block format has never worked, and permissions were only half the reason.** `=== WRITE` appears exactly once in `certcomp` — in the prompt that asks for it. Nothing parses it. Chapter 1's ten files and Chapter 3's fourteen were composed correctly and were never going to land. The materializer above replays all three manifests in order; running it is a two-minute fix that recovers three chapters of knowledge base.

**Two ledger items closed on evidence, and one opened.** `sources/` now holds the eight snapshots Chapter 3 flagged as missing — strike those flags. `chapter-lineup.md` row 8 assigns `leases` to Chapter 8, so Chapter 3's ledger row is stale and Chapter 4's bearing is right. And Chapter 3's promise that "later chapters say reconciliation" came due at Chapter 4 and went unpaid — the chapter describes the behavior three times without ever naming the word. One appositive at the §2 Fixed Point closes it, and Chapters 6, 11, 15, and 17 all need the term retrievable.
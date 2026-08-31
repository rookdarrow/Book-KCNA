I inspected the knowledge base on disk, then verified the integration report's open items against the shipped chapters, the 214-file source corpus, and the eleven prior Stage 14 manifests rather than taking them on trust. Four of the seven research gaps resolve differently than the revision notes assumed — one of them inverts an instruction the revision stage left for the author.

# Knowledge-Base Manifest — KCNA Chapter 14

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice, carried forward and re-verified.** `Book-KCNA/knowledge-base/` **still does not exist on disk** — confirmed directly, not inherited from Ch 13's manifest. Thirteen manifests now exist (`ch-01` … `ch-13`); none has been applied. Chapter 14 adds the fourteenth.
>
> **Ordering contract, inherited unchanged from Ch 12 and Ch 13.** **APPEND** for the three shared registers and for every shard that already exists; **WRITE** only for filenames that collide with nothing. Verified all 18 new slugs against the 138 slugs referenced across `ch-01`–`ch-13`: no collisions. Chapter 14 introduces **no new full-file WRITE to a shared register**, so infrastructure flag ⚑ I1's blast radius is unchanged by this chapter.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

Two tiers, following Ch 11–13. The integration report marked **8 terms** as needing entries; skill Part 16 requires every technical term the book introduces, so the **20 B7-owned Chapter 14 rows** (`term-ownership.md:452–475`) are harvested alongside them, plus four terms Chapter 14 introduces that the ledger does not assign at all.

### Tier 1 — entries whose definition is unsourced, provisional, or contested

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **`appVersion`** | *"`Chart.yaml` separately carries `appVersion`, the version of the application the chart installs. These move independently."* — ⚠ **UNSOURCED. Zero occurrences of the string `appVersion` across all 214 snapshots**, verified independently | Chapter 14 §4 |
| **APIService** | *Never defined.* Used six times as part of metrics-server's composition — ⚠ **UNSOURCED, and absent from shipped Ch 13 as well**. See ⚑ C2 | Chapter 14, Soundings A2 |
| **Strategic merge patch · JSON patch** | *"A strategic merge patch is a fragment of the object that looks like the object… A JSON patch is a list of explicit operations on paths."* — ⚠ **authored**; the snapshot supplies only the field names and the bare strings "the strategic merge patch standard" / "the json 6902 standard" | Chapter 14 §5 |
| **Subchart** | *"A chart nested inside another chart this way is a subchart."* — ⚠ **no body text in any snapshot**; appears only in `concepts_covered` frontmatter lists | Chapter 14 §2 |
| **Eventual consistency** | Glossed by mechanism only — *"a Deployment whose ConfigMap does not exist yet will produce Pods that cannot start until the ConfigMap shows up, and then it will recover on its own"* — ⚠ **no ledger row, no owner, no ambient-tier assignment**; load-bearing in §1's ordering argument and §6's comparison table | Chapter 14 §1 |
| **`helm push`** | The push semantics are taught (`oci://` prefix, inferred basename and tag); ⚠ **the command name's only literal appearance in the chapter is inside the answer key to the question that grades it** (Practice A17). See ⚑ C6 | Chapter 14, Practice A17 |
| **`helmCharts`** | *"a Helm chart inflation generator"* `[source: kubectl-book-kustomization-fields-2026-08-31]` — ⚠ **no ledger row**; reaches a graded answer key (Practice A13 distractor D) | Chapter 14 §5 |
| **`HELM_DRIVER`** | *"The `HELM_DRIVER` environment variable selects the backend and accepts `configmap`, `secret`, or `sql`."* `[source: helm-storage-backends-2026-08-31]` — ⚠ **no ledger row** | Chapter 14 §3 |
| **Tiller** | *"Helm 2's in-cluster component, introduced so multiple operators could interact with the same set of releases"* — ⚠ **no ledger row**; graded (Practice Q6 distractor A, Practice A10). Also carries the "operator for a person" canonical-forms breach | Chapter 14, Exam Alert |
| **Chart archive** | *"a tarred and gzipped, and optionally signed, chart"* `[source: helm-glossary-2026-08-31]` — ⚠ **no ledger row** | Chapter 14 §4 |

**I verified the two highest-severity gaps independently rather than accepting the draft's flags, and both hold.** `appVersion` returns **zero matches across all 214 files in `sources/`**. `APIService` returns **zero matches across the corpus and zero across shipped `chapter-13`** — the integration report's "check Ch 13's corpus first" resolves to *it is not there either*, which makes this materially worse than the report knew. See ⚑ C2.

### Tier 2 — the 20 ledger rows plus 4 unassigned terms, harvested per skill Part 16

Helm · chart · `Chart.yaml` · `values.yaml` · `templates/` · `charts/` · `crds/` · `NOTES.txt` · `_helpers.tpl` · subchart · Helm release · release revision · `helm install` · `helm upgrade` · `helm rollback` · `helm list` · `--generate-name` · `--all-namespaces` · `--skip-crds` · `--values`/`-f` and `--set` precedence · chart repository · `index.yaml` · chart archive · OCI registry as chart store · `oci://` · chart version vs `appVersion` · Kustomize · base · overlay · `kustomization.yaml` · Kustomization (the KRM object) · the kustomization field set · strategic merge patch · JSON patch · `configMapGenerator` · `secretGenerator` · `kubectl apply -k` · the CRD-in-chart ordering rule and its three limits · Tiller · `HELM_DRIVER`.

**The `Go template (in the Helm sense)` ledger row is now orphaned.** G-14c removed the claim for want of a source and the draft narrowed §2 to named partials only. The row at `term-ownership.md:461` assigns a term the chapter no longer defines. Restore on the fetch, or retire the row — do not leave it pointing at absent text.

---

## Concept shards at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/{slug}.md`

**Eighteen created.** Every one clears the 200-word threshold in the chapter; §7 gets its own shard because the Zenith is the chapter's transferable output and Ch 15's synthesis inherits it.

- `four-failures-of-a-manifest-directory.md` — **created** (§1; the chapter's spine, re-tabulated in §6)
- `helm.md` — **created** (§2; package manager, not template engine — B1 trap #79)
- `helm-chart.md` — **created** (§2; the anatomy — ⚑ and the entry it drops)
- `values-yaml.md` — **created** (§2, §3; the declared surface, and the override precedence ladder)
- `helm-release.md` — **created** (§3; one chart, many releases — B1 trap #80; absorbs `HELM_DRIVER`)
- `helm-release-revision.md` — **created** (§3; ⚑ the counter behaviour the corpus cannot settle)
- `helm-rollback-versus-rollout-undo.md` — **created** (§3; unit / scope / bookkeeping)
- `chart-repository.md` — **created** (§4; an HTTP server — B1 trap #81)
- `oci-registry-as-chart-store.md` — **created** (§4; the Ch 2 payoff)
- `chart-version-versus-appversion.md` — **created** (§4; ⚠ wholly unsourced, graded once)
- `tiller.md` — **created** (Exam Alert; the dating stamp)
- `kustomize.md` — **created** (§5; template-free, in kubectl)
- `base-and-overlay.md` — **created** (§5; without forking the originals)
- `kustomization-fields.md` — **created** (§5; the four groups)
- `strategic-merge-versus-json-patch.md` — **created** (§5; ⚠ authored, graded once)
- `crds-in-charts.md` — **created** (§6; failure two, and the three limits)
- `distribute-versus-adapt.md` — **created** (§6; what the choice turns on)
- `package-not-template.md` — **created** (§7; the Zenith)

**Fourteen amended by append.** Chapter 14 is a new-vocabulary chapter, so the create-to-append ratio inverts Ch 13's — but the appends are where the chapter earns its place in the book rather than merely adding a toolchain.

- `absent-component-pattern.md` — **appended** · ⚑ **Ch 14 uses Ch 10's canonical form, not Ch 13's drifted one** — good news for ⚑ C1 of the Ch 13 manifest
- `control-loop.md` — **appended** · §3's "Helm changed a record of intent, and a controller noticed"
- `kustomize`-adjacent: `configmap.md` — **appended** · `configMapGenerator`, and values.yaml as ConfigMaps one level up
- `custom-resource.md` — **appended** · the registration-before-use rule, applied to packaging
- `declarative-configuration.md` — **appended** · where `kubectl apply -f` stops, stated as four named failures
- `registry.md` — **appended** · a registry serves content, not images
- `oci.md` — **appended** · the distribution spec's reach beyond images
- `secret.md` — **appended** · Helm's bookkeeping is an ordinary Secret, with the access consequence
- `namespace.md` — **appended** · Helm 3 release scoping and `helm list`
- `pluggable-interfaces.md` — **appended** · CRDs as chart content; the Ch 17 §4 anchor
- `operator-pattern.md` — **appended** · ⚑ **canonical-forms breach: "operator" used for a person**
- `resource-metrics-pipeline.md` — **appended** · ⚑⚑ **the APIService gap, now known to be corpus-wide and shipped-text-wide**
- `published-vs-commonly-reported.md` — **appended** · ⚑⚑ **the chapter's strongest ethics pass, and a shipped-Ch-1 miscitation it exposes**
- `domain-weights-44-28-16-12.md` — **appended** · ⚑⚑ **do not restore the 8% → 16% claim**

Not shard-worthy, adequately carried by the glossary: `NOTES.txt`, `_helpers.tpl`, subchart, chart archive, `helm repo`, `--dry-run`, `generatorOptions`, `helmCharts`, `bases`-versus-`resources`.

---

## ⚑ Contradictions and conflicts — flagged, not resolved

Rule 6 requires these loud. **Two correct instructions the revision stage left for the author. One is an inversion.**

### ⚑ C1. HIGH — do **not** restore the 8% → 16% claim. Shipped Chapter 1 is the one that needs correcting.

The revision notes register **G-14e** with the instruction: *"CHECK CH 1'S CORPUS FIRST… The rhetoric is worth restoring if Ch 1 has the snapshot."* I checked. Chapter 1 has the sentence, and its source tag does not hold.

Shipped `chapter-01:274`:

> **Cloud Native Application Delivery doubled**, from 8% to 16% `[source: lf-kcna-program-changes-2026-08-23]`. That is the largest proportional change among the domains that survived the restructure, and material built for the old blueprint will under-serve it by roughly half…

That snapshot opens with a correction that removes exactly this figure:

> *"CORRECTION 2026-08-23: the previous capture of this page listed the retired five-domain weights (46/22/16/8/8) as if sourced here. Targeted re-fetch confirms **THE PAGE DOES NOT DISPLAY THE PREVIOUS DOMAIN STRUCTURE OR WEIGHTS.** Those figures have been removed from this snapshot."*

and closes: *"## Not stated on this page — No question count, no passing score, no duration, and **no retired-blueprint weights**."*

The only place in the corpus carrying `8%` for this domain is `provenance-kcna-60-questions-2026-08-23.md`, which is headed **"DO NOT CITE THE CONTENTS OF THIS FILE AS FACT"**, whose authority field reads *"NOT AUTHORITATIVE — community guest post"*, and whose own cross-check concludes *"46/22/16/8/8 — NOT independently sourced."* The intended source, `cncf-curriculum-repo-kcna-versions-2026-08-23.md`, is an **open gap**.

Three consequences, and the ordering matters:

1. **Chapter 14's revision stage was right, and following its own restore instruction would propagate a miscitation into a second chapter.** The draft-v1 phrasing Ch 14 cut — *"under-serves this material by half"* — is Chapter 1's sentence, inherited rather than invented. Cutting it broke the chain. **Leave Chapter 14 as revised.**
2. **`domain-analysis.md:39` asserts it flatly too** — *"Doubled from 8% to 16% in the revision — the single largest proportional change. Legacy prep material badly under-serves this domain."* A B-stage artifact carrying an unsourced figure is how this reached two chapters, and Ch 15 and Ch 16 read the same row.
3. **The irony is load-bearing and should be recorded, not just noted.** Chapter 1 §2's entire subject is published-versus-commonly-reported figures, and B3's must-not-retrieve list names *"the unpublished 60-question/75% figures"* explicitly — figures from the same non-authoritative snapshot that carries the 8%. The book's thesis chapter cites a community blog post's number under a Linux Foundation source tag.

**Fix, and it is Chapter 1's, not Chapter 14's:** either fetch `github.com/cncf/curriculum` for the retired KCNA blueprint and re-tag, or rewrite `chapter-01:274` to the supported claim (the domain carries 16%; the restructure rolled Observability under Architecture, which *is* sourced at `lf-kcna-program-changes:23`). Correct `domain-analysis.md:39` in the same pass. **Do not renormalize Chapter 14 upward toward Chapter 1.**

### ⚑ C2. HIGH — the `[retrieval: ch13]` item grades a fact Chapter 13 never states

**G-14d resolves worse than the revision notes assumed.** They say *"CHECK CH 13'S CORPUS FIRST."* I checked the corpus and the shipped chapter:

| Where | `APIService` | metrics-server composition (Deployment + Service + RBAC + APIService) |
|---|---|---|
| All 214 snapshots in `sources/` | **0 occurrences** | absent |
| Shipped `chapter-13` | **0 occurrences** | absent |
| Ch 13's own Stage 14 glossary block | absent | absent |
| Chapter 14 draft-v2 | **6 occurrences** | asserted 4× |

So Chapter 14's **Soundings A2** and **Taking Your Bearings (2) Q5 — whose correct answer is option B** — both ask the reader to retrieve a four-object composition that no chapter taught and no source supports. The `[retrieval: ch13]` tag is structurally valid (Ch 13 §7 owns metrics-server) and **false in substance**: the retrieval target does not exist upstream.

This is the specific failure the integration stage exists to catch, and it caught the shape of it while attributing it to the wrong place.

**Two clean fixes, author's choice.** (a) Fetch the metrics-server release manifest and tag the composition, then it is teachable — but it is still not *retrievable* from Ch 13, so Q5's key should be re-aimed at the sourced half (*"applying objects somebody else wrote"*, which Ch 13 §7 does establish). (b) Cut the object list from Soundings A2 and Q5 entirely and let both rest on the sourced half. **(b) needs no fetch and costs the chapter nothing** — the retrieval it actually wants is *"in a declarative system there is no installer,"* which Ch 13 states plainly.

### ⚑ C3. GOOD NEWS — G-14b is closable from the corpus already on disk. No fetch.

The revision notes say the only rollout snapshot is a bare command reference. That is true of `k8s-docs-kubectl-rollout-2026-08-24`, and there is a second snapshot they did not consult. `k8s-docs-deployment-2026-08-23.md`, § *Rolling back a Deployment*:

> *"By default, all of the Deployment's rollout history is kept in the system so that you can rollback anytime you want (you can change that by modifying revision history limit). **A Deployment's revision is created when a Deployment's rollout is triggered — a new revision is created if and only if the Deployment's Pod template (`.spec.template`) is changed; other updates, such as scaling the Deployment, do not create a Deployment revision.** `kubectl rollout undo deployment/<name>` rolls back to the previous revision, `--to-revision=<n>` to a specific one."*

That sources, verbatim and today:

- **TYB (1) Q4 option A's full form** — revision accounting, which the revision stage removed as unsupported.
- **Option B's rebuttal**, which the draft currently supports only by cross-bearing: *"other updates, such as scaling the Deployment, do not create a Deployment revision"* is a stronger and more precise rebuttal than the one in the key.
- The `--to-revision=<n>` form, which pairs neatly with `helm rollback`'s second argument in §3's contrast.

**Not sourced by it:** the ReplicaSet scale-up mechanism. Leave that out.

**G-14b should be struck from the open-gaps list and the stronger item restored from the corpus.** This is the cheapest of the seven and the revision notes rated it a fetch.

### ⚑ C4. MEDIUM — G-14g is genuinely open, and the reason is a second truncation

`helm-using-helm-2026-08-31.md` runs 30 lines and ends:

```
`helm rollback [RELEASE] [REVISION]`

Example:
```

It stops at the word `Example:` — immediately before the transcript that would show whether a rollback increments the counter. This is the **second** Helm snapshot truncated at exactly the point that would close a Chapter 14 gap; `helm-charts-2026-08-31.md` runs 18 lines and ends at *"Helm will expect a structure that matches this:"*, immediately before the field table carrying `appVersion` (⚑ G-14a).

**Recommendation for the harvester, not for this chapter:** two Helm fetches truncating at their first code block is a pattern, not a coincidence. Worth a look at the snapshot tool's handling of fenced blocks before the Ch 15 Helm-adjacent research runs. Both re-fetches are cheap and both close graded material.

`figure ch14-fig03`'s reader-facing **"rev 4 ???"** remains the ship-blocker the integration report named. I have nothing to add to its diagnosis and confirm the corpus cannot settle it.

### ⚑ C5. MEDIUM — the chart anatomy drops a sourced entry, and it is the one the section's thesis is about

`helm-charts-2026-08-23.md` enumerates the chart file structure and includes:

> *"values.schema.json — optional: a JSON Schema for imposing a structure on the `values.yaml` file"*

**`values.schema.json` returns zero occurrences in draft-v2.** Figure `ch14-fig02` and §2's walkthrough list `Chart.yaml`, `values.yaml`, `templates/`, `charts/`, `crds/`, `LICENSE`, `README.md` — and skip it.

That is not a cosmetic omission. §2's thesis is *"`values.yaml` is where the chart author states, in one place, which things an installer is allowed to change"* — and `values.schema.json` is the machine-checkable form of exactly that declaration. The section argues for a declared surface of variation and omits the entry that declares it.

**Fix: one gray-annotated line in fig02** (`values.schema.json — (gray: optional, a schema for values.yaml)`) and one clause in §2. Requires the fig02 image-spec regeneration the revision notes already schedule for the "grey"→"gray" and `crds/` changes, so the marginal cost is zero.

### ⚑ C6. MEDIUM — `helm push` is graded, and its only appearance is in its own answer key

`helm push` occurs **once** in draft-v2: inside **Practice A17**, the answer to the question that grades it. The stem says *"You push a Helm chart to an OCI registry"*; §4's prose says *"When pushing, the reference must be prefixed with `oci://`"* and never names the command.

This is the same shape as Ch 13's flagged *static Pod* — a term first appearing inside a graded answer key. It is milder here (the semantics are taught, only the command name is withheld), but the integration report's index-level instruction to add `helm-push` to `kb_tags.commands` on the grounds that the list means "demonstrated" **overstates what the chapter does**. Either name the command in §4's prose, or do not tag it as demonstrated.

**And `helm pull` is simply missing.** B6 assigns §4 *"`helm repo` and `helm pull`"*. The chapter covers `helm repo`, demonstrates `helm push`, and never mentions `helm pull`. The revision notes address only the `kb_tags` side of this and not the omission. One clause in §4 discharges the skeleton; alternatively record the substitution explicitly, since `helm push` is arguably the better teaching example for the OCI section.

### ⚑ C7. LOW — the interleave tag form diverges from the one shipped Chapter 13 established

Integration item 22 asks the author to *confirm* the D-numbering is competency-level. It is not, and the answer is in the book's own artifact. `domain-analysis.md:33`:

> *"Objective numbering below (D1.1, D1.2, …) is a **Lodestar convention**. CNCF publishes named competencies under each domain but does **not** number them."*

So a reader-facing `[interleaved: D1.1]` prints a house-invented identifier in the one chapter whose central disclosure is that CNCF publishes nothing beneath the competency. Chapter 13 — the only shipped chapter using these tags, three of them — solved this already:

| Shipped Ch 13 | Chapter 14 draft |
|---|---|
| `[interleaved: D1.1 workloads]` | `[interleaved: D1.1]` |
| `[interleaved: D1.3 scheduling]` | `[interleaved: D1.4]` |
| `[interleaved: D2.2 security]` | — |

The trailing topic word is what makes the tag legible without the numbering, which is precisely the mitigation. **Fix: `[interleaved: D1.1 core concepts]` and `[interleaved: D1.4 containerization]`.** House form, one chapter old, and it resolves the disclosure tension rather than merely surviving it.

### ⚑ C8. GOOD NEWS — Chapter 14 inherits Ch 10's canonical form, not Chapter 13's drifted one

Ch 13's Stage 14 manifest raised ⚑ C1: shipped Ch 13 retrieves the absent-component pattern by the **ledger** form (*"the object exists; nothing happens without the component"*) rather than the **shipped** form Ch 10 grades four options on (*"an object without its component does nothing"*). I re-checked: `chapter-13:1279` still carries the ledger form, so that fix was never applied.

**Chapter 14 does not repeat it.** §1's opening debt collection reads *"Install an Ingress controller, because the Ingress object does nothing without one"* — Ch 10's form, applied rather than quoted, with the correct cross-bearing. Chapter 14 needs no change. Recorded here so the Ch 17 §4 collection stage, which meets the whole thread at once, knows the drift is confined to Chapter 13.

*(Note for the same thread: B3's own summary also uses the ledger form. Three planning artifacts and one shipped chapter on one side, shipped Ch 10 and Ch 14 on the other. The graded text is Ch 10's; the artifacts should move, not the book.)*

---

## Infrastructure flags — the knowledge base itself

**⚑ I1 — HIGH, unchanged and now one chapter more expensive.** Chapters 03, 10 and 11 write `glossary.md`, `objective-coverage.md` and `retrieval-log.md` with full **WRITE** blocks; replaying `ch-01` → `ch-14` in order therefore discards everything written before each of those three points. Chapter 14 adds only APPENDs and does not extend the problem, but it does add to what a mis-ordered replay would destroy. **Convert those three chapters' twelve WRITE blocks to APPENDs before any replay.** Mechanical, and appends cannot clobber.

**⚑ I2 — MEDIUM, unchanged.** `concepts/pluggable-interface-pattern.md` and `concepts/pluggable-interfaces.md` are one concept under two slugs. Chapter 14 appends to the latter (Ch 11/12's file) and touches neither the former nor the CNI-ordinal conflict living in it. **Merge at the replay, leaving a stub**, before Ch 17 §4 reads one file and concludes it has the set.

**⚑ I3 — LOW, unchanged and now blocking a second thing.** `.pipeline-state/book-outline/retrieval-architecture.md` is 18 lines of permissions-failure message plus the stage's own summary; the B3 document was never written. Everything I cite from B3 above (the 20–25% band for Ch 14–18, the ≥4-chapters-back spacing floor, the must-not-retrieve list, the named Helm anchors) is recovered from that summary. **Re-run before Ch 19**, which is 100% retrieval by construction — and note it now also holds the only statement of the rule that would have caught ⚑ C1.

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Disclosure as craft** | "CNCF publishes the competency name, 'Application Delivery,' and publishes nothing beneath it… So the topic list in this chapter is authored inference… **It is, I think, clearly the right call. But you should know it is a call.** In practice this means one rule holds throughout: nothing in this chapter is described as 'frequently tested' or 'commonly appears,' because nobody outside the exam authority knows that." | **Strong candidate.** The catalog has exemplars that *make* a disclosure; this one discloses, defends the judgment, declines to hide behind the disclosure, and then converts it into a rule the chapter visibly keeps for 19,000 words. The first-person "I think" is rare in this book and earns its place. Best instance of Ethical Guardrail #8 as prose rather than compliance. |
| **Naming a failure precisely** | "Six weeks later somebody fixes a readiness probe in staging and does not fix it in production, because nothing told them there was a second copy. **This is drift, and it is not a discipline problem: it is what happens when two files are supposed to stay in sync and nothing in the system knows that they are.**" | **Strong candidate.** Refuses the moralizing diagnosis the reader expects and relocates the fault to the system. Skill Part 14's "respect their intelligence; don't moralize" made into a rhetorical move rather than an omission. |
| **Logbook Entry** | "It is called `k8s/` or `deploy/` or, in the most honest cases, `yaml/`… `deployment-prod-final-v2-USE-THIS-ONE.yaml`, whose name is a small monument to the moment somebody realized the naming scheme had stopped working and did not have time to fix it… **Step 4 is the whole problem, written down by somebody who could see it clearly and had no vocabulary for it.** … This is not incompetence." | **Strong candidate.** Recognition humor aimed squarely at the practitioner (Part 14 item 9, clean), and it closes by *withdrawing* the judgment it invited. The "no vocabulary for it" clause is the chapter's thesis smuggled into an anecdote. |
| **Zenith / synthesis compression** | "**You have been taking the sight from too low.** … They agree about everything that matters. Both exist to take a directory of loose files and turn it into **one addressable unit**… the argument the ecosystem spends so much energy on… is an argument about *how*, conducted between two tools that had already agreed on *what*." | **Strong candidate.** Brand vocabulary doing analytical work — "taking the sight from too low" is a real navigational error and a real reading error at once. Compare Ch 13's "a compass that reads north in every direction"; same construction, and the catalog can hold both. |
| **Extended Analogy** | "There is a *package*… There is an *installation*… And there is the *history* of that installation… **Chart, release, revision. You have had this mental model since the first time you administered anything.** Helm did not invent it; Helm brought it to Kubernetes, where the native tooling had objects but no packages." | **Strong candidate.** Three panels, each mapping to exactly one term, closing with the reason the vocabulary is worth learning *given* that the concepts are already held — which is a harder and more honest close than "so it's just like apt." |
| **Recruiting the reader's own answer** | Soundings Q7: "From your own professional experience with any package manager at all (apt, npm, pip, NuGet, Homebrew, whatever you have used), what does a package manager give you that a folder of files does not?" → A7: "**Hold onto whichever ones you named. You will need them shortly.**" | **Moderate to strong.** Generation effect (Part 10) executed on the reader's existing expertise rather than the chapter's content, and the answer key deliberately refuses to grade it. A distinct Soundings move the book has not nominated. |
| **Making the stakes concrete without inventing them** | The Voyage Ahead: "Somebody with cluster credentials on their laptop, running a command, from a machine nobody audits, at a moment nobody records… **If someone edits an object by hand next Tuesday, the cluster and the package quietly stop agreeing, and no one finds out until the next deploy overwrites the fix or the fix overwrites the deploy.**" | **Moderate.** Strong cliffhanger construction, and the last clause is a genuinely useful symmetry. Held at moderate only because Ch 15 will need the same beat and the catalog should not pre-empt it. |

---

## Objective coverage log

Appended to `objective-coverage.md`. Concept-level audit walked row by row against `domain-analysis.md:257–296`.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D3.1 — Application Delivery** | **Chapter 14** | **deep — the packaging half; GitOps and delivery to Ch 15** | — |

**D3.1 Helm concept coverage: 9 of 9 taught here.** Helm · Chart · `Chart.yaml` · `values.yaml` · `templates/` · `charts/` · `crds/` · Chart repository · Release — every B1 D3.1 Helm row lands in Chapter 14, at depth. The remaining D3.1 rows (GitOps and its four principles, OpenGitOps, Argo CD, source of truth, OutOfSync, sync, tracking targets, Knative, twelve-factor) belong to Ch 15 and Ch 16 by design and are correctly untouched.

**Trap coverage: 3 of 3 D3.1 Helm traps, all `[source]`-tagged, all deep.**

| # | Trap | Where addressed |
|---|---|---|
| 79 | "Helm is a templating engine" | §7's whole Zenith; Exam Alert trap row 1; Exam Alert high-priority #3 |
| 80 | Confusing chart with release | §3 ★ Fixed Point; ⚠ Hazards; TYB (1) Q1 keyed; Practice A1; Chapter Summary |
| 81 | Confusing `charts/` with a chart repository | Two 🪝 Snags (§2, §4); fig02 annotation; TYB (1) Q2 keyed; Practice Q11; Exam Alert |

Trap #79's correct understanding in the inventory reads *"chart (the package) → values (configuration) → templates (which render manifests) → **release** (an installed instance)"* — the Exam Alert's trap row reproduces that chain exactly, with **Helm release** bolded. Contract honoured without being copied.

**Research gaps closed by Chapter 14:**

| Gap | Status |
|---|---|
| **G19 — Kustomize.** *"Named inside the Argo CD and Helm-adjacent material as a manifest source, never explained. Overlay/base model is worth one paragraph."* | **Closed, and over-delivered.** §5 and §6 give it two sections. Defensible on domain weight, and it is what makes §7's Zenith possible — a chapter with one Kustomize paragraph could not have argued that templating is not the definition. |
| **G-14b** — Deployment revision accounting | **Closable today from `k8s-docs-deployment-2026-08-23`.** See ⚑ C3. Strike from the open list. |

**Still open and touching Chapter 14:** `appVersion` (**G-14a**, one graded item) · the Helm chart-template guide, for the Go-template claim and the strategic-merge/JSON-patch semantics (**G-14c**, one graded item) · metrics-server's composition (**G-14d**, one graded item, and see ⚑ C2 — this is now a retrieval-validity problem, not only a sourcing one) · the prior KCNA blueprint (**G-14e** — see ⚑ C1; **do not restore**) · the Helm 3.0 GA date (**G-14f**, cosmetic; the sourced Tiller marker does the work) · whether `helm rollback` increments the revision counter (**G-14g**, reader-facing in fig03).

---

## Retrieval-practice ledger

| Tested topic | Original chapter | Retested in |
|---|---|---|
| `kubectl rollout undo` reverts the Pod template; the controller reconciles | ch 6 §5 | ch 14 — Taking Your Bearings (1) Q4 |
| "Install metrics-server" is applying objects somebody wrote; `kubectl top` fails on a bare cluster | ch 13 §7 | ch 14 — Taking Your Bearings (2) Q5 ⚑ **see ⚑ C2** |
| A CRD must be registered before resources of its kind can be used | ch 6 §8 | ch 14 — Practice Q1 *(tagged `[interleaved: D1.1]`)* |
| One release contains many objects; a single act returns all of them | ch 6 §1 / ch 4 §2 | ch 14 — Practice Q9 *(tagged `[interleaved: D1.1]`)* |
| The OCI Distribution Spec distributes *content*, not images specifically | ch 2 §5 | ch 14 — Practice Q12 *(tagged `[interleaved: D1.4]`)* |

### ⚑ Compliance — and Chapter 13's denominator problem repeats

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of **Bearings** | 20–25% (Ch 14–18 band) | 2 of 10 = **20%** | ✅ at the floor |
| Retrieval share of the **Practice pool** | same target, *"applied to it once sized"* | **0 of 17 = 0%** | ❌ |
| Retrieval share of **all graded items** | 20–25% | 2 of 27 = **7.4%** | ❌ |
| Spacing floor (≥4 chapters back, from Ch 8 on) | ≥1 item | ch 6 is **eight** back | ✅ |
| Question inventory vs B4 (`length-budget.md:64`) | 8 Soundings · 10 Bearings · 17 Practice · 35 total | 8 · 10 · 17 · **35** | ✅ exact |

**This is Chapter 13's ⚑ C7 recurring, and two chapters make it a pattern rather than a lapse.** Both chapters put every `[retrieval:]` tag in Bearings and none in Practice; both carry genuine backward reach in Practice under `[interleaved:]` tags instead. A mechanical audit greps `[retrieval:` and reads both Practice pools as empty — and **Ch 19 is built by exactly such an audit**.

**Cheapest fix, needing no new questions and no new content.** Dual-tag Practice Q1, Q9 and Q12, combining with the ⚑ C7 form fix:

- Q1 → `[retrieval: ch6]` `[interleaved: D1.1 core concepts]`
- Q9 → `[retrieval: ch6]` `[interleaved: D1.1 core concepts]`
- Q12 → `[retrieval: ch2]` `[interleaved: D1.4 containerization]`

That puts Practice at 3 of 17 = 17.6% and the chapter at 5 of 27 = **18.5%** — still marginally under, but inside a rounding argument rather than reading as zero. Adding one item on the chart-versus-release distinction, which the Exam Alert already names as the material's most common collapse, reaches the band cleanly. **Recommend fixing this at the book level once rather than per chapter for the remaining five.**

**Soundings note.** All eight are retrieval, sourced from B2's Prerequisites column exactly as B3 requires, and every one is answerable from Ch 1–13 or professional experience. Excluded from the budget per B3. Q7 (any package manager you have used) is the only item in the book that draws on experience outside the book, and it is calibrated correctly — the answer key grades nothing.

### Obligations Chapter 14 discharged — eleven

All three of Chapter 6's chapter-level promises **verified by line number against shipped text**, not inferred:

| Promise | Shipped at | Discharged by |
|---|---|---|
| *"a Helm chart's job is to template this object"* | `chapter-06:372` | §2's closing worked instance — the Ch 6 Deployment, templated |
| *"Helm rollback and Deployment rollback are different mechanisms wearing the same word"* | `chapter-06:720` | §3's ★ Fixed Point, on all three axes |
| *"why Helm charts have a `crds/` directory"* | `chapter-06:1036` | §6, as failure two returning diagnosable |

Also verified: Chapter 13's closing handoff exists at `chapter-13:1830` and Chapter 14 quotes it accurately. *(Ch 13 names metrics-server, a logging backend and an Ingress controller; Ch 14's collection names a CNI plugin, an Ingress controller, a CSI driver and metrics-server, dropping the logging backend. Not a defect — Ch 14 collects a longer debt than Ch 13 named — but the lists differ and a reader comparing them will notice.)*

Further discharged: Ch 1's Helm pointer (`chapter-01:274`, *"GitOps, Helm, deployment strategies… [cross-bearing: see Ch 14–16]"* — ledger contract "name only, always with a pointer," honoured on both sides) · Ch 2 §3 and §5 (registries and OCI, paid off in §4 in a way the reader could not have predicted) · Ch 4 §1, §2, §4, §6 · Ch 10 §3 (the absent-component rule, in Ch 10's own form — see ⚑ C8) · Ch 13 §7.

### Forward obligations Chapter 14 creates

| Topic Ch 14 owns | Must be retrieved in | How |
|---|---|---|
| Charts as a delivery agent's manifest source | **Ch 15 §4** | Planted in §2. B6 records this number as **pinned by shipped pointers** — immovable. |
| Push-versus-pull, and who runs the install | **Ch 15 §3** | The Voyage Ahead asks the question and declines to answer it. Three cross-bearings emitted. |
| Rollback by revert — the third sense | **Ch 15 §4** | §3's ⚠ Hazards names all three and reserves the third. ⚠ **must use the ledger's exact `rollback by revert`** — §3 currently writes two other variants. |
| CRDs shipped as chart content | **Ch 17 §4** | Planted in §6. Also pinned by shipped pointers. |
| The control loop pointed at a Git repository | **Ch 15 §7** | §7 sets it up (*"a package is that same move, one level up"*) and correctly leaves the payoff unspent. |
| Kustomize as an Argo CD manifest source | **Ch 15 §4** | §5's `helmCharts` 🔭 Closer Look establishes the tools compose; B1 trap #77 needs it. |

### Ledger and glossary debts to record at the glossary build

New ledger rows for **Tiller** (or `helm-2-to-helm-3`), **chart archive**, **`helmCharts`**, **`HELM_DRIVER`**, **`helm push`**, and **eventual consistency** (needs an owner or an ambient-tier assignment; used load-bearing in two chapters). Correct **`kubectl -k`** → **`kubectl apply -k`** at `term-ownership.md:474` and in B6's §5 "owns" line — the bare form is not a valid invocation and the draft is right not to follow it. Retire or restore the orphaned **Go template** row (`:461`). Move **Helm** and **Release (Helm)** first-appearance from §2 to Why This Chapter Matters / §1; cosmetic, ownership unaffected. Carried forward unchanged from earlier gates: **CNAME**, **BGP**, **eBPF**, **IPVS**, **CIDR**, the **VPA** first-appearance correction, and the hyphenated "cloud-native" instances.

---

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 14 additions

> ⚠ **MERGE REQUIRED BEFORE PROMOTION.** A further A–Z sequence appended after the
> Chapter 13 block. Appended rather than merged in place because merging would require
> re-transcribing verbatim documentation definitions, and Rule 5 treats definitional drift
> as worse than a duplicated alphabet. Interleave mechanically before promoting this file
> to the shipped back-of-book glossary. No entry below duplicates an entry above.

---

## A

**`appVersion`** — The version of the *application a chart installs*, carried in `Chart.yaml`
separately from the chart's own version. The two move independently: "You can ship chart 4.1.2
and 4.1.3 that both install nginx 1.25.3, because what changed between them was the chart. You
can ship chart 5.0.0 that installs nginx 1.26.0, where both changed at once."
(Chapter 14 §4)

> ⚠ **PROVISIONAL — the highest-severity gap in this chapter, verified independently.** The
> string `appVersion` appears in **zero of the corpus's 214 snapshots**.
> `helm-glossary-2026-08-31` defines Chart Version and stops; `helm-charts-2026-08-31` is
> **18 lines** and truncates at *"Helm will expect a structure that matches this:"* —
> immediately before the `Chart.yaml` field table that would carry it. Three snapshots list
> `chart-version-versus-appversion` in `concepts_covered` with no body text behind it, which
> is not a citation.
>
> **Graded once** (Taking Your Bearings (1) Q5, keyed correct as B). **FIX:** re-fetch
> `helm.sh/docs/topics/charts/` and *extend* the existing snapshot past its truncation point —
> do not open a new one. If the fetch does not land, cut Q5 and reduce §4 to the sourced half
> (the chart's own version tracks the packaging).

**APIService** — ⚠ **NOT DEFINED ANYWHERE IN THE BOOK.** Used six times in Chapter 14 as one
of the objects composing metrics-server ("a Deployment, a Service, RBAC rules, an APIService
registration").

> ⚠ **PROVISIONAL, and worse than a sourcing gap.** `APIService` returns **zero matches across
> all 214 snapshots AND zero matches in shipped `chapter-13`** — both verified directly. The
> term therefore reaches graded text (**Soundings A2**; **Taking Your Bearings (2) Q5**, where
> it is part of the keyed *correct* answer, tagged `[retrieval: ch13]`) without having been
> taught anywhere. A retrieval item must retrieve something the reader was actually told.
> See the manifest's ⚑ C2 for the two clean fixes.

---

## B

**Base (Kustomize)** — The directory holding the unmodified upstream manifests and a
`kustomization.yaml`. "The base is not edited. The base is not copied." Overlays reference it
and declare only their own differences. (Chapter 14 §5)

---

## C

**Chart** — ★ *"A chart is a collection of files that describe a related set of Kubernetes
resources"*, laid out in a particular directory tree, and packageable into versioned archives
for deployment. *"A single chart might be used to deploy something simple, like a memcached
pod, or something complex, like a full web app stack with HTTP servers, databases, caches, and
so on."* `[source: helm-charts-2026-08-31]` The directory name is the name of the chart without
version information — a chart describing WordPress lives in a `wordpress/` directory.
`[source: helm-charts-2026-08-31]` (Chapter 14 §2; named at Ch 1)

> ★ **Note what the definition does not say: *templated*.** Templating is in a chart and is
> not in its definition. Versioning, a declared surface of variation, and packageability are
> what make it a chart. §7's Zenith is built entirely on that omission.

**Chart archive** — *"A tarred and gzipped, and optionally signed, chart."*
`[source: helm-glossary-2026-08-31]` (Chapter 14 §4)

> ⚠ No B7 ledger row and no register row.

**Chart repository** — ★ *"A chart repository is an HTTP server that houses an `index.yaml` file
and optionally some packaged charts."* `[source: helm-chart-repository-2026-08-31]` Managed
with the `helm repo` commands. `[source: helm-charts-2026-08-23]` Because it *"can be any HTTP
server that can serve YAML and tar files and answer GET requests, you have a plethora of
options for hosting your own."* `[source: helm-chart-repository-2026-08-31]`
(Chapter 14 §4)

> ⚠ **NOT `charts/`.** This is B1 trap #81 and the chapter's most-repeated warning. A chart
> repository is an **HTTP server on the network**; `charts/` is a **directory inside a chart**
> holding its dependencies. Same word, opposite ends of the pipeline.
>
> ⚠ Two sourced surface forms coexist unreconciled: `helm-charts-2026-08-23` says a repository
> *"houses one or more packaged charts"*; `helm-chart-repository-2026-08-31` says
> *"an `index.yaml` file and optionally some packaged charts."* The chapter uses the latter.
> No conflict, but §4 also introduces *"Helm repositories"* as a third form inside a sourced
> quotation, without reconciling it against the chapter's own headword.

**Chart version** — Charts are *"versioned according to the SemVer 2 specification"*, and
**a version number is required on every chart**. `[source: helm-glossary-2026-08-31]` The
version tracks *the packaging*: a template fixed, a default adjusted, a new value exposed.
(Chapter 14 §2, §4)

> ★ This requirement is failure three from §1 closed by fiat. A directory has no version
> because nothing makes it have one; a chart has one because Helm refuses to work with a chart
> that lacks one. See [[chart-version-versus-appversion]].

**`Chart.yaml`** — The chart's identity: name, version, description. **Every chart must have
this file.** `[source: helm-glossary-2026-08-31]` It is also where dependencies are declared,
having absorbed the older `requirements.yaml` in Helm 3 — which is why the file's own
`apiVersion` was bumped from `v1` to `v2` for Helm 3.
`[source: helm-changes-since-helm2-2026-08-31]` (Chapter 14 §2)

**`charts/`** — *"A directory containing any charts upon which this chart depends."*
`[source: helm-charts-2026-08-23]` A chart nested inside another this way is a **subchart**.
(Chapter 14 §2)

> ⚠ **See the warning under Chart repository.** This is one of the two genuinely easy
> confusions in the material and the chapter names it twice on purpose.

**`configMapGenerator`** — A `kustomization.yaml` field that *"generates ConfigMap resources"*
from literal values or files on disk, rather than requiring a hand-authored object with its
`data` map. `[source: kubectl-book-kustomization-fields-2026-08-31]` (Chapter 14 §5)

> Belongs in an overlay because ConfigMaps and Secrets are the objects that vary most between
> environments — generating them there puts the most environment-specific objects in the layer
> that is *about* environment specificity. Graded at Practice Q13.
>
> ⚠ The name-hash suffix these generators append is **deliberately not stated**; no snapshot
> covers it, and draft-v1 correctly omitted it rather than asserting it.

**`crds/`** — *"A special directory you can create in your chart to hold your CRDs."* These CRDs
are **not templated**, and are **installed by default** when you run `helm install` for the
chart. `[source: helm-crd-best-practices-2026-08-31]` (Chapter 14 §2, §6)

> ★ Three documented limits, and the second is the one that catches teams in production:
> `--skip-crds` skips the installation step; **there is no support at this time for upgrading
> or deleting CRDs using Helm**; and `--dry-run` is not currently supported for CRDs.
> `[source: helm-crd-best-practices-2026-08-31]`
>
> The symptom of the no-upgrade limit is confusing rather than loud: the chart upgrades
> successfully and the new feature does not work, because the API server is still serving the
> old schema. Graded at Taking Your Bearings (2) Q3.

---

## E

**Eventual consistency (as an apply-ordering argument)** — The property that covers most
ordering sins in a reconciling system: *"a Deployment whose ConfigMap does not exist yet will
produce Pods that cannot start until the ConfigMap shows up, and then it will recover on its
own."* It does **not** cover a manifest whose `kind` is unregistered — that is rejected, not
queued. (Chapter 14 §1, §6)

> ⚠ **No ledger row, no owning section, no ambient-tier assignment**, despite being
> load-bearing in §1's ordering argument and in §6's comparison table. The term carries a
> precise distributed-systems meaning; assign it or gloss it before the glossary build.

---

## G

**Generator (Kustomize)** — `configMapGenerator`, `secretGenerator`, and `generatorOptions`,
which controls their behavior. `[source: kubectl-book-kustomization-fields-2026-08-31]`
(Chapter 14 §5)

---

## H

**Helm** — ★ *"A package manager for Kubernetes."* `[source: helm-homepage-2026-08-31]`
Its packaging format is a chart; installing a chart creates a release. (Chapter 14 §2;
named at Ch 1)

> ★ **Helm is a package manager, not a template engine.** This is B1 trap #79 and the
> chapter's ☀️ Zenith. Kustomize solves the same problem with no templating at all
> `[source: kustomize-overview-2026-08-23]`, which is the cleanest available proof that
> templating was never the definition. See [[package-not-template]].
>
> Helm renders charts **client-side** and stores a record of the installation in Kubernetes.
> `[source: helm-changes-since-helm2-2026-08-31]` There is no Helm server component and no
> `kubectl` in the path.

**`helm install`** — Creates a release from a chart. **Helm 3 throws an error if no name is
provided**; `--generate-name` opts back into Helm 2's auto-naming, which *"proved to be more
of a nuisance than a helpful feature"* in production.
`[source: helm-changes-since-helm2-2026-08-31]` (Chapter 14 §3)

**`helm list`** — Lists the releases in your current context's namespace; `--all-namespaces`
widens it to the cluster. `[source: helm-changes-since-helm2-2026-08-31]` (Chapter 14 §3)

> ★ **This is the command a directory of manifests has no equivalent for.** §1 asks *"what is
> currently installed on this cluster?"* and leaves it open; `helm list` is the answer. Not
> because nobody wrote the directory equivalent — because a directory is not a thing you can
> ask about.

**`helm push`** — Pushes a chart to an OCI registry. The reference *"must be prefixed with
`oci://` and must not contain the basename or tag"*; the basename is inferred from the chart's
name and the tag from its semantic version. `[source: helm-oci-registries-2026-08-31]`
(Chapter 14 §4)

> ⚠ **Graded (Practice Q17), and the command name's only literal appearance in the chapter is
> inside that question's own answer key.** §4 teaches the semantics without naming the command.
> Name it in §4's prose, or do not tag it as "demonstrated" in the outline's `kb_tags.commands`.
>
> ⚠ **`helm pull` is assigned to §4 by the section skeleton and is entirely absent from the
> chapter.** Add a clause or record the substitution.

**`helm rollback`** — ★ *"The first argument is the name of a release and the second is a
revision (version) number; if this argument is omitted or set to `0`, it will roll back to the
previous release."* `[source: helm-rollback-cli-2026-08-31]` (Chapter 14 §3)

> ★ **Not the same mechanism as `kubectl rollout undo`, and neither calls the other.** Unit:
> a Helm release versus one workload object. Scope: everything the chart installed versus one
> Pod template. Bookkeeping: Secrets in the release's namespace versus the Deployment's
> ReplicaSets. See [[helm-rollback-versus-rollout-undo]].
>
> ⚠ **Helm's own wording says "previous *release*" where it means the preceding *revision*** —
> the exact conflation §3 exists to break. Practice A7 reconciles it four pages later; add a
> half-clause where the reader first meets it.
>
> ⚠ **Whether a rollback is itself recorded as a new numbered revision is NOT SETTLED by this
> corpus and must not be written from memory.** `helm-using-helm-2026-08-31` is 30 lines and
> truncates at the word *"Example:"*, immediately before the transcript that would show it.
> Figure `ch14-fig03` currently shows a reader-facing **"rev 4 ???"**. Resolve or explain.

**`helm upgrade`** — Changes an existing release. *"It will only update things that have
changed since the last release."* `[source: helm-using-helm-2026-08-31]` (Chapter 14 §3)

**Helm release** — ★ *"A release is an instance of a chart running in a Kubernetes cluster."*
`[source: helm-architecture-2026-08-31]` When a chart is installed, the Helm library creates a
release to track that installation `[source: helm-glossary-2026-08-31]`. **The same chart can
be installed many times, each creating a separately named release that can be upgraded and
rolled back independently.** `[source: helm-charts-2026-08-23]` (Chapter 14 §3)

> ★ **The chart is the thing on the shelf; the release is the thing you installed.** This is
> B1 trap #80 and the single most common collapse in the material. A sentence that conflates
> them cannot express the property that matters — *one chart installs many times*.
>
> Release state lives **in Secrets, in the namespace of the release, by default**; the
> `HELM_DRIVER` environment variable selects the backend and accepts `configmap`, `secret`,
> or `sql`. `[source: helm-storage-backends-2026-08-31]` Helm's bookkeeping is an ordinary
> Kubernetes object under the ordinary rules: whoever can read those Secrets can read it, and
> whoever can delete them can make Helm forget.

**`helmCharts`** — A `kustomization.yaml` field described as *"a Helm chart inflation
generator"*: Kustomize renders a chart and treats the output as resources to patch.
`[source: kubectl-book-kustomization-fields-2026-08-31]` (Chapter 14 §5)

> ⚠ No ledger row, and it reaches a graded answer key (Practice A13 distractor D). The two
> tools are not mutually exclusive at the mechanical level, whatever the arguments online
> suggest.

**`HELM_DRIVER`** — The environment variable selecting Helm's release-storage backend.
Accepts `configmap`, `secret`, or `sql`; the default is `secret`.
`[source: helm-storage-backends-2026-08-31]` (Chapter 14 §3)

> ⚠ No ledger row.

---

## I

**`index.yaml`** — The file at the root of a chart repository *"containing metadata about the
packages, including the contents of each chart's `Chart.yaml` file."*
`[source: helm-chart-repository-2026-08-31]` One file that tells a client what the server has,
and at what versions, without downloading anything else. (Chapter 14 §4)

---

## J

**JSON patch (JSON 6902)** — One of Kustomize's two patch styles, applied by
`patchesJson6902` *"using the json 6902 standard."*
`[source: kubectl-book-kustomization-fields-2026-08-31]` A list of explicit operations on
paths: replace this path, add to that array, remove this element. What you reach for when you
need surgical precision, particularly on list elements where merge semantics get ambiguous.
(Chapter 14 §5)

> ⚠ **PROVISIONAL — the semantics are authored.** The snapshot supplies only the field name
> and the bare string *"the json 6902 standard."* Draft-v1's expansion to *"JSON Patch,
> RFC 6902"* was removed because the RFC number was asserted from nothing; that removal was
> correct and should not be undone without a source. **Graded (Practice Q15).** Fetch the full
> kubernetes.io kustomization task page, or cut both the paragraph and Q15.

---

## K

**`kubectl apply -k`** — The kubectl-integrated Kustomize invocation. Kustomize *"is built into
kubectl as `apply -k`"* `[source: kustomize-overview-2026-08-23]`, and kubectl has supported
management of objects using a kustomization file since Kubernetes 1.14.
`[source: k8s-docs-kustomization-2026-08-31]` (Chapter 14 §5)

> ⚠ **The B7 ledger records this as `kubectl -k`, which is not a valid invocation.** The
> chapter is correct not to follow it. Fix `term-ownership.md:474` and B6's §5 "owns" line.
>
> ★ There is no engine to install and no client to distribute. If a machine has kubectl, it
> has Kustomize. That practical fact is half of §6's decision. Graded at Taking Your
> Bearings (2) Q2.

**Kustomization (the object)** — The kustomization file *"is itself a YAML specification of a
Kubernetes Resource Model object called a Kustomization"*, and a kustomization *"describes how
to generate or transform other objects."*
`[source: kubectl-book-kustomization-fields-2026-08-31]` (Chapter 14 §5)

> The customization instructions are themselves an object of a declared kind, not a script.
> Note also that `kustomization.yaml` is the one file in a Kustomize directory the API server
> will not accept — the API server serves the kinds it knows about, and nothing else.

**`kustomization.yaml` fields** — Grouped by what they do
`[source: kubectl-book-kustomization-fields-2026-08-31]`: **what to include** (`resources`;
also the older `bases`, *"add resources from a kustomization dir"*) · **blanket
transformations** (`namespace`; `namePrefix`/`nameSuffix`, which prepend or append to the names
of all resources *and references*; `labels`; `commonAnnotations`; `images`, which modifies name,
tags and/or digest; `replicas`) · **targeted patches** (`patches`, `patchesStrategicMerge`,
`patchesJson6902`) · **generators** (`configMapGenerator`, `secretGenerator`,
`generatorOptions`). (Chapter 14 §5)

> ★ *"and references"* is the load-bearing clause on `namePrefix`: a prefixed Deployment still
> finds its prefixed ConfigMap, because Kustomize understands the relationships and not just
> the strings. Graded at Practice Q14.

**Kustomize** — ★ *"Kustomize introduces a template-free way to customize application
configuration."* `[source: kustomize-overview-2026-08-23]` A standalone tool for customizing
Kubernetes objects through a kustomization file `[source: k8s-docs-kustomization-2026-08-31]`,
also built into kubectl as `apply -k` `[source: kustomize-overview-2026-08-23]`.
(Chapter 14 §5; named at Ch 14 §1)

> ★ **Template-free is the headline, not a footnote.** Each manifest in a Kustomize setup is
> an ordinary, valid, applyable Kubernetes object — `kubectl apply -f base/deployment.yaml`
> works with no rendering step, because there is nothing to render. Taking Your Bearings (2)
> Q1 distractor D exists solely to catch readers who filed Kustomize as "Helm with different
> syntax."
>
> **Closes B1 research gap G19**, which budgeted *"one paragraph"* for the base/overlay model.
> The chapter gives it two sections — over-delivery that §7's Zenith depends on.

---

## O

**OCI registry as a chart store** — *"With the release of Helm 3.8.0, Helm is able to store and
work with charts in container registries, as an alternative to Helm repositories."* Since OCI
artifacts make it possible to store more than container images, *"you can store charts, images,
and other artifacts in a single OCI registry."* `[source: helm-blog-oci-ga-2026-08-31]` The
Helm documentation now **recommends** using container registries with OCI support to store and
share chart packages. `[source: helm-oci-registries-2026-08-31]` (Chapter 14 §4)

> ★ **Why this works at all is a Chapter 2 payoff.** The OCI's own definition of a registry is
> *"a service that handles the required APIs defined in this specification"*
> `[source: oci-distribution-spec-2026-08-24]` — not *a service that stores images*. The
> Distribution Specification defines *"an API protocol to facilitate and standardize the
> distribution of content"*, with no requirement that the content be an image. Standardization
> at the OCI layer bought something nobody was aiming at when the spec was written.
>
> Structure: an OCI-based registry can contain zero or more Helm repositories, each containing
> zero or more packaged charts. `[source: helm-oci-registries-2026-08-31]`
>
> **The project wrote down its reasoning**, which is the more instructive half: chart
> repositories had *"a very hard time abstracting most of the security implementations required
> in a production environment"*; provenance signing was optional rather than integral; the same
> chart uploaded by two tenants cost twice the storage; and a single index file serving search,
> metadata and fetching was clunky to secure. Meanwhile Distribution had *"many years of
> hardening, security best practices, and battle-testing."*
> `[source: helm-changes-since-helm2-2026-08-31]`

**Overlay (Kustomize)** — A directory referencing a base and layering *"patches, name prefixes
and suffixes, labels, images, and generated ConfigMaps and Secrets"* on top, managing any
number of distinctly customized configurations **without forking the originals**.
`[source: kustomize-overview-2026-08-23]` (Chapter 14 §5)

> ★ *Without forking the originals* is the claim to hold. An overlay neither edits nor copies
> its base — it declares only its own differences and points at what it differs from. Taking
> Your Bearings (2) Q1 grades exactly this, and distractor A (*"copies it, then patches the
> copy"*) is the wrong model that puts you back at §1's failure one.

---

## R

**Release revision** — One numbered state of a Helm release over time. *"A sequential counter is
used to track releases as they change."* `[source: helm-glossary-2026-08-31]`
(Chapter 14 §3)

> ⚠ **Never write bare "revision" in Chapters 14–15** where the Deployment sense (Ch 6 §5)
> could be meant. The B7 canonical form is **"release revision"** or **"Helm revision."**
> §3's own subsection heading currently breaks this.
>
> ⚠ Two properties the corpus does **not** settle and that must not be written from memory:
> whether the counter starts at 1 on install, and whether a `helm rollback` is itself recorded
> as a new numbered revision. See the warning under `helm rollback`.

---

## S

**Strategic merge patch** — One of Kustomize's two patch styles, applied by
`patchesStrategicMerge` *"using the strategic merge patch standard."*
`[source: kubectl-book-kustomization-fields-2026-08-31]` A fragment of the object that looks
like the object: you write the piece of the Deployment you want to change, in the same shape,
and Kustomize merges it in. Reads more naturally than a JSON patch and handles most cases.
(Chapter 14 §5)

> ⚠ **PROVISIONAL — the semantics are authored.** See the warning under JSON patch; the two
> stand or fall together, and Practice Q15 grades the pair.
>
> Either style targets an object by identity — its `apiVersion`, `kind`, and `metadata.name`.
> That is how Kustomize knows which base object a delta belongs to.

**Subchart** — A chart nested inside another chart's `charts/` directory. Still a chart, so
still a source of manifests. (Chapter 14 §2)

> ⚠ **PROVISIONAL.** The term and the dependency-install semantics ("install the parent, get
> both") appear in no snapshot body text — only in `concepts_covered` frontmatter lists. §2's
> claim was narrowed by the revision stage to a composition of two sourced facts, correctly.
> **Practice Q3 distractor B rests on the unnarrowed version.** The `helm.sh/docs/topics/charts/`
> re-fetch closes this and `appVersion` together.

---

## T

**Templates (`templates/`)** — *"A directory of templates that, when combined with values, will
generate valid Kubernetes manifest files."* `[source: helm-charts-2026-08-23]` A template is a
manifest with holes in it; values fill the holes; the result is an ordinary manifest.
(Chapter 14 §2)

> Two entries in `templates/` are not manifests. `NOTES.txt` is *"optional: a plain text file
> containing short usage notes"* `[source: helm-charts-2026-08-23]`. Files whose names begin
> with an underscore — conventionally `_helpers.tpl` — *"are assumed to not have a manifest
> inside"*; they are **not rendered to Kubernetes object definitions** but are available
> everywhere within other chart templates. `[source: helm-named-templates-2026-08-31]`
> Neither becomes an object. Graded at Practice Q4.
>
> ⚠ Beyond named partials, **the template language is deliberately not characterised.**
> Draft-v1's *"Go template dialect with a substantial function library, conditionals, loops"*
> was cut: nothing in the captured text says "Go template," and no snapshot describes a
> function library. `go-template-in-helm` appears in two `concepts_covered` lists with no body
> text behind it. One fetch of `helm.sh/docs/chart_template_guide/` restores it — and the B7
> ledger row at `term-ownership.md:461` is **orphaned** until it does.

**Tiller** — Helm 2's in-cluster component, introduced so that multiple people could interact
with the same set of releases. With RBAC enabled by default from Kubernetes 1.6, locking it
down for production became difficult to manage, and the permissive default configuration could
grant users a far broader range of permissions than intended. **Helm 3 removed it entirely** —
*"one of the first decisions we made regarding Helm 3 was to completely remove Tiller"* —
storing release records in Kubernetes directly and evaluating permissions through your
kubeconfig instead. `[source: helm-changes-since-helm2-2026-08-31]`
(Chapter 14, Exam Alert; graded at Practice Q6 and Practice A10)

> ★ **Treat Tiller as a dating stamp.** Material that explains how to secure it is describing
> a Helm that no longer exists — which is reason enough to read carefully whatever else it
> tells you about this domain.
>
> ⚠ **No B7 ledger row.** Add one, as `tiller` or `helm-2-to-helm-3`.
>
> ⚠ **Canonical-forms breach at this entry's source sentence.** The chapter writes *"so
> multiple operators could interact with the same set of releases."* The ledger's
> canonical-forms table carries an explicit prohibition: **never use "operator" for a person** —
> and this chapter also uses "operator" correctly for software, twice, in §6. Fix to *"so that
> multiple people could interact."*
>
> ⚠ **Do not date the Helm 3 release.** Draft-v1's *"a Helm that has not existed since 2019"*
> was cut twice for want of a source; the corpus dates no Helm 3 release, and the sourced
> marker does the same work without a year.

---

## V

**`values.yaml`** — *"The default configuration values for this chart."*
`[source: helm-charts-2026-08-23]` More usefully: the file in which the chart author states, in
one place, **which things an installer is allowed to change**, giving each a value that works.
Everything in it is a knob; everything not in it is a decision the author made on your behalf.
(Chapter 14 §2)

> ★ **Overrides, in precedence order.** `--values` (or `-f`) points at a YAML file and *"can be
> specified multiple times and the rightmost file will take precedence"*; `--set` supplies
> overrides on the command line; and where both are used, ***"`--set` values are merged into
> `--values` with higher precedence."*** `[source: helm-using-helm-2026-08-31]`
> **Rightmost file wins; `--set` beats every file.** Graded at Practice Q5.
>
> ★ Same move as a ConfigMap, one level up. A ConfigMap externalizes configuration out of the
> image so the image can be environment-independent; `values.yaml` externalizes variation out
> of the manifests so the *manifests* can be. Nothing in it becomes an object — it is input to
> rendering (Practice Q3).
>
> ⚠ **A chart you have edited in place is no longer the versioned artifact you fetched**, which
> is the property packaging exists to give you. Practice Q2 distractor D grades this.

**`values.schema.json`** — ⚠ **OMITTED FROM THE CHAPTER.** The sourced chart file structure
includes *"values.schema.json — optional: a JSON Schema for imposing a structure on the
`values.yaml` file."* `[source: helm-charts-2026-08-23]`

> ⚠ Zero occurrences in the chapter. Figure `ch14-fig02` and §2's walkthrough enumerate the
> chart directory and skip it. This is not cosmetic: §2's thesis is that `values.yaml` is *"the
> declared surface of variation,"* and `values.schema.json` is the machine-checkable form of
> exactly that declaration. **Add one gray-annotated line to fig02 and one clause to §2** — the
> fig02 image-spec is already scheduled for regeneration, so the marginal cost is nil.

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/four-failures-of-a-manifest-directory.md ===
# Concept: The four things a folder of YAML cannot do

**Home:** Chapter 14 §1 · **Competency:** D3.1 · **Status:** canonical
**The chapter's spine** — re-tabulated in §6, and every section answers exactly one of these

## The premise, stated fairly

`kubectl apply -f manifests/` is not a compromise or a stepping stone. *"For a single
application on a single cluster maintained by a single person, this is not a compromise or a
stepping stone. It is correct, and you should keep doing it."* The four failures are where the
technique **stops** — not where it gets awkward.

## The four

| # | Failure | The precise defect | Answered by |
|---|---|---|---|
| 1 | **Environment variation** | Replica counts, image tags and resource limits are fields in the *manifest*, not configuration the app reads. A directory's only answer is another directory — and *"nothing in the system knows"* the two are supposed to stay in sync | Helm `values.yaml` · Kustomize overlays |
| 2 | **Apply ordering** | `apply -f` promises nothing about order. Eventual consistency covers most of it; a custom resource applied before its CRD is **rejected, not queued** | Helm `crds/` — the one case that is fatal rather than slow |
| 3 | **Versioning** | A directory has no version, so *"what is currently installed?"* has no answer, and there is no unit to undo. Five objects, five independent histories, and nothing knows they were one act | Chart version (required) + `helm list` |
| 4 | **Distribution** | You cannot hand it to a stranger. The variable parts are unmarked, the order lives in a README, and *"every installation is a small act of comprehension"* | Chart repositories and OCI registries |

## ★ They are four problems, not one

The section's own warning, and it is exam-shaped: *"Environment variation is about **what
varies**. Ordering is about **sequence**. Versioning is about **identity over time**.
Distribution is about **handing it to a stranger**. A tool can solve some and not others."*

## The asymmetry §6 makes explicit

Kustomize answers **one** of the four cleanly (variation), declines two by design (versioning
and distribution — there is nothing to distribute, which is its premise), and shares failure
two's limitation because `apply -k` is still an apply. That is not a deficiency. It is a smaller
tool solving the subset that occurs when there is nobody to distribute to.

## Where this came due

Thirteen chapters said "install that" and none said how. Chapter 13 named the debt out loud at
`chapter-13:1830`. See [[absent-component-pattern]] — the pattern that generated the debt, and
this shard is where it is finally paid.

## Related

[[absent-component-pattern]] · [[declarative-configuration]] · [[distribute-versus-adapt]] ·
[[helm-chart]] · [[base-and-overlay]] · [[crds-in-charts]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm.md ===
# Concept: Helm

**Home:** Chapter 14 §2 · **Competency:** D3.1 · **Status:** canonical
**Closes B1 trap #79** · **Pinned by** `chapter-01:274`, `chapter-06:372`, `:720`, `:1036`

## The definition, and what it is not

★ *"Helm is a package manager for Kubernetes."* `[source: helm-homepage-2026-08-31]`

**Not a template engine.** B1 trap #79 is precisely the mis-definition, and the chapter's
answer is structural rather than assertive: Kustomize solves the same problem with **no
templating at all** `[source: kustomize-overview-2026-08-23]`, which proves templating was
never the definition. See [[package-not-template]].

The chain B1 states and the Exam Alert reproduces: **chart** (the package) → **values**
(configuration) → **templates** (which render manifests) → **Helm release** (an installed
instance).

## Architecture, in one line

Helm *"fetches information from the Kubernetes API server, renders the charts completely
client-side, and stores a record of the installation in Kubernetes."*
`[source: helm-changes-since-helm2-2026-08-31]`

Three consequences worth holding:

- **No server component.** Tiller is gone. See [[tiller]].
- **No `kubectl` in the path.** `helm rollback` does not shell out to `kubectl rollout undo`;
  the two mechanisms never call each other. See [[helm-rollback-versus-rollout-undo]].
- **Manifests go the ordinary way.** *"Charts do not have a private channel into the cluster.
  They generate manifests and the manifests go the ordinary way"* — through the API server,
  as records of intent. See [[kubernetes-object]].

## Why a rendered chart still behaves like everything else

When Helm rolls a release back, it computes the objects the target revision described and
applies them. If that changes a Deployment's Pod template, the Deployment controller starts a
rolling update — *"a **consequence**, in the ordinary reconciling way. Helm did not ask for it.
Helm changed a record of intent, and a controller noticed."* See [[control-loop]].

## ⚠ What the chapter deliberately does not claim

**No frequency claim of any kind.** CNCF publishes the competency name "Application Delivery"
and nothing beneath it; *Helm* appears nowhere in the published curriculum, the exam page, or
the LFS250 outline `[source: cncf-kcna-curriculum-pdf-2026-08-23; lf-kcna-exam-page-2026-08-23;
lf-lfs250-course-outline-2026-08-31]`. The topic list is authored inference and the chapter
says so. See [[published-vs-commonly-reported]].

## Related

[[helm-chart]] · [[helm-release]] · [[values-yaml]] · [[chart-repository]] ·
[[package-not-template]] · [[kustomize]] · [[tiller]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-chart.md ===
# Concept: The Helm chart

**Home:** Chapter 14 §2 · **Competency:** D3.1 · **Status:** canonical

## Definition

★ *"A chart is a collection of files that describe a related set of Kubernetes resources"*,
laid out in a particular directory tree, and packageable into versioned archives for
deployment. *"A single chart might be used to deploy something simple, like a memcached pod, or
something complex, like a full web app stack with HTTP servers, databases, caches, and so on."*
`[source: helm-charts-2026-08-31]`

The directory name is the chart's name without version information — WordPress lives in
`wordpress/`. `[source: helm-charts-2026-08-31]`

★ **The definition says *collection of files*, *versioned*, *deployable*. It does not say
*templated*.** Hold that; [[package-not-template]] is built on it.

## The anatomy, by purpose rather than by name

| Entry | What it is FOR | Required? |
|---|---|---|
| `Chart.yaml` | The chart's identity — name, version, description; also dependencies since Helm 3 | **Yes**, and a version number in it |
| `values.yaml` | The declared surface of variation, with a working default for each knob | conventional |
| `templates/` | What gets created; combined with values, generates valid manifests | conventional |
| `charts/` | Dependency charts. **NOT a repository** | optional |
| `crds/` | Definitions that must exist first; not templated, installed by default | optional |
| `values.schema.json` | ⚠ **A JSON Schema for `values.yaml`** — sourced and **omitted from the chapter** | optional |
| `LICENSE` · `README.md` | optional | optional |

`[source: helm-charts-2026-08-23; helm-glossary-2026-08-31; helm-crd-best-practices-2026-08-31]`

Inside `templates/`, two entries are not manifests: `NOTES.txt` (short usage notes) and
underscore-prefixed files such as `_helpers.tpl`, which *"are assumed to not have a manifest
inside"* and hold reusable partials. `[source: helm-named-templates-2026-08-31]`

## ⚑ The omission, and why it is not cosmetic

**`values.schema.json` returns zero occurrences in the chapter**, despite appearing in the
sourced file-structure list. §2's thesis is that `values.yaml` is *"the declared surface of
variation"* — and `values.schema.json` is the machine-checkable form of that declaration. The
section argues for a declared surface and skips the entry that declares it.

Fix: one gray line in `ch14-fig02` and one clause in §2. The fig02 image-spec is already
scheduled for regeneration ("grey"→"gray", the `crds/` annotation narrowing), so this rides
along free.

## The thesis

**The chart is the unit, and templating is how the unit absorbs variation.** Versioning, a
declared variation surface, and packageability are what make it a chart.

## Related

[[helm]] · [[values-yaml]] · [[chart-repository]] · [[crds-in-charts]] ·
[[chart-version-versus-appversion]] · [[package-not-template]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/values-yaml.md ===
# Concept: `values.yaml` and the override ladder

**Home:** Chapter 14 §2, §3 · **Competency:** D3.1 · **Status:** canonical
**Graded** — Practice Q2, Q5

## What the file is for

*"The default configuration values for this chart."* `[source: helm-charts-2026-08-23]`

The definition undersells it. `values.yaml` is where the chart author states, in one place,
**which things an installer is allowed to change**, and gives each a value that works.

> **Everything in that file is a knob. Everything not in that file is a decision the chart
> author made on your behalf.**

That is failure one from [[four-failures-of-a-manifest-directory]], answered by declaration
rather than by discipline.

## The same move as a ConfigMap, one level up

A ConfigMap externalizes configuration out of the image so the *image* can be
environment-independent. `values.yaml` externalizes variation out of the manifests so the
*manifests* can be. Same principle, different layer. See [[configmap]].

## ★ The override ladder — commit it in this order

1. `values.yaml` — the chart author's defaults
2. `--values` / `-f` — *"can be specified multiple times and the **rightmost file** will take
   precedence"*
3. `--set` — *"If both are used, **`--set` values are merged into `--values` with higher
   precedence**"*

`[source: helm-using-helm-2026-08-31]`

**Rightmost file wins; `--set` beats every file.** The intuition that gets it right: the
command line is the most specific thing you said, so it wins. Practice Q5 grades exactly this,
with distractors inverting each rung.

## ⚠ Do not edit the chart

Overrides are supplied with `-f` or `--set`, which leaves the chart unmodified. **A chart you
have edited in place is no longer the versioned artifact you fetched** — which is the property
packaging exists to give you. Practice Q2 distractor D is the beginner's move and this is why
it is wrong.

## ⚠ Nothing in `values.yaml` becomes an object

It is *input* to rendering. Practice Q3 asks which chart entry contributes no Kubernetes
objects, and `values.yaml` is the answer — note that `charts/` **does** contribute, because a
subchart is still a source of manifests.

## Related

[[helm-chart]] · [[configmap]] · [[helm-release]] · [[base-and-overlay]] — the contrast is that
an overlay has no `values.yaml`, so it can patch anything: more powerful, less guided
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-release.md ===
# Concept: The Helm release

**Home:** Chapter 14 §3 · **Competency:** D3.1 · **Status:** canonical
**Closes B1 trap #80** · **Graded** — TYB (1) Q1, Practice Q6, Q9, Q10

## Definition

★ *"A release is an instance of a chart running in a Kubernetes cluster."*
`[source: helm-architecture-2026-08-31]` When a chart is installed, the Helm library creates a
release to track that installation. `[source: helm-glossary-2026-08-31]`

★ **"The same chart can be installed many times, each creating a separately named release that
can be upgraded and rolled back independently."** `[source: helm-charts-2026-08-23]`

> **The chart is the thing on the shelf. The release is the thing you installed.**

One WordPress chart, three releases — marketing, docs, staging — each with its own name, values
and history. Upgrading one does not touch the others. TYB (1) Q1 grades this; its distractor A
("it also rolls back, because both come from the same chart") is the collapse the whole section
exists to prevent.

## Naming and scoping, both changed in Helm 3

- **A name is required.** Helm 3 *"will throw an error if no name is provided"*; Helm 2's
  auto-naming *"proved to be more of a nuisance than a helpful feature"* in production.
  `--generate-name` opts back in. `[source: helm-changes-since-helm2-2026-08-31]`
- **Releases live in namespaces.** Release information is stored in the same namespace as the
  release, so you can install the same chart in two namespaces and refer to each by changing
  your namespace context. `[source: helm-changes-since-helm2-2026-08-31]` See [[namespace]].
- **`helm list`** lists the releases in your current context's namespace; `--all-namespaces`
  widens it. `[source: helm-changes-since-helm2-2026-08-31]`

★ `helm list` is the answer to the question §1 leaves open — *what is currently installed on
this cluster?* A directory has no such command, **not because nobody wrote one, but because a
directory is not a thing you can ask about.**

## ⚓ Where the state actually lives

**In Secrets, in the namespace of the release, by default.**
`[source: helm-storage-backends-2026-08-31]` Not in a Helm server component — there isn't one —
and not on your laptop. `HELM_DRIVER` selects the backend and accepts `configmap`, `secret`,
or `sql`.

**The implication is larger than the fact.** Helm's record of what it installed is an ordinary
Kubernetes object under the ordinary rules: whoever can read Secrets in that namespace can read
Helm's bookkeeping, and whoever can delete them can make Helm forget. See [[secret]].

*Improvement available:* the chapter cross-bears this to Ch 4 §4 (configuration outside the
image). **Ch 12 §4 owns Secret hardening** and is the better target for a security consequence.

## Related

[[helm]] · [[helm-chart]] · [[helm-release-revision]] · [[helm-rollback-versus-rollout-undo]] ·
[[secret]] · [[namespace]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-release-revision.md ===
# Concept: The release revision

**Home:** Chapter 14 §3 · **Competency:** D3.1 · **Status:** canonical, with two open questions
⚑ **Homonym with the Deployment revision (Ch 6 §5)** — see Canonical forms

## Definition

Installing a chart creates a new release object `[source: helm-using-helm-2026-08-31]`;
upgrading changes it. *"A sequential counter is used to track releases as they change."*
`[source: helm-glossary-2026-08-31]`

Upgrades are not wholesale replacements: `helm upgrade` *"will only update things that have
changed since the last release."* `[source: helm-using-helm-2026-08-31]` Unchanged objects stay
as they are.

## The rollback argument shape

*"The first argument is the name of a release and the second is a revision (version) number; if
this argument is omitted or set to `0`, it will roll back to the previous release."*
`[source: helm-rollback-cli-2026-08-31]` Practice Q7 grades the omitted-argument default.

## ⚑ Two things this corpus CANNOT settle. Do not write either from memory.

1. **Does the counter start at 1 on install?** Figure `ch14-fig03` asserts `rev 1 = install`.
   The corpus supports only *"a sequential counter is used."*
2. **Is a `helm rollback` itself recorded as a new numbered revision?** — i.e. does rolling
   back from rev 3 to rev 2 produce a rev 4 whose content matches rev 2, or move a pointer?

`helm-rollback-cli-2026-08-31` gives argument semantics only.
`helm-using-helm-2026-08-31` is **30 lines** and truncates at the literal word `Example:`,
immediately before the transcript that would show it — verified.

**This is the discriminating detail in §3's central contrast**, and figure `ch14-fig03` puts a
reader-facing **"rev 4 ???"** on the page. Either resolve it with a fetch of
`helm.sh/docs/helm/helm_upgrade/` or the release-lifecycle docs, **or** state the uncertainty in
prose so the question mark reads as deliberate rather than unfinished. Uncertainty handled by
silence plus a question mark is not an uncertainty signal — it is an incomplete figure.

## ⚠ Terminology discipline

The B7 canonical form is **"release revision"** or **"Helm revision"**, never bare "revision",
wherever the Ch 6 §5 sense could be meant. §3's own subsection heading currently uses the bare
form.

⚠ **Helm's own documentation says "previous *release*" where it means the preceding
*revision*** — the exact conflation this section exists to break. Practice A7 reconciles it
four pages later; the reader needs the half-clause where they first meet it.

## Related

[[helm-release]] · [[helm-rollback-versus-rollout-undo]] · [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-rollback-versus-rollout-undo.md ===
# Concept: Two rollbacks wearing one word

**Home:** Chapter 14 §3 · **Competency:** D3.1 · **Status:** canonical
**Discharges** `chapter-06:720` · **Graded** — TYB (1) Q4, Practice Q8, Q9, Exam Alert

## ★ The Fixed Point

**`helm rollback` and `kubectl rollout undo` are different mechanisms wearing the same English
word.** Three axes:

| Axis | `helm rollback` | `kubectl rollout undo` |
|---|---|---|
| **Unit** | a Helm release | one workload object — Deployment, DaemonSet or StatefulSet `[source: k8s-docs-kubectl-rollout-2026-08-24]` |
| **Scope** | everything the chart installed — Deployment, Service, ConfigMap, Ingress | one workload's Pod template |
| **Bookkeeping** | the release record — Secrets in the release's namespace `[source: helm-storage-backends-2026-08-31]` | the Deployment's ReplicaSets |

**Neither calls the other.** Helm renders charts client-side and stores its record in
Kubernetes `[source: helm-changes-since-helm2-2026-08-31]`; there is no `kubectl` in the path.

## 🪢 The scope is in the noun

`helm rollback` takes a **release** name. `kubectl rollout undo` takes a **Deployment** name.
One noun contains many of the other, so the blast radius follows from the grammar.

## The rolling update is a consequence, not a call

When Helm rolls a release back it computes the objects the target revision described and applies
them. If that changes a Pod template, the Deployment controller starts a rolling update **in the
ordinary reconciling way**. *"Helm did not ask for it. Helm changed a record of intent, and a
controller noticed."* See [[control-loop]].

## ⚑ The Kubernetes half is better-sourced than the chapter currently shows

`k8s-docs-deployment-2026-08-23`, § *Rolling back a Deployment*, states verbatim:

> *"A Deployment's revision is created when a Deployment's rollout is triggered — a new revision
> is created **if and only if** the Deployment's Pod template (`.spec.template`) is changed;
> **other updates, such as scaling the Deployment, do not create a Deployment revision.**
> `kubectl rollout undo deployment/<name>` rolls back to the previous revision,
> `--to-revision=<n>` to a specific one."*

The revision stage removed TYB (1) Q4's revision-accounting clause as unsourced, having
consulted only the command-reference snapshot. **This snapshot closes it today, no fetch
required** — and its scaling clause is a stronger rebuttal for distractor B than the one
currently in the answer key. It does **not** source the ReplicaSet scale-up mechanism; leave
that out. `--to-revision=<n>` also pairs neatly with `helm rollback`'s second argument.

## ⚠ Three rollbacks, and the bare noun distinguishes none

Deployment (Ch 6 §5) · Helm release (here) · **rollback by revert** (Ch 15 §4). The ledger
reserves that exact three-word form for the third sense. §3 currently writes it two other ways —
"rollback-by-revert" and "GitOps revert" — in the very section that teaches the discipline.

## Related

[[helm-release-revision]] · [[control-loop]] · [[helm-release]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/chart-repository.md ===
# Concept: The chart repository

**Home:** Chapter 14 §4 · **Competency:** D3.1 · **Status:** canonical
**Closes B1 trap #81** · **Graded** — TYB (1) Q2, Practice Q11

## Definition

★ *"A chart repository is an HTTP server that houses an `index.yaml` file and optionally some
packaged charts."* `[source: helm-chart-repository-2026-08-31]` Managed with the `helm repo`
commands. `[source: helm-charts-2026-08-23]`

**The plainness is the interesting part.** Not a service with an API surface. Not a daemon.
Because it *"can be any HTTP server that can serve YAML and tar files and answer GET requests,
you have a plethora of options for hosting your own."*
`[source: helm-chart-repository-2026-08-31]`

`index.yaml` contains *"metadata about the packages, including the contents of each chart's
`Chart.yaml` file"* `[source: helm-chart-repository-2026-08-31]` — one file telling a client
what the server has and at what versions, without downloading anything else.

A packaged chart is a **chart archive**: *"a tarred and gzipped, and optionally signed, chart."*
`[source: helm-glossary-2026-08-31]`

## ★ The distinction the chapter names twice

| | `charts/` | chart repository |
|---|---|---|
| What | a **directory inside a chart** | an **HTTP server on the network** |
| Holds | the charts this chart depends on | packaged charts + an index |
| Role | a component of a package | a place packages are kept |

**Same word, opposite ends of the pipeline.** B1 trap #81, and the chapter flags it in §2 and
again in §4 on purpose.

## ⚠ A third surface form, unreconciled

§4 quotes Helm's own text using **"Helm repositories"** twice, without reconciling it against
the chapter's headword "chart repository." In a chapter that spends two 🪝 Snags teaching that
`charts/` is not a repository, introducing a third form uncommented is a small self-inflicted
wound. One clause fixes it.

## ⚠ `helm pull` is missing

B6 assigns §4 *"`helm repo` and `helm pull`."* The chapter covers `helm repo`, demonstrates
`helm push`, and never mentions `helm pull`.

## Related

[[helm-chart]] · [[oci-registry-as-chart-store]] · [[registry]] · [[distribute-versus-adapt]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/oci-registry-as-chart-store.md ===
# Concept: An OCI registry holds more than images

**Home:** Chapter 14 §4 · **Competency:** D3.1 (interleaves D1.4) · **Status:** canonical
**Graded** — Practice Q12 `[interleaved: D1.4]`, Q17

## The Chapter 2 payoff

Re-read the OCI's own definition with fresh eyes: a registry is ★ *"a service that handles the
required APIs defined in this specification."* `[source: oci-distribution-spec-2026-08-24]`

**Not "a service that stores images."** A service that implements an API for distributing
*content*. The spec defines *"an API protocol to facilitate and standardize the distribution of
content"* — with no requirement that the content be an image. That distinction was doing quiet
work in Chapter 2 all along. See [[registry]] · [[oci]].

## What follows

*"With the release of Helm 3.8.0, Helm is able to store and work with charts in container
registries, as an alternative to Helm repositories."* Since OCI artifacts make it possible to
store more than container images, *"you can store charts, images, and other artifacts in a
single OCI registry."* `[source: helm-blog-oci-ga-2026-08-31]` The documentation now
**recommends** it. `[source: helm-oci-registries-2026-08-31]`

**Structure:** an OCI-based registry can contain zero or more Helm repositories, each containing
zero or more packaged charts. `[source: helm-oci-registries-2026-08-31]`

**Reference form:** the reference must be prefixed with `oci://`; on push it must not contain
the basename or tag, because the basename is inferred from the chart's name and the tag from
its semantic version. `[source: helm-oci-registries-2026-08-31]`

## Why they moved — the project's own reasoning

Chart repositories had *"a very hard time abstracting most of the security implementations
required in a production environment"*; provenance signing was optional rather than integral;
the same chart uploaded by two tenants cost twice the storage; and a single index file serving
search, metadata and fetching was clunky to design around securely. Meanwhile the Distribution
project had *"many years of hardening, security best practices, and battle-testing"* and was
offered as a product by many major cloud vendors.
`[source: helm-changes-since-helm2-2026-08-31]`

★ **Rather than reinvent a hardened content-distribution service, Helm moved onto the one the
industry had already built.** Standardization at the OCI layer bought something nobody was
aiming at when the distribution spec was written.

## ⚠ `helm push` is graded and under-taught

Practice Q17's correct answer includes *"must not contain the basename or tag on push"*, which
§4's prose conveys only obliquely. And the command name `helm push` appears **once** in the
chapter — inside that question's own answer key. State the clause and name the command in §4.

## Related

[[registry]] · [[oci]] · [[chart-repository]] · [[tag-vs-digest]] · [[image-reference]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/chart-version-versus-appversion.md ===
# Concept: Chart version vs `appVersion`

**Home:** Chapter 14 §4 · **Competency:** D3.1 · **Status:** ⚠ **PROVISIONAL — UNSOURCED**
**Graded once** — TYB (1) Q5

## The distinction

The chart's **`version`** tracks *the packaging*. It moves when the packaging changes: a
template fixed, a default adjusted, a new value exposed. Charts are *"versioned according to the
SemVer 2 specification"*, and **a version number is required on every chart**.
`[source: helm-glossary-2026-08-31]` — **this half is sourced.**

**`appVersion`** is the version of *the application the chart installs*. — **this half is not.**

They move independently. You can ship chart 4.1.2 and 4.1.3 that both install nginx 1.25.3,
because what changed was the chart. You can ship chart 5.0.0 installing nginx 1.26.0, where both
changed at once.

🪢 **Version is the box; `appVersion` is what's in the box.** You can redesign the box without
changing the contents, and change the contents without redesigning the box.

## ⚠⚠ THE HIGHEST-SEVERITY GAP IN CHAPTER 14

**The string `appVersion` appears in ZERO of the corpus's 214 snapshots.** Verified
independently, not inherited from the draft's flag.

- `helm-glossary-2026-08-31` defines *Chart Version* and stops.
- `helm-charts-2026-08-31` is **18 lines** and truncates at *"Helm will expect a structure that
  matches this:"* — immediately before the `Chart.yaml` field table that carries it.
- `helm-charts-2026-08-23` gives the file-structure list and no field table.
- Three snapshots list `chart-version-versus-appversion` in `concepts_covered` with no body
  text. **That is not a citation.**

**Assertion sites:** §4's closing subsection · the 🪢 Mnemonic · **TYB (1) Q5 and its answer
key** · the Chapter Summary row · the Exam Alert trap table. Draft-v1 asserted it a sixth time
in Practice Q13; the revision stage re-aimed that item at Kustomize generators, correctly
halving the graded footprint from two items to one.

**FIX:** re-fetch `helm.sh/docs/topics/charts/` and **extend the existing snapshot past its
truncation point** — the page enumerates `version` and `appVersion` and states that `appVersion`
is not related to the `version` field. Do not open a new snapshot; extend that one. The same
fetch closes [[helm-chart]]'s subchart gap.

**If the fetch does not land before ship:** cut TYB (1) Q5 and reduce §4 to the sourced half.
This is the one place in an otherwise scrupulously-tagged chapter where a graded item rests on
nothing.

## Related

[[helm-chart]] · [[values-yaml]] · [[tag-vs-digest]] — the same *identity vs pointer* instinct,
one layer up
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/tiller.md ===
# Concept: Tiller, and reading a source's date off its content

**Home:** Chapter 14, Exam Alert · **Competency:** D3.1 · **Status:** canonical
**Graded** — Practice Q6 distractor A, Practice A10 · ⚠ **no B7 ledger row**

## What it was, and why it went

Tiller was **Helm 2's in-cluster component**, introduced so that multiple people could interact
with the same set of releases. With RBAC enabled by default from Kubernetes 1.6, locking it down
for production *"became difficult to manage"*, and the permissive default configuration *"could
grant users a far broader range of permissions than intended."*

★ *"One of the first decisions we made regarding Helm 3 was to completely remove Tiller."*
Helm 3 stores release records in Kubernetes directly and evaluates permissions through your
kubeconfig instead. `[source: helm-changes-since-helm2-2026-08-31]`

## ★ Why this earns a place in a book that is not a Helm manual

**Tiller is a dating stamp.** A study resource that explains how to secure it is describing a
Helm that Helm 3 removed — which is reason enough to read carefully whatever else it tells you
about this domain.

This is the strongest available instance of the chapter's ethics posture: it offers a
**checkable fact** as a currency test rather than a claim about a competitor's quality, and the
inference it draws is hedged and earned. It does not strawman alternative study material; it
hands the reader a test they can run themselves.

## ⚠ Two things not to say

1. **Do not date the Helm 3 release.** Draft-v1's *"a Helm that has not existed since 2019"*
   appeared twice and was cut both times: the corpus dates no Helm 3 release, and the sourced
   marker does the same work without a year. Restoring it needs the Helm 3.0 GA announcement
   (**G-14f**, cosmetic).
2. **Do not pair it with a weight claim.** The Exam Alert's original phrasing leaned on
   "this domain doubled in weight" to sharpen the outdated-material argument. That claim is
   unsupported and, worse, its apparent source disclaims it. See
   [[domain-weights-44-28-16-12]] and [[published-vs-commonly-reported]]. The Tiller argument
   stands perfectly well on its own.

## ⚠ Canonical-forms breach at this entry's source sentence

The chapter writes *"so multiple **operators** could interact with the same set of releases."*
The B7 canonical-forms table carries an explicit prohibition — **never use "operator" for a
person** — and this same chapter uses "operator" correctly for *software* in §6 (*"Operators
shipped as charts run into this constantly"*), so the two senses collide inside one chapter.
Fix to *"so that multiple people could interact."* See [[operator-pattern]].

## Related

[[helm]] · [[helm-release]] · [[secret]] · [[rbac]] · [[published-vs-commonly-reported]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kustomize.md ===
# Concept: Kustomize

**Home:** Chapter 14 §5 · **Competency:** D3.1 · **Status:** canonical
**Closes B1 research gap G19** · **Graded** — TYB (2) Q1, Q2, Practice Q13–Q16

## Definition

★ *"Kustomize introduces a template-free way to customize application configuration."*
`[source: kustomize-overview-2026-08-23]` A standalone tool for customizing Kubernetes objects
through a kustomization file `[source: k8s-docs-kustomization-2026-08-31]`, and ★ *"built into
kubectl as `apply -k`"* `[source: kustomize-overview-2026-08-23]`. kubectl has supported
kustomization files since Kubernetes 1.14. `[source: k8s-docs-kustomization-2026-08-31]`

## Two independent claims — hold them separately

**Template-free.** There are no placeholders. Each manifest is an ordinary, valid, applyable
Kubernetes object; `kubectl apply -f base/deployment.yaml` works with **no rendering step,
because there is nothing to render.** TYB (2) Q1 distractor D ("renders the base through a
template engine using the overlay as values") exists solely to catch readers who filed Kustomize
as "Helm with different syntax."

*(The `kustomization.yaml` beside those manifests is Kustomize's own object, and is the one file
the API server will not take — the API server serves the kinds it knows about, and nothing
else.)*

**Built into kubectl.** No engine to install, no client to distribute, no version to keep in
step. **If a machine has kubectl, it has Kustomize.** Graded at TYB (2) Q2 — and note that a
standalone binary *does* exist `[source: k8s-docs-kustomization-2026-08-31]`, which is what
makes distractor A half-true and wrong where it counts.

## The move that is actually different

| | Helm | Kustomize |
|---|---|---|
| The artifact in your repo | **not** a valid Kubernetes object — a template that becomes one | a valid Kubernetes object throughout |
| The transformation | non-object → object (render) | object → object (patch) |
| Can a newcomer read it? | needs the template language | opens `base/deployment.yaml` and understands it |
| Is the variation surface declared? | **yes** — `values.yaml` | **no** — an overlay can patch anything |

More powerful, less guided. Neither column is a defect; §6 is about which side you want to be
standing on. See [[distribute-versus-adapt]].

## ⚠ B1 budgeted one paragraph; the chapter spends two sections

G19 reads: *"Kustomize. Named inside the Argo CD and Helm-adjacent material as a manifest
source, never explained. Overlay/base model is worth one paragraph."* Chapter 14 gives §5 and
§6. **Defensible, and load-bearing:** a chapter with one Kustomize paragraph could not have made
§7's argument that templating is not the definition. Recorded so the coverage audit reads the
over-delivery as deliberate.

## Related

[[base-and-overlay]] · [[kustomization-fields]] · [[strategic-merge-versus-json-patch]] ·
[[distribute-versus-adapt]] · [[package-not-template]] · [[helm]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/base-and-overlay.md ===
# Concept: Base and overlay

**Home:** Chapter 14 §5 · **Competency:** D3.1 · **Status:** canonical
**Graded** — TYB (2) Q1 (keyed correct), Practice Q16

## The arrangement

A fork/modify/rebase workflow: a **base** directory holds the upstream manifests and a
`kustomization.yaml`; **overlays** (dev, staging, prod) reference the base and layer *"patches,
name prefixes and suffixes, labels, images, and generated ConfigMaps and Secrets"* on top. This
manages any number of distinctly customized configurations ★ **"without forking the
originals."** `[source: kustomize-overview-2026-08-23]`

> **The base is not edited. The base is not copied. Each overlay declares only its own
> differences and points at the base it differs from.**

*A fixed reference, and a declared offset from it.*

## ★ Why "without forking" is the whole claim

If an overlay copied its base you would be back at failure one from
[[four-failures-of-a-manifest-directory]] — two directories, 95% identical, and nothing marking
the 5%. If an overlay *edited* its base, the base would become environment-specific, defeating
the arrangement entirely.

TYB (2) Q1's distractors are exactly those two wrong models plus the template-engine model. All
three are worth knowing by name.

## How a patch finds its target

By identity: `apiVersion`, `kind`, and `metadata.name`. That is how Kustomize knows which base
object a delta belongs to. See [[kubernetes-object]].

## ⚠ No version, and that is the premise not the gap

A Kustomize base has no version and no repository — a stranger has nothing to pin and nowhere to
fetch from. **Git supplies the identity**, which is why Practice Q16's distractor D ("overlays
remove the need to keep the base under version control") inverts the arrangement so badly: the
base is the thing that most needs a version. That job belongs to Chapter 15.

## Related

[[kustomize]] · [[kustomization-fields]] · [[four-failures-of-a-manifest-directory]] ·
[[distribute-versus-adapt]] · [[declarative-configuration]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kustomization-fields.md ===
# Concept: What a kustomization can declare

**Home:** Chapter 14 §5 · **Competency:** D3.1 · **Status:** canonical
**Graded** — Practice Q13, Q14

## The kustomization is itself an object

The kustomization file *"is itself a YAML specification of a Kubernetes Resource Model object
called a Kustomization"*, and a kustomization *"describes how to generate or transform other
objects."* `[source: kubectl-book-kustomization-fields-2026-08-31]`

**The customization instructions are an object of a declared kind, not a script.** Worth
noticing in a book that has spent thirteen chapters on records of intent.

## The four groups

`[source: kubectl-book-kustomization-fields-2026-08-31]`

**What to include** — `resources` names the base plus any manifests belonging to this overlay
alone. *(The list also carries the older `bases`, "add resources from a kustomization dir";
kustomizations in the wild use either, and modern ones list the base under `resources`.)*

**Blanket transformations** — `namespace` · `namePrefix` / `nameSuffix` · `labels` ·
`commonAnnotations` · `images` (modifies name, tags and/or digest) · `replicas`.

**Targeted patches** — `patches` · `patchesStrategicMerge` · `patchesJson6902`.
See [[strategic-merge-versus-json-patch]].

**Generators** — `configMapGenerator` · `secretGenerator` · `generatorOptions`.

## ★ Two fields that repay attention

**`namePrefix` updates names *and references*.** That clause is load-bearing: a prefixed
Deployment still finds its prefixed ConfigMap, because **Kustomize understands the
relationships, not just the strings.** Practice Q14 keys on it, with `images` and `resources` as
the near-miss distractors.

**The generators belong in the overlay, not the base.** ConfigMaps and Secrets are the objects
that vary most between environments, so generating them in the overlay *"puts the most
environment-specific objects in the layer that is **about** environment specificity."* Practice
Q13 grades the reasoning, not the syntax. See [[configmap]] · [[secret]].

The label transformer is Chapter 4's machinery applied across an overlay, with selectors updated
to match. See [[label-selector]].

## 🔭 `helmCharts`

*"A Helm chart inflation generator"* `[source: kubectl-book-kustomization-fields-2026-08-31]` —
Kustomize can render a chart and patch the output. **The two tools are not mutually exclusive at
the mechanical level**, whatever the arguments online suggest, and §6's "commonest production
shape" depends on it. ⚠ No ledger row, and it reaches a graded answer key (Practice A13
distractor D).

## ⚠ Omitted deliberately

The name-hash suffix `configMapGenerator` appends is **not stated**; no snapshot covers it, and
draft-v1 correctly omitted it rather than asserting it. Contrast the handling of the patch
semantics, which were asserted — see [[strategic-merge-versus-json-patch]].

## Related

[[kustomize]] · [[base-and-overlay]] · [[strategic-merge-versus-json-patch]] · [[configmap]] ·
[[label-selector]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/strategic-merge-versus-json-patch.md ===
# Concept: The two patch styles

**Home:** Chapter 14 §5 · **Competency:** D3.1 · **Status:** ⚠ **PROVISIONAL — AUTHORED**
**Graded once** — Practice Q15

## What the corpus actually supplies

`kubectl-book-kustomization-fields-2026-08-31` gives the field names and two bare strings:
`patchesStrategicMerge` patches *"using the strategic merge patch standard"*, and
`patchesJson6902` *"using the json 6902 standard."* **That is all.**

## What the chapter adds — one clause each, authored

- **Strategic merge patch:** a *fragment of the object that looks like the object*. You write
  the piece of the Deployment you want to change, in the same shape, and Kustomize merges it in.
- **JSON patch:** a *list of explicit operations on paths* — replace this path, add to that
  array, remove this element.

Strategic merge reads more naturally and handles most cases; JSON patch is for surgical
precision, particularly on list elements where merge semantics get ambiguous.

## ⚠ The status, stated plainly

**Both semantics are authored, and Practice Q15 grades them.** Q15's distractor B inverts the
pair exactly — it calls the merge patch the one that must restate the whole object — which is
the plausible error and the reason the item is worth keeping.

Draft-v1 additionally expanded "JSON 6902" to *"JSON Patch, RFC 6902"*. **That expansion was
removed and should stay removed**: the RFC number was asserted from nothing.

**Two honest options:** (a) fetch the full kubernetes.io kustomization task page and tag both
clauses; (b) cut the paragraph **and** Q15 together. Do not keep the item and drop the
paragraph, or vice versa.

**Instructive contrast within the same section.** `configMapGenerator`'s name-hash suffix was
the same kind of well-known-but-unsourced detail, and draft-v1 *omitted* it. Two adjacent
decisions, opposite calls. The omission is the one that matches this chapter's stated posture.

## Both target by identity

Either style targets an object by `apiVersion`, `kind`, and `metadata.name` — that part is not
in dispute and follows from [[kubernetes-object]].

## Related

[[kustomization-fields]] · [[kustomize]] · [[base-and-overlay]] · [[kubernetes-object]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/crds-in-charts.md ===
# Concept: Why charts have a `crds/` directory

**Home:** Chapter 14 §6 · **Competency:** D3.1 · **Status:** canonical
**Discharges** `chapter-06:1036` · **Anchors Ch 17 §4** · **Graded** — TYB (2) Q3, Practice Q1, Q3

## The rule that forces it

★ *"For a CRD, the declaration must be registered before any resources of that CRDs kind(s) can
be used."* `[source: helm-crd-best-practices-2026-08-31]` There is the declaration — the YAML
with kind `CustomResourceDefinition` — and then resources that *use* it.

**This is not a preference.** Until the CRD is registered, the custom kind does not exist as far
as the API server is concerned, and an object of that kind is not "not ready yet." **It is
invalid.** There is no reconciliation to wait for; there is only an error. See
[[custom-resource]].

## Why a directory rather than one more template

A chart's templates render to a stream of manifests. If the CRD were merely one more file in
`templates/`, whether it landed first would be a matter of luck. That is failure two from
[[four-failures-of-a-manifest-directory]] — **and the one case where the absence of an ordering
guarantee is fatal rather than merely slow.**

★ *"`crds/` is a special directory you can create in your chart to hold your CRDs; these CRDs
are **not templated**, but will be **installed by default** when running a `helm install` for
the chart."* `[source: helm-crd-best-practices-2026-08-31]`

Not templated → nothing to render and nothing to sequence within. Installed by default → getting
them in is the tool's responsibility rather than the README's.

## ⚠ Three documented limits

- `--skip-crds` skips the CRD installation step.
- ★ **There is no support at this time for upgrading or deleting CRDs using Helm.**
- `--dry-run` is not currently supported for CRDs.

`[source: helm-crd-best-practices-2026-08-31]`

**The middle one is the production trap** and TYB (2) Q3 grades it. A chart with a `crds/`
directory installs its CRDs on first install and does not update them on upgrade. If the next
chart version ships a CRD with new fields, **the release upgrades cleanly and the new feature
silently does not work**, because the API server is still serving the old schema.

The restriction is defensible: a CRD's removal or downgrade reaches every object of that kind in
the cluster. Helm declining to automate that is a decision, not an oversight.

**Second approach:** put the CRD in one chart and the resources that use it in another — *"more
useful for cluster operators who have admin access to a cluster."*
`[source: helm-crd-best-practices-2026-08-31]`

## Forward anchor — do not drop

**Ch 17 §4** collects the pluggable interfaces, and CRDs-shipped-as-chart-content is where the
extension mechanism and the packaging mechanism visibly interact. B6 records this pointer as
**pinned by shipped text** and therefore immovable. See [[pluggable-interfaces]].

## Related

[[custom-resource]] · [[helm-chart]] · [[pluggable-interfaces]] ·
[[four-failures-of-a-manifest-directory]] · [[operator-pattern]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/distribute-versus-adapt.md ===
# Concept: What the Helm-versus-Kustomize choice turns on

**Home:** Chapter 14 §6 · **Competency:** D3.1 · **Status:** canonical
**Graded** — TYB (2) Q4, Practice Q16

## The question, asked properly

Not a preference poll, not a maturity ladder, not a tribal marker. One question:

> ★ **Are you distributing software to people who will not read it, or adapting software you
> already have for environments you control?**

## Distributing → Helm

A stranger needs, and packaging supplies, exactly the four things §1 named:

| A stranger needs | Helm supplies | Source |
|---|---|---|
| a name and a version to pin | `Chart.yaml`, and **requires** the version | `helm-glossary-2026-08-31` |
| somewhere to fetch it without cloning your repo | a chart repository or an OCI registry | `helm-chart-repository-2026-08-31` · `helm-oci-registries-2026-08-31` |
| to know which parts are theirs to change | `values.yaml`, as a **declared** surface | `helm-charts-2026-08-23` |
| install / upgrade / undo as single acts | the release model | `helm-architecture-2026-08-31` |

★ **Which is why an operator, a controller, an ingress controller or a monitoring stack is
almost always shipped as a chart.** Not because templating is superior — **because the recipient
is a stranger, and everything a stranger needs is packaging.**

## Adapting → Kustomize

There is nobody to distribute to. The manifests are yours, they live in your repository, and the
people changing them can read them. A template engine is then overhead: it makes your artifacts
un-readable-as-manifests to buy a distribution capability you are not using.

## They combine, and that is the normal case

Take somebody's chart for third-party components, use Kustomize for your own applications, and
where a chart's values do not expose what you need, let Kustomize inflate the chart and patch
the result. `[source: kubectl-book-kustomization-fields-2026-08-31]`

*"This is not a compromise position. It is what 'package' and 'adapt' look like when both are
happening in the same repository, which is most of the time."*

## The four, closed — and note the shape of the second column

| Failure | Helm | Kustomize |
|---|---|---|
| Environment variation | `values.yaml` | overlays |
| Apply ordering | `crds/` | — (`apply -k` is still an apply) |
| Versioning | required chart version; `helm list` | — (Git supplies it; Ch 15) |
| Distribution | repositories and OCI registries | — (nothing to distribute; that is the premise) |

**Kustomize answers one cleanly, declines two by design, and shares the fourth's limitation.**
Not a deficiency — a smaller tool solving the subset of the problem that occurs when there is
nobody to distribute to.

## Related

[[four-failures-of-a-manifest-directory]] · [[helm]] · [[kustomize]] · [[chart-repository]] ·
[[package-not-template]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/package-not-template.md ===
# Concept: A package, not a template ☀️

**Home:** Chapter 14 §7 (the Zenith) · **Competency:** D3.1 · **Status:** canonical
**Closes B1 trap #79** · **Feeds Ch 15 §7**

## The move

> **You have been taking the sight from too low.**

Helm and Kustomize disagree about mechanism as completely as two tools can. One makes the
manifest incomplete and completes it from values; the other keeps the manifest complete and
describes differences against it. One has a template engine; the other advertises the *absence*
of one as its headline feature `[source: kustomize-overview-2026-08-23]`. **If mechanism were
the axis, they would be opposites.**

★ **They agree about everything that matters.** Both exist to take a directory of loose files
and turn it into **one addressable unit**: a thing with a name, a thing that installs as a
single act, a thing whose differences across environments are declared in one place rather than
scattered through copies.

**Neither was aiming at templating.** Templating is a thing Helm happens to use on the way.

So the argument the ecosystem spends its energy on — templating versus not, engine versus no
engine — *"is an argument about **how**, conducted between two tools that had already agreed on
**what**. And the **what** is the part that changes how you work."*

## Why this is the answer to B1 trap #79

Trap #79 is "Helm is a templating engine." The usual correction is to recite the definition.
**The chapter proves it instead**: a tool exists that solves the same problem with no templating
at all, and therefore templating was never the definition. That is a structural refutation, and
it is why §5 and §6 had to be as long as they are.

## The symmetry with Chapter 4

A Kubernetes object is a **record of intent** — a durable declaration of what should be true,
which controllers work to make true. See [[kubernetes-object]] · [[control-loop]].

★ **A package is that same move, one level up:** a durable declaration of what a whole
application should be, with a version number so you can say *which* declaration, and a name so
you can ask what happened to it. **Not a bigger object. The same idea applied to the set.**

## The question it leaves open — deliberately

You have a unit. It installs as one act and undoes as one act. **Who runs the install? When?
Triggered by what? From where?**

So far: a person, at a keyboard, with cluster credentials on their laptop. *"Packaging solved
**what you hand over**. It solved nothing at all about **how it gets applied and stays
applied**."*

⚑ **Ch 15 §7's control-loop payoff is correctly left unspent.** Chapter 14 sets the frame and
declines to reach for the synthesis Ch 15 is holding — the same discipline Chapter 13 showed.
See [[control-loop]].

## Related

[[kubernetes-object]] · [[control-loop]] · [[declarative-configuration]] ·
[[distribute-versus-adapt]] · [[four-failures-of-a-manifest-directory]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

---

## Chapter 14 §1 — the debt, collected

Chapter 14 opens by naming every instance of this pattern the book has accumulated, and treating
the accumulation itself as the problem:

> *"Install a CNI plugin, because the network model requires one and Kubernetes does not ship
> one. Install an Ingress controller, because the Ingress object does nothing without one.
> Install a CSI driver. Install metrics-server, or `kubectl top` will keep failing… **Not one
> of those chapters said how.**"*

**The pattern's cost, stated for the first time.** Every instance of "an object without its
component does nothing" generates an installation obligation, and thirteen chapters of them
generated thirteen obligations with no vocabulary for discharging any. That is
[[four-failures-of-a-manifest-directory]]'s failure four — distribution — arriving as a book
structure rather than as a tool limitation.

### ⚑ GOOD NEWS for the form conflict this shard has been tracking

Ch 11's block ruled that *"an object without its component does nothing"* is **the rule
sentence** (shipped Ch 3, Ch 10, Ch 11; verbatim in all four options of Ch 10 Practice Q18) and
that the B7 form — *"The object exists; nothing happens without the component"* — has **zero
occurrences in shipped text: do not adopt.** Ch 13's block then found that shipped Ch 13 adopted
it anyway.

**I re-verified: `chapter-13:1279` still carries the ledger form. That fix was never applied.**

**Chapter 14 does not repeat it.** §1 writes *"the Ingress object does nothing without one"* —
Ch 10's form, applied rather than quoted, with the correct cross-bearing to Ch 10 §3. Chapter 14
needs no change on this axis.

**Tally, for the Ch 17 §4 collection stage:**

| Form | Where |
|---|---|
| **Rule sentence** (canonical, graded) | shipped Ch 3, Ch 10, Ch 11, **Ch 14** |
| Ledger form (zero graded occurrences) | B7 ledger · B3's summary · **shipped Ch 13:1279** |

The drift is confined to one shipped chapter. **The artifacts should move toward the book, not
the book toward the artifacts.** Note that B3's own recovered summary also uses the ledger form,
which is likely how it reached Ch 13.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

---

## Chapter 14 §3, §7 — a controller noticed, and a package is the same move one level up

**§3 uses the loop to disarm the chapter's central trap.** When Helm rolls a release back it
computes the objects the target revision described and applies them. If that changes a
Deployment's Pod template, the Deployment controller starts a rolling update:

> *"The rolling update is a **consequence**, in the ordinary reconciling way. **Helm did not ask
> for it. Helm changed a record of intent, and a controller noticed.**"*

That is what makes `helm rollback` and `kubectl rollout undo` genuinely different mechanisms
rather than one wrapping the other — Helm never enters the workload path at all. See
[[helm-rollback-versus-rollout-undo]].

**§7 extends the loop's own framing to the packaging layer:**

> *"A Kubernetes object is a record of intent… **A package is that same move, one level up:** a
> durable declaration of what a whole application should be, with a version number on it so you
> can say *which* declaration, and a name so you can ask what happened to it. **Not a bigger
> object. The same idea applied to the set.**"*

**No ordinal is asserted.** Per this shard's standing ruling and the Ch 8 gate's "state the
pattern, never the count" convention, Chapter 14 states the pattern and points.

⚑ **One thing for the author, not a rule breach.** The Voyage Ahead enumerates three prior
sightings — *"a Deployment toward its spec, a scheduler toward a placement, a claim toward a
volume"* — and then names Ch 15 as the saved one. No number is stated, so the convention holds
to the letter. But the enumeration makes the arithmetic visible against shipped Ch 6's *"the
third time is the one that matters,"* since Ch 7 and Ch 11 added sightings after Ch 6 spoke.
**The defect, if any, is in shipped Ch 6.** Cheapest fix here is to de-enumerate:
*"You have watched the control loop reconcile toward specs, placements, and volumes."*
Author's call.

⚑ **Ch 15 §7's payoff is left unspent**, correctly. Chapter 14 sets the frame and stops.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/custom-resource.md ===

---

## Chapter 14 §1, §6 — registration-before-use, as a packaging problem

Chapter 14 takes the registration rule the reader already knows and shows what it costs a
distribution mechanism.

**§1 uses it as the sharpest case of apply-ordering.** Apply a `PostgresCluster` before the CRD
that defines it and *"the API server does not queue your object for later. It rejects it…
**There is no reconciliation to wait for. There is only an error.**"* Eventual consistency covers
a great many ordering sins; it does not cover this one, because the object is not *pending* — it
is **invalid**.

**§6 gives the rule in the Helm project's own words:** *"For a CRD, the declaration must be
registered before any resources of that CRDs kind(s) can be used."*
`[source: helm-crd-best-practices-2026-08-31]`

**And draws the consequence for packaging:** a chart's templates render to a stream of manifests,
so a CRD sitting in `templates/` would land in an order decided by luck. Helm therefore carves
out `crds/` — not templated, installed by default. See [[crds-in-charts]] for the three
documented limits, of which *no support for upgrading or deleting CRDs* is the one that catches
teams in production.

**Chapter 14 adds one thing this shard did not hold:** the registration obligation has an owner.
*"Somebody has to do that registering: a cluster administrator, or an operator's installation
procedure. Custom kinds do not exist until their definitions do."* That is where the CRD story
meets the packaging story, and Ch 17 §4 collects it.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/declarative-configuration.md ===

---

## Chapter 14 §1 — where `kubectl apply -f` stops, named precisely

This shard has held what declarative object configuration *does*. Chapter 14 is the first to
state, in four named parts, what it structurally **cannot** do — and it opens by defending the
technique rather than undermining it:

> *"For a single application on a single cluster maintained by a single person, this is not a
> compromise or a stepping stone. **It is correct, and you should keep doing it.**"*

Then: *"It stops working in four specific places. Not 'gets awkward' — **stops**."*

1. **Environment variation** — replica counts, image tags and resource limits are fields in the
   manifest, not configuration the application reads. A directory's only answer is another
   directory, and *"nothing in the system knows"* the two must stay in sync.
2. **Apply ordering** — `apply -f` promises nothing about order. See [[custom-resource]].
3. **Versioning** — a directory has no version, so *"what is currently installed?"* has no
   answer, and there is no unit to undo.
4. **Distribution** — *"every installation is a small act of comprehension."*

Full treatment at [[four-failures-of-a-manifest-directory]].

★ **The framing worth carrying forward:** the directory *"is the correct answer to 'how do I
describe what should be running.' It is the wrong answer to 'how do I give this to someone
else.'"* Not a technique being outgrown — a technique asked to do a job one size larger than the
one it was designed for.

⚠ **`eventual consistency` is used load-bearing here and in §6 with no definition, no ledger row
and no ambient-tier assignment.** It carries a precise distributed-systems meaning. Assign it or
gloss it before the glossary build.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/registry.md ===

---

## Chapter 14 §4 — the definition was never about images

Chapter 2 established the registry as where container images live. Chapter 14 re-reads the same
sourced sentence and finds it says something larger:

> ★ *"a service that handles the required APIs defined in this specification"*
> `[source: oci-distribution-spec-2026-08-24]`

**Not "a service that stores images." A service that implements an API for distributing
*content*.** *"That distinction was doing quiet work all along."*

What follows: *"With the release of Helm 3.8.0, Helm is able to store and work with charts in
container registries, as an alternative to Helm repositories"*, and *"you can store charts,
images, and other artifacts in a single OCI registry."*
`[source: helm-blog-oci-ga-2026-08-31]` The Helm docs now **recommend** it.
`[source: helm-oci-registries-2026-08-31]`

An OCI-based registry can contain zero or more Helm repositories, each containing zero or more
packaged charts. `[source: helm-oci-registries-2026-08-31]` Reference form: `oci://` prefix; on
push, no basename and no tag, both inferred from the chart's name and semantic version.

**This is the book's best-executed delayed payoff.** Chapter 2 taught a definition precisely;
twelve chapters later the precision turns out to have been load-bearing, and the reader who read
carefully gets the reward. See [[oci]] · [[oci-registry-as-chart-store]].
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/oci.md ===

---

## Chapter 14 §4 — standardization bought something nobody was aiming at

The OCI Distribution Specification defines *"an API protocol to facilitate and standardize the
distribution of content"* `[source: oci-distribution-spec-2026-08-24]` — **content**, addressed
by digest, with no requirement that it be an image. Helm charts now travel that way.

**The project wrote down its reasoning, and it is the more instructive half.** Chart
repositories had *"a very hard time abstracting most of the security implementations required in
a production environment"*; provenance signing was optional rather than integral; the same chart
uploaded by two tenants cost twice the storage; and a single index file serving search, metadata
and fetching was clunky to design around securely. Meanwhile the Distribution project — the
successor to the original Docker Registry — had *"many years of hardening, security best
practices, and battle-testing"* behind it, offered as a product by many major cloud vendors.
`[source: helm-changes-since-helm2-2026-08-31]`

★ *"Rather than reinvent a hardened content-distribution service, Helm moved onto the one the
industry had already built."*

**The transferable lesson, and it is an architecture lesson rather than a Helm one:** a
specification written for one artifact type, if it is honestly general, gets reused for artifact
types its authors did not anticipate. *"Standardization at the OCI layer turned out to buy
something nobody was specifically aiming at when the distribution spec was written."*

Graded at Practice Q12, `[interleaved: D1.4]` — one of the chapter's three genuine backward
reaches, and the only one tagged to Containerization.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/configmap.md ===

---

## Chapter 14 §2, §5 — the same externalization move, twice more

**§2 — `values.yaml` is a ConfigMap's move one level up.**

> *"A ConfigMap externalizes configuration out of the image so the image can be
> environment-independent. **`values.yaml` externalizes variation out of the manifests so the
> *manifests* can be environment-independent.** Same principle, different layer."*

The chapter also sharpens the boundary this shard has always implied. The reader knows
configuration goes in ConfigMaps — but *"the replica count is not configuration the application
reads. It is a field in the Deployment's spec. So is the resource limit. So is the image tag."*
**ConfigMaps solve config-in-the-image; they do not solve variation-in-the-manifest.** That
distinction is what makes packaging a separate problem rather than a ConfigMap problem, and it
is the cleanest statement of it in the book. See [[values-yaml]].

**§5 — `configMapGenerator`, and why it belongs in the overlay.**

`configMapGenerator` *"generates ConfigMap resources"* and `secretGenerator` generates Secrets,
from literal values or files on disk, rather than requiring a hand-authored object with its
`data` map. `[source: kubectl-book-kustomization-fields-2026-08-31]`

The argument is better than the convenience: *"ConfigMaps and Secrets are precisely the objects
that vary most between environments"*, so generating them in an overlay *"puts the most
environment-specific objects in the layer that is **about** environment specificity."* Graded at
Practice Q13, which keys on that reasoning rather than on the syntax.

⚠ The name-hash suffix these generators append is deliberately unstated — no snapshot covers it.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/secret.md ===

---

## Chapter 14 §3 — Helm's bookkeeping is an ordinary Secret

**Where a Helm release's state lives: in Secrets, in the namespace of the release, by default.**
`[source: helm-storage-backends-2026-08-31]` Not in a Helm server component — there isn't one,
since Helm 3 removed Tiller — and not on the client machine. The `HELM_DRIVER` environment
variable selects the backend and accepts `configmap`, `secret`, or `sql`.

★ **The consequence is a security consequence, and the chapter draws it:**

> *"Helm's record of what it installed is an ordinary Kubernetes object, subject to the ordinary
> rules. **Whoever can read Secrets in that namespace can read Helm's bookkeeping. Whoever can
> delete them can make Helm forget.**"*

Graded at Practice Q6, where distractor A (a Tiller pod in `kube-system`) is the single best
marker of pre-Helm-3 study material. See [[tiller]].

**⚑ Cross-bearing improvement available.** The chapter points this at Ch 4 §4 (configuration
kept outside the image), which resolves correctly but supports the *storage* claim rather than
the *access* claim. **Ch 12 §4 owns Secret hardening** and is the better target for "whoever can
read Secrets in that namespace." Point there instead, or additionally — the reader who has just
been told that a delivery tool's audit trail is a readable Secret is exactly the reader Ch 12 §4
was written for.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespace.md ===

---

## Chapter 14 §3 — Helm releases are namespace-scoped, and that is what makes many-from-one work

In Helm 3, *"information about a release is stored in the same namespace as the release
itself"*, so you can install the same chart in two namespaces and refer to each by changing your
namespace context. `[source: helm-changes-since-helm2-2026-08-31]` **A release name is scoped to
a namespace, exactly as most Kubernetes object names are.**

`helm list` follows the same scoping: the releases in your current context's namespace, with
`--all-namespaces` widening it to the cluster.
`[source: helm-changes-since-helm2-2026-08-31]`

★ **The pedagogically useful part is the direction of the implication.** TYB (1) Q2's distractor
C offers *"it rolls back only if it shares a namespace with `marketing`"* — which inverts why
namespaces matter here. Namespace scoping is **what makes two installations of one chart
possible in the first place**; it has nothing to do with whether one release's rollback reaches
another. Independence comes from the release model, not from namespace separation.

This is a clean instance of the shard's general rule — a name lives in a scope — applied to an
object type Kubernetes itself does not define.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-metrics-pipeline.md ===

---

## ⚑⚑ Chapter 14 — the composition claim has no source anywhere, and it is now graded

This shard records what the corpus supports about metrics-server: an addon component, not
deployed by default in all distributions, collecting and aggregating metrics pulled from each
kubelet, serving the Metrics API for HPA, VPA and `kubectl top`.

**Chapter 14 asserts something this shard does not hold and cannot license.** Four times, it
describes metrics-server as *"a Deployment, a Service, some RBAC, and an APIService
registration."*

**I checked both places the integration report and the revision notes pointed at:**

| Where | `APIService` | The four-object composition |
|---|---|---|
| All **214** snapshots in `sources/` | **0 occurrences** | absent |
| Shipped `chapter-13` | **0 occurrences** | absent |
| Ch 13's Stage 14 glossary block | absent | absent |

Both verified directly. The revision notes' instruction — *"CHECK CH 13's CORPUS FIRST"* —
resolves to **it is not there either**, which makes this materially worse than a sourcing gap.

### Why it is worse than unsourced

The claim reaches graded text at **Soundings A2** and at **Taking Your Bearings (2) Q5**, where
it forms part of the keyed **correct** answer, and Q5 carries the tag `[retrieval: ch13]`.

The tag is structurally valid — Ch 13 §7 owns metrics-server — and **false in substance**: the
retrieval target does not exist upstream. The reader is asked to recall a four-object
composition they were never shown. That is precisely the failure the integration stage exists to
catch, and it caught the shape while attributing it to the wrong location.

### Two clean fixes

**(a)** Fetch the metrics-server release manifest (`kubernetes-sigs/metrics-server`,
`components.yaml`) and tag the composition. It then becomes *teachable* — but still not
*retrievable from Ch 13*, so Q5's key should be re-aimed at the sourced half regardless.

**(b) ⭐ Recommended, needs no fetch.** Cut the object list from Soundings A2 and from Q5, and
let both rest on what Ch 13 §7 actually establishes: **in a declarative system there is no
installer; installation is applying objects somebody wrote.** That is the retrieval the item
wants, it is the retrieval Ch 13 taught, and it costs the chapter nothing.

**Already correctly removed by the revision stage:** draft-v1's *"about forty YAML files"*, which
contradicted the chapter's own inventory two sentences later and mis-describes an upstream that
ships a single `components.yaml`. Do not restore it.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interfaces.md ===

---

## Chapter 14 §1, §6 — the interfaces generate installation obligations

Chapter 14 opens by collecting what the pluggable-interface story has been quietly accruing:

> *"Install a CNI plugin, because the network model requires one and Kubernetes does not ship
> one. Install an Ingress controller… Install a CSI driver. Install metrics-server…"*

**Every pluggable interface is also a distribution problem.** An extension point that requires a
component to be installed requires a *mechanism* for installing it, and thirteen chapters named
the interfaces without naming the mechanism. That is what §1's failure four is, seen from the
extension side. See [[four-failures-of-a-manifest-directory]].

**§6 gives the interaction its own case.** CRDs shipped inside a chart are where the extension
mechanism and the packaging mechanism visibly meet: the CRD must be registered before any
resource of its kind can exist `[source: helm-crd-best-practices-2026-08-31]`, which is why
`crds/` is not templated and is installed by default — and why **Helm cannot upgrade or delete
CRDs at all**. See [[crds-in-charts]].

**Forward anchor, and it is pinned.** Chapter 14 §6 emits the pointer to **Ch 17 §4**, which B6
records as fixed by already-published pointers in shipped text. Ch 17 §4 collects; it does not
redefine.

⚑ **Reminder for the Ch 17 §4 collection stage** (infrastructure flag I2): half of this thread
lives in `concepts/pluggable-interface-pattern.md` under a second slug, including Ch 9's CNI
ordinal and the conflicts Ch 12's manifest was tracking. **Chapter 14 touches only this file and
adds nothing to that conflict.** Merge the two before Ch 17 reads one and concludes it has the
set.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/operator-pattern.md ===

---

## Chapter 14 §6 — operators are the canonical thing shipped as a chart

Chapter 14 supplies the practical reason operators and charts travel together:

> *"When you go looking for an operator, a controller, an ingress controller, or a monitoring
> stack, what you tend to find is a chart. **Not because templating is superior. Because the
> recipient is a stranger, and everything a stranger needs is packaging.**"*

And the trap that follows from it: an operator shipped as a chart ships CRDs, and **Helm cannot
upgrade CRDs**. *"Operators shipped as charts run into this constantly, and the symptom is
confusing: the chart upgraded successfully and the new feature does not work, because the API
server is still serving the old schema."* See [[crds-in-charts]].

### ⚑ Canonical-forms breach, in this chapter, on this word

The B7 canonical-forms table carries an explicit prohibition: **"Never use 'operator' for a
person."** Chapter 14's Exam Alert writes:

> *"Tiller was Helm 2's in-cluster component, introduced so multiple **operators** could interact
> with the same set of releases."*

**Severity is raised by proximity.** The same chapter uses "operator" correctly for *software*
twice in §6, so both senses appear within a few pages — in a book where the reader met the
operator pattern at Ch 6 §8 and is being asked here to hold operators-as-software while a
sentence quietly reassigns the word to humans.

*(The chapter's separate use of **"cluster operators"** in the sourced `crds/` passage is the
ledger-sanctioned two-word role name and is correct. The bare plural is the problem.)*

**Fix:** *"so that multiple people could interact with the same set of releases."* One word.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/published-vs-commonly-reported.md ===

---

## ⚑⚑ Chapter 14 — the book's best execution of this shard, and a shipped-Ch-1 miscitation it exposes

### The execution, first: this is the strongest instance in the book

Chapter 14 faces a harder version of Chapter 1's problem. CNCF publishes the competency name
*"Application Delivery"* and nothing beneath it — **the words *Helm* and *Kustomize* appear
nowhere** in the published curriculum, the Linux Foundation exam page, or the public LFS250
outline `[source: cncf-kcna-curriculum-pdf-2026-08-23; lf-kcna-exam-page-2026-08-23;
lf-lfs250-course-outline-2026-08-31]`. Verified: neither word occurs in either domain snapshot.

The chapter discloses this in Why This Chapter Matters, defends the judgment
(*"**It is, I think, clearly the right call. But you should know it is a call.**"*), and converts
it into a rule it then keeps for 19,000 words:

> *"Nothing in this chapter is described as 'frequently tested' or 'commonly appears,' because
> nobody outside the exam authority knows that."*

**The rule holds.** The Exam Alert repeats the disclaimer at its head. The chapter's many
frequency observations — *"the single most common collapse in this material"*, *"what most
people expect"*, *"the beginner's move"* — all tie frequency to **learners**, never to the exam.
That is the distinction this shard exists to protect, executed cleanly at scale.

### ⚑⚑ And it exposes a live miscitation in shipped Chapter 1

Chapter 14's draft-v1 asserted *"went from 8% of the exam to 16%"* and *"under-serves this
material by half."* The revision stage cut both for want of a source and left the instruction:
*check Ch 1's corpus; restore if found.* **I checked. Do not restore.**

`chapter-01:274` reads:

> *"**Cloud Native Application Delivery doubled**, from 8% to 16% `[source:
> lf-kcna-program-changes-2026-08-23]`… material built for the old blueprint will under-serve it
> by roughly half."*

**That snapshot explicitly disclaims the figure.** Its header:

> *"CORRECTION 2026-08-23: the previous capture of this page listed the retired five-domain
> weights (46/22/16/8/8) as if sourced here. Targeted re-fetch confirms **THE PAGE DOES NOT
> DISPLAY THE PREVIOUS DOMAIN STRUCTURE OR WEIGHTS.** Those figures have been removed from this
> snapshot."*

and its closing section: *"**Not stated on this page** — No question count, no passing score, no
duration, and **no retired-blueprint weights**."*

**The only place the corpus carries `8%` for this domain** is
`provenance-kcna-60-questions-2026-08-23.md` — headed **"DO NOT CITE THE CONTENTS OF THIS FILE
AS FACT"**, authority field *"NOT AUTHORITATIVE — community guest post syndicated onto the CNCF
blog"*, and whose own cross-check concludes *"46/22/16/8/8 — NOT independently sourced."* The
intended real source, `cncf-curriculum-repo-kcna-versions-2026-08-23.md`, is an **open gap**.

**The irony is exact and worth recording as canon.** That same snapshot is the provenance file
for the 60-question/75% claims — the claims this shard was created to handle, and which B3's
recovered summary lists among the four things that **must not be retrieved**. Chapter 1 §2
teaches readers to distrust a figure whose authority comes from where it is hosted rather than
who published it, and `chapter-01:274` prints such a figure under a Linux Foundation source tag.

**Consequences, in order:**

1. **Chapter 14 stays as revised.** Following its own restore instruction would propagate the
   miscitation into a second chapter. The revision stage was right by caution.
2. **`chapter-01:274` needs correcting**, not copying. Either fetch `github.com/cncf/curriculum`
   for the retired blueprint and re-tag, or rewrite to the supported claim — the domain carries
   16%, and the restructure rolled Observability under Cloud Native Architecture, which *is*
   sourced at `lf-kcna-program-changes:23`.
3. **`domain-analysis.md:39` carries the same unsourced assertion** and is how it reached two
   chapters. Ch 15 and Ch 16 read that row next. Correct it in the same pass.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/domain-weights-44-28-16-12.md ===

---

## ⚑⚑ Chapter 14 — do not restore the "doubled from 8%" claim, in this or any chapter

**What is published, and all that is published:** Cloud Native Application Delivery carries
**16%**, with competencies *Application Delivery* and *Debugging*. Confirmed identically across
three independent snapshots — `lf-kcna-exam-page-2026-08-23:43`,
`cncf-kcna-curriculum-pdf-2026-08-23:15`, `lf-kcna-program-changes-2026-08-23:39` — plus
`cncf-kcna-certification-page-2026-08-23:35`.

**The prior weight is not published anywhere in this corpus.** See
[[published-vs-commonly-reported]] for the full chain; in short:

- `lf-kcna-program-changes-2026-08-23` carries an explicit correction confirming the page
  **does not display** the previous structure or weights, and lists *"no retired-blueprint
  weights"* among what it does not state.
- The only `8%` in the corpus is in a snapshot headed **"DO NOT CITE THE CONTENTS OF THIS FILE
  AS FACT"**, whose own cross-check says the figures are *"NOT independently sourced."*
- `cncf-curriculum-repo-kcna-versions-2026-08-23.md` is the intended source and is an
  **open gap**.

### Standing ruling for Chapters 15–20

**The 16% figure is safe and fully sourced. Any statement of change — "doubled", "went from 8%",
"under-serves by half", "the largest proportional change" — is not, and must not be written**
until `github.com/cncf/curriculum` is fetched and tagged.

This matters beyond Chapter 14 because the argument is rhetorically attractive and will keep
presenting itself: Ch 15 and Ch 16 are the other two D3 chapters, and the "legacy prep material
under-serves this domain" line is exactly the kind of thing an Exam Alert reaches for.

### Two sites needing correction, outside Chapter 14

| Site | Text | Status |
|---|---|---|
| `chapter-01:274` | *"doubled, from 8% to 16% `[source: lf-kcna-program-changes-2026-08-23]`"* | **shipped, and the cited snapshot disclaims it** |
| `domain-analysis.md:39` | *"Doubled from 8% to 16% in the revision — the single largest proportional change."* | **B-stage artifact, unsourced; Ch 15/16 read this row next** |

**Chapter 14 currently states only the supported figure**, twice (Why This Chapter Matters and
the Exam Alert), with the tag. Both were rewritten together by the revision stage and **must
stay together** — if one is ever restored, so is the other, and only after the fetch lands.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 14 — D3.1 Application Delivery (the packaging half)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D3.1 — Application Delivery** | **Chapter 14** | **deep — packaging; GitOps and delivery to Ch 15** | — |

**Declared weight note.** The chapter's metadata line states the published **16%** for the whole
Cloud Native Application Delivery domain with its source tag, immediately followed by the house
disclaimer that the split across Ch 14–16 is an authored allocation. The outline's internal 5%
is a planning figure and appears nowhere in reader-facing text. Correct handling — CNCF
publishes no sub-competency weights (B1 gap G33, B2 disclosure #1).

**⚠ And a second, sharper disclosure unique to this chapter, correctly executed.** CNCF publishes
the competency *name* and nothing beneath it. Verified: **neither `lf-kcna-exam-page-2026-08-23`
nor `cncf-kcna-curriculum-pdf-2026-08-23` contains the word "Helm" or "Kustomize."** The chapter
says so plainly in Why This Chapter Matters and holds the resulting no-frequency-claim rule for
19,000 words. See [[published-vs-commonly-reported]].

## Concept-level — D3.1's nine Helm rows, all nine here

Walked row by row against `domain-analysis.md:257–296`.

| B1 concept | Covered in | Depth |
|---|---|---|
| Helm | Ch 14 §2 | deep |
| Chart | Ch 14 §2 | deep |
| `Chart.yaml` | Ch 14 §2 | deep |
| `values.yaml` | Ch 14 §2, §3 | deep — including the override ladder |
| `templates/` | Ch 14 §2 | substantial — template *language* deliberately bounded |
| `charts/` | Ch 14 §2 | deep — trap #81 twice |
| `crds/` | Ch 14 §2, §6 | deep — plus the three limits |
| Chart repository | Ch 14 §4 | deep |
| Release | Ch 14 §3 | deep — the chapter's centre |
| **Kustomize** *(not a B1 row — see G19)* | Ch 14 §5, §6 | deep |

**Correctly untouched, and belonging to Ch 15–16:** GitOps and the four OpenGitOps principles ·
Argo CD, source of truth, OutOfSync, sync, tracking targets, manifest sources · Knative ·
twelve-factor. §5's `helmCharts` beat sets up Argo CD's Kustomize/Helm manifest sources (B1 trap
#77) without encroaching.

## Trap coverage — 3 of 3 D3.1 Helm traps, all `[source]`-tagged

| # | Trap | Where addressed | Depth |
|---|---|---|---|
| 79 | "Helm is a templating engine" | §7's Zenith; Exam Alert trap row 1 and high-priority #3 | deep — refuted *structurally*, by the existence of a template-free tool solving the same problem, not by reciting the definition |
| 80 | Confusing chart with release | §3 ★ Fixed Point; ⚠ Hazards; TYB (1) Q1; Practice A1; Summary | deep |
| 81 | Confusing `charts/` with a chart repository | 🪝 Snags in §2 **and** §4; fig02 annotation; TYB (1) Q2; Practice Q11; Exam Alert | deep |

**Nine traps added by the Exam Alert and not in the B1 inventory:** Tiller as a currency test ·
assuming `helm rollback` wraps `kubectl rollout undo` · reading chart version as the software's
version · assuming Kustomize needs an engine installed · assuming an overlay edits or copies its
base · expecting a chart upgrade to upgrade its CRDs · editing a chart in place instead of
overriding · reading `values.yaml` as rendered output · treating the four failures as one
problem.

## Research gaps

| Gap | Status |
|---|---|
| **G19 — Kustomize.** *"Overlay/base model is worth one paragraph."* | **Closed, and deliberately over-delivered** — §5 and §6. A one-paragraph treatment could not have supported §7's argument that templating is not the definition. |
| **G-14b — Deployment revision accounting** | **Closable today from `k8s-docs-deployment-2026-08-23`, no fetch.** Its *Rolling back a Deployment* section states the if-and-only-if rule and that scaling creates no revision. Strike from the open list and restore the stronger form of TYB (1) Q4. |
| **G-14e — the prior blueprint weight** | **Resolved: DO NOT RESTORE.** The only `8%` in the corpus sits in a snapshot that disclaims itself. See [[domain-weights-44-28-16-12]]. |

**Still open and touching Chapter 14:** **G-14a** `appVersion` — zero of 214 snapshots, one
graded item · **G-14c** the chart-template guide, for the Go-template claim and the patch
semantics — one graded item, and it orphans a B7 ledger row · **G-14d** metrics-server's
composition — zero of 214 snapshots **and** zero in shipped `chapter-13`; now a retrieval-validity
problem, not only a sourcing one · **G-14f** the Helm 3.0 GA date (cosmetic) · **G-14g** whether
`helm rollback` increments the counter — reader-facing as *"rev 4 ???"* in `ch14-fig03`.

**⚑ A pattern in the corpus, not in the chapter.** Both Helm snapshots that would close a gap
truncate at their first code block: `helm-charts-2026-08-31` at *"Helm will expect a structure
that matches this:"* (18 lines) and `helm-using-helm-2026-08-31` at the literal word *"Example:"*
(30 lines). Worth checking the harvester's fenced-block handling before Ch 15's Helm-adjacent
research runs.

**⚑ Index-level fixes for the outline frontmatter**, confirming and extending the revision
notes: add `helm-push` to `kb_tags.commands` **only if §4 names the command in prose** (today it
appears once, inside its own answer key) · add `helm-2-to-helm-3` (or `tiller`) and
`chart-archive` to `kb_tags.concepts` · add `D1.1` and `D1.4` to `kb_tags.objectives`, which the
outline's own practice-question plan declares and this draft executes.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 14 — backward retrieval

| Tested topic | Original chapter | Retested in |
|---|---|---|
| `kubectl rollout undo` reverts the Pod template; the controller reconciles | ch 6 §5 | ch 14 — Taking Your Bearings (1) Q4 |
| "Install metrics-server" is applying objects somebody wrote; `kubectl top` fails on a bare cluster | ch 13 §7 | ch 14 — Taking Your Bearings (2) Q5 ⚑ |
| A CRD must be registered before resources of its kind can be used | ch 6 §8 | ch 14 — Practice Q1 *(tagged `[interleaved: D1.1]` only)* |
| One release contains many objects; a single act returns all of them | ch 6 §1 / ch 4 §2 | ch 14 — Practice Q9 *(tagged `[interleaved: D1.1]` only)* |
| The OCI Distribution Spec distributes *content*, not images specifically | ch 2 §5 | ch 14 — Practice Q12 *(tagged `[interleaved: D1.4]` only)* |

### ⚑ Compliance — and Chapter 13's denominator problem is now a pattern

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of **Bearings** | 20–25% (the Ch 14–18 band) | 2 of 10 = **20%** | ✅ at the floor |
| Retrieval share of the **Practice pool** | same target, *"applied to it once sized"* | **0 of 17 = 0%** | ❌ |
| Retrieval share of **all graded items** | 20–25% | 2 of 27 = **7.4%** | ❌ |
| Spacing floor (≥4 chapters back, from Ch 8 on) | ≥1 item | ch 6 is **eight** back | ✅ |
| Question inventory vs B4 (`length-budget.md:64`) | 8 · 10 · 17 · 35 | **8 · 10 · 17 · 35** | ✅ exact |

**Two chapters running makes this structural rather than a lapse.** Ch 13 and Ch 14 both place
every `[retrieval:]` tag in Bearings and none in Practice, while carrying genuine backward reach
in Practice under `[interleaved:]` tags. **A mechanical audit greps `[retrieval:` and reads both
Practice pools as empty — and Ch 19 is built by exactly such an audit.**

**Cheapest fix, no new questions**, combined with the tag-form fix below:

- Q1 → `[retrieval: ch6]` `[interleaved: D1.1 core concepts]`
- Q9 → `[retrieval: ch6]` `[interleaved: D1.1 core concepts]`
- Q12 → `[retrieval: ch2]` `[interleaved: D1.4 containerization]`

Practice reaches 3 of 17 = 17.6%; the chapter reaches 5 of 27 = **18.5%**. One further item on
the chart-versus-release distinction — which the Exam Alert already names as the material's most
common collapse — clears the band. **Recommend fixing this book-wide once**, rather than per
chapter for the remaining five.

### ⚑ Interleave tag form — the house convention already exists, one chapter old

`domain-analysis.md:33` states that the D-numbering is **"a Lodestar convention"** — CNCF publishes named competencies and does not number them. So a bare reader-facing `[interleaved: D1.1]` prints a house-invented identifier inside the one chapter whose central disclosure is that CNCF publishes nothing beneath the competency.

Shipped Chapter 13 — the only shipped chapter using these tags — already solved this:

| Shipped Ch 13 | Chapter 14 draft |
|---|---|
| `[interleaved: D1.1 workloads]` | `[interleaved: D1.1]` |
| `[interleaved: D1.3 scheduling]` | `[interleaved: D1.4]` |
| `[interleaved: D2.2 security]` | — |

The trailing topic word is what makes the tag legible to a reader who has never seen the numbering, which is exactly the mitigation the disclosure calls for. **Fix: `[interleaved: D1.1 core concepts]` and `[interleaved: D1.4 containerization]`.** House form, and it resolves integration item 22 rather than leaving it as a question.

The `[retrieval: chN]` form Chapter 14 uses matches the shipped convention exactly (25× `ch2`, 22× `ch4`, 19× `ch3`, 14× `ch5`, 7× `ch6`, 5× `ch10`, 4× `ch8`, 3× `ch9`, 2× `ch7`). No change needed there. Chapter 14 is the book's first `[retrieval: ch13]`.

### Soundings — excluded from the budget, doing the work anyway

All eight are retrieval, sourced from B2's Prerequisites column exactly as B3's drafting instruction requires, and every one is answerable from Ch 1–13 or from professional experience. Excluded from the budget per B3.

Q7 (*"From your own professional experience with any package manager at all — apt, npm, pip, NuGet, Homebrew…"*) is the only item in the book drawing on experience from outside it, and its key grades nothing: *"Hold onto whichever ones you named. You will need them shortly."* Correct calibration for a pre-test whose purpose is metacognitive rather than evaluative.

⚑ **Soundings A2 carries the same defect as TYB (2) Q5** — it answers "what does 'install metrics-server' consist of" with the four-object composition that neither the corpus nor shipped Ch 13 states. Fix both together.

### Obligations Chapter 14 discharged — eleven

**Chapter 6's three chapter-level promises, all verified by line number against shipped text:**

| Promise | Shipped at | Discharged by |
|---|---|---|
| *"a Helm chart's job is to template this object"* | `chapter-06:372` | §2's closing worked instance |
| *"Helm rollback and Deployment rollback are different mechanisms wearing the same word"* | `chapter-06:720` | §3's ★ Fixed Point, on all three axes |
| *"why Helm charts have a `crds/` directory"* | `chapter-06:1036` | §6 |

**Chapter 13's handoff verified** at `chapter-13:1830`: *"This chapter kept saying 'somebody has to install that': metrics-server, a logging backend, an Ingress controller."* Chapter 14 quotes it accurately. Note the lists differ — Ch 13 names three, Ch 14 collects four (adding CNI and CSI, dropping the logging backend). Not a defect; Ch 14 collects a longer debt than Ch 13 named.

**Chapter 1's ledger contract honoured on both sides** at `chapter-01:274` — Helm named with a pointer to Ch 14–16, defined here. *(That same line carries the ⚑⚑ miscitation; see [[published-vs-commonly-reported]].)*

Also discharged: Ch 2 §3 and §5 · Ch 4 §1, §2, §4, §5, §6 · Ch 10 §3 (in Ch 10's own canonical form) · Ch 13 §7.

### Forward obligations Chapter 14 creates

| Topic Ch 14 owns | Must be retrieved in | Status |
|---|---|---|
| Charts as a delivery agent's manifest source | **Ch 15 §4** | planted in §2; B6 records the number as pinned by shipped pointers |
| Push-versus-pull, and who runs the install | **Ch 15 §3** | The Voyage Ahead poses it and declines to answer; three pointers emitted |
| **Rollback by revert** — the third sense | **Ch 15 §4** | ⚠ §3 currently writes two non-canonical variants; must use the ledger's exact three-word form |
| CRDs shipped as chart content | **Ch 17 §4** | planted in §6; pinned |
| The control loop pointed at a Git repository | **Ch 15 §7** | set up, payoff correctly left unspent |
| Kustomize and Helm as Argo CD manifest sources | **Ch 15 §4** | §5's `helmCharts` 🔭 sets up B1 trap #77 |

=== END APPEND ===
```

---

## What this stage changed about the open-items list

Three of the seven research gaps resolve differently than the revision notes assumed, and the differences are worth stating plainly:

**G-14b is closed today, no fetch.** `k8s-docs-deployment-2026-08-23` — a snapshot the revision stage did not consult — carries the revision-accounting rule verbatim, including a *better* rebuttal for TYB (1) Q4's distractor B than the one currently in the key. Restore the stronger item from the corpus already on disk.

**G-14e inverts.** The instruction was *check Ch 1's corpus, restore if found.* The figure is in shipped Chapter 1, cited to a snapshot whose own correction header says the page does not carry it. Following the instruction would have propagated a miscitation into a second chapter. **Chapter 14 stays as revised; `chapter-01:274` and `domain-analysis.md:39` are what need fixing.**

**G-14d is worse than a sourcing gap.** `APIService` returns zero matches across all 214 snapshots *and* zero in shipped `chapter-13`. A `[retrieval: ch13]` item's correct answer therefore asks the reader to recall something no chapter taught. The cheap fix needs no fetch: cut the object list from Soundings A2 and TYB (2) Q5 and let both rest on what Ch 13 actually established.

Two further ship-gates stand as the integration report described them — **G-14a** (`appVersion`, the chapter's one graded item on nothing) and **fig03's reader-facing "rev 4 ???"**. Both Helm snapshots that would close them truncate at their first code block, which looks like a harvester issue rather than a coincidence and is worth a look before Ch 15's research runs.

Everything else in this manifest is pending write blocks against a knowledge base that has never been applied — fourteen manifests now, and infrastructure flag ⚑ I1 still says a chapter-order replay destroys nine chapters of work until Ch 03's, Ch 10's and Ch 11's twelve full-file WRITEs are converted to APPENDs.
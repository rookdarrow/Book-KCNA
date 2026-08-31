Working from the four binding inputs (skill, style ledger, section skeleton, term ledger) plus the draft. No knowledge-base shards were tagged, so shipped-chapter prose was unavailable — every claim below that would require it is marked as needing author verification rather than asserted.

```markdown
# Integration Check — KCNA Chapter 14

## Summary

- Terminology consistency: **fail** — 6 drift items against explicit canonical forms, all one-line mechanical fixes; none affects what the chapter teaches
- Callbacks to earlier chapters: **42 correct / 0 incorrect** (cross-bearings, verified mechanically against the section skeleton) — plus **5 prose callbacks** asserting what an earlier chapter promised, which cannot be verified from the inputs available
- Retrieval-practice accuracy: **pass** — both `[retrieval:]` tags point at chapters and sections that own the material; one carries a substance caveat (G-14d)
- Glossary coverage: **46 concepts/commands introduced, 41 defined in-chapter, 5 require glossary entries** (+4 defined in-chapter but absent from the B7 ledger)
- Contradictions with earlier canon: **none verified** — 6 items require checking against shipped text this stage does not have
- Ethical guardrails (skill Part 14): **pass**, with one caveat (the chapter's only unsourced reader-facing number)

**Section numbering:** all seven `§N` numbers and titles match the B6 skeleton exactly. Heading form is `## <difficulty> §N — Title` (the Ch 5–8 form the skeleton recommends for Ch 9–19) and the closing synthesis carries `☀️` (also per skeleton recommendation). No renumbering, no silent divergence.

**Skeleton decay-risk note satisfied.** B6 recorded that Helm has thin downstream presence and named two mandatory anchors that may not be dropped. Both are planted: §2 → `Ch 15 §4` (charts as a delivery agent's manifest source) and §6 → `Ch 17 §4` (CRDs shipped as chart content).

---

## Terminology consistency

Checked against the B7 ledger's **Canonical forms** section (homonyms table and sanctioned-variants table), which is a complete input to this stage and does not require shipped text. Occurrence counts are approximate where a form recurs.

| Term | Canonical form | Occurrences | Drift? |
|---|---|---|---|
| Helm | `Helm` | ~60 | no |
| chart (the package) | lowercase `chart`; Ch 14 §2 owns | ~120 | no |
| Kustomize | `Kustomize` | ~30 | no |
| `kubectl` | lowercase, **always code style, even sentence-initially** | ~24 | **yes** — ~12 unbackticked bare prose uses |
| Pod | `Pod` capitalized for the object | ~14 | **yes** — 1: "a Tiller pod" (Practice Q6 option A) |
| Deployment · ReplicaSet · StatefulSet · DaemonSet · ConfigMap · Secret · Service · PersistentVolumeClaim · CustomResourceDefinition | exact CamelCase, unspaced | many | no |
| Ingress controller | capitalized for object *and* controller | 2 | **yes** — 1: "an ingress controller" (§6) |
| namespace (the scope) | lowercase | ~14 | no |
| Secrets (the object) | capitalized | 5 | no |
| rollback (Helm) | `helm rollback`; never bare where either sense could be meant | ~14 | no |
| rollback by revert | **`rollback by revert`** (ledger-sanctioned surface form) | 2 | **yes** — "rollback-by-revert" (§3 prose) and "GitOps revert" (§3 ⚠ block) |
| revision (Helm sense) | **`release revision`** or **`Helm revision`**, never bare | ~18 | **yes** — §3's subsection heading and several prose uses are bare |
| release (Helm sense) | **`Helm release`** on first use in each Ch 14/15 section | ~40 | **yes** — three distinct problems, below |
| operator | **never for a person** | 4 | **yes** — 1: "so multiple operators could interact with the same set of releases" (Exam Alert) |
| cluster operator | two words, role name | 1 | no (sourced, two words) |
| metrics-server | lowercase, hyphenated | 6 | no |
| cloud native | never hyphenated | 3 | no |
| Kubernetes | spelled out; never `K8s` | ~25 | no |
| chart repository | the headword for the HTTP server | 12 | **soft yes** — "Helm repositories" appears twice in sourced text, unreconciled |
| GitOps | name only, **always with a pointer** | 2 | **soft yes** — one use (§3 ⚠ block) carries no pointer |
| Tiller | *no canonical form recorded* | 9 | n/a — ledger row missing (see Glossary) |

### The five that matter, expanded

**1. "operators" for people.** Exam Alert: *"Tiller was Helm 2's in-cluster component, introduced so multiple operators could interact with the same set of releases."* The canonical-forms table carries an explicit prohibition — *"Never use 'operator' for a person."* The reader met "operator" as the operator pattern at Ch 6 §8, and this sentence reassigns it to humans in the same chapter that spends §6 on operators-as-software ("Operators shipped as charts run into this constantly"). Fix: *"so that multiple people could interact…"*.

**2. `rollback by revert`.** The ledger reserves that exact three-word form for the GitOps sense, specifically so the book's three rollbacks stay distinguishable. §3 writes it hyphenated ("Chapter 15's rollback-by-revert") and the ⚠ block writes it as "GitOps revert" — two variants in the same section, in the section that owns the name collision. This one is worth fixing precisely because §3 is where the discipline is being taught.

**3. "release", three ways.**
- §1 uses generic-English "release" before Helm exists in the chapter: *"It does not roll back 'the release that also changed the ConfigMap…'"*. This is the collision the canonical-forms rule exists to prevent, and it lands 40 lines before the term is defined. Fix: "the change that also…" or "the deploy that…".
- The chapter's first Sense-B use (Dead Reckoning, Why This Chapter Matters) is bare "release" rather than "Helm release". Low severity — it is immediately defined.
- §4: *"with the release of Helm 3.8.0"* is a **third** sense (a software version release) inside a bolded sourced claim, in the chapter that owns the release/revision distinction. Fix: "as of Helm 3.8.0" or "Helm 3.8.0 introduced".

**4. Helm's own wording, unflagged.** §3 quotes the CLI reference: *"if that second argument is omitted or set to `0`, it rolls back to the previous release."* Helm's "previous release" means the preceding **revision** — exactly the conflation this section exists to break. Practice A7 does the reconciling work ("'previous release' means the immediately preceding revision"), but that is four pages after the reader first meets it. Add a half-clause at the §3 quotation.

**5. `kubectl` code style.** The chapter is internally inconsistent rather than uniformly wrong: `kubectl apply -f manifests/` and `kubectl rollout undo` are code-styled, while ~12 bare prose uses are not ("Built into kubectl", "If a machine has kubectl, it has Kustomize", "meaningless to bare kubectl", the Chapter Summary row, the Exam Alert rows). The lowercasing — the half that actually protects meaning — is correct throughout. Mechanical sweep.

---

## Callback correctness

### Cross-bearings — 42 pointers, 42 resolve

Verified mechanically against the B6 skeleton, per this stage's rule. 22 distinct target sections across 9 chapters.

| Target | Uses | Skeleton section | Verdict |
|---|---|---|---|
| Ch 2 §3 | 2 | Registries, Tags, and Digests | ✓ |
| Ch 2 §5 | 1 | The Open Container Initiative | ✓ |
| Ch 3 §5 | 1 | The Only Door In | ✓ |
| Ch 4 §1 | 1 | You File a Declaration | ✓ |
| Ch 4 §2 | 2 | The Anatomy of a Record | ✓ |
| Ch 4 §3 | 1 | Where a Name Lives | ✓ |
| Ch 4 §4 | 6 | Configuration Kept Outside the Image | ✓ |
| Ch 4 §5 | 1 | The Universal Join | ✓ |
| Ch 4 §6 | 2 | A Declaration, Not an Order | ✓ |
| Ch 6 §1 | 2 | The Resource That Holds the Intent | ✓ |
| Ch 6 §2 | 1 | A Loop You Can Watch Working (owns `kubectl scale`) | ✓ |
| Ch 6 §4 | 1 | Changing the Fleet Under Way | ✓ |
| Ch 6 §5 | 4 | Every Rollout Is a Revision | ✓ |
| Ch 6 §8 | 4 | The Control Loop, Extended | ✓ |
| Ch 9 §1 | 1 | Four Rules and a Plugin (owns network model + CNI) | ✓ |
| Ch 10 §3 | 1 | The Object Is Not the Implementation | ✓ |
| Ch 13 §2 | 1 | Pods That Never Start (owns missing-ConfigMap) | ✓ |
| Ch 13 §7 | 3 | Numbers Nobody Collects by Default | ✓ |
| Ch 14 §5 | 1 | Patching Instead of Templating (same-chapter) | ✓ |
| Ch 15 §3 | 3 | Push, or Pull | ✓ |
| Ch 15 §4 | 2 | An Agent That Watches a Repository | ✓ |
| Ch 17 §4 | 1 | Every Place Kubernetes Lets You In | ✓ |

Notes on the six forward pointers: all three targets (Ch 15 §3, Ch 15 §4, Ch 17 §4) are numbers the skeleton records as **pinned by already-published pointers** in shipped text, so they are immovable and safe to emit. Ch 9 §1's topic label reads "the network model and CNI" where the published-pointer wording is "CNI and pod networking" — the label is free text and names what the section owns, so this is not a defect.

The Ch 4 §4 pointer in §3's ⚓ Worth Securing ("Helm's record of what it installed is an ordinary Kubernetes object") resolves correctly, but the sentence it supports is a security consequence ("whoever can read Secrets in that namespace can read Helm's bookkeeping"), and **Ch 12 §4** owns Secret hardening. Optional improvement: point there instead, or additionally.

One same-chapter pointer, §1 → Ch 14 §5. The cross-bearing convention sanctions pointers that "span chapters or major sections," and §1→§5 does. Recorded only because Proxmox's reconcile pass flagged same-chapter self-references as noise; four sections' distance is not that case.

### Prose callbacks — 5 unverifiable from this stage's inputs

These assert what an earlier chapter *said or promised*. No knowledge-base shards were tagged for this chapter, so I have no shipped-chapter text and am not guessing. Each needs a one-minute grep before ship:

1. **Why This Chapter Matters** quotes Ch 13's closing verbatim, in italics: *"this chapter kept saying 'somebody has to install that.'"* Verify the wording exists. Note that B6 gives Ch 13 §8 an explicit handoff to **Ch 16 §1**, not to Ch 14, so a Ch 14-facing sentence there is plausible but not structurally guaranteed.
2. **§2:** *"Chapter 6 promised that a Helm chart's job is to template that object."*
3. **§3:** *"Chapter 6 owes you this one. It told you that you would meet the word 'rollback' twice more in this book… and pointed at this chapter and at Chapter 15."* Strongly supported by the ledger's ownership table (*"Ch 14 §3 owns Helm rollback and the name collision"*) but the verbatim promise is unconfirmed.
4. **§6:** *"Chapter 6 promised you an answer to this"* (why charts have a `crds/` directory).
5. **The Voyage Ahead:** *"You have seen the control loop reconcile a Deployment toward its spec, a scheduler toward a placement, a claim toward a volume."*

Item 5 deserves a paragraph, because it brushes a book-level convention. The ledger's **"state the pattern, never the count"** rule (ratified 2026-08-30) forbids asserting a running ordinal, and records that shipped Ch 6 closes by telling the reader they have seen the loop *twice* and that "the third time is the one that matters" — meaning Ch 15 §7. This draft asserts **no number**, so it complies with the letter of the rule. But it enumerates three prior sightings and then names Ch 15 as the saved one, which makes the arithmetic visible: a reader who took Ch 6's count literally is now at four-before-the-payoff, because Ch 7 and Ch 11 added sightings after Ch 6 spoke. The underlying defect, if there is one, is in shipped Ch 6, not here. Cheapest fix in this chapter: de-enumerate — "You have watched the control loop reconcile toward specs, placements, and volumes." **Author's call**; flagging rather than prescribing, since the draft breaks no stated rule.

---

## Retrieval-practice accuracy

| Tag | Item | Topic | Owning section (skeleton) | Verdict |
|---|---|---|---|---|
| `[retrieval: ch6]` | TYB1 Q4 | `kubectl rollout undo` reverts the Pod template; controller reconciles | Ch 6 §5 — Every Rollout Is a Revision | ✓ aligned |
| `[retrieval: ch13]` | TYB2 Q5 | "install metrics-server" = applying objects somebody wrote; `kubectl top` fails on a bare cluster | Ch 13 §7 — Numbers Nobody Collects by Default | ✓ aligned |

Both are genuine retrieval, not disguised current-chapter recall. The revision stage's trim of Q5 option B (from "…which somebody has packaged, commonly as a chart" to "…which somebody else wrote") was the right call and is what makes the item do the work its tag claims.

**Caveat carried from G-14d, and it is an integration matter rather than a fact-accuracy one.** Q5's correct answer, and Soundings A2, both rest on metrics-server's composition being *"a Deployment, a Service, RBAC rules, an APIService registration."* If Ch 13 §7 does not state it in those terms, the item asks the reader to retrieve something they were never told — which is the specific failure this stage exists to catch. Check Ch 13's corpus and text before ship.

Spacing arithmetic, for the record: TYB1 1/5 and TYB2 1/5 = 20% retrieval, at the floor of the ledger's 20–25% band for chapters 6+. Practice adds three interleaves (Q1, Q9 `[interleaved: D1.1]`; Q12 `[interleaved: D1.4]`), all three genuinely reaching earlier material.

---

## Glossary coverage

46 concepts and commands introduced (counting the `kustomization.yaml` field list as one). 41 defined in-chapter. Substantive rows:

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| Helm | yes | no |
| chart | yes | no |
| `Chart.yaml` · `values.yaml` · `templates/` · `charts/` · `crds/` | yes (all five) | no |
| `NOTES.txt` · `_helpers.tpl` | yes | no |
| subchart | yes | no |
| Helm release | yes | no |
| release revision | yes | no |
| `helm install` · `upgrade` · `rollback` · `list` | yes | no |
| `--values`/`-f` · `--set` precedence | yes | no |
| `--generate-name` · `--all-namespaces` · `--skip-crds` | yes | no |
| chart repository · `index.yaml` | yes | no |
| chart archive | yes | no — but **no ledger row** |
| OCI registry as chart store · `oci://` | yes | no |
| `helm push` | yes (push semantics) | recommended — graded (Q17) |
| chart version vs `appVersion` | yes | no — **unsourced (G-14a)** |
| `HELM_DRIVER` | yes | no — but **no ledger row** |
| Tiller | yes | **yes** — graded (Q6), and **no ledger row** |
| Kustomize · base · overlay · `kustomization.yaml` | yes | no |
| Kustomization (the KRM object) | yes | no |
| kustomization fields (`resources`, `namespace`, `namePrefix`/`nameSuffix`, `labels`, `commonAnnotations`, `images`, `replicas`, `patches`, `patchesStrategicMerge`, `patchesJson6902`, `configMapGenerator`, `secretGenerator`, `bases`) | yes | no |
| strategic merge patch · JSON patch | yes | no — **authored, unsourced (G-14c)**; graded (Q15) |
| `helmCharts` | yes | **yes** — appears in a graded key (A13), and **no ledger row** |
| `kubectl apply -k` | yes | no |
| CRD-in-chart ordering rule + its three limits | yes | no |
| **APIService** | **no** | **yes — highest priority** |
| **eventual consistency** | contextually glossed only | **yes** |
| `helm repo` | named only | yes (low) |
| `--dry-run` | named only | yes (low) |
| `generatorOptions` | named only | yes (low) |
| `helm pull` | **not mentioned** | see Recommended fixes |
| JSON 6902 | named (sourced), not expanded | register row |

**APIService is the one that matters.** It appears four times, is never defined anywhere in the chapter, and reaches graded text twice — Soundings A2 and TYB2 Q5's *correct answer*. The B7 ledger's own standing rule is that a term reaching question text or an answer key may not be glossary-only, and the converse holds too: a graded term needs a lookup path. Either confirm Ch 13 §7 defines it (plausible — metrics-server's APIService registration is Ch 13 §7 material, which I cannot check) or add a glossary entry plus a register row.

**Eventual consistency** is used twice as load-bearing vocabulary (§1's ordering argument and §6's comparison table) with a mechanism sketch but no definition, and it has no owner and no ambient-tier assignment. It carries a precise distributed-systems meaning; assign it or gloss it.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Every factual sentence carries a `[source:]` tag, and the seven open gaps are documented rather than papered over. The revision stage's removals are the right ones: the "forty YAML files" count, the "8% → 16%" and "under-serves by half" claims, "a Helm that has not existed since 2019", and "RFC 6902". *One caveat:* "95% identical" (§1 prose and fig01's bracket annotation) is the chapter's only unsourced reader-facing number. It is illustrative, describing a hypothetical pair of directories, not evidentiary — but the figure's annotation reads more assertive than the prose. In a chapter this scrupulous, "nearly identical" costs nothing.
- [x] **Fear-based content uses real examples.** The Logbook Entry's `deployment-prod-final-v2-USE-THIS-ONE.yaml` is recognizable rather than invented-scary, and it closes with *"This is not incompetence."*
- [x] **Simplification acknowledged.** Dead Reckoning in Why This Chapter Matters; §2 explicitly bounds its own template-language coverage ("That is as far as this book goes… You do not need to for this exam") and gives the pedagogical reason. *Partial:* §3 declines to state the revision-counter behavior because the corpus cannot settle it — the honest call — but the omission is silent while fig03 shows a reader-facing **"rev 4 ???"**. Uncertainty handled by omission plus an unexplained question mark reads as an unfinished figure, not as an uncertainty signal. See Recommended fixes.
- [x] **Authority claims cite legitimate sources.** Helm docs, kubernetes.io, the kubectl book, the OCI distribution spec, the LF exam page, the CNCF curriculum PDF.
- [x] **"Frequently tested" claims are verifiable.** Strongest pass in the chapter. Why This Chapter Matters discloses that CNCF publishes the competency name and nothing beneath it, that *Helm* and *Kustomize* appear nowhere in the published curriculum, exam page, or LFS250 outline, and that the topic list is therefore authored inference — then states the rule it will follow: *"nothing in this chapter is described as 'frequently tested' or 'commonly appears,' because nobody outside the exam authority knows that."* The Exam Alert repeats the disclaimer at its head. The rule holds throughout. The chapter's many practitioner-frequency observations ("the single most common collapse in this material", "what most people expect", "the beginner's move") are pedagogical, tie frequency to *learners* and never to the exam, and sit inside the register skill Part 1 sanctions.
- [x] **No strawmanning of alternative study methods.** The Tiller row comes closest, and stays on the right side: it offers a checkable fact (Helm 3 removed Tiller) as a dating test, not a claim about a competitor's quality. The inference that follows — "reason enough to read carefully whatever else it tells you" — is hedged and earned.
- [x] **Subject dignity (skill v5.7 Part 14 item 9).** All wry beats are oriented at practitioners: the accumulated `k8s/` directory, step 4 of the README "written down by somebody who could see it clearly and had no vocabulary for it", the note left for the next watch. No third-party harm is treated as amusing.

---

## Recommended fixes

### Already carried by the revision stage — not re-flagged, with one integration contribution

The consolidated AUTHOR-REVIEW block documents seven research gaps (G-14a…G-14g), three index-level `kb_tags` additions, the figure-anchor dispute between the Stage 10 rule and the structural contract, and the fig02 regen ("grey"→"gray", the `crds/` annotation narrowing). All are correctly scoped and none needs restating here.

**What this stage adds:** three of the seven are closable from a sibling chapter's corpus rather than a new fetch, which makes them cheaper than the block implies — **G-14d** (check Ch 13's corpus for a metrics-server snapshot), **G-14e** (check Ch 1's corpus for the superseded blueprint), **G-14b** (Ch 6's corpus may already carry the Deployment rolling-back page). Do those three lookups before opening any new fetches.

### Ship-blockers

1. **G-14a, restated because it is the only graded item in the chapter resting on an unsourced claim.** `appVersion` supports TYB1 Q5, its answer key, §4's closing subsection, a 🪢 Mnemonic, a Chapter Summary row, and a B7 ledger obligation ("Chart version vs `appVersion` | Ch 14 §4"). The fix is to extend the existing `helm-charts-2026-08-31` snapshot past its truncation point, not to add a snapshot. If it does not land, cut Q5 and reduce §4 to the sourced half.
2. **fig03's reader-facing "rev 4 ???".** Either resolve G-14g, or make the uncertainty explicit in prose so the question mark reads as deliberate: *"whether a rollback is itself recorded as a new numbered revision is not something Helm's own documentation settles here."* If the figure text changes, ch14-fig03's image-spec needs regeneration alongside fig02's.
3. **G-14d before TYB2 Q5 ships.** Confirm Ch 13 §7 states metrics-server's composition in the terms Soundings A2 and Q5 use. A retrieval item must retrieve something the reader was actually told.

### Should fix

4. §3 / Exam Alert: "so multiple operators could interact" → "so that multiple people could interact". Breaks an explicit "Never" in canonical forms.
5. §3: "rollback-by-revert" and "GitOps revert" → **`rollback by revert`**, twice.
6. §4: "with the release of Helm 3.8.0" → "as of Helm 3.8.0".
7. §3: add a half-clause at the quoted "rolls back to the previous release" noting that Helm's wording means the preceding *revision*. Practice A7 already does this work; the reader needs it where they first meet it.
8. `kubectl` code-style sweep (~12 unbackticked prose uses).
9. §6: "an ingress controller" → "an Ingress controller". Practice Q6 option A: "a Tiller pod" → "a Tiller Pod".
10. §5: *"Which is failure two from §1 in miniature: the API server serves the kinds it knows about, and nothing else."* Failure two is **ordering**; unknown-kind rejection was the *illustration* of it, not the failure itself. The four failures are the chapter's spine and get re-tabulated in §6, so precision here is load-bearing. Reword to "the same fact that made the CRD case in §1 sharp".
11. **`helm pull` is omitted.** B6 assigns it to §4 ("`helm repo` and `helm pull`"). The draft covers `helm repo`, demonstrates `helm push`, and never mentions `helm pull`. Either add a clause or record an AUTHOR-REVIEW noting the substitution — the revision notes address only the `kb_tags` side (adding `helm-push`), not the omission.
12. APIService: glossary entry + register row, or confirm Ch 13 §7 defines it. Graded twice.
13. §4: one reconciling clause for "Helm repositories" (sourced) against the chapter's own headword "chart repository". The chapter spends two 🪝 Snags teaching that `charts/` is not a repository, then introduces a third surface form without comment.
14. §4: Practice Q17's correct answer includes "must not contain the basename or tag on push", which §4's prose conveys only obliquely ("the basename is inferred from the chart's name, and the tag from the chart's semantic version"). State the clause.

### Optional — index-level and cosmetic

15. **B7 ledger rows to reconcile** (the ledger, not the chapter, is wrong in the first two):
    - `kubectl -k` → **`kubectl apply -k`**. The bare form is not a valid invocation. The draft is correct not to follow it; fix the ledger row and B6's §5 "owns" line.
    - "Go template (in the Helm sense) | Ch 14 §2" is now **orphaned** — G-14c removed the claim for want of a source. Restore on the fetch, or retire the row.
    - Add rows: Tiller (or `helm-2-to-helm-3`), chart archive, `helmCharts`, `HELM_DRIVER`.
    - "Helm" and "Release (Helm)" are recorded as first appearing in §2; both actually land in Why This Chapter Matters / §1. Chapter-level ownership is unaffected; cosmetic.
16. **Glossary queue:** APIService, eventual consistency, `helm repo`, `--dry-run`, `generatorOptions`, `helmCharts`, Tiller, `helm push`; register row for JSON 6902.
17. **fig01 is ~86 columns wide** — noticeably wider than fig02 (~70), fig05 (~77) and the rest. Outside this stage's remit, but worth running `check_reflow.py` before the EPUB gate rather than discovering it there.
18. "95% identical" → "nearly identical" in §1 prose and fig01's annotation (would require the fig01 image-spec regen).
19. §3's ⚠ block names GitOps without an accompanying pointer; the ledger's rule is "name only, **always** with a pointer". A pointer sits ten lines earlier in the same section, so this is genuinely optional.
20. The Voyage Ahead's three-item control-loop enumeration — see Callback correctness item 5. Author's call; no stated rule is broken.
21. The metadata line carries "Prerequisites: Standard", a vestige of the retired length formula's prerequisite factor (style ledger, LOCKED 2026-04-24). Harmless. Match whatever Ch 9–13 do; I cannot check.
22. `[interleaved: D1.1]` / `[interleaved: D1.4]` are reader-facing in the Practice stems. Confirm the D-numbering is **competency**-level (published on the LF exam page) rather than sub-topic-level — the chapter's own disclosure says CNCF publishes nothing beneath the competency, and the two must not appear to disagree.
```

Two things worth surfacing beyond the file itself:

- **The chapter is in good shape structurally.** All 42 cross-bearings resolve, all seven section numbers and titles match the skeleton, both mandatory downstream anchors are planted, and the ethics posture — particularly the authored-inference disclosure and the refusal to make any exam-frequency claim — is the strongest of the pass.
- **Three items are genuine gates, not polish:** G-14a (one graded item on an unsourced claim), fig03's unexplained "rev 4 ???" reaching the reader, and G-14d (a `[retrieval: ch13]` item whose correct answer may retrieve something Ch 13 never states). The last two are the ones the earlier diagnostics did not catch.
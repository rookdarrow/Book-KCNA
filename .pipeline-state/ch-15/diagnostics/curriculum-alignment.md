# Curriculum-Alignment Audit — KCNA Chapter 15

**Chapter:** 15 — *The Chart Is the Truth* · **Draft audited:** `draft-v1.md` (1310 lines) · **Audited:** 2026-08-31
**Authority:** `cncf-kcna-curriculum-pdf-2026-08-23` · **Supporting contracts:** `outline.md`, `research-manifest.md`

**Verdict: PASS with four required fixes.** Every concept the outline claims is present in the draft. Two of them are materially under-supported because the drafting stage received a **truncated copy of `argocd-auto-sync-policy-2026-08-31`** and wrote an AUTHOR-REVIEW asserting a gap the research manifest had already closed. One graded answer key attributes an unsourced claim to a snapshot that does not carry it. Neither is a coverage failure in the ordinary sense; both are correctable at Stage 11 from material already in the manifest.

---

## A note on granularity, read before the tables

The published authority for this chapter is three words. `cncf-kcna-curriculum-pdf-2026-08-23` line 15 gives:

> 16% – Cloud Native Application Delivery: **Application Delivery**; Debugging

There is no published sub-objective list, no topic enumeration, and no occurrence anywhere in the snapshot of *GitOps*, *Argo*, *Flux*, *twelve-factor*, *canary*, *blue-green*, or *CI/CD*. Audited strictly at published granularity, this chapter has exactly one objective row and it is covered.

That is a true audit and a useless one. So this file audits at **two** granularities: the published competency (below), and the authored concept ledger in `outline.md`'s `kb_tags.concepts`, which is the operational objective list every downstream stage actually consumes. **Everything in the second table is authored inference, not published curriculum**, and no finding in it should be read as a claim about what CNCF tests.

---

## Objectives the outline claims to cover

### Published granularity

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D3 | Cloud Native Application Delivery (16%) | YES | appropriate — one of three chapters splitting the domain |
| D3.1 | Application Delivery | YES | appropriate |
| D3.2 | Debugging | **NO — correctly deferred** | — (Ch 16; the Voyage Ahead at :1302 hands off explicitly) |

D3.2 is not a gap. The outline never claimed it, the barred-topics list explicitly excludes `kubectl debug`, ephemeral containers, and application-scope triage, and the draft holds that line — no occurrence of `kubectl debug` or "ephemeral container" anywhere in 1310 lines.

**Domain-weight disclosure is correct.** The metadata line (:4–6) states the published 16% with its tag and follows it with the house disclaimer that the Ch 14/15/16 split is authored. The frontmatter's `domain_weight_pct: 7` is never surfaced to the reader as a published figure. This satisfies B1 gap G33 and B2 disclosure #1.

**No-frequency-claims rule holds.** Zero occurrences of "frequently tested," "commonly appears," or any frequency claim. The Exam Alert (:1064) uses the sanctioned register — "distinctions that are easy to confuse, and they are the ones this material rewards getting right." Compliant with skill Part 14, Ethical Guardrail #8.

### Authored concept ledger (`kb_tags.concepts`, 37 entries)

| Concept | Claimed § | Covered? | Depth |
|---|---|---|---|
| twelve-factor-app | §1 | YES | appropriate |
| factor-iii-config-in-environment | §1 | YES | appropriate |
| factor-vi-stateless-processes | §1 | YES | appropriate |
| factor-ix-disposability | §1 | YES | appropriate |
| factor-xi-logs-as-event-streams | §1 | YES | appropriate |
| deployment-strategy-vocabulary | §2 | YES | appropriate |
| recreate-strategy | §2 | YES | appropriate |
| blue-green-deployment | §2 | YES | appropriate |
| canary-deployment | §2 | YES | appropriate |
| progressive-delivery | §2 | YES | appropriate |
| push-based-delivery | §3 | YES | appropriate *(unsourced — see G-15-1)* |
| pull-based-delivery | §3 | YES | appropriate |
| cicd | §3 | YES | **deep** — three terms fully defined under one tag |
| gitops | §3 | YES | appropriate |
| opengitops-four-principles | §3 | YES | appropriate |
| declarative-principle | §3 | YES | appropriate |
| versioned-and-immutable-principle | §3 | YES | appropriate |
| pulled-automatically-principle | §3 | YES | appropriate |
| continuously-reconciled-principle | §3 | YES | appropriate |
| blast-radius | §3 | YES | appropriate *(unsourced headword — see G-15-1)* |
| argo-cd | §4 | YES | appropriate |
| argo-cd-application-resource | §4 | YES | appropriate |
| source-of-truth | §4 | **partial** | delivered in §3 (:452, :514), not §4 — ownership drift |
| manifest-source | §4 | YES | appropriate |
| tracking-branch-tag-commit | §4 | YES | appropriate |
| synced-outofsync | §4 | YES | appropriate *(weakened — see fix 1)* |
| sync-operation | §4 | YES | appropriate |
| self-heal | §4 | **partial** | **shallow — under-covered.** One sentence (:649); default state absent; never retrieved |
| drift-detection | §4 | YES | appropriate |
| rollback-by-revert | §4 | YES | appropriate |
| delivery-agent-identity | §4 | YES | deep — proportionate; discharges two published pins |
| sync-hook-phases | §5 | YES | appropriate |
| sync-wave | §5 | YES | **over-covered in graded text** — see Depth mismatches |
| flux | §6 | YES | appropriate |
| flux-controller-set | §6 | YES | **over-covered** — 16 custom-resource names tabled, none tested |
| flux-bootstrap | §6 | YES | appropriate |
| multi-cluster-delivery | §6 | **partial** | Argo half sourced; **Flux half unsourced and graded** — see fix 2 |

**Budget compliance (all exact).** Soundings 8/8 · Bearings 16/16 across three checkpoints (6+5+5) · retrieval 4/16 = **25.0%**, the arc-outline ceiling hit precisely · Practice 21/21 · total 45/45 · figures 7/7 at their contracted anchor IDs, including the out-of-document-order `ch15-fig05` pin inside §3.

**Section pins honored.** All nine published numbered cross-bearings land where they were promised: §3 (push/pull), §4 (agent identity, rollback promise), §5 (ordering), §7 (Zenith). No section was merged, split, or renumbered.

**Practice allocation drifted by one:** §4 carries 6 items (Q13–Q18) against a planned 5; §6 carries 1 (Q21) against a planned 2. Total is unchanged. Recorded rather than flagged as a defect — Q18's three-way rollback discrimination is the chapter's own contribution and earns its slot. But see the §6 depth finding: §6 gained the most unplanned prose in the chapter while losing its second practice item, which is the wrong direction.

---

## Objectives covered in the draft but NOT in the outline

Drift risk: material that expanded scope beyond the outline. Ranked by how much author attention each deserves.

**1. Flux's RBAC model and the Kubernetes Impersonation API (§6, :879–:891). Research-sanctioned; ledger needs updating, not the draft.**
The outline's §6 introduces four concepts, none of them security. The draft adds a full subsection on `crd-controller`, `cluster-reconciler`, `cluster-admin` binding, soft multi-tenancy, and `.spec.serviceAccountName` impersonation. This looks like scope creep and is not: `research-manifest.md` note 7 explicitly recommends the narrowing mechanisms be used, on the grounds that they convert the §4 identity pin "from a warning into a demonstration" and land Ch 12 §3's lesson in production form. The draft split the recommendation — Argo's ClusterRole narrowing into §4, Flux's impersonation into §6 — which is a defensible reading. **Action: none to the draft. Add `delivery-agent-identity` and `blast-radius` to §6's introduces-list in `kb_tags`, and record the §6 expansion so B7's next run does not treat it as unowned.**

**2. Continuous delivery and continuous deployment as separately defined terms (§3, :392–:402).** The outline's acronym register (Open Question 10) authorized expanding CI, CD, and CI/CD once at first use. The draft goes further and gives each a full CNCF definition plus a Snag on the CD/CD collision. This is good teaching and manifest note 10 endorses it, but the concept index carries only `cicd`. **Low risk. Action: add `continuous-integration`, `continuous-delivery`, `continuous-deployment` as concept tags, or note in the ledger that `cicd` covers all three.**

**3. Argo CD component architecture — API server, repository server, application controller (§4, :534, :576, and Q14's key at :1224).** Not in the outline's §4 list. It earns its place: the repository server is what makes the manifest-source claim non-obvious, and Q14 turns on it. **No action.**

**4. `SyncFail` as a fourth hook phase (§5, :786).** The outline specified three. Manifest note 6 recommends "one clause," and the draft gives roughly that. But **Safe Harbor (:1058) and the Chapter Summary (:1297) both say "PreSync → Sync → PostSync" and omit it**, so the body teaches four and the summaries recall three. **Action: make them agree — either add SyncFail to both summary rows or drop it to a parenthetical in the body.**

**5. `Refresh` as a distinct Argo CD glossary term (§4, :564).** Minor, supports `sync-operation`. **No action.**

**6. Commands appear while `kb_tags.commands` is empty by design.** `git revert` is taught in prose (:661) and `argocd cluster add` appears inside a quotation (:689). The outline's COMMANDS NOTE anticipated exactly this: "`git revert` is the single plausible exception… add it here rather than letting the concept index under-claim." **Action: add `git revert` to `kb_tags.commands`. Leave `argocd cluster add` out — it is quoted, not taught, and no item turns on it.**

**7. A/B testing was dropped from What You'll Learn (:134) contrary to the outline's bullet.** Correct call, and better than the outline's own fallback — see the gaps section. **Action: correct the B6 skeleton and the B7 ledger so A/B is not re-asserted as a fifth strategy in a later regeneration.**

---

## Depth mismatches

Depth is judged against exam weight, not volume. The whole chapter serves one competency inside a 16% domain, split three ways by authored allocation, so the calibration question is *relative* — which topics carry more graded surface than their share of an already-inferred allocation.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| twelve-factor (§1) | authored, ⚪ tier | 12 named, 4 developed | OK — the outline's ruling held exactly |
| deployment strategies (§2) | authored, highest-yield | deep, 4 PQ | OK |
| push/pull + four principles (§3) | authored, chapter core | deep, 5 PQ | OK — best-sourced material in the corpus |
| Argo CD object model (§4) | authored, chapter core | deep, 6 PQ | OK |
| `self-heal` (§4) | authored | **shallow** | **under-covered** — one sentence, no default, zero graded items, absent from Safe Harbor and Chapter Summary |
| `sync-wave` (§5) | authored, 🟡 above tier | deep in graded text | **over-covered** — see below |
| `flux-controller-set` (§6) | authored | 16 CR names tabled | **over-covered** — recall surface with no assessment and no exam basis |
| multi-cluster (§6) | authored | 1 PQ | OK by count; sourcing is the problem, not depth |

**`sync-wave` over-coverage — the clearest depth finding.** The outline's §5 depth ruling is unambiguous: *"Teach the shape… and do not teach annotation syntax. A reader who can name the three phases and say why ordering is a problem GitOps has has learned everything this section owes them."* Manifest note 6 repeats it: *"annotation syntax is captured in the snapshot but should not reach the page."*

The draft puts `argocd.argoproj.io/sync-wave` on the page three times — body (:799), TYB3 Q1 key (:922), and PQ19 key (:1251) — and **two graded items require the reader to produce the annotation string and assign wave values**. §5 is marked 🟡 precisely because it sits above associate tier; grading vendor annotation-key recall there is the deepest ask in the chapter attached to its most explicitly out-of-scope material. The four-key precedence sort's steps 3 and 4 (by kind, by name) are Argo-internal detail with no plausible exam value.

Note what is *right*: the draft teaches the negative-wave fact, which manifest note 6 singled out as "the one detail I'd argue *is* worth teaching, because it is what makes waves an ordering system rather than a queue." Keep that. It is the string recall that overshoots.

**`flux-controller-set` over-coverage.** The §6 table (:857–:865) lists sixteen custom-resource names across five controllers. Nothing tests them; Q21 tests composability and multi-cluster only. This is the same shape of problem B3 barred for the graduated-projects roster: a dated vendor list presented as a memorization surface, where the durable content is the *contrast* (integrated vs composable), not the inventory. The section that gained the most unplanned prose also lost a practice item — content up, assessment down.

**`self-heal` under-coverage** is treated as fix 1 below, because its cause is upstream.

---

## Gaps the research stage flagged

`research-manifest.md` recorded four gaps and three must-not-write-from-memory facts. Handling, item by item:

| Gap | Status | Draft handling |
|---|---|---|
| **G-15-1** — push-side credential argument and the term "blast radius" unsourced; `opengitops.dev/faq` is a 404 and no corpus source uses the phrase | **OPEN — verified unclosable** | ⚠ **Not handled.** See below |
| **G-15-2** — Flux's multi-cluster topology unsourced | **OPEN** | ⚠ **Not handled, and mis-attributed in a key.** See fix 2 |
| **G-15-3** — `AppProject` is on declarative-setup, not core-concepts | Closed / advisory | ✅ Draft cites the right snapshots throughout; `AppProject` correctly not taught at associate tier |
| **G-15-4** — no source enumerates LFS250 modules | OPEN, unchanged from Ch 14 | ✅ Handled exactly as Open Question 7 prescribed: one back-bearing at :121, one sentence of positive basis (Argo/Flux graduated, OpenGitOps a CNCF project), then silent enforcement |
| **OQ 8(a)** — is self-heal on by default? | **PINNED by research: OFF** | ❌ **Draft asserts the opposite — that it is unanswerable.** See fix 1 |
| **OQ 8(b)** — Flux's five-minute interval | Pinned with a caveat | ⚠ Flagged in an AUTHOR-REVIEW (:887) but the caveat does not reach the graded key. See fix 3 |
| **OQ 2** — A/B testing: fetch or drop | **RESOLVED** | ✅ **Best handling in the chapter.** See below |

**G-15-1 is not handled, and the manifest was specific about what handling looks like.** It reads: *"Drafting may develop the argument as an architectural consequence… but it may not attribute the push-side characterization or the term 'blast radius' to a source. Recommend the draft either frames it explicitly as the book's own reading, or drops 'blast radius' as a headword and keeps `blast-radius` in `kb_tags` as a glossary-only concept."*

The draft takes neither option. "Blast radius" is introduced as a headword at :442 (*"The term for this is blast radius"*), promoted into Safe Harbor (:1051) and the Chapter Summary (:1286), and **graded twice** — TYB2 Q3 (:740) and PQ10 (:1132). The four consequences under Figure 15.3 (:440–:446) carry cross-bearings but no `[source:]` tags, and the push-side premise (*"a pipeline outside the cluster holds credentials to the cluster"*) is stated as fact. Against a book whose stated rule is that every factual sentence carries a source tag, and in the chapter that most loudly defines its own terms, silence is the wrong handling. The argument itself is sound and worth keeping; it needs one framing clause.

**G-15-2 is worse than unhandled — it is mis-attributed.** PQ21's key at :1265 states *"Flux's model is one Flux per cluster, each bootstrapped into its own repository or path and pulling independently, with no cluster holding credentials to another [source: flux-concepts-2026-08-31]."* The manifest verified that page **does not describe a multi-cluster topology at all**. A graded answer key is citing a snapshot for a claim it does not carry. The same claim appears untagged in the body at :895.

**OQ 2 — exemplary, and worth recording as precedent.** The manifest resolved A/B in an unexpected direction: it is documented on the Argo Rollouts *Experiment* CRD page as product experimentation, and the string "A/B" does not appear on the Canary strategy page at all. The manifest recommended keep-but-demote. §2's "One term this book will not teach you" (:319–:327) does exactly that — names it, sources it to `argo-rollouts-experiments-2026-08-31`, draws the real distinction (measuring *preference over a long duration* versus measuring *broken, as briefly as possible*), and closes the loop for the reader with "Nothing in this chapter's questions turns on A/B testing." A/B appears in no stem, key, or distractor. This is stronger than either the outline's fallback cut or the original listing.

**Also correct, unprompted:** manifest note 5's authority-priority rule. §2 presents Argo Rollouts' neutral mechanical description of blue/green and then lets CNCF's disapproving "smell" assessment follow (:283–:285), with CNCF's whole-system scoping caveat intact. CNCF is the exam authority; Argo is a vendor project; where they differ CNCF governs. The draft got the ordering and the attribution right without being told twice.

---

## Recommended fixes

Ordered by consequence. Fixes 1 and 2 should be treated as required before Stage 11 signs off; 3–6 are cleanups.

**Fix 1 — §4: delete the false AUTHOR-REVIEW at :651 and write self-heal's default from the research manifest. Highest-value fix in the chapter.**

The AUTHOR-REVIEW asserts that *"whether self-heal is enabled by default is not answerable from the cached corpus"* and that `argocd-auto-sync-policy-2026-08-31` *"is truncated at the declarative example."* That is true of the copy the drafting stage received and false of the snapshot. `research-manifest.md` lines 309–331 carry two headings reading, literally, **"Automatic pruning — DISABLED BY DEFAULT"** and **"Automatic self-healing — DISABLED BY DEFAULT"**, with the quotations:

- *"By default, changes that are made to the live cluster will not trigger automated sync."*
- *"By default (and as a safety mechanism), automated sync will not delete resources when Argo CD detects the resource is no longer defined in Git."*
- *"An automated sync will only be performed if the application is `OutOfSync`."*
- The automated sync interval *"defaults to `120s` with added jitter of `60s` for a maximum period of 3 minutes."*

This is not a missing detail. It is the chapter's second Fixed Point losing its best proof. Manifest note 2 saw it first: out of the box Argo CD **reports** drift and does not revert it, which is *"a better fit for the chapter's Fixed Point ('OutOfSync is a drift signal, not an error') than the reverting behavior would have been."* The Fixed Point at :600 currently rests on inference; it can rest on a documented default.

Three consequences follow, and the third is a live defect:

- **The chapter now teaches a misconception it never corrects.** §6 tells the reader that Flux *"promptly reverts"* manual `kubectl` changes (:874) and grades that behavior in TYB3 Q4 (:945). A reader generalizes: GitOps agents revert manual edits. Argo CD, by default, does not. Nothing in §4 blocks the generalization. Adding the default turns this into the chapter's sharpest ⚠ — *readers who assume the agent always reverts are wrong by default, and the two graduated implementations differ.*
- **Two graded items assume a capability that is off by default.** TYB2 Q4 (:715) and PQ16 (:1154) both premise *"delete resources that have been removed from the repository."* That is pruning, and pruning is opt-in. The items still work — they test RBAC, and the agent must be *permitted* to delete before it can be *configured* to — but the stems should not imply the behavior is automatic. One qualifier each ("…and, where pruning is enabled, delete resources removed from the repository") fixes both.
- **Argo CD gains a concrete reconciliation cadence** (120s + 60s jitter, max 3 minutes) to sit beside §6's Flux figure, which is currently the only number in the chapter.

Then give `self-heal` one graded item. It is a named owned concept appearing exactly once and retrieved nowhere; the auto-sync / self-heal / manual-sync distinction is a clean three-way discrimination and belongs in TYB 2 or as a §4 practice item.

**Fix 2 — §6 and PQ21: remove the unsourced Flux multi-cluster claim, or replace it with what is sourced.**

Per G-15-2, rewrite :895 and the "Multi-cluster difference" paragraph in the PQ21 key at :1265. The mis-attribution to `flux-concepts-2026-08-31` must go regardless — a graded key citing a snapshot for a claim it does not carry is the one defect in this chapter that cannot be argued as a judgment call.

The manifest supplies the replacement: soften to *"Flux's controllers run in the cluster they reconcile,"* which **is** supported by `flux-security-2026-08-31`, and let the contrast rest on the sourced asymmetry — Argo CD stores external clusters' credentials as Secrets in the `argocd` namespace [`argocd-security-cluster-credentials-2026-08-31`], and Flux's documented model has no equivalent. That preserves the section's teaching point and the blast-radius callback at :897 without asserting a topology no source states. Alternatively, cut the comparison to a single sourced sentence about Argo CD and drop the multi-cluster half of Q21.

**Fix 3 — §6 / TYB3 Q4: keep the five-minute caveat out of the answer key, or put it in.**

The AUTHOR-REVIEW at :887 correctly records manifest note 3's tension — `flux-concepts` says five minutes by default, the Kustomization API reference says `.spec.interval` is required with a 60-second minimum and declares no default, so "five minutes" describes Flux's bootstrap-generated Kustomization, not an API default. But TYB3 Q4's key (:945) grades on *"within roughly five minutes"* with no qualification, so the caveat is flagged for the author and hidden from the reader who is being marked on it.

Manifest note 3's recommendation applies directly: **secure the behavior, not the number.** Grade Q4 on *"the change is reverted, because principle 4 is continuous"* and let the interval appear as "typically five minutes, and always explicitly configured." The ⚓ Worth Securing at :876 already quotes the load-bearing sentence and needs no change.

**Fix 4 — §3: give the blast-radius argument one framing clause.**

Per G-15-1. The cheapest compliant version is a single sentence before or after :442 marking the push/pull risk comparison as this book's reading of principle 3 plus the two projects' documented in-cluster credential storage — not a claim any source makes in those terms. Two of the four consequences can also be anchored to tags now available: the credential-location consequence to `argocd-security-cluster-credentials-2026-08-31`, and the nothing-watches-between-deploys consequence to `cncf-glossary-gitops-2026-08-31`'s naming of drift as the problem GitOps addresses. `argocd-best-practices-2026-08-31` supplies the access-separation rationale directly (*"The developers who are developing the application, may not necessarily be the same people who can/should push to production environments"*), which is the closest thing in the corpus to the push-side argument and is currently unused in §3.

Keep the term. It is the right word and the reader will meet it in the field; it just needs to be visibly the book's word rather than an implied quotation.

**Fix 5 — §5: stop grading the annotation string; keep the negative-wave idea.**

Rewrite TYB3 Q1 (:922) and PQ19 (:1251) to test *ordering behavior* — which object must land first and why, what happens to a resource with no annotation, why negatives exist — without requiring the reader to produce `argocd.argoproj.io/sync-wave`. Leave the annotation in the body at :799 as illustration, where the closing line already says it is "here for concreteness, not for memorization." At present that line is contradicted by the two items that follow it. Consider dropping precedence steps 3 and 4 (by kind, by name) from the quoted algorithm; they add recall surface and answer no question a reader will be asked.

**Fix 6 — ledger and index corrections (no draft edits).**

- Reassign `source-of-truth` from §4 to §3 in the B7 term-ownership ledger, or move one definitional sentence into §4. The draft delivers the concept at :452 and :514; the ledger records §4.
- Add `delivery-agent-identity` and `blast-radius` to §6's introduces-list.
- Add `git revert` to `kb_tags.commands`, which is currently `[]`.
- Add the three CI/CD sub-terms as concept tags, or record that `cicd` covers all three senses.
- Record that A/B testing is **not** a fifth deployment strategy, with the `argo-rollouts-experiments-2026-08-31` basis, so B6 and B7 do not re-assert it on regeneration. Also drop it from the outline's What You'll Learn bullet, which the draft correctly already ignores.
- Make SyncFail consistent between the §5 body and the Safe Harbor / Chapter Summary rows.
- Trim the §6 controller table to controller names plus one representative custom resource each, or mark it explicitly as reference rather than recall.

**Recorded, no action:** the outline's Open Question 5 (figure `ch15-fig04`'s slug naming hooks it does not carry) is handled as the outline recommended — the anchor ID is unchanged, the figure renders sync states only, and `ch15-fig06` discharges the hooks half in §5. Figure captions number sequentially in reading order (15.1–15.7) while anchor IDs keep their contracted numbering, which is the correct resolution of the §3 `fig05` pin. Neither is a curriculum-alignment matter; both are noted so the integration stage does not read them as drift.
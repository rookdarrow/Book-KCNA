# Fact-Accuracy Audit — Chapter 17

**Mode detected: STANDARD.** The cached corpus contains 45 snapshots, and the draft carries inline `[source: ...]` tags throughout (~180 of them). Untagged factual claims are therefore FAIL.

**Anchoring note.** The draft was supplied to this stage inline (`draft-v2.md` absent; audited against `draft-v1.md` content), without line numbering. Findings are anchored by section heading + paragraph/callout so the revision stage can locate them unambiguously; where a line number is given it is approximate.

## Summary

- Total factual claims inspected: **186**
- Tagged claims verified: **168**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — every `[source:]` tag in the draft resolves to a snapshot present in this corpus
- **Untagged factual claims (FAIL): 10 findings, covering 16 sentences**
- **Contradicted claims (FAIL): 2**
- Minor discrepancies (WARN): **14**

---

## FAIL — Untagged factual claims

### F1. §"Why This Chapter Matters", Dead Reckoning block: "Domain 4 has three competencies."

Full span: *"Domain 4 has three competencies. Observability belongs to Chapter 18. This chapter carries the other two: Cloud Native Ecosystem and Principles, and Cloud Native Community and Collaboration."* and *"CNCF publishes weights for the four domains and does not publish weights for the competencies inside them."*

**Why it's a factual claim:** It asserts the internal structure and the names of the sub-competencies of a published exam blueprint, and separately asserts what CNCF does and does not publish.

**Corpus check:** `cncf-kcna-certification-page-2026-08-23` states the four domain names and weights and nothing else; its "Not stated on this page" section does not mention competencies at all. No cached snapshot names D4's competencies or their count. The `D4.2`/`D4.3` identifiers that appear in snapshot frontmatter are pipeline metadata, not source statements.

**Fix:** Open a research gap for the KCNA curriculum document (`github.com/cncf/curriculum` — the manifest already tracks `cncf-curriculum-repo-kcna-versions-2026-08-23` as an open gap) and tag both sentences to it once cached. The `12%` in the same paragraph is correctly tagged and is not in question.

---

### F2. "Common Traps" table, last row, and "The Voyage Ahead", ¶2 — the pre-change five-domain blueprint

Trap row: *"Observability is no longer a standalone domain, Container Orchestration rose to 28%, and Application Delivery doubled to 16%."*
Voyage Ahead: *"Under the old five-domain blueprint, Cloud Native Observability was a standalone domain with its own weight."*

**Why it's a factual claim:** "rose to 28%" and "doubled to 16%" are arithmetic assertions about a prior published blueprint (22% → 28%, 8% → 16%). They only mean anything if the old weights are established fact.

**Corpus check:** The only place in the corpus carrying the old split (46/22/16/8/8) is `provenance-kcna-60-questions-2026-08-23`, whose header reads **"DO NOT CITE THE CONTENTS OF THIS FILE AS FACT"** and which records the old blueprint as *"NOT independently sourced. See cncf-curriculum-repo-kcna-versions-2026-08-23.md (open gap)."* That snapshot exists to document provenance, not to supply it.

**Fix:** This is the highest-priority item in the audit — two comparative claims resting on a source the corpus explicitly bars. Either (a) narrow both to what is sourced: Observability is not one of the four current domains, and the current weights are 44/28/16/12 `[source: cncf-kcna-certification-page-2026-08-23]`, dropping "rose to" and "doubled"; or (b) hold both until the curriculum-repo gap is closed and the old blueprint is authoritatively cached.

---

### F3. §2, "Worth Securing" callout: "the foundation graduates several projects a year"

**Why it's a factual claim:** A rate claim about CNCF's behaviour.

**Corpus check:** Nothing in `cncf-project-maturity-levels-2026-08-23`, `cncf-toc-project-lifecycle-process-2026-08-31`, or `cncf-who-we-are-2026-08-23` states a graduation rate.

**Fix:** The callout's argument survives without it. Replace with the durable, sourced form: the roster is dated data and the levels are not. If the rate is wanted, it needs a cached source.

---

### F4. §5, ¶ following the Fixed Point: "Istio, the most widely deployed mesh, states its own version…"

**Why it's a factual claim:** A market-position/deployment-share assertion about a named third-party project, made in the book's own voice.

**Corpus check:** `istio-service-mesh-2026-08-23` says *"Istio is the most popular, powerful, and trusted service mesh"* — that is Istio's self-description on its own site, and it says *popular*, not *most widely deployed*. No snapshot supports a deployment-share ranking.

**Fix:** Use the formulation the section's own Closer Look already uses and which is defensible as authorial judgment — "the most widely documented" — or attribute: "Istio, which describes itself as the most popular service mesh, states…".

---

### F5. §4, closing paragraph, and Q10 answer — the Helm `crds/` directory

*"Helm charts have a `crds/` directory precisely because a chart that ships custom resources has to install the definitions before the objects that use them."*

**Why it's a factual claim:** A statement about a third-party packaging format's design and rationale.

**Corpus check:** No Helm snapshot exists in this chapter's corpus. Q10's answer cites `[cross-reference: Ch 14 §6]`, which is a book-internal pointer, not a source tag.

**Fix:** Either tag to whatever Helm snapshot Ch 14 §6 used (the cheapest fix, if that snapshot is in the full `sources/` tree), or open a research gap for helm.sh's chart-structure documentation. Note this claim carries real exam weight — it appears as a graded practice question — so a cross-reference is thinner support than it needs.

---

### F6. §8 — public SIG meetings

Three sentences: *"Every interface in §4 has a group of people behind it with a public meeting on a public calendar."* / Logbook: *"Every SIG has a public meeting on a public calendar, and every one of them has issues nobody has picked up."* / *"And it is free, public, and on the calendar this week."*

**Why it's a factual claim:** A universal ("every SIG") operational claim about the project, plus an availability claim about a public calendar.

**Corpus check:** `k8s-sig-list-and-groups-2026-08-31` supplies the roster and says SIGs "follow these guidelines"; `k8s-community-governance-2026-08-23` supplies the principle that "work and collaboration should be done in public". Neither states that every SIG holds a public meeting on a public calendar. The upstream `sig-list.md` does carry per-SIG meeting schedules, but that portion was not transcribed into the snapshot.

**Fix:** Re-fetch `sig-list.md` capturing the meeting-schedule columns, or soften "every" to what governance supports (work is done in public; SIG meetings are open). The invitation loses nothing by being scoped.

---

### F7. §8, Logbook Entry: "A great many people on the contributor ladder got their first merged PR by fixing documentation that was wrong…"

**Why it's a factual claim:** A prevalence claim about contributor behaviour.

**Corpus check:** Unsupported anywhere in the corpus. `k8s-community-membership-ladder-2026-08-23` gives requirements, not first-contribution demographics. Note that "SIG Docs exists. So does SIG Contributor Experience." **is** supported — both appear in the `k8s-sig-list-and-groups-2026-08-31` roster.

**Fix:** Mark as authorial experience explicitly (the book already uses that register — Ch 1's "in my experience"), which converts it from an unsourced fact to a stated judgment.

---

### F8. Taking Your Bearings 2, Q3 answer, option B explanation: "Some CNI plugins offer encryption as an additional feature."

**Why it's a factual claim:** A capability claim about third-party software.

**Corpus check:** `k8s-docs-network-plugins-2026-08-24` does not mention encryption; no other snapshot does.

**Fix:** The sentence is doing only defensive work in a distractor explanation. Deleting it costs nothing — the load-bearing half ("nothing in the Kubernetes network model requires it and nothing in the described setup provides it") is sound and follows from the network-plugins snapshot.

---

### F9. Practice Q2 answer, option D explanation: "conformance certification is a real CNCF program but has nothing to do with whether a platform meets this definition."

**Why it's a factual claim:** Asserts the existence and scope of a named CNCF program.

**Corpus check:** No snapshot in the corpus mentions Certified Kubernetes Conformance. `cncf-who-we-are-2026-08-23` enumerates CNCF *certifications for people* (KCNA, KCSA, CKA, CKAD, CKS, CNF) and does not cover platform conformance.

**Fix:** Delete the clause, or tag it to a cached conformance page. The distractor is refuted adequately by "invents a certification requirement that appears nowhere [in the definition]".

---

### F10. Practice Q8 answer, option A explanation: "describes the pre-CSI in-tree model that CSI migration exists to move away from."

**Why it's a factual claim:** Names a Kubernetes feature ("CSI migration") and a historical architecture ("in-tree volume plugins").

**Corpus check:** `csi-spec-objective-2026-08-25` states CSI's objective and goals; it says nothing about in-tree plugins or a migration effort. No other snapshot covers it.

**Fix:** Reduce to what the CSI spec supports — that CSI exists so a vendor can "develop a plugin once and have it work across a number of container orchestration (CO) systems" — or tag to whatever snapshot Ch 11 §5 used for the in-tree history.

---

## FAIL — Contradicted claims

### C1. §5, "mTLS, zero trust, and the leg that was unprotected", ¶ beginning "The mechanism has four named components"

**Tag:** `[source: istio-security-mtls-identity-2026-08-31]`

**Draft says:** *"The mechanism has four named components: a **Certificate Authority** for key and certificate management; a **configuration API server** that distributes authentication policies, authorization policies, and secure naming information to the proxies; and **sidecar and perimeter proxies** acting as Policy Enforcement Points."*

**Snapshot says:** *"Security in Istio involves multiple components: A Certificate Authority (CA) for key and certificate management; The configuration API server distributes to the proxies: authentication policies, authorization policies, secure naming information; Sidecar and perimeter proxies work as Policy Enforcement Points (PEPs) to secure communication between clients and servers."*

**The problem:** The snapshot enumerates **three** components and says "multiple", not "four". The draft's own enumeration also lists three (CA; configuration API server; sidecar and perimeter proxies). The stated count contradicts both the source and the sentence it introduces.

**Recommended fix:** Change "four named components" to **"three named components"**, matching the cached snapshot and the draft's own list. Do not resolve this by splitting "sidecar and perimeter proxies" into two — the snapshot treats them as one item. (If a later research pass finds the live Istio page carries a fourth item, the snapshot must be refreshed before the count changes.)

---

### C2. §1, ¶ after the block quote — and two further occurrences: "Twelve words in, the definition rules out the most common reading of the term it defines."

**Tag:** context is the block quote tagged `[source: cncf-cloud-native-definition-2026-08-23]`; the two repeats are Taking Your Bearings 1 answer 1 (*"the definition rules it out twelve words in"*) and Practice Q2 answer (*"'public, private, hybrid cloud' appears twelve words into the definition"*).

**Snapshot says:** *"Cloud native practices empower organizations to develop, build, and deploy workloads in computing environments (public, private, hybrid cloud)…"*

**The problem:** Counting the snapshot's own text, "public" is word **15** (Cloud·native·practices·empower·organizations·to·develop·build·and·deploy·workloads·in·computing·environments = 14). Word twelve is "in". No counting convention yields twelve.

**Recommended fix:** Replace all three occurrences with a formulation that cannot go stale or wrong — "in its first sentence" / "before the first sentence is half over" — or correct to "fifteen words in". Because the number appears three times, in body prose and in two graded answer explanations, fix all three together.

---

## WARN — Minor discrepancies

**W1. Attention Budget arithmetic (front matter).** Header says *"Total time: ~95 minutes"*; the table's own rows sum to **118 minutes** (10+8+12+6+8+12+14+7+8+10+12+7+4), and the table omits Why This Chapter Matters, the Exam Alert, 21 practice questions, and the Chapter Summary. 95 is exactly the running total through §7, which suggests rows were added after the header was written. Relatedly, *"If you only have 15 minutes: read §4 and §9 together, then take Taking Your Bearings 2"* prescribes 12+4+7 = 23 minutes of listed content. Not source-checkable and strictly outside this stage's remit, but cheap to fix and mechanically wrong.

**W2. Two epigraphs are quoted with inline attribution but no source tag.** Opening: *"We democratize state-of-the-art patterns…" — CNCF Cloud Native Definition v1.1*. Closing: *"Trust is a vulnerability." — CNCF Cloud Native Glossary*. Both verify **verbatim** against `cncf-cloud-native-definition-2026-08-23` and `cncf-glossary-zero-trust-architecture-2026-08-31` respectively. Not scored as FAIL because each names its document inline and the text is exact; add tags for consistency with the rest of the chapter.

**W3. §1: "That is CNCF Cloud Native Definition v1.1, in full and unabridged."** The four quoted paragraphs match the snapshot exactly, but the snapshot carries no completeness marker of its own, so "in full and unabridged" is an assertion about the cached text rather than one derived from it. Low risk; consider "That is CNCF Cloud Native Definition v1.1" or add a completeness note to the snapshot on next refresh.

**W4. §1: "part of the nonprofit Linux Foundation" is tagged to the wrong snapshot.** The sentence carries only `[source: cncf-charter-governance-bodies-2026-08-31]`, which supplies the mission line but not the Linux Foundation relationship. That fact is verbatim in `cncf-who-we-are-2026-08-23`: *"The Cloud Native Computing Foundation is part of the nonprofit Linux Foundation."* Add the second tag.

**W5. §5: the zero-trust block quote splices two sections of one glossary entry.** The draft prints the "In many networks today…" paragraph and *"Zero trust architecture however, recognises that trust is a vulnerability"* as one continuous quotation with a paragraph break. In `cncf-glossary-zero-trust-architecture-2026-08-31` the first belongs to the opening definition and the second to "Problem it addresses". Both are verbatim; the splice is undisclosed. Add an ellipsis or split into two quotations.

**W6. §5: "which is the reason ambient mode exists at all."** The quoted sentence — sidecar mode *"uses more computing resources and becomes more complex to manage as your system grows"* — is verbatim `[source: cncf-glossary-service-mesh-2026-08-31]`, but that entry's contrast case is the **sidecarless/eBPF** model, not Istio ambient (and the snapshot's drafting note bars the eBPF framing from graded text — correctly respected in the draft). No source states ambient mode's motivation. Soften to a pressure-not-cause formulation: "which is the pressure ambient mode is responding to".

**W7. §6: "request-driven" phrasing.** `knative-serving-autoscaling-2026-08-31` carries an explicit "Not stated on this page" note: *"The page does not use the phrase 'request-driven scaling model'."* The draft's "request-driven autoscaler" / "request-driven, scaled to zero when idle" is a fair paraphrase of Serving's sourced "HTTP-triggered autoscaling container runtime", but it must stay outside quotation marks and should not migrate toward the barred phrase in revision.

**W8. §6: "with a request-driven autoscaler attached and a floor of zero instead of one."** Unsourced, and loose as stated: a Deployment's replica count can be set to zero by hand. What Knative adds is the *automatic* return from zero on a request. Recommend: "…and an autoscaler that will take it to zero and bring it back on a request."

**W9. §7 and two echoes: "No metrics-server, no Metrics API, no HPA scaling."** The tagged snapshot calls metrics-server *"a reference implementation of the Metrics API"* and says *"you need an API extension server that provides the Metrics API"* — i.e. one implementation, not the only possible one. Same absolutism in Soundings answer 5 (*"there is nothing serving that API"*) and Q18's answer. Not wrong in practice; strictly overstated against the source. Consider "no Metrics API server — metrics-server or an equivalent — no HPA scaling."

**W10. §7, Worth Securing: "KEDA and Knative are stated as CNCF Graduated in their documentation."** True for Knative (`knative-overview-2026-08-23`: *"Knative is a CNCF graduated project"* — Knative's own docs). For KEDA, the corpus's statement is on **kubernetes.io** (`k8s-docs-autoscaling-and-vpa-2026-08-31`: *"KEDA is a CNCF-graduated project"*), not KEDA's documentation. Both also appear on the graduated roster in `cncf-project-maturity-levels-2026-08-23`. Fix the attribution clause; the contrast with Karpenter is otherwise sound and well sourced.

**W11. §7: the VPA quotation reproduces the source's own typo.** *"…but is a an add-on…"* is verbatim from `k8s-docs-autoscaling-and-vpa-2026-08-31`. This is correct quoting practice. Flagged so a later voice or copyedit stage does not silently "fix" it and thereby break verbatim fidelity — if it reads badly, add `[sic]` or paraphrase out of quotation, do not edit inside the quote marks.

**W12. §8: SIG-ownership mapping is tagged to a roster-only snapshot.** *"SIG Network owns the material of Chapters 9 and 10. SIG Storage owns Chapter 11's… SIG Autoscaling sponsors both node autoscalers… [source: k8s-sig-list-and-groups-2026-08-31]."* That snapshot lists SIG **names** and nothing about their ownership scope. The SIG Autoscaling sponsorship claim is genuinely sourced, but by `k8s-docs-node-autoscaling-2026-08-31` (*"the two Node autoscalers currently sponsored by SIG Autoscaling"*). Add that tag; the chapter-to-SIG mapping is the book's own and should read as such.

**W13. §8: the Cloud Native Community Groups description is tagged to the wrong snapshot.** *"free, volunteer-run local meetups, including Kubernetes Community Days"* is tagged `[source: cncf-mentoring-and-community-groups-2026-08-31]`, which says only that CNCF *"supports the worldwide community of the Cloud Native Community Groups (CNCGs)."* The quoted characteristics are in `cncf-landscape-and-community-2026-08-23`: *"free, volunteer-run meetups on the CNCF community platform, including Kubernetes Community Days."* Add the second tag.

**W14. §8: KCSA expansion, and the scope of the closing Mnemonic.** (a) *"CNCF also offers **KCSA** — the Kubernetes and Cloud Native Security Associate"* — `cncf-who-we-are-2026-08-23` gives the acronym inside a list and does not expand it; the expansion is unsourced. (b) The Mnemonic *"KCNA is the only one you can pass by knowing things"* sits one paragraph after KCSA is named, and no snapshot states KCSA's format, so the superlative reaches further than the corpus supports. Scope it: "KCNA is the only one on this ladder — CKA, CKAD, CKS — you can pass by knowing things."

**Also noted, not counted as findings:**

- **Claims carried by cross-bearing rather than by tag.** Several external facts owned by earlier chapters recur here untagged: NetworkPolicy cannot encrypt (Soundings 8, §5, TYB2 Q3, Q13, Common Traps, Summary), TLS terminates at the Ingress, a sidecar shares the Pod's network namespace and therefore `localhost` (Soundings 4), Ingress/Gateway API doing L7 north-south routing (§5 table), preemption evicting lower-priority Pods (Q19), and image immutability by digest (§3 Snag). Each carries an explicit `[cross-bearing: …]` to the section that taught it, which appears to be the pipeline's deliberate convention for re-asserted facts. Recorded here so the convention is a visible decision rather than an oversight; if the convention is meant to hold, no action.
- **Book-internal counts, not checkable against snapshots.** "Four hundred pages ago"; Ch 1 "pointed here, three separate times"; "Nine chapters fed it. Twenty-six cross-references from earlier chapters pointed at it"; and the block-quoted sentence attributed to Chapter 1. These belong to the integration/reconcile stage.
- **"Domain 4 is the smallest domain on the exam"** is untagged but follows directly from the tagged weights (44/28/16/12). No action needed.
- **Unused corpus that would close some findings cheaply:** `csi-spec-objective-2026-08-25`, `k8s-docs-cri-2026-08-24`, `k8s-docs-network-plugins-2026-08-24`, `k8s-docs-custom-resources-2026-08-23`, `k8s-docs-operator-pattern-2026-08-23`, and `metrics-server-install-2026-08-31` are all present and unreferenced by this draft. The last of these directly supports §4's *"metrics-server registers itself through the aggregation layer"* (*"kube-apiserver must enable an aggregation layer"*), which is currently carried by cross-bearing alone.

---

## PASS — Verified claims (sampled, by section)

**§1 — the definition.** All four paragraphs of the block quote match `cncf-cloud-native-definition-2026-08-23` word for word, including the characteristics clause reproduced in the Fixed Point ("secure, resilient, manageable, sustainable, and observable"), the seven-item technology list, "this list is non-exhaustive", and the payoff clause. CNCF mission line verbatim from the charter. 227 projects / 715 members / 329K+ contributors all match `cncf-who-we-are-2026-08-23` ("329K+", "715 CNCF members").

**§2 — maturity and governance.** All three rung descriptions verbatim from `cncf-project-maturity-levels-2026-08-23`. Archived correctly placed as a terminal state outside the ladder, double-sourced. Process detail verified item by item against `cncf-toc-project-lifecycle-process-2026-08-31`: application issue on the TOC repo; "5-7 adopters willing to be interviewed"; ~1-week internal TOC comment period; "The public comment period is open for two weeks"; "2/3 supermajority vote of the TOC". Incubation/Incubating terminology note matches the snapshot's own observation. Board and TOC quotations verbatim from charter and TOC README. All five current TAG names and scope strings verbatim from `cncf-tags-current-structure-2026-08-31`; pre-2025 eight-TAG list matches `cncf-toc-and-tags-2026-08-23`; May 2025 restructuring date matches the blog URL and text. End User TAB charter quote verbatim. Landscape quotations and all six category groups with their sub-categories match `cncf-landscape-and-community-2026-08-23` exactly. Six named Graduated projects (containerd, CoreDNS, etcd, Helm, Prometheus, Argo) all present on the snapshot roster, as is Kubernetes.

**§3 — microservices, coupling, immutability.** Every quoted fragment verbatim from `cncf-glossary-microservices-monoliths-coupling-2026-08-31`, including the monolith counter-argument. Immutable-infrastructure definition verbatim from `cncf-glossary-immutable-infrastructure-2026-08-31`; the enforcement mechanism is correctly rendered as prose rather than quotation, matching the snapshot's "[Paraphrase, NOT verbatim]" marking. The two-immutabilities Snag observes the B7 canonical-form ruling (full two-word phrase, back-bearing to Ch 2 §2).

**§4 — extension points.** The six-row documentation table reproduces `k8s-docs-extending-kubernetes-2026-08-23` faithfully, and "five plugin types crammed into the sixth" is a correct count of row 6. Aggregation-layer and device-plugin quotations verbatim from `k8s-docs-api-aggregation-and-device-plugins-2026-08-31`, including the load-bearing "The aggregation layer is different from Custom Resource Definitions" sentence. The book's four-interface grouping is explicitly declared as the book's own judgment rather than a published list — correct handling.

**§5 — service mesh.** CNCF glossary paragraphs 1–3 and the "without requiring code changes" Fixed Point verbatim; the eBPF/sidecarless paragraph correctly **not** imported, per the snapshot's scope note. Istio's three reasons, the data-plane/control-plane definitions, the security goals, the identity model, the four-step mTLS handshake, and permissive mode all verbatim from `istio-service-mesh-2026-08-23` and `istio-security-mtls-identity-2026-08-31`. Envoy's self-description and the "unaware of the network topology" passage verbatim. Ambient-mode block verified line by line against `istio-ambient-mode-2026-08-31`: per-node L4 + optional per-namespace L7; ztunnel; "secure overlay"; waypoint as "a deployment of the Envoy proxy; the same engine that Istio uses for its sidecar data plane mode"; coexistence. VirtualService correctly kept out of prose per the scope guardrail. Istio and Linkerd both confirmed on the Graduated roster.

**§6 — serverless.** All four serverless properties and both problem statements verbatim from `cncf-glossary-serverless-2026-08-31`; "abstracts servers away from the user" correctly emphasised as *abstracts*, not *eliminates*. Knative Serving / Eventing / Functions descriptions verbatim from `knative-overview-2026-08-23`, as are "builds on the Kubernetes Pod abstraction", the CRD implementation, and Graduated status. KPA, scale-to-zero, and the HPA-instead-of-KPA option verbatim from `knative-serving-autoscaling-2026-08-31`.

**§7 — autoscaling.** Horizontal/vertical distinction, HPA-as-resource-and-controller, the 15-second intermittent loop, and the DaemonSet exclusion all verbatim from `k8s-docs-hpa-2026-08-24`. VPA add-on status double-sourced (concepts page + VPA page), metrics-server prerequisite, and the recommender/updater/admission-webhook trio all match `k8s-docs-autoscaling-and-vpa-2026-08-31`. Node-autoscaling definition, provisioning trigger, consolidation, cloud-provider interaction, node groups, and the SIG Autoscaling sponsorship verbatim from `k8s-docs-node-autoscaling-2026-08-31`; Karpenter's self-description and job summary verbatim from `karpenter-concepts-2026-08-31`, with **no** CNCF maturity level assigned — correct, and matching that snapshot's explicit instruction. KEDA and the Cron scaler verbatim. Cluster Proportional Autoscaler matches `k8s-docs-autoscaling-2026-08-23`. **The in-place-resize treatment is the best-handled item in the chapter:** the v1.35 GA / v1.27 alpha / v1.33 beta history, the "As of Kubernetes 1.37, VPA does not support resizing pods in-place" sentence, and the contradicting `InPlaceOrRecreate` beta claim are all quoted accurately, the disagreement is stated as a disagreement, and the AUTHOR-REVIEW comment records it — exactly what the snapshot's ⚠ SOURCE CONFLICT note asks for.

**§8 — governance, releases, joining.** Four community principles, SIG/WG/Committee definitions, the three SIG orientations, the chair requirement, and subprojects all verbatim from `k8s-community-governance-2026-08-23`. "Most community activity is organized into Special Interest Groups (SIGs) and time bounded Working Groups" verbatim; the three Committees (Code of Conduct, Security Response, Steering) match the roster, and the figure's "~24" SIGs is an accurate count of the 24 listed. TAG/SIG shared-origin quotation verbatim from the CNCF blog, framed as causal history rather than as a frequency claim — inside the Ethical Guardrail #8 boundary. Release cadence, three maintained branches, ~1 year of patch support, the three phases, and the week-4/week-12/week-14 markers all verbatim from `k8s-release-cycle-and-cadence-2026-08-31`; the AUTHOR-REVIEW comment correctly quarantines the superseded 15-week figure. SIG Release charter quotations verbatim. KEP material verbatim from `k8s-keps-and-feature-stages-2026-08-23`. The full contributor ladder — all four rungs, Member's 2FA/sponsorship/mailing-list/issue requirements, Reviewer's 3 months / 5 PRs / 20 PRs, Approver's 3 months / 10 / 30 / nomination — matches `k8s-community-membership-ladder-2026-08-23` exactly, including "2 reviewers (from different companies)". LFX Mentorship, GSoC, and Outreachy descriptors verbatim from `cncf-mentoring-and-community-groups-2026-08-31`. Code of Conduct scope, pledge, and "a response within three business days" verbatim from `cncf-code-of-conduct-2026-08-31`, reported without editorialising per that snapshot's register guardrail. KCNA pre-professional framing and the CKA/CKAD/CKS format descriptions verbatim from `cncf-kcna-certification-page-2026-08-23`.

**Practice questions.** All 21 answer keys were checked against their cited snapshots; every quoted fragment in the explanations verifies (Q1, Q3, Q5, Q6, Q7, Q8, Q9, Q11, Q12, Q15, Q16, Q17, Q18, Q19, Q20, Q21 all confirmed verbatim). The exceptions are the three untagged explanation clauses recorded above as F8, F9 and F10.

**Notably absent, correctly:** the draft nowhere repeats the "60 questions" figure, and nowhere asserts a passing score, exam duration, cost, or validity period — all of which `provenance-kcna-60-questions-2026-08-23` and `cncf-kcna-certification-page-2026-08-23` mark as unsourced or not stated. That restraint is the single cleanest result in this audit, and F2 is the one place where the same discipline slipped.
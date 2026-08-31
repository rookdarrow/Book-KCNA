# Fact-Accuracy Audit — Chapter 19

**Mode detected: STANDARD.** The `Cached sources` section is populated (31 snapshots) and the draft carries ~70 inline `[source:` tags. Untagged factual assertions about the exam, the certifying body, or third-party project behaviour are therefore FAIL, not advisory.

**Note on line numbers.** The input was supplied as `draft-v1.md` inlined into the prompt without line numbering. Every line reference below is an *estimate* derived from position in the document; each finding is additionally anchored by section heading and a verbatim excerpt so the revision stage can locate it by text search.

## Summary

- Total factual claims inspected: **124**
- Tagged claims verified: **63**
- Tagged claims unverifiable (tag points to a snapshot that does not contain the claim, or to a snapshot outside this corpus): **5**
- **Untagged factual claims (FAIL): 16**
- **Contradicted claims (FAIL): 3**
- Minor discrepancies (WARN): **17**

The chapter's *sourced* work is strong: nearly every quotation is verbatim-accurate against its snapshot, the phrasing-discipline rules attached to the 60-question and 75% figures are followed correctly in §3, and the draft correctly declines to assert whether check-in consumes exam time. The failures cluster in three places: (1) §3's exam-interface mechanics, which the corpus explicitly records as undocumented, four separate times; (2) §4's retired-blueprint claims, which rest on a snapshot marked *do not cite*; (3) Practice Question 1, whose designated correct answer cannot produce the symptom its own stem describes.

---

## FAIL — Contradicted claims

### Line ~885 and ~968 (Practice Question 1, and its answer): "A frontend Pod in the same namespace cannot reach a backend Pod… **B. The CNI plugin does not implement NetworkPolicy.**"

**Tag:** untagged item; the answer explanation invokes the chapter's own sourced thread-3 formulation.
**The contradiction:** The designated correct answer cannot produce the stem's symptom, and the chapter's own statement of NetworkPolicy semantics is what proves it.

The stem describes a policy that *selects* `tier=backend` and *allows* ingress from `tier=frontend`, with no other policy anywhere. Work both enforcement states:

- **Policy enforced:** backend is selected, so its ingress is default-deny *except* the allow rule — which permits exactly the frontend traffic described. Traffic flows.
- **Policy not enforced** (answer B's scenario): nothing is restricted at all. Traffic flows.

Under both branches the frontend reaches the backend. The absent-component pattern for NetworkPolicy manifests as **traffic that should have been blocked getting through**, never as an allowed flow being denied. The answer text even states this against itself — "The NetworkPolicy object is valid and accepted by the API server; nothing enforces it" — which is a description of *unrestricted* connectivity.

None of A, B, C or D explains the stated symptom. The item is unanswerable as written.

**Recommended fix:** Invert the stem so the symptom matches the pattern. E.g.: *"…selecting Pods labeled `tier=backend` and allowing ingress only from Pods labeled `tier=frontend`. A Pod labeled `tier=batch` in the same namespace can still reach the backend Pods. No other NetworkPolicy exists anywhere."* Answer B then becomes correct and the distractor analysis for A, C and D survives unchanged.

### Line ~1045 (Practice Q10 answer, option D rebuttal) and line ~498 (§2 D4 table): "as of the sources cached here 'VPA does not support resizing pods in-place, but this integration is being worked on'"

**Tag:** `[source: k8s-docs-autoscaling-and-vpa-2026-08-31]`
**Snapshot says:** The quotation is verbatim from Source A. But the same snapshot carries an explicit banner:

> "⚠ SOURCE CONFLICT — see manifest Notes 1. Sources A, B and C are all kubernetes.io and do not agree on whether VPA supports in-place resize. Trap #105 must be written to the conflict, not through it."

Source B lists VPA update modes including `InPlaceOrRecreate` and `InPlace`. Source C (the v1.35 GA blog) states: *"Vertical Pod Autoscaler (VPA)'s `InPlaceOrRecreate` update mode, which leverages this feature, has graduated to beta."*

**Draft says:** presents Source A's sentence as the settled position, with no acknowledgement that two other kubernetes.io pages point the other way.
**Recommended fix:** Write to the conflict as the snapshot instructs. One sentence suffices in the Q10 rebuttal: note that the autoscaling concept page states VPA does not yet support in-place resize while the VPA page lists `InPlaceOrRecreate` among its update modes and the v1.35 release blog calls that mode beta — so **D is wrong** because VPA is not removed, not because the in-place question is closed. Also restore the source's own version anchor ("As of Kubernetes 1.37") rather than the vaguer "as of the sources cached here."

### Line ~1030 (Practice Q9 answer): "the TOC facilitates 'defining and maintaining the technical vision', **approving new projects within the scope the Board sets**"

**Tag:** `[source: cncf-charter-governance-bodies-2026-08-31]`
**Snapshot says:** the tagged file's verbatim section contains four quotations — the mission, the Board's remit, the TOC's technical-vision remit, and the End User TAB's remit. **It does not state that the TOC approves projects.** That claim appears only inside the file's *DRAFTING NOTE*, which is marked "not from source" and which attributes the wording to a different file: "the scope framing comes from the TOC README ('approving new projects within the scope of the CNCF set by the Governing Board')."

That file — `cncf-toc-and-tags-2026-08-23.md` — **is not among the 31 snapshots supplied to this stage.**

**Draft says:** builds Practice Q9's entire correct answer ("The TOC approves projects; the Governing Board decides the budget") on the project-approval half.
**Recommended fix:** Either re-tag the project-approval clause to `cncf-toc-and-tags-2026-08-23` and confirm that snapshot is in the corpus, or rewrite Q9 so the discriminator rests only on what the charter snapshot verifiably states — technical vision versus marketing/business/budget — which is sufficient to rule out all three distractors. The §2 D4 row already does exactly this and is clean; Q9 should match it.

---

## FAIL — Untagged factual claims

### Line ~625–650 (§3, "The first pass" / "The second pass"): the flag-and-return exam mechanic

> "**Can get it.** … If it does not, pick the more likely one, flag it, move." / "**The second pass.** Your flagged questions, in the order you flagged them." / "Always leave an answer even when you flag." / "**Change an answer only when you can say why.**"

**Why it's a factual claim:** It asserts that the KCNA exam interface supports flagging questions, returning to them, reviewing in flag order, and changing a submitted answer. These are properties of the exam delivery platform, not study advice.

**The problem is not merely absence of a tag — the corpus affirmatively records the absence, four times.** Every Linux Foundation snapshot that could carry it says so explicitly:

- `lf-mc-exam-important-instructions-2026-08-31`: "**Question navigation — NOT PRESENT ON PAGE.** No statement about skipping, flagging, marking for review, returning to previous questions, changing an answer, a review screen, or how the exam is submitted. Confirmed absent on targeted fetch 2026-08-31."
- `lf-mc-exam-faq-2026-08-31`: "Question navigation — NOT PRESENT ON PAGE."
- `lf-exam-rules-and-policies-2026-08-31`: "Question navigation — NOT PRESENT ON PAGE."
- `lf-handbook2-taking-the-exam-2026-08-31`: "Question navigation — NOT PRESENT ON PAGE."

The ★ Fixed Point at line ~605, the fig03 pacing diagram at line ~655, the Chapter Summary "Pacing" row (~1068), and §5's "Exam-day pacing" block all depend on this mechanic.

**Fix:** This needs an author decision, not a wording tweak. Either (a) open a research gap for a Linux Foundation or PSI BRIDGE source documenting multiple-choice exam navigation — if one exists, this is the single highest-value missing snapshot for the chapter; or (b) rewrite §3 so the two-pass rule degrades gracefully: keep "budget 60% for a first pass," but frame the reserve as *time held back for the questions you found hardest* and add one honest sentence that the Linux Foundation does not document its multiple-choice interface, so the reader should establish on the tutorial screen whether flagging is available. Option (b) is strictly more useful to the reader than an unhedged instruction that may not be executable.

### Line ~620 (§3, "Don't know it"): "Answer anyway. There is no penalty for a wrong answer that leaving it blank would avoid."

**Why it's a factual claim:** an assertion about the exam's scoring rule (no negative marking).
**The corpus records the opposite of support:** `lf-mc-exam-faq-2026-08-23` — "**Scoring methodology — NOT PUBLISHED.** No mention of scaled scoring, cut scores, or psychometric standard setting." The 08-31 full re-fetch of the same page adds only that exams "are scored automatically" and results arrive within 24 hours. Nothing addresses wrong-answer penalties.
**Fix:** Open a research gap for a Linux Foundation statement on scoring. Absent one, rewrite as a reasoning step the reader can verify for themselves rather than a fact: an unanswered question scores zero with certainty, so leaving an answer cannot score worse unless a penalty exists — and the Linux Foundation does not publish one either way.

### Line ~648 (§3): "changing an answer for an articulable reason improves your score, and changing it on a feeling does not"

**Why it's a factual claim:** an empirical claim about test-taking outcomes, offered explicitly to overturn "the folk wisdom about never changing answers, which is wrong."
**Fix:** Either cite the research (answer-change studies are a real literature and a citable snapshot could be cached), or demote to the chapter's own reasoning: *"A reason you can state is evidence; a feeling at minute seventy is usually fatigue."* The current phrasing asserts a measured effect the book cannot support.

### Line ~700 (§4) and line ~868 (Exam Alert): "It also has the best ratio of exam presence to study time in the entire book."

**Why it's a factual claim:** asserts relative exam presence of a competency — i.e. knowledge of the item distribution — which no published source provides. The Exam Alert repeats it as "Highest ratio of exam presence to study time in the book."
**Fix:** The defensible version is arithmetic and already available: Community and Collaboration is one of three competencies under a 12% domain, and its material is finite and bounded (governance bodies, SIG/WG/Committee, maturity levels), so an hour there covers a larger share of its surface than an hour spent on Domain 1 depth. Say that instead. Note the same paragraph's "reliably under-studied … The reasons are consistent" is an unsourced claim about candidate populations — recast as an observation about the material's character, not about what readers do.

### Line ~715 (§4, 🪝 Snag): "A five-domain list is the tell. If you see 'Cloud Native Observability' as a standalone domain with its own weight, that material predates the change."

**Why it's a factual claim:** states the retired blueprint's domain *count* and the retired domain's *name*.
**The only source in the corpus for either is one marked do-not-cite.** `provenance-kcna-60-questions-2026-08-23` lists "Cloud Native Observability 8%" among five domains, and is headed: "**DO NOT CITE THE CONTENTS OF THIS FILE AS FACT.**" The authoritative file, `cncf-curriculum-repo-kcna-versions-2026-08-23`, records the retired curriculum as an **OPEN GAP**: "The retired domain weights are NOT recorded in this snapshot… **DO NOT draft the retired weights from memory or from third-party study guides.**"

What *is* sourced: `lf-kcna-program-changes-2026-08-23` states observability "will be rolled under Cloud Native Architecture," which supports the inference that observability was previously not under Cloud Native Architecture. It does not support "five domains" or the name "Cloud Native Observability."
**Fix:** Retrieve `old-versions/KCNA_Curriculum old.pdf` (raw URL is in the versions snapshot) and cache the retired domain list, which closes the open gap for the whole book. Until then, rewrite the tell using only what is sourced: *"If your material lists observability as a domain in its own right rather than as a competency under Cloud Native Architecture, it predates the change."*

### Line ~710 (§4): "third-party study material purchased before that date is mis-allocated by roughly a full domain's worth of weight"

**Why it's a factual claim:** quantifies the magnitude of the blueprint drift, which requires the retired weights — the open gap above.
**Fix:** Drop the quantification until the retired PDF is cached. "Mis-allocated" alone, with the sourced observability move as the concrete instance, carries the point without the unsupported number.

### Line ~845 (§6, Logbook Entry): "It is one question out of sixty"

**Why it's a factual claim:** states the KCNA question count flatly, as a property of the reader's exam.
**This violates the phrasing discipline the correction snapshot mandates.** `provenance-kcna-60-questions-2026-08-31` and `lf-mc-exam-important-instructions-2026-08-31` both require the class-level hedge: "CORRECT: 'The Linux Foundation publishes a 60-question format for its multiple-choice exams, of which the KCNA is one.'" §3 gets this exactly right at line ~610; the Logbook drops it 235 lines later.
**Fix:** "It is one question out of sixty" → "It is one question out of the sixty the handbook describes" — or simply "one question out of the whole paper," which loses nothing rhetorically.

### Line ~447 (§2 D2 table) and line ~570 (Q4 answer): "Ingress is frozen; Gateway API is where new work happens" / "**frozen means no new features; deprecated means an end date**"

**Why it's a factual claim:** asserts the maintenance status of a Kubernetes API, and the answer to a full checkpoint question is built on it ("An option saying Ingress is deprecated or removed is wrong").
**No snapshot in the corpus addresses Ingress or Gateway API status.**
**Fix:** Open a research gap for the Kubernetes Ingress concept page and/or the Gateway API documentation. This is load-bearing — it is one of only two checkpoint questions in §2 and it is unverifiable as the corpus stands.

### Line ~535 (⚠ Navigational Hazards): "A second default IngressClass does not give you more coverage. Two defaults is an ambiguous configuration, not a redundant one."

**Why it's a factual claim:** asserts specific admission behaviour when multiple IngressClasses carry the default annotation. This is one of the four hazards the chapter singles out as "worth more attention than the rest of this section combined," and it is the only one of the four with no source.
**Fix:** Cache the Kubernetes Ingress documentation section on default IngressClass. The precise behaviour matters here — "ambiguous" is doing work that should be a documented rule.

### Line ~412 (§2 D1) and line ~538 (Hazards): "`Running` as a phase means 'scheduled, at least one container created'"

**Why it's a factual claim:** defines an API-level Pod phase. It is also **imprecise**: the Kubernetes definition of the `Running` phase is that the Pod is bound to a node, **all** containers have been created, and at least one is running or starting/restarting. "At least one container created" understates the condition — a Pod with one of three containers created is not `Running`.
**Fix:** Cache the Pod lifecycle concept page and tighten to "bound to a node, all containers created, at least one running or starting." The chapter's actual teaching point — that `Running` is a lifecycle position and not a health verdict — is unaffected and gets sharper.

### Line ~424 (§2 D1): "`restartPolicy: Never` does not stop a Deployment from creating a replacement Pod"

**Why it's a factual claim:** describes a specific configuration's behaviour — and the configuration described cannot exist. A Deployment's Pod template must have `restartPolicy: Always`; the API rejects other values, so a reader who tries the example will get a validation error rather than the illustrated behaviour.
**Fix:** Keep the rule (restartPolicy governs containers within a Pod, not the Pod object) and change the illustration to one that is constructible — a bare Pod, or a Job, where `Never` is legal and the container-versus-Pod distinction still lands.

### Line ~700 (§4, Dead Reckoning): "Kubernetes Fundamentals is Chapters 2–8. Container Orchestration is Chapters 9–13. Cloud Native Application Delivery is Chapters 14–16. Cloud Native Architecture is Chapters 17–18."

**Why it's a factual claim:** it sits inside a Dead Reckoning block, under a `[source: cncf-curriculum-kcna-readme-2026-08-31]` tag whose scope is the *weights*. The chapter-to-domain mapping is this book's editorial decision, not something CNCF publishes, and the layout invites the reader to take both halves as equally sourced.
**Fix:** Split the block, or add a clause: "The weights are CNCF's; the chapter mapping is this book's."

### Line ~493 (§2 D4): "**maturity-level ordering** — Sandbox → Incubating → Graduated. Entry, growing, proven."

**Why it's a factual claim:** states the CNCF project maturity ladder. The corpus contains the phrase "CNCF graduated project" (Knative, KEDA) but no snapshot defining the levels or their order. §5 and the Exam Alert both direct the reader to drill this material.
**Fix:** Cache the CNCF graduation criteria / project stages page. Cheap to close and the chapter leans on it in three places.

### Line ~182 (Thread 2 table), line ~455 (§2 D2), line ~285 (Thread 9), line ~450 (§2 D2 view/edit/admin): the RBAC claim cluster

Specifically: the four-way binding matrix including the "**Not valid** — a namespaced Role cannot be granted cluster-wide" cell; "RBAC is purely additive; nothing subtracts; RBAC has no deny and no conflict resolution"; "`view` reads (but not Secrets), `edit` writes workloads, `admin` adds the ability to manage RBAC within a namespace."

**Why they're factual claims:** normative statements about Kubernetes RBAC semantics and the contents of the default ClusterRoles. Three of these are named as ★-adjacent high-priority items in the Exam Alert, and Practice Q4's correct answer is derived from the additive rule.
**No RBAC snapshot exists in this corpus.** The claims are, to the best of ordinary knowledge, correct — which is exactly why they will pass unnoticed into print unsourced.
**Fix:** Cache `kubernetes.io/docs/reference/access-authn-authz/rbac/`. One snapshot covers the matrix, the additive semantics, and the default ClusterRole descriptions, and it retires this entire cluster plus the §1 thread-2 derivation.

### Line ~440 (§2 D2): "**NetworkPolicy needs both ends** — for traffic A→B to flow when both are restricted, A needs egress permitting B **and** B needs ingress permitting A" / line ~438 "Ask: *is this Pod selected by any policy?* No policy selects it → fully open."

**Why they're factual claims:** normative NetworkPolicy semantics, used as the discriminator for two table rows and as the basis of Practice Q1's option-A rebuttal.
**Fix:** Cache `kubernetes.io/docs/concepts/services-networking/network-policies/`. This snapshot would also let Practice Q1 be rebuilt correctly (see the Contradicted section) and would source the isolation-versus-non-isolation rule the whole §1 thread 9 rests on.

### Line ~415 (§2 D1) and Practice Q8: routine Kubernetes claims with no cached source

A group of individually low-risk assertions, listed together because one research pass closes all of them:

- probe semantics — "Liveness failing **restarts**… Readiness failing **removes it from Service endpoints**… Startup **suspends the other two**" (~413), and Q8's answer (~1015)
- "Secret is base64-*encoded*, not encrypted" (~417)
- Deployment/StatefulSet, DaemonSet, Job/CronJob discriminators (~419–422)
- OCI versus CRI scope (~423)
- "eviction order under node pressure is determined by QoS class" (Q8 answer, ~1018)
- "`kubectl top` needs metrics-server installed" (Q2 answer, ~980)
- headless / broken / selectorless Service (~437)
- Helm `charts/` directory versus chart repository (~463); "`templates/` contains Go templates, not rendered manifests" (Q5 answer, ~1000)
- Argo CD `OutOfSync` "reports a difference… That is a status, not a failure" (~470)
- "A span is a single unit of work" (~500) — the *trace* half of this row is sourced to the OpenTelemetry signals snapshot; the span definition is not, and that snapshot does not define span

**Fix:** One research pass covering the Pod lifecycle/probes page, the ConfigMap-Secret page, the Helm chart-structure docs, and the OpenTelemetry traces page retires the list. None of these is likely to be *wrong*; all of them are unverifiable as the corpus stands.

---

## WARN — Minor discrepancies

**1. Attention Budget total does not match its own table (line ~8).** Header says "Total time: ~95 minutes"; the ten rows sum to **122 minutes** (10+25+8+30+6+8+10+5+5+15). Either the header or the row times need adjusting.

**2. §1 heading says twenty chapters; the section traces seventeen (line ~120).** "Nine Threads Through Twenty Chapters" — the figure spans Ch 2–18 and every thread path terminates at Ch 18 or earlier. Body prose consistently says "eighteen chapters," which is correct for Ch 1–18. Suggest "Through Eighteen Chapters."

**3. The fig01 thread map disagrees with the prose paths, and two rows are a column short (lines ~130–152).** Specific mismatches:
- Thread 1: prose includes **Ch 4 §1** ("supplies the artifact the loop reads"); the row has no mark at Ch 4.
- Thread 3: the row marks **Ch 6** and **Ch 16**, neither of which appears in the prose path; the prose ends at **Ch 18** ("applies it to the whole observability stack") but the row's last mark is Ch 17.
- Row 5 (label join) and row 9 (additive/allow) contain **16 columns against the header's 17**, so every mark after the gap lands one chapter early — row 9's marks read as Ch 9 and Ch 11 where the prose says Ch 10 and Ch 12.
Since this ASCII block is the placeholder for `ch19-fig01-cross-domain-integration-map`, the corrected matrix should be settled here before the figure spec is cut, or the rendered diagram will inherit the errors.

**4. "Thirteen words" versus fourteen table rows (line ~505).** The homonym table has 14 rows. Additionally the **`plugin`** row has an empty Sense B column (it is a single-sense caution, not a homonym pair), and the **`volume`** row's Sense B ("A Docker volume") carries no chapter reference where every other cell does. Fixing `plugin` — either giving it a real second sense or moving it out of the table — makes the count thirteen and the row shapes uniform.

**5. Source typo reproduced inside a quotation (line ~495 and Q10 answer ~1040).** The VPA quotation carries the source's own error: "but is **a a**n add-on that you or a cluster administrator may need to deploy." Faithful, but it will read as a typesetting mistake. Add `[sic]` or paraphrase outside quotation marks; the sourced substance (VPA is an add-on, not shipped) survives either way.

**6. Istio waypoint quotation compressed into a false predication (line ~485).** Draft: "the waypoint proxy is 'the same engine that Istio uses for its sidecar data plane mode'." Snapshot: "The waypoint proxy **is a deployment of the Envoy proxy;** the same engine that Istio uses for its sidecar data plane mode." As compressed, the sentence says the proxy *is* an engine. Restore "is a deployment of the Envoy proxy — the same engine…"; it also names Envoy, which the row currently never does.

**7. Steering-committee governance claim tagged to the roster file (line ~490).** "Steering holds overall project governance while chartering the other two `[source: k8s-sig-list-and-groups-2026-08-31]`." That snapshot supplies the roster (three Committees: Code of Conduct, Security Response, Steering) — correctly cited. But "holds overall project governance" and "formed by the steering committee" are in `k8s-community-governance-2026-08-23`; in the roster file they appear only in a DRAFTING NOTE marked "not from source." Add the second tag.

**8–11. §6 details tagged to the wrong Linux Foundation handbook page.** Four paraphrases carry `[source: lf-handbook2-candidate-requirements-2026-08-31]` but originate elsewhere in the corpus:
- "a webcam **you can move to pan the room**" (~800) — candidate-requirements lists "Webcam" bare; the movability requirement is in `lf-mc-exam-faq-2026-08-31` ("Ensure the webcam is capable of being moved as you will have to pan your surroundings").
- "no papers or writing implements on the desk **and none below it**" (~815) — the below-the-surface clause is in `lf-mc-exam-faq-2026-08-31` ("No objects such as paper, trash bins, or other objects below the testing surface").
- "**décor is fine**, notes are not" (~815) — "Paintings and other wall décor is acceptable" is in `lf-mc-exam-faq-2026-08-31`.
- "**Public spaces are prohibited outright**" (~816) — sits after the candidate-requirements tag; the enumeration ("coffee shops, stores, open office environments") is in `lf-mc-exam-faq-2026-08-31` and `lf-mc-exam-important-instructions-2026-08-31`. Candidate-requirements says only "Space must be private where there is no excessive noise."
All four facts are cached and correct; only the attributions need moving.

**12. Second attribution in §3 untagged (line ~595).** "That number is published, on the KCNA exam page and in the candidate handbook." The handbook half is tagged; the exam-page half is supported by `lf-kcna-exam-page-2026-08-23` (Duration: "90 minutes") but carries no tag.

**13. `helm rollback` scope claim exceeds the CLI reference (line ~465, and Q5 answer ~995).** Draft: "re-applies that revision of the **whole release**" / "re-applies that revision of **everything the chart manages**." The snapshot supports the arguments ("the name of a release," "a revision (version) number") and the operation ("roll back a release to a previous revision"), but says nothing about the release's object membership. The distinction is what makes Q5's rebuttal of option A work. Cache the Helm release/revision concept page, or soften to what the CLI reference states.

**14. Speculative causal explanation presented as likely fact (line ~805).** "which usually means a managed endpoint blocking the secure browser at exactly the wrong moment." The Linux Foundation says only that work-provided devices "can result in technical challenges." "Usually means" attributes a specific mechanism and frequency the source does not give.

**15. Memory-science claims stated as fact (lines ~830, ~838, ~848).** "Institutional vocabulary learned in a state of anxiety… does not survive retrieval under pressure"; "retrieval is harder. It is *supposed* to feel harder, and the difficulty is what makes the memory durable"; "Sleep is a direct intervention on that failure mode." These describe real findings (testing effect, desirable difficulties) but are asserted without attribution in a book that otherwise sources its claims. Either cite, or frame as the narrator's counsel rather than as established mechanism.

**16. Population claims in the Logbook Entry (line ~843).** "Around day four, you will have a bad session… This is close to universal." Presented as a fact about candidates. The paragraph works equally well as observed experience ("this is common enough to be worth naming in advance").

**17. Item-construction claims (lines ~294, ~985, ~975, ~537, ~445).** "Any option offering a deny verb is **constructed to catch** a reader who assumed these behave like a firewall"; "Every distractor is off by exactly one on a different axis, **which is how these are usually built**"; "**the single most common instrument error**"; "**the most common Domain 1 discrimination failure**"; "the English is genuinely misleading **and the exam knows it**"; "**it costs points every year**." Each asserts knowledge of exam item construction or of aggregate candidate performance. Note that `cncf-tags-current-structure-2026-08-31` flags precisely this hazard for the TAG/SIG pair — "the sentence must not drift into 'which is why it's such a common exam trap'" — and the TAG/SIG row itself stays clean; these six do not. All are convertible to claims about the *material* ("the English is genuinely misleading, which is why `ReadWriteOncePod` exists to name the other case") at no rhetorical cost.

**18. `the-lodestar.md` described as shipping when it does not exist (line ~727).** "`the-lodestar.md` ships with this book at the repository root." The draft's own AUTHOR-REVIEW comment records that the file is not in the Book-KCNA repository and that the six block names in §5 are provisional. Logged here so it is not lost between stages: this is the chapter's one self-declared blocking gap, and the six block descriptions in §5 (~735–760) become factual claims about a shipped artifact the moment the file exists. They must be reconciled against it.

---

## PASS — Verified claims

Sampled tagged claims whose content matches the referenced snapshot. Quotation accuracy across the chapter is high; the following were checked word-for-word.

**Exam format and policy**
- 90 minutes for LF multiple-choice exams — matches `lf-mc-exam-faq-2026-08-31` verbatim (Soundings A1, §3 opening).
- "The system does not offer a way to pause the exam timer or to add time back to the exam during connection loss events" — verbatim, `lf-handbook2-taking-the-exam-2026-08-31`.
- "Candidate is not allowed to write or enter input on anything (whether paper, electronic device, etc.) outside of the Exam console screen" — verbatim, `lf-exam-rules-and-policies-2026-08-31`.
- The 60-question figure, §3 (~610): "The Linux Foundation publishes a 60-question format for its multiple-choice exams, in the candidate handbook, for that class of exam." **Matches the mandated CORRECT phrasing in `lf-mc-exam-important-instructions-2026-08-31` exactly**, including the class-level hedge and the refusal to attribute it to the KCNA exam page.
- ⚓ Worth Securing (~612): the where-a-fact-lives framing matches `provenance-kcna-60-questions-2026-08-31`, including its "not on the KCNA product page" distinction.
- Closed-book rule — "Candidates are NOT PERMITTED to access tools, resources or external sites…" verbatim; and the CKA/CKAD documentation-browsing contrast is correctly scoped to the performance-based exams (`lf-certification-resources-allowed-2026-08-31`).
- Check-in window (30 minutes before / no later than 30 after), the ≤15-minute specialist wait, ID upload and selfie, and the exact-name-match requirement — all verbatim-supported by `lf-handbook2-taking-the-exam-2026-08-31`.
- "You cannot take an exam using a virtual machine" — verbatim, `lf-mc-exam-important-instructions-2026-08-31`. Work-provided devices "can result in technical challenges" — verbatim, `lf-mc-exam-faq-2026-08-31`. "If the room has a door, it must be closed" — verbatim, `lf-handbook2-candidate-requirements-2026-08-31`.
- **Verified by restraint:** the chapter nowhere asserts whether check-in time counts against the 90 minutes, which `lf-handbook2-taking-the-exam-2026-08-31` explicitly instructs ("DO NOT ASSERT EITHER WAY"). §6's "Check in early" advice stays clear of it.

**Blueprint**
- 44 / 28 / 16 / 12 across four domains — `cncf-curriculum-kcna-readme-2026-08-31`, and the draft's note that the weights agree with the LF exam page and the curriculum PDF matches the snapshot's own cross-check.
- Community and Collaboration as one of Cloud Native Architecture's three competencies — `cncf-kcna-curriculum-pdf-2026-08-23` (Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration).
- "no earlier than November 24, 2025"; observability "rolled under Cloud Native Architecture"; "Any KCNA exam taken after the updated release will test on the new set of Domains and Competencies"; "The only date that matters is the date you sit for the exam" — all verbatim, `lf-kcna-program-changes-2026-08-23`.

**Kubernetes**
- Version skew, all four citations: kubelet up to three minor versions older and never newer; kubectl within one minor either direction; release branches for the most recent three minor releases — `k8s-version-skew-policy-2026-08-31`. **Practice Q3 verified against the snapshot's own worked examples**: apiserver 1.37 → kubelet supported at 1.37/1.36/1.35/1.34 (answer C's 1.34 is exactly three back) and kubectl supported at 1.38/1.37/1.36 (C's 1.38 is one newer). All three distractors fail correctly and for the stated reasons.
- `ReadWriteOnce` = single node, multiple Pods on that node permitted; `ReadWriteOncePod` = one Pod cluster-wide — `k8s-docs-persistent-volumes-depth-2026-08-25`.
- `Recycle` deprecated; `Retain` default for manually created PVs, `Delete` for dynamically provisioned — the second via `k8s-api-ref-persistentvolume-v1-2026-08-25`, which is the correct file for stating both defaults in one place.
- `storageClassName: ""` as explicit opt-out versus omission engaging DefaultStorageClass behaviour — `k8s-docs-persistent-volumes-depth-2026-08-25`.
- Practice Q6's quotations ("still exists and the volume is considered 'released'"; "is not yet available for another claim because the previous claimant's data remains on the volume") are drawn from the snapshot's **Reclaiming → Retain** section, not from the Phase bullets — which means they fall outside that snapshot's RETRIEVAL NOTE caveat against quoting the Phase bullets unverified. Correctly sourced.
- VPA is an add-on requiring separate deployment plus Metrics Server; VPA updates "a workload management resource (such as a Deployment or StatefulSet)"; cluster scaling "normally means adding or removing nodes"; node autoscaling triggered by Pods that "can't be scheduled on existing Nodes" — `k8s-docs-autoscaling-and-vpa-2026-08-31` and `k8s-docs-node-autoscaling-2026-08-31`.

**Cloud native ecosystem**
- Ambient mode "a per-node Layer 4 (L4) proxy, and optionally a per-namespace Layer 7 (L7) proxy" — verbatim, `istio-ambient-mode-2026-08-31`.
- Knative Serving and Eventing definitions — verbatim, `knative-overview-2026-08-23`.
- Governing Board "responsible for marketing and other business oversight and budget decisions"; TOC "defining and maintaining the technical vision"; End User TAB "the voice of End Users in the CNCF community" — all verbatim, `cncf-charter-governance-bodies-2026-08-31`. The §2 D4 row is clean (see the Contradicted section for the separate Q9 issue).
- TAGs as "the primary organizational units within the CNCF that oversee and coordinate interests across projects"; "bridges between CNCF projects, end users, and the Technical Oversight Committee"; the TOC "approved the creation of SIGs, later to be renamed Technical Advisory Groups" — verbatim, `cncf-tags-current-structure-2026-08-31`. The shared-origin framing is a causal explanation rather than a frequency claim, which is the distinction that snapshot's drafting note asks for.
- "time bounded" Working Groups; the three-Committee roster — `k8s-sig-list-and-groups-2026-08-31`. Closed committee membership — `k8s-community-governance-2026-08-23`.
- SLI / SLO / SLA definitions and the consequence test — all four quotations verbatim, `sre-book-service-level-objectives-2026-08-31`.
- Pushgateway "an intermediary service which allows you to push metrics from jobs which cannot be scraped" and "The only valid use case for the Pushgateway is for capturing the outcome of a service-level batch job" — verbatim, `prometheus-pushgateway-practices-2026-08-31`. The row's distractor guidance (long-running service; job tied to one machine) tracks the snapshot's drafting note.
- Traces among OpenTelemetry's signals alongside metrics, logs and baggage — `opentelemetry-signals-2026-08-23`.
- `helm rollback` argument structure (release name, revision number) — `helm-rollback-cli-2026-08-31`.

**Arithmetic**
- 0.6 × 90 = 54; 90 − 54 = 36; 60 questions ÷ 90 minutes = 90 seconds each; 54 minutes ÷ 60 = 54 seconds each. All correct.
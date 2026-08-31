# Integration Check — KCNA Chapter 15

## Summary

- Terminology consistency: **pass** (2 low-severity notes; 1 orphan that needs a gloss)
- Callbacks to earlier chapters: **15 correct / 3 incorrect** (all three are mis-targeted section numbers on otherwise-true claims)
- Cross-bearings vs. section skeleton (mechanical): **31 pointers / 31 resolve** — pass
- Inbound published pointers into Ch 15: **10 with explicit §, 10 honored** — pass
- Retrieval-practice accuracy: **pass** (4 tagged items, 4 verified aligned)
- Glossary coverage: **41 concepts introduced, 38 defined in the chapter, 7 require glossary entries, 9 require new ledger rows**
- Contradictions with earlier canon: **none** (1 surface-form conflict where shipped Ch 14 is the outlier, not this draft)
- Ethical guardrails (skill Part 14): **pass with one fix** — one untagged quantitative claim, resolvable from an existing snapshot

**Verification basis.** No knowledge-base shards were tagged for this stage, but Chapters 1–14 are all shipped in `../Book-KCNA/`. Every callback below was checked against shipped text with line citations rather than inferred from the contracts. Cross-bearings were checked mechanically against the section skeleton *and* against the shipped target's actual content — the three defects below pass the mechanical check and fail the content check, which is why they survived to this gate.

---

## Headline finding: two AUTHOR-REVIEW blockers are already resolvable

The revision stage removed two claims for want of a source and left AUTHOR-REVIEW comments asking whether the sources exist. They do. Both removals can be reverted at zero research cost, and one of them currently leaves a shipped inbound pointer landing on an incomplete thought.

### A. The 8%→16% weight — the snapshot exists and Chapter 1 already cites it

The comment at the top of "Why This Chapter Matters" states that "No cached snapshot carries any earlier revision of the KCNA curriculum." That is checking the wrong snapshot. The prior weights are not in the CNCF curriculum PDF; they are in the Linux Foundation program-changes page, which is cached:

> `sources/lf-kcna-program-changes-2026-08-23.md`

And shipped Chapter 1 already carries the exact claim, tagged:

> **Cloud Native Application Delivery doubled**, from 8% to 16% [source: lf-kcna-program-changes-2026-08-23].
> — `chapter-01-taking-departure.md:274`

**This is also an ethical-guardrail item, not just a completeness one.** The draft still says "this domain **doubled** in the 2025-11-24 blueprint revision" with no source tag. "Doubled" asserts the prior weight was 8% just as surely as writing "8%" does — the figure was removed, the claim was not. Under the fact-accuracy rule in `style-decisions.md` ("Untagged factual claims are an audit failure"), the sentence as it stands is worse than the version that was cut, because it makes the same claim with the tag stripped off.

**Fix:** restore the figure and mirror Chapter 1's tag — "this domain doubled, from 8% to 16%, in the 2025-11-24 blueprint revision [source: lf-kcna-program-changes-2026-08-23]" — and delete the AUTHOR-REVIEW comment.

### B. The §5 RBAC ordering example — the snapshot exists, and Chapter 12 shipped the claim correctly

The §5 comment asks whether `kubernetes.io/.../rbac/` can be cached for the "you cannot change the Role or ClusterRole that it refers to" passage, and says to verify against shipped Ch 12 §3 first. Both checks come back clean:

> "After you create a binding, you cannot change the Role or ClusterRole that it refers to."
> — `sources/k8s-docs-rbac-2026-08-23.md:17`

> **And a binding cannot be retargeted.** *"After you create a binding, you cannot change the Role or ClusterRole that it refers to"* [source: k8s-docs-rbac-2026-08-23]. If a RoleBinding points at the wrong role, you delete it and create a new one. That is a different operation with different consequences: a window during which the subject holds nothing, and, under a system that reconciles a cluster against a repository, a delete-and-create rather than an update. *[cross-bearing: see Ch 15 §5 — ordering the sync]*
> — `chapter-12-locks-keys-and-watchstanders.md:866`

The AUTHOR-REVIEW's diagnosis was right on the substance — the old draft named `subjects` when the immutable field is the role reference — and shipped Ch 12 words it correctly. So the corrected example can be restored exactly as the comment specifies.

**This one is more than a missed opportunity.** Chapter 12 emits a forward pointer *into* §5 on the strength of this example. As the draft stands, a reader following that pointer arrives at "Chapter 12 pointed here for a specific reason, and it is a good illustration of why ordering is not a theoretical concern" — followed by no illustration, then "Take the general shape instead." The reciprocal pair is broken at the receiving end.

**Fix:** restore one sentence at that point — a binding's role reference is immutable, so changing which role a binding grants is a delete-and-recreate, which is a real ordering constraint for a system reconciling a whole repository against a whole cluster — citing `k8s-docs-rbac-2026-08-23`.

*(The third removal — the twelve-factor 2011/provenance details — is left alone. That is fact-accuracy's domain and it was handled correctly there.)*

---

## Terminology consistency

| Term | Canonical form | Occurrences | Drift? |
|---|---|---|---|
| Argo CD | `Argo CD` (two words) | 47 | No — 0 instances of `ArgoCD`/`Argo-CD` |
| Flux | `Flux` | 31 | No — 0 instances of `FluxCD` |
| cloud native | unhyphenated | 3 | No — 0 hyphenated. Cleaner than shipped Ch 1–8 (⚑8) |
| Kubernetes / `K8s` | spell out; `K8s` only in quotes | 1 × `K8s` | No — the single instance is inside a quotation from `argocd-security-cluster-credentials-2026-08-31`, which the ledger permits |
| twelve-factor app | hyphenated, spelled out | 6 | No |
| rollback by revert | three words, unhyphenated | 9 | No — draft is correct; see canon note below |
| revision (Helm sense) | "Helm revision" / "release revision", never bare | 3 | No |
| Pod / Deployment / ServiceAccount / ConfigMap / Secret / StatefulSet | exact CamelCase | — | No |
| kubectl, etcd, containerd | always lowercase | — | No |
| Taking Your Bearings | never "Bearings" alone | 3 headings | No |
| Heading form `## <difficulty> §N — Title` | Ch 5–8 majority form | 7 sections | No — matches shipped Ch 14 |
| Zenith marked `☀️` | skeleton recommendation #4 | §7 | No — matches shipped Ch 14 §7 |

### Note 1 — SIGTERM/SIGKILL vs Ch 5's TERM/KILL (low severity)

§1's Factor IX says "the SIGTERM-then-SIGKILL sequence." Shipped Ch 5 §4 writes the same signals as "a TERM signal" and "they get KILL" (`chapter-05-the-smallest-vessel.md:559`). The draft's form matches its own source (`twelve-factor-ix-disposability-2026-08-31` says "SIGTERM"), so this is defensible, and neither form is in the ledger. Recorded only so a later sweep does not "correct" one toward the other by accident.

### Note 2 — "revision" in the Argo CD sense is used bare before it is disambiguated (low severity)

§4's "What it tracks" subsection uses bare *revision* five times in a third sense (a Git revision / Argo CD's `revision` field) — "An `Application` names a revision…", "updating the tracking revision". The Snag that disambiguates it ("A Git revision is a **commit**") sits two subsections later, under "Rollback, for the third time." The ledger's canonical-forms table covers only the Deployment and Helm senses, so this third sense has no rule and the draft invents one inline — correctly, but late.

**Fix:** move the disambiguating clause forward to first use in "What it tracks," and add a canonical-forms row for the Argo CD/Git sense.

### Orphan requiring action — **Argo Rollouts is never introduced**

This is the chapter's most consequential terminology gap, because it sits underneath graded material.

§2 draws its definitions of Recreate, RollingUpdate, blue/green, canary, and progressive delivery from `argo-rollouts-*` snapshots, and attributes them in prose as "Argo's description" (line 278), "Argo's comparison" (line 288), "Argo's documentation" (line 328), and once as "**Argo Rollouts** states the same idea" (line 284) — with no introduction of what Argo Rollouts is. Two sections later, §4 introduces "**Argo CD**" as though for the first time.

A reader who has met "Argo" five times in §2 will read §4's Argo CD as the same product. It is not: Argo Rollouts is a separate controller, and Argo CD does not include it. There is no ledger row for Argo Rollouts and no glossary entry.

**The fix closes two other holes at the same time.** §2's Fixed Point asserts that blue/green and canary "require tooling above the Deployment object" — and then never names any such tooling. Meanwhile shipped Ch 6 promises the reader precisely that: *"blue/green, canary, and A/B, and **the tooling that implements them**"* (`chapter-06-fleets-not-vessels.md:665`). Naming Argo Rollouts at line 278 discharges the Ch 6 promise, gives the Fixed Point a concrete referent, and prevents the Argo CD conflation, in one clause:

> Argo Rollouts — a separate controller in the Argo project from the Argo CD of §4, and one concrete example of the tooling this section says these patterns require.

---

## Callback correctness

**15 of 18 substantive callbacks verified correct against shipped text.** Confirmed, with line citations:

| Draft claim | Shipped source | Verdict |
|---|---|---|
| "Chapter 4 promised it about configuration" | `ch04:722` — "the third of the twelve factors… *[cross-bearing: see Ch 15 — the twelve factors, and which ones Kubernetes hands you for free]*" | ✓ |
| "Chapter 5 taught you `terminationGracePeriodSeconds` and the SIGTERM-then-SIGKILL sequence, and told you the word was coming" | `ch05:559` — teaches preStop → TERM → 30s → KILL, and promises "*disposability*" | ✓ exact |
| "Chapter 6 taught you… `RollingUpdate` and `Recreate`, `maxSurge` and `maxUnavailable`, pause and resume" | Ch 6 §4 | ✓ |
| "Chapter 6 called these 'release strategies'" (§2 Closer Look) | `ch06:665` — "a whole vocabulary of *release strategies*" | ✓ exact |
| "Chapter 6 named the second group and deferred them" | `ch06:665` names blue/green, canary, A/B and defers | ✓ |
| "Chapter 6 promised you this… the word would appear twice more" | `ch06:714` — "twice more in this book attached to entirely different mechanisms" | ✓ (see imprecision note) |
| "Chapter 14 spent the first… This is the second and last" | `ch14:671` — "This is the first of those two. The second is Chapter 15's rollback-by-revert" | ✓ reciprocal |
| "Chapter 6 told you that anyone can write a controller acting on custom resources" | Ch 6 §8 (969–1041) | ✓ |
| "Chapter 3 made a claim… the API server is the only thing that mutates cluster state" | Ch 3 §5 "The Only Door In" (610–676) | ✓ |
| §7 "The coordination is still watching, not telling… the same architecture, with a different thing in the hub position" | `ch03:653` — verbatim echo of Ch 3's own phrasing | ✓ excellent |
| "Chapter 14 opened by listing what a folder of YAML fails to give you, and one of the four was apply ordering" | `ch14:387+` — "It stops working in four specific places"; "### Failure two: apply ordering" | ✓ exact |
| "Chapter 12 pointed here for a specific reason" (§5) | `ch12:866` → `Ch 15 §5 — ordering the sync` | ✓ pointer exists |
| "Chapter 13 taught you to diagnose a cluster that will not run your Pod. It ended by handing something back" | Ch 13 §8 per skeleton | ✓ |
| "this domain doubled in the 2025-11-24 blueprint revision" | `ch01:274`, sourced | ✓ true, but untagged here — see Headline A |
| Ch 6 ordinal-count convention respected | Draft asserts no running ordinal for the control loop; Ch 6's sanctioned "third time is the one that matters" (`ch06:1465`) is left unspent | ✓ complies with the ledger's book-level convention |

### Three mis-targeted cross-bearings

All three attach a **true** claim to a section that does not contain it. Each passes the mechanical skeleton check — the target section exists with that title — which is why only a content check catches them.

**1. §4 — Argo CD's first appearance is in Ch 3 §5, not §6**

> "You have met the name once already, in Chapter 3, where it appeared as a promise about a sentence this chapter would retrieve *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*."

Argo CD is named exactly once in Chapter 3, at line 653, inside **§5 — The Only Door In** (610–676). Chapter 3 §6 (750–836) contains no mention of Argo. A reader following this pointer will not find the promise.

**Fix:** retarget to `*[cross-bearing: see Ch 3 §5 — the only door in]*`. The three §6 references immediately following it ("the thing Chapter 3 §6 defined") are correct and should stay.

**2. "Why This Chapter Matters" — the CNCF disclosure is in Ch 14's opening, not §1**

> "Chapter 14 made this statement at length… the published curriculum gives two competency names under this domain and no list of topics beneath either *[cross-bearing: see Ch 14 §1 — why a folder of YAML stops working]*."

Chapter 14 does make the statement at length — at `ch14:360–362`, inside **"Why This Chapter Matters"**. Chapter 14 §1 begins at line 387 and is entirely about the four failures of a manifest directory. A reader following this pointer lands on "Failure one: environment variation."

**Fix:** "Why This Chapter Matters" is unnumbered, so there is no §N to retarget to. Point at the chapter by name: `*[cross-bearing: see Ch 14 — Why This Chapter Matters]*`, or drop the bracketed pointer and name the section in prose.

*(No contradiction here: Ch 14 says CNCF publishes one competency name, "Application Delivery"; Ch 15 says two, adding "Debugging." Ch 14 is narrower because it covers only the packaging competency. Both are consistent with `cncf-kcna-curriculum-pdf-2026-08-23`.)*

**3. §7 — the "ten seconds" line is in Ch 6 §9, not §8**

> "…it is why Chapter 6 said what it said when it finished teaching the control loop: that when you met this, it would look like a new idea for about ten seconds *[cross-bearing: see Ch 6 §8 — the control loop, extended]*."

The line is real and verbatim — "When you meet that, it will look like a new idea for about ten seconds" (`ch06:1147`) — but line 1147 sits in **§9 — Nobody Sails One Pod** (1101–1153). Chapter 6 §8 ends at line 1041.

This one matters more than the other two because it is the closing sentence of the book's primary Zenith, where a reader is most likely to flip back and check.

**Fix:** retarget to `*[cross-bearing: see Ch 6 §9 — nobody sails one pod]*`.

### One callback imprecision (low severity)

§4 says Chapter 6 "said the word would appear twice more, and that **the second occasion would be a delivery tool**." Chapter 6 says "twice more" (`ch06:714`) and points at Ch 14 (`ch06:720`) and at Ch 15 (`ch06:721` — "and a third thing, again wearing it"). It does not characterize the third instance as a delivery tool. Suggest: "…said the word would appear twice more, and pointed at Chapter 14 and at this chapter."

---

## Retrieval-practice accuracy

| Tag | Question | Topic | Owning section | Verdict |
|---|---|---|---|---|
| `[retrieval: ch4]` | TYB1 Q3 | ConfigMap/Secret delivering environment-specific values | Ch 4 §4 | ✓ aligned |
| `[retrieval: ch6]` | TYB1 Q4 | `maxSurge`/`maxUnavailable` arithmetic | Ch 6 §4 | ✓ aligned |
| `[retrieval: ch12]` | TYB2 Q4 | ServiceAccount + ClusterRole/ClusterRoleBinding | Ch 12 §2–§3 | ✓ aligned |
| `[retrieval: ch3]` | TYB3 Q5 | what a controller compares, and how often | Ch 3 §6 | ✓ aligned |
| `[cross-domain: D2.2]` | Q16 | RBAC scope for a delivery agent | Ch 12 §3 | ✓ |
| `[cross-domain: D1.1]` | Q17 | `spec`/`status` mapped to target/live state | Ch 4 §2 | ✓ |

Spacing meets the skill's Part 10 target: TYB1 2/6 (33%), TYB2 1/5 (20%), TYB3 1/5 (20%).

**Worth noting as a design strength:** TYB3 Q5 is the retrieval item the chapter's payoff depends on, and it is correctly built — it forbids the words "Git, repositories, or delivery," and its answer key routes a reader who missed it back to Ch 3 §6 *before* §7 rather than after. The Soundings does the same thing for question 1. That is the right structure for a chapter whose Zenith is a recognition rather than a fact.

---

## Glossary coverage

41 concepts introduced. 38 are defined in-chapter and need no glossary entry under rule 4. The exceptions:

| Concept | Defined in-chapter? | Needs glossary entry? | Needs a ledger row? |
|---|---|---|---|
| **Argo Rollouts** | **no** — named once, never introduced | **yes** | **yes** — no owner anywhere in the ledger |
| **progressive delivery** | yes (§2, sourced) | **yes** — graded directly in Q7 and in TYB1 Q5's key | **yes** — no ledger row |
| **repository server** (Argo CD) | yes (§4 Snag) | **yes** — Q14's answer key requires naming it | yes |
| **sync operation status** | yes (§4) | **yes** — graded in Q13 and TYB2 Q2 | yes |
| **prune / pruning** | yes (§4) | no | **yes** — graded in TYB2 Q4 and Q16 |
| **Jsonnet** | no — named in a quoted list | **yes** — appears in Q14's answer key and the Common Traps table | no |
| **impersonation / Kubernetes Impersonation API** | named (§6, sourced) | **yes** | yes |
| **soft multi-tenancy** | no — appears only inside a quotation | **yes**, or drop the phrase | no |
| target state / live state / sync status / sync / refresh | yes (§4, from Argo's glossary) | no | yes — 5 rows |
| application source type / tool / config-management plugin | yes (§4, quoted) | no | yes |
| bootstrap (Flux) | yes (§6, sourced) | no | yes |
| blast radius | yes (§3), correctly marked as the book's own term | no | already rowed ✓ |
| `Git commit SHA` | used bare throughout §4 | optional — arguably ambient alongside "Git · repository · branch · tag · commit" | no |

**Nine new ledger rows are needed for Ch 15 §2–§6.** None of them conflicts with an existing owner; they are terms the B7 ledger simply did not anticipate, which is expected for a chapter whose sources are two vendor documentation sets.

### Two ledger rows the draft does not honor as written

**A/B testing.** The ledger assigns "A/B testing (as a release strategy)" to Ch 15 §2, the skeleton lists "rolling, Recreate, blue/green, canary, **A/B**" as §2's content, the acronym register points "A/B" at §2 — and shipped Ch 6 promises the reader "blue/green, canary, **and A/B**" (`ch06:665`).

The draft names it, sources it, and bounds it correctly under a subsection headed **"One term this book will not teach you."** The reasoning is sound: `argo-rollouts-experiments-2026-08-31` does present A/B as a use of the `Experiment` resource rather than a rollout strategy, and product experimentation genuinely is a different question from release mechanics.

So the substance is defensible; the framing collides with three contracts and one shipped promise. A reader arrives from Ch 6 expecting A/B and meets a heading announcing it will not be taught.

**Recommended fix (cheapest of the three):** retitle the subsection to something like "One term that belongs somewhere else" and open it by discharging the Ch 6 promise explicitly — "Chapter 6 promised you A/B alongside the other two. Here it is, and here is why it is not a fourth member of that list." Then amend the ledger row to read "named and bounded, not taught as a release strategy," so the register's pointer is honest. No content change required.

**Drift.** The ledger assigns "Drift · drift detection" to Ch 15 §4. The draft defines drift in **§3**, via OpenGitOps' glossary, and §4 does detection. This is the better arrangement — drift is what principle 4 exists to catch, so it belongs where the principles are — but the ledger should be amended to `§3 (definition) / §4 (detection)` rather than the draft moved.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims** — with one exception, resolved above: "this domain doubled" is currently untagged. Restore the tag from `lf-kcna-program-changes-2026-08-23`. Everything else quantitative in the chapter carries a source tag, including the two figures most at risk of being asserted from memory (Argo CD's 120s + 60s jitter sync interval; Flux's five-minute default).
- [x] **Fear-based content uses real examples** — the §3 Logbook Entry is explicitly framed as a composite ("There is a version of this story on every platform team"), makes no claim to a specific incident, and is generous to the engineer in it ("it is genuinely the right call in the moment"). This satisfies the subject-dignity guardrail: the wry register is aimed at the practitioners, never at anyone harmed.
- [x] **Simplification acknowledged** — Dead Reckoning present in "Why This Chapter Matters." §5 opens by conceding it "goes somewhat deeper than an associate credential is likely to reach" and closes by telling the reader not to memorize the annotation. §6 walks back Flux's "five minutes by default" against the API reference rather than leaving the tidier claim standing.
- [x] **Authority claims cite legitimate sources** — CNCF glossary, OpenGitOps, Kubernetes docs, Argo and Flux project documentation, 12factor.net. No vendor marketing.
- [x] **"Frequently tested" claims verifiable** — **exemplary here.** The chapter states its own rule up front ("nothing here is described as 'frequently tested' or 'commonly appears'… What you will see instead is 'easy to confuse'") and keeps it: 0 instances of "frequently tested" or "commonly appears," and the Common Traps preamble reads "these are distinctions that are easy to confuse." This inherits Ch 14's discipline (`ch14:362`) correctly.
- [x] **No strawmanning of alternative methods** — push-based CD is called "a perfectly good delivery system" and "a perfectly reasonable thing to build," twice. Recreate is "the correct choice rather than the lazy one."
- [x] **Inference marked as inference** — the chapter goes further than required. The §3 push/pull security argument carries an explicit "A note on what follows" paragraph declaring which consequences are sourced and which are the book's reading, and TYB2 Q3's and Q10's answer keys repeat the disclosure inside the graded text. The multi-cluster comparison in §6 does the same. This is the right handling of a chapter whose central argument is authored rather than published.

---

## Recommended fixes

Ordered by cost-to-benefit. Items 1–5 are cheap and unambiguous; 6 and 7 are author decisions.

**1. Restore the 8%→16% figure with Chapter 1's tag.** Clears the one guardrail failure. Delete the AUTHOR-REVIEW comment. *(Headline A)*

**2. Restore the §5 RBAC ordering example, correctly worded, citing `k8s-docs-rbac-2026-08-23`.** Repairs the receiving end of Ch 12's inbound pointer. Delete the AUTHOR-REVIEW comment. *(Headline B)*

**3. Retarget three cross-bearings:**
- §4 Argo CD promise: `Ch 3 §6` → `Ch 3 §5 — the only door in`
- Why This Chapter Matters: `Ch 14 §1` → `Ch 14 — Why This Chapter Matters` (chapter-level; the target is unnumbered)
- §7 "ten seconds": `Ch 6 §8` → `Ch 6 §9 — nobody sails one pod`

**4. Introduce Argo Rollouts in one clause at §2's first shorthand use (line 278).** Prevents the Argo CD conflation, gives §2's Fixed Point a concrete referent, and discharges Ch 6's "and the tooling that implements them."

**5. Move the "a Git revision is a **commit**" clause forward** to first bare use in §4's "What it tracks."

**6. Epigraph — confirmed verbatim reuse, and the repetition is larger than the comment suggests.** The AUTHOR-REVIEW asks whether to keep the callback. Verification confirms it: Ch 14's closing quote is character-identical, one chapter back. But the epigraph is not the only repetition — Ch 15's opening paragraph also restates Ch 14's closing paragraph nearly word-for-word:

> Ch 14: "Somebody with cluster credentials on their laptop, running a command, from a machine nobody audits, at a moment nobody records. They apply the version they believe is current. Afterward, nothing keeps watch."
> Ch 15: "Somebody with cluster credentials on a laptop, running a command from a machine nobody audits, at a moment nobody records. They apply the version they believe is current. Afterward, nothing keeps watch."

Together that is roughly 60 words of Chapter 14's final page reproduced on Chapter 15's first. Under skill Part 7 this is *channel* redundancy — same information, same channel, immediately adjacent — which is the kind the skill classifies as negative, and it lands at exactly the point in a chapter where arousal must be established.

**Recommendation: keep one, change the other.** The prose recap is doing real work (it sets up the two-halves structure that organizes the whole chapter), so the cheaper cut is the epigraph — substitute a practitioner quote about intent versus outcome, as the comment's second option proposes. Keeping the epigraph and paraphrasing the recap also works. Keeping both is the one option to avoid.

**7. The Zenith figure pair — escalating, not re-reporting.** The image-specs stage caught the chassis mismatch, and the draft's AUTHOR-REVIEW carries it. Verification adds one thing the earlier stages did not have: **three shipped chapters stake the book's payoff on this figure landing.**

> "you have seen the control loop twice now, at two altitudes, and recognized it the second time… **the third time is the one that matters.**" — `ch06:1465`
> "Chapter 15 makes the larger argument, and **it is the structural claim this whole book is building toward.** Don't get ahead of it." — `ch09:1249`
> "the recognition when that lands is **the one this book has been saving.**" — `ch14` Voyage Ahead

The skeleton is explicit that §7 "owns no new material — the payoff is recognition, and **it fails if the figure does not visually rhyme with Ch 3 §6's**." The caption asks the reader to lay the two side by side and see that one box changed; as drawn, `ch03-fig02-control-loop-desired-vs-current` has four boxes and no controller or API-server node, so the claim is not checkable by a reader who actually flips back. Of the three resolutions image-specs lists, **redrawing `ch03-fig02` onto this chapter's chassis** is the only one that preserves what three chapters have promised. It costs a Chapter 3 edit; that is a cheap price for the book's designated primary Zenith. This is the single highest-risk open item in the chapter.

---

## Not flagged (checked and clean)

Recorded so a later stage does not re-open them:

- **The `ch15-zenith-…` figure anchor is not a defect.** Image-specs flags it as violating the `chNN-figMM-slug` rule. Shipped Chapter 14 uses `ch14-zenith-package-not-template` — the identical pattern. So either both are defects and Ch 14 needs a retrofit, or the structural contract's Rule 4 should be amended to permit `chNN-zenith-slug` for the Zenith figure. **Recommend amending the rule**; the convention is established, legible, and already in a shipped chapter. This is a book-level consistency call, not a Chapter 15 fix.
- **`rollback-by-revert` hyphenation.** The ledger mandates the unhyphenated three-word form and this draft complies throughout. Shipped `ch14:671` writes `rollback-by-revert` hyphenated and is the outlier. Cosmetic sweep item for Chapter 14, author's call — no change to this chapter.
- **All 31 cross-bearing pointers resolve** against the section skeleton. The three defects above are content mismatches at valid targets, not invalid section numbers.
- **All 10 inbound published pointers into Ch 15 are honored** at their exact section numbers: Ch 5 §4 identity → §4; Ch 9 §7 → §7; Ch 12 §4/§6 → §4; Ch 12 §5 ordering → §5; Ch 14 ×3 → §3; Ch 14 ×2 → §4. The four pins the skeleton warned about (Argo CD forced into §4, pushing the OpenGitOps principles up into §3) are all satisfied.
- **No Ch 1 §N pointers emitted** — the draft addresses Chapter 1 by name only, correctly, per skeleton Collision #1.
- **No running ordinal asserted for the control loop.** The draft complies with the book-level convention ratified at the Ch 8 gate, and leaves Ch 6's sanctioned "third time" unspent for §7 to collect.
- **Figure caption/anchor ordinal mismatch (fig04 ↔ 15.5, fig05 ↔ 15.4)** was already caught by image-specs FLAG F-2 and by fact-accuracy item 13, with the fix recommendation recorded. No new action here.
- **Question budget:** Soundings 8 (content chapter) ✓; Taking Your Bearings 16 across 3 checkpoints, each ≥5 ✓; Practice 21. Chapter total 45.
I have what I need: the draft (1401 lines), the outline's ratified `question_budget` and per-block Practice plan, and — decisively — the shipped house form across chapters 1–9.

Emitting `diagnostics/question-quality.md`:

---

# Question-Quality Audit — Chapter 10

Audited against `draft-v1.md` (`draft-voice.md` does not exist at this stage). All line numbers cite `draft-v1.md`. Budget targets read from `outline.md` frontmatter lines 126–130; per-block Practice plan from `outline.md` § 7. House-form comparison drawn from the nine shipped `chapter-*.md` files at the book repo root.

## Summary

- Chapter type: **content**
- Total questions inspected: **40**
  - 🧭 Soundings questions: **8** (stems L50–L64; answers L69–L83)
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints — #1 L464, #2 L733, #3 L1038)
  - Practice questions: **17** (L1211–L1243; answer key L1249–L1349)
- Question budget compliance: **met** on all four frontmatter targets. Per-block Practice distribution has drifted: §3 over by 1, §5 short by 1, §6 short by 1.
- Weak distractors (WARN): **not assessable — 0 of 40 questions present distractors.**
- Trap answers that don't target real misconceptions (WARN): **not assessable — 0 trap answers exist.**
- Missing or incomplete why-wrong explanations (FAIL): **17** — the entire Practice set, structurally. See the lead finding. Under the open-response substitute standard, a further **7** keys carry no misconception treatment at all (WARN): B1.2, B1.5, B2.4, B2.5, P7, P12, P17.
- Retrieval-practice spacing: **short by one item.** 6 of 32 (18.75%) against the outline's ratified 7-item / 21.9% allocation and skill Part 10's 20–25% band for chapters 6+. ≥4-back floor met with margin.
- Soundings spoiler check: **clean at the stem level — 8 of 8 stems disclose nothing.** Three answer keys (S4, S5, S7) carry near-miss disclosures and one (S3) discloses a prerequisite half. **No FAIL.**

**The consequential finding is not any individual question. It is that Chapter 10 has no multiple-choice questions at all**, and every one of the nine shipped chapters does. The audit template's distractor apparatus, the outline's seven explicit "must appear as a distractor" mandates, and skill Part 11's entire self-correction design are all inapplicable to this draft — not because they were considered and rejected, but because the option layer was dropped while the answer keys that were written *for* it remained. Five answer keys discuss "options" and "distractors" that do not exist on the page. See the lead finding below.

---

## Lead finding — the Practice set has no options, and the answer keys know it

**Severity: FAIL (rule 3, and the outline's § 7 trap-answer requirement).**

### The evidence

| Chapter | `^[A-D]) ` option lines | Where they sit |
|---|---|---|
| chapter-01 | 24 | — |
| chapter-02 | 156 | Bearings **and** Practice |
| chapter-03 | 152 | Bearings **and** Practice |
| chapter-04 | 104 | — |
| chapter-05 | 92 | — |
| chapter-06 | 92 | — |
| chapter-07 | 72 | Practice only (18 × 4) |
| chapter-08 | 72 | Practice only (18 × 4, all after L1152) |
| chapter-09 | 84 | Practice only (21 × 4, all after L1265) |
| **ch-10 draft-v1** | **0** | **nowhere** |

The three most recent shipped chapters converge on a stable form: **Soundings and Bearings open-response; Practice Questions four-option multiple choice with per-option why-wrong explanations.** Chapter 10's Soundings and Bearings conform. Its Practice set does not.

### The answer keys were written against the missing layer

Five keys use option/distractor vocabulary for options that are not on the page:

| Line | Key text | Problem |
|---|---|---|
| L1263 (P3) | *"**Wrong option worth rejecting:** 'expose arbitrary TCP ports.'"* | No options offered. The reader never saw this and had no chance to reject it. |
| L1291 (P8) | *"**Distractor logic:** every wrong option in this family names something in the manifest — a bad `pathType`, a wrong Service port, a missing `host`."* | "In this family" is the tell: the key describes a distractor set that was designed and never written. |
| L1301 (P10) | *"**The two wrong options are the two one-half answers** … Offering only one of these in a question would teach the other, **which is why a well-built item offers both.**"* | The key explains the design principle of an item that does not exist. P10 offers neither wrong option. |
| L1333 (P15) | *"…more useful **as a distractor** than a generically wrong option…"* | Same. |
| L759 (B2.2) | *"**Distractor logic: this option is attractive** because 'no longer developed' *feels* like deprecation."* | "This option" has no referent. |

Four more quote a hypothetical wrong answer rather than an offered one — P1 L1253, P4 L1269, P5 L1275, P13 L1317 (*"Why 'X' is wrong…"*). Those read acceptably in open-response form; the five above do not.

### Why it matters pedagogically, not just formally

Skill Part 11's self-correction design is built on the reader *selecting* a trap answer and then being corrected:

> Reader gets it WRONG → detects "bit error" (misconception) → explanation corrects the error → reader re-encodes.

With no options, a reader who does not know the answer writes nothing, reads the key, and is corrected on a misconception **they were never induced to commit to**. The error-detection half of the loop is gone. This is most costly on exactly the items the outline built the chapter around: Soundings Q4 (L56) deliberately makes the reader *confidently wrong* about firewall defaults — and the outline says "the whole value is in the reader being confidently wrong for ninety seconds" — but no Practice item ever re-offers that wrong belief as a selectable option for them to fall into a second time and be caught.

### The outline's explicit mandates, all unmet

`outline.md` § 7 issues seven distractor requirements. None can be satisfied by an open-response set:

| Block | Mandate | Status |
|---|---|---|
| §2 | "**Trap #43 must appear as a distractor at least once.**" | **unmet** — trap #43 is named only inside P3's key (L1263) |
| §3 | "**Trap #42 must appear in two different question shapes.**" | **partially met** — P8 and B1.3 both test it, but as near-identical open items, not two shapes |
| §4 | "the two wrong options must be the **two different one-half answers**" | **unmet** — L1301 describes them; the question offers neither |
| §6 | "**Traps #48, #49 and #50 must each appear as a distractor at least once.**" | **unmet** — all three are treated in keys only |
| §6 | trap #48's wrong form ("no policy means no traffic") must appear | **unmet as an option**; named in B3.2's key (L1064) |
| §6 | trap #49's wrong form ("the more restrictive policy wins") must appear | **unmet as an option**; the closest thing is P15's key (L1333) |
| §7 | trap #47 as the silent-failure case | **met as an item** (P16), unmet as a distractor |

### Recommended fix

Convert the 17 Practice questions to four-option multiple choice, matching chapters 7–9. The distractors are already specified — the answer keys name them. Six items convert almost mechanically because the key already enumerates the wrong options:

- **P3** ← add "expose arbitrary TCP ports" as the fourth option (key L1263 supplies it).
- **P8** ← options: bad `pathType`, wrong Service port, missing `host`, **no Ingress controller installed** (key L1291 supplies all four).
- **P10** ← options: "deprecated and being removed", "unaffected and fully supported for new development", **both halves**, and one further one-half variant (key L1301 supplies the shape).
- **P13** ← add "outbound is now blocked" (key L1317).
- **P15** ← add "write a more restrictive policy selecting `payments` that excludes `app: legacy`" (key L1333).
- **P5** ← add "yes, `bb` is a prefix of `bbb`" (key L1275).

Leave Soundings and Bearings open-response — that matches chapters 7–9 and is working well here.

**If the open-response form was a deliberate departure**, it needs a `style-decisions.md` entry, and the nine shipped chapters need a consistency decision. Nothing in `outline.md` records such a departure; § 7 assumes multiple choice throughout.

---

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 15 | 15 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 (outline plans 3 × 5) | 3 (5 + 5 + 5) | **met** |
| Practice Questions | 17 | 17 | **met** |
| **Chapter total** | 40 | 40 | **met** |

Frontmatter compliance is clean. Difficulty signalling also conforms exactly to the outline's per-checkpoint plan (B1: ⚪⚪🔵🔵🔵; B2: ⚪⚪🟡🟡🟡; B3: 🔵🔵🟡🟡🔵), and the Part 10B struggle-label on B3.3 is present and correctly framed at L1046.

The problem is one level down.

### Practice distribution vs the outline's § 7 block plan

| Block | Planned | Actual | Questions | Status |
|---|---|---|---|---|
| §1 — ceiling and layer boundary | 2 | 2 | P1, P2 | met |
| §2 — the Ingress object | 3 | 3 | P3, P4, P5 | met |
| §3 — the controller | 3 | **4** | P6, P7, P8, P9 | **over by 1** |
| §4 — frozen | 2 | 2 | P10, P11 | met |
| §5 — Gateway API | 2 | **1** | P12 | **short by 1** |
| §6 — NetworkPolicy semantics | 4 | **3** | P13, P14, P15 | **short by 1** |
| §7 — the limits | 1 | 1 | P16 | met |
| (Zenith retrieval, § 7 places in §7 block) | 1 | 1 | P17 | met |

Three attached requirements are unmet:

1. **The §5 shortfall costs the cardinality item.** The outline specifies "one on the role/resource mapping, one on cardinality or request flow." P12 covers the mapping. **Neither Gateway cardinality nor the request flow appears in the Practice set.** Both are tested in Bearings #2 (B2.4 L743, B2.5 L745) — but Bearings is a mid-chapter checkpoint, not the end-of-chapter set a reader drills before an exam. The outline calls cardinality "the kind of cardinality detail multiple-choice exams reach for," and Exam Alert item 11 (L1181) promotes it to high-priority. It is the clearest case in the chapter of a fact promoted for the exam and then not drilled.

2. **The §6 shortfall is exactly the missing Ch 4 retrieval item.** See § Retrieval-practice spacing.

3. **Two of the four mandated interleaves are missing or weakened.** The outline requires "at least four questions must require two sections at once":

| Mandated interleave | Status |
|---|---|
| §2 + §4 — which API is recommended, and does that stop the other working | **present** — P11 (L1231) |
| §2 + §5 — express one requirement in both vocabularies | **present** — P12 (L1233) |
| §6 + §7 — a policy that looks correct, traffic that flows, **three** candidate explanations of which two are in this chapter and one is not | **weakened** — P16 (L1241) gives one explanation and asks about detection. B3.5 (L1050) asks for two. The three-candidate discrimination is written nowhere. |
| §3 + §7 + §8 — two objects, both correct, both inert; name what is missing in each **and the one difference in how you would find out** | **absent as an item.** P16's key does the work at L1339 (*"Note the contrast with question 8 … One breaks a website. The other breaks nothing you can see."*) — but the reader is told, not asked. |

The outline called the fourth of these "the only question in the set that tests the Zenith's operational value rather than its elegance." **Its content survives only as an aside in another question's answer key.** This is the same failure mode the Chapter 9 audit recorded ("The Zenith is untested") — second occurrence, so it is a pattern rather than an accident.

### Recall-vs-prediction calibration: on target

The outline warned this chapter's failure mode as a question set is *definition inflation* and budgeted "about five of the seventeen" for near-pure recall. Actual near-pure recall: **P1, P3, P6, P10, P17** (5), with P12 partly recall. The remaining eleven are prediction (P13, P14) or diagnosis (P2, P4, P5, P7, P8, P9, P11, P15, P16). **Calibration met.** §6 in particular got its two mandated prediction items (P13, P14), and P14's three-part structure is the best-constructed item in the chapter.

---

## Soundings spoiler check

Chapter ★ Fixed Points, against which each Soundings item is checked: **L148** (layer boundary), **L202** (HTTP/HTTPS only), **L288** (fanout vs virtual hosting), **L400** (Ingress controller required), **L549** (frozen ≠ deprecated), **L612** (Gateway resources + cardinality), **L874** (non-isolated by default), **L886** (additive, no deny), **L919** (both ends), **L979** (plugin dependency).

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| **1** (L50) | Virtual-hosting prior — what the server reads, and when it becomes available | **no** | Answer (L69) names the `Host` header and the post-connection timing, plus an SNI aside. Names no Kubernetes object. FP L288's new content — that Kubernetes has an *object* for this, that it splits on host *or* path, and that both put many Services behind one IP — is untouched. FP L202 (HTTP/HTTPS-only) is not reachable from a web-server prior. **Working as designed**; the payoff is deliberately deferred to B2.5 and §5 step 3. |
| **2** (L52) | Retrieval, Ch 9 §3 — LoadBalancer and what fifty cost | **no** | Answer (L71) is Chapter 9 material by construction. The *replacement* — one address, rules on it — is withheld. Clean. |
| **3** (L54) | Retrieval, Ch 9 §3 — which Service type routes by path | **partial — prerequisite half only** | Answer (L73): *"All four Service types operate on addresses and ports … nothing in Chapter 9 opens the request to look."* That is the first clause of FP L148 in substance. **Mitigation:** it is Chapter 9 §3's own published statement and therefore a prerequisite under skill Part 11 rule 2. The Fixed Point's chapter-new half — *"Everything in §2 through §5 reads **requests**. Which side of that boundary a mechanism sits on determines what it can know"* — is fully withheld. **Not counted as a finding.** |
| **4** (L56) | Firewall priors — default disposition and rule precedence | **no on the stem — WARN on the answer key** | The **stem is exemplary**: it names nothing Kubernetes, forces a commitment, and is phrased as a situation, exactly as the outline demanded. The **answer (L75) then telegraphs the reversal**: *"it is the instinct **§6 is going to take away from you.**"* That discloses *that* an inversion is coming — though not *what* it is. FP L874 and FP L886 remain unstated. **Cost:** the outline built this item so the reader would be "confidently wrong for ninety seconds"; the key ends the ninety seconds on the spot and hands §6 a reader who is already braced. **Fix:** cut the trailing clause after "sound instinct nearly everywhere." Nine words. |
| **5** (L58) | Deprecation prior — two announcements, two implications | **no — near-miss WARN** | Answer (L77) supplies the full *semantic* content of FP L549: *"**Deprecated** implies eventual removal … **No longer developed** says nothing about removal; it says the thing is finished. It may well be permanent."* What §4 still adds is real and substantial — the word **frozen**, that Ingress specifically is the second case, the GA stability guarantee, the Gateway recommendation, and the both-halves discipline. A strict reading of rule 7 could call this a FAIL; I do not, because the stem names no API and because the outline deliberately designed a *general* pre-test for a *specific* payoff. **Note the rubric already compensates**: the 6+ branch (L87) tells high scorers to *"Read §4 carefully anyway."* That is the right instinct and it should stay. |
| **6** (L60) | Retrieval, Ch 3 §4 — the absent-component rule | **no** | Answer (L79) states Chapter 3's rule and names its two Chapter 9 instances. Names neither Ingress nor a controller, so **FP L400 is intact**. A reader who answers this *can* predict FP L400 — and per the outline that is the intended design, since Ch 3 L601 made the rule a published prerequisite and pointed here. What the chapter teaches is not the rule but two new instances, one of which fails silently, plus the promotion at §8. **Working as designed.** |
| **7** (L62) | Retrieval, Ch 9 §1 — the segmentation hedge, and at what layer | **no — near-miss WARN, the strongest in the set** | Answer (L81): *"Since the **CNI plugin is what actually moves the packets, enforcement would have to live down there, at layer 3 or 4**."* That discloses the *locus* half of FP L979 and pre-states §6's scope sentence (L797). **Mitigation:** FP L979's teaching content is the *consequence* — the resource has **no effect** — and §7's is the silent-failure asymmetry. Neither is reachable from "enforcement lives in the plugin." §7 explicitly banks on the reader having got here (L1003: *"If you reasoned to something like this in Soundings question 7, you derived §7's central fact before the chapter told you"*) — though that sentence **overclaims**: the reader derived the dependency, not the no-effect consequence, and the wording should be softened to say so. **Fix:** drop *"at layer 3 or 4"* from L81. Chapter 9 taught that CNI moves packets; it did not teach the OSI framing of policy enforcement, so that clause has no prerequisite basis and is pure §6 content. |
| **8** (L64) | TLS-termination prior — where the connection ends, who holds the key | **no** | Answer (L83) is a generic reverse-proxy fact. TLS termination is not among the chapter's ten Fixed Points, and §2's Kubernetes-specific mechanism (L325 — a `kubernetes.io/tls` Secret with `tls.crt`/`tls.key`, single port 443, cleartext onward to Pods) is entirely withheld. Clean. |

**Pattern worth naming:** all four leaks sit in **answer keys inside the `<details>` block**, never in a stem. The pre-test itself is uncompromised — the reader commits before opening. What leaks is the *payoff*, which is spent slightly early. Three one-clause trims (S4, S5, S7) close all of it.

**Rubric check (rule 8): ✅ PASS.** Present and complete at L87–L91 — 6+ / 3–5 / 0–2 branches all present. The 0–2 branch carries the outline's mandated blunt Chapter 9 instruction verbatim (*"go back to Chapter 9 first. Not 'review' — go back"*), correctly naming questions 2, 3 and 7 as the diagnostic misses. This is the strongest rubric in the book so far and should be treated as the house exemplar.

**Answer disclosure (rule 9): ✅ PASS.** `<details>` opens L66, `<summary>` L67, closes L93. Answers are not visible before attempt.

---

## Per-question findings

Blocks below cover items with issues beyond the category-level finding. Items not listed are structurally sound as open-response questions.

### Q Practice 3 (L1215): "Which four capabilities may an Ingress be configured to provide?"

**Issue:** Pure list-recall with no options, and the key names a distractor the reader never saw. Trap #43's mandated §2 distractor is unmet here.

**Distractor analysis:** none offered. The key (L1263) names exactly one intended wrong option — *"expose arbitrary TCP ports"* — and calls it *"the fifth thing people assume is on the list and it is the one thing explicitly excluded."* That is a well-identified, genuinely common misconception. It is also invisible to the reader.

**Why-wrong explanation status:** **present and specific — but attached to nothing.**

**Recommended fix:** convert to four-option MC where the option set is five capabilities minus one, with "expose arbitrary TCP ports" occupying a slot. This is the single cheapest conversion in the chapter and it discharges the outline's trap-#43 mandate in one edit.

---

### Q Practice 10 (L1229): "State what the Kubernetes project has said about the Ingress API, in both of its halves…"

**Issue:** The key specifies a two-distractor design, explains why both must be offered together, and the question offers neither. **The most explicit gap between intent and delivery in the chapter.**

**Distractor analysis:** none offered. The key (L1301) reads: *"The two wrong options are the two one-half answers, and both must be rejected explicitly: 'deprecated and being removed' drops the stability half; 'unaffected and fully supported for new development' drops the no-development half. Offering only one of these in a question would teach the other, which is why a well-built item offers both."*

That is correct question-design reasoning about trap #44, and the outline endorses it (§ 7: "the two wrong options must be the two different one-half answers"). The reader receives the reasoning and never the item.

**Why-wrong explanation status:** **present and specific**, for absent options.

**Also:** P10 near-duplicates **B2.1** (L737). B2.1 asks for both halves; B2.1's own key (L753) already supplies the operational implications that P10 adds. Converting P10 to MC would differentiate them properly — B2.1 as open recall, P10 as forced discrimination between the two one-half answers.

**Recommended fix:** convert to four options: (A) deprecated and scheduled for removal; (B) GA, guaranteed, no removal plans, and actively developed; (C) **GA, guaranteed, no removal plans, and no longer developed** ✓; (D) no longer developed and therefore already deprecated. Option D is worth adding beyond the key's two, because it targets the reader who has both halves but has fused them.

---

### Q Practice 8 (L1225) / Q Bearings #1.3 (L472): the same question, twice

**Issue:** Near-duplicate items, and the outline's requirement that trap #42 appear "in two different question shapes" is not satisfied by asking the same shape twice.

- **B1.3:** *"A colleague applies a correct Ingress manifest to a fresh cluster. `kubectl get ingress` shows it. No traffic reaches the application. Name the most likely cause, and say what `kubectl get` actually proves."*
- **P8:** *"An Ingress object exists in a cluster and no traffic is being routed by it. The manifest passes review with no errors found. What is the most likely explanation, and what is notable about the manifest in this scenario?"*

Same scenario, same correct answer, same reasoning. P8 substitutes "manifest passes review" for "`kubectl get` shows it" — a rewording, not a second shape.

**Why-wrong explanation status:** both **present and good**. B1.3's key (L494–498) contains the chapter's best single line on this — *"It is a fact about storage. It is not a fact about routing"* — and correctly declines to blame the colleague (L498), which honours the Part 14 constraint the outline flagged. P8's key (L1291) supplies the distractor family.

**Recommended fix:** keep B1.3 as the diagnosis item. Rebuild P8 into the **second shape** the outline asked for and the **§3+§7+§8 interleave** that is currently missing — a single item that requires the reader to hold both inert objects at once: *"Two objects, both correct, both doing nothing: an Ingress on a cluster with no controller, and a NetworkPolicy on a plugin that does not implement it. Name what is absent in each, and name the one respect in which the two situations differ."* Correct answer: the controller and the plugin; the difference is that one failure is observable and the other is not. That one edit closes the duplication, discharges the trap-#42 "two shapes" mandate, and restores the mandated interleave.

---

### Q Practice 9 (L1227) / Q Bearings #1.4 (L474): the same question, twice

**Issue:** Near-duplicate. B1.4 asks "should you expect identical behaviour?" (yes/no); P9 asks "bug in the manifest, bug in one controller, or expected?" (three-way). Same fact (trap #45), same source sentence, same reasoning.

**Why-wrong explanation status:** B1.4 (L500) — **present but thin**; it explains why the fact reads like a caveat but never names the wrong belief ("the object is portable, so behaviour is identical"). P9 (L1293) — **present and specific**; *"Neither the manifest nor the controller is at fault in the sense the question invites"* correctly disposes of both wrong branches.

**Recommended fix:** P9 is the better item — keep it, and convert it to MC using its own three branches plus a fourth ("the reference specification is advisory, so neither controller is conformant"). Then repoint B1.4 at §3 material that is currently untested: **IngressClass and the default-class mechanism** are taught at L425–444 and reach only one question in the whole chapter (P6). Recovering B1.4 also relieves the §3 Practice block, which is over budget by one.

---

### Q Practice 12 (L1233): "Express the same requirement twice… name the resources involved…"

**Issue:** Carries the entire §5 Practice allocation alone, and carries no misconception treatment.

**Why-wrong explanation status:** **absent.** The key (L1307–L1311) states both vocabularies and closes with a genuinely valuable framing — *"It is the shapes you already know, redistributed across resources that belong to different owners. The routing requirement did not change. The ownership boundaries did."* No wrong belief is named or corrected. The obvious candidate, from the Exam Alert's own trap table (L1199), is *"Gateway API is a rename of Ingress"* — the exact misconception a translation exercise invites and the one it should be built to defeat.

**Also:** because P12 is the only §5 Practice item, **Gateway cardinality and the request flow are absent from the Practice set entirely** (see § Question-budget compliance).

**Recommended fix:** add a second §5 Practice item on cardinality (exactly one GatewayClass per Gateway; many Routes per Gateway), which restores the outline's allocation and drills a fact the Exam Alert has promoted. Add to P12's key: *"The tempting wrong reading is that Gateway API renames Ingress's parts. It does not — Ingress has one object and one owner; Gateway API has three objects and three owners, and that split is the reason the API exists."*

---

### Q Practice 7 (L1223) and Q Practice 17 (L1243): retrieval items with no misconception treatment

**Issue:** Both are recall-shaped retrieval items whose keys explain the value of the retrieval but name no wrong belief.

- **P7** key (L1281–L1285) ends *"The value is in converting a memorised component name into a recognised instance of a pattern."* True and worth saying. But the misconception available here is sharp and unaddressed: readers routinely believe the Ingress controller watches **Services** (or that the API server does the fulfilling). One clause would fix it.
- **P17** key (L1341–L1349) lists the four instances correctly and closes well. No wrong belief named — though for a "list everything you have met" item, the natural error is *undercounting*, and the key does not say that three-of-four is the common outcome or why.

**P17 also overlaps B1.5** (L476), which asks for the same rule plus the two Chapter 9 instances. This overlap is **defensible and deliberate** — the outline specifies P17 as "the Zenith assessed rather than merely asserted" and positions it last, and P17's superset framing (all four instances) is a genuine escalation over B1.5's two. Noting it only so the pattern is visible alongside the four unintended duplications.

**Recommended fix (P7):** add *"A common wrong answer names the API server as what does the fulfilling. The API server stores the object and serves it back; it changes nothing outside the cluster. That is the whole distinction between a record and a control loop."*

---

### Q Bearings #1.2 (L470), #2.4 (L743), #2.5 (L745): bare recall keys

**Issue:** No misconception treatment in any of the three keys.

- **B1.2** (key L490–492) gives both definitions and the discriminator. The obvious error — swapping the two — is never named as an error, even though the discriminator (host vs path) is stated. One clause: *"The error to watch for is swapping them. The tell is in the manifest: several entries under `paths` is fanout; several entries under `rules`, each with its own `host`, is virtual hosting."* That sentence already exists — at **P4's key, L1269**. It belongs in both.
- **B2.4** (key L767–769) is two words plus a note that exams reach for cardinality. Acceptable for a pure-cardinality item; flagged for completeness only.
- **B2.5** (key L771–773) closes Soundings Q1 nicely (*"The specification agrees with you"*) but names no wrong belief. The available one: readers commonly think the Gateway matches on the **path** rather than the `Host:` header, because §2 spent longer on paths.

**Severity:** WARN, not FAIL. All three are recall items where "the wrong answer" is largely "not knowing."

---

## Positive findings worth preserving

Four things in this question set are better than the shipped chapters and should survive revision:

1. **B3.2 / B3.3 / B3.4 / B3.5 are the strongest checkpoint in the book so far.** Every key names the wrong belief explicitly and corrects it in the reader's own terms: B3.2's *"Wrong answer to reject explicitly: 'no policy means no traffic.' That is the firewall instinct, and it is exactly backwards"* (L1064); B3.3's normalisation of the struggle (*"If you spent a while looking for the deny rule before accepting there isn't one, that is the correct experience of this question"*, L1072); B3.5's *"the reflex is to re-read the YAML, and the YAML is fine"* (L1084). This is exactly what rule 3 asks for in open-response form.
2. **B3.3's semantic framing is correctly pitched for downstream retrieval.** The key states additivity as *"the model has no subtraction operator"* (L1072) rather than as a NetworkPolicy quirk, and cross-bears to Ch 12 §9. That is precisely what the outline required so Ch 12's Zenith can retrieve rather than re-derive it. Do not let revision soften this phrasing.
3. **P14 is the best-constructed item in the chapter.** Three sub-questions over one scenario, each isolating a different rule (ingress isolation, the unselected-Pod default, direction independence), with a key that walks them individually and then names the trap (*"assuming one policy in a namespace changes the namespace's posture"*, L1327). This is the shape the rest of the §6 block should imitate.
4. **B2.3's key handles the `cluster operator` collision correctly** (L765), naming it as a role rather than the operator pattern of Ch 6 — the disambiguation the B7 ledger requires and the outline flagged. Likewise §6's opening word-collision disposal (L791–793) is doing real work for B3.1–B3.5.

---

## Retrieval-practice spacing

- **Chapter 10 target:** 20% of the combined Bearings + Practice pool **[B3 / arc outline]**, allocated by `outline.md` § 5 as **3 in Bearings and 4 in Practice = 7 of 32 (21.9%)**. Skill Part 10's band for chapters 6+ is 20–25%.
- **Actual:** **18.75% — 6 of 32**, tagged `[retrieval: chN]`.
  - **Bearings: 3 of 15** — B1.1 `ch9` (L468), B1.5 `ch3` (L476), B3.1 `ch4` (L1042). **Exactly the ratified allocation, in the ratified checkpoints** (2 in #1, 0 in #2, 1 in #3).
  - **Practice: 3 of 17** — P2 `ch9` (L1213), P7 `ch3` (L1223), P17 `ch3` (L1243). **Short by one.**
- **Status: short by 1.** Within rule 4's broad 10–25% band; **below** the outline's ratified allocation and below skill Part 10's 20–25% band for chapters 6+.

### The missing item is identified, and the draft miscounts it

`outline.md` § 5 specifies four Practice retrieval items. Three shipped. The fourth is fully specified and absent:

> **Labels and selectors** (Ch 4 §5) — §6 block. **[≥4-back, six chapters]**, carried as redundancy for the floor alongside Bearings #3 item 1. Framed as: *a single NetworkPolicy contains three selectors … Which is which, and what happens to the policy's effect if someone relabels a Pod that the first selector was matching?*

That item is worth recovering for a reason beyond arithmetic. Its correct answer — relabelling a Pod out of a policy's `podSelector` makes it **less** restricted, not more, because policies are the only thing that isolates — is a non-obvious consequence that the chapter teaches nowhere else and that no other question reaches. It is also the missing §6 Practice slot.

**The draft's own prose is off by one.** L1209 reads *"Seventeen questions. **Four** draw on earlier chapters, and they are tagged."* Three are tagged. Restoring the Ch 4 item makes the sentence true; otherwise the count needs correcting to three.

### ≥4-back floor: met, with the Chapter 4 anchor now unredundant

| Anchor | Distance | Carried by |
|---|---|---|
| Chapter 3 — the absent-component rule | **7 back** | B1.5, P7, P17 (three items) |
| Chapter 4 — labels and selectors | **6 back** | B3.1 **only** |

The floor is satisfied with margin. But the outline planned the Ch 4 Practice item explicitly as "redundancy for the floor alongside Bearings #3 item 1," and that redundancy is gone: **the six-chapters-back anchor now rests on a single question.** Chapter 8's outline established carrying a second ≥4-back item so the floor does not rest on one question, and Chapter 9 followed it. Chapter 10 has broken that practice on the Ch 4 side.

### Source diversity is thin

The arc outline's stated retrieval target is *"20%, from Ch 6–9."* Actual sources: **ch3 ×3, ch9 ×2, ch4 ×1. Nothing from Chapters 6, 7, or 8.** Only Chapter 9 represents the Ch 6–9 band.

Worse, the six items concentrate on **three facts**, not six:

| Fact retrieved | Items |
|---|---|
| Chapter 3's absent-component rule | B1.5, P17 (P7 retrieves the adjacent control-loop framing) |
| Chapter 9's Service-type ladder / HTTP limit | B1.1, P2 |
| Chapter 4's selectors | B3.1 |

**B1.1 and P2 are near-identical** — both ask which of two workloads an Ingress can carry (PostgreSQL/web app; message broker/HTTP app) and both answer "the HTTP one; the other goes to NodePort or LoadBalancer." P2's addition is "how many Services of which types," which forces the reader to remember the HTTP app also needs a backing Service. That is a real increment, but a thin one for a whole Practice slot in a chapter with the coverage gaps catalogued below.

**Recommended additions if short:**

1. **Restore the Ch 4 relabelling item** in the §6 Practice block, as specified. This fixes the count (7/32 = 21.9%), restores the Ch 4 redundancy, restores the §6 allocation, and tests a consequence nothing else reaches.
2. **Repoint P2 at an untested Ch 6–9 fact** to widen the band. The natural candidate is **Ch 9 §4's EndpointSlice**: the Services an Ingress routes to are backed by endpoint sets that can be empty, so an Ingress with a controller, correct rules, and a Service whose selector matches nothing fails in a *third* way that looks like neither §3 nor §7. That interleaves Ch 9 §4 with §2 and §3, and it strengthens §8's four-instance count by making the second instance a live consideration rather than a remembered one.
3. **Optionally add one Ch 8 retrieval item** to P6 or P9 — API versioning and the `networking.k8s.io/v1` group are Chapter 8 material, and §4's GA-stability argument (L555–561) leans on Ch 8 §6's vocabulary via cross-bearing without ever testing it.

---

## Coverage vs concepts

All 54 concepts and 3 commands from `outline.md` `kb_tags` (L136–193), checked against Bearings and Practice items. Soundings is a pre-test and does not count as coverage; where a concept reaches *only* Soundings, that is recorded as a gap.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| edge-router | marginal — P7 key (L1281) accepts it as an answer element; never required |
| cluster-network | **NO** |
| exposure-ceiling | **NO** — pre-tested at S2 (L52) only; §1's ceiling arithmetic reaches no post-reading item |
| l4-l7-boundary | yes (P1) |
| north-south-traffic | **NO** |
| east-west-traffic | **NO** |
| protocol-aware-routing | yes (P1, via the key) |
| ingress | yes (B1.1, P2, P3, and throughout) |
| ingress-rule | yes (P4, P12) |
| ingress-host | yes (B1.2, P4) |
| ingress-path | yes (P4, P5) |
| path-type | partial (P5 — `Prefix` only; see note below) |
| simple-fanout | yes (B1.2, P4) |
| name-based-virtual-hosting | yes (B1.2) — **Bearings only; no Practice item** |
| tls-termination | partial (P3, as one item in a four-item list) — **the mechanism is untested; see note** |
| default-backend | **NO** |
| single-service-ingress | **NO** |
| ingress-controller | yes (B1.3, P7, P8) |
| ingressclass | yes (P6) |
| reference-specification | yes (B1.4, P9) |
| absent-component-pattern | yes (B1.5, P8, P17) |
| feature-freeze | yes (B2.1, P10) |
| frozen-not-deprecated | yes (B2.1, B2.2, P10, P11) |
| ga-stability-guarantee | yes (B2.1, P10) |
| gateway-api | yes (B2.3, P12) |
| gatewayclass | yes (B2.3, B2.4, P12) |
| gateway | yes (B2.3, B2.4, P12) |
| httproute | yes (B2.3, B2.4, P12) |
| parentrefs | marginal — P12 key (L1309) names it; the stem does not require it |
| role-oriented-design | yes (B2.3, P12) |
| infrastructure-provider-role | yes (B2.3, P12) |
| cluster-operator-role | yes (B2.3, P12) |
| application-developer-role | yes (B2.3, P12) |
| gateway-request-flow | yes (B2.5) — **Bearings only; no Practice item** |
| networkpolicy | yes (B3.1–B3.5, P13–P16) |
| l3-l4-control | **NO** |
| application-centric-policy | **NO** |
| pod-selector | yes (B3.1) — **Bearings only** |
| namespace-selector | yes (B3.1) — **Bearings only** |
| ipblock | **NO** |
| cidr-range | **NO** |
| policy-types | yes (P13; B3.2 implicitly) |
| ingress-isolation | yes (B3.2, P14) |
| egress-isolation | yes (B3.2, P13, P14) |
| non-isolated-default | yes (B3.2, P14) |
| additive-policy-semantics | yes (B3.3, P15) |
| no-deny-rule | yes (B3.3, P15) |
| both-ends-must-allow | yes (B3.4) — **Bearings only**; P14's key mentions it in passing |
| default-deny-by-selection | **NO** |
| node-local-traffic-always-allowed | yes (B3.5; P14 key) |
| self-traffic-unblockable | yes (B3.5) |
| policy-plugin-dependency | yes (B3.5, P16) |
| silently-inert-policy | yes (B3.5, P16) |
| networkpolicy-out-of-scope | partial (P15 — explicit-deny item only; see note) |
| **`kubectl-get-ingress`** | yes (B1.3, L472) |
| **`kubectl-describe-ingress`** | **NO — and not taught either.** The command does not appear anywhere in the draft; `outline.md` §3 assigned it. §3 has no `kubectl describe` at all (the two occurrences, L858 and L987, are both NetworkPolicy). |
| **`kubectl-get-networkpolicy`** | **NO** — taught at L987, tested nowhere |

### The gaps that matter

**Eleven concepts are taught and never tested.** Four are consequential:

1. **`default-deny-by-selection` (taught L925–L949).** This is the *constructive payoff* of the entire additive/no-deny argument — the answer to the objection §6 explicitly raises ("if there is no deny rule, how does anyone ever lock anything down?"), complete with a sourced `podSelector: {}` manifest and the binding rule that an omitted `policyTypes` defaults to at least `Ingress`. **Not one question touches it.** B3.3 tests that you cannot subtract; nothing tests that you can still arrive at denial by construction. For a security-adjacent competency this is the single most valuable practical technique in §6 and it is unassessed.

2. **`default-backend` (taught L382).** Carries a hard structural rule — *"if no `.spec.rules` are specified, `.spec.defaultBackend` must be specified"* — plus the unmatched-request fallback. That is exactly the enumerable, either-known-or-not fact the exam form reaches for. Untested. It is also the mechanism behind `single-service-ingress` (L208–L218), likewise untested, so the §2 shapes progression is drilled at three of its four steps.

3. **`ipblock` / `cidr-range` (taught L803–L858).** The **third of the three identifiers**. B3.1 tests the two selector-based identifiers and stops. A reader could complete this chapter's entire question set without ever confirming that IP blocks exist as a peer type, and the `except` field in the §6 manifest (L830) is never revisited.

4. **`l3-l4-control` / `application-centric-policy` (taught L797).** §1's Fixed Point (L148) makes the layer ladder the chapter's organising idea, and §6's whole framing is that it *descends* back to layers 3 and 4. **P1 tests the ascent and nothing tests the descent.** A question asking at what layer a NetworkPolicy operates — and why that means it cannot see a hostname — would close the chapter's own structural argument and simultaneously reinforce §7's "no TLS, no Service-name targeting" limits.

**`north-south-traffic` / `east-west-traffic`** (L150–L158, with a 🪢 Mnemonic at L158 and a Chapter Summary row at L1359) are given a named beat, a mnemonic, and a summary entry — the full apparatus of something to be remembered — and are then never asked about. Either test them once or accept them as pure orientation vocabulary and drop the mnemonic.

**Three partial-coverage notes:**

- **`path-type`:** P5 tests `Prefix`'s element-wise semantics, and does it well. Untested: `Exact`, `ImplementationSpecific`, the requirement that every path have a `pathType`, and the **longest-match-wins / `Exact`-breaks-ties** precedence rule (L390). The precedence rule in particular is a classic enumerable exam target.
- **`tls-termination`:** reaches only P3, as one of four list items. The Kubernetes-specific mechanism — `kubernetes.io/tls` Secret, keys named `tls.crt`/`tls.key`, single TLS port 443, **cleartext onward to the Pods** — is untested despite the cleartext fact being promoted to Exam Alert item 6 (L1176) and carrying a forward cross-bearing to Ch 17 §5.
- **`networkpolicy-out-of-scope`:** the ten-item Dead Reckoning list (L1005–L1030) reaches only its explicit-deny entry, via P15. The Exam Alert trap table promotes three more — no TLS, no Service-name targeting, no logging (L1197, L1200) — and none is tested. **"NetworkPolicy can target a Service"** is the highest-value miss: §7's 🔭 Closer Look argues it follows necessarily from §6's Pod-selection semantics, which makes it a reasoning item rather than a recall item, and it is the out-of-scope entry a reader is likeliest to reach for after nine Service-shaped chapters.

**One taught-and-untested fact from a source-drift note:** §5 (L601–L608) names **four** stable Gateway API kinds including `GRPCRoute`, while FP L612 and B2.3 name three. The draft handles this carefully — B2.3's stem says "the three **role-mapped** resources," and the AUTHOR-REVIEW comment flags it — but no question disambiguates, so a reader asked "how many stable kinds does Gateway API define" has been taught four and drilled on three. Flagged here as a coverage note; the count itself is the fact-accuracy and curriculum-alignment stages' call.

---

## Recommended action, ordered

1. **Convert the 17 Practice questions to four-option multiple choice**, matching chapters 7–9. Six convert near-mechanically from distractors their own keys already name (P3, P5, P8, P10, P13, P15). This is the blocking item; everything below is cheaper once it is done.
2. **Restore the Ch 4 relabelling retrieval item** in the §6 Practice block. Fixes the retrieval count to 21.9%, restores the ≥4-back redundancy on the Chapter 4 anchor, restores the §6 allocation, and corrects the miscount at L1209.
3. **Rebuild P8 as the §3+§7+§8 interleave** the outline mandates — two inert objects, name what is absent in each and the one respect in which they differ. This removes the P8/B1.3 duplication, discharges trap #42's "two shapes" requirement, and gives the Zenith its operational assessment.
4. **Add a §5 cardinality Practice item**, restoring the outline's 2-item allocation and drilling a fact the Exam Alert has promoted.
5. **Repoint B1.4 at IngressClass** (P9 is the better reference-specification item), relieving the over-budget §3 Practice block and testing a section that currently reaches one question.
6. **Add one question for `default-deny-by-selection`.** It is the highest-value untested concept in the chapter.
7. **Three one-clause Soundings trims:** cut *"and it is the instinct §6 is going to take away from you"* (L75); cut *"at layer 3 or 4"* (L81); soften §7's overclaim at L1003 to say the reader derived the *dependency*, not the central fact. Leave S5 as designed and keep the 6+ rubric branch's instruction to read §4 carefully regardless.
8. **Fill the coverage gaps in priority order** as budget allows: `l3-l4-control`, `default-backend`, `ipblock`, the `pathType` precedence rule, "NetworkPolicy cannot target a Service."

---

**Two things I did not assess**, per the stage's scope: whether any stated answer is factually correct in the real world (fact-accuracy audit), and the voice or prose of the questions (theming-density audit). Where I quote a key approvingly, I am endorsing its *question architecture*, not certifying its content.
# Question-Quality Audit — Chapter 3

## Summary

- Chapter type: **content**
- Total questions inspected: **40**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **13** (across **3** checkpoints — 5 / 4 / 4)
  - Practice questions: **19**
- Question budget compliance: **met** (40 of 40, exact on every category)
- Weak distractors (WARN): **5** (3 clear, 2 borderline)
- Trap answers that don't target real misconceptions (WARN): **3**
- Missing or incomplete why-wrong explanations (FAIL): **0 missing, 2 incomplete**
- Retrieval-practice spacing: **non-compliant — 6.3% against a 10% target (short by 1 item)**
- Soundings spoiler check: **1 question reveals a Fixed Point — FAIL** (Q8 answer key; compounded by the epigraph)

**Two cross-cutting architecture defects outrank every individual question below and are reported in their own sections:**

1. **Answer-position bias.** Across all 32 Bearings + Practice items, the correct answer is **B in 21 of 32 (66%)** and **A in 0 of 32 (0%)**. On Practice alone it is B in 14 of 19 (74%). A test-wise reader who guesses B on every unfamiliar item scores roughly two-thirds without knowing anything.
2. **Correct-answer length tell.** In at least 8 items the correct option is the longest and most qualified in its set. Combined with (1), a meaningful fraction of this chapter's questions are answerable by exam technique rather than by knowledge.

Neither is a content problem — the questions themselves are, with the exceptions listed, unusually well-built. Both are mechanical and both are cheap to fix.

---

## Question-budget compliance

Compared against `question_budget` in the outline frontmatter.

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 13 | 13 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 | 3 | **met** |
| Practice Questions | 19 | 19 | **met** |
| **Chapter total** | **40** | **40** | **met** |

Checkpoint distribution matches the outline's planned 5 + 4 + 4 exactly, placed after §3, §5, and §6 as specified. No shortfall anywhere; this is the cleanest budget compliance the pipeline has produced.

**Difficulty mix drift (minor, no action required).** The outline planned roughly 6 ⚪ / 9 🔵 / 4 🟡 for Practice. Actual is **4 ⚪ / 11 🔵 / 4 🟡** — two Foundation items drifted up to Standard. The 🟡 allocation is exactly on plan and lands on the intended integrative items (Q12, Q14, Q17, Q18). Noted only so the book-level mix stays trackable.

**Scope discipline: clean.** No question in this chapter requires `spec`/`status` field names (Ch 4), ReplicaSet/Deployment (Ch 6), kube-proxy modes (Ch 9), the scheduler's filter/score/bind mechanism (Ch 7), or GitOps (Ch 15). Bearings #3 Q1 describes replica reconciliation without naming ReplicaSet, which is exactly the scope guard the outline asked for. Practice Q7 quotes only the scheduler *factor list* that §2 legitimately owns and never touches the algorithm. Worth recording as a pass — this was the checkpoint the outline predicted drafting would leak from, and it didn't.

---

## Soundings spoiler check

The chapter's three ★ Fixed Points:

- **FP1 (§3)** — the census: eight components, two optional for two different reasons, one not Kubernetes software.
- **FP2 (§6)** — the control loop: desired state, current state, an action that closes the gap, repeating without terminating.
- **FP3 (§7)** — orchestration, technically, is the execution of a defined workflow (A then B then C); Kubernetes disclaims it in favor of independent, composable control processes.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Script vs. continuous check when scaling 3 → 5 | **no — but stem is leading** (see WARN below) | Stem offers the loop as an option ("keeps checking the count and acts when it's wrong") and the trailing sentence names the criterion. Answer key is disciplined: "Most people with scripting experience answer 'start two.' §6 is written for that answer." No mechanism vocabulary. |
| 2 | Who notices a 3 a.m. node failure | no | "§6 tells you which one Kubernetes chose and why." Withholds the answer correctly. |
| 3 | Does every machine run the same software | no | "Two kinds of machine running two different sets of software. §2 and §3 name them." States the split, does not enumerate FP1. |
| 4 | Which node component owns the containers *[retrieval: ch2]* | no | Names the kubelet, which Chapter 2 already taught. Naming one previously-taught component is not the census. Sanctioned by the outline. |
| 5 | How many actors should reach the datastore directly | no | Answer "One." §5's hub claim is a ⚓ Worth Securing, not a ★ Fixed Point. Outline explicitly designed this as a rule-known / consequences-unknown pre-test. |
| 6 | Does Kubernetes build your images | no | "No. Images are built elsewhere and pulled. §1 has the rest of that list." Withholds the is-not list. |
| 7 | Written from scratch, or descended | no | Gives Borg + Omega. Not a Fixed Point. (Does hand the reader half of Practice Q3 — see note below.) |
| 8 | What does "orchestration" mean precisely | **YES — partial, verbatim** | Answer key: *"The technical definition of orchestration is the execution of a defined workflow: first do A, then B, then C."* §7's ★ Fixed Point opens: *"**Orchestration, technically, is the execution of a defined workflow: first do A, then B, then C.**"* Sentence-level verbatim match on the definitional clause. |

### FAIL — Soundings Q8 answer key discloses half of Fixed Point 3

**The compounding factor is the epigraph, not the question.** At line 34, *before* the Soundings block, the chapter prints:

> *"Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration."* — the Kubernetes documentation

So by the time a reader opens the `<details>` block, they have the *disclaimer* half of FP3 from the epigraph and now receive the *definition* half from A8. Between them, FP3 is fully in the reader's hands before §1 begins. §7's payoff then restates something the reader was told twice on page one.

**The outline sanctioned exactly this wording** ("Its answer key gives the dictionary sense only — orchestration as the execution of a defined workflow — and stops"), and the draft obeyed the letter of that instruction precisely: it does *not* say Kubernetes disclaims it, does *not* use "eliminates the need for orchestration," and does *not* contrast composable control processes. What the outline did not anticipate was its own epigraph recommendation (Open questions #11) landing two blocks above and supplying the withheld half.

**Recommended fix — pick one, not both:**

- **(a) Trim A8** to withhold the definition: *"It's a technical term with a specific meaning, and the meaning is narrower than the way the industry uses the word. §1 plants it; §7 settles it."* Keeps the epigraph, which is a genuine curiosity gap when the reader can't yet decode it.
- **(b) Swap the epigraph** to the outline's own fallback (Grace Hopper, *"The most dangerous phrase in the language is 'we've always done it this way'"*), which fits §1's era progression and spoils nothing. Keeps A8 as drafted.

(a) is cheaper and preserves the stronger epigraph. Either restores §7's Zenith.

### Rubric and disclosure checks

| Check | Status |
|---|---|
| `<details>` collapsible answer disclosure | **pass** (lines 59–84) |
| 6+ / 3–5 / 0–2 reading-strategy rubric, all three bands | **pass** — all three present, each with specific guidance, and 6+ correctly carries the two exceptions (read §6 at full pace; don't skim §4) |
| Question count for a content chapter (8) | **pass** |
| One-line-per-answer discipline | **partial** — A1, A2, and A8 run to 2–3 sentences. A1 and A2 spend the extra length on *where the chapter addresses it*, which is legitimate. A8's extra sentence is the spoiler above. |

**Minor note, no action.** A7 hands the reader "Borg, and its research successor Omega" verbatim, which is most of Practice Q3's answer. This is acceptable — the Soundings is a pre-test, §1 teaches the same fact in between, and Q3 additionally requires the language (Go). Recording it only so it isn't rediscovered as a defect later.

---

## Per-question findings

### WARN — Soundings Q1: "Would you write a script that starts two more, or build something that keeps checking the count and acts when it's wrong? Which is the better foundation for a system that also has to survive machines dying?"

**Issue:** The stem is leading, which defeats the diagnostic purpose the outline built it for.

The outline's stated intent: *"Nearly every reader with scripting background answers 'start two,' and that answer is the exact model §6 has to replace. Surfacing it first means §6 corrects a live belief rather than filling a void."* The drafted stem names the winning criterion in its second sentence — *"a system that also has to survive machines dying"* — which tells the reader which of the two options to pick. Nearly every reader will now answer "the loop," the pre-test will show no signal, and §6 will fill a void rather than correcting a live belief. This is the highest-value pre-test in the chapter and its diagnostic value is currently near zero.

**Distractor analysis:** N/A — Soundings are free-response; rule 1 does not apply.

**Why-wrong explanation status:** N/A for Soundings. The rationale line is present and correctly disciplined.

**Recommended fix:** Cut the second sentence. Ask the flat question and let the reader commit:

> You have three copies of an application running and you want five. How would you make that happen?

The answer key already does the corrective work ("Most people with scripting experience answer 'start two.' §6 is written for that answer"), so nothing is lost by removing the signpost from the stem.

---

### WARN — Bearings #1 Q3: "How does kube-controller-manager run its controllers?"

**Issue:** Why-wrong explanation for two of three distractors is present but vague, and vague in a way that can leave a wrong inference behind.

**Distractor analysis:**
- A) One operating-system process per controller — **plausible to a real misconception** (the docs' own sentence opens "Logically, each controller is a separate process"). This is B1 trap #3 and the distractor is excellent.
- B) One container per controller, in a single Pod — **plausible**; matches how a reader would guess Kubernetes packages things.
- C) One Pod per controller, in the kube-system namespace — **plausible**, same reason.
- D) All controllers compiled into a single binary, running in a single process — correct.

**Why-wrong explanation status:** **present but vague** for B and C. The current text is:

> **B and C are wrong** — plausible-sounding Kubernetes-flavored packaging that the documentation never describes. If you picked one of these, the useful lesson is that "sounds like how Kubernetes would do it" is not a reliable guide.

That teaches a meta-lesson ("don't trust plausibility") in place of the fact. Worse, it risks a wrong inference: a reader who has seen control-plane components running as Pods in `kube-system` will read "the documentation never describes that" as "the controller-manager doesn't run as a Pod," which is not what makes B and C wrong. What makes them wrong is the same single fact that makes A wrong — **all controllers are inside one binary in one process**, so there is no per-controller unit of any kind, whether process, container, or Pod.

**Recommended fix:** Replace the grouped explanation with the specific reason, and keep the meta-lesson as a trailing sentence rather than as the explanation:

> - **B and C are wrong** for the same reason A is: there is no per-controller unit of any kind. The unit is the controller-manager itself, and every controller lives inside it. Whatever the controller-manager is packaged as in your cluster, it is *one* of that thing, not one per controller.

---

### WARN — Bearings #2 Q2, option D: "cloud-controller-manager is not a real component"

**Issue:** Implausible distractor. The question is effectively three-option.

**Distractor analysis:**
- A) All three — **plausible to misconception "every cluster has one"** (B1 trap #2). This is the item's whole point and it works.
- B) The managed cloud cluster only — correct.
- C) The managed cloud cluster and the data center cluster — **plausible** to a reader who thinks "our own data center is also infrastructure, so it needs integrating." Good distractor.
- D) None — cloud-controller-manager is not a real component — **implausible.** The reader met this component in §2 sixty lines earlier, complete with its published description. No reader picks it, and no identifiable misconception produces it. The answer key confirms it is filler: *"it's a real, documented control-plane component. It's just conditional."*

**Why-wrong explanation status:** present and specific for A and C; present but necessarily hollow for D, because there is nothing to explain.

**Recommended fix:** Replace D with a distractor targeting a misconception that actually exists — the belief that the component is always present but idles when there's no provider to talk to:

> D) All three, but on the laptop and in the data center it runs with no provider configured

…with the why-wrong: *"Not 'runs and does nothing' — genuinely absent. The documentation states that a cluster on your own premises or in a learning environment on your own PC does not have a cloud controller manager. An idle-but-present component would still show up in a component listing; this one doesn't."* That converts a dead option into the item's second-best teaching moment.

---

### WARN — Bearings #2 Q3, option B: answer-length tell

**Issue:** The correct option is more than twice the length of any distractor and is the only one carrying a qualifying clause.

**Distractor analysis:**
- A) It cannot be used in production clusters (8 words) — plausible to "addon = not production-grade."
- B) It extends the cluster's functionality and is implemented using Kubernetes resources, rather than constituting the cluster (17 words) — **correct, and visibly the most complete option.**
- C) It runs on the control plane rather than on nodes (10 words) — plausible placement confusion.
- D) It is required on every cluster and is simply categorized separately (11 words) — plausible, and the answer key handles it very well.

The distractors are individually good. The problem is purely mechanical: B looks like the answer before it is read. See the aggregate section below — this item is one of eight with the same signature.

**Why-wrong explanation status:** present and specific for all three, and D's is the strongest explanation in the chapter (*"Something can be near-universal in practice and still not part of the cluster's definition. The gap between those two is exactly where the absent-component pattern lives."*).

**Recommended fix:** Shorten B and lengthen the distractors to match. E.g. B → *"It extends the cluster rather than constituting it, and is built from ordinary Kubernetes resources"*; C → *"It is a control-plane component that happens to be documented in a separate section."*

---

### WARN — Practice Q1, option D: "Schedule applications to run at different times of day"

**Issue:** Distractor targets no misconception, and the answer key says so outright.

**Distractor analysis:**
- A) Configure per-application resource quotas in the operating system — **strong distractor.** Modern readers know cgroups exist and will reach for this; the documented problem statement is precisely that no such boundary mechanism was available. Genuinely instructive.
- B) Run each application on a different physical server — correct.
- C) Run each application inside a hypervisor partition — **strong distractor**, targets era confusion, which is the exact discrimination §1 is teaching.
- D) Schedule applications to run at different times of day — **no misconception.** Its own why-wrong reads: *"never described anywhere as a real practice; it's an invented distractor."* An answer key that admits an option is filler has documented a rule-1 violation for us.

**Why-wrong explanation status:** present and specific for A and C; present and self-invalidating for D.

**Recommended fix:** Replace D with a period-plausible practice that still isn't the documented answer:

> D) Run each application under a separate operating-system user account with per-user limits

…why-wrong: *"A real historical practice, and it does constrain some resources — but not the ones that mattered. One application could still consume most of the machine's CPU or memory and starve the rest, which is the specific failure the documentation describes."* That preserves the discrimination the item is aiming at.

---

### WARN — Practice Q7: "Which of these is *not* listed among the factors kube-scheduler takes into account?"

**Issue:** The correct answer is absurd on its face, so the item is answerable with zero knowledge of the scheduler.

**Distractor analysis:**
- A) Individual and collective resource requirements — a real listed factor.
- B) Affinity and anti-affinity specifications — a real listed factor.
- C) Data locality — a real listed factor.
- D) The alphabetical order of node names — **correct answer, and transparently silly.** A reader who has never opened the documentation eliminates A, B, and C as "sounds like scheduling" and picks D on tone alone.

This inverts the intended difficulty. In a NOT-question the *key* has to be plausible; the distractors are already guaranteed plausible because they're real. Here the key carries a giveaway.

**Why-wrong explanation status:** present, grouped, and adequate for a NOT-question (*"A, B, and C are wrong as answers because all three are listed factors"*).

**Recommended fix:** Replace D with something that sounds like a scheduling input a reasonable system might use but that the documentation does not list:

> D) How recently each candidate node was rebooted

…why-wrong: *"Plausible as a stability heuristic, and some schedulers in other systems do weigh something like it. It is not among the factors the Kubernetes documentation lists, and this item is testing that list."* Alternatively, flip the item to positive form and test one factor directly — the outline's difficulty guidance for this chapter is that difficulty should come from combination, not from obscurity, and a NOT-question over a quoted list is neither.

---

### WARN — Practice Q13 + Q14: sequential answer leak

**Issue:** Q14's option C names both optional components, which gives away Q13's answer to anyone who reads ahead — and readers routinely scan a practice set before answering.

- **Q13** asks *which two* components the documentation marks optional. Correct: B) kube-proxy and cloud-controller-manager.
- **Q14** asks whether the two reasons are the same. Its correct option C reads: *"No — kube-proxy is optional because a network plugin may do its job; cloud-controller-manager is optional because there may be no cloud provider to integrate with."*

Q14 additionally collapses toward a two-way choice on its own: A and B both open "Yes," C and D both open "No," and D invents conditions transparently ("kube-proxy is optional only in single-node clusters; cloud-controller-manager is optional only in clusters without Services"), leaving C as the only credible "No."

**Why-wrong explanation status:** present and specific for both items. Not the problem here.

**Recommended fix:** Separate them. Move Q14 well away from Q13 — the natural home is late in the set, after Q17, where it also functions as the §2 + §4 interleaved item the outline wanted. Alternatively rewrite Q14 to name only one component in each option, e.g. *"kube-proxy is optional for the same reason cloud-controller-manager is: [X]"* with the component names carried in the stem rather than in the key.

---

### WARN — Practice Q19, options C and D: "invented mechanisms"

**Issue:** Grouped why-wrong is vague, and it mislabels option C in a way an informed reader will notice.

**Distractor analysis:**
- A) Edit the file inside the running container and restart the process — **strong distractor**, the exact instinct immutability rules out. Well explained.
- B) Build a new image that includes the change, then recreate the container — correct.
- C) Mount a writable layer over the container and patch it in place — **plausible and partly true.** Containers *do* have a writable layer; a reader who knows that will be confused by an explanation calling this "invented."
- D) Ask the kubelet to hot-patch the container's filesystem — fairly called invented; no such kubelet capability exists.

**Why-wrong explanation status:** **present but vague** — *"C and D are wrong — invented mechanisms."* One clause for two distractors, one of which is not invented.

**Recommended fix:** Split them and give C its real reason:

> - **C is wrong**, but not because the mechanism doesn't exist — a container's writable layer is real. It's wrong because anything written there belongs to *that container instance* and is gone the moment the container is replaced, which is the thing Kubernetes does constantly. That's the practical teeth of immutability: the change has to live in the image, or it doesn't survive.
> - **D is wrong** — there is no such kubelet capability. The kubelet starts and stops containers through the CRI; it doesn't reach inside their filesystems.

The existing trailing sentence connecting immutability to the control loop (*"replace, don't mutate"*) is good and should stay.

---

### Borderline — logged, no fix required

| Item | Option | Note |
|---|---|---|
| Bearings #3 Q4 | D) "No, but only in clusters with autoscaling enabled" | Weakest option in an otherwise excellent item. A reader who equates "constant change" with "autoscaling" could reach for it, so it isn't dead — just thin. The other three options (A intuitive-and-wrong, B "stuck in a loop" pathology, C correct) carry the item. |
| Practice Q5 | A) "It runs containers on control-plane machines" | Thin — few readers think a key-value store runs containers. C and D are both strong, so the item survives. Its larger problem is the length tell (B is 18 words against 8/8/9). |
| Practice Q16 | A/C/D grouped why-wrong | Grouped and terse, but the follow-on sentence — *"real terminology and invented terminology read identically until you've anchored the real pair"* — names the actual failure mode, which is what a why-wrong owes. Acceptable as written. |
| Practice Q11 | A/C/D | Tagged 🔵 but effectively ⚪: three of four options are components the reader memorized ten pages earlier. Contributes to the ⚪-shortfall noted under budget compliance. |

---

## Cross-cutting: answer-position bias and length tell

These two defects are worth more attention than any single question above, because they apply to the whole set and they are mechanical to fix.

### Correct-answer letter distribution

| | A | B | C | D | n |
|---|---|---|---|---|---|
| Bearings #1 | 0 | 2 | 2 | 1 | 5 |
| Bearings #2 | 0 | 3 | 1 | 0 | 4 |
| Bearings #3 | 0 | 2 | 2 | 0 | 4 |
| Practice | 0 | 14 | 4 | 1 | 19 |
| **Total** | **0 (0%)** | **21 (66%)** | **9 (28%)** | **2 (6%)** | **32** |

Practice alone is **B in 14 of 19 (74%)**. **Not one correct answer anywhere in the chapter is A.**

**Failure scenario:** a reader who has internalized nothing from §1–§7 opens the Practice set, guesses B on every item, and scores 14/19 (74%). The chapter's own rubrics then tell them they are in good shape. That is a false-competence signal produced entirely by question mechanics, and it is exactly the outcome the skill's ethical guardrails (*"NEVER create false beliefs about exam content or difficulty"*) exist to prevent. Secondary cost: the chapter trains a habit — "when unsure, pick B" — that will not transfer to the real exam.

**Recommended fix:** Mechanical reshuffle of option order. Target roughly 8/8/8/8 across the 32 items, with no letter above ~35% and none at zero. Reshuffling requires editing the option lists and the corresponding letters in each answer key; the explanations themselves are unaffected because they are all keyed to option *content*, not position. No 🪝/⚓/⚠ callout text references option letters, so nothing outside the question blocks needs touching.

### Correct-answer length tell

Items where the correct option is the longest and the only one carrying a qualifying clause:

| Item | Correct option length | Longest distractor | Ratio |
|---|---|---|---|
| Bearings #2 Q3 (B) | 17 words | 11 | 1.5× |
| Bearings #2 Q4 (B) | 18 | 14 | 1.3× |
| Practice Q5 (B) | 18 | 9 | 2.0× |
| Practice Q12 (B) | 14 | 9 | 1.6× |
| Practice Q14 (C) | 23 | 17 | 1.4× |
| Practice Q17 (B) | 17 | 12 | 1.4× |
| Bearings #1 Q3 (D) | 11 | 10 | 1.1× (mild) |
| Bearings #2 Q1 (C) | 13 | 12 | 1.1× (mild) |

**Failure scenario:** the standard test-taking heuristic "pick the most complete, most hedged option" resolves six of these correctly without any subject knowledge. Stacked on the B-bias, a knowledge-free reader clears most of the set.

**Recommended fix:** For the six 1.3×-and-up items, either trim the key to the distractors' register or extend the distractors with equivalent qualifying clauses. Extending is generally better here because these distractors are already good — giving them the same syntactic weight makes them harder to dismiss on sight. Practice Q5 is the worst offender and the easiest fix: *"A consistent, highly-available key value store holding all cluster data"* (10 words) instead of the current 18.

---

## Answer-key structure: revision prompts

Per the skill's self-correction design and the Ethical Checkpoint item *"Revision prompts included for low checkpoint scores,"* every ☆ Taking Your Bearings block owes a score-band rubric. Coverage is inconsistent:

| Checkpoint | Low band (0–2) | Middle band | Top band | Status |
|---|---|---|---|---|
| #1 — The Ship's Company (5 Q) | ✅ present, specific ("Go back to §2 and §3… ten minutes") | ✅ 3–4 present | ❌ no 5/5 line | **partial** |
| #2 — Arrangement and Optionality (4 Q) | ❌ **absent** | ❌ absent | ❌ absent | **FAIL — no rubric at all** |
| #3 — Controllers and the Loop (4 Q) | ✅ present, specific ("Re-read §6… Chapter 4 opens on the mechanics of desired state") | ❌ no 3 band | ❌ no 4/4 line | **partial** |

**Bearings #2 has no score guidance whatsoever.** It runs answers → `> **Design note:**` → `Checkpoint: You've Now Mastered`. A reader who misses three of four gets no signal that they should go back, and the checkpoint that follows congratulates them on mastery. This is the one checkpoint where a low score genuinely predicts trouble downstream — its Q4 is the chapter's second-most-important idea and Chapter 15 retrieves it.

**Recommended fix:** Add to Bearings #2, matching the register of the other two:

> **If you scored 0–2:** Re-read §5, particularly "The submission story," and look again at the figure — specifically at the arrows that aren't drawn. Then re-read the ⚠ Navigational Hazards in §4. Both traps in this checkpoint turn on the word "optional" and both are cheap points on exam day.
>
> **If you scored 3:** Solid. If Q4 was the one you missed, that's the one to go back for.

Add the missing top bands to #1 and #3 (one line each — the skill's Part 13 pattern is 5/5, 3–4, 0–2, and a reader who aced a checkpoint should be told so rather than dropped straight into the summary).

The `> **Design note:**` on Bearings #2 Q4 is a genuinely good device and should stay — it just isn't a substitute for a rubric.

---

## Retrieval-practice spacing

- **Chapter 3 target:** 10% (the schedule's opening rung, per the outline's `[B3]` inheritance; skill Part 10 places Chapter 3 at 10%). The outline scopes all retrieval to **Chapter 2** and excludes Chapter 1 and exam mechanics.
- **Outline's plan:** 3 items — **1 in Bearings, 2 in Practice** (3 of 32 = 9.4%).
- **Actual:** **2 items** tagged `[retrieval: ch2]` in the graded pool — Bearings #1 Q5 (the CRI boundary) and Practice Q19 (image immutability). Plus one untagged-for-budget item in the Soundings (Q4, the kubelet), which the outline explicitly excludes from the count.
- **Rate:** 2 of 32 = **6.3%** (or 1 of 13 = 7.7% counting checkpoint questions only). Skill Part 10's band for chapters 3+ is 10–25%.
- **Status: short-by-1.**

**What's missing, specifically.** The outline named three Chapter 2 anchors and assigned each a home:

| Ch 2 anchor | Planned home | Shipped? |
|---|---|---|
| The CRI boundary — which component talks to the runtime | Bearings #1, item 5 | ✅ **Bearings #1 Q5** — and it is the best question in the checkpoint. Option C ("kube-scheduler, by connecting directly to the container runtime") is the highest-value wrong answer in the chapter. |
| Image immutability | Practice | ✅ **Practice Q19** |
| **Container vs VM** | **Practice — "the architectural reason behind §1's era transition"** | ❌ **absent.** No Practice item asks it. Q1 covers the traditional era from this chapter's own text; Q2 covers the capability list. Nothing reaches back to Chapter 2's architectural contrast. |

**Recommended addition — one item, placed adjacent to Q1 so the era material clusters:**

> **Q1b.** 🔵 *[retrieval: ch2]* The container era's defining change is that containers have relaxed isolation properties compared with VMs. Architecturally, what is it that a container shares with the host that a virtual machine does not?
>
> A) The physical hardware
> B) The operating system kernel
> C) The filesystem
> D) The network interface
>
> **Q1b — B.** *[retrieval: ch2]* Containers have relaxed isolation properties that let them share the operating system kernel among applications, which is why they're considered lightweight. A VM is a full machine running all the components including its own operating system on top of virtualized hardware.
> - **A is wrong** — VMs share the physical hardware too; that's what virtualization *is*. Sharing hardware is the previous era's change, not this one.
> - **C is wrong** — and it's the reversal worth catching. A container has *its own* filesystem, just as it has its own share of CPU, memory, and process space. The filesystem is one of the things that stays separate.
> - **D is wrong** — networking is configurable in both models and isn't the architectural distinction the era transition turns on.

This brings the count to 3 of 33 = **9.1%**, inside tolerance of the 10% rung, and it fills the one anchor the outline named and the draft dropped. Note that option B's wording must match whatever Chapter 2 resolved for the "operating system" vs "kernel" question flagged in the §1 AUTHOR-REVIEW comment (line 128) — this question would become a fourth place in the book where that phrase appears.

**Tagging discipline: clean.** Both shipped retrieval items carry `[retrieval: chN]` in the stem *and* in the answer key, which is the convention the pipeline needs for later mechanical audits. Soundings Q4 is tagged in both places too. No untagged retrieval and no mistagged non-retrieval.

---

## Interleaving

The outline required **at least 5 of the 19 Practice items to combine two sections**. Actual: **4 clearly integrative.**

| Practice item | Sections combined | Verdict |
|---|---|---|
| Q12 (object exists, component absent) | §4 + §6 | ✅ integrative |
| Q13 (which two are optional) | §2 + §3 + §4 | ✅ integrative |
| Q14 (are the reasons the same) | §2 + §4 | ✅ integrative — the outline's named "§2 + §4" pairing |
| Q18 (A then B then C — what is that) | §1 + §7 | ✅ integrative — the outline's "§1 + §7" pairing |
| Q10 (which node component isn't K8s software) | §3 only | ⚠️ single-section; reads integrative but doesn't cross a boundary |
| Q19 (immutability) | Ch 2 only | ⚠️ the link to the control loop lives only in the *explanation*, not in the question |

**Missing: the outline's own top-rated pairing.**

> **§2 + §6** — given a controller's job, name the component that houses it and the loop it runs. *"The single best integrative item in the chapter, and it tests both Fixed Points at once."*

Nothing in the Practice set does this. It is the one item that would force a reader to hold the census and the loop simultaneously, which is precisely the discrimination §7 claims the chapter delivers.

**Recommended addition:**

> **Q20.** 🟡 The Node controller notices when nodes go down and responds. Which component is this controller running inside, and what does "responds" mean in control-loop terms?
>
> A) It runs inside the kubelet on each node; it restarts the node's containers
> B) It runs inside kube-controller-manager; it compares the desired node state against the observed node state and asks the API server to make changes
> C) It runs as its own control-plane component; it instructs the affected node's kubelet directly
> D) It runs inside kube-scheduler; it reschedules the node's Pods itself

This lands the §2 + §6 pairing, re-tests the one-binary-one-process fact from a second angle, and re-tests "controllers ask, they don't act" — all in one item. If the set must stay at 19, it is a straight swap for Practice Q7, which currently tests nothing (see the WARN above).

The §3 + §5 pairing the outline also named ("given a node component, say what it talks to and what it does not") *is* present — but as **Bearings #2 Q4**, not in Practice. That's a reasonable relocation and not a defect; recorded so the outline's list reconciles.

---

## Coverage vs concepts

Checked against `kb_tags.concepts` in the outline frontmatter (42 concepts; `kb_tags.commands` is empty, so there is no command coverage to audit).

| Concept introduced in chapter | Tested in a question? |
|---|---|
| deployment-eras | yes (P Q1) |
| traditional-deployment-era | yes (P Q1) |
| virtualized-deployment-era | **NO** — appears only as distractor P Q1-C |
| container-deployment-era | **NO** — the era's defining fact (shared kernel) is never asked |
| what-kubernetes-provides | yes, weakly (P Q2, as the three wrong options) |
| what-kubernetes-is-not | yes (P Q2) |
| self-healing | **NO** — distractor only (P Q2-A) |
| automatic-bin-packing | **NO** — distractor only (P Q18-D) |
| kubernetes-origin | yes (P Q3; S Q7) |
| borg | yes (P Q3; S Q7) |
| omega | yes (P Q3) |
| helmsman-etymology | **NO** |
| cncf-first-project | **NO** |
| cluster | yes (B1 Q1; S Q3) |
| control-plane | yes (B1 Q1) |
| worker-node | yes (B1 Q1) |
| kube-apiserver | yes (P Q4, P Q6; B2 Q4) |
| etcd | yes (B1 Q4; P Q5) |
| kube-scheduler | yes (B1 Q2; P Q7) |
| kube-controller-manager | yes (B1 Q3) |
| cloud-controller-manager | yes (B2 Q2; P Q13, P Q14) |
| kubelet | yes (B1 Q5; P Q8, P Q9) |
| kube-proxy | yes (B1 Q1; B2 Q1; P Q13, P Q14) |
| container-runtime | yes (B1 Q5; P Q10) |
| addons | yes (B2 Q3; P Q11) |
| cluster-dns | yes (B2 Q3) |
| optional-components | yes (B2 Q1, B2 Q2; P Q13, P Q14) |
| highly-available-control-plane | **NO** — P Q6 covers kube-apiserver horizontal scaling only, not "the control plane usually runs across multiple computers, providing fault tolerance and high availability" |
| api-server-as-front-end | yes (P Q4; B2 Q4) |
| controller | yes (B3 Q2; P Q15) |
| control-loop | yes (B3 Q1; P Q16) |
| reconciliation | yes (B3 Q1, B3 Q4) |
| desired-state | yes (B3 Q1; P Q16) |
| current-state | yes (B3 Q1; P Q16) |
| control-via-api-server | yes (B3 Q3; P Q15, P Q17) |
| direct-control | yes (B3 Q3; P Q17) |
| node-controller | **NO** — named as an example in §2; acceptable |
| job-controller | yes (B3 Q2) |
| endpointslice-controller | **NO** — named as an example in §2; acceptable |
| serviceaccount-controller | **NO** — named as an example in §2; acceptable |
| orchestration-technical-definition | yes (P Q18; S Q8) |
| composable-control-processes | **NO** |

**Coverage: 30 of 42 tested (71%).** Twelve untested, of which three (node-controller, endpointslice-controller, serviceaccount-controller) are documentation examples rather than teaching targets and need no coverage. That leaves **nine genuine gaps**, ranked:

1. **`composable-control-processes` — the most serious.** This is the second half of ★ Fixed Point 3. Practice Q18 asks the reader to name *"first do A, then B, then C"* (orchestration), but no question anywhere asks what Kubernetes offers **instead**. The chapter's culminating Fixed Point is therefore half-assessed: the reader can pass every question while knowing only what Kubernetes rejects, not what it substitutes. Given that §7 is the Zenith and Chapters 6, 15, and 17 all retrieve this shape, this gap is disproportionate to its size.

   **Suggested item** (extends Q18 into a pair, or replaces Q18's positive form):

   > **Q18b.** 🟡 The documentation says Kubernetes eliminates the need for orchestration. What does it say Kubernetes comprises instead?
   >
   > A) A centralized controller that computes an optimal execution order
   > B) A set of independent, composable control processes that continuously drive current state toward desired state
   > C) A workflow engine with pluggable step definitions
   > D) A message bus over which components exchange instructions

   Option D is a particularly good distractor here — it's the mental model §5 spent a whole section dismantling, and no question currently tests whether that dismantling landed.

2. **`container-deployment-era` / `virtualized-deployment-era`.** The era progression is a chapter frame, gets its own figure (`ch03-fig03`), and occupies a Chapter Summary row — but only the traditional era is tested. The proposed retrieval item Q1b covers the container era and closes both gaps at once, since its distractor A forces the virtualized-era contrast.

3. **`highly-available-control-plane`.** "In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault tolerance and high availability" is a sourced, exam-plausible sentence from §2 that no question touches. Practice Q6 tests kube-apiserver's horizontal scaling, which is a different claim about a different scope. Worth one ⚪ item.

4. **`cncf-first-project` and `helmsman-etymology`.** §1 spends a full paragraph on the announcement, v1.0, the CNCF donation, and the name — and Practice Q3 tests only the Borg/Omega/Go half of it. The outline flagged institutional material as historically under-studied by readers; zero questions on the CNCF half is a gap the exam may not forgive. One ⚪ item could carry both (*"Kubernetes was donated to which foundation, and what does the name mean?"*).

5. **`self-healing` and `automatic-bin-packing`.** Both appear only as distractors. Both are named capabilities from the published list, and self-healing in particular is the capability that §1 explicitly connects forward to §6 (*"Self-healing isn't an action; it's a standing condition. Hold that thought. It's the shape of §6."*). A question that cashes that connection would be a strong §1 + §6 interleave and would help the interleaving shortfall above.

**Net recommendation on count:** the chapter is exactly on budget at 40, and the outline's own headroom note (415 questions above the book floor) means adding is cheap. The three additions proposed in this report — Q1b (retrieval + era coverage), Q18b (composable control processes), Q20 (§2 + §6 interleave) — would take Practice to 22, chapter total to 43, close the retrieval shortfall, close the interleaving shortfall, and close the most serious coverage gap. Practice Q7 should be either repaired or dropped regardless, which would net the set to 21.

---

## What passed, and is worth not breaking

Recorded so a revision pass doesn't regress it:

- **Budget compliance is exact** on all four categories — the first chapter in this book to hit every number.
- **Zero missing why-wrong explanations.** Every wrong option in all 32 multiple-choice items has an explanation attached. Two are vague (flagged above); none are absent.
- **Trap fidelity is high where it counts.** All five of B1's `[source]`-tagged traps for this chapter are represented by real, well-built distractors: kube-proxy mandatory (B2 Q1-D), universal CCM (B2 Q2-A), one-process-per-controller (B1 Q3-A), orchestration-as-workflow (P Q18), PaaS (P Q2). Bearings #1 Q5 option C and Bearings #2 Q4 option A are the two best distractors in the chapter — both target the same widespread and genuinely wrong belief that the scheduler instructs the node.
- **The state-reversal trap** (Bearings #3 Q1 option C: desired and current swapped) is exactly the kind of trap the skill asks for — a specific, identifiable misconception that inverts the model rather than a random wrong fact.
- **Bearings #3 as a whole** is the strongest checkpoint: four items, twelve distractors, and every one traceable to a real misconception. It carries the chapter's most important Fixed Point and it earns it.
- **Scope discipline is clean** across all 40 questions — no forward leakage into Chapters 4, 6, 7, 9, or 15, which the outline predicted would be the hardest constraint to hold.
- **Retrieval tagging convention** is applied consistently in both stems and answer keys.
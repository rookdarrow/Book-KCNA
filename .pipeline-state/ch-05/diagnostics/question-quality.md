# Question-Quality Audit — Chapter 5

*Audited artifact: `draft-v1.md` (voiced, 1,195 lines). The stage brief listed `draft-voice.md` as unavailable — the voice stage rewrote in place and preserved `draft-v1-prevoice.md`, so `draft-v1.md` is the voiced draft. Question text is byte-identical between the two files; the voice pass did not touch question architecture.*

## Summary

- Chapter type: **content**
- Total questions inspected: **44**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints, 5 + 5 + 5)
  - Practice questions: **21** (all 4-option multiple choice; 84 option lines / 4 = 21, verified)
- Question budget compliance: **met** — exact match to outline on all three categories
- Weak distractors (WARN): **5**
- Trap answers that don't target real misconceptions (WARN): **0**
- Missing or incomplete why-wrong explanations (FAIL): **4** (+1 borderline WARN)
- Retrieval-practice spacing: **compliant** — 19.4% (7 of 36 Bearings+Practice), against a 20% target
- Soundings spoiler check: **clean** — 0 of 8 reveal a ★ Fixed Point

**Headline.** This is a strong question set. Budget is hit exactly, retrieval lands where the outline planned it, the Soundings does real pre-test work without spoiling anything, and the Q14/Q15 liveness↔readiness mirror is the best-engineered pair in the book so far. Four things need fixing before this ships: two dead distractors in Practice Q3, an incomplete answer key on Practice Q9 (the chapter's highest-value trap), three checkpoint items whose keys never address the likely wrong answer, and the absence of score-band revision prompts on all three Bearings checkpoints.

**One structural note that shapes the whole audit.** Only the 21 Practice questions are multiple choice. All 8 Soundings and all 15 Bearings items are open-response. Distractor analysis is therefore inapplicable to 23 of 44 questions — that is a design choice, not an omission, and a defensible one (open response recruits the generation effect, which is the point of a checkpoint). For those 23 the applicable test is different and I applied it: *does the answer key address the wrong answer the reader was most likely to generate?*

---

## Question-budget compliance

Compared against `question_budget` in the outline frontmatter.

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 15 | 15 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 | 3 | **met** |
| Practice Questions | 21 | 21 | **met** |
| **Chapter total** | **44** | **44** | **met** |

The outline raised Bearings from B4's allocated 10 to 15 under B4's standing "minimums are minimums" sanction (outline § Open questions #10). The draft delivered the raised figure, split 5/5/5 across three checkpoints placed after §3, §5 and §8 exactly as planned. No budget action needed.

Structural checks that ride alongside the budget:

| Check | Result |
|---|---|
| Soundings answers in a `<details>` collapsible | **pass** (lines 65–90) |
| Soundings 6+ / 3–5 / 0–2 reading-strategy rubric | **pass** (lines 84–88), and the 0–2 branch carries the outline's specific "if 7 and 8 were the misses, re-read Ch 4 §2 and Ch 2 §6" instruction |
| ★ Fixed Points present | 5, in §1/§3/§5/§7/§8 as planned |
| Score-band revision prompts on Bearings checkpoints | **fail — 0 of 3** (see § Self-correction gaps) |

---

## Soundings spoiler check

The five ★ Fixed Points this chapter teaches, which the Soundings must not give away:

1. **§1** — the Pod, not the container, is the unit of scheduling; one IP per Pod, shared by all containers, which reach each other over `localhost`.
2. **§3** — init containers run in declared order, to successful completion, all of them, before any app container starts.
3. **§5** — phase is Pod-scoped, state is per-container, and `Running` does not mean working.
4. **§7** — liveness kills; readiness de-registers; a configured startup probe suppresses both.
5. **§8** — requests are what the scheduler reads, limits are what the kubelet enforces; CPU limits throttle, memory limits kill.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Network reachability; what changes on one machine | **no** | Stem is provider-neutral ("two processes… over the network"). The key names `localhost` and "they share one network stack" — but as the *general* networking prior, not the Kubernetes claim. FP #1's content is that Kubernetes *chose* to hand a shared namespace to a container group and made that group schedulable. Untouched. |
| 2 | Shared filesystem path between two programs | **no** | Generic bind-mount/shared-directory prior. Names no Kubernetes object. |
| 3 | Enforcing ordering before a service accepts traffic | **no** | Stem explicitly scaffolds from entrypoint scripts, systemd, CI stages. Never names init containers, ordering-to-completion, or the all-must-succeed rule that is FP #2. |
| 4 | "Running" vs "can do its job" | **no** | Surfaces the *problem* §7 solves without naming probes, types, or failure behaviors. This is the strongest pre-test in the set — it makes the reader notice the gap FP #4 then fills. |
| 5 | Load balancer with a failing backend — and what it does *not* do | **no** | Primes readiness's de-register-don't-kill behavior as a *prior from another system*. FP #4 is that Kubernetes has three probes and that readiness specifically behaves this way; neither is revealed. |
| 6 | Reserving capacity vs capping it | **no** | Generic ("a JVM heap, a cgroup, a cloud instance type"). FP #5's content — *which component* reads which, and that CPU throttles while memory kills — is entirely absent from stem and key. |
| 7 | **[retrieval: ch4]** `spec` / `status`; which reports what is true | **no** | Ch 4 material the reader already owns. FP #3 is the phase/state scope split; retrieving `spec`/`status` is its setup, not its payoff. |
| 8 | **[retrieval: ch2]** `ImagePullBackOff` and what Ch 2 said it is reported *as* | **no — but the closest call in the set** | The expected answer is "a container in the **Waiting** state," which does surface one member of the three-state vocabulary. It clears the bar because (a) Chapter 2 line 783 already published this to the reader — the question retrieves what they were *told*, it does not teach; and (b) FP #3's claim is the *scope distinction* plus the `Running`-isn't-working corollary, and knowing one state name yields neither. The outline anticipated exactly this ("retrieving one instance does not give the taxonomy") and the draft honored the reasoning. |

**Verdict: clean.** No question stem, distractor, or answer discloses a Fixed Point. Six questions test priors the reader arrives with and two retrieve published earlier material — the 6/2 split the outline specified.

---

## Per-question findings

### P3: "A team proposes a Pod containing an API server, a Redis cache, and a PostgreSQL database… What is the strongest technical objection?"

**Issue:** Two of the three distractors target no misconception at all. This is effectively a two-option question, and the answer key admits it.

**Distractor analysis:**
- A) *A Pod can hold at most two containers* — **implausible.** No documented misconception, and no candidate who has read §2 (which discusses multi-container Pods without any cap) could hold it. The key's own rebuttal is "*A* is false; there's no such cap" — a why-wrong that reduces to "it is untrue" is the diagnostic signature of a distractor targeting nothing.
- B) *The three would need three separate IP addresses* — **plausible.** Targets trap #36 (per-container IPs). Keep.
- C) *They would scale, fail, and be replaced as a single unit* — correct.
- D) *PostgreSQL cannot run in a container* — **implausible.** Containerized databases are ubiquitous; this is not a belief anyone brings to a KCNA attempt. Key: "*D* is simply untrue."

**Why-wrong explanation status:** present but necessarily vague for A and D, because there is nothing to explain.

**Recommended fix:** replace A and D with objections that are wrong for *instructive* reasons. Two candidates, both drawn from misconceptions this chapter actually corrects:
- *"They would have to share a single `restartPolicy`"* — true, and genuinely tempting as "the strongest objection," but weaker than shared fate; it also quietly rehearses trap #8 (Pod-level restartPolicy) as a correct fact.
- *"Each would need its own readiness probe, and a Pod can only have one"* — false in the second clause, and it targets a real scope confusion (probes are per-container; the reader who has over-generalized "everything in a Pod is Pod-level" from §5 will bite).

### P9: "A Pod's single container crashes and restarts every twenty seconds. What phase does the Pod report?"

**Issue:** Incomplete answer key on the chapter's single highest-value trap. Two of three wrong options get no treatment.

**Distractor analysis:**
- A) `Failed` — plausible and well-chosen; explained in the key.
- B) `Pending` — plausible (a reader may think a container that never stays up has never "come up"). **Unexplained.**
- C) `Unknown` — plausible for a reader who reads `Unknown` as "the system is confused about this Pod." **Unexplained.**
- D) `Running` — correct.

**Why-wrong explanation status:** **present but incomplete.** Only option A is addressed. Per skill Part 11 and the Ethical Checkpoint, every wrong option needs a rebuttal — and this question is the one the chapter has been building toward since §5, so a partial key here costs more than it would anywhere else.

**Recommended fix:** add two sentences. For B: `Pending` ends once the Pod is bound to a node and all containers have been *created* — this container has been created repeatedly, so the Pod left `Pending` on the first attempt. For C: `Unknown` reports the control plane's inability to *obtain* state, not the application's inability to stay up; the node here is reporting fine, and what it is reporting is a crash loop. (The P15 key already has a clean one-line gloss of `Unknown` — reuse the phrasing for consistency.)

### P6: "A node fails while running a Pod. What happens to that Pod?"

**Issue:** One dead distractor.

**Distractor analysis:**
- A) *Scheduler moves it to a healthy node, preserving its UID* — **strong.** This is trap #9 exactly. Keep.
- B) correct.
- C) *It remains in phase `Running` until the node returns* — **plausible.** Good: it tempts a reader who has over-learned "`Running` is sticky" from §5's hazards block.
- D) *It is automatically converted into a DaemonSet Pod* — **implausible.** Key: "*D* invents a conversion that doesn't exist." Nobody believes Pods change kind.

**Why-wrong explanation status:** present and specific for A and C.

**Recommended fix:** swap D for *"It is recreated on the same node once the node recovers, with the same UID"* — which targets the residual half of trap #9 (that the *object* persists in some form) and forces the UID fact to do work.

### P16: "A container's startup probe is configured and has not yet succeeded. What is true of its liveness and readiness probes during that window?"

**Issue:** One arbitrary distractor.

**Distractor analysis:**
- A) *They run normally alongside the startup probe* — **strong.** This is trap #11, the assumption the section exists to break. Keep.
- B) *They run, but their failures are logged rather than acted on* — **plausible.** A well-chosen softened-behavior option; a reader who half-remembers "suppressed" may land here.
- C) correct.
- D) *They run at half their configured `periodSeconds`* — **implausible.** Arbitrary and oddly specific; no mental model produces it.

**Why-wrong explanation status:** present, though B and D are lumped ("*B* and *D* invent softened behaviors"). Fine for B; vacuous for D.

**Recommended fix:** replace D with *"They are disabled, and remain disabled for the container's lifetime"* — a genuine over-correction of the correct answer that tests whether the reader knows suppression *ends* on success. It also closes a small teaching gap: the draft states suppression begins but never explicitly tests that it lifts.

### P4: "A Pod declares two init containers and two app containers. Which statement correctly describes the startup order?"

**Issue:** One weak distractor. Lower severity than the above — flagging for completeness, not blocking.

**Distractor analysis:**
- A) *All four start in parallel* — plausible for a reader who has not internalized §3.
- B) *Init containers in parallel, then app containers in parallel* — **the strongest distractor in the set.** This is the precise error the ordering guarantee exists to prevent.
- C) correct.
- D) *The init containers run after the app containers, to perform cleanup* — **weak.** The word "init" forecloses it, and no misconception points this way.

**Why-wrong explanation status:** present. A and B handled well together; D gets "*D* inverts the sequence."

**Recommended fix:** optional. If touched, swap D for *"The init containers run in parallel with the app containers, and the Pod is Ready when all four are running"* — which pairs the parallelism error with a readiness error and interleaves §3 with §7.

### B1.2: "Someone proposes putting a web server and its database in a single Pod… Give the strongest argument against, in one sentence."

**Issue:** The key gives the correct answer and a "weaker but still correct" alternative, but never addresses a wrong answer.

**Why-wrong explanation status:** **missing.** The likely wrong generations are specific and worth catching: *"they'd collide on ports"* (true of some pairs, but incidental, and it teaches the wrong test), and *"a Pod should only run one process"* (a Docker-era doctrine that §2 explicitly does not endorse — §2's test is coupling, not process count).

**Recommended fix:** add two sentences after the "weaker but still correct" paragraph rejecting the port-collision answer as incidental rather than structural, and rejecting one-process-per-Pod as the wrong rule — §2's test is whether `localhost` or a shared volume is *needed*, not how many processes are involved.

### B1.5: "**[retrieval: ch3]** …what object is the kubelet reading, and what is it comparing that object against?"

**Issue:** The checkpoint's hardest item by the outline's own design, and its key contains no misconception handling.

**Why-wrong explanation status:** **missing.** Two wrong answers are highly likely here and both matter downstream: *"it reads the Deployment"* (which nothing in the book has yet ruled out, and which Chapter 6 will need corrected), and *"it compares the spec against etcd"* (the direct kubelet↔etcd error that Practice Q21's key rebuts thoroughly for the Practice reader but not for the checkpoint reader who never reaches Q21 with the question in mind).

**Recommended fix:** add a short why-wrong block naming both. The etcd rebuttal already exists verbatim in the P21 key (hub-and-spoke; the kubelet never talks to etcd) — pull it forward. This item is 260 lines earlier than P21 and is where the reader first forms the model.

### B2.4: "**[retrieval: ch2]** …give the Pod's phase, the container's state, and the field on the container status that tells you which specific failure it is."

**Issue:** No misconception handling on the item most likely to produce the chapter's signature error. **This is the most consequential of the three checkpoint gaps.**

**Why-wrong explanation status:** **missing.** The question asks for three values, which makes one specific wrong answer near-inevitable: naming `ImagePullBackOff` as the container **state**. That is precisely the Reason-vs-state conflation the whole §5 apparatus targets, and a reader who makes it will read their own answer as correct because the right string appears in it. Second likely miss: giving the phase as `Running` on the reasoning that the Pod exists and the kubelet is actively working on it.

**Recommended fix:** add a why-wrong block:
- *"State: `ImagePullBackOff`"* — `ImagePullBackOff` is a **`Reason`**, not a state. The three container states are `Waiting`, `Running`, `Terminated`, and nothing else is ever one of them. If you wrote the right string in the wrong slot, you have the fact and not yet the taxonomy — and that is the exact error §5's hazards block is about.
- *"Phase: `Running`"* — `Running` requires all containers to have been *created*. This one never was.

### P17: "Which statement about probe mechanisms is correct?"

**Issue:** Borderline (WARN, not FAIL). The three wrong options are the same error three times, and the key rebuts them in one lumped sentence.

**Distractor analysis:**
- A) liveness must `httpGet` / readiness must `exec`; C) only startup supports `tcpSocket`; D) `grpc` only for readiness — each is a different type↔mechanism pairing, so they are not duplicate-meaning, but they are structurally identical and a reader who rejects one rejects all three at once. That collapses the question's discrimination.
- B) correct.

**Why-wrong explanation status:** present but undifferentiated — "*A*, *C*, and *D* each invent a constraint pairing a type to a mechanism."

**Recommended fix:** low priority. If revised, make one distractor a *different* error class — e.g. *"`exec` probes run in a sidecar container, not the probed container"* — so the question tests two things instead of one.

---

## Trap fidelity

**0 findings.** Every distractor that the answer keys present as a documented misconception is one. The seven traps the Exam Alert claims (phase-vs-state, `Running` oversold, per-container `restartPolicy`, rescheduled-not-replaced, liveness≡readiness, startup-probe suppression, per-container IP) all trace to the B1 inventory's `[source]`-tagged D1 entries, and each has a matching Practice distractor that genuinely embodies it:

| Trap | Carried by |
|---|---|
| Phase vs container state | P7-A (`Waiting` offered as a phase — the cleanest instance in the chapter), P9 |
| `Running` means working | P9 |
| `restartPolicy` per-container | P10-A, P10-D |
| Failed Pod is rescheduled | P6-A |
| Liveness ≡ readiness | P14-D, P15-A |
| Startup probe doesn't suppress | P16-A |
| Per-container IP | P1-A, P3-B |
| `m` vs `M` memory suffix (non-B1, documentation-flagged) | P19 |

Notably, the keys are *honest* about their weak options — they say "invents," "is simply untrue," "is false" rather than dressing a filler distractor as a common mistake. That honesty is why the fidelity count is 0 while the weak-distractor count is 5: the problem is dead options, not mislabeled ones. Also clean: no distractor anywhere is supported by a fabricated frequency statistic, which the outline flagged as a Part 14 guardrail.

---

## Self-correction gaps (skill Part 11 / Part 13)

**No Bearings checkpoint carries a score-band revision prompt.** All three end with a "Checkpoint: You've Now Mastered" progress block (lines 308, 518, 799) and nothing else. Grep confirms score bands appear only in the Soundings (lines 84–88).

The skill requires the reverse: Part 11 specifies "If You Scored 0-2 / 3-4" revision prompts with a named section to re-read, Part 13 specifies micro-progress bands after checkpoints, and the Ethical Checkpoint lists "Revision prompts included for low checkpoint scores." Chapters 2–4 should be checked for the same omission before this is treated as a Chapter 5 defect — if it is a book-wide pattern it is a contract question, not a draft question.

Partially mitigating: three individual items embed targeted remediation (B1.1 — "stop and re-read §1 before continuing"; B2.3 — struggle normalization per Part 10B; the Soundings 0–2 branch names Ch 4 §2 and Ch 2 §6). So the *instinct* is present; the mechanism is not.

**Recommended fix:** three short rubrics, each naming the specific section to revisit — B1 → §1's shared-context subsection; B2 → §5's three movements, with the explicit note that §7 and §8 both assume the phase/state split; B3 → §7's failure-behavior table and §8's movement two. B2's matters most: it gates the two densest sections that follow.

*Scope note: revision prompts are adjacent to my six named dimensions rather than inside them. Reported here because they are the self-correction half of the why-wrong architecture I do own, and because the fix belongs in the same editing pass. Route to structural lint if this is contract-enforced.*

---

## Retrieval-practice spacing

- Chapter 5 target: **20%** of checkpoint questions from earlier chapters, drawn from Ch 2–4 (arc outline **[B3]**; the outline resolved the B4-vs-B3 conflict in favor of 20% — see outline § Open questions #8).
- Actual: **19.4%** — 7 of 36 Bearings + Practice questions carry a `[retrieval: chN]` tag.
- Status: **compliant.**

| Location | Tagged items | Rate |
|---|---|---|
| ☆ Bearings (15) | B1.5 `[ch3]`, B2.4 `[ch2]`, B2.5 `[ch4]` | 3/15 = 20.0% |
| Practice (21) | P5 `[ch4]`, P13 `[ch4]`, P20 `[ch2]`, P21 `[ch3]` | 4/21 = 19.0% |
| **Combined** | **7** | **19.4%** |
| 🧭 Soundings (outside the budget) | S7 `[ch4]`, S8 `[ch2]` | bonus |

All three of B3's named anchors landed in the section the outline specified:

| **[B3]** named anchor | Planned placement | Actual | Status |
|---|---|---|---|
| `imagePullPolicy` (Ch 2) as a cause of a container state | Bearings #2, item 4 | B2.4 | **as planned** |
| `spec`/`status` (Ch 4) read against Pod phase | Bearings #2, item 5 | B2.5 | **as planned** |
| Labels (Ch 4) on a Pod | Practice, §1–§3 block | P5 | **as planned** |

The remaining three Practice retrievals also match the outline's allocation exactly: service-account-token Secret in the §6 block (P13), image immutability in the §8 block (P20), control loop in the §8 block (P21). Source chapters are well spread — Ch 2 ×2, Ch 3 ×2, Ch 4 ×3 — and Chapter 1 is correctly excluded per B3.

Bearings #2's 40% internal concentration is intentional and defensible: both `[B3]` anchors require §5's vocabulary and belong nowhere else. The chapter-level rate is what governs, and it is on target.

**No additions needed.**

---

## Interleaving

The Practice preamble claims: *"five require two sections of this chapter at once."* The set does not support that claim.

| Outline-planned interleaving | Present in Practice? |
|---|---|
| Probe + `restartPolicy` (§7 + §5) | **weak** — P15's correct answer mentions restart policy, but no §5 reasoning is required to select it |
| Phase + init container (§5 + §3) | **absent** |
| Limit + container state (§8 + §5) | **absent from Practice** — delivered as B3.5 instead, in a checkpoint |
| Multi-container + phase (§2 + §5) | **absent** |
| Identity + namespace (§6 + Ch 4) | **present** — P12 |

Genuinely cross-scope Practice items: P12, P20, P21, and P10 (only via option C, which requires knowing init containers obey the Pod's `restartPolicy`). Of those, P20 and P21 are cross-*chapter* retrieval rather than cross-*section* interleaving — they are already counted under the retrieval budget and shouldn't be double-credited.

This matters because interleaving is what builds discrimination (skill Part 10), and the outline's calibration note asked specifically for behavioral, multi-section questions on the grounds that "KCNA tests recognition of *situations*, not vocabulary lists." The set is currently strong on single-section behavioral prediction and thin on cross-section synthesis.

**Recommended fix:** convert two existing single-section items rather than adding questions (the budget is exact and shouldn't drift). The two absent interleavings are both cheap to build and both close coverage gaps identified below:
- **Phase + init container** — replace or extend P4: *"A Pod's second of three init containers has been failing for ten minutes. What phase does the Pod report?"* Correct: `Pending` (accepted, containers not yet set up). This tests §3 and §5 together and gives `phase-pending` a second, harder appearance.
- **Multi-container + phase** — a new stem for P3's slot or an added variant: *"A Pod has three containers. One has terminated successfully; the other two are running. What phase does the Pod report?"* Correct: `Running`. Distractors: `Succeeded` (requires **all** containers terminated — a genuine and untested misconception), `Failed`, `Unknown`. This is the single highest-value edit available: it interleaves §2 and §5, and it is the only realistic way to test `phase-succeeded`, which is currently never tested at all.

---

## Coverage vs concepts

Checked against `kb_tags.concepts` in the outline frontmatter (65 concepts). Question IDs: **S**n = Soundings, **B**c.n = Bearings checkpoint c item n, **P**n = Practice.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| **§1** | |
| `pod` | yes (B1.1, P1, P3) |
| `smallest-deployable-unit` | **NO** — see note below |
| `co-located-co-scheduled` | partial (P3 tests shared fate; the co-scheduling guarantee itself is never the subject) |
| `pod-shared-context` | yes (P2) |
| `pod-network-namespace` | yes (P1, P2) |
| `pod-ip` | yes (B1.1, P1) |
| `localhost-communication` | yes (B1.1, P2) |
| `pod-shared-volumes` | yes (P2) |
| `podspec` | yes (B1.5, P21) |
| **§2** | |
| `single-container-pod` | **NO** — §2's default-to-one-container rule is taught and never tested |
| `multi-container-pod` | yes (P2, P3) |
| `sidecar-container` | **NO** — defined with three worked examples in §2, tested nowhere |
| **§3** | |
| `init-container` | yes (B1.3, B1.4, P4) |
| `init-container-ordering` | yes (B1.4, P4) |
| `run-to-completion` | yes (B1.4, P4) |
| **§4** | |
| `pod-lifetime` | yes (P6) |
| `pod-ephemerality` | yes (P6, P20) |
| `pod-uid` | yes (P6, P20) |
| `scheduled-once` | yes (P6) |
| `pod-replacement` | yes (P6, P20) |
| `pod-eviction` | **NO** |
| `pod-termination` | partial (B3.5 reaches the container `Terminated` state; Pod-level termination/deletion is untested) |
| **§5** | |
| `pod-phase` | yes (B2.1, B2.4, P7, P9) |
| `phase-pending` | yes (B2.4, P7) |
| `phase-running` | yes (B2.1, P9) |
| `phase-succeeded` | **NO** |
| `phase-failed` | partial (P9 distractor A only; the key does gloss its definition) |
| `phase-unknown` | partial (P9-C, P15-C distractors; defined in the P15 key, never a correct answer) |
| `container-state` | yes (B2.1, B2.4, P8) |
| `state-waiting` | yes (B2.4, P7-A, P8) |
| `state-running` | yes (B2.1, B3.5) |
| `state-terminated` | yes (B3.5) |
| `restart-policy` | yes (B2.2, P10) |
| `restart-backoff` | yes (B2.3, P11) |
| `backoff-reset` | yes (B2.3, P11) |
| **§6** | |
| `serviceaccount` | yes (B3.1, P12) |
| `default-serviceaccount` | yes (B3.1, P12) |
| `serviceaccount-name` | yes (P12 stem) |
| `tokenrequest` | yes (P13) |
| `projected-token-volume` | partial (named in the P13 key, not in any stem or option) |
| `workload-identity` | yes (B3.1) |
| **§7** | |
| `probe` | yes (P14–P18) |
| `liveness-probe` | yes (B3.2, P15) |
| `readiness-probe` | yes (B3.2, P14) |
| `startup-probe` | yes (B3.3, P16) |
| `probe-exec` | yes (P17) |
| `probe-httpget` | yes (P17, P18) |
| `probe-tcpsocket` | yes (P17, P18 key) |
| `probe-grpc` | yes (P17) |
| `probe-parameters` | partial (`failureThreshold` in P15-D, `successThreshold` in P18-D — distractors only) |
| **§8** | |
| `resource-request` | yes (B3.4, B3.5) |
| `resource-limit` | yes (B3.4, B3.5) |
| `cpu-unit` | **NO** — 1 cpu = 1 core, `0.1` = `100m`, `1m` floor: all taught, none tested |
| `millicpu` | partial (P19-D distractor and key) |
| `memory-units` | yes (P19) |
| `cpu-throttling` | yes (B3.5) |
| `oom-kill` | yes (B3.5) |
| `ephemeral-storage` | **NO** |
| `hugepages` | **NO** |
| `extended-resources` | **NO** |
| `qos-class` | **NO** — blocked, see below |
| `qos-guaranteed` | **NO** — blocked |
| `qos-burstable` | **NO** — blocked |
| `qos-besteffort` | **NO** — blocked |

**Tagged in the outline but not taught in the draft — correctly, so not testable:**

| Tag | Why |
|---|---|
| `pod-template` | Deferred to Ch 6 by design; appears in the draft only as a forward pointer in The Voyage Ahead |
| `kubectl-get`, `kubectl-describe`, `kubectl-explain` | The draft deliberately teaches no `kubectl` (§5: "What this section deliberately does not do is tell you what to *run*"), holding the published Ch 13 boundary. **These three tags should be dropped from the Ch 5 `kb_tags.commands` list** — they promise coverage the chapter is contractually forbidden to deliver. |

### Notes on the significant gaps

**`smallest-deployable-unit` — the chapter's own headline claim is never the subject of a question.** Fixed Point #1's first clause ("the **Pod**, not the container, is the unit of scheduling") is tested only through its consequences: P1 tests the IP, P3 tests shared fate, P4 tests init ordering. No question anywhere asks what Kubernetes actually schedules. There is a real argument that consequence-testing is the better pedagogy — the outline's own calibration note says so, and the Zenith's whole structure is "seven consequences of one decision." But a reader can currently answer every one of the 44 questions correctly while still privately believing Kubernetes schedules containers that happen to be grouped. Per Rule 5, that encoding is never confirmed. **Recommended:** fold the claim into the P3 replacement distractor or add it as a clause to P1's stem; it does not need its own slot.

**`sidecar-container`** — the word is introduced, defined, given three examples, and pointed forward to Ch 17. Zero questions. The reader will meet this term constantly and has no retrieval hook for it. Cheapest fix: rewrite P2's stem to name the pattern — *"A logging sidecar must read files the application writes. Which two mechanisms does the Pod's shared context make available?"* — which tests the same content and anchors the term at no budget cost.

**`phase-succeeded`** — never appears as a correct answer or an explained distractor. The multi-container interleaving question proposed above is the natural home: `Succeeded` requires **all** containers terminated successfully, and that "all" is exactly the kind of quantifier candidates drop.

**`cpu-unit`** — §8 teaches three testable facts (1 cpu = 1 core; `0.1` ≡ `100m`; no precision finer than `1m`) plus the absoluteness property in a 🔭 Closer Look, and P19 tests only the memory suffix. Given that the `m`/`M` trap turns on the reader knowing `m` is *correct* for CPU, the CPU half is load-bearing for the question that already exists. **Recommended:** extend P19's key, or convert one §8 slot.

**`ephemeral-storage`, `hugepages`, `extended-resources`** — introduced in the §8 resource-types table and untested. Low severity: they are enumeration items, not mechanisms, and the outline banded §8 as already the chapter's densest section. Acceptable to leave, but worth one Chapter Summary line if not tested.

**QoS classes — untested because untaught, and correctly so.** §8's movement four states only that the class exists and is derived from how requests and limits were filled in; the three class definitions, derivation rules, and eviction-ordering consequences are absent behind an `AUTHOR-REVIEW` block flagging the blocking source gap (outline § Open questions #2 — `pod-qos/` was never fetched). The draft was right not to write questions on material it could not source. **Downstream consequence for this stage:** once the research fetch lands and movement four is written, this chapter will need **2–3 additional Practice questions** on QoS, which will push the chapter total from 44 to 46–47. That is above the outline's `question_budget`, so either the budget is revised at the same time or two of the weak items identified above are cut to make room. Flagging now because the QoS material is also the lower half of `ch05-fig05`, the chapter's most-retrieved figure, and Ch 13's eviction material assumes it.

---

## What is working

Recorded so a revision pass doesn't damage it.

- **P14 / P15 are a deliberate mirror** — same four consequence-options, liveness and readiness swapped — and the key says so ("deliberately mirrored, because reversing them is the single most common probe error"). This is the best-engineered pair in the chapter and possibly the book.
- **P7 offers `Waiting` as a Pod phase.** A one-word distractor that is a category error, targeting the chapter's central distinction. The key handles it exactly right: the container in the scenario genuinely *is* `Waiting`, so the reader who picks it isn't ignorant, they're reading at the wrong scope.
- **P19 and P21** are near-perfect four-option sets — every wrong answer traceable to a specific, real, differently-shaped error.
- **B2.1's key distinguishes two misconceptions that produce the same answer** ("Yes, because a Pod can't be Running…" vs "No, because `Running` means the application is working"). Getting the right answer for the wrong reason is invisible to most assessment designs; catching it here is exactly the self-correction the skill's Part 11 asks for.
- **B2.3 is labeled as a challenge item and normalized in the key** ("Both outcomes are fine here; the struggle is doing the encoding work") — Part 10B desirable-difficulty compliance, done properly.
- **Soundings 4, 5 and 6 are phrased as situations, not definitions**, as the outline required. Each surfaces a *problem* the chapter later solves, which is the pretesting effect working as designed rather than a vocabulary quiz wearing a diagnostic's clothes.

---

## Recommended action list, in priority order

| # | Item | Severity | Fix cost |
|---|---|---|---|
| 1 | P9 — complete the answer key for options B and C | **FAIL** | 2 sentences |
| 2 | B2.4 — add why-wrong for the `ImagePullBackOff`-as-state conflation | **FAIL** | 3 sentences |
| 3 | P3 — replace dead distractors A and D | **WARN** | 2 options |
| 4 | B1.5 — add why-wrong (Deployment; etcd), reusing P21's phrasing | **FAIL** | 2 sentences |
| 5 | Bearings ×3 — add score-band revision prompts | **WARN** (adjacent) | 3 short blocks; check Ch 2–4 first |
| 6 | Interleaving — build the phase+init and multi-container+phase items; this also closes `phase-succeeded` | **WARN** | 2 stem rewrites |
| 7 | B1.2 — add why-wrong (port collision; one-process-per-Pod) | **FAIL** | 2 sentences |
| 8 | P6-D, P16-D — replace arbitrary distractors | **WARN** | 2 options |
| 9 | P2 — rename the stem to anchor `sidecar-container` | **WARN** | 1 stem edit |
| 10 | `kb_tags.commands` — drop the three `kubectl-*` tags from the Ch 5 outline | note | outline edit |
| 11 | P4-D, P17 A/C/D — optional distractor strengthening | note | discretionary |

Items 1, 2, 4 and 7 are the four FAIL-grade why-wrong gaps counted in the summary. None requires new questions; all four are additive edits to existing answer keys, and the budget stays at exactly 44.
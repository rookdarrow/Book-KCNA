I've verified the chapter against all twelve shipped chapters. Here is the stage output.

```markdown
# Integration Check — KCNA Chapter 13

## Summary

- Terminology consistency: **pass**
- Callbacks to earlier chapters: **9 correct / 3 incorrect**
- Retrieval-practice accuracy: **pass** (4 tagged items, 4 aligned)
- Glossary coverage: **26 concepts introduced, 24 defined in the chapter, 14 require glossary entries** (4 also require a term-ledger row)
- Contradictions with earlier canon: **2 flagged** (1 substantive, 1 advisory)
- Ethical guardrails (skill Part 14): **pass** (2 advisories)

Chapters 1–12 are all shipped and were read directly; this check is against
the files, not against the contracts alone. Cross-bearings were verified
mechanically against the B6 skeleton. **48 cross-bearings emitted, 48 resolve.**

The chapter's own AUTHOR-REVIEW comments are unusually disciplined and most of
them are correct. Two are now answerable from shipped text and should be closed
rather than routed to Stage 2 — see *Recommended fixes* 3 and 4.

## Terminology consistency

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| Pod / pod | `Pod` capitalized; lowercase only in `pod networking` and quotations | ~180 | No — lowercase uses are all inside verbatim k8s quotations or the sanctioned "pod networking" |
| kubectl | lowercase, code style, never sentence-initial bare | ~60 | No |
| etcd | lowercase always | 2 | No |
| crictl | lowercase, code style | 14 | No |
| containerd / CRI-O | `containerd`, `CRI-O` exact | 1 each (figure) | No |
| node controller | lowercase, two words | 9 | No — no `Node controller`, no "node lifecycle controller" |
| control plane | bare = the cluster's (Ch 3 §2) | 4 | No — no mesh sense present |
| metrics-server | `metrics-server` | 14 | No — the one `Metrics Server` is inside a verbatim doc quotation |
| kubelet | lowercase | ~45 | No — the one `Kubelet` is inside the cAdvisor quotation |
| endpoints | lowercase = backend addresses; `Endpoints` reserved and unused | 6 | No — correctly avoids the capitalized legacy object (ledger orphan) |
| Secret / secret | `Secret` for the object; "image pull secret" lowercase | 12 | No |
| Ingress | capitalized for object and controller | 4 | No |
| request | "resource request" near API-server sentences | 11 | No — homonym rule observed |
| namespace | Kubernetes sense only | 6 | No — no Linux-namespace sense present |
| PodDisruptionBudget | barred from explanatory/graded text (ledger ⚑3) | 1 | **No — compliant.** Sole use is inside a verbatim quotation of what the kubelet does *not* respect, and the draft flags it. Correct handling. |
| "the object exists; nothing happens without the component" | skeleton form uses a semicolon | 2 | **No in this chapter** — but see the book-level note below |

**Book-level surface-form drift (not a Ch 13 defect).** The named pattern now has
three forms in shipped text: Ch 6:1082 *"the object exists **but** nothing happens
without the component"*; Ch 11:815/1305 *"the object exists; the component does not;
nothing happens"*; and the skeleton/Ch 13 form *"the object exists; nothing happens
without the component."* The ledger says this phrase is "retrieved **by name**," so
the variants defeat the mechanism. **Ch 13 conforms to the skeleton; Ch 6 and Ch 11
are the outliers.** Cosmetic sweep, author's call — no change here.

**Acronym register.** `VPA` reaches this chapter inside a quotation. It is *not* a
first appearance — shipped Ch 3:606 and Ch 10:678 both use it, both with a pointer
to Ch 17 — but it is **unexpanded everywhere in the book**, which violates the
ledger's "every acronym is expanded on its first use, without exception." The fix
belongs at Ch 3:606, not here. The ledger's `First appears: Ch 17 §7 †` row is wrong
and should be corrected to Ch 3.

## Callback correctness

Every prose claim this chapter makes about an earlier chapter, checked against the file.

| # | Claim in Ch 13 | Target | Verdict |
|---|---|---|---|
| 1 | §2: Ch 12 said admission refusal "shows up at a different point in the triage flow" | Ch 12:1340 | ✓ verbatim |
| 2 | §2: "the point Chapter 7 made" — nothing retries Pending with relaxed constraints | Ch 7:426 | ✓ exact |
| 3 | §2: "Chapter 12 pointed a reader here" — Pod referencing a missing Secret | Ch 12:1099 | ✓ exact |
| 4 | §3: "Chapter 6 left you a specific promise here" | Ch 6:663 + Ch 6:778 | ✗ **broken — see fix 1** |
| 5 | §3: "Chapter 5 handed this case to this section by name" (`-c`) | Ch 5:392 | ✓ exact, pins Ch 13 §3 |
| 6 | §5: "You met the node conditions in Chapter 8" | Ch 8:690 | ✓ |
| 7 | §5: "Chapter 3 promised you this framing" (crictl below the API) | Ch 3:451, Ch 3:645–649 | ✓ |
| 8 | §6: Ch 8 said skew returns "in a form where you have to use it rather than recite it" | Ch 8:923 | ✓ verbatim |
| 9 | §7 + Soundings A8: "Chapter 10 named it so you could reuse it" | Ch 6:1082 / Ch 10 §3, §8 | ⚠ **misattributed — see fix 6** |
| 10 | §2: unbound PVC belongs to this family | Ch 11:588 | ✗ **promise unmet — see fix 2** |
| 11 | §8: Pending as an unconverged control loop | Ch 3 §6 | ✓ |
| 12 | §1/§8: the Ch 16 handoff | Skeleton Ch 16 §1 | ✓ (Ch 16 undrafted; skeleton is the authority) |

**Inbound pointers.** Shipped text aims **18** pointers at this chapter. **16 land.**
The two that miss are #4 and #10 above. All §-pinned inbound pointers
(Ch 5:392 → §3, Ch 5:1027 → §4, Ch 8:923 → §6, Ch 10:677 → §7, Ch 11:588 → §2,
Ch 12:1099/1340 → §2, Ch 3:451 → §5, Ch 6:778 → §3) resolve to the right section.

Ch 3:649 ("the debugging commands that ride those outbound paths" — logs, attach,
port-forward) is **partially** answered: `kubectl logs` lands in §3, and §1 explicitly
routes `exec`/`port-forward` to Ch 16 §3 and §5. Signposted, so it resolves. No action.

## Retrieval-practice accuracy

| Item | Tag | Topic | Owner per ledger | Verdict |
|---|---|---|---|---|
| TYB 1 Q6 | `[retrieval: ch2]` | tags vs digests, immutability | Ch 2 §3 | ✓ |
| TYB 2 Q6 | `[retrieval: ch5]` | `Guaranteed` QoS criteria | Ch 5 §8 | ✓ |
| TYB 3 Q2 | `[retrieval: ch8]` | kubelet skew, 1.37 / 1.33 | Ch 8 §6 | ✓ |
| TYB 3 Q3 | `[retrieval: ch10]` | object-exists-without-component | Ch 10 §3 | ✓ (same attribution caveat as callback #9) |

4 of 17 checkpoint questions are retrieval — **23.5%**, inside the skill's 20–25% band
for chapters 6+. Practice adds 3 interleaved items (Q2 D1.3, Q8 D1.1, Q9 D2.2).
Question budget: Soundings 8 (content chapter ✓), Bearings 17 across 3 checkpoints
of ≥5 (✓ ≥10 across ≥2), Practice 16. Total 41.

## Glossary coverage

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| Platform scope vs application scope | yes | yes |
| Triage order (S-P-C-E-L) | yes | no |
| `ErrImagePull` | yes | yes |
| `ImagePullBackOff` (diagnosis) | yes | yes |
| `ImageInspectError` | yes | yes |
| `ErrImageNeverPull` | yes | yes |
| `CreateContainerConfigError` | yes | yes |
| `PodInitializing` | yes | no |
| `CrashLoopBackOff` | yes | yes |
| `OOMKilled` (signature) | yes | yes |
| `Evicted` / node-pressure eviction | yes | yes |
| API-initiated eviction | yes (by contrast) | yes |
| Event (the object) | yes | yes |
| Event retention window / `--event-ttl` | yes | yes |
| `kubectl events` | yes | no |
| `kubectl logs --previous` / `-c` / `--all-containers` | yes | no |
| `kubectl config current-context` | yes | no |
| `crictl`, `crictl ps`, `crictl logs` | yes | yes |
| `--runtime-endpoint` / `/etc/crictl.yaml` | yes | no |
| Resource metrics pipeline | yes | yes |
| **cAdvisor** | yes | **yes — also needs a ledger row (new to the book)** |
| **Metrics API** | yes | **yes — also needs a ledger row (new, and in graded text)** |
| metrics-server / `kubectl top` | yes | yes |
| Cluster-level logging | yes | yes |
| Node-level logging agent | gloss + pointer only | no — Ch 18 §6 owns it (correct) |
| **static Pod / mirror Pod** | **only inside a graded answer key** | **yes — see fix 5** |
| **`ProgressDeadlineExceeded` / `progressDeadlineSeconds`** | named, not defined | **no entry — needs a ledger row at Ch 6 §4** |
| `journalctl -u kubelet` / systemd | named as out-of-scope | optional |

`cAdvisor`, `Metrics API`, `static Pod`/`mirror Pod` and `ProgressDeadlineExceeded`
are all absent from the B7 ledger entirely. The first two are explanatory-only and
defined in place, so a glossary entry suffices. The last two reach **graded** text,
which the ledger's own rule forbids for glossary-only terms.

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Strong. The chapter opens with an explicit
  disclosure that CNCF publishes no sub-competency weights and that every "high-value"
  judgement is authored, not published. The metadata line states the published 28% with
  its tag and disclaims the chapter's share. §4 even distinguishes an inference from a
  sourced claim in the reader's hearing ("that follows from two sourced facts… rather
  than from a source that states it outright"). No numbers are asserted without a tag.
- [x] **Fear-based content uses real examples.** The Logbook Entry (readiness cascade
  behind an intermittent 502) is a mechanism illustration, not a scare story, and it
  carries no invented figures.
- [x] **Simplification acknowledged.** Dead Reckoning present. §5 explicitly names where
  the trail continues past KCNA scope and why stopping there without saying so "would be
  dishonest." §7 states that metrics-server is *not* a monitoring system. §3 and §7 both
  teach that an absent signal is not evidence — the chapter's best uncertainty work.
- [x] **Authority claims cite legitimate sources.** Every factual sentence is tagged.
- [x] **"Frequently tested" claims verifiable.** The chapter never claims exam frequency.
  "High-Priority Topics" in the Exam Alert is authored priority, covered by the disclosure.
- [x] **No strawmanning of alternative study methods.** The "most study guides reduce this
  to a two-column glossary" passage grants that a glossary answers one question shape and
  argues a limitation rather than caricaturing. Passes, narrowly.
- [x] **Subject dignity (skill Part 14).** All wry beats are oriented at practitioners.

**Two advisories, neither blocking:**

1. §"Why This Chapter Matters": *"you would forget them within a week"* asserts a
   retention outcome as certainty. Soften to "would likely forget."
2. TYB 3 Q2 key: *"the single most common error in applying this rule"*; §4 Hazards:
   *"the easiest error to make in this material."* These are unhedged frequency claims
   about reader error. The skill's Part 2 explicitly sanctions this register ("Here's
   where most candidates lose points" is a ✓ example) and no number is invented, so
   they pass — but "the error this most often produces" costs nothing.

## Recommended fixes

The revision stage's diagnostics were addressed; everything below is new, found by
reading shipped text rather than the contracts.

**1. HIGH — Ch 6 promises "the six causes" twice; Ch 13 §3 delivers none.**
Shipped Ch 6 §4 line 663: *"Reading that signal, and finding out which of the six causes
you hit, is a diagnosis skill. [cross-bearing: see Ch 13 — diagnosing a stuck rollout]"*
And Ch 6 TYB #2 line 778, in a graded answer key: *"finding which of the six causes fired,
and fixing it is Chapter 13's. [cross-bearing: see Ch 13 §3]"*
Ch 13 §3 says only "Several quite different underlying causes produce that identical
condition" and works one example. The draft's AUTHOR-REVIEW records that "six" was removed
as unsourced — correct for this chapter's corpus, but the removal *creates* the
inconsistency rather than resolving it, because the book already asserts six twice.
**Route the Stage 2 fetch the draft asks for** (`…/controllers/deployment/#failed-deployment`,
which enumerates the documented causes), then either restore a sourced count and list them
in §3, or amend both Ch 6 sites. The book cannot ship with Ch 6 promising six and Ch 13
naming none.

**2. HIGH — Ch 11 promises a symptom-level discrimination Ch 13 §2 does not give.**
Shipped Ch 11:588: *"A claim that never binds is, from the Pod's point of view,
indistinguishable from a scheduling failure… **Chapter 13 will teach you to tell those two
apart from the symptoms.** [cross-bearing: see Ch 13 §2 — Pods that never start]"*
Ch 13 §2 gives one sentence of family membership, and its own AUTHOR-REVIEW concedes the
mechanism is unstated. The reader arrives expecting a discrimination. Needs either the
storage fetch the draft requests (note its own caveat: `WaitForFirstConsumer` inverts the
direction, so the fetch is genuinely required) or a softening edit at Ch 11:588.

**3. MEDIUM — cross-chapter contradiction on who performs an OOM kill.**
Ch 5 §8 line 1025, sourced to `k8s-docs-resource-management-2026-08-23`:
*"when it uses more than its memory limit, **the kernel** may terminate it."*
Ch 13 §4, sourced to `k8s-docs-pod-qos-2026-08-24`: *"killed and restarted by the kubelet."*
Both are true at different altitudes; the book asserts both without reconciling, and the
kubelet version sits in two graded keys (TYB 2 Q1, Practice Q6). **Good news for the draft:**
its AUTHOR-REVIEW cut the kernel/cgroup axis for want of a source, but Ch 5's snapshot is
already in the book's corpus and supports it. One clause in §4 — the kernel terminates,
the kubelet observes and applies the restart policy — reconciles them and lets the cut
discrimination axis be restored without a new fetch.

**4. MEDIUM — close the `Terminated`-state AUTHOR-REVIEW; no edit needed.**
The draft flags that "no snapshot in the corpus places OOMKilled on the Terminated state."
Shipped Ch 5 §8 line 1025 does exactly that, sourced to `k8s-docs-pod-lifecycle-2026-08-23`:
*"The container reaches the `Terminated` state, with a reason and an exit code recorded."*
The framing in §4 and TYB 2 Q1's stem is established canon. Delete the comment; do not
soften the prose.

**5. MEDIUM — `static Pod` and `mirror Pod` first appear in a graded answer key.**
Confirmed absent from Chapters 1–12. Practice Q13 distractor D introduces both, and the
key refutes it with a sourced quotation — the weakest possible teaching position, and it
violates the ledger's rule that a term in an answer key may not be glossary-only.
**Precedent applies:** the Ch 9 gate rebuilt a Practice Q16 distractor from taught material
so no graded item depended on eBPF. Do the same here — D can be rebuilt from §5's own
kubelet-registration material — or add a ledger row plus glossary entries.

**6. LOW — pattern attribution.** §7 and Soundings A8 both credit Chapter 10 with naming
"the object exists; nothing happens without the component." Ch 10 §3 owns it per the ledger
and §8 is titled for it, so the cross-bearing is right and should stay. But the reader was
told to *remember it by name* in **Ch 6 TYB #3, line 1082** ("Name the pattern, because you
will retrieve it by name"). A reader carrying that instruction is told the wrong chapter.
Cheapest fix: "the book named this for you and Chapter 10 built a section on it," pointer
unchanged.

**7. LOW-MEDIUM — §5's node-condition table partly restates Ch 8 §4.**
Ledger ⚑1: "Ch 13 §5 retrieves them as a diagnostic and **must not restate the table**."
§5 announces compliance ("This section does not restate that table") and then carries a
"What it is telling you" column that reproduces Ch 8 §4's definitions from the same
snapshots — including the `False`-vs-`Unknown` distinction that Ch 8 §4 teaches at line
809, warns about in its hazards table at 1128, and repeats in its chapter summary at 1349.
No contradiction; the two agree. Fix is small: compress or drop the middle column and keep
"Your next move," which is the genuinely new material.

**8. LOW — ledger and glossary debts to record at the glossary build.**
New rows needed for `cAdvisor`, `Metrics API`, `ProgressDeadlineExceeded` (assign to
Ch 6 §4, where line 663 already teaches it), and `static Pod`/`mirror Pod` if fix 5 keeps
them. Correct the ledger's `VPA` first-appearance to Ch 3, and expand the acronym at
Ch 3:606. Glossary entries for the nine signature strings, `crictl`, the metrics pipeline
and cluster-level logging.

**Two items of good news for the author, no action in this chapter:**

- Ch 2:604's open AUTHOR-REVIEW asks for exactly the crictl fetch this chapter now holds
  (`k8s-docs-crictl-2026-08-31`). Ch 2's softened "beneath Kubernetes" framing can be
  restored from Ch 13's snapshot.
- The chapter **asserts no running ordinal** for the object-exists pattern, the control
  loop, or the pluggable interfaces — fully compliant with the "state the pattern, never
  the count" convention ratified at the Ch 8 gate, and it correctly leaves Ch 15 §7's
  control-loop payoff unspent.

**Structural conformance, verified:** section numbers and titles match the B6 skeleton
exactly; heading form is `## <difficulty> §N — Title` (the skeleton's recommended Ch 5–8
form); the Zenith carries ☀️ per recommendation #4; `The Voyage Ahead` per style-decisions
2026-04-19; no `calculated_length_words` (budgets retired 2026-04-24); no pointer is
emitted at Ch 1 §N or Ch 20 §N.
```

**The two things worth your attention before this ships** are the broken promises: Ch 6 tells the reader twice — once in a graded answer key — that Chapter 13 will identify "which of the six causes" fired on a stalled rollout, and Ch 11 tells them Chapter 13 will teach them to tell an unbound PVC from a scheduling failure "from the symptoms." Neither is delivered. Both need the Stage 2 fetches the draft already requests, or edits to the promising chapters.

Two of the draft's own AUTHOR-REVIEW comments resolve against shipped text rather than needing research: the `Terminated`-state framing for `OOMKilled` is already canon in Ch 5 §8 with a source, and the kernel-agency axis the draft cut is supported by a snapshot the book already holds.
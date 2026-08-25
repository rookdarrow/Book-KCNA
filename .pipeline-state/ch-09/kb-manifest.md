I have everything verified. Four of my checks changed or added conclusions the integration report did not reach, so those lead.

```markdown
# Knowledge-Base Manifest — KCNA Chapter 9

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 9 — Every Pod Has an Address
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-25

**Inputs consulted:** the finalized chapter; `ch-09/integration.md`; `ch-09/outline.md` frontmatter (`kb_tags` — 53 concepts, 3 commands, `objectives: ["D2.1"]` on all eight sections); shipped `chapter-01` … `chapter-08` **and `chapter-10`**; the eight prior `kb-manifest.md` files; the BINDING B6 `section-skeleton.md` and B7 `term-ownership.md`; `book-outline/arc-outline.md` and `retrieval-architecture.md`; `sources/` (155 files, enumerated); `certcomp/pipeline/stages.py`.

---

## Structural findings — all verified on disk this pass

**1. ⚑ The `=== WRITE` / `=== APPEND` blocks are still inert, and the knowledge base still does not exist.**

Re-verified rather than inherited. `stages.py` defines stage 14 with exactly one output, `{ch}/kb-manifest.md`. A repo-wide search of `certcomp/**/*.py` for `=== WRITE` and `=== APPEND` returns **zero** parsers. `C:\dev\lodestar\Book-KCNA\knowledge-base\` **does not exist** — no `glossary.md`, no `concepts/`, no `objective-coverage.md`, no `retrieval-log.md`.

**Nine chapters' knowledge base now sits unapplied across nine manifests.** Replay order is load-bearing; this manifest appends to ten shards that earlier chapters create:

> ch-01 → ch-02 → ch-03 → ch-04 → ch-05 → ch-06 → ch-07 → ch-08 → **ch-09**

**2. ⚑ NEW — the integration report missed a four-instance canon contradiction, and it is the most consequential finding in this manifest.**

Chapter 9 asserts **four times** that the absent-component pattern has no name until Chapter 10:

| Line | Text |
|---|---|
| 517 (§3) | "Hold on to that shape — you will see it again in §4, and **Chapter 10 will give it a name**." |
| 727 (§4) | "Two instances now. **Chapter 10 will meet a third and give the pattern a name**." |
| 1558 (Practice Q13) | "This is the second instance in the chapter of the same shape… **Chapter 10 gives it a name**." |
| 1708 (Voyage Ahead) | "You have seen that shape twice in this chapter now. **Chapter 10 gives it a name**, and once it has a name you will start seeing it everywhere." |

**The pattern was named in Chapter 3 and retrieved by name in Chapter 6.** Shipped `chapter-03:601` is a ⚓ Worth Securing that names it outright — *"the absent-component pattern… Remember the phrase: **an object without its component does nothing.** You're going to meet it four more times in this book"* — and Chapter 3 carries it forward in three further places (`:725`, `:742`, `:1225`) plus its Chapter Summary (`:1302`). Shipped `chapter-06:1005` and `:1082` retrieve it by name explicitly.

**Chapter 10 gets this right and Chapter 9 does not.** Shipped `chapter-10:634` reads *"**Chapter 3's phrase, verbatim**… you have now personally met three instances"*, and `chapter-10:1347` reads *"**Chapter 3 gave you the sentence** — an object without its component does nothing — and told you that you would meet it four more times. This is where that debt comes due in full."* Chapter 10 casts itself as the **payoff**, not the naming. Chapter 9 is the only chapter in the book that says the pattern is nameless.

Chapter 9 uses the string `absent-component` or `without its component` **zero times** — verified by count.

**Root cause, and it exonerates the drafting stage.** `arc-outline.md:218` instructs, for Chapter 10: *"`ch10-zenith` is the named home of cross-cutting theme #3… **name the pattern here** so Ch 13 and Ch 17 can retrieve it by name."* Chapter 9 followed the plan. The plan was overtaken by shipped Chapter 3, which named it five chapters earlier than the arc outline expected. Chapter 10, drafted later, noticed and corrected; Chapter 9 did not.

**Rule 6 flag against `concepts/absent-component-pattern.md`.** That shard (created by ch-03) carries a capitalised **"⚑ USE THIS NAME. DO NOT RE-COIN IT."** Chapter 9 does not re-coin it — it does something the shard did not anticipate and that is worse for the shard's purpose: it **denies the name exists**. B3's stated rationale is *"Naming it once and retrieving it by name turns four gotchas into one rule."* A chapter that supplies two fresh instances while telling the reader the rule is not yet named spends the instances without buying the rule.

**The fix is one edit and it pays for itself twice — see the retrieval ledger.** Retrieving Chapter 3's phrase at §3 or §4, and tagging **Practice Q6 or Q13** `[retrieval: ch3]`, simultaneously (a) removes the contradiction, (b) discharges B3 cross-cutting theme #3 in the chapter that supplies its two best instances, and (c) lifts Chapter 9's retrieval rate from 18.9% to 21.6%, inside B3's 20–25% band, **without writing a new question**.

**3. ⚑ NEW — both BINDING scaffolding artifacts carry a wrong kube-proxy mode list, and the chapter is the one that is right.**

| Artifact | Mode list |
|---|---|
| B6 `section-skeleton.md:127` | "iptables, IPVS, nftables; **userspace as historical**" |
| B7 `term-ownership.md:316` | "iptables · IPVS · nftables · **userspace**" |
| **Chapter 9 §6** | iptables (the default), IPVS, nftables on Linux; **kernelspace** on Windows |

Both artifacts instruct coverage of `userspace` and **omit `kernelspace` entirely**. The chapter follows `k8s-docs-virtual-ips-kube-proxy-2026-08-23`, which documents exactly those four, and then **grades `userspace` as a wrong answer**: Practice Q16 option A is "userspace (default), iptables, IPVS", rejected because it "names a mode that is not among the documented Linux modes."

So a BINDING artifact tells a chapter to teach a mode that the same chapter's answer key marks incorrect. The chapter is correct against the snapshot. **Fix the artifacts, not the chapter** — and note this widens integration finding F1c: the B7 Ch 9 rows need a *content* correction as well as the section renumber.

**4. ✅ Confirming integration F1 from the knowledge-base side, with the exact remap.**

The B7 ledger's Ch 9 rows use the skeleton's **seven**-section numbering, independently confirming that the skeleton is the stale artifact rather than the chapter. The row-level remap F1c calls for, made precise:

| B7 row | Ledger says | Shipped chapter |
|---|---|---|
| Service · ClusterIP · Virtual IP | §2 | §2 ✓ (VIP is really §6) |
| `port`/`targetPort`/`nodePort` · NodePort · LoadBalancer · ExternalName | §3 | §3 ✓ |
| Service selector · EndpointSlice · Endpoints (legacy) · readiness gating | §4 | §4 ✓ |
| Headless Service · Service without selectors | §4 | **§5** |
| Service proxy · kube-proxy modes | §5 | **§6** |
| CoreDNS · cluster DNS · A/AAAA · SRV · FQDN · `svc.cluster.local` · search domain · Pod DNS record | §6 | **§7** |
| — | (no row) | **§8** Zenith |

Also: the ledger pins **Virtual IP / VIP to §2**, but the chapter defines the virtual IP properly in **§6** (§2 does not use the term at all). Move that row with the others.

**5. ✅ Confirming the control-loop ordinal collision, with the constraint the audit needs.**

Verified: `chapter-08:713` and `:1071` both claim **"the sixth"**; `chapter-09:1145` claims **"the sixth control loop in this book."** A book-wide ordinal grep finds these are the **only** explicit ordinal claims in shipped text — Chapter 8 counts "five instances since Chapter 3" implicitly rather than enumerating them, so the running tally is not independently recoverable from prose.

The binding constraint for the author's audit: **Chapter 8 has spent "sixth," and Chapter 9 contains two loops it identifies as such** (the EndpointSlice controller at §4/§8; kube-proxy at §6/§8). kube-proxy is therefore *at least* seventh and, if the EndpointSlice controller is counted, eighth. Do not renumber to "seventh" without deciding whether Chapter 9 consumes one ordinal or two.

**6. ⚑ The British-spelling regression is now two chapters running and slightly worse.**

Counted across ten word-families (`behaviour`, `colours`, `favours`, `recognise`, `memoris*`, `generalis*`, `kilometres`, `organis*`, `neighbour`, `centre`):

| Chapter | Count |
|---|---|
| Ch 4 | 0 |
| Ch 7 | 3 |
| Ch 8 | 21 |
| **Ch 9** | **22** |

ch-08's manifest flagged this as a new regression. It did not abate. It gates two voice-exemplar nominations below, exactly as it did for Chapter 8.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**58 terms contributed — 46 defined · 4 partial · 8 gap-only.**

Two counts are in play and are not in conflict. Stage 13 flags **10** terms needing glossary entries; skill Part 16 requires the glossary to carry every technical term introduced (100-term floor). Chapters 4, 5, 7 and 8 set the precedent of contributing the full owned set. Both are below, separated. Appended as a Chapter 9 section rather than merged into one A–Z — re-transcribing prior prose to preserve a single alphabet is exactly the drift Rule 5 forbids; book assembly merges alphabets mechanically.

### Priority rows — the 10 gaps Stage 13 flagged, plus 2 the ledger assigns and the chapter never delivers

Rule 5 forbids inventing wording. Where the chapter defines nothing, the row records what the chapter *does* say and names the gap rather than laundering a paraphrase into canon.

| Term | What the chapter gives | Status |
|---|---|---|
| **CNAME record** | Used 8× as load-bearing to ExternalName — "configures your cluster's DNS server to return a **CNAME record** with that external hostname value" — and never defined or expanded. | ⚑ **gap.** Highest-value of the ten: ExternalName's whole definition rests on it, and it is graded in Practice Q7 and Q8 |
| **eBPF** | Named twice with no pointer (§1 Cilium, §6 Closer Look) and used as **graded distractor C in Practice Q16**. | ⚑ **gap + ratified-decision violation.** See G2 |
| **BGP** | Named once (§1): Calico supports "overlay and non-overlay networks, with or without BGP." Never expanded. | ⚑ **gap** |
| **IPVS** | Named 9× as a mode label. Never expanded to *IP Virtual Server*. | ⚑ **gap — and an acronym-register violation.** In the register at `term-ownership.md:676`; the register's rule is "every acronym is expanded on its first use in the book, without exception" |
| **iptables · nftables · kernelspace** | Mode labels with function only: "configures packet forwarding rules using iptables / using nftables / in the Windows kernel." | **partial — sufficient at tier.** Rows record the function verbatim |
| **overlay network · native routing · encapsulation** | Quoted from the addons page as plugin properties; never glossed. | ⚑ **gap**, one combined entry |
| **NXDOMAIN** | Used once, Bearings #3 answer 4, unglossed. | ⚑ **gap** |
| **"GA since Kubernetes 1.33"** | Release-stage jargon, unglossed. | **defer to Ch 17 §8** (KEPs and feature stages), with a pointer row here |
| **`serving` / `terminating`** | Glossed in §4 and its 🔭 Closer Look: "actual readiness can be checked as a condition called `serving`"; "Terminating endpoints always have their `ready` status as `false`." | **defined — no gap.** Recorded because the three-condition *set* is not stated as a set |
| **`dnsPolicy` values** | Glossed in a 🔭 Closer Look, correctly marked out of scope, including the trap: "the value called `Default` is *not* the default." | **defined** |
| **`port` / `targetPort` / `nodePort`; node-port range** | **Nothing. Absent from the entire book** — verified across all ten shipped chapters; the only hits are Chapter 9's three AUTHOR-REVIEW comments saying so. | ⚑ **gap — BLOCKING, and now a downstream contract breakage.** See F3 note below |
| **`Endpoints` (the legacy object)** | **Nothing.** The chapter never mentions it. | ⚑ **gap — ledger-assigned and undelivered.** See F4 note below |

### Three of these need an author decision, not just a glossary row

**⚑ `port` / `targetPort` / `nodePort` is no longer a local omission.** B7 assigns the row to **Ch 9 §3** as an owned term, and the B6 skeleton plans **Ch 16 §4** around "`port` vs `targetPort`" as an application-side Service failure mode *referring back to Chapter 9*. An owned term that is never defined leaves the ledger claiming coverage the book does not have, and leaves Ch 16 pointing at nothing. The blocker is plumbing, not research: Stage 2 fetched `k8s-docs-service-ports-2026-08-24` on 2026-08-24 and could not write it; the body survives verbatim in `research-manifest.md` §3, and the file is confirmed absent from `sources/`. **Extract it, re-run corpus assembly, then add the §3 block and the Practice item after Q8.** Until then, record the gap in the B7 orphan section so Ch 16's drafting stage is not surprised.

**⚑ `Endpoints` (legacy) is assigned here and absent.** B7's Canonical forms table (`:838`) reserves the capitalized form *"only in Ch 9 §4's contrast"* — a contrast the chapter never draws. It is a real term a reader meets in older material and in `kubectl api-resources` output, and one sentence in §4 discharges it. Either write the sentence or move the row to the orphan list. Do not leave it assigned and undelivered.

**⚑ eBPF is used in graded text against an explicit ratified prohibition.** `term-ownership.md:771-775` rules it **glossary-only**: *"Any of the three sections may name it as an implementation detail **with a pointer to the glossary**. **Not eligible for graded text.**"* Chapter 9 names it twice **without a pointer** and grades it as Practice Q16's distractor C. The distractor is fair and the fact is true — this is a ratified-decision violation, not an accuracy defect. **Author's call:** write the glossary entry and add the two pointers, or swap the Q16 distractor for one built from taught material. The glossary row alone does not discharge it, because the ledger's condition is the *pointer*.

### Acronym-register additions required

Verified across all ten shipped chapters: **CNAME, BGP, eBPF and NXDOMAIN appear 23 times in total and every one is in Chapter 9.** All four are first-appearing here. Three need new rows in B7's acronym register, which currently omits them; IPVS has a row but is unexpanded at its first use, which is also here.

| Acronym | Expansion | Register status |
|---|---|---|
| CNAME | Canonical Name (record) | ⚑ **absent — add** |
| BGP | Border Gateway Protocol | ⚑ **absent — add** |
| eBPF | extended Berkeley Packet Filter | ⚑ **absent — add**, alongside the glossary-only ruling |
| NXDOMAIN | Non-Existent Domain | ⚑ **absent — add** |
| IPVS | IP Virtual Server | ✅ present (`:676`) — ⚑ **unexpanded at first use; expand in §6** |
| NAT | Network Address Translation | ✅ present (`:686`) — ✅ **satisfied by inversion**: §1 writes "address translation (NAT)" |
| CNI | Container Network Interface | ✅ present (`:664`) — ✅ expanded in §1 |
| FQDN | Fully Qualified Domain Name | ✅ present (`:672`) — ✅ used in §7 |

### Full Part-16 coverage — the 46 defined rows

Verbatim from the chapter, organised by section. Full text in the append block; representative rows:

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **Kubernetes network model** ★ | Four requirements: unique cluster-wide Pod IP; all Pods reach all Pods; no NAT and no proxies; node agents reach local Pods. | Ch 9 §1 |
| **Pod IP** ★ | "Each Pod in a cluster gets its own **unique cluster-wide IP address**." The Pod holds it; "every container in a Pod shares the network namespace, including the IP address and network ports." | Ch 9 §1 (introduced Ch 5 §1) |
| **CNI** ★ | "Pod networking is implemented by a **network plugin**, and the interface it plugs into is **CNI, the Container Network Interface**." CNI plugins are **binary plugins** — "Kubernetes executes them as external binaries rather than linking them in." | Ch 9 §1 |
| **Service** ★ | "A method for exposing a network application that is running as one or more Pods in your cluster. Each Service object defines a **logical set of endpoints** — usually those endpoints are Pods — along with a policy about how to make those Pods accessible." | Ch 9 §2 |
| **ClusterIP** | "Exposes the Service on a cluster-internal IP… only reachable from within the cluster. This is **the default** that is used if you don't explicitly specify a type." | Ch 9 §3 |
| **NodePort** ★ | "Exposes the Service on each node's IP at a static port… **Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP`**." | Ch 9 §3 |
| **ExternalName** ★ | "Maps the Service to the contents of the `externalName` field… configures your cluster's DNS server to return a **CNAME record**… **No proxying of any kind is set up**." | Ch 9 §3 |
| **EndpointSlice** ★ | "Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service." The selector is the question; the EndpointSlice is "the written-down answer." | Ch 9 §4 |
| **Readiness gate** ★ | "**selector → EndpointSlice → traffic.** The selector proposes; readiness disposes." A Pod must both match the selector **and** be Ready. | Ch 9 §4 |
| **Headless Service** ★ | "`clusterIP: None` is a **configuration, not a failure**. It says: *do not give me one address — give me all of them.*" | Ch 9 §5 |
| **kube-proxy** ★ | Implements "a **virtual IP mechanism for Services of type other than ExternalName**," watching Service and EndpointSlice objects and programming each node to "capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints." | Ch 9 §6 |
| **Cluster IP (the address)** ★ | "**Virtual.** Nothing is listening on it… It exists only as a rule, replicated on every node." A **rule, not a socket**. | Ch 9 §6 |
| **Service DNS record** ★ | `my-svc.my-namespace.svc.cluster-domain.example` — "resolves to the cluster IP" for a normal Service, and "to the set of IPs of all of the Pods selected by the Service" for a headless one. **Same name form, different answer.** | Ch 9 §7 |
| **DNS search list** ★ | "By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain." Not a Kubernetes special case — "ordinary DNS search-domain resolution." | Ch 9 §7 |
| **The Zenith** ☀️ | "A Service is a **label query with a name**. The virtual IP, the endpoint list, and the DNS record are three control loops publishing that one query's current answer in three different formats." | Ch 9 §8 |
| *(31 further rows in the append block)* | | |

---

## Concept shards at `Book-KCNA/knowledge-base/concepts/`

### Created — 9 shards

`kubernetes-network-model.md` · `cni.md` · `service.md` · `service-types.md` · `endpointslice.md` · `headless-and-selectorless-services.md` · `kube-proxy.md` · `cluster-dns.md` · `service-dns-records.md`

`headless-and-selectorless-services.md` is **one shard rather than two**, following the `predicates-priorities.md` (ch-07) and `resource-quota-and-limitrange.md` (ch-08) precedent: neither exception reaches 200 words alone, and §5's four-cell table — *the discrimination between them* — is the content. Splitting it would put the table in one file and orphan the other.

`service-dns-records.md` is split out of `cluster-dns.md` because the five record shapes are a lookup table Chapters 13 and 16 will consult directly, and a lookup table buried in a concept narrative is a lookup table nobody finds.

`cni.md` is created here rather than appended: the shard registry has `cri.md` (ch-02) and `pluggable-interface-pattern.md` (ch-03) but **no `cni.md`**, and B7 assigns CNI's definitional home to Ch 9 §1.

### ⚑ Rule 6 — three conflicts against prior canon. None overwritten.

**FLAG 1 — `absent-component-pattern.md`. Chapter 9 tells the reader a named pattern is nameless. This is the manifest's headline finding; full evidence in Structural finding 2.**

The shard carries a capitalised **"USE THIS NAME. DO NOT RE-COIN IT"** and B3's rationale that naming it once *"turns four gotchas into one rule."* Chapter 9 supplies the pattern's two best instances — a `type: LoadBalancer` Service with no provider (§3), and a Service whose selector matches nothing (§4) — and, four separate times, tells the reader the name is coming in Chapter 10.

**The shard is APPENDED, not rewritten.** The appended note records the two Chapter 9 instances as roster members, records that Chapter 9 declined to name them, and records *why* (the stale `arc-outline.md:218` instruction) so a later pass does not read it as carelessness. It does **not** relax the naming instruction, because shipped Chapter 10 depends on it: `chapter-10:634` counts "three instances" the reader has "personally met," two of which are Chapter 9's, and `chapter-10:1567` cites them as `Ch 9 §3` and `Ch 9 §4` by number.

⚑ **Consequence for the ch-06 open item.** ch-06's manifest escalated the competing-string conflict — the shard's *"absent-component pattern"* versus B3's *"the object exists but nothing happens without the component"* — as "author's call, now urgent." **Shipped Chapter 10 has now settled it in practice**: `chapter-10:634` adopts *"an object without its component does nothing"* and attributes it to Chapter 3, which is the shard's short form, not B3's string. Two shipped chapters (3, 10) now use the shard's wording against one (6) using B3's. Recommend ratifying the shard's form and sweeping `chapter-06:1005`/`:1082` to match. The ch-06 escalation can be closed.

**FLAG 2 — `control-loop.md`. Do not let the replay write an ordinal.**

ch-03 recorded this theme's chain as Ch 3→4→6→11→15→17. **Chapter 8 was not on that list and bore the theme anyway; Chapter 9 is not on it either and bears it twice.** ch-08's manifest flagged the first instance as unbudgeted. This is the second chapter running, which makes it a schedule defect rather than a one-off.

The appended shard records the two Chapter 9 loops **without an ordinal**, and records the collision constraint instead: Chapter 8 spent "sixth" twice, so Chapter 9's kube-proxy loop is at least seventh. A naïve replay that transcribed Chapter 9's "sixth" into the shard would install the contradiction in the knowledge base rather than merely in the prose.

*Incidental, and Chapter 8's defect:* `chapter-08:713` points at `Ch 3 §5 — the control loop`; the skeleton puts the control loop at **Ch 3 §6** (§5 is *The Only Door In*). Recorded for a future Ch 8 sweep; no Chapter 9 change follows.

**FLAG 3 — `pluggable-interface-pattern.md` / `cri.md`. The fourth interface is still named two ways, and Chapter 9 is on the correct side.**

Integration drift D1, confirmed independently: shipped Ch 2 §4 (`:598`) and §8 (`:914`, `:930`) say **"API extensions"**; shipped Ch 6 §8 (`:1032`), the B6 skeleton (Ch 17 §4), the B7 ledger, and Chapter 9 §1 all say **"CRDs."** Four sources to one.

The appended shard note records **both** forms with their locations and does **not** normalise, because the correction belongs to Ch 2 or to a Ch 17 §4 reconciliation, not to Chapter 9's Stage 14. Chapter 9 needs no edit — but its §1 cross-bearing label reads `see Ch 2 §4 — CRI, CNI, CSI and CRDs as the four pluggable interfaces`, which describes Ch 2's list using Ch 6's vocabulary. A reader who turns back finds a different fourth item than the label promised.

### Appended — 10 shards earlier chapters created that Chapter 9 extends

| Shard | Created by | What Ch 9 adds | Conflict? |
|---|---|---|---|
| `absent-component-pattern.md` | ch-03 | Two roster instances; the naming denial | ⚑ **FLAG 1 — append, do not rewrite** |
| `control-loop.md` | ch-03 | Two more instances (EndpointSlice controller, kube-proxy) | ⚑ **FLAG 2 — no ordinal** |
| `pluggable-interface-pattern.md` | ch-03 | CNI as **second of the four**, with the D1 drift recorded | ⚑ **FLAG 3 — do not normalise** |
| `pod-shared-context.md` | ch-05 | **The promise paid.** Ch 5 §1 said "the entire argument for why Services must exist rests on the Pod having an IP that changes when the Pod is replaced." §1 and §2 are that argument | no — promise paid |
| `label-selector.md` | ch-04 | **The selector as a *question* whose answer is written elsewhere** — and §8's observation that two controllers evaluate the same field with no coordination | no — extension |
| `probe.md` | ch-05 | **The object readiness acts in.** Ch 5 §7 named the mechanism and deferred the location; §4 supplies it: the EndpointSlice | no — promise paid |
| `namespace.md` | ch-04 | **All four deferred DNS items discharged** — the mechanism, what serves the records, what else gets one, how resolution proceeds | no — promise paid in full |
| `node-conditions.md` | ch-08 | `NetworkUnavailable` retrieved at exactly one chapter's distance, as the shortest proof the plugin is load-bearing | no — extension |
| `pod-lifetime.md` | ch-05 | Churn reframed from a Pod property into the **precondition an abstraction exists for** | no — extension |
| `optional-components.md` | ch-03 | kube-proxy as optional when the plugin does equivalent forwarding; Cilium named | no — extension |

**`namespace.md` note.** ch-04's manifest recorded four items deferred to Chapter 9 by name, quoting Ch 4 §3's own sentence. All four land in §7, and the integration report verified the four-item list is reproduced verbatim. This is the cleanest promise-payment in the book so far and the shard should record it as closed rather than open.

**`probe.md` note.** ch-05 registered this as a forward plant with published text: `chapter-05:858` reads *"When Chapter 9 explains how a Service knows which Pods to send traffic to, **this is the mechanism doing the removing**."* §4 pays it, and the pinned cross-bearing `Ch 9 §4 — readiness and Service endpoint membership` still resolves correctly under the shipped eight-section numbering. **This is one of the two pins that make the skeleton, not the chapter, the stale artifact** (integration F1).

---

## Voice-exemplar candidates nominated

Nominations only. Not written to `voice-exemplars.md` — the author ratifies exemplars explicitly (Rule 1).

| Function | Excerpt | Recommendation |
|---|---|---|
| **☀️ Zenith** | "A Service is a **label query with a name**… The Pods were never the stable thing. **The question was.**" and its follow-on: "Pods churn beneath it the way water churns beneath a fixed star. The question doesn't move." | **Strongest in the chapter.** A title paid off, a thesis compressed to four words, and a maritime figure that carries the technical claim rather than decorating it |
| **epistemic honesty / self-narrowing** | "The claim is a slogan, and slogans need narrowing until they're true. §3's type ladder and §7's record shapes are **not** consequences of this architecture… Those you memorise, the same as anyone." | **Strong** — and the direct successor to ch-08's top nomination, which was the same move. A chapter retracting its own thesis to the version that survives the exam. ⚑ *contains `memorise`* |
| **⚓ Worth Securing** | "Nothing is listening on a cluster IP. It is not a host, not a process, not a port on a machine. It is a rule on every node that **captures** traffic to that address and **redirects** it elsewhere." | **Strong.** Model §18.14 length discipline; the single most load-bearing correction in the chapter, stated in four sentences |
| **⚓ Worth Securing** | "'A Service is a load balancer' is the most durable wrong model in Kubernetes networking… A load balancer is *a thing that runs*. A Service is a **declaration that gets reconciled**." | **Strong.** Corrects a misconception by naming the *category* error rather than the fact error, which is the register Ch 4 established |
| **Part 14 restraint** | Bearings #3 answer 3: "it makes no claim about which mode is faster, more scalable, or better… The documentation states the list, the default, and the substitution, and says nothing about relative performance — **so neither does this book**." | **Strong.** The chapter arguing against its own convenience. The integration report singled this out and it deserves the nomination |
| **chapter epigraph** | "A harbor is rebuilt piece by piece until nothing original remains. The name on the chart never moves — and the name is how anyone finds it." | **Strong.** Lodestar-original, states the chapter's thesis before the thesis exists, and spells `harbor` **American** — consistent with the `🏆 Safe Harbor` marker |
| **— Dead Reckoning** | §7's five-record table, and the *Why This Chapter Matters* block that names the whole apparatus in eight sourced sentences. | **Moderate.** Competent and complete; not distinctive enough to anchor the form |
| **stakes without inflation** | "This is roughly seven points on our authored allocation… What that number understates is structural: within this book, Networking is the competency the others lean on." | ⚑ **DO NOT NOMINATE as written.** Sits four lines from the Attention Budget's unhedged "That is where this chapter's exam points concentrate" (G1). Re-nominate after the hedge |
| **Extended Analogy** | — | **None present.** Chapters 5, 9 and 10 carry no Logbook Entry and no Extended Analogy. Optional per §18.15, but three consecutive chapters is a pattern worth an author look |

**⚑ Two nominations gated by the spelling regression.** The self-narrowing excerpt contains `memorise`, and the surrounding §8 prose contains `generalises` and `Recognise`. This is the same gate ch-08 applied to its Extended Analogy nomination, for the same reason: an exemplar is a template, and a template that teaches the wrong orthography propagates it. Chapter 9's 22 instances against Chapter 4's 0 make this a book-wide sweep, not a chapter fix. **Re-nominate both after the sweep.**

**Note on the register generally.** Chapter 9 continues Chapter 8's strong Part 14 compliance: every numeric claim is tagged or declared authored, every narrowing forced by the fact-accuracy audit was made *downward* to what the corpus supports rather than papered over, and the subject-dignity check passes cleanly — the wry beats ("explaining at eight the next morning why the logs say every request came from the same three addresses") are aimed at the practitioner throughout. The two G1 exceptions are the only Part 14 blemishes, and both are one-clause fixes.

---

## Objective coverage log

`D2.1` = the first competency under CNCF domain **D2, Container Orchestration (28%)** — *"28% – Container Orchestration: **Networking**; Security; Troubleshooting; Storage"* (`cncf-kcna-curriculum-pdf-2026-08-23.md:14`).

All eight sections carry `objectives: ["D2.1"]`. **D2.1 is shared with Chapter 10**, which the arc outline confirms (`arc-outline.md:211` — Ch 10 also covers D2.1). Chapter 9 is the **first** coverage; Chapter 10 completes it.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D2.1 — Container Orchestration › Networking | Chapter 9 | **deep (1 sub-objective gap)** | — |

**One sub-objective ships with a gap: Service port mechanics.** `port` / `targetPort` / `nodePort` and the node-port range are owned by Ch 9 §3 per B7 and appear nowhere in the book. This is the chapter's only incomplete objective element and should be recorded as such rather than rounded up — particularly because **Ch 16 §4's planned content depends on it**.

**This is the first D2 row.** With D1 complete at 44% (Ch 2, 3, 7, 8) and D2.1 now open, the objective-coverage file spans two domains. ch-08 recommended a domain-level audit before Part III; Part III has now started, so the audit is overdue rather than upcoming. ⚑ **D1.4 (Ch 2) remains unrecorded because Chapter 2's Stage 14 never ran** — flagged by ch-03, unresolved through six chapters.

---

## Retrieval-practice ledger

**7 tagged items across 37 graded questions (15 Bearings + 22 Practice) = 18.9%. Below B3's 20–25% band for this chapter.** All seven tags are accurate — each points at a chapter that genuinely covers the material, verified against shipped text; three match the source chapter's wording verbatim.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| two containers, one port space, `localhost`, one Pod IP | ch 5 §1 | ch 9 — ☆ Bearings #1 item 2 |
| rolling update replaces every Pod, and every address with it | ch 6 §4 | ch 9 — ☆ Bearings #1 item 4 |
| a Service is a *different controller reading the same labels* | ch 6 §3 | ch 9 — ☆ Bearings #2 item 1 |
| three containers → one address, one endpoint | ch 5 §1 | ch 9 — Practice Q2 |
| one Pod, two independent selectors, no coordination | ch 4 §5 | ch 9 — Practice Q9 |
| readiness probe → the object it acts in | ch 5 §7 | ch 9 — Practice Q11 |
| a bare service name resolves in the caller's namespace | ch 4 §3 | ch 9 — Practice Q21 |

**✅ The ≥4-back floor is satisfied.** B3 requires, from Ch 8 on, at least one item from ≥4 chapters back. Practice Q9 and Q21 both draw on Ch 4 — five chapters back.

**⚑ Bearings #3 carries no retrieval item at all.** #1 has two, #2 has one, #3 has none. The distribution is the accounting problem, not the total.

### The cheapest fix is the one that also closes Structural finding 2

**Tag Practice Q6 or Q13 `[retrieval: ch3]`.** Q6 is the bare-metal `type: LoadBalancer` Service that waits indefinitely; Q13 is the Service with a cluster IP, a DNS record, and zero endpoints. Both are already-written instances of B3 cross-cutting theme #3, and Chapter 10 subsequently cites both by section number as the reader's own prior encounters (`chapter-10:723`, `:1567`).

That single tag yields **8/37 = 21.6%**, inside the band, and:

- discharges a scheduled cross-cutting theme in the chapter that supplies its two best instances;
- adds a **six-chapters-back** item, the longest span in the chapter;
- forces the §3/§4 prose to retrieve Chapter 3's phrase, which removes the four-instance contradiction;
- requires **no new question and no fetch**.

It is strictly better than adding a question, and better than tagging a Bearings item, because it fixes a canon defect as a side effect. If the author prefers the retrieval item in Bearings #3 (where the distribution gap actually is), Q13's content can be restated as a sixth Bearings item — but that costs a question and does not fix anything the tag does not already fix.

**⚑ Soundings load.** Items 2–5 pretest Chapters 4, 5 and 6 — correct Soundings design, excluded from the budget per B3 decision 2, and not counted above. Worth recording that Chapter 9's *pre*-test load on earlier chapters is heavier than its *post*-test load, which is the inverse of the usual shape and may explain why the graded rate came in low.

**⚑ Standing gap, fourth chapter running.** `book-outline/retrieval-architecture.md` is still not the B3 document — it is a permission-failure message plus a prose summary, re-verified this pass. The per-chapter schedule was never written to disk. `arc-outline.md` carries B3's stated figures forward marked `[B3]` and reconstructs the rest marked `[B5-reconstructed]`, which is a partial mitigation, not a replacement. **This ledger remains the only durable record of what has actually been retrieved** — which is, again, the strongest single argument for replaying these nine manifests.
```

Now the write intentions.

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

## Chapter 9 — Every Pod Has an Address (Networking · D2.1)

> Definitions inherited verbatim from Chapter 9 per Stage 14 Rule 5. Rows marked ⚑
> carry an open definitional gap: the chapter names or uses the term but does not
> define it. Do not paraphrase these into definitions — either land the named
> snapshot or have the author supply wording.

### The network model (§1)

**★ Kubernetes network model** — Four requirements, not a mechanism: a unique cluster-wide IP per Pod; all Pods able to reach all Pods; no NAT and no proxies between Pods; node agents able to reach the Pods on their node. "It describes what must be true, and says nothing about how." (Chapter 9 §1)

**★ Pod IP** — "Each Pod in a cluster gets its own **unique cluster-wide IP address**. A Pod has its own private network namespace, shared by all of the containers within it; processes running in different containers in the same Pod communicate with each other over `localhost`." The address belongs to the **Pod**; its containers share it. (Chapter 9 §1; introduced Chapter 5 §1)

**Pod network / cluster network** — "Handles communication between Pods. Barring intentional network segmentation, all Pods can communicate with all other Pods, **whether they are on the same node or on different nodes**." (Chapter 9 §1)

**★ NAT-free pod-to-pod traffic** — "Pods communicate with each other **directly, without the use of proxies or address translation (NAT)**." One documented exception: on Windows, the rule does not apply to host-network Pods. (Chapter 9 §1)

**Node-agent reachability** — "**Agents on a node** — system daemons, the kubelet — can communicate with all Pods on that node." (Chapter 9 §1)

**Flat network** — The consequence of rules 1–3: "An application inside the cluster can be written as though every other application in the cluster is on the same flat network, because it is." Two applications "can both listen on port 8080 forever, because they are not sharing a port space; each has its own." (Chapter 9 §1)

**★ CNI (Container Network Interface)** — "Pod networking is implemented by a **network plugin**, and the interface it plugs into is **CNI, the Container Network Interface**" — listed among Kubernetes' infrastructure extension points alongside CSI for storage, CRI for container runtimes, and device plugins. (Chapter 9 §1)

**CNI plugin** — "**Binary plugins**: Kubernetes executes them as external binaries rather than linking them in." (Chapter 9 §1)

⚑ **SOURCING NOTE — do not strengthen downstream.** The chapter states that a CNI plugin **implements** the model, not that one is **required** to, and names **no executor** for the binaries. Both are deliberate. The stronger normative form and the "Kubernetes implements none of it" form are available only from `k8s-docs-network-plugins-2026-08-24`, which Stage 2 fetched but never wrote to `sources/`; the body survives in `research-manifest.md` §1. The executor was dropped because CNI management was removed from the kubelet in Kubernetes 1.24. **⚑ Shipped `chapter-10:1228` carries BOTH superseded forms** ("implements none of it"; "binary plugins the kubelet executes") and attributes them to Chapter 9. Fix Ch 10, or land the snapshot and strengthen both chapters together.

**★ The division of labour** — "Kubernetes **defines** the network model. A **CNI network plugin implements** it. The four rules are requirements the plugin satisfies, not machinery Kubernetes provides." **Second of the four pluggable interfaces** this book tracks. (Chapter 9 §1)

**Calico** — "A networking and network policy provider supporting overlay and non-overlay networks, with or without BGP." (Chapter 9 §1)

**Cilium** — "Provides a flat Layer 3 network with an eBPF-based data plane, in either native routing or overlay mode, and is a CNCF project at the Graduated level." Can also "act as a replacement for kube-proxy." (Chapter 9 §1, §6)

**Flannel** — "An overlay network provider." (Chapter 9 §1)

⚑ **Overlay network · native routing · encapsulation · non-overlay** — Quoted as plugin properties; never glossed. GAP — one combined entry needed. The chapter's own point is that these "are genuinely different pieces of engineering, and every one of them satisfies the same four rules." (Chapter 9 §1)

⚑ **BGP** — Named once, unexpanded: Calico supports networks "with or without BGP." GAP. Expansion: *Border Gateway Protocol*. **Not in the B7 acronym register — add.** (Chapter 9 §1)

⚑ **eBPF** — Named twice as an implementation detail (Cilium's data plane, §1; the kube-proxy replacement, §6) and used as **graded distractor C in Practice Q16**. GAP, and a **ratified-decision violation**: `term-ownership.md:775` rules eBPF glossary-only, permitting it to be named "with a pointer to the glossary" and declaring it "**Not eligible for graded text.**" Neither mention carries a pointer. Expansion: *extended Berkeley Packet Filter*. **Not in the B7 acronym register — add.** (Chapter 9 §1, §6)

**`NetworkUnavailable`** — "`True` if the network for the node is not correctly configured." Retrieved from Chapter 8's node-condition list at one chapter's distance, as "the shortest demonstration available that the plugin is not a footnote." (Chapter 9 §1; introduced Chapter 8 §4)

### The problem, and the object (§2)

**The churn problem** — "If some set of Pods (call them 'backends') provides functionality to other Pods (call them 'frontends') inside your cluster, how do the frontends find out and keep track of which IP address to connect to?" "The set of Pods running at one moment can be different from the set running a moment later." (Chapter 9 §2)

**★ Service** — "A method for exposing a network application that is running as one or more Pods in your cluster. Each Service object defines a **logical set of endpoints** — usually those endpoints are Pods — along with a policy about how to make those Pods accessible." (Chapter 9 §2)

**★ Stable, long-lived address** — "The Service API lets you provide a **stable, long-lived** IP address or hostname for a service implemented by one or more backend Pods, where the individual Pods making up the service **can change over time**." The chapter's compression: "It is not a workaround for churn; it is the abstraction that makes churn a non-event." (Chapter 9 §2)

**Service selector** — "Services most commonly abstract access to Kubernetes Pods thanks to the selector" — a query over labels, the same mechanism a ReplicaSet uses. (Chapter 9 §2; introduced Chapter 4 §5)

**⚓ A Service is not a load balancer** — "A load balancer is *a thing that runs*: a process, on a machine, receiving your traffic and forwarding it. A Service is a **declaration that gets reconciled** — an object… stating that a set of Pods should be reachable at a stable address." (Chapter 9 §2)

### The four types (§3)

**ClusterIP** — "Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is **the default** that is used if you don't explicitly specify a type for a Service." (Chapter 9 §3)

**★ NodePort** — "Exposes the Service on each node's IP at a static port — the node port." And: "to make the node port available, **Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP`**." NodePort does not replace ClusterIP; it adds to it. (Chapter 9 §3)

**LoadBalancer** — "Exposes the Service externally using an external load balancer." (Chapter 9 §3)

**★ Kubernetes provides no load balancer** — "**Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider.**" `type: LoadBalancer` is a *signal*, not a provisioning act. On a cluster with no integration, the Service "sits there with no external address indefinitely… the signal is raised correctly, and there is nobody ashore to answer it." (Chapter 9 §3)

**★ ExternalName** — "Maps the Service to the contents of the `externalName` field… The mapping configures your cluster's DNS server to return a **CNAME record** with that external hostname value. **No proxying of any kind is set up.**" No cluster IP, no endpoint list, nothing to intercept. "A DNS alias flying a Service's colours." (Chapter 9 §3)

**⚠ ExternalName is not the fourth rung** — "It allocates no address, selects no Pods, and proxies nothing… The word 'External' in two type names (ExternalName, and LoadBalancer's external load balancer) is doing you no favours; they have nothing mechanically in common." (Chapter 9 §3)

**★ Additivity (as documented)** — "**A NodePort Service also has a cluster IP** — Kubernetes sets one up, exactly as if you had requested `type: ClusterIP`. Asking for a higher rung never removes the rungs below it." (Chapter 9 §3)

⚑ **SOURCING NOTE — narrowed deliberately.** The general form ("LoadBalancer implies NodePort implies ClusterIP") is **not** in the corpus. `k8s-docs-service-2026-08-23` documents the allocation for NodePort only; its LoadBalancer entry is one sentence about external exposure. `k8s-docs-service-ports-2026-08-24` carries "NodePort and LoadBalancer are supersets of ClusterIP" but was never written to `sources/`. **Restore the three-rung form in §3's Fixed Point, the Exam Alert, the Chapter Summary row and Bearings #1 answer 3 together — not piecemeal — once it lands.**

⚑ **CNAME record** — Used 8× and load-bearing to ExternalName's entire definition; never defined or expanded. GAP — the highest-value of the ten flagged, because Practice Q7 and Q8 both grade on it. Expansion: *Canonical Name record*. **Not in the B7 acronym register — add.** (Chapter 9 §3)

⚑ **`port` · `targetPort` · `nodePort` · the node-port range** — **ABSENT FROM THE ENTIRE BOOK.** Verified across all ten shipped chapters. B7 assigns these to Ch 9 §3 as owned terms and the B6 skeleton plans **Ch 16 §4** around "`port` vs `targetPort`" *referring back to Chapter 9*. **BLOCKING.** Blocker is plumbing, not research: `k8s-docs-service-ports-2026-08-24` was fetched and never written; body survives in `research-manifest.md` §3. Extract, re-run corpus assembly, add the §3 block, the Practice item after Q8, and +2 min to the §3 Attention Budget row.

**🪢 Mnemonic** — "*Inside · on every node · out in the world · somewhere else entirely.*" ClusterIP, NodePort, LoadBalancer, ExternalName. (Chapter 9 §3)

**The exposure ceiling** — "A LoadBalancer Service gives you one external address per Service… expensive and awkward for fifty." And: "none of these four types knows anything about HTTP. They move packets." Protocol-aware routing is the Gateway API's or Ingress's job. (Chapter 9 §3)

### The backends (§4)

**★ EndpointSlice** — "Kubernetes automatically manages EndpointSlice objects to provide information about the **Pods currently backing a Service**." The chapter's framing: "The selector is the question. The EndpointSlice is the written-down answer." (Chapter 9 §4; name-dropped Chapter 3)

**EndpointSlice controller** — One of the controllers in the kube-controller-manager, which "populat[es] EndpointSlice objects **to provide a link between Services and Pods**." (Chapter 9 §4)

**endpoints controller** — The Kubernetes documentation's older name for the same job, used on the Pod-lifecycle page. "One job, two names in the documentation. **Not two components.**" (Chapter 9 §4, §5)

⚑ **HEADWORD RULING PROPOSED — not currently in the B7 Canonical forms table.** The pair recurs in Ch 13 §7 and Ch 16 §4. **Recommend adding a row:** headword `EndpointSlice controller`; `endpoints controller` sanctioned only when quoting or paraphrasing the Pod-lifecycle page, and **never without the reconciliation sentence**. Chapter 9 reconciles it three times (§4, §5, Bearings #2 answer 2) and is the model.

**Labels vs owner references** — "Labels answer *which slices belong to this Service*. Owner references answer *what should be cleaned up when this Service is deleted*, and help different parts of Kubernetes avoid interfering with objects they don't control." (Chapter 9 §4; introduced Chapter 6 §3)

**★ Readiness gates membership** — "**selector → EndpointSlice → traffic.** The selector proposes; readiness disposes. A Pod must both **match the selector** and be **Ready** to appear in the Service's EndpointSlice and receive traffic." (Chapter 9 §4)

**Readiness probe, restated at its destination** — "If the readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod." A Pod's `Ready` condition means it "should be added to the load balancing pools of all matching Services." (Chapter 9 §4; introduced Chapter 5 §7)

**Terminating endpoints** — "Any endpoints that represent the terminating Pods are **not immediately removed** from EndpointSlices, and a status indicating terminating state is exposed from the EndpointSlice API. **Terminating endpoints always have their `ready` status as `false`**, so load balancers will not use them for regular traffic." The list "carries state" — a terminating Pod stays on it, marked, "so that anything watching can distinguish 'gone' from 'going.'" (Chapter 9 §4)

**`serving`** — "If traffic draining on a terminating Pod is needed, actual readiness can be checked as a condition called `serving`." The distinction between "should get new traffic" and "can still handle traffic it already has." (Chapter 9 §4)

⚑ **NOT ASSERTED AS A SET.** `ready` / `serving` / `terminating` appear individually, each where `k8s-docs-pod-termination-2026-08-24` states it. The three are **not** presented as *the* documented condition set, because `k8s-docs-endpoint-slices-2026-08-24` was fetched and never written (body in `research-manifest.md` §2). Also deliberately absent: why slices rather than one list, the default endpoints-per-slice limit, and `publishNotReadyAddresses`. **Keep `publishNotReadyAddresses` out** — it is a real exception to the readiness gate and would undercut the Fixed Point.

**★ The two causes of an empty endpoint list** — "If they don't [match], the Service's selector probably does not match the Pods' labels, **or** the Pods are not Ready." The chapter's compression: "**two different bugs, and they live in two different files**." (Chapter 9 §4)

**A Service with no endpoints** — "Not a broken Service. It is a correct Service whose selector currently matches nothing, or whose matching Pods are not Ready." (Chapter 9 §4)

⚑ **`Endpoints` (the legacy object)** — **ABSENT FROM THE CHAPTER.** B7 assigns it to Ch 9 §4 and reserves the capitalized form "only in Ch 9 §4's contrast" — a contrast never drawn. GAP. One sentence in §4 discharges it; otherwise move the row to the orphan list. (assigned Ch 9 §4, undelivered)

### The two exceptions (§5)

**★ Headless Service** — "Sometimes you don't need load-balancing and a single Service IP. In that case, you can create what are termed **headless Services**, by explicitly specifying `\"None\"` for the cluster IP address (`.spec.clusterIP`)." The chapter's compression: "`clusterIP: None` is a **configuration, not a failure**. It says: *do not give me one address — give me all of them.*" (Chapter 9 §5)

**Headless with selectors** — "The endpoints controller creates EndpointSlices in the Kubernetes API, and modifies the DNS configuration to return **A or AAAA records that point directly to the Pods** backing the Service." (Chapter 9 §5)

**Headless without selectors** — "**No EndpointSlices are created automatically.**" (Chapter 9 §5)

**Why StatefulSets need one** — "**StatefulSets currently require a headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service.**" Because a StatefulSet's Pods "are **not interchangeable**: each has a persistent identifier that it maintains across any rescheduling" — and for those workloads, "'send this to any one of them, I don't care which' is not a convenience; it is *precisely wrong*." (Chapter 9 §5)

**Service without selectors** — "When used with a corresponding set of EndpointSlice objects and **without a selector**, the Service can abstract other kinds of backends, including ones that run **outside the cluster**: an external database, a service in another namespace or cluster, or a workload being migrated." The chapter's compression: "The selector is how a Service *usually* finds its endpoints. It is not what a Service *is*." (Chapter 9 §5)

**The four-cell table** — Headless-or-not and selector-or-not are **independent** axes. All four combinations are supported configurations; "None of them is an error state." (Chapter 9 §5)

### The data plane (§6)

**★ kube-proxy** — "**Every node in a Kubernetes cluster runs a kube-proxy** — unless you have deployed your own alternative component in its place. The kube-proxy component is responsible for implementing a **virtual IP mechanism for Services of type other than ExternalName**." It "watches the Kubernetes control plane for the addition and removal of **Service and EndpointSlice objects**," and for each Service configures the node to "**capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints**." (Chapter 9 §6; introduced Chapter 3 §3)

**kube-proxy as a control loop** — "A control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server." (Chapter 9 §6)

**★ The cluster IP is virtual** — "**Nothing is listening on a cluster IP.** No process is bound to it. There is no host at that address, no socket, no server. It exists only as a rule, replicated on every node, that says: *packets addressed here go to one of those addresses instead.*" A **rule, not a socket** — and it follows from capture-and-redirect, which binds nothing. (Chapter 9 §6)

**Virtual IP / VIP** — The address a Service holds and nothing occupies. ⚑ **B7 pins this term to Ch 9 §2; the chapter defines it in §6.** Move the ledger row.

**kube-proxy modes** — On Linux: **`iptables`** — "configures packet forwarding rules using iptables, and is **the default**"; **`ipvs`** — "configures packet forwarding rules using IPVS"; **`nftables`** — "configures packet forwarding rules using nftables, **GA since Kubernetes 1.33**." On Windows, exactly one: **`kernelspace`** — "configures packet forwarding rules in the Windows kernel." (Chapter 9 §6)

⚑ **BOTH BINDING SCAFFOLDING ARTIFACTS CARRY A WRONG MODE LIST.** `section-skeleton.md:127` says "iptables, IPVS, nftables; **userspace as historical**"; `term-ownership.md:316` says "iptables · IPVS · nftables · **userspace**". Both include `userspace` and **omit `kernelspace`**. The chapter follows `k8s-docs-virtual-ips-kube-proxy-2026-08-23` and **grades `userspace` as wrong** (Practice Q16 option A — "names a mode that is not among the documented Linux modes"). **The chapter is correct. Fix the artifacts.**

⚑ **IPVS** — Named 9× and never expanded. Expansion: *IP Virtual Server*. **In the B7 acronym register at `:676`, but unexpanded at its first use in the book, which is here** — a register-rule violation ("every acronym is expanded on its first use, without exception"). Expand in §6.

⚑ **`iptables` · `nftables` · `kernelspace`** — Function stated ("configures packet forwarding rules using / in…"), underlying technology never explained. PARTIAL, and **sufficient at tier**: "That is the entire requirement at this level: recognise the four names, and know which one is the default."

**kube-proxy is optional** — "If you use a network plugin that implements packet forwarding for Services by itself, and provides equivalent behavior to kube-proxy, then **you do not need to run kube-proxy** on the nodes in your cluster." Cilium is a named example. (Chapter 9 §6)

⚑ **"GA since Kubernetes 1.33"** — Release-stage jargon, unglossed. **Defer the definition to Ch 17 §8** (KEPs and feature stages); carry a pointer row here.

### Names (§7)

**Cluster DNS** — "Kubernetes creates DNS records for Services and Pods. You can contact Services with consistent DNS names instead of IP addresses." "**DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on.**" (Chapter 9 §7)

**CoreDNS** — The cluster DNS addon that serves these records; "a flexible, extensible DNS server which can be installed as the in-cluster DNS for Pods." **It publishes the answer; it does not decide it.** (Chapter 9 §7; promised Chapter 3 §4)

**kubelet's DNS role** — "The kubelet configures Pods' DNS so that running containers can look up Services by name rather than IP." (Chapter 9 §7)

**★ Service DNS record (normal)** — "Normal (not headless) Services are assigned DNS A and/or AAAA records… with a name of the form `my-svc.my-namespace.svc.cluster-domain.example`. **This resolves to the cluster IP of the Service.**" Four labels: service name · namespace · the literal `svc` · the cluster domain (commonly `cluster.local`). (Chapter 9 §7)

**★ Service DNS record (headless)** — "**The same name form**; unlike normal Services, this resolves to **the set of IPs of all of the Pods** selected by the Service. Clients are expected to consume the set or else use standard round-robin selection from the set." (Chapter 9 §7)

**SRV record** — "Created for **named ports**… of the form `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example`." The Service's own four labels stay intact; the port name and protocol prefix on. (Chapter 9 §7)

**Pod DNS record** — "`pod-ipv4-address.my-namespace.pod.cluster-domain.example` — for example, `172-17-0-3.default.pod.cluster.local`." Dots in the address become dashes, "because dots are label separators in DNS and cannot appear inside a label." Position 3 is `pod`, **not** `svc`. (Chapter 9 §7)

**`hostname` + `subdomain`** — "When both are set and a headless Service exists with the same name as the subdomain, the Pod's FQDN is `hostname.subdomain.namespace.svc.cluster-domain.example`." The shape by which an individual StatefulSet member is addressable — what "network identity" cashes out to. (Chapter 9 §7)

**★ DNS search list** — "By default, a client Pod's DNS search list includes **the Pod's own namespace** and the cluster's default domain." A bare name resolves in the client Pod's own namespace only **because that namespace is in its search list** — "not a Kubernetes special case; it is ordinary DNS search-domain resolution." (Chapter 9 §7)

**⚠ The bare-name hazard** — "If **no** Service of that name exists in the caller's namespace, you get a resolution failure — annoying, but obvious. If a Service of that **same name** exists in the caller's namespace, the lookup **succeeds**, and your application connects to the wrong thing. No error. No timeout. No log line." (Chapter 9 §7)

**🪢 Mnemonic** — "*service, namespace, svc, cluster.local.* Four labels, always in that order… `svc` is a literal, not an abbreviation of anything in your cluster." (Chapter 9 §7)

**`dnsPolicy`** — "Controls how a Pod's DNS is configured. `ClusterFirst` — any query that does not match the configured cluster domain suffix is forwarded to an upstream nameserver — **is the default policy if `dnsPolicy` is not explicitly specified**." Also `Default` (inherit from the node), `ClusterFirstWithHostNet`, and `None` (all settings from `dnsConfig`). **The trap: "the value called `Default` is *not* the default."** (Chapter 9 §7)

⚑ **NXDOMAIN** — Used once (Bearings #3 answer 4), unglossed. GAP. Expansion: *Non-Existent Domain*. **Not in the B7 acronym register — add.**

⚑ **SCOPED OUT DELIBERATELY.** CoreDNS Corefile configuration, custom nameservers, stub domains and CoreDNS plugins are absent by design, per the outline and the `dns-cluster-addon` snapshot's own scope note. **Not a gap.**

**DNS-based service discovery vs name-based virtual hosting** — "One turns a name into an address before any traffic moves; the other sorts traffic that has already arrived at a single address." Both involve hostnames and "sit on opposite sides of the connection." (Chapter 9 §7; virtual hosting is Chapter 10 §2)

### Synthesis (§8)

**☀️ The Zenith** — "A Service is a **label query with a name**. The virtual IP, the endpoint list, and the DNS record are three control loops publishing that one query's current answer in three different formats. **The Pods were never the stable thing. The question was.**" (Chapter 9 §8)

**★ Where the claim stops** — "§3's type ladder and §7's record shapes are **not** consequences of this architecture. They are facts about an API… Those you memorise, the same as anyone." (Chapter 9 §8)

**⚓ The debugging heuristic** — "Ask two questions: **what does the selector currently match?** and **which loop hasn't caught up yet?**" (Chapter 9 §8)

⚑ **THE PATTERN CHAPTER 9 DOES NOT NAME.** The chapter supplies two instances of the **absent-component pattern** — a `type: LoadBalancer` Service with no provider (§3) and a Service whose selector matches nothing (§4) — and states four times that "Chapter 10 gives it a name." **It was named in Chapter 3 §4** ("an object without its component does nothing") and retrieved by name in Chapter 6 §8; shipped Chapter 10 credits Chapter 3 explicitly. See `concepts/absent-component-pattern.md` § Rule 6. **Do not propagate Chapter 9's framing.**

### Commands introduced

**`kubectl get endpointslices -l kubernetes.io/service-name=<service-name>`** — "Make sure the endpoints in the EndpointSlices match up with the number of Pods you expect to be members of your Service." (Chapter 9 §4)

⚑ **Planned but not delivered:** the outline's `kb_tags.commands` lists `kubectl-get-services` and `kubectl-describe-service`. Neither appears in the chapter. Not a defect — both are covered by Chapter 8 §1's verb table — but the outline's command list overstates what shipped.

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubernetes-network-model.md ===
# Concept: The Kubernetes network model

**Home:** Chapter 9 §1 · **Competency:** D2.1 · **Status:** canonical

## The four rules (verbatim)

1. **Unique cluster-wide IP.** "Each Pod in a cluster gets its own unique cluster-wide IP address. A Pod has its own private network namespace, shared by all of the containers within it; processes running in different containers in the same Pod communicate with each other over `localhost`."
2. **All Pods reach all Pods.** "Barring intentional network segmentation, all Pods can communicate with all other Pods, whether they are on the same node or on different nodes."
3. **No NAT, no proxies.** "Pods communicate with each other directly, without the use of proxies or address translation (NAT)." *Documented exception: on Windows, this does not apply to host-network Pods. Nothing in this book is built on it.*
4. **Node agents reach local Pods.** "Agents on a node — system daemons, the kubelet — can communicate with all Pods on that node."

## Why rule 3 is the load-bearing one

In ordinary infrastructure, reaching a process means reaching a host and then a port on it, and the address the receiver sees is frequently not the address the sender used. Kubernetes forbids all of it. The receiving Pod sees the sending Pod's **actual** address.

The consequence the chapter draws: a whole category of problems does not get *solved* here, it is **absent** — port collisions between unrelated applications, coordinating who gets which host port, address translation that hides the caller, maintaining a registry of where things currently live.

## Requirements, not a mechanism

The model "describes what must be true, and says nothing about how." That is why implementations differ so widely — overlay and non-overlay, with or without BGP, native routing or encapsulation, eBPF data planes — and why "an application inside the cluster cannot tell which one it is running on."

## Rule 2's hedge

*"Barring intentional network segmentation"* is deliberate. Kubernetes has an API for segmenting Pod-to-Pod traffic on purpose: NetworkPolicy, **Chapter 10 §6**.

## Related

`[[cni]]` · `[[pod-shared-context]]` · `[[service]]` · `[[node-conditions]]` (`NetworkUnavailable`) · `[[pluggable-interface-pattern]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cni.md ===
# Concept: CNI — the Container Network Interface

**Home:** Chapter 9 §1 · **Competency:** D2.1 · **Status:** canonical
**Position:** the **second** of the four pluggable interfaces this book tracks (CRI · **CNI** · CSI · CRDs)

## The division of labour

> Kubernetes **defines** the network model. A **CNI network plugin implements** it.

The four rules are requirements the plugin satisfies, **not machinery Kubernetes provides**.

CNI is "listed among Kubernetes' infrastructure extension points alongside CSI for storage, CRI for container runtimes, and device plugins for custom hardware." CNI plugins are **binary plugins**: "Kubernetes executes them as external binaries rather than linking them in."

## ⚑ Two deliberate narrowings — do not strengthen without the snapshot

**1. "Implements it," not "is required to implement it," and not "Kubernetes implements none of it."** The cached `k8s-docs-extending-kubernetes-2026-08-23` supports the positive claim and states no exclusive negative. The stronger normative form is available only from `k8s-docs-network-plugins-2026-08-24`, fetched by Stage 2 and **never written to `sources/`** (body survives in `research-manifest.md` §1).

**2. No executor is named.** The general extension-points page says the kubelet executes CNI binaries; the more specific network-plugins page records that **CNI management was removed from the kubelet in Kubernetes 1.24**, with the container runtime loading the plugins. Naming no executor is the safe form at associate tier. **Do not restore "external programs that the kubelet executes."**

## ⚑ Shipped Chapter 10 carries both superseded forms

`chapter-10:1228` reads: *"Chapter 9 taught that Kubernetes **defines** the network model and **implements none of it**… network plugins are binary plugins **the kubelet executes**."* Chapter 9 no longer says either. Either trim Ch 10, or land the snapshot and strengthen both chapters in one pass. This is a **revision-induced regression in already-shipped text** and is invisible from inside Chapter 9.

## Implementations named

| Plugin | As described |
|---|---|
| **Calico** | "A networking and network policy provider supporting overlay and non-overlay networks, with or without BGP" |
| **Cilium** | "A flat Layer 3 network with an eBPF-based data plane, in either native routing or overlay mode"; CNCF **Graduated**; can replace kube-proxy |
| **Flannel** | "An overlay network provider" |

## Deployment shape

⚑ **UNTAGGED CLAIM, RETAINED.** Chapter 9 §1 says cluster networking plugins "commonly ship as DaemonSets, one Pod on every node," attributing it to Chapter 6 §7. **`chapter-06:890` carries the same claim with no `[source:]` tag at all** — verified. The propagation option offered by the fact-accuracy audit is therefore unavailable. Only remaining path: fetch `kubernetes.io/docs/concepts/workloads/controllers/daemonset/`, whose "Use cases" section covers cluster networking daemons, which **retroactively fixes Chapter 6 as well**. Build nothing further on it until tagged.

## Related

`[[kubernetes-network-model]]` · `[[cri]]` · `[[pluggable-interface-pattern]]` · `[[kube-proxy]]` (Cilium as a replacement) · `[[optional-components]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/service.md ===
# Concept: The Service object

**Home:** Chapter 9 §2 · **Competency:** D2.1 · **Status:** canonical

## Definition (verbatim)

> A Service is "a method for exposing a network application that is running as one or more Pods in your cluster. Each Service object defines a **logical set of endpoints** — usually those endpoints are Pods — along with a policy about how to make those Pods accessible."

> The Service API "lets you provide a **stable, long-lived** IP address or hostname for a service implemented by one or more backend Pods, where the individual Pods making up the service **can change over time**."

## ★ The framing that matters

**The churn is not an inconvenience the Service copes with. The churn is the condition the Service exists for.** "It is not a workaround for churn; it is the abstraction that makes churn a non-event."

## ⚓ A Service is not a load balancer

> A load balancer is *a thing that runs*: a process, on a machine, receiving your traffic and forwarding it. A Service is a **declaration that gets reconciled** — an object stating that a set of Pods should be reachable at a stable address.

"Whether anything is listening, whether any Pod matches, whether traffic goes anywhere at all: none of that is the Service's doing, and none of it changes whether the Service exists."

This is the single most useful correction in Chapter 9 and the one that makes Chapter 10 straightforward instead of confusing.

## The problem it answers (documentation's own framing)

> "If some set of Pods (call them 'backends') provides functionality to other Pods (call them 'frontends') inside your cluster, how do the frontends find out and keep track of which IP address to connect to?"

The premise: **a Pod is replaced, not repaired** — "a new, near-identical Pod with a different UID," and therefore a different address. `[[pod-lifetime]]`

## ☀️ What a Service actually is

> A Service is a **label query with a name**. The virtual IP, the endpoint list, and the DNS record are three control loops publishing that one query's current answer in three different formats. **The Pods were never the stable thing. The question was.**

## Related

`[[service-types]]` · `[[endpointslice]]` · `[[headless-and-selectorless-services]]` · `[[kube-proxy]]` · `[[cluster-dns]]` · `[[label-selector]]` · `[[control-loop]]` · `[[spec]]` / `[[status]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/service-types.md ===
# Concept: The four Service types

**Home:** Chapter 9 §3 · **Competency:** D2.1 · **Status:** canonical

**Three of them are layers of the same mechanism. One is not a layer at all.**

## The three that stack

| Type | Reachable from | Note |
|---|---|---|
| **ClusterIP** | Inside the cluster only | **The default** if no type is specified |
| **NodePort** | Anything that can reach a node — `<node-ip>:<static-port>`, on every node | **Also allocates a cluster IP** |
| **LoadBalancer** | Wherever the provider's external address is reachable | Kubernetes supplies **no** load balancer |

## ★ Additivity — as documented, and only as documented

> "To make the node port available, **Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP`**."

Asking for a higher rung never removes the rungs below it.

⚑ **DO NOT GENERALISE TO LoadBalancer WITHOUT THE SNAPSHOT.** `k8s-docs-service-2026-08-23` documents this for **NodePort only**; its LoadBalancer entry is one sentence about external exposure and says nothing about the rungs beneath. `k8s-docs-service-ports-2026-08-24` carries "NodePort and LoadBalancer are supersets of ClusterIP" and **was never written to `sources/`**. When it lands, restore the three-rung form in **five places at once**: §3's Fixed Point, the §3 figure annotation, Bearings #1 answer 3, Exam Alert item 4, and the Chapter Summary's LoadBalancer row.

## ★ Kubernetes provides no load balancer

> "Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider."

`type: LoadBalancer` **signals** that one should be provisioned. With no integration and no add-on, the Service "sits there with no external address indefinitely… the signal is raised correctly, and there is nobody ashore to answer it."

⚑ **This is an instance of `[[absent-component-pattern]]`** — the object is correct, the actor is missing. Chapter 9 does not name it as such. See that shard's Rule 6 note.

## ExternalName — not a rung

> "Maps the Service to the contents of the `externalName` field… configures your cluster's DNS server to return a **CNAME record** with that external hostname value. **No proxying of any kind is set up.**"

No cluster IP. No endpoint list. Nothing to intercept, "because there is no address to intercept traffic *to*." It is "a DNS alias flying a Service's colours."

⚠ The word "External" in two type names (ExternalName; LoadBalancer's *external* load balancer) is a trap. **They have nothing mechanically in common.**

## The ceiling that motivates Chapter 10

One external address per Service, and **no protocol awareness at all** — "they move packets." `shop.example.com/checkout` and `shop.example.com/catalog` are indistinguishable to every type here.

## Related

`[[service]]` · `[[kube-proxy]]` (implements every type **except** ExternalName) · `[[cluster-dns]]` · `[[absent-component-pattern]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/endpointslice.md ===
# Concept: EndpointSlice, and the readiness gate

**Home:** Chapter 9 §4 · **Competency:** D2.1 · **Status:** canonical

## The path, in four steps

1. The Service carries a **selector** over Pod labels.
2. "Kubernetes automatically manages **EndpointSlice** objects to provide information about the Pods currently backing a Service."
3. The **EndpointSlice controller**, running inside kube-controller-manager, populates them "to provide a link between Services and Pods."
4. Anything needing a Service's current backends reads the **EndpointSlices**, not the selector.

> **The selector is the question. The EndpointSlice is the written-down answer.**

## ⚑ One controller, two documented names

The Kubernetes documentation calls it the **endpoints controller** on the Pod-lifecycle page and the **EndpointSlice controller** in the control-plane component list. **One job, two names. Not two components.** Chapter 9 reconciles this three times (§4, §5, Bearings #2 answer 2).

**Proposed B7 Canonical-forms row** (not currently present): headword `EndpointSlice controller`; `endpoints controller` sanctioned only when quoting the Pod-lifecycle page, and never without the reconciliation sentence. The pair recurs in Ch 13 §7 and Ch 16 §4.

## ★ Selection is necessary, not sufficient

> **selector → EndpointSlice → traffic. The selector proposes; readiness disposes.**

"If the readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod." A Pod's `Ready` condition means it "should be added to the load balancing pools of all matching Services."

**Three chapters converge here.** Ch 5 gave the probe; Ch 6 relied on the mechanism without explaining it (a bad release cannot take a Service down because a never-Ready Pod never joins the list, so the rollout stalls instead of the service failing); Ch 9 is where the wiring becomes visible.

## Termination runs it backwards

Endpoints for terminating Pods "are **not immediately removed**"; a terminating state is exposed via the API, and "**terminating endpoints always have their `ready` status as `false`**."

So the list is **not a boolean membership test** — it carries state. Note where the state lives: the *Pod* has a `Ready` condition; the Pod's *entry in the slice* has a `ready` status of its own. That is what distinguishes "gone" from "going," and what lets in-flight connections drain.

`serving` is the separate condition for "can still handle traffic it already has."

⚑ **NOT ASSERTED AS A SET.** `ready` / `serving` / `terminating` appear individually, each where the Pod-termination snapshot states it — never as *the* documented condition set, because `k8s-docs-endpoint-slices-2026-08-24` was fetched and never written (body in `research-manifest.md` §2). Also deliberately absent: why slices rather than one list, and the endpoints-per-slice limit. **Keep `publishNotReadyAddresses` out** — it is a real exception to the readiness gate and would undercut the Fixed Point.

## Labels vs owner references

Two mechanisms, two jobs. **Labels** answer *which slices belong to this Service*. **Owner references** answer *what to clean up when the Service is deleted*. `[[label-selector]]`

## ★ The two causes of an empty list

Selector mismatch, **or** Pods not Ready. "**Two different bugs, and they live in two different files.**" Neither is a network problem — endpoint membership is computed in the control plane by a controller reading the API.

```
kubectl get endpointslices -l kubernetes.io/service-name=<service-name>
```

⚑ **Endpoints (the legacy object)** is assigned to Ch 9 §4 by B7 and **never appears in the chapter**. One contrast sentence discharges it, or move the row to the orphan list.

## Related

`[[service]]` · `[[probe]]` · `[[label-selector]]` · `[[control-loop]]` · `[[kube-proxy]]` (reads this, does not write it) · `[[absent-component-pattern]]` (the empty-selector case)
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/headless-and-selectorless-services.md ===
# Concept: Headless and selectorless Services

**Home:** Chapter 9 §5 · **Competency:** D2.1 · **Status:** canonical
**One shard, not two** — the discrimination *is* the content (cf. `predicates-priorities.md`, `resource-quota-and-limitrange.md`).

## Two independent axes, four supported cells

| | **Has a selector** | **No selector** |
|---|---|---|
| **Normal** (has a cluster IP) | The ordinary case. EndpointSlices populated from the selector; DNS resolves to the cluster IP. | A cluster IP in front of endpoints you manage yourself; traffic proxied to the addresses you supplied. |
| **Headless** (`clusterIP: None`) | No cluster IP. EndpointSlices created; DNS returns A/AAAA records pointing **directly at the Pods**. | No cluster IP, and **no EndpointSlices are created automatically**. |

**None of the four is an error state.**

## ★ Headless

> "You can create what are termed **headless Services**, by explicitly specifying `"None"` for the cluster IP address (`.spec.clusterIP`)."

**A configuration, not a failure.** It says: *do not give me one address — give me all of them.* No *head* — no single virtual IP standing in front of the set.

## Why StatefulSets require one

> "**StatefulSets currently require a headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service.**"

Because a StatefulSet's Pods "are **not interchangeable**: each has a persistent identifier that it maintains across any rescheduling." For those workloads, *"send this to any one of them"* is **precisely wrong**. The headless Service subtracts the one feature the ordinary Service exists to provide, **and that subtraction is the feature**.

## ★ Selectorless

Not an exception to the address — an exception to the **backends**. Used "with a corresponding set of EndpointSlice objects and **without a selector**," a Service can abstract backends "including ones that run **outside the cluster**: an external database, a service in another namespace or cluster, or a workload being migrated."

> **The selector is how a Service *usually* finds its endpoints. It is not what a Service *is*.**

**The migration payoff:** clients address `database.production.svc.cluster.local` from day one, whether that resolves to a managed database elsewhere or to Pods moved in last night. Adding the selector hands the slice to the controller; **clients notice nothing.**

## Discriminating selectorless from ExternalName

Both reach an external backend by an in-cluster name. **The discriminator is proxying:**
- **Selectorless** — client connects to a cluster IP; traffic intercepted on the node and redirected. Kubernetes **is** in the path.
- **ExternalName** — client resolves a CNAME and connects directly. Kubernetes is **not** in the path, which changes TLS certificate names, the source address the external service sees, and anything inspecting the connection.

## Related

`[[service]]` · `[[service-types]]` · `[[endpointslice]]` · `[[service-dns-records]]` · `[[pod-lifetime]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kube-proxy.md ===
# Concept: kube-proxy and the virtual IP

**Home:** Chapter 9 §6 · **Competency:** D2.1 · **Status:** canonical

## The job (verbatim)

> "Every node in a Kubernetes cluster runs a kube-proxy — unless you have deployed your own alternative component in its place. The kube-proxy component is responsible for implementing a **virtual IP mechanism for Services of type other than ExternalName**. Each instance watches the Kubernetes control plane for the addition and removal of **Service and EndpointSlice objects**… to configure the node to **capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints**."

It reads the **computed answer** (EndpointSlice), not the raw Pods. `[[endpointslice]]` is what reads Pods.

## It is a control loop

> "A control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server."

⚑ **DO NOT RECORD AN ORDINAL HERE.** Chapter 9 §8 calls this "the sixth control loop in this book"; **shipped Chapter 8 already spent "sixth" twice** (`:713`, `:1071`). Chapter 9 also contains a *second* loop (the EndpointSlice controller), so this one is at least seventh. See `[[control-loop]]` § Rule 6.

## ★ Nothing is listening on a cluster IP

> "No process is bound to it. There is no host at that address, no socket, no server. It exists only as a rule, replicated on every node."

This is **not a separate fact to memorise** — it follows from *capture and redirect*, which binds no socket. Traffic passes **through** a rule; it is never delivered **to** the cluster IP. `ss` or `netstat` on the node shows nothing bound.

The ExternalName exclusion falls straight out of the same sentence: **there is no address to intercept**, so there is nothing to program.

## The modes

| Mode | Platform | Note |
|---|---|---|
| `iptables` | Linux | **The default** |
| `ipvs` | Linux | IPVS = *IP Virtual Server* |
| `nftables` | Linux | GA since v1.33 |
| `kernelspace` | Windows | The only mode on Windows |

**Requirement at this tier:** recognise the four names and know the default. Nothing about relative performance is claimed, because no cached snapshot states any.

⚑ **BOTH BINDING SCAFFOLDING ARTIFACTS ARE WRONG HERE.** `section-skeleton.md:127` ("userspace as historical") and `term-ownership.md:316` ("iptables · IPVS · nftables · userspace") both **include `userspace` and omit `kernelspace`**. Chapter 9 follows the cached snapshot and **grades `userspace` as a wrong answer** (Practice Q16 option A). **The chapter is correct; fix the artifacts.**

## kube-proxy is optional

> "If you use a network plugin that implements packet forwarding for Services by itself, and provides equivalent behavior to kube-proxy, then you do not need to run kube-proxy on the nodes in your cluster."

Cilium is a named example. **A cluster running no kube-proxy is not missing anything** — it is one implementation of one job, and the job can be done elsewhere.

## Related

`[[service]]` · `[[endpointslice]]` · `[[control-loop]]` · `[[cni]]` · `[[optional-components]]` · `[[node-components]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cluster-dns.md ===
# Concept: Cluster DNS

**Home:** Chapter 9 §7 · **Competency:** D2.1 · **Status:** canonical

## What serves it

> "Kubernetes creates DNS records for Services and Pods. You can contact Services with consistent DNS names instead of IP addresses."

- **CoreDNS** is the addon that serves the records — "a flexible, extensible DNS server which can be installed as the in-cluster DNS for Pods."
- **"DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on."** That is why you never installed it.
- **The kubelet** "configures Pods' DNS so that running containers can look up Services by name rather than IP."

**CoreDNS publishes the answer; it does not decide it.**

## ★ Why a bare name is namespace-local

> "By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain."

**That is the entire mechanism.** Not special-case Kubernetes behaviour — ordinary DNS search-domain resolution. A Pod in `payments` searching for `ledger` tries `ledger.payments.svc.cluster.local`, finds something, and **stops**.

## ⚠ The failure mode worth memorising

- No local Service of that name → **NXDOMAIN**. Obvious; fixed in a minute.
- A local Service of that **same** name → the lookup **succeeds against the wrong Service**. No error, no timeout, no log line.

The caller's own namespace is tried **first**, so a same-named local Service always wins. This is why the FQDN form is worth memorising rather than looking up.

## `dnsPolicy`

`ClusterFirst` — "any query that does not match the configured cluster domain suffix is forwarded to an upstream nameserver" — **is the default if not specified**. Also `Default` (inherit from the node), `ClusterFirstWithHostNet`, `None` (all settings from `dnsConfig`).

⚑ **The naming trap: the value called `Default` is *not* the default.**

## Boundary against Chapter 10

**DNS-based service discovery** maps a name to an address *before any traffic moves*. **Name-based virtual hosting** (Ch 10 §2) sorts traffic that has *already arrived* at a single address. Conflating them makes Chapter 10 considerably harder.

## ⚑ Deliberately out of scope — not a gap

CoreDNS Corefile configuration, custom nameservers, stub domains and CoreDNS plugins, per the outline and the `dns-cluster-addon` snapshot's own scope note.

## Related

`[[service-dns-records]]` · `[[namespace]]` (all four Ch 4 §3 deferrals discharged here) · `[[service]]` · `[[headless-and-selectorless-services]]` · `[[optional-components]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/service-dns-records.md ===
# Concept: The five DNS record shapes

**Home:** Chapter 9 §7 · **Competency:** D2.1 · **Status:** canonical, **lookup table**
Split out of `[[cluster-dns]]` deliberately: Ch 13 and Ch 16 consult this directly.

| Name shape | Resolves to |
|---|---|
| `my-svc.my-namespace.svc.cluster-domain.example` — **normal Service** | The **cluster IP** of the Service |
| `my-svc.my-namespace.svc.cluster-domain.example` — **headless Service** | The **set of IPs of all Pods** selected by the Service |
| `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` | The **named port** on that Service (SRV) |
| `pod-ipv4-address.my-namespace.pod.cluster-domain.example` (e.g. `172-17-0-3.default.pod.cluster.local`) | **That Pod** |
| `hostname.subdomain.namespace.svc.cluster-domain.example` (requires `hostname` + `subdomain` set **and** a headless Service named for the subdomain) | **That Pod, by a stable name** |

Record types are **A and/or AAAA** depending on IP family, except SRV records.

## ★ The two facts that get tested

**1. The top two rows are the SAME NAME.** Four labels, same order, same everything. Only the *number of answers* differs — one cluster IP, or the whole Pod set. **Nothing in the name announces that a Service is headless**, which is why a client library assuming one answer per lookup silently talks to only the first Pod.

**2. Column 3 is `svc` for everything except the Pod-by-address record**, where it is `pod`. Columns 2 and 4 are identical in every row.

## Reading the labels

| Position | Part |
|---|---|
| 1 | The Service's name (or the address, or `hostname.subdomain`) |
| 2 | The namespace |
| 3 | Literal `svc` — or `pod` |
| 4 | The cluster domain, commonly `cluster.local` |

**`svc` is a literal, not an abbreviation of anything in your cluster.** In the SRV form, the Service's four labels stay intact; the port name and protocol prefix on.

Dots in a Pod address become **dashes**, because dots are label separators in DNS and cannot appear inside a label.

## The StatefulSet connection

The `hostname` + `subdomain` shape is how an individual StatefulSet member becomes addressable. A stable per-member name of this shape, surviving rescheduling, **is what "network identity" cashes out to**.

## Related

`[[cluster-dns]]` · `[[headless-and-selectorless-services]]` · `[[service]]` · `[[namespace]]`
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

## ⚑ Rule 6 — Chapter 9 supplies two instances and tells the reader the pattern is nameless

**Added by ch-09 Stage 14, 2026-08-25. This shard is APPENDED, not rewritten. The naming
instruction above stands.**

### The roster grows by two

| Instance | Where | Shape |
|---|---|---|
| `type: LoadBalancer` with no provider and no add-on | **Ch 9 §3** | Declaration correct; the actor that would act on it is absent. "The signal is raised correctly, and there is nobody ashore to answer it" |
| A Service whose selector matches nothing | **Ch 9 §4** | Cluster IP allocated, DNS record published, EndpointSlice empty. "The control loop is doing exactly its job, and its job produces nothing" |

*Note: the §4 case is the softer member. It is not strictly component-absence — the
component is present and reconciling an empty set. Chapter 10 nonetheless counts it as an
instance (`chapter-10:723`, `:1567`), so it is recorded here as roster canon.*

### ⚑ The conflict

Chapter 9 states **four times** that the pattern is unnamed until Chapter 10:

- `chapter-09:517` — "Chapter 10 will give it a name."
- `chapter-09:727` — "Chapter 10 will meet a third and give the pattern a name."
- `chapter-09:1558` — "Chapter 10 gives it a name."
- `chapter-09:1708` — "Chapter 10 gives it a name, and once it has a name you will start seeing it everywhere."

Chapter 9 uses the string `absent-component` or `without its component` **zero times**.

**But the pattern was named in Chapter 3 and retrieved by name in Chapter 6.**
`chapter-03:601` is the ⚓ Worth Securing that coins it, carried through `:725`, `:742`,
`:1225` and the Chapter Summary at `:1302`. `chapter-06:1005` and `:1082` retrieve it.

**Shipped Chapter 10 agrees with Chapter 3, not with Chapter 9.** `chapter-10:634` reads
"**Chapter 3's phrase, verbatim**"; `chapter-10:1347` reads "**Chapter 3 gave you the
sentence**… and told you that you would meet it four more times. This is where that debt
comes due in full." Chapter 10 is the **payoff**, not the naming.

### Root cause — the drafting stage followed a stale instruction

`arc-outline.md:218` tells Chapter 10 to "**name the pattern here** so Ch 13 and Ch 17 can
retrieve it by name." That instruction was overtaken by shipped Chapter 3, which named it
five chapters earlier than planned. Chapter 10 noticed; Chapter 9 did not. **This is a
scaffolding defect, not carelessness in drafting.**

### Recommended fix — it pays for itself twice

Retrieve Chapter 3's phrase at §3 or §4, and tag **Practice Q6 or Q13** `[retrieval: ch3]`.
That removes the contradiction, discharges B3 cross-cutting theme #3 in the chapter that
supplies its two best instances, and lifts Chapter 9's retrieval rate from 18.9% to 21.6%
— inside B3's band — **with no new question and no fetch**. See `retrieval-log.md`.

### ✅ ch-06's escalation can now be closed

ch-06 escalated the competing-string conflict as "author's call, now urgent": this shard's
*"absent-component pattern"* / *"an object without its component does nothing"* versus B3's
*"the object exists but nothing happens without the component."* **Shipped Chapter 10 has
settled it in practice** — `chapter-10:634` adopts this shard's short form and attributes it
to Chapter 3. Two shipped chapters (3, 10) now use this shard's wording against one (6)
using B3's. **Recommend ratifying this shard's form and sweeping `chapter-06:1005` and
`:1082` to match.**

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

## Chapter 9 — two more instances, and an ordinal collision

**Added by ch-09 Stage 14, 2026-08-25.**

Chapter 9 identifies **two** control loops:

1. **The EndpointSlice controller** (§4, §8) — watches Services and Pods, evaluates the
   selector, writes down the answer. Desired state, observed state, reconciliation.
2. **kube-proxy** (§6, §8) — documented in as many words: "*a control loop ensures that the
   rules on each node are reliably synchronized with the Service and EndpointSlice state as
   indicated by the API server.*" Notable because it appears in a **reference page about
   packet forwarding**, not in conceptual material.

§8 makes the structural observation the shard should carry: **the EndpointSlice controller
and the ReplicaSet controller run the same shape over the same label set for entirely
different purposes, with no coordination and no conflict.** Two loops, one field, neither
told what the other decided.

### ⚑ NO ORDINAL IS RECORDED HERE, DELIBERATELY

`chapter-09:1145` calls kube-proxy "the sixth control loop in this book, and you should count
it." **Shipped Chapter 8 already claimed "the sixth" twice** (`chapter-08:713`, `:1071`).
Since Chapter 9 contains two loops, kube-proxy is **at least seventh and arguably eighth**.

A book-wide grep finds Ch 8 and Ch 9 are the **only** chapters making explicit ordinal
claims — Chapter 8 counts "five instances since Chapter 3" implicitly rather than enumerating
them, so the running tally is **not recoverable from shipped prose**. An audit is required
before any renumber. **Do not renumber to "seventh" without deciding whether Chapter 9
consumes one ordinal or two.**

A naïve replay that transcribed Chapter 9's "sixth" into this shard would install the
contradiction in the knowledge base rather than merely in the prose.

### ⚑ Unbudgeted, second chapter running

ch-03 recorded this theme's chain as **Ch 3 → 4 → 6 → 11 → 15 → 17**. Chapter 8 bore it
anyway (flagged by ch-08); **Chapter 9 bears it twice**. Two consecutive off-schedule
chapters makes this a schedule defect rather than a one-off. Settle before Ch 11, which
ch-03 flagged as still unbeared.

*Incidental:* `chapter-08:713` points at `Ch 3 §5 — the control loop`; the B6 skeleton puts
the control loop at **Ch 3 §6** (§5 is *The Only Door In*). Ch 8's defect; no Ch 9 change.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interface-pattern.md ===

## Chapter 9 — CNI lands as the second of four

**Added by ch-09 Stage 14, 2026-08-25.**

Chapter 9 §1 names CNI explicitly as the **second** of the four pluggable interfaces, and §8
retrieves the pattern by name: "*which is the second instance of an arrangement you first met
in Chapter 2, where CRI does the same thing for container runtimes.*"

The chapter is also careful about a scoping point worth preserving: the **published** list of
Kubernetes extension points "runs longer than four," and this book tracks a deliberately
chosen four (CRI, CNI, CSI, CRDs) rather than following the documentation item for item.

### ⚑ Rule 6 — the fourth member is still named two ways. Do not normalise here.

| Source | Fourth member |
|---|---|
| shipped `chapter-02:598`, `:914`, `:930` | **"API extensions"** |
| shipped `chapter-06:1032` | **"CRDs"** |
| B6 skeleton (Ch 17 §4), B7 ledger, **`chapter-09` §1** | **"CRDs"** |

Four sources to one. **Chapter 9 is on the majority side and needs no edit.** The correction
belongs to Chapter 2 (three instances) or to a Ch 17 §4 reconciliation, not to Chapter 9's
Stage 14 — recorded here so a replay does not silently rewrite either form.

**One consequential side effect:** Chapter 9 §1 emits the cross-bearing label *"see Ch 2 §4 —
CRI, CNI, CSI and CRDs as the four pluggable interfaces."* The target section exists and does
name CNI, but calls the fourth member "API extensions." A reader who turns back finds a
different fourth item than the label promised.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-shared-context.md ===

## Chapter 9 — the promise paid in full

**Added by ch-09 Stage 14, 2026-08-25.**

ch-05's manifest registered this shard's central fact as a **published promise**:
`chapter-05:365` tells the reader outright that *"that one fact is the premise of Chapter 9.
When you get to Services, the entire argument for why they must exist rests on the Pod having
an IP that changes when the Pod is replaced."*

**Chapter 9 §1 and §2 are that argument**, and §1 adds the half Chapter 5 could not source:
the address is not merely shared, it is **routable from anywhere in the cluster**.

Chapter 9 §1's 🪝 Snag restates the misconception at its own destination, and Practice Q2
tests it at its **downstream consequence** rather than at its definition — three containers in
one Pod contribute **one** address and **one** EndpointSlice entry, because an EndpointSlice
records Pods, not containers. Container count and endpoint count are unrelated numbers.

⚑ **One pointer to fix.** Chapter 9 §1 emits `see Ch 5 §2 — the Pod's shared network
namespace`, and Soundings answer 2 says `(Chapter 5 §2.)`. The B6 skeleton puts the shared
network namespace at **Ch 5 §1** (§2 is *More Than One Container Aboard*). Both should read
**Ch 5 §1**.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/probe.md ===

## Chapter 9 — where readiness actually acts

**Added by ch-09 Stage 14, 2026-08-25.**

ch-05 registered this as a forward plant with published text. `chapter-05:858`: *"When Chapter
9 explains how a Service knows which Pods to send traffic to, **this is the mechanism doing
the removing**."*

**Chapter 9 §4 pays it, and names the object:** the **EndpointSlice**. "That section told you
what a readiness probe does. This one tells you where it does it."

> "If the readiness probe fails, the endpoints controller removes the Pod's IP address from
> the endpoints of all Services that match the Pod."

**The distinction Practice Q11 exists to protect:** a failing readiness probe does **not**
change the Pod's phase, kill it, or restart it — that is the liveness probe. The Pod keeps
running, keeps being counted by its controller, and simply stops receiving traffic.

Readiness is a **gate**, not a step in a chain: matching the selector makes a Pod *eligible*;
it does not put the Pod on the list. The gate is a second, independent condition, evaluated
continuously rather than once at creation.

**✅ The pinned pointer holds.** `chapter-05:858` emits `Ch 9 §4 — readiness and Service
endpoint membership`, and §4 of the shipped eight-section chapter is exactly that. This is one
of the two published pins that make the B6 skeleton — not the chapter — the stale artifact in
integration finding F1.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/label-selector.md ===

## Chapter 9 — the selector as a question, and two loops reading one field

**Added by ch-09 Stage 14, 2026-08-25.**

Chapter 9 supplies the framing that makes the Ch 4 → 6 → 7 → 9 → 10 chain cohere:

> **The selector is the question. The EndpointSlice is the written-down answer.**

A Service **stores the query**; a separate object stores the answer; a separate controller
keeps that answer current. (Practice Q10's distractor A — "the Service itself stores them" —
is the natural guess and is wrong in exactly this instructive way.)

§8 adds the structural observation: **the ReplicaSet controller and the EndpointSlice
controller ask the same question of the same field for entirely different reasons, and do not
coordinate.** One asks in order to count and replace; the other asks in order to write down
addresses. Neither knows the other exists.

Two mechanisms, cleanly separated and worth keeping apart: **labels** answer *which slices
belong to this Service*; **owner references** answer *what to clean up when the Service is
deleted*. A fact that was a curiosity in Ch 6 becomes structural here.

**Retrieval note.** This theme now has instances in Ch 5, 6 (×3), 7 (×2) and 9 (Bearings #2
item 1, Practice Q9) — the most-retrieved cross-cutting theme in the book.

⚑ **One pointer to fix.** Chapter 9 §2 emits `see Ch 4 §7 — labels and selectors`, and
Soundings answer 4 says `(Chapter 4 §7…)`. **Chapter 4 has no §7** — labels and selectors are
**Ch 4 §5**.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespace.md ===

## Chapter 9 — all four deferred DNS items discharged

**Added by ch-09 Stage 14, 2026-08-25.**

ch-04's manifest recorded that `chapter-04:588` gave the Service DNS name form in a single
sentence and **explicitly deferred four things**: the mechanism, what serves the records, what
else gets one, and how resolution actually proceeds.

**All four land in Chapter 9 §7**, and the integration check verified the four-item list is
reproduced verbatim from Chapter 4's own wording:

| Deferred | Discharged |
|---|---|
| the mechanism | The DNS **search list** — the client Pod's own namespace plus the cluster's default domain |
| what serves the records | **CoreDNS**, a built-in addon launched automatically by the addon manager; Pod DNS config written by the **kubelet** |
| what else gets one | Pods (by dashed address, and by `hostname`+`subdomain`); named ports (SRV) |
| how resolution proceeds | Ordinary DNS search-domain resolution — the caller's namespace is tried **first**, and the search **stops** at the first hit |

**This is the cleanest promise-payment in the book so far.** Record the Ch 4 → Ch 9 DNS
bearing as **closed**.

The namespace-scoping consequence is now stated at both ends: a bare name resolves in the
caller's namespace only, and if a same-named Service exists there, the lookup **succeeds
against the wrong one** with no error emitted anywhere.

Also worth carrying: **a Service's selector is namespace-scoped**, so Pods in another
namespace are never selected. Chapter 9's Practice Q12 explanation correctly frames this as *a
special case of the "selector doesn't match" cause*, not a third cause.

⚑ **One pointer to fix.** Chapter 9 §7 emits `see Ch 4 §6 — namespaces and Service DNS names`
in one place; the B6 skeleton puts namespaces at **Ch 4 §3** (§6 is the chapter synthesis).
The §7 revision sweep already corrected most instances; verify none remain.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-conditions.md ===

## Chapter 9 — `NetworkUnavailable` retrieved at one chapter's distance

**Added by ch-09 Stage 14, 2026-08-25.**

Chapter 9 §1 retrieves this shard's `NetworkUnavailable` row as the shortest available proof
that the network plugin is load-bearing rather than a footnote:

> "A node whose network is not correctly configured reports the **`NetworkUnavailable`**
> condition — `True` if the network for the node is not correctly configured."

The pedagogical move is worth recording: the condition is not new material, it is **Chapter 8
material re-read with Chapter 9's model in hand.** Before §1, `NetworkUnavailable` is one row
in a five-row table; after §1, it is the observable consequence of an unsatisfied network
model.

**✅ The pointer is correct.** `see Ch 8 §4 — node conditions` resolves; Ch 8 §4 owns the
condition list (`chapter-08:638-730`).

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-lifetime.md ===

## Chapter 9 — churn reframed as a precondition, not a hazard

**Added by ch-09 Stage 14, 2026-08-25.**

Chapter 9 §2 takes this shard's central fact and inverts its valence. Chapters 5 and 6 present
Pod replacement as something the reader must *cope with*; Chapter 9 presents it as the
**condition an abstraction exists for**:

> "The set of Pods running at one moment can be different from the set running a moment
> later." Notice what that is **not**: "not a failure mode, not a bug, not a degraded state to
> be recovered from. It is the normal condition of a system that replaces workloads freely."

And, from the documentation's own framing of the Service API: a stable address "for a service
implemented by one or more backend Pods, **where the individual Pods making up the service can
change over time**."

**Not a contradiction of Ch 6.** `chapter-06:431` points forward with "this churn is exactly
why something needs a stable name" — compatible framings of one idea, and Chapter 9's is the
sharper one. Recorded so a later stage does not "fix" the difference.

⚑ **One pointer to fix, and it needs more than a number.** Chapter 9 §2 emits `see Ch 5 §3 —
Pod ephemerality`, adding "where you were told **in as many words** that this fact is the
premise of Chapter 9." Ch 5 **§4** is the ephemerality section, but it points forward to
Chapter 6, not Chapter 9; the "premise of Chapter 9" sentence lives at `chapter-05:365`, in
**Ch 5 §1**, and is about the *Pod holding the address*, not about ephemerality. Two clean
options: point at **Ch 5 §1** and keep the claim, or point at **Ch 5 §4** and drop "in as many
words." Retargeting the number alone leaves the claim false.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/optional-components.md ===

## Chapter 9 — kube-proxy joins the optional set

**Added by ch-09 Stage 14, 2026-08-25.**

> "If you use a network plugin that implements packet forwarding for Services by itself, and
> provides equivalent behavior to kube-proxy, then you do not need to run kube-proxy on the
> nodes in your cluster." Cilium "can act as a replacement for kube-proxy."

Two things worth recording, because they pull in opposite directions and both matter:

1. **kube-proxy is optional.** "If you meet a cluster running no kube-proxy at all, nothing is
   missing." It is one implementation of one job.
2. **This is NOT an instance of `[[absent-component-pattern]]`.** The job is still being done —
   by the plugin, in its own data plane. The pattern is *nothing acts*; this is *something else
   acts*. Chapter 9 keeps these apart correctly and the shard should preserve the distinction.

The satisfying structural point: **the plugin that implements the network model can also
implement the Service data plane**, which is a good inoculation against reading kube-proxy as
load-bearing architecture.

Also confirmed here: **cluster DNS is optional in the same formal sense** — "a built-in
Kubernetes service launched automatically using the addon manager cluster add-on," i.e. an
addon, not a component. Chapter 3 §4 established that framing and Chapter 9 §7 does not
disturb it.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D2.1 — Container Orchestration › Networking | Chapter 9 | deep (1 sub-objective gap) | — |

<!--
D2.1 notes (Stage 14, ch-09, 2026-08-25):

- Competency name is "Networking", under domain D2 "Container Orchestration" at 28%.
  Source: cncf-kcna-curriculum-pdf-2026-08-23.md:14 -- "28% - Container
  Orchestration: Networking; Security; Troubleshooting; Storage".

- D2.1 IS SHARED WITH CHAPTER 10. arc-outline.md:211 assigns Ch 10 the same
  competency (Ingress, Gateway API, NetworkPolicy). Chapter 9 is FIRST coverage;
  Chapter 10 completes it. Do not mark D2.1 closed on this row alone.

- All eight sections carry objectives: ["D2.1"].

- CNCF publishes DOMAIN weights only, not COMPETENCY weights. The chapter's ~7% is
  an authored allocation and the metadata line discloses it. Unchanged since Ch 7.

- ONE SUB-OBJECTIVE ELEMENT SHIPS AS A GAP: Service port mechanics. port /
  targetPort / nodePort and the node-port range are assigned to Ch 9 Section 3 by
  the B7 ledger and appear NOWHERE IN THE BOOK -- verified across all ten shipped
  chapters. This is now a downstream contract breakage, not just a local omission:
  the B6 skeleton plans Ch 16 Section 4 around "port vs targetPort" REFERRING BACK
  TO CHAPTER 9. Blocker is plumbing, not research -- k8s-docs-service-ports-2026-08-24
  was fetched 2026-08-24 and never written to sources/; body survives in
  research-manifest.md Section 3. Record as a gap, not deep.

- FIRST D2 ROW. D1 is complete at 44% (Ch 2, 3, 7, 8). ch-08 recommended a
  domain-level coverage audit before Part III; Part III has now started, so the
  audit is overdue rather than upcoming.

- STILL UNRECORDED, SEVENTH CHAPTER RUNNING: D1.4 (Chapter 2), because Chapter 2's
  Stage 14 never ran. Flagged by ch-03 and unresolved. Any domain-level audit will
  read D1 as incomplete until this is backfilled.
-->
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

| Tested topic | Original chapter | Retested in |
|---|---|---|
| two containers, one port space, `localhost`, one Pod IP | ch 5 §1 | ch 9 — ☆ Bearings #1 item 2 |
| rolling update replaces every Pod, and every address with it | ch 6 §4 | ch 9 — ☆ Bearings #1 item 4 |
| a Service is a *different controller reading the same labels* | ch 6 §3 | ch 9 — ☆ Bearings #2 item 1 |
| three containers → one address, one endpoint | ch 5 §1 | ch 9 — Practice Q2 |
| one Pod, two independent selectors, no coordination | ch 4 §5 | ch 9 — Practice Q9 |
| readiness probe → the object it acts in | ch 5 §7 | ch 9 — Practice Q11 |
| a bare service name resolves in the caller's namespace | ch 4 §3 | ch 9 — Practice Q21 |

<!--
Chapter 9 retrieval accounting (Stage 14, 2026-08-25):

- 7 tagged items / 37 graded items (15 Bearings + 22 Practice) = 18.9%.
  B3 sets Ch 9 in the 20-25% band. BELOW FLOOR.

- >=4-BACK FLOOR SATISFIED. Practice Q9 and Q21 both draw on Ch 4 -- five chapters
  back. B3 requires at least one such item from Ch 8 onward.

- DISTRIBUTION IS THE REAL PROBLEM, NOT THE TOTAL. Bearings #1 has two tagged
  items, #2 has one, #3 has NONE.

- CHEAPEST FIX, AND IT ALSO CLOSES A CANON DEFECT: tag Practice Q6 or Q13
  [retrieval: ch3]. Q6 is the bare-metal type: LoadBalancer Service that waits
  indefinitely; Q13 is the Service with a cluster IP, a DNS record and zero
  endpoints. Both are already-written instances of B3 cross-cutting theme #3
  ("an object without its component does nothing"), and shipped Chapter 10 cites
  BOTH by section number as the reader's own prior encounters (chapter-10:723,
  chapter-10:1567).

  That single tag yields 8/37 = 21.6%, inside the band, AND:
    * discharges a scheduled cross-cutting theme in the chapter that supplies its
      two best instances;
    * adds a SIX-chapters-back item, the longest span in the chapter;
    * forces the Section 3 / Section 4 prose to retrieve Chapter 3's phrase, which
      removes the four-instance contradiction documented in
      concepts/absent-component-pattern.md;
    * requires NO new question and NO fetch.

  Strictly better than adding a question. If the author prefers the item in
  Bearings #3 (where the distribution gap actually is), Q13's content can be
  restated as a sixth Bearings item -- but that costs a question and fixes nothing
  the tag does not already fix.

- ALL SEVEN TAGS VERIFIED ACCURATE against shipped chapter text on disk. Three
  match the source chapter's wording verbatim (Bearings #2 item 1 reproduces
  chapter-06:485's phrase exactly).

- SOUNDINGS LOAD IS INVERTED. Items 2-5 pretest Ch 4, 5 and 6 -- correct Soundings
  design, excluded from the budget per B3 decision 2, and not counted above. Worth
  recording that this chapter's PRE-test load on earlier chapters exceeds its
  POST-test load, which is the inverse of the usual shape and may explain the low
  graded rate.

- CONTROL-LOOP THEME BORNE OFF-SCHEDULE, SECOND CHAPTER RUNNING. ch-03 records the
  chain as Ch 3->4->6->11->15->17. Chapter 8 bore it anyway; Chapter 9 bears it
  TWICE. Two consecutive off-schedule chapters is a schedule defect, not a one-off.
  Settle before Ch 11.

- STANDING GAP, FOURTH CHAPTER RUNNING: book-outline/retrieval-architecture.md is
  NOT the B3 document -- re-verified this pass; it is a permission-failure message
  plus a prose summary. The per-chapter schedule was never written to disk.
  arc-outline.md carries B3's stated figures forward marked [B3] and RECONSTRUCTS
  the rest marked [B5-reconstructed], which is a partial mitigation, not a
  replacement. This log remains the only durable record of what has actually been
  retrieved.
-->
=== END APPEND ===
```

---

**Nothing above reaches disk on its own.** I re-verified rather than inheriting: `stages.py` gives stage 14 exactly one output (`kb-manifest.md`), no Python file in `certcomp` parses `=== WRITE` or `=== APPEND`, and `Book-KCNA/knowledge-base/` does not exist. **Nine chapters' knowledge base now sits unapplied across nine manifests.** Replay must run ch-01 → ch-09 in order, and eleven shards must be **appended, not overwritten** — `absent-component-pattern.md`, `control-loop.md` and `pluggable-interface-pattern.md` each carry a prior decision or an open conflict that a naïve overwrite would delete.

Four things I found that the integration report did not, in priority order:

1. **Chapter 9 tells the reader four times that the absent-component pattern is nameless until Chapter 10.** Chapter 3 §4 named it, Chapter 6 §8 retrieved it by name, and shipped Chapter 10 credits Chapter 3 explicitly. The chapter followed `arc-outline.md:218`, which was overtaken by shipped Chapter 3 — so this is a scaffolding defect, not a drafting one. The fix is one tag on Practice Q6 or Q13, and it simultaneously lifts retrieval from 18.9% to 21.6%, inside B3's band, with no new question.
2. **Both BINDING scaffolding artifacts carry a wrong kube-proxy mode list** — they specify `userspace` and omit `kernelspace`, and the chapter grades `userspace` as a wrong answer in Practice Q16. The chapter is right; fix the artifacts.
3. **The B7 ledger independently confirms integration F1** (the skeleton is stale, not the chapter) and needs a row-level remap I've specified — plus a content fix, since it also mispins Virtual IP to §2 when the chapter defines it in §6.
4. **The British-spelling regression is now two chapters running and slightly worse** (Ch 9: 22, Ch 8: 21, Ch 4: 0), which gates two of the strongest voice-exemplar nominations exactly as it did for Chapter 8.
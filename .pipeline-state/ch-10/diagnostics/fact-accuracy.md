# Fact-Accuracy Audit — Chapter 10

**Mode detected: STANDARD.** The `Cached sources` section carries 21 populated snapshots, and the draft carries ~144 inline `[source:]` tags. Untagged factual claims are therefore FAIL, not advisory.

**Input note.** `draft-v2.md` was not available; this audit ran against the inlined `draft-v1.md` per the fallback instruction. Because the draft arrived inlined rather than as a file, findings are anchored by **section › subheading › excerpt** rather than by line number. Every anchor below is greppable against `draft-v1.md`.

**Scope note.** Cross-chapter assertions ("Chapter 9 told you…", "Chapter 3 gave you the sentence…") are *not* checked here — verifying those against the section skeleton and shipped chapters is the integration stage's job. This audit checks the draft against the cached snapshot corpus only.

## Summary

- Total factual claims inspected: **171**
  - Tagged claim instances: 144
  - Untagged assertions weighed for factual content: 27 (18 judged non-factual, internal, or explicitly framed as the book's own inference / the reader's priors — see *Framing accepted*, below)
- Tagged claims verified: **138**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — all 11 distinct snapshot IDs cited by the draft are present in the corpus
- **Untagged factual claims (FAIL): 4**
- **Contradicted claims (FAIL): 0**
- Minor discrepancies (WARN): **14** (6 tagged-claim scope/attribution drifts, 5 untagged-but-defensible assertions, 3 internal-consistency defects)

**Headline:** no tagged claim contradicts its snapshot, and every YAML manifest in the chapter is byte-faithful to the corpus. The failures cluster in one place — the **Soundings answer key**, which asserts external protocol facts and carries zero source tags across all eight answers — plus one unsourced architectural count in *The Voyage Ahead*.

---

## FAIL — Untagged factual claims

### §Soundings › answer 1 — "The `Host` header, available only after the TCP connection is established and the request has been sent… HTTPS carries an earlier tell in the SNI field of the TLS handshake"

**Why it's a factual claim:** Two assertions about protocol behaviour attributed to no authority: (a) that host-based routing reads the `Host` header, (b) that TLS SNI carries the hostname earlier in the handshake. (b) appears **nowhere else in the chapter**, so it is never sourced at any point.

**Snapshot support available:** `k8s-docs-gateway-api-depth-2026-08-24` — "the reverse proxy receives the HTTP request and uses the `Host:` header to match a configuration". `k8s-docs-ingress-depth-2026-08-24` — "they will be multiplexed on the same port according to the hostname specified through the SNI TLS extension (provided the Ingress controller supports SNI)".

**Fix:** Tag both halves. The SNI clause should also inherit the snapshot's own hedge — the cached text conditions SNI multiplexing on *the Ingress controller supporting SNI*, which the draft's flat parenthetical drops.

---

### §Soundings › answer 3 — "All four Service types operate on addresses and ports."

**Why it's a factual claim:** A categorical assertion about the behaviour of every Kubernetes Service type. Untagged, and never restated with a tag anywhere in the chapter.

**Snapshot says** (`k8s-docs-service-2026-08-23`), on the fourth type: "**ExternalName** — Maps the Service to the contents of the externalName field… The mapping configures your cluster's DNS server to return a CNAME record with that external hostname value. **No proxying of any kind is set up.**"

**Fix:** Tag it *and* narrow it. ExternalName does not operate on addresses and ports at all — it is a DNS-level alias with no proxying. The load-bearing conclusion (no Service type can split `/checkout` from `/catalog`) survives intact; the premise as written does not. Suggested: "None of them reads HTTP. Three of the four operate on addresses and ports; the fourth, ExternalName, is a DNS alias with no proxying at all `[source: k8s-docs-service-2026-08-23]`."

---

### §Soundings › answer 8 — "At the reverse proxy or load balancer at the edge, which holds the certificate and private key. The application server behind it receives plain HTTP."

**Why it's a factual claim:** Asserts where TLS terminates and what the backend receives. This is the same fact §2 teaches under a tag; here, at first assertion, it is bare.

**Snapshot says** (`k8s-docs-ingress-depth-2026-08-24`): "The Ingress resource only supports a single TLS port, 443, and **assumes TLS termination at the ingress point (traffic to the Service and its Pods is in cleartext)**." Plus, for the key material: "The TLS secret must contain keys named `tls.crt` and `tls.key`."

**Fix:** Add `[source: k8s-docs-ingress-depth-2026-08-24]`. No wording change needed.

---

### §The Voyage Ahead — "You have collected two now: CRI at the container runtime, CNI at the network. Chapter 11 brings CSI, and by the time Chapter 17 collects all four in one place…" (and §5's cross-bearing "**CRDs as one of the four pluggable interfaces**")

**Why it's a factual claim:** Asserts that Kubernetes has *four* pluggable interfaces and, in the §5 cross-bearing, asserts membership of that set. Both untagged. No cached snapshot uses the phrase "four pluggable interfaces" or enumerates four.

**Snapshot says** (`k8s-docs-extending-kubernetes-2026-08-23`) — the only cached source that enumerates extension points — lists **six** extension points, and under point 6, *Infrastructure extensions*, **five** items: "Device Plugins (custom hardware); Storage plugins (CSI…); Network plugins (CNI…); Container runtime (CRI…); kubelet image credential provider plugins." CRDs are listed **separately**, under point 3, *API extensions* — not among the infrastructure plugins.

**Why this is worse than a missing tag:** The two mentions disagree with each other. If CRDs are one of the four (§5), the set is CRI/CNI/CSI/CRD — but the reader met CRDs in Ch 6, so "you have collected two now" is wrong. If the fourth is device plugins, §5's cross-bearing is wrong. Either way one of them needs to change, and the snapshot's taxonomy supports neither grouping as stated.

**Fix:** Decide the set, then either (a) source it — the closest defensible framing is "the interfaces where Kubernetes hands off to an implementation: CRI, CNI, CSI, and device plugins `[source: k8s-docs-extending-kubernetes-2026-08-23]`," dropping CRDs from the count and repairing §5's cross-bearing to point at API extensions instead — or (b) open a research gap for a source that enumerates a canonical "four interfaces" set, if the exam is calibrated against one. Note that the snapshot's fifth infrastructure item (image credential provider plugins) makes any bare "four" a book-side simplification that should be owned as such.

---

## FAIL — Contradicted claims

**None.** Every tagged claim's substance is supported by the snapshot it cites. Six carry scope or attribution drift and are filed as WARN below.

---

## WARN — Minor discrepancies

### 1. §1 › "The layer boundary" and Practice Q1 answer — "layer 4" / "layer 7" attributed to the network-model snapshot

**Tag:** `[source: k8s-docs-network-model-2026-08-23]`
**Snapshot says:** the page uses OSI layer numbers exactly once, and about a different object — "Network Policies — control traffic flow at the IP address or port level (OSI layer 3 or 4)". It never assigns a layer number to Services, `type: LoadBalancer`, Ingress, or Gateway API.
**Draft says:** "Everything in Chapter 9 operates at **layer 4**… Everything in §2 through §5 operates at **layer 7**," and, in the Practice Q1 answer, "Chapter 9's Service types operate at layer 4; Ingress operates at layer 7," with the tag immediately following.
**Why it matters:** The layer labels are a sound and conventional gloss, but the tag placement reads as if the snapshot supplies them. §6's layer-3/4 claim for NetworkPolicy *is* directly attested; §1's is not.
**Recommended fix:** Keep the framing, mark its provenance. Either move the tag so it clearly governs only the "protocol-aware routing" sentence, or add a half-line: "the layer numbering is ordinary practitioner vocabulary; the documentation attaches OSI layers only to NetworkPolicy."

### 2. §1 › "The layer boundary" and Practice Q1 answer — "protocol-aware HTTP/HTTPS routing" attributed to both Gateway API and Ingress

**Tag:** `[source: k8s-docs-network-model-2026-08-23]`
**Snapshot says:** in its sub-topic list the phrase belongs to Ingress alone — "**Ingress** — protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths; **Gateway API** — dynamic infrastructure provisioning and advanced traffic routing."
**Draft says:** "describing Gateway API and Ingress as protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths."
**Recommended fix:** Substantively defensible — `k8s-docs-gateway-api-depth-2026-08-24` does call Gateway API "protocol-aware" — but the attribution as written merges two snapshot lines into one. Either attribute the phrase to Ingress only, or cite the Gateway depth snapshot alongside for the Gateway half. The same sentence recurs in the Practice Q1 answer and needs the same treatment.

### 3. §1 › "North-south and east-west" — the definitions are the book's; only the pairing is attested

**Tag:** `[source: k8s-blog-gateway-api-north-south-east-west-2026-08-24]`
**Snapshot says:** "While the initial focus of Gateway API was always ingress (north-south) traffic… the same basic routing concepts should also be applicable to service mesh (east-west) traffic." That is the whole of it — the blog pairs the terms with ingress and mesh but never defines them.
**Draft says:** "**North-south** traffic enters the cluster from outside. **East-west** traffic moves between Pods inside it," then attributes the pairing.
**Recommended fix:** Two points. (a) The definitions are derivable from the pairing but are not stated by the source; a half-clause owning them as industry vocabulary would close the gap the research manifest's SOURCE NOTE originally opened. (b) The snapshot's own header warns that this is "a blog post, not the documentation — authoritative as a Kubernetes-project publication but **NOT normative reference documentation**." The chapter cites it exactly as it cites `kubernetes.io/docs` pages. Consider a provenance beat, or accept it and note the decision in the retro.

### 4. §1, §Soundings answer 2, §Chapter Summary — "One external address per Service"

**Tag:** none (untagged; treated as inherited Ch 9 material).
**Snapshot says:** `k8s-docs-service-2026-08-23` on LoadBalancer says only "Exposes the Service externally using an external load balancer. Kubernetes does not directly offer a load balancing component." No cached snapshot states a one-address-per-Service ratio, nor the cost consequences ("fifty line items on a cloud bill").
**Why it matters:** This is the premise the whole of §1 rests on, and the chapter's Summary states it as a bare fact.
**Recommended fix:** Confirm it was sourced in Ch 9; if so, no edit needed beyond a cross-bearing. If it was not sourced there either, this becomes a chapter-crossing research gap, not a Ch 10 defect. The cost enumeration is plainly the book's operational reasoning and reads fine as such.

### 5. §2 › "What Ingress is" — "Four capabilities. That is the complete list as the documentation gives it."

**Tag:** `[source: k8s-docs-ingress-depth-2026-08-24]`
**Snapshot says:** "An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL / TLS, and offer name-based virtual hosting." The sentence is a "may be configured to" enumeration; the page never claims it is exhaustive.
**Recommended fix:** Soften to "Four capabilities, as the documentation enumerates them." The exhaustiveness claim is the book's addition, and Practice Q3 rests on it ("Which four capabilities…"), so the item's authority depends on the wording holding up.

### 6. §2 › TLS — "The Secret must be of type `kubernetes.io/tls`"

**Tag:** `[source: k8s-docs-ingress-depth-2026-08-24]`
**Snapshot says:** the prose states only "The TLS secret **must contain keys named `tls.crt` and `tls.key`**." The `type: kubernetes.io/tls` line appears in the *example manifest*, not in a requirement sentence.
**Recommended fix:** The requirement is real (and `k8s-docs-secret-2026-08-23` lists `kubernetes.io/tls` as the built-in type for "data for a TLS client or server"), but as cached it is a strengthening of an example into a rule. Either cite the Secret snapshot alongside, or phrase as "the example Secret is of type `kubernetes.io/tls`, and must contain keys named `tls.crt` and `tls.key`."

### 7. §2 and Practice Q2 answer — "an Ingress routes to Services rather than directly to Pods"

**Tag:** `[source: k8s-docs-ingress-depth-2026-08-24]`
**Snapshot says:** "A backend is a combination of Service and port names… **or a custom resource backend by way of a CRD**," and documents a `Resource` backend at length: "A `Resource` backend is an ObjectRef to another Kubernetes resource… A common usage for a `Resource` backend is to ingress data to an object storage backend with static assets."
**Recommended fix:** Omitting `Resource` backends from the teaching is a defensible scope call. The categorical wording is what drifts — a candidate who has read the Ingress page has seen a non-Service backend. Soften to "routes to Services (the case this chapter covers) rather than directly to Pods."

### 8. §6 › "Getting default-deny with no deny rule" — `ingress: [- {}]` is not valid YAML

**Tag:** `[source: k8s-docs-network-policies-depth-2026-08-24]`
**Snapshot says:** the allow-all manifest is block style —
```
  ingress:
  - {}
```
**Draft says:** "a policy with `podSelector: {}` and a single empty rule, `ingress: [- {}]`".
**Recommended fix:** `[- {}]` mixes flow and block sequence syntax and will not parse. Inline flow style is `ingress: [{}]`. Fix the inline rendering, or quote the block form from the snapshot.

### 9. §4, §Bearings #2 answer 2, §Exam Alert item 4 — "the project recommends Gateway **for new work**"

**Tag:** `[source: k8s-docs-ingress-depth-2026-08-24]`
**Snapshot says:** "The Kubernetes project recommends using Gateway **instead of** Ingress." No new-work qualifier.
**Draft says:** three separate restatements add "for new work."
**Why it matters:** §4's whole thesis is word-level precision about what the project did and did not say, so a silently added qualifier is more costly here than it would be elsewhere. The Practice Q11 answer states it correctly and unqualified — so the chapter is already inconsistent with itself.
**Recommended fix:** State the recommendation as written, then give the new-work reading as the book's operational gloss, which is what §4 explicitly does two paragraphs later ("The honest practitioner reading is…"). That paragraph is well-built; the three shorthand restatements undercut it.

### 10. §2 › Snag — "If you have ever written an nginx `location` block, this is *almost* the semantics you expect"

**Tag:** none. Third-party product behaviour; no nginx snapshot exists in the corpus.
**Recommended fix:** Low risk — it is hedged, it is a reader-experience appeal rather than an authority claim, and the Kubernetes-side fact it decorates is fully sourced. Either leave it and accept it as an analogy, or drop the product name. Do **not** promote it to a sourced comparison without a cached nginx `location`-matching reference; the corpus deliberately excludes third-party controller products.

### 11. §5 › Worth Securing — "which is a large part of why so much real-world Ingress configuration ends up living in controller-specific annotations"

**Tag:** the adjacent quote is tagged; the causal claim is not.
**Snapshot says:** two supporting facts, no causal link. `k8s-docs-ingress-depth-2026-08-24`: "Ingress controllers frequently use annotations to configure behavior." `k8s-docs-gateway-api-depth-2026-08-24`: capabilities "that were only possible in Ingress by using custom annotations."
**Recommended fix:** Both facts are attested; the *because* is the book's. §7 handles exactly this situation exemplarily ("the dependency is sourced, the inference about detectability is ours"). One clause of the same discipline here would settle it.

### 12. §7 › Dead Reckoning — "As of the current release" (version anchor)

**Tag:** `[source: k8s-docs-network-policies-depth-2026-08-24]`
**Snapshot says:** "As of Kubernetes `{{< skew currentVersion >}}`" — a version-templated claim that resolves at render time.
**Status:** already flagged in-draft by an AUTHOR-REVIEW comment. Confirming the finding: "as of the current release" is faithful to the template but leaves the reader with no anchor, and the ten-item list is the kind of content that decays. **Recommended fix:** pin a concrete version at print time, or add an explicit decay note. Do not leave it to the reader to infer which release "current" means.

### 13. Header note and §Exam Alert › "A note on frequency" — negative claims about CNCF publication practice

**Excerpts:** "CNCF publishes no per-competency weights"; "the exam's question distribution is not published."
**Tag:** none. These are unfalsifiable against the current corpus: `cncf-kcna-curriculum-pdf-2026-08-23` publishes four domain-level percentages and nothing finer, which is *consistent with* both claims but cannot establish them — absence in one snapshot is not absence in CNCF's publications.
**Recommended fix:** Both claims are almost certainly true and both are load-bearing for the book's honesty posture, so they should be verifiable. **Open a research gap** for a snapshot of the Linux Foundation KCNA exam/registration page (`training.linuxfoundation.org/certification/kubernetes-cloud-native-associate/`). The corpus currently holds **no** exam-logistics source at all — no question count, duration, passing score, price, retake policy, or distribution. This chapter makes no positive claims of that kind (good), but the two negative ones cannot be upgraded past ADVISORY until that page is cached.

### 14. Internal-consistency defects (not source-derived; flagged for the revision stage)

Three arithmetic/count errors verifiable against the draft itself:

- **§Attention Budget.** The header states "**Total time: ~85 minutes**." The table's own per-row figures sum to **124** (10+6+12+8+6+6+12+6+14+8+6+5+25). The same table also contradicts "*If you only have 15 minutes: read §3, §4, and §6, and take Bearings #3*" — those four rows total **34 minutes**.
- **§Practice Questions.** "Seventeen questions. **Four** draw on earlier chapters, and they are tagged." Seventeen is correct. The retrieval tags number **three**: Q2 `[retrieval: ch9]`, Q7 `[retrieval: ch3]`, Q17 `[retrieval: ch3]`.
- **Two different "four"s.** §3 says "This is the **first of the four**" (Ingress), counting forward to Ch 13 and Ch 17. §8 says "You have now seen this **four times**, and two of the four were your own from last chapter," counting backward, which makes Ingress the third. Both readings are individually coherent; sharing a chapter without distinction, they are not. Worth one disambiguating clause.

---

## Framing accepted (no action)

Eighteen untagged assertions were weighed and cleared because the draft explicitly marks them as the book's own reasoning or as the reader's priors, rather than presenting them as documented fact. Two deserve naming as models of the discipline the rest of the chapter should match:

- **§7 › "Why this one is worse"** — "That is not a documented claim; the source states the plugin dependency and the no-effect consequence and stops there. The characterisation of the failure as *silent*… is this book's reasoning about what those two documented facts imply." Exemplary. The chapter's single most valuable claim, correctly fenced.
- **§5 › AUTHOR-REVIEW on `parentRefs`** — correctly identifies "an HTTPRoute attaches to a Gateway via `parentRefs`" as the book's prose gloss over a mechanism attested only inside an example manifest, matching the extractor's own note in `k8s-docs-gateway-api-depth-2026-08-24`. No further action needed.

Also cleared: the §Soundings question-4 firewall generalisation (framed as elicitation of reader priors, not as an authority claim), the CIDR gloss in §6 (correct, definitional), and the "Voyage Progress" / attention-cost apparatus (authorial).

---

## PASS — Verified claims

Sampled and confirmed against the cited snapshots. This is a subset; the full verified set is 138 tagged claim instances.

**Manifest fidelity — all eight YAML blocks byte-checked against the corpus:**

| Manifest | Snapshot | Result |
|---|---|---|
| `test-ingress` (single-Service) | `k8s-docs-ingress-depth-2026-08-24` | Exact ✓ (snapshot notes this one was re-verified against the raw example file) |
| `simple-fanout-example` | same | Exact ✓ (raw-file verified in snapshot) |
| `name-virtual-host-ingress` | same | Exact ✓ (raw-file verified in snapshot) |
| `tls-example-ingress` | same | Exact ✓ (raw-file verified in snapshot) |
| `IngressClass external-lb` | same | Exact ✓ |
| `test-network-policy` | `k8s-docs-network-policies-depth-2026-08-24` | Exact ✓ — apart from three added `# <--` comments, which are the book's and are accurate |
| `default-deny-all` | same | Exact ✓ |
| `Gateway` + `HTTPRoute` | `k8s-docs-gateway-api-depth-2026-08-24` | Exact ✓ both |

This matters given that snapshot's extraction-provenance warning: three Ingress manifests came back **fabricated** on the first extraction pass (invented hostnames and Service names). The draft uses the corrected, raw-file-verified versions throughout. No fabricated artifact survived into the draft.

**Spot-verified prose claims:**

- Domain weight 28% for Container Orchestration — `cncf-kcna-curriculum-pdf-2026-08-23` ✓
- "You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect" — verbatim ✓ (all four restatements)
- The full frozen-API Note, both bullets, quoted verbatim in §4 ✓
- "GA API versions may be marked as deprecated, but must not be removed within a major version of Kubernetes" — Rule 4a, verbatim ✓
- The hyperlink claim ("subject to the stability guarantees" → the deprecation policy page) — corroborated by the parenthetical in `k8s-docs-ingress-depth-2026-08-24` ✓
- Path-type behaviour: three types, element-wise `Prefix`, `/foo/bar` ≠ `/foo/barbaz`, `/aaa/bb` ≠ `/aaa/bbb`, longest-match-wins with `Exact` breaking ties ✓ (all five, including the Examples-table row the Snag quotes)
- Wildcard hostnames: single-label match, `*.foo.com` matches `bar.foo.com`, not `baz.baz.foo.com`, not `foobar.foo.com` ✓
- `defaultBackend` rules, all four claims including "if no `.spec.rules` are specified, `.spec.defaultBackend` must be specified" ✓
- IngressClass default-class mechanics, including the "**exactly one**" condition and the `"true"` string value of the annotation ✓
- "Ideally… should fit the reference specification. In reality… operate slightly differently" — confirmed present on **both** cited pages in near-identical words, exactly as the draft claims ✓
- Gateway API: four stable kinds; the three roles verbatim; "exactly one GatewayClass"; the bidirectional trust model; the six-step request flow; all four design principles; CRD-based installation ✓
- Gateway API appears on the cluster add-ons page under Networking and Network Policy — confirmed via the elision list in `k8s-docs-cluster-addons-2026-08-24`, which names it explicitly ✓
- NetworkPolicy: OSI 3/4; "application-centric"; the entity-word rationale; the three identifiers with both exceptions; non-isolated defaults in both directions; the `policyTypes` omission default; implicit reply traffic; additive/union/order-independent; both-ends-must-allow; empty-`podSelector`-selects-all; the AND/OR `from`-entry distinction ✓ (all verified verbatim or near-verbatim)
- The ten-item out-of-scope list — item count and content confirmed against the snapshot's own direct-count verification; the OS-component / L7 / admission-controller workaround note ✓
- CNI as a kubelet-executed binary plugin implementing pod networking — `k8s-docs-extending-kubernetes-2026-08-23` ✓
- "Kubernetes does not directly offer a load balancing component; you must provide one" — `k8s-docs-service-2026-08-23` ✓
- Gateway-as-successor framing ("supersedes", chapter subtitle) — supported, though untagged, by `k8s-docs-network-model-2026-08-23`: "The Gateway API (**or its predecessor, Ingress**)". Worth tagging at the subtitle or §5 rather than leaving to inference.
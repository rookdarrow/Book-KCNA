## Practice Questions

Eighteen questions, four options each. Four draw on earlier chapters, and they are tagged. Answers follow the full set — attempt them all before scrolling.

**1.** ⚪ Three mechanisms, three altitudes. At which OSI layer does each operate: the Service types from Chapter 9, an Ingress, and a NetworkPolicy?

A) Services at layer 4; Ingress at layer 7; NetworkPolicy at layer 7.
B) Services at layer 4; Ingress at layer 7; NetworkPolicy at layer 3 or 4.
C) Services at layer 3; Ingress at layer 4; NetworkPolicy at layer 3.
D) All three at layer 7, differing only in what they are permitted to configure.

**2.** 🔵 `[retrieval: ch9]` You need to expose an HTTP application and a message broker speaking its own binary protocol, both to clients outside the cluster. What do you need?

A) One Ingress carrying both, with a ClusterIP Service behind each.
B) One Ingress for the HTTP application with a ClusterIP Service behind it; a NodePort or LoadBalancer Service for the broker.
C) Two Ingresses, one per workload, each with a ClusterIP Service behind it.
D) No Ingress — a LoadBalancer Service for each, since an Ingress routes to Pods and both workloads have several.

**3.** ⚪ Which set correctly lists what an Ingress may be configured to provide?

A) Externally-reachable URLs for Services; load balancing; SSL/TLS termination; name-based virtual hosting.
B) Externally-reachable URLs for Services; load balancing; SSL/TLS termination; exposure of arbitrary TCP and UDP ports.
C) Externally-reachable URLs for Services; enforcement of which Pods may receive the traffic; SSL/TLS termination; name-based virtual hosting.
D) Externally-reachable URLs for Services; load balancing; end-to-end TLS all the way to the Pods; name-based virtual hosting.

**4.** 🔵 An Ingress rule has `host: shop.example.com` and two path entries, `/catalog` and `/checkout`, each naming a different backend Service. Which shape is this, and what is the rule reading in order to decide?

A) Name-based virtual hosting; the rule is reading the `Host:` header.
B) Simple fanout; the rule is reading the HTTP URI — the path.
C) A single-service Ingress; the rule reads nothing, because `defaultBackend` sends everything to one Service.
D) Name-based virtual hosting; the rule is reading the path, because a `host` is present.

**5.** 🟡 An Ingress path is configured with `pathType: Prefix` and `path: /aaa/bb`. A request arrives for `/aaa/bbb`. Does it match?

A) Yes — `bb` is a prefix of `bbb`, and that is what `Prefix` means.
B) No — `Prefix` matches element by element, and `bb` and `bbb` are different elements.
C) No — `Prefix` matches only the configured path itself and nothing longer.
D) Undeterminable from the manifest, because `pathType` semantics are left to the controller.

**6.** ⚪ A cluster runs one Ingress controller. An engineer applies an Ingress manifest with no `ingressClassName` field. Under what condition does it still get handled?

A) Whenever at least one IngressClass exists in the cluster.
B) When exactly one IngressClass is marked as default, by the `ingressclass.kubernetes.io/is-default-class` annotation set to `"true"`.
C) Always — with one controller installed, there is nothing else the Ingress could mean.
D) Never — `ingressClassName` is a required field and the manifest will be rejected.

**7.** 🔵 `[retrieval: ch3]` Chapter 3 said a controller watches for objects and drives reality toward what they describe. An Ingress controller is one. What does it watch, and what does it change?

A) It watches Ingress objects and the Services they reference, and changes a load balancer — or the edge router, or additional frontends — to match.
B) It watches Ingress objects and changes the Services they reference.
C) The API server watches Ingress objects and configures the load balancer; the controller only validates the manifest.
D) It watches Pods and changes the Ingress object's status to match.

**8.** 🔵 Two objects, both correct as written, both doing nothing: an Ingress on a cluster with no Ingress controller, and a NetworkPolicy on a cluster whose network plugin does not implement NetworkPolicy. What is absent in each, and in what one respect do the two situations differ?

A) The controller and the plugin. They differ in nothing that matters — both fail identically.
B) The controller and the plugin. They differ in what you can see: one produces traffic that visibly fails to arrive, the other produces no signal at all.
C) A `defaultBackend` and an `ipBlock`. Both objects are incomplete as written.
D) The controller and the plugin. They differ in that the Ingress is rejected at admission and the NetworkPolicy is accepted.

**9.** ⚪ What has the Kubernetes project said about the Ingress API, in both of its halves?

A) That it is deprecated, and scheduled for removal in a future release.
B) That it is generally available and subject to the stability guarantees for GA APIs with no plans for removal — and that it is no longer being developed, with no further changes or updates.
C) That it is generally available, fully supported, and actively developed for new work.
D) That it is no longer being developed, and therefore deprecated by definition.

**10.** 🔵 You are choosing an API for external HTTP routing on a system being designed today. Which does the Kubernetes project recommend, and does that recommendation mean the other one will stop working?

A) Gateway. Yes — Ingress will be removed once Gateway API reaches GA.
B) Gateway. No — Ingress is GA, carries the GA stability guarantees, and has no removal plans.
C) Ingress, because it is GA and Gateway API is not present in a default cluster.
D) Neither; the project is explicitly neutral between the two.

**11.** 🟡 Express one requirement twice — one host, two paths, two backend Services — first in the Ingress vocabulary, then in the Gateway API vocabulary, with the owning role for each Gateway API resource.

A) Ingress: one Ingress with one rule and two paths. Gateway API: one Gateway with two paths — the same object renamed, owned by the application developer.
B) Ingress: one Ingress with one rule and two paths, plus the two Services and a controller to fulfil it. Gateway API: a GatewayClass (infrastructure provider), a Gateway (cluster operator), and an HTTPRoute with two path matches and two `backendRefs` (application developer).
C) Ingress: one Ingress per path, so two. Gateway API: one HTTPRoute per path, so two, both owned by the cluster operator.
D) Ingress: one Ingress and one IngressClass. Gateway API: one Gateway and one GatewayClass — HTTPRoute being the Gateway API name for an IngressClass.

**12.** 🔵 In Gateway API, how many GatewayClasses does a Gateway reference, and how many Routes may attach to one Gateway?

A) Exactly one GatewayClass; many Routes.
B) Many GatewayClasses; exactly one Route.
C) Exactly one of each.
D) Many of each.

**13.** 🔵 A Pod is selected by a NetworkPolicy whose `policyTypes` lists only `Ingress`. What is permitted outbound from that Pod?

A) All outbound traffic.
B) No outbound traffic — declaring one direction isolates both.
C) Outbound traffic only to Pods in the same namespace.
D) Outbound traffic only to the peers named in the policy's `ingress` list, applied in reverse.

**14.** 🟡 Namespace `prod` contains Pods `web`, `api`, and `db`. One NetworkPolicy exists: it selects `db` and permits ingress from `app: api`. It declares no egress rules. Can `web` reach `db`? Can `web` reach `api`? Can `db` reach an external address?

A) No · Yes · Yes
B) No · No · Yes
C) No · No · No
D) Yes · Yes · No

**15.** 🟡 An engineer wants to stop a Pod labelled `app: legacy` from reaching the `payments` Pods. Two existing policies currently permit that traffic. What is the approach?

A) Write a more restrictive policy selecting `payments` that excludes `app: legacy`; the more restrictive policy wins.
B) Find and remove or narrow the two policies that currently permit it. There is no deny policy to write.
C) Add a deny rule naming `app: legacy` to one of the two existing policies.
D) Apply a policy selecting `app: legacy` with `policyTypes: [Egress]` and an empty egress list, which removes only its access to `payments`.

**16.** 🟡 `[retrieval: ch4]` A single NetworkPolicy carries a selector at the top of its `spec` and further selectors underneath `ingress.from`. Which chooses what — and what happens to the policy's effect on a Pod if someone relabels that Pod out from under the top-level selector?

A) The top-level `podSelector` chooses the Pods the policy governs; the selectors under `ingress.from` choose peers. Relabelling drops the Pod out of the policy's subjects, leaving it non-isolated — less restricted, not more.
B) The top-level `podSelector` chooses the Pods the policy governs; the selectors under `ingress.from` choose peers. Relabelling drops the Pod out of every policy, and a Pod outside every policy receives nothing.
C) The selectors under `ingress.from` choose the Pods the policy governs; the top-level `podSelector` chooses peers. Relabelling changes nothing about the policy's subjects.
D) All the selectors choose peers; the policy governs the whole namespace. Relabelling narrows the peer set.

**17.** 🔵 A NetworkPolicy has been applied. The policy is correct as written, and traffic it should be blocking is still flowing. Three of the four explanations below are ones this chapter has given you. Which is the one that **cannot** be the explanation?

A) The cluster's network plugin does not implement NetworkPolicy, so the resource has no effect.
B) The traffic is node-local, or the Pod is reaching itself — neither can be blocked by any policy.
C) Another policy in the namespace permits the same traffic, and policies combine by union.
D) The policy targets the destination Service rather than the Pods behind it, so it selects nothing.

**18.** 🟡 `[retrieval: ch3]` Name the rule Chapter 3 gave you about objects and components, and every instance of it you have met in this book so far.

A) *An object without its component does nothing.* Instances: a `type: LoadBalancer` Service with no provider to fulfil it (Ch 9 §3); a Service whose selector matches no Pods (Ch 9 §4); an Ingress with no Ingress controller (Ch 10 §3); a NetworkPolicy on a plugin that does not implement NetworkPolicy (Ch 10 §7).
B) *An object without its component does nothing.* Instances: an Ingress with no Ingress controller, and a NetworkPolicy on a plugin that does not implement NetworkPolicy.
C) *An object takes effect once the API server has admitted it.* Instances: the four above.
D) *An object without its component does nothing.* Instances: a `type: LoadBalancer` Service with no provider; an Ingress with no controller; a NetworkPolicy on an unsupporting plugin; an Ingress whose `pathType` does not match the request path.

---

### Answers with Explanations

**1. B.**

The documentation attaches OSI layer numbers to exactly one of these three: network policies control traffic flow at the IP address or port level — OSI layer 3 or 4 [source: k8s-docs-network-policies-depth-2026-08-24]. The layer numbering for Services and Ingress is ordinary practitioner vocabulary rather than a documented label; what is documented is the capability difference. Ingress is described as protocol-aware HTTP/HTTPS routing using URIs, hostnames and paths, set against `type: LoadBalancer` as the simpler, less-configurable path [source: k8s-docs-network-model-2026-08-23].

The shape worth carrying out of the chapter is the round trip. §2 through §5 climb to where the request itself is readable. §6 descends again, and the descent is why §7's limits are the limits they are.

*Why A is wrong:* it puts NetworkPolicy at layer 7. That is the error behind every expectation that a policy can match a hostname, a URL path, or a Service name — and every one of those is on the published out-of-scope list precisely because the mechanism is not up there.

*Why C is wrong:* it demotes Ingress to layer 4, which would make it a variant of the Service types rather than a different altitude. If that were true, the broker in question 2 could go behind it.

*Why D is wrong:* it collapses the distinction the whole chapter is built on. A mechanism that cannot read the request cannot route on its contents, no matter what it is permitted to configure.

**2. B.** `[retrieval: ch9]`

An Ingress does not expose arbitrary ports or protocols; exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer [source: k8s-docs-ingress-depth-2026-08-24]. The HTTP application still needs a Service behind the Ingress — an Ingress backend is a combination of Service and port, which is the case this chapter covers, rather than a Pod [source: k8s-docs-ingress-depth-2026-08-24] — and a ClusterIP is sufficient, because the Ingress is what makes it externally reachable.

The point of the item is **specialisation, not replacement.** A candidate who believes Ingress supersedes the Service ladder goes looking for a way to put the broker behind the Ingress, and there is not one.

*Why A is wrong:* it is the specialisation error in its purest form. The Ingress cannot carry the broker at all, so no arrangement of Services behind it helps.

*Why C is wrong:* two Ingresses do not solve a protocol problem. Adding a second one that also cannot carry binary traffic changes nothing.

*Why D is wrong:* the premise is false. An Ingress routes to a Service and port, not to individual Pods, so "several Pods" is not an obstacle — that is what the Service is for.

**3. A.**

An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL/TLS, and offer name-based virtual hosting [source: k8s-docs-ingress-depth-2026-08-24].

*Why B is wrong:* arbitrary TCP and UDP ports are the fifth thing people assume is on the list and the one thing explicitly excluded — exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer instead [source: k8s-docs-ingress-depth-2026-08-24]. This is the single most common wrong answer about what an Ingress is for.

*Why C is wrong:* deciding which Pods may receive traffic is NetworkPolicy's job, and it lives at a different layer entirely. An Ingress routes; it does not authorise.

*Why D is wrong:* the Ingress resource assumes TLS termination at the ingress point — traffic onward to the Service and its Pods is in cleartext [source: k8s-docs-ingress-depth-2026-08-24]. "End-to-end TLS to the Pods" is the opposite of what terminating TLS means, and the distinction matters the moment anyone asks what is on the wire inside the cluster.

**4. B.**

A fanout configuration routes traffic from a single IP address to more than one Service based on the HTTP URI being requested [source: k8s-docs-ingress-depth-2026-08-24].

*Why A is wrong:* virtual hosting splits on **host**, and here there is only one host to split on. The tell is where the list lives in the manifest: several entries under `paths` is fanout; several entries under `rules`, each with its own `host`, is virtual hosting.

*Why C is wrong:* `defaultBackend` handles requests that match none of the rules, and if no `.spec.rules` are specified then `.spec.defaultBackend` must be [source: k8s-docs-ingress-depth-2026-08-24]. This manifest has rules and paths, so the rules do the deciding; the default backend is a fallback, not the mechanism.

*Why D is wrong:* it gets the mechanism right and the name wrong, which is the more dangerous half of the error. The presence of a `host` does not make something virtual hosting — *several* hosts do.

**5. B.**

`Prefix` matching is done on a **path element by path element** basis, and the documentation gives this exact case: `Prefix` with path `/aaa/bb` against request path `/aaa/bbb` is **not** a match [source: k8s-docs-ingress-depth-2026-08-24]. The elements are compared as whole labels. That `bb` happens to be a string prefix of `bbb` is irrelevant.

*Why A is wrong:* this is the misconception the rule exists to prevent, and the documentation heads it off explicitly — if the last element of the path is a substring of the last element in the request path, it is not a match [source: k8s-docs-ingress-depth-2026-08-24].

*Why C is wrong:* it over-corrects. `Prefix` does match longer request paths — `/aaa/bb/cc` matches — provided every configured element matches a whole element of the request.

*Why D is wrong:* controllers do vary in documented ways, but this is not one of them. `Prefix` semantics are pinned by the specification with a worked example. Reaching for "it depends on the controller" where the spec is explicit is the caveat from §3 applied somewhere it does not belong.

**6. B.**

If `ingressClassName` is omitted and exactly one default IngressClass exists, Kubernetes applies it, and an IngressClass is marked as default by setting the `ingressclass.kubernetes.io/is-default-class` annotation to `"true"` [source: k8s-docs-ingress-controllers-2026-08-24].

Note the "exactly one." The condition is not "at least one."

*Why A is wrong:* an IngressClass existing is not the same as an IngressClass being marked default. The annotation is the whole mechanism.

*Why C is wrong:* the number of controllers installed is not what the rule is written against. The cluster resolves the class from the IngressClass resources, not by inferring that there is only one candidate.

*Why D is wrong:* `ingressClassName` is optional, which is exactly why the default-class mechanism exists.

**7. A.**

An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends [source: k8s-docs-ingress-depth-2026-08-24]. That is Chapter 3's control-loop shape with the nouns filled in: desired state recorded in an object, a controller watching, external reality reconciled toward the description.

The value of the item is in converting a memorised component name into a recognised instance of a pattern.

*Why B is wrong:* the controller reads the Services to learn where to send traffic. It does not modify them. Reversing this makes the Ingress sound like a mutation of the Service layer rather than a layer above it.

*Why C is wrong — and this is the misconception worth naming:* the API server stores the object and serves it back. It changes nothing outside the cluster. That distinction *is* the difference between a record and a control loop, and it is the reason an Ingress with no controller sits there looking perfectly healthy.

*Why D is wrong:* it inverts the direction of the loop. The object is the input, not the output.

**8. B.**

Both are the same structural failure. Only creating an Ingress resource has no effect [source: k8s-docs-ingress-depth-2026-08-24]; network policies are implemented by the network plugin, and creating a NetworkPolicy resource without a controller that implements it will have no effect [source: k8s-docs-network-policies-depth-2026-08-24]. In both cases nothing is wrong with the object at all, which is why re-reading the YAML produces nothing, indefinitely.

The difference is what reaches you. A website that does not load is a report; nobody has to go looking. Traffic that flows when a policy says it should not produces no report from anyone, because the only party who would notice is the traffic you were trying to stop.

*One clarification on provenance:* the two "no effect" facts are documented. The characterisation of the second failure as the harder one to detect is this book's reasoning about what those two facts imply, not a documented claim.

*Why A is wrong:* structurally identical, operationally not. Treating them as the same failure is what leaves the second one running for months.

*Why C is wrong:* neither object is incomplete. A `defaultBackend` is optional when rules are present, and `ipBlock` is one of three peer identifiers, not a requirement. The whole point is that both manifests review clean.

*Why D is wrong:* the API server admits both. It stores objects; it does not check that something exists to act on them. If it rejected an Ingress on a controller-less cluster, this chapter's central pattern would not exist.

**9. B.**

Both halves, in the project's own words: generally available and subject to the stability guarantees for GA APIs, with no plans for removal; and no longer being developed, with no further changes or updates [source: k8s-docs-ingress-depth-2026-08-24].

Operationally, the first half means there is no migration emergency for what you run today. The second means there is no future capability — whatever Ingress cannot do now, it never will.

*Why A is wrong:* it drops the stability half and replaces it with the wrong status. `deprecated` is a formal state with published consequences, and Ingress has not been given it.

*Why C is wrong:* it drops the no-development half. "Fully supported" is true; "actively developed" is the part the announcement specifically denies.

*Why D is wrong:* it fuses the two halves into a conclusion neither supports. No longer being developed says nothing about removal. GA APIs may be marked deprecated, but must not be removed within a major version of Kubernetes [source: k8s-docs-ingress-depth-2026-08-24] — and Ingress has not been marked deprecated in the first place.

Offering only one of A or C would teach the other, which is why a well-built item offers both.

**10. B.**

The Kubernetes project recommends using Gateway instead of Ingress [source: k8s-docs-ingress-depth-2026-08-24]. It simultaneously states that Ingress is GA, carries the GA stability guarantees, and has no removal plans [source: k8s-docs-ingress-depth-2026-08-24]. Both facts are true at once and point in different directions, and holding both is the skill this section tests. The practical reading — that the recommendation bites hardest on work being designed today, and least on work already running — is this book's gloss, not the project's wording.

*Why A is wrong:* Ingress is already GA and already guaranteed. There is no removal event waiting on Gateway API's maturity.

*Why C is wrong:* GA status is not a recommendation, and installation friction is not either. Gateway API arrives as custom resources rather than in a default cluster [source: k8s-docs-gateway-api-depth-2026-08-24], which is a real operational cost — and it is a separate question from what the project recommends.

*Why D is wrong:* the recommendation is explicit and unqualified. Reading neutrality into it is the mirror error of reading a deprecation into it.

**11. B.**

Ingress vocabulary: one Ingress object, one rule containing two paths, each naming a backend Service and port — plus the two Services and an Ingress controller to fulfil it [source: k8s-docs-ingress-depth-2026-08-24].

Gateway API vocabulary: a GatewayClass belonging to the infrastructure provider, a Gateway belonging to the cluster operator, and an HTTPRoute attached to that Gateway via `parentRefs`, carrying two path matches and two `backendRefs`, belonging to the application developer [source: k8s-docs-gateway-api-depth-2026-08-24].

The exercise is worth doing because it shows Gateway API is not a new routing model to learn from scratch. It is the shapes you already know, redistributed across resources that belong to different owners. The routing requirement did not change. The ownership boundaries did.

*Why A is wrong — and it is the tempting one:* it reads Gateway API as a rename of Ingress. It is not. Ingress is one object with one owner; Gateway API is three objects with three owners, and that split is the reason the API exists at all. A candidate who believes it is a rename will not be able to say why anyone bothered.

*Why C is wrong:* neither API needs one object per path. An Ingress rule holds many paths; an HTTPRoute holds many matches. And routes belong to the application developer, not the cluster operator — collapsing the roles is the same error as A wearing different clothes.

*Why D is wrong:* HTTPRoute is not the Gateway API analogue of IngressClass. GatewayClass is. HTTPRoute is where the routing rules live, which in the Ingress vocabulary is the Ingress object itself.

**12. A.**

A Gateway references exactly one GatewayClass, and Routes attach to Gateways rather than the other way round, so a single Gateway carries many [source: k8s-docs-gateway-api-depth-2026-08-24].

The cardinality is the kind of detail multiple-choice exams reach for, and it also encodes the role split. One GatewayClass per Gateway, because the infrastructure provider defines one kind of thing and the cluster operator instantiates it. Many Routes per Gateway, because many application teams share one entry point without asking each other's permission — which is the problem the three-role design was drawn to solve.

<!-- AUTHOR-REVIEW: the "exactly one GatewayClass" half is stated directly by the snapshot. The "many Routes" half is the reading §5 gives of the resource model rather than a counted statement in the source; Stage 2 note #10 flagged the same wording drift in §5 and left it. If a later pass tightens §5's phrasing, tighten this key to match. -->

*Why B is wrong:* it inverts both. A Gateway that could reference many classes would have no defined infrastructure behind it, and a Gateway limited to one Route would reproduce exactly the per-Service cost problem §1 opened with.

*Why C is wrong:* one Route per Gateway is the same cost problem again, and it would make the application-developer role meaningless — every new route would require a cluster operator.

*Why D is wrong:* many GatewayClasses per Gateway would leave the infrastructure ambiguous. The class is what determines the implementation.

**13. A.**

A Pod is isolated for egress only if some NetworkPolicy both selects it and has `Egress` in its `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24]. This policy names only `Ingress`, so it does not isolate the Pod for egress at all, and the default — non-isolated, all outbound connections allowed [source: k8s-docs-network-policies-depth-2026-08-24] — still stands.

*Why B is wrong:* the two directions are declared independently. Restricting one says nothing about the other, and this is the most reliably mis-answered fact in the section.

*Why C is wrong:* namespace boundaries are not a default. Nothing about declaring ingress isolation creates an egress rule of any shape, namespace-scoped or otherwise.

*Why D is wrong:* ingress rules are not applied in reverse to egress. They govern one direction, and they govern it only because `Ingress` is named in `policyTypes`.

**14. A.**

Take them one at a time.

`web` → `db`: **no.** `db` is selected by a policy naming `Ingress`, so it is isolated for ingress, and the only inbound connections permitted are those from its node and those the policy's ingress list allows — which is `app: api` only [source: k8s-docs-network-policies-depth-2026-08-24].

`web` → `api`: **yes.** `api` is selected by no policy at all, so it remains non-isolated for ingress and all inbound is allowed [source: k8s-docs-network-policies-depth-2026-08-24]. `web` is itself unselected, so it is non-isolated for egress. Both ends allow it, which is what a connection needs.

`db` → external: **yes.** The policy declares no egress rules, and if no `policyTypes` are specified then `Ingress` is set by default [source: k8s-docs-network-policies-depth-2026-08-24]. `db` is not isolated for egress, so all outbound connections are allowed.

*Why B is wrong:* it gets `web` → `api` backwards. This is the trap — assuming one policy in a namespace changes the *namespace's* posture. It changes exactly one Pod's posture, in exactly one direction.

*Why C is wrong:* it extends the same error to `db`'s outbound traffic, treating the policy as a wall around the namespace rather than a statement about one Pod's inbound connections.

*Why D is wrong:* it swaps the directions — permitting the inbound connection the policy restricts and restricting the outbound one it never mentions.

**15. B.**

Policies are additive and combine by union [source: k8s-docs-network-policies-depth-2026-08-24], and the ability to explicitly deny is on the published out-of-scope list. If two policies permit the traffic, the only way to stop permitting it is to stop permitting it — remove the grants, or narrow them so `app: legacy` falls outside.

*Why A is wrong:* this is the specific shape a firewall-experienced engineer's mistake takes, and it deserves an explicit answer rather than a shrug. There is no precedence between policies. A new policy does not override an old one, no matter how narrow it is; it adds its allowances to theirs. The correction is not "you wrote it wrong." It is "there is no such rule to write."

*Why C is wrong:* the API has no deny verb to add. A policy expresses what is permitted; there is nowhere in the schema to say what is not.

*Why D is wrong, and this one is close enough to be worth slowing down for:* selecting `app: legacy` with `policyTypes: [Egress]` and an empty egress list *does* work — it isolates the Pod for egress and permits nothing outbound. That is the default-deny idiom, applied correctly. What it does not do is remove *only* its access to `payments`. It removes access to everything, including DNS. The mechanism is right; the claim about its scope is wrong, and the scope is the whole question.

**16. A.** `[retrieval: ch4]`

The top-level `podSelector` in a policy's `spec` chooses which Pods the policy governs. The selectors underneath `ingress.from` — `podSelector` and `namespaceSelector` there — choose which peers are permitted [source: k8s-docs-network-policies-depth-2026-08-24]. Same selector grammar from Chapter 4, two entirely different jobs, distinguished only by where they sit in the document. (The third peer identifier, `ipBlock`, is not a selector at all — it names CIDR ranges, which have no labels to select on.)

Relabel a Pod out from under the top-level selector and the policy stops selecting it. It is not partially governed or governed by a narrower rule. It is outside the policy, and since a Pod is isolated only because some policy selects it, it reverts to non-isolated: all inbound allowed [source: k8s-docs-network-policies-depth-2026-08-24].

That consequence is worth sitting with, because it runs against the instinct. Editing a label — usually the safest change anyone makes — can make a Pod **less** restricted, and nothing about the operation announces that it has done so.

*Why B is wrong:* it has the mechanism right and the consequence exactly backwards. A Pod selected by no policy is not closed; it is open. This is trap #48 arriving through a side door, and if you chose B, that is the reflex to name.

*Why C is wrong:* it inverts the two positions. Under that reading, the peers would be governed and the governed Pods would be permitted — which would make every policy in the chapter mean the opposite of what it says.

*Why D is wrong:* a policy governs the Pods its top-level selector matches, never the namespace wholesale. An empty `podSelector` selects every Pod in the namespace, but that is a selector doing its job, not a default.

**17. D.**

A NetworkPolicy selects Pods. It has no field that names a Service, and targeting Services by name is on the published out-of-scope list [source: k8s-docs-network-policies-depth-2026-08-24]. So D is not a policy that is failing — it is a policy that cannot be written. If someone reports having written it, they have written something else.

The other three are all live:

**A** is §7's case. Network policies are implemented by the network plugin, and creating a NetworkPolicy resource without a controller that implements it will have no effect [source: k8s-docs-network-policies-depth-2026-08-24].

**B** is §6's pair of unconditional exceptions — traffic from a Pod's own node, and a Pod reaching itself, are permitted regardless of any policy [source: k8s-docs-network-policies-depth-2026-08-24].

**C** is union semantics doing what union semantics do. Policies are additive [source: k8s-docs-network-policies-depth-2026-08-24], so a second policy permitting the traffic permits it, and the order the two were written in does not matter.

The discriminating move here is rejecting a candidate that sounds like a policy problem and is not one. Three plausible explanations and a mechanism that does not exist is a harder set than three wrong ones, and it is closer to what a real hour of debugging feels like.

**18. A.** `[retrieval: ch3]`

*An object without its component does nothing.* Four instances so far:

- A `type: LoadBalancer` Service on a cluster with no provider to fulfil it (Ch 9 §3).
- A Service whose selector matches no Pods (Ch 9 §4).
- An Ingress with no Ingress controller (Ch 10 §3) [source: k8s-docs-ingress-depth-2026-08-24].
- A NetworkPolicy on a plugin that does not implement NetworkPolicy (Ch 10 §7) [source: k8s-docs-network-policies-depth-2026-08-24].

If you produced all four, §8's argument is one you assembled rather than one you were handed, and the question you take forward from it — *what is watching this, and is it installed?* — is a tool rather than a slogan.

*Why B is wrong, and it is the likeliest miss:* the common error here is undercounting, not misnaming. Recalling only this chapter's two instances leaves the pattern looking like an Ingress quirk. It is the two from Chapter 9 that make it a pattern, and it is the pattern that transfers to Chapter 13's metrics-server and Chapter 17's VPA.

*Why C is wrong:* admission is not the rule. The API server admitted every one of these four objects and stored them faithfully; that is precisely why none of them announced a problem. Mistaking storage for effect is the same error as question 7's option C.

*Why D is wrong:* it states the rule correctly and then supplies an instance that is not one. An Ingress with a mismatched `pathType` is a broken object with its component present — a manifest bug, findable by reading the manifest. Every genuine instance of this pattern is an object with nothing wrong with it. If re-reading the YAML can fix it, it is not this.

---
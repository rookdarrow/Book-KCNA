## 🟡 §7 — What NetworkPolicy Cannot Do

Two facts. This section teaches two facts and nothing else, and the first one is the highest-consequence sentence in the chapter.

### The prerequisite

**Network policies are implemented by the network plugin. To use network policies, you must be using a networking solution which supports NetworkPolicy. Creating a NetworkPolicy resource without a controller that implements it will have no effect** [source: k8s-docs-network-policies-depth-2026-08-24].

Read that last clause against §3's. *Only creating an Ingress resource has no effect.* *Creating a NetworkPolicy resource without a controller that implements it will have no effect.* The same sentence, twice, four sections apart, about two objects with nothing else in common.

> ★ **Fixed Point:** **NetworkPolicies are implemented by the network plugin.** On a plugin that does not implement NetworkPolicy, the resource has no effect [source: k8s-docs-network-policies-depth-2026-08-24].

### Why this one is worse

Here is the asymmetry, and it is the reason §7 exists as its own section.

When an Ingress does nothing, **requests fail.** The site is down, somebody's monitoring fires, a user complains, and within minutes someone is looking at it. The failure announces itself.

When a NetworkPolicy does nothing, **traffic flows exactly as it did before.** `kubectl get networkpolicy` shows the object. `kubectl describe` shows the rules, correctly parsed and neatly formatted. Everything you can observe about the object says it is fine, and the observable behaviour of an unenforced policy is *identical* to the observable behaviour of a perfectly enforced policy against traffic nobody happens to be sending. There is no signal. There is nothing to notice. One failure fires a flare; the other is an uncharted rock, and nothing on the surface says it is there.

That is not a documented claim; the source states the plugin dependency and the no-effect consequence and stops there. The characterisation of the failure as *silent*, and as harder to detect than a broken Ingress, is this book's reasoning about what those two documented facts imply. Hold the two apart: the dependency is sourced, the inference about detectability is ours. We think it is sound, it is the most valuable thing in this chapter, and it is still an inference.

> ⚠ **Navigational Hazards:** *"I applied a NetworkPolicy, so that traffic is blocked"* is only true if something is enforcing it. Verify that your network plugin supports NetworkPolicy before you rely on one, and test the restriction from somewhere the policy could actually govern rather than trusting the object's existence. The object existing is a fact about etcd.

Nothing about this is careless. You wrote a correct policy, the API accepted it, `kubectl` showed it back to you, and every signal available said the thing was working. The expectation is entirely reasonable. It is the *mechanism* that offers no feedback, and that is worth knowing about in advance precisely because you will not discover it in the moment.

### Where else could it possibly live?

You can reason your way to this dependency rather than memorising it.

Chapter 9 taught that Kubernetes **defines** the network model and implements none of it: a CNI plugin does the actual work of wiring Pods onto a network *[cross-bearing: see Ch 9 §1 — CNI and the Kubernetes network model]*. CNI is one of the interfaces where Kubernetes hands off to an implementation: network plugins are binary plugins the kubelet executes, and CNI is the interface used to implement pod networking [source: k8s-docs-extending-kubernetes-2026-08-23].

So if the plugin is what moves the packets, **where else could enforcement possibly live?** Nowhere. The dependency is not an oversight or an inconvenience. It is the only place in the stack where the machinery to enforce a layer-3/4 rule exists.

If you reasoned to something like this in Soundings question 7, you derived the *dependency* before the chapter stated it. Not the consequence — the silence is the part you had no way to predict — but the dependency itself, which is the half that makes the other half inevitable. Notice that.

### What it cannot do, stated flat

> **Dead Reckoning:** The source states this list as current "as of" whichever release you happen to be reading — a version-templated claim with no fixed version behind it, so there is no release number to pin here without asserting more than the documentation does. What follows is the list as it stood at this book's source snapshot, 24 August 2026. Treat it as a list that shrinks over time; check the current page before concluding that an item on it is still impossible [source: k8s-docs-network-policies-depth-2026-08-24].
>
> The following functionality does not exist in the NetworkPolicy API [source: k8s-docs-network-policies-depth-2026-08-24]:
>
> - Forcing internal cluster traffic to go through a common gateway.
> - Anything TLS related.
> - Node specific policies. You can use CIDR notation, but you cannot target nodes by their Kubernetes identities specifically.
> - Targeting of services by name. You can target Pods or namespaces by their labels, which is often a viable workaround.
> - Creation or management of "Policy requests" that are fulfilled by a third party.
> - Default policies which are applied to all namespaces or Pods.
> - Advanced policy querying and reachability tooling.
> - The ability to log network security events, for example connections that are blocked or accepted.
> - The ability to explicitly deny policies.
> - The ability to prevent loopback or incoming host traffic. Pods cannot block localhost access, nor can they block access from their resident node.
>
> The documentation notes that some of these may be achievable through operating-system components such as SELinux, OpenVSwitch or IPTables, through layer-7 technologies such as ingress controllers and service mesh implementations, or through admission controllers [source: k8s-docs-network-policies-depth-2026-08-24].

Ten items. Three of them earn a sentence each, because they are the ones you will actually reach for.

**No TLS.** Anything TLS related is out of scope, and the documentation says outright to use a service mesh or ingress controller for it [source: k8s-docs-network-policies-depth-2026-08-24]. §2 already told you that terminating TLS at the Ingress leaves the leg from Ingress to Pod in cleartext. NetworkPolicy will not encrypt it either. That gap has an owner *[cross-bearing: see Ch 17 §5 — service mesh, mTLS, and what a mesh adds inside the cluster]*.

**No targeting Services by name.** Policies select Pods. You can target Pods or namespaces by label, which the documentation calls a viable workaround [source: k8s-docs-network-policies-depth-2026-08-24], but you cannot write `allow traffic to the checkout Service`. This is surprising after nine chapters in which nearly everything has been Service-shaped, and it is the item on this list a reader is most likely to reach for by reflex.

**No explicit deny.** §6 taught additivity as a *property* of the model: policies grant, and the model has no subtraction operator. The out-of-scope list states that same architectural fact as a *limitation* — the ability to explicitly deny is simply not in the API [source: k8s-docs-network-policies-depth-2026-08-24]. Same fact, met from the side you will actually encounter it on. You go looking for a deny rule, and there is not one.

> 🔭 **Closer Look:** "No targeting of services by name" is stranger than it looks, and it follows directly from §6. A policy selects Pods. A Service is a stable name in front of a set of Pods that *changes*; that is the entire reason Chapter 9 gave you Services. Selecting the Service would mean selecting a moving target through an indirection that the policy layer, sitting at layer 3/4 on Pod IPs, does not have access to. The restriction is a consequence of the architecture, not an omission from the API. Deeper than the exam requires.

Two objects. Four sections apart. Nothing in common except a failure mode.

---
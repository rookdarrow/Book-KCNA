## ☆ Taking Your Bearings #1

Five questions on §1 through §3 — the ceiling, the object, and the component that has to exist. Two of them reach back to earlier chapters.

**1.** ⚪ `[retrieval: ch9]` You need to expose a PostgreSQL database and a web application to clients outside the cluster. Which one can an Ingress handle, and what do you use for the other?

**2.** ⚪ One IP address serves `shop.example.com` and `blog.example.com`, routing each to a different Service. Name the Ingress capability. Then: one host, with `/catalog` and `/checkout` going to different Services. Name that one.

**3.** 🔵 A colleague applies a correct Ingress manifest to a fresh cluster. `kubectl get ingress` shows it. No traffic reaches the application. Name the most likely cause, and say what `kubectl get` actually proves.

**4.** 🔵 An Ingress is applied with no `ingressClassName` set. Name the one thing in the cluster that decides whether it is assigned a controller anyway — and say what a *second* IngressClass carrying the same marking would do to that Ingress.

**5.** 🔵 `[retrieval: ch3]` Chapter 3 gave you a one-sentence rule about objects and components. State it, then name the two things from Chapter 9 that were instances of it.

---

**Answers with Explanations:**

**1. The web application, over HTTP/HTTPS. The database needs `Service.Type=NodePort` or `Service.Type=LoadBalancer`.**

An Ingress exposes HTTP and HTTPS routes and nothing else; exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer [source: k8s-docs-ingress-depth-2026-08-24]. PostgreSQL speaks its own wire protocol over TCP, so there is nothing for a layer-7 router to read.

The framing that matters here is **specialisation, not replacement.** Ingress does not sit *instead of* the Service-type ladder. It sits *above* it, for one class of traffic. The ladder is still the correct answer for everything else, which is why §4's news about the Ingress API being frozen is survivable rather than alarming: nothing you learned in Chapter 9 is going anywhere.

Why a wrong answer is wrong: "use an Ingress for both, with different ports" fails because an Ingress does not expose arbitrary ports at all [source: k8s-docs-ingress-depth-2026-08-24]. The port fields in an Ingress rule name the *backend Service's* port, not a port the Ingress listens on.

**2. Name-based virtual hosting; simple fanout.**

Name-based virtual hosting routes HTTP traffic to multiple host names at the same IP address [source: k8s-docs-ingress-depth-2026-08-24]. Simple fanout routes traffic from a single IP address to more than one Service based on the HTTP URI [source: k8s-docs-ingress-depth-2026-08-24]. Asked as a pair on purpose: the thing to retrieve is not either definition but the **discriminator**, host versus path. Both put many Services behind one address.

The error to watch for is swapping them. The tell is in the manifest: several entries under `paths` is fanout; several entries under `rules`, each with its own `host`, is virtual hosting.

**3. No Ingress controller is installed. `kubectl get` proves only that the object exists.**

Only creating an Ingress resource has no effect; a controller must be present to satisfy it [source: k8s-docs-ingress-depth-2026-08-24]. `kubectl get ingress` returning your object tells you a record is in etcd and the API server will serve it back. It is a fact about storage. It is not a fact about routing, and nothing in that output is evidence that any component has ever looked at the object.

Nothing here is a mistake on your colleague's part. The manifest is correct, the expectation was reasonable, and the missing piece is invisible from the object. That is precisely what makes this pattern worth learning as a *first* question rather than a last resort.

**4. An IngressClass marked as the cluster default. A second one carrying the same marking does not widen the net — it removes it, and the Ingress can no longer be created at all.**

Setting the `ingressclass.kubernetes.io/is-default-class` annotation to the string `"true"` on an IngressClass makes it the cluster default, and new Ingresses that do not specify an `ingressClassName` are assigned that class [source: k8s-docs-ingress-depth-2026-08-24]. The condition is **exactly one**. If more than one IngressClass is marked default, an Ingress that omits `ingressClassName` cannot be created; the resolution is to ensure at most one carries the marking [source: k8s-docs-ingress-depth-2026-08-24].

The instinct to correct: more defaults feels like more coverage. It is the opposite. Two defaults do not give an unclassed Ingress two chances to be adopted — they take away the one chance it had, because the cluster now has no way to choose.

Worth holding next to question 3. Both are the same failure in the end — an object that never reaches a controller. But this one fails at the moment you apply it, and that one applies cleanly and then quietly does nothing. Only one of them tells you.

<!-- AUTHOR-REVIEW: B1.4 was repointed off reference-specification drift (P9 tests that better, and §3 teaches it in prose) onto IngressClass and the default-class mechanism, per the question-quality audit — IngressClass otherwise reaches only one question in the chapter. The item assumes §3 states the consequence of a second default: an Ingress omitting `ingressClassName` can no longer be created. That fact is in k8s-docs-ingress-depth-2026-08-24 and verified by the fact-accuracy audit, but if §3's prose stops at the annotation and the single-default assignment, add the one clause there rather than softening the question. -->

**5. `[retrieval: ch3]` An object without its component does nothing.** The two Chapter 9 instances: a `type: LoadBalancer` Service on a cluster with no load balancer to provision one, and a Service whose selector matches no Pods.

The wrong answer to watch for is stopping at one. `type: LoadBalancer` is the instance people keep, because the absent piece has a name and a price attached to it. The Service whose selector matches nothing is the one they drop — nothing there is *un-installed*, and the object is complete and correct on its own terms. Same shape all the same: a record the cluster will serve back to you, and nothing behind it. And the Ingress controller from §3 is not one of the two. It is the third, and the one you found yourself.

If you can list the instances now, §8 will land as a count you already made rather than as an assertion the book handed you. That is the difference between remembering a rule and holding one.

---

**Checkpoint: You've Now Mastered**

✓ Where the Service-type ladder runs out, and the layer boundary that explains why
✓ What Ingress does, what it refuses to do, and the two shapes it takes
✓ Why a perfectly correct object can accomplish nothing
✓ Which controller an Ingress belongs to, and what happens when nothing says
✓ The rule, with three of your own instances behind it

Two sections on the API you just learned, and then we go somewhere completely different.

---
## ☆ Taking Your Bearings #2

Five questions on §4 and §5 — one API frozen, one API recommended, and the difference that word makes.

**1.** ⚪ State both halves of what the Kubernetes project has said about the Ingress API.

**2.** ⚪ True or false, with justification: *Ingress is deprecated and will be removed in a future release.*

**3.** 🟡 Name the three role-mapped Gateway API resources and say which organisational role each belongs to.

**4.** 🟡 How many GatewayClasses is a Gateway associated with, and how many Routes can attach to one Gateway?

**5.** 🟡 A request arrives at a Gateway's IP address. Name the header the reverse proxy uses to match a configuration, and name the two optional things the HTTPRoute may do before the request is forwarded.

---

**Answers with Explanations:**

**1. It is frozen: generally available and subject to the stability guarantees for GA APIs, with no plans for removal — *and* no longer being developed, with no further changes or updates** [source: k8s-docs-ingress-depth-2026-08-24].

An answer carrying only one half is wrong, because one half is precisely the error being tested.

And it is worth saying *why* both halves matter rather than just repeating them. The stability half means there is **no migration emergency**: what you are running keeps working, keeps being supported, and is not scheduled for removal. The no-development half means there is **no future capability**: whatever gap you find in Ingress today is permanent. Those two facts drive different decisions, one about existing systems, one about new ones, and that is exactly why the project stated both.

**2. False, on both counts.** Ingress has not been deprecated, and there are no plans to remove it [source: k8s-docs-ingress-depth-2026-08-24]. What has been said is that it will not be developed further, and that the Kubernetes project recommends using Gateway instead of Ingress [source: k8s-docs-ingress-depth-2026-08-24]. Take that recommendation in the project's own words rather than a softened paraphrase of them — §4 gave the operational reading of what a recommendation does and does not oblige you to do, and the reading is the book's, not the documentation's.

The wrong answer to watch for is the one that reasons from feel: "no longer developed" *feels* like deprecation, so a reader who has absorbed the second half of question 1 answers this one wrong. In Kubernetes, deprecation is a formally defined process with published rules about removal timelines [source: k8s-docs-deprecation-policy-2026-08-24], and the project did not invoke it here.

**3. GatewayClass — infrastructure provider. Gateway — cluster operator. HTTPRoute — application developer** [source: k8s-docs-gateway-api-depth-2026-08-24].

Asked as a mapping rather than a list because the mapping *is* the design. If you can produce the three names but not the three roles, you have memorised the consequence and missed the cause.

One point of precision the answer key must make: **"cluster operator" is a role — a team or a person who runs the cluster — not the operator pattern from Chapter 6.** The word does double duty in Kubernetes vocabulary, and this is the one place in this book where both senses are in play.

**4. Exactly one GatewayClass. Many Routes** [source: k8s-docs-gateway-api-depth-2026-08-24].

Pure recall, and exactly the kind of cardinality detail multiple-choice exams reach for, because it is unambiguous and either known or not.

The wrong answer to watch for is the Ingress-shaped one. In Ingress, a single object carries the entry point *and* every routing rule, so it is natural to expect a Gateway to carry its routes the same way. It does not. The routes attach to it from outside, and — per question 3 — they belong to a different role than the Gateway does.

**5. The `Host:` header. Then, optionally: header and/or path matching based on the HTTPRoute's match rules, and optional modification of the request based on its filter rules** [source: k8s-docs-gateway-api-depth-2026-08-24].

The wrong answer to watch for is *the path*. §2 spent considerably longer on paths than on hosts, and recency does what recency does: readers reach for path matching as the first thing a proxy performs. It is not first. The `Host:` header selects the configuration; path and header matching are among the optional steps that happen after that selection has already been made.

This also closes Soundings question 1. You named the `Host` header at the start of this chapter, from ordinary web experience and before reading a word of Kubernetes networking. The specification agrees with you. Notice that: a fair amount of this material is your existing knowledge wearing new vocabulary, and recognising which parts are genuinely new is how you spend study time well.

---

**Checkpoint: You've Now Mastered**

✓ *Frozen* and *deprecated*, precisely, in both halves
✓ Gateway API's role-oriented design, and the resources that fall out of it
✓ The cardinality, and the request flow end to end

That closes the API arc. What follows shares a chapter with it and shares nothing else: different layer, different direction, different problem. Everything from §1 to §5 has been about getting a request through the harbour wall; §6 is about what is permitted to move once it is already inside. Take the break here if you are taking one.

---
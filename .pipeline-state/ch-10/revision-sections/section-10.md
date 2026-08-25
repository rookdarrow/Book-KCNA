## ⚪ §4 — Frozen, Not Deprecated

Chapter 9 told you this section was coming and told you it was worth exam-level attention. Everything here is definition, and precision is the only thing it has to deliver.

### The statement

The Kubernetes documentation carries a note directly beneath its description of Ingress. Here it is, in full:

> The Kubernetes project recommends using Gateway instead of Ingress. The Ingress API has been frozen.
>
> This means that:
>
> - The Ingress API is generally available, and is subject to the stability guarantees for generally available APIs. The Kubernetes project has no plans to remove Ingress from Kubernetes.
> - The Ingress API is no longer being developed, and will have no further changes or updates made to it.

[source: k8s-docs-ingress-depth-2026-08-24]

Two bullets. Both load-bearing. Nearly everyone drops one.

### The split

| The half readers drop | What it actually says | What it means for you |
|---|---|---|
| **Still GA, still guaranteed, no removal plans** | It is not going away, and it is not going to break under you | Your existing Ingress configurations are not a migration emergency |
| **No further development, no changes or updates** | Nothing new will ever be added | Anything Ingress cannot do today, it will never do |

Collapse the first bullet and you get *"Ingress is deprecated,"* which is wrong, and which will have you planning a migration you do not need. Collapse the second and you get *"Ingress is fine, ignore the note,"* which is also wrong, and which will have you designing new systems around an API that has stopped growing.

> ★ **Fixed Point:** **Frozen ≠ deprecated.** Ingress is generally available, subject to GA stability guarantees, with **no plans for removal** — **and** no longer developed, with **no further changes or updates** [source: k8s-docs-ingress-depth-2026-08-24]. Both halves, or you have the wrong fact.

### Why "deprecated" is a different word

The two words point in different directions, and the difference is about *what* is being announced.

**Deprecation is a statement about future removal.** Kubernetes has a formal, published deprecation policy, and it exists precisely so that removals are predictable: the policy governs the removal of API objects, fields, annotations, enumerated values and component config structures, and its stated purpose is to avoid breaking existing users when a feature must be removed [source: k8s-docs-deprecation-policy-2026-08-24]. Under it, GA API versions **may be marked as deprecated, but must not be removed within a major version of Kubernetes** [source: k8s-docs-deprecation-policy-2026-08-24]. Deprecation is the first step on a defined path toward an eventual exit.

**A freeze is a statement about future development.** It says the thing is finished. Nothing more will be added. It says nothing whatsoever about removal, and a frozen API can be permanent.

Kubernetes has said one of these about Ingress and not the other, and the choice was deliberate. When the Ingress note says the API is "subject to the stability guarantees for generally available APIs," it links directly to that deprecation policy: the guarantees are the same ones any GA API enjoys [source: k8s-docs-ingress-depth-2026-08-24].

> ⚠ **Navigational Hazards:** A question offering *"Ingress is deprecated and will be removed in a future release"* is testing exactly one thing: whether you kept both halves. So is a question offering *"Ingress is unaffected and fully supported for new development."* Neither is the answer. Candidates get this wrong in both directions, which is why an exam can build a clean four-option question out of it. The two most attractive distractors write themselves.

> 🪢 **Mnemonic:** *Frozen things keep. They just don't grow.*

### What "recommends" obliges

*Recommends* is not *requires*.

Here is the recommendation exactly as the documentation states it, with nothing attached to it: **the Kubernetes project recommends using Gateway instead of Ingress** [source: k8s-docs-ingress-depth-2026-08-24]. Not *for new work*. Not *by some deadline*. Not *unless you have a reason*. One unqualified sentence — and what sits beside it is equally unqualified: the project has not deprecated Ingress, has announced no removal, and continues to extend it the stability guarantees that GA APIs carry. A light has been hung on the new channel; the old one has not been closed.

Where that leaves you in practice is a second question, and the answer to it is this book's reading rather than the project's wording: **do not panic about what you are running, and think hard before building something new on an API that will never gain a feature again.** If you have heard the recommendation summarised as *"use Gateway for new work"* — including elsewhere in this chapter — that framing is a practitioner's gloss on the second bullet, not a scope the documentation supplies. The documentation says *instead of*, and stops there.

Keep the two apart. On an exam, you are being asked what the project said, not what a sensible engineer does about it.

That is the whole of it. The project said what it said, precisely, and the reasoning behind the decision is not this book's to supply.

*[cross-bearing: see Ch 8 §6 — semantic versioning and API stability, which is the vocabulary this section spends]*

The obvious next question is what "use Gateway instead" actually means. §5.

---
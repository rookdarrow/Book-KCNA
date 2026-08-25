## Why This Chapter Matters

Chapter 9 ended by naming a ceiling. One external address per Service is reasonable when you have one Service. It is absurd when you have fifty. And no Service type in that chapter can tell `shop.example.com/checkout` from `shop.example.com/catalog`, because at the layer those mechanisms operate on, the difference between those two requests is bytes in a payload that nothing is opening.

This chapter is what sits above that ceiling *[cross-bearing: see Ch 9 §3 — the Service-type ladder and its limits]*.

But the more valuable thing here is not the objects. It is a question.

Every chapter so far has rewarded the same professional instinct: get the object right, and the cluster does the rest. Write a correct Deployment and Pods appear. Write a correct Service and a stable name appears. That instinct has been reliable for nine chapters, and this is the chapter where it stops being enough. This is where you learn the question that separates people who have run Kubernetes from people who have read about it.

The question is not *did I write the object correctly.* It is **is anything watching this object.**

Orders written out in a fair hand, with every heading correct, change nothing at all if nobody has been detailed to read them.

A well-formed Ingress on a cluster with no Ingress controller is a correct object that does nothing. A well-formed NetworkPolicy on a network plugin that does not implement NetworkPolicy is a correct object that does nothing. Unlike the Ingress, it does nothing *quietly*. Unreachability is loud: a pager goes off, a customer complains, somebody is looking at it within minutes. Unrestricted reachability is silent; everything works exactly as it did, which is indistinguishable from a policy working perfectly against traffic nobody happens to be sending. That asymmetry is the most valuable thing in this chapter, and you should have it in hand before you meet either object.

Chapter 9 told you that Chapter 10 would give a name to a shape you had already met twice. Here is the part Chapter 9 did not say: you will meet it **twice more in this chapter alone**, in two objects that have nothing to do with each other. This is where it stops being a curiosity and becomes a rule you can apply to things this book never mentions.

The stakes, stated flat. This is the smallest allocation in Part III, and the material still deserves full attention for two specific reasons. First, `frozen` versus `deprecated` is the most precise word-level distinction in the curriculum, and precise distinctions are what multiple-choice exams are built out of. Second, NetworkPolicy carries more cataloged traps than any other single topic in this book, and every one of them is a case where your existing firewall intuition hands you the wrong answer with complete confidence.

Two reasons. The chapter does not need a third.

---
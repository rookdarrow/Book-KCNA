## The Voyage Ahead

You now hold all four pluggable interfaces, and with them a rule you can state without help: an object without its component does nothing. You have watched that rule fire at the Ingress controller, at the network plugin, at the provisioner, and at the CSI driver — four sightings, one light. Chapter 17 will collect all four interfaces in one place and ask you what they have in common; you already know.

But this chapter also left something exposed, and the next one is about it.

Twice in these pages, storage handed a workload something it should probably not have had. `hostPath` mounts the node's filesystem into a Pod, and the documentation's warning was not about disk space. It was about *privileged system credentials* and *container escape*. Secrets mount as files backed by tmpfs, never written to non-volatile storage, which is a security property so specific it can only exist because someone was worried about the alternative.

Both of those are the same question wearing different clothes: **what is a workload allowed to do, and who decided?** You have spent this chapter learning that storage decisions were made elsewhere, by someone else, before you arrived — reading the manifest, not holding the keys. Chapter 12 asks the harder version. Not *what happens to your data* but *who is allowed to touch it*, and it turns out that Kubernetes' answer has a shape you have already met twice in this chapter without noticing.

Here is the tell. Carry it with you: the permission system you are about to learn has no way to say *no*. None. There is no deny rule, anywhere in it. You have already seen one other Kubernetes system with exactly that property *[cross-bearing: see Ch 10 §6 — allowing, never denying]*, and by the end of the next chapter you will understand why two systems built for entirely different purposes arrived at the same design, and why that design is a feature rather than an omission.

Bring the `secret` volume with you. Chapter 12 §4 has an argument to make about file mounts versus environment variables, and you already hold half of it.

---

🏆 **Safe Harbor** — Domain 2's storage competency is complete. You can trace a file from the container filesystem out to a cluster-scoped volume and name what stops it at each boundary; you can distinguish a PersistentVolume from a claim from a class and say which one a Pod actually references; you can predict whether a claim binds, waits, or provisions; you can read an access mode as a node count; and you can say where the decision about your data's survival was actually made. Chapter 6's five deferred verbs are all settled, and the book's one deliberate forward reference is closed.

> *"The hold is inventoried by people who never sail. That is not a failure of the arrangement. That is the arrangement."*
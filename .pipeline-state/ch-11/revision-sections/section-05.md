## What You'll Learn

By the end of this chapter, you'll be able to:

- **Trace** a file from the container filesystem outward, and say at which of three boundaries it stops surviving.
- **Distinguish** a PersistentVolume from a PersistentVolumeClaim from a StorageClass — the three-way distinction this book's domain analysis puts at the front of the Storage competency — and say which one a Pod actually references.
- **Predict** whether a claim will bind, sit unbound, or trigger a volume into existence, given a cluster's provisioning setup.
- **Read** an access mode as a statement about how many *nodes*, not how many Pods (a distinction with an entire fourth mode devoted to it, which should tell you something about how often it gets missed).
- **State** what happens to the data after the claim is deleted, and where that decision was actually made.
- **Explain** why a StatefulSet's storage survives not just a Pod restart but a reschedule onto a different node, closing the loop Chapter 6 opened on purpose.

You will also collect the last of the four pluggable interfaces, and with it a rule about interfaces that Chapter 17 will ask you to state without help.

---
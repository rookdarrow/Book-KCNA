## The Voyage Ahead

You have spent two chapters on the network, and you have been treating one thing as a given the entire time: that a Pod which restarts is a Pod that starts over. Chapter 5 said it directly — Pods are cattle, replaced rather than repaired — and Chapters 6 through 10 have quietly depended on it. A Service can point at an interchangeable set of backends precisely because they *are* interchangeable.

Chapter 11 is where that assumption runs out.

Some workloads write things down. A database has a disk, and the contents of that disk are not a detail of the Pod. They are the entire point of running it. Chapter 11 works out what happens to data when the Pod that produced it is deleted, and the answer turns out to be a ladder of three different lifetimes, only one of which survives the thing that created it.

It also closes a loop this book left open on purpose. Chapter 6 introduced StatefulSet and told you it was about stable *identity*, not about writing to disk, and then admitted the explanation was incomplete and would stay that way until storage arrived. Storage arrives in Chapter 11, and the second half of that answer arrives with it: what a per-replica volume claim is, and why it outlives not just the Pod but the rescheduling.

<!-- AUTHOR-REVIEW: The fact-accuracy audit flagged this next paragraph twice — the "four
     pluggable interfaces" claim was untagged, and the draft's count ("you have collected two
     now") contradicted §5's cross-bearing naming CRDs as one of the four. One of the fixes the
     audit offered was to drop CRDs from the set and repoint §5 at API extensions. That fix is
     declined here, because both binding contracts fix the set the other way: the B6 section
     skeleton assigns CRI to Ch 2 §4, CNI to Ch 9 §1, CSI to Ch 11 §5 and CRDs to Ch 6 §8 as the
     four, and the B7 canonical-forms row names "the four pluggable interfaces" as this book's own
     phrase for exactly that set, noting that shipped Ch 2 §4 already points at that wording. §5's
     cross-bearing therefore stands unedited and this section was corrected instead: the count is
     now three-of-four collected, which is what a reader who met CRDs in Ch 6 actually holds. The
     grouping is now owned as the book's rather than the documentation's, and the documentation's
     larger and differently-cut map is tagged. No snapshot in the corpus enumerates a canonical
     set of four; if the exam is calibrated against one, that remains a research gap. Note also
     that this is the chapter's third distinct "four" (§3 and §8 carry the absent-component-
     pattern count) — hence the full phrase rather than a bare number here. -->

And you will meet the last of the four pluggable interfaces. You have three of them already, collected one chapter at a time: CRI at the container runtime in Chapter 2, CRDs at the API itself in Chapter 6, CNI at the network last chapter. Chapter 11 brings CSI, at storage, and that closes the set. By the time Chapter 17 gathers all four in one place, the shape should be familiar enough that the gathering feels like recognition rather than instruction.

One caution about that number, since this chapter has made a point of separating what a source says from what we have concluded from it. *The four pluggable interfaces* is this book's phrase and this book's grouping. The documentation's own map of where Kubernetes can be extended is larger than ours and cut differently: six extension points, five plugin types under infrastructure alone, and custom resources filed under a different heading entirely [source: k8s-docs-extending-kubernetes-2026-08-23]. Chapter 17 sets both maps side by side *[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*. What makes our four a set is a judgement rather than a heading: at each of them, Kubernetes defines an interface and hands the implementation to somebody else. The judgement is ours. The four interfaces are real, and each one is sourced where you met it.

One last thing to carry across the chapter boundary. You will meet several objects in Chapter 11 that describe storage without providing any, and at least one arrangement where a claim sits unbound because the thing that would satisfy it has not been installed.

You know what question to ask about that now.

> *"An object is a record of intent. Intent does not act. Something has to be watching."*
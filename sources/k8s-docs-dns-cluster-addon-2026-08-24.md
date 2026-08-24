---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/"
fetched_at: "2026-08-24T03:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["cluster-dns", "addons", "addon-manager", "coredns"]
---
# Customizing DNS Service - cluster DNS as a built-in addon (kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/)

> **Snapshot note.** Narrow-scope snapshot. Only the introductory sentence bearing on Chapter 3
> Open question #8 (is cluster DNS effectively mandatory?) was transcribed, verified
> character-for-character against the rendered page. The remainder of the page is CoreDNS
> Corefile configuration, which is out of scope for Chapter 3 and Chapter 9.

"DNS is a built-in Kubernetes service launched automatically using the _addon manager_ [cluster add-on](https://github.com/kubernetes/kubernetes/blob/master/cluster/addons/addon-manager/README.md)."

The page's prerequisites additionally assume CoreDNS is already present in the cluster.

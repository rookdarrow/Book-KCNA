---
source_url: "https://github.com/flannel-io/flannel/blob/master/Documentation/kubernetes.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "flannel project (flannel-io/flannel), the project's own Kubernetes deployment documentation"
objectives_covered: ["D2.1", "D2 Networking"]
concepts_covered: ["network-plugin", "cni", "daemonset", "flannel", "per-node-agent"]
---

# Flannel — Kubernetes deployment documentation (flannel-io/flannel, Documentation/kubernetes.md)

> **Snapshot note.** Narrow-scope snapshot fetched 2026-09-04 during the Chapter 9 audit to
> source the retrieved Chapter 6 claim that cluster networking plugins ship as DaemonSets.
> Only the sentence describing the packaging of the `kube-flannel.yaml` manifest was
> transcribed. Cilium's component overview and Calico's architecture overview were checked
> on the same date; both say their node agent "runs on each node" but neither uses the word
> DaemonSet, so Flannel is the one named example the book cites.

## kube-flannel.yaml

"A DaemonSet for every architecture to deploy the `flannel` pod on each Node."

---
source_url: "https://kubernetes.io/docs/concepts/cluster-administration/addons/"
fetched_at: "2026-08-24T03:12:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["addons", "cluster-dns", "coredns", "optional-components", "kube-proxy-replacement", "dashboard"]
---
# Installing Addons (kubernetes.io/docs/concepts/cluster-administration/addons/)

> **Snapshot note.** Transcribed verbatim from the page's canonical Markdown source
> (github.com/kubernetes/website .../content/en/docs/concepts/cluster-administration/addons.md).
> The "Networking and Network Policy" list is long and mostly out of scope for Chapter 3; it has
> been trimmed to the entries that bear on kube-proxy optionality, with the elision marked.
> All retained text is verbatim, including original link syntax and emphasis (none added).

Add-ons extend the functionality of Kubernetes.

This page lists some of the available add-ons and links to their respective installation instructions. The list does not try to be exhaustive.

## Networking and Network Policy

[Entries for ACI, Antrea, Canal, CNI-Genie, Contiv, Contrail, Gateway API, Knitter, kube-router, Multus, OVN-Kubernetes, Nodus, NSX-T, Nuage, Romana, Spiderpool, Terway and Weave Net trimmed as out of scope for Chapter 3 - see the source URL for the full list.]

* [Calico](https://www.tigera.io/project-calico/) is a networking and network policy provider. Calico supports a flexible set of networking options so you can choose the most efficient option for your situation, including non-overlay and overlay networks, with or without BGP. Calico uses the same engine to enforce network policy for hosts, pods, and (if using Istio & Envoy) applications at the service mesh layer.
* [Cilium](https://github.com/cilium/cilium) is a networking, observability, and security solution with an eBPF-based data plane. Cilium provides a simple flat Layer 3 network with the ability to span multiple clusters in either a native routing or overlay/encapsulation mode, and can enforce network policies on L3-L7 using an identity-based security model that is decoupled from network addressing. Cilium can act as a replacement for kube-proxy; it also offers additional, opt-in observability and security features. Cilium is a [CNCF project at the Graduated level](https://www.cncf.io/projects/cilium/).
* [Flannel](https://github.com/flannel-io/flannel#deploying-flannel-manually) is an overlay network provider that can be used with Kubernetes.

## Service Discovery

* [CoreDNS](https://coredns.io) is a flexible, extensible DNS server which can be [installed](https://github.com/coredns/helm) as the in-cluster DNS for pods.

## Visualization & Control

* [Dashboard](https://github.com/kubernetes/dashboard#kubernetes-dashboard) is a dashboard web interface for Kubernetes.
* [Headlamp](https://headlamp.dev/) is an extensible Kubernetes UI that can be deployed in-cluster or used as a desktop application.

## Infrastructure

* [KubeVirt](https://kubevirt.io/user-guide/#/installation/installation) is an add-on to run virtual machines on Kubernetes. Usually run on bare-metal clusters.
* The [node problem detector](https://github.com/kubernetes/node-problem-detector) runs on Linux nodes and reports system issues as either [Events](/docs/reference/kubernetes-api/cluster-resources/event-v1/) or [Node conditions](/docs/concepts/architecture/nodes/#condition).

## Instrumentation

* [kube-state-metrics](/docs/concepts/cluster-administration/kube-state-metrics)

## Legacy Add-ons

There are several other add-ons documented in the deprecated [cluster/addons](https://git.k8s.io/kubernetes/cluster/addons) directory.

Well-maintained ones should be linked to here. PRs welcome!

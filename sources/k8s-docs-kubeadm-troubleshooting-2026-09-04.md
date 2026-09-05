---
source_url: "https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), 'Troubleshooting kubeadm' — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2.1", "D2.3"]
concepts_covered: ["cni-plugin-required", "pod-network-add-on", "coredns-pending-without-network", "kubeadm-bootstrap-symptoms"]
closes_gap: "Ch 20 item 2 walkthrough — the observable symptom of a bootstrapped cluster with no CNI plugin installed was asserted without a snapshot. Ch 9 §1 states that a CNI plugin is required to implement the network model but does not describe the symptom."
---

# Troubleshooting kubeadm — the no-network symptom

Fetched 2026-09-04 for the Chapter 20 mock exam. Two sections quoted; headings
verbatim, body sentences verbatim.

## Section: "`coredns` is stuck in the `Pending` state"

"This is **expected** and part of the design. kubeadm is network provider-agnostic, so the admin should install the pod network add-on of choice. You have to install a Pod Network before CoreDNS may be deployed fully. Hence the `Pending` state before the network is set up."

## Section: "Pods in `RunContainerError`, `CrashLoopBackOff` or `Error` state"

"Right after `kubeadm init` there should not be any pods in these states."

"`coredns` (or `kube-dns`) should be in the `Pending` state until you have deployed the network add-on."

"If you see Pods in the `RunContainerError`, `CrashLoopBackOff` or `Error` state after deploying the network add-on and nothing happens to `coredns` (or `kube-dns`), it's very likely that the Pod Network add-on that you installed is somehow broken."

## What this establishes, and what it does not

- ESTABLISHED: a cluster bootstrapped without a pod network add-on (a CNI plugin) has Pods that need the pod network sitting in `Pending`, by design, until the add-on is installed. CoreDNS is the documented example.
- ESTABLISHED: the control plane itself comes up without the network add-on — the page treats `kubeadm init` as complete and the cluster as inspectable before the add-on exists.
- NOT ON THIS PAGE: any statement about node `NotReady` status or the kubelet's "network plugin is not ready" condition. Do not cite this snapshot for those.
- NOT ON THIS PAGE: any statement about the API server refusing to start, or about ClusterIP allocation. Distractors turning on those are the book's own entailments, not documented behaviour.

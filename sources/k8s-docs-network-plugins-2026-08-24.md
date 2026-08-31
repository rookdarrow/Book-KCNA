---
source_url: "https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/"
source_url_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins.md"
fetched_at: "2026-08-24T14:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.1", "D2 Networking"]
concepts_covered: ["cni", "container-network-interface", "network-plugin", "network-model", "cri", "container-runtime", "loopback-cni"]
---
# Network Plugins (kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

> **Snapshot note.** Fetched to close arc-outline blocking gap **G11** for Chapter 9 §1.
> Transcribed from the rendered page and cross-checked against the canonical Markdown source
> in github.com/kubernetes/website. Hugo shortcodes (`{{< note >}}`, `{{< /note >}}`) are
> retained inline as delimiters so the note's boundaries stay visible; they are not prose.
> Per the outline's scope guard, CNI plugin *configuration* (`--cni-conf-dir`, plugin
> authoring, per-runtime setup detail) is deliberately NOT transcribed beyond the two
> runtime documentation links the page itself supplies.
>
> **⚠ Read "Notes for the author" in the Ch 9 research manifest before drafting from this
> file.** The page does **not** contain the sentence "Kubernetes ships no network plugin by
> default", and it revises the kubelet-executes-the-binary framing carried by
> `k8s-docs-extending-kubernetes-2026-08-23.md`.

## Opening

Kubernetes (version 1.3 through to the latest 1.36, and likely onwards) lets you use Container Network Interface (CNI) plugins for cluster networking. You must use a CNI plugin that is compatible with your cluster and that suits your needs.

A CNI plugin is required to implement the Kubernetes network model.

You must use a CNI plugin that is compatible with the v0.4.0 or later releases of the CNI specification.

## Installation

A Container Runtime, in the networking context, is a daemon on a node configured to provide CRI
Services for kubelet. In particular, the Container Runtime must be configured to load the CNI
plugins required to implement the Kubernetes network model.

{{< note >}}
Prior to Kubernetes 1.24, the CNI plugins could also be managed by the kubelet using the
`cni-bin-dir` and `network-plugin` command-line parameters.
These command-line parameters were removed in Kubernetes 1.24, with management of the CNI no
longer in scope for kubelet.

See [Troubleshooting CNI plugin-related errors](/docs/tasks/administer-cluster/migrating-from-dockershim/troubleshooting-cni-plugin-related-errors/)
if you are facing issues following the removal of dockershim.
{{< /note >}}

For specific information about how a Container Runtime manages the CNI plugins, see the
documentation for that Container Runtime, for example:

- [containerd](https://github.com/containerd/containerd/blob/main/script/setup/install-cni)
- [CRI-O](https://github.com/cri-o/cri-o/blob/main/contrib/cni/README.md)

For specific information about how to install and manage a CNI plugin, see the documentation for
that plugin or [networking provider](/docs/concepts/cluster-administration/networking/#how-to-implement-the-kubernetes-network-model).

## Network Plugin Requirements

### Loopback CNI

In addition to the CNI plugin installed on the nodes for implementing the Kubernetes network
model, Kubernetes also requires the container runtimes to provide a loopback interface `lo`, which
is used for each sandbox (pod sandboxes, vm sandboxes, ...).
Implementing the loopback interface can be accomplished by re-using the
[CNI loopback plugin.](https://github.com/containernetworking/plugins/blob/master/plugins/main/loopback/loopback.go)
or by developing your own code to achieve this (see
[this example from CRI-O](https://github.com/cri-o/ocicni/blob/release-1.24/pkg/ocicni/util_linux.go#L91)).

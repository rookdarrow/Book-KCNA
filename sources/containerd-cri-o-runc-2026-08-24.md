---
source_url: "https://cri-o.io/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "CRI-O project (CNCF), containerd project (CNCF graduated), runC (Open Container Initiative) — three primary project sources, see per-section URLs"
objectives_covered: ["D1.4"]
concepts_covered: ["containerd", "cri-o", "runc", "cri", "oci", "kubelet-runtime-boundary"]
---
# containerd, CRI-O, and runC — primary project sources

> Three URLs in one snapshot because they document one chain. Each section carries its
> own source_url. Serves Chapter 2 §4 (ch02-fig04, Fixed Point #2) and §5's hazard.

## CRI-O — source_url: https://cri-o.io/

> THE OCI/CRI BOUNDARY SENTENCE. Anchor §5's ⚠ Navigational Hazards on this rather
> than asserting the boundary in the book's own voice. Both acronyms, correct planes,
> one sentence, from the project itself.

"CRI-O is an implementation of the Kubernetes CRI (Container Runtime Interface) to
enable using OCI (Open Container Initiative) compatible runtimes."

"It is a lightweight alternative to using Docker as the runtime for kubernetes."

"It allows Kubernetes to use any OCI-compliant runtime as the container runtime for
running pods."

"Today it supports runc and Kata Containers as the container runtimes but any
OCI-conformant runtime can be plugged in principle."

"CRI-O supports OCI container images and can pull from any container registry."

The Kata sentence is a sourced §5 → §7 bridge: Kata appears as an OCI runtime slotting
under CRI, so §7 is visibly the SAME socket from §4, not a new mechanism.

## containerd — source_url: https://raw.githubusercontent.com/containerd/containerd/main/README.md

"containerd is an industry-standard container runtime with an emphasis on simplicity,
robustness, and portability."

"It is available as a daemon for Linux and Windows, which can manage the complete
container lifecycle of its host system: image transfer and storage, container execution
and supervision, low-level storage and network attachments, etc."

"containerd is a member of CNCF with 'graduated' status."

> THE containerd → runC HOP, previously unsourced:

"Most interactions with the Linux and Windows container feature sets are handled via
runc and/or OS-specific libraries (e.g. hcsshim for Microsoft)."

Before this, ch02-fig04's containerd → runC arrow rested only on oci-overview's
"cornerstone" sentence — which establishes provenance of the donation, not use.
Fixed Point #2's chain is now sourced end to end.

## runC — source_url: https://raw.githubusercontent.com/opencontainers/runc/main/README.md

runc is "a CLI tool for spawning and running containers on Linux according to the OCI
specification".

[Only this fragment returned as a quotation. The extractor found no further verbatim
statement about runC's relationship to the runtime spec or libcontainer. Do not
attribute more to this URL without re-fetching.]

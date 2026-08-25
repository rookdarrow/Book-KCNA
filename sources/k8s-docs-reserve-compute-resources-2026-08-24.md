---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/administer-cluster/reserve-compute-resources.md"
fetched_at: "2026-08-24T18:59:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["node-capacity", "node-allocatable", "kube-reserved", "system-reserved", "eviction-threshold"]
closes_gap: "ch-08 outline Open Question #6, at the recommended option (b) level. Chapter 7 line 408 promised 'what makes Capacity and Allocatable differ, and how it is configured'. The reservations are now nameable with verbatim definitions."
supersedes_note: "COMPLEMENTS k8s-docs-node-allocatable-2026-08-24.md, which is a deliberately shallow extraction of the SAME page for Chapter 7. Two snapshots share this source_url by design: the earlier file carries what Chapter 7 needed, this one carries the reservation model Chapter 7 deferred to Chapter 8."
---
# Reserve Compute Resources for System Daemons

> **Extraction note.** All passages below are **[VERBATIM]**.

## Why Capacity is not the number that matters

> "Kubernetes nodes can be scheduled to `Capacity`. Pods can consume all the available capacity on a node by default. This is an issue because nodes typically run quite a few system daemons that power the OS and Kubernetes itself."

## Node Allocatable

> "'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods."

## Kube Reserved

> "`kubeReserved` is meant to capture resource reservation for kubernetes system daemons like the `kubelet`, `container runtime`, etc. It is not meant to reserve resources for system daemons that are run as pods."

## System Reserved

> "`systemReserved` is meant to capture resource reservation for OS system daemons like `sshd`, `udev`, etc."

The section additionally states that `systemReserved` should "reserve `memory` for the
`kernel`", and that "reserving resources for user login sessions is also recommended."

## Eviction Thresholds

> "By reserving some memory via `evictionHard` setting, the `kubelet` attempts to evict pods whenever memory availability on the node drops below the reserved value."

---

## The arithmetic is still not extractable -- re-confirmed 2026-08-24

There is **no textual statement or equation** on this page relating Capacity,
`kube-reserved`, `system-reserved`, `eviction-threshold` and Allocatable. The relationship
is published only as an image (`node-capacity.svg`) with no text equivalent. This
re-confirms the extraction note in `k8s-docs-node-allocatable-2026-08-24.md`.

**Chapter 8 sec.4 must not state an arithmetic relationship.** What it may now say, and
what discharges the Chapter 7 promise at option (b): nodes run OS system daemons and
Kubernetes system daemons; `kube-reserved` and `system-reserved` are the reservations that
account for them; Allocatable is what is left for Pods. That is the "what makes the two
differ" half of the promise, honestly paid, with the "how it is configured" half left at
the two flag names -- which is where the associate tier stops.

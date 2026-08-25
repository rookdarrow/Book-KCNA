---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/administer-cluster/safely-drain-node.md"
fetched_at: "2026-08-24T18:58:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["drain", "cordon", "uncordon", "api-initiated-eviction", "node-maintenance"]
scope_note: "The outline caps sec.4's drain treatment at one clause ('it evicts') and BANS teaching PodDisruptionBudgets and --ignore-daemonsets. Those sentences are transcribed here as evidence for the fact-accuracy audit, NOT as a licence to teach them. See the drafting note at the foot of this file."
---
# Safely Drain a Node

> **Extraction note.** All passages below are **[VERBATIM]**.

## What drain does

> "You can use `kubectl drain` to safely evict all of your pods from a node before you perform maintenance on the node (e.g. kernel upgrade, hardware maintenance, etc.). Safe evictions allow the pod's containers to gracefully terminate and will respect the PodDisruptionBudgets you have specified."

## DaemonSet-managed Pods

> "If there are pods managed by a DaemonSet, you will need to specify `--ignore-daemonsets` with `kubectl` to successfully drain the node."

## After the drain returns

> "Once it returns (without giving an error), you can power down the node (or equivalently, if on a cloud platform, delete the virtual machine backing the node)."

> "you need to run `kubectl uncordon <node name>` afterwards to tell Kubernetes that it can resume scheduling new pods onto the node."

## Not on this page

No sentence on this page states that `kubectl drain` cordons the node as part of its
operation. The page discusses marking nodes unschedulable and later uses
`kubectl uncordon`, but the cordon-as-part-of-drain step is not asserted in prose.
**Chapter 8 must not claim it from this source.**

---

## Drafting note -- a tension the author should know about

The Nodes concept page states that "Pods that are part of a DaemonSet tolerate being run on
an unschedulable Node." This page states that draining a node with DaemonSet-managed Pods
requires `--ignore-daemonsets`. Both are true and they are about different things --
tolerating an unschedulable node is a *scheduling* fact, needing the flag is a *drain*
fact -- but a sharp reader who holds both may feel a contradiction. The outline bans
teaching `--ignore-daemonsets`. If the author wants the tension defused, one clause in
sec.4 is the ceiling; otherwise leave it, since sec.4 only asserts the scheduling fact.

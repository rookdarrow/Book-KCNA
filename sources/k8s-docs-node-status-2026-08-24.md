---
source_url: "https://kubernetes.io/docs/reference/node/node-status/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/node/node-status.md"
fetched_at: "2026-08-24T19:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["node-conditions", "ready-condition", "memorypressure", "diskpressure", "pidpressure", "networkunavailable", "node-monitor-grace-period", "node-capacity", "node-allocatable", "cordon", "unschedulable-node"]
supersedes_note: "CITATION CORRECTION. k8s-docs-nodes-2026-08-23.md carries the node conditions table and the three-valued Ready description under source_url .../concepts/architecture/nodes/. As of 2026-08-24 the concept page no longer carries that table -- it links out to this reference page. Chapter 8 sec.4 should cite THIS file for conditions, Capacity/Allocatable and Info. The 08-23 file remains correct for node registration, cordon/drain/uncordon, heartbeats and the node controller."
closes_gap: "ch-08 outline Open Question #5 (node-monitor-grace-period has a documented default) and the previously unsourced sec.8 claim that cordon writes a SPEC field."
---
# Node Status (reference)

> **Extraction note.** All passages below are **[VERBATIM]**.

## What a Node's status contains

> "A Node's status contains the following information: * Addresses * Conditions * Capacity and Allocatable * Info * Declared Features"

## Addresses

> "The usage of these fields varies depending on your cloud provider or bare metal configuration. * HostName: The hostname as reported by the node's kernel. Can be overridden via the kubelet `--hostname-override` parameter. * ExternalIP: Typically the IP address of the node that is externally routable (available from outside the cluster). * InternalIP: Typically the IP address of the node that is routable only within the cluster."

## Conditions

> "The `conditions` field describes the status of all `Running` nodes. Examples of conditions include:"

| Node Condition | Description (verbatim) |
|---|---|
| `Ready` | "`True` if the node is healthy and ready to accept pods, `False` if the node is not healthy and is not accepting pods, and `Unknown` if the node controller has not heard from the node in the last `node-monitor-grace-period` (default is 50 seconds)" |
| `DiskPressure` | "`True` if pressure exists on the disk size---that is, if the disk capacity is low; otherwise `False`" |
| `MemoryPressure` | "`True` if pressure exists on the node memory---that is, if the node memory is low; otherwise `False`" |
| `PIDPressure` | "`True` if pressure exists on the processes---that is, if there are too many processes on the node; otherwise `False`" |
| `NetworkUnavailable` | "`True` if the network for the node is not correctly configured, otherwise `False`" |

> "In the Kubernetes API, a node's condition is represented as part of the `.status` of the Node resource."

## The cordon note -- load-bearing for sec.8

> "If you use command-line tools to print details of a cordoned Node, the Condition includes `SchedulingDisabled`. `SchedulingDisabled` is not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec."

## Capacity and Allocatable

> "Describes the resources available on the node: CPU, memory, and the maximum number of pods that can be scheduled onto the node. The fields in the capacity block indicate the total amount of resources that a Node has. The allocatable block indicates the amount of resources on a Node that is available to be consumed by normal Pods."

## Info

> "Describes general information about the node, such as kernel version, Kubernetes version (kubelet and kube-proxy version), container runtime details, and which operating system the node uses."

---

## Notes for drafting

1. **`node-monitor-grace-period` now has a documented default: 50 seconds.** The ch-08
   outline instructed sec.4 to name the parameter and state no number, because no cached
   source carried one, and added: "If a later fetch supplies a default, it may be added as
   an illustration, never as a rule." This is that fetch. Recommended handling: name the
   parameter, then give "(default 50 seconds)" as a dated illustration, never as the
   examinable fact.
2. **`SchedulingDisabled` is not an API Condition.** It is a client-side display artifact.
   This is a ready-made Snag for sec.4 and it directly supports sec.8: what `cordon`
   actually changes is `.spec`, which is the reader's own declaration, not `.status`, which
   the system writes. That is the Practice-Questions retrieval item ("spec field or status
   field, and how do you know?") sourced rather than inferred.
3. "Declared Features" is a fifth status field on the current page. NOT extracted -- it is
   above associate tier and appears in no CNCF competency list.

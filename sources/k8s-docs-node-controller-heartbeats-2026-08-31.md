---
source_url: "https://kubernetes.io/docs/concepts/architecture/nodes/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/architecture/nodes.md"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 -- fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3"]
concepts_covered: ["node-lease-heartbeat", "node-death-handling", "kubelet-health", "node-conditions-as-diagnostic"]
closes_gap: "ch-13 outline Open Question 4, item 3 -- the node-death eviction timeout, which the outline barred from being written from memory. It is taint-based, and the node controller's wait is documented here."
companion: "Node conditions table and the node-monitor-grace-period default (50 seconds) are already sourced in k8s-docs-node-status-2026-08-24.md. Cite that file for the conditions themselves -- sec.5's guardrail forbids restating the table anyway."
---
# Node heartbeats and the node controller

> All passages below are **[VERBATIM]** from the kubernetes/website source markdown.

## Node heartbeats

> "Heartbeats sent by Kubernetes nodes help your cluster determine the availability of each node, and to take action when failures are detected."

> "For nodes there are two forms of heartbeats:
> - Updates to the `.status` of a Node.
> - Lease objects within the `kube-node-lease` namespace. Each Node has an associated Lease object."

## Node controller

> "The node controller is a Kubernetes control plane component that manages various aspects of nodes."

> "The node controller has multiple roles in a node's life. The first is assigning a CIDR block to the node when it is registered (if CIDR assignment is turned on)."

> "The second is keeping the node controller's internal list of nodes up to date with the cloud provider's list of available machines. When running in a cloud environment and whenever a node is unhealthy, the node controller asks the cloud provider if the VM for that node is still available. If not, the node controller deletes the node from its list of nodes."

> "The third is monitoring the nodes' health. The node controller is responsible for:
> - In the case that a node becomes unreachable, updating the `Ready` condition in the Node's `.status` field. In this case the node controller sets the `Ready` condition to `Unknown`.
> - If a node remains unreachable: triggering API-initiated eviction for all of the Pods on the unreachable node. **By default, the node controller waits 5 minutes between marking the node as `Unknown` and submitting the first eviction request.**"

> "By default, the node controller checks the state of each node every 5 seconds. This period can be configured using the `--node-monitor-period` flag on the `kube-controller-manager` component."

### Rate limits on eviction

> "In most cases, the node controller limits the eviction rate to `--node-eviction-rate` (default 0.1) per second, meaning it won't evict pods from more than 1 node per 10 seconds."

> "The node eviction behavior changes when a node in a given availability zone becomes unhealthy. The node controller checks what percentage of nodes in the zone are unhealthy (the `Ready` condition is `Unknown` or `False`) at the same time:
> - If the fraction of unhealthy nodes is at least `--unhealthy-zone-threshold` (default 0.55), then the eviction rate is reduced.
> - If the cluster is small (i.e. has less than or equal to `--large-cluster-size-threshold` nodes - default 50), then evictions are stopped.
> - Otherwise, the eviction rate is reduced to `--secondary-node-eviction-rate` (default 0.01) per second."

> "The corner case is when all zones are completely unhealthy (none of the nodes in the cluster are healthy). In such a case, the node controller assumes that there is some problem with connectivity between the control plane and the nodes, and doesn't perform any evictions."

### Taints for node problems

> "The node controller is also responsible for evicting pods running on nodes with `NoExecute` taints, unless those pods tolerate that taint. The node controller also adds taints corresponding to node problems like node unreachable or not ready. This means that the scheduler won't place Pods onto unhealthy nodes."

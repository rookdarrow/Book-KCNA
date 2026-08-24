---
source_url: "https://kubernetes.io/docs/concepts/architecture/nodes/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Administration", "D2 Troubleshooting"]
concepts_covered: ["node", "node-registration", "node-conditions", "ready", "diskpressure", "memorypressure", "pidpressure", "heartbeats", "lease", "node-controller", "cordon", "drain"]
---
# Nodes (kubernetes.io/docs/concepts/architecture/nodes/)

Kubernetes runs your workload by placing containers into Pods to run on Nodes. A node may be a virtual or physical machine, depending on the cluster. Each node is managed by the control plane and contains the services necessary to run Pods: the kubelet, a container runtime, and kube-proxy.

## Management
There are two main ways to have Nodes added to the API server: the kubelet on a node self-registers to the control plane (the default, --register-node=true), or you (or another human user) manually add a Node object. After you create a Node object, the control plane checks whether the new Node object is valid — a kubelet has registered with the API server that matches the metadata.name field of the Node; if the node is healthy (the necessary services are running), then it is eligible to run a Pod. The name of a Node object must be a valid DNS subdomain name and must be unique. **Manual Node administration:** marking a node as unschedulable (`kubectl cordon $NODENAME`) prevents the scheduler from placing new pods onto that Node but does not affect existing Pods on the Node; this is useful as a preparatory step before a node reboot or other maintenance (`kubectl drain` evicts the Pods; `kubectl uncordon` restores scheduling). Pods that are part of a DaemonSet tolerate being run on an unschedulable Node.

## Node status
A Node's status contains: Addresses (HostName, ExternalIP, InternalIP); Conditions; Capacity and Allocatable; Info (kernel version, container runtime, kubelet version). Conditions describe the status of all Running nodes: Ready — True if the node is healthy and ready to accept pods, False if the node is not healthy and is not accepting pods, and Unknown if the node controller has not heard from the node in the last node-monitor-grace-period; DiskPressure — True if pressure exists on the disk size; MemoryPressure — True if pressure exists on the node memory; PIDPressure — True if pressure exists on the processes; NetworkUnavailable — True if the network for the node is not correctly configured. `kubectl describe node <name>` shows them.

## Heartbeats
Heartbeats, sent by Kubernetes nodes, help your cluster determine the availability of each node, and to take action when failures are detected. For nodes there are two forms of heartbeats: updates to the .status of a Node, and Lease objects within the kube-node-lease namespace (each Node has an associated Lease object).

## Node controller
The node controller is a Kubernetes control plane component that manages various aspects of nodes: assigning a CIDR block to the node when it is registered; keeping the node controller's internal list of nodes up to date with the cloud provider's list of available machines; monitoring the nodes' health — updating the Ready condition to Unknown when a node becomes unreachable, and triggering API-initiated eviction of all the Pods from the node if it stays unreachable.

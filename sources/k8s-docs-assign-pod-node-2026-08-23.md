---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Scheduling"]
concepts_covered: ["node-labels", "nodeselector", "node-affinity", "pod-affinity", "pod-anti-affinity", "nodename", "required-vs-preferred"]
---
# Assigning Pods to Nodes (kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

You can constrain a Pod so that it is restricted to run on particular node(s), or to prefer to run on particular nodes. There are several ways to do this and the recommended approaches all use label selectors to facilitate the selection. Often, you do not need to set any such constraints; the scheduler will automatically do a reasonable placement (for example, spreading your Pods across nodes so as not to place Pods on a node with insufficient free resources). However, there are some circumstances where you may want to control which node the Pod deploys to, for example, to ensure that a Pod ends up on a node with an SSD attached to it, or to co-locate Pods from two different services that communicate a lot into the same availability zone.

## Node labels
Like many other Kubernetes objects, nodes have labels. You can attach labels manually. Kubernetes also populates a standard set of labels on all nodes in a cluster. Adding labels to nodes allows you to target Pods for scheduling on specific nodes or groups of nodes; if you use labels for node isolation, choose label keys that the kubelet cannot modify (the NodeRestriction admission plugin prevents the kubelet from setting labels with a node-restriction.kubernetes.io/ prefix).

## nodeSelector
nodeSelector is the simplest recommended form of node selection constraint. You can add the nodeSelector field to your Pod specification and specify the node labels you want the target node to have. Kubernetes only schedules the Pod onto nodes that have each of the labels you specify.

## Affinity and anti-affinity
Affinity and anti-affinity expand the types of constraints you can define: the language is more expressive; you can indicate that a rule is soft or preferred, so that the scheduler still schedules the Pod even if it can't find a matching node; you can constrain a Pod using labels on other Pods running on the node (or other topological domain). Node affinity functions like the nodeSelector field but is more expressive and allows you to specify soft rules; it has two types: requiredDuringSchedulingIgnoredDuringExecution — the scheduler can't schedule the Pod unless the rule is met; and preferredDuringSchedulingIgnoredDuringExecution — the scheduler tries to find a node that meets the rule, but if a matching node is not available, still schedules the Pod. IgnoredDuringExecution means that if the node labels change after Kubernetes schedules the Pod, the Pod continues to run. Operators: In, NotIn, Exists, DoesNotExist, Gt and Lt. Inter-pod affinity and anti-affinity allow you to constrain Pods against labels on other Pods ("only schedule on nodes in the same zone as a Pod with this label", or "spread these Pods across nodes").

## nodeName
nodeName is a more direct form of node selection than affinity or nodeSelector. nodeName is a field in the Pod spec. If the nodeName field is not empty, the scheduler ignores the Pod and the kubelet on the named node tries to place the Pod on that node. Using nodeName overrules using nodeSelector or affinity and anti-affinity rules; if the named node does not exist or does not have the resources, the Pod fails.

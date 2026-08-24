---
source_url: "https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/configure-pod-container/assign-pods-nodes.md"
fetched_at: "2026-08-24T09:51:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.3"]
concepts_covered: ["kubectl-get-nodes", "kubectl-label", "kubectl-get-pods", "node-labels", "nodeselector"]
closes_gap: "ch-07 outline Open Question #10 — the kubectl-get-nodes, kubectl-label and kubectl-get-pods command forms in kb_tags.commands, none of which previously appeared with argument syntax in any cached source"
---
# Assign Pods to Nodes (kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/)

> **Extraction note.** All command lines below are **[VERBATIM]** and safe to reproduce
> exactly as written.

## List the nodes in the cluster

    kubectl get nodes

## List nodes with their labels

    kubectl get nodes --show-labels

## Add a label to a node

    kubectl label nodes <your-node-name> disktype=ssd

## Verify the label was added

    kubectl get nodes --show-labels

## Verify the Pod was scheduled to the chosen node

    kubectl get pods --output=wide

## The nodeSelector step

**[VERBATIM]**

> This pod configuration file describes a pod that has a node selector, `disktype: ssd`.
> This means that the pod will get scheduled on a node that has a `disktype=ssd` label.

---

NOT IN THIS SNAPSHOT: the full YAML manifests referenced by the task, and the
"Create a pod that gets scheduled to a specific node" section using `nodeName`.

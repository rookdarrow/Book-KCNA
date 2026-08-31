---
source_url: "https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/"
fetched_at: "2026-08-31T04:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs; retrieved from the kubernetes/website source of record)"
objectives_covered: ["D3.1"]
concepts_covered: ["kustomize", "kustomization-yaml", "base-and-overlay", "strategic-merge-patch", "json-patch", "configmap-generator", "secret-generator", "kubectl-apply-k", "templating-versus-overlay"]
---
# Declarative Management of Kubernetes Objects Using Kustomize (kubernetes.io)

Kustomize is a standalone tool to customize Kubernetes objects through a kustomization file.

Since 1.14, kubectl also supports the management of Kubernetes objects using a kustomization file. To view resources found in a directory containing a kustomization file, run the following command:

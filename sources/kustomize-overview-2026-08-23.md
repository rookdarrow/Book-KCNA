---
source_url: "https://kustomize.io/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kustomize (Kubernetes SIG CLI)"
objectives_covered: ["D3 Application Delivery"]
concepts_covered: ["kustomize", "template-free", "overlays", "kubectl-apply-k", "kustomization-yaml"]
---
# Kustomize (kustomize.io)

Kubernetes native configuration management. Kustomize introduces a template-free way to customize application configuration that simplifies the use of off-the-shelf applications. Kustomize is built into kubectl as `apply -k`. It uses a purely declarative approach to configuration customization, encouraging a fork/modify/rebase workflow: a base directory holds the upstream manifests and a kustomization.yaml; overlays (for example dev, staging, prod) reference the base and layer patches, name prefixes/suffixes, labels, images, and generated ConfigMaps/Secrets on top — managing any number of distinctly customized Kubernetes configurations without forking the originals.

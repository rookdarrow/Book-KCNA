---
source_url: "https://kubectl.docs.kubernetes.io/references/kustomize/kustomization/"
fetched_at: "2026-08-31T04:20:00-0400"
authority: "Kubernetes project (Kubectl Book — kustomize reference)"
objectives_covered: ["D3.1"]
concepts_covered: ["kustomization-yaml", "base-and-overlay", "strategic-merge-patch", "json-patch", "configmap-generator", "secret-generator", "kustomize"]
---
# Kustomization file reference (kubectl.docs.kubernetes.io/references/kustomize/kustomization/)

The kustomization file is a YAML specification of a Kubernetes Resource Model (KRM) object called a *Kustomization*. A kustomization describes how to generate or transform other KRM objects.

## Fields

- **resources** — Resources to include.
- **configMapGenerator** — Generate ConfigMap resources.
- **secretGenerator** — Generate Secret resources.
- **generatorOptions** — Control behavior of ConfigMap and Secret generators.
- **namespace** — Adds namespace to all resources.
- **namePrefix** — Prepends the value to the names of all resources and references.
- **nameSuffix** — Appends the value to the names of all resources and references.
- **labels** — Add labels and optionally selectors to all resources.
- **commonLabels** — Add labels and selectors to add all resources.
- **commonAnnotations** — Add annotations to add all resources.
- **images** — Modify the name, tags and/or digest for images.
- **replicas** — Change the number of replicas for a resource.
- **replacements** — Substitute field(s) in N target(s) with a field from a source.
- **components** — Compose kustomizations.
- **crds** — Adding CRD support
- **bases** — Add resources from a kustomization dir.
- **patches** — Patch resources
- **patchesJson6902** — Patch resources using the json 6902 standard
- **patchesStrategicMerge** — Patch resources using the strategic merge patch standard.
- **vars** — Substitute name references.
- **openapi** — Specify where kustomize gets its OpenAPI schema.
- **buildMetadata** — Specify options for including information about the build in annotations or labels.
- **helmCharts** — Helm chart inflation generator.
- **sortOptions** — Change the strategy used to sort resources at the end of the Kustomize build.

## Structure

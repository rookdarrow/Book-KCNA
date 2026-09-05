---
source_url: "https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/"
fetched_at: "2026-09-04T17:10:00-0400"
authority: "Kubernetes project (kubernetes.io/docs; retrieved from the kubernetes/website source of record, content/en/docs/tasks/manage-kubernetes-objects/kustomization.md on branch main, because the rendered page truncated before the patches section)"
objectives_covered: ["D3.1"]
concepts_covered: ["kustomize", "kustomization-yaml", "base-and-overlay", "strategic-merge-patch", "json-patch", "configmap-generator", "secret-generator", "kubectl-apply-k", "templating-versus-overlay"]
---

# Declarative Management of Kubernetes Objects Using Kustomize (kubernetes.io)

> **Snapshot note.** Fetched 2026-09-04 to close Chapter 14's G-14c (the strategic-merge
> versus JSON-patch semantics, which the 2026-08-31 capture of this same page stopped before).
> Same page, same source_url. Scope of this capture: the opening definition, the
> Composing/Customizing prose, the Bases and Overlays definitions, and the feature-list rows
> for the two patch fields. Not transcribed: the shell examples, the generator walkthroughs,
> and the `images` / `replacements` material.

## Opening definition and `kubectl apply -k`

"Kustomize is a standalone tool to customize Kubernetes objects through a kustomization file."

"Since 1.14, kubectl also supports the management of Kubernetes objects using a kustomization
file."

"To apply those resources, run `kubectl apply` with `--kustomize` or `-k` flag:
`kubectl apply -k <kustomization_directory>`"

## Overview of Kustomize

"Kustomize is a tool for customizing Kubernetes configurations. It has the following features to
manage application configuration files:
- generating resources from other sources
- setting cross-cutting fields for resources
- composing and customizing collections of resources"

## Composing and Customizing Resources

"Kustomize offers composing resources from different files and applying patches or other
customization to them."

### Composing

"Kustomize supports composition of different resources. The `resources` field, in the
`kustomization.yaml` file, defines the list of resources to include in a configuration."

### Customizing

"Patches can be used to apply different customizations to resources. Kustomize supports
different patching mechanisms through `StrategicMerge` and `Json6902` using the `patches`
field. `patches` may be a file or an inline string, targeting a single or multiple resources."

"The `patches` field contains a list of patches applied in the order they are specified. The
patch target selects resources by `group`, `version`, `kind`, `name`, `namespace`,
`labelSelector` and `annotationSelector`."

"Small patches that do one thing are recommended. For example, create one patch for increasing
the deployment replica number and another patch for setting the memory limit. The target
resource is matched using `group`, `version`, `kind`, and `name` fields from the patch file."

(The page's strategic-merge example is a file `increase_replicas.yaml` containing only
`apiVersion`, `kind`, `metadata.name` and `spec.replicas: 3` — a fragment shaped like the
Deployment it changes.)

"Not all resources or fields support `strategicMerge` patches. To support modifying arbitrary
fields in arbitrary resources, Kustomize offers applying JSON patch through `Json6902`. To find
the correct Resource for a `Json6902` patch, it is mandatory to specify the `target` field in
`kustomization.yaml`."

(The page's JSON-patch example is a list of operations: `- op: replace`,
`path: /spec/replicas`, `value: 3`. The linked standard is RFC 6902.)

"For example, increasing the replica number of a Deployment object can also be done through
`Json6902` patch. The target resource is matched using `group`, `version`, `kind`, and `name`
from the `target` field."

## Bases and Overlays

"Kustomize has the concepts of **bases** and **overlays**. A **base** is a directory with a
`kustomization.yaml`, which contains a set of resources and associated customization. A base
could be either a local directory or a directory from a remote repo, as long as a
`kustomization.yaml` is present inside. An **overlay** is a directory with a
`kustomization.yaml` that refers to other kustomization directories as its `bases`. A **base**
has no knowledge of an overlay and can be used in multiple overlays."

"The `kustomization.yaml` in an **overlay** directory may refer to multiple `bases`, combining
all the resources defined in these bases into a unified configuration. Additionally, it can
apply customizations on top of these resources to meet specific requirements."

## How to apply/view/delete objects using Kustomize

"Use `--kustomize` or `-k` in `kubectl` commands to recognize resources managed by
`kustomization.yaml`. Note that `-k` should point to a kustomization directory."

## Kustomize Feature List (rows relevant to Ch 14)

| Field | Type | Explanation |
|---|---|---|
| images | []Image | "Each entry is to modify the name, tags and/or digest for one image without creating patches" |
| patchesJson6902 | []Patch | "Each entry in this list should resolve to a Kubernetes object and a Json Patch" |
| patchesStrategicMerge | []string | "Each entry in this list should resolve a strategic merge patch of a Kubernetes object" |

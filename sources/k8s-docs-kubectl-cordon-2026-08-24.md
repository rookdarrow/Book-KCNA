---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_cordon/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/kubectl/generated/kubectl_cordon/_index.md"
fetched_at: "2026-08-24T18:58:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["cordon", "unschedulable-node", "verb-resource-grammar"]
---
# kubectl cordon (generated reference)

> **Extraction note.** All passages below are **[VERBATIM]**.

## Synopsis

> "Mark node as unschedulable."

## Usage

> `kubectl cordon NODE`

## Examples

> `kubectl cordon foo`

---

Useful to sec.1 as the grammar instantiation: the synopsis is one verb, one resource type,
one name -- `kubectl` / `cordon` / `NODE` -- which is the four-slot shape with the flags
slot empty. The chapter's opening command, in the project's own reference form.

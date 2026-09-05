---
source_url: "https://helm.sh/docs/topics/charts/"
fetched_at: "2026-09-04T17:20:00-0400"
authority: "Helm project (CNCF graduated project); retrieved from the helm/helm-www source of record, docs/topics/charts.mdx on branch main, because helm.sh was unreachable from the fetch layer"
objectives_covered: ["D3.1"]
concepts_covered: ["chart", "chart-crds-directory", "crd-ordering-problem", "chart-dependencies-directory", "chart-templates-directory"]
---

# Helm — Charts (helm.sh/docs/topics/charts/) — the CRD section

> **Snapshot note.** Fetched 2026-09-04 to source the ordering claim that ch14-fig02's render
> carries ("Installed before the templates render") and that Chapter 14 §2 and §6 now state.
> The two earlier captures of this page (helm-charts-2026-08-23, helm-charts-2026-08-31) stop
> before this section. Scope of this capture: the reserved-directory sentence, the "Custom
> Resource Definitions (CRDs)" section and its "Limitations on CRDs" subsection. Not
> transcribed: the CronTab example YAML, chart hooks, library charts, schema files.

## The Chart File Structure (closing sentence)

"Helm reserves use of the `charts/`, `crds/`, and `templates/` directories, and of the listed
file names. Other files will be left as they are."

## Custom Resource Definitions (CRDs)

"Kubernetes provides a mechanism for declaring new types of Kubernetes objects. Using
CustomResourceDefinitions (CRDs), Kubernetes developers can declare custom resource types."

"In Helm 3, CRDs are treated as a special kind of object. They are installed before the rest
of the chart, and are subject to some limitations."

"CRD YAML files should be placed in the `crds/` directory inside of a chart. Multiple CRDs
(separated by YAML start and end markers) may be placed in the same file. Helm will attempt to
load _all_ of the files in the CRD directory into Kubernetes."

"CRD files _cannot be templated_. They must be plain YAML documents."

"When Helm installs a new chart, it will upload the CRDs, pause until the CRDs are made
available by the API server, and then start the template engine, render the rest of the chart,
and upload it to Kubernetes. Because of this ordering, CRD information is available in the
`.Capabilities` object in Helm templates, and Helm templates may create new instances of
objects that were declared in CRDs."

"Helm will make sure that the `CronTab` kind has been installed and is available from the
Kubernetes API server before it proceeds installing the things in `templates/`."

### Limitations on CRDs

"Unlike most objects in Kubernetes, CRDs are installed globally. For that reason, Helm takes a
very cautious approach in managing CRDs. CRDs are subject to the following limitations:

- CRDs are never reinstalled. If Helm determines that the CRDs in the `crds/` directory are
  already present (regardless of version), Helm will not attempt to install or upgrade.
- CRDs are never installed on upgrade or rollback. Helm will only create CRDs on installation
  operations.
- CRDs are never deleted. Deleting a CRD automatically deletes all of the CRD's contents across
  all namespaces in the cluster. Consequently, Helm will not delete CRDs."

"Operators who want to upgrade or delete CRDs are encouraged to do this manually and with great
care."

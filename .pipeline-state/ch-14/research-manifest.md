# Research Manifest — KCNA Chapter 14

**Chapter:** 14 — Packing for the Voyage
**Domain:** D3.1 Cloud Native Application Delivery (published weight 16%)
**Research run:** 2026-08-31
**Prior cached corpus for this chapter:** 33 lines total (`helm-charts-2026-08-23.md`, 23 lines; `kustomize-overview-2026-08-23.md`, 10 lines). Blocking gap G19 (Kustomize) is now **closed**.

All eight snapshots named as mandatory in the outline's Open Question 1 were fetched, plus eight supporting snapshots. Open Questions **1, 3(a), 3(b) and 5 are resolved**; Open Question 2 is resolved *against* the outline's stated basis and needs an author decision — see **Notes for the author, item 1**.

---

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts | Feeds |
|---|---|---|---|---|
| `helm-charts-2026-08-31.md` | Helm project (CNCF graduated) | D3.1 | chart, chart-yaml, values-yaml, chart-templates-directory, chart-dependencies-directory, chart-crds-directory, subchart, notes-txt, go-template-in-helm, chart-version-versus-appversion, crd-ordering-problem | §2, §4, §6 |
| `k8s-docs-kustomization-2026-08-31.md` | Kubernetes project (kubernetes.io/docs) | D3.1 | kustomize, kustomization-yaml, base-and-overlay, strategic-merge-patch, json-patch, configmap-generator, secret-generator, kubectl-apply-k | §5 (all of it) |
| `helm-using-helm-2026-08-31.md` | Helm project | D3.1 | helm-release, helm-release-revision, helm-rollback-versus-rollout-undo, helm-install, helm-upgrade, helm-rollback, helm-list | §3 |
| `helm-rollback-cli-2026-08-31.md` | Helm project | D3.1 | helm-rollback, helm-release-revision | §3 |
| `helm-chart-repository-2026-08-31.md` | Helm project | D3.1 | chart-repository, helm-repo-add | §4, trap 81 |
| `helm-oci-registries-2026-08-31.md` | Helm project | D3.1 | oci-registry-as-chart-store, chart-repository | §4 |
| `helm-blog-oci-ga-2026-08-31.md` | Helm project (blog) | D3.1 | oci-registry-as-chart-store | §4 |
| `helm-crd-best-practices-2026-08-31.md` | Helm project | D3.1 | chart-crds-directory, crd-ordering-problem | §6 (discharges `chapter-06:1036`) |
| `helm-changes-since-helm2-2026-08-31.md` | Helm project | D3.1 | helm, helm-release, tiller-hazard, chart-yaml, oci-registry-as-chart-store | Exam Alert (Tiller), §3, §2 |
| `helm-storage-backends-2026-08-31.md` | Helm project | D3.1 | helm-release, helm-release-revision | §3 (⚓ Worth Securing) |
| `helm-named-templates-2026-08-31.md` | Helm project | D3.1 | chart-helpers, go-template-in-helm | §2 |
| `helm-architecture-2026-08-31.md` | Helm project | D3.1 | helm, chart, chart-repository, helm-release | §2, §3, §7, trap 79 |
| `helm-glossary-2026-08-31.md` | Helm project | D3.1 | chart, helm-release, helm-release-revision, chart-repository, chart-version-versus-appversion, values-yaml | §2, §3, §4 |
| `helm-homepage-2026-08-31.md` | Helm project | D3.1 | helm, chart | trap 79, §7 |
| `kubectl-book-kustomization-fields-2026-08-31.md` | Kubernetes project (Kubectl Book) | D3.1 | kustomization-yaml, strategic-merge-patch, json-patch, configmap-generator, secret-generator | §5 |
| `lf-lfs250-course-outline-2026-08-31.md` | Linux Foundation | D3 (competency name only) | *(negative evidence)* | §1 honesty beat |

**Already cached and still authoritative for this chapter** (no re-fetch needed): `k8s-docs-kubectl-rollout-2026-08-24.md` (the `kubectl rollout undo` half of §3's contrast), `k8s-docs-custom-resources-2026-08-23.md` (Ch 6 §8's owned CRD definition), `oci-distribution-spec-2026-08-24.md` and `oci-overview-2026-08-23.md` (Ch 2 §5's back-bearing for §4), `k8s-docs-configmap-2026-08-23.md` and `k8s-api-ref-secret-v1-2026-08-24.md` (§5 generators), `cncf-kcna-curriculum-pdf-2026-08-23.md` and `cncf-kcna-certification-page-2026-08-23.md` (domain weight).

---

## Gaps

Flagged so drafting does **not** invent facts to fill them.

**G14-1 — CNCF publishes no sub-topic list for Application Delivery, and the LFS250 public page does not name Helm or Kustomize either.** This is worse than the outline assumed. The outline's honesty beat is written on the premise that the topic list is "derived from the bundled LFS250 module." The LFS250 course page publishes its outline only at chapter granularity — "Chapter 6. Cloud Native Application Delivery" — and no sentence on it names Helm or Kustomize (see `lf-lfs250-course-outline-2026-08-31.md`, which is deliberately a *negative-evidence* snapshot). **Drafting may not write "the LFS250 module on Helm" or any equivalent.** The defensible wording is that the bundled course devotes a chapter to Cloud Native Application Delivery, and that Helm and Kustomize are what the CNCF ecosystem uses for it. See Notes item 1.

**G14-2 — No official statement that `helm repo add` does not work with OCI registries.** Both `helm.sh/docs/topics/registries/` and `helm.sh/docs/topics/chart_repository/` were checked; neither addresses it. The §4 contrast between a chart repository and an OCI registry must be built from what each page *does* say (index.yaml vs. `oci://` references), not from an asserted incompatibility.

**G14-3 — No official statement that you cannot upload charts to a chart repository server.** The chart repository page describes hosting on static file hosts and describes `helm repo index`/`helm package`, but contains no sentence stating that repositories have no upload API. Do not assert it; the available, sourced framing is "an HTTP server that can serve YAML and tar files and can answer GET requests."

**G14-4 — No `helm history` example output block found showing revision numbers before/after a rollback.** The *narrative* rule is sourced and decisive (see Notes item 3), but there is no sourced table of revision numbers. If §3 wants to show a revision strip with concrete numbers, that must be authored illustration, not a `[source:]`-tagged claim — or handled entirely by `ch14-fig03`.

**G14-5 — No official source calls Kustomize a "SIG CLI" project in those words.** The Kubernetes doc links to `github.com/kubernetes-sigs/kustomize` and describes Kustomize as "a standalone tool"; the acronym is not used in prose. This *supports* the outline's §5 recommendation to say "maintained by the Kubernetes project itself" and avoid the acronym. No ledger conflict with Ch 17 §8.

**G14-6 — `values.schema.json`, `helm dependency update`, `helm pull`, `helm package`, `helm repo index`, `helm push`, `helm registry login`, `helm show`, `kubectl kustomize`, `kubectl diff -k`, `kubectl get -k`, `kubectl describe -k` are all now sourced but are NOT in the outline's `kb_tags.commands`.** This is not a gap in evidence — it is a note that the corpus now over-covers the outline's deliberately short command list. Per the outline's COMMANDS NOTE, keep the list short; do not teach a command merely because a snapshot exists.

**G14-7 — Trap "assuming `helm rollback` runs `kubectl rollout undo` underneath" has no direct refuting source.** No page says "Helm does not call kubectl rollout undo." The trap is still writable, but only as a *derived* claim built from two sourced halves: `helm rollback` operates on a release and its revision history (`helm-using-helm`, `helm-rollback-cli`, `helm-storage-backends`), and `kubectl rollout undo` operates on one workload (cached `k8s-docs-kubectl-rollout-2026-08-24.md`). Tag both halves; do not tag the conjunction.

---

## Notes for the author

**1. Open Question 2 — the honesty framing. The recommendation is confirmed, but the *basis sentence* must change.**
The outline proposed saying the topic list derives "from the bundled LFS250 module and from what the ecosystem actually uses." The LFS250 fetch will not support the first half at the granularity the outline implies. Sourced, defensible construction:

- CNCF publishes the competency name and the 16% weight, and nothing below that. *(cached curriculum snapshots)*
- The bundled Linux Foundation course devotes one chapter to "Cloud Native Application Delivery." *(`lf-lfs250-course-outline-2026-08-31.md`)* — and its public outline goes no deeper.
- Helm is a CNCF graduated project and describes itself as "the package manager for Kubernetes"; Kustomize ships inside `kubectl`. *(`helm-homepage`, `helm-architecture`, `k8s-docs-kustomization`)*

That is enough to justify the chapter and is honest about what is inferred. The no-frequency-claims rule in the outline's exam_domain note stands unchanged and is, if anything, more strongly warranted now.

**2. Open Question 1 is closed.** All eight mandatory snapshots are in hand, plus a CLI reference for `helm rollback`. §2, §3, §4, §5 and §6 are all now writable with `[source:]` tags.

**3. Open Question 3(a) is RESOLVED, and the answer is the one that makes §3 sharper.** `helm.sh/docs/intro/using_helm/`: *"A release version is an incremental revision. Every time an install, upgrade, or rollback happens, the revision number is incremented by 1."* A Helm rollback **does** create a new revision — it moves forward in the history to restore an earlier state. This is a genuinely good contrast beat against `kubectl rollout undo`, and it is now tagged rather than remembered.

**4. Open Question 3(b) is RESOLVED, and the ⚓ Worth Securing is available.** Two independent Helm pages: *"By default, release information is stored in Secrets in the namespace of the release"* (`topics/advanced`), and *"In Helm 3, Secrets are now used as the default storage driver"* (`faq/changes_since_helm2`). `HELM_DRIVER` accepts `configmap`, `secret`, `sql`. The Ch 4 §4 back-bearing the outline hoped for is fully supported.

**5. Open Question 5 is RESOLVED — the Tiller hazard is writable and the source is unusually good.** `faq/changes_since_helm2` gives the whole argument verbatim, including the RBAC-permissiveness reasoning and *"one of the first decisions we made regarding Helm 3 was to completely remove Tiller"* and *"Helm's permissions are evaluated using your kubeconfig file."* Note the page carries no date for the removal, so **do not write "removed in 2019"** unless a dated source is added; write "removed in Helm 3."

**6. ⚠ The Kubernetes Kustomize doc contradicts itself, and §5 must pick a side deliberately.** Within the single page `kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/`:
- The **worked examples** use the modern forms: `resources: - ../base` for overlays, and a unified `patches:` field carrying both `StrategicMerge` and `Json6902` patches.
- The **prose** in "Bases and Overlays" still says an overlay "refers to other kustomization directories as its `bases`."
- The **Kustomize Feature List table** still lists `bases`, `patchesStrategicMerge`, and `patchesJson6902` as fields.

Recommendation: teach what the examples show (`resources:` and `patches:` with `target:`), because that is what a reader will get from a current kubectl. Name the older field names once, in a single clause, so a reader meeting third-party material recognizes them. The Kubectl Book field reference (`kubectl-book-kustomization-fields-2026-08-31.md`) lists both old and new fields side by side without marking either deprecated — so **do not write "deprecated"**; write "older form."

**7. ⚠ Extraction-fidelity warning for `helm-architecture-2026-08-31.md`.** That page appears to have been rewritten from the wording long quoted in third-party material ("Helm is a tool for managing Kubernetes packages called charts"). Two independent extraction passes agreed on the sentences included in the snapshot, but the passes disagreed on the page's *heading structure*, so only the sentences confirmed by both passes were kept and the bullet list was dropped. If a fact-accuracy pass needs the bullet list, re-fetch. Nothing in the chapter outline depends on it — `helm-homepage-2026-08-31.md` carries the "package manager" claim independently, which is what trap 79 needs.

**8. `helm-glossary-2026-08-31.md` is deliberately partial.** Several glossary entries came back as extraction paraphrase rather than quotation and were omitted rather than smuggled in as evidence. Entries for *Chart Dependency (Subcharts)*, *Provenance file*, *Helm (and helm)*, *Release Number*, and *Values* are absent for that reason. The concepts they cover are sourced elsewhere in this batch (`helm-charts`, `helm-using-helm`, `helm-architecture`), so nothing is blocked — but do not cite the glossary for them.

**9. The `crds/` limitation is stated two different ways by two Helm pages, and both are quotable.** `topics/charts` enumerates three bullets ("CRDs are never reinstalled… never installed on upgrade or rollback… never deleted"). `chart_best_practices/custom_resource_definitions` compresses it to *"There is no support at this time for upgrading or deleting CRDs using Helm."* They do not conflict. §6 should use the compressed sentence for the claim and the three bullets for the detail.

**10. §6's `crds/` payoff is now fully sourced, including the ordering mechanism.** `topics/charts` gives the whole causal chain verbatim: Helm uploads the CRDs, *"pause[s] until the CRDs are made available by the API server, and then start[s] the template engine."* That is precisely §1's failure #2 returning as something solvable, exactly as the outline planned, and it discharges `chapter-06:1036` with a tag rather than an assertion.

**11. §4's OCI beat is sourced and dated.** Helm 3.8.0 is the version: *"With the release of Helm 3.8.0, Helm is able to store and work with charts in container registries, as an alternative to Helm repositories"* (blog, dated February 28, 2022). The `HELM_EXPERIMENTAL_OCI=1` flag survives in the older FAQ text and is quoted there — useful as a second instance of the blueprint-transition beat (old material describing a Helm that no longer behaves that way), alongside Tiller.

**12. Supersession.** `helm-charts-2026-08-31.md` supersedes the 23-line `helm-charts-2026-08-23.md`; `k8s-docs-kustomization-2026-08-31.md` and `kubectl-book-kustomization-fields-2026-08-31.md` supersede the 10-line `kustomize-overview-2026-08-23.md`. The old files are left in place (they are cited by nothing yet) but should not be the citation of record for this chapter. Consider a cleanup pass at reconciliation.

---

### A1 · `helm-charts-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/topics/charts/"
fetched_at: "2026-08-31T04:12:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm", "chart", "chart-yaml", "values-yaml", "chart-templates-directory", "chart-dependencies-directory", "chart-crds-directory", "subchart", "notes-txt", "go-template-in-helm", "chart-version-versus-appversion", "crd-ordering-problem"]
---
# Helm — Charts (helm.sh/docs/topics/charts/)

Helm uses a packaging format called *charts*. A chart is a collection of files that describe a related set of Kubernetes resources. A single chart might be used to deploy something simple, like a memcached pod, or something complex, like a full web app stack with HTTP servers, databases, caches, and so on.

Charts are created as files laid out in a particular directory tree. They can be packaged into versioned archives to be deployed.

## The Chart File Structure

A chart is organized as a collection of files inside of a directory. The directory name is the name of the chart (without versioning information). Thus, a chart describing WordPress would be stored in a `wordpress/` directory.

Inside of this directory, Helm will expect a structure that matches this:

```
wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  values.yaml         # The default configuration values for this chart
  values.schema.json  # OPTIONAL: A JSON Schema for imposing a structure on the values.yaml file
  charts/             # A directory containing any charts upon which this chart depends.
  crds/               # Custom Resource Definitions
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
```

Helm reserves use of the `charts/`, `crds/`, and `templates/` directories, and of the listed file names. Other files will be left as they are.

## The Chart.yaml File

The `Chart.yaml` file is required for a chart. It contains the following fields:

```
apiVersion: The chart API version (required)
name: The name of the chart (required)
version: The version of the chart (required)
kubeVersion: A SemVer range of compatible Kubernetes versions (optional)
description: A single-sentence description of this project (optional)
type: The type of the chart (optional)
keywords:
  - A list of keywords about this project (optional)
home: The URL of this projects home page (optional)
sources:
  - A list of URLs to source code for this project (optional)
dependencies: # A list of the chart requirements (optional)
  - name: The name of the chart (nginx)
    version: The version of the chart ("1.2.3")
    repository: (optional) The repository URL ("https://example.com/charts") or alias ("@repo-name")
    condition: (optional) A yaml path that resolves to a boolean, used for enabling/disabling charts (e.g. subchart1.enabled )
    tags: # (optional)
      - Tags can be used to group charts for enabling/disabling together
    import-values: # (optional)
      - ImportValues holds the mapping of source values to parent key to be imported. Each item can be a string or pair of child/parent sublist items.
    alias: (optional) Alias to be used for the chart. Useful when you have to add the same chart multiple times
maintainers: # (optional)
  - name: The maintainers name (required for each maintainer)
    email: The maintainers email (optional for each maintainer)
    url: A URL for the maintainer (optional for each maintainer)
icon: A URL to an SVG or PNG image to be used as an icon (optional).
appVersion: The version of the app that this contains (optional). Needn't be SemVer. Quotes recommended.
deprecated: Whether this chart is deprecated (optional, boolean)
annotations:
  example: A list of annotations keyed by name (optional).
```

As of v3.3.2, additional fields are not allowed. The recommended approach is to add custom metadata in `annotations`.

### Charts and Versioning

Every chart must have a version number. A version should follow the SemVer 2 standard but it is not strictly enforced. Unlike Helm Classic, Helm v2 and later uses version numbers as release markers. Packages in repositories are identified by name plus version.

For example, an `nginx` chart whose version field is set to `version: 1.2.3` will be named:

```
nginx-1.2.3.tgz
```

More complex SemVer 2 names are also supported, such as `version: 1.2.3-alpha.1+ef365`. But non-SemVer names are explicitly disallowed by the system. Subject to exception are versions in format `x` or `x.y`. For example, if there is a leading v or a version listed without all 3 parts (e.g. v1.2) it will attempt to coerce it into a valid semantic version (e.g., v1.2.0).

**NOTE:** Whereas Helm Classic and Deployment Manager were both very GitHub oriented when it came to charts, Helm v2 and later does not rely upon or require GitHub or even Git. Consequently, it does not use Git SHAs for versioning at all.

The `version` field inside of the `Chart.yaml` is used by many of the Helm tools, including the CLI. When generating a package, the `helm package` command will use the version that it finds in the `Chart.yaml` as a token in the package name. The system assumes that the version number in the chart package name matches the version number in the `Chart.yaml`. Failure to meet this assumption will cause an error.

### The `apiVersion` Field

The `apiVersion` field should be `v2` for Helm charts that require at least Helm 3. Charts supporting previous Helm versions have an `apiVersion` set to `v1` and are still installable by Helm 3.

Changes from `v1` to `v2`:

*   A `dependencies` field defining chart dependencies, which were located in a separate `requirements.yaml` file for `v1` charts.
*   The `type` field, discriminating application and library charts.

### The `appVersion` Field

Note that the `appVersion` field is not related to the `version` field. It is a way of specifying the version of the application. For example, the `drupal` chart may have an `appVersion: "8.2.1"`, indicating that the version of Drupal included in the chart (by default) is `8.2.1`. This field is informational, and has no impact on chart version calculations. Wrapping the version in quotes is highly recommended. It forces the YAML parser to treat the version number as a string. Leaving it unquoted can lead to parsing issues in some cases. For example, YAML interprets `1.0` as a floating point value, and a git commit SHA like `1234e10` as scientific notation.

As of Helm v3.5.0, `helm create` wraps the default `appVersion` field in quotes.

### Chart Types

The `type` field defines the type of chart. There are two types: `application` and `library`. Application is the default type and it is the standard chart which can be operated on fully. The library chart provides utilities or functions for the chart builder. A library chart differs from an application chart because it is not installable and usually doesn't contain any resource objects.

**Note:** An application chart can be used as a library chart. This is enabled by setting the type to `library`. The chart will then be rendered as a library chart where all utilities and functions can be leveraged. All resource objects of the chart will not be rendered.

## Chart Dependencies

In Helm, one chart may depend on any number of other charts. These dependencies can be dynamically linked using the `dependencies` field in `Chart.yaml` or brought in to the `charts/` directory and managed manually.

### Managing Dependencies with the `dependencies` field

The charts required by the current chart are defined as a list in the `dependencies` field.

```
dependencies:
  - name: apache
    version: 1.2.3
    repository: https://example.com/charts
  - name: mysql
    version: 3.2.1
    repository: https://another.example.com/charts
```

*   The `name` field is the name of the chart you want.
*   The `version` field is the version of the chart you want.
*   The `repository` field is the full URL to the chart repository. Note that you must also use `helm repo add` to add that repo locally.
*   You might use the name of the repo instead of URL

```
$ helm repo add fantastic-charts https://charts.helm.sh/incubator

dependencies:
  - name: awesomeness
    version: 1.0.0
    repository: "@fantastic-charts"
```

Once you have defined dependencies, you can run `helm dependency update` and it will use your dependency file to download all the specified charts into your `charts/` directory for you.

When `helm dependency update` retrieves charts, it will store them as chart archives in the `charts/` directory. So for the example above, one would expect to see the following files in the charts directory:

```
charts/
  apache-1.2.3.tgz
  mysql-3.2.1.tgz
```

#### Alias field in dependencies

In addition to the other fields above, each requirements entry may contain the optional field `alias`.

Adding an alias for a dependency chart would put a chart in dependencies using alias as name of new dependency.

One can use `alias` in cases where they need to access a chart with other name(s).

```
# parentchart/Chart.yaml
dependencies:
  - name: subchart
    repository: http://localhost:10191
    version: 0.1.0
    alias: new-subchart-1
  - name: subchart
    repository: http://localhost:10191
    version: 0.1.0
    alias: new-subchart-2
  - name: subchart
    repository: http://localhost:10191
    version: 0.1.0
```

In the above example we will get 3 dependencies in all for `parentchart`:

```
subchart
new-subchart-1
new-subchart-2
```

The manual way of achieving this is by copy/pasting the same chart in the `charts/` directory multiple times with different names.

#### Tags and Condition fields in dependencies

All charts are loaded by default. If `tags` or `condition` fields are present, they will be evaluated and used to control loading for the chart(s) they are applied to.

Condition - The condition field holds one or more YAML paths (delimited by commas). If this path exists in the top parent's values and resolves to a boolean value, the chart will be enabled or disabled based on that boolean value. Only the first valid path found in the list is evaluated and if no paths exist then the condition has no effect.

Tags - The tags field is a YAML list of labels to associate with this chart. In the top parent's values, all charts with tags can be enabled or disabled by specifying the tag and a boolean value.

##### Tags and Condition Resolution

*   **Conditions (when set in values) always override tags.** The first condition path that exists wins and subsequent ones for that chart are ignored.
*   Tags are evaluated as 'if any of the chart's tags are true then enable the chart'.
*   Tags and conditions values must be set in the top parent's values.
*   The `tags:` key in values must be a top level key. Globals and nested `tags:` tables are not currently supported.

### Managing Dependencies manually via the `charts/` directory

If more control over dependencies is desired, these dependencies can be expressed explicitly by copying the dependency charts into the `charts/` directory.

A dependency should be an unpacked chart directory but its name cannot start with `_` or `.`. Such files are ignored by the chart loader.

For example, if the WordPress chart depends on the Apache chart, the Apache chart (of the correct version) is supplied in the WordPress chart's `charts/` directory:

```
wordpress:
  Chart.yaml
  # ...
  charts/
    apache/
      Chart.yaml
      # ...
    mysql/
      Chart.yaml
      # ...
```

The example above shows how the WordPress chart expresses its dependency on Apache and MySQL by including those charts inside of its `charts/` directory.

**TIP:** *To drop a dependency into your `charts/` directory, use the `helm pull` command*

### Operational aspects of using dependencies

Suppose that a chart named "A" creates the following Kubernetes objects

*   namespace "A-Namespace"
*   statefulset "A-StatefulSet"
*   service "A-Service"

Furthermore, A is dependent on chart B that creates objects

*   namespace "B-Namespace"
*   replicaset "B-ReplicaSet"
*   service "B-Service"

After installation/upgrade of chart A a single Helm release is created/modified. The release will create/update all of the above Kubernetes objects in the following order:

*   A-Namespace
*   B-Namespace
*   A-Service
*   B-Service
*   B-ReplicaSet
*   A-StatefulSet

This is because when Helm installs/upgrades charts, the Kubernetes objects from the charts and all its dependencies are

*   aggregated into a single set; then
*   sorted by type followed by name; and then
*   created/updated in that order.

Hence a single release is created with all the objects for the chart and its dependencies.

The install order of Kubernetes types is given by the enumeration InstallOrder in kind_sorter.go.

## Custom Resource Definitions (CRDs)

Kubernetes provides a mechanism for declaring new types of Kubernetes objects. Using CustomResourceDefinitions (CRDs), Kubernetes developers can declare custom resource types.

In Helm 3, CRDs are treated as a special kind of object. They are installed before the rest of the chart, and are subject to some limitations.

CRD YAML files should be placed in the `crds/` directory inside of a chart. Multiple CRDs (separated by YAML start and end markers) may be placed in the same file. Helm will attempt to load *all* of the files in the CRD directory into Kubernetes.

CRD files *cannot be templated*. They must be plain YAML documents.

When Helm installs a new chart, it will upload the CRDs, pause until the CRDs are made available by the API server, and then start the template engine, render the rest of the chart, and upload it to Kubernetes. Because of this ordering, CRD information is available in the `.Capabilities` object in Helm templates, and Helm templates may create new instances of objects that were declared in CRDs.

For example, if your chart had a CRD for `CronTab` in the `crds/` directory, you may create instances of the `CronTab` kind in the `templates/` directory:

```
crontabs/
  Chart.yaml
  crds/
    crontab.yaml
  templates/
    mycrontab.yaml
```

The `crontab.yaml` file must contain the CRD with no template directives:

```
kind: CustomResourceDefinition
metadata:
  name: crontabs.stable.example.com
spec:
  group: stable.example.com
  versions:
    - name: v1
      served: true
      storage: true
  scope: Namespaced
  names:
    plural: crontabs
    singular: crontab
    kind: CronTab
```

Then the template `mycrontab.yaml` may create a new `CronTab` (using templates as usual):

```
apiVersion: stable.example.com
kind: CronTab
metadata:
  name: {{ .Values.name }}
spec:
   # ...
```

Helm will make sure that the `CronTab` kind has been installed and is available from the Kubernetes API server before it proceeds installing the things in `templates/`.

### Limitations on CRDs

Unlike most objects in Kubernetes, CRDs are installed globally. For that reason, Helm takes a very cautious approach in managing CRDs. CRDs are subject to the following limitations:

*   CRDs are never reinstalled. If Helm determines that the CRDs in the `crds/` directory are already present (regardless of version), Helm will not attempt to install or upgrade.
*   CRDs are never installed on upgrade or rollback. Helm will only create CRDs on installation operations.
*   CRDs are never deleted. Deleting a CRD automatically deletes all of the CRD's contents across all namespaces in the cluster. Consequently, Helm will not delete CRDs.

Operators who want to upgrade or delete CRDs are encouraged to do this manually and with great care.

## Templates and Values

Helm Chart templates are written in the Go template language, with the addition of 50 or so add-on template functions from the Sprig library and a few other specialized functions.

All template files are stored in a chart's `templates/` folder. When Helm renders the charts, it will pass every file in that directory through the template engine.

Values for the templates are supplied two ways:

*   Chart developers may supply a file called `values.yaml` inside of a chart. This file can contain default values.
*   Chart users may supply a YAML file that contains values. This can be provided on the command line with `helm install`.

When a user supplies custom values, these values will override the values in the chart's `values.yaml` file.
```

---

### A2 · `k8s-docs-kustomization-2026-08-31.md` (new)
```markdown
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

```shell
kubectl kustomize <kustomization_directory>
```

To apply those resources, run `kubectl apply` with `--kustomize` or `-k` flag:

```shell
kubectl apply -k <kustomization_directory>
```

## Overview of Kustomize

Kustomize is a tool for customizing Kubernetes configurations. It has the following features to manage application configuration files:

* generating resources from other sources
* setting cross-cutting fields for resources
* composing and customizing collections of resources

### Generating Resources

ConfigMaps and Secrets hold configuration or sensitive data that are used by other Kubernetes objects, such as Pods. The source of truth of ConfigMaps or Secrets are usually external to a cluster, such as a `.properties` file or an SSH keyfile. Kustomize has `secretGenerator` and `configMapGenerator`, which generate Secret and ConfigMap from files or literals.

#### configMapGenerator

To generate a ConfigMap from a file, add an entry to the `files` list in `configMapGenerator`. Here is an example of generating a ConfigMap with a data item from a `.properties` file:

```shell
# Create a application.properties file
cat <<EOF >application.properties
FOO=Bar
EOF

cat <<EOF >./kustomization.yaml
configMapGenerator:
- name: example-configmap-1
  files:
  - application.properties
EOF
```

The generated ConfigMap can be examined with the following command:

```shell
kubectl kustomize ./
```

The generated ConfigMap is:

```yaml
apiVersion: v1
data:
  application.properties: |
    FOO=Bar
kind: ConfigMap
metadata:
  name: example-configmap-1-8mbdf7882g
```

To generate a ConfigMap from an env file, add an entry to the `envs` list in `configMapGenerator`. Here is an example of generating a ConfigMap with a data item from a `.env` file:

```shell
# Create a .env file
cat <<EOF >.env
FOO=Bar
EOF

cat <<EOF >./kustomization.yaml
configMapGenerator:
- name: example-configmap-1
  envs:
  - .env
EOF
```

The generated ConfigMap is:

```yaml
apiVersion: v1
data:
  FOO: Bar
kind: ConfigMap
metadata:
  name: example-configmap-1-42cfbf598f
```

NOTE: Each variable in the `.env` file becomes a separate key in the ConfigMap that you generate. This is different from the previous example which embeds a file named `application.properties` (and all its entries) as the value for a single key.

ConfigMaps can also be generated from literal key-value pairs. To generate a ConfigMap from a literal key-value pair, add an entry to the `literals` list in configMapGenerator. Here is an example of generating a ConfigMap with a data item from a key-value pair:

```shell
cat <<EOF >./kustomization.yaml
configMapGenerator:
- name: example-configmap-2
  literals:
  - FOO=Bar
EOF
```

The generated ConfigMap is:

```yaml
apiVersion: v1
data:
  FOO: Bar
kind: ConfigMap
metadata:
  name: example-configmap-2-g2hdhfc6tk
```

To use a generated ConfigMap in a Deployment, reference it by the name of the configMapGenerator. Kustomize will automatically replace this name with the generated name.

The generated Deployment will refer to the generated ConfigMap by name:

```yaml
apiVersion: v1
data:
  application.properties: |
    FOO=Bar
kind: ConfigMap
metadata:
  name: example-configmap-1-g4hk9g2ff8
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: my-app
  name: my-app
spec:
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - image: my-app
        name: app
        volumeMounts:
        - mountPath: /config
          name: config
      volumes:
      - configMap:
          name: example-configmap-1-g4hk9g2ff8
        name: config
```

#### secretGenerator

You can generate Secrets from files or literal key-value pairs. To generate a Secret from a file, add an entry to the `files` list in `secretGenerator`. Here is an example of generating a Secret with a data item from a file:

```shell
# Create a password.txt file
cat <<EOF >./password.txt
username=admin
password=secret
EOF

cat <<EOF >./kustomization.yaml
secretGenerator:
- name: example-secret-1
  files:
  - password.txt
EOF
```

The generated Secret is as follows:

```yaml
apiVersion: v1
data:
  password.txt: dXNlcm5hbWU9YWRtaW4KcGFzc3dvcmQ9c2VjcmV0Cg==
kind: Secret
metadata:
  name: example-secret-1-t2kt65hgtb
type: Opaque
```

To generate a Secret from a literal key-value pair, add an entry to `literals` list in `secretGenerator`. Here is an example of generating a Secret with a data item from a key-value pair:

```shell
cat <<EOF >./kustomization.yaml
secretGenerator:
- name: example-secret-2
  literals:
  - username=admin
  - password=secret
EOF
```

The generated Secret is as follows:

```yaml
apiVersion: v1
data:
  password: c2VjcmV0
  username: YWRtaW4=
kind: Secret
metadata:
  name: example-secret-2-t52t6g96d8
type: Opaque
```

#### generatorOptions

The generated ConfigMaps and Secrets have a content hash suffix appended. This ensures that a new ConfigMap or Secret is generated when the contents are changed. To disable the behavior of appending a suffix, one can use `generatorOptions`. Besides that, it is also possible to specify cross-cutting options for generated ConfigMaps and Secrets.

```shell
cat <<EOF >./kustomization.yaml
configMapGenerator:
- name: example-configmap-3
  literals:
  - FOO=Bar
generatorOptions:
  disableNameSuffixHash: true
  labels:
    type: generated
  annotations:
    note: generated
EOF
```

### Setting cross-cutting fields

It is quite common to set cross-cutting fields for all Kubernetes resources in a project. Some use cases for setting cross-cutting fields:

* setting the same namespace for all resources
* adding the same name prefix or suffix
* adding the same set of labels
* adding the same set of annotations

Here is an example:

```shell
cat <<EOF >./kustomization.yaml
namespace: my-namespace
namePrefix: dev-
nameSuffix: "-001"
labels:
  - pairs:
      app: bingo
    includeSelectors: true
commonAnnotations:
  oncallPager: 800-555-1212
resources:
- deployment.yaml
EOF
```

Run `kubectl kustomize ./` to view those fields are all set in the Deployment Resource:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    oncallPager: 800-555-1212
  labels:
    app: bingo
  name: dev-nginx-deployment-001
  namespace: my-namespace
spec:
  selector:
    matchLabels:
      app: bingo
  template:
    metadata:
      annotations:
        oncallPager: 800-555-1212
      labels:
        app: bingo
    spec:
      containers:
      - image: nginx
        name: nginx
```

### Composing and Customizing Resources

It is common to compose a set of resources in a project and manage them inside the same file or directory. Kustomize offers composing resources from different files and applying patches or other customization to them.

#### Composing

Kustomize supports composition of different resources. The `resources` field, in the `kustomization.yaml` file, defines the list of resources to include in a configuration. Set the path to a resource's configuration file in the `resources` list. Here is an example of an NGINX application comprised of a Deployment and a Service:

```shell
# Create a kustomization.yaml composing them
cat <<EOF >./kustomization.yaml
resources:
- deployment.yaml
- service.yaml
EOF
```

The resources from `kubectl kustomize ./` contain both the Deployment and the Service objects.

#### Customizing

Patches can be used to apply different customizations to resources. Kustomize supports different patching mechanisms through `StrategicMerge` and `Json6902` using the `patches` field. `patches` may be a file or an inline string, targeting a single or multiple resources.

The `patches` field contains a list of patches applied in the order they are specified. The patch target selects resources by `group`, `version`, `kind`, `name`, `namespace`, `labelSelector` and `annotationSelector`.

Small patches that do one thing are recommended. For example, create one patch for increasing the deployment replica number and another patch for setting the memory limit. The target resource is matched using `group`, `version`, `kind`, and `name` fields from the patch file.

```shell
# Create a patch increase_replicas.yaml
cat <<EOF > increase_replicas.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  replicas: 3
EOF

# Create another patch set_memory.yaml
cat <<EOF > set_memory.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  template:
    spec:
      containers:
      - name: my-nginx
        resources:
          limits:
            memory: 512Mi
EOF

cat <<EOF >./kustomization.yaml
resources:
- deployment.yaml
patches:
  - path: increase_replicas.yaml
  - path: set_memory.yaml
EOF
```

Run `kubectl kustomize ./` to view the Deployment:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      run: my-nginx
  template:
    metadata:
      labels:
        run: my-nginx
    spec:
      containers:
      - image: nginx
        name: my-nginx
        ports:
        - containerPort: 80
        resources:
          limits:
            memory: 512Mi
```

Not all resources or fields support `strategicMerge` patches. To support modifying arbitrary fields in arbitrary resources, Kustomize offers applying JSON patch through `Json6902`. To find the correct Resource for a `Json6902` patch, it is mandatory to specify the `target` field in `kustomization.yaml`.

For example, increasing the replica number of a Deployment object can also be done through `Json6902` patch. The target resource is matched using `group`, `version`, `kind`, and `name` from the `target` field.

```shell
# Create a json patch
cat <<EOF > patch.yaml
- op: replace
  path: /spec/replicas
  value: 3
EOF

# Create a kustomization.yaml
cat <<EOF >./kustomization.yaml
resources:
- deployment.yaml

patches:
- target:
    group: apps
    version: v1
    kind: Deployment
    name: my-nginx
  path: patch.yaml
EOF
```

In addition to patches, Kustomize also offers customizing container images or injecting field values from other objects into containers without creating patches. For example, you can change the image used inside containers by specifying the new image in the `images` field in `kustomization.yaml`.

```shell
cat <<EOF >./kustomization.yaml
resources:
- deployment.yaml
images:
- name: nginx
  newName: my.image.registry/nginx
  newTag: "1.4.0"
EOF
```

Sometimes, the application running in a Pod may need to use configuration values from other objects. For example, a Pod from a Deployment object need to read the corresponding Service name from Env or as a command argument. Since the Service name may change as `namePrefix` or `nameSuffix` is added in the `kustomization.yaml` file. It is not recommended to hard code the Service name in the command argument. For this usage, Kustomize can inject the Service name into containers through `replacements`.

```shell
cat <<EOF >./kustomization.yaml
namePrefix: dev-
nameSuffix: "-001"

resources:
- deployment.yaml
- service.yaml

replacements:
- source:
    kind: Service
    name: my-nginx
    fieldPath: metadata.name
  targets:
  - select:
      kind: Deployment
      name: my-nginx
    fieldPaths:
    - spec.template.spec.containers.0.command.2
EOF
```

## Bases and Overlays

Kustomize has the concepts of **bases** and **overlays**. A **base** is a directory with a `kustomization.yaml`, which contains a set of resources and associated customization. A base could be either a local directory or a directory from a remote repo, as long as a `kustomization.yaml` is present inside. An **overlay** is a directory with a `kustomization.yaml` that refers to other kustomization directories as its `bases`. A **base** has no knowledge of an overlay and can be used in multiple overlays.

The `kustomization.yaml` in an **overlay** directory may refer to multiple `bases`, combining all the resources defined in these bases into a unified configuration. Additionally, it can apply customizations on top of these resources to meet specific requirements.

Here is an example of a base:

```shell
# Create a directory to hold the base
mkdir base
# Create a base/deployment.yaml
cat <<EOF > base/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  selector:
    matchLabels:
      run: my-nginx
  replicas: 2
  template:
    metadata:
      labels:
        run: my-nginx
    spec:
      containers:
      - name: my-nginx
        image: nginx
EOF

# Create a base/service.yaml file
cat <<EOF > base/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nginx
  labels:
    run: my-nginx
spec:
  ports:
  - port: 80
    protocol: TCP
  selector:
    run: my-nginx
EOF
# Create a base/kustomization.yaml
cat <<EOF > base/kustomization.yaml
resources:
- deployment.yaml
- service.yaml
EOF
```

This base can be used in multiple overlays. You can add different `namePrefix` or other cross-cutting fields in different overlays. Here are two overlays using the same base.

```shell
mkdir dev
cat <<EOF > dev/kustomization.yaml
resources:
- ../base
namePrefix: dev-
EOF

mkdir prod
cat <<EOF > prod/kustomization.yaml
resources:
- ../base
namePrefix: prod-
EOF
```

## How to apply/view/delete objects using Kustomize

Use `--kustomize` or `-k` in `kubectl` commands to recognize resources managed by `kustomization.yaml`. Note that `-k` should point to a kustomization directory, such as

```shell
kubectl apply -k <kustomization directory>/
```

Run the following command to apply the Deployment object `dev-my-nginx`:

```shell
> kubectl apply -k ./
deployment.apps/dev-my-nginx created
```

Run one of the following commands to view the Deployment object `dev-my-nginx`:

```shell
kubectl get -k ./
```

```shell
kubectl describe -k ./
```

Run the following command to compare the Deployment object `dev-my-nginx` against the state that the cluster would be in if the manifest was applied:

```shell
kubectl diff -k ./
```

Run the following command to delete the Deployment object `dev-my-nginx`:

```shell
> kubectl delete -k ./
deployment.apps "dev-my-nginx" deleted
```

## Kustomize Feature List

| Field | Type | Explanation |
|-------|------|-------------|
| bases | []string | Each entry in this list should resolve to a directory containing a kustomization.yaml file |
| commonAnnotations | map[string]string | annotations to add to all resources |
| commonLabels | map[string]string | labels to add to all resources and selectors |
| configMapGenerator | []ConfigMapArgs | Each entry in this list generates a ConfigMap |
| configurations | []string | Each entry in this list should resolve to a file containing Kustomize transformer configurations |
| crds | []string | Each entry in this list should resolve to an OpenAPI definition file for Kubernetes types |
| generatorOptions | GeneratorOptions | Modify behaviors of all ConfigMap and Secret generator |
| images | []Image | Each entry is to modify the name, tags and/or digest for one image without creating patches |
| labels | map[string]string | Add labels without automatically injecting corresponding selectors |
| namePrefix | string | value of this field is prepended to the names of all resources |
| nameSuffix | string | value of this field is appended to the names of all resources |
| patchesJson6902 | []Patch | Each entry in this list should resolve to a Kubernetes object and a Json Patch |
| patchesStrategicMerge | []string | Each entry in this list should resolve a strategic merge patch of a Kubernetes object |
| replacements | []Replacements | copy the value from a resource's field into any number of specified targets. |
| resources | []string | Each entry in this list must resolve to an existing resource configuration file |
| secretGenerator | []SecretArgs | Each entry in this list generates a Secret |
| vars | []Var | Each entry is to capture text from one resource's field |
```

---

### A3 · `helm-using-helm-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/intro/using_helm/"
fetched_at: "2026-08-31T04:24:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm-release", "helm-release-revision", "helm-rollback-versus-rollout-undo", "helm-install", "helm-upgrade", "helm-rollback", "helm-list", "values-yaml"]
---
# Helm — Using Helm (helm.sh/docs/intro/using_helm/)

## Installing a package, and the release object

Installing a chart creates a new *release* object.

If you want Helm to generate a name for you, leave off the release name and use `--generate-name`.

## Customizing the chart before installing

* `--values` (or `-f`): Specify a YAML file with overrides. This can be specified multiple times and the rightmost file will take precedence
* `--set`: Specify overrides on the command line.

If both are used, `--set` values are merged into `--values` with higher precedence.

## Upgrading a release and recovering on failure

It will only update things that have changed since the last release.

`helm rollback [RELEASE] [REVISION]`

Example:

```
helm rollback happy-panda 1
```

A release version is an incremental revision. Every time an install, upgrade, or rollback happens, the revision number is incremented by 1.

We can use `helm history [RELEASE]` to see revision numbers for a certain release.

## Uninstalling a release

```
helm uninstall happy-panda
```

If you wish to keep a deletion release record, use `helm uninstall --keep-history`.
```

---

### A4 · `helm-rollback-cli-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/helm/helm_rollback/"
fetched_at: "2026-08-31T04:31:00-0400"
authority: "Helm project (CLI reference)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm-rollback", "helm-release", "helm-release-revision", "helm-rollback-versus-rollout-undo"]
---
# helm rollback (helm.sh/docs/helm/helm_rollback/)

roll back a release to a previous revision

## Synopsis

The first argument of the rollback command is the name of a release, and the second is a revision (version) number.

If this argument is omitted or set to 0, it will roll back to the previous release.

```
helm rollback <RELEASE> [REVISION] [flags]
```

## Options (selected)

* `--cleanup-on-fail` — allow deletion of new resources created in this rollback when rollback fails
* `--force-conflicts` — if set server-side apply will force changes against conflicts
* `--force-replace` — force resource updates by replacement
* `--wait` — wait until resources are ready (up to --timeout). Use '--wait' alone for 'watcher' strategy, or specify one of: 'watcher', 'hookOnly', 'legacy'.
* `--dry-run` — simulates the operation without persisting changes. Must be one of: 'none' (default), 'client', or 'server'.
```

---

### A5 · `helm-chart-repository-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/topics/chart_repository/"
fetched_at: "2026-08-31T04:26:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart-repository", "helm-repo-add", "chart-version-versus-appversion"]
---
# Helm — The Chart Repository Guide (helm.sh/docs/topics/chart_repository/)

A chart repository is an HTTP server that houses an `index.yaml` file and optionally some packaged charts.

Because a chart repository can be any HTTP server that can serve YAML and tar files and can answer GET requests, you have a plethora of options when it comes down to hosting your own chart repository.

## The index file

The index file is a yaml file called `index.yaml`. It contains some metadata about the package, including the contents of a chart's `Chart.yaml` file.

Example (excerpt, first entry only):

```
apiVersion: v1
entries:
  alpine:
    - created: 2016-10-06T16:23:20.499814565-06:00
      description: Deploy a basic Alpine Linux pod
      digest: 99c76e403d752c84ead610644d4b1c2f2b453a74b921f422b9dcb8a7c8b559cd
      home: https://helm.sh/helm
      name: alpine
      sources:
      - https://github.com/helm/helm
      urls:
      - https://technosophos.github.io/tscharts/alpine-0.2.0.tgz
      version: 0.2.0
```

A valid chart repository must have an index file.

A repository will not be added if it does not contain a valid `index.yaml`.

## Repository directory layout

```
charts/
  |
  |- index.yaml
  |
  |- alpine-0.1.2.tgz
  |
  |- alpine-0.1.2.tgz.prov
```

## Commands

Charts in a chart repository must be packaged (`helm package chart-name/`).

```
$ helm package docs/examples/alpine/
```

```
$ helm repo index fantastic-charts --url https://fantastic-charts.storage.googleapis.com
```

```
$ helm repo add fantastic-charts https://fantastic-charts.storage.googleapis.com
```

## Hosting

You have options including Google Cloud Storage (GCS) bucket, Amazon S3 bucket, GitHub Pages, or even create your own web server.
```

---

### A6 · `helm-oci-registries-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/topics/registries/"
fetched_at: "2026-08-31T04:26:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["oci-registry-as-chart-store", "chart-repository", "chart-version-versus-appversion"]
---
# Helm — Use OCI-based registries (helm.sh/docs/topics/registries/)

It is recommended to use container registries with OCI support to store and share chart packages.

An OCI-based registry can contain zero or more Helm repositories and each of those repositories can contain zero or more packaged Helm charts.

When using `helm push` to upload a chart an OCI registry, the reference must be prefixed with `oci://` and must not contain the basename or tag.

The basename (chart name) of the registry reference *is* included for any type of action involving chart download (vs. `helm push` where it is omitted).

The registry reference basename is inferred from the chart's name, and the tag is inferred from the chart's semantic version.

## Commands

```
$ helm registry login -u myuser localhost:5000
```

```
$ helm push mychart-0.1.0.tgz oci://localhost:5000/helm-charts
```

```
$ helm pull oci://localhost:5000/helm-charts/mychart --version 0.1.0
```

```
$ helm show all oci://localhost:5000/helm-charts/mychart --version 0.1.0
```

```
$ helm install myrelease oci://localhost:5000/helm-charts/mychart --version 0.1.0
```

```
$ helm registry logout localhost:5000
```
```

---

### A7 · `helm-blog-oci-ga-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/blog/storing-charts-in-oci/"
fetched_at: "2026-08-31T04:28:00-0400"
authority: "Helm project (official project blog)"
objectives_covered: ["D3.1"]
concepts_covered: ["oci-registry-as-chart-store", "chart-repository"]
---
# Helm blog — Storing Helm Charts in OCI Registries (published February 28, 2022)

With the release of Helm 3.8.0, Helm is able to store and work with charts in container registries, as an alternative to Helm repositories.

Since OCI artifacts now makes it possible to store more than container images, you can store charts, images, and other artifacts in a single OCI registry.
```

---

### A8 · `helm-crd-best-practices-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/chart_best_practices/custom_resource_definitions/"
fetched_at: "2026-08-31T04:26:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart-crds-directory", "crd-ordering-problem", "subchart"]
---
# Helm — Custom Resource Definitions (helm.sh/docs/chart_best_practices/custom_resource_definitions/)

There is a declaration of a CRD. This is the YAML file that has the kind `CustomResourceDefinition`. Then there are resources that *use* the CRD.

For a CRD, the declaration must be registered before any resources of that CRDs kind(s) can be used.

## Method 1: Let `helm` Do It For You

There is now a special directory called `crds` that you can create in your chart to hold your CRDs. These CRDs are not templated, but will be installed by default when running a `helm install` for the chart.

If you wish to skip the CRD installation step, you can pass the `--skip-crds` flag.

There is no support at this time for upgrading or deleting CRDs using Helm.

The `--dry-run` flag of `helm install` and `helm upgrade` is not currently supported for CRDs.

## Method 2: Separate Charts

Put the CRD definition in one chart, and then put any resources that use that CRD in *another* chart.

This workflow may be more useful for cluster operators who have admin access to a cluster.
```

---

### A9 · `helm-changes-since-helm2-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/faq/changes_since_helm2/"
fetched_at: "2026-08-31T04:14:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm", "helm-release", "chart-yaml", "oci-registry-as-chart-store", "chart-repository", "helm-install"]
---
# Helm — Changes Since Helm 2 (helm.sh/docs/faq/changes_since_helm2/)

## Removal of Tiller

During the Helm 2 development cycle, we introduced Tiller. Tiller played an important role for teams working on a shared cluster - it made it possible for multiple different operators to interact with the same set of releases.

With role-based access controls (RBAC) enabled by default in Kubernetes 1.6, locking down Tiller for use in a production scenario became more difficult to manage. Due to the vast number of possible security policies, our stance was to provide a permissive default configuration. This allowed first-time users to start experimenting with Helm and Kubernetes without having to dive headfirst into the security controls. Unfortunately, this permissive configuration could grant a user a broad range of permissions they weren't intended to have. DevOps and SREs had to learn additional operational steps when installing Tiller into a multi-tenant cluster.

After hearing how community members were using Helm in certain scenarios, we found that Tiller's release management system did not need to rely upon an in-cluster operator to maintain state or act as a central hub for Helm release information. Instead, we could simply fetch information from the Kubernetes API server, render the Charts client-side, and store a record of the installation in Kubernetes.

Tiller's primary goal could be accomplished without Tiller, so one of the first decisions we made regarding Helm 3 was to completely remove Tiller.

With Tiller gone, the security model for Helm is radically simplified. Helm 3 now supports all the modern security, identity, and authorization features of modern Kubernetes. Helm's permissions are evaluated using your kubeconfig file. Cluster administrators can restrict user permissions at whatever granularity they see fit. Releases are still recorded in-cluster, and the rest of Helm's functionality remains.

## Release storage

In Helm 3, Secrets are now used as the default storage driver.

## Release Names are now scoped to the Namespace

With the removal of Tiller, the information about each release had to go somewhere. In Helm 2, this was stored in the same namespace as Tiller. In practice, this meant that once a name was used by a release, no other release could use that same name, even if it was deployed in a different namespace.

In Helm 3, information about a particular release is now stored in the same namespace as the release itself. This means that users can now `helm install wordpress stable/wordpress` in two separate namespaces, and each can be referred with `helm list` by changing the current namespace context (e.g. `helm list --namespace foo`).

With this greater alignment to native cluster namespaces, the `helm list` command no longer lists all releases by default. Instead, it will list only the releases in the namespace of your current kubernetes context (i.e. the namespace shown when you run `kubectl config view --minify`). It also means you must supply the `--all-namespaces` flag to `helm list` to get behaviour similar to Helm 2.

## Chart.yaml apiVersion bump

With the introduction of library chart support and the consolidation of requirements.yaml into Chart.yaml, clients that understood Helm 2's package format won't understand these new features. So, we bumped the apiVersion in Chart.yaml from `v1` to `v2`.

`helm create` now creates charts using this new format, so the default apiVersion was bumped there as well.

Clients wishing to support both versions of Helm charts should inspect the `apiVersion` field in Chart.yaml to understand how to parse the package format.

## Consolidation of `requirements.yaml` into `Chart.yaml`

The Chart dependency management system moved from requirements.yaml and requirements.lock to Chart.yaml and Chart.lock. We recommend that new charts meant for Helm 3 use the new format. However, Helm 3 still understands Chart API version 1 (`v1`) and will load existing `requirements.yaml` files.

## Pushing Charts to OCI Registries

This is an experimental feature introduced in Helm 3. To use, set the environment variable `HELM_EXPERIMENTAL_OCI=1`.

At a high level, a Chart Repository is a location where Charts can be stored and shared. The Helm client packs and ships Helm Charts to a Chart Repository. Simply put, a Chart Repository is a basic HTTP server that houses an index.yaml file and some packaged charts.

While there are several benefits to the Chart Repository API meeting the most basic storage requirements, a few drawbacks have started to show:

- Chart Repositories have a very hard time abstracting most of the security implementations required in a production environment. Having a standard API for authentication and authorization is very important in production scenarios.
- Helm's Chart provenance tools used for signing and verifying the integrity and origin of a chart are an optional piece of the Chart publishing process.
- In multi-tenant scenarios, the same Chart can be uploaded by another tenant, costing twice the storage cost to store the same content. Smarter chart repositories have been designed to handle this, but it's not a part of the formal specification.
- Using a single index file for search, metadata information, and fetching Charts has made it difficult or clunky to design around in secure multi-tenant implementations.

Docker's Distribution project (also known as Docker Registry v2) is the successor to the Docker Registry project. Many major cloud vendors have a product offering of the Distribution project, and with so many vendors offering the same product, the Distribution project has benefited from many years of hardening, security best practices, and battle-testing.

## Name (or --generate-name) is now required on install

In Helm 2, if no name was provided, an auto-generated name would be given. In production, this proved to be more of a nuisance than a helpful feature. In Helm 3, Helm will throw an error if no name is provided with `helm install`.

For those who still wish to have a name auto-generated for you, you can use the `--generate-name` flag to create one for you.
```

---

### A10 · `helm-storage-backends-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/topics/advanced/"
fetched_at: "2026-08-31T04:22:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm-release", "helm-release-revision"]
---
# Helm — Advanced Helm Techniques: Storage backends (helm.sh/docs/topics/advanced/)

By default, release information is stored in Secrets in the namespace of the release.

The `HELM_DRIVER` environment variable selects the backend. It accepts the values `[configmap, secret, sql]`.

To use the ConfigMap backend:

```
export HELM_DRIVER=configmap
```

To use the SQL backend (beta), which stores release information in a SQL database — useful when release data exceeds the 1MB limit imposed by Kubernetes/etcd:

```
export HELM_DRIVER=sql
export HELM_DRIVER_SQL_CONNECTION_STRING=postgresql://helm-postgres:5432/helm?user=helm&password=changeme
```

Only PostgreSQL is supported for the SQL backend.
```

---

### A11 · `helm-named-templates-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/chart_template_guide/named_templates/"
fetched_at: "2026-08-31T04:33:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart-helpers", "go-template-in-helm", "chart-templates-directory"]
---
# Helm — Named Templates (helm.sh/docs/chart_template_guide/named_templates/)

But files whose name begins with an underscore (`_`) are assumed to *not* have a manifest inside. These files are not rendered to Kubernetes object definitions, but are available everywhere within other chart templates for use.

In fact, when we first created `mychart`, we saw a file called `_helpers.tpl`. That file is the default location for template partials.

The `define` action allows us to create a named template inside of a template file.

To work around this case, Helm provides an alternative to `template` that will import the contents of a template into the present pipeline where it can be passed along to other functions in the pipeline.
```

---

### A12 · `helm-architecture-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/topics/architecture/"
fetched_at: "2026-08-31T04:29:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm", "chart", "chart-repository", "helm-release"]
---
# Helm — Architecture (helm.sh/docs/topics/architecture/)

Helm is the package manager for Kubernetes.

Three components describe how Helm works: charts, repositories, and releases.

A release is an instance of a chart running in a Kubernetes cluster.

The Helm client handles local chart development, manages repositories, manages releases, and sends charts to the Helm library to be installed, upgraded, or uninstalled.
```

---

### A13 · `helm-glossary-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/docs/glossary/"
fetched_at: "2026-08-31T04:29:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["chart", "chart-yaml", "helm-release", "helm-release-revision", "chart-repository", "chart-version-versus-appversion"]
---
# Helm — Glossary (helm.sh/docs/glossary/)

**Chart** — A Helm package that contains information sufficient for installing a set of Kubernetes resources into a Kubernetes cluster.

**Chart Archive** — A *chart archive* is a tarred and gzipped (and optionally signed) chart.

**Chart Version** — Charts are versioned according to the SemVer 2 spec. A version number is required on every chart.

**Chart.yaml** — Information about a chart is stored in a special file called `Chart.yaml`. Every chart must have this file.

**Kube Config (KUBECONFIG)** — The Helm client learns about Kubernetes clusters by using files in the *Kube config* file format. By default, Helm attempts to find this file in the place where `kubectl` creates it (`$HOME/.kube/config`).

**Lint (Linting)** — To *lint* a chart is to validate that it follows the conventions and requirements of the Helm chart standard.

**Release** — When a chart is installed, the Helm library creates a *release* to track that installation.

**Release Number (Release Version)** — A sequential counter is used to track releases as they change.

**Repository (Repo, Chart Repository)** — Helm charts may be stored on dedicated HTTP servers called *chart repositories* (*repositories*, or just *repos*).
```

---

### A14 · `helm-homepage-2026-08-31.md` (new)
```markdown
---
source_url: "https://helm.sh/"
fetched_at: "2026-08-31T04:29:00-0400"
authority: "Helm project (CNCF graduated project)"
objectives_covered: ["D3.1"]
concepts_covered: ["helm", "chart"]
---
# Helm — project homepage (helm.sh)

The package manager for Kubernetes

Helm is the best way to find, share, and use software built for Kubernetes.

Helm helps you manage Kubernetes applications — Helm Charts help you define, install, and upgrade even the most complex Kubernetes application.

Charts are easy to create, version, share, and publish — so start using Helm and stop the copy-and-paste.
```

---

### A15 · `kubectl-book-kustomization-fields-2026-08-31.md` (new)
```markdown
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

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
- {pathOrUrl}
- ...

generators:
- {pathOrUrl}
- ...

transformers:
- {pathOrUrl}
- ...

validators:
- {pathOrUrl}
- ...
```
```

---

### A16 · `lf-lfs250-course-outline-2026-08-31.md` (new)
```markdown
---
source_url: "https://training.linuxfoundation.org/training/kubernetes-and-cloud-native-essentials-lfs250/"
fetched_at: "2026-08-31T04:22:00-0400"
authority: "The Linux Foundation (exam and training authority for KCNA)"
objectives_covered: ["D3"]
concepts_covered: []
---
# Linux Foundation — Kubernetes and Cloud Native Essentials (LFS250)

Kubernetes and Cloud Native Essentials (LFS250)

The course, along with real-world experience and study, will provide the skills and knowledge also tested by the Linux Foundation's Kubernetes and Cloud Native Associate (KCNA) exam.

Bundle option listed on the page: "Course + Kubernetes and Cloud Native Associate (KCNA) certification exam – $299"

## Published course outline

- Chapter 1. Course Introduction
- Chapter 2. Cloud Native Architecture
- Chapter 3. Container Orchestration
- Chapter 4. Kubernetes Fundamentals
- Chapter 5. Working with Kubernetes
- Chapter 6. Cloud Native Application Delivery
- Chapter 7. Cloud Native Observability

## NEGATIVE EVIDENCE (the reason this snapshot exists)

No sentence on this public course page names Helm or Kustomize. The published outline resolves
only to the chapter title "Cloud Native Application Delivery"; no sub-topic list is published.
This snapshot is the evidence base for Chapter 14's mandatory honesty beat, and it establishes
what may NOT be claimed: the chapter may not attribute its Helm/Kustomize topic list to a named
LFS250 module on those tools.
```
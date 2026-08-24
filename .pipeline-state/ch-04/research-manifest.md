Found the contract: Stage 2's stdout *is* `research-manifest.md`, and the orchestrator harvests embedded fenced blocks into `sources/`. Note `harvest_research_snapshots` uses a non-greedy body match, so nested ``` fences would truncate a snapshot — matching the existing snapshots' convention of avoiding them. Emitting the artifact:

# Research Manifest — KCNA Chapter 4

**Chapter:** 4 — Records of Intent
**Exam:** KCNA (CNCF / Linux Foundation), curriculum effective 2025-11-24
**Objective covered:** D1.1 (Kubernetes Fundamentals / Kubernetes Core Concepts)
**Stage 2 run:** 2026-08-24
**Outcome:** all three source gaps the outline flagged (Open questions #1, #2, #3) are **resolved** with first-party sources. No section needs to be narrowed for want of a source.

---

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-object-management-2026-08-24.md` | Kubernetes project (kubernetes.io/docs) | D1 Core Concepts, D1.1 | imperative-command, imperative-object-configuration, declarative-object-configuration, declarative-configuration, kubectl-apply, kubectl-create, manifest |
| `k8s-docs-annotations-2026-08-24.md` | Kubernetes project (kubernetes.io/docs) | D1 Core Concepts, D1.1 | annotation, label, metadata, non-identifying-metadata |
| `k8s-docs-names-and-uids-2026-08-24.md` | Kubernetes project (kubernetes.io/docs) | D1 Core Concepts, D1.1 | object-name, object-uid, metadata, namespace, namespace-dns-form |
| `k8s-api-ref-secret-v1-2026-08-24.md` | Kubernetes API reference (kubernetes.io/docs) | D1 Core Concepts, D1.1, D2 Security | secret, secret-types, secret-storage-default, opaque-secret |
| `k8s-docs-secret-config-file-2026-08-24.md` | Kubernetes project (kubernetes.io/docs) | D1 Core Concepts, D1.1, D2 Security | secret, secret-storage-default, manifest |
| `k8s-docs-secrets-good-practices-2026-08-24.md` | Kubernetes project (kubernetes.io/docs) | D2 Security, D1 Core Concepts, D1.1 | secret, secret-storage-default, secret-hardening, encryption-at-rest, least-privilege |

## Snapshots already cached that this chapter draws on (verified present and on-topic)

| Snapshot | Authority | Sections served |
|---|---|---|
| `k8s-docs-objects-2026-08-23.md` | Kubernetes project | §1, §2, §6 — persistent entities, "record of intent", spec/status asymmetry, the Deployment three-replica example, the four required fields, manifests-YAML-by-convention, `kubectl apply -f` |
| `k8s-docs-controllers-2026-08-23.md` | Kubernetes project | §2, §6 — control loop, desired vs current state, control via API server |
| `k8s-docs-namespaces-2026-08-23.md` | Kubernetes project | §3 — complete: isolation, uniqueness within-not-across, when-to-use guidance, no nesting, one namespace per resource, labels-not-namespaces warning, all four initial namespaces, DNS form, not-all-objects-are-namespaced, `kubectl api-resources --namespaced` |
| `k8s-docs-configmap-2026-08-23.md` | Kubernetes project | §4 — complete: definition, no-secrecy caution, DATABASE_HOST motivation, 1 MiB limit, same-namespace requirement, four consumption paths with the kubelet-at-launch vs subscribe split, immutability since v1.19 |
| `k8s-docs-secret-2026-08-23.md` | Kubernetes project | §4 — definition, ConfigMap contrast, the storage Caution incl. the create-a-Pod-reads-any-Secret consequence, four hardening steps, uses, eight built-in types |
| `k8s-docs-labels-selectors-2026-08-23.md` | Kubernetes project | §5 — complete: definition and the no-semantics-to-the-core-system clause, example labels, syntax/character set, both selector types, ANDed requirements, newer-resources bridge, `matchLabels` ≡ `matchExpressions`+`In` |
| `k8s-docs-kubectl-overview-2026-08-23.md` | Kubernetes project | §1, §2 — `apply`, `get`, `create`, `explain` verb definitions at the altitude Ch 4 needs |
| `twelve-factor-app-2026-08-23.md` | The Twelve-Factor App | §4 forward bearing only — factor III, "Store config in the environment" |
| `cncf-kcna-curriculum-pdf-2026-08-23.md` | CNCF (cncf/curriculum) | Front matter / weighting — the four domain weights (44/28/16/12) |
| `lf-lfs250-course-outline-2026-08-23.md` | The Linux Foundation | Weighting cross-check — seven module titles only |

---

## Gaps

**No source gap blocks drafting.** The three the outline flagged are closed:

- **Open question #1 (BLOCKING for §1) — RESOLVED.** The object-management taxonomy page was indeed absent from the cached set; B2's "cached coverage sufficient" routing was wrong on exactly the point the outline identified. It is now captured in `k8s-docs-object-management-2026-08-24.md`: the three techniques, the comparison table (Operates on / Recommended environment / Supported writers / Learning curve), per-technique trade-offs, and the "should be managed using only one technique… results in undefined behavior" warning the §1 `🔭 Closer Look` was gated on. §1 does **not** need to narrow; the Closer Look is cleared to draft.
- **Open question #2 (BLOCKING for the §4 Fixed Point) — RESOLVED, and better than the outline hoped.** The `data`-field base64 mechanism is in the API reference and the config-file task page. More importantly, the claim B1's glossary asserted — that base64 is not encryption — is stated *explicitly by the Kubernetes project itself*: "Base64 encoding is *not* an encryption method, it provides no additional confidentiality over plain text." The §4 Fixed Point may carry the base64 clause on a first-party citation and does not have to rest on B1's glossary.
- **Open question #3 (non-blocking, §5) — RESOLVED.** `k8s-docs-annotations-2026-08-24.md` carries the full page: the explicit labels-select / annotations-do-not contrast, the eight-item list of what belongs in an annotation, syntax rules, the 256 KiB total-size ceiling, and a worked manifest. §5 can teach annotations with conventional-use examples rather than only as the contrast to labels.

**Genuine gaps that remain — none Stage-2-fixable. Drafting must not invent facts to fill them.**

| Gap | What is missing | Consequence for drafting |
|---|---|---|
| **G-A: per-chapter exam weight** | CNCF publishes four domain weights (44/28/16/12) and **no sub-competency weights**. Verified against `cncf-kcna-curriculum-pdf-2026-08-23.md`, which lists competency *names* under each domain but no percentages. | The outline's `domain_weight_pct: 6` is authored judgment, as its Open question #7 states. Front matter carries the disclosure. The draft must not present 6% as a CNCF figure. |
| **G-B: LFS250 sub-topic weighting (arc-outline G37)** | The cached LFS250 page gives seven module titles and no hour counts, lesson lists, or weightings. The Linux Foundation publishes no finer syllabus on the public course page. | G37 stays open; it cannot refine D1's internal weighting. Outline Open question #8 is unchanged — the section plan and its ordering are dependency-driven and would not move even if G37 landed. |
| **G-C: numeric size limit for a Secret** | The API reference states the limit symbolically — "The total bytes of the values in the Data field must be less than MaxSecretSize bytes" — with no byte value. The concept page's numeric statement was not reachable (see Note 1). | **Do not write "a Secret is limited to 1 MiB" into the draft.** The 1 MiB figure in the outline belongs to **ConfigMap**, where it is fully sourced. If §4 wants a Secret ceiling, use the symbolic phrasing or omit it. This is the single most likely place for a plausible-sounding invented fact to enter this chapter. |
| **G-D: `kubectl get` selector invocation** | The cached labels snapshot gives both selector *syntaxes* but not the `kubectl get pods -l …` command form. | Minor. §5 lists `kubectl-get` under concepts, but the outline's own scope boundary hands the kubectl command surface to Ch 8. Teach the selector syntax, not the invocation. Not a gap against the exam objective. |

---

## Notes for the author

**1. The Secret concept page truncates on fetch, and that shaped this run.** `kubernetes.io/docs/concepts/configuration/secret/` is long enough that retrieval cuts off partway through "ServiceAccount token Secrets" — before "Information security for Secrets" and before the size-limit and immutability sections. The existing `k8s-docs-secret-2026-08-23.md` is abridged for exactly this reason; the abridgement is *upstream of the tooling*, not an authoring choice. Everything Chapter 4 needs beyond that cut has been sourced from three other first-party pages. If a later stage needs the tail of that page (Ch 12 will), fetch the good-practices page and the API reference rather than re-trying the concept page.

**2. Cite the right page for the right half of the base64 claim.** Three distinct statements; only one is the interesting one:
   - *Mechanism* — Secret `data` holds base64-encoded strings → API reference, or the config-file task page.
   - *Security property* — base64 is not encryption and adds no confidentiality → **good-practices page only.** This is the sentence the §4 Fixed Point and trap #16 want.
   - *Storage default* — stored unencrypted in etcd; readable by anyone with API access, etcd access, or Pod-creation rights in the namespace → the cached concept-page snapshot.

   The outline's instinct was right that the unencrypted-storage claim "lands harder." Both are now available; the recommendation stands that unencrypted-in-etcd carries the weight and base64 is the supporting clause.

**3. The good-practices snapshot is mostly Chapter 12's, and §4 must not spend it.** It was fetched for one sentence. It also contains full RBAC-on-Secrets guidance, etcd shredding, TLS between etcd instances, the Secrets Store CSI Driver, and the do-not-commit-manifests warning — all the Ch 12 material the outline draws a hard boundary around. The snapshot being on disk is not permission to teach from it. §4's budget is unchanged: state the default, name the four steps, hand them forward.

**4. The object-management page sharpens §1's precision guard, in the chapter's favour.** The outline warns that "you never give Kubernetes orders" overclaims. The newly fetched page supplies the framing that fixes it: Kubernetes documents imperative commands as a *first-class, recommended* technique — "This is the recommended way to get started or to run a one-off task in a cluster" — with a documented cost, "it provides no history of previous configurations." That is a more honest §1 than a bare declarative-good/imperative-bad contrast, and it sets up §6's narrow claim without §6 having to climb out of a hole. The "undefined behavior" warning about mixing techniques on one object is also a strong, quotable, exam-flavoured fact.

**5. Annotations came back richer than the outline planned for.** The outline budgeted annotations as "purely the contrast to labels" on the assumption of one cached clause. The full page adds the 256 KiB total-size ceiling and the point that annotation values have *no* character-set restrictions where label values are capped at 63 characters. That contrast — selectable-and-constrained versus unselectable-and-unconstrained — is a sharper version of §5's one-sentence rule and is worth a line. Watch density: §5 already carries a Fixed Point, a Navigational Hazards block, and a Worth Securing marker.

**6. Names and UIDs was fetched unrequested; use it sparingly.** §2 teaches `metadata` as name, UID, optional namespace, which the objects snapshot supports in a single clause. The names page lets that clause be accurate rather than approximate — in particular: names are unique per resource type *within a namespace* (the docs' own example is one Pod and one Deployment both named `myapp-1234`), and a UID is unique across the whole cluster *and across time* ("Every object created over the whole lifetime of a Kubernetes cluster has a distinct UID"). That time dimension is the non-obvious half and the reason UID exists at all. The three DNS name standards (RFC 1123 subdomain / RFC 1123 label / RFC 1035 label) are **below associate tier** — the outline's "do not teach `metadata` exhaustively" guard applies to them.

**7. No source conflicts were found.** All six new snapshots are from kubernetes.io and agree with the cached set and with each other. The one apparent tension — good-practices saying Secret values "are encoded as base64 strings and are stored unencrypted by default" versus the concept page's Caution saying "stored unencrypted in the API server's underlying data store (etcd)" — is not a conflict. The first describes the serialization form, the second the storage property. Both are true and the chapter needs both.

**8. Version currency.** All pages fetched 2026-08-24 against current docs. The version-pinned facts Chapter 4 uses are immutable ConfigMaps "starting from v1.19" and the ServiceAccount-token shift "in Kubernetes v1.22 and later". Both come from the cached 2026-08-23 snapshots and both are stable historical statements, not moving targets. No re-verification needed before drafting.

**9. Exam-authority precedence was not tested this run.** The priority rule (exam authority over vendor docs on conflict) had nothing to arbitrate: the CNCF curriculum names D1's competencies but makes no technical claims about objects, namespaces, labels, ConfigMaps, or Secrets. On every fact in this chapter, kubernetes.io is both the vendor and the only authority speaking.

**10. Snapshot formatting.** Code examples in the embedded snapshots below use 4-space indented blocks rather than fenced blocks, matching the convention of the existing 87 snapshots. This is load-bearing: `harvest_research_snapshots` matches snapshot bodies non-greedily, so a nested fence would truncate the harvested file at that point.

---

## Embedded snapshots

### A1 · `k8s-docs-object-management-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/overview/working-with-objects/object-management/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["imperative-command", "imperative-object-configuration", "declarative-object-configuration", "declarative-configuration", "kubectl-apply", "kubectl-create", "manifest"]
---
# Kubernetes Object Management (kubernetes.io/docs/concepts/overview/working-with-objects/object-management/)

The `kubectl` command-line tool supports several different ways to create and manage Kubernetes objects.

**Warning:** A Kubernetes object should be managed using only one technique. Mixing and matching techniques for the same object results in undefined behavior.

## Management techniques

| Management technique | Operates on | Recommended environment | Supported writers | Learning curve |
|---|---|---|---|---|
| Imperative commands | Live objects | Development projects | 1+ | Lowest |
| Imperative object configuration | Individual files | Production projects | 1 | Moderate |
| Declarative object configuration | Directories of files | Production projects | 1+ | Highest |

## Imperative commands

When using imperative commands, a user operates directly on live objects in a cluster. The user provides operations to the `kubectl` command as arguments or flags.

This is the recommended way to get started or to run a one-off task in a cluster. Because this technique operates directly on live objects, it provides no history of previous configurations.

### Examples

Run an instance of the nginx container by creating a Deployment object:

    kubectl create deployment nginx --image nginx

### Trade-offs

Advantages compared to object configuration:

- Commands are expressed as a single action word.
- Commands require only a single step to make changes to the cluster.

Disadvantages compared to object configuration:

- Commands do not integrate with change review processes.
- Commands do not provide an audit trail associated with changes.
- Commands do not provide a source of records except for what is live.
- Commands do not provide a template for creating new objects.

## Imperative object configuration

In imperative object configuration, the kubectl command specifies the operation (create, replace, etc.), optional flags and at least one file name. The file specified must contain a full definition of the object in YAML or JSON format.

**Warning:** The imperative `replace` command replaces the existing spec with the newly provided one, dropping all changes to the object missing from the configuration file. This approach should not be used with resource types whose specs are updated independently of the configuration file. Services of type `LoadBalancer`, for example, have their `externalIPs` field updated independently from the configuration by the cluster.

### Examples

Create the objects defined in a configuration file:

    kubectl create -f nginx.yaml

Delete the objects defined in two configuration files:

    kubectl delete -f nginx.yaml -f redis.yaml

Update the objects defined in a configuration file by overwriting the live configuration:

    kubectl replace -f nginx.yaml

### Trade-offs

Advantages compared to imperative commands:

- Object configuration can be stored in a source control system such as Git.
- Object configuration can integrate with processes such as reviewing changes before push and audit trails.
- Object configuration provides a template for creating new objects.

Disadvantages compared to imperative commands:

- Object configuration requires basic understanding of the object schema.
- Object configuration requires the additional step of writing a YAML file.

Advantages compared to declarative object configuration:

- Imperative object configuration behavior is simpler and easier to understand.
- As of Kubernetes version 1.5, imperative object configuration is more mature.

Disadvantages compared to declarative object configuration:

- Imperative object configuration works best on files, not directories.
- Updates to live objects must be reflected in configuration files, or they will be lost during the next replacement.

## Declarative object configuration

When using declarative object configuration, a user operates on object configuration files stored locally, however the user does not define the operations to be taken on the files. Create, update, and delete operations are automatically detected per-object by `kubectl`. This enables working on directories, where different operations might be needed for different objects.

**Note:** Declarative object configuration retains changes made by other writers, even if the changes are not merged back to the object configuration file. This is possible by using the `patch` API operation to write only observed differences, instead of using the `replace` API operation to replace the entire object configuration.

### Examples

Process all object configuration files in the `configs` directory, and create or patch the live objects. You can first `diff` to see what changes are going to be made, and then apply:

    kubectl diff -f configs/
    kubectl apply -f configs/

Recursively process directories:

    kubectl diff -R -f configs/
    kubectl apply -R -f configs/

### Trade-offs

Advantages compared to imperative object configuration:

- Changes made directly to live objects are retained, even if they are not merged back into the configuration files.
- Declarative object configuration has better support for operating on directories and automatically detecting operation types (create, patch, delete) per-object.

Disadvantages compared to imperative object configuration:

- Declarative object configuration is harder to debug and understand results when they are unexpected.
- Partial updates using diffs create complex merge and patch operations.
```

### A2 · `k8s-docs-annotations-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["annotation", "label", "metadata", "non-identifying-metadata"]
---
# Annotations (kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

You can use Kubernetes annotations to attach arbitrary non-identifying metadata to objects. Clients such as tools and libraries can retrieve this metadata.

## Attaching metadata to objects

You can use either labels or annotations to attach metadata to Kubernetes objects. Labels can be used to select objects and to find collections of objects that satisfy certain conditions. In contrast, annotations are not used to identify and select objects. The metadata in an annotation can be small or large, structured or unstructured, and can include characters not permitted by labels. It is possible to use labels as well as annotations in the metadata of the same object.

Annotations, like labels, are key/value maps:

    "metadata": {
      "annotations": {
        "key1" : "value1",
        "key2" : "value2"
      }
    }

**Note:** The keys and the values in the map must be strings. In other words, you cannot use numeric, boolean, list or other types for either the keys or the values.

Here are some examples of information that could be recorded in annotations:

- Fields managed by a declarative configuration layer. Attaching these fields as annotations distinguishes them from default values set by clients or servers, and from auto-generated fields and fields set by auto-sizing or auto-scaling systems.
- Build, release, or image information like timestamps, release IDs, git branch, PR numbers, image hashes, and registry address.
- Pointers to logging, monitoring, analytics, or audit repositories.
- Client library or tool information that can be used for debugging purposes: for example, name, version, and build information.
- User or tool/system provenance information, such as URLs of related objects from other ecosystem components.
- Lightweight rollout tool metadata: for example, config or checkpoints.
- Phone or pager numbers of persons responsible, or directory entries that specify where that information can be found, such as a team web site.
- Directives from the end-user to the implementations to modify behavior or engage non-standard features.

## Syntax and character set

*Annotations* are key/value pairs. Valid annotation keys have two segments: an optional prefix and name, separated by a slash (`/`). The name segment is required and must be 63 characters or less, beginning and ending with an alphanumeric character (`[a-z0-9A-Z]`) with dashes (`-`), underscores (`_`), dots (`.`), and alphanumerics between. The prefix is optional. If specified, the prefix must be a DNS subdomain: a series of DNS labels separated by dots (`.`), not longer than 253 characters in total, followed by a slash (`/`).

If the prefix is omitted, the annotation Key is presumed to be private to the user. Automated system components (e.g. `kube-scheduler`, `kube-controller-manager`, `kube-apiserver`, `kubectl`, or other third-party automation) which add annotations to end-user objects must specify a prefix.

The `kubernetes.io/` and `k8s.io/` prefixes are reserved for Kubernetes core components.

Valid annotation values have no character set restrictions — unlike label values, annotation values may contain any string, including special characters, whitespace, and structured data such as JSON or YAML. If you plan to store binary data (such as CBOR), the Kubernetes project recommends that you base64 encode it. However, the total size of **all** annotations on a single object (keys and values combined) must not exceed 256 KiB.

For example, here's a manifest for a Pod that has the annotation `imageregistry: https://hub.docker.com/`:

    apiVersion: v1
    kind: Pod
    metadata:
      name: annotations-demo
      annotations:
        imageregistry: "https://hub.docker.com/"
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

### A3 · `k8s-docs-names-and-uids-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/overview/working-with-objects/names/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D1 Core Concepts", "D1.1"]
concepts_covered: ["object-name", "object-uid", "metadata", "namespace", "namespace-dns-form"]
---
# Object Names and IDs (kubernetes.io/docs/concepts/overview/working-with-objects/names/)

Each object in your cluster has a Name that is unique for that type of resource. Every Kubernetes object also has a UID that is unique across your whole cluster.

For example, you can only have one Pod named `myapp-1234` within the same namespace, but you can have one Pod and one Deployment that are each named `myapp-1234`.

For non-unique user-provided attributes, Kubernetes provides labels and annotations.

## Names

A client-provided string that refers to an object in a resource URL, such as `/api/v1/pods/some-name`.

Only one object of a given kind can have a given name at a time. However, if you delete the object, you can make a new object with the same name.

Names must be unique across all API versions of the same resource. API resources are distinguished by their API group, resource type, namespace (for namespaced resources), and name.

### DNS Subdomain Names

Most resource types require a name that can be used as a DNS subdomain name as defined in RFC 1123. This means the name must:

- contain no more than 253 characters
- contain only lowercase alphanumeric characters, '-' or '.'
- start with an alphanumeric character
- end with an alphanumeric character

### RFC 1123 Label Names

Some resource types require their names to follow the DNS label standard as defined in RFC 1123. This means the name must:

- contain at most 63 characters
- contain only lowercase alphanumeric characters or '-'
- start with an alphanumeric character
- end with an alphanumeric character

### RFC 1035 Label Names

Some resource types require their names to follow the DNS label standard as defined in RFC 1035. This means the name must:

- contain at most 63 characters
- contain only lowercase alphanumeric characters or '-'
- start with an alphabetic character
- end with an alphanumeric character

### Example

Here's an example manifest for a Pod named `nginx-demo`:

    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx-demo
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

## UIDs

A Kubernetes systems-generated string to uniquely identify objects.

Every object created over the whole lifetime of a Kubernetes cluster has a distinct UID. It is intended to distinguish between historical occurrences of similar entities.

Kubernetes UIDs are universally unique identifiers (also known as UUIDs). UUIDs are standardized as ISO/IEC 9834-8 and as ITU-T X.667.
```

### A4 · `k8s-api-ref-secret-v1-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/secret-v1/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs, Kubernetes API reference) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D1 Core Concepts", "D1.1", "D2 Security"]
concepts_covered: ["secret", "secret-types", "secret-storage-default", "opaque-secret"]
---
# Secret v1 — Kubernetes API reference (kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/secret-v1/)

## Resource description

"Secret holds secret data of a certain type. The total bytes of the values in the Data field must be less than MaxSecretSize bytes."

## Fields

### `data` (map[string][]byte)

"Data contains the secret data. Each key must consist of alphanumeric characters, '-', '_' or '.'. The serialized form of the secret data is a base64 encoded string, representing the arbitrary (possibly non-string) data value here. Described in https://tools.ietf.org/html/rfc4648#section-4"

### `stringData` (map[string]string)

"stringData allows specifying non-binary secret data in string form. It is provided as a write-only input field for convenience. All keys and values are merged into the data field on write, overwriting any existing values. The stringData field is never output when reading from the API."

### `immutable` (boolean)

"Immutable, if set to true, ensures that data stored in the Secret cannot be updated (only object metadata can be modified). If not set to true, the field can be modified at any time. Defaulted to nil."

### `type` (string)

"Used to facilitate programmatic handling of secret data. More info: https://kubernetes.io/docs/concepts/configuration/secret/#secret-types"

---

**Snapshot note (not source text):** the resource description states the limit as the symbolic constant `MaxSecretSize`; this reference page does not give a numeric byte value. See research manifest gap G-C.
```

### A5 · `k8s-docs-secret-config-file-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D1 Core Concepts", "D1.1", "D2 Security"]
concepts_covered: ["secret", "secret-storage-default", "manifest"]
---
# Managing Secrets using Configuration File (kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/)

## Create the Secret

"The `data` field is used to store arbitrary data, encoded using base64. The `stringData` field is provided for convenience, and it allows you to provide the same data as unencoded strings."

"The serialized JSON and YAML values of Secret data are encoded as base64 strings. Newlines are not valid within these strings and must be omitted."

## Specify unencoded data when creating a Secret

"This field allows you to put a non-base64 encoded string directly into the Secret, and the string will be encoded for you when the Secret is created or updated."

"When you retrieve the Secret data, the command returns the encoded values, and not the plaintext values you provided in `stringData`."

---

**Snapshot note (not source text):** this page documents *that* Secret `data` is base64-encoded. It does **not** contain the claim that base64 is not encryption. For that claim, cite `k8s-docs-secrets-good-practices-2026-08-24.md`.
```

### A6 · `k8s-docs-secrets-good-practices-2026-08-24.md` (new)

```markdown
---
source_url: "https://kubernetes.io/docs/concepts/security/secrets-good-practices/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D1 Core Concepts", "D1.1"]
concepts_covered: ["secret", "secret-storage-default", "secret-hardening", "encryption-at-rest", "least-privilege"]
---
# Good practices for Kubernetes Secrets (kubernetes.io/docs/concepts/security/secrets-good-practices/)

## Opening

"In Kubernetes, a Secret is an object that stores sensitive information, such as passwords, OAuth tokens, and SSH keys. Secrets give you more control over how sensitive information is used and reduces the risk of accidental exposure. Secret values are encoded as base64 strings and are stored unencrypted by default, but can be configured to be encrypted at rest."

## Base64 encoding

"Base64 encoding is *not* an encryption method, it provides no additional confidentiality over plain text."

## Cluster administrators

### Configure encryption at rest

"By default, Secret objects are stored unencrypted in etcd. You should configure encryption of your Secret data in `etcd`. For instructions, refer to Encrypt Secret Data at Rest."

### Configure least-privilege access to Secrets

"When planning your access control mechanism, such as Kubernetes Role-based Access Control (RBAC), consider the following guidelines for access to `Secret` objects."

- "**Components**: Restrict `watch` or `list` access to only the most privileged, system-level components. Only grant `get` access for Secrets if the component's normal behavior requires it."
- "**Humans**: Restrict `get`, `watch`, or `list` access to Secrets. Only allow cluster administrators to access `etcd`. This includes read-only access."

### Improve etcd management policies

"Consider wiping or shredding the durable storage used by `etcd` once it is no longer in use. If there are multiple `etcd` instances, configure encrypted SSL/TLS communication between the instances to protect the Secret data in transit."

### Configure access to external Secrets

"You can use third-party Secrets store providers to keep your confidential data outside your cluster and then configure Pods to access that information. The Kubernetes Secrets Store CSI Driver is a DaemonSet that lets the kubelet retrieve Secrets from external stores, and mount the Secrets as a volume into specific Pods that you authorize to access the data."

## Developers

### Restrict Secret access to specific containers

"If you are defining multiple containers in a Pod, and only one of those containers needs access to a Secret, define the volume mount or environment variable configuration so that the other containers do not have access to that Secret."

### Protect Secret data after reading

"Applications still need to protect the value of confidential information after reading it from an environment variable or volume. For example, your application must avoid logging the secret data in the clear or transmitting it to an untrusted party."

### Avoid sharing Secret manifests

"If you configure a Secret through a manifest, with the secret data encoded as base64, sharing this file or checking it in to a source repository means the secret is available to everyone who can read the manifest."
```
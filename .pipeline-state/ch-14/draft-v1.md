# Chapter 14: Packing for the Voyage

## *"A chart is not a release, and templates are not the point"*

**Domain: Cloud Native Application Delivery — Application Delivery | Domain Weight: 16% [source: lf-kcna-exam-page-2026-08-23]**
**Complexity: Mixed | Novelty: Moderate | Prerequisites: Standard**

> The 16% figure is the published weight for the whole Cloud Native Application Delivery domain, which this book divides across Chapters 14, 15, and 16. That division is an authored allocation, not a published one. CNCF publishes the domain weight and the competency names, and nothing finer.

---

## Attention Budget

**Total time: ~85 minutes | Recommended: Single session, or split after §4**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 Why a Folder of YAML Stops Working | 10 min | Low | Anytime |
| §2 What a Chart Contains | 15 min | Medium | Mid-session |
| §3 Chart, Release, Revision | 18 min | High | Peak attention |
| §4 Where Charts Come From | 8 min | Low | Anytime |
| ☆ Taking Your Bearings (1) | 6 min | Medium | After a brief break |
| §5 Patching Instead of Templating | 14 min | Medium | Mid-session |
| §6 Which One, When | 10 min | Medium | Mid-session |
| ☆ Taking Your Bearings (2) | 6 min | Medium | After a brief break |
| §7 A Package, Not a Template | 5 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*If you only have 15 minutes: read §3. It is the chapter, and the other six sections are its supporting cast.*

---

> *"Charts are easy to create, version, share, and publish — so start using Helm and stop the copy-and-paste."*
> — The Helm project [source: helm-homepage-2026-08-31]

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score tells you how to read what follows; there is no bad score here, only different reading strategies. Every question is answerable from Chapters 1 through 13 or from professional experience you already have.

1. You run `kubectl apply -f manifests/` against a directory holding twelve YAML files. What does that command do, and what does it promise you about the order in which those twelve files are applied?

2. You have a cluster with no metrics-server, and `kubectl top nodes` is failing. In a declarative system, what does "install metrics-server" actually consist of?

3. You run `kubectl rollout undo deployment/api`. What changes in the cluster, and what happens to the Deployment's revision history?

4. You apply a manifest whose `kind` is `PostgresCluster`. The API server rejects it because it does not recognize that kind. What has to happen first, and who is responsible for making it happen?

5. Your application needs a different database hostname in staging than in production. Where does that hostname belong, and why is baking it into the container image the wrong answer?

6. What is the difference between an image tag and an image digest, and what, precisely, is a registry?

7. From your own professional experience with any package manager at all (apt, npm, pip, NuGet, Homebrew, whatever you have used), what does a package manager give you that a folder of files does not?

8. Two clusters need to run the same application. One needs three replicas and the hostname `app.staging.example.com`; the other needs twelve replicas and `app.example.com`. Using only the tools this book has taught you so far, what are your options, and what is wrong with each of them?

<details>
<summary>Answers + reading strategy</summary>

**1.** It applies every manifest in the directory, creating what does not exist and updating what does *[cross-bearing: see Ch 4 §1 — declarative object configuration and kubectl apply]*. It promises nothing about ordering. The files go in; the API server accepts them; whether object A exists before object B is not something the command undertakes to arrange.

**2.** It consists of applying a set of Kubernetes objects that somebody else wrote: a Deployment, a Service, a ServiceAccount, RBAC rules, an APIService registration. There is no installer. There is only YAML and `kubectl apply` *[cross-bearing: see Ch 13 §7 — metrics-server and the resource metrics pipeline]*.

**3.** It sets the Deployment's Pod template back to a previous revision's template, which causes the Deployment controller to roll the workload back to the corresponding ReplicaSet. The rollback itself is recorded as a new revision: the history moves forward even though the workload moves backward *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*.

**4.** A CustomResourceDefinition naming that kind has to be registered with the API server first, and somebody has to do that registering: a cluster administrator, or an operator's installation procedure. Custom kinds do not exist until their definitions do *[cross-bearing: see Ch 6 §8 — the control loop, extended]*.

**5.** In a ConfigMap, or a Secret if it is sensitive, consumed by the Pod as an environment variable or a mounted file. Baking it into the image is wrong because it makes the image environment-specific: you would need one image per environment, which destroys the property that made images useful in the first place *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*.

**6.** A tag is a mutable, human-friendly pointer at an image; a digest is an immutable cryptographic hash of the image's content, and is therefore its identity. A registry is a service implementing the OCI distribution API: a place that stores and serves content addressed by digest *[cross-bearing: see Ch 2 §3 — registries, tags, and digests]*.

**7.** Most people's answer includes some subset of: a name, a version, a place to get it from, the ability to install without reading the contents, the ability to uninstall cleanly, and the ability to find out what is currently installed. Hold onto whichever ones you named. You will need them shortly.

**8.** Honest answers: copy the directory and edit the copy, and now you maintain two directories that will drift; run `sed` over the manifests in a shell script, and now your configuration is a text-substitution program with no validation; hand-edit before each apply, and now the process is a human with a good memory. Every one of these is a real thing people do. Every one of them has a specific failure mode, and this chapter names all four.

---

**If you got 6+ right:** Skim, but read §3 and §6 properly. Those two are what this chapter is actually about; the rest is vocabulary you can move through quickly.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Re-read **Ch 4 §1** before starting this chapter — not alongside it. That section is the foundation the whole first half rests on. If question 3 specifically was one you missed, add **Ch 6 §5** to that list; §3 of this chapter is unreadable without it.

</details>

---

## Why This Chapter Matters

Thirteen chapters have now told you to install something.

Install a CNI plugin, because the network model requires one and Kubernetes does not ship one *[cross-bearing: see Ch 9 §1 — the network model and CNI]*. Install an Ingress controller, because the Ingress object does nothing without one *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*. Install a CSI driver. Install metrics-server, or `kubectl top` will keep failing *[cross-bearing: see Ch 13 §7 — metrics-server and the resource metrics pipeline]*. Chapter 13 closed by naming this debt out loud: *this chapter kept saying "somebody has to install that."*

Not one of those chapters said how.

That was deliberate, and it is now due. Here is the shape of the answer, and the shape of the problem. In a declarative system there is no installer; there is only a set of objects that somebody wrote, which you apply. "Install metrics-server" means: fetch about forty YAML files, read enough of them to find the six values that need to be different on your cluster, change those six, apply the whole set in roughly the right order, and hope. That is not a distribution mechanism. That is a directory with instructions attached, and the instructions are a note somebody left for the next watch.

So the question this chapter opens on is not "which tool should I use." It is prior to that. **When somebody hands you forty YAML files and a README, what have they actually handed you, and why does it not have a name yet?**

Everything you have built in this book so far has been a single object. A Pod. A Deployment. A Service. A PersistentVolumeClaim. Practitioners do not hand each other objects. They hand each other *units*: a named, versioned thing that installs as one act, uninstalls as one act, can be given to somebody who will never read it, and can be undone when it turns out to have been a mistake. This chapter is where you stop writing manifests and start shipping software, and the shift is larger than the tooling makes it look.

The stakes are the ones Chapter 1 already put on the table. Cloud Native Application Delivery went from 8% of the exam to 16% under the current blueprint [source: lf-kcna-exam-page-2026-08-23], and study material built for the old one under-serves this material by half. This is the first chapter that cashes that.

**One disclosure before we start, because this book has been consistent about them and this is the chapter where consistency costs something.**

CNCF publishes the competency name, "Application Delivery," and publishes nothing beneath it [source: cncf-kcna-curriculum-pdf-2026-08-23]. No sub-topic list. No named tools. The words *Helm* and *Kustomize* appear nowhere in the published curriculum, nowhere on the Linux Foundation exam page [source: lf-kcna-exam-page-2026-08-23], and nowhere on the public course outline for LFS250, the training course the Linux Foundation bundles with the exam [source: lf-lfs250-course-outline-2026-08-31]. The published outline resolves only to a chapter title.

So the topic list in this chapter is authored inference. It comes from what the ecosystem actually uses to solve the problem the competency names, and from the fact that a domain called Application Delivery with no coverage of how applications are packaged would be a strange thing indeed. It is, I think, clearly the right call. But you should know it is a call. In practice this means one rule holds throughout: nothing in this chapter is described as "frequently tested" or "commonly appears," because nobody outside the exam authority knows that. Where two things are genuinely easy to confuse, I will say so, and that claim stands on its own.

> **Logbook Entry:** Every operations team eventually accumulates the directory. You know the one. It is called `k8s/` or `deploy/` or, in the most honest cases, `yaml/`. Inside it there is `deployment.yaml`, and beside that `deployment-staging.yaml`, and beside *that* `deployment-prod-final-v2-USE-THIS-ONE.yaml`, whose name is a small monument to the moment somebody realized the naming scheme had stopped working and did not have time to fix it.
>
> There is usually a `README` too, and the README usually contains a numbered list, and step 4 of that list usually says something like "change the image tag and the ingress host, then apply in this order." Step 4 is the whole problem, written down by somebody who could see it clearly and had no vocabulary for it.
>
> This is not incompetence. It is what happens when a perfectly good technique, declarative object configuration, is asked to do a job one size larger than the job it was designed for. The directory is the correct answer to "how do I describe what should be running." It is the wrong answer to "how do I give this to someone else."

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Name** the four things a folder of manifests cannot do, and recognize each one the moment you hit it
- **Read** a Helm chart's directory layout and say what each entry is *for*
- **Separate** package from installation from installed-state — chart, Helm release, release revision — and stop collapsing three things into one word
- **Distinguish** `helm rollback` from `kubectl rollout undo`: different unit, different scope, same English word
- **Explain** what Kustomize does instead of templating, and why it needs no engine you have to install
- **Choose** between the two for a given situation, and say what the choice actually turns on

*You'll also stop reading this as a chapter about YAML syntax, which is the misreading it exists to prevent.*

---

## ⚪ §1 — Why a Folder of YAML Stops Working

Start where Chapter 13 left you: with a cluster that needs metrics-server, and no idea how it gets there.

You already have a technique for this, and it is a good one. Write the objects you want. Put them in a directory. Run `kubectl apply -f manifests/`. The API server records your intent and the controllers reconcile toward it *[cross-bearing: see Ch 4 §6 — a declaration, not an order]*. For a single application on a single cluster maintained by a single person, this is not a compromise or a stepping stone. It is correct, and you should keep doing it.

It stops working in four specific places. Not "gets awkward" — stops. Each of the four is a thing the technique structurally cannot do, and naming them precisely matters, because the rest of this chapter answers exactly these four and nothing else.

### Failure one: environment variation

The same application runs in three places. Staging wants two replicas, production wants twelve, and the developer's laptop cluster wants one. Staging points at `db.staging.internal`, production at `db.prod.internal`. Production has resource limits; the laptop cannot afford them.

You know where the *configuration* goes: ConfigMaps and Secrets, kept outside the image *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. But the replica count is not configuration the application reads. It is a field in the Deployment's spec. So is the resource limit. So is the image tag. These are differences in the manifests themselves, and a directory of manifests has exactly one answer to that: make another directory.

Now you have two directories that are 95% identical, and the 5% is not marked. Six weeks later somebody fixes a readiness probe in staging and does not fix it in production, because nothing told them there was a second copy. This is drift, and it is not a discipline problem: it is what happens when two files are supposed to stay in sync and nothing in the system knows that they are.

<!-- FIGURE: ch14-fig01-manifest-to-package-progression -->
```
  ONE CLUSTER                THREE CLUSTERS                  WHAT YOU WANT
  ───────────                ──────────────                  ─────────────

  manifests/                 manifests-dev/     ◄─┐          package v1.2.0
    deployment.yaml            deployment.yaml    │            (one copy,
    service.yaml               service.yaml       │             versioned)
    configmap.yaml             configmap.yaml     │
                                                  │          + dev-values
       │                     manifests-staging/   │          + staging-values
       ▼                       deployment.yaml    ├─ 95%      + prod-values
   ┌────────┐                  service.yaml       │  identical
   │cluster │                  configmap.yaml     │  and nothing              │
   └────────┘                                     │  marks the 5%      ┌──────┼──────┐
                             manifests-prod/      │                    ▼      ▼      ▼
   Correct. Keep              deployment.yaml     │                 ┌───┐  ┌───┐  ┌───┐
   doing this.                service.yaml        │                 │dev│  │stg│  │prd│
                              configmap.yaml    ◄─┘                 └───┘  └───┘  └───┘

                             ▲▲▲ THIS IS WHERE MOST TEAMS LIVE ▲▲▲
```

### Failure two: apply ordering

`kubectl apply -f manifests/` applies everything in the directory. It does not undertake to apply things in an order that makes sense.

Mostly this does not matter, because Kubernetes is a reconciling system: a Deployment whose ConfigMap does not exist yet will produce Pods stuck in `CreateContainerConfigError` until the ConfigMap shows up, and then it will recover on its own *[cross-bearing: see Ch 13 §2 — diagnosing a Pod that will not start]*. Eventual consistency covers a great many ordering sins.

It does not cover all of them. The sharpest case is the one you pre-tested in the Soundings: a manifest whose `kind` is a custom resource. Custom kinds do not exist until a CustomResourceDefinition registers them with the API server *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. Apply a `PostgresCluster` before the CRD that defines `PostgresCluster`, and the API server does not queue your object for later. It rejects it, because as far as the API server is concerned you have asked it to create an object of a kind that does not exist. There is no reconciliation to wait for. There is only an error.

So the README says "apply the CRDs first, then everything else." Which is to say: the ordering information exists, and it lives in prose, in a file that no software reads.

### Failure three: versioning

A directory does not have a version.

This sounds like a small thing and it is not. Ask the question that operations teams ask at three in the morning: *what is currently installed on this cluster?* With a directory, the honest answer is "whatever was in that directory the last time somebody applied it, assuming nobody has applied anything since, and assuming the directory has not changed." You can check what objects exist. You cannot ask the cluster what *version of the thing* is installed, because the thing has no version and, strictly speaking, is not a thing. It is a set of objects that happen to have arrived together.

And because there is no version, there is no meaningful undo. You can roll back a Deployment *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*, and that is genuinely useful, but it rolls back one Deployment. It does not roll back "the release that also changed the ConfigMap and added a Service and modified the Ingress rule." Those are five objects with five independent histories, and nothing in the cluster knows they were once one act.

### Failure four: distribution

The one that matters most, and the one that is easiest to miss because it does not bite you. It bites the person you hand the directory to.

You cannot give somebody a directory of manifests and expect them to install it without reading it. They have to read it, because the parts they need to change are not marked, and the order is in the README, and the README might be out of date. Every installation is a small act of comprehension, which is a poor thing to require of somebody taking over the watch.

This is why "install metrics-server" is a forty-file operation. Not because metrics-server is complicated: it is a Deployment, a Service, some RBAC, and an APIService registration. It is a forty-file operation because there is no unit smaller than "all forty files, plus the knowledge of which parts are yours to change."

> 🪝 **Snag:** It is tempting to read these four as one problem, "manifests are messy." They are not one problem, and the difference shows up on exam-shaped questions. Environment variation is about *what varies*. Ordering is about *sequence*. Versioning is about *identity over time*. Distribution is about *handing it to a stranger*. A tool can solve some and not others, and §6 is entirely about which solves which.

Two tools in the ecosystem answer these four, from opposite directions. **Helm** is a package manager for Kubernetes [source: helm-homepage-2026-08-31], and is the whole of §2, §3, and §4. **Kustomize** takes a different route entirely and is §5 *[cross-bearing: see Ch 14 §5 — patching instead of templating]*.

That is all you get about the answers for now. Sit with the problem a moment longer; §2 will not mean much unless the problem is clear.

---

## ⚪ §2 — What a Chart Contains

Helm calls its packaging format a **chart**, which is a convenient word for a book like this one.

> ★ **Fixed Point**
>
> **A chart is a collection of files that describe a related set of Kubernetes resources**, laid out in a particular directory tree, and packageable into versioned archives for deployment [source: helm-charts-2026-08-31]. A single chart might deploy something as simple as one memcached Pod, or as complex as a full web-app stack with HTTP servers, databases, and caches [source: helm-charts-2026-08-31].

Note what that definition contains and what it does not. It says *collection of files*, *versioned*, *deployable*. It does not say *templated*. Templating is in there, and we will get to it, but the definition of a chart does not require it, and that is not an accident of phrasing. Hold onto it; §7 is built on it.

The directory name is the name of the chart, without version information: a chart describing WordPress lives in a `wordpress/` directory [source: helm-charts-2026-08-31].

<!-- FIGURE: ch14-fig02-helm-chart-anatomy -->
```
  wordpress/
  │
  ├── Chart.yaml ─────────► WHO THIS CHART IS.
  │                         Name, version, description. Every chart
  │                         must have this file.
  │
  ├── values.yaml ────────► THE KNOBS, AND THEIR DEFAULTS.
  │                         Everything the installer is allowed to
  │                         change, with a working value for each.
  │
  ├── templates/ ─────────► WHAT GETS CREATED.
  │                         Combined with values, generates valid
  │                         Kubernetes manifests.
  │     ├── deployment.yaml
  │     ├── service.yaml
  │     ├── NOTES.txt          (grey: usage notes printed on install)
  │     └── _helpers.tpl       (grey: partials, not manifests)
  │
  ├── charts/ ────────────► CHARTS THIS CHART DEPENDS ON.
  │                         *** NOT A REPOSITORY. ***
  │                         A directory, inside this chart, holding
  │                         other charts. See §4 for repositories.
  │
  ├── crds/ ──────────────► DEFINITIONS THAT MUST EXIST FIRST.
  │                         Not templated. Installed before the
  │                         templates render. See §6 for why.
  │
  ├── LICENSE                  (grey: optional)
  └── README.md                (grey: optional)
```

Take the five annotated entries one at a time, and notice that the useful question about each is not *what is it* but *what is it for*.

### `Chart.yaml` — the chart's identity

Every chart must have this file [source: helm-glossary-2026-08-31]. It carries the chart's name, its version, and its description. Charts are versioned according to the SemVer 2 specification, and **a version number is required on every chart** [source: helm-glossary-2026-08-31].

That requirement is failure three from §1, closed by fiat. A directory has no version because nothing makes it have one; a chart has a version because Helm refuses to work with a chart that lacks one. `Chart.yaml` is also where dependencies are declared, having absorbed the older `requirements.yaml` file in Helm 3 [source: helm-changes-since-helm2-2026-08-31].

### `values.yaml` — the declared surface of variation

`values.yaml` holds the default configuration values for the chart [source: helm-charts-2026-08-23].

This is failure one, and "it holds the defaults" undersells what the file accomplishes. `values.yaml` is where the chart author states, in one place, **which things an installer is allowed to change**, and gives each of them a value that works. Everything in that file is a knob. Everything not in that file is a decision the chart author made on your behalf.

That is the same move as ConfigMaps, one level up. A ConfigMap externalizes configuration out of the image so the image can be environment-independent *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. `values.yaml` externalizes variation out of the manifests so the *manifests* can be environment-independent. Same principle, different layer.

At install time you override those defaults. `--values` (or `-f`) points at a YAML file of overrides, and can be given more than once, with the rightmost file taking precedence; `--set` supplies overrides on the command line, and where both are used, `--set` values are merged into `--values` with higher precedence [source: helm-using-helm-2026-08-31].

### `templates/` — what gets created

A directory of templates that, **when combined with values, generate valid Kubernetes manifest files** [source: helm-charts-2026-08-23].

That sentence is the whole mechanism. A template is a Kubernetes manifest with holes in it; values fill the holes; the result is an ordinary manifest of the kind you have been writing since Chapter 4. Here is a fragment of a Deployment template beside what it renders to:

```
Template (in templates/deployment.yaml):

    spec:
      replicas: {{ .Values.replicaCount }}

With values.yaml containing `replicaCount: 3`, this renders to:

    spec:
      replicas: 3
```

That is as far as this book goes into Helm's template language. It is a Go template dialect with a substantial function library, conditionals, loops, and named partials, and you could spend a week on it. You do not need to for this exam, and, more to the point, spending pages on template syntax would argue against this chapter's own conclusion. The syntax is not what a chart *is*.

Two entries in `templates/` are not manifests. `NOTES.txt` is an optional plain-text file containing short usage notes [source: helm-charts-2026-08-23]: the "here is how to reach your new installation" text printed after a successful install. And files whose names begin with an underscore, conventionally `_helpers.tpl`, are assumed *not* to have a manifest inside; they are not rendered to Kubernetes object definitions but are available everywhere within other chart templates for use [source: helm-named-templates-2026-08-31]. They hold reusable partials. Neither becomes an object in your cluster.

### `charts/` — a directory of dependency charts

A directory containing any charts upon which this chart depends [source: helm-charts-2026-08-23]. A chart nested inside another chart this way is a **subchart**.

This solves a real problem: your application chart needs a Redis, and somebody has already written a good Redis chart, so you depend on theirs instead of writing your own. Install the parent, get both.

> 🪝 **Snag:** `charts/` is not a chart repository. It is a directory *inside a chart* holding the charts that chart depends on. A chart repository is something else entirely: an HTTP server, out on the network, which §4 covers. The two share a word and share nothing else, and this is one of the genuinely easy confusions in this material. If you take one thing from this figure, take that annotation.

### `crds/` — Custom Resource Definitions

A special directory you can create in your chart to hold your CRDs [source: helm-crd-best-practices-2026-08-31]. These CRDs are **not templated**, and are installed by default when you run `helm install` for the chart [source: helm-crd-best-practices-2026-08-31].

That is failure two, ordering, and §6 explains exactly why it needs its own directory rather than being one more file in `templates/`. For now, note the two properties: not templated, and installed first. Both will matter.

> ⚓ **Worth Securing:** The `Chart.yaml` `apiVersion` field was bumped from `v1` to `v2` for Helm 3, because Helm 2 clients could not understand the new library-chart support or the consolidation of `requirements.yaml` into `Chart.yaml` [source: helm-changes-since-helm2-2026-08-31]. If you ever find yourself looking at a chart in the wild and wondering how old it is, that field is the tell.

The section's thesis, stated plainly now that you have seen the parts: **the chart is the unit, and templating is how the unit absorbs variation.** Templating is not what makes it a chart. Versioning, a declared variation surface, and packageability are what make it a chart. That distinction is going to do a great deal of work in §7.

A worked instance, to make the abstraction concrete. Take the Deployment from Chapter 6, the one with the ownership chain down to ReplicaSets and Pods *[cross-bearing: see Ch 6 §1 — the resource that holds the intent]*. Chapter 6 promised that a Helm chart's job is to template that object, and here is what that means: the Deployment goes in `templates/deployment.yaml` with its replica count, image tag, and resource limits replaced by value references; the working defaults for those go in `values.yaml`; and the whole thing gets a name and a version in `Chart.yaml`. The Deployment did not change. It acquired a wrapper that knows what varies about it.

Everything in a chart's `templates/` becomes objects in a cluster the same way your hand-written manifests do, through the API server, as records of intent *[cross-bearing: see Ch 4 §2 — the anatomy of a record]*. Charts do not have a private channel into the cluster. They generate manifests and the manifests go the ordinary way.

One thing charts are *not*, and it is worth saying now so you are not surprised in Chapter 15: a chart is a source of manifests, not a thing that applies them on a schedule. A delivery agent that watches a repository and keeps a cluster in sync can use a chart as its manifest source, and that arrangement is where a great deal of production delivery actually happens *[cross-bearing: see Ch 15 §4 — an agent that watches a repository]*.

---

## 🔵 §3 — Chart, Release, Revision

This is the section the subtitle is about, and the one thing in this chapter to get exactly right.

Four words are in play, and readers routinely collapse them into two. You already own two of them. All four side by side, then the rest of the section goes to the two that are new.

| Word | What it is | Where you met it |
|---|---|---|
| **Package** | The chart. A named, versioned collection of files. | §2, just now |
| **Manifest** | What templates render to. An ordinary Kubernetes object description. | Ch 4 §2 |
| **Helm release** | One installation of a chart into a cluster. | Here |
| **Release revision** | One numbered state of that release over time. | Here |

### A release is an installation, not a package

> ★ **Fixed Point**
>
> **A release is an instance of a chart running in a Kubernetes cluster** [source: helm-architecture-2026-08-31]. When a chart is installed, the Helm library creates a release to track that installation [source: helm-glossary-2026-08-31]. **The same chart can be installed many times, each creating a separately named release that can be upgraded and rolled back independently** [source: helm-charts-2026-08-23].

Read that last clause twice. One chart, many releases. Independently upgradable. Independently rollbackable.

The chart is the thing on the shelf. The release is the thing you installed. If you install the same WordPress chart three times, one for the marketing site, one for the docs site, one for a staging copy, you have one chart and three releases, each with its own name, its own values, and its own history. Upgrading one does not touch the others.

Naming is now mandatory. In Helm 2, omitting a name produced an auto-generated one; in production that proved to be more of a nuisance than a helpful feature, so **Helm 3 throws an error if no name is provided with `helm install`** [source: helm-changes-since-helm2-2026-08-31]. If you want one generated anyway, `--generate-name` will do it [source: helm-changes-since-helm2-2026-08-31].

Releases live in namespaces, and that changed between Helm 2 and Helm 3. In Helm 3, information about a release is stored in the same namespace as the release itself, which means you can `helm install wordpress stable/wordpress` in two separate namespaces and refer to each by changing your namespace context [source: helm-changes-since-helm2-2026-08-31]. Under Helm 2, once a name was used by a release, no other release could use that name even in a different namespace [source: helm-changes-since-helm2-2026-08-31]. A release name is scoped to a namespace, exactly as most Kubernetes object names are *[cross-bearing: see Ch 4 §3 — where a name lives]*.

That same change reshaped `helm list`: it no longer lists all releases by default, listing only those in your current context's namespace, and you must supply `--all-namespaces` for Helm 2-like behavior [source: helm-changes-since-helm2-2026-08-31].

> ⚓ **Worth Securing:** Where does a Helm release's state actually live? **In Secrets, in the namespace of the release, by default** [source: helm-storage-backends-2026-08-31]. Not in a Helm server component — there isn't one — and not on your laptop. The `HELM_DRIVER` environment variable selects the backend and accepts `configmap`, `secret`, or `sql` [source: helm-storage-backends-2026-08-31].
>
> This is a small fact with a large implication: Helm's record of what it installed is an ordinary Kubernetes object, subject to the ordinary rules *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. Whoever can read Secrets in that namespace can read Helm's bookkeeping. Whoever can delete them can make Helm forget.

### A revision is a numbered state of a release

Installing creates a release at revision 1. Upgrading creates revision 2. Upgrade again, revision 3. **A sequential counter is used to track releases as they change** [source: helm-glossary-2026-08-31].

Upgrades are not wholesale replacements. `helm upgrade` will only update things that have changed since the last release [source: helm-using-helm-2026-08-31]. The unchanged objects stay as they are.

<!-- FIGURE: ch14-fig03-release-vs-chart-vs-revision -->
```
                        ┌──────────────────────────────┐
                        │   CHART:  wordpress 15.2.0   │
                        │   (a package. on the shelf.  │
                        │    installed zero times so   │
                        │    far in this diagram.)     │
                        └───────────┬──────────────────┘
                                    │
              helm install ─────────┴───────── helm install
                     │                              │
                     ▼                              ▼
        ┌─────────────────────────┐   ┌─────────────────────────┐
        │ RELEASE: "marketing"    │   │ RELEASE: "docs"         │
        │ namespace: marketing    │   │ namespace: docs         │
        │ values: 12 replicas     │   │ values: 2 replicas      │
        └───────────┬─────────────┘   └─────────────────────────┘
                    │                    (its own history,
                    │                     untouched by anything
                    │                     done to "marketing")
                    ▼
    ┌───────┐   ┌───────┐   ┌───────┐   ┌───────┐
    │ rev 1 │──►│ rev 2 │──►│ rev 3 │──►│ rev 4 │
    │install│   │upgrade│   │upgrade│   │  ???  │
    └───────┘   └───────┘   └───────┘   └───────┘
                                ▲
                                └─ helm rollback marketing 2
                                   returns the release to
                                   revision 2's state.
```

<!-- AUTHOR-REVIEW: the cached corpus does not state whether a `helm rollback` operation is itself recorded as a NEW numbered revision (i.e. whether rolling back from rev 3 to rev 2 produces a rev 4 whose content matches rev 2, or moves the pointer back to rev 2). The helm_rollback CLI reference [helm-rollback-cli-2026-08-31] gives only the argument semantics. Figure ch14-fig03 currently shows "rev 4 ???" and the prose below deliberately declines to state the counter behavior. This is the discriminating detail in this section's central contrast and MUST NOT be written from memory. Needs a fetch of helm.sh/docs/helm/helm_upgrade/ or the Helm release-lifecycle documentation before this can be resolved either way. -->

The rollback command's argument shape is straightforward: **the first argument is the name of a release and the second is a revision (version) number; if that second argument is omitted or set to `0`, it rolls back to the previous release** [source: helm-rollback-cli-2026-08-31].

### The word that means two things

Now the payoff, and Chapter 6 owes you this one. It told you that you would meet the word "rollback" twice more in this book, attached to entirely different mechanisms, and pointed at this chapter and at Chapter 15 *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*. This is the first of those two. The second is Chapter 15's rollback-by-revert *[cross-bearing: see Ch 15 §4 — an agent that watches a repository]*, and it is a third thing again.

> ★ **Fixed Point**
>
> **`helm rollback` and `kubectl rollout undo` are different mechanisms wearing the same English word.** They differ in three ways:
>
> - **Unit.** `helm rollback` operates on a *Helm release* — everything the chart installed. `kubectl rollout undo` operates on *one workload object*: a Deployment, DaemonSet, or StatefulSet [source: k8s-docs-kubectl-rollout-2026-08-24].
> - **Scope.** A Helm rollback returns the whole release to a previous revision: the Deployment, the Service, the ConfigMap, the Ingress rule, all of it. `kubectl rollout undo` changes one workload's Pod template and nothing else.
> - **Bookkeeping.** Helm's history lives in the release record, Secrets in the release's namespace [source: helm-storage-backends-2026-08-31]. A Deployment's revision history lives in its ReplicaSets *[cross-bearing: see Ch 6 §1 — the Deployment to ReplicaSet to Pod ownership chain]*.
>
> Neither calls the other. `helm rollback` does not run `kubectl rollout undo` underneath.

That last line is the trap to name outright, because the two mechanisms *look* like they should be related and are not. When Helm rolls a release back, it computes the objects the target revision described and applies them. If that changes a Deployment's Pod template, the Deployment controller does what it always does and starts a rolling update *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*. The rolling update is a *consequence*, in the ordinary reconciling way. Helm did not ask for it. Helm changed a record of intent, and a controller noticed.

> 🪢 **Mnemonic:** **The scope is in the noun.** `helm rollback` takes a *release* name. `kubectl rollout undo` takes a *Deployment* name. Whatever noun the command takes is the unit it moves, and since one of those nouns contains many of the other, the difference in blast radius follows from the grammar. If you can remember which command takes which noun, you cannot get the scope question wrong.

> ⚠ **Navigational Hazards**
>
> Three collapses to avoid, in increasing order of how often they catch people:
>
> **Chart and release used interchangeably.** "I rolled back the chart." You did not; a chart is a package and packages do not have installed state. You rolled back a release. This one matters because the correction is not pedantry: the whole point of the distinction is that *one chart installs many times*, and a sentence that conflates them cannot express that.
>
> **"Revision" left unqualified.** Chapter 6 owns the unqualified word for Deployment revisions. In this chapter and the next, say **release revision** or **Helm revision** whenever there is any chance of ambiguity.
>
> **"Rollback" left unqualified.** There are three rollbacks in this book — Deployment, Helm release, and GitOps revert — and the bare noun distinguishes none of them. Say which.

> **Extended Analogy:** Think about how you already reason about installed software on a machine you administer.
>
> There is a *package*: a named, versioned artifact sitting in a repository, identical for everyone who fetches it. Nobody's machine changes it. It is a thing you can name and a thing you can pin.
>
> There is an *installation*: what happened when you ran the install on this particular machine, with these particular options. Two machines can install the same package and end up meaningfully different, because the options differed. The installation has a location, a configuration, and a state.
>
> And there is the *history* of that installation, the record of what version was installed when, and what it was before, which is what lets you say "put it back the way it was on Tuesday."
>
> Chart, release, revision. You have had this mental model since the first time you administered anything. Helm did not invent it; Helm brought it to Kubernetes, where the native tooling had objects but no packages. The reason the vocabulary is worth learning precisely is not that the concepts are hard, since you already hold them, but that Kubernetes had no word for any of it until Helm supplied three.

---

## ⚪ §4 — Where Charts Come From

Failure four was distribution: you cannot hand somebody a directory. So where do charts live, and how do they travel?

### The chart repository

> ★ **Fixed Point**
>
> **A chart repository is an HTTP server that houses an `index.yaml` file and optionally some packaged charts** [source: helm-chart-repository-2026-08-31]. It is managed with the `helm repo` commands [source: helm-charts-2026-08-23].

That is the whole definition, and its plainness is the interesting part. Not a service with an API surface. Not a daemon. An HTTP server, holding an index file and some tarballs. Because a chart repository can be any HTTP server that can serve YAML and tar files and answer GET requests, you have a plethora of options for hosting your own [source: helm-chart-repository-2026-08-31].

The index is a YAML file called `index.yaml`, containing metadata about the packages, including the contents of each chart's `Chart.yaml` file [source: helm-chart-repository-2026-08-31]. That is how `helm repo add` works: fetch the index once, and now your client knows what that server has and at what versions, without downloading anything else.

A packaged chart is a **chart archive**: a tarred and gzipped, and optionally signed, chart [source: helm-glossary-2026-08-31].

> 🪝 **Snag:** Second half of the trap from §2, and this is the sentence to hold: `charts/` is a **directory inside a chart** containing the charts it depends on. A **chart repository** is an **HTTP server on the network** housing packaged charts. Same word, opposite ends of the pipeline: one is a component of a package, the other is a place packages are kept. If a question puts both in play, that is the distinction it is testing.

### Registries hold charts too

Here is the part that pays off Chapter 2 in a way you would not have predicted.

You learned about registries as the place container images live *[cross-bearing: see Ch 2 §3 — registries, tags, and digests]*. Re-read the OCI's own definition of a registry with fresh eyes: **"a service that handles the required APIs defined in this specification"** [source: oci-distribution-spec-2026-08-24]. Not "a service that stores images." A service that implements an API for distributing *content*.

That distinction was doing quiet work all along. The OCI Distribution Specification defines "an API protocol to facilitate and standardize the distribution of content" [source: oci-distribution-spec-2026-08-24]: content, addressed by digest, with no requirement that the content be an image.

So: **with the release of Helm 3.8.0, Helm is able to store and work with charts in container registries, as an alternative to Helm repositories** [source: helm-blog-oci-ga-2026-08-31]. Since OCI artifacts make it possible to store more than container images, you can store charts, images, and other artifacts in a single OCI registry [source: helm-blog-oci-ga-2026-08-31]. The Helm documentation now recommends using container registries with OCI support to store and share chart packages [source: helm-oci-registries-2026-08-31].

An OCI-based registry can contain zero or more Helm repositories, and each of those repositories can contain zero or more packaged Helm charts [source: helm-oci-registries-2026-08-31]. When pushing, the reference must be prefixed with `oci://` [source: helm-oci-registries-2026-08-31]; the registry reference basename is inferred from the chart's name, and the tag from the chart's semantic version [source: helm-oci-registries-2026-08-31].

The reasoning behind the shift is instructive, and the Helm project wrote it down. Chart repositories had "a very hard time abstracting most of the security implementations required in a production environment," a standard authentication and authorization API being important in production; chart provenance signing was optional rather than integral; the same chart uploaded by two tenants cost twice the storage; and a single index file serving search, metadata, and fetching was clunky to design around securely [source: helm-changes-since-helm2-2026-08-31]. Meanwhile the Distribution project, the successor to the original Docker Registry, had many years of hardening, security best practices, and battle-testing behind it, offered as a product by many major cloud vendors [source: helm-changes-since-helm2-2026-08-31].

Which is to say: rather than reinvent a hardened content-distribution service, Helm moved onto the one the industry had already built. Standardization at the OCI layer *[cross-bearing: see Ch 2 §5 — the Open Container Initiative]* turned out to buy something nobody was specifically aiming at when the distribution spec was written.

### Chart version is not application version

One quiet error to close on.

Charts are versioned according to SemVer 2, and a version number is required on every chart [source: helm-glossary-2026-08-31]. That version is **the chart's**, the packaging's. It moves when the packaging changes: a template fixed, a default adjusted, a new value exposed.

`Chart.yaml` separately carries `appVersion`, the version of the *application the chart installs*. These move independently. You can ship chart 4.1.2 and 4.1.3 that both install nginx 1.25.3, because what changed between them was the chart. You can ship chart 5.0.0 that installs nginx 1.26.0, where both changed at once.

> 🪢 **Mnemonic:** **Version is the box; `appVersion` is what's in the box.** You can redesign the box without changing the contents, and you can change the contents without redesigning the box. If a question gives you two numbers and asks which one the chart maintainer bumps when they fix a template typo, it is the box.

---

## ☆ Taking Your Bearings: The Package and the Thing You Installed

Five questions on §1 through §4. Take them before reading the answers.

**1.** You run `helm install marketing wordpress/wordpress` and then, in a different namespace, `helm install docs wordpress/wordpress`. Later you run `helm rollback marketing 2`. What happens to the `docs` installation?

A) It also rolls back to revision 2, because both come from the same chart
B) Nothing — releases are upgraded and rolled back independently
C) It is deleted, because the chart's release name was reused
D) Helm refuses the rollback, because two releases share a chart

**2.** A colleague says: "I looked in the chart's `charts/` directory to find the version of Redis available in our chart repository." What has gone wrong in that sentence?

A) Nothing — `charts/` is the local cache of the configured chart repository
B) `charts/` holds the charts this chart depends on; a chart repository is an HTTP server elsewhere on the network
C) `charts/` is where `helm repo add` writes its index, so it holds only metadata, not versions
D) `charts/` is only present after `helm install`, so it would be empty before then

**3.** Which of these is required to be present in every Helm chart?

A) `crds/`
B) `templates/NOTES.txt`
C) `Chart.yaml`, including a version number
D) `_helpers.tpl`

**4.** `[retrieval: ch6]` You run `kubectl rollout undo deployment/api`. Which statement is correct?

A) It reverts the Deployment's Pod template to a previous revision, and the rollback is itself recorded in the Deployment's revision history
B) It deletes the current ReplicaSet and recreates the previous one, discarding the newer revision from the history
C) It reverts the entire set of objects that were applied at the same time as the Deployment
D) It pauses the rollout so that no further changes take effect until resumed

**5.** Your team publishes a chart that installs nginx. You fix a typo in a template label — no change to which nginx is installed. Which field in `Chart.yaml` should move?

A) `appVersion`, because the chart's output changed
B) The chart `version`, because the packaging changed
C) Both, always, since they are required to stay in step
D) Neither; template fixes are not versioned changes

---

**Answers with Explanations**

**1. B.** One chart, many releases, each upgraded and rolled back independently [source: helm-charts-2026-08-23]. **A is wrong** and is the single most common collapse in this material: it treats the chart as if it had installed state, when the chart is a package and only the release is installed. **C is wrong** because the names differ, and in any case Helm 3 scopes release names to their namespace [source: helm-changes-since-helm2-2026-08-31]. **D is wrong**; sharing a chart is the normal case, not a conflict.

**2. B.** `charts/` is a directory containing any charts upon which this chart depends [source: helm-charts-2026-08-23]; a chart repository is an HTTP server housing an `index.yaml` and packaged charts [source: helm-chart-repository-2026-08-31]. **A is wrong**: it is not a cache of anything; it is part of the chart's own content. **C is wrong**: `helm repo add` does not write into a chart's `charts/` directory. **D is wrong**; `charts/` is authored content and exists in the chart as shipped.

**3. C.** Every chart must have `Chart.yaml` [source: helm-glossary-2026-08-31], and a version number is required on every chart [source: helm-glossary-2026-08-31]. **A is wrong**: `crds/` is a special directory you *can* create [source: helm-crd-best-practices-2026-08-31], not one you must. **B is wrong**: `NOTES.txt` is explicitly optional [source: helm-charts-2026-08-23]. **D is wrong**; `_helpers.tpl` is a convention for partials [source: helm-named-templates-2026-08-31], useful but not required.

**4. A.** `kubectl rollout undo` undoes a previous rollout [source: k8s-docs-kubectl-rollout-2026-08-24] by reverting the Pod template; the history moves forward even as the workload moves back. **B is wrong**: the previous ReplicaSet is not recreated, it is scaled back up; it never left. **C is wrong**, and this is the distractor worth dwelling on: the multi-object scope belongs to `helm rollback`, not to `kubectl rollout undo`, and mixing them up is exactly the confusion §3 exists to prevent. **D describes `kubectl rollout pause`**, a different subcommand entirely [source: k8s-docs-kubectl-rollout-2026-08-24].

**5. B.** The chart's own version tracks the packaging; `appVersion` tracks the application the chart installs, and they move independently. **A inverts the two.** **C is wrong**: nothing requires them to move together, and requiring it would force meaningless application-version bumps for template fixes. **D is wrong**: charts are versioned according to SemVer 2 and a version is required [source: helm-glossary-2026-08-31], so any published change gets one.

**If you scored 0–2:** Re-read **§3** before continuing. Not the whole chapter — §3. The chart/release/revision split is what §5 and §6 are built on, and if it has not landed yet, the Kustomize contrast will read as a second set of vocabulary rather than as a contrast.

**Checkpoint: You've Now Mastered**
✓ The four things a folder of manifests structurally cannot do
✓ What each entry in a chart directory is *for*
✓ Chart vs Helm release vs release revision — three words, three things
✓ Why `helm rollback` and `kubectl rollout undo` are not the same mechanism
✓ Where charts live, and why registries turned out to hold more than images

One more tool to meet, and it disagrees with Helm about almost everything except the goal.

---

## 🔵 §5 — Patching Instead of Templating

Everything so far has come from one idea: describe the manifest with holes in it, and fill the holes.

There is another answer, and it starts by refusing that idea outright.

> ★ **Fixed Point**
>
> **Kustomize introduces a template-free way to customize application configuration** [source: kustomize-overview-2026-08-23]. It is a standalone tool for customizing Kubernetes objects through a kustomization file [source: k8s-docs-kustomization-2026-08-31], and **it is built into kubectl as `apply -k`** [source: kustomize-overview-2026-08-23]. Since Kubernetes 1.14, kubectl has supported management of objects using a kustomization file [source: k8s-docs-kustomization-2026-08-31].

Two things in that block do independent work and should be held separately.

**Template-free.** There are no placeholders. The files in a Kustomize setup are ordinary, valid, applyable Kubernetes manifests, the kind you have been writing since Chapter 4. You could `kubectl apply -f` the base directory directly and it would work. Nothing needs rendering before it becomes valid.

**Built into kubectl.** There is no engine to install, no client to distribute to your team, no version to keep in step. If a machine has kubectl, it has Kustomize. That practical fact shapes when the tool is the right answer.

### Base and overlay

The organizing idea is a fork/modify/rebase workflow: a **base** directory holds the upstream manifests and a `kustomization.yaml`, and **overlays** (dev, staging, prod, say) reference the base and layer patches, name prefixes and suffixes, labels, images, and generated ConfigMaps and Secrets on top [source: kustomize-overview-2026-08-23]. This manages any number of distinctly customized configurations without forking the originals [source: kustomize-overview-2026-08-23].

That last clause is the claim, and it is the one to hold onto: **without forking the originals**. The base is not edited. The base is not copied. Each overlay declares only its own differences and points at the base it differs from.

<!-- FIGURE: ch14-fig04-kustomize-base-overlay -->
```
        overlays/staging/                                overlays/prod/
        ┌────────────────────┐                       ┌────────────────────┐
        │ kustomization.yaml │                       │ kustomization.yaml │
        │  resources:        │                       │  resources:        │
        │    - ../../base    │                       │    - ../../base    │
        │  namePrefix: stg-  │                       │  namePrefix: prod- │
        │  replicas: 2       │                       │  replicas: 12      │
        │  patches: [...]    │                       │  patches: [...]    │
        │                    │                       │                    │
        │  ONLY THE DELTAS   │                       │  ONLY THE DELTAS   │
        └─────────┬──────────┘                       └──────────┬─────────┘
                  │                                             │
                  │          base/                              │
                  │      ┌───────────────────────┐              │
                  └─────►│ kustomization.yaml    │◄─────────────┘
                         │ deployment.yaml       │
                         │ service.yaml          │
                         │                       │
                         │  NEVER EDITED.        │
                         │  NEVER COPIED.        │
                         │  ONE OF IT.           │
                         └───────────┬───────────┘
                                     │
                  ┌──────────────────┴──────────────────┐
                  ▼                                     ▼
        kubectl apply -k overlays/staging     kubectl apply -k overlays/prod
                  │                                     │
                  ▼                                     ▼
           stg- objects, 2 replicas            prod- objects, 12 replicas
```

The kustomization file is itself a YAML specification of a Kubernetes Resource Model object called a *Kustomization*, and a kustomization describes how to generate or transform other objects [source: kubectl-book-kustomization-fields-2026-08-31]. That framing is worth noticing: the customization instructions are themselves an object of a declared kind, not a script.

### What an overlay can declare

The kustomization file's field list is long; the useful ones for our purposes cluster into four groups [source: kubectl-book-kustomization-fields-2026-08-31].

**What to include.** `resources` names the resources to include: the base, plus any manifests belonging to this overlay alone.

**Blanket transformations.** `namespace` adds a namespace to all resources. `namePrefix` and `nameSuffix` prepend or append to the names of all resources *and references*. `labels` adds labels and optionally selectors to all resources, `commonAnnotations` adds annotations. `images` modifies the name, tags, and/or digest for images. `replicas` changes the replica count for a resource.

Two of these deserve a note. `namePrefix` updating *references* as well as names is why a prefixed Deployment still finds its prefixed ConfigMap: Kustomize understands the relationships, not just the strings. And the label transformer is the same machinery you learned in Chapter 4, labels applied across every object in the overlay, with selectors updated to match *[cross-bearing: see Ch 4 §5 — the universal join]*.

**Targeted patches.** `patches` patches resources; `patchesStrategicMerge` patches using the strategic merge patch standard; `patchesJson6902` patches using the JSON 6902 standard [source: kubectl-book-kustomization-fields-2026-08-31].

Two patch styles, and the difference is one clause each. A **strategic merge patch** is a fragment of the object that looks like the object: you write the piece of the Deployment you want to change, in the same shape, and Kustomize merges it in. A **JSON patch**, meaning JSON Patch, RFC 6902, is a list of explicit operations on paths: replace this path, add to that array, remove this element. Strategic merge reads more naturally and handles most cases; JSON patch is what you reach for when you need surgical precision, particularly on list elements where merge semantics get ambiguous.

Either way, the patch targets an object by identity: its `apiVersion`, `kind`, and `metadata.name` *[cross-bearing: see Ch 4 §2 — the anatomy of a record]*. That is how Kustomize knows which base object a delta belongs to.

**Generators.** `configMapGenerator` generates ConfigMap resources, `secretGenerator` generates Secret resources, and `generatorOptions` controls their behavior [source: kubectl-book-kustomization-fields-2026-08-31].

These build ConfigMaps and Secrets from literal values or from files on disk, rather than requiring you to hand-author the object with its `data` map. Given that ConfigMaps and Secrets are precisely the objects that vary most between environments *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*, having overlays generate them is more than a convenience: it puts the most environment-specific objects in the layer that is *about* environment specificity.

> 🔭 **Closer Look:** The field list also contains `helmCharts`, described as a Helm chart inflation generator [source: kubectl-book-kustomization-fields-2026-08-31]. Kustomize can take a Helm chart, render it, and treat the rendered output as resources to patch. The two tools are not mutually exclusive at the mechanical level, whatever the arguments online suggest; §6 returns to this. Well past what the exam requires, but a useful thing to know exists the first time you see it in somebody's repository.
>
> The list also shows its own history: `bases` is a separate field from `resources`, a survival from an earlier layout in which they were distinct. Modern kustomizations list the base under `resources`.

### The move that is actually different

Step back from the field list, because the field list is not the point and it is easy to read this section as "a second syntax for the same idea."

Helm's answer to environment variation is: *make the manifest incomplete, and complete it differently each time.* The artifact in your repository is not a valid Kubernetes object. It is a template that becomes one.

Kustomize's answer is: *keep the manifest complete and correct, and describe the differences separately.* The artifact in your repository is a valid Kubernetes object throughout. Nothing is ever rendered from a non-object into an object; the transformation is object-to-object.

That difference has real consequences. You can read a base directory without a rendering engine, because it is just manifests. You can validate it with any tool that validates manifests. A newcomer can open `base/deployment.yaml` and understand it without knowing anything about Kustomize at all. Against that: there is no `values.yaml`, no single file where the author declares "these, and only these, are the things you may change." An overlay can patch anything, which is more powerful and less guided.

Neither of these is a defect. They are the same trade-off seen from two sides, and §6 is about which side you want to be standing on.

<!-- AUTHOR-REVIEW: the cached corpus for Kustomize is thin — k8s-docs-kustomization-2026-08-31 is a two-sentence capture and kustomize-overview-2026-08-23 is a marketing-page summary. The kustomization field list is well sourced [kubectl-book-kustomization-fields-2026-08-31], but the *semantics* of strategic-merge vs JSON patch, and the behavior of configMapGenerator's name-hash suffix (which is a real and pedagogically valuable behavior — it triggers rolling updates when config changes), are written here from the field names plus general knowledge rather than from a snapshot. The name-hash behavior has been deliberately OMITTED from the prose above rather than asserted untagged. Needs a fetch of the full kubernetes.io kustomization task page and/or kubectl.docs.kubernetes.io/references/kustomize/kustomization/configmapgenerator/ before either can be stated. -->

---

## 🔵 §6 — Which One, When

Two tools. Same problem. Opposite mechanisms. Which do you use?

The question is asked badly most of the time: as a preference poll, or a maturity ladder, or a tribal marker. It is none of those. It has an answer, and the answer turns on one thing.

### The distinction that decides it

**Are you distributing software to people who will not read it, or adapting software you already have for environments you control?**

If you are **distributing**, you want Helm, and the reasons are precisely the four failures from §1. A stranger needs a *name* to ask for and a *version* to pin, and `Chart.yaml` supplies both, and requires them [source: helm-glossary-2026-08-31]. They need a place to fetch it from without cloning your repository, and a chart repository or an OCI registry supplies that [source: helm-chart-repository-2026-08-31] [source: helm-oci-registries-2026-08-31]. They need to know which parts are theirs to change without reading the manifests, and `values.yaml` supplies exactly that, as a declared surface. And they need to install, upgrade, and undo as single acts against a named thing, which the release model supplies [source: helm-architecture-2026-08-31].

That is why the ecosystem ships operators, controllers, ingress controllers, and monitoring stacks as charts. Not because templating is superior. Because the recipient is a stranger, and everything a stranger needs is packaging.

If you are **adapting**, you want Kustomize. There is nobody to distribute to: the manifests are yours, they live in your repository, and the people changing them can read them. In that setting a template engine is overhead, making your artifacts un-readable-as-manifests to buy you a distribution capability you are not using. Kustomize's proposition is that your manifests stay ordinary manifests and the differences live in small overlay files that say only what differs.

<!-- FIGURE: ch14-fig05-templating-vs-overlay-decision -->
```
  ┌────────────────────┬──────────────────────────┬──────────────────────────┐
  │                    │  HELM                    │  KUSTOMIZE               │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ What varies        │  values, filling holes   │  patches, applied to a   │
  │                    │  in templates            │  complete base           │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ The unit           │  a versioned chart       │  a directory. no version │
  │                    │  (version REQUIRED)      │  (nothing requires one)  │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ Distribution       │  chart repository, or    │  none. it's your repo.   │
  │                    │  an OCI registry         │                          │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ Lifecycle          │  releases and revisions; │  none. apply is apply.   │
  │                    │  install/upgrade/rollback│  no installed-state      │
  │                    │  as single acts          │  record of its own       │
  ├────────────────────┼──────────────────────────┼──────────────────────────┤
  │ Where the engine   │  a CLI you install       │  in kubectl. `apply -k`  │
  │ lives              │                          │  Nothing to install.     │
  ├────────────────────┴──────────────────────────┴──────────────────────────┤
  │  WHAT THE CHOICE ACTUALLY TURNS ON:                                      │
  │  Distributing to strangers who won't read it  ─────────────►  HELM       │
  │  Adapting what you already have, for yourself ─────────────►  KUSTOMIZE  │
  └──────────────────────────────────────────────────────────────────────────┘
```

And the two combine. The commonest production shape is: take somebody's chart for the third-party components, use Kustomize for your own applications, and, if you need to adjust a chart's rendered output in a way its values do not expose, let Kustomize inflate the chart and patch the result [source: kubectl-book-kustomization-fields-2026-08-31]. This is not a compromise position. It is what "package" and "adapt" look like when both are happening in the same repository, which is most of the time.

### Why charts have a `crds/` directory

Now the piece we deferred, and it closes the chapter's loop.

Chapter 6 promised you an answer to this *[cross-bearing: see Ch 6 §8 — the control loop, extended]*, and the answer is failure two from §1, ordering, returning at the end of the chapter as something you can now diagnose yourself.

Recall the rule, in the Helm project's own words: **"For a CRD, the declaration must be registered before any resources of that CRDs kind(s) can be used"** [source: helm-crd-best-practices-2026-08-31]. There is a declaration of a CRD, the YAML with kind `CustomResourceDefinition`, and then there are resources that *use* the CRD [source: helm-crd-best-practices-2026-08-31]. The declaration must come first, and this is not a preference. Until the CRD is registered, the custom kind does not exist as far as the API server is concerned, and an object of that kind is not "not ready yet." It is invalid.

Now apply the chart model to that. A chart's templates render to a stream of manifests. If the CRD were merely one more file in `templates/`, it would render alongside everything else and be applied alongside everything else, and whether it landed first would be a matter of luck. That is exactly failure two: no ordering guarantee, and one case where the absence of a guarantee is fatal rather than merely slow.

So Helm carved out a directory. **`crds/` is a special directory you can create in your chart to hold your CRDs; these CRDs are not templated, but will be installed by default when running a `helm install` for the chart** [source: helm-crd-best-practices-2026-08-31]. Not templated, so there is nothing to render and nothing to sequence within. Installed by default, so the ordering is the tool's responsibility, not the README's.

The mechanism has documented limits, and they are the kind of thing that catches people in production:

- `--skip-crds` will skip the CRD installation step [source: helm-crd-best-practices-2026-08-31].
- **There is no support at this time for upgrading or deleting CRDs using Helm** [source: helm-crd-best-practices-2026-08-31].
- The `--dry-run` flag of `helm install` and `helm upgrade` is not currently supported for CRDs [source: helm-crd-best-practices-2026-08-31].

There is a second approach: put the CRD definition in one chart, and any resources that use that CRD in *another* chart, a workflow that may be more useful for cluster operators who have admin access to a cluster [source: helm-crd-best-practices-2026-08-31].

> ⚠ **Navigational Hazards**
>
> The no-upgrade limitation is the one to internalize. A chart with a `crds/` directory installs its CRDs on first install and does not update them on subsequent upgrades [source: helm-crd-best-practices-2026-08-31]. If the chart's next version ships a CRD with new fields, upgrading the release will not bring you those fields. Operators shipped as charts run into this constantly, and the symptom is confusing: the chart upgraded successfully and the new feature does not work, because the API server is still serving the old schema.
>
> The reason for the restriction is defensible. Deleting or downgrading a CRD is potentially catastrophic, since it can take every custom resource of that kind with it. Helm declining to automate that is a decision, not an oversight.

Chapter 17 collects the pluggable interfaces this book has been accumulating, and CRDs shipped as chart content is one of the places where the extension mechanism and the packaging mechanism visibly interact *[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*.

### The four, closed

Look back at §1 and check the arithmetic:

| Failure | Helm's answer | Kustomize's answer |
|---|---|---|
| **Environment variation** | `values.yaml` — a declared surface of what may change | Overlays — declared deltas against an unmodified base |
| **Apply ordering** | `crds/` for the one case that is fatal | — (`apply -k` is still an apply; same eventual consistency, same CRD problem) |
| **Versioning** | Chart version, required on every chart | — (a directory still has no version; Git supplies one, which is Ch 15's subject) |
| **Distribution** | Chart repositories and OCI registries | — (nothing to distribute; that is the premise) |

Note the shape of that column. Kustomize answers *one* of the four cleanly, declines two of them by design, and shares the fourth's limitation. That is not a deficiency; it is a smaller tool solving the subset of the problem that occurs when there is nobody to distribute to. Working out which column your situation is in is the entire skill, and it takes about ten seconds once you know what to look at.

---

## ☆ Taking Your Bearings: Patching, and Choosing

Five questions on §5 and §6.

**1.** What does Kustomize do to the base directory when you apply an overlay?

A) Copies it into the overlay directory, then patches the copy
B) Edits the base files in place to reflect the overlay's values
C) Nothing — the base is neither modified nor duplicated; the overlay declares deltas against it
D) Renders the base through a template engine using the overlay as values

**2.** A colleague says they cannot use Kustomize because they are not allowed to install additional tooling on the build agents. What is the correct response?

A) They are right; Kustomize requires a standalone binary
B) Kustomize is built into kubectl as `apply -k`, so any machine with kubectl already has it
C) They can use Helm instead, which has no separate binary
D) Kustomize runs as a controller in the cluster, so nothing is installed on the agents

**3.** A chart ships a CRD in its `crds/` directory. You upgrade the release to a chart version whose CRD adds a new field. What happens?

A) The CRD is updated as part of the upgrade, and the new field becomes available
B) The upgrade fails, because Helm detects the CRD change and refuses
C) The CRD is not upgraded — Helm has no support for upgrading CRDs — so the new field is not available
D) The CRD is deleted and recreated, taking existing custom resources with it

**4.** You are publishing a monitoring stack for other teams to install on their own clusters. They should not need to read your manifests. Which approach fits, and why?

A) Kustomize, because a base plus overlays is simpler to understand
B) Helm, because a chart supplies a name, a required version, a fetchable location, and a declared set of values
C) Either — the choice is purely stylistic
D) Neither; cross-team distribution requires a GitOps agent

**5.** `[retrieval: ch13]` A cluster has no metrics-server and `kubectl top nodes` fails. Now that you have vocabulary for it, what does "install metrics-server" consist of?

A) Enabling a built-in Kubernetes feature gate on the API server
B) Applying a set of Kubernetes objects — a Deployment, Service, RBAC rules, an APIService — which somebody has packaged, commonly as a chart
C) Installing a binary on each node, since metrics collection is a node-level concern
D) Nothing; `kubectl top` works on any conformant cluster and the failure indicates a different problem

---

**Answers with Explanations**

**1. C.** Overlays reference the base and layer patches on top, managing customized configurations *without forking the originals* [source: kustomize-overview-2026-08-23]. **A is wrong** and is the most common wrong model: if it copied, you would be back at failure one from §1, with two directories drifting apart. **B is wrong**: an overlay that edited its base would make the base environment-specific, defeating the arrangement entirely. **D is wrong**, and it is the trap this whole section exists to disarm. Kustomize is explicitly a *template-free* way to customize configuration [source: kustomize-overview-2026-08-23]. There is no rendering step and no template engine.

**2. B.** Kustomize is built into kubectl as `apply -k` [source: kustomize-overview-2026-08-23], and kubectl has supported kustomization files since 1.14 [source: k8s-docs-kustomization-2026-08-31]. **A is half-true and wrong where it counts**: a standalone Kustomize binary does exist [source: k8s-docs-kustomization-2026-08-31], but it is not required for the kubectl-integrated path. **C inverts reality**: Helm is the one that needs a separate client. **D is wrong**; Kustomize is client-side, and nothing about it runs in the cluster.

**3. C.** There is no support at this time for upgrading or deleting CRDs using Helm [source: helm-crd-best-practices-2026-08-31]. **A is what most people expect and is the reason this trips teams up in production**: the release upgrades cleanly and the new capability silently is not there. **B is wrong**: the upgrade succeeds; it just skips the CRD. **D is wrong**, and it describes the catastrophic outcome the restriction exists to prevent.

**4. B.** Distribution to people who will not read your manifests is exactly what packaging is for: a required version [source: helm-glossary-2026-08-31], a fetchable location [source: helm-chart-repository-2026-08-31], and a declared surface of what they may change. **A is wrong**: simplicity is not the axis, and a Kustomize base gives a stranger no version to pin and no repository to fetch from. **C is wrong**; the choice turns on distribute-vs-adapt and has a defensible answer here. **D is wrong**: a delivery agent addresses *who applies it and when*, which is a different question and Chapter 15's *[cross-bearing: see Ch 15 §3 — push, or pull]*.

**5. B.** In a declarative system there is no installer; installation is applying objects somebody wrote *[cross-bearing: see Ch 13 §7 — metrics-server and the resource metrics pipeline]*. What this chapter added is the word for the packaged form of "objects somebody wrote." **A is wrong**: metrics-server is a separate component, not a feature gate, which is why `kubectl top` fails on a bare cluster in the first place. **C is wrong**: metrics-server is a Deployment that reads from the kubelets, not a per-node binary you install. **D is wrong**, and it is the misconception Chapter 13 named. `kubectl top` failing on a cluster without metrics-server is expected behavior, not a fault.

**If you scored 0–2:** Re-read **§5**, then the decision table in **§6**. The most common cause of a low score here is reading Kustomize as "Helm with different syntax," which makes every comparison question a coin flip.

**Checkpoint: You've Now Mastered**
✓ What an overlay does, and what it conspicuously does not do to its base
✓ Why Kustomize needs no engine installed
✓ What the Helm-vs-Kustomize choice actually turns on
✓ Why `crds/` exists, and the three limits on how it works

---

## ☀️ §7 — A Package, Not a Template

Here is the thing that has been true for the whole chapter, and is easiest to see now that both tools are in view.

**You have been comparing them at the wrong altitude.**

Helm and Kustomize disagree about mechanism as completely as two tools can. One makes the manifest incomplete and completes it from values. The other keeps the manifest complete and describes differences against it. One has a template engine; the other advertises the absence of a template engine as its headline feature [source: kustomize-overview-2026-08-23]. If mechanism were the axis, they would be opposites.

They agree about everything that matters. Both exist to take a directory of loose files and turn it into **one addressable unit**: a thing with a name, a thing that installs as a single act, a thing whose differences across environments are declared in one place rather than scattered through copies. They arrived at that goal from opposite directions and neither of them was aiming at templating. Templating is a thing Helm happens to use on the way.

Which means the argument the ecosystem spends so much energy on — templating versus not-templating, engine versus no-engine, Go templates versus patches — is an argument about *how*, conducted between two tools that had already agreed on *what*. And the *what* is the part that changes how you work.

<!-- FIGURE: ch14-zenith-package-not-template -->
```
        RENDER                                          PATCH
        ══════                                          ═════

   templates/ + values                          base/ + overlay/
          │                                            │
     ┌────┴────┐                                  ┌────┴────┐
     │ fill in │                                  │  merge  │
     │  holes  │                                  │  deltas │
     └────┬────┘                                  └────┬────┘
          │                                            │
          │        ┌──────────────────────┐            │
          └───────►│                      │◄───────────┘
                   │   ONE NAMED,         │
                   │   VERSIONED,         │
                   │   INSTALLABLE UNIT   │
                   │                      │
                   └──────────┬───────────┘
                              │
                              ▼
                        ┌──────────┐
                        │ cluster  │
                        └──────────┘

        The mechanisms could not be more different.
        The destination is the same one.
        The destination is the point.
```

That is what the subtitle meant. *A chart is not a release*: the package and the installation are different things, and collapsing them costs you the ability to say what is running where. *Templates are not the point*: they are one way of absorbing variation, and a tool exists that absorbs variation without them and solves the same problem anyway.

There is a nice symmetry in it with something you already know. Chapter 4 taught that a Kubernetes object is a *record of intent*, a durable declaration of what should be true, which controllers then work to make true *[cross-bearing: see Ch 4 §6 — a declaration, not an order]*. A package is that same move, one level up: a durable declaration of what a whole application should be, with a version number on it so you can say *which* declaration, and a name so you can ask what happened to it. Not a bigger object. The same idea applied to the set.

And now the question you cannot avoid, which this chapter has no way to answer.

You have a unit. It has a name, a version, and a place to be fetched from. It installs as one act and can be undone as one act.

**Who runs the install? When? Triggered by what? From where?**

Because so far the answer is: a person, at a keyboard, running a command. That person has cluster credentials on their laptop. They remember to do it, or they do not. They apply the version they think is current. Nothing checks whether the cluster still matches what was installed, and nothing notices when somebody else changes it by hand.

Packaging solved *what you hand over*. It solved nothing at all about *how it gets applied and stays applied*. That gap is where Chapter 15 lives, and it turns out the answer reaches back into the oldest idea in this book *[cross-bearing: see Ch 15 §3 — push, or pull]*.

---

## Exam Alert! 🚨

**High-Priority Topics**

1. **Chart, Helm release, release revision — three words, three things.** A chart is the package. A release is one installation of it [source: helm-architecture-2026-08-31]. A revision is one numbered state of that release [source: helm-glossary-2026-08-31]. One chart, many releases; one release, many revisions.
2. **`charts/` is not a chart repository.** `charts/` is a directory inside a chart holding its dependencies [source: helm-charts-2026-08-23]. A chart repository is an HTTP server housing packaged charts [source: helm-chart-repository-2026-08-31].
3. **Helm is a package manager, not a template engine** [source: helm-homepage-2026-08-31]. Templating is one mechanism inside it. Kustomize solves the same problem with no templating at all [source: kustomize-overview-2026-08-23], which is the cleanest available proof that templating was never the definition.
4. **Kustomize is built into kubectl** as `apply -k` [source: kustomize-overview-2026-08-23], and is template-free. Nothing to install; nothing rendered.

**Common Traps**

| The trap | The correct understanding |
|---|---|
| "Helm is a templating engine" | It is a package manager [source: helm-homepage-2026-08-31]. Chart → values → templates → **Helm release**. Templating is a means; the unit is the point. |
| Using "chart" and "release" interchangeably | One chart installs many times, each creating a separately named release, upgradable and rolled back independently [source: helm-charts-2026-08-23]. |
| Reading `charts/` as a chart repository | `charts/` holds dependency charts *inside* a chart [source: helm-charts-2026-08-23]. A repository is an HTTP server managed with `helm repo` [source: helm-chart-repository-2026-08-31]. |
| Assuming `helm rollback` runs `kubectl rollout undo` underneath | Different unit, different scope. `helm rollback` takes a release name [source: helm-rollback-cli-2026-08-31]; `kubectl rollout undo` takes one workload [source: k8s-docs-kubectl-rollout-2026-08-24]. |
| Reading chart version as the version of the software | The chart has its own SemVer version, required on every chart [source: helm-glossary-2026-08-31]. `appVersion` is the application's. They move independently. |
| Assuming Kustomize needs an engine installed | It is in kubectl [source: kustomize-overview-2026-08-23]. `kubectl apply -k` works on a stock installation. |
| Assuming an overlay edits or copies its base | It does neither — customization happens *without forking the originals* [source: kustomize-overview-2026-08-23]. |
| Expecting a chart upgrade to upgrade its CRDs | There is no support for upgrading or deleting CRDs with Helm [source: helm-crd-best-practices-2026-08-31]. The release upgrades; the CRD does not. |
| **"You have to run Tiller"** | **Helm 3 removed Tiller entirely** — "one of the first decisions we made regarding Helm 3 was to completely remove Tiller" [source: helm-changes-since-helm2-2026-08-31]. Material that describes installing or securing Tiller is describing a Helm that no longer exists. |

That last row deserves a sentence of its own, because it connects to something Chapter 1 warned you about. Tiller was Helm 2's in-cluster component, introduced so multiple operators could interact with the same set of releases; with RBAC enabled by default from Kubernetes 1.6, locking it down for production became difficult to manage, and the permissive default configuration could grant users a far broader range of permissions than intended [source: helm-changes-since-helm2-2026-08-31]. Helm 3 removed it, storing release records in Kubernetes directly and evaluating permissions through your kubeconfig instead [source: helm-changes-since-helm2-2026-08-31].

This domain doubled in weight under the current blueprint [source: lf-kcna-exam-page-2026-08-23], and a great deal of the freely available preparation material for it predates that change, some of it by a wide margin. Tiller is the clearest single marker: if a study resource explains how to secure Tiller, it was written for a Helm that has not existed since 2019, and you should be equally suspicious of everything else it tells you about this domain.

---

## Practice Questions

**1.** You run `kubectl apply -f manifests/` where the directory contains a CustomResourceDefinition and a custom resource that uses it. The custom resource is rejected. Why?

A) `kubectl apply` applies files alphabetically, and the resource sorted before the definition
B) The CRD declaration must be registered before any resources of its kind can be used, and applying a directory guarantees no ordering
C) Custom resources cannot be applied with `kubectl apply`; they require a controller
D) The CRD needs to be in a `crds/` directory for kubectl to recognize it

**2.** Which statement about `values.yaml` is correct?

A) It contains the rendered manifests that will be applied to the cluster
B) It holds the default configuration values for the chart, and defines what an installer may change
C) It is generated by Helm at install time from the `--set` flags
D) It is required only for charts that have subcharts

**3.** A chart directory contains `Chart.yaml`, `values.yaml`, `templates/`, and `charts/`. Which of these will *not* result in Kubernetes objects being created in your cluster?

A) `Chart.yaml`
B) `templates/`
C) `charts/`
D) `values.yaml`

E) Both A and D

**4.** In `templates/`, a file named `_helpers.tpl` is present. What is it for?

A) It contains helper Kubernetes objects created before the main templates
B) Files beginning with an underscore are not rendered to object definitions but are available for use within other templates
C) It stores the default values that `values.yaml` inherits from
D) It is the chart's test suite

**5.** You install the same chart twice with different release names in different namespaces. You then run `helm upgrade` on the first. What is the effect on the second?

A) It is upgraded too, since both track the same chart version
B) None — each release is upgraded and rolled back independently
C) It enters a pending state until it is also upgraded
D) It is uninstalled, since a chart may only have one active release per cluster

**6.** In Helm 3, where is a release's state stored by default?

A) In a Tiller pod in `kube-system`
B) In Secrets in the namespace of the release
C) In a local database on the machine running the Helm client
D) In etcd, under a Helm-specific prefix, bypassing the API server

**7.** `helm rollback my-app` is run with no revision argument. What happens?

A) The command errors, because a revision number is required
B) It rolls back to revision 1, the original installation
C) It rolls back to the previous release
D) It uninstalls the release entirely

**8.** Which is the clearest statement of how `helm rollback` differs from `kubectl rollout undo`?

A) `helm rollback` is faster because it does not perform a rolling update
B) `helm rollback` acts on a release — everything the chart installed — while `kubectl rollout undo` acts on a single workload object
C) They are equivalent; `helm rollback` is a wrapper around `kubectl rollout undo`
D) `kubectl rollout undo` acts on the whole namespace, while `helm rollback` acts on one Deployment

**9.** A team has a Deployment, a Service, a ConfigMap, and an Ingress, all installed together as one Helm release. A bad upgrade changed the Deployment's image and the ConfigMap's contents. Which single action returns all four objects to their prior state?

A) `kubectl rollout undo` on the Deployment
B) `helm rollback` on the release
C) `kubectl apply -f` with the old manifests
D) `kubectl rollout undo` on the Deployment plus a manual ConfigMap edit

**10.** `helm install` is run with no release name and no flags. What happens in Helm 3?

A) A name is auto-generated from the chart name
B) Helm throws an error, because a name is required
C) The chart name is used as the release name
D) The release is created in the `default` namespace with a random suffix

**11.** What is a chart repository?

A) A Git repository containing chart source files
B) An HTTP server housing an `index.yaml` file and optionally some packaged charts
C) A directory inside a chart holding its dependencies
D) A cluster-side component that serves charts to `helm install`

**12.** Why can an OCI registry store Helm charts?

A) Helm charts are internally structured as container images
B) The OCI Distribution Specification defines an API for distributing *content*, not specifically images, so registries can hold other artifacts
C) Helm converts charts to images at push time and back at pull time
D) It cannot; charts require a dedicated chart repository

**13.** A chart's `Chart.yaml` shows `version: 4.1.3` and `appVersion: 1.25.3`. The maintainer fixes a rendering bug in a template. Which number is expected to change in the next publish?

A) `appVersion`, to 1.25.4
B) `version`, to 4.1.4
C) Both, since they are kept in step
D) Neither; template fixes are published without a version change

**14.** What does the `namePrefix` field in a `kustomization.yaml` do?

A) Prepends a value to the names of all resources and references
B) Renames only the kustomization file's own metadata
C) Filters which resources from the base are included
D) Prepends a value to container image names

**15.** Which pair correctly describes Kustomize's two patch styles?

A) Strategic merge patch writes a fragment shaped like the object; JSON patch lists explicit operations on paths
B) Strategic merge patch operates on lists only; JSON patch operates on maps only
C) Strategic merge patch is server-side; JSON patch is client-side
D) Strategic merge patch requires a template engine; JSON patch does not

**16.** A team keeps their application manifests in their own Git repository, deploys to three clusters they administer, and has no external consumers. Which approach fits best, and why?

A) Helm, because versioning is always required
B) Kustomize, because there is nothing to distribute and the manifests stay readable as ordinary manifests
C) Helm, because three environments exceed what overlays can express
D) Neither; three environments require a service mesh

**17.** `[interleaved: D1.4]` You push a Helm chart to an OCI registry. Which statement about the reference is correct?

A) The reference must be prefixed with `oci://` and must not contain the basename or tag on push
B) The reference must include the chart's digest, since tags are not supported for charts
C) The reference is identical in form to a Helm repository URL
D) Charts pushed to OCI registries lose their version, which must be supplied at install time

---

**Answers with Explanations**

**1. B.** The declaration must be registered before any resources of that CRD's kinds can be used [source: helm-crd-best-practices-2026-08-31], and applying a directory makes no ordering promise. Failure two from §1, in its sharpest form. **A is wrong**: even if the ordering happened to be favorable, that would be luck, not a guarantee, and alphabetical ordering is not something `kubectl apply` undertakes. **C is wrong**; custom resources are applied exactly like any other object once their kind exists *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. **D is wrong**: `crds/` is a Helm chart convention [source: helm-crd-best-practices-2026-08-31], meaningless to bare kubectl.

**2. B.** `values.yaml` holds the default configuration values for the chart [source: helm-charts-2026-08-23], which is also the declared surface of what an installer may change. **A confuses values with rendered output**; the rendering happens from `templates/` combined with values [source: helm-charts-2026-08-23]. **C inverts the direction**: `--set` overrides `values.yaml`, merged with higher precedence [source: helm-using-helm-2026-08-31], not the reverse. **D is wrong**; values are how any chart, subcharts or not, absorbs variation.

**3. E (both A and D).** `Chart.yaml` carries the chart's identity [source: helm-glossary-2026-08-31] and `values.yaml` carries defaults [source: helm-charts-2026-08-23]; neither becomes an object. **B is wrong**: `templates/` combined with values generates valid manifests [source: helm-charts-2026-08-23], which is precisely how objects get created. **C is wrong**, and it is the interesting distractor: `charts/` holds dependency charts [source: helm-charts-2026-08-23], and installing the parent installs the subcharts, so objects absolutely do come from there.

**4. B.** Files whose names begin with an underscore are assumed not to have a manifest inside; they are not rendered to Kubernetes object definitions but are available everywhere within other chart templates [source: helm-named-templates-2026-08-31], and `_helpers.tpl` is the default location for template partials [source: helm-named-templates-2026-08-31]. **A is wrong**: nothing in `_helpers.tpl` becomes an object at all, let alone an early one. **C inverts the relationship**; values come from `values.yaml` and the command line [source: helm-using-helm-2026-08-31]. **D is wrong**: chart tests are a separate convention.

**5. B.** Each install creates a separately named release that can be upgraded and rolled back independently [source: helm-charts-2026-08-23]. **A is the chart/release collapse**; the chart has no installed state to propagate. **C is wrong**: nothing links the two releases' lifecycles. **D is wrong**, and it inverts Helm 3's actual behavior, which deliberately scoped release names to namespaces so the same name could be reused across them [source: helm-changes-since-helm2-2026-08-31].

**6. B.** In Helm 3, Secrets are the default storage driver [source: helm-changes-since-helm2-2026-08-31], and release information is stored in Secrets in the namespace of the release [source: helm-storage-backends-2026-08-31]. **A describes Helm 2**; Tiller was removed completely in Helm 3 [source: helm-changes-since-helm2-2026-08-31] and this is the single best marker of outdated material. **C is wrong**: state lives in the cluster, which is why any Helm client with the right kubeconfig sees the same releases. **D is wrong**; nothing writes to etcd directly, and the API server is the only door in *[cross-bearing: see Ch 3 §5 — the only door in]*.

**7. C.** If the revision argument is omitted or set to 0, it rolls back to the previous release [source: helm-rollback-cli-2026-08-31]. **A is wrong**; the argument is optional, with a documented default. **B is wrong**: revision 1 is a specific revision you would have to name. **D is wrong**; uninstalling is `helm uninstall`, a different operation entirely.

**8. B.** `helm rollback`'s first argument is a release name [source: helm-rollback-cli-2026-08-31]; `kubectl rollout undo` manages the rollout of a Deployment, DaemonSet, or StatefulSet [source: k8s-docs-kubectl-rollout-2026-08-24]. Different unit, different scope. **A is wrong on the mechanism**: a Helm rollback that changes a Pod template produces a rolling update as an ordinary consequence of reconciliation. **C is the trap this section exists to prevent**; neither calls the other. **D inverts both scopes.**

**9. B.** The release is the unit that contains all four objects, and rolling it back returns them together [source: helm-rollback-cli-2026-08-31]. **A is wrong** and is the single-object trap: it fixes the Deployment and leaves the ConfigMap wrong. **C might work** if you still have the old manifests and apply them correctly, but it is not a single action and it does not update Helm's release record, leaving the cluster and Helm's bookkeeping disagreeing. **D is A's problem plus manual work**, which is the state Helm exists to eliminate.

**10. B.** Helm 3 throws an error if no name is provided with `helm install` [source: helm-changes-since-helm2-2026-08-31]. **A describes Helm 2**, which auto-generated names, behavior that proved to be more of a nuisance than a helpful feature in production [source: helm-changes-since-helm2-2026-08-31]. You can still opt into it with `--generate-name` [source: helm-changes-since-helm2-2026-08-31]. **C and D are inventions**; neither is Helm's documented behavior.

**11. B.** A chart repository is an HTTP server that houses an `index.yaml` file and optionally some packaged charts [source: helm-chart-repository-2026-08-31]. **A is wrong**: a repository serves packaged charts over HTTP, not source files over Git, though Git is where chart source often lives. **C describes `charts/`** [source: helm-charts-2026-08-23], the confusion this chapter names twice. **D is wrong**; nothing cluster-side is involved. Any HTTP server that serves YAML and tar files and answers GET requests will do [source: helm-chart-repository-2026-08-31].

**12. B.** The OCI Distribution Specification defines an API protocol to facilitate and standardize the distribution of *content* [source: oci-distribution-spec-2026-08-24], and since OCI artifacts make it possible to store more than container images, a single registry can hold charts, images, and other artifacts [source: helm-blog-oci-ga-2026-08-31]. **A is wrong**: a chart is a tarred and gzipped chart directory [source: helm-glossary-2026-08-31], not an image. **C is wrong**; no conversion happens, and the registry stores the artifact as an artifact. **D is wrong**: Helm has supported this since 3.8.0 [source: helm-blog-oci-ga-2026-08-31] and now recommends it [source: helm-oci-registries-2026-08-31].

**13. B.** The chart's own SemVer version tracks the packaging, and a template fix is a packaging change. **A is wrong**: `appVersion` is the version of the application being installed, which did not change. **C is wrong**; nothing requires them to move together, and forcing it would mean lying about the application version. **D is wrong**: charts are versioned according to SemVer 2 with a version required on every chart [source: helm-glossary-2026-08-31], so a published change gets one.

**14. A.** `namePrefix` prepends the value to the names of all resources *and references* [source: kubectl-book-kustomization-fields-2026-08-31]. That "and references" clause is the load-bearing part: a prefixed Deployment still finds its prefixed ConfigMap. **B is wrong**; the transformation applies to the resources, not to the kustomization's own metadata. **C describes `resources`.** **D describes `images`**, which modifies name, tags, and/or digest for images [source: kubectl-book-kustomization-fields-2026-08-31].

**15. A.** `patchesStrategicMerge` patches using the strategic merge patch standard and `patchesJson6902` using the JSON 6902 standard [source: kubectl-book-kustomization-fields-2026-08-31]; a strategic merge patch is a fragment shaped like the object, and a JSON patch is a list of operations on paths. **B is an invented split**: both handle maps, and lists are precisely where JSON patch is often preferred. **C is wrong**; Kustomize renders client-side, and the server sees ordinary objects. **D is wrong**, and it contradicts the tool's headline property: Kustomize is template-free [source: kustomize-overview-2026-08-23].

**16. B.** Nothing is being distributed, the manifests are the team's own, and a Kustomize base stays readable as ordinary manifests with overlays declaring only deltas [source: kustomize-overview-2026-08-23]. **A is wrong**: a required version is valuable *for a stranger who must pin something*, and Git supplies identity for a team's own repository. **C is wrong**; overlays are explicitly designed for managing any number of distinctly customized configurations [source: kustomize-overview-2026-08-23]. **D is a non sequitur**: a mesh addresses service-to-service traffic, not configuration management *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*.

**17. A.** When using `helm push`, the reference must be prefixed with `oci://` and must not contain the basename or tag [source: helm-oci-registries-2026-08-31]. **B is wrong**: the tag is inferred from the chart's semantic version [source: helm-oci-registries-2026-08-31], so tags very much apply. **C is wrong**; the `oci://` prefix is exactly what distinguishes the two forms. **D is wrong**: the version is what the tag is derived from [source: helm-oci-registries-2026-08-31], so it travels with the chart rather than being supplied later.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **The four failures** | A folder of manifests cannot handle environment variation, cannot guarantee apply ordering, has no version, and cannot be handed to a stranger. Everything in this chapter answers one of these four. |
| **Chart** | A collection of files describing a related set of Kubernetes resources, laid out in a directory tree, packageable into versioned archives. The unit. |
| **`Chart.yaml`** | The chart's identity. Required on every chart, and a version number is required in it. |
| **`values.yaml`** | The declared surface of variation — what an installer may change, with a working default for each. |
| **`templates/`** | Combined with values, generates valid Kubernetes manifests. Files starting with `_` are partials, not objects. |
| **`charts/`** | Dependency charts *inside* this chart. **Not a repository.** |
| **`crds/`** | Not templated, installed first. Solves the one ordering failure that is fatal rather than slow. Cannot be upgraded by Helm. |
| **Helm release** | One installed instance of a chart, named, scoped to a namespace. One chart installs many times; each release upgrades and rolls back independently. |
| **Release revision** | One numbered state of a release. `helm rollback <release> <revision>`; omit the revision to go back one. |
| **`helm rollback` vs `kubectl rollout undo`** | Different unit (release vs one workload), different scope (everything the chart installed vs one Pod template), different bookkeeping. Neither calls the other. |
| **Chart repository** | An HTTP server housing `index.yaml` and packaged charts. Managed with `helm repo`. |
| **OCI registry as chart store** | The distribution spec standardized *content*, not images. Charts, images, and other artifacts in one registry. |
| **version vs appVersion** | The box vs what's in the box. They move independently. |
| **Kustomize** | Template-free customization, built into kubectl as `apply -k`. Nothing to install. |
| **Base and overlay** | The base is never edited and never copied. Overlays declare only their deltas and point at the base. |
| **The decision** | Distributing to strangers who will not read it → Helm. Adapting what you already have → Kustomize. |
| **Tiller** | Removed in Helm 3. Any material that explains securing it predates 2019. |
| **☀️ The Zenith** | Two tools that disagree completely about mechanism and agree completely about goal: turn a directory into one named, versioned, installable unit. The unit is the point; the templating argument is about *how*. |

---

## 🏆 Safe Harbor

Part IV opened with a debt thirteen chapters deep, and you have now collected on it. When a chapter told you to install a CNI plugin, an Ingress controller, a CSI driver, metrics-server, you now know exactly what that sentence was hiding, and you have the vocabulary to say what it should have said instead.

More than that: you can now read a stranger's `deploy/` directory and diagnose it. Which of the four failures is this directory living with? Is anything marked as variable? Is there a version? Could you hand this to a colleague on another team without a phone call? Those are not academic questions. They are the questions that decide whether an application is shippable, and until this chapter you did not have a way to ask them.

---

## The Voyage Ahead

You have a unit now. The hard part, turning a pile of files into one named, versioned, installable thing, is behind you.

And it has bought you less than it should have, because the unit still gets applied by a person. Somebody with cluster credentials on their laptop, running a command, from a machine nobody audits, at a moment nobody records. They apply the version they believe is current. Afterward, nothing watches. If someone edits an object by hand next Tuesday, the cluster and the package quietly stop agreeing, and no one finds out until the next deploy overwrites the fix or the fix overwrites the deploy.

The next chapter is about closing that gap, and about a question that sounds procedural and is not: **should the pipeline push changes into the cluster, or should something inside the cluster pull them?** The answer reshapes where your credentials live, how large a mistake can get before something catches it, and what "the truth" even means about a running system.

It also brings you back, one last time, to the oldest idea in this book, the one from Chapter 3 that has been quietly underneath everything since. You have seen the control loop reconcile a Deployment toward its spec, a scheduler toward a placement, a claim toward a volume. Chapter 15 points it at a Git repository, and the recognition when that lands is the one this book has been saving.

> *"The chart is what you meant. The cluster is what happened. The interesting question is who keeps them the same."*
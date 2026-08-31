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

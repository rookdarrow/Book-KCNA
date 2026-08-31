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

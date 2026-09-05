---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_cp/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), generated CLI reference (auto-generated from the kubectl Go source), CC BY 4.0 — fetched as the raw markdown source from kubernetes/website, main branch (content/en/docs/reference/kubectl/generated/kubectl_cp/_index.md)"
objectives_covered: ["D3.2"]
concepts_covered: ["kubectl-cp", "kubectl-cp-requires-tar"]
---

# kubectl cp (generated CLI reference)

"Copy files and directories to and from containers."

From the examples block, verbatim:

```
  # !!!Important Note!!!
  # Requires that the 'tar' binary is present in your container
  # image.  If 'tar' is not present, 'kubectl cp' will fail.
  #
  # For advanced use cases, such as symlinks, wildcard expansion or
  # file mode preservation, consider using 'kubectl exec'.

  # Copy /tmp/foo local file to /tmp/bar in a remote pod in namespace <some-namespace>
  tar cf - /tmp/foo | kubectl exec -i -n <some-namespace> <some-pod> -- tar xf - -C /tmp/bar

  # Copy /tmp/foo from a remote pod to /tmp/bar locally
  kubectl exec -n <some-namespace> <some-pod> -- tar cf - /tmp/foo | tar xf - -C /tmp/bar
```

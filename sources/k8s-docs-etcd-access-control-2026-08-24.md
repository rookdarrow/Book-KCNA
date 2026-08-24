---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/"
fetched_at: "2026-08-24T03:14:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Administration"]
concepts_covered: ["etcd", "etcd-access", "api-server-as-front-end", "control-plane"]
---
# Operating etcd clusters for Kubernetes - definition and access control (kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

> **Snapshot note.** This snapshot COMPLEMENTS and does not supersede
> `k8s-docs-etcd-backup-2026-08-23.md`, which covers the backup/restore portion of the SAME page.
> Two snapshots share this source_url by design: the 08-23 file carries the Chapter 8
> backup material, this 08-24 file carries the two sentences Chapter 3 sec.2/sec.5 depend on.
> Only sentences verified character-for-character against the rendered page are transcribed here.
> The page's TLS configuration guidance (peer/client certs, --client-cert-auth, --trusted-ca-file)
> was NOT transcribed - it is Chapter 8 material and was not verbatim-verified in this pass.

Opening definition:

"etcd is a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data."

From the securing/access-control guidance:

"Access to etcd is equivalent to root permission in the cluster so ideally only the API server should have access to it."

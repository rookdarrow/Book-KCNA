---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Administration"]
concepts_covered: ["etcd-backup", "snapshot", "etcdctl", "etcdutl", "disaster-recovery"]
---
# Operating etcd clusters for Kubernetes — backup and restore (kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

All Kubernetes objects are stored in etcd. Periodically backing up the etcd cluster data is important to recover Kubernetes clusters under disaster scenarios, such as losing all control plane nodes. The snapshot file contains all the Kubernetes state and critical information; keep it encrypted and store it outside the control plane nodes. Backing up an etcd cluster can be accomplished in two ways: a built-in snapshot (`etcdctl snapshot save backup.db`, optionally with --endpoints, --cacert, --cert and --key for a TLS-protected cluster), or a volume snapshot of etcd's storage. Restoring a cluster from a snapshot uses `etcdutl snapshot restore`, which operates directly on the etcd data files; after a restore, the control plane components are restarted against the restored data directory.

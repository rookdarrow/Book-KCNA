---
source_url: "https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1 Administration"]
concepts_covered: ["namespace", "default", "kube-system", "kube-public", "kube-node-lease", "namespaced-vs-cluster-scoped", "service-dns"]
---
# Namespaces (kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

In Kubernetes, namespaces provide a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc.) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc.).

## When to use multiple namespaces
Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, you should not need to create or think about namespaces at all. Start using namespaces when you need the features they provide. Namespaces provide a scope for names. Namespaces cannot be nested inside one another and each Kubernetes resource can only be in one namespace. Namespaces are a way to divide cluster resources between multiple users (via resource quota). It is not necessary to use multiple namespaces to separate slightly different resources, such as different versions of the same software: use labels to distinguish resources within the same namespace. For a production cluster, consider not using the default namespace. Instead, make other namespaces and use those.

## Initial namespaces
- default — Kubernetes includes this namespace so that you can start using your new cluster without first creating a namespace.
- kube-node-lease — This namespace holds Lease objects associated with each node. Node leases allow the kubelet to send heartbeats so that the control plane can detect node failure.
- kube-public — This namespace is readable by all clients (including those not authenticated). This namespace is mostly reserved for cluster usage, in case that some resources should be visible and readable publicly throughout the whole cluster. The public aspect of this namespace is only a convention, not a requirement.
- kube-system — The namespace for objects created by the Kubernetes system.

## Namespaces and DNS
When you create a Service, it creates a corresponding DNS entry. This entry is of the form <service-name>.<namespace-name>.svc.cluster.local, which means that if a container only uses <service-name>, it will resolve to the service which is local to a namespace. If you want to reach across namespaces, you need to use the fully qualified domain name (FQDN). All namespace names must be valid RFC 1123 DNS labels.

## Not all objects are in a namespace
Most Kubernetes resources (e.g. pods, services, replication controllers, and others) are in some namespaces. However namespace resources are not themselves in a namespace. And low-level resources, such as nodes and persistentVolumes, are not in any namespace. `kubectl api-resources --namespaced=true` / `--namespaced=false` lists which resources are and aren't namespaced.

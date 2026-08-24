---
source_url: "https://kubernetes.io/docs/reference/kubectl/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Administration", "D2 Troubleshooting"]
concepts_covered: ["kubectl", "kubeconfig", "kubectl-syntax", "get", "describe", "apply", "create", "delete", "logs", "exec", "scale", "rollout", "explain"]
---
# Command line tool (kubectl) (kubernetes.io/docs/reference/kubectl/)

Kubernetes provides a command line tool for communicating with a Kubernetes cluster's control plane, using the Kubernetes API. For configuration, kubectl looks for a file named config in the $HOME/.kube directory. You can specify other kubeconfig files by setting the KUBECONFIG environment variable or by setting the --kubeconfig flag.

## Syntax
kubectl [command] [TYPE] [NAME] [flags] — command specifies the operation that you want to perform on one or more resources, for example create, get, describe, delete. TYPE specifies the resource type; resource types are case-insensitive and you can specify the singular, plural, or abbreviated forms. NAME specifies the name of the resource; names are case-sensitive; if the name is omitted, details for all resources are displayed. flags specifies optional flags; flags that you specify from the command line override default values and any corresponding environment variables.

## In-cluster authentication and namespace overrides
By default kubectl will first determine if it is running within a pod, and thus in a cluster. It starts by checking for the KUBERNETES_SERVICE_HOST and KUBERNETES_SERVICE_PORT environment variables and the existence of a service account token file at /var/run/secrets/kubernetes.io/serviceaccount/token. If all three are found in-cluster authentication is assumed. When kubectl runs in a cluster it acts against the namespace of the ServiceAccount unless --namespace is given.

## Operations
- get — List one or more resources.
- describe — Display the detailed state of one or more resources.
- apply — Apply a configuration change to a resource from a file or stdin.
- create — Create one or more resources from a file or stdin.
- delete — Delete resources either from a file, stdin, or specifying label selectors, names, resource selectors, or resources.
- logs — Print the logs for a container in a pod.
- exec — Execute a command against a container in a pod.
- scale — Update the size of the specified replication controller / deployment.
- rollout — Manage the rollout of a resource. Valid resource types include deployments, daemonsets and statefulsets.
- explain — Get documentation of various resources (pods, nodes, services, etc.).
- config — Modifies kubeconfig files.

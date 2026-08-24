---
source_url: "https://kubernetes.io/docs/concepts/security/service-accounts/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Security", "D1 Core Concepts"]
concepts_covered: ["serviceaccount", "default-serviceaccount", "tokenrequest", "projected-token", "workload-identity"]
---
# Service Accounts (kubernetes.io/docs/concepts/security/service-accounts/)

A service account is a type of non-human account that, in Kubernetes, provides a distinct identity in a Kubernetes cluster. Application Pods, system components, and entities inside and outside the cluster can use a specific ServiceAccount's credentials to identify as that ServiceAccount. Service accounts exist as ServiceAccount objects in the API server. Service accounts are namespaced (bound to a Kubernetes namespace; every namespace gets a default ServiceAccount upon creation), lightweight, and portable. Service accounts are different from user accounts, which are authenticated human users in the cluster; by default, user accounts don't exist in the Kubernetes API server.

## Default service accounts
When you create a cluster, Kubernetes automatically creates a ServiceAccount object named default for every namespace in your cluster. The default service accounts in each namespace get no permissions by default other than the default API discovery permissions that Kubernetes grants to all authenticated principals if RBAC is enabled. If you delete the default ServiceAccount object in a namespace, the control plane replaces it with a new one. If you deploy a Pod in a namespace, and you don't manually assign a ServiceAccount to the Pod, Kubernetes assigns the default ServiceAccount for that namespace to the Pod.

## Use cases
Your Pods need to communicate with the Kubernetes API server (reading Secrets, cross-namespace access); your Pods need to communicate with an external service that requires an identity; authenticating to a private image registry using an imagePullSecret; an external service needs to communicate with the Kubernetes API server (CI/CD pipelines); you use third-party security software that relies on the ServiceAccount identity of different Pods to group those Pods into different contexts.

## How to use
Create a ServiceAccount object; grant permissions to it using an authorization mechanism such as RBAC; assign the ServiceAccount to Pods during creation via spec.serviceAccountName.

## Authenticating credentials
In Kubernetes v1.22 and later, Kubernetes gets a short-lived, automatically rotating token using the TokenRequest API and mounts the token as a projected volume. Recommended: the TokenRequest API or token volume projection. Not recommended: long-lived ServiceAccount token Secrets, which don't expire or rotate and pose a security risk.

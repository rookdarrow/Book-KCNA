---
source_url: "https://kubernetes.io/docs/concepts/cluster-administration/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Administration", "D2 Security"]
concepts_covered: ["planning-a-cluster", "managed-vs-self-hosted", "node-management", "resource-quota", "certificates", "authentication", "authorization", "admission-controllers", "auditing", "tls-bootstrapping"]
---
# Cluster Administration (kubernetes.io/docs/concepts/cluster-administration/)

## Planning a cluster
Before choosing a guide, consider: Do you want to try out Kubernetes on your computer, or do you want to build a high-availability, multi-node cluster? Will you be using a hosted Kubernetes cluster, such as Google Kubernetes Engine, or hosting your own cluster? Will your cluster be on-premises, or in the cloud (IaaS)? If you are configuring Kubernetes on-premises, consider which networking model fits best. Will you be running Kubernetes on "bare metal" hardware or on virtual machines (VMs)? Do you want to run a cluster, or do you expect to do active development of Kubernetes project code? Familiarize yourself with the components needed to run a cluster.

## Managing a cluster
Learn how to manage nodes, including node autoscaling. Learn how to set up and manage the resource quota for shared clusters.

## Securing a cluster
Generate Certificates; Kubernetes Container Environment; Controlling Access to the Kubernetes API; Authenticating; Authorization; Using Admission Controllers; Admission Webhook Good Practices; Using Sysctls in a Kubernetes Cluster; Auditing.

## Securing the kubelet
Control Plane-Node communication; TLS bootstrapping; Kubelet authentication/authorization.

## Optional cluster services
DNS Integration — describes how to resolve a DNS name directly to a Kubernetes service. Logging and Monitoring Cluster Activity — explains how logging in Kubernetes works and how to implement it.

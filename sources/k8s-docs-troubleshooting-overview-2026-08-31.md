---
source_url: "https://kubernetes.io/docs/tasks/debug/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["platform-scope-vs-application-scope", "triage-flow", "release-known-issues"]
load_bearing: "This is the official statement of the two-audience split that sec.1 owns, and the official warrant for sec.6's 'release-specific known issues as a legitimate triage step'."
---
# Monitoring, Logging, and Debugging (Troubleshooting overview)

> All passages below are **[VERBATIM]**.

> "Set up monitoring and logging to troubleshoot a cluster, or debug a containerized application."

> "Sometimes things go wrong. This guide helps you gather the relevant information and resolve issues. It has four sections:"

> "**Debugging your application** - Useful for users who are deploying code into Kubernetes and wondering why it is not working."

> "**Debugging your cluster** - Useful for cluster administrators and operators troubleshooting issues with the Kubernetes cluster itself."

> "**Logging in Kubernetes** - Useful for cluster administrators who want to set up and manage logging in Kubernetes."

> "**Monitoring in Kubernetes** - Useful for cluster administrators who want to enable monitoring in a Kubernetes cluster."

> **"You should also check the known issues for the release you're using."**
> (links to https://github.com/kubernetes/kubernetes/releases)

## Getting help — scope routing

> "If you have questions related to *software development* for your containerized app, you can ask those on Stack Overflow."

> "If you have Kubernetes questions related to *cluster management* or *configuration*, you can ask those on Server Fault."

## Bugs and feature requests

> "If you have what looks like a bug, or you would like to make a feature request, please use the GitHub issue tracking system."

> "If filing a bug, please include detailed information about how to reproduce the problem, such as:
> - Kubernetes version: `kubectl version`
> - Cloud provider, OS distro, network configuration, and container runtime version
> - Steps to reproduce the problem"

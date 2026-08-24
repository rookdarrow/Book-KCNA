---
source_url: "https://kubernetes.io/docs/tasks/debug/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Troubleshooting", "D3 Debugging"]
concepts_covered: ["debugging-applications", "debugging-clusters", "logging-architecture", "resource-metrics-pipeline", "kubectl-debug"]
---
# Monitoring, Logging, and Debugging (kubernetes.io/docs/tasks/debug/)

Sometimes things go wrong. This guide is aimed at making them right. It has two sections: Debugging your application — useful for users who are deploying code into Kubernetes and wondering why it is not working; Debugging your cluster — useful for cluster administrators and people whose Kubernetes cluster is unhappy.

- **Troubleshooting Applications** — debugging Pods, Services, StatefulSets, determining the reason for Pod failure, debugging Init Containers and running Pods.
- **Troubleshooting Clusters** — troubleshooting kubectl; the resource metrics pipeline; tools for monitoring resources; monitor node health; debugging Kubernetes nodes with crictl; auditing; developing and debugging services locally.
- **Resource metrics pipeline** — collects and aggregates resource-usage metrics from Kubelets (metrics-server) for kubectl top and autoscaling.
- **Logging Architecture** — how Kubernetes handles cluster and application logs; native logging patterns and integrating logging systems.
- **kubectl debugging tools** — kubectl debug and other diagnostic tools.

You should also check the known issues for the release you're using.

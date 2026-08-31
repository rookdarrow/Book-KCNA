---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["resource-metrics-pipeline", "metrics-server", "kubectl-top"]
supersedes_note: "Fuller than k8s-docs-resource-metrics-pipeline-2026-08-23.md (2.2KB). sec.7 is the definition home for metrics-server and Ch 17 sec.7 / Ch 18 sec.3 both refer back to it, so the definition must be complete enough to be referred to rather than re-derived -- cite THIS file."
---
# Resource metrics pipeline

> All passages below are **[VERBATIM]**.

> "For Kubernetes, the *Metrics API* offers a basic set of metrics to support automatic scaling and similar use cases. This API makes information available about resource usage for node and pod, including metrics for CPU and memory. If you deploy the Metrics API into your cluster, clients of the Kubernetes API can then query for this information, and you can use Kubernetes' access control mechanisms to manage permissions to do so."

> "The HorizontalPodAutoscaler (HPA) and VerticalPodAutoscaler (VPA) use data from the metrics API to adjust workload replicas and resources to meet customer demand."

> "You can also view the resource metrics using the `kubectl top` command."

> Note: "The Metrics API, and the metrics pipeline that it enables, only offers the minimum CPU and memory metrics to enable automatic scaling using HPA and / or VPA. If you would like to provide a more complete set of metrics, you can complement the simpler Metrics API by deploying a second metrics pipeline that uses the *Custom Metrics API*."

## The architecture components

> "The architecture components, from right to left in the figure, consist of the following:"

> "**cAdvisor**: Daemon for collecting, aggregating and exposing container metrics included in Kubelet."

> "**kubelet**: Node agent for managing container resources. Resource metrics are accessible using the `/metrics/resource` and `/stats` kubelet API endpoints."

> "**node level resource metrics**: API provided by the kubelet for discovering and retrieving per-node summarized stats available through the `/metrics/resource` endpoint."

> "**metrics-server**: Cluster addon component that collects and aggregates resource metrics pulled from each kubelet. The API server serves Metrics API for use by HPA, VPA, and by the `kubectl top` command. Metrics Server is a reference implementation of the Metrics API."

> "**Metrics API**: Kubernetes API supporting access to CPU and memory used for workload autoscaling. To make this work in your cluster, you need an API extension server that provides the Metrics API."

The rendered figure shows the flow: `Container runtime -> cAdvisor -> kubelet -> (node level resource metrics) -> Metrics-Server -> (metrics API) -> API server -> HPA`, with `API server -> kubectl top` as a separate consumer.

## Metrics API

> "The metrics-server implements the Metrics API. This API allows you to access CPU and memory usage for the nodes and pods in your cluster. Its primary role is to feed resource usage metrics to K8s autoscaler components."

> "Here is an example of the Metrics API request for a `minikube` node piped through `jq` for easier reading:"

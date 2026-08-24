---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D4 Observability", "D2 Troubleshooting"]
concepts_covered: ["metrics-server", "metrics-api", "kubectl-top", "cadvisor", "kubelet-metrics", "hpa-inputs"]
---
# Resource metrics pipeline (kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/)

For Kubernetes, the Metrics API offers a basic set of metrics to support automatic scaling and similar use cases. This API makes information available about resource usage for node and pod, including metrics for CPU and memory. If you deploy the Metrics API into your cluster, clients of the Kubernetes API can then query for this information, and you can use Kubernetes' access control mechanisms to manage permissions to do so. The HorizontalPodAutoscaler (HPA) and VerticalPodAutoscaler (VPA) use data from the metrics API to adjust workload replicas and resources to meet customer demand. You can also view the resource metrics using the `kubectl top` command.

## Metrics API
The metrics-server implements the Metrics API (metrics.k8s.io/v1beta1) and provides access to CPU and memory usage for nodes and pods in your cluster. Its primary role is to feed resource usage metrics to K8s autoscaler components.

## Metrics Server
The metrics-server fetches resource metrics from the kubelets and exposes them in the Kubernetes API server through the Metrics API for use by the HPA and VPA. It is a cluster addon component (not deployed by default in all distributions). It discovers all nodes on the cluster and queries each node's kubelet for CPU and memory usage; the kubelet collects the stats through cAdvisor, a daemon for collecting, aggregating, and exposing container metrics which is included as part of the kubelet binary. Metrics Server is meant only for autoscaling purposes — for example, don't use it to forward metrics to monitoring solutions, or as a source of monitoring solution metrics; in such cases collect metrics from the kubelet /metrics/resource endpoint directly.

---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/"
fetched_at: "2026-08-31T09:35:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["service-selector-mismatch", "empty-endpointslice-as-symptom", "port-versus-targetport", "service-dns-name-shape", "kubectl-get-endpointslices", "kubectl-describe-service"]
transcription: "verbatim"
transcription_note: "Transcribed from the CC BY 4.0 markdown source at kubernetes/website (content/en/docs/tasks/debug/debug-application/debug-service.md, main branch). TRIMMED ON-TOPIC: the iptables-save and ipvsadm dumps under 'Is the kube-proxy working?' are omitted — that is platform scope, owned by Ch 9 and Ch 13, and outside Ch 16 section 4. Everything bearing on selectors, ports, DNS and EndpointSlices is complete. A stray Hugo `{{< note >}}` shortcode in the source is preserved as a plain Note line."
---
# Debug Services

> All passages below are **[VERBATIM]**.

## Running commands in a Pod

> "For many steps here you will want to see what a Pod running in the cluster sees. The simplest way is to run an interactive busybox Pod:"

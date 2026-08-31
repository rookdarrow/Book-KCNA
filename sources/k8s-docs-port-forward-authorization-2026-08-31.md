---
source_url: "https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/"
fetched_at: "2026-08-31T09:52:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["service-path-versus-api-path", "port-forward-as-diagnostic"]
transcription: "verbatim"
transcription_note: "The 'Authorization and security considerations' section of the port-forward page, isolated because it is the load-bearing evidence for Ch 16 section 5's claim that port-forward travels the API-server path rather than the Service path. Retrieved by a targeted fetch that was instructed to report NO SUCH SECTION if absent; it returned these three sentences."
significance: "The `pods/portforward` SUBRESOURCE is the authoritative evidence that port-forward is an API-server operation, and 'may bypass network-level controls' is the closest the docs come to stating section 5's inference outright. See manifest Notes item 4 — the full path (API server -> kubelet -> Pod) is still NOT stated on any page found."
---
# Use Port Forwarding to Access Applications in a Cluster — Authorization

> All passages below are **[VERBATIM]**, from the section headed "Authorization and security considerations".

> "Access to `kubectl port-forward` is controlled by Kubernetes authorization mechanisms like Role-Based Access Control (RBAC)."

> "To use `kubectl port-forward`, a user must have permission to access the target resource (for example, a Pod or Service) and the `portforward` subresource. Typical required permissions include `get` on `pods` and `create` on `pods/portforward`."

> "Cluster administrators should carefully restrict these permissions, as port-forwarding can provide direct network access to workloads and may bypass network-level controls."

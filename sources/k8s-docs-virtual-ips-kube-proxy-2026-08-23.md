---
source_url: "https://kubernetes.io/docs/reference/networking/virtual-ips/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Networking"]
concepts_covered: ["kube-proxy", "virtual-ip", "proxy-modes", "iptables", "ipvs", "nftables", "kernelspace"]
---
# Virtual IPs and Service Proxies (kubernetes.io/docs/reference/networking/virtual-ips/)

Every node in a Kubernetes cluster runs a kube-proxy (unless you have deployed your own alternative component in place of kube-proxy). The kube-proxy component is responsible for implementing a virtual IP mechanism for Services of type other than ExternalName. Each instance of kube-proxy watches the Kubernetes control plane for the addition and removal of Service and EndpointSlice objects. For each Service, kube-proxy calls appropriate APIs (depending on the kube-proxy mode) to configure the node to capture traffic to the Service's clusterIP and port, and redirect that traffic to one of the Service's endpoints (usually a Pod, but possibly an arbitrary user-provided IP address). A control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server.

## Proxy modes
On Linux nodes, the available modes for kube-proxy are: iptables — a mode where the kube-proxy configures packet forwarding rules using iptables (the default); ipvs — a mode where the kube-proxy configures packet forwarding rules using ipvs; nftables — a mode where the kube-proxy configures packet forwarding rules using nftables (GA since Kubernetes 1.33). There is only one mode available for kube-proxy on Windows: kernelspace — a mode where the kube-proxy configures packet forwarding rules in the Windows kernel.

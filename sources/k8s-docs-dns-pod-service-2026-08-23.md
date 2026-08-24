---
source_url: "https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Networking"]
concepts_covered: ["cluster-dns", "coredns", "service-dns-record", "headless-dns", "srv-record", "pod-dns-record", "dnspolicy", "clusterfirst"]
---
# DNS for Services and Pods (kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

Kubernetes creates DNS records for Services and Pods. You can contact Services with consistent DNS names instead of IP addresses. Kubernetes publishes information about Pods and Services which is used to program DNS. The kubelet configures Pods' DNS so that running containers can look up Services by name rather than IP. Services defined in the cluster are assigned DNS names. By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain. CoreDNS is the cluster DNS addon that serves these records.

## Services
Normal (not headless) Services are assigned DNS A and/or AAAA records, depending on the IP family of the Service, with a name of the form my-svc.my-namespace.svc.cluster-domain.example. This resolves to the cluster IP of the Service. Headless Services (without a cluster IP) are also assigned DNS A and/or AAAA records with the same name form; unlike normal Services, this resolves to the set of IPs of all of the Pods selected by the Service. Clients are expected to consume the set or else use standard round-robin selection from the set. SRV records are created for named ports that are part of normal or headless Services: _port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example.

## Pods
In general a Pod has the DNS resolution of the form pod-ipv4-address.my-namespace.pod.cluster-domain.example (for example, 172-17-0-3.default.pod.cluster.local). The Pod spec has optional hostname and subdomain fields; when both are set and a headless Service exists with the same name as the subdomain, the Pod's FQDN is hostname.subdomain.namespace.svc.cluster-domain.example.

## Pod's DNS policy
dnsPolicy values: Default — the Pod inherits the name resolution configuration from the node that the Pods run on. ClusterFirst — any DNS query that does not match the configured cluster domain suffix is forwarded to an upstream nameserver by the DNS server; this is the default policy if dnsPolicy is not explicitly specified. ClusterFirstWithHostNet — for Pods running with hostNetwork, so that cluster DNS still applies. None — the Pod ignores DNS settings from the Kubernetes environment; all DNS settings are supplied via the dnsConfig field.

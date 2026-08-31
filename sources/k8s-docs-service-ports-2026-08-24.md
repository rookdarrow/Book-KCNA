---
source_url: "https://kubernetes.io/docs/concepts/services-networking/service/"
fetched_at: "2026-08-24T14:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.1", "D2 Networking"]
concepts_covered: ["service-port", "target-port", "node-port", "named-port", "nodeport-range", "service-type-ladder", "clusterip"]
---
# Service — port mechanics and the NodePort range (kubernetes.io/docs/concepts/services-networking/service/)

> **Snapshot note.** Companion snapshot to `k8s-docs-service-2026-08-23.md`, which cached
> this page at a shallower depth (Service definition, the four types, headless Services,
> Services without selectors). Fetched to resolve Chapter 9 § Open questions **#3** — the
> port-mechanics decision — in favour of option (a).
>
> Scope: `port` / `targetPort` / `nodePort` and the default node-port range **only**.
> Deliberately NOT transcribed, per the outline's §3 scope guards: `sessionAffinity`,
> external traffic policies, `allocateLoadBalancerNodePorts`, multi-port Services beyond the
> named-port example, protocol handling, and traffic-distribution fields.
>
> **⚠ TRANSCRIPTION CONFIDENCE.** Two independent extractions of the "supersets" sentence and
> of the three-port-field list returned slightly different wording. Both variants are
> recorded below under "Transcription variance". **Re-verify against the live page before
> quoting either verbatim in the book.** Everything else in this file was returned
> identically across extractions.

## Defining a Service — port and targetPort

A Service can map _any_ incoming `port` to a `targetPort`. By default and for convenience, the `targetPort` is set to the same value as the `port` field.

## Named ports

Port definitions in Pods have names, and you can reference these names in the `targetPort` attribute of a Service.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app.kubernetes.io/name: proxy
  ports:
  - name: name-of-service-port
    protocol: TCP
    port: 80
    targetPort: http-web-svc
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app.kubernetes.io/name: proxy
spec:
  containers:
  - name: nginx
    image: nginx:stable
    ports:
      - containerPort: 80
        name: http-web-svc
```

This works even if there is a mixture of Pods in the Service using a single configured name, with the same network protocol available via different port numbers.

## type: NodePort

If you set the `type` field to `NodePort`, the Kubernetes control plane allocates a port from a range specified by `--service-node-port-range` flag (default: 30000-32767). Each node proxies that port (the same port number on every node) into your Service. Your Service reports the allocated node port in its `.spec.nodePort` field.

### Choosing your own port

If you want a specific port number, you can specify a value in the `nodePort` field. Kubernetes will allocate that port or report back that the API transaction failed if the port is already in use. This means you need to care about possible port collisions yourself.

If you didn't specify a `nodePort`, one will be allocated for you.

If you set the `nodePort` value, it must be within the `--service-node-port-range` range configured for that cluster.

Using a NodePort gives you the freedom to set up your own load balancing solution, to configure environments that are not fully supported by Kubernetes, or even to expose one or more nodes' IPs directly.

## Transcription variance — re-verify before quoting

**The three port fields.** Variant A (preferred; reads as the page's own list):

- `port`: The port that will be exposed by this service.
- `targetPort`: The port on the container to send traffic to.
- `nodePort`: The port on each node to which the service is exposed.

Variant B (same content, looser wording): `nodePort` — the port exposed on each node;
`port` — the port exposed by the service; `targetPort` — the port on the pod that the
traffic is directed to.

**The additivity / "supersets" sentence.** Variant A:

> Note that Service of type NodePort and type LoadBalancer are supersets of ClusterIP. That is: a NodePort Service is reachable through its cluster IP.

Variant B:

> Note that Service of type NodePort and type LoadBalancer are supersets of type ClusterIP. That is, a NodePort Service is reachable through the cluster IP as well.

The *fact* is identical across both and is independently corroborated verbatim by
`k8s-docs-service-2026-08-23.md` ("To make the node port available, Kubernetes sets up a
cluster IP address, the same as if you had requested a Service of `type: ClusterIP`"). Only
the exact wording of this sentence is uncertain.

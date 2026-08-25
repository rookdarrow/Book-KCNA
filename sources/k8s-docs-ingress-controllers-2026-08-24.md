---
source_url: "https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/"
fetched_at: "2026-08-24T14:26:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["ingress-controller", "ingressclass", "absent-component-pattern", "reference-specification"]
---
# Ingress Controllers (kubernetes.io/docs/concepts/services-networking/ingress-controllers/)

(Fetched to support Ch 10 §3. The individual third-party controller products listed on this page
are deliberately NOT transcribed — the chapter outline forbids naming specific controllers.)

## Opening

In order for an Ingress to work in your cluster, there must be an *ingress controller* running. You need to select at least one ingress controller and make sure it is set up in your cluster.

## Using multiple Ingress controllers

You may deploy any number of ingress controllers using ingress class within a cluster. Note the `.metadata.name` of your ingress class resource. When you create an ingress you would need that name to specify the `ingressClassName` field on your Ingress object (refer to IngressSpec v1 reference). `ingressClassName` is a replacement of the older annotation method.

If you do not specify an IngressClass for an Ingress, and your cluster has exactly one IngressClass marked as default, then Kubernetes applies the cluster's default IngressClass to the Ingress. You mark an IngressClass as default by setting the `ingressclass.kubernetes.io/is-default-class` annotation on that IngressClass, with the string value `"true"`.

Ideally, all ingress controllers should fulfill this specification, but the various ingress controllers operate slightly differently.

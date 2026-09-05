---
source_url: "https://kubernetes.io/docs/concepts/services-networking/ingress/#default-ingress-class"
source_url_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/services-networking/ingress.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0 — canonical Markdown source of the Ingress concept page"
objectives_covered: ["D2.1"]
concepts_covered: ["ingressclass", "default-ingressclass", "ingress-controller", "absent-component-pattern"]
---

# Ingress — "Ingress class" and "Default IngressClass" (kubernetes.io/docs/concepts/services-networking/ingress/#default-ingress-class)

(Fetched 2026-09-04 to close a sourcing gap in Ch 10 §3 and Taking Your Bearings #1 Q4. The depth
snapshot `k8s-docs-ingress-depth-2026-08-24.md` carries the annotation sentence but not the page's
caution about more than one default IngressClass, which the chapter had been citing to it.
Transcribed verbatim from the canonical Markdown source in github.com/kubernetes/website; line
wraps joined. The Hugo `{{< caution >}}` shortcode is retained as a delimiter, not as prose.)

## Ingress class

"If the `ingressClassName` is omitted, a default Ingress class should be defined."

"Some ingress controllers work even without the definition of a default IngressClass. Even if you use an ingress controller that is able to operate without any IngressClass, the Kubernetes project still recommends that you define a default IngressClass."

## Default IngressClass

"You can mark a particular IngressClass as default for your cluster. Setting the `ingressclass.kubernetes.io/is-default-class` annotation to `true` on an IngressClass resource will ensure that new Ingresses without an `ingressClassName` field specified will be assigned this default IngressClass."

{{< caution >}}
"If you have more than one IngressClass marked as the default for your cluster, the admission controller prevents creating new Ingress objects that don't have an `ingressClassName` specified. You can resolve this by ensuring that at most 1 IngressClass is marked as default in your cluster."
{{< /caution >}}

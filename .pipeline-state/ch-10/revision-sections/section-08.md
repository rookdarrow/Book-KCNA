## ⚪ §3 — The Object Is Not the Implementation

Here is the sentence:

**You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect** [source: k8s-docs-ingress-depth-2026-08-24].

Not "less effect." Not "reduced functionality." None. The manifests in §2 are correct, well-formed, and accepted by the API server, and on a cluster with no Ingress controller they route nothing, because nothing is reading them.

> ★ **Fixed Point:** **You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect** [source: k8s-docs-ingress-depth-2026-08-24].

### What an Ingress controller is

**An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends to help handle the traffic** [source: k8s-docs-ingress-depth-2026-08-24]. There it is: §1's edge router, doing its job in a sentence you can now read without stopping. For an Ingress to work in your cluster, **there must be an ingress controller running**, and you need to select at least one and make sure it is set up [source: k8s-docs-ingress-controllers-2026-08-24].

Notice the structure of what you just read. The Ingress object is a *description of desired routing.* The controller is a control loop that reads that description and makes something in the real world match it. That is Chapter 3's control loop, unchanged and by now familiar: desired state in an object, a controller watching, reality dragged toward the description *[cross-bearing: see Ch 3 §6 — the control loop and the controller pattern]*. Recognising it here should cost you nothing, which is the point of having learned it once properly.

### The rule, retrieved

Chapter 3 gave you a sentence and asked you to keep it:

**An object without its component does nothing.**

It also told you that you would meet it four more times. This is the first of those four, and Chapter 3 published the pointer to this exact paragraph *[cross-bearing: see Ch 3 §4 — addons, and what else is optional]*.

Two counts run through this chapter, and they are not the same count. Chapter 3's four are the instances it lined up ahead of you: this one, one more in §7, and two in chapters still to come. The other count is your own — the instances you have personally watched fail. That one started last chapter, and it currently stands at two.

You do not have to take the rule on faith, because you have already collected that evidence. Last chapter, twice:

- A `type: LoadBalancer` Service on a bare-metal cluster with no provider integration. A real object. A real cluster IP. An external address field that stays `<pending>` forever, because Kubernetes does not directly offer a load balancing component; you must provide one, or integrate with a cloud provider [source: k8s-docs-service-2026-08-23] *[cross-bearing: see Ch 9 §3 — LoadBalancer and what has to exist beneath it]*.
- A Service whose selector matched nothing. A real object, a real cluster IP, a real DNS record, an empty EndpointSlice, and traffic that goes nowhere at all *[cross-bearing: see Ch 9 §4 — selectors, EndpointSlices, and the empty case]*.

Now a third: an Ingress with no controller.

> ⚓ **Worth Securing:** Chapter 3's phrase, verbatim, and worth writing on something you will see again: **an object without its component does nothing.** You have now personally met three instances: the LoadBalancer with no provider, the Service with no matching Pods, and this. Three sightings of the same light, and you stop calling it a coincidence and start calling it a landmark.

### Naming which controller: IngressClass

"You must have a controller" raises an obvious follow-up: *which one, if there are two?*

You may deploy any number of ingress controllers in a cluster, using **ingress class** to tell them apart [source: k8s-docs-ingress-controllers-2026-08-24]. Ingresses can be implemented by different controllers, often with different configuration, so **each Ingress should specify which controller it is intended to use** — done with the **`ingressClassName`** field on the Ingress, which references an **IngressClass** resource that carries additional configuration including the name of the controller that should implement the class [source: k8s-docs-ingress-depth-2026-08-24].

```yaml
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: external-lb
spec:
  controller: example.com/ingress-controller
  parameters:
    apiGroup: k8s.example.com
    kind: IngressParameters
    name: external-lb
```

If you do not specify an IngressClass on an Ingress and your cluster has **exactly one** IngressClass marked as default, Kubernetes applies that default [source: k8s-docs-ingress-controllers-2026-08-24]. You mark one as default by setting the `ingressclass.kubernetes.io/is-default-class` annotation to the string `"true"` [source: k8s-docs-ingress-controllers-2026-08-24]. Some ingress controllers work even without a default IngressClass defined; even so, the Kubernetes project still recommends that you define one [source: k8s-docs-ingress-depth-2026-08-24].

### The honest note

One more fact, and it is the one that keeps this from being a tidy story:

**Ideally, all Ingress controllers should fit the reference specification. In reality, the various Ingress controllers operate slightly differently** [source: k8s-docs-ingress-depth-2026-08-24].

That is the documentation's own phrasing, twice over: the Ingress page and the Ingress Controllers page say the same thing in nearly the same words [source: k8s-docs-ingress-controllers-2026-08-24]. It matters because the promise of a portable object is undercut, precisely, by the gap between a reference specification and any particular implementation of it. The documentation's own advice is to review your controller's documentation to understand the caveats of choosing it [source: k8s-docs-ingress-depth-2026-08-24].

> 🪝 **Snag:** Two clusters, the same Ingress manifest, different behaviour. Same chart, different pilot. The object is portable; the controllers are only *ideally* identical. The gap between the reference specification and a particular implementation is where a configuration that worked for a year stops working after a migration, and where the failure looks like a bug in your manifest rather than a difference in the thing reading it.

You now have a rule and three instances of it — three on your own count, one on Chapter 3's. Do not close the pattern here. §7 has a fourth, and it behaves differently from the first three in a way that turns out to matter more than all of them.

*[cross-bearing: see Ch 6 §8 — a custom controller acting on a custom resource is this same shape, met as the operator pattern]*
*[cross-bearing: see Ch 13 §7 — `kubectl top` on a cluster with no metrics-server]*
*[cross-bearing: see Ch 17 §7 — VPA, which is an addon and is not there by default]*

---
## 🔵 §4 — The List Behind the Name

A Service has a selector. The selector is a query. Somebody has to run the query, and somebody has to write down the answer, and the answer has to stay current while Pods appear and vanish underneath it.

### The path, in four steps

**One.** The Service carries a **selector** over Pod labels [source: k8s-docs-service-2026-08-23].

**Two.** **Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service** [source: k8s-docs-network-model-2026-08-23].

**Three.** The thing doing the managing is the **EndpointSlice controller**, one of the controllers running inside the kube-controller-manager, whose job is described as populating EndpointSlice objects **to provide a link between Services and Pods** [source: k8s-docs-cluster-architecture-2026-08-23]. You met the controller-manager's controller list in Chapter 3 *[cross-bearing: see Ch 3 §3 — the controllers inside kube-controller-manager]*; this is one of the names on it. You will also meet it under an older name — **endpoints controller** — including in a quotation later in this section. One job, two names in the documentation. Not two components.

**Four.** Anything that needs to know a Service's current backends reads the **EndpointSlices** — not the selector. The selector is the question. The EndpointSlice is the written-down answer.

<!-- FIGURE: ch09-fig03-service-endpointslice-selector-path -->
```
  Service: database                                    EndpointSlice
  ┌────────────────────┐                              ┌──────────────────┐
  │ selector:          │                              │ 10.244.1.7:5432  │
  │   app: db          │                              │ 10.244.4.2:5432  │
  └─────────┬──────────┘                              └────────▲─────────┘
            │                                                  │
            │ query                       ┌───────────┐        │
            ▼                             │  Ready?   │        │
   ┌──────────────────┐                   │  ╔═════╗  │        │
   │ Pod  app: db     │ ──── matches ────►│  ║ === ║  ├────────┘
   │      10.244.1.7  │      ✓ Ready      │  ╚═════╝  │
   ├──────────────────┤                   │   GATE    │
   │ Pod  app: db     │ ──── matches ────►│           ├────────┘
   │      10.244.4.2  │      ✓ Ready      │           │
   ├──────────────────┤                   │           │
   │ Pod  app: db     │ ──── matches ────►│ ✗ STOPPED │
   │      10.244.4.9  │      ✗ NOT Ready  │  at gate  │
   ├──────────────────┤                   └───────────┘
   │ Pod  app: cache  │  ✗ never matched the selector
   │      10.244.1.9  │     (different failure — different file)
   └──────────────────┘

            ┌──────────────────────────────┐
            │  EndpointSlice controller    │ ◄── watches Services + Pods,
            │ (in kube-controller-manager) │     writes the slice
            └──────────────────────────────┘
```

### Selection is not ownership

Chapter 6 already did half of this section's work, in a context where it was surprising. Its answer key established that a Service uses **labels** to allow the control plane to determine which EndpointSlice objects are used for that Service, and that in addition to the labels, each EndpointSlice managed on behalf of a Service carries an **owner reference** [source: k8s-docs-garbage-collection-2026-08-24].

Two mechanisms, doing two jobs. Labels answer *which slices belong to this Service*. Owner references answer *what should be cleaned up when this Service is deleted*, and help different parts of Kubernetes avoid interfering with objects they don't control [source: k8s-docs-garbage-collection-2026-08-24]. A fact that was a curiosity in Chapter 6 turns out to be structural here. *[cross-bearing: see Ch 6 §3 — selection versus ownership]*

### Readiness gates membership

Here is the part you were promised.

A Pod that matches the selector is **not automatically a destination**. It has to be **Ready**.

Chapter 5 taught you readiness probes and told you plainly that this is the mechanism doing the removing. The probe's documented behaviour says it outright: `readinessProbe` indicates whether the container is ready to respond to requests, and **if the readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod** [source: k8s-docs-pod-lifecycle-2026-08-23]. And the Pod's `Ready` condition is documented as meaning the Pod is able to serve requests and **should be added to the load balancing pools of all matching Services** [source: k8s-docs-pod-termination-2026-08-24].

That quotation is where the older name surfaces. The *endpoints controller* removing an address and the *EndpointSlice controller* writing the slice are the same job [source: k8s-docs-cluster-architecture-2026-08-23]; if you read them as two components, the path in this section grows a step it does not have.

*[cross-bearing: see Ch 5 §7 — readiness probes]*. That section told you what a readiness probe does. This one tells you where it does it: in the EndpointSlice.

★ **Fixed Point:** **selector → EndpointSlice → traffic.** The selector proposes; readiness disposes. A Pod must both **match the selector** and be **Ready** to appear in the Service's EndpointSlice and receive traffic.

Three chapters converge on that sentence, and it is worth naming the convergence. Chapter 5 gave you the probe. Chapter 6 relied on the mechanism without explaining it — the reason a bad release cannot take a Service down mid-rollout is that a new Pod which never reports Ready never joins the endpoint list, so traffic never reaches it, so the rollout stalls instead of the service failing. Chapter 9 is where the wiring becomes visible. *[cross-bearing: see Ch 6 §4 — why a failed rollout does not take the Service down]*

### The same fact, running backwards

Termination is the mirror image, and it is subtler than you'd guess.

At the same time as the kubelet is starting graceful shutdown of a Pod, **the control plane evaluates whether to remove that shutting-down Pod from EndpointSlice objects**, where those objects represent a Service with a configured selector. ReplicaSets and other workload resources no longer treat the shutting-down Pod as a valid, in-service replica [source: k8s-docs-pod-termination-2026-08-24].

But — and this is the interesting half — **any endpoints that represent the terminating Pods are not immediately removed from EndpointSlices**, and a status indicating terminating state is exposed from the EndpointSlice API. **Terminating endpoints always have their `ready` status as `false`**, so load balancers will not use them for regular traffic [source: k8s-docs-pod-termination-2026-08-24].

So the list is not a boolean membership test. It carries state — and note where that state lives. The Pod has a `Ready` condition; the Pod's *entry in the slice* has a `ready` status of its own [source: k8s-docs-pod-termination-2026-08-24]. A terminating Pod stays on the list, marked, so that anything watching can distinguish "gone" from "going" — which is what lets in-flight connections drain rather than being severed.

> 🔭 **Closer Look:** If traffic draining on a terminating Pod is needed, actual readiness can be checked as a condition called `serving` [source: k8s-docs-pod-termination-2026-08-24]. That is the distinction between "should get new traffic" and "can still handle traffic it already has." Deeper than the exam requires, and the reason graceful shutdown works at all rather than merely being promised.

### Looking at the list

You can inspect it directly:

```
kubectl get endpointslices -l kubernetes.io/service-name=<service-name>
```

Make sure the endpoints in the EndpointSlices match up with the number of Pods you expect to be members of your Service. **If they don't, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready** [source: k8s-docs-debug-pods-2026-08-23].

Two causes. That is the whole diagnostic content of this section, and it is stated as a fact rather than a procedure on purpose — Chapters 13 and 16 own the troubleshooting workflow, and they will retrieve this by name. *[cross-bearing: see Ch 16 §4 — a Service whose endpoint list is empty]*

> 🪝 **Snag:** A Service with no endpoints is not a broken Service. It is a correct Service whose selector currently matches nothing, or whose matching Pods are not Ready. Those are **two different bugs, and they live in two different files** — one is a mismatch between the Service's selector and the Pod template's labels; the other is an application that isn't passing its own health check. Confusing them costs you an afternoon, because you spend it editing the wrong YAML.

One more clause, closing a Chapter 7 loop. That chapter argued that a Service's backends landing on distinct nodes is what makes it resilient rather than merely load-balanced. Now you can see why the argument was necessary: the endpoint list is *just a list*. It has no opinion about where its endpoints are. Topology is the scheduler's problem, which is where you solved it. *[cross-bearing: see Ch 7 §5 — spreading replicas across failure domains]*

<!-- AUTHOR-REVIEW: outline § Open questions #4 — status changed, action still blocked. Stage 2 DID complete the EndpointSlice fetch (kubernetes.io/docs/concepts/services-networking/endpoint-slices/) on 2026-08-24, but its snapshot was never written to ../Book-KCNA/sources/ — the write was refused, and the body survives only inside research-manifest.md §2. So `k8s-docs-endpointslices-2026-08-24` cannot be cited from here without inventing a tag for a file that does not exist. Every claim in this section therefore still rests on five landed snapshots in combination. Still deliberately NOT asserted: why slices rather than one list, the default endpoints-per-slice limit, and ready/serving/terminating as THE documented condition set (the three names appear above only where k8s-docs-pod-termination-2026-08-24 states them individually). Once the snapshot lands on disk, apply curriculum-audit R4: state the three conditions as a documented set and give §4 the full chain — readiness probe -> Pod Ready -> EndpointSlice serving -> (absent termination) ready. Keep publishNotReadyAddresses out; it is a real exception to the readiness gate and would undercut the Fixed Point above. Keep the endpoints-per-slice limit and --max-endpoints-per-slice out of the body entirely. -->

<!-- AUTHOR-REVIEW: cross-bearing targets corrected this pass against the B6 section skeleton and B7 term ledger, both BINDING: readiness probes Ch 5 §6 -> §7 (skeleton pins probe definitions to Ch 5 §7 and names that pin in its own Ch 9 §4 entry); selection-versus-ownership Ch 6 §2 -> §3 (ownerReferences is owned by Ch 6 §3); failure-domain spreading Ch 7 §7 -> §5 (§7 is that chapter's Zenith; topologySpreadConstraints is §5); empty-endpoint troubleshooting Ch 13 §3 -> Ch 16 §4 (the skeleton names "empty EndpointSlice" under Ch 16 §4 explicitly, and that section's entry back-refers to Ch 9 §4 — a reciprocal pair). ONE POINTER LEFT UNRESOLVED: "Ch 3 §3 — the controllers inside kube-controller-manager". The skeleton places kube-controller-manager in Ch 3 §2 (The Control Plane) and node components in §3, which argues for §2; but the B7 ledger records EndpointSlice as first appearing in shipped Ch 3 §3, and the curriculum-alignment audit refers to this back-bearing as landing at §3. Needs a look at shipped Ch 3 to settle which section actually enumerates the controllers. Not changed on inference. -->

### The case that closes the section

A Service whose selector matches nothing is a completely valid object.

It has a cluster IP. It has a DNS record. Its EndpointSlice is empty, and traffic sent to it goes nowhere at all. Nothing is broken; nothing has failed; the declaration is being reconciled correctly against a set that happens to be empty. The control loop is doing exactly its job, and its job produces nothing, because there is nothing to produce.

You met the same shape in §3, with a LoadBalancer Service waiting on a provider that doesn't exist. Two instances now. Chapter 10 will meet a third and give the pattern a name.

---
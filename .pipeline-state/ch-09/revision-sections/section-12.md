## ☆ Taking Your Bearings #2

Five questions on what's actually behind the name, and the two times you deliberately don't want one — §4 and §5. A name on a chart is only as good as the survey behind it. These five ask what the survey found, and who keeps it current.

1. 🔵 **[retrieval: ch6]** Chapter 6 said a ReplicaSet finds its Pods by selector, and that a Service asking the same question about the same Pods is a *different controller reading the same labels*. Name the object where the Service's answer gets written down, and name the controller that writes it.

2. 🔵 A Service's selector matches four Pods. Three are Ready; one is failing its readiness probe. How many endpoints does the Service have, and what happens to the fourth Pod when its probe starts passing?

3. 🟡 `kubectl get endpointslices` for your Service returns no endpoints. The Pods are running. Name the two usual causes, and say how you would tell them apart.

4. 🔵 A teammate calls a headless Service "broken" because `kubectl` shows no cluster IP. Explain what `clusterIP: None` does, and give one workload for which it is the correct choice.

5. 🔵 You need cluster-internal clients to reach a database that runs on hardware outside the cluster, using an ordinary Service name. Two Service configurations could do this. Name both, and say what is different about what the client experiences.

> ⚠️ **Question 3 is intentionally challenging.** Your instinct will be to look at the network. The answer is in two YAML files. If you struggle with it, that struggle is the point — this is the item most likely to save you real time later, and it encodes better for having been hard.

---

**Answers with Explanations:**

**1. The EndpointSlice. Written by the EndpointSlice controller.**

Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service [source: k8s-docs-network-model-2026-08-23]; the EndpointSlice controller populates EndpointSlice objects to provide a link between Services and Pods [source: k8s-docs-cluster-architecture-2026-08-23].

Worth noticing what Chapter 6's framing bought you here *[cross-bearing: see Ch 6 §3 — how a controller knows its own]*. Two controllers ask the same question — *which Pods carry these labels* — for completely different reasons, and they do not coordinate. The ReplicaSet controller asks in order to count and to create replacements. The EndpointSlice controller asks in order to write down addresses. Neither knows the other exists. Both read the same field.

*Why a wrong answer is wrong:* **"The Service itself stores them"** is the natural guess and it's wrong in an instructive way. The Service stores the *query*. A separate object stores the *answer*, and a separate controller keeps that answer current.

**2. Three endpoints. When the fourth Pod's probe starts passing, it is added to the EndpointSlice and begins receiving traffic.**

A Pod's `Ready` condition means the Pod is able to serve requests and should be added to the load balancing pools of all matching Services [source: k8s-docs-pod-termination-2026-08-24]; if a readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod [source: k8s-docs-pod-lifecycle-2026-08-23].

One naming note before you carry that sentence forward. The documentation calls this component *the endpoints controller* on the Pod-lifecycle page and *the EndpointSlice controller* in the control-plane component list. That is one controller doing one job under two names — nothing additional is running, and question 1's answer and this one are describing the same thing.

Now connect it to Chapter 6, because this is the cheapest place to close that loop *[cross-bearing: see Ch 6 §4 — rolling-update mechanics]*. During a rolling update, a new Pod that never reports Ready **never receives traffic**. That is *why* a bad release cannot take your Service down — the broken replicas are excluded from the endpoint list by the same mechanism that admits the healthy ones. Chapter 6 depended on that behaviour to explain safe rollouts without ever naming the object it happens in. This is the object.

*Why a wrong answer is wrong:* **"Four"** counts the Pods the selector matches and stops there. As §4 put it, the selector proposes and readiness disposes — matching the labels makes a Pod *eligible* for the endpoint list; it does not put the Pod on it. The gate is a second, independent condition, and it is evaluated continuously rather than once at creation.

**3. Either the Service's selector doesn't match the Pods' labels, or the Pods are not Ready. Tell them apart by comparing the Service's selector against the Pods' labels, and by checking the Pods' Ready condition.**

If the endpoints don't match the Pods you expect, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready [source: k8s-docs-debug-pods-2026-08-23].

*Why the tempting wrong answers are wrong:*
- **"The network plugin is misconfigured"** would produce a much broader failure than one Service having no endpoints. Endpoint membership is computed by a controller reading the API; it does not touch the data plane at all.
- **"kube-proxy isn't running"** would break traffic to Services that *do* have endpoints. It cannot empty an endpoint list — kube-proxy reads that list, it doesn't write it.
- **"The Pods are on the wrong nodes"** — the endpoint list has no opinion about node placement whatsoever.

If you found this hard: good. It is genuinely counterintuitive that a *networking* symptom has two *non-networking* causes, and knowing that in advance is worth more than most of the recall material in this chapter.

**4. It means: don't allocate one virtual IP for this Service. DNS returns the Pod addresses directly instead. Correct choice for a StatefulSet.**

You create headless Services by explicitly specifying `"None"` for `.spec.clusterIP`; for headless Services that define selectors, DNS is configured to return A or AAAA records pointing directly to the Pods backing the Service [source: k8s-docs-service-2026-08-23]. StatefulSets currently require a headless Service to be responsible for the network identity of the Pods, and you are responsible for creating it [source: k8s-docs-statefulset-2026-08-24]. That requirement is the direct consequence of what a StatefulSet is for *[cross-bearing: see Ch 6 §6 — StatefulSet and stable identity]*: members that are not interchangeable need names that are not interchangeable either, and a single shared virtual IP cannot supply those.

*Why the wrong answer is wrong:* **"The cluster IP allocation failed"** treats `None` as an absence rather than a value. It is a value. Somebody typed it.

**5. A Service without a selector, backed by manually managed EndpointSlices; or `type: ExternalName`. The difference is proxying: the first puts kube-proxy in the path, the second does not.**

A Service used with a corresponding set of EndpointSlice objects and without a selector can abstract backends that run outside the cluster, including an external database [source: k8s-docs-service-2026-08-23]. ExternalName maps the Service to an external hostname via a CNAME record, and no proxying of any kind is set up [source: k8s-docs-service-2026-08-23].

**The proxying difference is the discriminator, and it is the reason this question exists.** Both are correct answers to the stated requirement, and they behave differently in ways that matter:

- With the **selectorless Service**, the client connects to a cluster IP inside the cluster. Traffic is intercepted on the node and redirected to the external address. The client's connection target is a cluster-internal address; DNS is ordinary Service DNS.
- With **ExternalName**, the client resolves the Service name, gets a CNAME to the external hostname, and connects to it directly. Kubernetes is not in the path at all. Which means TLS certificate names, source addresses seen by the external database, and anything that inspects the connection all behave differently.

This is the chapter's best interleaving item because it needs §3 and §5 simultaneously, and neither section alone gets you there.

---

**Checkpoint: You've Now Mastered**

✓ The path from selector to EndpointSlice to traffic
✓ Readiness as a gate on endpoint membership, not a step in a chain
✓ The two causes of an empty endpoint list, and why neither is a network problem
✓ Headless and selectorless Services as deliberate configurations

*This is the natural end of session one, if you're splitting the chapter — a reasonable place to put in for the night.* What remains is the component that actually moves the packet, the names you type, and the observation that ties all of it together.

---
## Chapter Summary

| Concept | Remember This |
|---|---|
| **Network model** | Four rules: unique cluster-wide Pod IP; all Pods reach all Pods; **no NAT, no proxies**; node agents reach local Pods |
| **Pod IP** | Belongs to the **Pod**. Containers share it and use `localhost` |
| **CNI** | Kubernetes **defines** the model; a **plugin implements** it. Second of **the four pluggable interfaces** this book tracks |
| **Service** | A stable, long-lived address for a set of Pods **that is expected to change**. An object, not a running thing |
| **ClusterIP** | The **default** type. Inside the cluster only |
| **NodePort** | Every node's IP at a static port — **and also a cluster IP** |
| **LoadBalancer** | Exposed externally by a load balancer **the provider supplies. Kubernetes supplies none** |
| **ExternalName** | A **CNAME**. Not on the ladder. **No proxying of any kind** |
| **Selector** | The **question**. A query over Pod labels |
| **EndpointSlice** | The **written-down answer**, maintained by the EndpointSlice controller |
| **Readiness** | The **gate**. Matching the selector is necessary and not sufficient |
| **Empty endpoints** | Selector mismatch, **or** Pods not Ready. Two bugs, two files |
| **Headless** | `clusterIP: None` — deliberate. DNS returns the Pod addresses. StatefulSets need one |
| **No selector** | Supported. Manually managed EndpointSlices, for backends outside the cluster |
| **kube-proxy** | Virtual IP for **every type but ExternalName**. Watches Service + EndpointSlice. **iptables is the default** |
| **Cluster IP** | **Virtual.** kube-proxy captures traffic addressed to it and redirects; nothing is listening. A **rule, not a socket** |
| **Cluster DNS** | **CoreDNS**, a built-in addon, serves every record below. It publishes the answer; it does not decide it |
| **Service DNS** | `<service>.<namespace>.svc.<cluster-domain>` — cluster IP for normal, **all Pod IPs for headless** |
| **Bare name** | **Local namespace only.** May succeed against the wrong Service |
| **The Zenith** | A Service is a **label query with a name**. Three loops publish its answer in three formats |

<!-- AUTHOR-REVIEW: LoadBalancer row narrowed per the fact-accuracy finding on
     additivity. The cached `k8s-docs-service-2026-08-23` snapshot documents the
     cluster-IP allocation for NodePort only ("Kubernetes sets up a cluster IP
     address, the same as if you had requested a Service of type: ClusterIP"); its
     LoadBalancer entry is one sentence and says nothing about a cluster IP or a node
     port. Restore "on top of NodePort" here, in §3's Fixed Point, in the Exam Alert
     and in the Common Traps table together — not piecemeal — once the targeted
     re-fetch of the Service page's `type: LoadBalancer` subsection lands in sources/.
     The "Kubernetes supplies none" half is separately sourced and stands as written. -->

<!-- AUTHOR-REVIEW: The Voyage Progress strip below reads "Ch 9 of 17". The binding
     B6 section skeleton runs Ch 1-20 (Ch 19 synthesis, Ch 20 mock exam). Either the
     strip counts a subset it does not name, or the denominator is stale. Left as
     shipped because no diagnostic adjudicated it and the other chapters' strips are
     not visible from this pass — confirm the figure once and sweep every chapter
     together. -->

---

🏆 **Safe Harbor** — the cluster's own network, and every object that names it.

You arrived at this chapter able to run workloads and unable to connect them. You now know what guarantees the cluster network makes, what a Service actually is, how its backends are computed and gated, what programs the node, and what the reader — sorry, the *client* — types. A Service is a name on the chart: what sits under it changes with the tide, and the name does not.

That is the inside of the cluster accounted for. Domain 2's Networking competency runs wider than one chapter — traffic arriving from outside, and the policy that decides which of it is allowed, is Chapter 10's work — but Chapters 10, 13 and 16 all stand on what you just finished.

**Voyage Progress:** 🗺️ → 🌊 **Ch 9 of 17** → 🌅

---
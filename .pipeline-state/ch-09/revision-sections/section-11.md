## 🟡 §5 — When You Don't Want a Single Address

Two deliberate exceptions. They only make sense now — a reader meeting either of these before §3 and §4 has no idea what is being subtracted from what.

### Headless: no single address, on purpose

Sometimes you don't need load-balancing and a single Service IP. In that case, you can create what are termed **headless Services**, by explicitly specifying `"None"` for the cluster IP address (`.spec.clusterIP`) [source: k8s-docs-service-2026-08-23].

What changes depends on whether the Service has a selector:

- For headless Services that **define selectors**, the endpoints controller creates EndpointSlices in the Kubernetes API, and modifies the DNS configuration to return **A or AAAA records that point directly to the Pods** backing the Service [source: k8s-docs-service-2026-08-23].
- For headless Services **without selectors**, no EndpointSlices are created automatically [source: k8s-docs-service-2026-08-23].

That first bullet carries the Kubernetes documentation's own phrasing — *the endpoints controller*. §4 called the same component **the EndpointSlice controller**. These are two names for one job, not two controllers: whichever name you meet, the object being written is an EndpointSlice.

★ **Fixed Point:** `clusterIP: None` is a **configuration, not a failure**. It says: *do not give me one address — give me all of them.* DNS returns the Pod addresses directly instead of a single virtual IP.

> 🪝 **Snag:** "Headless" sounds like something went wrong, and a teammate seeing `<none>` in the CLUSTER-IP column will often say so. It means the Service has no *head* — no single virtual IP standing in front of the set, no flagship to hail on the whole fleet's behalf. The Pods are all still there. You just get all of them, instead of one of them.

### Why anyone would want that

Chapter 6 already handed you the answer and then deferred it.

**StatefulSets currently require a headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service** [source: k8s-docs-statefulset-2026-08-24].

Think about what a StatefulSet is for. Its Pods are created from the same spec, but **are not interchangeable**: each has a persistent identifier that it maintains across any rescheduling [source: k8s-docs-statefulset-2026-08-24]. A database with one primary and two replicas. A quorum of peers that need to know each other by name. In those workloads, "send this to any one of them, I don't care which" is not a convenience — it is *precisely wrong*. If you need to reach the primary, an address that might land you on a read replica is not a stable endpoint. It is a signal sent to the whole fleet when what you needed was to raise one ship by name.

So the headless Service subtracts the one feature the ordinary Service exists to provide, and that subtraction is the feature. *[cross-bearing: see Ch 6 §6 — StatefulSets and stable identity]*, where you were told this and told to wait. §7 shows you what the resulting DNS looks like, and Chapter 11 closes the storage half of the same identity story *[cross-bearing: see Ch 11 §6 — StatefulSets and their per-replica volume claims]*.

### Services without selectors

The second exception is not an exception to the address; it is an exception to the *backends*.

Services most commonly abstract access to Kubernetes Pods thanks to the selector — but when used with a corresponding set of EndpointSlice objects and **without a selector**, the Service can abstract other kinds of backends, including ones that run **outside the cluster**: an external database, a service in another namespace or cluster, or a workload being migrated [source: k8s-docs-service-2026-08-23].

The selector is how a Service *usually* finds its endpoints. It is not what a Service *is*. Remove it, supply the endpoint addresses yourself, and everything downstream — the cluster IP, the DNS record, kube-proxy's interception, the client's connection — proceeds exactly as before.

> ⚓ **Worth Securing:** The selectorless Service is the fixed light a migration steers by. Your application inside the cluster talks to `database.production.svc.cluster.local` from day one — whether that name currently resolves to a managed database in a data centre three hundred kilometres away, or to Pods you moved in last night. The client never learns the difference, and never has to be redeployed to find out. The migration stops being the client's problem, which is usually the hardest part of making it happen at all.

### Two binaries, four cases

Headless-or-not and selector-or-not are independent, which means there are four combinations, and people routinely conflate two of them.

| | **Has a selector** | **No selector** |
|---|---|---|
| **Normal** (has a cluster IP) | The ordinary case from §3 and §4. Cluster IP; EndpointSlices populated automatically from the selector; DNS resolves to the cluster IP. | A cluster IP in front of endpoints you manage yourself. DNS resolves to the cluster IP; traffic is proxied to whatever addresses you supplied [source: k8s-docs-service-2026-08-23]. |
| **Headless** (`clusterIP: None`) | No cluster IP. The endpoints controller creates EndpointSlices; DNS returns A/AAAA records pointing directly at the Pods [source: k8s-docs-service-2026-08-23]. | No cluster IP, and **no EndpointSlices are created automatically** [source: k8s-docs-service-2026-08-23]. |

Four cells, and all four are supported configurations. None of them is an error state.

---
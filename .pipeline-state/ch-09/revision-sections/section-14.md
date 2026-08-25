## 🔵 §7 — Names, and Where They Resolve

Nothing so far has involved a name. The frontend still needs the database's cluster IP from somewhere, and hard-coding a cluster IP is barely better than hard-coding a Pod IP — you'd have to know it before the Service existed.

This section is where you stop needing to know any addresses at all. From here on the frontend steers by name rather than by position, and something else keeps the position current.

### What serves the records

**Kubernetes creates DNS records for Services and Pods. You can contact Services with consistent DNS names instead of IP addresses** [source: k8s-docs-dns-pod-service-2026-08-23]. Kubernetes publishes information about Pods and Services which is used to program DNS, and **the kubelet configures Pods' DNS so that running containers can look up Services by name rather than IP** [source: k8s-docs-dns-pod-service-2026-08-23].

The server doing the answering is **CoreDNS** — the cluster DNS addon that serves these records [source: k8s-docs-dns-pod-service-2026-08-23], listed under Service Discovery in the cluster addons as a flexible, extensible DNS server which can be installed as the in-cluster DNS for Pods [source: k8s-docs-cluster-addons-2026-08-24].

And the reason you have never installed it, never configured it, and possibly never thought about it: **DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on** [source: k8s-docs-dns-cluster-addon-2026-08-24].

Chapter 3 promised you CoreDNS by name *[cross-bearing: see Ch 3 §4 — cluster addons and CoreDNS]*, and Chapter 4 gave you a Service's DNS name in a single sentence and explicitly deferred four things: the mechanism, what serves the records, what else gets one, and how resolution actually proceeds *[cross-bearing: see Ch 4 §3 — namespaces and Service DNS names]*. All four are discharged in this section.

### The Service record

**Normal (not headless) Services are assigned DNS A and/or AAAA records, depending on the IP family of the Service, with a name of the form `my-svc.my-namespace.svc.cluster-domain.example`. This resolves to the cluster IP of the Service** [source: k8s-docs-dns-pod-service-2026-08-23].

Four labels, in a fixed order:

| Position | Part | What it is |
|---|---|---|
| 1 | `my-svc` | The Service's name |
| 2 | `my-namespace` | The namespace the Service lives in |
| 3 | `svc` | Literal. Marks this as a Service record |
| 4 | `cluster-domain.example` | The cluster domain — commonly `cluster.local` |

So the frontend types `database.production.svc.cluster.local`, and gets back a cluster IP that will not change for the life of the Service, regardless of what happens to the Pods behind it.

### The same name, a different answer

Here is the section's best fact, and it is the one people are most often surprised by.

**Headless Services (without a cluster IP) are also assigned DNS A and/or AAAA records with the same name form; unlike normal Services, this resolves to the set of IPs of all of the Pods selected by the Service. Clients are expected to consume the set or else use standard round-robin selection from the set** [source: k8s-docs-dns-pod-service-2026-08-23].

The name did not change shape. Same four labels, same order, same everything. What changed is the *number of answers*: one cluster IP for a normal Service, the whole Pod set for a headless one.

§5 told you this happens. This is where you can see that it happens **without a different name**, which is why it catches people — the client's configuration file looks identical in both cases.

★ **Fixed Point:** The **same name form** — `<service>.<namespace>.svc.<cluster-domain>` — gives you the **cluster IP** for a normal Service and **the set of Pod IPs** for a headless one.

### Why a bare name works, and where it stops

Chapter 4 gave you the rule flat: a bare `<service-name>` resolves to the Service local to your namespace, and reaching across namespaces requires the fully qualified domain name [source: k8s-docs-namespaces-2026-08-23].

Here is why, and it is more satisfying than a rule.

**By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain** [source: k8s-docs-dns-pod-service-2026-08-23].

That is it. That is the entire mechanism. It is not special-case Kubernetes behaviour — it is ordinary DNS search-domain resolution, the same thing that has let you type a short hostname on a corporate network for thirty years. A Pod in `payments` searching for `ledger` tries `ledger.payments.svc.cluster.local`, because `payments.svc.cluster.local` is in its search list. It finds something. It stops.

★ **Fixed Point:** A bare name resolves in the client Pod's **own namespace only** — **because that namespace is in the Pod's DNS search list**. This is not a Kubernetes special case; it is ordinary DNS search-domain resolution, which is also why crossing a namespace boundary requires the full `<service>.<namespace>.svc.<cluster-domain>`.

> ⚠ **Navigational Hazards:** The bare name is the single most common cross-namespace mistake, and it fails in the worst available way. If **no** Service of that name exists in the caller's namespace, you get a resolution failure — annoying, but obvious, and you'll fix it in a minute. If a Service of that **same name** exists in the caller's namespace, the lookup **succeeds**, and your application connects to the wrong thing. No error. No timeout. No log line. Just the wrong database, answering questions it shouldn't have been asked. This is why the FQDN rule is worth memorising rather than looking up.

> 🪢 **Mnemonic:** *service, namespace, svc, cluster.local.* Four labels, always in that order. The two in the middle are the ones people reverse under pressure — and note that `svc` is a literal, not an abbreviation of anything in your cluster.

### The other record shapes

Two more, compactly, plus one that closes §5's loop.

**SRV records** are created for **named ports** that are part of normal or headless Services, with the form `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` [source: k8s-docs-dns-pod-service-2026-08-23]. Note that the Service's own four labels are intact at the end; the port-name and protocol are prefixed on.

**Pods** get records too. In general a Pod has the DNS resolution of the form `pod-ipv4-address.my-namespace.pod.cluster-domain.example` — for example, `172-17-0-3.default.pod.cluster.local` [source: k8s-docs-dns-pod-service-2026-08-23]. The dots in the address become dashes, because dots are label separators in DNS and cannot appear inside a label. Note also that position 3 is `pod`, not `svc`.

And the one that finishes the StatefulSet story: the Pod spec has optional **`hostname` and `subdomain`** fields; **when both are set and a headless Service exists with the same name as the subdomain, the Pod's FQDN is `hostname.subdomain.namespace.svc.cluster-domain.example`** [source: k8s-docs-dns-pod-service-2026-08-23].

Note the shape, because it is the same shape by which an individual StatefulSet member is individually addressable. §5 told you a StatefulSet requires a headless Service to be responsible for the network identity of its Pods; a stable per-member name of this shape, surviving rescheduling, is what "network identity" cashes out to. *[cross-bearing: see Ch 6 §6 — StatefulSet Pod naming]*

<!-- FIGURE: ch09-fig05-dns-record-shapes -->
```
                    ┌───────────────┬──────────────┬───────┬─────────────────┐
                    │       1       │      2       │   3   │        4        │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Service (normal)  │    my-svc     │ my-namespace │  svc  │ cluster.local   │  → the cluster IP
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Service (headless)│    my-svc     │ my-namespace │  svc  │ cluster.local   │  → ALL the Pod IPs
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  SRV (named port)  │ _http._tcp.   │ my-namespace │  svc  │ cluster.local   │  → the named port
     prefixed with →│    my-svc     │              │       │                 │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Pod (by address)  │  172-17-0-3   │ my-namespace │  pod  │ cluster.local   │  → that Pod
                    │  (dots→dashes)│              │  ▲▲▲  │                 │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Pod (hostname +   │   hostname.   │  namespace   │  svc  │ cluster.local   │  → that Pod, by a
     subdomain)     │   subdomain   │              │       │                 │     stable name
  ──────────────────┴───────────────┴──────────────┴───────┴─────────────────┘  ─────────────────────────

  Columns 2 and 4 are identical in every row.
  Column 3 is `svc` for everything except the Pod-by-address record.
  The top two rows are the SAME NAME. Only the answer differs.
```

> **Dead Reckoning:** The five record shapes, stated flat.
>
> | Name shape | Resolves to |
> |---|---|
> | `my-svc.my-namespace.svc.cluster-domain.example` (normal Service) | The cluster IP of the Service |
> | `my-svc.my-namespace.svc.cluster-domain.example` (headless Service) | The set of IPs of all Pods selected by the Service |
> | `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` | The named port on that Service |
> | `pod-ipv4-address.my-namespace.pod.cluster-domain.example` (e.g. `172-17-0-3.default.pod.cluster.local`) | That Pod |
> | `hostname.subdomain.namespace.svc.cluster-domain.example` (requires `hostname` + `subdomain` set, and a headless Service named for the subdomain) | That Pod, by a stable name |
>
> Record types are A and/or AAAA depending on the IP family, except SRV records, which are SRV. Cluster DNS is served by CoreDNS, launched automatically by the addon manager. Pod DNS configuration is written by the kubelet. A bare service name resolves within the client Pod's own namespace because that namespace is in the Pod's default DNS search list. [source: k8s-docs-dns-pod-service-2026-08-23] [source: k8s-docs-dns-cluster-addon-2026-08-24]

> 🔭 **Closer Look:** A Pod's `dnsPolicy` field controls how its DNS is configured. `ClusterFirst` — any query that does not match the configured cluster domain suffix is forwarded to an upstream nameserver — **is the default policy if `dnsPolicy` is not explicitly specified** [source: k8s-docs-dns-pod-service-2026-08-23]. Also available: `Default` (inherit resolution config from the node), `ClusterFirstWithHostNet` (for Pods running with `hostNetwork`), and `None`, where the Pod ignores DNS settings from the Kubernetes environment and all settings come from the `dnsConfig` field [source: k8s-docs-dns-pod-service-2026-08-23]. Note the trap in the naming: the value called `Default` is *not* the default. Deeper than the exam requires — but if you ever meet a Pod that can't resolve cluster names at all, this field is where to look.

One boundary worth marking before Chapter 10. What you have just learned is **DNS-based service discovery** — mapping a name to an address, in the ordinary DNS sense. Chapter 10 introduces **name-based virtual hosting**: routing HTTP traffic to multiple host names at the same IP address [source: k8s-docs-ingress-2026-08-23]. Both involve hostnames, and they sit on opposite sides of the connection — one turns a name into an address before any traffic moves, the other sorts traffic that has already arrived at a single address. Conflating them makes Chapter 10 considerably harder than it needs to be. *[cross-bearing: see Ch 10 §2 — name-based virtual hosting]*

<!-- AUTHOR-REVIEW: outline explicitly scopes out CoreDNS Corefile configuration, custom nameservers, stub domains, and CoreDNS plugins. The dns-cluster-addon snapshot's own note records the rest of that page as out of scope. Nothing on cluster DNS customisation appears above; that omission is deliberate, not a gap. -->

<!-- AUTHOR-REVIEW: cross-bearing targets in this section were retargeted to conform to the BINDING B6 section skeleton, which no diagnostic flagged. Changes: `Ch 3 §6` -> `Ch 3 §4` (skeleton: Ch 3 §4 is "Addons, and What Else Is Optional"; §6 is the control loop); `Ch 4 §6` -> `Ch 4 §3` (skeleton: Ch 4 §3 "Where a Name Lives" owns namespaces; §6 is the chapter synthesis); `Ch 6 §5` -> `Ch 6 §6` (skeleton: Ch 6 §6 "When Pods Are Not Interchangeable" owns StatefulSet identity; §5 is "Every Rollout Is a Revision"); `Ch 10 §3` -> `Ch 10 §2` (skeleton: Ch 10 §2 "Routing by Host and Path" owns name-based virtual hosting; §3 owns Ingress controllers). The draft's back-pointers appear to be consistently off against the skeleton chapter-wide, not only in this section -- recommend a chapter-wide pointer sweep at the integration-check stage, and revert here if the skeleton's extraction is what is wrong rather than the draft. -->

---
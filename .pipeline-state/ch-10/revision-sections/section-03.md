## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score determines how to approach the content; no shame in any score, just different reading strategies. Four of these test priors you arrive with; four are deliberate retrieval from Chapters 3 and 9.

1. You run one web server on one IP address, and it serves `shop.example.com` and `blog.example.com` differently. What does the server have to look at to tell the two apart, and at what point in the connection does that information become available?

2. You have fifty services that all need to be reachable from outside the cluster. Chapter 9 gave you a Service type that does exactly that. Name it, then say what fifty of them costs you: addresses, and anything else you can think of.

3. Which of Chapter 9's four Service types can send `/checkout` to one set of Pods and `/catalog` to another? Say why.

4. On the firewalls you have configured or worked behind: if a packet matches no rule at all, is it allowed or dropped? And if one rule permits something a later rule forbids, which one wins?

5. Two APIs. One is announced as **deprecated**. The other is announced as **no longer being developed, with no further changes**. For each, say whether you would expect it to be removed, and whether you would start a new project on it today.

6. Chapter 3 asked you to remember a one-sentence rule about objects and the components that act on them. Write it down. Then name one place you have already met it.

7. Chapter 9's second network-model rule said all Pods can reach all Pods — *"barring intentional network segmentation."* What do you think that hedge was pointing at, and at what layer would something have to sit to enforce it?

8. A client connects to `https://shop.example.com` and the request eventually reaches an application server. Where does the TLS connection actually end? Who holds the certificate and private key, and what does the application server see arriving?

<details>
<summary>Click for answers + reading strategy</summary>

1. **The `Host` header, available only after the TCP connection is established and the request has been sent** `[source: k8s-docs-gateway-api-depth-2026-08-24]`. The client's DNS lookup resolved the name to an address before any traffic moved; the name itself travels inside the request. (HTTPS carries an earlier tell in the SNI field of the TLS handshake — traffic for several hostnames can be multiplexed on a single port that way, where the proxy terminating TLS supports SNI `[source: k8s-docs-ingress-depth-2026-08-24]` — but the routing decision is conventionally made on the `Host` header.)

2. **`Service.Type=LoadBalancer`** *[cross-bearing: see Ch 9 §3 — the Service type ladder]*. Fifty of them costs fifty external addresses, fifty provisioned load balancers, fifty line items on a cloud bill, and fifty things to configure, monitor, and eventually decommission.

<!-- AUTHOR-REVIEW: the one-address-per-Service ratio here is inherited from Ch 9 and carries no [source:] tag; no cached snapshot in this chapter's corpus states the ratio or its cost consequences. Confirm it was sourced at Ch 9 §3 — if it was not, this is a chapter-crossing research gap rather than a Ch 10 defect. The cost enumeration itself is the book's operational reasoning and reads correctly as such. -->

3. **None of them.** None of them reads HTTP. Three of the four operate on addresses and ports; the fourth, ExternalName, is a DNS alias with no proxying set up at all `[source: k8s-docs-service-2026-08-23]`. `/checkout` and `/catalog` are bytes inside an HTTP request, and nothing in Chapter 9 opens the request to look.

4. Most likely **dropped**, and **the deny wins**. That is how ordinary packet-filtering firewalls behave, and it is a sound instinct nearly everywhere.

5. **Deprecated** implies eventual removal, so you would avoid starting new work on it. **No longer developed** says nothing about removal; it says the thing is finished. It may well be permanent. You might still use it, knowing it will never gain a feature.

6. **An object without its component does nothing.** You have met it at least twice: a `type: LoadBalancer` Service on a cluster with no load balancer to provision, and a Service whose selector matched no Pods.

7. Something has to be able to restrict Pod-to-Pod reachability. Since the CNI plugin is what actually moves the packets, enforcement would have to live down there, wherever the packets themselves are handled.

8. **At the reverse proxy or load balancer at the edge**, which holds the certificate and private key. The application server behind it receives plain HTTP `[source: k8s-docs-ingress-depth-2026-08-24]`.

---

**If you got 6+ right:** Skim §1 and §2 — you have the priors. Read §4 carefully anyway; it is a word-level distinction and skimming is exactly how people lose that point. Then read §6 and §7 at full attention regardless of your score.

**If you got 3–5 right:** Read at normal pace. The material is in reach and this chapter is calibrated for you.

**If you got 0–2 right:** Read carefully. And if questions 2, 3, or 7 were among your misses, **go back to Chapter 9 first.** Not "review" — go back. This chapter re-teaches no part of the Service model. §1's argument is arithmetic on Chapter 9's ladder, §2's backends are Chapter 9's Services, and §6's subjects are Chapter 9's Pod IPs. A re-read of Chapter 9 will buy you more than a careful read of this chapter will.

</details>

---
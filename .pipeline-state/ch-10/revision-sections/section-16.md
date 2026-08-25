## ☀️ §8 — Nothing Happens Without a Controller

This chapter taught two objects that have nothing to do with each other.

One routes HTTP by hostname and path at the edge of the cluster, at layer 7, for traffic coming in from outside. The other permits and forbids TCP connections between Pods inside it, at layers 3 and 4, for traffic that never leaves. Different layers. Different directions. Different problems. In most organisations, different teams.

And they fail the same way.

Write either one perfectly. Apply it successfully. Watch `kubectl get` return it. And nothing happens, because in one case no Ingress controller is installed, and in the other the network plugin does not implement NetworkPolicy.

> ☀️ **Zenith:**
>
> You have now seen this four times, and two of the four were your own from last chapter.
>
> A `type: LoadBalancer` Service with no provider to fulfil it. A Service whose selector matched no Pods. An Ingress with no controller. A NetworkPolicy on a plugin that does not implement one.
>
> Chapter 3 gave you the sentence — *an object without its component does nothing* — and told you that you would meet it four more times. This is where that debt comes due in full.
>
> But the rule is not a fact about Ingress, and it is not a fact about NetworkPolicy. It is a fact about **what a Kubernetes object is**, which you have held since Chapter 4 without necessarily seeing where it led.
>
> An object is a record of intent. Intent does not act.
>
> Something has to be watching, and willing, and *present*. Every object in this book works this way: the Deployment that produced Pods, the Service that produced a stable name, the Job that ran to completion. In all of those cases the watcher happened to be there, so the object appeared to do the work itself. These four are simply the cases where the watcher is missing, and the appearance falls away.

A chart drawn perfectly is still a chart. Somebody has to stand the watch.

You did not need the book to tell you this, incidentally. Soundings question 6 asked you to write down Chapter 3's rule and name a place you had met it, and if you answered that question you had already assembled most of the argument. The four instances are yours; the sentence was handed to you seven chapters ago.

<!-- AUTHOR-REVIEW: the Ch 3 §6 cross-bearing below nests *why* and *that* inside the convention's own italic span, which breaks emphasis in most renderers and departs from the ratified `*[cross-bearing: see Ch N §M — brief topic]*` form. Structural lint passes it. Recommend recasting the topic without inner emphasis, or dropping the trailing clause. Not changed here — no diagnostic finding names it. -->
*[cross-bearing: see Ch 3 §6 — the control loop, which is *why* this is true rather than merely *that* it is]*
*[cross-bearing: see Ch 4 §1 — the declarative model, and the object as an artifact of intent]*

> ⚓ **Worth Securing:** You now own a question you can ask about anything: **what is watching this, and is it installed?**
>
> Chapter 13 will hand you a cluster where `kubectl top` returns an error, and the answer is metrics-server *[cross-bearing: see Ch 13 §7 — the resource metrics pipeline]*. Chapter 17 will hand you VPA, which is an addon and is not shipped by default *[cross-bearing: see Ch 17 §7 — the autoscaling landscape]*. Those two are the instances §3 was counting toward when it called this the first of four; the count above runs the other way, backward over the four already behind you. Chapter 3 published both of those pointers before you had any of the evidence. You have the evidence now.
>
> It also works on objects this book never mentions, which is the actual return on this chapter.

<!-- FIGURE: ch10-zenith-nothing-without-a-controller -->
```
  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
  │   Service   │  │   Service   │  │   Ingress   │  │NetworkPolicy│
  │type:LoadBal.│  │selector: {} │  │  host+path  │  │ podSelector │
  │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │
  ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│
  │  provider   │  │matching Pods│  │ Ingress     │  │  network    │
  │   ( none )  │  │   ( none )  │  │ controller  │  │  plugin     │
  │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│  │  ( none )   │  │  ( none )   │
  │             │  │             │  │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│
  ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
  │   nothing   │  │   nothing   │  │   nothing   │  │   nothing   │
  │             │  │             │  │             │  │ …and nothing│
  │             │  │             │  │             │  │  tells you  │
  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘

           An object without its component does nothing.
```

Look at the fourth panel one more time. Three of these announce themselves. One does not.

---

🏆 **Safe Harbor** — Chapter 10 complete. You crossed the boundary from moving packets to reading requests, met the API that does it and the one that supersedes it, went back down two layers to restrict traffic inside the cluster, and collected a rule that will outlast every object in this chapter.

🗺️ → 🌊 → 🌅 — *Part III: passage. Two chapters of the network behind you.*

---
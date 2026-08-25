## 🧭 Soundings

Before reading this chapter, try these questions. Your score determines how to approach the content — no shame in any score, just different reading strategies.

1. You are running three interchangeable copies of a service. One of them dies and is replaced by a copy at a different address. What does a client need so that nobody has to go and tell it the new address? Name two mechanisms you have seen do that job.

2. Chapter 5 said a Pod has one network namespace shared by all of its containers. Two containers in one Pod both want to listen on port 8080. What happens? And how does either one reach the other?

3. A Deployment performs a rolling update and every Pod is replaced. A client somewhere was holding the IP address of one of the old Pods. What happens to that client, and what would have to be true for it not to care?

4. Chapter 4 said a selector is a query over labels, and Chapter 6 said a ReplicaSet finds its Pods that way. Suppose a *different* controller needed to find the same set of Pods, for a different reason. What mechanism would you expect it to use — and what would break if someone edited one Pod's labels?

5. Chapter 4 gave you, in a single sentence, the DNS name form a Service gets. Write it out. Then: a container in namespace `payments` uses only the bare name `database`. Which Service does it reach, if there is a `database` Service in both `payments` and `billing`?

6. On an ordinary network, a request crosses a NAT boundary. What does the receiving process see as the source address, and name one thing that becomes harder because of it.

7. A platform that manages containers ships with no networking implementation of its own, and expects you to install one before anything works. Give one reason a system would be designed that way, and one cost of the design.

8. Something inside a private network has to be reachable from outside it. Name two mechanisms you have used or seen. For each, say who supplies the box that terminates the outside connection — you, or someone else.

<details>
<summary>Click for answers + reading strategy</summary>

1. **An indirection — something whose address doesn't change while the things behind it do.** A load balancer with a fixed VIP and a health-checked backend pool; a DNS name re-pointed as backends move; a service registry the client queries. Any two of those count.

2. **The second container cannot bind 8080 — they share one port space.** They reach each other over `localhost`, because they share one network namespace. The Pod has one IP address; the containers share it. *(Chapter 5 §2.)*

3. **The client breaks** — it holds a valid-looking address for something that no longer exists. It would not care if what it had been handed were something that doesn't move. *(Chapter 6 §4.)*

4. **A selector — a query over the same labels.** Editing a Pod's labels can drop it out of one controller's set, out of the other's, or out of both. Nothing arbitrates between them: each evaluates its own query against the same field, and neither is told what the other decided. *(Chapter 4 §7, Chapter 6.)*

5. `<service-name>.<namespace-name>.svc.cluster.local` [source: k8s-docs-namespaces-2026-08-23]. A bare `database` from inside `payments` resolves to the `database` Service **in `payments`** — the caller's own namespace. It never sees the one in `billing`.

<!-- AUTHOR-REVIEW: The question-quality audit flags this answer as a spoiler FAIL — it
     discloses both factual halves of the §7 ★ Fixed Point (the name form, and the bare-name
     rule) before the chapter starts. It cannot be fixed here. Both facts are genuine Chapter 4
     prerequisites, and §7 itself says so, which makes Soundings rule 2 (must be answerable
     from prerequisites) and rule 3 (must not reveal a Fixed Point) unsatisfiable at the same
     time for this item. The audit's ratified remedy is to leave question 5 as written and
     rewrite the §7 Fixed Point so its claim rests on the DNS search-list mechanism — the one
     part this Soundings withholds. That edit belongs to the §7 pass, not this one. -->

6. **The receiving process sees the NAT device's address, not the original sender's.** That makes source-based authorization, rate-limiting, audit logging, and debugging harder — anything that wanted to know *who* actually called.

7. **Reason:** pluggability. Different environments have genuinely different networking requirements, and a single built-in implementation would be wrong for most of them. **Cost:** nothing works out of the box; you must choose and install something before the platform functions at all.

8. Port forwarding on a firewall or router (**you** supply the box); a cloud load balancer with a public address (**the provider** supplies it); a reverse proxy on a bastion host (**you**); a tunnel service (**the provider**). Any two, with the ownership answered.

**If you got 6+ right:** Skim this chapter. Read §3 and §7 properly — they carry the memorizable material — and read every ★ Fixed Point and ⚠ Navigational Hazards callout. Then take all three ☆ Taking Your Bearings checkpoints, because the traps in this chapter are traps for people who already know some networking.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Read carefully. And specifically: **if questions 2, 3 and 4 were among your misses, go back to Chapter 5 §2 and Chapter 6 §4 before you start §2 of this chapter.** The first half of this chapter is built directly on the Pod's network namespace and on controller churn. Without both of those, §2 reads as a solution to a problem you have not yet felt.

</details>

---
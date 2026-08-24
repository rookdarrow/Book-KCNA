# Chapter 6: Fleets, Not Vessels
## *"Nobody sails one Pod"*

**Domain Weight: 6% (authored allocation — see front matter) | Complexity: Mixed | Novelty: Moderate**

---

## Attention Budget

**Total time: ~95 minutes | Recommended: Split across 2 sessions**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 — The Resource That Holds the Intent | 12 min | Medium | Mid-session |
| §2 — A Loop You Can Watch Working | 7 min | Low | Anytime |
| §3 — How a Controller Knows Its Own | 12 min | Medium | Mid-session |
| ☆ Taking Your Bearings #1 | 6 min | Medium | After brief break |
| §4 — Changing the Fleet Under Way | 16 min | **High** | Peak attention |
| §5 — Every Rollout Is a Revision | 11 min | Medium | Mid-session |
| ☆ Taking Your Bearings #2 | 6 min | Medium | After brief break |
| §6 — When Pods Are Not Interchangeable | 9 min | Medium | Mid-session |
| §7 — One Per Node, and Work That Ends | 8 min | Low | Anytime |
| §8 — The Control Loop, Extended | 12 min | Medium-High | Peak attention |
| ☆ Taking Your Bearings #3 | 6 min | Medium | After brief break |
| §9 — Nobody Sails One Pod | 5 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

**Recommended split point:** after Taking Your Bearings #2. Sections 1–5 are the Deployment arc from start to finish; 6–9 are the rest of the family and what the pattern turns into.

*If you only have 15 minutes: read §1 and the decision tree at the close of §7, then take Bearings #3. The ownership chain is the structural key to this chapter, and the decision tree is where three of the exam's documented confusions all resolve at once.*

---

> *"A fleet is not a number of ships. It is an intention, expressed in ships."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before reading this chapter, try these questions. Your score determines how to approach the content — no shame in any score, just different reading strategies.

Most of these describe *situations*, not definitions. Answer them the way you'd answer a colleague at a whiteboard.

1. You want three copies of a process running on a machine at all times. One of them dies at 3 a.m. What would have to be written down *in advance* for something else to restore it without waking you?

2. You need to replace a running service with a new version while it stays reachable the whole time. Describe how you have done this, or would do it, with tools you already know.

3. There are two ways to identify a group of things: an explicit list of names, or a rule about a property they share. What does each approach cost you when the group changes while you're not looking?

4. Consider a two-member database: one primary, one replica, each with its own data on disk. What actually breaks if you swap which machine is which — hostnames, storage, and all?

5. A log-collection agent has to run on every machine in your fleet — including the machines that will be added next Tuesday. How would you express that requirement, as opposed to "run six copies"?

6. Your init system supervises two things: a web server that should never exit, and a nightly backup script that should exit. How does it treat them differently, and what does "healthy" mean for each?

7. *[retrieval: ch3]* A control loop compares two things and acts on the difference. Name both, and say what the loop does when they match.

8. *[retrieval: ch5]* A Pod's node dies. Chapter 5 was emphatic that the Pod is not rescheduled. What did it say happens instead — and what did it say was left unanswered?

<details>
<summary>Answers + reading strategy</summary>

1. **The count and the recipe.** Something has to know *how many* you wanted and *what one of them looks like*, or it cannot tell that a copy is missing, and it cannot build a replacement if it notices. Both facts have to exist before the failure, not after.

2. **Any answer describing gradual replacement is correct.** Common ones: add new instances to a load-balancer pool and drain the old ones; stand up a second environment and flip DNS; restart instances one at a time behind a health check. The shared shape is *overlap* — old and new coexist for a while.

3. **A list is exact but goes stale; a rule stays current but can match things you didn't expect.** The list requires you to update it every time membership changes. The rule updates itself, which is the point, and is also the risk.

4. **Nearly everything.** Their hostnames are baked into replication configuration. Their on-disk data is not the same data. Something that connects to "the primary" is connecting to a name, and the name now points at a machine holding replica state. The two machines look identical from a distance and are not substitutable.

5. **As a property of the machines, not as a number.** "One on every machine matching this description" survives new machines joining; "six copies" does not. The count is an *output* of the rule, not an input to it.

6. **The web server exiting is a failure; the backup script exiting is success.** systemd calls these `service` and `oneshot`; a CI system calls them a daemon and a job. "Healthy" for the first means still running; for the second, it means exited zero and stopped.

7. **Desired state and current state.** The loop acts to bring current closer to desired. When they match, it does nothing — and it keeps not doing anything, on a loop, forever. A control loop at rest is still running *[cross-bearing: see Ch 3 §6 — the control loop]*.

8. **The Pod is not moved; it is replaced.** Chapter 5 said a Pod is never rescheduled to a different node — instead a new, near-identical Pod with a *different UID* is created [source: k8s-docs-pod-lifecycle-2026-08-23]. What Chapter 5 explicitly left open was *who creates it*.

---

**If you got 6+ right:** Skim this chapter. Focus on the ★ Fixed Points, the ⚠ Navigational Hazards blocks, and the decision tree in §7 — then go straight to the Taking Your Bearings checkpoints. You already have the instincts; we're attaching names and exact defaults to them.

**If you got 3–5 right:** Read at normal pace. The material is in reach; this chapter is calibrated for you.

**If you got 0–2 right:** Read carefully, and don't skip §2 — it's short and it's load-bearing. **If questions 7 and 8 were among your misses, re-read Chapter 3 §6 and Chapter 5 §4 before starting §2.** Those two are the questions this chapter collects and answers; without them, §2 will read as a vocabulary drill instead of a payoff.

</details>

---

## Why This Chapter Matters

Chapter 5 ended on a question and deliberately refused to answer it: if Pods are designed to be replaced rather than repaired, who does the replacing?

The honest answer is stranger than "a thing called a Deployment." Kubernetes has no special replacement machinery at all. It has the same control loop you met in Chapter 3 — the one that compares desired state to current state and closes the gap — given a count to hold and a template to copy from. Rolling updates, rollbacks, one-Pod-per-node agents, scheduled batch work, and the operator that runs somebody's production database are all *that one loop*, with different desired state plugged into it. This chapter has fewer ideas in it than it looks like. By §9 you'll be able to see that; the intervening sections are what make it visible rather than merely asserted.

What changes here is what kind of practitioner you are. Chapter 5 made you someone who can read what infrastructure is telling them. This chapter makes you someone who states what should be true and lets the system be responsible for it. That is the actual behavioral gap between people who are new to Kubernetes and people who aren't. Newcomers reach for the Pod. Then for a script that recreates the Pod. Then for a cron entry that checks whether the script ran, and eventually for a monitor that checks the cron entry. Practitioners write down the count and the template and go home. You have probably written one of those scripts. This chapter is about not needing it.

The stakes, stated without inflation: this material carries roughly six percent of the exam under this book's authored allocation — CNCF publishes four domain weights and twelve named competencies with no sub-weights, and the front matter says so plainly [source: cncf-kcna-curriculum-pdf-2026-08-23]. That number undersells the chapter twice. First, this is the beat the book's spine passes through: Chapter 3 introduced the control loop, this chapter instantiates it, and Chapter 15 generalizes it into something that looks like a completely different technology until you recognize the shape. Second, the workload-resource decision — Deployment or StatefulSet or DaemonSet or Job — is exactly the kind of thing a recognition exam asks about in a single sentence, and the three documented confusions around it can all be inoculated against with one well-ordered figure.

> **Dead Reckoning:** You do not manage Pods directly. You create a workload resource — Deployment, StatefulSet, DaemonSet, Job, or CronJob — which configures a controller that creates and deletes Pods on your behalf to match the state you specified [source: k8s-docs-workloads-2026-08-23]. The Deployment holds a Pod template and an update policy; it manages ReplicaSets; a ReplicaSet holds a replica count and maintains that many Pods [source: k8s-docs-deployment-2026-08-23] [source: k8s-docs-replicaset-2026-08-24]. That is the whole architecture. Everything else in this chapter is a variation on which desired state gets plugged in.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Trace** the ownership chain from a Deployment down to a running Pod, and say which layer holds the count and which holds the template.
- **Explain** how a controller knows which Pods belong to it — and what breaks when two controllers disagree about that.
- **Predict** what a cluster does during a rolling update, given `maxSurge` and `maxUnavailable`, and name the thing that makes the update *safe* rather than merely gradual.
- **Distinguish** the six workload resources by the one property that separates each from its nearest neighbor.
- **State** what actually creates a new revision — and what looks like it should, but doesn't.
- **Define** a custom resource, a custom controller, and the pattern that is the two of them together.

*You'll also stop reaching for `kubectl run`, which is a smaller change than it sounds and is the point of the whole chapter.*

---

## ⚪ §1 — The Resource That Holds the Intent

Chapter 5 asked who replaces a Pod when its node dies, and named the three pieces of the answer: a count that was wanted, a template for replacements, and a loop that notices *[cross-bearing: see Ch 5 §4 — Pod disposability and replacement]*. Here is the resource that holds the first two.

**The answer, in one sentence:** you don't need to manage each Pod directly — instead you use workload resources that manage a set of Pods on your behalf, and those resources configure controllers that make sure the right number of the right kind of Pod are running, to match the state you specified [source: k8s-docs-workloads-2026-08-23].

Read that again with an eye on the verbs. *You* specify. The *resource* configures. The *controller* makes sure. Nobody in that sentence performs the replacement as an action; the replacement is a consequence of a specification and a loop.

### Three layers, not two

The workload resource you'll meet most often is the **Deployment**. A Deployment manages a set of Pods to run an application workload — usually one that doesn't maintain state — and it provides declarative updates for Pods *and ReplicaSets* [source: k8s-docs-deployment-2026-08-23].

That second half is the part almost everyone skips on first reading, and it's the structural key to this chapter. There are three layers, not two.

<!-- FIGURE: ch06-fig01-deployment-replicaset-pod-ownership -->
```
        ┌──────────────────────────────────────────────┐
        │  Deployment: web                             │
        │                                              │
        │    Pod template ......  what a Pod looks like│
        │    Update strategy ...  how to change them   │
        └───────────────────────┬──────────────────────┘
                                │ owns
                                ▼
        ┌──────────────────────────────────────────────┐
        │  ReplicaSet: web-7d4b9c                      │
        │                                              │
        │    replicas: 3 ......  how many should exist │
        └───────┬──────────────┬──────────────┬────────┘
                │ owns         │ owns         │ owns
                ▼              ▼              ▼
        ┌──────────┐   ┌──────────┐   ┌──────────┐
        │   Pod    │   │   Pod    │   │   Pod    │
        │ (copy of │   │ (copy of │   │ (copy of │
        │ template)│   │ template)│   │ template)│
        └──────────┘   └──────────┘   └──────────┘

     intent flows DOWN          existence is reported UP
```

You create a Deployment to roll out a ReplicaSet; the ReplicaSet creates Pods in the background [source: k8s-docs-deployment-2026-08-23]. The division of labour is exact and it matters:

- The **Deployment** holds the Pod template and the update policy. It is the layer that knows *what* the application should look like and *how* to change it.
- The **ReplicaSet** holds the count. Its entire purpose is to maintain a stable set of replica Pods running at any given time [source: k8s-docs-replicaset-2026-08-24].
- The **Pods** are what actually run.

Hold onto that separation. Sections 4 and 5 are both direct consequences of the Deployment layer existing separately from the ReplicaSet layer — a rolling update works the way it does *because* a Deployment can hold two ReplicaSets at once, and a revision means what it means *because* the template lives one layer above the count.

> **★ Fixed Point**
>
> **The chain is Deployment → ReplicaSet → Pod. The Deployment holds the Pod template and the update policy. The ReplicaSet holds the replica count. The Pods run.**

### The Pod template

Everything Chapter 5 taught you about a Pod's `spec` is unchanged. It has simply moved: it now lives inside the workload resource as `.spec.template`, a pod template with exactly the same schema as a Pod, except that it's nested and has no `apiVersion` or `kind` of its own [source: k8s-docs-daemonset-2026-08-24]. Controllers for workload resources create Pods from that template and manage them on your behalf [source: k8s-docs-pods-2026-08-24].

That's the piece that gets copied when a replacement is needed. You don't need it developed further — you need it *located*. It's one nesting level down from where you last saw it *[cross-bearing: see Ch 4 §2 — the four fields every object carries]*.

> ⚓ **Worth Securing:** If you find yourself writing a bare Pod manifest for anything other than a one-off experiment, you've picked the wrong object. The Kubernetes docs put it flatly: Pods are generally not created directly, and are created using workload resources instead [source: k8s-docs-pods-2026-08-24]. A bare Pod is not replaced when its node fails — it is simply gone.

You may occasionally meet **ReplicationController** in older tutorials and in `kubectl scale`'s own help text. It is the legacy resource that ReplicaSet replaced [source: k8s-docs-workloads-2026-08-23]; ReplicaSets are its successors, serving the same purpose and behaving similarly, except that a ReplicationController doesn't support set-based selector requirements [source: k8s-docs-replicaset-2026-08-24]. One clause is all it deserves: if you see it, it's superseded.

So here is the reframe this section exists for. The Pod you spent an entire chapter learning is something you will almost never create directly. Not because Pods are unimportant — the Pod is still the unit of everything — but because *being the thing that gets created for you* is what a Pod is for.

*[cross-bearing: see Ch 14 §2 — a Helm chart's job is to template this object]*

---

## ⚪ §2 — A Loop You Can Watch Working

Chapter 3 promised you a control loop you could watch working in real time, and named the ReplicaSet as the place you'd see it *[cross-bearing: see Ch 3 §6 — the control loop]*. This is that.

A ReplicaSet is defined with a selector that specifies how to identify Pods it can acquire, a number of replicas indicating how many Pods it should be maintaining, and a Pod template specifying the data of new Pods it should create to meet the replica count criteria. It fulfills its purpose by creating and deleting Pods as needed to reach the desired number [source: k8s-docs-replicaset-2026-08-24].

Line that up against Chapter 3's thermostat and the mapping is exact:

| Control loop (Ch 3) | ReplicaSet |
|---|---|
| Desired state | `.spec.replicas` — the number you asked for |
| Current state | The number of Pods matching its selector that actually exist |
| Action on a gap | Create Pods, or delete them |

You don't need to be told to feel the recognition. You should be able to see it.

### The demonstration

This is the whole reason this section is separate: the loop is *visible*, and it takes two commands to see it.

Delete a Pod that a ReplicaSet owns. Then list the Pods.

```
$ kubectl delete pod web-7d4b9c-x8k2q
pod "web-7d4b9c-x8k2q" deleted

$ kubectl get pods
NAME                     READY   STATUS              AGE
web-7d4b9c-4mnzp         1/1     Running             12m
web-7d4b9c-9tvw6         1/1     Running             12m
web-7d4b9c-qh7bl         0/1     ContainerCreating   2s
```

Nobody triggered that third Pod. Nothing was scheduled. No script ran. A gap appeared between "three wanted" and "two exist," and a loop that was already running noticed and closed it. Note the name: `qh7bl`, not `x8k2q`. This is not the deleted Pod recovered. It is a *different Pod*, with a different UID, built from the same template — exactly the replacement behaviour Chapter 5 described [source: k8s-docs-pod-lifecycle-2026-08-23].

This is also the difference between a ReplicaSet and a bare Pod, stated in the docs in one line: unlike the case where a user directly created Pods, a ReplicaSet replaces Pods that are deleted or terminated for any reason, such as node failure or disruptive node maintenance like a kernel upgrade [source: k8s-docs-replicaset-2026-08-24].

### Scaling is the same field, from the other side

Horizontal scaling means changing the number of replicas [source: k8s-docs-autoscaling-2026-08-23], and `kubectl scale` is a first-class verb for exactly that — update the size of the specified deployment [source: k8s-docs-kubectl-overview-2026-08-23]. A ReplicaSet can be scaled up or down by simply updating the `.spec.replicas` field [source: k8s-docs-replicaset-2026-08-24].

```
$ kubectl scale deployment/web --replicas=5
deployment.apps/web scaled
```

Now look at what the loop sees. You asked for five; three exist. Gap of two, close it.

And when a Pod died a moment ago: you asked for three; two existed. Gap of one, close it.

The loop cannot tell those situations apart, and doesn't try to.

> ⚓ **Worth Securing:** Self-healing and scaling are the same operation. There is no "recovery mode" that switches on when something fails. The loop only ever sees a number it wanted and a number it has, and it only ever does one thing about the difference. Everything that looks like resilience in Kubernetes is this, wearing a different name.

> 🔭 **Closer Look:** The controller doesn't create Pods itself. Built-in controllers manage state by interacting with the cluster API server — the Job controller, for instance, does not run any Pods or containers itself; instead it tells the API server to create or remove Pods, and other components in the control plane act on that new information [source: k8s-docs-controllers-2026-08-23]. Chapter 3 established that nobody is in charge. It stays true at this altitude: the ReplicaSet controller is not a supervisor process holding your Pods. It's a program writing to an API.

### One name to hold, then move on

When the thing writing `.spec.replicas` isn't you, it's usually a **HorizontalPodAutoscaler** — an API resource plus a controller that periodically adjusts the desired scale of its target to match observed metrics such as average CPU utilization [source: k8s-docs-hpa-2026-08-24]. A ReplicaSet can itself be a target for an HPA [source: k8s-docs-replicaset-2026-08-24].

That's the whole introduction it gets here. The autoscaling landscape — what feeds an HPA, and what the other autoscalers do — belongs where there's a competency waiting for it *[cross-bearing: see Ch 13 §4 — metrics-server as the HPA's input]* *[cross-bearing: see Ch 17 §5 — the autoscaling landscape]*.

Two forward notes before we leave the loop. The Pod this loop just created still has to be *placed* somewhere, and sometimes it can't be *[cross-bearing: see Ch 7 §1 — scheduling and the unschedulable Pod]*. And the churn you just watched — Pods appearing and disappearing with different names each time — is precisely why something in the cluster has to provide a stable name that outlives them *[cross-bearing: see Ch 9 §1 — why a Service exists]*.

---

## 🔵 §3 — How a Controller Knows Its Own

Chapter 4 taught label selectors as the universal join and listed four places they're used. It also told you a ReplicaSet knows which Pods are *its* Pods by selector, and sent you here for the mechanism *[cross-bearing: see Ch 4 §5 — label selectors as the universal join]*. Here it is — plus a consequence Chapter 4 didn't state.

### Membership is a query

A ReplicaSet does not track its Pods by name. It does not hold a list. It has a `.spec.selector`, which is a label selector, and its Pods are whichever Pods match it — the labels used to identify potential Pods to acquire [source: k8s-docs-replicaset-2026-08-24].

You already have the machinery for this. `matchLabels` is a map of key/value pairs, equivalent to `matchExpressions` with operator `In`; `matchExpressions` lets you build more sophisticated selectors from a key, a list of values, and an operator relating them; when both are specified the result is ANDed [source: k8s-docs-labels-selectors-2026-08-23] [source: k8s-docs-daemonset-2026-08-24]. The join itself is drawn in `ch04-fig03-labels-selectors-join`, and it hasn't changed — this is that same figure with a ReplicaSet on the left and Pods on the right.

> **Before reading on:** Suppose a Deployment's Pod template applies the label `app: web`, but its selector looks for `app: frontend`. The controller creates a Pod. What happens next? Work it through before you read on — the answer follows from what you already know.

Here's the derivation. The controller creates a Pod carrying `app: web`. Then it looks for Pods matching `app: frontend` and finds none. Current state is zero; desired state is three. It creates another Pod. That one also doesn't match. It creates another. And another. The Pods are real, running, and consuming resources, and the controller cannot see a single one of them.

Kubernetes closes this particular door at the API. In a ReplicaSet, `.spec.template.metadata.labels` must match `spec.selector`, or the object will be rejected [source: k8s-docs-replicaset-2026-08-24]. The same rule holds for a Deployment: `.spec.selector` must match `.spec.template.metadata.labels`, or it will be rejected by the API [source: k8s-docs-deployment-spec-fields-2026-08-24], and for a DaemonSet, where config with the two not matching is rejected [source: k8s-docs-daemonset-2026-08-24].

The validation is a kindness. The *principle* is what you need to carry: because membership is computed rather than recorded, the labels a controller stamps on its own Pods have to satisfy the question it will later ask about them.

> **★ Fixed Point**
>
> **A controller's Pods are the Pods that match its selector. Membership is a query, not a list — which is why the Pod template's labels must satisfy the selector, and why two controllers whose selectors overlap are a hazard rather than a curiosity.**

### Ownership, and what it buys

Selectors answer "which Pods should I be looking at." Ownership answers "which Pods am I responsible for," and it's a separate mechanism.

A ReplicaSet is linked to its Pods via the Pods' `metadata.ownerReferences` field, which specifies what resource the current object is owned by. All Pods acquired by a ReplicaSet carry the owning ReplicaSet's identifying information in that field, and it is through this link that the ReplicaSet knows the state of the Pods it's maintaining [source: k8s-docs-replicaset-2026-08-24]. More broadly: many objects in Kubernetes link to each other through owner references, which tell the control plane which objects are dependent on others [source: k8s-docs-garbage-collection-2026-08-24].

Ownership is different from the labels-and-selectors mechanism, and the docs say so explicitly — using a Service and its EndpointSlices as the example, where labels determine *which* EndpointSlices belong to the Service and owner references keep different parts of Kubernetes from interfering with objects they don't control [source: k8s-docs-garbage-collection-2026-08-24].

What owner references buy you is **cascading deletion**. Kubernetes checks for and deletes objects that no longer have owner references — like the Pods left behind when you delete a ReplicaSet — and when you delete an object you can control whether its dependents are deleted automatically [source: k8s-docs-garbage-collection-2026-08-24]. In practice: delete the Deployment, and the ReplicaSets and Pods go with it. To delete a ReplicaSet and all of its Pods, use `kubectl delete`; the garbage collector automatically deletes all of the dependent Pods by default [source: k8s-docs-replicaset-2026-08-24].

That's the associate-tier fact. The machinery underneath it — foreground versus background cascading deletion, finalizers, the `blockOwnerDeletion` field — is real and documented [source: k8s-docs-garbage-collection-2026-08-24] and is not what you need here.

### Adoption, and the hazard it implies

The selector mechanism has a consequence that surprises people the first time they meet it. A ReplicaSet identifies new Pods to acquire using its selector: if there's a Pod that has no owner reference, or whose owner reference is not a controller, and it matches a ReplicaSet's selector, it will be immediately acquired by that ReplicaSet [source: k8s-docs-replicaset-2026-08-24].

Immediately. Not "on the next reconcile as a special case" — this *is* the reconcile.

The docs work the consequence through: if you create bare Pods carrying labels that match a ReplicaSet's selector *after* the ReplicaSet has already reached its replica count, the new Pods are acquired and then immediately terminated, because the ReplicaSet is now over its desired count. If you create them *before*, the ReplicaSet adopts them and only creates as many new Pods as it needs to reach the count [source: k8s-docs-replicaset-2026-08-24]. Which is why the docs recommend making sure bare Pods don't carry labels matching the selector of one of your ReplicaSets.

This is also the sharpest possible demonstration that membership is a query. The ReplicaSet is not limited to owning Pods created from its own template. It owns what matches.

> 🪝 **Snag:** Two controllers whose selectors overlap will fight over the same Pods — and neither one reports an error. Each sees a count that keeps changing for reasons it didn't cause, and each keeps acting on it. It looks like flapping, not like a configuration mistake, which is why it's expensive to diagnose. The ReplicaSet docs put the rule as a one-line warning about the Pod template's labels: *be careful not to overlap with the selectors of other controllers, lest they try to adopt this Pod* [source: k8s-docs-replicaset-2026-08-24].

The practical rule: give each workload a label that is genuinely unique to it, and don't hand-write labels that overlap across controllers. This is the fifteen seconds of care that saves the afternoon.

One forward note. A Service selects its backends with the same mechanism — a *different* controller reading the *same* labels *[cross-bearing: see Ch 9 §2 — a Service selects its backends by label]*. That is not a conflict. It's the point of a shared identifying vocabulary, and it's the thing Bearings #1 will ask you about. And deleting a workload does not automatically delete everything it merely *referenced* — a distinction that becomes load-bearing with storage *[cross-bearing: see Ch 12 §3 — what deletion does and does not remove]*.

---

## ☆ Taking Your Bearings #1

*Five questions on what holds the intent and how it finds its Pods. Items 4 and 5 reach back to earlier chapters.*

**1.** Name the three layers between a Deployment and a running container process, and say which layer holds the replica count and which holds the Pod template.

**2.** You delete a Pod that a ReplicaSet owns. Describe what happens and what caused it.

**3.** A Deployment's template labels do not match its selector, and somehow the object was created anyway. Predict the state of the cluster sixty seconds later.

**4.** *[retrieval: ch3]* Chapter 3 gave you a loop with two states and an action. Fill in all three for a ReplicaSet, using the actual field name for the desired state.

**5.** 🔵 *[retrieval: ch4]* Chapter 4 listed four things that use label selectors and told you a ReplicaSet was one of them. Now that you've seen it work: in Chapter 9, a Service will select Pods with the same mechanism. What would it mean for one Pod to be selected by both a ReplicaSet and a Service at once?

---

**Answers with Explanations:**

**1. Deployment → ReplicaSet → Pod. The ReplicaSet holds the replica count; the Deployment holds the Pod template (and the update strategy).**

Why the tempting wrong answers are wrong:

- **"Deployment → Pod" (two layers)** is the most common compression, and it is worth stopping on, because §4 is unintelligible without the middle layer. If a Deployment owned Pods directly, there would be nowhere for two versions of your application to coexist during an update. The ReplicaSet layer is exactly what makes a rolling update expressible: the Deployment scales one ReplicaSet down while scaling another up.
- **"The Deployment holds the count, the ReplicaSet holds the template"** inverts the division of labour. The count is what a ReplicaSet *is for* — maintaining a stable set of replica Pods [source: k8s-docs-replicaset-2026-08-24]. The template and update strategy sit above it because they're what a *change* is expressed in.

**2. A replacement Pod appears, with a different name and a different UID, and nothing triggered it.**

The correct answer turns on the absence of a trigger. A gap opened between `.spec.replicas` and the number of matching Pods, and the ReplicaSet's control loop closed it by creating a Pod from the template [source: k8s-docs-replicaset-2026-08-24]. If your answer included the word "restarted," reread §2 — the Pod was not restarted. It was replaced.

**3. A growing population of Pods the controller cannot see, and a replica count that is never satisfied.**

Each created Pod carries the template's labels; the controller then queries for the selector's labels and finds nothing; current state stays at zero; it creates another. In practice you will not reach this state through the API, because the API rejects a Deployment whose selector doesn't match its template labels [source: k8s-docs-deployment-spec-fields-2026-08-24]. Knowing *why* that validation exists is the point of the question.

**4.** Desired state: `.spec.replicas`. Current state: the number of Pods currently matching the ReplicaSet's selector. Action: create Pods, or delete Pods, until the two agree [source: k8s-docs-replicaset-2026-08-24]. If you wrote "the number of Pods it created" for current state, you've described a list rather than a query — see §3.

**5. Nothing unusual. They are independent queries over the same labels, and the Pod is simply a member of two sets.**

This is the checkpoint's hardest item and it's doing setup work for Chapter 9. A Pod's labels are not owned by any one controller. A ReplicaSet asks "which Pods match `app: web`?" to decide whether to create more; a Service asks the identical question to decide where to send traffic. Neither knows about the other; neither needs to. The label vocabulary is shared infrastructure, and that's precisely what makes it a *join* rather than a pointer. (Contrast this with §3's overlapping-selector hazard, which is two controllers of the *same kind* both trying to manage the same Pods — a genuine conflict, because both will act on the count.)

---

**Checkpoint: You've Now Mastered**

✓ The Deployment → ReplicaSet → Pod ownership chain, and which layer holds what
✓ Why "delete a Pod, get a Pod" is the same operation as "scale from 3 to 5"
✓ Selector-based membership, and why the template's labels must satisfy the selector
✓ Owner references, cascading deletion, and controller adoption

Next: what happens when you change the template that all of this is copying from. That's the chapter's densest section, and it's where Chapter 5's probes stop being a health-checking feature.

---

## 🔵 §4 — Changing the Fleet Under Way

Everything so far has been about holding a fleet steady. This is about changing it while it's carrying traffic.

### The mechanism

You declare the new state of the Pods by updating the PodTemplateSpec of the Deployment. A new ReplicaSet is created, and the Deployment manages moving the Pods from the old ReplicaSet to the new one at a controlled rate [source: k8s-docs-deployment-2026-08-23].

Stop on that. *Two ReplicaSets exist at once.* One is scaling down; one is scaling up; the Deployment is the layer holding both. This is §1's three-layer chain earning its keep. A reader who has the chain finds the rolling update obvious — of course you'd need somewhere for the old count and the new count to live separately. A reader who thinks a Deployment owns Pods directly finds it magic.

<!-- FIGURE: ch06-fig02-rolling-update-maxsurge-maxunavailable -->
```
  Pods
   12 ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  surge ceiling (10 + 25%)
      │        ███░░░
   10 ┼────────███░░░───────────────────────  desired: 10
      │  █████████░░░░░░
      │  ██████░░░░░░░░░░░░
    8 ┄┄│┄┄██████┄┄┄┄░░░░░░░░░░┄┄┄┄┄┄┄┄┄┄┄┄┄  availability floor (10 − 25%)
      │  ██████         ░░░░░░░░░
      │  ██████             ░░░░░░░░░░
    0 └──────────────────────────────────────▶ time

        ██ old version        ░░ new version

     total (old + new)  never rises above the surge ceiling
     available          never falls below the availability floor
```

### The two bounds

`.spec.strategy` specifies the strategy used to replace old Pods by new ones. `.spec.strategy.type` can be `Recreate` or `RollingUpdate`, and **`RollingUpdate` is the default value** [source: k8s-docs-deployment-2026-08-23].

`RollingUpdate` takes two tuning fields, and both accept an absolute number or a percentage of desired Pods:

- **`maxUnavailable`** — the maximum number of Pods that can be unavailable during the update process. The absolute number is calculated from the percentage by *rounding down*. **The default is 25%** [source: k8s-docs-deployment-spec-fields-2026-08-24].
- **`maxSurge`** — the maximum number of Pods that can be created *over* the desired number of Pods. The absolute number is calculated from the percentage by *rounding up*. **The default is 25%** [source: k8s-docs-deployment-spec-fields-2026-08-24].

Neither can be `0` if the other is `0` [source: k8s-docs-deployment-spec-fields-2026-08-24] — which makes sense once you say it out loud: with no headroom above and no slack below, there is no legal move.

Work it numerically once, because the arithmetic is what a question actually asks for and because doing it makes the two names stop being interchangeable.

**Ten replicas. Default strategy. Nothing configured.**

- `maxSurge` = 25% of 10 = 2.5, rounded **up** = **3**. Total Pods may reach 13.
- `maxUnavailable` = 25% of 10 = 2.5, rounded **down** = **2**. At least 8 must stay available.

The Kubernetes API reference works the same shape with a 30% example: with `maxSurge` at 30%, the new ReplicaSet can scale up immediately such that total old and new Pods do not exceed 130% of desired; with `maxUnavailable` at 30%, the old ReplicaSet can scale down to 70% of desired immediately, and the total available at all times during the update is at least 70% of desired [source: k8s-docs-deployment-spec-fields-2026-08-24].

> 🪢 **Mnemonic:** Surge is above the line. Unavailable is below it.

> **★ Fixed Point**
>
> **`RollingUpdate` is the default strategy. `maxSurge` and `maxUnavailable` both default to 25%. `Recreate` kills all existing Pods before any new ones are created.**

### Recreate, and why it isn't a mistake

`Recreate` is the other strategy: all existing Pods are killed before new ones are created [source: k8s-docs-deployment-2026-08-23]. The API reference is blunter still — *kill all existing pods before creating new ones* [source: k8s-docs-deployment-spec-fields-2026-08-24].

<!-- FIGURE: ch06-fig03-recreate-vs-rolling -->
```
  Recreate
  ────────
   old  ██████████
   new                        ░░░░░░░░░░░░░░░
        ├────────┤ ├────────┤ ├─────────────┤
                   ▲▲▲▲▲▲▲▲▲
                   NOTHING IS AVAILABLE
                   (this window is the whole point)

  RollingUpdate
  ─────────────
   old  ██████████████
   new           ░░░░░░░░░░░░░░░░░░░░░░░░░░░░
        ├──────────────────────────────────┤
                  ▲▲▲▲▲▲▲▲
                  both versions serving

        available count never reaches zero
```

That gap in the upper timeline is downtime, deliberately chosen. It exists because some applications genuinely cannot have two versions running at once — a schema migration that the old code can't read, an exclusive lock on a resource, a licence that permits one active instance. In those cases `Recreate` isn't the wrong answer; it's the correct answer with a known cost, and choosing it consciously is what a practitioner does. Choosing `RollingUpdate` for an application that can't tolerate two concurrent versions is the actual mistake, and it fails in a subtler and more expensive way.

> **Dead Reckoning:** `.spec.strategy.type` accepts two values: `Recreate` and `RollingUpdate`. `RollingUpdate` is the default. Under `Recreate`, all existing Pods are killed before any new Pod is created. Under `RollingUpdate`, updating `.spec.template` creates a new ReplicaSet; the Deployment scales the new ReplicaSet up and the old one down at a controlled rate, bounded by two fields. `.spec.strategy.rollingUpdate.maxSurge` caps how many Pods may exist above `.spec.replicas`; it defaults to 25% and rounds up when given as a percentage. `.spec.strategy.rollingUpdate.maxUnavailable` caps how many Pods may be unavailable; it defaults to 25% and rounds down when given as a percentage. Neither may be 0 if the other is 0. `.spec.minReadySeconds` is the minimum number of seconds a newly created Pod must be ready, without any container crashing, for it to count as available; it defaults to 0. `.spec.progressDeadlineSeconds` is how long the Deployment may go without progressing before the system reports failure; it defaults to 600 [source: k8s-docs-deployment-2026-08-23] [source: k8s-docs-deployment-spec-fields-2026-08-24].

### What makes it safe

A gradual replacement is not automatically a safe one. Replacing ten Pods slowly with ten broken Pods is still replacing ten Pods with ten broken Pods; it just takes longer to finish being wrong.

The thing that makes it safe is that a new Pod does not count as *available* until it reports ready. Kubernetes marks a Deployment as progressing when new Pods become ready or available — available meaning ready for at least `minReadySeconds` [source: k8s-docs-deployment-spec-fields-2026-08-24]. And `minReadySeconds` is precisely that: the minimum number of seconds for which a newly created Pod should be ready, without any of its containers crashing, for it to be considered available; it defaults to 0, meaning the Pod counts as available as soon as it is ready [source: k8s-docs-deployment-spec-fields-2026-08-24].

Now connect it to Chapter 5. A readiness probe indicates whether a container is ready to respond to requests; when it fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services matching the Pod [source: k8s-docs-pod-lifecycle-2026-08-23].

Put the two together and the safety property falls out:

**A new version that never becomes ready never displaces the old one.** The new Pods start. They don't report ready. They therefore don't count as available. The Deployment can't scale down the old ReplicaSet any further without breaching `maxUnavailable` — so it doesn't. The rollout stalls, both ReplicaSets alive, old Pods still serving, and *nobody outside the cluster notices anything at all.*

That's the promise Chapter 5 made when it said probes are what make a rolling update safe *[cross-bearing: see Ch 5 §7 — readiness probes]*. It's the moment probes stop being a health-checking feature and become a release-safety mechanism. If you write no readiness probe, you have opted out of this — a Pod with no readiness probe is ready as soon as its containers are running, whether or not the application inside can serve anything.

> 🪝 **Snag:** A stalled rollout is not a failed one, and it does not clean itself up. The Deployment sits there with both ReplicaSets alive, waiting for a Pod that will never become ready. Deployments can get stuck trying to deploy a newest ReplicaSet without ever completing, from causes including insufficient quota, readiness probe failures, image pull errors, insufficient permissions, and limit ranges [source: k8s-docs-deployment-spec-fields-2026-08-24]. `.spec.progressDeadlineSeconds` — 600 by default — is what eventually turns that silence into a reported condition: `type: Progressing`, `status: "False"`, `reason: ProgressDeadlineExceeded` [source: k8s-docs-deployment-spec-fields-2026-08-24]. Note the wording: the controller *keeps retrying*. The deadline reports; it does not abort.

The signal exists. Reading it — what to run, which events to look at, what to do next — is diagnosis, and diagnosis has its own chapter *[cross-bearing: see Ch 13 §3 — diagnosing a stuck rollout]*.

One more forward pointer, and only one. What you've learned here is rolling-update *mechanics*: two strategy values, two bounds, the readiness dependency. The strategy *vocabulary* that gets built on top of these mechanics — blue/green, canary, A/B — arrives later, where there's a delivery tool with the hooks to implement it *[cross-bearing: see Ch 15 §4 — deployment strategy vocabulary]*.

---

## 🔵 §5 — Every Rollout Is a Revision

Section 4 changed the fleet. This is what the cluster wrote down about it.

### The rule, and its exactness is the content

A Deployment's revision is created when a rollout is triggered — and a new revision is created **if and only if** the Deployment's Pod template (`.spec.template`) is changed. Other updates, such as scaling the Deployment, do not create a Deployment revision [source: k8s-docs-deployment-2026-08-23].

That "if and only if" is the section's whole content, and it's precisely the shape a recognition exam builds a question from, because the intuitive answer ("any change to the Deployment") is wrong and the correct answer is one clause long.

Scale from three to six: no revision. Change the image tag: revision. Change an environment variable in the template: revision. Change `maxSurge`: no revision — it's a strategy field, not a template field. Change a label on the template's Pods: revision, because the template changed.

The test is not "did I edit the Deployment." It is "did I edit `.spec.template`."

> **★ Fixed Point**
>
> **A new revision is created if and only if `.spec.template` changes. Scaling does not create a revision.**

### The verb surface

`kubectl rollout` manages the rollout of a resource; valid resource types include deployments, daemonsets, and statefulsets [source: k8s-docs-kubectl-overview-2026-08-23] [source: k8s-docs-kubectl-rollout-2026-08-24]. The subcommand set is small and closed:

| Command | What it does |
|---|---|
| `kubectl rollout status` | Show the status of the rollout |
| `kubectl rollout history` | View rollout history |
| `kubectl rollout undo` | Undo a previous rollout |
| `kubectl rollout pause` | Mark the provided resource as paused |
| `kubectl rollout resume` | Resume a paused resource |
| `kubectl rollout restart` | Restart a resource |

[source: k8s-docs-kubectl-rollout-2026-08-24]

`kubectl rollout history deployment/<name>` shows the revisions; `kubectl rollout undo deployment/<name>` rolls back to the previous revision, and `--to-revision=<n>` goes to a specific one [source: k8s-docs-deployment-2026-08-23].

**Pause and resume** need their motivation attached or they read as an arbitrary pair. When you update a Deployment, or plan to, you can pause rollouts before you trigger one or more updates, then resume when you're ready to apply the changes — this lets you apply multiple fixes in between pausing and resuming without triggering unnecessary rollouts [source: k8s-docs-deployment-2026-08-23].

Concretely: you need to change the image, an environment variable, and the resource limits. Applied one at a time, each edit touches `.spec.template` and each therefore starts a rollout — three rollouts, three revisions, three sets of Pod churn, and the first two are rolling out versions nobody wanted. Pause first, make all three edits, resume: one rollout, one revision.

> ⚓ **Worth Securing:** `pause` before a batch of edits. It is the difference between one rollout and four, and it costs one command.

### What's kept

By default, all of a Deployment's rollout history is kept in the system so that you can roll back any time you want — changeable by modifying the revision history limit [source: k8s-docs-deployment-2026-08-23]. `.spec.revisionHistoryLimit` specifies the number of old ReplicaSets to retain to allow rollback; **by default, 10 old ReplicaSets will be kept**. Setting it to zero means all old ReplicaSets with 0 replicas are cleaned up — and in that case a new Deployment rollout cannot be undone, since its revision history is cleaned up [source: k8s-docs-deployment-spec-fields-2026-08-24].

That's worth one clause because "can I still roll back?" is a real question at a real bad moment, and the default answer is yes, ten deep.

> ⚠ **Navigational Hazards**
>
> **The revision rule catches people, and it catches them in two directions.**
>
> **Hazard one: "I changed the Deployment, so there must be a new revision."** Scaling is the counterexample that matters, because scaling is the most common Deployment edit there is. You go from three replicas to six, run `kubectl rollout history`, and see exactly the same revision list you saw before. Nothing is broken. Scaling does not change the Pod template, so it does not create a revision [source: k8s-docs-deployment-2026-08-23].
>
> **Hazard two, which follows from it: "`rollout undo` will put my replica count back."** It will not. `rollout undo` restores a previous *Pod template*. Your replica count is not in the Pod template. If you scaled up and then rolled back an unrelated image change, you will still have six replicas afterward — and if you were expecting three, you will spend a while looking for the bug. There isn't one.
>
> The clean mental model: **revisions are a history of what your Pods are, not of how many.**

### What a rollback actually is

Rolling back is not undoing an edit, and it is not restoring a backup. It is setting the Pod template to a previous value and letting the same rolling update run in the other direction — same controller, same two ReplicaSets, same `maxSurge` and `maxUnavailable`, same readiness gate. The Deployment doesn't have a special reverse gear. It has one gear, and rollback points it at an older template.

The old ReplicaSet is still there — that's what `revisionHistoryLimit` is retaining [source: k8s-docs-deployment-spec-fields-2026-08-24] — so "rolling back" is largely a matter of scaling it back up while scaling the current one down.

Say that precisely, because two later chapters use the same word for different mechanisms. Helm's rollback operates on releases, not on Pod templates *[cross-bearing: see Ch 14 §5 — Helm rollback versus Deployment rollback]*. And a GitOps controller's rollback means reverting the committed configuration and letting reconciliation carry it into the cluster *[cross-bearing: see Ch 15 §3 — rollback to any committed configuration]*. Three mechanisms, one word. Knowing what *this* one is is what makes the other two distinguishable rather than confusing.

The `kubectl rollout` verbs exist here because the concepts need names attached to them. The command surface itself — flags, output formats, what else `kubectl` can do — belongs to its own chapter *[cross-bearing: see Ch 8 §2 — the kubectl command surface]*.

---

## ☆ Taking Your Bearings #2

*Five questions on changing the fleet and what a change is recorded as. Item 4 reaches back to Chapter 5.*

**1.** A Deployment with ten replicas is updated using default strategy settings. What is the largest number of Pods that may exist during the update, and the smallest number that must be available?

**2.** 🟡 ⚠️ **This one is intentionally hard, and most people get it wrong the first time.** You scale a Deployment from three replicas to six, then run `kubectl rollout history`. How many revisions do you see, and why?

**3.** Your application cannot run two versions at once because of a schema lock. Which strategy do you choose, and what exactly are you accepting?

**4.** *[retrieval: ch5]* You push a broken image. The new Pods start but never report ready. Describe what the Deployment does, and what the users of the service experience.

**5.** You need to change the image, an environment variable, and the resource limits on one Deployment. How do you do it as one rollout rather than three, and what are the two commands?

---

**Answers with Explanations:**

**1. Thirteen may exist; eight must remain available.**

`maxSurge` defaults to 25%: 25% of 10 is 2.5, rounded **up** to 3, so total may reach 13. `maxUnavailable` defaults to 25%: 25% of 10 is 2.5, rounded **down** to 2, so at least 8 must stay available [source: k8s-docs-deployment-spec-fields-2026-08-24].

Why the tempting wrong answers are wrong:

- **"Twelve and eight"** rounds surge down. Surge rounds up; unavailable rounds down. The asymmetry is deliberate — both directions err toward keeping more capacity available.
- **"Twelve and seven"** transposes the two bounds. This is the single most common error on this material and it's why the mnemonic exists: surge is above the line, unavailable is below it.
- **"Twelve and ten" (25% applied jointly)** treats the pair as one budget split between them. They're independent bounds on two different quantities — one caps *total*, the other floors *available*.

**2. One revision. The one that was already there.**

Scaling does not change `.spec.template`, and a new revision is created if and only if the Pod template changes [source: k8s-docs-deployment-2026-08-23]. Your Pods are identical before and after; there are simply more of them. There is nothing to record.

**How'd you do?** If you answered "two," you're in the majority, and you've now met the misconception at the cost of one question instead of one production incident. The intuition that "I changed the Deployment, so something got recorded" is reasonable and wrong. Reread §5's hazards block; this exact distinction is a recognition-exam favourite precisely because the intuitive answer is so clean.

**3. `Recreate`, and you are accepting a window of total unavailability as a deliberate cost.**

Under `Recreate`, all existing Pods are killed before new ones are created [source: k8s-docs-deployment-2026-08-23]. There will be a period during which zero Pods are serving. That is not a failure of the strategy; it is the strategy. You choose it when running two versions concurrently would be *worse* than being briefly down — which, with an exclusive schema lock, it is. A wrong answer here is any answer that treats `Recreate` as a misconfiguration.

**4. *[retrieval: ch5]* The rollout stalls with both ReplicaSets alive, the old Pods keep serving, and users see nothing.**

The new Pods start but never pass readiness. A Pod that isn't ready doesn't count as available [source: k8s-docs-deployment-spec-fields-2026-08-24], and a Pod that isn't ready has its address removed from the endpoints of matching Services [source: k8s-docs-pod-lifecycle-2026-08-23]. The Deployment cannot scale the old ReplicaSet down further without breaching `maxUnavailable`, so it stops. The old version is still there, still ready, still receiving traffic.

This is the item that converts probes from a health feature into a release-safety mechanism. The broken deploy did not take down the service — it *failed to happen*.

Note what the answer key deliberately doesn't cover: how you find out this occurred. Naming the stall is this chapter's job; the diagnostic procedure is Chapter 13's *[cross-bearing: see Ch 13 §3 — diagnosing a stuck rollout]*.

**5. `kubectl rollout pause`, make all three edits, `kubectl rollout resume`.**

Pausing before the edits means the three template changes accumulate and produce a single rollout on resume, rather than three rollouts as each edit lands. The documented motivation is exactly this: applying multiple fixes between pausing and resuming without triggering unnecessary rollouts [source: k8s-docs-deployment-2026-08-23]. Without the pause you get three revisions, and two of them are versions nobody intended to run.

---

**Checkpoint: You've Now Mastered**

✓ `RollingUpdate` versus `Recreate`, and when downtime is the right trade
✓ `maxSurge` and `maxUnavailable` — what they bound, and their defaults
✓ Why readiness is what makes a gradual rollout a safe one
✓ The if-and-only-if revision rule, and what a rollback actually does

That's the Deployment arc, start to finish. **This is the natural place to stop if you're splitting the chapter across two sessions.** What follows is the rest of the workload family and what the whole pattern turns into.

---

## 🔵 §6 — When Pods Are Not Interchangeable

Everything up to here has quietly assumed something. Time to name it.

A Deployment's Pods are **interchangeable**. That is not incidental — it's the reason a template and a count are sufficient to describe the entire workload. The Kubernetes docs make it a defining condition: a Deployment is a good fit for managing a stateless application workload on your cluster, *where any Pod in the Deployment is interchangeable and can be replaced if needed* [source: k8s-docs-workloads-2026-08-23]. Any Pod can be replaced by any other, so "three of these" is a complete specification.

Now the question Soundings #4 planted: what if they aren't?

What if this one is the primary and that one is the replica? What if each one holds data that belongs to it specifically, and its hostname is written into somebody else's replication configuration? Then "three of these" is not a specification at all. It's a count of things that happen to look similar.

### The resource

A **StatefulSet** runs a group of Pods and maintains a sticky identity for each of them — useful for applications that need persistent storage or a stable, unique network identity [source: k8s-docs-statefulset-2026-08-24].

The docs draw the contrast in one sentence, and it's worth reading slowly: like a Deployment, a StatefulSet manages Pods that are based on an identical container spec; *unlike* a Deployment, a StatefulSet maintains a sticky identity for each of its Pods — these Pods are created from the same spec, but **are not interchangeable**: each has a persistent identifier that it maintains across any rescheduling [source: k8s-docs-statefulset-2026-08-24].

Same spec. Not interchangeable. Those two facts sitting together is the entire concept.

That identity has three parts [source: k8s-docs-statefulset-2026-08-24]:

- **An ordinal index.** For a StatefulSet with N replicas, each Pod is assigned an integer ordinal, unique over the set, from 0 through N-1.
- **A stable network identity.** Each Pod derives its hostname from the StatefulSet's name and its ordinal: `$(statefulset name)-$(ordinal)`. A StatefulSet named `web` with three replicas produces Pods named `web-0`, `web-1`, `web-2` — every time, on every reschedule.
- **Stable storage.** For each `volumeClaimTemplate` entry, each Pod receives one PersistentVolumeClaim, and the same claim is bound to that Pod throughout its lifecycle.

<!-- FIGURE: ch06-fig05-statefulset-vs-deployment-identity -->
```
  DEPLOYMENT — Pods are interchangeable
  ─────────────────────────────────────
     web-7d4b9c-4mnzp   web-7d4b9c-9tvw6   web-7d4b9c-x8k2q
          │                  │                  │  dies
          │                  │                  ▼
          │                  │            web-7d4b9c-qh7bl
          │                  │            (different name,
          │                  │             different UID)
     nothing depended on which one it was


  STATEFULSET — Pods have identity
  ────────────────────────────────
        db-0              db-1              db-2  dies
         │                 │                 │
      ┌──┴──┐           ┌──┴──┐           ┌──┴──┐
      │ PVC │           │ PVC │           │ PVC │   ← storage belongs
      │  0  │           │  1  │           │  2  │     to the IDENTITY,
      └─────┘           └─────┘           └─────┘     not to the Pod
                                             ▲
                                             │ same name, same claim
                                          db-2 (replacement reattaches)
```

Also worth knowing: when a StatefulSet is deployed, Pods are created sequentially in order from 0 to N-1, and when they're deleted they're terminated in reverse order, N-1 down to 0. Before a scaling operation is applied to a Pod, all of its predecessors must be Running and Ready [source: k8s-docs-statefulset-2026-08-24]. Ordering, too, is part of identity — you cannot bring up a replica before the primary it replicates from.

> **★ Fixed Point**
>
> **The property that decides Deployment versus StatefulSet is *interchangeability*, not disk. A StatefulSet is for related Pods with stable identities, each typically paired with its own durable storage.**

> 🪝 **Snag:** The wrong version of this, which most people arrive holding, is: *"if my application writes to disk, I need a StatefulSet."* It isn't true, and believing it will send you to the harder resource for no benefit. A stateless web server can write to disk. A Deployment's Pod can mount a volume — Pods can specify shared storage volumes, and any Pod can use a PersistentVolumeClaim [source: k8s-docs-pods-2026-08-24] [source: k8s-docs-volumes-2026-08-23]. The question is never "does it write." It's "if I destroyed this Pod and built an identical one, would anything care *which one it was*?" If nothing cares, it's a Deployment, disk or no disk. If something cares — a hostname in a replication config, a specific shard of data, an election that assumed a fixed member list — that's a StatefulSet.

> **Extended Analogy:**
>
> Consider two ways of crewing a vessel.
>
> On a Deployment crew, any bosun's mate can stand any watch. If one falls ill, another takes the post, reads the same orders, does the same work. The roster is a number and a description: *four hands who can do this*. Losing one is a staffing question, not a continuity question. Nothing in the ship's operation depends on which particular person is holding the line.
>
> On a StatefulSet crew, the pilot who knows this harbour is the pilot who knows *this* harbour. Her replacement is not another pilot; her replacement is someone who has to have learned the same channel, and until they have, the post is not filled — it is merely occupied. The chart she's been annotating for six years is *hers*, and it needs to reach whoever stands in that berth next, or the knowledge is gone.
>
> Both crews are three or four people. Only one of them can be described by a count.

### The loop this section is deliberately leaving open

You've now met the storage half of that identity — each Pod matched with its own persistent volume — and you have been given none of the machinery behind it. That's on purpose, and you should know it rather than wonder what got skipped.

PersistentVolume, PersistentVolumeClaim, StorageClass, access modes, and how the pairing is actually provisioned all belong to the storage chapter, where they get the room they need *[cross-bearing: see Ch 11 §4 — PersistentVolumeClaims and StatefulSet storage]*. What this chapter owes you is the *taxonomy*: which resource, and why. What that chapter owes you is how the storage actually works. Two of the StatefulSet's documented limitations are pure Chapter 11 material and worth flagging now so they don't surprise you later: the storage must either be provisioned by a PersistentVolume provisioner based on the requested storage class or pre-provisioned by an admin, and deleting or scaling down a StatefulSet does **not** delete the associated volumes — deliberately, because data safety is generally more valuable than an automatic purge [source: k8s-docs-statefulset-2026-08-24].

One more open thread, smaller: StatefulSets currently require a **Headless Service** to be responsible for the network identity of the Pods, and you are responsible for creating it [source: k8s-docs-statefulset-2026-08-24]. That's the mechanism behind `db-0` being resolvable by name, and it lives with the rest of Services *[cross-bearing: see Ch 9 §5 — headless Services]*.

Debugging StatefulSets is named explicitly in the exam's troubleshooting competency, and it gets its own treatment *[cross-bearing: see Ch 16 §3 — debugging StatefulSets]*.

---

## ⚪ §7 — One Per Node, and Work That Ends

Three more resources, one defining property each. Then the figure that collects all six. This section is deliberately brisk — taxonomy sections that linger turn into lists.

### DaemonSet: one per node, automatically

A **DaemonSet** defines Pods that provide facilities local to nodes. Every time you add a node to your cluster that matches the specification in a DaemonSet, the control plane schedules a Pod for that DaemonSet onto the new node. Each Pod in a DaemonSet performs a job similar to a system daemon on a classic Unix server [source: k8s-docs-workloads-2026-08-23]. Stated from the other page: a DaemonSet ensures that all (or some) Nodes run a copy of a Pod — as nodes are added to the cluster, Pods are added to them; as nodes are removed, those Pods are garbage collected [source: k8s-docs-daemonset-2026-08-24].

Typical uses, from the docs themselves: running a cluster storage daemon on every node, running a logs collection daemon on every node, running a node monitoring daemon on every node [source: k8s-docs-daemonset-2026-08-24]. The workloads overview groups them by role — a DaemonSet might be fundamental to the operation of your cluster, such as a plugin to run cluster networking; it might help you manage the node; or it could provide optional behaviour that enhances the container platform [source: k8s-docs-workloads-2026-08-23].

Two of those come back later, which is a good reason to hold them concretely now. Networking plugins ship as DaemonSets *[cross-bearing: see Ch 9 §7 — CNI plugins in the cluster]*, and node-level log agents are the canonical observability example *[cross-bearing: see Ch 18 §3 — node-level logging agents]*.

You can narrow the set of nodes. If you specify a `nodeSelector` in the Pod template, the DaemonSet controller creates Pods only on nodes matching that selector; likewise for node affinity. If you specify neither, the controller creates Pods on all nodes [source: k8s-docs-daemonset-2026-08-24]. The Pods still go through scheduling — the controller creates a Pod for each eligible node and the default scheduler binds it — and the controller automatically adds a set of tolerations so DaemonSet Pods can run on nodes that are unschedulable, under disk or memory pressure, or not yet ready [source: k8s-docs-daemonset-2026-08-24]. The mechanism behind those tolerations is a scheduling topic *[cross-bearing: see Ch 7 §5 — taints and tolerations]*.

<!-- AUTHOR-REVIEW: no fetched sentence states verbatim that a DaemonSet has no `replicas` field. The claim is entailed by "The DaemonSet controller creates a Pod for each eligible node" plus the absence of `replicas` from the documented required fields, and independently by the HPA page's statement that horizontal pod autoscaling does not apply to a DaemonSet. Research manifest gap G-6A. Prose below states it as a consequence rather than as a quoted fact — confirm framing at revision. -->

The trap here is reaching for a DaemonSet to "run several copies." A DaemonSet does not take a replica count; its Pod count is a *consequence* of how many nodes are eligible, since the controller creates a Pod for each eligible node [source: k8s-docs-daemonset-2026-08-24]. The clearest corroboration is from the autoscaler: horizontal pod autoscaling does not apply to objects that can't be scaled — for example, a DaemonSet [source: k8s-docs-hpa-2026-08-24]. There's no number to adjust.

### Job: work that ends

A **Job** represents a one-off task that runs to completion and then stops. A Job creates one or more Pods and continues to retry execution until a specified number of them successfully terminate; when that number is reached, the Job is complete [source: k8s-docs-job-2026-08-24]. You can use a Job to define a task that runs to completion, just once [source: k8s-docs-workloads-2026-08-23].

The Job controller was Chapter 3's own worked example of a built-in controller, and it's worth collecting that now: when the Job controller sees a new task, it makes sure that somewhere in your cluster the kubelets on a set of nodes are running the right number of Pods to get the work done — and once the work is done, the Job controller updates the Job object to mark it Finished [source: k8s-docs-controllers-2026-08-23]. Same loop. Different desired state: *completion* rather than *a count* *[cross-bearing: see Ch 3 §6 — the Job controller as a built-in example]*.

Notice what this retroactively justifies. Chapter 5 taught you five Pod phases, and two of them — `Succeeded` (all containers terminated in success and will not be restarted) and `Failed` (all containers terminated, at least one in failure) — had no obvious use, because a long-running service that reaches `Succeeded` has malfunctioned [source: k8s-docs-pod-lifecycle-2026-08-23]. Here they earn their place. Work that ends is work that reaches a terminal phase, and for a Job those two phases are the entire scoreboard *[cross-bearing: see Ch 5 §5 — Pod phases]*.

One field difference follows directly: for a Job, only a `restartPolicy` of `Never` or `OnFailure` is allowed [source: k8s-docs-job-2026-08-24]. `Always` would be a category error — restarting a process that succeeded is precisely what you don't want.

### CronJob: the same Job, on a schedule

A **CronJob** creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24]. You can use a CronJob to run the same Job multiple times according to a schedule [source: k8s-docs-workloads-2026-08-23].

The docs give the cleanest possible mental model: one CronJob object is like one line of a crontab file on a Unix system. It runs a Job periodically on a given schedule, written in Cron format [source: k8s-docs-cronjob-2026-08-24]. The `.spec.schedule` field is required and takes standard five-field cron syntax — `0 3 * * 1` means weekly on a Monday at 3 a.m. [source: k8s-docs-cronjob-2026-08-24]. The `.spec.jobTemplate` defines the Jobs the CronJob creates, and has exactly the same schema as a Job [source: k8s-docs-cronjob-2026-08-24].

So the relationship is nested, not parallel: **a CronJob's output is Jobs.** It doesn't run work; it creates the thing that runs work.

> 🔭 **Closer Look:** A CronJob creates a Job approximately once per execution time of its schedule. The scheduling is approximate — there are circumstances where two Jobs might be created, or no Job might be created. Kubernetes tries to avoid those situations but does not completely prevent them, which is why the docs state that the Jobs you define should be **idempotent** [source: k8s-docs-cronjob-2026-08-24]. If your nightly report generator would double-bill a customer when run twice, that's a design problem the scheduler will eventually find for you.

> **★ Fixed Point**
>
> **DaemonSet: one Pod per matching node, added automatically as nodes join — no replica count. Job: runs to completion, once. CronJob: creates the same Job repeatedly, on a schedule.**

> ⚠ **Navigational Hazards**
>
> **Three confusions live in this section, and they share one root cause.**
>
> **"My app is stateful, so it needs a StatefulSet."** Covered in §6, repeated here because it belongs to the same family: the deciding property is interchangeability, not disk.
>
> **"I need six copies, so I'll use a DaemonSet."** A DaemonSet has no count to set. Its Pod count falls out of node eligibility [source: k8s-docs-daemonset-2026-08-24]. If you want six copies, you want a Deployment; if you want *one on each machine*, you want a DaemonSet — and if the cluster has four nodes today and nine next month, that's a feature.
>
> **"Job or CronJob — aren't they the same thing?"** A Job runs to completion once [source: k8s-docs-job-2026-08-24]. A CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24]. The relationship is that a CronJob *makes* Jobs.
>
> **The root cause of all three:** choosing a resource by what the application **is** rather than by how its Pods need to be **managed**. "It's a database" is a fact about your application. "Its Pods are not interchangeable" is a fact about management, and only the second one selects a resource. "It's a log agent" is a fact about your application; "it needs one instance per machine, including machines that don't exist yet" selects a resource.
>
> Get that ordering right and you don't need to memorize three separate corrections. You need one rule.

### The decision tree

Here's the payoff, and it's the most practically useful artifact in the chapter. Four questions, six resources.

<!-- FIGURE: ch06-fig04-workload-resource-decision-tree -->
```
                    ┌─────────────────────────┐
                    │  Does the work END?     │
                    └───────┬─────────┬───────┘
                       yes  │         │  no
              ┌─────────────┘         └──────────────┐
              ▼                                      ▼
   ┌──────────────────────┐            ┌───────────────────────────┐
   │ Does it repeat on    │            │ Must it run on EVERY node?│
   │ a schedule?          │            └──────┬──────────────┬─────┘
   └────┬────────────┬────┘               yes │              │ no
    yes │            │ no                     ▼              ▼
        ▼            ▼               ┌─────────────┐  ┌──────────────────┐
  ┌──────────┐  ┌──────────┐         │  DaemonSet  │  │ Are the Pods     │
  │ CronJob  │  │   Job    │         └─────────────┘  │ INTERCHANGEABLE? │
  └──────────┘  └──────────┘                          └───┬──────────┬───┘
                                                      yes │          │ no
                                                          ▼          ▼
                                              ┌────────────────┐ ┌─────────────┐
                                              │   Deployment   │ │ StatefulSet │
                                              │ (manages a     │ └─────────────┘
                                              │  ReplicaSet)   │
                                              └────────────────┘
```

Read the question order carefully, because the order is the pedagogy. The tree asks about the **shape of the work** before it asks about the **nature of the application**. Does it end? Does it need to be everywhere? *Then*, and only then, are the Pods interchangeable. A decision tree that opened with "is it stateful?" would reproduce the trap it's supposed to defuse.

This figure is worth photographing. It also belongs on your one-page reference.

---

## 🟡 §8 — The Control Loop, Extended

Chapter 3 closed by promising you'd meet controllers you configure yourself. Chapter 2 named CustomResourceDefinitions as the fourth socket in "Kubernetes defines an interface and lets the ecosystem implement it" and pointed here. Both debts come due now *[cross-bearing: see Ch 3 §6 — controllers you configure yourself]* *[cross-bearing: see Ch 2 §4 — the pluggable-interface pattern]*.

<!-- AUTHOR-REVIEW: the outline's frontmatter flags that chapter-02 line 600 published a cross-bearing pointing at "Ch 6 §3 — CRDs and extending the API", which under this chapter's section ordering is §8. Outline § Open questions #1 recommends a one-token edit in the shipped Chapter 2 text (§3 → §8) rather than renumbering here. Same situation for chapter-01 line 435 (StatefulSets, which land in §6 not §3). Both edits are outside this draft's scope. -->

This is the chapter's abstraction jump. Take it slowly; it's shorter than it looks.

### Start with the resource, not the pattern

A **resource** is an endpoint in the Kubernetes API that stores a collection of API objects of a certain kind — the built-in `pods` resource, for instance, contains a collection of Pod objects [source: k8s-docs-custom-resources-2026-08-23].

A **custom resource** is an extension of the Kubernetes API that is not necessarily available in a default Kubernetes installation; it represents a customization of a particular Kubernetes installation. Custom resources can appear and disappear in a running cluster through dynamic registration, and cluster admins can update them independently of the cluster itself. And here is the clause that makes it click: **once a custom resource is installed, users can create and access its objects using `kubectl`, just as they do for built-in resources like Pods** [source: k8s-docs-custom-resources-2026-08-23].

Nothing about your tooling changes. `kubectl get backup` works the same way `kubectl get pods` does, because as far as `kubectl` is concerned there was never a difference. Many core Kubernetes functions are now built using custom resources, which is what makes Kubernetes as modular as it is [source: k8s-docs-custom-resources-2026-08-23].

### The CRD is the thing that installs it

The **CustomResourceDefinition** API resource allows you to define custom resources. Defining a CRD object creates a new custom resource with a name and schema that you specify, and the Kubernetes API then serves and handles the storage of your custom resource — which frees you from writing your own API server, at the cost of some flexibility compared with API server aggregation [source: k8s-docs-custom-resources-2026-08-23].

You write a schema. The cluster gives you a working API endpoint for it. That's the whole transaction.

### The honest limitation

Here's where people are surprised, and where the section's Fixed Point lives.

On their own, custom resources let you store and retrieve structured data. That is all. A CRD by itself is a shape in a database with an HTTP interface in front of it. You can create objects; you can list them; you can delete them. **Nothing acts on them.**

When you combine a custom resource with a **custom controller**, custom resources provide a true declarative API. The Kubernetes declarative API enforces a separation of responsibilities: you declare the desired state of your resource, and the Kubernetes controller keeps the current state of Kubernetes objects in sync with your declared desired state — in contrast to an imperative API, where you instruct a server what to do [source: k8s-docs-custom-resources-2026-08-23]. You can deploy and update a custom controller on a running cluster, independently of the cluster's own lifecycle [source: k8s-docs-custom-resources-2026-08-23].

Read that "separation of responsibilities" sentence again and notice what it is. It's Chapter 3's control loop, written by somebody who does not work on Kubernetes.

> **★ Fixed Point**
>
> **A custom resource alone stores and retrieves structured data. A custom resource plus a custom controller is the operator pattern.**

> 🪝 **Snag:** "We installed the CRD but nothing happened." That is the correct behaviour, not a bug. You installed a place to put data. You did not install anything that reads it.
>
> **This is a pattern the book will hit four times, and it's worth naming once: the object exists, but nothing happens without the component.** You will meet it again with Ingress — creating an Ingress resource has no effect without an Ingress controller to fulfill it *[cross-bearing: see Ch 10 §3 — Ingress requires a controller]*. And with `kubectl top`, which needs metrics-server deployed *[cross-bearing: see Ch 13 §2 — the resource metrics pipeline]*. And with the VerticalPodAutoscaler, which is an add-on and not included by default [source: k8s-docs-autoscaling-2026-08-23] *[cross-bearing: see Ch 17 §5 — the autoscaling landscape]*. The same shape holds for NetworkPolicy: creating one without a controller that implements it has no effect [source: k8s-docs-network-policies-2026-08-23].
>
> Four gotchas, one rule. **A Kubernetes API object is a record of intent. Intent with nothing watching it is just a row.**

### The pattern, named

The **operator pattern** combines custom resources and custom controllers [source: k8s-docs-custom-resources-2026-08-23].

Its motivation is worth quoting properly, because it explains the name. The operator pattern aims to capture the key aim of a *human* operator who is managing a service or set of services — people who look after specific applications and have deep knowledge of how the system ought to behave, how to deploy it, and how to react if there are problems. The pattern captures how you can write code to automate a task beyond what Kubernetes itself provides [source: k8s-docs-operator-pattern-2026-08-23]. Operators are clients of the Kubernetes API that act as controllers for a custom resource, and the pattern lets you extend the cluster's behaviour **without modifying the code of Kubernetes itself** [source: k8s-docs-operator-pattern-2026-08-23].

What people actually automate with them, from the docs' own list: deploying an application on demand; taking and restoring backups of that application's state; handling upgrades of application code alongside related changes such as database schemas or extra configuration settings; publishing a Service to applications that don't support Kubernetes APIs to discover them; simulating failure in all or part of your cluster to test its resilience; choosing a leader for a distributed application without an internal member election process [source: k8s-docs-operator-pattern-2026-08-23].

Read that list as a job description and you'll see the argument. Those are the things a knowledgeable human on-call would do at 3 a.m. The operator pattern is the claim that they can be written down.

### The loop closes

Now the detail that makes this section land back on §1.

The most common way to deploy an operator is to add the CustomResourceDefinition and its associated controller to your cluster. **The controller will normally run outside of the control plane, much as you would run any containerized application — for example, as a Deployment** [source: k8s-docs-operator-pattern-2026-08-23].

The thing that extends Kubernetes is itself deployed *by* Kubernetes, using the resource from §1. An operator managing a production database is a Deployment: a Pod template, a replica count, a ReplicaSet, a control loop maintaining it. It is not privileged infrastructure. It is a workload, exactly like yours, that happens to spend its time watching an API and creating objects.

That is the fourth socket Chapter 2 promised. CRI let the ecosystem supply container runtimes; CNI, networking; CSI, storage; and **API extension** lets the ecosystem supply *resource types and the controllers that act on them* — the published extension points list API extensions (CRDs and the aggregation layer) and controllers among them explicitly [source: k8s-docs-extending-kubernetes-2026-08-23]. Collecting all four into one story is Chapter 17's job, and it's a better story told all at once *[cross-bearing: see Ch 17 §2 — the four pluggable interfaces]*.

> 🔭 **Closer Look:** CRDs are not the only route to extending the API. The other is **API server aggregation**, which gives more flexibility at the cost of writing and operating your own API server; the docs recommend considering a custom resource when your API is declarative, you want `kubectl` and dashboard support, and your resources are naturally cluster- or namespace-scoped [source: k8s-docs-custom-resources-2026-08-23]. For nearly everything, and certainly for everything at this level, the answer is a CRD.

Two forward notes. Charts ship CRDs as content — a Helm chart has a dedicated `crds/` directory for exactly this [source: helm-charts-2026-08-23] *[cross-bearing: see Ch 14 §3 — a chart's crds/ directory]*. And a certain widely-used delivery tool is implemented as a Kubernetes controller acting on custom resources, which will look like new technology right up until you notice it isn't *[cross-bearing: see Ch 15 §2 — a controller whose desired state lives in Git]*.

---

## ☆ Taking Your Bearings #3

*Five questions on the rest of the family and the pattern extended. Item 5 requires §1 and §8 together.*

**1.** An application writes to a local disk. Does that mean it needs a StatefulSet? Answer in one sentence, and give the property that actually decides.

**2.** You need six copies of a service running for capacity. A colleague suggests a DaemonSet. What's wrong with that, and what determines a DaemonSet's Pod count?

**3.** Nightly at 02:00, a report has to be generated, and the process must exit when it's done. Name the resource you'd use — and name the resource it creates each time it fires.

**4.** You install a CRD for a resource called `Backup`, then create a `Backup` object. `kubectl get backup` shows it. Nothing else happens. Is the cluster broken?

**5.** 🟡 An operator manages a database. Where does the operator's own controller run, and using which of this chapter's resources?

---

**Answers with Explanations:**

**1. No — the deciding property is whether the Pods are interchangeable.**

Writing to disk tells you nothing about which resource to use. A Deployment's Pod can mount a volume. The question is whether anything depends on *which* Pod it is: a hostname baked into a replication config, a specific shard of data, a member list in a consensus protocol. A StatefulSet's Pods are created from the same spec but are not interchangeable, each holding a persistent identifier maintained across rescheduling [source: k8s-docs-statefulset-2026-08-24].

Why the wrong answers are wrong:

- **"Yes — writing to disk means it's stateful, and stateful means StatefulSet."** This is the misconception in its exact common form. It equates *the application storing data* with *the Pods having identity*, and those are independent.
- **"Yes, because a Deployment's Pods can't have volumes."** Factually wrong. They can.
- **"No, because StatefulSets are only for databases."** Right answer, wrong reason. Plenty of non-databases need stable identity, and plenty of databases run fine as Deployments when their Pods genuinely are interchangeable.

**2. A DaemonSet has no replica count. Its Pod count is determined by how many nodes are eligible.**

The controller creates a Pod for each eligible node [source: k8s-docs-daemonset-2026-08-24]; the corroborating detail is that horizontal pod autoscaling doesn't apply to objects that can't be scaled, and the docs name DaemonSet as the example [source: k8s-docs-hpa-2026-08-24]. If you want six copies, use a Deployment with `replicas: 6`. If you happen to have six nodes today and use a DaemonSet, you'll get six Pods — and then five when a node drains, and nine when the cluster grows, and you'll wonder why your capacity keeps moving.

**3. A CronJob. Each time it fires, it creates a Job.**

`.spec.schedule: "0 2 * * *"`. The CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24], and the Job is what runs to completion and stops [source: k8s-docs-job-2026-08-24]. The second half of the question is the one that separates people who have the model from people who have the vocabulary: a CronJob doesn't run your report, it creates the thing that runs your report.

**4. No. The cluster is behaving exactly as documented.**

On their own, custom resources let you store and retrieve structured data [source: k8s-docs-custom-resources-2026-08-23]. You installed a schema and an API endpoint. You did not install anything that *watches* that endpoint and acts. What's missing is the custom controller — and a custom resource plus a custom controller is the operator pattern [source: k8s-docs-custom-resources-2026-08-23].

**This is an instance of a named pattern: the object exists, but nothing happens without the component.** Learn it here and you get Ingress-without-a-controller, `kubectl top`-without-metrics-server, and VPA-not-shipped-by-default for free — four gotchas, one rule.

Why the tempting wrong answers are wrong:

- **"The CRD is misconfigured."** Nothing about the CRD's correctness would change this. A perfectly valid CRD does nothing on its own; that's the design.
- **"It needs to be in `kube-system`."** Namespace has no bearing. There's no privileged location that makes a resource type start doing things.

**5. Outside the control plane, as an ordinary containerized workload — normally a Deployment.**

The operator's controller normally runs outside of the control plane, much as you would run any containerized application, for example as a Deployment [source: k8s-docs-operator-pattern-2026-08-23]. It is not special infrastructure. It's a Pod template and a replica count, managed by a ReplicaSet, maintained by a control loop — §1's chain, all the way down.

This is the direct precursor to a recognition waiting in Chapter 15. Once you accept that a program which extends Kubernetes is just another Deployment, a delivery tool that watches a Git repository stops looking like a new category of thing.

---

**Checkpoint: You've Now Mastered**

✓ StatefulSet, DaemonSet, Job, and CronJob — each by its one defining property
✓ The decision tree, and why its question order matters
✓ Custom resources, CRDs, custom controllers, and the operator pattern
✓ *The object exists but nothing happens without the component* — a rule you'll retrieve four more times

---

## ☀️ §9 — Nobody Sails One Pod

No new facts here. Just one thing seen properly.

> ☀️ **Zenith**
>
> You have spent this chapter learning six workload resources. You have actually been looking at one diagram the entire time.

Take Chapter 3's control loop — two states, compare, act on the difference — and plug this chapter's controllers into it one at a time. Nothing about the loop changes. The only thing that varies is what "desired" means.

<!-- FIGURE: ch06-zenith-control-loop-instantiated -->
```
                    a number
                        │
    "whatever its       │        a template
     author decided"    │        + an update policy
              ╲         │         ╱
               ╲        ▼        ╱
                ╲  ┌─────────┐  ╱
                 ╲ │ DESIRED │ ╱
                   └────┬────┘
                        │
                   ┌────▼────┐
                   │ compare │
                   └────┬────┘
                        │
                   ┌────▼────┐
                   │ CURRENT │
                   └─────────┘
                 ╱     │      ╲
                ╱      │       ╲
   a Job existing      │        one per matching node
   at each             │
   scheduled time    completion
```

- The **ReplicaSet's** desired state is a number.
- The **Deployment's** is a template plus an update policy.
- The **DaemonSet's** is *one per matching node* — a number, but one the cluster computes rather than one you write.
- The **Job's** is *completion*.
- The **CronJob's** is *a Job existing at each scheduled time*.
- The **operator's** is whatever its author decided a database, or a certificate, or a message queue ought to look like.

Six controllers. One shape. The loop is drawn once because there is only one — that is the argument, and it's the reason this figure has a single loop at its centre instead of six.

Here's the beat that carries forward. This shape is not a Kubernetes implementation detail. It is the thing Kubernetes *is*. Section 8 already showed you that anyone can write a controller — that the extension point is not a special API for privileged vendors but the same loop, in a Deployment, that you could write on a Tuesday. Chapter 15 will show you a controller whose desired state lives outside the cluster entirely, in a Git repository, and that will look like an entirely new technology right up until this section makes it look like the same one. When you get there, come back and check this figure. It will be the same figure.

And the title. Nobody sails one Pod — not because a single Pod is forbidden, but because a single Pod is a statement about *right now*. Every resource in this chapter is a statement about what should keep being true. That is the difference between operating infrastructure and authoring intent, and you crossed it somewhere around §2 without being asked to sign anything.

---

## Exam Alert 🚨

**High-Priority Topics** — in descending order of confidence:

1. **The workload-resource decision** — which resource for which shape of work. This chapter's highest-value block, and the one a recognition exam can ask about in a single sentence. If you memorize one figure, memorize the decision tree.
2. **Deployment versus StatefulSet is about interchangeability**, not about whether the app writes to disk.
3. **DaemonSet is one Pod per matching node**, added automatically as nodes join, with no replica count. The count is a consequence, not a setting.
4. **Job runs to completion once; CronJob creates the same Job on a schedule.**
5. **The ownership chain** Deployment → ReplicaSet → Pod, and which layer holds the count versus the template.
6. **`RollingUpdate` is the default strategy;** `maxSurge` and `maxUnavailable` both default to **25%**; `Recreate` kills all old Pods before creating any new ones.
7. **A revision is created if and only if the Pod template changes** — scaling does not create one.
8. **A CRD alone stores structured data; CRD plus custom controller is the operator pattern.**

---

**Common Traps** — these are documented confusions, not invented ones:

- **"Deployment versus StatefulSet is about whether the app writes to disk."** It isn't. It's about whether the Pods are interchangeable. Defused in §6.
- **"I need several copies, so I'll use a DaemonSet."** A DaemonSet has no count. Defused in §7.
- **"Job and CronJob do the same thing."** A CronJob's output is Jobs. Defused in §7.
- **"Scaling creates a revision."** Only a `.spec.template` change does [source: k8s-docs-deployment-2026-08-23]. This is mechanically checkable and therefore exactly the shape a multiple-choice item is built from.
- **`maxSurge` and `maxUnavailable` transposed.** The names are symmetrical and the defaults are identical, which is what makes them confusable. Surge is above the line; unavailable is below it. And they round in opposite directions — surge up, unavailable down [source: k8s-docs-deployment-spec-fields-2026-08-24].
- **"`Recreate` is a mistake."** It's a supported strategy with a stated cost. Treating it as an error is its own trap.
- **"Installing a CRD makes something happen."** It doesn't. That's the design, and it's one instance of a rule you'll meet four times.

The first three share one root cause worth stating one final time: **choosing a resource by what the application *is*, rather than by how its Pods need to be *managed*.** Get the question order right and three memorizations collapse into one rule.

---

## Practice Questions

*Nineteen questions. Four reach back to Chapters 3, 4, and 5. Five require two sections at once.*

---

**1.** A Deployment named `api` has `replicas: 4`. Which object holds the number 4?

A) The Deployment
B) The ReplicaSet the Deployment manages
C) Each Pod, in its own spec
D) The Pod template

**2.** *[retrieval: ch4]* You run `kubectl get deployment api -o yaml` and see both a `spec` block and a `status` block. Where does the replica count you *asked for* live, and where does the number *actually running* live?

A) Both in `spec`; `status` only reports errors
B) The requested count in `spec`, the running count in `status`
C) The requested count in `status`, the running count in `spec`
D) Both in `status`; `spec` is write-only

**3.** A ReplicaSet has `replicas: 3` and three matching Pods. You add a label to a bare, unowned Pod so that it now matches the ReplicaSet's selector. What happens?

A) Nothing — the ReplicaSet only manages Pods it created
B) The ReplicaSet adopts it and then terminates one Pod, because it is now over count
C) The ReplicaSet's replica count silently increases to 4
D) The API rejects the label change

**4.** *[retrieval: ch5]* A node fails. A Deployment's Pod on that node is replaced. Which statement about the replacement is correct?

A) It is the same Pod, moved to a new node, with the same UID
B) It is a new Pod with a different UID, created from the same template
C) It is the same Pod object with a new UID assigned
D) It retains the original Pod's name so that clients can reconnect

**5.** Two Deployments in the same namespace were written by different teams, and both selectors match the label `tier: web`. What is the most likely observed symptom?

A) The second Deployment fails to create with a duplicate-selector error
B) Both Deployments show replica counts that fluctuate, with no error reported
C) Kubernetes merges them into a single Deployment
D) The older Deployment takes exclusive ownership and the newer one idles

**6.** Which of these is the correct reason a Deployment's `.spec.template.metadata.labels` must match its `.spec.selector`?

A) So that `kubectl get pods --show-labels` renders consistently
B) So that the scheduler can find a node for the Pods
C) Because the controller finds its Pods by querying for the selector, so Pods it creates must satisfy that query
D) Because the API server uses labels to assign owner references

**7.** A Deployment has `replicas: 8` and default strategy settings. During a rolling update, what is the maximum total number of Pods and the minimum available?

A) 10 max, 6 min
B) 10 max, 6 min — with both values rounded up
C) 8 max, 6 min
D) 10 max, 8 min

**8.** A Deployment sets `maxSurge: 0`. What must be true of `maxUnavailable`?

A) It must also be 0
B) It must be greater than 0
C) It is ignored when `maxSurge` is 0
D) It must be expressed as a percentage

**9.** Which change to a Deployment creates a new revision?

A) Increasing `replicas` from 2 to 5
B) Changing `maxSurge` from 25% to 50%
C) Changing the container image in `.spec.template`
D) Changing `revisionHistoryLimit` from 10 to 3

**10.** You scaled a Deployment from 3 to 9 replicas, then later changed the image and immediately ran `kubectl rollout undo`. After the rollback completes, how many replicas are running?

A) 3 — the rollback restores the state from before the scale
B) 9 — the replica count is not part of the Pod template
C) 6 — the rollback averages the two counts
D) Indeterminate, until you run `kubectl scale`

**11.** *[interleaved: §1 + §4]* Midway through a rolling update, `kubectl get rs` shows two ReplicaSets, one with 6 Pods and one with 5. Which is which, and why do two exist?

A) The Deployment created a temporary copy; only one is real
B) The old ReplicaSet is scaling down and the new one is scaling up; both exist because the Deployment layer manages both
C) One belongs to the Deployment and the other belongs to a Service
D) The second was created by the scheduler to hold unschedulable Pods

**12.** *[interleaved: Ch 5 §7 + §4]* From the *probe's* side: why does a readiness probe failing on every new Pod stop a rolling update rather than merely slow it?

A) A failed readiness probe causes the kubelet to kill the container, so no new Pods ever exist
B) A Pod that is not ready does not count as available, so the Deployment cannot scale the old ReplicaSet down further without breaching `maxUnavailable`
C) The Deployment controller stops on the first probe failure and requires manual intervention
D) The scheduler refuses to place additional Pods until the existing ones report ready

**13.** An application acquires an exclusive database lock at startup and cannot tolerate a second instance. Which strategy, and what is the consequence?

A) `RollingUpdate` with `maxSurge: 0` — no downtime, no overlap
B) `Recreate` — a period of zero availability, accepted deliberately
C) `RollingUpdate` with `maxUnavailable: 0` — no downtime, no overlap
D) A StatefulSet, because locks imply state

**14.** *[interleaved: §3 + §6]* A StatefulSet's Pods are also selected by labels. What does the selector *not* tell you about them?

A) Which Pods belong to the StatefulSet
B) That the Pods are not interchangeable with one another
C) How many Pods the StatefulSet maintains
D) Which namespace the Pods are in

**15.** A cluster has 5 nodes. You create a DaemonSet with no `nodeSelector`. Two nodes are then added. How many DaemonSet Pods exist?

A) 5 — the count was fixed at creation
B) 7 — a Pod is scheduled onto each new matching node as it joins
C) 1 — a DaemonSet runs one Pod cluster-wide
D) Whatever `replicas` is set to

**16.** *[retrieval: ch5]* A Job's Pod finishes its work and exits with status 0. Which Pod phase does it reach, and why does that phase matter here specifically?

A) `Running` — Jobs keep their Pods running for inspection
B) `Succeeded` — all containers terminated in success and will not be restarted, which is precisely what "completion" means for a Job
C) `Failed` — exiting is always a failure for a supervised Pod
D) `Unknown` — the Job controller stops reporting once work is done

**17.** A CronJob with schedule `0 4 * * *` has been running for a week. What objects has it created?

A) Seven Pods, directly
B) Seven Jobs, each of which created one or more Pods
C) One Job, restarted seven times
D) Seven CronJob revisions

**18.** *[retrieval: ch3, interleaved with §8]* What does a custom controller have in common with the built-in controllers running inside kube-controller-manager?

A) Nothing — custom controllers use a separate extension API
B) Both are compiled into the control plane binary
C) Both watch a resource whose `spec` is desired state and act to bring current state closer to it
D) Both require cluster-admin privileges by design

**19.** *[interleaved: §8 + §1]* An operator that manages message queues has been installed. Which statement about the operator's own controller process is correct?

A) It runs as a control-plane component alongside kube-scheduler
B) It runs as an ordinary containerized workload in the cluster, normally a Deployment
C) It runs on the client machine, alongside `kubectl`
D) It is embedded inside the CustomResourceDefinition object

---

### Answers & Explanations

**1 — B.** The ReplicaSet holds the count [source: k8s-docs-replicaset-2026-08-24]; the Deployment holds the template and update strategy [source: k8s-docs-deployment-2026-08-23]. **A** is the near-miss: you *set* `replicas` on the Deployment, and the Deployment propagates it to the ReplicaSet it manages — but the object whose job is maintaining that many Pods is the ReplicaSet, and during a rollout there are two of them holding different numbers. **C** is wrong because a Pod has no concept of how many peers it has. **D** confuses the template (what a Pod looks like) with the count (how many).

**2 — B.** For objects that have a spec, you set it when you create the object, describing the desired state; the status describes the current state, supplied and updated by Kubernetes [source: k8s-docs-objects-2026-08-23]. The docs use this exact example: you set the Deployment spec to three replicas, the system starts three instances and updates status to match [source: k8s-docs-objects-2026-08-23]. **C** inverts it. **A** and **D** both misunderstand `status` as a log rather than a description of current state.

**3 — B.** A ReplicaSet acquires any Pod that matches its selector and has no controller owner reference, immediately [source: k8s-docs-replicaset-2026-08-24]. Since the count was already satisfied, the adopted Pod puts it over, and a Pod is terminated. **A** is the intuition this question exists to break — membership is a query, not a record of what the controller created. **C** would mean the controller changed its own desired state, which is not something controllers do. **D** is wrong: labels are freely mutable and the API does not police cross-object overlap.

**4 — B.** A Pod is never rescheduled to a different node; it is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23], and controllers create the replacement from the Pod template [source: k8s-docs-pods-2026-08-24]. **A** describes migration, which Kubernetes does not do at the Pod level. **C** is incoherent — a UID identifies an object over its whole lifetime; a new UID *is* a new object. **D** is wrong and matters: the name changes too, which is exactly why something else has to supply a stable address.

**5 — B.** Two controllers whose selectors overlap will each see a Pod population changing for reasons they didn't cause, and each will act on it. The docs warn about overlapping selectors precisely because of adoption behaviour [source: k8s-docs-replicaset-2026-08-24]. **A** is the answer people hope for; there is no such validation. **C** is not a thing Kubernetes does. **D** implies an ownership arbitration mechanism that doesn't exist — both controllers keep acting, which is what makes this expensive.

**6 — C.** The controller's Pods are whichever Pods match its selector [source: k8s-docs-replicaset-2026-08-24], so Pods it creates must satisfy that query or it can never see them. The API enforces the match [source: k8s-docs-deployment-spec-fields-2026-08-24], but the enforcement exists *because* of C, not the other way round. **D** inverts the relationship — owner references are set by the controller, and are documented as a mechanism distinct from labels and selectors [source: k8s-docs-garbage-collection-2026-08-24]. **A** and **B** are unrelated to selector semantics.

**7 — A.** `maxSurge` = 25% of 8 = 2, so max total 10. `maxUnavailable` = 25% of 8 = 2, so min available 6 [source: k8s-docs-deployment-spec-fields-2026-08-24]. (With 8 replicas both values are whole, so rounding doesn't bite — which is why **B**'s "both rounded up" is wrong as a *rule* even though its numbers happen to match: surge rounds up, unavailable rounds down.) **C** forgets surge headroom entirely. **D** transposes the bounds.

**8 — B.** `maxSurge` cannot be 0 if `maxUnavailable` is 0, and vice versa [source: k8s-docs-deployment-spec-fields-2026-08-24]. With no headroom above the desired count and no slack below it, there is no legal state transition — nothing can start, because nothing may stop. **A** would deadlock the rollout, which is why it's prohibited. **C** and **D** invent behaviour.

**9 — C.** A new revision is created if and only if `.spec.template` changes [source: k8s-docs-deployment-2026-08-23]. The image lives in the template. **A** is the most tempting distractor, and the docs name scaling explicitly as an update that does *not* create a revision. **B** changes `.spec.strategy`, which is a sibling of `.spec.template`, not part of it. **D** changes retention policy, not the template.

**10 — B.** `rollout undo` restores a previous Pod template. The replica count is not in the Pod template — that's the same fact as question 9, seen from the other side. You rolled back the image; you did not roll back the scale. **A** is what most people expect and is the reason this trap is worth a question. **C** is invented. **D** implies the count becomes undefined, which it does not.

**11 — B.** Updating the PodTemplateSpec creates a new ReplicaSet, and the Deployment manages moving Pods from the old to the new at a controlled rate [source: k8s-docs-deployment-2026-08-23]. Two ReplicaSets is the normal mid-rollout state, and it's only expressible because the Deployment layer sits above the ReplicaSet layer — §1's chain doing its actual job. **A** misreads a normal state as a transient artifact. **C** confuses ownership with selection; a Service selects Pods and owns nothing. **D** invents a scheduler behaviour.

**12 — B.** A newly created Pod counts as available only once it is ready (and stays ready for `minReadySeconds`) [source: k8s-docs-deployment-spec-fields-2026-08-24]; readiness failure also removes the Pod's address from matching Service endpoints [source: k8s-docs-pod-lifecycle-2026-08-23]. With no new Pods becoming available, scaling the old ReplicaSet down any further would breach `maxUnavailable`, so the Deployment stops — old version still serving. **A** describes a *liveness* probe, which kills and restarts the container; readiness does not [source: k8s-docs-pod-lifecycle-2026-08-23]. **C** implies a fail-fast abort; the controller keeps retrying. **D** attributes the behaviour to the scheduler rather than the Deployment controller.

**13 — B.** `Recreate` kills all existing Pods before creating new ones [source: k8s-docs-deployment-2026-08-23], guaranteeing the two versions never coexist, at the cost of a window with nothing available. **A** and **C** are the interesting wrong answers: setting one bound to 0 does not prevent overlap, it merely constrains *how much* overlap — and per question 8, one of them being 0 forces the other to be non-zero. **D** confuses "holds a lock" with "Pods have identity"; a single-replica Deployment with `Recreate` is a perfectly ordinary answer.

**14 — B.** The selector tells you membership and nothing else. Two Pods matching the same selector may be freely substitutable (Deployment) or may each hold a distinct identity and its own storage (StatefulSet) — the docs are explicit that StatefulSet Pods are created from the same spec but are not interchangeable [source: k8s-docs-statefulset-2026-08-24]. That distinction lives in the resource kind, not in the labels. **A** is exactly what the selector *does* tell you. **C** is `.spec.replicas`. **D** is `metadata.namespace`.

**15 — B.** Every time you add a node matching the DaemonSet's specification, the control plane schedules a Pod for that DaemonSet onto the new node [source: k8s-docs-workloads-2026-08-23]; with no `nodeSelector`, the controller creates Pods on all nodes [source: k8s-docs-daemonset-2026-08-24]. **A** treats the count as fixed, which is the opposite of the resource's purpose. **C** describes something closer to a single-replica Deployment. **D** is the trap — there is no `replicas` field to set, which is also why HPA does not apply to DaemonSets [source: k8s-docs-hpa-2026-08-24].

**16 — B.** `Succeeded` means all containers terminated in success and will not be restarted [source: k8s-docs-pod-lifecycle-2026-08-23], and a Job continues retrying until a specified number of Pods successfully terminate [source: k8s-docs-job-2026-08-24]. This is where that phase finally earns its place: for a long-running service, `Succeeded` would be a malfunction; for a Job, it's the goal. **C** is wrong and is the mirror-image error — it's `Failed` that means at least one container terminated in failure. **A** contradicts run-to-completion. **D** confuses reporting with phase.

**17 — B.** A CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24], and each Job creates the Pods that do the work [source: k8s-docs-job-2026-08-24]. Seven firings, seven Jobs, at least seven Pods. **A** skips the Job layer — this is the misconception the Job-versus-CronJob distinction is meant to prevent. **C** contradicts run-to-completion. **D** imports revision vocabulary from Deployments, where it doesn't belong. (Note the docs' caveat that scheduling is approximate and two Jobs might occasionally be created, or none [source: k8s-docs-cronjob-2026-08-24] — which is why Jobs should be idempotent.)

**18 — C.** A controller tracks at least one Kubernetes resource type whose objects have a `spec` field representing desired state, and the controller is responsible for making current state come closer to it [source: k8s-docs-controllers-2026-08-23]. A custom controller does exactly this, on a custom resource, providing a true declarative API when paired with one [source: k8s-docs-custom-resources-2026-08-23]. Same shape, different resource type, different author. **B** is false — a custom controller normally runs outside the control plane [source: k8s-docs-operator-pattern-2026-08-23]. **A** denies the whole point of §8. **D** confuses privilege with mechanism.

**19 — B.** The operator's controller normally runs outside the control plane, much as you would run any containerized application — for example, as a Deployment [source: k8s-docs-operator-pattern-2026-08-23]. **A** is the intuitive-but-wrong answer: extending Kubernetes doesn't require *being* Kubernetes. **C** describes a client-side tool, but operators are long-running API clients that must keep watching. **D** misunderstands a CRD as executable rather than as a schema.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **Workload resource** | You don't manage Pods; you declare intent and a controller manages Pods for you |
| **Ownership chain** | Deployment → ReplicaSet → Pod. Deployment holds template + strategy; ReplicaSet holds the count |
| **ReplicaSet** | Maintains a stable set of replica Pods. The control loop, with `.spec.replicas` as desired state |
| **Scaling vs self-healing** | The same operation. The loop can't tell "you asked for more" from "one died" |
| **Selector** | Membership is a query, not a list. Template labels must satisfy the selector |
| **Owner reference** | What makes cascading deletion work — and what adoption sets on Pods a controller acquires |
| **Overlapping selectors** | Two controllers fighting over one Pod population. No error is reported |
| **`RollingUpdate`** | The default. New ReplicaSet up, old one down, at a controlled rate |
| **`maxSurge` / `maxUnavailable`** | Both default to 25%. Surge is above the line (rounds up); unavailable is below (rounds down) |
| **`Recreate`** | All old Pods killed first. Downtime, deliberately chosen, for apps that can't run two versions |
| **What makes a rollout safe** | Readiness. A Pod that never reports ready never counts as available, so it never displaces the old one |
| **Revision** | Created if and only if `.spec.template` changes. Scaling does not create one |
| **Rollback** | Sets the Pod template to a previous value and runs the same rolling update backwards |
| **StatefulSet** | For Pods that are *not interchangeable*. Stable ordinal identity, stable network name, own storage |
| **The disk trap** | "Writes to disk" does not mean StatefulSet. Interchangeability decides |
| **DaemonSet** | One Pod per matching node, automatically as nodes join. No replica count |
| **Job** | Runs to completion, once. Reaches `Succeeded` or `Failed` |
| **CronJob** | Creates the same Job repeatedly on a cron schedule. Its output is Jobs |
| **Custom resource** | A new API endpoint. On its own, it only stores structured data |
| **Operator pattern** | Custom resource + custom controller. The controller normally runs as a Deployment |
| **The recurring rule** | The object exists, but nothing happens without the component |

---

## The Voyage Ahead

You can now write down what should be true and hand the responsibility to a loop. There is one thing that loop cannot do for you.

It creates a Pod. It does not decide *where the Pod goes*. Every replacement in this chapter, every surge Pod during a rolling update, every DaemonSet Pod on a newly joined node — each one arrives in the world unplaced, and something else has to find it a machine with room. Usually that works so smoothly you never think about it. Sometimes it doesn't, and a Pod sits in `Pending` while the count it was supposed to satisfy stays unsatisfied, and the loop that created it goes on cheerfully wanting one more.

Chapter 7 is about the component that makes that decision, the two-step process it uses, and the vocabulary you have for influencing it — how a Pod expresses what it needs from a machine, and how a machine expresses what it will accept. You've already met the mechanism in disguise: the DaemonSet's tolerations in §7 were a node saying "not for general traffic" and a controller saying "this one's an exception."

> *"You may declare what should exist. Where it exists is a separate question, and the sea does not always have room where you wanted it."*

---

🏆 **Safe Harbor**

Chapter 6 complete. You came in able to read a Pod and left able to author a fleet — six workload resources, one control loop, and the beginning of the recognition that the loop is the whole system rather than a feature of it.

**Voyage Progress:** 🗺️ → 🌊 → 🌅
*Part II, Chapter 6 of 18. The trunk of the book is behind you.*
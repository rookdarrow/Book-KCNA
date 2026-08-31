# Chapter 16: Your Application, Their Cluster
## *"Four questions that separate your bug from theirs"*

**Domain Weight: 16% (Cloud Native Application Delivery) [source: cncf-kcna-curriculum-pdf-2026-08-23] | Competency: Debugging | Authored allocation for this chapter: ~4%**
**Complexity: Mixed | Novelty: Moderate | Prerequisites: Heavy**

<!-- AUTHOR-REVIEW: the "~4%" figure is this book's own allocation across the two D3 chapters, not a CNCF-published number. CNCF publishes four domain weights (44/28/16/12) and no sub-competency weights. The metadata line above labels it as authored; confirm that phrasing survives revision. -->

---

## Attention Budget

**Total time: ~75 minutes | Recommended: Single session, or split after §5**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 Handed Back | 6 min | Low | Anytime |
| §2 When It Never Got Started | 9 min | Medium | Mid-session |
| §3 Getting Inside, and Adding What Isn't There | 16 min | High | Peak attention |
| ☆ Taking Your Bearings (1) | 6 min | Medium | After a brief break |
| §4 Is Anything Even Selected | 12 min | High | Peak attention |
| §5 Bypassing the Service on Purpose | 6 min | Low | Anytime |
| ☆ Taking Your Bearings (2) | 5 min | Medium | After a brief break |
| §6 When Each Replica Is Its Own | 7 min | Medium | Mid-session |
| §7 Before You Ship It | 5 min | Low | Anytime |
| ☆ Taking Your Bearings (3) | 5 min | Medium | After a brief break |
| §8 Mine, or the Platform's | 3 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*If you only have 15 minutes: read §1 and §4, then take the second Taking Your Bearings checkpoint.*

---

> *"The first step in troubleshooting is triage. What is the problem?"*
> — Kubernetes documentation, *Debug Pods*

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Every one of them is answerable from Chapters 1–15 or from general professional knowledge — none of them requires anything this chapter is about to teach you. Your score determines how to approach the content. No shame in any score; different scores just call for different reading strategies.

1. A Pod is `Running`. It reports `1/1 Ready`. Its restart count is zero, its node is healthy, and no other workload in the namespace is affected. The response it returns is still wrong. Whose problem is this — the platform's or the application's?

2. A Pod declares three init containers. The second one exits non-zero. What happens to the third init container, and what happens to the app containers?

3. A Pod is `Running` but reports `0/1 READY`. What has happened to its membership in the endpoint list behind its Service?

4. Of `port` and `targetPort` on a Service, which one names the port the container is actually listening on?

5. Write out the in-cluster DNS name a Pod would use to reach a Service named `api` in the namespace `payments`.

6. A StatefulSet Pod is rescheduled onto a different node. Name one thing about it that does not change.

7. You delete the Pod `web-2` from a three-replica StatefulSet. What happens to its PersistentVolumeClaim?

8. An image is built from a minimal base — no package manager, no `/bin/sh`, nothing but the application binary and its libraries. What happens when you run `kubectl exec <pod> -- sh` against it?

<details>
<summary>Answers + reading strategy</summary>

1. **The application's.** The mechanical test from Chapter 13 is: if the Pod is running and ready, and the fault is confined to one workload, the platform has done its job and the problem is yours. *[cross-bearing: see Ch 13 §1 — whose problem is this, and what to read first]*

2. **The third init container never runs, and neither do the app containers.** Init containers run in order and each must exit successfully before the next starts. The Pod stays in `Pending` with the `Initialized` condition false. *[cross-bearing: see Ch 5 §3 — everything that must happen first]*

3. **It has been removed from the endpoint list, or was never added.** Readiness gates endpoint membership: a Pod that is not ready is not a valid target for Service traffic. *[cross-bearing: see Ch 9 §4 — the list behind the name]*

4. **`targetPort`.** `port` is the port the Service itself is reachable on; `targetPort` is the port on the Pod that traffic is delivered to. *[cross-bearing: see Ch 9 §3 — four ways to be reachable]*

5. **`api.payments.svc.cluster.local`** — the general form is `<service>.<namespace>.svc.<cluster-domain>`. A Pod in the `payments` namespace could also just say `api`. *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*

6. **Any of: its hostname, its ordinal, its DNS name, or its PersistentVolumeClaim.** All four are part of the sticky identity a StatefulSet maintains across rescheduling. *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*

7. **Nothing. The PVC survives.** The default retention policy is `Retain` for both the scale-down and the delete case, and a Pod replaced after a node failure keeps its existing claim entirely. *[cross-bearing: see Ch 11 §6 — Pods that are not interchangeable, revisited]*

8. **It fails.** There is no shell in the image to execute. An image contains exactly what was put into it and nothing else — there is no ambient operating system underneath waiting to supply the missing pieces. *[cross-bearing: see Ch 2 §2 — what's inside an image]*

**If you got 6+ right:** Skim, but read §3 and §6 properly. Those two carry material with no analog anywhere earlier in the book, and skimming them will cost you.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Before you start this chapter, go back and re-read **Chapter 13 §1** — not the whole chapter, that one section. This chapter's opening move is receiving a handoff that Chapter 13 §1 made. Without it, everything here reads as a list of commands instead of a method.

</details>

---

## Why This Chapter Matters

Three chapters ago, the platform finished its work and handed you back your own problem.

That is where this chapter starts. Not with an introduction — with the far side of a handoff you were given in Chapter 13 and have been carrying ever since. The Pod is `Running`. It is `1/1 Ready`. The restart count is zero, the node is healthy, the events are quiet, and the thing your users are complaining about is still happening.

Chapter 13 taught you to stop reaching for the logs and read the phase first. The phase, here, has nothing left to say. Every diagnostic that has served you for two hundred pages returns a clean answer, and the system is broken anyway.

So what do you actually look at?

The answer is a different set of four questions and a different set of tools, and there is a reason those tools were withheld until now: every one of them requires a running container. `exec` needs a process to enter. An ephemeral container needs a Pod to attach to. `port-forward` needs something listening on the other end. All of them assume the condition Chapter 13 spent its whole length helping you establish.

There is also a shift in who you are while you use them. Chapter 13's reader stood outside somebody else's platform and interrogated it, asking whether the cluster had done its job. This chapter's reader is the person who shipped the thing — working inside a cluster they do not own, with permissions they did not grant themselves, on an image that may not contain a shell. That is the actual posture of an application engineer on Kubernetes, and it is what the chapter title names.

> **Dead Reckoning:** When a Pod is `Running` and `Ready` and the application is still wrong, the platform's own signals will keep reporting "fine," because from the platform's point of view everything is. The diagnostic surface you need is inside the container, in the Service that routes to it, and in the configuration the process actually read — none of which the platform inspects on your behalf. The tools for reaching those places are `kubectl exec`, `kubectl debug`, `kubectl port-forward`, and `kubectl get endpointslices`. Each answers a different question. Knowing which question you are asking is most of the work.

The stakes are specific. Cloud Native Application Delivery is 16% of the KCNA exam [source: cncf-kcna-curriculum-pdf-2026-08-23], and Debugging is one of its two competencies. That domain doubled from the previous blueprint, which means prep material written against the old five-domain shape under-serves this material more than any other part of the exam. What gets tested here is not flag syntax. It is which verb answers which question — and that is something a glossary cannot tell you, because the verbs are only distinguishable by the question each one is for.

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Take** the handoff from platform scope and state, mechanically, which side of the boundary a failure is on
- **Ask** the four questions that localize an application fault — is it running, is it healthy, is it reachable, is it configured — in the order that eliminates the most ground first
- **Read** a failing init container from the application side, and recognize the ordering and re-run assumptions that break one
- **Get inside** a running container with `exec`, and get inside one with no shell at all using an ephemeral container and `kubectl debug`
- **Diagnose** a Service that exists, selects nothing, and is therefore working exactly as written
- **Prove** where a break is by deliberately bypassing the Service path with `port-forward`
- **Ask** all four questions of a single StatefulSet replica, when the replicas are not interchangeable

*You'll also stop asking "is Kubernetes broken?" as your first question, which is the habit that costs application engineers the most time on somebody else's cluster.*

---

## ⚪ §1 — Handed Back

Here is the sentence Chapter 13 ended on, restated from this side: **the Pod is fine and the application isn't.**

That is not a failure of the platform's diagnostics. It is what a successful platform diagnosis looks like. The kubelet started your container. The scheduler placed it. The probes passed. Nothing crashed. Every question the cluster knows how to ask has been asked and answered in your favor, and the fault is somewhere the cluster does not look.

The Kubernetes documentation draws the same line at the top of its own application-debugging guide: *"This guide is to help users debug applications that are deployed into Kubernetes and not behaving correctly. This is not a guide for people who want to debug their cluster."* [source: k8s-docs-debug-pods-2026-08-31] Two audiences, two sets of tools, one boundary between them.

You already have the mechanical test for which side you are on — scope first, then phase, then conditions, then events, then logs, and a fault that is *not* confined to a single workload is still the platform's *[cross-bearing: see Ch 13 §1 — whose problem is this, and what to read first]*. What is new here is the direction of travel, and one honest addition to the test.

The addition is this: on somebody else's cluster, you will frequently be *unable* to check the platform side yourself. You may not have permission to read node conditions, or to list Pods in `kube-system`, or to see the events on a node you don't own. The boundary is therefore not only a statement about where the fault is. It is also a statement about what you are allowed to see — and the practical consequence is that you should be able to make your case for "this is platform-side" from evidence you *can* gather, because the person who can check the other half is going to ask you for it.

None of which makes the platform team an adversary. "Their cluster" in this chapter's title is a statement of scope, not of blame. They own the machinery; you own the workload; the boundary is where those two responsibilities meet, and the entire value of being able to place a fault on the correct side is that neither of you spends an afternoon on the other's half.

### The four questions

Everything after this section is one of four questions, asked in an order chosen to eliminate the most ground first:

**Is it running?** — Not "does the Deployment exist," but did this container's process actually get to the point of executing your code. A Pod that never cleared its init sequence has never run a line of your application.

**Is it healthy — and is it configured the way you think?** — The process is up. Is it doing what you told it, with the values you believe you gave it? These two are one question because the answer to both lives in the same place: inside the running container.

**Is it reachable?** — Something is listening. Can the traffic get to it, through the Service that is supposed to route it?

**Is it configured?** — Which appears twice, deliberately. Read on.

<!-- FIGURE: ch16-fig01-application-scope-triage -->
```
        FROM CH 13 — platform scope discharged
                        │
                        ▼
        ┌───────────────────────────────────┐
        │   APPLICATION SCOPE  (this book,  │
        │   this chapter, your problem)     │
        └───────────────┬───────────────────┘
                        │
     ┌──────────┬───────┴───────┬─────────────┐
     ▼          ▼               ▼             ▼
  RUNNING?   HEALTHY?       REACHABLE?    PER-REPLICA?
   (§2)     CONFIGURED?     (§4 → §5)        (§6)
              (§3)
```

The mapping to sections is direct, with one wrinkle:

| Question | Answered in |
|---|---|
| Is it running? | §2 |
| Is it healthy — and is it configured the way you think? | §3 |
| Is it reachable? | §4, then §5 |
| *(all four, for workloads whose replicas are not interchangeable)* | §6 |

**Note the doubling.** "Is it configured" gets answered in two places, because a configuration fault surfaces at two different times. A missing ConfigMap key can stop a Pod before it ever starts, and that shows up at init (§2). A *present* key with the wrong value gets read cleanly by a running process that then does the wrong thing, and that shows up only when you go in and look (§3). Same class of bug, two entirely different signatures, two different sections. Four questions, eight sections — the arithmetic works out because the questions overlap, not because anything is missing.

> ⚓ **Worth Securing:** Ask the questions in order. Each one, answered, deletes a large region of the search space. The temptation is to jump to whichever tool you learned most recently — usually `exec` — and start poking. That is how a fifteen-minute diagnosis becomes an afternoon: you can spend a very long time inside a container that was never going to work because its init container failed forty minutes ago.

---

## 🔵 §2 — When It Never Got Started

A Pod that is stuck before its first application container has run is the easiest fault in this chapter to misdiagnose, because the symptom — "nothing is happening" — looks identical to a dozen other things.

You have the model already. Init containers run before app containers, in the order written, one at a time, each to completion *[cross-bearing: see Ch 5 §3 — everything that must happen first]*. What Chapter 5 deliberately did not give you was the method for reading one when it goes wrong. And Chapter 13 owned the platform-side half of this failure — an init container whose *image* cannot be pulled is a platform-scope problem with a platform-scope signature *[cross-bearing: see Ch 13 §2 — pods that never start]*. What is left, and what this section owns, is the case where the init container runs perfectly well and does the wrong thing.

### Reading the state

Start with the Pod's status, which tells you which init container you are looking at:

```
kubectl get pod <pod-name>
```

The `STATUS` column carries a specific vocabulary for this case [source: k8s-docs-debug-init-containers-2026-08-31]. A Pod mid-sequence reports `Init:N/M` — N init containers complete out of M total. A Pod whose init container is failing reports `Init:Error` or `Init:CrashLoopBackOff`. That is already a lot of information: `Init:1/3` tells you the first one succeeded and you should be looking at the second.

The Pod's phase is `Pending` throughout, with the `Initialized` condition false *[cross-bearing: see Ch 5 §5 — Pod phase and container state]*. This is why "read the phase first" alone does not finish the job here — every Pod in this state has the same phase, and the discriminating detail is in the status string and the container list.

### Reading the logs

Here is where people lose time:

```
kubectl logs <pod-name>
```

This returns nothing useful. The plain form targets the Pod's app container, and the app container has not started — there is nothing to print. What you need is the `-c` flag naming the specific init container [source: k8s-docs-debug-init-containers-2026-08-31]:

```
kubectl logs <pod-name> -c <init-container-name>
```

The `-c` flag is not new to you *[cross-bearing: see Ch 13 §3 — reading logs from a multi-container Pod]*; what is new is that here it is not optional. A multi-container Pod at least gives you *a* log stream when you omit `-c`. An initializing Pod gives you an error or an empty result, and the reader who reads that as "the init container isn't logging anything" has just concluded something false about a container that is loudly complaining into a stream nobody asked for.

> 🪝 **Snag:** `kubectl logs <pod>` on a Pod stuck in init tells you nothing, and the nothing is misleading. Always name the init container with `-c`. If you don't know its name, `kubectl describe pod <pod>` lists the init containers in order, along with each one's state and exit code.

### The three ways an init container is wrong

**Ordering.** Init containers are your only ordering primitive inside a Pod, and the most common failure is an init container that waits for something which cannot arrive until this Pod is up. A classic shape: an init container that blocks until a Service has endpoints — for a Service whose only backend is *this* Pod. The init container waits forever, the app container never starts, the Service never gets an endpoint, and the deadlock is perfectly stable. Nothing in the platform will tell you this; the platform is doing exactly what you asked.

The tell is a `Init:0/1` Pod that has been sitting there for a long time with no error, no restarts, and a log stream that says something calm and patient like "waiting for dependency."

**Non-idempotency.** An init container will be re-run. Not might — will. If the Pod restarts, every init container executes again from the beginning [source: k8s-docs-init-containers-2026-08-24]. An init container that assumes a clean slate — that creates a directory without checking, that runs a migration without a guard, that appends to a file that should have one line — works perfectly the first time and fails on every restart after. This produces one of the more maddening signatures in Kubernetes: a workload that comes up fine on a fresh deploy and refuses to come back after any disruption at all.

> ⚓ **Worth Securing:** Write init containers as though they will run five times, because eventually they will. Idempotency is not a nicety here; it is a correctness requirement imposed by the restart semantics. If your init container's job is "create X," its actual job is "ensure X exists."

**Configuration errors visible at init.** Init containers are frequently where a config problem first becomes visible, because the init container is usually the first thing that reads the mounted configuration. A ConfigMap key that does not exist, a Secret whose value is base64-decoded into something the wrong shape, a mount path that collides with something in the image — these surface as an init container exiting non-zero with a message that names the actual problem *[cross-bearing: see Ch 4 §4 — ConfigMaps and Secrets]*.

That last point is worth dwelling on, because it is the good news in this section. A config error caught at init gives you a clean, specific, non-mysterious failure with the reason printed in a log. The *same* config error that gets past init — because the value is present but wrong — becomes §3's problem, and §3's problem is much harder.

<!-- FIGURE: ch16-fig05-init-sequence-debug-points -->
```
  init-1 ──────▶ init-2 ──────▶ init-3 ──────▶ app containers
    │              │              │                  │
    ▼              ▼              ▼                  ▼
 STATUS:        STATUS:        STATUS:            STATUS:
 Init:0/3       Init:1/3       Init:2/3           Running

 READ WITH:  kubectl logs <pod> -c <init-name>
 ALSO READ:  kubectl describe pod <pod>   (exit codes, order, state)

 STUCK, NO ERROR ......... ordering deadlock — what is it waiting for?
 FAILS ONLY ON RESTART ... non-idempotent — it assumed a clean slate
 EXITS NON-ZERO, LOUDLY .. config error — read the message, it's telling you
```

There is one more diagnostic surface here worth knowing. A container can write to a **termination message** file — by default `/dev/termination-log` — and Kubernetes surfaces the contents in the Pod's status [source: k8s-docs-determine-reason-pod-failure-2026-08-31]. The docs describe the purpose plainly: *"Termination messages provide a way for containers to write information about fatal events to a location where it can be easily retrieved and surfaced by tools like dashboards and monitoring software."* [source: k8s-docs-determine-reason-pod-failure-2026-08-31] For an init container that fails in a way that logs don't capture well, writing a one-line reason to the termination log makes the failure legible from `kubectl describe` alone.

> 🔭 **Closer Look:** The same source notes that in most cases, information you put in a termination message should also be written to the general Kubernetes logs [source: k8s-docs-determine-reason-pod-failure-2026-08-31]. The termination message is a summary surfaced in status, not a replacement for logging.

---

## 🔵 §3 — Getting Inside, and Adding What Isn't There

The Pod is running. Your code is executing. And you have run out of things you can learn from the outside.

This section is about getting inside a container — and about what to do when there is no inside to get into. It is the densest material in the chapter, and it has no analog anywhere earlier in the book. Chapter 8's kubectl verb table pointed here explicitly for `exec` *[cross-bearing: see Ch 8 §1 — the grammar of a command]*, and Chapter 12 pointed here for the debug-container case *[cross-bearing: see Ch 12 §6 — three levels, three modes]*. This is where both debts come due. If you are following one of those pointers and it said "getting inside a container" while another said "getting inside, and adding what isn't there" — same section, both phrasings, you are in the right place.

### `kubectl exec`

The direct move is to run a command inside a container that is already running:

```
kubectl exec -it <pod-name> -- /bin/bash
```

The docs describe it exactly this way — *"This page shows how to use `kubectl exec` to get a shell to a running container"* [source: k8s-docs-get-shell-running-container-2026-08-31]. For a multi-container Pod, name the container with `-c`, the same flag you have been using with `logs`:

```
kubectl exec -it <pod-name> -c <container-name> -- /bin/sh
```

The double dash matters. Everything after `--` is the command run inside the container; everything before it belongs to kubectl. Omit it and kubectl will try to interpret your command's flags as its own.

What you are actually doing in there, most of the time, is answering the second half of the second question: **is it configured the way you think?** Not "does the ConfigMap say what I meant" — you can read the ConfigMap from outside. The question is what the *process* got. Environment variables can be shadowed, mounted files can be masked by another mount, a default in the application code can quietly win over an empty string, and a value can be correct in the manifest and absent in the container because a mount path was one character off.

```
kubectl exec <pod-name> -- env | grep DATABASE
kubectl exec <pod-name> -- cat /etc/config/app.yaml
kubectl exec <pod-name> -- ls -la /etc/config/
```

That third one catches more bugs than the other two combined. A directory that is empty, or that contains a file named something you did not expect, is a mount that did not land the way the manifest reads.

> 🪝 **Snag:** The gap between "what the manifest says" and "what the process read" is where a large share of application-scope bugs live, and it is invisible from `kubectl get -o yaml`. The manifest is a statement of intent; the container's filesystem and environment are the outcome. When they disagree, `exec` is the only place you find out.

### The image with nothing in it

Now the problem.

```
kubectl exec -it <pod-name> -- /bin/sh
```
```
OCI runtime exec failed: exec failed: unable to start container process:
exec: "/bin/sh": stat /bin/sh: no such file or directory
```

There is no shell. There is no `cat`, no `ls`, no `env` binary, no package manager to install one with. The image contains your application binary, the libraries it links against, and nothing else. This is a **distroless** image, and it is not a mistake — it is a deliberate hardening choice. The Kubernetes documentation is direct about the trade: *"distroless images enable you to deploy minimal container images that reduce attack surface and exposure to bugs and vulnerabilities. Since distroless images do not include a shell or any debugging utilities, it's difficult to troubleshoot distroless images using `kubectl exec` alone."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

<!-- AUTHOR-REVIEW: "distroless" is used throughout this section and has no owner in the term ledger and no ambient-tier row. It reaches graded text in this chapter's Practice Questions. Queue a glossary entry and an acronym-register row at the glossary build. -->

Your first instinct is probably right and also unavailable: add a second container to the Pod with the tools in it. You cannot.

> **★ Fixed Point**
>
> **You cannot add a container to a Pod once the Pod has been created.** The Pod's container list is fixed at creation. That single fact is the entire reason ephemeral containers exist as a separate mechanism, and it is the fact the exam reaches for.

The documentation states the constraint and the consequence together: *"Since Pods are intended to be disposable and replaceable, you cannot add a container to a Pod once it has been created. Instead, you usually delete and replace Pods in a controlled fashion using deployments."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31] And then the exception: *"Sometimes it's necessary to inspect the state of an existing Pod, however, for example to troubleshoot a hard-to-reproduce bug. In these cases you can run an ephemeral container in an existing Pod to inspect its state and run arbitrary commands."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

### Ephemeral containers

An ephemeral container is a container that runs temporarily inside an existing Pod, added through a dedicated API path rather than by editing the Pod's spec. The documentation is explicit that it is not editable through the normal route: *"Ephemeral containers are created using a special `ephemeralcontainers` handler in the API rather than by adding them directly to `pod.spec`, so it's not possible to add an ephemeral container using `kubectl edit`."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

They are deliberately constrained, and the constraints are exam material [source: k8s-docs-ephemeral-containers-concept-2026-08-31]:

- **No ports, no probes.** *"Ephemeral containers may not have ports, so fields such as `ports`, `livenessProbe`, `readinessProbe` are disallowed."*
- **No resource requests or limits.** *"Pod resource allocations are immutable, so setting `resources` is disallowed."*
- **No removal, no change.** *"Like regular containers, you may not change or remove an ephemeral container after you have added it to a Pod."*
- **No restarts.** *"Ephemeral containers differ from other containers in that they lack guarantees for resources or execution, and they will never be automatically restarted, so they are not appropriate for building applications."*
- **Not on static Pods.** *"Note: Ephemeral containers are not supported by static pods."* *[cross-bearing: see Ch 13 §5 — when the node is the problem]*

Read those five together and the design intent is obvious: this is an instrument, not a workload. It gets no guarantees because it is not supposed to be part of your application, and it cannot be removed because a Pod's container list — even the ephemeral part of it — is append-only.

> 🪢 **Mnemonic:** An ephemeral container is a **tool you hand through the window**, not a room you add to the house. No resources reserved for it, no probes watching it, no restart if it dies, and once it's through the window you can't take it back.

### `kubectl debug`

`kubectl debug` is the verb that puts one there. In its simplest form it attaches an ephemeral container to a running Pod, using an image you choose — one that has the tools the target image lacks:

```
kubectl debug -it <pod-name> --image=busybox:1.28 --target=<container-name>
```

The `--target` flag matters for a distroless container specifically: it puts the debug container in the target container's process namespace, so you can see and interact with the target's processes. The docs note that *"When using ephemeral containers, it's helpful to enable process namespace sharing so you can view processes in other containers."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

That is one of three shapes. The other two answer different questions.

### `--copy-to`: a copy, not a repair

The second shape makes a **copy** of the Pod and modifies the copy:

```
kubectl debug <pod-name> -it --image=ubuntu --share-processes --copy-to=<new-pod-name>
```

The documentation's framing: *"Sometimes Pod configuration options make it difficult to troubleshoot in certain situations. For example, you can't run `kubectl exec` to troubleshoot your container if your container image does not include a shell or if your application crashes on startup. In these situations you can use `kubectl debug` to create a copy of the Pod with configuration values changed to aid debugging."* [source: k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31]

> **★ Fixed Point**
>
> **`--copy-to` makes a copy. The original Pod is not touched — and that is the feature, not a limitation.** You get a new Pod with whatever changes you need (a different command, an extra container, a shell as the entrypoint) while the broken Pod keeps running exactly as it was, still serving traffic, still available for the platform team to look at, still in the state that produced the bug.

This is the part most readers get backwards on first encounter. The mental model people arrive with is that a debugging tool operates on the thing being debugged — you attach a debugger to the process, you modify the running system. `--copy-to` does the opposite, and on a cluster you do not own, running a workload you did not deploy, that inversion is the whole point. You can experiment freely on a copy. You cannot experiment freely on production.

The copy is also the answer to a case `exec` can never handle: a container that crashes on startup. There is no running process to enter, and by the time you type the command it is gone again. Copy the Pod, change the entrypoint to a shell, and now you have a container built from the same image, with the same config, that sits still while you look at it.

> ⚓ **Worth Securing:** A copy is a real Pod. It consumes resources, it may be selected by a Service if it carries the right labels, and it will sit there until you delete it. Clean up after yourself — `kubectl delete pod <copy-name>` — and be aware that if the copy inherits the original's labels, it may start receiving live traffic. Some copy modes strip labels for exactly this reason; check what yours did before assuming.

### `kubectl debug node/`: stepping back over the line

The third shape targets a node rather than a Pod:

```
kubectl debug node/<node-name> -it --image=ubuntu
```

This creates a Pod on the target node with the node's filesystem mounted and access to the host namespaces. It is genuinely useful and it is, unmistakably, the moment you step back across the boundary §1 drew. A node is not application scope. If you find yourself reaching for `debug node/`, you have either concluded that the fault is platform-side — in which case the right move is usually to hand it to whoever owns the platform, with the evidence you gathered — or you *are* the person who owns the platform, wearing a different hat.

Which makes it an argument for the boundary rather than an exception to it: the tool exists, it is on the same documentation page as the others, and the reason it feels out of place here is that it *is* out of place here. Notice the feeling. It is the boundary doing its job. Node-level diagnosis, including the node-local tooling below the Kubernetes API, belongs to the platform-scope chapter *[cross-bearing: see Ch 13 §5 — when the node is the problem]*.

> ⚠ **Navigational Hazards**
>
> **A debug container is a container, and admission can refuse it.**
>
> You have RBAC permission to run `kubectl debug`. You run it. It fails — not with a permissions error on the verb, but with a rejection from admission control. This is not a bug and it is not RBAC.
>
> The ephemeral container you are injecting is subject to the same Pod Security Admission enforcement as any other container in that namespace. In a namespace enforcing the `restricted` standard, a debug image that wants to run as root, or wants elevated capabilities, or wants host namespace access, is going to be refused at the admission gate — because a container that would not be allowed to exist in that namespace does not become allowed by being ephemeral *[cross-bearing: see Ch 12 §6 — three levels, three modes]*.
>
> This is the single most likely way `kubectl debug` fails on a cluster you do not own, and the error is easy to misread as "I don't have permission to debug." You do. The *container you asked for* doesn't meet the namespace's standard. Try a debug image that runs as non-root, or ask the namespace's owner what the enforcement level is.

### Debug profiles

`kubectl debug` also accepts a `--profile` flag that sets a bundle of security-related properties on the debug container — whether it runs privileged, whether it gets host namespaces, and so on. The available profile names include `general`, `baseline`, `restricted`, `netadmin`, and `sysadmin`, with `general` as the default in the generated CLI reference [source: k8s-docs-kubectl-debug-reference-2026-08-31].

<!-- AUTHOR-REVIEW: the two cached snapshots disagree. k8s-docs-kubectl-debug-reference-2026-08-31 (generated CLI reference) lists five profiles with `general` as default; k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31 (the task page) lists six including `legacy` and names `legacy` as default. The generated reference is produced from the kubectl binary and is treated as authoritative here, but the conflict is real and version-dependent. The list above is deliberately introduced with "include" rather than presented as complete. Revision stage: confirm against a single dated snapshot, or soften further to "name two and describe the shape." -->

The shape to remember, rather than the list: a profile is a preset for how much privilege the debug container asks for, and asking for more than the namespace allows is what triggers the admission refusal in the Hazard above. The `restricted` profile exists precisely so that a debug container can be injected into a namespace enforcing the restricted standard.

<!-- FIGURE: ch16-fig02-ephemeral-container-debug -->
```
  (A) EPHEMERAL CONTAINER — into the running Pod
      ┌─────────── Pod (unchanged) ───────────┐
      │  [app: distroless]  + [debug: busybox]│  ← added, cannot be removed
      └───────────────────────────────────────┘
      ASKS: "what does the running process see right now?"

  (B) --copy-to — a NEW Pod, original untouched
      ┌─── Pod (running, untouched) ───┐   ┌─── Pod-copy ────────┐
      │  [app: crashing on startup]    │   │  [app: entrypoint   │
      │                                │   │        replaced]    │
      └────────────────────────────────┘   └─────────────────────┘
      ASKS: "what would happen if I changed something?"

  (C) node/ — the host, not the workload
      ┌─── Node ───────────────────────────────┐
      │  [debug Pod, host filesystem mounted]  │  ← PLATFORM SCOPE
      └────────────────────────────────────────┘
      ASKS: "is the machine itself the problem?"   (see Ch 13 §5)
```

Three shapes, three questions. They are not interchangeable, and choosing the wrong one is how you spend twenty minutes in a copy of a Pod investigating a problem that only exists in the original.

---

## ☆ Taking Your Bearings: Taking the Handoff, and Getting Inside

Six questions on §1 through §3. One of them tests material from an earlier chapter.

**1.** A Pod is `Running`, reports `1/1 Ready`, has zero restarts, and its node shows no adverse conditions. Two other workloads in the same namespace are behaving normally. The application returns HTTP 500 on one endpoint. What does the scope test tell you?

- A) Platform scope — a 500 indicates a runtime failure the kubelet should have caught
- B) Application scope — the fault is confined to one workload and every platform signal is clean
- C) Indeterminate — you need node-level access before you can decide
- D) Platform scope — readiness probes passing means the platform is asserting the app is correct

**2.** A Pod shows `STATUS: Init:1/3`. Which command gives you the most useful next piece of information?

- A) `kubectl logs <pod>`
- B) `kubectl logs <pod> -c <second-init-container-name>`
- C) `kubectl exec -it <pod> -- sh`
- D) `kubectl port-forward <pod> 8080:8080`

**3.** Why do ephemeral containers exist as a separate API mechanism rather than as an ordinary edit to a Pod's spec?

- A) Because ephemeral containers need a different container runtime
- B) Because a Pod's container list cannot be added to once the Pod exists
- C) Because ephemeral containers are scheduled to a different node
- D) Because RBAC cannot grant `update` on Pods

**4.** You run `kubectl debug <pod> --copy-to=<pod>-debug --image=ubuntu`. Immediately afterward, what is the state of the original Pod?

- A) Terminated and replaced by the copy
- B) Running, but with the ubuntu container now attached to it
- C) Running, entirely unchanged
- D) Paused until the debug session ends

**5.** An init container's job is `mkdir /data/cache`. The workload deploys cleanly. Three weeks later the node is drained and the Pod is rescheduled; the Pod now fails to start. What is the most likely explanation?

- A) The PersistentVolume failed to reattach on the new node
- B) The init container is not idempotent and fails when the directory already exists
- C) The init container image was garbage-collected from the new node
- D) Init containers do not run on rescheduled Pods

**6.** `[retrieval: ch2]` You run `kubectl exec -it <pod> -- /bin/sh` and get `stat /bin/sh: no such file or directory`. What does this tell you about the image?

- A) The image is corrupted and needs to be repulled
- B) The container runtime does not support `exec`
- C) The image was built without a shell — it contains only what was put into it
- D) `/bin/sh` exists but the container is running as a user without execute permission on it

---

**Answers with Explanations:**

**1 — B.** Every element of the mechanical test points the same way: the workload is running, ready, and stable; the fault does not extend beyond it; and no platform signal is adverse.

- **A is wrong** because HTTP status codes are application output. The kubelet has no opinion about your response bodies, and a 500 is not a container failure — the container is working fine, returning exactly what your code told it to return.
- **C is wrong** and this is the important distractor. It is true that you may lack node-level access. It is not true that this makes the diagnosis indeterminate — §1's addition to the test says the opposite. You make the case from what you *can* see, and here what you can see is conclusive.
- **D is wrong** because a readiness probe asserts that the container is willing to receive traffic, not that it produces correct answers. A probe that hits `/healthz` and gets a 200 will pass happily while every other endpoint returns garbage *[cross-bearing: see Ch 5 §7 — liveness, readiness, and startup probes]*.

**2 — B.** `Init:1/3` means the first init container completed and the second is where you are. Name it with `-c` and read its output.

- **A is wrong** — the most common time-waster in this whole section. The plain form targets an app container that has not started; you get nothing useful, and the nothing looks like silence rather than like a misdirected question.
- **C is wrong** because there is no app container running to exec into. You would need `-c` here too, and even then, exec into a *running* init container is a narrow move that only helps if the init container is hanging rather than exiting.
- **D is wrong** because nothing is listening. `port-forward` requires a running process on the target port; this Pod has not reached its application yet.

**3 — B.** This is the Fixed Point stated as a question. The container list is fixed at Pod creation, so a mechanism to add a *temporary* container had to be built outside the normal spec-editing path — hence the dedicated `ephemeralcontainers` API handler [source: k8s-docs-ephemeral-containers-concept-2026-08-31].

- **A is wrong** — ephemeral containers use the same runtime as every other container in the Pod.
- **C is wrong** — they run in the existing Pod, on the node the Pod is already on. That is the entire point; a container on another node would see none of the state you are trying to inspect.
- **D is wrong** — RBAC can grant permissions on the ephemeral containers subresource. The constraint is architectural, not authorization-based.

**4 — C.** Unchanged, still running, still serving. The copy is a separate Pod.

- **A is wrong** and is the misconception this option exists to catch. Nothing is deleted. If `--copy-to` terminated the original, it would be useless for its main purpose — debugging something you cannot afford to disturb.
- **B is wrong** — that describes the plain ephemeral-container form (`kubectl debug` without `--copy-to`), which is a different shape answering a different question.
- **D is wrong** — Kubernetes has no notion of pausing a Pod for inspection.

**5 — B.** A fresh deploy hits an empty volume and `mkdir` succeeds. A rescheduled Pod re-runs every init container [source: k8s-docs-init-containers-2026-08-24] against a volume where `/data/cache` already exists, `mkdir` exits non-zero, and the Pod is stuck. Classic non-idempotency.

- **A is possible in principle but is the wrong first answer** — and it is the wrong first answer in a specific, instructive way. A PV reattachment failure is platform scope, would produce a different signature (the Pod stuck on volume mounting, with events saying so), and would not be preceded by three weeks of clean operation followed by an init failure specifically. Reach for the application-scope explanation when the application-scope signature is what you're looking at.
- **C is wrong** — a garbage-collected image is repulled, and a pull failure has its own distinctive signature *[cross-bearing: see Ch 13 §2 — pods that never start]*.
- **D is wrong** and is the outright false statement in the set. Init containers run again on every Pod start, which is exactly what makes idempotency mandatory.

**6 — C.** An image contains exactly what was put into it. No shell in the image means no shell in the container — there is no host filesystem underneath supplying the gaps *[cross-bearing: see Ch 2 §2 — what's inside an image]*.

- **A is wrong** — a corrupt image fails at pull or at container creation, not with a clean "this specific path does not exist."
- **B is wrong** — the runtime supports `exec` fine. It attempted the exec and reported, accurately, that the binary you named is not there.
- **D is wrong** — a permission problem produces a permission error. `no such file or directory` is a statement about existence.

---

**Checkpoint: You've Now Mastered**

✓ Placing a fault on the correct side of the scope boundary, including when you cannot see the other side
✓ The four triage questions and why "is it configured" appears twice
✓ Reading a failing init container, and the three ways one goes wrong
✓ `exec` for the container that has a shell, and why the config the process *read* is the thing worth checking
✓ Ephemeral containers, `kubectl debug`, and the three shapes it takes

Two questions remain: is it reachable, and what changes when the replicas aren't interchangeable. The next section is the one where a perfectly correct Service does nothing at all.

---

## 🔵 §4 — Is Anything Even Selected

You have a Service. It exists. `kubectl get service` returns it, complete with a ClusterIP. Requests to it fail.

Chapter 9 gave you the model: a Service is a name and a selector, and behind the name is a list of endpoints assembled by matching that selector against Pod labels *[cross-bearing: see Ch 9 §4 — the list behind the name]*. Chapter 9 also told you, in as many words, that this chapter owns the troubleshooting workflow and would come back for those facts by name. Here we are.

The single most useful command in this section is the one that reads the list:

```
kubectl get endpointslices -l kubernetes.io/service-name=<service-name>
```

That label is not arbitrary — the control plane puts a `kubernetes.io/service-name` label on every EndpointSlice it creates precisely so you can look them up this way *[cross-bearing: see Ch 9 §4 — the list behind the name]*. And the interpretation is direct, from the docs: *"Make sure that the endpoints in the EndpointSlices match up with the number of pods that you expect to be members of your service. If they don't, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready."* [source: k8s-docs-debug-pods-2026-08-23]

> **★ Fixed Point**
>
> **A Service with no endpoints is not broken. It is working exactly as written, and selecting nothing.** There are two causes, and they live in two different files: the selector does not match the Pod labels, or the Pods match but are not Ready.

That distinction is the whole diagnostic value of the empty list. The Service object is fine. The controller is fine. Nothing has failed. Something is *mismatched*, and the mismatch is either in the label/selector relationship or in the readiness state — and knowing which of those two you are looking at tells you which file to open.

### Four break points, and two of them are not about the list

Here is where the section has to be careful, because four things can break a request to a Service and only two of them produce an empty endpoint list.

<!-- FIGURE: ch16-fig04-service-break-points -->
```
  client ──▶ DNS name ──▶ Service ──▶ EndpointSlice ──▶ Pod ──▶ container port
               │                          │                        │
               │                          │                        │
          ┌────┴────┐              ┌──────┴──────┐          ┌──────┴──────┐
          │ BREAK 4 │              │  BREAK 1+2  │          │   BREAK 3   │
          │ name    │              │  LIST EMPTY │          │ port ≠      │
          │ doesn't │              │  1 selector │          │ targetPort  │
          │ resolve │              │    mismatch │          │             │
          │ to this │              │  2 not Ready│          │ (list is    │
          │ Service │              │             │          │  POPULATED) │
          └─────────┘              └─────────────┘          └─────────────┘

  UPSTREAM of the list ....... breaks 1 and 2 → EMPTY LIST
  DOWNSTREAM of the list ..... break 3 → POPULATED LIST, request still fails
  BESIDE the whole path ...... break 4 → you never reached this Service at all
```

**Break 1 — selector/label mismatch.** The Service's `spec.selector` and the Pod template's `metadata.labels` are written in two different places, frequently in two different files, and they drift. Someone renames `app: web` to `app: web-frontend` in the Deployment and does not touch the Service. Everything applies cleanly. Nothing errors. The endpoint list goes empty and stays that way.

The docs are blunt about how ordinary this is: *"Make sure that the Pods you ran are actually selected by the Service"* [source: k8s-docs-debug-service-2026-08-31]. Check both sides:

```
kubectl describe service <service-name>        # what does it select?
kubectl get pods -l <selector-from-above>      # does anything match?
kubectl get pods --show-labels                 # what do the Pods actually carry?
```

**Break 2 — not Ready.** The Pods match perfectly. The selector is correct. And every one of them is `0/1 READY`, so none of them is in the list. Readiness gates endpoint membership — a Pod that is not ready is not a valid target, and the control plane removes it *[cross-bearing: see Ch 9 §4 — the list behind the name]*.

This is the quiet one, and it is quiet because the Pods look alive. `kubectl get pods` shows `Running`. The restart count is zero. Nothing is crashing. The `READY` column is the only place the truth is printed, and it is a column people's eyes slide past *[cross-bearing: see Ch 13 §4 — pods that start and then don't stay]*. If you have an empty endpoint list and the selector checks out, look at the readiness state before you look at anything else.

> 🪝 **Snag:** An empty endpoint list has exactly two causes, and you can tell them apart in one command. If `kubectl get pods -l <the-service-selector>` returns nothing, it's a label mismatch. If it returns Pods, look at their `READY` column — it's a readiness problem. Two causes, two different files to open: the labels live in the Deployment's Pod template, readiness lives in the probe definition.

**Break 3 — `port` vs `targetPort`.** Now a different failure shape entirely. The selector matches. The Pods are ready. The endpoint list is *populated*. And requests still fail, because the Service is delivering traffic to a port nothing is listening on.

`port` is the port the Service is reachable at. `targetPort` is the port on the Pod that traffic is forwarded to, and it is the one that has to match what the container actually binds. The docs put the question directly: *"Is the Service correct?"* and *"Is the Service defined correctly?"* [source: k8s-docs-debug-service-2026-08-31] — with the port pairing as one of the things being asked about.

```yaml
spec:
  ports:
  - port: 80          # clients connect here
    targetPort: 8080  # the container must be listening HERE
```

If the container listens on 8080 and `targetPort` says 80, everything selects correctly and every request lands on a closed port.

**Break 4 — the name.** And the fourth one is not about this Service at all: the DNS name the client is using does not resolve to the Service you have been staring at. A typo in the namespace, a name that resolves in the client's own namespace to something else, a hardcoded name from a different environment. The in-cluster form is `<service>.<namespace>.svc.<cluster-domain>` and a short name resolves relative to the *client's* namespace, not the service's *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*.

The docs' first debugging move for this is to run a Pod in the cluster and look from where the client looks: *"For many steps here you will want to see what a Pod running in the cluster sees. The simplest way is to run an interactive busybox Pod."* [source: k8s-docs-debug-service-2026-08-31] From inside that Pod, resolve the name and see what comes back — or whether anything does.

> ⚓ **Worth Securing:** Keep breaks 1–2 and breaks 3–4 in separate mental boxes. Breaks 1 and 2 produce an **empty list**. Break 3 produces a **populated list and a failed request**. Break 4 means you never reached this Service in the first place. If you conflate them, you will go hunting for a label mismatch on a Service whose endpoint list is full — and the endpoint list was telling you the answer the whole time.

---

## ⚪ §5 — Bypassing the Service on Purpose

There is a move available at this point that is more useful than it looks.

```
kubectl port-forward <pod-name> 8080:80
```

This opens a tunnel from a port on your local machine to a port on a Pod in the cluster. The docs describe the mechanism plainly: *"`kubectl port-forward` allows using resource name, such as a pod name, to select a matching pod to port forward to."* [source: k8s-docs-port-forward-2026-08-31] It is commonly used for convenience — reaching a database or an admin interface from a laptop without exposing it — and that use is real and fine and not what this section is about.

What this section is about is what happens when you use it as an experiment.

### Two paths that share almost nothing

<!-- FIGURE: ch16-fig03-portforward-vs-service-path -->
```
  THE SERVICE PATH (what your users travel)
  client ──▶ DNS ──▶ Service (ClusterIP) ──▶ service proxy ──▶ Pod:targetPort
                          │                        │
                     selector, endpoints      kube-proxy rules
                     [ §4 breaks 1-4 all live on this path ]

  THE PORT-FORWARD PATH (what you travel)
  kubectl ──▶ API server ──▶ kubelet ──▶ Pod:port
                    │
            pods/portforward subresource
            [ shares NO step with the path above except the Pod itself ]
```

The port-forward path is an API-server operation, not a networking one. The authorization requirements make this concrete: *"To use `kubectl port-forward`, a user must have permission to access the target resource (for example, a Pod or Service) and the `portforward` subresource. Typical required permissions include `get` on `pods` and `create` on `pods/portforward`."* [source: k8s-docs-port-forward-authorization-2026-08-31] You are not routing traffic through the cluster's Service machinery. You are asking the API server to open a channel to a Pod, and it does.

The same documentation notes the security consequence, which is also the diagnostic consequence: *"Cluster administrators should carefully restrict these permissions, as port-forwarding can provide direct network access to workloads and may bypass network-level controls."* [source: k8s-docs-port-forward-authorization-2026-08-31]

<!-- AUTHOR-REVIEW: no cached snapshot states the full port-forward request path (client → API server → kubelet → Pod) explicitly. The API-server involvement is established by the pods/portforward subresource and the "may bypass network-level controls" line; the kubelet hop is inferred from the general architecture and is not directly sourced. The figure above shows it. Either source the kubelet hop or redraw the figure to stop at the API server. -->

"May bypass network-level controls" is, from the diagnostic side, the entire point. If the path skipped nothing, the experiment would prove nothing.

### The inference, and the trap inside it

So: your Service call fails. You port-forward straight to a Pod behind that Service. It works. The application responds correctly.

The instinct at this moment is relief — *the app is fine.* And that instinct, left alone, is where the diagnosis stops being useful, because "the app is fine" is not a conclusion. It is half of one.

> **★ Fixed Point**
>
> **A working `port-forward` beside a failing Service call does not mean the application is fine. It means the application is fine *and the Service path is not.*** It is a narrowing step, not a clean bill of health — and the thing it narrows to is exactly the four break points in §4.

Read it as an elimination. The port-forward path shares nothing with the Service path except the Pod itself. If traffic arriving directly at the Pod produces a correct response, then the process is running, listening, and serving correctly — and every remaining candidate lives on the path you just skipped: the DNS name, the selector, the endpoint list, the service proxy, the port pairing.

> 🪢 **Mnemonic:** Port-forward is a **second road to the same house**. If the mail arrives by the back road but not the front, the house is fine and the front road is the problem. You have not fixed anything. You have halved the map.

And the negative case is just as informative. If the port-forward *also* fails — connection refused, or a hang, or the same wrong response — then the Service path is exonerated and the fault is inside the container. That sends you back to §3: exec in, check what the process is actually bound to, check what config it actually read.

> ⚓ **Worth Securing:** Note which port you forwarded to. `kubectl port-forward pod/x 8080:80` reaches container port 80. If the container is listening on 8080 and you happened to forward to 8080, you have accidentally routed around break 3 as well — and a successful port-forward on the *right* port while the Service points at the *wrong* one is precisely the `port`/`targetPort` signature. Forward to the port the container claims to use, then compare that number against the Service's `targetPort`.

One clarifying note on scope: `port-forward` is a diagnostic here, and only a diagnostic. It is not how applications reach each other in a cluster and it is not an exposure mechanism — the Service and Ingress machinery for that belongs to earlier chapters *[cross-bearing: see Ch 9 §6 — the component that makes it real]*. Also: it is TCP only, and it terminates when you stop the command.

---

## ☆ Taking Your Bearings: Reachability — What Selects, What Routes, What Proves

Five questions on §4 and §5. Two of them test material from earlier chapters — this is the checkpoint where the reachability material leans hardest on Chapter 9 and Chapter 5, so it is where that dependency gets verified.

**1.** `kubectl get endpointslices -l kubernetes.io/service-name=api` returns a slice with zero endpoints. `kubectl get pods -l app=api` returns three Pods, all `Running`, all `0/1 READY`. What is the cause?

- A) A selector/label mismatch between the Service and the Pod template
- B) Readiness is holding the Pods out of the endpoint list
- C) A `port`/`targetPort` mismatch on the Service
- D) The EndpointSlice controller has failed

**2.** `[retrieval: ch9]` A Service is defined with `port: 80` and `targetPort: 8080`. Which port must the container inside the Pod be listening on?

- A) 80
- B) 8080
- C) Either — Kubernetes tries both
- D) Neither; the container port is set by `containerPort` and is independent of the Service

**3.** You port-forward directly to a Pod behind a failing Service and the application responds correctly. What have you established?

- A) The application is working, so the incident is resolved
- B) The application serves correctly, and the fault is somewhere on the Service path
- C) The Service is correctly configured but the Pod is unhealthy
- D) Nothing — port-forward and the Service path are equivalent

**4.** `[retrieval: ch5]` A Pod is `Running` with a restart count of 0, and its readiness probe is failing. What is the state of its liveness probe, and what does that combination mean for traffic?

- A) Liveness must also be failing; the container will be restarted shortly
- B) Liveness is passing (or absent) — the container is not restarted, but it receives no Service traffic
- C) Liveness is irrelevant to readiness; the Pod receives traffic normally
- D) Readiness failure forces liveness failure after the failure threshold

**5.** A client Pod in namespace `frontend` calls `http://api/` and gets no response. The Service `api` exists in namespace `payments`, with a populated endpoint list. What is the most likely cause?

- A) The Service selector does not match its Pods
- B) The short name `api` resolves relative to the client's own namespace, not `payments`
- C) The Pods behind `api` are not Ready
- D) `port` and `targetPort` are mismatched on the `api` Service

---

**Answers with Explanations:**

**1 — B.** The Pods match the selector — they were returned by a query using it — so the labels are correct. `0/1 READY` on all three means readiness is holding every one of them out of the list.

- **A is wrong** because the label query returned Pods. If the selector didn't match, `kubectl get pods -l app=api` would have returned nothing, which is precisely how you tell the two causes apart.
- **C is wrong** because a `port`/`targetPort` mismatch produces a *populated* list and a failed request. It is downstream of the list; it cannot empty it.
- **D is wrong** and it is the "blame the platform" distractor. An empty list here is the controller working correctly — it is faithfully reporting that nothing eligible was found. Reaching for controller failure is the reflex §1 exists to break.

**2 — B.** `targetPort` names the port on the Pod that traffic is delivered to, so the container must be listening on 8080. `port: 80` is the port clients use to reach the Service *[cross-bearing: see Ch 9 §3 — four ways to be reachable]*.

- **A is wrong** — that inverts the two, which is exactly the confusion this question exists to catch.
- **C is wrong** — there is no fallback behavior. Traffic goes to `targetPort` and nowhere else.
- **D is half-true and therefore the most dangerous option.** `containerPort` in the Pod spec is largely informational, and the container's actual listening port is set by the application, not by Kubernetes. But `targetPort` is absolutely not independent of it — `targetPort` is where traffic is *sent*, and if the container isn't listening there, the request fails. The two must agree.

**3 — B.** The narrowing step. The port-forward path shares no step with the Service path except the Pod itself, so a correct response proves the process serves correctly, and moves every remaining candidate onto the Service path.

- **A is wrong** and is the trap this section is built around. Users travel the Service path. You just proved the Service path is broken. Nothing is resolved.
- **C is wrong** — it inverts the finding. You reached the Pod directly and it answered; the Pod is demonstrably healthy in the way that matters.
- **D is wrong** — the two paths differ almost entirely, which is what gives the experiment its power. If they were equivalent, both would fail identically.

**4 — B.** A zero restart count tells you liveness is not failing — a failing liveness probe restarts the container and increments that counter. So liveness is passing or not configured, the container keeps running, and readiness independently keeps it out of every Service endpoint list *[cross-bearing: see Ch 5 §7 — liveness, readiness, and startup probes]*.

- **A is wrong** — the restart count of 0 rules it out directly, and the two probes are independent. That independence is the design: readiness failing means "don't send me traffic," liveness failing means "kill me."
- **C is wrong** — readiness gates endpoint membership. A not-ready Pod gets no Service traffic at all.
- **D is wrong** — there is no such escalation. Neither probe influences the other's result.

**5 — B.** A short Service name resolves through the client's search domains, which start with the client's own namespace. A Pod in `frontend` asking for `api` looks for `api.frontend.svc.cluster.local` first. The fully qualified form `api.payments.svc.cluster.local` — or at minimum `api.payments` — is required to cross namespaces *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*.

- **A and C are wrong** for the same reason: the stem states the endpoint list is populated, which rules out both empty-list causes. Read the given facts before choosing a cause they exclude.
- **D is wrong** because a port mismatch would produce a connection to the Service that fails at the Pod — a refused connection or a timeout from a real target — rather than the resolution failure the namespace crossing produces. Different signature, and distinguishing signatures is the skill.

---

**Checkpoint: You've Now Mastered**

✓ Reading an endpoint list, and what an empty one actually means
✓ Telling the two empty-list causes apart in one command
✓ Keeping upstream breaks (empty list) separate from downstream ones (populated list, failed request)
✓ Using `port-forward` as an elimination step rather than a verdict

Two sections left. The first is what changes when the replicas are not interchangeable — where "the app is broken" turns out to mean "`web-2` is broken, and the other two are fine."

---

## 🟡 §6 — When Each Replica Is Its Own

Everything so far has assumed something that is usually true and sometimes catastrophically false: that your replicas are interchangeable. That if you diagnose one, you have diagnosed all of them.

For a Deployment, that assumption holds. Three replicas of a stateless service are three instances of the same thing; whichever one you exec into will tell you the same story. For a StatefulSet it does not hold at all, and the four questions have to be asked of a *particular* replica rather than of the workload.

Three things make this different, and each is a retrieval you already have with a diagnostic turn on it.

### Find out which one

A StatefulSet's Pods have stable ordinal identity — `web-0`, `web-1`, `web-2`, and that identity sticks across rescheduling *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*. The diagnostic consequence: **"the app is broken" is very frequently "`web-2` is broken, and `web-0` and `web-1` are fine."**

So the first move is not to investigate. It is to find out which replica you are investigating.

```
kubectl get pods -l app.kubernetes.io/name=MyApp
```

The docs give exactly this form for listing a StatefulSet's Pods by label [source: k8s-docs-debug-statefulset-2026-08-31]. Look at the whole list before you pick one. A single unhealthy ordinal among healthy siblings is a completely different diagnosis from all three being unhealthy — the first says something is wrong with that replica's *state*, the second says something is wrong with the *workload*.

The docs also flag one specific case worth knowing: a Pod in `Unknown` or `Terminating` state can block the StatefulSet controller from making progress, because the controller's ordering guarantees mean it will wait rather than proceed past an uncertain replica [source: k8s-docs-debug-statefulset-2026-08-31]. A StatefulSet that seems frozen mid-rollout usually has one Pod in one of those states, and the freeze is the controller obeying its own rules *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*.

<!-- AUTHOR-REVIEW: the Kubernetes "Debug a StatefulSet" page is a stub — it contains only the label-selector listing form and the Unknown/Terminating pointer, and nothing on per-replica PVC debugging, ordinal-specific triage, or headless-Service peer DNS. The remainder of this section is built from the Ch 6 and Ch 11 snapshots (k8s-docs-statefulset-2026-08-24, k8s-docs-statefulset-storage-2026-08-25) plus the DNS snapshot. Flagged so the fact-accuracy audit knows the sourcing is indirect by necessity, not by oversight. -->

### The state that survives everything you try

This is the one that most looks like a platform fault and is not.

Each StatefulSet replica gets its own PersistentVolumeClaim from `volumeClaimTemplates`, and that claim follows the identity *[cross-bearing: see Ch 11 §6 — Pods that are not interchangeable, revisited]*. The claim is not deleted when the Pod is deleted. The default retention policy is `Retain` for both the scale-down and the delete case: *"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted"* and *"The default for policies is Retain, matching the StatefulSet behavior before this new feature."* [source: k8s-docs-statefulset-storage-2026-08-25] And for the involuntary case: *"if a Pod associated with a StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch."* [source: k8s-docs-statefulset-storage-2026-08-25]

Now put that next to the most common debugging reflex in the industry.

Your application writes a corrupt record. `web-2` starts failing. You delete `web-2`. The controller recreates it, with the same name, the same DNS record, and **the same volume, containing the same corrupt record.** It fails again, identically. You delete it again. Same result.

> ⚠ **Navigational Hazards**
>
> **"Turn it off and on again" does not clear a StatefulSet replica's state, and the failure it leaves behind looks exactly like a platform bug.**
>
> The symptom is a replica that fails, gets deleted, comes back, and fails in precisely the same way — repeatedly, deterministically, immune to every restart. That signature reads as "something in the cluster is broken," and engineers have spent days on it from that angle.
>
> It is not the cluster. The PVC survived, by design, because throwing away a stateful workload's data on a restart would be the worse failure by a wide margin. The state is the thing that is broken, and no amount of restarting will touch it. Go look at the data: exec into the replica and inspect what is on the volume, or mount the PVC into a debug Pod and read it there.
>
> The diagnostic tell that separates this from a genuine platform fault: **it is deterministic and it is confined to one ordinal.** A platform problem would not preferentially afflict `web-2` and leave `web-0` and `web-1` untouched across repeated rescheduling.

> 🔭 **Closer Look:** `.spec.persistentVolumeClaimRetentionPolicy` has two settings — `whenDeleted` and `whenScaled` — each accepting `Delete` or `Retain`, with `Retain` the default for both [source: k8s-docs-statefulset-storage-2026-08-25]. A workload configured with `whenScaled: Delete` behaves differently on scale-down than the default described above. Check the StatefulSet's actual policy before you reason about what a deletion did; the default is only the default.

### Peers that find each other by name

The third difference is discovery. A StatefulSet uses a headless Service to give each Pod its own DNS name *[cross-bearing: see Ch 9 §5 — when you don't want a single address]*, and the form is `$(podname).$(governing service domain)` — for example `web-0.nginx.default.svc.cluster.local` [source: k8s-docs-statefulset-2026-08-24]. Replicas use these names to find each other: a database forming a cluster, a queue electing a leader, a cache building a ring.

That creates failure modes a ClusterIP workload never sees. If `web-1` cannot resolve `web-2`'s name, the peer relationship fails while both Pods look perfectly healthy from outside. And there is a genuine timing trap here, which the docs call out directly: *"Depending on how DNS is configured in your cluster, you may not be able to look up the DNS name for a newly-run Pod immediately. This behavior can occur when other clients in the cluster have already sent queries for the hostname of the Pod before it was created. Negative caching (normal in DNS) means that the results of previous failed lookups are remembered and reused, even after the Pod is running, for at least a few seconds."* [source: k8s-docs-statefulset-2026-08-24]

So a peer that came up, failed to resolve a sibling that did not exist yet, cached the negative result, and gave up — is a real and reproducible failure that has nothing to do with your code and everything to do with startup ordering. The diagnostic move is to resolve the peer names from inside a replica and see what comes back:

```
kubectl exec -it web-1 -- nslookup web-2.nginx
```

> 🪝 **Snag:** A headless Service is required for a StatefulSet's network identity, and **you are responsible for creating it** — the StatefulSet controller does not create it for you [source: k8s-docs-statefulset-2026-08-24]. A StatefulSet whose `serviceName` names a Service that does not exist will run, and its Pods will have no resolvable per-Pod DNS names. Peer discovery fails, and nothing in the Pod's own status says why.

The unifying point across all three: for a StatefulSet, "which replica" is a question you have to answer before any of the other four questions mean anything.

---

## 🟡 §7 — Before You Ship It

The fastest debugging loop is the one that runs on your own machine, where you have a debugger, an IDE, and a rebuild that takes two seconds instead of a container build and a rollout.

The judgment call is knowing when that loop is worth building and when the reproduction is worthless before you start.

### The dividing line

Some things about your application exist only in the cluster. Not "are easier in the cluster" — exist only there, and cannot be reproduced locally by definition:

- **Cluster-supplied identity.** The ServiceAccount token projected into the Pod, and everything it authorizes *[cross-bearing: see Ch 12 §2 — who you are]*.
- **Cluster DNS.** Any name resolution through `svc.cluster.local`, including peer discovery.
- **Injected configuration.** ConfigMaps and Secrets mounted or projected into the container. You can copy the values locally, but you are then testing a copy, and if the bug is that the value *isn't what you think*, you have just reproduced your own misunderstanding.
- **Admission mutation.** Anything a mutating webhook or a sidecar injector added to your Pod after you submitted it. Your local process was never mutated *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*.
- **Service routing.** Everything in §4. A local process is not behind a Service, has no selector, and appears in no endpoint list.

Everything else — your business logic, your parsing, your request handling, your math — usually reproduces locally just fine, and reproducing it there is much faster than reproducing it in a cluster.

> ⚓ **Worth Securing:** Before you build a local reproduction, ask one question: *does the failing behavior depend on anything the cluster supplies?* If yes, a local reproduction will either fail to reproduce the bug or reproduce a different one — and either outcome is worse than not trying, because both are misleading. That question takes ten seconds and routinely saves an afternoon.

### The pattern that resolves it

There is a third option between "reproduce it locally" and "debug it in the cluster," and it is the one worth knowing by shape: **proxy a local process into the cluster, so that your code runs on your machine with your debugger attached, while seeing the cluster's real dependencies.**

The Kubernetes documentation describes the motivation exactly: *"Kubernetes applications usually consist of multiple, separate services, each running in its own container. Developing and debugging these services on a remote Kubernetes cluster can be cumbersome, requiring you to get a shell on a running container in order to run debugging tools."* [source: k8s-docs-local-debugging-telepresence-2026-08-31] The tool the docs walk through for this is **Telepresence**, described as *"a tool to ease the process of developing and debugging services locally while proxying the service to a remote Kubernetes cluster,"* which *"allows you to use custom tools, such as a debugger and IDE, for a local service and provides the service full access to ConfigMap, secrets, and the services running on the remote cluster."* [source: k8s-docs-local-debugging-telepresence-2026-08-31]

That last clause is the whole pattern in one line: your process, their cluster's dependencies. The list above stops being a list of things you cannot reproduce, because you are not reproducing them — you are using the real ones.

Telepresence is one instance of the pattern and the one the Kubernetes docs happen to document. The tooling in this space changes; the pattern does not. Learn the shape — a local process, proxied into the cluster's network and configuration — and you will recognize whichever tool is current when you need one.

> 🔭 **Closer Look:** There is also a fourth option worth naming, which is running a small local cluster — kind, minikube, or k3s — rather than proxying into a shared one *[cross-bearing: see Ch 8 §5 — who owns the control plane]*. That gets you real cluster DNS, real ServiceAccounts, real admission, and real Services, on your laptop. What it does *not* get you is *their* cluster's config, *their* webhooks, and *their* network policy — so it reproduces the class of bug, not the instance. Useful for "does my manifest work at all," not for "why does it fail in staging."

Which brings the practical arc to its end. Four questions, five tools, one boundary — and one thing left to say about why the boundary was the point all along.

---

## ☆ Taking Your Bearings: Identity, Storage, and the Limits of Reproducing It Locally

Five questions on §6 and §7. One tests material from an earlier chapter.

**1.** A three-replica StatefulSet has one failing Pod, `db-1`. You delete it. The controller recreates `db-1`, which fails identically. You delete it twice more with the same result. What is the most likely cause?

- A) A node-level fault on whichever node `db-1` keeps landing on
- B) Corrupt or unexpected state on `db-1`'s PersistentVolumeClaim, which survives every deletion
- C) The StatefulSet's image is broken and needs to be repulled
- D) An admission webhook is rejecting `db-1` specifically

**2.** `[retrieval: ch11]` What is the default `persistentVolumeClaimRetentionPolicy` for a StatefulSet, for both the `whenDeleted` and `whenScaled` cases?

- A) `Delete` for both
- B) `Retain` for both
- C) `Retain` for `whenDeleted`, `Delete` for `whenScaled`
- D) There is no default; the field must be set explicitly

**3.** A StatefulSet's Pods run normally, but the replicas cannot discover each other and the cluster never forms. All Pods are `Running` and `Ready`. What should you check first?

- A) The readiness probe definitions
- B) The headless Service named by `serviceName`, and whether per-Pod DNS names resolve
- C) The `port`/`targetPort` pairing on the workload's ClusterIP Service
- D) The PersistentVolumeClaims for each ordinal

**4.** A bug appears only when the application runs in the cluster. The failing code path reads a value that a mutating admission webhook injects into the Pod. Is a local reproduction useful?

- A) Yes — copy the injected value into a local environment variable and run it locally
- B) No — the value's origin is the thing in question, and a local copy reproduces your assumption rather than the bug
- C) Yes — mutating webhooks run identically against local processes
- D) No — but only because local machines cannot run containers

**5.** Which of these is genuinely reproducible on a laptop, without any cluster or proxy?

- A) A ServiceAccount token's permissions against the API server
- B) A parsing error in the application's handling of a malformed request body
- C) A Service selector that fails to match its Pods
- D) Peer discovery through headless-Service DNS names

---

**Answers with Explanations:**

**1 — B.** The PVC follows the ordinal identity and survives Pod deletion by default [source: k8s-docs-statefulset-storage-2026-08-25]. Recreating the Pod reattaches the same volume with the same contents, so a state-caused failure reproduces exactly, every time.

- **A is wrong,** and the reasoning matters more than the answer. A node fault would not follow a specific ordinal across repeated rescheduling — the replacement Pod may well land somewhere else. Deterministic failure confined to one ordinal points at that ordinal's *state*, not at hardware.
- **C is wrong** — a broken image would fail all three replicas identically, since they share a Pod template. The confinement to one ordinal rules it out.
- **D is wrong** — an admission rejection would prevent the Pod from being created at all, producing a different signature entirely, and admission does not discriminate by ordinal.

**2 — B.** `Retain` for both, which is why deleting a replica does not clear its storage [source: k8s-docs-statefulset-storage-2026-08-25].

- **A is wrong** and would be actively dangerous as a default — it would mean a scale-down silently destroyed data.
- **C is wrong,** but it is a real configuration many teams choose deliberately. It is not the default, and assuming it is will cost you the diagnosis in question 1.
- **D is wrong** — the field is optional with documented defaults.

**3 — B.** Peer discovery in a StatefulSet runs on per-Pod DNS names provided by the headless Service, and you are responsible for creating that Service yourself [source: k8s-docs-statefulset-2026-08-24]. If it is missing or misnamed, the Pods run fine and simply cannot find each other.

- **A is wrong** — the stem says every Pod is `Ready`, so probes are passing.
- **C is wrong** — this is peer-to-peer traffic between replicas by individual name, not client traffic through a ClusterIP.
- **D is wrong** — a storage fault would show as a replica failing, not as healthy replicas that cannot see each other.

**4 — B.** The bug is about what the webhook injected. Copying a value you believe it injected tests your belief, not the system — and if your belief is the wrong part, the local run passes and tells you nothing.

- **A is wrong** for exactly that reason, and it is the appealing wrong answer because it *feels* like rigor.
- **C is wrong** — admission controllers run in the API server request path. A local process never passes through them.
- **D is wrong** on its facts. Local machines run containers fine; that is not the constraint here.

**5 — B.** Parsing logic is your code operating on your input, with no cluster-supplied dependency anywhere in the path. Reproduce it locally, fix it in seconds.

- **A, C, and D are all wrong** for the same reason, which is the point of the question: each depends on something only a cluster supplies — API-server authorization for a projected token, Service selection against real Pod labels, and cluster DNS respectively. All three are on §7's list.

---

**Checkpoint: You've Now Mastered**

✓ Asking "which replica" before asking anything else about a StatefulSet
✓ The surviving-PVC signature, and why it impersonates a platform fault
✓ Headless-Service peer DNS as a failure surface that ClusterIP workloads never have
✓ Which failures a local reproduction can and cannot reach, and the proxy pattern for the rest

🏆 **Safe Harbor reached** — the practical material of this chapter is behind you. One section remains, and it is about what the last two chapters were actually for.

---

## ☀️ §8 — Mine, or the Platform's

Here is the thing that has been true since Chapter 13 opened and has not been said outright until now.

These were never two chapters about two subjects. **The boundary is the method.**

Chapter 13 taught you to read the phase first — and the phase's last and most valuable answer, the one it works toward, is *"this is no longer mine."* Every signature in that chapter was a way of narrowing until the platform's contribution was fully accounted for. Chapter 16 taught you four questions, and their real function is not to find the bug either. It is to keep narrowing until the bug has nowhere left to be.

Same move. Different altitude.

<!-- FIGURE: ch16-zenith-mine-or-the-platforms -->
```
   PLATFORM SCOPE                    │                 APPLICATION SCOPE
   (Ch 13)                           │                 (Ch 16)
                                     │
   phase ──▶ conditions ──▶ events   │   running? ──▶ healthy? ──▶ reachable?
        ──▶ logs ──▶ node            │        ──▶ configured? ──▶ which replica?
                                     │
              ─────────────────────▶ │ ◀─────────────────────
                   narrowing         │        narrowing
                                     │
                            THE BOUNDARY
                    ( this line is the method )
```

Look at what each half of the arc did with its tools. Chapter 13's tools — `describe`, `events`, `logs --previous`, the node conditions — all answer questions about whether the cluster kept its promises. This chapter's tools — `exec`, `debug`, `port-forward`, `get endpointslices` — all answer questions about whether *you* kept yours. Neither set can answer the other's questions, and the reason the tools were split across two chapters is that the questions are split across one line.

The practitioner move is not knowing more commands. It is placing a failure on the correct side of that line quickly, and then staying on that side until the evidence moves you. Ninety seconds of scope triage saves an afternoon of confidently investigating the wrong half — and an engineer who does that reliably is doing the thing that separates someone who works with Kubernetes from someone who has read about it.

This is a shape you have met before in this book: narrowing by elimination, applied until only one candidate is left. What is different here is that the narrowing crosses an ownership boundary, which means the last step is not "I found it" but "I know whose it is." On somebody else's cluster, those are equally valuable outcomes — and knowing which one you have reached, and being able to show your work for it, is what makes you good to work with.

The chapter title is "Your Application, Their Cluster." Both halves are true at once, permanently, and the whole skill is knowing which half you are standing on.

---

## Exam Alert! 🚨

**High-Priority Topics:**

1. **Which verb answers which question.** This is the shape the exam favors for this competency. `logs` for what it said. `exec` for what it can see. `debug` for when there is nothing to exec into. `port-forward` for where the break is. `describe service` and `get endpointslices` for whether anything is even selected. You are being tested on the mapping, not on flag syntax.

2. **Ephemeral containers exist because a Pod's container list is immutable.** That single fact explains the entire mechanism — why it needs a dedicated API handler, why `kubectl edit` cannot do it, why the container cannot be removed once added [source: k8s-docs-ephemeral-containers-concept-2026-08-31].

3. **`kubectl debug` has three shapes.** Inject into the running Pod; `--copy-to` a copy; `node/` for the host. Each answers a different question and they are not interchangeable.

4. **An empty endpoint list has two causes** — selector mismatch, or Pods not Ready — and they live in two different files [source: k8s-docs-debug-pods-2026-08-23].

**Common Traps:**

| Trap | The correct understanding |
|---|---|
| Assuming `kubectl exec ... -- sh` works on any container | It requires a shell *in the image*. A distroless image has none, which is the whole reason ephemeral containers exist [source: k8s-docs-ephemeral-containers-concept-2026-08-31]. |
| Expecting `kubectl debug` to repair the broken Pod | It adds a process to look with, or makes a copy to experiment on. It fixes nothing, and an ephemeral container cannot be removed once added [source: k8s-docs-ephemeral-containers-concept-2026-08-31]. |
| Reading `--copy-to` as "debug the running Pod" | It is the opposite. The original is untouched — which is precisely the point on a workload you did not deploy. |
| Treating a working `port-forward` as proof the application is fine | It proves the application is fine **and** the Service path is not. Narrowing step, not clean bill of health. |
| Confusing `port` with `targetPort` | `targetPort` is the port the container listens on. A mismatch produces a Service that selects perfectly and routes into nothing. |
| Reading an empty EndpointSlice as a broken Service | The Service is correct and selecting nothing. Two different bugs, two different files. |
| Running plain `kubectl logs` on a Pod stuck in init | You get nothing useful. Name the init container with `-c` [source: k8s-docs-debug-init-containers-2026-08-31]. |
| Assuming a rescheduled StatefulSet replica comes back with empty storage | The PVC follows the identity and is retained by default [source: k8s-docs-statefulset-storage-2026-08-25]. A corrupt write survives every restart you try — which is exactly why it impersonates a platform fault. |
| Assuming `kubectl debug` always succeeds if you have RBAC for it | A debug container is a container. Under `restricted` enforcement, admission can refuse it *[cross-bearing: see Ch 12 §6 — three levels, three modes]*. |
| Treating D3 Debugging as a different subject from D2 Troubleshooting | The split is *scope*, not tooling. A question tagged to one may test the other's commands, because the commands do not respect the domain boundary — only the questions do. |

---

## Practice Questions

**Q1.** An application's Pod is `Running`, `1/1 Ready`, has zero restarts, and sits on a node reporting no adverse conditions. The application returns stale data. Three other Deployments in the namespace are unaffected. Which is the correct first move?

A) File a platform ticket; every application-side signal is clean
B) Treat it as application scope and begin the four triage questions
C) Delete the Pod to force a reschedule onto a different node
D) Check node conditions across the whole cluster before deciding

**Q2.** You are on a cluster where you cannot list nodes or read events in `kube-system`. A single workload of yours is failing while everything else in your namespace runs normally. What does §1's addition to the scope test say you should do?

A) Escalate immediately, because the scope test cannot be completed without node access
B) Make the application-scope case from the evidence you can gather, and be ready to show it if you later need the platform team
C) Assume platform scope by default, since the unverifiable half is the platform's
D) Request node access before starting any diagnosis

**Q3.** A Pod reports `STATUS: Init:2/4`. What is true?

A) Two init containers have completed and the third is running or failing
B) Two of four app containers have started
C) Two init containers failed and two remain
D) The Pod is `Running` with two containers ready

**Q4.** An init container runs `git clone` into a mounted volume. The workload deploys successfully. After the Pod is evicted and rescheduled, it will not start. What is the most likely cause?

A) The volume failed to reattach on the new node
B) The init container is not idempotent — the clone target already exists
C) The git repository became unreachable
D) Init containers are skipped on rescheduled Pods, so setup never ran

**Q5.** A Pod sits at `Init:0/1` for twenty minutes. No errors, no restarts, and the init container's log reads `waiting for service endpoint...`. The Service it is waiting on selects only this workload's Pods. What is happening?

A) A DNS failure is preventing the lookup
B) An ordering deadlock — the init container waits for an endpoint that only this Pod could provide
C) The init container image is being pulled slowly
D) The readiness probe on the init container is failing

**Q6.** You need to inspect the filesystem of a running container built from a distroless image. Which is correct?

A) `kubectl exec -it <pod> -- /bin/sh`
B) `kubectl debug -it <pod> --image=busybox --target=<container>`
C) `kubectl logs <pod> --previous`
D) `kubectl cp <pod>:/ ./local-copy`

**Q7.** Which statement about ephemeral containers is correct?

A) They may define a readinessProbe to report when the debug tooling is ready
B) They may set resource requests so the debug session is guaranteed CPU
C) They cannot be removed or changed once added to a Pod
D) They are automatically restarted if the debug process exits

**Q8.** An application container crashes immediately on startup, before you can exec into it. Which `kubectl debug` shape is designed for this case?

A) An ephemeral container injected into the running Pod
B) `--copy-to`, creating a copy of the Pod with the entrypoint changed
C) `debug node/<node>` to inspect the host
D) None — a crashing container cannot be debugged with `kubectl debug`

**Q9.** You run `kubectl debug` in a namespace enforcing the `restricted` Pod Security Standard, using a debug image that runs as root. The command is refused. You have verified you hold RBAC permission for the operation. What happened?

A) RBAC permissions do not cover the ephemeral containers subresource separately
B) The debug container was rejected by admission, because it is a container and must meet the namespace's enforced standard
C) `kubectl debug` is disabled in namespaces with Pod Security Admission enabled
D) The node lacked capacity for an additional container

**Q10.** `kubectl get endpointslices -l kubernetes.io/service-name=web` returns a slice with zero endpoints. `kubectl get pods -l <the Service's selector>` returns no Pods at all. What is the cause?

A) The Pods are running but not Ready
B) The Service's selector does not match any Pod's labels
C) `targetPort` does not match the container's listening port
D) The EndpointSlice controller is not running

**Q11.** A Service's endpoint list is fully populated with three ready Pods. Requests to the Service time out. Which break point is most likely?

A) A selector/label mismatch
B) Readiness holding Pods out of the list
C) A `port`/`targetPort` mismatch delivering traffic to a closed port
D) The EndpointSlice controller has stopped reconciling

**Q12.** A Service `cache` in namespace `data` has a healthy, populated endpoint list. A client Pod in namespace `web` calls `http://cache:6379` and gets nothing. What is the most likely cause?

A) The Service's Pods are not Ready
B) The short name resolves relative to the client's namespace, so `cache` resolves in `web`, not `data`
C) `port` and `targetPort` are mismatched
D) Redis requires a headless Service

**Q13.** You port-forward to a Pod behind a failing Service and the application responds correctly on the forwarded port. What is the correct conclusion?

A) The application is healthy and the incident can be closed
B) The application serves correctly; the fault lies somewhere on the Service path, which port-forward bypassed
C) The Service is fine and the Pod's probes are misconfigured
D) The result is inconclusive, because port-forward and Service traffic take the same path

**Q14.** A three-replica StatefulSet has one replica, `queue-0`, that fails on start. You delete it; the recreated `queue-0` fails identically. `queue-1` and `queue-2` are healthy. What should you investigate first?

A) The Pod template, since all replicas share it
B) The contents of `queue-0`'s PersistentVolumeClaim, which survived the deletion
C) The node `queue-0` was scheduled onto
D) The StatefulSet's image tag

**Q15.** A bug reproduces only in the cluster. The failing code path reads a config value mounted from a ConfigMap, and you suspect the mounted value differs from what the manifest declares. Which approach actually tests the hypothesis?

A) Copy the ConfigMap's declared value into a local environment variable and run the app locally
B) Exec into the running container and read the mounted file directly
C) Re-apply the ConfigMap and restart the Deployment
D) Reproduce in a local kind cluster using the same manifests

---

**Answers with Explanations:**

**Q1 — B.** Every element of the mechanical test resolves to application scope: running, ready, stable, confined to one workload, no adverse platform signal.

- **A is wrong** because "application-side signals are clean" is a misreading. Those signals are *platform* signals reporting on your workload, and their cleanliness is what hands the problem to you.
- **C is wrong** — deleting a Pod to see what happens is the reflex the four questions exist to replace. Stale data is not a placement problem, and you would have destroyed the state you needed to inspect.
- **D is wrong** because a fault confined to one workload is already answered by the scope test; a cluster-wide node sweep is effort spent on the half you have already eliminated.

**Q2 — B.** The addition is that the boundary is also a statement about what you can see, and the practical response is to build the application-scope case from available evidence.

- **A is wrong** — the test completes fine here. Confinement to one workload plus clean workload-level signals is sufficient.
- **C is wrong** and is the failure mode this guidance exists to prevent: defaulting to "must be the platform" whenever you cannot check something. That reasoning would make every fault platform-scope on a restricted cluster.
- **D is wrong** — waiting on an access request before diagnosing is how a fifteen-minute problem becomes a two-day one.

**Q3 — A.** `Init:N/M` counts *completed init containers* out of the total [source: k8s-docs-debug-init-containers-2026-08-31]. `Init:2/4` means two are done and the third is where your attention belongs.

- **B is wrong** — the counter refers to init containers only. App containers have not started; the Pod is still `Pending`.
- **C is wrong** — the status does not count failures, and a failing init container reports `Init:Error` or `Init:CrashLoopBackOff` instead.
- **D is wrong** — a Pod in init is `Pending`, with the `Initialized` condition false *[cross-bearing: see Ch 5 §5 — Pod phase and container state]*.

**Q4 — B.** A clone into a directory that already contains a clone fails. Every init container runs again on every Pod start [source: k8s-docs-init-containers-2026-08-24], and the volume persisted across the reschedule, so the second run hits a populated target.

- **A is possible but is not the *most likely* given the stated sequence**, and the discriminator is available: a volume reattachment failure produces a Pod stuck on mounting with events saying so, not a Pod whose init container ran and exited non-zero.
- **C is possible in principle** but would have been equally likely on the first deploy. Nothing in the timeline points at the repository.
- **D is a factual error** — init containers run on every start, which is the entire reason B is the answer.

**Q5 — B.** The circular wait. The init container blocks until the Service has an endpoint; the Service can only have an endpoint once this Pod's app container is ready; the app container cannot start until the init container exits. Perfectly stable, no error, waits forever.

- **A is wrong** — a DNS failure produces resolution errors in the log, not a calm "waiting" message.
- **C is wrong** — an image pull in progress reports `Init:ImagePullBackOff` or a pulling event, and the init container's log would not exist yet *[cross-bearing: see Ch 13 §2 — pods that never start]*.
- **D is wrong** on its facts: regular init containers do not support `readinessProbe` at all [source: k8s-docs-init-containers-2026-08-24].

**Q6 — B.** A distroless image has no shell to exec into, so the move is to inject an ephemeral container that *does* have tools, targeting the container you want to inspect [source: k8s-docs-ephemeral-containers-concept-2026-08-31].

- **A is wrong** — that is the command that fails, and the failure is why this whole section exists.
- **C is wrong** — `logs --previous` returns the previous container instance's output. Useful for a crash loop, useless for inspecting a filesystem.
- **D is wrong** for a subtle and worth-knowing reason: `kubectl cp` depends on `tar` being present *in the container image*. A distroless image does not have it either.

**Q7 — C.** *"Like regular containers, you may not change or remove an ephemeral container after you have added it to a Pod."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]

- **A is wrong** — probes are explicitly disallowed, because ephemeral containers may not have ports [source: k8s-docs-ephemeral-containers-concept-2026-08-31].
- **B is wrong** — *"Pod resource allocations are immutable, so setting `resources` is disallowed."* [source: k8s-docs-ephemeral-containers-concept-2026-08-31]
- **D is wrong** — they *"will never be automatically restarted"* [source: k8s-docs-ephemeral-containers-concept-2026-08-31], which is one of the reasons they are unsuitable for building applications.

**Q8 — B.** *"you can't run `kubectl exec` to troubleshoot your container if your container image does not include a shell or if your application crashes on startup. In these situations you can use `kubectl debug` to create a copy of the Pod with configuration values changed to aid debugging."* [source: k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31] Copy it, replace the entrypoint, and now the container sits still.

- **A is wrong** — an ephemeral container needs a Pod to attach to, and while the Pod exists, the *target container* is gone again before you can look at it.
- **C is wrong** — the node is not the problem, and that shape steps across the scope boundary for no reason.
- **D is wrong** — this is exactly the case `--copy-to` was built for.

**Q9 — B.** An ephemeral container is subject to the same Pod Security Admission enforcement as any other container in the namespace. A root-running debug image does not satisfy `restricted`, and admission refuses it *[cross-bearing: see Ch 12 §6 — three levels, three modes]*.

- **A is wrong** — the stem states RBAC is verified, and the refusal comes from a later gate. Authentication, then authorization, then admission *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*.
- **C is wrong** — `kubectl debug` is not disabled by PSA. A debug container that *meets* the standard is admitted normally, which is what the `restricted` debug profile is for.
- **D is wrong** — a capacity problem produces a scheduling failure with a distinct signature, not an admission refusal.

**Q10 — B.** The label query returned nothing, which means no Pod carries the labels the Service selects. Selector mismatch.

- **A is wrong** because not-ready Pods would still *appear* in a label query — they would just be absent from the endpoint list. The label query returning empty is what distinguishes the two causes.
- **C is wrong** — a port mismatch does not affect list membership at all. It is downstream of the list.
- **D is wrong** and is the reflexive platform-blame answer. The empty list is the controller reporting correctly that nothing matched.

**Q11 — C.** A populated list means selection and readiness are both fine. The remaining candidate on that path is the port pairing: traffic arriving at a port nothing is bound to.

- **A and B are wrong** for the same reason — both produce an *empty* list, and the stem says the list is populated. This is the upstream/downstream distinction the section is built on.
- **D is wrong** — a stalled controller would leave a stale or empty list, not a correct one.

**Q12 — B.** A short name resolves through the client's search domains, which begin with the client's own namespace. From `web`, `cache` means `cache.web.svc.cluster.local`, which is not the Service in question *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*.

- **A is wrong** — the stem states the endpoint list is healthy and populated, ruling readiness out.
- **C is wrong** — a port mismatch produces a connection failure against a real target, a different signature from a name that resolves elsewhere or not at all.
- **D is wrong** — a headless Service is for per-Pod DNS identity; a Redis client reaching a single ClusterIP Service needs no such thing.

**Q13 — B.** The paths share nothing but the Pod, so success on the port-forward path localizes the fault to the Service path.

- **A is wrong** — the trap. Users travel the Service path, which you just demonstrated is broken.
- **C is wrong** — it inverts the finding. You reached the Pod and it answered correctly.
- **D is wrong** — port-forward goes through the API server, not through the Service, ClusterIP, or service proxy [source: k8s-docs-port-forward-authorization-2026-08-31].

**Q14 — B.** The PVC survives Pod deletion by default and reattaches to the recreated replica [source: k8s-docs-statefulset-storage-2026-08-25]. Deterministic failure confined to one ordinal, immune to restart, is the surviving-state signature.

- **A is wrong** — a Pod template problem would fail all three replicas, and two are healthy.
- **C is wrong** — the replacement Pod is not guaranteed to land on the same node, so a node fault would not track the ordinal so faithfully.
- **D is wrong** — the image is shared by all three replicas.

**Q15 — B.** The hypothesis is that the mounted value differs from the declared one. The only way to test it is to read what is actually mounted, in the running container.

- **A is wrong** and is the most instructive distractor: copying the *declared* value locally tests your assumption rather than the system. If the declared and mounted values differ, this reproduces the wrong one and passes.
- **C is wrong** — restarting may make the symptom vanish without ever telling you what was wrong, which means the next occurrence starts from zero.
- **D is wrong** for the same reason as A, at larger scale: a local cluster with the same manifests reproduces what the manifests *say*, not what the target cluster's mount actually produced.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| The scope boundary | Running + ready + confined to one workload = yours. On someone else's cluster, it is also a statement about what you can see. |
| The four questions | Running (§2), healthy/configured (§3), reachable (§4→§5), and for StatefulSets, *which replica* (§6). |
| Init container logs | `kubectl logs <pod> -c <init-name>`. The plain form returns nothing useful and the nothing is misleading. |
| The three init failures | Ordering deadlock (waits forever, no error) · non-idempotency (fails only on restart) · config error (exits loudly, tells you why). |
| `exec` | Answers "what did the *process* actually read," which is where the manifest and reality diverge. |
| The distroless problem | No shell in the image means no shell in the container. Hardening win, debugging cost. |
| Ephemeral containers | Exist because you cannot add a container to a running Pod. No resources, no probes, no restart, no removal. |
| `kubectl debug`'s three shapes | Inject (what does it see now?) · `--copy-to` (what if I changed something?) · `node/` (is the machine the problem? — platform scope). |
| `--copy-to` | Makes a copy. The original is untouched, and that is the feature. |
| Empty endpoint list | Two causes, two files: selector mismatch, or Pods not Ready. `kubectl get pods -l <selector>` separates them in one command. |
| Populated list, failed request | Not a selection problem. Look at `port` vs `targetPort` — `targetPort` is the one the container listens on. |
| `port-forward` | Bypasses the Service path via the API server. A working forward beside a failing Service *localizes* the fault; it does not clear the app. |
| StatefulSet debugging | Ask "which ordinal" first. The PVC survives deletion by default, so a bad write is immune to restarts and impersonates a platform fault. |
| Headless-Service peer DNS | You create the headless Service, not the controller. Missing one means healthy Pods that cannot find each other. |
| Local reproduction | Anything cluster-supplied — identity, DNS, injected config, admission mutation, Service routing — is not reproducible locally. Everything else usually is. |

---

## The Voyage Ahead

Part IV closes here, and with it the two-chapter arc that began when the platform handed you back your own problem.

You now have both halves of a single skill: reading a cluster's report on your workload, and reading your workload once the cluster has nothing left to say. That skill is worth more than any individual command in either chapter, because commands change between releases and the boundary does not.

What comes next is a change of altitude. Part V steps back from the failing workload in front of you to the ecosystem the workload lives in — what "cloud native" actually names, who decides what belongs under that word, and the four places Kubernetes deliberately lets somebody else's software in. Chapter 17 finally answers the question Chapter 1 planted and left standing on purpose, and it collects a set of interfaces you have been meeting one at a time since Chapter 2 without ever seeing them side by side.

After that, the instruments. You have spent this chapter finding out what went wrong *after* someone told you something was wrong. Chapter 18 is about the systems that tell you first.

> *"The boundary is not a wall between two teams. It is the line that tells each of them where to look."*
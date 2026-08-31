# Chapter 15: The Chart Is the Truth
## *"GitOps is the control loop you already learned, pointed at a repository"*

**Domain Weight: 16% (Cloud Native Application Delivery) [source: cncf-kcna-curriculum-pdf-2026-08-23] | Complexity: Mixed | Novelty: Paradigm-shifting**

*CNCF publishes the competency name "Application Delivery" and no sub-topic list beneath it. The allocation of that 16% across Chapters 14, 15, and 16 is this book's authored judgment, not a published split.*

---

## Attention Budget

**Total time: ~85 minutes | Recommended: Split across 2 sessions**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| 🧭 Soundings | 8 min | Medium | Before you start |
| §1 Twelve Factors, and the Ones Kubernetes Already Solved | 10 min | Low | Anytime |
| §2 Ways to Replace What's Running | 12 min | Medium | Mid-session |
| ☆ Taking Your Bearings 1 | 6 min | Medium | After a short break |
| §3 Push, or Pull | 15 min | High | Peak attention |
| §4 An Agent That Watches a Repository | 15 min | High | Peak attention |
| ☆ Taking Your Bearings 2 | 5 min | Medium | After a short break |
| §5 Ordering the Sync | 8 min | Medium | Anytime |
| §6 The Other Agent, and More Than One Cluster | 8 min | Low | Anytime |
| ☆ Taking Your Bearings 3 | 5 min | Medium | Immediately before §7 |
| §7 The Control Loop, Pointed at a Repository | 8 min | Medium | Peak attention |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*Session break suggested after ☆ Taking Your Bearings 1. Sections 3 and 4 carry the chapter's argument and deserve a fresh head.*

*If you only have 15 minutes: read §3, then read §7. Those two sections are the chapter.*

---

> *"The chart is what you meant. The cluster is what happened. The interesting question is who keeps them the same."*
> — Lodestar Ledgers

<!-- AUTHOR-REVIEW: Outline Open Question 11 flagged this epigraph as an option, not a recommendation — it reuses Ch 14's closing quote verbatim as a deliberate callback binding the two Part IV delivery chapters. The structural contract prefers outside voices for epigraphs, and a reader met this line eight pages ago, which costs arousal. Author's call: keep the callback, or substitute a practitioner quote about intent versus outcome. -->

---

## 🧭 Soundings

Before reading this chapter, try these questions. Your score determines how to approach the content — no shame in any score, just different reading strategies.

This chapter leans harder on what came before than any other in the book. Two of these questions are load-bearing: miss them and the last section will not land, and no amount of careful reading here will fix that. Better to find out now.

1. A controller holds a recorded target and observes what actually exists. What does it do when the two differ, and how often does it check?

2. A Kubernetes object has one field you write and one the system writes. Which is which, and what does it mean when the two disagree?

3. What does a Deployment's default update strategy actually do, and what do `maxSurge` and `maxUnavailable` control?

4. You install a CustomResourceDefinition on a cluster. What can now exist that could not exist before, and what still has to be true before anything actually happens?

5. A process running inside the cluster needs to create and delete objects across several namespaces. What does it need in order to be allowed to, and what decides how much it may do?

6. Where does environment-specific configuration belong, and why is baking it into the container image the wrong answer?

7. General professional knowledge, no Kubernetes required: somebody makes a change directly on a production system, outside whatever process the team normally uses. What goes wrong afterward, and when do you find out?

8. General professional knowledge: you have a repository whose commit history records what was intended. What can you do with that history that you cannot do with the current state of a running server?

<details>
<summary>Click for answers + reading strategy</summary>

1. It acts to close the gap. It takes whatever action moves current state toward desired state, and it does this continuously, in a loop that never ends, not once at creation time. *(Ch 3 §6)*

2. You write `spec`; the system writes `status`. A disagreement between them means the system has not yet reached, or can no longer reach, what you asked for. It is a report, not necessarily a fault. *(Ch 4 §2)*

3. `RollingUpdate` replaces Pods gradually, standing up new ones while taking old ones down, so the application stays available throughout. `maxSurge` caps how many Pods may exist above the desired replica count during the update; `maxUnavailable` caps how many may be missing below it. *(Ch 6 §4)*

4. A new *kind* of object can now be created and stored through the API server: the API is extended. But storage is all you get. Nothing acts on those objects unless a controller is running and watching for them. *(Ch 6 §8, and the pattern named at Ch 10 §3)*

5. It needs an identity, a ServiceAccount, and it needs RBAC grants bound to that identity. The Role or ClusterRole defines what verbs on what resources are permitted; the binding attaches that permission set to the ServiceAccount. Permissions are additive, and there is no deny rule. *(Ch 5 §6, Ch 12 §2–§3)*

6. Outside the image, in ConfigMaps and Secrets, injected at runtime. Baking it in means one image per environment, which destroys the property that makes images useful: the artifact you tested is not the artifact you ship. *(Ch 4 §4, Ch 2 §2)*

7. The system now differs from whatever the team's records say it contains, and nothing announces this. You find out later, from the wrong direction: at the next deployment, when the change is silently overwritten, or when a new person reads the records and acts on a description that stopped being true weeks ago.

8. You can see what was intended and when, who intended it, what it replaced, and — critically — you can return to any previous intent exactly, because the history is complete and each entry is fixed. A running server tells you only what is true right now. It does not tell you what anybody meant.

---

**If you got 6+ right:** Skim §1 and §2. They name things you already do. Read §3, §4, and §7 properly; that is where the chapter's argument lives, and it is an argument rather than a vocabulary list.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Before you start, re-read **Ch 3 §6** (controllers and the control loop) and **Ch 4 §2** (spec versus status). Not alongside this chapter. Before it. Those two sections are the foundation this entire chapter stands on, and §7's payoff is a retrieval of Ch 3 §6 specifically. If you missed **question 1** in particular, that re-read is not optional. Everything else here will make sense without it. The last section will not.

</details>

---

## Why This Chapter Matters

The previous chapter left you holding a package and a complaint.

You have a unit now: a chart, a set of overlays, something with a version number that installs the same way twice. It has bought you less than it should have, because the unit still gets applied by a person. Somebody with cluster credentials on a laptop, running a command from a machine nobody audits, at a moment nobody records. They apply the version they believe is current. Afterward, nothing keeps watch.

That complaint has two halves, and this chapter answers them in order.

The first half is **who applies it**. That sounds procedural, the sort of thing settled in a runbook and forgotten. It isn't. The answer determines where cluster credentials physically live, who can reach them, and how large a single mistake gets before something catches it. Change the answer and you change the security posture of the whole delivery path. We take that up in §3.

The second half is **what happens afterward**. "Afterward, nothing keeps watch" is the actual defect, and it should strike you as strange, because you have spent thirteen chapters inside a system whose entire architecture is things that keep watch. A ReplicaSet keeps watch. The scheduler keeps watch. The node controller keeps watch. Kubernetes is, structurally, a collection of processes that notice a gap and close it, forever.

So you already own the answer to the second half. You have not yet been shown that you own it. That is what §7 is for, and it is why this chapter's subtitle gives the answer away on the second line: the recognition is worth more than the surprise.

**A shift in what you are.** Up to now you have been someone who *makes changes to a cluster*. This chapter asks you to become someone who *maintains a claim about what a cluster should contain*, and then never touches the cluster again.

That is genuinely uncomfortable, and it should be said plainly rather than sold. Thirteen chapters of your growing competence have been measured in `kubectl` fluency: knowing the verb, knowing the flag, knowing which object to reach for. This chapter asks you to give up the terminal as the instrument of change. Not as an instrument of *inspection* — you will read the cluster constantly, and Chapters 13 and 16 are built on it. But as the thing you use to make something different, the terminal goes away. What replaces it is a file, a commit, and a review.

Practitioners who make this shift describe the same two feelings in sequence: first that it is slower, then that they cannot go back.

The stakes here were banked in Chapter 1, and one clause will do: this domain doubled, from 8% to 16%. Chapter 14 cashed the first half. This is the second.

**About what CNCF actually publishes.** Chapter 14 made this statement at length and it covers this chapter too, so one back-bearing rather than a repetition: the published curriculum gives a competency name, "Application Delivery," and no list of topics beneath it *[cross-bearing: see Ch 14 §1 — why a folder of YAML stops working]*. What supports the inference that GitOps belongs here is positive rather than speculative. Argo and Flux are both CNCF **graduated** projects [source: cncf-project-maturity-levels-2026-08-23], and OpenGitOps is a CNCF project [source: opengitops-principles-2026-08-23]. A CNCF exam asking about application delivery is asking about the delivery model CNCF's own graduated projects implement. That is the basis. It is a good one, and it is honest about being an inference.

One consequence runs through the rest of the chapter without further comment: nothing here is described as "frequently tested" or "commonly appears." Those claims would require a published sub-topic list, and there isn't one. What you will see instead is "easy to confuse" and "this is the distinction the material rewards," which are claims this book can actually stand behind.

> **Dead Reckoning:** GitOps is a set of four principles about how desired state is stored and applied. The desired state is declarative; it lives in a version-controlled store that keeps a complete history; software agents pull it from that store rather than having it pushed to them; and those agents continuously compare actual state against it and act to close the difference [source: opengitops-principles-v1-2026-08-31]. Argo CD and Flux are two implementations. Both are Kubernetes controllers. Continuous integration is not part of the definition.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Name** the twelve factors, and say which ones Kubernetes hands you and which remain your application's problem
- **Distinguish** the two update strategies a Deployment implements from the release patterns that need tooling above it — blue/green and canary
- **State** the four OpenGitOps principles, and explain why a pipeline that pushes to a cluster satisfies none of the last two
- **Read** a delivery agent as what it structurally is: a controller, with its desired state in an unusual place
- **Explain** what `OutOfSync` reports, why it is a signal rather than an error, and why a person can cause one without anything failing
- **Recognize** the control loop from Chapter 3 wearing different clothes, and say exactly what changed and what did not

*You'll also stop thinking of GitOps as a deployment tool, which is the misreading this chapter exists to prevent.*

---

## ⚪ §1 — Twelve Factors, and the Ones Kubernetes Already Solved

Two chapters ago you were promised a methodology's word for a thing you already do. Chapter 4 promised it about configuration *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*, and Chapter 5 promised it about shutdown *[cross-bearing: see Ch 5 §4 — scheduled once, replaced never]*. Both promises point here.

The **twelve-factor app** is a methodology for building software delivered as a service, published in 2011 and drawn from experience running a large number of applications on a shared platform. Its own summary is that a twelve-factor app uses declarative formats for setup automation, keeps a clean contract with the underlying operating system for portability, is suitable for deployment on modern cloud platforms, minimizes divergence between development and production, and can scale up without significant changes to tooling or architecture [source: twelve-factor-app-2026-08-23].

Read that list again and notice something: it predates Kubernetes by three years and describes Kubernetes exactly.

That is not coincidence and it is not prophecy. Both came out of the same problem, running many applications reliably on shared infrastructure, and arrived at the same conclusions about what an application must do to be run that way.

Here are the twelve:

| | Factor | In one line |
|---|---|---|
| I | Codebase | One codebase tracked in revision control, many deploys |
| II | Dependencies | Explicitly declare and isolate dependencies |
| III | Config | Store config in the environment |
| IV | Backing services | Treat backing services as attached resources |
| V | Build, release, run | Strictly separate build and run stages |
| VI | Processes | Execute the app as one or more stateless processes |
| VII | Port binding | Export services via port binding |
| VIII | Concurrency | Scale out via the process model |
| IX | Disposability | Maximize robustness with fast startup and graceful shutdown |
| X | Dev/prod parity | Keep development, staging, and production as similar as possible |
| XI | Logs | Treat logs as event streams |
| XII | Admin processes | Run admin/management tasks as one-off processes |

[source: twelve-factor-app-2026-08-23]

Twelve numbered rules is a poor thing to memorize and a good thing to sort. The useful question is not "what is factor VII" but **who solves this**: the platform, or you.

<!-- FIGURE: ch15-fig01-twelve-factor-in-kubernetes -->
```
   THE PLATFORM GIVES        THE PLATFORM MAKES       STILL YOUR APPLICATION'S
   YOU THIS                  THIS EASY                PROBLEM

   III  Config               IV   Backing services    I    Codebase
   VI   Processes            V    Build/release/run   II   Dependencies
   VIII Concurrency          X    Dev/prod parity     VII  Port binding
   IX   Disposability                                 XII  Admin processes
   XI   Logs

   ConfigMaps, Secrets,      Services, image tags,    Your repo, your
   Deployments, SIGTERM,     namespaces per env       Dockerfile, your
   stdout collection                                  code
```

**Figure 15.1 — The twelve factors, sorted by who solves them.** The three columns are the argument: twelve unrelated-looking rules resolve into things the platform already does for you, things it removes the friction from, and things that remain entirely yours. The middle column is where most of the disappointment lives — Kubernetes makes dev/prod parity *achievable*, not automatic.

Four of these deserve development, because each one is a name for something you have already been taught.

### Factor III — Config

*"An app's config is everything that is likely to vary between deploys (staging, production, developer environments, etc)."* [source: twelve-factor-iii-config-2026-08-31]

The methodology's test for whether you have done this correctly is unusually sharp: *"A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials"* [source: twelve-factor-iii-config-2026-08-31]. That is a test you can run against your own repository this afternoon, and it is more honest than most compliance checklists.

The instruction is "store config in the environment," and this is where readers slip. It does **not** mean "put it in a config file." The document is explicit that a config file is an improvement over hard-coded constants but *"still has weaknesses: it's easy to mistakenly check in a config file to the repo"* [source: twelve-factor-iii-config-2026-08-31]. The prescription is environment variables, precisely because they live outside the codebase and cannot be accidentally committed.

Kubernetes gives you this in the form you already know: ConfigMaps and Secrets, mounted as environment variables or as files *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. The object model was designed for factor III.

> 🪝 **Snag:** "Store config in the environment" is a claim about *where config lives relative to your code*, not about the literal `env:` block. A ConfigMap mounted as a file satisfies factor III perfectly well: the file is supplied by the deploy environment, not checked into the repository. Readers who take the phrase literally conclude that mounted-file config violates the methodology. It doesn't.

One more piece of factor III catches people, and it is worth carrying. The methodology objects to grouping variables into named environments: *"In a twelve-factor app, env vars are granular controls, each fully orthogonal to other env vars. They are never grouped together as 'environments', but instead are independently managed for each deploy"* [source: twelve-factor-iii-config-2026-08-31]. If you have ever watched a `staging` config bundle acquire a permanent, load-bearing difference from `production` that nobody remembers introducing, you have seen why.

### Factors VI and VIII — Processes and Concurrency

*"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service, typically a database"* [source: twelve-factor-vi-processes-2026-08-31].

This is the assumption underneath Deployments. A Deployment can replace any Pod with any other Pod because the methodology's constraint holds: no Pod is carrying anything the next one will need. Scale out by adding processes, which is factor VIII, and any process can serve any request.

The methodology bans one thing by name here: *"Sticky sessions are a violation of twelve-factor and should never be used or relied upon"* [source: twelve-factor-vi-processes-2026-08-31].

And when the constraint genuinely does not hold, when the replicas are *not* interchangeable, Kubernetes has a different object for you. It is a different object precisely because it is stepping outside this factor *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*.

### Factor IX — Disposability

Chapter 5 taught you `terminationGracePeriodSeconds` and the SIGTERM-then-SIGKILL sequence, and told you the word was coming. Here it is.

*"The twelve-factor app's processes are disposable, meaning they can be started or stopped at a moment's notice"* [source: twelve-factor-ix-disposability-2026-08-31]. The two halves are startup and shutdown. On startup: *"Processes should strive to minimize startup time. Ideally, a process takes a few seconds from the time the launch command is executed until the process is up and ready to receive requests or jobs."* On shutdown: *"Processes shut down gracefully when they receive a SIGTERM signal from the process manager"* [source: twelve-factor-ix-disposability-2026-08-31].

And a third clause, which is the one that matters most on a real cluster: *"Processes should also be robust against sudden death, in the case of a failure in the underlying hardware"* [source: twelve-factor-ix-disposability-2026-08-31]. Graceful shutdown is a courtesy the platform extends when it can. A node that loses power extends nothing.

> 🪢 **Mnemonic:** Disposability has two speeds and a floor. **Fast up** (seconds, not minutes). **Clean down** (handle SIGTERM). **Survive the floor dropping** (be correct even when neither happens).

### Factor XI — Logs

*"Logs are the stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services"* [source: twelve-factor-xi-logs-2026-08-31].

The rule is that the application does not participate in log management at all: *"A twelve-factor app never concerns itself with routing or storage of its output stream. Each running process writes its event stream, unbuffered, to stdout"* [source: twelve-factor-xi-logs-2026-08-31]. The execution environment captures the stream, collates it with every other stream from the app, and routes it onward [source: twelve-factor-xi-logs-2026-08-31].

That is exactly why `kubectl logs` works on every container without any container being configured for it, and it is why cluster-wide log collection can be a node-level concern rather than an application concern *[cross-bearing: see Ch 18 §6 — lines from everywhere]*.

> ★ **Fixed Point**
>
> **The twelve-factor app is a set of constraints an application accepts in exchange for being run by a platform. Kubernetes implements the platform side — config injection, stateless replication, graceful termination, log collection. It cannot implement the application side. An application that writes its own log files, keeps session state in memory, or takes ninety seconds to start is not made twelve-factor by being containerized.**

Twelve-factor is also a predecessor of vocabulary you will meet later. When Chapter 17 lists the characteristics of cloud native systems, several of them are these factors under newer names *[cross-bearing: see Ch 17 §3 — small pieces, replaced whole]*.

---

## 🔵 §2 — Ways to Replace What's Running

Chapter 6 taught you the mechanics of replacing a running fleet: `RollingUpdate` and `Recreate`, `maxSurge` and `maxUnavailable`, pause and resume *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*. This section does not restate any of it. What it adds is the vocabulary: the names practitioners use for release patterns, the trade-off each one makes, and one line that readers persistently get wrong.

The line is this.

> ★ **Fixed Point**
>
> **`RollingUpdate` and `Recreate` are values of a field on a Deployment. Blue/green and canary are patterns that require tooling above the Deployment object. A Deployment cannot express either one on its own.**

Chapter 6 named the second group and deferred them. They arrive now.

### The umbrella: progressive delivery

The term that covers the whole family is **progressive delivery**: *"the process of releasing updates of a product in a controlled and gradual manner, thereby reducing the risk of the release, typically coupling automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23].

Note the two halves of that definition. *Gradual* is the visible part. *Metric analysis driving automated promotion or rollback* is the part that makes it more than a slow deploy: the release watches itself.

### The four, and what each costs

**Recreate.** *"A Recreate deployment deletes the old version of the application before bringing up the new version. As a result, this ensures that two versions of the application never run at the same time, but there is downtime during the deployment"* [source: argo-rollouts-strategies-2026-08-23].

The trade is stated in the definition: you accept downtime and you get the guarantee that two versions never coexist. That guarantee is not a consolation prize. If the new version runs a schema migration the old version cannot read, coexistence is the failure mode, and Recreate is the correct choice rather than the lazy one.

**RollingUpdate.** *"A RollingUpdate slowly replaces the old version with the new version. As the new version comes up, the old version is scaled down in order to maintain the overall count of the application. This is the default strategy of the Deployment object"* [source: argo-rollouts-strategies-2026-08-23].

No downtime, and the exact inverse guarantee: both versions serve traffic simultaneously, for the duration. Your application must tolerate that.

**Blue/green.** Two complete environments. CNCF's glossary describes the operator maintaining two environments, "blue" and "green," with one serving live production traffic while the other is updated; after testing on the inactive environment, traffic switches via load balancer [source: cncf-glossary-blue-green-deployment-2026-08-31]. Argo's description agrees and adds the reason: *"During this time, only the old version of the application will receive production traffic. This allows the developers to run tests against the new version before switching the live traffic to the new version"* [source: argo-rollouts-strategies-2026-08-23].

The cost is capacity. You run two full copies. What you buy is the ability to test the new version *in production, with production configuration and production backing services*, before a single user reaches it. The cutover is one moment rather than a gradual mix, which means the rollback is also one moment.

CNCF's glossary adds an assessment worth reading, because it is more critical than most vendor material: blue/green *"is an appropriate strategy for non-cloud native software that needs to be updated with minimal downtime. However, its use is normally a 'smell' that legacy software needs to be re-engineered so that components can be updated individually"* [source: cncf-glossary-blue-green-deployment-2026-08-31]. The glossary notes the term is typically applied to whole systems with multiple services updated in lockstep, and is sometimes misapplied to individual services [source: cncf-glossary-blue-green-deployment-2026-08-31].

**Canary.** *"A Canary deployment exposes a subset of users to the new version of the application while serving the rest of the traffic to the old version. Once the new version is verified to be correct, the new version can gradually replace the old version"* [source: argo-rollouts-strategies-2026-08-23]. Argo Rollouts states the same idea from the operator's side: *"a canary rollout is a deployment strategy where the operator releases a new version of their application to a small percentage of the production traffic"* [source: argo-rollouts-canary-2026-08-31].

CNCF's glossary is blunt about why anyone bothers: *"No matter how thorough the testing strategy, there are always some bugs discovered in production. Shifting 100% of traffic from one version of an app to another can lead to more impactful failures"* [source: cncf-glossary-canary-deployment-2026-08-31].

The cost is infrastructure. Canary needs something that can split traffic by proportion, and something that can judge whether the small proportion is going well. Argo's comparison states this directly: canary strategies *"offer greater flexibility but demand more infrastructure (traffic-splitting via a service mesh or ingress controller) and metric analysis; Blue/Green needs no traffic provider and suits workloads such as queue workers"* [source: argo-rollouts-strategies-2026-08-23].

That last clause is the practical answer to "which one." A queue worker has no inbound traffic to split. Canary is not a better blue/green; it is a different tool that needs a request path to work on *[cross-bearing: see Ch 10 §3 — the object is not the implementation]* *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*.

<!-- FIGURE: ch15-fig02-deployment-strategies-compared -->
```
  ┌─ FIELDS ON A DEPLOYMENT ──────────────────────────────────────┐
  │                                                               │
  │  Recreate            RollingUpdate                            │
  │  old ████░░░░░░      old ████▓▓▒▒░░░░                          │
  │  new ░░░░░░████      new ░░░░▒▒▓▓████                          │
  │      └gap┘                                                    │
  │  downtime; never     no downtime; both                        │
  │  two versions        versions live at once                    │
  │  needs: nothing      needs: nothing                           │
  └───────────────────────────────────────────────────────────────┘

  ┌─ PATTERNS NEEDING TOOLING ABOVE IT ───────────────────────────┐
  │                                                               │
  │  Blue/Green          Canary                                   │
  │  blue  ████████│░░   old ████████▓▓▓▓░░░░                      │
  │  green ░░░░░░░░│██   new ░░░░▒▒▒▒▓▓▓▓████                      │
  │            switch          5% → 25% → 50% → 100%              │
  │  test before any     small slice meets it                     │
  │  user arrives        first; metrics decide                    │
  │  needs: 2x capacity  needs: traffic splitting                 │
  │                             + metric analysis                 │
  └───────────────────────────────────────────────────────────────┘

  █ = new version serving   ░ = old version serving / absent
```

**Figure 15.2 — Four ways to replace what's running.** The two enclosures carry the point: the top pair are values you set on a Deployment, and the bottom pair are patterns something else has to implement for you. The footer rows are the actual decision criteria — what each strategy demands before you can use it at all.

> ⚓ **Worth Securing:** People choose blue/green over canary far more often for infrastructure reasons than for risk reasons. If there is no service mesh and no metrics pipeline wired to the release, canary is not on the menu regardless of how much you'd prefer it. Knowing *why* a team runs blue/green tells you more about their platform than about their risk appetite.

### One term this book will not teach you

You may have heard **A/B testing** listed alongside these four. This book leaves it out deliberately, and the reason is a real distinction rather than an omission.

A/B testing appears in Argo's documentation not as a rollout strategy but as a use of a separate resource: *"A user can use experiments to enable A/B/C testing by launching multiple experiments with a different version of their application for a long duration"* [source: argo-rollouts-experiments-2026-08-31]. It is product experimentation. You are measuring which version users prefer, over a long duration, on purpose. The four strategies above are release mechanics: you are measuring whether the new version is *broken*, for as short a duration as you can manage. Delivery tooling can implement both, which is why they end up in the same lists, but they answer different questions.

Nothing in this chapter's questions turns on A/B testing.

> 🔭 **Closer Look:** One vocabulary note, for readers with a good memory. Chapter 6 called these "release strategies" *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*. This book's headword is **deployment strategy**, and the reason is crowding: "release" already carries two other meanings here, a Kubernetes minor version and a Helm release *[cross-bearing: see Ch 14 §3 — chart, release, revision]*. Three senses of one word across two adjacent chapters is one too many. Both phrases name the same thing; if you meet "release strategy" in the field, it is this.

---

## ☆ Taking Your Bearings 1: The Application, and the Shapes of a Release

Six questions. Two of them reach back to earlier chapters. Those are marked, and they are marked because they are the point.

**1.** An application stores uploaded files on the local filesystem of whichever Pod handled the upload. Which twelve-factor factor does this violate, and what does it break in Kubernetes specifically?

**2.** A team stores its production database password in a file called `config/production.yml`, committed to the application repository, and reads it at startup. Apply the twelve-factor litmus test. What does it say?

**3.** [retrieval: ch4] Your application needs a different API endpoint URL in staging than in production, and the same container image must run in both. Name two Kubernetes mechanisms that deliver that URL to the running container, and say where the value physically lives in each case.

**4.** [retrieval: ch6] During a `RollingUpdate` on a Deployment with 10 replicas, `maxSurge: 2` and `maxUnavailable: 1`. What is the maximum number of Pods that may exist at any moment during the update, and the minimum number that may be available?

**5.** A team wants to release a new version to 5% of users, watch error rates for twenty minutes, and automatically abort if errors rise. Their workload is an HTTP API behind an Ingress. Which strategy is this, and what must already exist in the cluster for it to be possible?

**6.** Which of these is a value you can set on a Deployment's `.spec.strategy`, and which requires additional tooling: `Recreate`, blue/green, `RollingUpdate`, canary?

---

<details>
<summary>Answers with explanations</summary>

**1. Factor VI (Processes — stateless and share-nothing).** The twelve-factor rule is that *"any data that needs to persist must be stored in a stateful backing service"* [source: twelve-factor-vi-processes-2026-08-31]. What it breaks in Kubernetes: a Deployment replaces any Pod with any other Pod, and a request that retrieves the file may land on a replica that never had it. Worse, the Pod's writable layer is destroyed when the Pod is, so the data is not merely misplaced. It is gone at the next rollout, node drain, or eviction.

**Why not "factor IX, disposability"?** Tempting, and adjacent. A Pod holding unique data is certainly not disposable. But IX is about *startup and shutdown behavior*; the root violation is holding state at all, which is VI.

**2. It fails.** The test is whether *"the codebase could be made open source at any moment, without compromising any credentials"* [source: twelve-factor-iii-config-2026-08-31]. Publishing this repository publishes the production database password. The methodology anticipates exactly this: a config file is better than a hard-coded constant, but *"it's easy to mistakenly check in a config file to the repo"* [source: twelve-factor-iii-config-2026-08-31] — and here it wasn't even a mistake, it was the design.

**3. [retrieval: ch4] ConfigMap and Secret.** Either can be surfaced to the container as environment variables or mounted as files. Where the value lives: in the cluster, as an object in etcd, entirely outside the image. The image is identical in both environments; the object differs. That separation is what allows one tested artifact to run everywhere *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*.

**Common wrong answer:** "build two images with different baked-in values." This is the failure factor III exists to name. You are now shipping an artifact you did not test, because the thing you tested was the other image.

**4. Maximum 12 Pods; minimum 9 available.** `maxSurge: 2` permits two Pods above the desired count of 10. `maxUnavailable: 1` permits one below it. The two are independent caps, not a single budget: the controller may be simultaneously two over and one unavailable, which is what makes the update proceed at all *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*.

**Why "11 and 10" is wrong:** that reads `maxSurge` and `maxUnavailable` as if only one could be in effect. Both apply throughout.

**5. Canary.** The tell is the *proportion* of traffic plus *automated abort on a metric*. That is progressive delivery's definition, *"coupling automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23].

What must already exist: something that can split traffic by weight, a service mesh or an ingress controller, and a metrics system the release logic can query [source: argo-rollouts-strategies-2026-08-23]. Without traffic splitting there is no way to send 5% anywhere; without metrics there is nothing to abort on.

**6. `Recreate` and `RollingUpdate` are Deployment strategy values. Blue/green and canary require tooling above the Deployment.** This is the section's Fixed Point and the distinction most likely to be tested from this material. `RollingUpdate` *"is the default strategy of the Deployment object"* [source: argo-rollouts-strategies-2026-08-23]; the other two are patterns implemented by controllers that manage Deployments or replace them.

---

**If you got 5–6:** You have the application layer. §3 changes subject entirely: it stops asking what to deploy and starts asking who does it.

**If you got 3–4:** Solid. Re-read the answer to whichever you missed; the reasoning matters more than the fact.

**If you got 0–2:** Re-read **§1's factor III** and **§2's Fixed Point** before continuing. Those two ideas get used again in §3 and §4 without reintroduction.

</details>

---

## 🔵 §3 — Push, or Pull

This is the chapter's central argument, and it begins with a fact that clears the ground.

Kubernetes *"does not deploy source code and does not build your application. Continuous Integration, Delivery, and Deployment (CI/CD) workflows are determined by organization cultures and preferences as well as technical requirements"* [source: k8s-docs-overview-2026-08-23].

That is the documentation's own list of what Kubernetes is not, and it settles something. The cluster is indifferent to who builds your artifact and how. It receives objects through its API and reconciles them. Everything before that — compiling, testing, packaging, tagging — happens elsewhere, by arrangement. Chapter 4 told you this in passing *[cross-bearing: see Ch 4 §1 — you file a declaration]*; here it becomes load-bearing.

### The three letters, expanded

The abbreviation bundles three practices that are worth separating, since the exam-relevant distinctions live in the gaps between them.

**CI — continuous integration.** *"The practice of integrating code changes as regularly as possible"* [source: cncf-glossary-continuous-integration-2026-08-31]. In practice this means a server that checks every commit merges cleanly, runs quality checks and tests, and, as CNCF puts it, *"allows software teams to turn every code commit into either a concrete failure or a viable release candidate"* [source: cncf-glossary-continuous-integration-2026-08-31].

**CD — continuous delivery.** *"A set of practices in which code changes are automatically deployed into an acceptance environment (or, in the case of continuous deployment, into production)"* [source: cncf-glossary-continuous-delivery-2026-08-31]. It includes procedures ensuring software is adequately tested before deployment, and a way to roll changes back if needed [source: cncf-glossary-continuous-delivery-2026-08-31].

**CD — continuous deployment.** *"Goes a step further than continuous delivery by deploying finished software directly to production"* [source: cncf-glossary-continuous-deployment-2026-08-31].

> 🪝 **Snag:** CNCF abbreviates *both* continuous delivery and continuous deployment as "CD" [source: cncf-glossary-continuous-delivery-2026-08-31] [source: cncf-glossary-continuous-deployment-2026-08-31]. This is genuinely ambiguous in the field, not just on paper. When the distinction matters, and it matters when the question is whether a human approves the production step, spell the word out.

### The architectural question

Now the question this section exists for. An artifact has been built. Something must apply it to a cluster. There are two arrangements, and they differ in a way that is not a matter of taste.

**Push.** A pipeline runs outside the cluster. It holds credentials *to the cluster*. When it finishes building, it reaches inward across the cluster boundary and applies the manifests. This is what most teams do first, because it is the obvious extension of a build pipeline: the pipeline already has the artifact, so give it the ability to install the artifact.

**Pull.** An agent runs *inside* the cluster. It holds credentials *to a repository*. It reaches outward, fetches the desired state, and applies it locally. Nothing outside the cluster holds cluster credentials, because nothing outside the cluster needs them.

<!-- FIGURE: ch15-fig03-cicd-push-vs-gitops-pull -->
```
  PUSH
                    ┌ ─ ─ ─ cluster boundary ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
   ┌──────────┐     │                                          │
   │ pipeline │──── │ ────────────────►  API server            │
   │   🔑     │     │                                          │
   └──────────┘     │                                          │
    ▲               └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘
    │
   the key lives OUT HERE


  PULL
                    ┌ ─ ─ ─ cluster boundary ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
   ┌──────────┐     │  ┌─────────┐                             │
   │   repo   │◄─── │ ─│  agent  │────────►  API server        │
   │          │     │  │   🔑    │                             │
   └──────────┘     │  └─────────┘                             │
                    │       ▲                                  │
                    └ ─ ─ ─ │ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
                    the key lives IN HERE
```

**Figure 15.3 — Push and pull, mirrored.** The cluster boundary is the same line in both panels and the arrow is the only thing that reverses. Watch the key: in push it sits outside the boundary, in a system the cluster does not control. In pull it sits inside, in a Pod the cluster does control. Everything else in this section is a consequence of that one difference.

Four consequences follow, and none of them is subtle once you look.

**Where the credentials sit.** In push, a set of cluster-write credentials lives in your CI system: in its secret store, readable by its jobs, and often by anyone who can edit a pipeline definition. In pull, they live in a Kubernetes Secret in the cluster they apply to *[cross-bearing: see Ch 12 §4 — secrets are not encrypted]*.

**What a compromise gets.** This is the sharper version of the same point. Compromise a push pipeline and you have write access to every cluster it deploys to, which for a shared CI system may be all of them. Compromise a pull agent and you have one cluster, the one you were already inside. The term for this is **blast radius**: how far the damage from a single compromise reaches. Pull does not prevent compromise. It bounds it.

**What happens between deploys.** In push, nothing. The pipeline runs, exits, and the cluster is on its own until the next commit. In pull, the agent is still running. It is still comparing. This is the difference that turns out to matter most, and §4 is about what an agent does with the comparison.

**What "the truth" means.** In push, the authoritative answer to "what is supposed to be running" is whatever the last pipeline applied, a fact you must reconstruct from build logs. In pull, it is a file, in a repository, that anyone can read, with a history showing every previous answer.

> **Logbook Entry:** There is a version of this story on every platform team.
>
> The incident is small. A service is misbehaving on Friday afternoon, somebody with cluster access finds the cause, and fixes it directly: one field, one `kubectl edit`, thirty seconds. The service recovers. It is genuinely the right call in the moment; the alternative is a code review at 6pm.
>
> The fix is correct and it is also invisible. It exists nowhere except in the cluster's own state. Nobody writes it down, because writing it down was the slow path they were avoiding.
>
> Six weeks later somebody deploys a routine change to the same service. The deployment applies the manifests from the repository, which have never known about the Friday fix. The field reverts. The original problem returns, now with six weeks of distance between cause and effect, and a change log pointing at an unrelated commit.
>
> Push-based delivery has no mechanism that would have caught this. The pipeline was not running for those six weeks and had nothing to compare against if it had been. The gap between what the repository said and what the cluster contained was real, persistent, and completely silent.
>
> Keep this story in mind through §4. The mechanism that catches it has a name, and it is not an alarm.

### GitOps

**GitOps** is the name for the pull arrangement done rigorously. The definition is not a vendor's; it comes from OpenGitOps, a CNCF project, and it is four principles rather than a description of tooling.

*"GitOps is a set of principles for operating and managing software systems."* The desired state of a GitOps-managed system must be:

1. **Declarative** — *"A system managed by GitOps must have its desired state expressed declaratively."*
2. **Versioned and Immutable** — *"Desired state is stored in a way that enforces immutability, versioning and retains a complete version history."*
3. **Pulled Automatically** — *"Software agents automatically pull the desired state declarations from the source."*
4. **Continuously Reconciled** — *"Software agents continuously observe actual system state and attempt to apply the desired state."*

[source: opengitops-principles-v1-2026-08-31]

<!-- FIGURE: ch15-fig05-opengitops-four-principles -->
```
  ┌────────────────────────────┐  ┌────────────────────────────┐
  │ 1  DECLARATIVE             │  │ 2  VERSIONED & IMMUTABLE   │
  │                            │  │                            │
  │ desired state expressed    │  │ stored so as to enforce    │
  │ declaratively              │  │ immutability, versioning,  │
  │                            │  │ complete history           │
  │      ◄ you know this:      │  │      ◄ NEW HERE            │
  │        Ch 4 §1             │  │                            │
  └────────────────────────────┘  └────────────────────────────┘

  ┌────────────────────────────┐  ┌────────────────────────────┐
  │ 3  PULLED AUTOMATICALLY    │  │ 4  CONTINUOUSLY RECONCILED │
  │                            │  │                            │
  │ agents automatically pull  │  │ agents continuously observe │
  │ desired state from source  │  │ actual state and apply     │
  │                            │  │ desired state              │
  │      ◄ you know this:      │  │      ◄ you know this:      │
  │        Ch 3 §5             │  │        Ch 3 §6             │
  └────────────────────────────┘  └────────────────────────────┘
```

**Figure 15.4 — The four principles, and where you already met three of them.** The markers in each block are the figure's real content. Only principle 2 is new to you. The rest is Chapter 4's declarative model and Chapter 3's watch-and-reconcile architecture, restated with the desired state living somewhere else. Hold that thought; §7 collects on it.

Two of the four carry the weight, and both are places readers go wrong.

**Principle 3 is why push-based CD is not GitOps.** The word is *pulled*. Agents fetch the declarations; nothing hands the declarations to them. OpenGitOps states it as an active property of the agent: *"Software agents automatically pull the desired state declarations from the source"* [source: opengitops-1-0-announcement-2026-08-31]. A pipeline that stores manifests in Git and then pushes them into a cluster satisfies principles 1 and 2 and fails 3 and 4 completely. It is a perfectly reasonable thing to build. It is not GitOps, and calling it GitOps loses the distinction that the term exists to make.

The project is unusually explicit that this precision was deliberate: *"The wording of each principle and linked glossary item was very carefully chosen"* [source: opengitops-1-0-announcement-2026-08-31].

**Principle 4 is why GitOps is not a deploy-time event.** *Continuously* observe. Not "observe at deploy time," not "observe when triggered." The agent is described as having an ongoing obligation: *"The GitOps software agents have to be aware of the actual state of a system under management and attempt to apply the desired state"* [source: opengitops-1-0-announcement-2026-08-31].

OpenGitOps names the thing this catches. **Drift** is *"when a system's actual state has moved or is in the process of moving away from the desired state"* [source: opengitops-glossary-2026-08-31]. **Reconciliation** is *"the process of ensuring the actual state of a system matches its desired state"* [source: opengitops-glossary-2026-08-31].

CNCF's own glossary entry for GitOps names drift first among the problems the practice addresses, alongside failed deployments, inconsistent environments, and difficulty tracking historical changes, and adds the observation that *"configuration drift can be hard to detect and resolve without a source of truth governing it"* [source: cncf-glossary-gitops-2026-08-31].

> 🔭 **Closer Look:** "GitOps" names Git, but the principles do not require it. OpenGitOps says so: *"many version control systems can be used in GitOps as long as they meet those two basic requirements and teams use them in a conformant manner"* [source: opengitops-1-0-announcement-2026-08-31], the requirements being principle 2's immutability and complete version history. Git is the overwhelming practical choice. The definition is about the properties, not the tool.

### One thing GitOps does not do

Before §4 makes this concrete, kill a misreading that the phrase "the repository is the source of truth" invites.

> ⚠ **Navigational Hazards**
>
> A GitOps agent does **not** write to the cluster's datastore directly, and does not bypass the API server.
>
> Chapter 3 made a claim about this architecture that has held for twelve chapters: the API server is the only thing that mutates cluster state, and every actor — kubectl, the scheduler, every controller — goes through it *[cross-bearing: see Ch 3 §5 — the only door in]*. A delivery agent is an API client like any other. Its requests pass through authentication, then authorization, then admission, in that order, exactly as yours do *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*.
>
> **Where this goes wrong:** readers hear "the repository is the source of truth" and picture the repository *replacing* etcd, as though desired state now lives in Git instead of in the cluster. It does not. etcd still holds every object. What Git holds is the *authored* desired state, upstream of the cluster, and the agent's job is to keep the two in agreement by making ordinary API calls.
>
> The consequence you can act on: an agent that lacks RBAC permission to create a resource will fail to create it, with an ordinary authorization error. GitOps grants no exemption from any cluster control. If anything it is *more* constrained than a human operator, because its permissions are written down.

Which raises the question §4 opens with: what is this agent, exactly?

---

## 🔵 §4 — An Agent That Watches a Repository

**Argo CD** is a *"declarative, GitOps continuous delivery tool for Kubernetes"* [source: argocd-overview-2026-08-23]. You have met the name once already, in Chapter 3, where it appeared as a promise about a sentence this chapter would retrieve *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*.

Here is that sentence, and it is the most important one in the section.

The Argo CD application controller *"is a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the repo)"* [source: argocd-architecture-2026-08-31].

Read it as three separate claims:

- *is a Kubernetes controller* — the thing Chapter 3 §6 defined
- *continuously monitors and compares current against desired* — the thing Chapter 3 §6 said controllers do
- *desired target state as specified in the repo* — the only part that is new

Chapter 6 told you that anyone can write a controller acting on custom resources *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. Somebody did. This is what it looks like.

> ★ **Fixed Point**
>
> **A GitOps delivery agent is a controller. Its desired state lives in a repository instead of in etcd. Nothing else about the architecture is different — not the API server's position, not the watch-based coordination, not the shape of the loop.**

### The object model

Argo CD's own glossary defines the pieces, and the vocabulary is worth getting exactly right because the words are ordinary English used precisely.

**Application** — *"A group of Kubernetes resources as defined by a manifest. This is a Custom Resource Definition (CRD)"* [source: argocd-core-concepts-2026-08-31]. More precisely: *"The Application CRD is the Kubernetes resource object representing a deployed application instance in an environment"* [source: argocd-declarative-setup-2026-08-31].

An `Application` is defined by two pieces of information: a *"source reference to the desired state in Git (repository, revision, path, environment)"* and a *"destination reference to the target cluster and namespace"* [source: argocd-declarative-setup-2026-08-31]. That is the whole contract: *this content, from there, goes there*.

**Target state** — *"The desired state of an application, as represented by files in a Git repository."*
**Live state** — *"The live state of that application. What pods etc are deployed."*
**Sync status** — *"Whether or not the live state matches the target state. Is the deployed application the same as Git says it should be?"*
**Sync** — *"The process of making an application move to its target state. E.g. by applying changes to a Kubernetes cluster."*
**Refresh** — *"Compare the latest code in Git with the live state. Figure out what is different."*

[source: argocd-core-concepts-2026-08-31]

Notice that refresh and sync are separate words. Refresh compares. Sync acts. A system can know it is out of agreement without doing anything about it, and whether it acts is a policy decision, which is §4's second half.

> ⚓ **Worth Securing:** If you find yourself confusing *live state* and *target state* under pressure, anchor them to Chapter 4. **Target state is `spec`, kept outside the cluster. Live state is what `status` reports.** Argo CD's central comparison is the one you have been reading since Chapter 4, with one operand relocated *[cross-bearing: see Ch 4 §2 — the anatomy of a record]*.

### Where the manifests come from

An `Application`'s source is a repository path, but the content at that path need not be plain YAML. Argo CD accepts manifests specified *"in several ways: kustomize applications; helm charts; jsonnet files; plain directory of YAML/json manifests; any custom config management tool configured as a config management plugin"* [source: argocd-overview-2026-08-23].

Argo CD's glossary has a word for this choice: the **application source type** is *"which Tool is used to build the application,"* where a **tool** is *"a tool to create manifests from a directory of files. E.g. Kustomize"*, and a **configuration management plugin** is simply *"a custom tool"* [source: argocd-core-concepts-2026-08-31].

This is where the previous chapter's work gets collected. A Helm chart is a manifest source for a GitOps agent *[cross-bearing: see Ch 14 §2 — what a chart contains]*. So is a Kustomize overlay *[cross-bearing: see Ch 14 §5 — patching instead of templating]*. Chapter 14 gave you packaging; this chapter gives packaging somewhere to go. The agent renders the chart or builds the overlay, and compares the *result* against the cluster.

> 🪝 **Snag:** "Argo CD only deploys plain YAML" is a common and confident mistake, and it usually comes from having seen one tutorial. The tool's whole design assumes a rendering step: a dedicated component, the repository server, *"maintains a local cache of the Git repository holding the application manifests"* and is responsible for *"generating and returning the Kubernetes manifests"* given a repository URL, a revision, a path, and template-specific configuration [source: argocd-architecture-2026-08-31]. Rendering is not an add-on. It is a whole component.

### What it tracks

An `Application` names a revision as well as a repository, and there are three kinds of thing that revision can be. Argo CD's tracking documentation is precise about the difference, and the difference is about stability.

A **branch or symbolic reference** (including `HEAD`): *"Argo CD will continually compare live state against the resource manifests defined at the tip of the specified branch or the resolved commit of the symbolic reference"* [source: argocd-tracking-strategies-2026-08-31]. The tip moves; so does your target.

A **tag**: *"If a tag is specified, the manifests at the specified Git tag will be used to perform the sync comparison."* Tags are *"generally considered more stable, and less frequently updated"* than branches [source: argocd-tracking-strategies-2026-08-31].

A **pinned commit**: *"If a Git commit SHA is specified, the app is effectively pinned to the manifests defined at the specified commit."* And the consequence: *"Since commit SHAs cannot change meaning, the only way to change the live state of an app which is pinned to a commit, is by updating the tracking revision in the application to a different commit containing the new manifests"* [source: argocd-tracking-strategies-2026-08-31].

That last sentence is principle 2, versioned and immutable, showing up as an operational property rather than an abstraction. Argo CD's own best-practices documentation makes the same argument against tracking an unstable revision: *"Since this is not a stable target, the manifests for this kustomize application can suddenly change meaning, even without any changes to your own Git repository. A better version would be to use a Git tag or commit SHA"* [source: argocd-best-practices-2026-08-31].

> 🪢 **Mnemonic:** **Branch moves. Tag rarely moves. Commit never moves.** Pick according to how much you want the ground under your production cluster to shift without a commit of your own.

### Synced, and OutOfSync

Now the section's second Fixed Point, and the one most likely to be tested from this material.

*"A deployed application whose live state deviates from the target state is considered OutOfSync"* [source: argocd-overview-2026-08-23]. Argo CD *"reports and visualizes the differences, while providing facilities to automatically or manually sync the live state back to the desired target state"* [source: argocd-overview-2026-08-23].

> ★ **Fixed Point**
>
> **`OutOfSync` means live state deviates from the target state in Git. It is a drift signal, not an error. Nothing has necessarily failed. A person editing an object by hand produces an `OutOfSync` application, and so does a commit that has not been applied yet.**

Argo CD's glossary keeps these on separate lines for exactly this reason. **Sync status** answers *"is the deployed application the same as Git says it should be?"* A separate item, **sync operation status**, answers *"whether or not a sync succeeded"* [source: argocd-core-concepts-2026-08-31]. Two questions. Two answers. A sync can succeed and leave the application `OutOfSync`; the documentation says so outright: *"It is possible for an application to be `OutOfSync` even immediately after a successful Sync operation"* [source: argocd-diffing-outofsync-2026-08-31].

<!-- AUTHOR-REVIEW: argocd-diffing-outofsync-2026-08-31 quotes the claim but its own capture note says the page's enumerated causes (unknown fields, pruning disabled, mutating controllers/webhooks, Helm template functions, HPA metric reordering) were returned as summary rather than quotation and must not be attributed to that snapshot. The claim above is therefore stated without its causes, which weakens it. A fetch of the full diffing page would let §4 name at least one concrete cause. -->

Return to the Logbook Entry in §3. Friday afternoon, one field, thirty seconds, invisible for six weeks. Under a GitOps agent, that edit produces an `OutOfSync` status within one reconciliation interval. Not an alert, not a page, not a failure. A status field, changed, saying *these two things no longer agree*. The mechanism that catches the story is not an alarm. It is a comparison that never stops running.

<!-- FIGURE: ch15-fig04-argocd-sync-states-and-hooks -->
```
      TARGET STATE                 AGENT                LIVE STATE
      (Git repository)          (controller)             (cluster)

    ┌───────────────┐         ┌────────────┐         ┌───────────────┐
    │ deployment.yml│────────►│            │◄────────│ Deployment    │
    │  replicas: 3  │         │  compare   │         │  replicas: 3  │
    └───────────────┘         │            │         └───────────────┘
                              └─────┬──────┘
                                    │
                                 Synced
                            the two agree

    ┌───────────────┐         ┌────────────┐         ┌───────────────┐
    │ deployment.yml│────────►│            │◄────────│ Deployment    │
    │  replicas: 3  │         │  compare   │         │  replicas: 5  │
    └───────────────┘         │            │         └───────────────┘
                              └─────┬──────┘              ▲
                                    │                     │
                              OutOfSync            someone ran
                        the two do not agree     kubectl scale
                                    │              on Friday
                                    │
                                    ▼
                            ┌──────────────┐
                            │     SYNC     │  apply target state
                            │  (operation) │  → live matches again
                            └──────────────┘
```

**Figure 15.5 — The comparison, and the two answers it produces.** The lower panel shows the cause readers do not expect: nothing failed, no deploy went wrong, a person changed the cluster. `OutOfSync` reports the disagreement. Sync is the separate operation that closes it.

### Doing something about it

Reporting a difference and correcting it are separate decisions, and Argo CD keeps them separate.

*"Argo CD has the ability to automatically sync an application when it detects differences between the desired manifests in Git, and the live state in the cluster"* [source: argocd-auto-sync-policy-2026-08-31]. That ability is configured declaratively, which is itself in keeping, since the agent's own behavior is a field on an object in the repository.

Beyond automated sync sit two related behaviors, both named in the feature list: **automated configuration drift detection and visualization**, and **automated or manual syncing of applications to its desired state** [source: argocd-overview-2026-08-23]. **Self-heal** is the term for the agent correcting drift it detects in the cluster rather than only responding to new commits.

<!-- AUTHOR-REVIEW: outline Open Question 8(a) — whether self-heal is enabled by default is not answerable from the cached corpus. argocd-auto-sync-policy-2026-08-31 is truncated at the declarative example and does not state defaults for automated sync, selfHeal, or prune. The text above deliberately describes self-heal's shape without asserting its default state, per house practice. A fetch of the full auto-sync page would resolve it. Do not fill this in from memory — the default is exactly the sort of detail a well-built question turns on. -->

CNCF's glossary lists self-healing among GitOps's characteristic benefits, alongside *"transparency and traceability of changes, reliability and security through declarative states, and rollback, revert"* [source: cncf-glossary-gitops-2026-08-31], which brings us to the third thing in this book to wear a familiar word.

### Rollback, for the third time

Chapter 6 promised you this. When it taught `kubectl rollout undo`, it said the word would appear twice more, and that the second occasion would be a delivery tool *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*. Chapter 14 spent the first *[cross-bearing: see Ch 14 §3 — chart, release, revision]*. This is the second and last.

Argo CD offers *"rollback/roll-anywhere to any application configuration committed in Git repository"* [source: argocd-overview-2026-08-23].

Look at what is actually happening. You do not invoke a rollback subsystem. You change what the repository says, typically with `git revert`, producing a new commit whose content is the old content, and the agent does what it has been doing continuously since it started: it notices the target moved, and it closes the gap. The rollback mechanism *is* the sync mechanism. There is no second code path.

| | What moves | Where the previous state was kept |
|---|---|---|
| `kubectl rollout undo` (Ch 6 §5) | The Deployment's Pod template | In the old ReplicaSet, on the cluster |
| `helm rollback` (Ch 14 §3) | The Helm release to a prior revision | In Helm's release history, on the cluster |
| **Rollback by revert** (here) | A commit in the repository | In the repository's history |

Three mechanisms, one English word. This book writes the third as **rollback by revert**, always in that three-word form, so that it cannot be confused with the other two.

> 🪝 **Snag:** Do not call the thing you revert a "revision." In this book, *revision* has two owners already: a Deployment revision *[cross-bearing: see Ch 6 §5 — every rollout is a revision]* and a Helm release revision *[cross-bearing: see Ch 14 §3 — chart, release, revision]*. A Git revision is a **commit**. Argo CD's own API field happens to be called `revision`, which is why this needs saying rather than assuming.

### The agent's own identity

One thing remains, and two earlier chapters pointed at it explicitly *[cross-bearing: see Ch 5 §6 — a Pod's identity]* *[cross-bearing: see Ch 12 §2 — who you are]*.

A delivery agent is a Pod. A Pod that talks to the API server needs an identity, and in Kubernetes that identity is a ServiceAccount. The Kubernetes documentation lists this among the reasons non-human identities exist at all: *"an external service needs to communicate with the Kubernetes API server (CI/CD pipelines)"* [source: k8s-docs-service-accounts-2026-08-23].

Then ask what this particular Pod does for a living. It creates, updates, and deletes objects — Deployments, Services, ConfigMaps, RBAC objects, custom resources — across many namespaces, on behalf of whatever is committed to a repository. Its grants must be broad, because "apply whatever the repository says" is a broad job description.

Argo CD's security documentation states the default plainly: *"By default, Argo CD uses a clusteradmin level role in order to: 1. watch & operate on cluster state 2. deploy resources to the cluster"* [source: argocd-security-cluster-credentials-2026-08-31].

The same documentation immediately supplies the reduction: *"Although Argo CD requires cluster-wide read privileges to resources in the managed cluster to function properly, it does not necessarily need full write privileges to the cluster."* Operators may edit the ClusterRole of `argocd-manager-role` *"such that write privileges are limited to only the namespaces and resources that you wish Argo CD to manage"* [source: argocd-security-cluster-credentials-2026-08-31].

Note the asymmetry, because it is the interesting part: cluster-wide **read** is structural, since the agent cannot detect drift in something it cannot see, while broad **write** is a default, not a requirement.

For clusters other than the one it runs in, the credentials are ordinary Kubernetes objects: *"To manage external clusters, Argo CD stores the credentials of the external cluster as a Kubernetes Secret in the argocd namespace,"* comprising *"the K8s API bearer token associated with the `argocd-manager` ServiceAccount created during `argocd cluster add`, along with connection options to that API server"* [source: argocd-security-cluster-credentials-2026-08-31].

> ⚠ **Navigational Hazards**
>
> A delivery agent is not exempt infrastructure. It is a Pod with a ServiceAccount and, by default, cluster-admin-equivalent grants, which makes it one of the highest-value subjects in the entire cluster *[cross-bearing: see Ch 12 §3 — what you may do]*.
>
> **Where people get confused:** the reasoning goes "GitOps is more secure than push, therefore the agent is a security improvement, therefore I do not need to think about it." The first clause is defensible on blast-radius grounds. The conclusion does not follow. Pull moves the credentials *inside* the cluster; it does not make them smaller. Anyone who can commit to the tracked repository can, transitively, do whatever the agent may do.
>
> Which means: in a mature GitOps setup, the repository's branch-protection rules *are* an access-control mechanism, and they are exactly as load-bearing as your RBAC policy. That is not a metaphor. Commit access to the tracked branch is cluster access, mediated by an agent that will faithfully apply whatever it finds.

Two structural points before moving on, both of which discharge promises.

First: Argo CD's `Application` is a custom resource, and installing its CRD extends the API so that `Application` objects can *exist*. Whether anything *happens* to them depends entirely on whether the application controller is running, which is the pattern Chapter 10 named, and it has no cleaner instance in this book *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*. An `Application` on a cluster with no Argo CD controller is a stored document. It describes a deployment that will never occur.

Second: this is a controller acting on custom resources, which is precisely the thing Chapter 6 said you could build *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. It is not a new category of technology. It is the category you were taught, aimed somewhere unexpected.

---

## ☆ Taking Your Bearings 2: Push, Pull, and the Agent

Five questions. One reaches back.

**1.** A team stores all manifests in Git. Their CI pipeline, running on a hosted service, builds an image and then runs `kubectl apply -f manifests/` against the production cluster using credentials stored in the CI system's secret store. Which of the four OpenGitOps principles does this satisfy, and which does it fail?

**2.** An Argo CD application shows `OutOfSync`. The most recent sync operation completed successfully. Give two different explanations, only one of which involves anything going wrong.

**3.** Two teams run identical workloads. Team A uses push-based CD from a shared CI system that also deploys to eleven other clusters. Team B runs an in-cluster agent per cluster. An attacker obtains full control of the CI system. Describe the difference in what they can now reach, using the correct term.

**4.** [retrieval: ch12] A delivery agent needs to create Deployments and Services in namespaces it does not own, and delete resources that have been removed from the repository. Name the two kinds of object that must exist before any of that is permitted, and say which one determines the *scope* across namespaces.

**5.** An `Application` tracks the `main` branch. A colleague argues the team should track a Git tag instead. What changes about the system's behavior, and which OpenGitOps principle is the argument appealing to?

---

<details>
<summary>Answers with explanations</summary>

**1. Satisfies 1 (Declarative) and 2 (Versioned and Immutable). Fails 3 (Pulled Automatically) and 4 (Continuously Reconciled).**

Manifests are declarative and stored in Git with history, so the first two hold. Principle 3 requires that *"software agents automatically pull the desired state declarations from the source"* [source: opengitops-principles-v1-2026-08-31]; here the pipeline pushes, from outside. Principle 4 requires agents to *continuously* observe and apply; this pipeline runs once per commit and then exits, leaving nothing observing between runs.

This is a perfectly good delivery system. It is not GitOps. Storing manifests in Git is necessary and nowhere near sufficient, which is exactly the confusion the term is meant to prevent.

**2. Two explanations:**

*Nothing went wrong:* somebody edited a live object directly with `kubectl`. Live state now deviates from target state, so the status is `OutOfSync` [source: argocd-overview-2026-08-23]. The last sync succeeded; it just happened before the edit.

*Something did go wrong:* a new commit landed in the tracked path and has not been applied yet. The target moved; live state has not caught up.

And a third, worth knowing: the documentation states outright that *"it is possible for an application to be `OutOfSync` even immediately after a successful Sync operation"* [source: argocd-diffing-outofsync-2026-08-31]. Sync status and sync-operation status are separate facts about separate questions [source: argocd-core-concepts-2026-08-31].

**Why "the sync failed" is wrong:** that would show in *sync operation status*, which the question tells you succeeded. Reading `OutOfSync` as a failure is the misconception this item targets.

**3. Blast radius.** Compromising Team A's CI system yields write credentials to twelve clusters, because that is what the system holds in order to do its job. Compromising the same system for Team B yields the ability to build and publish images, which is bad and a real supply-chain problem, but not cluster-write credentials, because Team B's clusters hold their own credentials internally and the CI system never had any.

Pull does not prevent the compromise. It bounds what one compromise reaches.

**4. [retrieval: ch12] A ServiceAccount and an RBAC binding (with its Role or ClusterRole). The ClusterRoleBinding determines cross-namespace scope.**

The ServiceAccount is the identity; the binding attaches a permission set to it. Because the work spans namespaces the agent does not own, the grant must be cluster-scoped, a ClusterRole bound by a ClusterRoleBinding, rather than a Role in each namespace *[cross-bearing: see Ch 12 §3 — what you may do]*. Argo CD's own documentation confirms the shape: it uses a `argocd-manager` ServiceAccount, and reduction is done by editing the ClusterRole `argocd-manager-role` [source: argocd-security-cluster-credentials-2026-08-31].

**Why "just a ServiceAccount" is wrong:** a ServiceAccount alone gets almost nothing. Identity without a binding is a name with no permissions attached.

**5. Behavior change: the target stops moving on its own.** With a branch, Argo CD compares against *"the tip of the specified branch"*, which advances with every merge [source: argocd-tracking-strategies-2026-08-31]. With a tag, the target is fixed until someone deliberately moves the tag or changes what the `Application` tracks; tags are *"generally considered more stable, and less frequently updated"* [source: argocd-tracking-strategies-2026-08-31].

**The principle: 2, Versioned and Immutable** — *"Desired state is stored in a way that enforces immutability, versioning and retains a complete version history"* [source: opengitops-principles-v1-2026-08-31]. Argo CD's best-practices page makes exactly this argument, noting that an unstable revision means manifests *"can suddenly change meaning, even without any changes to your own Git repository"* [source: argocd-best-practices-2026-08-31].

---

**If you got 4–5:** You have the chapter's core. What remains is ordering, alternatives, and the synthesis.

**If you got 2–3:** Re-read §3's four principles and §4's `OutOfSync` Fixed Point.

**If you got 0–1:** Go back to **§3** and read it properly before continuing. §5 and §6 assume the push/pull distinction as settled ground.

</details>

---

## 🟡 §5 — Ordering the Sync

This section is marked Advanced, and the marking is honest: it goes somewhat deeper than an associate credential is likely to reach. It is here because the chapter raises a question it would be unsatisfying to leave hanging, and because a promise from Chapter 12 lands precisely on it.

The question is ordering.

Chapter 14 opened by listing what a folder of YAML fails to give you, and one of the four was apply ordering: `kubectl apply -f` over a directory offers no guarantee about which object lands first *[cross-bearing: see Ch 14 §1 — why a folder of YAML stops working]*. Helm's `crds/` directory exists partly to address one instance of this *[cross-bearing: see Ch 14 §6 — which one, when]*.

GitOps does not inherit that fix. It inherits the problem, at a larger scale. An agent reconciling an entire repository against an entire cluster faces the same ordering question about far more objects: a namespace before the things inside it, a CustomResourceDefinition before any custom resource that uses it, a database migration before the version of the application that expects the new schema.

Argo CD's answer has two levels, and the two are independent.

### Phases

A sync runs in phases, and hooks attach to them:

- **PreSync** — hooks run *"prior to the application of the manifests"*
- **Sync** — hooks run *"after all PreSync hooks completed and were successful, at the same time as the application of the manifests"*
- **PostSync** — hooks run *"after all Sync hooks completed and were successful, a successful application, and all resources in a Healthy state"*
- **SyncFail** — hooks run *"when the sync operation fails"*

[source: argocd-sync-phases-and-waves-2026-08-31]

Phase execution is strictly ordered and gated on success. PreSync-marked resources are applied first, and if any fail the process stops. Sync-marked resources are applied next; a failure marks the operation failed and also triggers SyncFail hooks. PostSync hooks run last, and their failure marks the deployment failed [source: argocd-sync-phases-and-waves-2026-08-31].

Read PreSync as *"this must be finished before anything else changes"*: the database migration, the schema check. Read PostSync as *"this runs only if everything else worked and is healthy"*: the smoke test, the notification, the traffic cutover.

That last one connects back. Argo CD's feature list ties hooks directly to §2's vocabulary: *"PreSync, Sync, PostSync hooks to support complex application rollouts (e.g. blue/green and canary upgrades)"* [source: argocd-overview-2026-08-23]. Section 2 told you blue/green and canary need tooling above the Deployment. Hooks are part of how that tooling is built; a PostSync hook is a natural place for "now switch the traffic."

### Waves

Phases are coarse. Within a phase you frequently need finer ordering, and that is what waves provide.

Waves are set with the `argocd.argoproj.io/sync-wave` annotation, which takes an integer. *"Hooks and resources are assigned to wave 0 by default. The wave can be negative, so you can create a wave that runs before all other resources"* [source: argocd-sync-phases-and-waves-2026-08-31].

The full ordering algorithm, in order of precedence:

> *"1. The phase
> 2. The wave they are in (lower values first)
> 3. By kind
> 4. By name"*
>
> [source: argocd-sync-phases-and-waves-2026-08-31]

Phase first, then wave, then a deterministic fallback by kind and name. Everything you can control is in the first two lines.

<!-- FIGURE: ch15-fig06-sync-waves-and-hook-phases -->
```
   PHASE ──────────────────────────────────────────────────────────►

   ┌───────────┐   ┌───────────────────────────────┐   ┌───────────┐
   │  PreSync  │   │            Sync               │   │ PostSync  │
   │           │   │                               │   │           │
   │  db       │   │  W  wave -1 ┌───────────┐     │   │  smoke    │
   │  migration│   │  A          │ Namespace │     │   │  test     │
   │           │   │  V          └───────────┘     │   │           │
   │           │   │  E   wave 0 ┌───────────┐     │   │           │
   │           │   │             │    CRD    │     │   │           │
   │           │   │  │          └───────────┘     │   │           │
   │           │   │  ▼   wave 1 ┌───────────┐     │   │           │
   │           │   │             │  custom   │     │   │           │
   │           │   │             │ resource  │     │   │           │
   │           │   │             └───────────┘     │   │           │
   └───────────┘   └───────────────────────────────┘   └───────────┘

   must finish     within the phase, lower wave        runs only if
   before          numbers land first (default 0;      everything
   anything        negatives run before that)          succeeded and
   is applied                                          is Healthy

   ordering precedence:  phase → wave → kind → name
```

**Figure 15.6 — Two orderings, nested.** The horizontal axis is the phase; the vertical axis inside `Sync` is the wave. The example is the ordering problem this section opened with: a namespace must exist before the CustomResourceDefinition, which must exist before any custom resource that uses it.

Chapter 12 pointed here for a specific reason, and it is a good illustration of why ordering is not a theoretical concern. RBAC bindings are immutable in their subject reference: you cannot retarget a binding, you must delete it and create a new one *[cross-bearing: see Ch 12 §3 — what you may do]*. Under a system that reconciles a whole repository against a whole cluster, that is a real ordering constraint. The delete must precede the create, and the objects that depend on the resulting permissions must come after both. Waves are how you say so.

**What to take from this section.** Phases run in a fixed order and are gated on success. Waves order resources within a phase, lower numbers first, defaulting to zero and permitting negatives. Ordering is a problem GitOps has and a single `kubectl apply` merely ignores.

That is the whole of what this section owes you. Annotation syntax is here for concreteness, not for memorization; you do not need to be able to write one from memory.

---

## 🔵 §6 — The Other Agent, and More Than One Cluster

Argo CD is not the only implementation, and the alternative is worth meeting. Not because you need to operate it, but because the two make genuinely different design choices and the contrast sharpens what "GitOps agent" means.

**Flux** is a **GitOps Toolkit**: *"a collection of specialized tools, Flux Controllers, composable APIs, and reusable Go packages"* [source: flux-concepts-2026-08-31]. The earlier phrasing was blunter: *"Flux is a GitOps Toolkit: a set of composable APIs and specialized tools that can be used to build Continuous Delivery on top of Kubernetes"* [source: flux-concepts-2026-08-23].

That word *composable* is the whole contrast. Argo CD presents as an integrated application: one controller, one API, one web UI, one concept of an `Application` that ties source to destination. Flux presents as a set of controllers you assemble, each owning its own custom resources:

| Controller | Its custom resources |
|---|---|
| Source | `GitRepository`, `OCIRepository`, `HelmRepository`, `HelmChart`, `Bucket` |
| Kustomize | `Kustomization` |
| Helm | `HelmRelease` |
| Notification | `Provider`, `Alert`, `Receiver` |
| Image Reflector / Image Automation | `ImageRepository`, `ImagePolicy`, `ImageUpdateAutomation` |

[source: flux-components-2026-08-31]

Neither posture is better. Argo CD's integration gives you one thing to learn and a UI that shows you everything at once. Flux's composition gives you pieces you can adopt separately and replace individually. Teams pick on organizational grounds more than technical ones.

**Sources as a first-class concept.** Flux elevates the idea of where-state-comes-from into its own API: *"A Source defines the origin of a repository containing the desired state of the system and the requirements to obtain it (e.g. credentials, version selectors)"* [source: flux-concepts-2026-08-31]. The source controller produces an artifact; other controllers consume it.

Notice `OCIRepository` and `HelmRepository` in that list. Chapter 14 taught you that OCI registries can hold charts *[cross-bearing: see Ch 14 §4 — where charts come from]*, and Flux treats that as one source kind among several. Its Kustomize controller consumes overlays *[cross-bearing: see Ch 14 §5 — patching instead of templating]*, and its `Kustomization` API *"defines a pipeline for fetching, decrypting, building, validating and applying Kustomize overlays or plain Kubernetes manifests"* [source: flux-kustomization-api-2026-08-31].

**The most concrete statement of principle 4 in this chapter.** Flux's own documentation gives reconciliation a number and a consequence:

*"The reconciliation runs every five minutes by default, but this can be changed with `.spec.interval`."* And: *"If you make any changes to the cluster using `kubectl edit/patch/delete`, they will be promptly reverted"* [source: flux-concepts-2026-08-31].

> ⚓ **Worth Securing:** *"If you make any changes to the cluster using `kubectl edit/patch/delete`, they will be promptly reverted"* [source: flux-concepts-2026-08-31]. Read that as principle 4 with the abstraction removed. Continuous reconciliation is not a scheduling detail. It means your manual change has a shelf life measured in minutes. This is the same property that makes a ReplicaSet recreate a Pod you deleted; the surprising part is only where the desired state is kept.

<!-- AUTHOR-REVIEW: outline Open Question 8(b) — the five-minute figure is stated by flux-concepts-2026-08-31 and reproduced above. Note the tension recorded in flux-kustomization-api-2026-08-31's capture note: the API reference states `.spec.interval` is REQUIRED with a 60-second minimum and declares no default, so "five minutes by default" describes Flux's bootstrap-generated Kustomization rather than an API-level default. Both snapshots are current (2026-08-31). The text above follows the concepts page. Consider whether the revision stage should add the API-level qualification. -->

**Bootstrap.** Flux installs itself the way it installs everything else. *"The process of installing the Flux components in a GitOps manner is called a bootstrap. The manifests are applied to the cluster, a `GitRepository` and `Kustomization` are created for the Flux components, then the manifests are pushed to an existing Git repository (or a new one is created)"* [source: flux-concepts-2026-08-31]. The 2026-08-23 capture puts the consequence plainly: *"Flux manages itself like any other resource"* [source: flux-concepts-2026-08-23].

Sit with that for a moment, because it is the sort of thing that either seems trivial or seems remarkable depending on how carefully you read it. Upgrading Flux is a commit. Reconfiguring Flux is a commit. The agent's own desired state lives in the repository the agent watches, and the agent applies it to itself.

**Where the credentials live in Flux.** The security model differs from Argo CD's in an interesting way. Flux installs a `crd-controller` ClusterRole with *"full access to all the Custom Resource Definitions defined by Flux controllers,"* and a `cluster-reconciler` ClusterRoleBinding referencing the `cluster-admin` ClusterRole, *"bound to service accounts for only `kustomize-controller` and `helm-controller`"*, because those two *"are the only two controllers that manage resources in the cluster"* [source: flux-security-2026-08-31].

The reduction path is impersonation rather than narrowing: *"In a soft multi-tenancy setup, Flux does not reconcile a tenant's repo under the `cluster-admin` role. Instead, you specify a different service account in your manifest, and the Flux controllers will use the Kubernetes Impersonation API under `cluster-admin` to impersonate that service account"* [source: flux-security-2026-08-31]. The `Kustomization` API exposes this directly: `.spec.serviceAccountName` specifies *"the ServiceAccount to be impersonated while reconciling"* [source: flux-kustomization-api-2026-08-31].

Same problem as §4's, a broadly privileged agent, solved by a different route. Argo CD narrows the ClusterRole; Flux keeps the broad role and impersonates a narrower identity per workload.

**More than one cluster.** Which brings us to the question that shows the two designs most clearly. Where does desired state live when there are twenty clusters?

Argo CD's answer is a control point: among its features is the *"ability to manage and deploy to multiple clusters"* [source: argocd-overview-2026-08-23], with each external cluster's credentials stored as a Secret in the `argocd` namespace of the managing cluster [source: argocd-security-cluster-credentials-2026-08-31]. One Argo CD, many destinations, one place to look.

Flux's answer is per-cluster: each cluster runs its own Flux, bootstrapped into its own repository or its own path within a shared one, each pulling independently. No cluster holds credentials to another.

Both are honest answers. The centralized model gives you one console and one place to reason about; it also gives you one component whose compromise reaches everywhere, which is §3's blast-radius argument returning at a larger scale. The per-cluster model gives you isolation and costs you a unified view.

> 🔭 **Closer Look:** Argo and Flux are both CNCF **graduated** projects [source: cncf-project-maturity-levels-2026-08-23], the maturity tier CNCF describes as stable, widely adopted, and production ready. What the levels *mean* is Chapter 17's subject, and that is the durable thing to know *[cross-bearing: see Ch 17 §2 — sandbox, incubating, graduated, and who decides]*. The roster of which projects currently hold which level is dated data that changes; do not memorize it.

---

## ☆ Taking Your Bearings 3: Ordering, and the Other Agent

Five questions. The last one is the most important retrieval item in this chapter. Read it carefully, because the next section is about to depend on your answer.

**1.** A repository contains a CustomResourceDefinition and a custom resource that uses it. Applied together with no ordering, the custom resource is rejected. What mechanism orders them, what value would you give each, and what happens to a resource you annotate with nothing?

**2.** A team needs a database schema migration to complete before any new application Pod starts, and a smoke test to run only after everything is up and healthy. Which hook phase does each belong to, and what does the second one additionally require before it runs?

**3.** Describe the structural difference between Argo CD's and Flux's design posture in one sentence each, and name one consequence of that difference for a team adopting either.

**4.** A colleague fixes a production incident with `kubectl patch` on a cluster managed by Flux. They do not commit the change. What happens, on what timescale, and which OpenGitOps principle is responsible?

**5.** [retrieval: ch3] In your own words: what does a controller do, what two things does it compare, and how often does it do it? Answer without mentioning Git, repositories, or delivery.

---

<details>
<summary>Answers with explanations</summary>

**1. Sync waves**, via the `argocd.argoproj.io/sync-wave` annotation, which takes an integer [source: argocd-sync-phases-and-waves-2026-08-31].

Give the CRD a lower wave than the custom resource: for instance the CRD at `-1` and the custom resource at the default `0`, or the CRD at `0` and the custom resource at `1`. Resources sync *"lower values first"*, and negative waves are permitted precisely so you can run something before everything else [source: argocd-sync-phases-and-waves-2026-08-31].

A resource annotated with nothing lands in **wave 0**: *"Hooks and resources are assigned to wave 0 by default"* [source: argocd-sync-phases-and-waves-2026-08-31].

**2. Migration → PreSync. Smoke test → PostSync.**

PreSync hooks run *"prior to the application of the manifests"*, before any new Pod exists [source: argocd-sync-phases-and-waves-2026-08-31].

PostSync additionally requires health, not merely completion. It runs *"after all Sync hooks completed and were successful, a successful application, and all resources in a Healthy state"* [source: argocd-sync-phases-and-waves-2026-08-31]. That health gate is the part readers miss: PostSync is not "after the apply," it is "after the apply worked and the result is healthy."

**3. Argo CD is integrated** — one application with one controller model, one `Application` resource binding source to destination, and a UI over the whole thing. **Flux is composable** — *"a collection of specialized tools, Flux Controllers, composable APIs"* [source: flux-concepts-2026-08-31], each with its own custom resources [source: flux-components-2026-08-31].

Any of these consequences earns credit: Flux lets you adopt or replace pieces independently while Argo CD is more nearly all-or-nothing; Argo CD gives one console showing every application while Flux's state is spread across controllers; Flux's per-controller APIs mean more objects to learn, Argo CD's integration means fewer.

**4. The change is reverted, within roughly five minutes, by principle 4 (Continuously Reconciled).**

Flux states both facts directly: *"The reconciliation runs every five minutes by default"* and *"if you make any changes to the cluster using `kubectl edit/patch/delete`, they will be promptly reverted"* [source: flux-concepts-2026-08-31]. Principle 4 requires that *"software agents continuously observe actual system state and attempt to apply the desired state"* [source: opengitops-principles-v1-2026-08-31]. The uncommitted patch is not the desired state, so it is not what the agent applies.

**Practical consequence worth stating:** under continuous reconciliation, an emergency fix must be committed to survive. The tool is not being obstructive; it is doing exactly the job it was installed for. A team that finds this intolerable during incidents needs a documented way to suspend reconciliation, not a workaround.

**5. [retrieval: ch3] A controller compares desired state against current state, and acts to close the gap. It does this continuously, in a loop, indefinitely** — not once at creation, and not only when something triggers it. If the two disagree it takes whatever action moves current toward desired, then it checks again *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*.

If that came back clean, keep it loaded. The next section is one substitution away from it.

If it did not come back clean, **re-read Ch 3 §6 now, before §7.** This is not a formality. The final section owns no new material; its entire content is a change made to the thing you just tried to state, and if the original is fuzzy, the change is invisible.

</details>

---

## ☀️ §7 — The Control Loop, Pointed at a Repository

This section teaches nothing new.

That is not modesty and it is not a warning; it is the design. Everything below has already been taught, most of it in Chapter 3, some of it as recently as four pages ago. What happens here is a single substitution, performed slowly, in front of you.

Here is the loop, as Chapter 3 gave it to you.

A controller holds a **desired state**, a record of what should be true. It observes the **current state**, what is actually true. When the two differ, it takes action to close the gap. Then it checks again. It does not stop. There is no completion condition, no final state, no moment at which the controller decides its work is finished and exits.

In Chapter 3, the desired state was in etcd, reached through the API server.

Now move it. Take the desired state out of etcd and put it in a Git repository.

<!-- FIGURE: ch15-zenith-control-loop-pointed-at-a-repo -->
```
                        ┌─────────────────┐
                        │  DESIRED STATE  │
                        │                 │
                        │  ╔═══════════╗  │   ◄── the ONLY substitution
                        │  ║    Git    ║  │       (was: etcd)
                        │  ║ repository║  │
                        │  ╚═══════════╝  │
                        └────────┬────────┘
                                 │
                                 │  observe
                                 ▼
                        ┌─────────────────┐
                        │                 │
             ┌─────────►│   CONTROLLER    │──────────┐
             │          │                 │          │
             │          └─────────────────┘          │  act to
             │                                       │  close the gap
             │  observe                              │
             │                                       ▼
    ┌────────┴────────┐                     ┌─────────────────┐
    │ CURRENT STATE   │◄────────────────────│   API SERVER    │
    │                 │                     │  (still the     │
    │  what is        │                     │   only door in) │
    │  actually true  │                     └─────────────────┘
    └─────────────────┘

              and then it does it again. forever.
```

**Figure 15.7 — The control loop, pointed at a repository.** Lay this beside Figure 3.2 and the point is that they are the same drawing. The loop is the same loop, the controller sits in the same place, the API server is still the only door in, and the arrows run in the same directions. One box changed contents.

Look at what did *not* move.

**The API server is still the only mutator.** The agent writes to the cluster the way everything else does: as an API client, through authentication, authorization, and admission *[cross-bearing: see Ch 3 §5 — the only door in]*.

**The coordination is still watching, not telling.** Nothing pushes work to the controller. It observes and decides. Chapter 3 called this out as the architecture's central property, and said it would be retrieved: the same architecture, with a different thing in the hub position.

**The controller is still shaped the same way.** Compare, act, repeat. No new lifecycle, no new mechanism, no new category of component.

**Reconciliation is still endless.** A ReplicaSet does not finish. Neither does this.

One box changed contents. That is the entire technical delta between "Kubernetes" and "GitOps."

### The four principles, re-read

Now the four principles from §3, which looked like a list when you met them and are not one.

**1. Declarative.** This is Chapter 4. You file a declaration; the system's job is to make it true *[cross-bearing: see Ch 4 §1 — you file a declaration]*. Nothing added.

**2. Versioned and immutable.** This is the only genuinely new thing in the whole model, and it is a property of the *store*, not of Kubernetes. etcd holds the current desired state. A repository holds every desired state there has ever been, in order, each one fixed. That difference is what makes rollback by revert possible at all: you cannot return to a state your store did not keep.

**3. Pulled automatically.** This is Chapter 3's watch *[cross-bearing: see Ch 3 §5 — the only door in]*. Agents observe a source and fetch from it. The direction of travel was never inward.

**4. Continuously reconciled.** This is the loop itself. Word for word, it is what Chapter 3 §6 told you a controller does.

Three of the four were already yours. You have been running GitOps-shaped machinery since Chapter 3; the principles simply name what happens when the desired-state store is one a human can read, review, and revert.

Which kills the misreading this chapter was built to prevent.

> ★ **Fixed Point**
>
> **GitOps is not "running CI from Git." None of the four principles mentions integration, building, testing, or a pipeline. All four are about desired state — how it is expressed, how it is stored, how it is obtained, and how it is applied. The build is somebody else's job, and Kubernetes said so in its own documentation: it *"does not deploy source code and does not build your application"* [source: k8s-docs-overview-2026-08-23].**

### Why the chapter is called what it is

The chart is the truth, but not because a file is inherently authoritative. Files are only ever claims. A YAML manifest on somebody's laptop is a claim nothing enforces; a repository full of manifests that nothing watches is a folder of hopeful documents, which is precisely what Chapter 14 left you holding.

The chart is the truth because **something is continuously making it true.** The authority is not in the file. It is in the loop that never stops comparing the file to the world and acting on the difference.

That is what you have been building toward since Chapter 3, whether or not it looked like it. And it is why Chapter 6 said what it said when it finished teaching the control loop: that when you met this, it would look like a new idea for about ten seconds *[cross-bearing: see Ch 6 §8 — the control loop, extended]*.

Ten seconds is about right.

---

## 🏆 Safe Harbor

**Checkpoint: You've Now Mastered**

✓ The twelve factors, sorted by who solves them — and the four that matter most in a cluster
✓ Deployment strategy vocabulary, and the line between a Deployment field and a pattern needing tooling
✓ Push versus pull as an architectural question about credentials and blast radius
✓ The four OpenGitOps principles, and why "pulled" and "continuously" carry the definition
✓ Argo CD as a controller: `Application`, manifest sources, tracking targets, `Synced` and `OutOfSync`
✓ Rollback by revert, and why it is the third mechanism to wear that word
✓ The delivery agent's identity, its default grants, and why commit access is cluster access
✓ Sync phases and waves, and the ordering problem they exist for
✓ Flux's composable posture, self-bootstrap, and the two shapes of multi-cluster delivery
✓ The control loop, pointed at a repository — and everything about it that did not change

---

## Exam Alert! 🚨

**High-Priority Topics**

**1. The four OpenGitOps principles, in order, with the words that matter.** Declarative; versioned and immutable; **pulled** automatically; continuously reconciled [source: opengitops-principles-v1-2026-08-31]. *Pulled* and *continuously* carry the distinction. A definition missing either one describes something that is not GitOps.

**2. `OutOfSync` is a drift signal, not an error.** It reports that live state deviates from the target state in Git [source: argocd-overview-2026-08-23]. A person editing the cluster produces it. Nothing failed.

**3. Argo CD is a Kubernetes controller.** It *"continuously monitors running applications and compares the current, live state against the desired target state"* [source: argocd-architecture-2026-08-31]. It does not bypass the API server, and it is not a new category of technology.

**4. Deployment strategy vocabulary versus Deployment fields.** `RollingUpdate` and `Recreate` are values on a Deployment [source: argo-rollouts-strategies-2026-08-23]. Blue/green and canary are patterns implemented by tooling above it.

---

**Common Traps** — these are distinctions that are easy to confuse, and they are the ones this material rewards getting right.

| The trap | The correct understanding |
|---|---|
| "GitOps means running CI from Git" | GitOps is four principles about *desired state*. Continuous integration is not one of them, and the cluster does not care who built the artifact. |
| Assuming a pipeline pushes to the cluster | Principle 3 is explicit: agents **pull** desired-state declarations from the source [source: opengitops-principles-v1-2026-08-31]. Push-based CD is not GitOps, whatever its manifests are stored in. |
| Treating reconciliation as a deploy-time event | Principle 4 is **continuous** and indefinite, the same property that makes a ReplicaSet recreate a Pod you deleted last Tuesday. Flux reverts a manual `kubectl` change within minutes [source: flux-concepts-2026-08-31]. |
| "`OutOfSync` means the sync failed" | Sync status and sync *operation* status are two different fields answering two different questions [source: argocd-core-concepts-2026-08-31]. An application can be `OutOfSync` immediately after a successful sync [source: argocd-diffing-outofsync-2026-08-31]. |
| "Argo CD only deploys plain YAML" | Kustomize applications, Helm charts, Jsonnet, plain YAML/JSON directories, and custom config-management plugins [source: argocd-overview-2026-08-23]. |
| "Argo CD can only track a branch" | Branches, tags, or a **pinned Git commit** [source: argocd-tracking-strategies-2026-08-31]. |
| Assuming a GitOps agent writes to the datastore directly | It is an API client like any other, subject to authentication, authorization, and admission. Chapter 3's claim about the only door in is not suspended *[cross-bearing: see Ch 3 §5 — the only door in]*. |
| Assuming a delivery agent needs no identity because it is "infrastructure" | It is a Pod with a ServiceAccount and, by default, cluster-admin-level grants [source: argocd-security-cluster-credentials-2026-08-31] — one of the highest-value subjects in the cluster. |
| Collapsing the third rollback into one of the first two | `rollout undo` restores a Pod template. `helm rollback` returns a release to a prior revision. **Rollback by revert** changes a commit and lets the agent reconcile. Three mechanisms, one word. |
| Assuming a Deployment can express blue/green or canary by itself | Both need something above the Deployment; canary additionally needs traffic splitting and metric analysis [source: argo-rollouts-strategies-2026-08-23]. |

---

## Practice Questions

Twenty-one questions. Several present a situation rather than asking for a definition; those are the ones worth slowing down for, because a glossary cannot answer them.

---

**Q1.** An application writes its logs to `/var/log/app.log` inside the container and rotates them itself with a background thread. Which twelve-factor factor does this violate, and what capability does it break?

**Q2.** According to the twelve-factor methodology, which of the following is the *strongest* evidence that an application has correctly factored out its config?

A) It reads all settings from a `config.yaml` file at startup
B) Its codebase could be made open source at any moment without compromising credentials
C) It has separate configuration bundles named `staging` and `production`
D) It stores all settings in a database table

**Q3.** A team argues that because their application is containerized and deployed by a Deployment, it is twelve-factor compliant. The application holds user session state in process memory. Evaluate the claim.

**Q4.** Which strategy guarantees that two versions of an application never run simultaneously, and what does it cost?

A) `RollingUpdate` — costs additional capacity
B) Canary — costs traffic-splitting infrastructure
C) `Recreate` — costs downtime
D) Blue/green — costs double capacity

**Q5.** A team runs a queue-consuming worker with no inbound HTTP traffic. They want to validate a new version against production configuration before it processes real work. Which strategy fits, and why is canary a poor choice here?

**Q6.** Sort these into "value of a Deployment's `.spec.strategy`" and "pattern requiring tooling above the Deployment": canary, `Recreate`, blue/green, `RollingUpdate`.

**Q7.** Progressive delivery is defined as releasing updates in a controlled and gradual manner, *"typically coupling automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23]. Which half of that definition distinguishes progressive delivery from simply deploying slowly, and why?

**Q8.** A pipeline builds an image, commits the new image tag to a Git repository, and then runs `kubectl apply` against the cluster from the CI runner. Which OpenGitOps principles does this satisfy and which does it fail?

**Q9.** Which statement about push-based delivery is accurate?

A) It cannot be automated
B) It stores cluster-write credentials outside the cluster
C) It is incompatible with storing manifests in Git
D) It bypasses the Kubernetes API server

**Q10.** Explain "blast radius" in the context of delivery architecture, using a compromised CI system as the example. Say what pull-based delivery does and does not change about it.

**Q11.** Which principle is violated by a system that stores declarative manifests in Git, has an in-cluster agent fetch them, applies them on each new commit, and then does nothing until the next commit?

A) Declarative
B) Versioned and immutable
C) Pulled automatically
D) Continuously reconciled

**Q12.** Kubernetes documentation states that it *"does not deploy source code and does not build your application"* [source: k8s-docs-overview-2026-08-23]. What does this establish about the relationship between CI and GitOps?

**Q13.** An Argo CD `Application` reports `OutOfSync`. Which of these could be the cause?

A) An engineer ran `kubectl scale` on a managed Deployment
B) A new commit landed in the tracked path and has not been applied
C) The most recent sync operation failed
D) All of the above

**Q14.** An Argo CD `Application` points at a repository path containing a Helm chart. A colleague says this cannot work because "Argo CD is a YAML tool, and Helm is a separate deployment mechanism." Correct them, naming the component involved.

**Q15.** A team pins an `Application` to a Git commit SHA. Their build pipeline pushes new commits to the tracked branch daily. What happens to the cluster, and what would have to change for it to update?

**Q16.** [cross-domain: D2.2] A GitOps agent must create Deployments and Services in twelve namespaces it does not own, and delete resources removed from the repository. What must exist for this to be permitted, and why is a Role in each namespace a poor answer?

**Q17.** [cross-domain: D1.1] An engineer describes `OutOfSync` as "the status field not matching the spec field." Is this a good analogy? Explain precisely what is being compared and where each operand lives.

**Q18.** Three things in this book are called rollback. Name the mechanism each one uses and where each keeps the state it returns to.

**Q19.** A repository contains a namespace, a CustomResourceDefinition, and a custom resource of the type that CRD defines. Applied simultaneously, this fails. Which mechanism orders them, and what is the default assignment for a resource with no ordering annotation?

**Q20.** Which hook phase runs *"after all Sync hooks completed and were successful, a successful application, and all resources in a Healthy state"* [source: argocd-sync-phases-and-waves-2026-08-31], and what does that make it suitable for?

**Q21.** Flux describes itself as a GitOps Toolkit — *"a collection of specialized tools, Flux Controllers, composable APIs"* [source: flux-concepts-2026-08-31] — while Argo CD presents as an integrated application with a single `Application` resource. Name one practical consequence of this difference for a team adopting either, and one way their multi-cluster answers differ.

---

<details>
<summary>Answers with full explanations</summary>

**Q1. Factor XI (Logs — treat logs as event streams).** The rule is that *"a twelve-factor app never concerns itself with routing or storage of its output stream"*; each process writes unbuffered to stdout and the execution environment captures it [source: twelve-factor-xi-logs-2026-08-31].

What it breaks: `kubectl logs` returns nothing useful, because the container's stdout is empty. Node-level log collection sees nothing. The logs exist only in the container's writable layer and are destroyed with the Pod, which means the logs from the crash you are investigating died with the thing that crashed.

**Q2. B.** *"A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials"* [source: twelve-factor-iii-config-2026-08-31].

**A is wrong** — a config file is explicitly called out as an improvement that *"still has weaknesses: it's easy to mistakenly check in a config file to the repo"* [source: twelve-factor-iii-config-2026-08-31]. **C is wrong**, and is in fact a named anti-pattern: env vars *"are never grouped together as 'environments', but instead are independently managed for each deploy"* [source: twelve-factor-iii-config-2026-08-31]. **D is wrong** — it relocates the problem without solving it; the database credentials still have to come from somewhere.

**Q3. The claim fails.** In-memory session state violates factor VI: *"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service"* [source: twelve-factor-vi-processes-2026-08-31]. The methodology bans the usual workaround by name — *"Sticky sessions are a violation of twelve-factor and should never be used or relied upon"* — and suggests a time-expiring datastore instead [source: twelve-factor-vi-processes-2026-08-31].

The general point matters more than this instance: containerization and Deployments implement the *platform* side of twelve-factor. They cannot implement the application side. Packaging a stateful process in a container produces a containerized stateful process.

**Q4. C.** *"A Recreate deployment deletes the old version of the application before bringing up the new version. As a result, this ensures that two versions of the application never run at the same time, but there is downtime during the deployment"* [source: argo-rollouts-strategies-2026-08-23].

**A is wrong** — `RollingUpdate` guarantees the opposite: both versions run concurrently by design, which is what avoids the downtime. **D is wrong** — blue/green does run both versions simultaneously; only one *receives production traffic* [source: argo-rollouts-strategies-2026-08-23], which is a different guarantee and does not help with, say, an incompatible schema migration. **B is wrong** — canary deliberately runs both against real traffic.

**Q5. Blue/green.** Both versions run, only the old receives production traffic, and *"this allows the developers to run tests against the new version before switching the live traffic"* [source: argo-rollouts-strategies-2026-08-23], against production configuration and production backing services.

Canary is a poor fit for a specific mechanical reason: it works by proportioning *traffic*, and a queue worker has no inbound traffic to proportion. Argo's own comparison makes the pairing: canary demands traffic-splitting via a service mesh or ingress controller, while blue/green *"needs no traffic provider and suits workloads such as queue workers"* [source: argo-rollouts-strategies-2026-08-23].

**Q6. Deployment strategy values: `Recreate`, `RollingUpdate`.** `RollingUpdate` *"is the default strategy of the Deployment object"* [source: argo-rollouts-strategies-2026-08-23]. **Requiring tooling above the Deployment: blue/green, canary.**

This is the section's Fixed Point. The trap is that all four sound like the same kind of thing when they appear in one list; two are a field value and two are an architecture.

**Q7. The metric-analysis half.** *Gradual* alone is just a slower deployment: a `RollingUpdate` with a small `maxSurge` is gradual and is not progressive delivery. What the definition adds is *"automation and metric analysis to drive the automated promotion or rollback of the update"* [source: argo-rollouts-strategies-2026-08-23]. The release evaluates itself against measurements and decides whether to continue or reverse. Gradual buys time; metric analysis is what uses the time.

**Q8. Satisfies 1 (Declarative) and 2 (Versioned and Immutable). Fails 3 (Pulled Automatically) and 4 (Continuously Reconciled).**

Committing manifests to Git satisfies the first two. But principle 3 requires that *"software agents automatically pull the desired state declarations from the source"* [source: opengitops-principles-v1-2026-08-31], and here the CI runner pushes. And principle 4 requires *continuous* observation; the runner exits after applying, and between commits nothing is watching.

Storing manifests in Git is the most common false positive for "we do GitOps." It is one principle out of four, and not the one that changes anything.

**Q9. B.** In push-based delivery the pipeline lives outside the cluster and must hold credentials to it.

**A is wrong** — push-based delivery is normally *entirely* automated; that is its appeal. **C is wrong** — many push pipelines apply manifests from Git; that is precisely the arrangement Q8 describes, and it is what makes the distinction subtle. **D is wrong** — nothing bypasses the API server, in either model *[cross-bearing: see Ch 3 §5 — the only door in]*.

**Q10. Blast radius is how far the damage from a single compromise reaches.** A shared CI system holding write credentials for a dozen clusters has a blast radius of a dozen clusters: whoever controls the pipeline controls every cluster it deploys to. Under pull-based delivery, each cluster's agent holds credentials only to its own cluster, so compromising the CI system yields the ability to build and publish artifacts, a serious supply-chain problem, but not direct cluster-write access anywhere.

**What pull does not change:** it does not prevent compromise, and it does not make the agent's own credentials smaller. Argo CD's default is *"a clusteradmin level role"* [source: argocd-security-cluster-credentials-2026-08-31]. Anyone who can commit to the tracked branch can, transitively, do whatever the agent may do. Pull relocates and bounds the risk; it does not remove it.

**Q11. D.** Principle 4 requires that agents *"continuously observe actual system state and attempt to apply the desired state"* [source: opengitops-principles-v1-2026-08-31]. A system that acts only on new commits satisfies principle 3, since it does pull, but has no answer to drift introduced any other way. A manual `kubectl edit` would persist indefinitely, which is exactly the failure GitOps exists to close.

**A, B, and C are all satisfied** by the described system: the manifests are declarative, they are in a versioned store, and the agent pulls them.

**Q12. It establishes that CI and GitOps are orthogonal concerns, not stages of one thing.** The cluster does not build your application and does not care who did; CI/CD workflows are *"determined by organization cultures and preferences as well as technical requirements"* [source: k8s-docs-overview-2026-08-23]. GitOps starts after a deployable artifact exists, and concerns itself only with how desired state is stored and applied. A team can have excellent CI and no GitOps, or GitOps with a build process that is entirely manual.

This is why "GitOps means running CI from Git" is wrong at the level of category, not just detail.

**Q13. D — all of the above.**

A and B produce `OutOfSync` with nothing failing: *"a deployed application whose live state deviates from the target state is considered OutOfSync"* [source: argocd-overview-2026-08-23], and deviation has many innocent causes. C can also leave an application `OutOfSync`, but the *failure* is reported in a different field; sync status and sync operation status are separate glossary entries answering separate questions [source: argocd-core-concepts-2026-08-31].

The item exists to break the assumption that `OutOfSync` implies a failed operation. It does not imply one, and does not exclude one.

**Q14. The colleague is wrong on both counts.** Argo CD accepts manifests *"in several ways: kustomize applications; helm charts; jsonnet files; plain directory of YAML/json manifests; any custom config management tool configured as a config management plugin"* [source: argocd-overview-2026-08-23].

The component: the **repository server**, which *"maintains a local cache of the Git repository holding the application manifests"* and is responsible for *"generating and returning the Kubernetes manifests"* given a repository URL, revision, path, and template-specific configuration [source: argocd-architecture-2026-08-31]. Rendering is a dedicated component, not an afterthought. Argo CD's glossary even names the choice: the **application source type** is *"which Tool is used to build the application"* [source: argocd-core-concepts-2026-08-31].

**Q15. Nothing happens to the cluster.** *"If a Git commit SHA is specified, the app is effectively pinned to the manifests defined at the specified commit"* [source: argocd-tracking-strategies-2026-08-31]. New commits on the branch are irrelevant; the `Application` is not looking at the branch.

To update: *"the only way to change the live state of an app which is pinned to a commit, is by updating the tracking revision in the application to a different commit containing the new manifests"* [source: argocd-tracking-strategies-2026-08-31]. Somebody must change the `Application`'s own revision field, which is itself typically a commit in a repository, and therefore itself reviewable. That is the point of pinning.

**Q16. [cross-domain: D2.2] A ServiceAccount, and a ClusterRole bound by a ClusterRoleBinding.** The ServiceAccount is the identity the agent's Pod runs as; the ClusterRole enumerates permitted verbs on resources; the ClusterRoleBinding attaches the permission set to the identity across the whole cluster *[cross-bearing: see Ch 12 §3 — what you may do]*.

**Why per-namespace Roles are a poor answer:** they work, and they break. Every new namespace the repository introduces requires a new Role and RoleBinding before the agent can act in it, which means the agent cannot create a namespace and populate it in one sync, and the failure appears as a permissions error at exactly the moment someone adds a namespace. Argo CD's own model uses a cluster-scoped role for this reason, noting that it *"requires cluster-wide read privileges to resources in the managed cluster to function properly"* even when write is narrowed [source: argocd-security-cluster-credentials-2026-08-31].

**Q17. [cross-domain: D1.1] It is a good analogy and worth being precise about.** Argo CD compares **target state** — *"the desired state of an application, as represented by files in a Git repository"* — against **live state** — *"the live state of that application. What pods etc are deployed"* [source: argocd-core-concepts-2026-08-31].

The mapping to Chapter 4: target state plays the role of `spec` (what was asked for), and live state is observed from the cluster, which is what `status` reports on *[cross-bearing: see Ch 4 §2 — the anatomy of a record]*.

The one refinement: the operands live in different places. In an ordinary object, `spec` and `status` are two fields of one record in etcd. Under GitOps, the authored `spec` lives outside the cluster entirely, and the cluster's copy is downstream of it. That relocation is the whole substitution, and it is why an object's own `spec` can be perfectly satisfied while the application is `OutOfSync`, if somebody changed the `spec` itself by hand.

**Q18. Three mechanisms:**

- **`kubectl rollout undo`** (Ch 6 §5) — restores a Deployment's Pod template. Prior state lives in the old ReplicaSet, on the cluster.
- **`helm rollback`** (Ch 14 §3) — returns a Helm release to a prior revision. Prior state lives in Helm's release history, on the cluster.
- **Rollback by revert** (this chapter) — changes a commit in the repository; the agent reconciles as it always does. Prior state lives in the repository's history. Argo CD describes the capability as *"rollback/roll-anywhere to any application configuration committed in Git repository"* [source: argocd-overview-2026-08-23].

The structural point worth carrying: the third has no dedicated rollback code path. You move the target and the loop does the rest, the same loop that handles every ordinary change.

**Q19. Sync waves**, via the `argocd.argoproj.io/sync-wave` annotation, an integer, ordered *"lower values first"* [source: argocd-sync-phases-and-waves-2026-08-31].

Default assignment: *"Hooks and resources are assigned to wave 0 by default. The wave can be negative, so you can create a wave that runs before all other resources"* [source: argocd-sync-phases-and-waves-2026-08-31].

For the example: namespace first, CRD second, custom resource third, for instance `-2`, `-1`, `0`, or `0`, `1`, `2`. What matters is the relative order, not the absolute numbers. The full precedence is *"1. The phase 2. The wave they are in (lower values first) 3. By kind 4. By name"* [source: argocd-sync-phases-and-waves-2026-08-31].

**Q20. PostSync**, and the quoted condition is what makes it distinctive: it requires not just completion but *"all resources in a Healthy state"* [source: argocd-sync-phases-and-waves-2026-08-31].

Suitable for: smoke tests, notifications, and traffic cutover, anything that should happen only once the new state is both applied and demonstrably working. Argo CD ties the hook mechanism to release patterns explicitly, describing hooks as supporting *"complex application rollouts (e.g. blue/green and canary upgrades)"* [source: argocd-overview-2026-08-23].

**Why not PreSync:** PreSync runs *"prior to the application of the manifests"* [source: argocd-sync-phases-and-waves-2026-08-31], before the thing you would be testing exists.

**Q21. Practical consequence** (any one earns credit): Flux's composability means a team can adopt the source and Kustomize controllers without the Helm or image-automation ones, and can replace pieces independently; Argo CD's integration means fewer objects to learn and a single UI showing every application's state, at the cost of being more nearly all-or-nothing. Flux's design surfaces as many custom resources across several controllers [source: flux-components-2026-08-31]; Argo CD's surfaces mainly as `Application` objects [source: argocd-core-concepts-2026-08-31].

**Multi-cluster difference:** Argo CD manages multiple clusters from one control point. The feature list includes the *"ability to manage and deploy to multiple clusters"* [source: argocd-overview-2026-08-23], with each remote cluster's credentials stored as a Secret in the `argocd` namespace [source: argocd-security-cluster-credentials-2026-08-31]. Flux's model is one Flux per cluster, each bootstrapped into its own repository or path and pulling independently, with no cluster holding credentials to another [source: flux-concepts-2026-08-31].

The trade is the one from §3 at a larger scale: a single control point gives you one console and one blast radius; per-cluster agents give you isolation and no unified view.

</details>

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| Twelve-factor app | Constraints an application accepts so a platform can run it. Kubernetes implements the platform half; the application half is still yours. |
| Factor III (Config) | Config is what varies between deploys. The test: could you open-source the repo today without leaking a credential? |
| Factor IX (Disposability) | Fast startup, graceful SIGTERM shutdown, correct even on sudden death. |
| `Recreate` / `RollingUpdate` | Values of a field on a Deployment. Downtime with no version overlap, versus no downtime with overlap. |
| Blue/green | Two full environments; only one takes traffic; test before the switch. Costs capacity, needs no traffic provider. |
| Canary | A slice of real traffic meets the new version first. Needs traffic splitting and metric analysis. |
| Progressive delivery | Gradual *plus* metric analysis driving automated promotion or rollback. Gradual alone is just slow. |
| Push | Pipeline outside the cluster holds cluster credentials and reaches in. Nothing watches between runs. |
| Pull | Agent inside the cluster holds repository credentials and reaches out. Never stops watching. |
| Blast radius | How far one compromise reaches. Pull bounds it; it does not shrink the agent's own grants. |
| The four principles | Declarative · versioned and immutable · **pulled** automatically · **continuously** reconciled. |
| Argo CD | A Kubernetes controller comparing live state against target state in a repository. |
| `Application` | The custom resource: a source (repo, revision, path) and a destination (cluster, namespace). |
| Manifest sources | Kustomize, Helm charts, Jsonnet, plain YAML/JSON, config-management plugins. |
| Tracking | Branch (moves), tag (rarely moves), pinned commit (never moves). |
| `OutOfSync` | Live state deviates from target state. A drift signal, not an error. A person can cause one. |
| Rollback by revert | Change the commit; the loop does the rest. No second code path. Third mechanism to wear the word. |
| Agent identity | A Pod, a ServiceAccount, broad grants by default. Commit access to the tracked branch is cluster access. |
| Sync phases | PreSync → Sync → PostSync, each gated on the previous succeeding. PostSync also requires Healthy. |
| Sync waves | Integer ordering within a phase, lower first, default 0, negatives allowed. |
| Flux | A composable toolkit of controllers. Bootstraps itself. Reverts manual `kubectl` changes within minutes. |
| The Zenith | The control loop, with a Git repository where etcd sat. Nothing else moved. |

---

## The Voyage Ahead

You now hold a delivery model in which nobody touches the cluster and something never stops watching it.

Which is exactly when you find out that the thing being watched is not the thing you thought.

The agent reports `Synced`. Every object matches the repository, every replica is present, the rollout completed and the health checks pass. And the application does not work. Users get errors, or timeouts, or the wrong data, and nothing in the delivery path has anything to say about it, because the delivery path did its job perfectly. It applied what you asked for. You asked for the wrong thing, or the right thing configured wrongly, and no amount of reconciliation can tell the difference.

Chapter 13 taught you to diagnose a cluster that will not run your Pod. It ended by handing something back: the case where the platform is fine and the problem is yours. That handoff comes due next.

The next chapter is about the Pod that is running, healthy, `Synced`, and wrong, and about the tools that let you get inside a container that was built with nothing in it to help you.

> *"Reconciliation will make the cluster match your intention exactly. It has no opinion about your intention."*
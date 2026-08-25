---
source_url: "https://kubernetes.io/docs/concepts/scheduling-eviction/api-eviction/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/scheduling-eviction/api-eviction.md"
fetched_at: "2026-08-24T18:58:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["api-initiated-eviction", "drain", "node-controller"]
---
# API-initiated Eviction

> **Extraction note.** Passages marked **[VERBATIM]** are safe to cite.

**[VERBATIM]**

> "You can request eviction by calling the Eviction API directly, or programmatically using a client of the API server, like the `kubectl drain` command. This creates an `Eviction` object, which causes the API server to terminate the Pod."

> "Using the API to create an Eviction object for a Pod is like performing a policy-controlled `DELETE` operation on the Pod."

> "API-initiated evictions respect your configured `PodDisruptionBudgets` and `terminationGracePeriodSeconds`."

> "the API server performs admission checks and responds in one of the following ways"

---

NOT VERBATIM-CAPTURED: the enumerated response outcomes following that last sentence
(200 OK / 429 / 500) were returned only as a gloss and must not be quoted. The page draws
no explicit contrast with node-pressure eviction; node-pressure eviction appears only as a
"what's next" link.

**Why this file exists.** The cached Nodes page says the node controller triggers
"API-initiated eviction of all the Pods from the node if it stays unreachable," and sec.4
lists `api-initiated-eviction` as a concept. This snapshot supplies the definition of the
term the Nodes page uses without defining. It is also the sourced link between `drain` and
eviction: drain is a client of the Eviction API, which is one more instance of sec.8's
claim -- an administrative command is a write through the one door.

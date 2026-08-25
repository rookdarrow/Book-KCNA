---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/tasks/debug/debug-cluster/audit.md"
fetched_at: "2026-08-24T18:59:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["auditing", "audit-policy", "audit-stages", "audit-backends"]
closes_gap: "ch-08 outline Open Question #4. Auditing was a page title with no cached definition; the option (a) fetch was recommended as free if Stage 2 was already in this doc tree. It was."
---
# Auditing

> **Extraction note.** Passages marked **[VERBATIM]** are safe to cite.

## Overview

**[VERBATIM]**

> "Kubernetes _auditing_ provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster."

> "Auditing allows cluster administrators to answer the following questions: what happened? when did it happen? who initiated it? on what did it happen? where was it observed? from where was it initiated? to where was it going?"

## Where audit records come from

**[VERBATIM]**

> "Audit records begin their lifecycle inside the kube-apiserver component. Each request on each stage of its execution generates an audit event."

## Stages

**[VERBATIM]**

- `RequestReceived` -- "The stage for events generated as soon as the audit handler receives the request"
- `ResponseStarted` -- "Once the response headers are sent, but before the response body is sent"
- `ResponseComplete` -- "The response body has been completed and no more bytes will be sent"
- `Panic` -- "Events generated when a panic occurred"

## Audit policy

**[VERBATIM]**

> "Audit policy defines rules about what events should be recorded and what data they should include."

The four audit **levels** are named on the page as `None`, `Metadata`, `Request` and
`RequestResponse`. **[NAMES ONLY]** -- their one-line definitions were not verbatim-captured
in this pass and must not be quoted. See research-manifest Gaps, G-8D.

## Backends

**[VERBATIM, lightly joined -- the bracketed conjunction is the fetch's, not the source's]**

> "Out of the box, the kube-apiserver provides two backends: Log backend, which writes events into the filesystem [and] Webhook backend, which sends events to an external HTTP API."

---

## Drafting note

The ch-08 outline caps auditing at one or two sentences in sec.2 and says the exam-relevant
fact is that it exists and what it records. This snapshot supports exactly that, plus one
better sentence than the outline expected: auditing lives **inside the kube-apiserver** and
every request generates an event at every stage of its execution. That is the same
single-door architecture stated a fourth way, and it costs one clause. The stages, the
policy levels and the backends are all above what the outline budgets -- cached for the
audit, not for the draft.

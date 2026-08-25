---
source_url: "https://kubernetes.io/docs/concepts/security/controlling-access/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/security/controlling-access.md"
fetched_at: "2026-08-24T18:55:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["api-access-gates", "authentication", "authorization", "admission-control", "admission-controller", "mutating-admission", "auditing", "api-request-stages"]
closes_gap: "ch-08 outline Open Question #2 (BLOCKING). No previously cached source stated the sequential semantics of the three gates, that admission runs after authorization and before persistence, or that admission modules may MODIFY rather than only reject. All four sub-claims are closed below."
---
# Controlling Access to the Kubernetes API

> **Extraction note.** Passages marked **[VERBATIM]** are quoted character-for-character
> from the source and are safe to cite. Headings are the source's own. A claim available
> only as an observation about the page's structure is marked **[STRUCTURAL]** and must
> not be quoted as prose.

## Overview

**[VERBATIM]**

> "Users access the Kubernetes API using `kubectl`, client libraries, or by making REST requests."

> "When a request reaches the API, it goes through several stages."

The page carries a diagram of the request path. Its alt text is **[VERBATIM]**:

> "Diagram of request handling steps for Kubernetes API request"

**[STRUCTURAL]** The page presents the stages as sequential H2 sections in this order:
Transport security, Authentication, Authorization, Admission control, Auditing.

## Transport security

**[VERBATIM]**

> "the Kubernetes API server listens on port 6443 on the first non-localhost network interface, protected by TLS."

> "you need a copy of that CA certificate configured into your `~/.kube/config`"

## Authentication

**[VERBATIM]**

> "The cluster creation script or cluster admin configures the API server to run one or more Authenticator modules."

> "The input to the authentication step is the entire HTTP request; however, it typically examines the headers and/or client certificate."

> "While Kubernetes uses usernames for access control decisions and in request logging, it does not have a `User` object."

> "If the request cannot be authenticated, it is rejected with HTTP status code 401."

## Authorization

**[VERBATIM]**

> "A request must include the username of the requester, the requested action, and the object affected by the action."

> "Kubernetes supports multiple authorization modules, such as ABAC mode, RBAC Mode, and Webhook mode."

> "if any module authorizes the request, then the request can proceed. If all of the modules deny the request, then the request is denied (HTTP status code 403)."

## Admission control

**[VERBATIM]**

> "Admission Control modules are software modules that can modify or reject requests."

> "Admission Control modules can access the contents of the object that is being created or modified."

> "When multiple admission controllers are configured, they are called in order."

> "Unlike Authentication and Authorization modules, if any admission controller module rejects, the request is immediately rejected."

> "admission controllers can also set complex defaults for fields."

> "Admission controllers act on requests that create, modify, delete, or connect to (proxy) an object. Admission controllers do not act on requests that merely read objects."

The sentence establishing persistence order -- **[VERBATIM]**:

> "Once a request passes all admission controllers, it is validated using the validation routines for the corresponding API object, and then written to the object store."

## Auditing

**[VERBATIM]**

> "Kubernetes auditing provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster."

---

## What this snapshot licenses Chapter 8 sec.2 to assert

1. The three gates are **sequential**, not parallel. The page orders them as stages of one
   request path and states the object reaches the store only after passing all admission
   controllers.
2. **Admission is the only gate that can change the request.** Authentication rejects with
   401; authorization denies with 403; admission modules "can modify or reject requests" and
   "can access the contents of the object that is being created or modified."
3. **Admission is also the only gate with unanimous-reject semantics.** Authorization is
   any-module-approves; admission is any-module-rejects. The page draws this contrast itself
   ("Unlike Authentication and Authorization modules...").
4. **Admission runs before persistence.** Validation and the write to the object store follow it.
5. Admission does not see reads. `get`, `watch` and `list` do not pass this gate.

NOT IN THIS SNAPSHOT: the mutating/validating phase split (see
`k8s-docs-admission-controllers-2026-08-24.md`), the RBAC object model, Konnectivity or
SSH tunnels (deliberately omitted -- ch-08 outline Open Question #7).

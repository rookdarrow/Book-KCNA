---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/authentication/"
fetched_at: "2026-09-04T09:25:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["user-and-group-external-identity", "authentication-plugins", "service-account-token", "jwt", "oidc"]
---
# Authenticating (kubernetes.io/docs/reference/access-authn-authz/authentication/)

Carries the authentication *mechanisms* that Ch 12 §2 names in one clause, and the two format facts the Term Ownership Ledger asks §2 to name (JWT, OIDC) without defining. Companion to `k8s-docs-service-accounts-2026-08-23.md`, which carries the ServiceAccount object and the TokenRequest recommendation.

## Users in Kubernetes

"All Kubernetes clusters have two categories of users: service accounts managed by Kubernetes, and normal users."

"In this regard, Kubernetes does not have objects which represent normal user accounts. Normal users cannot be added to a cluster through an API call."

## Authentication strategies

"Kubernetes uses client certificates, bearer tokens, or an authenticating proxy to authenticate API requests through authentication plugins."

"When multiple authenticator modules are enabled, the first module to successfully authenticate the request short-circuits evaluation."

## Authentication methods

The page's list of available methods, as headed on the page: X.509 client certificates; Bootstrap tokens; Service account tokens; Static token file; External integrations — JSON Web Tokens, OpenID Connect Tokens, Webhook token authentication, Authenticating reverse proxy.

## Service account tokens

"The created token is a signed JSON Web Token (JWT)."

## OpenID Connect tokens

"OpenID Connect is a flavor of OAuth2 supported by …" (the sentence continues by naming example providers)

"This token is a JSON Web Token (JWT) with well known fields, such as a user's …" (the sentence continues by listing the claims)

> NOTE FOR DRAFTING: the two OIDC quotations above are the openings of their sentences, verified verbatim to the ellipsis; the remainder names vendors and claim fields the chapter does not use.

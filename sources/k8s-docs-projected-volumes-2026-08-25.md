---
source_url: "https://kubernetes.io/docs/concepts/storage/projected-volumes/"
fetched_at: "2026-08-25T02:44:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["projected-volume", "secret-volume", "configmap-volume", "downwardapi-volume"]
---
# Projected Volumes (kubernetes.io/docs/concepts/storage/projected-volumes/)

Pays the chapter-05:775 debt ("Ch 11 — projected volumes"), which was dropped where
TokenRequest tokens are mounted.

## Introduction

"A `projected` volume maps several existing volume sources into the same directory."

## Volume sources that can be projected

"Currently, the following types of volume sources can be projected:

* `secret`
* `downwardAPI`
* `configMap`
* `serviceAccountToken`
* `clusterTrustBundle`
* `podCertificate`"

## serviceAccountToken projected volumes

"You can inject the token for the current service account into a Pod at a specified path."

"The `audience` field contains the intended audience of the token."

"The `expirationSeconds` is the expected duration of validity of the service account token. It defaults to 1 hour and must be at least 10 minutes (600 seconds)."

NOTE FOR §1 — the source list above is the payable form of the Ch 5 promise: the
projected volume the reader already met carrying a ServiceAccount token is the same
mechanism with `serviceAccountToken` as one of six named sources. Note also that the
current list has SIX entries (adding `clusterTrustBundle` and `podCertificate`),
whereas the cached k8s-docs-volumes-2026-08-23.md line 19 records FOUR
(secret, downwardAPI, configMap, serviceAccountToken). Prefer this file's list, or
say "several existing volume sources" and enumerate only the four the reader has met.

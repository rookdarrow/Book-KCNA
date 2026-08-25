---
source_url: "https://kubernetes.io/docs/reference/using-api/deprecation-policy/"
fetched_at: "2026-08-24T14:34:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["frozen-not-deprecated", "ga-stability-guarantee", "feature-freeze"]
---
# Kubernetes Deprecation Policy (kubernetes.io/docs/reference/using-api/deprecation-policy/)

(Fetched to close the verification flag on Ch 10 §4's third beat. This is the page the Ingress
"frozen" Note hyperlinks to when it says the Ingress API "is subject to the stability guarantees for
generally available APIs" — the anchor is #deprecating-parts-of-the-api. It supplies the formal
Kubernetes meaning of "deprecated", which the chapter contrasts against "frozen".)

## Overview

Kubernetes is a large system with many components and many contributors. As with any such software, the feature set naturally evolves over time, and sometimes a feature may need to be removed. This could include an API, a flag, or even an entire feature. To avoid breaking existing users, Kubernetes follows a deprecation policy for aspects of the system that are slated to be removed.

## Deprecating parts of the API

Since Kubernetes is an API-driven system, the API has evolved over time to reflect the evolving understanding of the problem space. The Kubernetes API is actually a set of APIs, called "API groups", and each API group is independently versioned.

The following rules govern the deprecation of elements of the API. This includes:

- REST resources (aka API objects)
- Fields of REST resources
- Annotations on REST resources, including "beta" annotations but not including "alpha" annotations.
- Enumerated or constant values
- Component config structures

These rules are enforced between official releases, not between arbitrary commits to master or release branches.

## Rules

**Rule #1: API elements may only be removed by incrementing the version of the API group.**

Once an API element has been added to an API group at a particular version, it can not be removed from that version or have its behavior significantly changed, regardless of track.

**Rule #2: API objects must be able to round-trip between API versions in a given release without information loss, with the exception of whole REST resources that do not exist in some versions.**

**Rule #3: An API version in a given track may not be deprecated in favor of a less stable API version.**

- GA API versions can replace beta and alpha API versions.
- Beta API versions can replace earlier beta and alpha API versions, but may not replace GA API versions.
- Alpha API versions can replace earlier alpha API versions, but may not replace GA or beta API versions.

**Rule #4a: API lifetime is determined by the API stability level**

- GA API versions may be marked as deprecated, but must not be removed within a major version of Kubernetes
- Beta API versions are deprecated no more than 9 months or 3 minor releases after introduction (whichever is longer), and are no longer served 9 months or 3 minor releases after deprecation (whichever is longer)
- Alpha API versions may be removed in any release without prior deprecation notice

**Rule #4b: The "preferred" API version and the "storage version" for a given group may not advance until after a release has been made that supports both the new version and the previous version**

Users must be able to upgrade to a new release of Kubernetes and then roll back to a previous release, without converting anything to the new API version or suffering breakages (unless they explicitly used features only available in the newer version).

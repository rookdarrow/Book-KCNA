---
source_url: "https://docs.docker.com/build/building/multi-stage/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["base-image", "image-layers"]
---
# Multi-stage builds — Docker documentation

## Problem solved

"Multi-stage builds are useful to anyone who has struggled to optimize Dockerfiles
while keeping them easy to read and maintain."

## Mechanism

"With multi-stage builds, you use multiple FROM statements in your Dockerfile. Each
FROM instruction can use a different base, and each of them begins a new stage of the
build."

"You can selectively copy artifacts from one stage to another, leaving behind
everything you don't want in the final image."

## What does not ship

"None of the build tools required to build the application are included in the
resulting image."

"The Go SDK and any intermediate artifacts are left behind, and not saved in the final
image."

## Scope note

Multi-stage builds are almost certainly beyond KCNA's D1.4 surface. Recorded because
G29 named them explicitly. §2 may name the technique in a clause; it should not teach
Dockerfile syntax.

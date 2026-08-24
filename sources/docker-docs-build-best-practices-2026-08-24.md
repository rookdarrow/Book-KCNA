---
source_url: "https://docs.docker.com/build/building/best-practices/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["base-image", "image-digest", "image-layers"]
---
# Building best practices — Docker documentation

> CLOSES the base-image-selection half of G29. Chapter 2 §2's ⚓ Worth Securing beat.

## Choosing a base image

"Docker Official Images are a curated collection that have clear documentation,
promote best practices, and are regularly updated."

"Verified Publisher images are high-quality images published and maintained by the
organizations partnering with Docker."

## Minimal base images — THE ⚓ WORTH SECURING SOURCE

"When building your own image from a Dockerfile, ensure you choose a minimal base image
that matches your requirements. A smaller base image not only offers portability and
fast downloads, but also shrinks the size of your image and minimizes the number of
vulnerabilities introduced through the dependencies."

"A small image with minimal dependencies can considerably lower the attack surface."

On Alpine: "tightly controlled and small in size (under 6 MB), while still being a full
Linux distribution."

## Pinning to a digest — THE §2 → §3 BRIDGE

"To fully secure your supply chain integrity, you can pin the image version to a
specific digest."

"even if the publisher updates the `3.21` tag, your builds would still use the pinned
image version."

This is a sourced hand-off from §2's base-image material to §3's tag-vs-digest Fixed
Point. It is also an independent, non-Kubernetes statement that a tag can move.

## Build cache

"Understanding how the build cache works, and how cache invalidation occurs, is
critical for ensuring faster builds."

[EXTRACTOR SUMMARY — NOT VERBATIM] The page advises always combining `RUN apt-get
update` with `apt-get install` in the same RUN statement to avoid caching stale
packages. Re-verify before quoting; out of scope for Chapter 2 regardless.

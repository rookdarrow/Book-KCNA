---
source_url: "https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "immutability", "base-image"]
---
# Understanding image layers — Docker documentation

## Composition and immutability

"container images are composed of layers. And each of these layers, once created, are
immutable."

"Each layer in an image contains a set of filesystem changes - additions, deletions,
or modifications."

## Reuse and dedup — SOUNDINGS Q4 ANSWER KEY

"This is beneficial because it allows layers to be reused between images."

Reuse makes "builds faster and reduce the amount of storage and bandwidth required to
distribute the images."

## Union filesystem — DEPTH

"When you run a container from an image, a union filesystem is created where layers are
stacked on top of each other, creating a new and unified view."

"When the union filesystem is created, in addition to the image layers, a directory is
created specifically for the running container. This allows the container to make
filesystem changes while allowing the original image layers to remain untouched."

The second sentence is a strong, sourced support for §2's immutability argument: the
image layers are never mutated even by a running container.

## Layer ordering

[EXTRACTOR SUMMARY — NOT VERBATIM] The page demonstrates ordering with a five-layer
example, showing later layers (application code) depending on foundational layers
(the runtime). Re-verify before quoting.

---
source_url: "https://raw.githubusercontent.com/opencontainers/image-spec/main/spec.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Image Format Specification"
objectives_covered: ["D1.4"]
concepts_covered: ["oci-image-spec", "image-layers", "image-digest", "container-image"]
---
# OCI Image Format Specification — overview

## What the specification defines

"This specification defines an OCI Image, consisting of an image manifest, an image
index (optional), a set of filesystem layers, and a configuration."

## Understanding the specification — the components

- "Image Manifest - a document describing the components that make up a container image"
- "Image Index - an annotated list of manifests"
- "Image Layout - a filesystem layout representing the contents of an image"
- "Filesystem Layer - a changeset that describes a container's filesystem"
- "Image Configuration - a document determining layer ordering and configuration of
  the image suitable for translation into a runtime bundle"

## How they fit together

"At a high level the image manifest contains metadata about the contents and
dependencies of the image including the content-addressable identity of one or more
filesystem layer changeset archives that will be unpacked to make up the final
runnable filesystem. The image configuration includes information such as application
arguments, environments, etc. The image index is a higher-level manifest which points
to a list of manifests and descriptors."

## Note for §5

"suitable for translation into a runtime bundle" is the spec's own link from
image-spec to runtime-spec. See oci-runtime-spec-bundle-2026-08-24.md.

---
source_url: "https://raw.githubusercontent.com/opencontainers/image-spec/main/manifest.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Image Format Specification, Image Manifest"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "image-digest", "base-image", "oci-image-spec"]
---
# OCI Image Manifest Specification

## Stated goals

"content-addressable images, by supporting an image model where the image's
configuration can be hashed to generate a unique ID for the image and its components"

The manifest is also to be "translatable to the OCI Runtime Specification".

[EXTRACTOR SUMMARY — NOT VERBATIM] A third goal concerns multi-architecture images
via a "fat manifest" referencing platform-specific image manifests. Re-verify before
citing.

## Required fields

- schemaVersion: "This REQUIRED property specifies the image manifest schema version.
  For this version of the specification, this MUST be `2`"
- config: "This REQUIRED property references a configuration object for a container,
  by digest"
- layers: "Each item in the array MUST be a descriptor"
- mediaType: "the media type `application/vnd.oci.image.manifest.v1+json`"

## Layer ordering — ch02-fig02 SOURCE

"The final filesystem layout MUST match the result of applying the layers to an empty
directory."

"The array MUST have the base layer at index 0. Subsequent layers MUST then follow in
stack order."

## Note for §2 and §3

"content-addressable images … the image's configuration can be hashed to generate a
unique ID" is the standards-body statement of the identity half of Fixed Point #1.
Corroborates k8s-docs-images' "a hash of the image's content" independently.

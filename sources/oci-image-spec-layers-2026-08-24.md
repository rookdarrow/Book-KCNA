---
source_url: "https://raw.githubusercontent.com/opencontainers/image-spec/main/layer.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Image Format Specification, Image Layer Filesystem Changeset"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "oci-image-spec"]
---
# OCI Image Layer Filesystem Changeset

> CLOSES THE OPEN HALF OF G29 (layer mechanics). Chapter 2 §2 and ch02-fig02.

## What a layer is

"This document describes how to serialize a filesystem and filesystem changes like
removed files into a blob called a layer. One or more layers are applied on top of
each other to create a complete filesystem."

## Change types

"Types of changes that can occur in a changeset are: Additions, Modifications,
Removals. Additions and Modifications are represented the same in the changeset tar
archive."

## Tar archives and media types

"Layer Changesets for the media type `application/vnd.oci.image.layer.v1.tar` MUST be
packaged in tar archive."

"Layer Changesets for the media type `application/vnd.oci.image.layer.v1.tar` MUST NOT
include duplicate entries for file paths in the resulting tar archive."

"The media type `application/vnd.oci.image.layer.v1.tar+gzip` represents an
`application/vnd.oci.image.layer.v1.tar` payload which has been compressed with gzip."

## Applying changesets

"Layer Changesets of media type `application/vnd.oci.image.layer.v1.tar` are applied,
rather than simply extracted as tar archives. Applying a layer changeset requires
special consideration for the whiteout files."

## Whiteout files — DEPTH, likely out of scope

"A whiteout file is an empty file with a special filename that signifies a path should
be deleted. A whiteout filename consists of the prefix `.wh.` plus the basename of the
path to be deleted."

Below KCNA's waterline. Suitable for a 🔭 Closer Look at most; cut without regret.

---
source_url: "https://raw.githubusercontent.com/opencontainers/runtime-spec/main/bundle.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Runtime Specification, Filesystem Bundle"
objectives_covered: ["D1.4"]
concepts_covered: ["filesystem-bundle", "oci-runtime-spec"]
---
# OCI Runtime Specification — Filesystem Bundle

## Definition

A filesystem bundle is "a set of files organized in a certain way, and containing all
the necessary data and metadata for any compliant runtime to perform all standard
operations against it."

## Required contents of a Standard Container bundle

config.json — "contains configuration data. This REQUIRED file MUST reside in the root
of the bundle directory and MUST be named `config.json`."

A root filesystem — the directory referenced by `root.path` in config.json, when that
property is set.

## Storage structure

"while these artifacts MUST all be present in a single directory on the local
filesystem, that directory itself is not part of the bundle."

## Note for §5

Previously `filesystem-bundle` rested only on oci-overview's phrase "a 'filesystem
bundle' that is unpacked on disk". §5's download → unpack → run flow now has a defined
middle artifact.

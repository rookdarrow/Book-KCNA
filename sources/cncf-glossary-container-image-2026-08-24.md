---
source_url: "https://glossary.cncf.io/container-image/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (EXAM AUTHORITY)"
objectives_covered: ["D1.4"]
concepts_covered: ["container-image", "immutability", "registry", "oci"]
---
# Container Image — CNCF Cloud Native Glossary

## What it is

"A container image is an immutable, static file containing the dependencies for the
creation of a container."

Contents named: "a single executable binary file, system libraries, system tools,
environment variables, and other required platform settings."

## Problem it addresses

"application servers are configured per environment, and applications are deployed to
them. Any misconfiguration between environments is problematic and often leads to
downtime or failed deployments."

## How it helps

"Container images bundle an application with any of its runtime dependencies, such as
an application server. This provides consistency across all environments, including a
developer's machine."

"container images can be used to instantiate as many containers as needed, allowing for
greater scalability."

## OCI conformance — §5 SUPPORT FROM THE AUTHORITY

Images "must follow the standard schema defined by the Open Container Initiative (OCI)."

## ⚠ DO NOT QUOTE THIS SENTENCE

The page also states that images are "typically stored in container registries, where
they can be downloaded and run as an isolated process using a Container Runtime
Interface (CRI)."

That is loose: CRI is the kubelet-to-runtime protocol, not the thing that runs an
image. It blurs precisely the boundary §5 exists to draw — and it comes from the exam
authority's own glossary. Use this page for the IMAGE DEFINITION only. Source CRI from
k8s-docs-cri-2026-08-24.md.

## Note for trap #30

The contents list here does NOT include a kernel, which supports §2's negative-space
argument. But no source in the cache states verbatim that "an image does not contain a
kernel." B1 tags trap #30 as [source]; treat it as ENTAILED from the kernel-sharing
statement in A13, not as a quotable fact.

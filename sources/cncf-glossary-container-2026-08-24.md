---
source_url: "https://glossary.cncf.io/container/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (EXAM AUTHORITY)"
objectives_covered: ["D1.4"]
concepts_covered: ["container", "shared-kernel-isolation"]
---
# Containers — CNCF Cloud Native Glossary

> Note the slug: /container/ (singular). /containers/ returns 404.
> This is the EXAM AUTHORITY's own definition. Weight accordingly.

## What it is

"A container is a running process with resource and capability constraints managed by
a computer's operating system."

## Problem it addresses

"Before containers were available, separate machines were necessary to run
applications. Each machine would require its own operating system, which takes CPU,
memory, and disk space, all for an individual application to function."

## How it helps

"Containers share the same operating system and its machine resources, spreading the
operating system's resource overhead and creating efficient use of the physical
machine."

## The isolation caveat — §7 SETUP

"Since containers share the same operating system, processes can be considered less
secure than alternatives."

This is the exam authority stating §1's tradeoff and §7's motivation in one sentence.
Strong support for the ⚓ Worth Securing beat in §1 ("relaxed isolation is a tradeoff,
not a deficiency") and for §7's existence.

## Absence noted

The extractor confirmed this page contains no direct sentence comparing containers to
virtual machines. For the VM contrast use k8s-docs-overview-2026-08-23.md,
cncf-glossary-containerization-2026-08-24.md, or
docker-docs-what-is-a-container-2026-08-24.md.

## Wording — see A13's note

This page says OPERATING SYSTEM, not kernel.

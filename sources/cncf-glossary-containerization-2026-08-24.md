---
source_url: "https://glossary.cncf.io/containerization/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (EXAM AUTHORITY)"
objectives_covered: ["D1.4"]
concepts_covered: ["container-vs-virtual-machine", "container-image", "immutability"]
---
# Containerization — CNCF Cloud Native Glossary

## What it is

"Containerization is the process of packaging of application code including libraries
and dependencies required to run the code into a single lightweight executable—called
container image."

## Problem it addresses

[EXTRACTOR SUMMARY — NOT VERBATIM. Re-verify before quoting any of this paragraph.]
Before containers, organizations used virtual machines on bare-metal hardware. VMs are
substantially larger than containers and need a hypervisor. VM template creation,
storage, and transfer are slow processes. Additionally, VMs can experience
configuration drift, violating immutability principles.

## How it helps

Container images are lightweight compared to traditional VMs. The containerization
process uses a dependency file that can be version controlled with automated builds.
Each container image has a unique identifier tied to its exact content and
configuration.

Verbatim fragment: when containers are scheduled and rescheduled, "they are always
reset to their initial state which eliminates configuration drift."

## Note for §2

The configuration-drift framing is the exam authority's own statement of WHY
immutability matters — the strongest available support for the chapter's organizing
principle. Pair with k8s-docs-containers' "build a new image … then recreate the
container" rule.

## ⚠ SCOPE BOUNDARY WITH CHAPTER 3

The "Problem it addresses" paragraph frames the pre-container world as VMs on bare
metal with a hypervisor. That is adjacent to Chapter 3's deployment-eras material
(B2 assigns the three eras and ch03-fig03 to Chapter 3). §1 may use this for the
ARCHITECTURAL contrast only. Do not narrate the timeline.

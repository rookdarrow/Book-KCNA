---
source_url: "https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["container", "shared-kernel-isolation", "container-vs-virtual-machine"]
---
# What is a container? — Docker documentation

> RESOLVES CHAPTER 2 OPEN QUESTION #1 and the live AUTHOR-REVIEW comment at
> chapter-01-taking-departure.md line 140. This is the source for the "kernel"
> sharpening. Read the wording note at the bottom before drafting §1.

## Definition

"Containers are isolated processes for each of your app's components."

"A container is simply an isolated process with all of the files it needs to run."

## What containers share — THE KERNEL SENTENCE

"If you run multiple containers, they all share the same kernel, allowing you to run
more applications on less infrastructure."

## The VM contrast

"A VM is an entire operating system with its own kernel, hardware drivers, programs,
and applications."

"Spinning up a VM only to isolate a single application is a lot of overhead."

## WORDING NOTE — READ BEFORE DRAFTING §1

Three authorities, two registers, no factual conflict:

  KERNEL  — this page (Docker, vendor): "they all share the same kernel"
  OS      — glossary.cncf.io/container/ (CNCF, THE EXAM AUTHORITY):
            "Containers share the same operating system and its machine resources"
  OS      — kubernetes.io/docs/concepts/overview/ (Kubernetes, vendor):
            "relaxed isolation properties to share the Operating System (OS)"

"Share the kernel" is the mechanism; "share the OS" is the looser formulation the exam
authority uses. Teach the mechanism, but ensure the reader recognizes OS phrasing on
the exam.

Internal corroboration already in cache: k8s-docs-runtime-class-2026-08-23.md says a
sandboxed runtime uses "a user-space kernel (such as gVisor)" — which presupposes that
the ordinary case is the HOST's kernel. §1 and §7 can agree on this without leaving
the cache.

DO NOT let Chapter 1 and Chapter 2 diverge on this sentence. The reconcile pass will
surface a mismatch.

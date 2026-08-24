---
source_url: "https://kubernetes.io/blog/2022/02/17/dockershim-faq/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Kubernetes project (official project blog) — published 2022-02-17"
objectives_covered: ["D1.4"]
concepts_covered: ["cri", "containerd", "oci", "container-runtime"]
---
# Dockershim Removal FAQ — Kubernetes project blog

> HISTORICAL DOCUMENT, dated 2022-02-17. Authoritative (Kubernetes project
> publication) but NOT current documentation. Do not present dockershim as current.
> Serves Chapter 2 Soundings Q5, §4's Snag, and B1 trap #34.

## Why "Docker" looks like the runtime

"Early versions of Kubernetes only worked with a specific container runtime: Docker
Engine. Later, Kubernetes added support for working with other container runtimes.
The CRI standard was created to enable interoperability between orchestrators (like
Kubernetes) and many different container runtimes. Docker Engine doesn't implement
that interface (CRI), so the Kubernetes project created special code to help with the
transition, and made that dockershim code part of Kubernetes itself."

"The dockershim code was always intended to be a temporary solution (hence the name:
shim)."

## Docker is not the ecosystem

"Docker popularized the Linux containers pattern and has been instrumental in
developing the underlying technology, however containers in Linux have existed for a
long time. The container ecosystem has grown to be much broader than just Docker.
Standards like OCI and CRI have helped many tools grow and thrive in our ecosystem,
some replacing aspects of Docker while others enhance existing functionality."

## Images built with Docker still run — SOUNDINGS Q5 ANSWER KEY LINE

"Yes, the images produced from `docker build` will work with all CRI implementations.
All your existing images will still work exactly the same."

## Why dockershim was removed

"In fact, maintaining dockershim had become a heavy burden on the Kubernetes
maintainers."

"Additionally, features that were largely incompatible with the dockershim, such as
cgroups v2 and user namespaces are being implemented in these newer CRI runtimes.
Removing the dockershim from Kubernetes allows further development in those areas."

## FRAMING CONSTRAINT (unchanged)

B1 trap #34 remains [inferred] AS TO EXAM FREQUENCY. Nothing on this page speaks to
how often the exam tests it. Write "easy to confuse", never "frequently tested".
What this page DOES license is describing the confusion as documented and
historically grounded rather than merely asserted.

## SCOPE GUARD

B2 assigns the historical deployment progression to Chapter 3. Chapter 2 gets one
Snag and one Soundings answer line from this page. Not a history section.

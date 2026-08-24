---
source_url: "https://opencontainers.org/about/overview/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Open Container Initiative (Linux Foundation)"
objectives_covered: ["D1 Containerization"]
concepts_covered: ["oci", "runtime-spec", "image-spec", "distribution-spec", "runc"]
---
# Open Container Initiative — Overview (opencontainers.org/about/overview/)

The Open Container Initiative is an open governance structure for the express purpose of creating open industry standards around container formats and runtimes. Established in June 2015 by Docker and other leaders in the container industry, the OCI currently contains three specifications:
- the Runtime Specification (runtime-spec) — outlines how to run a "filesystem bundle" that is unpacked on disk;
- the Image Specification (image-spec) — defines the OCI Image Format, which encompasses the image manifest, filesystem layer serialization, and image configuration needed to launch applications on target platforms;
- the Distribution Specification (distribution-spec) — reached v1.0 in May 2020 and was introduced to OCI as an effort to standardize the API to distribute container images.

At a high level an OCI implementation would download an OCI Image then unpack that image into an OCI Runtime filesystem bundle. At this point the OCI Runtime Bundle would be run by an OCI Runtime. Docker donated its container runtime, runC, to the OCI to serve as the cornerstone of this new effort.

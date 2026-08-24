---
source_url: "https://docs.docker.com/build/cache/"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Docker Inc. — official product documentation"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "base-image"]
---
# Docker build cache — Docker documentation

## Instructions map to layers

"Each instruction in this Dockerfile translates to a layer in your final image."

## Invalidation

"Whenever a layer changes, that layer will need to be re-built."

"If a layer changes, all other layers that come after it are also affected."

"Once a layer changes, then all downstream layers need to be rebuilt as well."

## Note for §2

This is the sourced warrant for the outline's claim that "the order of build steps has
consequences." Ordering guidance itself is NOT on this page — the extractor confirmed
it links out to separate "Optimize build cache" and "Cache invalidation" pages that
were not fetched. Do not attribute ordering advice to this URL; for ordering see
docker-docs-build-best-practices-2026-08-24.md.

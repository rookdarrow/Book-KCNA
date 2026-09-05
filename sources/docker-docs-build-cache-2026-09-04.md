---
source_url: "https://docs.docker.com/build/cache/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Docker Inc. — official product documentation, 'Docker build cache' (how the build cache works)"
objectives_covered: ["D1.4"]
concepts_covered: ["image-layers", "build-cache", "base-image"]
---

# Docker build cache — how a layer change propagates

Verbatim passages, section "How the build cache works":

"If a layer changes, all other layers that come after it are also affected."

"Once a layer changes, then all downstream layers need to be rebuilt as well."

What this supports in the book: Chapter 2 §2's third layer consequence, "Position in the stack determines rebuild cost" — changing a lower layer invalidates everything above it. The page does not itself state the ordering advice (put the least-changing content lowest); that sentence stays in the author's voice as "the conventional advice".

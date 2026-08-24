---
source_url: "https://buildpacks.io/docs/for-app-developers/concepts/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Cloud Native Buildpacks (CNCF graduated)"
objectives_covered: ["D1 Containerization", "D3 Application Delivery"]
concepts_covered: ["buildpacks", "builder", "base-image", "lifecycle", "detect", "build", "export", "oci-image"]
---
# Cloud Native Buildpacks — concepts (buildpacks.io)

A buildpack is software that transforms application source code into runnable artifacts by analyzing the code and determining the best way to build it. A builder is an OCI image containing an ordered combination of buildpacks and a build-time base image, a lifecycle binary, and a reference to a runtime base image. Base images: the build image is the environment in which the buildpacks run; the run image is the base for the final application image; the pairing is the stack. The platform (for example the pack CLI, or a CI system) orchestrates the process by invoking the lifecycle binary together with buildpacks and app source code to produce a runnable OCI image. The lifecycle runs in phases — detect (determine which buildpacks apply), build (compile and assemble the application), export (create the final OCI image with reproducible layers). Cloud Native Buildpacks is a Cloud Native Computing Foundation graduated project.

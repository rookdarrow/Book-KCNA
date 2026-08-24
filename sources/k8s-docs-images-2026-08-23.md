---
source_url: "https://kubernetes.io/docs/concepts/containers/images/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Containerization"]
concepts_covered: ["container-image", "registry", "image-tag", "image-digest", "latest-tag", "imagepullpolicy", "imagepullbackoff", "private-registry", "imagepullsecrets"]
---
# Images (kubernetes.io/docs/concepts/containers/images/)

A container image represents binary data that encapsulates an application and all its software dependencies. Container images are executable software bundles that can run standalone and that make very well defined assumptions about their runtime environment. You typically create a container image of your application and push it to a registry before referring to it in a Pod.

## Image names
Container images are usually given a name such as pause, example/mycontainer, or kube-apiserver. Images can also include a registry hostname; for example: fictional.registry.example/imagename, and possibly a port number as well. If you don't specify a registry hostname, Kubernetes assumes that you mean the Docker public registry. After the image name part you can add a tag or digest. Tags let you identify different versions of the same series of images. Digests are a unique identifier for a specific version of an image — a hash of the image's content — and are immutable; tags can be moved to point to different images. If you don't specify a tag, Kubernetes assumes you mean the tag latest. Examples: busybox is equivalent to docker.io/library/busybox:latest; registry.k8s.io/pause:3.5; registry.k8s.io/pause@sha256:1ff6…

Caution: you should avoid using the :latest tag when deploying containers in production as it is harder to track which version of the image is running and more difficult to roll back properly. Instead, specify a meaningful tag such as v1.42.0 and/or a digest.

## Updating images — imagePullPolicy
IfNotPresent — the image is pulled only if it is not already present locally. Always — every time the kubelet launches a container, the kubelet queries the container image registry to resolve the name to an image digest; if the kubelet has a container image with that exact digest cached locally, it uses its cached image; otherwise it pulls the image with the resolved digest. Never — the kubelet does not try fetching the image; if the image is somehow already present locally, the kubelet attempts to start the container, otherwise startup fails.

Default imagePullPolicy: if you omit imagePullPolicy and specify a digest — IfNotPresent; if the tag is :latest — Always; if no tag is specified — Always; if a tag other than :latest is specified — IfNotPresent. Once a Pod is created, imagePullPolicy is not updated if the image's tag or digest changes later.

## ImagePullBackOff
When a kubelet starts creating containers for a Pod using a container runtime, it might be possible the container is in Waiting state because of ImagePullBackOff. The ImagePullBackOff status means that a container could not start because Kubernetes could not pull a container image (for reasons such as invalid image name, or pulling from a private registry without an imagePullSecret). The BackOff part indicates that Kubernetes will keep trying to pull the image, with an increasing back-off delay, up to a compiled-in limit of 300 seconds (5 minutes).

## Using a private registry
Private registries may require keys to read images from them. Credentials can be provided by: configuring nodes to authenticate to a private registry; a kubelet credential provider to dynamically fetch credentials; pre-pulled images; specifying imagePullSecrets on a Pod (a Secret of type kubernetes.io/dockerconfigjson); vendor-specific or local extensions.

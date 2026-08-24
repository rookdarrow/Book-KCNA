---
source_url: "https://kubernetes.io/docs/concepts/configuration/configmap/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D3 Application Delivery"]
concepts_covered: ["configmap", "environment-variables", "volume-mount", "immutable-configmap", "decoupling-configuration"]
---
# ConfigMaps (kubernetes.io/docs/concepts/configuration/configmap/)

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume. A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.

Caution: ConfigMap does not provide secrecy or encryption. If the data you want to store are confidential, use a Secret rather than a ConfigMap, or use additional (third party) tools to keep your data private.

## Motivation
Use a ConfigMap for setting configuration data separately from application code. For example, imagine that you are developing an application that you can run on your own computer (for development) and in the cloud (to handle real traffic). You write the code to look in an environment variable named DATABASE_HOST. Locally, you set that variable to localhost. In the cloud, you set it to refer to a Kubernetes Service that exposes the database component to your cluster.

Note: A ConfigMap is not designed to hold large chunks of data. The data stored in a ConfigMap cannot exceed 1 MiB. If you need to store settings that are larger than this limit, you may want to consider mounting a volume or use a separate database or file service.

## ConfigMaps and Pods
The Pod and the ConfigMap must be in the same namespace. There are four different ways that you can use a ConfigMap to configure a container inside a Pod: inside a container command and args; environment variables for a container; add a file in read-only volume, for the application to read; write code to run inside the Pod that uses the Kubernetes API to read a ConfigMap. For the first three methods, the kubelet uses the data from the ConfigMap when it launches container(s) for a Pod. The fourth method lets the application subscribe to updates whenever the ConfigMap changes.

## Immutable ConfigMaps
Starting from v1.19 you can add an immutable field to a ConfigMap definition to create an immutable ConfigMap. Once a ConfigMap is marked as immutable, it is not possible to revert this change nor to mutate the contents of the data or the binaryData field. You can only delete and recreate the ConfigMap.

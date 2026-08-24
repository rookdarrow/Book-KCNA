---
source_url: "https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["custom-resource", "crd", "customresourcedefinition", "declarative-api", "api-aggregation"]
---
# Custom Resources (kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)

A resource is an endpoint in the Kubernetes API that stores a collection of API objects of a certain kind; for example, the built-in pods resource contains a collection of Pod objects. A custom resource is an extension of the Kubernetes API that is not necessarily available in a default Kubernetes installation. It represents a customization of a particular Kubernetes installation. However, many core Kubernetes functions are now built using custom resources, making Kubernetes more modular. Custom resources can appear and disappear in a running cluster through dynamic registration, and cluster admins can update custom resources independently of the cluster itself. Once a custom resource is installed, users can create and access its objects using kubectl, just as they do for built-in resources like Pods.

## Custom controllers
On their own, custom resources let you store and retrieve structured data. When you combine a custom resource with a custom controller, custom resources provide a true declarative API. The Kubernetes declarative API enforces a separation of responsibilities. You declare the desired state of your resource. The Kubernetes controller keeps the current state of Kubernetes objects in sync with your declared desired state. This is in contrast to an imperative API, where you instruct a server what to do. You can deploy and update a custom controller on a running cluster, independently of the cluster's lifecycle. The Operator pattern combines custom resources and custom controllers.

## CustomResourceDefinitions
The CustomResourceDefinition API resource allows you to define custom resources. Defining a CRD object creates a new custom resource with a name and schema that you specify. The Kubernetes API serves and handles the storage of your custom resource. This frees you from writing your own API server to handle the custom resource, but the generic nature of the implementation means you have less flexibility than with API server aggregation.

Consider a custom resource / API aggregation if your API is declarative, you want kubectl and dashboard support, your resources are naturally cluster- or namespace-scoped, and you want to reuse Kubernetes API support features; prefer a stand-alone API if your API does not fit the declarative model or you already have a program that serves it.

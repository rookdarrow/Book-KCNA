---
source_url: "https://kubernetes.io/docs/concepts/overview/working-with-objects/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts"]
concepts_covered: ["kubernetes-object", "record-of-intent", "spec", "status", "apiversion", "kind", "metadata", "manifest", "kubectl-apply"]
---
# Objects in Kubernetes (kubernetes.io/docs/concepts/overview/working-with-objects/)

Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Specifically, they can describe: what containerized applications are running (and on which nodes); the resources available to those applications; the policies around how those applications behave, such as restart policies, upgrades, and fault-tolerance.

A Kubernetes object is a "record of intent" — once you create the object, the Kubernetes system will constantly work to ensure that the object exists. By creating an object, you're effectively telling the Kubernetes system what you want your cluster's workload to look like; this is your cluster's desired state. To work with Kubernetes objects — whether to create, modify, or delete them — you'll need to use the Kubernetes API. When you use the kubectl command-line interface, for example, the CLI makes the necessary Kubernetes API calls for you.

## Object spec and status
Almost every Kubernetes object includes two nested object fields that govern the object's configuration: the object spec and the object status. For objects that have a spec, you have to set this when you create the object, providing a description of the characteristics you want the resource to have: its desired state. The status describes the current state of the object, supplied and updated by the Kubernetes system and its components. The Kubernetes control plane continually and actively manages every object's actual state to match the desired state you supplied.

For example: in Kubernetes, a Deployment is an object that can represent an application running on your cluster. When you create the Deployment, you might set the Deployment spec to specify that you want three replicas of the application to be running. The Kubernetes system reads the Deployment spec and starts three instances of your desired application — updating the status to match your spec. If any of those instances should fail (a status change), the Kubernetes system responds to the difference between spec and status by making a correction — in this case, starting a replacement instance.

## Describing a Kubernetes object
When you create an object in Kubernetes, you must provide the object spec that describes its desired state, as well as some basic information about the object (such as a name). Most often, you provide the information to kubectl in a file known as a manifest. By convention, manifests are YAML. In the manifest file for the Kubernetes object you want to create, you'll need to set values for the following fields: apiVersion — which version of the Kubernetes API you're using to create this object; kind — what kind of object you want to create; metadata — data that helps uniquely identify the object, including a name string, UID, and optional namespace; spec — what state you desire for the object. Apply a manifest with `kubectl apply -f <manifest>`.

Related object concepts: Namespaces (isolate groups of resources within a single cluster); Labels and Selectors (key/value pairs to identify and organize objects); Annotations (non-identifying metadata); Field Selectors; Finalizers (control object deletion).

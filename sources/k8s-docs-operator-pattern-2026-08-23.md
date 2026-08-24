---
source_url: "https://kubernetes.io/docs/concepts/extend-kubernetes/operator/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["operator-pattern", "custom-controller", "custom-resource", "automation"]
---
# Operator pattern (kubernetes.io/docs/concepts/extend-kubernetes/operator/)

## Motivation
The operator pattern aims to capture the key aim of a human operator who is managing a service or set of services. Human operators who look after specific applications and services have deep knowledge of how the system ought to behave, how to deploy it, and how to react if there are problems. People who run workloads on Kubernetes often like to use automation to take care of repeatable tasks. The operator pattern captures how you can write code to automate a task beyond what Kubernetes itself provides.

## Operators in Kubernetes
Kubernetes is designed for automation. Out of the box, you get lots of built-in automation from the core of Kubernetes. You can use Kubernetes to automate deploying and running workloads, and you can automate how Kubernetes does that. Kubernetes' operator pattern concept lets you extend the cluster's behaviour without modifying the code of Kubernetes itself by linking controllers to one or more custom resources. Operators are clients of the Kubernetes API that act as controllers for a Custom Resource.

## An example operator
Things you can use an operator to automate: deploying an application on demand; taking and restoring backups of that application's state; handling upgrades of the application code alongside related changes such as database schemas or extra configuration settings; publishing a Service to applications that don't support Kubernetes APIs to discover them; simulating failure in all or part of your cluster to test its resilience; choosing a leader for a distributed application without an internal member election process. Example shape: a custom resource named SampleDB; a Deployment that makes sure a Pod is running that contains the controller part of the operator; a container image of the operator code; controller code that queries the control plane to find out what SampleDB resources are configured; code to tell the API server how to make reality match the configured resources (creating PVCs, a StatefulSet and a Job when a SampleDB is added; snapshotting and cleaning up when it is deleted; scheduling backups; upgrading old versions).

## Deploying and using operators
The most common way to deploy an operator is to add the Custom Resource Definition and its associated Controller to your cluster. The Controller will normally run outside of the control plane, much as you would run any containerized application — for example, as a Deployment. Once you have an operator deployed, you'd use it by adding, modifying or deleting the kind of resource that the operator uses (`kubectl get SampleDB`, `kubectl edit SampleDB/example-database`); the operator takes care of applying the changes as well as keeping the existing service in good shape.

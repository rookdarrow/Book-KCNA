---
source_url: "https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts"]
concepts_covered: ["labels", "label-selectors", "equality-based-selector", "set-based-selector", "annotations", "matchlabels", "matchexpressions"]
---
# Labels and Selectors (kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

Labels are key/value pairs that are attached to objects such as Pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system. Labels can be used to organize and to select subsets of objects. Labels can be attached to objects at creation time and subsequently added and modified at any time. Each object can have a set of key/value labels defined. Each Key must be unique for a given object. Labels allow for efficient queries and watches and are ideal for use in UIs and CLIs. Non-identifying information should be recorded using annotations.

## Motivation
Labels enable users to map their own organizational structures onto system objects in a loosely coupled fashion, without requiring clients to store these mappings. Example labels: "release" : "stable" / "canary"; "environment" : "dev" / "qa" / "production"; "tier" : "frontend" / "backend" / "cache"; "partition" : "customerA" / "customerB"; "track" : "daily" / "weekly".

## Syntax and character set
Labels are key/value pairs. Valid label keys have two segments: an optional prefix and name, separated by a slash (/). The name segment is required and must be 63 characters or less, beginning and ending with an alphanumeric character with dashes, underscores, dots, and alphanumerics between. The prefix is optional; if specified, it must be a DNS subdomain no longer than 253 characters, followed by a slash. The kubernetes.io/ and k8s.io/ prefixes are reserved for Kubernetes core components. Valid label values must be 63 characters or less (can be empty).

## Label selectors
Via a label selector, the client/user can identify a set of objects. The label selector is the core grouping primitive in Kubernetes. The API currently supports two types of selectors: equality-based (=, ==, !=; e.g. environment = production, tier != frontend) and set-based (in, notin, exists; e.g. environment in (production, qa), tier notin (frontend, backend), partition, !partition). Set-based requirements are more expressive than equality-based; multiple requirements are ANDed with commas. Newer resources such as Job, Deployment, ReplicaSet, and DaemonSet support set-based requirements via matchLabels and matchExpressions; matchLabels is a map of {key,value} pairs equivalent to matchExpressions with operator In.

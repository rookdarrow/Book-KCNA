---
source_url: "https://kubernetes.io/docs/concepts/architecture/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1 Core Concepts", "D1 Administration"]
concepts_covered: ["control-plane", "worker-nodes", "kubelet", "kube-proxy", "container-runtime", "controllers", "cloud-controller-manager"]
---
# Cluster Architecture (kubernetes.io/docs/concepts/architecture/)

A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes, that run containerized applications. Every cluster needs at least one worker node in order to run Pods. The worker node(s) host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

## Control plane components
The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a Deployment's replicas field is unsatisfied).
- **kube-apiserver** — The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane. kube-apiserver is designed to scale horizontally — that is, it scales by deploying more instances. You can run several instances of kube-apiserver and balance traffic between those instances.
- **etcd** — Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data. If your Kubernetes cluster uses etcd as its backing store, make sure you have a back up plan for the data.
- **kube-scheduler** — Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on. Factors taken into account for scheduling decisions include: individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines.
- **kube-controller-manager** — Control plane component that runs controller processes. Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process. There are many different types of controllers, for example: Node controller (noticing and responding when nodes go down); Job controller (watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion); EndpointSlice controller (populates EndpointSlice objects to provide a link between Services and Pods); ServiceAccount controller (creates default ServiceAccounts for new namespaces).
- **cloud-controller-manager** — A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster. The cloud-controller-manager only runs controllers that are specific to your cloud provider. If you are running Kubernetes on your own premises, or in a learning environment inside your own PC, the cluster does not have a cloud controller manager.

## Node components
Node components run on every node, maintaining running pods and providing the Kubernetes runtime environment.
- **kubelet** — An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod. The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. The kubelet doesn't manage containers which were not created by Kubernetes.
- **kube-proxy (optional)** — kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept. kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster. If you use a network plugin that implements packet forwarding for Services by itself, and providing equivalent behavior to kube-proxy, then you do not need to run kube-proxy on the nodes in your cluster.
- **Container runtime** — A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment. Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI (Container Runtime Interface).

Related architecture topics on the same page: Nodes; Communication between Nodes and the Control Plane; Controllers (control loops); Leases; Cloud Controller Manager; About cgroup v2; Container Runtime Interface (CRI); Garbage Collection; Mixed Version Proxy.

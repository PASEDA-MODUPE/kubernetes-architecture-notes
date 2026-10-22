Kubernetes Architecture Notes

Overview

This project documents my learning of Kubernetes architecture, including the control plane, worker node components, and how Kubernetes creates and manages Pods.

Learning Objectives

* Understand Kubernetes cluster architecture.
* Identify the main control plane components and their responsibilities.
* Explain the worker node components.
* Understand the Pod creation workflow.
* Practise writing a Kubernetes Pod manifest.

Control Plane Components

* kube-apiserver: Handles Kubernetes API requests.
* etcd: Stores Kubernetes cluster data.
* kube-scheduler: Selects a suitable worker node for an unscheduled Pod.
* kube-controller-manager: Runs controllers that help maintain the desired state.
* cloud-controller-manager: Integrates Kubernetes with cloud-specific services when required.

Worker Node Components

* kubelet: Ensures assigned Pods run according to their specifications.
* Container runtime: Runs containers, for example, containerd or CRI-O.
* kube-proxy: Helps implement Service networking when used.

Pod Creation Workflow

1. Submit a Pod manifest using kubectl.
2. The API server validates and processes the request.
3. The Pod object is stored in etcd.
4. The scheduler selects a suitable worker node.
5. The scheduler records the node assignment through the API server.
6. The kubelet on that node works to ensure the Pod runs.
7. The container runtime creates and starts the container.
8. The kubelet reports the Pod status through the API server.

Project Files

* docs/kubernetes-architecture.md — Detailed architecture notes.
* diagrams/kubernetes-architecture.png — Architecture diagram.
* examples/pod.yaml — Example Pod manifest.

Official References

* Kubernetes Architecture
* Kubernetes Components
* Kubernetes Nodes
* Kubernetes Pods

Author

Modupe Paseda

Cloud and DevOps Learning Project
Kubernetes Architecture Notes

Overview

This project documents my learning of Kubernetes architecture, including the Control Plane, Worker Node components, and how Kubernetes creates and manages Pods.

Learning Objectives

* Understand Kubernetes cluster architecture.
* Identify the main Control Plane components and their responsibilities.
* Explain the Worker Node components.
* Understand the Pod creation workflow.
* Practise writing a Kubernetes Pod manifest.

Control Plane Components

* kube-apiserver: Handles Kubernetes API requests and coordinates communication between cluster components.
* etcd: Stores Kubernetes cluster data and state.
* kube-scheduler: Selects a suitable Worker Node for an unscheduled Pod.
* kube-controller-manager: Runs controllers that help maintain the desired state.
* cloud-controller-manager: Integrates Kubernetes with cloud-specific services when required.

Worker Node Components

* kubelet: Ensures assigned Pods run according to their specifications.
* Container runtime: Runs containers, for example, containerd or CRI-O.
* kube-proxy: Helps implement Service networking when used.
* Pods: The smallest deployable units in Kubernetes. A Pod contains one or more containers.

Pod Creation Workflow

1. Submit a Pod manifest using kubectl.
2. The API server validates and processes the request.
3. The Pod object is stored in etcd.
4. The scheduler selects a suitable Worker Node.
5. The node assignment is recorded through the API server.
6. The kubelet on the selected node detects the assignment.
7. The kubelet works with the container runtime to start the container.
8. The kubelet reports the Pod status through the API server.

Example Pod YAML

The following manifest defines a Pod running an NGINX container.

apiVersion: v1
kind: Pod
metadata:
  name: nginx-demo
spec:
  containers:
    - name: nginx
      image: nginx:stable
      ports:
        - containerPort: 80

Project Files

* Detailed Kubernetes Architecture Notes
* Kubernetes Architecture Diagram
* Example Pod YAML Manifest

Official References

* Kubernetes Architecture
* Kubernetes Components
* Kubernetes Nodes
* Kubernetes Pods

Author

Modupe Paseda

Cloud and DevOps Learning Project

Kubernetes Architecture

1. Introduction

Kubernetes is an open-source platform used to deploy, manage, and scale containerized applications. It helps ensure applications run as expected across a group of machines called a cluster.

A Kubernetes cluster consists of two main parts:

* Control Plane
* Worker Nodes

2. Kubernetes Cluster Architecture

Control Plane

The Control Plane manages the Kubernetes cluster. It makes decisions about scheduling workloads and maintaining the desired state of applications.

Its main components are:

kube-apiserver

* Exposes the Kubernetes API.
* Receives and validates requests from users and other components.
* Acts as the main communication point for the cluster.

etcd

* A distributed key-value store.
* Stores Kubernetes cluster state and configuration data.
* The API server accesses it to persist cluster information.

kube-scheduler

* Watches for newly created Pods that have not been assigned to a node.
* Selects a suitable worker node based on available resources and scheduling rules.

kube-controller-manager

* Runs controllers that monitor the cluster.
* Helps move the cluster toward its desired state.

cloud-controller-manager

* Integrates Kubernetes with supported cloud provider services.
* It is optional and is mainly used when cloud integration is needed.

Worker Nodes

Worker nodes run the application workloads assigned to them by Kubernetes.

Their main components include:

kubelet

* Runs on each worker node.
* Communicates with the API server.
* Ensures assigned Pods and their containers run as expected.

Container Runtime

* Downloads images and runs containers.
* Examples include containerd and CRI-O.

kube-proxy

* Supports network communication for Kubernetes Services on a node.
* Some cluster networking implementations provide equivalent functionality without kube-proxy.

Pods

* The smallest deployable units in Kubernetes.
* A Pod contains one or more containers that share network resources and may share storage.

3. How a Pod Is Created

A Pod can be defined in a YAML manifest and submitted to Kubernetes using kubectl.

Example command:

kubectl apply -f pod.yaml

The general workflow is:

1. The user submits the YAML manifest using kubectl.
2. The API server receives and validates the request.
3. The API server stores the desired cluster state in etcd.
4. The scheduler detects the unscheduled Pod and selects a suitable worker node.
5. The assignment is recorded through the API server.
6. The kubelet on the selected node detects the Pod assignment.
7. The kubelet works with the container runtime to pull the required image and start the container.
8. Kubernetes reports the Pod’s status through the API server.

The scheduler selects the node; it does not start the container. The kubelet and container runtime on the selected worker node handle the work needed to run the Pod.

4. Example Pod YAML

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

Explanation

* apiVersion: v1 specifies the Kubernetes API version for the Pod.
* kind: Pod identifies the resource type.
* metadata.name gives the Pod its name.
* spec describes the desired configuration.
* containers lists the containers in the Pod.
* image specifies the container image to run.
* containerPort: 80 documents the port the container listens on. It does not automatically expose the application outside the cluster.

5. Important Kubernetes Concepts

Desired state: The configuration that Kubernetes should maintain.

Reconciliation: Controllers repeatedly compare the current state with the desired state and take action when needed.

Declarative configuration: Users describe the desired result in a manifest instead of manually specifying every operation.

Self-healing: Kubernetes can restart failed containers and replace or reschedule workloads in supported circumstances.

Scalability: Kubernetes supports increasing or decreasing application replicas to meet workload needs.

6. Conclusion

Understanding Kubernetes architecture helps explain how cluster management, scheduling, networking, and container execution work together.

The Control Plane manages the cluster, while worker nodes run application workloads in Pods. The API server coordinates communication, etcd stores cluster state, the scheduler selects nodes, and the kubelet works with the container runtime to run assigned workloads.

7. Official Documentation

* Kubernetes Architecture: https://kubernetes.io/docs/concepts/architecture/
* Pods: https://kubernetes.io/docs/concepts/workloads/pods/
* kubectl: https://kubernetes.io/docs/reference/kubectl/

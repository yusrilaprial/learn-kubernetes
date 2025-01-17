# Learn Kubernetes

This repository contains the code and examples for the Learn Kubernetes.

## Requirements

- [Docker](https://www.docker.com/)
- [Kubernetes](https://kubernetes.io/)

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It was originally designed by Google and is now maintained by the Cloud Native Computing Foundation.

## Node

A node is a worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each node contains the services necessary to run pods and is managed by the control plane. The services on a node include the container runtime, kubelet, and kube-proxy.

### Node Components

- **Kubelet**: An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
- **Kube-proxy**: Maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.
- **Container Runtime**: The software that is responsible for running containers.

Commands:

```bash
# List all nodes
kubectl get nodes

# Get detailed information about a node
kubectl describe node <node-name>
```

## Pod

A pod is the smallest and simplest Kubernetes object. A Pod represents a set of running containers on your cluster.

### Pod Components

- **Containers**: A container is a runtime instance of a Docker image.
- **Pod IP**: Each Pod is assigned a unique IP address.
- **Pod Volume**: A volume is a directory that contains data, accessible to the containers in a pod.

Commands:

```bash
# Create a pod
kubectl create -f <filepod.yaml>

# List all pod
kubectl get pod

# Detail List all pod
kubectl get pod -o wide

# List all pod with labels
kubectl get pod --show-labels

# Get detailed information about a pod
kubectl describe pod <pod-name>

# Access Pod for Testing Runing or Not
kubectl port-forward <pod-name> 8080:80

# Add label to pod by command
kubectl label pod <pod-name> <label-key>=<label-value>
# Add label to pod by command overwrite
kubectl label pod <pod-name> <label-key>=<label-value> --overwrite

# Delete a pod
kubectl delete pod <pod-name>
kubectl delete pod <pod-name> <pod-name> ...

# Delete all pod in a namespace
kubectl delete pods --all --namespace <namespace-name>
```

## Labels

Labels are key/value pairs that are attached to objects, such as pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system.

Commands:

```bash
# Query with labels
kubectl get pod -l <label-key>
kubectl get pod -l <label-key>=<label-value>
kubectl get pod -l '!<label-key>'
kubectl get pod -l <label-key>!=<label-value>
kubectl get pod -l <label-key> in (<label-value1>, <label-value2>)
kubectl get pod -l <label-key> notin (<label-value1>, <label-value2>)
```

## Annotations

Annotations are similar to labels, but they are not used to identify and select objects. Annotations are used to store non-identifying metadata.

Commands:

```bash
# Add annotation to pod by command
kubectl annotate pod <pod-name> <annotation-key>="<annotation-value>"
# Add annotation to pod by command overwrite
kubectl annotate pod <pod-name> <annotation-key>="<annotation-value>" --overwrite
```

## Namespace

Namespaces are a way to divide cluster resources between multiple users. They are intended for use in environments with many users spread across multiple teams or projects.

Commands:

```bash
# Create a namespace
kubectl create namespace <namespace-name>

# List all namespaces
kubectl get namespaces

# Get detailed information about a namespace
kubectl describe namespace <namespace-name>

# Get Pods in a namespace
kubectl get pods --namespace <namespace-name>
kubectl get pods -n <namespace-name>

# Create a namespace
kubectl create namespace <namespace-name>

# Create a pod in a namespace
kubectl create -f <filepod.yaml> --namespace <namespace-name>

# Delete a namespace
kubectl delete namespace <namespace-name>
```

## Probe

Probes are diagnostic tools that are built into Kubernetes. They are used to determine the health of a container.

There are three types of probes:
- **Liveness Probe**: Indicates whether the container is running. If the liveness probe fails, the container will be restarted.
- **Readiness Probe**: Indicates whether the container is ready to serve traffic. If the readiness probe fails, the container will be removed from the service.
- **Startup Probe**: Indicates whether the container is ready to serve traffic. If the startup probe fails, the container will be restarted.

Methods for probes:
- **HTTP Get**: Makes an HTTP GET request to the specified path on the container.
- **Exec**: Executes a command inside the container.
- **TCP Socket**: Opens a TCP connection to the specified port on the container.

## Replication Controller

A Replication Controller ensures that a specified number of pod replicas are running at any one time. If there are too many pods, the Replication Controller will kill some. If there are too few, the Replication Controller will start more.

Commands:

```bash
# Create a Replication Controller
kubectl create -f <filereplicationcontroller.yaml>

# List all Replication Controllers
kubectl get replicationcontrollers
kubectl get rc

# Get detailed information about a Replication Controller
kubectl describe rc <replicationcontroller-name>

# Delete a Replication Controller
kubectl delete rc <replicationcontroller-name>

# Delete a replication controller without deleting the pods
kubectl delete rc <replicationcontroller-name> --cascade=false
```

## Replica Set

A Replica Set is the next-generation Replication Controller. It is similar to a Replication Controller, but it has more powerful selector support.

Commands:

```bash
# Create a Replica Set
kubectl create -f <filereplicaset.yaml>

# List all Replica Sets
kubectl get replicaset
kubectl get rs
```

# References

- [PZN](https://github.com/khannedy/belajar-kubernetes/tree/master)

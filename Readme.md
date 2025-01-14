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

# References

- [PZN](https://github.com/khannedy/belajar-kubernetes/tree/master)

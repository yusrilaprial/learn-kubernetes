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

# Exec into Pod
kubectl exec -it <pod-name> -- /bin/bash

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

### Match Expression

Match Expressions are used to select the pods that the Replica Set will manage.

Operators:
- **In**: Selects the pods that have the specified value in the specified key.
- **NotIn**: Selects the pods that do not have the specified value in the specified key.
- **Exists**: Selects the pods that have the specified key.
- **DoesNotExist**: Selects the pods that do not have the specified key.

## Daemon Set

A Daemon Set ensures that all (or some) nodes run a copy of a pod. As nodes are added to the cluster, pods are added to them. As nodes are removed from the cluster, those pods are garbage collected.

Commands:

```bash
# Create a Daemon Set
kubectl create -f <filedaemonset.yaml>

# List all Daemon Sets
kubectl get daemonsets
kubectl get ds
```

## Job

A Job creates one or more pods and ensures that a specified number of them successfully terminate. As pods successfully complete, the Job tracks the successful completions. When a specified number of successful completions is reached, the task is complete.

Commands:

```bash
# Create a Job
kubectl create -f <filejob.yaml>

# List all Jobs
kubectl get jobs
```

## Cron Job

A Cron Job creates a job on a repeating schedule.

Commands:

```bash
# Create a Cron Job
kubectl create -f <filecronjob.yaml>

# List all Cron Jobs
kubectl get cronjobs
```

## Node Selector

Node Selectors are used to constrain the set of nodes that a pod is eligible to be scheduled on.

Commands:

```bash
# Add label to node by command
kubectl label node <node-name> <label-key>=<label-value>
```

## Service

A Service is an abstraction that defines a logical set of pods and a policy by which to access them. Services enable a loose coupling between dependent pods. labels are used to select the pods that the service will route traffic to. Services can be exposed in different ways by specifying a type in the ServiceSpec. There are four supported service types:
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster.
    - DNS name: `<service-name>.<namespace-name>.svc.cluster.local:<port>` (e.g., my-service.default.svc.cluster.local:8080)
    - IP: `<cluster-ip>:<port>`
- **NodePort**: Exposes the service on each Node's IP at a static port. A ClusterIP service, to which the NodePort service will route, is automatically created.
- **LoadBalancer**: Exposes the service externally using a cloud provider's load balancer. NodePort and ClusterIP services, to which the external load balancer will route, are automatically created.
- **ExternalName**: Maps the service to the contents of the externalName field (e.g., foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up.

Commands:

```bash
# Create a Service
kubectl create -f <fileservice.yaml>

# List all Services
kubectl get services
```

## Ingress

An Ingress is an API object that manages external access to services in a cluster. It provides HTTP and HTTPS routing to services based on the host and path.

Commands:

```bash
# Create an Ingress
kubectl create -f <fileingress.yaml>

# List all Ingresses
kubectl get ingresses

# Get detailed information about an Ingress
kubectl describe ingress <ingress-name>
```

## Multi Container Pod

Multi-Container Pods in Kubernetes are Pods that run more than one container inside them. These containers share common resources, such as network namespaces, IPC namespaces, and sometimes volumes. This allows for very efficient communication between containers within a single Pod.

## Volume

A Volume in Kubernetes is a directory containing data, accessible to all containers within a Pod. It's a mechanism to persist data independently of the Pod's lifecycle, meaning that even if a Pod is terminated and restarted, the data in the volume persists.

- **emptyDir**: A simple, empty directory created when the Pod is created and deleted when the Pod is removed from the node. Useful for temporary storage shared between containers in the same Pod.
- **hostPath**: Mounts a directory from the underlying host node into the Pod. Useful for accessing resources on the host machine, but less portable.
- etc.

## Config Map

A ConfigMap in Kubernetes is an API object used to store non-confidential data in key-value pairs. This data can then be consumed by applications running in Pods. Essentially, it provides a mechanism to decouple configuration from your application images, making them more portable and configurable.

Commands:

```bash
# Show config map
kubectl get configmaps

# Detail config map
kubectl describe configmap <configmap-name>

# Delete config map
kubectl delete configmap <configmap-name>
```

## Secret

Secrets are objects used to store sensitive data, such as passwords, OAuth tokens, SSH keys, and certificates. Secrets ensure that this data is not exposed in the Pod configuration or other visible Kubernetes resources.

```bash
# Show secret
kubectl get secrets

# Detail secret
kubectl describe secret <secret-name>

# Delete secret
kubectl delete secret <secret-name>
```

## Imperative Management

```bash
# Create Kubernetes Object
kubectl create -f <file.yaml>

# Update Kubernetes Object
kubectl replace -f <file.yaml>

# Show Kubernetes Object
kubectl get -f <file.yaml> -o yaml/json

# Delete Kubernetes Object
kubectl delete -f <file.yaml>
```

## Declarative Management

```bash
kubectl apply -f <file.yaml>
```

## Deployment

A Deployment is a declarative way to manage stateless applications in Kubernetes. You describe the desired state of your application (like the number of replicas, the container image, resources, etc.) in a YAML file, and the Deployment controller ensures that the current state matches the desired state. It manages ReplicaSets, which in turn manages Pods.

## Rollout

Rollouts are a way to manage the update process of your deployments.  They allow you to control the speed and safety of updates, ensuring minimal disruption to your application.  They provide features like progressive rollouts, rollbacks, and pausing updates.

```bash
kubectl rollout status deployment <deployment-name>
kubectl rollout history deployment <deployment-name>
kubectl rollout undo deployment <deployment-name>
kubectl rollout pause deployment <deployment-name>
kubectl rollout resume deployment <deployment-name>
```

## Persistent Volume

Persistent Volumes (PVs) are pieces of storage in a Kubernetes cluster that have a lifecycle independent of any individual Pod. This means that a PV can outlive the Pods that use it, allowing data to persist even if the Pod is deleted or rescheduled. PVs are provisioned by an administrator and are a cluster-wide resource. They abstract the underlying storage implementation (whether it's a network file system, a cloud provider's block storage, or a local disk) from the users.

```bash
# List all Persistent Volumes
kubectl get pv

# Get detailed information about a Persistent Volume
kubectl describe pv <pv-name>

# Delete a Persistent Volume
kubectl delete pv <pv-name>

# List all Persistent Volume Claims
kubectl get pvc

# Get detailed information about a Persistent Volume Claim
kubectl describe pvc <pvc-name>

# Delete a Persistent Volume Claim
kubectl delete pvc <pvc-name>
```

## Stateful Set

A StatefulSet is a workload API object that manages stateful applications in Kubernetes. It's designed specifically for applications that require stable, persistent storage, ordered deployments, and unique network identifiers. Think of databases, distributed file systems, or other applications where the order of deployment and persistent identity are crucial.

```bash
# Create a Stateful Set
kubectl create -f <filestatefulset.yaml>

# List all Stateful Sets
kubectl get statefulsets
kubectl get sts

# Get detailed information about a Stateful Set
kubectl describe sts <statefulset-name>

# Delete a Stateful Set
kubectl delete sts <statefulset-name>
```

## Computational Resources

Kubernetes allows you to specify resource requests and limits for each container. These resources are then managed by the Kubernetes scheduler to ensure that Pods are placed on nodes with sufficient capacity.

Here's a breakdown related to computational resources in Kubernetes:
- **Requests**: The amount of CPU and Memory that a container requests from the Kubernetes scheduler. This is the minimum amount that the container is guaranteed to receive.
- **Limits**: The maximum amount of CPU and Memory that a container can consume. If a container attempts to use more resources than its limit, it may be throttled or terminated.

These requests and limits are specified in the Pod spec using resource units:
- **CPU**: Measured in CPU units (cores or millicores). For example, 100m is 100 millicores, which is equivalent to 0.1 CPU cores. 1 represents 1 CPU core.
- **Memory**: Measured in bytes. You can use suffixes like Mi, Gi, etc. For example, 128Mi represents 128 mebibytes of memory.

Example in a Pod spec:
```yml
spec:
  containers:
  - name: my-container
    image: my-image
    resources:
      requests:
        cpu: 500m
        memory: 256Mi
      limits:
        cpu: 1
        memory: 512Mi
```

## Horizontal Pod Autoscaler (HPA)

An HPA automatically adjusts the number of pods in a Deployment, ReplicaSet, StatefulSet, or ReplicationController based on observed metrics. This dynamic scaling ensures your application can handle varying loads while optimizing resource utilization.

Key Concepts:
- **Metrics:**  HPA uses metrics to make scaling decisions. Common metrics include CPU utilization, memory utilization, and custom metrics (e.g., requests per second).
- **Target Value:** The desired average value for the chosen metric (e.g., 70% CPU utilization).
- **Minimum and Maximum Replicas:** The HPA operates within these bounds, preventing runaway scaling.
- **Scaling Algorithm:**  The HPA's control loop uses an algorithm to calculate the desired number of pods.
- **Cooldown Period:** After scaling, the HPA waits for a cooldown period before further scaling actions.

How it Works:
1. **Metric Collection:** The HPA queries the metrics server (or custom metrics API) for resource utilization.
2. **Target Calculation:** The HPA compares current metrics to the target and calculates the desired replica count.
3. **Replica Adjustment:** The HPA adjusts the replica count of the target deployment (or other scalable object).
4. **Cooldown:**  The HPA enters a cooldown period to prevent rapid scaling oscillations.

Example:
```yml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
```

# References

- [Programmer Zaman Now](https://github.com/khannedy/belajar-kubernetes)

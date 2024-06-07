# k8s-yaml-manifests:
# Deploying Caddy Web Server on Kubernetes

This repository contains YAML manifests and instructions to deploy a Caddy web server on Kubernetes.

## Prerequisites

Before you begin, ensure you have the following installed:

- `kubectl`: Kubernetes command-line tool
- Docker Hub credentials
- Access to a Kubernetes cluster

## Steps to Deploy


1. **Create the docker Registry Key:**
Create a secret for Docker Registry authentication.
```bash
kubectl create secret docker-registry myregistrykey \
    --docker-username=username \
    --docker-password=secret \
    --docker-email=docker@email.com

```

- To check the version:

```bash
kubectl version
kubectl version --output=yaml
```

- To check info about the cluster

```bash
kubectl config view
```

- To run a Pod

```bash
kubectl run <pod name> --image <image name>
kubectl run myngix --image nginx
```

- To create a deployment

```bash
kubectl create deployment <name> --image <image name>
kubectl create deployment mynginx --image nginx
```

- To scale the deployment (increase replicas)

```
kubectl scale deployment <deployment name> --replicas <no of replicas>
kubectl scale deployment mynginx --replicas 2
```

- To check all running services, pods, etc.

```bash
kubectl get all
```

- To get the get details from the a particular namespace

```bash
kubectl get all -n <namespace name>
```

- To get the internal components running

```bash
kubectl get pods -A 
kubectl get pods -A -owide
```

- To check all the running services

```bash
kubectl get services
```

- To check all the running pods

```bash
kubectl get pods
```

```bash
// with extra details
kubectl get pods -o wide
```

- To check all the running node.

```bash
kubectl get nodes
```

- To check all the replicaset

```bash
kubectl get replicaset
```

- To check all the namespaces

```bash
kubectl get namespaces
```

- To get all the API resources

```
kubectl api-resources
```

- To delete the deployment

```bash
kubectl delete deployment <deployment-name>
```

- To delete the pods 

```bash
kubectl delete pod <pod-name>
```

- To get logs of a pod

```bash
kubectl logs <pod-name>
```

- To check logs or sh/bash of a container inside a pod. That if pods have multiple container an we have enter inside a container

```bash
kube exec -it <pod-name> -c <container-name> -- <bash command>
kube exec -it multi-container -c nginx-container -- curl localhost
kube exec -it multi-container -c nginx-container -- sh
kubectl logs multi-container -c nginx-container
```

- To get inside the pod

```
kubectl exec -it <pod name> -- sh
kubectl exec -it nginx -- sh
```

- Get a deep details/state chnages about a pod 

```bash
kube describe pod <pod -name>
```

- To watch the pods (watch refresh every few seconds)
```bash
kubectl get pods -w
```

- To check the cluster are avilable

```
kube config get-contexts
```

- To delete all the pods
```
kubectl delete pods --all
```

- Apply to a particular namespace

```bash
kubectl apply -f <config file name> --namespace=<namespace name>
```


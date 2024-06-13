# k8s-yaml-manifests
# Deploying Caddy Web Server on Kubernetes

This repository contains YAML manifests and instructions to deploy a Caddy web server on Kubernetes.

## Prerequisites

Before you begin, ensure you have the following installed:

- `kubectl`: Kubernetes command-line tool
- Docker Hub credentials
- Access to a Kubernetes cluster

## Steps to Deploy

- Create the docker Registry Key:
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

- To check all running services, pods, etc.

```bash
kubectl get all
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
- To get all the API resources

```
kubectl api-resources
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

- To delete all the pods
```
kubectl delete pods --all
```


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

2. **Apply HTML Pod Manifest:**

   Apply the HTML Pod manifest to deploy the Caddy web server pod.

   ```bash
   kubectl apply -f htmlpod.yaml
   ``
3. **Describe Pod Manifest:**
   Describe the pod for detailed information.
   ```bash
  kubectl describe pods
  ``
4. **Delete Pod Manifest:**
If needed, delete the existing pod.
  ```bash
  kubectl delete pod caddy-web-server
  ``

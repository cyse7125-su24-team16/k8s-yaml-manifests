# k8s-yaml-manifests:
# Deploying Caddy Web Server on Kubernetes

This repository contains YAML manifests and instructions to deploy a Caddy web server on Kubernetes.

## Prerequisites

Before you begin, ensure you have the following installed:

- `kubectl`: Kubernetes command-line tool
- Docker Hub credentials
- Access to a Kubernetes cluster

## Steps to Deploy

1. **Apply HTML Pod Manifest:**

   Apply the HTML Pod manifest to deploy the Caddy web server pod.

   ```bash
   kubectl apply -f htmlpod.yaml
   ```
2. **Describe Pod Manifest:**
  ```bash
  kubectl describe pods
   ```


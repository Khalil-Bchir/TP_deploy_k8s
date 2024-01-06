Certainly! Here's the full README content in one block:

```markdown
# Minikube Kubernetes Deployment for rancher-demo

This repository demonstrates the deployment of the "rancher-demo" application using Minikube, Kubernetes, and Docker.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Docker](https://docs.docker.com/get-docker/)

## Getting Started

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd TP_deploy_k8s
   ```

2. Set Minikube context:

   ```bash
   kubectl config use-context minikube
   ```

## Deploying as a Simple Pod

### Step 1: Create a Pod

Create a YAML file `rancher-demo-pod.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: rancher-demo-pod
spec:
  containers:
  - name: rancher-demo-container
    image: salahgo/rancher-demo
```

### Step 2: Apply the Pod Configuration

```bash
kubectl apply -f rancher-demo-pod.yaml
```

### Step 3: Check Pod Status

```bash
kubectl get pods
```

### Step 4: Visit the Application

```bash
minikube service rancher-demo-service
```

### Step 5: Cleanup

```bash
kubectl delete -f rancher-demo-pod.yaml
```

## Deploying with a Deployment

### Step 1: Create a Deployment

Create a YAML file `rancher-demo-deploy.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rancher-demo
  labels:
    app: rancher-demo
spec:
  selector:
    matchLabels:
      app: rancher-demo
  replicas: 1
  template:
    metadata:
      labels:
        app: rancher-demo
    spec:
      containers:
      - image: salahgo/rancher-demo
        name: rancher-demo-container
        ports:
        - containerPort: 80
```

### Step 2: Apply the Deployment Configuration

```bash
kubectl apply -f rancher-demo-deploy.yaml
```

### Step 3: Check Deployment Status

```bash
kubectl get deployments
```

### Step 4: Cleanup

```bash
kubectl delete -f rancher-demo-deploy.yaml
```

## Adding a NodePort Service

### Step 1: Create a NodePort Service

Create a YAML file `rancher-demo-svc.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: rancher-demo-service
  labels:
    app: rancher-demo
spec:
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: rancher-demo
  type: NodePort
```

### Step 2: Apply the Service Configuration

```bash
kubectl apply -f rancher-demo-svc.yaml
```

### Step 3: Visit the Application

```bash
minikube service rancher-demo-service
```

### Step 4: Cleanup

```bash
kubectl delete -f rancher-demo-svc.yaml
```

## Adding a LoadBalancer Service

### Step 1: Modify the Service to LoadBalancer

Modify the `rancher-demo-svc.yaml` file to set the service type to `LoadBalancer`.

### Step 2: Apply the Updated Service Configuration

```bash
kubectl apply -f rancher-demo-svc.yaml
```

### Step 3: Use Minikube Tunnel

```bash
minikube tunnel
```

### Step 4: Visit the Application

```bash
minikube service rancher-demo-service
```

### Step 5: Cleanup

```bash
kubectl delete -f rancher-demo-svc.yaml
```
```


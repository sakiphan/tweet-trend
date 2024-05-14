## Kubernetes Deployment

### Overview

This README provides instructions on deploying the `sakiphan-rtp` application on a Kubernetes cluster running on an EC2 `t3.medium` instance. It includes steps for creating and applying Kubernetes resources such as Namespace, Secret, Deployment, and Service. Additionally, it provides the necessary commands to apply these resources to your Kubernetes cluster.

### Prerequisites

- A running Kubernetes cluster on an EC2 `t3.medium` instance.
- The `kubectl` command-line tool installed.
- Docker image hosted on JFrog Artifactory and necessary credentials.

### Step 1: Create Namespace

Namespaces isolate Kubernetes resources. We will create a namespace called `sakiphan`.

**Namespace Definition (`namespace.yaml`):**

```yaml
apiVersion: v1
kind: Namespace
metadata:
 name: sakiphan
```

### Step 2: Create Secret

We will create a secret that contains the authentication information required to pull Docker images from JFrog Artifactory.

**Secret Definition (`secret.yaml`):**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: cred
  namespace: sakiphan
data:
  .dockerconfigjson: ewoJImF1dGhzIjogewoJCSJ2YWxheHkwNS5qZnJvZy5pbyI6IHsKCQkJImF1dGgiOiAiYkc5bmFXNTBiMkYzYzBCbmJXRnBiQzVqYjIwNlZtRnNZWGg1UURFeU13PT0iCgkJfQoJfQp9
type: kubernetes.io/dockerconfigjson
```

### Step 3: Create Deployment

A `Deployment` ensures that a specified number of pod replicas are running at any given time. We will create a deployment named `sakiphan-rtp`.

**Deployment Definition (`deployment.yaml`):**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sakiphan-rtp
  namespace: sakiphan
spec:
  replicas: 1
  selector:
    matchLabels:
      app: sakiphan-rtp
  template:
    metadata:
      labels:
        app: sakiphan-rtp
    spec:
      imagePullSecrets:
      - name: cred
      containers:
      - name: sakiphan-rtp
        image: sakiphan.jfrog.io/sakiphan-docker/ttrend:2.1.2
        imagePullPolicy: Always
        ports:
        - containerPort: 8000
        env:
        - name: CONSUMER_KEY
          value: "YOUR_KEY"
        - name: CONSUMER_SECRET
          value: "YOUR_SECRET"
        - name: ACCESS_TOKEN
          value: "YOUR_TOKEN"
        - name: ACCESS_TOKEN_SECRET
          value: "YOUR_TOKEN_SECRET"
```

### Step 4: Create Service

A `Service` exposes the pods to the external world. We will create a `NodePort` service to expose the `sakiphan-rtp` pod.

**Service Definition (`service.yaml`):**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: sakiphan-rtp-service
  namespace: sakiphan
spec:
  type: NodePort
  selector:
    app: sakiphan-rtp
  ports:
  - nodePort: 30082
    port: 8000
    targetPort: 8000
```

### Applying the Resources

Use the following commands to apply the defined Kubernetes resources to your cluster. These commands will create the namespace, secret, deployment, and service.

```sh
kubectl apply -f namespace.yaml
kubectl apply -f secret.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### File Structure

Organize your Kubernetes resource files and the apply script as follows:

```
.
├── namespace.yaml
├── secret.yaml
├── deployment.yaml
├── service.yaml
├── apply.sh
```

### apply.sh

To simplify the application process, use the following `apply.sh` script:

```sh
#!/bin/sh
kubectl apply -f namespace.yaml
kubectl apply -f secret.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Running on an EC2 `t3.medium` Instance

This setup assumes that your Kubernetes cluster is running on an Amazon EC2 `t3.medium` instance. The `t3.medium` instance type provides a balance of compute, memory, and network resources, making it suitable for a variety of workloads, including running Kubernetes clusters.

1. **Launch an EC2 `t3.medium` Instance**:
   - Go to the AWS Management Console.
   - Navigate to EC2 and launch a new instance.
   - Choose the `t3.medium` instance type.
   - Configure instance details, including network and security groups.
   - Launch the instance.

2. **Set Up Kubernetes on EC2**:
   - SSH into your EC2 instance.
   - Install Docker and Kubernetes.
   - Initialize your Kubernetes cluster using `kubeadm` or another tool.
   - Ensure your cluster is up and running by checking the status of the nodes and pods.

3. **Install kubectl on Your Local Machine**:
   - Install `kubectl` to interact with your Kubernetes cluster.
   - Configure `kubectl` to connect to your EC2-hosted Kubernetes cluster.

### Summary

This README provides the steps and definitions required to deploy the `sakiphan-rtp` application on a Kubernetes cluster running on an EC2 `t3.medium` instance. It includes instructions for creating Namespace, Secret, Deployment, and Service resources. Follow the steps above to deploy your application on Kubernetes and ensure it runs smoothly on your EC2 instance.
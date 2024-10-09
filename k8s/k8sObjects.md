# K8s Objects

In Kubernetes (K8s), objects are persistent entities in the Kubernetes system that represent the desired state of your cluster. They are the fundamental building blocks for deploying and managing applications, networking, storage, and configurations in the cluster.

Each Kubernetes object is defined in a manifest file (usually written in YAML or JSON), which describes the desired state of that object. Kubernetes then works to ensure that the actual state of the object matches the desired state, using controllers to manage and monitor resources.

### 1. Pod:

**Description:** A Pod is the smallest and simplest Kubernetes object, representing a group of one or more containers that share the same network namespace (IP address) and storage.
**Purpose:**
* Pods are the units of execution in Kubernetes.
* Containers inside the same pod can communicate with each other via localhost and can share storage volumes.
* A pod is typically ephemeral; if it crashes, Kubernetes will create a new one.
**Use Case:** Deploying one or more containers that need to share resources like networking or storage.

```agsl
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
spec:
  containers:
    - name: nginx
      image: nginx:latest

```
### 2. Deployment:

A Deployment in Kubernetes is an abstraction that allows you to define and manage the lifecycle of applications (specifically Pods) in a declarative manner. It automates the creation, scaling, updating, and rollback of Pods via ReplicaSets. A Deployment ensures that a specified number of replicas of a Pod are running at any given time.

*Key Features of a Deployment:*

* **Declarative Updates:**  You describe the desired state of your application in a YAML or JSON file, and Kubernetes automatically manages the creation and maintenance of Pods.
* **Self-Healing:** If a pod fails, the Deployment ensures new pods are created to meet the desired state.
* **Scaling:** You can easily scale your application up or down by modifying the number of replicas in the Deployment specification.
* **Rolling Updates:** Allows you to update your application without downtime by gradually replacing old Pods with new ones.
* **Rollback:** In case of a failed update, you can easily roll back to a previous state, ensuring stability.
* **Multiple Versions:** Supports blue-green and canary deployments for gradual rollouts of new features.

```agsl

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3  # Specifies that 3 replicas of the Pod should be running
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2  # Image of the application (Nginx web server in this case)
        ports:
        - containerPort: 80

```

### 3. Service:

In Kubernetes, a Service is an abstraction that defines a logical set of Pods and provides a stable way to access them. Pods in Kubernetes are ephemeral, meaning they can be created and destroyed frequently, and each time a Pod is recreated, it gets a new IP address. This makes it difficult to track and connect to the right set of Pods. A Service solves this by providing a permanent, stable endpoint (IP address or DNS name) that clients can use to connect to the set of Pods.

**Key Features of a Service:**

1. **Stable IP and DNS:** A Service provides a consistent and reliable network endpoint for accessing Pods, even if individual Pods change or are recreated.
2. **Load Balancing:** If multiple Pods match the Service selector, the Service can distribute traffic evenly across all Pods.
3. **Service Discovery:** Services in Kubernetes can be discovered using DNS or environment variables within the cluster.
4. **Internal and External Access:** Services can be exposed internally to other Pods (using a ClusterIP), externally to the internet (using a NodePort or LoadBalancer), or across multiple clusters using Ingress. This makes Services versatile for both internal microservices communication and external-facing applications.

**Types of Kubernetes Services:**

1. **ClusterIP (Default):**

* **Use Case:** For internal communication within the Kubernetes cluster.
* **Function:** Exposes the service on a cluster-internal IP. This makes the service reachable only within the cluster.
* **Example:** Microservices or databases that need to be accessed only by other services inside the cluster.

2. **NodePort:**

* **Use Case:** For exposing a service externally by binding it to a port on each Node.
* **Function:** Makes the service accessible on a static port (the NodePort) on each Node’s IP address.
* **Example:** Useful for simple testing or when external load balancers are not available.

3. **LoadBalancer:**

* **Use Case:** For external traffic when running Kubernetes in a cloud environment.
* **Function:** Provisions a cloud provider's load balancer and forwards traffic from the load balancer to the Pods behind the Service.
* **Example:** Production environments where you need external, highly available access to the application (e.g., a web application accessible on the internet).

4. **ExternalName:**

* **Use Case:** For accessing external services by mapping them to internal DNS.
* **Function:** Provides an internal DNS name for an external service by returning a CNAME record.
* **Example:** Useful when an internal service needs to communicate with a database or API hosted outside the Kubernetes cluster.

```agsl
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30007

```
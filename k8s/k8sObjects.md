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

## 4. ReplicaSet

### Description:
A **ReplicaSet** ensures that a specified number of replicas of a Pod are running at any given time.

### Purpose:
- Ensures high availability by maintaining the desired number of replicas of Pods.
- Automatically replaces failed or terminated Pods.
- Usually, **ReplicaSets** are indirectly managed by **Deployments**, which offer more advanced features (like rolling updates).

### Use Case:
- Scaling Pods up or down based on the desired number of replicas.

### Example:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
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
          image: nginx:latest
```

## 5. StatefulSet 

A **StatefulSet** manages stateful applications in Kubernetes, ensuring each Pod has a unique identity, stable network address, and persistent storage. It's used when the order of Pod creation, deletion, and persistence matters.

## Key Features:
- **Stable Pod Identity**: Each Pod has a consistent name (e.g., `myapp-0`, `myapp-1`), which remains the same after restarts.
- **Stable Network Identity**: Pods have stable hostnames, ensuring consistent communication.
- **Persistent Storage**: Each Pod gets its own persistent storage, retained even when the Pod is deleted or rescheduled.
- **Ordered Creation and Deletion**: Pods are created and deleted in a defined order, important for applications needing controlled startup and shutdown sequences.

## Use Cases:
- Databases (e.g., MySQL, MongoDB)
- Distributed systems (e.g., Kafka, Zookeeper)
- Applications requiring unique Pod identities or persistent data.

## Example YAML:
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: myapp
spec:
  serviceName: "myapp-service"
  replicas: 3
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp-container
          image: myapp:latest
  volumeClaimTemplates:
    - metadata:
        name: myapp-storage
      spec:
        accessModes: [ "ReadWriteOnce" ]
        resources:
          requests:
            storage: 1Gi
```

### Differences from Deployment:
Pods in a StatefulSet are unique and maintain persistent storage, while Deployments manage stateless Pods without these guarantees. Use StatefulSet for stateful applications that need data persistence and ordered Pod management.

## 6. DaemonSet

### Description:
A **DaemonSet** ensures that a specific pod runs on all (or selected) nodes in the cluster.

### Purpose:
- Deploys pods that need to run on every node, such as logging agents, monitoring agents, or network proxies.
- When new nodes are added to the cluster, the DaemonSet automatically runs a pod on those nodes.

### Use Case:
- Deploying system-level applications on all nodes like log collectors (e.g., Fluentd), monitoring agents (e.g., Prometheus), or networking solutions.

### Example YAML:
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-daemonset
spec:
  selector:
    matchLabels:
      app: fluentd
  template:
    metadata:
      labels:
        app: fluentd
    spec:
      containers:
        - name: fluentd
          image: fluentd:latest
```

## 7. Job
### Description:
A **Job** creates one or more Pods and ensures that a specified number of them successfully terminate.

### Purpose:
- Used for running batch jobs, where the job runs to completion (e.g., data processing, backups).
- Ensures that all Pods complete their task and then terminates.

### Use Case:
- Running batch jobs that should run once and then finish, like a data migration or file processing job.

### Example YAML:
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: data-migration-job
spec:
  template:
    spec:
      containers:
        - name: migration
          image: migration-script:latest
      restartPolicy: Never
  backoffLimit: 4
```

## 8. CronJob

### Description:
A **CronJob** is similar to a Job but runs on a scheduled basis, much like a cron job in Linux.

### Purpose:
- Runs jobs periodically at specified times (e.g., every day at midnight).
- Useful for scheduled tasks like backups, report generation, or cleanup tasks.

### Use Case:
- Running periodic jobs on a set schedule, such as database backups or sending emails.

### Example YAML:
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: backup-cronjob
spec:
  schedule: "0 0 * * *"  # Daily at midnight
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: backup
              image: backup-script:latest
          restartPolicy: OnFailure
```

## 9. ConfigMap

### Description:
A **ConfigMap** is used to store non-sensitive configuration data in key-value pairs. It is often used to inject configuration into Pods at runtime.

### Purpose:
- Allows decoupling configuration from application code, making it easier to modify configurations without rebuilding the application.
- Can be mounted as files or used as environment variables in containers.

### Use Case:
- Storing configuration data like database connection strings, API keys, or environment-specific settings.

### Example YAML:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  database_url: "mysql://db.example.com"
  api_key: "myapikey"
```

## 10. Secret

### Description:
A **Secret** is similar to a ConfigMap but used specifically for storing sensitive information, such as passwords, OAuth tokens, or SSH keys.

### Purpose:
- Stores sensitive data in a more secure way than plain text (encoded in base64).
- Kubernetes provides mechanisms to ensure that secrets are not exposed in plain text in logs, environment variables, or other places.

### Use Case:
- Managing sensitive information like passwords for databases or third-party APIs.

### Example YAML:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-password
type: Opaque
data:
  password: cGFzc3dvcmQxMjM=  # base64 encoded "password123"
```
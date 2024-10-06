## ClusterIP

#### Definition:

- The default service type in Kubernetes.
- ClusterIP exposes the service internally within the Kubernetes cluster using an internal IP address. Pods within the same cluster can access the service, but it is not accessible from outside the cluster.

#### Use Case:

Used when you want to make a service accessible only inside the cluster, for communication between pods or services (e.g., microservices interacting with each other).

#### Example:
Imagine a backend microservice (e.g., database) that needs to be accessed by frontend pods but not by external clients.

## NodePort

#### Definition:

- NodePort exposes the service on a static port on each node's IP address. The service becomes accessible externally through < NodeIP > : < NodePort >.
- The port range is typically between 30000-32767.
#### Use Case:

- Used when you need external access to your service but don't want to use a cloud provider's load balancer, or when you have a custom load balancing solution.
- It is suitable for testing and development environments.
#### Drawback:

Directly exposing a NodePort on all nodes in a cluster can be a security risk. In addition, clients need to know the node IP and the port number to access the service.
#### Example:

Exposing a service running in the cluster to external clients for direct access, such as a development web server.
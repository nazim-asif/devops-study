![kubernets architecture](https://github.com/nazim-asif/devops-study/blob/main/k8s/kubernet.png)

Kubernetes (K8s) has a master-worker architecture that is designed to automate the deployment, scaling, and management of containerized applications. This architecture is composed of various components that work together to manage the entire lifecycle of applications in a cluster.


### Working with Kubernetes

1. **We Create manifest (.yml):** Define the desired state of Kubernetes objects (e.g., pods, services, deployments) in a YAML manifest file.

2. **Apply Manifest to the Cluster (to master):** 
  
  i. Use kubectl apply -f <file.yml> to send the manifest to the Kubernetes API server on the master node.

  ii. The API server processes the request and updates the etcd database, which holds the cluster’s desired state.

3. **Pod Runs on Node:**

  i. The scheduler assigns the pod to a suitable worker node based on resource availability and constraints.

  ii. The kubelet on the worker node pulls the container image and starts the pod.

  iii. The master node continues to control and monitor the worker node, ensuring the pod stays in the desired state.

### Role of Master Node

In Kubernetes, the master node (also called the control plane) is responsible for managing the entire Kubernetes cluster. It acts as the "brain" of the system, making global decisions about scheduling, scaling, and ensuring the desired state of the cluster. The master node controls and manages the worker nodes, where the actual application workloads (containers) are run.

* **Kube api server:** The Kubernetes API Server (kube-apiserver) is a key component of the Kubernetes control plane. It serves as the main entry point for all administrative tasks in a Kubernetes cluster and is responsible for exposing the Kubernetes API, which users and internal components use to interact with and manage the cluster.

    i. *Central Communication Hub:* It handles all requests to manage Kubernetes resources (pods, services, nodes, etc.) from users (via kubectl or other tools) and internal components (scheduler, controllers, etc.).
    
    ii. *State Management:* It communicates with etcd, the cluster’s key-value store, to retrieve and update the cluster’s desired state (e.g., what pods should be running).

    iii. *Validation and Configuration:* It validates requests and ensures that resources are properly configured before they are committed to the cluster.

    iv. *Role in the Cluster:* The API server is the front-end of the Kubernetes control plane, providing the interface through which all other components and users manage the cluster.
* **etcd:** etcd is a distributed key-value store used in Kubernetes to store all cluster configuration data and state. It plays a critical role in ensuring that the cluster maintains consistency and can recover from failures.
    
    i. **Distributed and Highly Available:** Ensures cluster data is replicated and consistent across multiple nodes.

   ii. **Key-Value Store:** Stores all Kubernetes object data in a key-value format.

   iii. **Stores Cluster State:** Holds the entire state of the Kubernetes cluster, including configurations, secrets, and resource information.
   
    iv. **Backbone of Kubernetes Control Plane:** Without etcd, Kubernetes would not be able to function, as it relies on it for state persistence.
* **Kubernetes Scheduler:** The Kubernetes Scheduler (or kube-scheduler) is a critical component of the Kubernetes control plane responsible for assigning pods to nodes in a Kubernetes cluster. It decides where new or unscheduled pods will run based on resource requirements, policies, and the current state of the cluster.
   
   i.  **Pod Scheduling:** The main role of the kube-scheduler is to assign newly created or unscheduled pods to worker nodes based on various factors such as resource availability (CPU, memory), constraints, and policies. When a pod is created without a node assignment, it remains in a "Pending" state until the scheduler assigns it to a node.

   ii. **Node Selection Criteria:** The kube-scheduler considers several factors when selecting the best node for a pod:
    * *Resource availability:* Checks if the node has enough CPU, memory, and other resources required by the pod.
    * *Node affinity/anti-affinity:* Ensures that pods are scheduled on or away from certain nodes based on predefined rules.
    * *Pod affinity/anti-affinity:* Ensures that certain pods are placed together or kept apart.
    * *Taints and tolerations:* Prevents pods from being scheduled on nodes that are marked with specific "taints" unless they "tolerate" those taints.
    * *Node selectors and labels:* Ensures that the pod is scheduled on nodes that match certain labels (e.g., specific hardware, zones, etc.).
    * *Pod priority:* High-priority pods can preempt lower-priority ones if needed.
  
  iii. **Scheduling Workflow:** The scheduling process follows a two-step workflow:
    * **Filtering:** The scheduler filters out nodes that don’t meet the pod’s requirements. For example, nodes that don’t have enough resources or fail to meet affinity/anti-affinity rules are excluded.
    *  **Scoring:** The remaining nodes are ranked based on factors like resource utilization and node preferences. The scheduler picks the node with the highest score.

* **Controller Manager:** The Kubernetes Controller Manager is a key component of the Kubernetes control plane, responsible for running various controllers that regulate the cluster’s state. A controller in Kubernetes continuously monitors the desired state of resources and works to maintain that state by making necessary adjustments.

  i. **Controller Function:**

    * A controller watches over a specific type of Kubernetes resource (e.g., pods, nodes, endpoints) and ensures that its actual state matches the desired state defined in the cluster.
  
    * If any discrepancies occur (e.g., a node goes down, or a pod crashes), the controller takes corrective action.
  
  ii. **Single Process, Multiple Controllers:**

    * The kube-controller-manager runs several types of controllers as a single process, rather than having a separate process for each controller. This simplifies management and allows efficient resource usage.
  
  iii. **Types of Controllers:** Some of the key controllers managed by the Controller Manager include:
    * *Node Controller:* Monitors the status of nodes and handles node failures.
    * *Replication Controller:* Ensures the specified number of pod replicas are running.
    * *Endpoints Controller:* Manages the connections between services and their associated pods.
    * *ServiceAccount Controller:* Manages service accounts for pods, enabling them to authenticate with the API server.
    * *Job Controller:* Watches job objects and ensures that the specified number of pods run to completion.

### Role of worker node

* **worker machine:** In Kubernetes, a node is a worker machine (can be a physical server or a virtual machine) where the actual containerized applications run. It is managed by the Kubernetes control plane, which assigns workloads to it based on resource availability and policies. Each node in a Kubernetes cluster includes the necessary components to run and manage containers.

  ##### Key Components of a Node:
1. **kubelet:**

  i. **Role:** Agent responsible for ensuring that containers are running in pods on the node.
  ii. **Function:**
  * Communicates with the API server to receive instructions (e.g., start a pod).
  * Monitors the health of pods running on the node and reports back to the control plane.
  * Ensures that the actual state of the containers matches the desired state as specified in the pod spec.
  * Manages the lifecycle of containers (starting, stopping, or restarting them as needed).

2. **kube-proxy:**

  i. **Role:** Manages networking and enables communication within and between nodes.
  ii. **Function:**
  * Ensures that each pod can communicate with other pods, services, and external traffic.
  * Maintains network rules on the node and routes traffic to the appropriate containers based on IP addresses and ports.
  * Implements load balancing across pods in a service, ensuring even distribution of traffic.
  * Manages NAT (Network Address Translation) to route incoming requests to the correct pod.
3. **Container Runtime/Container engine:**

  i. **Role:** Runs and manages the containers in the pods.
  ii. **Function:**
  * The software that actually runs containers. Popular container runtimes include Docker, containerd, and CRI-O.
  * The container runtime pulls container images from registries, starts containers, and manages their lifecycle (start, stop, and delete).
  * Kubernetes abstracts away the runtime, but it ensures that the containers inside pods are consistently running.

4. **POD:** A pod is the smallest and most basic unit in Kubernetes. It represents a single instance of a running process in your cluster and typically consists of one or more tightly coupled containers that share resources like networking and storage.

#### Key Characteristics of a Pod:
  i. **Single or Multiple Containers:** A pod can run one container (the most common use case) or multiple containers that work together closely (e.g., a web server and a logging sidecar container).
  ii. **Shared Resources:**
   * Networking: Containers in a pod share the same network namespace and IP address. They can communicate with each other using localhost, and external communication is handled by the Kubernetes networking system.
   * Storage: Pods can use shared volumes (persistent or ephemeral) for storing data that containers need to access.
  iii. **Ephemeral Nature:** Pods are designed to be ephemeral. They are created, run, and then destroyed. If a pod fails, Kubernetes will not restart the same pod but will instead create a new pod based on the desired state defined in a controller like a Deployment or ReplicaSet.
  iv. **Deployment Unit:** Pods are the unit of deployment in Kubernetes. When you deploy an application, you are actually deploying pods. Each pod is scheduled on a node by the kube-scheduler, and the kubelet ensures the pod is running as intended.
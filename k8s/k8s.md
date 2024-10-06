![kubernets architecture](https://github.com/nazim-asif/devops-study/blob/main/k8s/kubernet.png)

### Working with Kubernetes

→ We Create manifest (.yml)

→ Apply this to Cluster (to master) to bring into desired state

→ Pod runs on node, which is Controlled by master

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
   
   i. *Pod Assignment:* Assigns pods to nodes based on resource requirements, policies, and constraints.

Node Selection: Evaluates nodes based on resources, affinity rules, taints/tolerations, and other factors.

   Two-Step Process: First filters out unsuitable nodes, then scores and picks the best node.
   Extensible: Can be customized with custom scheduling policies or even multiple schedulers for different use cases.
   Preemption Support: Higher-priority pods can preempt lower-priority ones to ensure critical workloads get scheduled.

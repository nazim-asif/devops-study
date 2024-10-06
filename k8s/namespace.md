## Namespace

A namespace in Kubernetes is a way to divide cluster resources between multiple users or teams. It is a logical separation within a Kubernetes cluster that allows different teams or projects to use the same cluster without interfering with each other. Think of it as a virtual cluster inside a physical Kubernetes cluster.

#### Key Features of Kubernetes Namespaces:

1. Isolation:

- Namespaces provide a way to group and isolate resources like pods, services, and deployments.
- Resources within one namespace do not directly affect resources in another namespace, unless explicitly allowed.

2. Scope of Namespaces:

- Not all Kubernetes resources are namespaced. For example, nodes and persistent volumes are cluster-wide resources, while resources like pods, services, config maps, and secrets are namespaced.

3. Default Namespace:

- By default, when you create resources in Kubernetes without specifying a namespace, they are placed in the default namespace.
4. Multi-Tenancy:

- Namespaces enable multi-tenancy by allowing different users or teams to operate in the same cluster but with logical boundaries.
5. Access Control:

- Kubernetes RBAC (Role-Based Access Control) can be used in conjunction with namespaces to provide access control. You can restrict which users or service accounts have access to certain namespaces.
6. Resource Quotas:

- You can define resource quotas (limits on CPU, memory, etc.) for specific namespaces to ensure that one team or project doesn't consume all the cluster resources.

#### Use Cases for Namespaces:
1. Environment Segmentation: You can create namespaces for different environments, such as dev, stage, and prod.
2. Team Segmentation: Each team or department in an organization can have its own namespace for managing its resources.
3. Multi-Tenant Clusters: Namespaces allow multiple tenants or clients to share the same Kubernetes cluster with resource and access control boundaries.

#### Commands for Working with Namespaces:

1. List All Namespaces:

        kubectl get namespaces

2. Create a New Namespace:

        kubectl create namespace <namespace-name>
3. Delete a Namespace:

        kubectl delete namespace <namespace-name>
4. View Resources in a Specific Namespace:

        kubectl get pods -n <namespace-name>
5. Switch Between Namespaces:

        kubectl config set-context --current --namespace=<namespace-name>
6. Describe a Namespace:

        kubectl describe namespace <namespace-name>
## Exercise 

Create namespace with name demo


      # create namespace 
      kubectl create ns demo

      # Create deployment under ns
      kubectl create deploy nginx-demo --image=nginx -n demo

      # Check it deployment under ns
      kubectl get deploy -n demo

      # Check pods under ns
      kubectl get pods -n=demo
      kubectl get pods -n=demo -o wide

      # Create 3 replica 
      kubectl scale --replicas=3 deploy/nginx-demo -n=demo

      # create and expose port for service
      kubectl expose deploy/nginx-demo --name=svc-demo --port 80 -n=demo

      # Check service
      kubectl get svc -n=demo

      # Enter pod
      kubectl exec -it <pod> -n demo -- sh

      # Check full qualified domain
      cat /etc/resolv.conf

      # Curl with full qualified domain
      curl svc-demo.demo.svc.cluster.local


Create namespace with name demo2


      # create namespace 
      kubectl create ns demo2

      # Create deployment under ns
      kubectl create deploy nginx-demo2 --image=nginx -n demo2

      # Check it deployment under ns
      kubectl get deploy -n demo2

      # Check pods under ns
      kubectl get pods -n=demo2
      kubectl get pods -n=demo2 -o wide

      # Create 3 replica 
      kubectl scale --replicas=3 deploy/nginx-demo2 -n=demo2

      # create and expose port for service
      kubectl expose deploy/nginx-demo2 --name=svc-demo2 --port 80 -n=demo2

      # Check service
      kubectl get svc -n=demo2

      # Enter pod
      kubectl exec -it <pod> -n demo2 -- sh

      # Check full qualified domain
      cat /etc/resolv.conf

      # Curl with full qualified domain
      curl svc-demo2.demo2.svc.cluster.local
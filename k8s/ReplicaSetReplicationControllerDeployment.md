## Replication Controller

#### Definition:

A Replication Controller (RC) ensures that a specified number of pod replicas are running at any given time. If a pod fails or is terminated, the RC will create a new one to maintain the desired count.

#### Key Features:
1. **Maintains a Stable Set of Pods:** If a pod crashes or is deleted, the RC will create a new pod to replace it.
2. **Self-Healing:** Ensures that the specified number of pods is always running.
3. **Simple Scale Up/Down:** Allows you to scale the number of replicas by modifying the RC configuration.

#### Limitations:
Replication Controllers have largely been superseded by ReplicaSets, which offer more flexibility.

##### Example: RC.yml

### Command:

1. **Create a Replication Controller:**

        kubectl create -f RC.yml
2. **List Replication Controllers:**

        kubectl get rc
3. **Describe a Replication Controller:**

        kubectl describe rc nginx-rc
4. **Update a Replication Controller:**

        kubectl apply -f RC.yml
5. **Scale a Replication Controller:**

        kubectl scale rc nginx-rc --replicas=5
6. **Delete a Replication Controller:**

        kubectl delete rc nginx-rc
7. **Label a Replication Controller:**

        kubectl label rc nginx-rc environment=production


## ReplicaSet

#### Definition:
A ReplicaSet (RS) is the next-generation replacement for Replication Controllers. It also ensures that a specified number of pod replicas are running but includes support for more advanced pod selection mechanisms, such as using set-based label selectors.

#### Key Features:
1. **Advanced Label Selection:** ReplicaSets can use set-based selectors, allowing for more complex pod matching criteria.
2. **Maintains Pod Count:** Like an RC, it ensures that the specified number of pods is always running.

##### Example: rs.yml
### Command:

1. **Create a ReplicaSet:**

        kubectl create -f rs.yml
2. **List ReplicaSet:**

        kubectl get rs
3. **Describe a ReplicaSet:**

        kubectl describe rc nginx-replicaset
4. **Update a ReplicaSet:**

        kubectl apply -f rs.yml
5. **Scale a ReplicaSet:**

        kubectl scale rs nginx-replicaset --replicas=5
6. **Delete a ReplicaSet:**

        kubectl delete rs nginx-replicaset
7. **Label a ReplicaSet:**

        kubectl label rs nginx-replicaset environment=production
8. **Port Forward a ReplicaSet:**

       kubectl port-forward rs/nginx-replicaset 8080:80
9. **Patch a ReplicaSet:** To modify (patch) a ReplicaSet's configuration on the fly:

            kubectl patch rs nginx-replicaset -p '{"spec":{"replicas":5}}'
10. **Autoscale a ReplicaSet:** To automatically scale a ReplicaSet based on CPU utilization (using Horizontal Pod Autoscaler):

            kubectl autoscale rs nginx-replicaset --min=2 --max=10 --cpu-percent=80

## Deployment:

#### Definition:
A Deployment is a higher-level controller that manages ReplicaSets and provides declarative updates to your applications. It is the most commonly used controller in Kubernetes for managing stateless applications.

#### Key Features:
1. **Declarative Updates:** Deployments allow you to define the desired state of your application, and Kubernetes will handle the process of updating pods to match that state.
2. **Rolling Updates:** Deployments support rolling updates, where pods are updated incrementally to avoid downtime.
3. **Rollbacks:** If something goes wrong during an update, Deployments allow you to roll back to a previous version.
4. **Manages ReplicaSets:** Deployments create and manage ReplicaSets, ensuring that the appropriate number of pods are running according to the desired state.

##### Example: deployment.yml

### Command:

1. **Create a deployment:**

        kubectl create -f deployment.yml
2. **List deployment:**

        kubectl get deployments
3. **Describe a deployment:**

        kubectl describe deployment nginx-deployment
4. **Scale a deployment:**

        kubectl scale deployment nginx-deployment --replicas=5
5. **Delete a deployment:**

        kubectl delete rs nginx-replicaset
6. **Update a Deployment (Rolling Update):** This command triggers a rolling update, where the old pods are gradually replaced with new ones.

         kubectl set image deployment/nginx-deployment nginx=nginx:1.15
7. **Pause a Deployment:**

         kubectl rollout pause deployment/nginx-deployment
8. **Resume a Deployment:**

         kubectl rollout resume deployment/nginx-deployment
9. **Roll Back a Deployment::**

         kubectl rollout undo deployment/nginx-deployment
10. **Check Deployment Rollout Status:**

         kubectl rollout status deployment/nginx-deployment
11. **List Deployment Revisions:**

        kubectl rollout history deployment/nginx-deployment
12. **View Specific Revision Details:**

            kubectl rollout history deployment/nginx-deployment --revision=2
13. **Delete a Deployment:**

            kubectl delete deployment nginx-deployment

14. **Label a deployment:**

        kubectl label deployment nginx-deployment environment=production
15. **Port Forward a deployment Pod:**

        kubectl port-forward rs/nginx-replicaset 8080:80
16. **Patch a deployment:** To modify (patch) a Deployment's configuration on the fly:

            kubectl patch deployment nginx-deployment -p '{"spec":{"replicas":5}}'

7**Autoscale a deployment:** To automatically scale a Deployment based on CPU utilization (using Horizontal Pod Autoscaler):

            kubectl autoscale deployment nginx-deployment --min=2 --max=10 --cpu-percent=80

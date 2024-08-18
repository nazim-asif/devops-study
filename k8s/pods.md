### Basic Pod Commands:

#### 1. Create a Pod:
    kubectl apply -f <pod-definition.yaml>

#### 2. List Pods:
    kubectl get pods
    kubectl get pods -o wide

- List all Pods in the current namespace. The -o wide option provides additional information like the node the Pod is running on and the Pod's IP.
#### 3. Describe a Pod:
    kubectl describe pod <pod-name>

#### 4. Delete a Pod:
    kubectl delete pod <pod-name>

#### 5. Get Pod Logs:
    kubectl logs <pod-name>
    kubectl logs <pod-name> -c <container-name>

- Retrieve the logs from a Pod. If the Pod contains multiple containers, specify the container with the -c option.

#### 6. Exec into a Pod:

    kubectl exec -it <pod-name> -- /bin/bash

- Start a shell session inside a running container in the Pod. Replace /bin/bash with the appropriate shell or command if necessary.

#### 7. Port Forwarding:

    kubectl port-forward <pod-name> <local-port>:<pod-port>

- Forward a local port to a port on a Pod, allowing you to access services running inside the Pod.

#### 8. Scale Pods (through Deployment or ReplicaSet):

    kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>

- Scale the number of replicas for a Deployment, which will create or terminate Pods as necessary.

#### 9. Copy Files to/from a Pod:

    kubectl cp <local-file> <pod-name>:/path/in/container
    kubectl cp <pod-name>:/path/in/container <local-file>

- Copy files between your local machine and a container in a Pod.

#### 10. Watch Pods:

    kubectl get pods --watch
    kubectl get pods --watch -o wide

- Continuously watch the status of Pods, with updates streamed to the terminal.

#### 11. Apply Resource Limits to a Pod:

    kubectl set resources pod <pod-name> --limits=cpu=200m,memory=512Mi

#### 12. Debug a Pod:
    kubectl debug pod/<pod-name> -it --image=<debug-image>

- Start a debugging session by attaching a new container to an existing Pod. The new container can be used for troubleshooting purposes.
  Drain



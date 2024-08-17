# MultiNode K8s Cluster Setup

## Installation

Kind is the tool for setup multi node cluster setup.

[installation docs](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).

[k8s cheat sheet](https://kubernetes.io/docs/reference/kubectl/quick-reference/).

### Command for creating multinode cluster

    kind create cluster --config multinodeClusterConfig.yaml

    kind create cluster --image kindest/node:v1.31.0@sha256:53df588e04085fd41ae12de0c3fe4c72f7013bba32a20e7325357a1ac94ba865 --name cka-cluster1 --config multinodeClusterConfig.yaml

    kind create cluster --image kindest/node:v1.31.0@sha256:53df588e04085fd41ae12de0c3fe4c72f7013bba32a20e7325357a1ac94ba865 --name cka-cluster2
    
    kubectl get nodes
    kind get clusters

    kubectl config get-contexts
    kubectl config use-context my-cluster-name 


    
    


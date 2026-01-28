# Kubernetes

## k8's cluster 
- Bunch of Nodes is called a cluster


## Master vs Worker node

1. Developer talk to Master node and then Master node tracks and manages the worker node 
2. Master node take Declarative command from developer and perform them 

## jargons 

### Nodes: 
- In kuberenetes we can create and connect various machine togethere, all of which is running kubernetes. Every machine here is know as node
- Two type of node: 
    - Master Node
    - Worker Node


### Master Node: 
Master Node has 4 main thing:- 
- API Server 
- etcd 
- kube-scheduler 
- kube-controller-manger

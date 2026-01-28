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

    #### 1. API Server: 
    The Api Server is gateway to the Kubernetes cluster. It processes all the managment request, whether from the cli(kubctl), ui dashboard or automation tool

    #### 2. etcd(Distribute key-value store):
    etcd serves as Kubernetes’ single source of truth, storing all cluster data, including:

    -  Configuration settings.
    -  Secrets and credentials.
    -  Current and historical states of      workloads.

    #### 3. Kube-Schedule:

    The Scheduler assigns Podds to worker nod, considering factors like
    
    - Resources availabilty
    - Node affinit and anti-affinity rules 
    
    *Affinity* : I want to be placed near/ on this kinf of node or pod 

    *Anti-Affinity* : I dont want to be placed near/ on this kinf of node or pod 


    #### 4. Kube-controller-manger:
    Kubernetes operates on the controller pattern, where controllers monitor the system’s state and take corrective actions. The Controller Manager oversees these controllers, ensuring essential functions such as:

    - Scaling workload based on demand
    - Managing failed nodes and rescheduling workloads
    - Enforcing desired states(e.g: ensuring Deployment always runs the specified number of replicas)

    #### 5. Cloud Controller Manager: 
    For Cloude-based kubernetes deployment, the Cloude Controller Manager integrates the cluster with cloud provider serives, handling: 

    - Provisiongin laod balancers
    - Allocating persistent storage volumnes
    - Scaling infrastrucre dynamically(e.g: adding virtual machine as nodes)


### Worker Node: 
It has 3 main thing: 

- kubelet: the node agent
- kube-Proxy: Networking and laod balancing
- Container Runtime: Running the containers 


    #### 1. Kube-proxy: 

    Kube-Proxy is responsible for managing network communication between services running on different nodes. It:

    - Configures network rules to allow seamless communication between Pods.
    
    - Facilitates service discovery and load balancing for inter-Pod networking.

    - Ensures traffic is routed correctly between nodes and external clients.



    #### 2. kublete: 

    Kubelet is the primary node-level agent that manages the execution of containers. It:

    - Continuously communicates with the API Server to receive instructions.
    
    - Ensure Pods are running as defined in thier specification.

    - Pulls container images and start the requires containers.

    #### 3. Container Runtime: 

   The container runtime is the software that executes containerized applications within Pods. Kubernetes supports multiple runtime options, including

    - containerd
    - CRI-O
    - Docker Engine

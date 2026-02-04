# Kubernetes (K8s)

## Kubernetes Cluster
- A **cluster** is a collection of **nodes** that work together to run containerized applications.
- All nodes in a cluster run Kubernetes components and are managed centrally.

---

## Control Plane vs Worker Nodes

1. Developers interact with the **Control Plane** using declarative configurations (YAML).
2. The Control Plane continuously ensures the **desired state** matches the **current state**.
3. Workloads actually run on **Worker Nodes**.

---

## Kubernetes Terminology

### Nodes
- A **node** is a machine (physical or virtual) that runs Kubernetes.
- Types of nodes:
  - **Control Plane Node**
  - **Worker Node**

---

## Control Plane Node

The Control Plane manages the entire cluster and makes global decisions.

### Core Components

#### 1. kube-apiserver
- The **entry point** to the Kubernetes cluster.
- Handles all requests from:
  - `kubectl`
  - UI dashboards
  - Automation tools
- Validates and processes REST API requests.

--- 

#### 2. etcd (Distributed Key-Value Store)
- The **single source of truth** for the cluster.
- Stores:
  - Cluster configuration
  - Secrets and credentials
  - Desired and current state of workloads
- Highly available and strongly consistent.

---

#### 3. kube-scheduler
- Decides **which worker node** a Pod should run on.
- Considers:
  - Resource availability (CPU, memory)
  - Node affinity and anti-affinity
  - Pod affinity and anti-affinity
  - Taints and tolerations
- **Does not run Pods**, only selects nodes.

**Affinity**
- Defines where a Pod *prefers* to be scheduled.

**Anti-Affinity**
- Defines where a Pod *should not* be scheduled.

---

#### 4. kube-controller-manager
- Runs controllers that continuously watch cluster state.
- Ensures the desired state is maintained, such as:
  - Restarting failed Pods
  - Scaling workloads
  - Maintaining replica counts for Deployments
- Works on a reconciliation loop.

---

#### 5. cloud-controller-manager (Cloud Environments Only)
- Integrates Kubernetes with cloud provider services.
- Handles:
  - Provisioning cloud load balancers
  - Managing persistent storage volumes
  - Adding or removing nodes dynamically

---

## Worker Node

Worker nodes run application workloads.

### Components

#### 1. kubelet
- The main node agent.
- Communicates with the API Server.
- Responsibilities:
  - Starts and stops containers
  - Pulls container images
  - Ensures Pods match their specifications

---

#### 2. kube-proxy
- Manages **network rules** on each node.
- Enables communication between:
  - Pods
  - Services
  - External traffic
- Implements Services using:
  - iptables or IPVS
- **Does not perform actual load balancing logic**

---

#### 3. Container Runtime
- Executes containers inside Pods.
- Kubernetes uses **CRI-compatible runtimes**, such as:
  - `containerd`
  - `CRI-O`
- Docker Engine is **not used directly** (removed in Kubernetes v1.24).

---

## Kubernetes Objects

### Pod
- Smallest deployable unit in Kubernetes.
- A Pod can contain one or more containers that share:
  - Network namespace
  - Storage volumes

---

### ReplicaSet
- Ensures a specified number of Pod replicas are running.

---

### Deployment
- Manages ReplicaSets.
- Supports:
  - Rolling updates
  - Rollbacks
  - Scaling
- Role of deployment
Deployment ensures that there is a smooth deployment, and if the new image fails for some reason, the old replicaset is maintained.
Even though the rs is what does pod management , deployment is what does rs management


#### Checkout the history of deployment
```
kubectl rollout history deployment/nginx-deployment
```


#### Undo the last deployment
```
Kubectl rollout undo deployment/nginx-deployment
```

---

### Service
- Provides a **stable network endpoint** for Pods.
- Enables internal and external access.

---

## Commands

### kind
- Runs Kubernetes **inside Docker containers**.
- Commonly used for local clusters.

```bash
kind create cluster -f cluster.yml
```

### kubectl

Command-line tool to interact with **the Kubernetes API Server**.
```
kubectl get pods
kubectl get replicasets
kubectl get deployments
kubectl describe pod <pod-name>
kubectl apply -f pod.yaml
kubectl run nginx --image=nginx
```


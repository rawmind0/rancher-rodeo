## Introduction

---

###  What is a container?

A container...
- is an isolated and limited context into a host OS shared kernel.
- generates a new namespace in the host OS kernel.
- has own resources of CPU, memory, network and storage.
- has just one OS dependency to run, container runtime.
- has near native performance, almost NO overhead
- execute only one app.
- contains all software and dependencies required to run inside app.
- is reproducible, portable, versionable and immutable.

---

###  Is a container like a VM?

Short answer is NO...
- Container = context (shared kernel) vs VM = virtualization (hypervisor)
- Containers are built to do specific tasks, VMs to do generic tasks.
- Container has near native performance, almost NO overhead.
- Container package all software requirements and dependencies needed to run the app.
- Containers are immutable, versionable and portable.

---

###  Why use containers?

Using containers...
- VMs don't need to manage dependencies, just container runtime.
- a clean, safe, hygienic & portable runtime env is available for your app.
- immutable versions of libraries and other dependencies for each app are packaged.
- build your app once, run anywhere.
- scale dynamically and horizontally.
- automate testing, integration, packaging...anything you can script.
- upgrade with no downtime.

---

### What is Docker?

- Docker is a container platform used to develop, deploy and execute dockerized app’s.
- Docker encapsulate everything needed to run a program in an isolated state.
- A docker is not a VM, it shares kernel with a existing Linux OS and Docker runtime.
- Dockers are processes in an os, that are isolated from each other by means of virtual filesystems, PID namespaces, virtual networks, cgroups, etc.

---

### Docker architecture

<img src="slides/intro/images/docker-schema.jpg", style="width:600; height:auto; background-color:white; float:center;"/>

---

### What is Kubernetes?

K8s...
- is a portable, extensible open-source platform for managing containerized workloads and services.
- facilitates both declarative configuration and automation.
- has a large, rapidly growing ecosystem.
- services, support, and tools are widely available.

---

### Kubernetes architecture

K8s has 3 distinct planes for its services:
- Etcd plane: etcd service that provides persistence to k8s cluster data.
- Control plane: k8s/Rancher stateless components which orchestrate and manage the Compute Plane.
- Worker plane: real workload (k8s pods), orchestrated and managed by control plane.

For production, running each plane on dedicated physical or virtual hosts is recommneded. For development, overlapping planes may be used to simplify management and reduce costs.

---

#### Kubernetes Overlapping planes

Characteristics
- Simple, low-cost environment for ephemeral and training
- Data plane and control plane resilient to minority of hosts failing
- Worker plane resiliency depends on the deployment plan
- Potential performance issues with etcd/k8s components

---

#### Kubernetes Overlapping planes

Instructions
- Create 3 hosts with >=1 CPU and >=4GB RAM.
- Create RKE template with 3 roles at every node.
- Deploy RKE cluster.

---

#### Kubernetes Overlapping planes
<img src="slides/intro/images/overlapped_planes-scheme-v2.0.svg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

#### Kubernetes Separated planes

Characteristics
- Data plane resilient to minority of hosts failing.
- Control plane resilient to all but one host failing.
- Worker plane resiliency that is dependent on the deployment plan.
- High-performance, production-ready environment.

---

#### Kubernetes Separated planes
Instructions
- Create 7 hosts with >=1 CPU and >=4GB RAM.
- Create RKE template with
  - 3 nodes with etcd role.
  - 2 nodes with controlplane role.
  - 2 nodes with worker role.
- Deploy RKE cluster.

---

#### Kubernetes Separated planes

<img src="slides/intro/images/separated_planes-scheme-v2.0.svg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

### What is Rancher?

Rancher... 
- is a portable, extensible open-source platform for managing k8s clusters and services. 
- makes it easy for DevOps teams to test, deploy and manage their applications.
- is used by operations teams to deploy, manage and secure every Kubernetes deployment regardless of where it is running.

---

### Rancher 2.x architecture

Rancher has 2 distinct components for its services:
- Management: Rancher server services, used to manage and operate k8s cluster.
- K8s components: 
  - cluster agent: running at every k8s cluster to get resources data.
  - Node agent: running each node to get resources data.

For production, running management on HA is recommended. 
For development, running management on standalone node is supported.

---

### Rancher 2.x architecture
<img src="slides/intro/images/rancher-diagram-v2.0.svg", style="width:auto; height:auto; background-color:white; align:center;"/>

---

### Rancher 2.x HA architecture
<img src="slides/intro/images/rancher-diagram-HA-v2.0.svg", style="width:auto; height:auto; background-color:white; align:center;"/>

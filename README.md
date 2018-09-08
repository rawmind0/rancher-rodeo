# rancher-rodeo

# Prerequisites
* Machine with 8GB RAM, SSD – Run 1 rancher server and 3 nodes (change the RAM size)
* 5 VMs running in Cloud (2GB each, ensure security group has TCP 22, 80, 443, 2376, 2379-2380,  6443, 9099, 10250-10252, 10254, 10256 & 30000-32767 and UDP 4789, 8472 & 30000-32767 open. Recommend all traffic on UDP and TCP allowed in local network)

**[Node requirements](https://rancher.com/docs/rancher/v2.x/en/installation/requirements/)**
**Run Docker 1.12.6 or 17.03.2 if you want the K8s demo to work!**

# Node roles
* 1 VM for running rancher server
* 3 VMs for running k8s cluster
* 1 VM for running NFS server

# Vagrant users
* https://www.vagrantup.com/ (For installing Vagrant)
* https://www.mls-software.com/opensshd.html (Windows only, install OpenSSHD on Windows to ensure vagrant can ssh into nodes to do provisioning
* https://github.com/rawmind0/rancher-rodeo (Github repository containing all the necessary files to run your Vagrant setup)
* Get started with:
```
$ git clone https://github.com/rawmind0/rancher-rodeo && cd rancher-rodeo
$ vagrant up
$ vagrant ssh rancherserver
```

# Running Rancher
* Connect to VM for running rancher server
* `sudo docker run -d --restart=unless-stopped \
-p 80:80 -p 443:443 \
rancher/rancher:latest`

# Creating k8s cluster
* Connect to rancher UI
* Add new custom cluster 
* Set node roles `etcd`, `Control Plane` & `Worker`
* Copy generated command
* Run command on all VMs for running k8s cluster
* Wait until cluster gets `active` state
* Access to your k8s cluster and get `kubeconfig file`

# Installing kubectl
* Determine version of kubectl needed by running `kubectl version` in CLI
* Download kubectl version for your platform (macOS/Linux/Windows): [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* If using RancherOS GA on cloud, run: (on Vagrant this is done automatically on `vagrant up`)
  * `sudo ros engine switch docker-1.12.6`
  * `sudo system-docker restart docker`
* Copy your cluster config file to `~/.kube/config`

# Deploying Wordpress from Catalog
* Connect to rancher UI
* Access to your k8s cluster and your project
* Access to `Catalog Apps`-`Launch` and find workpress package
* Set wordpress & mariadb password 
* `Launch`

# Persistent Storage: Setting up the NFS server
* Connect to VM for running NFS server
* `mkdir <NFS_folder>`
* `sudo docker run -d --name nfs --restart=always --privileged --net=host -v <NFS_folder>:/nfsshare -e SHARED_DIRECTORY=/nfsshare itsthenetwork/nfs-server-alpine:4` 
**NB: Update commands with the path to your NFS_folder**

# Persistent Storage: Setting up the NFS class and provisioner
* Go to rancher-rodeo repo root folder
* Create nfs storage class `kubectl apply -f k8s/managed-nfs-storage-class.yaml`
* Deploy nfs client provisioner `kubectl apply -f k8s/nfs-client-provisioner.yaml` **NB: Update the IP address to your NFS server IP address**

# Deploying Wordpress from Catalog using Persistent Storage
* Connect to rancher UI
* Access to your k8s cluster and your project
* Access to `Catalog Apps`-`Launch` and find workpress package
* Set wordpress & mariadb password and `Launch`
* Set `WordPress Persistent Volume Enabled` to true, set `WordPress Volume Size` & set `Default StorageClass for WordPress`
* Set `MariaDB Persistent Volume Enabled` to true, set `MariaDB Volume Size` & set `Default StorageClass for MariaDB`
* `Launch`


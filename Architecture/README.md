# Kubernetes Architecture

Reference Links:

https://www.youtube.com/watch?v=8C_SCDbUJTg&t=119s

![image](https://user-images.githubusercontent.com/63234624/145684973-0c1d9f5a-c7e0-4a13-9a26-b92e6692bb91.png)


# Components

## Control Plane (Master Node)

We can have one or more Master Nodes.

* **Container Runtime**: This contains the container runtime like Docker,Rocket etc.

* **etcd** : This is key value store which has all metadata for Master/Worker nodes and all cluster data which is readily available.

* **Kube Scheduler** : This component is used to schedule Pod's on Worker Nodes. It checks for new Containers/Pods and allocates it to available Worker Node.

* **Kube API Server** : This is API which K8 exposes which is used to interact with K8. Like Kubectl ot any other tools connects to K8 using this API server.
                    All components in Worker nodes interacts with Master Nodes via this API Server component.
                    
* **Kube Controller Manager**: This is control manager which is used to Control running of cluster. It is responsible for Node/Replica/Service working in Cluster.
                           It uses below Control managers to do its working,
                           * Node Controller
                           * Replica Controller
                           * Service Controller


## Worker Node
                           
We can have one or more Worker Nodes

* **Container Runtine**: This contains the container runtime like Docker,Rocket etc.

* **Kubelet** : This is agent which is installed on all worker nodes. This is heart of Worker Nodes.
            This components helps Master node if Node is up and working fine.
            
* **Kube Proxy** : This is Network proxy which runs on all worker nodes. Basically it is used to set Network rules for your Worker Nodes.

![image](https://user-images.githubusercontent.com/63234624/145821807-af57766e-558c-488c-925c-f5f1f2ca2b58.png)

# What are the Node level resources in a Kubernetes cluster?

In any given cluster with multiple nodes, there are a defined set of resources in the form of,

* CPU
* Memory
* Disk Spaces

CPU and memory are collectively referred to as compute resources, or just resources. These resources are measurable quantities that can be requested, allocated, and consumed.

# Unit Of Resources Type:

Each of the above resource types has a base unit, let get into the details of each one by one

1. CPU: CPU represents compute processing and is specified in units of Kubernetes CPU’s.

1 cpu, in Kubernetes, is equivalent to 1 vCPU/Core for cloud providers and 1 hyperthread on bare-metal Intel processors.

If not specified in resource request, by default, Kubernetes allocates 0.5 CPU to the pod or to the containers in the pod.

2. Memory : In Kubernetes requests for memory, resources are measured in bytes. The memory can be represented both as

simple integer values

Fixed point numbers

These both type of represented can use anyone the given: E, P, T, G, M, K

or,

One can also use the power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki

## Let’s understand by simple Example :

![image](https://user-images.githubusercontent.com/63234624/145822318-70a8a313-616e-494a-b8ad-9a862a2b0af3.png)


By default, Kubernetes assumes that any pod or container in the given pod will require 256 Mi of the node memory in which they are residing.


## Example Pod Definition To understand how you can manage resources & limits :

apiVersion: v1

kind: Pod

metadata:

  name: web-app
  
spec:

  containers:
  
  - name: app
  
    image: nginx
    
    resources:
    
      requests:
      
        memory: "128Mi"
        
        cpu: 0.5
        
      limits:
      
        memory: "256Mi"
        
        cpu: 1
        
        
        
        
## Resource specifications in the sample-pod.YAML file:

As can be seen in the YAML file above, we have allocated the resource request parameter along with the limit, by defining in our pod container resources:

resources:

      requests:
      
        memory: "128Mi"
        
        cpu: 0.5

and by defining limits:

limits:

        memory: "256Mi"
        
        cpu: 1

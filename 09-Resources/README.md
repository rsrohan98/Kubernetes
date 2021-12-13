
When it comes to architecting your system infrastructure requirements as a cloud architect or system architect, you need an efficient orchestrating tool to help you achieve the required flexibility and scalability. Kubernetes orchestration platform gives you this ability and simplifies your resource management process hassle-free.
What are the Node level resources in a Kubernetes cluster?
In any given cluster with multiple nodes, there are a defined set of resources in the form of
CPU
Memory
Disk Spaces
CPU and memory are collectively referred to as compute resources, or just resources. These resources are measurable quantities that can be requested, allocated, and consumed.
Unit Of Resources Type:
Each of the above resource types has a base unit, let get into the details of each one by one
CPU :
CPU represents compute processing and is specified in units of Kubernetes CPU’s.
1 cpu, in Kubernetes, is equivalent to 1 vCPU/Core for cloud providers and 1 hyperthread on bare-metal Intel processors.
If not specified in resource request, by default, Kubernetes allocates 0.5 CPU to the pod or to the containers in the pod.
Some examples to simplify unit economics for Kubernetes cpu.
0.1 cpu = 100 m= 1 hundred milli cpu
We can also represent it as 0.2, 0.3, 0.4 but it cannot go below 1 m.
1 vCPU = 1 vCPU on AWS, I GCP core, 1 Azure core, 1 Hyper thread
2. Memory :
In Kubernetes requests for memory, resources are measured in bytes. The memory can be represented both as
simple integer values
Fixed point numbers
These both type of represented can use anyone the given: E, P, T, G, M, K
or,
One can also use the power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki
Let’s understand by simple Example :

256 Mi or it can also be represented as 26843546
123 MI =129 M = 129e6=128974848
By default, Kubernetes assumes that any pod or container in the given pod will require 256 Mi of the node memory in which they are residing.
If you’re using Kubernetes v1.14 or newer, you can specify huge page resources. Huge pages are a Linux-specific feature where the node kernel allocates blocks of memory that are much larger than the default page size.
How Does Kubernetes Manage The Resource Request?
Each pod deployed on the cluster node can be optionally allocated resources like CPU, RAM, etc either by default or based on the resource provisioning defined in the pod definition. Every such request coming from the newly created pod is handled by the node scheduler, so if you have opted to define the resources requirement yourself as an administrator or Kubernetes developer, the scheduler will act according to your pod’s resource request parameters and decides which node will this pod be placed.
If the administrator has defined any resource limit for the container in the pod, the kubelet lying in the node enforces those limits so that the running container is not allowed to use more of that resource than the limit you set.
Example Pod Definition To understand how you can manage resources & limits :
Create your sample pod using the command
$ atom sample-pod.yaml
atom: here is the text editor, you can any text editor of your choice to create the file. After creating this file open this file in atom editor and type the YAML code specified below. Please feel free to make your own resource level provisioning as you want.
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
Resource specifications in the sample-pod.YAML file:
As can be seen in the YAML file above, we have allocated the resource request parameter along with the limit, by defining in our pod container
resources:
resources:
      requests:
        memory: "128Mi"
        cpu: 0.5
and by defining
limits:
limits:
        memory: "256Mi"
        cpu: 1
Let’s go ahead and create this pod.
Create this pod :
$ kubectl apply -f sample-pod.yaml
Let’s View the created pod web-app using the describe command:
$ kubectl describe po web-app

Fig-2
Explanation :
As per our provisioned resources and limits, our container pod has been created as shown in fig-2
So what goes behind when resource provisioning happens :
The moments any request to create Pod is received by the Kubernetes, the K8S scheduler takes the charge to assess the current capacity of the nodes lying in the given Kubernetes cluster, which helps the scheduler to decide the CPU and Memory available at the node’s disposal.
The scheduler has the responsibility to ensure that, for each resource type, the sum of the resource requests of the scheduled Containers is less than the capacity of the node. The scheduler refuses to place a Pod on a node if the capacity check on the available resources fails in that node fails.
This guard against a resource shortage on a node when resource usage later increases, for example, during a daily peak in request rate.
When the CPU & Memory limit is defined against the container, Kubernetes throttles the vCPU , so that container doesn’t go beyond the specified limit in the case of CPU. But when it comes to Memory, Kubernetes allows the container/pod to go beyond the set threshold memory limit, but if the pod continues to breach the limit Kubernetes eliminates the pods form the nodes
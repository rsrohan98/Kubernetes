# NameSpaces

## Read below blog and go through videos mentioned below,

https://ngugijoan.medium.com/understanding-kubernetes-namespaces-c2f81d0b94a5

Go through vides from Gourav for NameSpaces(Video no 34,35,36 )

https://www.youtube.com/watch?v=No0vQcYmNUI&list=PL6XT0grm_TfhFKUv_KI_DTVr0TCincl1r&index=35

## Types of Namespaces

i. Default

ii. Kube-system : This namespace contains all cluster related resources

iii. Kube-node-lease : This namespace contains resources which helps in maintianing heartbeats of Nodes which are sent to Master Node.

iv. Kube-public : This namespace contains resources which can be exposed outside of cluster without any authentication. eg: kubectl cluster-info
                  This can be access eg using Curl or any other exposed appp.
                  
                     kubectl cluster-info
                     
                     O/P: 
                     
                     Kubernetes master is running at https://127.0.0.1:65081
                     
                     KubeDNS is running at https://127.0.0.1:65081/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy



* We have a scenario where one Service is present in one namespace and applications are present in same namespace.
  So application can directly access the service using service name as below

    curl firstservice;

* But if we have  scenario where one Service is present in one namespace and applications are present in other namespace, then
  direct service call will not work. 
  To tackle this K8 provide Service DNS as below. Access service from different namespace using below command,

   curl <<servicename>servicename>. <<namespacename>namespacename>. svc.cluster.local

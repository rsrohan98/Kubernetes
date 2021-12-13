# NameSpaces

## Read below blog and got through videos mentioned below,

https://ngugijoan.medium.com/understanding-kubernetes-namespaces-c2f81d0b94a5

Go through vides from Gourav for NameSpaces(Video no 34,35,36 )

https://www.youtube.com/watch?v=No0vQcYmNUI&list=PL6XT0grm_TfhFKUv_KI_DTVr0TCincl1r&index=35

* We have a scenario where one Service is present in one namespace and applications are present in same namespace.
  So application can directly access the service using service name as below

    curl firstservice;

* But if we have  scenario where one Service is present in one namespace and applications are present in other namespace, then
  direct service call will not work. 
  To tackle this K8 provide Service DNS as below. Access service from different namespace using below command,

   curl <<servicename>servicename>. <<namespacename>namespacename>. svc.cluster.local

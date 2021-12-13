 # Services in Kubernetes

* Check video from Mumshaad on services from udemy
* check video from nana
   https://www.youtube.com/watch?v=T4Z7visMM4E
   

---------------------------------------
Service in K8
---------------------------------------
i. Cluster IP Service --> We can use this service within the Cluster. Default Service , also called as Internal Service

refer ClusterIP-definition.yaml for code

kubectl get services  --> Using IP for the Service generated to connect to the Conatiner in the Pod

curl 172.28.60.0:8000  --> if this does not work use below command

curl $(minikube service firstservice)   --> Connecting service from cluster.

or minikube service myservice

ii. NodePort Service  --> used to connect external world with our POD

curl $(minikube service firstservice)   --> Connecting service from cluster.

or minikube service myservice

iii. LoadBalancer

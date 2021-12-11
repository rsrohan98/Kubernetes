# Pods

* Pod is smallest and base unit in K8. Its nothing but the virtual cover/abstraction over conatiner.Pod can have 1 or more than 1
conatiner running in it. 
Each Pod gets a unique IP hence all conatiners running inside POD share same IP. And Ports available are also same. so if 1 container
 uses por 80 of the host i,e, POD then its not available for other container in that POD.

* Why was it required to have POD in K8. As we know application is run as container so why cant we run directly run contianer on Nodes??

**Answer**

* K8 supports mutiple contianer runtime like DOCKER,ROCKET etc. So if we dont use POD and directly create container in Node using eg. Docker
  then K8 will not be able to support other Conatiner runtime in it.
  - In addition to above point, if we create coantiner in the POD using Docker and if that contianer is destroyed then 
     we can also recrate container with POD with different Conatiner runtime as POD creation file will not be changed.
     
* PORT Mapping 
    If we just directly run conatiner on Node below scenario happens,
      Eg is running Postgress conatiner  --> docker conatiner run --name post1 -p 5000:5432 -e POSTGREES_PASSWORD=abc postgres:latest
      Here in above conatiner Port 5000 of host to mapped/bind to 5432 of coantiner. so 5000 port on host is blocked
      Similarly, -->  docker conatiner run --name post1 -p 5001:5432 -e POSTGREES_PASSWORD=abc postgres:latest.
      Here in above conatiner Port 5001 of host to mapped/bind to 5432 of coantiner. so 5001 port on host is blocked
      Now if we have lot of conatiners running so it difficult to keep track of ports on host.

 So we create POD. In POD we have unique IP and all ports same for that IP. So same postgres application can run on 5000 port on all POD's
 as each POD will have it own netwrok space ane ethernet connection to connect to host.

* Side Car Contianer application
   There might be some POD's which has more than 1 contianer running on it to have eg backup of main conatiner or Synchronize from main 
   conatiner as in DB. this is called sidecar container. These containers share same IP and network namespace so can easliy
   communicate with each other via localhost. eg localhost:80 / localhost:90

* Every POD has a Pause container which stores all n/w or ports related info with it.so even if main container is lost/destroyed
  and newly created it will get same Ip for POD. but if POD is gone then new POD is created and gets new IP.


Reference Link:

https://www.mirantis.com/blog/multi-container-pods-and-container-communication-in-kubernetes/
https://www.youtube.com/watch?v=5cNrTU6o3Fw


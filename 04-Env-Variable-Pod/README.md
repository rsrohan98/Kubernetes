# Commands

* kubectl exec -it myfirstpod /bin/bash  ( we consider only 1 container in the pod)

* kubectl exec -it secondpod -c <container_name> /bin/bash (as we consider we have more than one container in pod and we want to enter into specific container)

* kubectl exec -it mypod env ( this gives you all env variables for the POD)

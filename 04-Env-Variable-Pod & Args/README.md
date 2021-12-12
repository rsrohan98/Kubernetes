# Commands

* kubectl exec -it myfirstpod /bin/bash  ( we consider only 1 container in the pod)

* kubectl exec -it secondpod -c <container_name> /bin/bash (as we consider we have more than one container in pod and we want to enter into specific container)

* kubectl exec -it mypod env ( this gives you all env variables for the POD)

if we have to change command in a container that runs in a pod, use [args:] option in Yaml file.
Refer argspod.yml for reference

in Docker image file we have below 2 commnads,

-- ENTRYPOINT["sleep"] --> this is command that is fired when container starts
-- CMD["5"] --> this when used with ENTRYPOINT can act as argument to command mentioned in ENTRYPOINT. 
                CMD is the command that run in container as process which keeps container alive.

So in POD definition filw, if we have replace above 2 for iamge used to run conatiner , use below,

-- command --> used to overwrite ENTRTYPOINT of image 
-- args    --> used to overwrite CMD of image
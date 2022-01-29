# Lables: Used as labels in filtering or identifying. eg: among 100 POD's which POD is for DEV /SAS project etc.


Reference Links: https://devops4solutions.medium.com/kubernetes-labels-and-annotation-3bb0a5a22193
                 https://ishanul.medium.com/importance-of-labeling-and-annotating-your-kubernetes-objects-dee5d18d741c
                 
* kubectl label pod pod-with-labels app=nginx1 --overwrite

* kubectl label pod pod-with-labels env=dev

* kubectl label pod pod-with-labels team=dev org=abc

* kubectl label pod pod-with-labels env- (Here to delete label we give minus sign at end of label name)

* kubectl label pods --all proj=UBS (Giving labels to all POD's in current Namespace)

** Selecting Kubernetes Objects Using Label Selectors:

kubectl get pods -l app=nginx1

kubectl get pods -l app=nginx1,foo=bar

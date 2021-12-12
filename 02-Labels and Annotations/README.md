# Lables: Used as labels in filtering or identifying. eg: among 100 POD's which POD is for DEV /SAS project etc.


Reference Links: https://devops4solutions.medium.com/kubernetes-labels-and-annotation-3bb0a5a22193

                 https://ishanul.medium.com/importance-of-labeling-and-annotating-your-kubernetes-objects-dee5d18d741c
                 

kubectl label pod mypod3 env=DEV

kubectl label --overwrtie pod mypod3 env=PROD

kubectl get pods -o wide --show-labels

kubectl label pods podname label_name- (Here to delete label we give minus sign at end of label name)

kubectl label pods --all proj=UBS (Giving labels to all POD's in current Namespace)

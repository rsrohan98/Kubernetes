# Replication Controller

Replication controller, also termed as rc in short, is a wrapper on pod. 

The replication controller provides an additional functionality to the pods which is providing replicas.

The replication controller monitors pods and automatically restarts them if they fail. Also, if the whole node fails, the replication controller respawn all the pods of that 

node on some different node whereas in case of pods, once they dies, they won’t be spawn again unless and until they are wrapped around replication controller or replica set.

The scope of replication controller is decided by the label-selectors. Whichever pod matches its label with the provided selector, that will be managed by the replication 

controller.

A replication controller continuously monitors the list of running pods by running a reconciliation loop and ensures that the specified number of replicas are always running. It 

maintains the replicas in two ways:

By creating new replicas if the actual replicas are less than the desired replicas, and By removing extra replicas if the actual replicas are more than the desired replicas. 

This can be possible if,A pod is created of the same type manually.A label of an existing pod’s changes to a value which is same as the replication controller label-selector.

Someone decreases the desired number of pods. Replication Controller manifest Just as pod, the replication controller also has a spec file which, in addition to podSpecs defines the required number of replicas as shown below:

---

apiVersion: v1

kind: ReplicationController

metadata: 

  name: nginx-rc
  
spec:

  replicas: 3
  selector:
  
    app: nginx
    
    tier: dev
    
  template: 
  
    metadata:
    
      name: nginx
      
      labels: 
      
        app: nginx
        
        tier: dev
        
    spec:
    
      containers:
      
      - name: nginx-container
      
        image: nginx
        
        ports:
        
        - containerPort: 80
        
        
The manifest file of replication file consist of the following fields:

_apiVersion_ : This field specifies the version of kubernetes Api to which the object belongs. ReplicationController belongs to v1 apiVersion.

_kind_ : This field specify the type of object for which the manifest belongs to. Here, it is ReplicationController.

_metadata_ : This field includes the metadata for the object. It mainly includes two fields: name and labels of replication controller.

_spec_ : This field specifies the label selector to be used to select the pods, number of replicas of the pod to be run and the container or list of containers which the pod will run. In the above example, we are running 3 replicas of nginx container.

As I told before, the replication controller ensures that the actual pods always match the desired pods, we can verify the same by deleting a running pod controlled by replication controller manually and the replication controller will automatically spawn a new pod to meet the desired state. Here’s an example:

# Get the pod replicas:

kubectl get pods

# Delete any pod in replication controller fetched from previous cmd:

kubectl delete pod nginx-rc-haShCoDe

# Get the pod replicas again:

kubectl get pods
Here, you’ll see that a new pod has spawned with a different podname.

Also, inside the spec, if we didn’t put the selector, the replication controller will automatically configure it with the labels of pod, as the pod labels must be same as the replication controller selectors, otherwise the pods will move out of the scope of replication controller.

# kubectl commands for replication controller

Create a ReplicationController:

kubectl create -f nginx-rc.yml

# Get the ReplicationController:

kubectl get rc/nginx-rc

kubectl get rc/nginx-rc -o wide

kubectl get rc/nginx-rc -o yaml

kubectl get rc/nginx-rc -o json

# Describe the ReplicationController:

kubectl describe rc/nginx-rc

# To scale up the replicas:

kubectl scale rc nginx-rc --replicas=5

# To delete the ReplicationController:

1. kubectl delete rc nginx-rc

2. kubectl delete -f nginx-rc.yml 

Now, let’s see what new we have in replica set.

# Replica Set

Replica set, also termed as rs in short, is almost same as the replication controller is, only with a single difference. The replica set are also known as next generation 

replication controller. The only difference between replica set and replication controller is the selector types.

The replication controller supports equality based selectors whereas the replica set supports equality based as well as set based selectors.

## Equality based Selectors

Equality based selectors allow filtering by label keys and values. Matching objects must satisfy all of the specified label constraints, though they may have additional labels as well. 

Three operators used in set based equality based selectors are = , == , !=. The first two represent equality (and are simply synonyms), while the latter represents inequality. 

For example, if we provide the following selectors:

env = prod

tier != frontend

Here, we’ll select all resources with key equal to environment and value equal to production. The latter selects all resources with key equal to tier and value distinct from 

frontend, and all resources with no labels with the tier key.

One usage scenario for equality-based label requirement is for Pods to specify node selection criteria.

## Set Based Selectors

Unlike Equality based, Set-based label selectors allow filtering keys according to a set of values.

Three kinds of operators used in set-based selectors are in , notin, exists(only the key identifier).

For example, if we provide the following selectors:

env in (prod, qa)

tier notin (frontend, backend)

partition

Here, in the first selector will selects all resources with key equal to environment and value equal to production or qa.

The second example selects all resources with key equal to tier and values other than frontend and backend, and all resources with no labels with the tier key. The third example selects all resources including a label with key partition; no values are checked.

The set-based label selector is a general form of equality since environment=production is equivalent to environment in (production). Similarly for != and notin.

# Replica Set manifest

Just as replication controller, the replica set has a same spec file with the difference in the as shown below:

---

apiVersion: apps/v1

kind: ReplicaSet

metadata: 

  name: nginx-rs
  
spec:

  replicas: 3
  
  selector:
    matchLabels:
    
      env: prod
      
    matchExpressions:
    
    - { key: tier, operator: In, values: [frontend] }
    
  template:
  
    metadata:
      name: nginx
      
      labels: 
        env: prod
        
        tier: frontend
        
    spec:
    
      containers:
      
      - name: nginx-container
      
        image: nginx
        
        ports:
        - containerPort: 80
        
In the above spec file, under the selector, I’ve used matchLabels and matchExpression to specify the key value pair. The matchLabel works exactly same as the equality based selector, and the matchExpression is used to specify the set based selectors.

Also, the apiVersion of replicaSet is apps/v1. It weren’t there in the initial apiVersion and the kind is ReplicaSet.
Rest all is same as the replication controller.

## kubectl commands for replication set.

* Create a ReplicaSet:

kubectl create -f nginx-rs.yml

* Get the ReplicaSet:

kubectl get rs/nginx-rs

kubectl get rs/nginx-rs -o wide

kubectl get rs/nginx-rs -o yaml

kubectl get rs/nginx-rs -o json

* Describe the ReplicaSet:

kubectl describe rs/nginx-rs

* To scale up the replicas:

kubectl scale rs nginx-rs --replicas=5

* To delete the ReplicaSet:

1. kubectl delete rs nginx-rs
2. kubectl delete -f nginx-rs.yml

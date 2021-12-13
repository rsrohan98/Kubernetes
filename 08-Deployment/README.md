-----------------------------------------------------
Deployment
-----------------------------------------------------

Kubernetes has 2 types of Deployment stratergy


i. RollingUpdate --> This is default startegy. In this while rollout , 1 pod gets delete and 1 pod get created.


ii. Recreate --> in this all pods at once gets deleted and all at once Pods are created.
                 This has drawback that it gives downtime while deployment.

In deployment we have some important options as listed below,


i.  maxUnavailable  --> This decides while deployment how many POD's at a time can be destroyed and created.

                        Default value is 25%.

                        We can give interger or percentage as value

ii.  MaxSurge       --> This allows how many extra POD is max allowed while deploymennt . This is used when

                        any application does not want no of replicas to decrease ant any give point in time.

                        Default value is 25%.

iii. minReadySeconds   --> This gives you what the min time in seconds we think to that the POD can take to be LIVE.


# Deployment Commands

* kubectl apply -f deployment.yml

* kubectl rollout  --> This give all available option for rollout

* kubectl rollout status deployment deployment_name  ( Shows the Status of Deployment)

* kubectl rollout historty deployment deployment_name ( Shows History of Deplopyment)


## Rollout Undo

* kubectl rollout undo deployment deployment_name  -- > This rollbacks your application to just previous version

* kubectl rollout undo --to-revision=2 deployment deployment_name  --> This rollbacks your application to desired version(revision)

* kubectl rollout pause deployment deployment_name

* kubectl rollout resume deployment deployment_name


So after Deployment we think that now deployment is ok but some changes are wrong and we want to rollback our deployment.
In this case we can follow below steps

.. Check the history of deployment

* kubectl rollout history  deployment <deployment_name> ( this gives you revision_no and change_comment columns)

now based on the o/p of above command we can run below command

* kubectl rollout undo deployment <deployment_name> ( this command rollbacks your deployment to immediate previous version of app)

But if we want to rollack to any specific revision_version , then use below command

kubectl rollout undo --to-revision=2 deployment <deployment_name>

....

Whenever you do Rollout and check history with below command, we get revision_no and change-comments.

Generally Change-cause are NULL by default. so it becomes very difficult to track from history what all changes happended  for every rollout.
  
So to handle this, we can use below 2 options
 

* kubectl rollout history deployment <deployment_name>  ( this give history of deployment)

* kubectl apply -f deploy.yml --record=true ( this records the last commnad which is the same command itself and displays it in 
                                                Change-cause column. But this is of no use as such)

So to give proper commands, edit deployment.yml file and add _"kubernetes.io/change-cause: 'My changes'" in "Annontation"_ section with proper comments in Metadata section. 

This will give exact meaning of deployment and will be shown in Change-cause column in history command.


* By Default Revision History if Max=10, if we have to change, follow below

revisionHistoryLimit: 20  in spec or any no. inplace of 20. 

### In K8 when we create POD's we can specify how much resources(memory i.e RAM and CPU) that POD approx needs.

eg: in YAML file under image we can speicfy,

resources:

  request:

    memory: 200Mi

    cpu: 2

Also this above is minimum requirement. But sometimes POD can take over all of resources on Node.

To restrict that we can use limit as 

resources:

  request:

    memory: 200Mi

    cpu: 2

  limit:

    memory: 1Gi

    cpu: 5


This is Max that can be used but the POD.

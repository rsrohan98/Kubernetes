# ConfigMaps

ConfigMaps are Kubernetes objects that allow you to separate configuration data/files from image content to keep containerized applications portable.

ConfigMaps bind configuration files, command-line arguments, surroundings variables, port numbers, and alternative configuration artifacts to your Pods containers and system parts at run-time.

ConfigMaps are helpful for storing and sharing non-sensitive, unencrypted configuration data. 

Like Secrets, you’ll be able to produce config maps from files and with yaml declaration.

we are able to use config maps by relating its name and as a volume.

![image](https://user-images.githubusercontent.com/63234624/145948897-6bb5e0f0-43e1-4d43-a37e-a64abc9f2987.png)

## Create a configmap:

You can create config maps from directories, files, or literal values using kubectl create configmap.

/* Creating ConfigMap manually */

* kubectl create configmap c1 --from-literal=database_id="root" --from-literal=database_pwd="abc"

* kubectl describe cm C1

/*Creating configmap from file/files*/

* kubectl create configmap c2 --from-file=application.properties

* kubectl create configmap c3 --from-file=application.properties --from-file=superadmin.properties (More than one file )

If we have many files then above command becomes difficult. 

/* Creating configmap using directory */

* kubectl create configmap c4 --from-file=/app/sas_dev/application/

/* Creating Configmap as ENV file */

* kubectl create configmap c5 --from-env-file=abc.sh

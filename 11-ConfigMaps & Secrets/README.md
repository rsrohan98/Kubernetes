ConfigMaps are Kubernetes objects that allow you to separate configuration data/files from image content to keep containerized applications portable.

ConfigMaps bind configuration files, command-line arguments, surroundings variables, port numbers, and alternative configuration artifacts to your Pods containers and system parts at run-time.

ConfigMaps are helpful for storing and sharing non-sensitive, unencrypted configuration data. 

Like Secrets, you’ll be able to produce config maps from files and with yaml declaration.

we are able to use config maps by relating its name and as a volume.
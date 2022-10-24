* Let's assume we have nginx.conf file at /tmp directory in one of the worker nodes and we need to volume mount this file to all of the worker nodes. 
  - ```docker config create nginx-conf /tmp/nginx.conf```
* By running the above command, a config-object will be created and the contents of that config-object will be accessible from all of the nodes of the cluster. 
* while creating the service, run ```docker service create --replicas=5 --config nginx-conf nginx```
  - Now, a file named nginx-conf will be created at the root(/) directory of each worker nodes by default.
* But, If we need to place it to a specific location in the worker nodes, run the following:
  - ```docker service create --replicas=4 --config src=nginx-conf,target="/etc/nginx/nginx.conf" nginx```
* To remove a config-object from a service,
  - ```docker service update --config-rm nginx-conf nginx```
  - ```docker config rm nginx-conf```
* remove an existing config of any servcie and add a new config
  - create a new config-object ```docker config create nginx-conf-new /tmp/nginx-new.conf```
  - remove the old config and add the new ```docker service update --config-rm nginx-conf --config-add nginx-conf-new nginx```

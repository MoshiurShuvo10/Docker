## Replicated service mode
   - ```docker service create --replicas=5 web``` creates 5 replicas and distributes them equaly to all of the available worker nodes. It is the default mode of services. 
   - To check service mode: ```docker service inspect web --pretty | grep -i "service mode" ```


## Global service mode
   - ```docker servcie create --mode=global filebeat``` It creates one instance of filebeat to all of the worker nodes. When the node gets destroyed, the filebeat service also gets destroyed. Its not distributed to other available nodes. 
   - If any nodes is added to the cluster, one instance of filebeat will be automatically be replicated to the newly added node.

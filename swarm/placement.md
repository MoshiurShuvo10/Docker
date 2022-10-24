* We can configure containers to be placed in a specific type of worker nodes. 
  - Let's assume we have 3 types of containers. container1- web server, container2-Batch Processing, container3-Realtime data analytics.
  - 3 types of worker nodes. worker1-high cpu, worker2-hign memory, worker3-general purpose server.

* To do this, first add label to the worker nodes
  - ```docker node update --label-add type=cpu-optimized worker1```
  - ```docker node update --label-add type=momory-optimized worker2```
  - ```docker node update --label-add type=general-purpose worker3```

* Then place the containers according to labels
  - ```docker service create --constraint=node.labels.type==cpu-optimized batch-processing```
  - ```docker service create --constraint=node.labels.type==memory-optimized realtime-data-analytics```
  - ```docker servcie create --constraint=node.labels.type=general-purpose web-server```

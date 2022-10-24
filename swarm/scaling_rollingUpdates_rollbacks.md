## Scaling
* Create a service to one worker node

    ```docker service create -p 80:80 web```
* Scale up. Create 3 replicas. Now 3 instances of web will be created and distributed to 3 nodes of the cluster. ```docker service update --replicas=3 -p 80:80 web```
* Scale down. ```docker service update --replicas=1 -p 80:80 web```

## Rolling Update
* ```docker service update -p 80:80 --image=web:v2 web``` This command updates the image of the container web one by one. 
* ```docker service update -p 80:80 --update-delay 60s --image=web:v3 web``` updates image to the containers one by one but withing a time interval of 60s.
* ```docker service update -p 80:80 --update-paralelism 3 --image=web:v3 web``` Update parallely 3 containers

## On update failures | Rollback
* ```docker service update -p 90:90 --update-failure-action pause|continue|rollback --image=web:v2 web``` 
  - update failure action can be any of the 3 [pause/continue/rollback]
* ```docker service update --rollback web```
  - rollback all updates 

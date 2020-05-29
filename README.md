# Docker-KodeKloud
* What is the version of Docker Server Engine running on the Host?
```
docker --version
```
* How many images are available on this host?
```
docker images
```
* Run a container using the redis image
```
docker run redis
```
* Stop the container you just created
```
docker stop docker_id
```
* How many containers are RUNNING on this host now?
```
docker ps
```
* How many containers are PRESENT on the host now? Including both Running and Not Running ones
```
docker ps -a
```
* Delete all containers from the Docker Host.Both Running and Not Running ones. Remember you may have to stop containers before deleting them.
```
docker pa -a
docker stop cf95 af2b cfb1 b204
docker rm $(docker ps -aq)
```
* You are required to pull a docker image which will be used to run a container later. Pull the image nginx:1.14-alpine. Only pull the image, do not create a container.
```
docker pull nginx:1.14-alpine
```
* Run a container with the nginx:1.14-alpine image and name it webapp
```
docker run --name webapp nginx:1.14-alpine
```
* Delete all images on the host. Remove containers as necessary
```
docker images
docker rmi 89ec 6313 9617 a082 1171
```
* Run an instance of kodekloud/simple-webapp with a tag blue and map port 8080 on the container to 38282 on the host.
```
docker run -t -p 38282:8080 kodekloud/simple-webapp:blue
```
* Run a container named blue-app using image kodekloud/simple-webapp and set the environment variable APP_COLOR to blue. Make the application available on port 38282 on the host. The application listens on port 8080.
```
docker run --name blue-app -e APP_COLOR=blue -p 38282:8080 kodekloud/simple-webapp
```
* Deploy a mysql database using the mysql image and name it mysql-db.
Set the database password to use db_pass123. Lookup the mysql image on Docker Hub and identify the correct environment variable to use for setting the root password.
```
docker run --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
```
* Build a docker image using the Dockerfile and name it webapp-color. No tag to be specified.
```
docker build -t webapp-color .
```
* Run an instance of the image webapp-color and publish port 8080 on the container to 8282 on the host.
```
docker run -p 8282:8080 webapp-color
```
* What is the base Operating System used by the python:3.6 image?
```
docker run python:3.6 cat /etc/*release*
```
* First create a postgress database container called db, image postgres, environmental variable POSTGRES_PASSWORD=mysecretpassword
```
docker run --name db -e POSTGRES_PASSWORD=mysecretpassword postgres
```
* Explore the current setup and identify the number of networks that exist on this system
```
docker network ls
```

* Run a container named alpine-2 using the alpine image and attach it to the none network.
```
docker run --name alpine-2 --network=none alpine
```
* Create a new network named wp-mysql-network using the bridge driver. Allocate subnet 182.18.0.1/24. Configure Gateway 182.18.0.1
```
docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network
```
* Deploy a mysql database using the mysql:5.6 image and name it mysql-db. Attach it to the newly created network wp-mysql-network. Set the database password to use db_pass123. The environment variable to set is MYSQL_ROOT_PASSWORD
```
docker run --name mysql-db --network wp-mysql-network -e MYSQL_ROOT_PASSWORD\=db_pass123 mysql:5.6
```
* Deploy a web application named webapp, using image kodekloud/simple-webapp-mysql. Expose port to 38080 on the host. The application takes an environment variable DB_Host that has the hostname of the mysql database. Make sure to attach it to the newly created network wp-mysql-network
```
docker run --name webapp -p 38080:8080 -e DB_HOST=db_pass123 --network wp-mysql-network kodekloud/simple-webapp-mysql
```
* What location are the files related to the docker containers and images stored? 
```
/var/lib/docker
```
* Run a mysql container named mysql-db using the mysql image. Set database password to db_pass123
Note: Remember to run it in the detached mode.
```
docker run --name mysql-db -d -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
```
* Run a mysql container, map a volume to the container so that the data stored by the container is stored at /opt/data on the host. Use the name : mysql-db and same password: db_pass123 as before. Mysql stores data at /var/lib/mysql inside the container.
```
docker run --name mysql-db -v /opt/data:/var/lib/mysql -d -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
```

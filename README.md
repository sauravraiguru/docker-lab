# Docker-Lab

## 1. Running your first container 
https://labs.play-with-docker.com/

$ docker run ubuntu echo Hello World
Hello World

$ docker run -ti ubuntu bash 
Task: (getting inside container)

root@62deec4411da:/# pwd
/

$ docker container run -t ubuntu top

$ docker run ubuntu ps –ef

$ docker exec -it <mycontainerID> bash

$ Stop, remove/prune etc.



## 2. Exposing a port 
https://hub.docker.com/r/tutum/hello-world

$ docker pull tutum/hello-world

$ sudo docker run -d -p 80 tutum/hello-world

$ sudo docker port d35bf1374e88 80
output: sudo docker port c832a742ec80 80
0.0.0.0:32768

$ curl http://localhost:32768/

## 3. Building your container image 

Dockerfile:

$ vi Dockerfile

--> PASTE BELOW and 'ESC' + 'wq'

FROM ubuntu:latest
RUN apt-get update
WORKDIR /home


$ docker login
--> Enter docker ID/username & password after this.

$ docker build -t <imagename> .
example: docker build -t sauravubuntu .

$ docker tag firstimage YOUR_DOCKERHUB_NAME/firstimage
example: docker tag sauravubuntu:latest sauravraiguru/ubuntu

$ docker push YOUR_DOCKERHUB_NAME/firstimage
example: docker push sauravraiguru/ubuntu


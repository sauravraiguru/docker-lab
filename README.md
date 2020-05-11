# Docker-Lab

https://labs.play-with-docker.com/

$ docker run ubuntu echo Hello World
Hello World

$ docker run -ti ubuntu bash 
# (getting inside container)
root@62deec4411da:/# pwd
/
$ docker container run -t ubuntu top
$ docker run ubuntu ps –ef
$ docker exec -it <mycontainerID> bash

# Stop, remove/prune etc.



2nd-Exercise ( to expose a port )
https://hub.docker.com/r/tutum/hello-world

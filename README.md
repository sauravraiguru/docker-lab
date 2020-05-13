# Docker-Lab

## 1. Running your first container
We will use this Docker Playground link below
https://labs.play-with-docker.com/

Prerequisites: we will need a docker ID, and we can create it from here -
https://hub.docker.com/signup

- Let us run our first ubuntu container and checking few ubuntu commands

`docker run ubuntu -ti bash`

1. Try `ls -lah` command - to check the internal pwd

```console
total 0
drwxr-xr-x    1 root root  18 May 13 11:34 .
drwxr-xr-x    1 root root  18 May 13 11:34 ..
-rwxr-xr-x    1 root root   0 May 13 11:34 .dockerenv
lrwxrwxrwx    1 root root   7 Apr 23 11:06 bin -> usr/bin
drwxr-xr-x    2 root root   6 Apr 15 11:09 boot
drwxr-xr-x    5 root root 360 May 13 11:34 dev
```

2. Try `ps -ef`

```console
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 11:34 pts/0    00:00:00 bash
root         11      1  0 11:34 pts/0    00:00:00 ps -ef
```

3. Try `top` command and `Ctrl + C` after seeing the window

```console
top - 11:43:21 up 29 days, 15:46,  0 users,  load average: 42.53, 26.60, 28.66
Tasks:   2 total,   1 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s): 39.2 us, 54.2 sy,  0.1 ni,  3.2 id,  2.1 wa,  0.0 hi,  1.1 si,  0.0 st
MiB Mem :  32158.2 total,    658.6 free,  26521.2 used,   4978.4 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   4737.6 avail Mem

   PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                                                                                                           
     1 root      20   0    4108   3396   2844 S   0.0   0.0   0:00.04 bash                                                                                                                              
    13 root      20   0    6088   3204   2696 R   0.0   0.0   0:00.00 top

```

Please `exit` command the container bash

-  checking if the docker image is available in environment

`docker image ls`

```console
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

ubuntu              latest              1d622ef86b13        2 weeks ago         73.9MB
```

- Checking if the container is running

`docker container ls --all`

```console
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS                     PORTS               NAMES
69d811f64a3b        ubuntu              "echo Hello World"   8 minutes ago       Exited (0) 8 minutes ago                       ecstatic_kilby
```

- Stop, remove/prune etc.

`docker container stop 1de725f294f7`
<replace with your container ID>

`docker container rm 1de725f294f7`
<replace with your container ID>

Removing the image

`docker image rm -f ubuntu`


## 2. Exposing a port
We will try another web application to see how ports are exposed in containers.

https://hub.docker.com/r/tutum/hello-world
- Pulling the `tutum/hello-world` image from docker hub

`docker pull tutum/hello-world`
- Run the container image on port 80

`sudo docker run -d -p 80 tutum/hello-world`
```console
97dd670032f9348b35e60c7f36132ee3c86c80fbb577605763560b86549147b1
```
- Fetch the external port

`sudo docker port d35bf1374e88 80 `

```console
0.0.0.0:32768
```
- Try the below curl command

`curl http://localhost:32768/`

```console
<html>
<head>
        <title>Hello world!</title>
        <link href='http://fonts.googleapis.com/css?family=Open+Sans:400,700' rel='stylesheet' type='text/css'>
        <style>
        body {
                background-color: white;
                text-align: center;
                padding: 50px;
                font-family: "Open Sans","Helvetica Neue",Helvetica,Arial,sans-serif;
        }

        #logo {
                margin-bottom: 40px;
        }
        </style>
</head>
<body>
        <img id="logo" src="logo.png" />
        <h1>Hello world!</h1>
        <h3>My hostname is 97dd670032f9</h3>    </body>
</html>
```


## 3. Building your container image
Container image is created from a `Dockerfile`
Dockerfile:
- Create the below Dockerfile

`vi Dockerfile`

--> PASTE BELOW and 'ESC' + 'wq'

```
FROM ubuntu:latest
RUN apt-get update
WORKDIR /home
```
- Lets login into the our docker ID (because we have to push image later)

`docker login`

--> Enter docker ID/username & password after this.
- Build the image as per the Dockerfile above

`docker build -t <imagename> .`

example: docker build -t sauravubuntu .
```console
Successfully built 5da0d85aa364
Successfully tagged sauravubuntu:latest
```
- Let us `tag` our image with the path in docker hub repository

`docker tag firstimage YOUR_DOCKERHUB_NAME/firstimage`

example: docker tag sauravubuntu:latest sauravraiguru/ubuntu

- Let us `push` the tagged docker image to the repository

`$ docker push YOUR_DOCKERHUB_NAME/firstimage`

example: docker push sauravraiguru/ubuntu
```console
The push refers to repository [docker.io/sauravraiguru/ubuntu]
13d73eba8900: Pushed
8891751e0a17: Mounted from library/ubuntu
2a19bd70fcd4: Mounted from library/ubuntu
9e53fd489559: Mounted from library/ubuntu
7789f1a3d4e9: Mounted from library/ubuntu
latest: digest: sha256:cc843bde02f1dedc3532f9b64ef359545b37ea5b6bf3d79bf55b47ad2afd3918 size: 1364
```
- You should see your docker image here -

 https://hub.docker.com/repositories

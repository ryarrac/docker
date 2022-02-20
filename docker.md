# Docker Quick Notes

```docker
docker run <image name>
docker run hello-world
```

Overriding default command

```docker
docker run <image name> <Overriding command>
docker run busybox echo hi there
docker run busybox ls
```
List all containers running in docker

```docker
docker ps
```
Ususlly this command may no snhow any output since a docker programme closes immediately after running what it is intended for. Therefore to see this 'ps' command working, we will need to keep some docker programme running in the background.

```docker
docker run busybox ping google.com
```
and then run 
```docker
docker ps
```

To list all containers in your docker
```docker
docker ps --all
```


Connecting from Ubuntu

```sh
ryarra@onbv:~$ docker ps
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied
ryarra@onbv:~$ sudo chmod 666 /var/run/docker.sock
[sudo] password for ryarra:


```

Docker create, start and run

Create simply creates the docker in your local computer and it gives the id of the docker

```docker
docker create hello-world
```
Running the create command will reflect different container id.

To start 

```docker
docker start -a <docker id>
```
If we don't put -a, the outputs of the docker will not be visible in the command prompt..

```sh
ryarra@onbv:~$ docker create hello-world
5514348fddaea46872b15cf5f23e1091c59a6d2e1a916dc202103ee58893d039
ryarra@onbv:~$ docker create hello-world
89dc39b9a909d799c2ecbadb70e1c9e8982454fb2f8a2b6f9971a258c11eeffb
```


To start
```
ryarra@onbv:~$ docker start -a 89dc39b9a909d799c2ecbadb70e1c9e8982454fb2f8a2b6f9971a258c11eeffb
```
> Hello from Docker!
> This message shows that your installation appears to be working correctly.
> 
> To generate this message, Docker took the following steps:
>  1. The Docker client contacted the Docker daemon.
>  2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
>     (amd64)
>  3. The Docker daemon created a new container from that image which runs the
>     executable that produces the output you are currently reading.
>  4. The Docker daemon streamed that output to the Docker client, which sent it
>     to your terminal.
> 
> To try something more ambitious, you can run an Ubuntu container with:
>  $ docker run -it ubuntu bash
> 
> Share images, automate workflows, and more with a free Docker ID:
>  https://hub.docker.com/
> 
> For more examples and ideas, visit:
>  https://docs.docker.com/get-started/
> 

without -a, the output will be like

```sh
ryarra@onbv:~$ docker start  89dc39b9a909d799c2ecbadb70e1c9e8982454fb2f8a2b6f9971a258c11eeffb
89dc39b9a909d799c2ecbadb70e1c9e8982454fb2f8a2b6f9971a258c11eeffb
ryarra@onbv:~$

```

docker run is the combination of both docker create and docker start -a


Once a docker ran, we can rerun it with its id. To see all dockers irrespective of running or stopped status, we can use

```docker
docker ps --all
```
By fetching the docker id of a stopped container, we can rerun the docker again. However, if initially we had given a override command, this new run will also run the same command.

Say, we initially provided the command 
```docker
docker run busybox echo hello world
```
and assume that the docker had an id say <somne id>

if we issue the command

```docker
docker start -a <some id>
``` 
will also echo nhello world. However, if we don't provide `-a`, it will supress the `hello world` part. 

#### Erase the existing containers completely

To completely erase the containers, issue
```docker
docker system prune
```

It should display an warning message and once confirmed, it will erase all docker containers from your local machine. Next time if you want to start it again, it will need to be downloaded again.


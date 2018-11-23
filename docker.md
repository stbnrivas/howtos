# previous concepts 

- docker image: An image of docker is like a class of OOP, you can get from docker image from registry or a Dockerfile

- docker container: An container of docker is like instace of this class, you can get after execute docker run image

- docker cli: you need to learn docker command line interface

- dockerfiles: you need to learn Dockerfile sintax

- docker compose: yout need compose is a tool for defining and running multi-container Docker applications because the app uses multiples stuff like database, source, webserver...


# Docker Installation

```bash
$ dnf install docker-ce
$ sysctlenable docker
$ service docker start
$ service docker stop
```

- have you this installation problem ?

docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.26/containers/create: dial unix /var/run/docker.sock: connect: permission denied.

```bash
	sudo usermod -a -G docker $USER
```














# CLI and Docker Images vs Docker Containers

```bash
$ docker login
$ docker logout
```bash

- docker images is like a class of OOP

```bash
	$ docker image ls || docker image list
	$ docker search centos
		but there isn't way into docker cli to get tags of images
	$ docker pull mariadb
	$ docker history repo/tag
```bash

- instanciate a docker container from a docker image

```bash
	$ docker container run httpd:2.4
	$ docker container run -p 80:80 httpd:2.4
	$ docker container run -p 80:80 -p 443:443 httpd:2.4
	$ docker container run -p 80:80 --detach web-server:1.1 
```

- docker container is like instace of this class

```bash
	$ docker container ls || docker ps
	$ docker stop $CONTAINER_ID
	exit container it won't deleted
	$ docker rm $CONTAINER_ID
	$ docker container run || docker run

		-t --tty 			allocate a pseudo-TTY
		-i --interactive	keep STDIN open
		-d --detach			run a container in background
		-p --publish-list	container ports exposed
 ```bash

- docker command lets us run commands against a running container.

```bash
	$ docker container exec
	$ docker container exec -it $container_id /bin/bash
```

- docker has networks for containers

```bash
	$ docker network ls
	$ sudo ifconfig docker0
	
	docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 0.0.0.0
```

- check docker container status

```bash
	$ docker attach $CONTAINER_ID
	$ docker top $CONTAINER_ID		show top 
	$ docker logs $CONTAINER_ID	
```

- docker container stop

```bash
	docker pause $CONTAINER_ID
	docker stop $CONTAINER_ID
```

- create new image from docker container running

```bash
	$ docker pause $CONTAINER_ID
	$ docker commit $CONTAINER_ID
		=> return $NEW_IMAGE_ID for this container status
	$ docker tag $NEW_IMAGE_ID repo/newimagename
	$ docker restart $CONTAINER_ID
	
	$ docker inspect $CONTAINER_ID	
```

- docker containers don't persist any data if you need persistence need use docker volumes. there are two approaches involved copying a file into a container. copying into container

```bash
	$ docker container cp page.html elegant_noether:/usr/local/apache2/htdocs/
```

But as soon as the container is modified and stopped, all of those changes disappear. Is better to create a connection between files on our local computer (host) and the filesystem in the container. mounting a docker volume


```bash
	$ docker container run  --rm -it --mount type=bind, source=/tmp/data, destination=/data debian stretch
```
ADVICE: also you can use --volume -v flag but is better use --mount over --volume because is consistent with docker swarm

```bash
	$ docker container run --rm -it -v path_out_container:path_into_container
	$ docker container run --rm -it -v /tm/data:/data debian:stretch
	$ docker run -d -p 80:80 --name my-web -v /my-files:/usr/local/apache2/htdocs web-server:1.1
```

























# Dockerfiles Sintax: building docker images using docker file sintax

- workfllow:

write Dockerfile -> build Dockerfile to get Docker Image -> Run Docker Image as Docker Container

- docker has .dockerignore as .gitignore

- you must use versioning into dockerfiles like

```bash
	FROM debian:stretch
	RUN "echo '1' > /version "
```

- when you finish your Dockerfile

```bash
	$ docker image build --tag web-server:1.0 . || $ docker build -t webserver:1.0 .
	$ docker container run -p 80:80 web-server:1.0
```bash

sometimes has to build with cache cause conflict because the cache only is invalidate when there are new version of image. For this cases... build with --no-cache flag


## FROM






# Docker compose


# Docker orchestration
# Docker Installation

we love docker! 

dnf  install docker-ce

- installation problem 

docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.26/containers/create: dial unix /var/run/docker.sock: connect: permission denied.

sudo usermod -a -G docker $USER


$ sysctlenable docker
$ service docker start
$ service docker stop


## CLI and theory Images vs Containers

$ docker login
$ docker logout

- docker images is like a class of OOP

	$ docker image ls || docker image list
	$ docker search centos
		but there isn't way into docker cli to get tags of images
	$ docker pull mariadb

- docker container is like instace of this class

	$ docker container ls || docker ps
	$ docker stop $CONTAINER_ID
	exit container it won't deleted
	$ docker rm $CONTAINER_ID
	$ docker container run || docker run

		-t --tty 			allocate a pseudo-TTY
		-i --interactive	keep STDIN open
		-d --detach			run a container in background
		-p --publish-list	container ports exposed
 
- docker has networks for containers

	$ docker network ls

	sudo ifconfig docker0
	docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 0.0.0.0



### examples docker run/stop

$ docker container run httpd:2.4
$ docker container run -p 80:80 httpd:2.4
$ docker container run -p 9999:80 httpd:2.4
$ docker container run -p 80:80 --detach web-server:1.1 

you can run command into the container that is running.

$ docker container exec
$ docker container exec -it $container_id /bin/bash

check status into machine

$ docker attach $CONTAINER_ID
$ docker top $CONTAINER_ID		show top 
$ docker logs $CONTAINER_ID		show logs

$ docker save current state

$ docker pause $CONTAINER_ID
$ docker commit $CONTAINER_ID
	=> return $NEW_IMAGE_ID for this container status
$ docker tag $NEW_IMAGE_ID repo/newimagename

$ docker history repo/tag
$ docker inspect $CONTAINER_ID


## Dockerfiles: building docker images

write Dockerfile -> build Dockerfile -> get Docker Image -> Run Docker Image as Docker Container

$touch Dockerfile


```docker
FROM httpd:2.4
EXPOSE 80
RUN apt-get update
RUN apt-get install -y fortunes
RUN apt-get update && apt-get install -y fortunes
LABEL maintainer="moby-dock@example.com"
```

$ docker image build --tag web-server:1.0 . || $ docker build -t webserver:1.0 .
$ docker container run -p 80:80 web-server:1.0

sometimes has to build without cache because conflict think apt-get update are cached ...

$ docker build --no-cache 


### data volumes into containers

containers don't persist data!!!

 copy file into container

$ docker container cp page.html elegant_noether:/usr/local/apache2/htdocs/

### copy into Dockerfile

```docker
FROM httpd:2.4
EXPOSE 80
RUN apt-get update && apt-get install -y fortunes
COPY page.html /usr/local/apache2/htdocs/
LABEL maintainer="moby-dock@example.com"
```


 two approaches involved copying a file into a container. But as soon as the container is modified and stopped, all of those changes disappear.


### create a connection between files on our local computer (host) and the filesystem in the container.

docker run -d -p 80:80 --name my-web -v /my-files:/usr/local/apache2/htdocs web-server:1.1 to create a link between the folder /my-files


docker container exec -it my-web /bin/bash


docker run docker_file



## Docker compose
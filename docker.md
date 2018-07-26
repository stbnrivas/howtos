# Docker

docker images is like a class of OOP
docker container is like instace of this class




# docker installation

dnf  install docker-ce

# problem 

docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.26/containers/create: dial unix /var/run/docker.sock: connect: permission denied.

    sudo usermod -a -G docker $USER

# docker enable

sysctlenable docker

# docker start / stop 

service docker start
service docker stop


# docker networks

	docker network ls

	sudo ifconfig docker0
	docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 0.0.0.0



# docker search container

	docker search mariadb

# docker install 

	docker pull mariadb
	docker pull php
	docker pull httpd

# docker list container

docker container ls

# docker run/stop

docker container run httpd:2.4
docker container run -p 80:80 httpd:2.4
docker container run -p 9999:80 httpd:2.4
docker container run -p 80:80 --detach web-server:1.1 



# docker command lets us run commands against a running container.

docker container exec
docker container exec -it $container_id /bin/bash




# docker container files

touch Dockerfile

```docker

FROM httpd:2.4
EXPOSE 80
RUN apt-get update
RUN apt-get install -y fortunes

RUN apt-get update && apt-get install -y fortunes


LABEL maintainer="moby-dock@example.com"
LABEL maintainer="moby-dock@example.com"
```

docker image build --tag web-server:1.0 .

docker container run -p 80:80 web-server:1.0



# data volumes into containers

containers don't persist data!!!

## copy file into container

docker container cp page.html elegant_noether:/usr/local/apache2/htdocs/

## copy from Dockerfile

```docker
FROM httpd:2.4
EXPOSE 80
RUN apt-get update && apt-get install -y fortunes
COPY page.html /usr/local/apache2/htdocs/
LABEL maintainer="moby-dock@example.com"
```


 two approaches involved copying a file into a container. But as soon as the container is modified and stopped, all of those changes disappear.


## create a connection between files on our local computer (host) and the filesystem in the container.

docker run -d -p 80:80 --name my-web -v /my-files:/usr/local/apache2/htdocs web-server:1.1 to create a link between the folder /my-files


docker container exec -it my-web /bin/bash


docker run docker_file


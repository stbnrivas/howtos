# previous concepts

- docker image: An image of docker is like a class of OOP, you can get from docker image from registry or a Dockerfile

- docker container: An container of docker is like instace of this class, you can get after execute docker run image

- docker cli: you need to learn docker command line interface

- dockerfiles: you need to learn Dockerfile sintax

- docker compose: yout need compose is a tool for defining and running multi-container Docker applications because the app uses multiples stuff like database, source, webserver...


# Docker Installation

```bash
dnf install docker-ce
systemctl enable docker

service docker start
service docker stop
```

```bash
echo 'alias docker="sudo /usr/bin/docker"' >> ~/.bashrc
```
add user to use sudo. with visudo

- have you this installation problem ?

docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.26/containers/create: dial unix /var/run/docker.sock: connect: permission denied.

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```


# Docker Custom

customization who cares

```bash
touch ~/.docker/config.json
```

```json
{
  "psFormat": "table {{.ID}}\\t{{.Names}}\\t{{.Image}}\\t{{.RunningFor}}\\t{{.Status}}\\t{{.Ports}}"
}
```




# CLI and Docker Images vs Docker Containers

```bash
docker login
docker logout
```

- docker images is like a class of OOP

```bash
docker image ls || docker image list
docker search centos
	but there isn\'t way into docker cli to get tags of images
docker pull mariadb
docker history repo/tag
```
- instanciate a docker container from a docker image

```bash
docker container run $image:$tag
	# -p --publish			publish list of ports
	# -d --detach			run container in background
	#    --rm 				remove container when exits
	# -e --env				pass environment variable
	#    --env-file list    Read in a file of environment variables

docker container run httpd:2.4
docker container run -p 80:80 -p 443:443 httpd:2.4
docker container run -p 80:80 --detach web-server:1.1

# you can check ss -tunpl
```

- removing images

```bash
# List only your build images
docker images
# List all images
docker images --all
# Delete single image
docker image rmi $IMAGE_ID
# Delete all containers
docker rm $(docker ps -a -q)
# Delete all images
docker rmi $(docker images -q)
```


- docker container is like instance of this class

```bash
docker container ls
docker ps

docker run
docker container run
	-t --tty 			allocate a pseudo-TTY
	-i --interactive	keep STDIN open
	-d --detach			run a container in background

	-p --publish		container ports exposed
		--name $name

		                also can use -p IP:host_port:container_port or -p IP::port

		--link 			some-postgres:postgres
		--network=bridge
docker container run -it -p 3000:3000 --name $container_name  $image_name:$image_tag



docker stop $CONTAINER_ID
# exit container it won\'t deleted
docker rm $CONTAINER_ID
docker rm $CONTAINER_NAME
```

- docker command lets us run commands against a running container.

```bash
docker container exec
docker container exec -it $container_id /bin/bash
docker exec --interactive --tty aaba69ef37ec  /bin/bash
docker exec -u 0 -ti $container_id /bin/bash
```

- docker has networks for containers

```bash
docker network ls
sudo ifconfig docker0

# docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
#    inet 172.17.0.1  netmask 255.255.0.0  broadcast 0.0.0.0
```

- check docker container status

```bash
docker attach $CONTAINER_ID
docker top $CONTAINER_ID
docker logs $CONTAINER_ID
```

- docker container stop

```bash
docker pause $CONTAINER_ID
docker stop $CONTAINER_ID
```

- create new image from docker container running

```
docker pause $CONTAINER_ID
docker commit $CONTAINER_ID
# 	=> return $NEW_IMAGE_ID for this container status
docker tag $NEW_IMAGE_ID repo/newimagename
docker restart $CONTAINER_ID

docker inspect $CONTAINER_ID
```

- removing containers

```bash
docker container ls --all
docker container rm $CONTAINER_ID
# or kill all
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```


- docker containers don't persist any data if you need persistence need use docker volumes. there are two approaches involved copying a file into a container. copying into container

```bash
docker container cp page.html elegant_noether:/usr/local/apache2/htdocs/
```

But as soon as the container is modified and stopped, all of those changes disappear. Is better to create a connection between files on our local computer (host) and the filesystem in the container. mounting a docker volume

```bash
docker container run  --rm -it --mount type=bind, source=/tmp/data, destination=/data debian:stretch
docker container run  --rm -it --mount type=bind, source=/tmp/data, target=/data debian:stretch
```
ADVICE: also you can use --volume -v flag but is better use --mount over --volume because is consistent with docker swarm

```bash
docker container run --rm -it -v path_out_container:path_into_container
docker container run --rm -it -v /home/stbn/Developer/deleteme/:/app ruby:2.6.3
docker container run --rm -it -v /tm/data:/data debian:stretch
docker run -d -p 80:80 --name my-web -v /my-files:/usr/local/apache2/htdocs web-server:1.1
```



- docker volumes creation

```bash
docker volume --help
docker volume create
docker volume inspect
docker volume ls
docker volume rm

docker volume prune
```

copy something from the docker volume to host

```bash
docker cp $volumen_name:/path/into/volume /path/into/host

docker cp $nginx:/etc/nginx/ssl/cert.key ~/certs/
```


- docker networks

default networks in docker are:

 + bridge (default used if not specify, internal private network 172.17.0.0)
 + none
 + host (not multiple container in the same port)

```bash
docker run alpine
docker run alpine --network=none
docker run alpine --network=host
```

```bash
docker run mongo -p 27017:27017
docker port $(docker ps -lq) 27017

```


```bash
ip a | grep docker

#10: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
#    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0



docker network create \
	--driver bridge \
	--subnet 182.18.0.0/16 \
	--gateway 182.18.0.1/16 \
	$network_isolate_name


docker network inspect $network_name

docker network ls

docker network rm $network_name

docker network prune

docker network connect [OPTIONS] $network_id $container_id
docker network connect [OPTIONS] $network_name $container_name


docker run -d --name container1 centos
docker run -d --name container2 centos

docker exec container1 bash -c "ping 172.17.0.3" # success
docker exec container1 bash -c "ping container2" # fail in default network
docker exec container2 bash -c "ping container1" # fail in default network

docker run -d --network new_network --name container3 centos
docker run -d --network new_network --name container4 centos

docker exec container3 bash -c "ping container4" # fail in default network
docker exec container4 bash -c "ping container3" # fail in default network

# --user , -u 		Username or UID (format: <name|uid>[:<group|gid>])
docker exec container5 -u1  /bin/bash -c "ping container3" # fail in default network
```

```yml
version:
services:
	...
volumes:
	...
network:
  network_name:
    driver: bridge
    ipam:
      driver:default
      config:
        - subnet: 172.10.5.0/24
```







- docker container stop

```bash
docker pause $CONTAINER_ID
docker stop $CONTAINER_ID
docker restart $CONTAINER_ID
```

- create new image from docker container running

```bash
docker pause $CONTAINER_ID
docker commit $CONTAINER_ID
#	=> return $NEW_IMAGE_ID for this container status
docker tag $NEW_IMAGE_ID repo/newimagename
docker restart $CONTAINER_ID

docker inspect $CONTAINER_ID
```

- docker containers don't persist any data if you need persistence need use docker volumes. there are two approaches involved copying a file into a container. copying into container

```bash
docker container cp page.html elegant_noether:/usr/local/apache2/htdocs/
```

But as soon as the container is modified and stopped, all of those changes disappear. Is better to create a connection between files on our local computer (host) and the filesystem in the container. mounting a docker volume


```bash
docker container run  --rm -it --mount type=bind, source=/tmp/data, destination=/data debian stretch
```
ADVICE: also you can use --volume -v flag but is better use --mount over --volume because is consistent with docker swarm

```bash
docker container run --rm -it -v path_out_container:path_into_container
docker container run --rm -it -v /tm/data:/data debian:stretch
docker run -d -p 80:80 --name my-web -v /my-files:/usr/local/apache2/htdocs web-server:1.1
```




# Dockerfiles Sintax: building docker images using dockerfile sintax

[dockerfile documentation](https://docs.docker.com/engine/reference/builder/)

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
docker image build --tag web-server:1.0 . ||
OR
docker build -t webserver:1.0 .
docker container run -p 80:80 web-server:1.0

docker image rmi
docker rmi $hash $hash
```

sometimes has to build with cache cause conflict because the cache only is invalidate when there are new version of image. For this cases... build with --no-cache flag to force fully build

## FROM

[search into https://hub.docker.com/explore/](https://hub.docker.com/explore/)

```Dockerfile
FROM debian
```

## WORKDIR

sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD use absolute paths, you can use env variables too

```Dockerfile
WORKDIR /app
```

## COPY

source path are relative to Dockerfile and destination does not haver exist

```Dockerfile
COPY source destination
COPY robots.txt /data/robots.txt
COPY folder /data/
```

## ADD

for internet resources like repo
if resource is local it will be uncompressed for Internet resources unpack or tar gzip it will not uncompressed

```Dockerfile
ADD project.tar.gz
ADD http://example.com/foobar /
```

## RUN

```Dockerfile
RUN touch /tmp/test
```

the commands must be run as dependent commands to build

```Dockerfile
RUN apt-get update && \
	apt-get install -y \
		git \
		curl
```

sometimes there a problem  using RUN because pipe, then use this way

```Dockerfile
RUN /bin/bash -c "set -o pipefail && wget -0 -https://google.com | wc -l"
```

## SHELL

change default shell, specified in JSON format the run will use the new shell

```Dockerfile
FROM microsoft/windowsservercore
SHELL ["powershell","-NoProfile","-Command"]
```

## CMD

there can only be one CMD instruction, if you have more only last will take effect

```Dockerfile
CMD ["executable","param1","param2"] (exec form, this is the preferred form)
CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
CMD command param1 param2 (shell form)
```

## ENTRYPOINT

An ENTRYPOINT allows you to configure a container that will run as an executable.

```Dockerfile
ENTRYPOINT ["executable", "param1", "param2"] (exec form, preferred)
ENTRYPOINT command param1 param2 (shell form)
```

```Dockerfile
ENTRYPOINT ["echo"]
CMD "hello world"
```
## EXPOSE

EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified.

```Dockerfile
EXPOSE 80/tcp
EXPOSE 80/udp
```


## ENV

environment variables, you can set into another file and when build image use the --env-file=file flag

```Dockerfile
ENV var1 value1
ENV var2=value2
```

and you can use variable substitution like bash

$var							value					""
${var}							value					""
${var:+default}					value				default
${var:-default}					default					""

```Dockerfile
ENV MIRROR=http://downloadsoftware.com/ \
	VERSION=9.0.0
RUN curl -SL $MIRROR/version/$VERSION.bin
```

## ARG

works like ENV but only can set one variable and only is available during the build

```Dockerfile
ARG environment=test
COPY ${environment}.conf /app/app.conf
```

```bash
docker build -t demo --build-argument environment=production -f Dockerfile
	-t --tag		tag your image
```


## HEALTHCHECK

return 0 on success or 1 on fail

```Dockerfile
HEALTHCHECK [options] CMD check_command
```

```Dockerfile
HEALTHCHECK --interval=15s CMD /usr/bin/curl -Sf \
	http://localhost || exit 1
```
## dockerfiles examples to ruby containers

```Dockerfile
RUN touch ~/.gemrc && echo "gem: --no-document"
```


## INSPECTION OF DOCKER IMAGE WITHOUT HIS DOCKERFILE

```bash
docker images

# repo-name   	tag      IMAGE_ID    CREATED   		  SIZE
# debian		latest   309dasf03    1 day ago			170Mb

docker image history  $IMAGE_ID
```








# Docker compose

- use a yml file to build services
- docker set a network automatically to containers can connect between each other
- into container you can refer to another using the name given into yml file like an host alias


## docker-compose CLI

```bash
# check sintax
docker-compose config

# setting file
docker-compose -f deploy/docker-compose.yml [config|build|up]


docker-compose build
docker-compose up
# or
docker-compose up --build
docker-compose up --daemon
#
docker-compose down

docker-compose ps


docker-compose up -d --force-recreate web

docker-compose -p project-name up
```


```bash
docker-compose run --rm database psql -U postgres -h database
docker-compose run --rm web bin/rails db:create


docker-compose -p sc-local --file sc-local up
```


```bash
docker-compose exec web \
	bin/rails generate scaffold User first_name:string last_name:string
docker-compose exec web \
	bin/rails db:migrate
```

```bash
docker exec -it <container name> /bin/bash

docker exec -it -u 0 ${container_name} /bin/bash

docker-compose exec web /bin/bash
```


All Docker networks (except for the legacy bridge network) have built-in Domain
Name System (DNS) name resolution. That means that we can communicate
with other containers running on the same network by name

 docker-compose run --rm redis redis-cli -h redis
	-h redis is connect to the host named redis



# volumes in docker-compose

Part of the philosophy of using Docker is that we should treat containers as
ephemeral, we should persist our data creating volume which are decoupled from the life cycle of container.


```bash
docker-compose compose stop database
docker-compose rm -f database
```


```yml
version: '42'
	- services:
		web:
		database:
			image: postgres
			volumes:
				- db_data:/var/lib/postgresql/data
```

```bash
docker-compose up -d database
docker-compose exec web bin/rails db:create db:migrate
```


in linux the data will be placed

/var/lib/docker/volumes/$folder_name_app'\_'$volume_name/\_data




# networking with docker-compose

```yml
version: "3"
services:

  proxy:
    build: ./proxy
    networks:
      - frontend
  app:
    build: ./app
    networks:
      - frontend
      - backend
  db:
    image: postgres
    networks:
      - backend

networks:
  frontend:
    # Use a custom driver
    driver: custom-driver-1
  backend:
    # Use a custom driver which takes special options
    driver: custom-driver-2
    driver_opts:
      foo: "1"
      bar: "2"
```



# Docker orchestration

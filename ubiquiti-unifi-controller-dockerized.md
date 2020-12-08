# unifi controller docker




https://www.youtube.com/watch?v=_fBQVLZl80o


- backup existing unifi controller
- get uid and gid for user running unifi
- install unifi
- restore from backup
- finish config


## backup existing unifi

into existing controller: Settings > Maintenance > Backup > Download Backup (No limit)




https://hub.docker.com/r/linuxserver/unifi-controller


```bash
id
# uid=1000(?) gid=1000(?) ...

docker pull linuxserver/unifi-controller


docker create \
  --name=unifi-controller \
  -e PUID=1000 \
  -e PGID=1000 \
  -e MEM_LIMIT=1024M `#optional` \
  -p 3478:3478/udp \
  -p 10001:10001/udp \
  -p 8080:8080 \
  -p 8081:8081 \
  -p 8443:8443 \
  -p 8843:8843 \
  -p 8880:8880 \
  -p 6789:6789 \
  -v path to data:/config \
  --restart unless-stopped \
  linuxserver/unifi-controller
```



```yml
version: "2"
services:
  unifi-controller:
    image: linuxserver/unifi-controller
    container_name: unifi-controller
    environment:
      - PUID=1000
      - PGID=1000
      - MEM_LIMIT=1024M #optional
    volumes:
      - path to data:/config
    ports:
      - 3478:3478/udp
      - 10001:10001/udp
      - 8080:8080
      - 8081:8081
      - 8443:8443
      - 8843:8843
      - 8880:8880
      - 6789:6789
    restart: unless-stopped
```


When using a Security Gateway (router) it could be that network connected devices are unable to obtain an ip address. This can be fixed by setting "DHCP Gateway IP", under Settings > Networks > network_name, to a correct (and accessable) ip address.





https://localhost:8080
https://localhost:8443



For Unifi to adopt other devices, e.g. an Access Point, it is required to change the inform ip address. Because Unifi runs inside Docker by default it uses an ip address not accessable by other devices. To change this go to Settings > Controller > Controller Settings and set the Controller Hostname/IP to an ip address accessable by other devices.



```bash
docker volume create unifi_data

docker run \
  --name=unifi \
  --restart on-failure \
  -e PGID=1000 -e PUID=1000 \
  -p 3478:3478/udp \
  -p 10001:10001/udp \
  -p 8080:8080 \
  -p 8081:8081 \
  -p 8443:8443 \
  -p 8843:8843 \
  -p 8880:8880 \
  -p 6789:6789 \
  -v unifi_data:/data \
  -v unifi_data:/config \
  --network bridge \
  linuxserver/unifi
```










# unifi controller into docker


## using image  jacobalberty/unifi:stable
docker pull jacobalberty/unifi:stable


mkdir -p unifi-controllers/home
cd unifi-controllers/home

docker run --rm --init -p 8080:8080 -p 8443:8443 -p 3478:3478/udp -p 10001:10001/udp -e TZ='Africa/Johannesburg' -v ~/unifi:/unifi --name unifi jacobalberty/unifi:stable

it doesn't work


id -u $USER

docker run --rm --init -p 8080:8080 -p 8443:8443 -p 3478:3478/udp -p 10001:10001/udp -e TZ='Europe/Madrid' -e RUNAS_UID0='1000' -v ~/unifi-controllers/home:/unifi --name unifi-home jacobalberty/unifi:stable

docker run --rm --init -p 8080:8080 -p 8443:8443 -p 3478:3478/udp -p 10001:10001/udp -e TZ='Europe/Madrid' --user 1000 -e RUNAS_UID0='1000' -v ~/unifi-controllers/home:/unifi --name unifi-home jacobalberty/unifi:stable

sudo docker run --rm --init -p 8080:8080 -p 8443:8443 -p 3478:3478/udp -p 10001:10001/udp -e TZ='Europe/Madrid' --user 1000 -e RUNAS_UID0='1000' -v ~/unifi-controllers/home:/unifi --name unifi-home jacobalberty/unifi:stable

rm: cannot remove '/var/run/unifi/unifi.pid': Permission denied

PROBLEMS

WARNING: Running UniFi in insecure (root) mode
log4j:ERROR setFile(null,true) call failed.

you need pass environment variable

-e RUNAS_UID0='999'





## using image linuxserver/unifi

docker pull linuxserver/unifi:187


The docker create command creates a writeable container layer over the specified image and prepares it for running the specified command. The container ID is then printed to STDOUT. This is similar to docker run -d except the container is never started. You can then use the docker start <container_id> command to start the container at any point.

This is useful when you want to set up a container configuration ahead of time so that it is ready to start when you need it. The initial status of the new container is created.


```bash
PGID = 1000
PUID = 1000

docker create \
  --name=unifi \
  -v /home/stbn/unifi-controllers/home/:/config \
  -e PGID=1000 -e PUID=1000  \
  -p 3478:3478/udp \
  -p 10001:10001/udp \
  -p 8080:8080 \
  -p 8081:8081 \
  -p 8443:8443 \
  -p 8843:8843 \
  -p 8880:8880 \
  -p 6789:6789 \
  linuxserver/unifi
```
>   linuxserver/unifi
0b5c344e996a444ef9b108b4167d83368ac1fecf106b3c6529971fdf52a8f24b

last commnad create docker but need run

docker ps -a

CONTAINER ID    IMAGE               COMMAND    CREATED             STATUS       PORTS   NAMES
0b5c344e996a    linuxserver/unifi   "/init"    5 minutes ago       Created               unifi


docker container restart 0b5c344e996a

docker ps

https://ip:8443,
https://192.168.1.225:8443


Sometimes when using data volumes (-v flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user PUID and group PGID. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" TM.

-e PGID for GroupID - see below for explanation
-e PUID for UserID - see below for explanation


NOT WORK

docker container ls -a
docker container rm unifi

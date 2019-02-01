# unifi controller into docker

https://www.youtube.com/watch?v=_fBQVLZl80o


- backup existing unifi controller
- get uid and gid for user running unifi
- install unifi
- restore from backup
- finish config



# backup existing unifi

into existing controller: Settings > Maintenance > Backup > Download Backup (No limit)


# get uid

get UID and GID

```bash
id
# uid=1000(?) gid=1000(?) ...
```

# installation 

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
  linuxserver/unifi
```

https://localhost:8080
https://localhost:8443
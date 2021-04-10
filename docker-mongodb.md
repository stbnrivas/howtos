# dockerizing mongodb


```
docker pull mongo:4.4-bionic


#attaching to shell:
docker run    --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=secret mongo:4.4-bionic

docker run -d --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=secret mongo:4.4-bionic



mongo --host mongodb0.example.com --port 27017 --username root --password

docker container exec -it $container_id /bin/bash
docker container exec -it $container_id mongo

```


```
sudo apt install mongodb-dev
```


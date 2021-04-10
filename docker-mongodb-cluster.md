# a cluster of mongo db using docker-compose

```yml
version: "3.5"
volumes:
  vol-mongo-cluster-key:
  # not need keep data safe in dev
  # db-data:
networks:
  sc:
    driver: bridge


services:
  mongo_key_generator:
    container_name: mc-keygenerator
    image: depop/openssl-bats
    volumes:
      - vol-mongo-cluster-key:/mongo-conf
    command: 'bash -c "openssl rand -base64 741 > /mongo-conf/key; chmod 600 /mongo-conf/key; chown 999 /mongo-conf/key"'

  mongo_a:
    container_name: mc-node-a
    hostname: mc-node-a
    image: mongo:3.6
    # env_file:
    #   ./mongod.env
    environment:
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=secret
      - MONGO_INITDB_DATABASE=synchronicity
    ports:
      - "27017:27017"
    networks:
      - sc
    volumes:
      - vol-mongo-cluster-key:/opt/mongo-conf
      # - db-data:/data/db
    # command: 'find /opt/keyfile/mongo-keyfile -printf "%m:%f\n"'
    # command: 'whoami'
    command: 'mongod --smallfiles --auth --keyFile /opt/mongo-conf/key --bind_ip_all --replSet synchonicity '
    depends_on:
      - mongo_key_generator

  mongo_b:
    container_name: mc-node-b
    hostname: mc-node-b
    image: mongo:3.6
    # env_file:
    #   ./mongod.env
    environment:
      # - MONGODB_PORT=27017
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=secret
      - MONGO_INITDB_DATABASE=synchronicity
    ports:
      - "27018:27017"
    networks:
      - sc
    volumes:
      - vol-mongo-cluster-key:/opt/mongo-conf
      # - db-data:/data/db
    command: 'mongod --smallfiles --auth --keyFile /opt/mongo-conf/key --bind_ip_all --replSet synchonicity '
    depends_on:
      - mongo_a

  mongo_c:
    container_name: mc-node-c
    hostname: mc-node-c
    image: mongo:3.6
    # env_file:
    #   ./mongod.env
    environment:
      # - MONGODB_PORT=27017
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=secret
      - MONGO_INITDB_DATABASE=synchronicity
    ports:
      - "27019:27017"
    networks:
      - sc
    volumes:
      - vol-mongo-cluster-key:/opt/mongo-conf
      # - db-data:/data/db
    command: 'mongod --smallfiles --auth --keyFile /opt/mongo-conf/key --bind_ip_all --replSet synchonicity'
    depends_on:
      - mongo_a
      - mongo_b


# docker exec -it mc-node-a /bin/bash
# mongo -u root -p
# rs.initiate({
#   "_id":"synchonicity",
#   "members": [
#     {"_id":1,"host":"mc-node-a:27017"},
#     {"_id":2,"host":"mc-node-b:27017"},
#     {"_id":3,"host":"mc-node-c:27017"},
#   ]
# })

# conf = rs.config();
# conf.members[0].priority = 2;
# rs.reconfig(conf)

# use admin;
# db.createUser(
#   {
#     user:"admin",
#     pwd:"secret",
#     roles:[
#       {role:"userAdminAnyDatabase", db:"admin"},
#       {role:"clusterAdmin", db:"admin"}
#     ]
#   }
# )



# docker-compose -p mongocluster --file ./mongodb-cluster.yml build
# docker-compose -p mongocluster --file ./mongodb-cluster.yml up

# docker-compose -p mongocluster --file ./mongodb-cluster.yml --rm up
# docker-compose --file deploy/local/mongodb-cluster.yml up
```
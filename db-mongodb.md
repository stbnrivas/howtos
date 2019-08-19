# mongodb

```bash
apt-get install mongodb-clients

dnf install mongodb
```


```bash
mongo --port 27017
mongo --port 27020
```



# concepts

in mongodb a database is composed by collections
a collection is compose of documents

documents in mongodb are stored in bson format because json support 6 datatypes and bson support more than json


extended json is used to represent bson data types

```bson
{
	"_id": ObjectId("3fd55a56tr577swq44klf3"),
	"startTime": ISODate("2019-06-09T05:44:33.000Z"),
	"pid": NumberLong(934935394394934)
}
```

 
```bash
# mongod is a mongo server
mongod
mongod -version
mongod --port 27017
```


```bash
# mongo shell is a cli
mongo
mongo ds111086-a0.mlab.com:11086/<database> -u <dbuser> -p <dbpassword>
db.version()
```




## mongo shell

```javascript
db.version()

show dbs
/*
admin   0.000GB
config  0.000GB
local   0.000GB
orion   0.000GB
*/
show collections
// empty
use local
// startup_log
db.stats()

show users
```



## crud in mongodb


### database creation

```js
// use $database_name
use test 
// database isn't created yet


// db.createCollection("$collection_name")
db.createCollection("hardware")
// now database is created

show collections
```

### user creation

```js
db.createUser(
{
    user: "dev",
    pwd: "secret",
    roles: [
      { role: "readWrite", db: "synchronicity" }
    ]
})
```


### document operation

```js

// insertOne({})
// insertMany([{},{},{}])
db.hardware.insertOne({id:"laptop-0001"})
db.hardware.insertOne({"id":"laptop-0002"})

db.hardware.insertMany([{id:"laptop-0003"}, {id:"laptop-0004"}])

// find({query})
// findOne({query})
db.hardware.find({})
// { "_id" : ObjectId("5d1d204d704f98cfd98027cc"), "id" : "laptop-0001" }
// { "_id" : ObjectId("5d1d20ea704f98cfd98027cd"), "id" : "laptop-0002" }
db.getCollection('hardware').find({id:"laptop-0001"})
db.getCollection('hardware').find({_id:ObjectId("5d1d204d704f98cfd98027cc")})




db.hardware.findOne({})
// { "_id" : ObjectId("5d1d204d704f98cfd98027cc"), "id" : "laptop-0001" }


```




### mongo cluster with docker

thanks to [https://www.youtube.com/watch?v=-XzMfd4XQak](https://www.youtube.com/watch?v=-XzMfd4XQak)

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
    command: 'mongod --smallfiles --auth --keyFile /opt/mongo-conf/key --replSet synchonicity'
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
    command: 'mongod --smallfiles --auth --keyFile /opt/mongo-conf/key --replSet synchonicity'
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
    command: 'mongod --smallfiles --auth --keyFile /opt/mongo-conf/key --replSet synchonicity'
    depends_on:
      - mongo_a
      - mongo_b

```

build

```bash
docker-compose -p mongocluster --file ./mongodb-cluster.yml build
docker-compose -p mongocluster --file ./mongodb-cluster.yml up
docker-compose -p mongocluster --file ./mongodb-cluster.yml --rm up

docker-compose --file deploy/local/mongodb-cluster.yml up
```

connect to a node to configure

```bash
docker exec -it mc-node-a /bin/bash
mongo -u root -p
```

configure the cluster

```js

rs.initiate({
  "_id":"synchonicity",
  "members": [
    {"_id":1,"host":"mc-node-a:27017"},
    {"_id":2,"host":"mc-node-b:27017"},
    {"_id":3,"host":"mc-node-c:27017"},
  ]
})

conf = rs.config();
conf.members[0].priority = 2;
rs.reconfig(conf)

use admin;
db.createUser(
  {
    user:"admin",
    pwd:"secret",
    roles:[
      {role:"userAdminAnyDatabase", db:"admin"},
      {role:"clusterAdmin", db:"admin"}
    ]
  }
);
```

WARNING:

if you try connect be sure about you are using the same version of mongo and mongod

```bash
mongo --version
mongod --version # into container
```
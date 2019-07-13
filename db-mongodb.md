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
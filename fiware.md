# Fiware

is an opensource initiative definin a universal set of standards for context data management wich facilitate the development of Smart Solutions for different domains such as Smart Cities, Smart Industry, Smart Agrifood and Smart Energy

In any smart solution there is a need to gather and manage context information, processing that information and informing external actors, enabling them to actuate and therefore alter or enrich the current context. The FIWARE Context Broker component is the core component of any “Powered by FIWARE” platform. It enables the system to perform updates and access to the current state of context.

The Context Broker in turn is surrounded by a suite of additional platform components, which may be supplying context data (from diverse sources such as a CRM system, social networks, mobile apps or IoT sensors for example), supporting processing, analysis and visualization of data or bringing support to data access control, publication or monetization.

All interactions between applications or platform components and the Context Broker take place using the FIWARE NGSI RESTful API – a simple, yet powerful open standard.

Usage of the Orion Context Broker is sufficient for an application to qualify as “Powered by FIWARE”.


## Requirements concepts
+iot
+smart cities
+context
+


Fiware Interoperability Mechanism in synchronicity-iot.eu

+Context Management API: access to real time context [link](https://synchronicityiot.docs.apiary.io/reference/context-management-api)
+Shared data models: guidelines and cataloge of common data models in differents verticals [link](https://gitlab.com/synchronicity-iot/synchronicity-data-models)
+Marketplace API: it expose functionalites such catalog management, ordering management [link](https://synchronicityiot.docs.apiary.io/#reference/marketplace-api)
+Security API: API to register and authenticate user and apps to access Synchronicity enabled services [link](https://synchronicityiot.docs.apiary.io/#reference/security-api)
+Data Storage API:  allow to access to historical data and open data of reference zones [link](https://synchronicityiot.docs.apiary.io/#reference/data-storage-api-historical)

(see more at)[https://synchronicity-iot.eu/tech/]



## getting started

git clone git@github.com:FIWARE/tutorials.Getting-Started.git

```bash
docker-compose -p fiware up
```


```bash
curl -X GET 'http://localhost:1026/version'
```

 so lets add some context data into the system by creating two new entities

```bash
curl -X GET 'http://localhost:1026/v2/entities'
# []

curl -iX POST \
  'http://localhost:1026/v2/entities' \
  -H 'Content-Type: application/json' \
  -d '
{
  	"id":"urn:ngsi-ld:Store:001",
  	"type": "Store",
  	"address": {
  		"type": "PostalAddress",
  		"value": {
	  		"streetAddress": "Bornholmer  Straße 65",
	  		"addressRegion": "Berlin",
	  		"addressLocality": "Prenzlauer Berg",
	  		"postalCode": "10439"
  		}
  	},
  	"location": {
  		"type": "geo:json",
  		"value": {
  			"type": "Point",
  			"coordinates": [13.3986, 52.5547]
  		}
	},
	"name": {
		"type": "Text",
		"value": "Bösebrücke Einkauf"
	}
}'

curl -iX POST \
	'http://localhost:1026/v2/entities' \
	-H 'Content-Type: application/json' \
	-d '
{
    "type": "Store",
    "id": "urn:ngsi-ld:Store:002",
    "address": {
        "type": "PostalAddress",
        "value": {
            "streetAddress": "Friedrichstraße 44",
            "addressRegion": "Berlin",
            "addressLocality": "Kreuzberg",
            "postalCode": "10969"
        }
    },
    "location": {
        "type": "geo:json",
        "value": {
             "type": "Point",
             "coordinates": [13.3903, 52.5075]
        }
    },
    "name": {
        "type": "Text",
        "value": "Checkpoint Markt"
    }
}'

```

[Fiware data models ](https://fiware-datamodels.readthedocs.io/en/latest/guidelines/index.html)

check [schema.org](https://schema.org/)
check [geoson.org](http://geojson.org/)

```bash
curl -X GET \
	'http://localhost:1026/v2/entities/urn:ngsi-ld:Store:001?options=keyValues'

curl -X GET \
	'http://localhost:1026/v2/entities?type=Store&options=keyValues'

curl -X GET \
	'http://localhost:1026/v2/entities?type=Store&options=values'

curl -X GET \
  'http://localhost:1026/v2/entities?type=Store&options=keyValues&attrs=id'

# This example return all Stores within 1.5km the Brandenburg Gate in Berlin (52.5162N 13.3777W)

curl -X GET \
	'http://localhost:1026/v2/entities?type=Store&georel=near;maxDistance:1500&geometry=point&coords=52.5162,13.3777'
```


## entities

entities:

*store (tienda)
*product (product)
*shelf (estante de tienda)
*inventary-item (item de inventario)


we are going to create the shelf

```bash
curl -iX POST \
  'http://localhost:1026/v2/op/update' \
  -H 'Content-Type: application/json' \
  -d '{
  "actionType":"APPEND",
  "entities":[
    {
      "id":"urn:ngsi-ld:Shelf:unit001", "type":"Shelf",
      "location":{
        "type":"geo:json", "value":{ "type":"Point","coordinates":[13.3986112, 52.554699]}
      },
      "name":{
        "type":"Text", "value":"Corner Unit"
      },
      "maxCapacity":{
        "type":"Integer", "value":50
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit002", "type":"Shelf",
      "location":{
        "type":"geo:json","value":{"type":"Point","coordinates":[13.3987221, 52.5546640]}
      },
      "name":{
        "type":"Text", "value":"Wall Unit 1"
      },
      "maxCapacity":{
        "type":"Integer", "value":100
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit003", "type":"Shelf",
      "location":{
        "type":"geo:json", "value":{"type":"Point","coordinates":[13.3987221, 52.5546640]}
      },
      "name":{
        "type":"Text", "value":"Wall Unit 2"
      },
      "maxCapacity":{
        "type":"Integer", "value":100
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit004", "type":"Shelf",
      "location":{
        "type":"geo:json", "value":{"type":"Point","coordinates":[13.390311, 52.507522]}
      },
      "name":{
        "type":"Text", "value":"Corner Unit"
      },
      "maxCapacity":{
        "type":"Integer", "value":50
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit005", "type":"Shelf",
      "location":{
        "type":"geo:json","value":{"type":"Point","coordinates":[13.390309, 52.50751]}
      },
      "name":{
        "type":"Text", "value":"Long Wall Unit"
      },
      "maxCapacity":{
        "type":"Integer", "value":200
      }
    }
  ]
}'

```

create products

```bash
curl -iX POST \
  'http://localhost:1026/v2/op/update' \
  -H 'Content-Type: application/json' \
  -d '{
  "actionType":"APPEND",
  "entities":[
    {
      "id":"urn:ngsi-ld:Product:001", "type":"Product",
      "name":{
        "type":"Text", "value":"Beer"
      },
      "size":{
        "type":"Text", "value": "S"
      },
      "price":{
        "type":"Integer", "value": 99
      }
    },
    {
      "id":"urn:ngsi-ld:Product:002", "type":"Product",
      "name":{
        "type":"Text", "value":"Red Wine"
      },
      "size":{
        "type":"Text", "value": "M"
      },
      "price":{
        "type":"Integer", "value": 1099
      }
    },
    {
      "id":"urn:ngsi-ld:Product:003", "type":"Product",
      "name":{
        "type":"Text", "value":"White Wine"
      },
      "size":{
        "type":"Text", "value": "M"
      },
      "price":{
        "type":"Integer", "value": 1499
      }
    },
    {
      "id":"urn:ngsi-ld:Product:004", "type":"Product",
      "name":{
        "type":"Text", "value":"Vodka"
      },
      "size":{
        "type":"Text", "value": "XL"
      },
      "price":{
        "type":"Integer", "value": 5000
      }
    }
  ]
}'
```

```bash
curl -X GET 'http://localhost:1026/v2/entities?type=Store&options=keyValues'
curl -X GET 'http://localhost:1026/v2/entities?type=Product&options=keyValues'
curl -X GET 'http://localhost:1026/v2/entities?type=Shelf&options=keyValues'
```

we are going to create one-to-many relationships, (store to shelf)


```bash
curl -iX POST \
  'http://localhost:1026/v2/op/update' \
  -H 'Content-Type: application/json' \
  -d '{
  "actionType":"APPEND",
  "entities":[
    {
      "id":"urn:ngsi-ld:Shelf:unit001", "type":"Shelf",
      "refStore": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Store:001"
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit002", "type":"Shelf",
      "refStore": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Store:001"
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit003", "type":"Shelf",
      "refStore": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Store:001"
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit004", "type":"Shelf",
      "refStore": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Store:002"
      }
    },
    {
      "id":"urn:ngsi-ld:Shelf:unit005", "type":"Shelf",
      "refStore": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Store:002"
      }
    }
  ]
}'
```

```bash
curl -X GET \
  'http://localhost:1026/v2/entities/urn:ngsi-ld:Shelf:unit001/?type=Shelf&options=keyValues'

curl -X GET \
  'http://localhost:1026/v2/entities/urn:ngsi-ld:Shelf:unit001/?type=Shelf&options=values&attrs=refStore'

curl -X GET \
  'http://localhost:1026/v2/entities/?q=refStore==urn:ngsi-ld:Store:001&options=count&attrs=type&type=Shelf'
```


we are going to create a many to many relationships:

*creating a InventoryItem entitie
*asociating foreign key of store (refStore), shelf (refShelf), product (refProduct)

```bash

curl -iX POST \
  'http://localhost:1026/v2/entities' \
  -H 'Content-Type: application/json' \
  -d '{
    "id": "urn:ngsi-ld:InventoryItem:001", "type": "InventoryItem",
    "refStore": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Store:001"
    },
    "refShelf": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Shelf:unit001"
    },
    "refProduct": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Product:001"
    },
    "stockCount":{
        "type":"Integer", "value": 10000
    },
    "shelfCount":{
        "type":"Integer", "value": 50
    }
}'
```

```bash
curl -X GET \
  'http://localhost:1026/v2/entities/?q=refStore==urn:ngsi-ld:Store:001&options=values&attrs=refProduct&type=InventoryItem'

curl -X GET \
  'http://localhost:1026/v2/entities/?q=refProduct==urn:ngsi-ld:Product:001&options=values&attrs=refStore&type=InventoryItem'
```

data integrity, context data relationships should only be maintined between entities that exist

```bash
curl -X GET \
  'http://localhost:1026/v2/entities/?q=refStore==urn:ngsi-ld:Store:001&options=count&attrs=type'
```



## entity crud operations

create a new data entity

```bash
curl -iX POST \
  --url 'http://localhost:1026/v2/entities' \
  --header 'Content-Type: application/json' \
  --data '
  {
    "id":"urn:ngsi-ld:Product:010",
    "type":"Product",
    "name":{"type":"Text", "value":"Lemonade"},
    "size":{"type":"Text", "value": "S"},
    "price":{"type":"Integer", "value": 99}
  }'

# to check
curl -X GET 'http://localhost:1026/v2/entities?type=Product'
curl -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:010'
# if dont specify type product you will have poor performance i think
curl -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:010?type=Product'
```

create a new attribute

```bash
curl -iX POST \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:010/attrs' \
  --header 'Content-Type: application/json' \
  --data '
  {
    "specialOffer":{"value":true}
  }'
# check if it worked
curl -iX  GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:010'
# another product don't have special offer attributte
curl -iX  GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:004'
```

multiple creation of data entities or attributtes

```bash
curl -iX POST \
  --url 'http://localhost:1026/v2/op/update' \
  --header 'Content-Type: application/json' \
  --data '
  {
    "actionType": "append_strict",
    "entities":[
      {
        "id":"urn:ngsi-ld:Product:011",
        "type":"Product",
        "name":{"type":"Text","value":"Brandy"},
        "size":{"type":"Text","value":"M"},
        "price":{"type":"Integer","value":1199}
      },
      {
        "id":"urn:ngsi-ld:Product:012",
        "type":"Product",
        "name":{"type":"Text","value":"Port"},
        "size":{"type":"Text","value":"M"},
        "price":{"type":"Integer","value":1099}
      },
      {
        "id":"urn:ngsi-ld:Product:001",
        "type":"Product",
        "offerPrice":{"type":"Integer", "value":89}
      }
    ]
  }'

# the request will fail if any attributte already exist in then context, you can use "actiontype":"append"

curl -X GET 'http://localhost:1026/v2/entities?type=Product'

curl -iX POST \
  --url 'http://localhost:1026/v2/op/update' \
  --header 'Content-Type: application/json' \
  --data '{
    "actionType":"append",
    "entities":[
      {
        "id":"urn:ngsi-ld:Product:001",
        "type":"Product",
        "name": {"type":"Text", "value":"Brandy"},
        "size": {"type":"Text", "value": "M"},
        "price": {"type":"Integer", "value": 199}
      },
      {
        "id":"urn:ngsi-ld:Product:012", "type":"Product",
        "name":{"type":"Text", "value":"Port"},
        "size":{"type":"Text", "value": "M"},
        "price":{"type":"Integer", "value": 1099}
      }
    ]
  }'

curl -iX GET 'http://localhost:1026/v2/entities?type=Product'
```

read a single attribute from a data entity

```bash
curl -X GET \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001/attrs/name/value'
# "Brandy"

curl -X GET \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001/attrs/size/value'
# "M"
```

read a multiple attribute from a data entity


```bash
curl -X GET \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001?type=Product&options=keyValues&attrs=name,price'

curl -X GET \
  --url 'http://localhost:1026/v2/entities?type=Product'
```

list data entity by ID

```bash
curl -X GET \
  --url 'http://localhost:1026/v2/entities/?type=Product&options=count&attrs=id'
```

update single / multiple attributes

```bash
# single attributte 
curl -iX PUT \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001/attrs/price/value' \
  --header 'Content-Type: text/plain' \
  --data 91

curl -iX GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001'

# multiple attributes into single data entity
curl -iX POST \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001/attrs' \
  --header 'Content-Type: application/json' \
  --data '
  {
    "price": {"type":"Integer", "value": 42},
    "name": {"type":"Text", "value": "Brandy Solera" }
  }'

# update multiples attrs into multiple data-entity

curl -iX POST \
  --header 'Content-Type: application/json' \
  --url 'http://localhost:1026/v2/op/update' \
  --data '
  {
    "actionType":"update",
    "entities": [
      {
        "id": "urn:ngsi-ld:Product:001",
        "type":"Product",
        "price":{"type":"Integer","value":200}
      },
      {
        "id": "urn:ngsi-ld:Product:003",
        "type":"Product",
        "price":{"type":"Integer","value":100},
        "size":{"type":"Text","value":"XL"}
      }
    ]
  }'

curl -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001'
curl -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:003'


# create and overwrite
curl -iX POST \
  --url 'http://localhost:1026/v2/op/update' \
  --header 'Content-Type: application/json' \
  --data '{
  "actionType":"append",
  "entities":[
      {
        "id":"urn:ngsi-ld:Product:001", "type":"Product",
        "price":{"type":"Integer", "value": 1199}
      },
      {
        "id":"urn:ngsi-ld:Product:002", "type":"Product",
        "price":{"type":"Integer", "value": 1199},
        "specialOffer": {"type":"Boolean", "value":  true}
      }
  ]
}'

# replace full, only remains new attributes bitwise remove if it dont be
curl -iX POST \
  --url 'http://localhost:1026/v2/op/update' \
  --header 'Content-Type: application/json' \
  --data '{
  "actionType":"replace",
  "entities":[
      {
        "id":"urn:ngsi-ld:Product:001", "type":"Product",
        "price":{"type":"Integer", "value": 1199}
      }
  ]
}'
curl -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001'
```


## delete operations

```bash
# delete single entity
curl -iX DELETE \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:010'

# delete muliple entities
curl -iX POST \
  --url 'http://localhost:1026/v2/op/update' \
  --header 'Content-Type: application/json' \
  --data '{
  "actionType":"delete",
  "entities":[
      {
        "id":"urn:ngsi-ld:Product:001", "type":"Product"
      },
      {
        "id":"urn:ngsi-ld:Product:002", "type":"Product"
      }
  ]
}'

# delete attrs of single entity
curl -iX DELETE \
  --url 'http://localhost:1026/v2/entities/urn:ngsi-ld:Product:001/attrs/specialOffer'

# delete multiple attr on single entity
curl -iX POST \
  --url 'http://localhost:1026/v2/op/update' \
  --header 'Content-Type: application/json' \
  --data '{
  "actionType":"delete",
  "entities":[
    {
      "id":"urn:ngsi-ld:Product:003", "type":"Product",
      "price":{},
      "name": {}
    }
  ]
}'
# If any attribute does not exist in the context, the result will be an error response.
```


find existing data relationships to delete in cascade

```bash
curl -X GET \
  --url 'http://localhost:1026/v2/entities/?q=refProduct==urn:ngsi-ld:Product:001&options=count&attrs=type'

# if result has element you must delete before, to delete safely
```




## context data and context providers

"Knowledge is of two kinds. We know a subject ourselves, or we know where we can find information upon it."

— Samuel Johnson (Boswell's Life of Johnson)


things like The current temperature at the store location, The current relative humidity at the store, location, Recent social media tweets regarding the store. This information is always changing, and if it were statically held in a database, the data would always be out-of-date

The FIWARE platform makes the gathering and presentation of real-time context data transparent, since whenever an NGSI request is made to the Orion Context Broker it will always return the latest context by combining the data held within its database along with real-time data readings from any registered external context providers.


MAYBE A Bike-in can be a context provider to decide if port is free or busy, how time remain...


```bash
# to check content provider status
curl -X GET 'http://localhost:3000/health/content-provider-service'

# example
curl -X GET 'http://localhost:3000/health/content-provider-twitter'
curl -X GET 'http://localhost:3000/health/content-provider-temperature'


# Retrieving a single attribute value
curl -iX POST \
  'http://localhost:3000/proxy/static/temperature/queryContext' \
  --header 'Content-Type: application/json' \
  --data '{
    "entities": [
        {
            "type": "Store",
            "isPattern": "false",
            "id": "urn:ngsi-ld:Store:001"
        }
    ],
    "attributes": [
        "temperature"
    ]
}'

# Retrieving multiple attribute values
curl -iX POST \
  'http://localhost:3000/proxy/v1/random/weatherConditions/queryContext' \
  --header 'Content-Type: application/json' \
  --data '{
    "entities": [
        {
            "type": "Store",
            "isPattern": "false",
            "id": "urn:ngsi-ld:Store:001"
        }
    ],
    "attributes": [
        "temperature",
        "relativeHumidity"
    ]
}'
```


Registering a new Context Provider

```bash
curl -iX POST \
  --header 'Content-Type: application/json' \
  --url 'http://localhost:1026/v2/registrations' \
  --data '{
  "description": "Random Weather Conditions",
  "dataProvided": {
    "entities": [
      {
        "id": "urn:ngsi-ld:Store:001",
        "type": "Store"
      }
    ],
    "attrs": [
      "relativeHumidity"
    ]
  },
  "provider": {
    "http": {
      "url": "http://context-provider:3000/proxy/v1/random/weatherConditions"
    },
     "legacyForwarding": true
  }
}'

# after registered you can get context information from enpoint
curl -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Store:001/attrs/relativeHumidity/value'

# delete registration
curl -iX DELETE 'http://localhost:1026/v2/registrations/5ad5b9435c28633f0ae90671'
```



to show registration context provider for an entity

```bash
curl -X GET 'http://localhost:1026/v2/registrations/entity-id'

curl -X GET 'http://localhost:1026/v2/registrations'
```



## accessing the context data

![arquitecture of ](https://camo.githubusercontent.com/c7be2eaa7475203633283d600ded5903331ef810/68747470733a2f2f6669776172652e6769746875622e696f2f7475746f7269616c732e416363657373696e672d436f6e746578742f696d672f6172636869746563747572652e706e67)


NGSI v2 npm library, there is not ruby library NGSI v2 but ... you can use


maybe do a ruby a gem with implementation of NGSI v2 using nokogir??
+ngsi-v2
+ngsi-v2-cli


example that show how to an node app, show items that store has to sell accessing to the API and show on frontend website

```bash
curl -X GET 'http://localhost:1026/v2/entities/' \
  --data 'type=Product' \
  --data 'options=keyValues'
curl -X GET 'http://localhost:1026/v2/entities' \
  --data 'q=refStore==urn:ngsi-ld:Store:001' \
  --data 'type=InventoryItem' \
  --data 'options=keyValues'
```

, and what happpens when one of this is selled "updating context"

```bash
curl -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:InventoryItem:001/attrs/shelfCount/value'
curl -iX PATCH \
  --header 'Content-Type: application/json' \
  'http://localhost:1026/v2/entities/urn:ngsi-ld:InventoryItem:006/attrs' \
  --data '
  {
    "shelfCount": { "type": "Integer", "value": "13" }
  }'
```



### context subscription (NGSI Subscripte/Notify)

    "Don't call us, we'll call you"
    — Dorothy Kilgallen (The Voice Of Broadway)

Orion Context Broker offers also an asynchronous notification mechanism - applications can subscribe to changes of context information so that they can be informed when something happens.


![arquitecture](https://fiware.github.io/tutorials.Subscriptions/img/architecture.png)

```bash
curl -iX POST 'http://localhost:1026/v2/subscriptions'
  --header 'Content-Type: application/json'
  --data '
  {
    "description":"Notify me of all product price changes",
    "subject": {
      "entities": [{"idPattern":".*","type":"Product"}],
      "condition": {"attrs": ["price"]}
    },
    "notification": {
      "http:" {"url":"http://tutorial:3000/subscription/price-change"}
    }
  }'
```

and when the condition will be true ngsi will send at http://tutorial:3000/subscription/price-change

```json
{
  "subscriptionId":"5aeb0b...",
  "data": [
      {
        "id":"urn:ngsi-ld:Product:001",
        "type": "Product",
        "name": {"type":"Text","value":"Beer","metadata":{} },
        "price": {"type":"Integer","value":99,"metadata":{} },
        "size": {"type": "Text","value":"S","metadata":{} }
      },
      {
        "id":"urn:ngsi-ld:Product:002",
        "type": "Product",
        "name": {"type":"Text","value":"Red Wine","metadata":{} },
        "price": {"type":"Integer","value":100,"metadata":{} },
        "size": {"type": "Text","value":"L","metadata":{} }
      }
  ]
}
```


reducing the payload for every request using one of two ways, two cannot be used simultaneously

+attrs (return specific attrs)
+exceptAttrs (return all except especified)

```bash
# not tested
curl -iX POST 'http://localhost:1026/v2/subscriptions' \
  --header 'Content-Type: application/json' \
  --data '
  {
    "description":"Notify me of all product price changes",
    "subject": {
      "entities": [{"idPattern":".*","type":"Product"}],
      "condition": {"attrs": ["price"]}
    },
    "notification": {
      "http:" {"url":"http://tutorial:3000/subscription/price-change"},
      "attrs": ["price"]
    }
  }'

curl -iX POST 'http://localhost:1026/v2/subscriptions' \
  --header 'Content-Type: application/json' \
  --data '
  {
    "description":"Notify me of all product price changes",
    "subject": {
      "entities": [{"idPattern":".*","type":"Product"}],
      "condition": {"attrs": ["price"]}
    },
    "notification": {
      "http:" {"url":"http://tutorial:3000/subscription/price-change"},
      "exceptAttrs": ["size"]
    }
  }'
```


reducing scope of subscription example, if prize is change at specific product


```bash
# subscription for notification at Store 001
curl -iX 'http://localhost:1026/v2/subscriptions' \
  --header 'Content-Type: application/json' \
  --data '
  {
    "description": "Notify me of low stock in Store 001",
    "subject": {
      "entities": [{"idPattern"}: ".*", "type": "InventoryItem"],
      "condition": { "attrs": ["shelfCount"], "expression": {"q":"shelfCount<10;refStore==urn:ngsi-ld:Store:001"} }
    },
    "notification": {
      "http:" {"url":"http://tutorieal:3000/subscription/low-stock-store001"},
      "attrsFormat":"keyValues"
    }
  }'

# subscription for notification at Store 002
curl -iX 'http://localhost:1026/v2/subscriptions' \
  --header 'Content-Type: application/json' \
  --data '{
      "description": "Notify me of low stock in Store 002",
      "subject": {
        "entities": [{"idPattern": ".*","type": "InventoryItem"}],
        "condition": {"attrs":["shelfCount"],"expression": {"q": "shelfCount<10;refStore==urn:ngsi-ld:Store:002"} }
      },
      "notification": {
        "http": {"url": "http://tutorial:3000/subscription/low-stock-store002"},
        "attrsFormat" : "keyValues"
      }
  }'
```


CRUD operation over subscriptions

+create see above

+read

```bash
# list all
curl -X GET --url 'http://localhost:1026/v2/subscriptions'
# read specific
curl -X GET --url 'http://localhost:1026/v2/subscriptions/5aead3361587e1918de90aba'
```

+delete a subscription

```bash
curl -X DELETE --url 'http://localhost:1026/v2/subscriptions/5ae079b86e4f353c5163c939'
```

+update

```bash
curl -iX PATCH 'http://localhost:1026/v2/subscriptions/5ae07c7e6e4f353c5163c93e' \
  --header 'content-type: application/json' \
  --data '{
    "status": "active",
    "notification": {
        "http": {
            "url": "http://tutorial:3000/notify/price-change"
        }
    }
}'
```


## iot Agents & bots

each thing, smart device is uniquely identifiable, FIWARE is a system for managing context information. For a smart solution based on the internet of Things, 

actuator
sensor


UltraLight 2.0 is a lightweight text based protocol for constrained devices and communications where bandwidth and device memory resources are limited.


t|15|k|abc

Contains two attributes, one named "t" with value "15" and another named "k" with value "abc" are transmitted. Values in Ultralight 2.0 are not typed (everything is treated as a string).



Push Command using HTTP POST

```
<device name>@<command>|<param|<param>'
urn:ngsi-ld:Robot:001@turn|left|30

urn:ngsi-ld:Robot:001@turn|Turn ok
```

Requests generated from an IoT device and passed back upwards towards the Context Broker (via an IoT agent) are known as northbound traffic

a device can report new measures to an IoT Aggent using http Get to the context broker example

```
<iot-agent>/iot/d?i=motion001&d=c|12
```

```bash
curl -X POST 'http://localhost:3001/iot/lamp001' \
  --data urn:ngsi-ld:Lamp:001@on

curl -X POST 'http://localhost:3001/iot/lamp001' \
  --data urn:ngsi-ld:Lamp:001@off
```

The Orion Context Broker exclusively uses NGSI requests for all of its interactions. Each IoT Agent provides a North Port NGSI interface which is used for context broker interactions and all interactions beneath this port occur using the native protocol of the attached devices

IOT Agent, is a component that lets a group of devices send their data to and be managed from a Context Broker using their own native protocols. IoT Agent offers a facade pattern to handle this complexity.

IoT Agents should also be able to deal with security aspects of the FIWARE platform (authentication and authorization of the channel) and provide other common ser

The Orion Context Broker exclusively uses NGSI requests for all of its interactions. Each IoT Agent provides a North Port NGSI interface which is used for context broker interactions and all interactions beneath this port occur using the native protocol of the attached devices.



examples of iot agents


+IoTAgent-JSON - a bridge between HTTP/MQTT messaging (with a JSON payload) and NGSI
+IoTAgent-LWM2M - a bridge between the Lightweight M2M protocol and NGSI
+IoTAgent-UL - a bridge between HTTP/MQTT messaging (with an UltraLight2.0 payload) and NGSI
+IoTagent-LoRaWAN - a bridge between the LoRaWAN protocol and NGSI


HTTP requests generated by the Orion Context Broker and passed downwards towards an IoT device (via an IoT agent) are known as southbound traffic.

Requests generated from an IoT device and passed back upwards towards the Context Broker (via an IoT agent) are known as northbound traffic


There is no guarantee that every supplied IoT device <device-id> will always be unique and to allows the context broker to identify the original source of the context data. therefore needs to be able to create context data entities with unique IDs

all provisioning requests to the IoT Agent require two mandatory headers:

+fiware-service (is defined so that entities for a given service can be held in a separate mongoDB database. e.g. parks, transport)
+fiware-servipath (can be used to differentiate between arrays of devices. refers to specific park or specific entity)


Invoking group provision is always the first step in connecting devices since it is always necessary to supply an authentication key with each measurement and the IoT Agent will not initially know which URL the context broker is responding on.

```bash
# provisions an anonymous group of devices.
curl -iX POST 'http://localhost:4041/iot/services' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{
 "services": [
   {
     "apikey":      "4jggokgpepnvsb2uv4s40d59ov",
     "cbroker":     "http://orion:1026",
     "entity_type": "Thing",
     "resource":    "/iot/d"
   }
 ]
}'


```

then iot agent will send to endpoint like this http://iot-agent:7896/iot/d
```bash
curl -iX POST 'http://localhost:7896/iot/d?k=4jggokgpepnvsb2uv4s40d59ov&i=motion001' \
  --header 'Content-Type: text/plain' \
  --data 'c|1'
```

check if info was saved with send a query to context broker

```bash
curl -G -X GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Motion:001' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data 'type=Motion'
```

```json
{
    "id": "urn:ngsi-ld:Motion:001", "type": "Motion",
    "TimeInstant": {"type": "ISO8601","value": "2018-05-25T10:51:32.00Z","metadata": {}},
    "count": {
        "type": "Integer","value": "1",
        "metadata": {
            "TimeInstant": {"type": "ISO8601","value": "2018-05-25T10:51:32.646Z"}
        }
    },
    "refStore": {
        "type": "Relationship",
        "value": "urn:ngsi-ld:Store:001",
        "metadata": {
            "TimeInstant": {"type": "ISO8601", "value": "2018-05-25T10:51:32.646Z"
        }
    }
}
```



provisioning an actuator

```bash
curl -iX POST 'http://localhost:4041/iot/devices' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{
  "devices": [
    {
      "device_id": "bell001",
      "entity_name": "urn:ngsi-ld:Bell:001",
      "entity_type": "Bell",
      "protocol": "PDI-IoTA-UltraLight",
      "transport": "HTTP",
      "endpoint": "http://iot-sensors:3001/iot/bell001",
      "commands": [{ "name": "ring", "type": "command" }],
       "static_attributes": [{"name":"refStore", "type": "Relationship","value": "urn:ngsi-ld:Store:001"}
      ]
    }
  ]
}
'
```

we can test that a command can be sent to a device to the IoT Agent's North Port using the /v1/updateContext endpoint.

It is this endpoint that will eventually be invoked by the context broker once we have connected it up

```bash
curl -iX POST 'http://localhost:4041/v1/updateContext' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{
    "contextElements": [
        {
            "type": "Bell",
            "isPattern": "false",
            "id": "urn:ngsi-ld:Bell:001",
            "attributes": [{ "name": "ring", "type": "command", "value": "" }],
            "static_attributes": [{"name":"refStore", "type": "Relationship","value": "urn:ngsi-ld:Store:001"}]
        }
    ],
    "updateAction": "UPDATE"
}'
```

next query to the OrionContext

```bash
curl -G -iX GET 'http://localhost:1026/v2/entities/urn:ngsi-ld:Bell:001' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data 'type=Bell' \
  --data 'options=keyValues' \
```

```json
{
    "id": "urn:ngsi-ld:Bell:001",
    "type": "Bell",
    "TimeInstant": "2018-05-25T20:06:28.00Z",
    "refStore": "urn:ngsi-ld:Store:001",
    "ring_info": " ring OK",
    "ring_status": "OK",
    "ring": ""
}
```


The full list of provisioned devices can be obtained by making a GET request to the /iot/devices endpoint.

```bash
curl -X GET 'http://localhost:4041/iot/devices' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /'
```

to enabling Context Broker Commands,  we need to register the IoT Agent as a Context Provider for the command attributes. Once the commands have been registered it will be possible to ring the Bell, open and close the Smart Door and switch the Smart Lamp on and off by sending requests to the Orion Context Broker, rather than sending UltraLight 2.0 requests directly the IoT devices. ad /v1 endpoint

```bash
curl -iX POST 'http://localhost:1026/v2/registrations' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{
      "description": "Bell Commands",
      "dataProvided": {
        "entities": [{"id": "urn:ngsi-ld:Bell:001", "type": "Bell"}],
        "attrs": ["ring"]
      },
      "provider": {
        "http": {"url": "http://orion:1026/v1"},
        "legacyForwarding": true
      }
    }'

# and now we can invoke to command to do the bell ring
curl -iX PATCH 'http://localhost:1026/v2/entities/urn:ngsi-ld:Bell:001/attrs' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{ "ring": { "type" : "command", "value" : "" } }'

```

registering a smart door

```bash
curl -iX POST 'http://localhost:1026/v2/registrations' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{
      "description": "Door Commands",
      "dataProvided": {
        "entities": [ {"id": "urn:ngsi-ld:Door:001", "type": "Door"}],
        "attrs": [ "lock", "unlock", "open", "close"]
      },
      "provider": { "http": {"url": "http://orion:1026/v1"}, "legacyForwarding": true }
    }'

# open the door
curl -iX PATCH 'http://localhost:1026/v2/entities/urn:ngsi-ld:Lamp:001/attrs' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{ "open": {"type" : "command","value" : "" } }'
```


CRUD service group actions

```bash
curl -iX POST 'http://localhost:4041/iot/services' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  -data '{
 "services": [
   {
     "apikey":      "4jggokgpepnvsb2uv4s40d59ov",
     "cbroker":     "http://orion:1026",
     "entity_type": "Thing",
     "resource":    "/iot/d"
   }
 ]
}'
```


TODO: read again incomplete


## Iot over MQTT

MQTT is a publish-subscribe-based messaging protocol used in the internet of Things. It works on top of the TCP/IP protocol, and is designed for connections with remote locations where a "small code footprint" is required or the network bandwidth is limited. The goal is to provide a protocol, which is bandwidth-efficient and uses little battery power.


Until now ever we used HTTP every request/response paradigm that connects directly to the IoT Agent. MQTT is different in that publish-subscribe is event-driven and pushes messages to clientes. It requere an additional centarl communication point (knowk MQTT broker) whitch it is in charge of dispatching al messages between the senders and the rightful receivers.

Each client that publishes a message to the broker, includes a topic into the message.
Each client that wants to receive messages subscribes to a certain topi and teh broker delivers all messages with the matching topic.

This way the cliente don't have to know each oter they only communicate over the topic. This architecture enables higly scalable solutions without dependencies between teh data producres and data consumers


![https://fiware.github.io/tutorials.IoT-over-MQTT/img/architecture.png](https://fiware.github.io/tutorials.IoT-over-MQTT/img/architecture.png)


mosquitto is listing at

+Port 1883 is exposed so we can post MQTT topics
+Port 9001 is the standard port for HTTP/Websocket communications



## What is Fast-RTPS, What is Micro-RTPS??

eProsima Fast-RTPS is a c++ implemnttaion of the RTPS (real time publish subscribe) protocol over unreliable transports such as UDP.

eProsima Micro-RTPS protocols for RTPS (Real Time Publish Subscribe) as used in robotics and extremely constrained devices, which is a software solution that provides publisher-subscriber communication between eXtremely Resource Constrained Environments



## CORE CONTEXT MANAGEMENT

FIWARE Cygnus is new component that introduce a new data persistence component. From now the context is only interested in the current state of the system It is not the responsibility of any of the existing components to report on the historical state of the system, the context is based on the last measurement each sensor has sent to the context broker. In order to do this, we will need to extend the existing architecture to persist changes of state into a database whenever the context is updated.


![https://fiware.github.io/tutorials.Historic-Context-Flume/img/cygnus-mongo.png](https://fiware.github.io/tutorials.Historic-Context-Flume/img/cygnus-mongo.png)


```bash
# check cygnus working
curl -X GET 'http://localhost:5080/v1/version'
```

you can persist any entity, add new entity, register, and build a subcription to any changes cygnus was informed

```bash
curl -iX POST 'http://localhost:1026/v2/subscriptions' \
  --header 'Content-Type: application/json' \
  --header 'fiware-service: openiot' \
  --header 'fiware-servicepath: /' \
  --data '{
  "description": "Notify Cygnus of all context changes",
  "subject": {
    "entities": [
      {
        "idPattern": ".*"
      }
    ]
  },
  "notification": {
    "http": {
      "url": "http://cygnus:5050/notify"
    },
    "attrsFormat": "legacy"
  },
  "throttling": 5
}'
```

after you can read changes reading from a database that you use even multiples databases ...

analyzing time series data...

TODO not fully read...



## Identity management FIWARE Keyrock

FIWARE Keyrock is a generic enabler which introduces Identity Management into FIWARE services. The tutorial explains how to create users and organizations in preparation to assign roles and permissions to them

The following common objects are found with the Keyrock Identity Management database:

+User - Any signed up user able to identify themselves with an eMail and password. Users can be assigned rights individually or as a group
+Application - Any securable FIWARE application consisting of a series of microservices
+Organization - A group of users who can be assigned a series of rights. Altering the rights of the organization effects the access of all users of that organization
+OrganizationRole - Users can either be members or admins of an organization - Admins are able to add and remove users from their organization, members merely gain the roles and permissions of an organization. This allows each organization to be responsible for their members and removes the need for a super-admin to administer all rights
+Role - A role is a descriptive bucket for a set of permissions. A role can be assigned to either a single user or an organization. A signed-in user gains all the permissions from all of their own roles plus all of the roles associated to their organization
+Permission - An ability to do something on a resource within the system

Additionally two further non-human application objects can be secured within a FIWARE application:

+IoTAgent - a proxy between IoT Sensors and the Context Broker
+PEPProxy - a middleware for use between generic enablers challenging the rights of a user.

The relationship between the objects can be seen below - the entities marked in red are used directly within this tutorial:
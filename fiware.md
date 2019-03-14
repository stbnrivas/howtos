# Fiware

is an opensource initiative definin a universal set of standards for context data management wich facilitate the development of Smart Solutions for different domains such as Smart Cities, Smart Industry, Smart Agrifood and Smart Energy

In any smart solution there is a need to gather and manage context information, processing that information and informing external actors, enabling them to actuate and therefore alter or enrich the current context. The FIWARE Context Broker component is the core component of any “Powered by FIWARE” platform. It enables the system to perform updates and access to the current state of context.

The Context Broker in turn is surrounded by a suite of additional platform components, which may be supplying context data (from diverse sources such as a CRM system, social networks, mobile apps or IoT sensors for example), supporting processing, analysis and visualization of data or bringing support to data access control, publication or monetization.

All interactions between applications or platform components and the Context Broker take place using the FIWARE NGSI RESTful API – a simple, yet powerful open standard.


Usage of the Orion Context Broker is sufficient for an application to qualify as “Powered by FIWARE”.

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
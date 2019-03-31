# interesting links

+ [fiware zone ](https://fiware.zone) A Junta de Andalucia's and Telefonica initiative to support Fiware Support, they have two locations at Málaga and Sevilla...

# interesting repos

https://github.com/FIWAREZone/


https://github.com/FIWAREZone/Curso_FIWARE/tree/master/postman
https://github.com/FIWAREZone/Basic_course
https://github.com/FIWAREZone/Advanced_course
https://github.com/FIWAREZone/references

# Questions


## General

+geojson

in tutorial use 

"location":{
        "type":"geo:json", "value":{ "type":"Point","coordinates":[13.3986112, 52.554699]}
      },

but geojson is 

{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Point",
        "coordinates": [
          -3.515625,
          39.90973623453719
        ]
      }
    }
  ]
}


+Do you have any way to populate fiware installation?

+There is some way of populate an installation of Fiware?

+There is some website where to find work offers about Fiware?

+Do you build custom solutions on Fiware? Or do you know something that can do?

+There is some app of example that work on Fiware for educational purposes?

+There is some forum or way to know another companies who are working with Fiware, to share experiences?


is Sinchronicity an fiware with more things

## Tecnical

ssl para el context broker

pagination in the APi


fiware no esta o no pensado para que el cliente sea directamente el movil? osea yo tengo mi propia instalacion de fiware y deseo que un movil esté suscrito sobre un entity, como sabe fiware la notificacion, deberia haber una middleware para por ejemplo las notificaciones push

APNS use JSON Web Token (JWT) specification, letting you pass statements and metadata, called claims, to APNs, along with each push notification. For details, refer to the specification at ,Middle machine



O puede el content broker enviar directamente al APNS (apple push notification server) o GCM (Google Cloud Messaging)


¿Hay alguna manera de hacer una peticion de un campo simple especificando cuales quieres?

+Ejemplo el campo address de todos los entities de type Store


Librerias utiles de cara al desarrollo:

+swagger, swagger-codegen to generate API client librarires in differents languages, has Ruby

```bash
swagger-codegen config-help -l <language>
swagger-codegen generate \
 -l javascript \
 -i https://fiware.github.io/specifications/OpenAPI/ngsiv2/ngsiv2-openapi.json
```

npm i ngsi_v2


v1 vs v2 API



question about documentation: 

https://fiware-tutorials.readthedocs.io/en/latest/iot-agent/index.html

registering bell
registering lamp




fiware ready vs powered by Fiware
+ fiware ready (it is a iot device who is ready to work with context broker)
+ powered by fiware is when your platform use context broker

fiware marketplace


metadata for nested attibuttes ...


can reseller for another company your own datas



freeboard as dashboardo backend and more search into fiware marketplace























change postman variables

user            usr_greencities_19
pass            greencities$19
subservice      /greencities
service         fiware_zone
apikey          0ecbdff5261544548420228c5091acc3


zv7af1acs7ceub9xcg51ms8ne




mgmt-int.iotplatform.telefonica.com


get apikey from 

  https://mgmt-int.iotplatform.telefonica.com/


fiwarezoneiot


mqttbox





























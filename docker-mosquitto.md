# MQTT general

- QoS in MQTT

mqtt QoS level 0: At most once, "Fire & Forget"
mqtt QoS level 1: At least once
mqtt QoS level 2: Exactly once, 2-phase commit

- Persistent Session in MQTT

ideal for intermittent connectivity, automatic keep alive messages, QoS 1 & 2 messages are queued for clients which may be offline but not timed out

- Disconnect & Last Will & Testament messages

when the publisher disconnect

- support retained messages which are automatically delivered when a client subscribes to a topic


```
sudo apt search mosquitto-clients
```

```
# `+` single level wildcard
# `#` multi  level wildcard


mosquitto_pub
mosquitto_pub --help
mosquitto_pub  -h $HOST -p $PORT  -t $TOPIC

mosquitto_sub
mosquitto_sub --help
mosquitto_sub  -h $HOST -p $PORT  -t $TOPIC
```


```
topics
```


# MQTT broker


```
docker pull eclipse-mosquitto:1.6
```


```
 docker run -it -p 1883:1883 -p 9001:9001 -v mosquitto.conf:/mosquitto/config/mosquitto.conf eclipse-mosquitto
```


Three directories have been created in the image to be used for configuration, persistent storage and logs.

/mosquitto/config
/mosquitto/data
/mosquitto/log


```
docker run -it -p 1883:1883 -p 9001:9001 -v mosquitto.conf:/mosquitto/config/mosquitto.conf -v /mosquitto/data -v /mosquitto/log eclipse-mosquitto
```
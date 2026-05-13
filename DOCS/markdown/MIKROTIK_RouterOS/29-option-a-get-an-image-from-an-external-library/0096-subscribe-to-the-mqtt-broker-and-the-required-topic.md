## Subscribe to the MQTT broker and the required topic: 

```
/iot/mqtt/subscribe broker=mosquitto topic=test/topic
```

Publish a static MQTT message: 

1878 

```
/iot/mqtt/publish broker="mosquitto" topic="test/topic" message="{\"test\":\"123\"}"
```

Check subscriptions for received messages: 

```
/iot/mqtt/subscriptions/recv/print
```

```
 0 broker=mosquitto topic="test/topic" data="{"test":"123"}"
   time=2023-07-12 10:01:40
```

You can also check the container logs (if enabled), to confirm the mosquitto is operational: 

```
 12:47:28 container,info,debug 1675421248: New connection from 172.19.0.1:42240 on port 1883.
 12:47:28 container,info,debug 1675421248: New client connected from 172.19.0.1:42240 as MTD8580EC793C4 (p2,
c1, k60, u'test').
```

```
 12:47:38 container,info,debug 1675421258: Client MTD8580EC793C4 disconnected.
```

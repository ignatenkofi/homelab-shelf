## Publish a static MQTT message: 

```
/iot/mqtt/publish broker="mosquittoSSL" topic="test/topic" message="{\"test\":\"123\"}"
```

Check subscriptions for received messages: 

```
/iot/mqtt/subscriptions/recv/print
```

```
 0 broker=mosquittoSSL topic="test/topic" data="{"test":"123"}"
   time=2023-07-12 10:20:40
```

1881

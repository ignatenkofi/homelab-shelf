## Subscribe 

**==> picture [13 x 13] intentionally omitted <==**

Please remember that if you have an on-going connection with the broker (the connection is in the " connected=yes " status) and you subscribe to the topic via that broker, you have to re-establish the connection! 

This menu is used to subscribe to MQTT topics from the broker. 

**==> picture [516 x 173] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>broker  (string Select the broker, where to subscribe to.<br>; Default: )<br>force  (yes |  If set to "yes", when the connection with the broker is not yet established (" connected=no "), and subscription is attempted, RouterOS will<br>no; Default:  try to establish an MQTT connection with the specified broker first and then subscribe to the topic. If set to "no", RouterOS will not be<br>yes ) able to subscribe to the topic, unless the connection is already established beforehand (" connected=yes ").<br>qos  (integer: Quality of service parameter, as defined by the broker.<br>0..<br>4294967295<br>; Default: ) 0<br>topic  (string;  Topic, as defined by the broker, where to subscribe to.<br>Default: )<br>**----- End of picture text -----**<br>

An example of a subscription: 

```
/iot mqtt subscribe broker="broker" topic="my/test/topic"
```

Wildcard (single level " + " and multi-level " # ") subscriptions are also supported (RouterOS does not allow publishing to wildcard topics but allows subscribing to them): 

- `/iot mqtt subscribe broker="broker" topic="my/test/#" /iot mqtt subscribe broker="broker" topic="my/test/+"` 

This means that if you subscribe to `topic="my/test/#"` , you will be able to receive messages published to any topic that begins with the pattern before the wildcard symbol "#" (e.g., `"my/test/topic"` , `"my/test/topic/something"` ). 

And, if you subscribe to `topic="my/test/+"` , you will be able to receive messages published on the topic +1 level (e.g., `"my/test/topic"` , `"my/test /something"` ). 

1641

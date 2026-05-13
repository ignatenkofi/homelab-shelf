## Publish 

Publish menu is used to send MQTT messages to the MQTT broker. 

**==> picture [516 x 183] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>broker  (string Select the broker, where to publish the message.<br>; Default: )<br>disconnect- Parameter, that ensures that the connection with the broker will be automatically disconnected after the publish message is sent.<br>after  (yes |<br>no; Default:<br>no )<br>force  (yes |  If set to "yes", when the connection with the broker is not yet established (" connected=no "), and the message is attempted to be<br>no; Default:  published, RouterOS will try to establish an MQTT connection with the specified broker first and then publish the message. If set to "no",<br>yes ) RouterOS will not be able to send the message, unless the connection is already established beforehand (" connected=yes ").<br>message  (st The message that you wish to publish to the broker.<br>ring;<br>Default: )<br>**----- End of picture text -----**<br>


1640 

qos (integer: Quality of service parameter, as defined by the broker. 0.. 4294967295 qos=0 → the message will be received at most once (the message gets sent...fire and forget); ; Default: ) 0 qos=1 → the message will be received at least once (the message gets sent until the publisher receives a confirmation packet `PUBACK` from the broker); qos=2 → the message will be received exactly once (the message gets sent and a 4 way packet exchange happens to ensure it is delivered once); retain (yes | Whether to retain the message or to discard it if no one is subscribed to the topic. This parameter is defined by the broker. no; Default: no ) Retained messages are saved on the broker and are automatically send to the new subscribers (by the broker). topic (string; Topic, as defined by the broker. Default: ) 

An example of publishing the message: 

```
/iot mqtt publish message="test-message" broker="broker" topic="my/test/topic"
```

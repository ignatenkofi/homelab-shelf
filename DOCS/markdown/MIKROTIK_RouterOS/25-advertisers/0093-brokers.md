## Brokers 

To add a new MQTT broker (or an MQTT server), run the following command: 

1638 

```
/iot mqtt brokers add
```

Configurable properties are shown below: 

**==> picture [516 x 507] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP|hostn IP address or hostname of the broker.<br>ame; Default: )<br>auto-connect  (yes  When enabled, after the connection with the MQTT broker goes down/gets interrupted, RouterOS will try to re-establish the<br>| no; Default:  no ) connection over and over again.<br>certificate  (string;  The certificate that is going to be used for the SSL connection.<br>Default: )<br>client-id  (string;  A unique ID used for the connection. The broker uses this ID to identify the client.<br>Default: )<br>keep-alive  (integer A parameter that defines the time (in seconds), after which the client should "ping" the MQTT broker that it is "alive", to ensure the<br>:30..64800;  connection stays ongoing. This value should be set according to MQTT broker settings.<br>Default:  60 )<br>name  (string;  Descriptive name of the broker.<br>Default: )<br>parallel-scripts- A parameter that defines how many scripts the on-message feature for this broker is allowed to run at the exact same time. Can be<br>limit  (integer:3.. useful to reduce CPU, in cases when a large number of messages are constantly published.<br>1000; Default: off)<br>password  (string;  Password for the broker (if required by the broker).<br>Default: )<br>port  (integer:0.. Network port used by the broker.<br>4294967295;<br>Default:  1883 )<br>ssl  (yes | no;  Secure Socket Layer configuration.<br>Default:  no )<br>username  (string;  Username for the broker (if required by the broker).<br>Default: )<br>will-message  (stri Configures a Last Will and Testament (LWT) message, which is going to be sent to the broker during the connection. This<br>ng; Default: ) message will get stored on the broker. The message will not get published (by the broker), unless RouterOS unexpectedly<br>disconnects from the broker (without sending proper "DISCONNECT" packet).<br>will-qos  (integer;  Configure QoS value for the LWT message.<br>Default: )<br>will-retain  (yes |  Configure whether to retain LWT message or not to retain it.<br>no; Default: )<br>will-topic  (string;  Configure an LWT topic, where the  will-message  should be published.<br>Default: )<br>**----- End of picture text -----**<br>

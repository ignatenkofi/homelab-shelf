## Import the certificate: 

```
[admin@LTAP] > /certificate/import file-name=mqttserver.p12 passphrase=thingsboard_mqttcert_password
```

1895 

Add MQTT broker, where the address is the IP address " `dst-address` " that is used in the TCP 8883 port-forwarding rule on the ThingsBoard-container router: 

```
/iot/mqtt/brokers/add name=tbssl address=192.168.88.1 port=8883 username=YOUR_TOKEN ssl=yes
```

Publish a static test MQTT message in the JSON format: 

```
/iot/mqtt/publish broker="tbssl" topic="v1/devices/me/telemetry" message="{\"test\":\"123\"}"
```

And confirm that the broker received it → under the "Latest Telemetry" section on the ThingsBoard. 

1896

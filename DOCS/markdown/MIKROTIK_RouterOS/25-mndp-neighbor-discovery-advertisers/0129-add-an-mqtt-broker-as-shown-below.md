## Add an MQTT broker as shown below: 

```
/iot/mqtt/brokers/add name=tb address=x.x.x.x port=8883 certificate=cert.pem_0 ssl=yes
```

Change the " `address` " to the actual IP/domain address of your ThingsBoard server; Change the " `certificate` " selected to the actual client certificate name that you've imported; Make sure to use " `port=8883` " (the MQTT SSL port that the server is listening to); Make sure to enable " `ssl=yes` ".

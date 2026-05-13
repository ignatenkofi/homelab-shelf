## One-way SSL communication scenario 

**==> picture [13 x 12] intentionally omitted <==**

Recommended scenario to use! 

In this scenario, RouterOS needs to have a server certificate imported into its system. 

Drag-and-drop server certificate, that was installed into the ThingsBoard, into the router's "File List" menu: 

1655 

**==> picture [505 x 299] intentionally omitted <==**

Import server certificate: 

```
/certificate/import file-name=mqttserver.pem passphrase=""
```

When using SSL one-way communication and an access token scenario , add an MQTT broker as shown below: 

```
/iot/mqtt/brokers/add name=tb address=x.x.x.x port=8883 username=access_token ssl=yes
```

- Change the " `address` " to the actual IP/domain address of your ThingsBoard server; Change the " `username` " to the access token that you've used in the ThingsBoard settings; Make sure to use " `port=8883` " (the MQTT SSL port that the server is listening to); Make sure to enable " `ssl=yes` ". 

When using SSL one-way communication and an MQTT Basic scenario , add an MQTT broker as shown below: 

```
/iot/mqtt/brokers/add name=tb address=x.x.x.x port=8883 client-id=clientid password=password username=username
ssl=yes
```

Change the " `address` " to the actual IP/domain address of your ThingsBoard server; Change the " `username` ", " `password` " and " `client-id` " to the actual values that you've used in the ThingsBoard settings; Make sure to use " `port=8883` " (the MQTT SSL port that the server is listening to); Make sure to enable " `ssl=yes` ".

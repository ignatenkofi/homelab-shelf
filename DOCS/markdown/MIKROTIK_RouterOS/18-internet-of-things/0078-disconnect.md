## Disconnect 

To disconnect from the MQTT broker, issue the command: 

```
/iot mqtt disconnect broker="broker"
```

To confirm that the broker was disconnected, issue the command below and it should indicate " connected=no ": 

```
/iot mqtt brokers print
```

```
 0 name="broker" address="192.168.88.33" port=1883 ssl=no client-id="test-client" auto-connect=no keep-alive=60
connected=no
```

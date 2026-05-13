## An example of adding a broker: 

```
/iot mqtt brokers add name="broker" address="192.168.88.33" port=1883 ssl=no client-id="test-client" auto-
connect=no keep-alive=60
```

The result: 

1639 

```
/iot mqtt brokers print
```

```
 0 name="broker" address="192.168.88.33" port=1883 ssl=no client-id="test-client" auto-connect=no keep-alive=60
connected=no
```

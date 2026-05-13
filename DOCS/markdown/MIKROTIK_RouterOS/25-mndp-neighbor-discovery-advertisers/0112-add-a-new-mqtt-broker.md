## Add a new MQTT broker: 

```
/iot mqtt brokers
add address=mqtt.next.kaaiot.com name=kaaiot port=8883 ssl=yes
```

Connect to the broker and check whether the connection is ongoing with the help of the "print" command (" connected=yes " should be present): 

```
/iot mqtt connect broker=kaaiot
```

```
/iot mqtt brokers print
```

```
0 name="kaaiot" address="mqtt.next.kaaiot.com" port=8883 ssl=yes auto-connect=no keep-alive=60 parallel-scripts-
limit=off connected=yes
```

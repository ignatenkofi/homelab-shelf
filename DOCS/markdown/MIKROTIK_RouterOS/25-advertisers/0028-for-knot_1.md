## For KNOT_1: 

```
/iot/mqtt/brokers/add name=tb address=x.x.x.x port=1883 username=knot-1_access_token
```

Where: 

`name` is the name that you wish to give to the broker and this name will be used later in the script; 

`address` is the IP address of the broker/ThingsBoard server; 

`port` is the TCP port that the broker is listening for → for non-SSL it is typically TCP 1883; `username` is dictated by the MQTT broker and, in our case, it is an "access token" that was generated in the ThingsBoard management portal. 

For KNOT_2 and KNOT_3 → Do the same steps. Just change `username` to the respective access token that was generated.

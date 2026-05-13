## MQTT broker configuration 

In case it is a local test or the broker is available through the VPN, you can use non-SSL MQTT: 

```
/iot/mqtt/brokers/add name=tb address=x.x.x.x port=1883 username=access_token
```

Where: 

`name` is the name that you wish to give to the broker and this name will be used later in the script; `address` is the IP address of the broker; 

`port` is the TCP port that the broker is listening for → for non-SSL it is typically TCP 1883; 

`username` is dictated by the MQTT broker and, in our case, it is an "access token" that was generated in the ThingsBoard management portal. 

In case it is public access (when you want to access the broker via its public IP address), we advise you to use SSL MQTT : 

```
/iot/mqtt/brokers/add name=tb address=x.x.x.x port=8883 username=access_token ssl=yes
```

Where: 

`name` is the name that you wish to give to the broker and this name will be used later in the script; 

`address` is the IP address of the broker; 

`port` is the TCP port that the broker is listening for → for SSL it is typically TCP 8883; 

`username` is dictated by the MQTT broker, and, in our case, it is an "access token" that was generated in the ThingsBoard management portal; `ssl` enables SSL MQTT communication.

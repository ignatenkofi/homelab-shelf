## Setup NAT for outgoing traffic: 

```
/ip/firewall/nat/add chain=srcnat action=masquerade src-address=172.18.0.0/24
```

Forward TCP 9090 for HTTP management (the default HTTP port per ThingsBoard documentation): 

**==> picture [13 x 13] intentionally omitted <==**

We suggest using HTTP access only when testing locally or through a VPN (when you are certain that the local network is safe). When you want to access container WEB management from the internet (from the public network/WAN), please, instead, consider using HTTPS . 

```
/ip firewall nat add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=9090 protocol=tcp to-
addresses=172.18.0.2 to-ports=9090
```

1885 

In the `dst-address` field shown in DNAT (dst-nat) rule above, we use the device's local IP address. First, use local IPs (local access) to set everything up and confirm that everything is working . 

**==> picture [13 x 13] intentionally omitted <==**

After going through the rest of the steps shown in this guide and verifying that the ThingsBoard management portal works locally → further secure the setup : 

- (a) make sure that all default ThingsBoard user credentials were changed/removed and strong passwords were implemented (reference ThingsBoard documentation); 

- (b) enable HTTPS (the steps will be explained later on in the guide); 

- (c) preferably change HTTPS port to a non-standard one (reference ThingsBoard documentation). 

Only when you increase the security and only then →  you can consider enabling remote access from WAN (by using your public IP address in the `dst-address` field instead of the local IP used in the example above). Additionally, to further increase security, use `src-address` or `srcaddress-list` parameter, where you can input your trusted public source IP addresses (a list of known/trusted addresses that, for example, belong to your branch office from where you also want to have access to the server). Please understand that only you are responsible for the security. If you leave a door open, someone may exploit it. You need to have networking knowledge and understand the risks when setting up such scenarios. 

Forward TCP 1883 for non-SSL MQTT (the default MQTT port used per ThingsBoard documentation): 

**==> picture [13 x 13] intentionally omitted <==**

We suggest using non-SSL MQTT (TCP 1883) communication only when testing locally or through a VPN (when you are certain that the local network is safe). 

Please consider using SSL MQTT (TCP port 8883) , instead of non-SSL MQTT (TCP port 1883), for real-life applications, when it comes down to access from the internet (from the public network). If you use non-SSL MQTT, the communication between the client (MQTT publisher) and the server (MQTT broker) can be easily sniffed/packet captured, and that will compromise authentication data (such as client-ids, usernames and passwords). 

```
/ip firewall nat add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=1883 protocol=tcp to-
addresses=172.18.0.2 to-ports=1883
```

Same as with HTTP access, in the `dst-address` field shown in DNAT (dst-nat) rule above, we use the device's local IP address. First, use local IPs (local access) to set everything up and confirm that everything is working . 

**==> picture [13 x 13] intentionally omitted <==**

After going through the rest of the steps shown in this guide and verifying that the ThingsBoard non-SSL MQTT communication works locally → f urther secure the setup : 

- (a) consider removing template devices from the ThingsBoard installation; 

- (b) enable SSL MQTT (the steps will be explained later on in the guide); 

- (c) preferably change MQTT port to a non-standard one (reference ThingsBoard documentation). 

When you enable SSL MQTT, you can consider opening TCP 8883 (which is the default SSL MQTT port) from WAN (by using your public IP address in the `dst-address` field instead of the local IP, and changing `dst-port` and `to-ports` from 1883 to 8883). Additionally, to further increase security, use `src-address` or `src-address-list` parameters, where you can set up your trusted public IP address list. As a result, only configured trusted IPs will be able to establish an MQTT connection with the ThingsBoard broker.

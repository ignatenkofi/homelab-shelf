## Networking 

Add veth interface for the container: 

```
/interface/veth/add name=veth2 address=172.19.0.2/24 gateway=172.19.0.1
```

Create a bridge for containers and add veth to it: 

```
/interface/bridge/add name=msqt
```

```
/ip/address/add address=172.19.0.1/24 interface=msqt
```

```
/interface/bridge/port add bridge=msqt interface=veth2
```

Forward TCP 1883 for non-SSL MQTT (where 192.168.88.1 is the device's LAN IP address) for testing purposes if NAT is required (optional): 

```
/ip firewall nat add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=1883 protocol=tcp to-
addresses=172.19.0.2 to-ports=1883
```

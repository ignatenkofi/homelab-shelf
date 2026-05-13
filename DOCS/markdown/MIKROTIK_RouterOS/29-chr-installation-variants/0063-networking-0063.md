## Networking 

Add veth interface: 

1868 

```
/interface/veth/add name=veth2 address=172.19.0.2/24 gateway=172.19.0.1
```

Create a bridge for both containers and add veth interfaces to it: 

```
/interface/bridge/add name=ha
/ip/address/add address=172.19.0.1/24 interface=ha
```

```
/interface/bridge/port add bridge=ha interface=veth2
```

Forward TCP 8123 for home-assistant management (where 192.168.88.1 is the device's LAN IP address) if NAT is required (optional): 

```
/ip firewall nat add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=8123 protocol=tcp to-
addresses=172.19.0.2 to-ports=8123
```

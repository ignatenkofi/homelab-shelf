## The network configuration: 

```
/interface/veth/add name=veth1 address=172.17.0.2/24 gateway=172.17.0.1
/interface/bridge/add name=containers
```

```
/ip/address/add address=172.17.0.1/24 interface=containers
/interface/bridge/port add bridge=containers interface=veth1
/ip firewall nat
```

```
add chain=srcnat action=masquerade src-address=172.17.0.0/24
```

```
add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=80 protocol=tcp to-addresses=172.
17.0.2 to-ports=80
```

## RouterA: 

```
 /ip address add address=10.22.0.1/24 interface=ether1
 /interface vlan add interface=ether2 vlan-id=1 name=vlan1
 /ip address add address=10.22.0.1/32 interface=vlan1 network=10.23.0.1
 /ip route add gateway=10.23.0.1 dst-address=10.23.0.0/24
```

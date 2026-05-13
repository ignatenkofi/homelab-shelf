## Configuration 

```
/interface bridge
add name=bridge1
/interface bridge port
add interface=ether1 bridge=bridge1
add interface=ether2 bridge=bridge1
/interface vlan
add name=VLAN99 interface=ether1 vlan-id=99
/ip pool
add name=VLAN99_POOL range=192.168.99.100-192.168.99.200
/ip address add address=192.168.99.1/24 interface=VLAN99
/ip dhcp-server
add interface=VLAN99 address-pool=VLAN99_POOL disabled=no
/ip dhcp-server network
add address=192.168.99.0/24 gateway=192.168.99.1 dns-server=192.168.99.1
```

## Configuration 

```
/interface vlan
add interface=ether1 name=VLAN99 vlan-id=99
/interface bridge
add name=bridge1
/interface bridge port
add interface=ether2 bridge=bridge1
add interface=VLAN99 bridge=bridge1
```

## Configuration 

```
/interface bridge
add name=bridge1
add name=bridge2
/interface vlan
add interface=bridge1 name=VLAN vlan-id=99
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2
add bridge=bridge2 interface=VLAN
add bridge=bridge2 interface=ether3
```

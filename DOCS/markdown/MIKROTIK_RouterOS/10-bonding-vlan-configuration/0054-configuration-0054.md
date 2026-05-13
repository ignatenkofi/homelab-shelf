## Configuration 

```
/interface vlan
add interface=ether1 name=ether1_v10 vlan-id=10
add interface=ether2 name=ether2_v10 vlan-id=10
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1_v10
add bridge=bridge1 interface=ether2_v10
```

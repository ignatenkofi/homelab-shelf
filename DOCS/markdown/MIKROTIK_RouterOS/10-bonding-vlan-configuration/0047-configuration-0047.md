## Configuration 

Only the router part is relevant to this case, switch configuration doesn't really matter as long as ports are switched. Router configuration can be found below: 

```
/interface bridge
add name=bridge10
add name=bridge20
/interface vlan
add interface=ether1 name=ether1_v10 vlan-id=10
add interface=ether1 name=ether1_v20 vlan-id=20
add interface=ether2 name=ether2_v10 vlan-id=10
add interface=ether2 name=ether2_v20 vlan-id=20
/interface bridge port
add bridge=bridge10 interface=ether1_v10
add bridge=bridge10 interface=ether2_v10
add bridge=bridge20 interface=ether1_v20
add bridge=bridge20 interface=ether2_v20
```

## Configuration 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2
/interface vlan
add interface=bridge1 name=VLAN99 vlan-id=99
```

594

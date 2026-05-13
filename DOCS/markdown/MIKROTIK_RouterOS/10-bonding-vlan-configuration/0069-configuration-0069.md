## Configuration 

593 

```
/interface bridge
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether3 pvid=10
add bridge=bridge1 interface=ether4 pvid=20
/interface bridge vlan
add bridge=bridge1 tagged=ether2 vlan-ids=10,20
```

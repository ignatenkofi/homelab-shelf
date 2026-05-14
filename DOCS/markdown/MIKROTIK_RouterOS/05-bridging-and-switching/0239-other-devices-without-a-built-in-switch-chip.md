## Other devices without a built-in switch chip 

It is possible to do VLAN filtering using the CPU, there are multiple ways to do it, but it is highly recommended to use bridge VLAN filtering. 

513 

```
/interface bridge
add name=bridge1 frame-types=admit-only-vlan-tagged
/interface bridge port
add bridge=bridge1 interface=ether1 frame-types=admit-only-vlan-tagged
add bridge=bridge1 interface=ether2 pvid=20 frame-types=admit-only-untagged-and-priority-tagged
add bridge=bridge1 interface=ether3 pvid=30 frame-types=admit-only-untagged-and-priority-tagged
/interface bridge vlan
add bridge=bridge1 tagged=ether1 vlan-ids=20
add bridge=bridge1 tagged=ether1 vlan-ids=30
add bridge=bridge1 tagged=ether1,bridge1 vlan-ids=99
/interface vlan
add interface=bridge1 vlan-id=99 name=MGMT
/ip address
add address=192.168.99.1/24 interface=MGMT
/interface bridge
set bridge1 vlan-filtering=yes
```

More detailed examples can be found here. 

514

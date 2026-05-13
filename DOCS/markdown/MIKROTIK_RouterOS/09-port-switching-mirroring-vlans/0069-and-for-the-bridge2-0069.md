## And for the Bridge2: 

```
/interface vlan
add interface=bridge1 name=MGMT vlan-id=99
/ip address
add address=192.168.99.2/24 interface=MGMT network=192.168.99.0
/interface bridge vlan
add bridge=bridge1 tagged=bridge1,sfp-sfpplus1 vlan-ids=99
```

Add bridge VLAN entries and specify tagged and untagged ports. The VLAN 99 entry was already created when configuring management access, only VLAN 10 and VLAN 20 should be added now. Below are the configuration commands for the Bridge1:

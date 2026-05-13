## VLAN Configuration Example 

```
/interface/ethernet/switch set 0 l3-hw-offloading=no
```

```
/interface/bridge/port add bridge=bridge interface=ether2
/interface/bridge/vlan add bridge=bridge tagged=bridge,ether2 vlan-ids=20
/interface/vlan add interface=bridge name=vlan20 vlan-id=20
/ip/address add address=192.0.2.1/24 interface=vlan20
/interface/bridge set bridge vlan-filtering=yes
/interface/ethernet/switch set 0 l3-hw-offloading=yes
```

**==> picture [13 x 13] intentionally omitted <==**

For Inter-VLAN routing, the bridge interface must be a tagged member of every routable `/interface/bridge/vlan/` 

entry.

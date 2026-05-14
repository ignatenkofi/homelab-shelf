## Add both VLAN IDs to the bridge VLAN table: 

```
/interface bridge vlan
```

```
add bridge=bridge1 tagged=ether1 vlan-ids=10
add bridge=bridge1 tagged=ether2 vlan-ids=20
```

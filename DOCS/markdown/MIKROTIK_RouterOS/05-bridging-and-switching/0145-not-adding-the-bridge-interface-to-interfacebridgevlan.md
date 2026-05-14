## Not adding the bridge interface to /interface/bridge/vlan/ 

For Inter-VLAN routing, the bridge interface itself needs to be added to the tagged members of the given VLANs. In the next example, Inter-VLAN routing works between VLAN 10 and 11, but packets are NOT routed to VLAN 20. 

```
/interface bridge vlan
```

```
add bridge=bridge1 vlan-ids=10 tagged=bridge1,sfp-sfpplus1
add bridge=bridge1 vlan-ids=11 tagged=bridge1 untagged=sfp-sfpplus2,sfp-sfpplus3
add bridge=bridge1 vlan-ids=20 tagged=sfp-sfpplus1 untagged=sfp-sfpplus4,sfp-sfpplus5
```

The above example does not always mean an error. Sometimes, you may want the device to act as a simple L2 switch in some/all VLANs. Just make sure you set such behavior on purpose, not due to a mistake.

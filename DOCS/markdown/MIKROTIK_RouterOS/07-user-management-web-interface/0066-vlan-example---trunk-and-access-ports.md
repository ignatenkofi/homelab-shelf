## VLAN Example - Trunk and Access Ports 

**==> picture [504 x 323] intentionally omitted <==**

Create a bridge with disabled `vlan-filtering` to avoid losing access to the device before VLANs are completely configured. If you need a management access to the bridge, see the Management access configuration section. 

```
/interface bridge
add name=bridge1 vlan-filtering=no
```

Add bridge ports and specify `pvid` for access ports to assign their untagged traffic to the intended VLAN. Use `frame-types` setting to accept only tagged or untagged packets. 

374 

```
/interface bridge port
```

```
add bridge=bridge1 interface=ether2 frame-types=admit-only-vlan-tagged
```

```
add bridge=bridge1 interface=ether6 pvid=200 frame-types=admit-only-untagged-and-priority-tagged
add bridge=bridge1 interface=ether7 pvid=300 frame-types=admit-only-untagged-and-priority-tagged
add bridge=bridge1 interface=ether8 pvid=400 frame-types=admit-only-untagged-and-priority-tagged
```

Add Bridge VLAN entries and specify tagged ports in them. Bridge ports with `frame-types` set to `admit-only-untagged-and-prioritytagged` will be automatically added as untagged ports for the `pvid` VLAN. 

```
/interface bridge vlan
add bridge=bridge1 tagged=ether2 vlan-ids=200
add bridge=bridge1 tagged=ether2 vlan-ids=300
add bridge=bridge1 tagged=ether2 vlan-ids=400
```

In the end, when VLAN configuration is complete, enable Bridge VLAN Filtering. 

```
/interface bridge set bridge1 vlan-filtering=yes
```

Optional step is to set `frame-types=admit-only-vlan-tagged` on the bridge interface in order to disable the default untagged VLAN 1 ( `pvid=1` ). 

```
/interface bridge set bridge1 frame-types=admit-only-vlan-tagged
```

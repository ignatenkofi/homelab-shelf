## VLAN Example - Trunk and Hybrid Ports 

**==> picture [504 x 322] intentionally omitted <==**

Create a bridge with disabled `vlan-filtering` to avoid losing access to the router before VLANs are completely configured. If you need a management access to the bridge, see the Management access configuration section. 

375 

```
/interface bridge
```

```
add name=bridge1 vlan-filtering=no
```

Add bridge ports and specify `pvid` on hybrid VLAN ports to assign untagged traffic to the intended VLAN.  Use `frame-types` setting to accept only tagged packets on ether2. 

```
/interface bridge port
```

```
add bridge=bridge1 interface=ether2 frame-types=admit-only-vlan-tagged
add bridge=bridge1 interface=ether6 pvid=200
add bridge=bridge1 interface=ether7 pvid=300
add bridge=bridge1 interface=ether8 pvid=400
```

Add Bridge VLAN entries and specify tagged ports in them. In this example egress VLAN tagging is done on ether6,ether7,ether8 ports too, making them into hybrid ports. Bridge ports with `frame-types` set to `admit-all` will be automatically added as untagged ports for the `pvid` VLAN. 

```
/interface bridge vlan
```

```
add bridge=bridge1 tagged=ether2,ether7,ether8 vlan-ids=200
add bridge=bridge1 tagged=ether2,ether6,ether8 vlan-ids=300
add bridge=bridge1 tagged=ether2,ether6,ether7 vlan-ids=400
```

In the end, when VLAN configuration is complete, enable Bridge VLAN Filtering. 

```
/interface bridge set bridge1 vlan-filtering=yes
```

Optional step is to set `frame-types=admit-only-vlan-tagged` on the bridge interface in order to disable the default untagged VLAN 1 ( `pvid=1` ). 

```
/interface bridge set bridge1 frame-types=admit-only-vlan-tagged
```

**==> picture [13 x 13] intentionally omitted <==**

You don't have to add access ports as untagged ports, because they will be added dynamically as an untagged port with the VLAN ID that is specified in `pvid` , you can specify just the trunk port as a tagged port. All ports that have the same `pvid` set will be added as untagged ports in a single entry. You must take into account that the bridge itself is a port and it also has a `pvid` value, this means that the bridge port also will be added as an untagged port for the ports that have the same `pvid` . You can circumvent this behavior by either setting different `pvid` on all ports (even the trunk port and bridge itself), or to use `frame-type` set to `accept-only-vlan-tagged` .

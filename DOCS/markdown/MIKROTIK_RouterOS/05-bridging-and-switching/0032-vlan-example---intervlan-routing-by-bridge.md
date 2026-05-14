## VLAN Example - InterVLAN Routing by Bridge 

376 

**==> picture [504 x 323] intentionally omitted <==**

Create a bridge with disabled `vlan-filtering` to avoid losing access to the router before VLANs are completely configured.  If you need a management access to the bridge, see the Management access configuration section. 

```
/interface bridge
add name=bridge1 vlan-filtering=no
```

Add bridge ports and specify `pvid` for VLAN access ports to assign their untagged traffic to the intended VLAN. Use `frame-types` setting to accept only untagged packets. 

```
/interface bridge port
```

```
add bridge=bridge1 interface=ether6 pvid=200 frame-types=admit-only-untagged-and-priority-tagged
add bridge=bridge1 interface=ether7 pvid=300 frame-types=admit-only-untagged-and-priority-tagged
add bridge=bridge1 interface=ether8 pvid=400 frame-types=admit-only-untagged-and-priority-tagged
```

Add Bridge VLAN entries and specify tagged ports in them. In this example bridge1 interface is the VLAN trunk that will send traffic further to do InterVLAN routing. Bridge ports with `frame-types` set to `admit-only-untagged-and-priority-tagged` will be automatically added as untagged ports for the `pvid` VLAN. 

```
/interface bridge vlan
add bridge=bridge1 tagged=bridge1 vlan-ids=200
add bridge=bridge1 tagged=bridge1 vlan-ids=300
add bridge=bridge1 tagged=bridge1 vlan-ids=400
```

Configure VLAN interfaces on the bridge1 to allow handling of tagged VLAN traffic at routing level and set IP addresses to ensure routing between VLANs as planned. 

377 

```
/interface vlan
```

```
add interface=bridge1 name=VLAN200 vlan-id=200
add interface=bridge1 name=VLAN300 vlan-id=300
add interface=bridge1 name=VLAN400 vlan-id=400
```

```
/ip address
```

```
add address=20.0.0.1/24 interface=VLAN200
add address=30.0.0.1/24 interface=VLAN300
add address=40.0.0.1/24 interface=VLAN400
```

In the end, when VLAN configuration is complete, enable Bridge VLAN Filtering: 

```
/interface bridge set bridge1 vlan-filtering=yes
```

Optional step is to set `frame-types=admit-only-vlan-tagged` on the bridge interface in order to disable the default untagged VLAN 1 ( `pvid=1` ). 

```
/interface bridge set bridge1 frame-types=admit-only-vlan-tagged
```

Since RouterOS v7, it is possible to route traffic using the L3 HW offloading on certain devices. See more details on L3 Hardware Offloading.

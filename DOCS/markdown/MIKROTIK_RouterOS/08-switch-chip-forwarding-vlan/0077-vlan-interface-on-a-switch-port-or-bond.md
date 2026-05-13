## VLAN interface on a switch port or bond 

```
/interface/vlan
add name=vlan10 vlan-id=10 interface=sfp-sfpplus1
add name=vlan20 vlan-id=20 interface=bond1
```

Due to Layer 2 dependency, only VLAN interfaces created on a hardware-offloaded, vlan-filtering bridge is capable of L3HW offloading. The correct configuration is: 

445 

```
/interface/bridge/port
```

```
add bridge=bridge1 interface=sfp-sfpplus1 frame-types=admit-only-vlan-tagged
add bridge=bridge1 interface=bond1 frame-types=admit-only-vlan-tagged
```

```
/interface/bridge/vlan
add bridge=bridge1 tagged=bridge1,sfp-sfpplus1 vlan-ids=10
add bridge=bridge1 tagged=bridge1,bond1 vlan-ids=20
```

```
/interface/vlan
```

```
add name=vlan10 vlan-id=10 interface=bridge1
add name=vlan20 vlan-id=20 interface=bridge1
```

**==> picture [13 x 13] intentionally omitted <==**

If VLAN interfaces are created directly on Ethernet or bonding interfaces, packets may be offloaded incorrectly - bypassing CPU processing (such as firewall and NAT) and cause undefined behavior. 

If this type of configuration is required, L3HW offloading must be disabled on the related switch ports under the `/interface/ethernet /switch/port` menu by setting `l3-hw-offloading=no` .

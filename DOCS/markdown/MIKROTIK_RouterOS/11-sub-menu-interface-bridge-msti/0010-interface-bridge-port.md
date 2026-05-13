## `/interface bridge port` 

```
set [find where interface=ether1 or interface=wlan1] frame-types=admit-only-vlan-tagged ingress-filtering=yes
```

Set up the bridge VLAN table. Since VLAN99 is going to be our management traffic, then we need to allow this VLAN ID to be able to access the bridge interface, otherwise, the traffic will be dropped as soon as you will try to access the device. VLAN10 does not need to access the bridge since it is only meant to be forwarded to the other end. To achieve such functionality add these entries to the bridge VLAN table on AP and ST : 

```
/interface bridge vlan
add bridge=bridge tagged=ether1,wlan1 vlan-ids=10
add bridge=bridge tagged=ether1,wlan1,bridge vlan-ids=99
```

622 

**==> picture [13 x 13] intentionally omitted <==**

You can limit from which interfaces it will be allowed to access the device. For example, if you don't want the device to be accessible from `wlan1` , then you can remove the interface from the corresponding bridge VLAN entry. 

**==> picture [13 x 13] intentionally omitted <==**

For devices with hardware offloaded VLAN filtering and wireless interface support (e.g. RB4011 with RTL8367 switch chip, or LtAP with MT7621 switch chip), more attention needs to be paid. Packets going from HW offloaded ports to wireless can be filtered, if the VLAN access to the CPU is not allowed. It is possible to allow CPU access for a certain VLAN by adding the bridge interface as a VLAN member (similar to the VLAN99 example) or disabling HW offloading on bridge ports. 

All devices ( R1 , R2 , AP, and ST ) need a VLAN interface created to be able to access the device through the specific VLAN ID. For AP and ST create the VLAN interface on top of the bridge interface and assign an IP address to it: 

```
/interface vlan
add interface=bridge name=MGMT vlan-id=99
/ip address
add address=192.168.99.X/24 interface=MGMT
```

For R1 and R2 do the same, but the interface, on which you need to create the VLAN interface, will probably change, depending on your setup: 

```
/interface vlan
add interface=ether1 name=MGMT vlan-id=99
/ip address
add address=192.168.99.X/24 interface=MGMT
```

**==> picture [13 x 13] intentionally omitted <==**

To allow more VLANs to be forwarded, you simply need to specify more VLAN IDs in the bridge VLAN table, you can specify multiple VLANs divided by coma or even VLAN ranges.

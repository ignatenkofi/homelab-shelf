## VLAN Example 2 (Trunk and Hybrid Ports) 

VLAN Hybrid ports can forward both tagged and untagged traffic. This configuration is supported only by some Gigabit switch chips ( QCA8337, Atheros8327 ). 

**==> picture [504 x 323] intentionally omitted <==**

Switch together the required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
add bridge=bridge1 interface=ether4 hw=yes
add bridge=bridge1 interface=ether5 hw=yes
```

495 

**==> picture [13 x 13] intentionally omitted <==**

By default, the bridge interface is configured with `protocol-mode` set to `rstp` . For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features. 

Add VLAN table entries to allow frames with specific VLAN IDs between ports. 

```
/interface ethernet switch vlan
```

```
add ports=ether2,ether3,ether4,ether5 switch=switch1 vlan-id=200
add ports=ether2,ether3,ether4,ether5 switch=switch1 vlan-id=300
add ports=ether2,ether3,ether4,ether5 switch=switch1 vlan-id=400
```

In the switch port menu set `vlan-mode` on all ports and also `default-vlan-id` on planned hybrid ports: 

```
/interface ethernet switch port
set ether2 vlan-mode=secure vlan-header=leave-as-is
```

```
set ether3 vlan-mode=secure vlan-header=leave-as-is default-vlan-id=200
set ether4 vlan-mode=secure vlan-header=leave-as-is default-vlan-id=300
set ether5 vlan-mode=secure vlan-header=leave-as-is default-vlan-id=400
```

`vlan-mode=secure` will ensure strict use of the VLAN table. 

`default-vlan-id` will define VLAN for untagged ingress traffic on the port. 

In QCA8337 and Atheros8327 chips when `vlan-mode=secure` is used, it ignores switch port `vlan-header` options. VLAN table entries handle all the egress tagging/untagging and works as `vlan-header=leave-as-is` on all ports. It means what comes in tagged, goes out tagged as well, only `default-vlan-id` frames are untagged at the egress port.

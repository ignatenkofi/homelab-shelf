## Other devices with a built-in switch chip 

512 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether3
/interface ethernet switch vlan
add ports=ether1,ether2 switch=switch1 vlan-id=20
add ports=ether1,ether3 switch=switch1 vlan-id=30
add ports=ether1,switch1-cpu switch=switch1 vlan-id=99
/interface vlan
add interface=bridge1 vlan-id=99 name=MGMT
/ip address
add address=192.168.99.1/24 interface=MGMT
/interface ethernet switch port
set ether1 vlan-mode=secure vlan-header=add-if-missing
set ether2 vlan-mode=secure vlan-header=always-strip default-vlan-id=20
set ether3 vlan-mode=secure vlan-header=always-strip default-vlan-id=30
set switch1-cpu vlan-header=leave-as-is vlan-mode=secure
```

More detailed examples can be found here. 

**==> picture [13 x 13] intentionally omitted <==**

Not all devices with a switch chip are capable of VLAN switching on a hardware level, check the supported features for each switch chip, the compatibility table can be found here. If a device has `VLAN table` support, then it is capable of VLAN switching using the built-in switch chip. You can check the device's switch chip either in the provided link or by using `/interface ethernet switch print` 

**==> picture [13 x 13] intentionally omitted <==**

On QCA8337 and Atheros8327 switch chips, a default `vlan-header=leave-as-is` property should be used. The switch chip will determine which ports are access ports by using the `default-vlan-id` property. The `default-vlan-id` should only be used on access/hybrid ports to specify which VLAN the untagged ingress traffic is assigned to. 

**==> picture [13 x 13] intentionally omitted <==**

This type of configuration should be used on RouterBOARD series devices, this includes RB4xx, RB9xx, RB2011, RB3011, hAP, hEX, cAP, and other devices. 

**==> picture [13 x 13] intentionally omitted <==**

By default, the bridge interface is configured with protocol-mode set to `rstp` . For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features. 

**==> picture [13 x 13] intentionally omitted <==**

For devices that have multiple switch chips (for example, RB2011, RB3011, RB1100), each switch chip is only able to switch VLAN traffic between ports that are on the same switch chip, VLAN filtering will not work on a hardware level between ports that are on different switch chips, this means you should not add all ports to a single bridge if you are intending to use VLAN filtering using the switch chip, VLANs between switch chips will not get filtered. You can connect a single cable between both switch chips to work around this hardware limitation, another option is to use Bridge VLAN Filtering, but it disables hardware offloading (and lowers the total throughput).

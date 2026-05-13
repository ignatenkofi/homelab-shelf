## Tagged 

To make the device accessible only from a certain VLAN, you need to create a new VLAN interface on the bridge interface and assign an IP address to it: 

```
/interface vlan
add name=MGMT vlan-id=99 interface=bridge1
/ip address
add address=192.168.99.1/24 interface=MGMT
```

496 

Specify from which interfaces it is allowed to access the device: 

```
/interface ethernet switch vlan
```

```
add ports=ether1,switch1-cpu switch=switch1 vlan-id=99
```

**==> picture [13 x 13] intentionally omitted <==**

Only specify trunk ports in this VLAN table entry, it is not possible to allow access to the CPU with tagged traffic through an access port since the access port will tag all ingress traffic with the specified `default-vlan-id` value. 

When the VLAN table is configured, you can enable `vlan-mode=secure` to limit access to the CPU: 

```
/interface ethernet switch port
```

```
set ether1 vlan-header=add-if-missing vlan-mode=secure
set ether2 default-vlan-id=100 vlan-header=always-strip vlan-mode=secure
set switch1-cpu vlan-header=leave-as-is vlan-mode=secure
```

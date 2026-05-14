## Management access configuration 

In these examples, there will be shown examples for multiple scenarios, but each of these scenarios requires you to have switched ports. Below you can find how to switch multiple ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add interface=ether1 bridge=bridge1 hw=yes
add interface=ether2 bridge=bridge1 hw=yes
```

**==> picture [13 x 13] intentionally omitted <==**

By default, the bridge interface is configured with `protocol-mode` set to `rstp` . For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features. 

In these examples, it will be assumed that ether1 is the trunk port and ether2 is the access port, for configuration as the following: 

```
/interface ethernet switch port
set ether1 vlan-header=add-if-missing
set ether2 default-vlan-id=100 vlan-header=always-strip
/interface ethernet switch vlan
add ports=ether1,ether2,switch1-cpu switch=switch1 vlan-id=100
```

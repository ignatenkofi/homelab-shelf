## MAC Based VLAN 

**==> picture [13 x 13] intentionally omitted <==**

The Switch Rule table is used for MAC Based VLAN functionality, see this table on how many rules each device supports. MAC-based VLANs will only work properly between switch ports and not between switch ports and CPU. When a packet is being forwarded to the CPU, the `pvid` property for the bridge port will be always used instead of `new-vlan-id` from ACL rules. MAC-based VLANs will not work for DHCP packets when DHCP snooping is enabled. 

Enable switching on ports by creating a bridge with enabled hw-offloading: 

```
/interface bridge
```

```
add name=bridge1 vlan-filtering=yes
/interface bridge port
```

```
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
```

Add VLANs in the Bridge VLAN table and specify ports:

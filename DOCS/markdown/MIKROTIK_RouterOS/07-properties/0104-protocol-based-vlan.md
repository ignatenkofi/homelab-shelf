## Protocol Based VLAN 

**==> picture [13 x 13] intentionally omitted <==**

The Switch Rule table is used for Protocol Based VLAN functionality, see this table on how many rules each device supports. Protocol-based VLANs will only work properly between switch ports and not between switch ports and CPU. When a packet is being forwarded to the CPU, the `pvid` property for the bridge port will be always used instead of `new-vlan-id` from ACL rules. Protocol-based VLANs will not work for DHCP packets when DHCP snooping is enabled. 

Enable switching on ports by creating a bridge with enabled hw-offloading:

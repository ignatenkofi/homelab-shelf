## IGMP snooping configuration with VLANs 

The second example adds some complexity. There are two IGMP snooping bridges and we need to isolate the multicast traffic on a different VLAN. See a network scheme below. 

521 

**==> picture [504 x 280] intentionally omitted <==**

First, create a bridge on both devices and add the needed interfaces as bridge ports. To change untagged VLAN for a bridge port, use the `pvid` setting. The Bridge1 will be acting as an IGMP querier. Below are the configuration commands for the Bridge1: 

```
/interface bridge
add igmp-snooping=yes multicast-querier=yes name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 pvid=10
add bridge=bridge1 interface=ether3 pvid=10
add bridge=bridge1 interface=ether4 pvid=10
add bridge=bridge1 interface=ether5 pvid=20
add bridge=bridge1 interface=sfp-sfpplus1 pvid=10
```

## And for the Bridge2: 

```
/interface bridge
add igmp-snooping=yes name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether3 pvid=10
add bridge=bridge1 interface=ether4 pvid=10
add bridge=bridge1 interface=ether5 pvid=20
add bridge=bridge1 interface=sfp-sfpplus1 pvid=10
```

**==> picture [13 x 13] intentionally omitted <==**

Bridge IGMP querier implementation can only send untagged IGMP queries. In case tagged IGMP queries should be sent or IGMP queries should be generated in multiple VLANs, it is possible to install a multicast package, add a VLAN interface and configure a PIM interface on VLAN. The PIM interface can be used as an IGMP querier. 

Make sure to configure management access for devices. It is essential when configuring a bridge with VLAN filtering. In this example, a VLAN 99 interface with an IP address is added to the bridge. This VLAN will be allowed on the tagged sfp-sfpplus1 port. Below are configuration commands for the Bridge1: 

522 

```
/interface vlan
```

```
add interface=bridge1 name=MGMT vlan-id=99
/ip address
add address=192.168.99.1/24 interface=MGMT network=192.168.99.0
/interface bridge vlan
add bridge=bridge1 tagged=bridge1,sfp-sfpplus1 vlan-ids=99
```

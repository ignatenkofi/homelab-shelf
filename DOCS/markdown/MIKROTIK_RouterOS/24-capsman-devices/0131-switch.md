## Switch: 

In this example, we are going to be using Bridge VLAN Filtering to filter unknown VLANs and to assign other devices to the same networks. Some devices are capable of offloading this to the built-in switch chip, check Basic VLAN switching guide to see how to configure it on different types of devices. 

Setup Bridge VLAN Filtering 

1545 

```
/interface bridge
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether3
add bridge=bridge1 interface=ether4 pvid=10
add bridge=bridge1 interface=ether5 pvid=20
/interface bridge vlan
add bridge=bridge1 tagged=ether1,ether2,ether3 untagged=ether4 vlan-ids=10
add bridge=bridge1 tagged=ether1,ether2,ether3 untagged=ether5 vlan-ids=20
```

**==> picture [13 x 12] intentionally omitted <==**

In this example, untagged traffic is going to be used to communicate between CAPs and CAPsMAN Router. By default, if PVID is not changed, untagged traffic is going to be forwarded between ports that have the same PVID value set (including the default PVID).

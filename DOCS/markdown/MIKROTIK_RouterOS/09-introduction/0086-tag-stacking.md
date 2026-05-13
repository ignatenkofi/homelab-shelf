## Tag Stacking 

In the VLAN Tunnelling setup, we were adding a new VLAN tag that was different from the VLAN tag, but it is possible to add a new VLAN tag regardless of the packet contents. The difference between the regular VLAN tunneling setup is that the bridge does not check if the packet is tagged or untagged, it assumes that all packets that are received on a specific port are all untagged packets and will add a new VLAN tag regardless of whether a VLAN tag is present or not, this is called Tag Stacking since it "stacks" VLAN tags on top of the previous tag, regardless of the VLAN tag type. This is a very common setup for networks that do not support the IEEE 802.1ad standard, but still want to encapsulate VLAN traffic into a new VLAN. 

The VLAN tag that is going to be added depends on `ether-type` and `PVID` . For example, if you have `ether-type=0x8100` and `PVID=200` on a port, then the bridge will add a new IEEE 802.1Q VLAN tag right on top of any other tag (if such are present). The same VLAN filtering principles still apply, you have to determine which ports are going to be your trunk ports and mark them as tagged ports, determine your access ports, and add them as untagged ports. 

To explain how VLAN tagging and untagging works with tag stacking, let us use the same network topology as before: 

534 

**==> picture [504 x 225] intentionally omitted <==**

What we want to achieve is that regardless of what is being received on ether2 and ether3 , a new VLAN tag will be added to encapsulate the traffic that is coming from those ports. `Tag-stacking` forces a new VLAN tag, so we can use this property to achieve our desired setup. We are going to be using the same configuration as in the Trunk/Access port setup, but with `tag-stacking` enabled on the access ports: 

```
/interface bridge
add name=bridge1 vlan-filtering=yes ether-type=0x8100
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2 tag-stacking=yes pvid=20
add bridge=bridge1 interface=ether3 tag-stacking=yes pvid=30
/interface bridge vlan
add bridge=bridge1 tagged=ether1 untagged=ether2 vlan-ids=20
add bridge=bridge1 tagged=ether1 untagged=ether3 vlan-ids=30
```

**==> picture [13 x 13] intentionally omitted <==**

The added VLAN tag will use the specified `ether-type` . The selected EtherType will also be used for VLAN filtering. Only the outer tag is checked, but with tag-stacking in place, the tag checking is skipped and assumes that a new tag must be added either way. 

Let us assume that the devices behind ether2 and ether3 are sending tagged VLAN40 traffic. With this configuration, ALL packets will get encapsulated with a new VLAN tag, but you must make sure that you have added the VLAN ID from the outer tag to the bridge VLAN table. The VLAN40 is not added to the bridge VLAN table since it is the inner tag and it is not checked, we are only concerned about the outer tag, which is either VLAN20 or VLAN30 dependi ng on the port. 

Similar to other setups, the bridge VLAN table is going to be used to determine if the VLAN tag needs to be removed or not. For example, ether1 receives tagged VLAN20 packets, the bridge checks that ether2 is allowed to carry VLAN20 so it is about to send it out through ether2 , but it also checks the bridge VLAN table whether the VLAN tag should be removed and since ether2 is marked as an untagged port, then the bridge will forward these packets from ethe r1 to ether2 without the VLAN20 VLAN tag. 

From the access port perspective, the same principles as in the Trunk/Access port setup apply. All packets that are received on ether2 will get a new VLAN tag with the VLAN ID that is specified in PVID, in this case, a new VLAN tag will be added with VLAN20 and this VLAN will be subjected to VLAN filtering. See a packet example below: 

535 

**==> picture [504 x 171] intentionally omitted <==**

A packet example before and after tag stacking 

536

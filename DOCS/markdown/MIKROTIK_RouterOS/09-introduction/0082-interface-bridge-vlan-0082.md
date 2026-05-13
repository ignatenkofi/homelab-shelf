## `/interface bridge vlan` 

```
add bridge=bridge1 tagged=ether1 untagged=ether2,ether3 vlan-ids=20,30
```

Do NOT use multiple VLAN IDs on access ports. This will unintentionally allow both VLAN20 and VLAN30 on both access ports. In the example above, eth er3 is supposed to set a VLAN tag for all ingress packets to use VLAN30 (since `PVID=30` ), but this does not limit the allowed VLANs on this port when VLANs are being sent out through this port. The bridge VLAN table is responsible for deciding whether a VLAN is allowed to be sent through a specific port or not. The entry above specifies that both VLAN20 and VLAN30 are allowed to be sent out through ether2 and ether3 and on top of that the entry specifies that packets should be sent out without a VLAN tag (packets are sent out as untagged packets). As a result, you may create a packet leak from VLANs to ports that are not even supposed to receive such traffic, see the image below. 

**==> picture [504 x 225] intentionally omitted <==**

A misconfigured VLAN table allows VLAN20 to be sent through ether3, it will also allow VLAN30 through ether2 

**==> picture [13 x 13] intentionally omitted <==**

Don't use more than one VLAN ID specified in a bridge VLAN table entry for access ports, you should only specify multiple VLAN IDs for trunk ports. 

It is not necessary to add a bridge port as an untagged port, because each bridge port is added as an untagged port dynamically with a VLAN ID that is specified in the PVID property. This is because of a feature that automatically will add an appropriate entry in the bridge VLAN table for convenience and performance reasons, this feature does have some caveats that you must be aware of. All ports that have the same PVID will be added to a single entry for the appropriate VLAN ID as untagged ports, but note that the Bridge interface also has a VLAN ID. 

For testing purposes, we are going to enable VLAN filtering, but note that it might make you lose access to the device since it does not have management access configured yet (we will configure it later). It is always recommended to configure VLAN filtering while using a serial console, though you can also configure a device through a port, that is not added to a bridge. Make sure you are using a serial console or connected through a different port (that is not in a bridge) and enable VLAN filtering: 

```
/interface bridge set bridge1 vlan-filtering=yes
```

527 

**==> picture [13 x 13] intentionally omitted <==**

You might not lose access to the device as soon as you enable VLAN filtering, but you might get disconnected since the bridge must reset itself in order for VLAN filtering to take any effect, which will force you to reconnect (this is mostly relevant when using MAC-telnet). There is a chance you might be able to access your device using untagged traffic, this scenario is described below. 

If you have enabled VLAN filtering now and printed out the current VLAN table, you would see such a table: 

```
[admin@MikroTik] > /interface bridge vlan print
Flags: X - disabled, D - dynamic
 #   BRIDGE                     VLAN-IDS  CURRENT-TAGGED       CURRENT-UNTAGGED
 0   bridge1                    20        ether1               ether2
 1   bridge1                    30        ether1               ether3
 2 D bridge1                    1                              bridge1
                                                               ether1
```

There is a dynamic entry added for VLAN1 since `PVID=1` is set by default to all bridge ports (including our trunk port, ether1 ), but you should also notice that the bridge1 interface (the CPU port) is also added dynamically. You should be aware that bridge1 is also a bridge port and therefore might get added to the bridge VLAN table dynamically. There is a chance that you might unintentionally allow access to the device because of this feature. For example, if you have followed this guide and left PVID=1 set for the trunk port ( ether1 ) and did not change the PVID for the CPU port ( bridge1 ) as well, then access through ether1 to the device using untagged traffic is allowed, this is also visible when you print out the bridge VLAN table. This scenario is illustrated in the image below: 

**==> picture [504 x 225] intentionally omitted <==**

Unintentionally allowed management access using untagged traffic through the trunk port 

**==> picture [13 x 13] intentionally omitted <==**

Always check the bridge VLAN table if you have not unintentionally allowed certain VLANs or untagged traffic to specific ports, especially the CPU port (bridge). 

There is a simple way to prevent the bridge (CPU port) from being added as an untagged port, you can simply set the PVID on the trunk port to be different than the bridge's PVID (or change the bridge's PVID), but there is another option, which is more intuitive and recommended. Since you are expecting that the trunk port is only supposed to receive tagged traffic (in this example, it should only receive VLAN20/VLAN30 ), but no untagged traffic, then you can use ingress-filtering along with frame-type to filter out unwanted packets, but to fully understand the behavior of ingress filtering, we must first understand the details of management access. 

Management access is used to create a way to access a device through a bridge that has VLAN filtering enabled. You could simply allow untagged access and doing that is fairly simple. Let us say you wanted the workstation behind ether3 to be able to access the device, we assumed before that the workstation is a generic computer that will not use tagged packets and therefore will only send out untagged packets, this means that we should add the CPU port ( bridge1 ) as an untagged interface to the bridge VLAN table, to do so, simply use the same PVID value for the bridge1 and ether3 ports and set both ports as untagged members for the VLAN ID. In this case, you are going to connect from ether3 that has `PVID=30` , so you change the configuration accordingly: 

528 

```
/interface bridge set [find name=bridge1] pvid=30
```

```
/interface bridge vlan set [find vlan-ids=30] untagged=bridge1,ether3
```

**==> picture [13 x 13] intentionally omitted <==**

You can use the feature that dynamically adds untagged ports with the same PVID value, you can simply change the PVID to match between et her3 and bridge1 . 

Allowing access to the device using untagged traffic is not considered a good security practice, a much better way is to allow access to the device using a very specific VLAN sometimes called the management VLAN, in our case, this is going to be VLAN99 . This adds a significant layer of security since an attacker must guess the VLAN ID that is being used for management purposes and then guess the login credentials, on top of this you can even add another layer of security by allowing access to the device using only certain IP addresses. The purpose of this guide is to provide an in-depth explanation, for that reason, we are adding a level of complexity to our setup to understand some possible caveats that you must take into account. We are going to allow access from an access port using tagged traffic (illustrated in the image below). To allow access to the device using VLAN99 from ether3 , we must add a proper entry in the bridge VLAN table. Additionally, a network device connected to ether3 must support VLAN tagging. 

```
/interface bridge vlan
```

```
add bridge=bridge1 tagged=bridge1,ether3 vlan-ids=99
```

**==> picture [500 x 225] intentionally omitted <==**

Management access using tagged traffic through an access port (which makes it a hybrid port) 

**==> picture [13 x 13] intentionally omitted <==**

If PVID for ether1 and bridge1 matches (by default, it does match with 1), then access to the device is allowed using untagged traffic from ether1 because of the feature that dynamically adds untagged ports to the bridge VLAN table. 

But you might notice that access using VLAN99 does not work at this point, this is because you need a VLAN interface that listens for tagged traffic, you can simply create this interface for the appropriate VLAN ID and you can set an IP address for the interface as well: 

```
/interface vlan
add interface=bridge1 name=VLAN99 vlan-id=99
/ip address
add address=192.168.99.2/24 interface=VLAN99
```

**==> picture [13 x 13] intentionally omitted <==**

Our access port ( ether3 ) at this point expects tagged and untagged traffic at the same time, such a port is called a hybrid port . 

529 

At this point, we can benefit from using `ingress-filtering` and `frame-type` . First, we are going to focus on `frame-type` , which limits the allowed packet types (tagged, untagged, both), but for `frame-type` to work properly, `ingress-filtering` must be enabled, otherwise it will not have any effect. In our example, where we wanted to allow access from ether3 using tagged traffic ( VLAN99 ) and at the same time allow a generic workstation to access the network, we can conclude that this port needs to allow tagged and untagged packets, but ether1 and ether2 are supposed to receive only specific types of packets, for this reasons we can enhance our network's security. Since ether1 is our trunk port, it is only supposed to carry tagged packets, but ether2 is our access port so it should not carry any tagged packets, based on these conclusions we can drop invalid packets:

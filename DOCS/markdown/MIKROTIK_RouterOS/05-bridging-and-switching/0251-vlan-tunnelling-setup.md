## VLAN Tunnelling setup 

In some cases, you might want to forward already tagged traffic through certain switches. This is a quite common setup for backbone infrastructures since it provides a possibility to encapsulate traffic from, for example, your edge routers and seamlessly forward it over your backbone to another edge router. Below you can find an example of a VLAN tunneling topology: 

**==> picture [504 x 198] intentionally omitted <==**

**==> picture [82 x 8] intentionally omitted <==**

**----- Start of picture text -----**<br>
Provider bridge topology<br>**----- End of picture text -----**<br>

SVID stands for Service VID, indicating the tag type along with the VID. 

532 

**==> picture [13 x 13] intentionally omitted <==**

To fully understand how to configure VLAN tunneling properly, you should first read the Trunk/Access port setup section before proceeding any further. 

There are two possible ways to achieve this, one is the standardized IEEE 802.1ad way, and the other way is using Tag stacking , we will first review the standardized way since the same principles apply to both ways and only a couple of parameters must be changed to use the other method. The way VLAN tunneling works is that the bridge checks if the outer VLAN tag is using the same VLAN tag as specified as ether-type. If the VLAN tag matches, the packet is considered as a tagged packet, otherwise, it is considered as an untagged packet. 

**==> picture [13 x 13] intentionally omitted <==**

The bridge checks only the outer tag (closest to the MAC address), any other tag is ignored anywhere in a bridge configuration. The bridge is not aware of the packet contents, even though there might be another VLAN tag, only the first VLAN tag is checked. 

The ether-type property allows you to select the following EtherTypes for the VLAN tag: 

- 0x88a8 - IEEE 802.1ad, Service Tag 0x8100 - IEEE 802.1Q, Customer VLAN (regular VLAN tag) 0x9100 - Unofficial tag type (rarely used) 

To properly configure bridge VLAN filtering, you must understand how the bridge distinguishes between tagged and untagged packets. As mentioned before, the bridge will check if EtherType matches with the outer VLAN tag in the packet. For example, consider the following packet: 

```
FFFFFFFFFFFF 6C3B6B7C413E 8100 6063 9999
```

```
----------------------------------------
DST-MAC = FFFFFFFFFFFF
SRC-MAC = 6C3B6B7C413E
Outer EtherType = 8100 (IEEE 802.1Q VLAN tag)
VLAN priority = 6
VLAN ID = 99 (HEX = 63)
Inner EtherType = 9999
```

Let us assume that we have set **`ether-type=0x88a8`** , in this case, the packet above will be considered untagged since the bridge is looking for a different VLAN tag. Lets now consider the following packet: 

```
FFFFFFFFFFFF 6C3B6B7C413E 88A8 6063 8100 5062 9999
```

```
----------------------------------------
DST-MAC = FFFFFFFFFFFF
SRC-MAC = 6C3B6B7C413E
Outer EtherType = 88A8 (IEEE 802.1ad VLAN tag)
VLAN priority = 6
VLAN ID = 99 (HEX = 63)
Inner EtherType 1 = 8100 (IEEE 802.1Q VLAN tag)
VLAN priority = 5
VLAN ID = 98 (HEX = 62)
Innter EtherType 2 = 9999
```

This time let us assume that we have set **`ether-type=0x8100`** , in this case, the packet above is considered as untagged as well since the outer tag is using an IEEE 802.1ad VLAN tag. The same principles apply to other VLAN related functions, for example, the `PVID` property will add a new VLAN tag on access ports and the VLAN tag will be using the EtherType specified in ether-type. 

Both SW1 and SW2 are using the same configuration: 

```
/interface bridge
add name=bridge1 vlan-filtering=yes ether-type=0x88a8
/interface bridge port
add interface=ether1 bridge=bridge1 pvid=200
add interface=ether2 bridge=bridge1 pvid=300
add interface=ether3 bridge=bridge1
/interface bridge vlan
add bridge=bridge1 tagged=ether3 untagged=ether1 vlan-ids=200
add bridge=bridge1 tagged=ether3 untagged=ether2 vlan-ids=300
```

533 

In this example, we are assuming that all routers are passing traffic that is using a regular/customer VLAN tag. Such traffic on switches will be considered as untagged traffic based on the principle described above. Switches will encapsulate this traffic using a Service VLAN tag (the outer 802.1ad tag) and traffic between SW1 and SW2 will be considered as tagged. Before traffic reaches its destination, the switches will decapsulate the outer tag and forward the original 802.1Q tagged frame. See a packet example below: 

**==> picture [504 x 170] intentionally omitted <==**

A packet example before and after 802.1ad VLAN encapsulation 

**==> picture [13 x 13] intentionally omitted <==**

All principles that apply to the regular trunk/access port setup using IEEE 802.1Q also apply to VLAN tunneling setups, make sure you are limiting VLANs and packet type properly using the bridge VLAN table and ingress filtering. 

In case you want to create management access from, let's say, ether3 to the device and want to use VLAN99 , then you would use such commands: 

```
/interface bridge vlan
add bridge=bridge1 tagged=bridge1,ether3 vlan-ids=99
/interface vlan
add interface=bridge1 name=VLAN99 use-service-tag=yes vlan-id=99
/ip address
add address=192.168.99.2/24 interface=VLAN99
```

As you may notice, the only difference is that the VLAN interface is using `use-service-tag=yes` , this sets the VLAN interface to listen to IEEE 802.1ad VLAN tags. This will require you to use the IEEE 802.1ad VLAN tag to access the device using the management VLAN - you will not be able to connect to the device using a regular VLAN tag while bridge VLAN filtering is enabled. The ether-type is set globally and will affect all bridge VLAN filtering functions. 

**==> picture [13 x 13] intentionally omitted <==**

Devices with switch chip Marvell-98DX3257 (e.g. CRS354 series) do not support VLAN filtering on 1Gbps Ethernet interfaces for other VLAN types ( `0x88a8` and `0x9100` ).

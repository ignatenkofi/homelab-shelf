## Tag stacking 

Since RouterOS v6.43 it is possible to forcefully add a new VLAN tag over any existing VLAN tags, this feature can be used to achieve a CVID stacking setup, where a CVID (0x8100) tag is added before an existing CVID tag. This type of setup is very similar to the Provider bridge setup, to achieve the same setup but with multiple CVID tags (CVID stacking) we can use the same topology: 

**==> picture [504 x 198] intentionally omitted <==**

In this example R1 , R2 , R3, and R4 might be sending any VLAN tagged traffic, it can be 802.1ad, 802.1Q or any other type of traffic, but SW1 and SW2 needs isolate traffic between routers in a way that R1 is able to communicate only with R3 , and R2 is only able to communicate with R4 . To do so, you can tag all ingress traffic with a new CVID tag and only allow these VLANs on certain ports. Start by selecting the proper EtherType, use these commands on SW1 and SW2 : 

```
/interface bridge
```

```
add name=bridge1 vlan-filtering=no ether-type=0x8100
```

In this setup, ether1 and ether2 will ignore any VLAN tags that are present and add a new VLAN tag, use the `pvid` parameter to tag all ingress traffic on each port and allow `tag-stacking` on these ports, use these commands on SW1 and SW2 : 

```
/interface bridge port
add interface=ether1 bridge=bridge1 pvid=200 tag-stacking=yes
add interface=ether2 bridge=bridge1 pvid=300 tag-stacking=yes
add interface=ether3 bridge=bridge1
```

381 

Specify tagged and untagged ports in the bridge VLAN table, you only need to specify the VLAN ID of the outer tag, use these commands on SW1 and SW2 : 

```
/interface bridge vlan
```

```
add bridge=bridge1 tagged=ether3 untagged=ether1 vlan-ids=200
add bridge=bridge1 tagged=ether3 untagged=ether2 vlan-ids=300
```

When the bridge VLAN table is configured, you can enable bridge VLAN filtering, which is required in order for the `pvid` parameter to have any effect, use these commands on SW1 and SW2: 

```
/interface bridge set bridge1 vlan-filtering=yes
```

**==> picture [13 x 13] intentionally omitted <==**

By enabling vlan-filtering you will be filtering out traffic destined to the CPU, before enabling VLAN filtering you should make sure that you set up a Management port.

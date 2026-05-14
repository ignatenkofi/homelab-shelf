## VLAN Tunneling (QinQ) 

Since RouterOS v6.43 the RouterOS bridge is IEEE 802.1ad compliant and it is possible to filter VLAN IDs based on Service VLAN ID (0x88a8) rather than Customer VLAN ID (0x8100). The same principles can be applied as with IEEE 802.1Q VLAN filtering (the same setup examples can be used). Below is a topology for a common Provider bridge : 

**==> picture [504 x 199] intentionally omitted <==**

In this example, R1 , R2 , R3, and R4 might be sending any VLAN tagged traffic by 802.1Q (CVID), but SW1 and SW2 needs isolate traffic between routers in a way that R1 is able to communicate only with R3 , and R2 is only able to communicate with R4 . To do so, you can tag all ingress traffic with an SVID and only allow these VLANs on certain ports. Start by enabling the service tag 0x88a8, introduced by `802.1ad` , on the bridge. Use these commands on SW1 and SW2 : 

```
/interface bridge
```

```
add name=bridge1 vlan-filtering=no ether-type=0x88a8
```

In this setup, ether1 and ether2 are going to be access ports (untagged), use the `pvid` parameter to tag all ingress traffic on each port, use these commands on SW1 and SW2 : 

```
/interface bridge port
add interface=ether1 bridge=bridge1 pvid=200
add interface=ether2 bridge=bridge1 pvid=300
add interface=ether3 bridge=bridge1
```

Specify tagged and untagged ports in the bridge VLAN table, use these commands on SW1 and SW2 : 

```
/interface bridge vlan
add bridge=bridge1 tagged=ether3 untagged=ether1 vlan-ids=200
add bridge=bridge1 tagged=ether3 untagged=ether2 vlan-ids=300
```

When the bridge VLAN table is configured, you can enable bridge VLAN filtering, use these commands on SW1 and SW2: 

```
/interface bridge set bridge1 vlan-filtering=yes
```

380 

**==> picture [13 x 13] intentionally omitted <==**

By enabling vlan-filtering you will be filtering out traffic destined to the CPU, before enabling VLAN filtering you should make sure that you set up a Management port. 

Note, that if you are using the new EtherType/TPID 0x88a8 (service tag) and you also need a VLAN interface for your Service VLAN, you will also have to apply the `use-service-tag` parameter on the VLAN interface. 

**==> picture [13 x 13] intentionally omitted <==**

When `ether-type=0x8100` is configured, the bridge checks the outer VLAN tag and sees if it is using EtherType `0x8100` . If the bridge receives a packet with an outer tag that has a different EtherType, it will mark the packet as `untagged` . Since RouterOS only checks the outer tag of a packet, it is not possible to filter 802.1Q packets when the 802.1ad protocol is used. 

**==> picture [13 x 13] intentionally omitted <==**

Currently, only CRS3xx, CRS5xx series switches and CCR2116, CCR2216 routers are capable of hardware offloaded VLAN filtering using the Service tag, EtherType/TPID `0x88a8` . 

**==> picture [13 x 13] intentionally omitted <==**

Devices with switch chip Marvell-98DX3257 (e.g. CRS354 series) do not support VLAN filtering on 1Gbps Ethernet interfaces for other VLAN types ( `0x88a8` and `0x9100` ).

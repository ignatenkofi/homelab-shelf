## `/interface bridge` 

```
set bridge1 frame-types=admit-only-vlan-tagged ingress-filtering=yes
```

This does not only drop untagged packets, but disables the feature that dynamically adds untagged ports to the bridge VLAN table. If you print out the current bridge VLAN table you will notice that bridge1 is not dynamically added as an untagged port: 

```
[admin@MikroTik] > /interface bridge vlan print
Flags: X - disabled, D - dynamic
 #   BRIDGE       VLAN-IDS  CURRENT-TAGGED        CURRENT-UNTAGGED
 0   bridge1      20        ether1
 1   bridge1      30        ether1                ether3
 2 D bridge1      1                               ether1
 3   bridge1      99        bridge1
                            ether3
```

**==> picture [13 x 13] intentionally omitted <==**

When `frame-type=admit-only-vlan-tagged` is used on a port, then the port is not dynamically added as an untagged port for the PVID. 

While `frame-type` can be used to drop a certain type of packet, the `ingress-filtering` can be used to filter out packets before they can be sent out. To fully understand the need for ingress filtering, consider the following scenario: VLAN99 is allowed on ether3 and bridge1 , but you can still send VLAN99 traffic from ether1 to ether3 , this is because the bridge VLAN table checks if a port is allowed to carry a certain VLAN only on egress ports. In our case, eth er3 is allowed to carry VLAN99 and for this reason, it is forwarded. To prevent this you MUST use ingress-filtering. With ingress filtering, ingress packets are also checked, in our case, the bridge VLAN table does not contain an entry that VLAN99 is allowed on ether1 and therefore will be dropped immediately. Of course, in our scenario without ingress filtering connection cannot be established since VLAN99 can be forwarded only from ether1 to ether3 , but not from ether3 to ether1 , though there are still possible attacks that can be used in such a misconfiguration (for example, ARP poisoning). The packet dropping behavior is illustrated in the image below: 

530 

**==> picture [504 x 499] intentionally omitted <==**

Trunk/access port setup with and without ingress filtering. Ingress filtering can prevent unwanted traffic from being forwarded. Note that ether1 is not allowed to carry VLAN99 in the bridge VLAN table. 

**==> picture [13 x 13] intentionally omitted <==**

Always try to use `ingress-filtering` wherever it is possible, it adds a significant layer of security. 

The ingress-filtering can be used on the CPU port (bridge) as well, this can be used to prevent some possible attack vectors and limit the allowed VLANs that can access the CPU. It is better to drop a packet on an ingress port, rather than on an egress port, this reduces the CPU load, which is quite crucial when you are using hardware offloading with bridge VLAN filtering. 

**==> picture [13 x 13] intentionally omitted <==**

The `ingress-filtering` property only affects ingress traffic, but `frame-type` affects both egress and ingress traffic. 

531 

Even though you can limit the allowed VLANs and packet types on a port, it is never a good security practice to allow access to a device through access ports since an attacker could sniff packets and extract the management VLAN's ID, you should only allow access to the device from the trunk port ( ether1 ) since trunk ports usually have better physical security, you should remove the previous entry and allow access to the device through the port that is connected to your router (illustrated in the image below): 

```
/interface bridge vlan
```

```
add bridge=bridge1 tagged=bridge1,ether1 vlan-ids=99
```

**==> picture [504 x 224] intentionally omitted <==**

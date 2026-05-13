## MPLS IP VPN 

In VPNv4 setups packet arriving at PE router that needs to be forwarded to the CE router is not a typical "forward". 

If incoming label and destination is bound to the VRF Then after MPLS label is popped and: 

destination address is local to the router, then packet is moved to LOCAL_IN destination address is in the CE network, then packet is moved to LOCAL_OUT 

**==> picture [13 x 13] intentionally omitted <==**

Forwarded packets from MPLS cloud to the CE network will not show up in the forward. 

For example traffic from src:111.15.0.1 to dst:111.13.0.1 

```
[admin@CCR2004_2XS] /mpls/forwarding-table> print
Flags: L - LDP, P - VPN
Columns: LABEL, VRF, PREFIX, NEXTHOPS
#   LABEL  VRF      PREFIX
NEXTHOPS
0 P    17  myVrf    111.13.0.0/24
4 L    20  main     203.0.113.2    { label=impl-null; nh=111.11.0.1; interface=sfp-sfpplus1 }
[admin@CCR2004_2XS] /mpls/forwarding-table>
...
```

```
[admin@CCR2004_2XS] /ip/route> print detail
Flags: D - dynamic; X - disabled, I - inactive, A - active; c - connect, s - static, r - rip, b - bgp, o -
ospf, i - is-is, d - dhcp, v - vpn, m - modem, y - bgp-mpls-vpn;
H - hw-offloaded; + - ecmp
```

```
   DAc   dst-address=111.11.0.0/24 routing-table=main gateway=sfp-sfpplus1 immediate-gw=sfp-sfpplus1 distance=0
scope=10 suppress-hw-offload=no
         local-address=111.11.0.2%sfp-sfpplus1
   DAc   dst-address=203.0.113.1/32 routing-table=main gateway=lo immediate-gw=lo distance=0 scope=10 suppress-
hw-offload=no local-address=203.0.113.1%lo
   DAo   dst-address=203.0.113.2/32 routing-table=main gateway=111.11.0.1%sfp-sfpplus1 immediate-gw=111.11.0.1%
sfp-sfpplus1 distance=110 scope=20 target-scope=10
```

```
         suppress-hw-offload=no
   DAc   dst-address=111.13.0.0/24 routing-table=myVrf gateway=sfp-sfpplus2@myVrf immediate-gw=sfp-sfpplus2
distance=0 scope=10 suppress-hw-offload=no
```

```
         local-address=111.13.0.2%sfp-sfpplus2@myVrf
   DAy   dst-address=111.15.0.0/24 routing-table=myVrf gateway=203.0.113.2 immediate-gw=111.11.0.1%sfp-sfpplus1
distance=200 scope=40 target-scope=30 suppress-hw-offload=no [admin@CCR2004_2XS] /ip/route>
```

Packet will be seen in the output and postrouting chains, because now it is locally originated packet with source MAC address equal to vrfInterface: 

```
08:10:55 firewall,info output: in:(unknown 0) out:sfp-sfpplus2, connection-state:established src-mac f2:b5:e9:
17:18:3b, proto ICMP (type 8, code 0), 111.15.0.1->111.13.0.1, len 56
```

```
08:10:55 firewall,info postrouting: in:myVrf out:sfp-sfpplus2, connection-state:established src-mac f2:b5:e9:17:
18:3b, proto ICMP (type 8, code 0), 111.15.0.1->111.13.0.1, len 56
```

687 

On the other hand, for packets routed in the direction CE→PE will be seen in the "forward" as any other routed IP traffic before being sent to the MPLS: 

```
 08:10:55 firewall,info prerouting: in:sfp-sfpplus2 out:(unknown 0), connection-state:established src-mac dc:2c:
6e:46:f8:93, proto ICMP (type 0, code 0), 111.13.0.1->111.15.0.1, len 56
```

```
 08:10:55 firewall,info forward: in:sfp-sfpplus2 out:sfp-sfpplus1, connection-state:established src-mac dc:2c:
6e:46:f8:93, proto ICMP (type 0, code 0), 111.13.0.1->111.15.0.1, len 56
```

```
 08:10:55 firewall,info postrouting: in:sfp-sfpplus2 out:sfp-sfpplus1, connection-state:established src-mac dc:
2c:6e:46:f8:93, proto ICMP (type 0, code 0), 111.13.0.1->111.15.0.1, len 56
```

But there can be an exception. If destination IP of reply packet is local to the router and connection tracking is performing NAT translation then connection tracking will "force" packet to move through the firewall prerouting/forward/postrouting chains.

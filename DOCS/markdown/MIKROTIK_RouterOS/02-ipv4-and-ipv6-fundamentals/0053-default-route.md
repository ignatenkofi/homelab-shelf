## Default Route 

A default route is used when the destination cannot be resolved by any other route in the routing table. In RouterOS dst-address of the default route is 0.0.0 .0/0 (for IPv4) and ::/0 (for IPv6) routes. If the routing table contains an active default route, then the routing table lookup in this table will never fail. 

Typically home router routing table contains only connected networks and one default route to forward all outgoing traffic to the ISP's gateway: 

```
[admin@TempTest] /ip/route> print
Flags: D - dynamic; X - disabled, I - inactive, A - active; C - connect, S - static, r - ri
p, b - bgp, o - ospf, d - dhcp, v - vpn
Columns: DST-ADDRESS, GATEWAY, Distance
#      DST-ADDRESS     GATEWAY      D
   DAd 0.0.0.0/0       10.155.125.1 1
   DAC 10.155.125.0/24 ether12      0
   DAC 192.168.1.0/24  vlan2        0
```

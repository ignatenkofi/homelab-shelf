## Multipath (ECMP) routes 

To implement some setups, such as load balancing, it might be necessary to use more than one path to a given destination. 

181 

**==> picture [504 x 359] intentionally omitted <==**

ECMP (Equal cost multi-path) routes have multiple gateways (next-hop) values. All reachable next-hops are copied to FIB and are used to forward packets. 

These routes can be created manually, as well as dynamically by any of the dynamic routing protocols (OSPF, BGP, RIP). Multiple equally preferred routes to the same destination will have assigned + flag and grouped together automatically by RouterOS (see example below). 

```
[admin@TempTest] /ip/route> print
Flags: D - DYNAMIC; I - INACTIVE, A - ACTIVE; C - CONNECT, S - STATIC, m - MODEM; + - ECMP
Columns: DST-ADDRESS, GATEWAY, DISTANCE
#       DST-ADDRESS      GATEWAY       D
0   AS+ 192.168.2.0/24   10.155.125.1  1
1   AS+ 192.168.2.0/24   172.16.1.2    1
```

By default, ECMP uses Layer3 hash policy which hashes source IP and destination IP (for IPv4) or source IP, destination IP, flow label and IP protocol (for IPv6). 

It is possible to change hashing policies in /ip/setting and /ipv6/settings to Layer4 hashing or inner Layer3 hashing. 

**==> picture [427 x 67] intentionally omitted <==**

**----- Start of picture text -----**<br>
IPv4 IPv6<br>L3 srcIPv4, dstIPv4 srcIPv6, dstIPv6, flow label, IP proto<br>L4 srcIPv4, dstIPv4, srcPort, dstPort, IP proto srcIPv6, dstIPv6, srcPort, dstPort, IP Proto<br>**----- End of picture text -----**<br>

182 

L3-Inner srcIPv4, dstIPv4 (if inner IPv4) srcIPv4, dstIPv4 (if inner IPv4) srcIPv6, dstIPv6, flow label, IP proto (if inner IPv6) srcIPv6, dstIPv6, flow label, IP proto (if inner IPv6) Same as L3 if inner is not present. Same as L3 if inner is not present.

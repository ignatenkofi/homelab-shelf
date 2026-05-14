## Verify routes and reachability: 

```
[admin@CCR2004_2XS] /ip/route> print detail
Flags: D - dynamic; X - disabled, I - inactive, A - active;
```

```
c - connect, s - static, r - rip, b - bgp, o - ospf, i - is-is, d - dhcp, v - vpn, m - modem, y - bgp-mpls-vpn;
H - hw-offloaded; + - ecmp
```

```
   DAc   dst-address=111.11.0.0/24 routing-table=vrfTest1 gateway=sfp-sfpplus1@vrfTest1 immediate-gw=sfp-
sfpplus1 distance=0 scope=10 suppress-hw-offload=no
```

```
         local-address=111.11.0.1%sfp-sfpplus1@vrfTest1
```

```
 1  As   dst-address=111.12.0.0/24 routing-table=vrfTest1 pref-src="" gateway=vrfTest2 immediate-gw=vrfTest2
distance=1 scope=30 target-scope=10
         suppress-hw-offload=no
```

```
 2  As   dst-address=111.11.0.0/24 routing-table=vrfTest2 pref-src="" gateway=vrfTest1 immediate-gw=vrfTest1
distance=1 scope=30 target-scope=10
```

```
         suppress-hw-offload=no
```

```
   DAc   dst-address=111.12.0.0/24 routing-table=vrfTest2 gateway=sfp-sfpplus2@vrfTest2 immediate-gw=sfp-
sfpplus2 distance=0 scope=10 suppress-hw-offload=no
```

```
         local-address=111.12.0.1%sfp-sfpplus2@vrfTest2
```

```
[admin@cl2] > /ping 111.11.0.2 src-address=111.12.0.2
  SEQ HOST                                     SIZE TTL TIME
STATUS
    0 111.11.0.2                                 56  64 67us
```

```
    1 111.11.0.2                                 56  64 61us
    sent=2 received=2 packet-loss=0% min-rtt=61us avg-rtt=64u
```

**==> picture [13 x 13] intentionally omitted <==**

Keep in mind that trying to leak overlapping networks will not work. 

But now what if we want to access routers local address located in another vrf? 

1041 

```
[admin@cl2] > /ping 111.11.0.1 src-address=111.12.0.2
  SEQ HOST                                     SIZE TTL TIME
STATUS
    0 111.11.0.1
timeout
    1 111.11.0.1
timeout
    sent=2 received=0 packet-loss=100%
```

Approach with "interface@vrf" gateways works only when router is forwarding packets. To access local vrf addresses we need to route to the vrf interface. 

```
# add vrf routes
/ip route
add dst-address=10.11.0.0/24 gateway=vrfTest1@vrfTest1 routing-table=vrfTest2
add dst-address=10.12.0.0/24 gateway=vrfTest2@vrfTest2 routing-table=vrfTest1
```

```
[admin@cl2] > /ping 111.11.0.1 src-address=111.12.0.2
  SEQ HOST                                     SIZE TTL TIME
STATUS
    0 111.11.0.1                                 56  64 67us
    1 111.11.0.1                                 56  64 61us
    sent=2 received=2 packet-loss=0% min-rtt=61us avg-rtt=64u
```

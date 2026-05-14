## Example output 

```
[admin@MikroTik] /ip/route> print
Flags: D - dynamic; X - disabled, I - inactive, A - active; C - connect, S - stati
c, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn
Columns: DST-ADDRESS, GATEWAY, DIstance
#       DST-ADDRESS      GATEWAY      DI
0   XS   10.155.101.0/24  1.1.1.10
1   XS                    11.11.11.10
   D d   0.0.0.0/0        10.155.101.1 10
2   AS   0.0.0.0/0        10.155.101.1 1
3   AS + 1.1.1.0/24       10.155.101.1 10
4   AS + 1.1.1.0/24       10.155.101.2 10
5   AS   8.8.8.8          2.2.2.2      1
   DAC   10.155.101.0/24  ether12      0
|  ||| |   |                 |         |
|  ||| |   |                 |         \----Distance
|  ||| |   |                 \--Configured gateway
|  ||| |   \-- dst prefix
|  ||| \----- ECMP flag
|  ||\------- flag indicating which protocol have added the route (bgp, osf,static,connected etc.)
|  |\-------- route status flag (active, inactive, disabled)
|  \--------- shows if route is dynamic
\----------- console order number (shown only for static editable routes)
```

`routing route` output is very similar to ip route except that it shows routes from all address families in one menu and lists filtered routes as well. 

```
[admin@MikroTik] /routing/route> print
Flags: X - disabled, I - inactive, F - filtered, U - unreachable, A - active; c - connect, s - static,
r - rip, b - bgp, o - ospf, d - dhcp, v - vpn, a - ldp-address, l - ldp-mapping
Columns: DST-ADDRESS, GATEWAY, DIStance, SCOpe, TARget-scope, IMMEDIATE-GW
     DST-ADDRESS            GATEWAY      DIS SCO TAR IMMEDIATE-GW
Xs   10.155.101.0/24
Xs
d    0.0.0.0/0              10.155.101.1 10  30  10  10.155.101.1%ether12
As   0.0.0.0/0              10.155.101.1 1   30  10  10.155.101.1%ether12
As   1.1.1.0/24             10.155.101.1 10  30  10  10.155.101.1%ether12
As   8.8.8.8                2.2.2.2      1   254 254 10.155.101.1%ether12
Ac   10.155.101.0/24        ether12      0   10      ether12
Ic   2001:db8:2::/64        ether2       0   10
Io   2001:db8:3::/64        ether12      110 20  10
Ic   fe80::%ether2/64       ether2       0   10
Ac   fe80::%ether12/64      ether12      0   10      ether12
Ac   fe80::%bridge-main/64  bridge-main  0   10      bridge-main
A    ether12                             0   250
A    bridge-main                         0   250
```

`routing route print detail` shows more advanced info useful for debugging 

188 

```
[admin@MikroTik] /routing route> print detail
Flags: X - disabled, I - inactive, F - filtered, U - unreachable, A - active;
c - connect, s - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn, a - ldp-address, l - ldp-ma>
+ - ecmp
Xs dst-address=10.155.101.0/24
Xs
d afi=ip4 contribution=best-candidate dst-address=0.0.0.0/0 gateway=10.155.101.1
immediate-gw=10.155.101.1%ether12 distance=10 scope=30 target-scope=10
belongs-to="DHCP route" mpls.in-label=0 .out-label=0 debug.fwp-ptr=0x201C2000
As afi=ip4 contribution=active dst-address=0.0.0.0/0 gateway=10.155.101.1
immediate-gw=10.155.101.1%ether12 distance=1 scope=30 target-scope=10
belongs-to="Static route" mpls.in-label=0 .out-label=0 debug.fwp-ptr=0x201C2000
```

189

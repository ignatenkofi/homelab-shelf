## /routing/route 

A read-only table that lists routes from all the address families as well as all filtered routes with all possible route attributes. 

Default example output of the table with various route types: 

```
[admin@MikroTik] /routing/route> print
Flags: A - ACTIVE; c, s, a, l, y - COPY; H - HW-OFFLOADED
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE, IMMEDIATE-GW
    DST-ADDRESS                 GATEWAY           AFI   D  SCOPE  TA  IMMEDIATE-GW
 lH 10.0.0.0/8                                    ip4   0
;;; defconf
As  10.0.0.0/8                  10.155.130.1      ip4   1     30  10  10.155.130.1%ether1
 lH 10.155.130.0/25                               ip4   0
Ac  10.155.130.0/25             ether1            ip4   0     10      ether1
 aH 10.155.130.12/32                              ip4   0
 lH 111.13.0.0/24                                 ip4   0
Ac  111.13.0.0/24               ether2            ip4   0     10      ether2
 aH 111.13.0.1/32                                 ip4   0
Ac  111.111.111.2/32            loopback@vrfTest  ip4   0     10      loopback
Ac  2111:4::/64                 ether2            ip6   0     10      ether2
Ac  fe80::%ether1/64            ether1            ip6   0     10      ether1
Ac  fe80::%ether2/64            ether2            ip6   0     10      ether2
Ac  fe80::%ether3/64            ether3            ip6   0     10      ether3
Ac  fe80::%ether4/64            ether4            ip6   0     10      ether4
Ac  3333::2/128                 loopback@vrfTest  ip6   0     10      loopback
Ac  fe80::%loopback/64          loopback@vrfTest  ip6   0     10      loopback
Ay  111.111.111.2/32&65530:100  loopback@vrfTest  vpn4  0     10   5  loopback
Ay  3333::2/128&65530:100       loopback@vrfTest  vpn6  0     10   5  loopback
A H ether1                                        link  0
A H ether2                                        link  0
A H ether3                                        link  0
A H ether4                                        link  0
A H loopback                                      link  0
```

Detailed example output with some BGP, OSPF, and other routes: 

982 

```
[admin@MikroTik] /routing/route> print detail
```

```
Flags: X - disabled, F - filtered, U - unreachable, A - active;
```

```
c - connect, s - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn, m - modem, a - ldp-address, l - ldp-
mapping, y - copy; H - hw-offloaded;
```

```
+ - ecmp, B - blackhole
```

```
  o   afi=ip4 contribution=best-candidate dst-address=0.0.0.0/0 routing-table=main gateway=10.155.101.1%ether1
immediate-gw=10.155.101.1%ether1
```

```
       distance=110 scope=20 target-scope=10 belongs-to="OSPF route"
       ospf.metric=2 .tag=111 .type=ext-type-1
       debug.fwp-ptr=0x203425A0
```

```
 Ad + afi=ip4 contribution=active dst-address=0.0.0.0/0 routing-table=main pref-src="" gateway=10.155.101.1
immediate-gw=10.155.101.1%ether1
```

```
       distance=1 scope=30 target-scope=10 vrf-interface=ether1 belongs-to="DHCP route"
       debug.fwp-ptr=0x20342060
```

```
 As + afi=ip4 contribution=active dst-address=0.0.0.0/0 routing-table=main pref-src="" gateway=10.155.101.1
immediate-gw=10.155.101.1%ether1
       distance=1 scope=30 target-scope=10 belongs-to="Static route"
       debug.fwp-ptr=0x20342060
```

```
 Fb   afi=ip4 contribution=filtered dst-address=1.0.0.0/24 routing-table=main gateway=10.155.101.1 immediate-
gw=10.155.101.1%ether1 distance=20
```

```
       scope=40 target-scope=10 belongs-to="BGP IP routes from 10.155.101.217" rpki=valid
       bgp.peer-cache-id=*B000002 .aggregator="13335:172.68.180.1" .as-path="65530,100,9002,13335" .atomic-
aggregate=yes .origin=igp
       debug.fwp-ptr=0x20342960
```

**==> picture [506 x 334] intentionally omitted <==**

**----- Start of picture text -----**<br>
Read-only  Description<br>Property<br>active  (yes | no) A flag indicates whether the route is elected as Active and eligible to be added to the FIB.<br>afi  (ip4 | ip6 | link) Address family this route belongs to.<br>belongs-to  (string) Descriptive info showing from where the route was received.<br>bgp  (yes | no) A flag indicates whether this route was added by the BGP protocol.<br>bgp -  a group of parameters associated with the BGP protocol<br>.as-path (string) value of the AS_PATH BGP attribute<br>.aggregator  (strin<br>g)<br>.atomic-<br>aggregate  (yes |<br>no)<br>.cluster-list  (string<br>)<br>.communities  (str value of the COMMUNITIES BGP attribute<br>ing)<br>.ext- value of the EXTENDED_COMMUNITIES BGP attribute<br>communities  (stri<br>ng)<br>.igp-metric (string) value of the IGP_METRIC BGP attribute<br>**----- End of picture text -----**<br>

983 

**==> picture [506 x 680] intentionally omitted <==**

**----- Start of picture text -----**<br>
.large- value of the LARGE_COMMUNITIES BGP attribute<br>communities  (stri<br>ng)<br>.local-pref  (string) value of the LOCAL_PREF BGP attribute<br>.med  (string) value of the MED BGP attribute<br>.nexthop  (string)<br>.origin  (string)<br>.originator-id  (stri<br>ng)<br>.out-nexthop (stri<br>ng)<br>.peer-cache-id  (s The ID of the BGP session that installed the route. See  /routing/bgp/session  menu.<br>tring)<br>.unknown  (string) hex blob of unknown BGP attributes<br>.weight  (string)<br>blackhole  (yes | no) A flag indicates whether it is a blackhole route<br>check-gateway  (ping  Currently used check-gateway option.<br>| arp | bfd)<br>comment  (string)<br>connect  (yes | no) A flag indicates whether it is a connected network route.<br>contribution  (string) Shows the route status contributing to the election process, e.g "filtered, active, candidate"<br>copy  (yes | no) A flag indicates a copy of the route to be redistributed as the L3VPN route. VPNv4/6 related attributes are attached to this<br>"copy" route.<br>create-time  (string)<br>debug -  a group of debugging parameters<br>dhcp  (yes | no) A flag indicates whether the route was added by the DHCP service.<br>disabled  (yes | no) A flag indicates whether the route is disabled.<br>distance  (integer)<br>dst-address  (prefix) Route destination.<br>ecmp  (yes | no) A flag indicates whether the route is added as an Equal-Cost Multi-Path route in the FIB. Read more>><br>filtered  (yes | no) A flag indicates whether the route was filtered by routing filters and excluded from being used as the best route.<br>gateway  (string) Configured gateway, for the actually resolved gateway, see  immediate-gw  parameter.<br>hw-offloaded  (yes |  Indicates whether the route is eligible to be hardware offloaded on supported hardware.<br>no)<br>immediate-gw  (string) Shows actual (resolved) gateway and interface that will be used for packet forwarding. Displayed in format  [ip%<br>interface] .<br>label  (integer)<br>ldp-address  (yes | no) A flag indicates whether the route entry is an LDP address.<br>ldp-mapping  (yes | no) A flag indicates whether the route entry is the LDP mapping<br>**----- End of picture text -----**<br>

984 

**==> picture [506 x 681] intentionally omitted <==**

**----- Start of picture text -----**<br>
ldp  - a group of parameters associated with the LDP protocol<br>.label  (integer) LDP mapped MPLS label.<br>.peer-id  ()<br>local-address  (IP) Local IP address of the connected network.<br>modem  (yes | no) A flag indicates whether the route is added by the LTE or 3g modems.<br>mpls  - group of generic parameters associated with the MPLS<br>.in-label  () Mapped MPLS ingress label<br>.labels  ()<br>.out-label  () Mapped MPLS egress label<br>nexthop-id  ()<br>ospf  (yes | no) A flag indicates whether the route was added by the OSPF routing protocol.<br>ospf  - group of parameters associated with the OSPF protocol<br>.metric  (integer)<br>.type  (string)<br>pref-src  ()<br>received-from  ()<br>rip  (yes | no) A flag indicates whether the route was added by the RIP routing protocol<br>rip  - group of parameters associated with the RIP protocol<br>.metric  ()<br>.route-tag  ()<br>route-cost  ()<br>routing-table  () Routing table this route belongs to.<br>rpki  (valid | invalid |  Current status of the prefix from the RPKI validation process.<br>unknown)<br>scope  (integer) Scope used in the next-hop lookup process. Read more>><br>static  (yes | no) A flag indicates statically added routes.<br>target-scope  (integer) Target scope used in next-hop lookup process. Read more>><br>te-tunnel-id  () Traffic Engineering tunnel ID<br>total-cost  ()<br>unreachable  (yes | no) A flag indicates whether the route next-hop is unreachable.<br>update-time  ()<br>ve-block-offset<br>ve-block-size<br>ve-id<br>vpn  (yes | no) A flag indicates whether the route was added by one of the VPN protocols (PPPoE, L2TP, SSTP, etc.)<br>vrf-interface  () Internal use only parameter which allows identifying to which VRF route should be added. Used by services that add routes<br>dynamically, for example, DHCP client. Shown for debugging purposes.<br>**----- End of picture text -----**<br>

985

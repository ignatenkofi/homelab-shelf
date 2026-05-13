## Results 

Check that VPNv4 route redistribution is working: 

```
[admin@PE1] /routing/route> print detail where afi="vpn4"
Flags: X - disabled, F - filtered, U - unreachable, A - active;
```

```
c - connect, s - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn, m - modem, a - ldp-address, l - l
dp-mapping, g - slaac, y - bgp-mpls-vpn;
```

```
H - hw-offloaded; + - ecmp, B - blackhole
```

```
 Ab   afi=vpn4 contribution=active dst-address=111.16.0.0/24&1.1.1.1:111 routing-table=main label=16
       gateway=111.111.111.4 immediate-gw=111.13.0.2%ether9 distance=200 scope=40 target-scope=30
       belongs-to="bgp-VPN4-111.111.111.4"
       bgp.peer-cache-id=*2C00011 .as-path="65511" .ext-communities=rt:1.1.1.1:111 .local-pref=100
       .atomic-aggregate=yes .origin=igp
       debug.fwp-ptr=0x202427E0
```

```
[admin@PE1] /routing/bgp/advertisements> print
 0 peer=to-pe2-1 dst=10.1.1.0/24 local-pref=100 origin=2 ext-communities=rt:1.1.1.1:111 atomic-aggregate=yes
```

Check that the 10.3.3.0 is installed in IP routes, in the cust-one route table: 

```
[admin@PE1] > /ip route print where routing-table="cust-one"
Flags: D - DYNAMIC; A - ACTIVE; c, b, y - BGP-MPLS-VPN
Columns: DST-ADDRESS, GATEWAY, DISTANCE
# DST-ADDRESS     GATEWAY         DISTANCE
0 ADC 10.1.1.0/24 ether1@cust-one        0
1 ADb 10.3.3.0/24 10.5.5.3              20
```

Let's take a closer look at IP routes in cust-one VRF. The 10.1.1.0/24 IP prefix is a connected route that belongs to an interface that was configured to belong to cust-one VRF. The 10.3.3.0/24 IP prefix was advertised via BGP as a VPNv4 route from PE2 and is imported in this VRF routing table, because our configured import-route-targets matched the BGP extended communities attribute it was advertised with. 

1047 

```
[admin@PE1] /routing/route> print detail where routing-table="cust-one"
Flags: X - disabled, F - filtered, U - unreachable, A - active;
```

```
c - connect, s - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn, m - modem, a - ldp-address, l - l
dp-mapping, g - slaac, y - bgp-mpls-vpn;
```

```
H - hw-offloaded; + - ecmp, B - blackhole
```

```
 Ac   afi=ip4 contribution=active dst-address=10.1.1.0/24 routing-table=cust-one
       gateway=ether1@cust-one immediate-gw=ether1 distance=0 scope=10 belongs-to="connected"
       local-address=10.1.1.2%ether1@cust-one
       debug.fwp-ptr=0x202420C0
```

```
 Ay   afi=ip4 contribution=active dst-address=10.3.3.0/24 routing-table=cust-one label=16
       gateway=10.5.5.3 immediate-gw=10.2.2.3%ether2 distance=20 scope=40 target-scope=30
       belongs-to="bgp-mpls-vpn-1-bgp-VPN4-10.5.5.3-import"
       bgp.peer-cache-id=*2C00011 .ext-communities=rt:1.1.1.1:111 .local-pref=100
       .atomic-aggregate=yes .origin=igp
       debug.fwp-ptr=0x20242840
```

```
[admin@PE1] /routing/route> print detail where afi="vpn4"
```

```
Flags: X - disabled, F - filtered, U - unreachable, A - active;
```

```
c - connect, s - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn, m - modem, a - ldp-address, l - l
dp-mapping, g - slaac, y - bgp-mpls-vpn;
```

```
H - hw-offloaded; + - ecmp, B - blackhole
```

```
 Ay   afi=vpn4 contribution=active dst-address=10.1.1.0/24&1.1.1.1:111 routing-table=main label=19
       gateway=ether1@cust-one immediate-gw=ether1 distance=200 scope=40 target-scope=10
       belongs-to="bgp-mpls-vpn-1-connected-export"
```

```
       bgp.ext-communities=rt:1.1.1.1:1111 .atomic-aggregate=no .origin=incomplete
       debug.fwp-ptr=0x202426C0
```

```
 Ab   afi=vpn4 contribution=active dst-address=10.3.3.0/24&1.1.1.1:111 routing-table=main label=16
       gateway=10.5.5.3 immediate-gw=10.2.2.3%ether2 distance=200 scope=40 target-scope=30
       belongs-to="bgp-VPN4-10.5.5.3"
```

```
       bgp.peer-cache-id=*2C00011 .ext-communities=rt:1.1.1.1:111 .local-pref=100
       .atomic-aggregate=yes .origin=igp
       debug.fwp-ptr=0x202427E0
```

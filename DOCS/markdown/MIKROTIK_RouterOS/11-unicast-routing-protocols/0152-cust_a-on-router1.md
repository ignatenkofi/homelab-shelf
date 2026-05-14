## CUST_A on Router1 

```
[admin@CCR2004_2XS_111] /routing/route> print detail
```

```
...
 Ay   afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1.1.1.1:1 routing-table=main label=17 gateway=vrf-
dummy@vrfTest
       immediate-gw=vrf-dummy distance=200 scope=40 target-scope=10 belongs-to="bgp-mpls-vpn-1-connected-
export"
       bgp.ext-communities=rt:1:1 .origin=incomplete
       debug.fwp-ptr=0x20302240
```

```
 Ab   afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1.1.1.2:1 routing-table=main label=33 gateway=111.
11.0.1
       immediate-gw=111.11.0.1%sfp-sfpplus1 distance=200 scope=40 target-scope=30 belongs-to="bgp-VPNv4-
111.11.0.1"
       bgp.session=to-tester-1 .ext-communities=rt:1:1 .local-pref=100 .origin=igp
       debug.fwp-ptr=0x20302480
```

```
[admin@CCR2004_2XS_111] /ip/route> print
...
  DAc  111.12.0.0/24       vrf-dummy@vrfTest  vrfTest               0
  D y  111.12.0.0/24       111.11.0.1         vrfTest             200
```

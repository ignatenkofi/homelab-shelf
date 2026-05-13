## SLAAC IPv6 Address 

If under IPv6/Settings menu "accept-router-advertisements" option is enabled and the router receives a Router Advertisement packet, then the SLAAC IPv6 address will be automatically assigned to the interface on which the advertisements were received. This address will have DG flags meaning that the address is dynamic and global. Such addresses will show valid and lifetime parameters. 

```
[admin@R1] /ipv6/address/print detail where dynamic && global
Flags: X - disabled, I - invalid, D - dynamic; G - global, L - link-local
 0 DG address=2001:db8::::ba69:f4ff:fe84:545/64 from-pool="" interface=ether1
      actual-interface=test_fp eui-64=no advertise=no no-dad=no valid=4w2d
      preferred=1w
```

If SLAAC addresses are accepted, then also dynamic route toward the Internet will be generated. It will also contain a few limitations if specified on the advertisement packet. For example, hop-limit and MTU. If multiple addresses are received on the same interface, then the lowest of the MTU values per interface will be used. 

```
[admin@R1] /routing/route/print detail where slaac
Flags: X - disabled, F - filtered, U - unreachable, A - active;
c - connect, s - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn, m - modem, a - ldp-address, l - ldp-
mapping, g - slaac, y - bgp-mpls-vpn;
H - hw-offloaded; + - ecmp, B - blackhole
 Ag + afi=ip6 contribution=active dst-address=::/0 routing-table=main
       pref-src="" gateway=fe80::ba69:f4ff:fe84:7b2%ether1
       immediate-gw=fe80::ba69:f4ff:fe84:7b2%ether1 distance=1 scope=30
       target-scope=10 belongs-to="slaac" mtu=1400 hoplimit=10
       debug.fwp-ptr=0x201C2C00
```

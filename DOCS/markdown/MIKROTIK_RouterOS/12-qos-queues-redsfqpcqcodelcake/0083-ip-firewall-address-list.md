## `/ip firewall address-list` 

```
  add address=0.0.0.0/8 comment="defconf: RFC6890" list=no_forward_ipv4
```

```
  add address=169.254.0.0/16 comment="defconf: RFC6890" list=no_forward_ipv4
  add address=224.0.0.0/4 comment="defconf: multicast" list=no_forward_ipv4
  add address=255.255.255.255/32 comment="defconf: RFC6890" list=no_forward_ipv4
```

In the same case for IPv6, if multicast forwarding is used then the multicast entry should be disabled from the address-list. 

```
/ipv6 firewall address-list
```

```
  add address=fe80::/10  comment="defconf: RFC6890 Linked-Scoped Unicast" list=no_forward_ipv6
  add address=ff00::/8  comment="defconf: multicast" list=no_forward_ipv6
```

`Forward` chain will have a bit more rules than input: 

accept established, related and untracked connections; FastTrack established and related connections (currently only IPv4); 

drop invalid connections; 

drop bad forward IPs, since we cannot reliably determine in RAW chains which packets are forwarded drop connections initiated from the internet (from the WAN side which is not destination NAT`ed); drop bogon IPs that should not be forwarded. 

We are dropping all non-dstnated IPv4 packets to protect direct attacks on the clients if the attacker knows the internal LAN network. Typically this rule would not be necessary since RAW filters will drop such packets, however, the rule is there for double security in case RAW rules are accidentally messed up.

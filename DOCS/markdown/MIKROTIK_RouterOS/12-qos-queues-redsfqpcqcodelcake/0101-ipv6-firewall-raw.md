## `/ipv6 firewall raw` 

```
add action=accept chain=prerouting comment="defconf: enable for transparent firewall" disabled=yes
add action=accept chain=prerouting comment="defconf: RFC4291, section 2.7.1" src-address=::/128 dst-
address=ff02:0:0:0:0:1:ff00::/104 icmp-options=135 protocol=icmpv6
```

```
add action=drop chain=prerouting comment="defconf: drop bogon IP's" src-address-list=bad_ipv6
add action=drop chain=prerouting comment="defconf: drop bogon IP's" dst-address-list=bad_ipv6
```

```
add action=drop chain=prerouting comment="defconf: drop packets with bad SRC ipv6" src-address-list=bad_src_ipv6
add action=drop chain=prerouting comment="defconf: drop packets with bad dst ipv6" dst-address-list=bad_dst_ipv6
add action=drop chain=prerouting comment="defconf: drop non global from WAN" src-address-list=not_global_ipv6
in-interface-list=WAN
```

```
add action=jump chain=prerouting comment="defconf: jump to ICMPv6 chain" jump-target=icmp6 protocol=icmpv6
add action=accept chain=prerouting comment="defconf: accept local multicast scope" dst-address=ff02::/16
add action=drop chain=prerouting comment="defconf: drop other multicast destinations" dst-address=ff00::/8
add action=accept chain=prerouting comment="defconf: accept everything else from WAN" in-interface-list=WAN
add action=accept chain=prerouting comment="defconf: accept everything else from LAN" in-interface-list=LAN
add action=drop chain=prerouting comment="defconf: drop the rest"
```

Notice that the optional ICMP chain was used. If you want a very strict firewall then such strict ICMP filtering can be used, but in most cases, it is not necessary and simply adds more load on the router's CPU. ICMP rate limit in most cases is also unnecessary since the Linux kernel is already limiting ICMP packets to 100pps 

```
/ipv6 firewall raw
# Be aware that different operating systems originate packets with different default TTL values
add action=drop chain=icmp6 comment="defconf: rfc4890 drop ll if hop-limit!=255" dst-address=fe80::/10 hop-
limit=not-equal:255 protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: dst unreachable" icmp-options=1:0-255 protocol=icmpv6
add action=accept chain=icmp6 comment="defconf: packet too big" icmp-options=2:0-255 protocol=icmpv6
add action=accept chain=icmp6 comment="defconf: limit exceeded" icmp-options=3:0-1 protocol=icmpv6
add action=accept chain=icmp6 comment="defconf: bad header" icmp-options=4:0-2 protocol=icmpv6
add action=accept chain=icmp6 comment="defconf: Mobile home agent address discovery" icmp-options=144:0-255
protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: Mobile home agent address discovery" icmp-options=145:0-255
protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: Mobile prefix solic" icmp-options=146:0-255 protocol=icmpv6
add action=accept chain=icmp6 comment="defconf: Mobile prefix advert" icmp-options=147:0-255 protocol=icmpv6
add action=accept chain=icmp6 comment="defconf: echo request limit 5,10" icmp-options=128:0-255 limit=5,10:
packet protocol=icmpv6
add action=accept chain=icmp6 comment="defconf: echo reply limit 5,10" icmp-options=129:0-255 limit=5,10:packet
protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: rfc4890 router solic limit 5,10 only LAN" hop-limit=equal:255
icmp-options=133:0-255 in-interface-list=LAN limit=5,10:packet protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: rfc4890 router advert limit 5,10 only LAN" hop-limit=equal:255
icmp-options=134:0-255 in-interface-list=LAN limit=5,10:packet protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: rfc4890 neighbor solic limit 5,10 only LAN" hop-limit=equal:255
icmp-options=135:0-255 in-interface-list=LAN limit=5,10:packet protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: rfc4890 neighbor advert limit 5,10 only LAN" hop-limit=equal:
255 icmp-options=136:0-255 in-interface-list=LAN limit=5,10:packet protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: rfc4890 inverse ND solic limit 5,10 only LAN" hop-limit=equal:
255 icmp-options=141:0-255 in-interface-list=LAN limit=5,10:packet protocol=icmpv6
```

```
add action=accept chain=icmp6 comment="defconf: rfc4890 inverse ND advert limit 5,10 only LAN" hop-limit=equal:
255 icmp-options=142:0-255 in-interface-list=LAN limit=5,10:packet protocol=icmpv6
add action=drop chain=icmp6 comment="defconf: drop other icmp" protocol=icmpv6
```

739

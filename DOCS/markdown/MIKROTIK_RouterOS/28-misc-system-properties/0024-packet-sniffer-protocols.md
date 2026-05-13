## Packet Sniffer Protocols 

In this submenu, you can see all sniffed protocols and their share of the whole sniffed amount. 

```
[admin@MikroTik] /tool sniffer protocol> print
 # PROTOCOL IP-PROTOCOL PORT                                     PACKETS      BYTES        SHARE
 0 802.2                                                              1         60        0.05%
 1 ip                                                               215     100377       99.04%
 2 arp                                                                2        120        0.11%
 3 ipv6                                                               6        788        0.77%
 4 ip       tcp                                                     210      99981       98.65%
 5 ip       udp                                                       3        228        0.22%
 6 ip       ospf                                                      2        168        0.16%
 7 ip       tcp         8291 (winbox)                               210      99981       98.65%
 8 ip       tcp         36771                                       210      99981       98.65%
 9 ip       udp         646                                           3        228        0.22%
```

1798

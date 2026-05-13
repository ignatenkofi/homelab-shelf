## and Router2: 

```
/interface bonding set [find name=bond1] link-monitoring=arp arp-ip-targets=172.16.0.1
```

We will not change the arp-interval value in our example, RouterOS sets arp-interval to 100ms by default. Unplug one of the cables to test if the link monitoring works correctly, you might notice some ping timeouts until arp monitoring detects link failure. 

```
[admin@MikroTik] > ping 172.16.0.2
```

```
  SEQ HOST                                     SIZE TTL TIME  STATUS
    0 172.16.0.2                                 56  64 0ms
    1 172.16.0.2                                 56  64 0ms
    2 172.16.0.2                                 56  64 0ms
    3 172.16.0.2                                 56  64 0ms
    4 172.16.0.2                                              timeout
    5 172.16.0.2                                 56  64 0ms
    6 172.16.0.2                                 56  64 0ms
    sent=7 received=6 packet-loss=14% min-rtt=0ms avg-rtt=0ms max-rtt=0ms
```

765 

**==> picture [13 x 13] intentionally omitted <==**

For ARP monitoring to work properly it is not required to have any IP address on the device, ARP monitoring will work regardless of the IP address that is set on any interface. 

**==> picture [13 x 13] intentionally omitted <==**

When ARP monitoring is used, bonding slaves will send out ARP requests without a VLAN tag, even if an IP address is set on a VLAN interface in the same subnet as the arp-ip-targets

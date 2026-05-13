## MAC Ping Server 

MAC Ping Server can be either set to be "disabled" or "enabled": 

```
[admin@device] > tool mac-server ping print
  enabled: yes
```

You can enable or disable MAC ping with the help of the commands ( enable=yes → to enable the feature; enable=no → to disable the feature): 

```
[admin@device] > tool mac-server ping set enabled=yes
[admin@device] > tool mac-server ping set enabled=no
```

When MAC Ping is enabled, other hosts on the same broadcast domain can use ping tool to ping the mac address. For example, you can issue the following command to check MAC ping results: 

```
[admin@device] > /ping 00:0C:42:72:A1:B0
HOST                                    SIZE  TTL TIME  STATUS
00:0C:42:72:A1:B0                       56        0ms
00:0C:42:72:A1:B0                       56        0ms
    sent=2 received=2 packet-loss=0% min-rtt=0ms avg-rtt=0ms max-rtt=0ms
```

**==> picture [13 x 13] intentionally omitted <==**

If you disable the MAC server ping feature, the host's ARP ping functionality will also be disabled. 

**==> picture [13 x 13] intentionally omitted <==**

By default, a MAC ping attempts to reach the destination through all active interfaces. This can generate unwanted traffic and duplicate replies if the destination is reachable via multiple interfaces. To restrict a MAC ping to a specific interface, use the interface selector (append `%` followed by the interface name to the MAC address). For example: `/ping 00:11:22:33:44:55%ether1` 

222

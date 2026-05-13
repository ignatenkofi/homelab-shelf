## Rate limiting 

It is possible to set the bandwidth to a specific IPv4 address by using DHCPv4 leases. This can be done by setting a rate limit on the DHCPv4 lease itself, by doing this a dynamic simple queue rule will be added for the IPv4 address that corresponds to the DHCPv4 lease. By using the rate-limit parameter you can conveniently limit a user's bandwidth. 

**==> picture [13 x 13] intentionally omitted <==**

For any queues to work properly, the traffic must not be FastTracked, make sure your Firewall does not FastTrack traffic that you want to limit. 

First, make the DHCPv4 lease static, otherwise, it will not be possible to set a rate limit to a DHCPv4 lease: 

897 

```
[admin@MikroTik] > /ip dhcp-server lease print
Flags: X - disabled, R - radius, D - dynamic, B - blocked
 #   ADDRESS               MAC-ADDRESS       HOST-NAME               SERVER               RATE-
LIMIT               STATUS
 0 D 192.168.88.254        6C:3B:6B:7C:41:3E MikroTik
DHCPv4_Server                                 bound
```

```
[admin@MikroTik] > /ip dhcp-server lease make-static 0
```

```
[admin@MikroTik] > /ip dhcp-server lease print
Flags: X - disabled, R - radius, D - dynamic, B - blocked
 #   ADDRESS               MAC-ADDRESS       HOST-NAME               SERVER               RATE-
LIMIT               STATUS
 0   192.168.88.254        6C:3B:6B:7C:41:3E MikroTik
DHCPv4_Server                                 bound
```

Then you can set a rate to a DHCPv4 lease that will create a new dynamic simple queue entry: 

```
[admin@MikroTik] > /ip dhcp-server lease set 0 rate-limit=10M/10M
```

```
[admin@MikroTik] > /queue simple print
Flags: X - disabled, I - invalid, D - dynamic
 0  D name="dhcp-ds<6C:3B:6B:7C:41:3E>" target=192.168.88.254/32 parent=none packet-marks="" priority=8/8
queue=default-small/default-small limit-at=10M/10M max-limit=10M/10M burst-limit=0/0 burst-threshold=0/0 burst-
time=0s/0s
      bucket-size=0.1/0.1
```

**==> picture [13 x 13] intentionally omitted <==**

By default allow-dual-stack-queue is enabled, this will add a single dynamic simple queue entry for both DHCPv6 binding and DHCPv4 lease, without this option enabled separate dynamic simple queue entries will be added for IPv6 and IPv4. 

If allow-dual-stack-queue is enabled, then a single dynamic simple queue entry will be created containing both IPv4 and IPv6 addresses: 

```
[admin@MikroTik] > /queue simple print
Flags: X - disabled, I - invalid, D - dynamic
 0  D name="dhcp-ds<6C:3B:6B:7C:41:3E>" target=192.168.88.254/32,fdb4:4de7:a3f8:418c::/66 parent=none packet-
marks="" priority=8/8 queue=default-small/default-small limit-at=10M/10M max-limit=10M/10M burst-limit=0/0
burst-threshold=0/0
```

```
      burst-time=0s/0s bucket-size=0.1/0.1
```

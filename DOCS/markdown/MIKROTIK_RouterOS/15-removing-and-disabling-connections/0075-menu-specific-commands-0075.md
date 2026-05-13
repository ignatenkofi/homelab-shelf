## Menu specific commands 

Property Description make-static () Set dynamic binding as static. send-reconfigure (id) Send Reconfigure (forcerenew) message 

Rate limiting 

907 

It is possible to set the bandwidth to a specific IPv6 address by using DHCPv6 bindings. This can be done by setting a rate limit on the DHCPv6 binding itself, by doing this a dynamic simple queue rule will be added for the IPv6 address that corresponds to the DHCPv6 binding. By using the `rate-limit` the parameter you can conveniently limit a user's bandwidth. 

**==> picture [13 x 13] intentionally omitted <==**

For any queues to work properly, the traffic must not be FastTracked, make sure your Firewall does not FastTrack traffic that you want to limit. 

First, make the DHCPv6 binding static, otherwise, it will not be possible to set a rate limit to a DHCPv6 binding: 

```
[admin@MikroTik] > /ipv6 dhcp-server binding print
Flags: X - disabled, D - dynamic
# ADDRESS DUID SERVER STATUS
0 D fdb4:4de7:a3f8:418c::/66 0x6c3b6b7c413e DHCPv6_Server bound
```

```
[admin@MikroTik] > /ipv6 dhcp-server binding make-static 0
```

```
[admin@MikroTik] > /ipv6 dhcp-server binding print
Flags: X - disabled, D - dynamic
# ADDRESS DUID SERVER STATUS
0 fdb4:4de7:a3f8:418c::/66 0x6c3b6b7c413e DHCPv6_Server bound
```

Then you need can set a rate to a DHCPv6 binding that will create a new dynamic simple queue entry: 

```
[admin@MikroTik] > /ipv6 dhcp-server binding set 0 rate-limit=10M/10
```

```
[admin@MikroTik] > /queue simple print
```

```
Flags: X - disabled, I - invalid, D - dynamic
```

```
0 D name="dhcp<6c3b6b7c413e fdb4:4de7:a3f8:418c::/66>" target=fdb4:4de7:a3f8:418c::/66 parent=none packet-
marks="" priority=8/8 queue=default
```

```
-small/default-small limit-at=10M/10M max-limit=10M/10M burst-limit=0/0
burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1
```

**==> picture [13 x 13] intentionally omitted <==**

By default `allow-dual-stack-queue` is enabled, this will add a single dynamic simple queue entry for both DHCPv6 binding and DHCPv4 lease, without this option enabled separate dynamic simple queue entries will be added for IPv6 and IPv4. 

If `allow-dual-stack-queue` is enabled, then a single dynamic simple queue entry will be created containing both IPv4 and IPv6 addresses: 

```
[admin@MikroTik] > /queue simple print
```

```
Flags: X - disabled, I - invalid, D - dynamic
```

```
 0 D name="dhcp-ds<6C:3B:6B:7C:41:3E>" target=192.168.1.200/32,fdb4:4de7:a3f8:418c::/66 parent=none packet-
marks="" priority=8/8 queue=default
```

```
-small/default-small limit-at=10M/10M max-limit=10M/10M
burst-limit=0/0 burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1
```

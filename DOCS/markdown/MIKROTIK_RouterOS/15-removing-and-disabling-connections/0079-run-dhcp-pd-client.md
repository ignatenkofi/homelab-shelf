## Run DHCP-PD client: 

```
sudo dhcp6c -d -D -f eth2
```

Verify that prefix was added to the: 

909 

```
mrz@bumba:/media/aaa$ ip -6 addr
```

```
 ..
```

```
2: eth3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qlen 1000
 inet6 2001:db8:7501:1:200:ff:fe00:0/64 scope global
 valid_lft forever preferred_lft forever
 inet6 fe80::224:1dff:fe17:81f7/64 scope link
 valid_lft forever preferred_lft forever
```

You can make binding to specific client static so that it always receives the same prefix: 

```
[admin@RB493G] /ipv6 dhcp-server binding> print
Flags: X - disabled, D - dynamic
# ADDRESS DU IAID SER.. STATUS 0 D 2001:db8:7501:1::/62 16 0 loc.. bound
[admin@RB493G] /ipv6 dhcp-server binding> make-static 0
```

DHCP-PD also installs a route to assigned prefix into IPv6 routing table: 

```
[admin@RB493G] /ipv6 route> print
 Flags: X - disabled, A - active, D - dynamic, C - connect, S - static, r - rip, o - ospf, b - bgp, U -
unreachable
 # DST-ADDRESS GATEWAY DISTANCE
```

```
...
2 ADS 2001:db8:7501:1::/62 fe80::224:1dff:fe17:8... 1
```

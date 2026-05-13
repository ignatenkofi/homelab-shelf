## Testing 

First of all, check if both routers have correct flags at VRRP interfaces. On router R1 it should look like this 

```
/interface vrrp print detail
```

```
 0   RM name="vrrp1" mtu=1500 mac-address=00:00:5E:00:01:31 arp=enabled interface=ether1 vrid=49
        priority=254 interval=1 preemption-mode=yes authentication=none password="" on-backup=""
        on-master="" version=3 v3-protocol=ipv4
```

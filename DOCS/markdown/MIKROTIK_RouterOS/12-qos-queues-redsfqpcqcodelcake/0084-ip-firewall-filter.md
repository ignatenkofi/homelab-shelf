## `/ip firewall filter` 

```
  add action=accept chain=forward comment="defconf: accept all that matches IPSec policy" ipsec-policy=in,ipsec
disabled=yes
```

```
  add action=fasttrack-connection chain=forward comment="defconf: fasttrack" connection-state=established,
related
```

```
  add action=accept chain=forward comment="defconf: accept established,related, untracked" connection-
state=established,related,untracked
```

```
  add action=drop chain=forward comment="defconf: drop invalid" connection-state=invalid
```

```
  add action=drop chain=forward comment="defconf:  drop all from WAN not DSTNATed" connection-nat-state=!dstnat
connection-state=new in-interface-list=WAN
```

```
  add action=drop chain=forward src-address-list=no_forward_ipv4 comment="defconf: drop bad forward IPs"
  add action=drop chain=forward dst-address-list=no_forward_ipv4 comment="defconf: drop bad forward IPs"
```

IPv6 `forward` chain is very similar, except that IPsec and HIP are accepted as per RFC recommendations, and ICMPv6 with `hop-limit=1` is dropped. 

735

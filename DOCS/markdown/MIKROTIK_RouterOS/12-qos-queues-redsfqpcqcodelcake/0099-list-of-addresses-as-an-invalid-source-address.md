## List of addresses as an invalid source address 

```
/ipv6 firewall address-list
  add address=::/128 comment="defconf: unspecified" list=bad_src_ipv6
  add address=ff00::/8  comment="defconf: multicast" list=bad_src_ipv6
```

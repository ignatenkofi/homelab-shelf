## First, address-list contains all IPv4 addresses that cannot be used as src/dst/forwarded, etc. (will be dropped immediately if such address is seen) 

```
/ip firewall address-list
```

```
  add address=127.0.0.0/8 comment="defconf: RFC6890" list=bad_ipv4
  add address=192.0.0.0/24 comment="defconf: RFC6890" list=bad_ipv4
  add address=192.0.2.0/24 comment="defconf: RFC6890 documentation" list=bad_ipv4
  add address=198.51.100.0/24 comment="defconf: RFC6890 documentation" list=bad_ipv4
  add address=203.0.113.0/24 comment="defconf: RFC6890 documentation" list=bad_ipv4
  add address=240.0.0.0/4 comment="defconf: RFC6890 reserved" list=bad_ipv4
```

Another address list contains all IPv4 addresses that cannot be routed globally. 

736 

```
/ip firewall address-list
  add address=0.0.0.0/8 comment="defconf: RFC6890" list=not_global_ipv4
  add address=10.0.0.0/8 comment="defconf: RFC6890" list=not_global_ipv4
  add address=100.64.0.0/10 comment="defconf: RFC6890" list=not_global_ipv4
  add address=169.254.0.0/16 comment="defconf: RFC6890" list=not_global_ipv4
  add address=172.16.0.0/12 comment="defconf: RFC6890" list=not_global_ipv4
  add address=192.0.0.0/29 comment="defconf: RFC6890" list=not_global_ipv4
  add address=192.168.0.0/16 comment="defconf: RFC6890" list=not_global_ipv4
  add address=198.18.0.0/15 comment="defconf: RFC6890 benchmark" list=not_global_ipv4
  add address=255.255.255.255/32 comment="defconf: RFC6890" list=not_global_ipv4
```

And last two address lists for addresses that cannot be as destination or source address. 

```
/ip firewall address-list
  add address=224.0.0.0/4 comment="defconf: multicast" list=bad_src_ipv4
  add address=255.255.255.255/32 comment="defconf: RFC6890" list=bad_src_ipv4
add address=0.0.0.0/8 comment="defconf: RFC6890" list=bad_dst_ipv4
  add address=224.0.0.0/4 comment="defconf: RFC6890" list=bad_dst_ipv4
```

## `/ipv6 firewall filter` 

```
add action=accept chain=forward comment=established,related connection-state=established,related
add action=drop chain=forward comment=invalid connection-state=invalid log=yes log-prefix=ipv6,invalid
add action=accept chain=forward comment=icmpv6 in-interface=!in_interface_name protocol=icmpv6
```

```
add action=accept chain=forward comment="local network" in-interface=!in_interface_name src-address-list=allowed
add action=drop chain=forward log-prefix=IPV6
```

641

## `/ipv6 firewall filter` 

```
add action=accept chain=input comment="allow established and related" connection-state=established,related
add chain=input action=accept protocol=icmpv6 comment="accept ICMPv6"
```

```
add chain=input action=accept protocol=udp port=33434-33534 comment="defconf: accept UDP traceroute"
```

```
add chain=input action=accept protocol=udp dst-port=546 src-address=fe80::/10 comment="accept DHCPv6-Client
prefix delegation."
```

```
add action=drop chain=input in-interface=in_interface_name log=yes log-prefix=dropLL_from_public src-
address=fe80::/10
```

```
add action=accept chain=input comment="allow allowed addresses" src-address-list=allowed
add action=drop chain=input
```

```
/ipv6 firewall address-list
add address=fe80::/16 list=allowed
add address=xxxx::/48 list=allowed
add address=ff02::/16 comment=multicast list=allowed
```

**==> picture [13 x 13] intentionally omitted <==**

In certain setups where the DHCPv6 relay is used, the src address of the packets may not be from the link-local range. In that case, the srcaddress parameter of rule #4 must be removed or adjusted to accept the relay address.

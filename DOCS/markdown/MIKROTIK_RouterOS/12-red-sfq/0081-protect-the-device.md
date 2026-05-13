## Protect the Device 

The main goal here is to allow access to the router only from LAN and drop everything else. 

Notice that ICMP is accepted here as well, it is used to accept ICMP packets that passed RAW rules. 

```
/ip firewall filter
```

```
  add action=accept chain=input comment="defconf: accept ICMP after RAW" protocol=icmp
  add action=accept chain=input comment="defconf: accept established,related,untracked" connection-
state=established,related,untracked
```

```
  add action=drop chain=input comment="defconf: drop all not coming from LAN" in-interface-list=!LAN
```

IPv6 part is a bit more complicated, in addition, UDP traceroute, DHCPv6 client PD, and IPSec (IKE, AH, ESP) are accepted as per RFC recommendations. 

```
/ipv6 firewall filter
```

```
add action=accept chain=input comment="defconf: accept ICMPv6 after RAW" protocol=icmpv6
add action=accept chain=input comment="defconf: accept established,related,untracked" connection-
state=established,related,untracked
```

```
add action=accept chain=input comment="defconf: accept UDP traceroute" dst-port=33434-33534 protocol=udp
add action=accept chain=input comment="defconf: accept DHCPv6-Client prefix delegation." dst-port=546
protocol=udp src-address=fe80::/10
```

```
add action=accept chain=input comment="defconf: accept IKE" dst-port=500,4500 protocol=udp
add action=accept chain=input comment="defconf: accept IPSec AH" protocol=ipsec-ah
add action=accept chain=input comment="defconf: accept IPSec ESP" protocol=ipsec-esp
add action=drop chain=input comment="defconf: drop all not coming from LAN" in-interface-list=!LAN
```

734 

**==> picture [13 x 13] intentionally omitted <==**

In certain setups where the DHCPv6 relay is used, the src address of the packets may not be from the link-local range. In that case, the srcaddress parameter of rule #4 must be removed or adjusted to accept the relay address.

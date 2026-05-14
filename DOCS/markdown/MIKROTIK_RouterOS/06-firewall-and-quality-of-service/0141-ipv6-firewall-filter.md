## `/ipv6 firewall filter` 

```
add action=accept chain=forward comment="defconf: accept established,related,untracked" connection-
state=established,related,untracked
```

```
add action=drop chain=forward comment="defconf: drop invalid" connection-state=invalid
```

```
add action=drop chain=forward src-address-list=no_forward_ipv6 comment="defconf: drop bad forward IPs"
add action=drop chain=forward dst-address-list=no_forward_ipv6 comment="defconf: drop bad forward IPs"
add action=drop chain=forward comment="defconf: rfc4890 drop hop-limit=1" hop-limit=equal:1 protocol=icmpv6
add action=accept chain=forward comment="defconf: accept ICMPv6 after RAW" protocol=icmpv6
add action=accept chain=forward comment="defconf: accept HIP" protocol=139
```

```
add action=accept chain=forward comment="defconf: accept IKE" protocol=udp dst-port=500,4500
add action=accept chain=forward comment="defconf: accept AH" protocol=ipsec-ah
add action=accept chain=forward comment="defconf: accept ESP" protocol=ipsec-esp
```

```
add action=accept chain=forward comment="defconf: accept all that matches IPSec policy" ipsec-policy=in,ipsec
add action=drop chain=forward comment="defconf: drop everything else not coming from LAN" in-interface-list=!LAN
```

Notice the IPsec policy matcher rules. It is very important that IPsec encapsulated traffic bypass fast-track. That is why as an illustration we have added a disabled rule to accept traffic matching IPsec policies. Whenever IPsec tunnels are used on the router this rule should be enabled. For IPv6 it is much more simple since it does not have fast-track support. 

Another approach to solving the IPsec problem is to add RAW rules, we will talk about this method later in the RAW section

## IPsec policy matcher 

Let's set up an IPsec policy matcher to accept all packets that matched any of the IPsec policies and drop the rest: 

```
add chain=input comment="ipsec policy matcher" in-interface=WAN ipsec-policy=in,ipsec
add action=drop chain=input comment="drop all" in-interface=WAN log=yes
```

IPsec policy matcher takes two parameters direction, policy . We used incoming direction and IPsec policy. IPsec policy option allows us to inspect packets after decapsulation, so for example, if we want to allow only GRE encapsulated packet from a specific source address and drop the rest we could set up the following rules: 

```
add chain=input comment="ipsec policy matcher" in-interface=WAN ipsec-policy=in,ipsec protocol=gre
src=address=192.168.33.1
```

```
add action=drop chain=input comment="drop all" in-interface=WAN log=yes
```

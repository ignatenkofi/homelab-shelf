## On client: 

```
[admin@CE1] /ipv6 dhcp-client> print
Flags: D - dynamic, X - disabled, I - invalid
# INTERFACE STATUS REQUEST PREFIX
0 to-R1 bound prefix 2001:db8:1::/64
```

```
[admin@CE1] /ipv6 dhcp-client> /ipv6 pool print
Flags: D - dynamic
# NAME PREFIX PREFIX-LENGTH
0 D my-ipv6 2001:db8:1::/64 64
```

We can also see that IPv6 address was automatically added from the prefix pool:

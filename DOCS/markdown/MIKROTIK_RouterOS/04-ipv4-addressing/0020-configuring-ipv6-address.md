## Configuring IPv6 Address 

This example shows how to set up simple addressing with global IPv6 addresses between two routers. 

R1 configuration: 

```
/ipv6 address
add address=2001:DB8::1/64 interface=ether1 advertise=no
```

R2 configuration: 

```
/ipv6 address
add address=2001:DB8::2/64 interface=ether1 advertise=no
```

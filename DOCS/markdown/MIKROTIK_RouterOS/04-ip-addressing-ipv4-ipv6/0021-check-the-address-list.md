## Check the address list: 

```
[admin@R1] /ipv6 address> print
Flags: X - disabled, I - invalid, D - dynamic, G - global, L - link-local
#    ADDRESS                                     FROM-POOL INTERFACE     ADVERTISE
0  G 2001:db8::1/64                                        ether1        no
3 DL fe80::219:d1ff:fe39:3535/64                           ether1        no
```

167 

Notice that our added address has a G flag indicating that this address can be globally routed. We also have a link-local address on the interface which is created automatically for every IPv6-capable interface. 

Test connectivity: 

```
[admin@R1] /ipv6 address> /ping 2001:DB8::2
HOST                                     SIZE TTL TIME  STATUS
2001:db8::2                 56  64 12ms  echo reply
2001:db8::2                 56  64 0ms   echo reply
    sent=2 received=2 packet-loss=0% min-rtt=0ms avg-rtt=6ms max-rtt=12ms
```

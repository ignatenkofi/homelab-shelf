## `/ipv6 dhcp-client` 

```
 add interface=to-R1 request=prefix pool-name=my-ipv6
```

```
/ipv6 address add address=::1/64 from-pool=my-ipv6 interface=to-clients advertise=yes
```

## Simple DHCPv6 client 

This simple example demonstrates how to enable dhcp client to receive IPv6 prefix and add it to the pool. 

```
/ipv6 dhcp-client add request=prefix pool-name=test-ipv6 pool-prefix-length=64 interface=ether13
```

Detailed print should show status of the client and we can verify if prefix is received 

```
[admin@x86-test] /ipv6 dhcp-client> print detail
Flags: D - dynamic, X - disabled, I - invalid
```

```
 0 interface=bypass pool-name="test-ipv6" pool-prefix-length=64 status=bound
prefix=2001:db8:7501:ff04::/62 expires-after=2d23h11m53s request=prefix
```

Notice that server gave us prefix 2a02:610:7501:ff04::/62 . And it should be also added to ipv6 pools 

```
[admin@MikroTik] /ipv6 pool> print
Flags: D - dynamic
# NAME PREFIX REQUEST PREFIX-LENGTH
0 D test-ipv6 2001:db8:7501:ff04::/62 prefix 64
```

It works! Now you can use this pool, for example, for pppoe clients. 

890

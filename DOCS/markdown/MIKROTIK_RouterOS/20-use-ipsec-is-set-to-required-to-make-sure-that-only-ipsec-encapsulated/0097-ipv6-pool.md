## `/ipv6 pool` 

```
add name=myPool prefix=2001:db8:7501:ff00::/60 prefix-length=62
```

Now we can configure PPP profile and add PPPoE server 

```
/ppp profile set default dhcpv6-pd-pool=myPool
```

```
/interface pppoe-server server
add service-name=test interface=ether1
```

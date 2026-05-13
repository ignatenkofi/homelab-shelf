## At first we create an `address-list` from which you allow access to the device: 

```
/ipv6 firewall address-list add address=fd12:672e:6f65:8899::/64 list=allowed
```

Brief IPv6 firewall filter rule explanation: 

work with new packets, accept established/related packets; drop link-local addresses from Internet(public) interface/interface-list; accept access to a router from link-local addresses, accept multicast addresses for management purposes, accept your source address-list for router access; drop anything else;

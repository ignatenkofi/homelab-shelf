## Manual configuration 

To configure the DHCP server manually to respond to local requests you have to configure the following: 

An IP pool for addresses to be given out, make sure that your gateway/DHCP server address is not part of the pool. 

```
/ip pool add name=dhcp_pool0 ranges=192.168.88.2-192.168.88.254
```

A network indicating subnets that DHCP-server will lease addresses from, among other information, like a gateway, DNS-server, NTP-server, DHCP options, etc. 

```
/ip dhcp-server network add address=192.168.88.0/24 dns-server=192.168.88.1 gateway=192.168.88.1
```

In our case, the device itself is serving as the gateway, so we'll add the address to the bridge interface: 

```
/ip address add address=192.168.88.1/24 interface=bridge1 network=192.168.88.0
```

And finally, add DHCP Server , here we will add the previously created address pool , and specify on which interface the DHCP server should work on 

```
/ip dhcp-server add address-pool=dhcp_pool0 disabled=no interface=bridge1 name=dhcp1
```

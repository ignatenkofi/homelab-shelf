## Networks 

Lastly, you might notice that the **`network`** menu is missing and probably wondering how to advertise your own networks. Now networks are added to the firewall address-list and referenced in the BGP configuration. Following ROSv6 network configuration: 

```
/routing bgp network add network=192.168.0.0/24 synchronize=yes
/ip route add dst-address=192.168.0.0/24 type=blackhole
```

would translate to v7 as: 

```
/ip/firewall/address-list/
add list=bgp-networks address=192.168.0.0/24
```

```
/ip/route
add dst-address=192.168.0.0/24 blackhole
```

```
/routing/bgp/connection
set peer_name output.network=bgp-networks
```

1078 

There is more configuration to be done when adding just one network but offers simplicity when you have to deal with a large number of networks. v7 even allows specifying for each BGP connection its own set of networks. 

**==> picture [13 x 13] intentionally omitted <==**

In v7 it is not possible to turn off synchronization with IGP routes (the network will be advertised only if the corresponding IGP route is present in the routing table).

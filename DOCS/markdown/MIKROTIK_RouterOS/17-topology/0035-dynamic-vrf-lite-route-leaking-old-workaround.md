## Dynamic Vrf-Lite route leaking (old workaround) 

Before ROS v7.14 there were no mechanism to leak routes from one VRF instance to another within the same router. 

As a workaround, it was possible to create a tunnel between two locally configure loopback addresses and assign each tunnel endpoint to its own VRF. Then it is possible to run either dynamic routing protocols or set up static routes to leak between both VRFs. 

The downside of this approach is that tunnel must be created between each VRF where routes should be leaked (create a full mesh), which significantly complicates configuration even if there are just several VRFs, not to mention more complicated setups. 

For example, to leak routes between 5 VRFs it would require n * ( n – 1) / 2 connections, which will lead to the setup with 20 tunnel endpoints and 20 OSPF instances on one router. 

Example config with two VRFs of this method: 

1043 

```
/interface bridge
add name=dummy_custC
add name=dummy_custB
add name=lo1
add name=lo2
```

```
/ip address
add address=111.255.255.1 interface=lo1 network=111.255.255.1
add address=111.255.255.2 interface=lo2 network=111.255.255.2
add address=172.16.1.0/24 interface=dummy_custC network=172.16.1.0
add address=172.16.2.0/24 interface=dummy_custB network=172.16.2.0
```

```
/interface ipip
add local-address=111.255.255.1 name=ipip-tunnel1 remote-address=111.255.255.2
add local-address=111.255.255.2 name=ipip-tunnel2 remote-address=111.255.255.1
```

```
/ip address
add address=192.168.1.1/24 interface=ipip-tunnel1 network=192.168.1.0
add address=192.168.1.2/24 interface=ipip-tunnel2 network=192.168.1.0
```

```
/ip vrf
add interfaces=ipip-tunnel1,dummy_custC name=custC
add interfaces=ipip-tunnel2,dummy_custB name=custB
```

```
/routing ospf instance
add disabled=no name=i2_custB redistribute=connected,static,copy router-id=192.168.1.1 routing-table=custB
vrf=custB
add disabled=no name=i2_custC redistribute=connected router-id=192.168.1.2 routing-table=custC vrf=custC
/routing ospf area
add disabled=no instance=i2_custB name=custB_bb
add disabled=no instance=i2_custC name=custC_bb
/routing ospf interface-template
add area=custB_bb disabled=no networks=192.168.1.0/24
add area=custC_bb disabled=no networks=192.168.1.0/24
```

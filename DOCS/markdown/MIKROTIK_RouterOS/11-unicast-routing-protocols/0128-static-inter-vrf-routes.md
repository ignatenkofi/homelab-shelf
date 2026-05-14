## Static inter-VRF routes 

In general, it is recommended that all routes between VRF should be exchanged using BGP local import and export functionality. If that is not enough, static routes can be used to achieve this so-called route leaking. 

There are two ways to install a route that has a gateway in a different routing table than the route itself. 

The first way is to explicitly specify the routing table in the gateway field when adding a route. This is only possible when leaking a route and gateway from the "main" routing table to a different routing table (VRF). Example: 

```
# add route to 5.5.5.0/24 in 'vrf1' routing table with gateway in the main routing table
add dst-address=5.5.5.0/24 gateway=10.3.0.1@main routing-table=vrf1
```

The second way is to explicitly specify the interface in the gateway field. The interface specified can belong to a VRF instance. Example: 

```
# add route to 5.5.5.0/24 in the main routing table with gateway at 'ether2' VRF interface
add dst-address=5.5.5.0/24 gateway=10.3.0.1%ether2 routing-table=main
# add route to 5.5.5.0/24 in the main routing table with 'ptp-link-1' VRF interface as gateway
add dst-address=5.5.5.0/24 gateway=ptp-link-1 routing-table=main
```

As can be observed, there are two variations possible - to specify gateway as ip_address%interface or to simply specify an interface. The first should be used for broadcast interfaces in most cases. The second should be used for point-to-point interfaces, and also for broadcast interfaces, if the route is a connected route in some VRF. For example, if you have an address `1.2.3.4/24` on interface ether2 that is put in a VRF, there will be a connected route to `1.2.3.0/24` in that VRF's routing table. It is acceptable to add a static route `1.2.3.0/24` in a different routing table with an interface-only gateway, even though ether2 is a broadcast interface: 

```
add dst-address=1.2.3.0/24 gateway=ether2 routing-table=main
```

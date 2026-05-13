## Ros_Spine 

```
/ip address
add address=203.0.255.138 interface=lo
add address=172.16.1.1/30 interface=ether3
add address=172.16.2.1/30 interface=ether4
add address=172.16.3.1/30 interface=ether5
add address=172.16.4.1/30 interface=ether6
add address=172.16.5.1/30 interface=ether7
```

```
/routing ospf instance
add name=evpn_underlay
/routing ospf area
add disabled=no instance=evpn_underlay name=evpn-underlay-bb
/routing ospf interface-template
add area=evpn-underlay-bb disabled=no networks=172.16.0.0/16
add area=evpn-underlay-bb disabled=no interfaces=lo passive
```

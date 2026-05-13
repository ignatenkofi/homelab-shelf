## Basic configuration example 

In this example, static routing is used to reach remote VTEPs, but dynamic routing protocols like OSPF or BGP could also be used. The upstream interface has a higher MTU to support large packets and VXLAN encapsulation. Below is a network topology overview: 

sfp-sfpplus1 - upstream (underlay) interface sfp-sfpplus3 - bridged port for untagged VLAN 10 sfp-sfpplus4 - bridged port for untagged VLAN 20 vxlan-10010 - overlay port for untagged VLAN 10 vxlan-10020 - overlay port for untagged VLAN 20 

```
/interface bridge
add name=bridge1 vlan-filtering=yes
/interface ethernet
set [ find default-name=sfp-sfpplus1 ] l2mtu=9500 mtu=9500
/interface vxlan
add bridge=bridge1 bridge-pvid=10 local-address=192.168.1.1 name=vxlan-10010 vni=10010
add bridge=bridge1 bridge-pvid=20 local-address=192.168.1.1 name=vxlan-10020 vni=10020
/interface bridge port
add bridge=bridge1 interface=sfp-sfpplus3 pvid=10
add bridge=bridge1 interface=sfp-sfpplus4 pvid=20
/interface vxlan vteps
add interface=vxlan-10010 remote-ip=192.168.1.2
add interface=vxlan-10020 remote-ip=192.168.1.2
/ip address
add address=192.168.1.1 interface=lo network=192.168.1.1
add address=192.168.10.10/24 interface=sfp-sfpplus1 network=192.168.10.0
/ip route
add dst-address=192.168.1.2 gateway=192.168.10.20
/interface ethernet switch
set 0 l3-hw-offloading=yes
```

509

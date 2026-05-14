## PE2 Router (Cisco) 

```
ip vrf cust-one
rd 1.1.1.1:111
route-target export 1.1.1.1:111
route-target import 1.1.1.1:111
exit
interface Loopback0
ip address 10.5.5.3 255.255.255.255
mpls ldp router-id Loopback0 force
mpls label protocol ldp
interface FastEthernet0/0
ip address 10.2.2.3 255.255.255.0
mpls ip
interface FastEthernet1/0
ip vrf forwarding cust-one
ip address 10.3.3.3 255.255.255.0
router bgp 65000
neighbor 10.5.5.2 remote-as 65000
neighbor 10.5.5.2 update-source Loopback0
address-family vpnv4
neighbor 10.5.5.2 activate
neighbor 10.5.5.2 send-community both
exit-address-family
address-family ipv4 vrf cust-one
redistribute connected
exit-address-family
ip route 10.5.5.2 255.255.255.255 10.2.2.2
```

1046

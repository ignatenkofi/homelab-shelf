## Eos_Leaf 

On the Arista router we are setting vlan trunk, untagged traffic will be sent to the host 

```
vlan 10
!
interface Ethernet2
   switchport trunk allowed vlan 10
   switchport mode trunk
!
interface Vlan10
   ip address 192.168.10.128/24
!
interface Vxlan1
   vxlan source-interface Loopback0
   vxlan vlan 10 vni 1010
!
router bgp 65501
   vlan 10
      rd 203.0.255.128:1010
      route-target both 1010:1010
      redistribute learned
```

1027 

Host_1 

```
/ip address
add address=192.168.10.132/24 interface=ether2
```

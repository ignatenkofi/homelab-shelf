## Eos_Leaf 

```
interface Ethernet1
   no switchport
   ip address 172.16.5.2/30
!
interface Loopback0
   ip address 203.0.255.128/32
!
ip routing
!
router ospf 100
   router-id 203.0.255.135
   redistribute connected
   network 172.16.1.0/30 area 0.0.0.0
!
```

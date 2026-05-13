## Port Channel configuration 

Assuming that underly and overly is configured, and is up and running, we will proceed to port channel configuration on Arista switches: 

leaf_2 and leaf_4 config is exactly the same 

```
interface Port-Channel3
   switchport access vlan 10
   switchport trunk allowed vlan 10
   switchport mode trunk
   !
   evpn ethernet-segment
      identifier 0000:0000:0000:0333:3333
      route-target import 00:00:03:33:33:33
   lacp system-id 0000.0333.3333
!
interface Ethernet2
   channel-group 3 mode active
```

ros_host_2 

```
/interface bonding
add mode=802.3ad name=bond1 slaves=ether2,ether3
/interface vlan
add interface=bond1 mtu=1496 name=vlan10 vlan-id=10
/ip address
add address=192.168.10.130/24 interface=vlan10
```

Validate setup 

1032 

Now if we look at evpn routes we should see some new route types. Both Arista switches are advertising Type-1 AD routes and Type-4 Ethernet Segment (ES) routes to discover multihoming VTEPs 

```
[admin@gns3_spine1_ros] /routing/route>  print where afi=evpn dst-address~"(ad|es)"
Flags: A - ACTIVE; b - BGP
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE
   DST-ADDRESS                                                      GATEWAY        AFI   DISTANCE  SCOPE  TA
Ab [203.0.255.127:1]ad:4294967295|00:00:00:00:00:00:03:33:33:33     203.0.255.127  evpn        20     40  30
Ab [203.0.255.127:1]es:00:00:00:00:00:00:03:33:33:33|203.0.255.127  203.0.255.127  evpn        20     40  30
Ab [203.0.255.127:1010]ad:0|00:00:00:00:00:00:03:33:33:33           203.0.255.127  evpn        20     40  30
Ab [203.0.255.134:1]ad:4294967295|00:00:00:00:00:00:03:33:33:33     203.0.255.134  evpn        20     40  30
Ab [203.0.255.134:1]es:00:00:00:00:00:00:03:33:33:33|203.0.255.134  203.0.255.134  evpn        20     40  30
Ab [203.0.255.134:1010]ad:0|00:00:00:00:00:00:03:33:33:33           203.0.255.134  evpn        20     40  30
```

If we check both Eos leafs, we will see that designated forwarder 203.0.255.127 (eos_leaf_4) is selected: 

```
eos_leaf_2#show bgp evpn instance vlan 10
EVPN instance: VLAN 10
  Route distinguisher: 203.0.255.134:1010
  Route target import: Route-Target-AS:1010:1010
  Route target export: Route-Target-AS:1010:1010
  Service interface: VLAN-based
  Local VXLAN IP address: 203.0.255.134
  VXLAN: enabled
  MPLS: disabled
  Local ethernet segment:
    ESI: 0000:0000:0000:0333:3333
      Type: 0 (administratively configured)
      Interface: Port-Channel3
      Mode: all-active
      State: up
      ES-Import RT: 00:00:03:33:33:33
      DF election algorithm: modulus
      Designated forwarder: 203.0.255.127
      Non-Designated forwarder: 203.0.255.134
```

Lets suspend the link from host2 to eos_leaf_4 and see what happens: 

1033 

```
eos_leaf_2#show bgp evpn instance vlan 10
EVPN instance: VLAN 10
  Route distinguisher: 203.0.255.134:1010
  Route target import: Route-Target-AS:1010:1010
  Route target export: Route-Target-AS:1010:1010
  Service interface: VLAN-based
  Local VXLAN IP address: 203.0.255.134
  VXLAN: enabled
  MPLS: disabled
  Local ethernet segment:
    ESI: 0000:0000:0000:0333:3333
      Type: 0 (administratively configured)
      Interface: Port-Channel3
      Mode: all-active
      State: up
      ES-Import RT: 00:00:03:33:33:33
      DF election algorithm: modulus
      Designated forwarder: 203.0.255.134
```

```
[admin@spine1_ros] /routing/route>  print interval=1 where dst-address~"ad|es"
Flags: A - ACTIVE; b - BGP
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE
   DST-ADDRESS                                                      GATEWAY        AFI   DISTANCE  SCOPE  TA
Ab [203.0.255.134:1]ad:4294967295|00:00:00:00:00:00:03:33:33:33     203.0.255.134  evpn        20     40  30
Ab [203.0.255.134:1]es:00:00:00:00:00:00:03:33:33:33|203.0.255.134  203.0.255.134  evpn        20     40  30
Ab [203.0.255.134:1010]ad:0|00:00:00:00:00:00:03:33:33:33           203.0.255.134  evpn        20     40  30
```

```
[admin@host_2] /interface/bonding> /ping 192.168.10.132 interval=500ms
  SEQ HOST                                     SIZE TTL TIME       STATUS
    0 192.168.10.132                             56  64 2ms90us
    1 192.168.10.132                             56  64 2ms172us
    2 192.168.10.132                             56  64 2ms503us
    3 192.168.10.132                                               timeout
    4 192.168.10.132                                               timeout
    5 192.168.10.132                                               timeout
    6 192.168.10.132                             56  64 2ms191us
    7 192.168.10.132                             56  64 2ms31us
```

eos_leaf_2 became forwarder, eos_leaf_4 withdraw  ES and AD routes and traffic switched to other LACP link. 

1034

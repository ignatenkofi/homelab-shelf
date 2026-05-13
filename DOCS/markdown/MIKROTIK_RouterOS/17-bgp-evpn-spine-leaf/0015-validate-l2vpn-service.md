## Validate L2VPN Service 

Lets verify that IMET routes are present on leaf routers and that vteps are discovered 

```
[admin@ros_leaf_3] /routing/route> print where dst-address~"imet"
Flags: A - ACTIVE; b - BGP, e - EVPN
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE, IMMEDIATE-GW
   DST-ADDRESS                               GATEWAY        AFI   DISTANCE  SCOPE  TARGET-SCOPE  IMMEDIATE-
GW
Ab [203.0.255.128:1010]imet:0|203.0.255.128  203.0.255.128  evpn        20     40            30  172.16.3.1%
ether10
 e [203.0.255.133:256]imet:0|203.0.255.133   203.0.255.133  evpn       200     40
10
```

```
[admin@ros_leaf_3] /interface/vxlan/vteps> print
Flags: D - DYNAMIC
Columns: INTERFACE, REMOTE-IP
#   INTERFACE  REMOTE-IP
0 D vxlan1     203.0.255.128
```

On Arista: 

1028 

```
localhost#show bgp evpn route-type imet
BGP routing table information for VRF default
Router identifier 203.0.255.135, local AS number 65501
Route status codes: * - valid, > - active, S - Stale, E - ECMP head, e - ECMP
                    c - Contributing to ECMP, % - Pending BGP convergence
Origin codes: i - IGP, e - EGP, ? - incomplete
AS Path Attributes: Or-ID - Originator ID, C-LST - Cluster List, LL Nexthop - Link Local Nexthop
```

```
          Network                Next Hop              Metric  LocPref Weight  Path
 * >      RD: 203.0.255.128:1010 imet 203.0.255.128
                                 -                     -       -       0       i
 * >      RD: 203.0.255.133:256 imet 203.0.255.133
                                 203.0.255.133         -       100     0       65000 65003 i
```

```
localhost#show interfaces vxlan1
Vxlan1 is up, line protocol is up (connected)
  Hardware is Vxlan
  Source interface is Loopback0 and is active with 203.0.255.128
  Listening on UDP port 4789
  Replication/Flood Mode is headend with Flood List Source: EVPN
  Remote MAC learning via EVPN
  VNI mapping to VLANs
  Static VLAN to VNI mapping is
    [10, 1010]
  Note: All Dynamic VLANs used by VCS are internal VLANs.
        Use 'show vxlan vni' for details.
  Static VRF to VNI mapping is not configured
  Headend replication flood vtep list is:
    10 203.0.255.133
  Shared Router MAC is 0000.0000.0000
```

```
localhost#show vxlan flood vtep vlan 10
          VXLAN Flood VTEP Table
```

```
--------------------------------------------------------------------------------
```

```
VLANS                            Ip Address
-----------------------------   ------------------------------------------------
10                              203.0.255.133
```

At this point we can try to ping host_3 from host_1: 

```
[admin@host_1] /interface> print
...
1 R ether2  ether           1500  0C:50:85:84:00:01
[admin@host_1] /ip/address> /ping 192.168.10.129
  SEQ HOST                                     SIZE TTL TIME
STATUS
    0 192.168.10.129                             56  64 17ms26us
    1 192.168.10.129                             56  64 13ms119us
    2 192.168.10.129                             56  64 17ms192us
```

host-3 

```
[admin@host_1] /interface> print
...
1 R ether2  ether           1500  0C:74:39:88:00:01
```

1029 

Now we should be able to see that EVPN is used to learn remote MAC addresses by looking at MACIP routes. 

If we look at routes on ros_leaf, we can see that router 203.0.255.128 sent the macip route for 0C:74:39:88:00:01 mac address which is the host_1 mac address located behind eos_leaf. 

Eos also sends MAC/IP binding which is used for arp/nd suppression. Unfortunately at the time of writing this article RouterOS does not have this functionality. 

```
[admin@ros_leaf_3] /routing/route> print where dst-address~"macip"
Flags: A - ACTIVE; b - BGP, e - EVPN
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE, IMMEDIATE-GW
   DST-ADDRESS                                                   GATEWAY        AFI   DISTANCE  SCOPE  TARGET-
SCOPE  IMMEDIATE-GW
Ab [203.0.255.128:1010]macip:0|0C:74:39:88:00:01                 203.0.255.128  evpn        20
40            30  172.16.3.1%ether10
 e [203.0.255.133:256]macip:0|0C:50:85:84:00:01                  203.0.255.133  evpn       200
40            10
Ab [203.0.255.128:1010]macip:0|0C:74:39:88:00:01|192.168.10.129  203.0.255.128  evpn        20
40            30  172.16.3.1%ether10
```

Arista allows additionally to see remotely learned mac addresses in "vxlan mac table" and "vlan mac-address table" includes local mac addresses as well: 

1030 

```
localhost#show bgp evpn route-type mac-ip detail
BGP routing table information for VRF default
Router identifier 203.0.255.128, local AS number 65005
BGP routing table entry for mac-ip 0c50.8584.0001, Route Distinguisher: 203.0.255.133:256
 Paths: 1 available
  65000 65003
    203.0.255.133 from 203.0.255.138 (203.0.255.138)
      Origin IGP, metric -, localpref 100, weight 0, tag 0, valid, external, best
      Extended Community: Route-Target-AS:1010:1010 TunnelEncap:tunnelTypeVxlan
      VNI: 0 ESI: 0000:0000:0000:0000:0000
BGP routing table entry for mac-ip 0c74.3988.0001, Route Distinguisher: 203.0.255.128:1010
 Paths: 1 available
  Local
    - from - (0.0.0.0)
      Origin IGP, metric -, localpref -, weight 0, tag 0, valid, local, best
      Extended Community: Route-Target-AS:1010:1010 TunnelEncap:tunnelTypeVxlan
      VNI: 1010 ESI: 0000:0000:0000:0000:0000
BGP routing table entry for mac-ip 0c74.3988.0001 192.168.10.129, Route Distinguisher: 203.0.255.128:1010
 Paths: 1 available
  Local
    - from - (0.0.0.0)
      Origin IGP, metric -, localpref -, weight 0, tag 0, valid, local, best
      Extended Community: Route-Target-AS:1010:1010 TunnelEncap:tunnelTypeVxlan
      VNI: 1010 ESI: 0000:0000:0000:0000:0000
```

```
localhost#show vxlan address-table vlan 10
          Vxlan Mac Address Table
----------------------------------------------------------------------
VLAN  Mac Address     Type      Prt  VTEP             Moves   Last Move
----  -----------     ----      ---  ----             -----   ---------
  10  0c50.8584.0001  EVPN      Vx1  203.0.255.133    1       1:30:49 ago
Total Remote Mac Addresses for this criterion: 1
```

```
localhost#show mac address-table vlan 10
          Mac Address Table
------------------------------------------------------------------
Vlan    Mac Address       Type        Ports      Moves   Last Move
----    -----------       ----        -----      -----   ---------
  10    0c50.8584.0001    DYNAMIC     Vx1        1       1:31:17 ago
  10    0c74.3988.0001    DYNAMIC     Et2        1       1 day, 23:45:18 ago
Total Mac Addresses for this criterion: 2
          Multicast Mac Address Table
------------------------------------------------------------------
Vlan    Mac Address       Type        Ports
----    -----------       ----        -----
Total Mac Addresses for this criterion: 0
```

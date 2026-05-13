## Verify BGP Connectivity 

Eos_Leaf 

```
localhost#show bgp summary
BGP summary information for VRF default
Router identifier 203.0.255.128, local AS number 65005
Neighbor               AS Session State AFI/SAFI                AFI/SAFI State   NLRI Rcd   NLRI Acc
------------- ----------- ------------- ----------------------- -------------- ---------- ----------
203.0.255.138       65000 Established   IPv4 Unicast            Advertised              0          0
203.0.255.138       65000 Established   L2VPN EVPN              Negotiated              6          6
```

Ros_Leaf_3 

1026 

```
[admin@ros_leaf_3] /routing/bgp/session> print
Flags: E - established
```

```
 0 E name="to_spine-1" instance=bgp-instance-1
```

```
     remote.address=203.0.255.138 .as=65000 .id=203.0.255.138 .capabilities=mp,rr,gr,as4 .afi=evpn .messages=7 .
bytes=682 .eor=""
```

```
     local.address=203.0.255.133 .as=65003 .id=203.0.255.133 .cluster-id=203.0.255.133 .capabilities=mp,rr,gr,
as4 .afi=evpn .messages=7
     .bytes=698 .eor=""
     output.procid=20
     input.procid=20 ebgp
```

```
     multihop=yes hold-time=3m keepalive-time=1m uptime=1s620ms last-started=2025-05-29 11:01:38 prefix-count=0
```

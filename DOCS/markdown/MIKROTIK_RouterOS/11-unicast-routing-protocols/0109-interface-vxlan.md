## `/interface vxlan` 

```
add bridge=bridge1 bridge-pvid=40 local-address=203.0.113.1 name=vxlan1 vni=100040 learning=no
```

```
/routing bgp instance
add as=65000 name=evpn-inst
```

```
/routing bgp connection
```

```
add afi=evpn instance=evpn-inst local.address=203.0.113.1 .role=ebgp multihop=yes name=to-leaf-lo remote.
address=203.0.113.2 .as=65001
```

```
/routing bgp evpn
```

```
add instance=evpn-inst name=bgp-evpn-1o vni=100040
```

For simple setups with only one vni, there is no need to set route distinguisher and import/export route targets. 

**==> picture [13 x 13] intentionally omitted <==**

When RTs or RD are not specified, values are derived automatically. Route targets are set to <PE ASN>:<VNI>, route distinguishers <PE address>:<num derived from config id>). 

EVPN configuration is directly mapped to VXLAN configurations with matching VNIs

## PE1 Router 

1045 

```
/interface bridge add name=lobridge
/ip address add address=10.1.1.2/24 interface=ether1
/ip address add address=10.2.2.2/24 interface=ether2
/ip address add address=10.5.5.2/32 interface=lobridge
/ip vrf add name=cust-one interfaces=ether1
/mpls ldp add enabled=yes transport-address=10.5.5.2 lsr-id=10.5.5.2
/mpls ldp interface add interface=ether2
/routing bgp template set default as=65000
/routing bgp vpn
add vrf=cust-one \
  route-distinguisher=1.1.1.1:111 \
  import.route-targets=1.1.1.1:111 \
  import.router-id=cust-one \
  export.redistribute=connected \
  export.route-targets=1.1.1.1:111 \
  label-allocation-policy=per-vrf
/routing bgp connection
add template=default remote.address=10.5.5.3 address-families=vpnv4 local.address=10.5.5.2
```

```
# add route to the remote BGP peer's loopback address
/ip route add dst-address=10.5.5.3/32 gateway=10.2.2.3
```

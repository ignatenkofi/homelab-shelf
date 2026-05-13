## PE2 Mikrotik config 

1050 

```
/interface bridge add name=lobridge
/ip address
add address=10.2.2.3/24 interface=ether1
add address=10.3.3.3/24 interface=ether2
add address=10.4.4.3/24 interface=ether3
add address=10.5.5.3/32 interface=lobridge
/ip vrf
add name=cust-one interfaces=ether2
add name=cust-two interfaces=ether3
/mpls ldp add enabled=yes transport-address=10.5.5.3
/mpls ldp interface add interface=ether1
```

```
/routing bgp template set default as=65000
/routing bgp vpn
add vrf=cust-one \
  export.redistribute=connected \
  route-distinguisher=1.1.1.1:111 \
  import.route-targets=1.1.1.1:111,2.2.2.2:222 \
  export.route-targets=1.1.1.1:111 \
add vrf=cust-two \
  export.redistribute=connected \
  route-distinguisher=2.2.2.2:222 \
  import.route-targets=1.1.1.1:111,2.2.2.2:222 \
  export.route-targets=2.2.2.2:222 \
```

```
/routing bgp connection
add template=default remote.address=10.5.5.2 address-families=vpnv4 local.address=10.5.5.3
```

```
# add route to the remote BGP peer's loopback address
/ip route add dst-address=10.5.5.2/32 gateway=10.2.2.2
```

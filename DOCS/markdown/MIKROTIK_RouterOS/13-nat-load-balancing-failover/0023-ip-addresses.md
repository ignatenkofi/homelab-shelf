## IP Addresses 

```
/ip address
```

```
add address=10.10.4.100/24 interface=ether_ISP1 network=10.10.4.0
add address=10.10.5.100/24 interface=ether_ISP2 network=10.10.5.0
add address=192.168.100.1/24 interface=ether_LAN network=192.168.100.0
```

The router has two upstream (ISP) interfaces with the addresses of 10.10.4.100/24 and 10.10.5.100/24. The LAN interface has IP address of 192.168.0.1 /24. 

We are adding two new Routing tables, which will be used later: 

```
/routing table
add disabled=no fib name=ISP1_table
add disabled=no fib name=ISP2_table
```

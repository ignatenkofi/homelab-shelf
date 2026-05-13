## On R1 it will look like this: 

```
/mpls ldp
add afi=ip lsr-id=111.111.111.1 transport-addresses=111.111.111.1
/mpls ldp interface
add interface=ether2
```

**==> picture [13 x 13] intentionally omitted <==**

Note that the transport address gets set to 111.111.111.1. This makes the router originate LDP session connections with this address and also advertise this address as a transport address to LDP neighbors. 

Other routers are set up similarly. 

R2: 

```
/mpls ldp
add afi=ip lsr-id=111.111.111.2 transport-addresses=111.111.111.2
/mpls ldp interface
add interface=ether2
add interface=ether3
```

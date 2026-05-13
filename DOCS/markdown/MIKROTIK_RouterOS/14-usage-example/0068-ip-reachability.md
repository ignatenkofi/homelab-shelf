## Ip Reachability 

Not going deep into routing setup here is the quit export of the IP and OSPF configurations: 

843 

```
#R1
/interface bridge
add name=loopback
/ip address
add address=111.11.0.1/24 interface=ether2
add address=111.111.111.1 interface=loopback
```

```
/routing ospf instance
add name=default_ip4 router-id=111.111.111.1
/routing ospf area
add instance=default_ip4 name=backbone_ip4
/routing ospf interface-template
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.111.111.1
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.11.0.0/24
```

```
#R2
/interface bridge
add name=loopback
/ip address
add address=111.11.0.2/24 interface=ether2
add address=111.12.0.1/24 interface=ether3
add address=111.111.111.2 interface=loopback
```

```
/routing ospf instance
add name=default_ip4 router-id=111.111.111.2
/routing ospf area
add instance=default_ip4 name=backbone_ip4
/routing ospf interface-template
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.111.111.2
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.11.0.0/24
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.12.0.0/24
```

```
#R3
/interface bridge
add name=loopback
/ip address
add address=111.12.0.2/24 interface=ether2
add address=111.13.0.1/24 interface=ether3
add address=111.111.111.3 interface=loopback
```

```
/routing ospf instance
add name=default_ip4 router-id=111.111.111.3
/routing ospf area
add instance=default_ip4 name=backbone_ip4
/routing ospf interface-template
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.111.111.3
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.12.0.0/24
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.13.0.0/24
```

```
#R4
/interface bridge
add name=loopback
/ip address
add address=111.13.0.2/24 interface=ether2
add address=111.111.111.4 interface=loopback
```

```
/routing ospf instance
add name=default_ip4 router-id=111.111.111.4
/routing ospf area
add instance=default_ip4 name=backbone_ip4
/routing ospf interface-template
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.111.111.4
add area=backbone_ip4 dead-interval=10s hello-interval=1s networks=111.13.0.0/24
```

844

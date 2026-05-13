## Basic Configuration Example 

To start OSPF v2 and v3 instances, the first thing to do is to add the instance and the backbone area: 

```
/routing ospf instance
```

```
add name=v2inst version=2 router-id=1.2.3.4
add name=v3inst version=3 router-id=1.2.3.4
/routing ospf area
add name=backbone_v2 area-id=0.0.0.0 instance=v2inst
add name=backbone_v3 area-id=0.0.0.0 instance=v3inst
```

At this point, we can add a template. The template is used to match interfaces on which OSPF should be running, it can be done either by specifying the network or interface directly. 

```
/routing ospf interface-template
add networks=192.168.0.0/24 area=backbone_v2
add networks=2001:db8::/64 area=backbone_v3
add interfaces=ether1 area=backbone_v3
```

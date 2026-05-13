## Stub Area 

The main purpose of stub areas is to keep such areas from carrying external routes. Routing from these areas to the outside world is based on a default route. A stub area reduces the database size inside an area and reduces the memory requirements of routers in the area. 

**==> picture [505 x 263] intentionally omitted <==**

The stub area has a few restrictions, ASBR routers cannot be internal to the area, stub area cannot be used as a transit area for virtual links. The restrictions are made because the stub area is mainly configured not to carry external routes. 

This area supports 1, 2, and 3 LSAs. 

Let's consider the example above. Area1 is configured as a stub area meaning that routers R2 and R3 will not receive any routing information from the backbone area except the default route. 

R1: 

1004 

```
/routing ospf instance
```

```
add name=v2inst version=2 router-id=1.0.0.1
/routing ospf area
add name=backbone_v2 area-id=0.0.0.0 instance=v2inst
add name=area1 area-id=1.1.1.1 type=stub instance=v2inst
```

```
/routing ospf interface-template
add networks=10.0.0.0/24 area=backbone_v2
add networks=10.0.1.0/24 area=area1
add networks=10.0.3.0/24 area=area1
```

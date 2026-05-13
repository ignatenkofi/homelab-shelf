## `/routing ospf area` 

```
add name=backbone_v2 area-id=0.0.0.0 instance=v2inst
add name=stub_area area-id=1.1.1.1 instance=v2inst type=stub
add name=another_area area-id=2.2.2.2 instance=v2inst type=default
```

OSPF can have 5 types of areas. Each area type defines what type of LSAs the area supports: 

- standard/default - OSPF packets can normally be transmitted in this area, it supports types 1,2,3,4 and 5 LSAs 

- backbone - as already mentioned this is the main area where any other area connects. It is basically the same as the standard area but identified with ID 0.0.0.0 

- stub - this area does not accept any external routes 

- totally stubby - a variation of the stub area 

- not-so-stubby (NSSA) - a variation of the stub area

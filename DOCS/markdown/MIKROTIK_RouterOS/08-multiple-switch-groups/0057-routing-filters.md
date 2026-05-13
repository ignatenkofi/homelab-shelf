## Routing Filters 

For dynamic routing protocols like OSFP and BGP, it is possible to suppress HW offloading using routing filters. For example, to suppress HW offloading on all OSFP instance routes, use " **`suppress-hw-offload yes`** " property: 

```
/routing/ospf/instance
set [find name=instance1] in-filter-chain=ospf-input
/routing/filter/rule
add chain="ospf-input" rule="set suppress-hw-offload yes; accept"
```

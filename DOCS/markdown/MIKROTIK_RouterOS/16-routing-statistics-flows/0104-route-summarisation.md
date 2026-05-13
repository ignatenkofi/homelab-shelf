## Route Summarisation 

Route summarization is a consolidation of multiple routes into one single advertisement. It is normally done at the area boundaries (Area Border Routers). 

It is better to summarise in the direction of the backbone. That way the backbone receives all the aggregated routes and injects them into other areas already summarized. There are two types of summarization: inter-area and external route summarization. 

Inter-area route summarization works on area boundaries (ABRs), it does not apply to external routes injected into OSPF via redistribution. By default, ABR creates a summary LSA for each route in a specific area and advertises it in adjacent areas. 

Using ranges allows for creating only one summary LSA for multiple routes and sending only a single advertisement into adjacent areas, or suppressing advertisements altogether. 

If a range is configured with the ' `advertise` ' parameter, a single summary LSA is advertised for each range if there are any routes under the range in the specific area. Otherwise (when ' `advertise` ' parameter disabled) no summary LSAs are created and advertised outside area boundaries at all. 

Inter-area route summarization can be configured from the OSPF area range menu. 

Let's consider that we have two areas backbone and area1, area1 has several /24 routes from the 10.0.0.0/16 range and there is no need to flood the backbone area with each /24 subnet if it can be summarized. On the router connecting area1 with the backbone we can set up the area range: 

```
/routing ospf area range
```

```
add prefix=10.0.0.0/16 area=area1 advertise=yes cost=10
```

**==> picture [13 x 13] intentionally omitted <==**

For an active range (i.e. one that has at least one OSPF route from the specified area falling under it), a route with the type 'blackhole' is created and installed in the routing table. 

1007 

External route summarization can be achieved using routing filters.  Let's consider the same example as above except that area1 has redistributed /24 routes from other protocols. To send a single summarised LSA, a blackhole route must be added and an appropriate routing filter to accept only summarised route: 

```
/ip route add dst-address=10.0.0.0/16 blackhole
/routing ospf instance
set v2inst out-filter-chain=ospf_out
/routing filter rule
add chain=ospf_out rule="if (dst == 10.0.0.0/16) {accept} else {reject}"
```

## External Routing Information and Default Route 

On the edge of an OSPF routing domain, you can find routers called AS boundary routers (ASBRs) that run one of the other routing protocols. The job of those routers is to import routing information learned from other routing protocols into the OSPF routing domain. External routes can be imported at two separate levels depending on the metric type. 

1006 

type1 - OSPF metric is the sum of the internal OSPF cost and the external route cost type2 - OSPF metric is equal only to the external route cost. 

**==> picture [13 x 13] intentionally omitted <==**

Type 1 external paths are always preferred over type 2 external paths. When all paths are type 2 external paths, the paths with the smallest advertised type 2 metric are always preferred. (RFC2328) 

External routes can be imported via the instance `redistribute` parameter. The example below will pick and redistribute all static and RIP routes: 

```
/routing ospf instance
```

```
add name=v2inst version=2 router-id=1.2.3.4 redistribute=static,rip
```

Redistribution of default route is a special case where the `originate-default` the parameter should be used: 

```
/routing ospf instance
set v2inst originate-default=if-installed
```

Since redistribution is controlled by " `originate-default` " and " `redistribute` " parameter, it introduces some corner-cases for default route filtering. 

- if `redistribute` is enabled, then pick all routes matching redistribute parameters If `originate-default=never` , a default route will be rejected 

- run selected routes (or all routes if redistribute parameter is not set) through `out-select-chain` (if configured) run selected routes through `out-filter-chain` (if configured) if `originate-default` is set to `always` or `if-installed` : OSPF creates a fake default route without attributes; runs this route through `out-filter-chain` where attributes can be applied, but action is ignored (always accept); 

For a complete list of redistribution values, see the reference manual.

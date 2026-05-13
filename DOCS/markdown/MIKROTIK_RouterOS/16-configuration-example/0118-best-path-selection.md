## Best-Path Selection 

BGP routers can receive multiple copies of the global routing table from multiple providers. 

There should be some way to compare those multiple BGP routing tables and select the best route to the destination, the solution is the BGP Best Path Selection Algorithm. 

The route is evaluated by the algorithm only if it is valid. In general, the route is considered valid if: 

NEXT_HOP of the route is valid and reachable 

- AS_PATH received from external peers does not contain the local AS the route is not rejected by routing filters 

For more information read nexthop selection and validation. 

The best path algorithm also compares routes received only by a single BGP instance . Routes installed by different BGP instances are compared by the general algorithm, i.e. route distances are compared and the route with a lower distance is preferred. 

If all the criteria are met, then the following actions take place: 

1.  The first path received is automatically considered the 'best path'. Any further received paths are compared to the first received to determine if the new path is better. 

2.  Prefer the path with the highest WEIGHT . This parameter is not a part of the BGP standard, it is invented to quickly locally select the best route. A parameter is local to the router (assigned with routing filters in the BGP input) and cannot be advertised. A route without assigned WEIGHT has a default value of 0. 

3.  Prefer the path with the highest LOCAL_PREF . This attribute is used only within an AS. A path without the LOCAL_PREF attribute has a value of 100 by default. 

4.  Prefer the path with the shortest AS_PATH . (skipped if `input.ignore-as-path-len` set to yes ). Each AS_SET counts as 1, regardless of the set size. The AS_CONFED_SEQUENCE and AS_CONFED_SET are not included in the AS_PATH length. 

5. ~~Prefer the path that was locally originated via aggregate or BGP network~~ 

6.  Prefer the path with the lowest ORIGIN type. 

Interior Gateway Protocol (IGP) is lower than Exterior Gateway Protocol (EGP), and EGP is lower than INCOMPLETE 

in other words IGP < EGP < INCOMPLETE 

7.  Prefer the path with the lowest multi-exit discriminator (MED). 

The router compares the MED attribute only for paths that have the same neighboring (leftmost) AS unless `input.always-compare-med` is enabled. 

- Paths without explicit MED value are treated with MED of 0. 

- 8.  Prefer eBGP over iBGP paths 9.  Prefer lowest IGP metric . 

10.  Prefer the route that comes from the BGP router with the lowest router ID . If a route carries the ORIGINATOR_ID attribute, then the ORIGINATOR 

   - _ID is used instead of the router ID. 

11.  Prefer the route with the shortest route reflection cluster list . Routes without a cluster list are considered to have a cluster list of length 0. 

12.  Prefer the path that comes from the lowest neighbor address 

1013

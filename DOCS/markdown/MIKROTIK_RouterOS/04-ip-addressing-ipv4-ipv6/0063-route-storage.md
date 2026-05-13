## Route Storage 

Routing information is stored to take as little memory as possible in a common case. These optimizations have non-obvious worst cases and impact on performance. 

All routes and gateways are kept in a single hierarchy by the prefix/address. 

```
   Dst [4]/0 1/0+4                             18  <-- number of prefixes
```

```
        ^  ^ ^ ^ ^
```

```
        |  | | | |
```

```
        |  | | | \- bytes taken by Route distinguisher or Interface Id
```

- `|  | | \--- vrf/routing table` 

- `|  | \----- AFI` 

- `|  \------- netmask length of prefix` 

```
        \---------- bytes taken by prefix value
```

```
        [subject to change without notice]
```

Each of these 'Dst' corresponds to a unique 'dst-address' of route or address of the gateway. Each 'Dst' requires one or more 'T2Node' objects as well. 

All routes with the same 'dst-address' are kept in Dst in a list sorted by route preference. 

Note: WORST CASE: having a lot of routes with the same 'dst-address' is really slow! even if they are inactive! because updating a sorted list with tens of thousands of elements is slow! 

Route order changes only when route attributes change. If the route becomes active/inactive, the order does not change. 

Each Route has three copies of route attributes: 

private -- what is received from the peer, before passing in-filters. updated -- what is the result of applying in-filters. 

current -- what are the attributes currently used by the route. 

184 

Periodically (when needed), update attributes are calculated from private attri butes. This happens when route update is received, or when in-filter is updated. 

When the routing table is recalculated, current attribu tes are set to the value from updated attributes. 

This means, that usually if there is no in-filter that changes route attributes, pri vate , updated, and current share the same value. 

Route attributes are kept in several groups: 

L1 Data - all flags, list of extra properties, aspath; L2 Data - nexthops, RIP, OSPF, BGP metrics, route tags, originators, etc. 

L3 Data - distance, scope, kernel type, MPLS stuff extra properties - communities, originator, aggregator-id, cluster-list, unknown 

**==> picture [413 x 417] intentionally omitted <==**

Having for example many different combinations of distance and scope route attributes will use more memory! 

Matching communities or as-path using regexp will cache the result, to speed up filtering. Each as-path or community value has a cache for all regexp, which is filled on-demand with match results. 

Note: WORST CASE: changing attributes in 'in-filter' will make the route program use more memory! Because 'private' and 'updated' attributes will be different! Having a lot of different regexps will make matching slow and use a lot of memory! Because each value will have a cache with thousands of entries! 

Detailed info about used memory by routing protocols can be seen in `/routing stats memory` menu

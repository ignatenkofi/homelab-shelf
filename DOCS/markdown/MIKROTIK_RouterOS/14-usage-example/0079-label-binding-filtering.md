## Label binding filtering 

849 

During the implementation of the given example setup, it has become clear that not all label bindings are necessary. For example, there is no need to exchange IP route label bindings between R1 and R3 or R2 and R4, as there is no chance they will ever be used. Also, if the given network core is providing connectivity only for mentioned customer ethernet segments, there is no real use to distribute labels for networks that connect routers between themselves, the only routes that matter are /32 routes to endpoints or attached customer networks. 

Label binding filtering can be used to distribute only specified sets of labels to reduce resource usage and network load. 

There are 2 types of label binding filters: 

which label bindings should be advertised to LDP neighbors, configured in the `/mpls ldp advertise-filter` menu which label bindings should be accepted from LDP neighbors, configured in `/mpls ldp accept-filter` menu 

Filters are organized in the ordered list, specifying prefixes that must include the prefix that is tested against the filter and neighbor (or wildcard). 

In the given example setup all routers can be configured so that they advertise labels only for routes that allow reaching the endpoints of tunnels. For this 2 advertise filters need to be configured on all routers: 

```
/mpls ldp advertise-filter add prefix=111.111.111.0/24 advertise=yes
/mpls ldp advertise-filter add prefix=0.0.0.0/0 advertise=no
```

This filter causes routers to advertise only bindings for routes that are included by the 111.111.111.0/24 prefix which covers loopbacks (111.111.111.1/32, 111.111.111.2/32, etc). The second rule is necessary because the default filter results when no rule matches are to allow the action in question. 

In the given setup there is no need to set up accept filter because by convention introduced by 2 abovementioned rules no LDP router will distribute unnecessary bindings. 

Note that filter changes do not affect existing mappings, so to take the filter into effect, connections between neighbors need to be reset. either by removing neighbors from the LDP neighbor table or by restarting the LDP instance. 

So on R2, for example, we get: 

```
[admin@R2] /mpls/ldp/remote-mapping> print
Flags: I - INACTIVE; D - DYNAMIC
Columns: VRF, DST-ADDRESS, NEXTHOP, LABEL, PEER
#    VRF   DST-ADDRESS    NEXTHOP     LABEL      PEER
0 ID main  111.111.111.2              17         111.111.111.3:0
1 ID main  111.111.111.1              16         111.111.111.3:0
2  D main  111.111.111.3  111.12.0.2  impl-null  111.111.111.3:0
3  D main  111.111.111.4  111.12.0.2  18         111.111.111.3:0
4 ID main  111.111.111.2              16         111.111.111.1:0
5  D main  111.111.111.1  111.11.0.1  impl-null  111.111.111.1:0
6 ID main  111.111.111.3              17         111.111.111.1:0
7 ID main  111.111.111.4              18         111.111.111.1:0
```

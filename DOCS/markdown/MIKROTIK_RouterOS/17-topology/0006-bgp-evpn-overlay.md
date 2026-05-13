## BGP EVPN Overlay 

For BGP overly we will be using multihop eBGP that uses loopback addresses. 

1025 

To simplify configuration we will utilize BGP template to set common parameters and set connection to listen on all loopback address range. This is great for scalability, if we will want to add more leaf routers we won't need to configure anything on the spine routers. 

Also it is recommended to set nexthop-choice to propagate especially if there is more than one spine. In case if iBGP is used as overlay then spines should be route reflectors and nexthop propagation is happening by default.

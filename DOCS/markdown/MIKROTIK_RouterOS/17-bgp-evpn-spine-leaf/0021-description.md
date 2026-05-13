## Description 

RouterOS allows to create multiple Virtual Routing and Forwarding instances on a single router. This is useful for BGP-based MPLS VPNs. Unlike BGP VPLS, which is OSI Layer 2 technology, BGP VRF VPNs work in Layer 3 and as such exchange IP prefixes between routers. VRFs solve the problem of overlapping IP prefixes and provide the required privacy (via separated routing for different VPNs). 

It is possible to set up vrf-lite setups or use multi-protocol BGP with VPNv4 address family to distribute routes from VRF routing tables - not only to other routers, but also to different routing tables in the router itself.

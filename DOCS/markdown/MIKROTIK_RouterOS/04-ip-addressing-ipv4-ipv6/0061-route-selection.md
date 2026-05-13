## Route Selection 

There can be multiple routes with the same destination received from various routing protocols and from static configurations but only one (best) destination can be used for packet forwarding. To determine the best path, RIB runs a Route Selection algorithm that picks the best route from all candidate routes per destination. 

Only routes that meet the following criteria can participate in the route selection process: 

Route is not disabled. 

If the type of route is unicast it must have at least one reachable next-hop. ( if a gateway is from a connected network and there is a connected route active, the gateway is considered as reachable) Route should not be synthetic. 

The candidate route with the lowest distance becomes an active route. If there is more than one candidate route with the same distance, the selection of the active route is arbitrary.

## Routing Tables 

By default, all routes are added to the "main" routing table as it was before. From a configuration point of view, the biggest differences are routing table limit increase, routing table monitoring differences, and how routes are added to specific routing tables (see next example) 

v7 introduces a new menu /routing route, which shows all address family routes as well as all filtered routes with all possible route attributes. `/ip route` a nd `/ipv6 route` menus are used to add static routes and for simplicity show only basic route attributes. 

For more in-depth information on routing see this article (IP Routing). 

Another new change is that most common route print requests are processed by the routing process which significantly improves the speed compared to v6.

## `/routing/rip/instance` 

**==> picture [506 x 271] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name name of the instance<br>vrf  ( Default: main ) which VRF to use<br>afi  (ipv4 | ipv6; Default: ) specifies which afi to use.<br>in-filter-chain  (Default: ) input filter chain<br>out-filter-chain  (Default: ) output filter chain<br>out-filter-select  (Default: ) output filter select rule chain<br>redistribute  (bgp, bgp-mpls-vpn, connected, dhcp, fantasy, modem, ospf, rip, static, vpn;  which routes to redistribute<br>Default: )<br>originate-default  ( Default:) whether to originate default route<br>routing-table  ( Default: main) in which routing table the routes will be added<br>route-timeout  (Default: ) route timeout<br>route-gc-timeout   (Default: )<br>update-interval  (time; Default: ) specifies time interval after which the route is considered<br>invalid<br>**----- End of picture text -----**<br>

Note: The maximum metric of RIP route is 15. Metric higher than 15 is considered 'infinity' and routes with such metric are considered unreachable. Thus RIP cannot be used on networks with more than 15 hops between any two routers, and using redistribute metrics larger that 1 further reduces this maximum hop count.

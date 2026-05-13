## Proactive mode 

1497 

**==> picture [390 x 241] intentionally omitted <==**

The root announces itself by flooding RANN 

**==> picture [390 x 241] intentionally omitted <==**

**==> picture [120 x 8] intentionally omitted <==**

**----- Start of picture text -----**<br>
Internal nodes respond with PREGs<br>**----- End of picture text -----**<br>


In proactive mode, there are some routers configured as portals. In general, being a portal means that the router has interfaces to some other network, i.e. it is an entry/exit point to the mesh network. 

The portals will announce their presence by flooding the Root Announcement (RANN) message in the network. Internal nodes will reply with a Path Registration (PREG) message. The result of this process will be routing trees with roots in the portal. 

Routes to portals will serve as a kind of default route. If an internal router does not know the path to a particular destination, it will forward all data to its closest portal. The portal will then discover the path on behalf of the router if needed. The data afterward will flow through the portal. This may lead to suboptimal routing unless the data is addressed to the portal itself or some external network the portals have interfaces to. 

A proactive mode is best suited when most of the traffic goes between internal mesh nodes and a few portal nodes.

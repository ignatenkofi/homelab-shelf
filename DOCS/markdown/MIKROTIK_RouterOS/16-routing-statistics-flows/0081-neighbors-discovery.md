## Neighbors Discovery 

OSPF discovers potential neighbors by periodically sending Hello packets out of configured interfaces. By default Hello packets are sent out at 10-second intervals which can be changed by setting hello-interval in OSPF interface settings. The router learns the existence of a neighboring router when it receives the neighbor's Hello in return with matching parameters. 

The transmission and reception of Hello packets also allow a router to detect the failure of the neighbor. If Hello packets are not received within deadinterval (which by default is 40 seconds) router starts to route packets around the failure. "Hello" protocol ensures that the neighboring routers agree on the Hello interval and Dead interval parameters, preventing situations when not in time received Hello packets mistakenly bring the link down. 

|||
|---|---|
|Field|Description|
|network mask|The IP mask of the originating router's interface IP address.|
|hello interval|the period between Hello packets (default 10s)|
|options|OSPF options for neighbor information|
|router priority|an 8-bit value used to aid in the election of the DR and BDR. (Not set in p2p links)|
|router dead interval|time interval has to be received before considering the neighbor is down. ( By default four times bigger than the Hello interval)|
|DR|the router-id of the current DR|
|BDR|the router-id of the current BDR|
|Neighbor router IDs|a list of router ids for all the originating router's neighbors|



On each type of network segment Hello protocol works a little differently. It is clear that on point-to-point segments only one neighbor is possible and no additional actions are required. However, if more than one neighbor can be on the segment additional actions are taken to make OSPF functionality even more efficient. 

Two routers do not become neighbors unless the following conditions are met. 

Two-way communication between routers is possible. Determined by flooding Hello packets. The interface should belong to the same area; 

The interface should belong to the same subnet and have the same network mask unless it has network-type configured as point-to-point ; Routers should have the same authentication options, and have to exchange the same password (if any); Hello and Dead intervals should be the same in Hello packets; 

External routing and NSSA flags should be the same in Hello packets. 

**==> picture [13 x 13] intentionally omitted <==**

Network mask, Priority, DR, and BDR fields are used only when the neighbors are connected by a broadcast or NBMA network segment.

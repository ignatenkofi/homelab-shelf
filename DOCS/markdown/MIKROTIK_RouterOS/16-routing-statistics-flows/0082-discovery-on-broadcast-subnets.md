## Discovery on Broadcast Subnets 

998 

The attached node to the broadcast subnet can send a single packet and that packet is received by all other attached nodes. This is very useful for autoconfiguration and information replication. Another useful capability in broadcast subnets is multicast. This capability allows sending a single packet which will be received by nodes configured to receive multicast packets. OSPF is using this capability to find OSPF neighbors and detect bidirectional connectivity. 

Each OSPF router joins the IP multicast group AllSPFRouters (224.0.0.5), then the router periodically multicasts its Hello packets to the IP address 224.0.0.5. All other routers that joined the same group will receive a multicasted Hello packet. In that way, OSPF routers maintain relationships with all other OSPF routers by sending a single packet instead of sending a separate packet to each neighbor on the segment. 

This approach has several advantages: 

Automatic neighbor discovery by multicasting or broadcasting Hello packets. Less bandwidth usage compared to other subnet types. On the broadcast segment, there are n*(n-1)/2 neighbor relations, but those relations are maintained by sending only n Hellos. If the broadcast has the multicast capability, then OSPF operates without disturbing non-OSPF nodes on the broadcast segment. If the multicast capability is not supported all routers will receive broadcasted Hello packets even if the node is not an OSPF router.

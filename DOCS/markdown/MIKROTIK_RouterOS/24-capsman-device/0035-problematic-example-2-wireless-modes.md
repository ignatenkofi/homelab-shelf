## Problematic example 2: wireless modes 

Consider this (invalid) setup example: 

1501 

**==> picture [505 x 217] intentionally omitted <==**

Routers A and B are inside the mesh, router C: outside. For routers A and B all interfaces are added as mesh ports. 

It is not possible to bridge wlan1 and wlan2 on router B now. The reason for this is pretty obvious if you understand how WDS works. For WDS communications four address frames are used. This is because for wireless multihop forwarding you need to know both the addresses of the intermediate hops, as well as the original sender and final receiver. In contrast, non-WDS 802.11 communication includes only three MAC addresses in a frame. That's why it's not possible to do multi-hop forwarding in station mode. 

Troubleshooting : depends on what you want to achieve: 

1.  If you want router C to act as a repeater either for wireless or Ethernet traffic, configure the WDS link between router B and router C, and run mesh routing protocol on all nodes. 

2.  In other cases configure wlan2 on router B in AP mode and WLAN on router C in station mode. 

1502

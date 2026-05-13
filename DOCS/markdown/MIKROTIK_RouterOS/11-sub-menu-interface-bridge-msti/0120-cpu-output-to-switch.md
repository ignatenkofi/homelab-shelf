## CPU Output to Switch 

This process takes place when a packet exits the RouterOS software processing and is received on the switch-cpu port. Again, there are two paths the packet can take. One where hardware offloading and switching are not even used (e.g. a standalone interface for routing or a bridged interface but with deliberately disabled HW offloading), so the packet is simply sent out through the physical out-interface. Another path is taken when hardware offloading is active on the out-interface. This will cause the packet to pass through the switching decision. Just like any other switch port, the switch will learn the source MAC addresses from packets that are received on the switch-cpu port. This does come in handy when a bridge contains HW and non-HW offloaded interfaces, so the switch can learn which frames should be forwarded to the CPU. See the packet walkthrough when an out-interface is hardware offloaded: 

1.  A packet that exits the RouterOS software processing is received on the switch-cpu port; 

2.  The switch checks whether the out-interface is a hardware offloaded interface; 

3.  Run a packet through the switch host table to make a forwarding decision. If the switch finds a match for the destination MAC 

684 

address, the packet is sent out through the physical interface. A packet that ends up being flooded (e.g. broadcast, multicast, unknown unicast traffic) gets multiplied and sent out to every hardware offloaded switch port. 

**==> picture [505 x 327] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

A software bridge that sends a flooded packet through HW offloaded interfaces, will only send a single packet copy per HW offloaded switch group rather than per HW offloaded interface. The actual flooding will be done by the switch chip, this prevents the formation of duplicate packets.

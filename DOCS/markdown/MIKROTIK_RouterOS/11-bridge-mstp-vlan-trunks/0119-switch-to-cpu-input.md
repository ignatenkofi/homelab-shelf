## Switch to CPU Input 

This process takes place when a packet is received on a physical interface and it is destined to switch-cpu port for further software processing. There are two paths to the switch-cpu. One where hardware offloading and switching is not even used (e.g. a standalone interface for routing or a bridged interface but with deliberately disabled HW offloading), so the packet is simply passed further for software processing. Another path is taken when hardware offloading is active on the in-interface. This will cause the packet to pass through the switching decision and there are various reasons why the switch might forward the packet to the switch-cpu port: 

- a packet's destination MAC address match with a local MAC address, e.g. when a packet is destined to a local bridge interface; 

- a packet might get flooded to all switch ports including the switch-cpu port, e.g. when broadcast, multicast, or unknown unicast traffic is received; 

683 

- a switch might have learned that some hosts can only be reached through the CPU (switch-cpu port learning is discussed in the next section), e. g. when a bridge contains HW and non-HW offloaded interfaces, such as wireless, EoIP, and even Ethernet interfaces; a packet is intentionally copied to the switch-cpu, e.g. for a packet inspection; 

a packet is triggered by the switch configuration and should be processed in software, e.g. a DHCP or IGMP snooping. 

See the packet walkthrough when an in-interface is hardware offloaded: 

1.  The switch checks whether the in-interface is a hardware offloaded interface; 

2.  Run a packet through the switch host table to make a forwarding decision. In case any of the above-mentioned points are true, the packet gets forwarded to the switch-cpu port. 

3.  The packet exits through the switch-cpu port and it will be further processed by the RouterOS packet flow. 

**==> picture [505 x 326] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

- Any received packet that was flooded by the switch chip will not get flooded again by the software bridge to the same HW offloaded switch group. This prevents the formation of duplicate packets.

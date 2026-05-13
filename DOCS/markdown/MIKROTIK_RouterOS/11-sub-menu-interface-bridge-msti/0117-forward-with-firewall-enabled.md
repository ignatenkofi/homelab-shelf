## Forward With Firewall Enabled 

In certain network configurations, you might need to enable additional processing on routing chains for bridged traffic, for example, to use simple queues or an IP firewall. This can be done when the use-ip-firewall is enabled under the bridge settings. Note that additional processing will consume more CPU resources to handle these packets. All the steps were already discussed in previous points, below is a recap: 

1.  A packet goes through the bridge NAT dst-nat chain; 

2.  With the use-ip-firewall option enabled, the packet will be further processed in the prerouting chain; 

3.  A packet enters prerouting processing; 4.  Run packet through the bridge host table to make forwarding decision; 5.  A packet goes through the bridge filter forward chain; 

679 

6.  With the use-ip-firewall option enabled, the packet will be further processed in the routing forward chain; 

7.  A packet enters routing forward processing; 8.  A packet goes through the bridge NAT src-nat chain; 9.  With the use-ip-firewall option enabled, the packet will be further processed in the postrouting chain; 

10.  A packet enters postrouting processing; 

680 

**==> picture [505 x 423] intentionally omitted <==**

**==> picture [505 x 231] intentionally omitted <==**

Flow of Hardware Offloaded Packet 

681 

On the previous topic, we solely discussed a software bridging that requires the main CPU processing to forward packets through the correct bridge port. Most of the MikroTik devices are equipped with dedicated switching hardware, the so-called switch chip or switch ASIC. This allows us to offload some of the bridging functions, like packet forwarding between bridge ports or packet filtering, to this specialized hardware chip without consuming any CPU resources. In RouterOS, we have named this function Bridge Hardware (HW) Offloading. Different MikroTik devices might have different switch chips and each chip has a different set of features available, so make sure to visit this article to get more details - Bridge Hardware Offloading. 

**==> picture [504 x 189] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

Interface HTB will not work correctly when the out-interface is hardware offloaded and the bridge Fast Path is not active. 

**==> picture [504 x 327] intentionally omitted <==**

switching decision - widely depends on the switch model. This block controls all the switching-related tasks, like host learning, packet forwarding, filtering, VLAN tagging/untagging, etc. Certain switch configurations can alter the packet flow; 

switch-cpu port - a special purpose switch port for communication between the main CPU and other switch ports. Note that the switch-cpu port does not show up anywhere on RouterOS except for the switch menu, none of the software-related configurations (e.g. interface-list) can be applied to this port. Packets that reach the CPU are automatically associated with the physical in-interface. 

682 

The hardware offloading, however, does not restrict a device to only hardware limited features, rather it is possible to take advantage of the hardware and software processing at the same time. This does require a profound understanding of how packets travel through the switch chip and when exactly they are passed to the main CPU. 

**==> picture [13 x 13] intentionally omitted <==**

Switch features found in the "/interface/ethernet/switch" menu and its sub-menus, like ACL rules, mirroring, ingress/egress rate limiters, QoS, and L3HW (except inter-VLAN routing) may not rely on bridge hardware offloading. Therefore, they can potentially be applied to interfaces not configured within a hardware-offloaded bridge.

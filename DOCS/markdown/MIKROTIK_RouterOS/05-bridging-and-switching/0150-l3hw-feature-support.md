## L3HW Feature Support 

HW - the feature is supported and offloaded to the hardware. 

- CPU - the feature is supported but performed by software (CPU) 

- N/A - the feature is not available together with L3HW. Layer 3 hardware offloading must be completely disabled ( switch `l3-hw-offloading=no` ) to make this feature work. 

- FW - the feature requires `l3-hw-offloading=no` for a given switch port . On the switch level, `l3-hw-offloading=yes` . 

**==> picture [516 x 145] intentionally omitted <==**

**----- Start of picture text -----**<br>
Feature Support Comments Release<br>IPv4 Unicast  HW 7.1<br>Routing<br>IPv6 Unicast  HW /interface/ethernet/switch/l3hw-settings/set ipv6-hw=yes 7.6<br>Routing<br>IPv4  CPU<br>Multicast<br>Routing<br>IPv6  CPU<br>Multicast<br>Routing<br>**----- End of picture text -----**<br>

447 

**==> picture [516 x 689] intentionally omitted <==**

**----- Start of picture text -----**<br>
ECMP HW Multipath routing 7.1<br>Blackholes HW /ip/route add dst-address=10.0.99.0/24 blackhole 7.1<br>gateway=<int CPU/HW /ip/route add dst-address=10.0.0.0/24 gateway=ether1  7.1<br>erface_name><br>This works only for directly connected networks. Since HW does not know how to send ARP requests,<br>CPU sends an ARP request and waits for a reply to find out the DST MAC address on the first received packet of the<br>connection that matches a DST IP address.<br>After DST MAC is determined, HW entry is added and all further packets will be processed by the switch chip.<br>Bridge HW Routing from/to hardware-offloaded bridge interface. 7.1<br>VLAN HW Routing between VLAN interfaces that are created on hardware-offloaded bridge interface with vlan-filtering. 7.1<br>/interface/vlan<br>Bonding HW Routing between bonding interfaces. 7.1<br>/interface/bonding<br>Only  802.3ad  and  balance-xor  bonding modes are hardware offloaded.<br>IPv4 Firewall FW Users must choose either HW-accelerated routing or firewall. 7.1<br>Firewall rules get processed by the CPU.  Fasttrack connections get offloaded to HW.<br>IPv4 NAT FW NAT rules applied to the offloaded Fasttrack connections get processed by HW too. 7.1<br>MLAG N/A<br>VRF N/A Only the  main  routing table gets offloaded. If VRF is used together with L3HW and packets arrive on a switch port with  l3-hw-<br>offloading=yes , packets can be incorrectly routed through the main routing table. To avoid this, disable L3HW on needed<br>switch ports or use ACL rules to redirect specific traffic to the CPU.<br>VRRP N/A<br>Controller  N/A<br>Bridge and<br>Port Extender<br>Traffic-Flow N/A L3HW offloaded traffic is not repored through Traffic Flow.<br>VXLAN HW Support for hardware-offloaded VXLAN data plane, VXLAN encapsulation and decapsulation. This allows for static one-to-one  7.18<br>VLAN-to-VXLAN mappings within a vlan-filtering bridge.<br>At this point, some known features are not yet implemented.<br>Underlay (routing encapsulated VXLAN packets):<br>1. VTEPs are not supported over ECMP<br>2. VTEPs are not supported over bond, bridge, VLAN interfaces (only stand-alone routed Ethernet interfaces are supported)<br>3. VTEPs are not supported over multicast<br>4. VTEPs cannot operate within VRFs<br>5. VTEPs are not supported with IPv6<br>Overlay (forwarding between Ethernet and VXLAN):<br>1. VLAN tagging over VXLAN is not supported<br>2. Routing between different VXLAN VNIs is not supported<br>3. VTEPs are isolated, and there is no mechanism to control "horizon" between them.<br>4. Bridged VXLAN interfaces do not support IGMP snooping. When snooping is enabled, MDB entries on VXLAN are not<br>offloaded, and multicast traffic gets restricted between Ethernet and VXLAN.<br>5. Bridged VXLAN interfaces are not supported by MLAG.<br>/interface/vxlan<br>MTU HW The hardware supports up to 8 MTU profiles. 7.1<br>QinQ Routing CPU Stacked routable VLAN interfaces will lose L3HW offloading, while routable VLAN interfaces created directly on the bridge<br>interface can still use HW offloading.<br>**----- End of picture text -----**<br>

448 

Only the devices listed in the table below support L3 HW Offloading.

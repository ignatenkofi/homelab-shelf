## Sub-menu: `/interface ethernet switch rule` 

**==> picture [516 x 275] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>copy-to-cpu  (no | yes; Default: no ) Clones the matching packet and sends it to the CPU.<br>disabled  (yes | no; Default: no ) Enables or disables ACL entry.<br>dscp  (0..63) Matching the DSCP field of the packet (only applies to IPv4 packets).<br>dst-address  (IP address/Mask) Matching destination IPv4 address and mask. If  mac-protocol=arp<br>is specified, matches the destination IP in ARP packets. Without  mac-<br>protocol , matches only IPv4 packets.<br>dst-address6  (IPv6 address/Mask) Matching destination IPv6 address and mask.<br>dst-mac-address  (MAC address/Mask) Matching destination MAC address and mask.<br>dst-port  (0..65535) Matching destination protocol port number (applies to IPv4 and IPv6<br>packets if  mac-protocol  is not specified).<br>flow-label  (0..1048575) Matching IPv6 flow label.<br>mac-protocol  (802.2 | arp | capsman | dot1x | homeplug-av | ip | ipv6 | ipx |  Matching particular MAC protocol specified by protocol name or<br>lacp | lldp | loop-protect | macsec | mpls-multicast | mpls-unicast | mvrp |  number<br>packing-compr | packing-simple | pppoe | pppoe-discovery | rarp | romon |<br>service-vlan | vlan | or 0..65535 | or 0x0000-0xffff)<br>mirror  (no | yes) Clones the matching packet and sends it to the mirror-target port.<br>**----- End of picture text -----**<br>

406 

new-dst-ports (ports | bond | all 

) 

Changes the destination port to the specified value: 

- If the setting is left empty (e.g. `new-dst-ports=""` ), the packet will be dropped; If a port or  hardware-offloaded bonding interface is specified, the packet will be redirected to that port. Only single port or bond interface is supported; if you use the `all` argument, packet will be allowed to pass through to the egress processing without being dropped; If this parameter is not used, the packet will be accepted as is. 

**==> picture [516 x 411] intentionally omitted <==**

**----- Start of picture text -----**<br>
new-vlan-id  (0..4095) Changes the VLAN ID to the specified value. Requires  vlan-<br>filtering=yes .<br>new-vlan-priority  (0..7) Changes the VLAN priority (priority code point). Requires  vlan-<br>filtering=yes .<br>ports  (ports | bond) Matching switch interfaces where the rule will apply to incoming traffic.<br>Multiple ports and hardware-offloaded bonding interfaces can be<br>selected. Note that the  switch1-cpu  port cannot be selected. If  ports<br>property is left empty, the rule will apply to all switch interfaces.<br>protocol  (dccp | ddp | egp | encap | etherip | ggp | gre | hmp | icmp | icmpv6 |  Matching particular IP protocol specified by protocol name or number.<br>idpr-cmtp | igmp | ipencap | ipip | ipsec-ah | ipsec-esp | ipv6 | ipv6-frag | ipv6- Only applies to IPv4 packets if  mac-protocol  is not specified. To<br>nonxt | ipv6-opts | ipv6-route | iso-tp4 | l2tp | ospf | pim | pup | rdp | rspf | rsvp |  match certain IPv6 protocols, use the  mac-protocol=ipv6  setting.<br>sctp | st | tcp | udp | udp-lite | vmtp | vrrp | xns-idp | xtp | or 0..255)<br>rate  (0..4294967295) Sets ingress traffic limitation (bits per second) for matched traffic.<br>redirect-to-cpu  (no | yes) Changes the destination port of a matching packet to the CPU.<br>src-address  (IP address/Mask) Matching source IPv4 address and mask. If  mac-protocol=arp  is<br>specified, matches the source IP in ARP packets. Without  mac-<br>protocol , matches only IPv4 packets.<br>src-address6  (IPv6 address/Mask) Matching source IPv6 address and mask.<br>src-mac-address  (MAC address/Mask) Matching source MAC address and mask.<br>src-port  (0..65535) Matching source protocol port number (applies to IPv4 and IPv6<br>packets if  mac-protocol  is not specified).<br>switch  (switch group) Matching switch group on which will the rule apply.<br>traffic-class  (0..255) Matching IPv6 traffic class.<br>vlan-id  (0..4095) Matching VLAN ID. Requires vlan-filtering=yes .<br>vlan-header  (not-present | present) Matching VLAN header, whether the VLAN header is present or not.<br>Requires vlan-filtering=yes .<br>vlan-priority  (0..7) Matching VLAN priority (priority code point).<br>**----- End of picture text -----**<br>

Action parameters: 

copy-to-cpu redirect-to-cpu mirror new-dst-ports (can be used to drop packets) new-vlan-id new-vlan-priority rate 

Layer2 condition parameters: 

dst-mac-address mac-protocol src-mac-address 

407 

vlan-id vlan-header vlan-priority 

Layer3 condition parameters: 

dscp protocol IPv4 conditions: dst-address src-address IPv6 conditions: dst-address6 flow-label src-address6 traffic-class 

Layer4 condition parameters: 

dst-port src-port 

**==> picture [13 x 13] intentionally omitted <==**

For VLAN related matchers or VLAN related action parameters to work, you need to enable `vlan-filtering` on the bridge interface and make sure that hardware offloading is enabled on those ports, otherwise, these parameters will not have any effect. 

**==> picture [13 x 13] intentionally omitted <==**

When bridge interface `ether-type` is set to `0x8100` , then VLAN related ACL rules are relevant to frames tagged using regular/customer VLAN (TPID 0x8100), this includes `vlan-id` and `new-vlan-id` . When bridge interface `ether-type` is set to `0x88a8` , then ACL rules are relevant to frames tagged with 802.1ad service tag (TPID 0x88a8).

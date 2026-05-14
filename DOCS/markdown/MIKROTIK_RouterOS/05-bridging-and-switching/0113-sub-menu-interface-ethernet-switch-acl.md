## Sub-menu: `/interface ethernet switch acl` 

ACL condition part for MAC-related fields of packets. 

428 

**==> picture [507 x 685] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Enables or disables ACL entry.<br>table  (egress | ingress; Default: ingress ) Selects the policy table for incoming or outgoing<br>packets.<br>invert-match  (yes | no; Default: no ) Inverts the whole ACL rule matching.<br>src-ports  (ports,trunks) Matching physical source ports or trunks.<br>dst-ports  (ports,trunks) Matching physical destination ports or trunks. It is<br>not possible to match broadcast/multicast traffic on<br>the egress port due to a hardware limitation.<br>mac-src-address  (MAC address/Mask) Source MAC address and mask.<br>mac-dst-address  (MAC address/Mask) Destination MAC address and mask.<br>dst-addr-registered  (yes | no) Defines whether to match packets with registered<br>state - packets whose destination MAC address is<br>in UFDB/MFDB/RFDB. Valid only in the egress<br>table.<br>mac-protocol  (802.2 | arp | homeplug-av | ip | ip-or-ipv6 | ipv6 | ipx | lldp | loop-protect | mpls- Ethernet payload type (MAC-level protocol)<br>multicast | mpls-unicast | mvrp | non-ip | packing-compr | packing-simple | pppoe | pppoe-<br>discovery | rarp | service-vlan | vlan or integer: 0..65535 decimal format or 0x0000-0xffff hex  802.2  - 802.2 Frames (0x0004)<br>format) arp  - Address Resolution Protocol (0x0806)<br>capsman  - CAPsMAN to CAP MAC layer<br>connection (0x88BB)<br>dot1x  - EAPoL IEEE 802.1X (0x888E)<br>homeplug-av  - HomePlug AV MME (0x88E1)<br>ip  - Internet Protocol version 4 (0x0800)<br>ip-or-ipv6  - IPv4 or IPv6 (0x0800 or 0x86DD)<br>ipv6  - Internet Protocol Version 6 (0x86DD)<br>ipx  - Internetwork Packet Exchange (0x8137)<br>lacp  - Link Aggregation Control Protocol (0x88<br>09)<br>lldp  - Link Layer Discovery Protocol (0x88CC)<br>loop-protect  - Loop Protect Protocol (0x9003)<br>macsec  - MAC security IEEE 802.1AE<br>(0x88E5)<br>mpls-multicast  - MPLS multicast (0x8848)<br>mpls-unicast  - MPLS unicast (0x8847)<br>mvrp  - Multiple VLAN Registration protocol<br>(0x88F5)<br>non-ip  - Not Internet Protocol version 4 (not<br>0x0800)<br>packing-compr  - Encapsulated packets with<br>compressed IP packing (0x9001)<br>packing-simple  - Encapsulated packets with<br>simple IP packing (0x9000)<br>pppoe  - PPPoE Session Stage (0x8864)<br>pppoe-discovery  - PPPoE Discovery Stage<br>(0x8863)<br>rarp  - Reverse Address Resolution Protocol<br>(0x8035)<br>romon  - Router Management Overlay<br>Network RoMON (0x88BF)<br>service-vlan  - Provider Bridging (IEEE 802.1<br>ad) & Shortest Path Bridging IEEE 802.1aq<br>(0x88A8)<br>vlan  - VLAN-tagged frame (IEEE 802.1Q) and<br>Shortest Path Bridging IEEE 802.1aq with<br>NNI compatibility (0x8100)<br>**----- End of picture text -----**<br>

429 

) 

drop-precedence (drop | green | red | yellow 

Matching internal drop precedence. Valid only in the egress table. 

custom-fields 

ACL condition part for VLAN-related fields of packets. 

**==> picture [507 x 233] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>lookup-vid  (0..4095) VLAN id used in lookup. It can be changed before reaching the egress<br>table.<br>service-vid  (0-4095) Matching service VLAN id.<br>service-pcp  (0..7) Matching service PCP.<br>service-dei  (0..1) Matching service DEI.<br>service-tag  (priority-tagged | tagged | tagged-or-priority-tagged | untagged) Format of the service tag.<br>customer-vid  (0-4095) Matching customer VLAN ID.<br>customer-pcp  (0..7) Matching customer PCP.<br>customer-dei  (0..1) Matching customer DEI.<br>customer-tag  (priority-tagged | tagged | tagged-or-priority-tagged |  Format of the customer tag.<br>untagged)<br>priority  (0..15) Matching internal priority. Valid only in the egress table.<br>**----- End of picture text -----**<br>

ACL condition part for IPv4 and IPv6 related fields of packets. 

**==> picture [507 x 327] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>ip-src  (IPv4/0..32) Matching source IPv4 address.<br>ip-dst  (IPv4/0..32) Matching destination IPv4 address.<br>ip-protocol  (tcp | udp | udp-lite | other) IP protocol type.<br>src-l3-port  (0-65535) Matching Layer3 source port.<br>dst-l3-port  (0-65535) Matching Layer3 destination port.<br>ttl  (0 | 1 | max | other) Matching TTL field of the packet.<br>dscp  (0..63) Matching DSCP field of the packet.<br>ecn  (0..3) Matching ECN field of the packet.<br>fragmented  (yes | no) Whether to match fragmented packets.<br>first-fragment  (yes | no) YES matches not fragmented and the first fragments, NO matches other fragments.<br>ipv6-src  (IPv6/0..128) Matching source IPv6 address.<br>ipv6-dst  (IPv6/0..128) Matching destination IPv6 address.<br>mac-isolation-profile  (community1 | community2 |  Matches isolation profile based on UFDB. Valid only in the egress policy table.<br>isolated | promiscuous)<br>src-mac-addr-state  (dynamic-station-move | sa- Defines whether to match packets with registered state - packets whose destination MAC<br>found | sa-not-found | static-station-move) address is in UFDB/MFDB/RFDB. Valid only in the egress policy table.<br>flow-id  (0..63)<br>**----- End of picture text -----**<br>

ACL rule action part. 

430 

**==> picture [507 x 415] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (copy-to-cpu | drop | forward |<br>copy-to-cpu - Packets are copied to the CPU if they match the ACL conditions.<br>redirect-to-cpu | send-to-new-dst-ports;  drop - Packets are dropped if they match the ACL conditions.<br>Default: forward - Packets are forwarded if they match the ACL conditions.<br>redirect-to-cpu - Packets are redirected to the CPU if they match the ACL conditions.<br>forward )<br>send-to-new-dst-ports - Packets are sent to new destination ports if they match the ACL conditions.<br>new-dst-ports  (ports,trunks) If the action is "send-to-new-dst-ports", then this property sets which ports/trunks are the new<br>destinations.<br>mirror-to  (mirror0 | mirror1) Mirroring destination for ACL packets.<br>policer  (policer) Applied ACL Policer for ACL packets.<br>src-mac-learn  (yes | no) Whether to learn the source MAC of the matched ACL packets. Valid only in the ingress policy table.<br>new-service-vid  (0..4095) New service VLAN ID for ACL packets.<br>new-service-pcp  (0..7) New service PCP for ACL packets.<br>new-service-dei  (0..1) New service DEI for ACL packets.<br>new-customer-vid  (0..4095) New customer VLAN ID for ACL packets. If set to 4095, then traffic is dropped.<br>new-customer-pcp  (0..7) New customer PCP for ACL packets.<br>new-customer-dei  (0..1) New customer DEI for ACL packets.<br>new-dscp  (0..63) New DSCP for ACL packets.<br>new-priority  (0..15) New internal priority for ACL packets.<br>new-drop-precedence  (drop | green |  New internal drop precedence for ACL packets.<br>red | yellow)<br>new-registered-state  (yes | no) Whether to modify packet status. YES sets packet status to registered, NO - unregistered. Valid only in<br>the ingress policy table.<br>new-flow-id  (0..63)<br>**----- End of picture text -----**<br>

Filter bypassing part for ACL packets. 

**==> picture [507 x 149] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>attack-filter-bypass  (yes | no; Default: no )<br>ingress-vlan-filter-bypass  (yes | no;  Allows bypassing ingress VLAN filtering in the VLAN table for matching packets. This applies only to the<br>Default: no ) ingress policy table.<br>egress-vlan-filter-bypass  (yes | no;  Allows bypassing egress VLAN filtering in the VLAN table for matching packets. This applies only to the<br>Default: no ) ingress policy table.<br>isolation-filter-bypass  (yes | no; Default: no ) Allows bypassing the Isolation table for matching packets. This applies only to the ingress policy table.<br>egress-vlan-translate-bypass  (yes | no;  Allows bypassing egress VLAN translation table for matching packets.<br>Default: no )<br>**----- End of picture text -----**<br>

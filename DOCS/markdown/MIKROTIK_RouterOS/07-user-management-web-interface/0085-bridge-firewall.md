## Bridge Firewall 

The bridge firewall implements packet filtering and thereby provides security functions that are used to manage data flow to, from, and through the bridge. 

Packet flow diagram shows how packets are processed through the router. It is possible to force bridge traffic to go through `/ip firewall filter` r ules (see the bridge settings). 

There are two bridge firewall tables: 

filter - bridge firewall with three predefined chains: 

input - filters packets, where the destination is the bridge (including those packets that will be routed, as they are destined to the bridge MAC address anyway) 

output - filters packets, which come from the bridge (including those packets that has been routed normally) 

forward - filters packets, which are to be bridged (note: this chain is not applied to the packets that should be routed through the router, just to those that are traversing between the ports of the same bridge) 

- nat - bridge network address translation provides ways for changing source/destination MAC addresses of the packets traversing a bridge. Has two built-in chains: 

387 

srcnat - used for "hiding" a host or a network behind a different MAC address. This chain is applied to the packets leaving the router through a bridged interface 

dstnat - used for redirecting some packets to other destinations 

You can put packet marks in bridge firewall (filter and NAT), which are the same as the packet marks in IP firewall configured by `'/ip firewall mangle'` . In this way, packet marks put by bridge firewall can be used in 'IP firewall', and vice versa. 

General bridge firewall properties are described in this section. Some parameters that differ between nat and filter rules are described in further sections. 

Sub-menu: `/interface bridge filter, /interface bridge nat` 

**==> picture [502 x 580] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>802.3-sap  (integer; Default: ) DSAP (Destination Service Access Point) and SSAP (Source Service<br>Access Point) are 2 one-byte fields, which identify the network<br>protocol entities which use the link-layer service. These bytes are<br>always equal. Two hexadecimal digits may be specified here to match<br>an SAP byte.<br>802.3-type  (integer; Default: ) Ethernet protocol type, placed after the IEEE 802.2 frame header.<br>Works only if 802.3-sap is 0xAA (SNAP - Sub-Network Attachment<br>Point header). For example, AppleTalk can be indicated by the SAP<br>code of 0xAA followed by a SNAP type code of 0x809B.<br>action  (accept | drop | jump | log | mark-packet | passthrough | return | set- Action to take if the packet is matched by the rule:<br>priority; Default: )<br>accept - accept the packet. The packet is not passed to the next<br>firewall rule<br>drop - silently drop the packet<br>jump - jump to the user-defined chain specified by the value of  ju<br>mp-target parameter<br>log - add a message to the system log containing the following<br>data: in-interface, out-interface, src-mac, protocol, src-ip:port-<br>>dst-ip:port and length of the packet. After the packet is matched<br>it is passed to the next rule in the list, similar as  passthrough<br>mark-packet - place a mark specified by the new-packet-mark<br>parameter on a packet that matches the rule<br>passthrough - if the packet is matched by the rule, increase<br>counter and go to next rule (useful for statistics)<br>return - passes control back to the chain from where the jump<br>took place<br>set-priority - set priority specified by the new-priority parameter<br>on the packets sent out through a link that is capable of<br>transporting priority (VLAN or WMM-enabled wireless interface).<br>Read more<br>arp-dst-address  (IP address; Default: ) ARP destination IP address.<br>arp-dst-mac-address  (MAC address; Default: ) ARP destination MAC address.<br>arp-gratuitous  (yes | no; Default: ) Matches ARP gratuitous packets.<br>arp-hardware-type  (integer; Default: 1 ) ARP hardware type. This is normally Ethernet (Type 1).<br>arp-opcode  (arp-nak | drarp-error | drarp-reply | drarp-request | inarp-reply  ARP opcode (packet type)<br>| inarp-request | reply | reply-reverse | request | request-reverse; Default: )<br>arp-nak - negative ARP reply (rarely used, mostly in ATM<br>networks)<br>drarp-error - Dynamic RARP error code, saying that an IP<br>address for the given MAC address can not be allocated<br>drarp-reply - Dynamic RARP reply, with a temporary IP address<br>assignment for a host<br>drarp-request - Dynamic RARP request to assign a temporary IP<br>address for the given MAC address<br>inarp-reply - InverseARP Reply<br>inarp-request - InverseARP Request<br>**----- End of picture text -----**<br>


388 

reply - standard ARP reply with a MAC address 

reply-reverse - reverse ARP (RARP) reply with an IP address assigned request - standard ARP request to a known IP address to find out unknown MAC address request-reverse - reverse ARP (RARP) request to a known MAC address to find out the unknown IP address (intended to be used by hosts to find out their own IP address, similarly to DHCP service) 

arp-packet-type (integer 0..65535 | hex 0x0000-0xffff; Default: ) ARP Packet Type. arp-src-address (IP address; Default: ) ARP source IP address. arp-src-mac-address (MAC addres; Default: ) ARP source MAC address. chain (text; Default: ) Bridge firewall chain, which the filter is functioning in (either a built-in one, or a user-defined one). dst-address (IP address; Default: ) Destination IP address (only if MAC protocol is set to IP). dst-address6 (IPv6 address; Default: ) Destination IPv6 address (only if MAC protocol is set to IPv6). dst-mac-address (MAC address; Default: ) Destination MAC address. dst-port (integer 0..65535; Default: ) Destination port number or range (only for TCP or UDP protocols). in-bridge (name; Default: ) Bridge interface through which the packet is coming in. in-bridge-list (name; Default: ) Set of bridge interfaces defined in interface list. Works the same as `in -bridge` . in-interface (name; Default: ) Physical interface (i.e., bridge port) through which the packet is coming in. in-interface-list (name; Default: ) Set of interfaces defined in interface list. Works the same as `ininterface` . ingress-priority (integer 0..63; Default: ) Matches the priority of an ingress packet. Priority may be derived from VLAN, WMM, DSCP or MPLS EXP bit. read more ip-protocol (dccp | ddp | egp | encap | etherip | ggp | gre | hmp | icmp | IP protocol (only if MAC protocol is set to IPv4) icmpv6 | idpr-cmtp | igmp | ipencap | ipip | ipsec-ah | ipsec-esp | ipv6 | ipv6frag | ipv6-nonxt | ipv6-opts | ipv6-route | iso-tp4 | l2tp | ospf | pim | pup | dccp - Datagram Congestion Control Protocol rdp | rspf | rsvp | sctp | st | tcp | udp | udp-lite | vmtp | vrrp | xns-idp | xtp; ddp - Datagram Delivery Protocol Default: ) egp - Exterior Gateway Protocol encap - Encapsulation Header etherip - Ethernet-within-IP Encapsulation ggp - Gateway-to-Gateway Protocol gre - Generic Routing Encapsulation hmp - Host Monitoring Protocol icmp - IPv4 Internet Control Message Protocol icmpv6 - IPv6 Internet Control Message Protocol idpr-cmtp - Inter-Domain Policy Routing Control Message Transport Protocol igmp - Internet Group Management Protocol ipencap - IP in IP (encapsulation) ipip - IP-within-IP Encapsulation Protocol ipsec-ah - IPsec Authentication Header ipsec-esp - IPsec Encapsulating Security Payload ipv6 - Internet Protocol version 6 ipv6-frag - Fragment Header for IPv6 ipv6-nonxt - No Next Header for IPv6 ipv6-opts - Destination Options for IPv6 ipv6-route - Routing Header for IPv6 iso-tp4 - ISO Transport Protocol Class 4 l2tp - Layer Two Tunneling Protocol ospf - Open Shortest Path First 

389 

**==> picture [502 x 696] intentionally omitted <==**

**----- Start of picture text -----**<br>
pim - Protocol Independent Multicast<br>pup - PARC Universal Packet<br>rdp - Reliable Data Protocol<br>rspf - Radio Shortest Path First<br>rsvp - Reservation Protocol<br>sctp - Stream Control Transmission Protocol<br>st - Internet Stream Protocol<br>tcp - Transmission Control Protocol<br>udp - User Datagram Protocol<br>udp-lite - Lightweight User Datagram Protocol<br>vmtp - Versatile Message Transaction Protocol<br>vrrp - Virtual Router Redundancy Protocol<br>xns-idp - Xerox Network Systems Internet Datagram Protocol<br>xtp - Xpress Transport Protocol<br>jump-target  (name; Default: ) If action=jump specified, then specifies the user-defined firewall<br>chain to process the packet.<br>limit  (integer/time,integer; Default: ) Matches packets up to a limited rate. A rule using this matcher will<br>match until this limit is reached.<br>count - maximum average packet rate, measured in packets per<br>second (pps), unless followed by Time option<br>time - specifies the time interval over which the packet rate is<br>measured<br>burst - number of packets to match in a burst<br>log  (yes | no; Default:  no ) Add a message to the system log containing the following data: in-<br>interface, out-interface, src-mac, dst-mac, eth-protocol, ip-protocol,<br>src-ip:port->dst-ip:port, and length of the packet.<br>log-prefix  (text; Default: ) Defines the prefix to be printed before the logging information.<br>mac-protocol  (802.2 | arp | capsman | dot1x | homeplug-av | ip | ipv6 | ipx |  Ethernet payload type (MAC-level protocol). To match protocol type<br>lacp | length | lldp | loop-protect | macsec | mpls-multicast | mpls-unicast |  for VLAN encapsulated frames (0x8100 or 0x88a8), a vlan-encap prop<br>mvrp | packing-compr | packing-simple | pppoe | pppoe-discovery | rarp |  erty should be used.<br>romon | service-vlan | vlan | integer 0..65535 | hex 0x0000-0xffff; Default: )<br>802.2 - 802.2 Frames (0x0004)<br>arp - Address Resolution Protocol (0x0806)<br>homeplug-av - HomePlug AV MME (0x88E1)<br>ip - Internet Protocol version 4 (0x0800)<br>ipv6 - Internet Protocol Version 6 (0x86DD)<br>ipx - Internetwork Packet Exchange (0x8137)<br>length - Packets with length field (0x0000-0x05DC)<br>lldp - Link Layer Discovery Protocol (0x88CC)<br>loop-protect - Loop Protect Protocol (0x9003)<br>mpls-multicast - MPLS multicast (0x8848)<br>mpls-unicast - MPLS unicast (0x8847)<br>mvrp - Multiple VLAN Registration protocol (0x88F5)<br>packing-compr - Encapsulated packets with compressed IP<br>packing (0x9001)<br>packing-simple - Encapsulated packets with simple IP packing (0<br>x9000)<br>pppoe - PPPoE Session Stage (0x8864)<br>pppoe-discovery - PPPoE Discovery Stage (0x8863)<br>rarp - Reverse Address Resolution Protocol (0x8035)<br>service-vlan - Provider Bridging (IEEE 802.1ad) & Shortest Path<br>Bridging IEEE 802.1aq (0x88A8)<br>vlan - VLAN-tagged frame (IEEE 802.1Q) and Shortest Path<br>Bridging IEEE 802.1aq with NNI compatibility (0x8100)<br>new-packet-mark  (string; Default: ) Sets a new packet-mark value.<br>new-priority  (integer | from-ingress; Default: ) Sets a new priority for a packet. This can be the VLAN, WMM or<br>MPLS EXP priority Read more. This property can also be used to set<br>**----- End of picture text -----**<br>


390 

**==> picture [502 x 696] intentionally omitted <==**

**----- Start of picture text -----**<br>
an internal priori<br>out-bridge  (name; Default: ) Outgoing bridge interface.<br>out-bridge-list  (name; Default: ) Set of bridge interfaces defined in interface list. Works the same as  ou<br>t-bridge .<br>out-interface  (name; Default: ) Interface that the packet is leaving the bridge through.<br>out-interface-list  (name; Default: ) Set of interfaces defined in interface list. Works the same as out-<br>interface .<br>packet-mark  (name; Default: ) Match packets with a certain packet mark.<br>packet-type  (broadcast | host | multicast | other-host; Default: ) MAC frame type:<br>broadcast - broadcast MAC packet<br>host - packet is destined to the bridge itself<br>multicast - multicast MAC packet<br>other-host - packet is destined to some other unicast address,<br>not to the bridge itself<br>src-address  (IP address; Default: ) Source IP address (only if MAC protocol is set to IPv4).<br>src-address6  (IPv6 address; Default: ) Source IPv6 address (only if MAC protocol is set to IPv6).<br>src-mac-address  (MAC address; Default: ) Source MAC address.<br>src-port  (integer 0..65535; Default: ) Source port number or range (only for TCP or UDP protocols).<br>stp-flags  (topology-change | topology-change-ack; Default: ) The BPDU (Bridge Protocol Data Unit) flags. Bridge exchange<br>configuration messages named BPDU periodically for preventing loops<br>topology-change - topology change flag is set when a bridge<br>detects port state change, to force all other bridges to drop their<br>host tables and recalculate network topology<br>topology-change-ack - topology change acknowledgment flag is<br>sent in replies to the notification packets<br>stp-forward-delay  (integer 0..65535; Default: ) Forward delay timer.<br>stp-hello-time  (integer 0..65535; Default: ) STP hello packets time.<br>stp-max-age  (integer 0..65535; Default: ) Maximal STP message age.<br>stp-msg-age  (integer 0..65535; Default: ) STP message age.<br>stp-port  (integer 0..65535; Default: ) STP port identifier.<br>stp-root-address  (MAC address; Default: ) Root bridge MAC address.<br>stp-root-cost  (integer 0..65535; Default: ) Root bridge cost.<br>stp-root-priority  (integer 0..65535; Default: ) Root bridge priority.<br>stp-sender-address  (MAC address; Default: ) STP message sender MAC address.<br>stp-sender-priority  (integer 0..65535; Default: ) STP sender priority.<br>stp-type  (config | tcn; Default: ) The BPDU type:<br>config - configuration BPDU<br>tcn - topology change notification<br>tls-host  (string; Default: ) Allows matching https traffic based on TLS SNI hostname. Accepts GL<br>OB syntax for wildcard matching. Note that matcher will not be able to<br>match hostname if the TLS handshake frame is fragmented into<br>multiple TCP segments (packets).<br>**----- End of picture text -----**<br>


391 

Matches the MAC protocol type encapsulated in the VLAN frame. Matches the VLAN identifier field. Matches the VLAN priority (priority code point) 

vlan-encap (802.2 | arp | ip | ipv6 | ipx | length | mpls-multicast | mplsunicast | pppoe | pppoe-discovery | rarp | vlan | integer 0..65535 | hex 0x0000-0xffff; Default: ) 

vlan-id (integer 0..4095; Default: ) 

vlan-priority (integer 0..7; Default: ) 

Footnotes: 

STP matchers are only valid if the destination MAC address is `01:80:C2:00:00:00/FF:FF:FF:FF:FF:FF` (Bridge Group address), also STP should be enabled. 

ARP matchers are only valid if mac-protocol is `arp` or `rarp` 

VLAN matchers are only valid for `0x8100` or `0x88a8` ethernet protocols 

IP or IPv6 related matchers are only valid if mac-protocol is either set to `ip` or `ipv6` 

802.3 matchers are only consulted if the actual frame is compliant with IEEE 802.2 and IEEE 802.3 standards. These matchers are ignored for other packets.

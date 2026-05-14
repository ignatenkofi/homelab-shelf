## Feature Status 

N/A - Feature not yet available 

OK - Initial tests successful 

NOK - initial tests not successful 

Highlight Colors: 

Yellow - partially working Green - Working Red - Not working at the moment 

**==> picture [516 x 417] intentionally omitted <==**

**----- Start of picture text -----**<br>
Feature v7.6 v7.10 v7. v7. v7. v7. v7. v7. v7.<br>12 14 15 17 18 20 21<br>Winbox<br>BGP support<br>OSPF support<br>RIP support<br>Router ID support<br>Routing filter support<br>Generic<br>/31 address support<br>Convert route rules after upgrade from v6.x<br>Static IPv6 upgrade from ROS v6<br>IPv4 Route Rules<br>IPv6 Route Rules<br>ECMP flags<br>dst@table<br>gateway@table<br>gateway%interface<br>recursive route over ipv6 LL address<br>3 level recursive gateway with ECMP<br>IPV6 ECMP<br>IPv6 connected ECMP<br>Addresses from same subnet to multiple<br>interfaces<br>Show time when route was last updated<br>Check Gateway BFD not ready<br>Scope and target scope<br>IPv4 Mangle routing-mark<br>IPv6 Mangle routing-mark<br>**----- End of picture text -----**<br>

1067 

**==> picture [516 x 687] intentionally omitted <==**

**----- Start of picture text -----**<br>
Packet SRC address Does not work correctly with /32<br>addresses<br>Routing-table parameter for ping and telnet<br>Show if route is hardware accelerated Shows if route is candidate for HW<br>acceleration<br>Custom route selection policy<br>IPv4 with IPv6 nexthops for RFC5549<br>Routing id<br>VRF<br>Management services support for VRFs  telnet, ssh, api, www services can be<br>set to listen on specific VRF<br>Dynamically import/export routes from one vrf to<br>another within the same router<br>BFD Initial support<br>OSPF<br>Convert OSPF config from v6 to v7 after upgrade Known conversion problems:<br>NBMA neighbors place in<br>backbone<br>ospf-v2 networks + interface may<br>have issues<br>dynamic interfaces may have<br>issues<br>MPLS PE CE features are not<br>converted<br>OSPF neighbors in NSSA Area<br>OSPF in broadcast network<br>OSPF with routing filters<br>OSPF Virtual Link<br>OPSF input filtering<br>HMAC-SHA auth RFC5709 Initial support<br>OSPF SNMP monitoring<br>BGP SNMP monitoring For ipv4 sessions<br>IS-IS<br>IPv4 Initial<br>support<br>IPv6<br>Traffic Engineering<br>BGP<br>Convert BGP config from v6 to v7 after upgrade<br>BGP Templates and dynamic peers<br>BGP connect listen on a network<br>BGP guess remote.as<br>Show from which peer route received<br>BGP Address Families<br>BGP input.accept-*<br>eBGP nexthop self<br>Input Filter<br>Output Filter<br>BGP Local address auto selection<br>**----- End of picture text -----**<br>

1068 

**==> picture [516 x 692] intentionally omitted <==**

**----- Start of picture text -----**<br>
BGP route reflect<br>BGP route server<br>BGP Roles rfc roles not fully implemented<br>https://datatracker.ietf.org/doc/draft-ietf-idr-bgp-<br>open-policy/?include_text=1<br>BGP session uptime in "established" state<br>BGP session last established time<br>BGP Flow Spec Flow spec attributes are forwarded<br>BGP Selection<br>BGP Selection (Multipath)<br>BGP Confederation<br>BGP Aggregation<br>BGP ORF<br>Discard prefix RTBH  RFC 6666<br>AS-wide Unique BGP Identifier RFC 6286<br>Exported PDU PCAP saver<br>Exported PDU PCAP loader<br>BGP Advertisement monitoring Advertisements rework<br>BGP Prefix limit<br>BGP advertise IPv4 prefix with IPv6 nexthop  AFI<br>(RFC5549, RFC8950) /SAFI<br>1/1<br>BGP VPNv6 support Prerequisites are made, need<br>to add actual BGP Afi<br>BGP Instance config<br>EVPN Initial<br>suppo<br>rt<br>MPLS<br>Static label mapping<br>Static mapping upgrade from v6<br>LDP IPv4 mapping<br>LDP IPv6 mapping<br>LDP signaled VPLS<br>LDP config upgrade from v6<br>LDP Dual Stack<br>TE<br>TE Config upgrade from v6<br>VPLS Encap to TE<br>BGP signaled VPLS<br>VPLS config upgrade from v6<br>RSVP Fast reroute<br>FRR/RI-RSVP (RFC 8370)<br>MPLS ECMP<br>One label per VRF<br>Ability to use MPLS EXP-bit in Queues<br>MPLS Fast-Path<br>RPKI session<br>**----- End of picture text -----**<br>

1069 

RPKI possibility to view received info of specific prefix RPKI show connection status Filters Convert routing filters after upgrade from v6.x Syntax completion Routing filter chain drop by default without rules Routing filter prefix match Routing filter protocol match Routing filter append communities Routing filter append large community Routing filter set weight Routing filter set local pref Routing filter set MED Routing filter set origin Routing filter set igp metric from OSPF cost Routing filter match prefix with address list Routing filter match community/large community lists Routing filter add a prefix to address list Routing filter validate prefix with RPKI Multicast IGMP-Proxy PIM-SM

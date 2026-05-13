## Writeable Properties 

**==> picture [516 x 109] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Type Description<br>Numeric properties<br>distance route distance<br>scope<br>scope- target scope<br>target<br>**----- End of picture text -----**<br>


1056 

**==> picture [516 x 690] intentionally omitted <==**

**----- Start of picture text -----**<br>
bgp- BGP WEIGHT attribute<br>weight<br>bgp-med BGP MED attribute is local to the router. It is also used in the output of iBGP peers.<br>bgp-out- BGP MED attribute to be sent to a remote peer. Should be used in the output chain of eBGP peers.<br>med<br>bgp-local- BGP LOCALPREF attribute<br>pref<br>bgp-igp- BGP IGP METRIC<br>metric<br>bgp-path- Prepend last received remote peers ASN. If the prefix is originated from the router, then this parameter will not do<br>peer- anything on the router's output, because ASN does not exist yet.<br>prepend<br>If used as a matcher in BGP input, it is possible to filter prefixes exceeding a certain number of prepends. For<br>example, if a remote peer prepends its ASN 5 times, but we want to allow max 4 times prepended ASN, then we can<br>use: " if (bgp-path-peer-prepend > 4) {reject} "<br>This parameter also overrides any prepends received from the remote peer, for example, if the remote peer<br>prepended it's AS 3 times, we can remove this prepend by setting " bgp-path-peer-prepend  1" in BGP input<br>bgp-path- Prepend routers ASN, should be used in BGP output.<br>prepend<br>ospf-ext- OSPF External route metric<br>metric<br>ospf-ext- OSPF external route tag<br>tag<br>rip-ext- RIP External route metric<br>metric<br>rip-ext-tag RIP External route tag<br>Flag properties<br>ospf-ext- DN bit for external OSPF routes<br>dn<br>blackhole<br>suppress- Whether to suppress L3 HW offloading<br>hw-offload<br>use-te-<br>nexthop<br>Other properties<br>gw ipv4/6 address IPv4/IPv6 address or interface name. In the case of BGP output, a gateway can be adjusted in the following setups:<br>is BGP reflector<br>nexthop-choice is set to propagate<br>is not eBGP and nexthop-choice=force-self is not set.<br>gw-ll ipv6 link-local ipv6 link local nexthop attribute. In the case of BGP output, a gateway can be adjusted in the following setups:<br>is BGP reflector<br>nexthop-choice is set to propagate<br>is not eBGP and nexthop-choice=force-self is not set.<br>**----- End of picture text -----**<br>


1057 

**==> picture [516 x 338] intentionally omitted <==**

**----- Start of picture text -----**<br>
gw- interface_name Interface part of the gateway. Should be used if it is required to attach a specific interface for next-hop, like (1.2.3.4%<br>interface ether1)<br>gw-check none|arp|icmp<br>|bfd|bfd-mh<br>pref-src ipv4/6 address<br>bgp-origin igp|egp|incom<br>plete<br>ospf-ext- ipv4/6 address Forwarding address of External OSPF route<br>fwd<br>ospf-ext- type1|type2 OSPF External route type<br>type<br>comment string<br>bgp- inline_community BGP Communities attribute is defined in RFC 1997. Each community is 32-bit in size.<br>communiti _set |<br>es community_list_n<br>ame<br>bgp-ext- inline_ext_commu BGP Extended Communities attribute is defined in RFC 4360. RouterOS parses site-of-origin (prefixed with soo:) and<br>communiti nity_set |  route-target (prefixed with rt:) extended communities. For example, "set bgp-ext-communities rt:1111:2.3.4.5;". It is<br>es ext_community_li possible to set/match RAW extended communities value in 64-bit hex, for example, "set bgp-ext-community 0x.........;"<br>st_name<br>bgp-large- inline_large_com BGP Large Communities attribute is defined in RFC 8092. Suitable for use with all ASNs including 32-bit ASNs. Each<br>communiti munity_set |  community is 12-bytes in length and consists of 3 parts: "global_admin:locap_part_1:local_part_2".<br>es large_community<br>_list_name<br>**----- End of picture text -----**<br>

## Introduction 

IGMP (Internet Group Management Protocol) and MLD (Multicast Listener Discovery) snooping allow the bridge to listen to IGMP/MLD communication and make forwarding decisions for multicast traffic based on the received information. By default, bridges are flooding multicast traffic to all bridge ports just like broadcast traffic, which might not always be the best scenario (e.g. for multicast video traffic or SDVoE applications). The IGMP/MLD snooping tries to solve the problem by forwarding the multicast traffic only to ports where clients are subscribed to, see an IGMP/MLD network concept below. RouterOS bridge can process IGMP v1/v2/v3 and MLD v1/v2 packets. The implemented bridge IGMP/MLD snooping is based on RFC4541, and IGMP/MLD protocols are specified on RFC1112 (IGMPv1) RFC2236 (IGMPv2), RFC3376 (IGMPv3), RFC2710 (MLDv1), RFC3810 (MLDv2). 

**==> picture [13 x 13] intentionally omitted <==**

Source-specific multicast forwarding is not supported for IGMP v3 and MLD v2. 

515 

**==> picture [462 x 429] intentionally omitted <==**

The bridge will process the IGMP/MLD messages only when `igmp-snooping` is enabled. Additionally, the bridge should have an active IPv6 address to process MLD packets. At first, the bridge does not restrict the multicast traffic and all multicast packets get flooded. Once IGMP/MLD querier is detected by receiving an IGMP/MLD query message (the query message can be received by an external multicast router or locally by bridge interface with enabled `mul ticast-querier` ), only then the bridge will start to restrict unknown IP multicast traffic and forward the known multicast from the multicast database (MDB). The IGMP and MLD querier detection is independent, which means that detecting only IGMP querier will not affect IPv6 multicast forwarding and vice versa. The querier detection also does not restrict the forwarding of non-IP and link-local multicast groups, like 224.0.0.0/24 and ff02::1. 

**==> picture [13 x 13] intentionally omitted <==**

CRS3xx series devices with Marvell-98DX3236, Marvell-98DX224S or Marvell-98DX226S switch chips are not able to distinguish non-IP/IPv4 /IPv6 multicast packets once IGMP or MLD querier is detected. It means that the switch will stop forwarding all unknown non-IP/IPv4/IPv6 multicast traffic when the querier is detected. This does not apply to certain link-local multicast address ranges, like 224.0.0.0/24 or ff02::1.

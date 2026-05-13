## IPFIX 

Sub-menu: `/ip traffic-flow ipfix` 

Allows to customize flow records 

**==> picture [353 x 230] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bytes Total number of bytes processed in the flow.<br>ip-total-lenght Length of the IP packet in bytes.<br>src-address The source IP address of the flow.<br>dst-address The destination IP address of the flow.<br>ipv6-flow-label Label field from an IPv6 header, used to classify flows.<br>src-address-mask Network mask for the source address, useful in summarizing data.<br>dst-address-mask Network mask for the destination address.<br>is-multicast Indicates whether the flow is a multicast flow.<br>src-mac-address Source MAC address.<br>dst-mac-address Destination MAC address.<br>last-forwarded Timestamp of the last packet forwarded in a flow.<br>**----- End of picture text -----**<br>


1823 

**==> picture [353 x 472] intentionally omitted <==**

**----- Start of picture text -----**<br>
src-port Source port number.<br>dst-port Destination port number.<br>nat-dst-address Translated destination IP address by NAT.<br>sys-init-time System initialization time, can be used for timing analysis.<br>first-forwarded Timestamp of the first packet forwarded in a flow.<br>nat-dst-port Translated destination port number by NAT.<br>tcp-ack-num Acknowledgment number in a TCP connection.<br>gateway IP address of the gateway through which the flow was routed.<br>nat-events Events related to Network Address Translation for the flow.<br>tcp-flags Flags from the TCP header (e.g., SYN, ACK).<br>icmp-code ICMP code for error messaging and operational information.<br>nat-src-address Translated source IP address by NAT.<br>icmp-type Type of ICMP message, important for diagnostic messages.<br>nat-src-port Translated source port number by NAT.<br>tcp-seq-num Sequence number in a TCP connection.<br>tcp-window-size Window size in a TCP connection, indicating the scale of received data buffering.<br>igmp-type Type of Internet Group Management Protocol operation.<br>out-interface Interface through which packets of the flow are sent out.<br>in-interface Interface through which packets of the flow are received.<br>packets Number of packets processed in the flow.<br>ip-header-length Length of the IP header.<br>protocol Protocol number (e.g., TCP, UDP, ICMP).<br>tos Type of Service field in the IP header, indicating priority and handling of the packet.<br>ttl Time To Live for the packet, decremented by each router to prevent infinite loops.<br>udp-length Length of the UDP payload.<br>**----- End of picture text -----**<br>

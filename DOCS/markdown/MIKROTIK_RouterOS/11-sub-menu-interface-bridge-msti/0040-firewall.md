## Firewall 

**==> picture [504 x 181] intentionally omitted <==**

The firewall implements stateful (by utilizing connection tracking) and stateless packet filtering and thereby provides security functions that are used to manage data flow to, from, and through the router. Along with the Network Address Translation (NAT), it serves as a tool for preventing unauthorized access to directly attached networks and the router itself as well as a filter for outgoing traffic. 

Network firewalls keep outside threats away from sensitive data available inside the network. Whenever different networks are joined together, there is always a threat that someone from outside of your network will break into your LAN. Such break-ins may result in private data being stolen and distributed, valuable data being altered or destroyed, or entire hard drives being erased. Firewalls are used as a means of preventing or minimizing the security risks inherent in connecting to other networks. A properly configured firewall plays a key role in efficient and secure network infrastructure deployment. 

MikroTik RouterOS has very powerful firewall implementation with features including: 

stateless packet inspection stateful packet inspection Layer-7 protocol detection peer-to-peer protocols filtering traffic classification by: source MAC address IP addresses (network or list) and address types (broadcast, local, multicast, unicast) port or port range 

IP protocols 

protocol options (ICMP type and code fields, TCP flags, IP options and MSS) interface the packet arrived from or left through internal flow and connection marks DSCP byte packet content rate at which packets arrive and sequence numbers packet size packet arrival time 

and much more! 

Firewall is split in three major modules: 

filter/raw - used to deny traffic based on configured policies. Filtering in RAW tables allow to save resources if connection tracking is not required. mangle - used to mark certain connections, packets, streams, set priorities and do other tasks nat - used to set up address translation rules redirects and port forwarding

## Introduction 

NAT Port Mapping Protocol (NAT-PMP) is a protocol used for transparent peer-to-peer network connectivity of personal computers and network-enabled intelligent devices or appliances. 

Protocol operates by retrieving the external IPv4 address of a NAT gateway, thus allowing a client to make its external IPv4 address and port known to peers who may wish to communicate with it by creating dynamic NAT rules. 

NAT-PMP uses UDP port number 5350 - on the client, and 5351 on the server side. 

There are two interface types for PMP: internal (the one local clients are connected to) and external (the one the Internet is connected to).A router may only have one active external interface with a 'public' IP address on it 

**==> picture [13 x 13] intentionally omitted <==**

A router can have only one active external interface with a 'public' IP address on it. NAT-PMP internal interface can create NAT mapping for any subnet, not just the subnet present on the internal interface, so caution must be used when setting internal interfaces. 

For more details on NAT PMP see RFC 6886 

NAT-PMP configuration is accessible from `/ip nat-pmp` menu.

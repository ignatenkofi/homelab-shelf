## Introduction 

The MikroTik RouterOS supports Universal Plug and Play architecture for transparent peer-to-peer network connectivity of personal computers and network-enabled intelligent devices or appliances. 

UPnP enables data communication between any two devices under the command of any control device on the network. Universal Plug and Play is completely independent of any particular physical medium. It supports networking with automatic discovery without any initial configuration, whereby a device can dynamically join a network. DHCP and DNS servers are optional and will be used if available on the network. UPnP implements a simple yet powerful NAT traversal solution, that enables the client to get full two-way peer-to-peer network support from behind the NAT. 

There are two interface types for UPnP: internal (the one local clients are connected to) and external (the one the Internet is connected to). A router may only have one active external interface with a 'public' IP address on it , and as many internal interfaces as needed, all with source-NATted 'internal' IP addresses. The protocol works by creating dynamic NAT entries. 

**==> picture [13 x 13] intentionally omitted <==**

UPnP internal interface can create NAT mapping for any subnet, not just the subnet present on the internal interface, so caution must be used when setting internal interfaces. 

The UPnP protocol is used for many modern applications, like most DirectX games, as well as for various Windows Messenger features like remote assistance, application sharing, file transfer, voice, and video from behind a firewall.

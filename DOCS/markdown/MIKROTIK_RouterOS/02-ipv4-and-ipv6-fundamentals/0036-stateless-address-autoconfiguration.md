## Stateless address autoconfiguration 

There are several types of autoconfiguration: 

stateless - address configuration is done by receiving Router Advertisement messages. These messages include stateless address prefixes and require that host is not using stateful address configuration protocol. 

- stateful - address configuration is done by using the stateful address configuration protocol (DHCPv6). The stateful protocol is used if RA messages do not include address prefixes. 

both - RA messages include stateless address prefixes and require that hosts use a stateful address configuration protocol. 

A highly useful feature of IPv6 is the ability to automatically configure itself without the use of a stateful configuration protocol like DHCP ( See example). 

**==> picture [13 x 13] intentionally omitted <==**

Address autoconfiguration can only be performed on multicast-capable interfaces. 

It is called stateless address autoconfiguration since there is no need to manage the state on the router side. It is a very simple, robust, and effective autoconfiguration mechanism. 

RouterOS uses RADVD to periodically advertise information about the link to all nodes on the same link. The information is carried by ICMPv6 "router advertisement" packet, and includes the following fields: 

IPv6 subnet prefix 

Default router link-local address 

Other parameters that may be optional: are link MTU, default hop limit, and router lifetime. 

Then host catches the advertisement, and configures the global IPv6 address and the default router. Global IPv6 address is generated from the advertised subnet prefix and EUI-64 interface identifier. 

170 

Optionally, the host can ask for an advertisement from the router by sending an ICMPv6 "router solicitation" packet. On Linux rtsol utility transmits the router solicitation packet. If you are running a mobile node, you may want to transmit router solicitations periodically.

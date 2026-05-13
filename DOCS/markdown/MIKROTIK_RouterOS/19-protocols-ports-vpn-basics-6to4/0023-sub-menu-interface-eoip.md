## Sub-menu: `/interface eoip` 

Ethernet over IP (EoIP) Tunneling is a MikroTik RouterOS protocol based on GRE RFC 1701 that creates an Ethernet tunnel between two routers on top of an IP connection. The EoIP tunnel may run over IPIP tunnel, PPTP tunnel, or any other connection capable of transporting IP. When the bridging function of the router is enabled, all Ethernet traffic (all Ethernet protocols) will be bridged just as if there where a physical Ethernet interface and cable between the two routers (with bridging enabled). This protocol makes multiple network schemes possible. 

Network setups with EoIP interfaces: 

Possibility to bridge LANs over the Internet Possibility to bridge LANs over encrypted tunnels Possibility to bridge LANs over 802.11b 'ad-hoc' wireless networks 

The EoIP protocol encapsulates Ethernet frames in GRE (IP protocol number 47) packets (just like PPTP) and sends them to the remote side of the EoIP tunnel.

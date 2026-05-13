## Masquerade 

Firewall NAT `action=masquerade` is a unique subversion of `action=srcnat` , it was designed for specific use in situations when public IP can randomly change, for example, DHCP server changes assigned IP or PPPoE tunnel after disconnect gets a different IP, in short - when public IP is dynamic 

```
/ip firewall nat add chain=srcnat src-address=10.0.0.0/24 action=masquerade out-interface=WAN
```

648 

Every time when interface disconnects and/or its IP address changes, the router will clear all masqueraded connection tracking entries related to the interface, this way improving system recovery time after public IP change. If `srcnat` is used instead of `masquerade` , connection tracking entries remain and connections can simply resume after a link failure. 

Unfortunately, this can lead to some issues with unstable links when the connection gets routed over different links after the primary link goes down. In such a scenario following things can happen: 

on disconnect, all related connection tracking entries are purged; 

- next packet from every purged (previously masqueraded) connection will come into the firewall as new, and, if a primary interface is not back, a packet will be routed out via an alternative route (if you have any) thus creating a new masqueraded connection; 

- the primary link comes back, routing is restored over the primary link, so packets that belong to existing connections are sent over the primary interface without being masqueraded, that way leaking local IPs to a public network. 

To work around this situation blackhole route can be created as an alternative to the route that might disappear on disconnect. 

Hosts behind a NAT-enabled router do not have true end-to-end connectivity. Therefore some Internet protocols might not work in scenarios with NAT. Services that require the initiation of TCP connection from outside the private network or stateless protocols such as UDP, can be disrupted. 

To overcome these limitations RouterOS includes a number of so-called NAT helpers, that enable NAT traversal for various protocols. When `action=src nat` is used instead, connection tracking entries remain and connections can simply resume. 

**==> picture [13 x 13] intentionally omitted <==**

Though Source NAT and masquerading perform the same fundamental function: mapping one address space into another one, the details differ slightly. Most noticeably, masquerading chooses the source IP address for the outbound packet from the IP bound to the interface through which the packet will exit.

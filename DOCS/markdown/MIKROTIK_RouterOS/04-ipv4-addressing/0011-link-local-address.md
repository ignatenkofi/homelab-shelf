## Link-local Address 

A link-local address is required on every IPv6-enabled interface, applications may rely on the existence of a link-local address even when there is no IPv6 routing, that is why the link-local address is generated automatically for every active interface using its interface identifier (calculated EUI-64 from MAC address if present). The address prefix is always FE80::/64 and IPv6 router never forwards link-local traffic beyond the link. 

These addresses are comparable to the auto-configuration addresses 169.254.0.0/16 of IPv4. 

A link-local address is also required for IPv6 Neighbor Discovery processes. 

**==> picture [13 x 13] intentionally omitted <==**

If the interface is set as a bridge port, an interface-specific link-local address is removed leaving only the bridge link-local address

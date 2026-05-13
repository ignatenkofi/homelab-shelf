## `/ip/firewall/mangle` 

```
add action=add-src-to-address-list chain=prerouting address-list=WAN2_WireGuard_clients address-list-timeout=1m
dst-port=13231 in-interface=ether2 protocol=udp comment="add source IP address of WAN2 incoming WireGuard
traffic to address list"
```

```
add action=mark-connection chain=output dst-address-list=WAN2_WireGuard_clients dst-port=13231 new-connection-
mark=wan2 protocol=udp comment="mark WireGuard connection to the client peer by checking destination address
from the address list"
```

```
add action=mark-routing chain=output connection-mark=wan2 dst-port=13231 new-routing-mark=wan2 protocol=udp
comment="ensure that WireGuard traffic uses routing table associated with the WAN2 incoming interface"
add action=add-src-to-address-list chain=prerouting address-list=WAN3_WireGuard_clients address-list-timeout=1m
dst-port=13231 in-interface=ether3 protocol=udp comment="add source IP address of WAN3 incoming WireGuard
traffic to address list"
```

```
add action=mark-connection chain=output dst-address-list=WAN3_WireGuard_clients dst-port=13231 new-connection-
mark=wan3 protocol=udp comment="mark WireGuard connection to the client peer by checking destination address
from the address list"
```

```
add action=mark-routing chain=output connection-mark=wan3 dst-port=13231 new-routing-mark=wan3 protocol=udp
comment="ensure that WireGuard traffic uses routing table associated with the WAN3 incoming interface"
```

## `/ip/firewall/nat` 

```
add action=masquerade chain=srcnat log=yes out-interface=ether2 comment="ensure that packet has source IP of
WAN2 interface"
```

```
add action=masquerade chain=srcnat log=yes out-interface=ether3 comment="ensure that packet has source IP of
WAN3 interface"
```

First mangle rule is used to catch the source IP address by matching destination port of incoming WireGuard handshake and add it to the list which further will be used as a way to mark outgoing WireGuard handshake. Timeout is used to ensure that in the future same source IP address can establish WireGuard tunnel using different WAN interface. 

Second mangle rule marks connections which is further used to mark routing and also ensures that mark stays on connection after IP address is gone from the address list and tunnel is established. 

Third mangle rule is used to force the packet to use the correct routing table for the second WAN interface. 

Last NAT rule is required to ensure that packet is sent out with the correct source IP, as it is not adjusted by the mangle rules and if not implemented packet could have different source IP depending on the setup. 

As you can see rules are duplicated for WAN3, to ensure that WAN3 interface is also usable with WireGuard. 

This rule set, ensures that WireGuard tunnel is established on the interface that recived the incoming handshake. 

1283

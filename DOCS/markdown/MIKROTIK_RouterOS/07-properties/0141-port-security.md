## Port Security 

It is possible to limit allowed MAC addresses on a single switch port. For example, to allow 64:D1:54:81:EF:8E MAC address on a switch port, start by switching multiple ports together, in this example 64:D1:54:81:EF:8E is going to be located behind ether1 . 

Create an ACL rule to allow the given MAC address and drop all other traffic on ether1 (for ingress traffic): 

```
/interface ethernet switch rule
add ports=ether1 src-mac-address=64:D1:54:81:EF:8E/FF:FF:FF:FF:FF:FF switch=switch1
add new-dst-ports="" ports=ether1 switch=switch1
```

Egress traffic can still contain information that should not reach devices with unknown MAC addresses. Assuming the ports are switched, disable MAC learning and disable unknown unicast flooding on ether1 : 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1 hw=yes learn=no unknown-unicast-flood=no
add bridge=bridge1 interface=ether2 hw=yes
```

With MAC learning disabled, you need to add a static hosts entry for 64:D1:54:81:EF:8E (for egress traffic): 

```
/interface bridge host
add bridge=bridge1 interface=ether1 mac-address=64:D1:54:81:EF:8E
```

**==> picture [13 x 13] intentionally omitted <==**

Broadcast and multicast traffic will still be sent out from ether1 . You can use the `broadcast-flood` and `unknown-multicast-flood` param eters to prevent it. Note that some solutions might depend on these settings, such as streaming protocols and DHCP. 

408

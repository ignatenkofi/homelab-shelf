## Enabling dynamic source NAT rule generation 

If we look at the generated dynamic policies, we see that only traffic with a specific (received by mode config) source address will be sent through the tunnel. But a router in most cases will need to route a specific device or network through the tunnel. In such case, we can use source NAT to change the source address of packets to match the mode config address. Since the mode config address is dynamic, it is impossible to create a static source NAT rule. In RouterOS, it is possible to generate dynamic source NAT rules for mode config clients. 

1216 

**==> picture [504 x 210] intentionally omitted <==**

For example, we have a local network 192.168.88.0/24 behind the router and we want all traffic from this network to be sent over the tunnel. First of all, we have to make a new IP/Firewall/Address list which consists of our local network 

```
/ip firewall address-list
add address=192.168.88.0/24 list=local
```

When it is done, we can assign the newly created IP/Firewall/Address list to the mode config configuration. 

```
/ip ipsec mode-config
set [ find name=ike2-rw ] src-address-list=local
```

Verify correct source NAT rule is dynamically generated when the tunnel is established. 

```
[admin@MikroTik] > /ip firewall nat print
Flags: X - disabled, I - invalid, D - dynamic
0 D ;;; ipsec mode-config
```

```
chain=srcnat action=src-nat to-addresses=192.168.77.254 src-address-list=local dst-address-list=!local
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure the dynamic mode config address is not a part of a local network.

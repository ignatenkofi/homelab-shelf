## Configuration Example 

753 

**==> picture [505 x 499] intentionally omitted <==**

Let's consider that we already have this basic home setup illustrated above. 

Before enabling PMP-NAT we need to masquerade outgoing LAN packets. 

```
/ip firewall nat
add action=masquerade chain=srcnat out-interface=ether1
```

Now we can enable PMP and add internal, external interfaces: 

```
/ip nat-pmp set enable=yes
```

```
/ip nat-pmp interfaces> add interface=ether1 type=external disabled=no
```

```
/ip nat-pmp interfaces> add interface=ether2 type=internal disabled=no
```

When the client from the internal interface side sends PMP request, dynamic NAT rules are created on the router: 

754 

```
[admin@MikroTik] > ip firewall nat print
Flags: X - disabled, I - invalid, D - dynamic
```

```
0 chain=srcnat action=masquerade out-interface=ether1
```

```
1 D ;;; nat-pmp 192.168.88.10: ApplicationX
chain=dstnat action=dst-nat to-addresses=192.168.88.10 to-ports=55000 protocol=tcp
dst-address=10.0.0.1 in-interface=ether1 dst-port=55000
```

```
2 D ;;; nat-pmp 192.168.88.10: ApplicationX
chain=dstnat action=dst-nat to-addresses=192.168.88.10 to-ports=55000 protocol=udp
dst-address=10.0.0.1 in-interface=ether1 dst-port=55000
```

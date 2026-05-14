## Classless Route 

A classless route adds a specified route in the clients routing table. In our example, it will add 

dst-address=160.0.0.0/24 gateway=10.1.101.1 

dst-address=0.0.0.0/0 gateway=10.1.101.1 

According to RFC 3442: The first part is the netmask ("18" = netmask /24). Second part is significant part of destination network ("A00000" = 160.0.0). Third part is IP address of gateway ("0A016501" = 10.1.101.1). Then There are parts of the default route, destination netmask (0x00 = 0.0.0.0/0) followed by default route (0x0A016501 = 10.1.101.1) 

```
/ip dhcp-server option
add code=121 name=classless value=0x18A000000A016501000A016501
/ip dhcp-server network
set 0 dhcp-option=classless
```

Result: 

901 

```
[admin@MikroTik] /ip route> print
Flags: X - disabled, A - active, D - dynamic, C - connect, S - static, r - rip, b - bgp, o - ospf,
m - mme, B - blackhole, U - unreachable, P - prohibit
 #      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
 0 ADS  0.0.0.0/0                          10.1.101.1         0
 1 ADS  160.0.0.0/24                       10.1.101.1         0
```

A much more robust way would be to use built-in variables, the previous example can be rewritten as: 

```
/ip dhcp-server option
```

```
add name=classless code=121 value="0x18A00000\$(NETWORK_GATEWAY)0x00\$(NETWORK_GATEWAY)"
```

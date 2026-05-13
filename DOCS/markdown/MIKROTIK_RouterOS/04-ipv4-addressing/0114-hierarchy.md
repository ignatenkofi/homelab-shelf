## Hierarchy 

The console allows the configuration of the router's settings using text commands. Since there is a lot of available commands, they are split into groups organized in a way of hierarchical menu levels. The name of a menu level reflects the configuration information accessible in the relevant section. 

For example, you can issue the `/ip route print` command: 

```
[admin@MikroTik] > /ip route print
Flags: D - dynamic; X - disabled, I - inactive, A - active;
C - connect, S - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn
 #     DST-ADDRESS        GATEWAY            DISTANCE
 0  XS 4.4.4.4            10.155.101.1
   D o 0.0.0.0/0          10.155.101.1            110
 1  AS 0.0.0.0/0          10.155.101.1              1
   D b 1.0.4.0/24         10.155.101.1             20
   D b 1.0.4.0/24         10.155.101.1             20
   DAb 1.0.4.0/24         10.155.101.1             20
[admin@MikroTik] >
```

Instead of typing `/ip route` path before each command, the path can be typed only once to move into this particular branch of the menu hierarchy. Thus, the example above could also be executed like this: 

```
[admin@MikroTik] > /ip route
[admin@MikroTik] /ip/route> print
Flags: D - dynamic; X - disabled, I - inactive, A - active;
C - connect, S - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn
 #     DST-ADDRESS        GATEWAY            DISTANCE
 0  XS 4.4.4.4            10.155.101.1
   D o 0.0.0.0/0          10.155.101.1            110
 1  AS 0.0.0.0/0          10.155.101.1              1
   D b 1.0.4.0/24         10.155.101.1             20
   D b 1.0.4.0/24         10.155.101.1             20
   DAb 1.0.4.0/24         10.155.101.1             20
[admin@MikroTik] >
```

Each word in the path can be separated by space (as in the example above) or by "/" 

214 

```
[admin@MikroTik] > /ip/route/
[admin@MikroTik] /ip/route> print
Flags: D - dynamic; X - disabled, I - inactive, A - active;
C - connect, S - static, r - rip, b - bgp, o - ospf, d - dhcp, v - vpn
 #     DST-ADDRESS        GATEWAY            DISTANCE
 0  XS 4.4.4.4            10.155.101.1
   D o 0.0.0.0/0          10.155.101.1            110
 1  AS 0.0.0.0/0          10.155.101.1              1
   D b 1.0.4.0/24         10.155.101.1             20
   D b 1.0.4.0/24         10.155.101.1             20
   DAb 1.0.4.0/24         10.155.101.1             20
[admin@MikroTik] >
```

Notice that the prompt changes in order to reflect where you are located in the menu hierarchy at the moment. To move to the top level again, type " / " 

```
[admin@MikroTik] > ip route
[admin@MikroTik] /ip/route> /
[admin@MikroTik] >
```

To move up one command level, type " .. " 

```
[admin@MikroTik] /ip/route> ..
[admin@MikroTik] /ip>
```

You can also use / and  to execute commands from other menu levels without changing the current level: .. 

```
[admin@MikroTik] /ip/route> /ping 10.0.0.1
10.0.0.1 ping timeout
2 packets transmitted, 0 packets received, 100% packet loss
[admin@MikroTik] /ip/firewall/nat> .. service-port print
Flags: X - disabled, I - invalid
#   NAME                                                                PORTS
0   ftp                                                                 21
1   tftp                                                                69
2   irc                                                                 6667
3   h323
4   sip
5   pptp
[admin@MikroTik] /ip/firewall/nat>
```

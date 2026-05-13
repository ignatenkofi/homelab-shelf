## Example 

For example, you can issue the /ip route print command: 

```
[admin@MikroTik] > ip route print
Flags: X - disabled, A - active, D - dynamic,
C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme,
B - blackhole, U - unreachable, P - prohibit
 # DST-ADDRESS PREF-SRC G GATEWAY DIS INTE...
0 A S 0.0.0.0/0 r 10.0.3.1 1 bridge1
1 ADC 1.0.1.0/24 1.0.1.1 0 bridge1
2 ADC 1.0.2.0/24 1.0.2.1 0 ether3
3 ADC 10.0.3.0/24 10.0.3.144 0 bridge1
4 ADC 10.10.10.0/24 10.10.10.1 0 wlan1
[admin@MikroTik] >
```

Instead of typing / ip route path before each command, the path can be typed only once to move into this particular branch of the menu hierarchy. Thus, the example above could also be executed like this: 

```
[admin@MikroTik] > ip route
[admin@MikroTik] ip route> print
Flags: X - disabled, A - active, D - dynamic,
C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme,
 B - blackhole, U - unreachable, P - prohibit #
DST-ADDRESS PREF-SRC G GATEWAY DIS INTE...
0 A S 0.0.0.0/0 r 10.0.3.1 1 bridge1
1 ADC 1.0.1.0/24 1.0.1.1 0 bridge1
2 ADC 1.0.2.0/24 1.0.2.1 0 ether3
3 ADC 10.0.3.0/24 10.0.3.144 0 bridge1
4 ADC 10.10.10.0/24 10.10.10.1 0 wlan1 [
admin@MikroTik] ip route>
```

72 

Notice that the prompt changes to reflect where you are located in the menu hierarchy at the moment. To move to the top level again, type " / " 

```
[admin@MikroTik] > ip route
[admin@MikroTik] ip route> /
[admin@MikroTik] >
```

To move up one command level, type " .. 

" 

```
[admin@MikroTik] ip route> ..
[admin@MikroTik] ip>
```

You can also use / and .. to execute commands from other menu levels without changing the current level: 

```
[admin@MikroTik] ip route> /ping 10.0.0.1
10.0.0.1 ping timeout
2 packets transmitted, 0 packets received, 100% packet loss
[admin@MikroTik] ip firewall nat> .. service-port print
Flags: X - disabled, I - invalid
# NAME PORTS
0 ftp 21
1 tftp 69
2 irc 6667
3 h323
4 sip
5 pptp
[admin@MikroTik] ip firewall nat>
```

## Configuration Example 

**==> picture [505 x 226] intentionally omitted <==**

ISP gives to its client two physical links (DSL lines) 1Mbps each. To get aggregated 2Mbps pipe we have to set up MLPPP. Consider ISP router is preconfigured to support MLPPP. 

Configuration on router (R1) is: 

```
/interface pppoe-client
```

```
   add service-name=ISP interface=ether1,ether2 user=xxx password=yyy disabled=no \
   add-default-route=yes use-peer-dns=yes
```

```
[admin@RB800] /interface pppoe-client> print
Flags: X - disabled, R - running
```

```
 0    name="pppoe-out1" max-mtu=1480 max-mru=1480 mrru=disabled interface=ether1,ether2
      user="xxx" password="yyy" profile=default service-name="ISP" ac-name="" add-default-route=yes
      dial-on-demand=no use-peer-dns=yes allow=pap,chap,mschap1,mschap2
```

Now when PPPoE client is connected we can set up rest of configuration, local network address, enable DNS requests, set up masquerade and firewall 

```
/ip address add address=192.168.88.1/24 interface=local
```

```
/ip dns set allow-remote-request=yes
```

```
/ip firewall nat
add chain=src-nat action=masquerade out-interface=pppoe-out1
/ip firewall filter
add chain=input connection-state=invalid action=drop \
        comment="Drop Invalid connections"
add chain=input connection-state=established action=accept \
        comment="Allow Established connections"
add chain=input protocol=icmp action=accept \
        comment="Allow ICMP"
add chain=input src-address=192.168.88.0/24 action=accept \
        in-interface=!pppoe-out1
add chain=input action=drop comment="Drop everything else"
```

For more advanced router and customer protection check firewall examples 

. 

1259

## Firewall Setup 

```
/ip address
```

```
add address=192.168.88.1/24 interface=ether1
add address=10.0.0.17/24 interface=sfp-sfpplus16
```

```
/ip route
```

```
add gateway=10.0.0.1
```

```
/ip firewall filter
```

```
add action=fasttrack-connection chain=forward connection-state=established,related hw-offload=yes
add action=accept chain=forward connection-state=established,related
```

```
/ip firewall nat
```

```
add action=masquerade chain=srcnat out-interface-list=WAN
```

At this moment, all routing still is performed by the CPU. Enable hardware routing on the switch chip:

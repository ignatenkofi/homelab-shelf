## Set VLAN or WMM priority based on specific matchers 

It is possible to change the VLAN and WMM priorities based on specific matchers in IP mangle or bridge filter/nat rules. In this example, all outgoing ICMP packets will be sent with a VLAN or WMM priority using the IP mangle rule: 

```
/ip firewall mangle
```

```
add action=set-priority chain=output new-priority=2 protocol=icmp
```

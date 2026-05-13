## Set VLAN or WMM priority from DSCP 

In this example, the AP device will set WMM priority from DSCP when packets are routed through the wireless interface. 

```
/ip firewall mangle
```

```
add action=set-priority chain=forward new-priority=from-dscp out-interface=wlan2
```

**==> picture [13 x 13] intentionally omitted <==**

When packets are forwarded through a bridge, it is possible to pass packets through IP mangle rules with `use-ip-firewall=yes` under the bridge settings.

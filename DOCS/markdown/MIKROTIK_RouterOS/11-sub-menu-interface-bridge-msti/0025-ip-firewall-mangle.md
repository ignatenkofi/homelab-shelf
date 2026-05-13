## `/ip firewall mangle` 

```
add action=set-priority chain=prerouting in-interface=wlan2 new-priority=from-ingress
add action=change-dscp chain=prerouting in-interface=wlan2 new-dscp=from-priority
```

**==> picture [13 x 13] intentionally omitted <==**

When packets are forwarded through a bridge, it is possible to pass packets through IP mangle rules with `use-ip-firewall=yes` under the bridge settings.

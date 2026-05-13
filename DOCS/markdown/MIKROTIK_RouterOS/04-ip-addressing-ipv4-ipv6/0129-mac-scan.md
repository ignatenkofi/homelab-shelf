## MAC Scan 

Mac scan feature discovers all devices, which support MAC telnet protocol on the given network. The command requires you to select an interface that should be scanned: 

```
[admin@Sw_Denissm] > tool mac-scan interface=all
MAC-ADDRESS       ADDRESS                AGE
B8:69:F4:7F:F2:E7 192.168.69.1            26
2C:C8:1B:FD:F2:C3 192.168.69.3            56
```

In the example, above, all interfaces are chosen, and the scan will run infinitely unless stopped (by pressing "q"). 

You can also add a "duration" parameter that will dictate for how long the scan should go on: 

```
[admin@Sw_Denissm] > tool mac-scan interface=all duration=1
MAC-ADDRESS       ADDRESS                AGE
B8:69:F4:7F:F2:E7 192.168.69.1            48
2C:C8:1B:FD:F2:C3 192.168.69.3            17
```

In the example above, we set the "duration" parameter to 1 second.

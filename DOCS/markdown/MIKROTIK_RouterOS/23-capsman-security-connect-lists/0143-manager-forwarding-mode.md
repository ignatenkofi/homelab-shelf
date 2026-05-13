## Manager Forwarding Mode 

In this mode CAP sends all data received over wireless to CAPsMAN and only sends out over wireless, data received from CAPsMAN. CAPsMAN has full control over data forwarding including client-to-client forwarding. Wireless interface on CAP is disabled and does not participate in networking: 

```
...
```

```
1 X  ;;; managed by CAPsMAN
     ;;; channel: 5180/20-Ceee/ac, SSID: master, manager forwarding
     name="wlan2" mtu=1500 mac-address=00:03:7F:48:CC:07 arp=enabled
     interface-type=Atheros AR9888 mode=ap-bridge ssid="merlin"
...
```

Virtual-AP interfaces are also created as 'disabled' and do not take part in data forwarding on CAP.

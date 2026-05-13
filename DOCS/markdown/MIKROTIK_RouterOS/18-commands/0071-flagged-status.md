## Flagged status 

Along with the device-mode feature, RouterOS now can analyze the whole configuration at system startup, to determine if there are any signs of unauthorized access to your router. If suspicious configuration is detected, the suspicious configuration will be disabled and the flagged parameter will be set to "yes". The device has now a Flagged state and enforces certain limitations. 

1134 

```
[admin@MikroTik] > system/device-mode/print
     mode: advanced
  flagged: yes
  sniffer: no
  hotspot: no
```

If the system has this flagged status, the current configuration works, but it is not possible to perform the following actions: 

bandwidth-test, traffic-generator, sniffer, as well as configuration actions that enable or create new configuration entries (it will still be possible to disable or delete them) for the following programs: system scheduler, SOCKS proxy, pptp, l2tp, ipsec, proxy, smb. 

When performing the aforementioned actions while the router has the flagged state, you will receive an error message: 

```
[admin@MikroTik] > /tool sniffer/quick
```

```
failure: configuration flagged, check all router configuration for unauthorized changes and update device-mode
[admin@MikroTik] > /int l2tp-client/add connect-to=1.1.1.1 user=user
```

```
failure: configuration flagged, check all router configuration for unauthorized changes and update device-mode
```

To exit the flagged state, you must perform the command "/system/device-mode/update flagged=no". The system will ask to either press a button, or issue a hard reboot (cut power physically or do a hard reboot of the virtual machine). 

Important! Although the system has disabled any malicious looking rules, which triggered the flagged state, it is crucial to inspect all of your configuration for other unknown things, before exiting the flagged state. If your system has been flagged, assume that your system has been compromised and do a full audit of all settings before re-enabling the system for use. After completing the audit, change all the system passwords and upgrade to the latest RouterOS version. 

**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS version 7.17 device-mode restricts SwOS/RouterOS transition for dual-boot; in order to enable: system/device-mode /update routerboard=yes 

1135

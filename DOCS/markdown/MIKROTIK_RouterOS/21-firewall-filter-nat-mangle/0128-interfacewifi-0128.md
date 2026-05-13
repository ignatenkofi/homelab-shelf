## `/interface/wifi` 

```
add master-interface=wifi1 name=wifi1_owe configuration.ssid=MikroTik_OWE security.authentication-types=owe
security.owe-transition-interface=wifi1 configuration.hide-ssid=yes
```

```
set wifi1 configuration.country=Latvia configuration.ssid=MikroTik security.authentication-types="" security.
owe-transition-interface=wifi1_owe
```

```
enable wifi1,wifi1_owe
```

With such setting, the AP will broadcast two SSIDs →  visible " `MikroTik` " SSID, which should have "unecrypted" access (for legacy devices that do not support OWE), and hidden SSID " `MikroTik_OWE` ", which should have "OWE" security (non-password protected, but encrypted). The client devices will not see the hidden " `MikroTik_OWE` " SSID (in the client's WiFi list), however, the beacon packets of the visible " `MikroTik` " SSID, will advertise the link to the hidden " `MikroTik_OWE` " network instead, using the "OWE Transition mode" paramter (in the beacon packet). As a result, the client devices should prioritize connecting to the "OWE" network via `owe-transition-interface` setting. 

Client devices that support OWE will prefer the OWE interface. If you don't see any devices in your registration table that are associated with the regular open AP, you may want to move on from running a transition mode setup to a single OWE-encrypted interface:

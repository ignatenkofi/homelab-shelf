## `/interface wifi` 

```
add configuration.mode=ap .ssid=guest.ssid.2 disabled=no master-interface=wifi2 name=wifi3 security.
authentication-types=wpa2-psk .passphrase=guest.password
```

- `configuration.mode=ap` → ensures that it will act as an "access point" interface. 

- `ssid=guest.ssid2` → configures wireless network name (SSID), which the AP needs to broadcast. For "client roaming" to happen, use the exact same WiFi name from the router settings. 

- `master-interface=wifi2` → specify, which interface to "base" the "virtual" interface on (specify on-top of which interface to create it). `name=wifi3` → name the virtual interface. 

- `security.authentication-types=wpa2-psk` → select which authentication types to use. For "client roaming" to happen, use the exact same authentication type from the router settings. 

- `passphrase=guest.password` → sets password from the AP's WiFi network. For "client roaming" to happen, use the exact same password from the router settings. 

**==> picture [13 x 13] intentionally omitted <==**

The virtual interface will use the exact same frequency channel, which is used by the `master` interface. Wi-Fi frequency channel for this interface can not be changed.

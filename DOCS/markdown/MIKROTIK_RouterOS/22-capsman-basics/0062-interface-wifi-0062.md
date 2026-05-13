## `/interface wifi` 

```
set [ find default-name=wifi1 ] configuration.mode=ap configuration.country=Latvia .ssid=router.ssid.5
disabled=no security.authentication-types=wpa2-psk .passphrase=router.password
```

- `configuration.mode=ap` → configures interface to work in "access point" mode. 

- `configuration.country=Latvia` → select your actual country, so that you do not break any regulations (your country "laws"). Different country profiles have different allowed output powers per different frequency ranges. 

- `ssid=router.ssid5` → configures wireless network name (SSID), which the repeater needs to re-broadcast. It can be the same network name as the main router uses, or it can be a different name. For testing, better use a "unique" name so you can differentiate networks. For "client roaming" to happen, use the exact same WiFi name from the router settings. 

- `security.authentication-types=wpa2-psk` → select which authentication types to use. For "client roaming" to happen, use the exact same authentication type from the router settings. 

- `passphrase=router.password` → sets password from the repeaters WiFi network. For "client roaming" to happen, use the exact same password from the router settings.

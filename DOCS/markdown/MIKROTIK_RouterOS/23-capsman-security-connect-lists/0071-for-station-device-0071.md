## For Station device - 

Choose the same SSID, Password, frequency as the bridge device and choose station-bridge mode option that will act as a station for the setup, please see the example. 

Enable W60G interface after required parameters have been set. 

```
[admin@MikroTik] > /interface wireless security-profiles set [ find default=yes ] supplicant-
identity=MikroTik authentication-types=wpa2-psk mode=dynamic-keys wpa2-pre-shared-key=choosepassword
[admin@MikroTik] > /interface wireless set wlan1 frequency=auto scan-list=default installation=outdoor
mode=station-bridge ssid=MikroTik1 channel-width=20/40/80mhz-Ceee wireless-protocol=any security-
profile=default band=5ghz-a/n/ac
[admin@MikroTik] > /interface wireless enable wlan1
```

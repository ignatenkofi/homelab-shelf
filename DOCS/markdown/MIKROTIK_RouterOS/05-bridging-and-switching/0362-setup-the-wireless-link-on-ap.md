## Setup the Wireless link on AP : 

```
/interface wireless security-profiles
```

```
add authentication-types=wpa2-psk mode=dynamic-keys name=wlan_sec wpa2-pre-shared-key=use_a_long_password_here
/interface wireless
```

```
set wlan1 band=5ghz-a/n/ac channel-width=20/40/80mhz-Ceee disabled=no mode=bridge scan-list=5180 security-
profile=wlan_sec ssid=ptp_test
```
